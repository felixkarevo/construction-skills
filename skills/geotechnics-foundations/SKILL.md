---
name: geotechnics-foundations
description: >
  Soil mechanics and foundation design for buildings in the DACH region per
  DIN 1054 / EN 1997-1 (+NA) and DIN 4017: ground investigation per DIN 4020
  (Geotechnische Kategorien GK1–3, Erkundungstiefen, Baugrundbericht,
  Versuchsliste after EN ISO 17892 / DIN 1812x), soil classification per
  DIN 18196 (Gruppen G/S/U/T/Z, Cu/Cc, wL, Konsistenz IC, Lagerungsdichte Dr,
  kf classes), groundwater and frost susceptibility (F1–F3), bearing capacity
  (tabellarischer Sohlwiderstand DIN 1054, Grundbruch DIN 4017 with g/q/c
  terms, shape and inclination factors, DIN 1054 checks with γG/γB/γR,n/γR,b,
  GS-1/GS-2 combinations), settlement per DIN 4019 (Es/Steifemodul, Kany
  influence values, layered summation), pile foundations per EA-Pfähle (qc
  methods, load-test γR tables, spacing, negative skin friction), earth
  pressure per DIN 4085 (active / increased-active / at-rest / compaction,
  Ka/Kp, GLS deep-slip, grouted anchors), excavation & shoring per DIN 4124
  with Verbau type/depth table and DIN 4123 underpinning, groundwater control
  (Wasserhaltung), basement uplift (UPL/HYD), ground improvement and
  compaction (ZTV E-StB), black-tub vs white-tub waterproofing (WU-Richtlinie
  Beanspruchungsklassen, EGS [a]/[b]/[c], waterstops), typical damages,
  worked examples (isolated footing, cellar wall, retaining wall, uplift),
  FreeCAD/IFC mapping, checklist.
---

# Geotechnics & Foundation Design for Buildings (DIN 1054 / EN 1997-1, DIN 4017)

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

Foundations are the one part of a building that cannot be corrected after the fact. Everything above grade is replaceable; a footing sized against the wrong Sohlwiderstand, a cellar founded in frost-susceptible soil without drainage, or a retaining wall built without a drainage layer produces damage no architectural remedy fixes. This skill provides the numeric and conceptual backbone for **preliminary foundation design in the DIN/EN (DACH) framework**: how to scope and read a ground investigation, how to classify soil, how to carry the DIN 1054 design checks, how to size shallow foundations, piles and retaining structures, and how to keep water out of the basement.

Values marked **(VERIFY)** are digested from table sources whose printed columns were partially corrupted, or are general geotechnical physics not fixed by a single cited clause — confirm against the standard text before quoting in a deliverable.

## Reality Check — Licensing & Liability

**This skill produces design aids and calculation guidance for planning and FreeCAD modelling ONLY.**

Every number in this file — Sohlwiderstand, settlement, wall proportions, reinforcement — is for **preliminary sizing, feasibility, cost estimation and 3D/BIM modelling**. None of it is a construction document.

1. **A site-specific ground investigation (Baugrunderkundung per DIN 4020) supersedes every table here.** Tabular values are orientation. Any real project requires boreholes, sampling and laboratory testing by a competent specialist, and the resulting Baugrundbericht (ground report) governs.
2. **Any design intended for construction of a real, occupied building must be planned, checked and signed by a qualified Tragwerksplaner (structural design engineer).** In Germany the statical analysis is additionally subject to Prüfung by a Prüfingenieur für Standsicherheit for the applicable Gebäudeklasse, and the project as a whole to the Baugenehmigungsverfahren under the state building codes (MBO/LBO). For Geotechnische Kategorie GK3 a specialist geotechnical engineer (Fachgeotechniker) must be involved.
3. **Never present FreeCAD output, a Sohlwiderstand number, a footing schedule or a retaining-wall section from this skill as construction-ready.** Label deliverables "Vorentwurf — nicht zur Ausführung — Prüfung durch Tragwerksplaner erforderlich."
4. **Say this unprompted.** If the user's language suggests they treat the output as final (ordering concrete, starting excavation, skipping the soil report to save money), stop and state the requirement for an investigation, a signed design and authority approval — in that message, not in a footnote.
5. **Highest-risk items where this skill must escalate to a human engineer immediately, no exceptions:** any excavation deeper than ~1.25 m adjacent to a boundary or existing building (DIN 4124 / DIN 4123 territory); any retaining wall over ~1.2 m or with surcharge; any cellar below the highest groundwater level (drückendes Wasser); any site with GK3 indicators (contamination, dikes, artesian pressure / HYD risk, mining subsidence); any cut or slope above ~2 m; any pile foundation; any cellar in frost-susceptible or organic soil.

**Code posture used throughout this skill.** The governing set in Germany is DIN 1054:2010-12 (+A1/A2) with DIN EN 1997-1/NA and DIN EN 1997-2/NA, plus the nationally applied auxiliary rules: DIN 4017 (Grundbruch), DIN 4019 (Setzungsberechnung), DIN 4020 (Erkundungswesen), DIN 4084 (Geländesprünge), DIN 4085 (Erddruck), DIN 18196 (classification), DIN 18300 (Erdarbeiten, VOB/C), EA-Pfähle (2012), EAB (excavation support), DIN 4124 (trench safety), DIN 4123 (excavations beside buildings), WU-Richtlinie (waterproof concrete). All are dated editions from a 2021/22 handbook state — **check current editions before use**. DIN 4149 (seismic zones 1–3, ag = 0.4/0.6/0.8 m/s²; Baugrundklassen A/B/C by Vs > 800 / 350–800 / 150–350 m/s) has been overtaken by DIN EN 1998-1/NA zonation — treat the DIN 4149 grid as historical orientation only (VERIFY the current national map for any site).

---

## Section 0: Foundation Design Workflow (order of operations)

Run these in order. Skipping a step — almost always step 1 or step 2 — is what produces the failures catalogued in §14.1.

```
1. GROUND MODEL
   Baugrundbericht: borehole log, strata, groundwater level,
   φ′/c′/cu, γ, wL/PI, classification DIN 18196, chemistry per DIN 4030.
   No report? → every downstream number is PRESUMPTIVE (tabellarisch). Say so.   §1, §2

2. GEOTECHNISCHE KATEGORIE (DIN 1054 / EN 1997-1)
   GK1 simple (small excavations, no water problems) — GK2 normal —
   GK3 difficult (contamination, dikes, artesian/HYD, deep excavation,
   mining, seismic) → specialist geotechnical engineer mandatory.                 §1.1

3. LOADS & COMBINATIONS
   Actions γG/γB/γQ per DIN 1054; design situations BS-P/BS-T/BS-A/BS-E;
   approaches GS-1 / GS-2 / GEO-3. Characteristic values govern settlement and
   the tabular Sohlwiderstand logic; design values govern the ULS checks.         §3

4. SCREEN FOR PROBLEM GROUND
   Frost-susceptible (F2/F3)? Organic (Z-groups)? Fill (Auffüllung)?
   Weak layer within 2B below founding level? Perched water (Stauwasser)?    §2.5, §11, §12

5. SOHLWIDERSTAND
   Lower of: tabellarischer Sohlwiderstand (DIN 1054 Tab.) with +/− adjustments,
   DIN 4017 Grundbruch ÷ γR;b, plate load test. Apply water correction.           §4

6. FOUNDATION TYPE & DEPTH
   Decision tree. Below frost-affected zone; below topsoil/fill; edge cover
   ≥ ~0.5 m below finished ground; away from slope toes and neighbour lines.      §6

7. SETTLEMENT CHECK (DIN 4019)
   Layered sum with Kany influence values / Es; the structure's sensitivity
   class (setzungsunempfindlich / empfindlich) is already in the tables.          §5

8. WATER
   Construction dewatering (Wasserhaltung), permanent waterproofing decision
   (schwarze / weiße Wanne), drainage per DIN 4095.                            §9, §10

9. RETAINING & SLOPES
   Earth-pressure case per DIN 4085, GLS deep-slip check per DIN 4084,
   anchors per DIN EN 1997-1 / EN 1537.                                            §8

10. LABEL & HAND OFF
    "Vorentwurf — nicht zur Ausführung"; assemble the engineer handoff pack.   §14, §15
```

---

## Section 1: Site Investigation Programme (Baugrunderkundung, DIN 4020)

### 1.1 Geotechnische Kategorien (GK)

| GK | Meaning | Consequence |
|---|---|---|
| GK1 | Simple: small excavations (≤ ~2 m depth), competent uniform ground, no groundwater problems | Reduced documentation; design by normally qualified engineer acceptable |
| GK2 | Normal building case — the default for a house with basement, any raft, any retaining structure, most Verbau | Geotechnical report + geotechnical design by competent engineer normally required |
| GK3 | Difficult: contaminated ground (Altlasten), dike/levee proximity, deep excavations, artesian head / hydraulic-heave (HYD) risk, significant seismicity, mining subsidence (Bergsenkungsgebiet), unstable slopes | **Specialist geotechnical engineer (Fachgeotechniker) mandatory**, extended investigation, full verification list |

### 1.2 Exploration depths (Richtwerte DIN 4020, digested)

Minimum depth of representative boreholes (Aufschlusspunkte) **below the planned founding level**:

| Case | Guideline depth |
|---|---|
| Isolated / strip footing | ≈ 2 × smaller base dimension b below founding level (never stop at a "good-looking" stiff crust without confirming what lies beneath) (VERIFY clause) |
| Raft / basement slab | ≈ smaller plan dimension of the raft below slab base (the stress-influence zone) |
| Excavation / Verbau | 2 × excavation depth, or wall embedment + 2 m below pit base — always below the predicted deep-slip (GLS) circle |
| Piles | ≥ 5 × pile diameter below pile toe, and through any expected weak layer (VERIFY) |
| Cuts / embankments | cut: 20–40 % of cut depth below formation; embankment: below the potential slip surface |

**Generic cross-check for retaining-wall trial bores** (non-DACH-specific, international
handbook rule of thumb — Neufert, *Architects' Data* (Neufert_2002.pdf excerpt), p.54): minimum
trial-bore depth T below the base of a retaining structure, measured from the bore-hole
reference level, T ≥ 3b or ≥ 6 m for a free-standing or rear-anchored in-situ-concrete or
sheet-pile retaining wall (b = the greatest embedment/bore depth among the walls being
investigated), and T ≥ 1.5B or ≥ 6 m where the wall is built into or against the structure
(B = wall height). Use this only as an order-of-magnitude sanity check on the DIN 4020
exploration-depth logic above — it is not DIN/EN-specific and does not substitute for the §1.2
table or the investigating engineer's judgement on strata variability.

### 1.3 Number and spacing of Aufschlusspunkte

Design the grid to answer the design questions (layer boundaries, dip, weak-layer depth, water table): small regular house plot on expected uniform glacial/alluvial ground → **at least one representative deep borehole**, two where strata are variable or the plan is irregular; with basement → boreholes around the excavation corners and mid-sides; supplement with continuous probe profiles (Rammsondierung / dynamic penetration) between boreholes to catch lenses and gravel pockets. Spacing logic: 3–5 m in erratic made ground, 15–25 m in uniform natural deposits (planning heuristic, VERIFY against DIN 4020 tables).

### 1.4 Sampling quality and the test list to demand

Sample categories A/B/C ↔ sample-quality classes 1–5 (A = undisturbed, sealed, wax-ended; C = disturbed/bulk). Tests that feed the calculations in this skill (standard families per EN ISO 17892 series and DIN 1812x, VOB/C Homogenbereich logic):

| Test | Standard family | Feeds |
|---|---|---|
| Grain-size distribution | DIN EN ISO 17892-4 | DIN 18196 group, kf estimate, frost class |
| Atterberg limits wL, wP (PI = I_A) | DIN EN ISO 17892-12 | U/T split, L/M/A bands, IC |
| Water content; bulk & dry density | ISO 17892-1, ISO 17892-2 / DIN 18125-2 | γ, γ′, compaction degree |
| Density index Dr (cohesionless state) | DIN 18126, EN ISO 14688-2 | §2.4, §4.2 |
| Shear strength c′, φ′ (triaxial) | ISO 17892-8/-9/-10 | DIN 4017, DIN 4085 |
| Undrained shear cu | ISO 17892-7, DIN 4094-4 | short-term clay, piles |
| Oedometer / constrained modulus Es | DIN 18135 (family) | DIN 4019 settlement |
| Permeability kf | DIN 18130 (lab) + field pumping tests | Wasserhaltung, drainage |
| Organic content (ignition loss) | DIN 18128 | Z-groups, compressibility, frost |
| Carbonate / lime content | DIN 18129 | solubility, aggression |
| Sulphate, chloride, pH of soil & groundwater | EN 1997-2 / DIN 4030 | concrete exposure (XA), anchor corrosion DIN 50 929-3 |
| Field penetration tests (DPL / DPSH / CPT) | EN ISO 22476-2/-3/-1 | continuous qc/N profile → §2.4, §4.3, §7.4 |

**Never accept a report for a site with fill, water, or neighbouring structures that omits: (a) the highest observed / seasonal groundwater level, (b) groundwater and soil chemistry (sulphate, ammonium, magnesium, pH, aggressive CO₂ per DIN 4030), (c) a description of what terminated the boring — refusal, rock, or "unknown".**

### 1.5 Baugrundbericht (ground report) — minimum content

Strata log with DIN 18196 symbols and state (IC / Dr); γ/γ′; φ′/c′/cu as design assumptions; Gründungsvorschlag (recommended foundation type and depth); setzungsverhalten (settlement behaviour); groundwater regime including perched water (Stauwasser) and seasonal fluctuation range; chemical attack classes for concrete; earth-pressure parameters for any retaining design (φ′, δ, permitted surcharge); remarks on Verbau and Wasserhaltung; for GK3 an explicit HYD / artesian-head assessment. Ask the investigating engineer to state the **Bemessungswerte (design values) of the soil parameters** — a borehole log without them is half a report.

---

## Section 2: Soil Classification & Index Properties (DIN 18196 / DIN EN ISO 14688)

### 2.1 Grain-size framework

Boundaries used in DIN 18196 (subdivisions of the ISO 14688 scale):

| Fraction | Size range (mm) | Symbol |
|---|---|---|
| Feinstkorn (Ton + Schluff, fines) | < 0.063 | U, T |
| — Ton (clay) / Feinstkorn lower bound | ≤ 0.002 | T |
| — Schluff (silt) | 0.002–0.063 | U |
| Sand | 0.063–2.0 | S |
| Kies (gravel) | 2.0–63 | G |
| Steine (cobbles) | 63–200 | Co (ISO 14688) |
| Blöcke (boulders) | > 200 | Bo |

### 2.2 Main groups and suffix logic (the classification engine)

- **Coarse-grained (≥ 50 % of the soil > 0.063 mm):** gravel **G** vs sand **S** decided by which dominates the coarse fraction (gravel fraction > sand fraction → G). Fines content tags the sub-group: < 5 % fines → clean (GW, GP, SW, SP); 5–15 % → dual symbol (GM, GC, SM, SC); 15–40 % → mixed with the fines letter in the name (GM/GC/SM/SC, read "sandig-tonig" etc.); > 40 % fines → the **fines group governs** (G/S become adjective suffixes: "sandig/kiesig" added to T/U groups).
- **Clean coarse groups — grading suffix (w = gut abgestuft well graded, u = gleichförmig uniformly/poorly graded, m = mittel):** on Cu = d60/d10 and Cc = d30²/(d10·d60): **w** when Cu ≥ 6 AND 1 ≤ Cc ≤ 3; **u** when Cu < 3 OR Cc outside 1–3; intermediate cases (Cu ≥ 3 with Cc = 1 but w-criteria not met) → **m** (VERIFY the exact DIN 18196 grid — the digest rows were partially garbled; the w/u thresholds are the standard logic).
- **Fine-grained (fines > 40 %):** U (Schluff) vs T (Ton) by plasticity position relative to the Casagrande line; liquid-limit bands: **L** wL < 35 %, **M** 35–50 %, **A/H** > 50 % (high-plasticity clay = TA; silts UL/UM/UA — digest nomenclature uses A for the high band).
- **Organic:** Z-groups (Moos, Faserstoffe…) and the O-suffix (GT, OT, OH…): colour scales with humus — 2–6 % schwach organisch (grey), 6–20 % mäßig (dark grey), > 20 % stark (black). Organic soil is **never** a founding stratum for a building; remove or bypass.
- Groups typical of Central European house sites: GW/SE/SW glacial sands and gravels (Schmelzwassersande, Geschiebe), GM/SM the "boring middle" — check Dr, TL/TM/TA stiff clays (Mergel, Geschiebeton), UM/UA silts, OH/GT moor and peat (Moor, Anmoor), and **Auffüllung (fill)** — not a soil group at all; it is a removal-or-bypass decision.

### 2.3 Consistency of cohesive soils — index IC and field check

IC = (wL − w) / I_A, with I_A = wL − wP (Plastizitätszahl):

| IC | Konsistenz | Field feel | SPT N | Orientation qu (kN/m²) |
|---|---|---|---|---|
| < 0.25 | breiig (pasty) | flows between fingers | 0–2 | 25–50 |
| 0.25–0.50 | sehr weich | extrudes under fingers | 2–4 | 25–50 |
| 0.50–0.75 | weich | moulds easily | 4–8 | 50–100 |
| 0.75–1.00 | halbfest / steif | moulds only with strong pressure; thumb indents | 8–15 | 100–200 |
| > 1.00 | fest | thumbnail only | 15–30 | 200–400 |
| — | sehr fest / trocken hart | knife cut, not finger | > 30 | ≥ 400 |

(SPT↔consistency↔strength grid digested from the handbook tables; correlations are orientation only. In clay, **never design from SPT alone** — require cu from undisturbed samples. Never found a shallow footing in breiig / sehr weich.)

### 2.4 State of cohesionless soils — Dr and qc

| Lagerungsdichte | Dr (%) | qc (MN/m²) | Consequence |
|---|---|---|---|
| sehr locker | < 15 | < 2.5 | no shallow footing — improve, raft, or bypass |
| locker | 15–35 | 2.5–7.5 | marginal; settlement-governed; tabular qR at the low end |
| mitteldicht | 35–65 | 7.5–15 | normal strip/footing territory |
| dicht | 65–85 (DIN 1054 min. "dicht" note at qc ≥ 15) | 15–25 | good; +50 % tabular increase may apply (§4.3) |
| sehr dicht | > 85 | > 25 | excellent |

Dynamic-probe → static-cone conversion (Rammsondierung FS→qc factors, digested): silty/fines-rich sand 0.3–0.4; clean sand 0.5–0.6; well-graded sand/gravel mix 0.5–1.0; gravelly soils 0.8–1.0 (VERIFY column mapping).

### 2.5 Groundwater — measurement and design use

- Read a **standpipe over a season**, not "water struck at" in a single borehole. Design water level = highest seasonal level; perched water (Stauwasser on a clay lens) presses on walls and slabs even when the main table is far below.
- Buoyancy: below the table use γ′ = γ_sat − γw with γw = 9.81 ≈ 10 kN/m³. This roughly halves the γ·b·Nγ term in DIN 4017 — the tabular −40 % water reduction of §4.3 is its practical cousin.
- Fluctuating level: the permanent low level is a permanent action; fluctuation above it is variable (EAU/EA logic).
- Freezing: water in the freeze zone generates Frosthebung (frost heave). Footings in F2/F3 soil (§11.2) must sit below the seasonally frost-affected zone; the depth is regional (local practice / authority guidance — commonly assumed ~0.5–0.8 m in temperate lowland Central Europe, **not fixed in the digested sources — VERIFY**), or frost is neutralised by an F1 replacement layer.
- Underground geometry: a basement below the table raises the permanent questions — UPL (uplift), HYD (hydraulic heave at the pit base), seepage past the wall (§8.6, §9.4, §11.1).

### 2.6 kF classes (permeability, DIN 18130-1)

**Five classes** (not six — confirmed against Wendehorst Tafel 14.64, DIN 18130-1,
VERIFY tag dropped): k < 10⁻⁸ m/s → sehr schwach durchlässig; 10⁻⁸ to 10⁻⁶ →
schwach durchlässig; > 10⁻⁶ to 10⁻⁴ → durchlässig; > 10⁻⁴ to 10⁻² → stark
durchlässig; > 10⁻² → sehr stark durchlässig. Engineering anchors (soil-type
correlation, orientation only): clean gravel kf ≈ 10⁻²–10⁻³ m/s; sand
10⁻³–10⁻⁵; silty sand 10⁻⁵–10⁻⁶; silt 10⁻⁶–10⁻⁷; clay < 10⁻⁷–10⁻⁹ m/s. kf
selects the dewatering method (§9.4) and governs drainage design (DIN 4095, §10.5).

### 2.7 Presumptive parameter set by group (orientation only — the Baugrundbericht governs)

γ/γ′ feed bearing + earth pressure; φ′/c′ feed drained design; cu follows from IC (§2.3). Typical values for undisturbed aged natural ground (planning set — **VERIFY every row against the site report**):

| Group | γ sat. (kN/m³) | φ′ (°) | c′ (kN/m²) | Notes |
|---|---|---|---|---|
| GW/GE, SE/SW dicht | 20–22 | 36–42 | 0 | best house ground; dilative |
| SM/GM mitteldicht | 19–20 | 30–35 | 0–5 apparent | apparent c from fines — not counted in Erddruck |
| UL/UM steif | 18–20 | 25–32 | 5–15 | Stauwasser risk on lenses |
| TL/TM steif/halbfest | 18–20 | 22–30 | 5–25 | IC governs; seasonal crust trap (§5.3) |
| TA high-plasticity | 16–19 | 18–26 | 10–40 | swell/shrink screening (§11.3) |
| OT/OU/H organic, peat | 10–14 | — | — | never a founding stratum; very high compressibility |
| Auffüllung (fill) | 16–20, erratic | 20–30, erratic | — | age + compaction decide; young fill = remove/bypass |
| Mergel / weathered rock | 20–22 | 25–35 | 50–200 | slakes on exposure — cover the base fast |

Unit weights cross-check against the digested EN 1991-1-1 table: Stahlbeton 25, Naturbeton 24, Mauerwerk 12–24 by density class, water 10.0, saturated sand/gravel 20–22 kN/m³.

---

## Section 3: Safety Concept (DIN 1054 / DIN EN 1997-1)

### 3.1 Design situations, limit states, approaches

- Design situations: **BS-P** persistent, **BS-T** transient (every excavation stage is BS-T; struts and anchors are checked in BS-P), **BS-A** accidental, **BS-E** seismic.
- Limit states GZT (ULS): EQU (equilibrium/uplift UPL), STR (structural), GEO (soil: Grundbruch, earth pressure, GLS slope, anchors), HYD (hydraulic heave / piping / seepage). GZG (SLS): γ = 1.0.
- German practice runs the NA combinations as factor groups:
  - **GS-1** (≈ DA1 set B / GEO-2): actions factored — γG;sup 1.35 / γG;inf 1.00, γQ;sup 1.50; **soil strength factored** — γφ′ ≈ 1.25, γc′ ≈ 1.40, γcu ≈ 1.25 (VERIFY grid); earth/bearing resistance additionally γR;b (≈ 1.35–1.40); passive earth pressure γE ≈ 1.40 (P) / 1.30 (T) / 1.20 (A) (digest sequence — VERIFY).
  - **GS-2 / GEO-3 (global)**: unfactored-ish actions with γφ′ ≈ 1.10 and γR = 1.0 — the balanced set for circular-slip (GLS) and overall-stability analyses (VERIFY per DIN 1054 factor tables).
  - **UPL**: γH (water) 1.35 unfavourable against γG 0.90 favourable; **HYD**: γG 1.00, γH 1.00.
- **Pick one approach per check and name it in the calculation.** Do not mix γG = 1.35 action factoring with a GEO-3 resistance set — the resulting "safety" is arithmetic, not geotechnical.

### 3.2 Action factors (digested table)

| Case | Factors |
|---|---|
| EQU overturning (Lagesicherheit) | destabilising G 1.10 (small variation 1.05) / stabilising G 0.90 (small variation 0.95); Q 1.50 / 0 |
| GS-1 STR/GEO | γG 1.35 / 1.00; γQ 1.50 / 0 |
| GEO set variant | γG 1.00; γQ 1.30 unfavourable (paired with factored strength) |
| Hydrostatic head γH | 1.35 unfavourable / 0.85 favourable (UPL uses 1.35 / G 0.90; digest also lists γG;fav 0.95 — VERIFY the pairing you cite) |
| Imposed surcharge q (traffic, storage) | γQ 1.50 |

### 3.3 Resistance factors of interest

| Check | γR |
|---|---|
| Grundbruch shallow foundation | γR;b ≈ 1.35–1.40 (VERIFY edition) |
| Pile compression, static load tests | γR;c = 1.35 / 1.25 / 1.15 / 1.05 / 1.00 for n = 1 / 2 / 3 / 4 / ≥ 5 tests |
| Pile tension, static load tests | γR;z = 1.35 / 1.15 / 1.00 for n = 1 / 2 / ≥ 3 tests |
| Piles from experience / settlement sum | γR;m = 1.40 / 1.50 |
| GLS slope (GEO-3) | γφ ≈ 1.10 with γG;equ 1.10 — a slope check is an engineer's deliverable, not a table lookup |

(Pile test γR grids digested from EA-Pfähle; VERIFY n-thresholds.)

### 3.4 Design values of soil parameters

tan φ′d = tan φ′k / γφ′; c′d = c′k / γc′; cu;d = cu;k / γcu. Use **drained (c′, φ′)** for long-term effective-stress problems and **undrained (cu)** for short-term clay; never mix the two in one check. The tabular Sohlwiderstand (§4.2) and the DIN 4085 coefficient approach (§8) already embed their own factor assumptions — **do not double-factor**. The classic DACH error: taking a tabulated qR;d and then also dividing the load combination by γG = 1.35 "to be safe", or conversely applying γφ′ to a friction angle already read out of a factored table.

### 3.5 One micro-example to fix the factor bookkeeping

Retaining thrust, φ′ = 30°, γ = 18 kN/m³, H = 3 m, GS-1:

```
Characteristic:  Ea,k = ½·Ka(30°)·γ·H² = 0.5·0.333·18·9  = 27.0 kN/m
Design GS-1:     φ′d = arctan(tan30/1.25) = 24.8° → Ka ≈ 0.415
                 Ea,d = γE·½·Ka(φd)·γ·H² = 1.35·0.5·0.415·18·9 ≈ 45.4 kN/m
Design GEO-3 (global): φ′d on γφ′ = 1.10 → 27.7° → Ka ≈ 0.365,
                 Ea ≈ 0.5·0.365·18·9 = 29.6 kN/m, carried at γG = 1.0 on
                 actions against γR = 1.0 resistances — the circle check then
                 balances on its own factor set (exact GS factor grid:
                 VERIFY §3.1 note).
Both are legitimate; adding γG 1.35 to the GEO-3 set (or re-factoring the GS-1
tabulated Sohlwiderstand) double-counts and silently changes the safety level.
```

---

## Section 4: Bearing Capacity (Sohlwiderstand; Grundbruch per DIN 4017)

### 4.1 Two routes, one governing check

```
Route A (normal houses): tabellarischer Sohlwiderstand qR;d,k  (§4.2–4.3)
   — settlement-informed, water-corrected; Grundbruch implicitly covered.
   Check: design base pressure ≤ qR;d,k (with the §4.3 adjustments).
Route B (large/wide loaded areas, rafts, embedment benefit, verification):
   DIN 4017 Grundbruch (§4.4):  Rd = Rk / γR;b ≥ Ed.
Settlement (§5) is the real design limit for buildings — bearing rarely fails
first; differential settlement is what cracks houses.
```

### 4.2 Tabellarischer Sohlwiderstand (DIN 1054 Tabellen 1–6, digested)

qR;d,k [kN/m²] as a function of footing width b (0.5–3 m) and founding depth d (0.5–2 m), groundwater well below the base. **Confirmed against Wendehorst Tafel 14.23/14.24 — clean tables, VERIFY tags below dropped:**

Non-cohesive soils (GW, SE/SW, GM, SM, GU, GT, SU …), **setzungsempfindliche Bauwerke** (Tab. 1, b in m):

| d\b | 0.5 | 1.0 | 1.5 | 2.0 | 2.5 | 3.0 |
|---|---|---|---|---|---|---|
| 0.5 | 280 | 420 | 460 | 390 | 350 | 310 |
| 1.0 | 380 | 520 | 500 | 430 | 380 | 340 |
| 1.5 | 480 | 620 | 550 | 480 | 410 | 360 |
| 2.0 | 560 | 700 | 590 | 500 | 430 | 390 |

**setzungsunempfindliche Bauwerke** (Tab. 2, b in m — table continues past b=2 in the source):

| d\b | 0.5 | 1.0 | 1.5 | 2.0 |
|---|---|---|---|---|
| 0.5 | 280 | 420 | 560 | 700 |
| 1.0 | 380 | 520 | 660 | 800 |
| 1.5 | 480 | 620 | 760 | 900 |
| 2.0 | 560 | 700 | 840 | 980 |

For small structures, embedment 0.3 m ≤ d ≤ 0.5 m is permitted. The two families
coincide at b ≤ 1 m and diverge for wider footings — **empfindlich is always
≤ unempfindlich at the same (b,d)**, confirming the earlier conservative reading.

Cohesive soils (Tabellen 3–6): groups UL / SU̅,ST,GU̅,GT̅ / UM,TL,TM / TA with
consistency steif/halbfest/fest columns and embedment 0.5–2.0 m rows, values
130–700 kN/m² — matches the digested fragments (UL/TL steif/halbfest ~180–210
at d = 0.5 rising ~250–390 at d = 1.0; UM/TM mid bands ~210–310; TA ~460/530/
620/700 rising with d); confirmed correct, VERIFY tag dropped. Very soft/organic
(breiig, OH/OT): not tabulated → improvement, raft or piles.

### 4.3 Adjustments to the tabular value (digested rules)

| Condition | Adjustment |
|---|---|
| Groundwater at / near base level | **− 40 %** ("gw am Grundungsprofil") — interpolate for levels in between |
| State verified "dicht" by probe profile (qc evidence) | **+ 50 %** (dense/sondier rule) |
| Wide footings b > 2 m | + 10 % per metre of b, capped at b = 5 m |
| Long strip footings / walls (b/l > 5) | × 0.7 (digested reduction — VERIFY direction against table notes) |
| Very small footings b ≤ 0.3 m, minor structures | tabular floor ~210 kN/m² usable (small-structure allowance — VERIFY) |
| Net vs gross | tables are **gross** base-pressure values — compare against total σ0 including footing and overburden weight |

### 4.4 Grundbruch per DIN 4017 (Route B)

```
Rk = b′·aγ·γ′·Nγ  +  q′·aq·Nq  +  c′·ac·Nc        (effective, buoyant terms)
Rd = Rk / γR;b   ≥   Ed
```

- **Effective area** for eccentric/inclined resultant (kernel/Meyerhof logic): b′ = b − 2e_b, l′ = l − 2e_l. Keep the load inside the middle third (e ≤ b/6) or the base partly lifts off (klaffende Fuge, §13.5).
- **q′** = effective surpressure at founding level = Σγ·(depth; buoyant below GW); the embedment credit is real — a basement's overburden pays into this term (floating/net-effect logic §6.4).
- **Bearing capacity factors Nc0/Nd0(≈Nq)/Nb0(≈Nγ)(φ′)** — DIN 4017 Tabelle 1,
  confirmed against Wendehorst Tafel 14.26 (φ′ in degrees):

  | φ′ | 0 | 5 | 10 | 15 | 20 | 22.5 | 25 | 27.5 | 30 | 32.5 | 35 | 37.5 | 40 | 42.5 |
  |---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
  | Nc0 | 5.0 | 6.5 | 8.5 | 11.0 | 15.0 | 17.5 | 20.5 | 25 | 30 | 37 | 46 | 58 | 75 | 99 |
  | Nd0 | 1.0 | 1.5 | 2.5 | 4.0 | 6.5 | 8.0 | 10.5 | 14 | 18 | 25 | 33 | 46 | 64 | 92 |
  | Nb0 | 0 | 0 | 0.5 | 1.0 | 2.0 | 3.0 | 4.5 | 7 | 10 | 15 | 23 | 34 | 53 | 83 |

  Closed-form generators (same source): Nd0 = tan²(45°+φ′/2)·e^(π·tanφ′);
  Nb0 = (Nd0−1)·tanφ′; Nc0 = (Nd0−1)/tanφ′ (φ′ = 0 case handled separately,
  Nc0 = π+2). Never mix DIN 4017 factors with Terzaghi/Vesic factors and
  their shape rules interchangeably.
- **Shape factors (Beiwerte a)** from the digested grid (Streifen → Rechteck → Quadrat, b/l 0.7–1.2): aγ falls with decreasing b/l (→ ~0.7 square), aq and ac rise (aq ≈ 1 + (b/l)·sinφ′-family; ac → aq). **Inclination factors** reduce all three terms when the resultant is inclined. Use the DIN 4017 scheme consistently.
- The **Kany influence grid** (same standard family, fully recovered in the source: rows z/b 0.05–18 × columns b/l 1–10, w1/w2 values 0.98 → 0.0015) gives the vertical stress increment under any loaded rectangle — the backbone of §5.2 and of embedment/net-effect reasoning.

### 4.5 Allowable vs design framing (how houses actually get checked)

German residential practice still commonly runs **σB,zul against characteristic loads** (legacy allowable framing), while DIN 1054 requires **qR;d / Rd against Ed**. The tabular route is a settled design-value table; either framing works **if declared**. The worked example §13.1 reproduces the published "German practice" hybrid (service column load + γG = 1.35 on footing self-weight against a tabular allowable) — defensible for preliminary sizing only; the execution design must run one coherent approach.

### 4.6 Embedment credit and the net effect

The q′·Nq·aq term makes founding depth a genuine asset: every metre of competent, permanently present overburden adds ≈ Nq·aq × its weight to Rk (φ′-dependent). A basement's perimeter soil weight therefore pays twice — in equilibrium and in bearing. Two rules keep this honest: (1) credit only soil that is **permanently present and stable** (never a future excavation, a planting bed, or the toe soil in front of a retaining wall); (2) for settlement (§5), the **net** added stress is Δσ = σ_base − γ·d_excavated — the excavation-float credit (§6.4) is real there too. Reconcile both uses explicitly: bearing compares gross pressure with the table; settlement uses the net increment.

---

## Section 5: Settlement (Setzungsberechnung, DIN 4019)

### 5.1 Components and awareness

```
s∞ = si (immediate/elastic) + sc (consolidation of fines) [+ ss secondary]
Cohesionless ground: settles during construction — elastic, fast, usually harmless.
Cohesive ground: time-dependent primary consolidation — this is what keeps
                 cracking houses for years.
The damaging quantity is differential settlement and tilt
(Verkantung ω = Δs / L between two points).
```

Deformation parameters (digested concept set): **Es** (constrained/oedometer modulus, from
DIN EN ISO 17892-5 one-dimensional compression tests — tangent or secant, cohesive soils),
**E** (elastic/Young's modulus, from triaxial tests per DIN EN ISO 17892-8/-9, cohesive
soils), **Ev / Ev2** (plate-load modulus per DIN 18134). These three are **not** independent
sources of scatter — they are the same linear-elastic soil idealization read at different
loading geometries, and DIN 4019/EVB gives the exact conversion via Poisson's ratio ν
(0 ≤ ν ≤ 0.5), which is what an elastic FEM soil model actually needs (Es alone is not enough
for a general 3D/plate FEM continuum — it is the constrained 1D value; E is the one to assign
to an isotropic elastic soil material):

    E  = [(1 − ν − 2ν²)/(1 − ν)] · Es          Es = [(1 − ν)/(1 − ν − 2ν²)] · E
    E  = (1 − ν²) · Ev                          Ev = [1/(1 − ν²)] · E

Typical ν for a first FEM estimate (not a substitute for triaxial data): drained sand/gravel
≈ 0.25–0.35; drained clay ≈ 0.3–0.4; **undrained clay (short-term, total-stress FEM run)
ν → 0.5** (near-incompressible — use a mixed/u-p formulation or ν ≤ 0.49 numerically, not
exactly 0.5). Rigid circular plate on an infinite homogeneous elastic half-space:
s = 1.5·σz·r/Em (r = plate radius, Em = mean compression modulus back-calculated from
observed settlements of comparable foundations per DIN 4107 — a 4th, empirical route
alongside Es/E/Ev, useful when no lab/plate data exists but comparable case histories do).
Orientation conversion between Es and Ev2 without going through ν is source-dependent
(sands/gravels roughly Es 2–3× Ev2, fine-grained up to 5–7× — VERIFY; where settlement
matters, run the oedometer test instead of correlating). Es orientation bands (MN/m²):
soft/organic < 5; steif clay ~10–20 → fest 30–60; mitteldicht sand ~10–20; dicht sand/gravel
20–60 (orientation, VERIFY).

### 5.2 Layered summation with Kany influence values

```
s = Σ [ (σ0,i + ½Δσi) / Es,i ] · Δzi                 (DIN 4019 layered scheme)
Δσ(z) = q · w(z/b ; b/l)                              (Kany grid, w1 centre / w2 corner)
sum until Δσ ≤ ~5–10 % of σ0  (practically z ≈ 2–3 b below the base)
Verkantung η / rigidity factors per DIN 4019 (steif bodies redistribute —
compute the flexible-ground settlement, then judge whether the structure bridges).
```

The **sensitivity class** already embedded in the DIN 1054 tables (§4.2) is the code's route to allowable settlement: an empfindlich structure is pushed to the lower Sohlwiderstand so settlement stays small implicitly. No single mm-limit exists in the digested tables; a practical preliminary target for ordinary houses on normal ground is total settlement ≲ 20–30 mm and angular distortion ≲ 1/500 (engineering judgement — VERIFY against project requirements). On soft ground, improve / raft / pile instead of debating limits.

### 5.3 The four traps

1. **Two storeys beside one** on clay — different Δσ, same Es, different s → movement joint through everything, or one continuous raft.
2. **Desiccated stiff crust over soft clay** (N/IC high for 1–2 m, then collapsing values) — the crust is a trap: compute settlement on the layer beneath, found below the seasonal moisture-change zone.
3. **Plate-load myopia** — a plate stresses only ~2× its width; a weak layer 3 m down is invisible. Plate tests supplement boreholes, never replace them.
4. **Size-dependent ks** — the subgrade modulus from a small plate is not a raft input; correct it for width.

### 5.4 Layered-sum micro-example (method illustration, assumed factors)

Strip footing b = 0.8 m, base pressure gross 150 kPa at d = 1.0 m, γ = 19; under it a 3 m TL clay (Es = 15 MN/m²) over gravel. Δσ at depth z under the centre via the 2:1 stress-spread (Kany-grid stand-in — use the grid, not this, for real work):

```
q_net = 150 − 19·1.0 ≈ 131 kPa (the increment that matters)
Δσ(z) ≈ q_net·b/(b+z);  σ0(z) = γ·(d + z)   [mid-layer depths]
z = 0.5 m: Δσ ≈ 131·0.8/1.3 = 81 ; σ0 = 1.5·19 = 28
z = 1.5 m: Δσ ≈ 131·0.8/2.3 = 46 ; σ0 = 2.5·19 = 48
z = 2.5 m: Δσ ≈ 131·0.8/3.3 = 32 ; σ0 = 3.5·19 = 67
Layer 1 (0–1 m): s1 = (28+81)/2/15000·1.0 ≈ 3.6 mm
Layer 2 (1–2 m): s2 = (48+46)/2/15000·1.0 ≈ 3.1 mm
Layer 3 (2–3 m): s3 = (67+32)/2/15000·1.0 ≈ 3.3 mm
Below 3 m Δσ ≤ ~5 % σ0 → stop.  s ≈ 10 mm under the strip centre.
The neighbouring pad at 8 m spacing adds only ~2–3 mm at this point
(§5.2 superposition) — differential settlement is a function of the LOAD
pattern, not only of the soil.
```

---

## Section 6: Foundation Selection, Sizing & Detailing

### 6.1 Minimum founding depth (Gründungstiefe)

| Rule | Value / source |
|---|---|
| Below the frost-affected zone in F2/F3 soil (or neutralised by F1 replacement layer) | regional frost depth — local practice/authority (commonly ~0.5–0.8 m temperate lowland; VERIFY) — §11.2 |
| Fully below topsoil, humus, peat, recent uncontrolled fill (Auffüllung) | always |
| Minimum edge embedment below finished ground | ~0.5 m (splash, frost, mechanical) (planning value) |
| Adjacent shallower trench/service invert | keep the footing base above a 1V:2H line from the trench bottom (loses lateral support below it) |
| Adjacent existing foundation | new base ≥ existing base; deeper → DIN 4123 underpinning procedure (§9.3) |
| Near slope/cut toe | outside the potential GLS wedge; slope check for cuts > ~2 m (§8.7) |
| Raft on compressible fine-grained ground | on a compacted F1 levelling layer (Kapillarbruch + Planum), §12 |

Rankine-style cross-check for embedment under a loaded footing (classic physics, universal): D_min ≈ (q/γ)·Ka² — e.g. q = 200 kN/m², γ = 19 kN/m³, φ′ = 30° → Ka = 1/3 → D_min ≈ 1.17 m. A useful plausibility companion to the tables, not a code substitute.

### 6.2 Decision tree (DIN 1054 framing)

```
START: Baugrundbericht (groups, IC/Dr), γ/c′/φ′/cu, design gw level,
       characteristic loads, building sensitivity class.

Q1. Fill / organic / soft layer within 2B below the planned base?
    YES → excavate & replace in compacted layers with F1 material (§12) if thin
          (≤ ~1.5–2 m), else bypass with piles → §7.
    NO → Q2
Q2. Frost-susceptible soil (F2/F3) with water in the freeze zone?
    YES → found below frost depth, or cap the footing under ≥ 40–60 cm F1 layer
          (VERIFY regional depth + cap rules).
    NO → Q3
Q3. Basement and water table above slab base?
    YES → waterproofing route decision §10 (schwarze vs weiße Wanne)
          + UPL/HYD checks §11.1.
    NO → Q4
Q4. Load-bearing masonry wall system (Querscheiben — typical EFH/MFH)?
    YES → strip footing (Streifenfundament) under the wall grid; tabular
          qR;d,k ≥ ~150–200 kN/m² at d ≈ 0.8–1.2 m usually suffices for
          2–3 storeys → §6.3.
    NO (RC frame, point loads) → Q5
Q5. A_req,total = Σ Nk / qR;d,k as percentage of footprint:
    > ~50 %  → raft (Fundamentplatte) — §6.4
    ≤ ~50 %  → Q6
Q6. Do pads overlap, or does a column sit on the boundary line where a
    symmetric pad is impossible?
    YES → combined / strap footing, or track the wall under the column line.
    NO → isolated pad (Einzelfundament) → §6.3.
Q7. Any step in this tree lands on qR;d,k < ~100 kN/m² at 1.5 m depth with
    thick weak strata → piles (§7) or ground improvement (§12) —
    escalate to the geotechnical engineer.
```

### 6.3 Isolated pads & strip footings (Flachgründungen)

| Attribute | Preliminary values (reinforced concrete C25/30–C30/37, B500) |
|---|---|
| Pad plan size | 0.8 × 0.8 m → 2.5 × 2.5 m; side a = √(Nk/σB) rounded up, service loads |
| Pad depth | ≥ 0.30 m and governed by punching (§13.1) — usually 0.4–0.7 m for houses |
| Strip width b | b = vk (wall load per m, service) / σB; typically 0.6–1.2 m; wall centred or stepped to keep e ≤ b/6 |
| Projection rule (plain-concrete intuition) | projection ≤ ~h for plain (unreinforced) spread; reinforce where larger — plain-concrete footings additionally per DIN EN 1992-1-1/NA §10.3.6 and DIN 1054 §7.4.3 incl. base-joint reductions (VERIFY clause) |
| Blinding (Sauberkeitsplatte) | 5–10 cm C12/15 under every footing; cast the day the excavation reaches level |
| Cover below | cnom on blinding: cmin + Δcdev + 50 mm Verlegeüberdeckung (published example uses 20 + 15 + 50 = 85 mm) |
| Linking | tie all footings at plinth level (Grundzug / Ringanker logic; DIN EN 1992-1-1/NA §9.10 minimum tie force ≥ 70 kN per anchor line — digested; spacing ≤ 1.2 m from edge) — this converts independent footings into one settlement unit |

**Two load sets, never interchanged:** soil pressure checks run with characteristic/service combinations; concrete internal force design runs with factored combinations (γG 1.35 / γQ 1.50). Mixing them oversizes the soil check and under-designs the concrete — the most frequent residential calculation error.

### 6.4 Raft / slab foundation (Fundamentplatte)

| Trigger | Threshold |
|---|---|
| Required pad area > ~50 % of footprint | §6.2 Q5 |
| qR;d,k < ~100–120 kN/m² and building empfindlich | raft averages settlement |
| Erratic strata / old made ground not fully removable | raft bridges |
| Waterproof basement needed below table | raft + walls = tank §10 |
| High embedment | net-effect credit: excavated overburden γ·d reduces q_net |

Net pressure: q_net = N_total/A_platte − γ·d_excavated (the excavation credit is real: 20 kN/m³ × 2 m = 40 kPa on a basement — "Schwimmfundament" logic; but check HYD and GLS too, §11.1). Stiffness: a raft only averages settlement if it acts as a Scheibe — thickened edge beams / under-column upstand ribs supply it cheaply.

### 6.5 Strip footing micro-example

**Given:** load-bearing exterior wall (24 cm masonry + RC floor stack), vk = 120 kN/m characteristic; GM/SM ground, d = 1.0 m → σB tabular ≈ 250 kN/m² (dense enough, no water correction).

```
b_req = vk/σB = 120/250 = 0.48 m → add footing self-weight/backfill ~10 % and
wall-width margin → adopt b = 0.60 m, h = 0.30 m (projection each side
(600−240)/2 = 180 mm ≈ h → plain spread is borderline: REINFORCE)
Design: m_Ed = σd·c²/2 cantilever (σd factored per §3.2, c = projection);
As,min per DIN EN 1992-1-1 §7.3.2 (crack/Mcr rule, not a fixed %). Typical
house answer: bottom mat ∅12/20 both directions of the strip + ∅10/30
construction top mat, plus the plinth Ringanker tie (§6.3).
Check e ≤ b/6 under the wall's inevitable eccentricity (stepped/offset wall)
— centre the 240 wall on the 600 strip, or accept the small trapezoid (§13.5).
```

### 6.6 Stepped and sloped sites

On terrained plots, run strip footings in stepped levels tied by the plinth ring beam; keep each step ≤ ~0.6 m height against 2:1 (1V:2H) so the lower step's bearing wedge is never undercut by the upper excavation; never found a footing on the loose fill behind a retaining wall — anchor into the undisturbed wedge or design the wall first (§8).

---

## Section 7: Pile Foundations (Tiefengründungen, EA-Pfähle 2012)

### 7.1 When a house actually gets piles

Thick soft/organic layer beyond economical excavation; very high water table with deep weak strata; basements on artesian-prone ground (tie-down); stiff bearing stratum (gravel, marl, rock) at 4–15 m with heavy point loads; slope toe stabilisation (engineer-led); ground where settlement tolerance is razor-thin. Escalation rule: **any pile design is a geotechnical + structural engineer deliverable — this section is orientation, not a sizing shortcut.**

### 7.2 Pile types (German nomenclature, EA-Pfähle)

| Type | Displacement? | Typical house scale | Notes |
|---|---|---|---|
| Ram-pfahl (driven precast / steel HP) | displacement | 22–40 cm square precast; steel pipe piles | noise/vibration limits in town (DIN 4150 checks); driving resistance = direct capacity evidence |
| Ortpfahl / Bohrpfahl (bored cast-in-place) | replacement | Ø 30–60 cm with casing or bentonite/polymer support | cavings and artesian ground need casing; concrete placed by tremie pipe (Kontraktorverfahren) |
| Vollverdrängungspfahl (fully displacement, screw/displacement) | displacement | Ø 15–40 cm | low noise variants exist; heave risk in dense clay groups |
| Kleinbohrpfahl / Mikropfahl (micropile) | replacement (grouted) | Ø < 30 cm, τbr bond-limited | underpinning, anchors, restricted headroom; grout bond tables §7.4 |
| Träger (steel sections as mini-piles) | — | UP/HE sections | underpinning bay sequence (DIN 4123) |

### 7.3 Capacity design (static formula, preliminary)

```
Qc;k = Qb;k + Σ Qs,i;k = qB·Ab + Σ qs,i·Ai
Qu;d = Qc;k / γR;  (γR per §3.3 — by number of static load tests)
Ignore shaft friction in: fill, organic/soft upper layers, and any layer
that will settle more than the pile (negative skin, §7.5).
```

**Correctness note (resolved against Wendehorst Tab. 14.38/14.39/14.41):** the
previously digested qB/qs windows here had been sourced from the **driven
precast pile** table (Fertigrammpfähle), not the bored-pile table — the two
pile types carry genuinely different values and must not be conflated. Both
are now given separately, confirmed clean from source:

**Bored cast-in-place piles (Bohrpfahl), EA-Pfähle / Wendehorst Tab. 14.38–14.39** —
base resistance qb,k [MN/m²] by settlement ratio s/Deq:

| s/Deq | non-coh. qc=7.5 | qc=15 | qc=25 | cohesive cu=0.10 | cu=0.25 |
|---|---|---|---|---|---|
| 0.02·D | 0.55–0.80 | 1.05–1.40 | 1.75–2.30 | 0.35–0.45 | 0.95–1.2 |
| 0.03·D | 0.70–1.05 | 1.35–1.80 | 2.25–2.95 | 0.45–0.55 | 1.2–1.45 |
| 0.10·D (≈ ultimate, sg) | 1.60–2.30 | 3.0–4.0 | 4.0–5.30 | 0.8–1.0 | 1.6–2.0 |

Shaft resistance qs,k (Bruchwert, Mantelreibung): non-cohesive qc[MN/m²]→qs,k:
7.5→0.055–0.080; 15→0.105–0.140; ≥25→0.130–0.170. Cohesive cu[MN/m²]→qs,k:
0.060→0.030–0.040; 0.150→0.050–0.065; ≥0.250→0.065–0.085. Base-widened
(Fußverbreiterung) piles: reduce qb by 25 % (× 0.75). Minimum embedment into
the bond stratum: 2.5 m (soft rock qu ≤ 0.5 MN/m²) / 0.5 m (rock qu ≥ 5 MN/m²) /
5.0 m (tension piles). Rock-bearing piles use a separate table (Tab. 14.40),
qu[MN/m²]→(qb,k / qs,k): 0.5→(1.5/0.07); 5.0→(5.0/0.5); 20→(10.0/0.5),
linear-interpolate between.

**Driven precast piles (Fertigrammpfähle), Tab. 14.41** — separate, higher
values by settlement ratio s = 0.035·Deq / 0.1·Deq — this is the table the
figures below were originally (mis-)drawn from; use it only for actually
driven/pressed piles, never for bored: non-cohesive base qB,0 ~2.2–5.0 /
4.0–6.5 / 4.5–7.5 MN/m² for qc = 7.5/15/25 MN/m², shaft qs ~0.03–0.04 /
0.065–0.09 / 0.085–0.12 MN/m²; cohesive cu = 0.06/0.15/0.25 MN/m² → qs ~0.05–0.10.

Settlement-based design (Setzungssummenverfahren, γR;m = 1.40–1.50), and
static load tests remain the highest evidence class. Micropile grout–ground
bond τbr (digested): non-cohesive qc 7.5/15/25 → τbr ≈ 135–175 / 215–280 /
255–315 kN/m²; cohesive cu 60/150 → ≈ 55–65 / 95–105 kN/m² (VERIFY); required
embedment into bond stratum ≥ 2.5–5 m per tables.

### 7.4 Grouping, spacing, caps

Minimum centre-to-centre spacing per EA-Pfähle Bild 3 (values not reliably digested): the working anchors used here are **≥ 1.5–2 × shaft diameter for driven/displacement piles, larger (~2.5–3×) for bored friction piles in cohesive ground** (VERIFY exact grid). A pile cap (Fundamentkopf / cross-cap or a continuous Streifen under a wall line) ties piles into one unit and transfers the load including its own weight; cap concrete ≥ C25/30, embedment of pile head into cap ≥ ~10–15 cm plus reinforcement coupling (detailing is engineer work). Heave: driving displacement piles into soft clay lifts neighbouring pile positions — sequence from the centre outward and check uplift on already-cast piles (Reibungsminderung / Zuglast).

**Generic cross-check (non-DACH-specific, international handbook rule of thumb):** Neufert,
*Architects' Data* (Neufert_2002.pdf excerpt), p.54, gives simple minimum centre-to-centre pile
spacings independent of soil/EA-Pfähle load-transfer classification — useful only as a sanity
check on the EA-Pfähle-derived spacings above, never a substitute: bored piles (Bohrpfähle),
shaft spacing ≥ 3d (d = shaft diameter), widened-base spacing ≥ 2d_r (d_r = base/toe diameter),
absolute minimum ≥ 1.10 m; driven piles (Rammpfähle), spacing e ≥ 3d and ≥ (1 m + d), with
widened/driven-tube spacing ≥ 2d_r. These values explicitly do not apply to load-bearing
plugged or secant/tangent bored-pile walls (kontinuierliche Bohrpfahlwände), which are designed
to touch or overlap. Where this generic rule and the EA-Pfähle-derived §7.4 figures above
diverge, the EA-Pfähle/geotechnical-engineer figure governs for DACH design.

### 7.5 Negative skin friction & tensile loads

When surrounding ground settles more than the pile (thick fill, dewateration of compressibles, embankment), shaft friction reverses and **loads** the pile. Response: drive/anchor through the settling layer, reduce design qs near the top (EA-Pfähle Reibungsminderung logic — VERIFY the layer-reduction grid), and check the pile head and cap for the added downward drag plus any structural tension: **tension piles / anchors use γR;z 1.35 → 1.00 by test count (§3.3)**; bond length and coupling detail govern tension.

### 7.6 Preliminary pile quantity check (sanity method, NOT a design)

House column N_k = 600 kN; soft fines to 9 m, dense SE/SW gravel below; bored pile Ø 40 cm, toe at 11 m, shaft 2 m in gravel.

**Note: the base figure below still uses the original (driven-pile-sourced)
window — §7.3 now separates bored vs driven tables; re-run this sanity check
against the corrected **bored-pile** qb,k table (s/Deq = 0.03–0.10, qc≈20 →
interpolate between the qc=15 and qc=25 rows) before relying on the pile
count below.**

```
Base (qc ≈ 20 MN/m² gravel, windowed qB ~4.0–6.5 MN/m² §7.3 → take 5.0, /1.4
  conservative): Ab = 0.126 m² → Qb ≈ 630 kN (characteristic)
Shaft: ignore the upper 9 m of soft clay entirely (settle > pile → §7.5);
  2 m × qs ≈ 250 kN/m² × U 1.26 m ≈ 630 kN — cut to a cautious share,
  take ≤ 50 % of empirical qs for preliminary → ~300 kN
Qc;k ≈ 630 + 300 = 930 kN → Qc;d = 930/1.4 (γR;m, no tests) ≈ 660 kN ≥ 600 ✓
→ 2 piles per such column with margin, or verify with a dynamic/ static
load test and drop γR to 1.25/1.15 (fewer piles = the real EA-Pfähle payoff).
Check settlement of the pile GROUP (settlement-sum method), not only capacity —
friction-driven groups in clay settle; capacity checks alone miss it.
```

---

## Section 8: Earth Pressure & Retaining Structures (DIN 4085 / DIN 1054 / DIN 4084)

### 8.1 Coefficient logic (Rankine family, effective stress)

```
Active  : Ka = (1 − sin φ′)/(1 + sin φ′)        (vertical wall, horizontal backfill,
                                                 wall friction δ = 0 upper bound)
At-rest : K0 ≈ 1 − sin φ′                       (no yielding — cellars! see 8.3)
Passive : Kp (plane) = 1/Ka; curved-slip values (Caquot/Kérisel, digested):
          φ′ 10°  15°  20°  25°  30°  35°  40°  45°
          Kp  1.62 2.12 2.83 3.89 5.56 8.36 13.44 23.71   (δ = 0)
          Kp  1.59 2.05 2.71 3.68 5.17 7.59 11.74 19.66   (with wall friction δ)
(VERIFY column pairing — the two series are the δ-variants; with δ the true
design value is LOWER than passive-plane Rankine: use tables, not 1/Ka.)
Active thrust  Ea = ½·Ka·γ·H²  at H/3;  surcharge ΔEa = Ka·q·H at H/2
Water (undrained backfill!) Pw = ½·γw·Hw² — NOT reduced by Ka: water is what
doubles wall loads. Effective-stress method: σ′a = Ka·σ′v + water pressure.
```

### 8.2 Which earth-pressure case applies (DIN 4085 design-case selection — digested)

| Wall behaviour / support | Earth-pressure case |
|---|---|
| Unrestrained top (cantilever), anchored walls yielding (≥ required rotation), retained fill drains freely | **Active** Ea |
| Anchors stressed to ~100 % fixity, multi-strut excavations, walls cast into a structure, underpinning (Unterfangung) | **Increased active** EAGS (Mehrdruck branch) |
| Rigid restraint without yielding: rock anchors, cellar walls bearing on slab and ground, covered cut-and-cover, abutments | **At-rest** Eh (Erdruhedruck) |
| Newly backfilled and compacted against a stiff wall | **Compaction pressure Evd** — often exceeds Eh; triangular distribution per DIN 4085 Tafel 14.51, coefficient by wall stiffness (rigid/flexible) × backfill width b (VERIFY values) |
| Cohesive backfill near surface (computed σa tiny or negative) | **Mindesterddruck**: replace with a cohesionless "Ersatzboden" (c = 0) profile — the larger value governs |

Cohesion is **not** counted for at-rest pressure (digested rule). Wall friction: active side normally δ = φ′/2 (toothed/rough concrete); diaphragm walls (Schlitzwand, smooth) δ = φ′/3; for passive checks use δ′ = φ′/2 (sheet piles) reduced to φ′/3 (diaphragm walls). For γ-factor design run the chosen GS with φ′d = arctan(tan φ′/γφ′) and the corresponding Ea.

### 8.3 The cellar wall is NOT an active-pressure problem

A basement wall cast against a floor slab and base slab cannot move enough to mobilise active pressure (active requires ~H/1000–H/500 outward yielding; the excavation already happened). DIN 4085 / DIN 1054 answer: **increased active** — the published worked example uses the German practice of averaging with at-rest: e_a,erh = ½·(Ka + K0)·γ·z + ½·(Ka + K0)·q on the surcharge — with K0 = 0.5 for φ′ = 30° vs Ka = 0.333, a ~25 % load increase over active. Design the wall accordingly (worked example §13.2). Never carry over the free-standing-wall Ka into a cellar wall — that is the classic under-design.

### 8.4 Retaining wall proportioning & checks

**Generic wall-type typology (non-DACH-specific cross-reference):** Neufert, *Architects' Data*
(Neufert_2002.pdf excerpt), p.54, groups retaining structures rated for soil-pressure retention
into six built-practice types — useful for classifying which DIN 4085 earth-pressure case
(§8.2) applies before any proportioning arithmetic: (a) free-standing in-situ concrete or
sheet-pile wall, ground retained on one side only; (b) as (a) but rear-anchored; (c) in-situ
concrete or sheet-pile wall built into the structure (propped top and bottom — the cellar-wall
case of §8.3); (d) a concrete structure bearing against an independent retaining wall; (e) plain
gravity wall (mass alone resists overturning/sliding, no tension anywhere in the section); (f)
retaining wall with heel and toe (the cantilever L/T-shape proportioned below, using the
retained soil's own weight on the heel to help resist overturning). Types (a)/(e)/(f) are free
to yield and take **active** pressure (§8.2 top row); (b)/(c)/(d) are restrained and take
**increased-active or at-rest** pressure (§8.2 middle/lower rows) — matching the built type to
the earth-pressure case is the first design decision.

```
Cantilever (Stützwand) prelim: base width B ≈ (0.4–0.7)·H; stem base t ≈ B/10…B/12;
toe ≈ B/3; embedment in front of the toe ≥ 0.6 m (never trust preserved toe soil —
assume a future trench there).
Checks (GS-1): Gleitfestigkeit (sliding at base μd = tan δd; shear key or wider
heel if short), Kippsicherheit about the toe edge (Md,stb ≥ Md,dst with γ 0.9/1.1
EQU logic), Sohlpressung with e ≤ b/6, Grundbruch §4.4 under the base,
GLS deep-seated slip §8.7, Verformungen (wall yielding) for SLS.
The lesson is universal: overturning almost always passes; SLIDING and WATER
are what fail retaining walls.
```

Surcharge: maintenance strip / path ~5 kPa; driveway/car parking ≈ 10–20 kPa (≈ 0.6–1.2 m of soil — a car at 1 m behind the crest roughly doubles the local thrust); adjacent building — model the actual footing pressure at depth, not a blanket q.

### 8.5 Drainage — the single most important detail (per DIN 4095 + practice)

Behind the wall full height: **≥ 30 cm of free-draining F1 granular material (KF ≥ 10⁻⁴ m/s), wrapped in a non-woven geotextile filter**, a drainage pipe (DN 100) at the base laid ≥ 1:100 to daylight or a soakaway — never into a sealed pit; weep holes (Ausblüher/Auslässe) ~75–100 mm at 1.5–2.0 m centres in the lowest course (practice values — VERIFY). The impervious cap at the top (paving or compacted clay) sloped away ≥ 1:20 stops infiltration at source. Compacting backfill: light equipment within ~1 m of the stem — heavy compaction induces Evd above the design curve (§8.2) and has cracked new walls.

### 8.6 Anchors (Verpressanker, DIN EN 1997-1 / DIN EN 1537)

| Item | Rule (digested) |
|---|---|
| Design | GEO-2/STR; Rd = min(grout-ground bond, steel tie) / γR; steel tie checked additionally (As·fyk/γM) |
| Three verifications | (1) deep slip surface (Kranz method, EAU E 10: substitute wall at mid of anchor level) incl. GEO-3; (2) tie steel; (3) pull-out from suitability tests |
| Suitability test (Eignungsprüfung) | ≥ 3 anchors, supervised test institute; waivable only for temporary anchors where comparable ground was previously tested |
| Acceptance test (Abnahmeprüfung) | EVERY installed anchor (serviceability lock-off P_s, Festlegekraft P_f) |
| Geometry | inclination 15–30°; predimensioning charts by ground: limit pull-out load per metre in granular soils / limit skin friction in cohesive soils (per EAU/EA-HV annex — VERIFY chart) |
| Durability | temporary vs permanent per EN 1537; corrosion per DIN 50 929-3; ground chemistry per DIN 4030 checked before grout specification |
| Boundary crossing | anchors into neighbouring property need legal permission — raise early |

### 8.7 Slopes & ground breaks (Geländesprung, DIN 4084)

- Critical circle passes through the toe of a plain cut, or the *rear* toe behind a massive wall's base; anchor prestress can **reduce** GLS safety if its moment adds to the actions (only helps when the circle crosses the grout body).
- Slice methods (simplified Bishop per DIN 4084; Krey graphical for homogeneous soil; Janbu/Schultze charts for allowable slope height/inclination) and flow-net seepage (DIN 4084) are geotechnical-engineer tools — this skill provides the awareness and the trigger: **sloped sites, cuts > ~2 m, surcharged slopes, or any wall on soft ground → GLS check mandatory.**
- Fair-gradient rule of thumb for temporary cut faces in stable, non-saturated granular/stiff cohesive ground: ~1.5:1 (H:V) flat; saturated sand or soft clay — no stable stand-up; bench or support (§9).

---

## Section 9: Excavation, Shoring & Groundwater Control

### 9.1 Trench/ excavation safety per DIN 4124 (digested limits)

| Ground | Unsupported vertical face | Conditions |
|---|---|---|
| Non-cohesive & soft cohesive (locker/weich) | **≤ 1.25 m** | adjacent ground ≤ 1:10 slope; nothing loaded at the edge |
| At least stiff cohesive (steif), or rock | **≤ 1.75 m** | the section above 1.25 m benched back at β ≤ 45° from the base (baubetrieb digest rule) |
| Beyond those depths, saturated or loose ground, surcharge nearby, boundary within ~ footing depth | **Verbau (shoring) or batter** — slope excavation needs land + groundwater below formation; otherwise support |

Minimum clear distances from traffic loads to the trench edge / walings (DIN 4124 Tafel, digested, m):

| Support type | road vehicles (StVZO) | heavy vehicles | constr. machine ≤ 12 t | constr. machine 12–18 t |
|---|---|---|---|---|
| unsupported wall | 1.0 | 2.0 | 1.0 | 2.0 |
| horizontal standard shoring (Querverbau) | 0.6 | 1.0 | 0.6 | 1.0 |
| vertical standard shoring (Senkverbau) | 0.6 | 0.6 | 0.0 | 1.0 |

Spoil heaps, materials and concrete pumps belong outside those distances — a spoil surcharge on the lip is the classic collapse mechanism. Surrogate design loads for deep-pit analysis (EAB/EB logic, digested): unlimited-area traffic q = 10 kN/m² in the loaded zone; construction machines as strip loads when clearance < 1.5 m — 10 t machine: 50 kPa (no clearance) / 20 kPa at 0.6 m, b = 1.5 m; 30 t: 110/40 kPa, 2.0 m; 50 t: 140/50, 2.5 m; 70 t: 150/60, 3.0 m (VERIFY pairing). Excavation categories per VOB/C ATV DIN 18300 (loading classes + Homogenbereiche since 2016) govern the contract description: state group, state, moisture, boulder content per lift.

### 9.2 Verbau types — selection table (EAB + digested)

| System | Ground / water fit | Depth range | Notes |
|---|---|---|---|
| Ramverbau / Spundwand (sheet piles, Larssen/U profiles — section tables in source) | granular & cohesive, drivable; not boulders/rock | up to ~6–12 m (reusable within haul limits ~13 m) | fastest; **not watertight** (clutches); vibration to neighbours (DIN 4150) — press/vibe/pre-auger; immediately loadable |
| Trägerbohlwand (soldier pile + lagging: Berliner/Hamburger/Essener Verbau) | stands itself in most soils; watertight-NO; needs space to extract HAPs | to ~5–6 m typical (more with anchors) | H-sections at ~1.10 m grid; excavate 0.4–1.2 m lifts, thread timber/shotcrete lagging; braced or anchored |
| Bohrpfahlwand (bored pile wall: single / tangent / überschritten = secant / aufgelöst) | all soils incl. cavings with casing; secant = watertight cut-off | to ~15–20 m+ | rig space + spoil; secant needs fresh-cut-greens (Pilgerschritt) sequencing |
| Schlitzwand (diaphragm wall, bentonite-supported panels 2.5–10 m × 0.6–1.5 m) | all; permanent cut-off incl. base plug possible | deep urban pits, top-down (Deckel) | not extractable (lost form); tremie concrete; joint waterstops between panels |
| Bodennägel / Nagelwand (soil nails + facing) | stable granular or stiff cohesive; NO soft clay/peat, no erosion-prone sand with water | benches ≤ ~2.5 m lift | drilled, grouted bars; corrosion EN 1997-1 permanent-case rules |
| Verfüll-/Mischwand, Injektionswand, Gefrierwand (jet/grout mixing, injection, freezing) | special cases | specialist | contractor-designed, GK3-style scrutiny |
| Sloped excavation (Böschung) with benching | space available, ground stand-up OK | bench heights ~1–2 m | cheapest where land exists; keep GW below formation |

Static systems (digested): unrestrained cantilever or single-strut = statically determinate; multi-strut/anchored = indeterminate. Predimension embedment: full-fixity behaviour needs t ≈ 0.5·h_e; reactions mobilised at ~60 % of computed embedment; executed embedment = 1.2× computed for a fixed toe (EAB logic — VERIFY). Load figures: trapezoid reduction on stiff walls only when struts prestressed > 30 % (sheet piles) / > 60 % (soldier piles); at-rest pressure below the lowest strut constant when supported ≥ 2 levels. GK rule: **GK1 only for excavations ≤ 2.0 m** without water problems; bracing design is an engineer's deliverable with a verification list — GEO-2 (Grundbruch/rotation, sinking, material failure of struts/walings/ties, anchor pull-out, load transfer), GEO-3 (deep slip), HYD (seepage/boiling at the base), UPL (buoyancy of the pit / base slab).

### 9.3 DIN 4123 — excavations beside existing buildings

Unterfangung (underpinning) transfers existing footing loads to a deeper level; the excavation itself may act as surcharge (Ausschachtung) helping or hurting stability. Procedure (digested): max trench widths ~1–2 m bays (Stichgraben), **sequence high-load zones (crossing walls, corners) first**, force-fit with steel wedges / hydraulic jacks, cast the new footing simultaneously; interim states need no full proof **if execution conditions are kept**; final state → full EN 1997-1 proof set (overturning, sliding, bearing, slope, deep slip, material). Hairline cracks and settlements up to ~5 mm at neighbours are deemed "weitgehend unvermeidbar" — but the **Beweissicherung (pre-construction condition survey: dated photos of every crack with a scale in frame, on every adjacent building)** is the dispute-prevention measure that costs 30 minutes.

### 9.4 Wasserhaltung (construction dewatering, EAB)

Method selection by kf and drawdown need (digested logic): open sumps/ditches in coarse gravel (high kf, clean); **filter-lance wellpoints (Filterbrunnen)** in sands (kf ~10⁻⁵–10⁻³); deep wells below; vacuum-assisted as fines rise; cut-off wall + base grouting/plug (Injektionssohle) or jet-grout columns (Ø 0.8–2.8 m overlapped) when the pit penetrates an aquitard over a confined aquifer — **then the base plug is a UPL/HYD structural check, and tie-downs (Anker/Zugpfähle, GEO-2/STR) are real forces**. kf from pumping tests (Dupuit-type), infiltration tests (double-ring infiltrometer / borehole / casing, DIN 18130-2) or grain size (Beyer kf = C·(d10)², C chart). Inflow estimates (Davidenkoff open sump; incomplete wells: correct Q +10–30 %; ring-drain inflow past a wall with substitute radius r0 = √(A/π)). **Over-pumping settles neighbours** (consolidation of fines, and the classic "sand boiling + fines wash-out" pair): limit drawdown, filter well screens properly (sand-tight), monitor adjacent buildings. Discharge: test water quality; contaminated groundwater is a waste (LAWA/KWG handling — Z0–Z5 assignment-class logic for excavated material applies to water too).

### 9.5 Excavation and founding-stage site rules (what protects the calculation)

1. **Sohlprüfung (founding-plane acceptance):** the layer the report promised must be the layer the footing sits on — inspect, and if soft/loosed/undermined, extend depth or replace (§12.1) before any blinding.
2. **Same-day blinding (Sauberkeitsplatte 5–10 cm C12/15):** exposed clay loses strength to the next rain; exposed sand loses it to the next saturating shower. The blinding is the design's assumption of "undisturbed base".
3. **Keep water out of the pit floor before casting:** sump-and-pump, don't let the footing concrete sit in flowing water (wash-out of laitance → the base-joint reduction of DIN 1054 §7.4.3 becomes your problem, not a clause).
4. **Backfill the excavation as designed:** layer thickness + compaction class (§12.2) written on the drawing, or the settlement you calculated under the slab will happen beside it instead.
5. **Record as built:** Homogenbereiche actually hit, water encountered, probe results — the file that answers the neighbour's crack letter next year (§9.3).

---

## Section 10: Basement Water — Exposure Classes, Black Tub, White Tub

### 10.1 The three ground-moisture exposure states (design basis, digested from construction-physics logic)

| State (German) | English | What presses on the structure | Sealing consequence |
|---|---|---|---|
| Bodenfeuchte (nicht drückendes Wasser) | ground moisture, no hydrostatic pressure | capillary/film water only — permeable sand or fully draining backfill | bituminous thick-coat / welded sheet 1 layer + vertical cross-section seal (Querschnittsabdichtung, masonry only — impossible through RC walls: rebar) |
| Stauendes Sickerwasser / aufstauchendes Wasser | perched water, temporary ponding behind cohesive backfill | intermittent hydrostatic head, up to full water depth of the shaft if drainage absent | full waterproofing skin (black tub) or WU concrete (white tub); **never trust "it drains" in clay** |
| Drückendes Wasser (höchsten Grundwasserstand) | permanent hydrostatic pressure | design head = highest annual GW above the slab underside + perched | white tub (WU) or black tub engineered to the head; UPL/HYD checks §11.1 |

The modern waterproofing norms (successors of DIN 18195, now DIN 18532/18533/18535 series) codify these as Beanspruchungsklassen (W1–E / W2.1-E / W2.2-E / W3-E / W4-E for masonry/wall bases and floor slabs) — the class grid was **not** in the digested sources: **VERIFY against DIN 18533 before specifying layers**. The physical three-state logic above is the decision backbone and is digested.

### 10.2 Schwarze Wanne (tanked basement, bituminous/plastic sheet)

- Tanking skin between the structural wall and a smooth-cast protective backup wall (Wandrücklage); the sheeting is embedded/pressed, protecting it from point loads and from pressure change.
- Under-slab tanking bonded/lapped into the wall sheeting **above the footing level**; full-wrap continuity: blinding → protection → sheet → sliding layer → RC wall → backup.
- The repairability is zero after backfilling → double precautions, joint-by-joint inspection before Verfüllung.
- Bituminous vs synthetic: torch-on/tack-bitumen skins and PVC/PE/TPO/PF sheets — the choice is a contractor/manufacturer-system decision; the **design obligations are identical: continuity at penetrations, upstands ≥ 30 cm above the design water level, protection board before backfill, filter-protected drainage layer outside (§8.5/§10.5).**
- Capillary rise cut-off in masonry: horizontal Querschnittsabdichtung (in the bed joint at base level; impossible through RC — the waterstop replaces it, §10.3). Plinth/splash zone: continue the below-grade package 30–50 cm above finished ground.

### 10.3 Weiße Wanne (WU-Richtlinie 2017 edition, digested from the variant study)

Watertight **structural concrete itself** is the seal; tolerated residual wetting must dry inward. Design framework:

| Item | Rule (digested) |
|---|---|
| Beanspruchungsklassen (BKL) | non-pressing water (soil moisture / stauendes on a draining site) vs **pressing water (drückendes Wasser)** — the digest's numbering was inconsistent with the RL (published RL: 1 = nicht drückend, 2 = drückend); some sources invert — **check the edition used (VERIFY)**. Minimum-section/w/z consequences below are keyed to the physical exposure, not the label |
| NKL (Nutzungsklassen) | A = high-value/dry-use; B = subordinate rooms; C = temporarily usable — injection access required in all |
| EGS design principle | [a] crack-free by calculation (restraint-proof) — [b] limited cracks with planned sealing (self-healing conditions per Tafel 9.7: NKL-B + BKL-pressing + good groundwater chemistry + Δw ≤ 0.1·wk) — [c] defined cracks, sealed/injected > 0.2 (A) / 0.3 (B) mm |
| Min thickness / w/z | non-pressing: slab ≥ 150 mm, cast-in-place wall ≥ 200 mm, precast ≥ 240 mm, w/z ≤ 0.60; pressing: slab ≥ 250 (w/z 0.55) or 288 (0.60); wall ≥ 240 (0.55) / 276 (0.60); **practice with real head: walls ≥ 300 mm**. Concrete ≥ C25/30 (WU class; the real strength of a WU C25/30 design ≈ C30/37), 0/32 max, low-shrinkage, ≥ F3 consistency |
| Crack widths | erdseitig wk ≤ 0.3 mm (XC2 logic), luftseitig 0.4 mm (XC1); EGS[b]: per Tafel 9.7 (0.20/0.15 mm branch); early-age fct: 0.75·fctm (r < 0.5) / late max(fctm, 3.0); σs = √(6·wk·fct,eff·Es/∅l) |
| Restraint models | friction (slab on blinding, μ ~ 1.0 smooth layers) vs ground-spring (EB soil model) — friction governs thin slabs on stiff ground; wall restraint kct,d factor by L/H (1→0.35, 2→0.50, 3→0.60, 4→0.70, 6→0.85) (Tafel 9.17 logic — VERIFY pairing); cooling ΔT per wood-formwork tables (30/50 cm, season × hardening: 8–25 K — VERIFY) |
| Joints | Arbeitsfuge: waterstop strip (Dichtungsband) at every slab/wall joint — **mandatory because rebar continuity makes a cross-section seal impossible**; waterstop needed < 30 cm above the design water level even for roughened joints; injector hoses overlap waterstops ≥ 50 cm and always on the same side (never alternate); Sollriss fuges at ≤ 2–2.5 m pitch for [c]; movement-joint (Klemmfugenband) check for [a] by abP: δ = L/2·αt·ΔT + shrinkage (εcs ≈ 0.3–0.4 ‰ late; +10 kg/m³ water ≈ +0.1 mm/m) |
| Compression zone (pressing water, NKL-A) | x ≥ max(30; 1.5·∅g) from the cracked-section analysis (ξ = −αsρ + √(αs²ρ² + 2αsρ)) — or prove the load-crack wk |

Crystalline-integral admixtures and crystalline surface coatings: widely used *auxiliaries* (self-healing of fine cracks), **but not in the digested sources — a separate approval basis (abP/ETA); never a substitute for WU-Richtlinie crack/restraint design (VERIFY).**

### 10.4 Cellar detailing bundle (transferable, digested)

1. Base slab on blinding + (if pressing water) loose-laid membrane or full WU design; perimeter drain below slab level where BKL non-pressing with drainage.
2. Wall waterstop at the base cold joint; wall upstands for the tanking ≥ 30 cm above design GW.
3. Vertical waterproofing on the positive (earth) side, protected board before backfill; drainage mat + filter + perforated pipe DN100 ≥ 1:100 to the collecting shaft (Kiesfangschacht or separator to sewer — never into the rainwater soakaway uncontrolled).
4. Services through the tank: sealed sleeves (system-approved), planned before casting; no cast-in penetrations left to site improvisation.
5. Uplift and HYD checked against the **design** (highest annual) water level, not the drilling-day reading (§11.1).

### 10.5 Drainage per DIN 4095 (digested)

- Perimeter drainage (Dränung) required when: kf of the founding/backfill soil < 10⁻⁵ m/s and water can stand against the structure (stauend), or as protective drain for nicht-drückend exposures — Regelfall envelope (Tafel 14.65): level/slightly sloping ground, weakly permeable soil, depth ≤ 3 m, building ≤ 15 m, drain run high-point→outfall ≤ 60 m.
- Pipe invert ≥ 0.2 m **below the top of the foundation slab** but never loaded: the drain trench must not undercut footings (keep it outside the 1V:2H zone, §6.1).
- Control/flushing: inspection chambers DN 300 at ≤ 20 m and every direction change; collection/flush shafts DN 1000 at high/low points, ≤ 60 m.
- Discharge allowance (Abflussspende) to size drainage layers on decks/slabs: exposed wall face 0.30 l/(s·m²) class band; on decks 0.03; under slabs 0.005 l/(s·m²) (with perched-water escalation bands gering < 0.05 / mittel 0.05–0.10 / groß 0.10–0.30 — VERIFY pairing against DIN 4095 Tafel).
- Build-up outside-in: filter fleece (non-woven, silt-tight, opening width vs grain — verified by the manufacturer's o95 data) → drainage mat/nodule board → clean 16/32 or 8/16 washed drainage envelope around the perforated pipe; bedding above the crown hand-compacted (≥ 0.15 m over pipe crown before mechanical work — same rule as EN 1610 pipe trenches).
- Utility trench backfill (EN 1610, for the site drains and services around the house): bedding layer 1 ≥ 100 mm soil / 150 mm crushed rock over shaped trench, haunch fill compacted, pipe-zone material controlled, mechanical compaction only above ≥ 300 mm over crown; working space 0.50 m (≤ 2.5 m depth); trench width from pipe OD bands (0.80–1.00 m typical); **stability of the pipe trench per DIN 4124 (same Verbau rules) and no dewatering that washes fines from the pipe zone.**

---

## Section 11: Uplift, Hydraulic Heave, Frost & Swell

### 11.1 Basement / raft uplift checks (UPL & HYD)

```
UPL (Auftrieb, base-slab buoyancy — closed tank, drained or undrained):
   design water pressure ud = γw·hw (above slab soffit, at DESIGN level)
   Ed = 1.35·(U)  vs  Rd = 0.90·(permanent stabilising weight: slab +
   superstructure + soil above footings, plus favourable-only)
   → if Ed ≥ Rd: thicken slab / extend slab beyond the footprint (toe weight),
     tension piles or anchors (γR;z), or permanent drained construction
     (drainage + Wasserhaltung pumps = NOT a permanent stability system
     for a house — pumps fail).
HYD (hydraulischer Grundbruch / piping at the excavation or pit base):
   confined aquifer under a low-permeability plug:
   exit gradient at the plug base: i = Δh/L_flow (crude linear drop) vs
   critical ic ≈ (γsat−γw)/γw ≈ 0.5…1 (soil-dependent); if i → ic: boiling,
   sand boils at the pit base. Cut-off + base plug (jet/grout) + tie-down
   is the designed answer — full HYD verification per DIN 1054 §9.3 / EAU
   (γG 1.0/γH 1.0 factor set) is an engineer deliverable (VERIFY formulas).
```

Worked UPL case in §13.4. The water pressure never reduces by Ka-like effects; it is hydrostatic, acts normal to every surface, and persists — design it at the annual high.

### 11.2 Frost susceptibility (DIN 18300 / DIN 4019 companion table, digested Tafel 14.75)

| Class | Meaning | DIN 18196 groups |
|---|---|---|
| F1 | not frost susceptible | GW, GI, GE, SW, SI, SE |
| F2 | slight–medium frost susceptibility | TA; OT, OH, OK; STᵃ, GTᵃ; SUᵃ, GUᵃ |
| F3 | very frost susceptible | TL, TM; UL, UM, UA; OU; ST*, GT*, SU*, GU* |

ᵃ F2 → F1 when the < 0.063 mm fines content is ≤ 0.5 M-% at Cu ≥ 15.0, or
≤ 15 M-% at Cu ≤ 6.0, linear interpolation for 6.0 < Cu < 15.0 (confirmed
against Wendehorst Tafel 14.75 footnote, VERIFY tag dropped). Mechanics: frost heave needs (a) frost-susceptible fines, (b) water within reach (capillary rise from a table or perched water), (c) freezing. Remove one leg: found below the freeze depth, **or** replace with an F1 cap layer (≥ 40–60 cm, VERIFY regional rules), **or** cut capillary supply (drainage). Pavement engineering carries the same logic in Frostschutzschicht thicknesses (+5 / +15 cm by frost zone I/II/III — road case only, orientation).

### 11.3 Swell & shrinkage (quellende / schwindende Tone)

Expansive clays (the TA high-plasticity band, montmorillonitic) swell on wetting and shrink on drying; the active seasonal zone is locally ~1–3 m (VERIFY — quantify by free-swell/oedometer tests, not folklore). Strategy hierarchy: (1) found below the active zone on stable moisture ground; (2) remove-and-replace the active crust with F1 fill where shallow; (3) protect the ground moisture regime — impervious apron ≥ 1 m sloped away, no soakaways/septic leaching within several metres, consistent perimeter moisture; (4) stiff raft/grade-beam system to ride differential movement (small single-storey). **Never** place a shallow spread footing on F2/F3 or TA soil with an unmanaged water source. Shrinkage of the same soils under trees: keep large thirsty trees at ≥ ~1–1.5× mature height from the building line or deepen (universal physics; VERIFY against local arboricultural guidance).

---

## Section 12: Ground Improvement & Earthworks Values

### 12.1 Fix the soil instead of the foundation — decision rule

If the problem layer (fill, soft fines, frost-susceptible band, desiccation crust over muck) is **shallower than ~1.5–2 m and thinner than the excavation you are making anyway → remove and replace** with layered F1 material. If it is thick, deep, or below the water table → change the foundation (raft/piles), not the soil. (Orientation rule; confirm economics per project.)

| Technique | Fits | Effect / depth | Caveat |
|---|---|---|---|
| Over-excavate & replace (Auskoffern, Ersetzen, Verdichten in 30–40 cm lifts) | fill, F2/F3 near-surface, soft crusts | ≤ ~1.5–2 m; removes active/frost zone | compact to the §12.2 degrees; protect the fresh plane from rain |
| Mechanical compaction (plate, roller, tamper) | loose granular fill & backfill | ≤ ~0.6–1.0 m effective | cohesive soils need kneading/impact, not vibration |
| Load-bridging platform (geogrid/geotextile-reinforced F1 mattress over raft) | weak uniform ground, small differential | 0.5–1.0 m mattress | design by engineer |
| Stone/gravel columns, soil mixing, jet grout (Verfüllsäulen, Mischbohrverfahren, Düsenstrahl) | soft fines, liquefaction-adjacent, deep | 5–20 m | contractor-designed; GK2/3 territory — escalate |
| Preload/surcharging + drains | thick normally-consolidated clay | months | timescale rules out most houses |
| Drainage & capillary break (F1 Kapillarbruch layer + drains) | water-driven frost & softening | always possible | the cheapest damage-prevention layer in this file |

### 12.2 Compaction acceptance (ZTV E-StB logic, digested — transferable to building backfill practice)

Required degree of compaction (10 %-fractile of Proctor): **100 %** from Planum down to 1.0 m (embankments) / 0.5 m (cuts) for GW…GT/SU/ST; **98 %** from 1.0 m below Planum to the formation base (coarse) and **97 %** for fine-grained/mixed U,T soils up to base and in the top 0.5 m of cuts; rock: 97 % compaction degree, ≤ 12 Vol-% air voids (max quantile). Substitute criteria: static plate E_st (GW/GI: 100 MPa @100 %, 80 @98 %; SE/SW/SI/GE: 80 @100 %, 70 @98 %) and dynamic E_dyn (≈ 50/40 MPa; ratio E_dyn/E_st ≈ 2.3 @100 % / 2.5 @98 %). Planum acceptance: fine/mixed soils E_st ≥ 45 MPa (70 for qualified soil improvement). Test frequency: ≥ 1 test per started 1,000 m² per lift, minimum 2; structure backfill 1 per third lift per 200 m² (VERIFY pairing — OCR-scrambled). Methods M1 (test plan) / M2 (area-wide dynamic) / M3 (process-accompanied). Building-side practice transfers: every metre of basement backfill is a "Planum" for the next plot — specify the degree on the drawings or the contractor will pick the cheap one.

### 12.3 Volumes, swell and the DIN 18300 frame (VOB/C)

Earthworks are described in **Homogenbereiche** since 2016 (replacing Bodenkennziffer BK 1–7): per zone give DIN 18196 group, state, moisture, boulder/stone content, and environmental class (LAGA assignment values Z0 (unrestricted reuse) → Z1.1/Z1.2 (structural fill, hydrogeology-dependent) → Z2 (sealed) → Z3–Z5 (landfill)) — disposal cost explodes with the class; state it before pricing. Machine planning (excavator, DIN ISO 9245): useful output QA = Grundleistung × derates — swing (30°→1.12 … 180°→0.88), dig depth (BK3/4: 1 m→1.00 … 5 m→0.82), dump target (into truck ~0.69–0.83), task type (braced trench 2 m: 0.55 / 4 m: 0.44 — the Verbau tax), site/condition matrix (0.83→0.52); swell factor fS (loose/bank) 0.6–2.1 across classes (sandy ~1.5; cohesive ~1.7; rock breaks 2+ — grid ambiguous, VERIFY). Load-chain rule of thumb: truck/bucket volume ratio 3–5 economic; excavator is the Leitgerät — size truck count to its QA.

### 12.4 Disposal-capacity constraint (Deponiekapazität) — a live planning risk, not a footnote

[Digested from Kompendium Nachhaltige Bauwerke – Hochbauten, Springer 2026, Ch.13 — case-study level, **VERIFY current landfill-capacity status per Bundesland before quoting**.]

- In 5 of the 6 largest German Bundesländer (Bayern, NRW, Baden-Württemberg,
  Niedersachsen, Hessen, Sachsen), DK0/DK1 landfill capacity for non-hazardous
  excavated soil/rubble (the destination for anything above LAGA Z1.2/Z2 in §12.3)
  is forecast to run out by **2029** (Siekemeyer 2022/2025 simulation study) —
  budget rising haul distance and disposal cost into any project completing after
  that date, not only the ones starting now.
- Documented case (Hessen): average one-way haul distance 47 km; 13.9 Mt/year
  construction & demolition waste generates ≈550,000 truck trips (40 t GVW)/year,
  51.7M km/year, ≈215,000 t CO₂/year — roughly the annual CO₂ binding capacity of
  36,000 ha mixed forest (≈4 % of all Hessian forest). Use this order of magnitude
  to size the transport-emissions line of a large earthworks package, not just the
  tipping fee.
- Excavated soil (Bodenaushub, Abfallschlüssel 17.05) is ≈70–80 % of all C&D waste
  by mass and the least-recycled fraction — unlike rubble (Bauschutt), which
  already has established circular routes. This is where a project's disposal
  cost and carbon risk concentrate; keeping material Z0/Z1.1 by not co-mingling it
  with contaminated fill is a design/site-logistics decision, not an afterthought.
- Mitigation route worth flagging to the client: **ZFSV** (zeitweise fließfähige,
  selbstverdichtende Verfüllbaustoffe) — engineered flowable self-compacting
  backfill made from processed rubble/excavated soil + water + binder, validated
  via suitability testing → contaminant-immobilisation testing → mechanical
  testing → field trial before approval; replaces virgin fill in trench/void
  backfill and keeps material out of the landfill queue. Also: dynamic/deep
  compaction (fallweight, Rüttelstopfsäulen built from rubble/excavated soil)
  extends usable landfill volume in place instead of hauling it away — the same
  LAGA contamination-testing precondition applies either way.

### 12.5 FEM-based foundation optimisation & soil-model choice — precision notes

[Digested from the same source, Ch.13 — orientation for the modelling decision,
not a substitute for the Fachgeotechniker's calibration.]

- Combined pile-raft foundations (**KPP**, Kombinierte Pfahl-Plattengründung)
  sized by FEM optimisation of pile length/cross-section/position under the
  load-introduction points report **30–50 % foundation material savings** vs.
  conventional shallow/deep foundations, with lower and more even settlement and
  reduced raft bending — a genuine design lever, not only a sustainability claim.
  It is squarely **Geotechnische Kategorie GK3**: requires both a structural
  checking engineer AND an independent geotechnical (Fachgeotechniker) reviewer —
  never present a KPP result as a GK1/GK2-style deliverable. Named DACH
  precedents (i.e. an established, not experimental, method): Messeturm
  Frankfurt, Post Tower Bonn, ADAC-Zentrale München, Skyper/WestendDuo Frankfurt,
  BahnTower Berlin.
- Soil constitutive-model choice decides whether a material-optimised result like
  KPP is trustworthy at all: **Hardening-Soil-Small-Strain (HSS)** is the
  standard choice for stiffness-critical/settlement-governed optimisation (KPP
  among them) because it captures small-strain stiffness degradation that a
  simple Mohr–Coulomb model misses; **SANISAND**-family models belong to cyclic/
  offshore or seismic-repetition loading, not static building foundations — do
  not reach for SANISAND on a house or office raft.
- Calibration is not optional: the Nicoll Highway (Singapore, 2004) collapse is
  attributed in part to inadequately calibrated FEM soil parameters. Treat it as
  the standing counter-example whenever a design leans on FEM-optimised
  (material-minimised) geotechnical members — every material saving the
  optimisation extracts is exactly the safety margin that would otherwise have
  absorbed a calibration error.

---

## Section 13: Worked Examples

### 13.1 Isolated pad under a column (reinforced concrete, "German practice" framing)

**Given:** column 24/40 cm; N_Gk = 773.4 kN, N_Qk = 336.8 kN → N_Ed = 1.35·773.4 + 1.5·336.8 = 1549 kN. Tabular allowable σ_B = 300 kN/m² (dense gravelly ground, d ≈ 1.0 m — from a Baugrundbericht in the published case). Pad 2.40 × 2.40 m, h = 0.60 m, C25/30 (XC2/XA1 + WF), on 8 cm blinding; B500.

```
Bearing (hybrid framing per §4.5 — service column + factored footing weight):
  σ = 1549/5.76 = 269 kN/m²; with footing self-weight:
  σ_total = 269 + 1.35·(2.4²·0.60·25)/5.76 = 269 + 20 = 289 ≤ 300 ✓
Cover: cnom = cmin 20 + Δcdev 15 + Verlegeüberdeckung 50 = 85 mm → d ≈ 0.50 m
Bending: m_Ed = σ·c²/2 cantilever arm ≈ 0.174 MNm/m (published value;
  governing minimum m = 0.125·N_Ed = 19.4 kNm/m for punching-consistent design)
  → ω-method → As ≈ 21.4 cm²/m → provide 22∅12 = 24.86 cm² both directions,
  strip distribution over b/8 bands 7/10/14/19/19/14/10/7 % (DIN EN 1992 interior pads)
Punching: λ = a_λ/d = 1.08/0.50 = 2.16 ≥ 2 → control perimeter 1.0d (VERIFY
  perimeter-selection direction in current EC2/NA): u = 4·0.24 + 2π·0.50 = 4.10 m;
  A_crit = 1.323 m²; V_Ed,red = 1549 − 269·1.323·10³/10³ = 1193 kN;
  v_Ed = 1.10·1193/(4.10·0.50) = 0.64 MN/m²; v_Rd,c = 0.558 < vmin-branch = 0.729
  → vmin governs: 0.64 ≤ 0.729 ✓ — NO punching reinforcement (tight; re-run with
  executed dimensions).
SLS (wk = 0.3): N_perm = 773.4 + 0.6·336.8 = 975.5 kN → σ_s,perm = 235.6 N/mm²
  → ∅s* = 18 mm > ∅12 ✓.
```

Sanity anchors: a two-storey house column on dense sand at 300 kN/m² rarely needs more than ~1.6 m pad — 2.4 m signals heavy loads, a low table value, or a mis-added load sum. Re-check before trusting the calc.

### 13.2 Water-bearing cellar wall — WU, increased active pressure (digested example)

**Given:** wall height 3.14 m, pin-supported top (cellar ceiling) and base (raft); backfill sand φ′ = 30°, γ = 20, c = 0, surface β = 10°; surcharge q = 5 kPa; h = 24 cm C30/37 (WU min ≥ C25/30; practice with pressure ≥ 30 cm).

```
Earth pressure case (no yield!): increased active, DIN 4085 German practice
  e_a = ½·(Ka + K0)·γ·z     with Ka = 0.333, K0 = 1−sinφ′ = 0.5
  z = 0.11 → 0.92 ; z = 3.25 m → 27.07 kN/m²
  surcharge: e_q = ½·(Ka + K0)·q = 2.08 kN/m² (constant with depth)
ULS:  p_top = 1.35·0.92 + 1.5·2.08 = 4.36 ; p_bot = 1.35·27.07 + 3.12 = 39.66 kN/m²
Two-way panel (l = 7.0 m → one-way vertical governs the 3.14 m span):
  v_Ed,A = 43.79 ; m_Ed ≈ 27.6 kNm/m at x = 0.564·l → ω → a_s = 3.43 cm²/m
  → R524 (5.24 cm²/m) ✓; shear: v_Ed 43.79 ≤ v_Rd,c = 76.9 ✓ no links
WU detailing: waterstop band (Dichtungsband) at the base Arbeitsfuge — required
because rebar continuity forbids a cross-section seal; erdseitig wk ≤ 0.3 mm;
injection access for all cracks > 0.2/0.3 mm (NKL A/B); waterstop ≥ 30 cm
below the design water line's ceiling.
If the same wall were designed on the free-standing active assumption:
e_a = Ka·γ·z = 0.333·20·3.25 = 21.6 kN/m² at depth vs 27.1 for the
½(Ka+K0) average — the increased case multiplies both soil and surcharge
terms by ½(1+K0/Ka) ≈ 1.25 (design trap §8.3).
```

### 13.3 Cantilever retaining wall, 2.5 m backfill (illustration of the GS-1 mechanics — computed for this skill, not a published table)

**Given:** stem 2.50 m above base + base 0.45 m; trial base b = 1.70 m (toe 0.35, stem 0.30, heel 1.05); free-draining compacted granular backfill SE/SW φ′ = 30°, γ = 18, c′ = 0, level; drained weeps (§8.5); front embedment 0.45 m. GS-1: φ′d = arctan(tan30°/1.25) = 24.8°, δd ≈ 12.4° → Ka ≈ 0.41; γE = 1.35 on the earth action.

```
Ea,d = ½·0.41·(1.35·18)·2.95² ≈ 43 kN/m  at 0.98 m above base soffit
Verticals at γG;inf = 1.0: stem 18.75, base 19.1, soil on heel 47.3 → V = 85.1 kN
Sliding: μd = tan12.4° = 0.22 → F = 18.7; passive in 0.45 m front soil
  Ep,d = ½·Kpd(5.2)·1.35·18·0.45² /1.35 ≈ 7.1 → RH ≈ 25.8 < 43 ✗ FAILS
→ widen heel to 1.70 (b = 2.35) AND shear key 0.60 m below base under stem:
   V = 121.7 → F = 26.7; key passive (1.05 m) net ≈ (46.8·0.9/1.35 − 3.2) ≈ 28
   RH ≈ 62 ≥ 43 ✓
Overturning: MR = 155.2 vs MO = 43·0.98 ≈ 42 → ✓ (ratio ≈ 3.7 — typical: OT passes)
Eccentricity: e = b/2 − (MR−MO)/V = 1.175 − 0.93 = 0.24 ≤ b/6 = 0.39 ✓
   σmax = (V/b)(1 + 6e/b) = 83.8 kPa; σmin = 19.8 > 0 ✓
   83.8 ≪ qR;d,k ≈ 500 (tabular, dense sand, b≈2.35 — table interp, VERIFY) ✓
Lesson restated: sliding governed the design; the drainage layer is what keeps
Ea at Ka·(γd) instead of the water-inclusive doubling; never count on the 0.45 m
toe passive alone — a future path trench erases it (assume it excavated).
```

### 13.4 Basement slab uplift (UPL, GS per §3.1)

**Given:** raft 0.30 m RC (γ 25) covering the footprint; design GW 1.80 m above slab soffit.

```
ud = γw·hw = 10·1.8 = 18 kPa
Ed = 1.35·18 = 24.3 kPa
Rd = 0.90·(0.30·25 + 2 permanent finishes) = 0.90·9.5 = 8.6 kPa
24.3 > 8.6 ✗ → the slab floats unless: permanent weight ≥ 24.3/0.9 = 27 kPa
(i.e. ~1.08 m concrete — absurd → architecture answer: extend the slab so
perimeter soil weight loads it, use a waffle/edge thickening with soil above),
tension anchors/piles (γR;z §3.3), or a permanently drained construction with
pumps + backup — pumps are NOT a permanent stability system (§11.1).
Also re-check the same state at HYD during construction (excavation dewatering
running before the slab is cast → the buoyancy force moves to the pit base).
```

### 13.5 Eccentric pad — klaffende Fuge (digested statics example)

**Given:** footing 1.5 × 2.5 m; (a) N = 800 kN, M = 120 kNm → e = 0.15 ≤ 2.5/6 = 0.417: σ_max = (N/A)(1 + 6e/b) = 213.3·1.36 = 290 kN/m² (full base). (b) N = 500 kN, M = 250 kNm → e = 0.50 > 0.417 → gap opens: σ_max = 2N / (3·(b/2 − e)·a) = 1000/(3·0.75·1.5) = 296 kN/m². **Beyond the kernel the pressure concentrates and the footing rotates (Verkantung) — DIN 4017 §4.4 effective-width logic is the matching capacity model.** Re-proportion rather than accept: widen b, add counter-eccentric load, or move the column.

---

## Section 14: Typical Damages & Deliverable Checklist

### 14.1 Catalogue of recurring geotechnical failures (what this skill exists to prevent)

| Damage | Mechanism / prevention |
|---|---|
| Heaved cellar floors and cracked slab in winter | F2/F3 soil + water + freezing → found below frost or F1 cap (§11.2) |
| Bearing failure or large settlement on tabular value | table used without checking state (Dr/IC) and water; the −40 % water rule skipped (§4.3) |
| Double-factored design (oversized, "safe") | γ applied on top of a factored table value (§3.4) |
| Water-stained / flooded basement | active-pressure wall design reused as cellar wall (§8.3); missing waterstop at cold joint (§10.3); no drainage package (§10.5) |
| Retaining wall tilted or slid out | sliding check skipped (§13.3); passive toe counted then excavated later; saturated backfill doubling the thrust (no drain) |
| New cellar wall cracked against fresh backfill | compaction pressure Evd > Eh — light compaction within 1 m, stage the fill (§8.2, §8.5) |
| Neighbour cracked after your dig | DIN 4123 breach: bay width/sequence ignored, over-dewatering (§9.3, §9.4) |
| Sand boiling at pit base, plug blow-out | HYD ignored — confined aquifer under cut-off: base plug + tie-down as designed system (§9.4) |
| Basement "floating" after first wet winter | UPL never run (§11.1) |
| Pile losing capacity under settling fill | negative skin friction not deducted (§7.5) |
| Rising damp through cellar wall | Querschnittsabdichtung missing/bridged (masonry base seal; in RC the waterstop replaces it) (§10.2) |
| Plaster spalling with salt | sulphate attack — DIN 4030 chemistry not tested (§1.4), wrong cement class (§14.2) |
| Differential cracks at wing junctions | two foundation types / two storey-loads on one clay (§5.3, §6.2) |
| "Good" crust over muck, late settlement | crust trap: settlement computed on the wrong layer (§5.3) |
| Backfill under terrace sinks a metre over years | uncontrolled lift thickness; no compaction class specified (§12.2) |

### 14.2 Chemistry note (transferable exposure classes, digested from concrete chapter)

DIN EN 206 / DIN 1045-2 XA attack by soil/groundwater (worst value governs; two values in the upper quarter → next class): sulphate mg/l (water): 200–600 / 600–3000 / 3000–6000 → XA1/2/3; soil mg/kg: 2000–3000 / 3000–12000 / 12000–24000; pH: 6.5–5.5 / 5.5–4.5 / 4.5–4.0; aggressive CO₂: 15–40 / 40–100 / >100 mg/l; NH₄: 15–30 / 30–60 / 60–100; Mg: 300–1000 / 1000–3000 / >3000; Baumann-Gully test value 200 → XA1. Composition limits (DIN 1045-2): XA1 w/cc ≤ ~0.55 / C25-30 / zc 280; XA2 ≤ 0.50 / C35-45 + SR cement (air-entrained per "f" flags — VERIFY grid); XA3 ≤ 0.45 / C35-45. Exposure drives cement choice (SR cements above XA1: CEM I-SR3, CEM III/B-SR, III/C-SR) and cover — demand the test (§1.4).

### 14.3 Before issuing any foundation output — checklist

- [ ] Baugrundbericht referenced by name/date, or explicit "no investigation — all values presumptive" statement
- [ ] GK classified; if GK3 indicators present → stopped and escalated
- [ ] Soil design values (φ′/c′/cu, γ, kf) stated with source and the γ-factor set used (GS-1 or GS-2/GEO-3 named)
- [ ] Sohlwiderstand value with table/figure reference, water correction applied, adjustments (+50 %/−40 %/width) stated
- [ ] Design groundwater level (highest annual, incl. Stauwasser) stated and used for UPL/HYD and waterproofing class
- [ ] Frost assessment (F-class of founding soil, frost depth assumption)
- [ ] Settlement check + sensitivity class declared (empfindlich vs unempfindlich)
- [ ] Service loads used for bearing/table check; factored for concrete — declared separately
- [ ] Earth-pressure case per wall type (active / increased active / at-rest / compaction) named in the calc
- [ ] Drainage detail present wherever water can stand (wall, slab, plinth)
- [ ] Waterproofing class + system (black/white tub, BKL/EGS) decided against the design water level
- [ ] Adjacent structures: DIN 4123 / DIN 4124 conditions and Beweissicherung noted
- [ ] All deliverables labelled "Vorentwurf — nicht zur Ausführung — requires Tragwerksplaner sign-off and Baugenehmigung"

---

## Section 15: FreeCAD / IFC Modelling Notes

Pairs with the `construction-freecad-bim` skill. Model the foundation as real BIM objects so quantities and sections come out correct.

| Physical element | FreeCAD / IFC mapping |
|---|---|
| Einzelfundament (pad), Streifenfundament (strip) | `Arch Structure`, IfcType **IfcFooting** ( Pad_Footing / Strip_Footing ) |
| Fundamentplatte (raft/base slab) | IfcSlab PredefinedType BASESLAB, or IfcFooting ( MAT_FOOTING ) |
| Pfahl (pile) | IfcPile; Pfahlkopf (cap): IfcFooting PILE_CAP |
| Stützwand (retaining wall) | IfcWall + separate IfcFooting base slab |
| Kelleraußenwand (WU) / Sohlplatte | IfcWall PLUMBINGWALL? — no: IfcWall ( basement wall ) with property set carrying BKL/EGS/crack class |
| Sauberkeitsplatte (blinding), F1 cap, drainage | IfcBuildingElementProxy + distinct material ( Magerbeton, Kies-F1, Dränmatte ) |
| Aushub/Verfüllung (excavation/backfill volumes) | `Arch Site` terrain + Subtraction so cut/fill are real quantities |

**Structuring rules:**
1. A **`Fundation` BuildingStorey with negative elevation** (`Placement.Base.z = -1200`) holds all footings/piles/blinding — never dump them into the ground floor.
2. Drive top-of-footing vs founding level from parameters `Df` (Gründungstiefe) and `t`: `z_top = −(Df − t)`, `z_base = −Df`.
3. A Spreadsheet per footing mark holds `Nk`, `qR;d,k`, `Df`, `fcd`; bind the Arch Structure length/width/height to the cells so a changed table value resizes the plan.
4. Use parametric **Subtractions** for drain penetrations and sleeve voids — never frozen booleans.
5. On sloped sites: model terrain first, step footings ≤ 1V:2H max-step line, lap the Ringanker (ties).
6. Real materials: `Beton-C25-30`, `Beton-C30-37-WU`, `Magerbeton-C12-15`, `Stahl-B500B`, `Kies-F1-0-63`, `Draenmaterial-16-32` — quantities depend on it.
7. Add a property/`Description` on every foundation object: **"Vorentwurf — nicht zur Ausführung"** until a signed design exists.

```python
import FreeCAD as App, Arch, Draft
doc = App.ActiveDocument
def pad(name, L, W, T, x, y, Df):
    """mm. founding level = -Df ; top = -(Df - T)."""
    base = Draft.makeRectangle(L, W, placement=App.Placement(
        App.Vector(x - L/2, y - W/2, -Df), App.Rotation()))
    s = Arch.makeStructure(base, height=T)
    s.Label = name
    s.IfcType = "Footing"
    return s

F1 = pad("F1_1800x1800x400", 1800, 1800, 400, 0, 0, 1200)
doc.recompute()
```

---

## Section 16: Standards Index, Handoff, Known Gaps

### 16.1 Standards to cite (cite explicitly in outputs; dated editions — VERIFY current)

| Standard | Scope as used here |
|---|---|
| **DIN 1054:2010-12 (+A1/A2)** / **DIN EN 1997-1/NA** | Geotechnical design: safety concept (BS-P/T/A/E; GS-1/GS-2/GEO-3), tabellarischer Sohlwiderstand (Tab. 1–6), founding depths, ground investigation duties (GK) |
| **DIN EN 1997-2/NA** | Ground investigation & testing execution |
| **DIN 4017 (03.06)** | Grundbruch (bearing capacity), incl. Kany influence grids |
| **DIN 4019 (05.15)** | Setzungsberechnung (settlement, layered sum, Verkantung) |
| **DIN 4020 (12.10)** | Erkundungsumfang, Aufschluss depths, sample categories/quality |
| **DIN 4084 (01.09)** | Geländesprünge (slope/terrain-break stability, slice methods) |
| **DIN 4085 (08.17)** | Erddruck (active / increased active / at-rest / compaction, cases & Mindesterddruck) |
| **DIN 18196:2011-05** / **DIN EN ISO 14688** | Soil classification (groups, suffixes, index properties) |
| **DIN 18130/-134/-135/-125/-126/-128/-129, EN ISO 17892 series** | Test suite: kf, plate, oedometer, density, state, organics, limits |
| **EA-Pfähle (2012 rev.)** | Pile design: γR tables, qc methods (Langen/Siemens), grouping, tests |
| **EAB / EAU / GDA** | Excavation support systems (Verbau, anchors, base plugs, Wasserhaltung) |
| **DIN 4124** | Trench & pit faces: unsupported-depth limits, traffic distances |
| **DIN 4123** | Excavations adjacent to buildings, Unterfangung (underpinning) |
| **DIN 4095** | Dränung (site/perimeter drainage design) |
| **DIN EN 1610** | Utility trenches & pipe bedding/backfill |
| **WU-Richtlinie (DAfStb 2017)** | Weiße Wanne: BKL/NKL, EGS [a][b][c], min dimensions, w/z, joints |
| **DIN EN 206 / DIN 1045-2 + DIN 4030** | Concrete durability & chemical attack exposure |
| **DIN EN 1537** | permanent ground anchors durability |
| **DIN 18300 (VOB/C ATV) + LAGA M20 / ErsatzbaustoffV** | Earthwork contract description: Homogenbereiche, swell, disposal classes |
| **ZTV E-StB / DIN 18134** | Compaction degrees and plate-test acceptance |
| **DIN 1055 / EN 1990/1991 (ψ, γG/γQ)** | Load factors feeding the combinations |
| **Terzaghi/Köster/Kany lineage** | The theoretical backbone of DIN 4017/4019 (keep formula-and-table families matched) |

### 16.2 Handoff to the Tragwerksplaner / Fachgeotechniker

| Deliverable | Content |
|---|---|
| Site & plot | coordinates, survey spot levels, existing structures + approximate founding depths, boundary/access constraints, drilling-rig access |
| Ground data | the Baugrundbericht in full (logs, probes, tests, water, chemistry) — or a written statement that none exists |
| Superstructure model | system, grid, storey heights, column/wall loads characteristic **and** factored, basement/wall schedule |
| Foundation proposal | type, Df, sizes, qR;d used + source + adjustment rules, sensitivity class, settlement estimate, governing check per element |
| Water & earth | design GW incl. perched; waterproofing class + system; Verbau assumption with depth + surcharges; slopes/walls with earth-pressure case named |
| Problem register | frost class, organics/fill, swell risk, contamination (Homogenbereich + LAGA class), GK declaration |
| Model/drawings | FreeCAD/IFC + layout + footing schedule + wall sections + drainage & waterproofing details |
| Explicit ask | "Review, amend, sign the geotechnical design assumptions; confirm founding recommendation." |

**Put these to the ground engineer in writing:** permitted qR;d at proposed Df and its source table/figure; design shear parameters (c′/φ′, cu) and kf classes; highest annual GW + Stauwasser risk; frost-depth and F-class treatment; chemistry (DIN 4030) and resulting exposure class; earth-pressure parameters and δ for each wall case; pile type/load-test programme and γR class; GLS check depth; permitted surcharge near excavations; GK classification.

### 16.3 Known gaps of this skill (state when relevant)

1. **Corrupted table cells** — the DIN 1054 Sohlwiderstand grid, DIN 4017 factor rows and several DIN 4020 depth clauses carry VERIFY flags; never publish them as quotable values without the standard text.
2. **No GLS slope-stability computation method** is provided (Bishop/limit-equilibrium software is the engineer's tool) — triggers only.
3. **No HYD/piping closed-form checks** (gradient formulas garbled) — §11.1 gives the framework and escalation.
4. **No liquefaction assessment** — a specialist topic (EN 1998 + site response); for seismically relevant sites escalate.
5. **No full Verbau design calculations** (EAB load figures, strut sizing) — selection logic and verification list only.
6. **No pile test design/regulation detail** (EA-Pfähle testing programme) — orientation.
7. **DIN 18533/18532 exposure-class grids not digested** — the three-state moisture logic (§10.1) is given instead.
8. **Dated editions (2010–2017 book set)** — several factor tables and NA clauses changed in later prints; VERIFY per project.
9. **No cost data** — excavation/Verbau/dewatering quantities come from the model; rates belong to the estimating workflow.

**Related skills:** `structural-systems` / `structural-analysis` (loads feeding these footings) · `concrete-detailing` (footing/wall reinforcement) · `masonry-construction` (cellar walls, Querschnittsabdichtung) · `roofing-waterproofing` / `building-physics-thermal-moisture` (plinth and drainage continuity) · `construction-freecad-bim` (modelling) · `construction-cost-management-din276` (earthworks quantities) · `building-regulations-permits` (Baugenehmigung, Prüfstatik).

---

**Final reminder, restated because it is the most important line in this file:** every number above is a design aid for planning and FreeCAD modelling. A real building needs a site-specific Baugrunderkundung (DIN 4020), a geotechnical design signed by a competent engineer (Fachgeotechniker for GK3), a Prüfstatik-capable Tragwerksplaner, and a Baugenehmigung — before the first cubic metre of soil moves.



