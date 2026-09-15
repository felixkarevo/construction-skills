---
name: construction-freecad-bim
description: >
  Core modeling skill of the construction-design library: real, structurally verified BIM
  models in FreeCAD 1.x through a live GUI driven by the neka-nat/freecad-mcp bridge —
  Site/Building/Storey hierarchy, live parametric openings via Subtractions (never frozen
  booleans), classified makeStructure members, makeRebar cages, code-gated stairs, MEP
  risers/shafts, CalculiX FEM verification via run_fem_analysis, IFC import (NativeIFC,
  locked/unlocked modes) and export proven by parsing, renovation/retrofit modeling
  (Bestand baseline, Sanierungsstatus phase tagging, delta-volume tracking, degraded-
  material FEM overrides). Verify-by-measurement after every
  placement; honesty protocol: no member is
  adequate without solver output. Design values defer to sibling skills
  (concrete-detailing, structural-analysis, geotechnics-foundations, ...); this file owns
  modeling mechanics and MCP bridge behaviour.
---

# FreeCAD BIM Modeling & Structural Verification — Core Skill

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

This is the **core** file of a 30-skill construction-design library. It teaches an
MCP-capable agent to produce honest, parametric, solver-checked building models inside a
live FreeCAD 1.0.x GUI. Everything geometry-technical here was validated against FreeCAD
1.0.1 through the MCP bridge (CalculiX `ccx` and `gmsh` present) and against the
object-by-object study of FreeCAD's bundled example building
`usr/share/examples/BIMExample.FCStd` (361 objects: 41 walls, 18 doors, 18 windows,
9 slabs, 7 stairs, 5 storeys). The worked example bundled in this repository
(`model/`) documents the same object discipline on a compact residential building.

**Markers:** **[verified]** = executed live on FreeCAD 1.0.1 through this bridge —
evidence. **[unverified]** = knowledge **not** round-tripped through the solver or the
running instance — a lead to confirm, not evidence.

## Reality Check — Licensing & Liability

**This skill produces design aids, dimensional guidance and modeling workflow for planning
and FreeCAD modeling ONLY. It does not produce engineering design.**

- Any design for **actual construction of a real occupied building** MUST be reviewed,
  sealed and stamped by a **licensed structural engineer** — in DACH the
  `Tragwerksplaner` who signs the *bautechnischer Nachweis*, typically countersigned by a
  *Prüfingenieur* per the *Landesbauordnung* — and MUST pass **local authority approval**
  (*Baugenehmigungsverfahren* with *B-Plan*/BauNVO zoning, setback, coverage, height).
  See `building-regulations-permits`.
- A CalculiX/FEM result from this workflow is a **screening check, not a design**: linear-
  elastic, isotropic, homogeneous, small-displacement, single-load-case, mesh-dependent.
  For concrete it does **not** model cracking, tension stiffening, creep, shrinkage,
  long-term deflection, bar bond/anchorage, punching shear, or seismic/wind demand; no
  buckling, fatigue or connection checks. **Passing it does not mean a member is safe.**
- Soil bearing capacity used here is an **assumed value**; real footings need a
  geotechnical investigation (`geotechnics-foundations`). Frost depth, water table,
  expansive/collapsible soils, fill, site class: not knowable from a model.
- Reinforcement modeled here is **geometry, not a detailing design** — development
  lengths, laps, hooks, curtailment and confinement detailing follow the Eurocode rules
  owned by `concrete-detailing` (seismic: `seismic-design`). Cite and defer; never
  re-derive here.

**The agent must never present FreeCAD output as construction-ready.** If the user's
language treats it as final — *"so I can start building"*, *"send this to the
contractor"*, *"is this safe"*, *"final footing size"*, *"can I pour this"* — say so
**unprompted, first, in that reply**. See §7.3 for the exact status-block protocol.

## How this library fits

This file is the modeling engine. The other 29 skills own the *why* behind every number.
When a question here becomes a design question, switch to the owning skill — never
improvise a design value from a modeling recipe.

| Skill | Owns (one line) |
|---|---|
| `simple-first-building` | GOVERNING gate: standard tier + complexity ladder — every model object defaults to the simplest proven solution; escalations and downward deviations only via its documented decision machinery. |
| `building-planning-spatial` | Room programs, dimensions, circulation, planning grid — the plan this file models. |
| `building-typology` | Building types, housing forms, massing and typological section patterns. |
| `structural-systems` | Load-bearing system choice, load-path narrative, preliminary span/depth sizing tables. |
| `structural-analysis` | Structural action: load combinations, internal forces, deflection and stability checks — the hand calc every FEM run is compared against. |
| `concrete-detailing` | Eurocode (EN 1992) reinforcement rules: cover by exposure class, min/max steel, anchorage, laps, stirrups, bar schedules. |
| `masonry-construction` | Masonry build-up, wall types, EN 1996 constraints, confined-masonry practice. |
| `timber-steel-design` | Timber (EN 1995) and steel (EN 1993) member and connection design. |
| `geotechnics-foundations` | Soil investigation, bearing capacity, settlement, retaining, foundation type selection. |
| `seismic-design` | Earthquake action, regularity rules, ductility and confinement detailing (EN 1998). |
| `construction-detailing` | Physical junction details: DPC/DMP layers, sills, head conditions, movement joints. |
| `building-materials` | Material properties, unit weights, selection and specification. |
| `building-physics-thermal-moisture` | Hygrothermal performance: U-values, condensation, airtightness, build-up order. |
| `building-acoustics` | Sound insulation, room acoustics, flanking, separating-element rules. |
| `fire-protection-building` | Fire compartments, reaction classes, resistance periods (F30–F120), escape routes. |
| `roofing-waterproofing` | Roof build-ups, falls, drainage, membrane and tile detailing. |
| `openings-windows-doors` | Window/door design, lintels, sills, installation joints, glazing. |
| `stairs-vertical-circulation` | Stair geometry rules and the **hard code gates** this file's stair checks are parameterized with. |
| `accessibility-universal-design` | Barrier-free design (DIN 18040): widths, ramps, tolerances beyond minimums. |
| `building-services-tga` | TGA engineering: risers (*Steigstränge*), shafts (*Installationsschächte*), plant rooms, penetration coordination. |
| `construction-scheduling-site` | Time: schedules, sequence, site logistics, crane and laydown planning. |
| `cost-management-din276` | Cost per DIN 276 cost groups, quantities-to-cost mapping, BOQ discipline. |
| `building-regulations-permits` | Bylaws, setbacks, GRZ/GFZ, permit workflow, submissions. |
| `sustainable-construction` | Embodied carbon, circularity, material passports, certification systems. |
| `existing-structures-retrofit` | Building in existing conditions: assessment, Nachrechnung, strengthening, envelope retrofit. |
| `building-renovation-refurbishment` | Component-level renovation technique: Bestandsaufnahme, repair systems per building element, energetic/ecological retrofit workflow, Abbruch/Rückbau — the source of what §3.10's renovation modeling pattern renders. |
| `timber-building-renovation` | Historical timber diagnosis and repair: Schadensanalyse/-bewertung, Ertüchtigung technique, Fachwerk/Umgebindebau — the source of §3.10's degraded-material override numbers for timber. |
| `bim-management` | The BIM **process**: naming, LOIN/LOI/LOG (DIN EN 17412), MVD, CDE, IFC validation — the deep data discipline touched only lightly here. |
| `construction-drawing-sketching` | Drawing and sketch representation of the model: line weights, hatching, sheet craft. |

### Reading order

1. **This file + `building-planning-spatial`** — first; you cannot model what is not
   planned, and cannot plan what you cannot keep parametric.
2. `building-typology` → `structural-systems` — kind of building, load-bearing system.
3. `structural-analysis` → `concrete-detailing` → `geotechnics-foundations` — the numbers
   the model must carry honestly; then the material/hazard track: `masonry-construction` /
   `timber-steel-design` / `seismic-design`.
4. `openings-windows-doors` → `stairs-vertical-circulation` → `roofing-waterproofing` →
   `construction-detailing` — whose rules §3's recipes assert by measurement; then
   `building-materials` → `building-physics-thermal-moisture` → `building-acoustics` →
   `fire-protection-building` — performance properties that ride on the IFC export (§4).
5. `building-services-tga` → `accessibility-universal-design` — coordination and
   use-quality passes.
6. `building-regulations-permits` → `sustainable-construction` →
   `construction-scheduling-site` → `cost-management-din276` — compliance, lifecycle,
   time and money frame.
7. `bim-management` → `construction-drawing-sketching` — how the model is exchanged,
   validated and drawn for humans.

## 1. Setup — the FreeCAD ⇄ MCP bridge

Source of truth for the bridge: **https://github.com/neka-nat/freecad-mcp** (the tool —
the only external project this file names). The bridge = a FreeCAD addon exposing an RPC
server inside the running GUI + an MCP server any MCP-capable agent client registers.
Tool names are usually prefixed by the server name (e.g. `mcp__freecad__execute_code`);
bare names are used here.

### 1.1 Install (one-time, needs a human)

1. **FreeCAD 1.0+, GUI build.** The bridge drives a *live* GUI — no headless mode: under
   Xvfb the GUI thread hangs forever and every RPC call times out with no error.
2. Put the addon's `addon/FreeCADMCP` folder into the FreeCAD **Mod** directory —
   Linux `~/.local/share/FreeCAD/Mod`; Windows `%APPDATA%\FreeCAD\Mod`;
   macOS (1.1) `~/Library/Application Support/FreeCAD/v1-1/Mod`.
3. Restart FreeCAD → **MCP workbench** → **"Start RPC Server"**. **"Auto-Start Server"**
   persists the choice in `freecad_mcp_settings.json`.
4. Start the MCP server for the agent side: `uvx freecad-mcp` (or `uv run` from a cloned
   repo); register it in **any** MCP-capable agent client's config as an `mcpServers`
   entry.

### 1.2 The tool surface

| Tool | Use it for |
|---|---|
| `create_document` | New/replace target document. |
| `create_object` / `edit_object` / `delete_object` | Single-object CRUD by class/property — fine for boxes, too crude for parametric recipes (use `execute_code`, G-35). |
| `execute_code` | Python **on the GUI thread**; the workhorse for §3. |
| `execute_code_async` | Long computation off-thread, then `commit(fn, timeout=120)` applies results on the GUI thread (§1.4, G-23). |
| `insert_part_from_library` | Pull a prepared solid (e.g. multi-part window/door template) into the document (G-34). |
| `get_object` / `get_objects` / `list_documents` | Read properties/shape metadata; list open docs. |
| `get_view` | A screenshot of the GUI (§1.3). |
| `get_rpc_status` | Dispatch queue alive or `stuck`? (§1.4, §6.1) |
| `run_fem_analysis` | Runs CalculiX on an **already assembled** `Fem::FemAnalysis`; auto-creates `SolverCcxTools`; returns max/min von Mises, max displacement, node count, working dir, result object. |

### 1.3 Screenshot control — token economy (G-30)

- Every screenshot-capable call takes `include_screenshot` and `view_name`
  (`Isometric | Front | Top | Right`). `include_screenshot=False` is the **default for
  anything analytical** (face dumps, property reads, assertions, meshing, load
  arithmetic, FEM numeric runs); `True` only when a human should see the change, the
  final view, or the one FEM run whose stress picture *is* the deliverable. Pick
  `view_name` to show it: Front for an elevation, Top for a plan, Isometric for massing.
- Launch the server with `--only-text-feedback` to strip images from all responses —
  cheapest mode for long builds; re-enable selectively per call.

### 1.4 Timeouts, queueing and the GUI thread — the rules that prevent hangs

- RPC work is a **FIFO queue on the GUI thread** (G-28): one operation at a time, in
  order. **Never fan out parallel FreeCAD calls** around a solver or any long operation.
- `execute_code` budget: **90 s queue + 90 s execution; client socket up to 210 s**
  (G-22). Longer work must be split into smaller calls — never "just raise the timeout".
- `run_fem_analysis`: request `timeout` per compute budget; **client socket ≥ 2×timeout
  + 30 s** (queue + execution) (G-33).
- **Never long-block the GUI thread** (G-23): a solve, giant mesh or heavy boolean held
  there freezes every other RPC — including `doc.save()`. Use `execute_code_async`: build
  off-thread, then `commit(fn, timeout=120)` to apply on the GUI thread.
- `GUI_DISPATCH_STUCK` or `get_rpc_status → "stuck"`: GUI thread blocked — **stop
  queuing**, recover per §6.1.
- `execute_code` runs in a **persistent namespace** with `FreeCAD`/`App`/`Gui` aliases
  (G-27): variables survive across calls and are NOT clean after failures — keep calls
  self-contained. After an exception (especially dev/nightly builds), **inspect the
  `Proxy` of any half-built FeaturePython object before mutating the document** (G-29);
  delete-and-rebuild beats patch-in-place (§6.2).

### 1.5 Remote access (only if the human asks) — G-32

RPC listens on **localhost only** by default. Remote use needs the workbench's **Remote
Connections** option + **Allowed IPs** (CIDR) + the server's `--host` flag — an explicit
user security decision, never a convenience to enable silently.

### 1.6 Connection preflight — before touching the model

| Step | Call | Pass condition |
|---|---|---|
| 1. RPC alive? | `get_rpc_status` | not `stuck`; if stuck, restart per §6.1 |
| 2. Documents | `list_documents` | target present, or `create_document` |
| 3. Solver binaries | `execute_code`: check `ccx` and `gmsh` on PATH | both **[verified present on 1.0.1]** before any FEM plan |
| 4. Version | `execute_code`: `App.Version()` | 1.0.x — §5 gotchas are 1.0-specific |

### 1.7 Scripting discipline inside `execute_code`

- `try/except` + `print` the traceback around risky blocks — uncaught exceptions return
  terse, diagnostic-free failures. `doc.recompute()` after **every** structural change
  (G-08); fetch by **Label** (G-01); print explicit `PASS`/`FAIL` for every assertion —
  a silent script proves nothing.
- One element per call, verified, saved (`doc.save()`) — increments, not monoliths
  (§6.1 for why).

## 2. Modeling discipline — the doctrine

### 2.1 Spatial hierarchy — always build this first

Real BIM is `Site > Building > Storey(s) > elements`, not a flat document — in IFC the
spatial decomposition tree (`IfcSite → IfcBuilding → IfcBuildingStorey`; elements attached
by spatial containment). A flat document exports as orphaned objects no coordinator can
schedule. Each storey carries a real `Elevation` (mm); assign elements via
`spatial.assign_container` or the storey's `Group`. Build it **before placing a single
wall** — the bundled reference model has 5 storeys, each at a distinct real elevation.

```python
site     = Arch.makeSite(name="Site")
building = Arch.makeBuilding(name="Building")
ground   = Arch.makeFloor(name="Ground Floor")   # IfcType "Building Storey"
ground.Elevation = 0
upper    = Arch.makeFloor(name="Upper Floor")
# CRITICAL (G-12): Elevation is DERIVED from Placement.Base.z — set it through Placement:
p = upper.Placement; p.Base.z = 3200; upper.Placement = p   # mm, matches ground wall height
# nest: site contains building, building contains floors, floors contain elements
```

The bundled reference model had 5 storeys, each at a distinct real `Elevation` — build
the hierarchy **before placing a single wall**.

**Storey scheme for a house with foundations:**

| Storey label | Elevation (mm) | Contains |
|---|---|---|
| `Foundation` | **negative** (e.g. −1200) | footings, pile caps, PCC/lean layer, plinth beams below DPC |
| `Plinth` | −450 to 0 | plinth beam, plinth walls, fill, DPC |
| `Ground Floor` | 0 | slab-on-grade, walls, columns, doors/windows |
| `Upper Floor` | +3200 | suspended slab, walls, stair landing |
| `Roof` | +6400 | roof slab, parapet, water-tank base |

Footings belong to the **Foundation** storey — filed under Ground Floor they schedule and
quantify wrong and read as above-grade in IFC.

### 2.2 One source of truth — parametric objects, not baked geometry

- Wall openings = **live `Subtractions`** with hidden void solids (§3.1) — never a
  one-off `Part::Cut` pasted back; a frozen boolean can't take a second window, can't be
  schedule-counted, can't be re-verified. Repeated patterns = **one source shape**
  arrayed/cloned (§3.1), not N cuts.
- Structural elements = `Arch.makeStructure` with real properties (§3.3) — a `Part::Box`
  carries no BIM classification: no foundation/column in IFC, no schedule, no take-off.
  Rebar = `Arch.makeRebar` on host-face sketches (§3.4), never drawn wires.
- Positions that matter are **constrained sketches** — unconstrained geometry drifts on
  recompute and every downstream BoundBox check silently changes meaning.

### 2.3 Naming and classification conventions

- `name=` sets **Label**, not `Name` (G-01); fetch by Label. Pattern `<Role>_<ID>`:
  `PadFooting_F1`, `Column_C1`, `Wall_W-N-01`, `Win_W1-N01`, `Door_D-G01`, `Rebar_F1-B1` —
  stable IDs matter because verification stamps (§7.5) and bar marks attach by object
  identity.
- Every object: correct `IfcType` **proven by export+grep** (§4.4), not by property value.
- Helper solids `Void_*` are named, always hidden, and remain part of the parametric
  chain (openings are verified against their BoundBoxes, §3.5) — never rename/delete
  casually.
- Project-wide naming/Pset/MVD conventions come from `bim-management` (BEP
  *BIM-Abwicklungsplan* / AIA if one exists); this file enforces: label-fetchable,
  stable, classification proven.

### 2.4 Verify-by-measurement — after EVERY placement, no exceptions

1. **BoundBox** — print `obj.Shape.BoundBox` immediately after every `Placement` set on
   any `makeStructure` object; compare to intended world coordinates **before** the next
   step depends on it (catches G-13/G-19 at placement time).
2. **Volume diff** — every boolean cut must move `Shape.Volume` by the expected amount
   (§3.1); a no-op cut is invisible in a screenshot, obvious in a diff.
3. **Export-and-grep** — every claimed IFC classification must round-trip (§4.4).
Asserts print `PASS`/`FAIL`. "No error" is not "it worked".

### 2.5 Level of Information Need — minimum-information principle

Model only what the agreed use case needs (DIN EN 17412 *LOIN*: geometry **LOG** +
information **LOI** per object type and milestone; process depth in `bim-management`):

- The bundled reference shows what a real shipped example *doesn't* bother with: wall
  `Material`/`IfcProperties` empty even on finished walls, TechDraw minimal. **Do not
  over-invest in Psets/materials or drawing sheets unless construction documents were
  requested** — matching the reference's priorities is calibration, not laziness.
- **Exception: structural members are never "schematic".** A footing, column, beam, slab
  or rebar object with no real dimensions, concrete class and steel is not a detail level
  — **it is a false structural claim.** Model it properly (§3.3–§3.4) or leave it out and
  say it is absent.

**Effort calibration:**

| Ask | Build | Skip |
|---|---|---|
| "show me the massing / layout" | hierarchy, walls, openings, slabs | rebar, FEM, materials, TechDraw |
| "model my house" | + doors/windows as BIM objects, stairs with §3.6 gates, footings with real sizes | FEM unless a member is claimed adequate |
| "is this beam OK / can this span" | + FEM per §3.8, hand-check, convergence | Psets, drawing sheets |
| "prepare it for my engineer" | + rebar cages, bar schedule, IFC export, §7.3 status block | nothing — this is the full pass |

### 2.6 System-family thinking — define once, instance many

The reference model's repeated elements follow one pattern: one profile/void/member
definition, then `Draft.make_ortho_array` / `Draft.make_clone` instances pointing at the
source. When a whole *build-up* repeats (wall type, floor type, riser group), fix its
section once (sketch or preset) and place instances along the plan grid — the same
type/instance split IFC mapping exploits, where the export target reads it (§2.5).

### 2.7 Units — the #1 source of silent 1000× errors

FreeCAD's internal system is **mm, kg, s** (force = `mm·kg/s²` = milli-newtons; pressure
= `kg/(mm·s²)`).

| Quantity | Assign as | Read back as | Trap |
|---|---|---|---|
| Length | `"3000 mm"` or float mm | `.getValueAs("mm").Value` | bare floats are mm — fine |
| Force | `"21600 N"` **(string)** | `.getValueAs("N").Value` | raw print shows `21600000.0 mm*kg/s^2` |
| Pressure / stress | `"0.005 MPa"` **(string)** | `.getValueAs("MPa").Value` | 1 MPa = 1000 internal units; bare float **1000× wrong** |
| Density | `"2400 kg/m^3"` | `.getValueAs("kg/m^3").Value` | — |
| Young's modulus | `"30000 MPa"` | — | material dict values are **strings with units** |
| Angle | `"90 deg"` | `.getValueAs("deg").Value` | Placement rotations take degrees |

**Always assign quantities as unit-bearing strings; always read with `.getValueAs()`.
Never compare a raw quantity to a float.** (G-04, G-21.)

## 3. Recipes — every element, start to finish

**All code runs inside `execute_code`** (FreeCAD 1.x Python; persistent `App`/`Gui`
aliases per §1.4 — assume `import FreeCAD as App, Draft, Arch` and
`doc = App.ActiveDocument` at each call top so calls stay self-contained).

### 3.1 Walls with live parametric openings

**What does NOT work reliably**: `window.Hosts = [wall]` alone does not cut the wall
(verified: zero volume difference) (G-07). **What works**: `wall.Subtractions` performs a
real, live, parametric boolean cut — the subtracted object must be a plain solid: a
`Part::Extrusion` of a 2D sketch rectangle (or a `Draft.Array`/`Draft.Clone` of one for
repeats), not the Window/Door BIM object. `Arch.makeVoid` produces a purpose-built void
for the same slot **[unverified here]**; the sketch+extrusion path is the verified one.

```python
sketch = doc.addObject("Sketcher::SketchObject", "VoidProfile_W1-N01")
# ... constrain to a WxH rectangle at the opening's local wall-face position ...
void = doc.addObject("Part::Extrusion", "Void_W1-N01")
void.Base      = sketch
void.DirMode   = "Normal"
void.LengthFwd = wall.Width + 100     # through-cut with margin
void.Solid     = True
void.ViewObject.Visibility = False    # void shapes are always hidden

before = wall.Shape.Volume
wall.Subtractions = wall.Subtractions + [void]   # the live cut
doc.recompute()
after = wall.Shape.Volume
cut_m3 = (before - after) / 1e9
expected_m3 = (w_mm * h_mm * wall.Width.Value) / 1e9
print(f"cut={cut_m3:.4f} m3 expected~{expected_m3:.4f} m3 "
      f"-> {'PASS' if before > after else 'FAIL: NOTHING WAS CUT'}")
```

For a repeated facade pattern, build ONE void, then `Draft.make_ortho_array` /
`Draft.make_clone` it and subtract the array/clone — the bundled reference does exactly
this for its ribbed office facade (one `Extrude001` void, arrayed via `Array003` /
`Clone001`, both hidden, both in `wall.Subtractions`). One source shape edits the pattern.

`Arch.makeStructure` objects (footings, columns, beams) also expose `Subtractions`
**[verified]** — same technique cuts a service penetration through a beam or a sleeve
through a footing. **Every such penetration is a structural event**: it invalidates any
prior FEM result for that member (§7.4) and, in beams, may be prohibited in the tension
zone or near supports (`building-services-tga` + `concrete-detailing`). And cuts
re-index faces: re-dump (§3.8.2) after every change (G-06).

### 3.2 Floors and slabs

`Arch.makeFloor` creates the *storey* container (IfcType "Building Storey") — remember
its `Elevation` is set through `Placement.Base.z` (G-12). Slabs are elements inside it:

```python
slab = Arch.makeStructure(length=6000, width=4000, height=150, name="Slab_S1")
slab.IfcType = "Slab"
p = slab.Placement; p.Base = App.Vector(3000, 2000, 3050); slab.Placement = p
doc.recompute()
print(slab.Shape.BoundBox)   # CHECK NOW: "Slab" centers X/Y on Placement.Base (G-13)
```

The G-13 consequence for slabs: placed as if `Base` were a corner, the whole footprint
sits shifted by half its plan size — and a world-coordinate `Void_*` then cuts
**0.000 m³, no error**. Print BoundBox, fix Placement, then cut. Slab *thickness* is a
`structural-analysis` question; once chosen, model a real `Height` and verify
`V = L·W·H / 1e9` m³.

### 3.3 Columns, beams, footings, lintels — the makeStructure convention

`Arch.makeStructure(length, width, height, name)` produces a `Part::FeaturePython` that
accepts a real `IfcType` and exports correctly **[verified: `IFCFOOTING` in exported
.ifc]**. This is the one factory for rectangular structural elements.

```python
ftg = Arch.makeStructure(length=1500, width=1500, height=450, name="PadFooting_F1")
ftg.IfcType = "Footing"          # exports as IFCFOOTING  [verified]
doc.recompute()
assert round(ftg.Shape.Volume/1e9, 4) == 1.0125    # m3 — verify by volume, always
```

**Structural `IfcType` → FreeCAD object map:**

| Element | Factory | `IfcType` | IFC entity |
|---|---|---|---|
| Pad / isolated footing | `Arch.makeStructure` | `Footing` | `IFCFOOTING` **[verified]** |
| Strip / wall footing | `Arch.makeStructure` (long, thin) | `Footing` | `IFCFOOTING` |
| Raft / mat | `Arch.makeStructure` (full plan, thick) | `Footing` or `Slab` | `IFCFOOTING` / `IFCSLAB` *[unverified]* |
| Pile | `Arch.makeStructure` (cylinder base) | `Pile` | `IFCPILE` *[unverified]* |
| Pile cap | `Arch.makeStructure` | `Footing` | `IFCFOOTING` *[unverified]* |
| Plinth / grade beam (*Ringbalken*) | `Arch.makeStructure` | `Beam` | `IFCBEAM` |
| Column (*Stütze*) | `Arch.makeStructure` | `Column` | `IFCCOLUMN` |
| Beam / lintel (*Sturz*) | `Arch.makeStructure` | `Beam` | `IFCBEAM` |
| Slab | `Arch.makeStructure` | `Slab` | `IFCSLAB` |
| PCC / lean blinding | `Arch.makeStructure` | `Footing` (or plain solid, labelled) | — |
| Rebar | `Arch.makeRebar` | `Reinforcing Bar` | `IFCREINFORCINGBAR` **[verified]** |

**The centering rule (G-13, the one that eats half-days)** — verified on 1.0.1:

- **Column/Slab** (vertically extruded): X,Y **centered** on `Placement.Base`; Z
  **corner-based** (extends +Height upward).
- **Beam/Footing** (horizontally extruded): X **corner-based** (extends +Length);
  Y,Z **centered** on `Placement.Base`.

A lintel assuming corner-Z lands centered on its level — a 150 mm-deep lintel intended
with head at `z` sits 75 mm **too low**, dipping into its own opening. **Always print
`Shape.BoundBox` right after setting `Placement` and compare to intended world
coordinates.**

**Lintels.** Every window/door head under a load-bearing run requires a **lintel**
(`IfcType="Beam"`) — not floating masonry; an unlintelled opening is a structural
omission, and if left out goes under "Not modelled" in §7.3. Bearing lengths / edge
distances: `openings-windows-doors` + `masonry-construction` / `concrete-detailing`.

**Footings.** Type is a decision, not a default — route through `geotechnics-foundations`:

```
Geotechnical report with MEASURED allowable bearing pressure?
├─ NO  → you may NOT state a final size. Model a placeholder labelled
│         "ASSUMED <q> kPa — REQUIRES GEOTECH" and say so in the reply (§7.3).
└─ YES → q_allow known
    ├─ line load (wall)     → STRIP footing (practice rule width ≈ 2–3 × wall thickness)
    ├─ point load (column)  → PAD footing
    ├─ close/edge columns   → COMBINED — engineer
    ├─ pads > ~50 % of plan → RAFT — out of scope here, engineer
    ├─ weak/expansive soil  → PILES — out of scope here, engineer
    └─ retaining/sloping    → engineer (geotechnics-foundations)
```

Model out-of-scope cases as clearly-labelled placeholders if the user needs the massing —
never as if sized. Pad/strip sizing arithmetic (`A = P/q_allow`; **add footing
self-weight + overburden before declaring the bearing check passed** — the commonest
arithmetic omission; eccentricity limits) is owned by `geotechnics-foundations` +
`structural-analysis`. The modeling-side check that stays here:

```python
def check_strip_footing(ftg, wall_thk_mm, line_load_kN_per_m, q_allow_kPa,
                        min_width_factor=2.0, min_thk_mm=200):
    # min_thk/factors: PLACEHOLDER practice values — pass project minima from
    # geotechnics-foundations + concrete-detailing explicitly.
    B     = min(ftg.Length.Value, ftg.Width.Value)      # footing width, mm
    h     = ftg.Height.Value
    q_act = line_load_kN_per_m / (B / 1000.0)           # kPa
    rows = [
        (f"width >= {min_width_factor:g}x wall", B >= min_width_factor*wall_thk_mm,
         f"{B:.0f} vs {min_width_factor*wall_thk_mm:.0f} mm"),
        (f"thickness >= {min_thk_mm} mm", h >= min_thk_mm, f"{h:.0f} mm"),
        ("bearing q_act <= q_allow", q_act <= q_allow_kPa, f"{q_act:.0f} vs {q_allow_kPa:.0f} kPa"),
    ]
    for n, ok, v in rows:
        print(f"  [{'PASS' if ok else 'FAIL'}] {n}  {v}")
    return all(r[1] for r in rows)
```

**Model the PCC/lean layer** (typically 75–100 mm blinding under the footing) as a
separate solid: omitting it puts the cage at the wrong absolute elevation, cascading into
plinth and floor levels. Assign every foundation element to the **Foundation storey**
(§2.1).

**Plinth/grade beams — the element most often forgotten.** Isolated pads without a
plinth/grade beam tying them have no mechanism against differential settlement and no
path to distribute seismic base shear (`seismic-design`). Model as `IfcType="Beam"` on
the Plinth storey at/just below DPC, spanning pad-to-pad, wall-thickness wide × 225–300 mm
deep *[practice placeholder — owner: structural-systems]*. If omitted, list under "Not
modelled" in §7.3 — an absent tie beam is a real structural difference, not a detail level.

**Cover is modeled geometry, not a note.** Nominal cover comes from `concrete-detailing`
(exposure classes, Eurocode); it sets `makeRebar(offset=...)` (§3.4) and effective depth
`d = h − cover − (tie dia) − ø_main/2`. Model that arithmetic explicitly — wrong cover on
the earth face of a footing is the commonest way a modeled cage is quietly wrong.

### 3.4 Rebar cages as real parametric objects

> Scope: **how to build a cage in FreeCAD and measure it.** Min/max steel, cover tables,
> tie spacing, development lengths, laps, hooks, curtailment, bar bending schedules and
> confinement detailing are Eurocode rules owned by `concrete-detailing` (seismic:
> `seismic-design`). Numeric limits below are passed in as parameters or marked
> *[placeholder]* — design values are never owned by this file.

**`Arch.makeRebar(baseobj, sketch, diameter, amount, offset, name)`** **[verified]** —
needs a sketch attached to a host face describing one bar's path; replicates it `amount`
times and computes `Spacing` and `TotalLength` itself.

```python
import Part
ftg = doc.getObjectsByLabel("PadFooting_F1")[0]

sk = doc.addObject("Sketcher::SketchObject", "RebarPath_F1_B1")
sk.AttachmentSupport = [(ftg, "Face5")]      # Face5 = bottom face of a box  [verified]
sk.MapMode = "FlatFace"
doc.recompute()
sk.addGeometry(Part.LineSegment(App.Vector(-600,-600,0), App.Vector(600,-600,0)), False)
doc.recompute()

rb = Arch.makeRebar(ftg, sk, diameter=12, amount=7, offset=75, name="F1_Bottom_X")
doc.recompute()
print(rb.IfcType, rb.Amount, rb.Diameter, rb.Spacing, rb.TotalLength)
# -> Reinforcing Bar 7 12.0 mm 225.0 mm 8400.0 mm      [verified]
```

**[verified]** — properties: `Amount`, `Diameter`, `Direction`, `Distance`, `Host`,
`Mark`, `Material`, `OffsetStart`, `OffsetEnd`, `Rounding`, `Spacing`, `TotalLength`,
`IfcType = "Reinforcing Bar"`; exports as **`IFCREINFORCINGBAR`**.

Rules of use, each earned:

- `offset` = the **cover** from `concrete-detailing` (validated recipe used 75 for
  earth-cast); never 0.
- **`Direction` defaults to `(0,0,0)` → set it explicitly (G-14) [verified]**: with zero
  Direction, `amount=51, offset=75` on a 10287 mm strip returned `Spacing=3 mm` (bars
  spread over `2·offset`, not the host); setting `rb.Direction = App.Vector(0,1,0)` to the
  real replication axis gave `Spacing=202.7 mm`. Verify `Spacing ≈ L_host/(amount−1)`
  before trusting the cage — it never infers direction from sketch or host.
- `Spacing` is **derived**; to hit a target, `amount = floor((L − 2·cover)/s_target) + 1`.
  `TotalLength` is the authoritative bar-schedule quantity (take-off below).
- `host.Armatures` stays empty in the scripted path — check `rb.Host` (G-05).
- `OffsetStart`/`OffsetEnd` default **30 mm** — bars extend 30 mm past their wire endpoints;
  too short to be real lap/anchorage, so zero them unless modeling a lap deliberately
  (feeds G-15).
- `Rounding` = bend radius as **multiple of bar diameter** *[unverified]*; minimum bend per
  `concrete-detailing` — 0 models an unbuildable sharp bend. `Mark` = bar mark
  (`F1-B1`, `C1-MAIN`, `B2-STIRRUP`) so the take-off reads.
- A full cage = **two orthogonal bottom mats** (one sketch per direction) + top steel
  where continuous/cantilevered.

**Stirrups/ties = closed-loop sketch** on a cross-section face, replicated along the
member axis *[unverified pattern — follows from verified straight-bar behaviour]*:

```python
col = doc.getObjectsByLabel("Column_C1")[0]      # 300 x 300 x 3000
sk = doc.addObject("Sketcher::SketchObject", "TiePath_C1")
sk.AttachmentSupport = [(col, "Face5")]          # bottom cross-section face
sk.MapMode = "FlatFace"
doc.recompute()
c = 40                                           # cover to tie — per concrete-detailing
a, b = 150 - c, 150 - c
pts = [App.Vector(-a,-b,0), App.Vector(a,-b,0), App.Vector(a,b,0), App.Vector(-a,b,0)]
for i in range(4):
    sk.addGeometry(Part.LineSegment(pts[i], pts[(i+1) % 4]), False)
doc.recompute()
# amount from the tie-spacing rule in concrete-detailing, not from taste:
tie = Arch.makeRebar(col, sk, diameter=10, amount=11, offset=40, name="C1_Ties")
tie.Direction = App.Vector(0, 0, 1)              # replicate along the column axis (G-14)
tie.Mark = "C1-TIE"
tie.Rounding = 4          # multiple of dia  [unverified]
doc.recompute()
```

Seismic zones require **135°-hooked closed ties** in confinement zones
(`seismic-design` + `concrete-detailing`); `makeRebar` will not model hooks from a plain
rectangle — state hooks **not modelled** rather than implying a complete detail.

**Containment tolerance (G-15) [verified]:** endpoints sitting at a host's bbox limits do
NOT keep the bar inside — (1) the default 30 mm end offsets, and (2) even zeroed, a
stirrup flush with a member end pokes **half the bar diameter** past the endpoint (4 mm
for Ø8) — correct geometry, not a defect. **Any bbox-containment check needs tolerance
`bar_diameter/2 + margin`,** or correctly-detailed end stirrups false-FAIL.

```python
import math
BAR_AREA = {8: 50.3, 10: 78.5, 12: 113.1, 16: 201.1, 20: 314.2, 25: 490.9, 32: 804.2}

def check_min_steel(dia_mm, amount, width_mm, thickness_mm, rho_min):
    # rho_min per concrete-detailing (min flexural / shrinkage-temp ratio for the steel
    # class) — never hard-code from memory; pass it in.
    as_prov = amount * math.pi * (dia_mm ** 2) / 4
    as_min  = rho_min * width_mm * thickness_mm
    ok = as_prov >= as_min
    print(f"  As_prov={as_prov:.0f} mm2  As_min={as_min:.0f} mm2  -> {'PASS' if ok else 'FAIL'}")
    return ok

def check_max_spacing(spacing_mm, limit_mm):
    # limit_mm = min(k1*h, cap) with k1/cap per concrete-detailing.
    ok = spacing_mm <= limit_mm
    print(f"  spacing={spacing_mm:.0f}  limit={limit_mm:.0f} mm -> {'PASS' if ok else 'FAIL'}")
    return ok

def check_column_rebar(b_mm, h_mm, dia_long, n_long, dia_tie, tie_spacing_mm,
                       rho_min, rho_max, tie_limit_mm, n_min=4):
    # rho limits + tie spacing limit per concrete-detailing; the classic forms
    # (1–8% ratio; min(16d_long, 48d_tie, least dim)) must be CONFIRMED there, not
    # lifted from this file.
    rho = n_long * math.pi * dia_long**2 / 4 / (b_mm * h_mm)
    rows = [
        ("rho_g >= rho_min", rho >= rho_min, f"{rho*100:.2f}%"),
        ("rho_g <= rho_max", rho <= rho_max, f"{rho*100:.2f}%"),
        (f"n_long >= {n_min}", n_long >= n_min, f"{n_long}"),
        ("tie spacing <= limit", tie_spacing_mm <= tie_limit_mm,
         f"{tie_spacing_mm:.0f} vs {tie_limit_mm:.0f} mm"),
    ]
    for n, ok, v in rows:
        print(f"  [{'PASS' if ok else 'FAIL'}] {n}  {v}")
    return all(r[1] for r in rows)
```

Audit catching a silent error (illustrative `rho_min = 0.0018` placeholder — project
value from `concrete-detailing`): 1500×1500×450 pad, per direction `A_g = 675,000 mm²` →
`A_s,min = 1215 mm²`; modeled 7×Ø12 = `792 mm²` → **FAILS by 35 %**; fix 7×Ø16 or 11×Ø12
at 135 mm. Run it on **every** rebar object — short cages are what this audit exists to
catch.

```python
def audit_all_rebar(doc):
    """Over every rebar object in the document. Run before every handoff."""
    bad = []
    for o in doc.Objects:
        if getattr(o, "IfcType", None) == "Reinforcing Bar":
            host = o.Host
            print(f"{o.Label}  host={host.Label if host else 'NONE'}  "
                  f"dia={o.Diameter}  n={o.Amount}  s={o.Spacing}  L={o.TotalLength}")
            if host is None:
                bad.append((o.Label, "no host"))
            if o.OffsetStart.Value == 0 and o.OffsetEnd.Value == 0 and o.Mark == "":
                bad.append((o.Label, "zero end offsets and no mark — check intent (G-15)"))
    for lbl, why in bad:
        print(f"  [FAIL] {lbl}: {why}")
    return not bad

def steel_takeoff(doc):
    """TotalLength is authoritative [verified] — use it, don't re-derive."""
    total_kg = 0.0
    for o in doc.Objects:
        if getattr(o, "IfcType", None) == "Reinforcing Bar":
            L_m = o.TotalLength.getValueAs("mm").Value / 1000.0
            d   = o.Diameter.getValueAs("mm").Value
            kg  = L_m * (d*d) / 162.0        # generic site formula: mass_per_m = d²/162 kg/m
            total_kg += kg
            print(f"{o.Mark or o.Label:<16} Ø{d:.0f}  {L_m:7.2f} m  {kg:7.1f} kg")
    print(f"TOTAL STEEL (model geometry only, NO laps/hooks/wastage): {total_kg:.0f} kg")
    return total_kg
```

**This is a model quantity, not a BOQ.** Laps, hooks, chairs, wastage per
`cost-management-din276`; never hand this number over as a steel order.

### 3.5 Windows and doors — BIM object separate from the cut

Build the opening (void + `Subtractions`, §3.1) and the `Arch.makeWindow`/`makeDoor` BIM
object as **two separate things at the same location** — this matches the bundled
reference exactly (its real windows have `Hosts: None` yet export as valid `IFCWINDOW`;
the void already did the cutting).

```python
win = Arch.makeWindow(1150, 2100, name="Win_W1-N01")   # width, height
win.IfcType = "Window"   # or "Door" — same factory family, different IfcType string
win.Placement = App.Placement(App.Vector(x, y, z_sill), App.Rotation(App.Vector(0,0,1), wall_angle))
```

**Record every opening's parameters the moment you create it** — `label, type, W, H,
sill, wall angle, world pos, void label` into a JSON store from `execute_code` (§6.2);
corrupted openings are **deleted and rebuilt**, never patched (G-16/G-17).

**Frame fidelity ladder:** (1) plain box — acceptable schematic pass, known
simplification; (2) multi-part `WindowParts` — the reference windows have `OuterFrame`,
`Frame`, `Glass`, `Glass panel` as distinct named sub-shapes with real profiles: generate
one realistic template via the GUI's Window preset picker (or `insert_part_from_library`,
G-34) and reuse it programmatically (§2.6). A box is a pass, not the ceiling of Arch.

**The two door/window placement killers [verified]** — mechanics here, full rules at
G-16/G-17:

- **G-16 `Normal` corruption → Null shape:** a degenerate/zero `Normal` fails the shape
  build (object present, geometry gone); patching it back to default `(0,0,-1)` yields a
  **non-null but insane** flat "skylight" leaf. **"Not null" ≠ "geometrically sane"** —
  verify BoundBox vs the `Void_*`, else delete & rebuild (§6.2).
- **G-17 `Base`-sketch `Placement` is a no-op:** rotating/moving `door.Base.Placement` +
  recompute gives an identical `Shape.BoundBox` — the proxy ignores it. **Only the
  object's own `Placement` moves the built shape.** Standing a flat-built door upright:

```python
d.Placement = App.Placement()          # 1. identity, then raw bbox
doc.recompute()
bb, H = d.Shape.BoundBox, d.Height.Value
if abs(bb.XLength - H) < 5:            # 2. which local horizontal axis carries Height?
    rot = App.Rotation(App.Vector(0,1,0), -90)     # X -> tip up about Y
elif abs(bb.YLength - H) < 5:
    rot = App.Rotation(App.Vector(1,0,0), 90)      # Y -> tip up about X
else:
    rot = None; print("FAIL: neither span matches Height — inspect before touching")
if rot is not None:
    d.Placement = App.Placement(App.Vector(), rot); doc.recompute()
    vb = doc.getObjectsByLabel("Void_D-G01")[0].Shape.BoundBox   # 3. translate to void center
    nc = d.Shape.BoundBox.Center
    p = d.Placement
    p.Base = App.Vector(vb.Center.x - nc.x, vb.Center.y - nc.y, vb.Center.z - nc.z)
    d.Placement = p; doc.recompute()
# 4. verify final bbox INSIDE the void bbox (small tolerance), per axis
```

**Never batch-apply a "best-guess" rotation from sorted span magnitudes** — it can't
disambiguate the two valid rotation axes and misplaces doors with similar spans (confirmed:
one such batch attempt produced **10/12 wrong results**, re-breaking an already-verified
door). Per-object Height-axis identification, per-object verification. (Lintels over
openings: §3.3.)

### 3.6 Stairs — the comfort envelope is not a code check

Comfort guidance (riser 140–180 mm, tread 270–340 mm, `2R + T ≈ 600–650 mm`, from the
bundled reference study) is an envelope, **not a code check**. **Hard gates (max riser;
min tread with/without nosing; headroom; clear width; handrail height; landing length;
winder and guard rules) are owned by `stairs-vertical-circulation`** (beyond-minimum
access: `accessibility-universal-design`); this file owns that FreeCAD's stair object
silently fights those gates, and that the check must be scripted and run every time.

**FreeCAD's stair derivation [verified]:**

```
RiserHeight = Height / NumberOfSteps
TreadDepth  = Length / (NumberOfSteps - 1)
Nosing      defaults to 0.0 mm        <- the trap (G-10)
```

`Arch.makeStairs(length=4200, width=1100, height=3000, steps=17)` [verified] gives
`RiserHeight = 176.47 mm`, `TreadDepth = 262.5 mm`, `Nosing = 0.0`:

- Comfort `2R+T = 615.4` → "passes". Riser gate ✓. **Tread gate ✗** — with `Nosing = 0`
  the *larger* no-nosing minimum applies (279 mm in the reference regulation used during
  validation) and 262.5 < 279.
- **Fix:** set `Nosing = 25` (with-nosing minimum then applies, 262.5 ✓), or lengthen the
  flight: `Length = 280 × 16 = 4480 mm` for a 280 mm tread.

To hit a target tread with fixed floor-to-floor height `H`: `N = ceil(H / R_max)`
(`R_max` from `stairs-vertical-circulation`), `G = T_target × (N − 1)` — if the plan
offers less going than `G`, the stair **cannot** be one straight legal flight; it needs a
landing/dog-leg or the check fails. Say that; never silently shrink the tread.

**G-19 — stairs rotation/BoundBox:** `makeStairs` extends the flight along +X from
`Placement.Base`; `Placement.Rotation` rotates **about the Base point, not the flight's
centre**, so the flight swings off its stairwell sideways while still looking "placed".
Rotate first, then correct `Placement.Base` until `Shape.BoundBox` matches the stairwell
footprint — a stair whose bbox center is 1400 mm from its shaft is not "close enough"
(same pivot logic for the rotated roof slab, §3.7).

**Assertion script — run after every `makeStairs`.** Limits are *parameters*; the values
validated with this recipe (196 / 254 / 279 / 914 / 2032 / 3835 / 914 / 19–32 mm) are
example defaults — **confirm against `stairs-vertical-circulation` before any PASS:**

```python
def check_stair_gates(st, lim, headroom_mm=None, n_handrails=0, landing_len_mm=None):
    # lim: dict(riser_max, tread_min_nosing, tread_min_no_nosing, width_min,
    #           headroom_min, rise_max, landing_min, nosing_min, nosing_max, comfort=(lo,hi))
    R = st.RiserHeight.getValueAs("mm").Value; T = st.TreadDepth.getValueAs("mm").Value
    N = st.Nosing.getValueAs("mm").Value;      W = st.Width.getValueAs("mm").Value
    H = st.Height.getValueAs("mm").Value
    t_min = lim["tread_min_nosing"] if N > 0 else lim["tread_min_no_nosing"]
    checks = [
        ("riser <= riser_max",        R <= lim["riser_max"],                      f"{R:.1f}"),
        (f"tread >= {t_min:.0f} mm",  T >= t_min,                                 f"{T:.1f} (nosing {N:.0f})"),
        ("width >= width_min",        W >= lim["width_min"],                      f"{W:.0f}"),
        ("rise/landing <= rise_max",  H <= lim["rise_max"],                       f"{H:.0f}"),
        ("comfort 2R+T",              lim["comfort"][0] <= 2*R+T <= lim["comfort"][1], f"{2*R+T:.1f}"),
        ("total rise matches",        abs(st.NumberOfSteps*R - H) < 1.0,          ""),
        ("nosing within band",        (lim["nosing_min"] <= N <= lim["nosing_max"]) if N > 0 else None, f"{N:.0f}"),
        ("headroom >= headroom_min",  (headroom_mm >= lim["headroom_min"]) if headroom_mm is not None else None,
                                      f"{headroom_mm:.0f}" if headroom_mm is not None
                                      else "NOT MEASURED - check against slab/soffit above"),
        ("landing >= landing_min",    (landing_len_mm >= lim["landing_min"]) if landing_len_mm is not None else None,
                                      f"{landing_len_mm:.0f}" if landing_len_mm is not None else "NO LANDING MODELLED"),
        ("handrail present",          n_handrails >= 1,                           f"{n_handrails} modelled"),
    ]
    for name, ok, val in checks:
        print(f"  [{'PASS' if ok else ('----' if ok is None else 'FAIL')}] {name}  {val}")
    unresolved = [c[0] for c in checks if c[1] is None]
    if unresolved:
        print(f"  UNRESOLVED (must be stated in the reply): {', '.join(unresolved)}")
    return all(c[1] for c in checks if c[1] is not None), unresolved
```

**Headroom depends on the slab/soffit above, not the stair object** — measure it in the
model or the §7.3 block reads **NOT MEASURED**, never "assumed OK" [unverified — standard
OCC raycast, not round-tripped here]:

```python
def measure_headroom(stair, obstructions):
    """obstructions: solids above (slabs, landings, beams). Returns min clearance mm."""
    import Part
    R = stair.RiserHeight.getValueAs("mm").Value; T = stair.TreadDepth.getValueAs("mm").Value
    base = stair.Placement.Base; n = int(stair.NumberOfSteps); worst = float("inf")
    for i in range(n):
        p = App.Vector(base.x + i*T, base.y + stair.Width.Value/2, base.z + (i+1)*R)
        ray = Part.makeLine(p, App.Vector(p.x, p.y, p.z + 6000))
        for ob in obstructions:
            for v in ob.Shape.common(ray).Vertexes:
                worst = min(worst, v.Point.z - p.z)
    print(f"  min headroom = {worst:.0f} mm")
    return worst
```

**Stair as structural member:** an RC flight is an inclined slab (cantilevered or
simply-supported between landings) carrying its own considerable weight plus imposed load
— a commonly under-designed element; waist ~125–175 mm *[practice placeholder — sizing
per `structural-analysis`]*. If presented as viable: §3.8 treatment via a `Part::Box`
proxy of the waist slab at the developed span, stated (§3.8.10). `makeStairs` models **no
handrails** — absence is a code failure, not a rendering choice; list it. Flight/landing
bar geometry → `concrete-detailing`.

### 3.7 Roof — structural layer first, build-up second

Model the load-bearing roof as classified structure; the layered build-up (vapour,
insulation, underlay, counter-batten, covering) is `roofing-waterproofing` +
`building-physics-thermal-moisture`. Either model layers as separate thin `Slab` solids
at real thicknesses (LOIN call, §2.5) or model structure only and **say so**.

```python
# Mono-pitch RC roof slab, 5 deg about the eave (Y) axis
roof = Arch.makeStructure(length=6200, width=9200, height=180, name="RoofSlab_R1")
roof.IfcType = "Slab"
p = App.Placement()
p.Rotation = App.Rotation(App.Vector(0, 1, 0), -5.0)      # sign = falls toward -X
p.Base = App.Vector(0, 0, 6400)
roof.Placement = p
doc.recompute()
bb = roof.Shape.BoundBox                                   # G-13: Slab centers X/Y on Base
expected_rise = 6200 * math.tan(math.radians(5))           # run * tan(alpha)
print(f"[{'PASS' if abs(bb.ZLength - (180 + expected_rise)) < 20 else 'FAIL'}] "
      f"pitch rise {bb.ZLength-180:.0f} vs {expected_rise:.0f} mm")
```

The z-span check is verify-by-measurement made roof-specific: if the rotation pivoted at
the wrong point (G-19), the BoundBox says so immediately. Parapets = `IfcType="Beam"`
edge strips; water-tank base = `Slab` + the tank as a **load from the §3.8.1 take-down**,
never an invented force. Trussed/purlin roofs: `Beam`/`Member` frames along the
`structural-systems` load path. Roof penetrations (flues, PV ballast, drainage) are
coordination events — each a `Subtractions` cut and a §7.4 FEM-invalidator when it hits
structure.

### 3.8 Load derivation and FEM verification — the actual pipeline

#### 3.8.1 Load take-down before solver — **never invent a force value**

Every `ConstraintForce`/`ConstraintPressure` must trace to a written take-down.

- Load values, ULS/SLS combinations and the roof-to-soil path are owned by
  **`structural-analysis`** (system + preliminary span/depth tables: `structural-systems`).
  **Cross-check every member against `structural-systems`' preliminary sizing before
  treating the take-down as final** — disagreement over ~15–20 % must be stated and
  resolved, never averaged or cherry-picked.
- **Run stress and deflection as separate analyses** (ULS-type factors for stress,
  service for deflection — per `structural-analysis`). Factored-load deflection against a
  span/limit ratio is meaningless; service-load stress against factored capacity is
  unconservative. Crossing them is common and invisible.
- **Bearing checks use unfactored service loads** (`geotechnics-foundations`) and
  **include footing self-weight + overburden** before PASS.
- Screening unit weights used in validated examples (real values per
  `building-materials`): RC ≈ 24, plain concrete 23, masonry 18–20, water 9.81,
  steel 77 kN/m³; residential floor imposed ~2 kPa class, roof ~0.5 kPa class —
  project values come from `structural-analysis`, not this line.
- **Gravity-only: wind and seismic are out of scope — say so.** For a real occupied
  building in a seismic region, actually invoke `seismic-design` (or confirm it ran)
  before calling anything "checked"; otherwise §7.3 carries its own line *"lateral/
  seismic: NOT evaluated — seismic-design not invoked"*, not a buried bullet.

```
w_area (kPa)  ->  w_line (kN/m) = w_area x tributary_width
              ->  F_total (kN)  = w_line x span   ->  N = F_total x 1000
```

Validated-run example: RC beam 3.0 m span, 3.0 m tributary width, 150 mm slab +
finishes → dead ≈ 4.80 kPa, live 1.92 kPa, factored ≈ 8.83 kPa → 26.5 kN/m → **79.5 kN**.
The *solver calibration run itself* used a deliberately lighter 21.6 kN (clean hand-check
arithmetic, uncracked concrete) — substitute the real factored load for work. Build the
**full roof-to-soil column load table once per house** (each storey's slab dead +
finishes + walls + live → running axial at footing, then footing self-weight) and **print
it alongside any footing size stated** — a size with no visible take-down is an
unsupported claim even when the off-screen arithmetic was right.

| Physical load | FEM constraint | Value computation |
|---|---|---|
| UDL on beam top face | `ConstraintForce` top face | N = w_line (N/mm) × span (mm); solver distributes over face |
| Area load on slab | `ConstraintPressure` top face | MPa = kPa/1000: 8.83 kPa → `"0.00883 MPa"` |
| Point load (column onto beam) | `ConstraintForce` on partitioned face / vertex | partition first, or accept local stress artifact |
| Self-weight | `ConstraintSelfWeight` | needs `Density` on material; add whenever non-trivial |
| Axial on column | `ConstraintForce` top face, `Reversed=True` | service/factored N from take-down |
| Soil reaction under footing | `ConstraintPressure` bottom face (upward) | q_act in MPa, paired with column load on top |

**Pressure unit trap (G-21):** 8.83 kPa = 0.00883 MPa; a bare `8.83` equals that in
internal units **by accident** — the coincidence does not generalise. Always the string.

#### 3.8.2 Verify face indices before binding constraints — never assume

A constraint bound to the wrong face yields a **fully successful solve with meaningless
numbers** — the highest-severity silent failure here.

```python
def dump_faces(obj):
    for i, f in enumerate(obj.Shape.Faces, 1):
        c = f.CenterOfMass
        print("Face%-3d center=(%8.1f, %8.1f, %8.1f) area=%10.0f mm2" % (i, c.x, c.y, c.z, f.Area))

# Part::Box 3000x300x450 ->  [verified]
# Face1 (0,150,225)     Face2 (3000,150,225)   <- ends
# Face3 (1500,0,225)    Face4 (1500,300,225)   <- sides
# Face5 (1500,150,0)    Face6 (1500,150,450)   <- bottom, top

def assert_face(obj, name, cx=None, cy=None, cz=None, tol=1.0):
    idx = int(name.replace("Face", "")) - 1
    c = obj.Shape.Faces[idx].CenterOfMass
    for want, got, ax in ((cx, c.x, "x"), (cy, c.y, "y"), (cz, c.z, "z")):
        if want is not None and abs(want - got) > tol:
            raise AssertionError(f"{name} {ax}-center {got:.1f} != expected {want:.1f}")
    print(f"  [PASS] {name} confirmed at ({c.x:.0f},{c.y:.0f},{c.z:.0f})")
```

`Part::Box` face order **is** stable and confirmed empirically (G-20), but re-run
`dump_faces` after **any** boolean — cuts re-index faces (G-06). Assert center+area
**before** attaching anything.

#### 3.8.3 What `run_fem_analysis` does and does not do (G-26)

`run_fem_analysis(doc_name, analysis_name, timeout=..., include_screenshot=...,
view_name=...)` **only solves an already-assembled analysis** — it creates nothing
except `SolverCcxTools`. Build first:

1. A Part-derived solid — `Part::Box` proxy or Arch object (`Part::FeaturePython`)
   directly **[verified: gmsh meshed an `Arch.makeStructure` footing to 237 nodes]**.
2. `Fem::FemAnalysis` via `ObjectsFem.makeAnalysis(doc, "Name")` — accepted **[verified]**.
3. Material — `ObjectsFem.makeMaterialSolid`, added to the analysis.
4. ≥1 `Fem::ConstraintFixed` **and** ≥1 `Fem::ConstraintForce`/`ConstraintPressure` bound
   to §3.8.2-verified faces, added to the analysis.
5. `Fem::FemMeshGmsh` referencing the geometry, added, **with the mesh actually generated**.

Returns `max_von_mises_MPa`, `min_von_mises_MPa`, `max_displacement_mm`, `node_count`,
`working_dir`, `result_object`. **No safety factor is returned** — compute it yourself
(§3.8.6); any claim of a solver-reported SF is wrong for this environment.

Operational: the solve runs **synchronously on the GUI thread and blocks every other
call** (G-28); ~3000-node members solve in seconds but a full-building mesh times out —
**analyse one member at a time**; request `timeout` per budget with client ≥ 2×timeout+30
(G-33); `include_screenshot=False` for numeric runs; repeated runs pile up
`CCX_Results*` — clean or read newest (G-09, §3.8.8).

**What the pipeline structurally cannot tell you** — state every line as not-checked in
§7.3:

```
buckling (linear static only)      punching shear        cracking / tension stiffening
long-term deflection / creep       reinforcement bond     connection capacity
fatigue                            lateral / seismic      wind
torsional stability                soil-structure interaction    settlement
construction-stage loading         thermal / shrinkage restraint
```

#### 3.8.4 The full working script [verified end-to-end]

```python
import FreeCAD as App, ObjectsFem
from femmesh.gmshtools import GmshTools

doc  = App.newDocument("BeamCheck")
beam = doc.addObject("Part::Box", "BeamProxy")
beam.Length, beam.Width, beam.Height = 3000, 300, 450   # mm
doc.recompute()
dump_faces(beam)                      # §3.8.2 — assert before binding

analysis = ObjectsFem.makeAnalysis(doc, "BeamCheck")

mat = ObjectsFem.makeMaterialSolid(doc, "ConcreteC30")
m = mat.Material
m['Name']          = 'Concrete-C30/37'
m['YoungsModulus'] = '30000 MPa'      # §3.8.5 on choosing E
m['PoissonRatio']  = '0.20'
m['Density']       = '2400 kg/m^3'
mat.Material = m
analysis.addObject(mat)

fix = ObjectsFem.makeConstraintFixed(doc, "FixedEnd")
fix.References = [(beam, "Face1")]
analysis.addObject(fix)

frc = ObjectsFem.makeConstraintForce(doc, "FloorLoad")
frc.References = [(beam, "Face6")]
frc.Force    = "21600 N"      # from the take-down. ALWAYS a unit string.
frc.Reversed = True           # Face6 normal is +Z, so Reversed => downward
analysis.addObject(frc)

msh = ObjectsFem.makeMeshGmsh(doc, "BeamMesh")
msh.Shape                   = beam
msh.CharacteristicLengthMax = "120 mm"
msh.ElementOrder            = "2nd"     # REQUIRED for bending accuracy (G-11)
analysis.addObject(msh)
doc.recompute()
GmshTools(msh).create_mesh()
print("nodes:", msh.FemMesh.NodeCount, "volumes:", msh.FemMesh.VolumeCount)
# -> nodes: 2713 volumes: 1334   [verified]
```

Then: `run_fem_analysis(doc_name="BeamCheck", analysis_name="BeamCheck",
include_screenshot=False, timeout=300)` — actual verified return:

```json
{"success": true, "max_von_mises_MPa": 3.1926, "min_von_mises_MPa": 0.00042,
 "max_displacement_mm": 1.0909, "node_count": 2713,
 "working_dir": "/tmp/freecad_mcp_fem_ax8l10hu"}
```

Constraint reference — all **[verified]**:

| Constraint | Factory | Key properties |
|---|---|---|
| Fixed | `makeConstraintFixed` | `References` |
| Force | `makeConstraintForce` | `Force`, `Direction`, `Reversed`, `References` |
| Pressure | `makeConstraintPressure` | `Pressure`, `Reversed`, `Scale`, `References` (pass `"0.005 MPa"`) |
| Self-weight | `makeConstraintSelfWeight` | `GravityAcceleration`, `GravityDirection` |
| Displacement | `makeConstraintDisplacement` | per-axis fix/free — the tool for releasing rotation at a real simple support (§3.8.7) *[unverified property names]* |

#### 3.8.5 Calibrate against hand calculation — mandatory, every time

An uncalibrated solver run **is not evidence**. Validated case (cantilever,
`w = 7.2 N/mm`, `b = 300`, `h = 450`, `L = 3000`, `E = 30000 MPa`):

| Quantity | Hand calculation | FEM | Δ |
|---|---|---|---|
| Bending stress | `M = wL²/2 = 32.4×10⁶ N·mm`; `S = bh²/6 = 10.125×10⁶ mm³`; `σ = 3.20 MPa` | **3.193 MPa** | **0.2%** |
| Tip deflection | `I = bh³/12 = 2.278×10⁹ mm⁴`; `δ = wL⁴/8EI = 1.067 mm` | **1.091 mm** | **2.3%** (shear deformation) |

The hand side is exactly what **`structural-analysis`** owns — run its method (or pull
its result) first, then compare the solver against it. Closed forms for calibration
(UDL `w` N/mm, span `L` mm; `σ = M/S`, `S = bh²/6`, `I = bh³/12`):

| Case | M_max | δ_max |
|---|---|---|
| Cantilever, UDL | `wL²/2` (support) | `wL⁴/(8EI)` |
| Cantilever, tip point load P | `PL` | `PL³/(3EI)` |
| Simply supported, UDL | `wL²/8` | `5wL⁴/(384EI)` |
| Simply supported, midspan P | `PL/4` | `PL³/(48EI)` |
| Fixed-fixed, UDL | `wL²/12` support, `wL²/24` mid | `wL⁴/(384EI)` |
| Propped cantilever, UDL | `wL²/8` (fixed end) | `wL⁴/(185EI)` *[unverified]* |

**Acceptance:** Δ > ~10 % means **the model is wrong, not statics** — wrong face, load
direction, unit error, coarse mesh, or 1st-order elements (G-11). Fix before reporting.

**Modulus:** the run used `E = 30000 MPa` for C30/37; the class's secant modulus is the
`E_cm` value `concrete-detailing` carries, somewhat **below** 30 GPa — and E **directly
scales deflection** (≈ +17 % on the lower value). State which E was used. Deflection
limits and combinations: `structural-analysis`; this FEM gives **immediate elastic**
deflection only — long-term multipliers are not modeled.

#### 3.8.6 Material presets and interpretation — where von Mises lies

| Material | E (MPa) | ν | ρ (kg/m³) | Compare against |
|---|---|---|---|---|
| Structural steel (S275-class) | **210,000** | **0.30** | **7800** | yield (thickness-dependent — `timber-steel-design`); von Mises valid |
| Reinforcing steel (B500-class) | 200,000 | 0.30 | 7850 | yield per `concrete-detailing` |
| Concrete C30/37 | §3.8.5 (`E_cm` from `concrete-detailing`) | 0.20 | 2400 | rows below |
| Brick masonry | 3,000–8,000 *[unverified]* | 0.15–0.20 | ~1900 | compression only; tension ≈ 0 — von Mises meaningless |
| Softwood (∥ grain) | ~11,000 *[unverified]* | 0.35 | 500 | **orthotropic** — isotropic FEM a poor model |

```python
SF = f_yield / max_von_mises        # steel only
```

| Material | Criterion | Verdict rule |
|---|---|---|
| Structural steel | von Mises vs yield | `SF = f_y/σ_vm`; screening target per `timber-steel-design`; name it hand-adopted, never "solver-reported" |
| Concrete, tension | `f_ct` for the class **from `concrete-detailing`** (validated run recorded 3.40 MPa for C30/37 — that run's threshold, not a universal) | von Mises is **NOT** a concrete criterion; compare **max principal tensile stress** to `f_ct`; exceedance = "it cracks", not "it fails" |
| Concrete, compression | service cap per `concrete-detailing` | screening only |
| Masonry / timber | — | isotropic linear FEM invalid; **no safety factor may be reported** |

Validated beam: `σ_max = 3.193 MPa` vs recorded `f_ct = 3.40 MPa` → **marginally
uncracked, ~6 % margin** — at the real factored load (~3.7×) it would crack decisively,
normal for RC and precisely why a linear-elastic uncracked FEM **cannot** verify an RC
member: **it says whether the section cracks, not whether the reinforced section is
adequate afterwards.**

**Columns:** linear static FEM gives axial stress, **not buckling**. Euler hand-check,
reported *as hand-check*: `P_cr = π²EI/(kL)²` (`k` = 1.0 pinned-pinned, 0.5 fixed-fixed,
2.0 cantilever); `r = √(I/A) = 0.3h` for a rectangle; whether `kLu/r = 33.3` (300×300,
3 m, k=1) is stocky is the braced/unbraced threshold rule in `structural-analysis`.

**Mesh convergence:** one run = one data point. Re-run at ~half `CharacteristicLengthMax`;
peak stress moving > **~5 %** → unconverged → not reportable. Fixed-support peak stress is
a **mesh-dependent singularity** (G-24) that grows as the mesh refines — read ~1
member-depth away or label the peak a support artifact.

#### 3.8.7 Boundary conditions — the commonest wrong-but-plausible answer

| Real condition | Wrong idealization | Consequence | Do instead |
|---|---|---|---|
| Simply supported beam | Fixed **both** ends | `wL²/24` vs `wL²/8` — **understates bending ~3×**; dangerously unconservative | `ConstraintDisplacement` releasing rotation, or model as cantilever and accept conservatism |
| Beam on masonry bearing | Fixed | overstates restraint, understates deflection | partial `ConstraintDisplacement` |
| Continuous beam over middle support | one span in isolation | misses hogging | model both spans or hand-check hogging |
| Column base on pad footing | Fixed | overstates fixity, understates sway | OK for axial-only screening; **never** lateral |
| Slab on 4 walls | Fixed all edges | overstates two-way stiffness | pinned edges = conservative screen |
| Forces only, no fixed constraint | solver "succeeds" | rigid-body motion, garbage displacements | ≥1 `ConstraintFixed` mandatory |

**When in doubt, choose the conservative idealization and say which one.** "Modelled as
a cantilever (conservative); real condition partially restrained" is honest. "The beam
is fine" is not.

#### 3.8.8 Solver troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Prerequisite-check error | missing material/mesh/constraint/analysis membership | re-check §3.8.3 list; confirm objects in `analysis.Group` |
| Displacement in metres | rigid-body motion; fixed face not restraining all 6 DOF | add/extend `ConstraintFixed` |
| `nonpositive jacobian` (ccx) | degenerate mesh from a sliver face after a boolean | change `CharacteristicLengthMax`; `Part::Box` proxy (§3.8.10) |
| gmsh fails on Arch object | many `Subtractions`, compound/multi-solid | proxy box + state simplification |
| Stress 1000× expected | bare-float pressure/force | unit strings (§2.7, G-21) |
| Right numbers, wrong axis | `Reversed` unset / wrong `Direction` | check face normal; +Z top face needs `Reversed=True` for downward |
| Deflection ~2× hand-check | `ElementOrder="1st"` | `"2nd"` (G-11) |
| Timeout | mesh too fine / whole building | one member, coarsen, only then raise `timeout` |
| 2nd run = 1st run's numbers | stale `CCX_Results` (G-09) | delete old or read highest-numbered |
| `get_rpc_status` → `stuck` | GUI thread blocked | §6.1; restart; stop queueing |

```python
# clean result objects between runs
for o in list(doc.Objects):
    if o.Name.startswith("CCX_Results") or o.Name.startswith("ResultMesh"):
        doc.removeObject(o.Name)
doc.recompute()
```

#### 3.8.9 The thin-member mesh cap (G-18) — the rule that saves the session

**Mesh size on thin cantilevers can hang the GUI thread indefinitely, with no clean
cancel** [verified]: an uncapped `CharacteristicLengthMax` on a large thin member (a
canopy-style proxy, huge face-area-to-thickness ratio) produced a mesh in the **hundreds
of thousands of nodes**; the solve held the GUI dispatch thread past its stated timeout
(`get_rpc_status` `state:"stuck"` climbing past 1000+ s) and eventually **crashed the
FreeCAD process**, losing every unsaved change. Therefore:

1. **Generate the mesh yourself first** (`GmshTools(msh).create_mesh()`); check
   `msh.FemMesh.NodeCount` is low-thousands-to-tens-of-thousands **before** calling
   `run_fem_analysis` — never let an uncapped mesh go straight to the solver.
2. On thin members cap `CharacteristicLengthMax` at a few elements across the thickness
   (or shrink the analysed region), and state the idealization.
3. If `get_rpc_status` shows `stuck` on a FEM task: **stop queueing** — it cannot be
   safely cancelled; even `doc.save()` fails with "GUI dispatch unavailable" until
   restart (§6.1). After restart, **verify object counts before assuming anything was
   lost** — crash recovery may have preserved work; check, don't assume.

#### 3.8.10 Proxy vs BIM object, and which members deserve a solve

Gmsh meshes Arch objects directly **[verified]** — prefer it: BIM object and analysed
object are one object and cannot drift apart. Fall back to a `Part::Box` proxy for members
with many `Subtractions` where gmsh fails/degenerates, compounds, or a deliberately
conservative gross section — and **say so in the reply** ("checked as a 300×450 gross
rectangle; two Ø100 midspan penetrations not modelled"). A quiet proxy is the FEM
equivalent of a stale result. Prioritise solves (never pretend to check everything):

```
1. longest-span beam or slab        2. any cantilever (balcony, canopy, stair)
3. most heavily loaded column (take-down)  4. any transfer element (column on beam)
5. anything the user asked about
```

Everything else stays in the §7.3 "NOT verified by FEM" list. Five unverified members
honestly listed beat six implied checked.

### 3.9 MEP risers, site/boundary, septic — coordination objects

> Services engineering is owned by **`building-services-tga`** (riser sizing, shaft
> rules, fire-stopping with `fire-protection-building`, penetration zoning). This file
> models risers/shafts as classified solids and voids that coordinate cleanly.

**MEP risers (*Steigstränge*)** — vertical service solids per storey, inside a real
shaft void through every slab crossed [template — not round-tripped through this bridge]:

```python
riser = doc.addObject("Part::Cylinder", "Riser_Waste_DN100")
riser.Radius, riser.Height = 55, 6400       # DN100 stack incl. insulation allowance
riser.Placement = App.Placement(App.Vector(sx, sy, 0), App.Rotation())
shaft_void = doc.addObject("Part::Box", "Shaft_S1_void")
shaft_void.Length, shaft_void.Width, shaft_void.Height = 300, 250, slab_t   # through-slab
shaft_void.Placement = App.Placement(App.Vector(sx-150, sy-125, slab_z), App.Rotation())
shaft_void.ViewObject.Visibility = False
slab.Subtractions = slab.Subtractions + [shaft_void]
doc.recompute()      # verify by volume diff (§3.1) — every penetration is §7.4 material
```

Discipline: one shaft per service family (drainage, water, HVAC, electrical); every slab
crossing is a `Void_*` with real plan position; size shafts at planning stage (retrofit
core-drilling = the expensive failure mode); a duct that cannot cross a beam is a
coordination fact — check BoundBox intersection *before* the model pours the slab.

**Site and boundary** — the `Site` container exists (§2.1); add terrain and boundary so
setbacks are *measurable* [template]:

```python
plot = doc.addObject("Part::Box", "SitePlot")
plot.Length, plot.Width, plot.Height = 12640, 9000, 100      # example plot, mm
plot.Placement = App.Placement(App.Vector(0, 0, -100), App.Rotation())
site.addObject(plot)
# boundary lines: Draft.make_line at the setback offset per edge; assert min facade
# distance by BoundBox arithmetic, PASS/FAIL print like everything else
```

Setback/GRZ/GFZ figures are `building-regulations-permits` questions; the modeling
job is making them measurable from one shared project-zero origin (agreed in
`bim-management` before first placement).

**Septic / on-site wastewater (where no sewer)** — model as a buried classified volume
(`IfcType="Footing"` placeholder or labelled solid) at invert levels from
`building-services-tga`/`geotechnics-foundations`. The box is a **volume and position
claim only** — tank sizing (population equivalents, retention) must never be inferred
from a drawn box; without skill numbers, call the tank *schematic, unplaced*.

### 3.10 Renovation & retrofit modeling — Bestand baseline, status tagging, delta tracking

> Component-level renovation technique (what to repair, how) is owned by
> **`building-renovation-refurbishment`** and **`timber-building-renovation`**; structural
> condition assessment/Nachrechnung is owned by **`existing-structures-retrofit`**. This
> file owns only the *modeling pattern* that emulates a renovation process on a parametric
> model — never invent a repair method or a residual-strength number here.

**Establishing the Bestand baseline.** Two paths, both feeding the same spatial hierarchy
(§2.1):

- **Survey-derived IFC exists** — import it with NativeIFC (§4.2) as the Bestand document;
  do not flatten it, keep the link live so corrections from a re-survey round-trip.
- **No IFC, only a paper/photo survey** (the normal renovation case) — reconstruct the
  Bestand manually as ordinary parametric objects (§3.1–3.9) from the Bestandsaufnahme
  data (`building-renovation-refurbishment`'s survey workflow, or
  `timber-building-renovation` §Schadensanalyse for timber-specific condition mapping).
  A hand-reconstructed Bestand model is geometry the surveyor measured, not a design —
  tag it as such (§7.3 status-block vocabulary: *"Bestand, as-surveyed"*, never *"as-built
  verified"* unless it was).

**Status tagging — every object gets a renovation-phase property** [template, not
round-tripped through this bridge]:

```python
for obj in [wall, slab, window]:
    if not hasattr(obj, "Sanierungsstatus"):
        obj.addProperty("App::PropertyEnumeration", "Sanierungsstatus", "Renovation",
                         "Phase status of this element in the renovation process")
    obj.Sanierungsstatus = ["Bestand-erhalten", "Bestand-rueckbau", "Neu"]
    obj.Sanierungsstatus = "Bestand-erhalten"   # set per element from the survey/concept
```

Organize by three top-level `App::DocumentObjectGroup` containers — `Bestand`, `Rueckbau`,
`Neu` — mirroring the property, not replacing it (the property survives a regroup; a
Group alone does not carry the phase if an object is moved). Toggle
`group.ViewObject.Visibility` per group to render an "as-found" view (only `Bestand` +
`Rueckbau` visible), a "demolition" view (`Rueckbau` isolated), and an "as-built" view
(`Bestand-erhalten` + `Neu`, `Rueckbau` hidden) from one shared document instead of three
divergent files — the single-source-of-truth rule in §2.2 applies across renovation phases
too.

**Delta tracking — quantify what changes, don't eyeball it** [template]. Same
verify-by-measurement discipline as §2.4/§3.1, applied per phase:

```python
# before editing a Bestand element, snapshot its volume
vol_before = wall.Shape.Volume
# ... apply the renovation edit (resize, add/subtract opening, etc.) ...
doc.recompute()
vol_after = wall.Shape.Volume
delta_mm3 = vol_after - vol_before
print(f"{wall.Label}: {delta_mm3/1e9:.3f} m³ delta "
      f"({'added' if delta_mm3 > 0 else 'removed'})")
```

For a full Rückbau (element removed, not resized), record the pre-removal `Shape.Volume`
on a small log object or in the FreeCAD document's `Comment`/a dedicated
`App::PropertyQuantity` before deleting — once deleted, the geometry is gone and the
Abbruch-volume figure (needed for `building-renovation-refurbishment`'s
Abbruch/Rückbau section and any DIN 276 cost re-take-off) cannot be recovered from the
model.

**Degraded-material property override for FEM.** A Schadensbewertung
(`timber-building-renovation` §5, residual cross-section/strength for decayed timber) or a
historic material class (`existing-structures-retrofit` §4.3–4.4, reduced fck/fyk for old
concrete/reinforcement) is a number computed *outside* this file — never re-derive it
here. Apply it to the existing object's material definition before `run_fem_analysis`
instead of creating a parallel "damaged copy" object, so the FEM input and the visible
model geometry never drift apart [template]:

```python
mat = FreeCAD.ActiveDocument.getObject(beam.Material.Name) if beam.Material else None
# or: assign a fresh App::MaterialObject carrying the reduced values from the
# Schadensbewertung / historic-class lookup, then point beam.Material at it
mat.Material = {**mat.Material,
                 "YoungsModulus": "7000 MPa",   # e.g. reduced E for decay-affected timber
                 "CompressiveStrength": "12 MPa"}
doc.recompute()   # re-run run_fem_analysis after the override — a stale result is §7.4
```

Log the source of the override in the object's `Description` property (e.g. *"E reduced
per Schadensbewertung §5.3, Braunfäule Klasse 2"*) — a reduced number with no traceable
source is exactly the kind of unverified claim §7.2's honesty rule forbids presenting as
a check.

**LOD/LOI implications.** A Bestand model is typically **lower geometric fidelity, higher
condition-data fidelity** than a new-build model — a wall's exact thickness may carry
±20 mm survey uncertainty while its `Sanierungsstatus` and damage notes are precise. State
this asymmetry explicitly when handing off; see `bim-management` for how to declare it in
the LOIN.

## 4. IFC exchange and the bim-management handoff

### 4.1 The export path (and its one module trap)

```python
from importers import exportIFC          # NOT `import importIFC` — G-03
exportIFC.export([site], "/tmp/model.ifc")
```

Export the **root container** (`site`) so the hierarchy carries everything; loose element
lists break the spatial tree §2.1 built. If the exporter surfaces a schema option (IFC2x3
vs IFC4 — **check your build; [unverified] here**), pin it explicitly so consecutive
exports are comparable; the FILE_SCHEMA header line shows what you actually got.

### 4.2 Importing and round-tripping IFC files — NativeIFC

FreeCAD 1.0+ can hold an IFC file as its actual data structure instead of
translating it into Arch objects and back (the old lossy round-trip). No MCP
tool wraps this directly — drive it through `execute_code`
(`FreeCAD.openDocument(path)` for a native open, or the legacy
`from importers import importIFC; importIFC.open(path)` path for the
old parametric-Arch-object conversion, §4.1's counterpart) — and confirm
which mode you're in before editing, since the two behave very differently:

- **Locked mode**: the whole FreeCAD document *is* the IFC file — every edit
  writes straight back, no `exportIFC` call, no `.FCStd`. Toggled by the
  status-bar lock icon (`BIM_ToggleNativeIFC`) — **GUI-only, no scripted
  toggle documented**; if an agent needs this mode, ask the human to flip it,
  don't assume.
- **Unlocked mode** (default): IFC "project" objects can sit alongside plain
  BIM/Arch objects in one document. This is the safer default for an agent —
  it does not silently rewrite someone else's IFC file on every save.
- Opening an IFC file only renders top-level objects (Site/Building) at
  first — **an object with no visible children may just be unexpanded, not
  empty**; double-click (or the equivalent `execute_code` walk) to expand
  before asserting a model is missing content. Same trap-shape as §6.4's
  "invisible geometry" list — add this as a fourth entry when triaging.
- Once bound into a native IFC project, an object is IFC-controlled and
  **loses this skill's parametric recipes** (§2.2) for anything IFC doesn't
  model the same way — verify-by-measurement (§2.4) matters *more*, not
  less, on an imported IFC object, since you can no longer trust the FreeCAD
  parametric history to have produced the shape.
- **Comparing two versions of an IFC file** (e.g. before/after a coordination
  round-trip, or two exports of the same model): **Utils → IFC Diff**
  (`BIM_Diff`) diffs by IFC GlobalId — red/removed, green/added, yellow/
  geometry-changed, orange/properties-changed. Also GUI-only; for a
  scripted check, fall back to §4.4's grep/count discipline on both files.
- Legacy (non-native) import still exists and is what most non-1.0-workflow
  guidance elsewhere assumes: `importIFC.open()` with an import-mode
  preference (full parametric Arch objects / non-parametric Arch objects /
  Part shapes only / one shape per floor) trading fidelity for load speed on
  large files — pick full-parametric only when you actually intend to edit
  what comes in.

### 4.3 Pre-export validation — BIM Preflight (run before every export)

FreeCAD ships a built-in checker for exactly this handoff: **Manage → Preflight
checks…** (`BIM_Preflight`, GUI-only — no MCP tool wraps it, so either drive it
by hand or call the underlying Python checks via `execute_code` if scripting
access is needed). Run **Test All** before every export that leaves this
session; it catches classes of error grep can't:

- **Project hierarchy** — at least one Site→Building→Storey chain exists and
  every object sits inside a storey (this is the automated form of §2.1's
  hierarchy discipline — run it, don't just eyeball the tree).
- **Undefined objects** — plain `Part`/`Draft` shapes with no BIM type will
  export with no properties; this is the automated check for the "one source
  shape... carries no BIM classification" trap flagged at §2.1.
- **Solids** — invalid/open geometry per object.
- **Explicit quantities** — objects with Length/Width/Height not flagged for
  IFC export (**Manage → Manage IFC quantities…**, `BIM_IfcQuantities`); a
  quantity can silently read zero downstream even though the geometry is
  correct — this is a distinct failure mode from the volume-verification in
  §2.4, because it checks the *exported* quantity claim, not the modelled shape.
- **Common Psets present and complete** — e.g. `Pset_WallCommon`,
  `Pset_DoorCommon` attached and matching the schema (edit via **Manage →
  Manage IFC properties…**, `BIM_IfcProperties`; custom Psets live in
  `$USERAPPDATA/BIM/CustomPsets.csv`).
- **Materials assigned** to every BIM object.
- **Standard codes** — classification (Uniclass/Omniclass/etc, via **Manage →
  Manage classification…**, `BIM_Classification`) present; this is a formal
  standard-code slot, distinct from this skill's own `IfcType`/naming
  convention (§2.3) — populate both, they answer different questions
  (`IfcType` = what it is to the IFC schema; classification code = what it is
  to the client's cost/FM taxonomy).
- **Compatibility quirks** worth knowing before a client opens the file in
  Revit: extrusion-only geometry, "standard case" walls/structural elements,
  no line segments under 1/32", `IfcRectangleProfileDef` export disabled.

Preflight is advisory (failures don't block export) and does not replace
§4.4's export-and-grep discipline — it catches structural/organizational
problems *before* export; §4.4 proves the *specific* claims this skill made
about an object actually round-tripped. Run both.

### 4.4 Verify classification by parsing, not by trusting properties

```
grep -c IFCWINDOW  /tmp/model.ifc
grep -c IFCDOOR    /tmp/model.ifc
grep -c IFCFOOTING /tmp/model.ifc
grep -c IFCREINFORCINGBAR /tmp/model.ifc
```

`obj.IfcType == "Window"` alone is a claim; the round-trip is the measurement — same
discipline as the volume diff: an export is an instrument.

### 4.5 Handoff to `bim-management`

| Item | This skill guarantees | bim-management owns |
|---|---|---|
| Spatial tree | Site→Building→Storey, real elevations, elements contained | decomposition vs. project naming/Pset scheme (ISO 19650 flow; AIA/BAP) |
| Classification | correct `IfcType`, proven by grep (§4.4) | MVD/view fit (Reference vs Design Transfer), model-checker rules |
| Geometry | parametric, volume-verified, LOIN-appropriate (§2.5) | exchange format, Data Drops, coordinate/zero-point standard |
| Semantics | FEM verification stamped on objects (§7.5) | property sets, classification codes, FM information |
| Open items | §7.3 status block lists all unverified/unmodelled work | issue tracking (BCF-style), coordination, conflict resolution |

The DACH process frame (details in `bim-management`): **AIA**
(*Auftraggeber-Informationsanforderungen* ≈ EIR) and **BAP** (*BIM-Abwicklungsplan* ≈
BEP) define *what* the exchange carries; **LOIN** (DIN EN 17412) defines *how much* —
§2.5 is the modeling-side application. Do not duplicate process here.

## 5. GOTCHAS — the complete master list

FreeCAD-API rows validated on 1.0.1 through this bridge (mechanics in §3); MCP rows are behavioural facts of the neka-nat/freecad-mcp queue/timeout design. Each fails **quietly or misleadingly**; §3/§6 reference these IDs.

| ID | Gotcha | Wrong → Right |
|---|---|---|
| G-01 | `name=` on Arch factories sets **Label**, not `Name` | `doc.PadFooting` AttributeError → `doc.getObjectsByLabel("PadFooting")[0]` |
| G-02 | Sketch attachment renamed in 1.0 | `sk.Support = (obj,["Face5"])` → `sk.AttachmentSupport = [(obj,"Face5")]; sk.MapMode = "FlatFace"` |
| G-03 | IFC exporter module path | `import importIFC` → `from importers import exportIFC` |
| G-04 | Quantities read back in **internal units** (mm, kg, s) | raw `fc.Force` prints `21600000.0 mm*kg/s^2` → assign `"21600 N"`, read `.getValueAs("N")` |
| G-05 | `makeRebar` doesn't populate `host.Armatures` when scripted | `footing.Armatures == []` → check `rebar.Host` **[verified]** |
| G-06 | Face indices assumed, **any boolean re-indexes faces** | hard-coded `"Face1"` after a cut → enumerate+assert by `CenterOfMass` (§3.8.2) |
| G-07 | `window.Hosts = [wall]` does not cut the wall | geometry relies on it → `wall.Subtractions` void solid (§3.1) |
| G-08 | Missing `doc.recompute()` | stale `Shape.Volume` read → recompute, then read |
| G-09 | Repeated FEM runs accumulate `CCX_Results`, `CCX_Results001`… | reading old results → delete between runs or read newest (§3.8.8) |
| G-10 | `makeStairs` defaults `Nosing = 0.0` | assuming with-nosing tread minimum → zero nosing raises the minimum to the no-nosing value (§3.6) **[verified]** |
| G-11 | FEM `ElementOrder` | `"1st"` tets far too stiff/inaccurate in bending (~2× deflection) → `"2nd"` required **[verified]** |
| G-12 | `makeFloor.Elevation` looks directly settable | `floor.Elevation = "-1200 mm"` silently reverts to 0 on recompute — **derived from `Placement.Base.z`** → `p = floor.Placement; p.Base.z = -1200; floor.Placement = p` **[verified]** |
| G-13 | `makeStructure` centering **depends on IfcType** | assuming corner-based `Placement.Base`: **[verified 1.0.1]** Column/Slab → X,Y centered, Z corner (+H up); Beam/Footing → X corner (+L), Y,Z centered. Lintel lands 75 mm low for a 150 mm depth; slab footprint shifts half its size → world-coordinate voids cut 0.000 m³ silently. **Print `Shape.BoundBox` right after every Placement set and compare** |
| G-14 | `makeRebar.Direction` defaults `(0,0,0)` | trusting `Spacing`: 51 bars/offset 75 on a 10287 mm strip → **Spacing=3 mm** (spread over `2·offset`); set `Direction` to the replication axis → 202.7 mm as intended; verify `Spacing ≈ L/(n−1)` **[verified]** |
| G-15 | Rebar end-offset defaults + bar protrusion break naive containment | flat few-mm bbox fudge false-FAILs end stirrups: `OffsetStart/OffsetEnd` default **30 mm** (zero unless modeling laps); flush stirrup pokes **½·bar dia** past the endpoint (4 mm for Ø8) — correct geometry; tolerance must be **`bar_dia/2 + margin`** **[verified]** |
| G-16 | Window/Door `Normal` corruption → **Null shape** | patching `Normal` to default `(0,0,-1)` gives non-null but **flat, skylight-oriented** geometry; null ≠ sane — delete & rebuild from saved params, verify BoundBox vs `Void_*` (§3.5/§6.2) **[verified]** |
| G-17 | Door/Window `Base`-sketch `Placement` has **zero effect** on built shape | rotating/repositioning `door.Base.Placement` → identical BoundBox silently; only the **object's own `Placement`** transforms; upright-fix procedure §3.5; **never batch-guess rotations from sorted spans** — 10/12 wrong in one confirmed attempt **[verified]** |
| G-18 | Thin member + uncapped mesh kills the session | letting the solver generate a giant mesh: hundreds of thousands of nodes → GUI `stuck` 1000+ s past timeout → **crash**, unsavable; mesh yourself, gate on `NodeCount` (§3.8.9) **[verified]** |
| G-19 | Placement rotation pivots at `Placement.Base`, not element centre | assuming rotate-in-place for stairs/roof — flight/roof swings sideways off target; set rotation first, correct Base, verify BoundBox (§3.6/§3.7) |
| G-20 | `Part::Box` face order stable **(verified)**: F1 x=0, F2 x=L, F3 y=0, F4 y=W, **F5 bottom z=0, F6 top z=H** | assuming it survives a boolean → re-dump after any cut (G-06) |
| G-21 | Pressure as bare float can be right **by accident** | `8.83` for 8.83 kPa equals 0.00883 MPa internally — coincidence, never generalises → always the unit string |
| G-22 | `execute_code` budget: **90 s queue + 90 s exec; client socket 210 s** | monolithic 10-minute scripts → split into per-element calls (§1.4) |
| G-23 | Long ops block the whole GUI thread (saves included) | heavy boolean/solve inside `execute_code` → `execute_code_async` + `commit(fn, timeout=120)` (§1.4) |
| G-24 | Fixed-support peak stress is a **mesh-dependent singularity** | reporting it as design stress → read ~1 member-depth away or label as artifact (§3.8.6) |
| G-25 | **`GUI_DISPATCH_STUCK`** / `get_rpc_status → stuck` | queueing more calls → stop; stuck task uncancelable; restart per §6.1 |
| G-26 | `run_fem_analysis` only solves assembled analyses; **returns no safety factor** | expecting it to wire materials/BCs/meshes → build the 5 prerequisites (§3.8.3); compute SF vs the owning skill's criterion |
| G-27 | `execute_code` namespace **persistent** (`FreeCAD`/`App`/`Gui` pre-aliased) and dirty after errors | relying on leftovers → keep calls self-contained; inspect leftovers after failures (§6.2) |
| G-28 | GUI dispatch is **FIFO**, one operation at a time | parallel MCP fan-out around a solve → serialize everything |
| G-29 | Dev/nightly: `execute_code` exception can leave FeaturePython objects with broken `Proxy` | mutating them → inspect `obj.Proxy`/delete first (§6.2) |
| G-30 | Screenshots **on by default** — the token hog | default-on everywhere → `include_screenshot=False` for analytical calls, correct `view_name`, `--only-text-feedback` for long builds (§1.3) |
| G-31 | No headless: Xvfb hangs the GUI thread forever | `xvfb-run FreeCAD` → live GUI on a real display (§1.1) |
| G-32 | RPC localhost-only by default | "the port is open, right?" → Remote Connections + Allowed IPs (CIDR) + `--host` — an explicit user decision (§1.5) |
| G-33 | `run_fem_analysis` client socket must be **≥ 2×timeout + 30 s** | client cutting mid-queue → size the socket ceiling from the requested timeout (§1.4) |
| G-34 | `insert_part_from_library` supplies prepared templates (windows/doors) | rebuilding multi-part frames per project → one template, many instances (§2.6, §3.5) |
| G-35 | `create_object`/`edit_object` are single-property CRUD | assembling sketch-attached cages through them → parametric chains belong in `execute_code` |

## 6. Error recovery playbook

### 6.1 `GUI_DISPATCH_STUCK` / `state: "stuck"`

1. **Stop queueing** — every new call stacks behind the blocker and times out at the
   client (G-28); more damage, zero information.
2. `get_rpc_status` — confirm state and how long it has been stuck.
3. If a `run_fem_analysis`/mesh run: G-18's worst case applies — the task **cannot be
   cancelled** and even `doc.save()` fails until the process restarts.
4. Human restarts FreeCAD; crash recovery *may* have preserved unsaved work — **verify
   (§6.6) before assuming anything in either direction**.
5. Re-run §1.6 preflight; resume from the last verified checkpoint — which is exactly why
   §2.4 verifies incrementally and §1.7 saves after each. Prevention dominates anyway:
   short calls (G-22), async for heavy work (G-23), node-count gate before every solve
   (§3.8.9).

### 6.2 Null shapes / corrupted Window/Door — delete & rebuild from saved params

Symptoms: `obj.Shape` null/`isNull`; BoundBox spans inconsistent with `Width/Height`;
object present, geometry gone (after touching `Normal`, or an exception left a broken
`Proxy` — G-16, G-29). **Do not patch; rebuild** — only possible if creation stored params:

```python
import json
PARAM_STORE = "/tmp/opening_params.json"           # written at creation time

def save_opening_params(obj, void, w, h, sill, wall_angle, world):
    try: store = json.load(open(PARAM_STORE))
    except Exception: store = {}
    store[obj.Label] = dict(type=obj.IfcType, W=w, H=h, sill=sill,
                            angle=wall_angle, world=list(world), void=void.Label)
    json.dump(store, open(PARAM_STORE, "w"), indent=1)
    print(f"[PASS] params stored for {obj.Label}")
```

Rebuild order: remove the corrupted BIM object **and** its `Void_*` from `Subtractions` →
`doc.removeObject(...)` → recompute → rebuild void → re-cut → **volume diff** (§3.1) →
rebuild BIM object at saved placement → **verify BoundBox inside the void** (§3.5). Delete
any half-built FeaturePython with a broken `Proxy` too — stale proxies poison later label
fetches.

### 6.3 Recompute loops / stuck-touched objects

`doc.recompute()` keeps failing; objects stay `['Invalid','Touched']`.
1. Identify: `[o for o in doc.Objects if "Invalid" in o.State or "Touched" in o.State]`.
2. Usual causes: `Base`/`Subtractions` link to a deleted object; a sketch whose
   `AttachmentSupport` face vanished in a boolean (G-06); a null-profile void.
3. Clear broken links (`obj.Subtractions = [v for v in obj.Subtractions if v in doc.Objects]`),
   re-attach sketches to surviving faces, recompute; if one object poisons the document,
   delete & rebuild from params (§6.2) beats archaeology.

### 6.4 Misplaced or "invisible" geometry — the four classic lies

- **Cut did nothing (0.000 m³):** almost always the G-13 footprint shift — void is real,
  slab sits half its size away. Print both BoundBoxes, fix Placement, re-verify.
- **Stress/force 1000× wrong:** bare-float unit bug (G-04/G-21) — audit every numeric
  assignment to Force/Pressure/E; make them strings.
- **"I rotated it and nothing moved":** you edited a `Base` sketch Placement (G-17) or
  patched a `Normal` (G-16). Own-Placement only.
- **"This imported IFC object has no children/looks empty":** a freshly opened or
  imported native-IFC file only renders top-level objects by default (§4.2) —
  expand (double-click, or the scripted equivalent) before concluding content
  is missing.

### 6.5 Stale FEM results

Repeated runs leave `CCX_Results*`; reading the wrong one returns old numbers under a
fresh call. Delete old result objects between runs (§3.8.8) or read the highest-numbered,
and **stamp** results onto members (§7.5) so a stale number betrays itself by geometry
fingerprint even if cleanup is forgotten.

### 6.6 Post-restart verification protocol

```python
print(App.Version())
doc = App.ActiveDocument
print("objects:", len(doc.Objects))      # vs your last checkpoint note
for lbl in ("Wall_W-N-01", "PadFooting_F1", "Win_W1-N01"):
    o = doc.getObjectsByLabel(lbl)
    ok = o and o[0].Shape and not o[0].Shape.isNull()
    print(lbl, "->", "MISSING" if not o else ("NULL SHAPE" if not ok else o[0].Shape.BoundBox))
```

Every MISSING/NULL SHAPE is a §6.2 case; then re-run `fem_ledger(doc)` (§7.5) —
crash + recovery is when stamped-but-stale verification lies.

## 7. Agent workflow — brief → plan → model → verify → document

### 7.1 The loop

```
0. BRIEF        building type, storeys, use, location/standard, deliverable level
                (massing? model? engineer-ready?). A missing design value is a signal a
                sibling skill must run first — never a licence to guess.
1. PLAN         building-planning-spatial (program) + building-typology (form) +
                structural-systems (system, preliminary sizes) BEFORE any geometry;
                real projects additionally: geotechnics-foundations, concrete-detailing,
                structural-analysis, stairs-vertical-circulation, seismic-design.
2. SKELETON     §1.6 preflight → Site/Building/Storey hierarchy, real elevations (§2.1)
                → grid/axis reference → doc.save().
3. MODEL        one element type per increment (walls → openings → slabs → structure →
                rebar → stairs → roof → risers → site), one short execute_code call each
                (G-22), doc.save() after every verified increment.
4. VERIFY       BoundBox vs intent (G-13/G-19) → volume diff per cut (§3.1) → PASS/FAIL
                prints → stair/rebar/column audits → fem_ledger (§7.5). An increment
                without a printed PASS line did not happen.
5. SOLVE        what you claim: §3.8, prioritised §3.8.10, hand-check ≤ ~10 % (§3.8.5),
                convergence, stamped (§7.5).
6. EXPORT       §4: IFC export + grep; fix classification before calling it done.
7. DOCUMENT     §7.3 status block **from fem_ledger output**, §7.2 vocabulary, open items
                routed to owning skills.
```

### 7.2 The honesty rule and the vocabulary

> **Any element presented as structurally adequate must carry solver output. Any element
> without it must be flagged as unverified, in the reply, unprompted.**

1. **Absence of a check is information the user needs** — it degrades with every
   unflagged reply; re-state on every substantive model reply, not only the first.
2. **A passing FEM run is not a passing design** — name criterion, load case, margin;
   never the word "safe". 3. **Silence is a claim** — showing columns and footings
   without "unverified" asserts by omission that they are fine.

| Never say | Say instead |
|---|---|
| "the beam is fine / safe / adequate" | "FEM: σ_vm 3.19 MPa vs f_ct 3.40 MPa — uncracked, 6 % margin, under the stated load; not an RC design check" |
| "the footing is sized correctly" | "sized for an **assumed** 150 kPa bearing; needs geotech confirmation + punching check" |
| "structural model complete" | "geometry complete; FEM run on 1 of 6 members; 5 unverified" |
| "code-compliant stair" | "passes the riser/tread/width gates supplied by stairs-vertical-circulation; headroom **not measured**; handrails not modelled" |
| "the column is adequate" | "axial stress X MPa under the §3.8.1 take-down; buckling hand-checked only (kL/r = 33); no lateral case run" |
| "rebar is designed" | "cage modelled and checked against minimum-steel values passed from concrete-detailing; development lengths, laps, hooks not detailed" |
| "the model is verified" | "geometry verified by volume diff and IFC export; structure verified only where listed below" |
| "this is ready to build" | never — see the Reality Check |

### 7.3 The mandatory status block

Include whenever the model contains structural elements — **do not omit it because the
user did not ask**:

```
STRUCTURAL VERIFICATION STATUS
  Verified by FEM (CalculiX):   <member: sigma_vm, delta, load case, criterion compared,
                                 mesh + convergence delta, hand-check delta>
  NOT verified by FEM:          <every other structural member>
  Hand-checked only:            <member: formula, result>
  Assumed inputs:               <soil bearing, concrete class, E, loads, boundary
                                 idealization, which combination>
  Simplifications:              <proxy solids, omitted penetrations, single-span models>
  Not modelled at all:          <plinth beams, lintels, handrails, hooks/laps, ...>
  Not checked at all:           punching shear, one-way shear, wind, torsion, buckling,
                                connections, long-term deflection, cracking, settlement,
                                construction-stage loading
  Lateral / seismic:            NOT evaluated in this skill — seismic-design
                                <invoked: yes/no; if no, say so explicitly, don't bury
                                 it — for a seismic-region building this is a real gap>
  Cross-check vs preliminary sizing: <structural-systems consulted? agree within
                                 ~15-20%? if not run, say so>
  => NOT construction-ready. Requires a licensed structural engineer (Tragwerksplaner /
     equivalent) and building-authority approval (Baugenehmigung incl. bautechnischer
     Nachweis where applicable).
```

If **zero** members have been through the solver, lead with **"FEM NOT RUN — no member in
this model has been structurally verified."** — before describing the model at all.

### 7.4 What silently invalidates a previously-run FEM

Re-run, or downgrade to unverified, whenever **any** of these change: member dimensions;
`Subtractions` added/removed (new penetration or opening); material properties (class, E,
ν, density); load values, tributary width, or combination; boundary conditions or face
bindings (including face **re-indexing** after a boolean); span, support locations, or an
added/removed intermediate support; mesh density or element order; the proxy drifting
from the BIM object it stands in for. **A stale FEM result on an edited member is worse
than no result, because it looks like evidence.**

### 7.5 Machine-enforce the ledger — don't rely on memory

```python
def stamp_fem(obj, sigma_mpa, delta_mm, load_case, criterion, nodes, hand_delta_pct):
    if not hasattr(obj, "FEMStatus"):
        obj.addProperty("App::PropertyString", "FEMStatus", "Verification", "FEM record")
        obj.addProperty("App::PropertyString", "FEMStamp", "Verification", "geom fingerprint at run")
    obj.FEMStatus = (f"VERIFIED sigma={sigma_mpa:.3f}MPa delta={delta_mm:.3f}mm "
                     f"case={load_case} vs {criterion} nodes={nodes} hand_delta={hand_delta_pct:.1f}%")
    obj.FEMStamp = geom_fingerprint(obj)

def geom_fingerprint(obj):
    s = obj.Shape
    return f"{s.Volume:.3f}|{len(s.Faces)}|{len(obj.Subtractions) if hasattr(obj,'Subtractions') else 0}"

def fem_ledger(doc):
    """Print §7.3's first lines straight from the model. Run before every handoff."""
    structural = {"Footing","Column","Beam","Slab","Pile","Member","Stair"}
    verified, unverified, stale = [], [], []
    for o in doc.Objects:
        if getattr(o, "IfcType", None) in structural:
            st = getattr(o, "FEMStatus", "")
            if not st:
                unverified.append(o.Label)
            elif getattr(o, "FEMStamp", "") != geom_fingerprint(o):
                stale.append(o.Label)          # geometry changed since the run
            else:
                verified.append(f"{o.Label}: {st}")
    print("VERIFIED BY FEM:   " + ("; ".join(verified) or "NONE — FEM NOT RUN"))
    print("STALE (re-run):    " + (", ".join(stale) or "none"))
    print("NOT VERIFIED:      " + (", ".join(unverified) or "none"))
    return verified, stale, unverified
```

Run `fem_ledger(doc)` **immediately before any reply that describes the model** and copy
its output into §7.3 — reconstruction from memory is where unverified members quietly
become verified ones.

### 7.6 Worked example — a bad reply and a good one

**Bad** (defensible in parts, false as a whole):

> Here's your G+1 house model. The structure uses 300×300 columns on 1500×1500 pad
> footings with a 150 mm slab, and the FEM analysis came back at 3.19 MPa, well within
> limits. The stair is code-compliant at 176 mm risers. Ready for your contractor.

**Good:**

> **Not construction-ready** — a modeling and screening exercise; needs a licensed
> structural engineer plus building-authority approval before anyone builds from it.
>
> Model: G+1; Site → Building → 5 storeys (incl. Foundation at −1200); 22 walls, all
> openings parametric and volume-verified; IFC export confirms
> IFCFOOTING/IFCWINDOW/IFCREINFORCINGBAR.
>
> ```
> STRUCTURAL VERIFICATION STATUS
>   Verified by FEM:  Beam B1 (3.0 m) — sigma_vm 3.193 MPa vs f_ct 3.40 MPa (C30/37),
>                     delta 1.09 mm vs L/360 = 8.3 mm, case per §3.8.1 take-down,
>                     2713 nodes 2nd-order, hand-check delta 0.2%/2.3%.
>                     Modelled as CANTILEVER (conservative); real condition partially
>                     restrained. Mesh convergence NOT yet re-run.
>   NOT verified:     Columns C1-C6, footings F1-F6, slabs S1-S2, stair flight
>   Hand-checked:     C1 slenderness kL/r = 33 (stocky limit per structural-analysis?)
>   Assumed:          soil 150 kPa (NO GEOTECH), C30/37, E 30,000 MPa (skill value is
>                     lower — deflection scales with E; concrete-detailing)
>   Not modelled:     plinth beams, lintels, handrails, rebar hooks/laps
>   Not checked:      punching shear, wind, buckling, cracking, settlement
>   Lateral/seismic:  NOT evaluated — seismic-design not invoked; building sits in a
>                     seismic region, this is a real gap
>   Cross-check:      preliminary sizing NOT checked against structural-systems for B1
> ```
>
> Stair: riser 176.5 ✓, tread 262.5 with 25 nosing ✓, width 1100 ✓ — but **headroom not
> measured**, **no handrails modelled**.
>
> Biggest open item: footings sized on an assumed bearing pressure — get a geotech
> report before that number means anything.

## 8. Known gaps in this skill — state these when relevant

1. **Design values are placeholders by policy.** Every numeric limit this file needs
   (min steel, cover, bearing, stair gates, combinations) is passed in from its owning
   skill; defaults in check functions are validation-era examples, never code.
2. **Unverified patterns:** closed-sketch stirrups (§3.4); `ConstraintDisplacement`
   property names (§3.8.7); headroom raycast (§3.6); `Arch.makeVoid`,
   `insert_part_from_library` templates, §3.9 riser/site/septic blocks, §4.2's
   NativeIFC open/import and lock-mode behaviour, and the async
   `commit(fn, timeout=120)` pattern — directionally correct, not yet round-tripped
   through this bridge; verify before shipping into a live deliverable.
3. **No mesh-convergence second data point was ever taken** on the validated beam —
   §3.8.6 protocol is right, the re-run wasn't; any claim about that beam is single-mesh.
4. **No two-way slab, raft, pile or lateral workflow exists here at all** —
   engineer-only in the current state.
5. **IFC validation is grep plus an unwrapped GUI tool** — §4.4 proves entity
   presence and count; §4.3 (BIM Preflight) covers hierarchy/Psets/materials/
   classification/compatibility *if someone runs it*, but no MCP tool wraps
   it, so an agent working headless can't enforce it, only recommend it.
   Relational integrity of the exported file (does the Pset content match, do
   IFC relationships resolve) beyond what Preflight's own tests cover is still
   unchecked; schema-option exposure [unverified].
6. **Lateral/seismic is a named gap, not a solved handoff** — nothing confirms
   `seismic-design` ran or agrees with the gravity-only sizing here; close it by
   invoking the skill, not by citing its name.
7. **The §3.8.1 load path is not shown reconciled against `structural-systems` on a
   worked example** — treat any disagreement as something to resolve, not to average.

**Which skill owns what — defer rather than duplicate:**

| Topic | Owner skill |
|---|---|
| Soil investigation, bearing capacity, settlement, retaining, drainage | `geotechnics-foundations` |
| Cover, min/max steel, anchorage, laps, hooks, BBS, confinement detailing | `concrete-detailing` |
| System choice, preliminary member sizing tables, load-path narrative | `structural-systems` |
| Load combinations, internal forces, deflection/stability checks | `structural-analysis` |
| Earthquake action, regularity, ductile detailing | `seismic-design` |
| Masonry / timber / steel member & connection rules | `masonry-construction`, `timber-steel-design` |
| Room sizes, circulation, plan layout | `building-planning-spatial` |
| Stair/walk code gates | `stairs-vertical-circulation` |
| Bylaws, setbacks, permit workflow, structural submission | `building-regulations-permits` |
| Accessible stairs/ramps beyond minimums | `accessibility-universal-design` |
| Quantities, cost groups, BOQ discipline | `cost-management-din276` |
| Service sizing, riser/shaft engineering, penetration zoning | `building-services-tga` |
| Build-ups, U-values, acoustics, fire classes | `building-physics-thermal-moisture`, `building-acoustics`, `fire-protection-building` |
| Window/door design, lintel detailing | `openings-windows-doors` |
| BIM process, naming, MVD, CDE, model checking | `bim-management` |
| **This skill** | **Making all of the above real, parametric and solver-checked inside FreeCAD via the MCP bridge — and refusing to overstate the result** |

When a recipe raises a design question, stop modeling and open the owning skill — the
model is the argument's evidence, never the argument itself.
