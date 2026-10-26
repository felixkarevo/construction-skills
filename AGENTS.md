# AGENTS.md

This repo is a reference library, not an application — 33 discipline `SKILL.md`
files plus the `construction-skills-router` under `skills/*` covering DACH
(Germany/Austria/Switzerland) building design and engineering, plus a live
FreeCAD BIM demo under `example/`.

## Start here

**Read the router [`skills/construction-skills-router/SKILL.md`](skills/construction-skills-router/SKILL.md)
first**, before opening any other file under
`skills/*`. It's a router: it maps task keywords to the owning skill(s), gives
multi-skill sequences for project-level asks, and states Rule Zero —
`simple-first-building` (the complexity-ladder / civil-law governing skill)
is in scope alongside whatever specialist skill it points you to, whenever a
design decision (not a pure lookup) is being made.

If the router's keyword table doesn't resolve an ambiguity, `README.md`'s
"The skill library" table gives the same 33 skills grouped by category with
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
- **Appendix S (Source Check).** A skill may end with "Appendix S: Source Check", sections
  `S.1`, `S.2`, …: values read again in the books under `sources/`, each with book and
  place. When such a line changes a figure, correct the body section too and let it name
  the line; never leave the body and the appendix in disagreement. A section "Defaults of
  this library" inside the appendix holds choices that are **not** from a book and says so.
  The root router explains the wording (Confirmed / Typical / Defaults).
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
- **`sources/`** (maintainers only — **not distributed** with the public
  repo) holds the literature this library was distilled from. It is
  gitignored and was never committed; keep it that way — these are
  copyrighted books. If you have it, consult it for provenance when a figure
  looks wrong before changing it. Contributors without it should rely on the
  Appendix S citations (book, table/section, page) and open an issue instead
  of guessing.

## Adding a new skill

Follow the pattern of an existing skill closest to the new topic (frontmatter,
reality check, evidentiary tiers, `VERIFY` tags). Then:
1. Add it to the router's ([`skills/construction-skills-router/SKILL.md`](skills/construction-skills-router/SKILL.md))
   lookup table (and, if it changes a project-level sequence, the
   task-recipes section).
2. Add it to the matching category row in `README.md`'s "The skill library"
   table.
3. Add it to the `skills` array in `.claude-plugin/marketplace.json` (keeps
   `npx skills` / Claude Code marketplace / npm-sync discovery complete).

Install tooling: `package.json` (npm/bun git-URL install, `files` limited to
`skills/` + docs) and `.claude-plugin/marketplace.json` (plugin manifest) —
no build step, no dependencies; keep both in sync with the skill set.

## Reality check

**Nothing in this repository is construction-ready.** Member sizes,
reinforcement schedules, U-values and cost figures are planning-stage aids —
a licensed engineer/architect must review and sign off before real use, and
site-specific data (geotechnical investigation, current B-Plan, current
GEG/DIN edition) always overrides generic figures in these skills. See
`README.md`'s "Reality check" section for the full statement.
