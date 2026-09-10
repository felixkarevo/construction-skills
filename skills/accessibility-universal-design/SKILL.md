---
name: accessibility-universal-design
description: >
  Barrierfreies Bauen / design-for-all for DACH practice: anthropometric bases
  (wheelchair geometry, Bewegungsflächen 120x120/150x150 cm, clear floor 90x140,
  reach ranges), doors (lichte Breite 90 cm, thresholds ≤2 cm bevelled, handle
  heights 85-105 cm, closer forces), ramps (6% preferred / 1:12 max with VERIFY,
  landings, continuous handrails, edge protection), zero-step entries with drainage
  logic, corridors and turning geometry, stairs (two-sided handrails with extensions,
  vis-à-vis risers, 5-6.5 cm contrast nosing), sanitary (DIN 18040-2 style WC
  compartments, Haltegriffe geometry, Notruf seated+lying, curbless showers),
  lifts (EN 81-1 car sizes, EN 81-70 door widths, platform lifts EN 81-41, stair
  lifts), tactile guidance systems, signage/contrast (LRV ≥30 logic)/lighting for
  aging eyes, adaptable housing (altersgerecht, generationengerecht, rollstuhlgerecht),
  a floor-plan audit workflow with FreeCAD dimension queries, common-failure list
  and sign-off checklist. All German normative values are practice/reference values
  to VERIFY against current DIN 18040-1 (öffentlich zugängliche Bereiche) and
  DIN 18040-2 (Wohnungen); legal driver is the Landesbauordnungen' barrierfree
  clauses plus equality laws, per-Bundesland. Design guidance, never a compliance
  certificate.
---

# Accessibility & Universal Design (Barrierefreiheit) — DACH Practice Skill

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

Agent-neutral procedure skill for concept design, draft verification and review of
step-free, usable-for-all building design under the German-language regulatory
framework (Landesbauordnungen, DIN 18040 series, EN 81 lift series). German
regulatory and planning terms are kept in parentheses because submissions,
Baubeschreibungen and authorities communicate in German.

The former edition was anchored on US standards; those anchors are removed. What
is kept is the **universal anthropometric and geometric reasoning**, re-tagged
with German framework values (DIN 18040-1 publicly accessible areas, DIN
18040-2 apartments) where a mapping exists, and labelled **practice values —
VERIFY** where the German number is not re-derived from the norm text.

## 0. How to use this skill

Use this skill when the task involves ANY of:

- designing or auditing a house/apartment as **altersgerecht / generationengerecht /
  barrierefrei / rollstuhlgerecht** (four distinct quality levels — Section 3),
- zero-step entrance (Schwellenreduktion), ramp (Rampenanlage) geometry, door width
  decisions (lichte Breite), bathroom layouts for transfer from a wheelchair,
- corridor/turning geometry checks (Bewegungsflächen), reach-range checks for
  switches, sockets, handles,
- lift selection for wheelchair use (Personenaufzug, Hublift, Treppenlift),
- stair safety for old/unsteady users (handrails, contrast, risers),
- wayfinding, tactile guidance fields (Leitsystem/taktile Leitstreifen), signage,
  alarm for sensory-impaired users,
- an accessibility audit of a floor plan, with FreeCAD dimension queries,
- future-proofing decisions at design stage (wall blocking, stacked cupboards,
  door reserves) that are cheap now and impossible later.

**Siblings** (load them when the task crosses over):

| Skill | Overlap |
|---|---|
| `stairs-vertical-circulation` | Governing stair geometry (Auftritt/Steigung, podests, headroom, railing heights) — here only the accessibility/safety overlay |
| `building-regulations-permits` | Which Landesbauordnung applies, when barrierefreies Bauen is legally required, Baugenehmigung procedure, Abweichungen |
| `fire-protection-building` | Flucht- und Rettungswege widths/doors — fire rules and accessibility rules must both be satisfied on the same route |
| `openings-windows-doors` | Door build-up, frames, lintels — here only the clear-width and operating-force logic |
| `building-services-tga` | Lift full design, sanitary engineering, alarm systems — here only the accessibility interface |
| `building-physics-thermal-moisture` | Illuminance/lux targets, glare and reflection physics, acoustics — here only the aging-eyes and low-vision logic |
| `construction-freecad-bim` | Modelling mechanics, spreadsheets, IFC export — here the accessibility-specific verification objects |

## 1. Reality check (read before producing anything)

1. **This skill produces design aids and planning/FreeCAD-modelling guidance
   only.** Nothing here is an execution document. Every dimension, ramp run, grab
   bar height is for preliminary layout, feasibility and 3D/BIM modelling.
2. **German building law is Land law.** The Musterbauordnung (MBO) is a model;
   each Bundesland's Landesbauordnung (LBO) has its own clause on **barrierfreies
   Bauen** — typically requiring that buildings with more than a defined number of
   dwellings and with lifts be barrierfree in a defined share of units and in the
   common areas, and that publicly usable buildings (Versammlungsstätten,
   schools, shops, doctors' offices…) be barrierfree throughout. The exact
   thresholds, and whether DIN 18040-1 or -2 is the introduced technical rule,
   differ per Bundesland. **VERIFY against the actual LBO and the current edition
   of DIN 18040; never cite "the law" from this skill.**
3. **Equality laws drive public-sector buildings.** Behindertengleichstellungsgesetze
   (BGG of the federation and the Länder) and municipal bylaws push barrierfreiheit
   for publicly funded or publicly operated buildings; accessibility concepts
   (Barrierefrei-Konzept, sometimes with a Beirat) are becoming a planning condition
   for public projects. Conceptually: public money → public requirement. Details
   per Bundesland — VERIFY.
4. **Austria and Switzerland have parallel frameworks** (ÖNORM B 1600 in AT; SIA 500
   "Hindernisfreie Bauten" plus the BehiG equality law in CH). Same design logic,
   different numbers and legal triggers. If the project is not in DE, re-anchor —
   do not silently apply DIN values.
5. **Never claim legal compliance.** This skill can say a design *follows the
   dimensional practice of* DIN 18040. Only a plan examiner / Bauaufsicht /
   staatlich anerkannter Sachverständiger can attest compliance, and a
   Vorlageberechtigter must sign the drawings. If a client needs a certificate or
   a KfW "Altersgerecht Umbauen" / "Wohngebäude — barrierfree" style funding
   confirmation, that is a human specialist referral, full stop. (Funding programme
   names and criteria change annually — VERIFY current programme guidelines.)
6. **Widening a doorway is a structural act until proven otherwise.** Any opening
   enlarged in a load-bearing wall needs a new lintel (Sturz) sized by the
   structural engineer (Tragwerksplaner); a lift pit is an excavation touching
   waterproofing and the foundation. Flag every such change.
7. **Accessibility dimensions never override escape-route or fire-protection
   requirements on the same element** — a door must satisfy both lichte Breite for
   wheelchairs and Fluchtweg rules (opening direction, wirksame Breite per
   fire-protection-building). Check both.
8. **Say the limits unprompted.** If the user's language suggests they are treating
   output as final ("send to the Bauträger", "is this DIN certified?"), state the
   signing + approval requirement in that message. Label deliverables
   `ENTWURF – NICHT AUSFÜHRUNGSREIF – barrierefrei-Maße nach Praxis-/Referenzwerten,
   Prüfung gegen DIN 18040 aktuelle Fassung erforderlich`.

## 2. Knowledge tiers

Every number in this skill carries a tier tag. Use the tag when quoting it.

| Tag | Meaning | Trust |
|---|---|---|
| **[DIN-practice]** | German framework value mapped from DIN 18040-1/-2 concepts or the digested EN 81 / installation-zone tables | Solid German practice, but the digests are thin on this standard — **VERIFY against the current DIN 18040 text before any submission** |
| **[PR-VERIFY]** | Practice/reference value retained from the previous edition of this skill (universal anthropometric origin) | Geometrically/ergonomically sound; present as good-practice target, not as a norm value |
| **[UNIV]** | Universal anthropometric or mechanical logic (a wheelchair is 70 cm wide everywhere; a fist needs the same force everywhere) | Safe to reason with; safe to defend to a client |
| **[HEUR]** | Rule of thumb, comfort target | Concept-stage only |

Symbols: Lichte Breite (lb) = clear opening width; OKFF = finished floor level;
LRV = light reflectance value; Bewegungsfläche = manoeuvring space.

## 3. Terminology — four quality levels, three legal triggers

The German-language debate distinguishes quality levels; mixing them up is the
most common client conversation failure:

| Level | German term | Meaning | Typical trigger |
|---|---|---|---|
| 1 | **barrierearm / schwellenreduziert** | reduced thresholds, no steps at the main entry, wide-ish doors; the "visitability-like" minimum for a private house | Voluntary; resale/ageing argument |
| 2 | **altersgerecht / generationengerecht** | usable by all ages without assistive devices: handrails both sides, good light, no trip hazards, reachable controls — but no guaranteed wheelchair turn in every room | Voluntary; many LBA/Baugesellschaften clauses |
| 3 | **barrierefrei (nach DIN 18040)** | designed so people with disabilities have no difficulties: Bewegungsfläche ≥120×120 cm [DIN-practice], routes ≤6% [DIN-practice], lichte Breite ≥90 cm [DIN-practice] | Legal in many LBOs for the common parts and a share of units in lift-served multi-dwelling buildings; legal for most publicly accessible buildings (DIN 18040-1) |
| 4 | **rollstuhlgerecht (nach DIN 18040-2)** | the higher apartment standard: Bewegungsfläche ≥150×150 cm [DIN-practice], WC side transfer space, door widths that allow full transfer — the "wheelchair user dwelling" tier | Legal for a defined share of units in some Bundesländer; contractual in Bauträger contracts; the target for a known wheelchair-user occupant |

**Scope decision tree — run first:**

```
What is the building / brief?
│
├─ Private one/two-family house, no named wheelchair occupant
│  → Level 1-2 (barrierearm + altersgerecht). Sections 5-14, cost impact at
│    design stage ~0-1.5 % of build cost. Do NOT overbuild: full Level 4 in a
│    bungalow for an ambulant client produces bathrooms like hospital rooms.
│
├─ Private house, occupant IS or WILL BE a wheelchair user
│  → Level 4 (rollstuhlgerecht) in the rooms they use, upper bound of every
│    range, Bewegungsflächen audit in EVERY room (Section 20). Measure their
│    actual chair: a mid-wheel-drive power chair turns in 150 cm; a rear-wheel
│    drive chair with elevating legrest does not. Design to the person.
│
├─ Apartment building with Aufzug (lift)
│  → Common areas: Level 3 minimum in most LBO regimes [VERIFY per Bundesland].
│    Units: check the LBO share (often a fraction barrierefrei, some
│    rollstuhlgerecht) + KfW/funding standard if the client wants the loan
│    bonus. Consultant project at execution stage.
│
├─ Publicly accessible building (shops, Praxis, school, Versammlungsstätte…)
│  → Level 3 per DIN 18040-1 territory (Sections 5-16 in full) + Barrierefrei-
│    Konzept if required. Escalate: human Bauberater für Barrierefreiheit.
│
└─ Existing building retrofit / UMBAU
   → Sections 6.5 and 18 decision trees; Denkmalschutz and Abstandsflächen
     frequently defeat the textbook ramp.
```

**Rule: default to Levels 1-2 for a family house.** Full DIN 18040 depth is for
levels 3-4 projects. If asked for "barrierefrei" on a private home, ask once what
actually drives it (a resident? a caregiver? resale? funding?) before escalating.

## 4. Why the cheap-now list exists

The three things that are **impossible or brutally expensive to add later** — and
therefore the non-negotiable core of any residential brief:

| # | Requirement | Target | Cost designed in | Cost retrofitted |
|---|---|---|---|---|
| 1 | **One step-free entrance** from street/garage | threshold ≤2 cm bevelled, ideally 0 [DIN-practice] | ~0 (grading + plinth decision) | high (ramp eats Abstandsflächen, Section 6.5) |
| 2 | **Wide doors on the ground floor** | lichte Breite ≥90 cm [DIN-practice] → leaf ~100 cm | ~1-3 % of door budget + wall geometry | high — structural (new Sturz) |
| 3 | **One ground-floor bathroom usable from a chair** | Section 11 layout | low (plan decision) | very high (drainage, waterproofing, space) |

Everything else — grab bars, lever handles, raised sockets, motion lights — can be
retrofitted cheaply. These three cannot. They are the "visitability triad" of the
old edition, now expressed in German framework numbers.

## 5. Anthropometric bases — what a wheelchair physically needs

All values metric-first. Human-body and wheelchair geometry is universal [UNIV];
the *required* spaces are the German practice values.

### 5.1 Wheelchair geometry [UNIV]

| Parameter | Manual chair | Power chair (mid-wheel) | Power chair (rear-wheel) |
|---|---|---|---|
| Width incl. wheels/knobs | 62–70 cm | 65–75 cm | 70–80 cm |
| Length incl. legrests | 110–125 cm | 120–135 cm | 135–150 cm+ |
| Seat height (sitzhöhe) | 48–52 cm typical, 43–48 common range [UNIV] | +tilt/recline | +lift platforms |
| Turning radius (space needed) | ~140–150 cm | ~140–150 cm (zero-turn class) | 160–175 cm |
| Reach forward, seated | 38–120 cm band OK; max ~85 cm touching forward [UNIV] | — | — |
| Max lateral reach across body | ~55 cm [UNIV] | — | — |

**Consequences for design (all [UNIV], defensible anywhere):**

- A parked chair needs a **clear floor space of 90 × 140 cm** minimum in front of
  or beside every fixture, appliance, control, work surface (the old edition used
  76×122 cm; 90×140 is the wider German-leaning reservation — [PR-VERIFY], use it).
- Passing a 90 cm door through a 90 cm passage puts hands at the hinge edge —
  approach geometry (Section 8.3) matters as much as width.
- Transfer height logic: a seated user's seat top is 48–52 cm; a WC seat of
  46–48 cm [DIN-practice, VDI 6000-1] makes lateral transfer nearly level. Below
  43 cm the transfer becomes a lift; above 52 cm it becomes a drop.

### 5.2 Bewegungsflächen (manoeuvring spaces)

| Space | Size | Where | Tag |
|---|---|---|---|
| Bewegungsfläche **barrierefrei** | **120 × 120 cm** | in front of doors, fixtures, work surfaces; apartment quality level 3 | [DIN-practice] |
| Bewegungsfläche **rollstuhlgerecht** | **150 × 150 cm** | every room the chair must turn in; apartment level 4 | [DIN-practice] |
| Turning circle (older/alternate convention) | Ø 150 cm | equivalent to the 150×150 square; overlaps with fixtures allowed only if the square stays clear elsewhere | [PR-VERIFY] |
| T-turn alternative | 150×150 T, arms ≥90 cm wide × 150 long, base ≥60 deep | where the full square will not fit | [PR-VERIFY] |
| Restfläche (passing space) | 150 × 150 cm at intervals on long routes; two chairs pass | corridors in public buildings | [DIN-practice] |
| Overlap rule | Bewegungsflächen may overlap each other and the door swing area **if** the required clearance at each other fixture stays free | small bathrooms | [DIN-practice] |

Drop a physical box of these sizes into the FreeCAD model (Section 20) — never
eyeball a Bewegungsfläche on a 2D plan; fixtures, radiators and door handles
intrude.

### 5.3 Reach ranges [PR-VERIFY, re-tagged]

- **Forward reach, unobstructed, seated: 38–120 cm AFF** (top of an object you can
  still grasp from a chair ≈120–130 cm; a standing adult with restricted arm lift
  lands in the same band).
- **Side reach, unobstructed: 38–120 cm AFF**; across-body lateral max ≈55 cm.
- Over a **deep obstruction** (countertop front, machine shelf): the highest
  reachable point drops — keep daily-use items ≤85 cm where a counter deeper than
  55 cm stands in front. [UNIV logic; exact obstruction tables are in DIN 18040-1
  for public fixtures — VERIFY before commercial work.]
- **Knee clearance under a counter/basin**: height 68 cm clear, depth 50 cm+;
  toe space below that (old edition 68.5 cm/23+35 — same target rounded)
  [PR-VERIFY].

Design rule: **put every control a person needs daily into the 38–120 cm band** —
switches, sockets, thermostats, window handles, intercom, oven, hob controls,
microwave, coffee machine, alarm panel. This single band satisfies almost every
user: seated child, seated adult, stooping elder, standing adult.

## 6. Routes, surfaces, thresholds — getting in and across

### 6.1 Route geometry

| Element | Minimum | Preferred | Tag |
|---|---|---|---|
| Exterior accessible route clear width | 120 cm (public), 100 cm (residential) | 150 cm two-way | [DIN-practice]/[PR-VERIFY] |
| Interior route clear width | 105–120 cm | 150 cm at turns/junctions | [DIN-practice]/[PR-VERIFY] |
| Running slope, **not a ramp** ("Ramp" starts above this) | ≤6 % | 2–3 % for comfort + drainage | [DIN-practice] |
| Cross slope (all routes) | ≤2–3 % (drainage without tipping) | 2 % | [PR-VERIFY] |
| Surface | firm, stable, slip-resistant, joint-spaced ≤1.5 cm or joints filled | broom-finish concrete, unglazed tile; NOT loose gravel, NOT polished stone | [UNIV] |
| Gaps/gratings slots | ≤1.5 cm in direction of travel (castor trap!) | orient bars perpendicular to travel | [PR-VERIFY] |
| Change in level | ≤2 cm, bevelled ≥1:2 above 0.5 cm; >2 cm counts as ramp step | 0 cm (level) | [DIN-practice]; old edition's stricter ≤0.5–1.3 cm target remains the better design goal [PR-VERIFY] |
| Headroom on route | 220 cm (225 cm over ramps/crossings in public practice) | 230 cm | [PR-VERIFY] |

### 6.2 The single most useful trick: regrade instead of ramping

**A surface at ≤6 % (in old edition terms: the 1:20 "not-a-ramp" idea maps to the
first ~2–3 % being imperceptible) is not a ramp** [UNIV logic, German slope values
[DIN-practice]]: no mandatory handrails, no landings as long as each run stays
within limits, no institutional look. If you have run available, grading the
approach at 3–6 % is almost always better than building a ramp with rails.

```
Typical Central-European plinth/Fussboden rise:      45-67 cm above terrace grade
→ 6 % route:   7.5-11 m run          → 12 % ramp:  3.75-5.6 m + landings + rails
→ 3 % route:  15-22 m run (driveway can carry it)  → split: regrade to +20 cm, short ramp for the rest
```

German sites raise finished floors 40–80+ cm over street/terrace for cellar
storeys and flood/winter reasons. That is a **large rise** to overcome in a single
ramp. Options in order of preference:

1. **Slope the driveway/courtyard itself** at ≤6 % toward the entrance — the car
   ramp doubles as the accessible route. Costs earthwork only.
2. **Enter from the garage level** (Untergeschoss rampe): where the garage floor
   is 15–25 cm below the ground-floor finished level, a short internal route or
   small Hublift solves the whole problem.
3. **Split the rise:** regrade 2/3 at ≤6 %, short ≤8 % run (≈1:12) + one landing
   for the last 15–25 cm.
4. **Full ramp** — Section 7. Watch the **Abstandsfläche**: a front ramp must not
   project into the setback or over the boundary without permission; ramps
   touching the façade line are often not verfahrensfrei — check
   `building-regulations-permits`.
5. **Hublift/platform lift** — only where run is unavailable (tight plots); adds
   a maintenance item, needs power + rain protection (Section 15).

### 6.3 Threshold detail (the part that actually gets built wrong)

```
Target: 0 mm. Acceptable: ≤20 mm total, every upstand bevelled ≥1:2 [DIN-practice].

Working detail for a step-free house entrance (German winter/rain reality):
  · Outside: paved Vorplatz a few mm BELOW finished floor, sloped ~2 % away
    from the door toward a drain
  · Threshold: flush or low-profile sill ≤2 cm, bevelled BOTH faces
  · Drainage: linear channel/slot drain immediately outside the sill, slots
    ≤1.5 cm perpendicular to travel — THIS is what lets you go flush without
    water tracking in or slush banking up
  · Door bottom: brush seal or drop seal, not a raised weather bar
  · Canopy deep enough to keep driving rain + snow off the threshold zone
    (120-150 cm+ projection on the exposed side)
  · Heated drip line / drainage keeps the slot from freezing shut in winter —
    a frozen flush threshold becomes an ice dam and the owner re-adds a step
```

Without the drain detail, the zero-step entrance floods or ices. That is why
builders default to a step; give them the drain and the objection disappears.

### 6.4 Surfaces underfoot [UNIV]

- Firm low-pile carpet (pile ≤1.5 cm on firm pad) is acceptable; deep pile, loose
  rugs and thick door mats are the most common in-house mobility hazard — a
  front caster catches on a 3 cm rug edge exactly like a 3 cm step.
- Transitions between floor materials: flush metal/wood transition strip, no
  T-bar lips. Plan the build-ups so the finished levels actually meet (screed
  heights, not trim).
- Slip resistance in wet areas: mineral matte surfaces or classified
  slip-resistant tiles (German classification: **R9–R13 per DIN 51130 shoe walkway
  test; A/B/C per DIN 51097 barefoot wet-area test**) — for accessible
  bathrooms specify **R10–R11 minimum** [DIN-practice]; polished tile in an
  accessible bathroom is a design failure.

### 6.5 Retrofit decision tree — existing house, no step-free entry

```
Is there ANY door with rise ≤ 15 cm from a paved area?
├─ YES → short ramp: ≤1.8 m run at ≤8 % + two 150 cm landings; check rail rules
└─ NO
   ├─ Garage/Untergeschoss entry within one storey? → Hublift at the garage
   │   level + internal route (often the ONLY legal answer on tight plots)
   ├─ Is there ≥ (rise × 17) of run at 6 %? → graded route, no rail obligation
   ├─ ≥ (rise × 12) + 3 m? → straight 8 % (1:12) ramp
   ├─ ~5 × 2 m rectangle? → switchback 1:12 ramp
   ├─ Denkmalschutz / street façade fixed? → internal solution: platform lift
   │   inside the entrance hall, or relocate the accessible entrance to the
   │   courtyard side (equity check: it must stay the EQUAL entrance, Section 19)
   └─ None of the above → vertical platform lift (≤1 m outdoors) or lift;
       modular aluminium ramps are removable, often genehmigungsfrei indoors —
       verify with the untere Bauaufsichtsbehörde before promising "no permit".
```

## 7. Ramps (Rampenanlagen)

### 7.1 Geometry

| Parameter | Value | Tag / note |
|---|---|---|
| Preferred running slope | ≤6 % (1:16.7) | [DIN-practice] — the German target for barrierefrei routes |
| Absolute max (short constrained runs) | ≤10 % over limited length; the old edition's 1:12 (8.3 %) remains the safe general design ceiling | [PR-VERIFY] — DIN 18040-1 uses stepped slope/length pairs — VERIFY before using >6 % in public work |
| Cross slope | ≤2–3 % | [PR-VERIFY] |
| Max rise per run before landing | 30–76 cm (6 % slopes force shorter runs; old 76 cm@1:12 is the steep-side cap) | [PR-VERIFY] |
| Clear width between rails | 120 cm public; 100 cm residential | [DIN-practice]/[PR-VERIFY] |
| Width for two-way / caregiver alongside | 180 cm | [PR-VERIFY] |
| Landing top + bottom | 150 × 150 cm min (full width if wider) | [DIN-practice] |
| Landing at direction change | 150 × 150 cm (90°/180° turn) — non-negotiable | [DIN-practice] |
| Landing slope | ≤2 % all directions — a sloped landing defeats the landing | [PR-VERIFY] |
| Edge protection (Restbord) | upstand ≥5–12 cm curb, rail downstand, or wall — stops a castor dropping off | [DIN-practice], old 5 cm min [PR-VERIFY] |
| Handrails required | both sides whenever it IS a ramp (>6 % or rise >~20 cm depending on Land rules) | [DIN-practice]/[PR-VERIFY] |
| Handrail height | 90 cm; second rail at 70 cm for children/short users where public | [DIN-practice] |
| Handrail extensions | run the rail ~30–40 cm horizontally beyond top and bottom of the slope and return to the wall/ground — the extension warns of the run end by feel | [DIN-practice]/[PR-VERIFY] |
| Handrail grip | 3–4.5 cm circular/oval, ≥4–5 cm clear of the wall, continuous graspability, no pinch points | [UNIV]/[PR-VERIFY] |
| Ramp surface | slip-resistant, joints ≤1.5 cm; avoid open grating on the path | [UNIV] |

**Worked example — 67 cm plinth, switchback ramp on a 6 m front court:**

```
Rise 670 mm. Straight 1:12 (8.3 %) = 8.04 m + 2×1.50 m landings = 11.0 m → fails 6 m.
Split: regrade court to −250 mm at 5 % over 5 m (driveway carries it).
Remaining 420 mm at 1:12 = 5.04 m → switchback of two 210 mm legs (2.52 m each),
turn landing 150×150 shared → footprint ≈ 5.5 m × 2.2 m → FITS.
Rails both sides of both legs, continuous around the turn landing, extensions at
the two open ends; ≥5 cm edge curb both sides.
```

Sanity check every ramp: **rise ÷ slope + landings ≤ available run**, and the
footprint against the **Abstandsfläche/street boundary**. If it fails, return to
Section 6.2 regrading — **never** steepen past the practice ceiling. The old
edition's "constrained-site 1:10/1:8 exceptions" are not imported: if forced to
>8 % on a retrofit, tell the client explicitly it is unsafe to self-propel and
needs assistance or a lift.

### 7.2 Drainage and winter (DACH reality)

- Ramps collect sheet water AND snowmelt at the top landing in front of the door —
  put the drain channel there, not at the bottom. A 6 % landing with 2 % cross-fall
  drains; never design 0 % on an unsheltered landing.
- Surface: brushed/ground finish, not sealed-smooth resin in shade; drainage mat
  under pavers so the ramp does not heave in frost.

## 8. Doors (Türen)

### 8.1 Clear width — the number everyone gets wrong

**Lichte Breite is the CLEAR width of the opening with the leaf open 90°, measured
from leaf face to the opposite stop/frame — not the leaf size, not the Rohbaumaß.**
A leaf loses roughly 6–10 cm to leaf thickness, stop and hinge offset [UNIV].

| Door | Approx. clear width | Verdict |
|---|---|---|
| 61 cm leaf | ~53 cm | storage only |
| 76.5 cm leaf (old interior default, DE "83.5 cm BA") | ~61–63 cm | **FAILS** accessibility everywhere |
| 88.5 cm BA (leaf ~83.5) | ~71–75 cm | fails the 90 target |
| 100.5/101 cm BA (leaf ~98.5) | **~85–90 cm depending on frame/stop** | marginal — must be measured in the model |
| Element with lb ≥90 cm (often 110 cm BA or offset-hinge 100.5) | ≥90 cm | **PASSES — specify as accessibility minimum** [DIN-practice] |
| Double leaf 2×61 cm | only active leaf counts | **FAILS** unless one leaf ≥ lb 90 alone |

German practice target: **lichte Breite ≥90 cm** on the accessible route, with the
old edition's universal caution that a 91.5 cm leaf only yields
~81.5–84 cm clear — **below** the German 90 target [UNIV + DIN-practice]. The two
conventions differ; do not mix them. Action rule:

> Specify doors by **required lichte Breite ≥90 cm**, then back-calculate the
> leaf/frame/BA. On a Level-1/2 house, at minimum the entrance door, the
> ground-floor bathroom door and one bedroom/store room get lb ≥90; everything
> else lb ≥80.5-style generous widths where walls are being planned anyway.
> [DIN-practice + PR-VERIFY]

Recovery tricks when lb 90 will not fit:
- **Vordersättige Bänder / offset (swing-clear) hinges**: leaf swings fully clear
  of the opening, recovering 4–5 cm — turns a marginal door into a passing one.
- **Pocket (Schiebelement) / sliding door**: clear width = full opening minus
  ~2.5 cm; the best answer for tight bathrooms and it removes the swing conflict.
  Specify a **D-pull, not a recessed finger cup** (closed-fist test, Section 13.1).
  Fire/escape: sliding doors are generally NOT allowed on Fluchtwege where the
  door must be immediately openable — check fire-protection-building.
- **Remove the door**: a cased opening ≥90 cm passes and costs nothing.

### 8.2 Operating behaviour

| Item | Target | Tag |
|---|---|---|
| Threshold at doors | 0 cm preferred, ≤2 cm bevelled max | [DIN-practice] |
| Opening force, normal doors | ≤25–30 N practice ceiling (old edition 22 N; door closer in Germany on flats mostly at entrance/UB doors) | [PR-VERIFY] |
| Closer swing time | ≥5 s from 90° to latch if a closer is fitted | [PR-VERIFY] |
| Hold-open | electromagnetic hold-open at accessible entrances; no manual "prop it" | [UNIV] |
| Locking | lever/Hebel or panics operable with closed fist, ≤ one tightening grip | [UNIV] |
| View panel in door | glazed section with lower edge ≤85 cm so a seated user sees the corridor | [PR-VERIFY] |
| Door leaves on accessible WC | **open outwards or slide** — a fallen person must not be trapped against an inward swing, and the swing must not eat the Bewegungsfläche | [DIN-practice] |

### 8.3 Maneuvering clearance (Bewegungsfläche vor Türen)

The clear width is useless if a chair cannot line up on the handle side.

**Universal approach rule (the residential shortcut):** provide the door-front
Bewegungsfläche (120×120 barrierefrei / 150×150 rollstuhlgerecht [DIN-practice])
on the opening side, plus wall free of obstructions on the **handle side**:
**≥15 cm** ahead of the latch edge (pull side) and **≥50 cm** behind the hinge
side [DIN-practice — VERIFY direction/values against DIN 18040-1; the old edition
carried 46 cm latch-side, the German table mirrors the logic — VERIFY]. The
classic residential failure is a bathroom door hinged so it opens into a 90 cm
corner with zero handle-side wall.

- If the door is **power-assisted or push-button, or opens automatically**, the
  clearance shrinks to the closing-side reservation only. [PR-VERIFY]
- Angled approaches (corridor turning into the door) need the corridor geometry
  of Section 9.3, not just door clearance.

## 9. Circulation, corridors, obstructions

### 9.1 Widths and spaces

| Element | Minimum | Preferred | Note | Tag |
|---|---|---|---|---|
| Hallway clear width (DG house) | 100–105 cm | 120 cm | old 91.5 cm floor is below German practice | [DIN-practice]/[PR-VERIFY] |
| Hallway clear width (public/MB) | 120 cm (with Begegnungsnische 150×150 every ~15 m) | 150–180 cm | [DIN-practice] |
| Hallway with a 90° turn into a door | 120–150 cm at the turn | 150 cm | this is where 100 cm halls fail | [UNIV] |
| Turning space in every room used by the chair | 150 × 150 cm | more for large power chairs | [DIN-practice] |
| Clear floor at fixture | 90 × 140 cm | — | [DIN-practice]/[PR-VERIFY] |

**Corridor rule of thumb [UNIV]:** a 100 cm hallway that ends in a 90° turn into a
90 cm door **does not work** for most chairs (the footrest cuts the inside corner).
Either widen the hall at the turn, enlarge the door, or approach head-on. Model it
(Section 20.2), don't eyeball it.

### 9.2 Protruding objects and head room [UNIV logic, [DIN-practice] zones]

- Objects between 25 and 67 cm height are cane-detectable — allowed to protrude.
- Objects between **~67 cm and 220 cm AFF may protrude max 10–15 cm**; better:
  keep the route envelope (120–150 wide × 220–230 high) literally free.
- Below-stair (Treppenuntersicht): box in or rail off — the classic head-strike
  for a blind or inattentive user.
- Radiators, window sills projecting into the route, fire extinguisher cabinets,
  wall-hung basins outside the bathroom: all are route intrusions. Audit with the
  sweep solid (Section 20.3).

### 9.3 Floor-level discipline

- One finished level across the whole ground-floor accessible route: collect every
  Δh in the build-up table of the plan (Section 20.5). Any Δ >2 cm is a defect
  unless it is a designed ramp.
- Shower rooms on the route: the bathroom floor and shower floor share one level
  (Section 11.4).

## 10. Stairs — accessible-adjacent safety

An accessible route never uses stairs — but the house has them, and most users who
need the ramp also climb the stair at 70. **Altersgerecht overlay only**: for
governing stair geometry use `stairs-vertical-circulation`; derive no compliance
claim from this table.

| Element | Target | Tag |
|---|---|---|
| Steigung/Auftritt uniform | no variation at all within a flight; comfortable envelope 16–19 / 26–30 cm, resolve per Blondel 2s+a ≈ 62–65 cm | [PR-VERIFY] + `stairs-vertical-circulation` |
| Offene Setzstufen (open risers) | avoid — toe and cane catch | [UNIV] |
| Belag contrast | every tread edge visually contrasting; **anti-slip strip/nosing 5–6.5 cm** with LRV difference ≥30 (Section 14) | [DIN-practice]/[PR-VERIFY] |
| Handläufe | **both sides**, height 90 cm (110 where required by railing rules), continuously past the top and bottom step | [DIN-practice] |
| Handrail extensions | continue ≥ one tread-step + ~30 cm horizontally beyond the last riser at bottom; horizontal or safe-return at top; always **return to wall or floor** at the ends (no clothing-catch open ends) | [DIN-practice]/[UNIV] |
| Handrail grip | 3–4.5 cm round/oval, ~4–5 cm clear of wall, uninterrupted by newel posts | [UNIV] |
| Second child rail | ~70 cm where used by children | [DIN-practice] |
| Zwischenpodest | every ≤18 steps (fewer is kinder to old legs); landing depth ≥ the stair's lichte Breite, +150 where a door opens onto it | [DIN-practice]/[PR-VERIFY] |
| Windelstufen (winders) | avoid on the primary stair | [UNIV] |
| Beidseitige Treppenläufe (stair with central rail, two flights) | preferred for the frail — user never needs the open side | [HEUR] |
| Stair lighting + end signal | switched from BOTH ends, tread-lit no glare; first/last step carry tactile+colour change AND handrail extension | [PR-VERIFY]/[UNIV] |

## 11. The barrierfree bathroom

The bathroom is where accessibility either succeeds or becomes a clinical room.
Level-1/2 houses need **one** ground-floor bathroom usable from a chair — not every
bathroom hospitalised.

### 11.1 Which bathroom, and how big

- Ground floor, on the step-free route, reachable without passing through a
  bedroom if it is the guest/all-flat WC.
- If the house has a ground-floor bedroom (Section 18.3), the ideal is one
  bathroom serving both — a single barrierfree room doing two jobs.

| Layout | Size | Use | Tag |
|---|---|---|---|
| **Barrierefrei half-bath** (WC + basin, 120×120 Bewegungsfläche, door out/independent) | ~150 × 200 cm room min depending on arrangement | Levels 1–3 | [DIN-practice]/[HEUR] |
| **Rollstuhlgerecht WC compartment** (150×150 inside, side transfer both sides or 90×70 + 30 beside WC per digest convention) | **≥160 × 230 cm** typical with basin; door ≥90 lb, out-swing/slide, lock releasable from outside | Level 4 | [DIN-practice] |
| **Rollstuhlgerecht full bath** (WC + Dusche + Waschtisch, 150×150 turning, overlap allowed) | ~6.7–7 m² practice | Level 4 with shower | [DIN-practice] + [HEUR] |
| Additional bathroom rule: wheelchair-user apartments **>3 rooms** need a second barrierfree bathroom (or at least WC+Waschbecken reserve) | — | Level 4 | [DIN-practice] |

The old edition's parallel-approach half-bath (door at the end of a 90×150
strip; chair enters, transfers sideways, backs out, cannot close the door from
inside) survives only as a **barrierarm** retrofit last resort. [PR-VERIFY]

### 11.2 WC zone

| Item | Value | Tag |
|---|---|---|
| Seat height (WC-Sitzhöhe) | 46–48 cm OKFF (comfort/transfer band 43–52 cm) | [DIN-practice, VDI 6000-1] + [UNIV] |
| Side clearance for transfer | Bewegungsfläche beside WC: 90 × 70 cm minimum reservation + 30 cm opposite (digest convention), full 150×150 where rollstuhlgerecht | [DIN-practice] |
| Haltegriffe (support handles) beside WC | pair of grab bars **flanking the WC, ~65–70 cm apart, each extending ~15 cm past the WC front edge, mounted ~28 cm above the seat line** — i.e. the classic L/pair geometry: seat-to-bar relationship is what matters, not absolute height (≈85 cm AFF results) | [DIN-practice, digested] |
| Grab bar diameter/clearance | 3–3.5 cm, ~4 cm clear of wall, smooth continuous surface | [UNIV]/[PR-VERIFY] |
| Grab bar load | design the fixing zone for **≥1.1 kN point load in any direction** — this is a structural practice value, not a norm quote; it is why blocking matters (18.1) | [PR-VERIFY] |
| Paper dispenser | reachable from the seat, 40–50 cm ahead of the seat front | [UNIV] |
| WC flush | large paddle/plate on the side reachable from the seat, or sensor with manual backup; not a small chrome button behind the bowl | [UNIV] |

**Door swing rule [UNIV]:** the door must not swing into the required
Bewegungsfläche. In a small house bathroom there is never the extra clearance —
so **out-swing or slide**. Out-swing also lets a fallen occupant's door be opened
from outside. Pair with a lock that opens from outside in emergency.

### 11.3 Washbasin (Waschtisch)

| Item | Value | Tag |
|---|---|---|
| Rim height | ≤80–85 cm OKFF (rollstuhlgerecht ≤80) | [DIN-practice, VDI 6000-1] |
| Bowl depth | ≤15–16 cm so knees pass under | [UNIV] |
| Basin depth | ≤50–65 cm (digest: rollstuhlgerecht ≤65) | [DIN-practice] |
| Mounting | wall-hung, no pedestal, no fixed vanity box underneath | [UNIV] |
| Knee/toe space | knee 68 cm high × ~50 deep; toe space below recessed | [PR-VERIFY] |
| Siphon/hot supply | insulated or boxed — **leg burns are a real seated-user injury** | [UNIV] |
| Tap | Einhebelmischer (single lever) or touchless; lever projects forward so a closed fist/wrist works it | [UNIV] |
| Mirror | tilted or bottom edge ≤~105 cm so a seated face is visible; full standing coverage not required | [PR-VERIFY] |
| Vorwand/cistern niche | ≥11.5 cm deep for flat cistern — reserve in the build-up | [DIN-practice] |

### 11.4 Barrierfree shower (bodengleiche Dusche)

The German norm-adjacent standard detail — **die befahrbare, bodengleiche Dusche**:

| Item | Value | Tag |
|---|---|---|
| Shower Bewegungsfläche | 150 × 150 cm rollstuhlgerecht; 120 × 120 barrierefrei | [DIN-practice] |
| Useful niche size | ≥90 × 110 cm inside face | [DIN-practice, digest] |
| Threshold | 0 cm — floor-level entry, continuous waterproofed floor | [DIN-practice] |
| Floor fall | 1–2 % toward drain (digest: 1 % low / 2 % normal water load); never >2 % so a chair does not drift | [DIN-practice] |
| Drain | linear channel or point drain ≥10 cm from the wall; slotted grating slots ≤1.5 cm oriented across travel, or hinge-lift without slot hazard | [DIN-practice]/[UNIV] |
| Waterproofing upstand (Verbundabdichtung logic) | ≥15 cm up all walls, ≥20 cm above outlets/spray zone — plan the whole wet room as a tanked level surface | [DIN-practice] |
| Duschhocker (shower seat) | folding wall seat, ~150 cm in front of the operating side, seat 46–50 cm high, load-rated like grab bars | [DIN-practice]/[PR-VERIFY] |
| Controls | offset toward the seat/entry, ≤120 cm AFF, Hebel or thermostat with **Verbrühschutz locked 38–40 °C** (pain ~40, scald ≥50 — [UNIV]) | [DIN-practice]/[UNIV] |
| Hand shower | on a ~150 cm hose, in a holder reachable seated, slide bar preferred | [PR-VERIFY] |
| Haltestangen | L-shaped or paired grab bars at entry and seat wall | [UNIV] |
| Floor | R10 minimum (R11 public), matte, no dark-and-glossy "hotel look" | [DIN-practice] |
| Privacy | Dusch-WC or towel hooks must not intrude into the swept turning square | [UNIV] |

**Slab note (buildability — a design-stage decision that must reach the
Schalplan/statik):** level entry needs either (a) a recessed slab zone (dropped
shutter — free if planned, impossible after casting), (b) a **Duschrinne** with
single-direction 1:80–1:100 fall, or (c) a shallow integrated-trap waste laid in
the screed. Existing buildings: raise the whole bathroom + ≤2 cm bevelled entry.
Membrane per the wet-room system — no shortcuts on upstands.

### 11.5 Bath tubs

A tub is not part of the accessible route. If retained: rim 45–60 cm, low-entry
option 35–45 cm [DIN-practice, digest], grab bars, and a transfer bench — and tell
the client the curbless shower is the actually-usable option for ageing in place.
A future raised-platform soaking tub is possible — reserve the static load and
drainage position if the client is undecided [HEUR].

### 11.6 Emergency alarm (Notruf)

- Every barrierfree sanitary room: **ZugNotruf (pull-cord alarm) operable from the
  floor** — a fallen person lies down, so the cord must reach ~10 cm above the
  floor and release/reset from the plug end. [DIN-practice: required in public
  barrierfree WCs and in rollstuhlgerecht Wohnungen per many LBOs — VERIFY]
- Alarm must be confirmable **seated AND lying** [DIN-practice].
- In multi-unit buildings: alarm routes to a central panel or agreed contact;
  test-and-maintenance responsibility belongs to TGA — see
  `building-services-tga`.

## 12. Kitchen and utility (light-touch residential)

Commercial kitchen compliance is public-building work; for a house the
high-value low-cost moves [PR-VERIFY unless tagged]:

| Item | Target | Why / cost |
|---|---|---|
| Clear floor between opposing counters | ≥120 cm; **150 cm if U-shaped** (chair must turn) | layout only [DIN-practice] |
| Turning space | 150 × 150 somewhere in the kitchen | layout only [DIN-practice] |
| One work stretch knee-free | 85 cm high surface with 68 × 50 knee void (removable panel/cutlery drawer front) | low |
| Sink | rim ≤85 cm, shallow bowl, insulated siphon, front ≤50 cm clear | low |
| Tap | single lever, pull-out spray | trivial |
| Hob | **controls front or side — never behind the burners** (reaching over active burners seated = burn risk [UNIV]); induction lowers burn risk further; staggered zones help seated reach | trivial at spec |
| Oven | wall oven with seat-height top and hinged/slide door, adjacent landing surface ≥90 cm | moderate |
| Dishwasher / small appliances | door opening must not block the transfer route; appliances in the 38–120 cm band or on a pull-out shelf — not at 180 cm | low [UNIV] |
| Storage | pull-out drawers/lifts instead of deep cupboards; **D-pulls, not knobs**; one full-extension pantry pull-out | low |
| Outlets | on the counter apron front or ≥45 cm AFF wall sockets | trivial |

## 13. Hardware, controls, electrical

### 13.1 The closed-fist test [UNIV]

**Every control must work with one hand, closed fist, no pinching/twisting; ≤ ~25 N
operating force.** (Same logic on both sides of the Atlantic; the force number is
practice, VERIFY for public work.)

| Passes | Fails |
|---|---|
| Hebel/Türgriff (lever handle) | Rundknopf (round knob) |
| D-pull cabinet handles | small knobs, recessed finger cups |
| Einhebelmischer (single lever) | cross-head twin taps |
| Wippschalter (rocker) | small toggle switches, twist dimmers |
| Push/touch, Knebel at 85 cm | key-operated, thumb-turns |
| Loop/wand-operable window handles | casement twist catches above 120 cm |

The cheapest whole-house accessibility upgrade in existence: at spec stage lever
hardware costs ~ the same as knobs.

### 13.2 Mounting heights

| Control | Normal practice | Accessible target | Tag |
|---|---|---|---|
| Lichtschalter | 105 cm | **85 cm OKFF, ≥50 cm from room corner / door reveal** (matches the DIN 18015-3 installation-zone logic for vertical chases near reveals) | [DIN-practice, digested] |
| Steckdose | 30 cm | **≥45 cm** bottom edge (old edition 46 cm — same target) | [PR-VERIFY] |
| Thermostat / heat-control / AC panel | wherever | ≤120 cm | [PR-VERIFY] |
| Door hardware (Griff) | 105 cm | 85–105 band already fine | [DIN-practice] |
| Fensterbedienung | wherever | ≤120 cm, or motorised | [PR-VERIFY] |
| Zähler-/Sicherungsfeld | high | main switches ≤120 cm | [PR-VERIFY] |
| Sprechanlage / doorbell / video | varies | 85–120 cm | [PR-VERIFY] |
| Rollladen / blind control | cord | motorised or wand ≤120 cm | [UNIV] |
| Rauchwarnmelder | ceiling (no height choice) | plus visual alarm unit for deaf users, Section 16 | — |

### 13.3 Installation zones (DIN 18015-3 logic) [DIN-practice, digested]

Keeping electrical lines in the fixed installation zones (horizontal bands near
ceiling/floor, vertical bands at reveal/corner offsets) is an accessibility
*enabler*: later grab bars and adaptation hardware can be screwed in anywhere
outside those bands without drilling through live conduits. Reserve the grab-bar
band during the rough-in anyway (18.1).

### 13.4 Reach band reminder

Everything used daily lives in **38–120 cm** (Section 5.3). Sockets, switches,
hob/oven controls, window handles, alarm panels, microwaves (on a pull-out),
broom cupboard hooks. Free at design stage; a carpenter's afternoon later.

## 14. Lighting, contrast, glare — for aging and low-vision eyes

### 14.1 Light level logic (cross-reference physics)

Illuminance targets, sizing and glare physics belong to
`building-physics-thermal-moisture` / lighting design; the accessibility kernel
[UNIV]: a 60-year-old needs roughly **2×**, an 80-year-old roughly **3×** the
illuminance of a 20-year-old for the same task, and handles glare far worse.
Therefore:

- **Task lighting everywhere it matters** (kitchen counter, stair, mirror,
  reading chair, WC transfer zone) — never one ceiling point per room. Bathroom
  practice anchor ~200 lx plus **shadow-free mirror-front lighting** (light at
  the mirror plane, not above the head) [DIN-practice, VDI 6000-1].
- **Night route lighting**: low-level motion light bedroom → bathroom — this
  single intervention prevents a large share of elderly night falls; switch or
  sensor ≤120 cm.
- Stair lighting switched at **both** ends; light the treads, no bare lamps in
  the descending sightline; no glossy floor reflections reading as "wet/ice".
- Flicker-free drivers; flicker/strobe is a seizure/vertigo trigger for some
  users [UNIV].

### 14.2 Contrast (LRV) [UNIV logic, [DIN-practice] target]

**Light Reflectance Value difference ≥30 points** between adjacent surfaces that a
low-vision user must distinguish:

- door leaf vs wall, door leaf vs frame
- switch/Socket plate vs wall
- sanitaryware vs wall and floor (white-on-white tile in a white room is
  functionally invisible)
- grab bar vs wall
- stair nosing vs tread (plus the 5–6.5 cm contrasting strip, Section 10)
- floor route vs wall base; furniture edge vs floor
- level changes, ramp starts, glass doors (rail/bar band + markers both faces)

Avoid: high-gloss floors (read as wet), busy high-contrast floor patterns (read as
level changes/barriers by older users and confuse white cane reflection), and
mirrors facing doorways.

## 15. Lifts and vertical aids (Aufzüge, Hublifte)

### 15.1 Passenger lift sizing (EN 81-1 / ISO 8100-30 car series) [DIN-practice, digested]

| Capacity | Car (breit × tief) | Fitness for purpose |
|---|---|---|
| 320 kg | 0.90 × 1.00 m | not wheelchair-useful (platform-lift territory) |
| 450 kg | 1.00 × 1.20 m | marginal; wheelchair user alone, tight turns in/out |
| **630 kg** | **1.10 × 1.40 m** | **the accessible minimum** — wheelchair + pram; front or rear wall transfer possible |
| 1000 kg | 1.10 × 2.10 m | stretcher + wheelchair; two-way chair traffic possible in some plans |

Supporting rules [DIN-practice, digested]:

- **Car door lichte Breite ≥90 cm** for accessible use (EN 81-70 logic);
  **≥110 cm** where two-way flow or bed/stretcher service is expected. Door
  height 2.0–2.1 m; car height max 2.2 m.
- **630 kg / 110×140 is the floor for any "barrierefrei" apartment-building
  promise** — a 450 kg car in a "generationenwohnen" brochure is a red flag.
- Car controls: buttons ≤110–120 cm band, braille + raised numerals, position
  display visual + **akustische Sprachansage**, door-reopening sensor spanning
  35 cm–1.5 m AFF. [PR-VERIFY + EN 81-70 logic]
- Vorhalle (lift lobby): 150×150 manoeuvring in front, door swing outside the
  car's turning space; tactile floor numbers at each landing door.
- Fire service: firefighter lifts and EN 81-73 recall/fire mode are
  fire-protection-engineered — never mix the accessible-lift brief with the
  Feuerwehraufzug brief without reading `fire-protection-building` first.

### 15.2 Platform lifts and stair lifts where a full lift won't fit [DIN-practice, digested]

| Device | Envelope | Use case |
|---|---|---|
| **Hublift / platform lift (EN 81-41)** | speed ≤0.15 m/s, ≤300 kg, platform ≥0.90 × 1.00 m (≤2 m²), guard rail 0.9 m, enclosure needs on travel side | entrance rises ≤1–3 m where ramp run is impossible; outdoor versions need frost/snow rating |
| **Treppenlift / stair lift (EN 81-40)** | ≤300 kg, folded 20–40 cm projection | single stair, named occupant; **must not reduce Fluchtweg stair width or headroom** — check escape rules + `stairs-vertical-circulation` |
| Residential machine-roomless lift | from ~1 m² shaft + pit | new-build duplex/MB; plan pit + headroom + power at design stage |

Rule [UNIV]: every mechanical vertical aid is a **maintenance commitment**
(Prüfintervalle, spare parts, power-failure rescue). Prefer graded routes and
ramps first, lifts last — except where the rise makes a ramp absurd.

## 16. Sensory orientation — guidance, signage, alarms

For public buildings (DIN 18040-1 territory) this is a full discipline; for
residential work, take the low-cost kernel. All dimensional values [PR-VERIFY].

### 16.1 Tactile guidance (for blind and low-vision users)

- **Tactile ground surface indicator logic [UNIV]**: warning pattern (truncated
  domes/blisters, cane- and foot-perceptible) across the direction of travel at
  hazards: stair top/bottom, ramp ends, driveway crossings, lift lobby
  thresholds. Directional bars parallel to travel along primary routes.
- German public practice: **taktile Leitstreifen + Aufmerksamkeitsfelder** per
  DIN 18040-1 logic, LRV contrast ≥30 to the surrounding floor — VERIFY before
  specifying on a public project; residential retrofits get the 80 % win from
  stair nosing contrast + a consistent handrail line + no protrusions.
- Tactile floor numbering at stair landings and lift lobby doors, raised +
  braille at ~140–160 cm on the latch-side wall.

### 16.2 Signage

- Two-mode minimum for every essential message: **visual + tactile/braille
  indoors; visual + acoustic at alarms** [UNIV — principle 4].
- Sans-serif, character height scaled to viewing distance (~15 mm per 1 m),
  LRV ≥30, non-glare; mounted latch-side or on the approach wall at 140–160 cm,
  never solely on the moving leaf; pictograms + colour zoning for non-native
  speakers and cognitive access.

### 16.3 Alarms for all [UNIV/[PR-VERIFY]]

- Audible alarm clearly above ambient (practice ≥ +15 dBA or ~75 dBA
  unmeasurable); visual flash 1–3 Hz synchronised (photosensitivity caution).
  Every barrierfree room type gets a **visual alarm device**; the bathroom
  pull-cord (11.6) is separate and complementary.
- Intercom at the accessible entrance: camera at ~120–150 cm lens centre,
  indoor screen 110–140 cm, adjustable audio.

## 17. Workplaces and public buildings — pointers only

For workplaces or publicly accessible buildings the tables above shift from
"targets" to "requirements" and three regimes attach — cross-referenced, not
duplicated: **Arbeitsstättenrecht (ArbStättV + ASR rules, DGUV)** for barrierfree
workplaces and sanitary counts (ASR-analogue WC cells ~100×120 cm with out-swing
doors, Vorraum logic — workplace version of Sections 9/11; VERIFY current ASR
edition); **special-buildings ordinances** (Versammlungsstätten, schools,
hospitals) for wheelchair positions in seating rows and hearing-support systems
(Induktionsschleife / digitaler Übertragungskanal, T-ear symbol); and public-transport/
outdoor rules (150 cm manoeuvre radii at stops). A public client always needs a
Barrierefreiheit consultant early — the fee is trivial next to post-approval
rework.

## 18. Adaptable and future-proof housing (altersgerecht umbauen)

The cheap-now / impossible-later list for a Level 1–2 house. This is where most of
this skill's residential value lives.

### 18.1 Grab-bar / rail blocking in EVERY bathroom, always

```
Continuous solid backing (30 mm board, noggin band, or fully grouted cavity in
masonry) at:
  · 80-95 cm OKFF band, ≥20 cm tall — covers the Haltegriff zone wherever the
    WC ends up after tiling
  · around the WC: rear wall full width + side wall ≥120 cm from rear wall
  · all shower/tub walls full length; beside the basin
Load target: any 10 cm-wide zone carries ≥1.1 kN in any direction [PR-VERIFY].
```

Cost at construction ≈ 0. Cost later: opening tiled walls and rebuilding the
waterproofing. **Never omit because "they don't need bars yet".** Suction-cup
"grab bars" are not grab bars — they never get specified.

### 18.2 Door and wall reserves

- Ground floor: every room door planned at lb ≥90 (or at least the wall position
  chosen so the opening can later grow without touching a corner or a wet wall).
- Bathroom door on the ground floor: reserve for **out-swing or slider**.
- First-floor doors lb ≥80 at least — a bed, a chairlift component, and a
  walker all pass through them.
- Non-load-bearing internal partitions in the bathroom zone: plan so the
  bathroom can merge with the adjacent bedroom later (the "hotel suite"
  adaptation) without cutting a Sturz.

### 18.3 Ground-floor bedroom and the lift reserve

- One ground-floor room **≥3.0 × 3.6 m usable**, near the barrierfree bathroom,
  sill ≤110 cm, double socket clusters at 45 cm on two walls, network point.
  Study/guest now; bedroom later.
- **Stacked cupboards (Schrankreservierung):** align a 140 × 140 cm clear closet
  over closet with a non-structural floor panel — a future lift shaft for the
  cost of drawing it in the right place; add a spare circuit + draw-wire conduit.
- Stair from day one: straight flight ≥100 cm (curved stair = 3–5× stairlift
  rail), solid handrail walls (not plasterboard alone), landings where a lift
  chair parks clear of the Fluchtweg.
- Ceiling over bed + WC: solid band for a **Deckenlift** — flag ~1.5 kN dynamic
  point load to the engineer, not to the tiler.

### 18.4 Other future-proofing

- Level or minimal-fall garage slab → the second step-free route. Night route
  bedroom→bathroom ≤6 m, straight, sensor-lit (14.1).
- Pre-wire for motorised blinds, app/voice control, entrance door automation
  (needs the 90 cm door + power at the leaf side).
- Thermostatic mixing valves at every hot draw point — protects children as much
  as elders [UNIV]. Reserve **Notruf** conduit from each bathroom even if no
  system is installed now.

## 19. Universal design principles — the seven tests

The codes are minimums; these seven widely-used principles are the design intent
behind them. Run every scheme through them before the dimensional audit:

| # | Principle | One-line test |
|---|---|---|
| 1 | **Equitable use** | Do everyone and the wheelchair user use the *same* entrance and *same* route? A side-yard "accessible entrance" at the bins passes dimension and fails design. |
| 2 | **Flexibility in use** | Left/right, fast/slow, seated/standing, strong/weak — lever handles, double-sided rails, height-adjustable desk stretch. |
| 3 | **Simple & intuitive** | Can a first-time visitor with no shared language find the way? Sightlines from decision points, consistent placement. |
| 4 | **Perceptible information** | Every essential message in ≥2 modes (see 16.2). |
| 5 | **Tolerance for error** | What happens when someone misjudges? Contrasting nosings, slip-resistant wet floors, rail returns, no 2 cm trip ledges, door closers that don't slam. |
| 6 | **Low physical effort** | Neutral posture, ≤25–30 N operating, no stair to reach the bin store, automatic door where flow demands it. |
| 7 | **Size & space for approach and use** | Clear sightlines, 38–120 reach band, Bewegungsflächen even in the "small" rooms — assisted and unassisted, seated and standing. |

## 20. Audit workflow — walking a floor plan (agent procedure)

Run in this order on any plan/model. Every query is a FreeCAD/spreadsheet check,
not an eyeball judgement. Pair modelling mechanics with `construction-freecad-bim`.

1. **Classify (Section 3 tree).** Write the chosen quality level (1–4) and the
   assumed user (ambulant / rollator / manual chair / power chair) into the
   project notes; every later judgement reads against that line. If unknown: ask
   once; default Level 2 + Level-4 bathroom reserve.
2. **Route graph.** Identify: street/garage → entrance → Flur → bathroom →
   kitchen → bedroom(s) → balcony. Export the route polyline; all following
   tests run on it.
3. **Door clear-width table (Section 8.1).** Parametrise, don't measure drawings:
   `lb = opening − 2×jamb − leaf offset − stop` (side-hung 90°: ≈ leaf − 60..100
   mm; offset hinges ≈ leaf − 15..25 mm; sliding ≈ opening − 25 mm). ASSERT
   lb ≥ 900 mm (Level 3/4) / ≥ 800 mm elsewhere. Store `lb` as a
   spreadsheet-driven property on every door so the check re-runs on every size
   change; report room | leaf | lb | pass/fail.
4. **Bewegungsflächen clash test.** Drop floor boxes in every required room:
   1500×1500×500 (Level 4), 1200×1200×500 (Level 3), plus 900×1400×500 parking
   boxes at each fixture/control/door-front-handle-side. Boolean intersection
   against walls, fixtures, radiators, door swings: non-empty = fail, name the
   offending object.
5. **Route sweep.** Sweep a 1200×2200 (public 1500×2300) profile along the route
   polyline; clash against everything — one operation catches narrow halls, the
   corridor-into-door turn (9.1), protrusions 67–220 cm (9.2), door swings,
   under-stair head strikes, radiator/window intrusions.
6. **Level audit.** Query every floor/slab object's Z along the route; list any
   Δ >20 mm between adjacent route surfaces. Report; never fix silently.
7. **Ramp/slope check (if any).** Verify `rise/run ≤ target` numerically — never
   from the view; landings ≥150×150 as separate flat solids; rails with
   extensions modelled as real swept solids (extensions get omitted); curb
   modelled; footprint against Abstandsflächen/Grenzlinie.
8. **Reach and hardware scan.** Batch-query: switches 85 cm, ≥50 from corner;
   sockets ≥45; handles 85–105; shower/hob/oven controls ≤120; mirror bottom
   ≤105; alarm cord down to ~10 above floor. Anything outside → defect list.
9. **Contrast/lighting notes.** LRV ≥30 pairs (14.2) and task-light placement
   are a finish-schedule annotation check, not a solid clash. Flag any
   single-source room on the route.
10. **Report.** Deliver: chosen level + user assumption, PASS/FAIL per step,
    defect list with object names, cost-flagged changes (structural widening,
    slab recess, lift), and the Section 1 deliverable label. Structural impacts
    of widened openings, lift pits, hoist anchors go **in writing** to the
    engineer.

## 21. Common failures

1. **Interior doors planned at the local default (76.5/88.5 cm BA)** — clear
   width 61–75 cm; the single most common defect. Specify lb ≥90 by calculation.
2. **Quoting "90 cm door" for the Rohbaumaß or leaf instead of lichte Breite** —
   the 6–10 cm loss re-appears as a failed audit at handover.
3. **Ramp without a level landing at the top** — user must hold on the slope
   while operating the door; and **ramps built into the Abstandsfläche or over
   the boundary** without checking — refused or removed at approval.
4. **In-swinging bathroom door** eating the Bewegungsfläche — and trapping a
   fallen occupant. Same family: a 100 cm hall turning 90° into a 90 cm door,
   which geometrically fails (9.1).
5. **Grab bars in plasterboard/hollow block without blocking** — they pull out
   under exactly the load they exist for. Suction cups are not grab bars.
6. **Polished large-format tile in the accessible bathroom** ("hotel look") —
   specify R10/R11 matte.
7. **Bodengleiche Dusche decided after the slab is cast** — then a 5 cm lip
   appears or the whole floor rises and headroom dies. It is a Schalplan decision.
8. **Zero-step entry without drainage** — water/slush enters, owner re-adds a
   step in spring, accessibility lost.
9. **Switches at 105 cm crammed behind the door leaf against the corner** —
   violates both the 85 cm target and the ≥50 cm reveal reservation.
10. **Uninsulated basin siphon; hob controls behind the burners** — the two
    seated-user burn hazards.
11. **A 450 kg lift advertised as "barrierefrei"** — wheelchair users can't turn
    in it; the honest minimum story is 630 kg / 110×140.
12. **Foreign-standard thinking** — citing or claiming a non-German accessibility
    standard on a German project; only DIN 18040-territory practice plus the LBO,
    verified by the Bauaufsicht, answers the question.
13. **Contrast saved for "later decoration"** — white-on-white sanitaryware,
    invisible nosings, unmarked glass doors are a built-in failure; and treating
    the bathroom as the only requirement while the route to it has a 3 cm joint,
    a 5 kg door and a knob handle.
14. **Forgetting that fire and access rules share the same doors**: an out-swing
    barrierfree WC door, a sliding entrance door on the Fluchtweg, a stairlift in
    the Treppenraum — each needs BOTH rule sets checked.

## 22. Sign-off checklist (residential, Level 2+3 hybrid — adapt for Level 4)

```
LEVEL & DOORS
[ ] step-free entrance: threshold ≤2 cm (target 0, bevel ≥1:2) + drain detail
[ ] route grades ≤6 %; cross fall 2 % drains; all level changes ≤2 cm; no rugs
[ ] lb ≥90 cm calculated (not leaf size!) at entrance/bathroom/service rooms;
    lb ≥80 cm elsewhere ground floor; handle-side wall reservation kept
[ ] bathroom door out-swing/slide with emergency release; force ≤~25-30 N;
    closers ≥5 s; lever handles throughout

CIRCULATION
[ ] halls ≥100-105 cm; ≥120-150 cm at 90° turns into doors
[ ] Bewegungsfläche 120/150 modelled + clash-free in every required room
[ ] no protrusions 67-220 cm on route; under-stair boxed; 90×140 at every
    fixture, control, appliance position

SANITARY (ground floor, at least one)
[ ] 150×150 (L3: 120×120) with door swing excluded
[ ] WC seat 46-48; Haltegriffe pair 65-70 apart, 15 past front, ~28 above seat;
    blocking band 80-95 cm all bathroom walls, ≥1.1 kN zone
[ ] basin ≤85 (L4 ≤80), knee void, insulated siphon, lever tap
[ ] bodengleiche Dusche ≥120×120 (L4 150×150), 1-2 % fall, Rinne, R10/11,
    thermostatic 38-40 °C lock, folding seat on blocked wall
[ ] Zugnotruf reaching near floor, confirmable seated AND lying; mirror lighting

CONTROLS & SENSORY
[ ] switches 85 cm ≥50 from corners; sockets ≥45; daily controls in 38-120 band
[ ] night sensor light bedroom→bathroom; stair light both ends, no glare
[ ] LRV ≥30 pairs in finish schedule (door/wall, nosing, fixtures, rails)
[ ] alarm audible AND visible in occupied rooms (public: + tactile signage)

FUTURE-PROOF & DELIVERABLE
[ ] ground-floor bedroom ≥3.0×3.6 near bathroom, sill ≤110 cm
[ ] stacked 140×140 lift reserve + circuit + conduit; straight stair ≥100 cm;
    hoist band over bed+WC flagged to engineer; mixing valves at draws
[ ] Ø1500/150×150 clash test + 120×220 route sweep passed end to end
[ ] ramp numerically verified, landings/rail extensions/curb modelled
[ ] labelled ENTWURF – NICHT AUSFÜHRUNGSREIF – VERIFY DIN 18040 (aktuelle Fassung)
[ ] structural impacts in writing to engineer; L3/4 public/MB projects:
    Barrierefreiheit consultant engaged early
```

## 23. What this skill is not

Design guidance for barrierfree concept and layout. It certifies nothing — the
DIN 18040 paragraph values, each Bundesland's trigger thresholds and funding-
programme criteria all move; every [DIN-practice] figure is a digested practice
value to re-verify against the current norm text and local Baurecht by an
authorised person before submission. Level 3/4 public projects need a human
Barrierefreiheit specialist; execution documents need signing professionals;
construction needs the Baugenehmigung — see `building-regulations-permits`.
