---
name: existing-structures-retrofit
description: >
  Bauen im Bestand (working with existing structures) for DACH practice: condition
  assessment workflow (Dokumentation, Bestandsaufnahme, Voruntersuchung,
  Bauwerksprüfung with DIN 1076 cycles — Hauptprüfung 6 a / einfache Prüfung 3 a /
  Beobachtung, S/D/V Zustandsnote 0–4, RÜV and VDI 6200 CC/RC inspection cadence);
  material testing (reinforcement induction scan, half-cell potential, phenolphthalein
  carbonation, chloride profiles, Rebound ≥9 readings, cores per DIN EN 12504/13791
  with 5%-fractile statistics), historical concrete/rebar strength lookup tables
  (W200/Bn/B/TGL/C classes, Betonstahl I–IV fyk, smooth-bar bond caveats); code path
  (Bestandsschutz grandfathering, Anpassungsverlangen, Nachrechnung DIN 1045-2→EC2
  with reduced γM concrete 1.20–1.50 / steel 1.05–1.10 under qualified-inventory
  conditions, γF permanent −0.25/+1.15); load assumptions for old stock (Mp/m²
  conversions, historical use loads, snow); utilization re-check worked examples
  (1975 slab three-stage, slender column 2nd-order); strengthening with numbers
  (Aufbeton ≥40 mm + joint-shear check with roughness coefficients and dowels,
  Bewehrungsergänzung, Spritzbeton jackets with confinement gains, CFRP bonded/
  slotted λM factors, steel plates, prestress, added bracing walls, foundation
  underpinning DIN 4123); defect catalog (carbonation dk=α√t, chloride pitting,
  static vs active cracks, settlement signatures, frost, ASR, sulphate, rising
  damp); moisture/mould remediation ladder incl. fRsi≥0.7; energy retrofit
  (GEG component U-limits for owners, WDVS + fire constraints, roof/top-floor/
  cellar-ceiling plays, window replacement logic, heat-pump flow-temperature
  strategy 40–50 °C); LCC economics (operation 60–75% of lifecycle GHG, CRREM,
  VDI 2067); assess→target→verify→strengthen→monitor sequence with decision tree,
  failure patterns, verification checklist, and FreeCAD/IFC scan-to-BIM modelling
  of existing fabric. Practice values flagged [VERIFY] where source tables were
  lossy; not a statutory substitute for a Tragwerksplaner/Prüfingenieur.
---

# Existing Structures & Retrofit (Bauen im Bestand) — DACH Practice Skill

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

Agent-neutral procedure skill for assessing, re-checking and strengthening existing
buildings (and for deciding *whether* to), under the German-language regulatory and
normative framework. German terms are kept in parentheses because inventories,
Prüfberichte and submissions circulate in German.

**Scope.** Reinforced concrete / masonry stock of the 20th century is the core
(worked examples follow it); timber and steel defect logic is included at assessment
level. Bridges/civil works appear only through the inspection machinery (DIN 1076)
that building practice borrows. Energy and services retrofit is covered to the
interface where the building-physics, TGA and fire skills take over.

## 0. How to use this skill — and the [VERIFY] convention

Use this skill when the task involves ANY of:
- converting/intensifying use of an existing building (living→office, add-on storey, new
  openings),
- re-checking (Nachrechnung / Nachweis im Bestand) old members against current rules,
- planning strengthening (Aufbeton, jackets, CFRP, added walls, underpinning),
- diagnosing defects (cracks, spalling, corrosion, damp, mould, settlement),
- condition survey programmes and inspection cycles for owned/municipal stock,
- deciding retrofit vs. demolish, with whole-life numbers,
- modelling existing fabric (scan-to-BIM) for any of the above.

**[VERIFY] convention.** This skill is distilled from standards-adjacent references;
some source tables arrived lossy. Any figure or rule marked **[VERIFY]** must be
re-read in the current norm text (DIN EN 1990/1992, DIN 1045-2, DIN 1076, VDI 6200,
GEG in force at project date) before it goes into a calculation report. Unmarked
values are safe to use as planning figures; final design remains the job of a
licensed Tragwerksplaner, and re-checks in Germany are coordinated with the
Prüfingenieur für Standsicherheit / building authority early.

Hard limits of this skill: it never replaces a Voruntersuchung by qualified persons,
never certifies Standsicherheit, and treats pollutant findings as triggers for
specialist measurement (Schadstoffkataster), not as clearance.

## 1. Master sequence: assess → define target → verify → strengthen → monitor

Every Bestand project runs the same five phases; skipping or overlapping them is the
root cause of most retrofit failures.

| Phase | German | Output | Typical trap |
|---|---|---|---|
| 1 Assess | Bestandsaufnahme / Voruntersuchung | documented condition + material data + defects + pollutants | building on drawings alone; no cores; no crack mapping |
| 2 Target | Zieldefinition / Nutzungsänderung | load model, target utilization, residual life, service class | authority/owner expectations not fixed before measuring |
| 3 Verify | Nachrechnung / Bewertung | utilisation per member, code path (Bestandsschutz vs. new rules) | mixing code generations; ignoring old detailing rules |
| 4 Strengthen | Ertüchtigung / Instandsetzung | method choice with force-transfer details, staging checks | composite-interface shear forgotten; load-introduction zones |
| 5 Monitor | Beobachtung / Bauwerksbuch update | gauges, re-inspection cadence, documented as-built change | "repaired and forgotten"; no follow-up cycle |

Stock context that makes this discipline worth it: roughly **10 % of dwellings are
younger than 15 a, about 60 % were built before 1960**, and of refurbishments only
~25 % are driven by repair need while ~75 % are driven by change of use
(Nutzungsänderung). A re-check that cannot prove the existing member under the NEW
use will end in strengthening — plan for it.

Vocabulary (DIN EN 1990 / industry usage, keep them apart in reports):
- **Instandhaltung** — maintenance: preserves the target state (inspect, service).
- **Instandsetzung** — repair: restores the target state after damage (same design
  goals).
- **Ertüchtigung** — upgrade: raises the target state above the original (new loads,
  new code level, strengthening).
- **Nachrechnung** — re-check: proof of an existing structure under CURRENT rules,
  with code-permitted relaxations where the standard allows.
- **Bestandsschutz** — grandfathering: lawfully-erected fabric may remain even if
  today's rules differ (§ 2).
- **Nutzungsdauer / Lebensdauer** — design working life (DIN EN 1990: 50 a for
  buildings, 100 a for monumental/bridge-type structures) vs. actual service life.
- **Mischungsverbot** — do not mix code sets within one verification; exception:
  non-monolithic precast joints transmitting only support forces.

## 2. Code path: Bestandsschutz, change of use, and the Nachrechnung transition

### 2.1 Bestandsschutz (grandfathering) — what survives and what breaks it

Principle: a structure lawfully erected and maintained under the rules of its time
may remain, even though it would not be approved today. Repairs may follow the old
rules. Preconditions, all three:
1. original lawfulness (Baugenehmigung, conformity at erection),
2. **no substantial change** (keine wesentliche Änderung),
3. condition as intended at erection — normal wear only.

Bestandsschutz is **lost** where there is danger to life/health, or where the
intervention reaches the quality of a new building. Loss also never covers damage
that arose from a rule now known to be insufficient (example in the case law
tradition: overhead single-pane glazing ESG→VSG must be upgraded even on repair).

Authority levers (MBO logic, adopted into Landesbauordnungen):
- **Anpassungsverlangen (§85(1)5 MBO)** — authority may demand compliance to
  current requirements where a concrete danger exists; burden of proof on the
  authority. Health-hazardous products (e.g. asbestos in reachable condition) can
  trigger replacement even of untouched parts.
- **Harmonisierungsverlangen** — on a substantial change, directly adjacent
  constructive-related parts may be pulled up to current rules if no unreasonable
  extra cost results (e.g. a new stair may pull the adjacent landing and stair
  enclosure up to current rules).
- **Intervention grading (stages A–C)**: A = renewal of defective parts with same
  use, substance not destroyed → procedure-free; C = interventions so deep that a
  whole-building proof is triggered. Classify the planned work early.

### 2.2 Change-of-use / alteration rules that drive the statics

- **Durchbrüche (new openings)**: local compensation per CURRENT rules (e.g. RC
  frame action); no whole-building current-rule proof triggered by the opening.
- **Umbau storey loads**: load path of NEW or altered elements per current code;
  existing parts may keep the historic verification and merely carry the added
  loads; any strengthening member is designed to the new code.
- **Aufstockung (add-on storey)**: the added loads per current actions standard
  must be carried; unchanged lower parts are proven under the ORIGINAL code
  including the new loads; if lower storeys would need substantial change anyway,
  the whole building is treated as a new build.
- Later "neue Erkenntnisse" (corrected old rules) can reopen the historic proof.
- New products (retrofit adhesives, FRP, grouts) always need current conformity
  route (CE / abZ / ZiE) — grandfathering never covers them.

### 2.3 Nachrechnung: existing-code → EC2/DIN EN 1992 transition

Two-stage material assessment is the standard route: (1) derive nominal strengths
from documents/historic code tables, (2) upgrade by testing where needed.
The transition vocabulary old↔new must be exact in the report:
- **σ-Verfahren (working stress)** until 1972 in West Germany; **Traglastverfahren
  (ultimate load)** introduced in the GDR from 1955 with a global η factor —
  GDR-era calculations are NOT directly comparable to EC2 utilization.
- 1972 DIN 1045: strength classes Bn50–Bn550 as 5 % fractile 28 d cylinder, design
  value = β·Nennwert with global safety η; 1978 units switched N/mm²; 2001/2011
  C-classes (EN 206).
- Concrete and steel partial factors may be **reduced** for the re-check of
  existing RC if a qualified inventory exists (§ 4.7 modified γ table and its
  preconditions). Without qualified inventory, full current factors apply and the
  tabular historic strengths (§ 4.5) govern.

## 3. Documentation and survey programme (Bestandsaufnahme)

### 3.1 Paper/digital records to chase before any drilling

Checklist (as-found documentation set):
1. ownership + land survey (Lageplan), permits (Baugenehmigung incl. old annexes),
2. as-built statics: structural calculations, reinforcement plans/Barroschauen,
   formwork plans, precast connection drawings,
3. TGA as-builts, facade/waterproofing documentation, expert reports, test fields,
4. utility routes and Kampfmittel (UXO) records, maintenance logs / Bauwerksbuch,
5. records of changed actions: groundwater level shifts, adjacent excavations,
6. events: fire, storm, flood, mining subsidence, earthquakes,
7. alteration history (changes of use, added loads: racks, machines, PV, greening),
8. neighbour situation (Beweissicherung — documented adjacent-condition).

Missing records are the normal case for pre-1960 fabric and force the testing route
of § 4. The documentation set closes with a Bauwerksbuch-style conformity summary.

### 3.2 Physical survey methods (selection by question)

| Question | Method | Notes from practice |
|---|---|---|
| rebar position/diameter/cover | induction scanning / cover meter | destructive confirmation on anchorage zones |
| carbonation depth | phenolphthalein on fresh fracture | uncarbonated = red; carbonated stays colourless below pH≈9 |
| chloride content | powder from ground profiles, wet chemistry / potentiometric titration | profile vs. depth, not single surface value |
| corrosion activity | half-cell potential mapping | indications, not quantification |
| concrete strength | Rebound (Schmidt) and/or cores | Rebound supplementary only; cores per § 4.6 |
| crack width | calibrated loupe / gauge | map plan + elevation, mark active-crack monitors |
| crack depth | core or ultrasonic across crack | |
| voids/laminations masonry | tap test; endoscopy | |
| moisture | resistance/capacitive probe, CM method, oven-dry weight | |
| structure/moisture in depth | ultrasonic, seismic, radar, IR-thermography | |
| masonry strength | unit cores + mortar joint strength; wallette (lab) | tap/scratch + rebound as preselection |
| timber | resistograph (bore resistance), glue-area lab tests, moisture, fastener corrosion (destructive), pest expert | |
| steel member | coupons for composition/strength, weldability check, coating thickness (ultrasonic), lead/asbestos in old coatings | |

Site works order: photographic documentation → survey/control points → crack
mapping incl. gauges on the building AND at neighbours → function checks of
equipment → geometric control checks (dimensions, axes, storey heights vs.
drawings) → actual use loads / occupancy audit → maintenance-state audit.

### 3.3 Pollutants (Schadstoffe) — periods to trigger testing

Seen-at-inventory list with manufacturing/use windows (FRG/GDR; if in doubt test):
- **Asbestos**: sprayed asbestos (soft insulation) GDR ≤1969 / FRG ≤1979;
  weakly-bonded uses ≤1984; asbestos cement (Platten, pipes, flue linings) ≤1992;
  ban from 1995 (few exceptions).
- **KMF (artificial mineral fibres)**: old wool installed until 31.5.2000;
  recycled-bottle wool from 1996.
- **PCB**: facade/edge sealants old-Laender 1955–~1975 (peak 1964–72);
  acoustic ceiling paints ≤1971; capacitors/transformers ≤1984.
- **PAK (tar)**: waterproofing/bituminous single-plies ~≤1965; tar-asphalt screeds
  ≤ mid-1960s; parquet adhesives occasionally ≤ late 1970s; wood/timber
  protectants ≤ ~1991; wood-block mastic ≤1995; anti-corrosion coatings on
  water-works concrete ≤2000.
- **PCP**: indoor use effectively banned 1986 (FRG; outdoor until 1989), GDR
  approvals ran to 1978/1986; total ban >0.1 M-% [VERIFY exact limit].
- **Lead**: water pipes ≤1973; lead-white/chromate paints until the 1980s;
  PVC stabilisers only abandoned from 2015; red-lead primer never fully banned.
- **Magnesia/anhydrite screeds**: chloride content can attack RC slabs below —
  check old "magnesiaestrich" floors before strengthening with bonded toppings.

Framework: Schadstoffkataster per VDI/GVSS 6202-1, level **L1** (inventory +
first assessment from drawings/period) → **L2** (technical investigation: sampling
programme, cadastre, risk assessment). Demolition/works spec follows the hazardous-
waste demolition norm (ATV DIN 18459 logic) — asbestos/PCB handling is a separate
trade with notification duties.

## 4. Material assessment of existing concrete structures

### 4.1 Two-stage strength derivation

1. **Stage 1 — documents/historic codes:** read the concrete class from the old
   calculation notes and map to a current characteristic cylinder strength
   (§ 4.3 tables). Rebar: ≥3 samples per table entry, ≥5 per test zone if the type
   is unknown or a higher fyk is wanted; one steel type per zone.
2. **Stage 2 — verification by sampling/lab** if the documented class is doubtful,
   missing, or a higher strength is needed for the re-check. GDR stock has its own
  rebar traditions (St A-0 220, St B-IV 490, Roxor oval bars 490 …) — see § 4.4.

### 4.2 In-situ strength testing (DIN EN 12504 + DIN EN 13791)

- Methods: cores (12504-1), Rebound (12504-2), pull-out (12504-3), UPV (12504-4);
  classification of the result population per **DIN EN 13791** (test zones of one
  "population"), with direct / indirect (Rebound calibrated) / combined calibration.
- Rebound discipline: **≥9 valid readings** per area, spacing ≥25 mm, ≥25 mm from
  edges; supplementary only — never the sole basis for a Nachweis [VERIFY scope].
- Cores: **≥3 per test zone**; diameter ≥100 mm regardless of aggregate size;
  length = diameter (dry-stored 50/100/150 mm cores equate to wet 150 mm cubes —
  DIN EN 13791 NA equivalence, the drying and shape-factor corrections cancel
  approximately); avoid longitudinal rebar (transverse bars reduce strength);
  test dry, defect-free. For new-build sampling the rule ≥1 per casting day per
  100 m³ applies (≥3 per concrete composition); the relaxed 2-core rule is
  new-build only, never for Bestand. Relation f_ck,is,cube ≥ 0.85·f_ck,cube.
- Cube→cylinder, exact DBV/EN 13791 table (f_ck,is cylinder / cube, N/mm²): C8/10
  7.0/9.0; C12/15 10.0/13.0; C16/20 14.0/17.0; C20/25 17.0/21.0; C25/30 21.0/26.0;
  C30/37 26.0/31.0; C35/45 30.0/38.0; C40/50 34.0/43.0; C45/55 38.0/47.0;
  C50/60 43.0/51.0 — use this table, not a flat 0.82 ratio.
- Rebound (Schmidt) **without core calibration** is only admissible per DIN EN
  13791 if carbonation depth ≤ 5 mm (older stock: measure carbonation depth
  first; if > 5 mm the carbonated layer must be locally ground off before
  testing — rarely practicable, so calibrate instead).

Statistical reduction of a small test population (5 % fractile estimation),
two approaches per DIN EN 13791 NA — **pick by sample size and COV**:
- **Approach A** (≥9 cores, or 3–8 cores with COV Vx > 0.20): lognormal/normal
  5 %-fractile, fck,is = fm(n),is·(1 − kn·Vx), Vx = sx/fm(n),is with floor
  **Vx,min = 0.08**. kn by n (linear interpolation between): n=3→3.37; 4→2.63;
  5→2.33; 6→2.18; 7→2.08; 8→2.00; 9→1.96; 10→1.92; 15→1.82; 20→1.76; 30→1.73;
  ∞→1.64.
- **Approach B** (3–8 cores, only if Vx ≤ 0.20): fck,is = min(fm(n),is·k3 ;
  f_is,lowest + 4 N/mm²), with k3 by n: n=3→0.70; n=4–5→0.75; n=6–8→0.80. Simpler
  and less conservative than A but gated on the tighter COV — re-zone or add
  cores if Vx > 0.20 rather than force B.

### 4.3 Historic concrete classes → fck (cylinder, N/mm²) — mapping table excerpt

| Period / code basis | Old class | fck mapped |
|---|---|---|
| 1904–1916 (W300 mean) | W180 / W200 | 8 / 9 |
| 1916–1925 DAfEb W200 | 150 / 180 / 210 | 8 / 9.5 / 11 (extra conditions c) |
| 1925–1932 DIN W200 | 100 / 130 / 180 | 5 / 7 / 10 |
| 1932–1943 DIN W200 | 120 / 160 / 210 | 6.5 / 8.5 / 12 |
| 1943–1972 DIN W200 (GDR TGL≤1980) | B120 / B160 / B225 / B300 | 6.5 / 11 / 15 / 20 |
| " | Bc450 / Bc600 (precast, DIN 4225) | 30 / 40 |
| 1972–1978 DIN W200 5 % | Bn50 / 100 / 150 / 250 / 350 / 450 / 550 | 4 / 8 / 12 / 20 / 27.5 / 35.5 / 43.5 |
| 1978–2001 DIN W200 5 % | B5 / B10 / B15 / B25 / B35 / B45 / B55 | 4 / 8 / 12 / 20 / 27.5 / 35.5 / 43.5 |
| 1980–1990 GDR TGL W150 5 % | Bk10 / 15 / 25 / 35 / 45 | 7.5 / 11.5 / 19 / 26.5 / 34 |
| ab 2001 EN 206 (150 mm 5 %) | C12/15 … C40/50 | 12 … 40 |

Units: ≈ kp/cm² until 1972, N/mm² from 1978. Bn250 ≈ C20/25 is the standard bridge
value used in re-check examples. fck,min structural concrete per class (with/without
core support): C12/15→10/13; C16/20→14/17; C20/25→17/21; C25/30→21/26; C30/37→26/31
[VERIFY vs. current DIN EN 206 table].

### 4.4 Historic reinforcement fyk — mapping table excerpt (with ductility notes)

| Steel (period) | fyk N/mm² | class |
|---|---|---|
| smooth St00.12 (1860–37) / hand iron St37 (1895–43) / rail-head <1930 | 180 / 220 / 130–210 | B |
| high-quality rebar 1930–48 | 260 | — |
| Betonstahl I (1943–72) | 220–245 | B |
| Betonstahl II/III/IV (1948–72) | 315 | B |
| St48 (1925–32) / St52 (1932–43), BSt IIa | 290 / 340 | B |
| BSt220/340 GU · BSt420/500 RU(III) (1972–84) | 220 · 420 | B |
| BSt420S (1984–2009); verwunden (twisted) | 420 | B / A |
| BSt500S(IV); verwunden | 500 | B / A |
| GDR St A-0 220 / A-I 240 / T-III 400 / T-IV 490 / B-IV 490 | as named | B mostly |
| welded mesh GK(IV) (1972–84 onward) | 500 | A |
| old high-strength specialty (bi-Stahl 70/90→650–700; Neptun 800) | — | B |

Notes baked into the tables: pre-1943 products carry a +10 % γM penalty; **smooth
bars do NOT satisfy current bond assumptions** — anchorage/overlap must be checked
against the DBV design-bond table for plain bars (fctd rises from 0.7 at fck=8 to
1.7 at fck=50 N/mm²; ×0.7 for "moderate" bond conditions, ×0.85 for non-quasi-static
loading; favourable end hooks may be credited). Welded-mesh codes (Q/R/N/A/B ranges)
identify the era; strength of the plastic-knot composite mats era is special.

### 4.5 Old-code detailing artefacts to hunt for (they change the Nachweis)

- Steel strain capped at **5‰** in the old σ/traglast world → under EC2 the
  member may be "over-reinforced in strain" though under-reinforced in force:
  **crack-width and ductility verification become the binding check** (§ 6.1).
- **No stirrups** (rammed/poured old slabs, τ0 tables allowed it) → beware
  splitting cracks along span direction; shear then rides on V Rd,c only.
- Little or no top (field) rebar over supports; **cranked bars (Aufbiegungen)**
  with outdated shear-cover logic; corbel/curtain-wall anchors; old rivet
  edge distances where steel parts are reused.
- Old cover ≈25 mm vs. today's 30–40 mm → in 50-a stock the carbonation front
  (§ 8.1) often already reaches the bar level.

### 4.6 Modified partial factors for the re-check (qualified inventory only)

Preconditions (all, DBV-Merkblatt "Modifizierte Teilsicherheitsbeiwerte", 03/2013):
design working life 50 a; ≥5 a of proper existing use proven; qualified survey
proves damage-free condition; predominantly static live loads Qk ≤ 5 kN/m² and
point loads (Gk+Qk) ≤ 7 kN; load ratio **1.0 ≥ Gk/(Gk+Qk) ≥ 0.50**; normal
concrete C12/15–C50/60; section tolerances per DIN EN 13670/DIN 1045-3:2012 met
(else measure and use as-built geometry). Then — and **only with prior agreement
of the Prüfingenieur/authority** —:

- resistance factors γ_M per COV of the measured material (DBV modified-factor
  table):

| COV of concrete | γ_M concrete (persistent/transient) | γ_M steel |
|---|---|---|
| 0.25 | 1.20 | 1.05 |
| 0.30 | 1.25 | 1.10 |
| 0.35 | 1.30 (design stage only w/o member test variant) | 1.10 |
| 0.40 | 1.40–1.50 (bending RC members +20 %; axial/shear of unreinforced bending +40 % centric-compression caveats) | 1.10 |

Extraordinary-situation variant: γ_M concrete 1.10–1.30, steel 1.00. Justification:
shorter residual life + small geometric scatter of ONE known member beat the
population-wide calibration of new-design factors. Floors on the COV itself,
regardless of test result: **V_y,c ≥ 0.15, V_y,s ≥ 0.06**; without member testing
(design/Entwurf stage only) default to V_R,c = 0.30 → γ_C,mod = 1.30 and
V_R,s = 0.10 → γ_S,mod = 1.10. Design values: f_cd,mod = α_cc·f_ck,is/γ_C,mod with
**α_cc = 0.85 for reinforced concrete, 0.70 for plain/unreinforced concrete**;
f_yd,mod = f_yk,is/γ_S,mod.

- A separate, simpler route (**DAfStb Belastungsrichtlinie**, for the preparatory
  capacity assessment, same preconditions) fixes single values instead of the
  COV table: γ_G reduced **1.35 → 1.15** (permanent actions), γ_Q unchanged at
  **1.50** (variable actions), γ_C reduced **1.50 → 1.40**, γ_S reduced
  **1.15 → 1.10**. Never mix this set with the DBV COV-table set in one
  verification, and never adjust γ_G alone without also reviewing the resistance
  side — an isolated single-factor cut can silently lower the overall safety
  level below intent.

### 4.7 Load tests as last resort

DAfStb load-test guideline: computed capacity first, load-controlled testing, only
accredited test institutes (MPA/university) — risk of sudden shear-compression
failure under the jack. Use where strengthening is otherwise disproportionate.

## 5. Actions for existing buildings (load assumptions)

- **Unit archaeology:** 1 Mp/m² = 10 kN/m²; 1 kp/cm² = 0.1 N/mm²; old W-classes
  are cube crush strengths, not fck — convert before touching EC2 tables.
- **Historic use loads:** the DIN 1045:1972 dwelling-slab check ran on q = 7.0
  kN/m² total (§ 6.1); modern categories: A2 residential 1.5 (+1.0 partitions),
  B1 office 2.0 kN/m² — living→office raises q modestly, storage explodes it;
  classify the target use first.
- **GDR-era action factors (ETV Beton 1981, semi-probabilistic):** γ self-weight
  normal concrete 1.10, insulation 1.30, snow 1.40, wind 1.20 — a GDR "Traglast"
  safety margin is NOT an EC2 utilization; re-derive, don't translate coefficients.
- **Snow:** today's snow zones/heights differ from the maps at erection (and the
  modified-γ table explicitly addresses the German lowland snow case as an
  "extraordinary" situation) → for roofs, the Nachrechnung snow action follows the
  CURRENT DIN EN 1991-1-3/NA [VERIFY the Bestand-specific snow relaxation debate —
  some authorities allow the erection-date map for unchanged fabric under
  Bestandsschutz; do not count on it].
- **Added loads typical to Bestand:** PV/ballast on flat roofs, green roofs,
  mezzanines, racks/forklifts, safes/cranes, summer→ice-rink hall conversions
  (temperature/humidity regime change!) — each is a VDI 6200 "damage indicator
  class 1" trigger for re-check.
- Imposed-deformation actions (shrinkage/creep residual, temperature in old
  monolithic frames) rarely documented; measure crack widths before assuming they
  are dormant.

## 6. Verification worked examples (the numbers to imitate)

### 6.1 1975 RC slab, living → office, three-stage re-check

Geometry/stock: one-way slab, effective span 4.34 m (+support width → l_eff≈4.50 m),
h = 180 mm, d = 155 mm, concrete Bn250 (≈C20/25), steel "III 42/50" (BSt420),
provided As = 5.24 cm²/m (Ø10/15).

**Stage 0 — historic proof (DIN 1045:1972):** q = 7.0 kN/m²; m_F = 1.772 Mp·m/m →
a_s,erf = 5.15 ≤ 5.24 OK; shear at 0.5d τ₀ = 1.11 < 3.50 → no stirrups; l/h = 29 ≤
35 for deflection. *The slab was fine under its own code.*

**Stage 1 — EC2 with new use, NO survey:** fyk downgraded by the old→new total-
safety ratio (1.40·1.15)/1.75·420 = 384 MPa → fyd = 334; fck = 20 → fcd = 11.33;
loads g = 6.0 (1.5 new floor + 4.5 old allowance), q = 2.0 (office B1):
r_d = 1.35·6 + 1.5·2 = 11.1 kN/m² → m_Ed = 28.35 kNm/m → μ = 0.1041 → ω = 0.1103 →
a_s,erf = **5.80 > 5.24 cm²/m → fails (−11 %)**. Shear: v_Ed = 22.37 kN/m vs.
v_Rd,c ≈ 58.6 kN/m (k=2.0, ρ_l=0.34 %) OK. Deflections: historical record < l/250 →
waivable.

**Stage 2 — modified γ after qualified survey:** 9 cores Ø100 (h/d≈1) → lognormal
statistics (EN 1990 Annex D): f_cyl = 0.82·f_cube; mean 3.41 (ln), s = 0.174 →
fck,is = e^(3.46−1.96·0.174) = 22.70 N/mm²; V_D = √(0.05²+0.05²+0.176²) = 0.189 →
DBV table gives **γ_c,mod = 1.20, γ_s,mod = 1.10** → fcd = 16.08, fyd = 382;
measured d = 151 mm (as-built) → μ = 0.077 → a_s,erf = **5.11 ≤ 5.24 → OK**.
Strain check: εs = 25‰ exceeds the old 5‰ design cap → SLS governs: quasi-permanent
r = 6.6 kN/m² → m = 16.86 kNm/m → σs ≈ 237 N/mm²; XC1 w_k = 0.4 mm → limiting bar
Ø* = 24 mm, Øs = 24·fct,eff/fct,0 = 18 > 10 provided → **cracking OK**.

Moral: survey + modified factors turned an −11 % flexural failure into a pass
without strengthening; the old code's missing ductility is re-covered by the
crack-width proof, not by more steel.

### 6.2 Slender existing column — 2nd-order re-check (1985 stock)

30/30 cm, As = 8.04 cm² (4Ø20, fyk 450→fyd 435), l = 5.2 m, l₀ = 0.76·l = 3.95 m.
Cores n=6: mean 43.41 cube, s = 5.07, V = 0.117 → EN 13791 approach B:
fck,is = min(0.8·43.41 = 34.73; 37.52+4) = 34.73 cube → fck = 33.5 cylinder →
**C30/37**. Slenderness: λ = 45.6 > max(25; 16/√ν_Ed) → slender, 2nd order.
Accidental ecc e_i = αh·l₀²/2000-type ≈ 0.87 cm (αh from length; use code formula);
creep second-order e₂ = K_r·(fcd·…)·h ≈ 0.46 cm (K_r verified afterwards via
(N_Ed−N_Rd)/(N_Ed−N_bal) = (2.058−1.844)/(2.058−0.683) = 0.156 ≈ assumed 0.16 ✓).
e_tot = 1.33 cm → ω = 0.205 → column interaction chart (BT 2c, d₁/h 0.15, e_d/h
0.044 line) → **N_Rd = 1844 kN ≥ N_Ed → utilization ν_Ed = 1.08** [the example's
own load level; treat >1.0 as the strengthening trigger]. Procedure to copy:
strength from cores → class → slenderness gate → eccentricities → chart/numerical
interaction → K_r self-consistency check.

### 6.3 Re-check report skeleton (what a Tragwerksplaner expects)

1. object + construction type + GK/CC classification (VDI 6200); documents found
   vs. assumed (mark every assumption),
2. survey programme + results (zones, statistics, fck,is, fyk proven); code path
   declared (§ 2.1–2.3, no mixing),
3. member utilization table (ULS + SLS, as-built geometry) + detailing audit vs.
   old-code artefacts (§ 4.5),
4. deficits + option list (§ 7) incl. staging checks for execution states,
5. monitoring plan (§ 1 phase 5) and Bauwerksbuch entry.

## 7. Strengthening methods (Ertüchtigung) — options with numbers

Method families: added section (cast-in-place **Aufbeton**/jacket or **Spritzbeton**
shotcrete, with or without reinforcement, bonded or slot-bonded), prestressing,
change of structural system, injection; materials: concrete/shotcrete + rebar,
steel lamellae/sections, **CFRP/GFRP/AFRP** laminates & sheets. Composite action
behaves like a built-up section: bond laws govern, **the joint/interface ends are
the critical zone (delamination)**, and *unloading the existing member boosts the
efficiency of every method* (remove partitions/passive load, or jack actively).

### 7.1 Concrete topping (Aufbeton) + added reinforcement — flexure of slabs

Rules:
- thickness **≥ 40 mm** (shotcrete toppings thinner only by approval [VERIFY]);
  interfacial reinforcement anchored on BOTH sides of the joint;
- bending checks on the MONOLITHIC section use the **LOWER** of the two concrete
  strengths for the compression-zone contributions [VERIFY exact DAfStb rule];
- all intermediate construction stages checked (wet concrete weight before bond
  exists!);
- surface prep: shot-blasted + bonding bridge; joint shear verified below;
- added bars: small-dense (e.g. Ø6/20 B500B = 1.41 cm²/m) placed near the bottom
  of the topping.

**Joint shear.** DIN EN 1992-1-1's interface-shear model is validated for
new-build only ("abgesicherter Bereich"); for strengthening of existing members
use the **fib Model Code 2010** approach instead (Wendehorst/DAfStb practice).
Unreinforced interface (rigid bond):

τ_Rdi = [c_a·f_ctd + μ·σ_n] ≤ 0.5·ν·f_cd

Reinforced interface (perpendicular bond reinforcement, ρ = A_s/A_i):

τ_Rdi = c_r·f_ck^(1/3) + μ·(σ_n + ρ·κ1·f_yd) + ρ·κ2·(f_yd·f_cd)^0.5 ≤ β_c·ν·f_cd

with ν = 0.55·(30/f_ck)^(1/3) ≤ 0.55 (compression-strut strength reduction), and
roughness classes (R_t = Kaufmann sand-patch depth):

| Joint surface | R_t | c_a (adhesion) | c_r (interlock) | κ1 | κ2 | β_c | μ (f_ck≥20) | μ (f_ck≥30) |
|---|---|---|---|---|---|---|---|---|
| sehr rau (very rough) | ≥3.0 mm | 0.50 | 0.2 | 0.5 | 0.9 | 0.5 | 0.8 | 1.0 |
| rau (rough) | ≥1.5 mm | 0.40 | 0.1 | 0.5 | 0.9 | 0.5 | 0.7 | 0.7 |
| glatt (smooth) | — | 0.20 | 0.0 | 0.5 | 1.1 | 0.4 | 0.6 | 0.6 |
| sehr glatt (very smooth) | — | 0.025 | 0.0 | 0.0 | 1.5 | 0.3 | 0.5 | 0.5 |

μ jumps with concrete class (rougher/higher-strength joints get more friction
credit at f_ck≥30) — don't reuse the f_ck≥20 column once the topping is C30/37+.
Surface prep and cleanliness governs which row applies; sand-patch method is
imprecise (an optical roughness method is recommended in practice) — when in
doubt, classify one row down.

**Worked topping example (2-span 6.25 m, existing h=18 cm, Ø12/11 = 10.28 cm²/m,
new 5 cm topping):** loads g_k = 7.25, q_k = 1.5 (A2) → r_d = 12.05 kN/m²;
support moment M_B = −0.125·12.05·6.25² = −58.8 kNm/m → existing section alone
needs 11.51 > 10.28 → **add 1.41 cm²/m** in the topping → resultant d = 15.1 cm
→ μ = 0.205 → required total 10.91 ≤ 11.69 cm²/m OK. Shear: A-field d = 19.5,
ρ_l ≈ 0.13 % → v_Rd,c = 54.2 > v_Ed 25.2; B-support on OLD depth d = 14.5,
ρ_l = 0.71 % → v_Rd,c = 70.2 > 43.9 → no shear links. **Joint check (smooth class,
c_a = 0.20, μ = 0.6):** τ_rd = 0.2·f_ctd ≈ 0.17 ≥ ν_Ed = 0.165 at the high-shear
support → plain joint just OK (bare margin — a shot-blasted "rau" joint buys the
safety). Rule of thumb: verify the joint where the moment is NOT maximum.

### 7.2 Column jackets — cast-in-place or shotcrete (Spritzbeton)

Function: adds area **and** confinement; shotcrete jackets per tunnel-lining rules
(DIN 18551 §9.5 / DIN EN 14487 product logic):
- **no lasting force transfer at jacket ends** — load introduction is by bearing
  plates/wedges or a designed taper; added longitudinal bars only counted where
  force closure exists (head & base details);
- checks: base/head load-transfer zone, mid-height composite section, confinement
  contribution;
- detailing (DIN 18551 §9.5 / DAfStb Heft 467): closed hoops per EC2NA fig.
  NA.8.5g/h or welded links, longitudinal bars concentrated at hoop corners;
  intermediate anchors (Zwischenverankerungen) required once **h/b > 1.5**;
  load-introduction zone hoop spacing **≤ 80 mm**, zone length
  l_c = **30·d_s** (DIN 18551) or **2·d_k** (DAfStb Heft 467, use the larger);
  shotcrete shell contributes to **mid-height** capacity only, at a
  **0.80** efficiency factor (shrinkage/bond loss) — never assumed to transfer
  force at the jacket ends (no lasting force closure there without bearing
  plates/wedges).

**Confinement gain (effective confined area + capacity add):**

A_c,eff = λ_q·λ_l·A_k, A_k = b_k·d_k

λ_q = 1 − [2(b_k−d_s)² + 2(d_k−d_s)²] / (5.5·A_k) — corner-loss factor (d_s =
corner longitudinal-bar diameter)

λ_l = (1 − s_bü/2b_k)·(1 − s_bü/2d_k) — hoop-spacing loss factor (s_bü = hoop
pitch)

ΔN_Rd = 2.3·k_β·ρ_q·f_yd,bü·A_c,eff, with k_β = 1 + (f_ck−20)/100 ≥ 1 and
ρ_q = A_q/A_k = 2(b_k+d_k)·(A_bü/s_bü)/(b_k·d_k)

Old and new hoop confinement areas are computed **separately** (A_eff,alt +
A_eff,neu) and their ΔN_Rd contributions summed. Head/base capacity (bearing
transfer only, no shell credit):
N_Rd = A_c,alt·f_cd,alt + A_s,alt·f_yd,alt + ΔN_Rd,1 + ΔN_Rd,2

Mid-height capacity (shell credited at 0.80):
N_Rd = A_c,alt·f_cd,alt + A_s,alt·f_yd,alt + 0.80·A_b,neu·f_cd,neu + A_s,neu·f_yd,neu

Eccentricity reduces the confinement add (DIN 1045:1972-derived, retained in
practice): ΔN'_Rd = ΔN_Rd·(1 − 8M/(N·d_k)).

**Worked jacket example (30/30 B35→assessed C30/37, IV steel fyk 500, l₀ = 2.8 m,
N_Ed 1800 → 2300 kN):** existing column N_Rd ≈ 1871 kN (ecc. ω = 0.383 chart) →
deficit ~430 kN. Jacket 7.5 cm C30/37 + 4Ø16: mid-height added capacity with 0.8
shotcrete factor ≈ **1880 kN** (plain area+steel). Confinement: existing hoops
(s = 20 cm) add only 54 kN (λ_q 0.389, A_eff 0.00762 m²), jacket hoops (s = 7.5 cm)
add **478 kN** (λ_q 0.331, A_eff 0.0412 m², ρ_w = 0.0107); eccentricity-reduction
term (DIN 1045-1972 confined-member rule, retained in practice) 0.86.
**Load-introduction zone governs:** N_Rd,tot = 1871 + 0.86·(54+478) = **2328 >
2300 OK (util 0.99)**; mid-height = 1871 + 0.86·1880 = 3488 OK. Detailing: cover
XC1 c_min 10 + Δ_dev 10 → c_nom 20 ≤ 25 provided; jacket stirrups Ø≥6, spacing
≤ min(12Ø_s, h, 30) = 19.2 → 17.5 mid; transfer zone l_c = max(30Ø_s = 48; 2·d_j
= 78? shown 12@75=90≥78) → 12 stirrups @75.
Lesson: the head/base transfer capacity, not the middle, sets the jacket length
and congestion — detail it first.

### 7.3 FRP strengthening (CFRP laminates/sheets)

- Products: pultruded laminates (CarboDur S/M class; 160/2400-type naming) bonded
  with epoxy (MC-DUR 1280, Sikadur-type, StoPox SK41) or **slot-in
  (Schlitzverfahren)**; system approvals (Z-36.12-xx) carry expiry dates — always
  use the current abP/ETA, never a lapsed one.
- γ_M (DAfStb-Richtlinie bonded-reinforcement guideline, persistent/transient →
  extraordinary): CFRP laminate γ_LL **1.20 → 1.05**, CFRP sheets/gelege γ_LG
  **1.35 → 1.10**; bond adhesive γ_BA **1.50 (bonded) → 1.20**, γ_BE **1.30
  (slotted) → 1.05**; steel-on-steel or CFRP-on-CFRP bond γ_BG **1.30 → 1.05**.
- Laminate material properties for FEM/BIM (elastic, ≥-values per abZ, N/mm²
  unless noted): **CarboDur S** — ultimate strain ε_Luk ≥1.6 %, E_Lk ≥161,900,
  E_Lm ≥170,000, f_Lk ≥2800; **CarboDur M** — ε_Luk ≥1.3 %, E_Lk ≥200,000,
  E_Lm ≥210,000, f_Lk ≥2500; **MC-DUR/Carboplus 160/2400** — ε_Luk ≥1.6 %,
  E_Lk ≥160,000, E_Lm ≥162,000, f_Lk ≥2800; **MC-DUR/Carboplus 160/2800** —
  ε_Luk ≥1.8 %, E_Lk ≥164,000, E_Lm ≥168,000, f_Lk ≥3200; **MC-DUR/Carboplus
  200/3000** — ε_Luk ≥1.5 %, E_Lk ≥190,000, E_Lm ≥200,000, f_Lk ≥3200; **S&P
  150/2000** — ε_Luk ≥1.5 %, E_Lk ≥160,000, E_Lm ≥168,000, f_Lk ≥2350; **S&P
  200/2000** — ε_Luk ≥1.3 %, E_Lk ≥200,000, E_Lm ≥210,000, f_Lk ≥2500. E_Lk is
  the characteristic (design-side) modulus, E_Lm the mean — use E_Lm for FEM
  stiffness/deflection, E_Lk for ULS strength checks. Laminate thickness
  typically 1.0–3.0 mm, width 10–150 mm (slot-bonded strips narrower,
  10–30 mm) — geometry per the current abZ/ETA, not the type table alone.
  All approvals (Z-36.12-xx) carry an expiry date — confirm current before
  use, never model a lapsed system.
- Section analysis: plane sections, no concrete tension, perfect bond up to
  debonding; checks per member: **peeling (interfacial crack) / anchorage bond
  line AND tensile rupture line**, plus V Rd,c,max and durability of the adhesive
  (temperature!); redistribution allowed only in un-strengthened zones.
- Fire/impact/creep of adhesives are the weak link vs. steel plates; slotted CFRP
  survives edge delamination better.
- Steel lamellae follow the same composite logic with steel γ_M0-type factors;
  unbonded post-tensioned strips are a prestress variant (§ 7.5).

### 7.4 Steel sections / plates to existing members

Bolted/welded steel additions to concrete ride on post-installed anchors with
cracked-concrete approval (rebar scan FIRST to avoid hitting old bars) or epoxy
grout beds in bearing. Typical: side/bottom plates on beams, lacing on columns,
inserted bracing (system change § 7.6). Design per current steel code as new;
the interface is a new connection either way (anchor tables: concrete-detailing
skill).

### 7.5 Prestressing (Externale Vorspannung)

External tendons (threadbars over deflection blocks) or jacked strips: the ACTIVE
method — it *reduces* existing stresses and crack widths instead of only adding
capacity, and controls deflection. Losses, deviation-block bearing and anchorage
bursting are checked on the OLD concrete strength; fire protection and anchor
inspection per approval [VERIFY current guideline numbers — method level here].

### 7.6 Adding walls / changing the structural system (Nachträgliche Aussteifung)

For unbraced or RC1-type frames (single-storey column-stabilised halls, propped
cantilevers without continuity): introduce shear discs or a core.
- Masonry infill/added RC or timber-sheathed walls act as discs — keep the "longest
  bracing walls perpendicular to the largest facade" rule; ≥3 non-parallel non-
  concurrent rigid points per diaphragm;
- floors as diaphragms need edge chords + collectors: old screed joints and
  openings (stair voids!) break the chord — steel strap chords are the standard
  Bestand fix;
- Ringanker/Ringbalken (hoop beam/cordon) added at roof & floor level turn
  non-ductile masonry stock into a box (classic seismic retrofit, see the seismic
  skill for ductility detailing);
- moment-frame trade: adding fixity creates base moments ∝ storey height and
  drift ∝ H³ — fixed old columns only work up to ~2–3 storeys [rule of thumb];
- CLT/steel bracing inserted inside avoids facade change (heritage logic).

### 7.7 Foundation underpinning (Unterfangung, DIN 4123)

- Unterfangung = transferring existing footings to a deeper/broadened bearing
  level; Ausschachtung = excavation whose soil wedge initially still aids stability.
- **Sectional pits: max ~2 m wide** [OCR-lost exact figure], work high-load zones
  (cross-wall intersections, corners) FIRST, force-fit (Kraftschluss) the new
  footing via steel double wedges or hydraulic jacking, build the new footing
  immediately — the old footing must never hang unsupported across a pit.
- Execution sequence discipline replaces interim stability proofs: with the rules
  kept, no per-stage stability check is demanded; the FINAL state gets the full
  EN 1997-1 set (overturning, sliding, bearing, slope, deep slip, material).
- Settlement during underpinning: hairline cracks and displacements **≤ 5 mm** are
  deemed largely unavoidable — set the Beweissicherung trigger levels around that.
- Adjacent-structure protection follows excavation logic (prestressed struts,
  diaphragm/pile walls for sensitive neighbours) — geotechnics skill.

### 7.8 Method-selection cheat sheet

| Deficit | First-choice options | Watch |
|---|---|---|
| slab bending −5…−15 % | Aufbeton + bars (§ 7.1) | joint shear, stage loads, build-up height/doors |
| slab bending, height-constrained | CFRP soffit (§ 7.3) | peeling, fire, edge distance of slots |
| column N-deficit small | CFRP wrap (confinement only) or jacket | end transfer (§ 7.2) |
| column N-deficit large | shotcrete jacket w/ own hoops | head/base detail, 0.99 margin ≠ reserve |
| beam shear deficit | CFRP U-jackets/side bonded; steel flange straps | anchorage against peel |
| hall unbraced | added bracing/wall (§ 7.6) | diaphragm chords, transfer at foundations; bearing deficit → widen/underpin (§ 7.7) with 5 mm settlement honesty |
| deflection/serviceability | prestress strips (§ 7.5) | old-concrete bearing at deviators |

## 8. Defect catalog — mechanism, signature, first action

### 8.1 Carbonation-induced corrosion (the default 50-a RC disease)

- Mechanism: CO₂ + moisture carbonates cement stone → pH < 9 → passive film dies →
  uniform (Flächenkorrosion) rust; rust volume ≫ steel → splitting pressure →
  cracks parallel to bars → cover loss → "puff-pastry" section loss. Needs
  RH ≈ 45–95 % window; dry or saturated concrete barely carbonates; freely
  weathered = fastest.
- Progression: **d_k = α·√t**; example 5 mm at 10 a → α = 1.58 mm/√a → ≈ 11.2 mm
  at 50 a; compare with as-built cover (old 25 mm!) — d_k ≥ c means plan corrosion.
- Signatures: rust staining at bars (Rostfahnen), map/hairline cracks along rebar,
  hollow sound on tap, spalls at edges/splines; phenolphthalein stays colourless.
- Actions: remeasure depth, half-cell for activity, corrosion-inhibiting repair
  (realk Aktivierung) or cover restoration; structural check of residual section.

### 8.2 Chloride attack (XD/S classes, de-iced decks, coastal)

- Pitting (Lochfraß): localised deep attack, **little surface warning, sudden bar
  failure** — worse than carbonation for residual capacity. Chlorides ride water-
  filled pores; Volhard/titration profile vs. depth; old concrete often lacks the
  w/z ≤ 0.45–0.55 density of modern XD3 concrete.
- Actions: profile sampling, potential mapping, remove chloride-loaded cover +
  re-alkalise, or isolate surface (drainage!); structural: assume pitting loss
  ratios [VERIFY DBV Heft Instandsetzung assumption set].

### 8.3 Frost + de-icing salt (XF)

- Scaling needs saturation + fine pores; air voids (1–5.5 Vol.-% by Dmax class)
  are the defence old lean mixes lack; damage concentrates at splash zones, deck
  edges, parapet feet. Drainage first, then SR/PO repair mortar.

### 8.4 Cracks: classification that decides the repair

| Type | Typical cause | Pattern | Repair logic |
|---|---|---|---|
| unschädlich/statisch ruhig (dormant) | shrinkage ~0.6 mm/m final, temperature early | fine, even spacing, mid-depth of restrained zones, stable vs. gauge | seal for durability only |
| aktiv (moving) | live restraint, cyclic thermal, ongoing settlement | width changes with season/load, gauge drift | move the joint (open it properly) or relieve the restraint, then seal |
| load-carrying (statisch wirksam) | shear/flexure/punching overload | diagonal in shear span; vertical flexure at max M (soffit); punching cones/punctuations at column heads of flat slabs | STRUCTURAL re-check before sealing |
| splitting along bars | corrosion, old no-stirrup rammed concrete (Stopfbeton) | longitudinal cracks over bars, rust in the crack line | § 8.1 + shear re-check |
| settlement | differential bearing, adjacent excavation | diagonal cracks at stressed corners of openings, vertical at soft-storey/abrupt stiffness change, bulged masonry wythes | underpin or relieve; ≤5 mm honesty (§ 7.7) |

Crack-width gauges (Rissmonitore) over one full seasonal cycle distinguish
aktiv vs. ruhig empirically; self-healing (Rehydratation crystallisation) can close
hairline cracks < ~0.1–0.2 mm in wet phases [VERIFY size bound].

### 8.5 Alkali-silica reaction & chemical attack (XA)

ASR (AKR): reactive silica (flint, opal sandstone, greywacke) + alkalis + moisture
→ swelling gel → map cracking, gel exudation, deck-edge spalls; diagnose via core
microscopy + aggregate alkali class; measure = cut the moisture; diffuse stiffness
loss → re-check with reduced modulus [VERIFY factor]. Sulphate: expansive route
(sulphate → ettringite — old high-C3A CEM I in sewage/slurry exposure is a known
failure class) vs. dissolving route (acids/fats leach paste → soft chalky surface,
white blooms); check surface pH and reduced section.

### 8.6 Timber defects (assessment-level)

Rot fungi need MC > ~18–20 % (true house dry rot *Serpula* active from 20 % with a
moisture reservoir; brown/white rot, blue stain cosmetic); insects (Nagekäfer common
furniture beetle, Hausbock, Splintholzkäfer) attack even dry wood; shrinkage/warp
loosens old joints; beam heads (Balkenköpfe) in damp masonry are the classic rot
pocket; load-duration: old timber strength assumes short-term — 50-a sustained
strength ≈ 60 % of short-term. Resistograph for hidden decay; DIN 68800 hazard
classes GK0–GK4 [timber-specifics in the timber skill].

### 8.7 Steel defects (assessment-level)

Coating damage → section loss (ultrasonic thickness at worst spots); **fatigue**
under cyclic crane/traffic loads: look at weld ends, old rivet groups, missing or
loose bolts (locking must be chemical/mechanical, not friction only), flange wear
debris = overload evidence; deformation/out-of-plumb = impact history. Lead and
asbestos paints: sample before blasting (§ 3.3).

### 8.8 Envelope deterioration signatures (from the damage-indicator checklist)

- Pitched roofs: slipped tiles (wind), leaky chimney/window junctions, gutters
  frozen/ponding; flat roofs: **ponding**, wet/blistered insulation, added ballast
  (PV/greening) overload, missing/undersized emergency overflow, deflection
  ponding feedback loop;
- facades: spalled corners of two-leaf outer wythe (corner restraint against wire
  anchors), bulging, open/eroded joints (driven-rain class III exposure),
  efflorescence, **stalactites inside = persistent water path (white-tub failure)**;
- floors: leaking pipe pockets, wet screed, magnesia screed + chloride combo (§ 3.3);
- decks/parking: rutting, failed joints, signage-load confusion; bearings seized;
  expansion joints bridged (spalled lips) = active restraint present (§ 8.4).

## 9. Moisture and mould remediation (Feuchtesanierung)

Goal restated: not dryness, but **no persistent moisture** — allow occasional wet
plus guaranteed drying. Diagnostic ladder: locate source first (rain vs. ground vs.
condensation vs. leak vs. construction moisture Baufeuchte), then choose the
measure; moisture maps (capacitive grid + CM/oven-dry profiles) before any
remedial contract.

Measure ladder (escalate only as far as proven necessary):
1. **user-side:** ventilation concept (see § 10.5), dehumidify, remove vapour
   sources; fRsi ≥ 0.7 mould criterion at θ_i 20 °C/θ_e −5 °C/φ_crit 80 % [and
   fRsi,min up to ~0.94 for pool-type climates — per DIN 4108-3 logic];
2. **surface:** rain-tightness repair (joints, render, drip edges), clear
   ponding/gutters, raise ground levels away from plinth, repair drainage;
3. **plinth/ground:** continue the waterproof/insulation package 30–50 cm above
   finished ground; Querschnittsabdichtung (cross-section seal) in masonry bed
   joint cuts off capillary rise — injection barrier = specialist discipline
   [VERIFY product Z-requirements]; dense hydrophobic plinth render transition;
4. **basement classes:** Bodenfeuchte (simple coat) → stauendes Sickerwasser
   (full tanking) → drückendes Wasser (protected tanking; black-tub sheet wrap or
   WU white-tub concrete logic: crack control + waterstops at construction joints;
   never coat on top of soft insulation under point load);
5. **drainage package:** filter fleece → drainage mat → pipe at footing to
   soakaway/separator (control shafts, fall rules per drainage design);
6. **drying after damage:** dehumidification only where an outward-drying path
   exists; wet insulation (λ water 0.6 vs. air 0.025 ≈ 24×) is REPLACED, not dried
   in place.

Mould: surface treatment + remove the humidity cause; indoor-air measurement
campaigns per pollutant protocols; HVAC condensation (summer ice-rink-type regimes
§ 5) needs ventilation, not chemistry.

## 10. Energy retrofit of the envelope (energetische Ertüchtigung)

Demand context: unsanitised old stock runs 200–270 kWh/(m²a) heat demand (1980
levels), average today ≈ 130, target 15–50 for new-standard fabric; a staged
retrofit can cut demand by up to ~85 %. Law stack: WSchV/HeizAnlV → EnEV →
**GEG 2020 (amended 2024)** → the services framework already names a **GModG from 2026** —
check the in-force text at project date [VERIFY].

### 10.1 Owner obligations

GEG-style **component limits (Bauteilegrenzwerte)** bite on owners when elements
are *replaced or first insulated* (and historically on large buildings after
central-plant replacement): the retrofit U-maxima below are the numbers to design
to. Plus: 65 % renewable share for new heating installations (municipal heat
planning WPG 2024 rolling out; a 2026 relaxation debate is flagged —
[VERIFY at project date]); airtightness certificate when no blower-door history;
old low-efficiency boilers/insulation retirement duties exist in the EnEV/GEG
lineage [VERIFY current transition clauses]. Non-compliance is a fine risk AND a
subsidy blocker (BEG requires deeper-than-code fabric).

### 10.2 U-limit table for existing elements (19 °C rooms / 12–<19 °C halls)

| Element | U max W/(m²K) |
|---|---|
| external wall (replace or first insulation) | 0.24 / 0.35 |
| cladding/re-render with insulation | 0.24 / 0.35 (exempt if built to rules after 31.12.1983) |
| windows to outside | 1.3 |
| roof/top-floor ceiling | 0.24 |
| roof (membrane-covered flat) | 0.20 |
| roof windows | 1.4 |
| glazing-only replacement | 1.1 (box windows: IR-coating ε ≤ 0.2; limited cavity → Ug ≤ 1.3 [VERIFY]) |
| walls vs. ground/unheated | 0.30 |
| floor build-up (warm side) | 0.50 |
| ceiling vs. outside (replace) | 0.24 / 0.35 |
| curtain wall / special glazing | 1.5 / 1.9 (special: R′w ≥ 40 dB, bullet, fire ≥18 mm: 2.0; glazing-only 1.6) |

**Thin-layer rule (Dünnschichtregel):** if the max practical build-up thickness is
reached and λ ≤ 0.035 (blown/renewable 0.045) — the limit is waived. Modified
residential single/dual buildings (small, ≤350 m², or short use): Qp ≤ 1.40·Ref
(max +40 %) with H'T caps ~0.40–0.65 W/(m²K) by type [VERIFY table numbers].
Reference new-build comparison for planning: wall 0.28, roof 0.20, window 1.3
(g 0.60); primary-energy factors oil/gas 1.1, wood 0.2, grid power 1.8 (heading
to 1.5 with the decarbonising mix — flips WP-vs-gas rankings [VERIFY]).

### 10.3 Element playbook (retrofit sequence: fabric → bridges → windows → summer → ventilation → plant)

- **Single-leaf masonry:** exterior **WDVS** (ETICS render-on-insulation — no
  anchor penetrations through the insulation plane) or rear-ventilated rainscreen
  = easiest, moves the whole shell into the warm zone; interior insulation only
  with a hygrothermal proof (Glaser/dew-point inside the wall; GEG gives interior
  solutions a looser U target [VERIFY clause]) and with careful handling of timber
  beam heads (rot pocket § 8.6) and corner thermal bridges.
- **WDVS + fire constraints:** external wall finish classes follow the building
  class — GKL4 non-loadbearing external walls A1/A2 or F30-B with surface layers
  (incl. insulation) ≥ B1; GKL5 surfaces B1; reaction classes A2-s1,d0… per
  EN 13501-1; tall/Sonderbau projects may demand A2 non-combustible lamellas or
  fire-break strips (lamellen-streifen) — coordinate with the fire skill; never
  bury combustible insulation without the surface-class chain intact.
- **Two-leaf walls with cavity:** blow-in (check debris + outer-leaf condition
  first); already-filled cavity → external system or interior-proof route.
- **Plinth/basement:** perimeter insulation impossible post-hoc on precast tanked
  walls; interior rigid boards (foam glass/XPS) on the cold side, impact-faced;
  treat cellar stairs and doors as envelope (frequently missed losses).
- **Pitched roofs:** between-rafter (needs rafters ≥18 cm, add under-rafter layer)
  or over-rafter (best, only with re-roofing); historic decorated interiors →
  blown fibre from above + vapour-open underlay review.
- **Flat roofs:** 1930–60 warm-roof build-ups hold only 3–5 cm cork/EPS — today's
  target ≈ 20 cm WLG 035 → verify dead load + snow + new falls (parapet raising
  drives cost); inverted roof (XPS above tanking) protects the membrane but the
  insulation must be closed-cell (wd class).
- **Top-floor ceiling over unused attic (the cheapest tonne of CO₂):** loose-fill
  or laid boards ≥ 24–32 cm on the deck, walkway boards on top; pre-1960 timber
  joist floors U ≈ 0.8 or uninsulated 1.2–2 [VERIFY] → blow-in with moisture
  buffer respect (vapour-open from above?); 1960s concrete top slab U ≈ 1.3 →
  +12 cm meets limits; damp-proof course under loose fill.
- **Cellar ceiling (over unheated):** massive U ≈ 1.6 + 6 cm WLG035 from below is
  compliant; Prussian-cap (Preußische Kappe) vaults → suspended ceiling + blown
  fibre; ground slab U ≈ 2.0 only insulates from above when the floor build-up is
  renewed anyway (+ damp-proof membrane).
- **Windows:** replacement is *one* measure, not the retrofit; Uw 1.3 (Ug ≈ 1.1 +
  Uf ≤ 1.4 typical triple/good warm-edge double); reveals airtight-taped
  (three-joint rule — construction-detailing skill); new tightness → § 10.5;
  glazing-only swap (Ug ≤ 1.1) preserves heritage frames.
- **Thermal bridges:** balcony heads via connector elements (stainless/plastic),
  wrap protruding slabs; ψ-simplified details per the thermal-moisture skill;
  the better U gets, the colder every bridge tip → mould risk moves to bridges,
  not the wall (fRsi check on the worst detail, § 9.1).
- **Summer comfort is a retrofit side-effect:** insulation + airtightness kill
  night-cooling habits; dynamic overheat check (~1200 K·h residential [VERIFY]) →
  external shading (F_c ≤ 0.5, roller shutters best on old stock), internal mass,
  purge ventilation — plan WITH the envelope, not after.

### 10.4 Heat-pump retrofit flow-temperature strategy (services interface)

Sequence: heat load **per room** (not per building) → hydraulic concept (+buffer
where radiators dominate or tariff lock-outs apply) → emitter check → valves/
heat-interface → **hydraulic balance (Abgleich)** → lower the flow target.
- Radiator enlargement vs. legacy 90/70 °C: to 70/55 ×1.5 area, 60/50 ×2,
  55/45 ×2.5; **40–50 °C flow is the practical retrofit target** with enlarged
  radiators; below ~40 °C pure convection collapses (fan-assisted or serial-flow
  units, or raise radiant share — UFH ≤100 W/m², design 35/25); >50 °C is fine
  for any HP but costs SPF.
- **One-pipe (Einrohr) systems:** replace fixed bypasses with load-dependent
  adjustable ones, keep the ring ΔT constant in part load — or convert to
  two-pipe/Tichelmann per storey.
- DHW retrofit options: HP pre-heat + electric top-up (cheap, cycles summer);
  HP + second boiler (space/emissions, keeps HP low-T); HT-HP direct (poor SPF);
  rooming-station fresh-water "small system" (hygiene-clean, trace-heated short
  legs); decentral instantaneous electric on long dead legs (3.5–27 kW).
  Legionella rules (§ W551 logic: 60 °C storage/3-l rule) constrain how low the
  DHW side may run [VERIFY].
- Bivalence: air-source monovalent to ≈ −16 °C is new-build only; bivalent-
  alternative changeover ~50 % of max load → HP covers ~60 % of annual heat;
  bivalent-parallel with boiler at 50–70 % size is the old-radiator compromise.
  SPF anchors: air 2.7–3.2, ground 3.6–4.2, groundwater 3.8–4.6.
- Direct electric only where fabric ≥30 % better than reference (45 % if
  replacing a hydronic system) or on grandfathered exceptions — the old
  night-storage floor circuits can often stay as load buffer with PV.
- Noise/source siting (air units, TA Lärm to property line, borehole permits/
  VDI 4640 extraction values) per the services skill.

### 10.5 Ventilation after airtightness upgrade

Sealed windows + insulated envelope kill the old leak-based exchange → DIN
1946-6 moisture-protection level becomes mandatory. Retrofit standard:
**decentralised heat-recovery wall units** (~120 m³/h class) — mould prevention
independent of user behaviour; central Zu/Abluft = costly duct routes, reserve
for vacated refurbishments; CO₂ demand control where occupancy fluctuates; air
heating only below ~10 W/m² (fully modernised).

### 10.6 PV on existing roofs

Structural gate first: ballast vs. penetration-free framing, snow-clearance strip,
roof remaining-life vs. ~25-a PV life (re-roof BEFORE mounting), flat-roof ballast
loads vs. § 8.8 overload history. Tenant-electricity/building-supply models and
state PV mandates (roof duties by Land, parking-lot PV) [VERIFY per site];
balcony-PV as low-threshold entry step.

## 11. Economics, whole-life and the keep-vs-replace decision

- **Operation dominates:** offices ≈ **75 %** of lifecycle GHG arises in the use
  phase (space heat/cool + electricity), residential ≈ **60 %** — grey energy of
  a retrofit is repaid by operation savings that new-build demolition can never
  recover on short cycles. ~**80–90 % of the buildings needed in 2045 already
  exist**; building operation ≈ 35 % of final energy / ≈ 30 % of CO₂; the retrofit
  rate must double from ~1 %/a to ≥ 2 %/a [dated stock statistics — re-read].
- Cost logic: up to **80–85 % of whole-life cost arises AFTER construction**;
  operating costs historically equal the purchase cost after ~7 years [dated];
  life-cycle accounting per VDI 2067 annuities (capital- + demand- + operation-
  bound; lifetimes: gas condensing ≈ 20 a, HP 15–20, pumps 12, UFH 30, radiators
  ~25 [VERIFY lossy table]). BEG subsidy demands better-than-code fabric; CO₂ price
  path 25 → 30 → 55 €/t (2025) then trading band — fossil operation is a rising
  annuity, model it.
- **CRREM-style pathways:** plot do-nothing vs. stepped retrofit emissions; the
  crossing = stranding date (a 2006 hotel case stranded 2026 do-nothing, 2036 with
  two retrofit steps) — use it for sell/hold/refurbish decisions and DD.
- Material-side bonuses of keeping: brick ≈150-a service life, ~94 % of demolition
  material recyclable; 1 m³ wood stores ≈0.5–1 t CO₂ (timber add-on storeys spare
  foundations and dodge demolition emissions); bio-based retrofits (hemp-lime spray
  28–30 cm reaching U = 0.24 on a listed half-timbered wall; blown wood fibre on
  top floors) trade thickness for hygroscopic safety on old walls — a *moisture*
  argument, not only an energy one.
- Tenancy-law frame (residential): **Modernisierung** (energy upgrade) can be
  passed into rent per law; **Sanierung** (defect repair) cannot — sequence and
  document measures so the distinction survives audit. DIN 31051 terms
  (Inspektion/Wartung/Instandsetzung/Verbesserung) vs. DIN 32736 Modernisierung
  in facility plans.

## 12. Decision tree (condensed)

```
Existing member / building in question
├─ Lawful at erection & unchanged use? ── yes → Bestandsschutz: maintain to old rules;
│     but Verkehrssicherungspflicht: inspection cycle § 3 stays, danger findings override
├─ Change planned? (use ↑ / opening / add-on / new element)
│     └─ yes → new parts per CURRENT code; affected path re-checked (Nachrechnung)
│           ├─ qualified inventory feasible (cores+scans+records)? 
│           │     ├─ yes → modified γ (§ 4.6, authority agreement!) → utilisation
│           │     └─ no  → tabular historic strengths + full γ → utilisation
│           ├─ util ≤ 1.0 & detailing OK & SLS (cracks/defl) OK → keep, monitor
│           ├─ util 1.0–1.15 bending → Aufbeton/CFRP (§ 7.1/7.3)
│           ├─ util column N↑ → jacket with OWN confinement hoops (§ 7.2)
│           ├─ shear/punching deficit → bonded jackets/stirrup upgrade, re-check joint (§ 7)
│           ├─ stability/bracing deficit → system change (§ 7.6) + foundation checks
│           └─ bearing deficit → widen/underpin (§ 7.7) with Beweissicherung
├─ Defects (corrosion/chloride/settlement/ASR)? dormant & repairable →
│     Instandsetzung to old target state; active/structural → stop-use, expert
└─ Energy/regulation drive → § 10 ladder (fabric → windows → ventilation → plant)
      with summer-comfort + moisture proofs per touched element
```

## 13. Recurring failure patterns in Bestand projects (what actually goes wrong)

1. Statics on assumptions: no cores, no rebar scan → "as-drawing" d and cover lost
   to leveling screeds → utilization errors > 15 %.
2. Mixed code sets in one report (Mischungsverbot violation).
3. Strengthening designed at mid-span, failing at the ends (jacket load transfer,
   CFRP peel, topping joint shear — always check the ends first).
4. New stiffness attracts new forces: an added core/bracing bay redistributes
   everything; unreinforced old slabs as diaphragms crack at voids/openings.
5. Stage loads forgotten (wet topping, slurry, jacking) and unloading ignored →
   the strengthening only starts carrying after damage (pre-stress or prop it).
6. Durability not re-established: repaired but still carbonated chloride-rich zone;
   drainage left broken; vapour traps created by interior insulation without proof.
7. Pollutants discovered during demolition (asbestos under the carpet, PCB in the
   edge sealant) → stoppage + cost; § 3.3 testing is cheap.
8. Fire downgrade by stealth: exposed steel jacket/CFRP in a former F90 zone;
   WDVS surface class chain broken (A2-s1,d0 vs. B1 rules per GKL).
9. Moisture regime shifted by energy retrofit (tight envelope, no ventilation
    concept) → mould claims within one heating season.
10. Settlement honesty missing: no pre-work neighbour documentation, then the 5 mm
    "unavoidable" becomes a liability dispute.
11. Over-strengthening: util-0.99 jackets everywhere erode robustness budgets and
    cost; a monitor-first sequence often defers a third of the measures.
12. Missing Bauwerksbuch update after works → next owner repeats the whole survey.

## 14. Verification checklist

Assessment phase:
- [ ] records set § 3.1 chased + missing-items log signed
- [ ] inspection category & cycle chosen (DIN 1076 / RÜV / VDI 6200 CC-RC)
- [ ] survey plan: zones, ≥3 rebar samples (≥5 per unknown zone), cores ≥3/zone,
      carbonation+chloride profiles where XC/XD suspected; pollutant screening per
      § 3.3 periods with L2 follow-up where hit
- [ ] Beweissicherung (neighbour + own crack gauges) before any ground works
- [ ] as-built geometry captured (scan/survey), storey heights & slab thicknesses
Code path:
- [ ] Bestandsschutz classification A–C agreed in writing with owner/authority
- [ ] no mixed code sets; historic unit conversions documented
- [ ] modified-γ preconditions § 4.6 met AND agreed with Prüfingenieur
Verification:
- [ ] actions: target use categories, snow-zone audit, storage/rack/PV/greening loads
- [ ] member table: ULS + SLS (crack width where old 5‰ cap applies), as-built d
- [ ] detailing audit § 4.5 done (smooth-bar anchorage, stirrup absence, cranks)
- [ ] slender members: 2nd-order + K_r self-consistency (worked pattern § 6.2)
Strengthening:
- [ ] method chosen vs. deficit table § 7.8; ends/interfaces verified (joint shear,
      load-introduction zones, peel/anchorage lines)
- [ ] all execution stages checked (including temporary supports)
- [ ] durability of new system: cover on new surface, adhesive temp class, drainage
- [ ] fire rating impact of every added/exposed element re-assessed
Monitor:
- [ ] gauges read-in schedule + re-inspection date in Bauwerksbuch; as-built of
      strengthening handed over with materials' DoP/abP copies

## 15. FreeCAD / IFC workflow for existing fabric

- **Scan-to-BIM intake:** point cloud → reference in the model (IFC spatial zone
  "Bestand" [VERIFY entity mapping in current exporter]); model measured as-built
  geometry, never nominal drawings; scan tolerances (±20–30 mm on old walls) feed
  the § 4.6 tolerance precondition check.
- **Separate storey/phase for existing:** model Bestand and Ertüchtigung in
  distinct IFC stories/phases (`Existing-Slab-L2`, `Retrofit-Topping-L2`) with
  property sets carrying condition data: member key, fck,is source, util ratio,
  defect codes (S/D/V + Zustandsnote 0–4), last/next inspection — this keeps the
  Mischungsverbot visible in the model itself.
- Strengthening design: model composite sections (existing + topping/jacket) as
  separate solids on one reference axis; drive the § 6.1 μ/ω checks from a linked
  spreadsheet so every survey correction re-runs cheaply; coordinate service
  penetrations against rebar-scan zones before coring.
- Cross-reference: IFC exchange requirements, naming, MVD choice and curation
  cadence live in the **bim-management** skill; reinforcement-scan data hand-off
  format in **concrete-detailing**; structural-section setup in
  **structural-analysis**; U-value/blower-door models in
  **building-physics-thermal-moisture**.

## 16. Related skills

- Structure: `structural-analysis` (altered systems, 2nd order), `concrete-detailing`
  (post-installed anchors § 7.4), `masonry-construction` (Ringanker, repointing),
  `timber-steel-design` (member strengthening), `seismic-design` (ductility upgrade
  shares the § 7.6 logic).
- Ground & envelope: `geotechnics-foundations` (§ 7.7), `roofing-waterproofing`
  (§ 10.3 roofs), `building-physics-thermal-moisture` (Glaser/interior-insulation
  proofs § 9 and § 10.3).
- Services & compliance: `building-services-tga` (§ 10.4–10.5),
  `fire-protection-building` (§ 10.3 fire constraints), `cost-management-din276`
  (§ 11 LCC), `bim-management` (§ 15 phase/condition data).

---

*Norms referenced (edition check at use): DIN EN 1990/1991/1992 (+NA), DIN 1045
series incl. 1045-2/1045-3, historic DIN 1045 (1972/1978/1988) and GDR TGL/ETV
sets, DIN EN 12504 / 13791 / 206 / 13670, DIN 1076 + RI-EBW-PRÜF, RÜV, ARGEBAU
Bestand notes, VDI 6200, VDI/GVSS 6202-1, DIN 4123, DIN EN 1997-1, DAfStb
guidelines (bonded reinforcement, load tests, jackets), GEG/GModG, DIN 4108
series, DIN EN 12831, VDI 2067, VDI 4640, DIN V 18599, DIN 1946-6, DIN 4109.
All values are planning aids; [VERIFY]-tagged items and final designs must be
confirmed against the texts in force by an authorised professional.*
