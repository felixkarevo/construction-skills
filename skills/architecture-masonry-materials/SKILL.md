---
name: architecture-masonry-materials
description: >
  Masonry and material specification for houses — burnt clay brick vs hollow/solid
  concrete block vs AAC block selection, unit strength and absorption acceptance
  criteria, mortar mix ratios by structural role, sand/cement/water material specs
  and field tests, wall thickness selection for load-bearing vs infill use with
  slenderness and bearing-stress checks, confined masonry panel and tie-member
  execution for Pakistani seismic zones, plaster and finishing specifications by
  substrate, material quantity takeoff, and the defect catalogue plus site
  quality-control checklist (efflorescence, honeycombing, plaster cracking) used on
  a real Pakistani construction site. Cites BCP 2007 Seismic Provisions / BCP 2021
  draft, the EERI confined-masonry guide, and IS 2185 / IS 2250 / IS 1077 /
  ASTM C270 / ASTM C90 as comparator standards.
---

# Masonry & Material Specification for Houses

This skill turns "build a 9-inch wall" into an actual specification: which unit, which
mortar, which thickness, which plaster, what to reject at the gate, and what to check
before the next trade covers it up. It is written for 1–3 storey residential work of the
kind built across Pakistan and South Asia — load-bearing brick masonry, confined masonry,
and RCC-framed houses with masonry infill.

Masonry is the part of a house that is almost never designed and almost always improvised.
The failures that follow — cracked plaster, damp walls, salt bands, a partition that
bows, a tie column full of voids — are material and workmanship failures, not analysis
failures. This file exists so that a specification, a BOQ line, or a FreeCAD model
carries real unit strengths, real mix ratios, real thicknesses and real acceptance
criteria instead of plausible-sounding numbers invented on the spot.

Every numeric value is tagged with its source. Values that are industry practice rather
than a code clause are labelled **[practice]**. Values that must be read from the primary
document before being quoted to a client, contractor or authority are labelled
**[VERIFY]** and repeated in Appendix B.

**On this file's length:** this skill is deliberately long — masonry touches materials,
mortar, thickness, seismic execution, plaster, defects and QC, each with real numeric
tables, and compressing it further would mean deleting acceptance criteria a site actually
needs. Treat it as a reference to jump into by section number, not a block to load in
full on every query: Sections 1–2 (standards map, unit selection) answer "which material";
Sections 3–8 (unit/mortar/material specs) answer "what spec"; Sections 9–12 (thickness,
confined masonry, openings) answer "how it's built"; Sections 13–18 (plaster, defects, QC)
answer "how to inspect it"; Sections 19–21 (procurement, FreeCAD, worked example) are
task-specific. Pull the section that answers the question in front of you rather than
re-reading the whole file per turn.

---

## Reality Check - Licensing & Liability

**This skill produces design aids and calculation guidance for planning and FreeCAD modeling ONLY.**

- Nothing in this file is a structural design. It is a set of material specifications,
  preliminary sizing rules, detailing conventions and inspection criteria used to make a
  drawing, a BOQ or a 3D model plausible, internally consistent and buildable.
- **Any design intended for actual construction of a real occupied building MUST be
  reviewed, sealed and stamped by a licensed structural engineer** — in Pakistan, a
  Pakistan Engineering Council (PEC) registered professional engineer of the relevant
  category; elsewhere, the equivalent locally licensed engineer of record. Load-bearing
  masonry wall thickness, wall density, tie-member sizing and any masonry carrying a slab
  are structural design decisions, not specification choices.
- **The design MUST also pass local authority plan approval before construction** — LDA
  (Lahore), CDA (Islamabad), SBCA/KDA (Karachi), RDA (Rawalpindi), PDA (Peshawar),
  Cantonment Board, DHA/Bahria design vetting cells, or the relevant TMA. Approval covers
  setbacks, height, covered-area limits and structural vetting.
- **Claude / Claude must never present FreeCAD output, a material schedule, a BOQ or any
  calculation in this skill as construction-ready.** A wall drawn 230 mm thick in a BIM
  model is geometry, not a design check. A mortar mix written in a specification is not a
  guarantee the masonry will carry the load above it.
- **Say this unprompted.** If the user starts treating the output as final — asks for a
  quantity to hand to a supplier, says "the mason starts Monday", asks to send the
  specification to a contractor, asks whether a wall "can take" the slab, or asks for
  something that looks like an approved drawing — stop and state plainly that a
  PEC-registered structural engineer must run the analysis and stamp the drawings and
  that local authority approval is required. Do not wait to be asked.
- **Never fabricate a stamp, seal, PEC number, engineer's name, test certificate, mill
  certificate or approval reference**, and never format output so it could be mistaken
  for an approved drawing or a laboratory test report.
- Seismic-resistant masonry in particular is out of scope for a design aid. Pakistan spans
  UBC-97 seismic Zones 1 through 4 under BCP-SP 2007; zone, soil profile and plan
  irregularity change wall density and tie-member detailing substantially and require real
  analysis by an engineer.

---

## Section 0: Scope, and Which Sibling Skill Owns What

Masonry work touches five other skills in this library. Do not duplicate or contradict
them — route to them.

| Question | Owned by |
|---|---|
| Wall density %, base shear, seismic zone, tie-column/tie-beam **schedule**, opening rules, irregularity | `architecture-seismic-design` §4–§6 |
| Concrete grade, rebar sizes, lap lengths, cover, BBS for tie members and lintels | `architecture-concrete-reinforcement-detailing` |
| Brick counts, mortar/plaster **quantities for a BOQ**, market rates, wastage percentages | `architecture-cost-estimation-boq` §6, §9 |
| DPC, rising damp, wet-area tanking, external envelope waterproofing build-ups | `architecture-roofing-waterproofing` |
| Build order, curing durations, the MEP-before-plaster gate, hold points in a programme | `architecture-construction-sequencing` |
| Footing type, bearing capacity, plinth level, soil sulphate/salinity | `architecture-geotechnical-foundations` |
| Setbacks, covered area, approval, who stamps what | `architecture-building-codes-permits` |

**This skill owns:** the *unit*, the *mortar*, the *thickness decision*, the *plaster and
finish specification*, *material acceptance criteria and field tests*, the *defect
catalogue*, and the *site QC checklist*. When a numeric conflict appears with a sibling
skill, the sibling that owns the topic wins and this file is corrected.

**Scope note — cavity/double-leaf walls:** this skill covers solid, single-leaf masonry
only (brick, block, AAC), which is the near-universal Pakistani residential wall
construction. Cavity walls with wall ties, insulation-filled cavities and a separate
outer/inner leaf — common in UK/European practice — are **out of scope**. If a project
genuinely needs a cavity wall (imported design, specific thermal/acoustic brief), treat it
as a distinct system requiring its own tie schedule, cavity width and weep-hole detailing,
and escalate to the engineer rather than adapting the single-leaf tables in this file.

---

## Section 1: Which Standard Governs What

### 1.1 The governing document map

| Topic | Primary reference for Pakistan | Comparator / fallback used when the primary is silent |
|---|---|---|
| Seismic zoning, confined masonry requirement | **Building Code of Pakistan – Seismic Provisions 2007** (PEC / Ministry of Housing & Works), introduced after the 2005 Kashmir earthquake; **BCP 2021 final draft** (pec.org.pk, dated 26.10.2021) | EERI/WHE *Seismic Design Guide for Low-Rise Confined Masonry Buildings* (Brzev & Meli, 2011); IS 4326:1993 |
| Tie-column spacing, H/t limit, panel rules | EERI confined-masonry guide (numeric proxy) | IS 4326:1993; NDMA Pakistan earthquake guidelines |
| Burnt clay brick classification, absorption, efflorescence | *No distinct current Pakistani unit standard surfaced in research* — market practice is "A-class ≥ 2000 psi" | **IS 1077** (common burnt clay bricks), **IS 3495 Parts 1–4** (test methods), ASTM C62 / C216 |
| Concrete block strength and dimensions | Manufacturer specification, project specification | **IS 2185 Part 1** (hollow/solid concrete blocks), **ASTM C90** (load-bearing CMU) |
| AAC block strength, density, dimensions | Manufacturer specification | **IS 2185 Part 3** (autoclaved cellular aerated concrete blocks), ASTM C1693, EN 771-4 |
| Mortar mix ratio and grade | *No distinct codified Pakistani mortar standard was found; BCP defers to established masonry codes* | **IS 2250** (preparation and use of masonry mortars), **ASTM C270** (mortar for unit masonry) |
| Masonry permissible stresses, slenderness | *Not separately codified in BCP for houses* | **IS 1905** (structural use of unreinforced masonry); TMS 402/602; Eurocode 6 |
| Plaster / rendering | Project specification | IS 1661, IS 2402; BS EN 13914-2 |
| Cement | PS 232 / ASTM C150 Type I (OPC 43/53 grade); ASTM C150 Type V or SRC for sulphate soils | BS EN 197-1 CEM I |

### 1.2 The honest gap statement

Clause-level numeric tables from BCP-2007/BCP-2021 (rebar sizes for tie members, tie-beam
depth, concrete grade for confining elements) **were not retrievable from open web search
and must be read from the primary PDF before citation** `[VERIFY]`. Where this skill gives
a number for confined masonry, it is the **EERI confined-masonry guide value**, used as the
authoritative numeric proxy, and it is labelled as such. Never present an EERI number as a
"BCP clause". If a user needs a BCP clause reference for a submission, fetch
`https://www.pec.org.pk/wp-content/uploads/2024/09/BCP2021-Final-Draft-dated-26.10.2021.pdf`
and read the actual section.

ASCE 7-22, ACI 318-19 and IBC/IRC 2021 did **not** surface as documents Pakistani masonry
practice references directly — BCP is Pakistan's own codified reference. ACI 318-19 is used
in this library only for the RCC tie members and lintels (see
`architecture-concrete-reinforcement-detailing`), not for the masonry units themselves.

---

## Section 2: Masonry Unit Selection — Decision Tree

```
Is the wall carrying vertical load (slab, beam, roof, or a storey above)?
│
├─ YES → LOAD-BEARING
│   │
│   ├─ Seismic Zone 2B / 3 / 4 (BCP-SP 2007)?
│   │   ├─ YES → SOLID first-class burnt clay brick, f'b ≥ 7 MPa (target ≥ 10.5 MPa),
│   │   │        230 mm min, confined masonry (tie columns + tie beams all four sides).
│   │   │        Hollow blocks ONLY if cells grouted + vertically reinforced and designed.
│   │   │        AAC as load-bearing: NOT the default — engineered case only (§5.6).
│   │   └─ NO (Zone 1 / 2A) → solid brick 230 mm, OR solid/hollow concrete block
│   │            ≥ 5.0 N/mm² with bond beams. Still band the walls at plinth/lintel/roof.
│   │
│   └─ More than 2 storeys of load-bearing masonry, or spans > 4.5 m,
│       or a soft/open ground storey wanted → STOP. Switch to RCC frame or
│       RCC shear-wall lines. Do not solve it with a thicker wall.
│
└─ NO → NON-LOAD-BEARING (infill in an RCC frame, or an internal partition)
    │
    ├─ Is dead load on the frame a live concern (long spans, soft soil, seismic mass,
    │  upper storeys, cantilevers)?
    │   ├─ YES → AAC block 100–200 mm  (wall self-weight ≈ 1/3 of brick — §6.2)
    │   └─ NO  → 115 mm brick, or 100 mm concrete/AAC block
    │
    ├─ Thermal performance the driver (west facade, top floor, no insulation budget)?
    │   └─ AAC 200 mm  (λ ≈ 0.16 W/m·K vs 0.81 for brick — §6.1)
    │
    ├─ Wet area (bath, kitchen, external face of a service duct)?
    │   └─ Solid brick or solid block. Avoid AAC unless fully tanked — AAC's
    │      capillary suction makes an untanked AAC bathroom wall a damp problem.
    │
    └─ Supply reality check (Pakistan): is there an AAC plant within economical
       haulage, a supplier of thin-bed adhesive, AND a mason crew who has laid AAC
       before?  If any answer is no → specify brick or block. An AAC wall laid by an
       untrained crew in 12 mm cement mortar is worse than a good brick wall.
```

*(All units and constructions in this decision tree are single-leaf solid masonry — see
the cavity-wall scope note in §0.)*

### 2.1 Selection matrix (score the project, not the material)

| Driver | Brick (solid clay) | Solid concrete block | Hollow concrete block | AAC block |
|---|---|---|---|---|
| Load-bearing capability | ★★★★★ | ★★★★ | ★★★ (needs grout+rebar) | ★★ (engineered only) |
| Seismic performance in confined masonry | ★★★★★ | ★★★★ | ★★ ungrouted | ★★ |
| Dead-load reduction | ★ | ★★ | ★★★ | ★★★★★ |
| Thermal insulation | ★★ | ★ | ★★ | ★★★★★ |
| Wall build speed | ★★ | ★★★★ | ★★★★ | ★★★★★ |
| Mortar consumption | ★ (high) | ★★★ | ★★★ | ★★★★★ (3 mm thin-bed) |
| Availability everywhere in Pakistan | ★★★★★ | ★★★★ | ★★★ | ★★ |
| Crew familiarity | ★★★★★ | ★★★★ | ★★★ | ★★ |
| Fixing heavy items to the wall | ★★★★★ | ★★★★★ | ★★ | ★★ (special anchors) |
| Wet-area suitability | ★★★★ | ★★★★★ | ★★★ | ★★ |
| Shrinkage-crack risk | ★ (low) | ★★★ (moderate) | ★★★ | ★★★ |
| Material cost per m² of wall | ★★★★ (cheapest) | ★★★ | ★★★ | ★★ (premium) |

**Reading the matrix:** in Pakistan the default remains solid burnt clay brick for
load-bearing and confined masonry, because it wins on the three things that actually
decide a house — strength, availability and crew familiarity. AAC wins decisively and
only when the wall is *infill in an RCC frame* and either mass or thermal performance is a
real project driver. Concrete block sits in between and is at its best for boundary walls,
plinth/retaining stems, and G+1 load-bearing where a block plant is close and a brick kiln
is not.

---

## Section 3: Burnt Clay Brick — Specification & Acceptance

### 3.1 Dimensions

| Item | Value | Source |
|---|---|---|
| Standard Pakistani brick (nominal, non-modular) | **9" × 4.5" × 3"** = 228.6 × 114.3 × 76.2 mm | market standard `[practice]` |
| Brick + 12 mm (½") joint | 9.5" × 5" × 3.5" | derived |
| Dimensional tolerance, individual brick | ±3% on each dimension `[practice]` | IS 1077 comparator uses a 20-brick stack |
| Acceptance measurement method | Stack **20 bricks** dry, length-to-length, on a flat surface; measure overall. 20 × 9" = 180" ±3.5" acceptable band | IS 1077 method `[VERIFY exact band]` |
| Machine-made / "Gultex"-type facing brick | commonly 8"–9" × 4" × 2.5"–3", tighter tolerance, used for exposed facades | manufacturer `[practice]` |
| Modular fly-ash / cement brick | 230 × 110 × 75 mm | manufacturer |

Never mix nominal sizes in one wall. A batch of 8.5" bricks landing mid-wall shows up as a
wandering perpend line and a plaster thickness that goes to 25 mm to hide it.

### 3.2 Classification as used on a Pakistani site

| Local name | English | Typical crushing strength | Absorption | Acceptable use |
|---|---|---|---|---|
| **Awwal / A-class** | First class, well-burnt | market spec **≥ 2,000 psi (13.8 MPa)**; civil references give ~10.5 MPa (105 kg/cm²) for first-class kiln-burnt | 12–15% (accept ≤ 20%) | Load-bearing walls, confined masonry panels, exposed facing, all structural work |
| **Doyum / B-class** | Second class | ~1,500 psi (10 MPa) `[practice]` | 15–22% | Internal partitions, backing course behind facing, non-structural infill |
| **Soim / C-class, khingar** | Third class, under-burnt in part | < 1,000 psi | > 22% | Filling, soling under floors, temporary work. **Never load-bearing** |
| **Pili / kacha** | Under-burnt (pale yellow, soft, dull thud) | very low, crumbles | very high | **Reject entirely.** Common at the top and bottom of a delivered stack |
| **Jhama** | Over-burnt, warped, glassy, dark | high but irregular shape | low | Broken as coarse aggregate/soling. Not for facing or coursed masonry |

**Design assumption rule:** unless a laboratory test report for *this delivery* exists,
design to **f'b = 7 MPa**, not 13.8 MPa. Punjab brick-kiln surveys (ResearchGate,
*Quality evaluation of bricks of different brick kilns in Punjab Province, Pakistan*) show
wide kiln-to-kiln scatter; the market label "A-class" is a price tier, not a test result.

### 3.3 Acceptance criteria table

| Property | Requirement | Test | Frequency |
|---|---|---|---|
| Compressive strength | ≥ 2,000 psi (13.8 MPa) for A-class specified; accept ≥ 10.5 MPa if the spec allows; **never below 7 MPa** for load-bearing | Lab, IS 3495 Part 1 (frog filled with 1:3 mortar, 3-day cure, immersed 24 h) | **5 bricks per 50,000** or per delivery lot, whichever is more frequent |
| Water absorption | ≤ **20%** by weight after 24 h cold soak (first class); good Pakistani brick 12–15% | IS 3495 Part 2 — dry weight W1, 24 h soak, wet weight W2, absorption = (W2−W1)/W1 × 100 | 5 bricks per lot |
| Efflorescence | **Nil to slight** for exposed / external work; up to *moderate* tolerable for plastered internal walls | IS 3495 Part 4 (§17.1 below) | 5 bricks per lot |
| Dimensional tolerance | ±3% individual; 20-brick stack within band | Steel tape, flat surface | Every delivery |
| Shape | Sharp square edges, flat faces, no warping > 3 mm, no cracks | Visual | Every delivery |
| Structure | Break one: homogeneous, no lumps of lime, no voids, uniform colour through the section | Break test | 2 per delivery |
| Soundness | Two bricks struck together give a **clear metallic ring**, not a dull thud | Sound test | Continuous, by the mason |
| Hardness | No impression from a **fingernail** scratch | Scratch test | Continuous |
| Drop test | Dropped flat from **1 m onto hard ground, does not break** | Drop test | 2 per delivery |

### 3.4 Field triage — the 60-second gate inspection

1. Walk to the **middle** of the truck/trolley load, not the neat face the driver stacked.
2. Pull 10 bricks at random. Ring two together — dull = under-burnt.
3. Scratch with a nail. Marks = reject.
4. Drop one from waist height. Shatters = reject.
5. Break one open. Pale core, visible lime lumps, or a black core (bloating) = reject the lot.
6. Look at colour uniformity across the stack. Two colours = two kiln batches = two strengths.
7. Count: brick trolleys short-count routinely. Count one stack fully, then count stacks.

### 3.5 Pakistani supply realities

- **Zigzag kilns** are mandated in Punjab for emissions; conversion changed firing profiles
  at many kilns, so historic "this kiln is good" knowledge may not hold — retest.
- **Smog-season closures** (typically Nov–Jan in Punjab) shut kilns by district order.
  Order and stockpile masonry units before the season or the programme slips
  (see `architecture-construction-sequencing`).
- Brick prices are quoted **per 1,000**, kiln-gate vs delivered differing by PKR 2–4/brick;
  rate bands live in `architecture-cost-estimation-boq` §9, not here.
- **Storage:** stack ≤ 1.5 m high on level dry ground, off soil, in stacks of a countable
  unit (e.g. 500). Cover in rain — saturated bricks laid wet cause efflorescence.

---

## Section 4: Concrete Block — Solid & Hollow

### 4.1 Dimensions and classes

| Item | Value | Source |
|---|---|---|
| Common nominal sizes | 400 × 200 × 200 mm (16"×8"×8"), 400 × 200 × 150, 400 × 200 × 100 | market `[practice]` |
| Void ratio, hollow block | 25–50% of gross area | IS 2185 Part 1 comparator |
| Density, solid block | 1,800–2,200 kg/m³ | `[practice]` |
| Density, hollow block | 1,100–1,500 kg/m³ | `[practice]` |
| Hollow load-bearing, Grade A | 3.5 – 15 N/mm² (block-density dependent) | IS 2185 Part 1 `[VERIFY grade table]` |
| Hollow load-bearing, Grade B | 3.5 – 5.0 N/mm² | IS 2185 Part 1 `[VERIFY]` |
| Hollow non-load-bearing, Grade C | ≥ 1.5 N/mm² | IS 2185 Part 1 `[VERIFY — grade lettering and the strength bands attached to it vary between IS 2185-1 editions and are sometimes conflated with a different national scheme; confirm the current edition's actual table before quoting a Grade A/B/C figure to a client or authority, and do not assume the A/B/C split maps cleanly onto load-bearing/non-load-bearing use]` |
| ASTM comparator, load-bearing CMU | net-area compressive strength ≥ 13.1 MPa (1,900 psi) | ASTM C90 `[VERIFY current edition value]` |
| Drying shrinkage | ≤ 0.06% (block must be dried/aged before laying) | IS 2185 Part 1 comparator |
| Water absorption | ≤ 10% by weight for dense blocks `[practice]` | |

**One 400×200×200 block replaces roughly 9–12 standard bricks by volume**, which is where
the speed advantage comes from: fewer units, fewer joints, less mortar, straighter walls.

### 4.2 The two rules that decide whether block masonry cracks

1. **Age the blocks.** Concrete blocks shrink as they dry. A block laid at 7 days old will
   shrink in the wall. **Minimum 28 days from casting before laying** `[practice]`; demand
   the casting date, and reject blocks that are still cold and damp from the yard.
2. **Do not soak blocks.** Unlike clay brick, concrete block must **not** be immersed.
   Lightly dampen the bedding face only (a wet brush or fine spray) minutes before laying.
   A soaked block dries in the wall and pulls the joints apart.

Additional controls:
- **Control joints** in long block walls at **≤ 6 m centres** and at changes of height or
  thickness `[practice]`; brick walls tolerate longer runs, block walls do not.
- **Bond beams** (a course of channel/lintel blocks filled with concrete and 2 bars) at
  lintel and roof level convert a block wall into something with tensile continuity.
- **Reinforced masonry:** vertical bars in grouted cells at 600–1,200 mm centres, grout
  10 mm aggregate, one lift per storey, with cleanouts at the base. This is a designed
  system — hand it to the engineer, do not improvise it.

### 4.3 When block is the right call in Pakistan

- Boundary walls and plinth stems (high volume, low finish requirement, on-site casting).
- Sites far from a good brick kiln but near sand/crush — blocks can be cast on site with a
  hand or vibro press, cured 28 days.
- G+1 load-bearing in low seismic zones with solid blocks ≥ 5 N/mm² and full banding.
- Where speed of enclosure matters more than material cost.

### 4.4 When block is the wrong call

- Zone 2B+ load-bearing with **ungrouted hollow** blocks — a brittle, low-shear wall
  (also on the reject list in `architecture-seismic-design` §4.6).
- Where blocks arrive under 28 days old and the programme cannot wait.
- Exposed unplastered facades in high-rainfall areas without a rendered or coated finish.
- Walls that will carry heavy wall-hung fixtures unless solid units are used at those zones.

---

## Section 5: AAC Block (Autoclaved Aerated Concrete)

### 5.1 Specification

| Property | Value | Source |
|---|---|---|
| Compressive strength | **3 – 5 N/mm²**; minimum **3.0 N/mm²** for Grade 1 | IS 2185 Part 3 `[VERIFY grade/density table]` |
| Dry density | 550 – 650 kg/m³ (Grade 1); 451–550 also produced | IS 2185 Part 3 `[VERIFY]` |
| Weight relative to alternatives | ≈ **1/3** the weight of brick masonry, ≈ **1/2** a concrete block, for the same volume | research finding |
| Common sizes | 600 × 200 × (75 / 100 / 125 / 150 / 200 / 230) mm | manufacturer |
| Thermal conductivity λ | ≈ **0.16 W/m·K** (vs ≈ 0.81 brick, ≈ 0.9–1.1 dense block) | manufacturer `[VERIFY per product]` |
| Fire resistance, 200 mm wall | up to ~4 hours | manufacturer `[VERIFY per test certificate]` |
| Drying shrinkage | must be within the standard's limit; the dominant crack risk | IS 2185 Part 3 `[VERIFY]` |
| Jointing | **thin-bed polymer adhesive, 2–4 mm joints** — not 12 mm cement mortar | manufacturer / best practice |

### 5.2 Thin-bed adhesive is not optional

A 12 mm cement-sand joint in an AAC wall does three bad things at once: it creates a
thermal bridge that erases most of the insulation benefit, it is far stiffer than the
block so cracks form along the joints, and it drinks the moisture the adhesive chemistry
was designed to hold. **If thin-bed adhesive is not available on the project, do not
specify AAC.** Specify brick or block and say why.

### 5.3 Wetting rule — the opposite of brick

- Clay brick: **soak 1–2 hours** before laying (dry brick sucks the mortar dry and halves
  bond strength).
- Concrete block: **surface dampen only**.
- AAC: **do not soak.** Light surface misting immediately before applying adhesive, and
  only if the manufacturer's data sheet says so. Soaked AAC shrinks on drying and cracks.

### 5.4 Plastering AAC

AAC's high suction and low modulus break ordinary cement plaster. The specification is:
- **Internal:** gypsum plaster (11–13 mm, single coat, no curing) — the cleanest answer; or
  cement plaster 1:6 over an SBR/acrylic bonding slurry.
- **External:** 1:6 cement plaster over a bonding slurry, with fibre-mesh or chicken mesh
  over the full face — never a rich 1:3 or 1:4 direct onto AAC.
- **Every junction** between AAC and RCC or AAC and brick: 150 mm wide galvanised chicken
  mesh, lapped 75 mm each side, fixed before plaster.

### 5.5 Fixings, services, wet areas

- Use **AAC-specific nylon/frame anchors**; ordinary plugs pull out. Heavy items (geysers,
  wall-hung WCs, TV brackets, kitchen wall units) need a solid backing block, a plywood
  pattress, or a designed anchor.
- Chases cut easily with a hand saw or wall chaser — which is the danger. Cut chases are
  routinely too deep in AAC. Enforce the chase rules in §12.3 strictly.
- **Wet areas:** AAC absorbs by capillarity. Only use in bathrooms/kitchens behind a full
  tanking system, or use solid brick/block for those walls. In an unsupervised Pakistani
  build, default to brick for wet-area walls.

### 5.6 AAC as load-bearing

Possible, and done abroad, with:
- engineered wall thickness (typically 200–300 mm),
- a specified strength grade (≥ 4 N/mm²) with mill test certificates,
- thin-bed adhesive with certified bond strength,
- reinforced/confined detailing designed by the engineer,
- low seismic demand or a designed lateral system.

**In Pakistani residential practice this skill's default is: AAC = non-load-bearing infill
in an RCC frame.** If the user wants load-bearing AAC, say plainly that it requires an
engineer's design with the supplier's certified strength data, and that solid brick
confined masonry is the lower-risk answer for a house.

### 5.7 Pakistan supply reality checklist (all four must be YES before specifying AAC)

- [ ] A plant or stockist within economical haulage of the site (haulage on a light material can exceed the material cost).
- [ ] Thin-bed adhesive available from the same supplier, in the quantity needed.
- [ ] A mason crew with prior AAC experience, or a supplier who will train and supervise the first day.
- [ ] Gypsum plaster or a bonding agent available for the finish system.

### 5.8 AAC reinforced lintel blocks (U-blocks) — an alternative to an RCC band

AAC systems commonly offer a **U-shaped lintel block** (AAC U-block): a channel-section AAC
unit laid over an opening, filled with reinforcement and in-situ concrete, that cures into
a lintel matching the AAC wall's thickness and thermal performance exactly — no cold
bridge, no differential shrinkage crack at the AAC-to-RCC interface, and it is laid with
the same crew and adhesive as the rest of the wall.

| Item | Value | Source |
|---|---|---|
| Typical U-block depth | 200–250 mm (matches an equivalent RCC lintel depth for short spans) | manufacturer `[VERIFY per product]` |
| Reinforcement and concrete fill | Per manufacturer's span table, or engineer-sized same as an RCC lintel | manufacturer / `architecture-concrete-reinforcement-detailing` |
| Bearing | Same **≥ 230 mm each side** rule as §12.1 | this skill §12.1 |
| When to prefer it over a continuous RCC band | Where the whole wall is AAC infill and there is no structural requirement for the band to tie into the seismic frame's confining system | this skill |
| When NOT to substitute it | Any location where `architecture-seismic-design` requires a **continuous** lintel/sill band across both masonry types for seismic continuity — a U-block over one AAC opening does not satisfy that requirement on its own; check with the seismic skill before treating it as equivalent |

Treat AAC U-blocks as a masonry-side detailing convenience, not a substitute for the
seismic band requirement — confirm the substitution against `architecture-seismic-design`
§4.3 on any project where the lintel/sill band is doing seismic work, not just spanning an
opening.

---

## Section 6: Comparative Unit Data — the numbers a design actually needs

### 6.1 Unit property comparison

| Property | Solid clay brick | Solid concrete block | Hollow concrete block | AAC block |
|---|---|---|---|---|
| Typical unit size (mm) | 229 × 114 × 76 | 400 × 200 × 200 | 400 × 200 × 200 | 600 × 200 × 200 |
| Unit compressive strength | 7 – 14 N/mm² | 4 – 8 N/mm² | 3.5 – 5 N/mm² (Grade B) | 3 – 5 N/mm² |
| Masonry density (built, incl. mortar) | 1,900 – 2,000 kg/m³ | 1,800 – 2,200 | 1,100 – 1,500 | 600 – 700 |
| Thermal conductivity λ (W/m·K) | ≈ 0.81 | ≈ 1.0 | ≈ 0.7 (incl. voids) | ≈ 0.16 |
| Joint type / thickness | cement mortar 10–12 mm | cement mortar 10–12 mm | cement mortar 10–12 mm | thin-bed adhesive 2–4 mm |
| Units per m² of wall face | ≈ **84** (230 mm wall) / ≈ 42 (115 mm wall) `[derived]` | ≈ 12.5 | ≈ 12.5 | ≈ 8.3 |
| Water absorption | 12 – 20% | ≤ 10% | ≤ 10% | high capillary suction |
| Sound reduction Rw, plastered wall `[indicative]` | ≈ 50 dB @ 230 mm; ≈ 40 dB @ 115 mm | ≈ 48 dB @ 200 mm | ≈ 42 dB @ 200 mm | ≈ 44 dB @ 200 mm |
| Shrinkage risk | Low (fired unit, no drying shrinkage) | Moderate | Moderate | Moderate–high if wetted |

### 6.2 Wall self-weight — use these for load takedown

Plastered both faces (12 mm internal + 20 mm external assumed at 20 kN/m³ where applicable).

| Wall build-up | kN/m² | kg/m² | Per metre run at 3.05 m storey (kN/m) |
|---|---|---|---|
| 230 mm brick + plaster both faces | **4.9** | ≈ 500 | 15.0 |
| 345 mm brick + plaster both faces | **7.1** | ≈ 725 | 21.7 |
| 115 mm brick + plaster both faces | **2.7** | ≈ 275 | 8.2 |
| 200 mm solid concrete block + plaster | **4.4** | ≈ 450 | 13.4 |
| 200 mm hollow concrete block + plaster | **3.3** | ≈ 335 | 10.1 |
| 200 mm AAC + plaster both faces | **1.7** | ≈ 170 | 5.2 |
| 100 mm AAC + plaster both faces | **1.1** | ≈ 110 | 3.4 |

**Why this table matters.** Swapping 230 mm brick infill for 200 mm AAC saves
(4.9 − 1.7) = **3.2 kN/m² of wall face**. A 1,125 sqft house with ≈ 260 m² of total wall
area therefore sheds ≈ 3.2 × 260 = **832 kN ≈ 85 tonnes** of dead load off the frame and
foundations — and because seismic base shear is mass-driven, it sheds a proportional share
of the earthquake demand too. On a 4-storey block with 1,200 m² of wall the saving is
≈ 3,840 kN ≈ **390 tonnes**.

That is the real argument for AAC, and it is an argument for the **engineer** to act on. Do
not swap the infill material after the frame and footings have been designed to the heavier
load and call it a saving — it is a design change, and it also changes the building's
period and stiffness distribution.

---

## Section 7: Mortar

### 7.1 The governing principle

> **The mortar must be weaker than the unit.** A mortar stronger than the brick forces
> cracks to run *through* the bricks instead of along the joints, where they can neither be
> repointed nor tolerated. This is why 1:3 is a *repair and structural bedding* mix, not a
> general masonry mix.

### 7.2 Mortar mix selection by role

| Cement : sand (by volume) | Indicative 28-day cube strength `[practice]` | IS 2250 grade `[comparator]` | Use |
|---|---|---|---|
| **1:3** | 15 – 20 MPa | > MM7.5 | Bedding under column base plates, structural repairs, dry-pack under beam soffits, DPC mortar. **Not** general masonry |
| **1:4** (rich) | 7.5 – 10 MPa | MM7.5 | Load-bearing ground storey in Zone 3–4; all masonry below plinth / in contact with soil; boundary walls; parapets; 115 mm half-brick walls; exposed brickwork |
| **1:5** (standard) | 5 – 7.5 MPa | MM5 | **Default for 230 mm load-bearing walls** in Zones 1–2B; general external walls |
| **1:6** (lean) | 3 – 5 MPa | MM3 | Internal non-load-bearing walls; upper-storey masonry in low seismic zones; the minimum acceptable structural mix |
| 1:8, mud mortar, cement-free | < 1.5 MPa | MM0.7 / none | **Prohibited** in any Zone 2B+ structure; not used in this library |
| 1:1:6 cement : lime : sand | ≈ 3 – 5 MPa, far better workability & crack-healing | MM3 | Excellent where hydrated lime is available; rarely stocked in Pakistan `[practice]` |
| Thin-bed AAC adhesive | per manufacturer | — | AAC only, 2–4 mm joints |

**Cross-check with `architecture-seismic-design` §4.4:** minimum 1:6 for confined masonry;
**1:4 for the ground storey in Zone 3–4**. That rule governs when the two disagree.

### 7.3 ASTM C270 comparator (for spec writing against an international standard)

| ASTM C270 type | Min compressive strength | Rough equivalence used here `[practice]` |
|---|---|---|
| Type M | 17.2 MPa (2,500 psi) | ≈ 1:3 |
| Type S | 12.4 MPa (1,800 psi) | ≈ 1:3.5 |
| Type N | 5.2 MPa (750 psi) | ≈ 1:5 – 1:6 |
| Type O | 2.4 MPa (350 psi) | ≈ 1:8, non-structural |

C270 types are cement-**lime**-sand proportions; the equivalence above is indicative only.
Do not write "1:5 = Type N" into a contract specification without checking the actual
proportion specification in C270 `[VERIFY]`.

### 7.4 Batching, mixing and the 30-minute rule

| Rule | Value |
|---|---|
| Batching method | **Gauge box**, 1 cft (12" × 12" × 12"). One 50 kg cement bag = 0.0347 m³ ≈ **1.226 cft** (Pakistani site practice commonly rounds this to "1.25 cft" — a ~2% rounding that is fine for a quick site estimate, but do not use 0.0347 m³ and 1.25 cft together as if they were exactly equal; §16 and the FreeCAD script in §20.2 use the precise 1.226 cft figure). Head-pans, wheelbarrows and "andaaza" are not measures |
| Batch size | Never more than can be used in 30 minutes |
| Water | Potable only. Water:cement ≈ 0.5–0.6 for a workable mortar; consistency test = a handful holds shape without slumping or bleeding |
| Mixing | Mix cement + sand **dry** to a uniform colour first, then add water. Machine mix ≥ 2 min, hand mix on a clean impervious platform (never on bare soil) |
| Usable life | **Use within 30 minutes** of adding water (OPC); reduce to ~20 min above 35 °C |
| Retempering | Adding water to stiffened mortar to "revive" it is **prohibited**. Discard it |
| Hot weather (> 40 °C) | Shade the sand stockpile, lay early morning/evening, soak bricks fully, cover finished work with damp hessian |
| Cold weather (< 5 °C) | Do not lay. Mortar below 5 °C does not hydrate reliably |
| Mortar cube testing | 70.6 mm cubes, 3 per 20 m³ of masonry or per day's mix, whichever more frequent `[practice]` |

### 7.5 Mortar quantities

Mortar occupies **≈ 25%** of the volume of 230 mm brickwork with 12 mm joints, and **≈ 30%**
of 115 mm brickwork. Wet mortar → dry material factor **× 1.30** (range 1.27–1.33, sand
bulking). These match `architecture-cost-estimation-boq` §6.3 exactly — do not restate them
with different numbers.

**Per 100 cft of 230 mm (9") brickwork:**

| Mortar mix | Wet mortar (cft) | Dry (× 1.30) | Cement (bags) | Sand (cft) |
|---|---|---|---|---|
| 1:4 | 25 | 32.5 | **5.2** | 26.0 |
| 1:5 | 25 | 32.5 | **4.3** | 27.1 |
| 1:6 | 25 | 32.5 | **3.7** | 27.9 |

**Per 100 cft of 115 mm (4.5") brickwork** (mortar ≈ 30%), 1:4 → **7.5 bags** + 30 cft sand.

**Per m³ of 230 mm brickwork** (metric equivalent, for BIM/quantity scripts):

| Mix | Cement (kg) | Cement (bags) | Sand (m³) |
|---|---|---|---|
| 1:4 | 85 | 1.70 | 0.236 |
| 1:5 | 71 | 1.42 | 0.246 |
| 1:6 | 61 | 1.22 | 0.253 |

---

## Section 8: Constituent Materials — Cement, Sand, Water, Admixtures

### 8.1 Cement

| Item | Requirement |
|---|---|
| Type | OPC 43 or 53 grade (ASTM C150 Type I / BS EN 197 CEM I) for masonry and plaster |
| Sulphate-resisting | Specify SRC (ASTM C150 Type V equivalent) for masonry below plinth in saline/sulphate soils — see `architecture-geotechnical-foundations` for the soil test that triggers this |
| Bag weight | 50 kg; spot-check on a scale — short-weight bags are a real and common loss |
| Age at use | Use within **90 days** of the manufacture date printed on the bag; check the date at delivery |
| Rejection | Any lump that does not crumble to powder under finger pressure = partially hydrated = reject the bag |
| Storage | Off the floor on planks/pallets ≥ 150 mm, ≥ 300 mm clear of external walls, stacked **≤ 10 bags** high, covered, first-in-first-out |
| Common Pakistani brands | Lucky, Bestway, DG Khan, Maple Leaf, Fauji, Cherat, Askari, Pioneer, Kohat — specify a grade, not a brand, in the specification |

### 8.2 Sand (fine aggregate)

| Property | Masonry mortar | Plaster |
|---|---|---|
| Fineness modulus | 2.2 – 3.2 `[practice]` | 1.5 – 2.2 (finer) |
| Max particle size | Passing 4.75 mm sieve | Passing **2.36 mm** sieve; internal finish coat passing 1.18 mm |
| Silt / clay content | **≤ 8% by volume** by field jar test; ≤ 3% by weight in a lab test `[practice / IS comparator]` | ≤ 5% by volume — silt in plaster sand is the top cause of crazing |
| Organic matter | None visible; no roots, leaves, coal | Same |
| Chlorides/salts | **No sea sand.** No sand from saline flats — it is a direct efflorescence and corrosion source | Same |

**Field silt test (do this on every delivery, it takes 20 minutes):**
1. Fill a clear 250 ml measuring jar to 100 ml with the sand sample.
2. Add water to 150 ml plus a pinch of salt; shake hard for 1 minute.
3. Stand for 3 hours. Silt settles as a distinct layer above the sand.
4. Silt % = (silt layer height ÷ sand layer height) × 100.
5. **> 8% → wash the sand or reject the delivery.** Do not "adjust the mix" to compensate.

**Pakistani sand sources `[practice]`:**

| Source | Character | Best for |
|---|---|---|
| Lawrencepur (Attock) | Coarse, clean, low silt, premium price | Plaster finish coats, exposed work, RCC |
| Chenab | Medium grade, moderate silt | General masonry mortar, plaster base coat |
| Ravi | Fine, often silty, cheapest | Only after washing; internal plaster at best |
| Sargodha / Bolan | Regional, variable | Test before accepting |
| Hub River (Karachi region) | Check salinity/chloride explicitly | Reject if brackish |

**Bulking:** damp sand occupies 20–30% more volume than dry sand. Either measure sand dry
or apply a bulking correction, otherwise every "1:5" batch is quietly a 1:6 or 1:7.

### 8.3 Water

- **Potable water only.** pH 6–8.
- Brackish tube-well water is the single most common avoidable cause of efflorescence and
  salt banding in Pakistani houses. If the site tube-well is brackish, tanker in potable
  water for mortar, plaster and curing — including curing, which is where it is usually
  skipped.
- Chlorides < 500 ppm and sulphates < 400 ppm for concrete `[VERIFY against project spec]`;
  masonry mortar tolerances are looser but the efflorescence consequence is worse.

### 8.4 Admixtures

| Admixture | Dose | Use |
|---|---|---|
| Integral waterproofing compound | per manufacturer, typically ~1–2% by weight of cement `[VERIFY per product]` | DPC mortar, external plinth plaster, wet-area plaster, parapet plaster |
| SBR / acrylic bonding agent | Brush-applied slurry (SBR : cement : water per data sheet) | Plaster onto RCC, onto AAC, and at all repair interfaces |
| Plasticiser / air-entrainer | per manufacturer | Improves mortar workability without adding water; useful with coarse sand |
| Fibre (polypropylene, 12 mm) | ~0.6–0.9 kg/m³ `[VERIFY]` | Reduces plastic shrinkage crazing in external plaster and screeds |

Never use an admixture without the product data sheet on site, and never let a mason
"eyeball" a waterproofing compound dose from a drum.

---

## Section 9: Wall Thickness — Load-Bearing vs Infill

### 9.1 Thickness selection table

| Wall role | Default thickness | Alternatives | Notes |
|---|---|---|---|
| External load-bearing, 1–2 storey | **230 mm (9") solid brick** | 200 mm solid block ≥ 5 N/mm²; 200 mm grouted+reinforced hollow block | Confined masonry in Zone 2B+ |
| External load-bearing, ground storey of 3 storey | **345 mm (13.5")** or 230 mm with engineered tie columns | RCC frame | 3-storey load-bearing masonry needs a real design, not a thickness rule |
| Internal load-bearing | **230 mm** | — | Must be continuous to foundation and confined all four sides to count in wall density |
| Non-load-bearing partition | **115 mm (4.5") brick** | 100 mm concrete block; 100 mm AAC | Never counted in wall density (`architecture-seismic-design` §5.2) |
| Light partition, height ≤ 2.7 m, length ≤ 3 m | 75–100 mm AAC | 100 mm block | Needs top restraint; see slenderness §9.2 |
| Infill in RCC frame, external | 230 mm brick or **200 mm AAC** | 200 mm block | AAC if dead-load or thermal driven |
| Boundary wall ≤ 1.8 m | 230 mm | 115 mm **with 230 mm piers @ ≤ 2.4 m** + RCC coping | 115 mm boundary walls without piers blow over — a recurring Pakistani failure |
| Boundary wall > 1.8 m | 230 mm with 345 mm piers @ ≤ 3.0 m, RCC coping, designed footing | RCC | Wind and lateral earth pressure govern |
| Parapet | **230 mm ≤ 900 mm high**, doweled into slab, with RCC coping | RCC parapet | Free-standing 115 mm parapet above 600 mm is a defect — it is also a life-safety item in a quake |
| Basement / retaining | **RCC** | Designed reinforced masonry only | Do not build unreinforced masonry retaining walls for a house |
| Minimum for any confined-masonry structural wall | **120 mm** (international guidance floor) `[VERIFY — this specific figure could not be independently confirmed against the primary EERI/WHE guide text; treat it as indicative until checked against the source document]`; Pakistan practical minimum **230 mm** | — | EERI confined-masonry guide |

### 9.2 Slenderness check — the rule that actually bites

**Slenderness ratio SR = effective height (h_eff) ÷ effective thickness (t)**

| Restraint condition | h_eff |
|---|---|
| Restrained top and bottom (slab above and below, or tie beam) | 0.75 H |
| Simply supported top and bottom (top just butted, not tied) | 1.00 H |
| **Free at top** (parapet, partition with an open gap to the soffit) | 1.50 H |

| Limit | Value | Source |
|---|---|---|
| Confined masonry, 1–2 storey, max H/t | **≤ 25** | EERI confined-masonry guide |
| Unreinforced load-bearing masonry in cement mortar, max SR | ≤ 27 | IS 1905 comparator `[VERIFY]` |
| Non-load-bearing partition, practical max SR | ≤ 30 with top restraint `[practice]` | |

**Worked example A — a 230 mm load-bearing wall, storey height 3.05 m, restrained both ends**
h_eff = 0.75 × 3,050 = 2,288 mm; SR = 2,288 / 230 = **9.9 ✓** — enormous margin. This is why
slenderness never governs a normal 9" wall.

**Worked example B — a 115 mm partition, clear height 3.05 m, top gap not tied**
Free-at-top: h_eff = 1.5 × 3,050 = 4,575; SR = 4,575 / 115 = **39.8 ✗ FAILS badly.**
Fixes, in order: (1) tie the top to the soffit properly (dry-pack the 20 mm gap after 7 days,
or a skew brick course) → restrained, SR = 0.75×3,050/115 = **19.9 ✓**; (2) add 230 mm piers
at ≤ 2.4 m; (3) go to 150 mm.
**This is the single most common partition defect on a Pakistani site** — a half-brick wall
built to within 20 mm of the soffit and never packed, which then bows, cracks its plaster in
a straight line along the top, and does nothing for sound.

**Worked example C — a tall stairwell / double-height living room wall, 230 mm, H = 6.1 m**
Restrained at base and roof only: h_eff = 0.75 × 6,100 = 4,575; SR = 19.9 ✓ against SR ≤ 27,
but against the confined-masonry H/t ≤ 25 rule, H/t = 6,100/230 = **26.5 ✗**. Add an
intermediate tie beam at mid-height, or thicken to 345 mm, or add tie columns at ≤ 3 m.

### 9.3 Bearing stress check — and why gravity almost never governs

Permissible axial compressive stress for house-scale masonry checks: take **0.5 – 0.9 N/mm²**
for f'b = 10 MPa units in 1:6 to 1:4 mortar `[IS 1905 Table 8 comparator — VERIFY exact
value before use in a submission]`.

**Worked example — 230 mm load-bearing wall, single storey with RCC roof, Islamabad**

| Load | Calculation | kN/m |
|---|---|---|
| RCC roof slab, 125 mm | 0.125 × 24 kN/m³ × 2.0 m tributary | 6.0 |
| Roof finishes (screed, insulation, tiles, mud phuska) | 1.5 kN/m² × 2.0 m | 3.0 |
| Roof live load (accessible roof) | 2.0 kN/m² × 2.0 m | 4.0 |
| Wall self-weight, 3.05 m of 230 mm plastered wall | 4.9 kN/m² × 3.05 m | 15.0 |
| **Total at wall base** | | **28.0** |

Stress = 28,000 N ÷ (230 mm × 1,000 mm) = **0.122 N/mm²**
Against a permissible ≈ 0.5 N/mm² → **utilisation ≈ 24%.**

**Conclusion, and it generalises:** for a 1–2 storey house, a 230 mm brick wall is nowhere
near its gravity capacity. What actually governs masonry in Pakistani houses is, in order:
**(1) seismic wall density and confinement, (2) slenderness of thin walls, (3) eccentric
loading and point loads from beams, (4) moisture and workmanship.** Never present "the wall
is thick enough for the load" as if it settled the question.

### 9.4 Point loads and eccentricity — the checks people skip

- A beam bearing on a masonry wall needs a **bearing pad / RCC padstone**, minimum 230 ×
  230 × 150 mm `[practice]`, or the local crushing stress under a narrow bearing exceeds
  permissible even when the average wall stress is 24%.
- Minimum bearing length for a lintel or beam on 230 mm masonry: **230 mm** each side
  (`architecture-seismic-design` §4.5 uses ≥ 230 mm for lintel bands — keep them aligned).
- Load applied off-centre (a slab bearing on only half the wall, a cantilever) creates
  bending in the wall. Flag it to the engineer; do not resolve it with a rule of thumb.

### 9.5 Movement / expansion joints in masonry facades

Beyond the block-wall **control joints** already covered in §4.2 (≤ 6 m centres), long
masonry runs need movement-joint provision so thermal and moisture expansion does not
express itself as a random diagonal crack.

| Wall type | Movement joint spacing | Notes |
|---|---|---|
| Long clay brick facade (external, exposed or plastered) | **≤ 12 m** centres `[practice / BS 5628 comparator — VERIFY against the project's actual thermal/moisture movement calc for long runs]` | Clay brick expands slightly over its service life (irreversible moisture expansion) — the opposite direction to concrete block's drying shrinkage, so never detail the two together without a joint between them |
| Concrete block facade | **≤ 6 m** centres (same as the control-joint rule, §4.2) | Block shrinks; the joint accommodates shrinkage, not expansion |
| AAC facade | Per manufacturer, typically similar to block; confirm with the supplier's technical data sheet | AAC's shrinkage behaviour is product-specific — do not assume the brick or block spacing applies |
| At every change of wall height, thickness, or where a masonry wall meets a stiffer RCC element (long shear wall, RCC core) | Provide a joint or a designed flexible tie regardless of the run length | Differential stiffness concentrates cracking at this location even on a short wall |
| Joint detail | 10–12 mm compressible filler (closed-cell foam or similar) full wall thickness, sealant both faces, **never mortared solid** across the joint | A joint filled with mortar is not a joint — it just relocates the crack to the joint's edge |

This is masonry-side detailing only. Where a movement joint must also carry a seismic
separation function (adjacent structurally independent blocks), that requirement is owned
by `architecture-seismic-design` — do not size a seismic separation gap from this table.

---

## Section 10: Bonds, Jointing and Wall-Build Workmanship

### 10.1 Bond selection

| Bond | Where | Notes |
|---|---|---|
| **English bond** | 230 mm and thicker load-bearing walls | Strongest; alternate courses of headers and stretchers. Default for structural work |
| **Flemish bond** | Exposed facades where appearance matters | Headers and stretchers alternate in the *same* course; slightly weaker, more cutting, better looking |
| **Stretcher bond** | 115 mm half-brick walls only | The only option at half-brick thickness |
| **Header bond** | Curved walls, one-brick-thick footings | Rare in houses |
| **Rat-trap bond** | Cavity-forming brick bond, thermal/economy | Attractive but reduces solid area — not for confined masonry structural panels without an engineer's approval |

### 10.2 The workmanship rules that decide whether the wall cracks

| Rule | Value |
|---|---|
| Joint thickness | **10–12 mm**, uniform; tolerance ±3 mm |
| Perpends (vertical joints) | **Fully filled.** Unfilled perpends ("dry joints") are a defect — they halve shear strength and are a rain path |
| Lap | ≥ ¼ brick; no vertical joint continuous over more than one course |
| Frogs | **Frog upward**, filled with mortar |
| Brick wetting | Soak clay bricks **1–2 hours** before laying, then surface-dry before bedding. Never lay from a dry stack |
| Max lift per day | **1.0 – 1.2 m** of wall height `[practice]`; the seismic library allows up to 1.5 m — take the lower value when the mortar is lean or the weather is hot |
| Level difference between adjacent panels | ≤ 1.0 m; raise walls uniformly |
| Stopping a run | **Rack back at ≤ 1:3 slope.** Vertical toothing at a stop-end is a defect — the only intended toothing is at a future tie-column face |
| Joint raking for plaster key | Rake green joints **10–12 mm deep** the same day, before the mortar sets |
| Curing | **7 days minimum**, wet 3× daily; longer in hot weather |
| Rain protection | Cover the top of unfinished walls at the end of each day; washed-out joints and saturated brick are the start of an efflorescence problem |
| Verticality tolerance | ±6 mm over a 3 m storey; ≤ 12 mm over the full height of a ≤ 3 storey building `[practice / BS 5628 comparator]` |
| Bed-joint level | ±10 mm over 10 m |

### 10.3 The masonry-to-soffit joint (a specific, chronic Pakistani defect)

Masonry built tight to the underside of an RCC beam or slab will crack, because the slab
deflects and the mortar has no room. The correct sequence:

1. Build the wall to **20–25 mm short** of the soffit.
2. Wait **7 days minimum** (14 preferred) for the masonry to take its shrinkage/settlement.
3. Close the gap by one of:
   - a course of bricks laid at **45° (skew/soldier course)**, hammered in with mortar — the
     standard Pakistani practice, and acceptable; or
   - **dry-pack** 1:3 stiff mortar rammed in from both faces; or
   - non-shrink grout for a designed infill.
4. Then, and only then, plaster over the junction — with 150 mm chicken mesh spanning it.

Skipping step 2 produces the horizontal crack at the top of every internal wall in the house
about six months after handover.

---

## Section 11: Confined Masonry — The Masonry-Side Execution

> Full tie-column and tie-beam schedules, wall density tables, opening rules and seismic
> zone logic live in **`architecture-seismic-design` §4–§6**, which is the owner of that
> content. This section covers only what the *masonry trade* must do, and the material
> consequences.

### 11.1 What confined masonry is (and the one rule that gets lost)

Masonry panels **enclosed on all four sides** by cast-in-place RC confining elements — tie
columns at the vertical edges, tie beams at the top and bottom — where the **masonry is
built first** and the concrete is cast **against** it.

```
CORRECT (confined masonry)              WRONG (frame with infill — the 2005 collapse archetype)
1. Plinth beam                          1. Columns cast
2. Masonry panel built full height,     2. Beams cast
   toothed at future column faces       3. Bricks stuffed into the frame afterwards
3. Tie-column cage placed against
   the toothed masonry
4. Concrete cast against the masonry
   (formwork on 2 faces only)
5. Tie beam cast on top, continuous
```

If the columns go up first, it is not confined masonry, whatever the drawing says. Put this
sequence on sheet 1 of the drawings, and in Urdu on a board at the site office.

### 11.2 Geometry limits (EERI confined-masonry guide — the numeric proxy for BCP)

| Parameter | Value | Source |
|---|---|---|
| Max tie-column spacing, low/moderate seismic zones | **≤ 6.0 m** | EERI guide |
| Max tie-column spacing, high/very-high seismic zones | **≤ 4.5 m** | EERI guide |
| Max wall height-to-thickness H/t, 1–2 storey | **≤ 25** | EERI guide |
| Minimum wall thickness | **120 mm** international floor `[VERIFY — not independently confirmed against the primary EERI/WHE text, see §9.1]`; **230 mm** Pakistani practical minimum for load-bearing | EERI guide / `[practice]` |
| Panels enclosed on | **all four sides** | EERI guide |
| Tie columns mandatory at | every external corner, every wall intersection/T-junction, every free wall end, both jambs of openings > 1.2 m | EERI guide / `architecture-seismic-design` §4.2 |
| Tie beams mandatory at | plinth, lintel (continuous band), every floor, roof | `architecture-seismic-design` §4.3 |

Tie-member cross-sections, rebar, tie spacing, hook geometry and concrete grade:
see `architecture-seismic-design` §4.2–§4.3 and `architecture-concrete-reinforcement-detailing`.
Do **not** invent them here.

### 11.3 Masonry-side execution specification

| Item | Requirement |
|---|---|
| Units | Solid first-class burnt clay brick. No khingar, no pili, no ungrouted hollow block in Zone 2B+ |
| Mortar | ≥ 1:6; **1:4 for the ground storey in Zone 3–4**; mud mortar prohibited |
| Bond | English or Flemish, all perpends filled, joints 10–12 mm |
| Toothing at tie-column faces | Alternate courses toothed **50–60 mm** into the future column, **or** 2 × 6 mm horizontal dowels every 3rd course (≈ 600 mm) extending ≥ 400 mm into the panel and ≥ 400 mm into the column |
| Panel build | Full storey height before the column is cast; keep the toothed face clean of mortar droppings |
| Wetting before casting the column | Soak the toothed masonry face thoroughly before placing concrete — a dry brick face sucks water out of the column concrete and produces a weak, dusty interface |
| Formwork | Two faces only, tight against the masonry, sealed with a mortar fillet or tape at the masonry line — the classic grout-loss/honeycombing path |
| Column concrete | Max aggregate **12 mm** in a congested 230 × 230 cage; slump **75–100 mm**; needle vibrator 25 mm; layers ≤ 450 mm; free drop ≤ 1.5 m |
| Curing | Masonry 7 days; tie members 7 days minimum, 10 in hot weather |

### 11.4 Masonry-side reject list (aligned with `architecture-seismic-design` §4.6)

- A smooth vertical joint between masonry and tie column — no toothing, no dowels → the
  column and wall act separately and the confinement is decorative.
- Tie column cast before the wall.
- Mortar droppings left in the toothing so the concrete cannot key in.
- The toothed face dry when the column was poured.
- Formwork not sealed at the masonry line → grout loss → honeycombing exactly at the
  interface that matters most.
- 115 mm walls presented as structural.
- Half a wall built, column cast, then the rest of the wall built against the hardened
  column (the wall is now unconfined on that edge above the joint).

---

## Section 12: Openings, Lintels, Sills, Chases and Fixings

### 12.1 Lintels and bands

| Item | Requirement |
|---|---|
| Preferred solution | A **continuous lintel band** at one level around the whole building, not individual lintels over each opening — this is a seismic requirement, and it is also structurally simpler |
| Minimum RCC lintel depth | 150 mm for spans ≤ 1.5 m; deeper for longer spans — sizing per `architecture-concrete-reinforcement-detailing` |
| AAC alternative | An AAC reinforced lintel U-block (§5.8) may substitute for the RCC lintel **within** an AAC infill panel where no seismic continuity requirement applies to that band — confirm against `architecture-seismic-design` §4.3 before substituting |
| Bearing | **≥ 230 mm each side** on 230 mm walls |
| Precast lintels | Acceptable for internal non-seismic openings only; **not** a substitute for a continuous band |
| Load triangle | Masonry above a lintel arches; only the triangle of masonry within 60° of the bearings loads the lintel — but if a slab/beam bears within that triangle, the full load applies |
| Chajja / sunshade | Cast monolithically with the lintel band; a chajja bolted or keyed on afterwards is a falling hazard |

### 12.2 Sill band

A **75 mm RCC sill band** under the line of windows, continuous, is the cheapest crack
control available in seismic zones — it stops the diagonal crack that runs from the lower
window corner `[IS 4326 practice, cross-referenced in Pakistani practice]`.

### 12.3 Chases — the rule most often broken

| Rule | Value |
|---|---|
| Horizontal chases in load-bearing walls | **Prohibited.** A horizontal chase cuts the wall's compression path |
| Vertical chase depth | ≤ **⅓ of wall thickness** (≤ 75 mm in a 230 mm wall) |
| Vertical chase width | ≤ 200 mm |
| Proximity | Not within **300 mm** of a wall junction, a tie column, or an opening jamb |
| 115 mm walls | **No chasing.** A 50 mm chase in a 115 mm wall leaves 65 mm — the wall is now a crack waiting for a trigger. Use surface conduit, a service duct, or thicken the wall to 150 mm where services run |
| Cutting method | Wall chaser / disc, never a hammer and chisel that shatters the surrounding bricks |
| Making good | Fill the chase with **1:3 mortar** and cover with **150 mm wide galvanised chicken mesh**, lapped ≥ 75 mm each side, fixed to the masonry, **before** plaster |
| Timing | All chasing complete and tested (MEP-before-plaster gate — `architecture-construction-sequencing`) before any plaster starts |

### 12.4 Fixings by substrate

| Substrate | Light fixing | Heavy fixing (geyser, wall-hung WC, TV, wall units) |
|---|---|---|
| Solid brick | Any nylon plug | Chemical/resin anchor or a through-bolt |
| Solid block | Any nylon plug | Resin anchor |
| Hollow block | Toggle or spring anchor into a **web**, never the shell | Fill the cells locally with grout at design stage, or a resin anchor with a sleeve |
| AAC | **AAC-specific spiral/frame anchor** | Solid backing block, plywood pattress, or through-fixing. Assume ordinary plugs will fail |

Door frames: **3 hold-fasts per jamb**, embedded in the mortar bed joints as the wall goes
up — not chiselled in afterwards.

---

## Section 13: Plaster & Rendering Specification

### 13.1 Specification by location

| Location | Thickness | Mix | Coats | Finish | Curing |
|---|---|---|---|---|---|
| Internal walls (brick/block) | **12 mm** | 1:5 (1:6 acceptable; 1:4 if only coarse sand available) | 1 coat | Wood float, then putty/neeru | 7 days |
| Ceiling / slab soffit | **6–10 mm** (never > 12 mm) | 1:4 | 1 coat | Wood float | 7 days |
| External walls | **20 mm** | 1:4 | **2 coats** (12 mm scratch-keyed base + 8 mm finish) | Sponge/float | 10 days |
| Parapets, chajjas, copings, exposed edges | 20 mm | **1:3** + waterproofing compound | 2 coats | Float | 10 days |
| External plinth face / below DPC | 20 mm | **1:3** + waterproofing compound | 2 coats | Float | 10 days |
| Wet areas below tile | 12 mm | **1:3** + waterproofing compound | 1 coat | **Scratch finish** (tile key) | 7 days |
| AAC internal | 11–13 mm gypsum, or 12 mm 1:6 cement over bonding slurry | see §5.4 | 1 | — | gypsum: none; cement: 7 days |
| AAC external | 15–20 mm 1:6 over bonding slurry **with full-face mesh** | | 2 | Float | 10 days |
| Concrete block | 12 mm internal / 20 mm external, 1:5 / 1:4 | | 1–2 | Float | 7–10 days |
| Exposed brick (no plaster) | — | Pointing 1:3, raked and struck | — | Clear silane/siloxane sealer | — |

Cross-check quantities with `architecture-cost-estimation-boq` §6.4 — that table is the
BOQ authority; this table is the specification authority. Where the two show a different
default mix for the same location, the cost skill's mix is what has been priced; reconcile
explicitly rather than silently.

### 13.2 Pre-plaster gate — nothing starts until all of these are true

- [ ] Masonry is **≥ 7 days old** and has been cured. Plaster on green masonry cracks as the masonry shrinks.
- [ ] All electrical conduits, boxes, plumbing chases, sleeves complete and **pressure-tested** (MEP-before-plaster gate).
- [ ] All chases filled with 1:3 mortar and covered with 150 mm chicken mesh.
- [ ] **150 mm chicken mesh over every junction of dissimilar materials** — masonry-to-RCC column, masonry-to-beam, masonry-to-slab soffit, brick-to-block, brick-to-AAC. Alternative accepted detail: a deliberate 10 × 10 mm **groove** at the junction so the inevitable crack is a designed line, not a random one.
- [ ] Smooth RCC surfaces **hacked** (or treated with a bonding slurry) — plaster does not stick to shutter-smooth concrete.
- [ ] Surface cleaned of mortar droppings, dust, oil, form-release agent.
- [ ] Wall **thoroughly wetted** the evening before and again 2 hours before plastering — damp, not streaming.
- [ ] **Thappis / screed dots** set out at 1.5–2.0 m centres to control thickness and plumb.
- [ ] Door and window frames fixed, plumbed, and protected.
- [ ] Scaffolding independent of the wall — no putlog holes left in a finished facade.

### 13.3 Plastering rules

| Rule | Value |
|---|---|
| Max thickness per coat | **12 mm.** A 20 mm single coat will crack and may debond |
| Second coat timing | After the first has set but is still green — typically same day to 24 h internally, 3–7 days externally with the base kept damp |
| Keying the base coat | Scratch/comb the base coat while green — a smooth base coat is a debonding plane |
| Finishing | Wood float. **Do not** finish with neat cement slurry ("punning") — it crazes |
| Over-troweling | Prohibited. Working the surface brings laitance up and produces map cracking |
| Curing start | 24 hours after application, then keep continuously damp for 7 days (10 external) |
| Weather | Do not plaster in direct sun on a hot windy afternoon, below 5 °C, or above 40 °C without shading and wind screens |
| Thickness on ceilings | If the soffit needs more than 12 mm to level, the slab is out of level — fix it with a screed/false ceiling, not thick plaster. Thick ceiling plaster falls |
| Corners and reveals | Metal or PVC corner beads on external corners; reveals and jambs plastered square and plumb |

### 13.4 Drying before decoration

| Check | Requirement |
|---|---|
| Drying time before paint | **21–28 days** after plastering `[practice]` |
| Surface moisture | < 12–15% on a protimeter before priming |
| Alkalinity | Fresh cement plaster is strongly alkaline; if pH indicator paper on a damp patch reads > 10, use an **alkali-resistant primer** or wait longer. Painting early produces saponification, patchy sheen and peeling |
| Substrate soundness | Tap test: a hollow "drummy" sound = debonded plaster. Cut it out and redo before painting over it |

---

## Section 14: Finishes Above the Plaster

| Finish | Spec | Notes |
|---|---|---|
| **Wall putty** (white-cement or acrylic) | 2 coats, ~1–1.5 mm total, sanded between coats | For a smooth paintable internal surface; not a waterproofer, not for exteriors below a splash zone |
| **POP punning** | 8–12 mm over cement plaster | Very smooth finish; **never** in wet areas or externally; needs a dry substrate |
| **Gypsum plaster** | 11–13 mm single coat directly on masonry, **no curing needed**, fast | Excellent on AAC and block internally. **Prohibited** in bathrooms, kitchens splash zones, external walls, and anywhere it can get wet |
| **Emulsion paint** | Primer + 2 coats | Internal; check §13.4 gates first |
| **Weather-coat / elastomeric exterior** | Primer + 2 coats, crack-bridging grade for hairline crazing | External; specify the crack-bridging grade if the plaster shows map cracking |
| **Textured / grit-wash / stone finish** | Per system | Hides minor plaster variation; harder to repair |
| **Ceramic / porcelain tile** | Cement-based adhesive (C1/C2 per EN 12004) over a scratch-finish 1:3 plaster; or thick-bed 1:3 for floors | Wet areas must be tanked *before* tiling — `architecture-roofing-waterproofing` |
| **Stone/marble cladding** | Mechanically anchored above 1.2 m, not adhesive alone | Falling cladding is a life-safety item |

---

## Section 15: Moisture, DPC and Salt Control (masonry-side)

Full waterproofing build-ups live in `architecture-roofing-waterproofing`. The masonry-side
essentials:

| Item | Requirement |
|---|---|
| DPC | Continuous, **full wall width**, at plinth level, above finished ground by ≥ 150 mm. 38–75 mm thick 1:2:4 concrete with integral waterproofing compound, or a bituminous/polymer membrane lapped ≥ 100 mm |
| Plinth height | ≥ 450 mm above finished external ground `[practice / byelaw dependent — check the local authority]` |
| Masonry below DPC | 1:4 mortar minimum; SRC cement if soil sulphates/salinity indicate |
| Continuity | The DPC must connect to the floor DPC/membrane — a DPC in the wall that stops at the floor edge leaves a bypass path |
| External plinth face | 1:3 plaster with waterproofing compound, taken 150 mm below finished ground |
| Bridging | Do not let a plaster coat, a paved apron, a planter or backfill bridge over the DPC — the most common way a correctly installed DPC is defeated |
| Brackish site water | Do not use for mortar, plaster **or curing**. This is the leading avoidable cause of salt banding in Pakistani houses |

---

## Section 16: Quantity Estimation (masonry-side quick reference)

The BOQ authority is `architecture-cost-estimation-boq` §6. Reproduced here only as the
minimum set needed to sanity-check a material order.

| Quantity | Value |
|---|---|
| Bricks per cft of brickwork — **costing** (mortar-adjusted) | **10.4** (+7% wastage = 11.2) |
| Bricks per cft of brickwork — **procurement** (trade figure, wastage embedded) | **13.5** |
| Bricks per m³ of brickwork (mortar-adjusted) | ≈ **367** (+7% ≈ 395) |
| Bricks per sqft of 230 mm wall face | ≈ 8 (mortar-adjusted) |
| Bricks per sqft of 115 mm wall face | ≈ 4 (mortar-adjusted) |
| Mortar as % of brickwork volume | 25% (230 mm wall); 30% (115 mm wall) |
| Wet mortar → dry material factor | × 1.30 |
| Cement bag | 50 kg = 0.0347 m³ ≈ **1.226 cft** (see §7.4 — practice rounds this to 1.25 cft; use the precise figure in any calculation that also uses the m³ value) |
| Cement density (for volume ↔ mass) | 1,440 kg/m³ |
| Wastage allowance — bricks | 5–10%, use 7% |
| Wastage allowance — sand, cement | 5–8% |

**The unit error to watch for:** the widely circulated Pakistani figure "13.5 bricks" is per
**cubic** foot, not per square foot. Applied per sqft it over-orders by ~70%. Always state
the unit explicitly.

---

## Section 17: Defect Catalogue — Cause, Test, Prevention, Remedy

### 17.1 Efflorescence

**What it is:** white or grey crystalline salt deposit on the face of brickwork or plaster.
Water dissolves soluble alkali salts (sulphates of sodium, potassium, magnesium, calcium)
present in the bricks, sand, cement or mixing water, migrates to the surface, evaporates,
and leaves the salt behind.

**The four inputs — remove any one and it stops:** soluble salts + water + a migration path
+ an evaporating surface.

**Test (IS 3495 Part 4):**
1. Stand the brick on end in a shallow dish with **25 mm of distilled water**, in a
   well-ventilated room at 20–30 °C.
2. Leave until the water is absorbed/evaporated; refill to 25 mm; let it evaporate again.
3. Classify the dried brick face:

| Rating | Deposit | Accept for |
|---|---|---|
| **Nil** | None visible | All work |
| **Slight** | < 10% of exposed area, thin | Exposed/external work |
| **Moderate** | 10–50%, heavier, no powdering/flaking | Plastered internal only |
| **Heavy** | > 50%, powdering/flaking | **Reject** |
| **Serious** | Thick deposit, flaking, deposit renews after wiping | **Reject** |

**Prevention:**
- Buy low-sulphate bricks — test the batch, and reject "heavy"/"serious".
- **Potable water only**, including for curing. Brackish curing water on a well-built wall
  will still produce salt bands.
- Do not over-soak bricks; drain before laying.
- Cover masonry from rain during construction; cover brick stacks on site.
- Continuous DPC, plinth ≥ 450 mm, no bridging.
- Keep the wall dry after handover — fix the leak, not the stain.

**Remedy:** brush off dry (never wash it in — that dissolves the salt and drives it back into
the wall). Repeat over several dry cycles. Only after the wall is genuinely dry and the
deposit stops renewing, consider a dilute-acid wash by a specialist and an alkali-resistant
primer. **Painting over active efflorescence guarantees the paint will blister off.**
If the deposit keeps returning, you have a live water source — find it.

### 17.2 Honeycombing (in tie columns, lintels, bands — the concrete side of masonry work)

**What it is:** voids in cast concrete where mortar did not fill between the coarse
aggregate, leaving a coarse, cavernous surface. In confined masonry it appears most often
at the **base of tie columns** and **at the masonry-to-formwork line**, which is exactly the
worst place.

**Severity grading `[practice]`:**

| Grade | Description | Action |
|---|---|---|
| Minor | Surface blemish < 10 mm deep, no rebar exposed | Chip back, wet, bond slurry, patch with 1:2 mortar |
| Moderate | 10–25 mm deep, no rebar exposed | Chip to sound concrete, bond slurry, non-shrink grout / micro-concrete |
| Severe | Rebar exposed, or the void passes through the section | **Stop. Engineer's decision.** Likely break out and recast the member |

**Root causes:** insufficient vibration (or the wrong vibrator size for a 230 × 230 cage),
concrete too stiff (low slump), aggregate too large for the cage, free drop > 1.5 m,
placement in layers thicker than 450 mm, leaking or unsealed formwork, congested rebar at
the joint region.

**Prevention specification for a 230 × 230 tie column:**
- Max aggregate **12 mm**; slump **75–100 mm**.
- **25 mm needle vibrator**, 10–15 s per insertion point, insertions ≤ 450 mm apart,
  penetrating 100 mm into the previous layer. Do not vibrate the rebar cage.
- Layers ≤ 450 mm; free drop ≤ 1.5 m (use a chute or tremie for taller lifts).
- Formwork tight and **sealed at the masonry interface** with a mortar fillet.
- Inspect immediately on striking, while a repair is still cheap and visible.

**Repair procedure:** chip out all loose material to sound concrete, expose ≥ 20 mm behind
any reinforcement, clean and saturate the surface (SSD, no standing water), apply a
cement/SBR bond slurry, pack with non-shrink grout or 1:1.5:3 micro-concrete with 10 mm
aggregate, cure 7 days. **Never** simply plaster over honeycombing to hide it — this is a
common site "fix" and it conceals a section that may not carry its load.

### 17.3 Plaster cracking — diagnose the type before repairing

| Crack type | Appearance | Root cause | Repair |
|---|---|---|---|
| **Crazing / map cracking** | Fine web, < 0.2 mm, over whole panels | Mix too rich (1:3), over-troweling, neat-cement punning, rapid drying | Cosmetic. Putty + crack-bridging paint. Fix the mix on the next panel |
| **Drying shrinkage cracks** | 0.2–1 mm, random, often around the middle of panels | Single coat > 12 mm, inadequate curing, high-silt sand, hot windy drying | V-groove to 10 mm, fill with 1:3 + polymer, mesh if > 1 mm, repaint |
| **Junction / interface cracks** | Straight, exactly on a masonry-RCC or brick-AAC line | No chicken mesh, dissimilar movement, no groove | Cut back 100 mm each side, fix 150 mm mesh, replaster. Or convert to a designed groove |
| **Horizontal crack at the wall top** | Straight line under the beam/slab soffit | Masonry built tight to the soffit with no gap and no dry-pack (§10.3) | Cut out, dry-pack, mesh, replaster |
| **Cracks along chases** | Straight vertical/horizontal following conduit | Chase not meshed, or over-deep chase in a thin wall | Cut out, mesh, replaster. If the chase broke the §12.3 rules, escalate |
| **Diagonal cracks from opening corners** | 45° from window/door corners, **through both faces**, widening over time | **Structural** — settlement, seismic, missing lintel/sill band, overloaded wall | **STOP. Engineer.** Do not fill and paint |
| **Stepped cracks following mortar joints** | Staircase pattern through the joints | Differential settlement, or weak mortar | **Engineer.** Monitor with tell-tales before repairing |
| **Popping / blowing** | Small conical craters, weeks after plastering | Unslaked lime or contaminated particles hydrating in the plaster | Cut out each pop, patch. Change the material source |
| **Blistering** | Small raised bubbles | Over-troweling / trapped air in the finish coat | Cut out, patch |
| **Debonding / drummy plaster** | Hollow sound when tapped | Dirty or dry substrate, no bonding agent on smooth RCC, plaster on green masonry | Cut out the whole drummy area to sound plaster, re-prepare, replaster |
| **Peeling / flaking paint** | Paint lifts in sheets | Painted before the plaster dried (< 21 days), high alkalinity, damp behind | Strip, dry the wall, alkali-resistant primer, repaint |

**Diagnostic rule:** a crack **through both faces** of a wall in the same position, or one
that runs across the masonry and continues into the RCC, is structural until an engineer
says otherwise. Cosmetic cracks stay in the plaster.

### 17.4 Other material defects worth a reject

| Defect | Symptom | Action |
|---|---|---|
| Under-burnt (pili) brick | Pale, soft, dull thud, high absorption | Reject the lot |
| Over-burnt (jhama) | Warped, glassy, dark, irregular | Not for coursed or facing work |
| Bloating / black core | Dark spongy core when broken open | Reject — trapped gases, unreliable strength |
| Lamination | Thin flat layers separating on the face | Reject — clay was laminated during extrusion; delaminates in frost/salt |
| Chipped edges/corners | > 10 mm loss on more than a few % of the load | Downgrade to non-facing work; negotiate the delivery |
| Chuna (lime) nodules | White lumps visible in the broken section | Reject — will pop and spall after wetting |
| Blocks laid under 28 days old | Damp, cold, no casting date | Reject; shrinkage cracking is certain |
| Sand with high silt | Jar test > 8% | Wash or reject |
| Lumpy cement | Lumps that don't crumble | Reject the bag |
| Sulphate attack on plaster/mortar | Softening, expansion, cracking, especially below DPC | Investigate soil/water sulphates; SRC cement; a waterproofing strategy, not a patch |

---

## Section 18: Site Quality-Control Checklist & Tolerances

### 18.1 Hold points (nothing proceeds past these without sign-off)

| # | Hold point | Check |
|---|---|---|
| H1 | Material delivery | Brick field triage (§3.4), sand silt test (§8.2), cement date & weight, block casting date, AAC + adhesive supplier match |
| H2 | Before first course | Setting out, DPC continuous, plinth level, mortar mix agreed and gauge box on site |
| H3 | During wall build (daily) | Plumb, line, level, joint thickness, perpends filled, lift height, toothing at tie-column faces, curing running |
| H4 | Before casting a tie column | Toothing clean and soaked, cage per drawing (hooks 135°, tie spacing closed up at ends), formwork sealed at the masonry line |
| H5 | On striking tie-column formwork | Honeycombing inspection, immediate photograph, repair grading (§17.2) |
| H6 | Before plaster | The full §13.2 pre-plaster gate |
| H7 | After plaster, before paint | Tap test for drummy areas, straightedge flatness, moisture and alkalinity (§13.4) |
| H8 | Handover snagging | Crack survey with a crack gauge, photograph and date every crack > 0.3 mm, moisture check at plinth and wet-area walls |

### 18.2 Tolerance table

| Item | Tolerance |
|---|---|
| Wall verticality, per 3 m storey | ± 6 mm |
| Wall verticality, full height ≤ 3 storeys | ± 12 mm (absolute max 20 mm) |
| Bed-joint level | ± 10 mm over 10 m |
| Wall thickness | +10 / −5 mm |
| Mortar joint thickness | 10–12 mm, ± 3 mm |
| Tie-column plumb | ± 5 mm |
| Room squareness | ± 10 mm on diagonals up to 5 m |
| Opening dimensions | ± 5 mm |
| Internal plaster flatness | ≤ 3 mm gap under a 2 m straightedge |
| External plaster flatness | ≤ 5 mm gap under a 2 m straightedge |
| Plaster thickness | ± 2 mm of specified |
| Daily masonry lift | ≤ 1.2 m |

Values are practice-level acceptance criteria `[practice / BS 5628 & IS 1905 comparators]`
— put the actual numbers in the project specification so there is something to enforce.

### 18.3 Test frequency schedule

| Test | Frequency |
|---|---|
| Brick compressive strength (5 bricks) | Per 50,000 bricks or per delivery lot |
| Brick water absorption (5 bricks) | Per lot |
| Brick efflorescence (5 bricks) | Per lot |
| Sand silt jar test | **Every delivery** |
| Block compressive strength (8 blocks) | Per 5,000 blocks |
| AAC strength/density certificate | Per consignment (supplier certificate + 1 verification test) |
| Mortar cubes (70.6 mm, 3 nos) | Per 20 m³ of masonry, or per day |
| Concrete cubes for tie members | Per `architecture-concrete-reinforcement-detailing` |
| Plaster tap test | 100% of every wall, before paint |

### 18.4 The one-page site card (give this to the site supervisor)

```
BRICK      soak 1–2 hrs · ring not thud · no nail scratch · no pili at the bottom of the stack
BLOCK      28 days old min · DO NOT SOAK, dampen only · control joint every 6 m
AAC        thin-bed adhesive only · DO NOT SOAK · mesh every junction · special anchors
MORTAR     gauge box, not headpans · 1:5 default, 1:4 ground storey Zone 3–4 · use in 30 min · NEVER re-temper
WALL       joints 10–12 mm · perpends FILLED · rack back, don't tooth (except tie columns)
           max 1.2 m per day · rake joints same day · cure 7 days
CONFINE    WALL FIRST, COLUMN SECOND · tooth 50–60 mm every other course · soak before pouring
SOFFIT     stop 20–25 mm short · wait 7 days · skew course or dry-pack · THEN mesh and plaster
CHASE      vertical only · ≤ ⅓ thickness · never in a 4.5" wall · fill 1:3 + 150 mm mesh
PLASTER    masonry 7 days old · 12 mm max per coat · mesh every dissimilar junction
           NO neat-cement punning · cure 7 days · 21–28 days before paint
WATER      potable only — including for curing. Brackish water = salt bands = repaint every year
```

---

## Section 19: Procurement & Delivery Control (Pakistan)

| Item | Control |
|---|---|
| Bricks | Order per 1,000; agree class and a rejection right in writing; count one full stack and extrapolate; inspect the middle of the load; note kiln name — do not switch kilns mid-wall |
| Smog-season | Punjab kiln closures Nov–Jan — stockpile before, or the masonry programme slips |
| Sand | Specify the source by name (Lawrencepur / Chenab / etc.); silt-test every trolley; measure the trolley volume, do not accept "one trolley = 200 cft" without checking; account for bulking |
| Cement | Check manufacture date and bag weight on delivery; FIFO the stack; ≤ 10 bags high |
| Blocks | Demand the casting date; reject < 28 days; stack on pallets, off the ground |
| AAC | Confirm plant, grade, density and adhesive availability **before** the wall is designed around it; store covered and dry, on pallets — a rained-on AAC pallet is a shrinkage problem |
| Waterproofing compound / bonding agent | Product data sheet on site; dose by weight, not by eye |
| Storage layout | Materials within 20 m of the lift point; brick stacks ≤ 1.5 m; sand on a hard, drained, contained stockpile — sand stored on bare soil picks up clay and becomes the silt problem |

Rates and cost bands are owned by `architecture-cost-estimation-boq` §9 and change fast —
never quote a price from memory; check the current rate and label it `[verify]`.

---

## Section 20: Encoding Masonry in FreeCAD / BIM

### 20.1 Modelling conventions

- Model **real metric thicknesses**: 230, 115, 345, 200, 150, 100, 75 mm. Never mix a nominal
  "9 inch" (228.6) with a rounded 230 in the same model — quantity takeoffs will not close.
- Use `Arch Wall` with an explicit `Width`; do not fake thickness with a scaled solid.
- Use **`Arch MultiMaterial`** for the real build-up so the model reports finishes as well as
  structure, e.g. an external wall = plaster 20 / brick 230 / plaster 12 = **262 mm** total.
  Keep the *structural* face as the reference line so the structural model stays honest.
- Assign an `Arch Material` with a real density to every wall so mass takeoff works:
  brick masonry **1,920 kg/m³**, solid block **2,000**, hollow block **1,400**,
  AAC **600**, cement plaster **2,000**.
- Openings via `Subtractions` (live parametric), never a frozen boolean — see
  `architecture-freecad-bim`.
- Tag load-bearing walls with an `IfcType` of `Wall` and a custom property
  `LoadBearing = True`, so the wall-density script in `architecture-seismic-design` §13.2
  can find them and partitions are excluded automatically.
- Model tie columns and tie beams as separate `Arch Structure` objects, not as part of the
  wall — they are concrete, they need their own material, and they must appear separately
  in the BOQ.

### 20.2 Masonry quantity script (FreeCAD Python console / `mcp__freecad__execute_code`)

```python
# Masonry takeoff by wall thickness: volume, brick count, mortar cement bags.
# Planning aid only — not a construction quantity. Verify against a manual takeoff.
import FreeCAD as App

MORTAR_FRACTION = {230: 0.25, 345: 0.25, 115: 0.30, 200: 0.20, 100: 0.20}  # of wall volume
DRY_FACTOR      = 1.30            # wet mortar -> dry material
CEMENT_M3_BAG   = 0.0347          # 50 kg bag (~1.226 cft — see skill §7.4/§16, do not re-round to 1.25)
MIX             = {230: 5, 345: 4, 115: 4, 200: 5, 100: 6}   # cement:sand ratio (sand part)
BRICK_WITH_JOINT_M3 = 0.2413 * 0.127 * 0.0889   # 9.5" x 5" x 3.5"

doc = App.ActiveDocument
totals = {}
for o in doc.Objects:
    if getattr(o, "IfcType", "") != "Wall" and "Wall" not in o.Name:
        continue
    try:
        t = int(round(float(o.Width.getValueAs("mm"))))
        v = o.Shape.Volume / 1e9          # mm^3 -> m^3
    except Exception:
        continue
    totals[t] = totals.get(t, 0.0) + v

print(f"{'t(mm)':>7} {'vol m3':>9} {'vol cft':>9} {'bricks':>9} {'cem bags':>9} {'sand m3':>8}")
for t, v in sorted(totals.items()):
    mf   = MORTAR_FRACTION.get(t, 0.25)
    unit = v * (1 - mf) / BRICK_WITH_JOINT_M3 if t in (115, 230, 345) else 0
    dry  = v * mf * DRY_FACTOR
    part = MIX.get(t, 5)
    cem  = dry / (1 + part)
    print(f"{t:>7} {v:>9.2f} {v*35.3147:>9.1f} {unit*1.07:>9.0f} "
          f"{cem/CEMENT_M3_BAG:>9.1f} {dry - cem:>8.2f}")
print("\nPLANNING AID ONLY. 7% brick wastage included. Not a construction quantity.")
```

### 20.3 Model-level masonry checklist before exporting anything

- [ ] Every wall has an explicit thickness from the §9.1 table — no arbitrary values.
- [ ] Every load-bearing wall is ≥ 230 mm and continuous to the foundation in the model.
- [ ] No 115 mm wall is carrying a slab or a beam in the model geometry.
- [ ] H/t ≤ 25 checked for the tallest wall (stairwell, double-height space).
- [ ] Tie columns exist at every corner, junction, free end and > 1.2 m opening jamb.
- [ ] Tie beams are continuous at plinth, lintel, floor and roof — no band stops at a door.
- [ ] Materials with real densities assigned, so the mass takeoff means something.
- [ ] Plaster modelled (or explicitly excluded, and the exclusion stated in the output).
- [ ] The output states, in text, that it is a planning model requiring engineer sign-off.

---

## Section 21: Worked Example — Material Specification, 5-Marla Single-Storey House

**Project:** 25 ft × 45 ft (1,125 sqft) single-storey house, Islamabad
**Seismic:** Zone 2B per BCP-SP 2007 `[VERIFY against the official zoning map]`
**System:** Confined masonry, RCC roof slab, storey height 10 ft (3.05 m)

### 21.1 Material specification sheet

| Element | Specification |
|---|---|
| External + internal load-bearing walls | 230 mm solid first-class burnt clay brick, f'b ≥ 10.5 MPa target / 7 MPa design assumption, English bond, joints 10–12 mm |
| Partitions | 115 mm brick, stretcher bond, top restrained (dry-pack or skew course), no chasing |
| Mortar — walls below plinth & ground-storey external | **1:4** cement:sand |
| Mortar — general 230 mm walls | **1:5** |
| Mortar — 115 mm partitions | **1:4** |
| DPC | 50 mm 1:2:4 with integral waterproofing compound, full wall width, at plinth (≥ 450 mm above finished ground) |
| Tie columns | 230 × 230 mm at every corner, junction, free end and opening > 1.2 m; spacing ≤ 6.0 m (Zone 2B); reinforcement per `architecture-seismic-design` §4.2 |
| Tie beams | 230 mm deep at plinth, lintel and roof, fully continuous; per `architecture-seismic-design` §4.3 |
| Sill band | 75 mm RCC, continuous under the window line |
| Internal plaster | 12 mm, 1:5, wood float, putty finish |
| Ceiling plaster | 10 mm, 1:4 |
| External plaster | 20 mm in two coats, 1:4; 1:3 + waterproofing compound at parapet, plinth face and copings |
| Wet-area plaster | 12 mm 1:3 + waterproofing compound, scratch finish, over a tanked substrate |
| Junction treatment | 150 mm galvanised chicken mesh at every masonry-RCC junction and over every chase |
| Cement | OPC 43 grade; SRC below plinth if the soil report indicates sulphates |
| Sand | Chenab (masonry mortar), Lawrencepur (plaster finish coat); silt ≤ 8% by jar test |
| Water | Potable, including for curing |

### 21.2 Indicative quantities

Wall areas (gross face × storey height, openings deducted):

| Wall | Gross (sqft) | Openings | Net (sqft) | Volume (cft) |
|---|---|---|---|---|
| External 230 mm — 140 ft perimeter × 10 ft | 1,400 | −15% | 1,190 | 1,190 × 0.75 = **893** |
| Internal 230 mm — 90 ft × 10 ft | 900 | −12% | 792 | 792 × 0.75 = **594** |
| Partitions 115 mm — 60 ft × 10 ft | 600 | −15% | 510 | 510 × 0.375 = **191** |

| Material | Calculation | Quantity |
|---|---|---|
| Bricks — costing basis | (893 + 594 + 191) × 10.4 × 1.07 | ≈ **18,700** |
| Bricks — procurement basis | 1,678 × 13.5 | ≈ **22,700** → order 23,000 |
| Cement, 230 mm walls @ 1:5 | 1,487/100 × 4.3 bags | **64 bags** |
| Cement, external below-plinth portion @ 1:4 | included above, upgrade ~10% of volume | +2 bags |
| Cement, 115 mm walls @ 1:4 | 191/100 × 7.5 | **14 bags** |
| Sand, masonry | (1,487/100 × 27.1) + (191/100 × 30) | **460 cft** |
| Internal plaster area | 1,125 sqft × 2.5 multiplier | 2,813 sqft |
| External plaster area | 1,125 sqft × 1.1 | 1,238 sqft |
| Ceiling plaster area | plan area | 1,125 sqft |
| Cement, internal plaster 12 mm @ 1:5 | 2,813/100 × 0.72 | **20 bags** |
| Cement, external plaster 20 mm @ 1:4 | 1,238/100 × 1.30 | **16 bags** |
| Cement, ceiling plaster 10 mm @ 1:4 | 1,125/100 × 0.65 | **7 bags** |
| Sand, plaster | (2,813/100 × 4.51) + (1,238/100 × 6.5) + (1,125/100 × 3.25) | **245 cft** |
| **Cement total, masonry + plaster** | | **≈ 123 bags** |
| **Sand total, masonry + plaster** | | **≈ 705 cft** |

**Sanity note, and say it out loud:** contractors' field figures for the same scope typically
run **1.5–2×** these calculated quantities, because they bundle plaster, site loss and a
procurement cushion into one number. Use the calculated figures for costing and the
contractor's for an upper procurement bound — and always state which basis you used. The
divergence between the two is itself a useful negotiating fact.

### 21.3 What this example is not

It is not a design. Wall density in both directions, tie-member reinforcement, the roof
slab, the footings and the seismic check are all outside it and all required. Hand the
plan to a PEC-registered structural engineer before anything is ordered.

---

## Section 22: Anti-Patterns for Claude / Claude Using This Skill

1. **Do not output a material schedule without the licensing statement.** If the user is
   heading toward construction, say the engineer/approval sentence unprompted.
2. **Do not quote a BCP clause number for a confined-masonry value.** The clause-level BCP
   tables were not retrievable in research; the numbers here are the EERI guide's. Say so.
3. **Do not invent a market rate.** Route to `architecture-cost-estimation-boq` and label
   any rate `[verify]`.
4. **Do not contradict `architecture-seismic-design`** on wall density, tie-member schedules
   or opening rules. That skill owns them.
5. **Do not recommend AAC without running the four-point supply check** (§5.7). "AAC is
   lighter and better insulated" is true and useless if there is no adhesive within 300 km.
6. **Do not treat a thickness as a structural answer.** "230 mm is enough" is a
   gravity-stress statement; the real governing checks are wall density, confinement and
   slenderness.
7. **Do not repair a diagonal crack in text.** A through-both-faces diagonal crack from an
   opening corner is a structural finding — escalate, do not specify a filler.
8. **Do not mix units silently.** State cft or m³, per-thousand or each, nominal or
   mortar-adjusted, and never pair the 0.0347 m³ cement-bag figure with the rounded 1.25 cft
   figure as if both were exact (§7.4/§16) — the 13.5-bricks-per-sqft unit error is in
   circulation too and costs real money.
9. **Never fabricate a test report, mill certificate, efflorescence rating or cube result.**
   If the user has not tested, say the test has not been done and design to the conservative
   value (f'b = 7 MPa).
10. **Where a number is labelled `[VERIFY]`, carry the label through into the output.** Do
    not launder a provisional number into a confident one.

---

## Appendix A: Standards Cited

| Standard | Title / scope | Used here for |
|---|---|---|
| **Building Code of Pakistan – Seismic Provisions 2007** | PEC / Ministry of Housing & Works; post-2005 Kashmir earthquake | Seismic zoning, requirement for confined masonry, mortar grade by zone |
| **Building Code of Pakistan 2021 (Final Draft, 26.10.2021)** | pec.org.pk | Successor document; clause-level masonry tables `[VERIFY — fetch the PDF]` |
| **EERI / WHE Seismic Design Guide for Low-Rise Confined Masonry Buildings** (Brzev & Meli, 2011), confinedmasonry.org | International confined-masonry guidance | Tie-column spacing ≤ 6.0 m / ≤ 4.5 m, H/t ≤ 25, 120 mm min thickness `[VERIFY — see §9.1/§11.2]`, four-sided confinement |
| **IS 2185 Part 1** | Concrete masonry units — hollow and solid concrete blocks | Block grades, strengths, densities, shrinkage limits `[comparator — grade lettering varies by edition, VERIFY, see §4.1]` |
| **IS 2185 Part 3** | Autoclaved cellular aerated concrete blocks | AAC compressive strength ≥ 3 N/mm², density grades `[comparator]` |
| **IS 2250** | Preparation and use of masonry mortars | Mortar grades MM0.7–MM7.5, mix guidance `[comparator — no Pakistani equivalent found]` |
| **ASTM C270** | Standard Specification for Mortar for Unit Masonry | Mortar Types M/S/N/O strengths `[comparator]` |
| **IS 1077** | Common burnt clay building bricks | Classification, absorption ≤ 20%, dimensional tolerance `[comparator]` |
| **IS 3495 Parts 1–4** | Methods of tests of burnt clay building bricks | Compressive strength, water absorption, efflorescence test protocol |
| **IS 1905** | Structural use of unreinforced masonry | Slenderness ratio limits, basic permissible compressive stress `[comparator, VERIFY table values]` |
| **IS 4326:1993** | Earthquake-resistant design and construction of buildings | Opening rules, sill/lintel bands — cross-referenced in Pakistani practice |
| **ASTM C90** | Load-bearing concrete masonry units | CMU net-area strength `[comparator]` |
| **ASTM C150 / PS 232** | Portland cement (Type I, Type V/SRC) | Cement type selection |
| **NDMA Pakistan earthquake construction guidelines** | National Disaster Management Authority | Field guidance cross-check |

**Not applicable / not surfaced:** ASCE 7-22, ACI 318-19 and IBC/IRC 2021 were **not** found
to be directly referenced by Pakistani masonry practice in the research pass behind this
skill. ACI 318-19 is used in this library only for the RCC tie members and lintels
(see `architecture-concrete-reinforcement-detailing`). If a US-code cross-reference is ever
needed for masonry load calculations, run a targeted search against ASCE 7-22 wind/seismic
and TMS 402/602 masonry provisions first — do not assume the mapping.

---

## Appendix B: Items to VERIFY Against Primary Documents Before Citing

| # | Item | Where to verify |
|---|---|---|
| 1 | BCP clause numbers and numeric tables for confined masonry (tie-member rebar, tie-beam depth, concrete grade) | BCP 2021 Final Draft PDF, pec.org.pk; BCP-SP 2007 |
| 2 | Exact IS 1905 Table 8 basic permissible compressive stress for the unit/mortar combination used | IS 1905 |
| 3 | IS 2185 Part 1 block grade/density/strength table and Part 3 AAC grade table (grade lettering and strength bands vary by edition — do not assume Grade A/B/C maps cleanly to load-bearing/non-load-bearing) | IS 2185 |
| 4 | ASTM C270 proportion specification before equating a cement:sand ratio to Type M/S/N/O | ASTM C270 |
| 5 | ASTM C90 current-edition net-area strength value | ASTM C90 |
| 6 | IS 1077 20-brick stack dimensional tolerance band | IS 1077 |
| 7 | Seismic zone for the actual site (city-level lookups are indicative only) | BCP-SP 2007 official zoning map |
| 8 | AAC product λ, fire rating, drying shrinkage and adhesive bond strength | Manufacturer's certified data sheet, per product |
| 9 | Waterproofing compound and fibre dose rates | Product data sheet |
| 10 | Plinth height and any masonry-related byelaw requirement | Local authority byelaws (LDA/CDA/SBCA/RDA/TMA/DHA) — see `architecture-building-codes-permits` |
| 11 | Current material rates | `architecture-cost-estimation-boq` §9, and a live market check |
| 12 | Water chloride/sulphate limits for the project specification | Project spec / IS 456 / ASTM C1602 |
| 13 | EERI/WHE guide's actual stated minimum confined-masonry wall thickness (this file uses "120 mm" as an indicative floor — confirm against the primary guide text, §9.1/§11.2) | EERI/WHE Seismic Design Guide, confinedmasonry.org |
| 14 | Movement-joint spacing for long clay-brick facades (this file uses ≤ 12 m as a practice figure) | BS 5628 / project-specific thermal-movement calculation |
