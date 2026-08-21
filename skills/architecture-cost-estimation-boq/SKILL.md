---
name: architecture-cost-estimation-boq
description: >
  Construction cost estimation and Bill of Quantities (BOQ) for Pakistani
  residential projects: element-by-element quantity takeoff from a structural
  or architectural design, concrete mix and material conversion tables, steel
  reinforcement thumb rules and bar-weight schedules, brick and mortar
  quantities, Pakistan market rates for 2026, composite per-sqft rates,
  cost breakdown structure (grey vs finishes vs MEP), contingency and
  escalation allowances, contract types and payment schedules, and a
  structured procedure for sanity-checking a contractor quote against an
  independently derived BOQ estimate.
---

# Cost Estimation & Bill of Quantities — Pakistani Residential Construction

A BOQ is the bridge between a drawing and a budget. It converts geometry into measured
quantities, quantities into priced items, and priced items into a defensible total that
can be tendered, compared, and audited. This skill covers the full chain for low-rise
residential work in Pakistan — 5 Marla to 2 Kanal, RCC frame with masonry infill, the
dominant construction system across Punjab, Sindh, KPK and ICT.

The reference currency is PKR. Local trade units (cft, sqft, rft, Marla, Kanal, bag,
Lac, Crore) are used throughout because that is what quotations, MRS schedules and
suppliers actually use; SI equivalents are given wherever a code citation requires them.

---

## Reality Check - Licensing & Liability

**This skill produces design aids, quantity estimates and calculation guidance for
planning, budgeting and FreeCAD modeling ONLY.**

- Every quantity, rate, ratio and thumb rule in this file is a **planning-stage aid**. It
  is not a structural design, not a tender document, and not a construction-ready BOQ.
- Any design intended for the actual construction of a real occupied building **MUST** be
  reviewed, sealed and stamped by a **licensed structural engineer registered with the
  Pakistan Engineering Council (PEC)** — or the equivalent registered professional in the
  relevant jurisdiction — before a single foundation is dug.
- The drawings and BOQ **MUST** go through **local authority plan approval** before
  construction: LDA (Lahore), CDA (Islamabad), RDA (Rawalpindi), KDA/SBCA (Karachi), PDA,
  FDA, DHA, or the relevant TMA/cantonment board, under their current building byelaws
  (setbacks, FAR, height, covered-area limits, parking, structural submission
  requirements).
- Steel quantities derived from the thumb rules in Section 5 are **budgeting figures, not
  a bar bending schedule**. A real BBS comes from a stamped structural design to
  BCP-SP-2007 / BCP-2021 and ACI 318-19, with the correct seismic zone, soil bearing
  capacity, and load combinations.
- Rates in Section 8 are a **snapshot dated August 2026** in a market that has moved
  double-digit percentages within single quarters. Re-verify every rate at the moment of
  estimating. An estimate quoting stale rates as current is worse than no estimate.
  As Section 8.1 makes explicit, the large majority of the individual material and
  labour rates behind this entire skill are **Tier C — typical ranges, not independently
  sourced at this date** — including nearly everything feeding the Section 11 worked
  example. A worked example with exact-looking arithmetic is not evidence that its
  inputs are verified; treat every Tier C figure as a placeholder until re-priced
  locally, no matter how precise the final total looks.

**Behavioural rule for Claude / Claude:**
Never present a FreeCAD export, a generated BOQ table, or any calculation from this skill
as construction-ready. If the user's language suggests they are treating the output as
final — "so this is what I'll give the contractor", "we're breaking ground next week",
"I'll build to these numbers", "send this to the mason" — **say so unprompted, in the same
reply**, and state plainly that a PEC-registered structural engineer's stamp and local
authority approval are required first. Do not wait to be asked. Do not bury it in a
footnote.

---

## Section 1: The BOQ Derivation Pipeline

### 1.1 When to invoke this skill

- Any request for a construction cost, budget, or "how much will this house cost"
- Producing a BOQ, quantity takeoff, or material schedule from a plan or FreeCAD model
- Comparing or auditing a contractor's quotation or bid
- Setting a contingency, escalation or allowance figure
- Deciding between grey-structure-only, labour-rate, and turnkey contracting
- Converting a FreeCAD/BIM model into procurement quantities

Pair with `architecture-structural-systems` (member sizing that feeds the takeoff),
`architecture-spatial-planning` (covered-area determination), and
`architecture-freecad-bim` (model → quantities).

### 1.2 Eleven-step pipeline

```
1.  FIX THE SCOPE          → covered area per floor, storeys, inclusions/exclusions list
2.  FIX THE SPEC LEVEL     → economy / A-category / premium (drives finishes, not structure)
3.  CLASSIFY THE ELEMENTS  → substructure, superstructure, envelope, finishes, MEP, external
4.  MEASURE GROSS          → geometry only, from drawings or model, no rates yet
5.  APPLY DEDUCTIONS       → openings, voids, per Section 3 rules
6.  CONVERT TO MATERIALS   → concrete → cement/sand/crush; masonry → bricks/mortar; steel → kg
7.  ADD WASTAGE            → per-material factors, Section 3.4
8.  BUILD UNIT RATES       → material + labour + plant + transport + OH&P, Section 9
9.  PRICE THE BOQ          → quantity × rate, subtotal per element group
10. ADD SOFT COSTS         → professional fees, approvals, utilities, taxes (Section 14)
11. ADD CONTINGENCY + ESCALATION → per design maturity and programme duration (Section 13)
```

**Never skip step 4/5 separation.** Measuring net directly (eyeballing deductions while
measuring) is the single most common source of unreproducible estimates. Gross first,
deductions as a visible line, net as the result.

### 1.3 Three-method triangulation rule

A residential estimate is only trustworthy when **three independent methods agree within
±10%**. If they do not, one of them is wrong — find out which before issuing a number.

| Method | How | Use as |
|---|---|---|
| **A — Composite rate** | Covered area × PKR/sqft benchmark (Section 8.4) | Fast sanity bound |
| **B — Detailed BOQ** | Full element takeoff × unit rates (Sections 4–9) | The actual estimate |
| **C — Ratio build-up** | Grey structure cost ÷ grey share % (Section 10) | Independent cross-check |

Worked triangulation appears in Section 11.8.

---

## Section 2: BOQ Structure & Item Coding

### 2.1 Standard residential BOQ bill structure

| Bill | Title | Typical share of build cost |
|---|---|---|
| 1 | Preliminaries & site establishment | 2–4% |
| 2 | Earthwork & substructure | 6–10% |
| 3 | Concrete works (PCC + RCC) | 16–22% |
| 4 | Reinforcement steel | 14–19% |
| 5 | Masonry works | 6–9% |
| 6 | Plaster & rendering | 4–6% |
| 7 | Damp proofing, roof treatment & waterproofing | 2–3% |
| 8 | Doors, windows & joinery | 8–12% |
| 9 | Flooring & wall finishes | 10–14% |
| 10 | Painting & false ceiling | 4–7% |
| 11 | Plumbing & sanitary (rough-in + fixtures) | 6–9% |
| 12 | Electrical (conduiting + wiring + fixtures) | 6–9% |
| 13 | Steel fabrication (grills, railings, gates) | 2–4% |
| 14 | Elevation / facade works | 3–6% |
| 15 | External works & boundary | 2–5% |
| 16 | Provisional sums & prime cost items | as scheduled |

Bills 1–7 (+ MEP rough-in from 11 & 12) = **grey structure**. Bills 8–15 = **finishing**.

### 2.2 Item numbering convention

Use `B.SS.ii` — Bill, sub-section, item.

```
3.02.01   RCC 1:1.5:3 (M20) in isolated footings, incl. shuttering,   cft   900   650   585,000
          mixing, placing, compaction and curing; reinforcement paid
          separately under Bill 4.
```

Every BOQ line **must** carry: item code, full description including mix/grade/spec,
unit, quantity, rate, amount. A line missing the mix ratio, the steel grade, or the
brick class is not a BOQ line — it is a guess with a number next to it.

### 2.3 Units used in Pakistani practice

| Work type | Unit | Note |
|---|---|---|
| Excavation, PCC, RCC, brickwork, sand, crush | **cft** | 1 m³ = 35.3147 cft |
| Plaster, flooring, shuttering, paint, roof treatment, tiling | **sqft** | 1 m² = 10.7639 sqft |
| Skirting, cornice, railing, kerb, pipe runs | **rft** | running foot |
| Reinforcement steel, binding wire | **kg** or **tonne** | 1 t = 1,000 kg |
| Cement | **bag** | 1 bag = 50 kg = 1.25 cft = 0.0347 m³ |
| Bricks | **per 1,000 nos** | quoted as "per thousand" |
| Doors, windows, fixtures, fans | **each / no.** | |
| Land | **Marla / Kanal** | 1 Marla = 225 sqft (urban standard); 1 Kanal = 20 Marla = 4,500 sqft. Legacy Marla = 272.25 sqft — always confirm which. |

Money: 1 Lac = 100,000 PKR. 1 Crore = 100 Lac = 10,000,000 PKR.

---

## Section 3: Measurement Conventions & Deduction Rules

### 3.1 Deduction rules by work type

| Work | Deduct | Do NOT deduct | Add |
|---|---|---|---|
| **Excavation** | — | working space is measured, not deducted | 0.5–1.0 ft working margin each side of footing |
| **PCC** | — | — | 3" projection each side beyond footing |
| **RCC** | openings > 0.1 m² (≈ 1 sqft) | reinforcement volume; openings ≤ 0.1 m²; chases | — |
| **Brickwork** | openings > 0.5 m² (≈ 5 sqft) full area | openings ≤ 0.1 m²; bearings of lintels/beams ≤ 0.1 m² | — |
| **Plaster** | openings > 0.5 m² — deduct one face only for a single-face opening; both faces for through openings | openings ≤ 0.5 m² | jambs, soffits and reveals measured separately |
| **Flooring** | column bases, hearths, openings > 0.1 m² | skirting is separate (rft) | — |
| **Shuttering** | — | — | measure the actual contact area only |
| **Paint** | openings > 0.5 m² | — | grill/railing painted area × 2 for both faces |

### 3.2 Practical net factors (use when detailed openings are not yet drawn)

| Element | Gross → net factor | Basis |
|---|---|---|
| External 9" masonry | × 0.72 – 0.80 | 20–28% openings typical for A-category residential |
| Internal 9" masonry | × 0.85 – 0.90 | door openings only |
| Internal 4.5" partitions | × 0.85 | door openings only |
| Internal plaster | × 0.80 – 0.85 | applied to gross wall face area |

Flag these as assumptions in the estimate. Replace with real openings the moment the
elevations are drawn — a 5% error in opening area is a 4% error in masonry cost.

### 3.3 Useful area relationships (residential, double-storey)

| Derived quantity | Multiplier on covered area |
|---|---|
| Internal plaster (walls both faces + ceilings) | × 2.4 – 2.7 |
| External plaster | × 1.0 – 1.2 |
| Total paint area (int + ext) | × 3.4 – 3.8 |
| Flooring (tile/marble, net of stairs and terraces) | × 0.88 – 0.95 |
| Shuttering (all RCC) | × 2.2 – 2.6 |
| RCC volume | × 1.10 – 1.40 cft/sqft |
| Brickwork volume | × 0.75 – 0.95 cft/sqft |

### 3.4 Wastage allowances

| Material | Wastage | Notes |
|---|---|---|
| Bricks | 5–10% | breakage in transport, cutting at corners; use 7% default |
| Cement | 2–3% | bag damage, spillage |
| Sand & crush | 5–8% | stockpile loss, contamination at ground stockpiles |
| Reinforcement steel | 3–5% **plus** laps | laps are *not* wastage — schedule them (Section 5.5) |
| Floor tiles | 8–12% | pattern cuts; 15% for diagonal or large-format |
| Marble | 12–18% | vein matching, edge loss |
| Paint | 5% | |
| Timber / joinery | 10–15% | |

Wastage is applied to **procurement quantity**, never to the measured BOQ quantity that
the contractor is paid on (unless the contract explicitly says so). Keep the two columns
separate: `Measured Qty` and `Procurement Qty`.

---

## Section 4: Concrete — Mix Designs & Material Conversion

### 4.1 Nominal mixes and where they belong

| Grade | Nominal mix (C:S:A) | Approx. strength | Residential application |
|---|---|---|---|
| **1:4:8** | 1:4:8 | ~7.5 MPa / 1,100 psi | Lean/blinding PCC under footings, floor sub-base |
| **1:3:6** | 1:3:6 | ~10 MPa / 1,450 psi | Mass fill, plinth filling, non-structural pads |
| **M15** | 1:2:4 | 15 MPa / 2,175 psi | Isolated footings on good soil, low-load elements, boundary-wall footings |
| **M20** | 1:1.5:3 | 20 MPa / 2,900 psi | **The residential standard** — slabs, beams, columns, lintels, stairs on normal firm soil |
| **M25** | 1:1:2 | 25 MPa / 3,625 psi | Soft, clayey or sandy soils; raft foundations; tall/slender columns; water tanks |
| **M30+** | design mix | 30 MPa+ | Design-mix only — batching plant, not site mixing. Basements, deep rafts, high seismic zone frames. |

**Rule:** nominal mixes are permitted for small residential work up to ~M20/M25. Anything
above M25, or any structural element on questionable soil, requires a **design mix with
trial cubes** and an engineer's approval. Do not site-batch above M25 by volume.

**Soil trigger:** if the geotechnical report gives safe bearing capacity below
~1.0 kg/cm² (≈ 2 t/ft²), or the soil log shows plastic clay / loose sand, escalate the
mix and re-check the footing sizes with the structural engineer — this typically moves
foundation cost by +15–30%.

### 4.2 Dry-volume conversion factors

| Conversion | Factor | Why |
|---|---|---|
| Wet concrete → dry material volume | **× 1.54** | voids between aggregate + bulking |
| Wet mortar → dry material volume | **× 1.30** (1.27–1.33) | sand bulking |
| Bulk sand delivered wet → dry | ÷ 1.20 – 1.30 | measure sand dry or apply bulking correction |
| 1 cement bag | 50 kg = **1.25 cft** = 0.0347 m³ | |
| 1 m³ | 35.3147 cft | |

### 4.3 Material per unit volume of concrete — master table

**Per 100 cft of finished concrete** (dry volume = 154 cft):

| Mix | Cement (cft) | Cement (bags) | Sand (cft) | Crush (cft) |
|---|---|---|---|---|
| 1:4:8 | 11.8 | **9.5** | 47.4 | 94.8 |
| 1:3:6 | 15.4 | **12.3** | 46.2 | 92.4 |
| M15 (1:2:4) | 22.0 | **17.6** | 44.0 | 88.0 |
| M20 (1:1.5:3) | 28.0 | **22.4** | 42.0 | 84.0 |
| M25 (1:1:2) | 38.5 | **30.8** | 38.5 | 77.0 |

**Per 1 m³ of finished concrete** (dry volume = 1.54 m³):

| Mix | Cement (bags) | Cement (kg) | Sand (m³) | Sand (cft) | Crush (m³) | Crush (cft) |
|---|---|---|---|---|---|---|
| 1:4:8 | 3.4 | 170 | 0.47 | 16.6 | 0.94 | 33.2 |
| M15 (1:2:4) | 6.3 | 315 | 0.44 | 15.5 | 0.88 | 31.1 |
| M20 (1:1.5:3) | **8.06** | **403** | 0.42 | 14.8 | 0.84 | 29.7 |
| M25 (1:1:2) | 11.1 | 555 | 0.385 | 13.6 | 0.77 | 27.2 |

Derivation (M20, per m³): dry vol 1.54 m³ ÷ (1+1.5+3 = 5.5) = 0.280 m³ cement
= 0.280 ÷ 0.0347 = **8.06 bags**; sand = 0.280 × 1.5 = 0.42 m³; crush = 0.280 × 3 = 0.84 m³.

### 4.4 Water and admixtures

| Item | Rule |
|---|---|
| Water–cement ratio | 0.45–0.55 for M20 nominal; lower w/c = higher strength, worse workability |
| Water per bag | ~22–25 litres for w/c 0.45–0.50 |
| Curing water | 3–5 litres per sqft of slab per day, 7–14 days — budget it, sites always forget |
| Plasticiser | 0.5–1.0% by cement weight; adds ~PKR 8–15 per cft of concrete — worth it for columns and congested beams |

---

## Section 5: Steel Reinforcement Quantities

### 5.1 Bar weight schedule (W = d²/162 kg/m, d in mm)

| Local size | # (sutar) | Ø (in) | Ø (mm) | kg/m | kg/ft | kg per 40-ft bar |
|---|---|---|---|---|---|---|
| 3/8" | #3 | 0.375 | 9.53 | 0.560 | 0.171 | 6.8 |
| 1/2" | #4 | 0.500 | 12.70 | 0.994 | 0.303 | 12.1 |
| 5/8" | #5 | 0.625 | 15.88 | 1.552 | 0.473 | 18.9 |
| 3/4" | #6 | 0.750 | 19.05 | 2.235 | 0.681 | 27.2 |
| 7/8" | #7 | 0.875 | 22.22 | 3.042 | 0.927 | 37.1 |
| 1" | #8 | 1.000 | 25.40 | 3.973 | 1.211 | 48.4 |
| 8 mm | — | — | 8 | 0.395 | 0.120 | 4.8 |
| 10 mm | — | — | 10 | 0.617 | 0.188 | 7.5 |
| 12 mm | — | — | 12 | 0.888 | 0.271 | 10.8 |
| 16 mm | — | — | 16 | 1.578 | 0.481 | 19.2 |
| 20 mm | — | — | 20 | 2.466 | 0.752 | 30.1 |
| 25 mm | — | — | 25 | 3.853 | 1.174 | 47.0 |

Standard mill length in Pakistan is **40 ft (12.19 m)**. Order in whole bars; cutting
waste is a real cost line, not a rounding error.

### 5.2 Steel content per volume of RCC (budgeting thumb rules)

| Element | kg per m³ RCC | ≈ reinforcement ratio | kg per 100 cft |
|---|---|---|---|
| Isolated / strip footings | 40–60 | 0.5–0.75% | 113–170 |
| Raft foundation | 80–120 | 1.0–1.5% | 227–340 |
| Plinth beams | 100–130 | 1.3–1.7% | 283–368 |
| Suspended slabs (one/two-way, 5"–6") | 80–100 | 1.0–1.3% | 227–283 |
| Beams | 110–140 | 1.4–1.8% | 311–396 |
| Columns | 140–180 | 1.8–2.3% | 396–510 |
| Staircase (waist slab + steps) | 100–120 | 1.3–1.5% | 283–340 |
| Lintels, chajjas, sunshades | 80–110 | — | 227–311 |
| Retaining / basement walls | 100–150 | — | 283–425 |

Steel density = 7,850 kg/m³. Ratio = (kg/m³) ÷ 7,850.

### 5.3 Steel per sqft of built-up area (top-down check only)

| Design character | kg/sqft covered area |
|---|---|
| Lean, short spans (≤ 14 ft), low seismic zone, single storey | 2.8 – 3.4 |
| Conventional 5/10 Marla double-storey RCC frame | **3.3 – 4.2** |
| Long spans (16–20 ft), cantilevers, Zone 3/4 seismic detailing | 4.2 – 5.5 |
| Basement, raft, heavy transfer elements | 5.5 – 7.0 |

**Calibration warning — read this before using any market thumb rule.**
Contractors and material dealers in Pakistan routinely quote "4.5–5.5 kg/sqft" as the
universal figure. A properly derived element-by-element takeoff for a conventional 10
Marla double-storey frame lands at **3.3–4.0 kg/sqft**. The gap is real and has three
causes: (a) locally over-designed sections, (b) seismic confinement detailing that many
takeoffs omit, (c) laps and wastage folded silently into the thumb rule. Do not average
the two. Use:

- **Thumb rule (4.5–5.5)** → early budget envelope and contingency sizing
- **Derived takeoff (3.3–4.2)** → the BOQ line you tender
- **Explain the delta in writing** in the estimate notes

Also discard the sometimes-quoted "columns = 5–8 kg per sqft of built-up area" rule. It is
internally inconsistent (it would make columns alone exceed the whole-structure figure).
Columns are 140–180 kg/m³ of *column concrete*, which for a typical house is 0.55–0.75
kg/sqft of built-up area.

### 5.4 Column reinforcement limits — ACI 318-19 §10.6.1.1

```
0.01 ≤ ρg = Ast / Ag ≤ 0.08
```

- **Minimum 1%** — below this, creep and shrinkage transfer too much load to concrete
- **Maximum 8%** — practical ceiling is ~4% because of lap congestion at floor level
- Economic residential range: **1.5–2.5%**
- Minimum bars: 4 in rectangular ties, 6 in spirals (ACI 318-19 §10.7.3.1)
- Ties (ORDINARY, non-seismic provisions only — see seismic override below): not less
  than #3 for longitudinal bars up to #10; spacing ≤ min(16 d_bar, 48 d_tie, least column
  dimension)

**Seismic override — do not stop at the ordinary tie-spacing rule above.** The
16d_bar/48d_tie/least-dimension spacing in §5.4 is ACI 318-19's *ordinary* (non-seismic)
provision. Most of Pakistan sits in a moderate-to-high seismic zone under BCP-SP-2007's
zoning map, which triggers **ACI 318-19 Chapter 18 special seismic detailing** —
substantially tighter confinement within the "lo" region at each column end: hoop/tie
spacing there drops to roughly `min(8 d_bar, 24 d_tie, 0.5× least column dimension, 6 in
(150 mm))`, with the lo length itself ≥ (clear height/6, largest column dimension, 18 in).
This is not an optional refinement — it is a code-mandated confinement zone that a
non-seismic tie schedule will silently omit. **Never quote or cost tie spacing from §5.4
alone without first confirming the site's seismic zone and whether Chapter 18 detailing
applies** — for any real column schedule, get the zone and the confinement detailing
confirmed by the structural engineer, not derived from this thumb-rule table. The
tonnage impact of this override is captured in §18.1's seismic-zone cost sensitivity
note (+5 to +12% on steel).

**Cost consequence:** a 9"×15" column at ρg = 1.5% carries 2.0 kg/ft of longitudinal
steel; at 2.5% it carries 3.4 kg/ft. Across 480 rft of column in a 10 Marla house that is
a **PKR 220,000 swing** at 2026 rates. Always ask which ratio the structural design used
before accepting a steel tonnage.

### 5.5 Laps, development length and hooks

| Item | Rule of thumb | Code basis |
|---|---|---|
| Tension lap splice | 40–50 d (use 50 d in seismic zones) | ACI 318-19 §25.5 |
| Compression lap | 40 d | ACI 318-19 §25.5.5 |
| Development length (straight, tension) | 40–50 d for Gr 60 in M20 | ACI 318-19 §25.4.2 |
| 90° standard hook extension | 12 d | ACI 318-19 §25.3.1 |
| 135° seismic hook extension | 6 d (≥ 3 in) | ACI 318-19 §25.3.4 |
| Clear cover — footings cast against soil | 75 mm (3") | ACI 318-19 §20.5.1.3 |
| Clear cover — columns, beams | 40 mm (1.5") | ACI 318-19 §20.5.1.3 |
| Clear cover — slabs (interior) | 20 mm (0.75") | ACI 318-19 §20.5.1.3 |
| Binding wire | 8–12 kg per tonne of steel | trade practice |

Note the same override as §5.4 applies here: the lap and hook figures above are the
general (non-seismic) ACI 318-19 provisions. In a Chapter 18 seismic-detailing zone, 135°
hooks (not 90°) are mandatory at confinement ties/stirrups, and lap locations are
restricted away from the lo confinement region at column ends — confirm both with the
structural engineer rather than budgeting straight from this table.

**Lap allowance for estimating:** add **4–6%** to the theoretical bar length for laps in a
low-rise frame (columns lap once per storey; slab bars lap in long dimensions). Add
another 3–5% wastage. So a schedule showing 10,000 kg theoretical becomes ~10,800–11,100
kg procured.

### 5.6 Grade selection and cost

| Grade | f_y | Typical residential use | Aug 2026 rate |
|---|---|---|---|
| Grade 40 | 40,000 psi / 280 MPa | Ties, stirrups, slab distribution steel, low-rise footings | ~PKR 260/kg |
| Grade 60 | 60,000 psi / 420 MPa | **Default for all main reinforcement** — columns, beams, slabs | ~PKR 265/kg |

The price delta between Gr 40 and Gr 60 is under 2%, while the strength delta is 50%.
**There is almost never an economic case for Gr 40 main steel in 2026.** If a contractor
proposes Gr 40 for main bars "to save money", that is a red flag (Section 15.5) — the
saving is negligible and the design almost certainly assumed Gr 60.

---

## Section 6: Masonry, Mortar & Plaster Quantities

### 6.1 Standard Pakistani brick and wall thicknesses

| Item | Value |
|---|---|
| Standard burnt clay brick | 9" × 4.5" × 3" (nominal, non-modular) |
| Mortar joint | 1/2" (10–12 mm) |
| Brick with joint | 9.5" × 5" × 3.5" |
| A-class brick crushing strength | ≥ 2,000 psi (load-bearing); B-class for non-structural only |
| **9" wall** | External walls, load-bearing walls, boundary walls, party walls, walls carrying lintels |
| **4.5" wall** | Non-structural internal partitions only — bath/store divisions, dwarf walls |
| 13.5" / 18" walls | Basement retaining, tall boundary walls, older load-bearing construction |

### 6.2 Brick counts — get this right, the market figures are unit-confused

| Basis | Count | Notes |
|---|---|---|
| **Per cft of brickwork, nominal (no mortar deduction)** | **13.5 bricks/cft** | 1728 in³ ÷ 121.5 in³ = 14.2, rounded down to the trade figure 13.5. Widely quoted; **conservative**, absorbs breakage. |
| **Per cft of brickwork, mortar-adjusted** | **10.4 bricks/cft** | 1728 in³ ÷ (9.5×5×3.5 = 166.25 in³). The theoretically correct count. |
| Per sqft of **9" wall** face (= 0.75 cft) | 7.8 ≈ **8 bricks/sqft** | mortar-adjusted; 10.1/sqft nominal |
| Per sqft of **4.5" wall** face (= 0.375 cft) | 3.9 ≈ **4 bricks/sqft** | mortar-adjusted; 5.1/sqft nominal |
| Per sqft of **13.5" wall** face (= 1.125 cft) | ≈ 12 bricks/sqft | |

**The "13.5 bricks per sqft" figure that circulates in Pakistani construction blogs is a
unit error.** It is 13.5 bricks per **cubic** foot, not per square foot. Using it per sqft
over-orders bricks by ~70%. Always state the unit explicitly in the BOQ line.

**Recommended practice:**
- **Costing/tender quantity:** 10.4 bricks/cft + 7% wastage = **11.2 bricks/cft**
- **Procurement order:** 13.5 bricks/cft (wastage already embedded) — the ~20% cushion
  covers breakage, cutting and the perennial short-count on brick truck deliveries
- Reconcile the two in the estimate notes rather than silently picking one

### 6.3 Mortar quantities

Mortar occupies **~25% of brickwork volume** for 9" walls with 1/2" joints
(~30% for 4.5" walls, more joints per unit volume).

**Per 100 cft of 9" brickwork:**

| Mortar mix | Wet mortar (cft) | Dry (× 1.30) | Cement (cft / bags) | Sand (cft) |
|---|---|---|---|---|
| 1:4 (rich — load-bearing, boundary) | 25 | 32.5 | 6.5 / **5.2** | 26.0 |
| **1:5 (standard 9" walls)** | 25 | 32.5 | 5.4 / **4.3** | 27.1 |
| 1:6 (economy internal) | 25 | 32.5 | 4.6 / **3.7** | 27.9 |

**Per 100 cft of 4.5" brickwork** (mortar 30%): 1:4 mix → cement **7.5 bags**, sand 30 cft.

*Cross-check against the field figure in circulation:* "380.5 sqft of 9" wall needs ~25
bags cement + 150 cft sand at 1:5". That wall is 380.5 × 0.75 = 285 cft of brickwork.
Scaling the table: 285 cft → 12.3 bags + 77 cft sand. The field figure is roughly **2×**
the calculated one, because it bundles in the plaster on both faces and a generous
site-loss allowance. Use the table for BOQ pricing; use the field figure only as an upper
procurement bound, and say which you used.

### 6.4 Plaster quantities

| Location | Thickness | Mix | Note |
|---|---|---|---|
| Internal walls | 1/2" (12 mm) | 1:4 or 1:5 | single coat + finishing |
| Ceilings (soffit of slab) | 3/8" (10 mm) | 1:4 | thinner — adhesion limit |
| External walls | 3/4" (20 mm) | 1:4 | two coats; 1:3 for parapets and exposed faces |
| Bathroom/kitchen below tile | 1/2" | 1:3 + waterproofing admixture | |

**Per 100 sqft of plaster:**

| Thickness | Mix | Wet vol (cft) | Dry (× 1.30) | Cement (bags) | Sand (cft) |
|---|---|---|---|---|---|
| 3/8" | 1:4 | 3.13 | 4.06 | **0.65** | 3.25 |
| 1/2" | 1:4 | 4.17 | 5.42 | **0.87** | 4.34 |
| 1/2" | 1:5 | 4.17 | 5.42 | **0.72** | 4.51 |
| 3/4" | 1:4 | 6.25 | 8.13 | **1.30** | 6.50 |
| 3/4" | 1:3 | 6.25 | 8.13 | **1.63** | 6.10 |

---

## Section 7: Element-by-Element Takeoff Formulas

| # | Element | Formula | Unit | Notes |
|---|---|---|---|---|
| 1 | Site clearance | plot area | sqft | includes dismantling, levelling |
| 2 | Excavation (footings) | Σ (L+2m)(B+2m)×D | cft | m = 0.5–1.0 ft working space; D from plinth level |
| 3 | Excavation (trenches) | L × W × D | cft | plinth beams, sewer lines |
| 4 | Backfilling | excavation vol − (PCC + footing + neck vol below GL) | cft | usually 55–70% of excavation |
| 5 | Surplus earth disposal | excavation − backfill | cft | + 25% bulking on the truck |
| 6 | PCC blinding | Σ (L+0.5)(B+0.5) × 0.25 | cft | 3" thick, 3" projection each side |
| 7 | Isolated footings | Σ L × B × D | cft | D = pad depth incl. any sloped portion |
| 8 | Column necks | Σ a × b × h_below_plinth | cft | |
| 9 | Columns | Σ a × b × h_clear × storeys | cft | h_clear = floor-to-floor − beam depth |
| 10 | Plinth beams | Σ L × w × d | cft | perimeter + internal grid lines |
| 11 | Beams | Σ L × w × (D − t_slab) | cft | deduct slab thickness — do NOT double-count |
| 12 | Slab | covered area × t | cft | t = 5" (0.4167 ft) typical; 6" for spans > 16 ft |
| 13 | Staircase | (waist slab: L_incl × w × t) + (steps: ½ × R × T × w × n) | cft | R = riser, T = tread, n = steps |
| 14 | Lintels | Σ (opening width + 2×bearing) × w × d | cft | bearing = 9" each side |
| 15 | Chajja / sunshade | Σ L × projection × avg t | cft | |
| 16 | Parapet | perimeter × height × thickness | cft | 4.5" × 3 ft typical |
| 17 | Brickwork 9" | (gross wall area − openings) × 0.75 | cft | |
| 18 | Brickwork 4.5" | (gross area − openings) × 0.375 | cft | |
| 19 | DPC | wall length × wall thickness | sqft | 1.5"–2" 1:2:4 with waterproofing compound |
| 20 | Internal plaster | (wall faces − openings) + ceiling area | sqft | see §3.3 multiplier |
| 21 | External plaster | elevation area − openings + reveals | sqft | |
| 22 | Shuttering | contact area of all RCC | sqft | slab soffit + beam sides/soffit + column faces |
| 23 | Roof treatment | roof area + upstands | sqft | mud-phuska/screed + membrane/tiles |
| 24 | Flooring | floor area − openings | sqft | separate line per material |
| 25 | Skirting | room perimeter − door widths | rft | 4"–6" high |
| 26 | Doors/windows | count by type & size | no. + sqft | schedule them; do not lump |
| 27 | Paint | plaster area × coats spec | sqft | |
| 28 | Sanitary points | count fixtures | no. | 1 point ≈ 1 supply + 1 waste connection |
| 29 | Electrical points | count switches/sockets/lights/fans | no. | 8–12 points per 100 sqft typical |
| 30 | Boundary wall | length × height × thickness | cft | + footing + plaster + coping |

**The #11/#12 double-count trap:** measuring beams full-depth *and* the slab across the
full covered area counts the beam-slab overlap twice. Either (a) deduct slab thickness
from beam depth, or (b) deduct beam plan area from slab area. Pick one, state it in the
notes. This error typically inflates RCC by 4–7%.

---

## Section 8: Pakistan Market Rates — August 2026

### 8.1 Rate confidence tiers

| Tier | Meaning | How to treat |
|---|---|---|
| **A** | Researched from market data, August 2026 | Use directly; re-verify if estimate is > 60 days old |
| **B** | Derived arithmetically from Tier A inputs | Use; recompute if a Tier A input moves |
| **C** | Typical range, not independently sourced at this date | **Must be verified locally before issuing an estimate.** Marked `[verify]` |

**Read this before trusting any total built from this section.** Scan Sections 8.2–9.3:
the overwhelming majority of individual line rates — nearly all bricks, sand, crush,
binding wire, bitumen, most labour trades (foreman, plumber, electrician, tile layer),
and most composite trade rates in §9.3 — are tagged **Tier C `[verify]`**, meaning
"typical range, not independently sourced," not "confirmed current price." Only cement,
steel, unskilled/skilled-labour daily wage and the headline composite grey/turnkey
per-sqft bands carry Tier A. This matters most for the Section 11 worked example: its
arithmetic is exact to the rupee, but a large share of the unit rates feeding it are
Tier C placeholders. **Precision of the output does not imply verification of the
inputs** — treat every total derived through this section as provisional until the
Tier C rates in it have been re-priced against a real local quotation.

### 8.2 Basic material rates

| Material | Rate | Tier | Notes |
|---|---|---|---|
| **Cement, OPC 50 kg bag — national** | PKR 1,500 – 1,610 | A | |
| Cement — Karachi / Sindh | PKR 1,350 – 1,550 | A | closer to the plants |
| Cement — Lahore / Islamabad / Rawalpindi | PKR 1,400 – 1,560 | A | |
| **Steel Gr 60 deformed bar (saria)** | PKR 265/kg (258–265) | A | ≈ PKR 265,000/tonne |
| **Steel Gr 40 deformed bar** | PKR 260/kg | A | |
| A-class burnt clay brick | PKR 20 – 28 each (PKR 20,000–28,000/1,000) | C `[verify]` | wide regional spread; kiln-gate vs delivered differs by PKR 2–4 |
| Sand — Ravi / Chenab (masonry & concrete) | PKR 60 – 110 /cft | C `[verify]` | |
| Sand — Lawrencepur / sweet sand (plaster) | PKR 130 – 200 /cft | C `[verify]` | |
| Crush — Margalla / Sargodha 3/4" | PKR 110 – 170 /cft | C `[verify]` | |
| Crush — 1/2" (slab/beam) | PKR 120 – 180 /cft | C `[verify]` | |
| Binding wire | PKR 300 – 360 /kg | C `[verify]` | |
| Bitumen / waterproofing membrane | PKR 150 – 320 /sqft | C `[verify]` | spec-dependent |

### 8.3 Labour rates

| Trade | Daily wage (urban) | Tier |
|---|---|---|
| Unskilled labourer (mazdoor) | PKR 1,200 – 1,500 | A |
| Skilled mason (raaj) / carpenter / steel fixer | PKR 1,600 – 2,000 | A |
| Foreman / mistri | PKR 2,200 – 3,000 | C `[verify]` |
| Plumber / electrician (skilled) | PKR 1,800 – 2,500 | C `[verify]` |
| Tile layer / marble fitter | PKR 2,000 – 2,800 | C `[verify]` |

Karachi and Islamabad sit at the top of these bands; smaller cities and rural sites at the
bottom. Labour is **22–30% of grey structure cost** and **30–38% of finishing cost**.

### 8.4 Composite rates — PKR per sqft of covered area

| Package | Rate (PKR/sqft) | Tier | Includes |
|---|---|---|---|
| **Grey structure (with material)** | **2,800 – 3,500** | A | Bills 1–7 + MEP rough-in. Up to 3,800 in premium sectors / difficult sites. Bottom of band 2,650 for lean spec. |
| Grey structure — labour only (thekedari) | 600 – 950 | C `[verify]` | ≈ 22–30% of grey with-material |
| **Finishing — economy** | 2,400 – 3,000 | B | basic ceramic tile, flush doors, ordinary sanitary |
| **Finishing — A-category** | 3,000 – 5,300 | B | branded tile/marble, solid-wood doors, wardrobes, false ceiling |
| **Finishing — premium** | 6,000 – 11,000 | B | imported marble, custom joinery, imported fixtures, smart wiring |
| **Turnkey — economy** | 5,200 – 5,800 | A/B | |
| **Turnkey — A-category** | **5,800 – 8,800** | A | the mainstream band; 6,700–8,800 is typical for a well-finished house |
| **Turnkey — premium** | 10,000 – 15,000 | A | |

**Always attach the covered area to a per-sqft rate.** A rate without a defined covered
area (does it include mumty? terraces? porch? basement? boundary wall?) is meaningless and
is the #1 cause of disputes between homeowners and contractors.

### 8.5 Area inclusion convention (state this explicitly in every estimate)

| Space | Count as covered area | Weight |
|---|---|---|
| Enclosed habitable rooms, kitchen, baths, lobby, stairs | Yes | 100% |
| Mumty / stair head room | Yes | 100% |
| Covered car porch | Yes | 50–60% |
| Open terrace with slab below | Yes | 40–50% |
| Balcony / cantilevered | Yes | 50% |
| Open lawn, driveway | No | priced as external works |
| Boundary wall | No | priced per rft separately |
| Underground water tank / septic | No | priced as a lump item |

---

## Section 9: Composite Rates & Unit Rate Build-Up

### 9.1 The unit rate formula

```
Unit Rate = Material + Labour + Plant/Equipment + Transport & Handling
            + Overhead (8–12%) + Profit (8–15%) + Taxes/Levies
```

Overhead covers site office, supervision, scaffolding, security, water, temporary power,
insurance. Profit is a separate, negotiable line — **never let a contractor bury profit
inside the material rate**; it makes the quote un-auditable.

### 9.2 Worked build-up: RCC M20 in columns, per m³

| Component | Quantity | Rate | Amount (PKR) |
|---|---|---|---|
| Cement | 8.06 bags | 1,550 | 12,493 |
| Sand | 14.8 cft | 90 | 1,332 |
| Crush 1/2" | 29.7 cft | 130 | 3,861 |
| Water, curing | lump | — | 350 |
| Shuttering (contact area) | 12 m² | 350/m² | 4,200 |
| Mixing, placing, vibrating, curing labour | 2.5 man-days | 1,700 | 4,250 |
| Mixer + vibrator hire | 0.4 day | 3,500/day | 1,400 |
| **Direct subtotal** | | | **27,886** |
| Overhead @ 10% | | | 2,789 |
| Profit @ 12% | | | 3,681 |
| **Unit rate — concrete only, excl. steel** | | | **≈ 34,356 /m³ ≈ PKR 973 /cft** |
| Steel (separate BOQ line) | 160 kg | 310 in-place | 49,600 /m³ |
| **All-in column RCC incl. steel** | | | **≈ 83,956 /m³ ≈ PKR 2,378 /cft** |

### 9.3 Composite rate quick table (concrete-only, steel priced separately)

| Item | PKR/cft | Tier | Shuttering intensity |
|---|---|---|---|
| Excavation (mixed machine + manual) | 30 – 45 | C `[verify]` | — |
| Backfill & compaction | 15 – 25 | C `[verify]` | — |
| PCC 1:4:8 | 380 – 460 | B | nil |
| RCC M20 — footings | 600 – 720 | B | low |
| RCC M20 — plinth beams | 720 – 850 | B | medium |
| RCC M20 — columns | 820 – 980 | B | high |
| RCC M20 — beams + slab | 720 – 870 | B | medium-high |
| RCC M20 — staircase | 850 – 1,050 | B | very high |
| Brickwork 9", 1:5 mortar | 480 – 570 | B | — |
| Brickwork 4.5", 1:4 mortar | 560 – 680 | B | — |

| Item | PKR/sqft | Tier |
|---|---|---|
| Steel in place (material + cut/bend/fix/binding wire) | 300 – 325 **per kg** | B |
| Internal plaster 1/2" 1:5 | 75 – 100 | B |
| External plaster 3/4" 1:4 | 95 – 130 | B |
| Shuttering (if priced separately) | 30 – 45 | C `[verify]` |
| Roof treatment (screed + membrane + tile) | 150 – 260 | C `[verify]` |
| Ceramic floor tile, laid | 320 – 550 | C `[verify]` |
| Porcelain / imported tile, laid | 550 – 1,100 | C `[verify]` |
| Marble (Badal/Ziarat), laid & polished | 600 – 1,600 | C `[verify]` |
| Emulsion paint, 2 coats + primer + putty | 45 – 70 | C `[verify]` |
| Weathershield exterior paint | 60 – 95 | C `[verify]` |
| Gypsum false ceiling | 260 – 420 | C `[verify]` |
| Aluminium / uPVC window, glazed | 750 – 1,400 | C `[verify]` |
| MS grill, fabricated & painted | 700 – 1,200 | C `[verify]` |
| Electrical (complete, per sqft covered) | 180 – 280 | C `[verify]` |
| Plumbing rough-in (per sqft covered) | 130 – 210 | C `[verify]` |

---

## Section 10: Cost Breakdown Structure

### 10.1 Grey vs finishing split — the master ratio

| Split | Share of total build cost |
|---|---|
| **Grey structure** (Bills 1–7 + MEP rough-in) | **55 – 65%** |
| **Finishing** (Bills 8–15, incl. MEP finishing) | **35 – 45%** |

Drivers of where you land in that band:

| Condition | Pushes grey share |
|---|---|
| Economy finishes, basic tile, flush doors | ↑ toward 65% |
| Premium marble, imported fixtures, custom joinery | ↓ toward 50% or below |
| Long spans, basement, raft, high seismic zone | ↑ |
| Simple rectangular plan, short spans | ↓ |
| Steel/cement price spike | ↑ |

### 10.2 Pakistan-calibrated breakdown, % of total build cost (excl. land)

**Read this table as two mutually exclusive groups that sum to ~100% — Grey and
Finishing. MEP is not a third group to add on top: MEP rough-in (conduiting, pipework)
is already counted inside the Grey subtotal, and MEP finishing (wiring/fixtures,
plumbing fixtures/pumps) is already counted inside the Finishing subtotal. Do not also
add a separate "MEP total" line when reconciling a budget — that double-counts the
rough-in figure and will overstate the total by roughly 10 points.**

| Group | Item | % of total |
|---|---|---|
| **Grey** | Preliminaries & site establishment | 2 – 4 |
| | Earthwork & substructure (excavation, PCC, footings, plinth) | 6 – 10 |
| | Superstructure RCC — concrete (columns, beams, slabs, stairs) | 14 – 18 |
| | Reinforcement steel | 14 – 19 |
| | Masonry (9" + 4.5") | 6 – 9 |
| | Plaster & rendering | 4 – 6 |
| | Roof treatment & waterproofing | 2 – 3 |
| | MEP rough-in (conduiting + plumbing pipework) | 4 – 6 |
| | **Grey subtotal** | **55 – 65** |
| **Finishes** | Flooring — tile / marble | 8 – 12 |
| | Woodwork — doors, wardrobes, kitchen cabinets | 7 – 11 |
| | Paint & false ceiling | 4 – 7 |
| | Sanitary & kitchen fixtures/fittings | 4 – 7 |
| | Windows & glazing (aluminium / uPVC) | 2 – 4 |
| | Steel fabrication — grills, railings, main gate | 2 – 4 |
| | Elevation / facade | 3 – 6 |
| | External works, boundary finish, driveway | 2 – 5 |
| | Electrical finishing (wiring, DB, fixtures, fans) | 3 – 5 |
| | Plumbing finishing (pumps, tanks, connections) | 1 – 3 |
| | **Finishes subtotal (incl. MEP finishing)** | **35 – 45** |

**For reference only, not additive to the table above:** total MEP across both stages
(rough-in inside Grey + finishing inside Finishes) typically runs **8 – 14% of total
build cost**. Quote this figure only when someone asks "how much is MEP altogether" —
never re-add it to a Grey + Finishes total, since it is already contained within both.

### 10.3 International benchmark (for cross-reference only)

| Group | International share | Pakistan equivalent | Why they differ |
|---|---|---|---|
| Land & site prep | 10 – 20% | typically excluded; site prep 1–3% | land priced separately in PK practice |
| Foundation & structural | 20 – 30% | **34 – 43%** (concrete + steel + masonry) | PK uses RCC frame vs timber framing; steel is import-priced |
| Interior finishes | 30 – 40% | 30 – 40% | comparable |
| MEP / mechanical | 10 – 15% | 10 – 15% | comparable; PK has no central HVAC in most homes |
| Miscellaneous | 5 – 10% | 5 – 10% | comparable |

Do **not** substitute the international framing/exterior-finish percentages (framing
16.6%, exterior finishes 13.4%, foundations 10.4%, site work 7.6%) into a Pakistani
estimate. They describe timber-framed North American housing and will understate RCC and
steel by a factor of two.

### 10.4 Finishing sub-breakdown — 10 Marla reference

| Finishing item | PKR range | % of finishing |
|---|---|---|
| Tiles / marble | 1,200,000 – 1,800,000 | 20 – 24 |
| Woodwork (doors + cabinets) | 800,000 – 1,200,000 | 15 – 18 |
| Paint & false ceiling | 500,000 – 700,000 | 9 – 11 |
| Kitchen & bath fixtures | 700,000 – 1,000,000 | 12 – 15 |
| Electrical & plumbing finishing | 500,000 – 700,000 | 9 – 11 |
| Windows, grills, railings, gate | 900,000 – 1,400,000 | 15 – 18 |
| Elevation + external works | 700,000 – 1,200,000 | 12 – 15 |
| **Total finishing** | **4,000,000 – 5,500,000** *(basic)* to **8,000,000** *(A-category)* | 100 |

---

## Section 11: Worked Example — 10 Marla Double-Storey, Lahore/Islamabad, 2026

**Before using this example as a template:** as flagged in §8.1, most of the unit rates
below are Tier C `[verify]` typical ranges, not independently sourced prices. The
arithmetic is exact; the inputs are not yet verified. Treat every PKR figure in this
section as illustrative of *method*, and re-price the Tier C inputs locally before
quoting any total from it as a real budget.

### 11.1 Scope definition

| Parameter | Value |
|---|---|
| Plot | 10 Marla = 2,250 sqft |
| Ground floor covered | 1,650 sqft |
| First floor covered | 1,450 sqft |
| Mumty / stair head | 180 sqft |
| **Total covered area** | **3,280 sqft** |
| Structure | RCC frame, isolated footings, 9" infill masonry, 5" slabs |
| Soil | Normal firm, SBC ≈ 1.5 kg/cm² |
| Spec | A-category finishing |
| Programme | 14 months |
| Excluded | Land, basement, lift, solar, furniture, landscaping beyond driveway |

### 11.2 Concrete takeoff

| Element | Calculation | cft |
|---|---|---|
| Footings (20 nos, 6'×6'×1.25') | 20 × 45 | 900 |
| Columns GF + FF (20 nos, 9"×15", 12 ft each floor) | 2 × 20 × 0.75 × 1.25 × 12 | 450 |
| Plinth beams 9"×15", 340 rft | 340 × 0.9375 | 319 |
| GF beams 9"×18", 300 rft, measured **full depth** | 300 × 0.75 × 1.5 | 338 |
| GF slab 5", **net of beam plan area** (1,650 − 225) | 1,425 × 0.4167 | 594 |
| FF beams 9"×18", 260 rft, full depth | 260 × 0.75 × 1.5 | 293 |
| FF slab 5", net of beam plan area (1,450 − 195) | 1,255 × 0.4167 | 523 |
| Mumty roof slab + beams | 75 + 60 | 135 |
| Staircase (2 flights × 2 levels) | — | 220 |
| **Total RCC** | | **3,772 cft (106.8 m³)** |
| PCC 1:4:8 under footings, 3" | 20 × 6.5 × 6.5 × 0.25 | 220 |

**Double-count method declared:** beams are measured at full 18" depth and the slab is
measured *net of beam plan area* — method (b) of the §7 trap. Measuring beams full-depth
**and** the slab across the whole covered area would have added 175 cft (**+4.6%**), which
is precisely the error §7 warns about. State which method you used, every time.

*Check:* 3,772 cft ÷ 3,280 sqft = **1.15 cft RCC/sqft** — inside the 1.10–1.40 band (§3.3). ✔

### 11.3 Steel takeoff

**Reminder before pricing this table:** the column reinforcement ratio and the tie
spacing used to sustain the kg/m³ figures below assume the ratios and *ordinary*
(non-seismic) confinement in §5.2/§5.4. Confirm the site's seismic zone and whether
Chapter 18 confinement applies before treating this as more than a budgeting estimate —
seismic detailing can add 5–12% to the steel line (§5.4, §18.1).

| Element | cft | m³ | kg/m³ | kg |
|---|---|---|---|---|
| Footings | 900 | 25.5 | 50 | 1,275 |
| Columns | 450 | 12.7 | 160 | 2,032 |
| Plinth + all beams (319 + 338 + 293 + 60) | 1,010 | 28.6 | 120 | 3,432 |
| Slabs (594 + 523 + 75) | 1,192 | 33.8 | 95 | 3,211 |
| Staircase | 220 | 6.2 | 110 | 682 |
| **Subtotal (theoretical)** | | | | **10,632** |
| Laps + wastage @ 3.5% | | | | 372 |
| **Procurement steel** | | | | **≈ 11,000 kg = 11.0 t** |

*Concrete cross-check:* 900 + 450 + 1,010 + 1,192 + 220 = **3,772 cft** — reconciles with
§11.2. Every cft of RCC must appear in exactly one steel row; a steel table that does not
sum back to the concrete takeoff has either lost or double-counted an element.

*Check:* 11,000 ÷ 3,280 = **3.35 kg/sqft** — inside the derived-takeoff band (3.3–4.2),
below the market thumb rule (4.5–5.5). Flag the delta per §5.3.

### 11.4 Masonry & finishes takeoff

| Item | Gross | Net factor | Net | Unit |
|---|---|---|---|---|
| 9" walls (ext GF 1,870 + ext FF 1,760 + int 400) | 4,030 sqft | × 0.78 | 3,143 sqft = **2,357 cft** | |
| 4.5" partitions | 1,060 sqft | × 0.85 | **900 sqft = 338 cft** | |
| Internal plaster | 3,280 × 2.5 | — | **8,200 sqft** | |
| External plaster | 3,280 × 1.1 | — | **3,600 sqft** | |
| Flooring | 3,280 × 0.92 | — | **3,000 sqft** | |
| Roof treatment | GF terrace + FF roof + mumty | — | **1,830 sqft** | |
| Paint (int + ext) | 8,200 + 3,600 | — | **11,800 sqft** | |

### 11.5 Priced BOQ — grey structure

**All rates below carry the Tier from §8/§9 that produced them; the majority are Tier B
(derived) or Tier C (`[verify]`) — re-price locally before quoting this total as final.**

| # | Item | Qty | Unit | Rate | Amount (PKR) |
|---|---|---|---|---|---|
| 1.01 | Site establishment, water, scaffolding, security | 1 | LS | 250,000 | 250,000 |
| 2.01 | Excavation incl. working space | 4,200 | cft | 35 | 147,000 |
| 2.02 | PCC 1:4:8, 3" | 220 | cft | 420 | 92,400 |
| 2.03 | DPC, termite proofing, misc | 1 | LS | 180,000 | 180,000 |
| 3.01 | RCC M20 — footings | 900 | cft | 650 | 585,000 |
| 3.02 | RCC M20 — columns | 450 | cft | 880 | 396,000 |
| 3.03 | RCC M20 — plinth beams | 319 | cft | 780 | 248,820 |
| 3.04 | RCC M20 — GF beams + slab | 932 | cft | 780 | 726,960 |
| 3.05 | RCC M20 — FF beams + slab | 816 | cft | 780 | 636,480 |
| 3.06 | RCC M20 — mumty | 135 | cft | 800 | 108,000 |
| 3.07 | RCC M20 — staircase | 220 | cft | 900 | 198,000 |
| 4.01 | Reinforcement Gr 60, cut/bent/fixed | 11,000 | kg | 310 | 3,410,000 |
| 5.01 | Brickwork 9", 1:5 mortar | 2,357 | cft | 520 | 1,225,640 |
| 5.02 | Brickwork 4.5", 1:4 mortar | 900 | sqft | 230 | 207,000 |
| 6.01 | Internal plaster 1/2" | 8,200 | sqft | 85 | 697,000 |
| 6.02 | External plaster 3/4" | 3,600 | sqft | 110 | 396,000 |
| 7.01 | Roof treatment & waterproofing | 1,830 | sqft | 180 | 329,400 |
| 11.01 | Plumbing rough-in, sewerage, tanks | 1 | LS | 550,000 | 550,000 |
| 12.01 | Electrical conduiting & earthing | 1 | LS | 320,000 | 320,000 |
| | **GREY STRUCTURE SUBTOTAL** | | | | **10,703,700** |

**Grey rate = 10,703,700 ÷ 3,280 = PKR 3,263 /sqft** — inside the 2,800–3,500 band. ✔
As a lump sum this is PKR 1.07 Crore, at the top of the published Lahore band of
PKR 85 Lac – 1.0 Crore for a 10 Marla double-storey grey structure — correct, because
3,280 sqft is at the upper end of the 2,900–3,300 sqft covered-area range those figures
assume.

### 11.6 Priced BOQ — finishing (A-category)

| # | Item | Qty | Unit | Rate | Amount (PKR) |
|---|---|---|---|---|---|
| 9.01 | Floor tile / marble, laid & polished | 3,000 | sqft | 550 | 1,650,000 |
| 8.01 | Solid-wood / semi-solid doors, 14 nos | 14 | no. | 45,000 | 630,000 |
| 8.02 | Wardrobes + kitchen cabinets | 1 | LS | 700,000 | 700,000 |
| 8.03 | Aluminium / uPVC windows, glazed | 420 | sqft | 950 | 399,000 |
| 10.01 | Paint, int + ext, primer + putty + 2 coats | 11,800 | sqft | 55 | 649,000 |
| 10.02 | Gypsum false ceiling | 600 | sqft | 320 | 192,000 |
| 11.02 | Sanitary fixtures & fittings, 4 baths | 4 | no. | 160,000 | 640,000 |
| 11.03 | Kitchen sink, fittings, chimney, hob | 1 | LS | 250,000 | 250,000 |
| 11.04 | Plumbing finishing, pumps, UG/OH tanks | 1 | LS | 350,000 | 350,000 |
| 12.02 | Electrical wiring, DB, switches, fans, lights | 3,280 | sqft | 210 | 688,800 |
| 13.01 | MS grills | 500 | sqft | 900 | 450,000 |
| 13.02 | Main gate | 1 | no. | 180,000 | 180,000 |
| 13.03 | Stair & balcony railing | 1 | LS | 220,000 | 220,000 |
| 14.01 | Elevation — cladding, tiles, cornice | 1 | LS | 600,000 | 600,000 |
| 15.01 | Tuff tile driveway, boundary finish, misc external | 1 | LS | 400,000 | 400,000 |
| | **FINISHING SUBTOTAL** | | | | **7,998,800** |

### 11.7 Summary, soft costs, contingency and escalation

| Line | Amount (PKR) | Note |
|---|---|---|
| Grey structure | 10,703,700 | 57.2% of build cost |
| Finishing | 7,998,800 | 42.8% |
| **Build cost subtotal** | **18,702,500** | PKR 5,702/sqft |
| Professional & statutory @ 6% (architect 4%, structural 1%, approvals/NOC/utilities 1%) | 1,122,150 | §14 |
| **Subtotal** | **19,824,650** | |
| Contingency @ 7% (complete construction drawings) | 1,387,726 | §13.1 |
| Escalation: 19.82M × 0.58 material share × 12%/yr × 0.583 yr (½ of 14 months) | 804,421 | §13.3 |
| **GRAND TOTAL** | **≈ PKR 22,016,800 ≈ 2.20 Crore** | |
| **All-in rate** | **PKR 6,712 /sqft** | inside the 6,700–8,800 turnkey band ✔ |

### 11.8 Triangulation check

| Method | Calculation | Result | Δ |
|---|---|---|---|
| A — Composite rate | 3,280 sqft × 5,750/sqft | 18.86 M | +0.85% |
| B — Detailed BOQ | grey 10.70 M + finishing 8.00 M | 18.70 M | baseline |
| C — Ratio build-up | grey 10.70 M ÷ 0.572 | 18.71 M | +0.05% |

All three within 1% — the estimate is internally consistent and safe to issue as a
planning budget (with the Section-0 caveats attached). Had they diverged by more than
10%, the correct response is to find the broken method, **not** to average them. Note
that this internal consistency check validates the *arithmetic*, not the underlying
Tier C rates (§8.1) — a set of consistently-wrong inputs will triangulate just as
cleanly as a set of correct ones.

### 11.9 Master material procurement schedule

| Material | Derivation | Quantity |
|---|---|---|
| **Cement** | RCC 3,772 cft × 0.224 = 845 bags; internal plaster 8,200 sqft @ ½" 1:5 = 59; external plaster 3,600 sqft @ ¾" 1:4 = 47; brick mortar 2,695 cft @ 1:5 = 117; PCC = 21; flooring bed, DPC & misc = 120 | **≈ 1,210 bags (60.5 t)** |
| **Steel Gr 60** | §11.3 | **11.0 tonnes** |
| **Bricks** | (2,357 + 338) cft × 13.5 (procurement basis, §6.2) | **≈ 37,000 nos** |
| **Sand** | RCC 1,584 + brick mortar 730 + plaster 604 + PCC 104 | **≈ 3,050 cft** |
| **Crush** | RCC 3,168 + PCC 208 | **≈ 3,400 cft** |

*Cement cross-check:* thumb rule 0.4 bags/sqft × 3,280 sqft = **1,312 bags** vs derived
**1,210 bags** — 8% apart. Two independent methods agreeing inside 10% is a strong signal
the takeoff is sound. ✔ (The thumb rule sits high because it silently embeds site loss.)

*Brick cross-check:* 37,000 ÷ 3,280 = 11.3 bricks/sqft of covered area — inside the
typical 10–12 range for a double-storey house. ✔

*Core-five material cost:* cement 1,210 × 1,550 = 1.88M + steel 11,000 × 265 = 2.92M +
bricks 37,000 × 24 = 0.89M + sand 3,050 × 90 = 0.27M + crush 3,400 × 130 = 0.44M
= **PKR 6.40M = 60% of grey structure cost**. If a contractor's material
component falls outside 55–70% of their grey figure, ask why.

---

## Section 12: Plot-Size Calibration Benchmarks (2026)

| Plot | Covered area (double-storey) | Grey structure | Turnkey economy | Turnkey A-category | Turnkey premium |
|---|---|---|---|---|---|
| **3 Marla** (675 sqft) | 900 – 1,100 sqft | 28 – 38 Lac | 50 – 62 Lac | 62 – 90 Lac | 95 Lac – 1.4 Cr |
| **5 Marla** (1,125 sqft) | 1,350 – 1,600 sqft | **42 – 52 Lac** | **70 – 90 Lac** | 90 Lac – 1.10 Cr | 1.10 – 1.50 Cr |
| **7 Marla** (1,575 sqft) | 2,000 – 2,350 sqft | 60 – 78 Lac | 1.05 – 1.30 Cr | 1.30 – 1.70 Cr | 1.90 – 2.90 Cr |
| **10 Marla** (2,250 sqft) | 2,900 – 3,300 sqft | **85 Lac – 1.05 Cr** | **1.40 – 1.80 Cr** | 1.80 – 2.50 Cr | 2.90 – 4.50 Cr |
| **1 Kanal** (4,500 sqft) | 5,800 – 7,000 sqft | 1.75 – 2.35 Cr | 3.00 – 3.80 Cr | 3.80 – 5.20 Cr | 6.00 – 9.50 Cr |
| **2 Kanal** (9,000 sqft) | 11,000 – 13,500 sqft | 3.30 – 4.50 Cr | 5.70 – 7.30 Cr | 7.30 – 10.0 Cr | 11.5 – 18.0 Cr |

*Single-storey reduces covered area by ~50% but grey PKR/sqft rises 8–15% (foundations and
site costs amortise over less area).*

### 12.1 Reconciling contradictory published figures

Published sources routinely disagree by 30–50% on "the cost of a 10 Marla house". They are
not necessarily wrong — they are measuring different things. Before comparing any two
published figures, normalise both:

| Published figure | Implied covered area | Implied PKR/sqft grey | Interpretation |
|---|---|---|---|
| "10 Marla Islamabad grey: PKR 5.5 – 7.0 M" | ~2,000 – 2,300 sqft | 2,750 – 3,050 | **Single-storey or ground + partial first floor** |
| "10 Marla Lahore grey: PKR 85 Lac – 1.0 Cr" | ~2,900 – 3,300 sqft | 2,930 – 3,030 | **Full double-storey** |

Both resolve to the same PKR/sqft. **The rule: never compare lump sums. Reduce every
figure to PKR/sqft over an explicitly stated covered area first.** If a source does not
state its covered area, it cannot be used as a benchmark.

---

## Section 13: Contingency, Escalation & Allowances

### 13.1 Contingency by design maturity

| Design stage / condition | Contingency | Rationale |
|---|---|---|
| Concept sketch / napkin, no drawings | **20 – 25%** | scope itself is uncertain |
| Schematic design, preliminary BOQ | **15 – 20%** | quantities ±20% |
| Design development, most details resolved | **10 – 15%** | |
| **Complete construction documents, known site** | **5 – 10%** | industry standard for new build |
| Complete docs + firm subcontract prices + fully documented site | **3 – 5%** | floor — never go below 3% |
| Renovation / retrofit / addition to existing structure | **10 – 15%** minimum | hidden conditions |
| Renovation with unknown structural condition or no as-builts | **20 – 25%** | |

**Contingency reduces as design certainty increases.** Carry the higher figure at concept
stage and formally release the difference at each design milestone — do not silently keep
25% and treat the unused portion as profit or slack.

### 13.2 Contingency is not a slush fund

| Contingency covers | Contingency does NOT cover |
|---|---|
| Quantity variation within defined scope | Client scope changes (that's a variation order) |
| Minor unforeseen site conditions | Major geotechnical surprises (that's a separate risk allowance) |
| Small rate variations | Material price escalation (that's escalation, §13.3) |
| Coordination gaps between trades | Design errors requiring rework (that's professional liability) |
| Weather delays within normal range | Force majeure |

Track contingency drawdown as a visible line. A project 40% complete that has spent 80% of
its contingency is in trouble and must be re-forecast, not carried forward on hope.

### 13.3 Escalation allowance

Pakistan's construction market has seen double-digit annual movement in cement and steel.
Escalation is a **separate line from contingency** and must be sized against the
material-weighted portion of the cost over the *midpoint* of the programme:

```
Escalation = Base Cost × Material Share × Annual Inflation Rate × (Duration_years ÷ 2)
```

| Input | Typical residential value |
|---|---|
| Material share of total cost | 0.55 – 0.62 |
| Annual material inflation (2026 planning assumption) | 10 – 15% `[verify against current SPI/WPI]` |
| Duration ÷ 2 | half of the construction programme in years |

**Worked:** PKR 19.82 M base × 0.58 × 12% × 0.583 yr = **PKR 804,000 ≈ 4.1%**.

| Programme length | Typical escalation allowance |
|---|---|
| ≤ 6 months | 2 – 3% |
| 9 – 12 months | 3 – 5% |
| 15 – 24 months | 6 – 9% |
| > 24 months | 10%+ and insist on an indexed price-adjustment clause |

**Hedge alternative:** for cement and steel — 30% of the build cost and the two most
volatile items — front-loading procurement or locking a supplier rate at contract signing
often beats carrying an escalation allowance. Cost that decision explicitly (storage,
working capital, deterioration risk) rather than defaulting to it.

### 13.4 Allowances, provisional sums and PC items

| Type | Definition | Estimating treatment |
|---|---|---|
| **Provisional sum** | Work defined in scope but not yet specified (e.g. "landscaping — PKR 400,000") | Carry at face value; reconcile against actual on completion |
| **Prime cost (PC) item** | Client-selected material at a nominated supply rate (e.g. "floor tile PC PKR 450/sqft supply") | Laying labour is measured separately; only the supply rate is provisional |
| **Allowance** | Placeholder for a decision not yet made (kitchen, wardrobes, light fittings) | State the allowance clearly and warn that overruns are the client's, not the contractor's |
| **Dayworks** | Work priced at labour + material + % on instruction | Cap it; never leave dayworks open-ended |

The three most commonly under-allowed items in Pakistani residential projects, in order:
**(1) kitchen — cabinets, counters, appliances; (2) elevation/facade; (3) external works
— boundary wall finish, driveway, gate, lawn.** Together they routinely add 12–18% that
was never in the original number.

---

## Section 14: Soft Costs, Approvals & Taxes

| Item | Typical | Notes |
|---|---|---|
| Architectural design & drawings | 3 – 6% of build cost | lower % on larger projects |
| Structural design + BBS | 0.5 – 1.5% | **non-negotiable — this is the PEC-stamped work** |
| MEP design (if separate) | 0.3 – 0.8% | usually bundled in architecture for residential |
| Site supervision / project management | 3 – 6% | or a monthly retainer |
| Authority map approval fee (LDA/CDA/RDA/DHA) | varies by plot size & zone `[verify]` | includes scrutiny, sewerage, and completion fees |
| Building/completion certificate | lump `[verify]` | required before utility meters in most authorities |
| Utility connections — electricity (LESCO/IESCO/K-Electric) | demand notice, load-dependent `[verify]` | |
| Utility connections — Sui gas, water & sewerage | lump `[verify]` | gas connections currently restricted in many areas — budget LPG/electric alternative |
| Provincial sales tax on construction services | reduced-rate regime applies in Punjab/Sindh/ICT `[verify with an accountant]` | rate and input-adjustment rules change with each finance bill |
| Income tax withholding on contract payments (Income Tax Ordinance §153) | filer/non-filer rates differ substantially `[verify]` | withhold correctly or the liability lands on the client |
| **Total soft cost allowance** | **5 – 9% of build cost** | use 6% as a planning default |

**Never fold soft costs into the PKR/sqft build rate.** They are a separate tier of the
budget, they escalate differently, and clients consistently forget them — which is exactly
why projects "come in over budget" when the construction itself was on target.

---

## Section 15: Sanity-Checking a Contractor Quote

### 15.1 The seven-step audit

```
1. NORMALISE SCOPE      → force the quote onto your inclusions/exclusions checklist
2. NORMALISE AREA       → confirm the covered area definition (§8.5); recompute PKR/sqft
3. PARETO TAKEOFF       → independently measure the 5 items carrying ~80% of value
4. DECOMPOSE UNIT RATES → material + labour + plant + OH + profit; check each is plausible
5. TEST FOR BALANCE     → compare each item's % of total against the §10.2 benchmarks
6. AUDIT MARKUP & CONTINGENCY → validate separately from base cost, never as one blob
7. BENCHMARK            → compare against comparable completed projects, as a reasonableness
                          check only — never as a substitute for the takeoff
```

### 15.2 The Pareto five

In a residential BOQ, five items carry ~80% of the value. Measure these independently and
you have audited most of the quote:

| # | Item | Typical share | Independent check |
|---|---|---|---|
| 1 | Reinforcement steel | 14 – 19% | tonnage ÷ covered area → must be 3.3–5.5 kg/sqft (§5.3) |
| 2 | RCC concrete | 14 – 18% | cft ÷ covered area → must be 1.10–1.40 cft/sqft (§3.3) |
| 3 | Flooring (tile/marble) | 8 – 12% | sqft ÷ covered area → must be 0.88–0.95 (§3.3) |
| 4 | Masonry + plaster | 10 – 15% | brickwork cft ÷ covered area → 0.75–0.95 (§3.3) |
| 5 | Woodwork | 7 – 11% | count doors and running feet of cabinetry — no lump sums accepted |

### 15.3 Variance thresholds vs your independent estimate

| Variance | Verdict | Action |
|---|---|---|
| within **±7%** | Normal estimating spread | Accept |
| **+8 to +15%** | Scope creep, premium spec, or fatter markup | Itemise the delta line by line; negotiate |
| **> +15%** | Not reconcilable by normal spread | Demand the contractor's backup takeoff; retender |
| **−8 to −15%** | Investigate before celebrating | Check exclusions, steel grade, cement brand, brick class, mortar mix |
| **< −15%** | **Red flag** | Almost always missing scope, front-loaded cashflow, or claim-driven bidding. The gap will reappear as variation orders. |

### 15.4 Unbalanced-bid detection

Compare each BOQ item's percentage of the contractor's total against the §10.2 benchmark
range:

```
Flag if:  item_% > 1.5 × benchmark_upper   AND   the item occurs early in the programme
```

Front-loading (over-pricing excavation, PCC, footings; under-pricing finishes) is a
cashflow tactic: the contractor recovers most of their money in the first 30% of the
programme and has little incentive to finish. Counter it with a milestone payment schedule
tied to **verified physical completion**, not to BOQ line drawdown (§16.3).

### 15.5 Red-flag checklist

Any one of these means the quote is not yet auditable — send it back:

- [ ] A lump-sum "civil works" or "structure complete" line with no quantities
- [ ] Steel quoted without **grade** (Gr 40 vs Gr 60) or **mill/brand**
- [ ] Concrete quoted without **mix ratio** or grade
- [ ] Bricks quoted without **class** (A vs B) — B-class in load-bearing walls is a safety issue, not just a cost one
- [ ] Mortar and plaster mix ratios unstated
- [ ] Quantities given with no unit, or with "sqft" where "cft" is meant (§6.2)
- [ ] Covered area not defined, or porch/terrace/mumty inclusion unstated
- [ ] Wastage not disclosed, or wastage buried inside the unit rate
- [ ] Overhead and profit not shown as separate lines
- [ ] Escalation and contingency merged into a single "misc" percentage
- [ ] "As per site" or "as per requirement" against a priced item
- [ ] No exclusions list at all — the absence of exclusions is itself the warning
- [ ] Steel quantity below 3.0 kg/sqft or above 6.0 kg/sqft with no structural justification
- [ ] Grey structure below PKR 2,600/sqft in a 2026 quote — either the spec is being cut or the price will move

### 15.6 The plausibility band table

Fast triage on any residential quote:

| Metric | Plausible | Interrogate | Reject without explanation |
|---|---|---|---|
| Grey PKR/sqft | 2,800 – 3,500 | 2,600–2,800 or 3,500–3,800 | < 2,600 or > 4,200 |
| Turnkey PKR/sqft (A-category) | 5,800 – 8,800 | 5,200–5,800 or 8,800–10,000 | < 5,000 |
| Grey share of total | 55 – 65% | 50–55% or 65–70% | < 45% or > 75% |
| Steel kg/sqft | 3.3 – 5.0 | 3.0–3.3 or 5.0–6.0 | < 2.8 or > 6.5 |
| RCC cft/sqft | 1.10 – 1.40 | 1.00–1.10 or 1.40–1.60 | < 0.95 or > 1.75 |
| Cement bags/sqft | 0.36 – 0.45 | 0.32–0.36 or 0.45–0.50 | < 0.30 or > 0.55 |
| Bricks per sqft covered | 10 – 12 | 9–10 or 12–14 | < 8 or > 16 |
| Material share of grey cost | 55 – 70% | 50–55% or 70–75% | outside 45–80% |
| Overhead | 8 – 12% | 12–15% | > 18% |
| Profit | 8 – 15% | 15–20% | > 22% |

---

## Section 16: Contract Types & Payment Schedules

### 16.1 The three common Pakistani arrangements

| Model | Contractor supplies | Client supplies | Client risk | When to use |
|---|---|---|---|---|
| **Labour-rate (thekedari)** | Labour + tools only | All materials | **High** — client manages procurement, storage, theft, wastage | Client has time, market knowledge, and a trusted supervisor. Saves 10–18% if run well; loses more than that if run badly. |
| **Grey structure with material** | Everything for Bills 1–7 | Finishing separately | Medium | The mainstream choice. Structure is standardised and easy to specify; finishing is where taste and cost blow out, so the client keeps control of it. |
| **Turnkey (with material)** | Everything to handover | Nothing | **Low** | Client is time-poor or remote. Costs 8–15% more but transfers wastage, escalation and coordination risk. Requires a *very* tight specification annexure or the contractor optimises the spec downward. |

### 16.2 What must be annexed to any residential contract

1. Approved architectural + structural drawings (dated, revision-numbered)
2. The priced BOQ with quantities and rates — **not just a total**
3. Material specification schedule: cement brand, steel mill and grade, brick class, tile
   make/series/size, sanitary brand/model, paint brand and system, wire gauge and brand
4. Explicit inclusions and exclusions list
5. Covered-area definition and measurement method (§8.5)
6. Payment schedule tied to physical milestones (§16.3)
7. Variation order procedure and rate basis for extras
8. Programme with milestone dates and a liquidated-damages clause
9. Retention and defect liability period
10. Price-adjustment / escalation clause if programme > 12 months

### 16.3 Milestone payment schedule — grey structure

| Milestone | % | Cumulative |
|---|---|---|
| Mobilisation advance (against bank guarantee or material on site) | 10 | 10 |
| Excavation, PCC, footings, plinth beams complete + backfilled | 15 | 25 |
| Ground floor columns + GF roof slab cast & cured | 20 | 45 |
| First floor columns + FF roof slab cast & cured | 20 | 65 |
| Masonry (both floors) + mumty + parapet complete | 15 | 80 |
| Internal + external plaster + roof treatment complete | 10 | 90 |
| Grey completion, site cleared, snag list closed | 5 | 95 |
| **Retention released after defect liability period (6–12 months)** | 5 | 100 |

**Rules:** never pay ahead of physical progress; verify each milestone on site (or by
dated photographs with a scale reference) before releasing; hold 5% retention through the
defect liability period — waterproofing and plumbing failures surface in the first monsoon,
not at handover.

### 16.4 Finishing payment schedule

Finishing is trade-by-trade, not milestone-by-storey. Pay each trade on its own completion:
flooring, joinery, painting, electrical, plumbing, aluminium, steel fabrication. Hold 10%
per trade until the whole-house snag list is signed off — a painter paid in full will not
return to fix what the electrician damaged.

---

## Section 17: FreeCAD / BIM → BOQ Extraction

### 17.1 Model hygiene prerequisites

A BIM model only produces a trustworthy BOQ if it was built to produce one. Before
extraction, verify (see `architecture-freecad-bim`):

- Real spatial hierarchy: Site → Building → Storey → elements
- Every element carries a correct `IfcType` (`Wall`, `Slab`, `Column`, `Beam`, `Footing`,
  `Stair`, `Window`, `Door`, `Railing`)
- Openings are **live Subtractions**, not frozen boolean cuts — otherwise wall volumes are
  wrong and, worse, silently wrong
- No overlapping solids at beam–slab and column–beam junctions (the §7 double-count trap
  reappears here as geometric overlap)
- Materials assigned per element so concrete grades can be separated

### 17.2 Volume takeoff script

```python
# FreeCAD Python console — element volume takeoff bucketed by IfcType
import FreeCAD as App
from collections import defaultdict

doc = App.ActiveDocument
buckets = defaultdict(float)
counts  = defaultdict(int)

for o in doc.Objects:
    if not hasattr(o, "Shape") or o.Shape.isNull():
        continue
    if o.Shape.Volume <= 0:
        continue
    ifc = (getattr(o, "IfcType", None)
           or getattr(o, "IfcRole", None)
           or "Unclassified")
    buckets[ifc] += o.Shape.Volume / 1e9   # FreeCAD internal unit is mm -> m3
    counts[ifc]  += 1

print(f"{'IfcType':<22}{'nos':>5}{'m3':>12}{'cft':>12}")
for k in sorted(buckets, key=lambda x: -buckets[x]):
    m3 = buckets[k]
    print(f"{k:<22}{counts[k]:>5}{m3:>12.3f}{m3*35.3147:>12.1f}")

unclassified = counts.get("Unclassified", 0)
if unclassified:
    print(f"\nWARNING: {unclassified} objects have no IfcType — "
          f"their volume is NOT allocated to any BOQ bill.")
```

### 17.3 Area takeoff script (plaster, paint, flooring, shuttering)

```python
# Face-area takeoff: vertical faces -> wall/plaster area; horizontal -> floor/ceiling
import FreeCAD as App

doc = App.ActiveDocument
vert_m2 = horiz_m2 = 0.0
for o in doc.Objects:
    if not hasattr(o, "Shape") or o.Shape.isNull():
        continue
    for f in o.Shape.Faces:
        try:
            n = f.normalAt(0, 0)
        except Exception:
            continue
        a = f.Area / 1e6                       # mm2 -> m2
        if abs(n.z) > 0.9:
            horiz_m2 += a
        elif abs(n.z) < 0.1:
            vert_m2 += a

print(f"Vertical face area   : {vert_m2:8.1f} m2  ({vert_m2*10.7639:9.0f} sqft)")
print(f"Horizontal face area : {horiz_m2:8.1f} m2  ({horiz_m2*10.7639:9.0f} sqft)")
print("NOTE: raw face areas include internal/hidden faces. Reconcile against the "
      "§3.3 multipliers before using in a BOQ.")
```

### 17.4 Model → BOQ mapping

| IfcType | BOQ bill | Conversion |
|---|---|---|
| `Footing` | 3.01 | m³ × 35.3147 → cft; steel @ 40–60 kg/m³ |
| `Column` | 3.02 | cft; steel @ 140–180 kg/m³; shuttering = perimeter × height |
| `Beam` | 3.03/3.04 | cft; steel @ 110–140 kg/m³ — verify no slab overlap |
| `Slab` | 3.04 | cft; steel @ 80–100 kg/m³; soffit area = shuttering |
| `Stair` | 3.07 | cft; steel @ 100–120 kg/m³ |
| `Wall` (9" / 4.5") | 5.01/5.02 | cft; bricks @ 10.4–13.5/cft; mortar per §6.3 |
| `Window` / `Door` | Bill 8 | count + sqft; **their subtraction must already be reflected in wall volume** |
| `Railing` | 13.03 | rft |
| `Roof` | 7.01 | plan area sqft |

### 17.5 Extraction discipline

**A model-derived quantity is a first draft, not a BOQ.** Always:

1. Cross-check model RCC cft ÷ covered area against 1.10–1.40 (§3.3)
2. Cross-check model brickwork cft ÷ covered area against 0.75–0.95
3. Reconcile against a hand takeoff of at least two elements
4. List every `Unclassified` object and resolve it — unallocated volume is missing money
5. Never issue a BOQ from a model that has not passed steps 1–4

---

## Section 18: Standards, Codes & Rate Schedules

### 18.1 Governing codes

| Code | Scope | Relevance to this skill |
|---|---|---|
| **Building Code of Pakistan — Seismic Provisions 2007 (BCP-SP-2007)** | Seismic design of RCC, steel, masonry and timber buildings. Issued by the Ministry of Housing & Works / Pakistan Engineering Council, developed with NESPAK and input from ICC and ACI. | Seismic zone determines confinement detailing, tie spacing and lap lengths → drives steel tonnage. Confirm the site's zone from the code's zoning map before accepting a steel quantity. |
| **Building Code of Pakistan 2021 (BCP-2021)** | Updated, broader code based on IBC-2021; supersedes/extends BCP-2007. | The current reference for new design submissions where the authority has adopted it. |
| **ACI 318-19** — *Building Code Requirements for Structural Concrete* | RC member design; the substantive basis for Pakistani RCC practice. | §10.6.1.1 column ρg 1–8% (ordinary provisions); Chapter 18 special seismic detailing supersedes ordinary tie spacing/hooks in seismic zones (§5.4/§5.5); §10.7.3.1 minimum bars; §20.5.1.3 cover; §25.3 hooks; §25.4 development length; §25.5 lap splices; Ch. 22 sectional strength. |
| **IBC 2021** | Reference basis for BCP-2021. | Occupancy, egress, and load provisions carried into BCP-2021. |
| **ASTM A615 / A615M** | Deformed carbon-steel bars, Grade 40 and Grade 60. | The grades local mills certify against; demand mill test certificates. |
| **ASTM C150 Type I** (locally PS 232 for OPC `[verify current edition]`) | Ordinary Portland Cement. | Brand and type must be named in the BOQ. |
| **Local authority byelaws** — LDA / CDA / RDA / SBCA / DHA / TMA | Setbacks, FAR, covered-area limits, height, parking, submission requirements. | Determine the legally permissible covered area — which is the denominator of every PKR/sqft figure in this skill. |

**Seismic-zone cost sensitivity:** moving a design from a low seismic zone to a higher one
adds confinement ties, tighter stirrup spacing, longer laps and often larger sections —
typically **+5 to +12% on steel tonnage** and +2 to +5% on concrete. This is the same
Chapter 18 override flagged in §5.4/§5.5 — confirm the zone from BCP-SP-2007's zoning map
for the specific site; do not assume from the city name alone, and have the structural
engineer state the zone used and whether special seismic detailing applies on the
drawings.

### 18.2 Official rate schedules

| Schedule | Issuer | Use |
|---|---|---|
| **MRS — Market Rates System** | Finance Department, Government of Punjab; issued periodically (typically half-yearly) | Benchmark composite rates for public-sector work; useful as a floor/ceiling reference for private work. Always use the current issue. `[verify current edition]` |
| **CSR — Composite Schedule of Rates** | Provincial works departments | Item descriptions and analysis-of-rates methodology worth borrowing even for private BOQs |
| **NHA General Specifications** | National Highway Authority | Specification language for earthwork, concrete and materials |

These are public-works instruments. Private residential rates typically run **above** MRS
for finishing trades and **near or below** MRS for bulk civil items. Use them for
methodology and item wording, and market enquiry for the actual price.

---

## Section 19: Common Estimating Errors

| # | Error | Consequence | Fix |
|---|---|---|---|
| 1 | Beam depth measured full while slab measured over full area | RCC +4–7% | Deduct slab thickness from beam depth (§7) |
| 2 | "13.5 bricks per **sqft**" | Bricks +70% | It is per **cft** (§6.2) |
| 3 | Per-sqft rate quoted without defining covered area | Disputes, 10–25% argument | Always attach the area definition (§8.5) |
| 4 | Wastage folded into the measured quantity | Contractor paid for bricks that were never laid | Two columns: measured vs procurement (§3.4) |
| 5 | Contingency and escalation merged | Neither can be managed or released | Separate lines (§13) |
| 6 | Steel taken purely from a thumb rule | ±35% on 15% of project cost | Element takeoff (§5.2), thumb rule as check only (§5.3) |
| 7 | Soft costs folded into the build rate | "Over budget" on an on-target build | Separate tier (§14) |
| 8 | Kitchen, elevation and external works under-allowed | +12–18% late in the project | Allow explicitly (§13.4) |
| 9 | Stale rates quoted as current | Systematic understatement in an inflating market | Date-stamp every rate; re-verify > 60 days (§8.1) |
| 10 | Comparing published lump sums across sources | Apparent 30–50% "disagreement" that isn't real | Normalise to PKR/sqft first (§12.1) |
| 11 | Accepting a quote that is 15% low | Variation orders recover the gap and then some | Investigate low bids harder than high ones (§15.3) |
| 12 | No opening deductions in masonry/plaster | Masonry +20–28% | Apply §3.1/§3.2 |
| 13 | Model volumes taken without checking `Unclassified` objects | Silent missing scope | Run the warning check (§17.2) |
| 14 | Nominal mix used above M25 | Strength not achieved, structural risk | Design mix + trial cubes above M25 (§4.1) |
| 15 | Sand measured wet, priced dry | Sand +20–30% overpaid | Apply the bulking correction (§4.2) |
| 16 | Grey structure paid ahead of physical progress | No leverage at finishing stage | Milestone verification + 5% retention (§16.3) |
| 17 | Laps treated as wastage (or omitted entirely) | Steel −4–6% | Schedule laps; wastage on top (§5.5) |
| 18 | Single-point estimate with no range | False precision, no risk conversation | Always issue a range plus the base case |
| 19 | Ordinary (non-seismic) tie spacing used in a seismic zone | Under-confined columns, structural risk, understated steel | Confirm zone + Chapter 18 applicability before costing ties (§5.4/§5.5) |
| 20 | MEP rough-in double-counted against a separate "MEP total" line | Budget overstated by ~10 points of total cost | Grey vs Finishes are the only additive groups; MEP is a cross-reference only (§10.2) |

---

## Section 20: Output Templates

### 20.1 BOQ line template

```
| Item  | Description                                        | Unit | Qty   | Rate | Amount |
|-------|----------------------------------------------------|------|-------|------|--------|
| 3.02  | Providing and laying RCC 1:1.5:3 (M20) in columns, |      |       |      |        |
|       | incl. formwork, mixing, placing, vibrating, curing |      |       |      |        |
|       | and finishing; reinforcement paid under Bill 4.    | cft  |   450 |  880 | 396,000|
```

### 20.2 Estimate summary sheet

```
PROJECT              : <name>            LOCATION : <city / sector>
PLOT                 : <Marla/Kanal>     COVERED AREA : <sqft>  (definition: §8.5 basis)
SPEC LEVEL           : economy / A-category / premium
RATE BASIS DATE      : <YYYY-MM-DD>      PROGRAMME : <months>
PREPARED BY          : <name>            STATUS : PLANNING ESTIMATE — NOT FOR CONSTRUCTION

A.  Grey structure  (Bills 1-7 + MEP rough-in)              PKR ____________   (__%)
B.  Finishing       (Bills 8-15, incl. MEP finishing)       PKR ____________   (__%)
C.  BUILD COST SUBTOTAL (A+B)                               PKR ____________
    → per sqft                                              PKR ______ /sqft
D.  Professional & statutory @ __%                          PKR ____________
E.  SUBTOTAL (C+D)                                          PKR ____________
F.  Contingency @ __%   (design stage: ____________)        PKR ____________
G.  Escalation  @ __%   (matl share __, infl __%, T/2 __)   PKR ____________
H.  GRAND TOTAL (E+F+G)                                     PKR ____________
    → all-in per sqft                                       PKR ______ /sqft

TRIANGULATION   A: composite ______   B: BOQ ______   C: ratio ______   max Δ ___%
EXCLUSIONS      : land, ______________________________________________
ASSUMPTIONS     : ____________________________________________________
RATE CONFIDENCE : Tier A items ___%   Tier C [verify] items ___%
NOTE: MEP is already inside A (rough-in) and B (finishing) — do not add a third MEP line.

MANDATORY NOTE  : This is a planning estimate. Structural design must be sealed by a
                  PEC-registered engineer and drawings approved by <authority> before
                  construction. Rates are dated <date> and require re-verification.
```

### 20.3 Contractor quote comparison sheet

```
| Metric                    | Benchmark      | Contractor A | Contractor B | Verdict |
|---------------------------|----------------|--------------|--------------|---------|
| Covered area basis (sqft) | <your figure>  |              |              |         |
| Grey PKR/sqft             | 2,800-3,500    |              |              |         |
| Turnkey PKR/sqft          | 5,800-8,800    |              |              |         |
| Grey share of total       | 55-65%         |              |              |         |
| Steel kg/sqft             | 3.3-5.0        |              |              |         |
| RCC cft/sqft              | 1.10-1.40      |              |              |         |
| Cement bags/sqft          | 0.36-0.45      |              |              |         |
| Bricks per sqft           | 10-12          |              |              |         |
| Overhead shown separately | yes            |              |              |         |
| Profit shown separately   | yes            |              |              |         |
| Exclusions list provided  | yes            |              |              |         |
| Steel grade named         | Gr 60          |              |              |         |
| Cement brand named        | yes            |              |              |         |
| Brick class named         | A-class        |              |              |         |
| Variance vs own estimate  | ±7%            |              |              |         |
| Red flags (§15.5 count)   | 0              |              |              |         |
```

---

## Quick Reference Card

```
UNITS        1 m3 = 35.3147 cft | 1 m2 = 10.7639 sqft | 1 bag = 50 kg = 1.25 cft
             1 Marla = 225 sqft | 1 Kanal = 4,500 sqft | 1 Lac = 100k | 1 Crore = 10M

CONCRETE     dry factor 1.54 | mortar dry factor 1.30
             M20 (1:1.5:3) per m3  : 8.06 bags + 14.8 cft sand + 29.7 cft crush
             M20 per 100 cft       : 22.4 bags + 42 cft sand + 84 cft crush
             M15 (1:2:4) per 100cft: 17.6 bags + 44 cft sand + 88 cft crush

STEEL        W = d^2/162 kg/m | 7,850 kg/m3 | bar length 40 ft
             #3=0.171 #4=0.303 #5=0.473 #6=0.681 #8=1.211  kg/ft
             footings 40-60 | slabs 80-100 | beams 110-140 | columns 140-180  kg/m3
             ACI 318-19 10.6.1.1 (ordinary): 1% <= rho_g <= 8%  (economic 1.5-2.5%)
             SEISMIC ZONES: Ch.18 confinement overrides ordinary tie spacing/hooks —
             verify zone before costing ties (see 5.4/5.5/18.1)
             laps +4-6%, wastage +3-5%

MASONRY      13.5 bricks/CFT nominal | 10.4 bricks/cft with mortar
             9" wall = 0.75 cft/sqft = ~8 bricks/sqft | 4.5" = 0.375 cft/sqft = ~4/sqft
             mortar = 25% of 9" brickwork volume | 1:5 std, wastage 5-10%

RATIOS/SQFT  RCC 1.10-1.40 cft | brickwork 0.75-0.95 cft | steel 3.3-5.0 kg
             cement 0.36-0.45 bags | bricks 10-12 nos | int plaster x2.4-2.7
             ext plaster x1.0-1.2 | paint x3.4-3.8 | flooring x0.88-0.95

RATES 2026   MOSTLY TIER C [verify] — cement/steel/labour daily-wage are Tier A;
             bricks/sand/crush/most trade rates are unverified typical ranges (8.1)
             cement 1,500-1,610/bag | steel Gr60 265/kg, Gr40 260/kg
             labour 1,200-2,000/day | steel in place 300-325/kg
             GREY 2,800-3,500/sqft | TURNKEY 5,800-8,800/sqft | PREMIUM 10,000-15,000

SPLIT        grey 55-65% (incl. MEP rough-in) | finishing 35-45% (incl. MEP finishing)
             MEP total (both stages, reference only, NOT additive) ~8-14%
             soft costs +5-9% on top of build cost

RISK         contingency: concept 20-25% | schematic 15-20% | full docs 5-10% | floor 3%
             escalation  = base x matl_share(0.58) x infl x (months/24)

AUDIT        triangulate 3 methods within 10% | Pareto-5 items = 80% of value
             variance +-7% accept | >+15% retender | <-15% RED FLAG
             no grade/mix/class named = not auditable, send it back

ALWAYS       state covered-area definition | date-stamp rates | separate contingency
             from escalation | flag Tier C [verify] rates | issue a RANGE not a point
             SAY IT UNPROMPTED: PEC-stamped structural design + authority approval
             required before construction. This is a planning estimate only.
```
