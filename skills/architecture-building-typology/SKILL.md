---
name: architecture-building-typology
description: >
  Residential building typology for Pakistan — selecting and dimensioning the
  right building type for a plot. Covers the marla/kanal plot ladder and the
  typology it implies, detached houses (3/5/7/10 marla, 1 kanal), portion houses
  (upper/lower — Pakistan's real "duplex"), true duplexes and maisonettes,
  row houses/townhouses in gated schemes, farmhouses (1–5 kanal, courtyard/wind-
  tower/jaali configurations), and apartment blocks (walk-up, mid-rise, tower).
  Gives plot-size-driven house configurations, room programs with real numeric
  dimensions, unit mix, floor plate and core design, net-to-gross efficiency at
  house scale, structural typology selection (confined masonry vs RC frame) tied
  to BCP-SP-2007 and ACI 318-19, 2026 PKR cost bands per typology, and FreeCAD
  modelling recipes. Retains the general international typology reference
  (office, healthcare, education, cultural, hospitality, mixed-use, Western
  residential) as a secondary comparison layer.
---

# Building Typology — Pakistan Residential First

Typology is the decision that comes *before* room sizing and *after* the plot is known. Get it wrong and no amount of good plan-making rescues the project: a 5-marla plot laid out as if it were a 1-kanal house produces four rooms nobody can furnish; a 2-kanal farmhouse laid out as a scaled-up 10-marla house produces a dark, corridor-ridden box on a plot that could have carried a courtyard. In Pakistan the typology question is unusually well-determined, because the plot itself arrives pre-quantised — 3, 5, 7, 10, 20 (1 kanal), 40 (2 kanal) marla — and each rung of that ladder has a *conventional* built form, a conventional bedroom count, a conventional structural system, and a conventional buyer expectation. This skill encodes that ladder, then encodes the typologies that sit off it: the **portion house** (which Western typology literature has no name for and which is probably the most-built multi-unit form in urban Pakistan), the **farmhouse**, the **apartment block**, the **true duplex**, and the developer-built **row house / townhouse**.

This is the typology-selection layer. It deliberately does **not** re-derive room minimums, courtyard sun-angle proportioning, stair geometry, or setback law — those belong to `architecture-spatial-planning` and `architecture-building-codes-permits` respectively, and are cross-referenced rather than duplicated.

## Reality Check - Licensing & Liability

**This skill produces design aids, typological envelopes and calculation guidance for planning and FreeCAD modelling ONLY.**

- Nothing in this file is a construction document. No typology table, no floor plate, no room program, no slab thickness, no span limit, no cost figure, and no FreeCAD model derived from them is buildable as-is.
- Any design intended for the actual construction of a real, occupied building **MUST be reviewed, sealed and stamped by a licensed structural engineer registered with the Pakistan Engineering Council (PEC)**, and the architectural drawings by a **PCATP-registered architect** (Pakistan Council of Architects and Town Planners).
- The design **MUST go through local authority plan/map approval before construction** — LDA (Lahore), CDA (Islamabad), RDA (Rawalpindi), SBCA/KDA (Karachi), PDA (Peshawar), FDA (Faisalabad), the relevant TMA or Cantonment Board, or the private scheme's own building control (DHA, Bahria Town). **Their current byelaw schedule overrides every coverage, FAR, setback, height and unit-count number printed here.**
- The structural guidance here (confined masonry vs RC frame, slab thickness by span, wall thickness) is a **preliminary sizing aid to test whether a typology is plausible on a plot**. It is not a structural design. Member sizes, reinforcement, seismic detailing and foundation design are the PEC-registered engineer's territory, governed by **BCP-SP-2007 / BCP 2021** and **ACI 318-19**.
- **Claude must never present FreeCAD output or these calculations as construction-ready, permit-ready, or "approved" without that human sign-off.**
- **If a user appears to be treating the output as final** — talking about pouring a plinth, ordering steel or bricks, briefing a contractor, submitting to the authority, or saying "so we're good to build" — **say so unprompted, in that same reply, before answering anything else**: *"This is a typology and planning study, not a stamped drawing. A PEC-registered structural engineer has to review and stamp it, and it needs [authority] map approval before anyone breaks ground."*
- Cost figures are 2026 market bands from commercial sources, not quotations. They move with cement, steel and the exchange rate. Never present them as a budget without a dated caveat.

---

## Section 0: How to Use This Skill

### 0.1 Relationship to the sibling architecture skills

| Question | Skill that owns it |
|---|---|
| *"What kind of building goes on this plot? How many units? What floor plate? What's the core? What's the unit mix?"* | **This skill** |
| *"How big should the bedroom be? Where does the stair go? How wide is the passage? How do I proportion the courtyard for sun angle?"* | `architecture-spatial-planning` |
| *"What's the legal setback / coverage / FAR / height? How do I get the map approved? Who stamps it?"* | `architecture-building-codes-permits` |
| *"What seismic zone, confined masonry or frame, what's the base shear, what detailing?"* | `architecture-seismic-design` |
| *"What grid, what span, what beam depth, what lateral system?"* | `architecture-structural-systems` |
| *"What rebar, what lap length, what cover?"* | `architecture-concrete-reinforcement-detailing` |
| *"What's the BOQ, what does it cost per element?"* | `architecture-cost-estimation-boq` |
| *"Model it in FreeCAD"* | `architecture-freecad-bim` (+ Section 15 here for the typology-specific recipe) |

**Routing rule:** if the user's question is *"which building form"*, start here. If it is *"how big is the room"*, hand to spatial-planning. If it is *"is this legal"*, hand to codes-permits. Typology sits upstream of all of them, and every typology decision made here must then be re-tested against the byelaw envelope.

### 0.2 Evidentiary tiers (shared vocabulary with `architecture-spatial-planning`)

Pakistan has no codified residential typology standard. Every number below carries a tier. **Never present a T2/T3/T4 number as if it were Pakistani law.**

| Tier | Label | Source | Status |
|---|---|---|---|
| **T1** | Legally binding | LDA / CDA / SBCA / RDA / FDA / DHA byelaws; BCP for structure | Enforceable — approval fails without it |
| **T2** | Nearest codified reference | NBC India 2016, IS 456 | NOT Pakistani law; de facto practitioner reference |
| **T3** | Imported baseline | IRC 2021 (US), IBC 2021, ACI 318-19, ASCE 7-22 | Not adopted in Pakistan (ACI/ASCE partially by BCP reference); rigor benchmark |
| **T4** | Vernacular / built practice | Measured Pakistani house plans, developer plans, market norms | No legal force; **this is what clients actually expect** |
| **T5** | Empirical / peer-reviewed | World Housing Encyclopedia Report 173, climate studies | Performance data, not code |

Typology work lives overwhelmingly in **T4**. That is not a weakness — bedroom counts, portion-house conventions and farmhouse programs are cultural facts, and T4 is the correct evidence class for them. State the tier when quoting.

### 0.3 The five questions to answer before selecting a typology

Never propose a typology without all five. If one is unknown, say which decisions are blocked on it.

1. **Plot size and dimensions** — in marla/kanal *and* in feet (`45×25`, `50×90`). The marla is not a fixed unit (Section 2.1).
2. **Authority and scheme/phase** — determines coverage %, setbacks, whether an upper portion may have its own street entrance, whether apartments are permitted at all, and (above 1 kanal) whether the plot is actually farmhouse-zoned or just farmhouse-sized inside an ordinary residential scheme (Section 7.6).
3. **Occupancy model** — single family? family + rented upper portion? multi-generational (married sons)? investment/rental block? weekend farmhouse? developer row-house product?
4. **Budget class** — grey-structure-only, standard finish, or premium (drives typology as hard as plot size; a 1-kanal plot on a 10-marla budget should be built as a 10-marla house core with future expansion, not a hollow kanal shell).
5. **Number of bedrooms required, now and in 10 years** — the single strongest predictor of whether a plot band works.

---

## Section 1: Typology Selection Decision Tree

```
START: plot area + occupancy model + budget known?
  ├─ NO  → ask the five questions (0.3). Do not guess.
  └─ YES ↓

Is the plot ≤ 5 marla (≤ 1,250 sqft)?
  ├─ YES → DETACHED COMPACT HOUSE, G+1 mandatory (a single storey wastes the plot)
  │        Structure: confined masonry, 9" external / 4.5" internal
  │        Program: 3 bed / 1 lounge / 1 drawing / 1 kitchen / 2–3 bath / 1 car porch
  │        Do NOT attempt: internal courtyard (kills too much area), separate dining,
  │                        double-height space, side gali, basement (rarely economic)
  │        Portion split possible but tight — see Section 5.4
  │
  ├─ 7–10 marla (1,575–2,450 sqft)?
  │   ├─ Single family, one household     → DETACHED HOUSE G+1, 4–5 bed (Section 3.3)
  │   ├─ Family + rental income           → PORTION HOUSE (Section 5) — this is the
  │   │                                      dominant real answer in urban Punjab/Sindh
  │   ├─ Two related households, one deed → PORTION HOUSE with shared boundary wall
  │   │                                      + separate meters, no shared stair
  │   └─ Part of a gated-scheme block     → ROW HOUSE / TOWNHOUSE (Section 5.5) —
  │                                          when the developer, not the family, is
  │                                          driving the product
  │
  ├─ 1 kanal (4,500 sqft)?
  │   ├─ Single family, premium           → DETACHED HOUSE G+1(+basement), 5–6 bed,
  │   │                                      drawing + dining + family lounge split,
  │   │                                      2–3 car, servant quarter (Section 3.4)
  │   ├─ Rental yield priority            → APARTMENT BLOCK G+3/G+4, 3–4 units/floor
  │   │                                      (Section 8) — check byelaw permits apartments
  │   └─ Two households, formal split     → TRUE DUPLEX, two vertically stacked units
  │                                          each with internal stair (Section 6)
  │
  ├─ 2–5 kanal (9,000–22,500 sqft)?
  │   └─ FARMHOUSE (Section 7) — **first confirm the plot is actually farmhouse-zoned,
  │      not just farmhouse-sized inside an ordinary residential scheme (Section 7.6
  │      — this is a T1 gate, check it before quoting any coverage number).**
  │      If farmhouse-zoned: coverage drops to 40–55%; the plot's value is the
  │      landscape, not the covered area. Courtyard/atrium plan, split wings,
  │      RC frame mandatory (spans + double-height), basement viable and normal.
  │      Do NOT scale up a 10-marla plan — it produces a dark corridor building.
  │
  └─ Multi-plot / commercial-zoned site?
      └─ APARTMENT BLOCK, mid-rise or tower (Section 8). Now the core, lift count,
         corridor length and NTG ratio become the governing design problem, not
         the room program.
```

### 1.1 Overriding constraints that beat the tree

Apply these *after* the tree and let them override it:

| Constraint | Override |
|---|---|
| Byelaw prohibits apartments in the scheme (most DHA residential phases) | Apartment branch is dead regardless of yield logic. Fall back to portion house or duplex. |
| Corner plot | Two street frontages → portion house becomes *much* stronger (independent street entrances without an external side stair). Also unlocks side-entry car access. |
| Plot depth > 2.2 × width (deep narrow plot) | Courtyard/light-well becomes mandatory at any size ≥ 7 marla; central-passage plan fails. |
| Plot width < 25 ft | Car porch + entrance + stair compete for the same frontage. Drop to a single-car porch and side-entry stair, or accept no ground-floor bedroom. |
| Seismic Zone 3–4 (Muzaffarabad, Quetta, northern KP/AJK) | Load-bearing masonry above G+1 is off the table (see `architecture-seismic-design`). RC frame from the start; this reshapes the plan (columns on a grid, not walls where you want them). |
| Water table high / basement in Karachi coastal or riverine Punjab | Basement typology (theatre, parking, staff) becomes expensive and risky. Budget waterproofing before committing the program to a basement. |
| Client budget below ~PKR 5,800/sqft turn-key | Do not propose a typology whose covered area the budget cannot finish. Build a smaller covered area well, or build grey and finish in phases. |
| Plot 2+ kanal but inside an ORDINARY residential scheme, not a farmhouse-designated one | Farmhouse coverage tables (Section 7.1) do NOT apply. Normal kanal-band coverage (65–70%, Section 2.3) governs instead — see Section 7.6 before quoting a footprint. |

---

## Section 2: The Pakistani Plot Ladder

### 2.1 Unit definitions (T1/T4 — the marla is not one unit)

| Basis | 1 Marla | 1 Kanal (= 20 marla) | Where it applies |
|---|---|---|---|
| **Standard / housing-society marla** | **225 sqft** (25 sq yd) | **4,500 sqft** | Most of Punjab, DHA schemes nationwide, LDA schemes, general market |
| **Islamabad / some CDA-area societies** | **272.25 sqft** (30.25 sq yd) | **5,445 sqft** | Some Islamabad societies and older revenue records |
| **Revenue-record (rural) marla** | Varies by district, can exceed 272.25 sqft | Varies | Rural/agricultural land, inherited plots, un-regularised land |

**The 21% trap:** 272.25 / 225 = 1.21. A "1 kanal" plot in an Islamabad society can be 945 sqft (21%) larger than a "1 kanal" plot in Lahore. **Always confirm the plot in feet, never work from the marla figure alone.** If a client says "1 kanal" and you cannot get the dimensions, state your assumption explicitly in writing.

### 2.2 The ladder — plot band → conventional typology (T4)

Assumes the **225 sqft standard marla**. "Covered" = gross covered area across all floors including stair/mumty, on typical byelaw coverage.

| Plot | Area (sqft) | Common dimensions (ft) | Conventional typology | Storeys | Beds | Typical covered (sqft) | Structure |
|---|---|---|---|---|---|---|---|
| 3 marla | 675 | 20×34, 25×27 | Minimal detached / row-adjacent | G+1, often G+2 | 2–3 | 1,050–1,300 | Confined masonry |
| **5 marla** | **1,125** | **25×45** (DHA 25×50 = 1,250; older LDA 20×45 = 900, 25×40 = 1,000) | **Compact detached** | **G+1** | **3** | **1,750–2,000** | Confined masonry |
| 7 marla | 1,575 | 30×52.5, 35×45 | Detached | G+1 | 4 | 2,400–2,750 | Confined masonry / hybrid |
| **10 marla** | **2,250** (DHA 35×70 = 2,450 — see the reconciliation note below) | **35×65**, 30×75 | **Detached or portion house** | **G+1 (+basement)** | **4–5** | **3,300–4,650** | Hybrid or RC frame |
| 12 marla | 2,700 | 40×67.5 | Detached | G+1(+bsmt) | 5 | 3,800–5,000 | RC frame |
| **1 kanal** | **4,500** | **50×90** | **Premium detached / duplex / walk-up block** | **G+1(+bsmt)** | **5–6** | **4,710–5,770** | **RC frame** |
| 2 kanal | 9,000 | 75×120, 100×90 | **Farmhouse** (if farmhouse-zoned — Section 7.6) | G+1+bsmt | 6–7 | 8,000–9,500 | RC frame |
| 4 kanal | 18,000 | 120×150 | Farmhouse / estate | G+1+bsmt | 7–9 | ~10,140 | RC frame |
| 5 kanal | 22,500 | 150×150, 169×179 (irregular common) | Estate farmhouse | G+1+bsmt | 8–10 | 11,000–14,000 | RC frame |

**Sources:** plot dimensions and covered-area examples from Pakistani developer/architect plan sets (T4). 10-marla 4,200–4,650 sqft covered figures assume either a DHA-width plot, a basement, or gross measurement including projections — see the honesty note in Section 2.4.

**Reconciliation note — DHA's 35×70 "10 marla":** 35×70 = 2,450 sqft, which at the 225 sqft standard marla is ~10.9 marla, not 10. This is **not** a different marla basis for DHA (unlike the genuine Islamabad 272.25 sqft basis in Section 2.1) — it is DHA rounding the plot to a convenient rectangle that runs slightly over the nominal 10-marla area, the same way its 5-marla plot (25×50 = 1,250 sqft) runs over the nominal 1,125 sqft. **Always use the dimensioned figure (35×70 = 2,450 sqft), not the nominal marla count, for any buildable-area calculation** — this is the Section 2.1 "confirm in feet" rule applied to DHA's own product, and it is exactly why that rule exists.

### 2.3 Coverage and FAR by plot band (T1 — confirm against your authority)

| Plot band | Ground coverage limit | Rationale |
|---|---|---|
| Up to 10 marla | **80–85%** | Small plots would be unbuildable at lower coverage |
| Above 10 marla to 1 kanal | ~70–80% (authority-dependent) | Transition band |
| 1 kanal and above | **65–70%** | Preserve open/green character of large-plot neighbourhoods |
| Farmhouse-zoned land (2 kanal+) | Frequently **lower still (30–50%)** where the scheme has a farmhouse land-use category | The plot is meant to read as landscape with a building in it |

**Important:** the "1 kanal and above → 65–70%" row is the coverage that applies to a large plot inside an **ordinary residential scheme**. The lower farmhouse band applies only where the scheme/zone itself is designated for farmhouses. **Do not apply the farmhouse band by default just because a plot is 2 kanal or larger** — see Section 7.6 for the full decision gate and worked comparison.

**FAR:** commonly expressed as a ratio, e.g. **FAR 1:4** permits 4,000 sqft of total covered area across all floors on a 1,000 sqft plot. FAR and coverage bind *jointly* — coverage caps the footprint, FAR caps the total. Always check both; a generous FAR is useless if coverage limits your footprint and the height limit caps your storeys.

**Setbacks (T1, indicative — LDA / CDA / Etihad Town-class byelaws):**
- Front: **~5 ft** typical on small plots
- Rear: **~5 ft** typical on small plots
- Side "gali": plots **above 10 marla** must leave **5 ft on at least one side**
- Larger plots take proportionally larger setbacks; farmhouse zones take much larger.

→ Full authority-by-authority tables live in `architecture-building-codes-permits` Section 5. Use those, not these, for anything going near an approval.

### 2.4 Honesty note on market covered-area figures

Developer and estate-agent covered-area claims are systematically inflated relative to what coverage law permits. Worked check for 10 marla:

```
Plot            2,250 sqft (35 × 65 ft)
Setbacks        front 5, rear 5, one side gali 5
Buildable       30 × 55 = 1,650 sqft/floor  = 73% coverage
G+1             3,300 sqft
+ mumty                    ~120 sqft
TOTAL (no basement)  ≈ 3,420 sqft
```
A marketed "4,650 sqft covered 10 marla" therefore implies **a basement (+1,650), or a wider DHA 35×70 plot, or gross measurement counting the porch/terrace/projections.** When a client quotes a covered-area figure, ask which of those it is before designing to it. **Never quietly design to a number that the coverage byelaw does not permit** — it fails at map approval, not on site.

---

## Section 3: Detached House — The Default Typology

The detached single-family house on a rectangular urban plot is ~80% of Pakistani residential design work. Its typological variables are few and they interact tightly: **plot width** governs whether the car porch, entrance and stair can coexist on the frontage; **plot depth** governs whether the plan needs a courtyard or light well; **coverage** governs how much of that is legally usable.

### 3.1 The three canonical detached configurations (T4)

| Configuration | Plot width | How it works | Fails when |
|---|---|---|---|
| **Front-porch / rear-service** | 25–35 ft | Porch + main entry across the front; rooms in a single depth-wise sequence; kitchen and washing court at the rear | Depth > ~55 ft (middle rooms go dark) |
| **Side-passage / linear** | 30–45 ft | 3–5 ft side passage runs the plot depth; rooms open off it one side; rear court at the end | Width < 30 ft (passage eats too much of the frontage) |
| **Courtyard / central-void** | 45 ft+ (or any width with depth > 2.2× width) | Rooms wrap a central open court or double-height atrium; every room gets an external and/or courtyard face | Plot < 10 marla — the courtyard's minimum useful size (see spatial-planning §6.3) exceeds what the plot can spare |

→ Full archetype set, with plan diagrams and selection logic, is in `architecture-spatial-planning` Section 8. This table is the typology-level shortlist.

### 3.2 5 Marla detached — the canonical compact house

**Plot 25 × 45 = 1,125 sqft. Buildable at 85% ≈ 956 sqft/floor (25 × 38.25). At the more conservative 5 ft front + 5 ft rear setback: 25 × 35 = 875 sqft = 78%.**

**Reference room dimensions (T4, from Pakistani 5-marla plan sets):**

| Room | Dimension (ft) | Area (sqft) | Note |
|---|---|---|---|
| Drawing / entertaining | 14 × 11 | 154 | Guest-facing; must be reachable without crossing the family lounge |
| Family lounge | 17 × 14 | 238 | **Only fits a 25×50 DHA plot or a plan without a GF bedroom** — see check below |
| Lounge (5-marla-realistic) | 13 × 11 to 15 × 12 | 143–180 | What actually fits on a 25×45 |
| Kitchen | 11 × 9 | 99 | 7 × 14 (98) in linear-plan variants |
| Bedroom (master, GF) | 14 × 14 | 196 | With 9 × 9 (81 sqft) attached bath |
| Bedroom (secondary) | 11 × 14 | 154 | Attached bath 5 × 8 (40) |
| Drawing (alt layout) | 12 × 12 | 144 | |
| Lounge (alt layout) | 20 × 11 | 220 | Long-thin variant, doubles as circulation |
| Car porch | **10 × 14 minimum** | 140 | Usually in the front setback as an open porch where the byelaw permits |
| Stair | 8 × 14 to 9 × 16 | 112–144 | Straight or dog-leg; see spatial-planning §5 |

**Fit check — does the marketed room set actually fit?**
```
25 × 45 plot, 875 sqft buildable ground floor
Drawing 154 + Lounge 238 + Kitchen 99 + Bed 196 + Bath 81 + Stair 112 = 880 sqft
Wall loss at ~12% of gross must ALSO come out of 875.
→ DOES NOT FIT. Overshoot ≈ 110–120 sqft.

Same set on a DHA 25 × 50 plot, 1,000 sqft buildable ground floor:
Drawing 154 + Lounge 238 + Kitchen 99 + Bath 40 + Stair/passage 140 = 671
+ 12% wall loss ≈ 751 → 249 sqft left → one 12×14 (168) bedroom fits. TOTAL ≈ 919. FITS.
```
**Conclusion (state this to clients):** the widely-circulated 5-marla room schedule with a 17×14 lounge *and* a 14×14 ground-floor master belongs to a **25×50 plot**, not a 25×45. On a true 25×45, you get either the generous lounge **or** the ground-floor bedroom, not both.

**Standard 5-marla G+1 stacking (T4):**

| Floor | Program |
|---|---|
| Ground | Car porch (setback) · drawing room · lounge · kitchen · guest WC · stair · **optionally** 1 bedroom + attached bath (at the cost of lounge size) |
| First | 2–3 bedrooms with attached baths · family lounge (small, 11×12–13×14) · terrace over the porch |
| Mumty | Stair head + water tank + washing/drying terrace (~100–150 sqft, usually excluded from FAR count — **verify with the authority**) |

**Total covered:** ~1,750–2,000 sqft.

### 3.3 10 Marla detached

**Plot 2,250 sqft (35 × 65). Buildable ≈ 1,650–1,912 sqft/floor.**

**Reference room dimensions (T4):**

| Room | Range (ft) | Area (sqft) |
|---|---|---|
| Master bedroom | 14 × 16 → 16 × 18 | 224–288 |
| Secondary bedroom | 12 × 14 → 14 × 15 | 168–210 |
| Living room | 18 × 20 → 20 × 24 | 360–480 |
| Dining | 12 × 14 → 14 × 16 | 168–224 |
| Kitchen | 10 × 12 → 12 × 14 | 120–168 |
| Bathroom | 6 × 8 → 7 × 9 | 48–63 |

**Structural flag on the 20 × 24 living room:** a 24 ft clear span **cannot** be carried by the conventional 5–6 inch Pakistani slab (Section 11.3). Per the Section 11.1 decision tree, **any clear span over 16 ft already crosses out of pure confined masonry** — so this room forces at least a hybrid RC beam-and-column bay, not merely "a thicker slab" bolted onto an otherwise masonry house. The realistic options are a beam grid subdividing the span, a change to RC frame with a deep transfer beam, or a smaller room (worked in full in Section 14.2). **Flag this every time a client asks for a "big open living room" on a 10-marla plot** — it is the single most common source of "the contractor said it can't be done" mid-project.

**Standard 10-marla G+1 stacking (T4):**

| Floor | Program |
|---|---|
| Basement (optional) | Home theatre / gym / storage / servant quarter · requires waterproofing budget |
| Ground | 2-car porch · drawing room · dining · family living · kitchen + pantry/wash · guest WC · 1 bedroom + bath · stair · rear service court |
| First | Master suite (bed + dress + bath) · 2–3 bedrooms with attached baths · family lounge · front and rear terraces |
| Mumty | Stair head · laundry terrace · water tank |

**Total covered:** ~3,300–3,825 sqft without basement; 4,200–4,650 with basement or on a DHA-width plot.

### 3.4 1 Kanal detached — the premium single-family house

**Plot 4,500 sqft (50 × 90). Coverage 65–70% → GF footprint 2,925–3,150 sqft; first floor typically smaller (set back for terraces).**

**Real covered-area examples (T4, from Pakistani 1-kanal plan sets):**

| Variant | Ground (sqft) | First (sqft) | Total (sqft) | GF coverage |
|---|---|---|---|---|
| Conservative / terraced upper | 2,660 | 2,050 | **4,710** | 59% |
| Maximised | 3,110 | 2,660 | **5,770** | 69% |

**Program (T4):**

| Zone | Content | Typical area |
|---|---|---|
| Guest zone (GF, front) | Drawing room 20×16 · guest WC · separate guest entry where possible | 380–450 |
| Family zone (GF, rear) | Family lounge 20×18 · dining 16×14 · TV lounge | 700–850 |
| Service (GF, rear/side) | Kitchen 14×12 · dirty kitchen 10×8 · pantry · laundry · store · servant quarter with own WC | 450–600 |
| Sleeping (GF) | 1 bedroom + attached bath (elderly/guest) | 250 |
| Sleeping (FF) | Master suite 18×16 + dress + bath · 3 bedrooms 14×15 with attached baths · family lounge | 1,600–2,100 |
| Vehicle | 2–3 car porch/garage | 400–600 |
| Vertical | Main stair + service stair (premium builds) · mumty | 250–350 |

**Typology-level rules for 1 kanal (T4):**
- **Separate the guest sequence from the family sequence.** A drawing room a guest reaches only by crossing the family lounge is the defining failure of scaled-up 10-marla plans on kanal plots.
- **A second (service) stair** becomes worth its ~120 sqft/floor at 1 kanal — it lets staff move between kitchen, laundry and upper floors without crossing family space.
- **Set the first floor back** from at least one edge to make a usable terrace; a first floor matching the ground footprint reads as a block, not a kanal house.
- **The side gali (5 ft minimum on at least one side above 10 marla, T1) is a design asset**, not just a legal loss — it is the service/laundry access and the cross-ventilation path.

### 3.5 Detached house metric summary (Pakistan-calibrated, T4)

| Metric | 5 marla | 10 marla | 1 kanal | 2 kanal farmhouse |
|---|---|---|---|---|
| Plot (sqft) | 1,125 | 2,250 | 4,500 | 9,000 |
| GF coverage | 78–85% | 73–85% | 59–69% | 40–55% |
| Storeys | G+1 | G+1(+B) | G+1(+B) | G+1+B |
| Total covered (sqft) | 1,750–2,000 | 3,300–4,650 | 4,710–5,770 | 8,000–9,500 |
| Bedrooms | 3 | 4–5 | 5–6 | 6–7 |
| Bathrooms | 2–3 | 4–5 | 5–7 | 7–9 |
| Car spaces | 1 | 2 | 2–3 | 4+ |
| Structural system | Confined masonry | Hybrid / RC frame | RC frame | RC frame |
| Max clear span before beams | 14 ft | 14 ft (16 ft with beams) | 18–20 ft w/ beams | 20–24 ft w/ deep beams |
| Room-NIA / gross covered | 0.72–0.78 | 0.74–0.80 | 0.75–0.82 | 0.70–0.78 |
| Servant quarter | No | Optional | Yes | Yes (staff wing) |
| Courtyard viable | No | Marginal | Yes | **Yes — should be the organising idea** |

---

## Section 4: Room Program by House Size — Consolidated Reference

This is the typology-level program table: what rooms exist at each plot band and how many. Room *dimensions* and furniture-driven minimums are in `architecture-spatial-planning` §3.

| Space | 5 marla | 7 marla | 10 marla | 1 kanal | 2 kanal farmhouse |
|---|---|---|---|---|---|
| Drawing / guest room | 1 | 1 | 1 | 1 (+guest WC, own entry) | 1–2 (formal + informal) |
| Family lounge | 1 (small) | 1 | 1–2 (GF + FF) | 2 (GF + FF) | **2 (dual lounges, one per wing)** |
| Formal dining | shared with lounge | shared | 1 | 1 | 1 (+ outdoor dining) |
| Kitchen | 1 | 1 | 1 + pantry | 1 + dirty kitchen + pantry | 1 main + 1 dirty + prep + cold store |
| Bedrooms | 3 | 4 | 4–5 | 5–6 | **6–7, split across wings** |
| Attached baths | 2 | 3 | 4 | 5 | 7 |
| Guest WC | 1 (GF) | 1 | 1 | 1–2 | 2 |
| Store | 1 small | 1 | 1–2 | 2 | 3+ |
| Laundry / wash court | Terrace | Rear court | Rear court + FF laundry | Dedicated laundry room | Dedicated laundry + drying yard |
| Servant quarter | — | — | Optional (bsmt/rear) | 1 (with own WC + entry) | **Staff quarters block, 2–3 rooms** |
| Car | 1 open porch | 1–2 | 2 | 2–3 | **4+ covered garage** |
| Basement | Rare | Rare | Optional | Common | **Normal — theatre, gym, store, plant** |
| Courtyard / atrium | No | Light well only | Marginal | Yes | **Central organising element** |
| Prayer room | Corner of lounge | Corner | Small dedicated | Dedicated 8×8 | Dedicated 10×12 |
| Home office / study | No | No | Optional | 1 | 1–2 |
| Terrace | Over porch | Over porch | Front + rear | Multiple, setback-driven | Extensive, plus roof terrace |

**Bedroom-count reality check (T4):** clients routinely ask for one more bedroom than the plot band conventionally carries. The honest response is the trade, not a refusal: *"6 bedrooms on 10 marla is possible, but each drops to about 11×12 with a 5×7 bath, and the family lounge disappears. On 1 kanal you get 6 bedrooms at 14×15 with the lounge intact. Which matters more?"*

---

## Section 5: The Portion House — Pakistan's Real "Duplex"

This typology does not appear in Neufert, the Metric Handbook, or any Western typology reference, and it is probably the **most-built multi-unit residential form in urban Pakistan**. Getting the terminology right matters because international sources will mislead you.

### 5.1 Terminology (T4 — get this right before answering)

| Term | Pakistani meaning | Western/IRC meaning |
|---|---|---|
| **Portion** | A single plot physically and often legally split into an **upper portion** and a **lower portion**, each a complete independent dwelling (own kitchen, own bathrooms, own entrance, own meters) accessed by **separate stairs from the street** | No equivalent term |
| **Duplex** | **Two vertically stacked floors forming ONE unit**, with its own internal stair, no shared stair access, often a double-height void over the lounge | **Two dwellings side-by-side** sharing a party wall (a semi-detached pair) |
| **Maisonette** | Rarely used; the concept is covered by "duplex" | A 2-storey unit within a larger apartment building |
| **Apartment / flat** | Single-floor unit in a multi-storey block with a shared stair/lift core | Same |

**Hard rule:** if a Pakistani user says "duplex", they mean **one two-storey unit**, not two units. If they say "portion", they mean **two units stacked**. Confirm before designing — this single misreading has produced entire wrong schemes.

### 5.2 Portion house typology metrics (T4)

| Metric | Value |
|---|---|
| Viable plot band | **7 marla and above**; workable but tight on 5 marla; standard on 10 marla |
| Units | 2 (lower portion = ground floor; upper portion = first floor) |
| Access | **Two separate street entrances.** Lower: main door at grade. Upper: a dedicated external stair, usually running along the side gali or across the front setback |
| External stair footprint | **60–110 sqft** at ground level (3.5–4 ft wide × 16–20 ft run + landing) — this comes out of the setback or the covered area, and it is the typology's main cost |
| Meters | **Separate electricity, gas and water meters mandatory** for real rental independence. Budget for two SNGPL and two WAPDA/K-Electric connections. |
| Water tanks | Separate underground + overhead tanks, or a shared tank with separate pumps/meters. Shared uncontrolled tanks are the #1 source of tenant disputes. |
| Rent ratio | Upper portion typically rents at **60–75%** of lower portion (no ground access, stair climb, roof heat gain) |
| Roof rights | Upper portion normally gets exclusive roof/terrace/mumty use. **Write it down** — the most common portion-house dispute. |
| Sound separation | The intermediate RCC slab alone is inadequate. Budget a screed + insulation layer, or accept impact-noise complaints. |

### 5.3 Portion house design rules (T4)

1. **The upper stair must not pass through, overlook, or land inside the lower portion's private open space.** If the side gali is the only route, the lower portion loses that gali as private space — accept it and design the lower portion's outdoor space at the rear instead.
2. **Both kitchens should stack vertically** — one plumbing/gas riser, one exhaust route, one wet-area waterproofing detail repeated. Same for bathrooms. This is the single largest cost saving in the typology.
3. **The upper portion needs its own roof access** for water tank, dish antenna, and drying. Its mumty is not optional.
4. **Corner plots halve the difficulty.** Two street faces = two grade-level entrances, and the upper stair can rise from the secondary street without eating the primary frontage.
5. **Check the byelaw.** Some authorities and most DHA phases regulate or prohibit separate street entrances and separate utility connections on a single-family residential plot. This is a **T1 question** — route it to `architecture-building-codes-permits`.
6. **Design the upper portion's ceiling insulation seriously.** In Lahore/Karachi summer the top floor is 4–7 °C hotter without roof insulation, and that difference is exactly what suppresses the upper rent.

### 5.4 Portion on 5 marla — the tight case

On a 25 × 45 plot the external stair (say 3.5 × 18 = 63 sqft plus a 3.5 × 4 landing) consumes ~77 sqft of a ~875 sqft footprint — **9% of the lower portion, permanently.** It is done, routinely, but the honest framing is:

```
Lower portion: ~800 sqft usable → 2 bed / lounge / kitchen / 1.5 bath
Upper portion: ~875 sqft usable → 2 bed / lounge / kitchen / 2 bath (no stair loss upstairs)
Car:           1 space, shared or assigned to the lower portion
Verdict:       Works. Both units are small-family sized (not 3-bed family sized).
               If either household needs 3 bedrooms, 5 marla is the wrong plot for a portion split.
```

### 5.5 Row House / Townhouse — Gated-Scheme Product

Distinct from the traditional urban plot ladder (Sections 2–4), which assumes each plot is bought and built independently: gated master-planned schemes (Bahria Town, DHA Valley/City, Etihad Town, and similar private developments) increasingly sell **developer-built attached row houses / townhouses** as a single product — one structural party wall, one facade language, one handover date — rather than individual plots for owners to build on. This is now common enough in Pakistan to warrant its own typology entry rather than a dismissal as "no Pakistani equivalent" (see the international comparison caveat in Section 17).

#### 5.5.1 Typology metrics (T4)

| Metric | Value |
|---|---|
| Plot/unit width | 20–30 ft (narrower than a standalone 5-marla plot because party walls replace side setbacks) |
| Plot/unit depth | 45–70 ft |
| Unit footprint area (marla-equivalent) | 3.5–7 marla per unit |
| Storeys | G+1 or G+2, uniform across the row (structurally and aesthetically tied) |
| Party wall | Shared 9" masonry, structurally continuous across units within a block — a genuine common load path, unlike the informally-adjacent walls of two independently-built plots |
| Access | Every unit gets its own front door and (usually) rear service lane — no shared internal stair or corridor, unlike an apartment block |
| Parking | 1 car in an open porch, or a shared rear lane; rarely a garage |
| Facade control | Developer-controlled uniform elevation; individual owners typically cannot alter the front facade post-handover (a scheme by-law, not a structural constraint) |

#### 5.5.2 How it differs from the typologies already covered

| vs. | Difference |
|---|---|
| Detached house (Section 3) | No side setbacks between units — the party wall replaces them, so the frontage-competition problem (porch + entry + stair, Section 3.1) is worse, not better, on a narrower unit |
| Portion house (Section 5.1–5.4) | One household per unit, not two stacked — there is no upper/lower split; the "row" is horizontal, not vertical |
| Apartment block (Section 8) | Each unit has its own ground-level entrance and its own vertical circulation — no shared core, no lift, no corridor |
| Duplex pair (Section 6.2) | A duplex pair is two units on one plot, usually held together by one family; a row-house block can be 6–20+ units, each independently titled and sold to a different buyer |

#### 5.5.3 Design rules (T4)

1. **Design the end units differently from the middle units.** End-of-row units get a free side face — worth an extra window or a side entrance; middle units are single-aspect front/rear only. Do not repeat one plan blindly across the whole row.
2. **The party wall is structural, not just a boundary line.** Coordinate openings, service risers and roof drainage across the party line with the neighbouring unit's plan — this is the scheme architect's job, not left to whichever unit builds first (they are usually delivered together under one contract in any case).
3. **The rear service lane is the utility spine.** Gas, water, drainage and waste collection typically run off the rear lane in these schemes — do not plan a unit assuming front-only servicing.
4. **Repeat the structural bay, vary the finish only.** The efficient way to deliver a long row is one repeated structural/plan module (see the apartment "model one typical floor, then array" principle in Section 15.2) with cosmetic facade variation, not a genuinely different plan per unit.
5. **Byelaw check is still mandatory (T1).** Row-house schemes are usually governed by the private scheme's own by-laws (DHA Valley, Bahria Town) rather than LDA/CDA directly — confirm which authority actually governs before quoting coverage or setback numbers.

---

## Section 6: True Duplex and Maisonette

### 6.1 The Pakistani duplex (one unit, two stacked floors)

| Metric | Value (T4) |
|---|---|
| Typical plot | 1 kanal (as one of two duplex units on a plot), or a duplex unit within an apartment block |
| Unit area | 2,000–3,500 sqft across two floors |
| Access | Single private entrance; **internal stair** within the unit |
| Signature move | **Double-height void over the lounge** (17–22 ft floor-to-ceiling), with the upper-floor gallery/landing overlooking it |
| Internal stair cost | Consumes **90–140 sqft of net area per unit** (stair well counted once on each of two floors ≈ 45–70 sqft/floor) |
| Advantage | House-like quality inside a multi-unit building; dual-aspect on both levels; clean day/night zoning (living below, sleeping above) |
| Disadvantage | Stair area loss; accessibility limited to the entry level; heating/cooling the double-height void is expensive |
| Structural | The double-height void removes an intermediate slab diaphragm over that bay — **flag to the engineer**; in Zone 2B+ this is a diaphragm-discontinuity irregularity, not a free architectural gesture |

### 6.2 Kanal-plot duplex pair (two duplex units on one 1-kanal plot)

A pattern used where a family wants two independent households with parity (unlike a portion split, where upper and lower are unequal).

```
50 × 90 kanal plot, split lengthwise into two 25 × 90 halves
Each unit: G+1, own street entrance, own porch, own internal stair, own roof access
Per unit covered: ~1,500 GF + ~1,300 FF = ~2,800 sqft
Party wall: 9" masonry minimum; for real acoustic separation use a twin-leaf wall
            with a cavity, or 9" + independent 4.5" leaf with a gap
Advantage over portion: parity between the two households; both get grade access,
            garden, and porch. No "who gets the roof" dispute.
Disadvantage: each unit is now 25 ft wide — the same frontage problem as a 5-marla
            house (porch + entry + stair compete), just deeper.
```

### 6.3 Maisonette within an apartment block

Retained from general typology theory — relevant when designing a 1-kanal walk-up block with a premium top unit.

| Metric | Value |
|---|---|
| Plan depth | 26–46 ft (8–14 m) |
| Storeys per unit | 2 |
| Typical area | 700–1,300 sqft (65–120 m²) |
| Access | Corridor/landing every other floor (skip-stop) or private external stair |
| Advantage | Dual-aspect living; internal stair gives house-like quality; **reduces total corridor area in the building, raising NTG** |
| Disadvantage | Internal stair consumes 32–43 sqft (3–4 m²) net per unit; accessible only at entry level |
| Exemplars | Alexandra Road Estate (Neave Brown / Camden, 1978, London) — stepped maisonettes, 520 dwellings; Brunswick Centre (Patrick Hodgkinson, 1972, London) |

---

## Section 7: Farmhouse Typology (1–5 Kanal)

The farmhouse is not a big house. It is a **different typology** with a different organising logic: on a 2-kanal plot the land is the asset and the building is an object placed in it, whereas on a 10-marla plot the building *is* the plot. Designing a farmhouse as a scaled-up urban house is the characteristic failure — it produces a deep, dark, corridor-driven block sitting awkwardly in the middle of a large empty lawn.

**Before using any table in this section, confirm the plot is actually farmhouse-zoned — see Section 7.6.** Everything below assumes a genuine farmhouse-designated scheme/zone; a large plot inside an ordinary residential scheme is a different, more common case with a different (higher) coverage envelope.

### 7.1 Farmhouse metrics by plot (T4, farmhouse-zoned land)

| Plot | Area (sqft) | Typical total covered (sqft) | Total coverage across floors | GF coverage | Beds | Storeys |
|---|---|---|---|---|---|---|
| 1 kanal | 4,500 | 3,000–4,000 | 67–89% | 40–50% | 3–4 | G+1 |
| **2 kanal** | **9,000** | **8,000–9,500** | 89–106% | **40–55%** | **6–7** | **G+1+B** |
| 4 kanal | 18,000 | ~10,140 | 56% | ~33% | 7–9 | G+1+B |
| 5 kanal | 22,500 | 11,000–14,000 | 49–62% | ~30% | 8–10 | G+1+B |

Note the trend: **as the plot grows, GF coverage falls sharply** (55% → 30%) while covered area grows more slowly. That is the typology asserting itself — beyond ~2 kanal, more plot buys landscape, not building.

### 7.2 The 2-kanal farmhouse program (T4 — this is the Claude default)

| Zone | Content | Approx area (sqft) |
|---|---|---|
| **Arrival** | Gated entry · driveway · **4+ car covered garage** · porte-cochère · visitor parking | 900–1,400 |
| **Formal / guest wing** | Formal drawing room 24×18 · formal dining 20×16 · guest powder room · **1 guest suite with own entrance** | 1,100–1,400 |
| **Family wing** | Family lounge 22×18 · informal dining · pantry · TV/media room | 900–1,200 |
| **Sleeping (split across two wings)** | Master suite 20×18 + dress + bath 12×10 · 5–6 bedrooms 15×16 each with attached bath · upper family lounge | 2,600–3,400 |
| **Service** | Main kitchen 16×14 · **dirty kitchen 12×10** · cold store · laundry · 3+ stores | 700–900 |
| **Staff** | Staff quarters block (2–3 rooms + shared WC + own kitchenette), **separate entry, visually screened** | 400–700 |
| **Basement** | **Home theatre** · gym · games room · plant room (generator, UPS, pumps) · bulk store | 1,500–2,500 |
| **Outdoor (uncovered, not in FAR but is the point of the typology)** | Swimming pool · outdoor dining/BBQ · lawn · orchard/kitchen garden · service yard | — |

### 7.3 Farmhouse plan organisation — the four working models

| Model | Description | Best for | Watch out for |
|---|---|---|---|
| **Central courtyard / atrium** | Rooms wrap a central open court or a roofed double-height atrium; stair rises in the void | Hot-dry Punjab; large families needing acoustic separation between wings | Roofed atrium becomes a heat trap without a stack-ventilation strategy |
| **Split-wing (H or L)** | Two wings (family / guest, or adult / children) linked by a shared common core | 6–7 bedroom programs where privacy between household groups matters | The link becomes a corridor if it is not given a program (gallery, library, lounge) |
| **Pavilion / dispersed** | Discrete volumes (main house, guest house, staff block, pool house) connected by covered walkways | 4 kanal+; hot-humid Sindh; clients wanting resort character | Long service runs; expensive envelope-to-floor-area ratio |
| **Linear / view-facing bar** | One-room-deep bar oriented to a view or to the prevailing wind | Sloped or view sites; strong cross-ventilation priority | Very long circulation; poor on windowless service rooms |

### 7.4 The Farmhouse_2Kanal_Template — Claude's working reference

A validated FreeCAD model exists at `~/Documents/Farmhouse_2Kanal_Template.FCStd` (~1.2 MB). **Treat future "build a farmhouse like this" requests as starting from this file and its techniques, not from scratch.** Load `architecture-freecad-bim` before touching it.

**What the template demonstrates typologically:**

| Feature | Typological role |
|---|---|
| **7-sided (heptagon) plan** | Non-orthogonal perimeter maximises the number of rooms with two external faces on a large plot; every bedroom gets a corner |
| **Central double-height courtyard/atrium with a real staircase** | The organising void — stack ventilation, daylight to the plan core, and the vertical circulation all in one move |
| **Wind tower (badgir)** | Passive stack ventilation; draws hot air out of the atrium top. Only works when paired with low-level cool-air inlets |
| **Jaali (perforated brick screen) clerestory bands** | High-level perforated bands on hot-facing walls give Venturi-effect cross-ventilation plus filtered light without solar gain at occupant level |
| **Rooftop solar PV + water tank on a support plinth** | Farmhouse plots are usually at the edge of reliable grid/water supply — self-sufficiency is a typological requirement, not a luxury |
| **Staff quarters, 4+ car garage, basement** | The three program elements that distinguish a farmhouse from a large house |
| **29 classified `IfcWindow`/`IfcDoor` objects** | Verified by real IFC export — the model is BIM-valid, not just visually complete |

**Reusable FreeCAD techniques carried in that project (see the project memory note and `architecture-freecad-bim` for full detail):** wall openings must be cut with an explicit `Part.makeBox` boolean against `wall.Shape`, assigned to a new `Part::Feature` — `Arch.makeWindow`'s `Hosts`/`Subtractions` link does **not** auto-cut the wall in FreeCAD 1.0.1 (verified by a zero volume-difference test), though it *does* produce correct IFC classification. Jaali screens are built as a grid of small boxes cut sequentially from the wall's current shape.

### 7.5 Farmhouse-specific typology rules (T4/T5)

1. **Do not centre the building on the plot** unless the plan is a courtyard type. Push it back to create a deep arrival forecourt and a large private rear garden; a building floating in the middle leaves four unusable leftover strips.
2. **Coverage 40–55% is the design target, not the legal maximum, on genuinely farmhouse-zoned land.** Building to the maximum on a farmhouse plot destroys the typology's reason to exist.
3. **Separate the staff circulation completely.** Staff must reach kitchen, laundry, stores and guest rooms without crossing family living space. This drives a service corridor or a second stair, and it is non-negotiable at this scale.
4. **The dirty kitchen (masala/tandoor kitchen) is a required room, not an optional one,** at 1 kanal and above. Omitting it means the main kitchen becomes the dirty kitchen within a year.
5. **Spans get long fast.** A 24×18 drawing room, a double-height atrium, and a 4-car garage all exceed the conventional 14 ft slab limit — **RC frame with beams is mandatory**, and the column grid must be set before the plan is fixed, not after.
6. **Basement waterproofing is a first-order cost**, not a finish item. Budget it at concept stage. Check the water table before committing a theatre or gym to the basement (route to `architecture-geotechnical-foundations`).
7. **Utilities are the hidden program.** Generator + UPS/solar + water pump + underground tank + septic/treatment (farmhouse plots are frequently outside sewer networks) need a real plant room, typically 200–350 sqft in the basement or a detached service block.

### 7.6 A large plot that is NOT farmhouse-zoned — the more common real case

Everything in Sections 7.1–7.5 assumes the 2–5 kanal plot sits inside a **farmhouse-designated scheme or zone** (e.g. a dedicated farmhouse society, agricultural-conversion land), where coverage is deliberately capped low (30–55%) to preserve the landscape character that is the product being sold. **This is not the only — or even the most common — way a client arrives with a 2+ kanal plot.** Just as often, the plot is a large parcel inside an **ordinary residential scheme** (a 2-kanal plot in a DHA or LDA residential phase, for instance), where the applicable byelaw is the **normal kanal-plot coverage band (65–70%, Section 2.3)**, not the farmhouse band.

**This is a T1 gate, and it is the first question to ask on any plot above 1 kanal** — never default to farmhouse coverage assumptions without confirming the zoning:

| Question | If YES → | If NO → |
|---|---|---|
| Is the plot inside a scheme/zone specifically designated for farmhouses (its own land-use category, its own by-law schedule)? | Farmhouse coverage applies: 40–55% GF target (Section 7.1), courtyard/pavilion typology is the natural fit, landscape is the product | Ordinary residential coverage applies: 65–70% GF (Section 2.3) — **the client legally can build a much larger footprint than the farmhouse tables imply**, and probably expects to |

**Why this matters in practice:** a client with a 2-kanal plot inside an ordinary DHA residential phase who is shown the farmhouse-coverage tables in Section 7.1 will be quoted a building 30–40% smaller than what their byelaw actually permits — an under-design, not a safe conservative default. Conversely, treating a genuine farmhouse-zoned plot as an ordinary residential plot and designing to 65–70% coverage will very likely **fail map approval outright** if the scheme's farmhouse by-law caps it lower — an over-design that cannot be built as drawn.

**Worked comparison, 2-kanal plot (9,000 sqft), both readings:**

```
FARMHOUSE-ZONED (Section 7.1 table)          ORDINARY RESIDENTIAL ZONING
Coverage target        45%                   Coverage limit          65–70%
GF footprint            4,050 sqft            GF footprint            5,850–6,300 sqft
Typology                Courtyard/pavilion    Typology                Scaled-up detached
                        farmhouse, landscape                          house — but still apply
                        as the point                                  the "do not scale up a
                                                                       10-marla plan" warning
                                                                       from Section 7's intro;
                                                                       a large detached house on
                                                                       2 kanal still benefits from
                                                                       farmhouse-style planning
                                                                       even where the byelaw
                                                                       would allow more coverage
```

**The design recommendation, even when the higher residential coverage is legally available:** do not automatically build to 65–70% just because the byelaw permits it. The farmhouse organising logic (Section 7's opening paragraph — the land as the asset, courtyard/split-wing planning, the building as an object in the landscape) usually produces a better house on a 2+ kanal plot than maximising coverage does, **even where the client is not in a farmhouse-designated scheme**. Present both the legal envelope and the design recommendation separately, and let the client choose with the trade-off stated plainly:

> *"Your byelaw here allows up to about 6,000 sqft of ground floor — nearly 50% more than the farmhouse tables I'd normally use. You can build to that. But on a plot this size, a lower-coverage courtyard plan usually reads better and costs less to maintain than filling the plot. Which matters more to you — maximum covered area, or the farmhouse feel?"*

---

## Section 8: Apartment Block Typology

### 8.1 When apartments are the right answer in Pakistan

Apartments are the right typology when **the plot's yield matters more than the household's amenity**, and only where the byelaw permits them. Most DHA residential phases and many LDA residential schemes **prohibit** apartment buildings on single-family plots — this is a **T1 gate you must check first** (route to `architecture-building-codes-permits`).

Cultural note (T4): the Pakistani apartment market is **family-occupancy driven**. Studios and 1-bed units, which dominate Western urban blocks, are a thin market outside a few Karachi and Islamabad submarkets. **Design the mix around 2- and 3-bed family units.**

### 8.2 Apartment unit sizes in Pakistan (T4 — market data, ranges overlap; verify per developer)

| Unit type | Typical sqft | Notes |
|---|---|---|
| Studio | 350–550 | Thin market; mostly Karachi/Islamabad, expat or student submarkets |
| 1-bed | 550–800 | Rental-driven; small share of most schemes |
| **2-bed** | **800–1,200** | **The volume unit — design the block around this** |
| **3-bed** | **1,200+** (commonly 1,200–1,600) | The family unit; strongest resale |
| 4-bed | 1,200–1,600 | **Overlaps 3-bed** — Pakistani 4-bed units are compressed relative to Western norms; verify per developer rather than assuming a step up |
| Penthouse / duplex | 2,000–3,500 | Top-floor, roof terrace, often a true duplex (Section 6.1) |

**Honesty flag:** these bands come from Pakistani real-estate market sources, not code, and they compress at the top — a "4-bed" that is 1,300 sqft has four small bedrooms, not a larger unit. When a client cites a bedroom count, get the target sqft too.

### 8.3 Block configurations

**Walk-up block (G+3 / G+4)** — the standard on a 1-kanal or 2-kanal urban plot.

| Metric | Value (T4/T3) |
|---|---|
| Plot | 1 kanal (4,500 sqft) to 2 kanal |
| Floor plate (1 kanal at 70% coverage) | ~3,150 sqft gross per floor |
| Units per floor | 3 × ~900 sqft, or 2 × ~1,300 sqft |
| Core | Single stair (8×16 ≈ 128 sqft) + small lift shaft (6×7 ≈ 42 sqft) + landing (~100 sqft) ≈ **270 sqft ≈ 8.6% of plate** |
| Corridor | Minimise — target direct stair-landing access to every unit. A 4 ft × 30 ft corridor adds 120 sqft (3.8%) |
| Lift | Many byelaws exempt buildings below a threshold height/storey count — **verify (T1)**. Provide one anyway above G+2 for saleability |
| Floor-to-floor | 10'-6" to 11'-6" (3.2–3.5 m) including a 6" slab |
| Structure | **RC frame + shear walls at the core**; masonry infill |
| Parking | Ground-level stilt/open parking is the Pakistani norm; 0.5–1.0 spaces/unit. Basement parking is expensive below ~4 storeys |
| NTG (building NIA / GIA) | **0.72–0.78** |

**Mid-rise block (5–12 storeys)** — a consolidated multi-plot or commercial-zoned site.

| Metric | Value |
|---|---|
| Plan depth | 40–60 ft (12–18 m) double-loaded corridor |
| Floor plate | 6,500–16,000 sqft (600–1,500 m²) gross |
| Core | 1–2 lifts + firefighting stair + escape stair (code-dependent) |
| Units per core per floor | 4–10 |
| Structural grid | ~20 × 25 ft (6.0 × 7.5 m) residential |
| Floor-to-floor | 9'-4" to 10'-4" (2.85–3.15 m) |
| **Corridor length from core** | **≤ 100 ft (30 m)** for fire egress (T3, IBC/UK practice — confirm against BCP 2021 and the local fire authority) |
| NTG | 0.70–0.78 |
| Dual-aspect rule | Minimum 2 dual-aspect units per floor (the corners); avoid north-only single-aspect units |

**High-rise residential tower (13+ storeys)** — Karachi/Lahore/Islamabad towers; rare in Claude's actual workload but retained for completeness.

| Metric | Point tower | Slab tower |
|---|---|---|
| Plan depth / diameter | 60–80 ft (18–24 m) | 40–52 ft (12–16 m) depth |
| Floor plate (gross) | 4,300–9,700 sqft | 8,600–21,500 sqft |
| Core area | 860–1,600 sqft (80–150 m²) | — |
| Core-to-GIA ratio | 20–28% | 15–22% |
| Units per core per floor | 4–8 | 8–16 |
| NTG | 0.68–0.78 | 0.72–0.82 |
| Lifts | 2 per 80–120 units minimum, + 1 firefighting lift | |
| Floor-to-floor | 9'-10" to 10'-10" (3.0–3.3 m) standard; 11'-6" to 13'-1" (3.5–4.0 m) luxury | |
| Structure | RC core + flat slab / post-tensioned slab | |
| Wind | Wind analysis required above 10 storeys; corner balconies problematic above 15 | |

**Core configurations (T3, retained general theory):**
- **Stair access, no corridor** — single stair, 2–4 units per landing. Most efficient, best dual-aspect potential. This is the right model for Pakistani walk-up blocks.
- **Single-loaded corridor** — all units face one direction. Good daylight, NTG drops to 0.72–0.78.
- **Double-loaded corridor** — most area-efficient, but single-aspect units both sides. Plan depth 40–50 ft.
- **Scissor stair** — two interleaving stairs in one shaft; compact two-stair egress, used to ~30 storeys in UK practice.
- **Skip-stop** — corridor every 3rd floor with maisonettes between; cuts corridor area and raises NTG (the Unité d'Habitation model).

### 8.4 Worked floor-plate check — walk-up block on 1 kanal

```
Plot                  4,500 sqft (50 × 90)
Coverage @ 70%        3,150 sqft gross floor plate
LESS core             stair 128 + lift 42 + landing 100      = 270  (8.6%)
LESS external walls   perimeter ~180 ft × 0.75 ft            = 135  (4.3%)
                      (9" external wall)
LESS corridor         4 ft × 24 ft                           =  96  (3.0%)
= Net available for units                                    2,649 sqft (84.1% of plate)

Split 3 ways:         883 sqft gross per unit
LESS internal walls   ~10% of unit gross                      ≈ 88
= Unit net internal   ≈ 795 sqft  →  a genuine 2-bed unit (bottom of the 800–1,200 band)

Building over G+3:    4 floors × 3 units = 12 units
Building NIA / GIA    (795 × 12) / (3,150 × 4) = 9,540 / 12,600 = 0.757  → 76% NTG ✓
                      (consistent with the 70–78% apartment band)
Parking needed        12 units × 0.5–1.0 = 6–12 spaces
Ground stilt parking  3,150 sqft at ~150 sqft/space incl. aisle ≈ 21 spaces → ✓ ample
                      BUT stilt parking means the ground floor is not units → recheck
                      unit count as 3 floors × 3 = 9 units if G is fully parking.
```
**The lesson that check teaches:** on a 1-kanal plot, ground-floor stilt parking costs you a third of the units in a G+3 block. Either go G+4 (check height limit, T1), put parking in the setbacks and open court, or accept 9 units.

---

## Section 9: Unit Mix and Bedroom Program

### 9.1 Apartment unit mix by market segment (T4, Pakistan)

| Segment | Studio | 1-bed | 2-bed | 3-bed | 4-bed / penthouse |
|---|---|---|---|---|---|
| Affordable / mass housing | 0% | 10–15% | **55–65%** | 20–30% | 0% |
| Mid-income urban (typical) | 0–5% | 10–20% | **40–50%** | **30–40%** | 0–5% |
| Premium / DHA-adjacent | 0% | 5–10% | 30–35% | **40–45%** | 10–20% |
| Karachi expat / serviced | 10–15% | 25–30% | 35–40% | 15–20% | 0–5% |
| *(Western urban comparison, T3)* | *5–15%* | *30–40%* | *35–45%* | *15–25%* | *0–5%* |

**The structural difference from Western practice:** the Western mix peaks at 1-bed; the Pakistani mix peaks at 2-bed and carries a much heavier 3-bed tail. Designing a Pakistani block on a Western mix leaves unsellable small units and a shortage of the units the market wants.

### 9.2 Bedroom count by plot band — what the market expects (T4)

| Plot | Market-expected bedrooms | Stretch (with trade-offs) | Below this = hard to sell |
|---|---|---|---|
| 3 marla | 2–3 | 4 (all ~10×11, no lounge) | 2 |
| 5 marla | **3** | 4 (drops lounge to nominal) | 2 |
| 7 marla | **4** | 5 | 3 |
| 10 marla | **4–5** | 6 (all ~11×12, no family lounge) | 4 |
| 1 kanal | **5–6** | 7 | 4 |
| 2 kanal | **6–7** | 8 | 5 |

### 9.3 The bathroom rule (T4)

Pakistani market expectation has moved decisively to **attached baths**. The rule of thumb:

```
Bathroom count ≈ bedroom count (attached)
                + 1 guest WC on the ground floor
                + 1 staff WC where there is a servant quarter
```
A 5-bedroom 1-kanal house therefore needs **5 attached + 1 guest + 1 staff = 7**. Shared/common bathrooms are acceptable only for children's bedrooms in mid-market work and are a resale drag above 10 marla.

---

## Section 10: Net-to-Gross Efficiency at House Scale

### 10.1 Definitions (state which one you are using — they differ by 10–15 points)

| Term | Definition |
|---|---|
| **Gross Covered Area (GCA)** | Footprint measured to the outside face of external walls, × number of floors, + mumty. This is what byelaws and contractors count. |
| **Gross Internal Area (GIA)** | Inside face of external walls; includes internal partitions, stair, passages. |
| **Net Internal Area (NIA) — rooms only** | Sum of clear floor areas of named rooms (bedrooms, lounge, kitchen, baths). **Excludes** stair, passages, foyer. The strictest definition. |
| **Net Usable Area (NUA)** | NIA + circulation that is genuinely inhabited (an open-plan lounge that doubles as the route between rooms). The most honest measure for Pakistani houses. |

**Always say which you mean.** A house that is "78% efficient" on NUA is "70% efficient" on NIA and the client will feel cheated if you switch definitions mid-conversation.

### 10.2 Where the area goes — worked breakdown (5 marla ground floor)

```
Footprint (external face)      25 × 38.25              = 956 sqft   (GCA, this floor)
LESS external walls @ 9"       internal env. 23.5 × 36.75 = 864 sqft
                               loss = 92 sqft            (9.6% of GCA)
LESS internal partitions       ~90 lin ft @ 4.5" (0.375 ft) = 34 sqft (3.5%)
= GIA net of walls                                        830 sqft   (86.8% of GCA)
LESS stair well                8 × 14                     = 112 sqft (11.7%)
LESS passage + foyer                                      ≈  70 sqft ( 7.3%)
= NIA (rooms only)                                          648 sqft (67.8% of GCA)
= NUA (counting an open lounge-as-circulation, +55)         703 sqft (73.5% of GCA)
```

### 10.3 House-scale efficiency targets (T4, derived — see the honesty flag in 10.5)

| Typology | Wall loss | Vertical circ. | Horizontal circ. | **NIA / GCA** | **NUA / GCA** |
|---|---|---|---|---|---|
| 5 marla detached G+1 | 12–14% | 6–8% | 5–8% | **0.68–0.75** | 0.73–0.80 |
| 10 marla detached G+1 | 11–13% | 5–7% | 5–9% | **0.70–0.78** | 0.76–0.83 |
| 1 kanal detached | 10–13% | 5–7% | 6–10% | **0.70–0.78** | 0.77–0.84 |
| 2 kanal farmhouse | 10–12% | 4–6% | 8–14% | **0.66–0.75** | 0.72–0.81 |
| Portion house (per portion) | 12–15% | 3–5% (external stair) | 5–8% | 0.72–0.79 | 0.78–0.85 |
| Duplex unit | 11–13% | 7–10% (internal stair) | 4–7% | 0.68–0.75 | 0.75–0.82 |
| Walk-up apartment block | 12–15% | 6–9% (core) | 3–6% (corridor) | **0.70–0.78** (building) | — |

**Diagnostic use:** if a house plan comes out below **0.65 NIA/GCA**, something is structurally wrong with the plan — usually a corridor doing no work, a stair placed in the middle of the footprint instead of against a wall, or a light well too small to justify its area. Above **0.82 NIA/GCA**, check that the passages are actually wide enough to use (spatial-planning §4.1) — over-efficiency in Pakistani houses usually means 2'-6" passages nobody can carry furniture through.

### 10.4 Benchmark comparison (T3/T4)

| Building type | Net-to-gross efficiency | Source class |
|---|---|---|
| Commercial / office | **78–85%** (office GFA commonly ~22% larger than net) | Industry standard, well-documented |
| Residential apartment tower | **70–75%** historically; some newer designs reach **82%+** | Industry sources |
| Pakistani walk-up block | 70–78% | Derived (Section 8.4) |
| Pakistani detached house (NIA) | 68–78% | **Derived here — see 10.5** |
| Hospital | 55–65% | Industry standard (least efficient common type) |
| Theatre / performing arts | 45–55% | Industry standard (the least efficient building type) |

### 10.5 Honesty flag — the house-scale NTG data gap

**There is no codified or industry-standard net-to-gross ratio for single-family houses.** Office and apartment-tower efficiency figures are well-documented because they are commercial leasing metrics — someone is paid per net square foot, so someone measures it. Nobody leases a house by the net square foot, so the number was never standardised.

The house figures in 10.3 are **derived from first principles** (wall thickness × perimeter, stair and passage areas from typical Pakistani plans) and cross-checked against the apartment benchmark, **not read from a standard**. When quoting them:

> *"There's no published net-to-gross standard for single-family houses — that metric only got standardised for commercial leasing. This 0.72 is derived from the wall thicknesses and circulation in this specific plan, so treat it as a design diagnostic for comparing options, not as an industry benchmark you can cite."*

Do **not** present these as authoritative ratios. Do use them to compare two of your own plan options against each other — for that purpose they are exactly right.

---

## Section 11: Structural Typology Selection

Typology and structure are not separable in Pakistani residential work: the plot band effectively selects the structural system, and the structural system caps the spans, which caps the room sizes, which caps the program.

### 11.1 Selection decision tree

```
Storeys and spans known?
  ├─ G or G+1, all clear spans ≤ 14 ft, Seismic Zone ≤ 2A
  │     → CONFINED MASONRY (9" burnt-brick load-bearing walls with RC confining
  │       columns at corners/junctions/openings + tie beams at plinth and lintel level)
  │       ~8–12% cheaper than RC frame. Standard for 3/5/7 marla.
  │
  ├─ G+1 in Seismic Zone 2B or above
  │     → CONFINED MASONRY still viable, but UNREINFORCED masonry is NOT permitted
  │       in Zone 2B+ (see architecture-seismic-design). Confining elements are
  │       mandatory, not optional. If the mason cannot execute them, go RC frame.
  │
  ├─ G+2 or more, OR any clear span > 16 ft, OR a double-height void,
  │  OR Zone 3–4 above one storey
  │     → RC FRAME (columns + beams + slab), masonry infill, mandatory for that
  │       bay at minimum — a single long-span room inside an otherwise confined-
  │       masonry house still needs its own beam-and-column bay (see the worked
  │       reconciliation in Sections 3.3 and 14.2), not a slab-only workaround.
  │       Full RC frame is mandatory for: 1 kanal premium, all farmhouses, all
  │       apartment blocks
  │
  └─ 5+ storeys, or a tower
        → RC FRAME + SHEAR WALLS at the core, or full shear-wall system
          Route to architecture-structural-systems and architecture-seismic-design
```

### 11.2 Wall thicknesses (T5 / T4)

| Element | Thickness | Notes |
|---|---|---|
| **External load-bearing wall** | **9 inches** (single-wythe burnt brick) | The Pakistani standard, documented in World Housing Encyclopedia Report 173 "Brick Masonry Construction in Pakistan" (T5). Also gives thermal mass. |
| **Internal partition** | **4.5 inches** | **Non-load-bearing only.** Must be tied to the structure at top and to columns at ends. |
| Party wall (portion / duplex pair / row house) | 9" minimum; twin-leaf with cavity for real acoustic separation | The slab alone will not stop impact noise |
| Boundary wall | 9" with piers at 8–10 ft centres | T1 height limits per byelaw |
| Standard brick ("Awwal" / first class) | **9 × 4.5 × 3 inches** | 4 courses + mortar ≈ 13.5"; useful for setting out |

**Slenderness check for the 4.5" partition:** at a 10 ft (120 in) storey height, h/t = 120/4.5 = **26.7** — at or past the practical limit for an unrestrained masonry panel. A 4.5" wall over 10 ft **must** be restrained at the top (tied to the slab soffit) and at both ends (to columns or 9" walls). Never let a 4.5" wall carry load or stand free.

### 11.3 Slab thickness by span — correcting the practitioner rule against ACI 318-19

**The practitioner convention (T4):** RCC slab **5–6 inches**, ½-inch (12 mm) bars at 6-inch centres both ways. This is a blog-and-site-practice rule, **not a code citation**.

**Checked against ACI 318-19 Table 7.3.1.1** (minimum thickness of non-prestressed one-way slabs for deflection control, normalweight concrete, Grade 60 steel, not supporting partitions likely to be damaged by large deflections):

| Support condition | Minimum h | Max span at h = 5" (127 mm) | Max span at h = 6" (152 mm) |
|---|---|---|---|
| Simply supported | ℓ/20 | 8.3 ft | 10.0 ft |
| One end continuous | ℓ/24 | 10.0 ft | 12.0 ft |
| **Both ends continuous** | **ℓ/28** | **11.7 ft** | **14.0 ft** |
| Cantilever | ℓ/10 | 4.2 ft | 5.0 ft |

**The finding that matters typologically:**

> The "5–6 inch slab" rule works precisely because typical Pakistani room spans are **11–14 ft**. It is not a universal rule — it is a rule calibrated to the conventional room size. **Any room the client asks to make bigger than ~14 ft clear span breaks it.**

| Requested clear span | Required h (both ends continuous, ℓ/28) | Verdict |
|---|---|---|
| 12 ft | 5.1" | 5–6" slab ✓ |
| 14 ft | 6.0" | 6" slab ✓ (at the limit) |
| 16 ft | 6.9" | 7" slab, or introduce a beam |
| 18 ft | 7.7" | 8" slab, or beam grid |
| **20 ft** (farmhouse lounge) | **8.6"** | **Deep beams / RC frame required** |
| **24 ft** (the 10-marla "20×24 living room") | **10.3"** | **Beam grid mandatory — do not promise this as a flat slab** |

**Also note:** ACI 318-19 §8.3.1.1 sets a minimum of **5 in (127 mm)** for two-way slabs *without* drop panels regardless of span, so 5" is a floor, not a design.

**Mandatory caveats when quoting these:**
- These are **deflection-control minimums only**. They say nothing about flexural or shear capacity, which the engineer must design for the actual loads.
- ACI 318-19 is a **T3** reference. BCP 2021 adopts ACI/ASCE provisions by reference, but **the PEC-registered engineer's design governs**, not this table.
- **Loads** (dead + live + Pakistani-typical 4–6" earth/mud roof insulation layers, which are heavy) must come from ASCE 7-22 / BCP, not assumed.

### 11.4 Seismic overlay by typology (T1 — route to `architecture-seismic-design`)

**Building Code of Pakistan — Seismic Provisions 2007 (BCP-SP-2007)** is Pakistan's first nationwide seismic code, issued after the 2005 Kashmir earthquake, developed by the Pakistan Engineering Council with NESPAK/ICC/ACI input. It uses the **Equivalent Lateral Force (ELF)** method and — the point that matters most for residential work — **emphasises ductile detailing of RC members over pure strength design.**

| Typology | Seismic consequence |
|---|---|
| 5/7 marla confined masonry G+1 | Confining columns and tie beams are the seismic system. Skipping them (common on site) is the failure mode that killed people in 2005. Plinth beam mandatory in Zone 2B+. |
| 10 marla / 1 kanal with a big open living room | Long spans + few walls = a soft, torsionally irregular ground storey. Flag the irregularity explicitly. |
| **Farmhouse with a double-height atrium** | The void is a **diaphragm discontinuity** — the slab that would tie the structure together at that level is absent over that bay. This must be designed for, not assumed away. |
| Portion house with an external stair | The stair is often built as an appendage without proper tying — it can hammer against the main structure. Either tie it structurally or separate it with a proper seismic joint. |
| Apartment block | Shear walls at the core; regular plan; avoid a stilt-parking ground floor without adequate lateral stiffness (the classic soft-storey collapse). |
| Corner windows | **T4/T5 — avoid at corners in Zone 2B+ as good seismic-detailing practice**; corners are where masonry resists lateral load and a window there weakens it. This is professional-judgment guidance carried in this skill, **not a page-verified BCP clause** — do not cite a specific BCP section number for it; the engineer should confirm the treatment for the actual project. |

**Citation discipline:** BCP-SP-2007 section numbers were **not page-verified** in the research behind this skill. Do not quote a specific BCP section number as authoritative. Say *"BCP-SP-2007 governs this — the engineer should cite the clause"* rather than inventing one. The PDF is available via urbanunit.gov.pk; fetch and verify before citing sections. **This applies to every row in the table above, including the corner-window guidance** — treat it as engineering good practice carried in this skill, not a verified clause citation, until checked against the primary text.

### 11.5 Building envelope dimensions in Pakistani residential practice (T5)

World Housing Encyclopedia Report 173 documents typical Pakistani brick-masonry residential horizontal envelope dimensions at roughly **30 × 60 ft up to 60 × 90 ft rectangular footprints**. Read typologically:

- **30 × 60 ft** ≈ the 8–10 marla footprint — the lower bound of the documented range and the modal Pakistani house.
- **60 × 90 ft** ≈ a 1-kanal-plus footprint — the upper bound at which unreinforced/confined brick masonry is still the documented practice.
- **Beyond 60 × 90 ft** (i.e. most farmhouses), you are outside the documented masonry envelope. That is another independent reason farmhouses go to RC frame.

---

## Section 12: Floor-to-Floor and Dimensional Standards

### 12.1 Heights (T4 Pakistani practice, with T3 floor)

| Space | Pakistani clear height (T4) | Floor-to-floor (incl. 6" slab) | IRC 2021 minimum (T3 — US, not Pakistan-binding) |
|---|---|---|---|
| Habitable room, standard house | 10'-0" to 11'-0" | 10'-6" to 11'-6" | **7'-0"** (R305) |
| Drawing room, premium | 11'-0" to 12'-0" | 11'-6" to 12'-6" | 7'-0" |
| Farmhouse main spaces | 12'-0" to 14'-0" | 12'-6" to 14'-6" | 7'-0" |
| Double-height atrium/void | 18'-0" to 22'-0" | — | — |
| Bathroom / laundry | 9'-0" to 10'-0" | — | **6'-8"** |
| Basement | 9'-0" to 10'-6" | 9'-6" to 11'-0" | 7'-0" (habitable) |
| Apartment unit | 9'-4" to 10'-4" | 10'-0" to 11'-0" | 7'-0" |
| Garage / car porch | 8'-6" to 10'-0" | — | — |

**The gap is enormous and it is the point:** IRC's 7'-0" minimum is roughly 3 feet below Pakistani built practice. Pakistani houses are built tall for thermal reasons (hot air stratifies above head height) and for cultural expectation. **Never propose an IRC-minimum ceiling in Pakistan** — use IRC only as an absolute floor for sanity-checking an odd condition (a basement, a mezzanine, under a stair).

### 12.2 Circulation and egress dimensions (T3 IRC 2021 as a rigor benchmark, T4 as the design target)

| Element | IRC 2021 minimum (T3) | Pakistani design target (T4) |
|---|---|---|
| Stairway clear width | **3'-0" (36")** above handrail height (R311.7) | 3'-6" to 4'-0" main stair; 3'-0" service stair |
| Stairway headroom | **6'-8"** measured from the nosing | 7'-0" minimum; check the mumty landing |
| Egress door height | **6'-8" (80 in)** (R311.2) | 7'-0" standard door leaf |
| Main entrance door | — | 3'-6" to 4'-0" wide × 7'-0"–8'-0" |
| Passage / corridor | — | 3'-6" minimum, 4'-0" preferred |
| Bedroom escape opening | **Every sleeping room requires an emergency escape/rescue opening** (R310) | **Not enforced in Pakistan, but design to it anyway** — every bedroom should have an openable window to open air. In a deep-plan house this is a real design driver. |

**Label these correctly:** IRC 2021 is a **US code, not adopted in Pakistan**. Use it as a rigor benchmark and say so. The egress-window rule (R310) is the one worth importing on merit regardless of legal status — a windowless internal bedroom is a fire trap and is also unsellable.

→ Full stair geometry, riser/tread calculation and Pakistani-specific worked examples: `architecture-spatial-planning` §5.

### 12.3 Car and parking dimensions (T4)

| Element | Dimension |
|---|---|
| **Car porch, minimum** | **10 × 14 ft** (140 sqft) |
| Car porch, comfortable | 12 × 18 ft |
| 2-car porch | 18 × 18 ft to 20 × 20 ft |
| Garage bay (enclosed) | 10 × 20 ft per car |
| Farmhouse 4-car garage | 40 × 22 ft, or 2 × (20 × 22) |
| Driveway width | 10 ft minimum; 12 ft for a farmhouse approach |
| Apartment stilt parking | ~150 sqft/space including aisle |
| Turning circle (compact car) | 18 ft radius; farmhouse forecourt should allow a car to turn without reversing to the gate |

---

## Section 13: Cost by Typology (2026 PKR)

### 13.1 Base rates (T4 — 2026 market bands, multiple consistent sources)

| Scope | PKR per sqft of covered area |
|---|---|
| **Grey structure** (foundation, structure, walls, slab, plaster, no finishes) | **2,650 – 3,600** |
| **Turn-key / finished** (grey + electrical, plumbing, flooring, doors/windows, kitchen, baths, paint) | **5,800 – 8,800** |
| Finishes-only share (implied) | ~3,150 – 5,200 |

Variation within the bands is driven by city (Karachi and Islamabad above Lahore; Lahore above secondary cities), date within 2026 (cement and steel move), and finish grade.

### 13.2 Cost by typology (derived — round to 2 significant figures when quoting)

| Typology | Covered (sqft) | Grey @ 3,100 | Turn-key @ 7,000 | Turn-key premium @ 8,800 |
|---|---|---|---|---|
| 5 marla G+1 | 1,900 | **PKR 5.9 M** | **PKR 13.3 M** | 16.7 M |
| 7 marla G+1 | 2,600 | 8.1 M | 18.2 M | 22.9 M |
| 10 marla G+1 | 3,600 | **11.2 M** | **25.2 M** | 31.7 M |
| 10 marla G+1+basement | 5,250 | 16.3 M | 36.8 M | 46.2 M |
| 1 kanal G+1 | 4,710 | **14.6 M** | **33.0 M** | 41.4 M |
| 1 kanal maximised | 5,770 | 17.9 M | 40.4 M | 50.8 M |
| **2 kanal farmhouse** | **9,000** | **27.9 M** | **63.0 M** | **79.2 M** |
| 4 kanal farmhouse | 10,140 | 31.4 M | 71.0 M | 89.2 M |
| Walk-up block, 1 kanal G+3 | 12,600 | 39.1 M | 88.2 M | 110.9 M |

### 13.3 Typology-driven cost modifiers (apply on top of the base rate)

| Feature | Modifier | Why |
|---|---|---|
| Basement | **+15 to +30%** on that floor's area | Excavation, retaining, waterproofing, dewatering, ramp/stair |
| Double-height atrium | +10 to +20% on the affected bay | Lost floor area still costs envelope; long-span structure; high-level access for finishing |
| RC frame instead of confined masonry | **+8 to +12%** on grey | Formwork, steel, skilled labour |
| Spans > 16 ft | +5 to +15% on the structural package | Beams, thicker slabs, more steel |
| External stair for a portion house | ~PKR 250,000 – 500,000 | Plus the permanent loss of ~80–110 sqft of ground area |
| Second (service) stair | Full covered-area cost × 2 floors | ~120 sqft/floor at the applicable rate |
| Jaali / perforated screen walls | +30 to +60% on that wall area | Skilled masonry, slow, high wastage |
| Wind tower (badgir) | PKR 400,000 – 1,200,000 | Bespoke structure above roof level |
| Solar PV + battery (farmhouse standard) | PKR 1.5 M – 4 M | Sized to load; farmhouses need it, urban houses often do not |
| Boundary wall + gate (2 kanal) | PKR 2.5 M – 6 M | ~380 lin ft of 9" wall with piers, plus a gate |
| Landscaping/pool (2 kanal farmhouse) | PKR 3 M – 12 M | **Frequently omitted from the client's budget and then discovered late** |

### 13.4 The cost conversation rule

When a client gives a budget, **convert it to covered area before discussing typology**, not after:

```
Budget PKR 20 M, turn-key, standard finish (@ 7,000/sqft)
→ 20,000,000 / 7,000 = 2,857 sqft of finished covered area
→ That is a 7-marla G+1, or a 10-marla house built to ~80% of its plot potential,
  or a 10-marla grey structure now + finish in phases.
→ It is NOT a 1-kanal house and it is NOT a farmhouse. Say so in the first reply.
```
Always state the rate and the date: *"at 2026 rates of roughly PKR 7,000/sqft turn-key — verify against current quotes, cement and steel move."*

→ Element-level quantities and BOQ: `architecture-cost-estimation-boq`.

---

## Section 14: Worked Examples

### 14.1 "5 marla in Lahore, family of 5, budget PKR 15 M"

```
1. Plot        5 marla LDA scheme = 1,125 sqft (25 × 45 ft). Confirm in feet ✓
2. Envelope    Front 5, rear 5 setback → 25 × 35 = 875 sqft/floor (78% coverage)
               (85% coverage if the byelaw allows → 956 sqft; confirm with LDA — T1)
3. Typology    Detached compact house, G+1. Single storey is not an option.
4. Budget      15 M / 7,000 = 2,143 sqft of finished area.
               G+1 at 875 = 1,750 + mumty 120 = 1,870 sqft  →  BUDGET FITS with ~270 sqft
               of headroom → spend it on finish grade, not more area.
5. Program     GF: porch (in setback) · drawing 12×12 · lounge 14×12 · kitchen 11×9 ·
                   guest WC · stair 8×14
               FF: 3 bedrooms (master 13×13 + bath; two at 11×12 + shared or attached
                   baths) · small family landing
               Mumty: stair head + tank + drying terrace
6. Structure   Confined masonry, 9" external / 4.5" internal, 5–6" slab.
               All spans ≤ 14 ft ✓ — check the 14×12 lounge: 14 ft span at ℓ/28 needs
               6.0" slab. Specify 6", not 5".
7. Efficiency  NIA/GCA target 0.70–0.75. If the plan lands below 0.68, the stair or
               passage is misplaced.
8. Flag        Zone 2A (Lahore, per standard BCP-SP-2007-based zoning maps —
               Islamabad/Rawalpindi/Peshawar are the typical Zone 2B examples; verify
               the current zoning map before citing a zone as fact). Confining columns
               and a plinth beam remain required design practice at this scale
               regardless of the exact zone boundary; unreinforced masonry is never
               acceptable. Treat corner windows as something to avoid at this scale as
               good practice (Section 11.4) rather than citing a specific clause.
9. Say         "This is a planning study. PEC-stamped structural drawings and LDA
                map approval are required before construction."
```

### 14.2 "10 marla, client wants 6 bedrooms and a 20×24 living room"

```
Ask nothing — do the arithmetic first, then present the trade.

Plot 2,250 sqft. Buildable ~1,650/floor (with the 5 ft side gali).
G+1 = 3,300 sqft.

6 bedrooms at market-expected 12×14 (168) + attached bath (56)  = 224 each
                                                      × 6       = 1,344 sqft
Living 20×24                                                    =   480
Dining 12×14                                                    =   168
Kitchen 12×14 + pantry                                          =   200
Drawing 14×12                                                   =   168
Guest WC + stair + passages + wall loss (≈ 25% of gross)        =   825
                                                       TOTAL    = 3,185 sqft  → fits 3,300 ✓

BUT: the 20 × 24 living room needs a 24 ft clear span.
  ACI 318-19 Table 7.3.1.1, both ends continuous: h ≥ 24 ft / 28 = 10.3 inches.
  → A flat 5–6" slab CANNOT do this. Per the Section 11.1 decision tree, any clear
    span over 16 ft already crosses out of pure confined masonry — this room forces
    at least a hybrid RC beam-and-column bay, not a slab-only fix.
  → Options: (a) beam grid subdividing to 12 ft bays — visible downstand beams,
                 confined masonry elsewhere, RC frame bay here (hybrid, matches the
                 Section 3.5 "Hybrid / RC frame" 10-marla structural system)
             (b) full RC frame with a deep transfer beam at the perimeter — highest
                 cost, most flexibility if more open spans are wanted elsewhere too
             (c) reduce to 18 × 20 → 20 ft span → 8.6" slab — still over the 16 ft
                 threshold, still needs the hybrid beam-and-column bay from (a)
             (d) reduce to 16 × 20 → 16 ft span — sits exactly at the Section 11.1
                 threshold; still needs one intermediate RC beam on its own columns,
                 not a masonry-only fix, but it is the smallest such intervention

Present it as: "Six bedrooms fits. The 20×24 living room does not fit a normal
slab or pure confined masonry — every option needs at least one RC beam on columns
in that bay, visible in the room. Cheapest and least disruptive is (d). Which do
you want?"

Also flag: 6 bedrooms + a 480 sqft living room on 10 marla means the FAMILY LOUNGE
is gone. Confirm they want a formal living room rather than a family lounge.
```

### 14.3 "2 kanal farmhouse, weekend house, family of 8"

```
1. Plot        9,000 sqft. Confirm the plot is genuinely inside a farmhouse-
               designated scheme/zone, not just a large plot in an ordinary
               residential scheme (Section 7.6 — T1 gate, check this FIRST).
               This example assumes it IS farmhouse-zoned, so the lower coverage
               band below applies; if it is not, redo the coverage math at 65–70%
               per Section 7.6 and re-open the "how much footprint" conversation.
2. Coverage    Target 45% GF = 4,050 sqft footprint. G+1 + basement:
                 GF     4,050
                 FF     2,900 (set back for terraces)
                 Bsmt   2,000
                 TOTAL  8,950 sqft → in the 8,000–9,500 band ✓
3. Typology    FARMHOUSE — central courtyard/atrium or split-wing. NOT a scaled-up house.
4. Program     GF:   arrival + porte-cochère · 4-car garage · formal drawing 24×18 ·
                     formal dining 20×16 · family lounge 22×18 · main kitchen 16×14 +
                     dirty kitchen 12×10 · guest suite w/ own entry · 2 WCs · prayer room
               FF:   master suite 20×18 + dress + bath · 5 bedrooms 15×16 w/ attached
                     baths · upper family lounge · terraces
               Bsmt: home theatre · gym · plant room (generator/UPS/pumps) · bulk store
               Detached: staff quarters (2 rooms + WC + kitchenette), screened, own entry
5. Organising  Central double-height atrium with the main stair in the void; wind tower
   idea        over the atrium; jaali clerestory bands on the west and south walls.
               → This is the Farmhouse_2Kanal_Template pattern. Start from that file.
6. Structure   RC FRAME MANDATORY. Reasons, all independently sufficient:
                 - 24 ft and 22 ft spans exceed the masonry/flat-slab envelope
                 - the double-height atrium is a diaphragm discontinuity
                 - the footprint (>60 × 90 ft) is outside the documented Pakistani
                   brick-masonry envelope (WHE Report 173)
               Set the column grid BEFORE fixing the plan.
7. Cost        8,950 sqft. Grey @ 3,100 = PKR 27.7 M. Turn-key @ 8,800 (premium
               finish is the norm at this scale) = PKR 78.8 M.
               PLUS basement modifier +25% on 2,000 sqft   ≈ + 4.4 M
               PLUS boundary wall + gate                    ≈ + 4.0 M
               PLUS solar + water infrastructure            ≈ + 3.0 M
               PLUS landscaping + pool                      ≈ + 8.0 M
               REALISTIC ALL-IN ≈ PKR 98 M  (not the 79 M the base rate implies)
               → Tell the client the all-in number, not the base rate number.
8. Say         "Planning study. PEC-stamped structural design and authority approval
                required. The RC frame in particular is not something to shortcut —
                the atrium void and the long spans are exactly where an unstamped
                design fails."
```

### 14.4 "1 kanal — should I build a house or an apartment block?"

```
Gate first:    Does the byelaw permit apartments on this plot? Most DHA residential
               phases DO NOT. If prohibited → the question is closed; offer the
               portion-house, duplex-pair, or row-house alternative instead.
               (T1 → codes-permits)

If permitted, the comparison:

                          House (G+1)          Walk-up block (G+3, stilt parking)
Coverage                  65–70%               70%
Covered area              4,710 sqft           12,600 sqft gross (4 floors)
Sellable/lettable         1 unit               9 units × ~795 sqft net
                                               (ground floor lost to parking)
Turn-key cost @7,000      PKR 33.0 M           PKR 88.2 M
Structure                 RC frame             RC frame + core shear walls
NTG                       0.75 NIA             0.76 building
Occupancy                 One family, 5–6 bed  9 households, 2-bed each
Exit                      Single buyer,        9 separate sales or a rent roll;
                          slower, higher ticket smaller tickets, faster
Risk                      Low complexity       Byelaw risk, lift/fire compliance,
                                               parking shortfall, management burden

Say: "If the byelaw allows it and you want yield, the block. If you want a family
home or a clean single-buyer exit, the house. What is the actual goal — living in
it, renting it, or selling it?"
```

---

## Section 15: FreeCAD Modelling Integration by Typology

Load `architecture-freecad-bim` **before** writing any wall/window/door code. This section is the typology-specific overlay on top of it.

### 15.1 Model hierarchy per typology

| Typology | Site | Building | Storeys | Notes |
|---|---|---|---|---|
| Detached house | 1 Site (plot boundary + setback lines as Draft wires) | 1 Building | Ground, First, Mumty | Model the setback lines first — they are the design constraint, and having them visible prevents the classic overshoot |
| Portion house | 1 Site | 1 Building | Ground, First, Mumty | Model the **external stair as its own Storey-spanning group** so it can be shown/hidden — it is the typology's defining and most-negotiated element |
| Row house / townhouse | 1 Site | 1 Building per unit, or 1 Building with N named unit groups | Per unit | Model one typical unit properly, then array along the party-wall axis — same principle as the apartment typical floor (Section 15.2) |
| Duplex pair | 1 Site | **2 Buildings** (or 1 Building, 2 named groups) | Per unit | Keeping them as separate Buildings makes the party wall explicit |
| Farmhouse | 1 Site (large — model the landscape extents) | 1 main Building **+ 1 staff-quarters Building** | Basement, Ground, First, Roof | The detached staff block is a real second Building, not a group |
| Apartment block | 1 Site | 1 Building | Stilt/Parking, Typical ×N, Roof | Model **one** typical floor properly, then array it; do not hand-model 4 identical floors |

### 15.2 Typology-specific modelling recipes

**Setback envelope first (all typologies).** Before any wall: draw the plot rectangle and the setback offset as `Draft` wires on the Site. Extrude the setback polygon to the height limit as a translucent `Part::Box` "envelope check" object. Every wall must sit inside it. This catches the coverage overshoot at model time instead of at approval time.

**Wall openings (all typologies — the FreeCAD 1.0.1 gotcha).** `Arch.makeWindow`'s `Hosts` / `Subtractions` link does **NOT** cut the wall in this build — verified by a zero volume-difference test. The working technique:
1. `Arch.makeWall` from a `Draft.makeLine` — the wall's real geometry comes from the line's absolute `Start`/`End`; the Wall object's own `.Placement` stays identity.
2. Read `wall.Base.Start` / `.End`, compute direction and perpendicular vectors.
3. Build a `Part.makeBox` opening sized and rotated to match.
4. `wall.Shape.cut(opening_box)` assigned to a **new** `Part::Feature`; keep the original Arch wall pristine and hidden.
5. **Verify by comparing `.Volume` before and after** — do not trust the viewport.
6. Separately create an `Arch.makeWindow(...)` per opening with `.IfcType = "Window"`/`"Door"` and `.Hosts = [wall]`, positioned at the same coordinates, purely for correct IFC classification.

**Jaali screens (farmhouse).** Build as a grid of small `Part.makeBox` holes cut sequentially from the wall's *current* shape, using the same direction/perpendicular maths as window cuts. Place as a **high clerestory band near the ceiling** on hot-facing (west/south) walls. Pairs with the wind tower: cool air in low, hot air out high through the perforations.

**Double-height atrium (farmhouse / duplex).** Model the void as an explicit subtraction from the first-floor slab, and give it a name that makes the diaphragm discontinuity visible in the tree (e.g. `FF_Slab_Void_Atrium`). When exporting or reporting, call it out to the engineer.

**Apartment / row-house typical unit.** Model one floor or unit as a `Part::Compound`, then use `Draft.array` for the repeat. Do not duplicate objects by hand — the FreeCAD auto-naming gotcha (below) makes hand-duplicated floors nearly impossible to edit later.

### 15.3 Known FreeCAD gotchas carried forward

| Gotcha | Handling |
|---|---|
| Auto-naming pads inconsistently (`Wall`, `Wall001`…`Wall009`, `Wall010`) | **Always query actual names via `doc.Objects` / regex.** Never assume `f"Wall{n}"`. |
| `doc.getObject()` looks up by internal `.Name`, **not** `.Label` | `if doc.getObject(label_string):` silently returns `None` and skips — this caused a real bug where stale duplicate walls were never deleted. Match on `.Label` explicitly when that's what you have. |
| `Import.export()` silently does nothing for `.ifc` | Use `from importers import exportIFC; exportIFC.export(object_list, path)` |
| FreeCAD's bundled Python may lack `typing_extensions` | `~/Applications/squashfs-root/usr/bin/python -m pip install typing_extensions`, with `PATH`/`PYTHONHOME` pointed at the AppImage's bundled Python |
| Exporting Arch **Wall** objects to IFC throws `'NoneType' object has no attribute 'Shape'` | **Unresolved.** Window/Door export works. Chase this before promising a full-building IFC export. |
| Requires a real `DISPLAY` | Xvfb hangs forever; run on `DISPLAY=:1` via `./AppRun`. See the FreeCAD MCP setup note. |

---

## Section 16: General Typology Reference — Non-Residential

Retained from the general typology corpus. This is the **secondary** layer: use it when a project genuinely is an office, clinic, school, mosque-adjacent community building, or mixed-use scheme, and as a comparative benchmark for efficiency and dimensional reasoning. Figures are UK/US/international practice (T3) unless noted — **they are not Pakistani standards** and should be labelled as such when quoted.

### 16.1 Office

| Metric | Speculative shell & core | Corporate HQ | Co-working |
|---|---|---|---|
| Floor plate (NIA) | 1,000–2,500 m² | 2,000–10,000+ m² | 1,000–5,000 m² |
| Plan depth core-to-glass | 12–15 m (BCO max 15 m for naturally ventilated) | 15–25 m (with atria) | — |
| Floor-to-floor | 3.6–4.2 m (BCO typical 3.9 m) | 3.9–4.5 m | > 3.5 m preferred |
| Finished ceiling | 2.6–2.85 m (BCO min 2.6) | — | Exposed services |
| Raised floor | 100–150 mm (BCO min 150) | — | — |
| Ceiling void | 400–600 mm | — | — |
| Structural depth | 300 mm (PT slab) – 500 mm (composite) | — | — |
| Structural grid | 7.5 / 9.0 / 10.8 / 12.0 m (coordinate with parking at 7.2–7.5 m) | — | — |
| **NTG** | **0.80–0.85 (BCO target 82.5%)** | 0.72–0.80 | 0.72–0.78 |
| Core-to-GIA | 15–22% | — | — |
| Loading | 2.5 kN/m² + 1.0 kN/m² partitions | — | — |
| Density | — | — | 6–8 m²/person; 0.6–0.8 desks/member |

**Exemplars:** Willis Building (Foster + Partners, 2007, London) — crescent plan, 46,450 m², column-free 18 m spans · The Leadenhall Building (Rogers Stirk Harbour, 2014) — 51 storeys, external bracing, 84,424 m² · 22 Bishopsgate (PLP, 2020) — 62 storeys, 128,000 m² · Inland Steel Building (SOM/Bruce Graham, 1958, Chicago) — first modern curtain-wall office tower, all services in a separate tower, 18.3 m clear spans · Apple Park (Foster + Partners, 2017) — 260,000 m² ring plan, 1.6 km circumference · Bloomberg European HQ (Foster + Partners, 2017) — 102,000 m², BREEAM Outstanding 98.5% · Second Home (Selgascano, 2014, London) — elliptical glass offices within open plan, 2,500 m².

### 16.2 Healthcare

**Plan types:**

| Type | Configuration | Advantage | Disadvantage | Exemplar |
|---|---|---|---|---|
| Podium + tower | Podium 2–4 storeys, 5,000–15,000 m² plates (clinical); tower 6–15 storeys, 1,000–2,000 m² plates (wards) | Big column-free clinical plates; wards get daylight | Long vertical travel; structural transfer at the interface | Royal London Hospital (HOK/Skanska, 2012) — 17 storeys, 115,000 m² |
| Courtyard / chequerboard | 3,000–8,000 m² plates with internal courtyards, 3–6 storeys | Short horizontal travel, daylight to deep plans | Large footprint; limited vertical expansion | Khoo Teck Puat (CPG, 2010, Singapore) — 590 beds, biophilic |
| Finger / pavilion | Linear wings 12–18 m deep, 18–25 m apart, on a spine corridor | Excellent daylight/ventilation; phased expansion | Long horizontal travel; large site | Alder Hey Children's Hospital (BDP, 2015) |
| Nucleus / compact | Cruciform or radial around a central core, 2,000–4,000 m² plates | Short travel, efficient servicing | Dark centre; complex wayfinding | NHS Nucleus template hospitals (1970s–80s) |

**Key metrics:** corridor 2.4 m min clear for bed movement (2.7 m recommended), 1.8–2.1 m ambulatory · patient room door 1.2 m clear · nurse station with direct sightline to all beds (28–32 bed unit max) · unidirectional clean→dirty flow, no backtracking · stacking ED and Imaging at ground, Surgery above ED, Wards above Surgery · floor-to-floor 4.2–5.0 m · **NTG 0.55–0.65 (the most inefficient common building type).**

**Clinic / surgery centre:** 500–3,000 m², 1–3 storeys; consult room 14–16 m² (GP min 12 m²); waiting 1.5–2.0 m²/concurrent patient; NTG 0.70–0.78; parking 3–5 spaces per consulting room. Exemplar: Maggie's Centres (Gehry, Hadid, Heatherwick, Chipperfield) — 200–400 m², domestic scale, open kitchen as the heart, no waiting room.

### 16.3 Education

| Metric | Primary | Secondary | University |
|---|---|---|---|
| Site | 1.0–2.0 ha (1 FE = 210 pupils) | 3.0–7.0 ha (6–12 FE = 900–1,800 pupils) | Campus coverage 20–40% |
| GIA | 1,100–2,200 m² (BB103) | 6,000–12,000 m² (BB103) | — |
| Storeys | 1–2 | 2–4 | — |
| Classroom | 55–63 m², min 2.0 m²/pupil | 55–65 m² (30 pupils) | Lecture theatre 1.2–1.5 m²/seat |
| Specialist | — | 80–110 m² (labs, workshops) | Teaching lab 2.5–3.5 m²/student |
| Corridor | 1.8 m min, 2.4 m recommended | 2.4–3.0 m | — |
| Hall | Assembly/dining 120–170 m² | Sports hall 594 m² (4-court) / 891 m² (6-court) | Library 4–5 m²/reader |
| **NTG** | 0.72–0.78 | 0.68–0.75 | 0.60–0.72 (lab-heavy lower) |
| Floor-to-floor | — | 3.3–3.9 m | 3.6–4.5 m (labs) |
| Daylight | Every teaching space glazed; min 2% average daylight factor | — | — |

**School plan types:** *finger* (parallel classroom wings with outdoor space between — best daylight, needs a big site) · *cluster* (classroom groups around a shared learning space — collaborative teaching) · *street* (wide daylit central corridor, classrooms both sides — compact) · *courtyard* (classrooms wrap a secure outdoor space — urban sites, passive surveillance).

**Exemplars:** Burntwood School (AHMM, 2015) — Stirling Prize, prefabricated CLT · Fuji Kindergarten (Tezuka, 2007, Tokyo) — oval roof as playground, 600 children · Ørestad Gymnasium (3XN, 2007, Copenhagen) — open-plan school around a central stair · Rolex Learning Centre (SANAA, 2010, Lausanne) — single undulating 20,000 m² plate, no internal walls · Saw Swee Hock Student Centre (O'Donnell + Tuomey, 2014, LSE) — 6,300 m².

### 16.4 Cultural

**Museum plan types:** *linear sequence / enfilade* (prescribed route, total narrative control — Vatican, Uffizi) · *free-flow open plan* (moveable partitions, visitor chooses — Centre Pompidou, Tate Modern Turbine Hall) · *mixed* (permanent collection sequential, temporary free-flow — the contemporary default).

| Museum metric | Value |
|---|---|
| Gallery ceiling | 4.5–6.0 m (paintings); 6.0–10.0 m (large sculpture/installation) |
| Gallery width | 6–12 m (paintings); 15–30 m (sculpture) |
| Gallery proportions | 1:1.5 to 1:2 (width:length) for painting galleries |
| Hanging height | Eye line 1.5 m; work centre 1.45–1.55 m |
| Lighting | 200 lux max (paintings, UV filtered); **50 lux max, no natural light** (works on paper) |
| Climate | 20 ± 2 °C, 50 ± 5% RH, 24/7/365 |
| BOH | 40–60% of public area |
| **NTG** | 0.55–0.65 |
| Floor loading | 5.0 kN/m² min (sculpture galleries) |

**Theatre configurations:**

| Type | Capacity | Actor–audience distance |
|---|---|---|
| Proscenium | 300–2,500 | 15–30 m |
| Thrust | 200–1,200 | 8–18 m |
| Arena (in-the-round) | 100–600 | 5–12 m |
| Black box | 50–400 | Variable |
| Courtyard (galleried) | 200–1,000 | 8–20 m |

Seat width 500–530 mm min (550 premium) · row spacing 760–850 mm back-to-back · aisle 1.1 m min · sightline C-value 65–125 mm (cinema), 100–130 mm (theatre) · acoustic volume 6–10 m³/seat (symphony), 4–7 (drama), 3–5 (cinema) · RT60 1.7–2.2 s (symphony), 1.0–1.4 s (drama), 0.6–0.8 s (speech) · stage depth 10–14 m (proscenium) · fly tower 2.5× proscenium opening height · **NTG 0.45–0.55 — the least efficient building type there is.**

**Library:** stacks 5–7 m² per 1,000 volumes (mobile shelving halves it) · reading 4–5 m²/reader · digital 3–4 m²/workstation · floor loading 6.5 kN/m² stacks, 2.5 kN/m² reading · ceiling 3.0–4.0 m reading, 2.7 m min stacks · NTG 0.65–0.75.

**Exemplars:** Guggenheim Bilbao (Gehry, 1997) — 24,000 m² · MAXXI (Hadid, 2010, Rome) — 21,000 m² · Louvre Abu Dhabi (Nouvel, 2017) — 9,200 m² galleries under a 180 m dome · Tate Modern (Herzog & de Meuron, 2000/2016) — 35,000 m² power-station conversion · Sydney Opera House (Utzon, 1973) — 5,738 seats · Elbphilharmonie (Herzog & de Meuron, 2017) — 2,100-seat vineyard hall · Seattle Central Library (OMA, 2004) — 34,000 m², Book Spiral · Tianjin Binhai Library (MVRDV, 2017) — 33,700 m² · Bait Ur Rouf Mosque (Marina Tabassum, 2012, Dhaka) — courtyard as environmental mediator, and the closest exemplar in this list to South Asian climatic practice.

### 16.5 Hospitality

| Hotel plan type | Key metrics | NTG |
|---|---|---|
| Corridor-loaded (double) | Corridor 1.5–1.8 m (budget) / 1.8–2.1 m (luxury); room depth 6–12 m; room width 3.3–6.0 m; 20–40 rooms per wing | 0.62–0.72 |
| Atrium | Atrium 15–30 m wide, full height; 30–80 rooms/floor | 0.55–0.65 |
| Courtyard | Courtyard 15–40 m across; 2–5 storeys | 0.58–0.68 |
| Tower | Plate 800–2,000 m²; 12–30 rooms/floor; 2+ lifts + service + firefighting lift + 2 stairs | 0.60–0.68 |

| Metric | Budget | Midscale | Upscale | Luxury |
|---|---|---|---|---|
| Room NIA (m²) | 16–20 | 22–28 | 30–40 | 40–60+ |
| Bathroom (m²) | 3–4 | 4–5 | 6–8 | 8–12+ |
| Floor-to-floor (m) | 2.9–3.1 | 3.0–3.3 | 3.3–3.6 | 3.6–4.2 |
| Lobby (m²/room) | 0.5–0.8 | 0.8–1.2 | 1.2–1.8 | 1.8–3.0 |
| F&B (seats/room) | 0.3–0.5 | 0.5–0.7 | 0.7–1.0 | 1.0–1.5 |
| BOH (% of FOH) | 40–50% | 45–55% | 50–60% | 55–70% |
| GIA/room (m²) | 35–45 | 50–65 | 70–90 | 90–140 |
| Staff/room | 0.3–0.5 | 0.5–0.8 | 0.8–1.2 | 1.2–2.5 |

**Restaurant:** dining 1.4–1.8 m²/seat (casual), 1.8–2.5 (fine) · kitchen 40–60% of dining (full production), 25–40% (finishing) · bar 0.5–0.8 m²/stool · WC 1 per 30 covers (M), 1 per 15 (F) · floor-to-ceiling 3.0–3.5 m (4.0–5.0 destination) · kitchen ceiling 3.0 m min for extraction · separate service entrance.

**Exemplars:** Hyatt Regency Atlanta (John Portman, 1967) — the first atrium hotel, 22 storeys, 800 rooms · Marina Bay Sands (Safdie, 2010) — 3 towers, 2,561 rooms · Oasia Hotel Downtown (WOHA, 2016, Singapore) — 314 rooms, sky gardens every 6 floors, 89% green plot ratio.

### 16.6 Mixed-use and hybrid

**Podium-tower:** podium 2–6 storeys, 2,000–10,000 m² plates (retail/office/parking); tower 10–80+ storeys, 400–2,000 m² plates; structural transfer beams/slabs up to 3 m deep at the interface; tower set back 3–5 m from the podium edge for an amenity terrace. Exemplars: De Rotterdam (OMA, 2013) — 162,000 m² · Brickell City Centre (Arquitectonica, 2016) · Battersea Power Station Phase 2 (Foster + Gehry, 2021).

**Vertical stacking order (bottom to top):** Parking → Retail → Office → Hotel → Residential. Logic: heavier uses low, public uses at grade, quieter uses high. Floor-to-floor varies by use: retail 4.5 m, office 3.9 m, hotel 3.3 m, residential 3.0 m. 2-hour fire-rated floor between use classes; min 50 dB airborne + 55 dB impact between residential and commercial; **each use class needs its own lift lobby and fire escape.**

**Design challenges and resolutions:**

| Challenge | Resolution |
|---|---|
| Entrance separation | Each use gets its own lobby and street address; residential entrance distinct from commercial |
| Servicing conflicts | Separate loading docks, or a time-managed shared dock; separate waste collection |
| Structural grid mismatch | Office 9 m vs residential 6–7.5 m vs parking 7.2 m → transfer structure |
| Ceiling height variation | Careful section design at use interfaces |
| Acoustic isolation | Floating floors, isolated structural connections, buffer floors at transitions |
| Fire egress | Independent egress to grade per use class; **no shared escape routes** |
| Wind | Tower-on-podium creates downdrafts; pedestrian comfort wind study required |
| Parking | Zoned per use; different peak times enable a shared-use reduction |

**Vertical village:** self-contained community in one tall building; sky lobbies every 10–15 floors with shared amenity; outrigger trusses at sky lobbies for wind resistance. Exemplar: The Interlace (OMA/Ole Scheeren, 2013, Singapore) — 31 blocks of 6 storeys stacked at angles, 1,040 units, 170,000 m².

---

## Section 17: International Residential Typology Comparison

Retained as a comparison layer. Use it when a client cites a foreign precedent, when reasoning about density, or when a Pakistani scheme is genuinely trying a Western form (co-living in Karachi, terraced housing in a new town). **These are UK/EU/US figures (T3) — do not present them as applicable Pakistani norms.**

| Typology | Plan depth | Storeys | Unit GIA | Density (DU/ha) | NTG | Nearest Pakistani equivalent |
|---|---|---|---|---|---|---|
| Detached house | 8–12 m | 1–3 | 80–300 m² (860–3,230 sqft) | 10–30 | 0.85–0.92 | **5 marla – 1 kanal detached** (Pakistani NTG is lower — thicker walls, more attached baths) |
| Semi-detached | 8–10 m | 2–3 | 70–150 m² | 25–50 | — | **Duplex pair on a kanal plot** (Section 6.2) |
| Terrace / rowhouse | 8–12 m deep, 4.5–7 m wide | 2–4 | 65–140 m² | 40–80 | 0.85–0.90 | **Developer-built row house / townhouse in gated schemes (Section 5.5)** — increasingly common product; individually-sold 3-marla adjacent plots remain the low-end exception, not the rule |
| Walk-up apartment | 10–14 m (6–8 single-loaded) | 3–5 | 45–90 m² | 60–150 | 0.78–0.84 | **Walk-up block (Section 8.3)** |
| Mid-rise apartment | 12–18 m | 6–12 | — | 100–250 | 0.75–0.82 | Mid-rise block |
| High-rise tower | 18–24 m (point) / 12–16 m (slab) | 13+ | — | 200–600+ | 0.68–0.82 | Karachi/Islamabad towers |
| Maisonette | 8–14 m | 2 per unit | 65–120 m² | — | — | **Duplex unit (Section 6.1)** |
| Courtyard housing | 6–10 m wings around a 6–15 m court | 1–3 | 60–200 m² | 40–100 | — | **Traditional Lahore house; farmhouse courtyard plan (Section 7.3)** |
| Co-housing | — | — | 40–100 m² private + 150–300 m² common house | 30–80 | — | No Pakistani equivalent; extended-family compounds serve the function informally |
| Micro / co-living | — | — | 10–25 m² private + 5–10 m²/unit shared | 200–500+ | 0.65–0.75 | Thin market; hostel/student housing is the nearest form |

**Terrace key dimensions (T3):** min width for 2-bed 4.5 m internal (5.0–5.5 preferred); 3-bed 5.5 m (6.0–7.0 preferred); stair 850 mm min clear (900 preferred); hallway 900 mm min. **Note how far below Pakistani practice these are** — a 900 mm (2'-11") hallway is unacceptably narrow against the Pakistani 3'-6" target.

**Exemplars (retained):** Farnsworth House (Mies, 1951) 140 m² · Maison Bordeaux (OMA, 1998) 500 m² · Moriyama House (Nishizawa, 2005, Tokyo) 263 m² as a cluster of discrete volumes · Donnybrook Quarter (Peter Barber, 2006, London) 65 DU/ha · Accordia (FCB/Maccreanor Lavington/Alison Brooks, 2008, Cambridge) 47 DU/ha · Georgian Terrace (Bath/London/Edinburgh, 1714–1830) — 5–7 m wide, 12–15 m deep, the prototype · Borneo Sporenburg (2000, Amsterdam) 5.1 m wide, 100 DU/ha · Goldsmith Street (Mikhail Riches, 2019, Norwich) Stirling Prize Passivhaus terrace · Silodam (MVRDV, 2003) 157 units · Ely Court (Alison Brooks, 2015) · Via Verde (Grimshaw + Dattner, 2012, Bronx) 222 units · The Interlace (OMA, 2013, Singapore) 1,040 units · Unité d'Habitation (Le Corbusier, 1952, Marseille) 18 storeys, skip-stop, 337 units · Barbican Estate (Chamberlin Powell & Bon, 1969–76) 2,014 units · 432 Park Avenue (Viñoly, 2015) 85 storeys, 28.5 × 28.5 m plan, 104 units · Bosco Verticale (Boeri, 2014, Milan) 113 units, 900 trees · Alexandra Road Estate (Neave Brown, 1978) 520 dwellings · Marmalade Lane (Mole Architects, 2019, Cambridge) 42 co-housing homes · Carmel Place (nARCHITECTS, 2016, NY) 55 micro-units of 23–33 m² · The Collective Old Oak (PLP, 2016, London) 546 co-living units · Salk Institute (Kahn, 1965) · Courtyard Houses Matosinhos (Souto de Moura, 1993–99).

---

## Section 18: Answer Templates and Checklists

### 18.1 Standard opening for a typology question

```
Before I pick a typology I need five things:
1. Plot size AND dimensions in feet (the marla is 225 sqft in most schemes but
   272.25 sqft in some Islamabad societies — a 21% difference)
2. City, authority, scheme and phase (this sets coverage, setbacks, whether
   apartments or separate portion entrances are even allowed, and — above
   1 kanal — whether the plot is farmhouse-zoned or just farmhouse-sized inside
   an ordinary residential scheme)
3. Who lives there — one family, family + rental portion, two households, weekend
   use, or a developer row-house product?
4. Budget, and whether that's grey structure or turn-key
5. Bedrooms needed now and in ten years

Tell me what you have and I'll say which decisions are blocked on the rest.
```

### 18.2 Pre-handoff checklist — before presenting any typology proposal

- [ ] Plot confirmed **in feet**, not just marla
- [ ] Coverage % and FAR checked against the **actual authority** (not the generic table) — routed to `architecture-building-codes-permits`
- [ ] For any plot 2+ kanal: farmhouse-zoning gate checked (Section 7.6) — farmhouse coverage bands are NOT applied by default to a large plot in an ordinary residential scheme
- [ ] Setbacks applied, including the **5 ft side gali above 10 marla**
- [ ] Buildable footprint calculated and the program **actually fits inside it** (do the arithmetic, do not eyeball)
- [ ] Every clear span checked against the slab-thickness table (Section 11.3) — **any span > 14 ft flagged explicitly, and any span > 16 ft flagged as requiring at least a hybrid RC beam-and-column bay per Section 11.1**
- [ ] Structural system selected and stated (confined masonry vs RC frame vs hybrid), with the reason
- [ ] Seismic zone identified from a current zoning map (never assumed by city name from memory); confining elements / plinth beam / corner-window avoidance flagged in Zone 2B+, labelled as good practice unless a clause has actually been page-verified
- [ ] Bedroom and bathroom counts checked against market expectation for the plot band (Section 9.2, 9.3)
- [ ] Car parking provided at the plot band's expected count, at ≥ 10 × 14 ft per space
- [ ] NIA/GCA computed and sanity-checked (0.68–0.80 for a house)
- [ ] Cost stated as covered-area × dated 2026 rate, **with the modifiers** (basement, boundary wall, landscaping) — not the bare base rate
- [ ] Evidentiary tier stated for every number that a client might act on
- [ ] **Licensing disclaimer given** — PEC-stamped structural design and authority map approval required before construction
- [ ] If the user sounds like they're about to build: disclaimer restated **unprompted, at the top of the reply**

### 18.3 Phrases to use verbatim

| Situation | Say |
|---|---|
| Client cites a covered-area figure that exceeds coverage law | *"That number needs a basement or a wider plot to be legal. Which is it? I don't want to design to a figure that fails at map approval."* |
| Client wants a big open room | *"That's a [N] ft clear span. A normal 6-inch slab tops out around 14 ft, and anything past 16 ft needs at least one RC beam on its own columns even in an otherwise masonry house. You'll need beams, a thicker slab, or a slightly smaller room — cheapest is [option]. Which?"* |
| Client says "duplex" | *"Quick check — do you mean one two-storey unit with its own internal stair, or two separate units, upper and lower portion? Those are completely different buildings."* |
| Client has a 2+ kanal plot | *"Is this plot inside a scheme zoned specifically for farmhouses, or just a large plot in an ordinary residential phase? The legal coverage is very different — 40–55% for a real farmhouse zone versus 65–70% for an ordinary large residential plot."* |
| Client asks for an NTG benchmark | *"There's no published net-to-gross standard for single-family houses — that metric only exists for commercial leasing. I can compute it for your plan as a design diagnostic, but don't quote it as an industry figure."* |
| Client cites a BCP or IRC section number | *"IRC is a US code, not adopted in Pakistan — useful as a rigor benchmark only. For BCP clause numbers, the engineer should cite from the actual PDF; I don't want to quote a section I haven't page-verified."* |
| Client is about to build | *"This is a planning study, not a stamped drawing. A PEC-registered structural engineer has to review and stamp it, and it needs [authority] map approval before anyone breaks ground."* |

---

## References

### Pakistan — primary and near-primary

- **Building Code of Pakistan — Seismic Provisions 2007 (BCP-SP-2007)**, Pakistan Engineering Council / Ministry of Housing & Works. PDF hosted at `urbanunit.gov.pk`. *Section numbers and zone-boundary assignments in this skill are unverified against the primary text and current zoning maps — fetch and verify before citing clauses or classifying a specific city's zone.*
- **Building Code of Pakistan 2021** (IBC-based update). Full residential/non-seismic chapters not confirmed indexed in the research behind this skill — retrieve the PDF directly before citing specific sections.
- **Pakistan Engineering Council** — Building Code of Pakistan think-tank, `pec.org.pk/thinktank/building-code-of-pakistan-thinktank/`
- **LDA Building & Zoning Regulations 2019** (amended through 28 Jan 2020), Lahore Development Authority — `lda.gop.pk`
- **CDA Building Regulations** (Islamabad) — marla defined locally at 272.25 sqft; stricter FAR on 1-kanal-plus plots to preserve green character
- **FDA Building and Zoning Regulations 2020**, Faisalabad Development Authority
- **Etihad Town Building By-Laws** — a worked example of a private-scheme byelaw set
- **World Housing Encyclopedia Report 173 — "Brick Masonry Construction in Pakistan"** (EERI/IAEE), `world-housing.net` — **the primary source for the 9-inch wall thickness and 30×60 to 60×90 ft envelope data (T5).**
- UNDP Pakistan / ReliefWeb — *Seismic Design in Pakistan: Building Code, Bylaws and Recommendations for Earthquake Risk*

### International codes (T3 — reference/benchmark only, not Pakistan-binding)

- **ACI 318-19**, *Building Code Requirements for Structural Concrete* — Table 7.3.1.1 (one-way slab minimum thickness), §8.3.1.1 (two-way slab minimum, 5 in / 127 mm). **Cite this, not the practitioner 5–6" rule, for slab thickness.** Primary text not independently verified in the research behind this skill.
- **ASCE 7-22**, *Minimum Design Loads* — live/dead/wind loads; would supplement BCP-SP-2007
- **IRC 2021** (ICC, US) — R305 ceiling height, R310 emergency escape openings, R311.2 egress door (6'-8"/80 in), R311.7 stairways. **Not adopted in Pakistan.**
- **IBC 2021** (ICC) — non-residential and multi-family provisions
- **NBC India 2016**, Parts 3 & 4; **IS 456** — nearest codified South Asian reference where Pakistan is silent (T2)

### General typology (T3)

- Neufert, E. & Neufert, P. (2019). *Neufert Architects' Data*, 5th ed. Wiley-Blackwell.
- Littlefield, D. *Metric Handbook: Planning and Design Data*. Routledge.
- Kliment, S.A. (ed.). *Building Type Basics* series. Wiley.
- BCO (2019). *BCO Guide to Specification*. British Council for Offices.
- MHCLG (2015). *Technical Housing Standards — Nationally Described Space Standard*. UK Government.
- NHS Estates. *Health Building Notes* (HBN) series.
- DfE (2014). *Building Bulletin 103 / 104*. UK Department for Education.
- Sport England. *Design Guidance Notes*.
- Firley, E. & Stahl, C. (2009). *The Urban Housing Handbook*. Wiley.
- Mozas, J. & Fernández Per, A. (2006). *Density: New Collective Housing*. a+t.
- Koolhaas, R. & Mau, B. (1995). *S, M, L, XL*. Monacelli Press.
- CTBUH. *Tall Building Design Guides*.
- RIBA Plan of Work (2020).

### Pakistani market data (T4 — commercial sources, dated 2026, verify before quoting)

Plot-size conversion, room programs and covered-area examples drawn from Pakistani architect/developer plan sets and property portals (Zameen, Primarc Studio, Amanah, Gharhub, Avenir Developments, Highland Constructions, NZ Architects, Al Syed Construction, Elegant DHA, Makaan Solutions, Civil Engineers PK, Naksha Nigar, Medaghar, Aiwa Properties). 2026 construction-cost bands from Glorious Builders, Avenir Developments, HA Design Studio, Shelters Engineering, Elegant Design PK. Apartment unit-size bands from Zameen and Elegant DHA. Net-to-gross benchmark ranges from Coohom, illustrarch and Young Architect. **All T4 — market data, not code. Ranges overlap and move; re-verify before quoting to a client.**

### Internal cross-references

- `architecture-spatial-planning` — room sizing, courtyards, orientation, stairs, plan archetypes, circulation
- `architecture-building-codes-permits` — setbacks, coverage, FAR, approval process, PEC/PCATP stamping
- `architecture-seismic-design` — seismic zones, confined masonry rules, irregularities, detailing
- `architecture-structural-systems` — grids, spans, lateral systems, foundations
- `architecture-concrete-reinforcement-detailing` — rebar, laps, cover, BBS
- `architecture-geotechnical-foundations` — bearing capacity, water table, basement viability
- `architecture-cost-estimation-boq` — element-level quantities and BOQ
- `architecture-construction-sequencing` — build order, curing, hold points
- `architecture-accessibility-design` — accessible routes and dimensions
- `architecture-freecad-bim` — the FreeCAD modelling contract (load before writing any wall code)
- `drawio-diagrams` — 2D floor plans and blueprints as editable `.drawio` files
- Project memory: `project_farmhouse_2kanal` — the `~/Documents/Farmhouse_2Kanal_Template.FCStd` reference model and its verified techniques
