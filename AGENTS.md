# AGENTS.md

This repo is a reference library, not an application — 30 discipline `SKILL.md`
files under `skills/*` covering DACH (Germany/Austria/Switzerland) building
design and engineering, plus a live FreeCAD BIM demo under `example/`.

## Start here

**Read the root [`SKILL.md`](SKILL.md) first**, before opening any file under
`skills/*`. It's a router: it maps task keywords to the owning skill(s), gives
multi-skill sequences for project-level asks, and states Rule Zero —
`simple-first-building` (the complexity-ladder / civil-law governing skill)
is in scope alongside whatever specialist skill it points you to, whenever a
design decision (not a pure lookup) is being made.

If the router's keyword table doesn't resolve an ambiguity, `README.md`'s
"The skill library" table gives the same 30 skills grouped by category with
one-line descriptions.

## Working in this repo

- **Skills are reference content, not code.** There's no build/test/lint step
  for `skills/*/SKILL.md` — changes are prose/data edits. Read a skill fully
  before editing it; they're dense and cross-reference each other.
- **House style** (keep it when adding or editing a skill): YAML frontmatter
  with `name` + `description` (description states what the skill covers *and*
  when to trigger it); a reality-check section on what the output may/may not
  be used for; an evidentiary-tier system distinguishing law (GEG, MBO/LBO,
  Eurocode+NA as recognized rules of technique) from standards-of-practice
  from `VERIFY`-tagged placeholders; numeric density (real values, tables,
  worked examples) over prose description; no vendor/agent branding inside
  skill content (the library is agent-neutral — OpenCode, Claude Code, Codex,
  Cursor, etc. all load the same files).
- **Numbers are jurisdiction- and edition-sensitive.** Anything tagged
  `VERIFY` in a skill is a placeholder that must be checked against the
  current standard text or the local Bundesland/B-Plan before real use —
  don't strip these tags when editing, and add one when introducing a new
  figure you haven't confirmed against a current source.
- **`example/`** is a historical FreeCAD demo model (South-Asian plot,
  700+ objects, built via the [neka-nat/freecad-mcp](https://github.com/neka-nat/freecad-mcp)
  bridge). Treat it as a workflow demonstration, not planning guidance for a
  real project — `example/work_log_legacy.md` documents what was actually
  verified (volume-diff openings, load take-down footings, CalculiX FEM runs)
  versus what wasn't.
- **`sources/`** holds the literature this library was distilled from —
  consult it for provenance when a figure looks wrong before changing it.

## Adding a new skill

Follow the pattern of an existing skill closest to the new topic (frontmatter,
reality check, evidentiary tiers, `VERIFY` tags). Then:
1. Add it to the root [`SKILL.md`](SKILL.md) router's lookup table (and, if it
   changes a project-level sequence, the task-recipes section).
2. Add it to the matching category row in `README.md`'s "The skill library"
   table.

## Reality check

**Nothing in this repository is construction-ready.** Member sizes,
reinforcement schedules, U-values and cost figures are planning-stage aids —
a licensed engineer/architect must review and sign off before real use, and
site-specific data (geotechnical investigation, current B-Plan, current
GEG/DIN edition) always overrides generic figures in these skills. See
`README.md`'s "Reality check" section for the full statement.
