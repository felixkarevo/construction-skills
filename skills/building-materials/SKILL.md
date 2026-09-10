---
name: building-materials
description: >
  Baustoffe selection and verification for DACH/European construction: cement
  (EN 197-1/-5 types, strength classes 22.5-52.5, composition, special properties
  LH/SR/na/FE/SE), concrete (EN 206/DIN 1045-2 classes C8/10-C100/115, consistency
  F/C/S/SF/PJ/PL/VF/SR, exposure classes X0/XC/XD/XS/XF/XA/XM with max w/z,
  min cement, min class, min air, cover; k-value SCM crediting; mix-design
  procedure; SCC/UHPC), mortar (EN 998, MG groups, DM/LM), masonry units (Hochlochziegel
  HF/DF, Kalksandstein, Porenbeton, Leichtbeton; fmk design strength tables; EC6 NA),
  structural steel (S235-S700, EN 10025/10210/10219), reinforcement (B400/B500A/B,
  DIN 488, bar areas), timber (C14-C40, D30-D70, GL24h-GL36h, f_mk/E/kmod/kdef,
  DIN 68800 use classes), gypsum and lime binders, insulation materials (EN 13162-13171
  lambda classes, lambda_D to lambda_B), glass (EN 572 types, DIN 18008 fck 45/70/120),
  bitumen/asphalt, polymers and sealants, durability (carbonation, chloride,
  sulfate, ASR, freeze-thaw, alkali, wood decay), product marks (CE under CPR
  305/2011, DoP, abZ/ZiE, U-Zeichen, Bauregelliste), recycled and secondary raw
  materials (RC aggregate types, clinker factor, CSC/CCC labels, carbon textile),
  and consolidated material property tables (lambda/rho/mu/cp, unit weights,
  E-moduli, alpha-T) for structural and building-physics-thermal-moisture calculation.
---

# Building Materials (Baustoffe) — Selection and Verification

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

Skill for construction design agents: choosing, specifying and plausibility-checking
construction materials (Baustoffe) in DACH / European practice. Complements geometry
and detailing skills; supplies the material layer of any structural, physical or
durability verification.

## 1. Purpose and scope

Use this skill when the task involves any of:

- selecting a binder, concrete, mortar, masonry unit, steel grade, timber species/
  strength class, insulation, glass or membrane for a design brief;
- looking up classes, characteristic/design values, composition or property limits
  (w/z, cement content, cover, lambda, rho, mu, cp, f_mk, f_yk, f_ck...);
- checking a material specification for internal consistency (exposure vs concrete
  data sheet, strength class vs cover, use class vs wood species);
- assessing durability risk (carbonation, chloride, sulfate, ASR, frost, wood decay);
- judging whether a product may be used at all (CE/DoP, abZ, ZiE, national approval);
- compiling material data for structural analysis or building-physics-thermal-moisture models
  (thermal, hygric, acoustic, mass).

Out of scope: element design rules (use concrete-detailing / masonry-construction /
timber-steel-design), system choice (structural-systems), execution and site logic
(construction-detailing), ground characterization (geotechnics-foundations), energy
and moisture balance methods (building-physics-thermal-moisture), whole-building LCA
(sustainable-construction).

### Sibling skills

| Skill | Hands off what here |
|---|---|
| structural-systems | which material/system at all (Mauerwerk vs Stahlbeton vs Holz) |
| concrete-detailing | cover execution, bar spacing, anchorage, links |
| masonry-construction | bond, lintels, wall stability, movement joints |
| timber-steel-design | member/connection verification per EN 1993/1995 |
| building-physics-thermal-moisture | U-value, Glaser, dew-point, acoustic models |
| sustainable-construction | whole-building LCA, certification (DGNB/SQS/Minergie) |
| construction-detailing | joint geometry, layers, water-shedding logic |
| geotechnics-foundations | ground classes, bearing, groundwater aggression inputs |

## 2. Reality check — read before specifying

1. **Material choice is partly a legal decision, not only a technical one.** In
   Germany a product without CE under a harmonized hEN may need an abZ (allgemeines
   bauaufsichtliches Prüfzeugnis/ Zulassung) plus Ü-Zeichen; in Austria a
   Zulassung/genehmigungsbedürftiges Produkt; in Switzerland individual approvals or
   the list of approved products. Example: CEM II/C-M and CEM VI cements (EN 197-5)
   are not harmonized everywhere — in Germany they historically required abZ +
   Ü-Zeichen. VERIFY current status per project state (Bundesland) before specifying.
2. **The agent gives selection and property data; a responsible engineer confirms
   the spec.** Values here are digest-level summaries of standards and tabular
   handbooks; they carry edition-dependent dates. Standards cited by number only;
   always check the currently introduced version + National Annex (NA).
3. **National Annex (NA) differences are the rule, not the exception.** German NA
   values (e.g. alpha_cc = 0.85, gamma_M2 = 1.35 historically, DIN 488 grade set,
   DIN 1045-2 exposure limits, DIN 18008 for glass) differ from the EN base and from
   OE/CH practice. Exposure-class limits, minimum covers and approved cement×exposure
   matrices vary by country and can change with each revision (DIN 1045 series
   2023/24 restructured everything — VERIFY edition).
4. **Producer data beats generic tables** for anything that will be tendered:
   declared lambda_D, EPD values, DoP performance numbers. Tables here are for
   selection, pre-dimensioning and plausibility checks (T2/T3 tier).
5. **Recycled and low-carbon alternatives often shift requirements**, not just
   CO2: RC aggregate changes water absorption and w/z accounting; high-slag
   cements change early strength, curing duration and frost credit rules;
   REA-gypsum supply is energy-policy dependent.

## 3. Evidence tiers

Tag every number in an output with its tier; escalate when the use is load-bearing,
approval-relevant or tendered.

| Tier | Meaning | Examples here | Reliability |
|---|---|---|---|
| T1 | Harmonized EN product standard + Zulassung route; conformity system defined | EN 197-1 cement classes, EN 206 concrete characteristics, EN 10025 steel, EN 459-1 lime, EN 13279 gypsum | citable if edition verified |
| T2 | DIN EN + National Annex design tables (introducted nationally) | DIN 1045-2 Grenzwerte, DIN EN 1992/1995/1996 NA values, DIN 488, DIN 18008 | national, edition-sensitive |
| T3 | Producer/typical values, handbook tables, physical data | lambda_B/mu/cp per DIN 4108-4/ISO 10456, unit weights, GWP ranges | guidance only |
| T4 | Rules of thumb, empiric laws | carbonation alpha, +1% air ≈ −1.5 N/mm², paste volume needs | never spec-grade |

German regulatory concepts recur throughout: **Bauregelliste** (list of technical
rules for construction products, tied to MVV TB), **abZ** (general testing
certificate), **ZiE** (approval in individual case), **Ü-Zeichen** (conformity
mark for surveillance-required products), plus the DAfStb approved
cement/additive lists (VERIFY current publications) for concrete materials.

---

## 4. Materials

## 4.1 Binders: taxonomy and chemistry

Mineral binder classes (hardening behaviour decides use):

| Class (DE) | Hardening needs | Under water? | Water-resistant | Strength | Examples |
|---|---|---|---|---|---|
| nicht-hydraulisch (non-hydraulic) | CO2 + H2O, air only | no | no | low | gypsum, air lime (Luftkalk), anhydrite, clay |
| hydraulisch | H2O | yes | yes | high | Portland cement, hydraulic lime |
| latent-hydraulisch | activator (Ca(OH)2 / alkaline pore water) + H2O | yes | yes | high | granulated blast-furnace slag (Hüttensand) |
| puzzolanisch | H2O + Ca(OH)2 | yes | yes | strength-gaining, no own set | fly ash, silica fume (Silicastaub), metakaolin, trass, brick meal |

- CaO/SiO2 ratio rule: < 0.5 pozzolanic; ≤ 1.5 latent-hydraulic; > 1.5 hydraulic.
- Pozzolans consume Ca(OH)2 → pH drops → rebar corrosion risk if overdosed;
  latent-hydraulic materials keep pH ≈ constant.
- Non-hydraulic binders: interior only (render, screed, stucco).
- "Hydraulisch" in construction chemistry = water-binding AND water-resistant
  (not the physics meaning).
- Global volumes (order of magnitude, ~2018): clay ≈ 5 bn t/yr, cement ≈ 4.5 bn t,
  gypsum ≈ 350 Mt.

## 4.2 Cement (Zement)

Standard: **DIN EN 197-1** (27 harmonized types) + **DIN EN 197-5** (2021, adds
CEM II/C-M and CEM VI with higher clinker substitution; not fully harmonized in
the EU — in Germany approval route applies, VERIFY current status). Scope: cements
for concrete and mortar; composition, strength, setting, soundness, sulfate,
alkali, Cr(VI) limits. Factory production control + type testing under
conformity system **1+** per CPR (EU) 305/2011 → **DoP + CE mark**.

**Clinker chemistry** (rotary kiln, sintering zone 1450 °C; ground with 3–7 %
sulfate carrier — gypsum/anhydrite — as set regulator against C3A flash set):

| Phase | Formula | Code | Typical share (M-%) | Role |
|---|---|---|---|---|
| Alite | 3CaO·SiO2 | C3S | 50–75 (≈63) | early + late strength, high heat (520 J/g) |
| Belite | 2CaO·SiO2 | C2S | 5–20 (≈16) | late strength, low heat (260 J/g) |
| Aluminate | 3CaO·Al2O3 | C3A | 2–15 (≈11) | fastest, highest heat (1140–1670 J/g), sulfate/ASR vulnerability |
| Ferrite | 4CaO·Al2O3·Fe2O3 | C4AF | 5–15 (≈8) | minor strength, colour, 420 J/g |

- Free CaO (Freikalk) and periclase MgO: keep < 2 M-% each (expansion risk —
  soundness test Le Chatelier ≤ 10 mm).
- Hydration product C-S-H gives > 70 % of paste; portlandite Ca(OH)2 gives
  pH 12–13.5 → reinforcement passivation.
- Hydration periods: I induction (<15 min) → II dormant (15–60 min, setting start)
  → III acceleration (1–5 h, end set) → IV (5–24 h) → V final hardening (>24 h,
  months–years to full).

**Types (EN 197-1 groups):** CEM I Portland; CEM II Portland-composite (one
secondary constituent, letter S slag, D silica fume 6–10 only, P pozzolan,
Q shale/metakaolin-type, V siliceous fly ash, W calcareous fly ash, T calcined
shale, L limestone, LL low-clay limestone, M multiple); CEM III blast-furnace;
CEM IV pozzolanic; CEM V composite (slag+fly ash); CEM VI composite (EN 197-5).
A/B/C = low/medium/high secondary share.

Composition ranges (sulfate-free M-%), key types:

| Cement | Clinker | Other main constituent(s) |
|---|---|---|
| CEM I | 95–100 | — |
| CEM II/A-S | 80–94 | slag 6–20 |
| CEM II/B-S | 65–79 | slag 21–35 |
| CEM II/A-D | 90–94 | silica fume 6–10 |
| CEM II/A-V / A-W / A-L / A-LL / A-P / A-Q / A-T | 80–94 | 6–20 |
| CEM II/B-V / B-W / B-L / B-LL / B-P / B-Q / B-T | 65–79 | 21–35 |
| CEM II/A-M | 80–88 | multiple 12–20 |
| CEM II/C-M (EN 197-5) | 50–64 | 36–50 |
| CEM III/A | 35–64 | slag 36–65 |
| CEM III/B | 20–34 | slag 66–80 |
| CEM III/C | 5–19 | slag 81–95 (VERIFY boundary: digest garbled) |
| CEM IV/A | 65–89 (VERIFY) | pozzolan 11–35 |
| CEM IV/B | 45–64 (VERIFY) | pozzolan 36–55 |
| CEM V/A | 40–64 | slag 18–30 + fly ash 18–30 |
| CEM V/B | 20–38 | slag 31–49 + fly ash 31–49 |
| CEM VI (S-P/S-V/S-L/S-LL, EN 197-5) | 35–49 | slag 31–59 + pozzolan/limestone 6–20 |

- Naming example: CEM II/A-V 52,5 R SR = Portland fly-ash cement, 80–94 %
  clinker, 6–20 % fly ash, ≥ 52.5 N/mm² 28 d, high early, sulfate-resistant.

**Strength classes** (40×40×160 mm prism, EN 196-1; 28-d min = class value;
28-d upper cap ≤ 52.5 for 32.5/42.5, ≤ 62.5 for 52.5):

| Class | Early requirement | Value (N/mm²) |
|---|---|---|
| 32.5 L | 7 d | ≥ 12.0 (L only with CEM III) |
| 32.5 N | 7 d (some tables print) | ≥ 16.0 |
| 32.5 R | 2 d | ≥ 10.0 |
| 42.5 L | 7 d | ≥ 16.0 |
| 42.5 N | 2 d | ≥ 10.0 |
| 42.5 R | 2 d | ≥ 20.0 |
| 52.5 L | 7 d | ≥ 10.0 (VERIFY — rarely offered) |
| 52.5 N | 2 d | ≥ 20.0 |
| 52.5 R | 2 d | ≥ 30.0 |

Low-heat VLH 22.5 class exists under EN 14216 (very-low-heat cements). Setting
start (Vicat, EN 196-3): ≥ 75 / 60 / 45 min for 32.5 / 42.5 / 52.5.

**Special properties:**

| Code | Meaning | Requirement | Typical use |
|---|---|---|---|
| LH | low heat of hydration | ≤ 270 J/g characteristic | mass concrete, dams, warm weather |
| VLH | very low heat (EN 14216) | class 22.5 VLH | mass concrete |
| SR / HS | high sulfate resistance | CEM I: max C3A + Al2O3 limits (C3A < 3 %); CEM III/B,III/C: slag ≥ 66–70 % | sewage, soils per XA, seawater |
| (na) | low effective alkali | Na2O-eq ≤ 0.6 M-% (CEM III with high slag: ≤ 1.10) | ASR prevention |
| FE | early setting | start > 15 min and < class limit | precast |
| SE | quick setting | start < 45 min | shotcrete only |

**Practical limits:** hygroscopic storage — 52.5 use within ≤ 1 month, 42.5/32.5
≤ 2 months; bagged cement loses 10–30 % strength after 3 months (finer = worse).
True densities: PC 3.1, portland-slag/limestone 3.05, blast-furnace 3.0,
pozzolan 2.9 kg/dm³. Blaine fineness normal German cements 3100–5400 cm²/g.
Cr(VI) ≤ 2 ppm (REACH + EN 196-10). Hot cement is tolerable: +10 °C cement temp
at 300 kg/m³ raises fresh concrete only ~+1 °C; guide limit cement 70 °C
(ZTV Beton-StB).

**Sustainability one-liner:** cement ≈ 530 kg CO2-eq/t (DE mix, ~2/3 process
emissions from CaCO3 decarbonation at ~1450 °C, 1/3 combustion); CEM I clinker
~820 kg CO2/t cement, CEM II ~600–650 (VERIFY vintage); clinker factor of the
German mix ~67 % and falling; alternative fuels ~69 % of kiln energy (2024,
dated); recarbonation of crushed concrete takes back up to ~40 % of clinker CO2
over life (declared in EPDs).

## 4.3 Lime (Baukalk) — DIN EN 459-1

Types: Weißkalk CL, Dolomitkalk DL, natürlich hydraulischer Kalk NHL, hydraulischer
Kalk HL (blended), formulierter Kalk FL. Lime cycle: CaCO3 ↔(burn >900 °C) CaO
↔(slake, exothermic) Ca(OH)2 →(carbonate, needs CO2 + water) CaCO3. Air lime
hardens only by carbonation — slow, not water-resistant, interior only; superb
workability/water retention; historically disinfecting (limewash).

| Name | Code | CaO+MgO (M-%) | 28-d strength (N/mm²) |
|---|---|---|---|
| Weißkalk | CL 90 / 80 / 70 | ≥ 90 / ≥ 80 / ≥ 70 (MgO ≤ 5) | — |
| Dolomitkalk | DL 90-30 / 90-5 / 85-30 / 80-5 | MgO ≥ 30 or > 5 | — |
| Hydraulischer Kalk | HL 2 / 3.5 / 5 | — | ≥2 ≤7 / ≥3.5 ≤10 / ≥5 ≤15 (≤20 if bulk density < 0.90 kg/m³ — VERIFY direction of that footnote) |
| Natürlicher hydraulischer Kalk | NHL 2 / 3.5 / 5 | — | same bands as HL |
| Formulierter Kalk | FL 2 / 3.5 / 5 | — | same bands |

- NHL from burning marl (mergel, CaCO3 + clay) ~1000–1200 °C → C2S, C3A, C4AF,
  no C3S → hardens hydraulically + carbonatically. Roman cement = historic
  predecessor (opus caementitium). HL = lime blended with cement/slag/fly ash/
  limestone; FL = CL/NHL + pozzolanic additions (composition declared per
  EN 459-1 Annex D).
- Slaked-lime designations: Weißbranntkalk < 2 min slaking, Mittelbranntkalk
  2–6 min, Hartbranntkalk > 6 min; quicklime (Q) vs hydrated (S); saturated
  lime water pH ≈ 12.5.
- Sustainability one-liner: calcination emits process CO2 like cement but NHL/CL
  reabsorb much of it on carbonation (cradle-to-grave partially neutral; use
  EPD values).

## 4.4 Gypsum (Gips) — DIN EN 13279 / 13454

Non-hydraulic binder; raw material Gipsstein CaSO4·2H2O (natural or synthetic
REA-Gips from flue-gas desulfurization — historically ≈ 50 % of German demand,
declining with coal phase-out — VERIFY current share; availability is a supply
risk for plasterboard). Calcination cycle:

| Product | Phase | Formation T | Note |
|---|---|---|---|
| DH CaSO4·2H2O (gypsum stone) | α / β | 80–120 wet / 120–180 dry | raw |
| HH CaSO4·½H2O | α | wet (autoclave 110–140 °C) | dense crystals, high-strength plaster |
| HH CaSO4·½H2O | β | 120–180 dry (rotary kiln) | Stuckgips, fluffy, weaker |
| A-III CaSO4 | — | 110 wet / 290 dry | converts readily to HH |
| A-II CaSO4 | s / u | 300–500 / 500–700 | sparingly soluble / "dead-burnt" |
| Estrichgips (E) | — | > 700 | floor screed gypsum |
| A-I | — | 1180 | above → CaO + SO3 |

- Stoichiometric w/b: HH 0.19, A 0.26; practical 0.60–0.80 (down to 0.35 for
  high strength). Excess water → capillary porosity → strength/density loss.
- Setting 15–30 min (Stuckgips); volume expansion +0.2…1.0 %; ~40 % strength at
  set, rest on drying. β dry compressive 10–15, α up to 50 N/mm².
- Products (additive-free): Stuckgips 3–5 N/mm² (stucco, boards); Putzgips >3;
  Hartputzgips 40–50; Anhydrit-Binder AB5/AB20 5–20 (screeds, blocks).
- Fire: at ~110 °C water of crystallisation drives off; protected side capped at
  ~110 °C while water remains → excellent fire protection. Humidity buffering
  (capillary uptake to ~50 %) → interior climate benefit. Manufacture energy
  ≈ 1/10 of cement.
- Limits: water-soluble (solubility ≈ 2 g/L) → interior, no permanent damp;
  pH-neutral + sulfate → NO rebar corrosion protection; **never mix with lime or
  Portland cement** (delayed ettringite → expansion/cracking).
- Plasterboard: core 750–900 kg/m³ + paper liner carrying tension; gypsum fibre
  board = gypsum + cellulose.

## 4.5 Aggregates (Gesteinskörnung) — DIN EN 12620 / 13055 / 13139

Granular natural / industrial / recycled mineral material; 60–70 Vol.-% of normal
concrete; functions: cost/energy dilution, load-bearing skeleton, shrinkage and
hydration-heat reduction; light GK insulates, heavy GK shields radiation.

| By grain dry density | kg/m³ | Examples |
|---|---|---|
| Leichte Gesteinskörnung (light, EN 13055) | < 2000 | pumice, blast-furnace pumice/Hüttenbims, expanded clay/shale, crushed brick |
| Normale GK | 2000–3000 | limestone, quartzite, basalt, granite, graywacke |
| Schwere GK | ≥ 3000 | steel sand, hematite, magnetite, barite |

- Korngruppe d/D (e.g. 8/16); normative limits: Unterkorn ≤ 20 %, Überkorn 1–15 %
  (Kornklasse excludes them). Feinanteile 0–0.063 mm; Füller 0–0.125 mm;
  fine aggregate ≤ 4 mm; DIN 4022: Sand 0.06–2, Kies 2–63 mm.
- Gradation: Fuller-Thompson A(d) = (d/D)^q, q = 0.5 ideal; boundary curves A/B/C
  + gap curve U per DIN 1045-2. Indices: **Körnungsziffer k** = Σretained(0.25–63)/100;
  **D-Summe** = Σpassing. Fine curve → more water, low k, high D. Optimize by
  reducing Mittelkorn (e.g. ~40/20/40 split for 0/2 + 2/8 + 8/16).
- Packing: Füllkorn (fits voids) < Schlupfkorn (works into voids) < Sperrkorn
  (blocks packing). Dense skeleton → strength up, paste demand and shrinkage down.
- Density hierarchy ρ ≥ ρR ≥ ρS (Reindichte ≥ Kornrohdichte ≥ Schüttdichte);
  porosity P = (1 − ρR/ρ)·100; void ratio drives minimum paste volume.
- EN 12620 requirement categories with German-relevant limits: FI/SI shape
  (FI15…50, SI15…55), Feinanteile f classes (sand 0/2: 3/10/16/22 M-%), LA15–50
  crushing, SZ18–32, MDE10–35 wear, PSV ≥ 68/62/56/44 + AAV ≤ 10/15/20 (roadway),
  frost F1/F2/F4 (EN 1367-1, 10 cycles −17.5/+20 °C), MgSO4 MS18/25/35, water
  absorption WA (critical for light/RC aggregate — absorbed water not available
  for w/z), chlorides (Volhard, EN 1744-1), acid-soluble sulfate AS0.2/0.8,
  total S ≤ 1 M-%, organics (retard ≤ 120 min, 28-d loss ≤ 20 %; light particles
  ≤ 0.5 % fines / 0.1 % coarse).
- Shell content SC ≤ 10 %. AKR-reactive aggregates (opal, flint, quartz porphyry/
  Kieselkreide, greywacke) classified per national alkali guideline (DE: Alkali-
  Richtlinie DAfStb).
- Conformity: CE mandatory; concrete aggregate in DE: AVCP system 2+.
- **Sustainability one-liner:** 2022 DE: 564 Mt natural aggregate used, 75 Mt
  recycled (13.3 %), but only ~14.5 Mt into asphalt/concrete — RC use is a
  raw-material strategy, not a CO2 strategy (see §7).

## 4.6 SCM and chemical admixtures

**Type II additives (SCM)** credited via k-value (replaces cement in (w/z)eq =
w/(z + k·h)) — DIN EN 206 / DIN 1045-2:

| | fly ash (f) | silica fume (s) | FA+SF | GGBS (h) |
|---|---|---|---|---|
| k | 0.4 (underwater 0.7) | 1.0 | — | 0.4 national (VV TB); 0.6 recommended with CEM I/II/A |
| max content | ≤ 0.33 z (no P/V/D); ≤ 0.25 z with P/V; ≤ 0.15 z with D | ≤ 0.11 z | f ≤ 0.66z − 3.0s (CEM I); f ≤ 0.45z − 3.0s (others) | ≤ 0.33 z (no D); ≤ 0.15 z with D |
| not creditable | — | — | — | in XF2/XF4 (only FA creditable there — VERIFY footnote nuance) |

- Silica fume capped at 11 M-% of cement for rebar protection; needs SP; count
  suspension water in w/z; special curing (delayed pozzolanic reaction).
- Fly ash: spherical → water reduction, pumpability; supply shrinking (coal
  phase-out; ~2.5 Mt used DE 2020 — dated); GGBS supply shrinking with H2-DRI
  steel route (research on DRI slag). Calcined clays/metakaolin = future-pozzolan
  path; trass creditable per DIN 1045-2 but no k-value (abZ needed).
- **Fibers** (all need abZ as concrete additive in DE): steel (EN 14889-1) —
  flexural/tensile + crack bridging, industrial slabs, balling risk (Igelbildung);
  polymer PP/PE/PET/PA/PVA (EN 14889-2) — shrinkage-crack control and fire-spalling
  relief (melt channels); natural fibers research stage.
- **Type I (inert):** filler (limestone/quartz flour, majority < 0.063 mm) and
  pigments (EN 12878; iron oxides, TiO2, Cr2O3; high water demand may raise w/z).

**Chemical admixtures (EN 934-2, tests EN 480)** — dosage ≤ 5 M-% of cement,
≤ 50 g/kg (60 with combined types); water content of liquid > 3 L/m³ counts into w/z:

| Code | Function | Mechanism / notes |
|---|---|---|
| BV | water-reducing (~10 %) | lowers surface tension/viscosity; retards a bit |
| FM | superplasticizer (up to 30 %) | NSF/lignosulfonate = electrostatic (w/z > 0.35, effect 15–30 min); PCE = electrostatic + steric (long chains = early strength; short = workability retention; 30–60 min, often site-dosed) |
| LP | air-entraining | stable 10–300 µm spheres, spacing factor governs; +1 Vol-% air ≈ −5 L water and −1.5…−2 N/mm² strength; ice +9 % volume → pressure relief + capillary cut |
| BE | accelerator | set (Al salts — non-alkaline systems for shotcrete; Ca(NO3)2 with rebar, CaCl2 unreinforced only) vs hardening (nano C-S-H seeds) |
| VZ | retarder | sugar acids, lignosulfonate, phosphonates; overdose → reversal ("Umschlagen"); heat, long pours, ready-mix transit |
| DM | hydrophobic/membrane | silanes/siloxanes, metal soaps; capillary uptake −90 %, vapour −5–10 %; do not overrate vs low w/z |
| ST/VMA | stabilizer / viscosity-modifying | underwater concrete (HPC), SCC segregation control |

## 4.7 Concrete — fresh state (EN 206 + DIN 1045-2/-3, EN 12350)

**Consistency classes** (pick test method by stiffness):

| Class | Range | Test | Consistency word |
|---|---|---|---|
| F1 | spread ≤ 340 mm | table | steif (stiff) |
| F2 | 350–410 | | plastisch |
| F3 | 420–480 | | weich (recommended normal range) |
| F4 | 490–550 | | sehr weich |
| F5 | 560–620 | | fließfähig |
| F6 | ≥ 630 | | sehr fließfähig; > 700 = SVB (self-levelling, guideline) |
| C0 | compaction factor ≥ 1.46 | Ve-be/compaction | sehr steif (roller-compacted) |
| C1 | 1.45–1.26 | | steif |
| C2 | 1.25–1.11 | | plastisch |
| C3 | 1.10–1.04 | | weich |
| C4 | < 1.04 | | only pumpable light concrete |
| S1–S5 | slump 10–40/50–90/100–150/160–210/≥220 mm | cone (EN 206) | EN 206 declaration |
| V0–V4 | Ve-be ≥31/30–21/20–11/10–6/5–3 s | Ve-be | stiff concretes |

**SCC classes:** slump flow SF1 550–650, SF2 660–750, SF3 760–850 mm; viscosity
t500 VS1 < 2 s / VS2 ≥ 2 s (VS not for Dmax > 40); funnel VF1 < 9 s, VF2 9–25 s
(target 10–20); J-ring PJ1/PJ2 Δh ≤ 10 mm; L-box PL1/PL2 H2/H1 ≥ 0.80; sieve
segregation SR1 ≤ 20 %, SR2 ≤ 15 %. SVB = flows, fills, surrounds rebar under own
weight, no vibration — needs BV/FM; extra water alone → segregation + capillary pores.

**Minimum paste volume** (DIN 1045-2; applies ≥ F3 and ≥ C25/30; paste = cement +
SCM + effective water):

| Dmax (mm) | F3 | F4 | F5 | F6 |
|---|---|---|---|---|
| 32 | 270 | 280 | 290 | 300 l/m³ |
| 22 | 275 | 285 | 295 | 305 |
| 16 | 280 | 290 | 300 | 310 |
| 8 | 295 | 305 | 315 | 325 |

- Dmax ≤ 1/4…1/3 of smallest member dimension and ≤ clear bar spacing − 5 mm
  (VERIFY exact split between EN 206 / DIN 1045-2 / EN 13670).
- Fresh density ~2300 kg/m³ typical; entrapped air 1–2 Vol.-% even compacted;
  min air content: unreinforced 1.0 %, RC 0.4 %, prestressed 0.2 % (as-placed
  damage ceilings) — VERIFY national product-standard numbers.
- Fresh concrete temperature: max generally 30 °C; min at placement 5 °C (10 °C
  if cement < 240 kg/m³, LH cement, or air < −3 °C); frost protection until
  > 10 °C for 3 days or 5 N/mm² cylinder strength. Mixing formula:
  Tb = [0.84(z·Tz + f·Tf + g·Tg) + 4.2·w·Tw] / [0.84(z + f + g) + 4.2w].
- Transport: discharge within 90 min of first water (45 min without agitation,
  stiff). Free fall ≤ 1.5–2 m (tremie beyond; 0.5 m for architectural faces).
- **Curing (Nachbehandlung, DIN 1045-3/EN 13670):** classes NK1 (X0/XC1, ≥ ½ day),
  NK3 (all else: reach 50 % fck), NK4 (XM + XF4 slow hardening: 70 % fck). Minimum
  durations by surface temp υ (≥25/15–25/10–15/5–10 °C) × hardening rate
  r = fcm2/fcm28 (quick ≥ 0.50: 1/1/2/3 d; medium ≥ 0.30: 2/2/4/6; slow ≥ 0.15:
  2/4/7/10; very slow < 0.15: 3/5/10/15); double for NK4; extend below 5 °C.
  Water-retaining (formwork left, foil, curing compound) vs water-supplying
  (ponding, spray); redundant when evaporation is low (rain/fog).

## 4.8 Concrete — hardened state and design values

**Strength classes** (cylinder/cube, water-stored, 5 % fractile fck):

| Class | fck/fck,cube | Class | fck/fck,cube |
|---|---|---|---|
| C8/10 | 8/10 | C40/50 | 40/50 |
| C12/15 | 12/15 | C45/55 | 45/55 |
| C16/20 | 16/20 | C50/60 | 50/60 |
| C20/25 | 20/25 | C55/67 | 55/67 (HSC starts) |
| C25/30 | 25/30 | C60/75 | 60/75 |
| C30/37 | 30/37 | C70/85 | 70/85 |
| C35/45 | 35/45 | C80/95 | 80/95 |
| C90/105 | 90/105 | C100/115 | 100/115 (≥ C90/105: abZ in DE — VERIFY current) |

- Lightweight LC 8/9…LC 80/88 (dry 800–2000 kg/m³, density classes D1,0–D2,0);
  normal 2000–2600; heavy > 2600 kg/m³.
- Cube↔cylinder ≈ ×1.25 convention is inside the class pair; dry-stored specimens
  10–40 % higher: water↔dry cube conversion ≤ C50/60 ×0.92, ≥ C55/67 ×0.95;
  150 mm cube = 0.97 × 100 mm cube.
- Tensile: fctm ≈ 0.3·fck^(2/3) (EC2, ≤ C50/60); fctk,005/095 = 0.7/1.3 fctm;
  general form fct = c·fc^(2/3) with c 0.35–0.55 bending, 0.22–0.32 splitting,
  0.17–0.32 axial.
- Schmidt hammer (EN 12504-2) supplementary only: ≥ 9 readings, ≥ 25 mm spacing/edge.
- Water penetration depth (EN 12390-8): 500 kPa / 72 h — acceptance often ≤ 50 mm
  (VERIFY project spec); carbonation EN 12390-10; chloride migration −18.

**EC2 design values (German NA: alpha_cc = 0.85, gamma_c = 1.5, gamma_s = 1.15;
1.15/1.0 in extraordinary/accidental situations — VERIFY NA current):**

| Class | fcd (N/mm²) | fctd,005 (N/mm²) | Class | fcd | fctd,005 |
|---|---|---|---|---|---|
| C12/15 | 6.80 | 0.62 | C50/60 | 28.33 | 1.62 |
| C16/20 | 9.07 | 0.76 | C55/67 | 31.16 | 1.72 |
| C20/25 | 11.33 | 0.88 | C60/75 | 34.00 | 1.82 |
| C25/30 | 14.17 | 1.02 | C70/85 | 39.66 | 2.02 |
| C30/37 | 17.00 | 1.15 | C80/95 | 45.33 | 2.21 |
| C35/45 | 19.83 | 1.27 | C90/105 | 51.00 | 2.39 |
| C40/50 | 22.67 | 1.39 | C100/115 | 56.66 | 2.56 |
| C45/55 | 25.50 | 1.51 | | | |

(αcc·fck/γc, αcc = 0.85. Unreinforced concrete: 0.7·fck/γc — fcd 5.6…16.3 up to
max C35/45 in bending+axial; VERIFY current NA treatment.)

**Mean properties to C50/60 (Tafel 8.2 style):**

| Class | fck/fck,cube/fcm | fctm / fctk,005 / fctk,095 | Ecm (MPa) | eps_c2 / eps_cu2 (‰) |
|---|---|---|---|---|
| C12/15 | 12/15/20 | 1.6/1.1/2.0 | 27000 | 1.8/3.5 |
| C16/20 | 16/20/24 | 1.9/1.3/2.5 | 29000 | 1.9/3.5 |
| C20/25 | 20/25/28 | 2.2/1.5/2.9 | 30000 | 2.1/3.5 |
| C25/30 | 25/30/33 | 2.6/1.8/3.3 | 31000 | 2.2/3.5 |
| C30/37 | 30/37/38 | 2.9/2.0/3.8 | 33000 | 2.3/3.5 |
| C35/45 | 35/45/43 | 3.2/2.2/4.2 | 34000 | 2.4/3.5 |
| C40/50 | 40/50/48 | 3.5/2.5/4.6 | 35000 | 2.5/3.5 |
| C45/55 | 45/55/53 | 3.8/2.7/4.9 | 36000 | 2.55/3.5 |
| C50/60 | 50/60/58 | 4.1/2.9/5.3 | 37000 | 2.6/3.5 |
| C55/67→C100/115 | fcm 63…108 | fctm 4.2…5.2 | 38000→45000 | eps_cu2 falls 3.2→2.8 (HSC — VERIFY strain rows) |

Design-line strains: parabola-rectangle eps_c2 = 2.0 ‰, eps_cu2/eps_cu3 = 3.5 ‰
(≤ C50/60); bilinear 1.75/3.5; C12/15 only for predominantly static loads.
Age: fcm(t) = exp[s·(1 − (28/t)^0.5)]·fcm, s = 0.20 (R/52.5N), 0.25 (42.5N, 32.5R),
0.38 (32.5N/S); Ecm(t) ≈ (fcm(t)/fcm)^0.3·Ecm.

**Deformations:** ultimate compression strain 2.0–2.5 ‰ (plain-zone cracking
starts ~0.1–0.15 ‰ tension); Poisson 0.2 elastic; creep/shrinkage tables per
EC2 (h0, RH, t0, cement class — use code; indicative end shrinkage for normal
concrete ~0.5–0.8 ‰; paste alone ~3 ‰ after 1 d + drying). alpha_T concrete
(8–12) ×10⁻⁶/K (digest: normal ~10), steel 11–12 → compatible for RC.
+1 Vol-% porosity ≈ −3 N/mm²; percolation: watertight only below ~25 Vol-%
capillary porosity.

**SCC** (EN 206 Annex E) and **UHPC** (f_cm > 150 N/mm² class, w/z < 0.25 with
SF + PCE — national rules/abZ or ETA, e.g. UHPC recommendations; VERIFY route)
both change QA, cover and fire-spalling detail expectations; SCC aggregate < 40
Vol-%, paste-volume driven; UHPC needs its own execution standard (abZ in DE —
VERIFY; a DIN UHPC standard roadmap exists since 2024).

**Sustainability one-liner:** concrete itself ~50–120 kg CO2-eq/m³ for standard
RC (cement-driven; VERIFY against EPD/ÖKOBAUDAT — no source number digested);
low-clinker cements, SCM credit, RC aggregate (raw material, not CO2), surface
recarbonation; hollow-core precast −30–40 % material; carbon-textile sections
−50 % material ≈ −30 % CO2.

## 4.9 Concrete durability: exposure classes and composition limits

Design working life assumed ≥ 50 years (buildings); 100 years (bridges per
EN 1990). Classes per EN 206 / DIN 1045-2 (XM and moisture classes are national
additions). Strictest value governs when combined.

| Class | Environment | Mechanism |
|---|---|---|
| X0 | no risk (unreinforced, very dry RH ≤ 30 %) | — |
| XC1–4 | carbonation: dry/permanently wet / wet seldom dry / moderate / alternating | CO2 + H2O + Ca(OH)2 → CaCO3, pH < 9 → uniform corrosion |
| XD1–3 | chloride, not seawater (de-icing, brine) | pitting (Lochfraß) — silent, sudden bar loss |
| XS1–3 | seawater (spray / submerged / tidal-splash zone) | chloride + sometimes XA coupling |
| XF1–4 | freeze-thaw ± de-icer (moderate/high saturation × without/with) | ice +9 % volume → hydraulic pressure |
| XA1–3 | chemical attack (weak/moderate+marine/strong) | expansive (ettringite) or dissolving (acids, leaching) |
| XM1–3 | abrasion (pneumatic / solid tyres / tracked) | wear |

**Composition limits (DIN 1045-2 Grenzwerte; max w/z, min class, min cement
kg/m³ plain / with credited SCM, min air):**

| Class | max w/z | min class | min z | min z credited | min air |
|---|---|---|---|---|---|
| X0 | — | C8/10 | — | — | — |
| XC1 | 0.75 | C16/20 | 240 | 240 | — |
| XC2 | 0.75 | C16/20 | 240 | 240 | — |
| XC3 | 0.65 | C20/25 | 260 | 240 | — |
| XC4 | 0.60 | C25/30 | 280 | 270 | — |
| XD1 | 0.55 | C30/37 | 300 | 270 | — |
| XD2 | 0.50 | C35/45* | 320 | 270 | — |
| XD3 | 0.45 | C35/45 | 320 | 270 | — |
| XS1 | 0.55 | C30/37 | 300 | 270 | — |
| XS2 | 0.50 | C35/45* | 320 | 270 | — |
| XS3 | 0.45 | C35/45 | 320 | 270 | — |
| XF1 | 0.60 | C25/30 | 280 | 270 | — |
| XF2 | 0.55 (air-entr.) / 0.50 (no air, then C35/45*) | C25/30 | 300 | 270 | 4.0–5.5 % |
| XF3 | 0.55 C25/30 (air) / 0.50 C35/45* | C25/30 | 300/320 | 270 | 4.0–5.5 % |
| XF4 | 0.50 | C30/37 | 320 | 270 | 4.0–5.5 % mandatory |
| XA1 | 0.60 | C25/30 | 280 | 270 | — |
| XA2 | 0.50 | C35/45 | 320 | 270 | — |
| XA3 | 0.45 | C35/45 | 320 | 270 | — (protective layer usually required) |
| XM1 | 0.55 | C30/37 | 300 | 270 | — |
| XM2 | 0.55 troweled / 0.45 | C30/37 / C35/45 | 300/320 | 270 | — |
| XM3 | 0.45 (hard aggregate, DIN 1100) | C35/45 | 320 | 270 | — |

Footnotes (memorise the logic): air content by Dmax 8/16/32/63 = 5.5/4.5/4.0/3.5
Vol-% (individual value −0.5 max); Dmax 63 → −30 kg/m³ cement; air-entrained or
slow-hardening (r < 0.30) → one strength class lower allowed; max cement 380 kg/m³
(XM, below C70/85); ED-fibre concrete w/z ≤ 0.40 may omit air (VERIFY exact
footnote scope); XF2–4 SCM credit: fly ash only. A cement-type × exposure
applicability matrix exists (e.g. CEM II/A-P not for XF2/XF4; CEM III/B, III/C
preferred XA; CEM I 52,5 R common precast) — consult the DIN 1045-2 table, VERIFY.

**Moisture classes (ASR prevention):** WO mostly dry; WF frequently/long wet
(unprotected exterior, RH > 80 %, mass concrete > 0.80 m); WA wet + external
alkali (seawater, de-icer, alkali salts); WS wet+alkali+dynamic traffic — now
only in TL Beton-StB (road), not DIN 1045-2 (VERIFY). AKR needs reactive silica +
alkalis + moisture; break one link: (na) cement ≤ 0.60 % Na2O-eq, safe aggregate
class, or dry detail. Alkali input threshold ~3 kg Na2O-eq/m³.

**Chemical aggression thresholds (groundwater mg/l → XA):** sulfate 200–600 /
600–3000 / 3000–6000 = XA1/2/3; pH 6.5–5.5 / 5.5–4.5 / 4.5–4.0; aggressive CO2
15–40 / 40–100 / >100 mg/l; NH4 15–30 / 30–60 / 60–100; Mg2+ 300–1000 /
1000–3000 / >3000; soil sulfate mg/kg 2000–3000 / 3000–12000 / >12000. Worst
value governs; two in upper quarter of a band → next class. Baumann-gully field
test ≈ 200 → XA1.

**Waterproof structure (WU, DAfStb guideline):** usage class A (no damp spots) /
B (dark patches OK); load class 1 hydrostatic / 2 no pressure. "High resistance
to water penetration" recipe (t ≤ 400 mm): w/z(eq) ≤ 0.50–0.60 (VERIFY edition),
min z 280 (binder incl. SCM 270–280), ≥ C25/30. Crack-width culture: ground side
≤ 0.3 mm, air side (XC1) 0.4; early-age fct upper-bound factors 0.65/0.75/0.85
at 3/5/7 d for thick sections (WU-RL — VERIFY).

**BBQ classes (DIN 1045-1000, new 2023/24):** every member → Planungsklasse /
Betonklasse / Ausführungsklasse at level N/E/S → BBQ-N/-E/-S; Betonfachgespräch
(concrete specialist meeting) mandatory for BBQ-E/S; coordinator + concrete
concept + QA plan in tender. VERIFY adoption status per Bundesland — this is the
biggest recent change in German concrete specification.

**Minimum cover (EC2-1-1/NA, durability cmin [mm], design working life 50 y):**

| Class | cmin,rebar | cmin,tendon | Δc_dev |
|---|---|---|---|
| X0 | 10 (unreinforced — VERIFY) | — | 10 |
| XC1 | 10 | 20 | 10 |
| XC2 | 20 | 30 | 15 |
| XC3 | 20 | 30 | 15 |
| XC4 | 25 | 35 | 15 |
| XD1–3 / XS1–3 | 40 | 50 | 15 |
| XF | +10 over XC/XD/XS value | | (VERIFY NA footnote) |
| XM | sacrificial layer on top | | |

cmin ≥ bar Ø and ≥ 1.25·dmax; −5 mm allowed if concrete 2 classes above the
exposure minimum (not XC1; VERIFY); 100-year life: +5 mm (XC) / +10 mm (XD/XS,
VERIFY NA). Bond-driven cover is a separate table — see concrete-detailing.

## 4.10 Concrete mix design (k-value method, per 1 m³)

1. **Exposure limits:** collect max w/z, min class, min z, min z credited,
   min air from the strictest class.
2. **Required strength:** governs = max(static class, exposure min);
   fcm ≥ fck + production tolerance (Vorhaltemaß ~6–12 N/mm²; 12 without
   initial statistical tests — VERIFY lab value). Convert to dry-cube
   (÷0.92 ≤ C50/60, ÷0.95 HSC).
3. **w/z from Walz diagram** (fcm,dry,cube(28 d) vs w/z curves for cement
   28-d mortar strength N28 = class + 10, e.g. 42.5 → 52.5): governing
   w/z = min(Walz, exposure cap). Exposure-governed → over-strength →
   cheaper cement possible.
4. **Water demand:** standard gradation line (A/B/C per Dmax), compute k and
   D-Summe, read chart: e.g. B16 (k 3.66, D 534) ≈ 160/180/200 kg/m³ for
   F1/F2/F3; C32 ≈ 170/190/210; ±20 for unfavourable aggregate suction
   (typical ranges per national workbook — VERIFY against current DIN 1045-2
   charts or trial mix).
5. **Binder + SCM:** z = w/(w/z); credit SCMs with k: (w/z)eq = w/(z + k·f + 1·s);
   respect max-credit contents, then check min z and min z-with-credit.
   GGBS not combined with FA/SF for crediting.
6. **Paste volume check** (≥ F3 and ≥ C25/30): Vl = Σ(mass/true density) ≥ table §4.7.
7. **Aggregate:** Vg = 1000 − (Vl + entrapped air 1–2 %); per fraction
   g = Vg·A·ρR; surface-moisture correction (2 iterations); trial mix adjusts.

Worked logic (settlement tank): C40/50 + XC4/XF3/XA1 → w/z 0.50 governs; fcm
50+6=56 → dry 60.9 → Walz ≈ 0.50; k 3.68, D 532 → w 205; SF 5 %+FA ≤30 % z → z
350, f 105, s 17.5 kg/m³; paste 370 l/m³ ≥ 280; aggregate Vg = 1000−(370+15);
moisture-corrected w 199.5 kg/m³.

## 4.11 Mortar (Mörtel)

Mörtel = concrete with Dmax ≤ 4 mm (EN 206 definition). Two regulatory arms:
masonry mortar **EN 998-2**, plaster mortar **EN 998-1**, screed **EN 13813**,
tile adhesive **EN 12004** — CE/DoP each; design uses national groups.

| designation | scope |
|---|---|
| MG I / II / III (DIN V 18580 legacy, still the workhorse in EC6 NA tables) | mortar strength groups for masonry; normal mortars M 2.5 / 5 / 10 / 20 (N/mm² compressive) |
| Dünnbettmörtel DM (thin bed, 1–3 mm) | plan blocks (KS, PBC, HLzW), EN 998-2 decl. M…; higher bond shear fkv = 0.22 N/mm² |
| Leichtmörtel LM 21 / LM 36 | light insulating masonry (PBC, HLz), density ≤ 0.7/1.0 kg/dm³ |
| Werkmörtel (factory, EN 998-2) | if declared properties incomplete → downgrade mortar group (DIN 105-100/20000-4xx product rules) — VERIFY current note |
| Kalkzementmörtel / Kalkgips etc. | render families per EN 998-1, CS classes §4.12 |

Practical: cement mortar unit weight 19–23 kN/m³; lime mortar 12–18; gypsum
mortar 12–18; fresh mortar +1; water-retention agents (cellulose ethers 0.2–0.4 %)
keep w/b constant on suction backgrounds (tile adhesive good loss < 5 %, plaster
2–3 % on blotting test); polymer-modified (dispersion powder) mortars = tile
adhesives, WDVS base coats, self-levelling; shrinkage-compensated and rapid
grades exist (CAC-based — not for structural concrete contact: pH drop +
conversion porosity).

## 4.12 Masonry units (Mauerwerkssteine)

Product standards: **EN 771-1** clay (Ziegel + DIN 105-100/20000-401),
**-2** calcium silicate (KS + V 106/20000-402), **-3** concrete (LB/NB +
DIN V 18151-100/20000-403), **-4** autoclaved aerated concrete (PBC +
DIN EN 771-4/20000-404); natural stone EN 771-9 (see geotechnics-foundations
for stone, VERIFY). Design: DIN EN 1996-1-1 + NA.

Formats (DIN 4172/DF system): NF 240×115×71; DF 240×115×113; 2DF 490×240... ;
HF = half-format family; XL plan stones (KS-XL 333/499 mm long);
Lochanteil: Hochloch 15–50 % of bed area; Hohlblock/Plan blocks ≤ 1 m long;
Vollziegel solid; Vormauer facing; Dämmziegel/HLzW with insulating fill;
Riemchen slips.

**fmk characteristic compressive strength (N/mm²), German NA (EC6) — HLz A/B/E +
T1 + KS-hollow/HB (normal mortar M2.5/M5/M10/M20):**

| stone class | M2.5 | M5 | M10 | M20 |
|---|---|---|---|---|
| 4 | 2.1 | 2.4 | 2.9 | — |
| 6 | 2.7 | 3.1 | 3.7 | — |
| 8 | 3.1 | 3.9 | 4.4 | — |
| 10 | 3.5 | 4.5 | 5.0 | 5.6 |
| 12 | 3.9 | 5.0 | 5.6 | 6.3 |
| 16 | 4.6 | 5.9 | 6.6 | 7.4 |
| 20 | 5.3 | 6.7 | 7.5 | 8.4 |
| 28 | 5.3 | 6.7 | 9.2 | 10.3 |
| 36 | 5.3 | 6.7 | 10.6 | 11.9 |
| 48 | 5.3 | 6.7 | 12.5 | 14.1 |
| 60 | 5.3 | 6.7 | 14.3 | 16.0 |

(Stone class = min unit strength N/mm²; caps at weak mortar are real EC6
behaviour, not a typo. fmd = fmk/γM, γM = 1.5 simplified method — VERIFY NA
current method factors 1.5/2.0/2.2.)

Other unit families (same mortar columns):

| family | highlights |
|---|---|
| HLz W/T2-4/LLz (insulating fill etc.) | class 12 → 3.1/4.0/4.5/5.0; class 16 → 3.7/4.7/5.3/5.9; HLzW/T4 capped lower (3.1/4.0/4.5/5.0) |
| Vollziegel / KS-Voll / Vollblock | 8 → 4.2/4.7; 12 → 5.4/6.0/6.7/7.5; 24 → 8.8/9.9/11.0/12.4; 36 → 10.2/11.4/12.7/14.3; 60 → 10.2/11.4/15.1/16.9 |
| KS thin-bed (XL / XL-N,E / P) | XL: 12 → 9.4; 20 → 12.9; 28 → 16.0 cap; XL-N/E: 12 → 7.0; 28 → 13.8; P: 16 → 6.6; 36 → 7.6 cap |
| LM (light mortar, brick/KS) | 4 → 1.6/2.2; 8 → 2.5/3.3; 12–28 → 3.0/3.3 caps |
| LB (concrete masonry) Hbl/Hbn | 2 → 1.4/1.5/1.7; 8 → 2.9/3.7/4.0; 12 → 2.9/4.8/5.1 (M2.5 caps at 2.9!) |
| LB solid V/Vbl | 4 → 2.5/2.7/3.0; 8 → 3.4/4.5/5.0; 12 → 3.4/6.1/6.7; 16 → 3.4/6.1/8.3; 20 → 3.4/6.1/9.8 |
| LB Vn/Vbn/Vm/Vmb | 4 → 2.8/2.9; 8 → 3.6/4.7/5.0; 16 → 3.6/6.0/8.0; 20 → 3.6/6.0/9.1 |
| PBC (AAC) thin-bed DM | 2 → 1.8; 4 → 3.0; 6 → 4.1; 8 → 5.1 |

- Initial modulus: Ec,calc = coefficient·fk — brick 1100 (950–1250), KS 950,
  LB 950, concrete masonry 2400 (2050–2700), PBC 550 (500–650); fk = fmd·γM.
- fvk initial shear (plain joints): M2.5–M20 normal mortar 0.08/0.18/0.22/0.26
  N/mm²; DM 0.22; LM 0.18; fvRd = (fvk + α·σd)^… per EC6 (σd cap 5·fk? — VERIFY
  NA formula constants; use masonry-construction skill).
- Plaster mortars EN 998-1: CS I–IV (0.4–2.5 / 1.5–5.0 / 3.5–7.5 / ≥ 6.0 N/mm²),
  Wc water penetration ≤ 0.5 (Wc1)/≤ 2 (Wc2) kg/m²·min^0.5, WdT T1 ≤ 0.1 /
  T2 ≤ 0.2 W/(m·K); lightweight render classes; Qualitätsstufen Q1–Q4 (DIN
  18550/EN 13914). Tile substrate needs ≥ 2.0 N/mm² and ρ0 ≥ 1000 kg/m³ (no
  pure lime/earth without measures).
- Movement joints (unreinforced, non-loadbearing): brick 12 m, KS 8, concrete/
  LB 6, PBC 6, natural stone 12 (workbook guidance — VERIFY against EC6/NA and
  project exposure).
- **Sustainability one-liner:** brick 150-y service life, ~94 % recyclable,
  firing 850–1250 °C (burnt-clay GWP moderate); KS = lime + quartz sand,
  low firing energy (autoclaved); PBC = lowest GWP/m² wall of the family but
  lowest strength; clay blocks unburnt (−198 to +99 kg CO2-eq/m³ depending on
  drying — EPD values, dated).

## 4.13 Structural steel (Baustahl)

Standards: **EN 10020** (classification), **EN 10025** hot-rolled products and
structural steel, **EN 10210** hot-finished hollow sections, **EN 10219**
cold-formed hollow sections; execution EN 1090 (EXC classes); design EN 1993 + NA.
Steel = Fe alloy with C < 2 % (cast iron ≥ 2.06 % not hot-workable, brittle:
compression 500–1100, tension 100–400 N/mm²); stainless: Cr ≥ 10.5 %, C ≤ 1.2 %.
E = 210,000 N/mm², αT = 12×10⁻⁶/K, ρ = 7850 kg/m³, unit weight 77–78.5 kN/m³.
Capacity falls sharply above ~500 °C (charring/intumescence/cooling design per
fire skill); ductility vs C: 0.1 % C soft/tough, 0.6 % C hard/poor formability;
weldability worsens with C-equivalent (preheat rules per EN 1011 — VERIFY).

**Strength grades (EN 10025-2, nominal yield fy / tensile fu, N/mm², thickness
≤ 16 mm, non-alloy quality — table from standard practice; VERIFY per product
EN and thickness, values drop with t):**

| Grade | fy | fu | Notes |
|---|---|---|---|
| S235 (JR/J0/J2) | 235 | 360–510 | easiest to weld, light structures, sheets |
| S275 | 275 | 430–560 | intermediate, VERIFY current availability (often skipped) |
| S355 | 355 | 470–630 | standard for buildings/bridges (J2/NL sub-zero toughness common) |
| S420 | 420 | 520–680 | hollow sections, heavier plates |
| S460 | 460 | 550–725 | high-strength option — needs execution know-how |
| S500/S550/S620 (QR plate, EN 10025-4/6) | 500/550/620 | — | VERIFY scope; quenching/tempering |
| S690 (QL/QR) | 690 | 760–940 | special; fatigue/welding care, EXC up |

- Quality suffixes = impact-test temperature: +JR 20 °C, +J0 0, +J2 −20, +K2…;
  NL = normalized; M = thermomechanical; Q = quenched+tempered.
- Weathering steels (EN 10025-5, S355J0W etc.) = protective patina, detail for
  drainage; hot-dip galvanizing = decades of protection, often beyond member
  life; duplex (galv + paint) for C5 (EN ISO 12944 — VERIFY).
- Production CO2: integrated BF route (coke, ~2 t CO2/t steel, order of
  magnitude — VERIFY against current worldsteel system boundary) vs EAF 100 %
  scrap (power-mix dependent, far lower) vs H2-DRI + EAF (near-zero on green
  power; slag chemistry differs, DRI-slag use in construction under research);
  LESS/label tiers by GHG intensity emerging; steel infinitely recyclable
  without quality loss; bolted connections = Design for Disassembly.

## 4.14 Reinforcement (Betonstahl) — DIN 488

Products (DIN 488-1/-2/-3/-5): ribbed bars (Betonstabstahl, straight/coil),
welded meshes (Betonstahlmatten — Q equal, R unequal orthogonal sections),
open-web girders (Gitterträger), wire (Bewehrungsdraht, cold-worked, factory
cages only). Bond: Formverbund of ribs governs (cone breakout possible);
Haft/Reibungsverbund ignored in design.

| Grade | form | f_yk (N/mm²) | f_uk/f_yk | ε_uk | ductility class |
|---|---|---|---|---|---|
| B400A/B | bars (legacy grades BSt 400/420 superseded — VERIFY any current DIN 488 part still carrying B400) | 400 | see product standard | — | A normal / B high |
| B500A | bars φ6–40, meshes | 500 | ≥ 1.05 | ≥ 2.5 % | normal (N) |
| B500B | ribbed bars, meshes φ4–16 | 500 | ≥ 1.08 | ≥ 5.0 % | high (H) — redistribution allowed |
| B500C | special elongation | 500 | ≥ 1.08 | ≥ 7.5 % | VERIFY inclusion in current DIN 488 |

Design values (EC2 German NA): fyd = fyk/γs = 500/1.15 = **435 N/mm²**;
ftd ≈ 456; E = 200,000 N/mm²; εyd = 2.175 ‰; εud 25 ‰ (A) / 50 ‰ (B)
characteristic → /γs; redistribution limits linear: B 30 %, A 15 % (VERIFY —
this pairs with ductility class in current NA).

**Nominal bar data (B500):**

| φ (mm) | A (cm²) | mass (kg/m) | | φ | A (cm²) | mass |
|---|---|---|---|---|---|---|
| 6 | 0.283 | 0.222 | | 16 | 2.01 | 1.58 |
| 8 | 0.503 | 0.395 | | 20 | 3.14 | 2.47 |
| 10 | 0.785 | 0.617 | | 25 | 4.91 | 3.85 |
| 12 | 1.131 | 0.888 | | 28 | 6.16 | 4.83 |
| 14 | 1.54 | 1.21 | | 32/40 | 8.04/12.57 | 6.31/9.87 (VERIFY 32/40 areas — computed π·φ²/4) |

As [cm²/m] @ spacing 10 cm: φ6 2.83 · φ8 5.03 · φ10 7.85 · φ12 11.31 · φ16
20.11 · φ20 31.4 · φ25 49.1; @15: 1.89/3.35/5.24/7.54/10.26/13.41/20.9; @20:
half of @10 (grid complete in source for 5–18 cm).

Prestressing steel (EC2): ST 1470/1670, 1570/1770, 1660/1860 (wire/bar/strand);
fpd = fp0,1k/1.15 e.g. 1600→1391, 1860→1617; E 195,000–205,000; relaxation
classes 1/2 (initial 1000 h 2.5–13 %, extrapolated ×1.73–2.0 to 50/100 y —
VERIFY class mapping); stress-corrosion risk with chlorides → do not detail
prestressing into XD/XS without measures (concrete-detailing skill).
Weldability of rebar: only designated grades (C4/C5 suffixes old system; EC2-NA
3.2.5 process list RA24, E111, MAG135/136, RP21, FR42) — VERIFY current DIN 488
weldability declarations; Ø difference in welds max one size.

## 4.15 Timber (Holz)

Standards: **EN 338** strength classes, **EN 336** sizes, **EN 408/1915** grading,
**DIN 4074** visual grading (S7/S10/S13 ↔ C18/C24/C30/35), **EN 14080** glulam,
**EN 16351** CLT (2025-07 — VERIFY edition), **EN 13985** LVL, **EN 636** plywood,
**EN 300/312** OSB/particleboard; design EN 1995 + NA; protection **DIN 68800-1/-2** + EN 350.

Material reality: anisotropic (strongest tension ∥ grain); cell wall = cellulose
40–50 % (tension) + hemicellulose 20–25 % + lignin 20–30 % (compression
stiffness); extractives drive natural durability (density ≠ durability);
fibre saturation point FSP ≈ 23–35 % (use 30 %): shrinkage only below FSP;
movement tangential ~10 %, radial ~5 %, axial 0.1–0.3 % total dry→FSP;
moisture effect in service 8–18 %: +1 % u → −6 % compression, −4 % bending,
−3 % axial tension; duration of load: long-term strength ≈ 60 % of short-term
(→ kmod). E ∥ softwood ≈ 11,000 MPa (C24), hardwood 12,000; ⊥ 370/800 MPa.
αT ∥ 2.5–5, ⊥ 25–60 ×10⁻⁶/K.

**Conifer classes EN 338 / EN 1995 (N/mm²; ρ kg/m³; γ 3.5–5.0 kN/m³):**

| | C18 | C24 | C30 | C35 | C40 |
|---|---|---|---|---|---|
| fm,k | 18 | 24 | 30 | 35 | 40 |
| ft,0,k | 10 | 14.5 | 19 | 22.5 | 26 |
| ft,90,k | 0.4 | 0.4 | 0.4 | 0.4 | 0.4 |
| fc,0,k | 18 | 21 | 24 | 25 | 27 |
| fc,90,k | 2.2 | 2.5 | 2.5 | 2.7 | 2.8 |
| fv,k | 3.4 | 3.5 | 4.0 | 4.0 | 4.0 |
| E0,mean | 9000 | 11000 | 12000 | 13000 | 14000 |
| E0,05 | 6000 | 7400 | 8000 | 8700 | 9400 |
| E90,mean | 300 | 370 | 400 | 430 | 470 |
| Gmean | 600 | 690 | 750 | 810 | 880 |
| ρk / ρmean | 320/380 | 350/420 | 380/460 | 390/470 | 400/480 |
| γ (kN/m³) | 3.8 | 4.2 | 4.6 | 4.8 | 5.0 |

C14/C16/C22/C27 exist in the class system (unit weights 3.5/3.7/4.1/4.5 kN/m³
digested; strength rows not in source — VERIFY from EN 338 when needed; C16 ≈
interpolate between C18 columns minus ≈12 %). Grading mapping: S7→C18 (Fichte/
Kiefer; Tanne/Lärche/Douglasie C16), S10→C24, S13→C30, Douglasie C35.
Hardwood D30 (Eiche) / D35 / D40 / D60 (Buche): fm,k 30/35/40/60; ft,0 18/21/24/
36; fc,0 24/25/27/33; fc,90 5.3/5.4/5.5/10.5; E0,mean 11000/12000/13000/17000;
ρk 530/540/550/700.

**Glulam EN 1194 (combined/homogeneous):**

| | GL24h | GL28h | GL32h | GL36h |
|---|---|---|---|---|
| fm,k | 24 | 28 | 32 | 36 |
| ft,0,k | 16.8 | 19.6 | 22.4 | 25.2 (digest rows garbled — VERIFY vs EN 1194) |
| fc,0,k | 24 | 28 | 30 | 32 |
| fc,90,k | 2.5 | 2.5 | 2.5 | 2.5 |
| ft,90,k | 0.5 | 0.5 | 0.5 | 0.5 |
| fv,k | 3.5 | 3.5 | 3.5 | 3.5 |
| E0,mean | 11500 | 12600 | 13600 | 14200 |
| ρmean | 420 | 460 | 480 | 490 |

Combined grades GL24c–32c (fm 24/28/30/32, E0,mean 11000/12500/13000/13500)
exist; curved members and flat-use glulam get NA adjustments (bending strength
for flat use +? and size factor kh = (180/h)^0.2 ≤ 1.25 style — VERIFY exact NA
formula before use).

**Modification factors (German NA tables, indicative — VERIFY current NA):**

kmod, solid timber/BSH/LVL3/plywood-3: NKL1 / NKL2(NKL3):
ständig 0.60/0.50 · mittel 0.80/0.65 · kurz 0.90/0.70 · sehr kurz 1.10/0.90
(wind → between kurz and sehr kurz; NKL3 = NKL2 values — VERIFY). Panels lower: BSP/Balkenschichtholz 0.60·? pattern: ständig 0.40/0.30;
OSB/3,4 0.40/0.30; gypsum board 0.20→1.10 ladder (GKB/GKF: st 0.20, lang 0.40,
mittel 0.60, kurz 0.80, sehr kurz 1.10); GKFI/fibreboard NKL2: 0.15/0.30/0.45/
0.60/0.80; cement-bonded chipboard 0.30/0.20.

kdef: solid wood/BSH/LVL3/ply EN636-3: NKL1 0.60, NKL2 0.80, NKL3 2.00;
BSP/Balkenschichtholz/LVL2/SWP: 0.60/0.80; OSB/2: 2.25 (only NKL1); OSB/3,4:
1.50/2.25; particleboard P6/P7: 1.50/(2.25); cement-bonded 2.25/3.00;
fibreboard hard 3.00; gypsum board 3.00; GKBI/GKF fibre: 3.00/4.00 (VERIFY
NKL3 dashes). γM: timber and panels 1.3; connections steel parts 1.1 (simplified
bolt-group) / 1.3 (exact) — VERIFY NA current.

Service/use conditions: NKL1 u ≤ 12 % (heated interiors), NKL2 ≤ 20 % (covered),
NKL3 > 20 % (weather). Drying to 9–15 % for enclosed members; supply moisture ≈
in-service equilibrium; shrinkage example: 500 mm board, Δu 18 % → tangential
−36.9 mm vs radial −10 mm — grain layout decides warp (Rift/quarter-sawn most
stable; Herzboard pith cracks; Seitenbrett cupping).

**Wood-based panels:** glulam ≥ 3 lamellae finger-jointed, quality placement
(outer = tension grade); CLT cross-laid ≥ 3 layers; plywood odd layers, adjacent
90° ("Sperrwirkung"), Stabsperrholz vs face print-through; OSB long oriented
strands, strong axis; particleboard graded density, flat- vs strand-pressed
(weak in flat bending — must be faced); HDF/MDF isotropic smooth surfaces;
adhesives PF/UF standard, MEL/RF wetter, PUR/epoxy wood–metal.

**Sustainability one-liner:** 1 m³ wood ≈ 0.5–1 t CO2-eq stored (branch rule);
GWP A1–A3 incl. biogenic C: KVH ≈ −712, BSH ≈ −650, CLT ≈ −632, OSB ≈ −565,
MDF ≈ −676, parquet +50 kg CO2-eq/m³ (branch data 2012 vintage — VERIFY via
manufacturer EPDs); whole-building 30–45 % GWP saving vs mineral construction
typical; hotspots fasteners/resins/drying; certified forestry (PEFC/FSC) +
EUDR due-diligence for legality.

## 4.16 Thermal insulation (Dämmstoffe)

Product standards EN 13162–13171 (+14315–14318 in-situ, 14509 sandwich): CE per
DoP with declared lambda_D; design value lambda_B = lambda_D·factor (DIN 4108-4:
×1.03 min +1 mW; ×1.05 min +2; ×1.10 min +3; ×1.20; ×1.23 by product family).

| Product (EN) | lambda_D range W/(m·K) | lambda_B typical | mu | Burn behaviour (EN 13501-1, typical — VERIFY product DoP) |
|---|---|---|---|---|
| Mineral wool MW (13162) | 0.030–0.050 | 0.031–0.052 | 1 | A1 (stone wool) / A2-s1,d0; lamella-mat boards A2 |
| EPS (13163) | 0.030–0.050 | 0.031–0.052 | 20–100 | E (D-s2,d0 "flammability-retarded" grades standard for WDVS) |
| XPS (13164) | 0.022–0.045 | 0.023–0.046 | 80–250 | E class typical; verify |
| PUR/PIR (13165) | 0.020–0.040 | 0.021–0.041 | 40–200 | E–B-s1,d0 depending facing |
| Phenolic PF (13166) | 0.020–0.035 | 0.021–0.036 | 10–60 | B-s1,d0 typical, verify |
| Foam glass CG (13167) | 0.037–0.055 | 0.038–0.057 | ∞ | A1 |
| Expanded perlite (13169) | 0.045–0.050 | 0.046–0.052 | 5 | A1 |
| Cork ICB (13170) | 0.038–0.055 | 0.040–0.058 | 5–10 | E typical |
| Wood fibre WF (13171) | 0.032–0.060 | 0.034–0.063 | 3–5 | E (class-treated B available) |
| Wood wool (13168) | 0.060–0.100 | 0.063–0.105 | 2–5 | B-s1,d0 cement-bonded |
| Insulating render T1/T2 | 0.12 / 0.24 | — | 5–20 | A1/A2 |
| Aerogel/mat | ~0.014–0.020 | +10 % | — | A2–B, VERIFY |

- cp: mineral ≈ 840–1000 J/(kg·K); organic/bio ≈ 1600–2100 (wood ~1600–2100,
  cork ~1800 — indicative); low density → low areal heat storage (summer
  protection penalty vs massive, see building-physics-thermal-moisture).
- Application codes DIN 4108-10 (DAD/DUK/DEO/PW/PB/WAB/WAP/WZ/WH/WI...) with
  compressive (dk…dx), water uptake (wk/wf/wd), tensile (zk/zg/zh) classes:
  inverted roof DUK ≥ 70 kPa frost-tight; perimeter PW: XPS/CG/foam glass +
  protection board; WDVS = ETA system approval, not product only.
- **Sustainability one-liner:** fossil foams carry blowing-agent GWP and are
  circularity-poor (separate cleanly, no bitumen-foam laminates in nawaRo
  builds); MW/A2 highest fire-safety for tall WDVS; bio-based (WF, cork, hemp,
  reed, paludiculture boards λ 0.037–0.061) low PEI, hygric buffer; same-U
  comparison can invert mass-vs-insulation balance (AAC ~2× GWP of RC+EPS
  composite per one worked example — illustrative).

## 4.17 Glass (Glas)

Base products **EN 572**: float (-2), polished wired (-3), drawn flat (-4),
ornamental (-5), wired ornamental (-6), profiled (-7); borosilicate EN 1748.
Toughened ESG (EN 12150), thermally strengthened TVG (EN 1863), chemically
strengthened CVG (EN 12337); laminated VSG (EN ISO 12547, PVB/SGP/EVA interlayer).
Design: **DIN 18008-1…-6** (introducted via MVV TB; VERIFY editions) — not EN
1999 for building glazing in DE.

| Property | float FG | TVG | ESG |
|---|---|---|---|
| fck bending (N/mm²) | 45 | 70 | 120 |
| gamma_G material factor (18008) | 1.8 | 1.7 | 1.4 |
| kmod load duration | ständig 0.25 · mittel 0.40 (snow/climate) · kurz 0.70 (wind) | same | same |
| E (MPa) | 60000–73000 (use 70000 design) | | |
| rho / lambda / mu | 2500 kg/m³ / 1.0 W/(m·K) / ∞ | | |
| alpha_T | 3–9 ×10⁻⁶/K (use ~9 float) | | |

Sizes: float up to 3.21×6.00 m, t 2–25 mm; ESG 2–19/25; point-fixed holes only
in TVG/ESG per 18008-3; edge work classes KG/KGS/KMG/KGN/KPO matter for strength
(grinded > cut). Fall-through/walk-on/balustrade categories per 18008-4/-5/-6
(approved make-ups tables — VERIFY current edition; e.g. walk-on 8ESG/1.52PVB/
10ESG class patterns). SSG silicone joints = abZ route (ETA-02/ETAG 002 for
structural sealants — VERIFY). Insulating glass unit edge = warm-edge spacer,
but glass circularity at EoL is poor (mixed cullet → downcycle; flag in
sustainable-construction).

## 4.18 Bitumen, asphalt, sheet waterproofing

- Bitumen: thermoplastic hydrocarbon binder; ρ ≈ 1050 kg/m³, lambda 0.70 W/(m·K),
  mu ≈ 5·10⁴; aged/oxidised = brittle; never exposed permanently to UV/heat
  without protection. Sheet goods: DIN EN 13707 (bitumen roofing), 13969
  (below-ground sheets), legacy DIN 52129/52131-33; torch/weld-on, protective
  layers; unit weights laid 0.04–0.07 kN/m².
- Asphalt: Gussasphalt (mastix, poured, 23 kN/m³, DIN 18500 series), Asphaltbeton
  (hot-mix layers, road/deck, 24 kN/m³), mastic asphalt floors ≥ 7 mm, λ 0.70;
  unbound/bound layers per ZTV-StB/TL — see geotechnics/road scope.
- PM membranes: PVC-P (1.5 mm ≈ 0.02 kN/m²), TPO/FPO, EPDM (mu ~6000, ρ 1150),
  bitumen-polymer; liquid-applied per EN 1504-2 (DK/PA classes) or abZ;
  protection: no bitumen foams in nawaRo construction, separable layers,
  splash zone WAS + driving-rain classification (see building-physics-thermal-moisture skill).
- Use-class anchors: waterproofing against soil — legacy DIN 18195 replaced by
  Abdichtungsnormen family DIN 18531–18535 + DAfStb WU (VERIFY current split).

## 4.19 Polymers and sealants (Kunststoffe, Dichtstoffe)

| Family | Structure | Behaviour | Building examples |
|---|---|---|---|
| Thermoplaste | linear/branched | re-softenable, weldable, solvent-swell; amorphous (PS, PC, PMMA, PVC) vs semicrystalline (PE, PP, PA — stiffer, chemically better) | pipes, frames, membranes, profiles |
| Duroplaste | dense covalent network | rigid, no melting, decompose; chem/heat resistant, not weldable (EP, PUR, PF/UP) | resins, adhesives, GRP, injection |
| Elastomere | loose cross-link | reversible strain 8–10×, swelling (EVA, NR, BR, EPDM, polysulfide, silicone) | joint sealants, gaskets, foams |
| Silicone | Si-O backbone | oils → rubbers → resins by chain; heat/UV stable | facade/joint sealants, SSG |

- Tensile strength: thermoplastics 2–70, duroplastics 40–80, **GFRP 200–630
  N/mm²**; strong creep/relaxation, time-temperature superposition; solvent
  swelling under stress (microcracks); fire: combustible, smoke — EN 13501-1
  classification always check DoP.
- Sealant movement classes per ISO 11600 (E..L..M, 12.5/20/25/50 % capability);
  modulus: low for facade joints (LM), high for structural glazing (H, SSG via
  ETA/abZ); joint width rule ~2× expected movement, min 6 mm, max ~12.5×depth
  (construction-detailing skill).
- Construction chemical roles (mortar/adhesive context): dispersion-powder
  modified thin-beds, EP injection anchors/repair laminates, PU injection
  (low-viscosity PUR at ≤ 6 °C for crack sealing — water-reactive types for
  wet cracks), silane/siloxane hydrophobation, curing films.
- **FRP/carbon textile:** no corrosion → cover down to ~10 mm, sections −50 %
  material ≈ −30 % CO2 (DE: DAfStb carbon-textile guideline 2024 — VERIFY; ETA
  route for bars/meshes; brittle, no yielding → different detailing logic).

## 4.20 Master material property table (physics + structural inputs)

Consolidated from building-physics-thermal-moisture design values (DIN 4108-4/ISO 10456, T3 tier:
use declared producer values for proof) and load tables (EN 1991-1-1/NA + legacy
DIN 1055). Units: rho kg/m³; lambda W/(m·K); mu water-vapour diffusion number;
cp J/(kg·K); gamma kN/m³; E MPa; alpha ×10⁻⁶/K.

| Material | rho | lambda | mu | cp | gamma | E | alpha |
|---|---|---|---|---|---|---|---|
| Normal concrete (dry) | 2200–2400 | 1.65–2.0 | 70–130 | ~1000 | 24 | 27000–37000 | 8–12 (use 10) |
| RC with 1–2 % steel | 2300–2400 | 2.3–2.5 | 80–130 | ~1000 | 25 | as above | 10 |
| Lightweight concrete closed D1.6 | 1600 | 1.0 | 70–150 | 1000 | 16–18 | ~18000 VERIFY | 10 |
| AAC (Porenbeton) 500 / 600 | 500/600 | 0.14/0.18 | 5–10 | 1000 | 5.0/6.0 | ~1500–2000 (Ec 550·fk) | 6–10 |
| Solid brick 2000 | 2000 | 0.96 | 5–10 (perforated) | 1000 | 20–22 | 1100·fk | 6–10 |
| Hollow brick HLz 1000 filled | 1000 | 0.42–0.45 | 5–10 | 1000 | 10 | — | — |
| Sand-lime KS 2000 | 2000 | 1.1 | 15–25 | 1000 | 20 | 950·fk | 6–10 |
| Concrete masonry LB 2000 | 2000 | 1.3 | 5–15/20–30 | 1000 | 20–22 | 2400·fk | 6–10 |
| Natural stone (dense) | 2600–3000 | 2.3–3.5 | 200–250/∞ | 800–1000 | 26–30 | 20000–70000 | 5–8 |
| Structural timber (C24) | 350–480 | 0.12–0.13 | 20–50 (∥/⊥ varies) | 1600 | 3.8–4.2 | 11000 ∥ / 370 ⊥ | 2.5–5 ∥ / 25–60 ⊥ |
| Hardwood D30–D70 | 530–840 | 0.13–0.18 | 20–50/200 | 1800–2300 | 6.4–10.8 | up to 17000 | as above |
| Plywood/OSB | 300–700 | 0.09–0.17 | 40–250 | 1800–2000 | 5–7 | anisotropic ~4000–12000 | — |
| Wood fibre insulating board | 250–800 | 0.07–0.18 | 2–20 | 1700–2100 | 2.5–8 | — | — |
| Gypsum plaster/boards | 900–1500 | 0.30–0.56 | 4–10 | 1000 | 9–13 | ~1500–4000 | 10–20 VERIFY |
| Cement screed | 2000 | 1.4 | 15–35 | 840–1000 | 20–22 | ~27000 | 10 |
| Cast asphalt (GA) | 2300 | 0.90 | sd ≥ 1500 m | ~900 | 23 | — | — |
| Mastic asphalt ≥ 7 mm | 2000 | 0.70 | ∞ | — | 23 | — | — |
| Mineral wool | 20–200 boards | 0.031–0.052 | 1 | 1000 | 0.2–2 | — | — |
| EPS/XPS/PUR | 15–70 | 0.021–0.052 | 20–250 | 1400 | 0.15–0.7 | — | — |
| Float glass | 2500 | 1.0 | ∞ | 750 | 25 | 60000–73000 | 3–9 (use 9) |
| Clay brick masonry (historic) | 1600–1900 | 0.73–1.0 | 5–10 | 840–1000 | 16–19 | ~1000–1500·fk | — |
| Rammed earth/clay blocks | 1600–2200 | 0.85–1.4 | — | ~1000 | 16–22 | — | — |
| Water / ice | 1000 / 900 | 0.6 / 2.2 | — | 4190 / 2000 | 10 | — | — |
| Steel | 7850 | 50 | ∞ | 450 | 77–78.5 | 210000 (constr.) / 200000 (rebar) | 12 |
| Stainless austenitic | 7900 | 17 | ∞ | 500 | 79 | ~190000 | 17–18 |
| Aluminium | 2700–2800 | 160–200 | ∞ | 880–900 | 27 | 70000 | 20–24 (use 23) |
| Ground (dry→saturated) | 1800–2200 | 0.4–2.0 | 50 | ~800–1700 | 18–22 | — | — |
| Air (still) | 1.23 | 0.025 | 1 | 1008 | ~0 | — | — |

Notes: lambdas are design values (masonry incl. joints); porous materials show
mu low/high; alpha_T concrete moisture-dependent (4.5–14 — use 10).

---

## 5. Durability mechanisms (Dauerhaftigkeit)

Design service life logic: the material must survive the exposure it is detailed
into. Each mechanism has a governing variable the agent can check at spec time.

### 5.1 Carbonation (RC)
CO2 + H2O + Ca(OH)2 → CaCO3; pH < 9.5 → depassivation → **uniform corrosion**
(expanding rust → cracking/spalling; Tutti phases initiation → cracking →
spalling → failure). Needs moisture: fastest at RH ~50–70 %; dry (< ~85 % RH
no reaction medium) or saturated (no O2 ingress) barely carbonates; freely
weathered fastest. Depth law (T4): **d_k = alpha·sqrt(t)**; example 5 mm at
10 y → alpha = 1.58 mm/√a → 11.2 mm at 50 y. Slow with: low w/z, dense/compacted
paste, good curing, more cement, SR cements (slag slows carbonation itself but
worse pH buffer — net by quality); detection on site: phenolphthalein (uncarb.
= red, < pH 9 colourless). Counter: cover ≥ d_k(50 y) + Δc_dev + margin,
or quality (XC4 > XC3), or maintenance/coating.

### 5.2 Chloride attack
Cl− travels in water-filled pores → locally breaks passive film → **pitting**
(Lochfraß): deep craters, little rust, no warning, sudden section loss. Binding:
Friedel's salt (3CaO·Al2O3·CaCl2·10H2O); more binding in slag cements; bound Cl
can re-release on carbonation — only **free water-soluble Cl** is dangerous.
Critical-threshold rule of thumb (T4, not in digested sources — VERIFY against
model codes): ~0.4–0.5 M-% Cl− on cement for initiation, de-icer/sea exposure
dominates via XD/XS. Counter: w/z ≤ 0.45–0.55, CEM III, crack control, cover
≥ 40–50 mm, avoid water traps, maintenance plan for de-iced decks (DE:
Erhaltungszuschlag/ZTV-ING-R routines).

### 5.3 Sulfate attack (XA)
External MgSO4 → gypsum + brucite → **sulfate swelling**; internal: C3A +
CaSO4 + water → ettringite (volume × 7–8 → expansion beyond tensile strength =
crack + pulp). Special: thaumasite (CaO·SiO2·CaSO4·CaCO3·14.5H2O) at low T +
carbonate + moisture — think buried wet elements. Counter per XA1/2/3:
class + w/z table §4.9, SR cement (CEM I C3A < 3 %; CEM III/B ≥ 66–70 % slag),
XH: protective layers (XA3 demands separation: tile/EP/HDPE lining — see §5.7).

### 5.4 Alkali-silica reaction (ASR/AKR)
NaOH/KOH + poorly-crystalline silica (opal, flint, Kieselkreide, greywacke,
some siliceous limestones/glassy volcanics) → swelling gel → net cracking,
white haloes around grains. Needs all three: reactive aggregate + alkalis
(> ~3 kg Na2O-eq/m³) + moisture (WF/WA/WS classes). Break any leg: (na)-cement
≤ 0.60 % eq, classified aggregate (DAfStb Alkali-Richtlinie), dry detail/
waterproofing, or SCM dilution (fly ash/slag reduce effective alkali).

### 5.5 Freeze-thaw (XF)
Ice +9 % volume → hydraulic + osmotic pressure in capillaries (splitting
pressures up to hundreds of N/mm² claimed in T4 literature); damage needs high
saturation + fast cooling + big connected pores; de-icer worsens (brine keeps
reaction going, lowers freezing point — sat. NaCl −21 °C; more meltwater).
Counter: air-entrainment (LP) 4.0–5.5 Vol-% by Dmax table, spacing factor
≤ 0.2 mm philosophy (T4), w/z cap 0.50–0.55, dense surface, avoid ponding
details, XF4 always air-entrained + usually scale-resistant hard aggregate;
carbonation and frost attack the same weak layer (surface quality + curing!).

### 5.6 Chemical dissolution and other mineral damage
Acids (even food-grade lactic/citric on joints over years) and aggressive CO2
leach paste → porosity ↑, strength ↓, exposed aggregate ("washed" look);
sugar/fat/sewage (biogenic H2S → H2SO4 by bacteria, pH can hit 1–2 — sewer
concrete: SR + slope/vent, or lining DIN EN 206 XA3 + protective system).
Salt crystallisation: subflorescence pressure + hygroscopic re-wetting →
efflorescence and spalling (façade render, splash zone); free-lime/free-MgO
(over-10 mm Le Chatelier fail) → delayed expansion. Alkali attack on glass/
asphalt-like phases rare; high service temperature → skip (see fire skill).

### 5.7 Wood decay (DIN 68800, EN 350)
Use classes (DIN 68800-1:2019, T2): **GK0** fully enclosed, dry, permanent
≤ 12–15 % moisture (visible interior members; no chemical protection needed);
**GK1** enclosed, occasional brief wetting, moisture peak (old-beam ends in
masonry = GK2!) — GK1: insect risk Iv; **GK2** above ground, weather-protected
but condensation/wetting possible (covered bridges, beam heads) — P required;
**GK3.1/3.2** direct weather without ground contact (splash posts 3.1; permanently
humid outdoor 3.2) — Iv+P+W; **GK4** fresh/brackish water or ground contact —
Iv+P+W+E (soft rot); **GK5** sea water (termites too) — special species only.
Fungi need u > ~20–30 % (Echter Hausschwamm from 20 % — the dangerous exception);
insects (Nagekäfer, Hausbock, Splintholzkäfer) attack even dry wood — hence GK0–1
Iv requirement; termites = regional (flag for south-west DE and imports).
Natural durability EN 350 classes: 1 very durable (tropicals, Robinie 1–2),
2 durable (Eiche, Rosskastanie, Bankirai), 3 (Kiefer), 3–4 (Lärche, Douglasie),
4 (Fichte/Tanne — class 4 species unsuitable exterior), 5 not durable (Buche,
Esche, Weide — interior only); heartwood/splint matters (Fichte GK0 only;
Kiefer core to GK2; Lärche/Douglasie core to GK3.1; Eiche core to GK3.2;
Dauerhaftigkeit ≠ Dichte).
**Constructional protection rules (first choice, chemistry second):** roof
overhangs/drips; drained ventilated façades with 45° chamfered edges; posts
above splash zone, end grain never sucking from pavement, cap heads; no
capillary gaps at shoes; beam ends ventilated + on separating layer; rounded
exterior edges hold thicker coating; moisture-equilibrium at supply ≈ service;
design for drying faster than wetting. Chemical: KDI salts (metal/glass attack),
oil (carboliteum era), solvent; hazard-class product predicates Iv/P/W/E as above.

### 5.8 Corrosion of metals (non-RC)
Steel: rust needs O2 + H2O + electrolyte; C1–C5 / Im1–Im3 corrosivity classes
(EN ISO 9223/12944 — VERIFY); galvanizing ~10 µm/yr consumption logic → layer
≥ 80–100 µm for decades; stainless (Cr ≥ 10.5 %) pitting in chloride splash —
austenitic grades still crevice-risk; Al needs ventilation behind cladding
(pH > 9 attacks Al — no direct embedment in fresh mortar/concrete without
coating); bimetallic contacts → insulation; Cu/Zn runoff stains.

---

## 6. Product regulation (Bauproduktsrecht, DE-centric)

- **CE marking under CPR (EU) 305/2011**: harmonized technical specification =
  hEN or ETA/EAD; manufacturer draws up **DoP (Leistungserklärung)** declaring
  performance (fck, lambda_D, fire class, ...); AVCP system (1+, 1, 2+, 2, 3, 4)
  defines third-party involvement (cement 1+; aggregate 2+; rebar 1+...);
  placed on market = CE + DoP + traceability. UK CA/other markets separate.
- **National usability**: CE proves declared properties, NOT fitness for the
  regulated use. German route: product in Bauregelliste A (harmonized, technical
  rule = hEN + MVV TB introduction) → usable; not harmonized → **abZ** (general
  testing/inspection certificate by DIBt) or **ZiE/aBG** (approval in individual
  case by Bauaufsicht) + **Ü-Zeichen** surveillance mark; not approval-needed
  list (Bauregelliste C /MVV TB Anh. D) → generic proof of usability. Austria:
  üA/Ömark-ish route + list of approved products (VERIFY current names);
  Switzerland: list of approved construction products, ETA route, no CE duty
  per se.
- **Structural concretes**: use cements/SCM/admixtures from the **DAfStb
  approved-products lists** (Zementliste / Betonzusatzstoffliste — VERIFY
  current publications); fibres, new binder classes (EN 197-5), RGK beyond
  BK-N, most specialty concretes (UHPC, lightweight insulating structural
  with declarations) historically ride abZ/ETA paths; execution to EN 13670/
  DIN 1045-3 + factory production control of precast (DIN 1045-4/-40/41).
- Seismic/fire products: special approval families (ETA for anchors, EN 13501
  classes into Bauregelliste) — cross-reference relevant skill.
- Agent duty: when specifying, state which route the product takes (CE/hEN,
  abZ, ZiE) and flag "VERIFY national list" for anything off the beaten path
  (e.g. recycled-content declarations, bio-based panels lacking harmonized
  standards).

---

## 7. Recycled and secondary raw materials

- **RC aggregate (RGK)**: Germany 2022 13.3 % recycled share of 564 Mt used,
  but concrete/asphalt take only ~19 % of recyclates. DIN 1045-2 (2023) usage
  classes: **BK-N** ≤ 25 Vol-% (type-dependent, no extra req.), **BK-E** higher
  (extra exposure/moisture requirements), **BK-S** = beyond → abZ/ZiE.
  Types (EN 12620 + DIN 4226-101): Typ 1 Rcu90 (Rc+Ru ≥ 90 %, Rb ≤ 10, Ra ≤ 1,
  XRg ≤ 1, FL ≤ 2, WA ≤ 10 M-%); Typ 2 Rcu70 (Rb ≤ 30, WA ≤ 15); Typ 3/4 not
  for concrete; fine RGK only from Typ-1; absorbed water pre-saturation/credit
  in w/z accounting; durability deductions (strength, carbonation slower? —
  mixed findings; verify design assumptions).
- **R-Beton reality:** CO2 effect small (cement still the footprint), but key
  for primary raw material saving (up to ~50 Mt/yr theoretically substitutable);
  C&D waste is Germany's largest waste stream (~half of construction-year waste);
  sorted demolition (DIN SPEC 91484 selective deconstruction) is the precondition;
  aged-concrete duration behaviour caution: 52-y wall cores retained only
  ~70–75 % of strength at 70-d sustained load → αcc = 0.85 may be optimistic
  for RC reuse design (flag: research-level).
- **SCM supply trends:** fly ash (coal exit) and GGBS (H2-DRI steel route)
  shrink; REA gypsum (FGD) likewise — expect calcined clays, limestone
  calcined clay (LC3-type, research/abZ in DE), silica fume imports and
  recycled fines to fill the gap; supply risk = specification risk (VERIFY
  regional availability before locking an SCM into a standard detail).
- **Cement decarbonisation labels:** Cement Carbon Commitment classes (CCC A+…D,
  voluntary) and **CSC** (Concrete Sustainability Council plant/certification
  levels) increasingly asked in tenders; new EN 197-5 classes cut clinker to
  35–64 %; clinker factor of German mix ~67 %; check trade-off: lower clinker
  ↔ slower hardening, longer curing, early frost sensitivity, XF credit limits.
- **Steel scrap**: EAF route 100 % scrap (fossil energy only, power-mix bound);
  H2-DRI near-zero-C process route (pilot–early industrial; slag chemistry
  differs); scrap grading/trace elements (Cu, Sn embrittlement) limit open-loop
  cycles; ReUse of sections growing with digital passports (Madaster-type
  registries) and DfD bolted design.
- **Gypsum**: board recycling closed-loop exists (paper separation); REA
  substitute natural stone is the circularity story — coal-exit supply gap is
  a medium-term risk for DE board plants.
- **Carbon fibre textile** §4.19: material-saving but energy-intensive; recycle
  routes immature (pyrolysis) — specify for material-efficiency claims, not
  circularity claims.

---

## 8. Selection workflow — material from the design brief

Decision tree (answer top-down, then verify in the standards tables above):

1. **What does it carry, how far, how much?**
   - point/line loads, spans > ~6 m slender or industrial floors → steel
     (S235–S460) or RC/PSC; timber for ≤ ~12 m residential spans (GL24–32h);
     masonry only for compression-dominant ≤ 4–5 storeys (fmk ≥ 4–8, see
     masonry-construction); no tension elements in unreinforced masonry/UC.
   - storey height / load class → min section → strength class choice.
2. **What exposure (Einwirkung)?**
   - map to X0/XC/XD/XS/XF/XA/XM + moisture class + DIN 18195/WU need →
     concrete limits §4.9 / masonry restriction (KS no visible splash without
     measures; PBC exterior only sheltered; GK class for wood §5.7);
   - ground sulfate/pH table → XA → SR cement/lining;
   - interior humidity: gypsum/lime render OK, cement only where wet.
3. **Fire?**
   - required REI: massive (masonry, RC: cover + section) vs timber (char
     layer over-design) vs steel (needs protection above ~500 °C: boards,
     spray, intumescent) vs gypsum boards (water of crystallisation);
   - reaction-to-fire class (EN 13501-1) for escapes/facades (WDVS height rules
     2.5/7/22 m German pattern — VERIFY current MBO/ADR guidance).
4. **Acoustic mass / thermal storage?**
   - party-wall mass ≥ ~200 kg/m² (Rw table tier) → masonry/RC; lightweight
     → double-leaf + absorber (drywall skill); summer heat → internal
     insulation no good, massive layer or external + phase shift.
5. **Sustainability target (GWP/PEI cap)?**
   - budget by kg CO2-eq: timber negative (A1–A3 branch averages −565…−712
     kg/m³); clay/earth near-neutral unburnt; concrete low-clinker: CCC class,
     SCM credit, RC aggregate (materials, not CO2); steel EAF/H2-DRI grades;
     insulation: bio-based/mw vs fossil foams; verify via EPD/ÖKOBAUDAT.
6. **Budget tier & local supply?**
   - T1 regionally: standard C25/30 XC3 vs bespoke; KS where brick market thin;
     ready-mix radius, formwork reuse logic (construction-detailing).
7. **Approval route available?** CE-hEN product → specify by class; else
   check abZ/ETA list before writing it into the tender (never assume an
   innovative material is generically usable).
8. Output spec card per element: material + class + standard + exposure
   assumptions + cover/lambda/density + QA (Ü-Klasse/BBQ, factory control) +
   sustainability value (EPD module A1–A3) + tier tag (T1–T4).

## 9. Failure patterns and verification checklist

**Typical material-spec failure patterns** (each has killed designs):

| Failure pattern | Root cause | Guard |
|---|---|---|
| Spalled cover, rust stains | cover < carbonation depth; curing skipped | §4.9 cover + §5.1; curing classes §4.7 |
| Sudden rebar loss, no warning | chloride pitting in XD/XS with cracked permeable concrete | w/z 0.45, CEM III, 50 mm cover, no water traps |
| Pop-outs/net cracks, gel exudate | ASR (reactive aggregate + alkali + damp) | (na) cement / aggregate class / dry detail |
| Surface scaling/deep frost cracking | no air entrainment for XF2–4; early frost | LP mandatory, curing until ≥ 5 N/mm² |
| Ettringite expansion in sewers | sulfate + C3A + water | SR cement / XA table / lining |
| Delayed expansion + map cracking | free CaO/MgO (failed soundness) or gypsum-cement mix | Le Chatelier ≤ 10 mm; never mix gypsum + PC/lime |
| AAC/KS wall soft, stained in splash zone | wrong material-exposure pair | use-class discipline §5.7, §4.12 |
| Rotting beam heads / Hausschwamm | GK0 assumption for GK2 reality | constructional detail first, species/durability §5.7 |
| Warp/cracks in timber floors | supply moisture ≫ service, tangential movement ignored | drying target, quarter-sawn, fastening pattern |
| Gypsum screed + damp cover = mush | non-hydraulic binder under moisture barrier | EN 13813 use class, moisture control |
| WDVS delamination in high-rise | system approved but components swapped | ETA system integrity, no mixing producers |
| Glass balustrade shattered on impact | used FG where ESG/TVG + 18008 category required | fck table §4.17, category A–C make-ups |
| Cement 6 months old in silo | storage lapse → strength/setting loss | FIFO, 1–2 month rule §4.2 |
| Alkali-aggregate in road deck, WS class | WS dropped from DIN 1045-2 → forgotten | TL Beton-StB still demands for concrete road decks |
| "CE means allowed" | CE ≠ national fitness | §6 regulatory routes |

**Verification checklist before a material spec leaves the agent:**

- [ ] exposure class assigned (X..., moisture/WU/GK) and combined-strictest logic applied
- [ ] strength/consistency/cover/lambda/cp/mu numbers tagged T1–T4 with standard + edition
- [ ] National Annex route checked (DE/AT/CH project country)
- [ ] product regulatory route stated: CE + DoP / abZ + Ü / ZiE / approved-list
- [ ] cement×exposure applicability matrix respected (incl. SCM credit XF caveats)
- [ ] k-value / w/z / paste volume internally consistent (mix design order §4.10)
- [ ] curing class/duration written into spec where exposure needs it (NK + temps)
- [ ] durability mechanism walked through (§5) with the governing variable checked
- [ ] wood: use class ↔ species/durability ↔ constructional protection consistent
- [ ] fire: reaction-to-fire + REI route named (mass/char/protection)
- [ ] sustainability: EPD values (module A1–A3, biogenic-C convention) not blog numbers
- [ ] recycled/low-clinker alternatives assessed for changed requirements, not just labels
- [ ] tolerances/marking assumptions realistic (DIN 18202/18203 execution, bar-marking, delivery certs)
- [ ] all VERIFY items resolved against current documents or explicitly flagged for the responsible engineer
- [ ] sibling-skill boundaries respected (no element design, no energy balance inside this skill)
