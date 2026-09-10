---
name: building-acoustics
description: >
  Sound protection design for DACH/European construction: Schallschutz per DIN 4109
  (airborne R'w, D_nT,w; impact L'n,w, L'nT,w), C/Ctr spectrum adaptation, level
  arithmetic (10/20·lg rules, energy summing), point/line distance laws, mass law
  (30,9·lg m'-22,2 family), double-leaf walls (28+18·lg reduced-mass rule), resonance
  frequency f0 design and spring quality s', front shells (Vorsatzschalen) with
  delta-R_w(f0), floating screeds (164-35·lg m' bare slab, delta-L_w = f(m',s')),
  flanking paths and junction attenuation K_ij (DIN 4109-32), party-wall and floor
  design catalogues (masonry, drywall, timber beam/board decks, light roofs),
  requirements tables DIN 4109-1/-5, VDI 4100 comfort grading (SSt I-II-III),
  DEGA 103 certificate classes, room acoustics per DIN 18041 (T_soll formulas,
  Sabine A = 0,163·V/T, absorption catalogues, echo/transit-time criteria),
  outdoor noise immission (TA Lärm, 16. BImSchV, DIN 18005, L_DEN indices),
  facade/window insulation mixtures (R'w,ges), equipment/plant noise (TGA, lifts,
  heat pumps), and full worked verification examples reproducing the DIN 4109-33
  flanking computation. Use when rating walls/floors/windows, checking a build-up
  against a required value, sizing absorbers, or drafting acoustic notes.
---

# Building Acoustics (Schallschutz + Raumakustik)

Agent-neutral construction-design skill. English working language, German normative
terms in parentheses. Metric units only. Applies to DACH practice; other countries
must re-map norm references.

## 0. How to use this skill

- You are **drafting, checking or explaining** acoustic design in a building project:
  ratings of walls/floors/windows, requirement selection, flanking verification,
  room-acoustics sizing, outdoor noise assessment.
- Read §1 (reality check) and §2 (evidence tiers) before quoting any number.
- Every table/formula below carries a tier tag: **[T2]** normative, **[T3]** digested
  catalogue excerpt, **[T4]** rule of thumb. Values flagged **VERIFY** were ambiguous
  in the source material — confirm against the current norm before putting them in
  a deliverable.
- Cross-referenced sibling skills in this library (defer detail to them):
  `building-physics-thermal-moisture` (Glaser/U-values of the same build-ups),
  `construction-detailing` (junction execution: screed bands, separations, seals),
  `structural-systems`, `concrete-detailing`, `masonry-construction`,
  `timber-steel-design` (load-bearing context for wall/floor catalogues),
  `openings-windows-doors` (window/door product ratings, mounting),
  `building-services-tga` (plant rooms, ducts, pipe decoupling),
  `building-regulations-permits` (Bauvorlage, immission approvals, LBO/MBO context).

## 1. Reality check — what this skill is and is not

1. **This is a planning and verification aid, not the deliverable.** The formal
   sound-insulation proof (*Schallschutznachweis*) is an Engineer/Architekt
   deliverable, signed per state building-authority rules (Prüfingenieur für
   Schallschutz in several Länder for certain classes). Output of this skill must
   be re-stated in the project's own documentation with norm editions cited.
2. **Norm editions move.** DIN 4109-1/-2:2018, DIN 4109-3x catalogue parts (2016),
   DIN 4109-5:2020, VDI 4100:2012 (earlier edition withdrawn), DEGA 103:2018,
   DIN 18041:2016 — all flagged *verify current issue* in the source material.
   Never assume an edition year from this file is still on the bookshelf.
3. **Beiblatt/catalogue status.** DIN 4109-31…-36 are calculation-data parts
   (Rahmen, massiv, Holz/Leichtbau/Trockenbau, Vorsatzschalen, Fenster/Türen,
   gebäudetechnische Anlagen). Catalogue values are *design values*, not test
   certificates; for products outside the catalogues you need Prüfzeugnis or
   measured data (DIN 4109-4).
4. **Site measurement cannot be replaced by calculation.** Computed R'w is a
   prediction for a stated room geometry; the acceptance question in disputes is
   answered by in-situ measurement per DIN 4109-4 / ISO 16283, which the
   calculation neither guarantees nor forbids failing.
5. **Minimum is not comfortable.** Building to DIN 4109-1 alone satisfies public
   law; neighbours' complaints in the "normal comfort" band are then a
   civil-law risk of the builder if the contract implied more (see §2).
6. **Geometry-specific results.** A flanking computation is valid only for the
   room dimensions it was run with (S_s, joint lengths, V) — re-run per room type.

## 2. Evidentiary tiers

| Tier | Status | Content | Consequence of use |
|---|---|---|---|
| **T1** | Legal anchor | LBO/MBO requirement that buildings be arranged/erected so sound from foreseeable nuisances does not cause "unzumutbare Belästigungen"; this makes the **allgemein anerkannten Regeln der Technik** binding — for building acoustics that core is DIN 4109 | Public-law minimum; deviation downward = non-approvable; owner/buyer can additionally demand higher standard (contract) — building only DIN 4109-1 while market/contract expectation is VDI 4100 SSt II is a known civil-law exposure |
| **T2** | Normative texts | DIN 4109-1 (requirements), -2 (simplified calculation), -3 (catalogue data), -4 (measurement); DIN 4109-5 (abgestufter/erhöhter Schallschutz); VDI 4100 (Nachhall-/Komfort-Level SSt I/II/III, private law); DIN 18041 (room acoustics); TA Lärm, 16. BImSchV, 18. BImSchV, DIN 18005, DIN EN ISO 9613-2, DIN ISO 717-1/-2 | Quote with edition; values here are excerpts |
| **T3** | Digested catalogue excerpts | Representative rows of the DIN 4109-32/-33/-34/-35 tables, requirement excerpts, absorption catalogues, junction formulas | Usable for design iteration; final proof re-derived from the norm |
| **T4** | Rules of thumb | Mass-law shortcuts, thickness→dB ladders, "decouple the screed" heuristics | Pre-design only, ±3…5 dB; label as estimate in any written output |

Perception anchors used throughout (T2, ISO/DIN framing):
±1 dB barely perceptible, ±3 dB clearly perceptible, **10 dB ≈ double/half loudness**.
For services noise the digest notes +5 dB(A) ≈ perceived doubling below ~40 dB(A).

## 3. Metrics, spectra and level arithmetic

### 3.1 Hearing bands and quantities [T2]

- Hearing 16 Hz–20 kHz; **building acoustics evaluation band 100–3150 Hz**
  (third-octaves), room acoustics 63–8000 Hz; speech up to ~8 kHz.
- Third-octave mid-frequencies: 100, 125, 160, 200, 250, 315, 400, 500, 630,
  800, 1000, 1250, 1600, 2000, 2500, 3150 Hz (building-acoustics set).
- λ = c/f; c = 344 m/s (air 20 °C) → λ(1 kHz) = 0.34 m.
- L_p = 20·lg(p/p₀) dB, p₀ = 20 µPa (0 dB hearing threshold; ~120 dB pain).
- L_W = 10·lg(W/W₀) dB, W₀ = 1 pW. L_p = L_W at r = 0.28 m (full-sphere source).
- Transmission degree τ = transmitted/incident intensity (10⁻¹…10⁻⁸);
  R = 10·lg(1/τ).

### 3.2 Room-related descriptors (DIN 4109 / ISO 717 / ISO 16283) [T2]

| Symbol | Name | Definition | Notes |
|---|---|---|---|
| D | Pegeldifferenz | D = L₁ − L₂ | depends on receiving room |
| D_n | normalized level difference | D_n = D + 10·lg(A/A₀) | A₀ = 10 m² (25 m² for teaching rooms) |
| D_nT | standardized level difference | D_nT = D + 10·lg(T/T₀) | T₀ = 0.5 s; ISO 16283-1; T₀ ↔ A ≈ 0.32·V |
| R_w | weighted sound reduction index | lab, direct path only | single number, ISO 717-1 |
| **R'w** | **Bauschalldämm-Maß (apparent)** | in-situ, **includes flanking** | prime = field quantity |
| L'_n | normalized impact level | L_n = L + 10·lg(A/A₀) | tapping machine ISO 16283-2 |
| L'_nT | standardized impact level | L'_nT = L_i + 10·lg(T/T₀) | T₀ = 0.5 s |
| L_n,eq,0,w | equivalent normalized impact, bare slab | direct path, no topping | mass-law entry (§7) |
| ΔL_w | impact improvement of a floor build-up | ΔL_w = L'_n0 − L'_n1 | floating screed/covering credit |
| K_ij | Stoßstellendämm-Maß (junction attenuation) | structure-borne transmission quality at a joint | higher = better (§8) |
| C, C_tr | spectrum adaptation values | subtract from R_w for real spectra | §3.3 |
| C_I | impact spectrum adaptation | reported L'_n,w + C_I | §7.5 |

Naming convention (T2): R = calculated, P = lab (Prüfstand), B = built;
X'w forms with prime are in-situ/flanking-inclusive. VDI 4100 works in
D_nT,w / L'_nT,w (room-based); DIN 4109 in R'w / L'n,w (component-based);
conversions in §9 — keep them apart in tables or auditors will reject the mix.

### 3.3 Spectrum adaptation C / C_tr [T2]

- **C** (spectrum 1 — residential/announcement-like: speech, music, radio/TV,
  children playing; also high-speed rail, motorway > 80 km/h, jets near,
  mid/high-frequency industry).
- **C_tr** (spectrum 2 — traffic-like: city traffic, low-speed rail, aircraft
  distant, disco; low/mid-frequency industry).
- Weighted results: A_w,1 = X_w + C; A_w,2 = X_w + C_tr.
- Reporting style: `R'w(C; C_tr) = 53(−1; −4) dB` — single number alone hides
  low-frequency weakness; for traffic noise check **Ctr**, for mixed residential
  use **C** (Tafel guidance: Ctr for city traffic, C for dwelling pink noise).
- Typical digested values: homogeneous masonry single leaves C = −1.6,
  C_tr = −4.6 dB; timber floors C_I positive, bare RC negative (−15 ≤ C_I ≤ 0).

### 3.4 ISO 717-1 reference curve (airborne rating) [T2]

Shift the reference curve in 1 dB steps toward the measured/calculated curve
until Σ deficiencies over the 16 thirds ≤ 32 dB; R_w = curve value at 500 Hz.
Reference curve (thirds 100→3150 Hz):

| f | 100 | 125 | 160 | 200 | 250 | 315 | 400 | 500 | 630 | 800 | 1k | 1250 | 1600 | 2000 | 2500 | 3150 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| R | 33 | 36 | 39 | 42 | 45 | 48 | 51 | 52 | 53 | 54 | 55 | 56 | 56 | 56 | 56 | 56 |

Octave shortcuts (125/250/500/1k/2k): 36/45/52/55/56. Worked shift example
(§13 F6): data −9 shift → R'w = 52 − 9 = 43 dB with ΣU = 25 ≤ 32.

### 3.5 A-weighting (excerpt) [T2]

A-corrections, dB, by third: 100 −19.1 · 125 −16.1 · 160 −13.3 · 200 −10.9 ·
250 −8.6 · 315 −6.6 · 400 −4.8 · 500 −3.2 · 630 −1.9 · 800 −0.8 · 1000 0 ·
1250 +0.6 · 1600 +1.0 · 2000 +1.2 · 2500 +1.3 · 3150 +1.2.
Modern instruments: A and C networks only.

### 3.6 Level arithmetic [T2]

- Addition (incoherent sources): L_tot = 10·lg Σⱼ 10^(0.1·Lⱼ).
- n equal sources: L_tot = L + 10·lg n (2× → +3 dB, 4× → +6 dB, 10× → +10 dB).
- Subtraction: L_x = 10·lg(10^(0.1·L_tot) − 10^(0.1·L_rest)).
- Leq over T: energy average; Leq = 10·lg[(1/T)∫10^(0.1L(t))dt].
- Worked: 54+58+50+49 → 60.0 dB (S1); 7 cars @ 84 → 84+10lg7 = 92.7 ≈ 92;
  + plane 100 → 10lg(10^9.27 + 10^10) = 101 dB(A) (S2); from a total of 84 dB(A)
  removing a 77 dB(A) residual: L₅ = 10lg(10^8.4 − 10^8.3) = 77 dB(A) (S3).
- Rule: subtracting a source ≥10 dB quieter than the sum changes nothing audibly;
  −1 dB on a 94.6 dB orchestra means killing 12 of 25 blowers (S5).

### 3.7 Distance laws [T2]

- Point source, free field: ΔL = 20·lg(r₂/r₁); L_p = L_W − 11 − 20·lg r (m).
  Reflecting planes: 1 plane −8, 2 planes −5, 3 planes −2 (instead of −11).
- Line source: ΔL = 10·lg(r₂/r₁) — doubling distance −3 dB only.
  Free cylinder: L_p = L_W − 8 − 10·lg r; over ground (semi-cyl): −5 constant.
- Worked (S4): machine L_W = 101 dB(A), mixed-area day limit 60 dB(A), hemispherical
  radiation: r = 10^((101−8−60)/20) = 44.7 m → place ≥ 45 m; at 20 m the
  admissible L_W,max = 60 + 8 + 20·lg 20 = 94 dB(A).

## 4. Mass law — single-leaf elements

### 4.1 Theory [T2/T4]

Theoretical mass law (ideal plate, zero bending stiffness):
R(f) = 10·lg[1 + (2π·f·m′/(2·ρ·c))²];
→ **+6 dB per octave and +6 dB per mass doubling**; dips at grazing incidence
and at the coincidence (Koinzidenz) limit frequency f_g, where the acoustic
trace wavelength matches the bending wavelength.
- f_g < 100 Hz → treat as "sufficiently stiff" (biegesteif);
- f_g > 1500–2000 Hz → "sufficiently flexible" (biegeweich) — flat mass-law run;
- f_g inside 200–2000 Hz → coincidence dip is design-relevant (gypsum board,
  CLT, thin stone: check catalogue or measure).
- Old-form shortcut (non-normative, still circulating): R_w ≈ 20·lg(m′·f) − 47.5
  at f = 500 Hz (T4, VERIFY against current data parts before use).

### 4.2 Normative one-leaf design formulas (DIN 4109-32) [T3]

For quasi-homogeneous masonry (conditions §4.3), surface mass m′ = d·ρ_eff
(kg/m²), weighted direct rating R_w from lg m′:

| Material family | Formula (63…720/480 kg/m² validity) |
|---|---|
| Concrete / KS / Vollziegel / filled blocks | R_w = 30,9·lg(m′) − 22,2 (65–720 kg/m²) |
| Lightweight concrete masonry (LB) | R_w = 30,9·lg(m′) − 20,2 (140–480 kg/m²) |
| AAC (Porenbeton) m′ < 150 | R_w = 32,6·lg(m′) − 22,5 |
| AAC (Porenbeton) m′ ≥ 150 | R_w = 26,1·lg(m′) − 8,4 |

Ladder (normal-mortar family | LB family | AAC, dB at listed m′):

| m′ kg/m² | 50 | 70 | 100 | 140 | 160 | 200 | 240 | 280 | 300 | 400 | 500 | 600 | 700 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| R_w (normal) | — | 35 | 40 | 44 | 46 | 49 | 51 | 53 | 54 | 58 | 61 | 64 | 66 |
| R_w (LB) | — | 38 | 43 | 47 | 49 | 52 | 54 | 55 | 56 | — | — | — | — |
| R_w (AAC) | 33 | — | — | — | — | — | — | — | — | — | — | — | — |

(VERIFY column mapping; anchors: 100→40/43, 200→49/52, 500→61.)
C = −1.6, C_tr = −4.6 dB (single-leaf homogeneous). Same mass laws for single-leaf
**ceilings** (R_w of slab = wall formula with total mass incl. bonded layers).
Worked-example anchors: m′ = 432.8→59,3 · 442→59,5 · 466→60,2 · 528→61,9 ·
336.4→55,9 · 197→48,7 · 169.5→46,7.

### 4.3 Masonry density and mass build-up [T3]

- Stone density classes RDK 0,5…2,6 (steps ≈0,1 → 100 kg/m³; 0,5 = 410–500 …
  2,6 = 2410–2600 kg/m³).
- Wall gross density ρ (kg/m³): normal mortar **ρ = 900·RDK + 100** (RDK 0,35–2,2);
  light mortar ρ = 900·RDK + 50 (≤1,0); thin-bed mortar ρ = 1000·RDK − 100
  (>1,0), or 1000·RDK − 50 / −25 for class widths ≤1,0; up-turned hollow blocks
  sand-filled ρ = 1000·(RDK + 0,4); filled blocks ρ = ρ_stone·V_ribs + ρ_fill·V_fill.
- Plaster: gypsum/thin-bed 1000 · lime/lime-cement 1600 · light 900 ·
  insulating 250 kg/m³ → add ρ·d per layer.
- Concrete: plain normal-weight 2350, reinforced 2400 kg/m³; LB design ρ −12,5 %;
  hollow-core slab m′ −15 %; topping concrete 2100; cement screed 2000;
  mastic asphalt 2300.
- Quasi-homogeneous validity (else general test/approval needed): Hochlochbrick
  ≤240 any RDK, >240 only RDK ≥1,0; LB hollow/blocks ≤240 & RDK ≥0,8;
  perforated concrete ≤240 & ≥0,8; KS holes ≤50 %, round, not staggered slits.

Practical thickness ladder (MG IIa stone ρ 1600, T4): 55 mm → 37 dB ·
115 mm → 47 dB · 240 mm → 53 dB. Workable anchors: 24 cm KS RDK 1,8 ≈ 410 kg/m²
→ dwelling separating wall R'w 53; 30 cm RDK 2,0 ≈ 580 kg/m² → 57 dB (party
wall EFH/row); stairwall R'w 52 → 24 cm class 1,6 unplastered or 17.5 cm
plastered class 2,0/2,2.

### 4.4 Decoupled (elastically separated) single leaf [T3]

R_w,KE = R_w − K_E when the separating element ends on decoupled edges
(valid only if it does **not** bear against the flanking elements):
- m′ ≤ 150 kg/m²: K_E = 2 dB (2–3 edges) / 4 dB (all four);
- m′ > 150 kg/m²: K_E = 3 dB / 6 dB.
Example S38: 11 cm KS RDK 1,6 (m′ 197) → R_w 48.7, both vertical edges elastic
→ 45.7 dB — "3 dB is audible"; weigh decoupling against flanking gain case by case.

### 4.5 Solid timber / CLT (Massivholz) [T3/T4]

- Not covered by the DIN 4109 mass catalogue → proof by measurement (4109-4) for
  the formal Nachweis; pre-design estimate R_w ≈ 25 + 7·lg(m′) dB (rigidly bonded
  gypsum board counted into m′). **VERIFY**: one worked example evaluates a
  250-Hz variant giving 48.8 dB at m′ = 170; treat ±3 dB.
- Junction factors for CLT follow EN ISO 12354-1 (mass-ratio type, f_K = 500 Hz),
  not the masonry K_ij polynomial set.

## 5. Double-leaf walls and front shells (Vorsatzschalen)

### 5.1 Two-mass oscillator behaviour [T2]

Leaf 1 + spring (cavity/interlayer) + leaf 2:
- f < f₀: shells couple rigidly → only total mass acts, **no benefit**;
- f = f₀: resonance → strong **deterioration** (can be worse than single leaf);
- f > f₀: +6 dB/oct improvement.
Design target: **f₀ ≤ 100 Hz** (below the evaluation band floor). Consequences:
no rigid ties (wall ties, dowels, mortar spalls, continuous screed, boxes),
absorbent infill (≥70 % porous, flow resistivity r 5–50 kPa·s/m²),
one leaf biegeweich if the other is flanked continuously.

Resonance frequency (digested forms, equivalent):
- Air gap: **f₀ = 60·√( (1/m′₁ + 1/m′₂) / d )** [Hz] with d in m;
- General spring: **f₀ = 160·√( s′ · (1/m′₁ + 1/m′₂) )** with s′ = E_dyn/d [MN/m³];
- Front shell before heavy wall (m′₂ ≫ m′₁): f₀ = 160·√(s′/m′₁).
- Dynamic stiffness of an unfilled air layer: E_dyn = ρ_air·c² ≈ 0,142 MN/m²,
  so s′ = 0,142/d [MN/m³].

Sizing examples (full chains §14 B3):
- S19: 2×12.5 GKF (m′ 10), 4 cm gap → f₀ = 134 Hz (bad); gap ≥ 7.2 cm or
  double boards (m′ 20) → f₀ ≈ 95…100 Hz.
- S42: KS wall 352.5 + 2×GK (20), E_dyn 0,3 MN/m² → gap ≥ 50 mm for f₀ ≤ 100.
- S21: lining before wall 389.8, E_dyn 0,18, 6 cm gap → board ≥ 11.4 → 12.5 mm.

### 5.2 Spring quality s′ (and E_dyn) [T2/T3]

- s′ [MN/m³] = dynamic stiffness per unit area of the layer between masses;
  lower s′ = softer spring = lower f₀. E_dyn [MN/m²] of the material, s′=E_dyn/d.
- Typical anchors (digest): resilient gypsum linings s′ ≈ 2…10; EPS render layer
  far stiffer (f₀ ≈ 360 Hz, §5.4); TSD under floating screed s′ = 5…50;
  edge strips s′ ≤ 150 MN/m³ (cork/PE heavy foam; bitumen board ≤ 750).
- Multi-layer springs: **s′_tot = 1 / Σ(1/s′ᵢ)** (series softening).

### 5.3 Two-leaf masonry party wall (Gebäude-/Haustrennwand) [T3]

R_w,2s = **28 + 18·lg( m′₁·m′₂ / (m′₁ + m′₂) ) + ΔR_w,Tr − K**   [VERIFY: one
digest print shows 18·lg((m′₁m′₂)/2) — the reduced-mass form above is the one
that reproduces the worked values; confirm against DIN 4109-2/-32 text].
Conditions: joint ≥ 30 mm (≥ 50 mm if mineral-wool boards laid in, WTT/WTH per
DIN 4108-10); dense, staggered full-bed masonry; leaves m′ 100–150 need ≥ 50 mm;
≥ 150 → 30 mm OK.

ΔR_w,Tr surcharge by separation quality (both leaves ≤ 200; AAC leaves ≤ 250 LB):

| Case | ΔR_w,Tr (joint ≥30, unfilled) |
|---|---|
| 1 leaves fully separated, walls + floors independent above base slab | +12 |
| 2 walls continuous ≥ 575 kg/m² flank, floor with separation joint | +9 |
| 3 white-tank continuous basement: wall + floor continuous | +3 |
| 4 walls separated, foundations separated | +9 |
| 5 walls separated, floor separated on common foundation | +6 |
| 6 walls separated, floor continuous ≥ 575 kg/m² | +6 |

Footnotes: aerated-concrete leaves ≤200 kg/m²: cases 1–4 +3, 5–6 +6 (→15/12/6/12/…);
LB leaves ≤250 & stone ρ ≤ 800: +2 (→14/11/5/11/8/8); joint ≥50 mm filled with
mineral wool: general +14 (rows: 14/11/3/11/6…) and AAC 17/14/6/14/12(+2 rule);
example: 2×17.5 cm AAC RDK ≥0,6 + 50 mm WTH fill → **total +14**.
Joint K from flanking grid: K = 0 while m′f,m ≤ m′Tr,1, rising to ≈4,4 dB at
m′Tr 100 vs m′f,m 500 (table, T3): rows m′Tr 100/150/200/250/300/400/500 vs
m′f,m 100→500 give 0,6/1,6/2,3/2,8/3,2/3,9/4,4 at m′f,m=100… — use analytic
approximation K ≈ 0,6·lg(m′f,m/m′Tr,1) + 0,6 when m′f,m > m′Tr,1 [VERIFY], else 0.
m′f,m = mean of flanking masses (Σm′f,i/n), excluding fronts with f₀ < 125 Hz.

Design checks (§14 B3): to reach erf R'w = 67 (DIN 4109-5 row-house party):
reduced mass m′₁m′₂/(m′₁+m′₂) ≥ 165.8 → equal leaves m′ ≥ 331.5 kg/m²
(e.g. 17.5 cm KS RDK 1,2+putz) with ≥30 mm continuous joint, no mortar bridges,
soft MW fill. Two 24 cm RDK 1,4 leaves + putz (m′ 321,5) → R'w ≈ 67 ✓ (DEGA A).
Porenbeton 2×121 → 62.7: passes 4109-1 (59) and 4109-5 (62), fails VDI 4100 SSt II (63).
WU-tank shared basement (case 3): erf 64 → KS RDK 1,4 (m′ 248,9 each) → 66.5 ✓;
LB stone ρ 800 (m′ 141) → 61.6 ✗.
Top-floor continuation only counts if the roof is acoustically split (D_n,f,w proof).

### 5.4 Front shells and ETICS in front of massive walls (DIN 4109-34) [T3]

Improvement/penalty ΔR_w by f₀ of the shell (both flanks and direct path
corrected per (5.4.2-5): one side ΔR_(D,d); both sides (ΔR_D + ΔR_d + 2)/2):

| f₀ [Hz] | 30–160 | 200 | 250 | 315 | 400 | 500 | 630–1600 | 1600–5000 |
|---|---|---|---|---|---|---|---|---|
| ΔR_w | formula gain (see below) | −1 | −3 | −5 | −7 | −9 | −10 | −5 |

- 30 ≤ f₀ ≤ 160 Hz: positive gain per 4109-34 table; engineering approximation
  ΔR_w = 74,4 − 20·lg f₀ − 0,5·R_w (T4; reproduces 14.8 dB at f₀ = 60 Hz on a
  48.8 dB leaf — §14 B5).
- **WDVS/ETICS**: R_w = R_w,0 + ΔR_w,WDVS with ΔR = ΔR_S − K_D(plugs) − K_K(glue %)
  − K_S(render carrier) − K_TW(base level); cap −8…+19, **default −6** when not
  computed. f₀ = 160·√(s′/m′₁plaster). Real-world span (T4): −10…+20 dB.
  Design: thick mineral render on MW board (m′ ≈ 25, s′ ≈ 10 → f₀ ≈ 100 Hz) =
  gain; thin organic render on EPS (f₀ ≈ 360 Hz) = loss. Plugs touching render
  cost K_D ≈ 0,34·ΔR_S^0,4 per row — minimize.
- Board data: GF gypsum-fibre 1100 kg/m³/12,5 → m′ 13,75 · GK 680/12,5 → 8,5 ·
  GKF fire-clay board 800/12,5 → 10 · HW wood 600/16 → 9,6 kg/m².
- Rigid multi-leaf (at least one stiff leaf — e.g. brick outer skin, sandwich):
  R_w = 30,9·lg m′tot − C with C: two-leaf masonry w/ air or MW 17,2 · concrete
  sandwich/foam core 24,2 · single leaf + rear-ventilated cladding 22,2 (m′ inner
  only); LB: −15,2/−22,2/−20,2; AAC: <150 → 17,5/24,5/22,5; ≥150 → 13,4/10,4/8,4.
  Party wall butting onto inner leaf with m′ > 50 % of inner leaf → +3 dB.

### 5.5 Lightweight double-stud walls (DIN 18183/4109-33 catalogue) [T3]

CW stud walls, 12,5 GK boards, 40 mm MW unless noted (R_w, dB):

| Build-up | R_w |
|---|---|
| CW75/50, 1×GK both sides, 40 MW | 41 |
| CW75 @60 mm studs, 1×GK | 42 |
| CW100, 1×GK, 40/60/80 MW | 43 / 44 / 45 |
| CW75, 2×GK, 40/60 MW | 48 / 51 |
| CW100, 2×GK, 40/60/80 MW | 49 / 51 / 52 |
| double studs CW50, gap 105 (5 mm elastic), 2×40 MW | 60 |
| double studs CW100, gap 205, 80 MW | 61 |

Timber-frame inner walls (4109-33 Tab 3, R'w): 40/60 studs GK → 38; 120/60-140
GK → 41, GF → 44; 40/60-60/40 double GK → 43, GF+GF10 → 47; 140/60 GK+HW → 54;
separate top plate GF10+GF12,5 → 66; spring-rail 40/80-80/105 GK+SP13 → 58.
Rules (§5.1): maximize shell spacing, stud axes ≥ 600 mm, loose soft fill
(not fully bonded), different shell masses/seal all joints, elastic perimeter;
lining continuity hierarchy across the separating element: continuous boards
(worst) < jointed lining < cut-out decoupled (best).

## 6. Impact sound (Trittschall)

### 6.1 Quantities and excitation [T2]

- Excitation: standard tapping machine (Normhammerwerk; lab ISO 10140-3 without
  prime mover, in-situ ISO 16283-2). Levels: L_i averaged over ≥ 4 positions;
  L'_n = L_i + 10·lg(A/A₀), L'_nT = L_i + 10·lg(T/T₀), T₀ = 0,5 s.
- Total including flanks: L'_n = 10lg(10^0.1·L_n,d + Σ10^0.1·L_n,f,ij) (over/under
  rooms); adjacent rooms sum flanks only.
- Rated: L'_n,w from ISO 717-2 — shift reference curve **upward** in 1 dB steps,
  Σ exceedances ≤ 32, value at 500 Hz. Reference thirds (100→3150):
  62/62/62/62/62/62/61/60/59/58/57/54/51/48/45/42. Octaves 125/250/500/1k/2k:
  67/67/65/62/49. Worked: +4 shift → L'_n,w = 60+4 = 64 (ΣU = 28.6).
- **C_I**: massive well-covered decks ≈ 0; timber beams positive; bare RC negative,
  −15 ≤ C_I ≤ 0 (evaluated from L_n,sum over 50–2500; extended C_I,50–2500 possible).
  Always report L'n,w(C_I).

### 6.2 Bare slab: mass-law source level [T3]

**L_n,eq,0,w = 164 − 35·lg(m′)** for 100 ≤ m′ ≤ 720 kg/m² (hollow-core −15 % mass;
valid 100–900 in the flank-correlation clause). Anchors: 387,5 → 73.4 ·
442 → 71.4 · 510 → 69.2 · 528 → 68.7 · 538 → 68.4 · 600 → 66.1.
Heavier, stiffer slab = quieter impact source; note opposite slope vs airborne.

### 6.3 Floating screed design (schwimmender Estrich) [T3]

ΔL_w (cement / Ca-sulfate / anhydrite-flow / magnesia / resin screed,
60 < m′ < 160 kg/m², 6 < s′ < 50 MN/m³):
**ΔL_w = 13·lg(m′) − 14,2·lg(s′) + 20,8**
Prefabricated dry screed (15–40; 15–40): ΔL_w = (−0,21·m′ − 5,45)·lg(s′) + 0,46·m′ + 23,8.
Mastic asphalt (Gussasphalt, EN 18560-2, 58–87; 15–50): same prefabricated form.

Table (m′ = 80 kg/m²; cement-type | GA/dry prefabricated) by dynamic stiffness s′:

| s′ MN/m³ | 50 | 40 | 30 | 20 | 10 |
|---|---|---|---|---|---|
| cement screed ΔL_w | 21,4 | 22,8 | 24,6 | 27,1 | 31,3 |
| GA / prefabricated | 22,8 | 25,0 | 27,7 | 31,7 | 38,4 |

Sizing logic (worked, §14 B4/S62): required ΔL_w = L_n,eq,0,w − (zul. L'_n,w − 3 dB
margin) + K_flank → choose screed mass and TSD so the curve clears it
(e.g. 442 slab, zul 47, K 1,5 → ΔL_w ≥ 25,9 → 80 kg/m² + s′ ≤ 25 → ΔL_w ≈ 26 ✓;
inverse check: ΔL_w = 30 at m′ 69 → s′ ≤ 19,1 → E_dyn 0,6 → d ≤ 31 mm →
build ≥ 35 mm TSD).
- Multi-layer underlays: s′_tot = 1/Σ(1/s′ᵢ).
- Floating screed helps mid/high frequencies; low-f remains flank-dominated.

### 6.4 Acoustic bridges — the make-or-break details [T2/T3]

Bridges that destroy the computed ΔL_w: rigid screed–slab links (no edge strip or
edge strip compressed/absent), slab unevenness point contacts, **pipes buried in
the screed**, skirting/board fixings drilled into hard floor, screed running under
partitions, door thresholds and carpet edges bridging the separation, retro-cut
screed bands (worse than full-depth joints built from the start — flanking
D_n,f,w 40 dB cement / 46 mastic standard floating vs **57 dB with a joint running
through the whole build-up**).
Soft floor coverings (linoleum composite 14, PVC jute 13, cork 16, textile
needle-felt 20, pile carpet foamed 19/24/28 dB for 4/6/8 mm — minimum values) are
**not creditable in the new-build proof** (replaceable); on a floating screed only
the larger single ΔL may be counted.

### 6.5 Impact flanking corrections [T3]

L'_n,w = L_n,eq,0,w − ΔL_w + K (massive) or L'_n,w = L_n,w + K₁ + K₂ (light decks).
- K (no suspended ceiling): K = 0 for m′f,m ≤ m′s; else ≈ 0,6·(5,5 − 10·lg(m′f,m/m′s))
  as printed (5.4.7-4) — **VERIFY**, worked values read as ≈ 9·lg(m′s/m′f,m):
  442 vs mean flank 300 → K ≈ 1,5; with a decoupled suspended ceiling (ΔR ≥ 10 dB):
  K = 5,3 − 10,2·lg(m′f,m/m′s) — a 12 dB ceiling can drive K negative (S29:
  K = −2,8, i.e. 4,7 dB better).
- Room-layout K_T (stacking of source vs receiver): directly below **0**;
  beside/diagonal-below **+5** (rigid walls m′ ≥ 150); via intermediate room **+10**;
  vertically through load-bearing wall **+10**; through the floor above (screed on
  top) **+10**; skeleton frame column path **+20**; via two-leaf party wall **+15**.
- Timber decks (4109-2 Tab 3): Df path K₁ by receiver-wall lining — 2×GK on spring
  rail / 1×GK / battens-direct: GK 6/3/1, GF 7/4/1, HW 9/5/4 dB; plus K₂ for the
  screed-edge bridge DFf (e.g. GK+HW build-up: at L_n,w+K₁ = 35→+10 dB, 40→+5,
  45→+3, 50→+1, >55→0; capped reference values 44/40/38 dB by lining).

### 6.6 Staircases (massive, DIN 4109-32 Tab 6) [T3]

RC flight/landing ≥ 120 mm, L_n,eq,0,w / L'_n,w (dB):

| Detail | L_n,eq,0,w | L'_n,w |
|---|---|---|
| Landing cast into stiff single-leaf wall (m′ ≥ 380) | 63 | 67 |
| Flight bonded same way | 63 | 67 |
| Flight set back from wall | 60 | 64 |
| Landing with full building separation joint | ≤50 | ≤47 |
| Flight decoupled + separation joint | ≤43 | ≤40 |
| Flight elastically supported on landing | 35 | 39 |

Coverings/floating screed on top then compute via ΔL_w as §6.3. Rules: separation
joints ≥ 30 mm; landings must meet the requirement on their own (floating screed);
elastic bearings for flights; resilient coverings on escape stairs often blocked
by fire rules — coordinate with `building-regulations-permits`.

## 7. Flanking verification (DIN 4109-2 simplified model)

### 7.1 Path model and proof logic [T2]

Transmission paths: direct **Dd**, transmitting→flank **Df**, flank→receiving
**Fd**, flank-flank **Ff** (13 paths typical for a room pair). Energy sum:
R′w = −10·lg[ 10^(−0,1·R_Dd) + Σ 10^(−0,1·R_path) ] (per-path values combined as
transmission energies; paired ij/ji paths averaged as 10^−(Rij+Rji)/20 in the
worked workbook). Safety margins are built into the *requirement* side (§8.1):
compare with 0,1 dB precision (54,9 − 2 < 53 = FAIL — no rounding mercy).

Per-path airborne flanking (massive):
**R_Ff,w = R_F,w + R_f,w + ΔR_Ff,w − K_Ff − 10·lg(S_s/(l_f·l₀))**, l₀ = 1 m
[VERIFY sign/term layout vs ISO 12354-1 — the digest prints variants; worked
values follow this form]. R_F,w / R_f,w = ratings of the two flanking components,
ΔR from front shells on the receiving/source side (§5.4), K_ij junction (§7.2),
S_s separating element area, l_f joint length. Light construction: substitute
measured D_n,f,w flank catalogues (§7.3).

### 7.2 Junction attenuation K_ij (DIN 4109-32) [T3]

Mass ratio **M = lg(m′ᵢ/m′⊥ᵢ)** (separating vs perpendicular flank; can be negative).
Rigid massive joints (dB):

| Joint | K₁₃ (Ff) | K₁₂ = K₂₃ (Df/Fd) |
|---|---|---|
| T-junction | 5,7 + 14,1M + 5,7M² (M<0,215); else 8,0 + 6,8M | 4,7 + 5,7M² |
| Cross junction | 8,7 + 17,1M + 5,7M² (M<0,182); else 9,6 + 11,0M | 5,7 + 15,4M² |
| Corner | — | 2,7 + 2,7M² |
| Thickness change | 5,0M² − 5 | — |

- Elastic interlayer (E_dyn MN/m², thickness t m): ΔK_ij = 36 − 15·lg(E_dyn/t);
  K₁₃ + 2ΔK, K₁₂/K₂₃ + ΔK; decoupling-by-interlayer base K₁₃ = 3,7+14,1M+5,7M².
- Full circumferential decoupling: K_ij,max = K_ij + 20 dB (then flanking is
  effectively dead — S54: fully separated joint ≫ partial elastic).
- Floor-slab/interior-wall rubber-granulate interlayer example: E_dyn 0,63,
  15 mm → ΔK ≈ 11,7 → cross-joint K ≈ 18.
- Lower bound K_ij,min (geometry-capped, printed form ambiguous — VERIFY vs
  4109-32); if computed K < K_ij,min use K_ij,min.
- Gypsum-block walls: vertical cross +15/+5; horizontal cross ΔK cork 2 / PE 12.
- Offset flanking walls: continuation < 0,5 m → treat as cross joint; ≥ 0,5 m →
  kinked T with combined mass 0,5(m′₁+m′₂) (S37: offset costs ≈ 2 dB).

### 7.3 Light/roof construction flank data [T3]

- Timber/light: use catalogue **D_n,f,w** per junction detail (4109-33 tabs);
  rule of thumb: separation adequate when **D_n,f,w ≥ R'w + 5 dB**; exact:
  R_Ff,w = D_n,f,w + 10·lg(l₀/l_f) ± geometry term (10·lg(S_s/A₀)) — the two
  digest prints disagree on the S_s sign [VERIFY]; worked: wall D_n,f,w 76 →
  R_Ff 78/79 → total R'w 67 (S36); roof MW build-up 65 → R_Ff 64.5 vs rigid
  foam 53 → 52.5 → foam roof worsens R'w by ≈3 dB below the 54 target (S39);
  fixes: ballast + sealing (65→69) or 20 mm MW over foam + cavity damping (→66).
- Sub-ceiling flank examples (h = 400, fibre in cavity 0/40/80 mm): wall-abut
  1×GK continuous 48/49/50; 2×GK 55/56/56; jointed 1×GK 50/54/56; split layers
  2×GK 57/59/59; wall-to-slab + split ceiling 2×GK **57/65**. Absorber barrier
  across cavity b 300/400/500/600/800/1000 mm → +12/+14/+15/+17/+20/+22 dB
  (r ≥ 8; cap D_n,f,w ≤ 67). Suspension height > 400 mm: −2 (≤600) −5 (≤800)
  −6 (>800) with ≥50 mm cavity absorbent. Open grid ceilings 28–46 dB — poor flanks.
- Light roofs (4109-33): rigid-foam above-rafter builds R_w 34–58 by variant;
  MW above-rafter 100/160 mm → 46/50; wood-fibre 140/240 → 48/52 (+ballast 54/58);
  between-rafters + boards 50–59; roof flanking D_n,f,w by build-up type A/B/C
  53→>75 — full tables in norm; representative: combined above+between
  ≥120+≥140+2GK → R_w 58(−2;−8).

### 7.4 Conversions between room and component quantities [T3]

- D_nT,w = R′w + 10·lg(0,32·V_E/S_S) (receiving room); inverse for required R′w.
- L'_nT,w = L'_n,w + 10·lg(0,032·V_E) [VERIFY constant 0,032 vs 0,32 — worked
  VDI conversion 75,6 m³ shifts 37→40,8 consistent with 10lg(0,1·V)-type scaling;
  confirm in 4109-2 (5.4.8-3)].
- Required R′w from required D_nT,w: R′w,erf = D_nT,w,erf + 10·lg(S/A),
  A = 0,32·V (T₀-based) → strongly geometry-dependent: for a fixed
  D_nT,w = 53 requirement the needed R′w spans ≈ 45…63 dB over room depths
  10→3 m — small deep rooms punish light separating walls.
- Small source room S_s < 10 m²: D_n,w = R′w + 10·lg(S_s/10 m²).

## 8. Required values — DIN 4109 and graded standards

### 8.1 Proof logic (DIN 4109-1:2018 + -2) [T2]

- **Vorhaltemaß (design margin)**: airborne — provided value must **exceed**
  requirement by 2 dB (walls/ceilings and R′w,ges): R′w,erf = R′w,zul + 2;
  **doors +5 dB**; impact — provided must stay **3 dB below** limit:
  L′n,w,vorh = L′n,w,zul − 3 (equivalently prove L′n,w + 3 ≤ zul).
- Compute and compare at 0,1 dB resolution.
- Two legal regimes: public-law minimum (DIN 4109-1 via LBO "allgemein anerkannte
  Regeln") vs contractual (DIN 4109-5, VDI 4100, DEGA 103 — private law only).
  Wording like "gehoben"/"zeitgemäß" in a contract already implies above-minimum.
- Protected rooms (Schutzbedürftige Räume): living, bedrooms, hotel/sick rooms,
  teaching, offices, consulting/meeting rooms. Non-protected: corridors of own
  flat, stairs (partly), storage, garages, plant rooms.

### 8.2 Multi-family / office / mixed use (DIN 4109-1 Tab 2) [T3]

R′w required / L′n,w max (dB), ceilings (Decken) and walls:

| Element | R′w ≥ | L′n,w ≤ |
|---|---|---|
| Ceiling under usable roof/loft | 53 | 52 |
| Dwelling-separating floors (incl. flats' stairs) | 54 | 50 (timber/light/dry or pre-07/2016 alteration: 53) |
| Floors between foreign working rooms | 54 | 53 |
| Floors over cellar/hall/stair, under staying rooms | 52 | 50 |
| Floors over passages/garage ramps | 55 | 50 |
| Floors under/over play & common rooms | 55 | 46 |
| Under terraces/loggias (over rooms) · arcades | — | 50 · 53 |
| Balconies (over rooms) · duplex floors/stairs | — | 58 · 50 |
| Under bath/WC | 54 | 53 |
| Flights/landings (own dwelling) | — | 53 |
| Dwelling-separating walls | 53 | — |
| Stair-room / hall walls | 53 | — (wall-with-door: erf R′w,wall = erf R′w,door + 15 dB; strips < 30 cm ignored) |
| Walls beside passages/garages | 55 | — |
| Walls of play rooms | 55 | — |
| Lift-shaft walls at staying rooms | 57 | — |
| Doors: into closed corridor | 27 | — |
| Doors: directly into room | 37 | — (+5 Vorhaltemaß on top) |

### 8.3 Semi-detached / terraced (Tab 3) [T3]

Party walls (Haustrennwände): to rooms on lowest floor **≥ 59**, with ≥ 1 floor
below **≥ 62**; floors (horizontal/diagonal) L′n,w ≤ 41; slab-on-grade / cellar
ceiling ≤ 46; stairs ≤ 46. DIN 4109-5 raises these (see §8.6: 62/67, white-tank
continuous basement variant 64).

### 8.4 Hotels / hospitals / schools (Tabs 4–6) [T3]

- Hotels: floors ≥54/≤50 · pools & play ≥55/≤46 · bath/WC ≥54/≤53 · stairs ≤58
  (none if lift) · walls room↔corridor ≥47 · door corridor→room ≥32.
- Hospitals: floors ≥54/≤53 · pools ≥55/≤46 · stairs ≤58 · ward/corridor/consult
  walls ≥47 · rooms of discretion/quiet ≥52 · theatre/treatment ≥42 · ICU corridor
  ≥37 · doors: consult ≥37, discretion ≥37, ward/theatre ≥32.
- Schools (incl. day-care): floors teaching↔teaching & under corridors ≥55/≤53 ·
  vs halls/workshops ≥60/≤46 · vs loud rooms ≥55/≤46 · walls teaching↔teaching/
  corridor ≥47 · vs stairwells ≥52 · vs loud ≥55 · vs halls ≥60 · doors to
  corridor ≥32, between rooms ≥37.

### 8.5 "Particularly loud" rooms vs protected rooms (Tab 8) [T3]

R′w (ceilings/walls) / L′n,w (floors) / L_AF,max inside the loud room:
plant rooms 75–80 dB → ≥57 (81–85 dB → ≥62), ≤43 · trade/sales ≥57/≥62, ≤43 ·
kitchens until 22 h ≥55, ≤43; after 22 h ≥57, ≤33 (industrial kitchen + dwellings
above: 62) · gastronomy until 22 h ≥55/≤43; later L_max ≤ 85 → ≥62/≤33 ·
bowling: skittles room ≥67, lane floor ≤33, ball-drop zone ≤13 [VERIFY] ·
gastronomy with electroacoustic 85–95 dB → ≥72, ≤28 (see also VDI 3726 §8.9).
Building services into foreign protected rooms: sanitary water supply/drainage
L_AF,max,n ≤ 30 (living/bed) / ≤ 35 (teaching/work); other fixed tech + garages
same; restaurants/kitchens/shops day L_r ≤ 35 & L_max ≤ 45; night living L_r ≤ 25
& max ≤ 35. Own-flat HVAC: living ≤ 30, kitchen ≤ 33 (continuous ton-free +5
permitted; recommend 30/33). Tapware per ISO 3822: **group I ≤ 20 dB(A)**
(outlet fittings, valves…), group II ≤ 30; accessories ≤ 15/≤ 25; +5 at upper
pressure/flow. Group I mandatory where the plan is acoustically unfavourable.

### 8.6 DIN 4109-5:2020 "erhöht" grading (verify current) [T3]

Ceiling under roof ≥56/≤47 · dwelling separation floors ≥57/≤45 · cellar/hall
below ≥55/≤45 · garage ramp ≥58/≤45 · play ≥58/≤41 · terrace/loggia ≤45 · arcade
≤48 · balcony ≤58 · duplex ≤45 · bath/WC ≥57/≤47 · hall floor ≤45 · stairs ≤47 ·
dwelling-separating walls ≥56 · stair/hall walls ≥56 · garage walls ≥58 · play ≥58 ·
lift shaft ≥57 (=4109-1) · doors corridor→hall ≥32, →room ≥42 (40 with equivalent
vestibule). Row-house party wall ≥62 / ≥67 with a floor below (WU continuous 64);
floors ≤36, slab ≤41, stairs ≤41. Hotels: floors ≥57/≤45 · pools ≥58/≤41 ·
bath ≥57/≤47 · stairs ≤48 · walls ≥52 · door ≥37. Hospitals: floors ≥57/≤46 ·
pools ≥58/≤46 · bath ≥57/≤46 · stairs ≤48 · ward walls ≥52 · discretion ≥55 ·
theatre/ICU ≥42 · doors consult ≥40, ward ≥37. External elements: no extra
requirement (lower base noise caveat). Soft-floor credit not allowed for dwellings
(4109-5 Tab 1), allowed hotels/hospitals. Services: sanitary MFH L_max,n ≤ 27,
row ≤ 25 (spikes +10); own HVAC ≤ 27 (design air rate, e.g. 15 m³/(h·person)
bedroom; continuous +3; switch spikes +5).

### 8.7 VDI 4100 grading (10.2012, private law) [T3]

Levels: **SSt I** raised comfort from basic · **II** average comfort ·
**III** special comfort; **EB I/II** = own-area levels (within one dwelling).
Required D_nT,w (airborne) / L'_nT,w (impact):
- MFH between foreign rooms: D_nT,w ≥ 56/59/64; stair wall-with-door ≥ 45/50/55;
  row/semi to foreign ≥ 65/69/73; own EB I/II walls+floors 48/52; open-plan wall+
  door to separate room 26/31.
- Impact MFH all directions L'_nT,w ≤ 51/44/37; row/semi ≤ 46/39/32 (incl.
  balcony/loggia/terrace); enclosed stair 53/46.
- Services in foreign protected rooms L_AF,max,nT ≤ 30/27/24 (MFH), 30/25/22
  (row), 35/30 (own); spikes ≤ +10.
- External SSt III required R′w,res by Lärmpegelbereich I–VI: 35/35/40/45/50/55
  + area correction for (S_window+S_wall)/S_G: 2,5→+5 · 2,0→+4 · 1,6→+3 ·
  1,3→+2 · 1,0→+1 · 0,8→0 · 0,6→−1 · 0,5→−2 · 0,4→−3 dB.
- Perception anchors (base 20 dB(A) evening): SSt II — normal speech not
  intelligible, loud music still audible, walking not disturbing; SSt III —
  normal speech not audible, party still audible, services not/rarely disturbing.
- Older VDI 4100:2007 withdrawn — do not cite; sanitary MFH II/III 30/25 per both.

### 8.8 DEGA 103 (2018) certificate classes A*…F + EW1–3 [T3]

Direction-independent component requirements (site class A* very quiet … F
industrial): walls R′w F<50 E≥50 D≥53 C≥56 B≥62 A≥67 A*≥72 · ceilings ≥50/54/57/
62/67/72 · front doors to hall Rw ≥22/27/32/37/40 (direct into room ≥32/37/42,
C and better not permitted) · impact floors L′n,w >60/≤60/≤50/≤45/≤40/≤35/≤30 ·
balcony/terrace >63/≤63/≤50/≤48/≤43/≤38/≤33 (balcony D ≤58) · stairs/halls ≤53(D)/
≤48/≤43/≤38/≤33. Class D ≈ DIN 4109-1 level; external: B needs +Ctr,50–3150
correction; area character F GI ≥76 / E GE-MU 71–75 / D MI-WB 66–70 / C WA 61–65 /
B WR 56–60 / A,A* ≤55. Services+sanitary L_AF,max,n F>35 … A/A* ≤20; structure-
borne decoupling quality (hammer excitation) L_Kn,w >63/≤63/≤58/≤53/≤48/≤43/≤38.
Own area EW1/2/3: walls ≥40/43/47 · internal floors ≥48/51/55 · room doors (open
plan) ≥22/27/32, closed ≥17/22/27 · impact ≤58/53/46 · sanitary ≤35/30/25 ·
heating/vent ≤30/25/25. Validity assumptions: T = 0,5 s (A = 10 m²), V 30–60 m³,
S 10–15 m², smooth curves, base noise 20 dB(A) pink. Stairs/corridors absorption:
A/V ≥ 0,10 (D), ≥ 0,20 (C/B), even distribution.

### 8.9 Offices and special uses [T3]

- VDI 2569 (A/B/C confidentiality): D_nT,w single↔single ≥42/37/32 · multi↔multi
  ≥37/32/27 · to confidential ≥50/45 · L'_nT,w from traffic ≤55/60/65 ·
  max disturbance from loud room: single ≤25/30/35; services+external ≤30/35/40.
- VDI 3726 gastronomy/bowling: G-I (day cafés ≤22 h, PA ≤75) R′w 55 ·
  G-II (≤80 PA, after 22 h) 62 · G-III (≤95 PA) 72 · G-IV above that: separation/
  buffer only; bowling skittles room R′w 67 (L_AFm ≤85, max ≤90), lane ball-drop
  ≤95 R′w 67, pin-deck impact ≤105 >72.
- Sports halls DIN 18032 + 4109: services into foreign living/teaching ≤30;
  ceilings teaching↔hall ≥60/≤46; walls ≥60; vs protected rooms by hall level
  75–80/81–85 → ≥57/≥62; divider curtain ≥18 installed (incl. flanks) / ≥22 type
  tested — must carry absorption, minimize slots.

## 9. Element catalogues (T3 excerpts — representative rows)

### 9.1 Massive floors (ceilings) [T3]

- Direct airborne path: single-leaf mass law §4.2 with total m′ (§4.3 densities).
- Impact: §6.2 source level + §6.3 floating-screed ΔL_w − §6.5 corrections.
- Flanking D_n,f,w of floating screeds: cement/Ca-sulf/Mg 40 · mastic 46 ·
  full-penetration separation joint 57 dB (retro-cut joints worse).
- Grid/suspended ceilings as flank linings: closed-face boards m′ ≥ 4,5/6/8/10
  with 40/80 mm fibre → 45→62 dB band; open-faced mineral tiles 28–56;
  light-chip and perforated metal variants in norm tables (§7.3 anchors).

### 9.2 Timber beam decks (Holzbalkendecke, DIN 4109-33) [T3]

Representative L_n,w(C_I) / R_w(C;Ctr) build-up pairs:

| Build-up | L_n,w | R_w |
|---|---|---|
| Screed 50(120)/MW 40 (s′≤6)/HW 22/beam 220 | 47(−3) | — |
| + fill ≥45 kg/m² | 50(−2) | 67(−1;−6) |
| + ceiling on batts, 100 cavity absorbent, GK12,5 | 54(+2) | 63(−5;−11) |
| Spring-rail ceiling | 46(0) | 70(−3;−9) |
| Spring-rail + ballast | 30 | ≥70 |
| Board-stacked (BSB ≥120) + screed + MW | 56(−3) | 62(−2;−7) |
| BSB + ballast 45 | 45(−1) | ≥70 |
| BSB + fill 120 | 41(−1) | 70(−4;−10) |

Deck flank D_n,f,w with sub-ceiling: battens-through + GK 52 · spring bracket
59 · 2×GF battens-fixed 61 · 2×GF on spring-brackets 67 dB. Separator flanking:
m′ ≥ 350 slab/wall 76 · timber beam/solid 67 dB.

### 9.3 Light roofs (above-/between-rafter, 4109-33, rafters ≥ 600 mm) [T3]

R_w examples (C;Ctr): above-rafter rigid foam 100+19 NFS → 34(−2;−6); +ballast
≥10 → 39; +below DES ≥20 → 42; +above DAD → 45. Above-rafter MW 100/160 →
46(−3;−9)/50(−3;−10); WF 140/240 → 48/52, +ballast 54/58. Between + GK:
120–180 → 50; ≥180 → 52; ≥200 WF+GF → 57; 3×GF → 59; combined above+between
≥120+≥140+2GK → 58(−2;−8). Covering ΔR: concrete tile 0 / clay −2 / beaver +2.
Timber flat roof: gravel build-up 45, +extra lining m′>8 → 50. Roof flanking
D_n,f,w connection types A/B/C: rigid foam 53/58/65 · +ballast 56/60/69 ·
MW 65/68/>75 · WF 63/65/>75 (caps 67–75 by damping/sealing). Terrace over 200 mm
RC: ΔL_w 19 (pavers on pedestals, 2× bitumen + 60 EPS) to 34 dB (MW + 8 mm
rubber-crumb/PUR variants 21–29); cantilever balconies: impact diagonal-below
only; thermal-break elements with continuous rebar help acoustics (coordinate
with `building-physics-thermal-moisture`).

### 9.4 Windows (DIN 4109-35 / EN 12758) [T3]

Correction chain: R_w,Fenster = R_w + K_AH(−1 alu-wood) + K_RA(frame <30 %) +
K_S(stulp) + K_FV + K_F,1,5(<1,5 m²) + K_F,3(single pane ≥3 m², −2) + K_Sp(bars).
Installed practice: −2 dB margin; tilted window gives only 6–12 dB in that state.
Catalogue (double-glazed, total glass mm / cavity / R_glass dB, seals):

| R_w | Glazing basis | C;C_tr |
|---|---|---|
| 33 | ≥4+4/12/R≥30 | −2;−5 |
| 35 | ≥6+4/12/32 | −2;−4 |
| 37 | ≥6+4/12/35 (or 16/35 asym.) | −1;−4 |
| 38 | ≥8+4/16/38 AD/MD+ID | −2;−5 |
| 40 | R_glass ≥ 40, 2 seals | −2;−5 |
| 42 | ≥44 | −2;−5 |
| 44 | ≥49 (+K_FV) | −1;−4 |
| ≥46 | test required | — |

Glass panes (monolithic R_w−1−2 C;Ctr): 4 mm 29(−2;−3) · 6 mm 31(−2;−3) ·
8 mm 32(−2;−3) · VSG 6/8/10/12 → 32/33/34/36. DG air/argon: 4/16/4 → 29(−1;−4) ·
6/16/6 → 31(−1;−4) · 8/16/6 → 35(−3;−6) · 8/16/8 → 32 (coincidence dip — asymmetric!) ·
DG+VSG 6/16/10VG → 38(−1;−5) · 3-glazing 8/16/4/6/16/6 → 37(−3;−7).
Single-glazed/box windows: 25 (single ≥4, 1 seal) up to 45 (box 8+6, 2 seals);
box = ventilated cavity only with labyrinth seal. Roller-shutter boxes: catalogue
VDI 2719-style build-ups reach R_w ≥25…40 (inner apron + lid + all joints sealed);
≥45 needs lab test — classic weakest-link element (§10).

### 9.5 Doors and joints (DIN 4109-35) [T3]

- Door proof without test: leaf R_w ≥ req + 2 (rebated) / + 4 (flush); rebate
  seal R_S,w ≥ req + 10; floor seal R_S,w ≥ req + 10 (req ≤ 35, wood/metal frames,
  single-leaf). Frame corrections (single/multi-leaf, Rw 30–34/35–40): double
  frame 0/−2 · 15 % lite simple glazing +1/−3 · laminated +1/−1 · 50 % lite
  0/−8 · simple latch −1/−1 · double cover plates (DIN 68706) +2/0.
- Joint R_S,w (dB per 1 m² & 1 m): bare door bottom b5 20 / b7 18 / b10 15 ·
  drop-seal over carpet b5 25 · rebate seal full b5 ≥35. Permanent construction
  joints (depth 50–100): empty b10 15 / b20 10 / b30 5 · MW b10 35–45 ·
  mounting foam ≥50/47/45 · backer rod + elastic sealant ≥55/54/53 ·
  connector tape b≥1 mm ≥50/45/40.
- Criterion: joint loses ≤1 dB of a wall only if **R_S ≥ R_w + 10 dB**;
  combined: R_j,w = −10·lg[10^(−R_w/10) + (l/S)·10^(−R_S/10)].
- Mounting: one-side foam + elastic seal both faces; floating screed/hard floor
  split at the door line; carpets split by threshold (else impact bridge).

## 10. Outdoor noise and façade insulation

### 10.1 Required façade value (DIN 4109-1/-2) [T2/T3]

erf R′w,ges = L_a − K_Raumart + K_AL, K_AL = 10·lg(0,8·S_S/S_G)
(S_S envelope area of room, S_G floor area). K_Raumart: 25 (ward/hospital beds,
min R′w,ges 35) · 30 (apartments, hotel rooms, classrooms; min 30) · 35 (offices).
**Lärmpegelbereich (noise level zone) → design level L_a (dB(A))**:
I 55 · II 60 · III 65 · IV 70 · V 75 · VI 80 · VII >80 (site-specific).
If day−night difference < 10 dB → L_a = L_night + 10 (+3 per (5.3.2-8), VERIFY).
Source summation: road (DIN 18005-1:2002 nomograms +3 / 16. BImSchV calc +3),
rail (−5 spectral correction), air, industry (TA Lärm limit +3); one +3 on the
energetic total only. Opposite façade: open 5 / closed courtyard 10 dB(A) reduction.
Composite: R_e,i = R_i + 10·lg(S_ges/S_i); R′w,ges = −10·lg Σ(S_i/S_ges)10^(−R_e,i/10).
Slit/joint scaling: D_n,e,w = D_n,e,lab,w + 10·lg(l_situ/l_lab); open aperture
D_n,e ≈ 10·lg(1/S_Öffnung) — an open 1 m² vent alone caps the façade near 25–30 dB.

### 10.2 Limit-value tables (T2; verify current issues) [T3]

TA Lärm (commercial/industrial plants), outdoors day 6–22 / night 22–6 dB(A):
industrial 70/(—) · trade 65/50 · urban 63/45 · core/village/mixed 60/45 ·
**general residential/small settlement 55/40** · pure residential 50/35 ·
spa/hospital/care 45/35. Peaks day +30 / night +20; calm periods (+6 dB(A)):
weekdays 6–7 & 20–22; Sun/hol 6–9, 13–15, 20–22. Rare events (≤10 d/a, ≤2
consecutive weekends): trade & urban..general-residential 70/55. Indoors
(protected rooms): day 35 / night 25 dB(A), peaks +10; assess LR − 3 dB(A).
16. BImSchV (roads/rail fixed limits): hospital/school/spa/elderly 57/47 ·
pure+general residential & small settlement **59/49** · core/village/mixed 64/54 ·
trade 69/59 (note the clash with TA Lärm 55/40 for the same WA area — the
stricter/applicable regime depends on the polluting source; VERIFY in each case).
18. BImSchV (sports facilities) day/quiet/night ≈ trade 65/60/50, urban 63/58/45,
core-mixed 60/55/45, residential 55/50/40, pure 50/45/35, spa 45/45/35 [VERIFY
column alignment — digest print garbled].
DIN 18005-1 orientation values (urban planning, road|rail|ship / industry|leisure):
WR 50/40 & 50/35 · WA/WS 55/45 & 55/40 · cemeteries/parks 55 · WB 60/45 ·
MD/MI/MU 60/50 · MK 63/53 · GE 65/55 · open single window at >45 dB(A) night ≈
sleep disturbed (design cue for "noise-protected outdoor areas" — no digested
numerical procedure; treat balcony/garden levels per TA Lärm/18005 locally).
Lärmindizes (34. BImSchV / EU END): L_day 6–18, L_evening 18–22, L_night 22–6;
L_DEN = 10lg[1/24(12·10^0.1L_d + 4·10^(0.1(L_e+5)) + 8·10^(0.1(L_n+10)))]
[evening +5 / night +10 per directive, VERIFY vs digest which lists indices only];
mapping methods VBUSch/VBUS/VBUF/VBUI (2006), VBEB (2007); action plans mandatory.
DIN 18005 clearance distances (night, free field, no measures) from axis [m] for
L_r 55/50/45/40: motorway 60 000 veh → 520/900/1400/2000 · federal 15 000 →
110/240/470/840 · county 6000 → 50/110/240/480 · HSR 36 tr/250 km/h →
60/130/300/550 · mainline 200 → 300/600/1100/1800 · tram 200/60 → 5/20/35/70.
Road nomogram corrections (old): SMA/AC≤11 −2 · open-porous >60 −5 · uneven
paving ≥50 km/h +7 (30 km/h +5) · 80 on motorway −2,5 · 30 town −2,5 ·
multiple reflections +2 · junctions +2.

### 10.3 Propagation model summary (ISO 9613-2 class 2) [T2, condensed]

L_Aeq(DW) = L_W + D_C − A; A = A_div + A_atm + A_gr + A_bar + A_misc;
A_div = 20lg(d/d₀); A_atm = α·d/1000 (α = 0,1/0,3/1,1/2,8/5,0/9,0/22,9/76,6
dB/km at 20 °C/70 % RH for 63→8000 Hz bands); ground G = 0 hard / 1 porous,
A_gr up to ≈ −1,5…−10 dB by zone geometry q = max(0, 1−30(h_s+h_r)/d_p);
screening single-edge cap 20 dB, multi 25 dB, requires mass ≥ 10 kg/m²,
surface-closed, width > λ; housing additions cap 10 dB(A);
D_C = D_I (façade radiation: own side 0, flanks −5, back −10) + D_W directivity
(half-space +3, quarter +6, eighth +9); C_met = C0·(1−10(h_s+h_r)/d_p) for
long-term averages, d_p > 10(h_s+h_r). TA Lärm accounting: L_G,r =
10lg(10^0.1L_V,r + 10^0.1L_Z,r); tone/info K_T 0/3/6; impulse K_I 0/3/6;
building-envelope reradiation L_WAeq = L_I − R′_w + 10lg(S/S₀) (VDI 2571/12354-4;
+5 dB safety for strong low-frequency internals). Reference point: 0,5 m outside
the open window of the most affected protected room.

## 11. Room acoustics (DIN 18041)

### 11.1 Core physics [T2]

- Reverberation: **A = 0,163·V/T** (Sabine; A in m² equivalent absorption area;
  some references print 0,161 — VERIFY which constant the norm edition uses);
  T = 0,163·V/A. Doubling A halves T and drops level −3 dB.
- A = ΣαᵢSᵢ + ΣA_j(objects) + Σα_s,k·S_k + A_air; A_air = 4mV (m = air attenuation
  per m; 20 °C/50–70 % RH: m(125…8000 Hz) ≈ 0,1/0,3/1,1/2,2·10⁻³…0,0135 —
  ignore if V < 200 m³ and f ≤ 1000 Hz). Hard object: A_obj = 2·V_obj^(2/3).
- Diffuse-field level: L_p = L_W + 10·lg(4/A); level drop examples: A = 4 m² →
  0 dB · 16 → −6 · 28 → −8,5 dB; A ≈ 0,8·S_g typical furnished room.
- Reverberation radius r_H = 0,14·√A (beyond it added absorption cuts level;
  inside it it does not); boundary radius r_A = 0,2·√A.
- Transit-time/echo: reflection path difference Δl ≤ 17 m (≤ 50 ms) reinforces
  speech; 17–34 m (50–100 ms) worsens clarity; > 34 ms-equivalent → discrete
  echo. DIN 18041 window: ≤ 50 ms speech, ≤ 80 ms music; strict echo criterion
  ∆x = 17 m (speech) / 27 m (music) [VERIFY both prints coexist in sources].
- Room modes: f_nx = n·c/(2l); modal band up to f_g ≈ 2000·V^(−1/3) Hz
  [digest prints 125·(180/V)^(1/3) variants — VERIFY]; cubic 10×5 m room mode
  (1,1,0) = 38 Hz. Avoid dimension ratios ≈1:1:1 and near-integer ratios;
  good proportions chart x,y ≈ 1,0–2,4 (T4).
- Levels: L_NA disturbance budget; speech 10 dB above it; STI bands
  (IEC 60268-16): A+ >0,76 studio … D 0,62 lecture/classroom … G 0,50 alarm
  target, <0,36 unsuitable.

### 11.2 DIN 18041 requirements [T2/T3]

Group A (communication at distance; occupied ≥ 80 % seats): A1 music ·
A2 speech/lecture · A3 lecture-inclusive/teaching-communication (≤1000/5000 m³) ·
A4 teaching-inclusive (≤500 m³) · A5 sport (200–10000 m³). Target T (500–1000 Hz
mean, occupied):

| Use | T_soll [s] |
|---|---|
| A1 | 0,45 + 0,07·lgV (30–1000 m³) |
| A2 | 0,37 + 0,14·lgV (50–5000 m³) |
| A3 | **0,32 + 0,17·lgV** (30–5000 m³) |
| A4 | 0,26 + 0,14·lgV (30–500 m³) |
| A5 | 0,75·lgV − 1,0; = 2,0 above 10 000 m³; ±20 % at 250–2000 Hz |

Empty-room T may exceed by ≤ 0,2 s (A5 by chart); octave tolerance T/T_soll:
low bands down to 50 % (125), mid 80–145/170 %, high down to 50 % [figure read,
VERIFY bands]. Disturbance limits (A-rooms): L_NA,Bau+Betrieb A1 ≤30 · A2–A4 ≤35 ·
A5 ≤40 dB(A). Group B (short distance, absorption ratio A/V per m²/m³ at
250–2000 Hz excl. persons): B1 none · B2 ≥0,15 (h≤2,5 m) / ≥(4,80+4,69·lg h)⁻¹ ·
B3 ≥0,20/(3,13+4,69·lg h) · B4 ≥0,25/(2,13+…) · B5 ≥0,30/(1,47+…) — use the
norm tables for exact h-dependent values [VERIFY denominators].
Classrooms: T = (0,32·lgV − 0,17) s ±20 % mandatory (ASR A3.7 echoes this);
ASR A3.7: L_r ≤55 (I high concentration)/70 (II); T max call-centre 0,5 ·
multi-office 0,6 · single 0,8 s (250–2000). VDI 2569 offices: single ≤100 m³
T ≤ 0,6/0,8/1,0 (A/B/C; 125 Hz 0,8/1,0/1,2); small multi (dist <8 m) 0,4/0,5/0,7
(floor absorbers 0,2–0,3); large multi 0,6/0,7/0,9; D2,S ≥ 8/6/4 dB and
L_p,A,S,4m ≤ 47/49/51 dB; speech-privacy masking as last resort.
Kita: group rooms T60 ≤ 0,5–1,0 by V chart (63–8000 Hz) — recommend low T for
language development. Sports hall DIN 18032: 1,4 ≤ T_soll ≤ 2,5 s (A5 formula);
80–90 dB(A) during play — hearing protection >85 per VDI 2058-2; divider curtains
must absorb. Pools: Leq ≥ 80 typical; public T 1,7–2,0; with voice alarm 1,2–1,5
& STI ≥ 0,5; ball-proof absorbers; water surface hard.

### 11.3 Absorption coefficients α_s (octaves 125/250/500/1k/2k/4k) [T3 excerpts]

| Surface | α values |
|---|---|
| Concrete/rendered, plaster, brick | 0,01–0,03 flat |
| Lime-cement render / wallpaper | 0,02/0,03/0,04/0,05/0,07/0,08 |
| Double-glazed window | 0,28/0,20/0,11/0,06/0,03/0,02 |
| Parquet glued | 0,04/0,04/0,05/0,06/0,06/0,06 |
| Carpet ≤6 mm / 7–10 mm | 0,02/0,04/0,06/0,20/0,30/0,35 · 0,04/0,07/0,12/0,30/0,50/0,80 |
| 40 mm MW mat ρ20 direct (18 % perforated plate) | 0,11/0,36/0,68/0,88/0,89/0,97 (0,11/0,36/0,69/0,95/0,81/0,70) |
| Melamine foam 30/50 mm (8–10 kg/m³) | 0,12/0,31/0,66/0,86/0,87/0,92 · 0,16/0,56/0,87/0,96/0,97/0,97 |
| 35 mm wood-wool board direct | 0,08/0,17/0,70/0,71/0,64/0,64 |
| 9,5 perforated GK 19,6 % +30 MF+fleece a100 | 0,30/0,69/1,01/0,92/0,81/0,72 |
| Micro-perforated stretched ceiling 100 mm +40 fleece | 0,28/0,69/1,00/0,89/0,75/0,71 |
| Curtain woven 0,4 pleated 1:3 | 0,10/0,40/0,70/0,90/0,95/1,00 |
| Seated persons (theatre tip-up / padded chair) | 0,25/0,30×4 · 0,10/0,20/0,25/0,30/0,35/0,35 |
| ΔA per pupil primary/secondary (18041) | 0,05/0,10/0,20/0,35/0,40/0,45 · 0,10/0,15/0,35/0,50/0,50/0,55 m² |
| Large opening >1 m | 1,0 all bands |

### 11.4 Absorber physics and placement [T2/T4]

- Porous: needs thickness/air gap; flow resistivity r key (5–50 kPa·s/m² fills);
  thin acoustic plaster high-f only; carpet >1 kHz only.
- Panel resonator: f₀ = 160·√(s′/m′₁) type relation; cavity standing wave
  f_St = n·170/a; perforated/Loch absorber (Helmholtz):
  **f₀ = 170·√(S_H/(V_H·(d_H+2D_t)))** (S cm², V dm³, d cm; end correction
  0,8d round / 0,9a square / 0,9√A slot).
- Micro-perforated film (0,2 mm holes @2 mm pitch, m′ 0,14): α ≈ 0,5–0,9
  250–1000 Hz at 30–150 mm gap — visually clean option.
- Edge/corner "bass traps": velocity maxima → d = λ/4 depth (125 Hz → 68 cm);
  empirical α > 1 (volume-referenced); no calculation model.
- Reflectors need mass: ≈10 kg/m² (speech), ≈40 kg/m² (near-source music);
  structured surface seen when b_R > λ; concave radii between 0,5–2× source/
  listener distances cause focus — avoid; diffusers: g ≈ 500/f_opt (m), practical
  diffusion degree ≤ 0,8.
- Placement: concert halls — NO absorbers on side walls (first reflections) or
  stage; rear walls and ceiling borders yes; first-reflection ellipse check:
  a = 0,5(l₀+17), b = √(a² − 0,25·l₀²).
- Level reduction by retrofit absorption: ΔL = 10·lg(1+ΔA/A₀) = 10·lg(T₀/T) —
  +10 m² on A₀ = 10 → 3 dB; on A₀ = 60 → only 0,6 dB. Verify by before/after T.
- Lombard effect: speakers ramp to 50→85 dB(A) in loud classrooms — target
  ≤45 dB(A) speech level; avoid over-damping low-mids ("dröhnen").
- Hearing conservation: Leq 85 → 8 h exposure; each +3 dB halves time
  (88→4 h … 100→0,25 h); no damage probable at 85 dB ≤15 y (L_Ex,8h basis).

## 12. Equipment and plant noise (Gebäudetechnik coupling)

### 12.1 Limits and walls (DIN 4109-1 Tab 9/10 + -36) [T3]

- Sanitary supply/drainage into foreign protected rooms: L_AF,max,n ≤ 30 dB(A)
  (living/bed) / ≤ 35 (teaching/work); other fixed technology incl. garages same;
  gastro/kitchens/shops day L_r ≤ 35 & L_max ≤ 45, night living ≤ 25/≤ 35;
  own-flat HVAC living ≤ 30, kitchen ≤ 33 (continuous ton-free +5 permitted;
  spikes ≤ +5; design on night air rate, e.g. 15 m³/(h·person) bedroom).
  VDI 4100: water install MFH I/II/III 35/30/25; row 35/25/20; drainage alone II/III
  20/15; lifts at night 30 dB(A) dwellings/hotels/wards.
- Pipe-enclosing walls: m′ ≥ 220 kg/m²; no pipes in separating lightweight walls
  to protected rooms (voids the rating); tapware group I where unfavourable plan.
- Install noise is mostly structure-borne: decouple pipe↔clamp↔wall with resilient
  gaskets; closed-cell sleeve insulation OK, felt/open-cell NOT (mortar slurry =
  bridge); cover chases with plaster carrier + insulating fill, never mortar on
  pipe; allow thermal movement; exposed stacks often > 30 dB(A) — route through
  shafts away from bedrooms, ≥ 4 cm clear of wall face.

### 12.2 Plant rooms (Heizzentralen, RLT, CHP, lifts) [T3]

- Layout (MFeuVO/FeuVO frame, see `building-services-tga`): >50 kW own room, no
  openings except tight self-closing fire doors, no adjacency/connection to living
  or necessary stairs; ventilation openings upper+lower ≥ 150 cm² each — **treat
  vents as acoustic flanks**: silencers in supply/exhaust ducts, double-wall
  combustion exhaust shaft above roof with silencer (engine-driven HP > 50 kW).
- Inside: floating screed, resilient mounts under boilers/CHP/compressors,
  flexible connections, pipe decoupling; rooftop plant explicitly requires
  soundproofing (floating screed, resilient mounts, duct silencers).
- Lifts (DIN 8989 + VDI 2565/2566): machine-room shaft walls 490/580/670/740 kg/m²
  single-leaf by situation or two-leaf + MW joint; flanking walls ≥ 220–260;
  staircase wall ≥ 410; fully decoupled shaft = 30 mm joint + 380/580 kg/m² leaves;
  light partition beside shaft → heavy shaft wall; structure-borne acceleration
  limit 90 dB at 63 Hz (situation A). Responsibility = structural planner, not
  the lift vendor — resolve in the shell design.
- Duct regenerator note (RLT decentral units): alternating-cycle units and
  "phone-effect" duct coupling need silencers/regeneration at unit AND room
  entries (D_K path, §3.2).
- Emitting to outdoors (ISO 12354-4): L_p,i = L_w,i + D_c,i − A; segment walls
  b ≤ d/4; L_w = L_p,in + C_d − R′ + 10lg(S/S₀); C_d −6 small diffuse reflective,
  −3 absorptive, −5 large halls, −3/0 few directional; openings with silencer:
  L_w = L_p,in + C_d + 10lg(Σ(S_i/S)·10^(−0,1D_i)).
- Heat pumps (VDE/BAFA scheme): L_r = L_WAeq + K_T + K_0 − 20lg(s/s₀) − 11 + K_R
  dB(A); K_T tonality 0/3/6; K_0: free 3 m +3, one wall +6, corner/canopy +9;
  K_R +6 sensitive hours; ΔL table (day, K_0 = 3/6/9): s = 3 m → −5,5/−8,5/−11,5 ·
  5 → −10,0/−13,0/−16,0 · 10 → −16,0/−19,0/−22,0 · 20 → −22,0/−25,0/−28,0 dB
  (night −6); reference point 0,5 m before neighbour window. Mitigations in
  order: distance, unobstructed airflow, attenuate in/out air, fan matching,
  sealing, resilient mounting, duct silencers, cable loops 270–360° (§14 E5).
- Gastro to outdoors (VDI 2058 Bbl 1): erf R′w,res = L_AFm − L_r,zul − 20lg(s/s₀)
  + 10lg(S_g/S₀) − 12 dB; G-II…IV + bowling: windows egress-only (mechanical
  ventilation!), sound-lock double door to outside.

## 13. Worked examples (full numeric chains)

### E1 — Required party wall for DIN 4109-5 (S13/S15/S16 chain)

1. Requirement: row-house party wall with floor below, DIN 4109-5 → erf R′w = 67;
   Vorhaltemaß already inside the grade → design R′w ≥ 67 (T2 §8.6).
2. Candidate two-leaf: R′w = 28 + 18·lg(m′₁m′₂/(m′₁+m′₂)) + ΔR_w,Tr − K.
3. Solve: 18·lg(m′red) = 67 − 28 = 39 → m′red ≥ 165,8 kg/m² → equal leaves
   m′ ≥ 331,5 kg/m². With ΔR_w,Tr = 0 only achievable by KS/normal stone ≥ RDK 1,2.
4. Alternatives: 2×17,5 AAC RDK 0,6 + 50 mm WTH-filled joint: reduced mass 60,5
   → 60,1 + 14 = 74?? — digest prints base 28+18lg(121/2) = 62.7 with +2 rule not
   applied; treat as ≈63: meets 4109-1 (59) and -5 (62), NOT VDI 4100 SSt II (63).
5. 2×24 KS RDK 1,4 + putz, m′ 321,5 → m′red 160,8 → 28+38,5 = 66,5 + K 0,6 =
   67,1 ✓ with joint ≥ 30 mm, no mortar bridges (DEGA class A case).
6. WU shared basement (case 3, ΔR 3): KS RDK 1,4 m′ 248,9 → 66,5 ≥ 64 ✓;
   LB ρ 800 (m′ 141) → 61,6 ✗ → heavier stone or split the slab.

### E2 — Full DIN 4109-33 flanking workbook (S31 chain, must replicate)

Separating wall KS RDK 1,8, 24 cm: m′ = 432,8 → R_Dd = 59,3.
Flanks: exterior wall 336,4 (55,9) · ceiling 442 (59,5) · interior wall 146,5
(44,7) · floor 442 (+ΔR from screed 7,9/11,9 one/both sides). Geometry:
S_s = 10,84 m²; joint lengths 2,55 → 10lg(S_s/l₀-term) = 6,3 (wall), floor 4,25 → 4,1.
Joints: T K₁₃ = 5,7+14,1M+5,7M² with M = lg(m′ᵢ/m′⊥ᵢ) (e.g. 0,11 → K_Ff 7,3;
K₁₂ = 4,7+5,7M² → 4,8); cross K_Ff 8,5→14,1 at M≈1. Per-path:
R_Ff = R_F + R_f + ΔR − K − geometry → F1f1 69,5 · D1f1 68,7 · F2f2 72,1 ·
F3f3 65,8 · F4f4 84,0 (symmetric detail → R_Df = R_Fd).
Energy sum: **R′w = 55,9**. Requirement 53 + 2 = 55 → PASS at 0,1 dB resolution.
Offsets check (S37): l = 0,70 m > 0,5 → kinked T, m′₃ = 322,75, K_Ff 11,2 →
R_Ff 71,3, R_Df = R_Fd 69,2 → R′w drops to 55,4 (≈ −0,5…2 dB): offsets hurt.

### E3 — Façade mixture against sanatorium exposure (S7b chain)

1. Road 2000 Kfz/24 h at 20 m → L_a,day 64, night 54 → controlling L_a = 64+3 =
   67 dB(A) (DIN 18005 basis +3; day-night > 10 → use day value).
2. K_Raumart = 25 (bed room) → erf R′w,ges = 67 − 25 + K_AL(≈ −0,3…2,4 by room
   geometry) ≈ 41,7; + 2 Vorhaltemaß → design ≈ 44.
3. Wall (WDVS-optimized, E5 logic): m′ 466 → 60,2 − 1 EPS = 59,2 dB.
4. Windows+door must satisfy mixture: with S_w+d = 4,36, S_wall = 10,21,
   S_ges = 14,57 m² → R_e,window = 36,5 → **choose R_w 37** (installed −2 margin:
   product ≥ 39; penalty chain per §9.4 → order glazing package R_w 43, glass 46 —
   S51 lesson).
5. If the box window/shutter path is included (S12): worst element governs —
   RK-box 28 dB at 0,98 m² pulls 11,33 m² façade from ≈41 to 36,8 < 40 →
   solve needed R_RK = 34,7 → specify ≥ 35 dB box.

### E4 — Impact design of a parking-slab floor (S62 chain)

1. Slab 442 kg/m² → L_n,eq,0,w = 164 − 35·lg(442) = 71,4.
2. Requirement zul L′n,w = 50; margin: prove L′n,w + 3 ≤ 50 → target ≤ 47.
3. Flanking K = 0,6-type ≈ 9·lg(442/300) = 1,5 (T3, VERIFY form).
4. Required ΔL_w = 71,4 − 47 + 1,5 = 25,9 → floating screed 80 kg/m² + s′ ≤ 25
   → ΔL_w ≈ 26 ✓ (table §6.3). Edge strip full height, no pipes in screed.
5. Airborne through the slab/wall cross detail: with 15 mm rubber-granulate
   interlayer (E_dyn 0,63) cross-joint K ≈ 18 → R_Ff 72,8, R_Fd = R_Df 81,8 →
   detail R′w 46,5 vs lower-floor variant 46,4 → Δ 0,1 dB: the **direct path
   governs**; do not over-detail joints already ≥ R_w + 10 (S57 analog:
   stiff vs elastic edge 58,7/58,6 — "essentially nothing", 2,3 % energy).

### E5 — Double-leaf improvement design and its fragility (S41 chain)

1. Contract 64 dB (DEGA B + 2): light-concrete slab m′ 337,25 → raw 57,9 (LB-type
   curve, T3); needed ΔR = 6,1 dB → f₀ ≤ 93 Hz via ΔR = 74,4 − 20lgf₀ − 0,5R_w.
2. Spring under floating screed: with s′ = 30, m′₂ = [ (1000/2πf₀)²/s′ ]⁻¹ chain →
   build 60 mm screed → f₀ ≈ 93 → ΔR ≈ 6,1 ✓ → R′w ≥ 64.
3. Sensitivity: if the TSD creeps/stacks to s′ = 60 in service, f₀ > 100 Hz →
   improvement collapses → R′w falls below requirement — specify s′ with creep
   data and protect against point loads (failure pattern §15).

### E6 — Classroom reverberation sizing (S43 chain, DIN 18041 A3)

1. Room 262,5 m³ → T_soll = 0,32·lg(262,5) − 0,17 = **0,6 s** (500–1000 Hz).
2. A_needed = 0,163·V/T = 0,163·262,5/0,6 = 71,3 m².
3. Existing (occupied, no ceiling treatment): floor 75·0,05 = 3,75 · pupils
   24·0,35 = 8,4 · glazing 24,5·0,11 = 2,7 · door 2,45·0,06 = 0,15 · walls
   95,55·0,03 = 2,87 · air 0,63 → ΣA ≈ 18,5 (digest prints 18,5 incl. bookshelf?
   — recompute per project).
4. Deficit 52,8 m² on 75 m² ceiling: solve x·(0,71−0,09)·75 + 0,09·75 = 71,3
   → x = 0,99 → **100 % absorber ceiling required** (α 0,71 panel vs 0,09 paint);
   inclusive-use classrooms add rear-wall absorbers + curtains as reserve.
5. Echo check (S45 analog): lecture hall d_reflected − d_direct = 40,4 − 9,8 =
   30,6 m → 17–34 m band = clarity loss → absorb/tilt rear wall & rear ceiling;
   max room width for side-wall reflection ≤ 17 m extra path (S22): b_max = 28,3 m.

## 14. Design rules and planning sequence

### 14.1 Per-element rules of thumb [T4 unless tagged]

- Walls: choose mass ladder first (53 dB ≈ 24 cm KS RDK 1,8; 57 ≈ 30 cm RDK 2,0);
  double leaf only with clean separation, else lose more to flanking than f₀ gains.
- Party wall + WU basement: plan the separation in the foundation phase (case 3
  ΔR 3 vs case 1 ΔR 12 = 9 dB of future arguments).
- Floors: bare slab rating decides everything above; floating screed ≥ 45 mm,
  full-perimeter band, joints through build-up (57 dB flanks), no pipes inside;
  timber: spring-rail ceiling + ballast beats thicker boards.
- Stairs: bearing details, not coverings, own the result (35/39 dB elastic vs
  63/67 cast-in); landing is the weak plate — float it.
- Façade: windows set the limit; wall value beyond ≈ 5 dB over window+joint
  capability is wasted money; shutter boxes and roller boxes need their own spec
  line; > 50 % glazing share or > 40 % openable vent share → R′w,ges collapses.
- Rooms: group same-use rooms adjacently; small rooms → secondary use; no
  bath/WC above studies; no fittings in dwelling-separating walls.
- Installations: decouple on the LOUD side; Vorsatzschalen only with f₀ < 100 Hz;
  pipe sleeves closed-cell; shafts m′ ≥ 220 kg/m² (≥ 410–580 near lifts);
  light construction: separate cavity noggings, no continuous boards across
  separators, glued internal insulation raises s′ → flanking paths.

### 14.2 Planning sequence

1. **Usage map** (Nutzungsplanung): protected vs loud rooms, stack alignments,
   stair/plant cores away from bedrooms; group by equal requirement class.
2. **Requirement classes**: public-law DIN 4109-1 per use table; check contract/
   market standard (4109-5, VDI 4100 SSt, DEGA); fix the Nachweis basis and the
   margin convention (§8.1) in the design brief — before any build-up exists.
3. **Site levels**: L_a per source (DIN 18005/TA Lärm/16. BImSchV, +3 rules)
   → Lärmpegelbereich → façade erf R′w,ges incl. K_AL.
4. **Build-ups** (§4–§9 catalogues): walls/floors/windows selected with
   Vorhaltemaß; weak links (boxes, vents, doors) specified to the mixture, not
   the wall.
5. **Flanking proof** (§7): per room pair; iterate joint details with
   `construction-detailing`; re-check after every design change (offsets!).
6. **Equipment proof** (§12): plant, drainage groups, lifts, HP siting.
7. **Room acoustics** of shared rooms (§11): T_soll, A sizing, reflectogram/
   ellipse sanity, then absorber placement with fire/cleaning constraints.
8. Issue the Schallschutznachweis with editions, geometry assumptions,
   construction-sequence notes (screed band timing, joint cut-offs) and a
   measurement list for critical units (4109-4).

## 15. Failure patterns (design-site classics)

1. **Screed band gap / bridged floating floor**: edge strip omitted or compressed,
   partitions on continuous screed, retro-cut joints → ΔL_w evaporates; flanking
   57 → 40 dB class drop (§6.4).
2. **Light partition behind heavy wall / lining continuity**: continuous board
   skins across the separator transmit like a rail — worst of three lining cases
   (§5.5, §7.3).
3. **Double-leaf resonance in the audible band**: f₀ 134–360 Hz from thin gaps/
   stiff springs (EPS WDVS, tight studs) → ΔR −5…−10 (§5.1, E5).
4. **Rigid stair cast-in and floor-through party wall**: flight bonded to wall
   67 dB; floors through the split couple leaves into one mass (§6.6, §5.3).
5. **Weakest small element kills the façade mix**: shutter box 28 dB at 1 m²,
   open vent, jointed old box window replaced by "better" modern window that
   *fails* (S11: 42,9 → 40,0 < 41,5) — always recompute R′w,ges after swaps (§10.1, E3).
6. **Decoupling an edge that didn't need it**: K_E −3…−6 dB on light separators
   (§4.4) while flanks were already fine (S57) — spend the detail where K_ij ≤ R+10.
7. **Pipes/boxes in the separating element or screed**, mortar slurry through
   open-cell sleeves, mounting boxes in party walls (§12.1).
8. **Overstated single number**: quoting R_w without C/Ctr in a traffic area;
   mixing VDI 4100 D_nT,w targets with DIN 4109 R′w proofs (§7.4 conversions).
9. **Geometry-blind proof reuse**: one flanking computation cloned to shallow
   rooms where R′w,req rises to 63 (§7.4).
10. **Room acoustics: reflective box treated as "done"** — no absorber → T_soll
    missed → teachers' voice levels climb (Lombard) → Kita/classroom complaint
    (E6; §11.4).

## 16. Verification checklist (before issuing any acoustic note)

- [ ] Edition years stated (DIN 4109-1/-2/-3x, 18041, TA Lärm/BImSchV); re-confirm
      every VERIFY tag here against the current norm.
- [ ] Requirement basis (public vs contractual) agreed; Vorhaltemaß +2 / doors +5 /
      impact −3 applied; comparisons at 0,1 dB.
- [ ] Room geometry inputs (S_s, l_f, V, S/S_G) listed per computed pair; conversions
      D_nT,w ↔ R′w stated with the room they belong to.
- [ ] K_ij per joint from §7.2 formulas with M shown; offsets/kinks handled;
      decoupled details checked against K_ij,min.
- [ ] Flanking masses & front shells: f₀ of every Vorsatzschale/screed/ETICS
      computed and < 100 Hz (or the ΔR penalty taken).
- [ ] Façade: L_a build-up (sources, +3, day/night rule), mixture computed incl.
      boxes, joints, vents; window product rating carries the install margin &
      C_tr checked for traffic spectra.
- [ ] Impact: bare-slab level, ΔL_w curve chosen at *installed* s′ (creep noted),
      bridge list (§6.4) closed out on details, stairs detailed per §6.6.
- [ ] Equipment: group-I fittings where plan unfavourable, shaft masses, plant-room
      vents with silencers, HP/CHP siting; VDI 4100/DEGA promises stated in the
      contract if above DIN 4109-1.
- [ ] Room acoustics: T_soll formula + V band correct; A table sums in occupied
      state; Δl ≤ 17 m speech paths or absorbers on offending surfaces;
      L_NA budget consistent with §8 equipment limits.
- [ ] Outdoor immission: correct ordinance for the source (TA Lärm vs 16. BImSchV),
      quiet-hours/peak rules, reference point 0,5 m at open window; LDEN used only
      where the strategic-mapping regime applies.
- [ ] Measurement plan for risky units (in-situ R′w, L′nT,w, services L_AF,max,n —
      site checks cannot be replaced by the calculation, §1.4); sibling interfaces
      flagged: fire conflicts (resilient stair coverings, intumescent vs acoustic
      joint fill), thermal-break details at acoustic separations, window
      airtightness vs R_S.

*End of skill. Values carry the tier/VERIFY discipline of §2: when a number is
decisive for a signed proof, open the norm edition and re-derive it there.*
