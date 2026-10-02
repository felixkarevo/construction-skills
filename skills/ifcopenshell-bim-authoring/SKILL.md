---
name: ifcopenshell-bim-authoring
description: >
  Native IFC authoring without a CAD host: build discipline models (ARC, TWP, HLS, ELT)
  directly as IFC files with IfcOpenShell's Python API (`ifcopenshell.api.*`) — headless
  in a script, or driven by an LLM agent through the `ifcmcp` MCP server. Covers install
  and versions (IfcOpenShell 0.9.x), the IFC object model an author must get right
  (units, representation contexts, spatial tree, placements, types, material layer sets,
  Psets/Qtos, voids and fillings, distribution systems and ports), verified recipes for
  walls/openings/windows/slabs/pipes, the federation discipline (one IFC per discipline,
  shared coordinates, why not to merge), verification by geometry (volume/bbox via
  `ifcopenshell.geom`), `ifcopenshell.validate`, `ifctester` and `ifcpatch`, viewer
  choices for inspection, and the authoring gotchas that silently produce wrong files
  (e.g. `create_2pt_wall` does not assign its representation). Use when the user wants
  IFC files as the primary deliverable, wants to model without FreeCAD, mentions
  IfcOpenShell, ifcopenshell.api, ifcmcp, Bonsai/BlenderBIM scripting, or per-discipline
  IFC files; use `construction-freecad-bim` instead when the model lives in FreeCAD.
---

# IfcOpenShell BIM Authoring — Native IFC, Script- or MCP-Driven

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> only when the client **explicitly** asks for it, with cost/schedule impact stated;
> deviate **below** the usual standard or the aarRdT only via the documented
> risk-acceptance machinery (`simple-first-building` §3).

This skill is the **sibling of `construction-freecad-bim`**. Both produce BIM models; they
differ in where the model lives:

| | `construction-freecad-bim` | this skill |
|---|---|---|
| Source of truth | FreeCAD document (`.FCStd`), IFC is an export | the `.ifc` file itself — no export step, nothing lost in translation |
| Driver | live FreeCAD GUI via neka-nat/freecad-mcp | Python script (`ifcopenshell.api`) or the `ifcmcp` MCP server, headless |
| Strengths | parametric Arch objects, rebar, CalculiX FEM in the same session | exact IFC semantics (entity, `PredefinedType`, Psets, systems), per-discipline files, CI-friendly, no GUI hangs |
| Weak at | Pset/type fidelity on export, large models, discipline split | interactive look-and-feel (you need a separate viewer), FEM (hand off) |

Both feed the same downstream chain: `ifc-model-validation` proves the file,
`bim-management` owns the process (LOIN, naming, CDE, BCF).

**Markers:** **[verified 0.9.0]** = executed in this skill's test run against
`ifcopenshell 0.9.0` (PyPI, Python 3.12), with the printed result shown — evidence.
**[docs]** = taken from docs.ifcopenshell.org or the IfcOpenShell source, not re-run here.
**`VERIFY`** = version-, release- or availability-sensitive; check before relying on it.

## Reality Check — what this skill's output is

- An IFC file written by this workflow is a **coordination and information model**, not
  an engineering design. Wall thicknesses, slab depths and pipe diameters come from the
  owning skills (`structural-analysis`, `masonry-construction`, `building-services-tga`,
  `building-physics-thermal-moisture`, …) — never invent them in a modeling recipe.
- **A schema-valid file is not a correct building.** §5 shows a wall with no geometry at
  all passing `ifcopenshell.validate` with zero errors. Validity, information
  completeness (IDS) and design correctness are three separate claims; state which one
  you checked.
- A property value such as `FireRating = "REI 90"` is a **claim written into the file**,
  not a fire-resistance proof. It must be traceable to `fire-protection-building` and,
  for a real project, to the signed fire-safety concept.
- Nothing produced here is construction-ready. A licensed architect/engineer signs off;
  site data (Baugrundgutachten, current B-Plan, current GEG/DIN edition) overrides
  generic values. Say so unprompted when the user's language treats a model as final.

## 1. Setup

### 1.1 Library [verified 0.9.0]

```bash
python -m venv .venv && . .venv/bin/activate      # or: uv venv && uv pip install ...
pip install ifcopenshell          # 0.9.0 (PyPI, 2026-09-29) — VERIFY current; Python >=3.10
pip install ifctester ifcpatch ifcdiff ifc5d      # separate PyPI packages, same version line
pip install pytest                # needed only for `validate --rules` (see G-07)
```

`IfcConvert` (IFC → glb/obj/svg/stp/xeokit json) is **not** in the pip wheel; it ships
with the conda package (`conda install -c conda-forge ifcopenshell`) or as a standalone
download [docs: docs.ifcopenshell.org/ifcconvert.html].

`ifcopenshell.version` prints the installed version. Supported schemas for
`project.create_file(version=...)`: `"IFC2X3"`, `"IFC4"` (default), `"IFC4X3"`.
**Default to IFC4** for buildings (`bim-management` §8 for the version decision); IFC2X3
only if a receiving tool demands it, IFC4X3 for infrastructure/alignment work.

API modules shipped in 0.9.0 [verified 0.9.0]: `aggregate alignment attribute boundary
classification cogo constraint context control cost document drawing feature geometry
georeference grid group layer library material nest owner profile project pset
pset_template resource root sequence spatial structural style system type unit`.

### 1.2 The `ifcmcp` MCP server — `VERIFY` status

`ifcmcp` is the IfcOpenShell project's own MCP server (source `src/ifcmcp`, LGPL-3.0+).
It wraps the `ifcquery` (read) and `ifcedit` (write) command-line tools and keeps one
model loaded in memory across tool calls; nothing is written until `ifc_save`.

**Install name trap:** the docs page says `pip install 'ifcmcp[mcp]'`, but no `ifcmcp`
package exists on PyPI. The released package is **`ifcopenshell-mcp`** (0.9.0)
[verified 0.9.0]:

```bash
pip install 'ifcopenshell-mcp[mcp]'      # installs console scripts: ifcmcp, ifcquery, ifcedit
claude mcp add --transport stdio ifc -- ifcmcp          # Claude Code
```

Generic MCP client config (`.mcp.json` or equivalent):

```json
{ "mcpServers": { "ifc": { "type": "stdio", "command": "ifcmcp" } } }
```

Use the absolute path to the venv's `ifcmcp` if the client does not inherit the venv.
The `mcp` extra is pinned `<2` (mcp 2.0 renamed FastMCP) [docs/source].

Community alternative with a GUI: **Bonsai MCP** (`JotaDeRodriguez/Bonsai_mcp`, fork of
BlenderMCP) drives Blender + Bonsai over a socket, so the model updates visibly while
the agent works. Smaller project, not maintained by IfcOpenShell — `VERIFY` activity.

**Agent rule:** whichever bridge, the API semantics in §2–§4 are the same — `ifcedit`
and the Bonsai tools call `ifcopenshell.api` underneath. Learn the API, then use the
bridge as the transport.

### 1.3 A viewer for inspection

The agent writes files; a human must look at them. Recommended:

- **Bonsai** (Blender add-on, IfcOpenShell team) — native IFC, loads several discipline
  files side by side, spreadsheet/Pset inspection, clash, IDS, BCF. Largest open-source
  BIM community (OSArch).
- **Bonsai Viewer** — standalone C++/Qt6/WebGPU viewer from IfcOpenShell, early builds
  since 2026 — `VERIFY` maturity before recommending it as the main tool.
- Browser: **That Open Engine** (MIT, web-ifc MPL-2.0) or **xeokit** (AGPL-3.0) when
  building your own web viewer.
- FreeCAD (NativeIFC) opens the files too — convenient if it is already installed.

## 2. The IFC object model an author must get right

### 2.1 Use the API, not raw entity creation

`f.create_entity("IfcWall", ...)` / `f.createIfcWall(...)` writes a bare instance and
nothing else. `ifcopenshell.api.root.create_entity(f, ifc_class="IfcWall")` also creates
the `GlobalId`, owner history where the schema needs it (IFC2X3), and keeps the
relationship graph consistent. **Author with `ifcopenshell.api.*`; reserve
`f.create_entity` for geometry primitives the API has no function for.**

Call style: `ifcopenshell.api.root.create_entity(f, ifc_class="IfcWall")`. The older
`ifcopenshell.api.run("root.create_entity", f, ...)` still exists in 0.9.0 but its
docstring says it is **deprecated and will be removed** — don't write new code with it.
**Import every submodule you use** (G-01).

### 2.2 The minimum skeleton — nothing renders without it

Every authored file needs, in this order:

1. `IfcProject` (exactly one per file).
2. **Units** — `unit.assign_unit`. Pick one length unit for the project and stay in it
   (§2.6). `assign_unit(f)` with no arguments gives **millimetres** — a testing
   convenience per the docs, not a neutral default.
3. **Representation contexts** — a `Model` context and a `Body` sub-context
   (`target_view="MODEL_VIEW"`). Geometry assigned without a Body context is invisible
   to most viewers. Add `Axis` (`GRAPH_VIEW`) for wall/beam axes, `Plan` contexts only if
   you author 2D symbols.
4. **Spatial tree** — `IfcSite` → `IfcBuilding` → `IfcBuildingStorey` (→ `IfcSpace`)
   joined with `aggregate.assign_object`.
5. **Placements** on every spatial element (`geometry.edit_object_placement`), storey
   placement z = storey elevation, plus the `Elevation` attribute set to the same value.
6. Elements **contained** in exactly one storey (`spatial.assign_container`). Elements
   that span storeys (stair cores, façades) are contained in one and *referenced* in the
   others (`spatial.reference_structure`).

### 2.3 Aggregation vs containment vs reference

| Relationship | API | Use for |
|---|---|---|
| `IfcRelAggregates` | `aggregate.assign_object` | spatial decomposition (Site→Building→Storey→Space) and assemblies (element made of parts) |
| `IfcRelContainedInSpatialStructure` | `spatial.assign_container` | physical element lives on a storey — **one** container only |
| `IfcRelReferencedInSpatialStructure` | `spatial.reference_structure` | element also relevant to other storeys |
| `IfcRelVoidsElement` | `feature.add_feature` | opening cuts a wall/slab |
| `IfcRelFillsElement` | `feature.add_filling` | window/door sits in the opening |
| `IfcRelDefinesByType` | `type.assign_type` | occurrence ← type (shared material, Psets, geometry) |
| `IfcRelAssignsToGroup` (system) | `system.assign_system` | pipe/duct/cable belongs to a distribution system |

### 2.4 Placement

- `edit_object_placement(f, product=..., matrix=M)` takes a 4×4 matrix in **world
  coordinates and SI metres** (`is_si=True` default); the API stores an
  `IfcLocalPlacement` relative to the element's placement parent. [verified 0.9.0:
  window placed with `M[0,3]=2.0, M[2,3]=0.9` reads back `[2. 0. 0.9]` in world space via
  `ifcopenshell.util.placement.get_local_placement`; after `feature.add_filling` its
  `PlacementRelTo` is the **opening**, relative offset `(0,0,0)` — fillings are
  re-parented to their opening. Storey OG stores `z = 2.75` directly.]
- Rotation lives in the upper-left 3×3. For a wall from p1 to p2, x-axis = unit(p2−p1),
  y-axis = x rotated +90° — that is exactly what `create_2pt_wall` builds.
- Moving a storey later: `should_transform_children=True` keeps children in place in
  world space; the default moves them with the storey. Decide which you want.

### 2.5 Types, materials, properties, quantities

- **Types first.** Create `IfcWallType`/`IfcSlabType`/`IfcWindowType`…, assign the
  material set to the type, then `type.assign_type` each occurrence. Occurrences inherit
  material and type Psets — one edit to the type updates every instance (system-family
  thinking, same doctrine as `construction-freecad-bim` §2.6).
- **Layered walls/slabs:** `IfcMaterialLayerSet` on the type. After
  `type.assign_type` the occurrence gets an `IfcMaterialLayerSetUsage` automatically
  [verified 0.9.0: `ue.get_material(wall).is_a()` → `IfcMaterialLayerSetUsage`]. The
  geometric thickness of the wall must equal the sum of layer thicknesses — the API does
  not enforce this (G-05).
- **Psets:** `pset.add_pset` + `pset.edit_pset` with a dict. Use the standard
  `Pset_*Common` names and property names exactly (lookup: `bim-management` §8);
  project-specific data goes in a custom Pset with a project prefix, never invented
  `Pset_` names (reserved prefix).
- **Quantities:** compute them from geometry with `ifc5d` (§3.5) — it writes the
  standard `Qto_*BaseQuantities` sets. `pset.add_qto` + `pset.edit_qto` exist for
  manual sets; a hand-typed `GrossVolume` that disagrees with the shape is a silent
  defect. Custom quantity sets must **not** use the `Qto_` prefix [docs].

### 2.6 Units — pick metres or millimetres once

`unit.assign_unit(f, length={"is_metric": True, "raw": "METERS"})` → project in metres
[verified 0.9.0: `ifcopenshell.util.unit.calculate_unit_scale(f)` → `1.0`].
Millimetre projects (`"raw": "MILLIMETERS"`, scale `0.001`) are common in DACH exports
from Revit/ArchiCAD.

- API **geometry functions take SI metres by default** and convert to project units
  internally (`is_si=True` / unit-scale aware). Raw `f.create_entity` geometry is in
  **project units** — mixing the two is the 1000× error (G-04).
- IDS values are always SI (`ifc-model-validation` §4.6); Pset values are in project
  units unless the property type says otherwise.

## 3. Recipes [verified 0.9.0]

The script below builds a one-storey demo house (ARC file) and a heating stub (HLS file)
with identical spatial skeletons. Every printed result in this section came from running
it. Values (wall build-up, U-value, REI) are **demo placeholders**, not design values.

### 3.1 Shared skeleton (identical in every discipline file)

```python
import numpy as np
import ifcopenshell
import ifcopenshell.api.project, ifcopenshell.api.root, ifcopenshell.api.unit
import ifcopenshell.api.context, ifcopenshell.api.aggregate, ifcopenshell.api.spatial
import ifcopenshell.api.geometry, ifcopenshell.api.attribute, ifcopenshell.api.material
import ifcopenshell.api.type, ifcopenshell.api.pset, ifcopenshell.api.feature
import ifcopenshell.api.system
import ifcopenshell.api as api
from ifcopenshell.util.shape_builder import ShapeBuilder

STOREYS = [("EG", 0.00), ("OG", 2.75)]          # from building-planning-spatial

def skeleton(project_name):
    f = api.project.create_file(version="IFC4")
    project = api.root.create_entity(f, ifc_class="IfcProject", name=project_name)
    api.unit.assign_unit(f, length={"is_metric": True, "raw": "METERS"})
    model = api.context.add_context(f, context_type="Model")
    body = api.context.add_context(f, context_type="Model", context_identifier="Body",
                                   target_view="MODEL_VIEW", parent=model)
    site = api.root.create_entity(f, ifc_class="IfcSite", name="Grundstueck")
    bldg = api.root.create_entity(f, ifc_class="IfcBuilding", name="Haus A")
    api.aggregate.assign_object(f, relating_object=project, products=[site])
    api.aggregate.assign_object(f, relating_object=site, products=[bldg])
    api.geometry.edit_object_placement(f, product=site)
    api.geometry.edit_object_placement(f, product=bldg)
    storeys = {}
    for name, z in STOREYS:
        s = api.root.create_entity(f, ifc_class="IfcBuildingStorey", name=name)
        api.aggregate.assign_object(f, relating_object=bldg, products=[s])
        m = np.eye(4); m[2, 3] = z
        api.geometry.edit_object_placement(f, product=s, matrix=m)
        api.attribute.edit_attributes(f, product=s, attributes={"Elevation": z})
        storeys[name] = s
    return f, body, storeys
```

Same project name, same site/building/storey names and elevations, same origin in every
discipline file — that is what makes federation (§4) line up.

### 3.2 Layered wall type and walls

```python
f, body, st = skeleton("Demo Haus")

ks = api.material.add_material(f, name="Kalksandstein", category="masonry")
mw = api.material.add_material(f, name="Mineralwolle", category="insulation")
lset = api.material.add_material_set(f, name="AW 175 KS + 160 WDVS",
                                     set_type="IfcMaterialLayerSet")
for mat, t in ((ks, 0.175), (mw, 0.16)):          # build-up: building-physics skill
    layer = api.material.add_layer(f, layer_set=lset, material=mat)
    api.material.edit_layer(f, layer=layer, attributes={"LayerThickness": t})

wtype = api.root.create_entity(f, ifc_class="IfcWallType", name="AW-01",
                               predefined_type="SOLIDWALL")
api.material.assign_material(f, products=[wtype], type="IfcMaterialLayerSet",
                             material=lset)

walls = []
for i, (p1, p2) in enumerate([((0, 0), (10, 0)), ((10, 0), (10, 8)),
                              ((10, 8), (0, 8)), ((0, 8), (0, 0))]):
    w = api.root.create_entity(f, ifc_class="IfcWall", name=f"AW-EG-{i+1}")
    api.type.assign_type(f, related_objects=[w], relating_type=wtype)
    rep = api.geometry.create_2pt_wall(f, element=w, context=body, p1=p1, p2=p2,
                                       elevation=0.0, height=2.75, thickness=0.335)
    api.geometry.assign_representation(f, product=w, representation=rep)   # G-02!
    api.spatial.assign_container(f, relating_structure=st["EG"], products=[w])
    pset = api.pset.add_pset(f, product=w, name="Pset_WallCommon")
    api.pset.edit_pset(f, pset=pset, properties={
        "IsExternal": True, "LoadBearing": True,
        "FireRating": "REI 90", "ThermalTransmittance": 0.21})  # placeholders
    walls.append(w)
```

Walls are drawn counter-clockwise around the plan, so the thickness (local +y) points
**inward** for every wall [verified 0.9.0: bbox of AW-EG-2 = x 9.665…10.0].

Result [verified 0.9.0]: `get_type → AW-01`, `get_container → EG`,
`get_psets(w)["Pset_WallCommon"]` returns the four values. Corner overlap: walls 1/3 run
full length (10 m), walls 2/4 run 8 m, so the four corner blocks are counted twice —
fine for a massing demo, wrong for quantities (G-06).

### 3.3 Opening and window (void + filling)

```python
m = np.eye(4); m[0, 3] = 2.0; m[2, 3] = 0.9              # sill 0.90 m, 2.0 m from corner

opening = api.root.create_entity(f, ifc_class="IfcOpeningElement", name="Oeffnung W1")
orep = api.geometry.add_wall_representation(f, context=body, length=1.26,
                                            height=1.385, thickness=0.335)
api.geometry.assign_representation(f, product=opening, representation=orep)
api.geometry.edit_object_placement(f, product=opening, matrix=m)
api.feature.add_feature(f, feature=opening, element=walls[0])        # voids the wall

win = api.root.create_entity(f, ifc_class="IfcWindow", name="W1", predefined_type="WINDOW")
wrep = api.geometry.add_window_representation(f, context=body,
                                              overall_height=1.385, overall_width=1.26)
api.geometry.assign_representation(f, product=win, representation=wrep)
api.attribute.edit_attributes(f, product=win,
                              attributes={"OverallHeight": 1.385, "OverallWidth": 1.26})
api.geometry.edit_object_placement(f, product=win, matrix=m)
api.feature.add_filling(f, opening=opening, element=win)
api.spatial.assign_container(f, relating_structure=st["EG"], products=[win])
```

The opening body is as deep as the wall (0.335) so it cuts through cleanly. Opening
sizes are rough-opening (Rohbaumaß) sizes from `openings-windows-doors`.

**Volume-diff proof** [verified 0.9.0]: wall AW-EG-1 = 8.6279 m³ = 10 × 2.75 × 0.335
(9.2125) − 1.26 × 1.385 × 0.335 (0.5846). The cut happened.

### 3.4 Slab from a polyline (ShapeBuilder)

```python
slab = api.root.create_entity(f, ifc_class="IfcSlab", name="Decke EG",
                              predefined_type="FLOOR")
sb = ShapeBuilder(f)
outline = sb.polyline([(0, 0), (10, 0), (10, 8), (0, 8)], closed=True)
srep = sb.get_representation(body, [sb.extrude(sb.profile(outline), magnitude=0.22)])
api.geometry.assign_representation(f, product=slab, representation=srep)
m = np.eye(4); m[2, 3] = 2.75 - 0.22               # top of slab = OG level
api.geometry.edit_object_placement(f, product=slab, matrix=m)
api.spatial.assign_container(f, relating_structure=st["EG"], products=[slab])
```

[verified 0.9.0: volume 17.6 m³, bbox z 2.53…2.75.] `ShapeBuilder` coordinates are in
**project units** (here metres — G-04). For a slab with a stair hole, add an
`IfcOpeningElement` exactly as in §3.3. Slab depth: `structural-systems` /
`structural-analysis`, not this file.

### 3.5 Quantities

```python
qto = api.pset.add_qto(f, product=slab, name="Qto_SlabBaseQuantities")
api.pset.edit_qto(f, qto=qto, properties={"Width": 0.22, "GrossArea": 80.0,
                                          "GrossVolume": 17.6})
f.write("arc.ifc")
```

That is the manual way. Better — compute from geometry with `ifc5d` [verified 0.9.0]:

```python
import ifc5d.qto
els = set(f.by_type("IfcWall")) | set(f.by_type("IfcSlab"))
results = ifc5d.qto.quantify(f, els, ifc5d.qto.rules["IFC4QtoBaseQuantities"])
ifc5d.qto.edit_qtos(f, results)
```

AW-EG-1 then carries `Qto_WallBaseQuantities`: `Length 10.0, Height 2.75, Width 0.335,
GrossSideArea 27.5, NetSideArea 25.7549, GrossVolume 9.2125, NetVolume 8.6279` — net
values already subtract the window opening. Rule sets: `IFC4QtoBaseQuantities`,
`IFC4X3QtoBaseQuantities`. Same engine behind `ifcmcp`'s `ifc_quantify` and
`ifcedit quantify run`. Elements **without Body geometry are skipped silently** (G-13).

### 3.6 Distribution system with ports (HLS file)

```python
g, body2, st2 = skeleton("Demo Haus")              # same skeleton → federates with ARC
heating = api.system.add_system(g, ifc_class="IfcDistributionSystem")
api.attribute.edit_attributes(g, product=heating,
                              attributes={"Name": "Heizung VL", "PredefinedType": "HEATING"})
sb2 = ShapeBuilder(g)
segs = []
for i, (x0, length) in enumerate(((1.0, 3.0), (4.0, 3.0))):
    p = api.root.create_entity(g, ifc_class="IfcPipeSegment", name=f"VL-{i+1}",
                               predefined_type="RIGIDSEGMENT")
    solid = sb2.create_swept_disk_solid(sb2.polyline([(0, 0, 0), (length, 0, 0)]), 0.014)
    api.geometry.assign_representation(g, product=p,
                                       representation=sb2.get_representation(body2, [solid]))
    m = np.eye(4); m[0, 3] = x0; m[1, 3] = 0.5; m[2, 3] = 0.3
    api.geometry.edit_object_placement(g, product=p, matrix=m)
    api.spatial.assign_container(g, relating_structure=st2["EG"], products=[p])
    segs.append(p)
api.system.assign_system(g, products=segs, system=heating)
pa = api.system.add_port(g, element=segs[0]); pb = api.system.add_port(g, element=segs[1])
api.system.connect_port(g, port1=pa, port2=pb, direction="SOURCE")
g.write("hls.ifc")
```

Pipe radius 0.014 m = DN 25-ish outside radius, placeholder — sizing is
`building-services-tga`. Real MEP models also need fittings (`IfcPipeFitting`),
flow-direction ports placed at segment ends, and terminals (`IfcSpaceHeater`).

### 3.7 Other element classes — choose the right entity

Entity and `PredefinedType` choice (e.g. `IfcSlab` FLOOR vs ROOF vs BASESLAB,
`IfcFooting` STRIP_FOOTING, `IfcStair` + `IfcStairFlight`, `IfcCovering` for
screed/finishes, `IfcSpace` for rooms) is owned by `bim-management` §8 (entity map).
**Never fall back to `IfcBuildingElementProxy`** for something that has a real class —
`ifc-model-validation` treats proxies as a finding.

## 4. Federation — one IFC per discipline

What the BIM practice expects (and what `bim-management` §5–§6 describe as process):
each discipline delivers its own file — ARC (Architektur), TWP (Tragwerk), HLS
(Heizung/Lüftung/Sanitär), ELT (Elektro), optionally BRS (Brandschutz), AUS (Außenanlagen).
A coordinator loads them together for review and clash detection; nobody edits another
discipline's file.

Rules for authored files:

1. **Shared skeleton** (§3.1) — same `IfcSite`/`IfcBuilding`/storey names, elevations
   and origin in every file. Different names = viewers show two "EG" storeys that don't
   match.
2. **Shared coordinates.** Model near the origin (0,0,0); put the real-world position in
   georeferencing (`georeference.add_georeferencing` /
   `georeference.edit_georeferencing`, IFC4: `IfcMapConversion` + `IfcProjectedCRS`,
   in DACH typically ETRS89/UTM, EPSG:25832 or 25833 — `VERIFY` the project's CRS)
   — never by placing geometry 5 000 000 m from the origin (float precision, viewer
   jitter).
3. **Same schema and units** in every file of a delivery.
4. **One file per discipline per building** (large projects: per building section too).
   File naming per `bim-management` (ISO 19650 naming fields).
5. **Don't merge for delivery.** `ifcpatch` recipe `MergeProjects` does produce one
   file [verified 0.9.0: 1 `IfcProject`] — but it **duplicates the spatial tree**
   (storeys after merge: `['EG', 'OG', 'EG', 'OG']`). Merge only for a quick look;
   federate in the viewer for coordination.
6. Clash between discipline files: Bonsai/`ifcclash`, or `ifcmcp`'s `ifc_clash`;
   results go back as BCF (`bim-management` §11).

## 5. Verification — prove every increment

### 5.1 Geometry measurement

```python
import ifcopenshell, ifcopenshell.geom, ifcopenshell.util.shape as us
f = ifcopenshell.open("arc.ifc")
s = ifcopenshell.geom.settings(); s.set("use-world-coords", True)
for e in f.by_type("IfcElement"):
    g = ifcopenshell.geom.create_shape(s, e).geometry
    print(e.is_a(), e.Name, round(us.get_volume(g), 4), us.get_bbox(us.get_vertices(g)))
```

[verified 0.9.0] output (abridged):

```
IfcSlab   Decke EG     17.6    [0,0,2.53] .. [10,8,2.75]
IfcWall   AW-EG-1      8.6279  [0,0,0]    .. [10,0.335,2.75]    <- voided
IfcWall   AW-EG-2      7.37    [9.665,0,0]..[10,8,2.75]
IfcWindow W1           0.032   [2,0.05,0.9]..[3.26,0.125,2.285]
```

`create_shape` raises `RuntimeError: No suitable IfcRepresentation found` for an element
without Body geometry — catch it and report the element; that error is the evidence
for G-02. For many elements use `ifcopenshell.geom.iterator` (multi-core) instead of a
`create_shape` loop.

PASS/FAIL discipline is the same as `construction-freecad-bim` §2.4: every placement is
asserted against intent by bbox, every cut by volume difference, with a printed line.

### 5.2 Querying the model

`ifcopenshell.util.element`: `get_psets`, `get_type`, `get_container`, `get_material`,
`get_decomposition`. `ifcopenshell.util.selector.filter_elements` takes a query string
[verified 0.9.0]:

```python
sel.filter_elements(f, "IfcWall, Pset_WallCommon.IsExternal=TRUE")   # -> 4 walls
sel.filter_elements(f, 'IfcElement, location="EG"')                    # by storey
```

Note: `IfcElement` includes `IfcOpeningElement` (a feature element) — filter it out when
counting building elements.

### 5.3 Schema, rules, IDS — hand-off to `ifc-model-validation`

```bash
python -m ifcopenshell.validate arc.ifc            # schema + attribute types
python -m ifcopenshell.validate --rules arc.ifc    # + EXPRESS WHERE rules (needs pytest)
```

[verified 0.9.0: both report `No validation issues found` on the final demo file.]
**And the same zero-error result was obtained on the faulty first run in which all four
walls had no representation** — schema validation does not notice missing geometry,
missing Psets or wrong placement. That is why §5.1 and IDS exist.

IDS check with `ifctester` [verified 0.9.0]:

```python
import ifctester.ids, ifctester.reporter
ids = ifctester.ids.Ids(title="Demo")
spec = ifctester.ids.Specification(name="Aussenwaende haben FireRating", ifcVersion=["IFC4"])
spec.applicability.append(ifctester.ids.Entity(name="IFCWALL"))
spec.requirements.append(ifctester.ids.Property(propertySet="Pset_WallCommon",
                         baseName="FireRating", dataType="IFCLABEL"))
ids.specifications.append(spec)
ids.validate(ifcopenshell.open("arc.ifc"))
ifctester.reporter.Console(ids).report()            # -> [PASS] (4/4)
```

Full check chain, normative buildingSMART rules, DACH IDS starter set and quality
gates: `ifc-model-validation`.

## 6. Driving it through an agent (`ifcmcp`)

### 6.1 Tool surface [verified 0.9.0: 25 tools listed by `ifcopenshell-mcp` 0.9.0]

| Group | Tools |
|---|---|
| Session | `ifc_new(schema="IFC4")`, `ifc_load(path)`, `ifc_save(path="")` (empty path overwrites the loaded file), `ifc_reset()` |
| Query | `ifc_summary`, `ifc_tree`, `ifc_info(element_id)`, `ifc_select(query)` (selector syntax §5.2), `ifc_relations(element_id, traverse="")` (`"up"` → to project), `ifc_contexts`, `ifc_materials`, `ifc_schema(entity_type)`, `ifc_schedule`, `ifc_cost` |
| Check | `ifc_validate(express_rules=False)`, `ifc_clash(element_id, clearance=0.0, tolerance=0.002, scope="storey"\|"all")` (metres) |
| Edit | `ifc_list(module="")`, `ifc_docs(function_path)`, `ifc_edit(function_path, params)`, `ifc_quantify(rule, selector="")` |
| Shape builder | `ifc_shape_list`, `ifc_shape_docs(method)`, `ifc_shape(method, params)` |
| Look | `ifc_plot(selector, view="floorplan"\|"elevation"\|"section"\|"auto", …)` → PNG (needs `cairosvg`), `ifc_render(selector, view="iso"\|"top"\|…)` (needs `pyvista`) |

**`ifc_edit` is `ifcopenshell.api` by name.** `function_path` = `"module.function"`,
`params` = JSON object of the function's keyword arguments, minus `file`. Values are
coerced from the type hints: an entity is its step id as a string (`"42"`), a list of
entities is `"5,6,7"`, dicts/matrices are JSON, booleans `"true"`. Result:
`{"ok": true, "result": {"id": …, "type": …}}` — keep the returned ids, you need them
for the next call. Use `ifc_docs("geometry.add_wall_representation")` instead of
guessing parameters.

### 6.2 Bootstrapping a new model through MCP [verified 0.9.0]

`project.create_file` cannot be called through `ifc_edit` (it takes no `file`); use
`ifc_new`, then the §3.1 skeleton call by call:

```
ifc_new        {"schema": "IFC4"}
ifc_edit root.create_entity        {"ifc_class": "IfcProject", "name": "MCP Haus"}   -> #1
ifc_edit unit.add_si_unit          {"unit_type": "LENGTHUNIT"}                         -> #2 (METRE)
ifc_edit unit.assign_unit          {"units": "2"}
ifc_edit context.add_context       {"context_type": "Model"}                           -> #8
ifc_edit context.add_context       {"context_type": "Model", "context_identifier": "Body",
                                    "target_view": "MODEL_VIEW", "parent": "8"}        -> #9
ifc_edit root.create_entity        IfcSite #10, IfcBuilding #12, IfcBuildingStorey #11
ifc_edit aggregate.assign_object   {"products": "10", "relating_object": "1"}  (… site→building→storey)
ifc_edit geometry.edit_object_placement {"product": "10"}   (… for 12 and 11)
ifc_edit root.create_entity        {"ifc_class": "IfcWall", "name": "AW-1"}           -> #31
ifc_edit geometry.add_wall_representation {"context": "9", "length": 5, "height": 2.75,
                                    "thickness": 0.3}                                  -> #41
ifc_edit geometry.assign_representation {"product": "31", "representation": "41"}
ifc_edit geometry.edit_object_placement {"product": "31",
                                    "matrix": [[1,0,0,2],[0,1,0,1],[0,0,1,0],[0,0,0,1]]}
ifc_edit spatial.assign_container  {"products": "31", "relating_structure": "11"}
ifc_save       {"path": "mcp_new.ifc"}
```

Measured afterwards with §5.1: volume 4.125 m³ (= 5 × 2.75 × 0.3), bbox
`[2,1,0]..[7,1.3,2.75]` — the nested-list matrix is accepted. **The step ids above are
from one run; always use the ids the tool returns.**

### 6.3 Agent loop over MCP

1. `ifc_load` (or §6.2 bootstrap) → `ifc_summary` + `ifc_tree` to orient. Never read the
   file as text.
2. Per increment: `ifc_edit` calls → `ifc_select`/`ifc_info` to confirm the
   relationships → `ifc_validate` → `ifc_save` to a **new versioned path**
   (`arc_v003.ifc`), not over the input.
3. After geometry increments: `ifc_quantify` and compare the count with
   `ifc_select` (G-13); `ifc_plot` floorplan for a visual check; for hard numbers run
   §5.1 (outside MCP) on the saved file.
4. `ifc_validate` passing is necessary, not sufficient (§5.3) — run the project IDS with
   `ifctester` before calling a delivery done.

### 6.4 How an LLM should work with IFC files


From the IfcLLM study (Lamsal et al., arXiv 2605.13236, 2026) and this skill's own runs:

- **Never read a raw `.ifc` into the context.** The small FZK-Haus reference model
  tokenizes to ≈1.7 million tokens. Use structured tools (`ifc_summary`, `ifc_tree`,
  `ifc_select`, `ifc_info`, `util.selector`, `util.element`) that return only what the
  question needs.
- **Query narrowly.** The study's failures were queries that returned more rows than the
  model could hold; the fix was a more targeted query. Select by class + Pset filter +
  storey, return counts first, details second.
- **Retry-and-refine with validation beats one-shot.** First-attempt accuracy was
  93–100 % only *with* an iterative loop. For authoring the equivalent is
  write → measure (§5.1) → validate (§5.3) → repair, one increment at a time.
- **Watch semantic errors, not only syntax errors.** The study's model computed building
  height as the *sum* of storey elevations. Cross-check derived numbers (heights, areas,
  volumes) against an independent calculation before reporting them.
- Data protection: IFC models of real projects are confidential. An agent pipeline that
  sends model content to a cloud LLM needs the client's consent; local open-weight
  models are an option (the study used gpt-oss-120b).

## 7. GOTCHAS

| # | Symptom | Cause / fix |
|---|---|---|
| G-01 | `AttributeError: module 'ifcopenshell.api' has no attribute 'project'` | `import ifcopenshell.api` does not import submodules. `import ifcopenshell.api.project` (and every other module you call) explicitly (not `api.run`, deprecated). [verified 0.9.0] |
| G-02 | Walls exist in the tree, viewer shows nothing, `validate` reports 0 errors | `geometry.create_2pt_wall` **returns** the representation and sets the placement but does **not assign** the representation. Follow with `geometry.assign_representation`. Same for every `add_*_representation` function. [verified 0.9.0 — source read: function ends `return representation`] |
| G-03 | Window/door not cutting the wall | Window placed but no `IfcOpeningElement`, or opening not linked with `feature.add_feature`. Opening at least as deep as the wall — the docs make it slightly **deeper** (and start it slightly in front) to avoid coplanar-face float problems. Check by volume diff (§3.3). Removing an opening (`feature.remove_feature`) leaves its filling orphaned. |
| G-04 | Geometry 1000× too large/small | API geometry functions take SI metres; `ShapeBuilder` and raw `create_entity` geometry take project units. In a millimetre project, multiply by 1000 there. Check `util.unit.calculate_unit_scale(f)`. |
| G-05 | Layer set says 335 mm, wall body is 300 mm | API does not reconcile `LayerThickness` sum with representation thickness. Compute thickness from the layer set and pass it to the wall function. |
| G-06 | Wall quantities too high | Butt-joined walls drawn to the outer corner overlap. Shorten one wall by the thickness, or connect with `geometry.connect_path` and regenerate, then re-measure. |
| G-07 | `validate --rules` crashes in `rule_executor` / `_pytest` | `pip install pytest`. [verified 0.9.0] |
| G-08 | Two "EG" storeys in the viewer after loading discipline files | Spatial skeleton differs (names, elevations, placement) between files — or the files were merged with `MergeProjects` (§4). |
| G-09 | Element missing from storey schedules | Not contained (`spatial.assign_container`) — or contained in two storeys (illegal; use reference). |
| G-10 | Pset ignored by receiving tool | Misspelled standard Pset/property name or wrong data type. Names are case-sensitive; check against the schema (`bim-management` §8). |
| G-11 | Georeferenced model "jumps" or jitters | Geometry placed at real UTM coordinates. Keep geometry near origin, put the offset into `IfcMapConversion`. |
| G-12 | Quantities don't match geometry | Hand-typed `Qto_` values. Compute with `ifc5d` (§3.5). |
| G-13 | `ifc_quantify` reports fewer elements than selected | Elements without Body geometry are skipped, no warning. [verified 0.9.0: 5 walls selected, `elements_quantified: 4` — the 5th was created via `ifc_edit` without a representation.] Compare counts every time. |
| G-14 | `ifc_new` model won't take geometry | `ifc_new` creates a **completely empty** file — no project, units or contexts. Bootstrap per §6.2 first. |
| G-15 | `pip install ifcmcp` fails | Package is `ifcopenshell-mcp` (§1.2). |
| G-16 | Layer thicknesses 1000× off | `edit_layer` `LayerThickness` is in **project units** (metres here, mm in a mm project), unlike the SI-metre geometry helpers. |

## 8. Agent workflow

```
0. BRIEF      discipline(s), schema (IFC4), units, CRS, LOIN per bim-management.
1. PLAN       design values from owning skills (plan, build-ups, sizes) BEFORE geometry.
2. SKELETON   §3.1 skeleton, identical across discipline files; write + validate.
3. MODEL      one element type per increment: types/materials → walls → openings
              → slabs → roof → stairs → spaces → MEP systems.
4. VERIFY     after each increment: §5.1 measure (bbox/volume PASS/FAIL print),
              §5.3 validate; IDS at the end of each discipline.
5. FEDERATE   load all discipline files in the viewer; clash; BCF back.
6. DOCUMENT   status: what is measured, what is validated, what is placeholder.
              Structural adequacy: unverified unless analysed (structural-analysis;
              FEM via construction-freecad-bim §3.8) — say so unprompted.
```

Vocabulary rules from `construction-freecad-bim` §7.2 apply unchanged: "schema-valid",
"IDS pass (n/n)", "volume-diff verified" — never "correct", "safe" or "ready to build".
