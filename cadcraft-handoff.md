# CAD Craft handoff: paste the prompt below into a local session

Use a session that runs on your computer (Claude desktop app, or `claude remote-control`), with the Claude in Chrome extension enabled and CAD Craft open in a Chrome tab.

---

## Prompt to paste

I'm new to AutoCAD but have some SolidWorks experience. I'm using a program called "CAD Craft", which I believe is a recent AutoCAD or AutoCAD-based tool. It is open in my Chrome browser right now.

What I need:
1. Look at my open tabs and explore CAD Craft (menus, ribbon/toolbar, command line, workspaces). Work out what it actually is and which commands it supports. Don't assume it matches AutoCAD.
2. Teach me to use it step by step, using what you actually see in the interface.
3. Start with the things I need now:
   - Resize a rectangle (it was originally drawn as a rectangle): scale, stretch, grips, Properties palette.
   - Draw and resize circles (center/radius, diameter, editing via Properties).
   - Extrude 2D shapes into 3D (EXTRUDE, PRESSPULL), cut holes (draw a shape, extrude, SUBTRACT), UNION, FILLET/CHAMFER.
   - Switch the drawing plane (UCS, Dynamic UCS) since I'm used to SolidWorks sketch planes.
4. Teach me by having me do each step, one at a time, and tell me what you see on screen so we can correct course. Don't click or change my drawing without telling me first.

## Context from the earlier conversation

- Asked first about a SolidWorks "Smart Dimension" equivalent. Answer: `DIM` (annotation only) and `DIMCONSTRAINT` / Parametric tab (driving dimensions, closest to SolidWorks).
- Asked how to change the size of shapes. Covered `SCALE` (incl. Reference option), `STRETCH` (crossing window), grips, Properties palette (`Ctrl+1`), `LENGTHEN`.
- Asked for a general AutoCAD intro. Covered the 3D Modeling workspace, `REC` with `D`, `C`, `EXT`, `PRESSPULL`, `SUBTRACT`, `UNION`, the UCS, and a SolidWorks-to-AutoCAD cheat sheet.
- The cloud session could not see the browser, so CAD Craft has not been explored yet. It is unconfirmed whether CAD Craft is AutoCAD or just AutoCAD-like.

## SolidWorks to AutoCAD cheat sheet

| SolidWorks | AutoCAD |
|---|---|
| Smart Dimension | `DIM` (annotation) / `DIMCONSTRAINT` (driving) |
| Extruded Boss/Base | `EXTRUDE` / `PRESSPULL` |
| Extruded Cut | Extrude a shape, then `SUBTRACT` |
| Revolve | `REVOLVE` |
| Fillet / Chamfer | `FILLET` / `CHAMFER` |
| Combine | `UNION` / `SUBTRACT` / `INTERSECT` |
| Linear / Circular Pattern | `ARRAYRECT` / `ARRAYPOLAR` |
| Mirror | `MIRROR` / `MIRROR3D` |
| Sketch Plane | UCS |

## First practice exercise

1. Draw a 100 x 60 rectangle (`REC`, then `D`).
2. Extrude it 20 units (`EXT`).
3. Set the UCS to the top face (`UCS`, then `F`).
4. Draw a circle of radius 10 at the face center.
5. Extrude the circle 30 units, then `SUBTRACT` it from the solid.
6. `FILLET` the top edges with radius 3.
