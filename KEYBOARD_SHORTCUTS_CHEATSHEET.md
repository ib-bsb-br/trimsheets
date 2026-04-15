# TreeSheets Keyboard Shortcuts — Rectified & Exhaustive Cheat-Sheet

This document supersedes the earlier draft by providing a stricter, source-anchored and exhaustive inventory for the `ib-bsb-br/trimsheets` fork, plus a conflict-aware interpretation of the attached remap image.

## 1) Ground truth sources
- `src/tsframe.h`: menu accelerators and platform-conditional bindings.
- `src/document.h`: direct key handling (`RETURN`, `BACKSPACE`, `ESC`) and GTK fallback handling.

## 2) Attached remap image — interpreted mapping and confidence

| Image row (left -> right) | Interpreted as | Confidence | Notes |
|---|---|---|---|
| `f1 -> shift+enter` | Move tutorial action from F1 to Shift+Enter | High | Conflicts with Select First Child default. |
| `f2 -> f10` | Move jump-to-end edit from F2 to F10 | High | Conflicts with Fold toggle binding on Windows. |
| `ctrl+f2 -> CTRL+ALT+F10` | Custom remap | Medium | No default Ctrl+F2 accelerator in source. |
| `SHIFT+F2 -> ctrl+shift+f10` | Custom remap | Medium | No default Shift+F2 accelerator in source. |
| `ctrl+f3 -> show only search` | Map Ctrl+F3 to filter: show only current search | High | Default Ctrl+F3 is next filter match. |
| `f4 -> ctrl+f3` | Move open file to Ctrl+F3 | High | Conflicts with filter-next default. |
| `shift+f4 -> ctrl+shift+f` | Custom remap | Medium | Shift+F4 not hardcoded by default. |
| `ctrl+f5 -> open file` | Map Ctrl+F5 to open file | Medium | Ctrl+F5 not hardcoded by default. |
| `f8 -> shift+alt+i` | Move hierarchy swap to Shift+Alt+I | High | Shift+Alt+I currently inserts last image. |
| `f9 -> ctrl+RMB` | Move wrap-in-parent to Ctrl+RMB flow | Low | Ctrl+RMB is a mouse popup workflow, not pure accelerator. |
| `f10 -> filter by color` | Map F10 to filter-by-cell-color | High | Default F10/Ctrl+F10 is fold toggle. |
| `enter -> f2` | Swap Enter and F2 behaviors | High | High impact on editing ergonomics. |
| `ctrl+enter -> INS` | Move Ctrl+Enter action to Insert | High | Insert currently creates new grid on non-macOS. |
| `shift+enter -> f9` | Move select-first-child to F9 | High | F9 currently wraps selection. |
| `alt+enter -> f8` | Map Alt+Enter action to F8 | Medium | Alt+Enter has no default hardcoded accelerator. |
| `alt+up -> sort asc` | Replace scroll up with sort ascending | High | Alt+Up currently scrolls. |
| `alt+down -> sort desc` | Replace scroll down with sort descending | High | Alt+Down currently scrolls. |
| `INS -> alt+enter` | Move insert-new-grid to Alt+Enter | High | Insert is default new-grid on non-macOS. |
| `CTRL+SHIFT+H -> replace all` | Add replace-all alias | High | Replace All has no default accelerator. |
| `ctrl+shift+z -> ctrl+y` | Add redo alias | High | Common cross-app alias pattern. |

## 3) Exhaustive hard-coded keyboard accelerators (menu + explicit accelerators)

| Key combo | Operation label | Action ID | Source |
|---|---|---|---|
| `ALT+DOWN` | Scroll Down (mousewheel) | `A_ADOWN` | `src/tsframe.h`:490 |
| `ALT+LEFT` | Scroll Left | `A_ALEFT` | `src/tsframe.h`:491 |
| `ALT+PGDN` | Decrease column width (ALT+mousewheel) | `A_DECWIDTH` | `src/tsframe.h`:186 |
| `ALT+PGUP` | Increase column width (ALT+mousewheel) | `A_INCWIDTH` | `src/tsframe.h`:184 |
| `ALT+RIGHT` | Scroll Right | `A_ARIGHT` | `src/tsframe.h`:492 |
| `ALT+UP` | Scroll Up (mousewheel) | `A_AUP` | `src/tsframe.h`:488 |
| `BACK` | Delete Before | `A_BACKSPACE` | `src/tsframe.h`:424 |
| `CTRL+A` | Select all in current grid/cell | `wxID_SELECTALL` | `src/tsframe.h`:219 |
| `CTRL+ALT+A` | Variable Assign | `A_MARKVARD` | `src/tsframe.h`:670 |
| `CTRL+ALT+C` | Copy with Images | `A_COPYWI` | `src/tsframe.h`:403 |
| `CTRL+ALT+D` | Data | `A_MARKDATA` | `src/tsframe.h`:668 |
| `CTRL+ALT+F1` | Operation reference | `A_HELP_OP_REF` | `src/tsframe.h`:685 |
| `CTRL+ALT+F10` | Unfold All | `A_UNFOLDALL` | `src/tsframe.h`:453 |
| `CTRL+ALT+F5` | Run | `wxID_EXECUTE` | `src/tsframe.h`:676 |
| `CTRL+ALT+L` | Add... | `A_ADDSCRIPT` | `src/tsframe.h`:649 |
| `CTRL+ALT+O` | Operation | `A_MARKCODE` | `src/tsframe.h`:669 |
| `CTRL+ALT+PGDN` | Decrease column width (no sub grids) | `A_DECWIDTHNH` | `src/tsframe.h`:190 |
| `CTRL+ALT+PGUP` | Increase column width (no sub grids) | `A_INCWIDTHNH` | `src/tsframe.h`:188 |
| `CTRL+ALT+R` | Variable Read | `A_MARKVARU` | `src/tsframe.h`:671 |
| `CTRL+ALT+T` | Toggle cell typewriter | `A_TT` | `src/tsframe.h`:309 |
| `CTRL+B` | Toggle cell BOLD | `wxID_BOLD` | `src/tsframe.h`:307 |
| `CTRL+BACK` | Delete Word Before | `A_BACKSPACE_WORD` | `src/tsframe.h`:429 |
| `CTRL+C` | Copy | `wxID_COPY` | `src/tsframe.h`:401 |
| `CTRL+DEL` | Delete Word After | `A_DELETE_WORD` | `src/tsframe.h`:427 |
| `CTRL+DOWN` | Move Cells Down | `A_MDOWN` | `src/tsframe.h`:253 |
| `CTRL+E` | Edit Note | `A_EDITNOTE` | `src/tsframe.h`:414 |
| `CTRL+END` | End of text | `A_CEND` | `src/tsframe.h`:293 |
| `CTRL+F` | Search | `wxID_FIND` | `src/tsframe.h`:471 |
| `CTRL+F10` | Toggle Fold | `A_FOLD` | `src/tsframe.h`:444 |
| `CTRL+F11` | Toggle Fullscreen View | `A_FULLSCREEN` | `src/tsframe.h`:531 |
| `CTRL+F12` | Toggle Scaled Presentation View | `A_SCALED` | `src/tsframe.h`:537 |
| `CTRL+F3` | Go to next filter match | `A_FILTERMATCHNEXT` | `src/tsframe.h`:512 |
| `CTRL+G` | Insert New Grid | `A_NEWGRID` | `src/tsframe.h`:432 |
| `CTRL+H` | Replace | `wxID_REPLACE` | `src/tsframe.h`:479 |
| `CTRL+HOME` | Start of text | `A_CHOME` | `src/tsframe.h`:292 |
| `CTRL+I` | Toggle cell ITALIC | `wxID_ITALIC` | `src/tsframe.h`:308 |
| `CTRL+INSERT` | Copy (legacy accelerator) | `wxID_COPY` | `src/tsframe.h`:698 |
| `CTRL+J` | Replace in Current Selection  Jump Next | `A_REPLACEONCEJ` | `src/tsframe.h`:482 |
| `CTRL+K` | Replace in Current Selection | `A_REPLACEONCE` | `src/tsframe.h`:481 |
| `CTRL+L` | Collapse Cells | `A_COLLAPSE` | `src/tsframe.h`:411 |
| `CTRL+LEFT` | Move Cells Left | `A_MLEFT` | `src/tsframe.h`:250 |
| `CTRL+LEFT` | Word Left | `A_MLEFT` | `src/tsframe.h`:280 |
| `CTRL+N` | New | `wxID_NEW` | `src/tsframe.h`:154 |
| `CTRL+O` | Open... | `wxID_OPEN` | `src/tsframe.h`:155 |
| `CTRL+P` | Print... | `wxID_PRINT` | `src/tsframe.h`:167 |
| `CTRL+PGDN` | Zoom Out (CTRL+mousewheel) | `A_ZOOMOUT` | `src/tsframe.h`:516 |
| `CTRL+PGUP` | Zoom In (CTRL+mousewheel) | `A_ZOOMIN` | `src/tsframe.h`:515 |
| `CTRL+Q` | Exit | `wxID_EXIT` | `src/tsframe.h`:172 |
| `CTRL+R` | Reset column widths | `A_RESETWIDTH` | `src/tsframe.h`:192 |
| `CTRL+RIGHT` | Move Cells Right | `A_MRIGHT` | `src/tsframe.h`:251 |
| `CTRL+RIGHT` | Word Right | `A_MRIGHT` | `src/tsframe.h`:281 |
| `CTRL+S` | Save | `wxID_SAVE` | `src/tsframe.h`:159 |
| `CTRL+SHIFT+1` | Border 1 | `A_BORD1` | `src/tsframe.h`:197 |
| `CTRL+SHIFT+2` | Border 2 | `A_BORD2` | `src/tsframe.h`:198 |
| `CTRL+SHIFT+3` | Border 3 | `A_BORD3` | `src/tsframe.h`:199 |
| `CTRL+SHIFT+4` | Border 4 | `A_BORD4` | `src/tsframe.h`:200 |
| `CTRL+SHIFT+5` | Border 5 | `A_BORD5` | `src/tsframe.h`:201 |
| `CTRL+SHIFT+9` | Border 0 | `A_BORD0` | `src/tsframe.h`:196 |
| `CTRL+SHIFT+ALT+L` | Remove... | `A_DETSCRIPT` | `src/tsframe.h`:651 |
| `CTRL+SHIFT+C` | Reset colors | `A_RESETCOLOR` | `src/tsframe.h`:314 |
| `CTRL+SHIFT+DOWN` | Extend Selection Columns Down | `A_SCDOWN` | `src/tsframe.h`:266 |
| `CTRL+SHIFT+F` | Turn filter off | `A_FILTEROFF` | `src/tsframe.h`:495 |
| `CTRL+SHIFT+F10` | Fold All | `A_FOLDALL` | `src/tsframe.h`:451 |
| `CTRL+SHIFT+LEFT` | Extend Selection Rows Left | `A_SCLEFT` | `src/tsframe.h`:261 |
| `CTRL+SHIFT+LEFT` | Extend Selection Word Left | `A_SCLEFT` | `src/tsframe.h`:285 |
| `CTRL+SHIFT+M` | Shrink text of all sub-grids | `A_MINISIZE` | `src/tsframe.h`:182 |
| `CTRL+SHIFT+R` | Reset text styles | `A_RESETSTYLE` | `src/tsframe.h`:313 |
| `CTRL+SHIFT+RIGHT` | Extend Selection Rows Right | `A_SCRIGHT` | `src/tsframe.h`:262 |
| `CTRL+SHIFT+RIGHT` | Extend Selection Word Right | `A_SCRIGHT` | `src/tsframe.h`:286 |
| `CTRL+SHIFT+S` | Reset text sizes | `A_RESETSIZE` | `src/tsframe.h`:181 |
| `CTRL+SHIFT+T` | Transpose | `A_TRANSPOSE` | `src/tsframe.h`:331 |
| `CTRL+SHIFT+TAB` | Previous tab | `A_PREVFILE` | `src/tsframe.h`:528 |
| `CTRL+SHIFT+UP` | Extend Selection Columns Up | `A_SCUP` | `src/tsframe.h`:265 |
| `CTRL+SHIFT+V` | Paste Style Only | `A_PASTESTYLE` | `src/tsframe.h`:409 |
| `CTRL+SHIFT+a` | Extend Selection Full Columns | `A_SCOLS` | `src/tsframe.h`:264 |
| `CTRL+T` | Toggle cell strikethrough | `wxID_STRIKETHROUGH` | `src/tsframe.h`:311 |
| `CTRL+TAB` | Next tab | `A_NEXTFILE` | `src/tsframe.h`:518 |
| `CTRL+U` | Toggle cell underlined | `wxID_UNDERLINE` | `src/tsframe.h`:310 |
| `CTRL+UP` | Move Cells Up | `A_MUP` | `src/tsframe.h`:252 |
| `CTRL+V` | Paste | `wxID_PASTE` | `src/tsframe.h`:407 |
| `CTRL+W` | Close | `wxID_CLOSE` | `src/tsframe.h`:157 |
| `CTRL+X` | Cut | `wxID_CUT` | `src/tsframe.h`:400 |
| `CTRL+Y` | Redo | `wxID_REDO` | `src/tsframe.h`:418 |
| `CTRL+Z` | Undo | `wxID_UNDO` | `src/tsframe.h`:416 |
| `DEL` | Delete After | `A_DELETE` | `src/tsframe.h`:421 |
| `DOWN` | Move Selection Down (DOWN) | `A_DOWN` | `src/tsframe.h`:242 |
| `END` | End of line of text | `A_END` | `src/tsframe.h`:291 |
| `ENTER` | Enter/exit text edit mode | `A_ENTERCELL` | `src/tsframe.h`:295 |
| `ESC` | Select Parent | `A_CANCELEDIT` | `src/tsframe.h`:268 |
| `ESC` | Cancel text edits | `A_CANCELEDIT` | `src/tsframe.h`:304 |
| `F1` | Interactive tutorial | `wxID_HELP` | `src/tsframe.h`:683 |
| `F2` | ...and jump to the end of the text | `A_ENTERCELL_JUMPTOEND` | `src/tsframe.h`:296 |
| `F3` | Next Match | `A_SEARCHNEXT` | `src/tsframe.h`:475 |
| `F4` | Open file | `A_BROWSEF` | `src/tsframe.h`:374 |
| `F5` | Open link in browser | `A_BROWSE` | `src/tsframe.h`:372 |
| `F6` | Go To Matching Cell (Text) | `A_LINK` | `src/tsframe.h`:271 |
| `F7` | Go To Matching Cell (Image) | `A_LINKIMG` | `src/tsframe.h`:273 |
| `F8` | Hierarchy Swap | `A_HSWAP` | `src/tsframe.h`:337 |
| `F9` | Wrap in new parent | `A_WRAP` | `src/tsframe.h`:439 |
| `HOME` | Start of line of text | `A_HOME` | `src/tsframe.h`:290 |
| `LEFT` | Move Selection Left (LEFT) | `A_LEFT` | `src/tsframe.h`:221 |
| `LEFT` | Cursor Left | `A_LEFT` | `src/tsframe.h`:278 |
| `PGDN` | Scroll Down (mousewheel) | `A_ADOWN` | `src/tsframe.h`:489 |
| `PGUP` | Scroll Up (mousewheel) | `A_AUP` | `src/tsframe.h`:487 |
| `RIGHT` | Move Selection Right (RIGHT) | `A_RIGHT` | `src/tsframe.h`:228 |
| `RIGHT` | Cursor Right | `A_RIGHT` | `src/tsframe.h`:279 |
| `SHIFT+ALT+B` | Apply last border color | `A_LASTBORDCOLOR` | `src/tsframe.h`:318 |
| `SHIFT+ALT+C` | Apply last cell color | `A_LASTCELLCOLOR` | `src/tsframe.h`:316 |
| `SHIFT+ALT+F10` | Open text colors | `A_OPENTEXTCOLOR` | `src/tsframe.h`:320 |
| `SHIFT+ALT+F11` | Open border colors | `A_OPENBORDCOLOR` | `src/tsframe.h`:321 |
| `SHIFT+ALT+F12` | Open image dropdown | `A_OPENIMGDROPDOWN` | `src/tsframe.h`:322 |
| `SHIFT+ALT+F9` | Open cell colors | `A_OPENCELLCOLOR` | `src/tsframe.h`:319 |
| `SHIFT+ALT+T` | Apply last text color | `A_LASTTEXTCOLOR` | `src/tsframe.h`:317 |
| `SHIFT+ALT+i` | Insert last image | `A_LASTIMAGE` | `src/tsframe.h`:366 |
| `SHIFT+DELETE` | Cut (legacy accelerator) | `wxID_CUT` | `src/tsframe.h`:696 |
| `SHIFT+DOWN` | Extend Selection Down | `A_SDOWN` | `src/tsframe.h`:258 |
| `SHIFT+END` | Extend Selection to End | `A_SEND` | `src/tsframe.h`:288 |
| `SHIFT+ENTER` | Select First Child | `A_ENTERGRID` | `src/tsframe.h`:269 |
| `SHIFT+F3` | Previous Match | `A_SEARCHPREV` | `src/tsframe.h`:476 |
| `SHIFT+F6` | Go To Matching Cell (Text, Reverse) | `A_LINKREV` | `src/tsframe.h`:272 |
| `SHIFT+F7` | Go To Matching Cell (Image, Reverse) | `A_LINKIMGREV` | `src/tsframe.h`:274 |
| `SHIFT+HOME` | Extend Selection to Start | `A_SHOME` | `src/tsframe.h`:287 |
| `SHIFT+INSERT` | Paste (legacy accelerator) | `wxID_PASTE` | `src/tsframe.h`:697 |
| `SHIFT+LEFT` | Extend Selection Left | `A_SLEFT` | `src/tsframe.h`:255 |
| `SHIFT+PGDN` | Decrease text size (SHIFT+mousewheel) | `A_DECSIZE` | `src/tsframe.h`:179 |
| `SHIFT+PGUP` | Increase text size (SHIFT+mousewheel) | `A_INCSIZE` | `src/tsframe.h`:177 |
| `SHIFT+RIGHT` | Extend Selection Right | `A_SRIGHT` | `src/tsframe.h`:256 |
| `SHIFT+TAB` | Move to previous cell (SHIFT+TAB) | `A_PREV` | `src/tsframe.h`:211 |
| `SHIFT+UP` | Extend Selection Up | `A_SUP` | `src/tsframe.h`:257 |
| `TAB` | Move to next cell (TAB) | `A_NEXT` | `src/tsframe.h`:204 |
| `UP` | Move Selection Up (UP) | `A_UP` | `src/tsframe.h`:235 |

### Direct key-handler bindings not purely menu-driven

| Key | Behavior | Source |
|---|---|---|
| `RETURN` | Shift=>A_ENTERGRID / Ctrl=>A_ENTERCELL_JUMPTOSTART / default=>A_ENTERCELL | `src/document.h`:796 |
| `BACKSPACE` | A_BACKSPACE when Ctrl is not pressed | `src/document.h`:793 |
| `ESC` | A_CANCELEDIT | `src/document.h`:800 |

## 4) Rectified, cohesive key architecture for daily memory management

### First principles
1. **Do not break text entry primitives**: keep `Enter`, `Ctrl+Enter`, `F2`, `Insert` coherent.
2. **Keep navigation orthogonal to organization**: arrows/scroll should not silently become sort commands.
3. **Preserve reversible operations ergonomics**: keep `Ctrl+Z`, `Ctrl+Y` and add `Ctrl+Shift+Z` alias.
4. **Cluster retrieval operations**: search/filter bindings should stay adjacent conceptually and physically.
5. **Prefer additive aliases over destructive remaps** for stability in daily use.

### Recommended practical mapping (low-breakage, high utility)
- Keep defaults for: `Enter`, `Ctrl+Enter`, `Shift+Enter`, `F2`, `F8`, `F9`, `F10/Ctrl+F10`, `Insert`, `Alt+Up/Down`.
- Add aliases:
  - `Ctrl+Shift+Z` -> Redo (`wxID_REDO`).
  - `Ctrl+Shift+H` -> Replace All (`A_REPLACEALL`).
  - Optional: `Ctrl+Alt+Up` -> Sort Ascending (`A_SORT`).
  - Optional: `Ctrl+Alt+Down` -> Sort Descending (`A_SORTD`).
- Keep `Ctrl+F3` as “next filter match”; if “show only current search” is desired, assign it to a new dedicated combo to avoid mode confusion.

## 5) High-risk remaps from the image (should be staged, not applied wholesale)
- `Enter <-> F2` swap: high disruption to editing flow.
- `F10` reassignment from fold to filter-by-color: breaks fold muscle memory and platform conventions.
- `Insert` reassignment: conflicts with new-grid insertion workflow.
- `Alt+Up/Alt+Down` reassignment from scroll to sort: violates navigation consistency.
- `F8/F9` reassignment: destabilizes hierarchy manipulation workflows.

## 6) Implementation checklist for this fork
1. Add/adjust menu accelerators in `src/tsframe.h`.
2. Reconcile direct key handling logic in `src/document.h` for `RETURN/BACKSPACE/ESC` and platform fallbacks.
3. Validate per platform (Windows/macOS/Linux GTK) because bindings are conditional in source.
4. Regression-test: text entry, hierarchy ops (`F8/F9`), fold/unfold, filter/search loops, undo/redo aliases.
