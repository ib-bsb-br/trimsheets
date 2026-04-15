# TreeSheets Keyboard Shortcuts Cheat-Sheet

## Shortcut Framework for Memory Management

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
