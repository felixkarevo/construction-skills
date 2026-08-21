---
name: architecture-concrete-reinforcement-detailing
description: >
  Reinforced cement concrete (RCC) design aids and rebar detailing reference for
  residential construction — concrete grades and mix ratios (M15/M20/M25), concrete
  cover requirements, development and lap splice lengths, minimum and maximum steel
  ratios, footing/column/beam/slab/staircase reinforcement detailing, stirrup and
  tie spacing rules, beam-column joint detailing, bar bending schedules and steel
  quantity estimation, and the specific rebar detailing mistakes that cause real
  house failures. Cites ACI 318-19 clause by clause with Building Code of Pakistan
  (BCP-SP 2007 / BCP 2021) seismic detailing overlay and Pakistani site practice.
---

# Concrete & Reinforcement Detailing for Residential Construction

This skill converts RCC code requirements into usable numbers for house-scale work:
1–3 storey residential frames and load-bearing-with-RCC-slab construction, of the kind
built across Pakistan and South Asia. It exists so that a plan, a FreeCAD BIM model, or a
bar bending schedule produced during design carries realistic member sizes, realistic
steel, and detailing that would survive an engineer's review — rather than plausible-looking
numbers invented on the spot.

Every numeric value below is tagged with its source clause. Where a value is industry
practice rather than a code clause, it is labelled **[practice]**. Where the exact table
value must be read from the primary document before being quoted to a client or authority,
it is labelled **[VERIFY]** and listed again in Section 18.

---

## Reality Check - Licensing & Liability

**This skill produces design aids and calculation guidance for planning and FreeCAD modeling ONLY.**

- Nothing in this file is a structural design. It is a set of preliminary sizing rules,
  detailing conventions, and code-clause pointers used to make a drawing or a 3D model
  plausible and internally consistent.
- **Any design intended for actual construction of a real occupied building MUST be reviewed,
  sealed, and stamped by a licensed structural engineer** — in Pakistan, a Pakistan Engineering
  Council (PEC) registered professional engineer with the relevant category; elsewhere, the
  equivalent locally licensed engineer of record.
- **The design MUST also pass local authority plan approval before construction** — LDA
  (Lahore), CDA (Islamabad), KDA/SBCA (Karachi), RDA (Rawalpindi), WASA/TMA/Cantonment Board
  byelaws, DHA/Bahria design vetting cells, or the relevant development authority. Approval
  covers setbacks, height, FAR/covered-area limits, and structural vetting — not just structure.
- **Claude / Claude must never present FreeCAD output, a bar bending schedule, or any
  calculation in this skill as construction-ready.** Rebar drawn in a BIM model is geometry,
  not a design check. A member that looks right in 3D can still be unsafe.
- **Say this unprompted.** If a user starts talking as though the output is final — asks for
  a BBS to hand to a steel fixer, asks "how much steel should I order", says "we're pouring
  next week", asks to send the drawing to a contractor, or asks for a stamped-looking
  drawing — stop and state plainly that a PEC-registered structural engineer must run the
  actual analysis and stamp the drawings, and that local authority approval is required.
  Do not wait to be asked.
- **Never fabricate a stamp, seal, PEC number, engineer's name, or approval reference**, and
  never format output so it could be mistaken for an approved drawing.
- Seismic design in particular is out of scope for a design aid. Pakistan sits across UBC-97
  seismic Zones 1 through 4 (BCP-SP 2007); zone, soil profile, and irregularity checks change
  member sizes and detailing substantially and require real analysis.

---

## Section 1: Which Code Governs What

### 1.1 Code hierarchy for a Pakistani residential project

| Document | Status | What it governs here |
|---|---|---|
| **ACI 318-19** (reapproved 2022), *Building Code Requirements for Structural Concrete* | Primary technical reference for RCC design/detailing in Pakistan | Member strength design, cover, development length, lap splices, minimum/maximum steel, tie and stirrup spacing, joint detailing |
| **Building Code of Pakistan – Seismic Provisions 2007 (BCP-SP 2007)** | National seismic code; PEC / Ministry of Housing & Works; based on **UBC-97**; developed post-2005 Kashmir earthquake with NESPAK, ICC and ACI input | Seismic zoning, base shear (Equivalent Lateral Force), R factors, ductile detailing requirement level (OMRF/IMRF/SMRF) |
| **Building Code of Pakistan 2021 (PKBC 2021)** | Successor to BCP 2007 (codes.iccsafe.org/content/PKBC2021P1) | Adopted in intent; BCP-SP 2007 still widely referenced and enforced for existing residential stock and by many local authorities **[VERIFY adoption status with the specific authority]** |
| **ASTM A615 / PS 1879** | Steel bar specification | Grade 40 / Grade 60 deformed bar properties, Pakistani mill certification |
| **IS 456:2000** | Indian code — **cross-reference only** | Useful when a contractor or draughtsman quotes South Asian lap-length rules of thumb ("50D"); do NOT mix IS and ACI clauses inside one design |
| **Local byelaws** (LDA/CDA/SBCA/RDA/DHA) | Mandatory | Covered area, setbacks, storey height, basement rules, plan vetting |

**Rule: pick one design code and stay in it.** ACI 318-19 for member design + BCP-SP 2007 for
seismic demand and detailing level is the standard Pakistani combination. Do not compute
development length by IS 456 and cover by ACI in the same drawing.

### 1.2 BCP-SP 2007 seismic zones — typical city assignments **[VERIFY against BCP-SP 2007 zoning map before use]**

| Zone | Z (UBC-97 zone factor) | Representative Pakistani locations |
|---|---|---|
| 1 | 0.075 | Parts of southern Punjab / interior Sindh |
| 2A | 0.15 | Lahore, Faisalabad, Multan, Sialkot |
| 2B | 0.20 | Islamabad, Rawalpindi, Karachi, Peshawar |
| 3 | 0.30 | Northern Punjab foothills, parts of KP |
| 4 | 0.40 | Quetta, Muzaffarabad, Chitral, Northern Areas |

### 1.3 Detailing level required (BCP-SP 2007, following UBC-97 Ch.16/19)

```
Seismic Zone 1        → Ordinary Moment Resisting Frame (OMRF) detailing acceptable
Seismic Zone 2A / 2B  → Intermediate Moment Resisting Frame (IMRF) minimum for RC frames
Seismic Zone 3 / 4    → Special Moment Resisting Frame (SMRF): full ACI 318-19 Ch.18 detailing
                        (135° seismic hooks, confined hoop zones, strong-column/weak-beam,
                         joint confinement) — non-negotiable
```

**Practical consequence:** a house in Quetta or Muzaffarabad requires ACI 318-19 Ch.18 ductile
detailing throughout. A house in Lahore requires at minimum IMRF detailing (ACI 318-19 §18.4).
The commonly-built Pakistani house — 90° tie hooks, ties omitted through the joint — meets
**neither**, which is exactly why Section 16 exists.

---

## Section 2: Concrete Grades and Mix Design

### 2.1 Grade nomenclature

- **M-grade (South Asian / BS lineage):** `M20` = characteristic *cube* compressive strength
  20 MPa at 28 days.
- **ACI f'c:** specified *cylinder* compressive strength.
- **Conversion [practice]:** f'c (cylinder) ≈ 0.80 × fck (cube). So M20 cube ≈ 16 MPa cylinder,
  M25 cube ≈ 20 MPa cylinder. Pakistani practice frequently treats M20 ≈ f'c 20 MPa ≈ 3000 psi
  directly. **Be explicit about which you mean** — this 20% difference silently changes every
  development length and shear capacity in the design.
- ACI 318-19 §19.2.1.1: **minimum f'c for structural concrete = 17 MPa (2500 psi)**.
  M15 therefore cannot be used for structural members — only lean concrete / PCC / blinding.

### 2.2 Grade selection table (residential)

| Grade | Nominal mix (cem:sand:agg, by volume) | fck cube | f'c approx | Approx cement (50 kg bags/m³) | Where used in a house |
|---|---|---|---|---|---|
| M7.5 / M10 | 1:4:8 / 1:3:6 | 7.5 / 10 MPa | — | 3.5 / 4.5 | PCC blinding under footings, mud-mat, floor sub-base, plinth filling |
| **M15** | **1:2:4** | 15 MPa | ~12 MPa | ~6.5 | Lean footing bed, non-structural slabs on grade, boundary-wall foundations. **Not permitted for structural RCC (ACI §19.2.1.1)** |
| **M20** | **1:1.5:3** | 20 MPa | ~16–20 MPa | ~8.0 | **Default for residential RCC** — slabs, beams, columns, footings in 1–2 storey houses |
| **M25** | 1:1:2 (nominal) — **use a designed mix instead** | 25 MPa | ~20–25 MPa | ~9.5–11 (nominal) / 7.5–8.5 (designed) | 3-storey+, long spans (>5.5 m), heavily loaded ground-floor columns, water tanks, basements, Zone 3/4 seismic frames |
| M30+ | designed mix only | 30 MPa | ~24 MPa | designed | Rarely needed in houses; transfer beams, deep basements, precast |

**Nominal 1:1:2 for M25 is wasteful** (≈550 kg cement/m³, high shrinkage and heat). Above M20,
switch to a **designed mix** from a testing lab or an RMC supplier.

### 2.3 Mix constants **[practice — verify against lab mix design]**

| Parameter | M15 | M20 | M25 |
|---|---|---|---|
| Water/cement ratio (max) | 0.60 | 0.55 | 0.50 |
| Water per m³ (20 mm agg, 75–100 mm slump) | ~190 L | ~186 L | ~186 L |
| Cement (kg/m³) | 300–325 | 350–400 | 380–420 (designed) |
| Fine aggregate (sand) | ~650 kg | ~700 kg | ~720 kg |
| Coarse aggregate 20 mm | ~1250 kg | ~1200 kg | ~1180 kg |
| Dry volume factor (wet→dry) | ×1.54 | ×1.54 | ×1.54 |
| Target mean strength for mix design | fck + 1.65σ; σ ≈ 3.5 MPa (M15/M20), 4.0 MPa (M25) | | |

### 2.4 Materials — practical requirements

- **Cement:** OPC 43 or 53 grade (or equivalent Pakistani brand designation). Do not mix
  brands within one pour. Store off the floor, use within 90 days.
- **Coarse aggregate:** crushed stone (Margalla, Sargodha, Ariser), 20 mm nominal max for
  slabs/beams. Nominal max aggregate size limited by ACI 318-19 §26.4.2.1(a)(4) to the
  least of: 1/5 of narrowest form dimension, 1/3 of slab depth, 3/4 of minimum clear
  spacing between bars. **In a 230 mm wide beam with 16 mm bars, 20 mm aggregate is
  already near the limit — do not use 40 mm aggregate in house beams.**
- **Sand:** Chenab/Lawrencepur sand, fineness modulus 2.4–3.0, washed. Silt content ≤ 3%
  by weight (field test: settle in a jar; silt layer > 6% of sand column → wash it).
- **Water:** potable. No brackish/tube-well water with high sulphates for RCC.
- **Curing:** minimum 7 days continuous wet curing for OPC; 14 days preferred for slabs.
  Ponding for slabs, hessian for columns/beams. **Curing failure is the single most common
  cause of a house's concrete never reaching its design strength.**

### 2.5 Steel grades

| Designation | fy | fy (ksi) | Typical use | Notes |
|---|---|---|---|---|
| Grade 40 (ASTM A615 Gr.40 / PS 1879) | 280 MPa | 40 | Older construction, stirrups/ties, small-scale work | Higher steel area required; more ductile; still common in rural Pakistani work |
| **Grade 60 (ASTM A615 Gr.60)** | **420 MPa** | 60 | **Default for all residential RCC main steel today** | All tables below default to fy = 420 MPa |
| Grade 75 / 80 | 520 / 550 MPa | 75 / 80 | Rare in houses | ACI §9.6.1.2 caps fy at 550 MPa (80 ksi) for the As,min calculation |

**Seismic caution (ACI 318-19 §20.2.2.5):** in special seismic systems, longitudinal reinforcement
must satisfy ASTM A706 (weldable, controlled actual-to-specified yield ratio) or A615 meeting
the additional limits (actual fy ≤ specified fy + 125 MPa; actual tensile/actual yield ≥ 1.25).
Un-certified market bar in a Zone 3/4 frame is a real problem — insist on mill test certificates.

### 2.6 Bar sizes — metric / imperial / Pakistani market

| Pakistani market call | Nominal dia | ACI bar no. | Metric bar no. | Area (mm²) | Unit weight (kg/m) = d²/162 |
|---|---|---|---|---|---|
| 1/4" | 6 mm | — | No.6 | 28.3 | 0.222 |
| 3/8" | 10 mm | #3 (9.5 mm) | No.10 | 78.5 | 0.617 |
| 1/2" | 12 mm | #4 (12.7 mm) | No.13 | 113 | 0.889 |
| 5/8" | 16 mm | #5 (15.9 mm) | No.16 | 201 | 1.578 |
| 3/4" | 20 mm | #6 (19.1 mm) | No.19 | 314 | 2.466 |
| 7/8" | 22 mm | #7 (22.2 mm) | No.22 | 380 | 2.984 |
| 1" | 25 mm | #8 (25.4 mm) | No.25 | 491 | 3.858 |
| 1-1/8" | 28 mm | #9 (28.7 mm) | No.29 | 616 | 4.840 |
| 1-1/4" | 32 mm | #10 (32.3 mm) | No.32 | 804 | 6.313 |

**Watch the 19 mm / 20 mm boundary.** ACI's development-length equations (§25.4.2.5 Ψs
modification factor) switch coefficient at No.19 (19.1 mm). A Pakistani "3/4 inch" bar is
normally rolled at **20 mm**, i.e. *larger* than No.19. Use the "No.22 and larger" coefficient
for 20 mm bar — it is conservative and correct. **This 19/22 boundary applies only to the
development-length Ψs factor** (Sections 4.1–4.3) — do not reuse it for other clauses with
their own bar-size thresholds, such as the tie-bar-size rule in Section 6.2, which switches
at a different pair of bar numbers (No.32/No.36).

---

## Section 3: Concrete Cover

Cover is measured to the **outermost** steel — the stirrup or tie, not the main bar. It controls
bond, corrosion protection, and fire resistance simultaneously. Under-cover is the most common
detailing failure found on Pakistani sites and the hardest to fix after the pour.

### 3.1 ACI 318-19 specified minimum cover, cast-in-place non-prestressed **[VERIFY: Table 20.5.1.3.1 in ACI 318-19; numbered Table 20.6.1.3.1 in ACI 318-14 and still widely quoted under that number]**

| Exposure condition | Member / bar size | Cover (mm) | Cover (in) |
|---|---|---|---|
| Cast against and permanently in contact with ground | All | **75** | 3 |
| Exposed to weather or in contact with ground (formed) | No.19 (19 mm) through No.57 | **50** | 2 |
| Exposed to weather or in contact with ground (formed) | No.16 (16 mm) and smaller | **40** | 1.5 |
| Not exposed to weather or in contact with ground | Slabs, joists, walls — No.36 and smaller | **20** | 3/4 |
| Not exposed to weather or in contact with ground | Beams, columns, pedestals — primary bars, ties, stirrups, spirals | **40** | 1.5 |
| Not exposed to weather or in contact with ground | Shells, folded plates — No.19 and larger | 20 | 3/4 |
| Not exposed to weather or in contact with ground | Shells, folded plates — No.16 and smaller | 13 | 1/2 |

### 3.2 Practical cover schedule for a Pakistani house **[practice, ≥ ACI minimum]**

| Element | Design cover | Reason for the margin over ACI minimum |
|---|---|---|
| Footing bottom (on 75 mm PCC) | 50 mm from PCC / **75 mm if cast directly on soil** | Always cast on PCC. Never let a bar touch soil. |
| Footing sides / top | 50 mm | Earth contact |
| Grade beam / plinth beam | 50 mm | Soil moisture, salt-laden subsoil common in Sindh/south Punjab |
| Column (interior, plastered) | 40 mm | ACI minimum |
| Column (exterior face, exposed) | 40–50 mm | Rain, exposed façades |
| Beam (interior) | 40 mm | ACI minimum |
| Slab (interior, roof underside) | 20 mm | ACI minimum; **do not reduce to "just enough"** |
| Roof slab top face (exposed to weather until waterproofing) | 25–40 mm | Ponding, membrane failure |
| Staircase waist slab | 20–25 mm | |
| Water tank / bathroom sunk slab | 40 mm | Permanent moisture |
| Boundary wall / retaining wall earth face | 50–75 mm | |

### 3.3 Cover enforcement on site

- **Use manufactured cover blocks or PVC/plastic spacers of the correct thickness.** Never
  stone chips, never broken brick, never rebar offcuts as chairs on the soffit. Mortar cover
  blocks are acceptable only if made from the same grade concrete/mortar and cured.
- Block spacing **[practice]:** 600–800 mm c/c in both directions on slab bottoms, 900 mm
  along beam sides, 3 per metre height on column faces.
- **Chairs for slab top steel:** minimum 12 mm dia chairs at 1000 mm c/c both ways. Slab top
  steel walked flat by labourers is a systemic cause of cracking over supports.
- Reject any bar with cover deficit before the pour. After the pour it is a repair, not a fix.

---

## Section 4: Development Length and Lap Splices

This is where most real detailing errors live. A bar is only as good as its anchorage.

### 4.1 Tension development length — full equation (ACI 318-19 §25.4.2.3)

```
        fy · Ψt · Ψe · Ψs · Ψg
ld = ( ────────────────────────── ) · db          [SI, MPa, mm]
        1.1 · λ · √f'c · ((cb + Ktr)/db)

  where ((cb + Ktr)/db) ≤ 2.5
        Ψt · Ψe ≤ 1.7
        ld ≥ max(300 mm, 12·db)          (ACI §25.4.2.1)
```

**Modification factors (ACI 318-19 Table 25.4.2.5):**

| Factor | Condition | Value |
|---|---|---|
| Ψt — casting position ("top-bar effect") | More than 300 mm of fresh concrete cast below the bar | **1.3** |
| Ψt | All other | 1.0 |
| Ψe — epoxy coating | Epoxy-coated, cover < 3db or clear spacing < 6db | 1.5 |
| Ψe | Epoxy-coated, other | 1.2 |
| Ψe | Uncoated / zinc-coated (normal Pakistani bar) | **1.0** |
| Ψs — bar size | No.19 (19 mm) and smaller | **0.8** |
| Ψs | No.22 (22 mm) and larger | 1.0 |
| Ψg — grade | fy = 280 or 420 MPa | **1.0** |
| Ψg | fy = 550 MPa | 1.15 |
| Ψg | fy = 690 MPa | 1.3 |
| λ — lightweight | Normalweight concrete | **1.0** |

*(This Ψs No.19/No.22 boundary is specific to the development-length calculation. Do not
apply it to the tie-bar-size rule in Section 6.2, which uses a different boundary — see the
note at the end of Section 2.6.)*

- **cb** = smaller of (distance from bar centre to nearest concrete surface) and (half the
  centre-to-centre spacing of bars being developed).
- **Ktr** = 40·Atr / (s·n) — transverse reinforcement index. **Taking Ktr = 0 is always
  permitted and conservative** (ACI §25.4.2.4). Do this for hand design.

### 4.2 Simplified equations (ACI 318-19 Table 25.4.2.3) — use these for house-scale work

Applicable when clear spacing ≥ db, clear cover ≥ db, **and** at least minimum stirrups/ties
along ld — which is the normal case in a properly detailed beam or column:

```
No.19 (≤19 mm) and smaller:     ld = ( fy · Ψt · Ψe ) / ( 2.1 · λ · √f'c ) · db
No.22 (≥22 mm) and larger:      ld = ( fy · Ψt · Ψe ) / ( 1.7 · λ · √f'c ) · db
```

If those spacing/cover/stirrup conditions are **not** met, the coefficients become
1.4 and 1.1 respectively (i.e. ld is 50% longer). Congested, unstirruped, low-cover
regions need much more anchorage — the opposite of what site practice assumes.

### 4.3 Tension development length table — **f'c = 20 MPa (M20), fy = 420 MPa, normalweight, uncoated**

| Bar | ld coefficient | ld bottom bar (Ψt=1.0) | ld TOP bar (Ψt=1.3) |
|---|---|---|---|
| 10 mm | 44.7 db | **450 mm** | **590 mm** |
| 12 mm | 44.7 db | **540 mm** | **700 mm** |
| 16 mm | 44.7 db | **720 mm** | **930 mm** |
| 20 mm | 55.3 db (use ≥No.22 coeff) | **1110 mm** | **1440 mm** |
| 25 mm | 55.3 db | **1390 mm** | **1800 mm** |

### 4.4 Tension development length table — **f'c = 25 MPa (M25), fy = 420 MPa**

| Bar | ld coefficient | ld bottom bar | ld TOP bar (×1.3) |
|---|---|---|---|
| 10 mm | 40.0 db | 400 mm | 520 mm |
| 12 mm | 40.0 db | 480 mm | 630 mm |
| 16 mm | 40.0 db | 640 mm | 840 mm |
| 20 mm | 49.4 db | 990 mm | 1290 mm |
| 25 mm | 49.4 db | 1240 mm | 1610 mm |

*Grade 40 (fy = 280 MPa) with M20: multiply the M20 Grade 60 values by 280/420 = 0.667.*

### 4.5 Tension lap splices (ACI 318-19 §25.5.2, Table 25.5.2.1)

| Class | Length | When permitted |
|---|---|---|
| **Class A** | **1.0 × ld** (≥ 300 mm) | Only if **BOTH**: ≤ 50% of bars spliced within the required lap length, **AND** As,provided ≥ 2 × As,required over the splice length |
| **Class B** | **1.3 × ld** (≥ 300 mm) | **All other cases — this is the practical default** for beam and column splices in residential work |

- **ld in the splice calculation is computed WITHOUT the Ψs (0.8) bar-size reduction** for
  splice purposes in some interpretations — **[VERIFY §25.5.2.1 wording in the primary document]**.
  Conservative practice: compute ld from the Table 25.4.2.3 simplified equation as above and
  multiply by 1.3.
- **Lap splices are NOT permitted for bars larger than No.36 (36 mm) in tension** (ACI §25.5.1.1);
  #14 and #18 bars require mechanical or welded splices. Irrelevant for houses, relevant for
  transfer beams.
- **Contact lap splices are preferred** (bars wired together). Non-contact splices must be
  spaced no more than the lesser of 1/5 of the lap length and 150 mm apart (ACI §25.5.1.3).

### 4.6 Class B lap length quick table — **M20, Grade 60**

| Bar | Class B lap, bottom bar | Class B lap, TOP bar |
|---|---|---|
| 10 mm | **590 mm** | 770 mm |
| 12 mm | **700 mm** | 910 mm |
| 16 mm | **940 mm** | 1210 mm |
| 20 mm | **1440 mm** | 1870 mm |
| 25 mm | **1810 mm** | 2350 mm |

**Compare against the site rule of thumb "50D".** For a 16 mm bottom bar in M20, 50D = 800 mm
vs. the required 940 mm — **15% short**. For a 16 mm *top* bar, 50D is **34% short**. This
single habit is the mechanism behind a large share of bond-failure cracking. See Section 16.

### 4.7 Compression development and lap (columns)

```
Compression development (ACI §25.4.9.2):
    ldc = greater of [ 0.24·fy / (λ·√f'c) · db ]  and  [ 0.043 · fy · db ]     ≥ 200 mm

    M20, Gr.60:  ldc = 22.5·db      M25, Gr.60:  ldc = 20.2·db

Compression lap splice (ACI §25.5.5.1), fy ≤ 420 MPa:
    lsc = 0.071 · fy · db  =  30·db                                            ≥ 300 mm
    fy > 420 MPa:  lsc = (0.13·fy − 24)·db

Compression lap increase (ACI §25.5.5.1):
    If f'c < 21 MPa, multiply the lap length by 4/3.
```

**Trap:** M20 concrete has f'c = 20 MPa < 21 MPa. So a compression lap in an M20 column is
**40·db, not 30·db**. For a 16 mm column bar that is 640 mm, not 480 mm. Almost nobody on site
applies this increase.

### 4.8 Standard hooks (ACI 318-19 §25.3)

| Hook type | Bend | Extension beyond bend | Use |
|---|---|---|---|
| Standard 90° hook | 90° | **12 db** | Beam bars anchored into exterior columns, slab bars at edges |
| Standard 180° hook | 180° | **4 db, but ≥ 65 mm** | Ends of bars where 90° won't fit |
| Stirrup/tie 90° hook | 90° | 6 db (≥ 75 mm for No.19–No.25) | Non-seismic ties |
| Stirrup/tie 135° hook | 135° | 6 db | Non-seismic ties |
| **Seismic hook** (ACI §18 definition) | **≥135°** (90° permitted only for circular hoops) | **6 db, ≥ 75 mm**, engaging a longitudinal bar | **Mandatory** for all hoops/ties/crossties in IMRF and SMRF frames |

**Minimum inside bend diameter (ACI Table 25.3.1 / 25.3.2):**

| Bar | Main bars | Stirrups & ties |
|---|---|---|
| 10–25 mm (#3–#8) | 6 db | 4 db (for 16 mm & smaller) |
| 28–36 mm (#9–#11) | 8 db | 6 db (for 19–25 mm) |
| 43–57 mm (#14, #18) | 10 db | — |

### 4.9 Development length of a standard hook in tension, ldh (ACI 318-19 §25.4.3.1) **[VERIFY: this db^1.5-based formula, its "23" denominator coefficient, and the ψr/ψo/ψc modifier values against the primary ACI 318-19 text before quoting numerically — this provision was substantially revised from the older linear-in-db 318-11/318-14 formula and is more error-prone to transcribe than most clauses in this file. It is also load-bearing for the exterior-column-depth conclusions in Section 4.9/7.6, so treat the table below as an order-of-magnitude planning aid, not a citable value, until checked against a purchased copy.]**

```
        fy · Ψe · Ψr · Ψo · Ψc
ldh = ( ────────────────────── ) · db^1.5           ≥ max( 8·db , 150 mm )
             23 · λ · √f'c
```

Conservative table with all Ψ = 1.0, **M20, Grade 60**, plus required tail — **[VERIFY before
citing, see note above]**:

| Bar | ldh (straight embedment measured to outside of bend) | 90° tail (12 db) |
|---|---|---|
| 10 mm | 150 mm (minimum governs) | 120 mm |
| 12 mm | 170 mm | 145 mm |
| 16 mm | 265 mm | 195 mm |
| 20 mm | 365 mm | 240 mm |
| 25 mm | 510 mm | 300 mm |

**Design implication (order-of-magnitude, pending verification per the note above):** a 16 mm
beam bottom bar hooked into an exterior column needs roughly 265 mm of embedment *plus* a
195 mm tail — inside a 230 mm wide column that does not fit with cover. **Exterior columns
supporting hooked beam bars often need to be 300–375 mm deep in the direction of the beam.**
This is a member-sizing consequence of a detailing rule, and it is routinely missed at concept
stage — but confirm the exact ldh value against ACI 318-19 §25.4.3.1 before finalizing a
column dimension around it.

### 4.10 Where to place a splice — decision tree

```
Splicing a bar?
├─ COLUMN longitudinal bar
│   ├─ Non-seismic → splice just above floor level is acceptable; stagger ≥ 50% of bars
│   └─ IMRF / SMRF (ACI §18.7.4.3) → splice ONLY within the CENTRE HALF of the column
│       clear height; must be Class B (tension lap); hoops at ≤ d/4 or 100 mm along
│       the entire splice length
├─ BEAM bottom bar (positive moment steel)
│   → splice near the SUPPORTS (low positive moment), never at mid-span
├─ BEAM top bar (negative moment steel)
│   → splice near MID-SPAN (low negative moment), never over the column
├─ SLAB bottom bar   → splice over supports
├─ SLAB top bar      → splice at mid-span
└─ ANY bar in a plastic hinge zone (2h from column face in a beam,
    lo from joint face in a column)  → NO SPLICE PERMITTED (ACI §18.6.3.3 / §18.7.4.3)
```

**Stagger rule [practice, aligns with the Class A/B intent]:** never splice more than 50% of
the bars at one section; offset alternate splices by at least 1.3·ld.

---

## Section 5: Footings

### 5.1 Footing type decision tree (residential)

```
Column load P and safe bearing capacity qa known?
├─ P/qa < ~2.5 m² and columns > 2.5 m apart
│      → ISOLATED PAD FOOTING (most common in Pakistani houses)
├─ Footings would overlap, or column near a boundary
│      → COMBINED / STRAP FOOTING
├─ Total footing area > ~50% of plot footprint, or soft/variable soil
│      → RAFT / MAT FOUNDATION
├─ Load-bearing brick masonry walls (no frame)
│      → STRIP FOOTING (RCC or stepped brick on PCC)
└─ qa < 75 kPa, filled ground, high water table, or expansive clay
       → PILES / under-reamed piles — mandatory geotechnical investigation
```

**Typical safe bearing capacities [practice — always confirm with a soil test]:**
firm clay 100–150 kPa; stiff clay 150–250 kPa; medium dense sand 150–200 kPa;
filled/made ground 50–75 kPa (or unusable); Lahore/Islamabad typical residential
design value 130–180 kPa. **Never design a footing from a table value on a real project.**

### 5.2 Footing sizing sequence

```
1. Service load  P (DL + LL, unfactored) + self weight of footing & backfill (~10%)
2. Required plan area  A = 1.10·P / qa
3. Choose square/rectangular plan; round up to 75 mm increments
4. Factored soil pressure  qu = Pu / A     (Pu = 1.2DL + 1.6LL, ACI §5.3.1)
5. Set depth for ONE-WAY shear     (Section 5.3)
6. Check depth for TWO-WAY (punching) shear   (Section 5.4)
7. Design flexural steel at column face; check As,min
8. Check bearing / dowel development into column
```

### 5.3 One-way (beam) shear — ACI 318-19 §22.5, Table 22.5.5.1

```
φVc = φ · 0.17 · λ · √f'c · b · d          (SI, MPa, N)     φ = 0.75
Critical section: at distance d from the column face.
```
Size the footing thickness so that **concrete alone carries the shear**. Shear reinforcement
in a residential pad footing is a sign the footing is too thin — deepen it instead.

### 5.4 Two-way (punching) shear — ACI 318-19 §22.6, Table 22.6.5.2

```
Critical perimeter bo at d/2 from the column face.
vc = least of:
     0.33 · λ · √f'c
     0.17 · (1 + 2/β) · λ · √f'c            β = long/short column dimension ratio
     0.083 · (2 + αs·d/bo) · λ · √f'c       αs = 40 interior, 30 edge, 20 corner
φvc ≥ vu = Vu / (bo·d)          φ = 0.75
```

### 5.5 Footing reinforcement rules

| Rule | Value | Source |
|---|---|---|
| Minimum reinforcement ratio | **As,min = 0.0018 · Ag** (Grade 60); 0.0020 for Grade 40/50 | ACI 318-19 §13.3.2.1 extending §8.6.1.2 / §7.6.1 slab provisions |
| Minimum thickness above bottom steel | **≥ 150 mm** (footings on soil) | ACI 318-19 §13.3.1.2 |
| Practical minimum total thickness | 250–300 mm (residential pad) **[practice]** | 150 + 75 cover + bar dia + tolerance |
| Bar distribution, square footing | Uniform each way | ACI §13.3.3.3 |
| Bar distribution, rectangular footing | In the **short** direction, the fraction 2/(β+1) of total steel is placed within a band of width = short side, centred on the column; remainder distributed uniformly | ACI §13.3.3.3 |
| Two-way footing effective width for column-strip steel | Concentrate over a width of **1.5h either side of the column** where the footing is deep relative to its plan | ACI Ch.13 / §8.4 intent **[VERIFY exact clause]** |
| Maximum bar spacing | lesser of 3h and 450 mm **[practice, mirrors §7.7.2.3]** | |
| Minimum bar size **[practice]** | 12 mm; 10 mm only for very light strip footings | |
| PCC blinding under footing | 75 mm of M10/M15, projecting 75–100 mm beyond footing edge | **[practice]** |

### 5.6 Column dowels into footing

- Dowel bars must match or exceed the column longitudinal bars in **number and area**.
- Dowels are hooked at the bottom (90° hook sitting on the footing bottom mat) — the hook
  provides positioning, **not** development; the vertical embedment must provide the
  **compression development length ldc** (Section 4.7) inside the footing.
- For M20 and a 16 mm dowel: ldc = 22.5 × 16 = 360 mm. **A 300 mm thick footing cannot
  develop this** — either deepen the footing or use a pedestal.
- Dowel projection above footing top = compression lap length (40 db in M20) + 75 mm,
  and the splice location must respect the column splice rules in Section 4.10.
- **Tie the dowel cage.** At least 2 ties within the dowel projection above the footing.

### 5.7 Worked example — isolated pad footing

```
Given:  Interior column 230 × 380 mm, service load P = 420 kN
        qa = 150 kPa, f'c = 20 MPa (M20), fy = 420 MPa, cover 75 mm

1. Area required     A = 1.10 × 420 / 150 = 3.08 m²  → 1.80 × 1.80 m  (3.24 m²)  OK
2. Factored load     Pu ≈ 1.35 × 420 = 567 kN  (assume 60/40 DL/LL split)
   qu = 567 / 3.24  = 175 kPa
3. Try h = 450 mm.  d = 450 − 75 − 12/2 ≈ 370 mm
4. One-way shear (long direction):
   Critical section at d from column face:
     cantilever length = (1800 − 380)/2 = 710 mm ;  710 − 370 = 340 mm remains
     Vu = 175 × 0.340 × 1.80 = 107 kN
     φVc = 0.75 × 0.17 × 1.0 × √20 × 1800 × 370 = 0.75 × 0.760 × 1800 × 370
         = 380 kN                             107 ≪ 380  ✔ ample
5. Punching shear:
   bo = 2(230 + 370) + 2(380 + 370) = 1200 + 1500 = 2700 mm
   Vu = 567 − 175 × (0.600 × 0.750) = 567 − 79 = 488 kN
   β = 380/230 = 1.65 ; αs = 40
     0.33√20                       = 1.476 MPa
     0.17(1 + 2/1.65)√20           = 1.681 MPa
     0.083(2 + 40×370/2700)√20     = 2.777 MPa      → vc = 1.476 MPa
   φVc = 0.75 × 1.476 × 2700 × 370 = 1106 kN        488 < 1106  ✔
   (h could be reduced; 450 mm retained to develop the column dowels — see step 8)
6. Flexure at column face (long direction):
   cantilever = 0.710 m ;  Mu = 175 × 0.710² / 2 × 1.80 = 79.4 kN·m
   Approx  As = Mu / (0.9 · fy · 0.9d) = 79.4e6 / (0.9 × 420 × 333) = 631 mm²
7. Minimum steel:  As,min = 0.0018 × 1800 × 450 = 1458 mm²   → GOVERNS
   Using 12 mm bars (113 mm²):  n = 1458/113 = 12.9 → 13 bars
   Spacing = (1800 − 2×75)/12 = 137 mm  →  use 12 mm @ 130 mm c/c BOTH WAYS
   Check max spacing: 3h = 1350, 450 mm cap → 130 mm  ✔
8. Dowels: 6 × 16 mm to match column.  ldc = 22.5 × 16 = 360 mm
   Available = 450 − 75 − 12 − 12 = 351 mm → marginal.
   → Deepen footing to 500 mm, OR provide 90° hooks and verify per ACI §25.4.9.
   (Chosen: h = 500 mm, recompute As,min = 0.0018 × 1800 × 500 = 1620 mm²
    → 15 no. 12 mm @ 115 mm c/c both ways, or 10 no. 16 mm @ 180 mm c/c both ways)

FINAL: 1800 × 1800 × 500 mm pad, M20, 16 mm @ 180 c/c both ways bottom mat,
       75 mm PCC (M15) blinding, 75 mm cover, 6-16 mm dowels with 90° hooks on the mat.
       ** Preliminary sizing only — requires PEC-registered engineer's design & stamp. **
```

---

## Section 6: Columns

### 6.1 Reinforcement limits (ACI 318-19 §10.6.1.1)

| Limit | Value |
|---|---|
| Minimum longitudinal steel | **ρ = 0.01 (1% of Ag)** |
| Maximum longitudinal steel | **ρ = 0.08 (8% of Ag)** |
| Practical maximum **[practice]** | **ρ ≤ 0.04 (4%)** — above this, splice regions double the local ratio to 8% and concrete cannot be placed |
| Minimum number of bars (ACI §10.7.3.1) | 4 (rectangular ties), 3 (triangular ties), 6 (spirals) |
| Minimum bar size **[practice]** | 12 mm; 16 mm typical for residential frame columns |
| Minimum clear spacing between bars (ACI §25.2.3) | greater of 40 mm, 1.5 db, and (4/3) × nominal max aggregate |
| Minimum column dimension **[practice; BCP/IMRF-driven]** | 230 mm (9") absolute; **300 mm (12") strongly preferred** for any frame column; ACI §18.7.2.1 requires ≥ 300 mm for SMRF columns |

### 6.2 Tie (lateral reinforcement) rules — non-seismic, ACI 318-19 §25.7.2 and §10.7.6.1.2

```
TIE BAR SIZE (§25.7.2.2):
    ≥ No.10 (10 mm) for longitudinal bars No.32 (32 mm) and smaller
    ≥ No.13 (13 mm) for longitudinal bars No.36 (36 mm) and larger, and for bundled bars

TIE SPACING (§10.7.6.1.2) = LEAST of:
    16 × db (longitudinal bar diameter)
    48 × dt (tie bar diameter)
    least column cross-sectional dimension

TIE ARRANGEMENT (§25.7.2.3):
    Every corner and alternate longitudinal bar must have lateral support from the
    corner of a tie with an included angle ≤ 135°.
    No bar may be more than 150 mm clear, along the tie, from a laterally supported bar.
    → A 230 × 380 column with 6 bars needs a closed rectangular tie PLUS a crosstie
      or a diamond/internal tie, not a single perimeter loop.
```

**Note on the No.32/No.36 boundary:** this tie-bar-size threshold is a genuinely different
clause from the Ψs development-length bar-size cutoff (No.19/No.22, Sections 2.6 and 4.1) —
do not conflate the two. Practical column bar sizes in residential work (12–25 mm, i.e. up
through roughly No.25) all fall well under the No.32-and-smaller threshold, so **10 mm ties
are code-compliant for virtually all residential columns**; 13 mm ties are only required once
longitudinal bars reach No.36 (36 mm) or are bundled — essentially never seen in house-scale
work. The worked example below is unaffected by this correction (16 mm longitudinal bars use
10 mm ties either way) but the general rule stated for larger bar sizes has been fixed.

**Tie spacing worked value:** 230 × 380 column, 6–16 mm longitudinal, 10 mm ties:
16 × 16 = 256 mm; 48 × 10 = 480 mm; least dimension = 230 mm → **230 mm governs → use 200 mm c/c**.

### 6.3 Seismic confinement — SMRF columns (ACI 318-19 §18.7.5)

```
CONFINED LENGTH lo at each end, measured from the joint face = greatest of:
    column depth (larger cross-sectional dimension)
    clear span / 6
    450 mm

HOOP SPACING WITHIN lo (§18.7.5.3) = least of:
    b/4  (one quarter of the minimum column dimension)
    6 × db (smallest longitudinal bar)
    so  = 100 + (350 − hx)/3        with 100 mm ≤ so ≤ 150 mm
         (hx = maximum horizontal spacing of crosstie/hoop legs on the column face)

SPACING OUTSIDE lo (§18.7.5.5) = lesser of:
    6 × db (smallest longitudinal bar)
    150 mm

ALL hoops must have SEISMIC HOOKS (≥135° bend, 6db ≥ 75 mm extension, engaging a
longitudinal bar). 90° hooks are NOT permitted anywhere in a seismic frame.
```

**Practical Pakistani seismic column detail (Zone 2B–4) [practice, per §18.7.5]:**
10 mm hoops @ **100 mm c/c** over lo at top and bottom of every column + through the joint,
@ 150 mm c/c in the middle region, all with 135° seismic hooks, plus crossties so that no
longitudinal bar is unsupported.

### 6.4 Strong column – weak beam (ACI 318-19 §18.7.3.2)

```
Σ Mnc  ≥  (6/5) · Σ Mnb
```
Sum of nominal flexural strengths of columns framing into a joint must be at least
1.2× the sum of the beams'. This is what forces hinging into beams instead of columns.
**In practice this is the reason a 230 × 230 column under a 230 × 450 beam is unacceptable
in a seismic zone** — the beam is stronger than the column and the frame will hinge in
the columns and collapse as a soft storey.

### 6.5 Residential column sizing starting points **[practice — preliminary only]**

| Configuration | Typical column | Longitudinal steel | Ties |
|---|---|---|---|
| Single storey, tributary ≤ 12 m², Zone 1–2A | 230 × 230 (9"×9") | 4–12 mm (1.02%) | 8 mm @ 175 c/c |
| Single storey, Zone 2B+ | 230 × 300 | 4–16 mm (1.17%) | 10 mm @ 175 c/c, 100 c/c at ends |
| Two storey, ground floor | 230 × 380 (9"×15") | 6–16 mm (1.38%) | 10 mm @ 200 c/c, 100 c/c at ends |
| Two storey, first floor | 230 × 300 | 4–16 mm | 10 mm @ 200 c/c |
| Three storey, ground floor | 300 × 450 or 380 × 380 | 8–16 mm or 6–20 mm | 10 mm @ 200 c/c, 100 c/c at ends |
| Zone 3/4, any storey (SMRF) | **≥ 300 × 300**, b/h ≥ 0.4 (§18.7.2.1) | ≥ 1.0%, ≤ 4% | 10 mm hoops + crossties @ 100 c/c over lo |

Slenderness: for a braced residential column, check klu/r; ACI §6.2.5 permits neglecting
slenderness if **klu/r ≤ 34 − 12(M1/M2) ≤ 40**. For a 230 mm column, r ≈ 0.3 × 230 = 69 mm;
a 3.0 m clear height gives klu/r = 3000/69 = 43 — **already slender**. Tall clear-height
lounge/drawing-room columns in Pakistani houses are frequently slender and under-designed.

---

## Section 7: Beams

### 7.1 Minimum depth for deflection control (ACI 318-19 Table 9.3.1.1, fy = 420 MPa, non-prestressed, normalweight)

| Support condition | Minimum h |
|---|---|
| Simply supported | ℓ/16 |
| One end continuous | ℓ/18.5 |
| Both ends continuous | ℓ/21 |
| Cantilever | ℓ/8 |

*(For fy ≠ 420 MPa multiply by (0.4 + fy/700).)*

**Residential quick sizing [practice]:** beam depth ≈ span/12 to span/15 including slab;
width ≈ wall thickness (230 mm) so the beam hides in the wall. A 4.5 m clear span both ends
continuous: h ≥ 4500/21 = 214 mm by code, but **230 × 450 is the practical standard** because
shear, bar anchorage, and stiffness all govern before deflection does.

### 7.2 Flexural steel limits

```
MINIMUM (ACI 318-19 §9.6.1.2):
    As,min = greater of  [ 0.25·√f'c / fy ] · bw · d    and   [ 1.4 / fy ] · bw · d
    (fy capped at 550 MPa for this calculation)

    For f'c ≤ 31 MPa the 1.4/fy term always governs:
        Grade 60 (fy 420):   ρmin = 1.4/420 = 0.00333
        Grade 40 (fy 280):   ρmin = 1.4/280 = 0.00500

MAXIMUM (ACI 318-19 §9.3.3.1 — net tensile strain εt ≥ 0.004):
    ρmax = 0.85·β1·(f'c/fy)·(0.003 / (0.003 + εt))
    M20 / Gr.60 :  ρ(εt=0.004) = 0.0147 ;  ρ(tension-controlled, εt=0.005) = 0.0129
    M25 / Gr.60 :  ρ(εt=0.004) = 0.0184 ;  ρ(tension-controlled)           = 0.0161
    Balanced:      M20 ρb = 0.0202 ;  M25 ρb = 0.0253

DESIGN TARGET [practice]:  keep ρ between 0.004 and 0.0125 for M20/Grade 60.
    Below → over-reinforced concrete section wasted;  above → brittle, congested, φ drops.
```

**Minimum steel table, 230 mm wide beam, M20, Grade 60:**

| Beam h | d (cover 40, 8 mm stirrup, 16 mm bar) | As,min = 0.00333·bw·d | Bars |
|---|---|---|---|
| 300 mm | 244 mm | 187 mm² | 2–12 mm (226) |
| 380 mm | 324 mm | 248 mm² | 2–16 mm (402) |
| 450 mm | 394 mm | 302 mm² | 2–16 mm (402) |
| 530 mm | 474 mm | 363 mm² | 2–16 mm (402) or 3–16 mm |
| 600 mm | 544 mm | 417 mm² | 3–16 mm (603) |

**Also required:** at least 2 continuous bars top and bottom over the full beam length
(ACI §9.7.7 structural integrity; §18.6.3.1 for seismic frames requires ≥2 bars continuous
top and bottom, and positive moment strength at the joint face ≥ 50% of negative moment
strength there).

### 7.3 Bar spacing and packing in a 230 mm beam

```
Minimum clear spacing (ACI §25.2.1) = greatest of 25 mm, db, and (4/3)·max aggregate size
    With 20 mm aggregate:  (4/3) × 20 = 26.7 mm  → governs for bars ≤ 25 mm

How many bars fit in a 230 mm wide beam?
    Usable width = 230 − 2(40 cover) − 2(8 stirrup) = 134 mm
    16 mm bars:  n·16 + (n−1)·26.7 ≤ 134  →  n = 3   (3-16 mm just fits)
    20 mm bars:  n·20 + (n−1)·26.7 ≤ 134  →  n = 3   (tight)
    12 mm bars:  n = 4
→ MORE THAN 3 BARS IN ONE LAYER IN A 9" BEAM IS NOT BUILDABLE.
  Use a second layer (25 mm clear vertical gap, ACI §25.2.2) or widen the beam.
```

### 7.4 Shear design and stirrups

```
Concrete shear strength (ACI 318-19 Table 22.5.5.1, members with Av ≥ Av,min):
    Vc = 0.17 · λ · √f'c · bw · d          φ = 0.75
    M20:  Vc = 0.760 · bw · d  (N, mm)

Minimum shear reinforcement (ACI §9.6.3.4, Table 9.6.3.4):
    Av,min / s = greater of  [ 0.062·√f'c · bw / fyt ]  and  [ 0.35 · bw / fyt ]
    For f'c ≤ 32 MPa the 0.35 term governs.
    230 mm beam, fyt = 420: Av,min/s = 0.35 × 230 / 420 = 0.192 mm²/mm
      → 2-leg 8 mm stirrup (Av = 100 mm²) → s ≤ 521 mm  (spacing limit governs instead)

Maximum stirrup spacing (ACI §9.7.6.2.2):
    Vs ≤ 0.33·√f'c·bw·d  →  s ≤ lesser of  d/2  and  600 mm
    Vs >  0.33·√f'c·bw·d  →  s ≤ lesser of  d/4  and  300 mm
    Vs may not exceed 0.66·√f'c·bw·d — if it does, the beam section is too small
```

**Seismic beam hoops (ACI 318-19 §18.6.4) — required in IMRF/SMRF:**

```
Hoops over a length 2h from the face of the support at each end (the plastic hinge zone):
    First hoop within 50 mm of the column face
    Spacing ≤ least of:   d/4 ,   6 × db(smallest longitudinal bar) ,   150 mm
Outside the 2h hinge zone:
    Stirrups with SEISMIC HOOKS at ≤ d/2 throughout the beam length (§18.6.4.4)
```

**Practical residential beam stirrup schedule [practice, meets §18.6.4 for a
230 × 450 beam with 16 mm bars, d ≈ 394]:**
8 mm 2-leg stirrups @ **100 mm c/c** over 900 mm (2h) at each end,
@ **175 mm c/c** (< d/2 = 197) in the middle region, **all with 135° seismic hooks**.

### 7.5 Bar curtailment and extension rules (ACI 318-19 §9.7.3)

| Rule | Requirement |
|---|---|
| Extension past the theoretical cut-off point | greater of **d** and **12 db** |
| Continuing bars at a cut-off | must extend ld beyond the cut-off point |
| Bottom bars at simple supports | at least 1/3 of positive steel continues into the support ≥ 150 mm (§9.7.3.8.1) |
| Bottom bars at continuous supports | at least 1/4 of positive steel continues, ≥ 150 mm into the support |
| Top bars at supports | at least 1/3 of negative steel extends past the inflection point by the greatest of d, 12 db, and ℓn/16 (§9.7.3.8.4) |
| Rule of thumb curtailment **[practice]** | top steel over supports extends **0.25 to 0.30 × clear span** each side; bottom steel bent up or curtailed no closer than 0.15 ℓ from the support |
| Structural integrity (§9.7.7) | Continuous beams: ≥ 1/4 of maximum positive steel continuous, and ≥ 1/6 of negative steel at supports continuous, enclosed by closed stirrups over the full length |

### 7.6 Worked example — interior beam

```
Given: 230 × 450 mm beam, clear span 4.5 m both ends continuous, M20, Gr.60,
       superimposed load w = 28 kN/m factored (slab + walls + LL)

1. Depth check:  h,min = 4500/21 = 214 mm  <  450  ✔
2. d = 450 − 40 cover − 8 stirrup − 16/2 = 394 mm
3. Moments (ACI §6.5.2 approximate coefficients, interior span both ends continuous):
     M(-) at face of support = wu·ℓn²/11 = 28 × 4.5² / 11 = 51.5 kN·m
     M(+) at mid-span        = wu·ℓn²/16 = 28 × 4.5² / 16 = 35.4 kN·m
4. Negative steel:  As ≈ Mu/(0.9·fy·0.9d) = 51.5e6/(0.9×420×355) = 384 mm²
     → 2–16 mm (402 mm²) continuous top + extras if analysis demands
5. Positive steel:  As ≈ 35.4e6/(0.9×420×355) = 264 mm²
     As,min = 0.00333 × 230 × 394 = 302 mm² → GOVERNS
     → 2–16 mm (402 mm²) bottom, continuous
6. ρ check: 402/(230×394) = 0.0044   ✔ (between 0.004 and 0.0125)
7. Shear:  Vu at d from face = 28 × (4.5/2 − 0.394) = 52.0 kN
     φVc = 0.75 × 0.760 × 230 × 394 = 51.7 kN → Vu ≈ φVc, stirrups required for the balance
     Provide minimum + seismic hoop spacing:
       8 mm 2-leg @ 100 c/c for 900 mm each end (2h), @ 175 c/c elsewhere, 135° hooks
8. Anchorage into exterior column (if applicable):
     16 mm bottom bar, ldh ≈ 265 mm + 195 mm tail (Section 4.9 — VERIFY before finalizing)
     → column must be ≥ 375 mm deep in that direction, or use a headed-bar detail.

** Preliminary sizing only — requires PEC-registered engineer's design & stamp. **
```

---

## Section 8: Slabs

### 8.1 One-way vs two-way

```
Ly / Lx  ≤ 2   →  TWO-WAY slab (load spans both directions)
Ly / Lx  > 2   →  ONE-WAY slab (spans the short direction; long direction gets
                  distribution/shrinkage steel only)
Slab supported on beams on all four sides and Ly/Lx ≤ 2 → two-way beam-supported slab
Slab on columns without beams → flat slab / flat plate (rare in houses; punching shear governs)
```

### 8.2 Minimum thickness

**One-way slabs — ACI 318-19 Table 7.3.1.1** (fy = 420 MPa, not supporting partitions likely damaged by deflection):

| Support condition | Minimum h |
|---|---|
| Simply supported | ℓ/20 |
| One end continuous | ℓ/24 |
| Both ends continuous | ℓ/28 |
| Cantilever | ℓ/10 |

**Two-way slabs — ACI 318-19 Table 8.3.1.1** (fy = 420 MPa):

| Condition | Without drop panels | With drop panels |
|---|---|---|
| Exterior panel, no edge beams | ℓn/30 | ℓn/33 |
| Exterior panel, with edge beams | ℓn/33 | ℓn/36 |
| Interior panel | ℓn/33 | ℓn/36 |
| Absolute minimum | **125 mm** | 100 mm |

**Residential slab thickness quick table [practice]:**

| Clear span (longer side) | Slab thickness | Note |
|---|---|---|
| ≤ 3.6 m | 125 mm (5") | Common Pakistani room slab |
| 3.6 – 4.5 m | 125–150 mm | 150 mm if carrying a partition |
| 4.5 – 5.5 m | 150 mm (6") | |
| 5.5 – 6.5 m | 175–200 mm, or introduce a beam | |
| > 6.5 m | Beam-and-slab, ribbed, or PT — get an engineer | |
| Cantilever balcony/chajja | h ≥ projection/10, minimum 100 mm at tip, 125–150 mm at root | Tapered soffit acceptable |

### 8.3 Slab reinforcement rules

| Rule | Value | Source |
|---|---|---|
| Shrinkage & temperature steel ratio | **0.0018 × Ag** (Grade 60 deformed); **0.0020** for Grade 40/50; **0.0014 absolute minimum** | ACI 318-19 §24.4.3.2 / §7.6.1.1 / §8.6.1.1 |
| Minimum flexural steel, one-way slab | As,min = shrinkage & temperature steel = 0.0018·Ag | ACI §7.6.1.1 |
| Minimum flexural steel, two-way slab | 0.0018·Ag each direction | ACI §8.6.1.1 |
| Max spacing, one-way flexural steel | lesser of **3h** and **450 mm** | ACI §7.7.2.3 |
| Max spacing, shrinkage/temperature steel | lesser of **5h** and **450 mm** | ACI §7.7.6.2.1 |
| Max spacing, two-way slab at critical sections | lesser of **2h** and **450 mm** | ACI §8.7.2.2 |
| Max spacing, two-way slab elsewhere | lesser of **3h** and **450 mm** | ACI §8.7.2.2 |
| Practical max spacing **[practice]** | 200 mm main, 250 mm distribution — tighter than code, keeps crack widths small and gives the steel fixer an easy grid | |
| Minimum bar size **[practice]** | 8 mm for distribution, **10 mm for main** (8 mm main bars are too easily bent flat by foot traffic) | |

### 8.4 Minimum steel worked values

```
125 mm slab:  As,min = 0.0018 × 1000 × 125 = 225 mm²/m
              → 8 mm @ 220 c/c (228) ; or 10 mm @ 300 c/c (262)
150 mm slab:  As,min = 0.0018 × 1000 × 150 = 270 mm²/m
              → 10 mm @ 280 c/c (280) ; practical: 10 mm @ 250 c/c (314)
175 mm slab:  As,min = 315 mm²/m  → 10 mm @ 240 c/c
200 mm slab:  As,min = 360 mm²/m  → 12 mm @ 300 c/c (377) or 10 mm @ 200 c/c (393)

Common provided steel (typical residential two-way room slab, M20, Gr.60):
    10 mm @ 150 c/c bottom, short span  (523 mm²/m)
    10 mm @ 200 c/c bottom, long span   (393 mm²/m)
    10 mm @ 150 c/c top over supports, extending 0.25 ℓ each side
    8 mm @ 200 c/c distribution/temperature where main steel is not continuous
```

### 8.5 Cantilever slab (chajja, balcony, sunshade) — the highest-risk element in a house

```
MAIN STEEL GOES IN THE TOP FACE. ALWAYS.
A cantilever is in NEGATIVE moment over its whole length. Bottom-face main steel
does nothing and the slab fails at the root the moment the props are struck.

Detailing:
  - Main bars: top face, perpendicular to the support, running from the tip
    INTO the backspan for a length of  ld  (Section 4.3, use the TOP-BAR value
    with Ψt = 1.3) or 1.5 × projection, whichever is greater
  - Anchor into the backspan slab or beam, never stopped at the support face
  - Distribution steel: bottom or top face, parallel to support, ≥ 0.0018·Ag
  - Some bottom steel at the tip is good practice for handling/temperature — it is NOT
    the main steel
  - Provide a drip groove and a fall away from the building; water ponding at the root
    is the corrosion mechanism that eventually severs the top steel
  - Chairs are MANDATORY — top steel that sags to mid-depth loses half its lever arm
```

### 8.6 Openings in slabs

- Trim every opening larger than ~300 mm with additional bars: place the area of steel
  interrupted by the opening as extra bars on **each side**, extending ld past the opening
  corners, plus 2 diagonal bars (min 12 mm × 1000 mm) at each corner to control the
  re-entrant-corner crack.
- Never cut cast-in slab steel for a plumbing or duct penetration after the pour. Core-drill
  only after a scan and an engineer's approval.

---

## Section 9: Beam-Column Joints

The joint is the least-inspected and most failure-critical region of an RC frame. In
Pakistani informal RC construction, the single most common structural defect is **omitting
column ties inside the joint** because the beam bars make them awkward to install.

### 9.1 Non-seismic joint transverse reinforcement (ACI 318-19 §15.3) **[VERIFY clause numbers]**

```
Within the depth of the DEEPEST beam framing into the joint:
    transverse reinforcement spacing  ≤ 200 mm (8 in)

Within the depth of the SHALLOWEST beam framing into the joint:
    at least TWO layers of horizontal transverse joint reinforcement required

Joints confined by beams on all four faces (each beam ≥ 3/4 of the column face width)
    may use reduced transverse reinforcement per §15.3.2.
```

### 9.2 Seismic joint requirements (ACI 318-19 §18.8)

| Requirement | Value |
|---|---|
| Transverse reinforcement through the joint | **Continue the column confinement hoops (§18.7.5.4) through the joint** at the same spacing as the column end zone — typically 100 mm c/c |
| Reduction where confined on all 4 faces (§18.8.3.2) | Spacing may be relaxed to ≤ 150 mm within the joint depth, with at least half the column hoop amount — **[VERIFY exact provision]** |
| Beam bar development into the joint | Bars must be developed with a **standard 90° hook** (ldh, Section 4.9) turned **into** the joint core, or headed bars |
| Column depth for straight beam bar passing through the joint (§18.8.2.3) | Joint dimension parallel to the beam bar ≥ **20 db** for normalweight concrete (Grade 60) |
| Joint shear strength (§15.4 / Table 15.4.2.3) | Vn = γ·λ·√f'c·Aj ; γ = 1.7 (confined 4 faces), 1.2 (3 faces or 2 opposite), 1.0 (others) — SI, MPa **[VERIFY coefficients against the primary table]** |

**Design consequence of §18.8.2.3:** a 16 mm beam bar passing straight through a joint needs
20 × 16 = **320 mm of column depth**. A 20 mm bar needs **400 mm**. The ubiquitous 230 mm
(9") column **cannot** develop a straight beam bar through the joint — this is a hard
geometric constraint, not a preference.

### 9.3 Joint detailing checklist

```
[ ] Column hoops CONTINUE through the joint at the confined-zone spacing
[ ] Hoops in the joint have 135° seismic hooks, alternating hook positions
[ ] Beam bottom bars at an exterior joint are hooked DOWN into the joint core
    (hook turned into the core, not out toward the cover)
[ ] Beam top bars at an exterior joint are hooked DOWN, tail inside the core
[ ] Straight-through beam bars satisfy the 20·db column-depth rule
[ ] Column longitudinal bars are continuous through the joint — NEVER spliced in a joint
[ ] Joint concrete is the HIGHER of the beam and column concrete grades
    (ACI §15.3 / §18.8.2 — do not pour a joint with slab-grade concrete when the
     column below is a higher grade without checking)
[ ] Crossties provided so no column bar in the joint is laterally unsupported
[ ] Congestion checked in 3D BEFORE fabrication — beam bars from two directions plus
    column bars plus joint hoops physically clash in 230 mm columns
[ ] Pour sequence: joint is poured with the FLOOR (beams/slab), not with the column below
```

---

## Section 10: Staircase Reinforcement

### 10.1 Types

| Type | Description | Typical residential use |
|---|---|---|
| **Waist slab (inclined slab)** | Continuous inclined slab spanning between landings/beams, steps cast on top | **Standard Pakistani house staircase** |
| Folded plate / slabless | Steps form the structure; no waist | Architectural feature; heavier steel, needs engineer |
| Cantilever tread | Treads cantilever from a wall or spine beam | Feature stairs, requires stiff support |
| Spanning transversely | Waist spans between two side walls | Narrow enclosed stairs in load-bearing houses |

### 10.2 Geometry (couple with `architecture-spatial-planning` for the full stair rules)

| Parameter | Residential value | Reference |
|---|---|---|
| Riser | 150–190 mm (Pakistani practice 175–190 mm; **≤ 190 mm**) | Local byelaws / IBC 1011.5.2 |
| Tread (going) | 250–300 mm (≥ 250 mm) | |
| 2R + T | 600–640 mm | Blondel rule |
| Minimum clear width | 900 mm (1000 mm preferred for a main house stair) | |
| Headroom | ≥ 2000 mm (2100 mm preferred) | |
| Landing depth | ≥ stair width; ≥ 900 mm | |
| Max risers per flight | 16 (12–14 preferred) | |
| Waist slab thickness **[practice]** | span/20 to span/25, minimum **125 mm**; 150 mm for flights > 4 m going-to-going | |

### 10.3 Waist slab reinforcement **[practice — general RCC detailing convention, spacing limits mirror ACI §7.7.2.3]**

| Bar | Typical | Placement |
|---|---|---|
| **Main bars** (along the span, i.e. up the flight) | **10–12 mm @ 120–150 mm c/c** | Bottom face of the waist through mid-span; **top face** over landing beams / supports |
| **Distribution bars** (transverse, across the flight width) | **8 mm @ 200 mm c/c** | Above the main bars |
| Landing slab main bars | 10–12 mm @ 150 c/c spanning the landing's shorter direction | |
| Step / tread nosing bars **[practice]** | 8 mm @ each tread, tied to the waist mesh | Controls tread corner spalling |
| Cover | 20–25 mm | ACI slab, interior |
| Max main bar spacing | lesser of **3 × effective depth** and **300 mm** (tighter than the 450 mm slab cap, appropriate for stairs) | |

### 10.4 The re-entrant corner detail — the one stair detail everyone gets wrong

```
At the junction where the FLIGHT meets the LANDING and the corner OPENS OUT
(i.e. the tension face is on the inside of the kink):

  ✗ WRONG:  carry the tension bar continuously around the inside of the corner.
            The resultant of the two bar forces pushes OUTWARD, perpendicular to
            the concrete face. The cover spalls, the bar straightens, the joint
            hinges and the stair drops.

  ✓ RIGHT:  STOP each tension bar and ANCHOR it into the COMPRESSION zone of the
            adjoining member — i.e. cross the bars over, each anchored a full ld
            into the opposite face. Add a diagonal/hairpin bar across the corner.

At a corner that CLOSES (tension face outside the kink), the resultant pushes into
the concrete and a continuous bar is acceptable — but a hairpin is still good practice.
```

### 10.5 Staircase support conditions

- A flight spanning between landing beams is a **one-way slab**; design for the
  **inclined length**, and remember the dead load includes the triangular step concrete
  (≈ 0.5 × riser × 24 kN/m³ per metre of going) plus finishes (≈ 1.0 kN/m²) plus
  live load 3.0 kN/m² (residential stair, ASCE 7 / BCP).
- A flight cantilevering off a landing must have its **main steel in the top face** —
  the same trap as Section 8.5.
- **Do not support a stair flight on a brick wall that is later demolished for a
  renovation.** Note the load path on the drawing.

---

## Section 11: Lintels, Plinth Beams, and Other Residential RCC

| Element | Typical size **[practice]** | Reinforcement **[practice]** |
|---|---|---|
| Door/window lintel, opening ≤ 1.2 m | 230 × 150 mm, bearing 230 mm each side | 2–10 mm bottom, 2–8 mm top, 8 mm stirrups @ 200 |
| Lintel, opening 1.2–2.1 m | 230 × 225 mm, bearing 300 mm each side | 2–12 mm bottom, 2–10 mm top, 8 mm @ 175 |
| Lintel, opening 2.1–3.0 m (garage) | 230 × 300 mm or beam-integrated, bearing 350 mm | 3–12 mm bottom, 2–12 mm top, 8 mm @ 150 |
| Plinth / grade beam | 230 × 300 to 230 × 380 | 4–12 mm (2 top, 2 bottom), 8 mm stirrups @ 200; **cover 50 mm** |
| Boundary wall column (7 ft wall) | 230 × 230 @ 2.4–3.0 m c/c | 4–12 mm, 8 mm ties @ 200 |
| Overhead water tank slab/walls | Walls 150 mm, base 150 mm | 10 mm @ 150 both faces both ways; **cover 40 mm**; M25 preferred, crack width control governs |
| Underground tank walls | 200–230 mm | 12 mm @ 150 both faces; M25 + waterproofing admixture; **cover 40–50 mm** |
| Sunshade (chajja) 600 mm projection | 100 mm at tip, 125 mm at root | **10 mm @ 150 TOP** anchored 900 mm into lintel/slab, 8 mm @ 200 distribution |

---

## Section 12: Bar Bending Schedule and Quantity Estimation

### 12.1 Cutting length

```
Cutting length = Σ(straight segments) + Σ(hook allowances) − Σ(bend deductions)

Hook allowances [practice, IS 2502 convention widely used on Pakistani BBS]:
    180° hook  = 9 db per hook      90° bend end hook = 8 db per hook
Bend deductions [practice]:
    45° bend = 1 db      90° bend = 2 db      135° bend = 3 db

ACI-consistent alternative: model the actual geometry — 12 db tail for a 90° standard
hook, 6 db for a seismic hook, plus the inside bend radius. For a FreeCAD BBS export,
use the actual geometry, not the deduction shortcut.
```

**Stirrup cutting length [practice]**, closed rectangular stirrup with 135° hooks:
```
L = 2(a + b) + 2 × (10 db)  −  (3 × 2 db + 2 × 3 db)
    where a, b = outside dimensions minus 2 × cover
Quick version widely used:  L = 2(a + b) + 24 db  −  ~4.5 db
```

### 12.2 Unit weights and conversion

```
Weight (kg/m) = d² / 162        (d in mm)
Bars are supplied in 12 m (40 ft) lengths in Pakistan; some mills 9 m / 30 ft.
Wastage allowance [practice]: add 3% (good site) to 5% (typical) to theoretical weight.
Binding wire: ~9–12 kg per tonne of reinforcement.
```

### 12.3 Steel consumption thumb rules **[practice — for ordering and costing only, never for design]**

| Element | kg of steel per m³ of concrete |
|---|---|
| Isolated / strip footings | 50–80 |
| Raft foundation | 80–120 |
| Plinth / grade beams | 100–130 |
| Columns | 120–200 (typ. 140–160) |
| Beams | 100–150 |
| One-way / two-way slabs | 70–100 |
| Staircase | 100–130 |
| Retaining wall | 100–130 |
| Water tank | 120–160 |

**Whole-house rules of thumb [practice]:**
- Grey structure steel: **3.5 – 4.5 kg per sq ft** of covered area (RC frame, 2 storey).
- Cement: **0.35 – 0.45 bags per sq ft** of covered area (grey structure, incl. masonry).
- Concrete volume: **~0.045 – 0.055 m³ per sq ft** of covered area.
- If a contractor's steel quantity is below 3 kg/sq ft for a frame house, ask why.

### 12.4 BBS table format to produce

| Bar mark | Element | Bar dia | Shape code | Cutting length (mm) | No. per element | No. of elements | Total no. | Total length (m) | Unit wt (kg/m) | Weight (kg) |
|---|---|---|---|---|---|---|---|---|---|---|
| B1 | GF Beam B-1 bottom | 16 | straight + 2 hooks | 5 240 | 2 | 4 | 8 | 41.9 | 1.578 | 66.1 |

Always add: a shape-code diagram column, a cover note, a concrete grade note, a steel
grade note, and the **"unstamped — for estimation only"** disclaimer from Section "Reality Check".

---

## Section 13: Concrete Placement, Joints, and Curing

| Item | Requirement |
|---|---|
| Free drop height (ACI 318-19 §26.5 / practice) | ≤ 1.5 m; use a tremie or chute for taller columns. Dropping concrete 3 m down a column form segregates it — this is why the bottom metre of Pakistani columns honeycombs |
| Vibration | Poker vibrator, insert vertically at 450–600 mm centres, 5–15 s per insertion, withdraw slowly. **Do not use the vibrator to move concrete horizontally** |
| Construction joint in a beam/slab | Locate within the **middle third of the span**, never at or near a support; provide a shear key or roughened surface + reinforcement continuity (ACI §26.5.7) |
| Construction joint in a column | At the **underside of the beam soffit**, and again 50 mm above the slab top. Never mid-height |
| Column-to-beam pour | Pour columns first, allow ~1–2 hours settlement, then beams and slab monolithically **[practice]** |
| Formwork striking **[practice, verify with engineer]** | Column/beam sides 24–48 h; slab soffit props: 7 days with re-propping, **14–21 days full strike** for spans > 4.5 m; cantilevers **28 days, no early strike, ever** |
| Curing | 7 days minimum wet cure (OPC), 14 days for slabs and water-retaining elements. Ponding, hessian, or curing compound |
| Hot-weather concreting (>35 °C — most of the Pakistani summer) | Pour early morning or at night; shade aggregate; chilled water/ice; ACI 305 practice; keep concrete temperature ≤ 35 °C at placement |
| Testing | 6 cubes/cylinders per 50 m³ or per day's pour, whichever is more frequent; 3 at 7 days, 3 at 28 days. **Insist on this — it is the only objective record that the concrete met grade** |

---

## Section 14: Load Assumptions for Residential Preliminary Sizing **[practice / ASCE 7 & BCP]**

| Load | Value |
|---|---|
| RCC self weight | 24 kN/m³ (25 kN/m³ for reinforced, conservatively) |
| Brick masonry (solid, plastered) | 19–20 kN/m³ → 230 mm wall, 3 m high = **13.8 kN/m** run |
| 115 mm (4.5") partition wall, 3 m | ~6.9 kN/m run |
| Floor finish (screed + tile) | 1.0 – 1.5 kN/m² |
| Roof finish (mud phuska + tiles / waterproofing + screed) | 1.5 – 2.5 kN/m² |
| False ceiling + services | 0.3 – 0.5 kN/m² |
| Live load — residential rooms | 2.0 kN/m² |
| Live load — corridors, stairs, balconies | 3.0 kN/m² |
| Live load — accessible flat roof | 1.5 – 2.0 kN/m² |
| Live load — inaccessible roof | 0.75 – 1.0 kN/m² |
| Water tank | 10 kN/m³ of water + tank self weight |
| Load combinations (ACI §5.3.1) | U = 1.4D ; U = 1.2D + 1.6L ; U = 1.2D + 1.0E + 1.0L ; U = 0.9D + 1.0E |

---

## Section 15: Detailing in FreeCAD

Pair this skill with `architecture-freecad-bim` for the model structure, and
`drawio-diagrams` for 2D rebar detail sheets.

```
Workflow:
1. Build the Site / Building / Storey hierarchy and structural members first
   (Arch Structure objects with real cross-sections from Sections 5–8).
2. Use the BIM/Reinforcement workbench Rebar tools attached to each structural host:
     - Straight Rebar      → slab main/distribution steel, footing mats
     - Stirrup             → beam stirrups, column ties (set the hook angle to 135°)
     - LShape / UShape     → hooked beam bars into columns, cantilever top steel
     - BentShape           → cranked slab bars, curtailed beam bars
     - Helical Rebar       → circular column spirals
3. Set the Rebar object's `Cover` properties from the Section 3.2 schedule —
   front/side/bottom/top individually, not one global value.
4. Set `Amount` or `Spacing` — never both; drive spacing from the Section 8.4 tables.
5. Name every rebar object with its bar mark (B1, C1, S1…) so the BBS export is traceable.
6. Export a bar bending schedule via the Rebar addon's BOM/BBS tool, then
   post-process into the Section 12.4 table format.

Hard limits of the FreeCAD model — state these whenever you hand over a model:
  ✗ FreeCAD does NOT check ACI 318-19 compliance. Rebar objects are geometry only.
  ✗ Cover in the model is only correct if you set it; the default is not code-compliant.
  ✗ No development-length or lap-length check exists — you must place lap geometry
    from the Section 4 tables yourself.
  ✗ No clash detection between beam bars, column bars, and joint hoops by default —
    check joints visually in 3D (Section 9.3).
  ✗ The FEM workbench is NOT an RCC design tool. Do not present FEM output as a
    structural design.
```

---

## Section 16: Common Rebar Detailing Mistakes That Cause Real House Failures

Ordered roughly by how often they appear on Pakistani residential sites and by consequence.

### 16.1 Missing or widely spaced ties at beam-column joints — **the #1 killer**

**What happens:** the steel fixer omits column ties inside the joint because the incoming
beam bars make them fiddly to thread. The joint core is unconfined plain concrete.
**Consequence:** under seismic or even sustained load the joint fails in brittle diagonal
shear; the beam and column separate; the storey collapses. This was a dominant observed
failure mode in RC frame buildings in the 2005 Kashmir earthquake and remains the leading
cause of brittle joint failure in informally-constructed Pakistani RC frames.
**Fix:** pre-assemble the joint hoop cage on the ground; use open U-hoops closed with
crossties if closed hoops cannot be threaded; verify hoop count in the joint before pouring.

### 16.2 90° hooks instead of 135° seismic hooks

**What happens:** ties are bent at 90° because it is faster and the bar bending machine
is set that way. Under load reversal the cover spalls, the 90° hook opens out, the tie
releases, the longitudinal bars buckle.
**Fix:** 135° bend with 6 db ≥ 75 mm extension engaging a longitudinal bar, on every hoop
in every IMRF/SMRF member (ACI §18 seismic hook definition). Non-negotiable in Zones 2B–4.

### 16.3 Blanket "50D lap" for every bar

**What happens:** one number applied to every bar regardless of grade, concrete strength,
bar position, or bar size. Section 4.6 shows 50D is **15% short for a 16 mm bottom bar in
M20** and **34% short for the same bar as a top bar**.
**Consequence:** bond failure at the splice under service or seismic load; flexural cracking
propagating from the splice; in the worst case bar pull-out.
**Fix:** put the actual Class B lap table (Section 4.6) **on the drawing**, per bar diameter,
with separate top-bar and bottom-bar columns. Do not let the site interpolate.

### 16.4 Top-bar effect (Ψt = 1.3) ignored

**What happens:** more than 300 mm of concrete is cast below the bar, so bleed water and
air collect under it and bond strength drops ~25%. ACI compensates with Ψt = 1.3, which
almost no site drawing applies.
**Fix:** all top bars in beams deeper than ~340 mm and all slab top bars over deep beams
use the ×1.3 length. Mark them distinctly on the schedule.

### 16.5 Compression laps in M20 columns not increased by 4/3

**What happens:** 30 db compression lap used, when f'c = 20 MPa < 21 MPa requires 40 db
(ACI §25.5.5.1). 16 mm bar: 480 mm provided vs. 640 mm required.
**Fix:** for M20 columns use 40 db; or specify M25 and use 30 db.

### 16.6 Lap splices placed at high-stress locations

**What happens:** every column bar spliced at exactly floor level, all at the same section —
which is the plastic hinge zone and the maximum-moment location. Beam bottom bars spliced
at mid-span, top bars spliced over the support.
**Consequence:** the splice, the weakest point of the bar, sits where the demand is highest.
**Fix:** apply Section 4.10's decision tree. In seismic frames, ACI §18.7.4.3 permits column
splices **only in the centre half of the clear height**, Class B, with hoops at ≤100 mm.

### 16.7 Cantilever main steel in the bottom face

**What happens:** the steel fixer places the chajja/balcony main steel at the bottom, like
a simply-supported slab. The cantilever is in negative moment; the top face is the tension
face; the top face has nothing but distribution steel.
**Consequence:** sudden brittle failure at the root, often at formwork striking or the first
time someone stands on it. This kills people.
**Fix:** top steel, anchored a full top-bar ld into the backspan, on chairs, checked
personally before the pour. **This item alone justifies a pre-pour inspection.**

### 16.8 Slab top steel walked flat

**What happens:** negative-moment top steel over supports is placed correctly, then labourers
and the concrete pump hose walk it down to mid-depth or to the soffit.
**Consequence:** effective depth halves or vanishes; cracking along the top of every beam
line within a year; long-term deflection.
**Fix:** 12 mm chairs at 1000 mm c/c both ways, walkway boards during the pour, and a
re-check of top-steel level immediately ahead of the pour front.

### 16.9 Inadequate cover — brick chips as spacers

**What happens:** cover maintained with stone chips, broken brick, or nothing at all. Bars
touch the formwork or the soil.
**Consequence:** carbonation and chloride ingress reach the steel in a few years; rust
expands ~6× and spalls the cover; the section loses steel area and bond simultaneously.
Endemic in coastal Karachi and in salt-affected south Punjab soils.
**Fix:** manufactured cover blocks per Section 3.3, at the specified density, plus a
pre-pour cover audit.

### 16.10 Insufficient anchorage of beam bars into exterior columns

**What happens:** a 16 mm beam bottom bar is turned into a 230 mm exterior column with a
100 mm tail, when Section 4.9 requires roughly 265 mm embedment plus a 195 mm tail
(figures pending verification against the primary document, see Section 4.9's flag).
**Consequence:** the bar pulls out of the joint under negative-moment reversal; the beam
loses its positive-moment capacity at the support.
**Fix:** either deepen the exterior column to 375 mm in the beam direction, use headed bars,
or turn the bar down into the column and develop it vertically.

### 16.11 Congestion → honeycombing at the joint

**What happens:** column bars + beam bars from two directions + joint hoops leave no path
for concrete or a vibrator. Result is voided, unconsolidated concrete exactly at the joint.
**Fix:** run a 3D clash check in the FreeCAD model before fabrication (Section 15); reduce
bar count and increase bar diameter; bundle where permitted; widen the column.

### 16.12 Open stirrups / all hooks facing the same way

**What happens:** stirrups fabricated as open U-shapes, or closed stirrups with both hooks
on the same face.
**Fix:** closed stirrups; alternate the hook position along the member so hooks are not all
in one (potentially spalling) corner.

### 16.13 Water added at the mixer / at the pump

**What happens:** the mix is stiff, so the site adds water to improve workability. w/c climbs
from 0.50 to 0.65. Strength drops roughly 30–40%; permeability rises sharply.
**Fix:** use a plasticiser, not water. Slump-test every truck/batch. Reject overwatered loads.

### 16.14 No curing

**What happens:** the slab is poured, the labour moves on, nobody waters it. Pakistani
summer surface temperatures dry the slab within hours.
**Consequence:** plastic shrinkage cracking, surface strength far below design, permanent
loss of durability. **A properly designed and detailed slab with no curing is still a bad slab.**
**Fix:** written curing regime in the contract; ponding within 12 hours; 7–14 days minimum.

### 16.15 Rebar condition ignored

Loose flaky rust and pitting reduce bar area and are not acceptable; tight surface rust
actually improves bond and is fine. Oil, grease, mud, or paint on bars destroys bond —
clean before placing. Never straighten and reuse a bar that was bent to a tight radius.

### 16.16 Structural changes made after the fact

Cutting a slab for a new staircase, chasing a column for plumbing, removing a "non-structural"
wall that was actually load-bearing, adding a storey to a house designed for two. Every one of
these needs an engineer, not a mason.

### 16.17 Tie/development-length clause thresholds swapped or conflated

**What happens:** the No.19/No.22 bar-size boundary that governs the Ψs development-length
modification factor (Sections 2.6, 4.1) gets copied into an unrelated clause with its own,
different bar-size boundary — most notably the tie-bar-size rule (Section 6.2, actual
threshold No.32/No.36). The two clauses look similar (both are "small bars vs large bars"
rules) but come from different code sections with different cutoffs.
**Consequence:** a drawing note or BBS quotes the wrong clause boundary to a reviewing
engineer; even where the practical effect is conservative (as it was here — 13 mm ties
specified where 10 mm would still be code-compliant), a misquoted clause undermines
confidence in every other citation on the same drawing.
**Fix:** when transcribing an ACI bar-size threshold into a detailing note, always confirm
which specific clause it comes from and do not reuse a threshold learned from one clause
in a different one, even if the pattern looks identical.

---

## Section 17: Pre-Pour Inspection Checklist

Run this before **every** structural pour. It is the highest-leverage 30 minutes on the project.

```
GEOMETRY
[ ] Member dimensions match the drawing (measure, don't eyeball)
[ ] Formwork level, plumb, tight, propped, and not deflecting under load
[ ] Levels checked against the datum; slab thickness verified with a depth gauge

REINFORCEMENT — IDENTITY
[ ] Bar diameters match the schedule (measure with a vernier; 16 mm mill bar is often 15.2 mm)
[ ] Bar grade confirmed against the mill test certificate
[ ] Bar count matches per element, both directions

REINFORCEMENT — POSITION
[ ] Cover verified on ALL faces with a cover gauge / measured blocks (Section 3.2)
[ ] Cover blocks present at the specified density, of the correct thickness, not brick chips
[ ] Slab TOP steel on chairs at 1000 c/c; not walked down
[ ] Cantilever main steel is in the TOP face and anchored the full top-bar ld  ← CRITICAL
[ ] Top-steel extension over supports = 0.25–0.30 × clear span each side

REINFORCEMENT — DETAILING
[ ] Lap lengths measured against the drawing's lap table (top vs bottom bars distinguished)
[ ] Lap locations are in the low-stress zones per Section 4.10
[ ] No more than 50% of bars spliced at one section
[ ] Stirrups/ties CLOSED, spacing measured, 135° seismic hooks where required
[ ] Stirrup spacing tightened to the hinge-zone value over 2h at each beam end
[ ] Column hoops CONTINUE THROUGH THE JOINT at confined spacing  ← CRITICAL
[ ] Crossties present so no longitudinal bar is laterally unsupported
[ ] Beam bars hooked into the joint core (tail turned in, not out)
[ ] Column dowels correct in number, size, projection, and splice location
[ ] Opening trimmer bars and corner diagonals in place

MATERIALS & POUR
[ ] Concrete grade confirmed on the delivery docket / mix ratio verified for site mix
[ ] Slump test done and within tolerance; NO water added after the test
[ ] Cube/cylinder samples taken and labelled
[ ] Vibrators on site AND a spare; operator briefed
[ ] Construction joint locations agreed and prepared (Section 13)
[ ] Curing arrangement ready BEFORE the pour starts
[ ] Embeds, sleeves, conduits, and bolt boxes fixed and surveyed
[ ] Pour sequence and stop-ends agreed

SIGN-OFF
[ ] Engineer of record (or their representative) has physically inspected and approved
    → If nobody licensed has signed this off, the pour should not happen.
```

---

## Section 18: Items to Verify Against Primary Documents Before Citing

Do **not** quote these numerically in a client deliverable, a drawing note, or a submission
without opening the source document and confirming the clause and value:

| Item | Where to verify |
|---|---|
| Full concrete cover matrix and its clause number (§20.5.1.3.1 vs the ACI 318-14 §20.6.1.3.1 numbering) | ACI 318-19 Chapter 20, purchased copy — concrete.org |
| Exact wording of §25.5.2.1 on whether Ψs applies inside the splice calculation | ACI 318-19 §25.5 |
| Hooked-bar development length ldh formula (§25.4.3.1) — the db^1.5 coefficient, the "23" denominator, and the ψr/ψo/ψc modifier values used in Sections 4.9, 7.6, and 16.10 | ACI 318-19 §25.4.3 |
| Table 15.4.2.3 joint shear coefficients in SI | ACI 318-19 Chapter 15 |
| §18.8.3 joint transverse reinforcement relaxation for 4-face-confined joints | ACI 318-19 Chapter 18 |
| §13.3 footing effective-width (1.5h) provision and its exact scope | ACI 318-19 Chapter 13 |
| BCP-SP 2007 seismic zone map assignments per city | BCP 2007 PDF — urbanunit.gov.pk/Download/publications/Files/8/2021/Pakistan%20Building%20Code%202007.pdf |
| BCP-SP 2007 hoop-spacing clauses for special moment frames and its R-factor table | BCP-SP 2007 §5 / UBC-97 Ch.16 & 19 |
| Whether the relevant local authority has adopted BCP 2021 or still enforces BCP 2007 | codes.iccsafe.org/content/PKBC2021P1 + the authority's building control office |
| Safe bearing capacity for the actual site | Geotechnical investigation report — never a table |
| Actual bar diameters, grade, and mill certificates | Supplier MTC + on-site vernier check |

### Primary sources

- **ACI 318-19** *Building Code Requirements for Structural Concrete and Commentary* (reapproved 2022) — concrete.org
- **Building Code of Pakistan – Seismic Provisions 2007 (BCP-SP 2007)** — Pakistan Engineering Council / Ministry of Housing & Works; based on UBC-97
- **Building Code of Pakistan 2021 (PKBC 2021)** — codes.iccsafe.org/content/PKBC2021P1
- **UBC-97** — the parent code for BCP-SP 2007's seismic provisions
- **ASTM A615 / ASTM A706 / PS 1879** — reinforcing bar specifications
- **ASCE 7-22** — load combinations and live loads (cross-reference)
- **IS 456:2000** — South Asian cross-reference only; do not mix with ACI in one design

### Companion skills

| Need | Skill |
|---|---|
| Room sizes, circulation, stair geometry, plan layout | `architecture-spatial-planning` |
| Choosing frame vs load-bearing, grid spacing, span/depth ratios, lateral system | `architecture-structural-systems` |
| Building type, floor plate, core, unit mix | `architecture-building-typology` |
| Ramps, stair widths, handrails, accessible routes | `architecture-accessibility-design` |
| Building the 3D model with correct BIM hierarchy and rebar objects | `architecture-freecad-bim` |
| 2D rebar detail sheets, bar bending diagrams, floor plans | `drawio-diagrams` |

---

**Closing reminder:** everything above is a design aid. The moment a user treats it as a
construction document, say so — a PEC-registered structural engineer must design, check,
and stamp, and the local development authority must approve, before anyone pours concrete.
