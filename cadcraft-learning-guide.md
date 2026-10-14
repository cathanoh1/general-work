# CADCraft learning guide (for someone coming from SolidWorks)

Sources: I loaded the live editor (CADCraft 0.6.2 at photocrafteditor.com/cadcraft/editor) in a headless browser, opened every menu, used the built-in Command Reference (F1), and read the project's landing pages and repo docs (README, ROADMAP, gaps list). Items marked **[tested]** I ran myself in the editor. Items marked **[docs]** come from the project's documentation and I have not run them. Items marked **[standard]** are normal AutoCAD behaviour that CADCraft says it copies, but I did not confirm.

---

## 0. Read this first: what CADCraft is and isn't

- Free, open-source 2D drafting app that copies AutoCAD's command line and workflow. Written in Rust, by the ArtCraft team. Not affiliated with Autodesk.
- **2D only.** `3DORBIT` returns "not available yet: CADCraft draws in 2D (plan view) only". `EXTRUDE`, `PRESSPULL`, `BOX`, `CYLINDER` and `UCS` are unknown commands. The Modeling tool set's Primitives and Solid tools are greyed out. 3D is on the roadmap at roughly 2% done. **[tested]**
- **Pre-alpha, by the project's own rating.** Its ROADMAP says it is about 38% "ready for real work" and that four of five core workflows fail its alpha gate: precise drafting (no object snap tracking, some TRIM/EXTEND/OFFSET options stubbed), blocks, plotting, and lossless DWG save. **[docs]**
- **Professional-standard caveat:** you can learn the skills here and they transfer to AutoCAD, but don't use CADCraft for production drawings where file fidelity matters. Saving drops objects it doesn't model yet. Nobody has verified its DWG/DXF files open cleanly in AutoCAD. Always keep your original file. **[docs]**
- **Web build limits:** opens and saves DXF only (DWG needs the desktop app). No autosave in the browser, so save often and export. **[docs]**
- SHX fonts are not read yet. A stroke font stands in. **[docs]**

If your goal is "professional 2D drafting skills", learn here, then repeat the same habits in AutoCAD, BricsCAD or DraftSight. If your goal is "extrude and make solids", you need a 3D tool (see section 10).

---

## 1. The screen **[tested]**

| Area | What it is |
|---|---|
| Menu bar (top) | File, Edit, View, Insert, Format, Tools, Draw, Dimension, Modify, Window, Help |
| Tabs under the menu | Start, plus one tab per open drawing (e.g. Drawing1, Bracket) |
| Tool Sets (left) | Drafting tab (Draw, Hatch, Block, Modify, Text, Dimension, Leader) and Modeling tab (mostly greyed) |
| Drawing area | Crosshair cursor, ViewCube and WCS marker top right, UCS icon bottom left |
| Right panels | Layers palette on top, Properties palette below |
| Command line (bottom centre) | `>_ Type a command`. Prompts and clickable [Keywords] show here |
| Layout tabs and status bar (bottom) | Model, Layout1, Layout2; scale (1:1); coordinates; toggle buttons for grid, snap, ortho, polar, object snap |
| Help | F1 = searchable **Command Reference** (every command, its alias and a description). Help > About CADCraft, Help > Open Sample Drawing |

Useful windows: `Ctrl+1` Properties, `Ctrl+3` Tool Sets, `Ctrl+8` QuickCalc (shown in the Window menu).

Sample drawing: Help > Open Sample Drawing (or the "Bracket" tab). It's a mounting bracket with dimensions, a section hatch, notes and a title block. Study it. It is the standard to aim for.

---

## 2. The one skill that matters: the command line

In SolidWorks you click tools. In CAD drafting you **type commands and numbers** and click points only when quick.

- Type a command name or alias, press **Enter**. Prompts appear at the command line. **[tested]**
- **Enter, Space or right-click repeats** the last command. **Esc** cancels. **[docs]**
- Options inside a prompt are in [Square/Brackets]. Type the capital letters (or click them). Example: `FILLET` shows `[Undo/Polyline/Radius/Trim/Multiple]`, so type `R` for radius. **[tested]**
- Press **F1** for the Command Reference. Filter by typing in the Filter box.

### Entering points (this is how you draw to exact sizes)

| Input | Meaning |
|---|---|
| `3,4` | Absolute point X=3, Y=4 **[tested]** |
| `@8,5` | Relative: 8 right, 5 up from the last point **[tested]** |
| `@5<45` | Relative polar: distance 5 at 45 degrees **[docs]** |
| `#x,y` | Absolute even when dynamic input would otherwise read it as relative **[docs]** |
| Direct distance | Move the cursor in a direction (ortho/polar on), type a number, Enter **[docs]** |

### Drawing area basics
- Wheel zooms, hold wheel to pan. `ZOOM` then `E` = zoom extents (fit everything). **[tested]**
- Selection: window (left to right) selects objects fully inside; crossing (right to left) selects anything touched. **[standard]**

---

## 3. Tested exercise: a dimensioned plate **[tested]**

I ran these exactly and the results were correct (8 x 5 plate, holes in the right places, dimensions of 8.0000 and 5.0000).

1. Click the **Drawing1** tab (or File > New Drawing).
2. `REC` Enter. First corner: `0,0` Enter. Other corner: `@8,5` Enter. (A rectangle, 8 wide and 5 high.)
3. `ZOOM` Enter, `E` Enter.
4. `C` Enter (Circle). Center `1,1`, radius `0.3`.
5. `C`, center `7,1`, radius `0.3`.
6. `C`, center `4,2.5`, radius `1`.
7. `FILLET` Enter, type `R` (radius), enter `0.5`, then click two adjacent rectangle edges to round that corner. (I confirmed the prompt and the "Radius" option. I did not click edges.)
8. `DIMLINEAR` Enter. First point `0,0`, second point `8,0`, dimension line location `4,-1`. This gives 8.0000. Repeat for the height: `0,0`, `0,5`, `-1,2.5` gives 5.0000.
9. `LAYER` Enter opens the **Layer Properties Manager** (on/off, freeze, lock, plot, colour, linetype, lineweight, transparency, per-viewport freeze).

Next, try on your own: `OFFSET` (type a distance, click an object, click a side), `TRIM`, `MIRROR`, `ARRAY`, then dimension the circles with `DIMDIAMETER`.

---

## 4. Tool reference by job

Names below are from the project's feature table and the menus I opened. **[docs]** unless noted.

### Draw
`LINE` (L), `PLINE` (polyline with arcs and widths), `CIRCLE` (C: centre-radius, centre-diameter, `2P`, `3P`), `ARC`, `RECTANG` (REC, with fillet/chamfer/width options **[tested prompt]**), `POLYGON`, `ELLIPSE`, `SPLINE`, `POINT`, `XLINE` (construction line), `RAY`, `DONUT`, `TEXT`, `MTEXT`, `HATCH`, `GRADIENT`, `BOUNDARY`, `REGION`, `REVCLOUD`, `WIPEOUT`, `MULTILINE`, `CENTERMARK`, `CENTERLINE`, `HELIX`, `TABLE`.

### Modify
`ERASE`, `MOVE`, `COPY`, `ROTATE`, `SCALE` **[tested: starts and prompts for objects]**, `MIRROR`, `STRETCH` **[tested]**, `OFFSET`, `TRIM`, `EXTEND`, `FILLET`, `CHAMFER`, `BREAK`, `JOIN`, `EXPLODE`, `LENGTHEN`, `BLEND`, `ARRAY` (rectangular, polar, path), `OVERKILL`, draw order, `FLATTEN`.

### Precision
Object snaps: endpoint, midpoint, centre, geometric centre, node, quadrant, intersection, insertion, perpendicular, tangent, nearest. Also polar tracking, ortho, grid snap, and hot grips (click an object, click a grip, press Space to cycle Stretch / Move / Rotate / Scale / Mirror). The status-bar buttons at the bottom right toggle these. Object snap **tracking** is not implemented yet.

### Annotate
`DIMLINEAR` **[tested]**, `DIMALIGNED`, `DIMRADIUS`, `DIMDIAMETER`, `DIMANGULAR`, `DIMARC`, `DIMORDINATE`, `DIMCONTINUE`, `DIMBASELINE`, `QDIM`, `DIM`, `MLEADER`, `TABLE`, `DIMSTYLE` (full variable control), `TOLERANCE`. Dimensions are **associative**: they follow the geometry when you stretch or move it.

### Layers and properties
`LAYER`, the Layers palette (right), layer tools (isolate, freeze, off, lock, match, previous), Properties palette (`Ctrl+1`): colour, layer, linetype, linetype scale, lineweight, and per-object values. Format > Units, Drawing Limits, Linetype, Lineweight.

### Blocks
`BLOCK`, `INSERT`, attributes, nested blocks, `BEDIT` (static blocks). No dynamic-block authoring yet.

### Layouts and plotting
Model tab = your drawing at 1:1. **Layout tabs = paper sheets** with viewports at a set scale. `MSPACE` / `PSPACE`, page setups, `PLOT` and `EXPORTPDF`. Double-click a viewport to work in model space through it.

### Parametric (closest to SolidWorks)
`DIMCONSTRAINT` **[tested: prompt shows Linear/Horizontal/Vertical...]**, `GEOMCONSTRAINT`, `AUTOCONSTRAIN`, `PARAMETERS` (named values and expressions). Constraints re-solve after every edit.

### Files
Web: open and save **DXF** (R12 to 2018 read, R2000 write). Desktop app: DWG R13 to 2018 read, R2000 write. Export PDF, SVG, PNG. `SCRIPT` runs `.scr`-style command scripts. Useful: you can paste a list of commands into a script file and replay it.

---

## 5. Professional habits (this is what "professional standard" means in drafting)

1. **Draw full size, 1:1, in model space.** Scale happens in the layout viewport, not by shrinking the geometry.
2. **Pick units first** (`UNITS` / Format > Units) and stick to them. Decide mm or inches before you draw.
3. **Use layers deliberately.** At minimum: Outline, Hidden, Centre, Dimensions, Text, Hatch, Title block. Set colour and linetype per layer, then leave objects on **ByLayer**. Never draw on layer `0`.
4. **Never eyeball a point.** Type coordinates, use object snaps, or direct distance entry. Click points that are not snapped are wrong by a small unknown amount.
5. **Use polylines for outlines** (so `OFFSET`, `FILLET` and `HATCH` behave).
6. **Dimension with a DIMSTYLE** that matches your standard (arrow, text height, precision) and keep dimensions on their own layer. Leave the default dimension text, never type over a measured value.
7. **Dimension each feature once, and not as a closed chain.** Pick a datum and dimension from it.
8. **Lineweights and linetypes by layer.** Hidden lines dashed, centre lines chain.
9. **Use blocks** for repeated things (title block, symbols, standard parts).
10. **Plot from a layout**, not from model space, with viewport scale set and locked.
11. **Save a copy before experimenting,** and **save often** in this app (the web build has no autosave).

---

## 6. SolidWorks to CADCraft translation

| SolidWorks | CADCraft |
|---|---|
| Sketch (on a plane) | Model space (always the XY plane) |
| Smart Dimension (driving) | `DIMCONSTRAINT` (driving). `DIMLINEAR` etc. are annotation only |
| Relations (horizontal, tangent, coincident...) | `GEOMCONSTRAINT`, `AUTOCONSTRAIN` |
| Equations / global variables | `PARAMETERS` |
| Trim Entities / Extend | `TRIM` / `EXTEND` |
| Offset Entities | `OFFSET` |
| Sketch Fillet / Chamfer | `FILLET` / `CHAMFER` |
| Mirror / Linear Pattern / Circular Pattern | `MIRROR` / `ARRAY` (rectangular or polar) |
| Convert Entities / Construction geometry | `XLINE`, `RAY`, or a layer set to a construction linetype |
| Drawing (sheet, views) | Layout tab with viewports |
| Hole Callout / Smart dimension on a hole | `DIMDIAMETER` or `MLEADER` |
| Extruded Boss / Cut | **not available in CADCraft** |

The big mindset difference: in SolidWorks you model the 3D part and the drawing views come from it. Here you **draw each 2D view yourself** (front, side, section), and keep them aligned using construction lines and snaps.

---

## 7. A four-session practice plan

1. **Session 1: Mechanics.** Setup (units, layers). Draw a plate with typed coordinates. `OFFSET`, `TRIM`, `FILLET`, `MIRROR`, `ARRAY`. Learn `ZOOM E`, object snaps and grips.
2. **Session 2: Annotation.** Dimension the plate fully. Create a `DIMSTYLE`. Add centre marks, a `MLEADER` note, a title block as a block with attributes. Add section `HATCH`.
3. **Session 3: Layouts.** Make a Layout with a viewport at 1:2. Lock it. Plot to PDF. Reproduce the sample Mounting Bracket from scratch (compare against the "Bracket" tab).
4. **Session 4: Parametric.** Draw a shape, run `AUTOCONSTRAIN`, add `DIMCONSTRAINT` values, change one value and watch the geometry change. Use `PARAMETERS` for a named variable.

---

## 8. Things I have not confirmed (check these as you go)

- Whether the F-key toggles (F3 object snap, F8 ortho, F10 polar) match AutoCAD. Use the status-bar buttons if not.
- Alias names beyond `REC`, `C`, `L`: check F1 (Command Reference), which lists each alias.
- `SCALE` with the Reference option, `STRETCH` selection by crossing window, `OFFSET`, `TRIM`: I only confirmed they start. Test each on your plate.
- Saving: try File > Save As and reopen the file before you trust it.

---

## 9. Where to learn more
- In-app: F1 Command Reference; Help > Open Sample Drawing.
- Project: https://getartcraft.com/apps/cadcraft and https://github.com/storytold/cadcraft (README, `ROADMAP.md`, `docs/gaps.md` = honest list of what's missing). Community: ArtCraft Discord.
- Because it copies AutoCAD, general AutoCAD 2D tutorials (command by command) transfer well. Search for "AutoCAD 2D drafting basics" and "AutoCAD layouts and plotting".

## 10. If you need extrusion / 3D
CADCraft cannot do it. Closest to what you know from SolidWorks: **Onshape** (free, browser), **Fusion** (free for personal use), **FreeCAD** (free, open source). In AutoCAD itself: `EXTRUDE`, `PRESSPULL`, `SUBTRACT`, and the UCS.
