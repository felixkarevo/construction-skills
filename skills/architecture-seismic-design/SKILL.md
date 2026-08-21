---
name: architecture-seismic-design
description: >
  Seismic design knowledge for residential buildings in Pakistan covering BCP SP:07
  seismic zoning and zone factors, both the UBC-94-style (Z·I·C/Rw) and UBC-97-style
  (Cv·I/R·T with Ca caps and near-source factors) base-shear procedures with worked
  examples, a synthesised house-scale seismic design category tier (the prescriptive
  layer BCP lacks), confined masonry and RCC frame ductile detailing schedules (tie
  columns, tie beams, hoops, 135 degree seismic hooks), wall-density and out-of-plane
  slenderness checks, soft-storey / torsion / short-column / re-entrant irregularity
  avoidance in house plans, diaphragms and Pakistani roof systems, foundations and
  liquefaction screening, non-structural hazards, timber-laced vernacular systems
  (dhajji dewari, bhatar), retrofit of existing unreinforced masonry houses, an honest
  base-isolation assessment, the real cost delta of seismic detailing, per-zone house
  spec sheets, and concrete do/don't rules distilled from real Pakistan earthquake
  damage patterns (1935 Quetta, 2005 Kashmir, 2013 Awaran, 2019 Mirpur). Includes
  FreeCAD modelling conventions and a runnable wall-density check script.
---

# Seismic Design for Houses (Pakistan-Focused)

Pakistan sits on the Indian–Eurasian collision boundary. The Chaman fault system (west), the Main
Boundary / Main Frontal Thrust belt (north), the Kashmir / Balakot–Bagh fault (northeast) and the
Makran subduction zone (south) put most of the country's population in moderate-to-very-high seismic
hazard. The 8 October 2005 Kashmir earthquake (Mw 7.6) killed an estimated **~87,000 people**, destroyed
**272,019 buildings**, damaged **182,886 more**, left **>3.5 million homeless**, and caused **>$5 billion**
in direct losses; **over 90% of surveyed engineered buildings** fell in EMS damage grades 4–5. That event
directly triggered the *Building Code of Pakistan — Seismic Provisions 2007 (BCP SP:07)*. The death toll,
not the property-damage figures, is the number that actually justifies every rule in this document — a
building code exists because ~87,000 people did not have to die that day, and the ones who did mostly died
of the same handful of preventable configuration and detailing failures catalogued in §15.

Almost none of those deaths were caused by exotic engineering problems. They were caused by heavy roofs
on weak walls, open ground storeys, short columns, asymmetric plans, missing ties, unfilled mortar
joints and 90° hooks. This skill turns those failure modes into numeric, checkable rules that can be
applied at concept-plan stage, argued with a client, encoded in a FreeCAD model, and handed to a
licensed engineer as a coherent design basis.

## Reality Check - Licensing & Liability

**This skill produces design aids and calculation guidance for planning and FreeCAD modelling ONLY.**

- Everything here — zone factors, base-shear arithmetic, wall-density tables, tie-column schedules,
  detailing rules, cost deltas — is a **preliminary design aid and a checking tool**, not a structural
  design.
- Any design intended for the **actual construction of a real occupied building MUST be reviewed,
  calculated, and stamped by a licensed structural engineer registered with the relevant authority** —
  in Pakistan a **PEC-registered (Pakistan Engineering Council) professional engineer** of the
  appropriate category; elsewhere the equivalent licensed PE / CEng / chartered structural engineer.
- The design MUST also go through **local authority plan approval** before construction: LDA (Lahore),
  CDA (Islamabad), RDA (Rawalpindi), KDA/SBCA (Karachi), PDA (Peshawar), GDA, the relevant
  TMA / Cantonment Board, or the AJK / GB authority, under that authority's building byelaws — which
  are separate from, additional to, and sometimes stricter than BCP.
- **Claude / Claude must never present FreeCAD output, wall-density numbers, base-shear values, rebar
  schedules, or any content derived from this skill as construction-ready.** They are inputs to a
  licensed engineer's work, nothing more. The only correct framing is: *"preliminary seismic basis for
  coordination — to be verified and stamped by a PEC-registered structural engineer."*
- **Say this unprompted.** If a user starts treating the output as final — asking for a bar-bending
  schedule "to give the mason", asking to skip the engineer, talking about pouring next week, asking to
  delete a wall "because the model still stands up", or sharing the model with a contractor — stop and
  state the licensing requirement in plain language *before* continuing. A seismic zone is precisely the
  case where an unstamped design kills people.
- **Never certify.** Do not produce anything resembling a stamped drawing, a structural stability
  certificate, a soil report, or an engineer's signature block. Do not put a PEC number on output.
- **Soil is never assumed.** Every soil-profile and foundation number here is conditional on a
  site-specific geotechnical investigation. "Assume SD / 150 kPa" is a modelling placeholder, never a
  design input.
- **Seismic zone is never guessed.** City→zone lists in this skill are indicative. Verify against the
  official BCP SP-2007 hazard map (or the authority's own submission form) for the exact plot. Near a
  zone boundary or a mapped active fault, **take the higher zone**.
- Post-2007 probabilistic seismic hazard studies argue the BCP 2007 map **underestimates** ground motion
  in several regions. **Zone assignment is a code floor, not a ceiling on real hazard.**
- Nothing is "earthquake-proof". The honest phrase is *"designed to reduce the risk of collapse in the
  design-level earthquake, subject to engineer review."*

---

## How To Use This Skill (order of operations)

```
1. Establish the hazard        → §1  (zone, Z, soil profile, I, near-source)
2. Pick the category & system  → §2  (HSC H1–H4, confined masonry vs RC frame)
3. Size the demand             → §3  (base shear both formulations, storey forces, drift)
4. Fix the CONFIGURATION       → §6  (irregularity — do this BEFORE any detailing)
5. Check wall density          → §5  (the single most useful house-scale check)
6. Detail the system           → §4 confined masonry  /  §7 RC frame
7. Tie it together             → §8 diaphragms/roof  ·  §9 foundations
8. Kill the cheap killers      → §10 non-structural
9. Encode & check the model    → §16 FreeCAD conventions + checklist
10. Hand off honestly          → §17 to the PEC engineer, with the flags listed
```

**Configuration beats calculation.** A regular, symmetric, well-tied house designed with rules of thumb
outperforms an irregular one with a sophisticated analysis. Spend the effort at step 4.

Companion skills: `architecture-structural-systems` (system choice, gravity sizing),
`architecture-concrete-reinforcement-detailing` (rebar, laps, cover, BBS),
`architecture-geotechnical-foundations` (SBC, settlement, liquefaction),
`architecture-building-codes-permits` (approval route, byelaws, stamping),
`architecture-cost-estimation-boq` (rates for the §14 quantity deltas),
`architecture-freecad-bim` (model hierarchy, parametric openings, FEM).

---

## Section 1: Pakistan Seismic Hazard & Zoning (BCP SP:07)

### 1.1 Zone table (BCP 2007 Seismic Provisions)

| Zone | Peak Ground Acceleration (PGA) | Zone factor **Z** | Hazard | Design posture for houses |
|---|---|---|---|---|
| 1   | 0.05 – 0.08 g | 0.075 | Low | Good-practice detailing; plinth + roof ties still required |
| 2A  | 0.08 – 0.16 g | 0.15  | Moderate | Confined masonry with full tie system |
| 2B  | 0.16 – 0.24 g | 0.20  | Moderate–high | Confined masonry; wall-density check mandatory |
| 3   | 0.24 – 0.32 g | 0.30  | High | Confined masonry or ductile RC frame; engineer mandatory |
| 4   | > 0.32 g      | 0.40  | Very high | Engineered design only; 1–2 storeys strongly preferred |

### 1.2 Indicative city → zone lookup (VERIFY against the official map)

| Zone | Indicative locations |
|---|---|
| 4 | Quetta, Ziarat, Chaman, Pishin, Muzaffarabad, Balakot, Bagh, Rawalakot, parts of Gilgit-Baltistan |
| 3 | Islamabad, Rawalpindi, Murree, Abbottabad, Mansehra, Peshawar, Mardan, Swat/Mingora, Chitral, Kohat, Mirpur (AJK), Gilgit, Skardu |
| 2B | Lahore, Sialkot, Gujranwala, Gujrat, Jhelum, Karachi, Hyderabad, Thatta, Gwadar / Makran coast |
| 2A | Multan, Faisalabad, Sargodha, Bahawalpur, Sukkur, Larkana, D.G. Khan |
| 1 | Parts of interior Sindh and Cholistan / far south-eastern Punjab |

**⚠ Islamabad / Rawalpindi flagged specifically:** this table lists them Zone 3. Some Pakistani engineering
references instead cite the official BCP SP-2007 hazard map as Zone 2B for Islamabad/Rawalpindi. This is
exactly the kind of plot-specific number a reader is likely to take at face value without opening the map —
**do not use "3" or "2B" for an Islamabad/Rawalpindi project from this table alone.** Pull the actual zone
from the BCP SP-2007 map or the CDA/RDA submission form before any calculation, and if the plot is near the
Margalla / MBT-MFT structures, apply the rule below and design one zone higher than whichever the map shows.

**Rules for using this table**

1. It is indicative only. Pull the actual zone from the BCP SP-2007 map, or from the LDA/CDA/SBCA
   submission form for the plot.
2. Site within ~10 km of a mapped active fault (Chaman, MBT/MFT, Balakot–Bagh, Riasi, Allah Bund,
   Makran interface, Kalabagh) → **design one zone higher** than the map says, and in Zone 4 apply the
   near-source factors of §1.6.
3. Karachi / coastal Sindh: also screen tsunami inundation and liquefaction, not just shaking.
4. If the client cannot state the zone, **do not guess downward**. Default to Zone 3 for northern
   Punjab / KP / AJK / GB, Zone 2B elsewhere, and put the assumption in writing on every output.
5. A hill site is not automatically a higher zone, but it *is* automatically a higher-risk site
   (landslide, topographic amplification, split-level construction). Treat it as §9 hillside.

### 1.3 Soil profile — two vocabularies, do not mix them

BCP SP:07 is UBC-derived, and Pakistani practice quotes both the older **S1–S4 / coefficient S** system
and the UBC-97 **SA–SF / Ca, Cv** system. Pick one formulation (§3) and stay inside it.

**UBC-94 style (used with `C = 1.25·S / T^(2/3)`):**

| Soil type | Description | **S** |
|---|---|---|
| S1 | Rock or stiff soil, vs > 750 m/s, or stiff/dense soil < 60 m deep | 1.0 |
| S2 | Dense or stiff soil > 60 m deep | 1.2 |
| S3 | 6–12 m of soft-to-medium clay over sand/gravel | 1.5 |
| S4 | > 12 m of soft clay (PI > 20, w > 40%, su < 25 kPa) | 2.0 |

**UBC-97 style (used with `Ca`, `Cv`):**

| Profile | Description (top 30 m) | vs (m/s) | Typical Pakistani example |
|---|---|---|---|
| SA | Hard rock | > 1500 | Margalla/Salt Range rock outcrop |
| SB | Rock | 760–1500 | Northern rock sites |
| SC | Very dense soil / soft rock | 360–760 | Gravelly Potohar, firm Quetta valley terrace |
| SD | Stiff soil | 180–360 | **Default for most urban Punjab/KP plots** |
| SE | Soft soil profile, > 3 m of soft clay | < 180 | Peshawar valley silt, parts of coastal Karachi, riverine Sindh |
| SF | Liquefiable, quick/highly sensitive clay, peat, > 36 m soft clay | site-specific | Requires site response analysis — no shortcut |

**Defaults with no geotechnical report:** S2 / **SD**. On soft alluvium (Peshawar valley, riverine
Sindh/Punjab, parts of Karachi) assume S3 / **SE** until proven otherwise — and say a geotechnical
investigation is required before final design.

### 1.4 Importance factor I

| Occupancy | I |
|---|---|
| Standard house / ordinary residential | 1.00 |
| House containing a hazardous store, or an assembly space for >300 occupants | 1.25 |
| Essential facility (clinic, fire station, emergency shelter, school used as shelter) | 1.25 |

For a private house `I = 1.00` essentially always. Raise it only if the building has a genuine
post-earthquake function — and if it does, it is no longer a "house" for approval purposes either.

### 1.5 Structural system factors

**UBC-94 style `Rw` (used with `V = Z·I·C·W / Rw`):**

| System | Rw | Height limit for houses |
|---|---|---|
| Unreinforced masonry bearing wall (URM) | **Not permitted in Zone 2B+** | — |
| Reinforced / confined masonry bearing wall | 6 | 2 storeys Zone 3–4; 3 storeys Zone ≤ 2B (with engineer) |
| RC ordinary moment frame (OMF) | 5 | **Not permitted Zone 3–4** |
| RC intermediate moment frame (IMF) | 8 | Zone ≤ 2B |
| RC special (ductile) moment frame (SMF) | 12 | Any zone; ACI 318-19 Ch. 18 detailing mandatory |
| RC shear-wall bearing-wall system | 6 | Any zone |
| Dual system (SMF + shear walls) | 12 | Any zone |
| Timber-laced masonry (dhajji dewari, bhatar) | treat as 6, engineer-judged | 2 storeys |

**UBC-97 style `R` (used with `V = Cv·I·W / (R·T)`):**

| System | R | Ωo |
|---|---|---|
| Bearing wall — reinforced/confined masonry shear walls | 4.5 | 2.8 |
| Bearing wall — RC shear walls | 4.5 | 2.8 |
| Building frame — RC shear walls | 5.5 | 2.8 |
| Light-framed walls with structural panel sheathing | 5.5 | 2.8 |
| RC OMF | 3.5 | 2.8 |
| RC IMF | 5.5 | 2.8 |
| RC SMF | 8.5 | 2.8 |
| Dual: SMF + RC shear walls | 8.5 | 2.8 |

Rough relationship: `Rw ≈ 1.4 R`. **Never mix an Rw with a Ca/Cv formulation or an R with the
`1.25S/T^(2/3)` formulation** — that is the most common arithmetic error in Pakistani house
calculations and it can halve the design force.

### 1.6 Near-source factors Na, Nv — Zone 4 only

Applied to Ca and Cv in Zone 4 when the site is close to a known seismic source (relevant for Quetta /
Chaman, Muzaffarabad / Balakot–Bagh).

| Seismic source type | Distance ≤ 2 km | 5 km | 10 km | ≥ 15 km |
|---|---|---|---|---|
| **Na** — Type A (M ≥ 7.0, high slip rate) | 1.5 | 1.2 | 1.0 | 1.0 |
| **Na** — Type B | 1.3 | 1.0 | 1.0 | 1.0 |
| **Na** — Type C | 1.0 | 1.0 | 1.0 | 1.0 |
| **Nv** — Type A | 2.0 | 1.6 | 1.2 | 1.0 |
| **Nv** — Type B | 1.6 | 1.2 | 1.0 | 1.0 |
| **Nv** — Type C | 1.0 | 1.0 | 1.0 | 1.0 |

For a short-period house `Ca` governs, so `Na` is the one that bites: a Quetta house 2 km from a Type A
source sees **50% more** design force than the bare Zone 4 value.

### 1.7 Ca and Cv tables (UBC-97 basis, verify against the code)

**Ca (short-period / acceleration-controlled — governs for houses):**

| Soil | Z=0.075 | Z=0.15 | Z=0.20 | Z=0.30 | Z=0.40 |
|---|---|---|---|---|---|
| SA | 0.06 | 0.12 | 0.16 | 0.24 | 0.32 Na |
| SB | 0.08 | 0.15 | 0.20 | 0.30 | 0.40 Na |
| SC | 0.09 | 0.18 | 0.24 | 0.33 | 0.40 Na |
| **SD** | **0.12** | **0.22** | **0.28** | **0.36** | **0.44 Na** |
| SE | 0.19 | 0.30 | 0.34 | 0.36 | 0.36 Na |

**Cv (velocity-controlled — governs for taller/flexible buildings, rarely for houses):**

| Soil | Z=0.075 | Z=0.15 | Z=0.20 | Z=0.30 | Z=0.40 |
|---|---|---|---|---|---|
| SA | 0.06 | 0.12 | 0.16 | 0.24 | 0.32 Nv |
| SB | 0.08 | 0.15 | 0.20 | 0.30 | 0.40 Nv |
| SC | 0.13 | 0.25 | 0.32 | 0.45 | 0.56 Nv |
| **SD** | **0.18** | **0.32** | **0.40** | **0.54** | **0.64 Nv** |
| SE | 0.26 | 0.50 | 0.64 | 0.84 | 0.96 Nv |

SF requires a site-specific response analysis — no table value exists.

---

## Section 2: House Seismic Design Category — the missing prescriptive tier

BCP 2007 gives an engineered force procedure but **no prescriptive "house table"**. Compare with the US
route, where **IRC 2021 Table R301.2.2.1.1** converts ASCE 7-22 spectral accelerations into a **Seismic
Design Category (SDC A–F)** and then lets a non-engineer use prescriptive bracing tables (e.g. IRC
§R602.10.10.1 restricting cripple-wall bracing to WSP / CS-WSP in SDC D0/D1 and for townhouses in SDC C;
1–2 family dwellings above two storeys in SDC D2 must be engineered rather than prescriptive).

**That prescriptive tier does not exist in Pakistani code for informal house construction.** This is a
genuine gap, not an oversight in this skill. Section 2.1 is a **synthesised** house-category ruleset that
fills it *for planning purposes only*. It is not a code and must not be described as one.

### 2.1 House Seismic Category (HSC) — synthesised, planning use only

| HSC | Trigger | Permitted systems | Mandatory measures |
|---|---|---|---|
| **H1** | Zone 1, ≤ 2 storeys | Confined masonry; RC frame | Plinth + roof tie beams; corner tie columns; symmetric plan |
| **H2** | Zone 2A–2B, ≤ 2 storeys | Confined masonry; RC IMF/SMF | Full tie system; wall-density check; no soft storey; no short columns |
| **H3** | Zone 3, ≤ 2 storeys | Confined masonry; RC SMF | H2 + tie-column spacing ≤ 4.5 m; continuous lintel band; wall density per §5; PEC engineer sign-off |
| **H4** | Zone 4 any storeys; **or** Zone 3 with 3 storeys; **or** any zone with a plan/vertical irregularity that cannot be designed out; **or** soil SE/SF | RC SMF or engineered confined masonry only | Full engineered analysis, no prescriptive shortcut, irregularity explicitly analysed, geotechnical report mandatory |

### 2.2 Approximate BCP zone ↔ ASCE 7 / IRC SDC mapping (for cross-reading US guidance)

| BCP zone | PGA band | Rough ASCE 7 SDC equivalent | What that unlocks in US guidance |
|---|---|---|---|
| 1 | 0.05–0.08 g | A / B | Minimal prescriptive seismic requirements |
| 2A | 0.08–0.16 g | B / C | Some bracing restrictions begin |
| 2B | 0.16–0.24 g | C | Townhouse bracing limits; irregularity checks start |
| 3 | 0.24–0.32 g | D0 / D1 | Restricted bracing methods; detailing mandated |
| 4 | > 0.32 g | D2 / E | Engineered design; extreme irregularities prohibited |

**Use this mapping only to read across to US literature.** It is approximate (SDC depends on Sds/Sd1 and
Risk Category, not PGA alone) and it is not a substitute for the BCP zone in any Pakistani submission.

### 2.3 Decision tree — pick the structural system for a house

```
START: What zone, how many storeys, who is actually building it?
│
├─ Zone 1–2A, 1–2 storeys, mason-built, no site engineer
│     → CONFINED MASONRY (HSC H1/H2). Simplest reliable option.
│
├─ Zone 2B–3, 1–2 storeys, mason-built with periodic supervision
│     → CONFINED MASONRY (HSC H2/H3). Ductility comes from confinement geometry,
│       not from precise rebar detailing at joints — far more forgiving of
│       average Pakistani site workmanship than an RC frame.
│
├─ Zone 3–4, any storeys, full-time engineer + competent contractor
│     → RC SPECIAL MOMENT FRAME (ACI 318-19 Ch. 18) with explicitly isolated or
│       fully-tied infill, OR RC shear-wall / dual system.
│       Choose this ONLY if the detailing will actually be built as drawn.
│
├─ Zone 3–4, 3+ storeys
│     → HSC H4. Engineered only. Confined masonry above 2 storeys in Zone 3–4
│       is outside the prescriptive envelope of every guide referenced here.
│
├─ Large column-free span needed (drawing room > 6 m, basement parking)
│     → RC frame line or RC shear-wall box inserted into an otherwise
│       confined-masonry house; the two systems must be separated by a joint
│       or analysed together — never silently mixed.
│
├─ Hill site (Murree, Abbottabad, AJK, Swat), any zone
│     → Stepped foundations + level-by-level tie beams. NEVER a row of
│       varying-length columns on a cut slope (short-column + torsion killer).
│
├─ Rural / low-budget / no cement supply chain, Zone 3–4
│     → Timber-laced masonry (dhajji dewari / bhatar) per §11, light roof.
│       Do NOT default to adobe or random rubble.
│
└─ Existing unreinforced masonry house needing improvement
      → §12 retrofit (splint-and-bandage, corner stitching, roof tie, hazard removal).
```

### 2.4 Why confined masonry, not "RC frame with brick infill", for ordinary Pakistani houses

The default Pakistani "grey structure" — RC columns and beams cast first, then 9" brick infill packed in
afterwards — is **not** an RC frame in any code sense unless the frame is detailed and analysed as one.
In 2005 the principal collapse modes among such buildings were: no confinement hoops at joints, no
capacity design (weak column–strong beam), infill panels acting as unintended bracing, and short columns
created by partial-height infill.

Confined masonry inverts the sequence — **masonry panel first, tie columns and tie beams cast against it
afterwards** — so wall and confinement act as one composite element and the failure mode is distributed
cracking rather than storey collapse.

| | Confined masonry | RC moment frame (informally built) |
|---|---|---|
| Construction sequence | Wall first, tie elements cast against it | Frame first, infill later |
| Where ductility comes from | Confinement geometry + toothing/dowels | Precise hoop detailing at joints |
| Sensitivity to workmanship | Moderate | **Severe** |
| Typical Pakistani outcome 2005 | Cracked but standing | Storey collapse |
| Steel content | Low (~4–8 kg/m² of floor) | High (~25–45 kg/m² of floor) |
| Cost | Lower | Higher |
| Plan flexibility | Low (walls are structure) | High |
| Vertical extension later | Hard — recheck density + foundation | Easier if originally designed for it |

---

## Section 3: Base Shear — two formulations and worked examples

### 3.1 Which formulation

BCP SP:07 derives from the UBC family. Pakistani practice and literature quote **both**:

- **Form A (UBC-94 style)** — `V = Z·I·C·W / Rw`, `C = 1.25·S / T^(2/3) ≤ 2.75`, floor `C/Rw ≥ 0.075`.
- **Form B (UBC-97 style)** — `V = Cv·I·W / (R·T)`, capped by `V ≤ 2.5·Ca·I·W / R`, floored by
  `V ≥ 0.11·Ca·I·W`, plus in Zone 4 `V ≥ 0.8·Z·Nv·I·W / R`.

**Rule:** state which form you used, on the same page as the number. If the two disagree (they do — see
§3.3), design to the **more onerous** unless the PEC engineer directs otherwise.

### 3.2 Procedure (both forms)

1. `T = Ct · h^0.75` — `Ct = 0.0488` (metric) for masonry / bearing-wall / braced systems,
   `Ct = 0.0731` for RC moment frames. `h` = height above base, m.
2. Compute `C` (Form A) or `Ca`, `Cv` (Form B).
3. Compute `V`, applying the caps and floors.
4. Distribute vertically: `Fx = V · wx·hx / Σ(wi·hi)`. Top force `Ft = 0` when `T ≤ 0.7 s`
   (all normal houses).
5. Storey shear at level x = sum of all `Fx` above that level.
6. Load combinations (ACI 318-19 §5.3, strength design): `1.2D + 1.0E + 1.0L + 0.2S`, `0.9D ± 1.0E`.
7. Drift: `Δm ≤ 0.025 h` for T < 0.7 s (`0.020 h` for T ≥ 0.7 s). For masonry target service-level
   drift ≤ **0.004 h** for crack control — the code limit is a collapse limit, not a damage limit.
8. Apply **accidental torsion**: shift the centre of mass ±5% of the plan dimension perpendicular to the
   force, in both directions, and re-check.
9. Check each direction **independently**; orthogonal combination (100% + 30%) is required where
   irregularities or corner columns govern.

**Seismic weight W includes:** all dead load; permanent partitions; 25% of live load for storage
occupancies only (not for houses); the full weight of overhead water tanks; 20% of flat-roof snow load
where snow > 1.5 kPa (northern Pakistan). It **excludes** ordinary residential live load.

### 3.3 Worked example — 2-storey confined masonry house, Islamabad

**Given:** 10 m × 10 m footprint (100 m²/floor), 2 storeys, floor-to-floor 3.2 m, h = 6.4 m.
Zone 3 → Z = 0.30 (**assumed for this worked example — verify against the official BCP map before use on
an actual Islamabad plot; see the §1.2 flag on this exact city pair**). Soil: no report → S2 / SD.
Standard house → I = 1.0. Confined masonry → Rw = 6 (Form A) / R = 4.5 (Form B).
9" (0.23 m) solid brick walls, 40 m wall run per storey; 150 mm RC slabs.

**Period**
```
T = 0.0488 × 6.4^0.75 = 0.0488 × 4.02 = 0.196 s
```

**Seismic weight W**

| Item | Calculation | kN |
|---|---|---|
| Slab DL (self 0.15 × 24 = 3.6 + finishes 1.2 = 4.8 kPa) | 4.8 × 100 | 480 per level |
| Wall weight, one storey (40 m × 3.2 m × 0.23 m × 19 kN/m³) | | 559 per storey |
| Level 2 (roof) | 480 + ½(559) | **760** |
| Level 1 (first floor) | 480 + ½(559) + ½(559) | **1039** |
| **W total** | | **1799** |

**Form A (UBC-94 style)**
```
C     = 1.25 × 1.2 / 0.196^(2/3) = 1.50 / 0.337 = 4.45  →  capped at 2.75
C/Rw  = 2.75 / 6 = 0.458 ≥ 0.075  ✓
V     = 0.30 × 1.0 × 2.75 / 6 × 1799 = 0.1375 × 1799 = 247 kN      (13.75% W)
```

**Form B (UBC-97 style), soil SD → Ca = 0.36, Cv = 0.54, R = 4.5**
```
V(T)  = 0.54 × 1.0 × 1799 / (4.5 × 0.196) = 971 / 0.882 = 1101 kN   (governed by cap)
Vcap  = 2.5 × 0.36 × 1.0 × 1799 / 4.5 = 1619 / 4.5     = 360 kN     (20.0% W)  ← governs
Vfloor= 0.11 × 0.36 × 1.0 × 1799                        = 71 kN
V     = 360 kN
```

**Result: 247 kN (Form A) vs 360 kN (Form B) — a 46% difference on the same house.** Design to 360 kN,
say so explicitly, and let the engineer resolve which the authority expects. This divergence is exactly
why "we did a seismic calculation" is not a meaningful claim without the formulation attached.

**Vertical distribution (using V = 360 kN)**
```
Σ(w·h) = 1039 × 3.2 + 760 × 6.4 = 3325 + 4864 = 8189
F1 = 360 × 3325/8189 = 146 kN     storey shear, ground storey = 360 kN
F2 = 360 × 4864/8189 = 214 kN     storey shear, upper storey  = 214 kN
```

**Useful mental constant:** *a Zone 3 house must resist a horizontal force of roughly one-fifth of its
own weight, applied at floor levels, in each direction independently.*

**Cross-check against masonry shear capacity — ⚠ ASSUMED PLACEHOLDER, not a design value.** Ground-storey
shear 360 kN per direction. The `v_d` used below is a rule-of-thumb figure for illustrating the *method*
only; it is **not** a validated or code-derived design shear stress — real values depend entirely on the
actual tested brick and mortar strength and axial precompression on site, and must be substituted before
this cross-check is used for anything beyond understanding the arithmetic (see §18 gap #6 for the same
caveat stated again at the gaps register). With an **assumed** design in-plane shear stress for confined
masonry `v_d ≈ 0.20 MPa` on the net wall cross-section (Pakistani first-class brick f'b ≈ 10.5 MPa with
1:6 mortar, illustrative only):

```
Required net wall area per direction = 360,000 N / 0.20 N/mm² = 1.80 × 10^6 mm² = 1.80 m²
Required effective wall length (0.23 m thick) = 1.80 / 0.23 = 7.8 m per direction
```

The wall-density rule in §5 asks for **3.5 m² (15.2 m)** for this case — roughly **2× more conservative**
than the raw stress check. That margin is doing real work: it silently covers torsion, openings, poor
mortar, out-of-plane demand and workmanship scatter. **Use the density rule for design; use the stress
check only as a cross-check, and only after replacing the placeholder `v_d` with a tested value.**

### 3.4 Worked example — 2-storey RC frame house, Karachi (for comparison)

Same 10 × 10 m, 2 storeys, h = 6.4 m, Zone 2B (Z = 0.20), soil SD (Ca = 0.28, Cv = 0.40),
RC SMF → R = 8.5 / Rw = 12. W ≈ 1650 kN (lighter walls, heavier frame).

```
T = 0.0731 × 6.4^0.75 = 0.294 s
Form A: C = 1.25 × 1.2 / 0.294^(2/3) = 1.50/0.442 = 3.39 → cap 2.75
        V = 0.20 × 1.0 × 2.75/12 × 1650 = 0.0458 × 1650 = 76 kN   (4.6% W)
Form B: V(T)   = 0.40 × 1650 / (8.5 × 0.294) = 660/2.50 = 264 kN
        Vcap   = 2.5 × 0.28 × 1650 / 8.5 = 1155/8.5      = 136 kN  ← governs (8.2% W)
        Vfloor = 0.11 × 0.28 × 1650                       = 51 kN
```

Note how much lower the frame's design force is than the masonry house's — **because the code is buying
that reduction with ductility that only exists if ACI 318-19 Ch. 18 detailing is actually built.** If the
hoops are at 250 mm with 90° hooks, the R = 8.5 reduction is fiction and the building is being designed
for a fraction of what it will actually see. This is the single most important sentence in this skill for
Pakistani RC frame houses. §7.6 continues this same Karachi frame numerically into the joint-level
strong-column/weak-beam and joint-shear check.

### 3.5 Zone-scaled base shear coefficients for houses

**Form A (`C = 2.75` governing, I = 1.0):**

| Zone (Z) | Confined masonry Rw=6 | RC IMF Rw=8 | RC SMF Rw=12 |
|---|---|---|---|
| 1 (0.075) | 0.034 W | 0.026 W | 0.017 W |
| 2A (0.15) | 0.069 W | 0.052 W | 0.034 W |
| 2B (0.20) | 0.092 W | 0.069 W | 0.046 W |
| 3 (0.30) | 0.138 W | 0.103 W | 0.069 W |
| 4 (0.40) | 0.183 W | 0.138 W | 0.092 W |

**Form B (`V = 2.5·Ca·I/R`, soil SD, I = 1.0, Na = 1.0):**

| Zone (Ca, SD) | Masonry R=4.5 | RC IMF R=5.5 | RC SMF R=8.5 |
|---|---|---|---|
| 1 (0.12) | 0.067 W | 0.055 W | 0.035 W |
| 2A (0.22) | 0.122 W | 0.100 W | 0.065 W |
| 2B (0.28) | 0.156 W | 0.127 W | 0.082 W |
| 3 (0.36) | 0.200 W | 0.164 W | 0.106 W |
| 4 (0.44) | 0.244 W | 0.200 W | 0.129 W |

Multiply by 1.25 for essential occupancy; by `Na` in Zone 4 near a source. Both tables assume the
short-period cap governs, valid for essentially all 1–3 storey houses.

### 3.6 Drift, separation and pounding

| Quantity | Rule | Worked value (6.4 m house) |
|---|---|---|
| Inelastic drift limit `Δm` | ≤ 0.025 h for T < 0.7 s | ≤ 160 mm total, ≤ 80 mm per storey |
| Masonry service-level target | ≤ 0.004 h (crack control) | ≤ 13 mm per storey |
| Seismic separation between blocks of one building | ≥ 25 mm + 15 mm per metre of height above 3 m | ≈ **75 mm** |
| Separation from a neighbouring building | `≥ √(δ1² + δ2²)` (SRSS of the two buildings' drifts); when the neighbour's drift is unknown, use `≥ Δm` of your own building | ≥ 160 mm — usually impossible on a Pakistani plot, so **align floor levels with the neighbour** so slabs meet slabs, never slab-against-column |
| Joint construction | Full height, foundation to roof, filled with compressible filler + flexible sealant, covered with a slip cover plate. **A joint bridged by plaster, tiles or a coping is not a joint.** | — |

**Pounding is the under-appreciated urban Pakistani hazard.** On a row of party-wall houses in Lahore or
Karachi, mismatched floor levels mean one building's slab edge hammers the neighbour's column at
mid-height — a short-column failure created by the neighbour. When zero gap is achievable, the mitigation
is level alignment plus a stiff, well-tied structure, and it should be stated as a residual risk.

---

## Section 4: Confined Masonry — Detailing Specification

Reference: EERI / World Housing Encyclopedia *Seismic Design Guide for Low-Rise Confined Masonry
Buildings* (Brzev & Meli), IS 4326:1993 (cross-referenced throughout Pakistani practice), NDMA Pakistan
Earthquake Guidelines. **Numeric values below are the practical baseline — cross-check against the NDMA
guideline tables and actual tested masonry strengths before any construction document.**

### 4.1 The non-negotiable construction sequence

```
1. Foundation + plinth beam cast
2. Masonry panel built FULL HEIGHT, with toothed vertical edges (or dowels) at every
   future tie-column location
3. Tie-column reinforcement cage placed against the toothed masonry edge
4. Tie-column concrete cast AGAINST the masonry (formwork on 2 faces only)
5. Tie-beam cage placed on top of the wall, continuous over all tie columns
6. Tie-beam cast monolithically with the slab where possible
7. Next storey repeats from step 2
```

**If the columns are cast before the wall, it is not confined masonry** — it is an undetailed RC frame
with infill, which is the 2005 collapse archetype. This single sequencing rule is the thing most often
lost in translation on site. Put it on the drawing in Urdu, and photograph the toothing before the cage
goes in.

### 4.2 Tie-column (vertical confining element) schedule

| Parameter | Requirement |
|---|---|
| Location — mandatory | Every external corner; every wall intersection / T-junction; every free end of a wall; **both jambs of every opening wider than 1.2 m** (or wider than half the storey height); both sides of every seismic joint |
| Maximum spacing along a wall | **4.5 m** in Zone 3–4 (high / very high); **6.0 m** in Zone 1–2B (low / moderate). Also ≤ 1.5 × storey height |
| Minimum cross-section | Wall thickness × ≥ 200 mm. For a 9" (230 mm) wall use **230 × 230 mm**; never less than 150 mm in any dimension |
| Minimum concrete | f'c ≥ 17.5 MPa (2500 psi); **prefer 20 MPa (3000 psi)** in Zone 3–4; max aggregate 12 mm for congested cages; slump 100–125 mm so it flows against the toothing |
| Main reinforcement | **4 bars × 12 mm (½")** minimum, Grade 60 (or Grade 40 with the engineer's check); **4 × 16 mm** for 3-storey work or the Zone 4 ground storey |
| Ties / stirrups | 6 mm @ 200 mm centres at mid-height; **@ 100 mm within 450 mm of each end** (top and bottom — the joint region is exactly where it fails) |
| Hooks | **135° seismic hooks, extension ≥ 6 d_b and ≥ 75 mm (3")**. 90° hooks are a defect — reject them |
| Cover | 20 mm to ties on faces cast against masonry; 40 mm where exposed to weather or soil |
| Lap splices | ≥ 50 d_b (600 mm for a 12 mm bar); **never lapped inside a joint region**; stagger so < 50% of bars lap at one section |
| Continuity | Continuous from plinth beam to roof tie beam; anchored ≥ 40 d_b into the plinth beam and the roof beam |
| Casting | Full storey height in one pour — **no cold joint at mid-height** |

**Quantity check:** one 230 × 230 × 3200 mm tie column = **0.169 m³** concrete and ≈ **16 kg** steel
(4 × 12 mm main = 11.4 kg; ~22 ties × 0.91 m × 0.222 kg/m = 4.4 kg).

### 4.3 Tie-beam (horizontal confining element / band) schedule

| Parameter | Requirement |
|---|---|
| Levels — mandatory | **Plinth level**, **lintel level** (all openings in one continuous band), **every floor level**, **roof level**; plus a **gable band** following the slope of any gable end |
| Maximum vertical spacing | **≤ 3.0 m** — one per storey minimum, plus a lintel band wherever storey height > 2.7 m or openings are large |
| Minimum section | Width = wall thickness; depth ≥ 150 mm (use **230 mm** in Zone 3–4) |
| Reinforcement | 4 × 12 mm minimum (2 top, 2 bottom); stirrups 6 mm @ 150–200 mm, **@ 100 mm within 450 mm of every intersection** |
| Continuity | **Fully continuous around the entire building perimeter AND along every internal load-bearing wall.** A band that stops at a doorway is not a band |
| Corner detail | L-bars or continuous bent bars with ≥ 40 d_b anchorage both ways. **Never** two straight bars simply overlapping at a corner — the corner is where the band earns its keep |
| Lintel band | If a lintel band and a floor band fall within 500 mm of each other, merge them into one deeper band rather than casting two weak ones |
| Interaction with slab | Cast monolithically with the RC slab where possible so band and diaphragm are one element |

**Quantity check:** 230 × 230 mm band ≈ **0.053 m³/m** concrete and ≈ **4.7 kg/m** steel
(4 × 12 mm = 3.55 kg/m + stirrups ≈ 1.15 kg/m at 175 mm centres).

### 4.4 Masonry panel rules

| Parameter | Requirement |
|---|---|
| Wall thickness | ≥ 230 mm (9") for load-bearing walls; 115 mm (4.5") walls are **partitions only**, never counted in wall density, never carrying a slab |
| Height / thickness ratio **H/t** | **≤ 25** for 1–2 storey (≤ 5.75 m for a 230 mm wall — always satisfied at 3.2 m storey height; the rule bites for double-height living rooms, stairwell walls and gable walls). ≤ 20 for 3 storey. See §5.4 for the out-of-plane check the ratio is a proxy for |
| Panel max dimension between confining elements | ≤ 4.5 m (Zone 3–4) / 6.0 m (Zone 1–2B); panel aspect ratio (length : height) preferably ≤ 1.5 |
| Minimum wall length to count as a shear element | ≥ 1.2 m, and length/height ≥ 0.4 |
| Brick strength | First-class solid clay brick, f'b ≥ 7 MPa (target ≥ 10.5 MPa / 1500 psi). **No khingar / under-burnt brick; no hollow concrete block unless grouted and reinforced, in Zone 2B+** |
| Mortar | ≥ 1:6 cement:sand; **1:4 for the ground storey in Zone 3–4**. Mud mortar prohibited in Zone 2B+ |
| Bond | English or Flemish bond; fully filled bed **and** perpend joints; joint thickness 10–12 mm |
| Toothing | Alternate courses toothed 50–60 mm into the future tie column; **or** 2 × 6 mm horizontal dowels every third course (≈ 600 mm) extending ≥ 400 mm into the panel and ≥ 400 mm into the tie column |
| Wetting & curing | Bricks soaked before laying; walls cured 7 days. Dry bricks suck the mortar dry and roughly halve bond strength — which is the strength the whole system depends on |
| Chases | No vertical chase in a counted shear wall or a tie column. Horizontal chases ≤ 1/3 wall thickness, never within 300 mm of a band |

### 4.5 Opening rules (IS 4326:1993 Cl. 8.3 / Table 4 — standard Pakistani cross-reference)

`L` = length of wall between cross-walls / confining elements.

| Rule | 1 storey | 2 storey | 3 storey |
|---|---|---|---|
| Total length of openings ≤ fraction of `L` | **0.50 L** | **0.42 L** | **0.33 L** |
| Pier width between two consecutive openings | ≥ 0.5 m | ≥ 0.6 m | ≥ 0.6 m |
| Distance from an inside corner of a wall junction to the nearest opening | ≥ 0.5 m (min 230 mm, 1 storey) | ≥ 0.6 m | ≥ 0.6 m |
| Vertical distance between two openings, one above the other | ≥ 0.6 m | ≥ 0.6 m | ≥ 0.6 m |
| Opening wider than 1.2 m | Tie column at **both** jambs | same | same |
| Opening top | Must sit under the continuous lintel band, bearing ≥ 230 mm each side | same | same |
| Opening area as % of wall face | ≤ 30% preferred | ≤ 25% | ≤ 20% |

**Corner windows** — an opening wrapping a building corner — are **prohibited in Zone 2B+**. They destroy
the corner, which is the single most important element in a masonry box. When a client insists, the only
honest answers are: (a) move it 600 mm off the corner, (b) make the corner an RC column designed for the
full corner force, or (c) accept a documented reduction in seismic performance in writing.

### 4.6 Reinforced masonry variant (where confinement is impractical)

Where tie columns cannot be formed (curved walls, block masonry, very tight programme), the alternative
is **reinforced masonry**: vertical bars grouted into aligned cavities/cells.

| Parameter | Requirement |
|---|---|
| Vertical bars | 1 × 12 mm minimum at every corner, wall end, opening jamb, and at ≤ 1.2 m centres in Zone 3–4 (≤ 2.0 m in Zone ≤ 2B) |
| Grout | f'c ≥ 20 MPa, high slump (200–250 mm), grouted in ≤ 1.5 m lifts, consolidated |
| Horizontal reinforcement | Bed-joint reinforcement (2 × 6 mm or ladder mesh) every third course, plus the same band system as §4.3 |
| Cells | Every cell containing a bar must be **fully grouted** — ungrouted cells around a bar are the classic hollow-block failure |
| Zone 3–4 | Solid grouting of the whole wall is preferred; partial grouting requires engineer justification |

Reinforced masonry is more sensitive to grouting quality than confined masonry is to concrete quality.
On an unsupervised site, prefer confined masonry.

### 4.7 Common confined-masonry defects on Pakistani sites — reject list

- Tie columns cast **before** the masonry (frame-and-infill masquerading as confined masonry).
- Smooth, untoothed, undowelled vertical joint between column and wall → zero shear transfer.
- Ties with **90° hooks**, or hooks straightened on site to fit the formwork.
- Tie spacing uniform at 200 mm with **no closing-up at the ends**.
- Lintel band stopped either side of a door and "made up" with a loose precast lintel.
- Roof band omitted because "the RC slab does the same job" — it does not, unless the slab is designed
  and reinforced as a diaphragm and tied into every wall.
- Tie-column bars lapped at floor level, inside the joint.
- Half-brick (4.5") walls counted as structural, or carrying a slab edge.
- Hollow-block walls with ungrouted cells in Zone 3–4.
- Plumbing / electrical chases cut vertically through a tie column or through the middle of a counted
  shear wall after casting.
- Concrete placed without vibration into a 230 mm cage — honeycombing at exactly the joint region.
- A cold joint at mid-height of a tie column because the pour ran out of concrete.

---

## Section 5: Wall Density — the single most useful house-scale check

**Wall density `d` = (total horizontal cross-sectional area of load-bearing walls in one direction) ÷
(floor plan area of that storey), as a percentage.** Compute separately for X and Y, at **every** storey,
and satisfy it in **both**.

### 5.1 Minimum wall density (%) — planning table

| Zone (PGA) | 1 storey | 2 storey (check ground storey) | 3 storey (check ground storey) |
|---|---|---|---|
| 1 (≈0.07 g) | 1.0 % | 1.5 % | 2.0 % |
| 2A (≈0.12 g) | 1.0 % | 1.5 % | 2.5 % |
| 2B (≈0.20 g) | 1.5 % | 2.5 % | 4.0 % |
| 3 (≈0.28 g) | 2.0 % | 3.5 % | 5.0 % (not recommended) |
| 4 (>0.32 g) | 2.5 % | 4.5 % | **Not permitted without full engineered analysis** |

**Adjustments**
- Weaker brick or mortar (f'b < 7 MPa, or 1:8 mortar): **× 1.25**.
- Soft soil (S3/S4 or SE): **× 1.25**.
- Both: **× 1.5**, and treat the house as HSC H4.
- Hollow block instead of solid clay brick, fully grouted: **× 1.2**; ungrouted: not permitted Zone 2B+.

*Calibration caveat: these approximate the EERI/WHE confined-masonry guide's simplified density tables
for solid clay brick with ordinary mortar. The engineer's own calculation governs.*

### 5.2 Counting rules

- Count **only** walls ≥ 230 mm thick, continuous from foundation to the level above, confined on all
  four sides.
- Count only the wall **length in that direction**. A wall at 45° counts in **neither** direction — and
  is itself a nonparallel-system irregularity.
- **Subtract openings.** A 4.0 m wall with a 1.2 m door counts as 2.8 m.
- A wall shorter than **1.2 m**, or with length/height < 0.4, contributes almost nothing in shear — do
  not count it.
- A wall interrupted by a chase, a duct, or a full-height cupboard recess is not continuous.
- Walls must be reasonably **distributed**, not concentrated on one side (see §6 torsion).

### 5.3 Worked example

Zone 3, 2 storey, 10 m × 10 m = 100 m² per floor → required `d = 3.5%` → **3.5 m² per direction** at the
ground storey. With 230 mm walls: required effective length = 3.5 / 0.23 = **15.2 m in X and 15.2 m in Y**.

A typical 10 × 10 plan has two 10 m external walls plus one 10 m internal wall per direction = 30 m gross.
Subtract openings (a 1.5 m window and a 1.0 m door per wall ≈ 7 m total) → ~23 m effective.
**23 m > 15.2 m ✓ passes with margin.**

Now the same plan with a fully open ground-floor drawing/dining/parking side: X-direction effective wall
length drops to ~9 m → **9 m < 15.2 m ✗ FAILS** — and it fails in one direction only, which also creates
torsion. This is exactly the plan the client will ask for. Fixes, in order of preference:

1. Add a **1.5–2.0 m return wall at each end** of the open side (turns one open wall into two piers).
2. Convert the open side to an **RC shear wall** or a ductile RC frame line designed for the full storey
   shear plus the torsional amplification.
3. **Move the open side to the upper floor**, where the demand is lower and the storey below stays stiff.
4. Reduce the opening width and add tie columns at both jambs.
5. If none is accepted: document in writing that the design does not meet the density criterion, name the
   consequence (soft-storey collapse mechanism), and refer it to the engineer as an explicit exception.

### 5.4 Out-of-plane wall check (what H/t is a proxy for)

The H/t ≤ 25 rule is a shortcut. The underlying check, worth running for tall walls, gable ends and
parapets:

```
Element force (UBC-97 §1632 basis):
    Fp = ap · Ca · Ip · Wp · (1 + 3 hx/hr) / Rp
    with ap = 1.0, Rp = 3.0 for a wall spanning between bands
    bounded:  0.7·Ca·Ip·Wp  ≤  Fp  ≤  4.0·Ca·Ip·Wp
```

**Worked example — 230 mm brick wall, top storey, Zone 3, soil SD (Ca = 0.36):**
```
Wp = 0.23 × 19 = 4.37 kN/m²
At roof level, hx/hr = 1.0:
Fp = 1.0 × 0.36 × 1.0 × 4.37 × (1 + 3)/3 = 2.10 kN/m²
Wall spans 3.2 m vertically between bands:
M  = w·L²/8 = 2.10 × 3.2² / 8 = 2.69 kNm per metre width
Section modulus, 230 mm wall: Z = 1000 × 230² / 6 = 8.82 × 10^6 mm³
Flexural tensile stress = 2.69 × 10^6 / 8.82 × 10^6 = 0.31 MPa
```
Allowable flexural tension for clay brick in 1:6 mortar is roughly **0.1–0.25 MPa** — so this wall
**fails** the elastic out-of-plane check on its own. It survives only because the bands and tie columns
turn it into a two-way panel supported on four sides. **That is the argument for bands: without them, a
perfectly ordinary 3.2 m brick wall cannot span out-of-plane in Zone 3.** Never omit the lintel band to
save money on a tall room.

Practical out-of-plane rules:
- Gable walls: add a **gable band** following the roof slope, plus vertical bars at ≤ 1.5 m; or replace
  the gable masonry with a light infill.
- Free-standing walls (boundary, parapet): see §10.
- Any wall panel with an unsupported dimension > 4.5 m in either direction needs an intermediate
  confining element, regardless of H/t.

---

## Section 6: Configuration & Irregularity Rules for House Plans

Reference thresholds: **ASCE 7-22 Table 12.3-1 (horizontal irregularities)** and **Table 12.3-2 (vertical
irregularities)** — the numeric definitions behind IBC/IRC, used analogously in engineered design checked
against BCP.

### 6.1 Irregularity threshold table

| Irregularity | Definition | Extreme |
|---|---|---|
| **Soft storey (stiffness)** | Storey lateral stiffness **< 70%** of the storey above, or **< 80%** of the average of the three storeys above | **< 60%** / **< 70%** — extreme soft storey is **prohibited** in higher seismic design categories |
| **Weak storey (strength)** | Storey lateral strength **< 80%** of the storey above | **< 65%** — prohibited above 2 storeys in high SDC |
| **Torsional** | Max storey drift at one end **> 1.2 ×** the average of the two ends (accidental torsion included, Ax = 1.0) | **> 1.4 ×** |
| **Re-entrant corner** | Plan projection beyond a re-entrant corner **> 15%** of the plan dimension in that direction | — |
| **Diaphragm discontinuity** | Cut-out / open area **> 50%** of gross diaphragm area, or diaphragm stiffness change **> 50%** between storeys | — |
| **Out-of-plane offset** | A lateral-force-resisting element offset out of plane between storeys | — (severe; avoid entirely in houses) |
| **Nonparallel system** | Vertical LFRS elements not parallel to the major orthogonal axes | — |
| **Mass (weight)** | Effective mass of a storey **> 150%** of an adjacent storey | — |
| **Vertical geometric** | Horizontal dimension of the LFRS **> 130%** of the adjacent storey | — |
| **In-plane discontinuity** | Wall/frame offset in plane greater than its own length, or a reduction in stiffness of the storey below | — |

### 6.2 Translation into concrete house-plan rules

**DO**

- Keep the plan a simple rectangle or square. **Plan aspect ratio ≤ 3:1, prefer ≤ 2:1.**
- Place walls **symmetrically about both axes**; target centre-of-mass to centre-of-rigidity eccentricity
  **≤ 10%** of the plan dimension in that direction (the 5% accidental eccentricity is added on top of
  whatever real eccentricity you leave in).
- Provide **at least two lines of lateral resistance in each direction**, spaced ≥ 75% of the plan
  dimension apart. A wide couple resists torsion; two walls next to each other do not.
- Keep the **same wall/column layout at every storey**, foundation to roof — an uninterrupted vertical
  load path is worth more than any calculation.
- Keep storey heights equal (± 10%). Where one room needs a higher ceiling, split the building into two
  blocks with a joint.
- If the plan is L, T, U, H or +, **split it into rectangular blocks with a seismic separation joint**
  rather than analysing the re-entrant corner (joint width per §3.6).
- Make every floor and the roof a **rigid diaphragm** (§8).
- Place the staircase symmetrically, or tie it fully into the structure, or separate it entirely — a
  stair flight is an unintended diagonal brace and it attracts force it was not designed for.
- Put the heaviest elements (water tank, stone cladding, planted terrace) **low and over wall lines**.

**DON'T**

- **Open ground storey** for parking, a shop, a *baithak* or a *dera* under a heavier masonry storey
  above. This is the classic soft/weak storey and the single most lethal configuration in South Asian
  housing. If parking is unavoidable: (a) add RC shear walls in both directions at the ground storey,
  (b) design the ground columns for amplified overstrength forces, and (c) never let ground-storey
  stiffness drop below 70% of the storey above.
- **Short columns.** A partial-height infill, mezzanine sill, half-height parapet, ventilator strip or
  plinth-to-sill wall braces part of a column's clear height. Shear demand scales as `V = 2Mp / h_clear`
  — halving the clear height **doubles** the shear, and the column fails in brittle shear before any
  flexural ductility is mobilised. Explicitly identified as a major collapse mechanism in 2005 Kashmir
  reconnaissance (EERI, NZSEE).
  - Fixes: continue the infill full height; **or** provide a full-height **25–50 mm gap** with
    compressible filler and sealant between infill and column; **or** design it as a short column with
    closed hoops @ 100 mm over the **entire** clear height and shear capacity based on the reduced height.
- Asymmetric wall placement — solid masonry on two adjacent sides, glass on the other two → torsion; the
  building twists and the flexible corner fails first.
- Cantilevered upper floors or heavy overhangs projecting > 1.0 m without a designed backspan (and never
  cantilevering a masonry wall).
- Heavy roofs on weak walls: thick mud roofs on wooden joists, or a full RC slab on unconfined 4.5"
  masonry. Roof mass is the demand multiplier — every kN up there costs you ~0.2 kN of shear in Zone 3.
- A water tank on a slender column-supported frame on the roof (whip effect + mass irregularity at the
  worst possible height).
- Later roof-level additions ("one more floor next year") without re-checking wall density, W, drift and
  the foundation.
- Adjacent buildings without a separation gap or level alignment → pounding (§3.6).
- All openings concentrated in one wall line with none in the parallel wall.
- A basement under only part of the footprint (in-plane discontinuity + differential foundation stiffness).

### 6.3 Plan-check quick scoring (run at concept stage, before any detailing)

| Check | Pass | Flag |
|---|---|---|
| Plan aspect ratio | ≤ 2:1 | > 3:1 → split with a joint |
| Re-entrant projection | ≤ 15% | > 15% → seismic joint |
| Wall density X and Y | ≥ Table §5.1 | < table → redesign |
| Wall density X ÷ wall density Y | 0.7 – 1.4 | outside → torsion risk |
| Ground-storey wall length ÷ upper-storey wall length | ≥ 1.0 | < 0.7 → soft storey |
| Eccentricity (centre of mass → centre of rigidity) | ≤ 10% of plan dimension | > 10% → torsion, redistribute walls |
| Openings per wall panel | ≤ IS 4326 Table (§4.5) | over → add piers / tie columns |
| Same column/wall grid at all levels | yes | no → in-plane / out-of-plane discontinuity |
| Any column with clear height reduced by infill | none | any → short-column fix required |
| Storey mass ratio | ≤ 1.5 | > 1.5 → mass irregularity |
| Storey height variation | ≤ ±10% | > 10% → stiffness irregularity |
| Diaphragm opening (stair + light well) area | ≤ 30% of floor plate | > 50% → diaphragm discontinuity |

**Rule: fix every flag on the plan before drawing a single tie column.** Detailing cannot rescue a bad
configuration; it can only make a good one work.

### 6.4 Client red-flag phrases → what to say

| Client says | Seismic consequence | Response |
|---|---|---|
| "Open the whole ground floor for cars" | Soft/weak storey — the archetypal collapse mechanism | Offer shear walls in both directions, or move the open space upstairs |
| "I want a corner window in the drawing room" | Destroys the corner of the masonry box | 600 mm offset, or an RC corner column designed for it |
| "Put the *baithak* wall in later, we'll decide" | Unplanned stiffness → torsion or short columns | Decide now; the wall is structure, not furniture |
| "Cantilever the first floor over the porch" | Vertical geometric irregularity + backspan demand | Designed backspan, or columns to ground |
| "We'll add a floor in a few years" | Mass, W and foundation all change | Design for it now (foundation + density) or accept it is not possible |
| "The mason knows how to do this" | The 2005 failure population was mason-built without ties | Ties and sequencing on the drawing, in Urdu, with photos required |
| "Skip the engineer, it's only a house" | Unstamped design, no approval, life safety | Non-negotiable: PEC-registered engineer + authority approval |
| "Two half-brick walls instead of one 9-inch" | Two 4.5" leaves are not a 9" wall | Solid 230 mm, or engineered cavity wall with ties |

---

## Section 7: RCC Frame Houses — Ductile Detailing

Applies when an RC moment frame is genuinely chosen **and will genuinely be supervised**.
Reference: **ACI 318-19 Chapter 18 (Earthquake-Resistant Structures)**.

### 7.1 Special moment frame (SMF) essentials

| Item | Requirement (ACI 318-19 Ch. 18) |
|---|---|
| Minimum column dimension | 300 mm (12"); shorter : longer section ratio ≥ 0.4 |
| Concrete | f'c ≥ 21 MPa (3000 psi); normalweight for SMF |
| Strong column – weak beam | **ΣMnc ≥ 1.2 ΣMnb** at every joint (§18.7.3.2) |
| Column longitudinal steel ρ | 1% ≤ ρ ≤ 6% (practically ≤ 4% for constructability) |
| Confinement length `lo` at column ends | max of (member depth, clear span / 6, **450 mm**) |
| Hoop spacing within `lo` | ≤ min(**b/4**, **6 d_b** of the smallest longitudinal bar, **s_o** where 100 ≤ s_o ≤ 150 mm) |
| Max horizontal spacing of laterally supported bars, `hx` | ≤ **350 mm (14 in)** normally; tightened to ≤ **200 mm (8 in)** where `Pu > 0.3 Ag f'c` or `f'c > 70 MPa` (§18.7.5.2 / Table 18.7.5.4) → in practice this forces crossties on interior bars of larger or heavily loaded columns |
| Hoop spacing outside `lo` | ≤ min(6 d_b, 150 mm) |
| Beam hoops | Over **2h** from each face of support: ≤ min(d/4, 6 d_b, 150 mm); first hoop ≤ 50 mm from the column face |
| Beam bottom steel at supports | ≥ 50% of the top steel; positive moment strength ≥ ½ the negative moment strength at the joint face |
| Beam geometry limits | Clear span ≥ 4d; width ≥ min(0.3h, 250 mm) |
| Hooks / crossties | **135° seismic hooks**, extension ≥ 6 d_b and ≥ 75 mm; crossties alternated end-for-end along the member |
| Joints | Hoops **continued through the joint**; joint shear checked (§18.8); beam bars anchored with standard hooks into the confined core; joint dimension ≥ 20 d_b of the largest beam bar passing through |
| Lap splices | Only in the **middle half** of the member, enclosed by hoops at ≤ 100 mm; never within `lo`, never in a joint, never at the column base |
| Shear design | Capacity design — shear from probable moment strengths `Mpr` (1.25 fy), not from the analysis shear |

### 7.2 Intermediate moment frame (IMF)

Permitted in Zone ≤ 2B (SDC C analogue). Relaxations versus SMF: no strong-column/weak-beam requirement;
hoop spacing over `2h` at ≤ min(d/4, 8 d_b, 24 d_tie, 300 mm); reduced joint requirements. **Ordinary
moment frames are not permitted in Zone 3–4.**

### 7.3 Infill walls in RC frames — decide explicitly, never by default

Three legitimate strategies. Pick one and draw it:

1. **Isolated infill** — 25–50 mm gap on both sides and at the top, filled with compressible material and
   sealed; infill restrained out-of-plane by steel angles or dowels that transfer **no** in-plane force.
   Frame designed as a bare frame. Detail the gap on the drawing or it will be filled with mortar.
2. **Participating infill** — infill modelled as an equivalent diagonal strut; frame + infill designed
   together; infill tied to the frame with dowels at ≤ 600 mm; column shear amplification from the strut
   explicitly checked.
3. **Confined masonry** — abandon the frame idea and build per §4.

The illegal fourth option, universal on Pakistani sites, is: build a bare-frame design, then pack the bays
tight with brick and hope. That produces unintended stiffness, torsion, short columns, and a soft storey
at whichever level the infill happens to be omitted.

### 7.4 Why an RC frame is the *riskier* choice for an unsupervised house

In 2005 the RC frames that collapsed did so with textbook signatures: hoops at 250 mm straight through
the joint zone, 90° hooks, columns weaker than beams, lap splices at the column base, unconfined joint
cores, and infill-driven short columns. Confined masonry does not require that precision to work.

**Recommend a frame only when the answer to "will the joint hoops actually be tied at 100 mm with 135°
hooks, and will someone photograph them before the pour?" is a credible yes.** If it is not, recommending
an SMF is recommending a design whose entire force reduction (R = 8.5) rests on detailing that will not
be built.

### 7.5 RC shear walls in a house

Often the cheapest way to rescue an open ground floor.

| Parameter | Rule |
|---|---|
| Minimum thickness | 150 mm (200 mm preferred in Zone 3–4) |
| Minimum reinforcement | ρ ≥ 0.0025 each way, two curtains where thickness ≥ 200 mm or shear is high; spacing ≤ 450 mm |
| Boundary elements | Required where the compressive stress at the wall end exceeds 0.2 f'c (ACI 318-19 §18.10.6); detail as a confined column |
| Placement | Symmetric, in both directions, continuous to the foundation on its own footing/raft strip |
| Typical house application | Two 2.0 m walls per direction at the ground storey of an otherwise open plan; stair and lift shafts as a core |
| Fatal mistake | A shear wall that stops at first-floor level and lands on a beam — out-of-plane/in-plane discontinuity, the worst irregularity in the table |

### 7.6 Worked example — strong-column/weak-beam and joint shear, Karachi RC SMF house

Continues the §3.4 Karachi 2-storey RC SMF house (Zone 2B, R = 8.5, `V = 136 kN` at the base). Numbers
below are an illustrative single-joint check, not a full frame analysis — the actual joint forces depend
on the real grid, tributary widths and column/beam sizing the engineer sets.

**Given (ground-storey exterior joint, typical grid line):** columns 350 × 350 mm, `f'c = 21 MPa`,
`fy = 420 MPa`; beam 300 × 450 mm framing in from one side (single-bay exterior joint).

**Step 1 — beam probable moment strength `Mpr` (capacity-design shear source, §7.1 last row):**
```
As,top (beam, at column face) = 4 × 20 mm = 1257 mm², d = 400 mm
Mpr(beam) = 1.25 · As · fy · (d − a/2), a = 1.25·As·fy / (0.85·f'c·b)
a  = 1.25 × 1257 × 420 / (0.85 × 21 × 300) = 659,925 / 5,355 = 123 mm
Mpr = 1.25 × 1257 × 420 × (400 − 61.5) = 1.25×1257×420×338.5 ≈ 223.5 kNm
```

**Step 2 — required column moment capacity, strong-column/weak-beam (§7.1: ΣMnc ≥ 1.2 ΣMnb):**
```
ΣMnb (nominal, one beam framing in one direction) ≈ Mpr / 1.25 = 178.8 kNm   (nominal, not probable)
Required ΣMnc ≥ 1.2 × 178.8 = 214.6 kNm, split between column above and below the joint
→ each column ≥ 107.3 kNm nominal moment capacity at this axial load
```
A 350 × 350 mm column at this Zone 2B house's typical axial load (`Pu ≈ 0.15 Ag f'c` for a 2-storey
house) comfortably provides > 107 kNm with 8 × 20 mm bars (ρ ≈ 2%) — **the check is stated to show the
arithmetic path, not to substitute for the engineer's own interaction-diagram calculation**, which must
use the actual `Pu` at every load combination, not the illustrative value here.

**Step 3 — joint shear (ACI 318-19 §18.8):**
```
T (beam tension steel, at Mpr) = 1.25 × As × fy = 1.25 × 1257 × 420 = 659.9 kN
Vcol (column shear delivering the couple, estimated from storey shear / clear height) ≈ 30 kN (illustrative)
Vjoint = T − Vcol = 659.9 − 30 = 629.9 kN

Joint effective area Aj = column width × column depth = 350 × 350 = 122,500 mm²
Permissible joint shear (exterior joint, confined on 2 or fewer faces):
  φVn = φ × 1.0 × √f'c × Aj  (γ = 1.0 for this joint category, ACI Table 18.8.4.3)
      = 0.85 × 1.0 × √21 × 122,500 = 0.85 × 4.58 × 122,500 = 477,300 N ≈ 477 kN
```
**629.9 kN demand > 477 kN capacity → the joint as sized FAILS the shear check.** This is deliberately
left failing in the worked example to make the point concrete: fixing it means enlarging the column
(larger Aj), increasing joint confinement category, or reducing the beam's top steel / span — exactly
the kind of decision an SMF house needs its engineer to resolve at the design stage, not discover on
site. **Never treat the strong-column/weak-beam pass in Step 2 as sufficient on its own — the joint
shear check in Step 3 is a separate, independent gate, and either one can govern.**

---

## Section 8: Diaphragms, Roofs & Wall–Roof Connections

The lateral system only works if the floor and roof can collect the inertia force and deliver it to the
walls. In Pakistani houses this is where the assumption most often fails silently.

### 8.1 Roof / floor systems, ranked

| System | Diaphragm quality | Weight | Seismic verdict for houses |
|---|---|---|---|
| **RC solid slab, cast monolithic with tie beams** | Rigid — excellent | Heavy (~3.6 kPa self at 150 mm) | **Preferred** in all zones, provided the mass is accounted for and walls are tied into it |
| RC slab on a separate beam grid, not tied to walls | Rigid but disconnected | Heavy | Must be positively tied — add dowels/anchors into the tie beam |
| **Precast planks / hollow-core with a 50–75 mm RC topping + mesh, tied into a perimeter band** | Semi-rigid — acceptable | Medium | OK Zone ≤ 2B with the topping; **topping and perimeter tie are mandatory** |
| Precast planks with no topping | Poor — planks slide | Medium | **Not acceptable in Zone 2B+** |
| **CGI sheet on timber/steel trusses with a horizontal bracing plane + continuous roof band** | Flexible but tied | Very light | **Excellent seismic choice**, especially in Zone 3–4 rural/hill work |
| CGI on trusses with no bracing and no roof band | None | Light | Walls act independently out-of-plane and fail — very common |
| **Jack-arch roof (brick arches on steel joists)** | Very poor — thrust + no diaphragm | Heavy | **Do not use in Zone 2B+.** Legacy stock: retrofit with a tie plane and ties across the joists |
| **Heavy mud roof on timber joists** (traditional northern) | None | Very heavy (2–4 kPa+) | **The 2005 killer.** Replace with CGI in any repair; never specify new |
| Ferrocement / thin shell | Depends entirely on edge ties | Light | Engineered only |

### 8.2 Wall–roof / wall–floor connection rules

- Every wall must be tied to the diaphragm at its top: for RC slabs, the tie beam cast monolithic with
  the slab is the tie; for light roofs, a **continuous RC or steel roof band** with the roof members
  anchored to it (straps, holding-down bolts at ≤ 1.2 m) is the tie.
- **Anchorage force for a wall out-of-plane at the roof** (UBC-97 basis): `Fp = 4.0 · Ca · Ip · Wp`, with
  a floor around 4.0 kN/m of wall for ordinary cases. For the Zone 3 SD example (Ca = 0.36,
  Wp = 4.37 kN/m²): `Fp = 4.0 × 0.36 × 4.37 = 6.29 kN/m²` of wall tributary — design the anchors for
  this, not for nothing.
- Truss/joist bearing on masonry: minimum bearing 100 mm on a wall plate on the band, positively strapped;
  never a joist end simply pocketed into brickwork.
- **Diaphragm openings** (stairwell, light well, courtyard): keep total < 30% of the floor plate; provide
  a trimming beam and continuous chord reinforcement all round; never place a big opening adjacent to a
  wall the diaphragm has to deliver force into.
- **Courtyard houses** (very common in Pakistan): a central courtyard means the floor diaphragm is a ring.
  Ring diaphragms are weak in transferring force across the opening — provide a full perimeter tie beam
  on **both** the outer and courtyard edges, and treat the courtyard as a diaphragm discontinuity in the
  irregularity check.
- **Cantilever balconies / chajjas** must be anchored into the slab with top steel developed a full
  anchorage length into the backspan, and must not be the sole path for anything.

### 8.3 Staircase

- A stair flight is a diagonal strut. Options, in order of preference:
  1. Place the stair inside an RC shear-wall core (best — it becomes the lateral system).
  2. Tie it fully in and model the flights in the analysis.
  3. Separate it with a sliding joint at one end (a proper detail, not a gap left by accident).
- **Never** leave a stair to brace one corner of an otherwise symmetric plan — it is a torsion generator,
  and the half-landing creates short columns in any adjacent frame.
- Mid-landing beams framing into columns create the classic short-column condition in RC houses. If they
  must, hoop those columns at 100 mm over the full clear height.

---

## Section 9: Foundations, Soil & Site

| Item | Rule for houses |
|---|---|
| Plinth beam (grade beam) | **Mandatory in Zone 2B+**; continuous in both directions under every load-bearing wall and column line; min 230 × 300 mm, 4 × 12 mm bars, stirrups 6 mm @ 150 mm (@ 100 near intersections) |
| Isolated pad footings | Not acceptable alone in Zone 3–4 — **must be tied in both directions** with tie beams designed for ≥ 10% of the larger column's factored axial load (ACI/IBC practice) |
| Strip footings under masonry | Continuous, width per bearing capacity, min 2 × 10 mm longitudinal bars top and bottom; **step** (never slope) on gradients — step ≤ 600 mm vertical with ≥ 1.2 m horizontal run |
| Founding depth | ≥ 900 mm below finished ground, and below any expansive-clay active zone, fill, or topsoil |
| Mixed foundation types | **Never** mix pads and strips, or shallow and deep, under one continuous block — differential dynamic response cracks the superstructure |
| Raft | Appropriate for poor/variable soil, high water table, or where strip footings would overlap; thickness typically 250–450 mm for a house, with edge and internal beams |
| Split-level / hillside | Stepped footings + a tie beam at every step level; **never a row of columns of different free lengths** on a cut slope (short column + torsion). Retain the slope with an independent retaining structure, structurally separated from the house |
| Liquefaction screen | Saturated loose-to-medium sand (SPT N < 15) with water table < 10 m, in Zone 2B+ → **geotechnical investigation mandatory**. Relevant to Karachi and coastal Sindh, riverine Punjab/Sindh, Peshawar valley alluvium, and — as 2019 Mirpur showed — canal-side alluvium in AJK |
| Slope stability | 2005 Kashmir losses were heavily amplified by landslides. Do not site a house on, or immediately below, a marginal slope without a geotechnical assessment. Setback from a crest ≥ the slope height where feasible |
| Retaining walls | Design for seismic earth pressure (Mononobe–Okabe increment, roughly `ΔPae ≈ 0.375 kh γ H²` for typical geometry) — a static-only retaining wall next to a house is a common omission |
| Soil profile default | S2 / SD with no report; S3 / SE on soft alluvium — and state that a geotechnical report is required |
| Water table | Where it is within 2 m of founding level, drainage and waterproofing become structural issues (softening reduces bearing capacity under cyclic load) |

Companion: `architecture-geotechnical-foundations` for SBC determination, settlement limits and
under-reamed piles.

---

## Section 10: Non-Structural Elements — where the casualties actually come from

Falling non-structural elements cause a disproportionate share of injuries, and they are the cheapest
things in the whole project to fix.

| Element | Rule |
|---|---|
| **Boundary walls** | The classic Pakistani killer, and the biggest single cause of casualties in moderate events like 2019 Mirpur. 230 mm wall: max free height **1.8 m**, with 340 mm piers at ≤ 3.0 m centres, a continuous RC coping band on top, and a plinth beam at the bottom. Zone 3–4: vertical bars in each pier anchored into the foundation. **115 mm boundary walls: prohibited above 1.0 m.** Gate piers designed for the gate's dynamic load |
| **Parapets** | Max free height **600 mm** unreinforced; above that, vertical bars continuous from the roof band plus a coping beam. A 1.2 m unreinforced parapet on a 2-storey house is a guillotine |
| **Water tanks** | On the roof: sit over wall or column lines, never on a slender independent frame; strap the tank down; include the **full** tank mass in W. Underground tanks: check they do not undermine a footing |
| **Gas cylinders, geysers, boilers** | Strapped to a structural wall; **flexible connections** on all gas lines (post-earthquake fire is a secondary killer) |
| **Stone / tile cladding, chimneys, decorative copings** | Mechanically anchored above 3 m, never mortar-adhered alone |
| **Suspended ceilings, fans, heavy light fittings** | Positive mechanical fixing to the structural slab; ceiling fans on hooks embedded in the slab, never in a false-ceiling board |
| **Tall furniture, almirahs, bookcases, LPG heaters** | Anchored to walls — free advice worth giving every client |
| **Glazing** | Large panes need edge clearance for drift; laminated glass for anything over a circulation route |
| **Escape route** | At least one exit door that opens **outward** and is not blocked by a collapsible parapet, boundary wall, or overhead tank. Check the escape path against everything else in this table |

---

## Section 11: Timber-Laced & Alternative Vernacular Systems

The 2005 reconstruction found that traditional timber-laced systems markedly outperformed unreinforced
masonry, and ERRA subsequently approved several for reconstruction. Worth knowing for hill sites, rural
work, heritage repair, and any project without a reliable cement supply chain.

| System | What it is | Seismic behaviour | Practical spec |
|---|---|---|---|
| **Dhajji dewari** | Timber frame with small masonry infill panels ("patchwork quilt" wall) | **Excellent** — many small panels give many small energy-dissipating cracks; light; failure is graceful | Timber studs/braces at ≤ 1.0–1.2 m forming triangulated panels; infill of brick or stone in mud/lime mortar; continuous timber wall plate; light CGI roof; max 2 storeys |
| **Bhatar / cator-and-cribbage** | Horizontal timber lacing bands laid through a stone masonry wall at regular vertical intervals | **Good** — the timber bands act as the tie beams the wall otherwise lacks | Timber runners every 600–900 mm vertically, both wythes, cross-ties at ≤ 1.0 m; through-stones between; wall thickness ≥ 450 mm |
| **Taq** | Timber-laced brick masonry with heavy timber ladder bands at floor levels | Good | Ladder bands at every floor and at lintel level |
| **Confined masonry** | §4 | Very good | The modern default |
| **Adobe / mud block** | Sun-dried earth blocks | **Poor** — 2013 Awaran destroyed this stock almost totally | **Not acceptable in Zone 3–4** without stabilisation, confinement, light roof and an engineer. Never for a new build in a high zone |
| **Random rubble in mud mortar** | Uncoursed stone, mud mortar | **Very poor** — delaminates out-of-plane | Only with through-stones ≤ 1.2 m, bands, light roof — and preferably not at all |
| **Light-gauge steel / timber platform frame** | Studs + sheathing | **Very good** — light, ductile, high redundancy | Rare and expensive in Pakistan; needs a supply chain and a competent erector. IRC bracing tables (WSP/CS-WSP) are the relevant prescriptive reference |

**Universal rules for all vernacular systems:** light roof, continuous horizontal lacing/bands, positive
wall-to-roof connection, plan regularity, and no more than 2 storeys. The system does not save an
irregular plan.

---

## Section 12: Retrofitting Existing Houses

Most of Pakistan's housing stock is unreinforced masonry with no confinement. The ERRA/UNDP post-2005
reconstruction programme validated a small set of low-tech interventions.

| Technique | What it does | Typical spec |
|---|---|---|
| **Splint and bandage** (jacketing strips) | Adds the missing tie system to an existing URM wall | Vertical "splints" at corners and opening jambs + horizontal "bandages" at lintel and eaves level, formed with welded wire mesh (12–14 gauge, 25–50 mm grid) anchored with through-bolts at ≤ 450 mm and covered with 25–40 mm of micro-concrete or rich cement plaster |
| **Corner stitching** | Restores box action at corners | Diagonal or L-shaped mesh/rebar stitches across both faces of every external corner, anchored through the wall |
| **Through-stones / through-bolts** | Connects the two wythes of a rubble or two-leaf wall so it cannot delaminate | Through elements at ≤ 1.2 m horizontally, ≤ 600 mm vertically |
| **Added lintel / eaves band** | Retrofits the missing horizontal band | Surface-mounted RC band or paired steel angles, fully continuous, anchored at ≤ 600 mm |
| **Roof diaphragm improvement** | Stops the roof spreading the walls apart | Horizontal bracing plane in a timber/CGI roof; plywood or diagonal bracing; positive straps from roof members into the wall band |
| **Ferrocement / shotcrete overlay** | Adds in-plane strength to a weak wall | 30–40 mm overlay with mesh on both faces, connected through the wall; treat as a structural change requiring design |
| **New shear wall / buttress insertion** | Fixes a wall-density failure | New RC wall on its own foundation, positively tied into the existing diaphragm at each level |
| **Removing the hazard** | Cheapest of all, and often the most effective | Demolish heavy mud roof overlays, oversized parapets, unbraced boundary walls; replace a heavy roof with CGI |
| **Short-column cure** | Eliminates a brittle mechanism | Either complete the infill full height, or cut a full-height isolation gap; add jacketing hoops @ 100 mm over the full clear height |

**Retrofit triage order** for an existing house:
1. Life-threatening non-structural items (parapets, boundary walls, roof tank, cladding).
2. Out-of-plane wall restraint and the roof–wall connection.
3. Corners and box action.
4. In-plane strength (wall density).
5. Foundation.

Doing (4) before (2) is a common and dangerous inversion: a strengthened wall that still cannot span
out-of-plane simply fails the same way with more mass. **Every retrofit above cosmetic level needs the
PEC-registered engineer too** — retrofit design is harder than new design, not easier.

---

## Section 13: Base Isolation & Advanced Systems — honest assessment

**Verdict: technically real, essentially inapplicable to ordinary Pakistani house budgets today.**

- Base isolation decouples the superstructure from ground motion with flexible bearings, cutting
  superstructure accelerations dramatically. It is proven and appropriate for hospitals, data centres,
  museums and critical infrastructure.
- **Japan is the only country with meaningful base-isolated single-family housing stock (~5,000 houses)**,
  and those use highly engineered, factory-produced systems inside a regulatory and inspection framework.
- **No code-approved commercial base-isolation product for Pakistani single-family houses was found**, and
  no verified cost-premium figure exists for that market. Cost, fabrication tolerance, the moat/clearance
  detail, flexible service connections, and long-term maintenance and inspection are the binding
  constraints — not physics.
- Research-stage low-cost options for developing-country masonry housing do exist and are worth knowing:
  - **Unbonded fibre-reinforced elastomeric isolators (U-FREI)** — recycled rubber with fibre
    reinforcement instead of steel plates; lower manufacturing cost, higher damping, shorter operational
    height than conventional bonded steel-reinforced bearings.
  - **Rolling-ball isolators** — a ball between a flat and a concave concrete plate; laboratory concept.
  - Both are research-grade: no Pakistani code path, no supply chain, no maintenance regime, no installer
    base.
- Base isolation also **requires** things a Pakistani house usually cannot provide: a stiff, well-tied
  superstructure above the isolation plane (an isolated bad building is still a bad building), a
  continuous seismic gap all round, and flexible water/gas/electrical connections across the gap.
- **What to say when a client asks for base isolation on a house:** *"It is real engineering, but for a
  Pakistani house the same money spent on confined-masonry detailing, wall density, plan regularity and
  removing the soft storey buys far more life safety per rupee. Base isolation makes sense here only for
  an essential facility with an engineer and a budget for bearings and their inspection."*
- Related systems with the same verdict for houses: viscous dampers, tuned mass dampers,
  buckling-restrained braces, friction pendulum bearings. All are engineered-building tools.

---

## Section 14: What Seismic Resistance Actually Costs

Clients resist ties because they believe they are expensive. They are not — the quantities are small and
checkable. Below is the **quantity delta** for adding a full confining system to a 100 m²/floor, 2-storey
brick house (40 m of wall run per storey, 3.2 m storey height, 16 tie columns per storey, 60 m of band run
per band, 2 bands per storey). Apply current rates from `architecture-cost-estimation-boq`.

| Item | Quantity per storey | Basis |
|---|---|---|
| Tie-column concrete | 16 × 0.169 = **2.7 m³** | 230 × 230 × 3200 mm each |
| Tie-column steel | 16 × 16 kg = **256 kg** | 4 × 12 mm + 6 mm ties |
| Tie-beam concrete (2 bands) | 120 m × 0.053 = **6.4 m³** | 230 × 230 mm section |
| Tie-beam steel (2 bands) | 120 m × 4.7 kg = **564 kg** | 4 × 12 mm + 6 mm stirrups |
| **Total added per storey** | **≈ 9.1 m³ concrete, ≈ 820 kg steel** | |
| **Per m² of floor area** | **≈ 0.09 m³/m² concrete, ≈ 8 kg/m² steel** | |

Interpretation:
- 8 kg/m² of steel is roughly **a quarter to a fifth** of what a full RC frame house uses (25–45 kg/m²).
- Against a typical Pakistani grey-structure cost, a full confining system usually lands in the region of
  **a single-digit percentage** of grey-structure cost — small compared with what people spend on
  finishes. **State it as a percentage of grey structure, computed from live rates, never as a memorised
  rupee figure.**
- The genuinely expensive seismic decisions are the ones about **configuration**: adding shear walls to
  rescue an open ground floor, splitting an L-plan with a joint, or engineering a cantilever. Which is
  another argument for fixing the configuration at concept stage, when it is free.
- The most cost-effective seismic spending, in order: (1) plan regularity — free; (2) correct construction
  sequence and 135° hooks — free; (3) light roof instead of heavy — often cheaper; (4) bands and tie
  columns — small; (5) shear walls — moderate; (6) full ductile frame — large; (7) base isolation — not
  applicable.

---

## Section 15: Lessons from Real Pakistan Earthquakes → Rules

| Event | What happened | Rule it generates |
|---|---|---|
| **1935 Quetta, Mw 7.7** (~30,000+ deaths) | Unreinforced masonry and mud houses pancaked; led to the "Quetta bond" — horizontal reinforcement laid in brickwork | Horizontal reinforcement / bands in masonry are a **century-old Pakistani lesson**, not an imported novelty |
| **2005 Kashmir, Mw 7.6** — **~87,000 deaths**, 272,019 buildings destroyed, 182,886 damaged, >3.5 m homeless, >$5 bn losses, **>90% of surveyed engineered buildings at damage grade 4–5** | Dominant modes: **soft ground storeys, short columns, plan and elevation irregularity, undetailed RC frames, poor construction quality, heavy roofs on weak walls**; thousands of school buildings collapsed during class hours; landslides amplified losses | Every rule in §4, §6, §7 and §8. The damage concentrated in **configuration and detailing**, not in exotic analysis — which is why this skill spends its length there. **The death toll, not the buildings-destroyed count, is the reason this document exists** |
| **2005 Kashmir — what survived** | Timber-laced systems (**dhajji dewari**, **bhatar**) markedly outperformed URM; ERRA later approved dhajji for reconstruction | Distributed ductile connections + light weight beat mass and rigidity. A light, well-tied house outperforms a heavy, untied one |
| **2013 Awaran, Balochistan, Mw 7.7** | Near-total destruction of adobe / mud-block housing across a wide rural area | Adobe and mud-block have no place in Zone 3–4 without engineered stabilisation, confinement and a light roof |
| **2019 Mirpur AJK, Mw 5.6** | A *moderate* event caused severe damage — surface faulting, liquefaction along canal alluvium, and widespread boundary-wall and infill failures | Moderate shaking on bad soil with bad detailing is enough. **Soil matters; boundary walls kill.** Magnitude is not the design variable — site and detailing are |
| **2015 Hindu Kush, Mw 7.5 (deep)** | Wide felt area, damage concentrated in already-weak stock in KP | A deep, distant event still finds every unconfined wall in the province |

### 15.1 The distilled do/don't card (put this on the first drawing sheet)

**DO**
1. Simple, symmetric, compact rectangular plan (aspect ratio ≤ 2:1).
2. Same walls and columns at every storey, foundation to roof.
3. Tie beams at plinth, lintel, floor and roof — **continuous, everywhere, closing a loop**.
4. Tie columns at every corner, junction, wall end and both jambs of wide openings; ≤ 4.5 m apart in
   Zone 3–4.
5. Masonry built first; tie elements cast against toothed edges afterwards.
6. 135° hooks, 75 mm extension, ties closed up to 100 mm near every joint.
7. Meet the wall-density table in **both** directions at **every** storey.
8. Light roof; if RC, tie the slab into every wall band and count its mass.
9. Plinth beam and a continuous, tied foundation of one single type.
10. Separation joint between blocks of different height or shape, and level alignment with the neighbour.

**DON'T**
1. No open ground storey under a heavier storey.
2. No short columns from partial-height infill, sills, ventilators, mid-landings or sloping ground.
3. No corner windows; no openings within 600 mm of a wall junction.
4. No 4.5" walls carrying load; no ungrouted hollow blocks in Zone 2B+.
5. No 90° hooks, no ties skipped at joints, no laps inside joints or at column bases.
6. No heavy roof, overhead tank or tall parapet without design and anchorage.
7. No cast-first columns with tight-packed infill called "confined masonry".
8. No mixing foundation types under one block.
9. No extra storey later without re-checking density, W, drift and the foundation.
10. No construction from this skill's output without a PEC-registered engineer's stamp and authority
    approval.

---

## Section 16: Encoding the Rules in a FreeCAD Model

Pairs with `architecture-freecad-bim` (Site/Building/Storey hierarchy, parametric openings via
Subtractions, FEM pipeline) and `architecture-structural-systems`.

### 16.1 Modelling conventions

- Model tie columns as **separate Arch Structure objects with `IfcType = "Column"`**, never merged into
  the wall solid — this makes them countable, checkable, and exportable to IFC for the engineer.
- Model tie beams as `IfcType = "Beam"` running along wall tops; set each one's `Description` to
  `TIE-BEAM PLINTH` / `LINTEL` / `FLOOR` / `ROOF`.
- Give every load-bearing wall `Width = 0.23 m` and tag partitions `0.115 m`, so the density script can
  exclude them automatically.
- Keep walls axis-aligned (0° / 90°). A non-orthogonal wall is a nonparallel-system irregularity flag
  anyway, and the script will report it as one.
- Put a property set on the **Building** object recording `SeismicZone`, `Z`, `SoilProfile`, `S` or
  `Ca`/`Cv`, `I`, `R` or `Rw`, `T`, `W`, `V`, and **which formulation was used** — so the model
  self-documents its design basis and cannot be silently reinterpreted later.
- Model openings as real parametric `Subtractions`, not frozen booleans, so the density script can be
  extended to net them off.
- Model the roof water tank as a real object with real mass, at its real location. It is the most
  commonly forgotten 20–30 kN in the whole building.

### 16.2 Wall-density check script (FreeCAD Python console, or via `mcp__freecad__execute_code`)

```python
import FreeCAD as App, math

doc = App.ActiveDocument
MIN_STRUCTURAL_T = 200.0          # mm — below this it's a partition
MIN_PIER_LENGTH  = 1200.0         # mm — shorter contributes ~nothing in shear
FLOOR_AREA_M2    = 100.0          # set from the plan
REQUIRED_PCT     = 3.5            # from Section 5.1 for this zone / storey count

ax = ay = 0.0                     # counted wall cross-section area, mm^2, per direction
skipped = []

for o in doc.Objects:
    if getattr(o, "IfcType", "") != "Wall":
        continue
    t = float(o.Width.Value)
    L = float(o.Length.Value)

    # net off modelled openings (doors/windows as Subtractions)
    for sub in getattr(o, "Subtractions", []):
        try:
            L -= float(sub.Width.Value)
        except Exception:
            pass

    if t < MIN_STRUCTURAL_T:
        skipped.append((o.Name, "partition", t)); continue
    if L < MIN_PIER_LENGTH:
        skipped.append((o.Name, "short pier after openings", round(L, 0))); continue

    rot = o.Placement.Rotation
    ang = math.degrees(rot.Angle * (1 if rot.Axis.z >= 0 else -1)) % 180.0
    if   ang < 15 or ang > 165: ax += t * L
    elif 75 < ang < 105:        ay += t * L
    else: skipped.append((o.Name, "NON-ORTHOGONAL - IRREGULARITY FLAG", round(ang, 1)))

area_mm2 = FLOOR_AREA_M2 * 1e6
dx, dy = 100 * ax / area_mm2, 100 * ay / area_mm2
print(f"wall density X = {dx:.2f}%  (need {REQUIRED_PCT}%)  -> {'PASS' if dx >= REQUIRED_PCT else 'FAIL'}")
print(f"wall density Y = {dy:.2f}%  (need {REQUIRED_PCT}%)  -> {'PASS' if dy >= REQUIRED_PCT else 'FAIL'}")
ratio = dx / dy if dy else float('inf')
print(f"X/Y balance = {ratio:.2f}  -> {'OK' if 0.7 <= ratio <= 1.4 else 'TORSION RISK'}")
for s in skipped:
    print("  skipped:", s)
print("\nPRELIMINARY CHECK ONLY - NOT A STRUCTURAL DESIGN - PEC ENGINEER REVIEW REQUIRED")
```

*(Opening netting depends on openings being modelled as `Subtractions` with a `Width` property. Verify
against the plan before trusting the number; run it once per storey.)*

### 16.3 Model-level seismic checklist before exporting anything

- [ ] Tie column present at every external corner, every wall T/L junction, every free wall end
- [ ] Tie column at both jambs of every opening > 1.2 m
- [ ] Max tie-column spacing along any wall ≤ 4.5 m (Zone 3–4) / 6.0 m (Zone 1–2B)
- [ ] Tie beams modelled at plinth, lintel, each floor and roof — continuous loops, no gaps at doors
- [ ] Gable band modelled on any gable wall
- [ ] Wall-density script passes in X **and** Y at **every** storey
- [ ] X/Y density ratio between 0.7 and 1.4
- [ ] Ground-storey counted wall length ≥ upper-storey counted wall length (no soft storey)
- [ ] Identical wall/column footprint at every storey (vertical continuity)
- [ ] No wall or column whose clear height is partially braced by an adjacent lower wall (short column)
- [ ] Plan aspect ratio ≤ 3:1; any re-entrant projection ≤ 15% or a separation joint modelled
- [ ] Diaphragm openings (stair, courtyard, light well) ≤ 30% of the floor plate, trimmed
- [ ] Openings satisfy §4.5 (total length, pier width, distance from junction, vertical spacing)
- [ ] Parapets ≤ 600 mm unreinforced; roof tank modelled with real mass, over a wall line
- [ ] Boundary wall modelled with piers at ≤ 3.0 m and free height ≤ 1.8 m
- [ ] Building object carries the design-basis property set (zone, Z, soil, I, R/Rw, T, W, V, formulation)
- [ ] A visible note on every exported sheet: **PRELIMINARY — NOT FOR CONSTRUCTION — REQUIRES
      PEC-REGISTERED STRUCTURAL ENGINEER REVIEW AND LOCAL AUTHORITY APPROVAL**

---

## Section 17: Site Supervision & Handoff

### 17.1 Site quality-control checklist (give to the client / supervisor)

- [ ] Bricks: first class, soaked before laying; reject under-burnt / khingar
- [ ] Mortar measured by box, not by shovel-eye; 1:6 minimum, 1:4 for the Zone 3–4 ground storey
- [ ] All bed **and** perpend joints fully filled; joint thickness 10–12 mm
- [ ] Toothing or dowels present at every tie-column location **before** the cage goes in — photograph it
- [ ] Tie-column cages: 4 × 12 mm min; ties **135° hooks with 75 mm extension**; closed up to 100 mm
      within 450 mm of both ends
- [ ] Concrete: min 1:2:4 / f'c ≥ 17.5 MPa; slump controlled; **vibrated**, not rodded-and-hoped
- [ ] No cold joint mid-height in a tie column — pour the full storey height in one go
- [ ] Tie beams continuous — physically walk the loop and confirm it closes
- [ ] Bands not interrupted at doorways, ducts or the stair
- [ ] Curing: 7 days minimum for all concrete and masonry
- [ ] No chases cut in tie columns or in counted shear walls after casting
- [ ] Roof-to-wall straps/anchors installed on light roofs before sheeting
- [ ] Photographs of **every** reinforcement cage before concrete, dated and filed

### 17.2 What to hand the PEC-registered structural engineer

1. Site: exact location, BCP zone, distance to the nearest mapped fault, geotechnical report — or an
   explicit written statement that none exists.
2. Architectural plans, elevations, sections at all levels, plus the IFC / FreeCAD model.
3. The assumed design basis: **which formulation**, Z, I, soil profile, S or Ca/Cv, R or Rw, T, the W
   build-up, V, and the storey forces (as in §3).
4. The wall-density calculation per direction per storey, with the counting assumptions stated.
5. The irregularity checklist (§6.3), with every flag called out honestly rather than quietly dropped.
6. Intended materials: brick strength, mortar mix, concrete grade, steel grade, roof system.
7. **A list of everything the client refuses to change** (e.g. "the ground floor must be open for
   parking") — so the engineer designs for reality rather than discovering it on site.
8. The non-structural schedule (§10) — boundary wall, parapet, tank — which is routinely left out of a
   structural brief and is where the casualties come from.

### 17.3 Anti-patterns for Claude / Claude using this skill

- Quoting a zone factor without saying the official map must be checked.
- Giving a base shear without naming the formulation (§3.1) — the two differ by ~45%.
- Mixing an `Rw` with a `Ca/Cv` calculation, or an `R` with `1.25S/T^(2/3)`.
- Producing a rebar schedule that reads like a construction document.
- Saying "this design is earthquake-proof". Nothing is. The phrase is *"designed to reduce the risk of
  collapse in the design-level earthquake, subject to engineer review"*.
- Letting a client's plan request (open ground floor, corner window, cantilevered upper floor) pass
  without naming the seismic consequence out loud.
- Asserting that BCP 2007 contains a prescriptive house table — it does not (§2). The HSC table is
  synthesised by this skill and must be labelled as such every time it is used.
- Treating the BCP zone as the ceiling of real hazard when post-2007 hazard studies say otherwise.
- Recommending base isolation for an ordinary house.
- Quoting a memorised rupee cost for the confining system instead of deriving it from §14 quantities and
  live rates.
- Going quiet about the licensing requirement because the user sounds knowledgeable.
- Quoting the §1.2 Islamabad/Rawalpindi row (or any city→zone row) as a final zone number without the
  verify-against-the-map caveat attached — that pair is explicitly flagged as disputed in this skill.
- Presenting the §3.3 `v_d ≈ 0.20 MPa` cross-check stress as a validated design value rather than the
  assumed placeholder it is.

---

## Section 18: Known Gaps in This Skill (state these when relevant)

1. **The HSC table (§2.1) is synthesised, not code.** Pakistan has no prescriptive seismic tier for
   houses. Always label it.
2. **BCP SP:07 numeric tables were not machine-extractable** during research (binary PDF). Zone factors
   and the force procedure are well corroborated; the confined-masonry numbers are the practical
   EERI/WHE + IS 4326 baseline. **Cross-check against NDMA's current Earthquake Guidelines and IS 4326
   before publishing any hard number in a construction document.**
3. **BCP 2021 (PKBC 2021)** is IBC-based and supersedes parts of the 2007 provisions. Which document the
   local authority actually enforces varies. Confirm per authority; where they differ, design to the more
   onerous.
4. **The Ca/Cv, Na/Nv and R tables (§1.5–1.7)** are the standard UBC-97 values reproduced from secondary
   sources. Verify against the code text before design use.
5. **Wall-density values (§5.1)** are approximations of simplified guide tables calibrated for solid clay
   brick. They are not a Pakistani code table.
6. **The masonry shear stress `v_d ≈ 0.20 MPa` (§3.3) is an assumed placeholder, flagged inline at the
   point of use, not only here.** Real values depend on tested brick and mortar strength and axial
   precompression.
7. **No verified cost-premium percentage** for seismic detailing or base isolation in the Pakistani market
   was found. §14 gives quantities, deliberately, not prices.
8. **Post-2007 hazard research** suggests the zoning map underestimates ground motion in places. This
   skill flags it but cannot substitute a site-specific PSHA.
9. **Soil–structure interaction, vertical ground motion, and near-fault pulse effects** are outside scope
   — they matter for Zone 4 sites near the Chaman system and are the engineer's territory.
10. **Nothing here has been validated against a physical test or a real post-earthquake survey by this
    skill's author.** It is a distillation of published guidance and reconnaissance findings.
11. **The §1.2 city→zone table is disputed for at least one entry** (Islamabad/Rawalpindi — listed here
    as Zone 3, but some Pakistani engineering references cite the official BCP-2007 map as Zone 2B for
    that pair). Flagged inline in §1.2; treat every row in that table as a starting point for verification,
    not a citable zone.

---

## Appendix A: Standards Cited

- **Building Code of Pakistan — Seismic Provisions 2007 (BCP SP:07)**, Ministry of Housing & Works /
  Pakistan Engineering Council — zoning map, Z factors, static lateral force procedure (UBC-derived).
- **Building Code of Pakistan 2021 (PKBC 2021)** — IBC-based, hosted at codes.iccsafe.org.
- **UBC-97 (Uniform Building Code 1997)** — `V = Cv I W/(RT)`, caps `2.5 Ca I W/R` and floor
  `0.11 Ca I W`, Tables 16-Q (Ca), 16-R (Cv), 16-N (R), near-source factors Na/Nv, §1632 non-structural
  element forces, drift limits.
- **UBC-94** — `V = Z I C W / Rw`, `C = 1.25 S / T^(2/3) ≤ 2.75`, `C/Rw ≥ 0.075`; the formulation most
  often quoted in Pakistani house practice.
- **ASCE/SEI 7-22**, Ch. 11 (seismic design criteria), Ch. 12 — **Table 12.3-1** horizontal
  irregularities, **Table 12.3-2** vertical irregularities, §12.8 equivalent lateral force, §12.8.4
  accidental torsion, Ch. 13 non-structural components.
- **IRC 2021**, Table R301.2.2.1.1 (Seismic Design Category from ASCE 7-22), §R602.10.10.1 (cripple-wall
  bracing limits in SDC C / D0 / D1; engineered design required for 1–2 family dwellings above two
  storeys in SDC D2) — the comparative model for the prescriptive tier Pakistan lacks.
- **ACI 318-19**, Chapter 18 (Earthquake-Resistant Structures) — SMF/IMF detailing, §18.6 beams,
  §18.7.3.2 strong column–weak beam, §18.7.5 column confinement and the `hx ≤ 200 mm (8 in)` tightening
  (Table 18.7.5.4), §18.8 joints, §18.10 special structural walls; §5.3 load combinations;
  Table 20.5.1.3 cover.
- **IS 4326:1993** — Earthquake Resistant Design and Construction of Buildings, Code of Practice;
  Cl. 8.3 / Table 4 opening rules; band and vertical-reinforcement detailing. Routinely cross-referenced
  in Pakistani practice. Companion: **IS 13828** (low-strength masonry), **IS 13935** (repair and
  seismic strengthening).
- **EERI / World Housing Encyclopedia — Seismic Design Guide for Low-Rise Confined Masonry Buildings**
  (Brzev & Meli) — confinedmasonry.org, world-housing.net; wall density, tie spacing, H/t limits,
  toothing details.
- **NDMA Pakistan Earthquake Guidelines (2025)** and **NDMA Infrastructure Audit Guidelines** —
  ndma.gov.pk.
- **ERRA / UNDP post-2005 reconstruction guidelines** — dhajji dewari and bhatar approvals, splint-and-
  bandage retrofit specifications.
- **EERI Kashmir Earthquake Reconnaissance Report (2005)** and **NZSEE Bulletin** damage studies — the
  failure-mode evidence base for §6, §7 and §15.
- Local authority byelaws: **LDA, CDA, RDA, KDA/SBCA, PDA, GDA, TMA / Cantonment Board** — always
  governing on top of the code.

## Appendix B: Quick-Reference Constants

| Constant | Value |
|---|---|
| Zone factors Z | 0.075 / 0.15 / 0.20 / 0.30 / 0.40 (Zones 1, 2A, 2B, 3, 4) |
| PGA bands | 0.05–0.08 / 0.08–0.16 / 0.16–0.24 / 0.24–0.32 / >0.32 g |
| C cap (Form A) | 2.75 (governs for essentially all houses) |
| C/Rw floor (Form A) | 0.075 |
| V cap (Form B) | 2.5 Ca I W / R  (governs for essentially all houses) |
| V floor (Form B) | 0.11 Ca I W; plus 0.8 Z Nv I W / R in Zone 4 |
| Ct (metric) | 0.0488 masonry / bearing wall; 0.0731 RC moment frame |
| Rw (UBC-94) | 6 confined/reinforced masonry; 8 IMF; 12 SMF/dual |
| R (UBC-97) | 4.5 masonry bearing wall; 5.5 IMF / building frame; 8.5 SMF/dual |
| Default soil, no report | S2 (S=1.2) / SD (Ca, Cv from §1.7) |
| Base shear, Zone 3 confined masonry | ≈ **0.138 W** (Form A) / **0.200 W** (Form B, SD) |
| Base shear, Zone 4 confined masonry | ≈ **0.183 W** (Form A) / **0.244 W** (Form B, SD, Na=1) |
| Max tie-column spacing | 4.5 m (Zone 3–4) / 6.0 m (Zone 1–2B); also ≤ 1.5 × storey height |
| Max tie-beam vertical spacing | 3.0 m |
| Tie-column min steel | 4 × 12 mm; ties 6 mm @ 200 mm (100 mm within 450 mm of ends) |
| Tie-beam min steel | 4 × 12 mm; stirrups 6 mm @ 150–200 mm |
| Seismic hook | **135°**, extension ≥ 6 d_b and ≥ 75 mm (3") |
| Wall H/t limit | ≤ 25 (1–2 storey); ≤ 20 (3 storey) |
| Min structural wall thickness | 230 mm (9") |
| Min wall length counted in density | 1.2 m, and length/height ≥ 0.4 |
| Wall density, Zone 3, 2 storey | 3.5% per direction, ground storey |
| Wall density, Zone 4, 2 storey | 4.5% per direction, ground storey |
| Opening total length limit | 0.50 L (1 storey) / 0.42 L (2) / 0.33 L (3) |
| Min distance, wall junction to opening | 0.5 m (1 storey) / 0.6 m (2–3 storey) |
| Soft storey | < 70% stiffness of storey above (extreme < 60%) |
| Weak storey | < 80% strength of storey above (extreme < 65%) |
| Torsional irregularity | drift ratio > 1.2 (extreme > 1.4) |
| Re-entrant corner | projection > 15% of plan dimension |
| Mass irregularity | storey mass > 150% of adjacent |
| Diaphragm discontinuity | opening > 50% of gross area (keep houses ≤ 30%) |
| ACI hx tightening trigger | Pu > 0.3 Ag f'c or f'c > 70 MPa → hx ≤ 200 mm (8 in) |
| ACI column confinement length lo | max(member depth, clear span/6, 450 mm) |
| Drift limit (T < 0.7 s) | Δm ≤ 0.025 h  (masonry service target ≤ 0.004 h) |
| Seismic separation joint (6.4 m tall house) | ≈ 75 mm; between buildings √(δ1²+δ2²) |
| Parapet, unreinforced max free height | 600 mm |
| Boundary wall (230 mm), max free height | 1.8 m with 340 mm piers @ ≤ 3.0 m + coping band |
| Confining system quantity delta | ≈ 0.09 m³/m² concrete, ≈ 8 kg/m² steel of floor area |
| 2005 Kashmir death toll | ≈ 87,000 (Mw 7.6) — the number that justifies this entire skill |

## Appendix C: One-Page Spec Sheet by Zone (confined masonry house, 1–2 storey)

| Item | Zone 1 | Zone 2A | Zone 2B | Zone 3 | Zone 4 |
|---|---|---|---|---|---|
| HSC | H1 | H2 | H2 | H3 | H4 |
| Z | 0.075 | 0.15 | 0.20 | 0.30 | 0.40 |
| Base shear (Form B, SD, R=4.5) | 0.067 W | 0.122 W | 0.156 W | 0.200 W | 0.244 W·Na |
| URM permitted | Discouraged | Discouraged | **No** | **No** | **No** |
| Max storeys, confined masonry | 3 (engineer) | 3 (engineer) | 3 (engineer) | 2 | 2 |
| Wall density, 1 storey | 1.0% | 1.0% | 1.5% | 2.0% | 2.5% |
| Wall density, 2 storey (ground) | 1.5% | 1.5% | 2.5% | 3.5% | 4.5% |
| Tie-column spacing | ≤ 6.0 m | ≤ 6.0 m | ≤ 6.0 m | ≤ 4.5 m | ≤ 4.5 m |
| Tie-column steel | 4 × 12 mm | 4 × 12 mm | 4 × 12 mm | 4 × 12 mm (16 mm at 3 storey) | 4 × 16 mm ground storey |
| Bands required | Plinth + roof | Plinth + lintel + roof | Plinth + lintel + floor + roof | All, + gable band | All, + gable band |
| Mortar (ground storey) | 1:6 | 1:6 | 1:6 | **1:4** | **1:4** |
| Concrete f'c | 17.5 MPa | 17.5 MPa | 17.5 MPa | **20 MPa** | **20 MPa** |
| Plinth beam | Recommended | Recommended | **Mandatory** | **Mandatory** | **Mandatory** |
| Isolated pads allowed untied | Yes | Yes | Tie recommended | **Must be tied** | **Must be tied** |
| Corner windows | Allowed | Allowed | **No** | **No** | **No** |
| Hollow block, ungrouted | Allowed | Allowed | **No** | **No** | **No** |
| Geotechnical report | Recommended | Recommended | Recommended | **Required** | **Required** |
| Engineer | Required for approval | Required | Required | **Required, full design** | **Required, full analysis** |

**Every column of this table is preliminary planning guidance. None of it authorises construction.**
