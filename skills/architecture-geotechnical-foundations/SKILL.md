---
name: architecture-geotechnical-foundations
description: >
  Geotechnical investigation and foundation design for residential buildings in
  Pakistan and South Asia: SPT and plate-load-test interpretation, safe bearing
  capacity determination, foundation type selection decision tree (isolated,
  strip, combined, raft, pile, under-reamed), footing sizing and depth-below-grade
  rules, ACI 318-19 footing detailing, pile capacity and uplift checks, ground
  improvement options, excavation and adjacent-structure protection, differential
  settlement limits, damp-proof course and below-grade waterproofing, retaining
  walls for sloped sites, and high-water-table plus expansive (black cotton),
  collapsible and saline soil mitigation. Provides numeric tables, worked examples,
  and code citations for preliminary design and FreeCAD BIM modelling.
---

# Geotechnical Investigation & Foundation Design for Houses

Foundations are the one part of a house that cannot be corrected after the fact. Everything above grade — walls, slabs, finishes — is replaceable; a footing sized against the wrong bearing capacity, founded inside an expansive soil's active zone, or built without drainage behind a retaining wall produces cracking that no architectural remedy fixes. This skill provides the numeric backbone for preliminary residential foundation design in the Pakistan / South Asia context: how to scope and read a soil investigation, how to pick a foundation type, how to size and detail it, and how to protect it from water and swelling clay.

## Reality Check - Licensing & Liability

**This skill produces design aids and calculation guidance for planning and FreeCAD modelling ONLY.**

Every number in this file — bearing capacities, footing sizes, reinforcement, wall proportions, settlement limits — is for **preliminary sizing, feasibility studies, cost estimating, and 3D/BIM modelling**. None of it is a construction document.

1. **A licensed geotechnical investigation supersedes every table here.** Generic soil tables are orientation values. Any real project requires a site-specific investigation (boreholes + SPT + laboratory testing) by a competent geotechnical firm, and its report governs.
2. **Any design intended for the actual construction of a real, occupied building MUST be reviewed, sealed, and stamped by a licensed structural engineer** — in Pakistan, a **PEC-registered** Professional Engineer; in India an appropriately licensed/chartered structural engineer; elsewhere, the equivalent registered professional.
3. **The design MUST go through local authority plan approval before construction** — LDA (Lahore), CDA (Islamabad), SBCA (Karachi), RDA (Rawalpindi), TMA/Cantonment Board, or the relevant development authority — under their building byelaws, setback, plinth-level and structural-vetting rules.
4. **Claude / Claude must never present FreeCAD output, a bearing-capacity number, a footing schedule, or a retaining-wall section from this skill as construction-ready.** Label deliverables "PRELIMINARY — NOT FOR CONSTRUCTION — requires licensed engineer review."
5. **Say this unprompted.** If a user's language suggests they are treating the output as final (asking for a bar bending schedule to hand a contractor, asking "so I can start excavation?", asking for quantities to order steel, asking to skip the soil test to save money), stop and state the requirement for a soil report, a stamped design, and authority approval — in that message, not in a footnote.
6. **Highest-risk items where this skill must escalate to a human engineer immediately, no exceptions:** any retaining wall over ~1.2 m; any basement below the water table; any site with known expansive/black-cotton or filled/made-up ground; any slope steeper than ~1V:3H; any site in seismic Zone 3 or 4 (Quetta, Muzaffarabad, northern areas); any building over 2 storeys; any liquefaction-susceptible site.

**Code posture used throughout this skill.** Pakistan's BCP 2007 (Seismic Provisions, SP-2007) is drafted around **UBC-1997-era** load and seismic provisions and contains **no** Pakistan-specific numeric geotechnical design tables; it predates ASCE 7-22 by well over a decade. BCP 2021 (the newer, IBC-oriented draft) moves toward referencing ASCE 7 / ACI 318 **by reference**, but is itself still in draft status in most jurisdictions at the time of writing. Neither BCP edition should be read as citing ASCE 7-22 verbatim — that is a *substitution this skill makes for numeric convenience*, not a claim about what the Pakistani text itself says. Standard subcontinent practice therefore uses:

| Domain | Governing document used here |
|---|---|
| Seismic zone, site class, load combinations, lateral loads | **BCP 2007 (SP-2007, UBC-1997-based) / BCP 2021 Ch. 16 "Structural Design" (references ASCE 7 / ACI 318 / UBC)**. This skill substitutes **ASCE 7-22 Ch. 2, 11, 12** as the modern standard-of-practice numeric source, since BCP 2007 itself contains no updated tables — treat this as an engineering substitution, not a citation of BCP text |
| Foundation general requirements, min depth, settlement criteria | **IS 1904:2000** |
| Bearing capacity calculation methods | **IS 6403:1981**, Terzaghi (1943), Meyerhof (1963), Skempton (1951) |
| Plate load test procedure | **IS 1888:1982** |
| Standard penetration test | **IS 2131:1981 / ASTM D1586** |
| Footing concrete design (shear, flexure, cover, durability) | **ACI 318-19 Ch. 13, 22; Tables 19.3.1.1, 19.3.2.1, 20.5.1.3** |
| Under-reamed piles in expansive soil | **IS 2911 (Part 3):1980** |
| Damp-proof course | **IS 3067:1988**, BS 8215:1991 |
| Expansive soil classification | **IS 2720 (Part 40)** free swell index, IS 1498 classification |
| Comparative frost-depth reference only (US) | **IRC 2021 R403.1.4, R403.3** — *not* applicable to Pakistan lowlands |

---

## Section 0: Foundation Design Workflow (order of operations)

Run these in order. Skipping a step — almost always step 1 or step 3 — is what produces the failures catalogued in §10.2.

```
1. GROUND MODEL
   Soil report (boreholes + SPT + lab) → strata log, water table, cu / φ / γ,
   PI + free swell index, sulphate & chloride.
   No report? → every downstream number is PRESUMPTIVE. Say so in the output.       §1, §2

2. SCREEN FOR PROBLEM GROUND                                                        §8
   Expansive? Collapsible loess? Uncontrolled fill? Liquefiable? Saline?
   Any YES → problem-soil branch governs; ignore the "nice" SBC number.

3. LOADS
   Service (ASD) loads for soil bearing.  Factored (LRFD) loads for concrete.
   Two separate load sets. Never interchange them.                     ASCE 7-22 §2.3/§2.4

4. SBC
   Lower of: SPT correlation (Terzaghi–Peck vs Meyerhof), Terzaghi/Skempton
   general-shear ÷ FS 2.5–3.0, plate load test ÷ FS, presumptive table.
   Apply water-table correction Cw.                                          §1.4–1.6, §2

5. FOUNDATION TYPE                                                                  §3
   Run the decision tree. Output: type + founding depth Df.

6. SIZE & DETAIL
   Plan area from service load ÷ SBC → punching shear → one-way shear → flexure
   → As,min → development length → cover & durability class.                        §4

7. SETTLEMENT CHECK
   Total ≤ 25 mm target, angular distortion ≤ 1/500. If it fails, go back to 5.      §5

8. WATER & MOVEMENT PROTECTION
   DPC, below-grade waterproofing, perimeter drain, plinth beams,
   expansive-soil voids/aprons.                                                 §6, §8

9. SLOPED SITES
   Retaining walls: overturning, sliding (usually governs), bearing, drainage.       §7

10. LABEL & HAND OFF
    "PRELIMINARY — NOT FOR CONSTRUCTION"; assemble the engineer handoff pack.  §10, §12
```

---

## Section 1: Site Investigation Programme

### 1.1 Scope of Investigation by Project Size

| Plot / building | Minimum boreholes | Depth below founding level | Typical field programme |
|---|---|---|---|
| 5 marla – 10 marla (125–250 m²), G+1 | 1 borehole (2 preferred) | 6 m or 1.5×B, whichever greater | SPT @ 1.5 m intervals + 2 disturbed + 1 UDS |
| 1 kanal (505 m²), G+1 / G+2 | 2 boreholes | 8–10 m | SPT @ 1.5 m + UDS in every cohesive stratum |
| 2 kanal+ / farmhouse, spread plan | 3–4 boreholes (grid, 15–25 m apart) | 10 m, or 1.5×B below raft | SPT + 1 plate load test at founding level |
| Any site with basement | ≥2 boreholes | 2× basement depth, min 10 m | + standpipe piezometer for water table |
| Sloped / hillside site | ≥3 (crest, mid, toe) | to competent stratum or 2× cut height | + slope stability profile, rock coring if refusal |

**Borehole spacing across a foundation footprint: 3–5 m for erratic ground, 15–25 m for uniform alluvium.** Minimum depth rule: go to **1.5 × footing width (B)** below founding level for isolated footings, **1.5 × raft width** for rafts (often reduced to a practical 10–15 m), or to refusal/rock, whichever is shallower. Rationale: the 2:1 stress-distribution method shows the induced vertical stress under a square footing falls to ~10% of the applied pressure at ≈2B depth and ~20% at ≈1.5B — below that, settlement contribution is negligible for residential loads.

### 1.2 Standard Penetration Test (SPT) — ASTM D1586 / IS 2131

Procedure: 63.5 kg hammer, 760 mm free fall, split-spoon sampler driven 450 mm in three 150 mm increments. **N = blows for the second + third increments** (the first 150 mm is seating and is discarded). Refusal at 50 blows for any 150 mm increment.

**Corrections — apply in this order:**

```
N60   = N_field × (CE · CB · CS · CR) / 0.60      (energy/equipment correction)
(N1)60 = CN × N60 ,  CN = √(95.8 / σ'v0[kPa])  (Liao & Whitman), capped at 1.7
```

| Correction | Typical value (South Asia practice) |
|---|---|
| CE — hammer energy ratio | 0.45–0.55 donut hammer w/ rope-and-pulley (common local rigs); 0.7–0.9 automatic trip |
| CB — borehole diameter | 1.00 (65–115 mm); 1.05 (150 mm); 1.15 (200 mm) |
| CS — sampler | 1.00 standard; 1.10–1.30 sampler without liner |
| CR — rod length | 0.75 (<4 m); 0.85 (4–6 m); 0.95 (6–10 m); 1.00 (>10 m) |
| Dilatancy (fine saturated sand/silt, N>15) | N_corr = 15 + 0.5(N − 15) — Terzaghi & Peck |

**Warning for local practice:** many Pakistani drilling contractors report raw field N with rope-and-pulley hammers at ~50% energy. If the report does not state the energy ratio, assume CE ≈ 0.5 and treat the reported N as *optimistic*; ask the geotech firm for the hammer type in writing.

### 1.3 Interpreting N — Consistency, Strength, Bearing

**Cohesionless soils (sand/gravel):**

| (N1)60 | Relative density | Dr (%) | φ' (°) | Character |
|---|---|---|---|---|
| 0–4 | Very loose | <15 | <28 | Unsuitable for shallow footings — improve, raft, or pile |
| 4–10 | Loose | 15–35 | 28–30 | Marginal; check settlement, consider compaction |
| 10–30 | Medium dense | 35–65 | 30–36 | Normal isolated footings OK |
| 30–50 | Dense | 65–85 | 36–41 | Good — high SBC |
| >50 | Very dense | >85 | >41 | Excellent |

**Cohesive soils (clay/silt):**

| N60 | Consistency | cu (kPa) | Field test | Notes |
|---|---|---|---|---|
| 0–2 | Very soft | <12.5 | Extrudes between fingers | Never found shallow footings here |
| 2–4 | Soft | 12.5–25 | Easily moulded | Raft or piles |
| 4–8 | Medium stiff | 25–50 | Moulded with strong pressure | Check consolidation settlement |
| 8–15 | Stiff | 50–100 | Indented by thumb | Typical Punjab alluvium at 1.5–3 m |
| 15–30 | Very stiff | 100–200 | Indented by thumbnail | Good bearing |
| >30 | Hard | >200 | Difficult to indent | Excellent, but check for desiccated expansive crust |

Correlation: **cu ≈ 4.5 N60 to 6 N60 kPa** (Stroud, 1974) — use **cu = 5 N60** for insensitive clays as a default, but *never* rely on SPT alone in clay; require unconfined compression (UCS) or triaxial results on undisturbed samples.

### 1.4 Bearing Capacity from SPT — Two Correlations, Take the Lower

For **shallow footings on sand**, net allowable bearing pressure limited to 25 mm settlement:

```
Terzaghi & Peck (1948):
   B ≤ 1.2 m :  qa (kPa) = 8 · N
   B > 1.2 m :  qa (kPa) = 5.3 · N · [(B + 0.3)/B]²

Meyerhof (1956/1963):
   B ≤ 1.2 m :  qa (kPa) = 12 · N
   B > 1.2 m :  qa (kPa) =  8 · N · [(B + 0.3)/B]²

Water-table correction Cw:  qa,corrected = Cw · qa
   Cw = 0.5   water table at founding level
   Cw = 1.0   water table at or below depth (Df + B)
   interpolate linearly between
For settlement other than 25 mm:  qa,S = qa,25 × (S / 25)
```

**Rule: compute both, adopt the lower value, then check it against the plate load test and the general shear equation.** The literature disagrees on which correlation is conservative in which soil (Meyerhof's settlement equation gives ~50% higher allowable pressure than Terzaghi–Peck for the same N, while Meyerhof's *ultimate* bearing factors with depth/shape/inclination factors often give lower ultimate capacity than Terzaghi's for clays and silts). Do not arbitrate — take the minimum of the methods you ran, and state which method governed in the output.

### 1.5 Ultimate Bearing Capacity — Terzaghi (general shear)

```
Strip   :  qu = c·Nc + q·Nq + 0.5·γ·B·Nγ
Square  :  qu = 1.3·c·Nc + q·Nq + 0.4·γ·B·Nγ
Circular:  qu = 1.3·c·Nc + q·Nq + 0.3·γ·B·Nγ
   where q = γ·Df (surcharge at founding level)
q_net,ultimate = qu − γ·Df
SBC = q_net,ultimate / FS  + γ·Df       (FS = 2.5–3.0 for residential)
```

**Terzaghi bearing capacity factors:**

| φ (°) | Nc | Nq | Nγ |
|---|---|---|---|
| 0 | 5.7 | 1.0 | 0.0 |
| 5 | 7.3 | 1.6 | 0.5 |
| 10 | 9.6 | 2.7 | 1.2 |
| 15 | 12.9 | 4.4 | 2.5 |
| 20 | 17.7 | 7.4 | 5.0 |
| 25 | 25.1 | 12.7 | 9.7 |
| 30 | 37.2 | 22.5 | 19.7 |
| 35 | 57.8 | 41.4 | 42.4 |
| 40 | 95.7 | 81.3 | 100.4 |

For **saturated clay, φ = 0 (undrained)**, use Skempton: `q_net,u = cu · Nc`, with Nc = 6.2 for a square/circular footing at Df/B = 0, rising to 7.5 at Df/B = 1 and capped at 9.0 for Df/B ≥ 4. Strip footing: Nc = 5.14 at surface, capped at 7.5.

**Local shear (loose sand, N < 10, or soft clay):** substitute `c* = (2/3)c` and `tan φ* = (2/3) tan φ` and re-enter the table.

### 1.6 Plate Load Test — IS 1888:1982

| Parameter | Specification |
|---|---|
| Plate | Rigid mild-steel, 25 mm thick, square 300 / 450 / 600 / 750 mm (or circular equivalent) |
| Test pit | Width ≥ 5 × plate width, floor at the proposed founding level |
| Seating load | ~70 kPa (0.7 kg/cm²) applied and released before the test proper |
| Load increments | 1 kg/cm² (≈100 kPa) **or** 1/5 of estimated ultimate bearing capacity, whichever is *less* |
| Settlement reading | 2 (or 4) dial gauges, 0.02 mm least count, at 1, 2.25, 4, 6.25, 9, 16, 25 min then hourly |
| Increment held until | Settlement rate < 0.02 mm/min, or 60 min, whichever earlier |
| Terminate at | 25 mm settlement, or the clear "break" (rapid settlement) point, or 1.5× estimated design pressure |
| Factor of safety | **FS = 2.0–3.0; use 2.5–3.0 for residential** |

**Reading the curve:** ultimate bearing capacity = the pressure at the sharp break/knee of the load–settlement plot (dense sand/stiff clay show a clear break; loose sand/soft clay do not — then take the pressure at settlement = 10–20% of plate width, or use the log–log double-tangent intersection).

**Critical: settlement must be scaled from plate size to real footing size.** A 300 mm plate massively under-predicts the settlement of a 1.8 m footing at the same pressure, because the stressed soil volume scales with footing width.

```
Sand :  Sf = Sp · [ 2·Bf / (Bf + Bp) ]²
Clay :  Sf = Sp · ( Bf / Bp )

Bearing capacity scaling:
Sand (φ governs) :  qu,f = qu,p · (Bf / Bp)
Clay (c governs) :  qu,f = qu,p            (independent of width)
```

**Worked example — plate to footing.** 600 mm plate, ultimate pressure at break = 450 kPa, settlement at the design pressure of 150 kPa = 4.0 mm. Design footing 1.8 m square on medium dense sand.
- SBC from plate = 450 / 3.0 = **150 kPa** (plate scale) → scale to footing in sand: qu,f = 450 × (1.8/0.6) = 1350 kPa; but width scaling of ultimate capacity is unreliable for a shallow test pit — **settlement, not shear, governs residential footings on sand**, so the settlement check controls.
- Settlement of footing: Sf = 4.0 × [2 × 1.8 / (1.8 + 0.6)]² = 4.0 × (3.6/2.4)² = 4.0 × 2.25 = **9.0 mm** at 150 kPa. Acceptable (< 25 mm). Adopt SBC = 150 kPa.

**Limitation to always state:** the plate stresses only ~2× plate width (≈1.2 m) of soil. A weak stratum 3 m down is invisible to the plate test. **A plate load test never replaces boreholes — it supplements them.**

### 1.7 Laboratory Tests to Demand in the Report

| Test | Standard | Why it matters for a house |
|---|---|---|
| Grain size / hydrometer | IS 2720 Pt 4 | USCS/IS 1498 classification; liquefaction screening |
| Atterberg limits (LL, PL, PI) | IS 2720 Pt 5 | Expansive-soil screening (PI), consolidation correlation |
| Natural moisture content, bulk & dry density | IS 2720 Pt 2 / 29 | γ for bearing & earth-pressure calcs |
| Unconfined compression / UU triaxial | IS 2720 Pt 10 / 11 | cu for clay bearing capacity — non-negotiable in clay |
| Consolidation (oedometer) — Cc, e0, pc | IS 2720 Pt 15 | Long-term settlement in normally consolidated clay |
| Free swell index / swell pressure | IS 2720 Pt 40 | Black-cotton / expansive soil identification |
| Chemical: SO₄²⁻, Cl⁻, pH of soil & groundwater | IS 2720 Pt 27 | ACI 318-19 sulphate exposure class → cement type & cover |

**Never accept a soil report for a Pakistani coastal or interior-Sindh site that omits sulphate and chloride content.** Saline groundwater destroys ordinary Portland concrete footings.

---

## Section 2: Preliminary Safe Bearing Capacity Reference Table

**Orientation values only — widely circulated as "IS 1904 presumptive values". These are for feasibility sketches and preliminary FreeCAD massing. A site investigation supersedes them absolutely.**

| Stratum | Presumptive SBC (kN/m²) | Notes |
|---|---|---|
| Hard rock (granite, trap, diorite) — no laminations | 3240 | Cap by concrete/masonry capacity, not soil |
| Laminated / foliated rock (limestone, sandstone, schist) | 880–1620 | Karachi limestone often in this band |
| Residual deposit of shattered rock, hard shale | 440–880 | Murree formation (Islamabad/Potohar) |
| Soft rock, weathered shale | 440 | Check slaking on wetting |
| Gravel / sand-gravel, compact | 440 | |
| Coarse sand, compact and dry | 440 | |
| Medium sand, compact and dry | 245 | |
| Fine sand, silt (dry lumps easily pulverised) | 150 | |
| Loose gravel or sand-gravel mixture | 245 | |
| Loose coarse to medium sand, dry | 245 | |
| **Loose fine sand, dry** | **100** | Typical marginal condition |
| Fine sand, loose and saturated | 100 | Apply water-table reduction |
| **Soft shale, hard/stiff clay in deep bed, dry** | **440** | |
| Medium clay, readily indented with thumb | 245 | |
| Moist clay & sand-clay mixture, squeezable | 150 | Common Punjab alluvium |
| **Soft clay** | **100** | Marginal — raft territory |
| **Very soft clay (extrudes between fingers)** | **50** | Unsuitable for shallow footings |
| **Black cotton / expansive soil, ~50% saturated, dry state** | **130–160** | **Bearing is NOT the problem — swell is. See §8** |
| Black cotton soil, wet / seasonally saturated | 50–100 | Plus heave; do not found shallow |
| Fill / made-up ground, uncompacted | **Not to be used** | Remove, or bypass with piles |

**Reduction rules to apply to any presumptive value:**
- **Water table at founding level:** multiply by 0.5 (submerged unit weight roughly halves the γ·B·Nγ term). Interpolate to 1.0 when the water table is at depth ≥ Df + B.
- **Sloping ground:** reduce for the reduced passive wedge; require a slope-stability check for slopes steeper than 1V:3H.
- **Eccentric loading:** use effective width B' = B − 2e (Meyerhof) rather than reducing the SBC.
- **Seismic (BCP Zone 2B and above):** a 25–33% increase in allowable bearing pressure is conventionally permitted for transient seismic/wind load combinations — but **only** where the geotechnical report explicitly allows it and never in liquefiable or sensitive clay.

---

## Section 3: Foundation Type Selection Decision Tree

### 3.1 The Decision Tree

```
START: You have SBC (kPa), column/wall service loads (kN), water table depth,
       soil type, and expansive-soil screening (PI, free swell index).

Q1. Is the soil expansive? (Free swell index > 35, or PI > 35, or known black cotton)
    YES → go to EXPANSIVE BRANCH (§8.2). Shallow spread footings inside the
          active zone are FORBIDDEN regardless of how good the SBC looks.
    NO  → Q2

Q2. Is there uncontrolled fill, organic soil, or a soft layer within 2B below
    founding level?
    YES → remove & replace with engineered fill (if <1.5 m deep) → recheck,
          OR bypass with piles to competent stratum.
    NO  → Q3

Q3. Is the superstructure a load-bearing masonry wall system (9" / 13.5" brick),
    which is the default for Pakistani residential construction?
    YES → STRIP / CONTINUOUS FOOTING (§3.3) — unless SBC < 75 kPa → RAFT
    NO (RC frame with columns) → Q4

Q4. Compute total required footing area:
        A_req,total = Σ(1.1 × service column load) / SBC
    Express as a percentage of the building footprint.
    A_req,total > ~50% of footprint  → RAFT / MAT (§3.5)
    A_req,total ≤ ~50%               → Q5

Q5. Would adjacent isolated footings overlap, or is a column on/near the
    property line where a symmetric footing cannot be built?
    YES → COMBINED or STRAP (cantilever) FOOTING (§3.4)
    NO  → Q6

Q6. Is SBC ≥ 100 kPa AND water table below (Df + B) AND settlement check passes?
    YES → ISOLATED / SPREAD PAD FOOTING (§3.2)  ← cheapest, default for
          Pakistani G+1/G+2 houses on decent ground
    NO  → Q7

Q7. Is competent bearing stratum reachable at ≤ 3 m by deepening the footing?
    YES → deepen isolated footings (check excavation shoring & economics vs raft)
    NO  → RAFT if the weak layer is shallow and uniform;
          PILES if the weak layer is thick or the water table is high (§3.6)
```

### 3.2 Isolated / Spread Pad Footing

| Attribute | Value |
|---|---|
| Use when | RC frame, single column, SBC ≥ 100 kPa, columns ≥ ~3 m apart, 1–3 storeys |
| Typical plan size (residential) | 900 × 900 mm to 2500 × 2500 mm |
| Typical thickness | 300–600 mm (min effective depth to bottom bars 150 mm — ACI 318-19 §13.3.1.2) |
| Typical Df | 1.0–1.5 m (IS 1904 absolute minimum 500 mm) |
| Concrete | M20–M25 (f'c 20–25 MPa); PCC blinding 75–100 mm of 1:4:8 |
| Reinforcement | T12–T16 @ 150–250 mm c/c both ways, Fe500 / Grade 420 |
| Cost band (Pakistan, 2026 order-of-magnitude) | Lowest of all types per m² of building — baseline 1.0× |
| Fails when | Soft/variable soil (differential settlement), high water table (dewatering cost), overlapping footings |

**Rule-of-thumb widely used in Pakistan for a G+1, 9" brick + RC column hybrid on sand/gravel with SBC 150–200 kPa: 1.2 × 1.2 × 1.2 m (4 ft cube) footing, M20, T10 @ 150 mm c/c, Fe500.** Treat this as a *sanity benchmark only*. If your calculation lands wildly outside it, re-check your loads before trusting the calc; if your calculation lands inside it, you still need the soil report.

### 3.3 Strip / Continuous Footing

| Attribute | Value |
|---|---|
| Use when | Load-bearing masonry walls (the dominant Pakistani residential system), uniform soil, moderate SBC |
| Width | `B = wall service load per metre (kN/m) × 1.1 / SBC (kPa)` — typically 600–1200 mm for a house |
| Projection beyond wall face | ≤ footing thickness for plain concrete (45° load spread); reinforce if greater |
| Thickness | 200–450 mm (RC); 300–600 mm (plain concrete / brick stepped footing) |
| Traditional brick stepped footing | Each step 1 brick (≈115 mm) offset per 1–2 courses; total spread ≤ 2× wall thickness; acceptable only for single-storey on SBC ≥ 150 kPa |
| Reinforcement | Transverse T10–T12 @ 150–200 mm, longitudinal T10 @ 200 mm (distribution + continuity) |
| Advantage | Bridges local soft spots; naturally ties the plan together |

**Worked example.** 9" (230 mm) brick wall, G+1, service wall load = 95 kN/m (walls + slabs + finishes + live). SBC = 130 kPa. B = 1.1 × 95 / 130 = 0.80 m → **adopt 850 mm wide × 300 mm thick RC strip at Df = 1.2 m**, projection each side = (850 − 230)/2 = 310 mm > 300 mm thickness → reinforce transversely (T12 @ 150 c/c) rather than relying on plain-concrete load spread.

### 3.4 Combined & Strap Footings

- **Combined (rectangular / trapezoidal):** two or more columns on one footing, used when pads would overlap (columns < ~1.5×(B₁+B₂)/2 apart) or when one column sits on a property line. Proportion the footing so its **centroid coincides with the resultant of the column loads** — this keeps soil pressure uniform. Trapezoidal shape is used when the property-line column is heavier and length is restricted.
- **Strap / cantilever footing:** two separate pads connected by a stiff strap beam that transfers moment from the eccentric (boundary) pad to the interior pad. Use when the columns are far apart (> ~6 m) and a combined footing would be uneconomically long. Strap beam is designed for shear and moment only — it must **not** bear on the soil (cast on a compressible layer / void former beneath it).
- Very common in Pakistani plots because side walls sit exactly on the plot boundary with zero setback.

### 3.5 Raft / Mat Foundation

| Trigger for a raft | Threshold |
|---|---|
| Low bearing capacity | SBC < 75–100 kPa |
| Isolated footing area | > ~50% of the building footprint |
| Soil variability | Loose fill, pockets of soft clay, erratic strata |
| Water table | At or above founding level (raft doubles as a water-resisting slab) |
| Differential settlement risk | High — raft averages settlement across the whole plan |
| Buoyancy / basement | Basement below water table (check uplift: W_building ≥ 1.2 × uplift) |

**Types and residential thickness guide:**

| Raft type | Typical thickness | Use |
|---|---|---|
| Flat plate raft | 300–600 mm (houses); ≈ span/12 for column loads | Uniform light column loads |
| Flat plate with pedestals/thickened panels | 300 mm + 600–800 mm local | Punching shear at heavier columns |
| Beam-and-slab (ribbed) raft | 200–250 mm slab + 450–750 mm deep beams | **Most economical for Pakistani houses on soft/expansive soil** — beams give stiffness cheaply |
| Cellular / box raft | Two slabs + walls, 1.0–2.0 m overall | Very soft soil, heavy structure — rare for houses |

Net bearing pressure under a raft = `(Σ loads / raft area) − γ·Df` — the excavated soil weight is a genuine credit ("floating foundation"). For a 1.5 m deep raft in soil of γ = 18 kN/m³, the credit is 27 kPa, which on marginal ground can be the difference between raft and piles.

**Rigidity check (IS 2950 / conventional method applies when the raft is "rigid"):**
`λ = ⁴√(Ks·B / (4·Ec·I))` — if column spacing < 1.75/λ, the conventional rigid method is acceptable; otherwise use a flexible/elastic-foundation (Winkler spring) analysis. Modulus of subgrade reaction ks: soft clay 12–25 MN/m³, medium clay 25–50, stiff clay 50–100, loose sand 8–25, medium sand 25–125, dense sand 125–250 MN/m³. **ks is footing-size dependent — never take a plate-test ks straight into a raft model without the width correction.**

**Worked example — is a raft justified?** 1-kanal G+1 house, footprint 18.0 × 12.0 m = 216 m², 14 columns, Σ service column loads = 4,200 kN, SBC = 70 kPa (soft clay), Df = 1.2 m, γ = 18 kN/m³.

```
Isolated-footing route:  A_req,total = 1.1 × 4200 / 70 = 66.0 m²
                         66.0 / 216 = 30.6% of footprint  → under the 50% trigger,
                         BUT the largest column (450 kN) needs 1.1×450/70 = 7.07 m²
                         → 2.66 m square footing: over the practical 2.5 m residential
                         limit, and SBC < 75 kPa. → raft indicated.

Raft route (gross):      q = 4200 / 216 = 19.4 kPa  (before raft self-weight)
Raft self-weight (400 mm avg incl. beams, 24 kN/m³) = 9.6 kPa → q_gross = 29.0 kPa
Excavation credit:       γ·Df = 18 × 1.2 = 21.6 kPa
q_net = 29.0 − 21.6 = 7.4 kPa  ≪ 70 kPa   ✓ enormous margin on bearing
```

The bearing check on a house raft is almost always trivially satisfied — **settlement and raft stiffness govern, not bearing.** Adopt a beam-and-slab raft: 200 mm slab + 450 × 250 mm downstand beams under every column line at ~3.5 m centres, and check differential settlement across the plan against 1/500 (§5).

### 3.6 Pile Foundations

| Use when | Detail |
|---|---|
| Weak soil to significant depth | Bypass to competent stratum |
| High water table + heavy load | Bored cast-in-situ with casing/bentonite |
| Expansive soil | **Under-reamed piles anchored below the active zone** — the subcontinent standard |
| Fill / made-up ground | Socket through it |
| Sloped sites, scour, or flood-prone plots | Depth gives lateral & scour resistance |

**Residential pile options in Pakistan/India:**

| Type | Diameter | Typical safe load | Notes |
|---|---|---|---|
| Under-reamed bored pile (IS 2911 Pt 3), single bulb | 250–375 mm stem, bulb = 2.0–2.5 × stem | ~80–200 kN | Standard black-cotton-soil solution |
| Under-reamed, double bulb | 300–375 mm | ~150–300 kN | Bulb spacing ≥ 1.5 × bulb dia |
| Bored cast-in-situ | 450–600 mm | 300–800 kN | Needs a rig; overkill for most houses |
| Driven precast / micropile | 150–300 mm | 100–400 kN | Vibration issues in dense urban plots |

Under-reamed pile rules (IS 2911 Part 3): **minimum length 3.5 m** in expansive soil; the top bulb at least **1.5 m below ground level** and always **below the active zone**; centre-to-centre spacing ≥ 2 × bulb diameter; piles must be tied by a **capping/grade beam** with a **75–100 mm void beneath** it (§8.2). Safe-load values from the IS 2911(Pt 3) tables are indicative only — confirm by an initial load test on at least one pile (routine test on 0.5–2% of production piles, per IS 2911 Part 4).

**Pile capacity — static formula (use for preliminary sizing only; confirm by load test):**

```
Qu = Qb + Qs = qb·Ab + Σ(fs,i · As,i)

Cohesive (α-method):  qb = Nc·cu = 9·cu (deep, Nc = 9)
                      fs = α·cu    α = 1.0 (cu ≤ 25 kPa), 0.5 (cu ≈ 60 kPa),
                                   0.4–0.45 (cu ≥ 100 kPa)   [IS 2911 / API]
Cohesionless (β-method): qb = σ'v·Nq (cap ≈ 11 MPa), fs = β·σ'v, β = K·tanδ ≈ 0.27–0.50
Safe load  Q_safe = Qu / FS ,  FS = 2.5 (with load test) to 3.0 (without)
Ignore shaft friction over: the full active zone in expansive soil, any fill,
and ~2 bulb diameters immediately above an under-ream.
```

**Worked example — under-reamed pile in black cotton soil.** Stem Ds = 300 mm, single bulb Db = 750 mm (2.5 × stem), pile length 5.0 m, active zone 3.0 m, cu = 60 kPa below the active zone, α = 0.5.

```
Ab (bulb)  = π/4 × 0.75²  = 0.4418 m²
Qb         = 9 × 60 × 0.4418                       = 238.6 kN
Shaft length counted = 5.0 − 3.0 (active zone) − 1.5 (2×Db above bulb) = 0.5 m
Qs         = 0.5 × 60 × π × 0.30 × 0.5             =  14.1 kN
Qu         = 252.7 kN  →  Q_safe = 252.7 / 2.5     ≈ 101 kN per pile   ✓ (in the 80–200 kN band)

UPLIFT CHECK (the check people forget — swelling soil grips the stem and pulls it up):
Uplift shear in the active zone, τ ≈ 40 kPa (expansive clay, wetted):
   U = 40 × π × 0.30 × 3.0                         = 113.1 kN  (upward)
Resistance:
   Bulb anchorage  = (π/4)(0.75² − 0.30²) × 9 × 60 = 200.4 kN
   Shaft below AZ                                   =  14.1 kN
   Pile self-weight ≈ 0.0707 × 5.0 × 24            =   8.5 kN
   Σ resisting                                      = 223.0 kN
FS_uplift = 223.0 / 113.1 = 1.97   ✓ (≥ 1.5 required; ≥ 2.0 preferred)
Plus: the house dead load on the pile adds resistance — but design uplift for the
CONSTRUCTION STAGE too, when the pile is in the ground and the house is not yet on it.
```

Reinforce the full length of any pile in expansive soil (minimum 0.4% steel, 4–6 T10/T12 + T6 spirals @ 150–250 mm) — the stem goes into **tension** under uplift, which plain concrete cannot take.

### 3.7 Ground Improvement — When to Fix the Soil Instead of the Foundation

| Technique | Applicable to | Depth range | Effect | Residential economics |
|---|---|---|---|---|
| Over-excavate & replace with engineered fill (sand / moorum / crushed stone, 95% MDD in 200–300 mm layers) | Shallow soft clay, shallow expansive layer, uncontrolled fill | ≤ 1.5–2.0 m | SBC to ~150–200 kPa; removes active-zone clay | ★ Cheapest fix for a small house; the default in Pakistan |
| Surface compaction / proof-rolling | Loose sandy fill, backfilled plots | ≤ 0.6 m | Modest density gain | Cheap, limited benefit |
| Dynamic compaction | Loose granular fill, large plots | 3–8 m | Densifies, reduces liquefaction risk | Not viable on a house plot — vibration + plant cost |
| Stone / granular columns (vibro-replacement) | Soft clay, loose silty sand, liquefiable ground | 5–15 m | SBC 1.5–2.5×; drainage path; liquefaction mitigation | Only for large plots / multiple units |
| Lime stabilisation (4–8% hydrated lime) | Expansive clay | 0.5–1.0 m | Drops PI and swell substantially | Viable; **mandatory sulphate check** — lime + sulphate → ettringite heave |
| Cement / RBI-type stabilisation | Silty and sandy subgrades | 0.3–0.6 m | Strength + moisture resistance | Viable for plinth fill and aprons |
| Geogrid / geotextile-reinforced granular mattress | Soft clay under a raft | 0.5–1.0 m | Spreads load, reduces differential settlement | Good pairing with a ribbed raft |
| Preloading / surcharge with wick drains | Thick normally-consolidated clay | 5–20 m | Pre-consolidates | Timescale (3–12 months) rules it out for houses |

**Decision rule:** if the problem layer is **shallower than ~1.5 m and thinner than the excavation you were going to do anyway**, remove and replace — it is almost always cheaper than upgrading the foundation type. If the problem layer is thick, deep, or below the water table, change the foundation (raft or piles), not the soil.

### 3.8 Selection Summary Matrix

| Condition | Isolated | Strip | Combined | Raft | Pile |
|---|---|---|---|---|---|
| SBC > 200 kPa, RC frame | ★ Best | – | if overlap | Overkill | No |
| SBC 100–200 kPa, RC frame | ★ Best | – | if overlap | If plan slender | No |
| SBC 100–200 kPa, masonry walls | – | ★ Best | – | – | No |
| SBC 75–100 kPa | Marginal | Marginal | – | ★ Best | If deep soft layer |
| SBC < 75 kPa | No | No | No | ★ (ribbed) | ★ if soft is thick |
| Water table at founding level | Poor | Poor | Poor | ★ (waterproofed) | ★ |
| Expansive / black cotton | **No** | **No** | **No** | ★ ribbed raft (small houses) | ★★ under-reamed (preferred) |
| Uncontrolled fill > 1.5 m | No | No | No | No | ★ Only option |
| Sloped / hillside | Stepped only | Stepped | – | If benched | ★ |

---

## Section 4: Footing Sizing, Depth & Detailing

### 4.1 Depth of Foundation Below Grade

| Rule | Value | Source |
|---|---|---|
| Absolute code minimum below finished ground level | **500 mm** | IS 1904:2000 |
| Practical residential design depth (Punjab/Sindh plains) | **1.0–1.5 m** | Standard practice — gets below the seasonal moisture/temperature variation zone and topsoil disturbance |
| Below topsoil/organic layer | Always fully below | IS 1904 |
| Below any adjacent service trench, sewer, or septic tank invert | 45° load-spread rule; keep footing base below a 1V:2H line from the trench bottom | IS 1904 |
| Adjacent to an existing building | New footing base ≥ existing footing base; if deeper, underpin or step at ≤ 1V:2H | IS 1904 |
| Expansive / black cotton soil | Below the **active zone**: **1.5–3.5 m** (up to 4.5 m in severe cases) | §8 |
| Frost — Pakistan lowlands | **Not applicable** (no meaningful frost penetration below ~1,000 m elevation) | — |
| Frost — northern Pakistan (Murree, Kalam, Skardu, Gilgit, Naran, AJK highlands) | Footing base ≥ 150 mm below the local frost line; frost penetration typically **0.3–0.9 m** at 1,800–3,000 m | Local practice |
| Frost — US comparative reference only | Footing depth = local frost line **+ 150 mm (6 in) minimum bearing**; or a Frost-Protected Shallow Foundation at 300–400 mm (12–16 in) with rigid insulation, permitted **only** for a heated structure with mean monthly indoor temp ≥ 64 °F | IRC 2021 **R403.1.4**, **R403.3** |
| Scour / flood-prone plot (riverine Punjab/Sindh, hill torrents) | Below anticipated scour depth; plinth above highest recorded flood level | Local authority byelaw |

**Rankine minimum-depth check (a useful cross-check, not a substitute):**
```
D_min = (q / γ) · [ (1 − sin φ) / (1 + sin φ) ]²  =  (q / γ) · Ka²
```
*Worked:* q = 150 kPa, γ = 18 kN/m³, φ = 30° → Ka = 0.333, Ka² = 0.111 → D_min = 8.33 × 0.111 = **0.93 m**. Consistent with the 1.0–1.5 m practical rule.

### 4.2 Footing Area Sizing

```
A_required = (Service load P + footing/backfill self-weight allowance) / SBC
Self-weight allowance: +10% of P for Df ≤ 1.5 m; +15% for Df 1.5–2.5 m
Then:  square side  a = √A ,  rounded up to the next 50 mm (or 3 in on site)
Eccentric load: use B' = B − 2e_B and L' = L − 2e_L , keep e ≤ B/6 so no uplift
```

**Quick example (the sanity check).** Column service load 150 kN, SBC 200 kPa → A = 1.1 × 150 / 200 = 0.825 m² → 910 mm square → **adopt 900 × 900 mm** (the 10% allowance and rounding absorb the difference; verify).

### 4.3 Fully Worked Isolated Footing — ACI 318-19

**Given:** interior RC column 300 × 300 mm; service dead load D = 300 kN, live load L = 120 kN; SBC = 150 kPa; Df = 1.2 m; f'c = 25 MPa; fy = 420 MPa (Grade 60 / Fe500 used at 420 design); soil γ = 18 kN/m³; non-aggressive groundwater.

**Step 1 — Plan area (SERVICE loads, ASCE 7-22 §2.4 ASD combination D + L):**
```
P_service = 300 + 120 = 420 kN
A_req = 1.1 × 420 / 150 = 3.08 m²   →  √3.08 = 1.755 m  →  adopt 1.8 × 1.8 m (3.24 m²)
```
*Soil pressure is always checked with **service/ASD** loads. Concrete design uses **factored/LRFD** loads. Mixing these is the single most common error in residential foundation calculations.*

**Step 2 — Factored net pressure (ASCE 7-22 §2.3.2: 1.2D + 1.6L):**
```
Pu = 1.2(300) + 1.6(120) = 360 + 192 = 552 kN
qu = 552 / 3.24 = 170.4 kPa
```

**Step 3 — Trial depth.** Try overall D = 350 mm, cover 75 mm (ACI 318-19 Table 20.5.1.3, cast against and permanently exposed to earth), T16 bars → **d ≈ 350 − 75 − 16 = 259 mm; use d = 255 mm** (average of two layers).

**Step 4 — Two-way (punching) shear, ACI 318-19 §22.6.** Critical perimeter at d/2 from the column face:
```
b0 = 4 × (300 + 255) = 2220 mm ;  critical area = 0.555² = 0.308 m²
Vu = 170.4 × (3.24 − 0.308) = 499.5 kN
vc = min of:
   0.33 λ √f'c                       = 0.33 × 1 × 5 = 1.65 MPa   ← governs
   0.17 (1 + 2/β) λ √f'c, β = 1      = 0.17 × 3 × 5 = 2.55 MPa
   0.083 (2 + αs·d/b0) λ √f'c, αs=40 = 0.083 × (2 + 40×255/2220) × 5
                                     = 0.083 × (2 + 4.595) × 5
                                     = 0.083 × 6.595 × 5 ≈ 2.74 MPa
φVc = 0.75 × 1.65 × 2220 × 255 / 1000 = 700.5 kN  >  499.5 kN   ✓ (ratio 1.40)
```
*(The third term, 2.74 MPa, does not govern this near-square, moderate-d geometry — 1.65 MPa does — but it will govern on shallower/very rectangular footings, so carry the correct value through: 0.083 × (2 + 4.595) × 5 = 2.74 MPa, not 3.06 MPa.)*

**Step 5 — One-way shear, ACI 318-19 §22.5.** Critical section at d from the column face:
```
Cantilever beyond critical section = (1.8 − 0.3)/2 − 0.255 = 0.495 m
Vu = 170.4 × 0.495 × 1.8 = 151.8 kN
φVc = 0.75 × 0.17 × 1 × √25 × 1800 × 255 / 1000 = 292.6 kN  >  151.8 kN   ✓
```

**Step 6 — Flexure at the column face:**
```
Cantilever arm = (1.8 − 0.3)/2 = 0.75 m
Mu = 170.4 × 1.8 × 0.75² / 2 = 86.3 kN·m
As = Mu / (φ · fy · j·d), j ≈ 0.95
   = 86.3×10⁶ / (0.9 × 420 × 0.95 × 255) = 942 mm²
As,min = 0.0018 × Ag = 0.0018 × 1800 × 350 = 1134 mm²   ← GOVERNS
   (ACI 318-19 §13.3.2.1 → shrinkage & temperature reinforcement, Table 24.4.3.2)
Provide 7 – T16 each way = 7 × 201 = 1407 mm²  →  T16 @ 250 mm c/c both ways   ✓
Max spacing: lesser of 3h = 1050 mm and 450 mm → 250 mm OK
```

**Step 7 — Development length, ACI 318-19 §25.4.2.3 (db ≤ 19 mm):**

The simplified equation has two cases, distinguished by clear spacing/cover:
- **Case 1** (divisor 2.1) applies when clear spacing between developed bars ≥ db **and** clear cover ≥ db, **or** clear spacing ≥ 2db (regardless of cover) — no minimum stirrups/ties required beyond normal detailing.
- **Case 2** (divisor 1.4, giving ~50% longer ld) applies to everything else — i.e. tighter spacing/cover without compensating ties.

*Check which case applies here:* bars at 250 mm c/c, db = 16 mm → clear spacing = 250 − 16 = 234 mm, and clear cover = 75 mm (from Step 3). Both 234 mm ≥ db (16 mm) and 75 mm ≥ db (16 mm) are satisfied by a wide margin → **Case 1 governs**, so the 2.1 divisor is the correct one to use, not an arbitrary pick.

```
ld = (fy · ψt · ψe · ψs) / (2.1 λ √f'c) × db = (420 × 1.0 × 1.0 × 0.8)/(2.1 × 5) × 16 = 512 mm
Available from critical section to bar end = 750 − 75 = 675 mm  >  512 mm   ✓
```
*If bar spacing were tight (e.g. clear spacing < db with no compensating ties), Case 2 would govern and ld would be ~50% longer (≈768 mm here) — always verify spacing/cover against the two cases before quoting a development length on a different geometry.*

**Step 8 — Minimum depth check.** ACI 318-19 §13.3.1.2: depth of a footing on soil shall be such that the **effective depth to the bottom reinforcement is at least 150 mm** — 255 mm ✓. (For footings on piles the equivalent minimum is 300 mm.)

**FINAL (PRELIMINARY, NOT FOR CONSTRUCTION):** 1800 × 1800 × 350 mm footing, top of footing at −0.85 m, base at −1.20 m below NSL, on 75 mm PCC (1:4:8) blinding; M25 concrete; T16 @ 250 c/c both ways bottom; 75 mm clear cover; column starter bars lapped 50db above footing top.

### 4.4 Durability & Concrete Specification (ACI 318-19 Ch. 19)

| Exposure | Trigger | Max w/cm | Min f'c | Cement |
|---|---|---|---|---|
| **S0** | SO₄ < 0.10 % in soil, < 150 ppm in water | — | 17 MPa | Any |
| **S1** | SO₄ 0.10–0.20 % / 150–1500 ppm | 0.50 | 28 MPa | Type II (moderate SR) |
| **S2** | SO₄ 0.20–2.00 % / 1500–10 000 ppm | 0.45 | 31 MPa | **Type V (sulphate-resisting)** |
| **S3** | SO₄ > 2.00 % / > 10 000 ppm | 0.45 | 31 MPa | Type V + pozzolan/slag |

*(Cite ACI 318-19 Tables 19.3.1.1 and 19.3.2.1 in any output using this table.)*
**Karachi coastal, Sindh sabkha, and saline-groundwater sites in southern Punjab routinely fall in S2/S3 — specify sulphate-resisting cement (locally available as SRC), w/cm ≤ 0.45, 75 mm cover, and a bituminous coat to all buried concrete faces.**

Cover (ACI 318-19 Table 20.5.1.3): **75 mm** for concrete cast against and permanently exposed to earth; 50 mm for formed surfaces exposed to earth/weather with bars > 16 mm.

### 4.5 Plinth / Grade Beams — Standard Pakistani Residential Detail

| Item | Typical |
|---|---|
| Plinth beam size | 230 × 300 mm (9" × 12") for G+1; 230 × 380 mm (9" × 15") for G+2 |
| Reinforcement | 4–T12 (2 top, 2 bottom) minimum, 6–T12 for longer spans; T8 stirrups @ 150 mm at ends / 200 mm mid |
| Level | At plinth level, tying every column and under every load-bearing wall |
| Plinth height above NSL | 450–600 mm typical; **above the highest recorded local flood level** in flood-prone districts |
| Function | Ties footings into a single settlement unit; carries the wall above; arrests differential movement; anchors DPC line |

**Plinth beams are not optional on soft, filled, or expansive ground — they are the primary differential-settlement control device in low-rise residential construction.**

### 4.6 Excavation, Shoring & Protection of Adjacent Structures

Dense Pakistani urban plots share boundaries with existing houses whose footings are typically 0.9–1.5 m deep and undocumented. Foundation excavation is where neighbour disputes and third-party damage happen.

| Situation | Rule |
|---|---|
| Unsupported excavation depth in stiff clay | ≤ 1.5 m vertical without shoring; batter to 1V:1H beyond that |
| Unsupported in dry sand/gravel | Batter to the angle of repose ≈ 1V:1.5H (34°); never vertical |
| Unsupported in saturated sand | **Never** — shore, or dewater and batter to 1V:2H |
| Excavation deeper than the neighbour's footing base | Underpin in short hit-and-miss bays (≤ 1.2 m wide, ≤ 25% of the wall length open at once), or keep your footing base above a 1V:2H line drawn down from the neighbour's footing edge |
| Trench alongside a new footing (drains, services) | Keep the trench bottom above a 1V:2H line from the footing base; otherwise the footing loses lateral support |
| Spoil and plant | Keep spoil heaps and concrete mixers ≥ 1.0 × excavation depth back from the edge — a spoil surcharge is the classic cause of trench collapse |
| Duration | Do not leave a foundation trench open through a rain event; a wetted clay founding surface loses strength immediately. Cast the PCC blinding the same day the excavation reaches level. |
| Founding surface | Hand-trim the last 100–150 mm; remove all loosened/softened soil; blind with 75–100 mm PCC 1:4:8 before placing steel |

**Pre-construction condition survey:** photograph and date every existing crack on neighbouring walls, with a scale in frame, before excavation begins. This is the single cheapest dispute-prevention measure on an urban plot and takes 30 minutes.

---

## Section 5: Settlement & Differential Settlement Control

### 5.1 Settlement Components

```
S_total = S_i (immediate/elastic) + S_c (primary consolidation) + S_s (secondary creep)

Immediate:      S_i = q · B · (1 − ν²) · If / Es
Consolidation:  S_c = (Cc / (1 + e0)) · H · log10[(σ'0 + Δσ) / σ'0]      (NC clay)
                Cc ≈ 0.009 (LL − 10)   (Terzaghi & Peck, remoulded correlation)
Stress increase: 2:1 method →  Δσ = P / [(B + z)(L + z)]
```

| Soil | Es (MPa) | ν | Influence factor If (flexible, centre / rigid square) |
|---|---|---|---|
| Soft clay | 5–25 | 0.40–0.50 | 1.12 / 0.82 |
| Medium–stiff clay | 25–100 | 0.30–0.40 | 1.12 / 0.82 |
| Loose sand | 10–25 | 0.20–0.35 | 1.12 / 0.82 |
| Medium sand | 25–50 | 0.25–0.35 | 1.12 / 0.82 |
| Dense sand / gravel | 50–150 | 0.30–0.40 | 1.12 / 0.82 |

Sands settle essentially immediately (during construction — usually harmless). **Clays keep settling for years; consolidation settlement is what cracks houses.**

### 5.2 Allowable Settlement & Angular Distortion

**Skempton & MacDonald (1956)** — derived from 98 case-history buildings, still the practical benchmark:

| Criterion | Limit |
|---|---|
| Angular distortion **δ/L** — onset of architectural (cosmetic) cracking in walls & finishes | **1/300** |
| Angular distortion — structural damage to beams/columns of a frame | **1/150** |
| Angular distortion — no cracking expected (safe design target) | **1/500** |
| Tilt visible to the naked eye | 1/250 |
| Isolated/pad footing on sand — Skempton & MacDonald max **total** settlement guideline | ~40 mm |
| Isolated/pad footing on clay at δ/L = 1/500 — max differential settlement | ~25 mm |
| Isolated/pad footing on clay at δ/L = 1/300 — max differential settlement | ~76 mm |
| Raft — max **total** settlement | 40–65 mm |
| Raft on clay — differential settlement at δ/L = 1/300 | 76–127 mm |

**IS 1904:2000 codified limits — use these as the design values, not the Skempton & MacDonald total-settlement guideline above, since the two sources give different numbers for the same isolated-footing-on-clay case (65 mm vs 40 mm) and only one can be "the" design limit.** (Directional guidance — verify the exact clause and table in the current IS 1904 text before quoting a hard number in a deliverable): for isolated foundations on clay, max total settlement ≈ 65 mm and max differential ≈ 40 mm; on sand, max total ≈ 40 mm, differential ≈ 25 mm; rafts are permitted larger totals (up to ~100 mm on clay) with the same differential limits, because a raft distributes movement.

**Design target for a residential project: total settlement ≤ 25 mm, angular distortion ≤ 1/500.** Anything at 1/300 will produce visible plaster cracking and an unhappy client, even if it is "code compliant". Where the presumptive Skempton & MacDonald figure and the IS 1904 figure disagree, **state both explicitly in the output and adopt the more conservative (lower) number for the governing check**, rather than silently picking one.

### 5.3 Differential Settlement Control — Seven Rules

1. **Keep soil pressures uniform.** Size every footing so the *service* bearing pressure is within ±10% across the building, not just below the SBC. Two footings at 60 kPa and 140 kPa on the same clay will settle by very different amounts.
2. **Never mix foundation types under one structure** on markedly different bearing strata — an isolated footing next to a strip footing next to a pile cap invites hinge cracking at the junction. If you must, put a full movement joint between the two zones, straight through the plinth beam, walls, and slab.
3. **Tie everything with plinth/grade beams** on soft or variable soil. They convert independent footings into one stiff plate.
4. **Found everything at the same level** where possible. Where the plan steps (garage, terrace, basement), step the footings at ≤ 1V:2H and lap the plinth beams.
5. **Watch the load-history difference.** A single-storey garage wing attached to a double-storey block on clay settles far less — the differential is at the junction. Either isolate it with a movement joint or run a continuous raft under both.
6. **Beware the neighbouring construction.** In dense Pakistani plots, a neighbour excavating for a new basement removes lateral support and de-waters your clay. Photograph and record pre-existing cracks; specify a party-wall condition survey.
7. **Trees.** A mature eucalyptus/shisham/neem within 1× to 1.5× its mature height of the foundation desiccates clay and causes shrinkage settlement; removing a mature tree causes heave. On shrinkable clay keep large trees at ≥ 1.0× mature height (≥ 1.5× for high-water-demand species) from the building line, or deepen/pile the foundation.

---

## Section 6: Damp-Proofing & Waterproofing

### 6.1 Damp-Proof Course (DPC) — IS 3067:1988 / BS 8215:1991

| Requirement | Value |
|---|---|
| Level | At plinth level, continuous through every wall, and lapped into the floor slab DPM |
| Height above external finished ground level | **150–200 mm** (150 mm minimum; 200 mm preferred; more where splashback or monsoon ponding occurs) |
| Continuity | Unbroken horizontally; stepped (never sloped abruptly) where levels change; lapped ≥ 100 mm at joints; carried up ≥ 150 mm at abutments |
| Cavity/retaining condition | Vertical DPC on the earth face where a wall retains soil, joined to the horizontal DPC |

**DPC material specifications:**

| Material | Thickness / spec | Notes |
|---|---|---|
| Cement concrete DPC | **38–50 mm**, M15 (1:2:4), with integral waterproofing admixture | Most common in Pakistani residential; admixture dosage per manufacturer (Pudlo / Impermo / Waterlock type) |
| Rich cement mortar DPC | **20–25 mm**, 1:3 cement:sand + waterproofing liquid | For light single-storey work |
| Bituminous / mastic coating | 2 coats × ~1.5 mm = **~3 mm** total, hot applied | Cheap, effective, but brittle — protect during backfill |
| Mastic asphalt | **10–15 mm** | Excellent, flexible, expensive |
| Polyethylene (LDPE) sheet | **500 micron (0.5 mm)** minimum, laps ≥ 100 mm sealed | Under floor slabs as DPM; can slip under heavy walls |
| Bitumen felt / self-adhesive membrane | 1.5–2.0 mm | Modern proprietary option, good laps |

**Common site failures to check for:** DPC bridged by rendering/plaster carried down over it (the single most common cause of rising damp in Pakistani houses); DPC laid then punctured by services; external ground level raised above the DPC by later paving; DPC not lapped into the floor DPM leaving a gap at the wall-slab junction.

### 6.2 Below-Grade Waterproofing (High Water Table / Basement)

Standard system for a residential basement or a footing below the water table:
1. **Blinding + membrane below the slab:** 75–100 mm PCC blinding, then a loose-laid or bonded membrane (HDPE sheet / SBS bitumen membrane / bentonite panel), turned up and lapped with the wall membrane.
2. **Positive-side (external) waterproofing on the retaining/foundation wall:** two coats bituminous or a bonded sheet membrane over a cementitious levelling coat, taken from the footing kicker to 150 mm above finished ground.
3. **Protection board** before backfill — the membrane is destroyed by angular backfill otherwise.
4. **Perimeter drainage:** 100–150 mm perforated PVC/uPVC pipe laid to ≥ 1:100 fall in a 300–450 mm envelope of clean 20–40 mm gravel wrapped in non-woven geotextile, at or just below the footing base level, discharging to a sump/soakaway/storm drain. This is a **French drain**, and it is what actually keeps water off the wall.
5. **Crystalline / integral admixtures** in the structural concrete as a second line of defence for water-retaining rafts.
6. **Uplift check for basements:** `FS = W_permanent / U ≥ 1.2` where `U = γw × (depth of water above raft soffit) × raft area`. If it fails: thicken the raft, extend a toe to mobilise soil weight, or install tension piles/anchors. **Never rely on a pumped drainage system for permanent uplift stability in a house.**

**Pakistan relevance:** canal-irrigated Punjab (Faisalabad, Sahiwal, Multan belt), the Karachi coastal strip, Hyderabad and lower Sindh, and any plot near a nullah or an irrigation channel routinely have water tables within 2–4 m. Assume waterproofing is required unless the piezometer says otherwise.

---

## Section 7: Retaining Walls for Sloped Sites

### 7.1 Lateral Earth Pressure

```
Rankine active:   Ka = (1 − sin φ) / (1 + sin φ)
Rankine passive:  Kp = (1 + sin φ) / (1 − sin φ) = 1/Ka
At-rest (rigid, e.g. basement wall):  K0 = 1 − sin φ  (use K0 whenever the wall
                                       cannot rotate ~0.001H — basements ALWAYS)
Active thrust:    Pa = 0.5 · Ka · γ · H²   acting at H/3 above the base
Surcharge q:      ΔPa = Ka · q · H         acting at H/2
Water (if undrained backfill): Pw = 0.5 · γw · Hw²  ← this is what doubles the load
```

| φ (°) | Ka | K0 | Kp | Typical backfill |
|---|---|---|---|---|
| 26 | 0.390 | 0.562 | 2.56 | Silty clay (poor backfill — avoid) |
| 28 | 0.361 | 0.531 | 2.77 | Silty sand |
| 30 | 0.333 | 0.500 | 3.00 | Clean medium sand |
| 32 | 0.307 | 0.470 | 3.25 | Sand-gravel |
| 34 | 0.283 | 0.441 | 3.54 | Well-graded gravel |
| 36 | 0.260 | 0.412 | 3.85 | Compacted crushed stone |

**Ka ≈ 0.27–0.33 for the typical φ = 30–35° granular backfill you should be specifying.** Never backfill a residential retaining wall with the excavated clay — it has low φ, holds water, and can be expansive.

### 7.2 Proportioning a Cantilever RC Retaining Wall

| Element | Rule of thumb |
|---|---|
| Base width B | **0.4H – 0.7H** (0.5H–0.6H typical for granular backfill, no surcharge) |
| Base slab thickness | H/12 – H/10, min 300 mm |
| Stem thickness at top | 200–250 mm min (for bar placing and compaction) |
| Stem thickness at base | H/12 – H/10, min 250 mm |
| Toe projection | B/3 (from front face of stem) |
| Shear key (if sliding fails) | Depth 0.3–0.6 m below base, located under the stem |
| Embedment of base below finished grade at toe | ≥ 0.6 m, and below frost/active zone |
| Gravity (mass concrete / stone masonry) wall | Base ≈ 0.5H–0.7H, top width ≥ 0.3 m, batter the face 1:6 to 1:4 |

**Required factors of safety:**

| Check | Minimum FS |
|---|---|
| Overturning about the toe | **2.0** (1.5 acceptable where Rankine active is used with no surcharge, per some codes — use 2.0) |
| Sliding along the base | **1.5** (base friction only, ignoring passive) |
| Bearing (max toe pressure vs SBC) | **3.0** on ultimate, i.e. q_max ≤ SBC |
| Eccentricity | e ≤ B/6 (keeps the whole base in compression) |
| Global/slope stability | 1.5 (static), 1.1 (seismic) — requires a slope-stability analysis |

### 7.3 Worked Retaining Wall Example (shows why sliding usually governs)

**Given:** cantilever RC wall, total height H = 2.5 m (top of wall to base soffit), granular backfill φ = 32°, γ_soil = 18 kN/m³, γ_concrete = 24 kN/m³, level backfill, no surcharge, SBC = 150 kPa. Trial: base B = 1.60 m × 0.30 m thick; stem 0.25 m thick × 2.20 m high; toe 0.45 m; heel 0.90 m.

```
Ka = (1 − sin32°)/(1 + sin32°) = 0.4701/1.5299 = 0.307
Pa = 0.5 × 0.307 × 18 × 2.5² = 17.29 kN/m   at 2.5/3 = 0.833 m above base
Overturning moment about toe, Mo = 17.29 × 0.833 = 14.41 kN·m/m

Resisting (per metre run):
  Stem   0.25 × 2.20 × 24 = 13.20 kN  @ x = 0.575 m →  7.59 kN·m
  Base   1.60 × 0.30 × 24 = 11.52 kN  @ x = 0.800 m →  9.22 kN·m
  Soil on heel 0.90 × 2.20 × 18 = 35.64 kN @ x = 1.150 m → 40.99 kN·m
  ΣW = 60.36 kN/m ,  Mr = 57.80 kN·m/m

FS_overturning = 57.80 / 14.41 = 4.01   ✓  (> 2.0)

Sliding: δ = (2/3)φ = 21.3° → μ = tan 21.3° = 0.390
  F_friction = 0.390 × 60.36 = 23.5 kN/m
FS_sliding = 23.5 / 17.29 = 1.36   ✗  (< 1.5)  ← GOVERNS
  Fix: 0.35 m deep shear key under the stem, OR extend base to B = 1.90 m,
       OR mobilise passive resistance in front of the toe (only if the toe soil
       is guaranteed never to be excavated — usually it is NOT, so do not rely on it).

Bearing:
  e = B/2 − (Mr − Mo)/ΣW = 0.80 − (57.80 − 14.41)/60.36 = 0.80 − 0.719 = 0.081 m
  e = 0.081 m  <  B/6 = 0.267 m   ✓ (no uplift, full base in compression)
  q_max = (ΣW/B)(1 + 6e/B) = 37.7 × (1 + 0.304) = 49.2 kPa   ✓ (< 150 kPa)
  q_min = 37.7 × (1 − 0.304) = 26.2 kPa   ✓ (> 0)
```

**The lesson to carry into every retaining wall: overturning almost always passes; sliding and drainage are what fail.**

### 7.4 Drainage — The Single Most Important Detail

Saturated backfill can **roughly double** the lateral load on a wall (the water thrust 0.5·γw·H² is not reduced by Ka, and the soil's effective weight drops only to buoyant). Most residential retaining wall failures in Pakistan are drainage failures, not structural under-design.

| Element | Specification |
|---|---|
| Granular drainage blanket behind the wall | **300–450 mm (12–18 in)** of clean 20–40 mm crushed stone / washed gravel, full height |
| Geotextile separator | Non-woven, wrapping the drainage stone, to stop fines migrating in and clogging it |
| Base drain | 100 mm perforated pipe at the heel, ≥ 1:100 fall, discharging to daylight or a storm drain (never into a closed pit) |
| Weep holes | **75–100 mm dia PVC, spaced 1.2–2.0 m horizontally**, lowest row ~150–300 mm above finished grade at the toe, one row per 1.0–1.5 m of height, each backed by a gravel pocket + geotextile |
| Surface at the top | Impervious cap (compacted clay layer or paving) sloped **away** at ≥ 1:20 for the first 2 m, plus a cut-off drain upslope |
| Backfill compaction | Compact in 200–300 mm layers to 95% MDD, but **light plate compactor within 1 m of the wall** — heavy rollers apply compaction-induced pressures far above Ka·γ·H and have cracked new stems |

### 7.5 When a Retaining Wall Needs a Full Engineered Design

| Height | Requirement |
|---|---|
| **≤ 0.9–1.2 m (3–4 ft)**, level backfill, no surcharge, good drainage | Standard/prescriptive detailing generally accepted; still show it to an engineer |
| **> 1.2 m** | **Full engineered design mandatory** — overturning, sliding, bearing, global stability, structural design of stem/toe/heel, plus authority approval |
| Any height with a surcharge (driveway, adjacent building, sloping backfill) | Full engineered design |
| Any height in seismic Zone 3/4 (Quetta, Muzaffarabad, northern areas) | Full engineered design incl. Mononobe–Okabe seismic earth pressure |
| Terraced/stacked walls | Full engineered design — the upper wall surcharges the lower one |

**Surcharge allowances:** pedestrian/light 5 kPa; car parking/driveway **10–12 kPa** (≈ 0.6 m of soil); adjacent building — model the actual footing pressure, do not use a blanket surcharge.

**Pakistan relevance:** the Margalla foothill plots in Islamabad (E-7, F-6/F-7 upper sectors, Bani Gala), Murree, Nathia Gali, Abbottabad, and the Swat/Kaghan valleys are all sloped-site construction where cut-and-fill terracing and retaining walls dominate the foundation cost — and where slope instability, not bearing failure, is the actual hazard. **Never place a footing on filled ground behind a retaining wall.**

---

## Section 8: Water Table & Expansive (Black Cotton) Soil

### 8.1 High Water Table

| Effect | Consequence & response |
|---|---|
| Reduced effective bearing capacity | Submerged unit weight γ' ≈ γ_sat − 9.81 ≈ half of γ → the 0.5·γ·B·Nγ term halves. Apply Cw = 0.5 when the water table is at founding level. |
| Buoyancy / uplift | Rafts and basements float. Check FS_uplift = W/U ≥ 1.2. |
| Construction dewatering | Well-point or sump pumping during excavation; budget for it. Over-pumping settles neighbouring buildings — limit drawdown and monitor. |
| Reduced soil strength / boiling | Sand boiling and base heave in excavations. Keep excavation slopes ≤ 1V:2H in saturated sand, or shore. |
| Chemical attack | Test sulphate & chloride; specify per ACI 318-19 exposure class (§4.4). |
| Liquefaction | Saturated loose sand with (N1)60 < 15 and water table within ~10–15 m, in seismic Zone 2B or higher → **liquefaction assessment mandatory**. Relevant to Karachi's Malir/Lyari riverbed deposits and Indus floodplain sites. Mitigation: densification (vibro/stone columns), or pile through to non-liquefiable stratum. |
| Long-term | Design for the **highest seasonal / monsoon water table**, not the level found during a dry-season borehole. Ask for a piezometer reading, not a one-off "water struck at" note. |

### 8.2 Expansive / Black Cotton Soil — the Subcontinent's Foundation Killer

**Identification:**

| Indicator | Low | Medium | High | Very high |
|---|---|---|---|---|
| Free swell index (IS 2720 Pt 40) | < 20 | 20–35 | 35–50 | > 50 |
| Plasticity index PI | < 18 | 18–35 | 35–55 | > 55 |
| Shrinkage limit (%) | > 15 | 10–15 | 7–10 | < 7 |
| Clay fraction (< 2 µm) | < 15% | 15–30% | 30–60% | > 60% |
| Field signs | — | — | Deep polygonal shrinkage cracks in the dry season; sticky, black, greasy when wet; "cotton soil" | Same, plus historic heave damage nearby |

**Behaviour:** volumetric swell can exceed **10%** on wetting; swelling (uplift) pressures reported up to **~263 kN/m² (≈5500 psf)** in severe cases — an order of magnitude greater than the bearing pressure a light house applies. This is why a house on black cotton soil lifts and cracks even though the soil's "bearing capacity" table value (130–160 kPa) looks fine. **Bearing capacity is never the governing issue in expansive soil — heave and shrinkage are.**

**Active zone:** the depth over which seasonal moisture change drives swell/shrink. **Typically 1.5–3.5 m in the subcontinent (up to 4.5 m in severe, deeply-desiccated profiles).** Any shallow footing founded inside this zone will cycle up and down every monsoon and dry season.

**Mitigation hierarchy (best first):**

1. **Under-reamed piles (IS 2911 Part 3)** — the standard subcontinent solution. Stem 250–375 mm, bulb 2.0–2.5 × stem, **minimum 3.5 m long**, bulb anchored **below the active zone**. The bulb provides anchorage against uplift; the stem is designed for the tensile uplift force from swelling soil gripping it.
2. **Grade/capping beams with a void beneath** — cast the grade beam on 75–100 mm of compressible material (EPS board, brick-on-edge sacrificial layer, or a proprietary void former) so that swelling soil pushes into the void and never directly loads the structure. **This detail is what makes the pile solution work; omitting it defeats the piles.**
3. **Deep, narrow strip footings below the active zone**, with a low-friction sleeve (polythene wrap / bitumen coat) on the sides of the foundation shaft so swelling soil cannot grip and lift it.
4. **Remove and replace** the top 1.0–1.5 m with non-expansive engineered fill (sand/moorum/crushed stone) compacted to 95% MDD — economical for small single-storey houses where the expansive layer is shallow.
5. **Lime stabilisation** — 4–8% hydrated lime mixed into the top 0.5–1.0 m reduces PI and swell substantially; requires proper mixing plant and a mix design, plus a sulphate check (lime + sulphate = ettringite heave, worse than the original problem).
6. **Stiff ribbed raft** (beam-and-slab raft, beams 450–750 mm deep at 3–4 m centres) — a reasonable compromise for a small single-storey house where piling is uneconomical. The raft rides the movement as one rigid body, converting differential heave into acceptable tilt.
7. **Moisture control around the perimeter** — mandatory alongside any of the above:
   - Impervious apron/paving **1.0–1.5 m wide** all round, sloped away at ≥ 1:20.
   - No ponding, no soakaways, no septic tanks, no leaking pipes within 3 m.
   - **No large trees within 1.0–1.5 × mature height**; never remove a mature tree adjacent to an existing shallow-founded building without an engineer's advice (removal causes heave).
   - Consistent perimeter moisture — either keep it uniformly dry (apron + drainage) or uniformly damp; the damage comes from the *differential*.

**Never do on expansive soil:** shallow isolated pads inside the active zone; a slab-on-grade tied rigidly to deep-founded columns (it will crack at the junction as the slab heaves and the columns do not); a strip footing at 1.0 m depth "because that's what we always do"; backfilling around foundations with the excavated black cotton soil.

### 8.3 Other Problem Soils Found on South Asian Plots

| Soil | How to spot it | Why it bites | Response |
|---|---|---|---|
| **Collapsible loess** (Potohar plateau, parts of northern Punjab, Balochistan fans) | Low dry density (11–14 kN/m³), open structure, stands in vertical faces when dry, high void ratio | Holds load fine when dry, then **collapses suddenly on first wetting** — a leaking pipe or the first monsoon after occupation drops a corner of the house | Soaked (double-oedometer) collapse-potential test. If collapse potential > 2%: pre-wet and compact, remove/replace, or found below the collapsible layer. Waterproof and drain the perimeter obsessively. |
| **Uncontrolled / made-up fill** (extremely common on newly developed housing-society plots) | Brick bats, plastic, ash, variable N (2 → 25 in one hole) | Unpredictable, keeps settling for years, often organic | Never found on it. Remove entirely (if ≤ 1.5–2 m) or pile through it. Discount all shaft friction inside fill. |
| **Soft marine / lagoon clay** (Karachi coastal belt, Indus delta) | Grey-black, high water content, cu < 25 kPa, shell fragments | Very large long-term consolidation settlement; low SBC | Raft with a granular mattress, or piles to the underlying stiff stratum. Consolidation test mandatory. |
| **Sabkha / saline crust** (coastal Sindh, southern Punjab) | Salt efflorescence, high chloride/sulphate | Destroys ordinary concrete and rebar; volume change on wetting | Sulphate-resisting cement, w/cm ≤ 0.45, 75 mm cover, bituminous coat to all buried faces, capillary break under slab (§4.4, §6) |
| **Liquefiable loose saturated sand** (Indus/Malir floodplain, Zone 2B+) | (N1)60 < 15, uniform fine sand, water table < 10 m | Loses all strength in a design earthquake; the house sinks/tilts | Formal liquefaction assessment (Youd & Idriss / NCEER simplified). Mitigate by densification, stone columns, or pile through to non-liquefiable strata. |
| **Desiccated expansive crust over soft clay** | High N in the top 1–2 m, then N drops to 3–5 | The "good" crust is a trap — it is stiff only while dry, and the soft clay below controls settlement | Ignore the crust in the settlement calculation; design against the underlying soft layer. |

### 8.4 Pakistan Regional Ground Conditions (planning-stage orientation only)

| Region | Typical profile | Foundation implication |
|---|---|---|
| Central/upper Punjab (Lahore, Faisalabad, Gujranwala, Sialkot) | Indus/Ravi alluvium — interbedded silty clay (CL/ML) and fine sand; SBC ~100–150 kPa at 1.2–1.5 m; water table 3–12 m, higher near canals | Isolated/strip footings at 1.2–1.5 m usually adequate; check consolidation in clay lenses; seismic Zone 2A/2B |
| Southern Punjab / interior Sindh (Multan, Bahawalpur, Sukkur) | Alluvium with expansive clay pockets and saline/sabkha soils; sulphate-rich groundwater | Screen for expansive soil; sulphate-resisting cement; deeper founding |
| Karachi & coastal Sindh | Highly variable: shallow limestone/shale (Gaj/Manchhar) giving very high SBC in parts, vs soft marine clay and loose sand in Malir/Lyari/coastal belt; saline groundwater | Investigation is essential — adjacent plots differ wildly. Liquefaction screening in loose saturated sand. S2/S3 sulphate exposure. Zone 2B |
| Islamabad / Rawalpindi / Potohar | Stiff residual silty clay over Murree Formation sandstone-shale; foothill slopes; loess in places (collapsible on wetting) | Good bearing at modest depth; sloped sites need retaining walls; check collapsible loess by a soaked oedometer test; Zone 2B |
| Northern areas / AJK (Murree, Abbottabad, Swat, Gilgit, Muzaffarabad) | Colluvium, talus, boulder beds over rock; steep slopes; landslide-prone | Slope stability governs; benched/stepped footings or rock anchors; frost depth 0.3–0.9 m above ~1,800 m; **seismic Zone 3/4 — engineer mandatory** |
| Balochistan (Quetta, Ziarat) | Alluvial fan gravels, some expansive clays; very high seismicity | **Zone 4** — seismic detailing governs the whole structure, tie all footings with grade beams |

**Seismic zones (BCP 2007 / SP-2007) and PGA bands:**

| Zone | Effective PGA | Character |
|---|---|---|
| 1 | 0.05–0.08 g | Minor |
| 2A | 0.08–0.16 g | Moderate |
| 2B | 0.16–0.24 g | Moderate-strong |
| 3 | 0.24–0.32 g | Strong |
| 4 | > 0.32 g | Severe |

*City-to-zone assignments circulate widely (e.g. Karachi 2B, Lahore 2A/2B, Islamabad/Rawalpindi 2B, Peshawar 2B, Quetta 4, Muzaffarabad 4) but **must be read off the official BCP SP-2007 seismic zoning map for the actual site coordinates** before use in any calculation.*

**Seismic foundation rules (this skill's practice substitution — see the Code Posture note above — drawing on ASCE 7-22 Ch. 12 as the numeric standard-of-practice source, since BCP 2007 itself predates it):** in Zone 2B and above, tie all isolated footings together with grade beams or a slab capable of carrying **10% of the larger column's factored vertical load** in tension/compression (ASCE 7-22 §12.13.8.2 / IBC §1809.13); found all footings of one building at the same level where possible; avoid founding on liquefiable or sensitive soil without mitigation.

---

## Section 9: FreeCAD BIM Modelling of Foundations

Pairs with the **`architecture-freecad-bim`** skill. Model the foundation as real BIM objects, not as decorative boxes, so quantities and sections come out correct.

| Physical element | FreeCAD / IFC mapping |
|---|---|
| Isolated pad, strip, combined footing | `Arch Structure` (from a sketch profile + extrusion), IfcType = **IfcFooting** |
| Raft / mat | `Arch Structure` slab, IfcType = **IfcSlab** with PredefinedType BASESLAB (or IfcFooting/SLAB_FOOTING) |
| Pile | `Arch Structure`, IfcType = **IfcPile** |
| Pile cap / capping beam | `Arch Structure`, IfcType = **IfcFooting** (PILE_CAP) |
| Plinth / grade beam | `Arch Structure`, IfcType = **IfcBeam** |
| Retaining wall | `Arch Wall`, IfcType = **IfcWall**, with a separate `IfcFooting` base slab |
| PCC blinding | `Arch Structure`, IfcType = **IfcFooting** or a generic `IfcBuildingElementProxy`, distinct material |
| DPC layer | Material layer in the wall's `Arch MultiMaterial`, not a separate solid |
| Excavation / backfill | `Arch Site` terrain object with a Subtraction, so cut/fill volumes are real |

**Structuring rules:**
1. Create a **`Foundation` BuildingStorey** with a **negative elevation** (e.g. `Placement.Base.z = -1200`) inside the Building, and put every footing, pile, blinding, and grade beam inside it. Do not dump foundations into the Ground Floor storey — the storey schedule and section cuts will be wrong.
2. Model **top of footing** and **founding level** as distinct, driven by parameters `Df` (founding depth below NSL) and `t` (footing thickness): `z_top = -(Df - t)`, `z_base = -Df`.
3. Drive footing dimensions from a **spreadsheet** (`Spreadsheet` workbench) holding `P_service`, `SBC`, `Df`, `f'c` per column mark, and bind the Arch Structure Length/Width/Height to the cells. Then a change in SBC re-sizes the whole foundation plan.
4. Use **Subtractions** (parametric) for service penetrations and the void beneath grade beams on expansive soil — never a frozen boolean cut.
5. For sloped sites, model the terrain first (`Arch Site` with an imported/roughed mesh) and step the footings to follow it; a 1V:2H maximum step line between adjacent footing levels.
6. Assign real **materials** (`Arch Material`): `Concrete-M25`, `Concrete-PCC-1:4:8`, `Steel-Fe500`, `Gravel-Drainage`, `Soil-Backfill` — this is what makes the quantity take-off usable.
7. Add a `Description`/`IfcData` property on every foundation object reading **"PRELIMINARY — NOT FOR CONSTRUCTION"** until a stamped design exists.

**Minimal parametric footing snippet (FreeCAD Python console / MCP `execute_code`):**

```python
import FreeCAD as App, Arch, Draft
doc = App.ActiveDocument
def pad(name, L, W, T, x, y, Df):
    """L,W,T,x,y,Df in mm. Founding level = -Df; top of pad = -(Df - T)."""
    base = Draft.makeRectangle(L, W, placement=App.Placement(
        App.Vector(x - L/2, y - W/2, -Df), App.Rotation()))
    s = Arch.makeStructure(base, height=T)
    s.Label = name
    s.IfcType = "Footing"
    return s

F1 = pad("F1_1800x1800x350", 1800, 1800, 350, 0, 0, 1200)
doc.recompute()
```

---

## Section 10: Deliverable Checklist & Common Errors

### 10.1 Before Issuing Any Foundation Output

- [ ] Soil investigation report referenced by name/date, **or** an explicit statement that none exists and all values are presumptive
- [ ] SBC stated with its source (borehole + method, or plate load test, or presumptive table) and the factor of safety used
- [ ] Water table depth and season of measurement stated
- [ ] Expansive-soil screening result stated (free swell index / PI), even if the answer is "not tested"
- [ ] Sulphate/chloride result stated, or flagged as required, for any coastal/saline site
- [ ] Service loads used for bearing check; factored loads used for concrete design — **stated separately**
- [ ] Settlement estimate and the angular-distortion check against 1/500
- [ ] Foundation depth justified (active zone / frost / scour / adjacent footings / topsoil)
- [ ] Drainage and DPC/waterproofing specified, not assumed
- [ ] Seismic zone and the ASCE 7 §12.13.8.2 grade-beam tie requirement addressed for Zone 2B+
- [ ] Every drawing/model/schedule labelled **"PRELIMINARY — NOT FOR CONSTRUCTION — requires review and seal by a licensed (PEC-registered) structural engineer and local authority approval"**

### 10.2 Errors This Skill Exists to Prevent

| Error | Why it's wrong |
|---|---|
| Using factored (1.2D+1.6L) loads to check soil bearing | SBC already contains a factor of safety of 2.5–3.0; double-factoring oversizes footings ~35% |
| Using service loads to design footing shear/flexure | Under-designs the concrete — dangerous |
| Taking a presumptive table SBC as the design value | Presumptive tables are for feasibility. A soil report governs. |
| Ignoring the plate-size-to-footing-size settlement scale-up | Under-predicts real settlement by 2–3× |
| Founding a shallow footing in black cotton soil at 1.0 m "as usual" | Inside the active zone → cyclic heave → guaranteed cracking |
| No water-table correction on sand bearing capacity | Overestimates SBC by up to 2× |
| Retaining wall with no drainage blanket / weep holes | Saturated backfill can roughly double the design thrust |
| Relying on passive resistance at the toe of a retaining wall | The toe soil is routinely excavated later for a drain or a path |
| Mixing footing types under one house | Differential settlement at the junction |
| Cement plaster carried down over the DPC | Bridges the DPC → rising damp, the most common Pakistani residential defect |
| Backfilling against a new stem with a heavy roller | Compaction-induced pressure far exceeds Ka·γ·H → stem cracks |
| Picking the wrong development-length Case (1 vs 2) without checking bar spacing/cover | Understates ld by ~30–50% if Case 2 actually governs |
| Skipping the soil test on a "small" house to save money | A Rs 50k–150k investigation against a Rs 1–3 crore house and an unfixable defect |

---

## Section 11: Standards Index (cite these explicitly in outputs)

| Standard | Scope as used here |
|---|---|
| **BCP 2007 (SP-2007, UBC-1997-based) / BCP 2021 Ch. 16 "Structural Design"** | Pakistan seismic zoning, site class, load combinations; BCP 2021 references ASCE 7 / ACI 318 / UBC. Neither edition contains Pakistan-specific numeric geotechnical tables; BCP 2007 predates ASCE 7-22 and does not cite it. |
| **ASCE 7-22** Ch. 2 (load combinations), Ch. 11–12 (seismic), §12.13 (foundation design), §12.13.8.2 (grade-beam ties) — used here as this skill's **substitute** modern numeric source, not as text BCP 2007 itself references | Loads feeding foundation design |
| **ACI 318-19** Ch. 13 (Foundations), §13.3.1.2 (min depth), §13.3.2.1 (min reinforcement), Ch. 22 (§22.5 one-way, §22.6 two-way shear), Tables 19.3.1.1/19.3.2.1 (sulphate exposure), Table 20.5.1.3 (cover), §25.4.2.3 (development length, Case 1/Case 2) | Footing concrete design |
| **IS 1904:2000** | Foundations in soils — general requirements: min depth 500 mm, settlement criteria (verify exact clause before quoting — see §5.2), foundations near existing structures |
| **IS 6403:1981** | Determination of bearing capacity of shallow foundations |
| **IS 1888:1982** | Method of load test on soils (plate load test) |
| **IS 2131:1981 / ASTM D1586** | Standard penetration test |
| **IS 2911 (Part 3):1980; (Part 4)** | Under-reamed piles; pile load testing |
| **IS 2950 (Part 1)** | Design of raft foundations |
| **IS 1498 / IS 2720 (Parts 2, 4, 5, 10, 11, 15, 27, 29, 40)** | Soil classification and laboratory testing incl. free swell index |
| **IS 3067:1988 / BS 8215:1991** | Damp-proof courses |
| **IS 456:2000** | RC design where Indian practice is followed instead of ACI (min reinforcement 0.12% HYSD, cover 50 mm to footings) |
| **IRC 2021 R403.1.4, R403.3** | US frost-depth and Frost-Protected Shallow Foundation provisions — **comparative reference only, not applicable to Pakistan lowlands** |
| **Terzaghi (1943), Terzaghi & Peck (1948)** | Ultimate bearing capacity; SPT settlement correlation |
| **Meyerhof (1956, 1963)** | SPT allowable-pressure correlation; bearing capacity factors with shape/depth/inclination |
| **Skempton (1951)** | Nc for saturated clay (6.2 → 9.0 with depth) |
| **Skempton & MacDonald (1956)** | Allowable settlement and angular distortion limits (1/300 architectural, 1/150 structural) — a *guideline*, distinct from and sometimes numerically different than the IS 1904 codified limits; see §5.2 |
| **Stroud (1974)** | cu ≈ 4.5–6 × N60 |
| **Liao & Whitman (1986)** | SPT overburden correction CN |

---

## Section 12: Handoff to the Geotechnical & Structural Engineer

What to give the licensed engineer so the review is a review and not a redesign:

| Deliverable | Content |
|---|---|
| Site & plot data | Address/coordinates, plot size, survey with spot levels, existing structures and their approximate founding depths, boundary conditions, access for a drilling rig |
| Ground data | The geotechnical report in full (borelogs, SPT, lab results, water table, chemistry) — or a written statement that no investigation exists |
| Superstructure model | Structural system, grid, storey heights, column marks with **service and factored** axial loads + moments, wall loads per metre, any future vertical extension intended |
| Foundation proposal | Type, founding depth, sizes, the SBC used and where it came from, the FS used, the settlement estimate, the governing check for each footing |
| Special conditions | Expansive soil, water table, slope, retaining walls, basement, adjacent construction, seismic zone |
| Drawings/model | FreeCAD/IFC model + foundation layout, footing schedule, sections through every retaining wall and step in level, DPC and waterproofing details |
| Explicit ask | "Please review, amend and seal this preliminary foundation design for construction, and confirm the geotechnical assumptions." |

**Questions to put to the geotechnical engineer in writing** (the answers change the design, and getting them verbally is how they get lost): recommended net SBC at the proposed founding depth and the FS applied; recommended foundation type; estimated total and differential settlement for the given loads; seasonal high water table; swell pressure and active-zone depth if expansive; ACI sulphate exposure class; SPT hammer energy ratio; whether a seismic bearing-capacity increase is permitted; whether liquefaction assessment is required.

## Section 13: Known Gaps in This Skill (state these when relevant)

1. **No Pakistan-specific numeric geotechnical code exists to cite.** The numeric backbone here is IS (Indian Standard) practice plus ACI/ASCE. That is standard subcontinent practice, but it is a substitution, not a citation of Pakistani law. Say so rather than implying BCP contains these tables, and never imply BCP 2007 itself references ASCE 7-22 by name — it predates that edition.
2. **The presumptive SBC table (§2) is folklore-grade.** It is widely circulated as "IS 1904 values" but the provenance of individual rows is weak. Use only for feasibility.
3. **IS 1904 settlement limits (§5.2) are quoted directionally, and disagree numerically with the Skempton & MacDonald guideline quoted alongside them.** Verify the exact clause and table in the current IS 1904 text before putting a hard number in a deliverable, and always flag which source a quoted settlement limit comes from.
4. **Seismic zone assignments (§8.4) are commonly-cited, not authoritative.** Read the official BCP SP-2007 map for the actual site coordinates.
5. **No slope-stability analysis method** is given (Bishop/Janbu/limit equilibrium) — sloped sites need a geotechnical engineer with software, not a rule of thumb.
6. **No liquefaction calculation procedure** is given, only the screening trigger.
7. **No basement structural design** (propped cantilever walls, heave of the base slab, construction sequence) — out of scope; escalate.
8. **Cost figures are relative, not absolute.** Rates move fast in Pakistan; take current rates from the `architecture-cost-estimation-boq` skill, not from here.
9. **Machine foundations, water tanks, swimming pools, boundary walls over 2.5 m** are not covered.

**Related skills:** `architecture-structural-systems` (superstructure loads feeding these footings) · `architecture-concrete-reinforcement-detailing` (bar bending, laps, cover) · `architecture-seismic-design` (zone, tie requirements) · `architecture-roofing-waterproofing` (DPC/tanking continuity above plinth) · `architecture-freecad-bim` (modelling) · `architecture-cost-estimation-boq` (excavation, PCC, RCC quantities) · `architecture-building-codes-permits` (LDA/CDA/SBCA approval).

---

**Final reminder, restated because it is the most important line in this file:** every number above is a design aid for planning and FreeCAD modelling. A real house needs a site-specific geotechnical investigation, a design sealed by a licensed (PEC-registered) structural engineer, and local authority plan approval before a single cubic metre of soil is excavated.
