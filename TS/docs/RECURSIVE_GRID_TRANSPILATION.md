# Recursive JSON-to-Grid Isomorphism for a TreeSheets-Style UI

## Goal
This document explains the phenomenon of transpiling a TreeSheets-like hierarchical data model into a recursive UI framework where visual geometry mirrors data topology.

## What the phenomenon consists of
The pattern is a **structural isomorphism** between:

1. **Data shape** (nested JSON nodes).
2. **Render shape** (recursive component tree).
3. **Layout shape** (CSS Grid track and placement model).

In practice, each node in the JSON graph is rendered by the same component:

- Scalar node -> render leaf content.
- Object/array node -> render container + recursively render children.

This creates a self-similar interface: every level uses the same rules, so deep branches and shallow branches coexist without introducing bespoke layout code for each depth.

## How it behaves

### 1) Recursive function (render engine)
A single component dispatches behavior by type:

- Primitive (`string`, `number`, `boolean`, `null`) => leaf cell.
- Composite (`array`, `object`) => grid container with child nodes.

Because recursion reproduces the input tree in the DOM, visual depth corresponds directly to data depth. Debugging and mental mapping improve because position and containment reflect structural truth.

### 2) Subgrid (alignment contract)
When available, `grid-template-columns: subgrid` lets descendants inherit ancestor column tracks. This prevents misalignment where each nested level would otherwise create incompatible local columns.

Effect:

- Deep descendants align to root coordinate tracks.
- Jagged branches still share a coherent column rhythm.
- The UI remains scan-friendly even when branch depths differ substantially.

### 3) Auto-placement (flow contract)
`grid-auto-flow: dense` backfills holes from irregular spans/branch lengths. Jagged data no longer creates permanently wasted space; the layout engine attempts tighter packing while respecting order constraints.

Effect:

- Better area utilization.
- Masonry-like compaction without JS geometry calculations.
- Reduced need for custom measuring/reflow code.

## Why this pattern emerged

### A) Cognitive depth externalization
Nested data is hard to reason about in text-only form. The pattern externalizes depth into visible containment, turning abstract hierarchy into a navigable spatial model.

### B) Performance partitioning
JS framework code is responsible mainly for semantic structure (what exists), while CSS performs geometric resolution (where it goes). This shifts expensive placement logic from userland JS to the browser's optimized layout engine.

### C) Jagged-structure tolerance
Traditional table models assume regular rows/columns. Hierarchical tools receive irregular, sparse, or variably deep data; grid + recursion adapts naturally because spans and intrinsic sizing can absorb irregularity.

## Data model implications for TreeSheets-style transpilation
A practical target schema usually includes:

- `id`: stable identity for updates.
- `type`: node category (`leaf`, `object`, `array`, `rich_text`, etc.).
- `children`: ordered nested nodes when composite.
- `meta`: optional style/behavior hints (collapsed, selected, formula, error state).
- `span`: optional hints for row/column spanning when needed.

The renderer can then remain generic:

1. Resolve node type.
2. Emit semantic wrapper.
3. Recurse through children.
4. Let CSS grid compute final placement.

## Behavior with jagged arrays
In jagged arrays, sibling branches can differ in child count and depth. Grid-based rendering handles this by allowing:

- Variable span occupancy.
- Dense backfill for empty gaps.
- Subgrid-aligned columns across depth boundaries.

The result is a "breathing" layout: compact where sparse, expanded where dense, while preserving parent-child topology.

## Key trade-offs

### Benefits
- Strong visual-data correspondence.
- Lower custom layout complexity.
- Better scalability for unpredictable hierarchy depth.
- Clearer debugging and inspection.

### Costs
- Subgrid support may vary by target browser baseline.
- Dense packing can visually reorder fill opportunities in ways that may surprise users if strict reading order is expected.
- Very deep recursion may require virtualization or incremental rendering strategies.

## Minimal implementation sketch (framework-agnostic)

1. Parse/import TreeSheets source structure into normalized JSON nodes.
2. Render with one recursive component.
3. Use CSS Grid at each composite node.
4. Apply `subgrid` where supported; provide fallback track definitions otherwise.
5. Enable `grid-auto-flow: dense` selectively (views where compaction is beneficial).
6. Add virtualization/collapse controls for deep or very large trees.

## Summary
The phenomenon is a **topology-preserving UI architecture**: recursive rendering guarantees structural fidelity, subgrid guarantees cross-depth alignment, and dense auto-placement guarantees spatial efficiency for jagged data. Together they yield a fractal-like interface where the visual form is a direct projection of the underlying hierarchical model.
