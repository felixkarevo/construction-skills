# Construction Design & Engineering Skills for AI Agents

**A complete, agent-neutral knowledge library for designing, engineering and delivering buildings — plus a working FreeCAD BIM workflow.** 30 dense reference skills (`SKILL.md`) covering the whole construction stack, **governed by a simple-first principle**: the default building answer is always the *simplest proven solution at the agreed standard tier* — more demanding construction only on explicit, priced client request, and any deviation below the usual standard only through the documented German civil-law risk-acceptance machinery. The stack: spatial planning, structural systems and analysis, concrete/masonry/timber/steel design, geotechnics, seismic design, building physics (heat, moisture, acoustics, fire), materials, construction detailing, building services (TGA), roofing & waterproofing, stairs, openings, accessibility, BIM management, cost (DIN 276), scheduling, building law & permits, sustainable construction, existing structures, home renovation & refurbishment, and technical drawing — calibrated to **German and European practice (DIN, EN, Eurocodes + National Annex, GEG, MBO/LBO, VOB, HOAI, ISO 19650)**, distilled from specialized construction literature.

Works with **any MCP-capable AI agent** (OpenCode, Claude Code, Codex, Cursor, …) — no agent product is required or referenced inside the skills.

The repository also bundles a real, verifiable demo: a complete residential BIM model built entirely through a live agent ↔ FreeCAD connection ([`example/`](example/)).

![Isometric view of the example model](example/images/isometric.png)

## How to use

1. **Load the skills** into your agent's skill/knowledge directory (most agents accept a folder of `SKILL.md` files, e.g. `.claude/skills/`, `skills/`, or system-prompt includes). Every file is self-contained reference material with frontmatter (`name`, `description`). The root [`SKILL.md`](SKILL.md) is a **router**: it maps tasks/keywords to the right discipline skill(s) and gives the multi-skill sequence for project-level asks — consult it first, especially for anything spanning more than one discipline. Agent harnesses that read an `AGENTS.md` will pick this up automatically via [`AGENTS.md`](AGENTS.md).
2. **Connect FreeCAD** with the [neka-nat/freecad-mcp](https://github.com/neka-nat/freecad-mcp) server:
   - Install FreeCAD **1.0+** (desktop GUI — the RPC bridge needs a live event loop, not headless).
   - Copy the `addon/FreeCADMCP` folder of the repo into FreeCAD's Mod directory (Linux: `~/.FreeCAD/Mod/` or `~/.local/share/FreeCAD/Mod/`; Windows: `%APPDATA%\FreeCAD\Mod\`; macOS: `~/Library/Application Support/FreeCAD/v1-1/Mod/`), restart FreeCAD, open the **MCP** workbench and **Start RPC Server** (an Auto-Start option exists).
   - Register the MCP server with your agent, e.g. via `uv`:
     ```json
     { "mcpServers": { "freecad": { "command": "uvx", "args": ["freecad-mcp"] } } }
     ```
   - Tools exposed: `create_document`, `create_object`, `edit_object`, `delete_object`, `execute_code` (persistent Python namespace with `FreeCAD`/`App`/`Gui`), `insert_part_from_library`, `get_view`, `get_object(s)`, `list_documents`, `get_rpc_status`, and `run_fem_analysis` (CalculiX solver: von Mises, displacement, node count). Screenshot feedback can be toggled per call (`include_screenshot`, `view_name`) or globally (`--only-text-feedback`) to save tokens.
3. **Set the standard first** — read [`skills/simple-first-building/SKILL.md`](skills/simple-first-building/SKILL.md): it fixes the complexity ladder (what "simple" means per discipline), the civil-law default machinery (§ 633 BGB, aarRdT, DIN presumption), how to deviate up or down lawfully, and the Gebäudetyp E / pilot-standard status. It's governing — the root router loads it alongside whatever specialist skill it points you to. Then read [`skills/construction-freecad-bim/SKILL.md`](skills/construction-freecad-bim/SKILL.md) for modeling mechanics; its "How this library fits" table also routes every task to the right discipline skill.

## The skill library

| Group | Skills |
|---|---|
| **Governing** | `simple-first-building` (THE default-setting skill: complexity ladder per discipline; § 633 BGB defect mechanics, aarRdT as implied minimum, DIN presumption & rebuttal, lawful downward deviation with Beweislast/insurance/Gleichwertigkeit, liability through Kauf-/Miet-kette, Gebäudetyp E Eckpunkte + Bavaria/Hamburg/Schleswig-Holstein pilots with numbers; every other skill carries its simple-first gate) |
| **Modeling & BIM** | `construction-freecad-bim` (core: spatial hierarchy, parametric openings via void-extrusion, `Arch.makeRebar` cages, FEM verification, IFC import (NativeIFC) and export, 35+ FreeCAD gotchas), `bim-management` (ISO 19650 requirement chain, CDE, LoD/LoI/LOG, IFC/BCF, FM handover) |
| **Planning & form** | `building-planning-spatial` (B-Plan envelope → dimensionally defensible plan), `building-typology` (EFH/DHH/Zeile/MFH/atrium decision logic), `construction-drawing-sketching` (representation, sketch→model→review loop) |
| **Structural engineering** | `structural-systems` (concept choice, grids, load paths), `structural-analysis` (EN 1990/1991 actions & combinations, worked chains), `concrete-detailing` (EC2 + NA: anchorage, laps, cover, WU), `masonry-construction` (EC6 + NA), `timber-steel-design` (EC5/EC3 incl. connectors, plate buckling, warping torsion), `geotechnics-foundations` (DIN 1054/4017, EA-Pfähle), `seismic-design` (EC8 configuration & detailing discipline) |
| **Building physics** | `building-physics-thermal-moisture` (U/Ψ, Glaser, fRsi/mould, n50, summer heat), `building-acoustics` (DIN 4109, mass/flanking laws, DIN 18041, TA Lärm), `fire-protection-building` (MBO building classes, F/T/R classes, DIN 4102 ↔ EN 13501, Eurocode fire design) |
| **Construction & materials** | `construction-detailing` (layer buildups, junctions, joints, tolerances), `building-materials` (cement→concrete→steel→timber→glass: classes, values, durability, CE/abZ), `roofing-waterproofing` (pitched + flat roofs, DIN 18531-18535), `openings-windows-doors` (lintels, three-seal joint, Uw data), `stairs-vertical-circulation` (DIN 18065 geometry, EN 81 lifts) |
| **Services & delivery** | `building-services-tga` (heat pump/HP hydraulics, FBH, DIN 1946-6 ventilation, DVGW water hygiene, DIN 18015/VDE electrical, coordination), `construction-scheduling-site` (CPM/Takt/BAS productivity, site setup, SiGeKo, incl. surveying methods), `cost-management-din276` (DIN 276:2018, KLR Bau price buildup, VOB/C, HOAI), `building-regulations-permits` (Bauleitplanung, B-Plan reading, LBO/GEG layers, VOB/B, liability) |
| **Whole-life** | `sustainable-construction` (LCA/EPDs, GWP per material, GEG duties, circularity, taxonomy/CRREM), `accessibility-universal-design` (DIN 18040 audit workflow), `existing-structures-retrofit` (Nachrechnung, DIN 1076, strengthening, GEG retrofit), `building-renovation-refurbishment` (Bestandsaufnahme, Bauteil-Sanierungstechnik, Sanierungsfahrplan/GEG, ökologisches Sanieren, Abbruch/Rückbau, Artenschutz), `timber-building-renovation` (historische Holzkonstruktionen, Schadensanalyse/-bewertung, Ertüchtigung, Fachwerk/Umgebindebau) |

**Reading order for a project:** `simple-first-building` (tier + ladder profile as contract text!) → `building-regulations-permits` + `building-planning-spatial` → `building-typology` → `structural-systems` → physics skills as governing constraints → detailing/materials skills → `building-services-tga` + `construction-scheduling-site` + `cost-management-din276` → `construction-freecad-bim` (+ `bim-management` for data discipline) → verification per `structural-analysis`.

Every skill carries a **reality check** (what the output may and may not be used for) and an **evidentiary tier system** that separates law (`GEG`, `MBO`/`LBO`, Eurocode + NA as recognized rules of technique), standards-of-practice and tagged `VERIFY` placeholders — so a planning placeholder is never confused with a binding figure. Values that depend on jurisdiction or edition are explicitly marked for confirmation.

## The example model (`example/`)

`example-house.FCStd` — a real BIM model with 700+ parametric objects (walls with verified void openings, footings, tie columns, rebar cages, doors/windows, MEP risers, electrical schedule), built and verified entirely through the MCP bridge: opening geometry checked by volume-diff, footings by load take-down + bearing check, selected members by actual CalculiX runs via `run_fem_analysis`. `example/work_log_legacy.md` documents what broke and how it was fixed — several FreeCAD API gotchas in the core skill came from this log. The model's original commission was a compact South-Asian plot; it is kept as a historical demonstration of workflow, not as planning guidance (see the banner in the docs).

## ⚠️ Reality check — read before building anything

**Nothing in this repository is construction-ready.** All member sizes, reinforcement schedules, U-values and cost figures are **planning-stage aids**. Before real use:

1. A **licensed engineer/architect** (Tragwerksplaner, Prüfstatik where required, energy certificate issuer per GEG, Brandschutzfachplaner) must review and sign the design.
2. **Site-specific geotechnical investigation** replaces every assumed soil value (DIN 4020 GK classes apply).
3. **Current legal texts prevail**: land building codes differ by Bundesland, GEG/DIN editions change, B-Plans override generic figures. Every skill flags which numbers must be re-verified at building-authority level.
4. FEM/reinforcement coverage in the example model is **partial** — see the work log for what was checked and what was not.

## License

Skills and documentation: MIT. Example model & renders: CC-BY-4.0 (attribution appreciated).

## Contributing

PRs welcome: new discipline skills, corrections to standards figures (with edition date), more FreeCAD gotchas, ports of the tier system to other jurisdictions. Keep the house style: frontmatter `name`+`description`, reality check, evidentiary tiers, numeric density, `VERIFY` tags for anything not grounded in a standard's current text — and no vendor/agent branding inside skill content.
