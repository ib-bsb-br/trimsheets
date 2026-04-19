# Mapping TreeSheets Recursive Multi-Array Structures to Kinship Degrees

## Purpose

This document defines a deterministic method for converting recursive, nested TreeSheets-like arrays into kinship-degree labels (self, parent, grandparent, sibling, cousin-like relations, and descendants).

The method is designed for:

- Hierarchical spreadsheet imports/exports.
- Genealogy-style traversal of nested cell structures.
- Rule-based relationship labeling for scripts and integrations.

---

## 1) Data Model Assumptions

Treat a TreeSheets hierarchy as a rooted tree projected from nested arrays:

```text
Node = {
  id: string,
  label: string,
  children: Node[]
}
```

Equivalent multi-array form:

```text
[
  id,
  label,
  [ child_1, child_2, ... ]
]
```

Where each child has the same recursive shape.

---

## 2) Kinship Degree Definitions

Given two nodes `A` (reference) and `B` (target):

- **Degree 0**: `A == B` -> `self`
- **Ascendant degree n**: `B` is n levels above `A`
  - 1: parent
  - 2: grandparent
  - 3+: great^k-grandparent (k = n - 2)
- **Descendant degree n**: `B` is n levels below `A`
  - 1: child
  - 2: grandchild
  - 3+: great^k-grandchild (k = n - 2)
- **Collateral relation** (neither ancestor nor descendant):
  - Let `L = LCA(A, B)` (lowest common ancestor).
  - Let `u = distance(A, L)` and `v = distance(B, L)`.
  - **Collateral degree** = `u + v`.
  - Common label strategy:
    - `u = 1, v = 1` -> sibling
    - `u = 1, v = 2` -> niece/nephew (direction depends on perspective)
    - `u = 2, v = 1` -> aunt/uncle
    - `u >= 2 and v >= 2` -> cousin class with removal

Cousin normalization:

- `cousin_order = min(u, v) - 1`
- `removed = abs(u - v)`

Examples:

- `u=2, v=2` -> 1st cousin
- `u=2, v=3` -> 1st cousin once removed
- `u=3, v=3` -> 2nd cousin

---

## 3) Required Preprocessing

For efficient repeated queries, build indexes in one DFS pass:

- `parent[node_id]`
- `depth[node_id]` (root depth = 0)
- `children[node_id]`

Optional for high-volume queries:

- Binary lifting ancestor table for `O(log N)` LCA.
- Euler tour + RMQ for near-constant LCA queries.

---

## 4) Core Algorithm

### Step A: Normalize target pair

Input: `reference_id`, `target_id`

- If ids are equal -> return `self, degree=0`.

### Step B: Detect direct ancestor/descendant

- Walk parents from deeper node upward to match depths.
- If one node reaches the other:
  - classify as ascendant/descendant
  - degree = absolute depth delta.

### Step C: Compute collateral kinship

- Find `L = LCA(reference, target)`.
- Compute:
  - `u = depth[reference] - depth[L]`
  - `v = depth[target] - depth[L]`
- Return collateral degree `u + v`, plus a human-readable label.

---

## 5) Labeling Function (Deterministic)

Recommended output schema:

```json
{
  "relation_type": "self|ascendant|descendant|collateral",
  "degree": 0,
  "distance_up": 0,
  "distance_down": 0,
  "label": "self",
  "cousin_order": null,
  "removed": null
}
```

Label rules:

1. Self: `degree=0` -> `self`
2. Ascendant/Descendant:
   - 1 -> parent/child
   - 2 -> grandparent/grandchild
   - 3+ -> repeat `great-` prefix `degree-2` times
3. Collateral:
   - (1,1) -> sibling
   - (1,2) -> niece/nephew
   - (2,1) -> aunt/uncle
   - otherwise cousin formula.

---

## 6) Reference Pseudocode

```text
function map_kinship(reference_id, target_id, parent, depth):
    if reference_id == target_id:
        return { relation_type: "self", degree: 0, label: "self" }

    a = reference_id
    b = target_id

    # align depths
    while depth[a] > depth[b]:
        a = parent[a]
    while depth[b] > depth[a]:
        b = parent[b]

    # if ancestor/descendant direct after alignment checks
    if a == target_id:
        d = depth[reference_id] - depth[target_id]
        return ascendant_label(d)

    if b == reference_id:
        d = depth[target_id] - depth[reference_id]
        return descendant_label(d)

    # find LCA by synchronized climb
    x = a
    y = b
    while x != y:
        x = parent[x]
        y = parent[y]

    lca = x
    u = depth[reference_id] - depth[lca]
    v = depth[target_id] - depth[lca]

    if u == 1 and v == 1:
        return collateral("sibling", 2, u, v)
    if u == 1 and v == 2:
        return collateral("niece/nephew", 3, u, v)
    if u == 2 and v == 1:
        return collateral("aunt/uncle", 3, u, v)

    order = min(u, v) - 1
    removed = abs(u - v)
    label = cousin_label(order, removed)
    return collateral(label, u + v, u, v, order, removed)
```

---

## 7) Worked Example on Nested Arrays

Input structure:

```text
[
  "R", "Root", [
    ["A", "Alex", [
      ["C", "Casey", []],
      ["D", "Drew", []]
    ]],
    ["B", "Blair", [
      ["E", "Evan", [
        ["F", "Fin", []]
      ]]
    ]]
  ]
]
```

Relationships from `C` (Casey):

- to `A`: parent (degree 1)
- to `R`: grandparent (degree 2)
- to `D`: sibling (collateral degree 2)
- to `E`: 1st cousin (u=2, v=2, collateral degree 4)
- to `F`: 1st cousin once removed (u=2, v=3, collateral degree 5)

---

## 8) Complexity

- Preprocessing DFS: `O(N)` time, `O(N)` memory.
- Per query (simple parent climb): `O(H)` where `H` is tree height.
- Per query with LCA acceleration: `O(log N)` (binary lifting) after `O(N log N)` preprocessing.

---

## 9) Integration Notes for TreeSheets/Trimsheets

- The algorithm is agnostic to UI representation; it requires only parent-child adjacency.
- For exported table-like structures, normalize to explicit tree form before kinship mapping.
- If data can contain repeated labels, key strictly by unique node id, not displayed text.
- If multiple roots exist, create a synthetic super-root to preserve connected traversal semantics.

---

## 10) Edge Cases

- Missing parent pointer for non-root node: mark data invalid and skip kinship mapping until repaired.
- Cycles in nested data: reject input (kinship requires a DAG/tree, typically a strict tree).
- Duplicate ids: fail fast and request canonicalization.
- Orphan subtrees: either discard or attach to synthetic super-root with provenance metadata.

