# TreeSheets Keyboard Shortcut Cheat-Sheet (ib-bsb-br/trimsheets)

## 1) Scope and audit method

This cheat-sheet was built by auditing the hard-coded menu accelerators and key event handlers in:

- `src/tsframe.h` (menu-defined shortcuts and platform-conditional bindings).
- `src/document.h` (non-menu key handling and GTK-specific fallbacks).

It also incorporates your attached remapping table as a **target key layout proposal**.

---

## 2) Conflict-aware remap matrix (from your attachment vs current source)

| Legacy key combo (source/default) | Default operation in source | Proposed key / behavior from attachment | Conflict status |
|---|---|---|---|
| `F1` | Interactive tutorial | `Shift+Enter` | Conflict (tutorial displaced) |
| `F2` | Enter text edit and jump to end | `F10` | Conflict |
| `Ctrl+F2` | No hard-coded default menu accelerator | `Ctrl+Alt+F10` | Custom-only mapping |
| `Shift+F2` | No hard-coded default menu accelerator | `Ctrl+Shift+F10` | Custom-only mapping |
| `Ctrl+F3` | Go to next filter match | `Show only search` (Filter: show only cells in current search) | Semantic remap |
| `F4` | Open file from selected cell text | `Ctrl+F3` | Conflict |
| `Shift+F4` | No hard-coded default menu accelerator | `Ctrl+Shift+F` | Custom-only mapping |
| `Ctrl+F5` | No hard-coded default menu accelerator | `Open file` | Custom-only mapping |
| `F8` | Hierarchy swap | `Shift+Alt+I` | Conflict |
| `F9` | Wrap in new parent | `Ctrl+RMB` (set cell text to tag popup workflow) | Conflict / modal behavior |
| `F10` | Toggle fold (Windows) / `Ctrl+F10` on non-Windows | Filter by same cell color | Conflict |
| `Enter` | Enter/exit text edit mode | `F2` | Conflict |
| `Ctrl+Enter` | Enter text edit and progress to first cell in new row | `Ins` | Conflict |
| `Shift+Enter` | Select first child | `F9` | Conflict |
| `Alt+Enter` | No hard-coded default menu accelerator | `F8` | Custom-only mapping |
| `Alt+Up` | Scroll up | Sort ascending | Conflict |
| `Alt+Down` | Scroll down | Sort descending | Conflict |
| `Ins` | Insert new grid (non-macOS default) | `Alt+Enter` | Conflict |
| `Ctrl+Shift+H` | No hard-coded default menu accelerator | Replace all | Custom-only mapping |
| `Ctrl+Shift+Z` | No hard-coded default menu accelerator | `Ctrl+Y` (Redo) | Common UX alias |

### Observations

- Several proposed bindings overwrite highly-used defaults (`Enter`, `F2`, `F8`, `F9`, `F10`, `Ins`, `Alt+Up/Down`).
- Some attached targets are **actions, not key combos** (e.g., “show only search”, “filter by color”, “open file”).
- A practical implementation should preserve muscle-memory-safe defaults for text entry and navigation while reassigning secondary/rare keys.

---

## 3) Full source-grounded shortcut inventory (hard-coded)

> Notes:
> - `CTRLORALT+<n>` means platform-dependent `Ctrl` or `Alt` modifier (as defined in source).
> - `F11/F12` are platform-conditional (`Ctrl+F11/F12` on macOS, plain `F11/F12` elsewhere).
> - `F10` fold is conditional (`F10` on Windows, `Ctrl+F10` on non-Windows).

### Core file / edit

- `Ctrl+N` New
- `Ctrl+O` Open
- `Ctrl+W` Close
- `Ctrl+S` Save
- `Ctrl+P` Print
- `Ctrl+Q` Exit
- `Ctrl+X` Cut
- `Ctrl+C` Copy
- `Ctrl+V` Paste
- `Ctrl+Alt+C` Copy with images
- `Ctrl+Shift+V` Paste style only
- `Ctrl+Z` Undo
- `Ctrl+Y` Redo
- `Del` Delete after
- `Backspace` Delete before
- `Ctrl+Del` Delete word after
- `Ctrl+Backspace` Delete word before

### Cell/grid traversal and selection

- `Tab` Next cell
- `Shift+Tab` Previous cell
- `Esc` Select parent / cancel edit
- `Shift+Enter` Select first child
- `Enter` Enter/exit text edit mode
- `F2` Enter text edit and jump to end
- `Ctrl+Enter` Enter text edit and progress to first cell in new row
- `Left/Right/Up/Down` Move selection (grid mode)
- `Ctrl+Left/Right/Up/Down` Move cells
- `Shift+Left/Right/Up/Down` Extend selection
- `Ctrl+Shift+Left/Right` Extend selection rows
- `Ctrl+Shift+Up/Down` Extend selection columns
- `Ctrl+A` Select all in current grid/cell

### Text navigation/editing

- `Left/Right` Cursor left/right
- `Ctrl+Left/Right` Word left/right
- `Shift+Home/End` Extend to start/end
- `Home/End` Start/end of line
- `Ctrl+Home/End` Start/end of text

### Search / replace / filter

- `Ctrl+F` Search
- `F3` Next match
- `Shift+F3` Previous match
- `Ctrl+H` Replace
- `Ctrl+K` Replace in current selection
- `Ctrl+J` Replace in selection + jump next
- `Ctrl+Shift+F` Turn filter off
- `Ctrl+F3` Next filter match
- Filter actions also exist without default accelerator: show only current search, filter by same cell color, show notes, etc.

### Structure / organization

- `Ins` (non-macOS) / `Ctrl+G` (macOS): Insert new grid
- `F9` Wrap in new parent
- `F8` Hierarchy swap
- `Ctrl+Shift+T` Transpose
- Sort Ascending / Sort Descending exist as menu actions (no default accelerator)

### Fold, view, scrolling, zoom

- `F10` (Windows) / `Ctrl+F10` (non-Windows): Toggle fold
- `Ctrl+Shift+F10` Fold all
- `Ctrl+Alt+F10` Unfold all
- `PgUp`, `Alt+Up` Scroll up
- `PgDn`, `Alt+Down` Scroll down
- `Alt+Left/Right` Scroll left/right
- `Ctrl+PgUp/PgDn` Zoom in/out
- `Ctrl+Tab` Next tab (not on GTK menu path)
- `Ctrl+Shift+Tab` Previous tab
- `F11`/`Ctrl+F11` Toggle fullscreen
- `F12`/`Ctrl+F12` Toggle scaled presentation

### Styling and formatting

- `Ctrl+B` Bold
- `Ctrl+I` Italic
- `Ctrl+U` Underline
- `Ctrl+T` Strikethrough
- `Ctrl+Alt+T` Typewriter style
- `Ctrl+Shift+R` Reset text styles
- `Ctrl+Shift+C` Reset colors
- `Shift+Alt+C/T/B` Reapply last cell/text/border color
- `Shift+Alt+F9/F10/F11/F12` Open color/image dropdown panels
- `Ctrl+Shift+1..5,9` Set border width presets
- `Ctrl+R` Reset column widths
- `Shift+PgUp/PgDn` Increase/decrease text size
- `Alt+PgUp/PgDn` Increase/decrease column width
- `Ctrl+Alt+PgUp/PgDn` Increase/decrease width (no subgrids)
- `Ctrl+Shift+S` Reset text sizes
- `Ctrl+Shift+M` Shrink text in all sub-grids

### Navigation helpers and references

- `F4` Open file from selected cell text
- `F5` Open link in browser
- `F6/Shift+F6` Go to matching text cell (forward/reverse)
- `F7/Shift+F7` Go to matching image cell (forward/reverse)
- `F1` Interactive tutorial
- `Ctrl+Alt+F1` Operation reference

### Layout/render style family

- `CTRLORALT+1` Vertical layout + grid style
- `CTRLORALT+2` Vertical layout + bubble style
- `CTRLORALT+3` Vertical layout + line style
- `CTRLORALT+4` Horizontal layout + grid style
- `CTRLORALT+5` Horizontal layout + bubble style
- `CTRLORALT+6` Horizontal layout + line style
- `CTRLORALT+7` Grid style rendering
- `CTRLORALT+8` Bubble style rendering
- `CTRLORALT+9` Line style rendering
- `CTRLORALT+0` Toggle vertical layout

### Script / program actions

- `Ctrl+Alt+L` Add script
- `Ctrl+Shift+Alt+L` Remove script
- `Ctrl+Alt+F5` Run
- `Ctrl+Alt+D/O/A/R` Mark Data / Operation / Variable Assign / Variable Read

### Legacy accelerators defined via wx accelerator table

- `Shift+Delete` Cut
- `Shift+Insert` Paste
- `Ctrl+Insert` Copy

---

## 4) Rectified “daily memory management” key architecture

To maximize praxeological day-to-day usage (capture -> link -> review -> organize -> recall), use this framework:

1. **Capture Layer** (fast entry)
   - Keep `Enter`, `F2`, `Ctrl+Enter`, `Ins` semantics close to defaults.
   - Avoid remapping `Enter` to non-entry actions.

2. **Link/Jump Layer** (context traversal)
   - Reserve `F4..F7` for external file/web and internal matching links.
   - Keep directional movement and selection unchanged.

3. **Review Layer** (search + filter)
   - Keep `Ctrl+F`, `F3`, `Shift+F3`.
   - Bind high-frequency review actions to nearby combos:
     - `Ctrl+F3`: next filter match (already present)
     - `Ctrl+Shift+F`: filter off (already present)
     - Add alias `Ctrl+Shift+H` => Replace all (custom)

4. **Structure Layer** (hierarchy shaping)
   - Keep `F8` hierarchy swap and `F9` wrap parent.
   - Map sort ascending/descending to ergonomic alternatives **without** stealing scroll keys:
     - Suggested: `Ctrl+Alt+Up` / `Ctrl+Alt+Down`.

5. **Safety Layer** (undo/redo compatibility)
   - Keep `Ctrl+Z`, `Ctrl+Y`.
   - Add `Ctrl+Shift+Z` as redo alias to improve cross-app consistency.

---

## 5) Recommended minimal adoption of your attachment (low breakage variant)

Adopt immediately (safe):

- `Ctrl+Shift+Z` -> Redo (alias of `Ctrl+Y`)
- `Ctrl+Shift+H` -> Replace all
- `Ctrl+F3` -> Show only current search (if desired workflow) **or** keep as next filter match and add separate key for "show only current search"

Defer or redesign (high breakage risk):

- Replacing `Enter`, `F2`, `F8`, `F9`, `F10`, `Ins`, `Alt+Up`, `Alt+Down`.

---

## 6) Implementation notes for this fork

- Most shortcuts are menu-backed and can be changed through key binding customization UI, but some behaviors are still enforced in key handlers (`src/document.h`) and OS/platform conditionals.
- Any fork-level “rectified map” should therefore include both:
  1) menu accelerator edits (or persisted user config), and
  2) key event handler reconciliation for special keys (`Enter`, `Backspace`, GTK-specific paths, etc.).

