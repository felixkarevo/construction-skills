---
name: architecture-roofing-waterproofing
description: >
  Roofing systems and building-envelope waterproofing for houses: RCC flat roof
  slab detailing and membrane build-ups, pitched roof and truss selection,
  parapet/coping and rainwater drainage design with falls calculations, damp-proof
  course and rising-damp control, basement and foundation waterproofing (positive,
  blind and negative side), bathroom and wet-area tanking, and the ranked catalogue
  of real-world leakage failure points with the detailing rules that prevent them.
  Includes numeric tables, worked examples, code citations (ASCE 7-22 Ch.8,
  ACI 318-19, IRC 2021 R406, IBC 2021 §1805, BS 6229:2018, BS 8102, IS 3067/1346,
  ANSI A118.10, NHBC Ch.7.2) and FreeCAD/BIM modelling guidance.
---

# Roofing & Building Envelope Waterproofing for Houses

Water is the single most destructive agent acting on a house, and almost every water failure is a **detailing failure, not a materials failure**. Industry claims data (NRCA) puts *flashing and junction detailing* — not membrane defects — as the number-one cause of roof leaks. This skill is the design-side counterpart to `architecture-structural-systems`: it covers how the roof slab or truss is shaped, sloped, drained, tanked and terminated so that the structure stays dry for its design life. It is calibrated for **single- and two-storey houses**, with a bias toward the RCC flat-roof + parapet construction that dominates Pakistan, India and the Gulf, while carrying the pitched-roof/truss and UK/US code material needed for other contexts.

Use this skill **before** modelling any roof, parapet, plinth, basement or bathroom in FreeCAD, and **before** writing any roofing or waterproofing specification, BOQ line or detail drawing. Pair it with `architecture-structural-systems` (slab spans, foundations), `architecture-seismic-design` (parapet and roof-to-wall connection bracing/reinforcement in seismic zones), `architecture-spatial-planning` (wet-area stacking), `architecture-freecad-bim` (model hierarchy) and `drawio-diagrams` (2D detail drawings).

---

## Reality Check - Licensing & Liability

**This skill produces design aids and calculation guidance for planning and FreeCAD modelling ONLY.**

- Every number, table, span, thickness, slope, drain size and detail in this file is a **preliminary sizing and coordination aid**. None of it is a construction-ready design.
- Any design intended for the **actual construction of a real occupied building** MUST be reviewed, calculated and **stamped by a licensed structural engineer registered with the relevant authority** — in Pakistan a **PEC-registered** professional engineer; elsewhere the equivalent (SE/PE in the US, Chartered Engineer/IStructE in the UK, etc.). Waterproofing specifications for basements and podium/plaza decks should additionally be reviewed by a specialist waterproofing consultant or the membrane manufacturer's technical department, and warranties are void without their sign-off.
- The design MUST pass **local authority plan approval** before construction — LDA, CDA, RDA, TMA/Municipal byelaws in Pakistan; the equivalent building-control or permit authority elsewhere. Setbacks, parapet heights, rainwater discharge points, plinth levels and basement depths are all byelaw-controlled and vary by jurisdiction.
- Clause-level requirements of the **Building Code of Pakistan 2007 / SBC-07** and the **BCP 2021 draft** were not fully retrievable in searchable form when this skill was written. Where a local clause is needed for submission, the actual PDF must be consulted (URLs in Section 16). Do not cite a BCP clause number that has not been read. This same rule applies to every other cited code below: where this file states what a clause requires, verify the exact clause/table/footnote text in the actual current edition before it appears in a stamped drawing or submission — do not assume which edition introduced a provision, or that a paraphrase here is the verbatim requirement.
- **Claude / Claude must never present FreeCAD geometry, a layer build-up, a falls calculation or a drain-sizing table from this skill as construction-ready.** If a user starts treating the output as final — asks a contractor to price it, sends it for construction, or says "so we can build this" — say so **unprompted**, in plain language, before continuing: *this is a planning model; it needs a PEC-registered engineer's stamp and local authority approval before anyone pours concrete.*
- Waterproofing failures are expensive, slow to appear and hard to reverse. When uncertainty exists, state the uncertainty and recommend the conservative detail; never invent a code clause, a warranty term, a product data-sheet value or a local unit rate.

---

## Section 1: Roof System Selection

### Decision Tree: Which Roof System?

```
1. Is the roof surface to be USED (terrace, sleeping, water tank, solar, garden)?
   ├─ YES → Flat RCC roof, accessible grade. Waterproofing MUST be protected
   │         (screed + tile/paver topping). Go to Section 2 + 3.
   └─ NO  → continue

2. Annual rainfall / peak intensity?
   ├─ > 1000 mm/yr OR peak 5-min intensity > 100 mm/hr (monsoon, coastal)
   │    → Prefer pitched, or flat with over-sized redundant drainage (Section 5)
   └─ < 600 mm/yr (arid: Lahore ~630 mm, Karachi ~200 mm, Quetta ~250 mm)
        → Flat RCC is culturally and economically dominant; still design falls

3. Snow load present (northern areas, Murree, Gilgit-Baltistan, Swat)?
   ├─ YES → Pitched, ≥ 6/12 (26.6°) to shed; design for ASCE 7-22 Ch.7 /
   │         local ground snow load; avoid valleys and internal gutters
   └─ NO  → continue

4. Span / structural system already chosen?
   ├─ RCC frame or load-bearing masonry with RCC slab → flat RCC (Section 2)
   ├─ Steel or timber frame, long clear span → truss/pitched (Section 6)
   └─ Both → cost and maintenance decide (table below)

5. Insulation / thermal performance a priority (energy code, comfort)?
   → Warm-roof build-up (insulation ABOVE structure, below membrane or
     inverted above membrane) — see Section 4. Cold roofs need ventilation.
```

### Flat RCC vs Pitched — Comparison

| Criterion | Flat RCC slab | Pitched RCC | Pitched truss (timber/steel) |
|---|---|---|---|
| Typical span | 3.5–6.5 m (one-way), 4–8 m (two-way) | 3.5–6 m | 6–12 m (Fink), 12–20 m (attic/scissor/steel) |
| Structural depth | 100–200 mm slab | 100–150 mm slab | 300–1200 mm truss depth |
| Usable roof surface | Yes (terrace, tank, solar) | No | No (attic possible) |
| Waterproofing criticality | **Critical** — water sits | Moderate — water sheds | Low — covering sheds, underlay is 2nd line |
| Typical structure cost (indicative $/m²) | 55–95 | 65–110 | 45–85 |
| Life of waterproofing layer | 8–20 yrs (membrane dependent) | 15–25 yrs | 25–50 yrs (tile/metal covering) |
| Failure mode | Ponding → membrane fatigue → slab leak | Slippage at flashings | Underlay UV degradation, flashing |
| Thermal mass benefit | High (good for hot-dry Punjab nights) | High | Low (needs insulation at ceiling) |
| Dead load (structure only) | 2.5–5.0 kN/m² | 2.5–4.5 kN/m² | 0.4–0.9 kN/m² |
| Best fit | Urban plots, terrace culture, tanks/solar | Rare in residential | Snow zones, hill stations, long-span halls |

**Rule:** never call a roof "flat". Every "flat" roof is a **low-slope** roof with a minimum designed fall. A truly level roof is a defect.

---

## Section 2: RCC Flat Roof Slab Detailing

### 2.1 Slab Thickness — Deflection Control (ACI 318-19)

If the empirical minimum thickness is met, an explicit deflection calculation per **ACI 318-19 §24.2** is **not required**. This is the fastest legitimate route to a defensible preliminary slab thickness.

**One-way slabs — ACI 318-19 Table 7.3.1.1 / 24.2.2** (non-prestressed, normalweight concrete, fy = 420 MPa, not supporting partitions likely to be damaged by deflection):

| Support condition | Minimum h |
|---|---|
| Simply supported | ℓ / 20 |
| One end continuous | ℓ / 24 |
| Both ends continuous | ℓ / 28 |
| Cantilever | ℓ / 10 |

For fy other than 420 MPa, multiply by `(0.4 + fy/700)` with fy in MPa.

**Two-way slabs without interior beams — ACI 318-19 Table 8.3.1.1** (ℓn = clear span in long direction; long:short clear-span ratio must not exceed 2):

| Panel condition | Without drop panels | With drop panels |
|---|---|---|
| Exterior panel, no edge beams | ℓn / 30 | ℓn / 33 |
| Exterior panel, with edge beams | ℓn / 33 | ℓn / 36 |
| Interior panel | ℓn / 33 | ℓn / 36 |
| **Absolute minimum h** | **125 mm** | **100 mm** |

Values tabulated above are for **fy = 420 MPa**. ACI 318 also has provisions addressing higher-grade (e.g. Grade 550) reinforcement in its deflection/thickness clauses. **Do not treat that as a settled fact about what changed between ACI editions** — this file has not verified the exact table/footnote wording in the current ACI 318-19 text. Before citing a specific footnote or Grade-550 adjustment factor in a stamped drawing, pull the actual current ACI 318-19 table and footnotes and confirm the wording directly; for any grade other than 420 MPa, treat the multiplier/interpolation as something the engineer of record must confirm against the primary source, not something to take from this summary.

**Practical residential RCC roof slabs (Pakistan/India norms, verify by calc):**

| Clear span (two-way, room) | Typical slab h | Typical reinforcement (indicative only) |
|---|---|---|
| up to 3.0 m | 100–115 mm | 10 mm @ 150 c/c both ways |
| 3.0–4.0 m | 115–125 mm | 10 mm @ 125 c/c both ways |
| 4.0–5.0 m | 125–150 mm | 12 mm @ 150 c/c both ways + top steel at supports |
| 5.0–6.0 m | 150–175 mm | 12 mm @ 125 c/c + edge/torsion steel |
| 6.0–7.5 m | 175–200 mm, or beam-and-slab | Engineer-designed |

Cover to reinforcement on a roof slab: **20 mm** minimum (interior/protected soffit), **40 mm** for the top face if permanently exposed or in aggressive/coastal environments. Do not shave cover to gain depth — corroding top steel in a leaking roof slab is the terminal failure mode.

### 2.2 The Slab Is Not the Waterproofing

An RCC slab, even a well-compacted one with 0.45 w/c and an integral admixture, is **not watertight** at cracks. Design intent:

1. **Slab = structure + first line of resistance** (dense, low-permeability, crack-controlled)
2. **Membrane = the actual waterproofing** (continuous, laid to falls, dressed up all upstands)
3. **Screed/topping = protection + slope** (protects membrane from UV, foot traffic, thermal shock)

Crack control on the structural slab, before membrane:
- Water/cement ratio ≤ 0.45–0.50; slump 75–100 mm; no site water added after batching
- Continuous wet curing **minimum 7 days** (14 days preferred in Punjab summer); ponding or hessian + polythene
- Integral crystalline or hydrophobic admixture (Xypex Admix, Penetron Admix, Sika WT) reduces permeability but **does not replace a membrane**
- Construction joints located at low-shear positions with a hydrophilic waterstop or swellable strip
- Distribution steel at the top face to control shrinkage/thermal cracking in exposed slabs
- **Cure fully and dry before priming.** Membrane over green or damp concrete is the classic blistering/debond failure.

### 2.3 Rain Loads and Ponding — ASCE 7-22 Chapter 8

This is the most-cited *structural* cause of flat-roof failure: the slab deflects, water collects in the deflection, added weight increases deflection — **ponding instability**.

**ASCE/SEI 7-22 Ch.8 requirements:**
- Rain load **R = 0.0098 (ds + dh)** kN/m², with ds and dh in mm
  (US units: R = 5.2 (ds + dh) psf, with ds, dh in inches)
  - `ds` = depth of water to the inlet of the *secondary* drainage system when the primary is blocked (static head)
  - `dh` = additional hydraulic head above the secondary inlet at design flow
- The formula itself combines static head (ds) and hydraulic head (dh) into one rain-load term. **This file has not verified, clause-by-clause, exactly what changed between ASCE 7-16 and ASCE 7-22 on whether ponding head was previously optional** — do not repeat a specific "no longer optional, this is new in 7-22" claim without reading both editions' Ch.8 text yourself; treat "ponding head must be included in the rain-load calc" as the safe design practice regardless of edition, and confirm the precise clause wording before citing an edition-specific change in a submission.
- A **secondary (overflow) drainage system is mandatory**, with its inlet set **higher** than the primary inlet, and both sized on the design storm return period (100-yr / 15-min in common ASCE 7-22 practice — confirm the exact return period requirement in the clause before citing it)
- Roofs must be checked for **ponding instability** where the roof slope toward drains is small

**Quick conversion:** 100 mm of standing water = **0.98 kN/m²** (~1.0 kN/m²) added dead-ish load. For a domestic roof designed at 1.5 kN/m² imposed, 150 mm of ponded water consumes the entire live-load allowance.

### 2.4 Minimum Slope

| Standard / practice | Minimum fall | Notes |
|---|---|---|
| General RCC flat-roof practice (IN/PK) | **1:50 (2%)** = 20 mm per metre | Design value; the reliable target |
| Absolute minimum "finished" fall (BS 6229 principle) | 1:80 (1.25%) *as built* | Design at 1:40 so that construction tolerance still yields ≥1:80 |
| Gutter / channel falls | 1:100 to 1:200 | Continuous, no back-falls |
| Wet-area / bathroom floors (IPC) | **1/4 in per ft = 1:48 ≈ 2.1%** | To floor drain |
| Shower seats, curbs, sills, niches | 1:50 minimum, all horizontal surfaces | "Everything must slope to the drain" |

**Design rule:** specify **1:40 (25 mm/m)** on drawings for a house roof, and use 1:40 consistently as the design fall in every worked calculation in this file. Screeding tolerances of ±10 mm over 3 m routinely eat 1:100 of fall. Designing at the minimum guarantees back-falls somewhere.

---

## Section 3: Waterproofing Membrane Systems

### 3.1 System Comparison Table

> **Cost data caveat — read before using any figure below:** every dollar figure in this table is US market data, order-of-magnitude only, for relative comparison between systems — not for entry into any BOQ. If you are quoting or copying a single row for a Pakistan/India estimate, **stop**: these numbers must be re-quoted locally first. Do not convert to PKR/INR and present as a local estimate.

| System | Typical thickness | Service life | Installed cost (**USD/ft², US market data — do not use for a Pakistan/India BOQ without local re-quotation**) | Crack bridging | UV stable | Best use |
|---|---|---|---|---|---|---|
| **Torch-applied APP modified bitumen** (single ply) | 3 mm or 4 mm | 10–18 yrs | $4–7 | Good (2–3 mm movement) | Only if mineral-surfaced | Flat RCC roofs, hot climates (APP = polypropylene, high softening pt) |
| **Torch/self-adhered SBS modified bitumen** | 3 mm or 4 mm | 12–20 yrs | $4–7 | Very good, better cold flex | With cap sheet | Cold climates, movement joints |
| **2-ply modified bitumen** | 2 × 3 mm | 15–25 yrs | $3.50–6.50 | Excellent (redundant) | Cap sheet | Terraces, podiums, high-value roofs |
| **3-ply modified bitumen / BUR** | 3 layers | 20–30 yrs | $4–7 | Excellent | Cap sheet | Plaza decks, large flat roofs |
| **Liquid-applied polyurethane (PU)** | 1.5–2.5 mm DFT | 10–15 yrs | $3–8 | Excellent, seamless | Yes (aliphatic topcoat) | Complex geometry, many penetrations, parapets |
| **Liquid-applied polyurea (spray)** | 2–3 mm | 15–25 yrs | $7–12 | Excellent | Needs topcoat | Tanks, fast-track, complex shapes |
| **Cementitious 2-component flexible** | 2 coats, 2 mm total | 10–15 yrs | $1.50–3 | Limited (<0.5 mm) | Yes, overcoatable | Wet areas, water tanks, negative side |
| **Crystalline integral / slurry** | 1–1.2 kg/m² slurry | Life of concrete | $1–2.50 | **None (>0.4 mm)** | N/A | Supplement only — never sole roof system |
| **EPDM sheet** | 1.14–1.52 mm | 25–35 yrs | $5–9 | Excellent | Yes | Simple large flat roofs, low penetration count |
| **TPO / PVC single ply** | 1.2–1.8 mm | 20–30 yrs | $5–10 | Excellent | Yes (white, high SRI) | Cool-roof requirement, mechanically fastened |
| **Hot-applied rubberised asphalt** | 90–125 mil (2.3–3.2 mm) | 30–40 yrs | $8–15 | Excellent, self-healing | No (must be buried) | Plaza/podium decks, under-slab, high hydrostatic head |
| **Bituminous acrylic / elastomeric coating** | 0.5–1.0 mm | 4–8 yrs | $0.80–2 | Poor | Yes | Refurbishment/economy only — NOT a primary house roof system |
| **Brick-bat coba** (traditional IN/PK) | 75–115 mm | 15–25 yrs if done well | local labour dominated | Mass system | Yes (tile finish) | Slope + insulation + protection in one; heavy (~1.8 kN/m²) |
| **Mud phaska + tile terracing** (traditional) | 75–100 mm mud + tile | 10–20 yrs | local | Mass system | Yes | Thermal mass + slope; poor if drainage neglected |

> **Cost caveat, repeated:** USD figures above are from US market data and are order-of-magnitude planning aids only. For Pakistan/India, **all rates must be re-quoted locally** before entering any BOQ. Do not convert these figures to PKR and present them as a local estimate.

### 3.2 Torch-On Modified Bitumen — Application Parameters

| Membrane thickness | Torch dwell time (indicative) | Side lap | End lap | Notes |
|---|---|---|---|---|
| 1.5 mm | 30–45 sec/m² | 75–100 mm | 100–150 mm | Underlayer / vertical faces only |
| 3 mm | 45–60 sec/m² | 100 mm | 150 mm | Standard single-ply roof |
| 4 mm | 60–75 sec/m² | 100 mm | 150 mm | Cap sheet, high-traffic terraces |

Application sequence (aligned with **IS 3067:1988** general preparatory practice and **IS 1346:1991** bitumen-felt roofing):

1. **Substrate**: fully cured (28 days ideal, 14 days minimum), dry (< 5% moisture by carbide/ hygrometer), clean, no laitance, no curing compound residue, no standing water
2. **Repair**: grind off fins and projections; fill honeycombs and blowholes with polymer-modified mortar; **cove fillet** 50 × 50 mm (min) at every wall/slab junction — a 90° internal corner is a guaranteed membrane split
3. **Cementitious slurry key coat / primer**: bitumen primer at 0.25–0.35 l/m², fully dry before torching (touch-dry, no solvent smell)
4. **Falls**: apply screed to falls **before** the membrane (screed-to-falls is preferred) or use a tapered insulation layer; membrane must never be asked to create the fall
5. **Lay from the low point upward**, so every lap sheds water downhill (shingle-fashion). Laps up-slope are a defect.
6. **Corners and penetrations first**: preformed corner pieces or a separate reinforcing patch under the field sheet. **No field seam at an inside or outside corner.**
7. **Upstands**: minimum **150 mm** above finished roof level (see Section 5), separately torched, mechanically terminated with a batten/termination bar into a chase, sealed with polyurethane sealant — **not sealant alone**
8. **Test**: flood test 24–48 h before any covering (Section 14)
9. **Protect immediately**: geotextile separation layer + protection screed/tiles. UV kills unprotected bitumen in 2–4 summers.

### 3.3 System Selection Decision Tree

```
Roof to be walked on / used as terrace?
├─ YES → 2-ply modified bitumen OR liquid PU, + geotextile + 50mm protection
│        screed + tile/paver finish. NEVER leave membrane as wearing surface.
└─ NO
   ├─ Many penetrations, parapets, odd geometry (typical small house)?
   │    → Liquid-applied PU (seamless, no laps to fail) or torch-on with
   │      preformed corners
   ├─ Simple large rectangle, low penetration count?
   │    → Single-ply EPDM/TPO (fastest, longest life) or torch-on 4mm
   ├─ Budget-critical, short horizon, existing roof refurbishment?
   │    → Liquid acrylic/bituminous coating — declare the 5–8 yr life honestly
   └─ Water tank / sunken slab / negative-side situation?
        → 2-component flexible cementitious + crystalline admixture
```

---

## Section 4: Roof Build-Ups (Stack-Ups)

Layer order matters more than layer choice. Always draw the stack bottom-up.

### 4.1 Warm Roof — Inaccessible (insulation above deck, membrane on top)

| # | Layer | Thickness | Weight (kN/m²) |
|---|---|---|---|
| 1 | RCC structural slab | 125–150 mm | 3.0–3.6 |
| 2 | Cement slurry key coat + bitumen primer | — | ~0.02 |
| 3 | Vapour control layer (VCL) — bitumen or 0.3 mm PE, laps sealed | 1–2 mm | 0.02 |
| 4 | Rigid insulation (XPS 30–50 kPa, or PIR) | 50–100 mm | 0.03–0.06 |
| 5 | Screed to falls, 1:40, min 40 mm at low point | 40–120 mm | 0.8–2.4 |
| 6 | Waterproofing membrane (3 mm torch-on / 1.8 mm PU) | 2–4 mm | 0.04 |
| 7 | Solar-reflective coating or mineral cap | — | 0.01 |
| | **Total** | **220–380 mm** | **~4.0–6.1** |

### 4.2 Inverted / Protected Membrane Roof — Accessible Terrace (recommended for hot climates)

| # | Layer | Thickness | Weight (kN/m²) |
|---|---|---|---|
| 1 | RCC structural slab | 125–175 mm | 3.0–4.2 |
| 2 | Slurry key coat + primer | — | 0.02 |
| 3 | **Screed to falls 1:40**, min 40 mm at outlet | 40–150 mm | 0.8–3.0 |
| 4 | Waterproofing membrane (2-ply modified bitumen) | 6 mm | 0.08 |
| 5 | **Flood test here** | — | — |
| 6 | XPS insulation (closed cell, water-resistant — XPS only, never EPS/PIR here) | 50–75 mm | 0.03 |
| 7 | Geotextile separation/filter layer (150–200 g/m²) | 1 mm | 0.01 |
| 8 | Protection screed OR pedestal-mounted pavers | 40–50 mm screed | 0.9–1.1 |
| 9 | Terrace finish: 20 mm tile / 40 mm paver | 20–40 mm | 0.4–0.9 |
| | **Total** | **300–500 mm** | **~5.2–9.3** |

The inverted arrangement puts the membrane under the insulation, where it never sees UV, foot traffic or the 70 °C summer surface temperature of a Lahore terrace. This roughly doubles membrane life.

### 4.3 Traditional Brick-Bat Coba (still valid, still common)

| # | Layer | Thickness |
|---|---|---|
| 1 | RCC slab, cured | 125–150 mm |
| 2 | Cement slurry with waterproofing compound | 2 coats |
| 3 | Brick-bat + lime/cement mortar laid to falls 1:50 | 75–115 mm (avg 90) |
| 4 | Curing 7–14 days, joints raked | — |
| 5 | 20 mm cement plaster 1:4 with waterproofing compound, IPS finish or clay tiles | 20–25 mm |
| | **Total** | **~230–290 mm**, dead load ~1.8–2.3 kN/m² above slab |

Advantages: creates slope, insulation and protection in one; repairable by any local mason. Disadvantages: heavy (must be in the structural load case from day one), quality entirely labour-dependent, no crack-bridging — a slab crack telegraphs straight through. **Best practice hybrid:** torch-on membrane on the slab, brick-bat coba as the protection/slope layer above it.

### 4.4 Cold Roof Warning

A cold roof (insulation at ceiling level, void above) requires **cross-ventilation of the void**: per IRC R806.2, net free ventilation area of **1/150** of the ventilated area, reducible to **1/300** when 40–50% of the vent area is in the upper portion of the space and a Class I/II vapour retarder is installed on the warm side. An unventilated cold roof in a humid climate condenses on the underside of the deck and reads as a "leak" that has no rain correlation. In flat RCC construction, **avoid cold roofs entirely — use warm or inverted.**

---

## Section 5: Slope, Drainage, Parapets & Rainwater Design

### 5.1 Falls — Worked Example A

**Roof:** 12.0 m × 9.0 m RCC terrace, Lahore, parapet on all four sides, two outlets on the north edge.

1. **Choose drainage layout.** Two outlets on the 12 m north edge, at 3 m and 9 m from the west corner. Maximum flow path from the south-east corner ≈ 9.0 m (across) with a 3.0 m diagonal component ≈ **9.5 m**.
2. **Fall at 1:40** (the design rule from Section 2.4, used consistently through this whole example). Rise over 9.5 m = 9500/40 = **237 mm**, plus 40 mm screed minimum at the outlet → **277 mm at the high point**. That is an unacceptable screed thickness for a house.
3. **Re-plan the drainage** — this is the actual lesson. Split the roof into more zones using screed valleys running to additional outlets, targeting a maximum flow path of ≈ **4.5 m** so the high-point screed stays in a buildable range.
4. **Revised layout:** five outlets along the north edge (up from two), positioned so no point on the roof is more than **4.5 m** from an outlet. Fall at **1:40** = 4500/40 = **112.5 mm** (round to 113 mm). Screed 40 mm at the outlet → **153 mm at the high point**, average ≈ **(40+153)/2 ≈ 96 mm**.
5. **Check against the high-point guideline:** 153 mm still exceeds the ~125 mm point past which adding another outlet is cheaper than thickening the screed further (see Section 10, failure point #2). A real project would iterate again here — split one more zone, or add a shallow valley — before finalising. This worked example carries the five-outlet numbers forward only to show how the resulting load is calculated; treat the additional iteration as the next step a designer must actually take, not as optional.
6. **Screed volume (five-outlet scheme, illustrative):** 108 m² × 0.096 m ≈ **10.4 m³**; dead load ≈ 0.096 × 20 kN/m³ = **1.92 kN/m²** — must be in the slab design load case.
7. **Weight check:** slab 150 mm (3.6) + screed (1.92) + membrane/finish (0.5) = **6.0 kN/m² dead**, plus 1.5–2.0 kN/m² imposed for an accessible terrace. Feed this back to the structural engineer *before* fixing slab depth.
8. **Ponding check (ASCE 7-22 Ch.8):** with secondary overflow scuppers set 50 mm above the primary outlet invert, ds = 50 mm; assume dh = 25 mm at design flow → R = 0.0098 × 75 = **0.74 kN/m²**. Confirm this is within the design imposed load and that slab deflection at mid-span does not create a local low point deeper than the fall (ponding instability).

**Lesson generalised:** the fall is set by the *longest flow path*, and the longest flow path is set by the *outlet layout*. Fix drainage layout first, screed second, always at the **1:40 design fall** — never switch to a laxer fall mid-calculation just because the numbers are inconvenient. If screed thickness still exceeds ~125 mm at the high point after a layout revision (as in step 5 above), that is the signal to iterate the layout again, not to accept the thick screed or to relax the fall.

### 5.2 Design Rainfall Intensity

Rainwater systems are sized from the **local short-duration design intensity**, not annual rainfall. Use a 1-in-50 or 1-in-100-year, 5-minute intensity for a roof with parapets (where overflow means water entering the building) and a 1-in-20-year value for free-edge roofs.

| Location class | Indicative design intensity (mm/hr) — **verify with local met data** |
|---|---|
| Arid inland (Quetta, Multan) | 50–75 |
| Punjab plains, monsoon (Lahore, Faisalabad) | 75–100 |
| Coastal / heavy monsoon (Karachi cloudburst, Mumbai, Chittagong) | 100–150 |
| Temperate UK/EU | 50–75 |
| US Gulf/Southeast | 100–175 |

> Never size a rainwater system from a table like this alone in a real project. Pull the actual IDF curve / 100-yr 15-min value from the meteorological department or the local code annex.

### 5.3 Gutter and Downspout Sizing

> **Unit/market caveat:** the base capacities and rules of thumb below come from US customary practice (inches, ft², in/hr) and US product sizing. Use them only as an order-of-magnitude cross-check; re-derive gutter/downspout/khurra sizing from the local design intensity (Section 5.2) and locally available product sizes before it goes into a Pakistan/India spec.

Base capacities are quoted at **1 in/hr (25.4 mm/hr)** and scale **inversely with intensity**.

| Component | Drainage area @ 1 in/hr | @ 2 in/hr (51 mm/hr) | @ 3 in/hr (76 mm/hr) |
|---|---|---|---|
| 5" K-style gutter | 5,520 ft² (513 m²) | 2,760 ft² (256 m²) | 1,840 ft² (171 m²) |
| 6" K-style gutter | 7,960 ft² (740 m²) | 3,980 ft² (370 m²) | 2,653 ft² (246 m²) |
| 3" round downspout | 706 ft² (65.6 m²) | 353 ft² (32.8 m²) | 235 ft² (21.9 m²) |
| 4" round downspout | 1,255 ft² (116.6 m²) | 628 ft² (58.3 m²) | 418 ft² (38.9 m²) |

**Rules of thumb (then check against the table):**
- One downspout per **~600 ft² (56 m²)** of roof area, **minimum two** per roof
- Or one downspout per **40 linear ft (12 m)** of gutter
- **Add 50%** capacity in heavy-rainfall regions
- Gutters fall **1:100 to 1:200** toward outlets; no back-falls; expansion joints every 12–15 m in metal gutters
- Roof area for sizing = **plan projected area**; for pitched roofs in windy conditions add an allowance for wind-driven rain (commonly plan area + 50% of the vertical wall area facing the prevailing wind)

**Flat-roof outlets (khurra / rainwater spouts) — practical sizing:** a 100 mm (4") outlet drains ≈ **39 m² at 76 mm/hr**. For the Worked Example A roof (108 m² at 76 mm/hr) the required capacity is 108/39 ≈ 2.8 → **at least 3 outlets of 100 mm**, and the five-outlet layout from Section 5.1 (driven by the falls/screed-thickness constraint, not by flow capacity alone) comfortably covers this with redundancy. Never rely on a single outlet on any roof, at any size.

### 5.4 Primary + Secondary (Overflow) Drainage — mandatory

ASCE 7-22 Ch.8 requires a **secondary drainage system with its inlet above the primary**. On a parapeted house roof:

- **Primary:** rainwater outlet with a domed leaf-guard grating, invert flush with the screed low point, connected to a downpipe
- **Secondary:** an **overflow scupper through the parapet**, invert set **50 mm above the primary invert** and **at least 50 mm below the level of any door threshold, DPC, or the top of the membrane upstand**
- Size the secondary for the full design flow — it must cope alone with the primary 100% blocked
- Discharge the secondary somewhere **visible** (weeping down the façade is the intended alarm — it tells the owner the primary is blocked)
- Minimum one overflow per drainage zone/quadrant, and one per enclosed low area created by a parapet, upstand or planter

### 5.5 Parapets and Copings

| Dimension | Requirement | Source |
|---|---|---|
| Waterproofing upstand above finished roof level | **≥ 150 mm** | BS 6229:2018; NHBC Standards Ch.7.2 |
| Upstand at door thresholds onto terraces | 150 mm ideal; 75 mm absolute minimum with a drained/heated threshold detail and channel drain | BS 6229 / NHBC accessible-threshold variance |
| Coping overhang each face | **≥ 40 mm** beyond the wall face | Parapet good practice / BS 5642 |
| Drip groove projection on coping underside | **≥ 5 mm** deep throat, min 10 mm from the face | BS 5642 |
| Coping DPC / cavity tray | Bedded **at or above** roof level, full width of coping, lapped 100 mm at joints, sealed | NHBC Ch.7.2 |
| Cavity-tray step-down over openings/abutments | **≥ 150 mm** vertical step | NHBC / Approved Doc C |
| Coping joint | Sealed movement joint with backer rod every 4–6 m; **never a butt joint left open** | BS 5642 |
| Parapet height (safety) | 1.0–1.1 m to top for an accessible terrace — check local byelaw (LDA/CDA) | Local authority |

**Seismic note — read before finalising any parapet in Pakistan:** everything in this section addresses the parapet as a **waterproofing/coping** element. It does **not** cover the parapet's own structural adequacy. Unreinforced or under-tied masonry/RCC parapets are a well-documented earthquake failure mode — out-of-plane overturning and collapse of the free-standing parapet, independent of any waterproofing detail. Pakistan is a high-seismic-zone country under BCP-SP-2007. **Load `architecture-seismic-design` before finalising parapet height, thickness, reinforcement and the roof-to-parapet structural connection** — this skill only governs what happens to the parapet once it is already structurally adequate.

**Canonical parapet detail, bottom-up:**

```
                     ┌───────────────┐  ← coping, falls INWARD to roof (1:40),
                     │  coping unit  │    ≥40mm overhang + drip groove BOTH faces
      ═══════════════╧═══════════════╧═══  ← coping DPC, full width, lapped 100mm
                     │               │
                     │   parapet     │
                     │   masonry     │
      outside        │               │   inside (roof)
                     │  ┌────────────┤  ← termination bar into 20×20 chase,
                     │  │ membrane   │    PU sealant over, mechanically fixed
                     │  │ upstand    │    (NOT sealant-only)
                     │  │ ≥150mm     │
                     │  │            │
    ─────────────────┴──┤            │  ← 50×50 cove fillet (mandatory)
      finished roof level └──────────╧═════════════  ← membrane, continuous,
    ══════════════════════════════════════════════      NO field seam at corner
              screed to falls 1:40
    ══════════════════════════════════════════════
              RCC slab
```

**Non-negotiables at a parapet:**
1. The membrane runs **continuously** from the roof field, over the cove fillet, up the parapet, with **no seam at the internal corner**
2. Cove fillet **50 × 50 mm** minimum in polymer mortar at every horizontal-to-vertical junction
3. Upstand **≥ 150 mm**, mechanically terminated (bar/batten in a chase), then sealed. Sealant is the *secondary* seal, never the primary one
4. Coping falls **inward**, so wind-driven water goes onto the roof (which is tanked) rather than down the façade (which is not)
5. Every coping joint is a designed, sealed movement joint
6. Coping DPC is separate from and *above* the membrane upstand termination
7. Parapet masonry itself absorbs water — render the roof face and consider a liquid membrane over the full parapet inner face, not just the 150 mm upstand
8. Parapet reinforcement, thickness and its structural tie to the roof diaphragm are a **seismic design item** (`architecture-seismic-design`), not a waterproofing item — do not finalise a parapet based on this section's dimensions alone

### 5.6 Flashing Typology — the #1 Failure Point, Detailed

Flashing is ranked first in leak-cause data (Section 10). Every flashing is a two-part assembly unless stated otherwise: a **base flashing** bonded to / continuous with the membrane and turned up ≥150 mm, and a **counter-flashing** mechanically fixed into a chase or reglet above it, lapping the base by ≥75 mm. Sealant closes the reglet; sealant is never the barrier.

| Flashing type | Where | Key dimensions | Failure if wrong |
|---|---|---|---|
| **Base + counter (two-part)** | All wall/roof abutments, parapets, curbs | Base ≥150 mm up; counter laps ≥75 mm; reglet 20 × 20 mm chase, 25 mm min into masonry | Sealant-only versions fail in 3–8 yrs |
| **Apron flashing** | Downslope face of a chimney or wall abutment | ≥100 mm onto the covering, ≥150 mm up the wall | Water driven behind at the low face |
| **Step flashing** | Sloping roof meeting a vertical wall | One piece per shingle/tile course; ≥100 mm × 100 mm legs; ≥50 mm head lap between pieces | A single continuous strip instead of steps = guaranteed leak |
| **Kickout (diverter) flashing** | Where a roof edge terminates at a wall (bottom of a step-flashed run) | Min 100 mm leg, bent ≥100° to throw water clear into the gutter; **IRC R903.2.1** | Water sheets into the wall cavity — the classic hidden-rot detail |
| **Chimney cricket / saddle** | Upslope side of any chimney | **Required where the chimney is > 30 in (762 mm) wide** — IRC R903.2.2; cricket slope ≥ the roof slope, min 1:12 | Snow/debris dam; standing water against masonry |
| **Valley flashing** | Internal roof valleys | 600 mm wide min (300 mm each side of centreline); self-adhered high-temp membrane full-bond beneath | Highest-volume flow path on the roof |
| **Vent-pipe boot / collar** | Every pipe penetration | Lead/EPDM boot with a 100 mm flange, membrane-collared and clamped; boot upstand ≥75 mm above the covering | Sealant-only collar = rank-3 failure |
| **Drip edge / gravel stop** | Eaves and rakes, flat-roof free edges | Set **flush or below** the membrane plane; ≥50 mm onto the deck, ≥25 mm down the fascia | Raised edge dams water — rank-4 failure |
| **Cavity tray / through-wall flashing** | Abutment of a lower roof to an upper wall | Step-down ≥150 mm; stop-ends both sides; weeps ≤900 mm c/c | Water in the wall above bypasses the roof upstand entirely |
| **Curb flashing** | Skylights, roof hatches, AC/plant plinths | Curb height ≥150 mm above finished roof (200 mm in heavy-snow zones); membrane dressed up and over the curb top | Flush-mounted plant is unwaterproofable |
| **Expansion-joint cover** | Structural movement joints crossing the roof | Raised twin-curb (each ≥150 mm) with a bellows membrane loop between | Flat-taped joints tear on the first thermal cycle |
| **Scupper / spout sleeve** | Parapet penetrations | Preformed sleeve with a 100 mm flange, membrane sandwiched, external drip lip | The parapet penetration is a hole in the tanking |

**Material selection:** stainless or lead-coated copper for chases in masonry; aluminium acceptable at eaves/rake drip edges but **never in direct contact with wet cement or copper** (galvanic/alkali attack); galvanised steel is the economy option and must be repainted on a cycle. In Pakistan practice, 24-gauge GI is common — specify it painted or, better, substitute stainless at chimney and valley locations where replacement means opening the roof.

---

## Section 6: Pitched Roofs and Trusses

### 6.1 Pitch Selection

| Pitch (rise/run) | Angle | Common name | Suitable coverings |
|---|---|---|---|
| 1/4 : 12 | 1.2° | Near-flat | Structural standing-seam metal only |
| 2/12 | 9.5° | Low slope | Asphalt shingle **only with doubled underlayment**; standing seam |
| 3/12 | 14.0° | Low slope | Standing seam, lapped metal panels |
| **4/12** | 18.4° | Conventional min | Asphalt shingle, metal, concrete tile (w/ underlay) |
| **6/12** | 26.6° | **Typical residential** | All coverings; walkable limit |
| 8/12 | 33.7° | Steep | Tile, slate, shingle; roof jacks needed |
| 9/12 | 36.9° | Steep | Tile, slate |
| 12/12 | 45.0° | Very steep | Slate, shingle, shakes; scaffolding required |

**Minimum pitch by covering (verify against manufacturer):** structural standing-seam metal 1/4:12 · architectural/lapped metal 3:12 · asphalt shingle 2:12 with double underlayment, 4:12 normal · concrete tile 2.5:12 with sealed underlay, 4:12 normal · clay pantile 4.5:12 · natural slate 4:12 minimum, 6:12 preferred · thatch 45°.

### 6.2 Truss Selection and Spacing

| Truss type | Span range | Typical use |
|---|---|---|
| **Fink (W-truss)** | 6–12 m (20–40 ft) | Dominant residential type |
| King post | 5–8 m | Short spans, exposed feature |
| Queen post | 8–10 m | Medium spans |
| Howe | 6–12 m | Steel or timber, industrial |
| Attic / room-in-roof | 7–11 m | Habitable attic, needs ≥ 8/12 pitch |
| Scissor | 8–14 m | Vaulted ceiling |
| Mono-pitch | 4–8 m | Lean-to, extensions |
| Steel portal/lattice | 12–30 m | Halls, workshops, garages |

**Spacing and members (US/light-frame practice):**
- **24" (600 mm) o.c.** standard for 2×4 chord trusses spanning 20–40 ft
- **16" (400 mm) o.c.** for heavier loads (tile covering, snow, storage attic) or 2×6 chords
- Purlins/battens sized to the covering: 38 × 50 mm battens at 300–345 mm gauge for concrete tile; 50 × 75 mm purlins at 900–1200 mm for corrugated metal
- Bracing: continuous lateral bracing to web members plus diagonal wind bracing in the plane of the rafters — **the number-one cause of truss roof collapse during construction is missing temporary bracing**
- Trusses are **engineered products** — the truss fabricator provides stamped calculations. Never size a truss from a general table for construction.

### 6.3 Pitched Roof Waterproofing Layers

The covering is the primary weather layer; the **underlayment is the actual waterproofing** and must be treated as such.

| # | Layer | Spec |
|---|---|---|
| 1 | Truss / rafter | Engineered |
| 2 | Deck (plywood/OSB 15–18 mm, or RCC/purlin system) | Continuous, screwed |
| 3 | **Underlayment** — breathable membrane, or self-adhered ice-and-water shield | 150 mm horizontal laps, 300 mm end laps, laid low-to-high |
| 4 | Self-adhered high-temp membrane at valleys, eaves (900 mm up-slope from the wall line in ice-dam zones), hips, penetrations | Full-bond |
| 5 | Counter-battens (drainage/ventilation gap 25–40 mm) | Along rafters |
| 6 | Tile battens | At covering gauge |
| 7 | Covering (tile, shingle, metal) | Per manufacturer |
| 8 | Flashings, ridge, hip, eaves comb, verge | Metal, mechanically fixed |

**Eaves/verge rules:** overhang the fascia so water enters the gutter, not behind it (gutter front edge below a line extended from the roof plane); drip edge/eaves flashing under the underlayment at rakes and over it at eaves; verge closed with a dry-verge system or bedded undercloak.

### 6.4 Ventilation of Pitched Roofs

- Cold roof: **1/150** net free area of the ventilated space; **1/300** if 40–50% of the vent area is high (ridge) and a vapour retarder is installed (IRC R806.2)
- Split roughly 50/50 between eaves (low) and ridge (high) to drive stack ventilation
- **Warm roof (insulation on the rafter line):** no ventilation required if a fully sealed vapour control layer is on the warm side — but a failed VCL in an unvented warm roof rots the deck silently. Use a breathable membrane above.

---

## Section 7: Damp-Proof Course (DPC) and Rising Damp

### 7.1 Rules

| Item | Requirement |
|---|---|
| Horizontal DPC height above finished external ground | **≥ 150 mm** (UK Approved Document C; widely used as a global rule of thumb) |
| DPC below timber ground floor | Above the ventilated void, continuous with the DPM |
| Vertical DPC at openings / abutments | Full height of the reveal, lapped to horizontal DPC and cavity tray |
| Cavity tray step-down | ≥ 150 mm vertically, with stop-ends and weep holes at max 900 mm centres |
| DPC lap | ≥ 100 mm, or full width at angles/junctions |
| Under-slab DPM | 0.3 mm (1200 gauge) polyethylene, 150 mm sealed laps, dressed up and lapped to the wall DPC |
| Plinth protection | Apron/paving falling **away** at 1:60 minimum for 600–1000 mm from the wall |

### 7.2 DPC Materials

| Material | Thickness | Notes |
|---|---|---|
| Polyethylene sheet DPC | 0.5 mm (500 micron) | Cheap, must not be punctured; poor at re-entrant corners |
| Bitumen felt / hessian-based | 1.5–3 mm | Traditional; can squeeze under heavy load |
| Polymer/pitch polymer | 1.1–1.5 mm | Best all-round flexible DPC |
| Engineering brick DPC (2 courses, Class B, in 1:3 mortar) | 2 courses | Common in older/heritage work, load-transmitting |
| **Cement mortar 1:2 with integral waterproofer, 20–25 mm** | 20–25 mm | **Standard Pakistan/India practice at plinth level**; add a coat of bitumen over it for better performance |
| Preformed cavity trays | Moulded | Use at all abutments — do not site-fabricate from sheet |

### 7.3 Termite / Anti-Pest Barrier Coordination with the DPC

In much of Pakistan's residential construction, a termite/anti-pest barrier is detailed at the same plinth zone as the DPC, and the two should be coordinated rather than treated as unrelated trades:

- **Soil-applied chemical barrier** (pre-construction termiticide treatment) goes down under the foundation and around the plinth **before** the DPC/DPM is laid — sequence it so the DPC install does not disturb the treated soil zone.
- **Physical termite barriers** (stainless steel mesh, graded-particle basaltic barriers) are installed at the same horizontal plane as the DPC, typically bedded into the plinth masonry alongside or just below the DPC course — treat them as running in parallel with the DPC, not as a substitute for it (a termite barrier stops insects; it does not stop rising damp, and vice versa).
- Any penetration through the DPC/termite-barrier plane (services, columns, steps) must maintain continuity of **both** systems — a gap left for one is usually a gap left for the other too.
- Never let the physical termite barrier double as, or replace, the structural DPC material — specify both, coordinated at the same level, as separate systems with separate continuity checks.

### 7.4 Common Rising-Damp Detailing Failures

1. **Ground level raised after construction** (new driveway, paving, planting) bridging the DPC — the single most common cause of "sudden" rising damp in an old house. Re-establish 150 mm, or form a drained gravel channel.
2. **Render or plaster carried down across the DPC line** onto the plinth — a mortar bridge. Stop external render 25 mm *above* the DPC with a bell-cast bead.
3. **Cavity fill / mortar droppings** bridging a cavity wall at DPC level.
4. **Internal floor screed lapped over the DPC without a DPM tie-in.** DPM and DPC must be physically lapped and sealed, not merely adjacent.
5. **Splash-back damp** — even a correct DPC will show damp to 300 mm above ground if rain splashes off hard paving. Use a gravel margin or a drip-detail plinth band.
6. **DPC omitted at internal walls** — internal load-bearing walls sitting on the foundation with no DPC wick moisture into the house.

---

## Section 8: Basement and Foundation Waterproofing

### 8.1 When Waterproofing Is Required vs Dampproofing

- **IRC 2021 §R406** (residential): dampproofing is required for foundation walls retaining earth and enclosing interior spaces below grade. **Waterproofing** (a higher standard) is required where a **high water table or other severe soil-water condition is known to exist**.
- **IBC 2021 §1805**: the same threshold logic for non-residential — dampproofing where hydrostatic pressure will not occur, waterproofing where it will.
- **BS 8102:2022** classifies by required internal environment rather than by soil condition:

| BS 8102 Grade | Internal environment | Typical house use |
|---|---|---|
| Grade 1 | Some seepage/damp tolerable | Plant room, car park |
| Grade 2 | No water penetration; damp vapour tolerable | Workshop, storage |
| Grade 3 | Dry, habitable, ventilated | Basement bedroom, home cinema, gym |

**Practical rule for houses:** if the basement will be habitable, design to **Grade 3**, and always with **two independent systems** (e.g. Type A barrier + Type C drained cavity). A single system in a habitable basement has no redundancy and no route to repair.

### 8.2 The Three Systems (BS 8102 Types)

| Type | Name | How it works | Best for | Repairability |
|---|---|---|---|---|
| **Type A** | Barrier / tanking | Membrane or coating on the positive (external) or negative (internal) face | New build with open excavation | Poor once backfilled |
| **Type B** | Structurally integral | Watertight reinforced concrete (crack-width controlled, waterstops at all joints) | Deep basements, high water table | Repairable by injection |
| **Type C** | Drained cavity | Water is admitted, collected in a cavity drain membrane, taken to a sump and pumped out | Retrofit, habitable basements | **Excellent** — maintainable |

### 8.3 Positive / Blind / Negative Side

| Approach | Where applied | When to use | Pros | Cons |
|---|---|---|---|---|
| **Positive side (exterior)** | Outer face of the wall, against the water | **New construction with open excavation — the default and best option** | Keeps water out of the structure entirely; protects concrete and rebar | Requires access; unrepairable after backfill; damaged by careless backfill |
| **Blind side (pre-applied)** | Applied to the excavation support / lagging *before* the concrete is poured against it | Zero-lot-line, shored excavations, under-slab | Works where there is no external access | Must be fully-adhered systems (HDPE/polyolefin) or water tracks between membrane and concrete |
| **Negative side (interior)** | Inner face of an existing wall | Retrofit, existing basements | Only option with no excavation | Water still enters and saturates the wall; hydrostatic pressure pushes the coating off; freeze-thaw and rebar corrosion continue |

### 8.4 Materials

**Under-slab membranes (IBC-listed):** rubberised asphalt · butyl rubber · **fully-adhered HDPE** · polyolefin composite · **PVC ≥ 6 mil (0.15 mm)**.
For **high hydrostatic head / commercial-grade** work: hot-applied rubberised asphalt at **90–125 mil (2.3–3.2 mm)**.

**Wall membranes:** self-adhered rubberised asphalt sheet (1.5 mm) · pre-applied HDPE for blind side · bentonite panels (self-healing, needs confinement) · liquid-applied polyurethane/polyurea · sheet HDPE dimpled drainage board (protection + drainage, **not** waterproofing on its own).

### 8.5 Foundation Waterproofing — Mandatory Companion Details

A membrane alone does not keep a basement dry. Every basement needs the full package:

1. **Perimeter drain (French drain / weeping tile)**: 100 mm perforated pipe, holes down, laid **at or below the underside of the slab**, in 300 mm of clean washed gravel (20–40 mm), wrapped in geotextile, falling 1:200 to a sump or gravity outfall
2. **Drainage board / dimpled membrane** on the wall face — relieves hydrostatic pressure and protects the membrane during backfill
3. **Cove/fillet at the wall-footing junction** and a **waterstop** in the construction joint (hydrophilic strip or PVC waterstop)
4. **Under-slab DPM/membrane** lapped and sealed to the wall membrane — the wall-to-slab junction is the most common basement leak point
5. **Backfill** with free-draining granular material for at least 300 mm; never backfill with the excavated clay directly against the membrane
6. **Ground surface** falling away from the building at ≥ 1:20 for 1.5 m; downpipes discharged to a drain **away** from the wall, never soaking at the plinth
7. **Sump + pump with battery/second pump** for any Type C system or any habitable basement below the water table

### 8.6 Worked Example B — Basement Selection

**Case:** 6 m × 9 m habitable basement, 2.8 m deep, Lahore, groundwater table reported at 5 m but seasonal perched water expected in the monsoon; open excavation possible on all sides.

1. Habitable → **BS 8102 Grade 3**
2. Open excavation → **positive-side (Type A)** is available and preferred
3. Water table below slab but seasonal perched water → hydrostatic pressure **possible** → per IRC R406 this is a **waterproofing**, not dampproofing, condition
4. Grade 3 needs redundancy → **combine Type A + Type C**
5. Specification:
   - Structure: 250 mm RC wall, w/c ≤ 0.45, crack width ≤ 0.2 mm, crystalline admixture, PVC waterstops at all construction joints (**Type B contribution**)
   - Positive side: 1.5 mm self-adhered rubberised asphalt sheet, fully bonded, dressed 150 mm onto the footing and lapped 150 mm to the under-slab membrane (**Type A**)
   - Protection/drainage: dimpled HDPE drainage board, geotextile-faced
   - Under-slab: 1.5 mm HDPE pre-applied membrane over 50 mm blinding, laps taped
   - Perimeter: 100 mm perforated pipe in washed gravel to a sump
   - Internal: cavity drain membrane on walls and floor, perimeter channel to a **twin-pump sump with battery backup** (**Type C**)
   - Finishes: battened/independent wall lining, never plastered directly on the cavity membrane
6. **Stamp gate:** the wall thickness, crack-width class and pump sizing are engineer's items — flag to the user, do not finalise.

---

## Section 9: Bathroom and Wet-Area Waterproofing

Bathrooms leak more houses than roofs do, because the water is present daily and the failures are hidden.

### 9.1 Standards

- **ANSI A118.10** — performance criteria for load-bearing, **bonded waterproof membranes** for thin-set tile (sheet or liquid-applied). Specify "A118.10-compliant membrane", not "waterproofing".
- **TCNA Handbook** — governs the whole assembly (method numbers: B415 for a bonded membrane shower receptor, B421 for pre-sloped foam trays, F122 for interior floors with membrane, etc.)
- **ANSI A108.1A §2.3.6** — mortar bed **≥ 1.5 in (38 mm)** thick
- **IPC** — minimum slope to drain **1/4 in per ft (1:48, ~2%)**
- **AS 3740** (Australia, widely referenced internationally) — 150 mm membrane upstand at the floor/wall junction generally, **1800 mm** up the wall in the shower zone, 150 mm above the bath lip

### 9.2 The Rules

1. **Continuous membrane through every plane change**, from the drain flange to full tile-assembly height. No seam, no lap and no field joint at any inside or outside corner — use preformed corners or reinforcing fabric.
2. **Every horizontal surface slopes to a drain** — floor, shower seat, curb top, niche shelf, window sill, threshold. A level shower seat is a designed puddle.
3. **Drain must be a bonding-flange (clamping-ring) drain**, with the membrane clamped **into** the drain — a membrane that stops next to the drain is not waterproof.
4. **Puddle flange** at every pipe penetration through the tanked area; sealant alone at a pipe penetration is not acceptable.
5. **Slope the substrate, not the membrane.** Pre-slope under the membrane in a mortar-bed system (mud bed pre-slope, membrane, mortar bed on top), or use a pre-sloped foam tray.
6. **Flood test 24 h before tiling** — plug the drain, fill to 25 mm above the highest point of the membrane, mark the level, check after 24 h and inspect the ceiling below (ASTM D5957).
7. **Movement joints** at all perimeter and plane-change tile joints (TCNA EJ171) — silicone, not grout.
8. **Never penetrate the membrane** after it is tested. Fixings for glass screens, grab rails and mixer plates must be planned before tanking, with sealed sleeves.

### 9.3 Sunken-Slab Bathroom Detail (standard IN/PK construction)

| # | Layer / step | Spec |
|---|---|---|
| 1 | Sunken RCC slab, 250–350 mm below finished floor level, cured | Cast monolithically, integral waterproofing admixture |
| 2 | Cementitious slurry key coat | 2 coats with waterproofing compound |
| 3 | **First waterproofing layer** on the sunken slab, dressed **150 mm up all four sides** | 2-component flexible cementitious or 1.5 mm liquid PU |
| 4 | Flood test #1, 24 h | Mark level, record |
| 5 | Plumbing installed; every penetration collared and sealed | Slope waste lines ≥ 1:48 |
| 6 | **Lightweight fill** — EPS blocks, aircrete blocks, or foam concrete. **Never brick-bat + sand** (holds water forever, and any leak becomes a permanent damp reservoir) | Density ≤ 600 kg/m³ |
| 7 | 40 mm RCC/screed capping laid to falls 1:48 toward the floor trap | Reinforced with mesh |
| 8 | **Second waterproofing layer** (the ANSI A118.10 bonded membrane), continuous, clamped into the drain flange, up 150 mm generally and **1800 mm in the shower zone** | Sheet or liquid |
| 9 | Flood test #2, 24 h, **inspect the ceiling below** | Mandatory hold point |
| 10 | Bonded mortar bed ≥ 38 mm / thin-set, then tile | ANSI A108.1A |
| 11 | Silicone movement joints at all corners and perimeters | Not grout |

### 9.4 Wet-Area Failure Points

| Failure point | Why it fails | Detail against it |
|---|---|---|
| Floor/wall junction | 90° corner in a membrane splits | Preformed corner or fabric-reinforced fillet |
| Drain connection | Membrane stops short of the flange | Clamping-ring drain, membrane sandwiched in |
| Shower niche | Level shelf holds water; corner seams | Slope shelf 1:50; single-piece pre-formed niche |
| Shower curb/kerb | Three exposed faces, tiled directly | Membrane over all three faces continuously, top sloped in |
| Pipe penetrations | Sealant-only, moves and cracks | Puddle flange bonded to the membrane |
| Glass screen fixings | Drilled after tanking | Pre-plan; use sealed sleeves; or channel-fix into the curb top with a membrane-safe detail |
| Door threshold / hob | Water tracks out under the tile bed | Continue the membrane 150 mm beyond the wet zone and turn up at the threshold |
| Bath/shower tray perimeter | Grouted, not sealed | Silicone with backer rod; membrane up 150 mm behind |
| Sunken fill saturated | Brick-bat fill absorbs any leak permanently | Lightweight closed-cell fill + a secondary drain point through the first membrane |

---

## Section 10: Leakage Failure Points — Ranked, and How to Detail Against Them

Industry claims data (NRCA and roofing-inspection sources) consistently ranks these. Design review should walk this list top-down.

| Rank | Failure point | Mechanism | Detailing counter-measure |
|---|---|---|---|
| **1** | **Flashing failure** at chimneys, skylights, vents, parapet/roof edges | Flashing is the discontinuity in an otherwise continuous surface; sealant-only flashings fail in 3–8 yrs | Two-part flashing: **base flashing** (bonded to membrane, ≥150 mm up) + **counter-flashing** (mechanically fastened into a chase, overlapping the base by ≥75 mm). Sealant is a secondary seal only. Preformed corners. No field seam at a corner. |
| **2** | **Inadequate slope / ponding** | Water standing >48 h fatigues bitumen, grows biofilm, magnifies UV and thermal cycling; ponding instability under deflection | Design at **1:40**, verify as-built ≥1:80; outlets at true low points; check slab deflection doesn't create low points between outlets; ASCE 7-22 ponding check |
| **3** | **Deteriorated sealant at penetrations** | Sealant has a 5–10 yr life; owners never re-apply | Never make sealant the primary barrier. Sleeve + clamp + membrane collar at every penetration. Schedule sealant renewal in the O&M manual. |
| **4** | **Improper eave/edge detail causing perimeter ponding** | Drip edge set too high, gravel stop dams water, gutter above the roof line | Drip edge/gravel stop set flush or below the membrane plane; roof falls **toward** outlets, never toward a raised edge |
| **5** | **Incorrectly lapped or under-torched seams** | Laps up-slope, short laps, cold seams | Lay low-to-high; side lap ≥100 mm, end lap ≥150 mm; visible bitumen bleed-out at every seam as the QC signal; probe every seam with a rounded tool |
| **6** | **Parapet/coping joints and copings falling outward** | Open coping joints deliver water directly into the wall core | Coping falls inward; sealed movement joints; coping DPC full width; drip grooves both faces |
| **7** | **Blocked outlets** | Leaves, bird nests, construction debris; no redundancy | Domed leaf guards; **mandatory secondary overflow** above the primary invert; maintenance schedule |
| **8** | **Substrate not cured / not primed** | Blistering, debonding, membrane never bonded at all | 14–28 day cure; moisture test <5%; slurry key coat + primer; reject green slabs |
| **9** | **Wall/roof abutment at an upper storey** | Water runs down a wall and behind the membrane upstand | Cavity tray in the wall above, ≥150 mm step, weeps at 900 mm; counter-flashing chased into the wall above the tray |
| **10** | **Thermal movement cracking at junctions** | Roof slab moves relative to parapet; rigid finish cracks | Movement joint at the roof/parapet junction; reinforced membrane strip over the joint; expansion joints in screed at 6 m grid and over all structural joints |
| **11** | **Services installed after tanking** | Solar mounts, AC stands, satellite dishes drilled through the membrane | Pre-plan all roof-mounted plant; use **ballasted** or **membrane-flashed curb** supports; never a raw fixing through a finished roof |
| **12** | **Rising damp / plinth bridging** | Ground raised after construction, render bridging DPC | 150 mm DPC height, bell-cast render stop, gravel margin |

### 10.1 The Six Universal Counter-Measures

Every counter-measure above reduces to six rules. Apply them everywhere, in every system:

1. **Continuity** — the membrane is one unbroken surface through every plane change; no field seam at any corner
2. **Redundancy** — two drainage systems (primary + overflow); two membranes in habitable basements and wet areas
3. **Mechanical termination** — every membrane edge is mechanically fixed and then sealed; sealant is never the primary barrier
4. **150 mm** — the universal upstand: parapets, thresholds, wet-area walls, DPC above ground, cavity-tray step-downs
5. **Positive slope, verified** — design 1:40, accept ≥1:80 as-built, no back-falls, low point = outlet
6. **Substrate first** — cured, dry, clean, cove-filleted, primed. More membranes fail from bad substrate prep than from bad membranes.

---

## Section 11: Critical Dimensions Cheat Sheet

| Dimension | Value | Applies to |
|---|---|---|
| Roof fall (design) | **1:40** (25 mm/m) | Flat RCC roofs |
| Roof fall (as-built minimum) | 1:80 (12.5 mm/m) | Acceptance criterion |
| Gutter fall | 1:100 – 1:200 | Eaves gutters, channels |
| Wet-area floor fall | 1:48 (1/4 in/ft) | Bathrooms, balconies |
| Membrane upstand | **≥ 150 mm** | Parapets, walls, kerbs |
| Shower wall membrane height | 1800 mm | Shower zone |
| Cove fillet | 50 × 50 mm | All horizontal/vertical junctions |
| Membrane side lap | ≥ 100 mm | Sheet systems |
| Membrane end lap | ≥ 150 mm | Sheet systems |
| Counter-flashing overlap over base flashing | ≥ 75 mm | All flashings |
| Curb height above finished roof (skylight/hatch/plant) | ≥ 150 mm (200 mm in snow zones) | Roof penetrations |
| Valley flashing width | ≥ 600 mm total (300 mm each side) | Pitched roof valleys |
| Chimney cricket trigger width | > 762 mm (30 in) | IRC R903.2.2 |
| Coping overhang | ≥ 40 mm each face | Parapet copings |
| Coping drip groove | ≥ 5 mm projection/throat | Copings, sills, bands |
| Cavity tray step-down | ≥ 150 mm | Abutments, openings |
| DPC above finished ground | ≥ 150 mm | External walls |
| DPM under slab | 0.3 mm (1200 g) PE, 150 mm laps | Ground floors |
| Under-slab membrane (IBC) | ≥ 6 mil (0.15 mm) PVC or listed equivalent | Basements |
| Hot rubberised asphalt (high head) | 90–125 mil (2.3–3.2 mm) | Plaza/podium/basement |
| Overflow scupper invert | 50 mm above primary invert, ≥50 mm below threshold/DPC | Parapeted roofs |
| Perimeter drain | 100 mm perforated, at/below slab underside, 1:200 fall | Basements |
| Ground fall away from building | ≥ 1:20 for 1.5 m (or 1:60 apron min) | All buildings |
| Screed minimum at outlet | 40 mm | Screed-to-falls |
| Mortar bed under tile | ≥ 38 mm (1.5 in) | ANSI A108.1A |
| Flood test depth / duration | 25 mm above high point / 24–48 h | All tanked areas |
| Attic ventilation | 1/150 (or 1/300 with high vents + VCL) | Cold pitched roofs |

---

## Section 12: Worked Example C — Complete House Envelope Specification

**Project:** 10 marla (≈ 250 m²) two-storey house, Lahore. Ground + first floor, accessible roof terrace with an overhead water tank and solar panels, one basement-level store (not habitable), three bathrooms stacked.

| Element | Specification | Rationale |
|---|---|---|
| Roof structure | 150 mm two-way RCC slab, max clear span 4.8 m (ℓn/33 = 145 mm → 150 mm), 25 mm cover top face | ACI 318-19 Table 8.3.1.1 |
| Roof build-up | Inverted: slurry key coat → screed to falls 1:40 (40 mm min) → 2-ply 3 mm SBS torch-on → flood test → 50 mm XPS → geotextile → 50 mm protection screed → 20 mm terrace tile | Terrace is used; membrane must be buried |
| Roof dead load allowance | 6.2 kN/m² (slab 3.6 + screed 1.9 + insulation/finish 0.7) + 2.0 kN/m² imposed | Feed to structural engineer |
| Drainage | 4 × 100 mm outlets (one per quadrant, max flow path 5.6 m) + 4 × 75 × 150 mm overflow scuppers at 50 mm above outlet inverts, discharging on the façade | ASCE 7-22 Ch.8 primary + secondary |
| Water tank plinth | Cast on a raised RCC plinth **above** the membrane with the membrane dressed 150 mm up the plinth; tank overflow piped to an outlet, never onto the roof | Never fix plant through a finished membrane |
| Solar mounts | Ballasted frames on paver pads over a sacrificial membrane strip; zero penetrations | Rank-11 failure mode |
| Parapet | 1050 mm high, inner face rendered + liquid PU full height, membrane upstand 200 mm, precast coping falling inward 1:40 with 50 mm overhang and drip grooves both faces, DPC under coping, sealed joints at 4 m; reinforcement and structural tie to the roof diaphragm per `architecture-seismic-design`, not by this table | BS 6229:2018 / NHBC 7.2 |
| Bathrooms | Sunken slab 300 mm, two-membrane system per Section 9.3, EPS fill, 1800 mm shower-zone membrane, clamping-ring drains, two flood tests | ANSI A118.10 / TCNA |
| Basement store | BS 8102 Grade 2 (not habitable): 250 mm RC wall with crystalline admixture + waterstops (Type B) + positive-side 1.5 mm self-adhered sheet + drainage board + 100 mm perimeter drain to sump | IRC R406 / BS 8102 |
| Plinth / DPC | 25 mm 1:2 cement mortar DPC with integral waterproofer + bitumen coat at 450 mm above NSL (≥150 mm above finished paving), lapped to under-slab 1200 g DPM; termite barrier coordinated at the same plinth level (Section 7.3) | Approved Doc C rule of thumb |
| External paving | Falls 1:60 away from the wall for 900 mm; 300 mm gravel margin at planted edges | Splash-back control |
| Rainwater downpipes | 4 × 100 mm uPVC, discharging to a paved channel/soakaway ≥ 1.5 m from the building | Never soak at the plinth |
| Hold points | (a) slab cure + moisture test, (b) screed falls survey, (c) roof flood test, (d) bathroom flood test #1 and #2, (e) basement membrane inspection before backfill | Non-negotiable QA gates |

**Stamp gate reminder:** slab depths, reinforcement, tank plinth loading, parapet seismic detailing and basement wall design in this table are **preliminary**. PEC-registered engineer sign-off + LDA approval required before construction.

---

## Section 13: Screed, Insulation and Thermal Coordination

| Item | Value |
|---|---|
| Screed-to-falls minimum thickness at low point | 40 mm (bonded), 65 mm (unbonded), 75 mm (floating over insulation) |
| Screed mix | 1:4 cement:sharp sand, or lightweight foam concrete (600–1200 kg/m³) where dead load is critical |
| Screed movement joints | Bay size ≤ 6 × 6 m, over all structural joints, at all upstands (isolation joint 10 mm) |
| Screed density (weight) | 20 kN/m³ (sand-cement); 6–14 kN/m³ (foam concrete) |
| XPS compressive strength for inverted roofs | ≥ 300 kPa (foot traffic), ≥ 500 kPa (paver/planter loading) |
| XPS water absorption | ≤ 0.7% by volume — **only XPS is valid in an inverted roof**; EPS and PIR absorb |
| Typical roof U-value target (hot-dry) | 0.35–0.50 W/m²K → 50–75 mm XPS over RCC |
| Typical roof U-value target (temperate/cold) | 0.13–0.18 W/m²K → 150–200 mm PIR |
| Tapered insulation as an alternative to screed | Saves 1.0–2.0 kN/m² dead load; costs more; use where slab capacity is tight |
| Thermal shock on a black membrane, Punjab summer | Surface can reach 70–80 °C — a further reason to bury or reflect-coat the membrane |

---

## Section 14: QA, Testing and Commissioning

### 14.1 Hold Points (no work proceeds past these without sign-off)

| # | Hold point | Test / evidence |
|---|---|---|
| 1 | Slab cured and dry | 14–28 days elapsed; moisture ≤ 5% (carbide/hygrometer); photo record |
| 2 | Substrate prepared | Cove fillets present at every junction; no laitance; primer applied and dry |
| 3 | Falls set | Dumpy-level/laser survey grid at 1 m centres; **no point with a back-fall**; record the levels |
| 4 | Membrane complete, before any covering | **Flood test** per ASTM D5957: plug outlets, 25 mm above the highest point, hold **24–48 h**, mark start level, inspect the soffit |
| 5 | Complex/critical roofs | **Electronic leak detection** — low-voltage vector mapping or high-voltage spark test (ASTM D7877) |
| 6 | Wet areas | Flood test on the primary membrane and again on the secondary membrane |
| 7 | Basement, before backfill | Visual inspection of full membrane, laps, terminations, corners; photograph every metre; drainage board and perimeter drain in place |
| 8 | Rainwater system | Hose test each outlet at full flow; verify the overflow discharges before any water reaches the threshold |
| 9 | Post-handover | Re-inspect after the first monsoon/heavy storm |

### 14.2 Common Test Failures and Their Meaning

| Symptom | Likely cause |
|---|---|
| Flood test drops but no visible leak below | Water tracking laterally under the membrane to a distant exit; membrane not fully bonded |
| Blisters in a torch-on membrane | Damp or uncured substrate; trapped solvent from primer; under-heated bond |
| Leak only during wind-driven rain | Parapet/coping or flashing failure, not the field membrane |
| Leak only after prolonged rain, none in short storms | Ponding-related; drainage inadequate |
| Damp on the soffit in dry weather | Condensation (cold roof, missing VCL) or plumbing, not rainwater |
| Damp band 300–900 mm above floor internally | Rising damp / bridged DPC / splash-back |
| Efflorescence on a basement wall | Water passing through the concrete — negative-side coating failing or absent positive side |

### 14.3 O&M Schedule to Hand to the Owner

- **Before and after each monsoon:** clear all outlets, gutters and scuppers; verify the overflow is unobstructed
- **Annually:** inspect all flashings, coping joints and sealants; re-seal any sealant showing adhesion loss
- **Every 5 years:** renew exposed sealants as a matter of course (they are consumables)
- **Every 5–8 years:** re-coat solar-reflective coating on exposed membranes
- **Never:** drill, fix, or set new plant on a finished roof without a membrane-flashed curb detail

---

## Section 15: FreeCAD / BIM Modelling Guidance

Use with `architecture-freecad-bim` (Site → Building → Storey hierarchy, live parametric openings via Subtractions).

### 15.1 What to Model vs What to Annotate

| Element | Model as solid? | Notes |
|---|---|---|
| RCC roof slab | **Yes** — `Arch Structure`, IfcSlab, PredefinedType ROOF | Real thickness; this is the structural datum |
| Screed to falls | **Yes**, as a separate `Part::Loft`/`Solid` between the flat top of the slab and the sloped top surface | Gives real volume for quantities and real geometry for the parapet junction |
| Waterproofing membrane | **No solid** — model as a 2–4 mm `Arch Component` face only if a detail view is needed | Modelling 3 mm layers across a whole house bloats the file for no benefit; specify in the material/annotation layer instead |
| Insulation | **Yes** where it affects dimensions (inverted roof build-up, U-value schedule) | IfcCovering or IfcPlate |
| Protection screed / tiles | Yes, as one combined `Arch Floor`-type solid | Keeps terrace level correct relative to thresholds |
| Parapet | **Yes** — `Arch Wall`, IfcWall, with the coping as a separate `Arch Component`/IfcCovering | Model the coping's inward fall; it drives the visible section. Reinforcement/thickness for seismic adequacy comes from `architecture-seismic-design`, not this skill |
| Copings, drip grooves | Groove: **annotate only** | Sub-10 mm features are detail-drawing items |
| Rainwater outlets, downpipes | **Yes** — simple cylinders, IfcFlowSegment / IfcFlowTerminal | Positions must be coordinated with the falls model |
| Overflow scuppers | **Yes** — as a Subtraction void in the parapet wall | Proves the invert level graphically |
| DPC | **Annotate** at plinth level | 25 mm layer, no geometric value |
| Sunken bathroom slab | **Yes** — model the step-down in the slab | Drives beam depths and headroom below |
| Basement membrane | Annotate; model the drainage board only if it affects excavation width | Excavation width matters for the site plan |
| Trusses | **Yes** — `Arch Structure` members or the BIM Truss tool | Model the real chord/web layout, not a solid prism |

### 15.2 Modelling the Falls (practical FreeCAD recipe)

1. Model the flat slab as an `Arch Structure` at the true structural level.
2. Sketch the roof outline on the slab top face. Create a second sketch of the same outline, placed at the high-point level.
3. For a simple two-way fall to one corner, create the screed solid with `Part → Loft` between the outline at the low point (40 mm above slab) and a point/edge at the high point — or build it as a `Part::Wedge` per quadrant for a four-way fall.
4. For a multi-zone fall (Worked Example A), create one wedge/loft solid per outlet zone, meeting at the screed valleys, then `Part → Boolean → Union`.
5. Name objects explicitly: `Roof_Slab_L2`, `Roof_Screed_Falls_Z1..Z5`, `Parapet_North`, `Coping_North`, `RWO_1..5`, `Overflow_Scupper_N1`.
6. Verify the fall by measuring: `Measure` tool from the outlet invert to the high point, divided by the plan distance, must be ≥ 1:40 as modelled.
7. Set the material on every object (`IfcMaterial`) so the quantity take-off returns screed volume separately from concrete volume.

### 15.3 Naming and Classification

| Object | IFC class | PredefinedType |
|---|---|---|
| Roof slab | IfcSlab | ROOF |
| Screed / topping | IfcCovering | FLOORING |
| Insulation | IfcCovering / IfcPlate | INSULATION |
| Membrane (if modelled) | IfcCovering | MEMBRANE |
| Parapet | IfcWall | PARAPET |
| Coping | IfcCovering | CLADDING (annotate as coping) |
| Rainwater outlet | IfcFlowTerminal | — |
| Downpipe | IfcFlowSegment | — |
| Truss | IfcMember / IfcBeam | — |
| Basement wall | IfcWall | SOLIDWALL |
| Sunken slab | IfcSlab | FLOOR |

### 15.4 Model Checks Before Presenting

- [ ] Every roof low point has an outlet **and** an overflow modelled
- [ ] Screed thickness ≥ 40 mm at every outlet and ≤ ~150 mm at the high point (or flagged for further outlet iteration if it isn't)
- [ ] Parapet height and coping fall direction visibly correct in section
- [ ] Terrace finished level is **≥ 150 mm below** any door threshold, or a channel drain + 75 mm minimum detail is modelled
- [ ] Sunken bathroom slabs modelled with the correct step and the beams below checked for headroom
- [ ] Plinth level ≥ 150 mm above finished external ground in the model, and paving falls away
- [ ] Basement excavation width includes drainage board + working space (600 mm min)
- [ ] A note is attached to the model file stating it is a planning model requiring engineer sign-off
- [ ] Parapet reinforcement/bracing has been checked against `architecture-seismic-design`, not assumed from the waterproofing dimensions alone

---

## Section 16: Standards Referenced

| Standard | Scope | Used here for |
|---|---|---|
| **ASCE/SEI 7-22 Ch.8** | Rain loads | R = 0.0098(ds+dh) kN/m²; ponding head considered in the rain-load calc; primary + secondary drainage — verify exact clause wording before citing an edition-specific requirement |
| **ASCE/SEI 7-22 Ch.7** | Snow loads | Pitched roofs in northern Pakistan |
| **ACI 318-19 Table 8.3.1.1** | Two-way slab minimum thickness | RCC roof slab depth — verify exact footnote text for grades other than 420 MPa before citing |
| **ACI 318-19 Table 24.2.2 / §24.2** | Deflection control | Skipping explicit deflection calc when min h met |
| **ACI 318-19 Table 7.3.1.1** | One-way slab min thickness | ℓ/20, ℓ/24, ℓ/28, ℓ/10 |
| **IRC 2021 §R406** | Foundation dampproofing/waterproofing (residential) | Waterproofing trigger = high water table / severe soil-water condition |
| **IBC 2021 §1805** | Foundation waterproofing/dampproofing | Under-slab membrane material list |
| **IRC R806.2** | Attic ventilation | 1/150 and 1/300 rules |
| **IRC 2021 §R903.2.1** | Kickout flashing | Diverter required where a roof edge meets a wall |
| **IRC 2021 §R903.2.2** | Chimney crickets/saddles | Required for chimneys > 30 in (762 mm) wide |
| **BS 6229:2018** | Flat roofs with continuously supported flexible coverings | 150 mm upstand; design falls vs as-built falls |
| **NHBC Standards Ch.7.2** | Flat roofs (UK warranty) | 150 mm upstand; coping DPC; cavity tray |
| **BS 8102:2022** | Protection of below-ground structures against water | Grades 1–3; Types A/B/C |
| **UK Approved Document C** | Site preparation & resistance to contaminants and moisture | DPC ≥ 150 mm above ground |
| **BS 5642 / BS 4729** | Sills and copings / special masonry units | Coping overhang, drip groove |
| **IS 3067:1988** | General design details & preparatory work for damp-proofing/waterproofing | Substrate prep, cove fillets, sequence |
| **IS 1346:1991** | Waterproofing of roofs with bitumen felts | Felt roofing laps, layer counts |
| **IS 9918:1981** | In-situ waterproofing with glass-fibre-tissue-reinforced bitumen | Alternative membrane system |
| **IS 7198:1974** | Damp-proofing using bitumen mastic | Mastic DPC |
| **ANSI A118.10** | Bonded waterproof membranes for tile | Wet-area membrane performance spec |
| **ANSI A108.1A §2.3.6** | Mortar bed thickness | ≥ 38 mm |
| **TCNA Handbook** | Tile installation methods | Wet-area assembly method numbers |
| **AS 3740** | Waterproofing of domestic wet areas | 150 mm / 1800 mm upstands |
| **IPC** | Plumbing | 1/4 in per ft slope to drain |
| **ASTM D5957** | Flood testing horizontal waterproofing | 24–48 h flood test procedure |
| **ASTM D7877** | Electronic methods for detecting membrane leaks | ELD / vector mapping |
| **TCNA EJ171** | Movement joints in tile | Perimeter and plane-change joints |
| **Building Code of Pakistan 2007 / SBC-07** | Local governing code (structural/seismic) | **Clause-level roofing/waterproofing text NOT retrieved — read the PDF before citing a clause** |
| **BCP 2021 (PEC final draft)** | Successor Pakistan code | Same caveat |

**Source PDFs to read before citing a Pakistan clause number:**
- `https://urbanunit.gov.pk/Download/publications/Files/8/2021/Pakistan%20Building%20Code%202007.pdf`
- `https://www.pec.org.pk/wp-content/uploads/2024/09/BCP2021-Final-Draft-dated-26.10.2021.pdf`
- `https://internationalaccord.org/wp-content/uploads/2023/09/Pakistan-Accord-Building-Standard-Version-1-1.pdf`

---

## Section 17: Design Review Checklist

Run this before issuing any roof/waterproofing package or presenting a FreeCAD model.

**Roof**
- [ ] Every roof area has a designed fall of ≥ 1:40 and a surveyed flow path ≤ ~6 m
- [ ] Outlet count checked against design intensity, not just rule of thumb
- [ ] Secondary overflow provided for **every** enclosed drainage zone, invert 50 mm above primary
- [ ] Ponding + rain load (ASCE 7-22 Ch.8) included in the structural load case
- [ ] Screed dead load included in the slab design
- [ ] Membrane specified by system, thickness, number of plies and standard — not just "waterproofing"
- [ ] Membrane is protected (buried or reflective-coated), not left as a wearing surface
- [ ] Cove fillets shown at every horizontal/vertical junction on the details
- [ ] 150 mm upstand shown everywhere; 75 mm variance only with a channel drain
- [ ] All roof-mounted plant on ballasted or curb-flashed supports; zero raw penetrations
- [ ] Flood test written into the specification as a hold point

**Parapets and edges**
- [ ] Coping falls inward, ≥ 40 mm overhang, drip grooves both faces
- [ ] Coping DPC full width, lapped, joints sealed as movement joints
- [ ] Cavity tray with ≥ 150 mm step and weeps at all abutments
- [ ] Counter-flashing mechanically fixed into a chase, overlapping base flashing ≥ 75 mm
- [ ] Step flashing (not a continuous strip) at every sloping-roof-to-wall junction, terminated with a kickout
- [ ] Cricket/saddle upslope of any chimney wider than 762 mm
- [ ] All curbs (skylight, hatch, plant) ≥ 150 mm above finished roof level
- [ ] Parapet reinforcement and roof-to-parapet structural tie checked against `architecture-seismic-design` — not assumed from waterproofing dimensions

**Walls and plinth**
- [ ] DPC ≥ 150 mm above finished external ground, lapped to under-slab DPM
- [ ] Render stopped above DPC with a bell-cast bead
- [ ] Paving falls away ≥ 1:60 for 900 mm; downpipes discharge away from the plinth
- [ ] Vertical DPCs at all reveals and abutments
- [ ] Termite/anti-pest barrier coordinated with the DPC at plinth level (Section 7.3), not left to a separate uncoordinated trade

**Basement**
- [ ] BS 8102 grade declared and matched to the intended use
- [ ] Two independent systems for any habitable basement
- [ ] Perimeter drain at/below slab level, in washed gravel, geotextile-wrapped, falling to a sump
- [ ] Wall-to-slab junction detail drawn, with waterstop and membrane lap
- [ ] Pre-backfill inspection written in as a hold point
- [ ] Sump pump redundancy (twin pump / battery backup) for Type C

**Wet areas**
- [ ] ANSI A118.10 membrane specified, continuous through all plane changes
- [ ] Clamping-ring drains; puddle flanges at all penetrations
- [ ] All horizontal surfaces slope to drain, including seats, curbs and niches
- [ ] 1800 mm membrane height in shower zones; 150 mm elsewhere
- [ ] Lightweight fill (not brick-bat) in sunken slabs
- [ ] Two flood tests scheduled
- [ ] Screen/rail fixings pre-planned before tanking

**Governance**
- [ ] The user has been told, in plain language, that this is a planning-stage package
- [ ] PEC-registered engineer review flagged as required
- [ ] Local authority (LDA/CDA/TMA or equivalent) approval flagged as required
- [ ] No BCP clause number cited that has not actually been read
- [ ] No ASCE/ACI/other code edition-specific "this changed from the prior edition" claim cited that has not been verified against the actual clause text
- [ ] All cost figures labelled as indicative and requiring local re-quotation
