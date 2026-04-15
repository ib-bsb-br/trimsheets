# Dimensional Modeling Constructs for TreeSheets

## Purpose
This document proposes ten practical constructs for modeling, teaching, and representing multi-dimensional information inside TreeSheets. The constructs are designed for recursive cell-and-grid documents in which each node may hold text, nested grids, or both.

## Scope Assumptions
- TreeSheets is treated as a hierarchical, recursively nestable information space.
- "Dimension" is interpreted broadly as an independent axis of description, analysis, navigation, or computation.
- Constructs are selected for utility across low-dimensional, high-dimensional, and effectively unbounded (infinite-feature) data contexts.

---

## Top 10 Constructs

### 1. Coordinate Tuple Grid (Canonical Axis Encoding)
**What it is**  
A compact grid where each row is one entity and each column is one explicit axis (dimension), analogous to an n-tuple.

**Why it is useful**  
- Gives a baseline representation of independent variables.
- Supports direct comparison and filtering.
- Acts as the interoperability bridge to CSV/JSON/table tools.

**TreeSheets pattern**  
- Parent cell: dataset name.
- Child grid: headers as dimensions (`x1`, `x2`, ..., `xn`).
- Optional nested cell in each row for notes, provenance, or formulas.

**Best for**  
Vector-space style modeling, parameter sweeps, feature tables, metrics dashboards.

---

### 2. Recursive Dimension Decomposition Tree (Axis Factorization)
**What it is**  
A top-down hierarchy that progressively splits a complex space into orthogonal or near-orthogonal subspaces.

**Why it is useful**  
- Makes high-dimensional sets cognitively tractable.
- Aligns with TreeSheets' native recursive structure.
- Separates strategic dimensions (top levels) from operational dimensions (deeper levels).

**TreeSheets pattern**  
- Root: domain/problem statement.
- Level 1: major dimensions.
- Level 2+: sub-dimensions, indicators, measures, data sources.

**Best for**  
Ontology design, requirements engineering, curriculum maps, multidomain knowledge systems.

---

### 3. Dimensional Lattice / Cross-Classification Matrix
**What it is**  
A 2D matrix whose row and column dimensions define cells, with each cell optionally containing a nested subgrid for additional dimensions.

**Why it is useful**  
- Encodes interactions between dimensions, not only isolated values.
- Scales by recursive nesting when dimensions exceed two.
- Works as a didactic bridge from 2D intuition to nD structure.

**TreeSheets pattern**  
- Outer matrix: two dominant axes.
- Each intersection cell: nested mini-grid with secondary axes and local evidence.

**Best for**  
Risk matrices, competency-by-context maps, strategy canvases, scenario analysis.

---

### 4. Multi-Resolution Zoom Stack (Scale Dimension)
**What it is**  
A representation where the same entity is described at multiple granularities (overview, mid-level, detailed).

**Why it is useful**  
- Adds "resolution" as an explicit dimension.
- Supports didactic progression from simple to complex.
- Reduces overload by staged disclosure.

**TreeSheets pattern**  
- Parent cell contains executive summary.
- Nested child grids provide increasingly fine-grained decompositions.
- Each level preserves trace links to parent abstractions.

**Best for**  
Technical documentation, system architecture, pedagogy, progressive analytics.

---

### 5. Temporal Layering Grid (Time as a First-Class Dimension)
**What it is**  
A structure that versions the same dimensional model across time slices (t0, t1, ... tn).

**Why it is useful**  
- Distinguishes state vs change.
- Enables trajectory analysis and event causality.
- Supports audits and retrospective learning.

**TreeSheets pattern**  
- One timeline column or row for periods.
- Per period: nested snapshot grid of all non-temporal dimensions.
- Delta cells summarize changes from previous snapshot.

**Best for**  
Roadmaps, incident timelines, longitudinal research, product evolution tracking.

---

### 6. Observer/Context Frames (Relativized Coordinates)
**What it is**  
Parallel representations of the same object under different observer roles, environments, or assumptions.

**Why it is useful**  
- Mirrors frame-dependent interpretation (analogous to coordinate transforms).
- Prevents false consensus caused by single-view models.
- Clarifies invariants vs context-dependent attributes.

**TreeSheets pattern**  
- Top-level split by observer frame (e.g., user, engineer, manager, regulator).
- Shared invariant block plus frame-specific derived dimensions.

**Best for**  
UX/system alignment, policy analysis, stakeholder negotiation, safety-critical documentation.

---

### 7. Constraint Manifold Blocks (Feasible Region Encoding)
**What it is**  
A construct that stores dimensions together with rules that define valid combinations.

**Why it is useful**  
- Captures not only data points but admissible space.
- Reduces ambiguity in decision support.
- Provides a didactic path from raw dimensions to structured solution spaces.

**TreeSheets pattern**  
- Grid of variables and domains.
- Adjacent nested cells for constraints (`if`, inequalities, dependency rules).
- Feasible/infeasible examples under each rule.

**Best for**  
Configuration systems, compliance modeling, optimization prep, design-space exploration.

---

### 8. Basis-and-Projection Views (Dimension Reduction for Understanding)
**What it is**  
A pair of structures: one for selected basis dimensions, another for projections/aggregations onto lower-dimensional views.

**Why it is useful**  
- Supports explainability when raw dimensionality is large.
- Preserves relationship between full model and simplified view.
- Enables didactic "from projection back to source" navigation.

**TreeSheets pattern**  
- Full-space grid (all dimensions).
- Projection grids (2D/3D slices, grouped summaries).
- Explicit mapping cells listing which dimensions were dropped or aggregated.

**Best for**  
Business intelligence, feature engineering documentation, classroom demonstrations.

---

### 9. Hypergraph Relation Cells (Beyond Pairwise Links)
**What it is**  
A relation model where one link can connect many entities and many dimensions simultaneously.

**Why it is useful**  
- Avoids distortion from forcing complex relations into binary edges.
- Fits domains where events involve multiple actors, resources, times, and states.
- Integrates naturally with nested records per relation.

**TreeSheets pattern**  
- One relation cell per event/transaction.
- Nested list of participants, roles, attributes, and contextual dimensions.
- Back-reference indices to entity cells.

**Best for**  
Knowledge graphs, provenance tracking, legal/forensic case structures, complex workflows.

---

### 10. Infinite-Feature Dictionary with Progressive Activation
**What it is**  
A sparse, extensible dimension dictionary where potential axes are unbounded, but only activated dimensions are instantiated per node.

**Why it is useful**  
- Handles effectively infinite-dimensional contexts (function-space-like feature sets, open-world annotation).
- Keeps documents lightweight by sparsity.
- Supports continuous schema evolution without breaking existing structures.

**TreeSheets pattern**  
- Global dictionary sheet of possible dimensions (name, type, semantics, units, validation).
- Entity sheets activate only relevant keys.
- Versioned dictionary changes plus migration notes.

**Best for**  
Research notebooks, open-ended taxonomies, AI feature repositories, evolving knowledge bases.

---

## Recommended Teaching Sequence (Didactic Path)
1. Coordinate Tuple Grid  
2. Cross-Classification Matrix  
3. Recursive Decomposition Tree  
4. Temporal Layering  
5. Observer Frames  
6. Constraint Manifold  
7. Basis-and-Projection Views  
8. Hypergraph Relations  
9. Multi-Resolution Zoom Stack  
10. Infinite-Feature Dictionary

This sequence starts with intuitive Euclidean/tabular thinking and progressively introduces relational, temporal, contextual, constrained, and high-dimensional abstractions.

## Practical Selection Heuristic
- If the goal is **measurement and comparability**: start with Tuple Grid.
- If the goal is **interaction effects**: use Cross-Classification Matrix.
- If the goal is **knowledge organization**: use Recursive Decomposition.
- If the goal is **change over time**: use Temporal Layering.
- If the goal is **multi-stakeholder truth alignment**: use Observer Frames.
- If the goal is **decision validity**: use Constraint Manifold.
- If the goal is **explainability under high dimensionality**: use Basis-and-Projection.
- If the goal is **event complexity**: use Hypergraph Relation Cells.
- If the goal is **pedagogical zooming**: use Multi-Resolution Stack.
- If the goal is **open-world extensibility**: use Infinite-Feature Dictionary.
