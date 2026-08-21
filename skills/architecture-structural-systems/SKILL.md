---
name: architecture-structural-systems
description: >
  Residential structural systems for 1-3 storey houses, calibrated to Pakistan
  (BCP-SP 2007 / BCP 2021) with ACI 318-19, ASCE 7-22, UBC-97 and IRC 2021 as
  deep-detail cross-references. Covers system choice (load-bearing masonry vs
  confined masonry vs RCC frame vs light steel/timber vs hybrid), preliminary
  slab/beam/column/wall/footing sizing tables for residential spans, tributary
  load take-down method, roof-to-soil load path, gravity plus wind and seismic
  load basics, masonry compressive and wall-density checks, confined masonry
  detailing rules, sloped-roof and truss framing for snow country, quantity
  sanity-check ratios, and FreeCAD modelling defaults. Provides worked numeric
  examples for a typical G+1 Pakistani house.
---

# Structural Systems for Houses (1-3 Storey, Pakistan-Calibrated)

This skill is a **preliminary sizing and modelling aid** for single- and double-storey (and at most G+2) houses — the kind actually built on 3, 5, 10 marla and 1 kanal plots in Pakistan, or their equivalents elsewhere. It exists so that a floor plan drawn in FreeCAD has *plausible, code-anchored* wall thicknesses, column grids, beam depths, slab depths and footing sizes rather than arbitrary ones, and so that the load path from roof tile to soil can be narrated and checked. Everything below is a rule of thumb, a code minimum, or a hand calculation — none of it is a substitute for analysis and design by a licensed engineer.

## Reality Check - Licensing & Liability

**This skill produces design aids and calculation guidance for planning and FreeCAD modelling ONLY.**

- Every number here is a **preliminary sizing estimate, a code minimum, or a rule of thumb**. Rules of thumb are calibrated to "typical" loads, spans, soils and seismicity. Your house is not typical until someone has checked it.
- **Any design intended for the actual construction of a real occupied building MUST be reviewed, analysed, and stamped by a licensed structural engineer** — in Pakistan, a **PEC-registered (Pakistan Engineering Council) Professional Engineer** with the relevant structural category. Outside Pakistan, the equivalent locally licensed/chartered structural engineer.
- **The design MUST also go through local authority plan approval before construction** — LDA (Lahore), CDA (Islamabad), RDA (Rawalpindi), SBCA (Karachi), PDA, GDA, or the relevant TMA/Cantonment Board — under their building byelaws (setbacks, height, FAR, covered area, staircase and ventilation rules), which are *separate* from and *additional to* the structural code.
- **Claude / Claude must never present FreeCAD output, a sizing table result, or any calculation in this skill as construction-ready.** Not as "the structure", not as "the design", not as "final". The correct framing is always: *"preliminary massing and sizing for coordination — to be verified and stamped by a PEC-registered structural engineer."*
- **Say this unprompted.** If a user starts talking as though the output is final — asks for a bar bending schedule to hand a contractor, asks "so how much steel do I buy", says "we're pouring next week", asks to remove a column "since the model still stands up", or shares the model with a mason — stop and state the licensing requirement explicitly *before* continuing. Do not wait to be asked.
- **Never certify.** Do not produce anything that looks like a stamped drawing, an engineer's certificate, a structural stability certificate, or a soil report. Do not put an engineer's name, PEC number, or signature block on output.
- **Soil is never assumed.** Every foundation number in this skill is conditional on a **site-specific geotechnical investigation** (trial pits / SPT boreholes). "Assume 150 kPa" is a placeholder for a modelling parameter, never a design input.
- **Seismic zone is never guessed.** City-to-zone assignments below are *commonly cited* and must be confirmed against the current governing map (BCP 2021, superseding BCP-SP 2007) before any real use.
- **The output of an FEM run is not a stamp.** Even a converged CalculiX/`run_fem_analysis` result in FreeCAD is a check on the model you built, not a check on the building. It shares every one of the model's assumptions.

---

## Section 0: How to Use This Skill

### 0.1 Route by question type

| The user asks… | Go to |
|---|---|
| "What system should this house use?" | §1 decision tree → §1.2 catalogue → §1.4 hybrid rules |
| "How thick is the slab?" | §5.1 practical table, §5.6 span/depth quick reference |
| "How deep is the beam over this span?" | §6.2 table (or §6.1 rule: span(m) × 60-65 mm) |
| "What size are the columns?" | §7.3 quick table; §7.2 if a real take-down is wanted |
| "Is this wall thick enough / can it carry the floors?" | §8.1 masonry compressive + slenderness check |
| "Will this house survive an earthquake?" | §2.2 zone → §10 ELF → §1.2 wall-density table (CM/URM) |
| "How big are the footings?" | §12 — but first: **is there a soil report?** |
| "Draw/model this in FreeCAD" | §17 defaults, then hand off to `architecture-freecad-bim` |
| "Is it done / can I build it?" | §18 handoff checklist + Reality Check, unprompted |
| "How much steel and concrete?" | §16 sanity ratios for a feel; `architecture-cost-estimation-boq` for real numbers |

### 0.2 The 60-second default house

When someone needs *a* plausible answer immediately for a normal 1-2 storey Pakistani house on ≤ 4.5 m spans, in Zone 1-2B, on soil with SBC ≥ 150 kPa:

```
System            confined masonry
Structural wall   230 mm (9"),  partitions 115 mm (4.5")
Tie-columns       230 × 230 mm at corners, junctions, free ends, ≤ 4.0 m spacing
Tie-beams         230 × 230 mm at every floor + roof, continuous ring
Slab              125 mm (5") two-way solid, 150 mm (6") if any span > 4.3 m
Lintels           150-230 mm deep over every opening, 230 mm bearing each side
Plinth beam       230 × 230 mm on every wall line
Strip footing     600 mm wide × 300 mm thick, founded 1.2-1.5 m below NGL
Floor-to-floor    3200 mm (10'-6"), clear height 2750 mm
```

Then immediately say: *preliminary, subject to soil investigation, seismic zone confirmation, and PEC-registered engineer's design.*

### 0.3 Sibling skills — hand off rather than duplicate

| Topic | Skill |
|---|---|
| Building the 3D BIM model, parametric openings, FEM run | `architecture-freecad-bim` |
| Rebar detailing, lap/development lengths, bar bending schedules | `architecture-concrete-reinforcement-detailing` |
| Soil investigation, SBC derivation, settlement, retaining walls | `architecture-geotechnical-foundations` |
| Full seismic analysis, irregularity checks, retrofit | `architecture-seismic-design` |
| Byelaws, setbacks, plan approval, PEC/PCATP stamping process | `architecture-building-codes-permits` |
| Room sizes, circulation, plan layout | `architecture-spatial-planning` |
| BOQ, quantities, market rates | `architecture-cost-estimation-boq` |
| Build order, curing, formwork striking, QC hold points | `architecture-construction-sequencing` |
| Roof waterproofing, insulation, drainage detail | `architecture-roofing-waterproofing` |
| Services routing, slab penetrations, shaft coordination | `architecture-mep-coordination` |

### 0.4 Units convention used throughout

Metric is primary; imperial in parentheses because Pakistani sites, masons and steel yards work in feet and inches. Bar sizes are given as US **#** designations with the metric equivalent that is actually sold locally: **#3 = 10 mm, #4 = 12/13 mm, #5 = 16 mm, #6 = 19/20 mm, #7 = 22 mm, #8 = 25 mm.** Loads in kN and kN/m²; stresses in MPa; soil bearing in kPa.

---

## Section 1: Choosing the House Structural System

### 1.1 Decision Tree

```
START: 1-3 storey house
│
├─ Q1. Number of storeys (including any future planned storey)?
│   ├─ 1-2 storeys, no planned addition ......... masonry systems viable
│   ├─ 3 storeys ............................... confined masonry (upper limit) or RCC frame
│   └─ 4+ storeys or planned vertical extension  RCC FRAME. Stop considering masonry.
│
├─ Q2. Seismic zone (BCP-SP 2007 / BCP 2021)?
│   ├─ Zone 1 or 2A (Lahore, Multan, Faisalabad*)  any system; URM acceptable if simple box plan
│   ├─ Zone 2B (Karachi, Islamabad, Peshawar*) ... confined masonry MINIMUM; URM discouraged
│   └─ Zone 3 or 4 (Quetta, Muzaffarabad, Gilgit*) confined masonry with full detailing,
│                                                   or ductile RCC frame. URM: DO NOT USE.
│                                                   (*verify every city against current map)
│
├─ Q3. Largest required clear span?
│   ├─ ≤ 4.5 m ....... any system; masonry walls comfortably carry a solid slab
│   ├─ 4.5 - 6.0 m ... masonry + one-way slab on beams, or RCC frame
│   └─ > 6.0 m (large drawing room, car porch, basement parking, column-free hall)
│                      RCC FRAME (or an RCC frame element inserted into a masonry house)
│
├─ Q4. Plan regularity?
│   ├─ Simple rectangle / near-square, walls line up floor to floor .. masonry fine
│   └─ L / T / U shape, big re-entrant corners, cantilevered upper floor,
│      open ground floor for parking (soft storey) ................... RCC FRAME
│                                                                       + seismic joint at re-entrants
│
├─ Q5. Budget vs speed vs supervision quality?
│   ├─ Lowest cost, mason-buildable, low supervision ....... load-bearing / confined masonry
│   ├─ Mid cost, needs competent bar-bending supervision ... confined masonry
│   └─ Highest cost, needs real supervision + testing ...... RCC frame
│
├─ Q6. Any of these hard triggers → RCC FRAME regardless of the above?
│   • Basement under the house
│   • Ground-floor car porch/parking spanning > 5 m with rooms above
│   • Any column that does NOT continue to foundation ("floating column") in the design intent
│   • Ground floor to be left open for future shop fronts
│   • Roof carrying a large overhead water tank away from a wall line
│   • Slope site with a stepped/split-level structure
│
└─ Q7. Does part of the house trip Q3/Q6 while the rest does not?
    → HYBRID: confined masonry wing + RCC frame bay. Legitimate and common,
      but only under the rules in §1.4. Do NOT mix casually.
```

### 1.2 System Catalogue

#### System A — Load-Bearing Unreinforced Masonry (URM)

The walls themselves are the structure. Slab bears directly on the wall. No RC columns.

| Parameter | Value |
|---|---|
| Storeys | 1-2 safely; 3 only in Zone 1/2A with a simple box plan and engineer's check |
| Structural wall thickness | 230 mm (9") minimum for load-bearing; 345 mm (13.5") at ground floor of a 3-storey |
| Non-structural partition | 115 mm (4.5") — **carries nothing, must never support a slab** |
| Typical floor span | 3.0-4.5 m (slab spanning wall to wall) |
| Max practical span | 4.5 m one-way solid slab; 5.5 m two-way |
| Wall slenderness limit | effective height / thickness ≤ 20 (unreinforced); ≤ 27 permitted with checks |
| Openings | Total opening width ≤ 50% of wall length per storey; nearest opening edge ≥ 600 mm from a corner |
| Lintels | RC lintel over every opening, bearing ≥ 230 mm each side (300 mm preferred) |
| Relative cost | **1.00× (baseline)** |
| Speed | Slowest per floor (4-6 weeks/floor traditional) but no formwork trades |
| Fire | Inherent — 230 mm solid brick achieves ≥ 120 min REI |
| Thermal | Excellent thermal mass — a real comfort advantage in Punjab/Sindh summers |
| Where it fails | Out-of-plane wall collapse and corner separation in earthquakes; near-total loss of life risk in Zone 3/4 |

**Verdict:** cheapest and thermally best, but it is the system that killed people in the 2005 Kashmir earthquake. Acceptable only for a simple 1-2 storey rectangular house in Zone 1/2A. **Do not propose URM in Zone 2B, 3 or 4.**

#### System B — Confined Masonry (CM) — *the recommended default for Pakistani houses*

Masonry walls are still the primary gravity and lateral system, but each wall panel is **confined** on all four sides by small cast-in-place RC tie-columns and tie-beams. **Critical sequencing: the masonry wall is built FIRST, with toothed (indented) vertical edges, and the tie-column concrete is poured against it afterwards.** This is the opposite of an RCC frame with infill and it is what makes the system work — the concrete bonds into the toothing so wall and confinement act as one panel.

| Parameter | Value |
|---|---|
| Storeys | 1-3 (3 storeys requires full detailing + engineer check) |
| Wall thickness | 230 mm structural; 115 mm partitions only |
| Tie-column size | Wall thickness × 230 mm minimum (i.e. 230 × 230 mm typical) |
| Tie-column reinforcement | 4 – #4 (4 – 12 mm) longitudinal, ties #3 (10 mm) @ 150 mm c/c, closed to 100 mm c/c over top and bottom 450 mm |
| Tie-beam size | 230 × 230 mm minimum at each floor and roof level (may be combined with the slab band) |
| Tie-beam reinforcement | 4 – #4 (12 mm), ties #3 @ 150 mm c/c |
| Max spacing of tie-columns | **4.0 m**, or 1.5 × storey height, whichever is smaller |
| Mandatory tie-column locations | Every building corner; every wall intersection/T-junction; both sides of any opening wider than 1.2 m; free wall ends |
| Panel aspect ratio | Panel length ≤ 1.5 × panel height; height / thickness ≤ 25 |
| Relative cost | **1.10 - 1.20× URM** |
| Speed | ~ URM plus 3-5 days per floor for tie-column/tie-beam pours |
| Where it fails | Poor toothing (smooth cold joint), tie-columns cast before the wall, tie-columns not continuous to foundation |

**Wall density check (the single most useful CM screening number).** Wall density index `d = (Σ cross-sectional area of structural walls in one direction) / (floor area of that storey)`, computed **separately for each orthogonal direction, for each storey**:

| Seismic demand | 1 storey | 2 storeys | 3 storeys |
|---|---|---|---|
| Low (PGA ≤ 0.10 g / Zone 1-2A) | ≥ 1.0 % | ≥ 1.5 % | ≥ 2.5 % |
| Moderate (0.10-0.20 g / Zone 2A-2B) | ≥ 1.5 % | ≥ 2.5 % | ≥ 3.5 % |
| High (0.20-0.32 g / Zone 3) | ≥ 2.5 % | ≥ 4.0 % | ≥ 5.5 % |
| Very high (> 0.32 g / Zone 4) | ≥ 3.5 % | ≥ 5.0 % | not recommended — use RCC frame |

Guideline values in the tradition of the Confined Masonry Network / Build Change guidance; treat as a screening filter, not a design. **If a plan fails wall density in either direction, the fix is more/longer walls in that direction or a switch to RCC frame — not thicker slabs.**

#### System C — RCC Moment Frame with Masonry Infill

Columns and beams carry everything; walls are non-structural infill built *after* the frame. Dominant in Karachi and increasingly common elsewhere.

| Parameter | Value |
|---|---|
| Storeys | Any (unlimited with proper lateral design); the only choice above 3 for a house |
| Typical column | 230 × 300 mm (G+0/G+1, low seismic) up to 300 × 450 mm (G+2, Zone 3/4) — see §7 |
| Typical beam | 230 × 380 mm to 300 × 530 mm for 4-6 m spans — see §6 |
| Typical slab | 125-150 mm solid two-way |
| Bay size | 3.5-5.0 m is the residential sweet spot; > 6 m starts driving beam depth hard |
| Relative cost | **1.30 - 1.55× URM** (grey structure) |
| Speed | 7-14 days per floor with traditional shuttering |
| Requires | Real supervision: cube tests, bar spacing, cover blocks, confinement ties at joints, vibration |
| Where it fails | Non-ductile detailing (no confinement in the beam-column joint); short-column effect from partial-height infill; soft storey at open ground floor; infill not isolated *or* not tied — the worst case is "half-attached" |

**Infill decision — pick one and detail it:**
1. **Isolated infill** — 20-25 mm gap at the top and sides of the panel, filled with compressible material, panel restrained out-of-plane by dowels/angles. Frame designed alone for lateral load. Honest and analysable.
2. **Integral infill** — panel tight to the frame, treated as a strut in analysis and confined. Stiffer, but changes period and force distribution.
   **Never build tight infill and analyse a bare frame.** That combination is the most common cause of unexpected torsion, short columns, and soft storeys in Pakistani RCC houses.

#### System D — Light Steel (Cold-Formed) Framing

| Parameter | Value |
|---|---|
| Studs | 89 mm (3.5") or 152 mm (6") C-sections, 0.84-1.37 mm gauge, @ 400 mm (16") or 600 mm (24") o.c. |
| Floors | C-joists 200-300 mm deep @ 400 mm o.c., span 3.5-5.5 m |
| Storeys | 1-3 |
| Speed | Very fast, dry, prefabricable |
| Weight | ~ 1/8 of masonry → *much* lower seismic force, but wind uplift becomes a real check |
| **Pakistan reality** | **Effectively no residential supply chain, no trained trades, no local code guidance, and a large cost premium. Not recommended for a Pakistani house unless the client has a specific reason and an imported system with its own engineering.** |

#### System E — Timber Platform Framing

| Parameter | Value |
|---|---|
| Studs | 2×4 @ 400 mm o.c. (1-2 storey walls); 2×6 @ 400 mm o.c. for taller/3-storey bearing walls — IRC 2021 §R602.3.1, Table R602.3(5) |
| Headers | Sized from IRC 2021 §R602.7, Tables R602.7(1)/(2) |
| Joists | 2×8 to 2×12 @ 400 mm o.c., spans 3.0-5.5 m |
| Sheathing | 12 mm OSB/plywood shear walls — excellent seismic performance per unit weight |
| **Pakistan reality** | **Structural-grade seasoned timber is scarce and expensive; termite and moisture exposure is severe; no local prescriptive code. Not recommended except for hill stations (Murree, Nathiagali, Swat, Gilgit) where a timber tradition exists — and there, the snow load check in §4.5 governs.** |

**Note on the IRC 2021 tables cited above:** IRC is a **US prescriptive residential code**. It is quoted here as a *model* for what prescriptive residential tables look like and as a fallback where no Pakistani equivalent exists. It is not adopted in Pakistan, its load basis is different, and its seismic/wind categories do not map onto BCP zones. Never present an IRC table as a Pakistani requirement.

### 1.3 House System Comparison Matrix

| Criterion | URM | Confined Masonry | RCC Frame | Light Steel | Timber |
|---|---|---|---|---|---|
| Max storeys (house) | 2 (3 in Zone 1/2A) | 3 | Any | 3 | 3 |
| Max economical clear span | 4.5 m | 5.0 m | 7.0 m | 5.5 m | 5.5 m |
| Relative grey-structure cost | 1.00× | 1.10-1.20× | 1.30-1.55× | 1.6-2.2× (PK) | 1.8-2.5× (PK) |
| Seismic performance | Poor | Good | Good *if ductile* | Very good | Very good |
| Structure self-weight | Very high | Very high | High | Very low | Very low |
| Plan flexibility (future) | Very low | Low | High | Medium | Medium |
| Vertical extension later | No | Only if designed for it | Yes if columns/footings sized for it | Limited | Limited |
| Supervision demand | Low | Medium | High | High | High |
| Thermal mass (summer comfort) | Excellent | Excellent | Good (infill) | Poor | Poor |
| Fire | Inherent | Inherent | Inherent (cover) | Needs protection | Charring/encapsulation |
| Availability of trades in PK | Universal | Common | Common | Rare | Rare |
| Foundation load intensity | High → wider footings | High | Concentrated at pads | Low | Low |
| **Default recommendation** | Zone 1/2A only | **Default for 1-3 storey PK house** | Long spans, soft storey, basement, 4+ | No | Hill stations only |

### 1.4 Hybrid Systems — Confined Masonry Wing + RCC Frame Bay

This is the most common *real* answer for a Pakistani house: the bedroom/service wing is CM, and one bay — drawing room, car porch, or a double-height lounge — is a frame. It is legitimate. It also fails in specific, predictable ways if the rules below are not followed.

```
Hybrid decision:
  Is the frame element ONE bay inserted into an otherwise masonry house?
    ├─ YES → follow rules 1-6 below. Acceptable.
    └─ NO — frame and masonry are interleaved across the plan
              → STOP. Make the whole house a frame. Interleaved
                dual systems on a house budget are not analysable
                to any useful accuracy and will not be detailed correctly on site.
```

1. **Stiffness truth.** A 230 mm masonry shear wall is one to two orders of magnitude stiffer in-plane than an RC frame of the same length. In a shared line, the wall takes essentially all the shear until it cracks, then dumps it into the frame suddenly. **Never assume the two share load in proportion to strength.**
2. **Separate the load paths in plan.** The CM wing resists lateral load in its own footprint; the frame bay resists in its own. Do not put a masonry shear wall and a frame in the *same* structural line and hope.
3. **Continuous diaphragm across the junction.** The slab must be cast monolithic across the CM/frame boundary, with a collector beam along the boundary line tying the frame beams into the masonry tie-beam ring.
4. **Match the foundation level and type at the junction.** A pad footing at 1.5 m next to a strip footing at 1.0 m across a 300 mm gap is a differential-settlement crack waiting to happen. Step them, or found both at the same level.
5. **The frame bay must be self-stable.** Design it as if the masonry wing were not there — because in a strong shake, after the masonry cracks, it briefly is not.
6. **Where the two blocks differ in height by a full storey**, do not hybridise — separate them with a **seismic joint of 50-100 mm** and treat them as two buildings (§14 movement joints).

---

## Section 2: Pakistan Code Context & Seismic Zoning

### 2.1 Which code governs

| Code | Status | Use for |
|---|---|---|
| **Building Code of Pakistan 2021 (BCP 2021)** | **Current governing code** since end-2021; IBC/ASCE-lineage | The code of record. It explicitly notes that BCP 2007 *understated* seismicity in several regions — so never use a BCP 2007 zone as a justification for a *lower* force. |
| **BCP-SP 2007** (Seismic Provisions) | Superseded but still the widely-known reference; derived from **UBC-97** | Method (Equivalent Lateral Force), ductile detailing philosophy, and the zone map most practitioners still quote |
| **BCP 2016 (Fire Safety Provisions)** | Current | Fire, egress — not structural |
| **ACI 318-19** | Cross-reference | RC member design, minimum thicknesses (Tables 7.3.1.1, 9.3.1.1, 8.3.1.1), deflection limits (§24.2, Table 24.2.2), cover (Table 20.5.1.3), seismic detailing (Ch. 18) |
| **ASCE 7-22** | Cross-reference | Load combinations (Ch. 2), live loads (Table 4.3-1), snow (Ch. 7), wind (Ch. 26-28), seismic ELF (§12.8) |
| **TMS 402/602-22** | Cross-reference | Masonry design; the first mainstream US standard with explicit **confined masonry** provisions |
| **IRC 2021** | Cross-reference only | A *model* for prescriptive residential tables (Ch. 4 Foundations, Ch. 6 Walls, Table R507.3.1 footings). **US code — never apply directly in Pakistan without adaptation.** |
| **UBC-97** | Historical | Basis of BCP-SP 2007; source of the Z / Ca / Cv / R tables reproduced in §10 |
| **IS 456 / IS 1905** | Regional cross-reference | Sometimes used in Pakistani practice for RC and masonry working-stress checks; not a governing code here |
| **Local byelaws** | Mandatory, separate | LDA / CDA / RDA / SBCA / PDA / TMA / Cantt — setbacks, height, covered area, FAR, staircase width, ventilation |

### 2.2 BCP-SP 2007 Seismic Zones

BCP-SP 2007 divides Pakistan into **five zones by Peak Ground Acceleration at a rock site (Vs30 = 760 m/s)**, from a hazard map at **10 % probability of exceedance in 50 years (~475-year return period)**. Design method: **Equivalent Lateral Force (ELF)**, with heavy emphasis on ductile detailing of RC members.

| Zone | PGA range (g) | UBC-97 equivalent zone factor Z | Character |
|---|---|---|---|
| 1 | 0.05 - 0.08 | 0.075 | Low |
| 2A | 0.08 - 0.16 | 0.15 | Moderate |
| 2B | 0.16 - 0.24 | 0.20 | Moderately high |
| 3 | 0.24 - 0.32 | 0.30 | High |
| 4 | > 0.32 | 0.40 | Very high (near-fault) |

**Commonly cited city assignments — VERIFY against the current BCP 2021 map before any real use:**

| City | Commonly cited zone |
|---|---|
| Lahore, Faisalabad, Multan, Sahiwal, Bahawalpur | 2A |
| Karachi, Hyderabad | 2B (Karachi coastal strip commonly cited 2B) |
| Islamabad, Rawalpindi | 2B |
| Peshawar, Mardan, Abbottabad | 2B |
| Quetta, Ziarat, Chaman | 4 |
| Muzaffarabad, Balakot, Bagh | 4 |
| Gilgit, Chitral, Skardu | 3-4 |
| Murree, Swat, Mansehra | 3 |

**Honest gap:** the per-zone PGA bands above are the published ranges; the *exact* BCP-SP 2007 per-zone numeric table and per-city assignment must be read off the actual BCP-SP 2007 / BCP 2021 hazard map (available via PEC, or Fawad Najam's BCP archive at fawadnajam.com/bcp). Never assign a zone from memory in a real project.

### 2.3 The BCP 2021 / ASCE 7-22 route (spectral parameters, not zone factors)

BCP 2021 moves away from the UBC-97 single zone factor `Z` toward the modern IBC/ASCE-style **spectral acceleration** framework. If the engineer is working in that framework — or if you are cross-checking with ASCE 7-22 — the path is:

```
1. Read Ss (short-period, 0.2 s) and S1 (1 s) spectral accelerations from the hazard map
2. Determine Site Class (A-F) from Vs30 / SPT-N / Su.  Default when unknown: Site Class D
3. Site coefficients Fa, Fv  → ASCE 7-22 Tables 11.4-1 / 11.4-2
4. SMS = Fa·Ss     SM1 = Fv·S1
5. SDS = (2/3)·SMS   SD1 = (2/3)·SM1
6. Seismic Design Category (SDC) from SDS, SD1 and Risk Category — Tables 11.6-1 / 11.6-2
7. Cs   = SDS / (R/Ie)
   Cs,max = SD1 / ( T · (R/Ie) )        for T ≤ TL
   Cs,min = 0.044 · SDS · Ie  ≥ 0.01
   (S1 ≥ 0.6g adds Cs,min = 0.5·S1/(R/Ie))
8. V = Cs · W        then distribute:  Fx = V · wx·hx^k / Σ(wi·hi^k),  k = 1 for T ≤ 0.5 s
```

`T = Ct·hn^x`: **Ct = 0.0466, x = 0.9** for RC moment frames (SI, hn in m); **Ct = 0.0488, x = 0.75** for "all other structural systems" — which is where masonry and confined masonry sit.

For a 1-3 storey house `T` is always well under 0.5 s, so `k = 1`, `Ft = 0`, and **Cs,max almost never governs — the SDS-based `Cs` or the `Cs,min` floor does**. Practically this means the two routes (UBC-97 and ASCE 7-22) give a similar answer for a house: a base shear of roughly **8-20 % of W in Zone 2A-2B, 20-35 % of W in Zone 3-4**. If a calculation lands far outside that band for a house, something is wrong.

**Which route to use:** use whichever the engineer of record will use. Present the UBC-97/BCP-SP 2007 route (§10) as the default because it is what most Pakistani practitioners still quote, and note the ASCE route as the cross-check. **Never mix the two mid-calculation** — an ASCE `R` with a UBC `Ca` is meaningless.

### 2.4 Ductile detailing expectation

BCP-SP 2007's central message is not the force level — it is **detailing**. For any RC house in Zone 2B and above:
- Closed hoops with 135° seismic hooks, extension ≥ 6 d_b (≥ 75 mm), in columns and beams
- Confinement zone `lo` at each member end = max(depth of member, clear span/6, 450 mm), ties @ ≤ 100 mm within `lo` — ACI 318-19 §18.7.5
- **Joint confinement** — ties must continue *through* the beam-column joint. The single most-skipped item on Pakistani sites.
- Lap splices only in the middle half of the member, never at the joint face
- Strong-column / weak-beam: ΣMnc ≥ (6/5) ΣMnb — ACI 318-19 §18.7.3.2
- **Longitudinal steel ratio in columns detailed as special moment frames (Zone 2B and above): 0.01 ≤ ρ ≤ 0.06 — ACI 318-19 §18.7.4.1.** This tighter seismic limit governs over the general §10.6.1.1 range in §7.4 whenever ductile detailing applies.

Full rebar geometry, lap and development lengths belong to `architecture-concrete-reinforcement-detailing`; this skill only sets the member sizes that make that detailing physically fit.

---

## Section 3: Materials & Local Construction Spec

| Material | Local designation | Strength / property | Notes |
|---|---|---|---|
| Concrete (mass/PCC) | 1:4:8 | ~ 10 MPa (1500 psi) | Lean base under footings, 75-100 mm |
| Concrete (general RCC) | **1:2:4** | ~ 20 MPa (3000 psi) | Default for houses: slabs, beams, columns, footings |
| Concrete (higher grade) | 1:1.5:3 | ~ 27.5 MPa (4000 psi) | Zone 3/4 frames, heavily loaded columns, water tanks |
| Reinforcement | Grade 60 (ASTM A615) | fy = 420 MPa (60 ksi) | Default. Grade 40 (fy = 280 MPa) still sold — **if used, all ACI minimum-thickness values must be scaled**, see §5.1 |
| Brick (first class) | *awwal* | ≥ 12 MPa (1750 psi) compressive | Standard PK brick 9" × 4.5" × 3" (229 × 114 × 76 mm) |
| Concrete block (solid) | — | 7-10 MPa (1000-1500 psi) | Common in Karachi/Balochistan |
| Mortar (load-bearing walls) | 1:4 or 1:6 cement:sand | — | **1:6 minimum for structural walls; never mud mortar in Zone 2B+** |
| Masonry prism strength f'm | — | 3-5 MPa (first-class brick, 1:6 mortar) | Governs the compressive check in §8.1 |
| Masonry shear strength v_m | — | 0.20-0.35 MPa | Working-stress allowable ~ 0.08-0.12 MPa |
| Brick masonry unit weight | — | 19 kN/m³ (plastered) | 230 mm plastered wall = 4.4 kN/m² of wall face |
| RCC unit weight | — | 24 kN/m³ | |
| Soil (for backfill/overburden) | — | 18 kN/m³ | |
| Water (for tank loads) | — | 10 kN/m³ | |

### 3.1 Concrete cover (ACI 318-19 Table 20.5.1.3)

| Condition | Cover |
|---|---|
| Concrete cast against and permanently in contact with ground (footings) | **75 mm** |
| Exposed to earth or weather, #6 (19 mm) bars and larger | 50 mm |
| Exposed to earth or weather, #5 (16 mm) and smaller | 40 mm |
| Not exposed — slabs, joists, walls | 20 mm |
| Not exposed — beams, columns (to ties) | 40 mm |

Cover is measured **to the outside of the tie/stirrup**, not to the main bar. On site, mandate cover blocks — "the mason will hold it up" is how slabs crack.

### 3.2 Standard house dimensional conventions (Pakistan)

| Item | Imperial | Metric |
|---|---|---|
| Structural exterior wall | 9" | 230 mm |
| Interior partition | 4.5" | 115 mm |
| Solid slab (short span) | 5" | 125 mm |
| Solid slab (typical) | 6" | 150 mm |
| Typical beam | 9" × 15" or 9" × 18" | 230 × 380 / 230 × 460 mm |
| Typical column | 9" × 12" or 12" × 12" | 230 × 300 / 300 × 300 mm |
| Floor-to-floor | 10'-6" to 11'-0" | 3200-3350 mm |
| Clear room height | 9'-0" to 10'-0" | 2750-3050 mm |
| Plinth above natural ground | 1'-6" to 2'-6" | 450-750 mm |
| Footing founding depth | 4'-0" to 5'-0" | 1200-1500 mm |
| Plot: 3 marla | 75 sq yd | 62.7 m² |
| Plot: 5 marla | 125 sq yd | 104.5 m² |
| Plot: 10 marla | 250 sq yd | 209 m² |
| Plot: 1 kanal | 500 sq yd | 418 m² |
| Plot: 2 kanal | 1000 sq yd | 836 m² |

---

## Section 4: Design Loads for a House

### 4.1 Dead loads (D)

| Item | Load |
|---|---|
| RCC solid slab, 100 mm | 2.40 kN/m² |
| RCC solid slab, 125 mm | 3.00 kN/m² |
| RCC solid slab, 150 mm | 3.60 kN/m² |
| RCC solid slab, 175 mm | 4.20 kN/m² |
| RCC solid slab, 200 mm | 4.80 kN/m² |
| Floor finish: 40 mm screed + 20 mm tile/marble | 1.20-1.50 kN/m² |
| Floor finish: 75 mm screed + marble (thick PK practice) | 1.80-2.00 kN/m² |
| Roof: mud phuska 100 mm + tile terracing + waterproofing | **2.00-2.50 kN/m²** (a big, frequently-forgotten load) |
| Roof: modern insulation + screed + membrane | 1.20-1.60 kN/m² |
| Plaster, both faces of a wall | included in 19 kN/m³ wall weight |
| 230 mm plastered brick wall | 4.40 kN/m² of wall face → **13.2 kN/m run at 3.0 m height** |
| 115 mm plastered brick wall | 2.30 kN/m² of wall face → **6.9 kN/m run at 3.0 m height** |
| 345 mm plastered brick wall | 6.60 kN/m² of wall face → 19.8 kN/m run at 3.0 m height |
| Suspended ceiling + services + fans | 0.25-0.40 kN/m² |
| Distributed allowance for internal partitions on a slab | 1.0-1.5 kN/m² (use only when partition positions are not yet fixed) |
| Overhead water tank (per m³ of water) | 10 kN/m³ — a 1000-gallon (4.5 m³) tank = **45 kN plus tank self-weight** |
| Staircase waist slab + steps (equivalent) | 6.0-7.5 kN/m² on plan |
| CGI sheet roof on purlins (sloped, hill station) | 0.15-0.25 kN/m² sheet + 0.15-0.30 purlins/truss |
| Clay tile roof on battens | 0.55-0.85 kN/m² |

### 4.2 Live loads (L) — ASCE 7-22 Table 4.3-1, consistent with BCP practice

| Space | kN/m² | psf |
|---|---|---|
| Residential rooms, bedrooms, lounges | **1.92** | 40 |
| Corridors and stairs within a dwelling | 1.92 | 40 |
| Kitchens / stores in a dwelling | 1.92-2.40 | 40-50 |
| Balconies and decks | **2.87** (1.5 × served area, capped 4.79) | 60 |
| Accessible flat roof (Pakistani roofs are *used* — charpai, drying, seating) | **1.92** | 40 |
| Non-accessible roof (roof live L_r) | 0.96 | 20 |
| Garage / car porch slab | 1.92 uniform, plus 13.3 kN concentrated | 40 + 3000 lb |
| Servant quarter / storage | 2.40 | 50 |
| Guardrail / handrail | 0.73 kN/m or 0.89 kN point | 50 plf / 200 lb |

**Local reality note:** design the main roof of a Pakistani house for **1.92 kN/m² accessible live load**, not 0.96. The roof will be occupied.

**Live load reduction** (ASCE 7-22 §4.7): `L = L0 (0.25 + 4.57/√(KLL·AT))` in SI. For a house it is essentially never worth applying — the tributary areas are small and `KLL·AT` rarely reaches the 37 m² threshold. Ignore it and take the small conservatism.

### 4.3 The tributary-area load take-down method

This is the procedure behind every column and footing number in this skill. Run it explicitly whenever a user asks "will this column/wall/footing work".

```
STEP 1 — Draw the tributary area
   • Interior column: half the span to each neighbouring column, all four sides
       AT = (L1/2 + L2/2) × (B1/2 + B2/2)
   • Edge column: half-span inward, to the slab edge outward
   • Corner column: quarter of one bay, roughly
   • Load-bearing wall: half the slab span on each side that bears on it, per metre run
       w = (span_left/2 + span_right/2) × (D + L)   [kN per metre of wall]

STEP 2 — Total the AREA loads at each level
   Floor:  D = slab + finishes + partitions(+ceiling/services)
           L = 1.92 kN/m²
   Roof:   D = slab + phuska/insulation + waterproofing
           L = 1.92 kN/m² (accessible)

STEP 3 — Add LINE and POINT loads that sit on the element
   • Wall directly over the column line or on the slab strip
   • Beam self-weight (b × h × 24 kN/m³) if not already in the slab figure
   • Water tank, AC condenser platform, parapet over the line

STEP 4 — Add the element's OWN weight, per storey
   Column:  b × h × storey height × 24 kN/m³
   Wall:    t × storey height × 19 kN/m³ (plastered)

STEP 5 — Accumulate DOWNWARD, storey by storey
   P_base = Σ over all levels above

STEP 6 — Produce BOTH numbers, and label them
   Pu (FACTORED, ASCE 7-22 §2.3)  → for concrete member strength (column, beam, slab)
   P  (SERVICE, ASCE 7-22 §2.4)   → for SOIL BEARING and masonry working stress
   Mixing these up is the single most common hand-calc error in house sizing.
```

**Sanity check on the result:** for a normal Pakistani house, factored floor load `wu` lands at **10-13 kN/m²** and roof at **9-11 kN/m²**. Per storey per column, a 16 m² tributary gives **~160-190 kN factored**. If your number is 3× that, you have double-counted; if it is a third of that, you have forgotten the finishes or the walls.

### 4.4 Load combinations (ASCE 7-22 §2.3, LRFD)

```
1.  1.4 D
2.  1.2 D + 1.6 L + 0.5 (Lr or S or R)
3.  1.2 D + 1.6 (Lr or S or R) + (1.0 L or 0.5 W)
4.  1.2 D + 1.0 W + 1.0 L + 0.5 (Lr or S or R)
5.  1.2 D + 1.0 E + 1.0 L + 0.2 S
6.  0.9 D + 1.0 W
7.  0.9 D + 1.0 E              ← governs overturning / footing uplift
```

Service (ASD) combinations, ASCE 7-22 §2.4 — **use these for soil bearing and for masonry working-stress checks**:

```
a.  D
b.  D + L
c.  D + (Lr or S or R)
d.  D + 0.75L + 0.75(Lr or S or R)
e.  D + (0.6W or 0.7E)
f.  D + 0.75L + 0.75(0.6W) + 0.75(Lr or S or R)
g.  0.6D + 0.6W
h.  0.6D + 0.7E
```

**Soil bearing capacity is always checked against SERVICE loads, never factored loads.** Concrete member strength is always checked against FACTORED loads. Write which one you used next to every number you produce.

### 4.5 Snow (S) — northern Pakistan only, but non-negotiable there

Houses in Murree, Nathiagali, Kaghan, Naran, Swat, Malam Jabba, Ziarat, Gilgit-Baltistan and Chitral carry real snow. Typical **ground snow loads of 1.0-3.0 kN/m² below 2000 m, rising steeply above** — and drifted loads far above that at valleys and against parapets.

- Read the ground snow load from the **BCP snow map** for the site elevation. Do not interpolate from memory.
- Flat roof snow load `pf = 0.7 · Ce · Ct · Is · pg` (ASCE 7-22 §7.3). For a house: `Is = 1.0` (Risk Cat II), `Ct = 1.0` (heated), `Ce = 0.9-1.2` depending on exposure and terrain.
- Sloped roof: `ps = Cs · pf`, with `Cs` reducing toward zero above ~30° on a slippery unobstructed surface (ASCE 7-22 §7.4).
- Flat RCC roofs in snow country accumulate; a sloped roof (≥ 30°) with a smooth surface sheds. **Design the slab for the *unshed* case anyway** — a roof that should shed will not, the one winter someone leaves a parapet or a solar frame on it.
- **Drift against a parapet or a taller adjoining wall can be 2-4× the balanced load.** ASCE 7-22 Ch. 7 gives the drift geometry method.
- **Unbalanced load** on a gable roof: the leeward side carries substantially more than the windward. Check the truss/rafter for the unbalanced case, not just the symmetric one.
- A 150 mm slab designed for a plains house (roof D+L ≈ 6.5 kN/m²) is **not** adequate for a Murree house with 2.5 kN/m² balanced snow plus 5 kN/m² drift at the parapet.

### 4.6 Loads that houses actually forget

| Forgotten load | Typical magnitude | Where it bites |
|---|---|---|
| Mud phuska / tile terracing on the roof | 2.0-2.5 kN/m² | Roof slab, every column below it |
| Thick marble bedding (75 mm screed) | 1.8-2.0 kN/m² | Floor slabs, especially in "luxury" specs |
| Overhead water tank | 45-90 kN point | Roof slab, the wall/column line under it, seismic mass at the top |
| Stair flight landing on a slab, not a beam | 6-7.5 kN/m² over the flight | The slab strip under the landing |
| Boundary/parapet wall on the roof edge | 0.5-1.0 kN/m run | Roof edge beam, cantilever back-span |
| Future second storey "we might add later" | Doubles column and footing load | Everything |
| AC outdoor units + solar array + frames on the roof | 0.3-0.6 kN/m² localised | Roof slab, parapet fixings, wind uplift on the array |
| Earth fill in a raised plinth / planter box | 18 kN/m³ | Plinth wall, retaining action, footing eccentricity |

---

## Section 5: Slab Systems for Houses

### 5.1 RCC Solid Slab (the default)

**One-way vs two-way — decide this first:**

```
ly = longer clear span,  lx = shorter clear span
   ly / lx  ≥ 2.0   →  ONE-WAY.   Main steel along lx only; distribution steel along ly.
   ly / lx  <  2.0  →  TWO-WAY.   Main steel BOTH ways; corners need torsion steel.
Supported on only TWO opposite edges (regardless of ratio) → ONE-WAY by definition.
```

Most Pakistani rooms (3.5 × 4.2 m, 3.0 × 4.5 m) are **two-way**. A long corridor or a verandah strip (1.8 × 6.0 m) is **one-way**. Getting this wrong doubles or halves the steel in the wrong direction.

**ACI 318-19 Table 7.3.1.1 — minimum thickness, one-way solid non-prestressed slabs** (h, no deflection check required):

| Support condition | Minimum h |
|---|---|
| Simply supported | ℓ / 20 |
| One end continuous | ℓ / 24 |
| Both ends continuous | ℓ / 28 |
| Cantilever | ℓ / 10 |

**ACI 318-19 Table 9.3.1.1 — minimum thickness, non-prestressed beams:** ℓ/16 (simply supported), ℓ/18.5 (one end continuous), ℓ/21 (both ends continuous), ℓ/8 (cantilever).

**fy modifier:** these values assume normalweight concrete and **fy = 420 MPa (Grade 60)**. For other grades multiply by `(0.4 + fy / 700)` in SI [ = `(0.4 + fy / 100,000)` with fy in psi ]. For **Grade 40 (fy = 280 MPa)**: factor = 0.4 + 280/700 = **0.80** → *thinner* minimum permitted by the table, but with more steel required for strength. In practice, keep the Grade 60 thickness and take the deflection margin.

**ACI 318-19 Table 8.3.1.1 — minimum thickness, two-way slabs without interior beams, fy = 420 MPa:**

| Panel | Without drop panels | With drop panels |
|---|---|---|
| Exterior, no edge beams | ℓn / 30 | ℓn / 33 |
| Exterior, with edge beams | ℓn / 33 | ℓn / 36 |
| Interior | ℓn / 33 | ℓn / 36 |
| **Absolute minimum h** | **125 mm** | **100 mm** |

Two-way slabs *with* beams on all four sides (the normal house case — masonry walls or RC beams on all edges) commonly go to ℓn/36 - ℓn/40 with the deflection check of ACI 318-19 §24.2.

**ACI 318-19 Table 24.2.2 — maximum permissible computed deflections:**

| Member and condition | Deflection considered | Limit |
|---|---|---|
| Flat roof, NOT supporting/attached to non-structural elements likely to be damaged | Immediate, due to L_r / S / R | ℓ / 180 |
| Floor, NOT supporting/attached to elements likely to be damaged | Immediate, due to L | ℓ / 360 |
| Roof or floor supporting/attached to elements **likely** to be damaged | That part occurring after attachment (long-term + subsequent live) | **ℓ / 480** |
| Roof or floor supporting/attached to elements **not likely** to be damaged | Same | ℓ / 240 |

For a Pakistani house, **ℓ/480 is the one that matters** — a 4.5 m slab over a brick partition or a full-height glazed panel may deflect only 9 mm after the partition goes up, or the partition cracks. This, not strength, is why house slabs are as thick as they are.

Long-term multiplier: `λΔ = ξ / (1 + 50ρ')` with `ξ = 2.0` at 5 years (ACI 318-19 §24.2.4.1.1). With no compression steel, long-term deflection is **3× the immediate value**. Design accordingly.

**Practical residential slab thickness table (two-way, supported on four sides, Grade 60, 1:2:4 concrete, D+L ≈ 8-9 kN/m²):**

| Shorter clear span ℓn | Slab thickness | Imperial | Typical bottom steel (both ways) |
|---|---|---|---|
| ≤ 3.0 m | 100 mm | 4" | #3 (10 mm) @ 175 mm c/c |
| 3.0 - 3.6 m | 115 mm | 4.5" | #3 (10 mm) @ 150 mm c/c |
| 3.6 - 4.3 m | **125 mm** | **5"** | #3 (10 mm) @ 125 mm c/c |
| 4.3 - 5.0 m | **150 mm** | **6"** | #4 (12 mm) @ 150 mm c/c |
| 5.0 - 5.5 m | 175 mm | 7" | #4 (12 mm) @ 125 mm c/c |
| 5.5 - 6.0 m | 200 mm | 8" | #4 (12 mm) @ 100 mm c/c, or switch to beam-and-slab |

*Steel shown is an order-of-magnitude indication for modelling and quantity feel only — it is NOT a bar bending schedule and must be designed.*

Minimum slab steel (shrinkage/temperature), ACI 318-19 §24.4.3.2: **ρ = 0.0018** for Grade 60, **0.0020** for Grade 40 — with maximum spacing 5h or 450 mm. Flexural steel spacing in slabs: max 2h or 450 mm (§7.7.2.3).

**Top steel over supports.** A continuous slab has hogging moment over every internal wall/beam. Provide top steel over supports for at least **0.25-0.30 of the clear span each side**, area ≈ the bottom steel. The classic Pakistani site failure is a slab poured with only bottom mesh, cracking in a straight line over every internal wall within two years.

### 5.2 Waffle (Ribbed) Slab

Used in Pakistani houses mainly to achieve a large column-free drawing room or a basement without deep beams, and for an exposed decorative soffit.

| Parameter | Value |
|---|---|
| Economic span | 6-12 m (below 6 m a solid slab is simpler and cheaper) |
| Overall depth | span / 24 to span / 28 → 250-450 mm for house spans |
| Rib width | 100-150 mm |
| Rib spacing | 600-900 mm c/c (set by the mould) |
| Topping | 50-75 mm |
| Material saving vs solid slab of same span | **~ 30 % less concrete, ~ 20 % less reinforcement** |
| Formwork | Reusable moulds — economics depend on amortising over **up to ~50 pours**; on a single house you rent, you do not buy |
| Watch | Solid drop panel required around every column for punching shear; services must weave between ribs |

**Verdict for houses:** worth it only when there is a genuine 6 m+ column-free requirement, or when the soffit is exposed as a design feature. For a normal 3.5-4.5 m residential grid, a solid slab wins on cost, speed and simplicity.

### 5.3 Precast Slab (hollow-core / precast plank / double-tee)

Available commercially in Pakistan (Tameerkaro, TameerEasy and similar suppliers offer precast girders, slabs and double-tee products).

| Parameter | Value |
|---|---|
| Hollow-core plank | 150-400 mm deep × 1200 mm wide; spans 6-16 m; span/depth ≈ 30-40 |
| Double-tee | 400-800 mm deep × 2400 mm wide; spans 12-24 m (over-scaled for a house) |
| Construction time | **Dramatically faster** — one comparative study measured ~9 working days vs ~31 for cast-in-situ on the same scope |
| Cost | Highly supply-chain dependent. One study reported ~$26 k precast vs ~$99 k cast-in-situ for a comparable scope — **treat as project-specific, absolutely not a universal ratio.** Get a local quote. |
| Structural topping | 50-75 mm RC topping with mesh is normally required to form the diaphragm |
| **Diaphragm warning** | **Precast planks are not a diaphragm until they are tied together and to the walls.** In a seismic zone this is the critical detail: topping + mesh + edge tie beam + connection to every supporting wall. Untied precast planks in an earthquake behave like loose boards. |
| Watch | Crane access to the plot — a tight 5-marla urban plot with 20-foot street frontage may not admit the delivery/erection crane at all |

### 5.4 Other slab options seen in Pakistani houses

| System | What it is | Verdict |
|---|---|---|
| **Filler-slab / block-and-rib** | Hollow clay blocks or EPS between narrow ribs, topped with RC | Cheap, light, decent insulation; needs a reliable block supplier and careful rib steel. Reasonable for a 4-5 m span. |
| **Flat plate (no beams)** | Solid slab straight onto columns | Only worth it for a basement or a very clean soffit. **Punching shear at the columns governs and is unforgiving** — houses rarely need this. |
| **Composite steel deck** | Profiled steel sheet + concrete topping | No residential supply chain in PK. Skip. |
| **Jack-arch (historic)** | Brick arches between steel I-joists | Found in old houses. **Not a diaphragm, no seismic capacity.** If encountered in a retrofit, treat it as a hazard to be replaced or tied, not a system to be extended. |

### 5.5 Slab System Choice for a House

```
Clear span ≤ 4.5 m, walls on all sides       → solid two-way slab, 125-150 mm. DEFAULT.
Clear span 4.5-6.0 m                          → solid slab 150-200 mm, or slab + beams
Clear span 6-9 m, want flat soffit            → waffle slab, or RC beam grid
Need speed and crane access exists            → precast hollow-core + 50-75 mm topping
Basement / car porch with rooms over          → beam-and-slab RCC frame
Snow zone, sloped roof                        → sloped RCC slab or timber/steel truss + sheeting (§13)
Cost-critical and a block supplier exists     → filler-slab / block-and-rib
```

### 5.6 Span-to-Depth Quick Reference (residential range)

| Element | Span/depth | 3.5 m | 4.5 m | 5.5 m |
|---|---|---|---|---|
| One-way RC slab, both ends continuous | ℓ/28 | 125 mm | 160 mm | 195 mm |
| Two-way RC slab on four edges | ℓ/36 | 100 mm | 125 mm | 155 mm |
| RC beam, simply supported | ℓ/12 | 290 mm | 375 mm | 460 mm |
| RC beam, continuous | ℓ/15 | 235 mm | 300 mm | 365 mm |
| RC cantilever slab (balcony) | ℓ/10 | 1.2 m cant. → 120 mm | 1.5 m → 150 mm | 1.8 m → 180 mm |
| Waffle slab | ℓ/26 | — | — | 210 mm (uneconomic below 6 m) |
| Hollow-core precast plank | ℓ/32 | 110 mm | 140 mm | 175 mm |
| Timber joist (2×) | ℓ/18 | 195 mm (2×8) | 250 mm (2×10) | 305 mm (2×12) |
| Steel C-joist (cold-formed) | ℓ/20 | 175 mm | 225 mm | 275 mm |
| Timber/steel pitched truss (overall rise) | span/5 | 700 mm | 900 mm | 1100 mm |

---

## Section 6: Beam Sizing for Residential Spans

### 6.1 Rules of thumb

- **Metric:** depth `h ≈ span(m) × 60 to 65 mm`
- **Alternative:** `h = span / 12` (simply supported) to `span / 15` (continuous)
- **Imperial site rule:** *1 foot of span ≈ 1 inch of depth* (16 ft span → 16" deep beam)
- **Width:** `b ≈ h / 2.5` to `h / 3`, rounded to the wall thickness (230 mm or 300 mm) so the beam hides in the wall
- Effective span/depth ratios (rule of thumb, cross-check against ACI 318-19 Table 9.3.1.1): **cantilever 7, simply supported 20, continuous 26**
- **Effective span** (for these ratios) = clear span + effective depth, or centre-to-centre of supports, whichever is smaller

### 6.2 Preliminary beam depth table (RCC, residential loads)

| Clear span | Depth (imperial) | Depth (metric) | Typical section (b × h) |
|---|---|---|---|
| ≤ 3.0 m | 9" | 230 mm | **230 × 230 mm** (absolute minimum beam) |
| 3.0 - 4.0 m | 9-12" | 230-300 mm | 230 × 300 mm |
| 4.0 - 4.5 m | 12" | 300 mm | 230 × 300 mm |
| 5.0 m | 12-14" | 300-350 mm | 230 × 380 mm |
| 6.0 m | 14-15" | 350-380 mm | 230 × 460 mm |
| 7.0 m | 16-18" | 400-460 mm | 300 × 460 mm |
| 8.0 m | 18-20" | 460-500 mm | 300 × 530 mm |
| 9.0 m | 20-22" | 500-560 mm | 300 × 600 mm |
| 10.0 m | 24" | 600 mm | 350 × 600 mm |

Depths include the slab where the beam is cast monolithically (T-beam action) — quote the **total depth from top of slab**, which is what matters for FreeCAD and for the ceiling height.

**Adjust upward from this table when:**
- The beam is **simply supported** rather than continuous (+15-20 % depth)
- It carries a **wall above** its full length (a 3 m tall 230 mm wall adds 13 kN/m — often more than the slab)
- It carries a **point load** from a floating column, tank or transfer condition (**engineer it, do not table it**)
- It is a **cantilever** (use span/8 total, and the tension steel is at the TOP)
- It supports a **car porch / garage slab** with a 13.3 kN concentrated wheel load

### 6.3 Lintel beams (every opening)

| Opening width | Lintel depth | Bearing each side | Steel (indicative) |
|---|---|---|---|
| ≤ 1.0 m (door) | 115 mm | 230 mm | 2 – #3 bottom |
| 1.0 - 1.5 m (window) | 150 mm | 230 mm | 2 – #4 bottom |
| 1.5 - 2.1 m (main door, wide window) | 230 mm | 300 mm | 3 – #4 bottom, 2 – #3 top |
| 2.1 - 3.0 m (car porch shutter, sliding door) | 300 mm | 300 mm | designed beam, not a lintel |
| > 3.0 m | designed RC beam with columns/tie-columns each side |

**Rule:** in confined masonry, any opening wider than **1.2 m must have a tie-column on both sides**, full height, continuous to foundation.

**Load on a lintel** — the useful simplification: masonry above an opening arches, so the lintel carries only the **triangular wedge** of masonry within a 45-60° triangle above it (plus any slab/beam load landing inside that triangle). A lintel with 1.5 m of clear wall above it does *not* carry the whole wall. But if a slab, beam, or the wall above is interrupted within the triangle, the arching is broken and the full load comes down — that is when the "small" lintel cracks.

### 6.4 ACI 318-19 seismic beam limits (§18.6.2.1, special moment frames)

- Clear span `ℓn ≥ 4 d`
- Width `bw ≥ 0.3 h` and `bw ≥ 250 mm`
- Width `bw ≤` the **smaller of `(c2 + h)` and `(c1 + 1.5h)`**, where `c1` = column dimension parallel to the beam span, `c2` = column dimension transverse to the beam span, and `h` = beam depth — the beam may not simply be assumed to extend an arbitrary 1.5 × column depth past both faces of the column; check the smaller of the two limits, not just one

A 230 mm wide beam **fails** the 250 mm minimum for a *special* moment frame. In Zone 3/4 residential RCC, use **300 mm minimum beam width**, and re-check that width against the smaller of the two limits above for the actual column size chosen — a wide beam on a narrow column can still fail even though it clears the 250 mm floor.

### 6.5 Deep-beam and hidden-beam warnings

- **Hidden (concealed) beam** — a beam the same depth as the slab, wide and shallow, used to keep a flat soffit. It is *extremely* inefficient: halving the depth quarters the stiffness. A 230 × 900 mm hidden beam is weaker and far more flexible than a 230 × 460 mm downstand. **Never propose one to span more than ~3.5 m, and never as a transfer element.** If the architecture demands a flat soffit over a long span, the answer is a thicker slab or a waffle, not a hidden beam.
- **Deep beam** (clear span / overall depth ≤ 4, ACI 318-19 §9.9): behaves as a strut-and-tie element, not a flexural one. Occurs in houses at short spandrel beams between closely spaced columns. Flag it to the engineer rather than sizing it from §6.2.
- **Beam landing on a beam:** avoid. If unavoidable, the supporting beam takes a large point load and needs designed hanger reinforcement at the junction — this is a detail masons never provide unless drawn.

---

## Section 7: Column Sizing for 1-3 Storey Houses

### 7.1 Preliminary axial sizing formula

For a short tied RC column with ρ ≈ 1 % steel, f'c = 20 MPa (1:2:4), fy = 420 MPa:

```
φPn,max = 0.65 × 0.80 × [ 0.85 f'c (Ag − Ast) + fy Ast ]
        ≈ 0.52 × [ 0.85 × 20 × 0.99 + 420 × 0.01 ] × Ag
        ≈ 10.9 MPa × Ag            (Ag in mm², result in N)

⇒  Ag ≥ Pu / 10.9      [Pu in N, Ag in mm²]
```

With f'c = 27.5 MPa (1:1.5:3) the coefficient rises to ≈ 14.3 MPa.

**This formula is pure axial.** Real columns carry moment too (frame action, unbalanced spans, lateral load). For a house, applying it and then rounding *up* to the §7.3 table sizes covers the moment adequately at preliminary stage — but say so.

### 7.2 Worked load take-down — interior column, 4.0 × 4.0 m tributary

```
FLOOR (typical):   D = slab 150 mm      3.60 kN/m²
                     + finishes         1.50
                     + partitions       2.00
                                       ------
                                 D =    7.10 kN/m²
                   L = 1.92 kN/m²
   wu = 1.2(7.10) + 1.6(1.92) = 8.52 + 3.07 =  11.59 kN/m²
   Per column per floor = 11.59 × 16 m² =        185 kN

ROOF:              D = slab 3.60 + mud phuska 2.20 = 5.80 kN/m²
                   L = 1.92 kN/m² (accessible)
   wu = 1.2(5.80) + 1.6(1.92) = 6.96 + 3.07 =    10.03 kN/m²
   Per column = 10.03 × 16 =                      160 kN

COLUMN SELF WEIGHT: 0.3 × 0.3 × 3.2 m × 24 × 1.2 ≈  8 kN per storey
```

| Building | Pu at base of ground-floor column | Required Ag = Pu/10.9 | Strength-only size | **Use (min. governs)** |
|---|---|---|---|---|
| G+0 (single storey, roof only) | 160 + 8 = **168 kN** | 15,400 mm² | 125 × 125 mm | **230 × 230 mm** |
| G+1 (one floor + roof) | 185 + 160 + 16 = **361 kN** | 33,100 mm² | 182 × 182 mm | **230 × 300 mm** |
| G+2 (two floors + roof) | 2(185) + 160 + 24 = **554 kN** | 50,800 mm² | 225 × 225 mm | **300 × 300 mm** |
| G+2, Zone 3/4, ductile frame | **554 kN** | 50,800 mm² | 225 × 225 mm | **300 × 380 mm** (ACI 318-19 §18.7.2.1 + confinement space) |

**The lesson to state out loud to any user:** for a normal house, **axial strength almost never governs the column size.** Minimum dimensions, ductile detailing space (you need room for 4-8 bars, 40 mm cover both ways, and 10 mm ties), buckling, and the width of the wall the column hides inside are what govern. Anyone who says "the calculation says 6 inches is enough" has calculated the wrong thing.

### 7.3 Column size quick table

| Storeys | Tributary area | Low seismic (Zone 1-2A) | Moderate (2B) | High (3-4) |
|---|---|---|---|---|
| G+0 | ≤ 12 m² | 230 × 230 mm (9"×9") | 230 × 300 | 300 × 300 |
| G+0 | 12-20 m² | 230 × 300 mm (9"×12") | 230 × 380 | 300 × 300 |
| G+1 | ≤ 12 m² | 230 × 300 | 300 × 300 | 300 × 300 |
| G+1 | 12-20 m² | 230 × 380 (9"×15") | 300 × 300 | 300 × 380 |
| G+1 | 20-28 m² | 300 × 300 (12"×12") | 300 × 380 | 300 × 450 |
| G+2 | ≤ 16 m² | 300 × 300 | 300 × 380 | 300 × 450 |
| G+2 | 16-25 m² | 300 × 380 (12"×15") | 300 × 450 | 380 × 450 |
| G+2 | 25-35 m² | 300 × 450 (12"×18") | 380 × 450 | 380 × 530 |

**Hard minimums:**
- ACI 318-19 §18.7.2.1 (special moment frames): least column dimension **≥ 300 mm**, and `least dimension / perpendicular dimension ≥ 0.4`
- Practical constructability minimum anywhere: **230 × 230 mm**
- Slenderness: keep `clear height / least dimension ≤ 12` for an unbraced column; a 3.2 m clear storey needs ≥ 270 mm least dimension on that criterion alone
- ACI 318-19 §6.2.5: slenderness may be neglected for a braced column when `k·ℓu / r ≤ 34 − 12(M1/M2) ≤ 40` (M1/M2 negative for single curvature, positive for double curvature — mind the sign, it moves the limit the other way for double-curvature columns); with `r ≈ 0.3h` for a rectangular section, a 300 mm column at 2.85 m clear, bent in single curvature with M1/M2 ≈ 0, gives `k·ℓu/r ≈ 32` — just inside, and only because it is braced

### 7.4 Indicative column reinforcement

| Column | Longitudinal | Ties |
|---|---|---|
| 230 × 230 | 4 – #4 (12 mm) | #3 (10 mm) @ 150 c/c, @ 100 in `lo` |
| 230 × 300 | 4 – #4 or 6 – #4 | #3 @ 150 c/c, @ 100 in `lo` |
| 300 × 300 | 4 – #5 (16 mm) or 8 – #4 | #3 @ 150 c/c, @ 100 in `lo` |
| 300 × 380 | 6 – #5 (16 mm) | #3 @ 150 c/c, @ 100 in `lo` |
| 300 × 450 | 8 – #5 (16 mm) | #3 @ 150 c/c, @ 100 in `lo` |
| 380 × 450 | 8 – #6 (19 mm) | #4 (12 mm) @ 150 c/c, @ 100 in `lo` |

**ρ limits — two different code provisions, do not mix them up:**
- **General (non-seismic) tied columns: 0.01 ≤ ρ ≤ 0.08 (ACI 318-19 §10.6.1.1).** This is the governing range for an ordinary column in Zone 1/2A with no special ductile detailing requirement.
- **Special moment-frame columns (Zone 2B and above, per §2.4 ductile detailing): 0.01 ≤ ρ ≤ 0.06 (ACI 318-19 §18.7.4.1).** This tighter seismic limit applies whenever the column is detailed as part of a ductile frame — which in practice means most Pakistani RCC houses, since Zone 2B is the default assumption once seismic detailing is invoked.
- In both cases, keep ρ ≤ 0.04 in practice where bars lap, or congestion makes the pour impossible — well inside either code ceiling.

`lo` = max(member depth, clear span/6, 450 mm) at each end. Tie spacing outside `lo`: ≤ 16 d_b (longitudinal), ≤ 48 d_b (tie), ≤ least column dimension — whichever is smallest.

### 7.5 Column grid layout for a house

| Guidance | Value |
|---|---|
| Residential sweet-spot bay | 3.5 - 5.0 m in both directions |
| Beyond which beam depth becomes intrusive | > 6.0 m |
| Column grid should align with | wall lines, so columns disappear inside 230 mm walls |
| Column projecting into a room | acceptable up to ~100 mm; beyond that, rotate the column or thicken the wall locally |
| Minimum columns for stability in one direction | **3** (two gives no redundancy and a hinge mechanism) |
| Grid regularity | keep the grid orthogonal and continuous floor-to-floor; every offset is a transfer element |
| Corner columns | most heavily stressed in seismic (biaxial moment + uplift). Upsize them, do not minimise them |

**Orient the column's long dimension** to match where the moment is: along the direction of the longer beam span, or along the direction with fewer shear walls. A 300 × 450 mm column turned the wrong way is 2.25× weaker about the axis that matters.

---

## Section 8: Masonry Wall Design Checks

Confined masonry is the recommended default for a Pakistani house, so the walls are the structure and deserve their own checks. Two things must be verified: **the wall can carry the gravity load (§8.1)**, and **the plan has enough wall to carry the earthquake (§1.2 wall density + §10.4 shear check)**. In practice the second almost always governs — but do both, because a 3-storey house on 230 mm walls can genuinely run out of compressive capacity.

### 8.1 Compressive stress and slenderness check (working stress)

```
STEP 1 — Actual compressive stress at the critical level (usually plinth)
   fa = P_service / (t × 1000)     [MPa, with P in N per metre run, t in mm]

STEP 2 — Basic permissible compressive stress from unit strength + mortar
STEP 3 — Multiply by the slenderness reduction factor ks
STEP 4 — Multiply by the eccentricity reduction factor ke
STEP 5 — Check   fa  ≤  f_basic × ks × ke
```

**Basic permissible compressive stress (working stress, indicative — IS 1905 tradition, consistent with Pakistani practice):**

| Brick crushing strength | 1:4 mortar (cement:sand) | 1:6 mortar | Mud mortar |
|---|---|---|---|
| 7.5 MPa (second class) | 0.60 MPa | 0.48 MPa | not permitted structurally |
| 10 MPa | 0.75 MPa | 0.60 MPa | not permitted structurally |
| **12.5 MPa (PK first class / awwal)** | **0.90 MPa** | **0.70 MPa** | not permitted structurally |
| 15 MPa | 1.05 MPa | 0.83 MPa | — |
| Solid concrete block, 10 MPa | 0.80 MPa | 0.65 MPa | — |

**Slenderness reduction factor ks** — where slenderness ratio `SR = effective height / thickness`:

| SR | 6 | 8 | 10 | 12 | 14 | 16 | 18 | 20 | 22 | 24 | 27 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| ks | 1.00 | 0.95 | 0.89 | 0.84 | 0.78 | 0.73 | 0.67 | 0.62 | 0.56 | 0.50 | 0.43 |

**Effective height** of a wall restrained top and bottom by a monolithic RC slab / tie-beam = **0.75 × storey height**. For a wall restrained at only one end, use 1.5 × height (and reconsider the design).

**Eccentricity reduction factor ke** — where `e` is the eccentricity of the load on the wall thickness:

| e/t | 0 | 1/24 | 1/12 | 1/8 | 1/6 (kern limit) | 1/4 |
|---|---|---|---|---|---|---|
| ke | 1.00 | 0.95 | 0.90 | 0.86 | **0.84** | 0.67 |

A slab bearing on **half** the wall thickness (very common — slab stops at the outer skin, or bears on a shelf) produces `e ≈ t/6` at minimum, so **use ke = 0.84 unless the load is genuinely centred**.

**Worked check — 2-storey CM house, ground-floor external wall, 230 mm, 1:6 mortar, first-class brick:**

```
Service load per metre run at plinth (from §12.3)      P = 65.4 kN/m = 65,400 N/m
Actual stress    fa = 65,400 / (230 × 1000)             = 0.284 MPa

Basic stress (12.5 MPa brick, 1:6 mortar)               = 0.70 MPa
Effective height = 0.75 × 3200                          = 2400 mm
SR = 2400 / 230 = 10.4                        → ks     ≈ 0.88
Slab bears eccentrically, e ≈ t/6             → ke      = 0.84

Permissible  = 0.70 × 0.88 × 0.84                       = 0.517 MPa

CHECK:  0.284 ≤ 0.517     →  OK, utilisation 55 %       ✓
```

**Same wall, 3-storey house** (add one more floor ≈ +34 kN/m → P ≈ 99 kN/m):

```
fa = 99,000 / 230,000 = 0.430 MPa   vs   0.517 MPa permissible
→ OK but utilisation 83 % — MARGINAL.
   Fixes: 1:4 mortar (basic 0.90 → permissible 0.665, utilisation 65 %)
          or 345 mm (13.5") ground-floor wall
          or reduce eccentricity by seating the slab centrally on a tie-beam
```

**The conclusion to state:** for 1-2 storeys, masonry gravity capacity is comfortable and the wall thickness is set by slenderness and buildability, not by crushing. **At 3 storeys the compressive check becomes real** — which is exactly why 3 storeys is the confined-masonry ceiling and why the ground floor of a 3-storey masonry house is often 345 mm.

### 8.2 Slenderness limits

| Condition | Max SR (effective height / thickness) |
|---|---|
| Unreinforced load-bearing wall, 1-2 storeys | 20 |
| Unreinforced load-bearing wall, with full engineering checks | 27 |
| Confined masonry panel (height/thickness) | **≤ 25** |
| Non-load-bearing partition (out-of-plane only) | 30 |
| Free-standing boundary wall (cantilever) | height ≤ 6 × thickness without piers |

A 230 mm wall at 3.2 m storey height, restrained both ends: `SR = 0.75 × 3200 / 230 = 10.4`. Comfortable. The same wall in a **double-height lounge** with no intermediate restraint: `SR = 0.75 × 6400 / 230 = 20.9` — **at the limit, and that is before any out-of-plane wind or seismic force.** Double-height masonry walls need intermediate tie-beams, pilasters, or an RC frame.

### 8.3 Pier and opening rules

| Rule | Value |
|---|---|
| Minimum pier width between two openings | **≥ 600 mm**, and ≥ 1/4 of the height of the taller adjacent opening |
| Minimum distance from an opening edge to a corner or tie-column | **≥ 600 mm**, or 1.5 × wall thickness |
| Total opening width in a wall, per storey | **≤ 50 %** of the wall length (≤ 40 % in Zone 3/4) |
| Vertical alignment | openings must stack floor to floor; a window over a solid pier over a door is a shear discontinuity |
| Opening > 1.2 m wide (CM) | **tie-column both sides**, full height, continuous to foundation |
| Sill band | 75 mm RC band under every window sill in Zone 3/4 — stops the diagonal crack from the sill corner |
| Opening within 600 mm of a slab soffit | treat the strip above as a coupling beam, not a wall |

### 8.4 Out-of-plane wall check (the one that kills people)

In-plane shear failure damages a building. **Out-of-plane wall collapse drops the floor and kills the occupants.** For any masonry house:

```
Out-of-plane force on a wall (simplified, ASCE 7-22 §12.11 style):
    Fp = 0.4 · SDS · Wp · (component amplification)     ≈ 0.4-1.2 kN/m² for houses in Zone 2A-4
    where Wp = wall weight per m² (4.4 kN/m² for a 230 mm plastered wall)

Wall spans VERTICALLY between the floor below and the floor/tie-beam above.
    M = Fp · h² / 8     per metre width
Unreinforced masonry has essentially NO reliable tensile capacity in this direction.
```

**Which is why the mitigations are geometric and connective, not analytical:**
1. **Tie the wall to the diaphragm at every floor level** — a continuous tie-beam cast monolithic with the slab, present at *every* level including the roof.
2. **Keep the unsupported height ≤ 25 × thickness** (§8.2).
3. **Confine every panel** on all four sides (§9 checklist) — the tie-columns halve the effective out-of-plane span by providing two-way action.
4. **Never leave a gable end or a parapet unrestrained.** Both are pure cantilevers with no floor above to hold them.
5. **Anchor a roof truss/rafter to the wall** with an embedded anchor into the tie-beam, not by resting it on the brickwork.

---

## Section 9: Confined Masonry Detailing Rules (the buildable checklist)

Because CM is the recommended default for a Pakistani house, these rules deserve their own section. Every one of them is a thing masons get wrong.

1. **Sequence: wall first, tie-column second.** Build the masonry panel full height with **toothed vertical edges** (alternate courses projecting ~50-60 mm into the tie-column zone), then place the tie-column cage and pour against the toothed face. A smooth vertical cold joint destroys the system.
2. **Tie-columns are continuous from footing to roof tie-beam.** Starter bars come out of the plinth beam / footing. A tie-column that starts at first-floor level is decoration.
3. **Tie-column at:** every external corner, every internal wall intersection (T and cross junctions), every free end of a wall, both sides of every opening > 1.2 m, and at intervals **≤ 4.0 m** or **≤ 1.5 × storey height** along any wall.
4. **Tie-beam at every floor level and at roof level**, continuous around the entire perimeter *and* along internal structural walls, forming a closed ring. It may be cast monolithically with the slab as a thickened band.
5. **Plinth beam is mandatory** in Zone 2B and above — 230 × 230 mm minimum, tying all footings, at plinth level, with 4 – #4 and #3 @ 150.
6. **Slab bears on the tie-beam**, not directly on brickwork, at every level where tie-beams exist.
7. **Wall panel geometry:** length ≤ 1.5 × height; height/thickness ≤ 25; minimum structural wall thickness 230 mm.
8. **Openings:** total width of openings ≤ 50 % of the wall length in that storey; nearest opening edge ≥ 600 mm (or 1.5 × wall thickness) from a corner or tie-column; vertically aligned floor to floor.
9. **Mortar 1:6 cement:sand minimum.** No mud mortar in any seismic zone.
10. **Wall density check (§1.2 table) in BOTH directions, on EVERY storey.** Walls must be reasonably symmetric in plan or the house will twist.
11. **Bricks soaked before laying; joints fully filled (10-12 mm); no more than 1.2 m of wall height built per day** — an unbraced fresh wall is a falling wall.
12. **115 mm partitions carry nothing.** They must not be shown supporting a slab, a beam, or a water tank in the model.
13. **Parapet walls must be confined too** — a 1.0 m unreinforced parapet on a roof edge is a projectile. Extend tie-columns up through the parapet and cap with a coping tie-beam.
14. **Horizontal reinforcement in the bed joints** (2 – 6 mm bars every 4th course, or a prefabricated ladder) is a cheap upgrade in Zone 3/4 — it holds the diagonal crack together after it forms.
15. **Do not cut chases in a structural wall for plumbing.** A 100 mm deep vertical chase in a 230 mm wall removes 43 % of its section. Route services in the 115 mm partitions or in a dedicated duct. If a chase is unavoidable, it must be shown on the drawing and checked.

### 9.1 The five site errors that void the system

| Error | What it looks like on site | Consequence |
|---|---|---|
| Tie-column poured **before** the wall | Smooth vertical concrete face, wall butted against it | Panel and confinement act independently → URM behaviour with extra cost |
| Tie-column stops at a floor | Bars cut off at slab level, no continuity | Load path broken; the confinement above is dead weight |
| No toothing | Straight, smooth masonry edge | Same as error 1 — no shear transfer across the joint |
| Tie-beam is a lintel band only | Ring beam present at the perimeter but not on internal walls | Diaphragm cannot deliver force to internal shear walls |
| Tie-column reinforcement lapped at the joint | Bar splice at the tie-beam intersection | Plastic hinge zone is the weakest point — exactly backwards |

---

## Section 10: Load Path — Roof to Soil

### 10.1 Gravity load path, by system

**Confined masonry / load-bearing masonry house:**
```
Roof finish (mud phuska, tiles, waterproofing)
  → RCC roof slab (two-way, spanning to all four walls)
    → roof tie-beam (ring beam)
      → masonry wall panel (in compression)  ← the primary vertical element
        + tie-columns (share axial load, confine the panel)
        → first-floor tie-beam
          → ground-floor masonry wall + tie-columns
            → plinth beam
              → strip footing under the wall (continuous)
                → bearing soil
```

**RCC frame house:**
```
Roof finish
  → RCC roof slab (two-way)
    → RC beams (edge + interior)
      → RC columns
        → next storey beams → columns … (repeat per storey)
          → plinth beam (ties column bases, carries ground-floor partition walls)
            → isolated pad footing under each column
              → bearing soil
                (infill walls carry their OWN weight only, into the beam below them)
```

**Sloped-roof (hill station) house:**
```
Roofing sheet / tile
  → battens / purlins  (spanning between trusses or rafters)
    → truss or rafter  (spanning wall to wall or to a ridge beam)
      → wall plate / RC tie-beam, ANCHORED to the wall (not resting on it)
        → masonry wall or RC column
          → … as above → footing → soil
   PLUS: horizontal thrust from a rafter pair must be resolved by a tie
         at the rafter feet, or the walls are pushed outward.
```

**Critical rule (unchanged from any building):** every element in the chain must be continuous. **A column on the first floor must have a column directly below it on the ground floor.** If it does not, you have created a *floating column* on a transfer beam — see §15.

### 10.2 Lateral load path

```
Wind pressure on wall face  /  Seismic inertia of the floor mass
  → out-of-plane bending of the wall or cladding, spanning vertically between floors
    → RCC slab acting as a rigid horizontal DIAPHRAGM at each level
      → in-plane shear transferred to the vertical lateral elements:
           • masonry walls parallel to the load (shear walls)  [CM/URM]
           • RC frames + any RC shear walls / stair core        [frame]
        → those elements act as vertical cantilevers over the building height
          → overturning moment + base shear delivered to the foundation
            → resisted by footing bearing pressure (moment) and
              base friction + passive earth pressure (shear)
              → soil
```

**Diaphragm rules for a house:**
- A cast-in-situ RC slab is a good diaphragm by default. A precast plank floor is **not** until topped and tied. A timber joist floor needs sheathing.
- A stair opening, a light well, or a double-height lounge void punches the diaphragm. Provide an RC edge/collector beam all around any opening larger than ~1/6 of the floor area.
- **Every wall must be tied to the diaphragm at every floor** — this is what stops out-of-plane collapse, the number-one killer in masonry buildings.
- A **sloped roof is not a diaphragm** unless it is a braced/sheathed plane or a concrete slab. A tiled roof on purlins needs a horizontal ceiling-level diaphragm or roof-plane bracing.

### 10.3 Load path continuity audit (run this on every model)

- [ ] Every column has a column directly beneath it at every level down to a footing
- [ ] Every tie-column runs unbroken from plinth beam to roof tie-beam
- [ ] Every beam lands on a column, a tie-column, or a structural wall — never on another beam if avoidable, and never on a 115 mm partition
- [ ] Every structural wall stacks over a structural wall below (not over a slab span)
- [ ] The overhead water tank sits over a wall line or a column line
- [ ] The staircase has its own defined support at both landings
- [ ] The diaphragm is continuous at each level, with collectors around every opening
- [ ] Cantilever back-spans are at least **2 × the cantilever length** and are held down by the floor above or by a wall
- [ ] Rafter/truss thrust is tied, not pushed into the wall head
- [ ] Nothing structural is chased, notched, or drilled through in the model

---

## Section 11: Lateral Loads — Seismic (BCP-SP 2007 / UBC-97 ELF)

### 11.1 The ELF equations (UBC-97, the basis of BCP-SP 2007)

```
Base shear:   V = ( Cv · I / ( R · T ) ) · W

Upper bound:  V ≤ ( 2.5 · Ca · I / R ) · W
Lower bound:  V ≥ 0.11 · Ca · I · W
Zone 4 extra: V ≥ ( 0.8 · Z · Nv · I / R ) · W

Period:       T = Ct · (hn)^0.75      [hn in metres]
              Ct = 0.0731  RC moment-resisting frame
              Ct = 0.0853  steel moment-resisting frame
              Ct = 0.0488  all other systems (masonry, shear-wall, confined masonry)

Vertical distribution:  Fx = ( V − Ft ) · wx·hx / Σ( wi·hi )
              Ft = 0 when T ≤ 0.7 s  (always true for a 1-3 storey house)
```

`W` = total dead load + 25 % of storage live load + permanent equipment + full weight of any water tank. For a house, `W ≈ Σ (D per floor × floor area)`, plus a partial live allowance if the roof is genuinely occupied.

For a 1-3 storey house `T` is always short (0.15-0.30 s), which means **the `2.5·Ca·I/R` cap essentially always governs**. In practice: `V ≈ 2.5·Ca·W/R`. Do the full calculation anyway so the governing branch is visible, but expect that answer.

### 11.2 Seismic coefficients Ca, Cv (UBC-97 Tables 16-Q, 16-R)

| Soil profile | Z=0.075 (Zone 1) | Z=0.15 (2A) | Z=0.20 (2B) | Z=0.30 (3) | Z=0.40 (4) |
|---|---|---|---|---|---|
| **Ca** | | | | | |
| S_B (rock) | 0.08 | 0.15 | 0.20 | 0.30 | 0.40 Na |
| S_C (very dense soil/soft rock) | 0.09 | 0.18 | 0.24 | 0.33 | 0.40 Na |
| S_D (stiff soil — **default if unknown**) | 0.12 | 0.22 | 0.28 | 0.36 | 0.44 Na |
| S_E (soft soil) | 0.19 | 0.30 | 0.34 | 0.36 | 0.36 Na |
| **Cv** | | | | | |
| S_B | 0.08 | 0.15 | 0.20 | 0.30 | 0.40 Nv |
| S_C | 0.13 | 0.25 | 0.32 | 0.45 | 0.56 Nv |
| S_D | 0.18 | 0.32 | 0.40 | 0.54 | 0.64 Nv |
| S_E | 0.26 | 0.50 | 0.64 | 0.84 | 0.96 Nv |

`Na`, `Nv` = near-source factors, applicable in Zone 4 only, based on distance to a known seismic source (1.0 at ≥ 10-15 km; up to 1.5-2.0 within 2 km). Muzaffarabad, Balakot and Quetta sites can be near-source — check.

**Soil profile types (UBC-97 Table 16-J), for picking the row above:**

| Type | Description | Vs30 (m/s) |
|---|---|---|
| S_A | Hard rock | > 1500 |
| S_B | Rock | 760 - 1500 |
| S_C | Very dense soil / soft rock | 360 - 760 |
| **S_D** | **Stiff soil — the Pakistani plains default when unknown** | 180 - 360 |
| S_E | Soft soil (> 3 m of soft clay) | < 180 |
| S_F | Site-specific evaluation required (liquefiable, peat, very high plasticity clay) | — |

### 11.3 Response modification factor R (UBC-97 Table 16-N)

| System | R |
|---|---|
| Bearing wall system — **reinforced masonry shear walls** | 4.5 |
| Bearing wall system — concrete shear walls | 4.5 |
| Bearing wall system — **unreinforced masonry** | not permitted in Zone 2B+; treat R = 1.5-2.0 where permitted |
| **Confined masonry** | **not tabulated in UBC-97.** Practice: use R ≈ 3.0-4.5, treated as reinforced masonry bearing wall. Confirm with the engineer; ASCE 7-22 likewise has no CM entry, and TMS 402-22 introduced CM provisions separately. |
| RC **ordinary** moment-resisting frame | 3.5 (not permitted in Zone 3/4) |
| RC **intermediate** moment-resisting frame | 5.5 (Zone 2 only) |
| RC **special** moment-resisting frame | 8.5 |
| Light-frame walls with wood structural panel shear panels | 5.5 |
| Light-frame walls with cold-formed steel + sheathing | 5.5 |

Importance factor `I` = **1.0** for a private house (Occupancy Category 4, standard occupancy).

**ASCE 7-22 cross-reference** (if working in the ASCE framework instead — see §2.3): `Cs = SDS / (R/Ie)`, `T = Ct·hn^x` with `Ct = 0.0488, x = 0.75` for "all other structural systems"; R from Table 12.2-1 (ordinary reinforced masonry shear walls R = 2, intermediate 3.5, special 5; special RC moment frame R = 8, intermediate 5, ordinary 3). **Note that ASCE's masonry R values are substantially lower than UBC-97's** — do not carry a UBC R into an ASCE calculation.

### 11.4 Worked example — G+1 confined masonry house, Lahore

```
GIVEN
  Location    Lahore → Zone 2A → Z = 0.15   (VERIFY against BCP 2021 map)
  Soil        S_D assumed (stiff alluvial silty clay) → Ca = 0.22, Cv = 0.32
  System      Confined masonry → R = 4.5 (treated as reinforced masonry bearing wall)
  Importance  I = 1.0
  Height      hn = 6.4 m (two storeys at 3.2 m)
  Covered area 150 m² per floor

PERIOD
  T = 0.0488 × (6.4)^0.75 = 0.0488 × 4.024 = 0.196 s

BASE SHEAR
  V = Cv·I / (R·T) · W = 0.32 / (4.5 × 0.196) · W = 0.363 W
  Cap:  2.5·Ca·I/R = 2.5 × 0.22 / 4.5           = 0.122 W   ← GOVERNS
  Min:  0.11·Ca·I  = 0.11 × 0.22                = 0.024 W
  ⇒  V = 0.122 W

SEISMIC WEIGHT W
  Per floor:  slab 3.60 + finishes 1.50 + walls (distributed) 3.00
              + 25% of live 0.48                     =  8.58 kN/m²
  Roof:       slab 3.60 + phuska 2.20 + parapet 0.50
              + 25% of live 0.48                     =  6.78 kN/m²
  W = 150 × 8.58  +  150 × 6.78 = 1287 + 1017        =  2304 kN

  V = 0.122 × 2304 =  281 kN

VERTICAL DISTRIBUTION  (Fx = V · wx·hx / Σ w·h)
  Level 1 (h=3.2 m): w·h = 1287 × 3.2 = 4118
  Roof   (h=6.4 m): w·h = 1017 × 6.4 = 6509
  Σ w·h = 10627
  F1   = 281 × 4118/10627 = 109 kN
  Froof= 281 × 6509/10627 = 172 kN

WALL SHEAR CHECK (ground storey, one direction)
  Storey shear at ground level = 281 kN
  Allowable masonry shear (working) ≈ 0.10 MPa on net wall area
  Required wall area = 281,000 N / 0.10 N/mm² = 2.81 × 10⁶ mm² = 2.81 m²
  With 230 mm walls: required wall LENGTH = 2.81 / 0.23 = 12.2 m in that direction

WALL DENSITY CHECK
  Provided walls in that direction, say 16 m of 230 mm wall = 3.68 m²
  d = 3.68 / 150 = 2.45 %
  Required (Zone 2A, 2 storeys, moderate) ≥ 2.5 %  →  MARGINAL — add wall or upgrade
```

**Reading of the result:** the house is *close* to the wall-density limit in that direction. The right responses are (a) lengthen or add a wall in the deficient direction, (b) move an opening to gain wall length, or (c) convert two tie-columns into real RC columns with a beam and treat that line as a frame. The **wrong** response is to thicken the slab or add steel to the slab — the slab is not the deficient element.

### 11.5 Same house, Zone 4 (Quetta / Muzaffarabad) — why the system changes

```
Z = 0.40, Soil S_D → Ca = 0.44 Na, Cv = 0.64 Nv.  Take Na = Nv = 1.0 (>15 km from source).
Confined masonry, R = 4.5:
  V ≤ 2.5 × 0.44 × 1.0 / 4.5 = 0.244 W    →  V = 0.244 × 2304 = 562 kN   (2× Lahore)
  Required wall area = 562,000 / 0.10 = 5.62 m²
  Required 230 mm wall LENGTH per direction = 24.4 m  (vs 12.2 m in Lahore)
  Wall density required (Zone 4, 2 storeys) = 5.0 %  → 7.5 m² of wall per 150 m² floor
  → 32.6 m of 230 mm wall per direction, per storey.

On a 150 m² floor plate that is roughly a wall every 4 m in BOTH directions,
with openings under 40 %. Possible for a compartmented plan; impossible for
an open-plan house with a big drawing room.

⇒ In Zone 4, an open-plan house is an RCC ductile frame. Confined masonry only
  survives the wall-density check if the plan is genuinely cellular.
```

### 11.6 Seismic irregularities that a house actually hits

| Irregularity | House version of it | What to do |
|---|---|---|
| **Soft/weak storey** (vertical) | Open ground floor for cars, solid above | Add shear walls / braced bay at ground; upsize + confine ground columns |
| **Torsional** (plan) | All the solid walls on one side (party wall on a corner plot), glazing on the other | Add stiffness on the open side; keep the centre of rigidity near the centre of mass |
| **Re-entrant corner** (plan) | L / T / U plan, very common on irregular plots | Seismic joint (50-100 mm), or heavy collector steel across the corner |
| **Diaphragm discontinuity** | Double-height lounge, large stair void, courtyard | Collector beams all round; check the diaphragm is not cut into two |
| **Out-of-plane offset** | Upper floor cantilevers or steps back off the wall line below | Avoid; if unavoidable, design the transfer element explicitly |
| **Mass irregularity** | Heavy roof (mud phuska + tanks + solar) on a light frame | Reduce roof dead load; move tanks over walls |
| **Setback** (vertical geometric) | Second floor much smaller than the first | Fine if the lateral system is continuous; check the discontinuity level |

Deep treatment: `architecture-seismic-design`.

---

## Section 12: Lateral Loads — Wind (ASCE 7-22)

### 12.1 Method

ASCE 7-22 basic wind speed `V` is a **3-second gust at 10 m (33 ft) above ground in Exposure C**, read from the Fig. 26.5-1 maps. **Risk Category II (a normal house) uses the 300-year MRI map, and there is NO separate importance factor** — the return period is baked into the map value (a change from pre-ASCE 7-16 editions where `I` was applied separately).

```
Velocity pressure:   qz = 0.613 · Kz · Kzt · Kd · Ke · V²     [N/m², V in m/s]

  Kz   exposure/height coefficient        ASCE 7-22 Table 26.10-1
  Kzt  topographic factor (hills, escarpments — matters in Murree/Islamabad foothills)  §26.8
  Kd   directionality factor = 0.85 for buildings   Table 26.6-1
  Ke   ground elevation factor (= 1.0 conservatively; < 1.0 at altitude)  §26.9

Design pressure (MWFRS, low-rise, Ch. 27 Directional):
  p = q·G·Cp − qi·(GCpi)
      G     = 0.85 (rigid building)
      Cp    = +0.8 windward, −0.5 to −0.2 leeward, −0.7 sidewall
      GCpi  = ±0.18 (enclosed), ±0.55 (partially enclosed)
```

**Kz at low heights:**

| Height | Exposure B (suburban/urban) | Exposure C (open) | Exposure D (coastal/flat) |
|---|---|---|---|
| 0-4.6 m | 0.57 | 0.85 | 1.03 |
| 6.1 m | 0.62 | 0.90 | 1.08 |
| 7.6 m | 0.66 | 0.94 | 1.12 |
| 9.1 m | 0.70 | 0.98 | 1.16 |
| 12.2 m | 0.76 | 1.04 | 1.22 |

**Exposure category (ASCE 7-22 §26.7):**

| Exposure | Definition | Pakistani examples |
|---|---|---|
| **B** | Urban/suburban, wooded, closely spaced obstructions ≥ 800 m upwind | Most city plots — Lahore DHA, Karachi Gulshan, Islamabad sectors |
| **C** | Open terrain, scattered obstructions < 9 m | Farmhouses, city-edge plots, open agricultural land, airport surrounds |
| **D** | Flat unobstructed, water surfaces upwind ≥ 1.6 km | Coastal Karachi facing the sea, large lake frontage |

**Enclosure classification** matters more than people expect. A house with large sliding doors that will be **open during a storm** — or that will blow in — is *partially enclosed*, and `GCpi = ±0.55` instead of ±0.18. That triples the internal pressure contribution and is the mechanism by which roofs come off.

### 12.2 Worked example — same G+1 house

```
GIVEN
  V   = 40 m/s (144 km/h) 3-s gust — INDICATIVE. Read the actual value from the
        BCP wind map / regional map for the site. Pakistan design gusts commonly
        fall in the 33-47 m/s (120-170 km/h) band.
  Exposure B (suburban plot), h = 6.4 m → Kz ≈ 0.62
  Kzt = 1.0, Kd = 0.85, Ke = 1.0

  qh = 0.613 × 0.62 × 1.0 × 0.85 × 1.0 × 40²
     = 0.613 × 0.62 × 0.85 × 1600 = 517 N/m² = 0.52 kPa

  Windward:  p = 0.52 × 0.85 × 0.8  = 0.35 kPa
  Leeward:   p = 0.52 × 0.85 × 0.5  = 0.22 kPa
  Net on projected face                = 0.57 kPa

  Projected face: 12.0 m wide × 6.4 m tall = 76.8 m²
  Total base shear from wind = 0.57 × 76.8 = 44 kN
```

### 12.3 The conclusion that matters

```
Seismic base shear (Zone 2A, confined masonry)  = 281 kN
Wind base shear   (V = 40 m/s, Exposure B)      =  44 kN
                                                  ─────────
SEISMIC GOVERNS by a factor of ~6.
```

**General rule for Pakistani houses:**
- **Masonry or RCC house (heavy) → seismic almost always governs the lateral design**, because base shear scales with mass.
- **Light steel or timber house → wind may govern**, and **wind UPLIFT on the roof becomes the critical check** (a light roof can be peeled off long before the walls fail in shear). Design roof-to-wall and wall-to-foundation hold-downs explicitly.
- **Exposed hilltop, escarpment, coastal Karachi, or a farmhouse in open country → recompute wind with the right Kzt and Exposure before assuming seismic governs.** `Kzt` on a sharp escarpment crest can reach 1.4-1.6, which is a **2× increase in pressure**.
- **Parapets, boundary walls, and roof-mounted water tanks are wind- and seismic-critical appendages** and get checked separately — free-standing unreinforced boundary walls are a classic collapse item in both wind storms and earthquakes.

### 12.4 Roof uplift — the check nobody does on a light roof

```
Net uplift on a roof plane (components & cladding, ASCE 7-22 Ch. 30):
    p = qh · [ (GCp) − (GCpi) ]
    Zone 1 (field):   GCp ≈ −0.9 to −1.1
    Zone 2 (edge):    GCp ≈ −1.4 to −1.8
    Zone 3 (corner):  GCp ≈ −2.0 to −2.8      ← 2-3× the field value
    plus internal (GCpi) = ±0.18 enclosed, ±0.55 partially enclosed

Worked, qh = 0.52 kPa, enclosed, corner zone GCp = −2.6:
    p = 0.52 × (−2.6 − 0.18) = −1.45 kPa uplift at the corner
CGI sheet roof dead load ≈ 0.4 kPa (sheet + purlins).
    Net uplift = 1.45 − 0.6×0.4 = 1.21 kPa  →  the roof leaves.
```

**Consequences for design:**
- A **heavy RCC roof slab** (3.6-6.0 kPa dead) never uplifts. This is one real advantage of the Pakistani flat-slab roof.
- A **CGI / tile roof on a hill station house** must have a continuous tie-down chain: sheet → purlin (screwed, not nailed) → truss → **anchor cast into the RC tie-beam** → wall → footing. Every link must be present, and the corner and edge fixings must be at closer spacing than the field.
- **Overhangs are the worst case** — pressure acts on both faces. Limit eaves overhang to ~600 mm unless it is specifically designed.
- **Solar arrays** add a large uplift-prone surface. Their fixings must go into the structure, not into the waterproofing screed.

---

## Section 13: Roof Structure — Flat and Sloped

### 13.1 Flat RCC roof (the plains default)

Structurally identical to a floor slab (§5), with three differences:

| Difference | Consequence |
|---|---|
| Carries **mud phuska / terracing** (2.0-2.5 kN/m²) | Add it to D before sizing. Frequently forgotten. |
| Must **fall to drain** at 1:80 to 1:100 minimum | Achieved in the screed, not by tilting the slab. Add the average screed weight. |
| Is **accessible** in Pakistan | Use L = 1.92 kN/m² (40 psf), not roof live load 0.96. |

Parapet: 900-1050 mm high, 230 mm, **confined** (tie-columns extended up at ≤ 3.0 m c/c, coping tie-beam). Waterproofing detailing: `architecture-roofing-waterproofing`.

### 13.2 Sloped roof — when and how

Required in snow country (Murree, Nathiagali, Kaghan, Swat, Gilgit) and used for aesthetics elsewhere.

| Roof covering | Minimum pitch | Notes |
|---|---|---|
| CGI / corrugated steel sheet | 1:6 (≈ 9.5°) | 1:4 (14°) preferred in snow/heavy rain |
| Standing-seam metal | 1:12 (≈ 5°) | |
| Clay/concrete tile | 20° | 25-30° in exposed locations |
| Slate / shingle | 20-25° | |
| **Snow shedding (any covering)** | **≥ 30°** | Below 30°, assume it accumulates and design for the full balanced load |
| RCC sloped slab | any | Behaves as a slab; above ~25° needs top shuttering to hold the pour |

### 13.3 Rafter, purlin and truss sizing (indicative)

| Element | Rule | Typical for a 6 m span house |
|---|---|---|
| Pitched truss overall rise | span / 5 | 1200 mm at 6 m span |
| Truss spacing (with purlins) | 2.4 - 3.6 m c/c | 3.0 m |
| Rafter spacing (no truss, rafter-and-ridge) | 400 - 600 mm c/c | 450 mm |
| Timber rafter depth | span / 18 to span / 20 | 4.0 m rafter → 2×8 (195 mm) |
| Purlin spacing | 1.2 - 1.5 m along the slope | 1.35 m |
| Timber purlin | 2×4 to 2×6 at 1.2-1.5 m | 2×6 at 1.35 m |
| Cold-formed steel purlin (C/Z) | 100-150 mm at 1.2-1.5 m | C150 × 1.6 mm |
| Steel truss member (angle) | L 50×50×5 to L 65×65×6 | web/chord depending |
| Ridge beam (if no ties) | designed beam — takes the whole rafter reaction | — |

### 13.4 The two things that go wrong on a sloped roof

1. **Rafter thrust pushes the walls out.** A pair of rafters meeting at a ridge with no tie at their feet is an arch: it delivers a *horizontal* thrust into the wall head. On a 30° roof carrying 2 kN/m², that thrust is roughly `H = wL²/(8·rise)` per metre — easily 3-6 kN/m outward on a masonry wall with no tensile capacity. **Fix:** a collar tie or ceiling joist at rafter-foot level, a proper truss (self-equilibrating), or a designed ridge beam so the rafters act as simple beams. **Never a rafter pair on an unrestrained masonry wall.**
2. **The roof is not anchored down.** See §12.4. A light roof in a wind zone must have a fixing chain into the tie-beam, and gable ends need bracing in the roof plane.

### 13.5 Gable walls

A masonry gable is a **triangular cantilever above the last floor diaphragm**, with nothing at its apex. It is one of the most common partial-collapse items in earthquakes and windstorms.

- **Confine it:** extend the tie-columns up into the gable and cast a **raking tie-beam along the underside of the roof slope**, connected to the roof structure.
- Or **replace it** with a light framed and clad gable (timber/steel studs + sheeting) sitting on the tie-beam.
- Never leave 2 m of unreinforced brick triangle above the eaves tie-beam.

---

## Section 14: Foundations for Houses

### 14.1 Selection

```
Soil investigation done? ──NO──► STOP. Get trial pits / SPT. Everything below is
                                  conditional on a real SBC value.
       │ YES
       ▼
SBC at founding depth?
  ├─ > 200 kPa (dense sand/gravel, stiff clay, weathered rock)
  │      → strip footing (walls) / isolated pad (columns). Minimum sizes govern.
  ├─ 100-200 kPa (medium-stiff clay, medium-dense sand) — the Punjab norm
  │      → strip footing / isolated pad, sized by calculation
  ├─ 50-100 kPa (soft clay, loose sand, filled ground)
  │      → footings get uneconomically wide and overlap → RAFT / MAT FOUNDATION,
  │        or ground improvement (compaction, replacement, lime/cement stabilisation)
  ├─ < 50 kPa (very soft clay, peat, uncontrolled fill, high water table)
  │      → raft with ground improvement, or short bored piles + pile cap.
  │        Do not put spread footings on this.
  └─ Expansive clay / high sulphate / collapsing loess (parts of Sindh, Balochistan,
     Potohar) → special measures: deepen below the active zone, sulphate-resisting
     cement, void formers, moisture barrier. Engineer-specific.
```

### 14.2 Presumed bearing capacities (indicative only — never a substitute for a site investigation)

| Soil / rock | Presumed SBC (kPa) |
|---|---|
| Strong igneous / metamorphic rock | 10,000+ |
| Strong limestone / sandstone | 2,000-10,000 |
| Weak rock (shale, mudstone, weathered) | 500-2,000 |
| Dense gravel / dense sand | 300-600 |
| Medium-dense sand | 100-300 |
| Loose sand | 50-100 (settlement-critical) |
| Stiff clay (Su > 150 kPa) | 150-300 |
| Firm clay (Su 75-150 kPa) | 75-150 |
| Soft clay (Su < 75 kPa) | 50-100 (settlement-critical) |
| Very soft clay / peat / uncontrolled fill | Not suitable for shallow foundations |

**Indicative regional character in Pakistan** (screening only — a site investigation always overrules):

| Region | Typical shallow profile | Indicative SBC at 1.2-1.5 m |
|---|---|---|
| Lahore / central Punjab | Alluvial silty clay, silty sand | 100-150 kPa |
| Islamabad / Rawalpindi / Potohar | Stiff clay, shale, gravelly | 150-250 kPa |
| Karachi (inland) | Stiff clay, weathered rock in places | 100-200 kPa |
| Karachi (coastal / reclaimed) | Soft marine clay, fill, high water table | 50-100 kPa — raft territory |
| Interior Sindh | Silt / fine sand, high water table | 75-150 kPa |
| Quetta valley | Silty clay, gravels | 100-200 kPa (and Zone 4 seismic) |
| Northern valleys | Boulders, glacial deposits, highly variable | Extremely variable — investigate |

A Pakistan-specific practitioner discussion of minimum SBC thresholds for strip foundations under double-storey residential buildings exists on sepakistan.com and is worth reading for local numeric practice; it does not replace a site investigation.

### 14.3 Strip footing (load-bearing / confined masonry walls)

**Worked example — 2-storey CM house, external wall:**

```
SERVICE load per metre run of wall (ASCE 7-22 §2.4: D + L)
  Roof:   (3.60 + 2.20 + 1.92) × 2.0 m tributary   = 15.4 kN/m
  Floor:  (3.60 + 1.50 + 1.92) × 2.0 m tributary   = 14.0 kN/m
  Wall self-weight: 0.23 m × 6.4 m × 19 kN/m³      = 28.0 kN/m
  Plinth beam + footing self-weight (allow)        =  8.0 kN/m
                                                     ───────────
                                              Total ≈ 65.4 kN/m
```

| SBC | Required width = 65.4/SBC | Use (rounded up, practical) | Imperial |
|---|---|---|---|
| 250 kPa | 0.26 m | **0.60 m** (minimum practical) | 2'-0" |
| 200 kPa | 0.33 m | 0.60 m | 2'-0" |
| 150 kPa | 0.44 m | **0.60 m** | 2'-0" |
| 100 kPa | 0.65 m | **0.75 m** | 2'-6" |
| 75 kPa | 0.87 m | **0.90 m** | 3'-0" |
| 50 kPa | 1.31 m | 1.35 m — **check for overlap with adjacent footings → raft** | 4'-6" |

**Same table for a 3-storey CM house** (add one floor ≈ +14 kN/m plus extra wall ≈ +20 kN/m → ≈ 99 kN/m):

| SBC | Required width = 99/SBC | Use | Imperial |
|---|---|---|---|
| 250 kPa | 0.40 m | 0.60 m | 2'-0" |
| 200 kPa | 0.50 m | 0.60 m | 2'-0" |
| 150 kPa | 0.66 m | **0.75 m** | 2'-6" |
| 100 kPa | 0.99 m | **1.05 m** | 3'-6" |
| 75 kPa | 1.32 m | 1.35 m — **overlap likely → raft** | 4'-6" |

Strip footing construction:
- **75-100 mm lean PCC (1:4:8) blinding** below
- Footing thickness 230-300 mm reinforced (or a stepped brick footing in low-load 1-storey URM: 3-4 offset courses of 57 mm each)
- Transverse steel #4 (12 mm) @ 150 mm, longitudinal #3 (10 mm) @ 225 mm — indicative
- **75 mm cover to earth face** (ACI 318-19 Table 20.5.1.3)
- Founding depth ≥ 1.2 m, and **below the frost line / active zone / any expansive-clay seasonal moisture zone**
- **Projection rule of thumb:** keep the footing projection each side ≤ the footing thickness, or the footing must be designed for flexure and one-way shear rather than treated as a rigid spread
- **Plinth beam** on top, tying the whole footing ring

### 14.4 Isolated / pad footing (RCC frame columns)

```
SERVICE column load (from §7.2, un-factored):
  G+1 interior column, 16 m² tributary
  Floor: (7.10 + 1.92) × 16 = 144 kN
  Roof:  (5.80 + 1.92) × 16 = 124 kN
  Column self weight          =  10 kN
                               ───────
                        P ≈    278 kN
```

| SBC | Required area = 278/SBC | Square footing | Imperial | Thickness |
|---|---|---|---|---|
| 250 kPa | 1.11 m² | 1.10 × 1.10 m | 3'-6" | 300 mm |
| 200 kPa | 1.39 m² | 1.20 × 1.20 m | 4'-0" | 300 mm |
| 150 kPa | 1.85 m² | 1.40 × 1.40 m | 4'-6" | 350 mm |
| 100 kPa | 2.78 m² | 1.70 × 1.70 m | 5'-6" | 400 mm |
| 75 kPa | 3.71 m² | 1.95 × 1.95 m | 6'-6" | 450 mm |
| 50 kPa | 5.56 m² | 2.40 × 2.40 m | 8'-0" | 500 mm — **check overlap → raft** |

Pad footing checks the engineer will run (know they exist, do not skip them in the narrative):
1. **Bearing pressure** ≤ SBC under service loads, including any moment (`p = P/A ± M/Z`; keep the whole base in compression, i.e. `e ≤ B/6`)
2. **One-way (beam) shear** at distance `d` from the column face
3. **Two-way (punching) shear** on the perimeter at `d/2` from the column face — this usually sets the thickness
4. **Flexure** at the column face → bottom steel both ways
5. **Development length** of the bottom bars past the critical section
6. **Overturning / uplift** under `0.9D + 1.0E` at corner columns of a frame in Zone 3/4

**When two pads nearly touch** (boundary column, close grid, weak soil): use a **combined footing** (rectangular or trapezoidal, sized so its centroid coincides with the resultant load), a **strap footing** (boundary pad tied by a rigid strap beam to the nearest internal pad, to resolve the eccentricity), or go to a raft. Do not simply overlap two pads and hope.

### 14.5 Raft / mat foundation

| Parameter | Value |
|---|---|
| When | SBC 50-100 kPa; highly variable soil; high water table; basement present; individual footings would cover > ~50 % of the plan area |
| Thickness (house scale) | 300-450 mm; 450-600 mm with thickened bands under column/wall lines |
| Reinforcement | Two-way mesh top and bottom, e.g. #4 (12 mm) @ 150 mm each way each face — indicative |
| Design bearing | Rafts are often designed to a **reduced allowable pressure with a factor of safety** — one documented case designed a mat for 50 kPa although the measured SBC was 110 kPa, giving FS ≈ 2 against a settlement-controlled criterion |
| Advantage | Bridges soft spots, spreads load, minimises differential settlement, doubles as the ground-floor slab and part of the waterproofing |
| Watch | Hydrostatic uplift where the water table is above the underside — 1 m of head = 10 kPa uplift; a 2 m submerged raft must resist 20 kPa net upward |

**Average bearing pressure sanity check for a house on a raft:** total building service weight ÷ raft area. A G+1 masonry house typically lands at **35-55 kPa**; a G+2 at **55-80 kPa**. If your number is far outside that, recheck the take-down.

### 14.6 Plinth beam (non-optional in seismic zones)

- Size: 230 × 230 mm minimum (230 × 300 mm for G+2), 4 – #4 with #3 ties @ 150 mm
- Runs on **every** load-bearing wall line and between **every** pair of column footings
- Purpose: ties all footings into one unit so they settle and shake together, carries the ground-floor wall, and stops the differential foundation movement that cracks masonry
- Set at plinth level, with the **DPC (damp proof course)** immediately above

### 14.7 Settlement limits to quote

| Criterion | Limit |
|---|---|
| Total settlement, isolated footings on sand | 25 mm |
| Total settlement, isolated footings on clay | 40 mm |
| Total settlement, raft | 50-75 mm |
| **Differential settlement between adjacent footings** | ≤ 20 mm |
| **Angular distortion (δ/L) — cracking of masonry walls** | **1/500** |
| Angular distortion — structural damage | 1/250 to 1/150 |
| Tilt visible to the eye | 1/250 |

Masonry is brittle: **1/500 angular distortion cracks it.** This is why the plinth beam and matched founding depths matter more in a masonry house than in a frame.

Full geotechnical treatment: `architecture-geotechnical-foundations`.

---

## Section 15: Stairs, Cantilevers, Parapets, Water Tanks

| Element | Rule |
|---|---|
| **Stair riser/tread** | Riser ≤ 190 mm, tread ≥ 254 mm (IRC 2021 §R311.7.5). Pakistani residential comfort: **riser 175 mm, tread 275 mm**. Check `2R + T = 600-650 mm`. |
| **Stair width** | ≥ 900 mm clear (IRC R311.7.1); 1050-1200 mm for a comfortable house; check the local byelaw — many require 1.0 m minimum |
| **Stair headroom** | ≥ 2030 mm (IRC R311.7.2); design to **2100 mm** |
| **Stair structure** | Waist slab 125-150 mm spanning between landings; landing beams at each end. **The staircase is a stiff diagonal element — in an RCC frame it attracts seismic force and can create a short-column condition on the adjacent columns.** Either isolate it or model it. |
| **Balcony cantilever** | Typical 1.2-1.8 m. Slab depth = cantilever / 10 (so 1.5 m → 150 mm). **Top steel** (tension is at the top — the classic site error is placing it at the bottom). Back-span ≥ 2 × cantilever, anchored by the floor/wall above. |
| **Chajja / sunshade** | 450-750 mm projection, 75-100 mm thick, cast monolithic with the lintel, top steel from the lintel |
| **Parapet** | 900-1050 mm high (byelaw-dependent). **Must be confined** — tie-columns extended up at ≤ 3.0 m centres, plus a coping tie-beam. An unreinforced 1 m parapet is the first thing to fall. |
| **Overhead water tank** | 500 gal = 2.3 m³ = 23 kN; 1000 gal = 4.5 m³ = 45 kN; 1500 gal = 6.8 m³ = 68 kN — **plus** the RC tank's own weight. Place it **directly over a wall line or column line**, never mid-span on a 125 mm slab. It is also a seismic mass at the highest point of the building — it amplifies the roof-level force. |
| **Underground tank / septic** | Keep the excavation outside the 1:2 load-spread cone from any footing, or design a retaining structure. A UG tank dug next to a strip footing after construction has undermined many houses. |
| **Boundary wall** | Free-standing 230 mm masonry wall > 1.5 m tall needs **piers at ≤ 3.0 m centres and a coping beam**, or it is a wind/seismic collapse hazard onto the street. |
| **Lift / dumbwaiter shaft** | An RC shaft is a very stiff shear wall — it attracts a large share of the base shear and shifts the centre of rigidity. Locate it centrally, or accept and design for the torsion. |
| **Roof solar array** | 0.15-0.30 kN/m² dead but a large uplift surface (§12.4). Fixings into the structure, not the screed. Check the added mass at roof level for seismic. |

---

## Section 16: Sanity-Check Ratios and Quantity Feel

Use these to smell-test a number, catch a factor-of-ten error, or give a client a rough feel. **They are not an estimate.** For real quantities and money, hand off to `architecture-cost-estimation-boq`.

### 16.1 Concrete and steel per unit of covered area (RCC frame or CM house, grey structure)

| Quantity | Typical range | Note |
|---|---|---|
| Concrete volume | **0.18 - 0.25 m³ per m² of covered area** | Slab alone is 0.125-0.15; the rest is beams, columns, footings |
| Reinforcement | **38 - 54 kg per m² of covered area** (≈ 3.5 - 5.0 kg/sqft) | The classic Pakistani thumb rule is "4 kg per sqft" |
| Steel as % of concrete volume | 1.0 - 1.5 % by volume | |
| Cement (1:2:4 concrete) | ~ 6.3 bags (50 kg) per m³ | ≈ 0.22 m³ loose cement per m³ concrete |
| Bricks in a 230 mm wall | ~ 13-14 bricks per sqft of wall face (≈ 145/m²) | Standard 9"×4.5"×3" brick |
| Bricks per m³ of brickwork | ~ 500 including waste | |

### 16.2 Reinforcement density by member (kg of steel per m³ of concrete)

| Member | kg/m³ |
|---|---|
| Solid slab (residential) | 70 - 100 |
| Beam (residential) | 110 - 180 |
| Column (residential) | 150 - 220 |
| Isolated footing | 50 - 90 |
| Strip footing | 40 - 70 |
| Raft | 90 - 130 |
| Staircase | 100 - 140 |
| Tie-column / tie-beam (CM) | 120 - 160 |
| Retaining wall | 90 - 130 |

If a member's steel comes out below the lower bound, the design is probably under-reinforced or the concrete is oversized. Above the upper bound, the member is too small and congestion will make it unbuildable.

### 16.3 Whole-building smell tests

| Check | Expected for a house |
|---|---|
| Service dead+live load per floor | 8 - 11 kN/m² |
| Factored load per floor | 10 - 13 kN/m² |
| Total building service weight, G+1, 150 m²/floor | 2,200 - 2,700 kN |
| Seismic base shear as a fraction of W | 8-20 % (Zone 2A-2B), 20-35 % (Zone 3-4) |
| Wind base shear as a fraction of seismic, heavy house | 10 - 25 % |
| Column axial at ground level, G+1, 16 m² tributary | 350 - 400 kN factored / 270 - 300 kN service |
| Wall load at plinth, G+1 external CM wall | 60 - 75 kN/m service |
| Raft average bearing pressure, G+1 | 35 - 55 kPa |
| Structural cost as % of total house cost (grey + finishes) | 25 - 40 % |

### 16.4 Cost — what this skill will and will not say

Relative multipliers only (§1.3): **URM 1.00× / CM 1.10-1.20× / RCC frame 1.30-1.55×** for grey structure. **This skill deliberately does not quote a rupees-per-square-foot number** — cement and steel prices in Pakistan move fast enough that any hard-coded rate is wrong within months. Get a current local contractor or quantity-surveyor rate, or use `architecture-cost-estimation-boq`.

---

## Section 17: Failure Modes and Anti-Patterns (house-specific)

| # | Anti-pattern | Why it fails | Fix |
|---|---|---|---|
| 1 | **Soft storey** — open ground floor for car parking, solid infill above | Stiffness discontinuity concentrates all drift in the ground storey; the classic pancake collapse | Add RC shear walls or braced bays at ground level; increase ground-storey column size and confinement; never rely on the infill above |
| 2 | **Floating / hanging column** — an upper column landing on a beam, not a column | Creates a transfer element with no redundancy; the beam becomes a key element | Continue the column to foundation, or design the transfer beam explicitly as a key element with enhanced robustness |
| 3 | **Short column** — partial-height infill or a mezzanine beam braces part of a column | The free length shortens, stiffness rises as 1/L³, shear demand spikes, brittle X-crack shear failure | Full-height infill with a gap, or full-height isolation joint, plus closely spaced ties over the whole clear height |
| 4 | **Slab supported on a 115 mm partition** | Partition is not designed as a bearing wall; punches or crushes | Either upgrade to a 230 mm wall with a footing under it, or beam the slab past it |
| 5 | **Tie-columns cast before the masonry** (CM built like a frame) | No toothing, smooth cold joint, panel and confinement do not act together | Enforce the sequence: wall with toothing first, then pour |
| 6 | **Openings too close to a corner** | The corner pier is too short to carry shear; corner separation | ≥ 600 mm from the corner, or put a tie-column there |
| 7 | **L / T / U-shaped plan with no joint** | Re-entrant corner concentrates stress; wings vibrate out of phase | Seismic separation joint (50-100 mm for a 2-storey), or heavy diaphragm reinforcement at the corner |
| 8 | **Unreinforced parapets, gables and boundary walls** | Cantilever with no reinforcement; falls outward onto people | Confine, cope, and pier them; raking tie-beam in gables |
| 9 | **Water tank placed mid-span / off a wall line** | 45+ kN point load on a slab designed for 8 kN/m²; plus a high seismic mass | Move over a wall/column line, or design a dedicated support frame |
| 10 | **Cantilever top steel placed at the bottom** | Tension face unreinforced → sudden collapse | Site supervision; chair bars; photograph before pour |
| 11 | **No plinth beam** | Footings settle independently; masonry cracks; no seismic tie | Plinth beam on every wall and between every footing pair |
| 12 | **Vertical extension later, without designing for it** | Existing columns and footings sized for G+1 now carry G+2; ~55 % overload | Decide the final storey count at day one and size columns/footings for it — the marginal cost at construction is small, the retrofit cost is enormous |
| 13 | **Precast planks with no topping/tie** | No diaphragm; planks separate in shaking | 50-75 mm topping with mesh + edge tie beam + connection to every support |
| 14 | **Excavating next to an existing footing** (UG tank, neighbour's basement) | Undermines the bearing wedge | Keep outside the 1:2 spread cone or underpin/shore |
| 15 | **Mud mortar or 1:8 mortar in structural walls** | Almost no shear or tensile bond capacity | 1:6 minimum, 1:4 preferred, for any load-bearing wall |
| 16 | **Ignoring snow in the north** | A plains-spec 150 mm slab under 2.5 kN/m² balanced + drift | Read the BCP snow map; design the roof for balanced + drift |
| 17 | **Hidden (concealed) beam spanning far** | Shallow wide beam has a fraction of the stiffness; sags and cracks the slab | Downstand beam, thicker slab, or waffle — never a long hidden beam |
| 18 | **Rafter pair with no tie at the feet** | Horizontal thrust pushes the masonry walls outward | Collar tie / ceiling joist, a true truss, or a ridge beam |
| 19 | **Vertical plumbing chase cut in a 230 mm structural wall** | Removes up to 40 % of the section, exactly where the shear is | Route in partitions or a duct; if unavoidable, show it on the drawing and check it |
| 20 | **No top steel over internal supports in a continuous slab** | Hogging moment is unreinforced; a straight crack over every internal wall | Top steel for 0.25-0.30 of the span each side of every support |
| 21 | **Different founding depths across the plan with no step detail** | Differential settlement; angular distortion > 1/500 cracks masonry | Match levels, or step at 1:2 max with the plinth beam continuous |
| 22 | **Ground floor filled and raised with uncompacted earth** | Floor slab settles, sinks away from the walls, services shear | Compact in ≤ 200 mm layers to spec, or suspend the ground floor slab |

### Movement and separation joints (house scale)

- **RC structures:** expansion joint every 45-60 m of continuous length. A house is almost always shorter than this — but a long boundary wall or a row of terraced units is not.
- **Seismic separation joints:** required where two building blocks of different height or stiffness abut. Width ≈ sum of the two blocks' expected drifts; for a 2-storey house block against a 3-storey block, **50-100 mm** is the practical range. Undersized joints cause pounding damage.
- **Settlement joints:** where a heavy block (tower/upper storeys) meets a light block (single-storey servant quarter, porch), and especially where founding depths differ.
- **Masonry crack-control joints:** vertical joints in long unbroken masonry runs > 8-10 m, especially in parapets and boundary walls.

---

## Section 18: Full Worked Example — 10-Marla G+1 House, Lahore

```
BRIEF
  Plot          10 marla = 250 sq yd = 209 m²   (approx 35' × 65' = 10.7 m × 19.8 m)
  Covered       ~150 m² per floor after setbacks
  Storeys       Ground + First (G+1), roof accessible, overhead tank on roof
  Location      Lahore  → Zone 2A (Z = 0.15) — VERIFY on the BCP 2021 map
  Soil          assume S_D, SBC 150 kPa at 1.5 m — CONDITIONAL on trial pits
  Largest room  Drawing room 5.5 m × 6.5 m; car porch 5.0 m clear

STEP 1 — SYSTEM
  Q1 storeys = 2                → masonry viable
  Q2 zone 2A                    → confined masonry acceptable
  Q3 largest span 6.5 m         → EXCEEDS the 5.0 m CM comfort limit
  Q6 car porch 5.0 m clear      → RCC frame trigger
  Q7 only ONE bay trips it      → HYBRID permitted under §1.4
  ⇒ HYBRID: confined masonry for the bedroom/service wing (spans ≤ 4.5 m),
    with an RCC frame bay inserted over the drawing room and car porch.
    Grid for the frame bay: 3 bays of ~3.3 m in one direction, 6.5 m clear
    in the other, carried on 300 × 450 mm columns and 300 × 530 mm beams.
    Per §1.4: collector beam along the CM/frame boundary; frame bay checked
    as self-stable; both foundations founded at 1.5 m.

STEP 2 — VERTICAL ELEMENTS
  CM wing:    230 mm structural walls, 115 mm partitions
              tie-columns 230 × 230 at all corners, junctions, free ends,
              and at ≤ 4.0 m along every wall
              tie-beams 230 × 230 at first-floor and roof level
  Frame bay:  columns 300 × 450 mm (from §7.3: G+1, ~21 m² tributary, Zone 2A)
              beams 300 × 530 mm over the 6.5 m span
                    (6.5 m × 65 mm ≈ 420 mm; round up for the porch's
                     concentrated live load and continuity → 530 mm total depth)
              porch beam over the 5.0 m opening: 300 × 460 mm

STEP 2b — MASONRY WALL COMPRESSIVE CHECK (§8.1)
  Ground-floor external CM wall, 230 mm, 1:6 mortar, first-class brick
  fa = 65.4 kN/m / 230 mm = 0.284 MPa
  Permissible = 0.70 × ks(0.88) × ke(0.84) = 0.517 MPa
  → utilisation 55 %.  OK.

STEP 3 — SLABS
  Rooms: check one-way vs two-way.  Bedroom 3.6 × 4.2 m → ly/lx = 1.17 → TWO-WAY.
  CM wing rooms, max clear span 4.2 m  →  125 mm (5") two-way solid slab
  Drawing room, 5.5 m × 6.5 m           →  175 mm (7") two-way slab on the RC beam grid
                                           (5500/36 = 153 mm; round to 175 for the
                                            6.5 m direction and roof accessibility)
  Deflection: 5500/480 = 11.5 mm allowable after partitions attach — the 175 mm
              depth is chosen for this, not for strength.
  Roof over both                        →  same as the floor below, plus 100 mm
                                           mud phuska (2.2 kN/m²) in the load case
  Top steel over every internal support, 0.3 × span each side.

STEP 4 — FLOOR-TO-FLOOR
  Clear height              2750 mm
  + slab                     175 mm
  + finishes (screed+tile)    75 mm
  + services/ceiling zone    150 mm  (fans, conduit, no ducting in a typical PK house)
  ────────────────────────────────
  Floor-to-floor            3150 mm  → adopt 3200 mm (10'-6")
  Building height hn = 2 × 3200 = 6400 mm

STEP 5 — SEISMIC (from §11.4)
  V = 0.122 W,  W = 2304 kN  →  V = 281 kN
  F_roof = 172 kN, F_1st = 109 kN
  Wall density check: 2.45 % provided vs 2.5 % required → MARGINAL
  ACTION: lengthen the rear wall by 1.2 m by narrowing a window, taking d to 2.63 %.

STEP 6 — WIND (from §12.2)
  V_wind = 44 kN  <<  V_seismic = 281 kN  →  seismic governs. Wind is checked
  separately for the parapet and the boundary wall only.
  Roof is a heavy RCC slab → no uplift check needed (§12.4).

STEP 7 — FOUNDATIONS  (SBC 150 kPa, founding at 1.5 m)
  CM walls, 65 kN/m service       → strip footing 0.60 m wide × 300 mm thick
  Frame columns, 278 kN service   → pad footing 1.40 × 1.40 m × 350 mm
  Corner column with uplift check under 0.9D + 1.0E → engineer to verify
  Plinth beam 230 × 300 mm on every wall line and between all pads
  75-100 mm lean PCC (1:4:8) blinding under all footings
  DPC at plinth level
  Founding levels MATCHED across the CM/frame boundary (§1.4 rule 4)

STEP 8 — APPENDAGES
  Roof tank 1000 gal (45 kN + tank ~15 kN = 60 kN) placed directly over the
  intersection of two 230 mm walls in the service wing. NOT over the drawing room slab.
  Parapet 1050 mm high, confined, tie-columns extended up at 3.0 m c/c, coping beam.
  Stair: waist slab 150 mm, riser 175 mm, tread 275 mm, width 1100 mm, headroom 2100 mm.
  Stair void: collector beam all round (§10.2 diaphragm rule).

STEP 9 — QUANTITY SANITY CHECK (§16)
  Covered area 300 m² total (2 floors)
  Concrete ≈ 0.22 × 300 = 66 m³        (in the 0.18-0.25 band ✓)
  Steel    ≈ 45 × 300   = 13.5 tonnes  (in the 38-54 kg/m² band ✓)

STEP 10 — OUTPUT STATUS
  ⚠ PRELIMINARY. Not construction-ready. Requires:
    • Geotechnical investigation to confirm SBC and founding depth
    • Confirmation of seismic zone from the current BCP 2021 map
    • Full analysis and design by a PEC-registered structural engineer
    • LDA plan approval (setbacks, height, covered area, FAR, staircase, ventilation)
```

---

## Section 19: FreeCAD Modelling Defaults

Use these when building the BIM model so the geometry is dimensionally plausible from the first pass. Pair with the `architecture-freecad-bim` skill for the Site/Building/Storey hierarchy and parametric openings.

| Parameter | Default value | Note |
|---|---|---|
| Structural external wall | **230 mm** | `Arch Wall` width; classify IfcWall |
| Internal partition | **115 mm** | non-structural; never supports a slab |
| Ground-floor wall of a 3-storey masonry house | 345 mm | from the §8.1 compressive check |
| Tie-column (CM) | 230 × 230 mm | model as a distinct object so it can be counted |
| RC column (frame) | 300 × 300 mm (G+1) / 300 × 450 mm (long span or G+2) | IfcColumn |
| Beam | 230 × 380 mm typical; 300 × 530 mm at 6-7 m spans | IfcBeam; quote **total depth from top of slab** |
| Tie-beam / ring beam | 230 × 230 mm at every floor and roof | IfcBeam; continuous closed ring |
| Slab | 125 mm (≤ 4.3 m) / 150 mm (4.3-5.0 m) / 175 mm (5-5.5 m) | IfcSlab |
| Plinth beam | 230 × 230 mm (G+1) / 230 × 300 mm (G+2) | at plinth level |
| Strip footing | 600 × 300 mm (SBC ≥ 150 kPa) | IfcFooting |
| Pad footing | 1400 × 1400 × 350 mm (G+1, SBC 150 kPa) | IfcFooting |
| Lean PCC blinding | 100 mm, projecting 75 mm beyond the footing | |
| Floor-to-floor | **3200 mm** | 10'-6" |
| Clear room height | **2750 mm** | 9'-0" |
| Plinth above natural ground | 600 mm | |
| Founding depth below NGL | 1500 mm | |
| Door opening | 900 × 2100 mm (rooms), 1050 × 2100 (main), 750 × 2100 (bath) | |
| Window opening | 1200 × 1350 mm sill at 900 mm | |
| Lintel over every opening | 150-230 mm deep, 230 mm bearing each side | model it — it drives the wall cut |
| Stair | riser 175, tread 275, width 1100, waist 150 | |
| Parapet | 1050 mm high × 230 mm | confined |
| Cantilever balcony | 1500 mm projection × 150 mm slab | back-span ≥ 3000 mm |
| Sloped roof pitch (snow) | 30° | trusses at 3.0 m, purlins at 1.35 m |
| Concrete cover (to tie/stirrup) | 20 mm slabs / 40 mm beams-columns / 75 mm footings | ACI 318-19 Table 20.5.1.3 |

**Modelling discipline:**
1. Model **tie-columns and RC columns as separate objects from walls**, so the load-path audit in §10.3 can be run visually and so quantities are meaningful.
2. Model every **lintel and plinth beam** — they are what make the wall cuts and the plinth line correct.
3. Model the **footings**, even schematically — a plan where two pad footings overlap is telling you to switch to a raft, and you will only see that in the model.
4. Never let a slab or beam land on a 115 mm wall in the model. If it does, the model is telling you the plan is wrong.
5. Model the **water tank as a real mass object** at its real position, so the load-path audit catches it sitting mid-span.
6. Keep openings **parametric** (Arch Window/Door Subtractions), not frozen boolean cuts, so the wall-density and opening-ratio checks can be re-run after a plan change.
7. Annotate the model or its README with the **assumed SBC, seismic zone, material grades, and the fact that it is preliminary**, so nobody downstream inherits invisible assumptions.
8. If an FEM run is performed (`mcp__freecad__run_fem_analysis`): record the load case, the boundary conditions, the material properties used, and state plainly that a converged result validates the *model*, not the *building*.

---

## Section 20: Handoff to the PEC-Registered Engineer

### What to give the engineer

- [ ] Architectural plans, elevations, sections — all floors, dimensioned
- [ ] Site plan with plot boundaries, setbacks, levels, neighbouring structures and their foundation depths
- [ ] **Geotechnical report** (trial pits / SPT boreholes) with SBC, water table, soil classification, any expansive/collapsing soil flags
- [ ] Confirmed **seismic zone** from the current governing map, and the site soil profile class
- [ ] Confirmed **basic wind speed**, exposure category, and any topographic condition
- [ ] Snow load, for northern sites
- [ ] Intended structural system and this skill's preliminary sizing — **clearly labelled as preliminary**
- [ ] Final storey count *including any planned future extension*
- [ ] Position and capacity of the overhead water tank, underground tank, and septic
- [ ] Non-negotiable architectural constraints (the clear spans, the column-free room, the porch width)
- [ ] Material grades intended (concrete mix, steel grade, brick class, mortar mix)
- [ ] Every assumption made in this skill's output, listed explicitly

### Coordination checklist (run before the model is called "done")

- [ ] Structural system chosen against the §1.1 decision tree, with the reason recorded
- [ ] Hybrid rules (§1.4) followed if CM and frame are mixed
- [ ] Seismic zone confirmed from the current map, not from memory
- [ ] Wall density checked in **both** directions on **every** storey (CM/URM)
- [ ] Masonry compressive + slenderness check done at plinth level (§8.1)
- [ ] Every wall panel within the height/thickness ≤ 25 limit, including double-height spaces
- [ ] One-way vs two-way decided for every slab panel (§5.1)
- [ ] Deflection limit ℓ/480 satisfied wherever masonry partitions or glazing sit on a slab
- [ ] Top steel over internal supports called out on continuous slabs
- [ ] Load path continuity audit (§10.3) passed — no floating columns, no slab on a 115 mm wall
- [ ] Every opening > 1.2 m has a tie-column or real column on both sides
- [ ] Every opening has a lintel with adequate bearing; pier widths ≥ 600 mm
- [ ] Plinth beam ring is complete
- [ ] Diaphragm is continuous; collectors around the stair void and any light well
- [ ] Soft-storey / short-column / re-entrant-corner / torsion conditions identified and resolved
- [ ] Water tank sits on a wall or column line
- [ ] Parapet, gable and boundary walls confined
- [ ] Cantilever back-spans ≥ 2 × cantilever, top steel called out
- [ ] Rafter thrust tied (sloped roof); roof anchored down (light roof)
- [ ] Footings sized from a real SBC, no two footings overlapping, founding levels matched
- [ ] Quantities pass the §16 sanity ratios
- [ ] Future vertical extension decided; if yes, columns and footings sized for the final storey count
- [ ] Snow checked (northern sites)
- [ ] Byelaw compliance flagged for the architect: setbacks, height, covered area, FAR, staircase, ventilation
- [ ] **Output labelled: "Preliminary — requires design and stamp by a PEC-registered structural engineer, and local authority approval, before construction."**

---

## Section 21: Known Gaps in This Skill (state these when relevant)

1. **Exact BCP-SP 2007 / BCP 2021 per-zone PGA table and per-city assignments** are not reproduced verbatim here — only the published 0.05 g to > 0.32 g band structure and commonly cited city zones. Pull the actual BCP-SP 2007 / BCP 2021 hazard map (PEC, or Fawad Najam's BCP archive at fawadnajam.com/bcp) before any real use.
2. **BCP 2021's own Ss / S1 spectral maps** are not reproduced. The ASCE-style route in §2.3 gives the *method*; the map values must come from the code itself.
3. **BCP wind speed map values by city** are not reproduced. The 33-47 m/s band used in §12.2 is indicative. Read the map.
4. **BCP snow map values by elevation** are not reproduced. Northern sites must read the map.
5. **Hard 2026 cost-per-sq-ft data for Pakistan** (grey structure rates for URM vs CM vs RCC frame) is not included — only *relative* multipliers (1.00× / 1.10-1.20× / 1.30-1.55×) and the quantity ratios in §16. Get a local quantity surveyor's or contractor's current rates; the market moves fast with cement and steel prices.
6. **Confined masonry has no R-factor in UBC-97 or ASCE 7-22 Table 12.2-1.** The R ≈ 3.0-4.5 used here is practice, not a tabulated code value. TMS 402-22 introduced confined masonry provisions separately; the engineer must decide.
7. **Masonry allowable stresses in §8.1** follow the IS 1905 working-stress tradition, which is common in Pakistani practice but is not a Pakistani code. TMS 402-22 strength design gives different (generally less conservative) numbers. Say which basis you used.
8. **Steel and timber residential framing in the Pakistani context** is thinly covered because the local supply chain and trade base barely exist. The IRC 2021 prescriptive tables cited are a US model, not directly applicable.
9. **All reinforcement quantities shown are indicative for feel and quantity estimating only.** No bar bending schedule in this skill is a bar bending schedule. Use `architecture-concrete-reinforcement-detailing` for real detailing.
10. **Liquefaction, slope stability, and retaining structures** are out of scope here — route to `architecture-geotechnical-foundations`. Coastal Karachi and riverine Sindh sites in particular need a liquefaction assessment that this skill does not provide.
11. **Retrofit and assessment of an existing house** is not covered. Evaluating a built structure is a different discipline from sizing a new one, and requires site inspection, material testing, and an engineer.
12. **Column reinforcement ratio limits cite two different ACI 318-19 provisions depending on ductility class** (§7.4: §10.6.1.1 general vs §18.7.4.1 seismic) — always state which one applies to the column being sized, since the two ceilings (0.08Ag vs 0.06Ag) are not interchangeable.
