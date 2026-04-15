# TreeSheets Keyboard Shortcuts Cheat-Sheet (Fork Audit + Rectified Mapping)

This document audits the keyboard shortcuts currently embedded in the codebase and contrasts them with the remapping matrix provided for `ib-bsb-br/trimsheets`.

## 1) Source-of-Truth Baseline (hard-coded/default)

The default shortcut system is defined primarily through menu accelerators in `src/tsframe.h`, with additional key handling in `src/document.h`.

### Core editing and navigation

- `ENTER`: Enter/exit text edit mode.
- `F2`: Enter/edit and jump cursor to end of text.
- `SHIFT+ENTER`: Select first child.
- `CTRL+ENTER` (non-macOS) / `ALT+ENTER` (macOS): Progress to first cell in new row.
- `ALT+ENTER` (non-macOS) / `CTRL+ENTER` (macOS): Progress to next cell on the right.
- `ESC`: Select parent / cancel text edits.
- `TAB`, `SHIFT+TAB`: Next/previous cell.
- `INS` (non-macOS) / `CTRL+G` (macOS): Insert new grid.

### Search, replace, filter

- `CTRL+F`: Search.
- `F3`, `SHIFT+F3`: Next/previous search match.
- `CTRL+H`: Replace dialog.
- `CTRL+K`: Replace in current selection.
- `CTRL+J`: Replace in current selection and jump next.
- `CTRL+SHIFT+F`: Turn filter off.
- `CTRL+F3`: Go to next filter match.
- `Show only cells in current search`: available, no default key.
- `Filter by the same cell color`: available, no default key.

### Structural operations

- `F8`: Hierarchy Swap.
- `F9`: Wrap in new parent.
- `F10` (Windows) / `CTRL+F10` (non-Windows): Toggle Fold.
- `CTRL+SHIFT+F10`: Fold all.
- `CTRL+ALT+F10`: Unfold all.
- `ALT+UP`, `ALT+DOWN`: Scroll up/down (not sort by default).
- Sort ascending / descending: available, no default key.

### File, browser, and utility

- `F4`: Open file from selected cell text.
- `F5`: Open link in browser.
- `F1`: Interactive tutorial.
- `CTRL+ALT+F1`: Operation reference.
- `SHIFT+ALT+I`: Insert last image.
- `CTRL+Y`: Redo.

## 2) Remapping Matrix (from provided keyboard image)

The following is interpreted as **Current key -> Desired operation/key target**.

| Current key | Desired remap target | Action-level interpretation |
|---|---|---|
| `F1` | `SHIFT+ENTER` | Select first child |
| `F2` | `F10` | Toggle Fold |
| `CTRL+F2` | `CTRL+ALT+F10` | Unfold all |
| `SHIFT+F2` | `CTRL+SHIFT+F10` | Fold all |
| `CTRL+F3` | `Show only search` | Show only cells in current search |
| `F4` | `CTRL+F3` | Next filter match |
| `SHIFT+F4` | `CTRL+SHIFT+F` | Filter off |
| `CTRL+F5` | `Open file` | Open file from selected cell |
| `F8` | `SHIFT+ALT+I` | Insert last image |
| `F9` | `CTRL+RMB` | Set cell text to tag popup (mouse chord feature) |
| `F10` | `Filter by color` | Filter by same cell color |
| `ENTER` | `F2` | Enter/edit + jump to end |
| `CTRL+ENTER` | `INS` | Insert new grid |
| `SHIFT+ENTER` | `F9` | Wrap in new parent |
| `ALT+ENTER` | `F8` | Hierarchy swap |
| `ALT+UP` | `Sort asc` | Sort ascending |
| `ALT+DOWN` | `Sort desc` | Sort descending |
| `INS` | `ALT+ENTER` | Progress to next cell on the right |
| `CTRL+SHIFT+H` | `Replace all` | Replace all occurrences |
| `CTRL+SHIFT+Z` | `CTRL+Y` | Redo alias |

## 3) Conflict & Feasibility Analysis (code-aware)

- Some desired mappings target actions that already exist but are **unbound by default** (e.g., show-only-search, sort asc/desc, filter-by-color, replace-all); these can be added via key-binding customization and/or code-level defaults.
- Some desired mappings overlap with platform-sensitive behavior (`F10`, `CTRL/ALT+ENTER`, `INS`).
- `CTRL+RMB` is a mouse chord and not a pure keyboard action; binding this to `F9` requires explicit code behavior redesign, not only accelerator reassignment.
- `ENTER -> F2` changes text-entry ergonomics significantly; this is high impact for daily note capture and should be treated as an intentional mode shift.

## 4) Rectified Cohesive Shortcut Framework for Memory Management

The remap can be made coherent by organizing usage into four memory-oriented phases:

### Phase A — Capture

- `ENTER` -> jump-to-end edit mode (fast append in existing memory cells).
- `CTRL+ENTER` -> insert new grid (quickly create memory containers).
- `SHIFT+ENTER` -> wrap selection in parent (encapsulate thought clusters).

### Phase B — Structure

- `ALT+ENTER` -> hierarchy swap (promote/demote structures).
- `ALT+UP` / `ALT+DOWN` -> sort ascending/descending (clean lists, dates, tags).
- `INS` -> horizontal progression (rapid form-like data entry).

### Phase C — Review / Focus

- `CTRL+F3` -> show only current search matches.
- `F4` -> next filter match.
- `SHIFT+F4` -> clear filter.
- `F10` -> filter by same color.

### Phase D — Maintenance / Retrieval

- `F2` -> fold toggle.
- `CTRL+F2` -> unfold all.
- `SHIFT+F2` -> fold all.
- `CTRL+SHIFT+H` -> replace all.
- `CTRL+SHIFT+Z` -> redo.

## 5) Practical implementation notes for this fork

- Most of this framework can be implemented with existing action IDs and key binding infrastructure (`Options -> Key bindings...`).
- For a fully deterministic fork-wide default (out of the box), set these bindings in code where menu labels/accelerators are declared and where key events are manually handled.
- Validate on Linux/macOS/Windows due to known accelerator differences (`F10`, `CTRL+TAB`, special key handling on GTK).
