---
name: architecture-spatial-planning
description: >
  Residential spatial planning calibrated to Pakistani house design: marla/kanal
  plot geometry, LDA/CDA ground coverage, FAR and setback-driven massing, room
  sizing minimums and built-practice targets, area budgeting against a client
  brief, circulation, door/window and passage sizing, staircase geometry and
  placement, courtyard and light-well proportioning by solar altitude,
  climate-driven orientation, shading and window-to-wall ratios for Pakistan's
  hot-dry and hot-humid zones, wet-zone stacking and structural-grid
  coordination, net-to-gross efficiency, worked plans for 5 marla to 2 kanal,
  and a FreeCAD/BIM handoff checklist. Retains general plan-archetype,
  daylight-depth and legibility theory, re-weighted from towers to houses.
---

# Spatial Planning for Houses (Pakistan-Calibrated)

This skill turns a plot (5 marla to 2 kanal) into a dimensionally defensible house plan: how big the plot really is, how much of it may legally be covered, how many floors the FAR permits, whether the client's brief even fits, how large each room should be, how wide the passages and stairs must be, where the courtyard and staircase go, and which way the house should face for sun and wind. Every number is tagged with its evidentiary tier (Section 0) so a legally binding bylaw figure is never confused with an imported reference minimum, a practitioner habit, or — critically — a figure this skill itself could not verify.

Use it before modelling anything in FreeCAD (`architecture-freecad-bim`), before drawing a plan in `drawio-diagrams`, and alongside `architecture-structural-systems` (spans, wall thickness, grids), `architecture-building-typology` (house form and unit configuration), `architecture-accessibility-design` (clear widths, aging in place) and `architecture-seismic-design` / `architecture-building-codes-permits` (plan-configuration seismic risk and the authoritative bylaw text — see Sections 2.6 and 9.5 below for why this skill cannot stand alone on either).

---

## Reality Check - Licensing & Liability

**This skill produces design aids and calculation guidance for planning and FreeCAD modelling ONLY.**

- Nothing in this file is a construction document, a structural calculation, or an approved plan.
- Any design intended for actual construction of a real occupied building **MUST be reviewed and stamped by a licensed engineer/architect registered with the relevant authority** — in Pakistan, a **PEC-registered engineer** for structure and services, and a **PCATP-registered architect** for architectural drawings.
- The design **MUST go through local authority plan approval** before construction — LDA (Lahore), CDA (Islamabad), RDA (Rawalpindi), KDA/SBCA (Karachi), PDA (Peshawar), the relevant TMA/Cantonment Board, or the private scheme's own building control (DHA, Bahria Town). **Their current bylaw schedule overrides every coverage, FAR and setback number printed here — including, and especially, the ones flagged UNVERIFIED below.**
- **Claude must never present FreeCAD output or these calculations as construction-ready.** No massing study, no room-size table, no stair calculation, no courtyard proportion from this skill is buildable as-is.
- If a user appears to be treating the output as final — talking about pouring a plinth, ordering steel, briefing a contractor, or submitting to an authority — **say so unprompted, in that reply**, and state plainly: *"This is a planning study. It needs a PEC-registered engineer's stamp and LDA/CDA/TMA approval before anyone builds from it."*
- Seismic, soil-bearing, water table, sewerage/septic capacity, and fire safety are **out of scope for final design** here. This skill DOES flag plan-configuration seismic risk (Section 2.6, 9.5) because plan shape is decided in this document and cannot be undone later — but the actual seismic calculation is the engineer's and `architecture-seismic-design`'s territory, not this skill's.

---

## Section 0: Evidentiary Tiers — Which Numbers Are Law

Pakistan has **no single authoritative residential-scale numeric building code**. BCP 2007 and the BCP 2021 Final Draft are dominated by structural and seismic provisions; they do not give you minimum bedroom areas, kitchen sizes, corridor widths, or bathroom clearances. Real numbers must therefore be triangulated from tiers with **different evidentiary status**. Always state the tier when quoting a number to a client — and never round an unverified number up to a more confident tier than it earned.

| Tier | Label | Source | Status | Use for |
|---|---|---|---|---|
| **T1** | **Legally binding** | LDA / CDA / RDA / SBCA / DHA / Bahria bylaws, sourced and current | Enforceable; approval fails without it | Ground coverage %, FAR, setbacks, height limit, mumty allowance, parking |
| **T1-U** | **Legally binding, but UNVERIFIED by this skill** | Same category of source, but this document could not confirm the figure against a citable, dated bylaw document | **Treat as a planning placeholder only — confirm against the authority's current published schedule before it is used for anything beyond a first-pass massing study** | Nothing should be quoted to a client or built into a FreeCAD massing check without re-confirming — see 2.1 and 2.4 |
| **T2** | **Nearest codified reference** | NBC India 2016 (Parts 3 & 4), IS 456 | **NOT Pakistani law.** De facto reference used by Pakistani practitioners where local code is silent | Habitable-room / kitchen / bath minimum areas, ceiling heights, stair riser-tread |
| **T3** | **Imported baseline** | IRC (US) R311, IBC Ch.10 | Not applicable in Pakistan; useful floor value only | Hallway/stair clear-width sanity floor, emergency-escape window logic |
| **T4** | **Vernacular / built practice** | Measured Pakistani house plans, market norms | No legal force; reflects client expectation | Actual bedroom/kitchen/passage sizes people expect, porch sizes, servant quarters |
| **T5** | **Climate-science-backed** | Peer-reviewed Pakistan/South Asia studies | Empirical performance data, not code — **quote the study's own metric, not a rounded-up restatement of it** | Courtyard proportions, orientation angles, cooling-load reduction |

**Hard rule:** never present a T2 or T3 number as if it were Pakistani law, and never present a **T1-U** number as if it had the same standing as a sourced **T1** number. Say *"NBC India 2016 sets 7.5 m² as the minimum habitable room — Pakistan has no equivalent clause, and Pakistani practice builds far larger anyway,"* and say *"LDA's coverage/FAR figures below are the best available secondary-source table, flagged unverified — pull the current LDA schedule before this goes into a submission drawing."*

**T4 runs measurably more generous than T2/T3.** A Pakistani house is commonly built with 7 ft passages against an IRC 3 ft minimum, and 12×14 ft bedrooms against NBC's 7.5 m² (81 sq ft ≈ 9×9 ft). Designing to the codified minimum in Pakistan produces a house that reads as substandard to the client even though it is technically compliant. **Design to T4; verify against T1 (or T1-U, re-confirmed); cite T2/T3 only as a floor.**

---

## Section 0.5: The Working Sequence

Do these in order. Skipping step 1 or 2 wastes every downstream decision, because the envelope determines the brief, not the other way round.

```
1. CONFIRM THE PLOT      Marla basis (272.25 vs 225)? Dimensions? Which side is the road?
                         → Section 1.  Never assume the basis. Ask.
2. FIX THE ENVELOPE      Authority + plot band → coverage %, FAR, setbacks, mumty, height.
                         → Section 2.  Re-confirm every T1-U figure against the authority's
                           current published schedule before treating it as final.
3. TEST THE BRIEF        Sum the client's rooms at T4 sizes vs available carpet.
                         → Section 3.8.  If it does not fit, resolve it NOW, not in plan.
4. FIX ORIENTATION       City → latitude, prevailing wind, buffer facade.
                         → Section 7.  Free at this stage, impossible to retrofit.
5. PICK THE ARCHETYPE    Frontage + coverage + climate + rental intent + seismic regularity.
                         → Section 8.9 decision tree, cross-checked against 2.6.
6. PLACE THE STAIR       Before any room. It is the most constrained object in the plan.
                         → Section 5.  Compute risers from the real F2F.
7. PLACE THE COURTYARD   Size by W/H against city solar altitude; check it as a diaphragm cut.
                         → Section 6, 2.6.  On <7 marla accept a light well, do not fake a courtyard.
8. LAY OUT ROOMS         T4 sizes, wet zones stacked, buffer rooms on the bad facade.
                         → Sections 3, 9.
9. VERIFY                Coverage, FAR, circulation %, NTG, stacking, escape windows, W/H,
                          plan regularity.
                         → Sections 10, 13, 14.  Compute; do not eyeball.
10. STATE THE CAVEAT     Planning study, needs PEC stamp + authority approval — attach it to
                          the specific risky decisions (courtyard cut, L-shape, split level),
                          not only as a closing paragraph.
```

**Rule:** never move to step 5 with step 2 unconfirmed. "I'll assume 70% coverage" is how a plan gets rejected after it is drawn.

---

## Section 1: Plot Geometry — Marla, Kanal, and the 17% Trap

### 1.1 The two marla standards

| Basis | 1 Marla | Where it applies |
|---|---|---|
| **272.25 sq ft** (30.25 sq yd, 25.29 m²) | Standard | Most new Islamabad societies, general/legal usage |
| **225 sq ft** (25 sq yd, 20.90 m²) | ~17% smaller | Many older schemes, and commonly quoted in DHA / Bahria / older LDA contexts |

**1 Kanal = 20 Marla. 8 Kanal = 1 Acre.**

**Never start a plan without confirming which basis the plot deed uses.** A "10 marla" plot is either 2,722.5 sq ft or 2,250 sq ft — a 472 sq ft (17%) difference, roughly one whole bedroom plus a bath. Ask; do not assume.

### 1.2 Plot area by basis

| Plot | 272.25-basis (sq ft / m²) | 225-basis (sq ft / m²) |
|---|---|---|
| 3 Marla | 816.8 / 75.9 | 675.0 / 62.7 |
| 5 Marla | 1,361.3 / 126.5 | 1,125.0 / 104.5 |
| 7 Marla | 1,905.8 / 177.0 | 1,575.0 / 146.3 |
| 10 Marla | 2,722.5 / 252.9 | 2,250.0 / 209.0 |
| 1 Kanal | 5,445.0 / 505.9 | 4,500.0 / 418.1 |
| 2 Kanal | 10,890.0 / 1,011.7 | 9,000.0 / 836.1 |

### 1.3 Common built plot dimensions (T4)

| Plot | Typical dimensions (ft) | Frontage : depth | Planning consequence |
|---|---|---|---|
| 3 Marla | 20×41, 25×33 | 1:2.05 / 1:1.32 | Single-bay; stair on side wall; no courtyard possible, use a light shaft |
| 5 Marla | **25×50**, 25×54.5, **30×45** | 1:2.0 / 1:1.5 | 25 ft frontage = one room + passage across the front. 30×45 is materially easier to plan than 25×54.5 |
| 7 Marla | 30×63.5, 35×55 | 1:2.1 / 1:1.57 | Two rooms across the width becomes possible at 35 ft frontage |
| 10 Marla | **35×70**, 35×77.8, 40×68, 30×90 | 1:2.0 | Two-bay plan; central passage; small courtyard viable |
| 1 Kanal | **50×90**, 50×108.9, 60×90 | 1:1.8 / 1:1.5 | Three-bay plan; real courtyard; separate mardana/guest wing |
| 2 Kanal | 75×145, 100×109 | 1:1.93 / 1:1.09 | Near-square; courtyard-centred or pavilion plan; detached servant block |

**Frontage is the binding constraint, not area.** At 25 ft frontage minus two 9-inch external walls you have 23.5 ft internal. One 12 ft room + 4 ft passage + 7 ft bath = 23 ft: that is the entire width. A 30 ft frontage on the same area (30×45) buys 28.5 ft internal and changes the plan from linear to two-bay. **When a client can choose between 25×54.5 and 30×45 for the same 5 marla, recommend 30×45.**

### 1.4 Frontage → plan structure lookup

| Internal clear frontage | What fits across the width | Plan type forced |
|---|---|---|
| < 20 ft | one room OR a room + stair | Linear, stair on party wall, no passage across |
| 20–23.5 ft (25 ft plot) | one 12–14 ft room + 4 ft passage + 5 ft bath | Linear / side-passage (8.1) |
| 26–28.5 ft (30 ft plot) | 14 ft room + 4 ft passage + 9 ft room OR 12+4+12 | Linear with a second shallow bay |
| 33.5 ft (35 ft plot) | 14 + 4.5 + 14 ft | True central-passage (8.2) |
| 38.5 ft (40 ft plot) | 14 + 4.5 + 14 + 5 ft services strip | Central-passage + L-yard (8.4) |
| 48.5 ft (50 ft plot) | 16 + 14 courtyard + 16 ft | Real courtyard plan (8.3) |

Deduct **1.5 ft total** for two 9-inch external walls, plus 0.4 ft for each 4.5-inch internal partition crossed.

### 1.5 Orientation nomenclature

Plots in Pakistan are described by the road side: an "east-open" plot has its road/entrance on the east. This determines both the entrance sequence and the solar exposure of the front facade — see Section 7. **East-open and north-open plots are the most planning-friendly in Punjab and KP; west-open is the hardest (afternoon sun on the entrance facade).**

---

## Section 2: Coverage, FAR and Setbacks — The Legal Envelope

### 2.1 LDA (Lahore) ground coverage and FAR by plot band — STATUS: T1-U, UNVERIFIED

> **This table is flagged T1-U, not T1.** The figures below were assembled from secondary practitioner sources and could not be checked against a dated, citable LDA bylaw document. They also fail an internal sanity check: the smallest band shows a **higher** coverage cap (80%) but a **lower** FAR (1:1.18) than the next band up (75% coverage, 1:1.8) — meaning this table implies the smallest plots get more ground coverage but proportionally *less* total buildable floor area than a slightly larger plot. Real coverage/FAR schedules do not typically behave this way (smaller plots are usually given comparable or better FAR headroom to compensate for their smaller footprint, not worse). **Do not use this table for a submission drawing, a client-facing envelope commitment, or as ground truth in a FreeCAD massing check without first pulling LDA's current published Building Regulations and replacing these numbers.** Treat everything downstream in this file that uses this table (Section 2.2, the massing decision tree, Section 12 worked examples) as a **methodology demonstration using placeholder numbers**, not a verified massing result.

| Plot band | Max ground coverage | FAR |
|---|---|---|
| Below 5 Marla | 80% *(unverified — see note above)* | 1 : 1.18 *(unverified — internally inconsistent, see note above)* |
| 5 – 10 Marla | 75% *(unverified)* | 1 : 1.8 *(unverified)* |
| 10 Marla – 1 Kanal | 70% *(unverified)* | 1 : 1.5 *(unverified)* |
| 1 – 2 Kanal | 65% *(unverified)* | 1 : 1.4 *(unverified)* |

**Before using this table for anything but a placeholder study:** pull the current LDA Building Regulations (or the specific scheme's own conditions — DHA/Bahria publish their own, often stricter, schedules) and replace every figure in this table. If the source cannot be dated and cited, keep the T1-U flag and say so to the client in the same sentence you quote the number.

### 2.2 What those (unverified) numbers would permit, IF confirmed

Worked, on the 272.25 sq ft marla basis, **using the T1-U placeholder figures above — re-run this table with confirmed T1 numbers before relying on it**:

| Plot | Plot area | Max footprint | FAR cap (total covered) | G+1 covered | Floors FAR allows | Mumty allowance (9–13% plot) |
|---|---|---|---|---|---|---|
| 5 Marla | 1,361 sq ft | 1,021 sq ft (75%) | 2,450 sq ft | 2,042 sq ft | 2.40 | 123–177 sq ft |
| 7 Marla | 1,906 sq ft | 1,429 sq ft (75%) | 3,430 sq ft | 2,859 sq ft | 2.40 | 172–248 sq ft |
| 10 Marla | 2,723 sq ft | 1,906 sq ft (70%) | 4,084 sq ft | 3,811 sq ft | 2.14 | 245–354 sq ft |
| 1 Kanal | 5,445 sq ft | 3,811 sq ft (70%) | 8,168 sq ft | 7,623 sq ft | 2.14 | 490–708 sq ft |
| 2 Kanal | 10,890 sq ft | 7,079 sq ft (65%) | 15,246 sq ft | 14,157 sq ft | 2.15 | 980–1,416 sq ft |

**Reading the table (methodology, valid regardless of the exact numbers once confirmed):** for every band, **coverage binds the footprint and FAR binds the floor count.** G+1 (ground + first) is comfortably legal in every band shown. G+2 breaches FAR in every band shown — a third full-footprint floor requires either a reduced third-floor plate or a different plot band. The mumty (stair tower / rooftop room) is typically allowed **on top of** the coverage limit at 9–13% of plot area; it is the legitimate way to get a rooftop room without a third storey. **Re-derive this table once 2.1's figures are confirmed — the row-by-row arithmetic pattern will hold, the exact numbers may not.**

**Massing decision tree:**

```
Client wants N sq ft of covered area on a plot of area A
        │
        ├─ N ≤ A × coverage%              → single storey, done. Maximise courtyard.
        ├─ N ≤ 2 × (A × coverage%) and N ≤ A × FAR
        │                                  → G+1 at full footprint
        ├─ N ≤ A × FAR but > 2 × footprint
        │                                  → G+1 full + partial 2nd floor
        │                                    (2nd floor plate = A×FAR − 2×footprint)
        └─ N > A × FAR                     → ILLEGAL. Options:
                                             (a) reduce brief
                                             (b) basement (often excluded from FAR —
                                                 CONFIRM with the authority; see 2.4a
                                                 for when this is not feasible)
                                             (c) buy the next plot band
```

**Basement:** frequently excluded from FAR when used for parking/services and when the ceiling sits below a defined height above natural ground. This is the single biggest lever on a tight plot — **but it is authority-specific and must be confirmed in writing before it is designed in.** See 2.4a for the water-table feasibility check that must run alongside the FAR-exemption check — a basement can be legally FAR-exempt and still physically the wrong move.

### 2.3 Setbacks — legal minimums vs common construction practice

**Two different kinds of number are at risk of being conflated here — keep them apart.**

**(a) T1-U legal setback minimums** (indicative, unverified — confirm locally before use):

| Plot band | Front | Rear | Sides |
|---|---|---|---|
| 5 Marla (RDA / typical private scheme) | 5 ft | 5 ft | *(see note b — do not read as "0 ft required")* |
| 7–10 Marla | 5–10 ft | 7–10 ft | ≥5 ft on at least one side |
| 1 Kanal | 10–20 ft | 10 ft | 5–10 ft each side |
| 2 Kanal | 20–25 ft | 10–15 ft | 10 ft each side |

**(b) Common construction practice, NOT a bylaw figure:** on many 5-marla schemes, houses are built wall-to-wall with **no side setback at all**, sharing a party wall with the neighbour on both sides. **This is a private-scheme construction pattern, not a legal side-setback requirement of "0 ft."** Some schemes' bylaws technically require a minimum side gap that is routinely not observed; others explicitly permit zero side setback below a plot-size threshold. **Never tell an authority or a client "the setback is zero" as if that were a confirmed legal minimum — say "party-wall construction is common practice on this plot size; the scheme's own bylaw on side setback must be checked before assuming it."**

**Setbacks and coverage interact — check both, adopt the smaller footprint.** On a 30×45 ft plot with 5 ft front and rear setbacks, the setback-buildable area is 30×35 = 1,050 sq ft, but 75% coverage caps you at 1,013 sq ft. Coverage binds. On a 50×90 ft plot with 15 ft front, 10 ft rear and 7 ft sides, setbacks give 36×65 = 2,340 sq ft while 70% coverage would allow 3,150 sq ft. **Setbacks bind.** Always run both, and always re-confirm both against the current authority schedule — this entire section is T1-U.

**Practice note:** on 5 marla, actual ground coverage frequently reaches 80–85% (≈1,100 sq ft on a 1,361 sq ft plot) — i.e. above the nominal 75%. That is a widespread compliance gap, **not a licence**. Design to the published figure and let the client decide, with the deviation stated explicitly.

### 2.4 CDA / Islamabad — STATUS: T1-U, UNVERIFIED

- Low-density sectors (e.g. Gulberg Greens-type): ground coverage reportedly capped at **20–25%**, leaving 75–80% for landscape and open space. **This figure has no citable regulation number, gazette date, or URL behind it in this document — it is a secondary-source claim, flagged T1-U exactly like the LDA table in 2.1, and must be pulled from CDA's own bylaw document before it drives any real massing decision.** This is a completely different design problem from a Lahore 5 marla — the house is a pavilion in a garden, not a plot-filling block, **if the figure holds up**.
- Commercial main-boulevard FAR is reported at **1:10 to 1:12**; residential FAR is plot-size dependent, not a flat number. Same T1-U flag applies.
- CDA setback schedules are enumerated in CDA's own bylaw PDF; secondary sources are unreliable on exact footages. **Pull the source document — do not cite "CDA Islamabad Building Regulations 2026" or any other dated title unless you can produce the regulation number and the actual document.**

### 2.4a Basement feasibility vs water table (missing from the FAR-lever discussion above)

A basement being FAR-exempt (2.2, option b) is a legal question. Whether it is *buildable at reasonable cost* is a separate, physical question that must be checked before recommending it as the fix for a brief that overshoots FAR:

| City / area | Water table situation | Basement implication |
|---|---|---|
| Coastal Karachi (DHA Phase 8, Clifton, Defence near the coast) | High water table, often within a few feet of grade | Basement usually infeasible or requires expensive permanent tanking/dewatering — **do not offer it as the default FAR-lever here** |
| Lahore (older, low-lying sectors; monsoon season) | Seasonally high water table | Basement feasible most of the year but needs full waterproofing/tanking design; flag the seasonal risk, do not assume year-round dry excavation |
| Islamabad, Rawalpindi, most of Punjab uplands | Generally lower, more stable water table | Basement usually the most viable FAR-lever of the three cities in this table |
| Any site near a canal, drain, or low-lying flood-prone pocket | Locally elevated water table regardless of city | Always ask for the plot's own soil report before recommending a basement — city-level generalisation is not enough |

**Rule:** before recommending a basement to solve a FAR shortfall, ask (1) is it FAR-exempt here — in writing, and (2) what is the water table on THIS plot — from a soil report or, failing that, from neighbours' basement experience on the same street. Recommending a basement on an unchecked high-water-table plot is a planning error that surfaces expensively at excavation, not at design review.

### 2.5 Non-negotiable open space, whatever the bylaw allows

Even where 80% coverage is legal, reserve:
- **Rear open space ≥ 5 ft × full width** — kitchen light and ventilation, washing area, water tank access, sewer chamber access. A kitchen with no rear opening is unworkable in Pakistan.
- **A light shaft ≥ 4 ft × 4 ft** for any internal bathroom on a party-wall plot.
- **Car standing** — 9×18 ft per car minimum (Section 3.7). If the porch is inside coverage, it eats a room.

### 2.6 Plan-configuration seismic risk — what THIS skill controls, and must not wave past

Detailed seismic design (base shear, ductility detailing, member sizing) is `architecture-seismic-design`'s job and a PEC-registered engineer's sign-off, not this skill's. **But plan shape is decided here, in spatial planning, and a bad shape decision cannot be fixed later without a re-plan.** Islamabad and Peshawar sit in a real seismic zone (BCP-SP 2007 Zone 2B/3 territory); Lahore and Multan are lower but not zero. Apply these plan-level regularity rules whenever choosing an archetype (Section 8.9):

| Plan-level decision made in this skill | Seismic consequence if ignored | Simple mitigation at the planning stage |
|---|---|---|
| **L-shaped plan (8.4)** — a re-entrant corner | Torsional irregularity: the two wings vibrate somewhat independently in an earthquake, concentrating stress at the inside corner of the L | Keep each wing's plan aspect ratio ≤ 1:3, or introduce a seismic separation joint at the re-entrant corner on larger (1 kanal+) L-plans — flag this explicitly to the structural engineer, do not leave it implicit |
| **Open courtyard (8.3, 6.x)** as a hole in the floor diaphragm | A large central opening reduces the diaphragm's ability to distribute lateral load between the wings around it — effectively the same torsional problem as an L-plan, worse if the courtyard is off-centre | Keep the courtyard centred on the plan's geometric centre where possible; size the edge beam around it generously (9.4 already requires an edge beam on all four sides — treat that requirement as seismic-driven, not just gravity-driven, and say so to the engineer) |
| **Pavilion / detached plan (8.6)** with long thin wings | Long, narrow wings have a soft/weak axis in the short direction | Keep wing width:length inside roughly 1:3–1:4; avoid a single-room-wide wing longer than ~30 ft without an intermediate shear wall or cross-wall |
| **Split-level plan (8.7)** on sloping ground | Mid-height floor offsets create a soft-storey-like discontinuity in the lateral load path between half-levels | Avoid split-level entirely on sites in Zone 3 (Islamabad hills, Murree) for anything beyond a single half-level step; if unavoidable, flag it explicitly for the engineer to detail a continuous lateral system across the offset |
| **Column stranded off-grid (9.4 rule 1)** | Irregular load path, same failure mode as everywhere else in this list | Already covered in 9.4 — repeated here because it is also a seismic issue, not only a gravity/cost issue |

**Rule for this skill's output:** whenever Section 8.9's decision tree lands on an L-shape, a courtyard, a pavilion with long wings, or a split-level, **say so explicitly in the plan handoff** — e.g. *"This plan has a re-entrant L-corner / a central courtyard cut / a split-level offset — flag this specifically to the structural engineer for seismic plan-irregularity review, not just general structural sign-off."* This is a plan-configuration sanity check, not a substitute for `architecture-seismic-design` or the engineer's actual analysis.

---

## Section 3: Room Sizing — Minimums vs What People Actually Build

### 3.1 Codified minimums (T2 — NBC India 2016, nearest South Asian reference; Pakistan is silent)

| Space | NBC minimum | In sq ft | Note |
|---|---|---|---|
| Habitable room (single-room dwelling) | 9.5 m² | 102 sq ft | Absolute floor |
| Other habitable rooms (bedroom, living, dining) | 7.5 m² | 81 sq ft | ≈ 9×9 ft |
| Kitchen, separate | 5.0 m² | 54 sq ft | 4.5 m² if a separate store is provided |
| Kitchen + dining combined | 7.5 m² | 81 sq ft | |
| Bathroom (bath only) | 1.8 m² | 19 sq ft | |
| Water closet only | 1.1 m² | 12 sq ft | |
| Combined bath + WC | 2.8 m² | 30 sq ft | ≈ 5×6 ft |
| Ceiling height, habitable rooms | 2.75 m | 9'-0" | Bedroom, living, dining, kitchen |
| Ceiling height, bath/WC | 2.10 m | 6'-11" | |
| Window area, habitable room | ≥ 1/10 of floor area | | Openable for ventilation |

### 3.2 Pakistani built-practice targets (T4) — design to these

| Space | 5 Marla | 7 Marla | 10 Marla | 1 Kanal | 2 Kanal |
|---|---|---|---|---|---|
| Master bedroom | 12×14 | 13×15 | 14×16 | 16×18 | 18×20 |
| Bedroom 2 / 3 | 11×12 | 12×13 | 12×14 | 14×16 | 16×16 |
| Guest bedroom | 12×12 | **12×14** | **12×14** | 14×16 | 16×16 |
| Drawing room (formal guest) | — (merged) | 12×14 | 14×16 | 16×20 | 18×24 |
| Lounge / family living | 12×14 | 13×16 | 14×18 | 18×22 | 20×26 |
| Dining | in lounge | 10×12 | 11×13 | 14×16 | 16×18 |
| Kitchen | **7'0"×9'6"** | 8×11 | 9×12 | **16×16** or **18×12** | 14×18 |
| Dirty / wash kitchen | — | — | 6×8 | 8×10 | 10×12 |
| Attached bath (WC+basin+shower) | 5×8 | 5×8 | 6×8 | 6×9 | 7×10 |
| Common bath | 5×7 | 5×7 | 5×8 | 6×8 | 6×9 |
| Powder / guest WC | 3×5 | 3×5 | 3'6"×6 | 4×6 | 4×7 |
| Store | 4×6 | 5×6 | 6×8 | 7×9 | 8×10 |
| Utility / laundry | — | — | 6×8 | 7×9 | 8×10 |
| Servant room + bath | — | — | 8×10 + 4×6 | 10×12 + 5×7 | 12×12 + 5×8 |
| Stair well (dog-leg) | 7×12 | 7×12 | 8×13 | 9×14 | 10×15 |
| Car porch | 9×18 (1) | 9×18 (1) | 16×18 (2) | 18×20 (2) | 18×36 (4) |

All dimensions in **feet**, internal clear.

**The gap between 3.1 and 3.2 is the point.** NBC's 81 sq ft bedroom is 9×9 ft. Nobody in Pakistan accepts a 9×9 ft master bedroom in a 10 marla house. Quote 3.2 to clients; keep 3.1 only to prove a tight room is not sub-code.

### 3.3 Furniture-driven minimums (why the T4 sizes are what they are)

**Bedroom** — a king bed is 6'0"×6'6"; queen 5'0"×6'6".
- Circulation one long side: **30 in (2'6")** comfortable, 24 in absolute.
- Circulation second long side: **24 in** minimum.
- Foot of bed to wall/wardrobe: **36 in** if a wardrobe door opens there, 30 in otherwise.
- Wardrobe: 24 in deep + **36 in** standing clearance to open and reach.
- Minimum workable master with king bed + wardrobe wall: `6'0" bed + 2'6" + 2'0" = 10'6"` wide × `6'6" bed + 3'0" + 2'0" wardrobe = 11'6"` deep. **This is why 12×14 is the practical floor, not 9×9.**

**Kitchen** — counter depth 24 in, upper cabinet depth 12–14 in.
- Single-cook aisle: **42 in (3'6")**. Two-cook / family kitchen: **48 in (4'0")**.
- Work triangle (sink–hob–fridge) perimeter: **13–26 ft**; under 13 ft is cramped, over 26 ft is a walking exercise.
- A 7'0"×9'6" 5-marla kitchen = single-run counter along the 9'6" wall with a 42 in aisle. It works, but only as a single-cook galley.
- 16×16 kitchens on 1 kanal are island-capable: island needs **42 in clear on all working sides**.

**Bathroom** — WC clear width **30 in**, clear in front **24 in** (IRC 21 in absolute).
- Basin: 30 in wide × 21 in deep, 30 in clear in front.
- Shower: **36×36 in** minimum, 36×48 comfortable.
- Minimum 3-fixture bath: 5×8 ft. Below that, split WC and bath.

**Dining** — 30 in per seated person along the table edge; **36 in** behind a chair to pull out and pass (24 in to pull out only).
- 6-seat table 3×6 ft + 3 ft all round = **9×12 ft room**.
- 8-seat table 3'6"×8 ft + 3 ft all round = **9'6"×14 ft room**.

**Drawing room (Pakistani formal sofa set)** — a 3+2+1+1 set plus centre table needs a clear rectangle of about **11×13 ft**; that is the real reason the T4 drawing room starts at 12×14 and not at NBC's 9×9.

### 3.4 Ceiling heights (T4 with T2 floor)

| Space | NBC min (T2) | Pakistani practice (T4) |
|---|---|---|
| Habitable rooms | 2.75 m (9'-0") | **3.05–3.35 m (10'-0" to 11'-0")** |
| Drawing/double-height feature | — | 3.66–4.88 m (12'–16') |
| Bath / WC / store | 2.10 m (6'-11") | 2.44–2.75 m (8'–9') |
| Under-beam clear | — | keep ≥ 2.13 m (7'-0") at doors |

Higher ceilings are a genuine passive-cooling measure in Punjab and Sindh — hot air stratifies above the occupied zone. The traditional 12 ft ceiling is not just ornament. Cost: each extra foot of height adds masonry, plaster, column length and stair risers.

**Floor-to-floor default for FreeCAD:** clear 10'-0" (3048 mm) + 6 in (150 mm) slab = **3200 mm**. Use 3350 mm (11'-0" F2F) for a generous house.

### 3.5 South Asian program elements the Western literature omits (T4)

These are not optional extras in a Pakistani house; omitting them is a design error.

| Element | What it is | Planning rule |
|---|---|---|
| **Drawing room (mardana / baithak)** | Formal male-guest reception | **Directly off the entrance, with its own attached bath or adjacent powder room, and no sightline into the family lounge.** A guest must never traverse the family zone to reach a WC. |
| **Lounge (family living)** | Everyday family space | Central, connected to dining and kitchen, screened from the entrance |
| **Purdah / visual privacy** | Family zone not visible from entry | Use a foyer, a screen wall, or an L-turn between the main door and the lounge. Never a door that opens straight onto the lounge. |
| **Dirty kitchen / wash kitchen** | Heavy cooking (tarka, degh), keeps smoke and smell out of the main kitchen | Rear, externally ventilated, adjacent to main kitchen and the rear open space |
| **Servant quarter** | Live-in domestic help | Separate external entrance where possible; own WC; on 1 kanal+, detached at the rear |
| **Roof terrace + mumty** | Sleeping in summer, drying, water tanks | Mumty is the only stair enclosure at roof level; roof must be reachable without passing through a bedroom |
| **Underground + overhead water tanks** | Municipal supply is intermittent | UG tank 500–1,500 gal under the porch/lawn; OH tank sized 250–500 gal, structurally supported over a wall/column line, not mid-span — see 9.6 for roof coordination with the mumty and solar panels |
| **Jaali / screen** | Perforated screen for shaded ventilation and privacy | Use on courtyard-facing and west-facing openings; see `architecture-freecad-bim` for parametric jaali modelling |
| **Ablution point / wudu area** | Near a prayer space | Small tap point off a bath or utility, floor drained |

### 3.6 Bedroom count by plot (T4 market expectation)

| Plot | G+1 typical | Bedrooms | Baths |
|---|---|---|---|
| 3 Marla | G+1 | 2–3 | 2 |
| 5 Marla | G+1 | 3 | 3 + powder |
| 7 Marla | G+1 | 3–4 | 4 |
| 10 Marla | G+1 | 4–5 | 5 + powder |
| 1 Kanal | G+1 | 5–6 | 6 + powder + servant |
| 2 Kanal | G+1 | 6–8 | 8 + powder + 2 servant |

### 3.7 Parking (T1-U where bylaws mandate — confirm locally, T4 otherwise)

- Standard car bay: **8'×16' minimum, 9'×18' comfortable** (2.44×4.88 m / 2.74×5.49 m).
- SUV/Land Cruiser: **9'×20'**.
- Porch clear height: **8'-0" (2.44 m)** minimum under the beam.
- Driveway width at the gate: **10'-0"** minimum for a single car; **12'-0"** for a comfortable turn from a narrow street.
- Turning: a car cannot turn into a 9 ft bay from a street narrower than ~20 ft without a 3-point turn. On a 20 ft street, **make the porch 2 bays wide even for one car**, or angle it.

### 3.8 Area budgeting — does the brief actually fit?

Do this **before drawing anything**. It is arithmetic, it takes two minutes, and it prevents the single most common failure: a plan that only fits because every room was quietly shrunk 15%.

```
STEP 1  Available covered area  = footprint × floors        (Section 2.2 — placeholder
                                                               figures; re-derive once 2.1
                                                               is confirmed)
STEP 2  Available carpet area   = covered × NTG target      (Section 10.2)
STEP 3  Required carpet         = Σ (T4 room areas from 3.2)
STEP 4  Compare.
        Required ≤ 0.95 × Available  → comfortable, proceed
        0.95–1.05 × Available        → tight; expect to lose one store or shrink one bedroom
        > 1.05 × Available           → the brief does not fit. Resolve NOW:
                                        (a) drop a room
                                        (b) merge drawing room into lounge
                                        (c) move a bedroom to the mumty level (if allowed)
                                        (d) next plot band
```

**Carpet budget by plot (G+1, 272.25 basis, at "good" NTG — using Section 2.2's placeholder coverage/FAR figures, re-derive once confirmed):**

| Plot | Covered G+1 | NTG target | Carpet available | Realistic program it buys |
|---|---|---|---|---|
| 5 Marla | 2,042 sq ft | 70% | ~1,430 sq ft | 3 bed + 3 bath + lounge/dining + kitchen + drawing (merged) |
| 7 Marla | 2,859 sq ft | 71% | ~2,030 sq ft | 4 bed + 4 bath + separate drawing + dining + kitchen |
| 10 Marla | 3,811 sq ft | 72% | ~2,744 sq ft | 5 bed + 5 bath + drawing + lounge + dining + dirty kitchen + servant |
| 1 Kanal | 7,623 sq ft | 70% | ~5,336 sq ft | 6 bed + 6 bath + full formal/family split + servant block |
| 2 Kanal | 14,157 sq ft | 68% | ~9,627 sq ft | 8 bed + full service wing; efficiency stops being the constraint |

**Worked — 5 marla (30×45), client wants 4 bedrooms + separate drawing room:**
```
Available carpet (G+1)                 = 2,026 × 0.70 = 1,418 sq ft
Required at T4 sizes:
  Master 12×14                = 168
  Bed 2  11×12                = 132
  Bed 3  11×12                = 132
  Bed 4  11×12                = 132
  4 × attached bath 5×8       = 160
  Powder 3×5                  =  15
  Drawing 12×14               = 168
  Lounge 12×14                = 168
  Dining 10×12                = 120
  Kitchen 7×9.5               =  67
  Store 4×6                   =  24
  Foyer 5×6                   =  30
                       TOTAL  = 1,316 sq ft
Ratio = 1,316 / 1,418 = 0.93  → fits, but with only 7% slack.
VERDICT: buildable, but the drawing room and lounge cannot both be generous.
         Recommend: merge drawing + lounge (frees 168) OR drop bed 4 (frees 172).
         Do NOT proceed by shrinking every bedroom to 10×11 — that is how a
         5 marla house ends up feeling like a hostel.
```

**Rule:** when a client insists on a brief that scores >1.05, put the arithmetic in front of them in exactly this form. It converts an argument about taste into an argument about numbers, and the numbers win.

---

## Section 4: Circulation — Passages, Doors, Windows, Foyer

Circulation in a well-planned Pakistani house should be **8–14% of covered area**. Over 18% means the plan is fighting itself — usually a stair in the wrong place or a passage serving only two rooms.

### 4.1 Passage widths

| Situation | IRC floor (T3) | Pakistani practice (T4) | Recommend |
|---|---|---|---|
| Minimum any residential corridor | **36 in (3'-0") clear** | — | never below this |
| Passage serving 1–2 rooms | 36 in | 3'-6" – 4'-0" | **4'-0" (1219 mm)** |
| Passage serving 3+ bedrooms | 36 in | 4'-0" – 5'-0" | **4'-6" (1372 mm)** |
| Main spine / entrance gallery | 36 in | **7'-0"** commonly built | 5'-0" – 7'-0" by budget |
| Passage doubling as a gallery/seating | — | 7'-0"+ | 7'-0" (2134 mm) |

**Two mechanics that catch people out:**
1. **36 in is measured finished-surface to finished-surface.** Frame the rough opening at **38 in** so plaster and finishes still leave 36 in clear.
2. **Pakistani vernacular runs at 7 ft, more than double the IRC floor.** That is a cultural preference for generous circulation, not a code requirement. Quoting "3 ft is the code minimum" to a Pakistani client and building it will read as a cheap house.

**Wheelchair / aging-in-place:** 36 in passage + a 32 in clear door works for straight-through travel, but a **90° turn from passage into a room needs 42 in passage with a 32 in door, or 36 in passage with a 36 in door.** See `architecture-accessibility-design`.

### 4.2 Door sizes (T4)

| Door | Leaf size (ft) | Leaf (mm) | Clear opening |
|---|---|---|---|
| Main entrance (single) | 3'-6" × 7'-0" | 1067 × 2134 | 1000 mm |
| Main entrance (double) | 2× 3'-0" × 7'-6" | 2× 914 × 2286 | 1750 mm |
| Bedroom | 3'-0" × 7'-0" | 914 × 2134 | 850 mm |
| Kitchen | 3'-0" × 7'-0" | 914 × 2134 | 850 mm |
| Bathroom | 2'-6" × 7'-0" | 762 × 2134 | 700 mm |
| Bathroom (accessible) | 2'-10" × 7'-0" | 864 × 2134 | 810 mm |
| Store | 2'-6" × 7'-0" | 762 × 2134 | 700 mm |
| Terrace / French | 2× 2'-6" × 7'-0" | 2× 762 × 2134 | 1450 mm |

**Door-swing rule:** a bathroom door must not swing into the WC clearance zone; on baths under 5×7 ft, use an outward swing or a sliding door — otherwise a person who falls inside blocks the door.

### 4.3 Window and opening sizes (T4)

| Opening | Typical size (ft) | Size (mm) | Sill (mm) | Notes |
|---|---|---|---|---|
| Bedroom | 5'-0" × 4'-0" or 6' × 4' | 1525×1220 / 1830×1220 | 900 | Must satisfy ≥1/10 floor area AND the escape geometry (4.5) |
| Lounge / drawing | 6' × 5' or 8' × 5' | 1830×1525 / 2440×1525 | 750–900 | Lower sill for a seated sightline |
| Dining | 5' × 4' | 1525×1220 | 900 | |
| Kitchen (over counter) | 4' × 3' | 1220×915 | **1200** | 900 counter + 300 splash |
| Bathroom | 2' × 2' or 3' × 2' | 610×610 / 915×610 | 1500–1800 | High sill for privacy; must be openable |
| Stair half-landing | 3' × 4' | 915×1220 | 900 | The one window that stops an unlit stair |
| Ventilator / roshandan | 2' × 1'-6" | 610×455 | 1980 (over door head) | Cheapest stack-ventilation device there is |
| Terrace / French door | 5' × 7' | 1525×2134 | 0 | Counts as an opening, not a window |

**Window head is set at the door head (2134 mm) as default** so lintels align on one continuous band — structurally simpler, visually calmer, and it makes the chajja a single continuous slab rather than a series of stubs.

**Two arithmetic traps:**
1. **The 1/10 rule is on floor area, and it bites on big rooms.** A 12×14 ft bedroom (168 sq ft) needs ≥16.8 sq ft of window. A 4'×4' window is 16 sq ft — **fails**. A 5'×4' is 20 sq ft — passes. Compute it; do not eyeball it.
2. **Sliders halve your openable area.** A 5'×4' sliding window presents 20 sq ft of glass but only 10 sq ft of opening. For the ventilation check (≥5% of floor area openable) and for the escape check, count **openable** area, not glazed area. Casements and top-hungs do not have this problem.

### 4.4 Foyer and entrance sequence

- Foyer minimum: **5×6 ft**; comfortable 7×8 ft.
- Provide a **visual break** between the main door and the family lounge: an L-turn, a screen wall (jaali or solid, 4–5 ft from the door), or a foyer with a closed lounge door.
- Locate the **powder room off the foyer or the drawing room**, never off the family passage.
- Shoe storage: 2'-0" deep × 3'-0" wide niche at the entrance — universally needed, almost always forgotten.

### 4.5 Egress logic for a house

Pakistan has no residential egress clause equivalent to IRC R310. Apply as **good practice (T3)**:
- **Every bedroom should have one openable window usable as an escape:** net clear opening ≥ 5.7 sq ft, minimum clear height 24 in, minimum clear width 20 in, sill ≤ 44 in above floor.
- Check against 4.3: a 5'-0" × 4'-0" casement with two leaves gives ~2'-5" × 4'-0" = 9.7 sq ft clear per leaf ✓. The same size as a **slider** gives 2'-6" × 4'-0" = 10 sq ft, width 30 in ✓, height 48 in ✓ — also passes. A 3'×2' bathroom window does **not** pass and is not an escape route.
- On a G+1 house, this is what makes an upper-floor bedroom survivable if the single stair is blocked.
- **Burglar grilles defeat this.** If grilles are used (they usually are), specify at least one **openable/quick-release grille per bedroom**, keyed and with the key stored in the room.
- A single stair is normal and acceptable in a house. **Do not put the only stair inside a closed kitchen or store** — the two rooms most likely to be the fire origin.

---

## Section 5: Staircase Design and Placement

### 5.1 Geometry

| Parameter | NBC 2016 Pt.4 / IS 456 (T2, South Asia) | IRC (T3, US) | Pakistani practice (T4) |
|---|---|---|---|
| Riser | 150–175 mm; **capped 175 mm residential**, 150 mm institutional | max 7¾ in (197 mm) | 165–180 mm (6.5–7 in) |
| Tread (going) | min **230 mm**, typical 250–300 mm | min 10 in with nosing / 11 in without | 250–280 mm (10–11 in) |
| Riser variation in a flight | uniform | max ⅜ in (9.5 mm) | uniform — enforce on site |
| Comfort rule | 2R + T = 600–640 mm | R + T ≈ 17–18 in | **2R + T = 620 mm target** |
| Clear width (house) | 900 mm min | 36 in (914 mm) | **1000–1200 mm** |
| Headroom | 2100 mm | 2032 mm (80 in) | **2100 mm min, measured vertically from nosing** |
| Max risers per flight before a landing | 12–15 | flight rise ≤ 12 ft | **≤ 12 risers, then a landing** |
| Landing depth | ≥ stair width | ≥ stair width | ≥ stair width, min 1000 mm |
| Handrail height | 900 mm from nosing | 34–38 in (864–965) | **900 mm**, both sides if width > 1100 mm |
| Balustrade gap | — | sphere 4 in (102 mm) must not pass | **≤ 100 mm** — child safety, non-negotiable |

### 5.2 Worked stair calculation — the default Pakistani house stair

```
Floor-to-floor        = 3200 mm  (10'-0" clear + 150 mm slab)
Trial riser           = 165 mm
Risers needed         = 3200 / 165 = 19.4  → round to 20
Actual riser          = 3200 / 20 = 160 mm            ✓ (150–175 band)
Treads                = 20 − 1 = 19
Choose tread          = 265 mm                        ✓ (≥230 mm)
Comfort check         = 2(160) + 265 = 585 mm         ⚠ below 600–640 target
Re-solve for comfort:  tread = 620 − 2(160) = 300 mm  ✓ (upper end of NBC band)
```

**Two viable solutions:**

| Option | Riser | Tread | 2R+T | Total going (19 treads) | Dog-leg well (L × W) |
|---|---|---|---|---|---|
| **A — compact** | 160 mm | 265 mm | 585 | 5,035 mm | flight going 9×265 = 2,385 + landing 1,200 = **3,585 × 2,150 mm** ≈ **11'-9" × 7'-1"** |
| **B — comfortable** | 160 mm | 300 mm | 620 | 5,700 mm | flight going 9×300 = 2,700 + landing 1,200 = **3,900 × 2,150 mm** ≈ **12'-10" × 7'-1"** |

Well width for both: two 1,000 mm flights + 150 mm gap = **2,150 mm (7'-1")**.

**This is why the stair well in the Section 3.2 table is 7×12 ft — it is the arithmetic, not a convention.** A 5 marla plan that allocates less than 7 ft of width to the stair will end up with a non-compliant riser or a winder.

**Higher floor-to-floor:** at 3,350 mm F2F, 21 risers @ 159.5 mm, 20 treads. At 3,660 mm (12 ft), 22 risers @ 166 mm, 21 treads — flight going grows to 3,150 mm, well length **4,350 mm (14'-3")**. Tall ceilings cost stair footprint on every floor.

**Odd riser counts** (21 at 3,350 F2F) mean an unequal dog-leg: 11 risers up to the landing, 10 after. That is acceptable and common — what is **not** acceptable is a different riser *height* between the two flights. Divide the F2F once, apply the same riser everywhere.

**Headroom check — the step people skip.** At the half-landing, the underside of the upper flight passes over the lower flight. Clear headroom = F2F/2 minus the waist slab thickness (typically 150 mm) minus finishes. At 3,200 F2F: 1,600 − 150 − 25 = 1,425 mm at the landing edge, rising by one riser (160 mm) per tread as you walk back. You clear 2,100 mm after `(2100 − 1425)/160 = 4.2` → **5 treads back from the landing nosing**. Verify this in the model; a 3-tread-deep understair store will hit your head.

### 5.3 Stair type selection

| Type | Well needed | When to use | Avoid when |
|---|---|---|---|
| **Straight single flight** | 1,000 × 5,700 mm | Long narrow plot, stair along a party wall | Short plots; consumes 19 ft of length |
| **Dog-leg (half-turn, 2 flights + landing)** | 2,150 × 3,600–3,900 mm | **Default for 5–10 marla** — most compact, lands you back near the start | — |
| **Quarter-turn (L-shape)** | ~2,100 × 4,000 mm | Corner locations, entrance foyer | Tight plots |
| **Open-well (3 flights)** | 2,700 × 3,300 mm | 1 kanal+, lets light down the well | Small plots — wasteful |
| **Winder** | 1,000 × 3,600 mm | Absolute last resort on 3 marla | **Anywhere a child or elderly person lives** — winder treads narrow to nothing at the inside |
| **Spiral** | Ø 1,600–2,000 mm | Roof-only access, mumty | Primary stair — cannot move furniture |

### 5.4 Placement rules

1. **Central to the plan, adjacent to the passage, never inside a room.** The stair should land in circulation on both floors, not in a bedroom.
2. **Stack it exactly.** The ground and first floor stair must occupy the identical footprint — misaligned stairs force a transfer beam and a wasted void.
3. **Put it on the party wall on small plots.** On a 25 ft frontage, a central stair kills the plan; against the side wall it costs 7 ft of width and nothing else.
4. **Keep the mumty over the stair.** The mumty is the top flight's enclosure; if the stair is not stacked to the roof, you need a second stair or a ladder — both are failures.
5. **Give it light.** A stair well against an external wall or a courtyard gets a window on the half-landing; an internal stair gets a skylight in the mumty. **An unlit stair is the most common defect in Pakistani spec housing.**
6. **Under-stair space:** the triangular volume under a dog-leg is 25–35 sq ft — use it as a store or powder room only if headroom ≥ 6'-6" at the WC, which usually means the powder goes under the *upper* flight.
7. **Separate-floor rental (very common in Pakistan):** if the first floor may be let separately, the stair must be reachable **from the entrance/porch without entering the ground-floor house** — plan that from day one, retrofitting it is impossible.

---

## Section 6: Courtyards and Light Wells

### 6.1 Why (T5 — quoted at the study's own metric, not rounded up)

Peer-reviewed evidence for courtyards in arid/semi-arid climates, quoted at the precision the underlying research actually supports:

- **A Pakistan-specific study of a mud-brick, wind-catcher-equipped courtyard house variant reports roughly a 20% reduction in total annual energy use** versus an equivalent non-courtyard house — this is an *annual energy* figure for that specific building variant, **not** a universal "cooling load" percentage applicable to any courtyard house, and should not be quoted as a tight 20–30% cooling-load range without naming the specific study and variant it came from.
- Indoor temperature reductions from thermal mass plus self-shading are reported in the low single digits (°C) in the South Asian literature; treat any number quoted here as **order-of-magnitude, study-specific, and non-additive with the energy figure above** — do not present both as if they describe the same mechanism at the same confidence level.
- A dedicated Pakistan-specific study — *Climate responsive courtyard design for urban sustainability in five Marla houses in Rawalpindi* (Discover Cities, Springer Nature, 2026) — models courtyard performance **at the exact plot scale most common in urban Pakistan**, i.e. the courtyard is not a luxury reserved for 1 kanal. Cite this study by name when quoting its findings; do not merge its numbers with the mud-brick wind-catcher study above as if they were one dataset.
- The Lahore traditional courtyard house is the documented regional precedent: deep-plan block, single central open space, all rooms opening inward.

**Mechanism:** the courtyard is a night-cooled cold-air reservoir. Dense masonry absorbs heat by day; at night the courtyard radiates to the clear sky, cool air pools in it and drains into surrounding rooms. It fails if (a) the courtyard is fully paved with high-albedo hard surface and no vegetation/water, (b) it is glazed over, or (c) it is so wide it stops self-shading.

**Rule for quoting these numbers to a client:** name the specific study and what it actually measured (annual energy vs a specific variant, not a generic "cooling load"). Say *"a Pakistan-specific courtyard study found roughly 20% lower annual energy use for a mud-brick wind-catcher variant — your masonry-frame house won't behave identically, but the same physical mechanism (thermal mass + night radiative cooling + self-shading) applies in the same direction."* Never state a bare "20–30% cooling-load reduction" as if it were an established, general-purpose figure.

### 6.2 Proportioning by sun angle

Solar noon altitude by city (needed for every courtyard and overhang decision):

| City | Latitude | Summer solstice | Equinox | Winter solstice | Courtyard W/H for winter noon sun to reach the floor |
|---|---|---|---|---|---|
| Karachi | 24.9°N | 88.5° | 65.1° | 41.7° | **1.12** |
| Hyderabad | 25.4°N | 88.0° | 64.6° | 41.2° | 1.14 |
| Multan | 30.2°N | 83.2° | 59.8° | 36.4° | 1.36 |
| Quetta | 30.2°N | 83.2° | 59.8° | 36.4° | 1.36 |
| Lahore | 31.5°N | 81.9° | 58.5° | 35.1° | **1.42** |
| Faisalabad | 31.4°N | 82.0° | 58.6° | 35.2° | 1.42 |
| Islamabad | 33.7°N | 79.7° | 56.3° | 32.9° | **1.55** |
| Peshawar | 34.0°N | 79.4° | 56.0° | 32.6° | 1.57 |

Formulae, if you need a city not in the table:
`summer altitude = 90 − lat + 23.44` · `equinox = 90 − lat` · `winter = 90 − lat − 23.44` · `W/H factor = 1 / tan(winter altitude)`

Read as: **required courtyard width W = H × (W/H factor)**, where H is the height of the wall on the sun-facing (south) side of the courtyard.

**Worked, Lahore, G+1 house, courtyard wall height H = 6.7 m (two 3.2 m storeys + parapet):**
```
Winter noon sun to courtyard FLOOR:  W = 6.7 × 1.42 = 9.5 m (31 ft)
    → impossible on 5 marla (25 ft frontage). Do not chase it.
Winter noon sun onto the NORTH WALL of the courtyard at 2 m above floor:
    effective H = 6.7 − 2.0 = 4.7 m  →  W = 4.7 × 1.42 = 6.7 m (22 ft)
    → still large. On 5 marla, accept sun on the upper north wall only.
Single-storey courtyard, H = 3.4 m:  W = 3.4 × 1.42 = 4.8 m (16 ft) → achievable.
```

**The honest conclusion for small plots:** on 5 marla you cannot get winter sun to the courtyard floor, and that is fine — **the courtyard's job there is ventilation, daylight and privacy, not winter solar gain.** Size it for daylight and stack ventilation, and take winter warmth from south-facing windows on the street or rear facade instead.

### 6.3 Courtyard sizing by plot (T4/T5 synthesis)

| Plot | Courtyard type | Plan size | W/H (2-storey) | Primary function |
|---|---|---|---|---|
| 3 Marla | Light shaft | 4×4 ft (1.2×1.2 m) | 0.18 | Bath/stair ventilation only |
| 5 Marla | Light + vent well | **6×8 ft to 8×10 ft** | 0.27–0.36 | Cross-ventilation, kitchen/bath light, stack effect |
| 7 Marla | Small courtyard | 10×10 ft | 0.45 | + daylight to internal rooms |
| 10 Marla | Courtyard | **12×14 ft to 14×16 ft** | 0.54–0.63 | + usable outdoor room, dual-aspect bedrooms. **Diaphragm note:** check against 2.6 — centre the cut, generous edge beam. |
| 1 Kanal | Full courtyard | **18×20 ft to 20×24 ft** | 0.82–0.91 | + planting, water feature, real thermal mass reservoir. **Diaphragm note:** see 2.6 — this is a large cut, flag it to the engineer explicitly. |
| 2 Kanal | Central courtyard | 25×30 ft+ | 1.14+ | Full climate courtyard, winter sun reaches floor. **Diaphragm note:** see 2.6. |

**Ratio guidance:**
- **W/H < 0.3** — this is a *light well*, not a courtyard. Ventilation and code light only. Keep it, it still works: a 4×4 ft shaft driving stack ventilation is worth more than a windowless bathroom.
- **W/H 0.3–0.7** — hot-dry optimum. Deep, self-shading, strong stack effect, minimal direct solar gain. **This is the right band for Lahore/Multan/Faisalabad on 5–10 marla.**
- **W/H 0.7–1.2** — balanced. Daylight to lower floors, some winter sun. Right for 1 kanal in Punjab, and for Islamabad/Peshawar where you want more winter gain.
- **W/H > 1.2** — this is a yard, not a courtyard. Loses the self-shading benefit; needs trees or pergolas to work in summer.

**Aspect ratio in plan:** keep the courtyard between **1:1 and 1:2**. Long thin courtyards (1:3+) behave as light slots and lose the air reservoir.

### 6.4 Making the courtyard actually perform

1. **Vegetation and/or water.** A bare paved courtyard in Multan becomes a heat trap. One tree, or planting on ≥30% of the courtyard floor, or a small water body — evaporative cooling is the second half of the mechanism.
2. **Shade it in summer, open it in winter.** Retractable shade (chatai, tensile, pergola with deciduous vine) over the courtyard from May–September.
3. **Openable connection to every adjacent room.** The courtyard cools nothing if the rooms cannot draw from it. Every room touching the courtyard gets an openable window or door onto it.
4. **Pair with a high outlet.** Stack ventilation needs an exit: a stair-well skylight, a mumty vent, or high-level courtyard windows. **Inlet low and shaded (courtyard side), outlet high (roof/mumty).**
5. **Drain it.** A courtyard is an open drain during monsoon. Slope ≥ 1:100 to a floor gully sized for the local rainfall intensity, and never let it drain into the house.
6. **Jaali the upper courtyard walls** where overlooking between floors or from neighbours is an issue — preserves airflow, kills the sightline.

### 6.5 Light wells and internal bathrooms

- Minimum shaft for a single internal bathroom: **4×4 ft (1.2×1.2 m)** open to sky.
- Serving two bathrooms stacked either side: **4×6 ft**.
- Shafts deeper than **1:8 (width:height)** deliver effectively no daylight — treat as ventilation only and provide artificial light.
- **Never cap a light well with a fixed skylight** if it is the ventilation route for a WC. Use a louvred/openable rooflight or a raised vent cowl.

### 6.6 Courtyard vs light well — decision tree

```
Is there ≥ 10 ft of plan width to spare after the room budget (Section 3.8)?
  └─ NO  → LIGHT WELL. 4×4 ft minimum, sized only to ventilate baths/stair.
  │        Do not call it a courtyard to the client. It is not one.
  └─ YES ↓
Is the climate hot-dry / hot-arid (Lahore, Multan, Faisalabad, Karachi, Bahawalpur)?
  └─ NO (Quetta, Murree — heating-dominated)
  │        → SMALL COURT or none. A courtyard is a heat-loss surface in Quetta.
  │          Prefer a compact form + south glazing.
  └─ YES ↓
Can W/H reach ≥ 0.3 at the built wall height?
  └─ NO  → still build it as a vent well; state honestly that its value is
  │        ventilation and daylight, not thermal mass performance.
  └─ YES → COURTYARD. Size to the 0.3–0.7 band, long axis E–W,
           ≥30% soft/planted floor, openable connection from every adjacent room,
           high-level outlet at the stair skylight or mumty, centred on plan
           (2.6) and flagged to the engineer as a diaphragm cut.
```

---

## Section 7: Orientation for Pakistan's Climate

### 7.1 The headline (T5)

**Good orientation alone, with no mechanical cooling, is reported to cut indoor temperatures by roughly 5–7 °C** in the Pakistan-specific orientation literature (see Appendix A) — treat this as an order-of-magnitude finding from that literature, not a guaranteed result for every house. It is free at design stage and impossible to retrofit. Fix orientation before fixing the plan.

**Core rule: the long walls of the house face north and south; the short walls face east and west.** East and west facades receive low-angle morning and afternoon sun that no overhang can shade — minimise their area. North-facing windows admit daylight with almost no direct heat gain year-round.

### 7.2 City-specific findings (T5)

| City | Climate zone | Finding | Design action |
|---|---|---|---|
| **Lahore** | Hot semi-arid (BSh) | **Southwest orientation found optimal** for balancing combined heating and cooling loads | Long axis roughly E–W; principal living spaces to the S/SW with deep shading; kitchen and services on the west |
| **Karachi** | Hot arid, coastal | **Prevailing breeze from ~245° (SW).** Residential zones typically planned E–W with facades perpendicular to prevailing wind | Openings on the SW facade as inlets; sea breeze is the primary cooling resource — **never block the SW face with services** |
| **Islamabad / Rawalpindi** | Humid subtropical | **Prevailing winds from north and southeast** | Inlets on N and SE; more winter solar gain wanted than Lahore — larger south glazing, shallower overhangs |
| **Multan / Bahawalpur** | Hot desert (BWh) | Extreme summer; dust storms | Minimise E/W glazing to near-zero; courtyard W/H at the low end (0.3–0.5); heavy thermal mass |
| **Peshawar** | Hot semi-arid | Similar to Lahore, higher latitude | As Lahore; winter gain slightly more valuable |
| **Quetta** | Cold semi-arid | Heating-dominated | **Invert the priority:** maximise south glazing, minimise shading, compact form, small courtyard |

**Note the Karachi/Lahore conflict.** In Lahore the SW facade is a heat liability to be buffered. In Karachi the SW facade is the breeze inlet and must stay open. **Do not carry a Lahore rule to Karachi.** When the city is not stated, ask before applying any orientation rule.

### 7.3 Room-by-room orientation (Punjab/Sindh default)

| Room | Best orientation | Why |
|---|---|---|
| Bedrooms (primary) | **North / North-east** | Cool at night, no afternoon gain, soft morning light |
| Living / lounge | **South** | Winter sun with a shallow overhang; shaded in summer |
| Drawing room (occasional use) | Any, incl. east | Low occupancy hours; can absorb a poorer aspect |
| Kitchen | **North or east**; **never west** | A west kitchen at 4 pm in Multan is unusable. If forced west, add a dirty kitchen to the north/rear. |
| Dining | East / south-east | Morning light at breakfast |
| Bathrooms, stores, stairs, servant room | **West and south-west** | Use low-occupancy rooms as a **thermal buffer** on the worst facade |
| Car porch / garage | West or south-west | Same buffer logic; shades the wall behind it |
| Courtyard | Centre; long axis E–W | Maximises self-shading of the north and south courtyard walls |
| Roof terrace | Whole roof | Insulate: this is the largest solar-gain surface on a low-rise house |

**The buffer principle is the single highest-value orientation move on a constrained plot:** you rarely get to choose the plot's orientation, but you always get to choose which rooms take the beating.

### 7.4 Window-to-wall ratio by facade (T5 / practitioner)

WWR = glazed area ÷ gross facade area of that elevation. Targets for hot-dry and hot-arid Pakistan (Lahore, Multan, Faisalabad, Bahawalpur, Karachi):

| Facade | WWR target | Rationale |
|---|---|---|
| **North** | 20–30% | Diffuse daylight, negligible direct gain. Put your glass here. |
| **South** | 15–25% | Good with a 300 mm chajja; winter gain is a bonus in Punjab |
| **East** | 8–12% | Low morning sun; shade with vertical fins or jaali |
| **West** | **0–8%** | No horizontal device works (7.5). Prefer solid wall + buffer rooms. |

Heating-dominated exception (Quetta, Murree): raise **south to 30–40%** and drop the shading; the goal inverts.

### 7.5 Shading device sizing (worked)

For a south-facing window of height H, a horizontal overhang of depth D fully shades it at solar noon when `D = H / tan(altitude)`.

**Lahore, 2.1 m (7 ft) tall south window:**
```
Summer solstice, altitude 81.9°, tan = 7.02
    D = 2.1 / 7.02 = 0.30 m (12 in)  → fully shaded at noon in June ✓
Winter solstice, altitude 35.1°, tan = 0.704
    Shadow drop from a 0.30 m overhang = 0.30 × 0.704 = 0.21 m
    → 1.89 m of the 2.1 m window in full winter sun ✓
```
**A 12-inch overhang on a Lahore south window is a complete seasonal shading solution.** This is why south is the easy facade.

**Same window, west-facing, Lahore, 4 pm July: solar altitude ≈ 25–30°, azimuth ≈ 280°.**
```
D = 2.1 / tan(27°) = 2.1 / 0.51 = 4.1 m of horizontal overhang
```
**4.1 m — absurd.** No horizontal overhang shades a west window. The only working solutions on west are: vertical fins, jaali screens, external louvres/shutters, a deep verandah, or simply **not putting the window there**.

| Facade | Working shading device | Typical depth |
|---|---|---|
| South | Horizontal overhang / chajja | 0.3–0.6 m |
| North | None needed (small early/late summer sun) | 0.15 m for rain |
| East | Vertical fins angled north, or jaali | fins 0.3–0.45 m @ 0.6 m c/c |
| West | Jaali, external louvre, verandah, minimise glazing | verandah 1.8–2.4 m |
| Roof | Insulation + reflective finish + shaded terrace | 50–75 mm insulation min |

**Chajja (the Pakistani projecting sunshade)** is the vernacular answer and it works: 12–24 in over every opening, doubling as rain protection. Model it in FreeCAD as a slab projection from the lintel line.

**The roof is the biggest single gain surface on a one- or two-storey house** — it sees the sun all day at high altitude, while walls only get a few hours each. Insulating the roof and shading the terrace beats any facade tweak on a low-rise house; treat it as the first move, not the last.

### 7.6 Cross-ventilation

- Every habitable room wants **two openings on different walls** (ideally opposite or adjacent-perpendicular). A single-opening room does not ventilate, it only leaks.
- **Outlet area > inlet area.** Ratio **outlet : inlet = 1.25 : 1 to 1.5 : 1** increases indoor air velocity. Small inlet, large outlet.
- Openable window area ≥ **1/10 of floor area** (NBC T2), and ≥ 5% for effective ventilation. **Count openable, not glazed** — see 4.3.
- Place inlets **low** (on the shaded/courtyard side) and outlets **high** (leeward, or a roof-level stack) so wind-driven and buoyancy-driven flows reinforce rather than fight each other.
- Internal doors need **transoms or undercuts (min 15 mm)** or the cross-flow stops at the first closed door.
- **Roshandan (high ventilator, 2'×1'6" above the door head)** is the cheapest cross-ventilation device in the Pakistani vocabulary and works even with the door shut. Put one over every internal door on a deep plan.

**Karachi-specific:** with the breeze from 245°, put openable inlets on the SW facade and outlets on the NE. A Karachi house that faces its solid wall southwest has thrown away its main cooling asset.

---

## Section 8: House Plan Archetypes

The plan archetype determines structural grid, servicing, daylight and the whole occupant experience. These are the configurations that actually occur at house scale on Pakistani plots. (General theory retained from the tower-oriented predecessor and re-weighted; a `Tower reference` line notes where the type scales up, for the rare mixed-use brief.) **Every archetype involving an L-shape, a courtyard, a pavilion with long wings, or a split level carries a plan-configuration seismic note — cross-check Section 2.6 before finalising.**

### 8.1 Linear / Side-Passage Plan

Rooms in a single file along one side of a longitudinal passage against the party wall.
- **Plot fit:** 3–5 marla, narrow frontage (20–25 ft)
- **Depth:** rooms 11–14 ft off a 4 ft passage; total 15–18 ft of the 23.5 ft internal width
- **Structure:** load-bearing 9 in brick cross-walls at 11–14 ft, or RCC frame at 12–14 ft
- **Daylight:** front and rear only; middle rooms are the weak point — this is exactly where a light well earns its cost
- **Efficiency:** passage serves one side → circulation 12–16% of covered area
- **Verdict:** the default 3–5 marla plan. Accept it, and fix the middle with a light shaft.
- *Tower reference:* single-loaded corridor (Park Hill, Sheffield, 1961)

### 8.2 Central-Passage / Double-Loaded Plan

Rooms on both sides of a central spine passage.
- **Plot fit:** 7 marla upward, ≥35 ft frontage
- **Depth:** two 12–14 ft room bands flanking a 4–5 ft passage = 28–33 ft
- **Structure:** three lines of load-bearing wall or a 3-bay RCC frame
- **Daylight:** good at front and rear; the passage itself is dark → **skylight it, or terminate it in a window**
- **Efficiency:** best in class — circulation 8–11% of covered area
- **Verdict:** the workhorse 10 marla plan.
- *Tower reference:* double-loaded corridor (Unite d'Habitation, Marseille, 1952)

### 8.3 Courtyard Plan (Traditional Lahore House)

Rooms wrap a central open courtyard; circulation is the courtyard verandah.
- **Plot fit:** 10 marla upward for a true courtyard; 5–7 marla for a light-well variant
- **Depth:** 12–16 ft room band around a 12–24 ft courtyard
- **Structure:** load-bearing masonry historically; RCC frame today. **Seismic note (2.6): the courtyard is a diaphragm cut — centre it, provide a continuous edge beam on all four sides, and flag it explicitly to the engineer, especially at 1 kanal+ where the cut is largest.**
- **Daylight:** **best of any type** — dual-aspect rooms (street/rear + courtyard) throughout
- **Climate:** genuine thermal-mass and self-shading benefit — see Section 6.1 for the correctly-scoped numbers (do not overstate as a flat 20–30% cooling-load cut)
- **Privacy:** every room gets outdoor access without any street exposure — the purdah logic that produced the type
- **Efficiency:** verandah circulation adds length; circulation 14–18%, but it doubles as living space, so do not count it as waste
- **Exemplars:** traditional courtyard houses of the Walled City, Lahore; contemporary reinterpretations across Punjab
- **Verdict:** the climatically correct Pakistani house. Recommend it whenever the plot allows.

### 8.4 L-Shaped / Side-Yard Plan

Building forms an L, with the open space along one side and the rear.
- **Plot fit:** 10 marla – 1 kanal, wider plots (≥40 ft frontage)
- **Daylight:** very good; the side yard gives the internal leg of the L a second aspect
- **Advantage over a courtyard:** the open space is contiguous with the rear garden — a single usable outdoor room instead of two small ones
- **Disadvantage:** less self-shading than an enclosed courtyard; the yard is overlooked from the neighbour's side
- **Seismic note (2.6):** the inside corner of the L is a re-entrant corner — a torsional irregularity point. Keep each wing's aspect ratio ≤ 1:3, and flag the corner explicitly to the structural engineer.
- **Verdict:** the pragmatic 1 kanal plan when the client wants a lawn rather than a courtyard.

### 8.5 Compact Block / Deep Plan

A near-square footprint filling the plot with no internal void.
- **Plot fit:** any, but almost always 3–5 marla by necessity
- **Daylight:** poor — internal rooms depend entirely on borrowed light
- **Efficiency:** highest NTG of any type; circulation can drop to 7–9%
- **When justified:** maximum bedroom count on a tiny plot; heating-dominated Quetta (compact form minimises heat loss)
- **When it fails:** Multan or Karachi with no ventilation route — it becomes an oven
- **Mandatory mitigation:** at least one light/ventilation shaft, and a stair skylight.

### 8.6 Pavilion / Detached Plan

Freestanding house set within its plot on all four sides.
- **Plot fit:** 1–2 kanal; **the required type in low-coverage CDA sectors (20–25%, T1-U — see 2.4)**
- **Daylight:** excellent on all four sides
- **Efficiency:** low — long external wall perimeter, high envelope cost per sq ft
- **Climate:** all four facades exposed → shading strategy must be complete, not partial
- **Seismic note (2.6):** keep any long wing to roughly 1:3–1:4 width:length; avoid a single-room-wide wing longer than ~30 ft without an intermediate shear wall or cross-wall.
- **Verdict:** the Islamabad low-density type. Design it as a garden pavilion, not a shrunken block.

### 8.7 Split-Level / Stepped Plan

Half-storey level changes between zones.
- **Plot fit:** sloping plots (Islamabad, Murree, Quetta, hillside Karachi)
- **Advantage:** follows grade without mass excavation; creates volumetric interest and natural zone separation
- **Cost:** more stairs, harder to service, **poor for aging in place**
- **Seismic note (2.6):** mid-height offsets create a soft-storey-like discontinuity in the lateral load path. Avoid beyond a single half-level step in Zone 3 areas (Islamabad hills, Murree); if unavoidable, flag it explicitly for the engineer to detail a continuous lateral system across the offset.
- **Rule:** never split-level a house intended for elderly occupants or with a single ground-floor bedroom brief.

### 8.8 Two-Unit / Rental-Floor Plan

Ground floor for the family, first floor let separately (extremely common in urban Pakistan).
- **Requirement 1:** **stair reachable from the porch/entrance without entering the ground-floor unit** — see 5.4(7)
- **Requirement 2:** separate electricity and gas meters, and independent water storage
- **Requirement 3:** the upper unit needs its own kitchen and its own roof access
- **Plan consequence:** the stair migrates to the front of the plan, near the entrance, not the centre. **Decide this before the first sketch** — it is the one decision that cannot be retrofitted.

### 8.9 Archetype selection tree

```
Plot frontage < 25 ft?
  └─ YES → Linear / side-passage (8.1) + light shaft. Stop.
  └─ NO ↓
Coverage limit ≤ 30% (CDA low-density, T1-U — confirm before committing)?
  └─ YES → Pavilion (8.6). Check wing proportions against 2.6. Stop.
  └─ NO ↓
Plot sloping > 1:10?
  └─ YES → Split-level (8.7), Zone-3 seismic check per 2.6, unless elderly occupants
           → then terraced flat platforms
  └─ NO ↓
Upper floor to be let separately?
  └─ YES → Two-unit (8.8) — front stair — combined with 8.2 or 8.5
  └─ NO ↓
Plot ≥ 10 marla AND climate hot-dry/hot-arid (Lahore, Multan, Karachi, Faisalabad)?
  └─ YES → Courtyard (8.3), centred per 2.6 ← strongest climatic answer
  └─ NO ↓
Frontage ≥ 40 ft and client wants a lawn?
  └─ YES → L-shaped (8.4), re-entrant corner checked per 2.6
  └─ NO  → Central-passage (8.2)
```

---

## Section 9: Vertical Stacking, Services and Structural Grid

The house-scale version of core planning. A house has no core, but it has wet zones, a stair, risers and column lines — and they must line up.

### 9.1 The stacking rules

1. **Wet-on-wet.** Every first-floor bathroom sits directly over a ground-floor bathroom, kitchen, store, or utility — **never over a bedroom or the drawing room.** A leak above a bedroom ceiling is the most common serious defect in Pakistani houses.
2. **Kitchen over kitchen** where there are two units; otherwise kitchen over store/utility/porch.
3. **Stair stacks exactly** (Section 5.4).
4. **Columns run to foundation.** Any column that stops at first-floor level needs a transfer beam — 2–3× the cost of normal structure and a coordination liability. On a house, there is almost never a good reason.
5. **Soil stacks fall vertically.** 100 mm (4 in) soil stack per bathroom group + 50 mm vent. Horizontal offsets: max ~2 m lateral displacement per offset, and always with a rodding access.
6. **Horizontal drainage gradient: 1:40 to 1:60** for 100 mm soil, 1:80 for larger. A bathroom placed far from the stack forces either a deep floor build-up or a fall that will not clear.
7. **Overhead water tank over a wall or column line**, never mid-span. A 500-gallon tank is ~2.3 tonnes. See 9.6 for roof-level coordination with solar panels and the mumty.
8. **Underground tank clear of the foundation zone** — under the porch or lawn, not against a footing.
9. **Electrical riser:** a 150×150 mm shaft or a chased duct from the ground-floor DB to the first-floor DB, adjacent to the stair.
10. **Gas:** external routing where possible; never conceal a gas line in a wet-wall chase.

### 9.2 Typical Pakistani G+1 stack

```
Roof         Mumty (stair enclosure) + overhead water tanks + solar panels
             Terrace: sleeping/drying, insulated + shaded — see 9.6 for how these
             three roof elements are coordinated, not just co-located
First floor  2–3 bedrooms + attached baths + family lounge/TV + kitchenette (if let)
             Front terrace over the porch
Ground floor Drawing room + powder (front, off entry)
             Lounge + dining + kitchen + dirty kitchen (centre/rear)
             1 bedroom + attached bath (rear — the aging-in-place / guest room)
             Store, stair, servant room (rear)
Site         Car porch (front), lawn, underground tank, septic/sewer chamber
Basement     (optional, often FAR-exempt — CONFIRM, and check water table per 2.4a)
             parking, store, plant
```

**Always put one bedroom with attached bath on the ground floor.** Elderly parents, a sick family member, a guest who cannot climb — this is the most-requested and most-often-omitted item in Pakistani house briefs.

### 9.3 Wall thicknesses for stacking and FreeCAD

| Element | Thickness | Notes |
|---|---|---|
| External wall, brick | **9 in (230 mm)** | Standard; 13.5 in (345 mm) for load-bearing ground floor of G+2, or thermal mass in Multan |
| Internal partition | **4.5 in (115 mm)** | Non-loadbearing |
| Internal load-bearing | 9 in (230 mm) | |
| Party wall | 9 in (230 mm) | Sound and fire; 13.5 in where each side is separately owned |
| Wet-wall (plumbing chase) | 9 in min | 4.5 in cannot take a 100 mm stack |
| RCC slab | **5–6 in (125–150 mm)** | Spans up to ~14 ft one-way; see 9.4 for the corrected depth-vs-span table beyond that |
| Plinth height | **1'-6" to 2'-6" (450–760 mm)** | Above road crown; 2'-6" in flood-prone/low-lying areas |
| Plaster | 0.5 in (12 mm) internal, 0.75 in (20 mm) external | **Deduct from clear dimensions** |

**FreeCAD default set:** external walls 230 mm, internal 115 mm, slab 150 mm, floor-to-floor 3200 mm, door height 2134 mm, window head 2134 mm, sill 900 mm (bedrooms) / 1200 mm (baths, kitchens over counter).

### 9.4 Structural grid coordination (preliminary — verify with `architecture-structural-systems`)

The plan and the structure must be decided together. Choosing room sizes first and asking the engineer to catch up is how you end up with a column in the middle of a bedroom.

| Decision | Preliminary rule | Consequence for the plan |
|---|---|---|
| **Load-bearing masonry (up to G+1)** | 9 in cross-walls at **11–16 ft** centres | Room widths *are* the structural grid. No free-plan; walls cannot move floor to floor. |
| **RCC frame (G+1, G+2)** | Column grid **12–16 ft**, columns 9×12 in or 9×15 in | Free-plan possible, but every column must sit **inside a wall line** — plan the walls to the grid, not the reverse |
| **One-way slab depth, span ≤ 14 ft** | span/28 to span/32 → **4.5–6 in** | Keeps F2F at 3200 mm with a 150 mm slab |
| **One-way slab depth, span 14–16 ft** | span/28 to span/32 → **6–6.9 in** | A 16 ft room needs a genuinely deeper slab than a 12 ft one — do not carry the 5–6 in figure past 14 ft |
| **Beam depth** | span / 12 to span / 15 | 14 ft span → 12–14 in deep beam. 18 ft porch span → **18 in deep** |
| **Porch beam** | 16–18 ft clear span typical | 18 in beam under an 8 ft clear porch pushes the slab soffit to ~9'-6". Coordinate with ground F2F or the porch ceiling drops below 8 ft. |
| **Cantilever (terrace, chajja)** | ≤ span/3 of the backspan | A 6 ft terrace cantilever needs ≥18 ft of backspan or a counterweight |

**Coordination rules:**
1. **Draw the column grid before the furniture.** Move rooms to the grid; never leave a column stranded mid-room and call it a "feature".
2. **Grid lines should coincide with the party walls, the passage walls and the stair walls** — those are the three lines that run continuously through the plan.
3. **Rooms wider than 16 ft need either a deeper slab, a two-way slab, or an intermediate beam.** A 18×22 ft 1-kanal lounge is a real structural decision, not a plan decision.
4. **A courtyard is a hole in the diaphragm — this is a seismic issue as well as a gravity one (Section 2.6).** The slab edge around it needs an edge beam on all four sides. Size the courtyard to fall on grid lines, and keep it centred where possible.
5. This section is **preliminary sizing for planning and modelling only.** Final member sizes come from a PEC-registered engineer.

### 9.5 Cross-reference: this skill vs `architecture-seismic-design` and `architecture-building-codes-permits`

This skill deliberately does two things and no more on seismic and bylaw matters: (1) it flags plan-configuration seismic risk that originates from spatial decisions made here (Section 2.6, 8.x notes), and (2) it tags every coverage/FAR/setback figure with an honest evidentiary tier so a T1-U placeholder is never mistaken for a confirmed T1 bylaw figure. **It does not perform seismic design (base shear, ductility detailing, lateral system sizing) — that is `architecture-seismic-design` and the PEC engineer's job — and it does not replace pulling the actual current bylaw document — that is `architecture-building-codes-permits`'s reference material and, ultimately, the authority's own published schedule.** Treat this skill's T1-U tables as a starting massing hypothesis to be replaced, not a citation.

### 9.6 Roof-level coordination: mumty, terrace shading, solar panels and OH tanks

The roof of a Pakistani G+1 house typically has to host four things at once — the mumty (stair enclosure), the OH water tank(s), solar panels, and a usable shaded terrace — and they are usually drawn as if they don't interact. They do:

1. **Solar panel orientation competes with the mumty's shadow.** Panels want unobstructed south-facing tilt (roughly the site latitude, e.g. ~31° for Lahore) for maximum year-round output. A mumty on the south side of the roof throws a shadow across part of the panel array for a meaningful part of the day — **place the mumty on the north or east portion of the roof plate specifically so its shadow falls away from the panel zone, not as an afterthought after the panels are laid out.**
2. **OH tank support must not land on the panel structure.** The tank (9.1: ~2.3 t per 500 gal) needs its own wall/column line support (9.1 rule 7); do not let the panel mounting frame's ballast or structure double as tank support, and do not let the tank's access ladder/platform cut across the panel array's cleaning/access path.
3. **The shaded terrace and the panel array compete for the same south-facing roof area.** A retractable/fixed shade structure over the terrace (Section 6.4's summer-shade logic, applied at roof level) should be planned on the *opposite* orientation preference from the panels where possible — terrace shade wants to block the sun, panels want to catch it. Resolve by zoning the roof: **panel zone (unshaded, south-tilted) + terrace zone (shaded, can be north or partially screened) + mumty (north/east, low-shadow-impact position)** rather than treating the roof as one undifferentiated surface.
4. **Coordinate at the same stage as Section 14's model checklist** — add "roof zoning: panels / terrace / mumty / OH tank, checked for shadow conflict" as an explicit FreeCAD model check, not an afterthought sketched in after the structure is fixed.

---

## Section 10: Efficiency Metrics for Houses

### 10.1 Definitions at house scale

- **Covered area** — total built-up area measured to the external face of external walls, all floors. What FAR is computed on and what a contractor quotes per sq ft.
- **Carpet area** — usable floor inside the rooms, measured to the internal face of walls, excluding walls, stair, passage.
- **Net-to-gross (carpet / covered)** — the efficiency measure.

### 10.2 Targets

| Plot | Poor | Typical | Good | Excellent |
|---|---|---|---|---|
| 3–5 Marla | <62% | 65–68% | 68–72% | 72–75% |
| 7–10 Marla | <64% | 67–70% | 70–74% | 74–77% |
| 1 Kanal | <62% | 65–69% | 69–72% | 72–75% |
| 2 Kanal | <60% | 63–67% | 67–70% | 70–73% |

Walls alone consume 8–12% of covered area in 9 in brick construction. Circulation 8–14%. Stair 5–8%.

**Efficiency is not the goal.** A courtyard house scores worse on NTG than a compact block and is a far better house. Use NTG to catch *waste* — a passage serving one room, a stair placed so it splits the plan, a duplicated lobby — not to justify eliminating the courtyard.

### 10.3 Where houses leak efficiency

1. **A passage that serves fewer than three doors.** Every such passage is a design failure; re-plan so rooms open off a shared node.
2. **Stair in the middle of a narrow plot.** Costs 7 ft of width twice (both floors) and cuts the plan in half.
3. **Unstacked baths.** Forces horizontal drainage, deeper floor build-up, and a bulkhead in the room below.
4. **Two separate lobbies** (one for the drawing room, one for the family). Merge into a single foyer with a screen.
5. **Over-thick walls where they carry nothing.** A 9 in internal partition that is not load-bearing wastes 4.5 in × its length across two floors.
6. **A dead corner.** Any plan corner not reachable by a door is lost area — usually a re-entrant caused by an ill-placed stair.
7. **Porch counted inside coverage but usable only as parking.** Where a bylaw permits an uncovered/cantilevered porch outside coverage, take it.

### 10.4 Cost anchoring (T4, volatile — always re-verify)

Construction cost in Pakistan is quoted **per sq ft of covered area**, grey structure vs finished. Rates move fast with steel and cement, so **never quote a figure from memory** — check current market rates at the time of the conversation and say that you did. What is stable is the *structure* of the estimate:

```
Total = covered area (sq ft) × rate (Rs/sq ft, grey or finished)
      + boundary wall (running ft × rate)
      + external development (gate, driveway, lawn, tanks, septic)
      + approval fees + PEC/PCATP professional fees
```
Grey structure typically runs 40–50% of the finished total. Rule of thumb for planning: **each additional bathroom adds disproportionate cost** (plumbing, tiling, fittings, waterproofing) relative to its 40 sq ft.

---

## Section 11: Legibility and Wayfinding at House Scale

A house does not need signage; it needs a plan a first-time guest can read. Kevin Lynch's legibility elements (paths, edges, districts, nodes, landmarks) still apply, scaled down.

- **Path:** one clear spine from the main door to the lounge. A visitor should never face three identical doors.
- **Edge:** the public/private threshold — the point past the drawing room where family territory starts. Mark it with a level change, a material change, or a door.
- **District:** guest zone (front), family zone (centre), service zone (rear), private zone (upper). **Four zones, in that order, is the diagram of a good Pakistani house.**
- **Node:** the foyer and the stair landing are the two decision points. Both should be lit and visible from the entrance sequence.
- **Landmark:** the stair, a courtyard view, or a double-height drawing room — one memorable spatial event orients the whole plan.

**Practical rules:**
- **Sightline from the main door must not reach the family lounge or any bedroom door.** Privacy and legibility here are the same requirement.
- **The stair should be visible (or clearly implied) from the foyer.** A hidden stair makes the upper floor feel like a separate building.
- **Light the ends of passages.** A passage that terminates in a blank wall reads as a dead end even when it isn't; terminate it in a window, a courtyard, or at minimum a niche.
- **Ceiling height as hierarchy:** drawing room / lounge 11–12 ft > bedrooms 10 ft > passages and baths 9 ft. Compressing the passage before the lounge amplifies arrival.
- **Aging in place:** ground-floor bedroom + attached bath, 36 in clear passages, no split levels, lever handles, 900 mm handrail both sides of the stair. See `architecture-accessibility-design`.

---

## Section 12: Worked Examples

**Standing caveat for every example below:** all coverage/FAR/setback figures used here trace back to Section 2's **T1-U (unverified)** tables. Every "✓" against a coverage or FAR number in these examples means "consistent with the placeholder figures used in this document" — **not** "confirmed against a current, cited LDA/CDA schedule." Re-run each example's envelope arithmetic with confirmed figures before treating it as more than a methodology demonstration.

### 12.1 5 Marla, 30×45 ft, Lahore, east-open, G+1, 3 bedrooms

```
PLOT       30 × 45 ft = 1,350 sq ft (~5 marla, 272.25 basis)
BYLAW      LDA 5–10 marla band (T1-U, unverified — see 2.1): coverage 75%, FAR 1:1.8
ENVELOPE   Max footprint  = 1,350 × 0.75 = 1,013 sq ft
           FAR cap        = 1,350 × 1.8   = 2,430 sq ft
           G+1 at full fp = 2,026 sq ft    (consistent with FAR placeholder — CONFIRM)
           Mumty          = 122–176 sq ft  (on top of coverage)
SETBACK    Front 5 ft (porch), rear 5 ft, sides = party-wall construction, common
           practice NOT a confirmed "0 ft" legal setback (see 2.3b) — confirm the
           scheme's own side-setback bylaw before assuming zero.
           Buildable = 30 × 35 = 1,050 sq ft → coverage binds at 1,013 (30 × 33.8)
INTERNAL   30 ft − (2 × 0.75 ft external walls) = 28.5 ft clear width
BUDGET     Carpet available = 2,026 × 0.70 = 1,418 sq ft
           Required (3 bed, merged drawing/lounge) ≈ 1,150 sq ft → 0.81 (comfortable,
           relative to the placeholder envelope above)

ORIENTATION  East-open. Morning sun on the entrance facade (tolerable).
             West = rear → put kitchen dirty-area, stair and baths on the rear/west
             as a thermal buffer. Bedrooms take the north side.
             WWR: north 25%, south 20% w/ 300 mm chajja, east 12%, west ~3%.

GROUND FLOOR (≈1,013 sq ft covered)
  Porch (front 5 ft setback, uncovered)         9 × 18
  Foyer + screen                                 5 × 6
  Drawing room (front, east)                    12 × 14
  Powder (off foyer)                             3 × 5
  Lounge + dining (centre)                      12 × 16
  Kitchen (rear/north-west)                    7'0" × 9'6"
  Bedroom 1 + attached bath (rear, north)       11 × 12 + 5 × 8
  Stair (party wall, west)                       7 × 12
  Light well (centre-west, serving stair+bath)   6 × 8
  Rear open space                               30 × 5

FIRST FLOOR (≈1,013 sq ft covered)
  Master bedroom + attached bath (north)        12 × 14 + 5 × 8
  Bedroom 3 + attached bath                     11 × 12 + 5 × 8
  Family lounge / study (over drawing room)     12 × 12
  Front terrace (over porch)                     9 × 12
  Stair (stacked)                                7 × 12
  Light well (stacked)                           6 × 8

ROOF   Mumty 8 × 12 (96 sq ft, within allowance), placed north-east corner of the
       roof plate so its shadow clears the south-facing solar panel zone (9.6).
       Terrace + OH tank over the party wall line, tank supported on the party
       wall itself, clear of the panel mounting frame (9.6).

STAIR  F2F 3200 → 20 risers @ 160 mm, 19 treads @ 265 mm, well 3,585 × 2,150 mm
       Window on the half-landing onto the light well.

STRUCTURE  Load-bearing 9 in cross-walls at 12–14 ft (room widths), 5 in one-way
           slab (span ≤14 ft everywhere here — 9.4 table applies at the lower band).
           Porch: 18 ft span → 18 in deep beam; check 8 ft clear under it.
           No L-shape, no courtyard cut, no split-level in this plan — Section 2.6
           plan-irregularity checks do not apply here (single rectangular block).

CHECKS  Coverage 1,013 / 1,350 = 75.0% — consistent with the T1-U placeholder;
                                          CONFIRM against current LDA schedule
        Covered 2,026 / FAR cap 2,430 — consistent with placeholder; CONFIRM
        Circulation ≈ 118 sq ft of 1,013 = 11.6% ✓ (this ratio holds regardless
                                          of the exact coverage figure used)
        Master window: 168 sq ft floor → need 16.8 sq ft → 5'×4' = 20 ✓
        Every bedroom has an external openable window meeting escape geometry ✓
        Wet zones stacked (baths over baths/kitchen) ✓
        Ground-floor bedroom + attached bath present ✓
        Light well 6×8, W/H = 1.8/6.7 = 0.27 → ventilation-grade, acceptable ✓
        Zero west habitable glazing ✓
```

### 12.2 10 Marla, 35×77.8 ft, Islamabad, north-open, G+1, courtyard

```
PLOT       35 × 77.8 ft = 2,723 sq ft (10 marla)
BYLAW      Band 10 marla–1 kanal (T1-U, unverified — see 2.1): coverage 70%, FAR 1:1.5
           (CDA sector schedule is separately T1-U per 2.4 — CONFIRM both, they may
           differ from the LDA-derived placeholder used here)
ENVELOPE   Footprint 1,906 sq ft; FAR cap 4,084; G+1 = 3,811 (placeholder — CONFIRM)
SETBACK    Front 10, rear 8, sides 5 (one side) → buildable ~30 × 60 = 1,800 sq ft
           → SETBACKS BIND (1,800 < 1,906) under the placeholder figures. Adopt
           1,800 sq ft footprint pending confirmation.
BUDGET     Carpet = 3,600 × 0.72 = 2,592 sq ft → supports 5 bed + 5 bath +
           drawing + lounge + dining + dirty kitchen + servant, relative to the
           placeholder envelope.
ARCHETYPE  Central-passage with a courtyard inserted mid-plan (8.2 + 8.3 hybrid)
COURTYARD  12 × 14 ft, long axis E–W, CENTRED on the plan per Section 2.6.
           H = 6.7 m two storeys → W/H = 3.66/6.7 = 0.55
           → hot-dry optimum band (0.3–0.7) ✓
           **Diaphragm flag (2.6): this courtyard is a real cut in the floor
           diaphragm on a seismically live site (Islamabad). Edge beam on all
           four sides is load-bearing AND seismic-load-path-critical — say so
           explicitly to the structural engineer, not just "size an edge beam."**
           Islamabad winter-sun-to-floor would need W = 6.7 × 1.55 = 10.4 m —
           not achievable; courtyard serves daylight + stack ventilation, and
           winter gain comes from the south rear facade instead.
ORIENTATION North-open → entrance and drawing room north (excellent: no heat gain
           on the guest facade). Living/lounge to the south rear with a 0.35 m
           chajja (Islamabad summer altitude 79.7° → D = 2.1/5.49 = 0.38 m).
           Islamabad prevailing winds N and SE → inlets on the north and
           south-east faces, outlet at the courtyard/stair skylight.
           WWR: north 28%, south 25% (Islamabad wants winter gain), east 10%, west 5%.
GROUND     Drawing 14×16 + powder | foyer | lounge 14×18 | dining 11×13 |
           kitchen 9×12 + dirty kitchen 6×8 | bedroom 12×14 + bath 6×8 |
           courtyard 12×14 (centred) | stair 8×13 | store 6×8 | servant 8×10 + 4×6
FIRST      Master 14×16 + bath 6×8 | bedrooms 12×14 ×2 + baths | family lounge
           14×16 | terrace over porch | stair stacked | courtyard void
ROOF       Solar panels south-tilted (~34° for Islamabad latitude); mumty placed
           north side of roof plate to keep its shadow off the panel zone (9.6).
STRUCTURE  RCC frame, 14 ft grid. Courtyard on grid lines with an edge beam all
           four sides, treated as a seismic diaphragm requirement (2.6/9.4), not
           only a gravity one. Lounge 14×18 → 18 ft span needs 15 in beam or a
           mid-beam; slab depth for this span is 6–6.9 in per the corrected 9.4
           table (not 5–6 in).
CHECKS     Coverage 1,800/2,723 = 66% — consistent with placeholder (under the
                                        70% cap; setbacks bound it) — CONFIRM
           Circulation ~9% ✓ | Courtyard W/H 0.55 in optimum band ✓
           Wet zones stacked ✓ | GF bedroom + bath ✓ | escape windows ✓
           Courtyard flagged to engineer as diaphragm/seismic item ✓
```

### 12.3 1 Kanal, 50×90 ft, Multan, west-open, G+1 — the hard orientation

```
PLOT       50 × 90 = 4,500 sq ft (1 kanal, 225 basis — CONFIRM which basis)
BYLAW      Band 10 marla–1 kanal (T1-U — see 2.1): coverage 70% → footprint 3,150 sq ft
           FAR 1:1.5 → cap 6,750; G+1 = 6,300 (placeholder — CONFIRM before use)
WATER TABLE  Multan is inland, generally moderate water table away from canals —
           still confirm with a site soil report before assuming a basement is
           feasible if the brief later needs one (2.4a); not exercised in this
           example since the brief fits G+1.
PROBLEM    West-open in Multan (hot desert, BWh) — the entrance facade takes the
           full afternoon load, and no horizontal overhang shades a west window
           (D = 2.1/tan 27° = 4.1 m).
STRATEGY   1. Buffer the west: porch (18×20), garage, stair, store, servant room
              and all baths on the west strip. Zero west-facing habitable glazing.
           2. Deep verandah 8 ft along the west entrance face — the only working
              west shading device at this scale.
           3. Jaali screen to the west verandah: airflow retained, sightline and
              radiation cut.
           4. Courtyard 20×24 ft centred (2.6), long axis E–W. W/H = 6.1/6.7 = 0.91
              → balanced band; plant one shade tree + a water channel.
              **Diaphragm flag (2.6): a 20×24 ft cut on a 1-kanal plate is
              substantial — explicit edge-beam-as-seismic-load-path note to the
              engineer, same as 12.2.**
              Multan is extreme: add retractable summer shade over the courtyard.
              Quote the courtyard performance per Section 6.1's corrected framing
              (a specific mud-brick study's ~20% annual-energy finding, not a
              blanket "20–30% cooling load" claim) — Multan's masonry-frame
              construction will not replicate that study's numbers exactly.
           5. Bedrooms all on the north and east.
           6. Living/lounge south with 0.30 m chajja (Multan summer alt 83.2°
              → D = 2.1/8.35 = 0.25 m; use 0.30 m for rain).
           7. Thermal mass: 13.5 in external brick on the west and south faces.
           8. Roof: 75 mm insulation + shaded terrace, zoned separately from the
              solar panel area per 9.6 — the largest gain surface.
WWR        North 25%, south 18%, east 8%, west 0% habitable (verandah openings only).
CHECKS     Coverage 3,150/4,500 = 70% — consistent with placeholder — CONFIRM
           west habitable glazing = 0 ✓
           Courtyard W/H 0.91 ✓ | all baths stacked over baths/service ✓
           Courtyard flagged to engineer as diaphragm/seismic item ✓
```

### 12.4 2 Kanal, 100×109 ft, Islamabad CDA low-density sector

```
PLOT       100 × 109 = 10,900 sq ft
BYLAW      CDA low-density (T1-U, unverified — see 2.4, no citable regulation
           document behind this figure): ground coverage reportedly 20–25% →
           footprint 2,180–2,725 sq ft (drastically different from LDA's 65% —
           CONFIRM the actual sector schedule before using this number for
           anything beyond an initial massing conversation with the client)
ARCHETYPE  Pavilion (8.6) — the reported coverage cap would force it, if confirmed.
           A plot-filling block would be illegal here under the placeholder figure;
           the house is treated as an object in a garden pending confirmation.
MASSING    G+1 at ~2,500 sq ft/floor = 5,000 sq ft covered on a 10,900 sq ft plot.
           75–80% of the plot would be landscape, under the placeholder figure.
BUDGET     Carpet = 5,000 × 0.68 = 3,400 sq ft → this reads as a 5-bedroom house,
           NOT the 8-bedroom the plot size alone would suggest. IF the 20–25%
           coverage figure is confirmed, tell the client at the first meeting that
           the coverage cap, not the plot area, sets the brief.
CONSEQUENCE All four facades exposed → complete shading strategy required, not
           partial. Every facade gets its correct device (Section 7.5).
           **Seismic note (2.6): keep each pavilion wing to roughly 1:3–1:4
           width:length; Islamabad is a real seismic zone and a long thin wing
           on a low-density pavilion plan is exactly the soft-axis condition
           Section 2.6 warns about.**
           A courtyard is optional here (the garden does the work), but a small
           internal court still helps stack-ventilate a deep plan — if used,
           still centre it and flag it per 2.6.
NOTE       This is the case where the tower-derived "maximise NTG" instinct is
           actively wrong. Efficiency is irrelevant; envelope performance and
           the house-to-garden relationship are everything. It is also the case
           in this whole document with the least-verified bylaw number (2.4) —
           lead with that caveat, not with the massing conclusion, when this
           reaches the client.
```

---

## Section 13: Common Failure Modes — Red-Flag Checklist

Run this list against any plan before presenting it. Each line is a real, recurring defect in Pakistani house design, with the fix.

| # | Failure | Fix |
|---|---|---|
| 1 | Marla basis assumed, not confirmed | Ask for the deed. 17% of the plot is at stake (1.1). |
| 2 | Coverage checked, setbacks not — or vice versa | Run both, adopt the smaller footprint (2.3). |
| 3 | Basement assumed FAR-exempt | Confirm in writing with the authority before it is designed in (2.2) — and check the water table, not just the FAR rule (2.4a). |
| 4 | Brief never tested against available carpet | Run the Section 3.8 arithmetic before drawing. |
| 5 | Every room quietly shrunk 10–15% to make the brief fit | Drop a room instead. A house of undersized rooms is worse than a smaller house. |
| 6 | No ground-floor bedroom with attached bath | Add it. Most-requested, most-omitted item in Pakistani briefs (9.2). |
| 7 | Bathroom over a bedroom | Restack. Wet-on-wet only (9.1). |
| 8 | Stair not stacked between floors | Restack, or accept a transfer beam and its cost. |
| 9 | Stair with no natural light | Half-landing window onto the courtyard/light well, or a mumty skylight (5.4). |
| 10 | Stair riser derived from a guessed F2F | Recompute from the real F2F; state riser, tread and 2R+T (5.2). |
| 11 | Understair powder room with <6'-6" headroom | Move it under the upper flight; check the 5-tread headroom rule (5.2). |
| 12 | Winder stairs in a family house | Replace with a dog-leg. Winders and children do not mix (5.3). |
| 13 | West-facing habitable glazing with a horizontal overhang | No horizontal device works on west. Jaali, verandah, fins, or no window (7.5). |
| 14 | Kitchen on the west | Move to north/east, or add a north dirty kitchen (7.3). |
| 15 | Window sized by eye, fails the 1/10 rule | Compute: floor area ÷ 10 ≤ window area (4.3). |
| 16 | Sliding windows counted at full area for ventilation/escape | Halve them. Count openable, not glazed (4.3, 4.5). |
| 17 | Bedroom with only one opening | Add a second on a different wall, or a roshandan (7.6). |
| 18 | Burglar grilles fixed over the only escape window | Specify one quick-release grille per bedroom, key in the room (4.5). |
| 19 | "Courtyard" at W/H 0.15 sold as a climate feature | Call it a light well. It ventilates; it does not perform thermally (6.6). |
| 20 | Courtyard fully paved, no planting or water | ≥30% soft/planted floor or the evaporative half of the mechanism is gone (6.4). |
| 21 | Courtyard with no high-level outlet | Stack ventilation needs an exit: stair skylight or mumty vent (6.4). |
| 22 | Courtyard draining toward the house | Slope ≥1:100 to a gully, away from thresholds (6.4). |
| 23 | Passage serving fewer than three doors | Re-plan around a shared node (10.3). |
| 24 | Main door with a direct sightline to the lounge or a bedroom | Foyer, L-turn or screen wall (4.4, 11). |
| 25 | Guest must cross the family zone to reach a WC | Powder off the foyer or drawing room (3.5). |
| 26 | Column stranded mid-room | Move the room to the grid, or move the grid (9.4). |
| 27 | Overhead water tank sitting mid-span | Support it over a wall or column line — 2.3 t per 500 gal (9.1, 9.6). |
| 28 | Rental upper floor with the stair inside the ground-floor unit | Unfixable later. Decide at first sketch (8.8). |
| 29 | Circulation over 18% of covered area | Usually a misplaced stair. Re-place it before anything else (10.3). |
| 30 | Output presented as construction-ready | Say the caveat, unprompted, in that reply (Reality Check). |
| 31 | A T1-U (unverified) coverage/FAR/setback figure quoted to a client or authority as if confirmed | Say "unverified — flagged for confirmation against the current bylaw" every time (Section 0, 2.1, 2.4). |
| 32 | L-shape, courtyard, long-wing pavilion, or split-level plan handed off with no seismic plan-irregularity note | Attach the specific Section 2.6 flag to that specific decision in the handoff, not just in a closing paragraph. |
| 33 | Roof laid out with mumty, panels, terrace shade and OH tank as if they don't interact | Zone the roof explicitly per 9.6 — panel zone, terrace zone, mumty position, tank support line. |

---

## Section 14: FreeCAD / BIM Handoff Checklist

Before modelling (see `architecture-freecad-bim` for the actual object hierarchy):

**Confirmed inputs**
- [ ] Marla basis (272.25 or 225 sq ft) confirmed from the deed, not assumed
- [ ] Plot dimensions and orientation (which side is the road)
- [ ] City → latitude, prevailing wind, climate zone (Section 7.2)
- [ ] Authority (LDA/CDA/RDA/DHA/Bahria/TMA) and its **current, sourced and cited** coverage, FAR, setback, height and mumty schedule — **the Section 2.1/2.4 tables in this document are T1-U placeholders and must be replaced with confirmed figures before this box is checked**
- [ ] Whether basement is FAR-exempt — in writing — AND whether the site's water table makes it physically feasible (2.4a)
- [ ] Brief tested against the carpet budget (Section 3.8) and it fits
- [ ] Plan archetype checked against Section 2.6's seismic plan-irregularity notes if it is an L-shape, courtyard, long-wing pavilion, or split-level

**Dimensional defaults to set in the model**
| Parameter | Value |
|---|---|
| External wall | 230 mm |
| Internal partition | 115 mm |
| Load-bearing internal | 230 mm |
| Slab | 150 mm (up to 14 ft span — deeper beyond, see 9.4) |
| Floor-to-floor | 3200 mm (3350 for generous) |
| Plinth | 600 mm above road crown |
| Door height | 2134 mm |
| Window head | 2134 mm |
| Window sill (habitable) | 900 mm |
| Window sill (bath/kitchen) | 1200 mm |
| Ventilator sill | 1980 mm |
| Stair riser / tread | 160 / 265 mm (compact) or 160 / 300 mm (comfortable) |
| Chajja projection | 300 mm south, 450 mm east, verandah on west |
| Parapet | 1050 mm |

**Spatial hierarchy** — Site → Building → Storey (Ground, First, Roof), with rooms as Spaces so areas can be scheduled and coverage/FAR verified from the model rather than by hand.

**Verify in the model before presenting**
- [ ] Ground-floor footprint area ≤ coverage limit **and** within the setback envelope — read both off the model, not the sketch — **and both are still T1-U pending confirmation**
- [ ] Sum of all floor areas ≤ FAR cap; mumty within its separate allowance
- [ ] Every bathroom sits over a bathroom, kitchen, store or utility
- [ ] Stair footprint identical on both floors; mumty over the stair
- [ ] Stair: 2R+T computed and stated; headroom ≥ 2100 mm checked at the flight underside
- [ ] Every bedroom has an external openable window meeting the escape-opening geometry
- [ ] Every habitable room's openable window area ≥ 1/10 of its floor area (openable, not glazed)
- [ ] No habitable room below the NBC 7.5 m² floor (and none below the T4 target without a stated reason)
- [ ] Passage clear width ≥ 1219 mm everywhere; ≥ 914 mm absolute nowhere breached
- [ ] Courtyard W/H computed and reported against the Section 6.3 bands; if present, flagged as a diaphragm/seismic item per 2.6
- [ ] Zero west-facing habitable glazing without a stated shading device; WWR per facade reported
- [ ] Circulation as % of covered area computed and ≤ 14%; NTG computed against Section 10.2
- [ ] Every column sits inside a wall line; no stranded columns
- [ ] Roof zoned for panels / terrace shade / mumty / OH tank with no shadow or structural conflict (9.6)
- [ ] Section 13 red-flag list run end to end, including items 31–33

**And then say it — attached to the specific decisions it applies to, not only as a closing line:** *"This is a planning model. It is not construction-ready and must be reviewed and stamped by a PEC-registered engineer and approved by [authority] before construction. In particular: [name the T1-U figures still needing confirmation] and [name any L-shape/courtyard/split-level plan-irregularity flagged per Section 2.6] need explicit engineer sign-off, not just the general caveat."*

---

## Appendix A: Standards and References

| Source | Scope | Tier | Jurisdiction |
|---|---|---|---|
| **Building Code of Pakistan (BCP) 2007 — Seismic Provisions** | Structural/seismic only. **Not a source for room sizes, egress or circulation** | T1 (structure) | Pakistan |
| **BCP 2021 Final Draft** (Pakistan Engineering Council) | Successor draft; still structure-weighted | T1 | Pakistan |
| **LDA Building Regulations** | Ground coverage %, FAR, setbacks by plot band | **T1-U in this document (Section 2.1) — pull the current dated regulation before use** | Lahore |
| **CDA Islamabad building bylaws** | Coverage (reported 20–25% low-density sectors), setbacks, commercial FAR reported 1:10–1:12 | **T1-U in this document (Section 2.4) — no citable regulation number/date/URL held here; pull the actual document** | Islamabad |
| **RDA / SBCA / PDA / TMA / Cantonment Board bylaws** | Local coverage, setbacks, approval | **T1-U — confirm per authority** | Respective |
| **DHA / Bahria Town building regulations** | Scheme-specific, often stricter than the city authority | **T1-U — confirm per scheme** | Scheme |
| **NBC India 2016, Parts 3 & 4** | Habitable room / kitchen / bath minimum areas, ceiling heights, stair geometry | **T2 — not Pakistani law** | India (de facto reference) |
| **IS 456** | Stair riser/tread geometry, RCC | T2 | India |
| **IRC R311.6 / R311.7** | Residential hallway 36 in, stair riser 7¾ in / tread 10 in | T3 | USA |
| **IRC R310** | Emergency escape opening geometry (5.7 sq ft, 24 in h, 20 in w, 44 in sill) | T3 | USA |
| **IBC Chapter 10** | Means of egress principles where local code is silent | T3 | USA |
| **PEC (Pakistan Engineering Council)** | Engineer registration — required for structural sign-off | Legal | Pakistan |
| **PCATP** | Architect registration — required for architectural drawings | Legal | Pakistan |
| *Climate responsive courtyard design for urban sustainability in five Marla houses in Rawalpindi* (Discover Cities, Springer Nature, 2026) | Courtyard performance **at 5-marla scale** — cite by name; do not merge its figures with other courtyard studies | **T5** | Pakistan |
| Mud-brick/wind-catcher courtyard variant study (South Asia arid-climate literature) | Reports ~20% **annual energy** reduction for that specific variant — **not** a general "cooling load" figure; cite the specific variant when quoting | **T5** | Pakistan/regional |
| *Building Orientation and Its Effect on House Plan Configuration for the Climate of Lahore* | SW orientation optimum for Lahore | T5 | Pakistan |
| *Enhancing Energy Conservation, Visual and Thermal Comfort in Small Houses of Karachi* (JAABE) | Karachi small-house comfort, wind from ~245° | T5 | Pakistan |
| *The Traditional Courtyard House of Lahore* | Vernacular courtyard typology analysis | T5 | Pakistan |
| **Neufert Architects' Data** | Furniture and clearance dimensions | T4 | International |
| Kevin Lynch, *The Image of the City* (1960) | Legibility theory (Section 11) | Theory | Academic |

## Appendix B: Rules of Thumb

| Parameter | Value |
|---|---|
| 1 Marla | 272.25 sq ft (or 225 sq ft — **confirm the basis**) |
| 1 Kanal | 20 Marla; 8 Kanal = 1 Acre |
| 1 sq m | 10.764 sq ft |
| Deduct for two 9 in external walls | 1.5 ft off the plot frontage |
| Minimum workable master bedroom | 12 × 14 ft |
| Minimum workable kitchen (single cook) | 7'0" × 9'6" |
| Minimum 3-fixture bathroom | 5 × 8 ft |
| Minimum internal passage | 4'-0" (1219 mm); absolute floor 3'-0" (914 mm) |
| Pakistani vernacular passage | 7'-0" (2134 mm) |
| Dog-leg stair well (3200 mm F2F) | 7'-1" × 11'-9" to 12'-10" |
| Stair comfort rule | 2R + T = 600–640 mm (target 620) |
| Car bay | 9 × 18 ft; SUV 9 × 20 ft |
| Circulation share of covered area | 8–14% target, >18% is waste |
| Walls share of covered area | 8–12% (9 in brick) |
| Carpet : covered ratio | 65–75% typical |
| Brief-fit test | required carpet ÷ available carpet ≤ 0.95 |
| Courtyard W/H, hot-dry optimum | 0.3–0.7 |
| Courtyard W/H factor for winter sun to floor | 1 / tan(winter solar altitude) |
| Courtyard cooling performance | study-specific — ~20% annual energy for one mud-brick/wind-catcher variant (6.1); do not restate as a universal "20–30% cooling load" figure |
| Orientation-only temperature saving | ~5–7 °C reported in the Pakistan orientation literature — order-of-magnitude, not guaranteed |
| WWR targets (hot-dry) | N 20–30%, S 15–25%, E 8–12%, W 0–8% |
| South chajja depth (Punjab, 7 ft window) | 300 mm |
| West window shading | no horizontal overhang works — use jaali/verandah/fins |
| Cross-ventilation outlet : inlet | 1.25 : 1 to 1.5 : 1 |
| Openable window area | ≥ 1/10 of room floor area (openable, not glazed) |
| Escape opening | ≥5.7 sq ft net, ≥24 in high, ≥20 in wide, sill ≤44 in |
| One-way slab depth | span/28 to span/32 (4.5–6 in up to 14 ft; 6–6.9 in at 14–16 ft — do not use 5–6 in past 14 ft) |
| Beam depth | span/12 to span/15 |
| Soil stack | 100 mm per bathroom group; fall 1:40–1:60 |
| Overhead tank weight | ~2.3 t per 500 gallons — support on a wall/column line, clear of solar panel structure (9.6) |
| Mumty allowance | 9–13% of plot area, on top of coverage |
| Coverage/FAR/setback figures in Sections 2.1/2.3/2.4 | **T1-U — unverified placeholders. Confirm against the current dated bylaw before any client-facing or submission use.** |

## Appendix C: Daylight Depth vs Ceiling Height

Effective daylight penetration is approximately **2.0–2.5× the window head height** above floor.

| Floor-to-ceiling (m) | Window head (m) | Effective daylight depth (m) | In feet |
|---|---|---|---|
| 2.75 (NBC min) | 2.13 | 4.3–5.3 | 14–17 ft |
| 3.05 (10 ft) | 2.13 | 4.3–5.3 | 14–17 ft |
| 3.35 (11 ft) | 2.44 | 4.9–6.1 | 16–20 ft |
| 3.66 (12 ft) | 2.75 | 5.5–6.9 | 18–23 ft |
| 4.27 (14 ft, drawing room) | 3.35 | 6.7–8.4 | 22–27 ft |

**Consequence for house planning:** with a standard 2134 mm window head, a room deeper than **~17 ft loses useful daylight at the back**. That is precisely why 12×14 and 14×16 are the recurring Pakistani room sizes — beyond ~17 ft of depth from the window you need a second aspect (courtyard, light well, clerestory) or the room goes dark. Rooms deeper than 2.5× window head require: a courtyard-side opening, a clerestory above 2.75 m, a light shelf, or borrowed light through a transom.

## Appendix D: Client Intake — Ask These Before Planning

Never begin a plan with any of these unanswered. An assumption here costs a redesign later.

**Plot and legal**
1. Which marla basis does the deed use — 272.25 or 225 sq ft?
2. Exact plot dimensions, and which side is the road (east-open, north-open…)?
3. Which authority approves: LDA, CDA, RDA, SBCA, DHA, Bahria, TMA, Cantonment?
4. Current coverage %, FAR, setback and height schedule for this plot band — obtained, not assumed, and NOT taken from this document's Section 2 tables (those are flagged T1-U)?
5. Is a basement permitted, and is it FAR-exempt? In writing? And is the site's water table checked (2.4a)?
6. Corner plot, or party walls on both sides? Any existing neighbour construction to match?
7. Is the plot level, or sloping? Slope > 1:10? (Triggers the Section 2.6 split-level seismic note.)
8. Road width in front (determines whether a car can turn into the porch).

**Brief**
9. Number of bedrooms, and how many need attached baths?
10. Separate drawing room, or merged into the lounge?
11. Dirty kitchen required?
12. Servant quarter — attached or detached? Separate external entry?
13. Will the upper floor ever be let separately? (Decides stair position permanently.)
14. Cars to be parked — how many, what size?
15. Any elderly or wheelchair-using occupant, now or foreseeable? (Kills split-level; mandates a GF bedroom.)
16. Prayer space / wudu point required?
17. Single storey now with a floor added later? (Changes foundation and column design today.)

**Context**
18. City — for latitude, prevailing wind, climate zone, and which orientation rules apply.
19. Flood-prone or low-lying area? (Sets plinth height.)
20. Budget band — grey structure only, or finished? (Sets ceiling height, courtyard, finishes.)
21. Is the site in a locally elevated seismic zone (Islamabad hills, Peshawar, Murree)? (Triggers the Section 2.6 plan-irregularity checks for any L-shape/courtyard/pavilion/split-level archetype.)
22. Will solar panels and/or an OH tank be needed at roof level? (Triggers the Section 9.6 roof-zoning coordination.)

**Then, and only then, start at Section 0.5 Step 1.**
