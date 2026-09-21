---
name: construction-skills-router
description: >
  Router / index for the 31 discipline skills in this DACH construction-design
  library (skills/*). Consult this FIRST for any building-design, structural,
  building-physics, cost, scheduling, legal/permit, BIM, or FreeCAD-modeling
  task in this repo — before opening any single discipline skill — so the
  right skill(s) get loaded instead of guessed at. Especially important for
  broad or ambiguous asks that span multiple disciplines ("design a house",
  "check this wall", "what U-value do I need", "size the foundation", "model
  this in FreeCAD", "what does this cost") where picking only one skill would
  miss the governing or adjacent ones. Always load simple-first-building's
  complexity ladder alongside whatever specialist skill this router points to.
---

# Construction Skills Router

This repo is 31 dense reference skills (`skills/*/SKILL.md`) covering the
whole DACH (Germany/Austria/Switzerland) building-design stack, plus a live
FreeCAD BIM workflow. No single skill covers a whole project — this file maps
a task or question to the skill(s) that actually answer it, so you load the
right reference instead of guessing or trying to answer from general
training data (DIN/EN/Eurocode figures, thresholds and edition traps are
exactly what these skills correct for).

## Rule zero: simple-first-building is always in scope

`simple-first-building` is the **governing** skill: it sets the complexity
ladder (what "simple" means per discipline) and the German civil-law
machinery behind it (§ 633 BGB defect test, aarRdT, DIN presumption, lawful
downward deviation, Gebäudetyp E). Every other skill defers its default
answer to this one. Load it alongside any specialist skill whenever a design
decision (not just a lookup) is being made — i.e. whenever you're choosing a
build-up, a system, or a standard tier, not just reading off a table.

## How to use this router

1. Identify what the user is actually asking: a **lookup** (one number/rule),
   a **check** (verify something against a standard), a **design** (produce
   a sized/detailed solution), or a **project-level** task (spans phases).
2. Match keywords/intent against the table below to find the owning skill(s).
3. If the task spans categories (most real design tasks do), load all
   matching skills — cross-references between them are called out in each
   skill's own text (e.g. structural-systems hands off to
   structural-analysis, concrete-detailing, masonry-construction).
4. If still unsure between two close skills, read both descriptions in
   `skills/*/SKILL.md` frontmatter (one paragraph each) before picking —
   they are dense and specific, cheaper to skim than to guess wrong.

## Lookup table: task/keyword → skill

| If the task involves... | Use skill |
|---|---|
| Default complexity tier, "keep it simple", contract/defect liability, § 633 BGB, aarRdT, DIN presumption, Gebäudetyp E | `simple-first-building` (governing — see Rule zero) |
| Plot/B-Plan reading, GRZ/GFZ, envelope test, room sizing, orientation/sun, staircase-first layout | `building-planning-spatial` |
| Choosing house form (EFH/DHH/Reihenhaus/MFH/atrium), plan-depth/daylight, compactness, density | `building-typology` |
| Freehand/CAD drawing conventions, projections, hatching, dimensioning, plan-set types | `construction-drawing-sketching` |
| Building law, permits, Bauleitplanung, Bauvorlagen, HOAI Leistungsphasen, VOB/BGB contract basics | `building-regulations-permits` |
| Choosing the structural concept, load paths, spans, grids, bracing systems | `structural-systems` |
| Actions/load combinations (EN 1990/1991), beam/slab/column sizing, worked static checks | `structural-analysis` |
| RC reinforcement detailing, bar scheduling, anchorage, laps, cover, WU/Weiße Wanne, fibre/steel-fibre concrete (Faserbeton), carbon/textile-reinforced concrete | `concrete-detailing` |
| Masonry wall design (EC6), unit/mortar groups, shear walls, wall typologies | `masonry-construction` |
| Timber (EC5) or steel (EC3) member/connection design, CLT, profiles, bolted/welded joints | `timber-steel-design` |
| Soil, foundations, bearing capacity, settlement, piles, earth pressure, excavation/shoring | `geotechnics-foundations` |
| Earthquake design, EC8 configuration, ductility, regularity, confined masonry | `seismic-design` |
| U-values, thermal bridges, condensation/Glaser, airtightness (n50), summer heat protection | `building-physics-thermal-moisture` |
| Sound insulation (airborne/impact), flanking transmission, room acoustics, noise immission | `building-acoustics` |
| Fire resistance classes, escape routes, fire compartments, Eurocode fire design | `fire-protection-building` |
| Layer build-ups/junction details, joint grammar, tolerances, movement joints | `construction-detailing` |
| Material selection/properties: concrete, masonry units, steel, timber, insulation, glass, CE marks | `building-materials` |
| Roof design (pitched/flat), waterproofing membranes, below-grade tanking (black/white tub) | `roofing-waterproofing` |
| Lintels, window/door build-ups, U_w calc, sealing joints, mounting classes, structural glazing/DIN 18008, isochoric climatic load | `openings-windows-doors` |
| Stair geometry/set-out, ramps, lifts, stair structural/acoustic/fire checks | `stairs-vertical-circulation` |
| Heating/cooling systems, DHW/legionella, ventilation, TGA sizing, heat pumps | `building-services-tga` |
| Construction sequencing, CPM/Takt scheduling, site layout, crew productivity | `construction-scheduling-site` |
| Cost estimating/planning (DIN 276), unit-price buildup, VOB/C, HOAI fees | `cost-management-din276` |
| Whole-life carbon/LCA, EPDs, GEG energy duties, circularity, sustainability certification | `sustainable-construction` |
| Accessibility/barrier-free design, DIN 18040 audit, wheelchair geometry | `accessibility-universal-design` |
| Existing buildings: condition assessment, Nachrechnung, strengthening, retrofit, cathodic protection (KKS), component reuse/circular deconstruction — the structural-engineering side of Bauen im Bestand | `existing-structures-retrofit` |
| Home renovation/refurbishment (Sanierung, Renovierung, Modernisierung, Instandsetzung) at the building-component level: Bestandsaufnahme workflow, Naturstein/Beton/Metall/Mauerwerk/Dach/Decken/Fenster/Türen/Fugen/Putz repair, Sanierungsfahrplan (iSFP) and GEG Nachrüstpflichten, ökologisches Sanieren, Abbruch/Rückbau, bautechnischer Artenschutz, ÖNORMEN supplement | `building-renovation-refurbishment` |
| Historical/existing timber construction: Schadensanalyse (fungal/insect/moisture diagnosis, Hausschwamm), Schadensbewertung (residual strength of decayed members), Ertüchtigung/Instandsetzung technique, Fachwerk, Umgebindebau, historische Zimmermannsverbindungen and Dübelnormung | `timber-building-renovation` |
| ISO 19650 BIM process, CDE, LOD/LOIN, IFC/BCF, model coordination, material passports/Ressourcenpass data schema; IFC schema lookup — which entity a component becomes, `PredefinedType`, which `Pset_*`/`Qto_*` properties exist, IFC2x3/IFC4/IFC4.3 version breaks, where to fetch the schema | `bim-management` |
| Actually modeling in FreeCAD via the MCP bridge (objects, storeys, rebar, FEM, IFC import/export) | `construction-freecad-bim` |
| Proving an IFC export correct instead of assuming it: model checking, IDS (`.ids`) authoring and running, buildingSMART normative/Gherkin rule failures, `ifcopenshell.validate` / `ifctester` / `ifcpatch`, quality gates for an automated author→export→check→repair loop | `ifc-model-validation` |

## Task recipes (multi-skill sequences)

For anything project-shaped rather than a single lookup, load skills in this
order (skip phases that don't apply):

1. `simple-first-building` — fix the standard tier before anything else.
2. `building-regulations-permits` + `building-planning-spatial` — what's
   legally buildable on this plot.
3. `building-typology` — pick the building form.
4. `structural-systems` — pick the structural concept and grid.
5. Physics skills as governing constraints: `building-physics-thermal-moisture`,
   `building-acoustics`, `fire-protection-building` (and `seismic-design`,
   `geotechnics-foundations` where relevant).
6. Detailing/materials skills: `construction-detailing`, `building-materials`,
   `concrete-detailing` / `masonry-construction` / `timber-steel-design`,
   `roofing-waterproofing`, `openings-windows-doors`, `stairs-vertical-circulation`.
7. `building-services-tga` + `construction-scheduling-site` +
   `cost-management-din276` — services, sequencing, cost.
8. `construction-freecad-bim` (+ `bim-management` for data discipline) — build
   the model.
9. `ifc-model-validation` — prove the export: syntax/schema, normative rules, then
   the project's IDS. Run it after every export, not once at the end.
10. Verify against `structural-analysis`.

Round out with `accessibility-universal-design`, `sustainable-construction`,
`existing-structures-retrofit` whenever the brief touches those concerns. For a
renovation/refurbishment project specifically, load `building-renovation-refurbishment`
(+ `timber-building-renovation` where timber is involved) alongside step 5's physics
skills and step 6's detailing skills, and use `construction-freecad-bim` §3.10 to model
the Bestand→Neu transition.

## Full skill index

See the table in `README.md` ("The skill library") for the same 31 skills
grouped by category with one-line descriptions each — read that if this
router's keyword table doesn't resolve the ambiguity.
