---
name: architecture-mep-coordination
description: >
  MEP-to-structure coordination for house design: sleeve and opening planning
  through RCC beams and slabs without impairing structural capacity, electrical
  conduit embedment rules in concrete, plumbing stack layout and drainage slope
  requirements, septic tank and soak pit sizing for off-grid/unsewered houses,
  water storage tank loading on structure, LPG/piped-gas coordination and
  safety separation, and a clash-prevention coordination checklist across
  architectural, structural and MEP drawings. Numeric authorities are
  ACI 318-19 Ch. 20, IPC Ch. 7, and IS 2470 Pt. 1 & 2 (directly citable
  clauses), plus SP 34-derived beam-opening detailing practice (flagged as
  handbook practice, not a single IS 456 clause), with BCP 2007/2021 as the
  Pakistan adopting-code context.
---

# MEP Coordination with Structure for House Design

Most site-level rework on a house is not a design failure — it is a coordination failure. A 110mm soil pipe meets a 600mm beam that was never told about it; a plumber core-drills the beam on a Sunday; nobody records which bars were cut. This skill exists to move those decisions to the drawing board, where they cost nothing, and to give hard numbers for the four places where MEP and structure actually collide: **penetrations, embedments, gravity drainage, and concentrated service loads.**

The numeric authorities used throughout are cited inline. Where a number is regionally contested or edition-dependent it is flagged `⚠ VERIFY`. Where a widely-repeated field rule of thumb does not reconcile with the code calculation, both are shown and the calculation wins.

---

## Reality Check - Licensing & Liability

**This skill produces design aids and calculation guidance for planning and FreeCAD modeling ONLY.**

- Every number, table, formula and checklist here is for **preliminary planning, coordination studies, quantity estimation and 3D/BIM modeling**. None of it is a structural calculation, a sanitary design, or an electrical design in the legal sense.
- Any design intended for the **actual construction of a real occupied building** MUST be reviewed and stamped by a **licensed structural engineer registered with the relevant authority** — in Pakistan, a **PEC-registered engineer** (Pakistan Engineering Council), with the sanitary/plumbing and electrical scopes signed off by the correspondingly licensed practitioners.
- The design MUST additionally pass **local authority plan approval** before construction — LDA, CDA, RDA, KDA, TMA or the relevant cantonment board / development authority — under the applicable building byelaws and the Building Code of Pakistan (BCP 2007 seismic provisions / BCP 2021 draft).
- **Any opening, sleeve or chase through a beam, column, shear wall, or slab requires the structural engineer's written approval on a stamped drawing before casting.** No exception. Post-cast core drilling through a beam or column without engineer approval is treated in this skill as a defect, not an option.
- **Claude / Claude must never present FreeCAD output, IFC models, or the calculations in this skill as construction-ready.** If a user appears to be treating the output as final — sending it to a contractor, quoting it to a mason, dimensioning steel from it, ordering a septic tank from it — **say so unprompted, in plain language, before continuing.** State what is missing (stamped structural calcs, soil investigation, percolation test, authority approval) rather than issuing a generic disclaimer.
- Off-grid sanitation carries a public-health liability that is separate from the structural one. Septic and soak-pit sizing here is a planning aid; **an actual percolation test on the actual plot** and compliance with local groundwater-protection rules are non-negotiable before construction.

---

## Section 1: Which Code Supplies Which Number

Pakistan's BCP is an **adopting/context code** for these specific provisions — it does not restate the concrete-embedment or septic-sizing clauses in usable numeric detail. So cite the source standard for the number, and BCP for the local adoption.

| Question | Primary numeric authority | Clause | Local adoption context |
|---|---|---|---|
| Max size of a pipe/conduit **embedded in** a slab, wall or beam | **ACI 318-19** (language from 318-11 §6.3, carried to 318-19 Ch. 20) | §20.6 / §6.3.7 legacy | BCP 2007/2021 via IBC/ACI-based RCC practice |
| Conduit **inside a column** | ACI 318 | 4% of gross cross-section | as above |
| **Openings through the web** of an RCC beam | **IS 456:2000** + **SP 34:1987** (Handbook on Concrete Reinforcement & Detailing) | detailing provisions — ⚠ see 3.0 note: the specific ratios (0.4d, 0.33d, d/4, 0.004d²) are commonly-used SP 34-derived design-handbook practice, not a single citable IS 456 clause number | South Asian standard practice, incl. Pakistan |
| Cover to reinforcement / to embedded conduit | IS 456 Table 16 · ACI 318 cover table | — (exposure-class dependent; see 2.1 note) | BCP 2021 |
| **Slope of horizontal sanitary drainage** | **IPC §704.1 / Table 704.1** (mirrored in UPC) | Ch. 7 | Adopted in practice; no conflicting BCP table |
| Trap-to-vent distance, cleanouts, venting | IPC Ch. 7 & 9 | ⚠ VERIFY adopted edition | — |
| **Septic tank volume & proportions** | **IS 2470 Part 1** | full standard | De-facto regional reference; no distinct PK standard |
| **Soak pit / soil absorption sizing** | **IS 2470 Part 2** + CPHEEO Manual on On-Site Sanitation | full standard | as above |
| Septic separation distances (well, boundary, foundation) | IS 2470 Pt.1 + **NBC 2016 (India)** | — | Check local TMA/WASA byelaw — it may be stricter |
| **Buried (soil) conduit cover depth** | **NEC Table 300.5** | Art. 300 | Pakistan Electricity Rules 1937 + BS/PS for wiring |
| Seismic detailing that constrains where you may cut | BCP 2007 Seismic Provisions | Ch. 5 | mandatory in PK |

**Rule 1.1 — Do not conflate NEC Table 300.5 with ACI 20.6.** Table 300.5 is *minimum burial cover in soil*. ACI 20.6 is *maximum embedment size in structural concrete*. They govern different conditions and neither substitutes for the other.

---

## Section 2: The Universal Embedment Rule (ACI 318 §20.6)

This is the single hardest-working numeric rule in the whole skill. It applies identically to **plumbing pipe, electrical conduit, data conduit, and gas line** cast into structural concrete.

### 2.1 The clause, stated exactly

For conduits and pipes **embedded within** a slab, wall or beam — *other than those merely passing through* — unless the drawings are specifically approved by the structural engineer:

| Limit | Value |
|---|---|
| Max outside dimension | **≤ 1/3 the overall thickness** of the slab, wall or beam in which it is embedded |
| Min centre-to-centre spacing | **≥ 3 diameters (or widths)** on centre |
| Strength | Shall not impair the strength of the construction **significantly** |
| Conduit in a **column** | Total embedded area **≤ 4% of the gross column cross-section area** |
| Min cover to pipe/conduit | **≥ 40 mm (1½ in)** exposed to earth or weather; **≥ 20 mm (¾ in)** not exposed |
| Aluminium conduit | **Prohibited** in structural concrete unless coated/sheathed against alkali reaction |
| Hot service | Pipes carrying liquid/gas/vapour above **93 °C (200 °F)** shall not be embedded unless specifically designed |

**⚠ Note on the cover figures above:** the 40 mm / 20 mm cover values are a **planning default**, not a single flat ACI clause. ACI 318's actual cover requirements are set by exposure class (Table 20.6.1.3.1 in 318-19) and vary with member type, casting condition (cast against earth vs. formed) and environment — a conduit run in a severe-exposure or cast-against-earth condition can require more than 40 mm, while some formed-and-not-exposed conditions permit less. Treat 40/20 mm as a safe coordination-drawing default for house-scale work; **the structural engineer's cover schedule for the actual exposure class governs**, not this table.

### 2.2 The distinction that everyone gets wrong

- **Embedded (runs *along* inside the member)** → the 1/3 and 3-diameter limits bite.
- **Merely passing through (a transverse sleeve)** → exempt from the 1/3 rule as written, **but still subject to "shall not impair strength"** — which for a beam means IS 456 / SP 34 opening rules (Section 3) take over, and for a slab means Section 4. "Exempt from 1/3" is *not* "do whatever you like".

### 2.3 Ready-reckoner: max embedded conduit OD by member thickness

Metric PVC conduit is designated by **outside** diameter, so the comparison is direct.

| Member overall thickness | 1/3 limit | Largest standard conduit permitted | Min c/c spacing at that size |
|---|---|---|---|
| 100 mm slab | 33 mm | **32 mm** | 96 mm |
| 110 mm slab | 36 mm | 32 mm | 96 mm |
| 125 mm slab | 41 mm | **40 mm** | 120 mm |
| 150 mm slab | 50 mm | **50 mm** | 150 mm |
| 175 mm slab | 58 mm | 50 mm | 150 mm |
| 200 mm slab | 66 mm | 63 mm | 189 mm |
| 230 mm RCC wall | 76 mm | 75 mm | 225 mm |
| 100 mm (4 in) US slab | 1-⅓ in | 1-⅜ in conduit *(the classic textbook case — exactly at the limit)* | 4-⅛ in |

### 2.4 Worked example — column conduit

Column **300 × 300 mm**, gross area = 90,000 mm². 4% allowance = **3,600 mm²**.

- One 63 mm OD conduit: π/4 × 63² = 3,117 mm² → **OK (3.5%)**
- Two 50 mm OD conduits: 2 × 1,963 = 3,927 mm² → **FAILS (4.4%)** — reroute one, or run both in the adjacent masonry infill, not the column.
- Practical house rule: **never run conduit in a column at all.** Bring the vertical riser up an adjacent non-structural masonry pier or a dedicated shaft. Columns in a seismic zone (all of Pakistan is in BCP seismic Zone 2A–4) have congested confinement hoops at the ends where conduit does the most harm.

---

## Section 3: Openings Through RCC Beams (IS 456:2000 / SP 34)

A transverse hole through a beam web is the highest-risk MEP-structure interaction in a house. Beams fail in shear, and a hole is a shear defect.

### 3.0 ⚠ What is actually "code" here vs. what is handbook practice

Be precise about what backs these numbers, because it matters for who can override them. **IPC Table 704.1** in Section 6 is a real, directly citable numbered clause — you can hand a contractor the table and the clause number and it is unambiguous. The numeric ratios in this section (**0.4d** height limit, **0.33d** compression-face clearance, **d/4** large-opening threshold, **1000 mm² / 0.004d²** small-opening area) are **not** a single, directly citable IS 456:2000 clause in the same way. They are **long-standing detailing practice** derived from SP 34:1987 (Handbook on Concrete Reinforcement and Detailing) and repeated across South Asian RC design textbooks and design-office practice — genuinely conservative, widely used, and a reasonable planning default, but the specific ratios themselves are handbook/practice-derived rather than a numbered IS 456 sub-clause. Treat every number in 3.1–3.3 as **"commonly used detailing practice, use for planning — get the project structural engineer's actual calculation and sign-off before any beam is drilled or cast with an opening.**" Do not represent these ratios to a client or contractor as a direct IS 456 clause citation.

### 3.1 Classification by size

Let **d** = effective depth of the beam (overall depth − cover − stirrup − ½ main bar dia).

| Class | Criterion | Design consequence |
|---|---|---|
| **Small opening** | Area ≤ **1000 mm²** when d ≤ 500 mm; or area ≤ **0.004 d²** when d > 500 mm | No special design; keep to the rules in 3.2 |
| **Intermediate** | Above small limit, but largest dimension ≤ **d/4** | Local check + nominal trimming reinforcement |
| **Large opening** | Largest dimension **> d/4** | Full design per 3.3; engineer calculation mandatory |

### 3.2 Placement rules for any opening (small or large)

| Rule | Value |
|---|---|
| Height of opening | **≤ 0.4 d** |
| Distance from **compression face** to opening edge | **≥ 0.33 d** |
| Clear spacing between adjacent openings | **≥ 150 mm** (and ≥ the depth of the larger opening) |
| Vertical position | **Mid-depth of the web**, in the tension/low-shear zone |
| **Forbidden zones** | Bottom of the beam near supports (max shear + max tension steel); top of the beam near mid-span (compression block); anywhere within the **confinement zone at beam ends = 2 × overall depth from the column face** (seismic detailing per BCP 2007) |
| Preferred longitudinal position | **Middle third of the clear span**, where shear is lowest |
| Never | Through a **transfer beam**, **cantilever beam**, or any beam flagged by the engineer as a key element |

### 3.3 Extra reinforcement at a large opening

- Additional **stirrups flanking each side** of the opening, distributed over a length up to **d/2** each side.
- Those stirrups sized to carry **twice the design shear** at the opening location (the conventional SP-34 detailing allowance for stress concentration at the corners).
- **Diagonal bars at each corner** of a rectangular opening to control corner cracking; chamfer or radius rectangular corners where possible — circular openings are always structurally cheaper than square ones of the same area.
- Longitudinal chord bars above and below the opening (the two residual chords act as a mini Vierendeel).

### 3.4 Worked example — 110 mm soil pipe through a house beam

Beam **300 wide × 600 deep**, 25 mm cover, 8 mm stirrup, 16 mm main bar → **d ≈ 600 − 25 − 8 − 8 = 559 mm**.

1. d > 500 → small-opening area limit = 0.004 × 559² = **1,250 mm²** → max "free" circular hole ⌀ 39.9 mm. A 110 mm pipe (⌀ 9,503 mm² incl. sleeve) is far past this.
2. Large threshold = d/4 = **139.8 mm**. A 160 mm sleeve (for a 110 mm pipe) **exceeds** it → this is a **large opening** → full engineered detailing required.
3. Height check: 160 ≤ 0.4 d = 223.6 mm → geometry acceptable *if* engineered.
4. Compression-face clearance: ≥ 0.33 d = **184.5 mm** from the top face to the top edge of the hole → hole centreline sits at ≥ 184.5 + 80 = 264.5 mm below the top → roughly mid-depth. Consistent.
5. End-zone check: keep it ≥ 2 × 600 = **1,200 mm** clear of each column face.

**Verdict:** technically feasible, but for a *house* the correct answer is almost always **do not put a 110 mm soil pipe through a beam.** Reroute: drop the WC in a duct/shaft alongside the beam, or step the false ceiling, or shift the WC 300 mm so the stack lands in the wet-wall shaft. A 160 mm hole in a 300 × 600 house beam buys you 100 mm of ceiling height at the price of a designed, inspected, rebar-critical detail.

### 3.5 The pass/fail decision tree for any proposed beam penetration

```
Pipe/conduit needs to cross a beam line
        │
        ├─ Can it be rerouted around the beam (shaft, wall chase, ceiling drop, fixture shift)?
        │       └─ YES → reroute. STOP. (Correct answer ~90% of house cases.)
        │
        ├─ Is it a gravity drain (slope-locked, cannot be lifted)?
        │       ├─ YES → is a lowered false ceiling / stepped soffit acceptable?
        │       │          └─ YES → drop the ceiling. STOP.
        │       └─ Continue only if genuinely trapped.
        │
        ├─ Is the beam a transfer beam / cantilever / key element?
        │       └─ YES → NO OPENING. Redesign the service route. STOP.
        │
        ├─ Is the location inside 2×D of a column face, or in the outer third of span?
        │       └─ YES → relocate to the middle third. Re-enter tree.
        │
        ├─ Size class?
        │       ├─ Small (≤1000 mm² / ≤0.004d²) → cast-in sleeve, note on structural drawing.
        │       ├─ Intermediate (≤ d/4)          → engineer check + trimming bars.
        │       └─ Large (> d/4)                 → full engineered detail, 2×shear stirrups over d/2,
        │                                           corner diagonals, engineer stamp.
        │
        └─ In ALL cases: sleeve is CAST-IN on the structural shop drawing before pouring.
           Post-cast coring through a beam without engineer approval = defect.
```

### 3.6 Cast-in vs. post-cast coring

| | Cast-in sleeve | Post-cast core drill |
|---|---|---|
| Rebar control | Bars are shifted/trimmed **by design**, drawn and checked | Bars are cut **blind**; GPR/rebar scanner reduces but does not eliminate risk |
| Location accuracy | Fixed by formwork; verify before pour | Free, but that is the problem |
| Cost | ~0 (a piece of PVC and a nail) | Rig, operator, water, delay, remediation |
| Acceptable in a beam? | **Yes, when designed** | **No** without a stamped structural approval and a scan record |
| Acceptable in a slab? | Yes | Small holes only (see 4.3), scanned, engineer-noted |

---

## Section 4: Slab Penetrations and Sleeve Planning

### 4.1 Sleeve sizing

Sleeve internal diameter = pipe OD + **25–50 mm annulus**, so the pipe can be adjusted, insulated and fire-stopped.

| Service pipe (nominal) | Pipe OD approx. | Sleeve ID | Sleeve material |
|---|---|---|---|
| 15–25 mm water | 20–32 mm | 50 mm | PVC offcut |
| 32–40 mm waste | 40–50 mm | 63–75 mm | PVC |
| 50 mm waste / shower | 63 mm | 90 mm | PVC |
| 75 mm waste / rain | 90 mm | 110 mm | PVC |
| 110 mm soil / stack | 110 mm | **160 mm** | PVC or MS pipe |
| 160 mm main drain | 160 mm | 200 mm | MS pipe |
| Split-AC refrigerant + drain pair | — | 75 mm sloped **outward 1:100** | PVC |
| Electrical riser bank | — | size to conduit count + 30% spare | GI or PVC |

**Fire-stopping:** any sleeve crossing a fire compartment floor gets an intumescent collar or approved mastic seal. In a single-family house this matters most at the **stair enclosure**, **garage-to-house slab**, and **service shaft floors**.

### 4.2 Where slab penetrations may and may not go

| Zone | Rule |
|---|---|
| Within **0.2 × span of a support / near a column** | Avoid — punching shear zone in a flat slab, high negative moment in a beam-slab |
| **Column strip** of a flat slab | Avoid entirely; group services into the **middle strip** |
| Mid-span of a one-way slab | Best zone for small penetrations |
| **Post-tensioned slab** | **Zero tolerance** — never drill. All penetrations pre-planned, tendon layout drawing overlaid before any hole is marked |
| Cantilever slab (balcony, chajja) | No penetrations in the top 1/3 near the root; rainwater outlets at the free edge only |
| Grouped penetrations (bathroom cluster) | Treat as one large opening: trim with edge bars, provide a **cast-in RC upstand kerb 75–100 mm** around wet-area clusters |

### 4.3 Small unplanned holes in slabs

A single hole ≤ **⌀ 40 mm** in a house slab away from supports, with a **rebar scan** confirming no bar is cut, and with the engineer notified, is normally tolerable. Anything larger, anything in a cluster, anything near a support, or anything that cuts a bar → engineer decision. Record every one on the as-built.

### 4.4 Trimming reinforcement around slab openings (planning default)

- Opening < 150 mm: no trimming needed if no bar cut; shift bars around it.
- Opening 150–500 mm: replace the interrupted bars with **equivalent area added each side** of the opening, plus **2 × ⌀12 diagonal bars 1,000 mm long** at each corner.
- Opening > 500 mm (e.g. a stair well or a duct shaft): treat as a structural opening — trimmer beams, engineer design.

---

## Section 5: Electrical Conduit Routing in RCC

### 5.1 Governing rules

Everything in Section 2 applies. On top of it:

| Rule | Value / requirement |
|---|---|
| Position within slab depth | Conduit sits **between the top and bottom reinforcement mats**, ideally in the **middle third of the slab depth** |
| Never | Displace, cut, bend or rest a conduit *on top of* the top mat where it steals cover |
| Cover retained to **rebar** | Conduit must not reduce rebar cover below IS 456 Table 16: **20 mm mild / 30 mm moderate / 45 mm severe** exposure |
| Crossing angle | Cross main bars at **~90°**; never run a conduit parallel to and directly above/below a main bar for more than ~500 mm |
| Conduits in one plane at a crossing | **Max 3**; beyond that, fan them out or step levels |
| Cluster at a DB drop | Add a local **mesh reinforcement patch** (e.g. ⌀8 @ 150 c/c, 1,000 × 1,000 mm) over the conduit fan, tied above the conduits |
| Bends | Long-radius sweeps; **max 3 × 90° bends** between pull points; provide a junction box at the 4th |
| Spare capacity | Leave **≥ 30% spare** conduit space and a pull-string in every riser — retro-chasing an RCC wall is how houses get cracked |
| Expansion / movement joint crossings | Never cast a rigid conduit straight across a movement joint — use a flexible coupling |
| Columns & shear walls | **No conduit.** Route in adjacent masonry or a shaft (see 2.4) |

### 5.2 Chases in masonry (the correct alternative to cutting RCC)

| Chase type | Max depth | Note |
|---|---|---|
| Vertical chase in a masonry wall | **≤ 1/3 wall thickness** | ⚠ VERIFY against local byelaw / BS 5628 practice |
| Horizontal chase in a masonry wall | **≤ 1/6 wall thickness** | Horizontal chases are far more damaging — avoid where possible |
| Chase in an **RCC shear wall / column** | **Not permitted** | — |
| Back-to-back chases on opposite faces | **Not permitted** | Offset by ≥ 300 mm horizontally |
| Chase within | 300 mm of an opening jamb, or below a lintel bearing | Avoid |

### 5.3 Buried conduit — NEC Table 300.5 (distinct rule set) ⚠ VERIFY edition

Minimum cover, **in soil**, for a residential installation:

| Wiring method / condition | Min cover |
|---|---|
| Direct-buried cable | **600 mm (24 in)** |
| Rigid metal / intermediate metal conduit | **150 mm (6 in)** |
| Rigid non-metallic conduit (PVC) approved for direct burial | **450 mm (18 in)** |
| Residential branch circuit ≤ 120 V, 20 A, GFCI-protected | **300 mm (12 in)** |
| Under a building | 0 (must be **in a raceway**) |
| Under a driveway / parking area (one/two-family dwelling) | **450 mm (18 in)** |
| Under 100 mm (4 in) concrete slab exterior, no vehicle traffic | **450 mm** raceway, or reduced per the table footnotes |

Add a **warning tape 300 mm above** the run and a route marker at every change of direction. In Pakistan, the wiring installation itself follows Pakistan Electricity Rules 1937 and the BS/PS-derived electrical works chapter; the cover depths above are the NEC values used in practice for coordination drawings.

### 5.4 Separation from other services

| Pair | Min clear separation |
|---|---|
| Power conduit ↔ data/telecom conduit (parallel run) | **300 mm** (or a metallic barrier) |
| Power conduit ↔ water pipe (parallel) | **150 mm**, power **above** water where possible |
| Power conduit ↔ gas line | **300 mm**, and never in the same chase/shaft |
| Any conduit ↔ hot water / boiler flue | **150 mm** + insulation |
| Crossings | 90° crossings may reduce to 50 mm with a sleeve/barrier |

---

## Section 6: Plumbing — Stacks, Drainage Slope and Venting

### 6.1 Minimum slope of horizontal sanitary drainage (IPC §704.1 / Table 704.1)

This table is the whole ballgame for coordination: **drainage slope is the one MEP dimension that cannot be negotiated away**, so it wins every clash against ducts, conduit and pressure pipe.

| Pipe size | Min slope (imperial) | Min slope (metric) | Fall per metre | Fall over 6 m run |
|---|---|---|---|---|
| ≤ 2½ in (≤ 65 mm) | **¼ in / ft** | **≈ 2.08 %** (1:48) | 20.8 mm | 125 mm |
| 3 in – 6 in (75–150 mm) | **⅛ in / ft** | **≈ 1.04 %** (1:96) | 10.4 mm | 62 mm |
| ≥ 8 in (≥ 200 mm) | **1/16 in / ft** | **≈ 0.52 %** (1:192) | 5.2 mm | 31 mm |

- **Practical house default:** 100 mm soil line at **1:80 to 1:60** (12.5–16.7 mm/m). Steeper than 1:40 is *not* better — the liquid outruns the solids and the line silts up.
- **Self-cleansing velocity:** target **≥ 0.6 m/s** (2 ft/s) at design flow; ≤ 3 m/s to avoid scour.
- **Uniform slope:** IPC requires *uniform* slope. Sags and back-falls are the #1 cause of a blocked house drain and are invisible until commissioning — check with a level and a water test, not by eye.

### 6.2 The invert-level budget (the calculation that drives coordination)

Before you fix finished floor level, run this and see whether the drain can actually get out.

```
Available fall  =  (Invert of the ground-floor WC connection)  −  (Invert at the septic tank inlet)
Required fall   =  (total horizontal run in m) × (slope from Table 6.1)
                 + 50 mm  drop across the septic tank (inlet→outlet invert, per IS 2470)
                 + fall required from tank outlet to soak pit
Margin          =  Available − Required     →  MUST be positive, target ≥ 100 mm slack
```

**Worked example.** Ground-floor WC in the rear bath, 14 m run to an inspection chamber, then 6 m to the septic tank.
- 100 mm pipe at 1:80 → 12.5 mm/m × 20 m = **250 mm** total fall.
- Plus 150 mm for two IC drops and bends. → Tank inlet invert must be **≥ 400 mm** below the WC connection invert.
- WC connection sits ~50 mm below FFL inside a 100 mm floor screed. So the tank inlet invert lands **≈ 450 mm below FFL**, and the tank internal soffit + freeboard pushes the **tank excavation to roughly 2.0–2.3 m deep** for a 1.05 m liquid depth. Check this against water table *and* against Section 10 setbacks **before** finalising the plinth level. On a flat plot in Lahore/Karachi with a high water table this is exactly where designs break — the answer is usually to raise the plinth, not to flatten the drain.

### 6.3 House pipe sizing (planning defaults)

| Fixture / line | Trap size | Waste/branch | Vent |
|---|---|---|---|
| Wash basin | 32 mm | 40 mm | 32 mm |
| Kitchen sink | 40 mm | 50 mm | 40 mm |
| Shower / bath | 50 mm | 50 mm | 40 mm |
| Washing machine | 40 mm | 50 mm | 40 mm |
| Floor drain | 50 mm | 50–75 mm | — |
| WC | integral | **110 mm** | 50 mm |
| Soil stack (whole house) | — | **110 mm** | 110 mm through roof |
| Waste stack (no WC) | — | 75 mm | 75 mm |
| Main house drain to septic | — | **110–160 mm** | — |
| Rainwater downpipe | — | 75–110 mm (1 per ~40–60 m² roof) | — |

- **Trap seal depth: 50 mm minimum.** Deep seal (75 mm) in hot dry climates / infrequently used floor drains, or fit a trap primer.
- **Trap arm max length (trap to vent), IPC Table 909.1** ⚠ VERIFY edition: 32 mm → 1.5 m; 40 mm → 1.8 m; 50 mm → 2.4 m; 75 mm → 3.6 m; 100 mm → 3.6 m.
- **Cleanouts (IPC Ch. 708)** ⚠ VERIFY: at the **base of every stack**, at every change of direction > 45°, at the building drain exit, and at intervals **≤ 30 m** on horizontal runs.
- **Vent terminal:** ≥ 150 mm above the roof surface, ≥ 600 mm above / 3 m horizontally from any openable window or air intake.

### 6.4 Stack layout rules that keep plumbing out of structure

1. **One wet-wall per floor plate.** Stack all WCs, basins and kitchen on a single vertical plane where possible — one stack, one shaft, one set of penetrations.
2. **Stack the bathrooms vertically** between floors. A first-floor bath that does not sit over the ground-floor bath forces a horizontal drain run inside the floor zone — which is where beams live.
3. **Shaft, not chase.** Provide a real duct/shaft **≥ 300 × 450 mm clear** for a 110 mm stack plus vent plus water risers. Frame it with the structure (a slab opening), do not carve it later.
4. **Offsets in a stack** below the topmost fixture need relief venting and are a clash generator — design a straight stack.
5. **Never route a gravity drain through a beam if a 150 mm ceiling drop solves it.** Compare: 160 mm engineered beam opening vs. a gypsum ceiling 150 mm lower over a 1.2 m corridor strip. The ceiling wins.
6. **Bathrooms over habitable rooms** need the drain in a **sunk slab (150–250 mm sunk) or a raised platform**. Decide this at structural design stage — a sunk slab is a structural instruction, not a plumbing one.

---

## Section 7: Mechanical / HVAC and Water Storage Loads

### 7.1 Split-AC and ducting in a house

| Item | Coordination requirement |
|---|---|
| Refrigerant + drain wall sleeve | 65–75 mm PVC, sloped **1:100 outward**, min 150 mm from any beam/column face, never through a lintel |
| Condensate drain | Min **1 % (1:100)** continuous fall to a safe discharge; never into a soil stack without a trap |
| Outdoor unit on a slab/parapet | 50–120 kg point load + vibration — set on a plinth over a beam line, with 25 mm neoprene isolators |
| Ceiling-concealed unit | Needs **350–450 mm** clear plenum + a **600 × 600 mm** access panel; verify against beam soffit before promising a flat ceiling |
| Duct crossing a beam line | **Ducts never pass through beams in a house.** Transition to a flat oval / step the ceiling / re-route |
| Kitchen exhaust duct | 150 mm ⌀, direct to outside, through **masonry** not RCC, with a fire damper if it crosses a compartment |
| Services zone under beam soffit | Allow **200–350 mm** for a typical house; state it on the section drawing before slab levels are frozen |

### 7.2 Water tanks — the concentrated load nobody coordinates

| Tank | Typical house capacity | Water mass | Note |
|---|---|---|---|
| Overhead tank (OHT) | 500 imp gal = 2,273 L | **2.27 t / 22.3 kN** | — |
| Overhead tank (OHT) | 1,000 imp gal = 4,546 L | **4.55 t / 44.6 kN** | Common Pakistani house default |
| Underground tank (UGT) | 1,000–2,000 imp gal | 4.5–9.1 t | Below slab, but see 7.3 |
| Solar geyser on roof | 150–300 L + collector | 0.2–0.4 t | Still a point load |

**Worked example — the OHT that cracks the roof slab.** A 1,000 gal PVC tank has a footprint ≈ 1.8 × 1.2 m = **2.16 m²**. Load = 44.6 kN / 2.16 m² = **20.6 kN/m²**. A typical residential roof slab is designed for a live load of **1.5–2.0 kN/m²**. That is a **10–14× overload** on that patch.

**Therefore:**
- The OHT position must be fixed at **structural design stage**, not by the plumber.
- Support it on a **plinth/kerb that spans onto beams or columns**, never on the mid-span of a slab panel.
- Tell the structural engineer the tank capacity, footprint and exact grid position; it becomes a designed patch load.
- Water storage sizing for the brief: **135–200 L/person/day** total demand; OHT ≈ ⅓–½ of one day's demand, UGT ≈ 1–2 days.
- UGT within 3 m of a foundation → check for hydrostatic uplift when empty and for softening of founding soil if it leaks. Line it and keep it **≥ 3 m from the septic tank and ≥ 15 m from any soak pit**.

### 7.3 Gas pipeline coordination (LPG cylinder/manifold and SNGPL piped natural gas)

Gas is not a minor incidental service in Pakistani houses — most kitchens run on either an **SNGPL piped natural gas** connection or a **cylinder/manifold LPG** setup, and both interact with structure and with the other services in ways that matter for a coordination pass, not just the separation-distance line items already in 5.4 and the embedment note in Section 2.

| Item | Requirement / coordination note |
|---|---|
| Governing authority (piped gas) | **SNGPL/SSGC** service-connection rules; OGRA safety regulations for the overall gas sector. House-side pipework and appliance connection is normally done by an SNGPL-approved fitter — this skill does not substitute for that sign-off. |
| Governing authority (LPG) | **OGRA LPG (Marketing) Rules** and OGRA LPG (Distribution/Marketing) safety rules for cylinder storage, manifold rooms and regulator sets |
| Embedment in RCC | Gas pipe is **never embedded in a slab, wall or beam** the way water/electrical runs are — Section 2's 1/3-thickness rule assumes a plumbing/electrical/data conduit; a gas line cast into concrete cannot be inspected, pressure-tested in place, or repaired without breaking out structure. **Route gas exposed, in a surface-mounted or chased masonry (not RCC) run, or in a dedicated riser/duct — never cast in.** |
| Sleeve at a wall/floor crossing | Where a gas line must cross a wall or floor, it passes through a **sleeve with clearance annulus** (as Section 4.1), sealed at the ends with a non-combustible mastic — never grouted solid, and never a friction-fit cast-in embedment |
| Routing near electrical | **≥ 300 mm** clear from power conduit, never sharing a chase or shaft with electrical (Section 5.4) — a gas leak into an electrical shaft is an ignition-source risk, not just a code checkbox |
| Routing near heat sources | Keep clear of flues, boiler exhausts and hot-water pipework; do not run gas pipe directly above/below a hot service without clearance and, where unavoidable, insulation |
| LPG cylinder/manifold location | **Outdoors or in a dedicated, ventilated enclosure** — never inside a habitable room, never below grade (LPG is heavier than air and pools in pits/basements), clear of drains and any ignition source; keep away from the septic tank/soak pit vent (Section 9/10) for the same pooling-gas reason |
| Ventilation | Any enclosed gas meter/manifold room needs **high-level and low-level ventilation openings** — piped gas (lighter than air) needs the high vent, LPG (heavier than air) needs the low vent; do not rely on one or the other alone if the house could ever switch supply type |
| Isolation valve | An accessible, clearly marked shut-off valve at the point of entry to the house, before the first branch — coordinate its location into the plant/meter zone (11.3), not tucked behind a fixed cupboard |
| Leak-test before concealment | Any gas run gets a **pressure/soap test witnessed and recorded before it is boxed in, tiled over, or the ceiling is closed** — this is the gas equivalent of the plumbing water-test in Section 6.1, and is just as easy to skip and just as dangerous to skip |
| Never | Never let a gas line join Section 2's "merely passing through" logic as if it were a plumbing/electrical embedment — the exemption language in 2.2 is written for pipes and conduit generally, but a gas installer, not this skill's embedment table, decides how a gas line actually crosses a structural member |

**This subsection is a coordination-planning aid, not a gas-fitting design.** Actual gas pipe sizing, pressure-drop calculation, and appliance connection must be done and signed off by an SNGPL-approved gas fitter / licensed gas contractor — this is a public-safety scope (fire/explosion risk) fully outside a structural or architectural coordination pass.

---

## Section 8: Septic Tank Sizing (IS 2470 Part 1)

For a house with no municipal sewer — normal in peri-urban and rural Pakistan.

### 8.1 The formula

```
V = P × ( C × T  +  N × S )

V = required liquid volume (litres)
P = number of users (design occupancy, not current)
C = sewage flow per person per day (L)
T = detention period (days)
N = desludging interval (years)
S = sludge accumulation per person per year (L)
```

### 8.2 Parameter selection

| Parameter | Value | When to use |
|---|---|---|
| **C** — sewage flow | **85–90 L/p/d** | Rural, hand pump / limited supply |
| | **120 L/p/d** | Standard urban house — **default** |
| | **135–150 L/p/d** | Premium house, multiple bathrooms, washing machine, dishwasher |
| **T** — detention | **1.0 day** | Standard — **default** |
| | **1.5 days** | Low flow (< 6 users) or rural intermittent use |
| **N** — desludging | **2 years** | Standard house — **default** |
| | 1 year | Commercial / heavy use |
| | 3 years | Deliberately oversized, remote site, no easy tanker access |
| **S** — sludge accumulation | **25–35 L/p/yr** (use **30**) | Higher end where kitchen grease is significant |

### 8.3 Tank geometry (IS 2470 Pt.1)

| Parameter | Requirement |
|---|---|
| Length : Width | **2:1 to 4:1** (2:1 typical for a house) |
| Liquid depth | **1.0 – 1.8 m** (1.0–1.2 m typical for small tanks) |
| Freeboard above liquid | **≥ 300 mm** |
| Chambers | **Two**, split **2/3 (first) + 1/3 (second)** of volume |
| Baffle wall | Full-height with a submerged transfer slot at mid-depth |
| Inlet tee/pipe submergence | **150 – 200 mm** below liquid level |
| Outlet tee/pipe submergence | **350 – 450 mm** below liquid level |
| Inlet → outlet invert drop | **≥ 50 mm** |
| Access covers | **≥ 600 × 600 mm**, one per chamber, gas-tight, over inlet and outlet tees |
| Vent pipe | 50–75 mm, terminating ≥ 2 m above ground and clear of windows, with a mosquito-proof cowl |
| Min practical liquid volume | **1,000 L** even if the formula gives less |
| Walls / base | 230 mm brick in cement mortar or 150 mm RCC; **12 mm cement plaster (1:3) with waterproofing compound** internally; watertight base — a leaking septic tank next to a foundation is a settlement risk |

### 8.4 Worked example A — 6-person urban house

```
P = 6,  C = 120 L/p/d,  T = 1.0 d,  N = 2 yr,  S = 30 L/p/yr

V = 6 × (120 × 1 + 2 × 30)
  = 6 × (120 + 60)
  = 6 × 180
  = 1,080 L  liquid volume
```

Size the box: choose liquid depth **1.05 m**, L:W = 2:1.
- Required plan area = 1.080 m³ / 1.05 m = **1.029 m²**
- W = √(1.029 / 2) = 0.717 m → adopt **W = 0.75 m**, **L = 1.50 m**
- Provided liquid volume = 1.50 × 0.75 × 1.05 = **1.181 m³ = 1,181 L ✓** (9% margin)
- Overall internal depth = 1.05 + 0.30 freeboard = **1.35 m**
- Chamber split: first chamber 1.00 m long, second 0.50 m long (2:1)
- Excavation depth ≈ 1.35 + 0.15 base + inlet invert depth from 6.2 → ~2.0–2.3 m

### 8.5 Worked example B — 10-person joint-family rural house

```
P = 10,  C = 90 L/p/d,  T = 1.5 d,  N = 2 yr,  S = 30 L/p/yr

V = 10 × (90 × 1.5 + 2 × 30)
  = 10 × (135 + 60)
  = 10 × 195
  = 1,950 L
```

Liquid depth 1.20 m → plan area 1.625 m² → L:W 2.5:1 → W = 0.81 → adopt **W = 0.85, L = 2.10 m** → 2.10 × 0.85 × 1.20 = **2.142 m³ = 2,142 L ✓**. Overall internal depth 1.50 m.

### 8.6 Quick-size table (T = 1.0 d, N = 2 yr, S = 30, freeboard 300 mm)

| Users | C = 90 L/p/d | C = 120 L/p/d | C = 150 L/p/d | Suggested L × W × liquid depth (at C=120) |
|---|---|---|---|---|
| 4 | 600 L → use 1,000 | 720 L → use 1,000 | 840 L → use 1,000 | 1.40 × 0.70 × 1.05 m |
| 5 | 750 → 1,000 | 900 → 1,000 | 1,050 | 1.40 × 0.70 × 1.05 m |
| **6** | 900 → 1,000 | **1,080** | 1,260 | **1.50 × 0.75 × 1.05 m** |
| 8 | 1,200 | 1,440 | 1,680 | 1.70 × 0.80 × 1.10 m |
| 10 | 1,500 | 1,800 | 2,100 | 2.00 × 0.85 × 1.10 m |
| 12 | 1,800 | 2,160 | 2,520 | 2.20 × 0.90 × 1.15 m |
| 15 | 2,250 | 2,700 | 3,150 | 2.50 × 1.00 × 1.15 m |
| 20 | 3,000 | 3,600 | 4,200 | 2.90 × 1.15 × 1.15 m |

*(Always re-verify the chosen box volume against the formula — the table rounds to buildable brick dimensions.)*

---

## Section 9: Soak Pit / Soil Absorption (IS 2470 Part 2)

The septic tank does **not** dispose of effluent; it only settles it. Disposal is the soak pit's job, and the soil decides the size.

### 9.1 Percolation test — do it, do not guess

Dig a 300 × 300 mm test hole at the proposed soak pit invert depth. Pre-soak 4 hours (24 h in clay). Fill to 150 mm and time the drop of the last 25 mm.

| Time for 25 mm drop | Interpretation | Action |
|---|---|---|
| **< 5 min** | Excessively rapid — groundwater contamination risk | **Not acceptable** as-is; increase separation from wells, consider a lined trench/filter bed |
| **5 – 60 min** | Acceptable | Design normally |
| **> 60 min** | Inadequate absorption | **Dispersion trench / raised mound / packaged treatment required** — a soak pit will surcharge |

### 9.2 Percolation load by soil type

| Soil type | Percolation capacity (L/m²/day) | Suitability |
|---|---|---|
| Gravel / coarse sand | **50** | Excellent — but check well separation (see 10.1) |
| Sandy loam / fine sand | **40** | Good |
| Loam | **30** | Good |
| Silt loam / porous clay | **20** | Fair |
| Clay loam | **12** | Poor — dispersion trench likely required |
| Clay / black cotton soil | **8** | Unsuitable for a pit — **dispersion trench mandatory** |

### 9.3 Sizing method

```
Effluent flow Q (L/day)         =  P × C          (same C as the septic calc)
Required absorption area A (m²) =  Q / percolation capacity
Design on SIDEWALL AREA ONLY:      A = π × D × H_eff
                                   (the base silts up within a year — do not count it)
H_eff = effective depth of the pit BELOW the inlet invert
```

**Geometry limits:** diameter **0.9 – 2.5 m**; effective depth **1.0 – 3.0 m**; pit base must clear the highest seasonal water table by **≥ 1.5 m**; fill with **40–80 mm graded stone / brick bats**, top 300 mm sand + soil, with an access cover and a vent.

### 9.4 Worked example — 6-person house (continuing 8.4)

```
Q = 6 × 120 = 720 L/day
Soil = sandy loam → 40 L/m²/day
A required = 720 / 40 = 18.0 m²  (sidewall)

Try D = 1.8 m:  H_eff = 18.0 / (π × 1.8) = 3.18 m  → exceeds the 3.0 m limit
Try D = 2.1 m:  H_eff = 18.0 / (π × 2.1) = 2.73 m  → OK
Try D = 2.4 m:  H_eff = 18.0 / (π × 2.4) = 2.39 m  → OK

ADOPT: soak pit ⌀ 2.4 m diameter × 2.4 m effective depth below inlet
       (the calculated 2.39 m is rounded UP to 2.4 m to the nearest practical
       excavation increment — a deliberate conservative rounding, not the
       exact calculated figure; never round down on an absorption-area check)
       + 0.3 m top cover  →  total excavation ≈ 2.7 m
       Water table must be below 2.4 + 1.5 = 3.9 m from inlet invert.
```

If the water table is shallower, **do not just make the pit smaller** — switch to **two smaller pits in parallel** (≥ 3 m apart, alternating via a diversion chamber) or a **dispersion trench**: 600 mm wide × 600–900 mm deep trench, 100 mm perforated pipe on gravel at **1:200 fall**, trench length = A / 0.6 m width, max 30 m per trench line, trenches ≥ 2 m apart.

### 9.5 ⚠ Discrepancy flag — the "1.5 m × 2.0 m per 1000 L/day" field rule

Field guides commonly quote *"~1.5 m diameter × 2.0 m deep soak pit per 1,000 L/day in gravel/coarse sand."* **This does not reconcile with the area calculation:**

- Sidewall only: π × 1.5 × 2.0 = 9.42 m² × 50 L/m²/day = **471 L/day**
- Sidewall + base: 9.42 + 1.77 = 11.19 m² × 50 = **560 L/day**

The rule of thumb is roughly **half** of what the calculation supports. **Use the calculation (9.3), not the rule of thumb.** Where the field figure appears in a client's or contractor's proposal, flag it — an undersized soak pit surfaces as sewage ponding in the second monsoon, not on handover day.

### 9.6 Two-pit / alternating design (recommended default)

Provide **two pits sized at 100% each**, with a diverter chamber. Use one for 2 years, switch, let the first rest and biologically recover. Cost delta is small at house scale; it roughly doubles the system's service life and removes the single point of failure.

---

## Section 10: Siting and Separation Distances

### 10.1 Minimum separations (IS 2470 Pt.1/Pt.2 + NBC 2016; check local byelaw for stricter)

| From | To | Minimum |
|---|---|---|
| Septic tank / soak pit | **Drinking water well or borewell** | **15 m** |
| Septic tank / soak pit | Well, in **fissured rock, gravel or laterite** | **30 m** |
| Septic tank | Building foundation | **3 m** |
| Soak pit | Building foundation | **3 m** (5 m preferred — saturated soil under a footing is a settlement risk) |
| Septic tank / soak pit | Plot boundary | **5 m** |
| Septic tank / soak pit | Large tree / root zone | **8 m** |
| Soak pit base | Highest seasonal groundwater table | **≥ 1.5 m clearance** |
| Soak pit | Adjacent soak pit | **≥ 3 m** (2 × pit diameter) |
| Septic tank | Underground water storage tank | **≥ 15 m** — never on the same side as the UGT inlet |
| Septic tank access | Vehicle/tanker access route | Within **30 m** of a hose reach, otherwise desludging is impossible |

**If the plot cannot satisfy these** (common on a 5-marla urban plot), the honest answer is: **this plot cannot take on-site disposal** — connect to the sewer, or use a sealed holding tank with scheduled pump-out, or a packaged treatment unit with a compliant discharge point. Do not shrink the setbacks. Say this to the user explicitly.

### 10.2 Slope and drainage siting

- Septic/soak pit **downhill and downgradient** of any water source.
- Never under a driveway, parking bay, or future extension footprint.
- Never inside the **zone of influence of a foundation**: keep clear of a 1:2 (V:H) line drawn down and out from the underside of the nearest footing. For a footing at 1.5 m depth, that is ~3 m horizontally — which is exactly why the 3 m rule exists.

---

## Section 11: Coordination Workflow and Clash Prevention

### 11.1 Sequence — architecture and structure lock first

```
1. ARCHITECTURAL layout frozen      → room positions, wet areas, FFL, ceiling heights
2. STRUCTURAL grid + depths frozen  → column grid, beam depths, slab thickness/type,
                                       sunk-slab zones, cantilevers, transfer elements
3. SERVICE ZONES declared           → shaft sizes, plenum depth, beam-soffit clearance,
                                       wet-wall plane, riser positions, OHT/UGT positions
4. MEP ROUTED within those zones    → drainage first (slope-locked), then large ducts,
                                       then large pipes, then pressure pipes, then conduit
5. PENETRATION SCHEDULE produced    → every sleeve, tagged, sized, located, classified
6. STRUCTURAL ENGINEER reviews      → approves / relocates / details each penetration
7. CLASH REVIEW on the federated model → hard, soft, 4D
8. SHOP DRAWINGS issued for casting → sleeves appear on the structural drawing
9. PRE-POUR SITE CHECK (Section 12) → physical verification before concrete
10. AS-BUILT recorded               → every sleeve, every deviation
```

**Never invert steps 2 and 4.** Routing MEP before beam depths are fixed guarantees rework.

### 11.2 Space-allocation priority (who yields to whom)

When two services want the same volume, the **lower number wins**:

| Priority | System | Why |
|---|---|---|
| 1 | **Structure** | Immovable |
| 2 | **Gravity drainage (soil, waste, rainwater)** | Slope-locked; cannot be lifted or offset freely |
| 3 | **Large ducts** | Large section, limited flexibility, needs straight runs |
| 4 | **Large pipes (fire main, large water main)** | Bulky, but can offset |
| 5 | **Small pressure pipes (water, gas)** | Can bend and route freely |
| 6 | **Electrical conduit / cable tray / data** | Most flexible — always the one that moves |

If electrical is forcing a beam penetration, the routing is wrong. Priority-6 services do not cut priority-1 elements.

### 11.3 Coordination hot zones (where 80% of house clashes occur)

| Hot zone | Typical clash | Mitigation |
|---|---|---|
| **Wet-wall / bathroom cluster** | 110 mm stack vs. beam or column | Fix the shaft in the structural grid at concept stage |
| **Kitchen wall** | Sink waste + gas + power + exhaust in one 115 mm wall | Use a 230 mm wall or a service void |
| **Under-stair** | Drain run + DB + water riser + storage | Reserve it as a service zone; do not sell it as a cupboard |
| **Riser / duct shaft at every floor** | Slab penetration alignment drifts floor to floor | Single plumb-line dimension from the grid, repeated on every plan |
| **Ceiling plenum in corridors** | Drain crossing beams; AC duct vs. beam soffit | Declare the plenum depth (200–350 mm) and hold it |
| **Pump / plant room, UGT top** | Pump base, pipes, DB, ventilation | Give it 1.5 m clear working space; it is a room, not a leftover |
| **Roof / OHT plinth** | Tank load, solar mounts, vent terminals, rainwater outlets | Coordinate as patch loads on the roof structural plan (Section 7.2) |
| **Balcony / chajja** | Rainwater outlet through a cantilever root | Outlet at free edge only |
| **Garage / porch slab** | Buried conduit cover under a driveway | NEC 300.5 depths (5.3) |

### 11.4 Clash classification

| Class | Definition | House example | Resolution |
|---|---|---|---|
| **Hard clash** | Two solids occupy the same volume | 110 mm stack passes through a 600 mm beam | Reroute, or engineer the opening |
| **Soft clash** | Clearance, access or maintenance envelope violated | AC unit fits, but no room for the 600 × 600 access panel | Move; enforce clearance zones as modelled solids |
| **4D / sequencing clash** | Physically fine, but not installable in that order | Sleeve required in a slab already poured; tank set after the wall that blocks the crane | Sequence review; sleeve schedule before the pour |
| **Code clash** | Geometry fine, code violated | Drain at 1:200 on a 100 mm line; soak pit 8 m from the well | Table-check against Sections 6, 9, 10 |

### 11.5 Clash detection at house scale

Professional practice runs a federated model in Navisworks / Revit / Solibri. For a single house that is overkill; the equivalent rigour is:

1. **Overlay method.** Print/plot architectural + structural + MEP at the same scale and origin; overlay. Every crossing of a service line with a beam line is a penetration candidate — mark it.
2. **Section cuts.** Cut a section through **every wet wall and every corridor** and draw the beam soffit, plenum, duct and drain to scale. Most clashes are invisible in plan and obvious in section.
3. **Model-based (FreeCAD).** See Section 13 — boolean intersection of a structure group against an MEP group; any non-zero result volume is a hard clash.
4. **Penetration schedule as the single source of truth** (11.6) — if a hole is not on the schedule, it does not get cut.

### 11.6 Penetration schedule format

Every sleeve gets a tag: `SL-<storey>-<discipline>-<nn>` (e.g. `SL-GF-P-07`, disciplines P/E/M/D = plumbing/electrical/mechanical/drainage).

| Tag | Storey | Element | Element ID | Service | Sleeve ⌀ | Position (grid X, Y, level) | Class (S/I/L) | Engineer status | Cast-in date |
|---|---|---|---|---|---|---|---|---|---|
| SL-GF-D-01 | GF | Slab | S-101 | 110 soil | 160 | B2/C2 +150 | S | Approved | — |
| SL-FF-P-04 | FF | Beam | B-207 | 50 waste | 90 | 2.4 m from C3 | I | **Pending** | — |

**Nothing with a Pending or Rejected status may be cast or cut.**

---

## Section 12: Pre-Pour Sign-Off Checklist

Run this **physically, on site, before every concrete pour**. It takes 20 minutes and it is the last free chance to fix any of it.

- [ ] Penetration schedule printed and in hand; every sleeve for this pour has status **Approved**
- [ ] Every scheduled sleeve is **physically present** in the formwork, at the scheduled position (tape-measured off two grid lines, not eyeballed)
- [ ] Sleeves are **capped/plugged** so concrete cannot enter, and **braced** so they cannot float or shift
- [ ] No sleeve or conduit exceeds **1/3 of member thickness**; spacing ≥ **3 diameters** c/c (Section 2)
- [ ] Beam openings: none inside **2 × D of a column face**; all in the middle third of span; all with the specified **flanking stirrups and corner diagonals** already tied
- [ ] Slab openings: trimming bars / corner diagonals in place; no opening in the column strip of a flat slab; **no penetration in a PT slab** without the tendon-layout overlay signed
- [ ] Conduits sit **between the two rebar mats**; nothing is stealing cover; **≥ 3 conduits max** at any crossing; mesh patch present over the DB fan
- [ ] Concrete cover to conduit ≥ **40 mm** (earth/weather) / **20 mm** (internal); cover blocks in place
- [ ] Sunk-slab zones formed at the scheduled depth for bathrooms over habitable rooms
- [ ] Drain **invert levels and falls** set out and checked with a level — not by eye (Section 6.2)
- [ ] Drainage line has **continuous uniform fall**; no back-fall, no sag; water-test the run where possible
- [ ] OHT / plant plinth reinforcement and position match the structural patch-load drawing (Section 7.2)
- [ ] Movement-joint crossings use flexible couplings, not rigid cast-in conduit
- [ ] Photographs taken of **every sleeve and conduit run before the pour**, tagged with the schedule ID → this becomes the as-built record
- [ ] Structural engineer (or their site representative) has **signed the pour card**

**And after the pour:** update the as-built drawing the same week. A sleeve nobody recorded is a sleeve somebody will core through later.

---

## Section 13: FreeCAD / BIM Modeling Workflow for MEP Coordination

For use alongside `architecture-freecad-bim`.

### 13.1 Model organisation

```
Site
└── Building
    ├── Storey_GF
    │   ├── BP_Structure   (Arch Walls, Structures, Slabs, Beams, Columns)
    │   ├── BP_Architecture(partitions, doors, windows, fixtures)
    │   └── BP_MEP
    │        ├── Grp_Drainage   (Arch Pipe / PipeConnector, 110/75/50)
    │        ├── Grp_Water
    │        ├── Grp_Electrical (conduit runs, DB solids)
    │        └── Grp_Sleeves    (the void objects)
    └── Storey_FF ...
```

Keep MEP in its **own BuildingParts/groups** so a whole discipline can be hidden, exported, or intersected as one body.

### 13.2 Sleeves as live parametric voids, not frozen booleans

Model each sleeve as a cylinder/box and add it to the host wall/slab/beam's **`Subtractions`** list (Arch object property) — the same technique the FreeCAD BIMExample uses for window openings. This keeps the opening **parametric**: move the sleeve, the hole moves. A one-off `Part → Cut` freezes the geometry and breaks the moment someone shifts a fixture.

- Sleeve object naming = the schedule tag: `SL_GF_D_01`.
- Add `Description` = service + size, so it survives IFC export as a readable property.
- For beam openings, model the **actual designed void**, not the pipe — the void is what the structural engineer approves.

### 13.3 Clash check by boolean intersection

```python
# FreeCAD Python console — hard-clash check between two discipline groups
import FreeCAD as App, Part
doc = App.ActiveDocument

def solids(group_label):
    grp = doc.getObjectsByLabel(group_label)[0]
    out = []
    for o in grp.OutList:
        if hasattr(o, "Shape") and o.Shape.Solids:
            out.append(o)
    return out

struct = solids("BP_Structure")
mep    = solids("BP_MEP")

TOL = 1e-6
for s in struct:
    for m in mep:
        common = s.Shape.common(m.Shape)
        if common.Volume > TOL:
            print(f"HARD CLASH: {s.Label} <-> {m.Label}  vol={common.Volume/1000:.1f} cm3")
```

Any printed line is a hard clash. Then:
- If the host already has that sleeve in `Subtractions`, the intersection volume goes to ~0 → the penetration is *modelled and accounted for*.
- If it is still non-zero → the pipe is passing through solid concrete that nobody has approved. **Log it in the penetration schedule; do not silently subtract it.**

### 13.4 Soft-clash (clearance) check

Model **clearance envelopes as transparent solids** and run the same intersection:
- Access panel zone: 600 × 600 × 600 mm in front of every concealed unit / valve / cleanout.
- Maintenance zone in the plant room: 900 mm clear in front of the pump/DB, 1.5 m for a UGT hatch.
- Desludging access: a 1.0 m clear corridor from the septic access cover to the tanker route.

A clearance solid intersecting a wall, a slab or another service is a **soft clash** — report it as such, do not treat it as noise.

### 13.5 Checks to run before exporting IFC

- [ ] Every pipe has a real diameter (not a default), so the 1/3 rule can actually be checked
- [ ] Every drain run has the correct slope modelled (a horizontal drain in the model is a lie that hides an invert-level failure)
- [ ] Every sleeve exists as a `Subtractions` void on its host, with the schedule tag as its Label
- [ ] Discipline groups export as separate IFC classes (IfcPipeSegment, IfcDuctSegment, IfcCableCarrierSegment) — verify by re-importing the export, not by assuming
- [ ] Penetration schedule (11.6) regenerated from the model, not maintained by hand in parallel

---

## Section 14: Common Failure Modes (and the rule each one breaks)

| Failure seen on site | Rule broken | Correct action |
|---|---|---|
| Plumber cores a 110 mm hole through a 300 × 450 beam near a column | §3.2 forbidden zone + cast-in rule | Stop work; engineer assessment; likely jacketing / FRP repair |
| 40 mm conduit cast in a 100 mm slab | ACI 20.6 (limit 33 mm) | Limit to 32 mm, or thicken the slab locally |
| Six conduits fanned in one plane over a DB | §5.1 (max 3) | Step levels; add mesh patch |
| Bathroom drain at 1:150 on a 100 mm line | IPC 704.1 (min 1:96) | Re-lay at ≥ 1:96; usually needs a sunk slab or higher plinth |
| Back-fall of 15 mm mid-run, invisible in plan | IPC "uniform slope" | Level survey + water test before closing the floor |
| 1,000 gal OHT set mid-span on a bedroom roof slab | §7.2 (20.6 vs 2.0 kN/m²) | Relocate over beams; engineer check for cracking |
| Septic tank 4 m from the borewell | §10.1 (15 m) | Relocate or abandon on-site disposal — public health issue |
| Soak pit sized from the "1.5 m × 2.0 m" rule of thumb | §9.5 | Recalculate from percolation area |
| Soak pit base 0.5 m above the water table | §9.3 / §10.1 (1.5 m) | Redesign: dispersion trench or raised mound |
| Bathroom on 1st floor not stacked over ground-floor bath | §6.4 rule 2 | Either stack them or accept a sunk slab + ceiling drop, decided at structural stage |
| Sleeve present in the wall, absent from any drawing | §11.6 | Add to as-built; check what it passed through |
| Post-cast chase cut horizontally across a 115 mm wall for a 32 mm conduit | §5.2 (1/6 = 19 mm) | Surface conduit / skirting trunking, or a service void |
| Condensate drain teed straight into the soil stack | §7.1 | Trap it, or run to a separate safe discharge |

---

## Section 15: Quick Reference Card

```
EMBEDMENT (ACI 318 §20.6)
  Pipe/conduit embedded in slab/wall/beam:  OD ≤ 1/3 member thickness
  Spacing:                                   ≥ 3 diameters c/c
  In a column:                               total area ≤ 4% of gross section
  Cover to conduit:                          ≥ 40 mm earth/weather, ≥ 20 mm internal
  "Merely passing through" is exempt from 1/3 — but NOT from "shall not impair strength"

BEAM OPENINGS (SP 34-derived detailing practice — see §3.0: not a single citable IS 456 clause)
  Small:        area ≤ 1000 mm² (d ≤ 500) or ≤ 0.004 d² (d > 500)
  Large:        any dimension > d/4  → engineered detail, 2× shear stirrups over d/2
  Height:       ≤ 0.4 d      Edge from compression face: ≥ 0.33 d
  Clear gap between openings: ≥ 150 mm
  Keep out of: end zones (2×D from column face), outer third of span, transfer/cantilever beams

GAS (LPG / SNGPL piped) — §7.3
  Never embedded in RCC — exposed, chased masonry, or dedicated riser only
  ≥300 mm from power conduit, never shared chase/shaft with electrical
  LPG cylinder/manifold: outdoors or dedicated ventilated enclosure, never below grade
  Leak/pressure test witnessed and recorded BEFORE any concealment
  Sizing, pressure-drop and appliance connection = licensed gas fitter scope, not this skill

DRAINAGE SLOPE (IPC 704.1)
  ≤ 65 mm  → 1/4 in/ft = 2.08 %      (20.8 mm/m)
  75–150   → 1/8 in/ft = 1.04 %      (10.4 mm/m)
  ≥ 200    → 1/16 in/ft = 0.52 %     (5.2 mm/m)
  Self-cleansing velocity ≥ 0.6 m/s; uniform slope, no sags.

SEPTIC (IS 2470 Pt.1)     V = P × (C×T + N×S)
  C 90 rural / 120 urban / 150 premium L/p/d   T = 1.0 d (1.5 low-flow)
  N = 2 yr    S = 25–35 (use 30) L/p/yr        Min 1,000 L
  L:W 2:1–4:1 · liquid depth 1.0–1.8 m · freeboard ≥ 300 mm · 2 chambers 2/3 + 1/3
  Inlet tee 150–200 mm submerged · outlet tee 350–450 mm · invert drop ≥ 50 mm
  Access covers ≥ 600 × 600 mm
  6-person example: 6×(120+60) = 1,080 L → 1.50 × 0.75 × 1.05 m

SOAK PIT (IS 2470 Pt.2)   A = Q / percolation ;  A = π D H_eff (sidewall only)
  gravel/coarse sand 50 · sandy loam 40 · loam 30 · silt loam 20 · clay loam 12 · clay 8
  Perc test: <5 min excessive · 5–60 min OK · >60 min → dispersion trench
  Base ≥ 1.5 m above water table · D 0.9–2.5 m · H_eff 1.0–3.0 m

SETBACKS
  Tank/pit → well 15 m (30 m fissured rock/gravel/laterite)
  → foundation 3 m · → boundary 5 m · → trees 8 m · pit → pit 3 m

PRIORITY WHEN SERVICES CLASH
  Structure > gravity drainage > large ducts > large pipes > pressure pipes > conduit

AND ALWAYS
  Every penetration cast-in, scheduled, and engineer-approved BEFORE the pour.
  Nothing here is construction-ready until a licensed (PEC) engineer stamps it
  and the local authority approves the plan.
```
