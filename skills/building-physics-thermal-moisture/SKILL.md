---
name: building-physics-thermal-moisture
description: >
  Steady-state and hygrothermal verification of opaque building elements and
  windows for DACH/European practice: heat protection (Wärmeschutz) with
  R/U/λ/ψ calculations per DIN EN ISO 6946, surface resistances, design thermal
  conductivity values, inhomogeneous build-ups, air layers, inverted-roof and
  fastener corrections, thermal-bridge linear transmittance (Ψ) auditing with
  fRsi temperature-factor and mould criteria (DIN 4108-2), GEG new-build and
  existing-building U-value checks for walls, roofs, floors, windows (Uw/ Ug/
  Uf/ψg, g-value) and doors; moisture protection (Feuchteschutz) with
  psychrometrics, dew-point and condensation-plane location, sd-value vapour
  design, Glaser method (DIN 4108-3) with condensation limits and drying
  reserves, capillary water uptake, wind-driven rain exposure groups,
  terrarium-effect (Terrarien-Effekt) trapping warnings; airtightness
  (Luftdichtheit) n50 targets and
  blower-door practice (EN ISO 9972, DIN 4108-7), summer heat protection
  (sommerlicher Wärmeschutz) via solar-gain index S with Sonneneintragskennwerte
  S1–S6 and F_C shading factors or dynamic simulation limits, roof-specific
  vapour physics (warm/inverted/ventilated, ZVDH underlay classes), ground
  transmission (DIN EN ISO 13370 simplified), plus worked numeric verification
  examples the agent can replicate line by line.
---

# Building Physics: Heat & Moisture Protection (Bauphysik: Wärme- und Feuchteschutz)

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

Use this skill when the agent must check, design-verify, or explain the thermal
and hygric behaviour of an opaque building element, window, roof, or above/below-
grade assembly: U-value compliance (GEG / DIN 4108-2 Mindestwärmeschutz), thermal
bridges and Ψ values, interior surface temperature and mould risk (fRsi,
12.6 °C criterion), interstitial condensation by Glaser method, vapour-control
layer and sd placement, airtightness (n50, blower door, DIN 4108-7 detailing),
summer overheat proof (S-index / F_C / simulation limits), wind-driven rain,
capillary moisture, and ground heat transfer. Trigger also on layer-buildup
review requests ("is there a dew point in this wall?"), retrofit insulation
sizing, window Uw assembly, or when a roof/wall section is proposed without a
stated moisture strategy.

Sibling skills (call them, do not duplicate their scope):
- building-acoustics — airborne/impact sound, DIN 4109 proofs (mass law, flanking).
- fire-protection-building — reaction/fire-resistance classes, compartments, escapes.
- roofing-waterproofing — waterproofing layer rules, detailing of seals, gutters.
- building-materials — product data, λ/μ only as material properties, not proofs.
- construction-detailing — joint grammar, layer continuity, three-stage sealing.
- structural-systems — load paths, bracing, dimensioning of the structure itself.
- construction-freecad-bim — geometry, sections, IFC export (see handoff section).

Units convention: λ [W/(m·K)], R [m²K/W], U [W/(m²K)], Ψ [W/(m·K)], χ [W/K],
sd [m], μ [−], moisture content u [M-%], capillary coefficient W [kg/(m²·h^0.5)],
vapour pressure p [Pa], temperatures θ [°C]. German term in parentheses at first
use of each concept; numeric values always with the tier tag from the next table.

## Reality check — not a construction document

1. The agent produces **planning and calculation aids** (Planungs-/Nachweishilfen),
   not enforceable construction documents. Every output of this skill must be
   labelled as such when it leaves the chat or a model.
2. The statutory energy proof (energetischer Nachweis, GEG) requires a
   **zugelassenes Verfahren** (accepted calculation procedure, e.g. DIN V 18599
   or DIN V 4108-6/4701-10 as far as still permitted) executed and, where the
   Land law demands it, signed by a **licensed Energieberater / Fachunternehmer**.
   A hand-run U-value or S-index check from this skill is a pre-check, never the
   proof itself.
3. **GEG and DIN text in force at project date prevails** over every number in
   this file. The digests behind these values contain flagged editions
   (DIN 4108-2:2013-02, DIN 4108-3:2014-11, GEG 2020/amendments). Values marked
   VERIFY must be re-checked in the current norm/regulation text before use.
4. When the user treats agent output as final ("das ist dann unser Nachweis"),
   the agent must state explicitly: planning aid only; proof requires accepted
   procedure + licensed practitioner; current GEG/DIN text prevails; this check
   used flagged edition values.
5. Condensation, mould, and airtightness verdicts from stationary methods
   (Glaser, fRsi) carry method limits (stationary climate, constant properties,
   no construction moisture). For internal insulation, flat roofs, timber
   structures near risk thresholds, the honest answer is: stationary tier passed
   or failed — confirm with transient coupled heat-moisture simulation
   (DIN EN ISO 15026 tools of WUFI/DELPHIN class) before deciding.

## Evidentiary tiers (never mix tiers in one number chain)

| Tier | Status | Examples (this skill) |
|------|--------|------------------------|
| T1 | Law / legally-binding energy & safety requirements | GEG (§26 airtightness, §49 ff. requirements, Referenzgebäude), DIN 4108-2 Mindestwärmeschutz via Baurecht (Technische Baubestimmungen), Landesbauordnungen, EnEV-history flags |
| T2 | DIN/EN calculation methods and tabulated design inputs | DIN EN ISO 6946 (R/U), 10211 (bridge numerics), 13788 (surface humidity), 10456 (λ/μ design), DIN 4108-3 (Glaser/period balance), DIN 4108-4/-6, DIN EN ISO 10077 (windows), 13370 (ground), 13786/13793, DIN V 18599 |
| T3 | Recognised practice values (rules of technique / trade sheets) | DIN 4108 Bbl. 2 planning examples, ZVDH Fachregeln/Produktdatenblätter, WTA-Merkblatt-style values, DIN 4108-7 material classification, window class tables DIN EN 12207 |
| T4 | Rules of thumb (only for plausibility, never for proof) | "1 cm good insulation ≈ 15 cm brick", Ψ≈0.05 typical bad junction, "U ≤ 0.28 beats most retrofit caps", 12.6 °C memory value |

Mixing rule: a T1 limit (e.g. GEG U ≤ 0.20 roof) may be checked with T2 methods
(ISO 6946) and T2/T3 input data (DIN 4108-4 λ_B), but a T4 estimate never
closes a T1 requirement. If the only available number is T4, say so in the
output.

## 1. Steady-state heat transfer (Wärmeleitung) — core calculation

### 1.1 Quantities and formulas (T2, DIN EN ISO 6946)

- Heat flow rate: Φ = Q/t [W]; flux density q = Φ/A [W/m²].
- Layer conduction: q = λ·(θ₁−θ₂)/d = Δθ/R_i, with **R_i = d_i/λ_i** [m²K/W].
- Multi-layer (homogeneous layers): R = Σ R_i.
- Total resistance: **R_T = R_si + Σ(d_i/λ_i) + R_se**.
- **U = 1/R_T [W/(m²K)]** (U-Wert, Wärmedurchgangskoeffizient).
- Whole element: q = U·(θ_i − θ_e); surfaces: q = h_i(θ_i−θ_si) = h_e(θ_se−θ_e).
- Round R_T and U to 2 decimals (DIN 4108-2 convention).
- Temperature at depth x: θ_x = θ_i − q·(R_si + Σ d_x/λ) — proportional-drop
  method; graphical alternative: plot θ over cumulative R, straight line from
  θ_i (R=0) to θ_e (R=R_T); intermediate layer temps read at R boundaries.
- Transient material response (context only): diffusivity a = λ/(ρ·c_p) [m²/s];
  effusivity (Wärmeeindringkoeffizient) b = √(λ·ρ·c_p); low a ⇒ slow
  temperature wave (good phase shift: low λ, high ρ·c_p).

### 1.2 Surface coefficients / resistances (T2)

Convective design coefficients (ISO 6946): h_ci = 5.0 (heat flow upward),
2.5 (horizontal), 0.7 W/(m²K) (downward); exterior h_ce ≈ 4·v̄^0.4 (v̄ wind m/s);
radiative h_r = ε·h_ro with h_ro (blackbody): −10 °C→4.13, 0→4.61, 10→5.10,
20→5.70, 30→6.31, 40→6.95, 50→7.64, 60→8.37 W/(m²K). ε ≈ 0.9 for most
non-metallic materials (bright Al 0.05–0.07, polished Cu 0.03 — reflective foils
work only with enclosed air gap).

Standardized surface resistances R_s = 1/(h_c+h_r) [m²K/W]:

| Situation | R_si (interior) | R_se (exterior) | Tier/note |
|-----------|-----------------|-----------------|-----------|
| Heat flow upward (roof) | 0.10 | 0.04 | T2 ISO 6946 |
| Horizontal (wall, heat flow sideways) | 0.13 | 0.04 | T2 ISO 6946 |
| Heat flow downward (floor) | 0.17 | 0.04 | T2 ISO 6946 |
| Against ground / earth-coupled face | per direction (0.17/0.13/0.10) | 0 | T2 |
| Thermal-bridge & mould checks (DIN 4108-2) | **0.25** | 0.04 | T1/T2 boundary value |
| Moisture verification Glaser (DIN 4108-3) | **0.25** | 0.04 | T2 |
| Glazing / window frame surfaces | 0.13 (up 0.10 / down 0.17) | 0.04 | T2 13788/10077 |
| Behind built-in (sealed-back) furniture | 1.0 | — | T2 DIN 4108-8 |
| Behind free-standing furniture | 0.5 | — | T2 DIN 4108-8 |
| Strongly ventilated air layer replaces layer | — | use R_si value on that face | T2 ISO 6946 |

R_si = 0.25 is the **verification-only** value (slow surface convection assumed
for hygrothermal checks); U-values for energy law use 0.10/0.13/0.17. Never mix
the two in one chain. Unheated adjacent space: R_se of that face = R_si of the
unheated space; or use F_x temperature correction (thermal-bridge section) —
but never both Ru-method and F_x-method together (double count).

### 1.3 Design thermal conductivity λ_B and moisture rule (T2, DIN 4108-4 / DIN EN ISO 10456)

Design values (Bemessungswerte) refer to hygroscopic equilibrium moisture at
23 °C / 80 % RH. Conversion from declared λ_D per material family
(footnote rules captured in digests):

- λ_B = λ_D·1.03, min +1 mW/(m·K): MW, EPS, XPS, PUR, PF, CG, EPB, WW, WF, in-situ MW, EP in-situ.
- λ_B = λ_D·1.05 min +2; ·1.10 min +3 (PUR/PIR spray & dispensed EN 14315/-18: 0.020→0.023 … 0.040→0.044); ·1.20 (vermiculite EN 14317, PEF EN 16069); ·1.23.
- Metal-faced sandwich (EN 14509): U_B = U_D·1.03.
- Quartz-sand note: +20 % λ for 2-chamber, +15 % for 3–6-chamber hollow blocks.

### 1.4 λ / μ / c_p table — common materials with design densities (T2, DIN 4108-4 style; μ dry/wet where given)

| Material (DE) | ρ [kg/m³] | λ [W/(m·K)] | c_p [J/(kg·K)] | μ [−] |
|---------------|-----------|-------------|----------------|-------|
| Kalk-/Kalkzementputz (lime/lime-cement plaster) | 1800 | 1.0 | 1000 | 15/35 |
| Gipsputz (gypsum plaster) | 900→1500 | 0.30→0.56 (≈+0.045 per +100) | 1000 | 4/10 |
| Leichtputz (light plaster) | ≤1300/≤1000/≤700 | 0.56/0.38/0.25 | 1000 | 15/20 |
| Zementmörtel (cement mortar) | 2000 | 1.6 | 1000 | 15/35 |
| Normalmörtel / Dünnbett (mortar NM/DM) | 1800/1600 | 1.2/1.0 | 1000 | 15/35 |
| Zementestrich (cement screed) | 2000 | 1.4 | 1000 | 15/35 |
| Gussasphalt (cast asphalt screed) | 2300 | 0.90 | 1000 | sd ≥ 1500 m |
| Beton / RC (concrete, 1–2 % steel) | 2200–2400 | 1.65–2.5 | 1000 | 80/130 |
| Porenbeton, Planstein (AAC) | 350→800 | 0.11→0.23 (500→0.14, 600→0.18) | 1000 | 5/10 |
| Vollziegel (solid clay brick) | 1800–2400 | 0.81–1.40 | 1000 | 5/10 |
| Verblendziegel/Klinker (facing/clinker) | 1800–2400 | 0.81–1.40 | 1000 | 50/100 |
| Hochlochziegel HLzA/B, LM mortar (hollow brick) | 550→1000 | 0.27→0.40 (LM) / 0.32→0.45 (NM) | 1000 | 5/10 |
| Kalksandstein (sand-lime, unperforated) | 1600–2000 | 0.79–1.1 | 1000 | 15/25 |
| Betonstein Hohlblock Gr.1 (CHB group 1) | 600–1600 | 0.24 (LM21) –0.74 | 1000 | 5/10 |
| Naturstein kristallin (granite/basalt) | 2800 | 2.8–3.5 | 1000 | 10⁴ |
| Sandstein (sandstone) | 2600 | 2.3 | 850 | 30/40 |
| Kalkstein (limestone soft→hard) | 1600–2600 | 0.85–2.3 | — | 150–250 |
| Nadelholz konstruktiv (softwood) | 450 | 0.12 | 1600–1700 | 20/50 |
| Holz 700 (hardwood-class) | 700 | 0.18 | 1600 | 50/200 |
| OSB | 650 | 0.13 | 1600–1700 | 30/50 |
| Sperrholz (plywood) | 500→1000 | 0.13→0.24 | — | 70/200…110/250 |
| Spanplatte (chipboard) | 600 | 0.14 | 1700 | 15/50 |
| Holzweichfaser WDHF/MDF (wood fibre) | 250→800 | 0.07→0.18 | 1700–2000 | 1/3–20/30 |
| Gipsfaserplatte (gypsum-fibre) | 1000 | 0.34 | 1000 | 4/10 |
| Gipskarton GK (plasterboard) | 700→900 | 0.21→0.25 | 1000 | 4/10 |
| Mineralfaser MW (mineral wool) | 10–200 | λ_D+1 mW: 0.031…0.052 | 1030 | 1 |
| EPS (expanded polystyrol) | 15–30 | 0.031…0.052 (design) | 1300–1450 | 20/100 |
| XPS (extruded polystyrol) | 25–65 | 0.023…0.046 (design) | 1450 | 80/250 |
| PUR/PIR (polyurethane) | 28–60 | 0.021…0.041 (design) | 1400 | 40/200 |
| Phenolharz PF (phenolic foam) | 25–60 | 0.021…0.036 | 1400 | 10/60 |
| Schaumglas CG (foam glass) | 100–160 | 0.038…0.057 | 1000 | ∞ |
| Kork gebläht ICB (expanded cork) | 100–140 | 0.040…0.058 | 1560 | 5/10 |
| Holzholzwolle WW (wood-wool board) | 250–450 | 0.063…0.105 | 1470 | 2/5 |
| Zelluloseflockung loose (cellulose) | 20–60 | 0.035–0.042 | 1600 | 1–2.2 (u23,80 = 18 M-%) |
| Bitumenschweißbahn (bitumen sheet) | 1200 | 0.17 | 1000 | 2·10⁴ |
| Dachziegel (clay tile) | 2000 | 1.0 | 800 | 30/40 |
| Betondachstein (concrete tile) | 2100 | 1.5 | 1000 | 60/100 |
| Glas (float) | 2500 | 1.0 | 750 | ∞ |
| PVC-Weichfolie d=1.2–2 mm (membrane) | 1200–1400 | 0.17–0.25 | 900 | ≈10⁴–10⁵ (sd by type) |
| EPDM/FPO Dachbahn (single-ply) | 1150–1200 | 0.25 | 1000 | ≥10⁴ |
| Stahl (steel) | 7800 | 50 | 450 | ∞ |
| Edelstahl austenitisch (stainless) | 7900 | 17 | 500 | ∞ |
| Aluminium | 2800 | 160 | 880 | ∞ |
| Kupfer (copper) | 8900 | 380 | 380 | ∞ |
| Wasser 10–80 °C / Eis 0 °C / Schnee | 1000/900/100–500 | 0.60–0.67/2.2/0.05–0.6 | 4190/2000/2000 | — |
| Luft still (still air) | 1.23 | 0.025 | 1008 | 1 |
| Boden: Kies trocken/gesättigt | 1800–2200 | 0.4/1.8 | — | 50 |
| Boden: Sand trocken/dampfe/gesättigt | — | 0.4–0.7/1.4/2.4 | — | 50 |
| Boden: Ton schluffig trocken/gesättigt | 1200–1800 | 0.5–1.5/1.7 | 1670–2500 | 50 |
| Fels (rock) / generischer Bodenansatz (ISO 13789) | — | 3.5 / 2.0 | — | — |

Membrane sd values (T2, ISO 10456 measurement practice): PE-foil 0.15 mm→50 m;
PE 0.25→100; 3×PE 0.15→8 m (staggered); polyester 0.2→50; Al-laminate 0.4→10;
Al-foil 0.05→1500; diffusion-open roof membrane on walls→0.2; paint coat→0.1;
gloss varnish→3; vinyl wallpaper→2; PVC foil→30; bitumen paper 0.1→2.
Humidity-variable (smart) membranes: μ varies with RH (EN 13984) — must be
modelled at both dry and wet value.

μ selection rule for Glaser (T2, DIN 4108-3): use the **unfavourable** split —
small μ from interior side to condensation plane, large μ from plane to
exterior. Porous materials under stationary conditions: dry values per
ISO 15148 logic; for periodic balance use wet/critical column.

## 2. Special U-value cases (T2)

### 2.1 Inhomogeneous build-ups (studs, rafters, columns) — ISO 6946 limit method

For bays + ribs (e.g. timber frame f_stud, rafter roof f_ribs):
- Upper limit (parallel heat flow paths, 1D each): R′T = 1 / Σ(f_q / R_Tq).
- Lower limit (isothermal layers): **R″T = R_si + Σ_j [1 / Σ_q (f_q/R_j,q)] +
  R_se**, R_j,q = d_j/λ_j,q per layer-path — each layer's resistance formed.
- Mean: digest examples use **R_T = (R′T + R″T)/2**; the DIN EN ISO 6946:2008 wording records
  the ISO 6946:2008 weighting **R_T = (R′T + 2·R″T)/3** — flag: use the method
  (and weighting) of the edition named in the current project's proof; state
  which was applied. VERIFY.
- Simplified averaging NOT allowed if R′T/R″T > 1.5, or if insulation
  inhomogeneity is caused by **metallic** elements → 2D/3D numerical per
  DIN EN ISO 10211. (Edition note: some editions allow the upper bound
  shortcut up to ratio < 3.) VERIFY.
- Worked anchors (digest): pitched roof f_ribs=0.11: R_Ta=1.651, R_Tb=4.991 →
  R′=4.083, R″=3.940, ratio 1.04 → R_T=4.011 → U=0.25. Skeleton wall with
  concrete column strip f_col=0.05: R_Ta=2.335/R_Tb=4.215 → R′=4.052,
  R″=2.881, ratio 1.41 → R_T=3.467 → U=0.29 (vs 0.25 pure insulated strip —
  the stiffness bridge penalty is real).

### 2.2 Air layers (T2, ISO 6946; applies d ≤ 30 cm, < 0.1× other dimension, no exchange with room air, ε ≥ 0.8)

Classification by opening cross-section to outdoor air: still (ruhend)
A ≤ 500 mm² per m (vertical) / per m² (horizontal); weakly ventilated
500 < A < 1500 mm²; strongly ventilated ≥ 1500 mm². Weakly: R = (R_still +
R_vent)/2. Strongly: **omit the air layer and every layer outboard of it**;
replace R_se by the elevated value (may use R_si). Weep holes of a masonry
outer leaf ≠ ventilation opening.

Still-air layer resistance R_g [m²K/W] by thickness (up / horizontal / down):
5 mm 0.11/0.11/0.11 · 7 mm 0.13 · 10 mm 0.15 · 15 mm 0.16/0.17/0.17 ·
25 mm 0.16/0.18/0.19 · 50 mm 0.16/0.18/0.21 · 100 mm 0.16/0.18/0.22 ·
300 mm 0.16/0.18/0.23 (linear interpolation; convection onset caps upward).

### 2.3 Waterproofed components, inverted roofs, perimeter insulation

- Waterproofed elements (T1/T2 DIN 4108-2): count R, R_T, U **only for layers
  on the dry (warm) side** of the membrane; wet-side layers normally neglected.
  Earth-contact elements for Mindestwärmeschutz use a "konstruktiver
  Wärmedurchlasswiderstand" computed per ISO 6946 (deviating from ISO 13370
  detailed ground methods).
- Umkehrdach / inverted roof (insulation above waterproofing): only closed-cell
  XPS (EN 13164) or foam glass (EN 13167) per DIN 4108-10 counts; add runoff-
  cooling surcharge ΔU (T1, DIN 4108-2): share of insulation R below/above
  logic — room-side R below membrane ratio (R_T−R_i)/R_T: <10 % → ΔU = 0.05;
  10–50 % → 0.03; >50 % → 0.00 W/(m²K). Lightweight roofs (areal mass
  < 250 kg/m²) require R ≥ 0.15 m²K/W below the membrane. ΔU = 0 allowed only
  for approved systems with water-draining separation layer.
- Perimeterdämmung (PW/PB on the waterproofing side): XPS/foam glass count
  toward U; excluded: under foundation slabs (Bodenplatten) and surfaces
  exposed to groundwater or long-standing water.
- Wedge-shaped layers (falls ≤ 5 %): ISO 6946 Annex E average/logarithmic
  method; worked case: R_Keil = (d₂/λ)·ln((d₁+d₂)/d₁): 2 % single-side
  drain over 4.0 m adds 8 cm apex → minimum thickness must grow to keep U
  (lesson: single drainage needs thicker insulation than double).
- Fasteners penetrating insulation (T2, ISO 6946 Annex F): ΔU = ΔU_g + ΔU_f +
  ΔU_r; apply only if total ΔU > 3 % of U. ΔU_g air-gap grades: 0 (sealed/
  tongue-groove) → 0.00; grade 1 (butt joints >5 mm, no circulation) → 0.01;
  grade 2 (circulation possible, gaps through insulation) → 0.04 W/(m²K).
  ΔU_f = n_f·A_f·(λ_f−λ_W)/d_0 × reduction factor with (R₁/R_T)²-type weighting
  (a = 0.8 full penetration; VERIFY exact Annex F.2 form). Skip for: masonry
  anchors over air space, fixings λ < 1.0, plates both ends. Digest anchor:
  Ø6.3 steel dowels, 2.78/m² through 14 cm EPS → ΔU_f ≈ +0.02 W/(m²K) on a
  U = 0.25 build-up (~8 % penalty) — WDVS plug allowance must be checked.
- Unventilated roof space (T2, ISO 6946): R_u (incl. construction) tiles
  without felt 0.06; tiles+felt 0.20; +low-ε soffit 0.30; boarding+felt 0.30
  m²K/W. Other unheated rooms: R_u = A_i/(Σ U_e·A_e + 0.33·n·V/A_i); defaults
  U_e = 2.0, n = 3 h⁻¹. Alternative: F_x with R_se = R_si — never both.
- DIN 4108-4 slab (decke) R average/worst-point catalogue exists for ribbed,
  hollow-core, brick-infill decks (e.g. RC ribbed 200 mm: R 0.24/0.10;
  hollow-core 100 mm: 0.15/0.05) — use table values, not 1D calc, for
  unreinforced-rib decks. VERIFY edition.

**Generic material-property cross-check** (non-edition-specific; Neufert, *Architects' Data*
(Neufert_2002.pdf excerpt), p.114): thermal resistance 1/Λ [m²K/W] by construction thickness for
unplastered reinforced-concrete and hollow-clay-block floor systems, given as (average value in
the field / worst-point value through the rib or web) — a physical-property cross-check against
the DIN 4108-4 catalogue above, not a substitute for it. **VERIFY every row against the current
DIN 4108-4 material table before quoting in a deliverable** (source predates current editions and
is a UK/international handbook digest, not a DIN table):

| Floor system (unplastered) | Thickness (mm) | 1/Λ average (m²K/W) | 1/Λ worst point (m²K/W) |
|---|---|---|---|
| RC ribbed floor (Rippendecke) | 120 / 140 / 160 / 180 / 200 / 220 / 250 | 0.20 / 0.21 / 0.22 / 0.23 / 0.24 / 0.25 / 0.26 | 0.06 / 0.07 / 0.08 / 0.09 / 0.10 / 0.11 / 0.12 |
| RC beamed floor (Balkendecke) | 120 / 140 / 160 / 180 / 200 / 220 / 250 | 0.16 / 0.18 / 0.20 / 0.22 / 0.22 / 0.24 / 0.28 | 0.06 / 0.07 / 0.07 / 0.08 / 0.09 / 0.09 / 0.10 |
| Hollow clay blocks, no cross webs | 115 / 140 / 165 | 0.15 / 0.16 / 0.18 | 0.06 / 0.07 / 0.08 |
| Hollow clay blocks, with cross webs | 190 / 225 / 240 / 265 / 290 | 0.24 / 0.26 / 0.28 / 0.30 / 0.32 | 0.09 / 0.10 / 0.11 / 0.12 / 0.13 |
| RC + hollow clay blocks, partly grouted joints | 115 / 140 / 165 / 190 / 225 / 240 / 265 / 290 | 0.15 / 0.18 / 0.19 / 0.24 / 0.27 / 0.30 / 0.33 / 0.36 | 0.06 / 0.07 / 0.08 / 0.09 / 0.10 / 0.11 / 0.12 / 0.13 |
| RC + hollow clay blocks, fully grouted joints | 115 / 140 / 165 / 190 / 225 / 240 / 265 / 290 | 0.13 / 0.16 / 0.19 / 0.22 / 0.25 / 0.28 / 0.31 / 0.34 | 0.06 / 0.07 / 0.08 / 0.09 / 0.10 / 0.11 / 0.12 / 0.13 |
| RC hollow beams (unplastered) | 65 / 80 / 100 | 0.13 / 0.14 / 0.17 | 0.03 / 0.04 / 0.05 |

Reading: "average" is the field value including the insulating effect of the hollow block/void;
"worst point" is the value through the solid rib/web alone (no block credit) — the same
average/worst-point split the DIN 4108-4 catalogue above uses, so the two sources cross-check
row-for-row where constructions coincide (e.g. RC ribbed floor ≈ 200 mm lands at 0.24/0.10 in
both digests).

## 3. U-value requirements, targets and minimum thermal protection

### 3.1 GEG new-build reference level (T1, GEG 2020 Referenzgebäude; VERIFY current GEG/BEG-era text — amendments 2024+ shift these)

Reference-building component U-values (Wohngebäude, GEG Anlage 1 Table 1 row set):

| Element | U_ref [W/(m²K)] | g⊥ note |
|---------|-----------------|---------|
| External wall (incl. roof-integrated wall) | 0.28 | — |
| Wall/ceiling against ground or unheated | 0.35 | — |
| Roof / top-floor ceiling | 0.20 | — |
| Window (vertical) | 1.3 | g⊥ 0.60 |
| Roof window | 1.4 | 0.60 |
| Glass roof / light band | 2.5 (dome 2.7) | 0.63/0.64 |
| Door | 1.8 | — |
| Thermal-bridge allowance ΔU_WB | 0.05 | (Bbl-2 quality assumed) |

- Primary-energy main requirement: Q_P ≤ 0.55 × Q_P,Ref (residential) per the
  energy-law capture; a second capture records 0.75 × Ref for DIN
  V 18599:2018-09 residential procedure — conflicting edition capture,
  **VERIFY the factor against current GEG §109/Anlage text before quoting**.
- Nebenanforderung residential: specific transmission heat loss
  H′_T ≤ 1.0 × H′_T,Ref (= reference level ≈ 0.28 W/(m²K) class).
- Non-residential mean-U ceiling (T1, GEG Anlage 3, zones ≥19 °C / 12–<19 °C):
  opaque 0.28/0.50 · transparent 1.5/2.8 · curtain wall 1.5/3.0 · glass
  roofs/light bands/domes 2.5/3.1 W/(m²K); ground/unheated-weighted ×0.5;
  slab area beyond 5 m from edge ignorable. Reference U (Anlage 2): wall 0.28
  (0.35), curtain wall 1.4 g 0.48 (1.9 g 0.60), roof 0.20/0.35, window 1.3/1.9,
  door 1.8/2.9, ΔU_WB 0.05/0.10.
- Extensions/additions > 50 m² connected usable area: full new-build level on
  the new envelope (H′_T ≤ 1.2× Ref residential; non-res mean U ≤ 1.25× limit),
  summer heat proof mandatory.

### 3.2 Existing-building retrofit limits (T1, GEG Annex 7 / §49 ff.; VERIFY current table)

Changed components must meet (19 °C use / 12–<19 °C bracket):

| Measure | U_max [W/(m²K)] |
|---------|------------------|
| External wall (replacement or first insulation; cladding/re-render) | 0.24 (0.35) |
| Window to outdoors | 1.3 (1.9) |
| Roof window | 1.4 (1.9) |
| Glazing-only replacement | U_g ≤ 1.1 (box windows: IR-coating ε ≤ 0.2; if thickness-limited U_g ≤ 1.3) |
| Curtain wall | 1.5 (1.9); special glazing 2.3/3.0 |
| Glass roof | 2.0 (2.7) |
| Lift-slide door | 1.6 (1.9) |
| Special glazing (R′w ≥ 40 dB, bullet, fire ≥18 mm) | element 2.0 (2.8); glass only 1.6 |
| External door | 1.8 (leaf) |
| Roof / top-floor ceiling | 0.24 (0.35) |
| Flat roof when waterproofing replaced | 0.20 (0.35) |
| Wall against ground/unheated | 0.30 |
| Floor build-up (warm side) | 0.50 |
| Ceiling against outdoors (replacement) | 0.24 (0.35) |

- Thin-layer rule where build-up thickness is limited (heritage façade etc.):
  λ ≤ 0.035 (blown/renewable insulation 0.045) with max practical thickness.
- Overall relaxation: compliance group alternative if Q_P and H′_T do not
  exceed maxima by more than **40 %** (existing buildings, GEG Teil 3 logic);
  H′_T caps (EnEV-era table, VERIFY): detached A_N ≤ 350 m² → 0.40; >350 →
  0.50; terraced/duplex → 0.45; other → 0.65 W/(m²K).
- De-minimis: measures up to 10 % of a component group are exempt.
- Small buildings ≤ 50 m² heated area: first-installation U values suffice.

### 3.3 DIN 4108-2 Mindestwärmeschutz (T1 via Baurecht; surface-condensation floor, edition-flagged)

Applies rooms ≥ 19 °C (low-heated 12–<19 °C: wall R ≥ 0.55). Minimum
Wärmedurchlasswiderstand R_min [m²K/W], heavy elements (m′ ≥ 100 kg/m²):

| Junction | R_min |
|----------|-------|
| Wall vs outdoor air / ground / garage / unheated room | 1.2 (low-heated ≥ 0.55) |
| Sloped roof vs outdoor air | 1.2 |
| Flat roof / top-floor ceiling vs outdoor air | 1.2 |
| Ceiling vs ventilated space between slopes & knee wall | 0.90 |
| vs unheated/crawlable roof space | 0.90 |
| vs space between insulated slopes & knee walls | 0.35 |
| Floor slab vs outdoor air / garage / passage / ventilated crawl | 1.75 |
| Floor vs unheated cellar | 0.90 |
| Slab on ground (occupied, ≤ 5 m depth) | 1.75 |
| Flat party wall / room divider between heated rooms | 0.07 |
| Apartment separation floor | 0.35 |

Light elements (m′ < 100 kg/m²) and frame/skeleton: light external wall & roof
1.75; skeleton infill (Gefach) 1.75; component mean 1.0; roller-shutter box
mean 1.0 / lid 0.55; opaque panels of transparent elements 1.2 (U_f ≤ 2.9).
Inadmissible without extra insulation: cantilevered balconies, parapets, free
columns, walls λ > 0.5 running into uninsulated roof/outdoor air.
Newer DIN 4108-2 editions flag: fRsi criterion raised to 0.71/0.67
by class and R_min values restructured — **VERIFY edition in force**.

## 4. Thermal bridges (Wärmebrücken) — Ψ, χ, fRsi

### 4.1 Definitions and balance term (T2, DIN EN ISO 10211 / 14683)

- Ψ [W/(m·K)]: linear thermal transmittance of a 2D line bridge; χ [W/K]:
  point bridge (3D). Ψ = excess heat flow over undisturbed 1D flow at the
  junction: Ψ = L_2D − Σ(U_k·A_k/l) with the 1D reference terms taken at the
  GEG **outer dimensions of the system boundary** → negative Ψ is possible and
  legitimate (e.g. ridge, external corner).
- Types: geometric (Kühlrippen/fin effect at corners, projections) vs
  constructive (material change: window-head, slab penetration); convective and
  radiation-induced effects also exist. Bridges are physically unavoidable —
  not a defect per se, but they lower interior surface temperature and raise
  loss. Absolute Ψ alone does not rate quality (thick insulation + bad detail
  can show high Ψ with low total loss); compare to catalogue/Beiblatt values.
- Envelope transmission balance (T1/T2): H_T = Σ(U_i·A_i·F_x,i) + H_WB;
  H_WB = Σ Ψ_j·l_j = ΔU_WB·A. Flat-rate options (GEG/DIN V 18599, VERIFY
  current values): 0.10 W/(m²K) without any proof; 0.15 with internal
  insulation + bonded solid floors (>50 % wall area); **0.05** if relevant
  junctions follow DIN 4108 Bbl. 2 (2019-06) examples (category A) with
  equivalence proof; **0.03** if all junctions per category B; or exact ΣΨ·l
  by ISO 10211 numerics. Equivalence proof may be waived where adjoining
  components already beat the Musterlösung U values (GEG/DIBt note).
- Simplified indicative Ψ catalogue: DIN EN ISO 14683 (T2); for the energy
  balance only Ψ based on the reference conditions of the claimed catalogue
  may be used (Beiblatt-2 conditions for equivalence proof); inner-dimension
  values must be converted before GEG use.

### 4.2 Numerical model rules (T2, DIN EN ISO 10211)

- Model = flanking elements + central bridge element. **1-Meter-Regel**: cut
  planes ≥ 3× flanking thickness AND ≥ 1 m from the bridge; extend/skip zones
  disturbed by windows, ribs. **Symmetrie-Regel**: symmetry planes allowed for
  repeating elements (window axes, stud bays).
- Ground cut-plane distances (model rules): horizontal-to-vertical inside
  ≥ 3× wall d (surface temp) / 0.5× floor dimension (heat flow); outside
  ≥ 3× d / 2.5× floor width; vertical below ground surface ≥ 3 m / 2.5× w;
  if floor > 2 m below grade ≥ 1 m / 2.5× w. Isotherms parallel, adiabats
  perpendicular at the cut.
- Two calculation purposes: (a) surface temperature → fRsi; (b) heat flow →
  L_2D [W/(mK)] / L_3D [W/K].
- IR thermography: qualitative only — no quantitative Ψ; relative Δθ to few
  tenths K, absolute ± ~2 K; interpretation depends on ε, reflections,
  convection.

### 4.3 Temperature correction factor F_x (T2, DIN V 4108-6/18599-2; same tables both purposes)

θ_x = θ_e + F_x·(θ_i − θ_e). F_e = 1.0 for wall/window/roof vs outdoor air and
roof as boundary; top-floor ceiling over uninsulated attic 0.8; knee-wall rooms
(Drempel/Abseiten) 0.8; walls/ceilings to unheated rooms (not cellar) 0.5;
low-heated rooms (12–19 °C) 0.35; unheated glass annex: single glazing 0.8,
double IGU uncoated 0.7, coated/argon multi-glazing 0.5. Ground-coupled F_x
depends on R and B′ (see ground section table §9.2).

### 4.4 Interior surface temperature, condensation, mould criterion (T1/T2, DIN 4108-2)

- **f_Rsi = (θ_si − θ_e)/(θ_i − θ_e)**; requirement **f_Rsi ≥ 0.7** under the
  standard verification climate θ_i = 20 °C, φ_i = 50 %, θ_e = −5 °C,
  R_si = 0.25 (opaque; 0.50 furniture-shielded; 0.13 glazing/frames),
  R_se = 0.04. Equivalent surface floor: **θ_si,min ≥ 12.6 °C** — the dew-point
  temperature of 20 °C/50 % air (θ_d = 9.3 °C) plus safety so surface RH stays
  ≤ 80 % (mould germination threshold φ_si = 80 % on nutrient-bearing surfaces;
  dust makes even glass growable). Newer editions: 0.71/0.67 by class — VERIFY.
- Unheated reference zones for verification: unheated roof space / car-park
  slab θ_u = −5 °C; unheated cellar/buffer θ_u = +10 °C; ground model bottom
  θ_g = +10 °C (ISO 10211 Tab. 1).
- R_min for condensation-free surfaces (walls, T2 DIN 4108-3):
  **R_min = R_si·(θ_i − θ_e)/(θ_i − θ_si,min) − (R_si + R_se)**; require
  R_vorh ≥ R_min. (See worked example 4.)
- Point (3D) bridges: at line-bridge crossings, approximate fRsi from the 2D
  results of the crossing details plus mean of adjacent 1D components
  (DIN 4108-2); otherwise full 3D numerics; Beiblatt 2 covers standard cases
  (gable/attic, corner window under parapet).
- Exempt from bridge proof: edges of compliant elements with continuous
  insulation layer; details executed per DIN 4108 Bbl. 2 or equivalent.
- Physical intuition (T4): Ψ = 0.6 with U = 0.2 means each metre of bridge
  loses as much as 3 m² of normal wall. Steel λ ≈ 1700×, aluminium ≈ 5700×
  mineral wool — metal fixings are "dangerous bridges"; stainless (17–30) and
  plastic-glass connectors (λ ≈ 0.25) are the standard balcony-coupler logic.
- Remedies ladder (T3, construction-detailing logic): (1) wrap projecting
  element fully in insulation; (2) insulate partway along its length; (3) cut
  the section + low-λ minimal connectors; (4) support the projection free of
  the envelope. Positive corners: add corner insulation (isotherm compression
  = geometric bridge); compact volume (low A/V) beats articulated massing.

### 4.5 Indicative Ψ value set from a digested whole-house audit (T2/T3; project-specific numerics govern)

| Junction (audit example) | Ψ [W/(m·K)] |
|---------------------------|-------------|
| Wall–floor slab (AW–BP) | 0.042 |
| Attic floor junction | 0.016 |
| External corner (90°, insulated) | −0.004 |
| Roof ridge | −0.012 |
| Eaves (Traufe, computed FE example) | −0.057 |
| Verge (Ortgang) | 0.031 |
| Parapet upstand | 0.092 |
| Wall–flat-roof junction | −0.012 |
| Window reveal (Laibung) | 0.065 |
| Window sill | 0.068 |
| Window head | 0.068 |
| Door reveal | 0.071 |
| Door threshold | 0.074 |
| Door head | 0.074 |

Rule of thumb for reading results: Ψ ≤ 0.01 W/(m·K) = "bridge-equivalent to
standard construction". Reveal/sill/head values > 0.06 show why window
position in the insulation plane (or wrap) matters more than frame U.

## 5. Windows, doors, transparent elements (T2, DIN EN ISO 10077-1/-2, DIN EN 673)

### 5.1 Assembly formula

**U_w = (A_g·U_g + A_f·U_f + l_g·Ψ_g + l_gb·Ψ_gb) / (A_g + A_f)** — frame
fraction typical 25–30 % of window area; l_g = glass edge/perimeter length;
Ψ_g spacer edge; Ψ_gb integrated glazing bars (l_gb = bar length).
Box window (Kastenfenster): 1/U_w = 1/U_w1 + 1/U_w2 − (1/R_si + R_s + 1/R_se),
R_si = 0.13, R_se = 0.04; cavity R_s per ISO 15099/VDI 6007-2 (gap resistance
tab: 12 mm uncoated 0.377; ε 0.1: 0.316; ε 0.2: 0.247; ε 0.4: 0.182; ε 0.8:
0.173; 50 mm drops to 0.406/0.336/0.260/0.189/0.179 due to convection).
Curtain wall (ISO 12631): U_CW = (U_g·A_g + U_p·A_p + Ψ_TJ·l_TJ)/A_CW.

### 5.2 Glazing U_g anchors (T2, DIN EN 673; vertical, gas fill ≥ 90 %)

| Stack (mm) | air | Ar | Kr | Xe |
|------------|-----|----|----|----|
| 2-gl. uncoated 4-16-4 | 2.7 | 2.6 | 2.6 | 2.6 |
| 2-gl. ε ≤ 0.1, 12 mm gap | 1.1 | 0.9 | 0.6 | 0.6 |
| 2-gl. ε ≤ 0.05, 16 mm (6-16-6) | 1.4 | 1.2 | 1.2 | 1.2 |
| 3-gl. one coating ε ≤ 0.1, 12+12 | 1.1 | 0.9 | 0.6* | 0.6* |
| 3-gl. two coatings ε ≤ 0.05, 12+12 | 1.0 | 0.8 | 0.5 | 0.5 |

(*column mapping partially garbled in digest — VERIFY row before quoting.)
Air-gap R alone (uncoated vertical): 6 mm → 0.13; 15 mm → 0.19; 50 mm → 0.18
(m²K/W; convection onset). Horizontal glazing has lower gap resistance
(heat flow up) → higher U_g. Noble-gas fill + low-e is the only route to
U_g < 0.7.

### 5.3 Frame U_f typical (T3/T4 ranges; manufacturer declared value governs)

wood 1.4–1.8 · PVC 2-chamber 2.3–2.8, 3-ch 1.7–2.2, 4-ch 1.4–1.6, 5-ch 1.2–1.3,
7-ch 0.95–1.1 · Al thermally broken 2.8–3.5 · Al optimised 1.4–1.5 ·
Passivhaus frame 0.7–0.8 W/(m²K). Opaque panels of transparent assemblies:
wood/wood-based/plastic door leaf 2.9; metal frame+cladding 4.0; gates: single
metal no break 6.5, with insulation core (λ ≤ 0.04 or R ≥ 0.5 at 15 mm) 2.9,
wood ≥ 15 mm 4.0, ≥ 25 mm 3.2.

### 5.4 Spacer edge Ψ_g and glazing bars Ψ_gb (T2, 10077 tables; typ./improved)

Ψ_g typ. values used in examples: 0.08 (metal break/older spacer, W24),
0.05 (improved, W32). Integrated bars (λ_metal ≤ 160 / plastic ≤ 0.30,
width ≤ 30 mm): 2-glazing, gap ≥ 2 mm: 0.03/(0.00) uncoated, 0.07/(0.04)
low-e; gap ≥ 4 mm: 0.01/(0.00), 0.04/(0.02). 3-glazing one cavity: ≥2 mm
0.03/(0.02), ≥4 mm 0.01/(0.01); both cavities: ≥2 mm 0.05/(0.03), ≥4 mm
0.02/(0.02) W/(m·K). Panel-edge spacers (curtain wall): type Al/Al 0.13–0.20;
steel/glass 0.14–0.18.

### 5.5 Uw grid anchors and g-value

- 30 % frame fraction (T2 grid anchors): U_g 1.0 + U_f 1.2 → U_w 1.3;
  U_g 0.7 + U_f 0.8 → U_w 0.9; old single glazing U_w ≈ 4–5 — any energy
  discussion with single glazing starts at replacement, not adjustment.
- g-value (Gesamtenergiedurchlassgrad): total solar energy transmittance,
  vertical incidence; typical double low-e g⊥ ≈ 0.6, triple ≈ 0.5, sun-control
  < 0.4; GEG reference window g 0.60 (see summer section for g_tot = g·F_C).
- Roller-shutter box (T2/T3): minimum quality via U_sb ≤ 0.85 W/(m²K) AND
  f_Rsi ≥ 0.70 at the junctions (model: top + underside adiabatic, roll cavity
  classification by e_tot ≤ 2 mm unventilated / ≤ 35 mm slight / > 35 mm well
  ventilated; PU-foam λ = 0.035 design; guide sleeve R handled per 10077-2).
- Closed external shutters add ΔR (informative, not for design U): airtight
  0.95·R_sh + 0.17 m²K/W down to very-high-permeability 0.08 — do not credit.
- Air-permeability classes (T3, DIN EN 12207 simplified per DIN 4108-4): all
  window types with age-resistant, replaceable, soft-gasketed, continuous
  single-plane seals → class 3; external doors comparable → class 2; old
  un-gasketed timber windows far below. Functional window joints must reach
  class 2 (≤ 2 storeys) / class 3 (> 2 storeys) per DIN 4108-2; component
  joint air permeability < 0.1 m³/(m·h·daPa^(2/3)) (unit flag: printed
  daPa^(2/3) — VERIFY Pa vs daPa in current text).
- Deep reveals with window in wall plane, spacer edge, frame rebate (~1.5 cm
  glass cover) are the weak chain; roof windows: inclined → worse U_g, stronger
  outward long-wave radiation → extra surface-condensation risk; optimise sill
  reveal, prefer external shading, small panes for shock ventilation, heater
  below window; never a bathtub under a window.

## 6. Moisture protection (Feuchteschutz)

### 6.1 Psychrometrics essentials (T2)

- Humid air = dry air + vapour; Dalton p = p_L + p_D; R_vapour = 461.5 J/(kg·K);
  standard air 1013.25 hPa, ρ_N 1.292 kg/m³; design indoor air ρ·c_p =
  0.34 Wh/(m³K) for ventilation loads.
- Saturation vapour pressure, Magnus (construction-grade, T2):
  **p_s = 610.5·exp(17.269·θ/(237.3+θ)) Pa** (0…30 °C, water);
  ice: 610.5·exp(21.875·θ/(265.5+θ)) (−20…0 °C).
  Anchor table p_s [Pa]: −10→259 · −5→401 · 0→611 · 5→872 · 10→1227 ·
  15→1704 · 20→2337 · 25→3166 · 30→4241.
- Saturation vapour content c_s [g/m³]: −10→2.14 · −5→3.24 · 0→4.84 · 5→6.79 ·
  10→9.39 · 15→12.82 · 20→17.27 · 25→23.01 · 30→30.31.
- Relative humidity φ = p_D/p_s; vapour concentration c_D = p_D/(R·T)
  = φ·c_s. Dew point (Magnus inverse): γ = ln(φ/100) + 17.269·θ/(237.3+θ);
  **θ_d = 237.3·γ/(17.269−γ)**. Anchors: 20/50→9.3 · 20/60→12.0 · 20/70→14.4 ·
  20/80→16.4 · 30/50→18.4 · 10/80→6.7 · 22/60→13.9 · 24/65→17.0 (via c-route).
- Surface condensation begins when θ_si ≤ θ_d; mould needs φ_si > 80 % for
  days → surface RH ≈ 1.25× room RH at cold surface → mould-limit formula
  p_si,sat = p_i/0.8 (T2 ISO 13788), θ_si,min = 12.6 °C at 20/50 %.
- Design indoor RH "normal occupancy" (T2, DIN EN ISO 13788 monthly):
  φ_i = 35 % for θ_e ≤ −10 °C; φ_i = θ_e + 45 (%) for −10 < θ_e < 20;
  65 % for θ_e ≥ 20. High occupancy: 40 % / θ_e + 50 / 70 %. EN 15026 comfort
  band variant: 30 % / θ_e + 40 / 60 %. Indoor air-quality RH target for
  comfort: 30–65 % (below 30 % dry mucosa, above 65 % mould risk; above
  ~18 °C RH should fall with rising temperature; cap 12 g/kg absolute).
- Room moisture balance: G = G_intern + V̇(v_e − v_i) ± sorption; ventilation
  transport V̇ = n·V. Typical gains (T3): person resting/light 30–60 g/h,
  physical work 100–140, sleeping ~300 g/8 h; bath+shower ~800 g/d; cooking
  600–800 g/d; spinning laundry 4.5 kg → 1000–2000 g total; dripping tap
  100–500 g/h; uncovered aquarium ~40 g/(h·m²). Highest-load rooms:
  bathroom, kitchen, bedroom.

### 6.2 Moisture in materials (T2/T3)

- Contents: mass u = m_w/m_b [M-%]; volume ψ [Vol-%]. Uptake regions:
  hygroscopic (adsorption, RH-driven), transition (capillary condensation at
  pore-RH 90–100 %), capillary range (liquid "sucking" Saugen).
- Equilibrium moisture u23,50 / u23,80 [M-%] anchors: EPS/XPS/MW/PU/CG 0/0 ·
  Vollziegel 0–0.7/0.5–1.1 · KS 0.5–1.3/1.1–2.6 · wood-fibre board 2/3 ·
  Porenbeton 2.6/4.5 · mortar 2–16/3–24 · cork 6–9/8–12 · wood-wool
  7–12/11–20 · cellulose loose 11/18.
- Capillary water uptake coefficient W [kg/(m²·h^0.5)]: concrete B15 0.96 ·
  Porenbeton 3.1–5.0 · Kalksandstein 3.6 · Vollziegel masonry 6.6 ·
  PS/PU/MW 0 · gypsum board 17.2 · cellulose 60 · sandstone 2.3–5.8
  (Seeberger) / 13.5–16.3 (Nebraer) · spruce along grain 0.2–0.4.
  Classification: saugend (sucking) W > 2; wasserhemmend < 2; wasserabweisend
  (repellent) < 0.5; wasserundurchlässig < 0.001 kg/(m²·h^0.5).
- Critical RH thresholds: metals corrosion-safe < 60 % RH; wood damage line
  u = 20 M-% (≈ 85 % RH); steel in carbonated concrete corrodes from ≈ 80 %
  equilibrium RH. Hygric strain ε_h = α_h·Δu; max reversible swelling:
  sandstone 0.14 %, AAC 0.17 %, KS 0.04 %, clinker 0.01 %. Wood tangential
  movement ≈ 10× longitudinal — gaps/joints must absorb transverse movement;
  structural timber install moisture u ≤ 15 ± 3 M-%, wood-based panels
  ≤ 12 ± 3 M-% (flat-roof rules below).
- Diffusion: μ = δ_air/δ_material (dry/wet tabulated); s_d = μ·d [m]
  (diffusion-equivalent air layer). Classes (T2, DIN 4108-3 / WTA finer):
  s_d ≤ 0.5 diffusionsoffen (open) · 0.5–2 diffusionshemmend (retarding) ·
  WTA: 2–5 moderat · 5–10 · 10–100 stark dampfbremsend · 100–400 dampfsperrend
  · ≥ 1500 dampfdicht (barrier; 1500 m = "infinite" in practice).
- Fundamental placement law (T2 baukonstruktion logic + DIN 4108-3): diffusion
  resistance **high on the warm (interior) side, low on the cold (exterior)
  side** — "inside retard, outside open". Materials combining perfect
  watertightness with vapour openness DO NOT EXIST (no Gore-Tex principle in
  building sheets); every trapped insulation package between two nearly closed
  skins is a **terrarium effect (Terrarien-Effekt)** candidate: construction
  moisture plus any ingress has no drying path → decay. Ventilated/steep roofs
  may instead rely on outward drying; flat roofs on decks ALWAYS need a vapour
  barrier (Dampfsperre) under the insulation because the top skin is
  vapour-tight by necessity.
- Transport mechanisms to respect: diffusion (vapour-pressure gradient),
  convection (total air-pressure gradient — carries ~far more water than
  diffusion, countered by airtightness DIN 4108-7), capillary conduction,
  surface diffusion, percolation/gravity, hydraulic pressure, osmosis (salts,
  rising damp). Unwanted liquid/convective routes are closed constructively by
  waterproofing + air/wind tight layer — not by hoping the membrane breathes.

### 6.3 Interstitial condensation verification (T2, DIN 4108-3 period balance + DIN EN ISO 13788 monthly)

Two stationary methods — choose by use:
- **Periodenbilanzverfahren** (DIN 4108-3): living/occupiable rooms without
  air conditioning; temperate-optimised; fixed interior climate; winter
  (condensation) period Dec–Feb = 90 d = 2160 h; summer (evaporation) period
  Jun–Aug = 2160 h; tends more critical (stricter). Boundary values (T2):
  condensation: θ_i 20 °C / φ_i 50 % → p_i = 1168 Pa; θ_e −5 °C / φ_e 80 % →
  p_e = 321 Pa. Evaporation: p_i ≈ 1200 Pa (≈18 °C/60 %), p_e ≈ 1200 Pa
  (≈15 °C/70 %); saturation pressure at the condensation plane p_c = 1700 Pa
  (≈15 °C 100 %), **roofs facing outdoor air p_c = 2000 Pa** (solar heating of
  the dark surface). Use R_si = 0.25 / R_se = 0.04.
- **Monatsbilanzverfahren** (DIN EN ISO 13788): monthly means, variable indoor
  humidity (formels §3.6); tends milder; for non-residential/humid uses;
  surface-mould check per month with p_si,sat = p_i/0.8 and f_Rsi comparison.

Glaser procedure (T2, stepwise — the agent must show the table):
1. Fix climate boundary conditions (above, or project climate).
2. Layer table: d, λ, μ (unfavourable split at plane), R_i, s_d_i,
   Δθ_i = R_i·(θ_i−θ_e)/R_T, θ at boundaries, p_s(θ) at boundaries.
   Subdivide layers with Δθ > 10 K AND high s_d into thirds (p_s is convex in
   θ; monolithic elements split in 3 equal layers, small μ for the two inner
   parts first); exterior layers with s_d < 0.1 m → set 0.1 m.
3. Draw temperature profile and saturation-vapour polygon p_s over Σs_d
   (x-axis = cumulative s_d, y = pressure).
4. Draw actual vapour-pressure line p_v from p_i to p_e as straight line over
   s_d (neglect surface resistances; slope = diffusion flow).
5. If p_v stays below p_s everywhere (Fall A): no condensation — acceptable.
   If p_v touches/crosses p_s: tangent polygon — touch point(s) = condensation
   plane(s); p_c = p_s(θ_c).
6. Condensation amount (cold period): g_i = δ·(p_i−p_c)/s_d,i,
   g_e = δ·(p_c−p_e)/s_d,e with **δ = 0.00072 g/(m·h·Pa)**;
   **M_c = t_c·(g_i − g_e)** [g/m² per period]; two planes: M_c = M_c1+M_c2
   with the between-plane flow g_z; band case: evaporation from mid-plane
   (s_d,i + 0.5·s_d,z).
7. Evaporation (warm period, p_c = 1700/2000 Pa, p_i = p_e = 1200):
   g_i,ev = δ(p_c−p_i)/s_d,i and g_e,ev = δ(p_c−p_e)/s_d,e;
   M_ev = t_ev·(g_i,ev + g_e,ev); require **M_c ≤ M_ev**.

Acceptance limits (T2 DIN 4108-3 / T3 practice): annual condensate
M_c ≤ **0.5 kg/(m²·a)** where the adjacent layer is water-repellent/
water-impervious (non-capillary surfaces: air layers, foam barriers, concrete
contact), ≤ **1.0 kg/(m²·a)** for sucking/water-resisting layers; wood:
moisture increase Δu ≤ **5 M-% solid wood / 3 M-% wood-based panels**
(wood-wool boards exempt per EN 13168) → M_c,lim = Δu·ρ·d·1000 g/m².
Extra drying reserve for convective ingress + initial moisture (T3,
DIN 68800-2 concept; 2022 edition withdrawn → transient proof preferred —
VERIFY status): roofs ≥ **250 g/(m²·a)**, walls/ceilings ≥ **100 g/(m²a)**.
If M_c exceeds the cap, the build-up FAILS even when M_ev > M_c: the drying
surplus cannot rescue a failed condensate amount (two-plane failure case).

Roof vapour-ratio rule (T2 DIN 4108-3, no-verification timber roofs):
required interior s_d,i vs exterior s_d,e (above/below insulation):
s_d,e ≤ 0.1 m → s_d,i ≥ 1.0 m · 0.1 < s_d,e ≤ 0.3 → s_d,i ≥ 2.0 m ·
0.3 < s_d,e ≤ 2.0 → s_d,i ≥ 6·s_d,e · s_d,e > 2.0 → s_d,i ≥ 6·s_d,e
(last valid only if no wood/wood-based material between the two functional
layers). Pitched-roof no-verification case additionally: layers below the
interior retarder carry ≤ 20 % of total thermal resistance (dew point must
sit inside the insulation). Required barrier sizing (T2):
**s_d,erf = s_d,e·(p_i−p_c)/(p_c−p_e) − s_d,i**.

Deemed-to-satisfy wall builds (T2, no Glaser proof; require DIN 4108-2 + -7
compliance): ETICS/WDVS; rear-ventilated claddings with ≥ 2 cm draining vent
cavity and ≥ 50 cm² vents per m wall length; water-repellent exterior plasters;
listed timber-frame builds; facebrick with interior plaster per thickness rows.
Internal insulation: period balance usually over-critical → transient model
(WUFI/DELPHIN class); thickness limit 4–5 cm practice, R_min target 1.2
(DIN 4108-3)/1.0 (WTA practice); airtightness behind the insulation is the
critical workmanship item (convective loops = mould); capillary-active systems
provable only transiently; hydrophobation blocks capillary drying too (fix
rising damp first; salts crystallise behind treated zone → spalling).

Timber flat-roof state-of-the-art rules (T3, post-damage practice):
1) fall ≥ 3 %; 2) dark unshaded membrane (solar absorption drives drying);
3) no topping (ballast/green/deck) over the build-up; 4) smart (moisture-
variable) VCL; 5) no uncontrolled cavities on the cold side of insulation;
6) verified air-tightness; 7) initial moisture: wood-based panels u ≤ 12 ± 3
M-%, solid structural timber u ≤ 15 ± 3 M-%. Flat roofs WITH toppings: place
insulation directly under the top layer so condensate cannot form in the
statically relevant layers below. Adequacy of the 250 g/(m²·a) reserve is
questioned in current research — whether summer reverse diffusion suffices
depends on insulation thickness: assess transient for real decisions.

Glaser method limits (state when reporting): constant properties (no moisture
dependence of λ/μ), no construction moisture, no thermal/hygric storage,
stationary climate, monotonic 1D, summer reverse diffusion underrepresented →
internal insulation, flat roofs, pools, and any near-threshold build-up deserve
a transient DIN EN ISO 15026 simulation (hourly TRY + moisture reference years,
rain included; result scatter depends on model + material data).

### 6.4 Wind-driven rain and surface water (T1/T2, DIN 4108-3; DIN 18550/18540 logic)

- Exposure groups (Beanspruchungsgruppen) by annual rainfall + site:
  **I gering**: < 600 mm/yr or specially sheltered; **II mittel**: 600–800 mm
  (or sheltered > 800, or exposed in low-rain region); **III stark**: > 800 mm
  or windy/coastal/mountain regions (or exposed in medium region); high-rise or
  exposed site bumps one group up. Add Spritzwasser at plinths and chemical
  loads (sea/de-icing salt).
- Wall suitability (T2 table logic): masonry/concrete with normal exterior
  plaster → lower groups; water-repellent exterior plaster → also group III;
  single-leaf fair-faced/facebrick: ≥ 31 cm incl. interior plaster (lower
  groups), ≥ 37.5 cm (higher); tiled bonded cladding per DIN 18515-1
  (higher groups need water-repellent bonding mortar); rear-ventilated cladding
  with open joints per DIN 18516 does NOT impair rain protection; ETICS with
  general type approval; timber with weather protection per DIN 68800-2.
  (Exact checkmark-to-group mapping lost in digest — VERIFY against DIN 4108-3.)
- Water-repellent plaster criterion (T2): w ≤ 0.5 kg/(m²·h^0.5) AND
  s_d ≤ 2.0 m AND product **w·s_d ≤ 0.2 kg/(m·h^0.5)** (trade-off: tighter
  plaster must breathe more).
- Joints: vertical — constructive detailing groups I/II; group III sealants
  per DIN 18540. Horizontal open swell-profile joints: sill height h ≥ 60 mm
  (I) / 80 (II) / 100 (III); or DIN 18540 sealant + constructive measure
  h ≥ 50 mm. Sealant geometry: depth ≈ 1/3–1/4 width via backer rod ≥ 10 mm,
  avoid 3-sided adhesion, flanks in tension-compression not peel.
- Windows/doors rain tightness (T2, DIN EN 12208): class 3 = 100 Pa, 4 = 150,
  5 = 200, 6 = 250, 7 = 300 (8A = 450, 9A = 600); selection per DIN 18055
  from wind zone, terrain category, height/geometry. Curtain walls: EN 12154
  R4–R7 = 150–600 Pa.
- Below grade: load cases Bodenfeuchte (non-pressing, permeable coarse soils),
  Sickerwasser (percolating), Stauwasser (perched, temporary over fines),
  Grundwasser/drückendes Wasser (permanent, hydrostatic + buoyancy);
  waterproofing design per DIN 18195 heritage — superseded by DIN 18533/-1853x
  series (VERIFY current class-to-measure table; white-tub WU vs black-tub
  tanking logic in sibling roofing-waterproofing skill).
- Physical driver (T4 intuition): driving-rain drop kinetic energy ≈ 10× calm
  rain (Ø 5 mm drop: 5.4 → 17.0 m/s; 7.5·10⁻⁶ → 7.6·10⁻⁵ J). Vertical walls
  drain; horizontal surfaces pond — flat roof is the single most severe
  exposure; every joint raised out of the water plane (upstand/Aufkantung) or
  bridged multi-stage.

## 7. Airtightness (Luftdichtheit) — layer, detailing, verification

### 7.1 Requirements and targets

- Legal (T1, EnEV 2014 §6 → GEG §26): heat-transferring envelope incl. joints
  permanently air-impermeable per recognised rules of technique = DIN 4108-7
  (T2/T3). Meeting a measured n50 does NOT replace the qualitative layer rules.
- Limits at 50 Pa, Verfahren B, per cooled/heated air volume (T1,
  EnEV Anl. 4 Nr. 2 = GEG §26 / DIN 4108-7): **without room-air technology
  n50 ≤ 3.0 h⁻¹; with ventilation system n50 ≤ 1.5 h⁻¹**; buildings with air
  volume > 1500 m³ (residential under DIN V 18599 primary-energy, or non-
  residential): envelope-related q50 ≤ 4.5 m³/(h·m²) without / ≤ 2.5 with RLT.
  DIN 4108-7 recommends n50 ≤ 1.0 where mechanical ventilation exists.
  Passivhaus certified: **n50 ≤ 0.6 h⁻¹**. Joint air permeability (T2
  DIN 4108-2): < 0.1 m³/(m·h·daPa^(2/3)).
- Design values when NOT measured (T1, DIN V 18599): category I = DIN 4108-7
  compliance + completed test: n50 2 (no RLT)/1 (RLT) for V ≤ 1500 m³, q50 3/2
  above; category II = new build without planned test: n50 4 / q50 6;
  category III = other: 6 / 9; category IV = visible leaks (open joints in the
  tight layer): 10 / 15. Convection losses in leaky existing buildings ≈
  25–40 % of heating-season heat.
- Free-infiltration design air-change (legacy balance): 0.7 without test / 0.6
  with test / 0.55 exhaust system / 0.6 supply+exhaust (h⁻¹).

### 7.2 The air-tight layer (T2/T3, DIN 4108-7)

Must enclose the heated volume **continuously**, traceable "without lifting
the pen" on every section; exceptions only functional joints of openable parts
and planned ventilation elements. Airtight materials: concrete; masonry with
one-sided plaster skin; plastic/bitumen/paper webs or foils; suitable boards
(plasterboard, fibre cement, wood-based boards, plastered wood-wool); sheet
metal. NOT airtight: porous wood-fibre boards, unplastered wood-wool, tongue-
and-groove boards, **mounting foam as such** (foam fills a joint but the foam
body itself is not the tight layer; large crack-prone timber sections cannot be
assumed tight). Joint methods: adhesive/sealing tapes and profiles, injectable
sealants/adhesives, foil edges embedded in plaster, gasketed battens/profiles;
tape joints behind claddings mechanically secured. Plan the layer inside a
second insulation layer so services do not perforate it; minimise
penetrations; tape strain-free; pre-compressed foams need residual compression.

Typical leak paths + sealing details (T3, construction-detailing digest):
- **Wand-Fenster-Anschluss three-layer rule** (Folien-Prinzip / three-stage
  sealing): outer stage rain brake (open, vapour-out), middle stage air/wind
  tightness (the single continuous Luftdichungsebene), inner stage vapour-
  retard seal — "outside more permeable than inside" applies to the junction
  too. Sequence at the sill/jamb: sill drip → frame rebate gasket →
  compression tape → interior airtight tape; render/smooth sealant plane
  BEFORE frame install; closed-cell backer rod + sealant, or fleece tape;
  functional joint class ≥ 2/3 (storeys) per DIN 4108-2.
- Gable/foundation and element-to-element connections: adhesive + pressure
  batten; overlapping membrane joints (single-sided tape on hard backing, or
  double-sided + batten; weld/glue); penetrations: moulded collars, sealed
  grommets, clamped insulated pipes through slabs; internal-wall penetrations
  into the airtight plane kept outside the insulated zone where possible.
- Kitchen hoods ducted directly outdoors: close (not "seal") during testing —
  not RLT openings per ministry interpretation digest.
- Verify with **intermediate blower-door test while accessible** (before
  drywall closes the layer); use compatible system components (single-manufacturer
  tapes/membranes on the same substrate).

### 7.3 Blower-door test (T2, DIN EN ISO 9972:2015-12, REPLACES DIN EN 13829)

- Norm procedures 1 (use state) / 2 (envelope) / 3 (purpose); German practice
  **Verfahren A** ≈ use state (permanent mechanical openings sealed only) and
  **Verfahren B** = envelope test (all deliberate free-ventilation openings and
  intermittent fans sealed too) — GEG/EnEV checks require Verfahren B. Interior
  doors open; HVAC and combustion appliances off.
- Convert fan volume flow to 20 °C standard state (worked conversion: 1000 m³/h
  fan flow at test temperature ↔ 943 m³/h ambient ↔ 1017 m³/h at 20 °C).
- Report: leakage curve, **n50 = q_pr(50 Pa)/V_e [h⁻¹]**, q_E50 [m³/(h·m²
  envelope)], q_F50 [m³/(h·m² floor area)].

## 8. Summer heat protection (sommerlicher Wärmeschutz)

### 8.1 Regulatory path and waivers (T1/T2, GEG → DIN 4108-2:2013-02 §8 "rules of technique")

Applies new builds and additions > 50 m² usable; with cooling plant installed,
amortising structural measures first. Physics trio: gain (solar through
glazing dominant; conduction only matters for uninsulated old stock; ventilation
when θ_e > θ_i; internal gains), storage (mass, C_wirk; do not block with
suspended ceilings; PCM optional), removal (night ventilation effective when
Δθ inside−outside ≥ 2 K; stack/cross-flow; TABS passive cooling).
Waiver by window-to-floor ratio f_WG (T2 Tab. 6): tilt 0–60° any orientation
f_WG ≤ 7 %; vertical (60–90°) NW–S–NE ≤ 10 %; other N orientations ≤ 15 %;
multi-orientation → smallest limit governs; sum all window areas. Extra
residential waiver: f_WG ≤ 35 % with O/E/W-glazing g ≤ 0.40 + F_C ≤ 0.35, or
g > 0.40 + F_C ≤ 0.30. Glass annexes: no proof (rooms vented only through them:
deemed satisfied with adequate vents + shading; else simulate). Rooms
proofed: only the critical (highest-requirement) occupied room(s).

### 8.2 Method 1 — solar gain index (S-Verfahren): S_vorh ≤ S_zul

S_vorh = Σ(A_w,j·g_tot,j)/A_G with g_tot = g·F_C (window area from rough
opening; structural shading: g_tot = g·F_C·F_S, F_S = lowest of F_h/F_f/F_0).
S_zul = S_1 + S_2 − S_3 + S_4 + S_5 + S_6:

S_1 base value (Tab. 8; A/B/C = summer climate regions, C hottest — ambiguous
site → worse region):

| Use / night vent / build | A | B | C |
|---|---|---|---|
| Wohn, none, light/medium/heavy | 0.071/0.080/0.087 | 0.056/0.067/0.074 | 0.041/0.054/0.061 |
| Wohn, raised n≥2 h⁻¹, l/m/h | 0.098/0.114/0.125 | 0.088/0.103/0.113 | 0.078/0.092/0.101 |
| Wohn, high n≥5 h⁻¹, l/m/h | 0.128/0.160/0.181 | 0.117/0.152/0.171 | 0.105/0.143/0.160 |
| Nichtwohn, none, l/m/h | 0.013/0.020/0.025 | 0.007/0.013/0.018 | 0.000/0.006/0.011 |
| Nichtwohn, raised, l/m/h | 0.071/0.089/0.101 | 0.060/0.081/0.092 | 0.048/0.072/0.083 |
| Nichtwohn, high, l/m/h | 0.090/0.135/0.170 | 0.082/0.124/0.158 | 0.074/0.113/0.145 |

Without proving C_wirk → assume leichte Bauart. Construction class by
C_wirk/A_G (DIN EN ISO 13786, 1-day period): leicht < 50 · mittel 50–130 ·
schwer > 130 Wh/(K·m²); effective layers: from room surface to first
insulation layer, 10 cm max depth (1-d period), internal partitions half
thickness; simplified: schwer ≈ RC slabs + area-mean ρ ≥ 1600, no decoupled
ceilings/internal insulation, height ≤ 4.5 m; mittel ρ ≥ 600.
- S_2 = a − b·f_WG: residential a=0.060 b=0.231; non-res a=0.030 b=0.115.
- S_3 = +0.03·(share of g ≤ 0.4 sun-control glazing; equal-credit: permanent
  diffuse-reducing device achieving g_tot ≤ 0.4).
- S_4 = −0.035·f_neig (roof-windows tilted 0–60° penalised).
- S_5 = +0.10·f_nord (N/NE/NW vertical; 0 if F_S already used).
- S_6 = passive cooling bonus: light 0.02 / medium 0.04 / heavy 0.06 (energy
  only for pumping medium, e.g. TABS + earth heat exchanger).
- Room depth: proof field A_G ≤ 3× clear height; façades > 6× h opposite →
  separate 3×h zones.

F_C fixed-shading factors (Tab. 7; columns: 2-gl sun-control g≤0.40 / 3-gl
g>0.40 / 2-gl g>0.40 — VERIFY column mapping): none 1.00/1.00/1.00; interior
or between panes — white/high-reflect (transparency ≤ 10 %, reflection ≥ 60 %)
0.65/0.70/0.65; light colours/low transparency (<15 %) 0.75/0.80/0.75;
dark/higher transparency 0.90/0.90/0.85; external — shutters/roller shutters
3/4 closed 0.35/0.30/0.30; fully closed 0.15/0.10/0.10 (NOT usable in proof);
venetian/louvers 45° lamellae 0.30/0.25/0.25; 10° lamellae 0.20/0.15/0.15;
awning parallel to glazing 0.30/0.25/0.25; canopies/free louvres 0.55/0.50/0.50
(must exclude direct sun: south β ≥ 50°; E/W β ≥ 85° or γ ≥ 115°; intermediate
β ≥ 80°; orientation tolerance ±22.5°). Devices must be permanently installed;
external shading most effective; double skins/transparent insulation/annex-
vented rooms → simulation only.

### 8.3 Method 2 — dynamic thermal simulation (T2 DIN 4108-2)

Limit = Übertemperaturgradstunden: residential **1200 Kh/a**, non-res
**500 Kh/a**; reference operative temperature by summer climate region
A 25 / B 26 / C 27 °C; full calendar year, TRY (2010/2011), norm-fixed usage,
setpoints, gains, ventilation and shading logic; climate-region map ( NRW
example: Bochum…Witten = C; Essen/Duisburg/Düsseldorf… = B).

## 9. Roof assemblies — vapour logic by type

| Type | Cross-section logic (warm→cold) | Moisture rule |
|------|--------------------------------|---------------|
| Warm flat roof (herkömmlich) | deck (falls ≥ 2 %, practice ≥ 3 % on timber), vapour barrier (Dampfsperre, mandatory — top skin vapour-tight), spot-bonded separating/pressure-equalising perforated layer, insulation (compressive class per use: dg living, ds/dx traffic), covering 2–3 layers or single-ply, ballast gravel 16/32 or protection | dew point inside insulation; no drying outward through sealed skin → keep barrier continuous incl. upstands; negative corners chamfered (Abfastung); parapets: upstand joint raised out of water plane, cover flashing with drip |
| Umkehrdach (inverted) | waterproofing → XPS/foam glass above (DUK class), filter fleece, ballast/pavers | waterproofing doubles as vapour barrier; insulation closed-cell (water uptake wd class); ΔU surcharge + drainage; never light-roof < R 0.15 below membrane |
| Ventilated (cold/kalt) roof | interior liner, insulation layer, free air space 0.06–0.30 m²K/W (R_u table), outer skin | only for low vapour load (unheated); moving air removes leaked vapour but convective loss risk through insulation if inlet/outlet unbalanced (≥ 5 ‰ roof area ≥ 200 cm²/m eaves, ≥ 1.25 ‰ ≥ 50 cm²/m ridge, ≤ 5° pitch variants per ZVDH capture — VERIFY current ZVDH numbers) |
| Warm steep roof (Zwischensparren) | GK/lining, smart/standard retarder, rafters+insulation, vapour-open sarking (UDB/USB), battens, tiles | modern thick builds have no under-rafter ventilation → verify condensation; membrane rain-impermeable yet vapour-open relative to required interior s_d (roof sd-ratio rule §6.3) |
| Aufsparren (above-rafter) | lining + insulation below deck, rigid insulation above rafters + covering | fewer rafter bridges; wedge/taper insulation per §2.3 |
| Metal-hall sandwich | steel skins, PUR/MW core, vapour barrier tape at inner seams | airtight package both sides = no drying path (terrarium); joints raised above water path, minimum pitch, never flat |

ZVDH underlay classes (T3, roofers' rules; required Unterdach class by pitch
deficit u_rdn below Regeldachneigung × number of further "erhöhte
Anforderungen" 0/1/2/3): deficit 0° → 6/6/5/4; ≤ 4° → 4/4/3/3; 4–8° →
3/3/3/3* (* = extra product-test requirements); 8–12° → 2/2/1/1. Residential
use counts as TWO increased requirements. Construction→class: watertight
Unterdach on deck 1.1 = Kl 1; rain-safe Unterdach 1.2 = Kl 2; seam/perforation-
protected Unterdeckung 2.1 = Kl 3; welded/bonded Unterdeckung 2.2 = Kl 4;
bitumen-overlapped 2.3 = Kl 4; lapped/seamed Unterspannung 2.4/3.x: 3.1 = Kl 3,
3.2 = Kl 4, 3.3 = Kl 6. Temporary weather cover (Behelfsdeckung): only UDB-A/
UDB-B/USB-A with proven direct-driving-rain impermeability (independent
certified driven-rain test) + manufacturer release. Building-integrated PV as covering:
joint rain-tightness by product test under realistic driving rain. Wood
rafters/structure: drying reserve rules §6.3; initial moisture limits; avoid
enclosing untreated timber in double-sealed packages; keep sarking overlapped
toward drainage; Unterdach counter-batten integrated in watertight type,
nail-sealing tape in rain-safe type.

## 10. Ground heat transfer (T2, DIN EN ISO 13370 simplified / DIN V 18599 annex)

- Characteristic dimension **B′ = A_G/(0.5·P)** (floor area / half perimeter).
- Effective floor thickness d_f = d_w + λ·(R_si + R_f) (R_si = 0.17 down);
  vertical wall d_bw = λ·(R_si,v=0.13 + R_w); slab-on-ground U_0 (compact form,
  digest-flagged): d_f < B′: U_0 = 2λ/(B′+d_f)·ln(B′/d_f + 1); d_f ≥ B′:
  U_0 = λ/(0.457·B′ + d_f) — VERIFY exact EN forms before proof use; L_s = A·U_0.
- Periodic part: penetration depth d_pe = √(3.15·10⁷·λ/(ρ·c)) (≈ 3.2 m
  sand/gravel, 2.2 m clay, 4.2 m rock; default λ 2.0); harmonic conductance
  L_pe ≈ 0.37·λ·P/ln(...)-form (digest garbled — VERIFY); monthly
  L*_s,m = L_s·F_x,m/(θ_i−θ_e,m) with F_x,m = 1 + (L_pe/L_s)·
  (θ_e,amp/(θ_i−θ_e))·cos(2π(m−t−b)/12); b = 1 floor on ground, 2 with edge
  insulation.
- Design λ_ground (T2 ISO 10456/13370): clay/silt 1.5 · sand/gravel 2.0 ·
  rock 3.5 · peat 0.2–0.5 · generic 2.0 W/(m·K).
- Energy-balance F_x ground table (T1/T2 DIN V 18599-2; bands R ≤ 0.3 / ≤ 1 /
  ≤ 3 / >3 m²K/W): floor of heated cellar, B′ < 5 m: 0.20/0.45/0.55/0.70 →
  B′ > 10: 0.15/0.30/0.40/0.55; cellar wall (all B′): 0.35/0.55/0.65/0.75;
  floor on grade no edge ins: <5: 0.30/0.55/0.70/0.80 → >10: 0.15/0.35/0.45/
  0.60 (with Randdämmung 5 m horizontal/2 m vertical: down to 0.10–0.55);
  cellar ceiling with Perimeterdämmung 0.35/0.65/0.75/0.80 (<5) →
  0.25/0.50/0.65/0.70 (>10). Larger B′ (compact slab) and larger R shrink F_x.
- Edge loss as line bridge: U* = U_0 + Ψ·l_WB/A (captured form); slab–
  wall earth junction Ψ computed per W30 chain (worked example 5b) — Ψ always
  normalised to the AIR Δθ even when one side is earth; earth-side 1D terms
  keep their own Δθ; only warm-side layers up to waterproofing count;
  replaceable floor finish ignored.
- Frost heave (T2 ISO 13793): design frost index F_n from ≥ 20-winter series
  (F50/F100 buildings); heated slab on ground needs no ground insulation for
  F_d ≤ 30 000 K·h; else edge insulation R_v tables by F_d and depth bands;
  DIN 1054 default foundation depth ≥ 0.80 m below frost-exposed surface;
  non-frost-sensitivity via gravel drainage layer or dense/aired concrete
  (baukonstruktion logic).

## 11. Worked verification examples (full arithmetic chains, reproduction-ready)

### Example 1 — Opaque U check, retrofit sizing, fastener and window corrections (T2/T1)

(a) 1D wall: 1.5 cm lime-cement plaster λ1.0 + 14 cm EPS λ0.04 + 17.5 cm KS
λ0.79 + 1 cm gypsum λ0.51:
R: 0.015/1.0=0.015 · 0.14/0.04=3.500 · 0.175/0.79=0.222 · 0.01/0.51=0.020;
R_T = 0.13+0.015+3.500+0.222+0.020+0.04 = 3.927 → **U = 1/3.927 = 0.25 W/(m²K)**.
Against unheated garage: Ru-method Ru = Ai/(ΣUe·Ae + 0.33·n·V) =
30/(87·2.0+0.33·3·105) = 30/277.9 = 0.108 → U = 1/(3.927+0.108) = 0.25 — OR
F_x = 0.5 with R_si=R_se=0.13: R_T = 4.016 → 0.25. **Pick one method; mixing
double-counts.**
(b) WDVS sizing on 24 cm Vollziegel λ1.2 + plasters: R_without_insul (layers
only) = 0.235; R_rest incl. films = 0.405.
a) Mindestwärmeschutz DIN 4108-2: R_min = 1.2 → d = (1.2−0.235)·0.04 = 0.0386
→ 4 cm EPS. b) GEG existing limit U ≤ 0.24 → R_T ≥ 1/0.24 = 4.167 →
d ≥ (4.167−0.405)·0.04 = 0.1505 → build 16 cm. (Edition flags: R_min 1.2 is
digest-era DIN 4108-2 heavy-class value; U_max 0.24 GEG Annex 7 — VERIFY.)
(c) Fastener correction on U = 0.25 build-up (Ø6.3 steel dowels λ50, 2.78/m²,
14 cm EPS λ0.04): A_f = π/4·0.0063² = 3.12·10⁻⁵ m²; R_D = 0.14/0.04 = 3.5;
R_T,h = 1/0.25 = 4.0; ΔU_f = n·A_f·(λ_f−λ_W)/d × (R-weighting) ≈ **+0.02**
(~8 %) → corrected **U = 0.27**. Apply corrections only if ΣΔU > 3 % of U —
here 8 % ⇒ mandatory.
(d) Window 1.6×0.8 m (A_w = 1.28 m²), A_g 0.84, A_f 0.44, U_g 1.2, U_f 1.5,
l_g 4.0 m, Ψ_g 0.08, internal bar l_gb 0.6 m with ΔU-bar 0.07 (d_gb = 3 mm):
U_w = (0.84·1.2 + 0.44·1.5 + 4.0·0.08 + 0.6·0.07)/1.28 =
(1.008+0.660+0.320+0.042)/1.28 = 2.030/1.28 = **1.59 W/(m²K)** — above GEG
1.3: change glass/frame or accept 1.9 bracket. Reverse case (frame budget):
target U_w 1.1, A_w 2.0, U_g 0.9, U_f 1.4, l_g 4.1, Ψ_g 0.05:
1.1·2.0 = (2.0−A_f)·0.9 + A_f·1.4 + 4.1·0.05 → 2.20 = 1.80+0.205+0.5A_f →
A_f = 0.39 m² → **max frame share 19.5 %**.
(e) Inhomogeneous pitched roof (f_ribs 0.11 / f_bay 0.89): R_T,rib = 1.651,
R_T,bay = 4.991 → R′ = 1/(0.11/1.651+0.89/4.991) = 4.083; R″ = 3.940; ratio
1.04 ≤ 1.5 → R_T = (4.083+3.940)/2 = 4.011 → **U = 0.25** (mean method;
digest also records the (R′+2R″)/3 ISO weighting — state the edition).

### Example 2 — Glaser / period-balance proof with numbers (T2)

Build-up (warm→cold): 1 cm gypsum μ4 (s_d 0.04) · 24 cm KS hollow μ15 (3.60)
· 12 cm MW μ1 (0.12) · 11.5 cm clinker μ100 (11.50). R_T = 3.636 (U 0.27);
Σs_d = 15.26 m. Climate: p_i = 1168 Pa (20/50), p_e = 321 Pa (−5/80);
t_c = 2160 h.
1. θ at boundaries from R shares; p_s at the MW/clinker plane: 411 Pa.
2. The p_v line runs above the p_s polygon around the MW/clinker boundary →
   tangent construction there: **condensation plane MW/clinker**, plane
   pressure p_c = 446 Pa (polygon value 411 Pa; p > p_s confirms τw).
3. s_d,i = 0.04+3.60+0.12 = 3.76 m; s_d,e = 11.50 m.
4. Inflow  g_i = 0.00072·(1168−446)/3.76 = 0.1383 g/(m²h);
   outflow g_e = 0.00072·(446−321)/11.50 = 0.0078 g/(m²h);
   M_c = 2160·(0.1383−0.0078) = **282 g/m² ≤ 500** (capillary-blocking
   clinker neighbour) → check 1 PASS.
5. Evaporation period (p_i = p_e = 1200, p_c = 1700): g_i,ev =
   0.00072·(1700−1200)/3.76 = 0.0957; g_e,ev = 0.00072·(1700−1200)/11.50 =
   0.0313 → M_ev = 2160·(0.0957+0.0313) = **274 g/m² < 282 → check 2 FAIL**.
   Fix: lower-μ lining or higher-μ carrier to move the plane/flows, or
   transient simulation credit; adding drying reserve (100 g/m²a wall) is NOT
   available — it must still be provided, not consumed.
Contrast passes: monolithic 30 cm AAC + plasters (split masonry in thirds):
R_T 1.753, Σs_d 3.065, plane inside masonry, M_c = 2160·(0.202−0.148) =
117 g/m² ≤ 1000 (capillary-active neighbours) and M_ev = 1140 ≥ 117 → PASS;
zero-condensation φ_i,max = 41 % (p_i rotated to tangency: 952/2337).
Warm flat roof double-bitumen (gypsum/RC 18/butyl μ2000 s_d 6.0/EPS 16
s_d 3.2/sealing s_d 120): Σs_d 143.6, plane at dam/EPS p_c 407: M_c = 49 ≤ 500;
dark roof → p_c,summer = 2000 Pa: M_ev = 63 ≥ 49 → PASS — but drying margin
is thin: any topping would kill summer reverse diffusion (see roof rules).
Timber-frame bay (gipsfaser 20 mm μ13 / MW 240 μ1 / WF 50 μ6 / lime 10 μ15):
R_T 8.22, Σs_d 0.95; plane MW/WF p_c 526 vs p 834: g_i = 0.00072·(1168−526)/
0.50 = 0.924, g_e = 0.00072·(526−321)/0.45 = 0.328, M_c = 2160·0.596 =
**1287 g/m² > 750** (= 0.03·500·0.05·1000, 3 M-% panel cap) **and > 500 →
FAIL although M_ev = 3283**. Zero-condensation barrier: s_d,erf ≈ 0.91 m
(existing interior 0.45 → +0.46 m); OSB μ30 → **min 30 mm OSB** inside.
Two-plane lesson (gypsum+8 MW+24 KS+6 MW+0.5 resin plaster): M_c1 2430 +
M_c2 203 = 2633 g/m² > 1000 → FAIL even though M_ev 6849 — **caps govern,
drying surplus cannot rescue**.

### Example 3 — Building-level Ψ audit and GEG H′_T check (T1/T2)

ΣΨ·l house (14×16 m footprint, pitched+flat roof mix), Ψ set of §4.5:
slab junction 60 m × 0.042 = 2.52; attic floor 146 m × 0.016 = 2.34; corners
47.2 m × (−0.004) = −0.19; parapet 34 m × 0.092 = 3.13; reveals 74.8 m ×
0.065 = 4.86; … total **ΣΨ·l = 20.88 W/K**; A = 1153 m² →
**ΔU_WB = 0.018 W/(m²K)** « flat rates 0.10 (unproved) / 0.05 (Bbl-2 A) /
0.03 (Bbl-2 B) → detailed proof unlocks a large credit; negative ridge/corner
values are legitimate.
Failing check and fix (refurbished bungalow): U_AW = 1/(0.13+0.01/0.51+
0.24/0.81+0.12/0.035+0.115/1.2+0.04) = 0.25; areas W 24.2 (U 1.4), AW 136.8,
G 48.0 (0.28), D 48.8 (0.20); A_e = 257.8; H_WB = 0.10·257.8 = 25.8;
H_T = ΣU·A·F_x + H_WB = 111.7 → H′_T = 111.7/257.8 = **0.433 > 0.40 → FAIL**.
Recover: H_T,allow = 0.40·257.8 = 103.1 → H_WB,max = 103.1−(111.7−25.8) =
17.2 → ΔU_WB,max = 0.067 W/(m²K) → achievable only by Bbl-2 category-A
detailing or full Ψ·l proof. (H′_T = 0.40 cap is EnEV-era; GEG reference-
building H′_T governs now — VERIFY.)
Earth-contact Ψ from 2D (FE loss F_B = 26.175 W/m, wall/floor junction,
θ_i 20, θ_e −5, ground +5): U1 cellar wall (warm-side layers only) =
1/(0.13+0.30/2.3+0.10/0.04) = 0.36; U2 floor = 1/(0.17+0.065/1.4+0.08/0.04)
= 0.45; reference lengths at insulation centreline l1 = 1.16, l2 = 1.40 m;
Ψ = (26.175 − 0.36·1.16·15 − 0.45·1.40·15)/25 = (26.175−6.264−9.450)/25 =
**0.42 W/(m·K)** — normalised to air Δθ (25 K); earth terms keep Δθ 15 K.
Ground companion (slab on grade, ISO 13370): λ_E 2.0; A = 109.3, P = 41.9 →
B′ = 5.22 m; R_f = 0.045/1.4+0.04/0.04+0.16/2.3+0.08/0.045 = 2.879;
d_eff = 0.365+2·(0.17+2.879+0.04) = 6.54 m → U_0 = 0.22 → L_s = 24.05 W/K;
d_pe = √(3.15·10⁷·2/(π·1.6·10³·… ρc≈1.28·10⁶)) ≈ 3.96 m → L_pe ≈ 14.68 W/K.

### Example 4 — Interior surface temperature, mould and condensation sizing (T1/T2)

Criterion pair: condensation θ_si ≥ θ_d; mould θ_si ≥ θ_si,min (φ_si ≤ 80 %);
under standard climate 20/−5/50 %: **θ_si,min = 12.6 °C ↔ f_Rsi ≥ 0.7**.
(a) Bathroom wall 22 °C/65 %, θ_e −5: dew point θ_d(22;65) = 15.1 °C →
R_min = R_si·(θ_i−θ_e)/(θ_i−θ_si,min) − (R_si+R_se) = 0.25·27/6.9 − 0.29 =
**0.69 m²K/W** (no surface water). Mould-free: θ_si,min = 18.6 °C →
R_min = 0.25·27/3.4 − 0.29 = **1.7 m²K/W**. Lesson: mould, not dew, governs
wet rooms.
(b) EPS wall, θ_e −15, +2 K safety: θ_si,min = 14.6 → R_min = 0.25·35/5.4 −
0.29 = 1.33; existing R 0.235 → d ≥ (1.33−0.235)·0.04 = 0.044 → **5 cm EPS**.
(c) Furniture effect: wardrobe sealed to wall → R_si = 1.0:
20 − 1.0·25/(1.0+0.246+d/0.04) ≥ 14.6 → d ≥ 0.135 → **14 cm** to stay mould-
free behind furniture (vs 5 cm bare wall — layout forbids external-wall
built-ins, or insulate the flanking zone).
(d) Uninsulated RC wall 20/−10, φ_i 65 %: R_T = 0.41 → q = 0.41⁻¹·30 =
73.2 W/m² → θ_si = 20 − 0.25·73.2 = 1.7 °C ≪ θ_d = 13.2 → running
condensation; fix with λ0.045 outside: R_min = 0.25·30/6.8 − 0.29 = 0.81 →
R_T,req = 0.81+0.29 = 1.10; ΔR = 1.10 − 0.41 = 0.69 → d ≥ 0.69·0.045 ≈ 0.031
→ build 4 cm.
(e) Surface condensation on old window U 2.2, 22/−5: q =
U·Δθ = 2.2·27 = 59.4 W/m²; θ_si = 22 − 0.13·59.4 = 14.3 °C →
φ_krit = p_s(14.3)/p_s(22) = 1629/2642 = **62 %** → fogs above 62 % room RH.
(f) Pool hall wall 28 °C/75 %, −10: existing R_T 2.585 → θ_si = 24.3 °C <
θ_si,min 26.9 → FAIL; required R_min = 0.25·38/1.1 − 0.29 = 8.34 →
d_ins = (8.34−0.30)·0.04 ≈ **0.31 m** — high-humidity use explodes the
requirement; challenge the room climate, not just the wall.
(g) ISO 13788 monthly (class 3, heavy, U 0.40): f_Rsi,vorh = 1 − U·R_si =
1 − 0.40·0.25 = 0.90; worst month Jan: θ_e 2.8, φ_e 0.92, Δp(chart) 711 →
p_i = p_e+Δp = 1398 Pa → p_si,sat = 1398/0.8 = 1747 → θ_si,min = 15.38 →
f_Rsi,min = (15.38−2.8)/(20−2.8) = 0.732 → 0.90 ≥ 0.732 PASS.

### Example 5 — Summer heat S-index proof, failure, and shade sizing (T2)

(a) PASS case (residential, region C, assumed night ventilation):
A_G = 5.5·4.2 = 23.1 m²; windows E 4.04 m² (g 0.65, awning parallel F_C 0.25),
S 4.56 m² (g 0.55, louvre 45° F_C 0.25).
S_vorh = (4.04·0.65·0.25 + 4.56·0.55·0.25)/23.1 = (0.6565+0.6270)/23.1 =
**0.0555**. Construction class: C_wirk by 10-cm rule (effective areas AW 25.3,
floor 23.1, roof 27.46, door 2.03; c = 1 kJ/kgK, thicknesses per build-up list) →
ΣC_wirk = 4269 Wh/K → C_wirk/A_G = 4269/23.1 = 184.8 > 130 → **schwere Bauart**.
S_1 (Wohn, raised night vent, heavy, C) = 0.101; f_WG = 8.6/23.1 = 0.37;
S_zul = 0.101 − (0.060−0.231·… )→ equivalent legacy form 0.101 − (f_WG−0.2)·0.15 =
0.101 − 0.0255 = **0.0755**; 0.0555 ≤ 0.0755 → **PASS** (with DIN 4108-2:2013
S_2 = 0.060−0.231·f_WG the arithmetic lands identically at −0.0255).
(b) FAIL case (office, light construction, region C, night vent):
f_WG = 16.3/28.2 = 57.8 % > 30 % → proof required; S_zul = 0.048 − 0.012 =
0.036; S_vorh = 16.3·0.75·0.25/28.2 = **0.108 ≫ 0.036 → insufficient**;
reduce window area and/or g (sun-control or external shading), or simulate.
(c) Shade sizing (reverse algebra): A_W 10.6, A_G 36.1 → f = 29.4 %; medium
build, region A, night vent: S_zul = 0.114 − 0.008 = 0.106 → required
F_C ≤ S_zul·A_G/(A_W·g) = 0.106·36.1/(10.6·0.85) = **0.42** → external roller
shutter 3/4 closed (F_C 0.30) qualifies (fully closed 0.15 is informational,
NOT creditable); alternatives louver 45° or parallel awning 0.25.

## 12. Agent workflow — "is there a dew point in this build-up?"

Layer-by-layer verification procedure (run in order, report each gate):
1. Classify the element: use class (residential? humid? unheated side?),
   orientation, exposure group (driving rain I/II/III), ground contact, roof
   type (warm/inverted/ventilated).
2. Build the layer table: d, λ_B (design value, not λ_D), μ (dry/wet), R_i,
   s_d_i. Mark unknowns VERIFY. Choose R_si/R_se per purpose: energy (0.10/
   0.13/0.17+0.04), bridge/moisture (0.25+0.04), furniture (0.5/1.0), glazing
   (0.13). Never mix films in one chain.
3. U check vs applicable T1 limit (GEG new/existing) and DIN 4108-2 R_min;
   apply Annex F corrections only if total > 3 %.
4. Surface temperature: f_Rsi at flat area AND worst junction (catalogue/FE);
   θ_si ≥ 12.6 °C standard climate, or monthly ISO 13788 for humid/non-res.
   Any junction where f_Rsi < 0.7 → flag mould risk and propose §4.4 remedy.
5. Condensation-plane scan: monotonic temperature drop → dew point exists
   wherever p_v line crosses p_s polygon; run Glaser steps §6.3; report plane
   location, M_c vs caps (500/1000 g/m²·wood Δu), M_ev, reserve. If plane sits
   on a structural timber layer or non-capillary interface, tighten the limit.
6. Vapour design rule sweep: sd ratio inside/outside (roof rule §6.3;
   warm-side retarder + cold-side openness); flag terrarium traps (double
   sealed insulation package without drying path), flat roofs without barrier,
   membranes ordered inside-open/outside-closed.
7. Airtightness: trace the Luftdichungsebene "without lifting the pen" on the
   section; list every penetration and junction (window three-layer rule,
   Leitungsdurchführungen); confirm target n50 (3.0/1.5, 0.6 Passivhaus) and
   intermediate blower-door plan (Verfahren B per EN ISO 9972).
8. Summer: waiver check f_WG; else S_vorh ≤ S_zul with F_C from fixed devices
   only; if exceeded, size F_C required or recommend dynamic simulation
   (Kh/a limits 1200/500).
9. Retrofit audit: existing U (compute as-is, incl. fasteners), WDVS thickness
   to both R_min and GEG U_max, H′_T budget with window-area trade (solve
   A_W,max), ΣΨ·l vs flat-rate credit.
10. Report tiers: T1 verdict (meets/exceeds limit), T2 method + inputs,
    T3/T4 estimates flagged; every superseded value printed with VERIFY.
    State the reality-check paragraph if output may be treated as final.

FreeCAD/BIM handoff (no geometry needed for physics data):
- Compute layer data in a table first; then write per-element property sets
  onto the corresponding IFC entities via the FreeCAD MCP execute_code path
  (neka-nat/freecad-mcp): create/extend Psets like `Pset_BuildingPhysics` with
  keys `UValue [W/m2K]`, `RT [m2K/W]`, `LambdaDesign`, `SdTotal [m]`,
  `VapourClass` (open/retarding/barrier), `fRsi`, `PsiValue [W/mK]`,
  `n50Target`, `AirTightLayer` (traceable yes/no), `ProofTier` (T1..T4),
  `VerificationStatus` (passed/failed/VERIFY).
- Keep the verification table itself in the model as a document/attachment or
  spreadsheet element — a U-value without its layer table and tier tag is not
  auditable. In section views annotate: airtight-layer line (one continuous
  stroke rule), vapour-control sd value per layer, fall arrows ≥ 2/3 %.

## 13. Common failure patterns (cause → detection → fix)

1. **Bridged ties through insulation** (sandwich/stay rods, wire anchors,
   steel shelf angles): cause — outer-leaf self-weight eccentricity grows with
   insulation thickness → strong anchors → linear bridges; detection — Ψ
   ≫ 0.05 at element joints, IR line patterns, f_Rsi < 0.7 at anchors;
   fix — FRP/plastic ties, stainless (λ 17) not plain steel (50), separate
   foundation for outer leaf, Bbl-2 details.
2. **Membrane order error (inside open / outside tight)**: cause — wrong
   face of smart/retarder foil, or vapour-open sarking paired with vapour-
   tight interior; detection — p_v above p_s in winter profile, damp plaster/
   rot at cold-side sheathing, summer sd-ratio rule violated; fix — re-
   establish "high sd warm side, low sd cold side" (roof rule §6.3); if
   already built: transient proof + drying concept, else strip & redo.
3. **Airtightness continuity breaks**: cause — mounting foam treated as air
   barrier, taped joints unloaded/not mechanically secured behind cladding,
   socket clusters and pipe chases perforating the layer, layer "switched"
   at material changes; detection — blower-door n50 ≫ target, q_E50 hot
   spots, smoke/IR during intermediate test before drywall; fix — single
   traceable plane, grommets/collars for Leitungsdurchführungen, second
   protection insulation inside the room-side, install tape under
   compression, intermediate test while accessible.
4. **Trapped moisture in inverted roofs / under toppings**: cause — topping
   (ballast, green, deck) or light-coloured membrane over damp-prone build-up
   kills solar drying; XPS wrong class (water uptake) or joints open;
   detection — water films in the insulation layer at inspection, U drift,
   ΔU surcharge ignored in proof; fix — drainage separation layer systems,
   wd-class XPS, fall ≥ 3 %, dark membrane, no uncontrolled cold-side
   cavities, transient re-proof per §9.
5. **Cold-corner mould behind furniture/at parapets**: cause — geometric fin
   effect + furniture shielding (R_si 0.5–1.0) + elevated φ_i (drying laundry,
   aquaria); detection — θ_si < 12.6 °C equivalent (f_Rsi < 0.7 at corner),
   user reports winter window/run streaks, musty corner; fix — continuous
   exterior insulation, corner insulation wedges, reveal insulation,
   layout rule (no external-wall wardrobes), ventilation concept +
   ≥ 20 °C continuous heating advice; verify junction by FE not 1D.
6. **Dew point moved into structural/insulation plane by retrofits**: cause —
   added interior or above-sarking insulation shifts the profile; partial
   internal insulation leaves bridges at slab returns; detection — Glaser
   plane in timber or at concrete contact (cap 500 g/m²), M_c > cap despite
   drying potential; fix — increase retarder sd to s_d,erf (§6.3 formula),
   flank/return insulation 50–100 cm into adjoining walls, airtight backing,
   transient proof for any internal insulation.
7. **Fastener/plug allowance omitted**: cause — U quoted without Annex F
   ΔU_f; detection — as-built U +0.02 (WDVS) beyond proof; fix — compute
   ΔU_f, declare plug pattern, or λ < 1.0 fixings.
8. **Single-drainage wedge under-sized**: cause — tapered insulation one
   outlet (2 % over 4 m = 8 cm extra apex) treated as negligible;
   detection — log-mean layer calc shows U above target; fix — raise
   minimum thickness (11 cm→12 cm) or split drainage planes.
9. **Terrarium sandwich packages**: cause — factory-sealed panels/rooms with
   both faces near-vapour-tight, any construction or leak moisture has no
   escape; detection — persistent RH drift, condensate at seams, no drying
   reserve in proof; fix — provide at least one drying direction (variable-μ
   layer, service cavity with venting), joint sealing as critical workmanship,
   avoid encasing hygroscopic cores.
10. **n50 credited to windows alone**: cause — class-3 window gaskets
    assumed to save the envelope; detection — q50 fails with intact windows;
    fix — perimeter three-layer junction, connection airtightness at sill
    (drip → gasket → compression tape → interior tape), not sealant hope.
11. **Glaser used where it must not**: internal insulation, flat roofs,
    pools, near-threshold timber: stationary verdicts only as screening —
    always recommend ISO 15026 transient confirmation before construction.
12. **Window share vs summer budget conflict solved by more glass**: cause —
    winter H′_T headroom spent on glazing, S-index then fails (example 5b);
    fix — couple §3.1/§4.5 budget and §8 S-check in one iteration, add
    creditable fixed shading or g ≤ 0.4 units.

## 14. Pre-delivery verification checklist (agent runs every item)

- [ ] Every numeric has a tier tag (T1/T2/T3/T4); no T4 in a T1 closure.
- [ ] Edition/date flags present for: GEG values, DIN 4108-2 fRsi 0.7 vs
      0.71/0.67, DIN 4108-3 driving-rain table, DIN 18195→1853x,
      EN 13829→ISO 9972, DIN 68800-2 reserve withdrawal, ISO 6946 averaging
      weight, primary-energy factor, EnEV-era H′_T caps, daPa²ᐟ³ unit.
- [ ] R_si/R_se set consistent with purpose (energy vs bridge/moisture); no
      Ru+F_x double count; no 0.25 in an energy U chain (or vice versa).
- [ ] λ = design values (λ_B), μ = unfavourable split at plane; layers with
      Δθ > 10 K & high s_d subdivided in thirds; exterior s_d floor 0.1 m.
- [ ] U corrections checked (air gap grade, fasteners, inverted-roof ΔU_r,
      3 % application threshold).
- [ ] fRsi evaluated at flat area AND worst junction; θ_si ≥ 12.6 °C or
      monthly ISO 13788 for humid/non-residential use.
- [ ] Glaser: M_c vs 500/1000 g/m²·a and wood Δu 5/3 M-%; M_ev ≥ M_c;
      reserve 250/100 g/(m²·a) shown (with withdrawn-status flag); caps
      treated as decisive over drying surplus.
- [ ] sd-ratio roof rule + warm-side retarder + cold-side openness verified;
      terrarium traps flagged; flat-roof barrier present.
- [ ] Airtight layer traceable on every section without pen lift; penetrations
      listed with sealing product; target n50 + Verfahren B test plan stated.
- [ ] Driving-rain group assigned; plaster w·s_d ≤ 0.2 / sill heights
      60/80/100 mm / joint sealing strategy consistent.
- [ ] Summer: waiver or S-chain complete (S_1..S_6, F_C from installed
      devices only, C_wirk class proven or leichte assumed); Kh/a route noted.
- [ ] Roof: type logic (warm/inverted/cold) matches ZVDH class and falls;
      timber initial moisture limits stated.
- [ ] Ground: B′, d_f, U_0 with VERIFY flags where EN formulas garbled;
      frost-heave relevance checked (F_d, foundation depth ≥ 0.80 m).
- [ ] Worked examples: arithmetic chains reproduce; unit of each result stated;
      deviations between digest variants shown rather than silently averaged.
- [ ] Reality-check sentence appended when output might be treated as final;
      sibling skills referenced for acoustics/fire/waterproofing/geometry.

---

## Appendix S: Source Check 2026-10 — values re-read from the literature

Each line below was read again in the source books (`sources/`) in October 2026, with the
place it stands at. "Confirmed" means: a dated book prints the rule and names the standard
or law; it does not mean the current edition of that standard was opened. State law
(LBO) and local rules still override; `VERIFY` tags elsewhere in this skill stay in force
unless a line here names the edition. Where a line here differs from a section of this
skill, that section was corrected and names the line ("S.n"); the appendix governs.

### S.1 GEG reference building, residential (book state: GEG 2020)

- Confirmed: exterior wall and ceiling against outside air U = 0.28 W/(m²K); wall against
  ground, floor slab, walls and ceilings to unheated rooms U = 0.35 W/(m²K); roof, top-floor
  ceiling U = 0.20 W/(m²K); windows and French doors Uw = 1.3 W/(m²K) with g = 0.60;
  exterior doors U = 1.8 W/(m²K); thermal bridge surcharge ΔU_WB = 0.05 W/(m²K). —
  *Wendehorst Bautechnische Zahlentafeln* Tab. 17.9 (rows 1.1 to 1.7 and 2); *Bausanierung*
  Tab. 3.2. A later book (*Gebäudetechnik* 8.2) prints the same 0.28 for the exterior wall
  under the successor law; check the text in force.

### S.2 Design thermal conductivity (DIN 4108-4)

- Confirmed: gypsum plaster without aggregate (ρ 1200) λ = 0.51 W/(mK); lime, lime-cement
  plaster (ρ 1800) λ = 1.0 W/(mK); sand-lime brick masonry ρ 1400 / 1600 / 1800 / 2000:
  λ = 0.70 / 0.79 / 0.99 / 1.1 W/(mK). — *Wendehorst Bautechnische Zahlentafeln* Tab. 17.25;
  *Allgemeine Grundlagen des Bauwesens*, plaster table in ch. 2.
- Books that use 0.70 or 0.99 for sand-lime brick are using another density class, not
  another rule: name the density with the value.

### S.3 Doors: reference value and design value are different things

- Confirmed: the design value for the heat-loss calculation of an exterior door of wood,
  wood-based material or plastic is U = 2.9 W/(m²K), of metal 4.0 W/(m²K) (DIN 4108-4). —
  *Wendehorst Bautechnische Zahlentafeln* Tab. 17.46. The 1.8 of S.1 is the reference
  building, not a product default.
