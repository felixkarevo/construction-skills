---
name: architecture-freecad-bim
description: >
  Build real, structurally-verified BIM models in FreeCAD via the live FreeCAD MCP
  connection — correct spatial hierarchy (Site/Building/Storey), live parametric wall
  openings via Subtractions (not a frozen boolean cut), rich multi-part windows/doors,
  foundations/footings/plinth beams/rebar cages as real parametric BIM objects sized to
  ACI 318-19, IRC 2021 code-compliant staircases with landing/winder/headroom gates,
  roof-to-soil load derivation from ASCE 7-22, and actual structural verification through
  the CalculiX FEM pipeline via mcp__freecad__run_fem_analysis (material presets,
  boundary-condition idealization, hand-check calibration, mesh convergence, solver
  troubleshooting). Enforces an honesty protocol: no member may be presented as adequate
  without solver output, and every unverified member must be flagged unprompted. Derived
  from studying FreeCAD's bundled BIMExample.FCStd object-by-object and from a validated
  end-to-end FEM run on FreeCAD 1.0.1. Use whenever building a house/building model in
  FreeCAD, and always before presenting any member as structurally adequate.
---

# FreeCAD BIM Modeling & Structural Verification

This skill exists because a first attempt at a farmhouse model (2026-08-19) worked but cut corners a real BIM model shouldn't: no Site/Building/Storey hierarchy, non-parametric "frozen" wall cuts, oversimplified box-only windows, and an unvalidated staircase. Studying FreeCAD's bundled `usr/share/examples/BIMExample.FCStd` (a real 361-object professional building model: 41 walls, 18 doors, 18 windows, 9 slabs, 7 stairs, 5 storeys) resolved every one of those gaps with verified, working technique.

**Part 0 (§0)** is environment preflight — the connection, the units, the solver binaries, and the token discipline that makes everything else cheap to run.
**Part 1 (§1–§5)** is BIM geometry knowledge, preserved from the BIMExample.FCStd study.
**Part 2 (§6–§14)** closes the gap that matters most: *a model that looks like a building is not a building.* Foundations, footings and reinforcement must be real parametric objects with real dimensions, sized against a real code; members presented as adequate must be checked by an actual solver run; stairs must pass hard numeric code gates, not just the comfort formula; and any structural claim made without solver output must be flagged as such, out loud.

Everything marked **[verified]** was run against a live FreeCAD 1.0.1 instance through this MCP connection (CalculiX `ccx` and `gmsh` both present in the AppImage at `/home/oye/Applications/squashfs-root/usr/bin/`). Everything marked **[unverified]** is code-book or API knowledge that has **not** been round-tripped through the solver or the running instance — treat it as a lead to confirm, not as evidence.

## Reality Check — Licensing & Liability

**This skill produces design aids, dimensional guidance and calculation/modeling workflow for planning and FreeCAD modeling ONLY. It does not produce engineering design.**

- Any design intended for **actual construction of a real occupied building** MUST be reviewed, sealed and stamped by a **licensed structural engineer registered with the relevant authority** — in Pakistan, a **PEC-registered** Professional Engineer; elsewhere, the equivalent licensing body (PE / CEng / RPEQ / SE).
- Any such design MUST also go through **local authority plan approval** before construction — in Pakistan that means **LDA / CDA / DHA / SBCA / RDA / TMA / cantonment board byelaws** and their zoning, setback, coverage, height, FAR and structural-submission requirements, plus the **Building Code of Pakistan (BCP-2007 seismic provisions / BCP-2021, PEC)** as the locally applicable code. See `architecture-building-codes-permits` for the submission workflow.
- A CalculiX/FEM result produced by this workflow is a **screening check, not a design**. It is linear-elastic, isotropic, homogeneous, small-displacement, single-load-case and mesh-dependent. For concrete it does **not** model cracking, tension stiffening, creep, shrinkage, long-term deflection, reinforcement bond/anchorage, punching shear, or any seismic/wind lateral demand. It does not perform buckling, fatigue, or connection checks. **Passing it does not mean a member is safe.**
- Soil bearing capacity used in any footing sizing here is an **assumed value**. Real footings require a **geotechnical investigation report** (see `architecture-geotechnical-foundations`). Frost depth, water table, expansive/collapsible soils, made-up fill and seismic site class are project-specific and are not knowable from a model.
- Reinforcement modelled here is **geometry**, not a detailing design. Development lengths, lap splices, hook geometry, curtailment, and seismic confinement detailing are governed by ACI 318-19 Ch. 25 / Ch. 18 and BCP-SP 2007 — see `architecture-concrete-reinforcement-detailing`.

**Claude must never present FreeCAD output or these calculations as construction-ready.** If the user's language suggests they are treating the output as final — *"so I can start building"*, *"send this to the contractor"*, *"is this safe"*, *"give me the final footing size"*, *"can I pour this"* — say so **unprompted**, in that reply, **before anything else**. Do not bury it in a closing caveat. See §11 for the exact wording protocol.

---

# Part 0 — Environment & Preflight

## 0. Before touching the model

### 0.1 Connection preflight

| Step | Call | Pass condition |
|---|---|---|
| 1. Is the RPC alive? | `mcp__freecad__get_rpc_status` | not `stuck`; if `stuck`, the GUI thread is blocked — FreeCAD likely needs a restart, do not queue more work |
| 2. What documents exist? | `mcp__freecad__list_documents` | target doc present, or create with `create_document` |
| 3. Solver binaries present? | `execute_code`: check `ccx` and `gmsh` on PATH / in AppImage `usr/bin/` | both present **[verified on 1.0.1 AppImage]** |
| 4. FreeCAD version | `execute_code`: `App.Version()` | 1.0.x — the §4 gotchas are 1.0-specific |

**Hard rule from `project_freecad_mcp_setup`:** FreeCAD must run on a **real DISPLAY** (`:1`), launched via `./AppRun`. Under Xvfb the GUI thread hangs forever and every RPC call times out with no error.

### 0.2 Token discipline

`execute_code` and `run_fem_analysis` both default to `include_screenshot=True`. A screenshot is expensive and useless for analytical steps.

```
include_screenshot=False   → face dumps, property reads, assertions, mesh generation,
                             min-steel checks, load arithmetic, FEM numeric runs
include_screenshot=True    → after a geometry change the user should see; final model view;
                             one FEM run where the deformed/stress view is the deliverable
view_name                  → pick the view that shows the change ("Front" for a wall elevation,
                             "Top" for a plan, "Isometric" for massing)
```

### 0.3 Units cheat sheet — the #1 source of silent 1000× errors

FreeCAD's internal unit system is **mm, kg, s** (so force = `mm·kg/s²` = milli-newtons, pressure = `kg/(mm·s²)`).

| Quantity | Assign as | Read back as | Trap |
|---|---|---|---|
| Length | `"3000 mm"` or float mm | `.getValueAs("mm").Value` | bare floats are mm — fine |
| Force | `"21600 N"` **(string)** | `.getValueAs("N").Value` | printing raw shows `21600000.0 mm*kg/s^2` |
| Pressure / stress | `"0.005 MPa"` **(string)** | `.getValueAs("MPa").Value` | 1 MPa = 1000 internal units; a bare float is **1000× wrong** |
| Density | `"2400 kg/m^3"` | `.getValueAs("kg/m^3").Value` | — |
| Young's modulus | `"30000 MPa"` | — | material dict values are **strings with units** |
| Angle | `"90 deg"` | `.getValueAs("deg").Value` | Placement rotations take degrees |

**Rule: always assign quantities as unit-bearing strings; always read them with `.getValueAs()`.** Never compare a raw quantity to a float.

### 0.4 Scripting discipline inside `execute_code`

- Wrap risky blocks in `try/except` and `print` the traceback — an uncaught exception returns a terse failure with no diagnostics.
- `doc.recompute()` after **every** structural change; a stale document silently reports old volumes and old shapes.
- Fetch objects by **label**, never by attribute: `doc.getObjectsByLabel("PadFooting_F1")[0]` (§4).
- Print an explicit `PASS`/`FAIL` line for every assertion. A script that ends silently proves nothing.
- Never fan out parallel FreeCAD MCP calls around a solver run — it blocks the GUI thread (§9.1).

---

# Part 1 — BIM Geometry (verified against BIMExample.FCStd)

## 1. Spatial hierarchy — always build this first

Real BIM models are organized `Site > Building > Storey(s) > elements`, not a flat document. Each storey has a real `Elevation` (mm) and elements are assigned to their storey via `spatial.assign_container` or by adding to the storey's `Group`.

```python
site     = Arch.makeSite(name="Site")
building = Arch.makeBuilding(name="Building")
ground   = Arch.makeFloor(name="Ground Floor")   # IfcType "Building Storey"
ground.Elevation = 0
upper    = Arch.makeFloor(name="Upper Floor")
upper.Elevation = 3200   # mm, matches ground floor wall height
# nest: site contains building, building contains floors, floors contain elements
```

The reference example had 5 storeys (Ground, Upper, Street level, Basement, Roof) each with a distinct real `Elevation` — build this hierarchy **before placing a single wall**, not after.

**Storey scheme for a house with foundations** (extends the original guidance):

| Storey label | Elevation (mm) | Contains |
|---|---|---|
| `Foundation` | **negative** (e.g. −1200) | footings, pile caps, PCC/lean layer, plinth beams below DPC |
| `Plinth` | −450 to 0 | plinth beam, plinth walls, fill, DPC |
| `Ground Floor` | 0 | slab-on-grade, walls, columns, doors/windows |
| `Upper Floor` | +3200 | suspended slab, walls, stairs landing |
| `Roof` | +6400 | roof slab, parapet, water tank base |

Footings belong to the **Foundation** storey, not to Ground. A footing filed under Ground Floor will schedule and quantify wrong, and will read as an above-grade element in IFC.

## 2. Wall openings — the critical fix

**What does NOT work reliably**: setting `window.Hosts = [wall]` alone does not cut the wall (verified: zero volume difference on direct test). Don't rely on it for geometry.

**What actually works, confirmed by studying real walls in the reference file**: `wall.Subtractions` DOES perform a real, live, parametric boolean cut — but the subtracted object must be a plain solid (typically a `Part::Extrusion` of a 2D sketch rectangle, or a `Draft.Array`/`Draft.Clone` of one for repeated openings), not the Window/Door BIM object itself.

```python
# 1. Build the void profile and extrude it through the wall (plus margin both sides)
sketch = doc.addObject("Sketcher::SketchObject", "VoidProfile")
# ... constrain sketch to a WxH rectangle at the opening's local wall-face position ...
void = doc.addObject("Part::Extrusion", "Void")
void.Base    = sketch
void.DirMode = "Normal"
void.LengthFwd = wall.Width + 100   # through-cut with margin
void.Solid   = True
void.ViewObject.Visibility = False   # void shapes are always hidden

# 2. Assign as a live subtraction — this is what actually cuts, and stays parametric/recomputable
wall.Subtractions = wall.Subtractions + [void]
doc.recompute()
```

For a repeated facade pattern (a ribbed row of identical windows, common on long walls), build ONE void extrusion then `Draft.make_ortho_array` or `Draft.clone` it across positions and subtract the array/clone object — the reference building does exactly this for its ribbed office facade (one `Extrude001` void, arrayed via `Array003`/`Clone001`, both hidden, both in `wall.Subtractions`). This keeps the whole repeated pattern editable from one source shape instead of N independent cuts.

**Verify every cut by volume, every time**:

```python
before = wall.Shape.Volume
wall.Subtractions = wall.Subtractions + [void]
doc.recompute()
after = wall.Shape.Volume
cut_m3 = (before - after) / 1e9
expected_m3 = (w_mm * h_mm * wall.Width.Value) / 1e9
print(f"cut={cut_m3:.4f} m3 expected~{expected_m3:.4f} m3 "
      f"-> {'PASS' if before > after else 'FAIL: NOTHING WAS CUT'}")
```

A cut that silently does nothing (wrong position, non-overlapping box, wrong property) is invisible in a screenshot from the wrong angle but obvious in a volume diff.

`Arch.makeStructure` objects (footings, columns, beams — §6) also expose `Subtractions` **[verified]**, so the same technique cuts service penetrations through a beam or a pipe sleeve through a footing. **Every such penetration is a structural event** — it invalidates any prior FEM result for that member (§11.4) and, for beams, may be prohibited outright in the tension zone or near supports (see `architecture-mep-coordination`).

## 3. Windows and doors — separate visual/IFC object from the cut

Build the actual opening (previous section) and the `Arch.makeWindow` BIM object as two separate things placed at the same location — this matches the reference file exactly (its real windows have `Hosts: None` and still export as valid `IFCWINDOW` entities; the wall doesn't need to "know" about the window object to cut correctly, because the void extrusion already did that job).

```python
win = Arch.makeWindow(width=1150, height=2100, name="BathroomWindow")
win.IfcType = "Window"   # or "Door" for a door — same factory function, different IfcType string
win.Placement = App.Placement(world_pos, App.Rotation(App.Vector(0,0,1), wall_angle))
```

For higher fidelity than a plain box (the reference windows have `WindowParts` — `OuterFrame`, `Frame`, `Glass`, `Glass panel` as distinct named sub-shapes with real frame profiles), use the FreeCAD GUI's Window preset picker once to generate a realistic multi-part `WindowParts` template, then reuse that preset programmatically for consistency — a plain box is acceptable for a fast schematic pass but is a known simplification, not the ceiling of what Arch supports.

**Verify BIM classification by actually exporting**:

```python
from importers import exportIFC          # NOT `import importIFC` — §4
exportIFC.export([site], "/tmp/model.ifc")
# then grep the raw text:
#   grep -c IFCWINDOW /tmp/model.ifc
#   grep -c IFCDOOR   /tmp/model.ifc
#   grep -c IFCFOOTING /tmp/model.ifc
#   grep -c IFCREINFORCINGBAR /tmp/model.ifc
```

Don't trust `obj.IfcType == "Window"` alone — confirm it round-trips to real IFC data, the same discipline as the "render, don't just validate" lesson.

**Openings above structure:** a window or door head sitting under a wall run requires a **lintel** — model it (`Arch.makeStructure`, `IfcType="Beam"`) rather than leaving masonry floating over a void. An unlintelled opening in a load-bearing wall is a structural omission, not a modelling shortcut, and must be listed in the §11.3 status block if left out.

## 4. FreeCAD 1.0 API gotchas that silently corrupt a scripted model [verified]

These were all hit and confirmed on FreeCAD 1.0.1 through this MCP connection. Each one fails quietly or with a misleading error.

| Gotcha | Wrong | Right |
|---|---|---|
| `name=` on Arch factories sets **Label**, not `Name` | `doc.PadFooting` → `AttributeError` | `doc.getObjectsByLabel("PadFooting")[0]` |
| Sketch attachment renamed in 1.0 | `sk.Support = (obj,["Face5"])` → `AttributeError: no attribute 'Support'` | `sk.AttachmentSupport = [(obj,"Face5")]; sk.MapMode = "FlatFace"` |
| IFC exporter module path | `import importIFC` → `ModuleNotFoundError` | `from importers import exportIFC` |
| Quantities read back in **internal units** (mm, kg, s) | `fc.Force` prints `21600000.0 mm*kg/s^2` | assign strings (`fc.Force = "21600 N"`), read with `.getValueAs("N")` |
| Pressure internal unit is `kg/(mm·s²)`; 1 MPa = 1000 of them | assigning a bare float | `pr.Pressure = "0.005 MPa"` |
| `Arch.makeRebar` does not populate `host.Armatures` when scripted | checking `footing.Armatures` → `[]` | check `rebar.Host` instead |
| Face indices are assumed, not guaranteed | hard-coding `"Face1"` | enumerate and assert by `CenterOfMass` (§9.2) |
| `window.Hosts = [wall]` does not cut the wall | relying on it for geometry | `wall.Subtractions` with a void solid (§2) |
| Missing `doc.recompute()` after a property change | reading a stale `Shape.Volume` | recompute, then read |
| Repeated FEM runs accumulate results | reading `CCX_Results` after run 3 | read the newest, or delete old result objects between runs (§9.8) |
| `Arch.makeStairs` defaults `Nosing = 0.0` | assuming the 254 mm tread minimum applies | with zero nosing the **279 mm** minimum applies (§10.2) |
| `Arch.makeFloor.Elevation` looks settable directly | `floor.Elevation = "-1200 mm"` → silently reverts to 0 on recompute | `Elevation` is **derived from `Placement.Base.z`**, not the reverse — set `p = floor.Placement; p.Base.z = -1200; floor.Placement = p` |
| `Arch.makeStructure(length, width, height)` centers some axes and corner-bases others, **and the rule depends on `IfcType`** | assuming Placement.Base is a corner for every axis, on every member | verified on FreeCAD 1.0.1: **Column/Slab** (vertically-extruded) → `Length`(X) and `Width`(Y) are **centered** on `Placement.Base`, `Height`(Z) is **corner-based** (extends +Height upward). **Beam/Footing** (horizontally-extruded) → `Length`(X) is **corner-based** (extends +Length), `Width`(Y) and `Height`(Z) are **centered** on `Placement.Base`. A lintel built assuming Z is corner-based lands centered on its intended level — for the skill's default lintel (150mm deep, head at `zb+h`), it sits 75mm **too low**, dipping into the opening it's meant to cap. A slab built assuming X/Y are corner-based lands with its whole footprint shifted by half its own plan dimensions — any `Subtractions` void positioned in real world coordinates will silently fail to overlap it (0.000 m³ cut, no error). **Always print `obj.Shape.BoundBox` immediately after setting `Placement` on any `Arch.makeStructure` object and compare it to the intended world coordinates before proceeding** — this is the same "verify by volume diff" discipline as §2, applied one level earlier, before the cut is even attempted. |

`Part::Box` face order **is** stable and was confirmed empirically:

| Face | Location on a `Part::Box(Length=X, Width=Y, Height=Z)` |
|---|---|
| `Face1` | x = 0 (start end) |
| `Face2` | x = Length (far end) |
| `Face3` | y = 0 (near side) |
| `Face4` | y = Width (far side) |
| `Face5` | **z = 0 (bottom)** |
| `Face6` | **z = Height (top)** |

Confirm anyway on any non-box solid, and on any box that has been cut by `Subtractions` — a boolean re-indexes faces.

## 5. What real models skip (don't over-invest here)

Studying the reference file also showed what a real, shipped example *doesn't* bother with: wall `Material` and `IfcProperties` were empty/`None` even on finished walls, and the bundled TechDraw sheet was minimal (one `Template` + a `DraftView` projection + an `Annotation` — not a fully dimensioned construction-grade sheet). Don't over-invest in material/Pset assignment or elaborate drawing sheets unless the user specifically asks for construction documents — matching the reference project's own priorities is a legitimate calibration, not laziness.

**Exception added by Part 2:** this does *not* extend to structural members. A footing, column, beam, slab or rebar object with no real dimensions, no concrete grade and no steel is not an acceptable schematic simplification — **it is a false structural claim.** Either model it properly per §6–§7 or leave it out and say it is absent.

**Effort calibration:**

| Ask | Build | Skip |
|---|---|---|
| "show me the massing / layout" | hierarchy, walls, openings, slabs | rebar, FEM, materials, TechDraw |
| "model my house" | + doors/windows as BIM objects, stairs with §10 gates, footings with real sizes | FEM unless a member is claimed adequate |
| "is this beam OK / can this span" | + FEM per §9, hand-check, convergence | Psets, drawing sheets |
| "prepare it for my engineer" | + rebar cages, bar schedule, IFC export, §11.3 status block | nothing — this is the full pass |

---

# Part 2 — Structure, Foundations, Reinforcement, Verification

## 6. Foundations and footings as real parametric BIM objects

### 6.1 The object to use

`Arch.makeStructure` produces a `Part::FeaturePython` that accepts a real `IfcType` and exports correctly **[verified: `IFCFOOTING` present in exported .ifc]**. Never model a footing as a bare `Part::Box` in a deliverable model — a box carries no BIM classification and will not appear as a foundation in IFC, in a schedule, or in a quantity take-off.

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
| Plinth / grade beam | `Arch.makeStructure` | `Beam` | `IFCBEAM` |
| Column | `Arch.makeStructure` | `Column` | `IFCCOLUMN` |
| Beam / lintel | `Arch.makeStructure` | `Beam` | `IFCBEAM` |
| Slab | `Arch.makeStructure` or `Arch.makeFloor` slab | `Slab` | `IFCSLAB` |
| PCC / lean blinding | `Arch.makeStructure` | `Footing` (or plain solid, labelled) | — |
| Rebar | `Arch.makeRebar` | `Reinforcing Bar` | `IFCREINFORCINGBAR` **[verified]** |

Assign every foundation element to the **Foundation storey** at negative elevation, not to Ground (§1).

### 6.2 Footing type selection — decision tree

```
Is there a geotechnical report with a MEASURED allowable bearing pressure?
├─ NO  → you may NOT state a final footing size. Model a placeholder, label it
│         "ASSUMED 2000 psf / 95 kPa — REQUIRES GEOTECH", and say so in the reply (§11).
└─ YES → q_allow known
    │
    ├─ Load is a line load (masonry / RC wall)              → STRIP footing   (§6.3)
    ├─ Load is a point load (isolated column)               → PAD footing     (§6.4)
    ├─ Two columns close together / one near a boundary     → COMBINED footing — engineer
    ├─ Pads would cover >50% of plan area                   → RAFT / mat — out of scope, engineer
    ├─ q_allow < ~75 kPa, or expansive / collapsible soil   → PILES / under-reamed — engineer
    └─ Sloping site, or basement wall retaining >1.2 m      → retaining design — engineer
                                                              (see architecture-geotechnical-foundations)
```

Model the out-of-scope cases as clearly-labelled placeholders if the user needs the massing — never as if they were sized.

### 6.3 Strip (wall) footing — dimensional table

IRC-derived residential minimums, for **light-frame or single-leaf masonry** construction. Metric conversions are exact-rounded.

| Storeys | Soil 2000 psf (95 kPa) width | Soil 1500 psf (72 kPa) width | Min thickness |
|---|---|---|---|
| 1 | 12 in / **305 mm** | 16 in / 405 mm *[unverified, interpolated]* | 6 in / **150 mm** (IRC min) |
| 2 | 15 in / **380 mm** | 20 in / **510 mm** | 8 in / 200 mm (practice) |
| 3 | 18 in / **455 mm** | 24 in / 610 mm *[unverified, interpolated]* | 10–12 in / 250–300 mm (practice) |

- **Rule of thumb:** footing width = **2–3 × wall thickness**. A 230 mm brick wall → 460–690 mm strip. Cross-check the table row against this; if they disagree by more than ~30%, the assumed bearing pressure is probably wrong.
- **Thickness:** IRC absolute minimum **150 mm (6 in)**; standard practice **200–300 mm (8–12 in)**. Use practice, not the minimum.
- **Depth to underside:** must sit **below the local frost line** — 12 in (300 mm) in warm climates, up to 48 in (1200 mm) or more in cold. In Lahore/Punjab frost is not the governing case; **founding below the active/expansive zone and below any made-up fill** is. Typical Pakistani residential practice is 900–1500 mm below NGL, but this is a geotech decision, not a modeling one.
- **Model the PCC/lean layer** (typically 75–100 mm of 1:4:8 blinding under the footing) as a separate solid. Omitting it puts the rebar cage at the wrong absolute elevation, which cascades into plinth level and floor level.

Direct check of a modelled strip footing:

```python
def check_strip_footing(ftg, wall_thk_mm, line_load_kN_per_m, q_allow_kPa):
    B = min(ftg.Length.Value, ftg.Width.Value)      # footing width, mm
    h = ftg.Height.Value
    q_act = line_load_kN_per_m / (B / 1000.0)       # kPa (kN/m divided by m width)
    rows = [
        ("width >= 2 x wall thickness", B >= 2*wall_thk_mm, f"{B:.0f} vs {2*wall_thk_mm:.0f} mm"),
        ("thickness >= 150 mm (IRC min)", h >= 150, f"{h:.0f} mm"),
        ("thickness >= 200 mm (practice)", h >= 200, f"{h:.0f} mm"),
        ("bearing q_act <= q_allow", q_act <= q_allow_kPa, f"{q_act:.0f} vs {q_allow_kPa:.0f} kPa"),
    ]
    for n, ok, v in rows:
        print(f"  [{'PASS' if ok else 'FAIL'}] {n}  {v}")
    return all(r[1] for r in rows)
```

### 6.4 Pad (isolated) footing — sizing arithmetic

```
1. Service axial load on column      P    (kN)  ← from §8 load take-down, UNFACTORED for bearing
2. Required bearing area             A_req = P / q_allow          (m2)
3. Square side                       B = sqrt(A_req), round UP to 50 mm
4. Depth by ACI 318-19 §13.3.1.2     effective depth d >= 150 mm (6 in)
5. Overall thickness                 h = d + cover + one bar dia
                                       = 150 + 75 + 16 ~= 250 mm minimum
6. Punching (two-way) shear check    → GOVERNS most pads. Not doable reliably by hand here,
                                       and linear-elastic FEM does NOT check it either.
                                       Flag as ENGINEER-REQUIRED (§11).
7. One-way (beam) shear check        → also engineer-required
8. Overturning / eccentricity        → if the column is eccentric on the pad, resultant must
                                       stay in the middle third; otherwise → combined footing
```

**Worked example.** Column service load P = 320 kN, q_allow = 150 kPa.
`A_req = 320/150 = 2.13 m²` → `B = 1.46 m` → adopt **1500 × 1500 mm**.
Bearing check: `320 / (1.5×1.5) = 142 kPa ≤ 150 kPa` ✓.
Thickness: adopt **450 mm** (gives `d = 450 − 75 − 8 = 367 mm`, comfortably above the 150 mm floor, and helps punching shear).
Self-weight sanity: `1.5 × 1.5 × 0.45 × 24 = 24.3 kN` — about 7.6% of P, so re-checking bearing with self-weight gives `(320+24.3)/2.25 = 153 kPa` → **marginally over 150 kPa**. Adopt **1550 × 1550** or confirm q_allow. *Always add footing self-weight and overburden before declaring the bearing check passed* — this is the most common arithmetic omission.
This is otherwise exactly the `PadFooting_F1` object in §6.1.

### 6.5 ACI 318-19 concrete cover — non-negotiable, and it changes the geometry

| Condition | Cover |
|---|---|
| Cast against and permanently in contact with earth (footings, pile caps) | **75 mm (3 in)** |
| Cast in removable forms, then exposed to weather/earth, bars #6–#18 | **50 mm (2 in)** |
| Cast in removable forms, exposed to weather, bars #5 and smaller | 40 mm (1½ in) *[unverified]* |
| Not exposed to weather, slabs / walls / joists | 20 mm (¾ in) *[unverified]* |
| Not exposed to weather, beams / columns (measured to the **tie**, not the main bar) | 40 mm (1½ in) *[unverified]* |

Cover is **modeled geometry**, not a note. It sets `Arch.makeRebar(offset=...)` (§7) and it reduces effective depth `d`, which reduces capacity. Getting cover wrong on the earth face of a footing is the single most common way a modeled rebar cage is quietly wrong.

**Note on the mm values above:** the metric figures in this table are rounded from the inch values in common practice (e.g. 1½ in is properly 38.1 mm, shown here as 40 mm; ¾ in is 19.05 mm, shown as 20 mm) rather than independently derived metric clause values — they are marked *[unverified]* for exactly this reason. Use the inch value if you have the real ACI 318-19 clause open, and treat the mm figure as a rounded convenience, not a precise transcription.

**Cover propagates:** `d = h − cover − (tie dia if present) − (main bar dia / 2)`. Model that arithmetic explicitly rather than assuming `d = h − 75`.

### 6.6 Slab thickness — ACI 318-19 Table 24.2.2 (one-way, non-prestressed, normal-weight, Grade 60)

| Support condition | Minimum h |
|---|---|
| Simply supported | ℓ / 20 |
| One end continuous | ℓ / 24 |
| Both ends continuous | **ℓ / 28** |
| Cantilever | ℓ / 10 |

For a 4200 mm clear span, both ends continuous: `h ≥ 4200/28 = 150 mm`. This is a **deflection-control** minimum that lets you skip an explicit deflection calculation — it is **not** a strength check, and it does not apply to two-way slabs (ACI 318-19 Table 8.3.1.1 governs those).

### 6.7 Plinth beams and grade beams — the element most often forgotten

A house on isolated pads without a plinth/grade beam tying them together has no mechanism to resist differential settlement or to distribute seismic base shear. In Pakistani residential practice a plinth beam is standard and BCP-SP 2007 seismic detailing expects tie beams.

| Item | Typical residential value | Note |
|---|---|---|
| Plinth beam depth | 225–300 mm | *[practice, unverified]* |
| Plinth beam width | = wall thickness (230 mm typical) | |
| Position | at or just below DPC level, spanning pad-to-pad | |
| Model as | `Arch.makeStructure`, `IfcType="Beam"`, Plinth storey | |

If the model omits plinth beams, say so in the §11.3 block under "Not modelled" — an absent tie beam is a real structural difference, not a level of detail.

## 7. Reinforcement as real parametric BIM objects

> Scope boundary: this section covers **how to build a rebar cage in FreeCAD and check it against minimums**. Development lengths, lap splices, hook geometry, curtailment, bar bending schedules in construction format, and seismic confinement detailing live in `architecture-concrete-reinforcement-detailing`. Do not re-derive those here; cite and defer.

### 7.1 `Arch.makeRebar` — the verified working recipe

`Arch.makeRebar(baseobj, sketch, diameter, amount, offset, name)` **[verified]**. It needs a **sketch attached to a face of the host** describing one bar's path; it then replicates that bar `amount` times across the host and computes `Spacing` and `TotalLength` itself.

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

Observed properties **[verified]**: `Amount`, `Diameter`, `Direction`, `Distance`, `Host`, `Mark`, `Material`, `OffsetStart`, `OffsetEnd`, `Rounding`, `Spacing`, `TotalLength`, `IfcType = "Reinforcing Bar"`. Exports as **`IFCREINFORCINGBAR`** **[verified]**.

- `offset` is the **cover** — pass 75 for an earth-cast footing (§6.5), never leave it at 0.
- `Spacing` is **derived**, not set. To hit a target spacing, solve for `amount`: `amount = floor((L − 2·cover) / s_target) + 1`.
- `TotalLength` is the bar-schedule quantity. Use it directly for steel take-off; do not re-derive it.
- `host.Armatures` stays empty in the scripted path — check `rb.Host` instead **[verified gotcha]**.
- **`Direction` defaults to `(0,0,0)` and must be set explicitly, or `Spacing` silently computes a degenerate value unrelated to the host's real length** [verified]: with `Direction=(0,0,0)`, `amount=51, offset=75` on a 10287mm-long strip footing returned `Spacing=3mm` (bars packed nonsensically close) — the tool was distributing the bars over a span derived from `2*offset` (150mm), not the host's actual extent. Setting `rb.Direction = App.Vector(0,1,0)` (the host's real replication axis) before/after creation fixed it immediately: same `amount=51` then gave `Spacing=202.7mm`, matching the intended ~200mm target. **Always set `Direction` explicitly to the axis you want the bars spread along, and verify `Spacing` looks sane (compare it to `host_length / (amount-1)`) before trusting the cage** — don't assume the tool infers replication direction from the sketch or the host geometry.
- `Rounding` is the bend radius as a **multiple of bar diameter** *[unverified]*; ACI minimum bend diameter is 6d_b for #3–#8. Leaving it at 0 models a physically unbuildable sharp bend.
- `Mark` is the bar mark for the schedule — set it (`F1-B1`, `C1-MAIN`, `B2-STIRRUP`) so the take-off is readable.
- A full cage needs **two orthogonal bottom mats** (one sketch per direction), plus top steel where the member is continuous or cantilevered.

### 7.2 Stirrups, ties and links — closed-loop rebar

A straight-line sketch gives a straight bar. A **closed rectangular sketch** (four `LineSegment`s, or a `Sketcher` rectangle) on a **cross-section face** gives a stirrup/tie, replicated along the member axis *[unverified — pattern follows directly from the verified straight-bar behaviour but has not been round-tripped]*.

```python
col = doc.getObjectsByLabel("Column_C1")[0]      # 300 x 300 x 3000
sk = doc.addObject("Sketcher::SketchObject", "TiePath_C1")
sk.AttachmentSupport = [(col, "Face5")]          # bottom cross-section face
sk.MapMode = "FlatFace"
doc.recompute()
c = 40                                           # cover to tie (§6.5)
a, b = 150 - c, 150 - c                          # half-dims inside cover
pts = [App.Vector(-a,-b,0), App.Vector(a,-b,0), App.Vector(a,b,0), App.Vector(-a,b,0)]
for i in range(4):
    sk.addGeometry(Part.LineSegment(pts[i], pts[(i+1) % 4]), False)
doc.recompute()

# amount from the §7.3 tie-spacing rule, not from taste
tie = Arch.makeRebar(col, sk, diameter=10, amount=11, offset=40, name="C1_Ties")
tie.Mark = "C1-TIE"
tie.Rounding = 4          # bend radius as multiple of dia  [unverified]
doc.recompute()
```

Ties must close with **135° seismic hooks** in any seismic zone (BCP-SP 2007 / ACI 318-19 Ch. 18). `Arch.makeRebar` will not model the hook geometry from a plain closed rectangle — state that the hooks are **not modelled** rather than implying the detail is complete.

### 7.3 Minimum and maximum reinforcement — ACI 318-19

**Footings and slabs:**

| Rule | Value | Section |
|---|---|---|
| Min flexural / shrinkage-temp ratio, Grade 60 | **A_s ≥ 0.0018 · A_g** | ACI 318-19 |
| Same, Grade 40 | **A_s ≥ 0.0020 · A_g** | ACI 318-19 |
| Min effective depth, foundation bottom bars | **d ≥ 150 mm (6 in)** | §13.3.1.2 |
| Max spacing, shrinkage/temp bars | lesser of **5h** or **450 mm (18 in)** | ACI 318-19 |
| Max spacing, primary flexural bars in slabs | lesser of **3h** or **450 mm** | ACI 318-19 §7.7.2.3 *[unverified]* |

**Check the modeled cage against the minimum — always.** For the 1500×1500×450 footing above, per direction:
`A_g = 1500 × 450 = 675,000 mm²` → `A_s,min = 0.0018 × 675,000 = 1215 mm²`.
Modeled: 7 × Ø12 = `7 × 113.1 = 792 mm²` → **FAILS by 35%**.
Fix: 7 × Ø16 = `7 × 201.1 = 1408 mm² ≥ 1215` ✓, or 11 × Ø12 = 1244 mm² ✓ (spacing `(1500−150)/10 = 135 mm`).
This is the check to script and print for **every** rebar object you create — the modeled cage in §7.1 is deliberately shown failing it, because a plausible-looking cage that is short on steel is exactly the silent error this section exists to catch.

```python
import math

BAR_AREA = {8: 50.3, 10: 78.5, 12: 113.1, 16: 201.1, 20: 314.2, 25: 490.9, 32: 804.2}

def check_min_steel(dia_mm, amount, width_mm, thickness_mm, grade=60):
    ratio   = 0.0018 if grade >= 60 else 0.0020
    as_prov = amount * math.pi * (dia_mm ** 2) / 4
    as_min  = ratio * width_mm * thickness_mm
    ok = as_prov >= as_min
    print(f"  As_prov={as_prov:.0f} mm2  As_min={as_min:.0f} mm2  -> {'PASS' if ok else 'FAIL'}")
    return ok

def check_max_spacing(spacing_mm, h_mm, kind="temp"):
    lim = min(5*h_mm, 450.0) if kind == "temp" else min(3*h_mm, 450.0)
    ok = spacing_mm <= lim
    print(f"  spacing={spacing_mm:.0f} mm  limit={lim:.0f} mm -> {'PASS' if ok else 'FAIL'}")
    return ok

def audit_all_rebar(doc):
    """Run over every rebar object in the document and report. Run before every handoff."""
    bad = []
    for o in doc.Objects:
        if getattr(o, "IfcType", None) == "Reinforcing Bar":
            host = o.Host
            print(f"{o.Label}  host={host.Label if host else 'NONE'}  "
                  f"dia={o.Diameter}  n={o.Amount}  s={o.Spacing}  L={o.TotalLength}")
            if host is None:
                bad.append((o.Label, "no host"))
            if o.OffsetStart.Value == 0 and o.OffsetEnd.Value == 0:
                bad.append((o.Label, "zero cover offset"))
    for lbl, why in bad:
        print(f"  [FAIL] {lbl}: {why}")
    return not bad
```

### 7.4 Column reinforcement — ACI 318-19 §10.6.1.1 and §25.7.2

| Rule | Value |
|---|---|
| Longitudinal steel ratio ρ_g = A_st / A_g | **1% ≤ ρ_g ≤ 8%** (§10.6.1.1) |
| Practical upper bound at lap-splice locations | ~4% (8% doubles at a lap and becomes unplaceable) *[practice]* |
| Min number of longitudinal bars, rectangular tied column | 4 *[unverified]* |
| Tie size, longitudinal bars #10 and smaller | **#3** (§25.7.2) |
| Tie size, longitudinal bars #11 / #14 / #18 | **#4** (§25.7.2) |
| Max tie spacing | smallest of **16 × d_long**, **48 × d_tie**, **least column dimension** (§25.7.2) |

**Worked example.** 300 × 300 mm column, 4 × Ø16 longitudinal, Ø10 ties.
`A_g = 90,000 mm²`; `A_st = 4 × 201.1 = 804 mm²`; `ρ_g = 0.89%` → **FAILS the 1% floor**.
Fix: 4 × Ø20 = `1257 mm²` → `ρ_g = 1.40%` ✓ (and comfortably below 8% = 7200 mm²).
Tie spacing = min(16×20, 48×10, 300) = min(320, 480, 300) = **300 mm**. Adopt 300 mm, reduced to 150 mm in confinement zones near joints *[unverified — seismic detailing is BCP-SP 2007 / ACI Ch.18 territory, engineer-required]*.
Number of ties over a 3000 mm column at 300 mm: `floor(3000/300) + 1 = 11` → matches the `amount=11` in §7.2.

```python
def check_column_rebar(b_mm, h_mm, dia_long, n_long, dia_tie, tie_spacing_mm):
    ag   = b_mm * h_mm
    ast  = n_long * math.pi * dia_long**2 / 4
    rho  = ast / ag
    s_lim = min(16*dia_long, 48*dia_tie, min(b_mm, h_mm))
    rows = [
        ("rho_g >= 1% (ACI 10.6.1.1)", rho >= 0.01,  f"{rho*100:.2f}%"),
        ("rho_g <= 8% (ACI 10.6.1.1)", rho <= 0.08,  f"{rho*100:.2f}%"),
        ("n_long >= 4",                n_long >= 4,  f"{n_long}"),
        ("tie spacing <= limit (ACI 25.7.2)", tie_spacing_mm <= s_lim,
                                       f"{tie_spacing_mm:.0f} vs {s_lim:.0f} mm"),
    ]
    for n, ok, v in rows:
        print(f"  [{'PASS' if ok else 'FAIL'}] {n}  {v}")
    return all(r[1] for r in rows)
```

### 7.5 Steel take-off straight from the model

`TotalLength` is authoritative **[verified]** — use it, don't re-derive it.

| Bar Ø (mm) | Area (mm²) | Mass (kg/m) |
|---|---|---|
| 8 | 50.3 | 0.395 |
| 10 | 78.5 | 0.617 |
| 12 | 113.1 | 0.888 |
| 16 | 201.1 | 1.578 |
| 20 | 314.2 | 2.466 |
| 25 | 490.9 | 3.853 |
| 32 | 804.2 | 6.313 |

`mass_per_m = dia² / 162` (kg/m, dia in mm) — the standard site formula, matching the table.

```python
def steel_takeoff(doc):
    total_kg = 0.0
    for o in doc.Objects:
        if getattr(o, "IfcType", None) == "Reinforcing Bar":
            L_m = o.TotalLength.getValueAs("mm").Value / 1000.0
            d   = o.Diameter.getValueAs("mm").Value
            kg  = L_m * (d*d) / 162.0
            total_kg += kg
            print(f"{o.Mark or o.Label:<16} Ø{d:.0f}  {L_m:7.2f} m  {kg:7.1f} kg")
    print(f"TOTAL STEEL (model geometry only, NO laps/hooks/wastage): {total_kg:.0f} kg")
    return total_kg
```

**This is a model quantity, not a BOQ.** Add laps, hooks, chairs, wastage (typically +3–5% wastage and +5–10% for laps) — see `architecture-cost-estimation-boq`. Never hand this number over labelled as a steel order.

### 7.6 Pakistan note

`BCP-2007` (seismic provisions, post-2005 Kashmir earthquake) and **BCP-2021** (Pakistan Engineering Council) are the locally applicable codes and must be named as such in any deliverable. Their specific foundation and reinforcement clauses were **not retrievable** during the research behind this skill and are therefore **not quoted numerically anywhere in it**. All numeric values above are **ACI 318-19 / IRC 2021 / ASCE 7-22**. For a real Pakistani project, obtain the BCP PDF directly from `pec.org.pk` and reconcile before citing any number as BCP-derived. **Do not present an ACI number as a BCP number.** `architecture-building-codes-permits` and `architecture-seismic-design` carry the Pakistan-specific overlay.

## 8. Load derivation — ASCE 7-22, to get real numbers into the solver

An FEM run is only as honest as the load you feed it. **Never invent a force value.** Every `ConstraintForce` or `ConstraintPressure` in the model must be traceable to a written take-down.

**Cross-check against `architecture-structural-systems` before treating §8 as final.** This section builds its own tributary-area / ASCE 7-22 load path from scratch, which is fine for a from-first-principles take-down, but it is not a substitute for the preliminary member-sizing tables and load-path narrative that `architecture-structural-systems` owns. Before running FEM on a member sized here: (1) pull that skill's preliminary span/depth guidance for the same member type and span, (2) compare it against the §8.4 take-down and the section chosen in §6/§7, and (3) if the two disagree by more than ~15–20%, say so explicitly and treat the discrepancy as a flag to resolve — not something to silently average or discard in favour of whichever number is more convenient. Don't present the §8 load path as the whole structural-sizing story; it is the FEM-input half of it.

### 8.1 Load table

| Load | Value (imperial) | Value (metric) | Source |
|---|---|---|---|
| Residential live, rooms other than sleeping | **40 psf** | **1.92 kPa** | ASCE 7-22 Table 4.3-1 |
| Residential live, sleeping rooms | 30 psf | 1.44 kPa | ASCE 7-22 Table 4.3-1 *[unverified]* |
| Stairs and exit ways, residential | 40 psf | 1.92 kPa | ASCE 7-22 Table 4.3-1 *[unverified]* |
| Balconies / decks | 1.5 × the served occupancy, ≤ 100 psf | — | ASCE 7-22 Table 4.3-1 *[unverified]* |
| Live load reduction, large tributary area | per §4.7.2 | — | ASCE 7-22 §4.7.2 |
| Roof live, reducible low-slope / large tributary | down to **12 psf** | **0.57 kPa** | ASCE 7-22 |
| Dead, wood-framed floor, structure only | ~10 psf | ~0.48 kPa | typical |
| Dead, wood floor with tile / stone finish | 12–15+ psf | 0.57–0.72 kPa | typical |
| Dead, 150 mm RC slab | — | **3.60 kPa** (24 kN/m³ × 0.15) | computed |
| Dead, floor finish + screed (50 mm) | — | ~1.20 kPa | practice |
| Dead, 230 mm brick wall, 3 m high | — | ~**12.4 kN/m** run (18 kN/m³) | computed |
| Dead, 115 mm brick partition, 3 m high | — | ~6.2 kN/m run | computed |
| Dead, plaster both faces | — | ~0.4 kPa on wall area | practice |
| Water tank (1000 L on roof) | — | ~10 kN point + tank dead | computed |

Unit weights used: RC **24 kN/m³**, brick masonry **18–20 kN/m³**, plain concrete/PCC **23 kN/m³**, water **9.81 kN/m³**, steel **77 kN/m³**.

### 8.2 Load combinations

| Purpose | Combination |
|---|---|
| Strength (what you feed the **stress** check) | **1.2 D + 1.6 L** (ASCE 7-22 §2.3.1) |
| Strength, dead-dominated | 1.4 D |
| Strength with roof live | 1.2 D + 1.6 L_r + 0.5 L *[unverified]* |
| Serviceability (what you feed the **deflection** check) | **1.0 D + 1.0 L** |
| Bearing pressure on soil (footing sizing) | **unfactored service**: 1.0 D + 1.0 L |

**Run stress and deflection as separate FEM analyses.** A factored-load deflection compared against an L/360 limit is meaningless, and a service-load stress compared against a factored capacity is unconservative. Getting these crossed is a common and invisible error.

Lateral load combinations (wind, seismic) exist in ASCE 7-22 §2.3 and BCP-SP 2007 but are **out of scope for this FEM workflow** — the pipeline here is gravity-only. Say so.

**Pakistan is a seismic country — this gap is not cosmetic.** Every numeric value in this skill (§8, §9, §13) is gravity-only ACI/ASCE/IRC; no seismic base shear, wall density, drift limit, or confined-masonry detailing is derived anywhere in this file. This skill defers that entirely to `architecture-seismic-design`. Do not just cite that skill name in a reply — before telling the user a model or a member is "checked", actually invoke `architecture-seismic-design` (or confirm it has already run for this project) whenever the building is a real occupied structure in a seismic zone. If that skill is unavailable or has not been run, the §11.3 status block must say so explicitly (e.g. *"lateral/seismic: NOT evaluated — architecture-seismic-design not invoked"*), not merely list "wind/seismic" among generic unchecked items.

### 8.3 Tributary-area take-down → force in newtons

```
w_area (kPa)  ->  w_line (kN/m) = w_area x tributary_width
              ->  F_total (kN)  = w_line x span
              ->  N             = F_total x 1000
```

**Worked example** (this is the load used in the validated FEM run in §9):
RC beam, span 3.0 m, tributary width 3.0 m, 150 mm slab.
- Dead: slab 3.60 + finishes 1.20 = **4.80 kPa**
- Live: **1.92 kPa** (ASCE 7-22 Table 4.3-1)
- Factored: `1.2(4.80) + 1.6(1.92) = 5.76 + 3.07 = 8.83 kPa`
- Line load: `8.83 × 3.0 = 26.5 kN/m`
- On a 3.0 m span: `26.5 × 3.0 = 79.5 kN` total.

The validated run in §9 used a deliberately lighter **21.6 kN** (a 7.2 N/mm UDL) so the hand-check arithmetic stays clean and the concrete stays uncracked; substitute the real factored load for real work.

### 8.4 Full roof-to-soil load path — the take-down that feeds every member check

This is the table to build once per house, then reuse for every FEM run and every footing. G+1 house, 3.0 × 3.0 m tributary bay, 150 mm slabs, 230 mm walls, 3.0 m storey height.

| Level | Element | Load contribution | Running service total |
|---|---|---|---|
| Roof | 150 mm RC slab | 3.60 kPa × 9 m² = 32.4 kN | 32.4 kN |
| Roof | finish + waterproofing | 1.00 kPa × 9 = 9.0 kN | 41.4 kN |
| Roof | roof live (reduced) | 0.57 kPa × 9 = 5.1 kN | 46.5 kN |
| Upper | 1st-floor slab dead | 4.80 × 9 = 43.2 kN | 89.7 kN |
| Upper | 1st-floor live | 1.92 × 9 = 17.3 kN | 107.0 kN |
| Upper | walls on this floor (3 m wall run × 12.4 kN/m = 37.2 kN) | 37.2 kN | 144.2 kN |
| Ground | ground-floor walls | 37.2 kN | 181.4 kN |
| Ground | column self-weight (0.3×0.3×6.0×24) | 13.0 kN | 194.4 kN |
| Foundation | **service axial at footing** | — | **≈ 194 kN** |
| Foundation | footing self-weight (1.2×1.2×0.4×24) | 13.8 kN | **≈ 208 kN on soil** |

At q_allow = 150 kPa: `A_req = 208/150 = 1.39 m²` → `B = 1.18 m` → adopt **1200 × 1200 mm**, re-check `208/1.44 = 144 kPa ≤ 150` ✓.

Print this table alongside any footing size you state. A footing size with no visible take-down is an unsupported claim, even when the arithmetic happened correctly off-screen.

### 8.5 Converting a take-down into the right FEM constraint

| Physical load | FEM constraint | How to compute the value |
|---|---|---|
| UDL over a beam top face | `ConstraintForce` on the top face | total N = w_line (N/mm) × span (mm); FreeCAD distributes over the face |
| Area load on a slab | `ConstraintPressure` on the top face | pressure in MPa = kPa / 1000; e.g. 8.83 kPa → `"0.00883 MPa"` |
| Point load (column onto beam) | `ConstraintForce` on a small partitioned face, or a vertex | partition the face first, or accept a local stress artifact |
| Self-weight | `ConstraintSelfWeight` | requires `Density` set on the material; add it whenever self-weight is non-trivial |
| Axial on a column | `ConstraintForce` on the top face, `Reversed=True` | total service or factored N from §8.4 |
| Soil reaction under a footing | `ConstraintPressure` on the bottom face (upward) | q_act in MPa; pair with the column load on top |

**Pressure unit trap:** 8.83 kPa = 0.00883 MPa. Passing `8.83` as a bare float means `8.83 kg/(mm·s²)` = 0.00883 MPa by accident in this case, but the coincidence does not generalise — always pass the unit string.

## 9. FEM verification — the actual, validated pipeline

### 9.1 What the tool does and does not do

`mcp__freecad__run_fem_analysis(doc_name, analysis_name, timeout=600, include_screenshot=True, view_name="Isometric")` **only runs the solver on an analysis you have already fully assembled.** It creates nothing except the `SolverCcxTools` object.

**You must build all of these first:**

1. A Part-derived solid — a `Part::Box` proxy, or an Arch object (`Part::FeaturePython`) directly **[verified: gmsh meshed an `Arch.makeStructure` footing to 237 nodes]**.
2. `Fem::FemAnalysis` container — `ObjectsFem.makeAnalysis(doc, "Name")`. (The tool's docstring says `Fem::AnalysisPython`; `Fem::FemAnalysis` from `makeAnalysis` **is accepted** **[verified]**.)
3. A material — `ObjectsFem.makeMaterialSolid`, added to the analysis.
4. At least one `Fem::ConstraintFixed` **and** one `Fem::ConstraintForce` or `Fem::ConstraintPressure`, bound to named faces, added to the analysis.
5. A `Fem::FemMeshGmsh` referencing the geometry, added to the analysis, **with the mesh actually generated**.

**It returns:** `max_von_mises_MPa`, `min_von_mises_MPa`, `max_displacement_mm`, `node_count`, `working_dir`, `result_object`.
**It does NOT return a safety factor** — you compute that yourself (§9.5). Any claim of a solver-reported safety factor is wrong for this environment.

**Operational constraints:**
- The solver runs **synchronously on the FreeCAD GUI thread and blocks every other RPC call** — never fan out parallel FreeCAD requests around it.
- Default `timeout=600 s`. A house-scale member at ~3000 nodes solves in seconds; a full-building mesh will time out. **Analyse one member at a time.**
- Repeated runs accumulate `CCX_Results`, `CCX_Results001`, … in the document; read the newest, or delete old ones between runs (§9.8).
- Use `include_screenshot=False` for numeric runs; the stress plot costs tokens and adds nothing to a number you are about to hand-check.

**What the pipeline structurally cannot tell you** — state these as not-checked in every §11.3 block:

```
buckling (linear static only)      punching shear        cracking / tension stiffening
long-term deflection / creep       reinforcement bond     connection capacity
fatigue                            lateral / seismic      wind
torsional stability                soil-structure interaction    settlement
construction-stage loading         thermal / shrinkage restraint
```

### 9.2 Verify face indices before binding constraints — never assume

A constraint bound to the wrong face produces a **fully successful solve with meaningless numbers.** This is the highest-severity silent failure in the whole workflow.

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

Assert the face you picked has the center and area you expect **before** attaching a constraint to it. Re-run `dump_faces` after **any** boolean/Subtraction change — face indices are not stable across a boolean.

### 9.3 The full working script [verified end-to-end]

```python
import FreeCAD as App, ObjectsFem
from femmesh.gmshtools import GmshTools

doc  = App.newDocument("BeamCheck")
beam = doc.addObject("Part::Box", "BeamProxy")
beam.Length, beam.Width, beam.Height = 3000, 300, 450   # mm
doc.recompute()
dump_faces(beam)                      # §9.2 — and assert before binding

analysis = ObjectsFem.makeAnalysis(doc, "BeamCheck")

mat = ObjectsFem.makeMaterialSolid(doc, "ConcreteC30")
m = mat.Material
m['Name']          = 'Concrete-C30/37'
m['YoungsModulus'] = '30000 MPa'      # see §9.4 on choosing E
m['PoissonRatio']  = '0.20'
m['Density']       = '2400 kg/m^3'
mat.Material = m
analysis.addObject(mat)

fix = ObjectsFem.makeConstraintFixed(doc, "FixedEnd")
fix.References = [(beam, "Face1")]
analysis.addObject(fix)

frc = ObjectsFem.makeConstraintForce(doc, "FloorLoad")
frc.References = [(beam, "Face6")]
frc.Force    = "21600 N"      # from the §8 take-down. ALWAYS a unit string.
frc.Reversed = True           # Face6 normal is +Z, so Reversed => downward
analysis.addObject(frc)

msh = ObjectsFem.makeMeshGmsh(doc, "BeamMesh")
msh.Shape                   = beam
msh.CharacteristicLengthMax = "120 mm"
msh.ElementOrder            = "2nd"     # 2nd order is REQUIRED for bending accuracy
analysis.addObject(msh)
doc.recompute()
GmshTools(msh).create_mesh()
print("nodes:", msh.FemMesh.NodeCount, "volumes:", msh.FemMesh.VolumeCount)
# -> nodes: 2713 volumes: 1334   [verified]
```

Then call the tool:

```
mcp__freecad__run_fem_analysis(doc_name="BeamCheck", analysis_name="BeamCheck",
                               include_screenshot=False, timeout=300)
```

Actual returned result **[verified]**:

```json
{"success": true, "max_von_mises_MPa": 3.1926, "min_von_mises_MPa": 0.00042,
 "max_displacement_mm": 1.0909, "node_count": 2713,
 "working_dir": "/tmp/freecad_mcp_fem_ax8l10hu"}
```

**Constraint reference** — all **[verified]**:

| Constraint | Factory | Key properties |
|---|---|---|
| Fixed | `makeConstraintFixed` | `References` |
| Force | `makeConstraintForce` | `Force`, `Direction`, `Reversed`, `References` |
| Pressure | `makeConstraintPressure` | `Pressure`, `Reversed`, `Scale`, `References` (internal unit `kg/(mm·s²)` — pass `"0.005 MPa"`) |
| Self-weight | `makeConstraintSelfWeight` | `GravityAcceleration`, `GravityDirection` — add whenever `Density` is set and self-weight matters |
| Displacement | `makeConstraintDisplacement` | per-axis `x/y/zFix` / `xFree` … — the tool for releasing rotation to model a real simple support (§9.6) *[unverified property names]* |

### 9.4 Calibrate against hand calculation — mandatory, every time

A solver run that has not been sanity-checked against closed-form statics **is not evidence.** For the validated case above (cantilever, `w = 21600/3000 = 7.2 N/mm`, `b = 300`, `h = 450`, `L = 3000`, `E = 30000 MPa`):

| Quantity | Hand calculation | FEM | Δ |
|---|---|---|---|
| Bending stress | `M = wL²/2 = 32.4×10⁶ N·mm`; `S = bh²/6 = 10.125×10⁶ mm³`; `σ = 3.20 MPa` | **3.193 MPa** | **0.2%** |
| Tip deflection | `I = bh³/12 = 2.278×10⁹ mm⁴`; `δ = wL⁴/8EI = 1.067 mm` | **1.091 mm** | **2.3%** (shear deformation) |

**Closed-form formulas to calibrate against** (UDL `w` in N/mm, span `L` in mm):

| Case | M_max | δ_max |
|---|---|---|
| Cantilever, UDL | `wL²/2` (at support) | `wL⁴/(8EI)` |
| Cantilever, point load P at tip | `PL` | `PL³/(3EI)` |
| Simply supported, UDL | `wL²/8` (midspan) | `5wL⁴/(384EI)` |
| Simply supported, point load P at midspan | `PL/4` | `PL³/(48EI)` |
| Fixed-fixed, UDL | `wL²/12` (support), `wL²/24` (mid) | `wL⁴/(384EI)` |
| Propped cantilever, UDL | `wL²/8` (fixed end) | `wL⁴/(185EI)` *[unverified]* |

With `σ = M/S`, `S = bh²/6`, `I = bh³/12`.

**Acceptance:** if your Δ exceeds ~10%, **something is wrong with the model, not with statics** — wrong face, wrong load direction, unit error, mesh too coarse, or 1st-order elements. Fix it before reporting a number.

**On the modulus:** the run used `E = 30000 MPa`. ACI 318-19 §19.2.2.1 gives `E_c = 4700√f'c`, so for f'c = 30 MPa the correct value is **25,740 MPa** — which would increase the computed deflection by ~17%. The E you feed **directly scales the deflection result**; state which one you used.

| f'c (MPa) | `E_c = 4700√f'c` (MPa) | Common Pakistani grade equivalent |
|---|---|---|
| 17 (M20-ish) | 19,380 | M20 |
| 21 | 21,538 | M20/M25 |
| 25 | 23,500 | M25 |
| 30 | **25,743** | M30 |
| 35 | 27,806 | M35 |

### 9.5 Material presets for the FEM material object

| Material | E (MPa) | ν | ρ (kg/m³) | Limit to compare against |
|---|---|---|---|---|
| Structural steel (S275 / A36-ish) | **210,000** | **0.30** | **7800** | **yield 250 MPa** — von Mises valid |
| Reinforcing steel Grade 60 | 200,000 | 0.30 | 7850 | yield 420 MPa *[unverified]* |
| Concrete C30/37 (f'c 30) | 25,743 (per ACI) | 0.20 | 2400 | tension `f_r = 0.62√f'c` = **3.40 MPa**; compression 0.45f'c ≈ 13.5 MPa service *[unverified]* |
| Concrete C25 (f'c 25) | 23,500 | 0.20 | 2400 | `f_r` = 3.10 MPa |
| Concrete C20 (f'c 20) | 21,019 | 0.20 | 2400 | `f_r` = 2.77 MPa |
| Brick masonry | 3,000–8,000 *[unverified]* | 0.15–0.20 | 1900 | compression only; tension ≈ 0 — von Mises meaningless |
| Softwood timber (parallel to grain) | ~11,000 *[unverified]* | 0.35 | 500 | strongly **orthotropic** — isotropic FEM is a poor model |

Only the steel row was used in a validated run; the concrete C30 row was used with `E = 30000` (see §9.4 for why that was slightly wrong).

### 9.6 Interpreting the result — and where von Mises lies to you

```python
SF = f_yield / max_von_mises        # steel only
```

| Material | Criterion | Verdict rule |
|---|---|---|
| Structural steel | von Mises vs yield | `SF = 250 / σ_vm`. Target **SF ≥ 1.67** on service load — this is the classic allowable-stress-design factor (1/0.6 ≈ 1.67, the AISC ASD Ω for yielding), quoted here as a screening target, not an FEM-reported or code-mandated value for this workflow. State it as a hand-adopted target, and cite AISC 360 Ch. B / ASD if a real design basis is needed. |
| Concrete, tension | `f_r = 0.62√f'c` (3.40 MPa for f'c 30) | von Mises is **NOT** a valid failure criterion for concrete. Compare **max principal tensile stress** to `f_r`, and treat exceedance as "it cracks", not "it fails". |
| Concrete, compression | 0.45 f'c service ≈ 13.5 MPa for f'c 30 *[unverified]* | screening only |
| Masonry / timber | — | isotropic linear FEM is not a valid model; do not report a safety factor |

For the validated beam: `σ_max = 3.193 MPa` vs `f_r = 3.40 MPa` → the section is **marginally uncracked at this load**, with only 6% margin. Under the real §8.3 factored load (79.5 kN, ~3.7× larger) it would crack decisively — which is normal and expected for reinforced concrete, and is precisely why a linear-elastic uncracked FEM **cannot** verify an RC member. **It can tell you whether the section cracks; it cannot tell you whether the reinforced section is adequate after it does.**

**Deflection gates** *[unverified — ACI 318-19 Table 24.2.2 deflection limits]*:

| Limit | Ratio | For L = 3000 mm |
|---|---|---|
| Immediate live-load deflection | **L/360** | 8.3 mm |
| Total (incl. long-term), members supporting non-structural elements likely to be damaged | **L/480** | 6.3 mm |
| Total, not supporting damageable elements | **L/240** | 12.5 mm |

The 1.091 mm result passes all three — but it was computed on an unfactored, unrealistically light load, and linear FEM gives **immediate elastic** deflection only. Long-term multiplier for sustained load is roughly 2.0 for RC *[unverified — ACI 318-19 §24.2.4.1.1]*.

**Columns:** linear static FEM reports axial stress, **not buckling**. Do a separate Euler hand-check and report it as a hand-check:

```
P_cr = pi^2 * E * I / (k*L)^2          k = 1.0 pinned-pinned, 0.5 fixed-fixed, 2.0 cantilever
r    = sqrt(I/A) = 0.3h for a rectangle
Slenderness may be NEGLECTED (ACI 318-19 §6.2.5) if:
   braced/non-sway frame:  k*Lu/r <= 34 - 12(M1/M2) <= 40        [unverified]
   sway frame:             k*Lu/r <= 22                          [unverified]
```

For a 300×300 mm, 3000 mm column: `r = 0.3 × 300 = 90 mm`; `k=1.0` → `kL/r = 33.3` → below 34, slenderness likely negligible in a braced frame. State it as a hand-check, not as an FEM result.

**Mesh convergence:** one run is one data point. Re-run at roughly half the `CharacteristicLengthMax`; if peak stress moves more than **~5%**, the mesh is not converged and the number is not reportable.

| Run | `CharacteristicLengthMax` | Nodes | σ_vm | Δ vs previous |
|---|---|---|---|---|
| 1 | 120 mm | 2713 | 3.193 MPa | — |
| 2 | 60 mm | *(re-run)* | *(record)* | must be < 5% to report |

Peak stress at a fixed-support face is a **singularity** — it grows without bound as the mesh refines. Read stress away from the support (roughly one member-depth in), or state explicitly that the reported peak is a support artifact.

### 9.7 Boundary conditions — the most common way to get a wrong-but-plausible answer

| Real condition | Wrong FEM idealization | Consequence | Do instead |
|---|---|---|---|
| Simply supported beam | `ConstraintFixed` on **both** ends | Fixed-fixed midspan moment is `wL²/24` vs `wL²/8` simply supported — **understates bending by ~3×**. Dangerously unconservative. | `ConstraintDisplacement` releasing rotation, or model as a cantilever and accept conservatism |
| Beam on masonry bearing | Fixed | overstates restraint, understates deflection | partial `ConstraintDisplacement` |
| Continuous beam over a middle support | analysing one span in isolation | misses the hogging moment over the support | model both spans, or hand-check the hogging case |
| Column base on pad footing | Fixed | overstates fixity, understates sway | acceptable for axial-only screening; **never** for lateral |
| Slab supported on 4 walls | Fixed on all 4 edges | overstates two-way stiffness | pinned edges is the conservative screen |
| Any model with only forces, no fixed constraint | solver runs, huge/garbage displacements | rigid-body motion — the model is unrestrained | at least one `ConstraintFixed` is mandatory |

**When in doubt, choose the conservative idealization and say which one you chose.** "Modelled as a cantilever (conservative); the real condition is partially restrained" is an honest sentence. "The beam is fine" is not.

### 9.8 Solver troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Prerequisite-check error from the tool | missing material / mesh / constraint / analysis membership | re-check the 5 prerequisites in §9.1; confirm each object is in `analysis.Group` |
| Enormous displacement (metres) | rigid-body motion — no fixed constraint, or fixed on a face that doesn't restrain all 6 DOF | add/extend `ConstraintFixed` |
| `nonpositive jacobian` in ccx output | degenerate mesh, usually from a sliver face after a boolean | coarsen or refine `CharacteristicLengthMax`; or use a `Part::Box` proxy (§9.9) |
| gmsh fails on an Arch object | many `Subtractions`, compound/multi-solid geometry | mesh a `Part::Box` proxy and state the simplification |
| Stress 1000× expected | pressure or force assigned as a bare float | assign unit strings (§0.3) |
| Result looks right but is on the wrong axis | `Reversed` not set, or wrong `Direction` | check the face normal; `Reversed=True` on a +Z top face gives a downward load |
| Deflection ~2× hand-check | `ElementOrder = "1st"` — first-order tets are far too stiff/inaccurate in bending | set `"2nd"` |
| Solver times out | mesh too fine, or whole building meshed | analyse one member; coarsen mesh; raise `timeout` only after coarsening |
| Second run returns first run's numbers | reading a stale `CCX_Results` object | delete old result objects, or read the highest-numbered one |
| `get_rpc_status` reports `stuck` | GUI thread blocked by a prior long op | restart FreeCAD; do not queue more calls |

```python
# clean result objects between runs
for o in list(doc.Objects):
    if o.Name.startswith("CCX_Results") or o.Name.startswith("ResultMesh"):
        doc.removeObject(o.Name)
doc.recompute()
```

### 9.9 When to use a `Part::Box` proxy instead of the Arch object

Gmsh meshes Arch objects directly **[verified]**, so prefer that — the BIM object and the analysed object are then the same object, and can't drift apart. Fall back to a `Part::Box` proxy when:

- the member carries many `Subtractions` (openings, sleeves) and gmsh fails or produces a degenerate mesh;
- the member is a compound / multi-solid;
- you want a deliberately simplified, conservative gross section.

If you use a proxy, **say so in the reply** and state the simplification (e.g. *"checked as a 300×450 gross rectangle; the two Ø100 service penetrations at midspan were not modelled"*). A proxy that quietly differs from the BIM object is the FEM equivalent of a stale result.

### 9.10 Which members are worth solving

You will not FEM-check every member of a house, and you should not pretend to. Prioritise:

```
1. The longest-span beam or slab              (deflection/stress governs)
2. Any cantilever (balcony, chajja, stair)    (unforgiving, high moment at support)
3. The most heavily loaded column             (from the §8.4 take-down)
4. Any transfer element                       (a column landing on a beam)
5. Anything the user specifically asked about
```

Everything else stays explicitly in the **"NOT verified by FEM"** list in §11.3. Five unverified members honestly listed is a better deliverable than six members implied to be checked.

**Mesh size on thin cantilevers can hang the GUI thread indefinitely, with no clean cancel** [verified]: an unconstrained/too-fine `CharacteristicLengthMax` on a large, thin cantilevered member (a chajja proxy, large-face-area-to-thickness ratio) generated a mesh in the hundreds of thousands of nodes. The solve then held the GUI dispatch thread past its own stated timeout (confirmed via `mcp__freecad__get_rpc_status` showing `state: "stuck"` climbing past 1000+ seconds with no sign of returning), and eventually crashed the FreeCAD process entirely — losing every unsaved change in the document until a restart. **Always generate the mesh yourself first (`GmshTools(msh).create_mesh()`) and check `msh.FemMesh.NodeCount` is in the low-thousands-to-tens-of-thousands range *before* calling `run_fem_analysis`** — never let an uncapped `CharacteristicLengthMax` on a thin/large-area member go straight to the solver. If `get_rpc_status` ever reports `state: "stuck"` on a `run_fem_analysis` task, do not queue further calls against that document — the task cannot be safely cancelled, and even `doc.save()` will fail with the same "GUI dispatch unavailable" error until the process is restarted (at which point FreeCAD's own crash-recovery may preserve unsaved work — verify object counts before assuming anything was lost, don't assume the worst without checking).

**`Arch.makeRebar`'s default `OffsetStart`/`OffsetEnd` (30mm) plus the bar's own diameter can make a correct cage fail a naive bbox-containment check** [verified]: placing a rebar wire's endpoints exactly at a host's bounding-box limits does not guarantee the resulting bar geometry stays inside that bbox. Two independent effects stack: (1) `Arch.makeRebar` defaults `OffsetStart`/`OffsetEnd` to 30mm, extending the bar 30mm past each wire endpoint unless explicitly zeroed — this is too short to be a real lap/anchorage length, so treat it as a cosmetic default to zero out, not a design feature, unless you are deliberately modeling a lap splice; (2) even after zeroing both offsets, a **closed stirrup bar drawn flush with a member's end** will still poke past the theoretical zero-thickness endpoint by half the bar diameter (e.g. 4mm for an 8mm bar) — this is correct, expected geometry, not a defect. **A bbox-containment check must use a tolerance of `bar_diameter/2 + small_margin`, not a flat few-mm fudge factor**, or correctly-detailed end stirrups will read as false "outside host" failures.

**A `Door`/`Window` object's `Base` sketch `Placement` has ZERO effect on the built shape — only the object's own `Placement` does** [verified]: an ArchWindow/Door built via a preset does not derive its 3D shape by transforming the linked `Base` sketch through that sketch's own `Placement`. Rotating or repositioning `door.Base.Placement` and recomputing produces an identical `Shape.BoundBox` every time — the sketch's transform is silently ignored by the proxy's shape-building code. The object's *own* `Placement` property is what actually moves/rotates the built shape. If a door/window was ever fixed for a crash by reverting `Normal` to its default `(0,0,-1)` (see the Null-Shape gotcha above), re-verify with `Shape.BoundBox` afterward — that default builds the leaf lying flat (as if it were a skylight facing down), not standing upright in a vertical wall opening, and "shape is not null" is not the same as "shape is geometrically sane." To stand a flat-built door upright: reset `Placement` to identity, read the raw `Shape.BoundBox` at identity, determine which local horizontal axis (X or Y) carries the `Height` property value (compare span to `Height` within a few mm) — if it's X, apply `Rotation(Vector(0,1,0), -90)`; if it's Y, apply `Rotation(Vector(1,0,0), +90)` — then translate by matching the rotated shape's per-axis center to the corresponding `Void_*` object's BoundBox center. Verify the final `Shape.BoundBox` falls inside the void's BoundBox (with a small tolerance) before considering the door fixed — do not batch-apply a "best-guess" rotation chosen by matching sorted span magnitudes alone, since that can't disambiguate between the two valid rotation axes and will silently misplace doors that happen to have similar-sized spans (confirmed: this produced 10/12 wrong results in one batch attempt, including re-breaking an already-verified door).

## 10. Stairs — comfort formula is not enough; IRC 2021 gates are

The Part-1 guidance (riser 140–180 mm, tread 270–340 mm, `2R + T ≈ 600–650 mm`, from BIMExample.FCStd) is a good *comfort* envelope and stays. It is **not** a code check, and a stair can pass it and still fail code.

### 10.1 IRC 2021 §R311.7 hard limits

| Rule | Limit | Section |
|---|---|---|
| Max riser height | **196 mm (7¾ in)** | R311.7.5.1 |
| Min tread depth, **with** nosing | **254 mm (10 in)** | R311.7.5.2 |
| Min tread depth, **without** nosing | **279 mm (11 in)** | R311.7.5.2 |
| Max variation riser-to-riser / tread-to-tread within one flight | **9.5 mm (⅜ in)** | R311.7.5 |
| Nosing projection (solid risers) | **19–32 mm (¾–1¼ in)** per IRC R311.7.5.3; some summaries cite 25–38 mm (1–1½ in) — **verify against your adopted edition** | R311.7.5.3 |
| Min headroom, vertical from nosing line / landing | **2032 mm (6 ft 8 in)** | R311.7.2 |
| Min clear width above handrail height | **914 mm (36 in)** | R311.7.1 |
| Min clear width below handrail, one handrail | 800 mm (31½ in) | R311.7.1 |
| Min clear width below handrail, two handrails | 686 mm (27 in) | R311.7.1 |
| Handrail height above nosing | **864–965 mm (34–38 in)** | R311.7.8 |
| Max handrail projection into required width | 114 mm (4½ in) | R311.7.8 |
| Min clearance, wall to handrail | 38 mm (1½ in) | R311.7.8 |
| Max vertical rise between landings | 3835 mm (12 ft 7 in) | R311.7.3 *[unverified]* |
| Landing length in direction of travel | ≥ **914 mm (36 in)** | R311.7.6 *[unverified]* |
| Winder tread, min depth at narrow end | 152 mm (6 in) | R311.7.5.2.1 *[unverified]* |
| Winder tread, min depth 305 mm from narrow end | 254 mm (10 in) | R311.7.5.2.1 *[unverified]* |
| Spiral: min clear width / min tread at 305 mm / max riser / headroom | 660 mm / 190 mm / 241 mm / 1982 mm | R311.7.10.1 *[unverified]* |
| Guard height at open sides / landings | 914 mm (36 in) | R312.1.2 *[unverified]* |
| Guard opening limit | no 102 mm (4 in) sphere passes | R312.1.3 *[unverified]* |

**Pakistani residential practice** *[practice, unverified]* commonly runs riser 165–190 mm, tread 250–280 mm — i.e. **routinely tighter than the IRC tread minimum**. If designing to local practice rather than IRC, say which standard the stair was checked against; do not report an IRC PASS for a stair that was sized to practice.

### 10.2 Flight geometry arithmetic

```
NumberOfSteps  N        (risers)
RiserHeight    R = floor_to_floor_height / N
TreadDepth     T = going_length / (N - 1)        [verified: FreeCAD's own derivation]
Total going    G = T * (N - 1)
Stair angle    theta = atan(R / T)               comfortable 30-35 deg; IRC-legal up to ~37 deg
Headroom       measured vertically from the nosing line to the soffit above
```

To hit a target tread with a fixed floor-to-floor height:

```
N = ceil(H / R_max)  with R_max = 196 mm   ->  minimum riser count that keeps risers legal
G = T_target * (N - 1)                      ->  the going length the plan must accommodate
```

For H = 3000 mm: `N = ceil(3000/196) = 16 risers` → `R = 187.5 mm`; at T = 280 mm → `G = 280 × 15 = 4200 mm`. If the plan only offers 3600 mm of going, the stair **cannot** be a single straight legal flight — it needs a landing/dog-leg, or the code check fails. Say that, rather than silently shrinking the tread.

### 10.3 How FreeCAD's stair defaults violate this [verified]

`Arch.makeStairs` derives its proportions and **defaults `Nosing = 0.0 mm`**:

```
RiserHeight = Height / NumberOfSteps
TreadDepth  = Length / (NumberOfSteps - 1)     [verified]
```

Run `Arch.makeStairs(length=4200, width=1100, height=3000, steps=17)`:

```
NumberOfSteps = 17     RiserHeight = 176.47 mm     TreadDepth = 262.5 mm     Nosing = 0.0 mm
```

- Comfort formula: `2(176.47) + 262.5 = 615.4 mm` → **inside 600–650, "passes"**.
- IRC riser: 176.47 ≤ 196 → **PASS**.
- IRC tread: nosing is 0, so the **279 mm** limit applies. 262.5 < 279 → **FAIL**.

A stair that passes the comfort check and fails the code is exactly the failure this section exists to prevent. **Fix:** set `Nosing = 25` (then the 254 mm limit applies, 262.5 ✓), or lengthen the flight — to hit a 280 mm tread with 17 steps, `Length = 280 × 16 = 4480 mm`.

### 10.4 Assertion script — run after every `makeStairs`

```python
def check_stair_irc(st, headroom_mm=None, n_handrails=0, landing_len_mm=None):
    R = st.RiserHeight.getValueAs("mm").Value
    T = st.TreadDepth.getValueAs("mm").Value
    N = st.Nosing.getValueAs("mm").Value
    W = st.Width.getValueAs("mm").Value
    H = st.Height.getValueAs("mm").Value
    t_min = 254.0 if N > 0 else 279.0
    checks = [
        ("riser <= 196 mm (R311.7.5.1)",          R <= 196.0,              f"{R:.1f}"),
        (f"tread >= {t_min:.0f} mm (R311.7.5.2)", T >= t_min,              f"{T:.1f} (nosing={N:.0f})"),
        ("width >= 914 mm (R311.7.1)",            W >= 914.0,              f"{W:.0f}"),
        ("rise between landings <= 3835 mm (R311.7.3)", H <= 3835.0,       f"{H:.0f}"),
        ("comfort 2R+T in 600-650",               600 <= 2*R+T <= 650,     f"{2*R+T:.1f}"),
        ("angle 30-37 deg",       30 <= math.degrees(math.atan(R/T)) <= 37,
                                  f"{math.degrees(math.atan(R/T)):.1f} deg"),
        ("total rise matches",
             abs(st.NumberOfSteps*R - H) < 1.0, ""),
    ]
    if N > 0:
        checks.append(("nosing 19-32 mm (R311.7.5.3)", 19.0 <= N <= 32.0, f"{N:.0f}"))
    checks.append(("headroom >= 2032 mm (R311.7.2)",
                   (headroom_mm >= 2032.0) if headroom_mm is not None else None,
                   f"{headroom_mm:.0f}" if headroom_mm is not None
                   else "NOT MEASURED - must check against slab/soffit above"))
    checks.append(("landing >= 914 mm (R311.7.6)",
                   (landing_len_mm >= 914.0) if landing_len_mm is not None else None,
                   f"{landing_len_mm:.0f}" if landing_len_mm is not None else "NO LANDING MODELLED"))
    checks.append(("handrail present (R311.7.8)",
                   n_handrails >= 1, f"{n_handrails} modelled"))
    for name, ok, val in checks:
        tag = 'PASS' if ok else ('----' if ok is None else 'FAIL')
        print(f"  [{tag}] {name}  {val}")
    unresolved = [c[0] for c in checks if c[1] is None]
    if unresolved:
        print(f"  UNRESOLVED (must be stated in the reply): {', '.join(unresolved)}")
    return all(c[1] for c in checks if c[1] is not None), unresolved
```

### 10.5 Headroom — the check that cannot come from the stair object

Headroom depends on the slab/soffit above, not on the stair. Measure it in the model:

```python
# Vertical clearance from each nosing to the first solid above it.
def measure_headroom(stair, obstructions, samples=None):
    """obstructions: list of solids above (slabs, landings, beams). Returns min clearance mm."""
    import Part
    R = stair.RiserHeight.getValueAs("mm").Value
    T = stair.TreadDepth.getValueAs("mm").Value
    base = stair.Placement.Base
    n = int(stair.NumberOfSteps)
    worst = float("inf")
    for i in range(n):
        p = App.Vector(base.x + i*T, base.y + stair.Width.Value/2, base.z + (i+1)*R)
        ray = Part.makeLine(p, App.Vector(p.x, p.y, p.z + 6000))
        for ob in obstructions:
            sec = ob.Shape.common(ray)
            for v in sec.Vertexes:
                worst = min(worst, v.Point.z - p.z)
    print(f"  min headroom = {worst:.0f} mm -> {'PASS' if worst >= 2032 else 'FAIL'} (R311.7.2)")
    return worst
```

*[unverified — the raycast pattern is standard OCC usage but has not been run through this MCP connection.]* If you do not run it, the headroom line in the §11.3 block must read **NOT MEASURED**, not "assumed OK".

### 10.6 The stair as a structural member

An RC stair flight is a **cantilever or inclined slab carrying 40 psf live load plus its own considerable dead weight**, and is one of the most commonly under-designed elements in a house. Waist slab thickness typically 125–175 mm *[practice]*.

- If the stair is presented as structurally viable, it needs the same §9 treatment as a beam — usually idealised as an inclined one-way slab spanning between landings.
- `Arch.makeStairs` geometry is generally not directly meshable for a clean check; use a `Part::Box` proxy of the waist slab at the developed span and state the simplification.
- Handrails are usually **not modelled** by `makeStairs` at all. If a stair is presented without handrails, say so — R311.7.8 requires them, and their absence is a code failure, not a rendering choice.
- Stair reinforcement detailing (main bars in the waist, distribution steel, the critical bar geometry at the landing/flight junction where a wrongly-bent bar pushes concrete out) is in `architecture-concrete-reinforcement-detailing` §10.

## 11. Honesty protocol — no unverified structural claims

The Part-1 disciplines were "verify by volume diff" and "verify by IFC export". Part 2 adds the one that matters most, because its failure mode is not a broken model but a **false statement about a real building**.

### 11.1 The rule

> **Any element presented as structurally adequate must carry solver output. Any element without it must be flagged as unverified, in the reply, unprompted.**

Three corollaries:

1. **Absence of a check is information the user needs**, and it degrades — the longer a model is discussed without the flag being repeated, the more the user assumes it was checked. Re-state it on every substantive reply about the model, not only the first.
2. **A passing FEM run is not a passing design.** The correct sentence names the criterion, the load case, and the margin — never the word "safe".
3. **Silence is a claim.** Presenting a model with columns and footings and saying nothing about verification asserts, by omission, that they are fine.

### 11.2 Vocabulary — say the accurate one

| Never say | Say instead |
|---|---|
| "the beam is fine / safe / adequate" | "FEM: σ_vm 3.19 MPa vs f_r 3.40 MPa — uncracked with 6% margin under the stated load; not an RC design check" |
| "the footing is sized correctly" | "sized for an **assumed** 150 kPa bearing; requires geotech confirmation and a punching-shear check" |
| "structural model complete" | "geometry complete; FEM run on 1 of 6 members; 5 unverified" |
| "code-compliant stair" | "passes IRC riser/tread/width; headroom **not measured**; handrails not modelled" |
| "the column is adequate" | "axial stress X MPa under the §8.4 take-down; buckling hand-checked only (kL/r = 33); no lateral case run" |
| "rebar is designed" | "cage modelled and checked against ACI minimum steel; development lengths, laps and hooks not detailed" |
| "the model is verified" | "geometry verified by volume diff and IFC export; structure verified only where listed below" |
| "this is ready to build" | never — see the Reality Check section |

### 11.3 The mandatory status block

When presenting any model containing structural elements, include this block. **Do not omit it because the user did not ask.**

```
STRUCTURAL VERIFICATION STATUS
  Verified by FEM (CalculiX):   <member: sigma_vm, delta, load case, criterion compared,
                                 mesh + convergence Δ, hand-check Δ>
  NOT verified by FEM:          <list every other structural member>
  Hand-checked only:            <member: what formula, what result>
  Assumed inputs:               <soil bearing, f'c, E, load values, boundary idealization,
                                 which combination>
  Simplifications:              <proxy solids used, penetrations omitted, single-span
                                 idealizations>
  Not modelled at all:          <plinth beams, lintels, handrails, hooks/laps, ...>
  Not checked at all:           punching shear, one-way shear, wind, torsion,
                                buckling, connections, long-term deflection, cracking,
                                foundation settlement, construction-stage loading
  Lateral / seismic:            NOT evaluated in this skill — architecture-seismic-design
                                <invoked: yes/no; if no, say so explicitly, don't bury it
                                 in the generic "not checked" list above — Pakistan is a
                                 seismic country and this is a real coverage gap, not a formality>
  Cross-check vs preliminary sizing: <architecture-structural-systems consulted for this
                                member? agree within ~15-20%? if not run, say so>
  => NOT construction-ready. Requires a licensed (PEC-registered) structural engineer
     and local authority (LDA/CDA/TMA) approval.
```

If **zero** members have been through the solver, lead with a single line —
**"FEM NOT RUN — no member in this model has been structurally verified."**
— before describing the model at all.

### 11.4 What silently invalidates a previously-run FEM

Re-run, or downgrade the claim to unverified, whenever **any** of these change:

- member dimensions (length, width, depth)
- `Subtractions` added or removed (a new penetration, a new opening)
- material properties (f'c, E, ν, density)
- load values, tributary width, or load combination
- boundary conditions or face bindings (including face **re-indexing** after a boolean)
- span, support locations, or the addition/removal of an intermediate support
- mesh density or element order
- the proxy solid drifting from the BIM object it stands in for

**A stale FEM result attached to an edited member is worse than no result, because it looks like evidence.**

### 11.5 Machine-enforce the ledger — don't rely on memory

Stamp verification state onto the object itself so it survives context loss and is auditable:

```python
def stamp_fem(obj, sigma_mpa, delta_mm, load_case, criterion, nodes, hand_delta_pct):
    if not hasattr(obj, "FEMStatus"):
        obj.addProperty("App::PropertyString", "FEMStatus", "Verification",
                        "FEM verification record")
        obj.addProperty("App::PropertyString", "FEMStamp", "Verification",
                        "Geometry fingerprint at time of FEM run")
    obj.FEMStatus = (f"VERIFIED sigma={sigma_mpa:.3f}MPa delta={delta_mm:.3f}mm "
                     f"case={load_case} vs {criterion} nodes={nodes} hand_delta={hand_delta_pct:.1f}%")
    obj.FEMStamp = geom_fingerprint(obj)

def geom_fingerprint(obj):
    s = obj.Shape
    return f"{s.Volume:.3f}|{len(s.Faces)}|{len(obj.Subtractions) if hasattr(obj,'Subtractions') else 0}"

def fem_ledger(doc):
    """Print the §11.3 block's first two lines straight from the model. Run before every handoff."""
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

Run `fem_ledger(doc)` **immediately before writing any reply that describes the model.** Copy its output into the §11.3 block rather than reconstructing it from memory — reconstruction is where an unverified member quietly becomes a verified one.

### 11.6 Worked example — a bad reply and a good one

**Bad** (every sentence is defensible in isolation; the whole is a false impression):

> Here's your G+1 house model. The structure uses 300×300 columns on 1500×1500 pad footings with a 150 mm slab, and the FEM analysis came back at 3.19 MPa, well within limits. The stair is code-compliant at 176 mm risers. Ready for your contractor.

**Good:**

> **Not construction-ready** — this is a modelling and screening exercise and needs a PEC-registered structural engineer plus LDA approval before anyone builds from it.
>
> Model: G+1, Site→Building→5 storeys (incl. Foundation at −1200), 41 walls with parametric openings (all cuts volume-verified), IFC export confirms IFCFOOTING/IFCWINDOW/IFCREINFORCINGBAR.
>
> ```
> STRUCTURAL VERIFICATION STATUS
>   Verified by FEM:  Beam B1 (3.0 m) — sigma_vm 3.193 MPa vs f_r 3.40 MPa (f'c 30),
>                     delta 1.09 mm vs L/360 = 8.3 mm, case 1.2D+1.6L per §8.3,
>                     2713 nodes 2nd-order, hand-check Δ 0.2% stress / 2.3% deflection.
>                     Modelled as a CANTILEVER (conservative); real condition is
>                     partially restrained. Mesh convergence NOT yet re-run.
>   NOT verified:     Columns C1–C6, footings F1–F6, slabs S1–S2, stair flight
>   Hand-checked:     C1 slenderness kL/r = 33 (below ACI 34 threshold, braced frame)
>   Assumed:          soil 150 kPa (NO GEOTECH), f'c 30 MPa, E 30,000 MPa (ACI gives 25,743)
>   Not modelled:     plinth beams, lintels, handrails, rebar hooks/laps
>   Not checked:      punching shear, wind, buckling, cracking, settlement
>   Lateral/seismic:  NOT evaluated — architecture-seismic-design not invoked for this
>                     model; Pakistan is a seismic zone, this is a real gap
>   Cross-check:      preliminary sizing NOT cross-checked against
>                     architecture-structural-systems for this beam
> ```
>
> Stair: riser 176.5 mm ✓, tread 262.5 mm with 25 mm nosing ✓, width 1100 mm ✓ — but **headroom not measured** and **no handrail modelled** (IRC R311.7.8 requires one).
>
> Biggest open item: the footings are sized on an assumed bearing pressure. Get a geotech report before that number means anything.

## 12. Process checklist for the next building model

**Preflight (Part 0)**
1. `get_rpc_status` → `list_documents` → confirm FreeCAD 1.0.x on a real DISPLAY. Set `include_screenshot=False` for all analytical calls.

**Geometry (Part 1)**
2. Build Site → Building → Storey hierarchy with real elevations FIRST, including a **Foundation** storey at negative elevation if footings exist, and a Plinth storey if there are plinth beams.
3. Build walls from `Draft.makeLine` + `Arch.makeWall`.
4. For every opening: hidden void extrusion → `wall.Subtractions` → **verify by volume diff**. Model a lintel over every opening in a load-bearing wall.
5. Create the matching `Arch.makeWindow`/Door BIM object at the same placement, `IfcType` set correctly.
6. For repeated facade patterns, array/clone one void + one window rather than N independent cuts.
7. Verify BIM classification via real IFC export + grep, not the property value.

**Structure (Part 2)**
8. Model footings with `Arch.makeStructure` + `IfcType="Footing"`; pick the type from the §6.2 tree; size per §6.3–§6.4 **including footing self-weight**; model the PCC layer; record the **assumed** bearing pressure explicitly. Add plinth beams (§6.7) or list them as not modelled.
9. Model reinforcement with `Arch.makeRebar` (attached sketch, `offset` = real cover per §6.5, `Mark` set, `Rounding` non-zero); run `check_min_steel` and `check_max_spacing` on every cage (§7.3); run `check_column_rebar` on every column (§7.4); finish with `audit_all_rebar(doc)`.
10. Build the **full §8.4 roof-to-soil take-down table** once, and derive every load from it. Never invent a force. Pick the right combination for stress vs deflection (§8.2), and the right constraint type (§8.5). Cross-check the sized members against `architecture-structural-systems`' preliminary tables (§8, opening paragraph); flag any disagreement over ~15–20% rather than silently picking one number. If the building is in a seismic zone, confirm `architecture-seismic-design` has actually been invoked for lateral/seismic — don't just cite its name.
11. For each member being claimed adequate (prioritise per §9.10): verify face indices (§9.2) → assemble the analysis (§9.3) → `run_fem_analysis` → **hand-check within ~10%** (§9.4) → mesh-convergence re-run at half the characteristic length → compare to the **correct material criterion**, not von Mises-vs-concrete (§9.6). Choose and state the boundary idealization (§9.7). Euler/slenderness hand-check every column.
12. Size stairs against **both** the comfort envelope and the IRC 2021 gates; run `check_stair_irc`; set `Nosing` explicitly (defaults to 0 and silently raises the tread minimum to 279 mm); measure or explicitly disclaim headroom; state whether handrails are modelled.
13. Run `fem_ledger(doc)` and emit the §11.3 STRUCTURAL VERIFICATION STATUS block **from its output**. If nothing was solved, lead with **"FEM NOT RUN"**. If the user's language implies they think it is buildable, lead with the Reality Check.
14. Skip material/Pset assignment and elaborate TechDraw dimensioning unless specifically requested — **but never skip real dimensions, grades or steel on structural members** (§5 exception).

## 13. Standards index & scope boundaries

**Cite these explicitly in outputs; never present one code's number as another's.**

| Standard | Used here for |
|---|---|
| **ACI 318-19** | §13.3.1.2 min foundation effective depth; cover (earth-cast 75 mm / formed 50 mm); min flexural & shrinkage-temp steel 0.0018 / 0.0020; Table 24.2.2 one-way slab min thickness and deflection limits; §10.6.1.1 column ρ_g 1–8%; §25.7.2 tie size and spacing; §19.2.2.1 `E_c = 4700√f'c`; §6.2.5 slenderness thresholds |
| **ASCE 7-22** | Table 4.3-1 live loads (40 psf residential); §4.7.2 live load reduction; roof live reduction to 12 psf; §2.3.1 strength load combinations |
| **IRC 2021** | §R311.7 stairs — riser 7¾ in, tread 10/11 in, ⅜ in uniformity, nosing, R311.7.2 headroom 6 ft 8 in, R311.7.8 handrails, R311.7.1 widths, R311.7.6 landings; footing width/thickness minimums |
| **BCP-2007 / BCP-2021 (PEC)** | Named as the locally applicable Pakistan code. **No numeric clause is quoted from it in this skill** — obtain from pec.org.pk and reconcile before citing |
| **FreeCAD FEM / CalculiX ccx / gmsh** | The solver pipeline itself |

**Which skill owns what** — defer rather than duplicate:

| Topic | Owner skill |
|---|---|
| Soil investigation, SBC, settlement, retaining walls, waterproofing | `architecture-geotechnical-foundations` |
| Development length, laps, hooks, curtailment, BBS, seismic detailing | `architecture-concrete-reinforcement-detailing` |
| System choice, preliminary member sizing tables, load path narrative, wind/seismic basics | `architecture-structural-systems` |
| Seismic zoning, base shear, confined masonry, wall density, irregularities | `architecture-seismic-design` |
| Room sizes, circulation, plan layout | `architecture-spatial-planning` |
| Byelaws, setbacks, plan approval, PEC stamping workflow | `architecture-building-codes-permits` |
| Accessible stairs/ramps beyond IRC minimums | `architecture-accessibility-design` |
| Quantities, rates, BOQ, contractor quote checking | `architecture-cost-estimation-boq` |
| Service penetrations through structure | `architecture-mep-coordination` |
| 2D drawings / floor plans as editable files | `drawio-diagrams` |
| **This skill** | **Making all of the above real, parametric and solver-checked inside FreeCAD, and refusing to overstate the result** |

## 14. Known gaps in this skill — state these when relevant

1. **BCP numeric clauses are absent.** Everything numeric is ACI/ASCE/IRC. For a Pakistani project this is a real gap, not a formality.
2. **Stirrup/tie rebar via closed sketch is [unverified]** — the pattern follows from verified straight-bar behaviour but has not been round-tripped through this MCP connection. Verify before relying on a modelled cage's tie geometry.
3. **`ConstraintDisplacement` property names are [unverified]** — the recommended fix for the simply-supported idealization (§9.7) has not been executed here.
4. **No mesh-convergence run has actually been completed** — the §9.6 protocol is correct but the second data point was never taken on the validated beam. Any current claim about that beam is single-mesh.
5. **The headroom raycast (§10.5) is [unverified].**
6. **No two-way slab, raft, pile or lateral-load workflow exists here at all** — those are engineer-only in this skill's current state.
7. **No IFC round-trip validation beyond grep** — entity presence is confirmed, but property sets, geometry fidelity and structural relationships in the exported file are unchecked.
8. **Lateral/seismic is a named gap, not a solved handoff.** This skill repeatedly points to `architecture-seismic-design`, but nothing here confirms that skill actually exists, has run, or agrees with the gravity-only sizing done here — for a real Pakistani house that gap must be closed by actually invoking it, not by citing it in a table.
9. **The §8 load path is not shown reconciled against `architecture-structural-systems`.** Both skills can independently size the same member; this file's internal load-path arithmetic (§8.3–§8.4) has not been demonstrated to match that skill's preliminary member-sizing tables on a real worked example — treat any disagreement as something to resolve, not to average away.

---

Related: [[project-farmhouse-2kanal]] (the model this lesson came from), [[project-freecad-mcp-setup]] (how the live connection is set up), [[feedback-architecture-skills]] (the dimensional-standards skills this pairs with), [[feedback-freecad-bim-deep-skill]] (the BIMExample.FCStd study).
