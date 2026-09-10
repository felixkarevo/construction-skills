---
name: construction-scheduling-site
description: >
  Bauablauf & Baustellenorganisation for residential builds in the DACH region:
  the standard sequence for a house (Baustelleneinrichtung → excavation/
  Baugrube → Kellersohlplatte/substructure → shell/Rohbau per storey → roof &
  weather-tight → fit-out/Ausbau → Abnahme) with typical phase durations;
  duration estimation from digested crew-productivity tables (LSA
  Lohnstundenaufwandswerte: formwork h/m², rebar h/t, concrete h/m³ per unit,
  derived m²/day crew outputs, 9-h-day convention); LSA/Gantt bar-chart
  practice and the schedule-plan ladder (Meilenstein-, Rahmen-, Grob-,
  General-, Koordinations-, Detailterminplan — who owns which); CPM network
  planning (Vorgangsknoten, EA/AA/EE/AE logic ties, FAZ/FEZ/SAZ/SEZ = ES/EF/
  LS/LF, Gesamtfloat/Freifloat = TT/FT/FZ/GF formulas + worked 18-day
  pipeline-trench example); flow-line Taktplanung (takt-time formulas, formwork
  set-count, weekly floor cycle, Produktions-Zeit-Diagramm); resource levelling
  (Mittelplanung, Belegschaftskurve, capacity-shortfall ladder); weather and
  seasonality (winter surcharge/Winterbaukosten, frost protection and concrete
  temperature rules per DIN EN 13670 practice, hot-weather concreting);
  site-layout planning (BE: crane radius and coverage, storage-area demand
  list, access/Baustraße rules, fencing, temporary facilities areas,
  mass-centre/working-field/road triangle); engineering survey support for the
  setting-out and as-built steps (§8A Ingenieurgeodäsie: coordinate/height
  systems & Projektmaßstab, polar method, Helmert transformation, free
  stationing, trigonometric height transfer, curve setting-out, accuracy
  classes & DIN 18710/18202 tolerances, control-point protection, as-built
  & deformation-monitoring basics, FreeCAD/IFC georeferencing); machinery selection (excavator
  classes, tower-crane sizing heuristics, mobile-crane classes, f-factors incl
  swell/Auflockerung, loading chain truck/bucket ratio, concrete conveying
  pump-vs-skip); shoring per DIN 4124 (unsupported-cut limits, surcharge
  setbacks, Verbau type matrix); site safety and OSH coordination (BaustellV,
  SiGeKo duties, RAB 30/31/32/33, Gefährdungsbeurteilung, TOP principle,
  first-aid ratios, side protection EN 13374, scaffold norms); quality
  supervision Eigen-/Fremdüberwachung and hold points; delay and VOB/B §6
  Behinderung claims logic (notice duties, schedule-linked narrative proof,
  Vorhaltekosten, idle-crew worked example); reporting and as-built
  documentation; programme checklists.
---

# Construction Scheduling & Site Organisation (Bauablauf & Baustelleneinrichtung)

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

A design package tells you *what* to build. A construction programme (Bauablaufplan) turns it into *when, with whom, with which machine, and at what cost per week of delay*. In European practice the difference between a house delivered on time and one that bleeds money for months is almost never the drawing — it is the schedule and the site setup behind it: crew sizes derived from real productivity values instead of guesswork, a shoring decision made before the excavator arrives, a tower crane positioned so nothing waits for hoisting, winter concrete planned with its surcharge priced in, and a daily-report discipline that makes every later claim provable.

This skill covers the execution-planning layer (Arbeitsvorbereitung, AV) between an approved design (or FreeCAD/BIM model) and a finished building: the canonical build sequence with durations, the two scheduling methods (bar chart and CPM network) with their formulas and worked examples, flow-line (Takt) planning, resource levelling, site layout, machinery selection, excavation support, site-safety coordination, quality supervision, and the delay/claims interface. Detailed trade-level execution sequences, hold points and finishing order sit in the companion `construction-scheduling-site` skill; this file focuses on **programmes, productivity numbers, plant, site organisation and coordination**.

## Reality Check — Liability & Planning Posture

**This skill produces planning aids, duration heuristics and calculation guidance for programming and FreeCAD/BIM modelling ONLY.**

1. Every duration, productivity value (LSA, GL), float, set count, crane capacity and shoring limit in this file is a **planning heuristic for first-pass programmes** — not a construction instruction. Crew-productivity values scatter strongly with site conditions, crew qualification, weather and motivation; they must be validated against your own experience (Nachkalkulation records) before being used to commit dates or money.
2. **Scheduling is not shoring, and plant selection is not a lift plan.** Excavation support beyond DIN 4124 simple cases, falsework (Traggerüst) design, crane foundations/anchoring, and load-rigging are **engineered, life-safety deliverables** by qualified persons (Tragwerksplaner, Kransteller, Gerüstnehmer), not table lookups. A tower crane's load chart at the actual radius of the heaviest pick governs; a heuristic count of cranes never does.
3. Contract-relevant statements — Bauzeit, Fertigstellungstermin, Vertragsstrafen, Behinderungsanzeigen, Nachträge — must go through the actually agreed contract terms (VOB/B vs. BGB; editions change; VOB/B only privileged when adopted wholly and unmodified) and professional review. Cited clauses here are pointers for a human to verify in the current edition.
4. **Never present FreeCAD output, a Gantt chart, a network plan or these tables as construction-ready.** If the user appears to treat any output from this skill as a final, buildable or approved programme, state immediately and plainly: *"This is a planning model — dates, capacities and shoring decisions need review by the responsible engineers and the contracting parties before anyone digs."*
5. Values flagged **VERIFY** were digested from sources whose printed table grids were partially corrupted or dated (equipment catalogues 1994–2017, factor tables); re-check against current BGL/Zahlentafeln, manufacturer catalogues and the standard text before quoting in a deliverable.
6. Known gap, stated openly: the **week-by-week house programmes in §15 are modelled estimates** built from the digested crew-productivity values and cycle times — no authoritative single-family-house week plan exists as a cited standard. Treat them as plausibility baselines.

---

## Section 1: The Master Build Sequence (Baualgorithmus)

### 1.1 Canonical Order — DACH residential house

```
 0. Pre-construction: Baugenehmigung, contractor award, baseline
    schedule (Basisablaufplan), utility applications, SiGeKo appointed,
    SiGePlan, Gefährdungsbeurteilungen, notice to BG/authority
 1. Baustelleneinrichtung (BE): fencing, gate, site cabins, sanitary,
    temporary power/water, crane pad/runway, Baustraße, delivery concept
 2. Vermessung: setting-out of building corners + elevation benchmarks
    (main point method), boundary check vs. approved site plan (§8A)
 3. Excavation: Baugrube or trench system, with shoring decision
    per DIN 4124 BEFORE digging; spoil management & disposal classes
 4. Groundwork at formation: blinding/Leinfundament, capillary break,
    soil exchange or improvement if formation is not as assumed
 5. Substructure (Keller or WU-Fundamentplatte in slab-on-grade):
    reinforced watertight base slab, basement walls (white tub per
    WU-Richtlinie or black tub per DIN 18533), waterstops at joints,
    backfill to DIN-4124-compacted layers once walls are propped/braced
 6. Ground-floor slab / floor build-up: insulation, pipes in screed zone,
    DPM; or top-of-basement slab with waterproofing to below-grade edge
 7. Shell (Rohbau) storey cycle — per floor:
    columns/walls (steel + formwork + pour) → slab falsework + formwork
    → slab steel + cast-ins → pre-pour hold point → pour → cure/strip
    → strike props per engineer's release → next storey
 8. Staircore/lift shaft ahead as climbing reference; staircase usable
    as site access early — never leave it to last
 9. Roof structure: timber roof (Zimmermann) or flat-roof build-up;
    membrane/waterproofing + ponding test on flat roofs
10. Weather-tight milestone (Winddichtigkeit): windows/doors in, roof on,
    membrane sealed — GATE for all wet fit-out trades
11. MEP first fix: electrical conduits/boxes, heating, plumbing,
    ventilation ducts — chases in masonry, not in structure
12. MEP gate: rough-in complete, pressure/continuity tests,
    photo record BEFORE any closing layer (plaster/drywall/screed)
13. Plaster/rendering (internal + external), floor screed (Estrich)
    per ATV DIN 18560 with drying times; anhydrite vs cement rules
14. Insulation systems (ETICS/WDVS external), roof build-up completion
15. Fit-out (Ausbau): drywall/ceilings, wall & floor tiles, painting
    (primer + coats), joinery/cabinets, doors hung after floor build-up
    confirmed
16. MEP second fix: switches, sockets, sanitary ware, heating
    commissioning, electrical installation test (DGUV V3 / wiring regs)
17. External works: paths, drainage to separation system, landscaping —
    never bridging the DPC/Abdichtung level
18. Cleaning, functional tests, punch list, technical completion
    (Technische Abnahme per VOB/B §12 or §640 BGB), handover pack,
    defects-limitation period (Verjährung 4 y VOB/B / 5 y BGB) starts
```

**Hard-gate logic that never changes** (from universal sequencing, restated because it dominates European programmes): nothing gets buried before its inspection; nothing gets loaded before its strength release; nothing wet starts before the building is weather-tight. The three longest non-compressible waits on a house programme are: concrete strength gain (pour → strike → prop release), screed drying (≈ 1 day/cm for cement screed up to 5 cm, ≈ 0.7 day/cm beyond — cement; anhydrite flow screed ~20–30 mm: ~1 day/cm up to 4 cm then slower, and **underfloor heating needs a heating protocol/Heizprotokoll before impermeable floors** — VERIFY per current practice), and paint/primer substrate dry-out.

### 1.2 Phases and Typical Durations — single-family house with basement

Planning baseline for an ~140 m² living-area house, ~340 m² enclosed volume (BRI) basement + two storeys, conventional in-situ concrete/ masonry shell, normal spring/summer start, continuous funding. **Modelled heuristic from the §4 productivity tables — not a cited standard; adjust for crew size, winter, and delivery lead times.**

| Phase | Typical duration | Notes |
|---|---|---|
| BE + setting out | 1–2 wk | Temporary utilities have weeks-long lead time — order in phase −1 |
| Excavation + shoring + formation | 1–2 wk | ~350–600 m³ spoil for a full basement — 1–3 excavator days + truck cycles; weather-sensitive |
| Base slab + basement walls | 2–4 wk | WU concrete pour + cure + backfill sequence; single slab pour strongly preferred |
| Ground floor slab + shell GF (walls+ceiling) | 3–4 wk | weekly-to-fortnightly floor cycle at this size |
| Upper floor shell | 3–4 wk/floor | with second full formwork set; without, +1–2 wk/set cycle |
| Roof structure + covering | 2–3 wk | timber trusses/panels ordered ~10–14 wk ahead (long-lead!) |
| Windows/doors in (weather-tight) | 1–2 wk | ~10–16 wk delivery lead — order at shell start; the most common programme-breaker |
| MEP first fix + screed | 4–6 wk | screed drying then follows §1.1 drying rates (parallel: underfloor heating pipes) |
| Plaster/drywall + painting | 4–6 wk | external render only above +5 °C sustained (see §3.4) |
| Floor finishes, joinery, second fix | 4–6 wk | |
| Commissioning + punch + Abnahme | 1–2 wk | |
| **Total** | **~30–40 weeks (7–10 months)** | plus approval phase; plus winter surcharge if crossing Nov–Feb |

**Reality pattern:** the shell (Phases 1–6) takes ~30–35% of calendar time, fit-out ~65–70%; and the fit-out end is when subcontractor coordination (not physics) breaks programmes — see §7/§13.

### 1.3 The Four Dependency Types

Not all "A before B" is equal. Classify every link before compressing anything.

| Type | Meaning | Compressible? | Example |
|---|---|---|---|
| **Physical (FT, physikalisch)** | B impossible until A exists | Never | No slab pour before formwork and steel |
| **Material/chemical (FT, stofflich)** | B waits for A's strength/cure/drying | Never — this is chemistry | Prop release per cube results; screed dry-out |
| **Legal/inspection (FT, juristisch/organisatorisch)** | B buries A; inspection must come first | Only by inspecting faster | Pre-pour check (Bewehrungsabnahme), Abnahme |
| **Preferential (FT, vorzugsweise)** | Convention, damage avoidance | Yes, with protection | Flooring before/after painting |

**Rule:** when someone asks to "run these in parallel to save time", name the dependency type first. Only preferential links are free. Compressing a chemical link cracks slabs; compressing an inspection link reopens walls; compressing a *legal* link (starting before permit/notice duties) stops the job.

### 1.4 Decision Tree — Can Activity B Start?

```
Is predecessor A complete (or complete in this Bauabschnitt/zone)?
├── NO → Can B start on a completed zone portion? (zoned flow working)
│         ├── YES → Check zone boundaries: no shared falsework grid,
│         │          no shared propping system, no shared curing element.
│         │          Flow-line/Takt conditions per §6.
│         └── NO  → B waits.
└── YES → Has A's strength/cure/drying wait elapsed (measured, not assumed)?
          ├── NO → Is B a loading activity (crane outtrigger on slab,
          │        materials stacked, falsework erection above)?
          │        ├── YES → WAIT. Non-negotiable. Engineer's release only.
          │        └── NO  → Non-loading prep may proceed (marking, staging).
          └── YES → Has the hold point/inspection been signed?
                    ├── NO → STOP — this is the rework gate.
                    └── YES → Will B conceal A permanently?
                              ├── YES → Photo/as-built record FIRST.
                              └── NO  → Proceed.
```

### 1.5 Cast-In Items — the "now or never" list (before any pour)

Everything below must be placed and checked **before concrete goes in**; retrofitting = core-drilling = engineer approval = cost + programme:

- Conduits and boxes crossing slabs/walls; ceiling mounting points; downlight runs
- Sleeves through beams/slabs/walls (waste stacks, vents, roof outlets, ducts)
- Wall-boxes set to **finished** face (plaster/tile build-up — model it!)
- Puddle flanges (Ablaufstutzen mit Dichtmanschette) at wet-area and roof penetrations
- Base plates, holding-down bolts, structural embeds, scaffold tie points (later Gerüstverankerung!)
- Lightning-protection conductors and bonds; earthing in slab
- Lift pockets, stair nosing inserts, anchorage for later balustrades (EN 13374 post bases)
- Lifting anchors for precast/roof elements (plan the crane path of the finished structure)

---

## Section 2: Duration Estimation — LSA, GL and Crew Tables

### 2.1 The two fundamental metrics

**LSA (Lohnstundenaufwandswert / man-hour rate)** — work-hours per unit, independent of crew size:

```
LSA [Ah/E] = Arbeitstunden [Ah] ÷ Menge [m², m³, t, m]
d(TV_i) [work-days] = M_i × LSA_i ÷ (K_i × h_T)
   M = quantity, K = crew size (workers), h_T = shift length
   (German convention: 9-h paid day, ~8 effective h at site — use 9 consistently)
```

**Ah (Arbeitsstunden) ≠ clock hours**: 3 workers × 1 hour = 3 Ah. You **cannot** infer crew size from an LSA: the optimum lies between a practical minimum (2 people even for small jobs) and mutual interference (a 24-man trench is chaos, not speed). Influences to sanity-check: zone subdivision, quantity size, qualification (learning curve on ramp-up — first cycle always slower), aids, logistics, season.

**GL (Geräteleistung / machine output)** — quantity per machine-hour for machine-dominated work (excavators, cranes, pavers):

```
d(TV_i) = M_i ÷ GL_i   (machine hours → days)
```

GL is already a *long-run* value net of interruptions. In a mixed crew+machine work, the machine with the governing cost/capacity is the **Leitgerät** (lead machine); size everything else to it (§10.3).

### 2.2 Crew-productivity tables (digested, BAS-style; h per unit)

**Formwork/Schalung (h/m² contact area unless noted):**

| Element | Conventional (timber/beam) | System (beam & plate) | Large-panel |
|---|---|---|---|
| Strip footing edge | 0.6–0.8 | 0.3–0.5 | — |
| Wall ≤3 m | 0.7–1.2 | 0.3–0.6 | 0.2–0.5 (>3 m: +0.2–0.4) |
| Slab ≤3 m span, ≤250 mm | 0.8–1.0 | 0.45–0.65 (timber-beam) / 0.40–0.60 framed + drop head | (+0.1–0.3 if >3 m) |
| Beam | 1.5–2.0 | 0.9–1.3 (+0.1–0.2 small) | — |
| Edge beam / parapet | 1.1–1.3 | 0.7–1.05 (+0.25–0.4 if h ≤ 0.5 m) | — |
| Column | 1.3–1.8 | 0.9–1.4 (+0.2–0.3 small) | — |
| Opening (per each) | 0.25–0.65 h | — | — |

**Reinforcement/Bewehrung (h/t placed):**

| Element | Ø < 10 mm | Ø 10–20 mm | Ø > 20 mm | Range all |
|---|---|---|---|---|
| Footings/slabs | 18–21 / 22–25 (slab) | 11–15 / 16–20 | 8–10 / 9–12 | footings 8–21, slabs 9–25 |
| Walls | 24–27 | 18–21 | 12–15 | 12–27 |
| Beams | 26–28 | 19–22 | 14–17 | 14–28 |
| Columns | 28–30 | 21–24 | 15–18 | 15–30 |
| Welded mats: slab 14–20 (lighter mesh = higher h/t), wall 16–22 | | | | |
| Delivery/handling raw 0.5–0.7; cut/bend plant: Ø<10 9–11, 10–20 6–8, >20 4–6 (plant h/t, not site) | | | | |

**Concrete/Beton placement, boom pump (h/m³; add ≈ +25% labour if by tower-crane skip):**

| Element | h/m³ |
|---|---|
| Blinding (per m²) | 0.01–0.02 h/m² |
| Mass fill | 0.2–0.3 |
| Unreinforced footing | 0.3–0.5 |
| Reinforced footing | 0.4–0.8 |
| Slab horizontal: 100–150 mm (>100 m²) | 0.6–0.8 |
| Slab 160–200 mm | 0.5–0.7 |
| Slab 210–300 mm (>200 m²) | 0.4–0.6 |
| Slab 310–500 mm | 0.35–0.55 |
| Slab >500 mm (>500 m²) | 0.3–0.5 |
| Wall ≤5 m high: 100–150 mm | 1.0–1.4 |
| Wall 160–250 mm | 0.8–1.2 |
| Wall 260–400 mm | 0.6–1.0 |
| Wall 410–600 mm | 0.4–0.8 |
| Wall >600 mm | 0.35–0.6 |
| Beam | 0.5–1.0 |

(thin/small pours cost more per m³ — rig-up amortisation; values drop with thickness and area.)

### 2.3 Derived planning bands — what a crew does per day

Using `output/day = K × h_T ÷ LSA`, at 9-h day:

| Work | Crew assumption | LSA used | Output/day |
|---|---|---|---|
| Wall formwork, system | 5 workers | 0.4–0.6 h/m² | **75–110 m²** |
| Slab formwork, panel + drop head | 6 workers | 0.40–0.60 | **90–135 m²** |
| Slab formwork, conventional | 6 workers | 0.8–1.0 | **54–67 m²** |
| Column formwork, system | 4 workers | 0.9–1.4 | **26–40 m²** |
| Slab rebar (mesh + top bar) | 4 workers | 12–16 h/t | **2.2–3.0 t/day — plan ~2.5 t/day** |
| Wall rebar | 3 workers | 12–27 h/t | **1.0–2.2 t/day** |
| Slab concrete, pumped | 4 workers + pump | 0.4–0.7 h/m³ | **45–90 m³/day** |
| Wall concrete, pumped | 4 workers + pump | 0.8–1.2 h/m³ | **30–45 m³/day** |

These are *planning* bands for a trained crew on a good site; first-cycle learning, tight plots and rebar-heavy detailing push toward the low end. VERIFY against your own Nachkalkulation before committing dates.

### 2.4 Worked example — single column (observation study, digested)

One rectangular column: formwork first half 4 m² by 3 workers in 64 min → 3×(64/60) Ah ÷ 4 m² = **0.8 Ah/m²**; rebar cage 125 kg by 2 workers in 90 min → **24 Ah/t**; close second half → 0.8 Ah/m²; pour 1 m³ by 2 workers in 66 min → **2.2 Ah/m³**; strip + clean 8 m² by 3 workers in 112 min → **0.7 Ah/m²**. Reading: one small column costs ~5–6 Ah — but on a multi-column grid the system-formwork LSAs (§2.2) apply instead; observation studies like this are how you calibrate your own values from site reports.

### 2.5 Worked example — 1-family house foundation level (9-h day, digested)

| Activity | Quantity | Output/LSA | Crew K | Hours | Days |
|---|---|---|---|---|---|
| Excavation (machine) | 512 m³ | 35 m³/h (GL) | — | 14.6 h | ~2 (incl. moves) |
| Subgrade compaction | 137.5 m² | 58 m²/h (GL) | — | 2.4 h | <1 |
| Blinding concrete | 126 m² | 0.25 h/m² | 3 | 10.5 h | ~1.2 |
| Strip footing edge formwork | 21.5 m² | 0.9 h/m² | 3 | 6.5 h | <1 |
| Base-slab rebar | 4.6 t | 26 h/t | 4 | 29.9 h | ~3.3 |
| Base-slab concrete | 46 m³ | 0.8 h/m³ | 4 | 9.2 h | ~1 |

### 2.6 Worked example — full storey cycle, Arbeitsverzeichnis (digested)

One storey, 9-h day:

**Slab 250 m²:** formwork 0.5 h/m² → 125 Ah ÷ 6 → **2.31 d**; rebar 3.15 t @ 12 h/t → 37.8 Ah ÷ 3 → **1.40 d**; pour 45 m³ @ 0.6 h/m³ → 27 Ah ÷ 4 → **0.75 d**; strip + clean @ 0.10 h/m² → **0.46 d**. **Subtotal ≈ 4.9 d.**

**Walls 360 m²:** formwork 0.4 → 144 Ah ÷ 6 → **2.67 d**; rebar 1.62 t @ 14 → 22.7 Ah ÷ 3 → **0.63 d**; pour 32.4 m³ @ 0.75 → 24.3 Ah ÷ 4 → **0.68 d**; strip 0.15 → 54 Ah ÷ 6 → **1.00 d**. **Subtotal ≈ 5.0 d.**

**Reading the result:** wall+slab cycle ≈ 10 working days of crew-time per storey for the shell trades — with two full sets of slab formwork and overlapping wall/slab zones, this lands at the classical **weekly floor cycle (Wochentakt)** of multi-storey in-situ construction; with one set it becomes ~2 weeks per floor. Formwork is ~25% of shell cost and the high-stripping-time member is the slab — hence the set-count arithmetic in §6.2.

### 2.7 Planning lead times feeding the programme (digested)

| Deliverable | Lead before use |
|---|---|
| Formwork drawings (Schalpläne) preliminary | 6 weeks |
| Schalpläne approved incl. penetration coordination | 4 weeks |
| Rebar drawings/shop drawings (Bewehrungslisten) approved | 3 weeks (bespoke mats ≥ 2 wk fabrication) |
| Precast erection drawings | 2 weeks before assembly |
| Windows/doors after on-site measurement | 10–16 weeks (order at shell start) |
| Roof trusses/panels | 10–14 weeks |
| Elevator (if any) — long-lead champion | 20+ weeks; interface at shell design, not fit-out |

A programme that ignores the procurement lines (Beschaffungs-Liniens) fails on the *delivery bar*, not the labour bar. Model delivery as an activity with its own float.

---

## Section 3: Weather, Seasonality and Concrete-Temperature Constraints

European scheduling is seasonal scheduling: winter stops or surcharges unheated work, and the weather loss itself is a contractual category (BRTV weather-loss provisions; weather-related short-time work exists as an industry mechanism). Plan the season, don't fight it.

### 3.1 Winter construction (Winterbau) — what changes

| Constraint | Practical rule |
|---|---|
| Fresh concrete must not freeze | Keep above ~+5 °C until it has reached ~10 N/mm² (approx. 3 days at +20 °C, far longer cold — the strength-vs-temperature clock slows roughly with every 10 K drop). Frost damage in the first days is permanent: strength loss, scaling, freeze-thaw failure of the surface. |
| Measures (in order of preference) | Insulated formwork/quilt covers (Schalungsbatterien, thermohaube), heated enclosure or scaffolding with tarps + heaters, warm mixing water/heated aggregate, insulation over finished surfaces, wind-tight protection; accelerators/admixtures only per the concrete supplier's written winter recipe (chloride-free) — **VERIFY per DIN EN 13670 / DIN EN 206 winter-concreting rules and the current national annex — not fixed in the digested sources** |
| Programme effect | Cold weather lengthens every chemical wait in §1.1: striking, prop release, screed drying, paint drying all extend. Expect +20–50% on concrete-cycle activities Nov–Feb unless heated. |
| Cost effect | Winter surcharge (Winterbaukosten: insulation, heating energy, enclosures, slower crews) is a **time-independent site-overhead item** (BGK special costs) — it must be priced at tender, not discovered in January. |
| Mortar/masonry | No masonry or rendering below ~+5 °C sustained (mortar frost damage); typical stop Nov 15–Feb 15 unless site-heated. External render: only above +5 °C day and night, not on frozen or sun-hot substrate, no rain for the drying window. |
| Excavation | Frozen soil needs ripping/milling (GL collapses); formation must not freeze under the night — cover, or place blinding immediately. Backfill in frozen lumps does not compact — frost-heave risk under floors/paths later. |
| Labour | Snow/ice clearance on roofs, ramps, scaffold decks is a safety duty first, productivity second; wet-cold drops output measurably — use the low end of §2.3 bands. |

### 3.2 The contractual weather layer

- Weather is normally the contractor's risk within "customary for the period" limits; **abnormal** weather (longer frost, non-seasonal rain weeks) can underpin a §6 VOB/B extension (weather proof = the Bautagebuch entries + official station data — keep the §14 discipline from day 1).
- Unusual rain days (außergewöhnliche Regenmengen) are claimed day-by-day with work-affected proof, not in hindsight. The daily report (§14) is the only memory a tribunal trusts.

### 3.3 Hot weather and summer storms

Same physics as the universal practice, retargeted to Central-European summers (which are getting hotter):

| Control | Guidance |
|---|---|
| Placement temperature | Request ≤ ~26–28 °C fresh concrete in summer (supplier: shaded aggregate stock, chilled water/ice flake) — **VERIFY per DIN EN 13670/206; limits are spec-dependent** |
| Pour window | Early morning; never midday slab pours in heat waves |
| Plastic shrinkage | Start protection immediately after finishing — wind + low humidity cracks the surface in the first hours, before the concrete is hard: fogging, immediate covering, foil or curing agent (curing agent = bond-breaker: never under bonded screed/tanking — abrade off) |
| Curing | Keep moist ≥ 2–3 days minimum, longer for slabs in sun/wind; in summer the failure window is the weekend (nobody waters Sat/Sun) — ponding, foil, or curing membrane instead |
| Evaporation vs. winter | A slab needs the *same total moisture history* whichever season; winter slows the clock, summer steals the water |

### 3.4 Seasonal programme adjustments (planning defaults)

| Season | Effect on programme |
|---|---|
| Mar–May | Best concrete/earthworks window; schedule the foundation + shell cycle here |
| Jun–Aug | Storm cells can wash out pours/cuts; keep 10–15% weather float on exposed earthworks; roof-on before autumn |
| Sep–Oct | Last good render/waterproofing window; weather-tight by mid-October protects the fit-out season indoors |
| Nov–Feb | Winter rules §3.1; either heat + price it, or plan indoor fit-out (dry trades, heated shell) and freeze the concrete cycle |
| Mar (again) | Spring thaw: formations soft, frost-heaved subgrades fail — re-verify compaction before slabs/paths |

A house started in April with the §1.2 sequence lands weather-tight in autumn and finishes indoors. Started in September, the shell crosses winter and the programme absorbs §3.1 surcharges — show that in the baseline, don't discover it in February.

---

## Section 4: Bar-Chart Programmes and the Schedule-Plan Ladder

### 4.1 The bar chart (Balkenplan / LSA / Gantt)

The bar chart (Balkenplan, LSA/Gantt family) remains the contract-facing view; the network (§5) is the computation behind it; the bar **lengths** come from the §2 productivity values — a bar without a crew calculation behind it is a wish.

Rules that make a bar chart useful rather than decoration:

- **Mark non-working days** (weekends, holidays, and contractual shutdowns) as shaded calendar columns; bars crossing them count **working days (AT, Arbeitstage)** only. State which calendar you use (AT vs. KT vs. CA "Werkeltage").
- Group bars by trade or procurement lot (Fachlose), with summary bars per group; keep activity codes stable across all versions — a renamed bar cannot carry a claim.
- Write actuals onto the printed plan on site (or update digitally daily) → **Soll(0) → Soll(1) → … → Ist versions**; the version stack itself is the delay-claim documentation (§13).
- Every chemical wait (§1.1) gets its own bar with a lag, not a smaller bar — a hidden wait becomes an invisible claim.
- Link the chart to the resource plan (§7): a bar with no crew behind it is a wish, not a plan.

### 4.2 The schedule-plan ladder (Terminplanarten) — who owns what

| Plan | Owner | Phase & role |
|---|---|---|
| **Meilensteinplan** (milestone plan) | Client (Bauherr) | Idea stage: a few key dates — permit, shell start/finish, weather-tight, completion |
| **Rahmenterminplan** (framework) | Client/planner | Tender document — the bidders must fit (or flag) it |
| **Grobterminplan** (outline) | Bidder | With the offer: proves the Rahmenplan is feasible (Plausibilitätsprüfung — an implausible offer gets excluded) |
| **Generalterminplan** (general) | Contract | Binding dates inside the contract; base for the client's other contracts |
| **Koordinations-/Feinterminplan** | Contractor AV | Execution detail; only made as fine as coordination requires |
| **Steuerungs-/Detailterminplan** | Client PM/Steuerung | Cross-contractor interface control on multi-firm sites |

**The single most important scheduling act is contractual, not graphical: agree a baseline schedule (Basisablaufplan) with a document/plan-delivery list and mock-up dates in the contract** (§13). Without a frozen Soll(0) every later "delay" is a matter of opinion.

### 4.3 Milestone plan types — contractor vs. client view

- **Client milestone plan:** permits → award → start → shell complete → weather-tight → technical completion (Abnahme) → handover. These are contract dates with consequences (Vertragsstrafe §11 VOB/B: day-rate 0.3%/AT overruns admissible, 0.5% struck down; cap 5% of net account — case law, **VERIFY against current contract terms**).
- **Contractor milestone/look-ahead plan:** the 5-day plan (see §7.3) and weekly plans, sequenced by zones and crew continuity.
- **Interface milestones** (both views agree them): crane erect/demob, scaffold in/out, "power on", "screed pourable", "windows in", each with a preceding lead (e.g. "screed pourable" needs heating on + weather-tight + first fix signed).

---

## Section 5: CPM Network Planning (Netzplan, Vorgangsknoten)

### 5.1 Logic ties (Anordnungsbeziehungen, AB) — four types, lags in working days

| Code (DE) | EN | Meaning | Worked sense |
|---|---|---|---|
| **EA** (Ende–Anfang) | FS | B after A ends | Pour → strip after 2 d lag |
| **AA** (Anfang–Anfang) | SS | B starts n after A starts | Excavation follows shoring crew at +1 d |
| **EE** (Ende–Ende) | FF | B ends n after A ends | Marking ends ≤ 4 d after laying ends |
| **AE** (Anfang–Ende) | SF | B ends only after A starts | Traffic diversion must end by closure start (rare; avoid where possible) |

Lags "n" can be **negative** (a lead): AA(−2) = B starts 2 d *before* A. Prefer EA (FS) links — they're the only ones everyone reads the same way; use AA/EE deliberately for crew-continuity flow, and almost never SF.

### 5.2 The pass formulas (activity-on-node)

Convention used here: days numbered 1..N, `FEZ = FAZ + d − 1` (end-of-day counting). Converted to calendar, remember the computed time points are unit-end instants — add 1 unit when mapping start times onto the calendar.

```
Node = activity:  name | duration d
forward pass (early, from project start, FAZ₁ = 1):
   FAZ (ES) = max over predecessors p of (FEZ_p + lag_ea)   [and AA/EE variants]
   FEZ (EF) = FAZ + d − 1
   at a merge keep the MAXIMUM
backward pass (late, from project end; LF = planned finish):
   SEZ (LF) = min over successors s of (SAZ_s − 1 − lag_ea)  [AA/EE variants likewise]
   SAZ (LS) = SEZ − d + 1
   at a diverge keep the MINIMUM
floats:
   GF/TT (total float, Gesamtfrist)   GZ = SAZ − FAZ = SFZ − FEZ
   FF/FT (free float, Freie Frist)    FZ = FAZ(successor) − FEZ − lag − 1
critical activity: TT = 0 → chain of them = critical path (kritischer Pfad)
   — any slip there = project slip (and the only place delay claims
     on AN-caused events actually bite for the whole programme)
```

Free float ≤ total float always. Use float for **spatial de-confliction** (shift a crew to another zone inside its float) — that is scheduling's whole game on a small plot. Do not schedule risky activities at their latest times: spending float as "safety" is invisible risk transfer; keep a deliberate early-start variant on the activities with the widest outcome spread (weather-dependent, single-source supply).

### 5.3 Worked CPM example — pipeline/trench run, 18 days

A trench run for buried services (municipal logic; identical for a house's service lines). Reconstructed clean teaching variant of the classic worked example — durations and ties chosen to be fully self-consistent: **early finish day 18, exactly one activity with float**.

| ID | Activity | d | Predecessor (AB) |
|---|---|---|---|
| V1 | Remove paving (Fräse/Aufbruch) | 2 | — |
| V2 | Install shoring (Verbau) | 3 | V1 EA |
| V3 | Trench excavation to formation | 2 | V1 EA |
| V4 | Bedding / blinding concrete | 1 | V2 EA **and** V3 EA |
| V5 | Lay and joint pipe | 3 | V4 EA |
| V6 | Pressure / line test | 2 | V5 EA |
| V7 | Backfill in layers, compaction proof | 3 | V6 EA |
| V8 | Re-instate paving | 4 | V7 EA |

Forward pass (FAZ₁ = 1): V1 1–2. Both V2 and V3 start day 3: V2 3–5, V3 3–4. V4 needs *both* → FAZ = max(5,4)+1 = **6**. Then serial: V5 7–9, V6 10–11, V7 12–14, V8 15–18. **Early finish = 18 working days.**

Backward pass from LF(V8) = 18: V7 12–14, V6 10–11, V5 7–9, V4 6–6; V2 LF = FAZ(V4)−1 = 5 → LS 3; V3 LF = 5 → **LS 4**.

| | V1 | V2 | V3 | V4 | V5 | V6 | V7 | V8 |
|---|---|---|---|---|---|---|---|---|
| FAZ–FEZ | 1–2 | 3–5 | 3–4 | 6 | 7–9 | 10–11 | 12–14 | 15–18 |
| SAZ–SEZ | 1–2 | 3–5 | **4–5** | 6 | 7–9 | 10–11 | 12–14 | 15–18 |
| TT (GF) | 0 | 0 | **1** | 0 | 0 | 0 | 0 | 0 |
| FF (FZ) | 0 | 0 | **1** | 0 | 0 | 0 | 0 | 0 |

- **Critical path V1→V2→V4→V5→V6→V7→V8.** V3 (excavation) is the only non-critical activity: total float 1 d = free float 1 d (FF(V3) = FAZ(V4) − FEZ(V3) − 1 = 6 − 4 − 1). Sliding the dig to days 4–5 costs nothing; days 5–6 slips the whole run.
- **Read the method, not the numbers:** bedding waits for the *shored* trench, so the Verbau sits on the critical path **by construction** — which is exactly why the §10 shoring choice is a scheduling decision, not only a safety one. A system that keeps pace with the dig (hydraulic boxes, driving sheet piles ahead of excavation) collapses V2+V3 into one machine cycle; an in-situ bored-pile wall replaces the Verbau bar with a cure wait instead.
- Calendar mapping (Mon start, Mon–Fri): mark the weekend columns in the bar chart; 18 AT = 3.6 calendar weeks of run + 2 weekend gaps = finish in week 6 Monday.
- The same tie structure solves a house foundation: divide into zones (BA per bay), one crew hopping zones inside network floats, instead of one monolithic serial chain.

### 5.4 Programme acceleration logic

When dates are blown, the ladder is always: (1) re-sequence (more zones, AA ties), (2) add crew/equipment on non-critical-to-critical shifts (mind §7 space limits — more men in one trench is slower, §2.1), (3) buy time with product (fast-setting concrete with engineered striking release — §12 proof, not opinion), (4) reduce scope — last and only by the client. Compressing a chemical or inspection dependency is not acceleration; it is deferred failure.

---

## Section 6: Flow-Line Planning (Taktplanung)

### 6.1 The idea

Split the building into **Bauabschnitte (BA, zones)** — per floor/bay/fire-section — sized so **every trade's work content in one zone is approximately equal (the Takt Δt)**. Crews then move zone→zone like a production line: wall crew, slab crew, MEP crew each entering the next zone every Δt. The programme collapses to a repeating cycle and the critical path becomes a rhythm you can protect, staff and measure.

### 6.2 The core formulas

```
Takt time:        Δt ≈ max over trades of (work content per zone ÷ that crew/day-rate)
                  (balance zones until one trade governs; that trade sets Δt)
Serial (no overlap):      T = Σ per-trade durations
Flow-line duration:       T_Takt = (n + m − 1) × Δt  (+ inter-trade lags/Laschen)
                  n = number of zones, m = number of following trades
Formwork set count:       S_erf ≈ (time cast→strike→clean→return) ÷ Δt  → round up
                  ("full sets" = working set + striking set(s) + return lag)
```

**Worked set-count example:** weekly cycle Δt = 5 AT, slab props can be struck at day 4 with one-day clean/turn → S ≈ (4 + 1 + 5)/5 = **2 full sets + 1 partial** → order 2 slab sets + 60% second wall set for a 2-storey; at 10-day cycle 1 set suffices. This is the arithmetic behind §1.2's "one set vs two sets" duration jump — and behind the Takt's other lever: **change the cycle, not the crew**, when the plot is too small for two slab crews working zones at once.

### 6.3 Rhythm examples (digested anchors)

- Multi-storey in-situ wall+slab: **1-week floor cycle is the classical target** (formwork crew, rebar crew, concrete + pump each enter the next floor weekly). At this rhythm, propping of *all* lower floors stays in until the engineer's release cascade catches up (statics check per §12) — the props, not the cycle, gate the next cycle's rebar.
- High-rise core/wall cycle after the learning curve: ~1 week/wall lift with self-climbing formwork (crane-independent, 3 working decks; base section built with standard formwork).
- Cooling-tower-class ring wall: 1-day cycle after crew learning (extreme case showing cycle ≠ universal).
- Conventional timber formwork, single crew: realistically **fortnightly per floor** for small footprints.

### 6.4 Production-time and route-time diagrams

**Produktions-Zeit-Diagramm** (production-time): x = time, y = zones completed; slope = each crew's output rate. If the *follower* (e.g. rebar) is faster than the *leader* (formwork), the critical time between successive crews a(1→2) throttles the follower → idle time → cost. Coupling rule: match **END** points when the follower is faster; match **START** points when the preceding volume is smaller; optimise sequence order to save the total offset Δz.

**Weg-Zeit-Diagramm** (route-time, linear works: trenches, roads, pipes): x = chainage, y = time; slope = advance rate; negative slope = working against chainage; **vertical segments = standstill (no output — weather, waiting)**. Combine with a bar-chart insert for point works on the line. This diagram makes weather and waiting *visible* — the two claim categories you must document (§13) anyway.

---

## Section 7: Resource Levelling and Production Control

### 7.1 Belegschaftsplanung — the headcount rules

- Ideal manpower curve: **ramp up → plateau → taper** — not a sawtooth. Peaks above site capacity (working space, hoisting, storage, sanitary) are self-inflicted interference (§2.1's 24-man trench); troughs are dead Vorhaltekosten.
- Plot the bar chart with crew demand *under* every bar; then flatten within the floats: shifting an activity by ≤ its total float is free levelling; anything beyond is a change to the baseline (Soll(1) version + written approval).
- **Never let hoisting gear be the bottleneck** (crane queue = crew queue): labour dominates cost, crews idling for material/hoist are the worst loss on the site. Match crane coverage (§9.4, §8) to the flow.
- Size the crane crew-served count: 15–20 work crews per tower crane with skip concrete; 20–30 with pump; 3–5 with precast (§9.4) — beyond that the crane is the Leitgerät the schedule lost.

### 7.2 Capacity-shortfall ladder (when ahead of/behind plan)

```
1. overtime / Saturday shifts (surcharge cost, fatigue limit)
2. labour pulled from other sites (only if your other site can spare it —
   check before promising)
3. subcontract (NU) packages added — needs interface + supervision +
   their lead time; NU = complete service incl. warranty;
   labour-only help (Fremdunternehmer) is NOT a capacity fix for
   specialist works
4. rent equipment / buy a second formwork set (moves money into the
   next project's amortisation — formwork is rented per month where
   cycles are uncertain)
```

### 7.3 The control loop (Fertigungssteuerung) and the 5-day plan

Release resources → monitor (Soll/Ist, cause analysis) → steer back (re-plan if the target is already unreachable). Practical instruments:

- **Weekly plan** by (Ober-)Bauleiter: week-as-validity window carrying completion dates, mock-up dates, **order dates for long-lead items**, deliveries, plan-provision dates, other firms' entries — the coordination instrument on multi-firm sites.
- **5-day plan**: the next five days' activities *by name and person*, with material, machines, and miscellaneous — the look-ahead that catches "the pump is booked elsewhere" four days early. Its power is face-to-face commitment, which is also how the crew absorbs the schedule instead of receiving it.
- Document every loop iteration into the cost-control records (Sollkosten/IST comparison per position — feeds the next tender's LSA values: §2 discipline closes the loop).

### 7.4 Time–cost coupling: the cash-flow curve (Zahlplan)

The programme's second output is the **liquidity plan** — value earned and value spent per week:

- **Time-dependent costs follow the bar chart**: Vorhaltekosten (crane rent, containers, falsework standing, site management, financing Bauzinsen, bond fees) accrue per week → every week the programme moves shows in this line. Time-independent costs (materials) follow quantities, not dates — the reason extension ≠ damages (§13.4).
- Progress billing runs on the Leistungsmeldung (measured positions × agreed unit rates, part-positions at completion %) — the cash curve lags the work curve by the payment cycle (~3–6 weeks); model that lag in the programme, it is where site insolvency (still the sector's #1 knock-out) becomes visible early.
- Retention/security schedules (§14.3) and advance payments for long-lead items (Vorauszahlung §16(2) VOB/B against the window order) are lines on the same chart.
- Freeze the cash curve at contract award; update per version (Soll(1)...) together with the schedule — the two documents share every input.

---

## Section 8: Site Layout Planning (Baustelleneinrichtung, BE)

### 8.1 Three planning partners, one iterative drawing

The BE plan is produced in an iteration: **client's execution concept** (milestones, basic BE framework) → **SiGeKo refines it** (safety zones, escape routes, separation of people/traffic) → **executing firms detail it** (crane, storage, containers). On a small house the contractor does all three hats — do them in that order anyway, because safety and access are constraints the storage layout must live inside, not afterthoughts.

### 8.2 Method — requirements-list to layout

Work the plot in 3D/object terms, in this sequence:

1. **Immovable elements first:** existing structures, trees to keep, pits, boundary walls, neighbouring windows/routes, overhead lines (crane!), entry point.
2. **Movement envelopes of key plant:** tower crane = fixed mast + jib swept field (and runway if rail-mounted); excavator = arm reach + tracked path; concrete pump = outrigger box + boom reach diagram from the supplier. Overlay envelopes before placing anything else.
3. **Inner traffic routes:** truck paths (delivery to storage and back out — one-way loop or turning bay, not a dead-end reversing onto the crane pad), then widths and gradients.
4. **Storage and working areas inside crane/hoist reach** (or reachable by the truck-mounted crane that actually delivers).

**Demand list, worked case (single-family house, wall+slab, digested):** crane jib 25 m; brick/block store 12 m²; mortar/silo 4 m²; wall-formwork store 6 m²; slab-formwork store 20 m²; timber/roof material 20 m²; skip container; site store container; WC container; site office; power distributor; water tap; street connection; road access pad 2.5 × 6 m; construction fence. A missing line item on this list is how a site discovers it has no place to put a pallet of tiles — **write the list before the drawing**, and scale areas with footprint (rough planning heuristic: covered+open laydown ≈ 10–20% of building footprint for a house; larger for masonry, smaller with JIT delivery — VERIFY against your own jobs).

### 8.3 Operation rules

- The three main elements to reconcile are the **mass centre of the structure, the working field, and the construction road** — align the crane's working field with the structural zones and the flow levels; keep storage of the heaviest bulk *under* the jib.
- Provide a **separate short-term storage area (2–5 h dwell)** at the crane: it absorbs delivery-sequencing disruptions so the crane is never disassembling a stack to reach one item.
- The truck with its own crane (delivery vehicle) must be able to **reach every storage area without entering the crane's loaded swing** — and no storage beyond crane reach unless the delivering truck can place it.
- Easy exit at all times (emergency vehicles; deliveries don't queue across the public road).
- Delivery sketch (Andienung) issued to main suppliers — every supplier gets the same one-page routing/parking/booking sheet.
- **Social facilities outside the entrance zone** (ArbStättV/ASR logic); site office with a sightline onto the gate — the gate is where chaos is caught.
- Keep an order regime (housekeeping) — a 100 m² plot used as 300 m² of storage is a safety and output failure, not a tight-site reality.
- Observe the equipment-specific UVV/DGUV rules for every machine placed (clearance to overhead power lines, outrigger mats, slewing restrictions).

### 8.4 Crane siting rules (the layout decision with the longest tail)

- Position so **every storage zone and every work zone is covered by at least one crane**; where two cranes are used, **slew fields must overlap for relay**, and interlock (priority/Vorfahrt + slew limiters) is engineered and documented before the first simultaneous slew.
- **Never sweep loads or empty hooks over site cabins, containers or the public way** — cabin placement is therefore *after* crane siting, and street-level signalman arrangements for climbing cranes near boundaries.
- Near airfields/flight paths: height caps + aviation warning lights — check before the crane order, not at erection.
- Untendreher (luffing, self-erecting) for tight small-house sites without neighbour over-sail; Obendreher (top-slew, trolley) is the housing-site default — jib must clear adjacent roofs with the legally-agreed clearance.
- Climbing cranes (mast-tied or inside-core climbers) for towers; tie-in schedule must be **coordinated with the facade design** (ties through insulation = thermal bridge + cost) — a scheduling decision at structural-design time.

### 8.5 Construction roads & connections (Baustraße, Medien)

| Item | Rule |
|---|---|
| Subgrade | Check for HGV axle loads (delivery trucks arrive loaded — the pad under the skip container is the same design case); max longitudinal/cross fall documented; passing niches and turning areas where the plot forces two-way use |
| Handover | Document condition at start (photos/dilapidation of the public entry); restore-to-original is contractual |
| Utilities | Temporary power/water coordinated with network operators early (weeks of lead); **power connection is the single most common week-1 stall** — apply in the pre-construction phase; frost-protected water line; shielded/cabled power runs, RCD protection on every distribution board |
| Sewage | No direct discharge — collection/treatment and haul-off; sanitary rooms per ASR A4.1 (wash, WC counts by headcount) |
| Fencing | Closed site fence at street/boundary; gate locked out-of-hours; signage per local requirements; the fence line is also your theft boundary — materials disappear fastest in week 2 |

---

## Section 8A: Engineering survey for construction (Ingenieurgeodäsie)

The Vermessung step of §1.1 is what puts the drawing on the ground — and what proves afterwards that it stayed there. Engineering geodesy = all surveying work in connection with planning (Planung), setting-out (Absteckung) and monitoring (Überwachung) of technical objects; on a job site that is the same three phases: capture existing conditions (Bestand) as planning basis, transfer the planned object into nature, monitor executed work and surroundings. Results must carry documentary value (Urkundenwert) — "the surveyor fixed it" is a contractual position, "we eyeballed it" is not. Framework standard: **DIN 18710-x "Ingenieurvermessung"** (parts: general requirements, Aufnahme, Absteckung, Überwachung), recommended as reference in survey scope-of-work documents; terms per DIN 18709 (editions cited 2013 — **VERIFY** current text). The fundamental process: Absteckung *repeats until* the deviation from target coordinates stays under the permitted value; monitoring *repeats until* an alarm threshold trips — so the programme must carry time for both, not one "survey day".

### 8A.1 Coordinate and height systems — agree in writing before the first coordinate is used

- **Plane, Germany:** official geodata since the 2018/19 transition: **ETRS89** (GRS80 ellipsoid, ≈ WGS84 at cm level) with plane coords in **UTM** (zones 32N/33N). Legacy: **DHDN** (DHDN90) on the Bessel ellipsoid with **Gauss-Krüger** 3°-strip projection (±50′ either side of the central meridian ≈ 100 km wide, neighbouring zones overlap ~23 km; Rechtswert = Y + 500,000 m with zone number prefixed). Old cadastre extracts and DB nets are still DHDN/GK — a DHDN↔ETRS89 mix is a **metre-scale blunder** (DB project net DB_REF: ETRS89 referenced but mapped on Bessel/GK, differs from DHDN90 by 0.5–1.0 m, up to 3 m near borders). Check the EPSG code of every file imported.
- **Heights:** normal heights above NHN (network DHHN, reworked 2006–2012 → DHHN2016, reference surface GCG2016); official benchmarks every 1–2 km as wall/pillar bolts (Mauer-/Pfeilerbolzen); zero defined by tide-gauge mean water (Nationaler Pegel; "Europahorizont" planned from Neuer Amsterdamer Pegel 1940–58 mean). **SAPOS** (permanent GNSS reference network, official surveying): EPS ≈ 0.5–3 m, HEPS ≈ 1–5 cm (1–2 cm networked), GHPS sub-cm; RTK on the pole 1–2 cm, static multi-hour → mm — planning-grade control for site nets without a levelling campaign.
- **Distances: projection + curvature = Projektmaßstab.** UTM fixed scale 0.9996 → length-true at ~180 km from the central meridian; a 100 m line shortens 40 mm at the meridian and lengthens 23 mm at the zone edge; +10 m height ⇒ 1.6 mm/km. Combined effect across Bavaria (UTM 32N): −6.7 to +10.7 cm/100 m. Site practice: either work in a local **Baustellenkoordinatensystem (BKS)** with scale 1 (CAD distance = field distance; the usual choice for house→block scale), or apply the project scale to every distance both ways — never mix silently. Legal dimensions (Abstandsflächen, boundary distances) must hold *as measured on the ground*, regardless of grid.
- Meridiankonvergenz and Lotabweichung (deflection of the vertical) matter on long/steep sights and tunnels, not on a 30 m house baseline — noted so nobody "corrects" what doesn't need it.

### 8A.2 Point determination — the field formulas

All plane computation in German survey practice uses **gon** (400 gon = full circle) with Y = easting, X = northing.

```
Richtungswinkel (bearing) between two known points:
  t = arctan(ΔY/ΔX) with quadrant correction:
  I  ΔY+ ΔX+ → t      II ΔY+ ΔX− → t + 200 gon
  III ΔY− ΔX− → t + 200 gon      IV ΔY− ΔX+ → t + 400 gon   (0 ≤ t < 400)
Worked (digested): ΔY = 67.77, ΔX = 25.76 → t = 76.875 gon (quad I)

Polar method (Polarpunktberechnung), station S oriented on A:
  t_i = t_S,A + α_i (mod 400);  Y_i = Y_S + S_i·sin t_i;  X_i = X_S + S_i·cos t_i
  inverse — setting-out data (Absteckung):
  α_i = t_i − t_S,A (+400 if < 0);  S_i = √(ΔY² + ΔX²)
Worked (digested, retained): S(4826.27/3427.19), A(5083.69/4217.38)
  → t_S,A = 20.0489 gon;  P1 with α = 67.1252 gon, S = 120.125 m
  → t = 87.1741 gon, Y = 4943.966, X = 3451.227
```

Other methods: Vor-/Rückwärtsschneiden (forward/reverse angle intersection), Bogenschnitt (distance arc-cut); combined angle+distance is the modern total-station default. **Traverse (Polygonzug)** strength ladder: closed ring / bearing+coordinate tie at both ends > one-sided (angegrenzt) > suspended/free (no usable orientation) — long one-sided traverses are systematic-error prone and get gyro-strengthened on route jobs. Traverse coords ΔY = S·sin t, ΔX = S·cos t; misclosure distributed proportional to leg length: v_ΔY,i = −(S_i/ΣS)·f_y. Worked class-2 example (digested, retained): ΣS = 830.94 m, f_y = +0.012 / f_x = −0.055 m → longitudinal L = 0.056 m, cross Q = 0.001 m vs limits 0.095 / 0.091 m → met; angular misclosure −0.0092 gon distributed 0.0013 gon/station, limit ≈ 15.2 mgon → met. Limit *formulas* (√n-angle, √ΣS-position families) survived corrupted in the digest — **VERIFY coefficients against the current state surveying rule set (see 8A.6) before quoting.**

### 8A.3 Helmert transformation (similarity, 4-parameter)

Local (x,y) → network (Y,X) with translation, rotation, scale — **no shear** (affine 6-param only where a shear is physically justified — VERIFY before ever using one):

```
Y = Y0 + o·x + a·y      X = X0 + a·x − o·y
M = √(a² + o²)  (scale)     rotation = arctan(o/a)     |M−1| typically < 10 ppm
```

- **2-point case** (parameters from two identical points). Worked (digested, retained): M = 0.999515, rotation 179.2437 gon, Y0 = 86.425, X0 = 208.176.
- **n-point least squares** (n ≥ 2, more = checked): reduce all coords to centroids, then o = Σ(x̄·Ȳ − ȳ·X̄)/Σ(x̄² + ȳ²), a = Σ(ȳ·Ȳ + x̄·X̄)/Σ(x̄² + ȳ²); Y0, X0 from centroid difference. Unit-weight standard deviation S0 = √(Σ(v_y² + v_x²)/(2n − 4)). Worked 4-point case (digested): M = 1.000038, angle 34.574 gon, residuals ≤ 0.111 m, S0 = 0.043 m (residual table partially garbled in source — **VERIFY arithmetic before reuse**).
- Site practice: set **M = 1 (no scale)** for local nets so CAD distances match field distances; GNSS→state transformations use ≥3 well-distributed identical points.

### 8A.4 Free stationing (Freie Standpunktwahl)

Instrument anywhere with views on ≥2 (better ≥3) known points: measure directions + distances, compute provisional coords in a purely local frame (y_i = S·sinZ·sin r_i, x_i = S·sinZ·cos r_i — the sinZ reduces slope distances to horizontal), then Helmert-transform into the target net; the station's coordinates *are* −Y0, −X0 of that transform. **The acceptance check is the Klaffungen (residuals) at the known points.** Worked case (digested, retained): Klaffungen 0.05/0.03/0.04/0.05 m vs the class-2 limit 0.04 m → points 10 and 13 rejected — restation or resolve the gross error *before* setting out a single point. No backsight orientation needed — why it is the default on cluttered sites.

### 8A.5 Height transfer to the site — levelling and trigonometric

**Geometric levelling (Nivellement)** remains the backbone for Anschlusshöhen (connection heights): Δh = R − V (backsight − foresight) per setup; always Hin-/Rückmessung (out and back), connected to known benchmarks at both ends; equalise sight lengths; never aim below 0.3 m on the staff; change plate (Frosch) on change points; **connect to at least two benchmarks** (town BM spacing ~300 m). Staffs/instruments per DIN 18703 accuracy grades: ≤10 / ≤3 / ≤0.5 mm per km of double levelling (√km normalisation convention — **VERIFY**). Worked case (digested, retained): out +2.132 / back −2.134 → ΔH = 2.133 m; connection misclosure −0.003 m (IST −8.326 vs SOLL −8.329) against a limit of form F = √(a² + b²·s[km]) mm (≈ 3.7 mm at 0.38 km; coefficients garbled — VERIFY per state rule) → distributed +0.0006 m/setup → adjusted H100 = 259.537 m.

**Trigonometric height transfer** (total station; the quick way across deep cuts and structures) with zenith angle Z, slope distance S, instrument height i, target height t:

```
ΔH = S·cos Z + i − t + (1 − k)·S²/(2R)     R = 6371 km
refraction coefficient k: ideal mean 0.13 (→ the 0.87 constant in the source
worked example); mid-latitude range ≈ −1 (day) to +1 (night), −10…+10 over
desert/glacier → correction unreliable at night/heat.
```
Keep transfer sights short (~≤100 m), observe both faces (Lage I/II), and treat the level (or SAPOS-derived heights at a stable point) as the checking authority. Worked example retained (i = 1.425 m; Z ≈ 94–107 gon over 287–452 m gave ΔH ≈ −2.3 to −30.4 m) — sign/constant **VERIFY** against your instrument's Z convention before field use.

**On the building:** the site **Pegel** — a fixed reference height (commonly +0.50 or +1.00 m above a defined level) transferred onto every rising structure and re-checked against the benchmark net at each stage; axes + Pegel are what all trades actually read. Vertical transfer: trigonometric OK for a few floors; optical/plumb methods from ~50 m (Zenitlot laser plummet ≈ 1:200,000 = 0.5 mm at 100 m, keep ≥15 cm off walls for lateral refraction; Pendel-/Schwimmlot alternatives); very tall buildings sway → GNSS tilt-compensated absolute methods at the climbing scaffold.

### 8A.6 Accuracy classes and tolerances

- German cadastral/official practice grades points into **Genauigkeitsstufen 1** (high land value / dense areas) **and 2** (other areas); limits scale with √(stations) and √(Σ lengths). Digested concrete numbers: free-station Klaffung limit — Stufe 1 ≤ 3 cm, Stufe 2 ≤ 4 cm (Baden-Württemberg rule set). The governing rule collections (state Vermessungstechnik-Vorschriften, TGB/AGSB family — **VERIFY exact name, edition and coefficients per Bundesland; not fully digested here**).
- Execution tolerances are a *different* system: **DIN 18202 Toleranzen im Hochbau** governs the built component (elevations, plane/vertical deviations) — the survey should control against them, and on tall structures the practice digest gives surveying only **~20 % of the construction tolerance** to secure axes and vertical reference lines (multi-storey/high-rise rule).
- Contract posture: name DIN 18710-2/-3/-4 (Aufnahme/Absteckung/Überwachung) quality levels in the survey scope of work; per legacy HOAI fee framing (2013 edition cited, since replaced — VERIFY allocation under current HOAI) "Bauausführungsvermessung" covers baubegleitende Absteckungen, Eigenüberwachung measurements + documentation, and continuous capture for the Bestandsplan — i.e. it is *recurring* site time, not one mobilisation.

### 8A.7 Curve setting-out (Kreis- and Klothoidennäherung)

Road/rail/pipe default, but curved façades, circular retaining walls and pipe links hit house-scale sites too:

```
Circle:      tangent length T = r·tan(τ/2)          arc b = r·τ  (τ in rad = gon·π/200)
Clothoid (transition curve), parameter A, end radius r:
  length l = A²/r;  normalised l_e = l/A;  for l_e ≤ 1 series approximation:
  X_UE = A·(l_e − l_e⁵/40)        Y_UE = A·(l_e³/6 − l_e⁷/336)
  tangent angle τ_UE = l_e²/2 [rad]
  shift   Δr = Y_UE − r·(1 − cos τ_UE)      tangent offset X_M = X_UE − r·sin τ_UE
```
Worked (digested, retained): A = 300, r = 400 → l = 225.0 m, l_e = 0.75 → X_UE = 223.227 m, Y_UE = 20.975 m, τ_UE = 17.905 gon, Δr = 5.259 m, X_M = 112.204 m (last-digit drift vs full series — VERIFY if you stake from it). Asymmetric clothoid–arc–clothoid and reverse transitions (Wendelinie, Doppel-Wendelinie) chain the same elements with (t_i, Δr_i, β) bookkeeping — digested worked cases run to tangent lengths 1092.5/1174.3 m etc.; beyond single curves, this is the specialist surveyor's deliverable, not the site agent's.
**Earthworks link (feeds §9/§10):** volumes between cross-sections on a curved alignment must be scaled by the centroid curvature factor k = r/(r − Y_S) (r negative left) — worked case (retained): V = 1513.37 m³ with k̄ = 1.029 vs 1470.67 m³ uncorrected (2.9 % low). Shoelace section areas A = ½|Σ(y_i z_{i+1} − y_{i+1} z_i)|, centroid Y_S from the same coordinate sums.

### 8A.8 Construction-survey tasks per phase

| Phase | Survey deliverable | Programme note |
|---|---|---|
| BE, before dig | Achsabsteckung: building corners + axes with offset stakes (Absteckpfähle) outside dig and haul routes; house scale often done as Schachtbaum (offset corner frame); boundary check vs approved plan | HP-01 (§12.3); setting-out repeats per 8A loop until within tolerance |
| " | Anschlusshöhen: connect to ≥2 official BMs or SAPOS points; fix site benchmarks/Pegel outside the dig, recorded with description in the BKS | one benchmark = one point of failure |
| " | Beweissicherung: pre-construction condition capture (photo + levels, scanner if contract demands) of adjacent buildings/public way | claim-proof baseline (§13.3); standard before sensitive excavations/tunnelling |
| Earthworks | formation-level and excavation-depth checks (Auskofferungskontrolle), volume sections incl. 8A.7 curvature factor, Fortschritts-/Abrechnungssurvey for billing | ties directly to §9.1 output and §10 dig control; 3D machine guidance (excavators consuming BKS + control net) is a surveyor's installation task in modern practice |
| Structure | per storey: axis transfer + corner points, Pegel mark, verticality check; keep survey slots (~0.5–1 d/floor) on the critical path | high-rise rules §8A.5; "never leave axis re-establishment to the steel erector's line" |
| As-built | Schluss-/Bestandsvermessung: executed object tachymetered or laser-scanned (scanner: ≥3 tie marks Passpunkte for georeferencing; measurement : post-processing ≈ 1:20 — plan the office time), deformation-true into CAD/BIM, quantities certified; if built reality deviates significantly, the BIM model must be updated from the survey, not left aspirational | capture into the official system keeps cadastre/state data current; feeds §14.3 |
| Monitoring | deformation monitoring per DIN 18710-4: reference net, Bezugsmessung/Nullmessung, defined alarm thresholds, statistical evaluation (confidence/deformation ellipses); hydrostatic systems <0.05 mm on fixed installations; ground-based radar 0.01–0.1 mm radial for continuous large-area cases | rare on a single house; standard where the §10 Verbau or adjacent property needs proof |

**Control-point protection (Vermarkung):** short-term = timber stakes with nail centre; routine durable = 2 cm iron pipes, granite blocks with drilled mark, survey nails with notched head (city ground), adhesive cross targets indoors; precision long-term = concrete piers. Every surviving point gets protection/cover + a marked spot on the BE drawing *outside* crane swing, spoil haul and laydown; losing an axis stake mid-pour costs a re-establishment day.

### 8A.9 QA discipline (survey-specific)

- [ ] Every setting-out coordinate traceable to a named control point and a stated system (BKS/UTM/DHDN) **in writing**; never assume the model and the field robot speak the same frame (8A.11)
- [ ] ≥2 independent height connections; ≥2 (prefer 3) well-distributed plane references spanning the site — redundant control, not one lucky station
- [ ] **Independent re-read:** a second person (or second setup/instrument) recomputes or re-measures corner coordinates + Anschlusshöhe before HP-01 sign-off; free-station Klaffungen within class limits (8A.4), rejected points documented, not quietly dropped
- [ ] Both-face (Lage I/II) observations for transfer work; residuals (Klaffungen) between faces within instrument class
- [ ] Control register (point, type, system, date, fixed-by, condition) maintained; damage/loss logged with re-establishment date
- [ ] Tolerance source named on every check sheet: survey class limit (8A.6) vs DIN 18202 component limit — different numbers, different purposes

### 8A.10 FreeCAD / BIM integration

- **Store the control net in the model** via the FreeCAD MCP `execute_code` path (rules of companion `construction-freecad-bim` apply — short self-contained calls): keep a spreadsheet `Vermessung` with columns `id, Y_E, X_N, H, system, epoch, fixed_by, note`, and mirror each point as a labelled datum/`Part::Vertex` in a `Vermessung` group, so HP-01 geometry, axes and Pegel are queryable and export-stable. FreeCAD stores lengths internally in **mm** — enter site metres ×1000, and make the model origin *the* BKS (0,0,0) by written agreement, never by accident.
- **Axes as construction geometry:** setting-out lines as named `A1…An` line objects carrying their site coordinates in the label → the 4D/checklist tooling can diff model vs re-survey and the §15 programme's survey tasks point at real objects.
- **IFC georeferencing:** the IFC itself keeps a local cartesian project CRS (origin near the object, scale 1 — no height/projection reductions inside the model); the link to the official system rides on `IfcProject` → `IfcMapConversion` + `IfcCoordinateReferenceSystem`/`IfcProjectedCRS` with EPSG codes (e.g. EPSG:25832 = ETRS89/UTM 32N; nested placements via `IfcLocalPlacement`). Agree the conversion — and thereby the Projektmaßstab question of 8A.1 — in the BIM-Abwicklungsplan, exactly as the written system agreement on drawings. (BIM/IFC mechanics: companion `construction-freecad-bim` / bim-management practice.)

---

## Section 9: Machinery and Plant Selection

### 9.1 Output theory (DIN ISO 9245 terms)

```
Grundleistung QB  = V_G × n × f_L        [m³/h, bank/compacted "fest" state]
   V_G = bucket volume;  n = cycles/h = 3600 ÷ t_S;  t_S ≈ 18–30 s (backhoe TLE)
   f_L = f_S × f_F   (soil looseness conversion × bucket-fill factor)
Nutzleistung QA   = QB × f_E             ← THE planning value (all derates in)
f_E = product of derating factors fH1 (swing) · fH2 (dig depth) · fH3 (dump
      target) · fH4 (task type) · fB (site/operating condition matrix)
```

- **Volumes default to bank ("fest") state.** The swell factor fS (Auflockerung: loose ÷ in-situ) is ≈ 1.1–1.4 for soils, up to ≥ 2 for blasted rock; shrink factor fV (compacted ÷ loose) ≈ 0.75–0.9. Bucket fullness fF by soil: free sand/gravel ≈ 1.0–1.2; sticky/clayey lower (~0.6–0.9). Exact grids in machine tables were ambiguous in the digest — **VERIFY before publishing numbers (digested range across classes ~0.6–2.1).**
- **Swing fH1 (digested):** 30°→1.12 · 45°→1.08 · 60°→1.05 · 90°→1.00 · 120°→0.96 · 150°→0.92 · 180°→0.88.
- **Dig-depth fH2 (soil class BK3–4 / legacy; modern contracts use Homogenbereiche):** 1 m→1.00 · 2 m→0.93 · 3 m→0.87 · 4 m→0.84 · 5 m→0.82 (BK5–6 milder: 1.00/0.95/0.91/0.87/0.85). Optimal dig depth ≈ 1–2 × bucket size.
- **Dump target fH3:** onto ground/heap 1.00; into truck by truck/bucket volume ratio: 2→0.69 · 3→0.73 · 4→0.76 · 5→0.79 · 6→0.81 · >6→0.83.
- **Task fH4:** free digging 1.00 · frequent repositions 0.73 · open trench 0.90 · **braced trench 2 m 0.55 / 4 m 0.44** — the shoring tax, and one reason Verbau-vs-slope is a cost decision (± see §10).
- **Site condition fB matrix (site × operating):** 0.83 (very good/very good) down to 0.52 (bad/bad).
- **Worked derate:** a 239 m³/h Grundleistung machine chain derated by the seven-factor version lands at **QA ≈ 145 m³/h** — planning values are ~60% of catalogue. (An alternative practice set: f1 swing 1.07/1.00/0.94/0.89; f2 depth ±; f3 dump 1.00/0.95/0.90; f4 volume ratio 0.82@2→1.0@≥7; f5 = t_H/60 with 50-min hour; f6 operator 0.75–1.0; f7 maintenance −5 min/h → 0.92.) Interpolate linearly; **validate against your own stop-watch observations — these scatter.**

### 9.2 Excavator classes and house-scale selection

| Class | Size | Use |
|---|---|---|
| Mini/midi | 1.5–8 t | House trenches, basement pad, demolition inside shell; rubber undercarriage protects paving, but tracked digs better in soil |
| Gr. 1 | ≤ 25 t / ≤ 125 kW | House-scale Baugrube with truck loading — the default "one digger, four trucks" machine |
| Gr. 2 | ≤ 60 t / ≤ 300 kW crawler | Large excavations, quarries, dams; needs low-loader transport |
| Gr. 3 | open-cast | not house scale |

Backhoe (TLE) dominates: it works *retreating*, top of cut never driven over. Face shovels/high-caps only for bulk from above. Digested service outputs: **excavation pit 500–1000 m³/day; trench 4–20 m³/h.** A full-house basement (~400 m³ bank) is therefore 1–2 productive days of a Gr.1 machine — the programme weeks around it are shoring, trucks, weather, and the formation inspection, not digging.

### 9.3 Loading chain (excavator + trucks)

- **Truck:bucket volume ratio 3–5 is economic** (1:1 → the excavator shunts half-empty trays; 10:1 → the excavator waits for the last scoop of a full truck).
- The excavator is the **Leitgerät** (higher capital rate): `N_trucks = QA_exc / QA_truck`, + ≈15% reserve for the cycle queue.
- **Worked example (digested, dam-fill case — method transfer):** excavator QA 217 m³ fest/h; load cycle for a 16 m³ tray: 8 scoops × 25.7 s + 1.73 loaded travel + 1.0 tipping + 1.24 return + 0.5 spot change = 7.87 min → truck QA ≈ 81 m³/h → 217/81 = 2.7 + reserve → **4 trucks.** Same arithmetic sizes a house's spoil haul: fix haul time → truck cycle → count.
- Fleet types: rigid dumpers 3–4 axle 8–15 m³; articulated site dumpers for muddy plots; tailgate trucks standard for spoil.

### 9.4 Tower cranes (Hochbau)

Selection criteria: **rated load moment (Nennlastmoment, tm) is primary** — capacity falls with radius (moment = radius × load); check the **load chart at the actual radius of the heaviest pick**, plus jib length, hook height under the highest obstruction, tip load, hoist/slew speeds, and (for the site) erection/demob assistance need.

Sizing heuristics for in-situ shell (Ortbeton):

```
crane count ≈ BRI ÷ (build duration [months] × L_Kr)
   L_Kr ≈ 3000–4000 m³/month per crane with pumped concrete
   L_Kr ≈ 2000 m³/month with crane + skip
by crews served: n_max ≈ 15–20 crews (crane+skip concrete)
                    20–30 crews (pumped)
                    3–5 crews (precast erection: 50–80 t or 8–15
                    elements per shift → 1000–1400 t/month)
area potential: A_max ≈ ψ × A_avg, ψ = 1.3–1.5
```

A single-family house never needs the formula — one small Untendreher or even a truck-mounted loader crane covers it; the formula sizes apartment blocks and tells you when a second crane pays for itself against crew-queueing (§7.1). Tower-crane cycle base **T0 = 150–300 s** in shell work; operator skill/machine-condition matrices and η_G ≤ ~50% useful share of standing time (it is a Vorhaltegerät — it idles, distributes, waits, and is repaired; its money is in the rent month, not the productive minute).

Types: top-slew with trolley jib (**Obendreher** — the housing default; telescopic/folding/runway variants) vs luffing-jib base-slew (**Untendreher** — self-erecting trailers, tight plots, no over-sail); climbing variants (§8.4); overlapping cranes need interlocks. **Data caveat: mobile-crane catalogue figures digested from 1994–2017 sources — refresh from current catalogues/BGL (VERIFY).**

### 9.5 Mobile cranes (indicative classes — VERIFY current catalogues)

| Class | Pad needed | Reach | Duty |
|---|---|---|---|
| 2/3-axle ~24 t | ≈ 11 × 7 m | 45 m hoist, 40 m radius; 35 t @ 3 m / 0.5 t @ 40 m | precast lintels, roof panels on a house |
| 4/5-axle ~50 t | ≈ 13 × 8 m | 75 m / 60 m; 100 t @ 3 m / 1 t @ 50 m | beams, large elements, crane assist |
| 6–8 axle ~75 t+ | ≈ 20 × 10 m | 115 m / 90 m; 300 t @ 3 m | hall/bridge lifts; crawler for multi-day heavy sites with truck-crane assist |

Mobile = Leistungsgerät (mobilise on demand, demob after the lift; outrigger pads + ground check mandatory — an outrigger on a backfilled trench line is an incident waiting to be scheduled). For precast/steel delivery days the tower crane often lacks capacity — a truck crane arrives for the day precisely so the tower crane stays in the shell cycle.

### 9.6 Concrete conveying

| Route | Constraint / cost |
|---|---|
| Direct from truck mixer chute | free fall ≤ **1.5 m**; anything deeper → drop pipe/chute, ≥ 0.5 m visible concrete in the pipe (segregation guard) |
| Tower crane + skip | adds ≈ **+25% labour** vs boom pump; only economic where the pump can't reach or the crane is otherwise idle — it isn't, in shell phase (§7.1) |
| Truck boom pump | capacity chart: reach/height vs output; **never tie/clamp the line pipe to formwork** (pressure surges move the form); gate valves on long lines; place from the finished slab forward, boom over the truck, not over the crew |
| Static pump / line pump | to ~600 m horizontal lifts for basements/long slabs where the boom can't reach |
| Pump scheduling | the truck-mixer convoy is a production line (plant cycle tF+tM+tL+tR, operating factor ≈ 0.8): book the pump, the pour crew, and the mixer sequence as one activity — a cancelled pump hour idles 10 people |

### 9.7 Aiding equipment (after the crane era of the job)

Material/personnel hoists (mast-tied); climbing work platforms ("electric scaffold"); mobile MEWPs (stable ground + set-up area reserved); **facade scaffolds with stair towers for the fit-out phase once cranes are gone**; load stages (Lastbühnen) at every floor edge for internal distribution; chain blocks/electric winches for hand moves. In fit-out the programme is governed by Etagenlogistik (floor-by-floor material distribution) — plan hoist time slots per trade in the weekly plan (§7.3) or the stair tower becomes the queue.

---

## Section 10: Excavations and Shoring (Baugrube, Verbau — DIN 4124)

The shoring decision is made **in the AV, before the excavator arrives**: it fixes method, cost (the fH4 dig §9.1), plot space, programme and the safety regime simultaneously.

### 10.1 DIN 4124 simple cases — where you may dig unsupported

| Condition | Limit |
|---|---|
| Vertical unsupported trench/slope wall — non-cohesive or soft cohesive soil | depth ≤ **1.25 m**, AND adjacent ground profile no steeper than 1:10 |
| Vertical wall in **at least stiff cohesive** soil or rock | ≤ **1.75 m**, provided the wall above 1.25 m over the formation is benched/sloped back at β ≤ 45° |
| Anything deeper / looser / loaded at the crest / adjacent to structures | **sloped excavation** (needs land + groundwater below formation) or **Verbau** (§10.3) |
| Working space beyond the footing edge | 300–500 mm each side for formwork + workers (tie to the shoring system, not vice versa) |

Sloping back is free on a wide plot and impossible on a terraced row — the adjacent-structure condition is why Verbau is the default in town. Beyond these simple cases the support is an engineered design (EAB/EB or EN 1997-1 with a competent designer): never a hire-company improvisation.

### 10.2 Crest surcharge — the numbers that prevent the classic collapse

Minimum clear distances from loads to the slope edge/walings (DIN 4124, digested):

| Support type | road vehicles | heavy road vehicles | constr. veh. ≤ 12 t | constr. veh. 12–18 t |
|---|---|---|---|---|
| unsupported walls | 1.0 m | 2.0 m | 1.0 m | 2.0 m |
| horizontal standard shoring | 0.6 m | 1.0 m | 0.6 m | 1.0 m |
| vertical standard shoring | 0.6 m | 0.6 m | 0.0 m | 1.0 m |

Spoil, containers, fuel bowsers and truck stand-off live **behind these lines** — a spoil heap at the crest is a surcharge load exactly where the cut is weakest. Surrogate design loads for deeper-pit analysis (strip loads when machine clearance < 1.5 m; VERIFY pairing): 10 t machine → 50 kPa (no clearance)/20 kPa @ 0.6 m over b = 1.5 m; 30 t → 110/40 kPa, 2.0 m; 50 t → 140/50, 2.5 m; 70 t → 150/60, 3.0 m; unlimited-area traffic surrogate q = 10 kN/m². Excavators and cranes keep ≥ 1.5 m from the edge or count as surcharge.

**Universal trench-entry rules (life-safety, non-negotiable):** no entry into an unsupported cut beyond the DIN 4124 limits; competent-person inspection **daily before entry** and after rain/vibration/cracks at the crest; ladder/ramp egress within reach of every worker in the trench; treat every unidentified buried line as live — obtain utility records (Leitungspläne), hand-dig trial holes where services are expected, mark confirmed routes physically; where UXO (Kampfmittel) risk exists regionally, clear it contractually before the dig; atmosphere check for deep pits with stagnant water/organics. Yesterday's stable cut proves nothing about today's.

### 10.3 Verbau type matrix (house → basement scale, and beyond)

| System | Water-tight? | Extractable? | Vibration/noise | Schedule character |
|---|---|---|---|---|
| **Trägerbohlwand** (soldier piles + timber/shotcrete lagging; Berliner/Hamburger/Essener variants) | NO | piles extractable, lagging often lost | moderate (pressed/drilled piles quiet-ish) | excavate in 0.4–1.2 m lifts behind the piles; bracing = ground anchors (boundary-crossing anchor permit!) or waling+struts/corner struts |
| **Stahlspundwand** (sheet piles, U/Z/Larssen) | ~sealed by clay driving; not designed tight | yes (vibrated/pressed) | **high when driven** — neighbour veto territory; pre-augering/pressing mitigates | immediately loadable — no cure wait; road haul ≈ 13 m lengths; circular cofferdams dewater to dig |
| **Bohrpfahlwand** (contiguous/tangent/secant bored piles) | secant = yes | no (permanent) | low | needs concrete cure before full dig — adds weeks; Ø ≤ 1.9 m rigs ≈ 76 t class, 58 m depth |
| **Schlitzwand** (diaphragm wall, bentonite-supported panels 2.5–10 m × 0.6–1.5 m) | yes | no (permanent/lost) | low (hydromill) | deep urban basements; top-down/Deckelbauweise lets the slab = permanent strut early |
| Ground anchors vs internal struts | anchors cross boundaries (permits!) and cost less in open plans; struts occupy the pit and must be designed with the excavation sequence (prestress: >30% sheet piles / >60% soldier piles for reduced-pressure design) | | | |
| **Base plugs** below groundwater in permeable soil (hydraulic-heave/HYD guard) | jet-grout columns Ø 0.8–2.8 m overlapped, or injected slab (permits + groundwater-protection rules) | | | adds a construction phase before the final dig |

**Wasserhaltung selection by kf (from the geotechnics companion skill):** open sump/pits in gravels with small inflow; wellpoint deepening; only a cut-off + plug (or freezing) where the pit must go below the water table in sand under pressure. Dewatering *adjacent ground* settles adjacent structures — the dilapidation survey (HP-01 in §12.3, photo regime §14.1) is your protection too. Underpinning next to existing footings = DIN 4123 territory: engineer, not schedule.

---

## Section 11: Site Safety and OSH Coordination (Arbeitsschutz, BaustellV)

### 11.1 The dual supervision system

Occupational safety runs on two rails: **state** (ArbSchG + BetrSichV, BaustellV, ArbStättV, GefStoffV, LärmVibrArbSchV...; enforced by labour inspectorates with unannounced visits, orders and shutdown powers) and **statutory accident insurance** (Berufsgenossenschaft **BG BAU** under DGUV/SGB VII: prevention rules DGUV Vorschrift 1, inspectors, fines; benefits and reha). Both can land on the same site on the same day.

**Falls from height are the dominant fatal accident class — even below 2 m** (roofs, skylights, ladders, scaffold edges). Design-out risk early: the client and the designer hold the biggest safety leverage (a membrane edge detail that needs no guardrail is a decision made at drafting, not at hoisting).

**TOP principle:** Technical measures before Organisational before Personal (PPE = last resort, never the plan).

### 11.2 BaustellV and the SiGeKo — coordination duties

| Instrument | Trigger / owner | Content |
|---|---|---|
| **SiGeKo** (safety & health coordination) | required whenever employees of **more than one employer** work on site — *even sequentially*; client must appoint **early in planning** | coordinate the Grundsätze of §4 ArbSchG/RAB 33 in design and tender; between firms during execution |
| Qualification | **RAB 30**: building-tech knowledge + occupational-safety knowledge + coordination competence + experience | |
| **SiGePlan** | **RAB 31**; for larger/complex sites and especially dangerous works | firms + their protective duties; client's traffic-safety (Verkehrssicherungspflicht) measures for third parties; key dates; info/materials for chosen measures. Drafted in preparation; **re-reconciled against actual progress** during execution |
| **Vorankündigung** | large sites / dangerous works → authority notification before tender/close | |
| **Unterlage für spätere Arbeiten** | **RAB 32** (per DIN 4426 — e.g. anchor points, roof access routes) | must exist **before** tendering the later trades; client keeps and updates for the life of the building |
| **Gefährdungsbeurteilung (GB)** | every employer, per ArbSchG §5/6, per project | 7 steps: scope (incl. pregnant/nursing, young workers) → identify hazards (BG BAU modules) → assess risk → measures per TOP → implement with responsible+deadline → verify effectiveness → update (results also feed the *tender*) |

**Liability sharp edges:** the site manager (Bauleiter) who fails to order a missing guardrail takes contributory negligence when a worker — *including another firm's worker* — falls there; the duty extends to pointing out the danger and escalating (NU management, then BG BAU) even without directive authority over that firm. Failing to run the project GB, instruct (Unterweisung) and monitor is a criminal-offence category, not an admin miss. Helmet-refusal ladder: verbal warning with witness → signed written notice → escalation (works council where it exists / formal warning).

### 11.3 Edge protection, scaffolds and openings (values)

| Element | Requirement |
|---|---|
| Temporary side protection (Seitenschutz) | per **EN 13374**: three parts — top rail (Geländerholm, ≥ ~1.0 m above deck, 0.7 m at low-risk edges per class — VERIFY class table), mid rail (Zwischenholm), toe board **Bordbrett 15 cm** |
| Access scaffolds | EN 12811 series (+ protective roofs where people pass below); prefabricated facade scaffolds EN 12810; assembly/use/dismantling instruction (Montageanweisung) derived from GB + manufacturer guide (BetrSichV); daily visual check by user before use |
| Scaffold load class | working scaffolds: distributed load limits by class — light trades (painter/plasterer tier) ≈ 2 kN/m² in one deck (material stacked on decks beyond class = the common failure; VERIFY current class grid EN 12811-1) |
| Falsework (Traggerüst) | EN 12812 (not 12811) for support structures incl. traffic loads; props steel EN 1065 / alu EN 16031; box beams EN 13377; formwork ties DIN 18216; **design + erection scheme by competent person; the "who computes the slab propping" question must have a documented answer before the first prop lands** |
| Floor openings / stair voids | guarded or rigidly covered (marked as load-bearing); no working over or through uncovered voids |
| Ladders | access only, short reach, tied; work from ladders is time-limited by GB logic — tower scaffolds/MEWPs for real work |
| Installation labour (BAS, for programme sizing) | guardrail 0.3–0.5 h/m; cantilever catch-fence 0.2–0.3 h/m; tube-frame scaffold 0.2–0.3 h/m³, framed 0.05–0.2 |

### 11.4 First aid, PPE, welfare

- **First aid:** ≥ 1 trained first-aider (Ersthelfer, 1-day course, refresh every 2 y; paid by BG, time by employer) per 2–20 insured present; above 20 → ~10% of the on-site crew. First-aid material within **≤ 100 m / ≤ 1 floor** of any fixed work point. Accident = DGUV Unfallanzeige form; site record same day.
- **PPE (PSA)**: helmet, safety boots, hi-vis as site rule from the gate; task-specific (fall-arrest only as the technical/organisational cascade says, with anchor points designed in).
- Welfare: wash/toilet/drying/heated-break rooms per ASR A4.1 headcount tables; drinking water; these are not "nice-to-haves" — they set the mobilisation cost line and the productivity floor.
- Insurance/registration realities: construction social-fund levies (holiday/pay equalisation) and sector minimum-wage rules apply to every firm and posted worker on site — contractor and client both carry checking duties; paper non-compliance stops sites.

---

## Section 12: Quality Supervision — Eigen- and Fremdüberwachung, Hold Points

### 12.1 The three-layer system

| Layer | Who | What |
|---|---|---|
| **Eigenüberwachung** (self-monitoring / production control) | each executing firm | check own work per the trade rules (VOB/C ATVs = "anerkannte Regeln der Technik" contractually); pour records, compaction tests, tolerances — **documented**, not felt |
| **Fremdüberwachung** (independent surveillance) | external/independent bodies | ready-mix concrete plant surveillance; execution of the **Prüfingenieur/Prüfsachverständiger** for the statics (system 4/Prüfstatik per state code), accredited labs for cube/core tests, Güteüberwachung on surveillance-required products (MVV TB marking logic, e.g. formwork/falsework products) |
| **Bauüberwachung** (site supervision for the client) | architect/Ingenieur **HOAI LPH 8** | monitors execution against approved planning + recognised rules; runs the hold-point register; the Bauablaufplan duty ("Aufstellen, Fortschreiben, Überwachen") is an LPH 8 Grundleistung |

Contract anchor: a defect is measured against the agreed Beschaffenheit **and** the anerkannten Regeln der Technik *at the time of Abnahme* — a mid-project rule change must be flagged by the contractor and the client chooses old (with a documented Bedenkenfreizeichnung) or new (→ variation order). Non-compliance with the applicable ATV = defect *and* rules-of-the-art breach, regardless of what the programme says.

### 12.2 Concrete evidence chain (the one the programme depends on)

- Strength is proven by **sampling + casting companion specimens witnessed at the pour** (record truck ticket, time, pour ID), cured correctly (immersion/controlled temp — not a windowsill), tested by an **accredited independent lab**; the signed report with calibration reference goes to the handover pack.
- Where early striking/loading drives the programme: **strike on measured strength with the engineer's written release**, not on elapsed days — extra cubes cured alongside the element are the tool; back-propping (Nachsteifen) below is an engineered arrangement spreading construction load through 2–3 floors (weekly-cycle multi-storeys keep lower-floor propping per statics check).
- Core-test backing if specimens are suspect (digested frequency logic from the existing-building tables: **≥ 1 core per started 100 m³ per casting day, ≥ 3 per mix**, Ø ≥ 100 mm): **VERIFY** the current EN 12504/EN 13791 + execution-standard (DIN EN 13670/DIN 1045-3) regime for new-build acceptance before quoting.
- Compaction Eigenüberwachung (earthworks, ZTV E-StB logic transferred to building backfill): degree-of-compaction tests per lift — subgrade/planum ≥ 1 test per started 1,000 m² per lift, min 2; structure backfill 1 per third lift per 200 m²; declare the required degree (100/98/97% family + E_st/E_dyn substitute criteria) **on the drawings** or the cheapest interpretation wins (VERIFY grid cells against current ZTV E-StB/DIN 18134).

### 12.3 Schedule-level hold-point register

Hold point = nothing proceeds until signed; witness point = notice given, may proceed if inspector is absent. On a house, run them all as hold points — a 30-minute inspection versus a two-week reopen is arithmetic, not philosophy.

| ID | Stage | Check | Signer |
|---|---|---|---|
| HP-01 | BE/setting out | boundary vs approved plan, benchmarks fixed outside the dig, neighbour dilapidation photo log, utility marks/UXO clearance; survey method + re-read per §8A.9 | client rep + surveyor |
| HP-02 | Formation level | strata = ground report, no soft spots/water, levels, shoring adequate to DIN 4124/design | TWS/geotech |
| HP-03 | Pre-pour, every structural pour | steel count/spacing/cover/splices, **cast-in list §1.5 complete**, formwork tight/plumb, props on design layout, pour route + pump booked, cubes sampled | TWS / Bauüberwachung |
| HP-04 | Post-pour | curing regime started, surface OK, cube chain recorded | site engineer |
| HP-05 | Waterproofing/white-tub & DPC continuity | joint waterstops, upturns, **flood/ponding tests 24–48 h**, protection layer before backfill/backfill load case | specialist + Bauüberwachung |
| HP-06 | Structural release to load (props out / next storey) | cube/lab results vs release threshold + **engineer's written release** | TWS |
| HP-07 | **MEP rough-in before any closing layer** | full checklist + pressure tests + photo record per wall (see companion skill) | all trades + client |
| HP-08 | Weather-tight milestone | roof/membrane closed, windows in, drying regime can start | Bauüberwachung |
| HP-09 | Screed/pourable notice | heating on/off state, substrate dry, thickness over pipes | screed + heating firms |
| HP-10 | Technical completion / Abnahme | punch list closed, tests (electrical DGUV V3/EN 62305, functional), handover pack (§14.3) | client (only the client or expressly authorised person accepts!) |

### 12.4 The three clocks, restated (every compression talk collides here)

*Curing* (keep it wet, days) ≠ *striking* (shutters off: foundations/walls/columns ~1–3 d, slabs ~3–8 d per digested Ausschalfristen — cold weather extends, measured strength governs) ≠ *full design strength / loading* (28-d reference). A prop-removal request is a §12.2 evidence request, not a calendar question.

---

## Section 13: Delay and VOB/B Claims Logic (Behinderung, Nachträge)

The schedule is the evidence base of the claims interface. This is a pointer map for planning discipline, not legal advice — every contract question runs past the actually-agreed terms (VOB/B wholly incorporated vs. pure BGB) and a professional.

### 13.1 The §6 VOB/B mechanism (BGB §642/BGB-analogous where VOB/B not adopted)

```
Disturbance (Behinderung/Verhinderung) arises
  → contractor notifies UNVERZÜGLICH (without delay), IN WRITING (§6(1))
  → extension of time on request — verschuldensunabhängig (no fault needed, §6(2))
      neutral events (abnormal weather, higher force) → time yes, money no (§6(2b/c))
  → if the client is responsible (late plans, late decisions, missing
      site-readiness, other firms' delays it caused) → damages §6(6)
      (lost profit only for intent/gross negligence)
  → prolonged total standstill → extraordinary termination rights (§6(3)-(5))
  → client orders acceleration (§2(5) Anordnung) → its cost is priceable
```

Contractor's own prior-firm default (Vorunternehmer) is normally *not* automatically the client's §6(6) event — mind the contractual chain.

### 13.2 What a Behinderungsanzeige must contain (11-point list)

start/stop of the hindrance · cause · begin/end/duration · **affected activities** · the planned start & duration of those activities · actual impact on the sequence · site status photo/record · contractor's own readiness to work · any sequence changes forced · extra work arising · whose responsibility sphere. Written, dated, specific — "we are delayed" is not an notice; the named activities + baseline bars are the claim's skeleton.

### 13.3 Proof structure: the schedule-linked narrative

Case law puts the full presentation-and-proof burden on the contractor; the accepted method is the **bauablaufbezogene Darstellung** — a schedule-linked reconstruction: compare Ist against the disturbance-modified Soll' at every disturbance window, attribute each delay day to one sphere (client / contractor / neutral), separate the "envelope" of client-caused hindrance from contractor default. Practical consequences for the planning desk: (a) an agreed **Basisablaufplan (Soll(0))** with document list is the reference curve — get it signed; (b) the Soll(1), Soll(2)... re-baselines + Ist overlay are only credible if the daily reports (§14) support them; (c) Anglo-American methods (as-planned-vs-impacted, time-impact, window analysis) inform but do not by themselves meet the local proof standard. **Oral warning before the first written notice** — same project, fewer lawyers.

### 13.4 The cost side — why the schedule is money

- **Time-dependent costs** (Vorhaltekosten: crane/containers/falsework standing, site management, financing/Bauzinsen, bond fees) accrue per week of extension → they are the money in a delay claim; **time-independent costs** (materials) don't — which is exactly why an extension of time and a cost claim are different animals.
- **Worked idle-crew figure (digested):** a 4-man formwork crew idled 2 working days × 9 h × 34.07 €/h loaded labour ≈ **2,453 €** — plus the Vorhalte of anything they were waiting on. Small numbers, multiplied by every crew-week, decide whether a claim is worth filing.
- Quantity deviations on unit-rate contracts: the ±10% band around the tender quantity is contractor risk; beyond it, unit prices re-form (§2(3) VOB/B family: reduced quantities → overhead recovery pushed onto the remainder on demand; increased → new price above 110%). Design changes/orders (§2(5)/§650b) and extra services (§2(6)/§650c: actual required costs + agreed mark-ups, or continuation from the deposited **Urkalkulation**) each carry their own notice duties — the AV desk tracks them in the change log from day 1.
- Interim billing discipline (Leistungsmeldung: measured quantities per position × EP, partly-done positions at completion %) is both cash flow and claim record.

---

## Section 14: Reporting, Documentation and As-Built Discipline

### 14.1 The reporting system (what to produce, at what frequency)

| Record | Owner / cadence | Content & rules |
|---|---|---|
| **Bautagebuch** (client diary, HOAI LPH 8) / **Bautagesbericht** (contractor daily report, ≥ weekly) | see §8.1 roles | weather + temperature; firms/workers present by trade incl. sickness; equipment; works vs LV positions; hindrances & quality issues; client visits/orders; plan/model deliveries — signed weekly. **Not a billing basis** (billing = plans + Aufmaß + hour sheets) but *the* reconstruction basis for claims and accidents |
| **Hour sheets** (Tages-/Wochenstundenberichte) | daily, submitted ≤ 3 days, 2 copies for signature | names + personnel no., total hours, task split per LV position **rounded to 0.25 h**; piece-work jobs also log material & device usage |
| **Machine daily report** | per machine | total hours split operation/maintenance/**standby** — standby is claim fuel (§13.4) |
| **Material report** | daily | in/out incl. third parties: supplier, delivery note no., qty+unit |
| **Photo discipline** | Polier daily + at every HP | date/project/path structure; scale visible; the pre-concealment photos (services before plaster, steel before pour, formation before blinding) are the ones nobody can re-take |
| **Drawing register** (Planeingangsliste) + minutes log | continuous | request/response dates; late drawings are a Behinderung with a date stamp |
| **Schedule versions** | baseline + updates per §4.1 | Soll(0)→Soll(n)→Ist stack |

### 14.2 Communication and file order

Every letter: date · author · addressee · number · subject. Document management (plans, correspondence, minutes) with one filing rule per job; the claim-defense/claim-mine file is assembled *during* the job (tender docs, baseline plan, deposited Urkalkulation incl. subcontractor prices at a depth that reveals price formation, minutes, daily reports, hour sheets, monthly progress by trade/element/level), not reconstructed afterwards.

### 14.3 As-built and handover (Übergabe nach Fertigstellung)

- As-built record (Bestandspläne incl. **concealed-services photo archive indexed by room/wall**), test certificates (concrete, pressure, flood, electrical), warranty/O&M docs, meter readings, keys, permits/completion notices to the authority, and the **Unterlage für spätere Arbeiten** (RAB 32 — access/anchor/roof-route info the future maintainer needs) form the handover pack.
- Abnahme mechanics that a planner must know: acceptance is the client's act (a Bauleiter/architect cannot accept without authority); only the client (or expressly authorised person) triggers it; VOB/B fiction after written completion notice (12 Werktage) where the client stalls without cause; **reserve known defects in the protocol** or the §634 Nr.1–3 rights (and any Vertragsstrafe) are lost at acceptance; a refused acceptance obliges a joint Zustandsfeststellung whose silence presumes later-caused damage.
- Retention/security release schedules (typically 5% performance → exchanged after completion for 3% warranty retention, or bank sureties throughout) are calendar items in the programme's tail — they decide the job's final cash, so the "close-out week" bar in §15 is genuinely work.

---

## Section 15: Worked Programme — Two-Storey House, Full Method Walk-Through

Basement + 2 storeys + pitched roof, ~150 m² footprint, in-situ walls/-columns + slab, masonry infill, **two full formwork sets**, spring start, 9-h days, working days (AT). Every duration below comes from the §2 tables with stated crew sizes — the model is reproducible.

### Step 1 — zones and activity list

BA-1 = basement, BA-2 = ground floor, BA-3 = upper floor + roof, then fit-out zones per floor. Activities per BA: formwork (walls) → rebar (walls) → pour → strip; falsework+slab formwork → slab rebar+cast-ins → HP-03 → pour → cure; then infill, roof, weather-tight, MEP first fix, screed, finishes.

### Step 2 — durations from the LSA tables (crew sizes in brackets)

| Activity | Qty | LSA | Crew | Ah | AT |
|---|---|---|---|---|---|
| BE + setting out | — | — | 2 + subs | — | 8 |
| Baugrube + Verbau (hybrid boxes) | 480 m³ | GL 35 m³/h + Verbau ahead | 3 + machine | — | 6 |
| Blinding + base-slab rebar | 4.6 t | 26 h/t | 4 | 120 | 3.3 |
| Base slab pour (pump) | 46 m³ | 0.6 h/m³ | 4 | 28 | 0.8 → 1 |
| Cure + strike walls at 3 d; backfill at 7 d | — | chemical | — | — | 5 wait |
| Wall formwork per floor (system) | 340 m² | 0.5 | 5 | 170 | 3.8 |
| Wall rebar per floor | 1.6 t | 14 | 3 | 22 | 0.8 |
| Wall pour per floor | 31 m³ | 0.9 | 4 | 28 | 0.8 |
| Slab formwork per floor | 150 m² | 0.55 | 5 | 83 | 1.8 |
| Slab rebar + cast-ins per floor | 3.1 t | 12–16 | 4 | 45 | 1.2 |
| Slab pour per floor (pump, single pour) | 45 m³ | 0.6 | 4 | 27 | 0.75 |
| Cure → strip soffit (props in) → release cascade | — | §12.2 | — | — | 3 + 5 wait |
| → **storey cycle with 2 sets** | | | | | **≈ 12–14 AT** |
| Roof structure + covering | — | timber sub | — | — | 12 |
| Windows delivery+install to weather-tight | — | lead 12 wk | — | — | 8 (install 3) |
| MEP first fix per floor | — | allowance | — | — | 10 + 8 |
| Screed (50 mm cement, UFH) + drying | — | §1.1 rates | — | — | 3 + ~25 wait |
| Plaster internal/external, painting, tiles, joinery, second fix, external works | — | fit-out phases | — | — | ~55–70 (overlapped) |
| Punch + tests + Abnahme | — | | | | 6 |

### Step 3 — the network, flattened

Serial hard core: BE(8) → dig(6) → base slab(5) → cure/backfill(5) → GF shell(13) → UG shell(13) → roof(12) → weather-tight(11 gate) → MEP1(18 parallel-ish) → screed+dry(28) → finishes(60 with 3-week internal overlaps by floor) → close-out(6) ⇒ **≈ 175–195 AT ≈ 37–41 calendar weeks**, i.e. the §1.2 band with the second storey included. The chemical waits (cure/drying) are ~30 AT — show them as bars.

### Step 4 — resource check

Peak crews: shell weeks = formwork 5 + rebar 3–4 + concrete 4 + machine gang ⇒ plot the Belegschaftskurve (§7.1): ramp 3→16→plateau 16→taper 8. If the plateau exceeds what the 6 m-wide jib and the 12 m² store can serve, cut Δt (the Takt, §6.2) — not the crews; two crews in one zone is where storey cycles die.

### Step 5 — version discipline from day 1

Soll(0) = this programme agreed in contract with the plan-delivery list; every change → Soll(1)... + daily reports; the winter (if the shell crosses Nov–Feb) already carries the §3.1 surcharge bar. When someone later says "you're three weeks late," the answer is a curve, not an opinion.

---

## Section 16: Common Scheduling & Site-Organisation Mistakes

Ranked by frequency × cost on residential/small-commercial jobs. Each has a section that prevents it.

| # | Mistake | Mechanism | Consequence | Prevention |
|---|---|---|---|---|
| 1 | **No agreed baseline schedule (Soll(0)) in the contract** | "we'll settle dates on site" | every slip becomes opinion; no extension, no claim, both sides lose | §4.2 — Basisablaufplan + plan-delivery list signed at award |
| 2 | **Long-lead items treated as site work** (windows, roof trusses, lift, pump booking) | bars modelled, deliveries not | job stalls warm and roofed waiting for glass | §2.7 procurement bars from week 1 of the programme |
| 3 | **Crane as bottleneck** — crew queue at the hook | hoist capacity never checked against Takt | worst loss type: paid labour idling while labour dominates cost | §7.1 / §9.4 crew-served limits; §8.2 coverage before layout |
| 4 | **Durations from optimism, not from LSA ÷ crew** | "always finished a floor in a week elsewhere" | every downstream bar floats away in week 3 | §2 — every bar traceable to quantity × LSA ÷ (K × 9) |
| 5 | **One storey cycle assumed regardless of formwork sets** | sets not counted | cycle silently doubles at floor 2 | §6.2 set-count formula; §1.2 the "one set vs two" duration jump |
| 6 | **Shoring decided by the digger operator on day 3** | no AV shoring choice | re-dig, surcharge incidents, DIN 4124 breach, weather-held open cut | §10 — method chosen in AV; §18.1 checklist line |
| 7 | **Prop removal on calendar days, not measured strength** | programme pressure at next-storey start | deflection/cracking (and worse) — and the engineer never signed | §12.2/§12.4 — release on test + written approval, back-props engineered |
| 8 | **Chemical waits hidden inside trade bars** | curing/drying made invisible | no float exists when someone asks to compress; weather claims unprovable | §4.1 — waits as own bars with lags |
| 9 | **Winter started without Winterbaukosten in the price** | season not modelled | January: unheated enclosure, no insulation stock, frozen formation, no claim | §3.1 — surcharge priced at tender or the cycle parked |
| 10 | **5-day/weekly plan skipped because "we have a Gantt"** | one static chart, no look-ahead | interfaces discovered at the gate: pump elsewhere, scaffold not out, no storage | §7.3 — the instrument, not the artefact, coordinates |
| 11 | **No daily reports/photos until the first dispute** | "admin later" | hindrance days unattributable; §6(2) extension fails for want of proof; §642 gone | §14 — reporting discipline from day 1 |
| 12 | **Storage of heaviest bulk outside crane reach** | BE drawn after the crane | double handling: every brick moved twice = LSA blown silently | §8.2/§8.3 mass-centre–working-field–road triangle |
| 13 | **Subcontractor float spent by the main schedule** | "they have 2 weeks spare" | those 2 weeks were their mitigation for their own risk | §5.2 — risky activities at early times; protect, don't consume, their float |
| 14 | **MEP first fix left out of the weather-tight gate** | trade sequence from old jobs | screed poured over untested pipes; chase-and-retest in finished rooms | §1.1/§12.3 HP-07 gate as written programme milestone |
| 15 | **Site power/water applications started in week 1** | assumed instant | most common stalled week 1; crews standing paid | §8.5 — media lines in the pre-construction phase |

---

## Section 17: Integration with FreeCAD / BIM (4D Sequencing)

When this skill is used alongside the BIM modelling skill:

1. **Model in construction order.** Site → building → storey → zone (BA) → element, created in §1.1 order; the model then filters by ConstructionStage and colours the programme onto the geometry (4D).
2. **Zone the model like the Takt.** Bauabschnitte exist in the model (properties/sections), or flow-line planning (§6) stays decorative.
3. **Model the temporary.** Crane + swing circle, site fence, containers, scaffold phases, Verbau — as real (low-LOD) objects with start/finish dates; they are the objects programmes actually collide over. A clash between a jib and a neighbour's roof or a scaffold tie and a window schedule is free to fix in the model and expensive on site.
4. **Model the cast-ins** (§1.5) as voids/embeds with pour dates; anything that exists only on the MEP drawing gets missed at HP-03.
5. **Attach durations, not just geometry:** object property sets = `LSA source, crew, AT, float, HP-ref` → the model answers "which wall is not yet poured on day 46" — that is the weekly plan (§7.3) from the other side.
6. **Cash-flow from quantities:** model quantities × unit rates = the Zahlplan curve (§7.4); quantities measured from the model keep billing and schedule on the same source.
7. **Never label the export as construction-ready** — same posture as the Reality Check: planning model until reviewed and contracted.

---

## Section 18: Checklists and Quick Reference

### 18.1 Pre-start checklist (the programme is ready when…)

- [ ] Baugenehmigung + notices (BaustellV Vorankündigung, BG registration, utility diversions) done or dated
- [ ] SiGeKo appointed; SiGePlan + GBs exist for the phases being tendered
- [ ] Baseline programme (Soll(0)) agreed with plan-delivery + long-lead list (windows 10–16 wk, roof 10–14 wk, pump booking, crane order)
- [ ] Ground report read; **shoring method + spoil disposal classes decided before the digger books** (DIN 4124 matrix §10.1–10.3)
- [ ] BE drawing: crane envelope covers store + work zones, truck route loops, cabins out of the slew, gate sightline, utilities ordered
- [ ] Control net fixed & protected: ≥2 plane references + ≥2 height connections outside dig/haul routes, Klaffungen within class limits, BKS origin + EPSG agreed in writing (§8A.1/8A.4/8A.6); Beweissicherung of neighbours logged with HP-01
- [ ] Survey QA flow staffed: who sets out vs who independently re-reads axes + Anschlusshöhe before first pour (§8A.9); model origin = BKS, control points in the `Vermessung` sheet/vertices (§8A.10)
- [ ] Durations traced to crew sizes (§2) with a named crew for every bar; chemical waits as visible bars
- [ ] Formwork set count vs storey cycle checked (§6.2); prop-release cascade with the TWS mapped (§12.2)
- [ ] Hold-point register (§12.3) issued to all parties with who-signs/notice-time
- [ ] Winter plan: heated-season concrete priced (Winterbaukosten in BGK) or the cycle parked; render window protected
- [ ] Daily-report + photo + hour-sheet regime started day 1 (§14)

### 18.2 Weather-season posture

| Window | Do | Avoid |
|---|---|---|
| Mar–Jun | excavate, foundations, shell | — |
| Jul–Aug | shell + roof; storm float on exposed work | long exposed cuts over weather fronts |
| Sep–Oct | weather-tight, external render/waterproofing | starting new slabs late Oct without winter plan |
| Nov–Feb | indoor fit-out; winter concrete only with priced protection | masonry/render/plaster below +5 °C; frozen backfill compaction |
| Mar thaw | re-verify formations & compaction | trusting last autumn's subgrade |

### 18.3 Quick-reference numbers

| Item | Value |
|---|---|
| Productivity formula | d = M × LSA ÷ (K × 9 h); machine work: d = M ÷ GL |
| Wall formwork (system) | 0.3–0.6 h/m² → ~75–110 m²/day per 5-crew |
| Slab formwork (panel+drop head) | 0.40–0.60 h/m² |
| Rebar placing | slabs 9–25, walls 12–27, columns 15–30 h/t |
| Concrete (pump) | slabs 0.3–0.8, walls 0.35–1.4 h/m³; crane skip ≈ +25% |
| Striking (Ausschalfristen, normal temp) | walls/columns 1–3 d; slabs 3–8 d; **measured strength + written release governs loading** |
| Storey cycle | ≈ 1 week multi-storey (2+ sets, crane-served); ≈ 12–14 AT per floor at house scale |
| Excavator planning output | trench 4–20 m³/h; pit 500–1000 m³/day; QA ≈ 0.6 × catalogue QB |
| Tower crane monthly output | pumped 3000–4000 m³/month; crane+skip ≈ 2000; crews served 15–30 (§9.4) |
| DIN 4124 unsupported cut | 1.25 m (non/stiff-cohesive boundary at 1.75 m with 45° bench above 1.25) |
| Crest surcharge setback | 0.6–2.0 m table (§10.2); machines ≥ 1.5 m or count as load |
| Side protection EN 13374 | top rail + mid rail + 15 cm toe board; falls fatal even < 2 m |
| First aid | 1 Ersthelfer / 2–20 present; > 20 → ~10%; kit ≤ 100 m/1 floor |
| CPM | ES/EF forward (max), LS/LF backward (min); TT = LS−ES; FF = ES(succ)−EF−lag−1; TT=0 ⇒ critical |
| Flow line | T = (n + m − 1)·Δt; sets ≈ (cast→strike→return)/Δt |
| Idle-crew claim math | crew × days × 9 h × Mittellohn + Vorhaltekosten (§13.4) |

### 18.4 The two sentences to say when the programme is argued with

> *"Which dependency are we compressing — physical, chemical, inspection, or preferential? Only the last one is free, and we protect it in writing."*

> *"This is a planning model, not a stamped schedule — durations, shoring, crane picks and prop releases need the responsible engineers' review, and dates bind only through the contract actually agreed."*

### 18.5 Standards & rules index (dated editions — VERIFY current text before quoting)

| Rule/standard | Governs here |
|---|---|
| **VOB/B §§2, 5, 6, 11, 12, 13, 14, 16** (edition 2019+ — check adoption) | schedule interface: orders, quantities, hindrance/extension, penalties, Abnahme, payment |
| **VOB/C ATV DIN 18299 + trade ATVs** (18300 earth, 18330 masonry, 18331 concrete, 18336 waterproofing, 18350 plaster, 18353 screed, 18451 scaffold...) | recognised rules, Neben-/Besondere Leistungen, measurement |
| **DIN EN 13670 / DIN 1045-3** | concrete execution incl. winter provisions (cited by practice; **VERIFY clause detail — not fully digested**) |
| **DIN 18218** | fresh-concrete pressure (γ 25 kN/m³, trapezoid, rise ≤ 7 m/h logic) — formwork/prop design input |
| **DIN 4124 / DIN 4123 / EAB / DIN EN 1997-1+NA** | trench limits, adjacent excavations, shoring design |
| **ZTV E-StB / DIN 18134** | compaction degrees & plate tests (transferred to building backfill) |
| **BaustellV + RAB 30/31/32/33** | SiGeKo, SiGePlan, Vorankündigung, Unterlage |
| **ArbSchG, BetrSichV, ArbStättV/ASR A4.1, DGUV rules (BG BAU)** | GB, PPE, welfare, accident insurance system |
| **EN 13374 / EN 12810-12812 / EN 1065 / EN 16031 / EN 13377 / DIN 18216** | side protection, scaffolds/falsework, props, beams, ties |
| **BGL (Baugeräteliste) + machine catalogues** | equipment rates/outputs — digested catalogue data 1994–2017, **refresh before pricing (VERIFY)** |
| **HOAI LPH 8 (fee freely negotiable since 2021)** | Bauüberwachung duties incl. schedule upkeep |
| **DIN 276:2018** | cost/quantity structure feeding the programme's money curve |
| **DIN 18710-x (Ingenieurvermessung) / DIN 18709 / DIN 18703 / DIN 18202** | execution surveying quality parts, terms, levelling staffs, building tolerances (§8A; cited editions 1996–2013 — VERIFY current) |

---

*End of skill. Companion files: `construction-scheduling-site` (trade-level execution order, finishing gates), `geotechnics-foundations` (ground model, Verbau design, Wasserhaltung), `construction-cost-management-din276` (rate build-up that consumes the LSA tables here), `construction-freecad-bim` (4D tagging of this programme onto the model).*
