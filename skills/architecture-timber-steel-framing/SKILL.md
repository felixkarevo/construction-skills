---
name: architecture-timber-steel-framing
description: >
  Alternative structural framing systems for houses beyond RCC and masonry —
  light-gauge (cold-formed) steel framing, hot-rolled structural steel portal
  frames, and timber platform/Dhajji framing — calibrated to Pakistan. Covers
  the code basis for each (AISI S100/S200/S230/S240/S400, ASCE 7-22, AISC 360,
  IRC 2021 Ch. 5/6/8 [R502/R602/R802], PKBC 2021 Ch. 23, BCP-SP 2007), member
  designation systems, indicative span and sizing tables, connection detailing
  (screws, bolted haunches, nailing schedules, hold-downs and uplift load
  path), seismic mass and base-shear comparison against RCC, durability/fire/
  thermal trade-offs, hybrid systems, realistic 2026 Pakistan availability and
  cost context, worked examples, and FreeCAD modelling defaults. Use when
  deciding whether a house should be framed in something other than
  RCC/masonry, or when modelling one that already is.
---

# Timber & Steel Framing for Houses (Alternatives to RCC/Masonry, Pakistan-Calibrated)

This skill is the counterpart to `architecture-structural-systems`, which covers the default Pakistani house systems — unreinforced masonry, confined masonry and RCC frame — and which explicitly lists "steel and timber residential framing in the Pakistani context" as a known gap. This file closes that gap. It exists so that when a project has a real reason to leave RCC behind (speed, clear span, site access, seismic mass, remote supply chain), the alternative can be selected, preliminarily sized, detailed at the connections, priced against the RCC baseline, and modelled in FreeCAD with plausible geometry — and so that when there is **no** such reason, the skill says so plainly and sends the project back to confined masonry or RCC frame, which is the correct answer for the overwhelming majority of Pakistani houses.

---

## Reality Check - Licensing & Liability

**This skill produces design aids and calculation guidance for planning and FreeCAD modelling ONLY.**

- Every span, gauge, section size, bolt count and screw spacing below is a **preliminary sizing aid, a code minimum, a prescriptive-table indication, or a rule of thumb**. Several tables in this file are reconstructed indicatively and are explicitly flagged as *"verify against the source standard PDF"* — treat those flags as binding, not decorative.
- **Any design intended for the actual construction of a real occupied building MUST be analysed, designed and stamped by a licensed structural engineer** — in Pakistan a **PEC-registered (Pakistan Engineering Council) Professional Engineer** in the relevant structural category. Outside Pakistan, the locally licensed/chartered equivalent.
- This is *more* true, not less, for the systems in this skill. RCC/masonry in Pakistan has a deep trade base that absorbs a lot of design sloppiness. LGSF, portal frames and timber framing do not: they are **connection-governed, uplift-governed and stability-governed** systems where a single missed hold-down, an unbraced compression flange or an untied portal base is a collapse mechanism, not a crack.
- **The design MUST also go through local authority plan approval before construction** — LDA (Lahore), CDA (Islamabad), RDA (Rawalpindi), SBCA (Karachi), GDA, PDA, DHA, or the relevant TMA / Cantonment Board — under their byelaws, which are separate from and additional to the structural code. **Several Pakistani development authorities and housing societies restrict or refuse non-RCC/non-masonry residential structures, or classify them as "temporary" or "prefabricated" with different rules.** Confirm in writing with the approving authority *before* designing a house in LGSF, steel or timber. See §12.3.
- **Claude / Claude must never present FreeCAD output, a span-table lookup, a section size, or any calculation in this skill as construction-ready.** The correct framing is always: *"preliminary sizing and coordination geometry — to be designed and stamped by a PEC-registered structural engineer."*
- **Say this unprompted.** If a user starts treating output as final — asks for a cutting list to send a fabricator, asks "so how many tons of steel do I order", says the crew arrives Monday, asks to delete a brace "because the model still stands", or forwards the model to a PEB supplier as a design — stop and state the licensing and approval requirement explicitly *before* continuing.
- **Never certify.** No stamped drawing, no structural stability certificate, no engineer's name/PEC number/signature block, no fabrication drawing presented as approved-for-construction.
- **Soil is never assumed.** Portal-frame bases and LGSF hold-downs both deliver *concentrated uplift and horizontal thrust* into foundations. Every foundation number here is conditional on a site-specific geotechnical investigation.
- **Wind and seismic parameters are never guessed.** Lightweight systems are frequently **wind-uplift governed rather than gravity governed** — the reverse of RCC. Basic wind speed, exposure, and seismic zone must come from the current governing map (PKBC 2021 / BCP-SP 2007), not from memory or from this file.
- **Fabricator-supplied "engineering" is not engineering.** PEB and prefab suppliers in Pakistan routinely provide shop drawings and a supplier calculation. That is a vendor submittal. It still requires independent review by the owner's PEC-registered engineer, especially for the foundation, the base thrust, and anything the vendor's standard shed detail did not contemplate (residential floors, masonry infill, roof tanks).

---

Three systems are covered:

1. **LGSF / CFS** — light-gauge steel framing (cold-formed steel), stud-and-track walls, the direct analogue of North American wood platform framing built in galvanized steel.
2. **Steel portal frames** — hot-rolled haunched moment frames, PEB (pre-engineered building) practice, for large clear spans.
3. **Timber framing** — platform framing and traditional Dhajji-Dewari / timber-laced masonry, viable in Pakistan essentially only in KPK, Gilgit-Baltistan and AJK.

---

## Section 1: When an Alternative Actually Beats RCC/Masonry

### 1.1 The default answer

For a normal Pakistani house — 3/5/10 marla or 1 kanal, G+1 or G+2, subdivided rooms, spans ≤ 5 m, urban site with road access, conventional contractor — the correct system is **confined masonry or RCC frame**, per `architecture-structural-systems` §1. It wins on cost, on trade availability, on supervision tolerance, on thermal mass, on approvals, on bank valuation, and on the owner's ability to get anything repaired in ten years.

**An alternative system must be justified by a specific project constraint, not by novelty.** If the user cannot name the constraint, the answer is RCC/masonry.

### 1.2 Trigger decision tree

```
START: house project, RCC/masonry is the assumed default
│
├─ T1. Is there a CLEAR-SPAN requirement > 6.5 m with no columns?
│      (great room, double-height living, workshop, 3+ car garage, indoor court,
│       hall/marquee annexe, poultry/livestock shed on the same plot)
│   ├─ YES, span 7-12 m .... RCC transfer beam is possible but deep and expensive;
│   │                        STEEL (portal frame or simple beam-and-column) usually wins
│   ├─ YES, span > 12 m .... STEEL PORTAL FRAME. RCC is effectively out.
│   └─ NO ................. continue
│
├─ T2. Is SCHEDULE the binding constraint? (weeks, not months)
│      disaster relief, flood rehousing, site handover deadline, rental income clock,
│      staff/labour housing, a season-limited build window in the north
│   ├─ YES → LGSF (factory panels, 2-3 wk fab + 1-2 wk erect) or PEB portal frame
│   │        (shell in 25-30 days) vs 6-12 months for RCC
│   └─ NO → continue
│
├─ T3. Is SITE ACCESS the binding constraint?
│      no ready-mix supply, no road for a transit mixer or pump, hill/valley site,
│      river crossing, aggregate must be hauled 100+ km, no water for curing
│   ├─ YES and site is in KPK/GB/AJK with local timber .... TIMBER (or hybrid: masonry
│   │                                                        plinth + timber superstructure)
│   ├─ YES anywhere else ................................. LGSF (hand-portable panels)
│   └─ NO → continue
│
├─ T4. Is SEISMIC MASS the binding constraint?
│      Zone 3/4 site (Quetta, Muzaffarabad, Gilgit, Chitral, Mansehra, Balakot),
│      poor soil with low bearing capacity, tall storey heights, or a client with
│      explicit earthquake-performance priority
│   ├─ YES → LGSF is genuinely superior on physics: ~25-35% of the seismic weight of
│   │        an equivalent masonry/RCC house, and a higher R-factor (§9)
│   │        Timber/Dhajji has an excellent historical record in AJK/KPK but sits
│   │        OUTSIDE explicit BCP-SP 2007 coverage → engineer's analysis, not a code
│   │        table lookup (§7.6)
│   └─ NO → continue
│
├─ T5. Is this a light ancillary structure, not the main house?
│      car porch canopy, roof-top room, servant quarter, boundary shed, guard room,
│      farmhouse veranda, workshop, poultry shed, storage
│   ├─ YES → STEEL (portal or simple frame) almost always. Do not pour a frame for it.
│   └─ NO → continue
│
├─ T6. Is this a VERTICAL EXTENSION on an existing structure with limited
│      foundation/column capacity? (adding a floor to an existing G+1)
│   ├─ YES → LGSF or timber upper storey adds ~30% of the weight of an RCC storey.
│   │        Often the only way to add a floor without underpinning.
│   │        STILL requires an engineer's assessment of the existing structure.
│   └─ NO → continue
│
└─ NONE of T1-T6 apply
    → RCC / CONFINED MASONRY. Say so directly. Explain that in Pakistan the
      alternative systems carry a trade-availability, approval and resale penalty
      that is not repaid unless one of the triggers above is real.
```

### 1.3 Trigger → system matrix

| Constraint | LGSF | Steel portal | Timber | RCC/masonry |
|---|---|---|---|---|
| Clear span 7-12 m | ✗ (not its job) | ★★★ | ✗ (rare, glulam only) | ★ (deep transfer beam) |
| Clear span > 12 m | ✗ | ★★★ | ✗ | ✗ |
| Schedule in weeks | ★★★ | ★★★ | ★★ (if local supply) | ✗ |
| No plant/ready-mix access | ★★★ | ★ (needs crane/gin pole) | ★★★ (north only) | ✗ |
| Seismic Zone 3/4 | ★★★ | ★★ | ★★ (no code table) | ★★ (CM, detailed) |
| Weak soil / low SBC | ★★★ (light) | ★ (concentrated base loads) | ★★★ | ✗ |
| Lowest cost, generic footprint | ★ | ★★ (shell only) | ★ | ★★★ |
| Trade availability in Pakistan | ★ | ★★ (industrial only) | ★ (north only) | ★★★ |
| Thermal comfort, 45 °C summers | ★ (needs insulation) | ✗ (needs full envelope) | ★★ | ★★★ (mass) |
| Bank valuation / resale | ✗ | ✗ | ✗ | ★★★ |
| Owner-repairable in 10 years | ★ | ★ | ★★ (north) | ★★★ |
| Termite / damp exposure (Punjab, Sindh) | ★★★ | ★★★ | ✗ without treatment | ★★★ |
| Coastal corrosion (Karachi) | ★ (needs Z275+) | ★ (needs paint system) | ★★ | ★★★ |
| Fire without added protection | ★★ (non-combustible, but strength loss) | ★★ | ✗ | ★★★ |

### 1.4 Weighted selection scorecard (use when two systems are genuinely close)

Score each system 1-5 on each criterion, multiply by weight, sum. Record the scores in the project notes so the choice is auditable.

| Criterion | Default weight | Raise the weight when… |
|---|---|---|
| Structural fitness (span, storeys, loads) | 5 | any T1 trigger |
| Programme / speed | 3 | any T2 trigger → 5 |
| Capital cost (all-in, finished) | 4 | tight budget → 5 |
| Local trade & supply availability | 4 | remote site or first-time owner-builder → 5 |
| Seismic performance | 3 | Zone 3/4 → 5 |
| Thermal comfort / running cost | 3 | Punjab/Sindh, no continuous AC budget → 4 |
| Durability & maintenance (termite, corrosion, damp) | 3 | coastal or high water table → 5 |
| Approval risk with the authority | 3 | DHA/CDA/society plot → 5 |
| Resale / financeability | 2 | build-to-sell → 4 |
| Fire safety | 2 | multi-family or rental → 4 |

**Hard veto rules (no score can override these):**
- No timber framing as a primary structure in Punjab/Sindh without a full pressure-treatment and termite-barrier specification, and even then, question it.
- No LGSF or timber primary structure where the approving authority has not confirmed in writing that it will be approved.
- No steel portal frame whose base thrust has not been explicitly resolved into a tie or a moment foundation (§6.5).
- No lightweight roof anywhere without a continuous, detailed uplift load path from sheeting to foundation (§9.3).

---

## Section 2: Code Basis — What Governs What

### 2.1 Standards map

| System | Primary design standard | Prescriptive / simplified route | Seismic detailing | Pakistan adopting context |
|---|---|---|---|---|
| LGSF / CFS | **AISI S100** (North American Specification for the Design of Cold-Formed Steel Structural Members) | **AISI S230-19** — Prescriptive Method for One- and Two-Family Dwellings, up to 3 storeys, aligned to 2015+ IRC and ASCE 7-10 | **AISI S400** — Seismic Design of Cold-Formed Steel Structural Systems; required by **ASCE 7-22 Ch. 12** for the seismic force-resisting system in **SDC B-F** | No native Pakistani CFS standard. De facto basis = BCP-SP 2007 seismic chapter (steel scope) + PKBC 2021 + AISI S-series as the referenced material standard |
| LGSF general provisions | **AISI S200** (General Provisions), **AISI S240** (Structural Framing) | — | — | as above |
| LGSF non-structural | **AISI S220-20** (Nonstructural Members) — ceiling grids, partitions, drywall framing | — | ASCE 7-22 now pulls some interior CFS partitions into engineered scope in higher SDCs | as above |
| Steel portal frame | **AISC 360** (or Eurocode 3 / BS 5950 legacy, depending on the fabricator's house practice) | PEB manufacturer standard frames | **AISC 341** + ASCE 7-22 Ch. 12; in low-rise SDC B/C, R = 3 "not specifically detailed for seismic resistance" is commonly used | **BCP-SP 2007 steel chapter** (AISC/UBC-derived). Fabrication commonly to **IS 2062 Gr. E350** plate/section steel in the Pakistani PEB market |
| Timber framing | **PKBC 2021 Chapter 23 "Wood"** — a real, citable in-country provision set | **IRC 2021 Ch. 8** span tables: rafters **R802.4.1(1)-(8)**, ceiling joists **R802.5.1(1)-(2)**; floor joists **R502.3.1** (Ch. 5); headers **R602.7**, fastening schedule **R602.3(1)** (Ch. 6) | ASCE 7-22 for wood light-frame; **BCP-SP 2007 does NOT explicitly recognise wood-frame or Dhajji-Dewari as a structural type** | PKBC 2021 Ch. 23 is the citable Pakistani provision; the seismic gap is real and must be closed by engineering analysis |
| Loads (all systems) | **ASCE 7-22** — Ch. 4 live, Ch. 7 snow, Ch. 26-30 wind, Ch. 11-12 seismic | — | — | BCP-SP 2007 uses a UBC-97-derived ELF method; PKBC 2021 is IBC/ASCE-aligned |

**A note on naming — read this before citing anything above.** This skill standardizes on two distinct document names and does not use them interchangeably:

- **PKBC 2021** (Pakistan Building Code 2021) — the current, IBC/ASCE-aligned general building code. This is what an earlier draft of this file, and much informal industry usage, calls "BCP 2021." **They are the same document.** Cite it as **PKBC 2021**, chapter and clause, in every drawing note and submission — "BCP 2021" is the colloquial name, not the citable title, and using it on a submission risks the plan checker not recognising the reference.
- **BCP-SP 2007** (Building Code of Pakistan, Seismic Provisions, 2007) — a separate, older, still-in-force document that carries the UBC-97-derived seismic zoning map and ELF method. It has **not** been superseded by PKBC 2021 for seismic zoning purposes as of this writing; both are cited together because PKBC 2021 covers general building provisions while BCP-SP 2007 remains the seismic-zoning authority. **Do not merge these two into one citation** — "PKBC 2021 / BCP-SP 2007" appearing together in this file means two separate documents being cited jointly, not one document under two names.

**Confirm both document titles and their current status with the approving authority before submission** — code editions and the division of scope between them can change, and this skill's citations are only as good as the last time they were checked against the source PDFs.

### 2.2 The honest Pakistani code position

1. **LGSF has no Pakistani standard.** A PEC engineer designing an LGSF house in Pakistan is applying AISI S100/S240/S400 (a North American material standard) with PKBC/ASCE loads. That is defensible and normal practice, but it means **the approving authority's plan checker may never have seen it before**. Budget time for that conversation and submit the AISI references with the drawings.
2. **AISI S230-19 is the shortcut, and it has limits.** It is a *prescriptive* method: within its stated geometric, load, and seismic limits (one- and two-family dwellings up to 3 storeys, aligned to 2015+ IRC / ASCE 7-10 loads), stud size, spacing, fastening and bracing can be read from tables without full member design. **Outside those limits — larger openings, higher wind speed, higher seismic demand, irregular plan, taller storeys — S230 does not apply and the frame must be engineered to S100/S240.** Do not stretch S230 to a plot in Quetta with 4 m storey heights.
3. **There is no "residential portal frame" code anywhere.** Portal frames are designed to general steel codes plus manufacturer practice. Residential use is a borrowed industrial technology; residential detailing (insulation, condensation, acoustics, fixings for internal linings) is *outside* the PEB supplier's core competency and must be designed by the architect/engineer, not assumed.
4. **BCP-SP 2007's silence on timber/Dhajji is a live problem.** Dhajji-Dewari (timber-laced masonry, traceable to 12th-century Kashmiri urban construction) has documented strong real-world seismic performance in Kashmir and KPK, including in 2005. But the 2007 seismic provisions do not carry it as a recognised structural type with an R-factor and detailing rules. **Consequence: a Dhajji or timber-frame house today cannot be approved by code-table lookup.** It requires an engineer willing to analyse it and take responsibility. Say this to the client early; it is a schedule and cost item, not a footnote.

### 2.3 Section-level citations used in this skill

- ASCE 7-22 **Table 12.2-1** — R, Ω₀, Cd for light-frame CFS and steel systems. **Cite the specific printing/errata date you designed to** — see the citation-precision note at the end of §3.6; do not cite "ASCE 7-22" bare on a drawing.
- ASCE 7-22 **§12.8** — equivalent lateral force procedure
- ASCE 7-22 **Ch. 4, Table 4.3-1** — residential live loads
- ASCE 7-22 **§30** — components and cladding wind pressures (governs roof uplift on light roofs)
- AISI **S230-19** — prescriptive dwelling tables (stud/joist/header size, spacing, fastening, bracing)
- AISI **S240** §D, §E — wall, floor and roof framing requirements; §F web crippling and bracing
- AISI **S400** §E1-E3 — CFS light-frame shear walls (sheathed and strap-braced) seismic detailing
- AISC **360** Ch. F, H, J — flexure, combined forces, connections (portal frame members and haunches)
- IRC 2021 **Table R802.4.1(1)/(2)** (Ch. 8) — rafter spans, 20 psf roof live load, L/Δ = 180 (ceiling not attached) / 240 (ceiling attached)
- IRC 2021 **Table R802.5.1(1)/(2)** (Ch. 8) — ceiling joist spans
- IRC 2021 **Table R502.3.1** (Ch. 5) — floor joist spans
- IRC 2021 **Table R602.3(1)**, **R602.7** (Ch. 6) — fastening schedule, headers
- PKBC 2021 **Ch. 23** — Wood
- BCP-SP 2007 — seismic zoning, ELF (UBC-97 derived)

---

## Section 3: Light-Gauge Steel Framing (LGSF / CFS) — System Description

### 3.1 What it is

Galvanized cold-formed steel C-sections ("studs") seated in U-sections ("track"), screwed together into wall, floor and roof panels — dimensionally the same idea as North American 2×4/2×6 wood platform framing, executed in 0.5-2.5 mm galvanized steel. Panels are either **stick-built on site** (cut and screw in place) or, more commonly and more sensibly in Pakistan, **panelised in a factory** (roll-formed to length, punched, pre-assembled into wall panels) and bolted/screwed together on site.

**Structural model:** load-bearing stud walls carry gravity to a track and thence to the floor below or to the foundation. Lateral load is carried by **shear walls** — either sheathed panels (steel sheet or wood structural panel) or **flat strap X-bracing** in the stud cavity — never by the studs' bending alone.

### 3.2 Member designation (AISI S200 / SFIA universal designator)

```
        350 S 162 - 54
         │  │  │     └── design thickness in mils (1 mil = 0.001 in)
         │  │  └──────── flange width in 1/100 in  (162 = 1.62 in = 41 mm)
         │  └─────────── member type: S = stud/joist (C with lip)
         │                            T = track (U, no lip)
         │                            U = channel (cold-rolled)
         │                            F = furring
         └────────────── web depth in 1/100 in (350 = 3.50 in = 89 mm)
```

### 3.3 Thickness / gauge / grade table

| Mils | Common gauge | Design thickness (in) | Design thickness (mm) | Minimum Fy | Typical use |
|---|---|---|---|---|---|
| 18 | 25 ga | 0.0188 | 0.48 | 33 ksi / 230 MPa | Non-structural partitions, ceiling framing (AISI S220) |
| 27 | 22 ga | 0.0283 | 0.72 | 33 ksi / 230 MPa | Non-structural, tall partitions |
| 30 | 20 ga (drywall) | 0.0312 | 0.79 | 33 ksi / 230 MPa | Non-structural — **not interchangeable with 33 mil** |
| 33 | 20 ga (structural) | 0.0346 | 0.88 | 33 ksi / 230 MPa | Light load-bearing studs, single storey, short walls |
| 43 | 18 ga | 0.0451 | 1.15 | 33 ksi / 230 MPa | Load-bearing studs (typical single/upper storey), joists (short spans) |
| 54 | 16 ga | 0.0566 | 1.44 | 50 ksi / 340 MPa | **Workhorse**: load-bearing studs G+1, floor joists, headers |
| 68 | 14 ga | 0.0713 | 1.81 | 50 ksi / 340 MPa | Ground-floor studs of a 2-3 storey, long joists, headers, jamb studs |
| 97 | 12 ga | 0.1017 | 2.58 | 50 ksi / 340 MPa | Heavy headers, hold-down posts, boxed jambs |
| 118 | 10 ga | 0.1242 | 3.15 | 50 ksi / 340 MPa | Special hold-downs, transfer members |

**Galvanizing:** G60 (Z180, 180 g/m² total both faces) is the North American structural minimum. **In Pakistan specify G90 (Z275) minimum for anything in an external wall, and G90+ or a duplex coating for Karachi/coastal, high-humidity or any member within 500 mm of grade.** Cut ends must be touched up with a zinc-rich paint; punched service holes are pre-galvanized only if the coil was, so re-check.

### 3.4 Indicative load-bearing stud selection

> ⚠ **VERIFY.** The table below is an *indicative* planning aid consistent with the form of the AISI S230-19 prescriptive tables. It is **not** a transcription of the literal S230 table cells (which were not available at the resolution of this skill's research). For any real project, read the size, spacing, thickness and bracing directly from the AISI S230-19 PDF, or have the studs designed to AISI S100/S240. Do not quote these numbers to a fabricator.

Assumptions: residential loads (roof 20 psf LL, floor 40 psf LL per ASCE 7-22 Table 4.3-1), storey height ≤ 3.05 m (10 ft), sheathed both faces, wind ≤ 145 km/h (≈ 40 m/s) basic, low-moderate seismic.

| Condition | Stud | Spacing | Note |
|---|---|---|---|
| Single-storey, roof only | 350S162-33 (89 mm, 20 ga) | 600 mm o.c. | 400 mm o.c. if wind or opening density is high |
| Single-storey, roof + heavy tile/snow | 350S162-43 | 400 mm o.c. | Northern sites: check snow explicitly |
| G+1, upper-storey walls | 350S162-43 or 400S162-43 | 400-600 mm o.c. | |
| G+1, ground-storey walls | 400S162-54 (102 mm) or 600S162-43 (152 mm) | 400 mm o.c. | 152 mm depth buys insulation space as well as capacity |
| G+2, ground-storey walls | 600S162-54 / 600S162-68 | 400 mm o.c. | Approaching the S230 3-storey ceiling — engineer it |
| Jamb studs each side of an opening | Boxed pair or back-to-back, one gauge heavier than field studs | — | Count = f(header reaction); never a single field stud |
| Non-load-bearing partition, ≤ 3 m | 92S125-30 / 350S125-30 | 600 mm o.c. | AISI S220 scope |
| Non-load-bearing partition, 3-4.5 m | 400S162-33 / 600S162-33 | 400-600 mm o.c. | ASCE 7-22 may pull these into engineered scope in SDC B-F |

**Universal stud rules:**
- Studs must **bear directly on the track web** and be aligned within 3 mm of the framing member below ("in-line framing") so that axial load runs stud-over-stud-over-joist. Off-line framing forces the track to span in bending and it cannot.
- Every load-bearing stud needs **bridging/bracing** (cold-rolled channel through the punchouts + clip angle, or strapping both faces + blocking) at maximum **1220 mm (4 ft) vertical spacing** to control weak-axis and torsional buckling — this is the most commonly skipped item on Pakistani sites and the most consequential.
- **Web holes:** use factory punchouts only. Field-cut holes destroy the design; if a service must pass elsewhere, it needs a designed reinforcing plate.
- **Never weld cold-formed studs in the field.** At 0.9-1.4 mm the arc burns through, and it destroys the galvanizing on both faces. Screw them. (Welding is acceptable only in a controlled shop with procedure and re-coating.)

### 3.5 Indicative CFS floor joist and header spans

> ⚠ **VERIFY** against AISI S230-19 / manufacturer load tables. Indicative only.

Floor joists, 40 psf (1.9 kPa) live + 15 psf (0.7 kPa) dead, L/480 live-load deflection:

| Joist section | Depth | @ 400 mm o.c. | @ 600 mm o.c. |
|---|---|---|---|
| 550S162-43 | 140 mm | ~3.0 m | ~2.5 m |
| 800S162-43 | 203 mm | ~3.9 m | ~3.3 m |
| 800S162-54 | 203 mm | ~4.3 m | ~3.7 m |
| 1000S162-54 | 254 mm | ~5.0 m | ~4.3 m |
| 1000S162-68 | 254 mm | ~5.4 m | ~4.7 m |
| 1200S162-68 | 305 mm | ~6.2 m | ~5.4 m |
| 1200S200-97 | 305 mm | ~7.0 m | ~6.1 m |

**Serviceability, not strength, governs CFS floors.** A CFS floor that passes strength can still be unacceptably bouncy. Use **L/480 for live load** as the working limit for residential floors (not L/360), and add a rigid topping — 40-50 mm sand-cement screed on a cement-board deck, or a lightweight concrete topping on steel deck — for both damping and acoustics. A bare screwed-board CFS floor in a Pakistani house will generate complaints.

Headers (box or back-to-back C sections) over openings, single-storey roof load above:

| Opening clear width | Indicative header |
|---|---|
| ≤ 1.2 m | Box 2 × 350S162-54 |
| 1.2-1.8 m | Box 2 × 550S162-54 |
| 1.8-2.4 m | Box 2 × 800S162-54 |
| 2.4-3.0 m | Box 2 × 800S162-68 or 1000S162-54 |
| 3.0-4.0 m | Box 2 × 1000S162-68 / engineered |
| > 4.0 m | Hot-rolled steel beam or engineered CFS truss — leave prescriptive territory |

Add one full-height **jamb (king) stud** plus the required **cripple (jack) studs** each side; the header reaction must land on a continuous stack of studs down to the foundation. **Web crippling at header bearing** is a real limit state in CFS (AISI S240/S100) — bearing stiffeners are usually needed and are usually forgotten.

### 3.6 Lateral system — shear walls and strap bracing

| Shear-wall type | R (ASCE 7-22 Table 12.2-1) | Ω₀ | Cd | Pakistan practicality |
|---|---|---|---|---|
| CFS light-frame sheathed with **wood structural panels (OSB/ply) or steel sheet** rated for shear | **6½** | 3 | 4 | ⚠ OSB is not a mainstream Pakistani building material; ply of structural grade is inconsistent. **Steel sheet sheathing (0.68-0.84 mm screwed to studs) is the realistic route here.** |
| CFS light-frame using **flat strap X-bracing** | **4** | 2 | 3½ | ★ The most buildable option in Pakistan — flat galvanized strap is locally available |
| CFS light-frame with **shear panels of all other materials** (e.g. gypsum board, cement board) | **2** | 2½ | 2 | Very low R — quadruples design base shear vs sheathed. Do not rely on cement board as the SFRS |

> ⚠ **VERIFY** the R/Ω₀/Cd values against the specific published edition and printing of **ASCE 7-22 Table 12.2-1** in force at the date of design — table rows for CFS light-frame seismic force-resisting systems have shifted between successive editions and errata cycles, so "ASCE 7-22" alone is not a precise-enough citation to put on a drawing or a calculation. Record the printing/errata date actually used, and cross-check the matching **AISI S400** commentary cycle for consistency. The values above are quoted as commonly cited figures, not verified against a specific dated printing — **the §8.2 base-shear worked comparison inherits this same caveat**, and its numeric ratio must not be presented as a final design conclusion without that citation check.

**The Pakistan-specific trap:** designers copy a North American LGSF detail that assumes OSB shear sheathing, then substitute locally available cement board or gypsum because OSB cannot be sourced — and silently drop the R from 6½ to 2 while keeping the North American brace layout. That is a 3.25× under-design of the lateral system. **Decide the sheathing/bracing type first, then design the lateral system to the R that material actually earns.**

Strap-braced shear wall detailing essentials (AISI S400 §E):
- Straps on **both faces** of the wall in an X, anchored at panel corners.
- **Gusset plates** at each strap end, screwed to the chord stud *and* the track, with the screw group designed for the full strap yield force — the connection must not be the weak link (capacity design).
- **Chord studs boxed** (2 or more studs) — the strap force delivers a large axial couple into the end studs.
- **Hold-down at each end of every braced panel**, anchored to the foundation with a cast-in anchor rod, not a post-drilled wedge anchor unless specifically designed.
- Strap must be **pre-tensioned/snug** — a slack strap does nothing until the building has already moved.

### 3.7 Connections — screws and anchorage

| Connection | Fastener | Rule |
|---|---|---|
| Stud to track (each end, each flange) | #8 or #10 self-drilling pan/wafer head | Minimum **2 screws per stud end** (one per flange); more where axial load is transferred |
| Steel to steel, ≤ 43 mil combined | #8 self-drilling | — |
| Steel to steel, 54-97 mil | #10 or #12 self-drilling hex head | Drill point must exceed the combined thickness |
| Steel to steel, > 97 mil | #12-14 or bolted | Consider bolts; screws struggle |
| Sheathing (board) to studs | #6-#8 bugle head | 200 mm o.c. edges, 300 mm field (non-structural) |
| Shear-wall sheathing | #8/#10 | **50-100 mm o.c. at panel edges**, 300 mm field — the edge spacing *is* the shear capacity |
| Strap to gusset/chord | #10/#12 | Screw group designed to develop strap yield |
| Track to concrete foundation | Cast-in anchor rod, or designed post-installed anchor | **Maximum 1200 mm o.c.**, and within 300 mm of every panel end / corner / opening jamb |
| Hold-down to foundation | M16-M24 cast-in rod with plate washer, embedment per design | Not a shot-fired pin. Not a plastic plug. |
| Joist to track / rim | Clip angle + screws, or web stiffener + screws | Bearing stiffener at every point load |

**Screw rules that matter:**
- Minimum **edge distance = 1.5 × screw diameter**; minimum **spacing = 3 × diameter**.
- Screw must project **≥ 3 threads past the far face**, otherwise it has not engaged.
- **Do not over-drive.** A stripped screw hole in 0.88 mm steel has essentially zero pull-out capacity, and it looks fine from the outside. Use depth-limited or clutch drivers on shear walls.
- Bimetallic/stainless screws for anything in a wet or coastal zone — carbon-steel screws in galvanized steel at the coast is the fastest corrosion path in the building.

### 3.8 Envelope, fire, thermal and acoustic realities

| Issue | Physics | Required response in Pakistan |
|---|---|---|
| **Thermal bridging** | A steel stud has ~350-400× the conductivity of wood. Steel studs at 400 mm o.c. can degrade the *effective* R-value of cavity insulation by **40-60%** | **Continuous exterior insulation is mandatory, not optional**: 25-50 mm XPS/EPS/PIR outside the studs, or a thermal-break strip on every stud face. Cavity insulation alone is close to wasted |
| **Low thermal mass** | RCC/brick stores and delays the heat pulse; an LGSF wall does not. Indoor peak temperature tracks outdoor peak with a short lag | High insulation + deep shading + light-coloured roof + night ventilation. In Multan/Jacobabad, an uninsulated LGSF house will be **hotter than a brick one**, and the client will blame the system, correctly |
| **Fire** | Steel is non-combustible but loses ~50% of yield strength by ~600 °C, faster than a heavy timber section chars | Rated gypsum board: 1 × 12.5-15 mm Type X each face ≈ 45-60 min; 2 layers ≈ 90-120 min. Fire-stop every wall/floor junction and every service penetration |
| **Acoustics** | Lightweight walls transmit airborne sound; steel studs are worse than wood because they are stiff | Resilient channel or staggered studs, mineral wool in the cavity, 2 board layers. For a floor: screed topping + resilient layer |
| **Corrosion** | Galvanic and atmospheric | Z275 min externally, seal all penetrations, keep steel ≥ 200 mm above finished grade, never embed a stud in masonry or soil, isolate from copper/brass |
| **Condensation** | Steel is the coldest surface in the wall; interstitial condensation corrodes from the inside | Vapour control layer on the warm side (in Pakistan's cooling-dominated climate, the *outside* for much of the year — this needs actual hygrothermal thought, not a copied detail) |
| **Fixings for occupants** | Nobody can hang a shelf on a 0.88 mm stud with a plastic plug | Provide **noggings/blocking** at TV, cabinet, geyser, AC bracket, curtain and grab-rail locations *during framing* and record them on an as-built plan. Missing this is the #1 owner complaint |

### 3.9 Pakistan availability and cost (2026)

| Item | Position |
|---|---|
| Supply base | A handful of specialised fabricators/roll-formers (prefab and LGS building suppliers such as Pak Insulation and the Portaking-type prefab market). **Not a mainstream trade.** No general contractor will have an LGSF crew; the supplier's own crew erects |
| Cost | **~PKR 3,500/sq ft** quoted for panel-built LGSF prefab homes (insulated walls, basic facilities), per Pakistani prefab supplier pricing |
| RCC baseline it competes with | **PKR 2,800-3,500/sq ft** grey structure in most cities; **PKR 3,200-5,800/sq ft** in Islamabad (to ~PKR 6,000 in premium DHA sectors) |
| Verdict on cost | **Roughly at parity to slightly above RCC grey structure in most cities; potentially competitive in Islamabad and clearly competitive against premium-sector RCC.** It does not win on cost outside the north/premium markets — it wins on speed, weight and site access |
| Real constraint | **Labour and expertise, not material.** Screw-gun discipline, bridging, hold-downs and shear-wall edge spacing are all skills the local trade does not have. Assume a supplier-led, supervised erection or accept a badly built frame |
| Lead time | Factory roll-forming and panelisation typically 2-3 weeks; erection of a 2,000 sq ft shell 1-2 weeks; full finish 6-10 weeks |
| Hidden costs | Continuous exterior insulation; imported or scarce sheathing boards; rated gypsum; hold-down anchors; the RCC plinth/raft you still have to pour; the higher-spec envelope needed to make the house comfortable |

> **Scope warning — do not net these against each other:** it is common to see the Pakistani ~PKR 3,500/sq ft figure quoted alongside a US stick-framing labour-and-material rate of roughly **$2-4/sq ft** as if they were comparable. They are not, for at least three reasons: different currencies at a floating exchange rate, different scope (the Pakistani figure is a turnkey-ish panelised quote including "basic facilities"; the US figure is framing labour and material *only* — no panels, no insulation, no finish), and different markets (US volume-built subdivision framing vs a bespoke Pakistani prefab supplier quote). **Treat the two figures as separate reference points from different contexts, never as a ratio or a "how much cheaper/more expensive" comparison** — consistent with the scope discipline in §7.1.

---

## Section 4: LGSF — Assembly Anatomy (for modelling and detailing)

```
ROOF:      trussed rafters (CFS) or CFS rafters @ 600 o.c.
              ↓ every truss/rafter tied to the wall top track with a designed
                uplift clip — this is the load path that actually fails in wind
TOP TRACK  ──────────────────────────────────────────────
STUDS      │ │ │ │ │ │  @ 400/600 o.c., in-line with joists below
           ├─┼─┼─┼─┼─┤  bridging @ ≤ 1220 mm vertically (CRC through punchouts + clips)
           │╲│ │ │ │╱│  flat strap X-brace on braced panels, BOTH faces
BOT TRACK  ══════════════════════════════════════════════
              ↓ anchor rods ≤ 1200 o.c. + hold-down at every braced-panel end
FLOOR:     CFS joists @ 400 o.c. + rim track + web stiffeners at bearings
              screed/topping over deck board
GROUND:    RCC raft or strip/pad + plinth beam  ← still concrete. LGSF does not
                                                   remove the foundation trade
```

**Non-negotiable LGSF checklist (run on every model and every drawing set):**

- [ ] Studs in-line with joists and with studs above/below (≤ 3 mm eccentricity)
- [ ] 2 screws minimum at every stud-to-track connection
- [ ] Bridging/bracing at ≤ 1220 mm vertically on every load-bearing wall
- [ ] Web stiffeners at every concentrated bearing (header ends, joist bearings, beam supports)
- [ ] Boxed jamb studs each side of every opening > 900 mm
- [ ] Continuous stud stack from every header reaction down to the foundation
- [ ] Shear walls identified on plan with their sheathing/bracing type and edge screw spacing
- [ ] Hold-down at each end of each shear wall, anchored into concrete
- [ ] Anchor rods ≤ 1200 mm o.c. and within 300 mm of panel ends and corners
- [ ] **Continuous uplift path**: sheeting → purlin/rafter → clip → top track → stud → bottom track → anchor → foundation, with no "assume friction" link
- [ ] Continuous exterior insulation specified
- [ ] Blocking/noggings scheduled for every wall-hung item (geyser, AC, TV, cabinets, grab rails)
- [ ] Z275 galvanizing specified externally; cut ends touched up
- [ ] Steel ≥ 200 mm above finished grade everywhere

---

## Section 5: Structural Steel Portal Frames — System Description

### 5.1 Anatomy

```
              apex splice (bolted, 4-8 bolts)
                       ╱╲
                     ╱    ╲        rafters, pitch 6°-20°
        haunch ▄▄▄ ╱        ╲ ▄▄▄ haunch
              ║                  ║
              ║ column           ║ column      eaves height h
              ║                  ║
        ══════╩══════      ══════╩══════  base plate, nominally pinned (4 HD bolts)
         pad footing            pad footing
              └───── tie beam / tie rod resisting horizontal thrust ─────┘

  Secondary steel: Z-purlins on rafters @ 1.2-1.8 m; C/Z side rails on columns;
                   eaves beam; cross-bracing in end bays (roof plane + wall plane);
                   sag rods on long purlin runs.
```

**Frame spacing (bay):** 4.5-7.5 m, **6.0 m typical**. Wider bays = fewer frames but heavier purlins and frames; the optimum for houses is usually 4.5-6.0 m because it aligns with room and window modules.

### 5.2 Economical span range and the residential reality check

| Span | Verdict for a house |
|---|---|
| < 9 m (30 ft) | Portal frame is **oversized as a concept**. A simple beam-and-column steel frame, or an RCC beam, is simpler and cheaper. Use portal only if the same detail repeats many times |
| 9-12 m (30-40 ft) | Entering the sensible range. Competitive with a deep RCC transfer beam, much faster |
| **12-30 m (40-100 ft)** | **The economical range** (published economical span band 40-150 ft, optimum 60-100 ft). This is industrial-shed scale |
| > 30 m | Fine structurally; almost never a house |

**Say this out loud to clients:** the portal frame's cost advantage in Pakistan is measured on *industrial sheds* — big rectangular volumes with sheeted envelopes and no internal subdivision. A house is small, subdivided, and needs a finished envelope. **Applying shed economics to a subdivided house is the single most common error with this system.** Portal frames earn their place in a house at the *specific volume that needs the clear span* — the great room, the double-height hall, the garage/workshop, the covered court — usually as an annexe or a wing, with the bedrooms in masonry.

### 5.3 Preliminary member sizing — span/depth ratios

**Rule:** rafter depth ≈ **span/40 to span/55** for UB sections (span/40 to span/50 for AISC W sections). Columns are typically the **same serial size or one size deeper** than the rafter.

| Clear span | Rafter depth range (span/55 → span/40) | Indicative rafter section | Indicative column |
|---|---|---|---|
| 9 m (30 ft) | 165-225 mm | UB 254×102×25 / W10×22 | UB 254×146×31 |
| 12 m (40 ft) | 220-300 mm | UB 305×102×33 / W12×26 | UB 305×165×40 |
| 15 m (50 ft) | 275-375 mm | UB 356×127×39 / W14×34 | UB 356×171×45 |
| 18 m (60 ft) | 330-450 mm | UB 406×178×54 / W16×40 | UB 406×178×60 |
| 21 m (70 ft) | 380-525 mm | UB 457×191×67 | UB 457×191×74 |
| 24 m (80 ft) | 435-600 mm | UB 533×210×82 | UB 533×210×92 |
| 27 m (90 ft) | 490-675 mm | UB 610×229×101 | UB 610×229×113 |
| 30 m (100 ft) | **550-750 mm** | UB 610×229×125 / 686×254×125 | UB 686×254×140 |

> The 30 m → 550-750 mm figure is the anchor data point; the rest of the table is the same span/40-55 rule applied consistently. All of it is **preliminary massing only** — final sections come from analysis with the actual loads, the actual haunch stiffness, the actual restraint positions, and a stability (P-Δ / member buckling) check.

**Haunch rules:**
- **Haunch depth = 1.5 to 2.0 × rafter depth** (i.e. total depth at the eaves ≈ 2-3 × rafter depth).
- **Haunch length = span/10 to span/7.** For a 30 m span that is **3.0-4.5 m**; for a 12 m span, 1.2-1.7 m.
- Haunches are cut from the same serial-size section (a rafter offcut welded under the rafter) — cheap, and it makes the bolted moment connection possible.
- **The haunch dictates the internal head height at the eaves.** On a house this is a *planning* issue: a 12 m span with a 1.5 m haunch eats headroom over the perimeter 1.5 m of floor. Model it before locating anything against that wall.

**Restraint:** the **inside (bottom) flange of the rafter near the eaves and the inside flange of the column are in compression under gravity load and are unrestrained by the purlins.** They need **fly braces / knee braces** from the purlin or side rail to the inside flange. Missing fly bracing is the classic portal-frame failure mode — the frame looks complete and fails by lateral-torsional buckling. Show them on the model and the drawings.

### 5.4 Secondary steel

| Element | Typical | Rule |
|---|---|---|
| Purlins | Z 150-200 mm deep, 1.5-2.5 mm, galvanized | Spacing **1.2-1.8 m**; sleeved/overlapped over frames for continuity; sag rods at mid-span on runs > 6 m |
| Side rails | C/Z 150-200 mm | Spacing 1.5-2.0 m; sag rods |
| Eaves beam | C or hollow section | Ties frames, supports gutter and the top of the wall cladding |
| Roof plane bracing | Circular hollow section or angle cross-bracing in **end bays** and at intervals ≤ 5 bays | Carries wind from the gable into the wall bracing |
| Wall bracing | Cross-bracing or a portalised bay | **Must exist in the longitudinal direction** — the portal frame only resists load in its own plane |

**The most common conceptual error:** a portal frame is a **moment frame in one direction only**. In the longitudinal direction it is a pin-jointed mechanism until braced. Every portal-frame building needs an explicit longitudinal bracing system. On a house where the end walls are masonry, the masonry can sometimes serve — but only if it is actually detailed and designed as a shear wall connected to the steel, not just built between the columns.

### 5.5 Connections

| Connection | Typical detail | Notes |
|---|---|---|
| **Eaves (rafter-to-column)** | Bolted extended end-plate moment connection through the haunch. 20-25 mm end plate; **8-12 bolts M20/M24 grade 8.8** in two vertical rows, concentrated in the tension zone (top) | Designed to AISC 360 Ch. J / equivalent. Bolt group, end-plate bending, column flange bending, web panel shear and stiffeners all check separately |
| **Apex** | Bolted end-plate splice, **4-8 bolts M20/M24**, often with a small haunch | Site splice — locate it where the crane and the transport length allow |
| **Base** | Base plate 20-30 mm, **4 holding-down bolts M20-M24**, embedment 375-450 mm with plate washer/anchor plate, grout bed 25-40 mm | Designed as **nominally pinned**. 4 bolts give some real fixity; analysis commonly assumes 10-20% base fixity for deflection only, and pinned for strength — the engineer must be explicit which |
| **Purlin to rafter** | Purlin cleat welded/bolted to rafter, 2 bolts M12/M16 | Cleat position sets the roof plane; get it right in the model |
| **Fly brace** | Angle from purlin/side rail to inside flange, bolted both ends | Never omit |
| **Bracing** | HSS/angle with gusset plates, or tension rods with turnbuckles | Pre-tension rod bracing |

**Field welding vs bolting:** Pakistani PEB practice is **shop-weld, site-bolt**. Keep it that way. Field welding on a house site means no NDT, no procedure control, weather exposure, and paint damage. If a detail requires field welding, redesign the detail.

**Corrosion protection:** shop blast to Sa 2½, zinc-rich primer + intermediate + finish, or hot-dip galvanize the secondary steel. **Karachi coastal: specify the paint system by exposure category (ISO 12944 C4/C5-M), not by "two coats of enamel".**

### 5.6 The base thrust problem (the thing that bites)

A pitched portal frame pushes **outward** at its bases. That horizontal thrust must go somewhere.

**Hand check (conservative, three-hinged idealisation):**

```
H ≈ w · L² / (8 · f)

  w = load per metre along the frame = (roof load in kPa) × (bay spacing in m)
  L = span (m)
  f = rise from eaves level to apex (m) = (L/2) · tan(pitch)
```

**Worked: 12 m span, 6 m bay, factored roof load 1.5 kPa, two pitch options**

| Pitch | f = 6·tan(θ) | w = 1.5 × 6 = 9 kN/m | H ≈ wL²/(8f) |
|---|---|---|---|
| 6° | 0.63 m | 9 kN/m | **257 kN** per base |
| 10° | 1.06 m | 9 kN/m | **153 kN** per base |
| 15° | 1.61 m | 9 kN/m | **101 kN** per base |
| 20° | 2.18 m | 9 kN/m | **74 kN** per base |
| 25° | 2.80 m | 9 kN/m | **58 kN** per base |

**Read the table.** Halving the thrust by steepening the roof from 6° to 20° is free structural performance and it also sheds monsoon rain better. Flat-ish shed pitches are an industrial habit; on a house, **15-25° is usually the right answer** for thrust, drainage, tile compatibility, and looking like a house.

> A real two-hinged frame with stiff members and haunches carries part of this in bending, so the analysed H is lower than the three-hinged hand value. **Use the formula as a conservative order-of-magnitude sanity check on the foundation, never as the design value.**

**Resolving the thrust — pick one and show it on the drawings:**
1. **Tie rod / tie beam** between opposing bases, cast into or under the ground slab. Cheapest, most reliable. *The rod must be protected from corrosion and must not be cut by a later plumber.*
2. **Moment-resisting pad footings** — much larger pads, sized for the overturning couple. Expensive; often 2-3× the pad size.
3. **Passive soil resistance on a deepened pad / shear key** — only with a geotechnical report that supports it.
4. **A stiff RCC ground beam ring** around the building.

**Never** leave it to "the floor slab will hold it". An unreinforced ground slab is not a tie, and the moment somebody saw-cuts a service trench across it, the frame spreads.

### 5.7 Pakistan cost, speed and supply (2026)

| Item | Figure | Source context |
|---|---|---|
| PEB / portal shed **structure only** | **PKR 1,800-2,000/sq ft** | Pakistani PEB supplier pricing, industrial shed spec |
| Foundation | **PKR 270-400/sq ft** | as above |
| **PEB all-in shell** | **PKR 2,100-2,500/sq ft** | as above |
| Traditional (RCC/masonry) equivalent-footprint building | **PKR 4,000-6,000/sq ft** | as above (warehouse/large-span comparison, not a small house) |
| Erection speed | Prefabricated portal frames erect **~40% faster** than conventional steel; Pakistani PEB sheds bolt together in **25-30 days** vs **6-12 months** for traditional construction of comparable footprint | as above |
| Steel grade | **IS 2062 Grade E350** plate/sections is the common Pakistani PEB spec | as above |

**Mandatory caveat whenever these numbers are quoted:** the PKR 2,100-2,500/sq ft figure is a **sheeted industrial shell** — steel frame, purlins, single-skin or lightly insulated sheeting, a slab. It contains **no** internal partitions, no ceilings, no insulation to residential standard, no plaster, no MEP fit-out, no joinery, no flooring, no residential-grade thermal or acoustic performance. To reach a finished house standard, add a realistic **PKR 1,500-3,000/sq ft** of envelope and fit-out on top. **Present it as a shell-cost comparison, never as a like-for-like finished-house cost**, and say so before the client does the arithmetic themselves.

---

## Section 6: Timber Framing

### 6.1 Regional viability in Pakistan — be blunt

| Region | Viability | Reason |
|---|---|---|
| **KPK (Hazara, Swat, Chitral, Dir), Gilgit-Baltistan, AJK** | ★★★ Genuinely viable | Deodar and pine supply chain, living carpentry trade, cold/moderate climate suits timber, traditional Dhajji/Bhatar know-how, difficult site access makes RCC expensive, low termite pressure at altitude |
| **Murree / Galiyat / Nathiagali belt** | ★★ Viable | Same supply chain, tourism/holiday-home market that wants timber, but higher fire risk in dense hillside development |
| **Punjab (Lahore, Rawalpindi, Faisalabad, Multan)** | ✗ Not realistic as a primary structure | No structural-timber supply chain, no framing carpentry trade, **severe subterranean termite pressure**, high summer temperatures and monsoon damp, no code-familiar plan checkers, near-zero resale acceptance |
| **Sindh (Karachi, Hyderabad, interior)** | ✗ Not realistic | As above plus coastal humidity and salt |
| **Balochistan** | ✗ (except limited northern pockets) | No supply chain |

**Rule:** if the site is not in the northern belt, timber framing is a **roof-and-joinery material, not a structural system**. Timber roof trusses/rafters over masonry walls remain perfectly sensible everywhere (§8.3) — that is a hybrid, not timber framing.

### 6.2 Species

| Species | Local name | Density (kg/m³) | Structural use | Notes |
|---|---|---|---|---|
| **Cedrus deodara** | **Deodar / Diyar** | ~550-580 | **The** structural species: beams, joists, rafters, posts, ceiling boarding | Straight grain, dimensionally stable, natural oils give real fungal and insect resistance. Regulated/protected in places — check legality of supply |
| *Pinus wallichiana / roxburghii* | Kail / Chir | ~500-550 | Secondary framing, rafters, purlins | Lower natural durability; **requires preservative treatment**; resinous |
| *Abies pindrow / Picea smithiana* | Partal / Fir, Spruce | ~420-480 | Internal, non-exposed only | Low durability. Do not use in contact with masonry or outdoors |
| *Dalbergia sissoo* | Shisham / Tali | ~750-800 | Joinery, doors, furniture, occasional posts | Hard, durable, expensive, prone to twist in long lengths. Uneconomic as framing |
| *Populus / Eucalyptus* | Poplar, Sufaida | ~380-550 | **Formwork/shuttering only** | Not a structural framing timber |
| Imported softwood | Malaysian/NZ pine, "yellow pine" | ~450-520 | Framing where imported supply is organised | Usually kiln-dried and gradeable — an advantage over ungraded local stock |

**Indicative permissible stresses for Deodar** (Group B softwood, inside/dry location): bending ≈ **9-10 N/mm²**, E ≈ **9,400 N/mm²**, density ≈ 560 kg/m³.
> ⚠ **VERIFY** against **PKBC 2021 Chapter 23** (the citable Pakistani authority) and/or IS 883 grade tables before any design use. These values are indicative and were not verified cell-by-cell in this skill's research.

**The grading problem.** Pakistani timber is sold by species and by the cubic foot, **not by structural grade**. There is no routine stress-grading, no stamped grade mark, no moisture-content certificate. Consequences:
- Apply a **conservative grade assumption** and a generous factor of safety, or organise independent grading.
- **Moisture content matters more than anything else.** Green timber at 30%+ MC will shrink, twist, split at fasteners, and drop out of a joist hanger. Specify ≤ 18-20% MC at installation for framing, ≤ 12% for internal joinery; expect to season/stack on site.
- Reject: excessive slope of grain, large knots at mid-span in the tension face, wane at bearings, shakes, insect holes, fungal staining.

### 6.3 Indicative timber span tables

> ⚠ **VERIFY.** Reconstructed indicatively in the form of IRC 2021 Tables R802.4.1 / R802.5.1 (Ch. 8) / R502.3.1 (Ch. 5) for a #2 grade softwood. **Not** a transcription of literal IRC table cells, and **not** calibrated to Deodar's actual graded properties. Use for preliminary FreeCAD geometry only; design to PKBC 2021 Ch. 23 with real graded stresses.

**Rafters — 20 psf (0.96 kPa) roof live load, 10-15 psf dead, no snow:**

| Member (nominal) | Actual (mm) | @ 400 mm o.c. | @ 600 mm o.c. | Deflection basis |
|---|---|---|---|---|
| 2×4 | 38×89 | ~2.7-3.0 m | ~2.3-2.6 m | L/180 (ceiling not attached) per R802.4.1(1) |
| 2×6 | 38×140 | ~4.2-4.4 m | ~3.6-3.8 m | " |
| 2×8 | 38×184 | ~5.5-5.8 m | ~4.7-5.0 m | " |
| 2×10 | 38×235 | ~6.8-7.1 m | ~5.9-6.2 m | " |
| 2×12 | 38×286 | ~8.0-8.3 m | ~6.9-7.2 m | " |

Where the **ceiling is attached to the rafters** (cathedral ceiling), the deflection limit tightens to **L/240** per Table R802.4.1(2) and spans reduce by roughly 8-12%. **In the northern belt, snow governs and these spans do not apply** — get the ground snow load and use the correct table (ASCE 7-22 Ch. 7 / PKBC snow map).

**Ceiling joists — 20 psf attic live load (limited storage), L/240:** approximately the rafter spans above less ~10%. Uninhabitable attic with no storage (10 psf) allows ~15-20% more. Per Tables R802.5.1(1)/(2).

**Floor joists — 40 psf (1.9 kPa) live, L/360 (per IRC Table R502.3.1, Ch. 5):**

| Member | Actual (mm) | @ 400 mm o.c. | @ 600 mm o.c. |
|---|---|---|---|
| 2×6 | 38×140 | ~2.6 m | ~2.3 m |
| 2×8 | 38×184 | ~3.5 m | ~3.0 m |
| 2×10 | 38×235 | ~4.4 m | ~3.8 m |
| 2×12 | 38×286 | ~5.1 m | ~4.4 m |

**Headers over openings (IRC R602.7 form, Ch. 6), single storey + roof above, ~6 m building width:**

| Opening | Header |
|---|---|
| ≤ 1.0 m | 2 × 2×6 |
| 1.0-1.5 m | 2 × 2×8 |
| 1.5-2.1 m | 2 × 2×10 |
| 2.1-2.7 m | 2 × 2×12 |
| > 2.7 m | Engineered (built-up, flitch plate, glulam, or a steel beam) |

Add one **king stud** and the required **jack studs** each side, and a continuous bearing stack to the foundation.

### 6.4 Platform frame anatomy

```
ROOF  rafters @ 400/600 + ridge board; COLLAR TIES in the upper third;
      RAFTER TIES (or the ceiling joists acting as ties) at the plate line —
      without a tie, the rafters push the walls out. Same physics as §5.6.
      ↓ hurricane/uplift strap at EVERY rafter-to-plate connection
DOUBLE TOP PLATE  (laps at corners and intersections tie the walls together)
STUDS  38×89 or 38×140 @ 400/600 o.c.; blocking/noggings at mid-height
SOLE PLATE
────── floor deck (sheathing) nailed to ──────
JOISTS @ 400/600 + rim joist + solid blocking over supports
────── SILL PLATE: pressure-treated, on a DPC, anchor-bolted ──────
MASONRY / RCC PLINTH WALL, top ≥ 200 mm (preferably 450 mm) above finished grade
STRIP FOOTING
```

**Lateral system:** sheathed shear walls (structural ply) or let-in/flat strap bracing, with hold-downs at panel ends. Same principle as CFS: the studs do not resist lateral load; the diaphragm and shear walls do.

### 6.5 Timber connections

| Connection | IRC R602.3(1)-style rule | Note |
|---|---|---|
| Stud to sole plate | 4 × 8d toe-nail, or 2 × 16d end-nail | |
| Sole plate to joist/blocking | 16d @ 400 mm o.c. | |
| Double top plate | 16d @ 600 mm o.c., **laps ≥ 600 mm**, 8 × 16d at each lap | The lap is what makes the wall continuous |
| Rafter to top plate | 3 × 10d toe-nail **plus a designed uplift strap** | Toe-nails alone do not resist wind uplift |
| Ceiling joist to rafter (heel) | Nail count per IRC Table R802.5.2 — a function of span, pitch and snow | This is the tension tie; it is not a nominal connection |
| Collar tie to rafter | 4 × 10d, in the **upper third** of the rafter height | Resists ridge separation |
| Joist to beam/ledger | **Metal joist hanger** with the manufacturer's full nail pattern | Never a nailed-on ledger strip alone for anything structural |
| Built-up beam plies | 2 rows of 16d @ 400 mm o.c., staggered | |
| Sheathing to framing | 8d @ 150 mm edges / 300 mm field (shear walls: 100 mm or 75 mm edges) | Edge spacing *is* the shear capacity |
| Sill plate to foundation | M12-M16 anchor bolts, **≤ 1800 mm o.c.**, ≥ 2 per plate piece, within 300 mm of each end, plate washers | Plate washers, not standard washers — a standard washer pulls through |
| Bolted connections | Min edge distance 4d, end distance 7d in tension, spacing 4d | Pre-drill 1.0-1.2 × bolt diameter |

**Timber connection principles:**
- **Nails in withdrawal are worthless.** Every uplift and tension path uses straps, hangers or bolts, never nail withdrawal.
- **Metalwork must be compatible with treated timber.** Copper-based preservatives corrode plain steel connectors — use hot-dip galvanized (ideally to a heavy class) or stainless.
- **Timber shrinks across the grain, not along it.** Never stack members so that cumulative cross-grain shrinkage sits in a load path (the classic multi-storey platform-frame shrinkage problem). Detail slip joints at masonry/timber interfaces.
- **Split at the fastener = failed connection.** Pre-drill near ends, and never fasten green timber tightly.

### 6.6 Dhajji-Dewari and seismic performance

**What it is:** a timber frame — posts, horizontal members and **diagonal braces** forming small closed panels — with the panels infilled with brick, stone or mud masonry. The timber lacing subdivides the masonry into small confined cells.

**Why it performs:** the masonry cannot form long crack paths (each panel is small and confined), the timber frame's nailed/pegged joints dissipate energy through friction and local yielding, the whole assembly is **light**, and even after severe cracking the timber lacing holds the debris in place, so partial damage does not become collapse. The technique is traceable to **12th-century Kashmiri urban construction**, and its performance in real Himalayan earthquakes — including 2005 — is documented.

**The code gap, stated plainly:** **BCP-SP 2007 does not explicitly incorporate wood-frame or timber-laced masonry as a recognised structural type.** There is no R-factor, no prescriptive detailing chapter, no design example. **PKBC 2021 Chapter 23 "Wood"** gives material provisions but is not a Dhajji design manual.

**Practical consequence:**
1. A Dhajji or timber-frame house **cannot be approved by looking up a code table.** It needs an engineer's analysis and judgement.
2. UN-Habitat / ERRA / NESPAK post-2005 reconstruction guidance and the academic literature on Dhajji seismic performance are the practical detailing references. Cite them; do not pretend they are code.
3. Expect the plan checker to be unfamiliar. Submit with an explanatory note and the engineer's calculations.
4. **Never present a Dhajji design as "code compliant".** Present it as "an engineered design based on documented traditional practice, outside explicit BCP-SP 2007 prescriptive coverage, requiring the engineer's analysis and stamp".

**Dhajji detailing essentials:** continuous vertical posts from plinth to eaves; horizontal members at ≤ 900-1200 mm; diagonal braces in every panel; panel size kept small (typically ≤ 900 × 1200 mm); infill built tight into the frame; timber never in contact with the ground (masonry plinth ≥ 450 mm); a continuous timber wall plate at eaves tying the whole perimeter; light roof.

### 6.7 Durability — the constraint that decides everything outside the north

| Threat | Where | Mitigation (all of them, not some) |
|---|---|---|
| **Subterranean termites** | Severe in Punjab and Sindh, moderate in lower KPK | Pressure-treated (CCA/ACQ/borate) sill and any member within 450 mm of grade; a physical termite barrier or treated soil zone; ≥ 200 mm (prefer 450 mm) clearance above finished grade; no timber-to-soil contact anywhere, ever; annual inspection access |
| **Fungal decay** | Anywhere with damp: monsoon, plumbing leaks, condensation, rising damp | DPC under every sill plate; ventilate the underfloor void; keep MC < 20%; roof overhangs and drips; never bury timber in masonry without an air gap and a DPC wrap |
| **Powder-post beetle** | Ubiquitous | Borate treatment; reject infested stock at delivery |
| **Fire** | Everywhere; acute in dense hillside settlements | Softwood chars at **~0.6-0.8 mm/min**; oversize members for a required char depth, or line with rated gypsum. **Fire-stop every cavity** at floor and wall junctions — an unstopped timber cavity is a chimney |
| **Shrinkage/movement** | Everywhere, worst with green timber | ≤ 18-20% MC at installation; slip joints at masonry interfaces; no cumulative cross-grain shrinkage in load paths |
| **UV/weathering** | Exposed members | Coating maintenance cycle stated to the owner in writing (typically 3-5 years) |

### 6.8 Pakistan timber cost and supply

**No verified 2026 PKR/cft rate is carried in this skill** — the research behind this file did not return reliable current timber market rates, and fabricating one would be worse than useless.

To price a timber scheme, get **current per-cubic-foot rates by species and section from an actual timber market** (Ravi Road Lahore, Peshawar and Rawalpindi timber markets, or the local mandi in the northern district), and separately price: seasoning/kiln drying, preservative treatment, connectors and straps (often imported), skilled carpentry labour, and the maintenance cycle. **Compare that total against the RCC grey-structure baseline of PKR 2,800-3,500/sq ft (PKR 3,200-5,800 in Islamabad)** for the same footprint.

Expect the honest answer in most of Pakistan to be: **timber framing is not cheaper**, and it wins only in the north where local supply, difficult access and seismic performance combine.

---

## Section 7: Cost, Speed and Weight — The Comparison Tables

### 7.1 Cost (Pakistan, 2026)

| System | Structure/shell rate | What that rate includes | What it excludes |
|---|---|---|---|
| **RCC frame + brick infill** (baseline) | **PKR 2,800-3,500/sq ft** general; **PKR 3,200-5,800/sq ft** Islamabad (to ~PKR 6,000 premium DHA) | Grey structure: foundation, frame, slabs, walls, plaster, roof | Finishes, MEP fit-out, joinery, fixtures |
| **LGSF panel prefab** | **~PKR 3,500/sq ft** | Panel-built insulated walls + basic facilities per supplier quote | Verify inclusions line by line; foundation may or may not be in |
| **Steel portal / PEB** | **PKR 1,800-2,000/sq ft** structure + **PKR 270-400/sq ft** foundation = **PKR 2,100-2,500/sq ft** | Frame, purlins, sheeting, foundation — **industrial shed spec** | Everything that makes it a house: partitions, insulation, ceilings, MEP, finishes (add ~PKR 1,500-3,000/sq ft) |
| **Timber framing** | No verified 2026 rate — price from the local timber market | — | — |
| Traditional construction, large-span equivalent | **PKR 4,000-6,000/sq ft** | Comparator quoted against PEB for warehouse-scale buildings | Not a small-house rate |

**Input material rates (2026, for cross-checking any quote):**

| Material | Rate | Note |
|---|---|---|
| Steel reinforcement (rebar) | **PKR 270-320/kg** | Represents **25-30% of grey structure cost** — the single biggest swing factor in an RCC quote |
| Cement | **PKR 1,350-1,610 per 50 kg bag** | |

**How to use these honestly:**
1. Always compare **the same scope**. Shell-to-shell or finished-to-finished. Never shell-to-finished.
2. Always name the **city**, because Islamabad RCC (3,200-5,800) and Faisalabad RCC (2,800-3,500) are different competitions.
3. Always separate **structure cost** from **envelope cost**. Lightweight systems shift cost from the frame into the envelope; that money does not disappear.
4. Always add the **foundation**, which none of these systems removes.
5. State the **date** of the rates. Pakistani steel and cement prices move fast enough that a six-month-old comparison is fiction.
6. Never compare figures quoted in **different currencies or from different national markets** (e.g. a Pakistani PKR/sq ft quote against a US $/sq ft framing rate) as if they were a direct ratio — see the scope warning in §3.9.

### 7.2 Programme

| Phase | RCC/masonry G+1 (~2,000 sq ft) | LGSF | Steel portal (shell) |
|---|---|---|---|
| Design + approval | 4-10 weeks | 4-10 weeks (+ extra for an unfamiliar plan checker) | 4-10 weeks |
| Fabrication / procurement | — (material on demand) | 2-3 weeks factory panelisation | 3-6 weeks shop fabrication |
| Foundation | 3-5 weeks | 2-4 weeks | 3-4 weeks |
| Superstructure / erection | **6-12 months total build** | 1-2 weeks erection | **25-30 days** to bolt the shell together |
| Envelope + finishes | (included above) | 6-10 weeks | 8-16 weeks (from bare shell to house) |
| **Realistic total** | **6-12 months** | **3-5 months** | **3-6 months** for a finished house; ~1 month for a usable shed |

Prefabricated portal frames erect **~40% faster** than conventional site-fabricated steel — the gain is in the shop, not on site.

### 7.3 Weight (this is the number that drives seismic and foundations)

| Assembly | Unit weight | Comment |
|---|---|---|
| 150 mm RCC slab + 40 mm finishes | ~5.1 kPa | 0.15 × 24 = 3.6 kPa + 1.5 |
| 230 mm brick masonry wall | ~4.4 kPa of wall face (≈ **13 kN/m** run at 3 m height) | 19 kN/m³ |
| 115 mm brick partition | ~2.2 kPa of wall face | |
| CFS floor: joists + deck board + 40 mm screed | ~1.8-2.5 kPa | The screed is most of it |
| CFS wall: studs + board both faces + insulation | ~0.5-0.7 kPa of wall face (≈ **2 kN/m** run at 3 m) | **~15% of a brick wall** |
| Timber platform floor: joists + deck | ~0.8-1.2 kPa | |
| Timber stud wall + boards | ~0.5-0.8 kPa of wall face | |
| Light roof: sheeting + purlins + insulation + ceiling | ~0.4-0.6 kPa | |
| Tiled roof on timber/steel | ~0.9-1.3 kPa | |
| RCC roof slab | ~4.5-5.1 kPa | |

---

## Section 8: Seismic and Wind — Worked Comparison

### 8.1 Worked seismic weight comparison — 2,000 sq ft/floor G+1

Footprint 186 m² per floor. Wall length per floor ≈ 60 m (external + internal structural). Storey height 3.0 m.

**Option A — RCC frame + 230 mm brick infill**

```
Floor slab + finishes : 186 m² × 5.1 kPa           = 949 kN
Walls (full storey)   :  60 m × 13 kN/m            = 780 kN
Frame (cols + beams, allow)                        = 150 kN
                                          per floor ≈ 1,879 kN
Roof level (slab + parapet + half walls)           ≈ 1,400 kN
                        TOTAL SEISMIC WEIGHT  W ≈ 3,280 kN
```

**Option B — LGSF**

```
Floor: 186 m² × 2.2 kPa                            = 409 kN
Walls: 60 m × 2.0 kN/m                             = 120 kN
                                          per floor ≈  529 kN
Roof (light, 0.6 kPa over 186 m² + half walls)     ≈  175 kN
                        TOTAL SEISMIC WEIGHT  W ≈  704 kN
```

**W(LGSF) / W(RCC) ≈ 0.21 — about one-fifth the seismic weight.**

### 8.2 Base shear consequence

Base shear V = C_s · W (ASCE 7-22 §12.8) with C_s ∝ 1/R.

| System | W | R (indicative) | Relative V = W/R |
|---|---|---|---|
| RCC frame (intermediate, non-special) | 3,280 kN | 5 | 656 |
| Confined masonry | ~3,300 kN | ~3 (practice, not tabulated) | 1,100 |
| **LGSF, strap-braced** | **704 kN** | **4** | **176** |
| **LGSF, steel-sheet sheathed** | **704 kN** | **6½** | **108** |
| LGSF, cement-board "shear" panels | 704 kN | **2** | 352 |
| Steel portal frame (R=3, not detailed for seismic) | varies with envelope | 3 | — |

> The R values in this table carry the same citation caveat as §3.6: they are commonly cited ASCE 7-22 Table 12.2-1 figures, not verified against a specific dated printing. **Confirm the exact edition/printing before using the resulting V-ratio in any real design decision.**

**Interpretation:** an LGSF house designed with a *proper* strap-braced or steel-sheet-sheathed lateral system attracts roughly **one-quarter to one-sixth** of the design base shear of an equivalent RCC/masonry house. That is a genuine, physics-based advantage and it is why ASCE 7-22 carries CFS light-frame as its own seismic force-resisting system category with AISI S400 detailing. It is also why the same house needs **much smaller foundations** on weak soil.

**But note the cement-board row.** Choose the wrong sheathing and you throw away most of the advantage while thinking you still have it.

### 8.3 Wind uplift — the load case that actually governs light systems

For RCC, gravity holds the building down and wind is a secondary check. **For LGSF, timber and portal frames with light roofs, net uplift governs the roof, its connections, the walls and the anchorage.**

Illustrative: light roof dead load 0.5 kPa; ASCE 7-22 Ch. 30 components-and-cladding uplift on a corner/edge zone of a low-slope roof can readily reach **1.5-2.5 kPa** at residential wind speeds.

```
Net uplift = 1.8 kPa (uplift) − 0.9 × 0.5 kPa (dead, using the 0.9D combination)
           ≈ 1.35 kPa upward, sustained, over the roof area
```

Over a 1.5 m purlin spacing and a 6 m bay, that is ~12 kN pulling a single purlin cleat upward. **Every link in the chain must be designed for it:**

```
sheeting fixings → purlin → purlin cleat/bolts → rafter/truss → uplift clip →
top track/plate → stud → bottom track/sill plate → anchor rod → foundation mass
```

**Rules:**
1. **Corners and edges, not the field, govern.** ASCE 7-22 Ch. 30 zone factors are much higher at corners; do not design the whole roof to the field pressure.
2. **Anchorage must be checked against overturning AND net uplift** with the 0.9D combination — the dead load you are relying on is factored *down*.
3. Sheeting fixings pull through before they pull out — specify washered fixings at the correct density in the edge zones.
4. On a hill or ridge site (very common in the northern belt), apply the **topographic factor K_zt** — it can nearly double pressures.

---

## Section 9: Hybrid Systems — Usually the Right Answer in Pakistan

The best real-world Pakistani answer is rarely "all LGSF" or "all steel". It is a hybrid that puts each system where it earns its keep.

| Hybrid | Where it fits | Watch out for |
|---|---|---|
| **RCC/masonry house + steel portal or beam over the one big span** (great room, garage, covered court) | The single most common justified use of steel in a Pakistani house | Base thrust must be resolved into the RCC structure (§5.6); differential stiffness at the interface; corrosion where steel enters masonry |
| **Masonry walls + timber or CFS roof structure** (instead of an RCC roof slab) | Everywhere, especially north; cuts roof weight by 70-80%, hugely reduces seismic demand on the walls | Uplift anchorage into a continuous RC ring beam; the wall plate must be bolted down, not just bedded; loses the flat roof (a real lifestyle loss in Pakistan — no charpai on the roof) |
| **RCC ground floor + LGSF or timber upper storey** | Vertical extensions; keeps the heavy, robust, termite-proof floor at grade and puts the light structure on top | Stiffness/mass discontinuity is a seismic irregularity — engineer must check; continuity of the lateral system across the interface; anchor the light frame into the RCC slab properly |
| **RCC/masonry core (stair, wet areas, service shaft) + LGSF around it** | Gets a stiff lateral core and puts the plumbing in masonry where it belongs | The core will attract nearly all the lateral load — design it for that, do not "share" naively |
| **Confined masonry + Dhajji-style timber lacing** | Northern belt, traditional idiom, high seismic | Outside explicit BCP coverage; engineer's analysis required |
| **Steel portal shell + masonry infill walls** | Farmhouse/workshop/annexe | The masonry must be *isolated* from the frame (soft joint) or *designed as part of it* — the in-between condition (tight infill nobody analysed) is a short-column/stiffness trap |

---

## Section 10: Failure Modes and Anti-Patterns

### 10.1 LGSF

| Anti-pattern | Consequence |
|---|---|
| Bridging/bracing omitted or spaced > 1220 mm | Stud buckles at a fraction of its table capacity |
| Studs not in-line with joists/studs below | Track spans in bending; local crushing and progressive sag |
| No web stiffener under a header or beam bearing | Web crippling — a brittle local failure |
| Field-cut service holes in stud webs | Section capacity destroyed silently |
| Field welding thin sections | Burn-through, no capacity, galvanizing destroyed both faces |
| Sheathing substituted (OSB → cement board) without re-designing to the lower R | 3× under-designed lateral system |
| Shear-wall edge screws at 300 mm instead of 50-100 mm | Shear wall capacity a fraction of design |
| Hold-downs omitted at shear-wall ends | Panel rotates, overturns; the braces do nothing |
| Post-drilled plugs instead of cast-in anchors | Anchorage fails in uplift |
| No continuous exterior insulation | 40-60% loss of insulation effectiveness; unhappy client |
| No noggings for wall-hung items | Geyser, AC or cabinet cannot be fixed after handover |
| Carbon-steel screws in a coastal build | Rust streaks in year one, connection loss in year five |
| Steel starting at, or below, finished grade | Corrosion at the most highly stressed location |

### 10.2 Steel portal frames

| Anti-pattern | Consequence |
|---|---|
| Base thrust left to "the slab" | Frame spreads; cracked slab; sagging ridge |
| No fly/knee bracing to the inside flange at eaves | Lateral-torsional buckling — the classic collapse |
| No longitudinal bracing system | Building is a mechanism in the long direction |
| Haunch geometry ignored in planning | Head height lost at the perimeter; doors/windows clash |
| Very shallow pitch on a house | Enormous base thrust (§5.6), poor monsoon drainage, ponding |
| Purlin sag rods omitted on long runs | Purlin twist, sheeting fixings loosen |
| Field welding on site | Uncontrolled, untested, unpainted |
| Shed-grade envelope on a house | Condensation, noise, thermal misery; the client blames "steel" |
| Tight masonry infill built between columns with no analysis | Unintended stiffness, short-column effect, cracking |
| PEB supplier's calculation accepted as the engineering | Nobody has checked the foundation, the thrust, or the residential loads |

### 10.3 Timber

| Anti-pattern | Consequence |
|---|---|
| Untreated timber in Punjab/Sindh | Termites; total structural loss in years, not decades |
| Timber sill directly on concrete without DPC | Rising damp, decay at the most critical connection |
| Timber within 200 mm of finished grade | Damp and termite bridge |
| Green (unseasoned) timber framed tight | Shrinkage, splitting at fasteners, loose hangers, cracked finishes |
| Rafters without ties or collar ties | Walls pushed outward; ridge sags |
| Nails relied on for uplift | Roof leaves in the first serious wind |
| Ledger strip instead of joist hangers | Splits along the nail line; joists drop |
| Plain steel connectors with copper-based preservative | Galvanic corrosion of the connector |
| Unstopped cavities | Fire spreads through the structure |
| Dhajji presented as "code compliant" | Approval refused, or worse, approved on a false premise |

---

## Section 11: Worked Examples

### 11.1 Example A — LGSF G+1, 2,000 sq ft/floor, Islamabad hillside plot

**Constraints:** steep plot, no transit-mixer access to the upper terrace, client wants occupancy in 4 months, Zone 2B, wants earthquake performance.
**Triggers hit:** T2 (schedule), T3 (site access), T4 (seismic mass). → LGSF is justified. Record that.

| Item | Preliminary |
|---|---|
| Ground-floor load-bearing studs | 600S162-54 @ 400 mm o.c. (152 mm depth — also gives insulation space) |
| Upper-floor studs | 400S162-43 @ 400 mm o.c. |
| Floor joists (max 4.2 m span) | 1000S162-54 @ 400 mm o.c., L/480, 40 mm screed topping |
| Bridging | CRC + clips at 1200 mm vertically, all load-bearing walls |
| Headers (2.4 m living-room opening) | Box 2 × 800S162-68 with bearing stiffeners |
| Lateral system | Flat strap X-bracing both faces, **R = 4**; braced panels at all four corners plus two internal lines each direction |
| Hold-downs | At each end of every braced panel, M20 cast-in rods into the RCC raft |
| Anchorage | M16 anchor rods @ 1200 mm o.c., within 300 mm of panel ends |
| Roof | CFS trusses @ 600 mm o.c., 20° pitch, light tile-profile sheeting; uplift clip at every truss |
| Foundation | RCC raft or strip on the terraced platform — **still concrete**; sized for W ≈ 700 kN, far smaller than the RCC alternative |
| Seismic weight | **≈ 704 kN vs ≈ 3,280 kN for the RCC equivalent (§8.1)** |
| Envelope | 50 mm continuous XPS outside the studs + 100 mm mineral wool in the cavity; deep overhangs; light roof colour |
| Cost check | ~PKR 3,500/sq ft LGSF vs PKR 3,200-5,800/sq ft Islamabad RCC grey structure → **competitive here**, unlike in Faisalabad |
| Programme | 3 wk fab + 3 wk foundation (parallel) + 2 wk erect + 8 wk finish ≈ **4 months** ✓ |

**Flag to the client, unprompted:** plan-checker unfamiliarity with AISI-based design; the need for supplier-led erection; the exterior insulation is not optional; blocking schedule required before boards go on; PEC engineer's design and stamp required.

### 11.2 Example B — 12 m clear-span great room + double garage annexe, farmhouse near Lahore

**Constraint:** T1 — 12 m clear span, no columns, attached to an otherwise conventional brick/RCC farmhouse.

| Item | Preliminary |
|---|---|
| Span / bays | 12 m span × 3 bays @ 6.0 m = 18 m long |
| Pitch | **20°** (chosen deliberately to cut base thrust — see below — and to shed monsoon rain) |
| Rafter | Depth range span/55-span/40 = 220-300 mm → UB 305×102×33 preliminary |
| Column | UB 305×165×40, eaves height 4.0 m |
| Haunch | Depth 1.5-2 × rafter ≈ 460-610 mm total; length span/10-span/7 = **1.2-1.7 m** → **check head height along the perimeter 1.7 m of the room** |
| Eaves connection | Extended end plate, 22 mm, 10 × M24 grade 8.8, two rows |
| Apex | End-plate splice, 6 × M20 |
| Base | 25 mm plate, 4 × M20 HD bolts, 400 mm embedment, nominally pinned |
| Purlins | Z 175 × 2.0 mm @ 1.5 m, sleeved, sag rods at mid-span |
| Bracing | Roof-plane and wall-plane cross-bracing in both end bays; longitudinal system explicitly shown |
| Fly bracing | At eaves haunch and at the first two purlins each side — **mandatory** |
| **Base thrust hand check** | w = 1.5 kPa × 6 m = 9 kN/m; f = 6·tan20° = 2.18 m; H ≈ 9 × 144/(8 × 2.18) ≈ **74 kN/base** (three-hinged, conservative) |
| Thrust resolution | **Tie rod between opposing bases, cast under the floor slab**, corrosion protected, recorded on the services drawing so nobody trenches through it |
| Compare: 6° pitch | H would be **≈ 257 kN** — 3.5× the foundation problem. This is why the pitch was chosen |
| Cost frame | ~PKR 2,100-2,500/sq ft shell + PKR 1,500-3,000/sq ft to finish it to house standard |
| Interface | Soft joint between the steel frame and the adjoining masonry farmhouse, or a designed connection — not tight untreated infill |

### 11.3 Example C — Deodar-framed roof + Dhajji upper walls, Gilgit-Baltistan

**Constraints:** T3 (no ready-mix, aggregate hauled), T4 (Zone 4), local Deodar supply, local carpentry trade, heavy snow.

| Item | Preliminary |
|---|---|
| Plinth | Stone/brick masonry plinth, **top 450 mm above finished grade**, DPC under the timber wall plate |
| Ground floor | Confined masonry (per `architecture-structural-systems`) or stone with timber lacing |
| Upper walls | **Dhajji-Dewari**: Deodar posts at ≤ 1.2 m, horizontals at ≤ 900 mm, diagonal brace in every panel, stone/brick infill built tight |
| Roof | Deodar rafters — **snow governs, so IRC 20 psf spans in §6.3 DO NOT APPLY**; get the ground snow load and design to PKBC 2021 Ch. 23 |
| Rafter ties | Ceiling joists acting as ties at plate level + collar ties in the upper third |
| Roof covering | Light — CGI sheet or shingle, not slate/heavy stone, to keep seismic mass down |
| Uplift/snow-slide | Straps at every rafter-to-plate; snow guards |
| Timber spec | Deodar, MC ≤ 18-20% at installation, rejected for wane at bearings and mid-span tension-face knots |
| Connectors | Hot-dip galvanized straps and hangers; pre-drilled bolts |
| **Code position** | **Dhajji is outside explicit BCP-SP 2007 coverage.** Design is an engineered scheme referencing post-2005 reconstruction guidance and the Dhajji seismic literature, requiring the PEC engineer's analysis and stamp. **Do not label it code-compliant** |
| Fire | Fire-stop all cavities; state the coating maintenance cycle to the owner |

---

## Section 12: Practical Delivery in Pakistan

### 12.1 Questions to ask a prefab/PEB/LGSF supplier before believing a quote

1. What **exactly** is in the rate — structure only, structure + envelope, or turnkey? Get it line by line.
2. Is the **foundation** included? Whose design?
3. What **steel grade and thickness (mils/gauge)** — with a mill certificate?
4. What **galvanizing class** (G60/Z180 vs G90/Z275)? Where is it applied — coil or after fabrication?
5. What **standard** was the design done to (AISI S230? S240? AISC? "our standard"?) and **who is the PEC-registered engineer of record**?
6. What **wind speed and seismic zone** was it designed for? (A standard panel designed for Lahore is not a Quetta panel.)
7. What is the **lateral system** and what R was used?
8. **Sheathing/bracing type** and edge fastener spacing?
9. Is **continuous exterior insulation** included, or only cavity insulation?
10. What **blocking/noggings** are provided, and where?
11. Who **erects** it, and is their crew experienced with this system?
12. What is the **warranty** and what voids it?
13. Have they built and can they show a **completed, occupied house** (not a shed, not a site office) of this system in Pakistan?

### 12.2 What to hand the PEC-registered engineer

- [ ] Architectural plans, sections, elevations with all clear spans dimensioned
- [ ] The **constraint that justified the alternative system** (T1-T6), stated explicitly
- [ ] Site location, seismic zone from the current map, basic wind speed, exposure, topography, ground snow (north)
- [ ] Geotechnical report / SBC — **and** the note that this system delivers concentrated uplift and thrust, not just bearing
- [ ] Intended system, with this skill's preliminary sizing **clearly labelled preliminary**
- [ ] The intended **lateral system and sheathing/bracing material** — because it sets R
- [ ] Storey count including any future extension
- [ ] Roof covering weight, water tank position and capacity, solar array if any (uplift!)
- [ ] Any supplier/PEB submittals, marked as vendor documents requiring independent review
- [ ] Fire, acoustic and thermal performance targets

### 12.3 Approvals and money — the non-structural risks

| Risk | Reality | Mitigation |
|---|---|---|
| **Plan approval** | Some development authorities and housing societies (DHA/CDA sectors especially) restrict, refuse, or reclassify non-RCC residential structures; a plan checker may have never seen an AISI-based submission | **Confirm in writing before design.** Submit the standards references and the engineer's letter with the drawings. Budget schedule for it |
| **Bank valuation / mortgage** | Pakistani valuers price "pukka" RCC/brick construction; a steel or timber house is commonly valued lower or flagged | Warn the client at the start if they intend to sell or finance |
| **Insurance** | Fire and cat cover for non-standard construction may be priced differently or refused | Check before, not after |
| **Resale market** | Buyer perception in Pakistan strongly favours RCC/brick | Only relevant if selling; state it once, clearly |
| **Maintenance trade** | In ten years, can a local mason/electrician work on this house without wrecking it? For LGSF the answer is often no | Provide an as-built with structural members, blocking, brace lines and services marked. Insist on it |
| **Spare parts / repair** | Proprietary panels, clips and fixings may not be available later | Ask for a spares allowance and the connector schedule |

---

## Section 13: FreeCAD Modelling Defaults

Pair with `architecture-freecad-bim` for the Site/Building/Storey hierarchy, parametric openings via Subtractions, and the FEM verification pipeline. Pair with `architecture-structural-systems` for the RCC/masonry defaults.

### 13.1 LGSF

| Parameter | Default | Note |
|---|---|---|
| External load-bearing wall (modelled thickness) | **152 mm** frame + 50 mm continuous insulation + finishes → model the **Arch Wall at 230 mm overall** | Classify **IfcWall**; note the frame depth in the object description |
| Internal load-bearing wall | 102 mm frame → 150 mm overall | IfcWall |
| Partition | 92 mm frame → 125 mm overall | IfcWall, non-load-bearing |
| Stud spacing | 400 mm o.c. (600 for light single-storey) | **Do not model every stud** on a whole-house model — it destroys performance. Model studs only in a detail view or a single representative bay |
| Floor zone depth | 254-305 mm joist + 50 mm screed = **~355 mm** | IfcSlab or IfcMember set |
| Floor-to-floor | **3050 mm** | LGSF is dimensioned in imperial-derived modules; 3050 = 10 ft |
| Clear ceiling height | 2700 mm | |
| Roof truss depth at eaves | ≥ 300 mm (insulation + ventilation) | |
| Foundation | RCC raft 250-300 mm, or strip 600 × 300 mm | IfcFooting — **still concrete** |
| Hold-down / anchor positions | Model as distinct small objects at braced-panel ends | So they are visible and countable |

### 13.2 Steel portal frame

| Parameter | Default | Note |
|---|---|---|
| Frame member | `Arch Structure` with a profile from the FreeCAD profile library (UB/IPE/W) | Classify **IfcColumn** / **IfcBeam**; set the profile name in the description |
| Bay spacing | 6000 mm | |
| Eaves height (house) | 3600-4500 mm | |
| Pitch | **15-25°** for a house (see §5.6) | Model it correctly; the haunch geometry depends on it |
| Haunch | Depth 1.5-2 × rafter, length span/10-span/7 | **Model the haunch** — it is what eats perimeter head height |
| Purlins | Z 175 @ 1500 mm | IfcMember; model a representative set, not necessarily all |
| Base plate + HD bolts | Model schematically as a plate object | So the foundation interface is visible |
| Tie rod / tie beam | **Model it** | It is the item most likely to be forgotten on site |
| Bracing | Model as IfcMember in the end bays | Makes the longitudinal system visible |

### 13.3 Timber

| Parameter | Default | Note |
|---|---|---|
| Stud | 38 × 89 or 38 × 140 @ 400/600 o.c. | IfcMember |
| Rafter / joist | 38 × 184 or 38 × 235 @ 400 o.c. | IfcMember |
| Wall (modelled) | 140 frame + finishes → 200 mm overall | IfcWall |
| Floor zone | 235 mm joist + 20 mm deck = 255 mm | |
| Sill plate level | **≥ 450 mm above finished grade**, on a masonry plinth with DPC | Model the plinth — it is a structural and durability requirement, not a detail |
| Dhajji panel module | ≤ 900 × 1200 mm with a diagonal in every panel | Model one bay in detail; array it |
| Roof pitch | 25-40° in the snow belt | |

### 13.4 Modelling discipline (all systems)

1. **Model the lateral system as visible, distinct objects** — braced bays, shear-wall panels, tie rods, hold-downs. If they are invisible in the model, they will be invisible on site.
2. **Model the foundation.** None of these systems removes it, and all of them concentrate load into it.
3. **Model the haunch, the tie rod and the plinth** — the three items most likely to be value-engineered out by someone who does not know what they do.
4. **Do not model every stud in a whole-house model.** Use a representative bay or a detail file; the whole-house model should carry walls as Arch Walls with the framing described in metadata.
5. **Annotate the model or its README with:** system chosen, the T1-T6 trigger that justified it, assumed wind speed and seismic zone, assumed SBC, sheathing/bracing type and the R it earns, galvanizing/treatment spec, and the statement *"Preliminary — requires design and stamp by a PEC-registered structural engineer and local authority approval before construction."*
6. If the model is going to FEM (`mcp__freecad__run_fem_analysis`), remember that these systems are **connection- and stability-governed**. A solved member stress does not verify a screw group, a haunch bolt group, a hold-down, or a lateral-torsional buckling limit state. Say so when reporting results.

---

## Section 14: Known Gaps in This Skill (state these when relevant)

1. **AISI S230-19 and S220-20 literal table values are NOT reproduced here.** The stud/joist/header tables in §3.4 and §3.5 are indicative reconstructions in the form of the prescriptive tables, not transcriptions of the actual cells. **Obtain the AISI S230-19 PDF and read the real tables** before any project use. This is the single most important gap in this file.
2. **IRC 2021 rafter, ceiling-joist, floor-joist and header spans in §6.3 are indicative**, not literal transcriptions of Tables R802.4.1(1)/(2) (Ch. 8), R802.5.1(1)/(2) (Ch. 8), R502.3.1 (Ch. 5) or R602.7 (Ch. 6), and they are calibrated to a generic North American #2 softwood, **not to graded Deodar**. Read the actual tables, and design Deodar to PKBC 2021 Ch. 23 with real graded stresses.
3. **Deodar permissible stresses and E** (§6.2) are indicative. Verify against PKBC 2021 Ch. 23 / IS 883 grade tables.
4. **ASCE 7-22 Table 12.2-1 R/Ω₀/Cd values** for CFS light-frame systems (§3.6, §8.2) are quoted as commonly cited values, **not tied to a specific edition/printing/errata date**, and must be verified against the exact current published table before design — see the citation-precision note at the end of §3.6.
5. **Portal frame section sizes in §5.3** are the span/40-55 rule applied consistently, anchored on the published 30 m → 550-750 mm data point. They are massing aids. Real sections come from analysis with actual loads, restraints and stability checks.
6. **The base-thrust formula H ≈ wL²/(8f) is a three-hinged idealisation** used as a conservative hand check. A real two-hinged haunched frame carries part of it in bending. Do not use the hand value as a design value.
7. **No verified 2026 Pakistani timber market rates** are carried in this file. Price from an actual timber market.
8. **The PKR 2,100-2,500/sq ft PEB figure is an industrial-shed shell rate**, drawn from industrial-shed suppliers and **not verified for finished residential fit-out standards**. It is a shell-cost comparison only.
9. **LGSF prefab pricing (~PKR 3,500/sq ft)** is a single supplier's quoted figure for panel-built homes with "basic facilities" — the inclusion list was not verified line by line, and it must never be netted against a differently-scoped foreign-currency figure (see §3.9 scope warning).
10. **PKBC 2021 / BCP-SP 2007 seismic zone maps, wind speed maps and snow maps are not reproduced.** Every reference to "Zone 3/4", a wind speed or a snow load in this file is indicative and must be confirmed against the current governing map. See §2.1 for the reconciliation of these two document names.
11. **BCP-SP 2007 has no wood-frame or Dhajji-Dewari structural type, R-factor, or detailing provisions.** This is a gap in the *code*, not just in this skill, and it is the controlling practical obstacle to timber framing in Pakistan.
12. **Hygrothermal (condensation) design for lightweight envelopes in Pakistani cooling-dominated climates is not solved here.** Copying a North American vapour-barrier detail into Multan is a known way to build a mould farm. This needs actual hygrothermal analysis, not a rule of thumb.
13. **Acoustic performance targets and constructions** are described qualitatively only; no STC/Rw-rated build-ups are specified.
14. **Nothing in this file is a fabrication drawing, a cutting list, a bar bending schedule, a bolt schedule or a connection design.** Every screw count, bolt count and fastener spacing shown is an order-of-magnitude planning value requiring the engineer's design.

---

## Section 15: Cross-References

| Need | Skill |
|---|---|
| RCC, confined masonry, URM systems; the baseline this file compares against | `architecture-structural-systems` |
| Seismic zoning, ELF, detailing | `architecture-seismic-design` |
| Foundations, SBC, geotechnical investigation | `architecture-geotechnical-foundations` |
| RCC detailing where a hybrid touches concrete (plinth, raft, ring beam, tie beam) | `architecture-concrete-reinforcement-detailing` |
| Brick, block, mortar specs for hybrid infill and plinths | `architecture-masonry-materials` |
| Roof coverings, waterproofing, uplift-resistant sheeting details | `architecture-roofing-waterproofing` |
| Authority byelaws, plan approval, PEC stamping process | `architecture-building-codes-permits` |
| BOQ, quantity takeoff, contractor quote sanity-check | `architecture-cost-estimation-boq` |
| Build sequence and programme | `architecture-construction-sequencing` |
| Services routing through light framing and portal structures | `architecture-mep-coordination` |
| Room sizing, spans required, plan geometry | `architecture-spatial-planning` |
| Building the model and running FEM verification | `architecture-freecad-bim` |
