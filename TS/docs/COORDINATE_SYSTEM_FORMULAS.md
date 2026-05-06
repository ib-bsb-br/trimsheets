# Coordinate System Formulas (Cell ↔ Grid ↔ Parent ↔ Absolute)

This note formalizes the coordinate relations used by TreeSheets cells and grids.

## 1) Cell-local coordinates to parent-grid coordinates

For a cell `c` inside a parent grid `g`, the layout stores the cell anchor in parent-grid space as:

- `c.ox`: x-offset of cell origin inside `g`
- `c.oy`: y-offset of cell origin inside `g`

If `(u, v)` is a point in the cell's **local** coordinate system (`0 <= u < c.sx`, `0 <= v < c.sy`), then the same point in **parent-grid** coordinates is:

- `x_g = c.ox + u`
- `y_g = c.oy + v`

At the cell-origin (`u = 0, v = 0`):

- `origin_in_parent_grid(c) = (c.ox, c.oy)`

## 2) Cell-local coordinates to parent-cell coordinates

A grid is rendered inside its owning (parent) cell. Therefore, moving from cell-local to parent-cell coordinates is the same additive transform used by `GetX/GetY` recursion:

- `x_parent_cell = c.ox + u + x_parent_origin`
- `y_parent_cell = c.oy + v + y_parent_origin`

where `(x_parent_origin, y_parent_origin)` is the parent cell's origin in the next enclosing space.

For immediate parent-cell space (with parent origin as zero), this collapses to:

- `x_parent_cell = c.ox + u`
- `y_parent_cell = c.oy + v`

## 3) Cell-local coordinates to absolute canvas coordinates

TreeSheets computes absolute coordinates recursively:

- `GetX(c) = c.ox + (parent(c) ? GetX(parent(c)) : hierarchysize)`
- `GetY(c) = c.oy + (parent(c) ? GetY(parent(c)) : hierarchysize)`

So a local point `(u, v)` in cell `c` maps to absolute/canvas coordinates:

- `X_abs = GetX(c) + u`
- `Y_abs = GetY(c) + v`

Expanded over ancestors `a_0 = c, a_1 = parent(c), ..., a_k = root_cell`:

- `X_abs = hierarchysize + sum_{i=0..k} a_i.ox + u`
- `Y_abs = hierarchysize + sum_{i=0..k} a_i.oy + v`

## 4) Grid index formulas (local and absolute-by-path)

### 4.1 Local linear index in one grid

Each grid stores cells in row-major order:

- `index_local(x, y) = x + y * xs`

with `0 <= x < xs`, `0 <= y < ys`.

### 4.2 Hierarchical absolute index (path form)

Because TreeSheets is hierarchical, there is no single built-in flat global index across the full document tree. A canonical absolute identifier is a path of local indices from root to target:

- `path(c) = [ i_0, i_1, ..., i_d ]`
- `i_j = x_j + y_j * xs_j` in ancestor grid `j`

This path is stable relative to structure and is the recommended "absolute" identifier in a nested grid tree.

### 4.3 Optional scalarization of path (mixed radix)

If a single integer is required, define per-level radix `R_j = xs_j * ys_j` and encode:

- `I = i_0 + i_1 * R_0 + i_2 * (R_0 R_1) + ... + i_d * prod_{m=0..d-1} R_m`

Decode with repeated division/modulo by radices `R_j`.

## 5) Practical summary

- **Cell local → parent grid:** add `(ox, oy)`.
- **Cell local → parent cell:** same additive offsets (the grid lives in parent-cell content space).
- **Cell local → absolute canvas:** recursively add ancestor offsets plus `hierarchysize` base margin.
- **Grid coordinates → local linear index:** `x + y * xs`.
- **Tree-wide absolute identity:** use index-path (or mixed-radix scalarization if needed).
