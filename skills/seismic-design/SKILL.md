---
name: seismic-design
description: >
  Earthquake-resistant design of buildings in the Eurocode 8 mindset for the DACH
  region (Germany: DIN EN 1998-1 + Nationaler Annexe/NA, DIN EN 1998-5; low-to-moderate
  seismicity): hazard framing without inventing map values (ag from the NA zoning map,
  ground classes A-E, importance factor gamma_I), behaviour factor q and ductility
  classes DCM/DCH, base-shear logic V_B = Se(T1)/q * lambda * W with VERIFY flags on
  every exact coefficient, plan/elevation regularity audit (eccentricity e/r thresholds,
  storey-stiffness ratios, mass, diaphragm, re-entrant corners, soft-storey and torsional
  rules stated as EC8 logic), load path and floor/roof diaphragm design (chord and
  drag-collector forces C = w*L^2/(8b) style statics, ring-anchor/Ringanker trigger list,
  stiffness-proportional load sharing V_i = I_i/SigmaI * F, system shear-centre and core
  placement rules), bracing-system selection (shear walls vs frames vs dual; longest
  discs perpendicular to largest facade), confined-masonry detailing for digested
  European/German practice (tie columns/Randglieder, ring beams/Ringbalken, masonry-first
  construction sequence, opening rules), ductile RC detailing concepts (strong
  column-weak beam, confinement, capacity-design shear — all VERIFY vs EN 1998-1/NA),
  connection and continuity discipline (Formschluss/Kraftschluss/Stoffschluss matrix,
  shortest force path, mechanical anchors in cracked concrete at concept level with
  VERIFY to EN 1992-4), non-structural design (parapets, boundary walls, WDVS/ETICS
  cladding, drift-sensitive partitions), site effects (ground classes, topography,
  liquefaction screening), foundation continuity, retrofit triage for unreinforced-
  masonry stock per DIN EN 1998-3 logic, a worked shear-wall example (stiffness
  distribution + in-plane shear check), a plan-quality regularity audit an agent can run
  on any plan including FreeCAD geometry queries via neka-nat/freecad-mcp, and a
  red-flag list. Prominent caveat: in Germany seismic design is required per
  DIN EN 1998-1/NA with its own zoning (Germany low-to-moderate; the NA's acceleration
  values must be looked up — never invented); for a design agent this skill is primarily
  a plan-configuration and detail-regularity checklist discipline, not a substitute for
  the Tragwerksplaner.
---

# Earthquake-Resistant Design — Eurocode 8 Mindset (DACH Focus)

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

> **Regulatory note (read first, applies to every section).** In Germany, seismic design is
> required by **DIN EN 1998-1 (Eurocode 8 Teil 1) with its Nationaler Annexe (NA)**, plus
> DIN EN 1998-5 for foundations and geotechnical aspects; Austria and Switzerland have their
> own EC8-compliant codes with their own national annexes. Germany sits in the **low-to-moderate
> seismicity** range: most of the country needs far less strength reduction (q) and far more
> *configurational and detailing discipline* than high-seismic regions. The **seismic zone
> (Erdbebenzone) and the reference ground acceleration `ag` for a specific plot must be looked up
> in the current DIN EN 1998-1/NA hazard map — never quoted from memory, never invented, never
> "assumed as zone 2".** Where this skill shows an `ag` value, it is explicitly labelled
> *illustrative placeholder*.
>
> **For a design agent, this skill is a plan-configuration and detail-regularity checklist
> discipline.** Low forces do not excuse bad configuration: soft storeys, torsion, missing
> tie systems and out-of-plane failures kill in moderate earthquakes too. The agent's real
> job is to make the building **regular, continuous, well-tied and checkable before a
> licensed engineer (Tragwerksplaner) ever calculates it** — and then to say honestly which
> exact EC8 coefficients still have to be verified against DIN EN 1998-1 + NA.

**Every rule in this document exists because unreinforced or badly configured masonry and
untied frames collapse in earthquakes — in Central Europe included (the 1976 Friuli event and
the 2012/2013 Emilia sequences damaged ordinary low-rise buildings hard; most historical German
stock is unconfined masonry).** The failure modes are universal and preventable: heavy roofs on
weak walls, open ground storeys, short columns, asymmetric plans, missing ring beams, unbonded
corners, 90° hooks where 135° belong. This skill turns those failure modes into numeric,
checkable rules that can be applied at concept-plan stage, argued with a client, encoded in a
FreeCAD model, and handed to a licensed engineer as a coherent design basis.

Nothing here is a structural design. See the reality check below.

## Reality Check — Licensing, Liability & the Limits of This Skill

**This skill produces design aids and calculation guidance for planning and FreeCAD modelling ONLY.**

- Everything here — regularity thresholds, q logic, tie-element schedules, diaphragm rules,
  detailing geometry — is a **preliminary design aid and a checking tool**, not a structural
  design.
- Any design for an actual occupied building must be **calculated, reviewed and signed by a
  licensed statically responsible engineer (Tragwerksplaner; where required a Prüfingenieur,
  and in the approval process a Nachweisberechtigter für Tragwerksplanung per the applicable
  Landesbauordnung)**, and must pass the local building authority (Baugenehmigungsverfahren).
  Seismic design is part of that statical proof, not an alternative to it.
- Never present FreeCAD output, wall-density numbers, base-shear values or rebar schedules
  derived from this skill as construction-ready. The only correct framing is: *"preliminary
  seismic basis for coordination — to be verified and signed by the Tragwerksplaner."*
- **Say this unprompted** when a user starts treating output as final ("give me the bar-bending
  schedule for the mason", "skip the engineer, it's only a house", "delete that wall, the model
  still stands", sharing the model with a contractor). Stop and state the licensing requirement
  in plain language before continuing.
- **Never certify.** No stamp, no signature block, no "stability certificate", no soil report.
- **Soil is never assumed.** Every ground class (A–E), every amplification factor S, every
  foundation number is conditional on a site-specific geotechnical investigation
  (geotechnischer Untersuchungsbericht per DIN EN 1997-2 / DIN EN 1998-5). A default is a
  modelling placeholder, never a design input.
- **Hazard is never guessed.** Zone and `ag` come from the NA map for the plot. Between zones
  or near mapped active structures (Oberrheingraben/Rheingraben, Niederrheinisches Becken,
  Schwäbische Alb, Vogtland, Alpenvorland fault zones — indicative list, **verify against the
  NA map and its fault provisions**), take the more onerous treatment and say so in writing.
- Exact numeric EC8 coefficients are marked **VERIFY — read DIN EN 1998-1 + NA** throughout.
  Do not launder a VERIFY-flagged number into a confident claim.
- Nothing is "earthquake-proof". The honest phrase: *"entworfen zur Reduktion des
  Einsturzrisikos beim Bemessungsbeben, vorbehaltlich ingenieurtechnischer Prüfung"* —
  designed to reduce collapse risk in the design-level earthquake, subject to engineer review.

---

## How To Use This Skill (order of operations)

```
1. Establish the hazard basis     ->  §1   (zone/ag from NA map = LOOKUP, ground class, S,
                                            gamma_I, importance class)
2. Pick system, q, ductility class->  §2   (confined masonry / RC walls / RC frame / dual;
                                            DCM vs DCH decision)
3. Fix the CONFIGURATION          ->  §3   (regularity audit — BEFORE any calculation)
4. Design the load path           ->  §4   (diaphragms, chords, collectors, Ringanker)
5. Place the bracing system       ->  §5   (shear walls vs frames vs dual; placement rules)
6. Detail the system              ->  §6   confined masonry / §7 RC frames & walls
7. Make the connections work      ->  §8   (continuity, anchors, Schlussarten)
8. Kill the cheap killers         ->  §9   non-structural (parapets, WDVS, partitions)
9. Ground and foundations         ->  §10–§11
10. Retrofit existing stock       ->  §12
11. Quality-control mindset       ->  §13
12. Encode & audit the model      ->  §14  (FreeCAD queries, plan-quality checklist)
13. Worked example as pattern     ->  §15
14. Red flags & client talk       ->  §16
15. Hand off honestly             ->  §17  (to the Tragwerksplaner, flags listed)
```

**Configuration beats calculation.** A regular, symmetric, well-tied house designed to
`q ≤ 1.5` with sound detailing outperforms an irregular one with a sophisticated analysis. In
low-to-moderate seismicity this is doubly true: the forces are small enough that
*geometry mistakes, not force magnitudes, are what fail buildings*. Spend the effort at step 3.

Companion skills: structural-systems (system choice, gravity sizing), concrete-detailing and
masonry-construction (execution), structural-analysis (models, combinations),
building-materials, freecad-bim (model hierarchy, property sets), fire-protection.

---

## Section 1: Hazard Basis Under Eurocode 8

### 1.1 The parameters that define the action

| Parameter | German term | Meaning | Source of truth |
|---|---|---|---|
| `ag` | Bezugserdbeschleunigung | reference horizontal ground acceleration (475-yr return period, ~10% in 50 yr) | **DIN EN 1998-1/NA zoning map — LOOK UP PER PLOT. Never quote from this skill.** |
| `γI` | Bedeutungsbeiwert / importance factor | multiplies `ag` per importance class (ordinary housing lowest; hospitals/emergency use higher) | EC8-1 §2 + NA — VERIFY class mapping |
| `S`, ground class A–E | Baugrundklassen | soil amplification of the spectrum | §1.4; EN 1998-5 classification by `vs,30` |
| `T1` | Grundschwingungsdauer | fundamental period — a configuration property, not a material property | §1.5 |
| `q` | Verhaltensbeiwert | behaviour factor — the central concept of EC8 | §2; EC8-1 system tables + NA caps — VERIFY |
| `λ` | higher-mode correction | ≈ 0.85 correction for multi-storey, multi-mass systems (period-range dependent) | legacy German practice used λ = 0.85 for > 2 storeys; EC8 form in §1.6 — VERIFY |

**Importance classes (Bedeutungsklassen), concept:** ordinary residential → lowest relevant
class, γI ≈ 1.0. Buildings whose failure raises off-site risk (hazardous materials) or which
must stay operational (fire stations, hospitals, emergency shelters, schools used as shelters)
→ higher γI (order 1.2–1.5 depending on class — **VERIFY the exact mapping in DIN EN
1998-1/NA; older German practice (DIN 4149:2005, withdrawn) used four categories with
γI = 0.8 / 1.0 / 1.2 / 1.4**). A private house is essentially always the ordinary class.
Raising the class raises every other requirement (analysis, detailing, documentation) — do it
only for a genuine post-earthquake function.

### 1.2 Design objectives and return periods

EC8 is a **life-safety code with damage limitation**:

- **No-collapse objective (ULS / GZT Erdbeben):** the structure keeps vertical load capacity
  with significant damage in the design earthquake (475-yr; γI scales it).
- **Damage-limitation objective (SLS / GZG):** in the frequent earthquake (475/γI yr) the
  structure and non-structural elements remain usable; drift limited (order 0.5% for brittle
  non-structure, 1% for ductile — **VERIFY drift limits and the γI division rule in the NA**).
- The reduced return period is handled **entirely through γI on ag, never through q**.

Practical consequence for houses in Germany: the no-collapse case is usually not
force-governing — the **damage-limitation case (drift, stiff layout, no soft storeys) and the
detailing rules do the work.** That is why §3 and §6 are the heart of this skill.

### 1.3 The response spectrum, conceptually (elastic spectrum Se(T))

- `Se(T) = ag · S · η · [plateau; descending branches]` with corner periods `TB, TC, TD`
  depending on ground class; `η = 1` for standard 5% damping; `η ≤ 1` only with proven added
  damping (never assumed for masonry or ordinary structures).
- **Houses and low-rise masonry/RC sit on the acceleration plateau (T < TC)** — short-period,
  mass-controlled. The demand is **proportional to mass**: heavy roofs, heavy cladding, full
  water tanks, planted terraces multiply straight into the force. Every other demand nuance is
  second order in Germany.
- **Vertical component (`agV`, own TB/TC):** contributes where significant permanent load
  combines with live load; for ordinary one/two-storey housing its effect is small, but
  **include it in ULS combinations for heavily loaded spans and long cantilevers** —
  **VERIFY when vertical action must be combined per EN 1998-1/NA.**
- **Torsional spectrum `Se,T(T)`** applies to torsionally sensitive structures — see §3.1.
- Exact plateau ordinates and branch periods per ground class: legacy German tables
  (DIN 4149:2005: β0 ≈ 1.0–2.5 by ground combination, TC ≈ 0.2–0.5 s, vertical ag ×0.7)
  corroborate the structure of the spectrum, but **the current DIN EN 1998-1/NA spectrum
  governs — VERIFY everything.**

### 1.4 Ground classes (Baugrundklassen) — site effects

| Class | Description | `vs,30` (m/s) | Typical German occurrence |
|---|---|---|---|
| A | Rock | > 800 | outcrops (Rheingraben flanks, Mittelgebirge) |
| B | Very stiff soil | 360–800 (legacy tables: 350–800) | dense glacial till, gravel terraces |
| C | Stiff / deep soil | 180–360 (legacy: 150–350) | **most urban plots default here until proven otherwise** |
| D | Soft soil | < 180 | soft clays/peats, moorland, some Rhine-valley sediments |
| E | Soft-over-stiff profile | (top ~5 m soft, then stiffer) | basin sediments, hydraulic fills |

- Each class carries an amplification factor `S` (order 1.0–1.8, largest on soft ground —
  **VERIFY per NA**). The *relative* logic is what matters for planning: **soft ground
  amplifies and lengthens the response** — on class D/E, §9 and §11 stop being optional
  niceties.
- **Do not mix ground-class vocabularies.** DIN 4149 (withdrawn) used Baugrundklassen A/B/C
  with Untergrundklassen R/T/S; EC8 uses A–E by `vs,30`. Use EC8 only; if a legacy building
  file cites DIN 4149 zones or ground combinations, re-derive per the current NA.
- **Topographic amplification:** steep crest/ridge/slope positions amplify (factor order
  1.1–1.4 depending on geometry per EN 1998-5 §4.2 — **VERIFY thresholds and when it may be
  ignored**). A hillside site is not automatically a higher zone, but it *is* automatically a
  higher-risk site: see §11 (stepped foundations, split levels) and §10 (landslide).
- **Site response analysis** (1-D equivalent linear) is required for unusual soil profiles
  and important buildings on soft ground — **VERIFY the class boundaries in EN 1998-5.**
  For a two-storey house: never. For 5+ storeys on class D/E: expect the engineer to ask.

### 1.5 Fundamental period T1 — configuration shows up in the numbers

Real dynamic analysis governs, but planning needs an estimate:

- Masonry / shear-wall systems: **order 0.05 s per storey** (short, wall-stiff).
- RC moment frames without walls: **order 0.1 s per storey**; T rises with height.
- Braced / dual systems: in between. **VERIFY the empirical expressions in EN 1998-1 §4.3.3.**
- Rule of thumb that survives any coefficient revision: **adding walls shortens T; removing
  them lengthens it; a soft storey both lengthens the period AND concentrates drift there.**

### 1.6 Seismic base shear — the static-equivalent logic (EC8 §4.3.3 skeleton)

For a regular low-rise building with one dominant mode (fine for houses):

```
W    = seismic weight (§1.7)
V_B  = Se(T1)/q · λ · W            (EC8 equivalent lateral force logic)
Se(T1) = ag · γI · S · β0          on the plateau for short-period structures
λ    ≈ 0.85  higher-mode correction when T1 > 0.1 s / more than ~2 storeys — VERIFY
F_x  = V_B · wx·hx / Σ(wi·hi)      (triangular mass×height distribution; for masonry-type
       systems with short T1 a uniform storey distribution is permitted — VERIFY threshold)
e_ds = ± 0.05·a                    accidental eccentricity per direction (a = plan dimension)
```

**VERIFY every constant** (β0, λ, the uniform-distribution threshold, the 5% accidental
eccentricity, the q eligibility caps) **against DIN EN 1998-1 + NA — the block above is the
logic skeleton, not a quotation.** Analysis-method eligibility (linear static vs modal vs
dynamic) depends on regularity, height and ductility class per §3.4 — run the regularity audit
before choosing the method.

**Mental constant for the agent:** *in a German low-to-moderate zone with q ≤ 1.5, the design
horizontal force is a few percent of the building weight — comparable to or below a severe wind
action on the large façade. The earthquake does not punish a well-configured house. It punishes
the configurational mistakes (soft storey, torsion, unbonded corners, missing ties) that are
invisible under wind and gravity.* This is precisely why the weight of this skill sits on
configuration and detailing, not on force arithmetic.

### 1.7 Seismic weight W (seismische Masse)

Include: all permanent actions (self weight, finishes, permanent partitions, façades), the
combination fractions of variable actions per EN 1990 (ψ2,i·Qk,i; storage occupancies at a much
higher fraction — **VERIFY the ψ2,i table and NA additions**), **full** water-tank weight, snow
where the NA requires a fraction, fixed equipment. Exclude ordinary residential live load.

- Build W **per storey and per direction** — it feeds the mass-regularity checks (§3) and the
  damage-limitation check.
- In FreeCAD: model the tank, the cladding, the screed with real mass at real location. The
  forgotten 20–30 kN on the roof is the classic error (§9.1).

---

## Section 2: Behaviour Factor q, Ductility Classes, System Choice

### 2.1 The q concept (Verhaltensbeiwert) — the central EC8 idea

`q` divides the **elastic** spectral force down to the **design** force. The reduction is not a
gift; it is a **promise**: the structure will behave ductilely, yield in planned zones (plastic
hinges / distributed masonry cracking), dissipate energy, and survive large inelastic
deformations without losing vertical capacity.

- **q ≈ 1.5 (DCM — mäßig duktil):** essentially-elastic demand with modest ductility.
  Detailing is moderate; the promise is cheap to keep.
- **q = 2–6+ (DCH — hoch duktil):** large force reduction bought with full capacity-design
  detailing (confinement hoops, strong-column-weak-beam, joint checks…). **If the detailing is
  not built, the reduction is fiction and the building is designed for a fraction of what it
  will actually see.** This sentence is the most important in the skill.
- Masonry systems (§6) get **low q** and lean on geometry (confinement) rather than rebar
  precision — which makes them *forgiving of average workmanship*, their great virtue.
- National annexes for low/moderate seismicity (Germany included) frequently **cap q**
  (often ≈ 1.5–2 for ordinary systems) or restrict DCH use — **VERIFY the q caps in the NA
  before designing anything with q > 1.5.** If the NA caps q low, the design conversation
  becomes: a little more strength, ordinary detailing, and 100% configuration discipline.
- Rough cross-code intuition: q plays the role older codes called R; `q ≈ R/1.5`. Never mix
  one code's factor into another code's formula — that is the most common arithmetic error in
  house-scale seismic calculations and it can halve or double the design force.

### 2.2 Ductility classes and their consequences

| | **DCM** (q ≤ 1.5) | **DCH** (q > 1.5) |
|---|---|---|
| Analysis | linear static for eligible structures | modal/dynamic as required; capacity design |
| Detailing | code minimums + constructive ties (§6–§8) | full plastic-hinge detailing (§7) |
| Typical use in low/moderate zones | **ordinary housing — the default** | higher zones, taller/important buildings, where the NA permits |
| Penalty if detailing shortcuts | modest (forces were near-elastic anyway) | severe (design forces fictitiously low) |
| Agent's job | enforce configuration + tie continuity | enforce configuration + deliver a detailing scope the engineer can check |

### 2.3 Structural systems, ranked for the house scale in low-to-moderate hazard

| System | Bracing character | Ductility source | Notes |
|---|---|---|---|
| **Cross-wall / box masonry with ring anchors** (Wandschaliges Mauerwerk mit Ringankern) | shear discs | ring system + bond | German standard for 1–3 storeys; works if walls are continuous and the ring closes |
| **Confined masonry** (Mauerwerk mit bewehrten Beton-Randgliedern) | discs + frame action around panels | confinement geometry (§6) | the best low-tech seismic system known; far more forgiving than an informal RC frame |
| **RC shear walls** (Stahlbeton-Aussteifungsscheiben) | cantilever discs | flexural base hinge | most efficient bracing; must be continuous to foundation |
| **RC moment frames** (Rahmendruckglied-Systeme) | frame action | plastic hinges | only when genuinely designed AND supervised; see §7 |
| **Dual systems** (frame + walls) | walls + frame | both | walls carry the bulk; frame sized for a defined share or as stability backup — VERIFY NA participation rules |
| **Braced frames (steel/timber)** | triangulation | members + plates | braces must act both directions — a single tension-only diagonal is not allowed, the force reverses; CLT buildings: shear panels + chord ties |
| **Precast panel systems** | discs + joints | joint ductility | pinned site joints need explicit hold-down + diaphragm ties; special rules apply — VERIFY EN 1998-1 §4.3/§9 logic + NA |
| **Unreinforced masonry without confinement** (unbewehrtes Mauerwerk) | discs | (brittle) | not a defensible choice for new construction where the NA demands any ductility; retrofit context only (§12) |

### 2.4 The "grey structure" warning, European edition

The default continental "Rohbau" habit — RC columns cast first, masonry packed into the bays
afterwards, with no explicit decision about whether the infill contributes — is **not an RC
frame in any code sense**, and it is worse than either parent system: the infill adds unintended
stiffness (torsion; soft storeys at levels where it happens to be omitted), traps columns as
short columns, and nobody capacity-designed any of it. EC8 requires an explicit choice; three
legitimate strategies exist and exactly one must be drawn on the plan:

1. **Isolated non-structural infill** — full-height and head gaps (25–50 mm) with compressible
   filler and sealant; panel restrained out-of-plane but transferring no in-plane force; bare
   frame designed alone. **Detail the gap on the drawing or it will be filled with mortar.**
2. **Participating (structural) infill** — modelled (equivalent strut or panel), frame + infill
   designed together, frame forces capacity-designed against the strut, short-column effect
   explicitly addressed.
3. **Confined masonry** — abandon the frame idea and build per §6: masonry first, confining
   elements cast against it.

The illegal fourth option, universal on unsupervised sites: bare-frame design + tight-packed
brick + hope.

---

## Section 3: Regularity in Plan and Elevation (Regelmäßigkeit)

**Run this audit before any calculation and before any detailing.** Detailing cannot rescue a
bad configuration; it can only make a good one work. The thresholds below are the EC8-1 §4.2.3
criteria expressed as logic; **VERIFY every exact factor against DIN EN 1998-1 + NA**
(regularity tables and the analysis-eligibility rules).

### 3.1 Plan regularity criteria (Grundriss)

| # | Criterion | Regular when (logic) | Irregular when | Severe / notes |
|---|---|---|---|---|
| 1 | **Torsional sensitivity** | `e_max = max|e_ds,i| / r ≤ 0.25` (e_ds = design eccentricity incl. ±5% accidental; r = radius of gyration of the storey mass) | `e_max > 0.25` | the 0.2–0.25 band still demands care; above → torsional analysis + diaphragm-force amplification |
| 2 | **Storey stiffness** | `K_T ≥ 0.7 · K_T,avg` (avg of storey + adjacent storeys) | `< 0.7` | `< ~0.5` severe — a house must never be here |
| 3 | **Storey mass** | `m(x) ≤ 1.5 · m_avg` | `> 1.5` | `> ~2.0` severe — a roof tank is exactly this mistake |
| 4 | **Diaphragm action** | storey displacements with in-plane flexibility within ~10% of the rigid-diaphragm assumption | 10–20% "non-structural"; > 20% structural | > 20% → design as flexible diaphragm; large openings (> ~⅓ of gross area) or abrupt stiffness changes = diaphragm irregularity |
| 5 | **Out-of-plane offset of bracing elements** | offset ≤ ~0.05·b (b = floor width) | `0.05–0.3·b` | `> ~0.3·b` geometric offset — avoid entirely in houses |
| 6 | **Re-entrant corners** | concavity area ≤ ~15% of bounding rectangle | `> 15%` | narrow slab necks between concavities (< ~0.3·l_avg) flag too |

`K_T` and `r` need a model, but **the agent can compute proxies from plan geometry**:
`I_i = t·l³/12` per wall line (stiffness-share formula), `K_T ∝ ΣI` per direction, centre of
rigidity from `Σ(EI·y)/ΣEI`, radius of gyration of a rectangular plate ≈ 0.25–0.29 of the plan
dimension. The FreeCAD audit (§14.3) implements exactly these proxies.

### 3.2 Elevation regularity criteria (Aufriss)

| # | Criterion | Logic | Notes |
|---|---|---|---|
| 1 | **Vertical geometric** | plan dimension of the bracing system at a storey ≤ ~1.4× that of the storey below (setback `(b−x)/b ≤ ~0.25`; the 0.15–0.25 band = lower consequence) — VERIFY constants | stepped wall setbacks = this irregularity |
| 2 | **Soft storey (Weichgeschoss)** | `K_T,j ≥ 0.7·K_T,j+1` AND `≥ ~0.75 × avg` of the three storeys above (mass-adjusted) — VERIFY ratios | **the open ground floor for parking/shops.** Severe at ≈ 0.5×; soft storeys then need amplified design forces (order 1.5–2× — VERIFY the NA soft-storey multiplier) and DCH-grade detailing regardless of the rest of the building |
| 3 | **Strength irregularity** | storey lateral strength not substantially below the storey above (the plastic mechanism must not be invited to form at a weak floor) | same openings as row 2 cause both |
| 4 | **Mass irregularity** | per §3.1 row 3, storey by storey | roof tank, gallery with stone cladding |
| 5 | **In-plane discontinuity of elements** | no bracing wall/brace offset or interrupted between storeys | **a shear wall that lands on a beam at first-floor level is the single worst defect on this table** |
| 6 | **Out-of-plane offset of columns** | ≤ ~0.3× column dimension in the offset direction — VERIFY | sloping-site steps create it silently |
| 7 | **Torsional (elevation)** | storeys with high torsional sensitivity must not stack with shifting torsional axes | single off-centre core + setbacks |
| 8 | **Foundation** | no large rotational-stiffness differences between adjacent foundation elements | half-basement under part of the plan = elevation irregularity |

### 3.3 Translating the criteria into house-plan rules

**DO**

- Simple rectangular plan. **Aspect ratio ≤ 2:1 preferred, ≤ 3:1 hard.** Long thin plans bend
  in-plane as diaphragms — the deeper the diaphragm span, the more the floor itself spends
  in-plane deformation budget (§4).
- Place walls **symmetrically about both axes**; aim real eccentricity ≈ 0 so the ±5%
  accidental alone rules. **Target e ≤ ~10% of the plan dimension before accidental, then
  verify against the 0.25·r criterion once stiffness is distributed.**
- At least **two bracing lines per direction, well spaced** — a wide couple resists torsion;
  two walls beside each other do not. Put the **longest discs perpendicular to the largest
  loaded façade** (the stiffest elements attract the biggest load).
- **Same wall/column grid every storey, foundation to roof.** An uninterrupted load path is
  worth more than any calculation.
- Equal storey heights (± 10%). One taller room → split into two blocks with a joint (§9.5).
- L/T/U/H/+ plans: prefer **separation joints splitting the building into regular rectangular
  blocks** over analysing the concavity (joint width §9.5).
- Make every floor and the roof a **positive diaphragm** (§4).
- Staircase: inside the bracing core, **or** fully tied in and modelled, **or** separated with
  a designed sliding support. A stair flight is an unintended diagonal brace that attracts
  force it was never designed for; mid-landing beams framing into columns are the classic
  short-column generator.
- Put heavy elements (tanks, stone, planters) **low and over wall lines**.

**DON'T**

- **Open ground storey** under a heavier masonry storey (parking, shops, the panorama-open
  *Wohnküche* without bracing). The classic soft/weak storey and the single most lethal house
  configuration worldwide. If unavoidable: (a) RC shear walls both directions at ground level,
  (b) those elements designed with soft-storey amplification, (c) stiffness never below the
  70% line of §3.2.
- **Short columns (Kurze Stützen):** any partial-height infill, sill wall, ventilator strip,
  mezzanine or landing restraint that braces part of a column's clear height. Shear demand
  scales as `V ≈ ΣMp / h_clear` — halving the clear height doubles the shear; the column fails
  in brittle shear before any flexural ductility mobilises. Fixes: continue the infill full
  height; **or** a designed full-height 25–50 mm isolation gap with compressible filler and
  sealant; **or** design it explicitly as a short column with close hoops over the **entire**
  reduced clear height.
- Asymmetric wall placement — solid masonry on two adjacent sides, glass on the other two →
  the building twists and the flexible corner fails first.
- Cantilevered upper floors or heavy overhangs > ~1.0 m without a designed backspan; never
  cantilever masonry.
- Heavy roofs on weak walls: roof mass is the demand multiplier — in a mass-controlled regime
  every kN up there is spent directly.
- A water tank on a slender independent roof frame (mass + torsion + whip at the worst height).
- Later storey additions ("one floor next year") without re-checking wall layout, W, drift and
  the foundation.
- Adjacent buildings without a separation gap or level alignment (§9.5 pounding).
- All openings concentrated in one wall line with none in the parallel line.
- A basement under only part of the footprint (in-plane discontinuity + differential foundation
  stiffness).

### 3.4 What irregularity costs in method terms

- **Regular, short, stiff, eligible:** linear static analysis with DCM detailing may cover the
  whole design — the common German house case.
- **Irregularities present:** expect escalation — modal (or dynamic) analysis, torsional
  analysis, diaphragm-force amplification, soft-storey multipliers, a reduced q, or outright
  prohibition of the configuration above certain height/class. **Exact eligibility thresholds
  (height limit, T1 vs TB, storey count) — VERIFY EN 1998-1 §4.2.2/§4.2.5 + NA.**
- The agent's deliverable on an irregular plan: the irregularity list naming the violated
  criterion per §3.1/§3.2, the proposed geometric fix, and an explicit note that whatever
  remains is for the engineer to analyse — not to be averaged away.

---

## Section 4: Load Path, Diaphragms, Chords and Collectors (Aussteifung, Scheibenwirkung)

The bracing system only works if floors and roofs **collect** the inertia forces, **transmit**
them in-plane, and **deliver** them into the discs that carry them down to the foundation.
Every step is a named load path; every delivery is a connection (§8). European practice splits
the diaphragm role: a cast RC slab (Massivdecke) is a true disc; hollow-core + structural
topping is semi-rigid; a timber joist floor is a diaphragm **only** with structural boards or
bracing planes **plus** a ring tie (Ringanker).

### 4.1 Diaphragm classification, ranked for houses

| System | Diaphragm quality | Notes |
|---|---|---|
| RC solid slab cast monolithic with ring beams | Rigid — excellent | heaviest option; count its mass; the reference case |
| Precast planks / hollow-core + ≥ 50–75 mm composite topping with mesh + edge ties | Semi-rigid — acceptable | topping and perimeter tie mandatory; keyed joints + transverse compression activate the disc (half-precast/element slabs the same logic) |
| CLT (Brettsperrholz) floor with designed joints and edge ties | Good disc both ways | chord ties at boundaries; concentrate forces into edge members |
| Timber joists + structural board deck + continuous ring anchor | Tied but flexible | works only if deck fastening is designed; bracing planes + edge members |
| Timber joists alone, or planks without topping | None | walls act independently out-of-plane — the historical failure; acceptable only with explicit horizontal bracing trusses + ring system |

**Ring-anchor / designed-diaphragm trigger list (German practice, digested):** buildings
**above 2 storeys**, building length **> 18 m**, large façade openings, unfavourable ground,
or lightweight (joist) floors — whenever the floor is not obviously a monolithic disc, provide
and design the ring. **Ring beam practical span limit: ≲ 30 × slab thickness between
fix-points.** A joist floor without sheathing has **no diaphragm action** — the Ringanker then
carries the entire horizontal distribution alone.

### 4.2 Chord and drag-collector forces (pure statics — universal)

For a rigid diaphragm spanning `L` between two bracing walls spaced `b` apart:

```
Uniform line load w along the diaphragm (total W = w·L):
    chord force      C = T = M/b = w·L² / (8·b) = W·L / (8·b)
Concentrated force P at mid-span:
    C = T = P·L / (4·b)
General: chord force diagram = moment diagram of the diaphragm / b. Draw it.
```

The chord tension is taken by reinforcement along the slab edge — fully anchored at the discs
and detoured continuously around every opening — with slab-edge compression as the return
path. **EC8 amplifies diaphragm/transmission forces for irregularity and ductility class
(capacity-design factors, order 1.0–2.0+ depending on q and NA) — VERIFY the factor; design
the ties at least for the amplified action, never for the bare elastic statics alone.**

**Collector (Verband) rules at openings** (stair, light well, courtyard):

- Collector force changes across an opening by exactly the force the interrupted chord used to
  carry — accumulate it along the edge from a force diagram, don't guess.
- Keep total opening area **≤ ~30% of the floor plate**; trim every opening with a continuous
  chord loop on all four sides — the trimmed ring IS the load detour.
- Never place a large opening adjacent to a disc edge the diaphragm must deliver into.
- **Courtyard / ring diaphragms** (Atrium, Lichthof): the floor is an annulus — full perimeter
  ties on **both** outer and inner edges, and count it as a diaphragm discontinuity in the
  audit.

### 4.3 Stiffness-proportional load sharing (universal statics method)

Storey shear distributes to bracing elements by **lateral stiffness**:

```
Same-height wall group (bending-shear-corrected):
    V_i = (I_i / ΣI) · F,   I_i = t·l³/12   (thickness-weighted centre line)
Flexible / slender walls (cantilever flexibility incl. shear deformation):
    f_i = H³/(3·E·I_i) + 1.2·H/(G·A_i),     G ≈ E/2(1+ν), ν ≈ 0.2 → G ≈ 0.4E
    k_i = 1/f_i;   V_i = (k_i/Σk) · F
    (shear term matters for stocky discs, l/h ≲ 3; digested example split: 73% / 27%)
Torsional moment M_T = F · e (real + accidental) adds a component ∝ stiffness × distance:
    V_i,total = (k_i/Σk)·F  ±  (k_i·r_i / Σ(k·r²))·M_T
System shear/stiffness centre of the wall group (for asymmetric plans):
    YM = [ΣIy·Σ(Iz·Z) − ΣIz·Σ(Iyz·Y)] / [ΣIy·ΣIz − (ΣIyz)²]   (Z analogous)
Equilibrium sanity check: Σ(transverse actions about the centre) → the influence shares must
sum consistently (digested worked checks reach Σ = 1.00).
```

The agent computes the **first-order** version from model geometry (§14.3) and flags elements
whose share swings wildly through asymmetry; the engineer performs the authoritative
distribution with real sections and floor diaphragm behaviour.

**Placement corollaries (digested doctrine):**

- Bracing walls in both directions with **axes not all intersecting at one point** (else
  torsion is unconstrained); minimum determinate layout = ≥ 3 non-parallel, non-concurrent
  restraint lines.
- **Cores:** a closed box (stair/lift/wet rooms) is the classic — bracing out of the usable
  space. A core **must keep surcharge** (perimeter cores lack it → uplift hard to manage).
  Keep it central or proportion the layout (rectangular core, long side perpendicular to the
  large façade). **Peripheral cores at the ends of long buildings → restraint cracks → place
  an expansion joint near the core releasing the slab in one direction; twin cores: slide the
  floor between them or accept Zwängungen — a core's bracing effect dies in the direction you
  slide it.**
- Bracing walls need **vertical load** to develop their shear/friction reserve — rotate floor
  spanning direction storey by storey to keep loading the bracing walls; **never rob a bracing
  wall by putting a column beside it — replace the column WITH the wall.**
- Walls support each other (corner bond / Querscheibe logic): box construction is the ideal —
  which is why the "corner is sacred" rule (§6.5) exists.

### 4.4 Second-order / non-sway eligibility (proxy the agent can run)

A braced (ausgesteiftes) system may be analysed without second-order amplification if, per
principal axis: `F_V,Ed·L² / (E_cd·ΣI_c) ≤ ~0.2–0.3` (recommended constant K1 ≈ 0.31 in the
storey-count form `K1·(n_S+1)/(n_S+1.6)` — **VERIFY the current EN 1992-1-1/NA clause and its
interaction with EN 1998 second-order rules**). If bracing is nearly symmetric, the torsional
variant of the check (warping + St.-Venant terms; plan-diagonal approximation
`ΣF·r² ≈ F_V,Ed·(d²/12 + c²)` with c = shear-centre offset) may be omitted. The agent cannot
run the check authoritatively but can compute `ΣI` from geometry and flag visibly
under-braced plans long before anyone argues about the constant.

### 4.5 Roof-specific rules

- **Light pitched roof (truss or rafter) = very low mass = low demand — seismically the best
  roof system.** Its diaphragm must be explicit: a braced plane (triangulated trusses or
  structural sheathing), continuous ridge/eave members, braced gables, and a continuous ring
  beam at the wall plate; truss/joist ends anchored to the band (straps/holding bolts at
  ≤ ~1.2 m) with ≥ ~100 mm bearing on a wall plate. **A joist end simply pocketed into
  brickwork is a defect.**
- RC slab roof: rigid disc, heavy — count it, tie it, keep the roof band monolithic with the
  slab so band and diaphragm are one element.
- Gables: gable band following the slope + vertical bars at ≤ ~1.5 m, or light gable infill;
  the gable ties into the roof bracing plane.
- Out-of-plane roof→wall anchorage forces: §9.2.

---

## Section 5: Choosing and Placing the Bracing System

### 5.1 Selection logic (decision tree)

```
START: ag·γI (from NA map = LOOKUP), ground class, storeys, supervision level, plan demands
│
├─ 1–2 storeys, compact plan, masonry-built, low/moderate NA demand
│     → CROSS-WALL/BOX MASONRY WITH RING ANCHORS, or CONFINED MASONRY (§6).
│       Simplest reliable option; ductility from geometry, not joint precision.
│
├─ 2–3 storeys, open ground floor wanted, or class D/E ground
│     → CONFINED MASONRY + isolated RC SHEAR WALLS (stair core, or ≥ 2 m walls per
│       direction at the open storey) — continuous to foundation.
│
├─ ≥ 4 storeys, or DCH/q > 1.5 demanded by the plan
│     → RC SHEAR-WALL / DUAL SYSTEM, fully engineered. Masonry above 2–3 storeys is
│       outside every simplified-method envelope — VERIFY the exact simplified limits
│       you are standing on before using them at all (§6.5 note, EN 1996-3).
│
├─ Large column-free span (lobby, basement parking, atelier)
│     → insert an RC frame line or wall box into the masonry house: EITHER separate the
│       systems by a joint OR analyse them together with the interaction designed.
│       Never mix silently (§2.4).
│
├─ Hill site (Hanggrundstück, Alb, Alpenvorland), any zone
│     → stepped foundations + ring beam at every step level + tie system per floor.
│       NEVER a row of varying-length free columns on a cut slope (short column +
│       torsion + foundation rotational irregularity).
│
└─ Existing unreinforced-masonry house → §12 retrofit.
```

### 5.2 Placement rules for discs and cores (universal)

- Bracing **in both directions**, in **≥ 2 lines each**, well spaced apart.
- **Longest discs perpendicular to the largest loaded face** — stiffest elements attract the
  largest load, so make them long and give them surcharge.
- Stiffness balance between directions: `dX/dY` order **0.7–1.4**; outside it, the building
  twists toward the soft direction and one system over-strengths uselessly.
- Stacked stiffness **continuous to the foundation**: a storey without bracing is a
  mechanism, and worst at the base. Shifted walls transfer their reactions via columns —
  **never via floor bending; floors have no transverse stiffness to spend.**
- Stair/lift cores symmetric or paired; a single off-centre core on a long slab = torsion +
  restraint cracking (§4.3).
- The bracing elements are **structure, not furniture**: a wall the client "wants to move
  later" is already in the load path. Decide during the audit, never on site.

### 5.3 Ductile vs brittle bracing behaviour (concepts to reason with)

- **Ductile mechanisms (wanted):** planned flexural yielding at the base of a well-confined
  wall; distributed stepping cracking in confined masonry; planned beam hinges in a capacity-
  designed frame. Predictable, energy-absorbing, standing during and after the event.
- **Brittle mechanisms (suppressed by every rule in §6–§8):** diagonal shear cracking of
  unconfined panels; joint shear without hoops; laps in hinge zones; out-of-plane overturning
  of slender panels; unbonded corners expelling; unanchored heads; short columns; soft-storey
  mechanisms. EC8's detailing apparatus exists to force the structure through the first list.
- Masonry discs fail **in-plane by stepped diagonal cracking** and **out-of-plane by one/two-way
  bending plus corner expulsion**. The ring system (§6) converts the out-of-plane mode into a
  supported panel and confines the in-plane mode; axial load from floors raises shear capacity
  (friction activation) — loading the bracing walls (§4.3) is a seismic act, not only gravity.

---

## Section 6: Confined Masonry & Ring-Beam Practice (Mauerwerk mit bewehrten Beton-gliedern / Ringankern)

Confined masonry inverts the frame sequence — **build the masonry panel first, cast the
confining elements (Randglieder) against it afterwards** — so wall and confinement act as one
composite and failure is distributed cracking, not storey collapse. EC8-1 §10.5 covers masonry
systems; German execution practice leans additionally on DIN EN 1996 + the EC8 NA (typically
low q, DCM). **VERIFY detailing against both — where this section conflicts with a current NA
table, the NA governs.** The geometry below is the practical baseline distilled from good
confined-/masonry-seismic practice and German ring-anchor execution.

### 6.1 The non-negotiable construction sequence (Reihenfolge)

```
1. Foundation + plinth beam (Fundament-Ringbalken) cast
2. Masonry panel built FULL HEIGHT, with toothed edges (Verzahnung) or wall ties at every
   future tie-column position
3. Tie-column reinforcement cage placed against the toothed masonry
4. Tie-column concrete cast AGAINST the masonry (formwork on 2 faces only)
5. Ring/tie-beam (Ringbalken) cage on the wall head, continuous over all tie columns
6. Ringbalken cast monolithically with the floor/roof slab where possible
7. Next storey repeats from step 2.
```

**If the columns are cast before the wall, it is not confined masonry** — it is an undetailed
frame with infill (§2.4), the collapse archetype. This one sequencing rule is the thing most
often lost on site: put it on the drawing in German and photograph the toothing before the
cage goes in.

### 6.2 Tie-column / vertical confining element (Randglied) schedule

| Parameter | Requirement (practice baseline — VERIFY vs EN 1998-1 §10.5 + NA / EN 1996) |
|---|---|
| Mandatory at | every external corner; every wall junction (L/T); every free wall end; **both jambs of every opening wider than ~1.2 m** (or > half the storey height); both sides of every movement/seismic joint |
| Max spacing along a wall | **~4.5 m at higher demand, ~6.0 m in low NA zones**; also ≤ 1.5 × storey height |
| Minimum section | wall thickness × ≥ 200 mm; for a 24 cm wall use **24 × 24 cm**; never < 150 mm in any dimension |
| Minimum concrete | C20/25 preferred (legacy practice C16/20); ≤ 16 mm aggregate for congested cages; soft consistency (S4/F5 class) so it flows against the toothing |
| Main reinforcement | **4 × Ø12 mm B500 minimum** (the legacy German tie-reinforcement benchmark is 4Ø12); 4 × Ø16 for 3 storeys or at the ground storey of higher demand |
| Links | Ø6–8 @ 200 mm at mid-height; **@ 100–150 mm within ~450 mm of each end** (the joint region is exactly where it fails) |
| Hooks | **135° seismic hooks, extension ≥ 6Ø and ≥ 75 mm.** 90° hooks are a defect — reject them |
| Cover | per EN 1992-1-1 exposure-class table; ≥ 20 mm to links on faces cast against masonry, more where earth-exposed |
| Lap splices | ≥ 50Ø; **never inside the joint region**; stagger < 50% lapped at one section |
| Continuity | plinth beam → every ring beam → roof; anchored ≥ ~40Ø into each horizontal member |
| Casting | full storey height in one pour — no cold joint at mid-height |

**Quantity check:** one 240 × 240 × 3200 mm Randglied ≈ 0.18 m³ concrete, ≈ 16–18 kg steel.

### 6.3 Ring beam / tie beam (Ringbalken, Ringanker) schedule

| Parameter | Requirement |
|---|---|
| Levels — mandatory | **plinth**, **lintel level (all openings in one continuous band)**, **every floor**, **roof**; plus a **gable band** following any gable slope |
| Max vertical spacing | **≤ ~3.0 m** — at least one per storey; add the lintel band wherever storey height > ~2.7 m or openings are large |
| Minimum section | width = wall thickness; depth ≥ 150–200 mm (~240 mm at higher demand) |
| Reinforcement | 4 × Ø12 minimum (2 top, 2 bottom); links Ø6–8 @ 150–200 mm, **closed up at every intersection**; legacy German benchmark for foundation/wall ties: 4Ø12 B500 |
| Continuity | **fully closed loop around the entire perimeter AND along every internal load-bearing wall.** A band that stops at a doorway is not a band |
| Corner detail | bent/L bars with ≥ ~40Ø anchorage both ways; **never two straight bars simply overlapping at the corner — the corner is where the band earns its keep** |
| Merge rule | lintel band and floor band within ~500 mm → merge into one deeper band, not two weak ones |
| Interaction with slab | cast monolithically where possible → band + diaphragm one element (§4) |
| Robustness floor | EN 1992-1-1/NA robustness ties for slabs require edge ties of order **70 kN** (digested benchmark) — the seismic ring beam must not be weaker than the non-seismic one |

**Quantity check:** 240 × 240 band ≈ 0.058 m³/m concrete, ≈ 4.8 kg/m steel.

### 6.4 Masonry panel rules (EN 1996 context)

| Parameter | Requirement |
|---|---|
| Wall thickness | ≥ 24 cm for load-bearing seismic walls (the EN 1996 bracing-wall definition already demands ≥ 11.5 cm, `t ≥ ⅓` of the braced wall, effective length ≥ h/5 — **VERIFY seismic NA may demand more**); 11.5 cm = partition only, never counted, never carrying a slab |
| H/t slenderness | ≤ ~25 (1–2 storey), ≤ ~20 (3 storey) as out-of-plane proxy — the real check is §9.2/§9.3 |
| Panel between confining elements | ≤ 4.5–6.0 m; panel aspect (length:height) preferably ≤ 1.5 |
| Minimum counted pier | ≥ 1.2 m long and length/height ≥ 0.4 |
| Units | solid or high-quality masonry units per EN 771; **fill head joints in counted shear walls** — leaving them open roughly halves the initial shear strength (digested: open-joint fv values ≈ half of pointed values) |
| Mortar | ≥ M5 (MG II); richer at the ground storey under higher demand; joints 10–12 mm |
| Bond | full bed **and** head joints; proper lap (Überbindung) — staggered bond IS the in-plane shear coupling (digested masonry doctrine) |
| Toothing | alternate courses 50–60 mm into the future Randglied, **or** bed-joint anchors (2 × Ø6 every ~3rd course) extending ≥ 400 mm into panel and column |
| Wetting & curing | units dampened before laying (dry units suck the mortar and roughly halve bond — the strength the whole system depends on); mortar cured |
| Chases | no vertical chase in a counted wall or Randglied; horizontal/inclined chases only per the EN 1996-1-1/NA slot tables (digested: walls t > 11.5 cm, within ~400 mm of floor/ceiling, in installation zones, never in horizontally-perforated units, never in chimney flues, avoid bearing zones) |

### 6.5 Opening rules (simplified-method good-practice table — VERIFY vs EN 1996-3/NA + EC8)

`L` = wall length between cross-walls / confining elements:

| Rule | 1 storey | 2 storey | 3 storey |
|---|---|---|---|
| Σ opening length ≤ | 0.50·L | 0.42·L | 0.33·L |
| Pier between two openings | ≥ 0.5 m | ≥ 0.6 m | ≥ 0.6 m |
| Junction corner → nearest opening | ≥ 0.5 m | ≥ 0.6 m | ≥ 0.6 m |
| Vertical distance, stacked openings | ≥ 0.6 m | ≥ 0.6 m | ≥ 0.6 m |
| Opening area % of wall face | ≤ 30% | ≤ 25% | ≤ 20% |
| Opening > 1.2 m wide | Randglied at **both** jambs | same | same |
| Opening head | bears ≥ 240 mm each side under the continuous lintel band | same | same |

Universal perforated-façade doctrine (digested German masonry rules) behind the table:
**keep openings strictly stacked, equal width per floor** — offsets force horizontal load
detours → tension cracks and pier concentration; window height is unimportant **as long as the
parapet strip keeps racking/frame action**; avoid openings against corners; a storey-high stack
of openings splits the panel into two halves levering against overturning.

**Corner windows** (opening wrapping the building corner): **prohibited in masonry construction
at any meaningful seismic demand** — they destroy the corner, the single most important element
of the masonry box. When a client insists: (a) move it ≥ 600 mm off the corner, (b) make the
corner a designed RC element carrying the full corner force, or (c) document the performance
reduction in writing and let the engineer decide.

**Lintels (Stürze):** arch action above an opening is self-supporting only for the load wedge
over the opening (base = opening width, apex up — the digested EN 845-2 way of thinking), so
the lintel carries that wedge plus any superimposed tie force; masonry arch/flat lintels act as
compression chord + steel tie for spans ≲ ~3 m with undisturbed springing piers; RC/steel
bending lintels concentrate reveal stresses, and steel lintels' differential thermal movement
cracks the render around them (digested). Room-height openings: use the slab edge itself as the
lintel with local top reinforcement.

### 6.6 Reinforced / grouted masonry variant (where confinement is impractical)

Vertical bars in aligned cells, **fully grouted** (grout C12/15–C25/30-class, high flow, lifts
≤ 1.5 m, consolidated), bars at every corner/end/jamb and at ≤ ~1.2 m centres under higher
demand (≤ ~2.0 m under low demand), bed-joint reinforcement every ~3rd course, plus the §6.3
band system. Ungrouted cells around a bar are the classic hollow-block failure. Reinforced
masonry is *more* sensitive to grouting quality than confined masonry is to concrete quality —
on an unsupervised site, prefer confined. (VERIFY vs EN 1996-1-1 §9 + NA.)

### 6.7 Confined-masonry defect list — site reject criteria (universal)

- Tie columns cast **before** the masonry (a frame masquerading as confined masonry).
- Smooth, untoothed, tie-less vertical joint between column and wall → zero shear transfer.
- Links with **90° hooks**, or hooks straightened on site to fit the formwork.
- Uniform link spacing with **no closing-up at the ends**.
- Lintel band stopped either side of a door and "made up" with a loose precast lintel.
- Roof band omitted "because the RC slab does the same job" — it does not, unless the slab is
  designed as a diaphragm and tied into every wall.
- Tie-column bars lapped at floor level, inside the joint region.
- Half-leaf walls counted structurally or carrying slab edges.
- Hollow-block walls with ungrouted cells.
- Chases cut post-cast through a Randglied or the middle of a counted shear wall.
- Unvibrated honeycomb at exactly the joint region; cold joint mid-height in a Randglied.
- Dry-laid units, unfilled head joints.

---

## Section 7: RC Frames and Walls — Ductile Detailing (Duktilitätsgerechte Ausbildung)

Apply when the system genuinely requires it or when the NA pushes toward DCH. The tables below
are EC8 capacity-design logic in universal form; **every value carries a VERIFY tag —
DIN EN 1998-1 §5.4 + NA is the source of truth.** Design material values per the digested
EC2 German benchmarks (fcd = αcc·fck/γc with αcc = 0.85, γc = 1.5 → C30/37: fcd = 17.0 N/mm²;
B500 fyd = 435 N/mm²) — confirm against the current EN 1992-1-1/NA.

### 7.1 Beams (DCH)

- Plastic-hinge regions: **2h from each face of the support** (h = beam depth) — VERIFY.
- Inside hinges: links with 135° hooks; spacing ≤ min(h/4; 6Ø_long; ~150 mm tightening with
  moment demand) — **VERIFY Table 7.x values.**
- **Compression steel ≥ 50% of tension steel** at the support section (moment reversal
  ductility) — VERIFY.
- Continuous bottom steel at joints ≥ ½ of top steel at the joint; ≥ ¼ of top at mid-span —
  VERIFY.
- Geometry: clear span ≥ 4h; width ≥ ~0.3h and ≥ ~200 mm; l/d limits per §7.5 of the frame
  design standard — VERIFY.
- **Shear from moment capacities, not analysis shear** (capacity design):
  `V_Ed = (M_Rd,L + M_Rd,R)/l_n + V_Ed,G`, envelope of both hinge sign combinations.
- Laps prohibited inside hinge zones (DCH); restricted in DCM — VERIFY.

### 7.2 Columns (DCH)

- Min section dimension ≥ ~200 mm; ratio of side lengths ≥ ~1/3 — VERIFY.
- **Axial-load limit** so confinement can deliver rotation capacity: `ν_d = N_Ed/(A_c·f_cd)`
  capped in the order 0.5–0.65 by ductility class — **VERIFY exact values.** Exceeding the cap
  means enlarging the section, not adding hoops.
- **Strong column – weak beam at every joint:** `ΣM_Rd,c ≥ 1.1·γ_Rd·ΣM_Rd,b` with `γ_Rd` of
  order 1.2 (DCH) / 1.1 (DCM) — **VERIFY the exact product (order 1.2–1.35) in the NA;**
  distribute the joint moment sum to the columns above/below in proportion to their capacity.
- Confinement length each end: `l0 = max(h_col; l_n/6; ~450 mm)` — VERIFY; link spacing
  inside `l0` ≤ min(b0/4; 6Ø_long; ~150–175 mm demand-dependent) — VERIFY; with crossties
  instead of closed hoops, apply the capacity reduction factor (order 0.6–0.8) — VERIFY.
- Laterally supported longitudinal bars: clear spacing ≤ ~200 mm → crossties on interior bars
  of wide/heavily loaded columns.
- First link ≤ 50 mm from the joint face; **links continue through the joint.**
- Joints: beam bars anchored with standard hooks into the confined core; joint shear checked
  from beam tensions developed at capacity; the joint is a separate, independent gate from
  the strong-column check — **either can govern.**
- Column shear: capacity-designed from the over-strength hinge sequence above and below —
  **never** the bare analysis storey shear; a frame's own yielding can drive column shear far
  above it.

### 7.3 RC shear walls (Stahlbeton-Aussteifungsscheiben) — the house-scale rescue for open plans

| Parameter | Rule (VERIFY vs EN 1998-1 §5.4.4 + §7 + NA) |
|---|---|
| Minimum thickness | ≥ 150 mm (≥ 200 mm preferred at the base) |
| Reinforcement | ≥ ~0.25% (order 0.0025) each face; two curtains where t ≥ 200 mm or shear is high; spacing ≤ 450 mm |
| Boundary elements | confined end zones where compressed stress exceeds ~0.2·fcd or where flexural demand is DCH — detail as a confined column |
| Base plastic hinge | no lap splices or cold joints in the hinge height above the base (order = wall length for stocky walls — VERIFY); bars anchored into the footing with full development **and a real uplift tie** (§8.2) |
| Shear | capacity-designed from the over-strength base moment; verify the diagonal-compression/tension checks of the concrete standard |
| Placement | symmetric, both directions, continuous to the foundation on its own footing/raft strip |
| House use | two ~2 m walls per direction at the open storey; stair/lift core as coupled or uncoupled core |
| Fatal mistake | a wall that stops at first-floor level on a beam — in-plane/out-of-plane discontinuity, the worst row in §3.2 |

Coupled walls: coupling beams ductilely reinforced (diagonal bars for stocky openings) —
VERIFY; beyond most house needs.

### 7.4 Infill in frames — decide explicitly (§2.4), and remember the short column (§3.3).

### 7.5 Worked example pattern — joint-level check, done honestly (arithmetic path only)

One exterior joint of a 2-storey RC frame, all inputs illustrative:

```
Beam top steel at joint: As = 4Ø20 = 1257 mm², d = 400 mm; C30/37 fcd = 17.0, B500 fyd = 435
  a = As·fyd/(0.85·fcd·b) = 1257·435/(0.85·17·300) ≈ 126 mm
  M_Rd,beam ≈ As·fyd·(d − a/2) ≈ 1257·435·337 ≈ 184 kNm
Strong-column-weak-beam: ΣM_Rd,c ≥ ~1.32 × 184 ≈ 243 kNm, split above/below by column
  capacity — check each against its own interaction curve at REAL Nu (the engineer's job).
Joint shear at yield: beam-bar tension T = As·fyd ≈ 546 kN; V_joint = T − V_col;
  compare with joint shear capacity ≈ 0.5–0.7·fcd·A_j for an exterior joint confined on
  two faces or fewer — a 350×350 joint CAN fail this even when the strong-column check
  passes. Fixing it = bigger column (bigger A_j), more confinement category, or less
  beam steel/span.
```

The lesson is deliberate: **passing the equilibrium-style strong-column check does not prove
the joint; the shear check is an independent gate.** The agent runs neither authoritatively —
it delivers geometry, load path and flags so the engineer runs both.

---

## Section 8: Connections, Continuity and Anchors (Anschlüsse, Verbinden)

### 8.1 The Schlussarten matrix (the agent's design language for every joint)

Every joint direction (6 translations + 6 rotations) must be assigned a closure type:

- **Formschluss (form-fit):** the load itself closes the joint; needs assembly play; force
  transmits only after slip — pockets, dowels, stacking, keyed joints.
- **Stoffschluss (material bond):** welding, gluing — rigid in every sense, blocks
  deformation → Zwängungen (restraint forces); irreversible.
- **Kraftschluss (force/friction-fit):** preloaded bolts, clamping, friction; adhesion
  (bonded anchors, mortars) grouped here — depends on surface + normal force, sensitive to
  relaxation, creep and dynamic load.

Masonry bed joints live on tangential Kraftschluss activated by surcharge — which is exactly
why **bracing walls need vertical load** (§4.3) and why lightweight masonry without floor
loads topples. Saying "the connection is rigid" describes one direction; classify them all.

### 8.2 Continuity doctrine — keep the force on the shortest path

- **"Don't take forces for a walk."** Align element axes concurrent at one point where
  possible; every detour (offset wall, interrupted ring beam, unbonded corner) is a bending
  demand and a candidate failure point.
- The seismic load path is a **tension chain**: disc edge → chord → collector → disc (wall or
  head beam) → **hold-down** → foundation → ground. Tension does not turn corners through
  mortar alone: corners need bond (Verzahnung, bed-joint anchors) or bent steel with ≥ ~40Ø
  anchorage. **A band that stops at a door and a corner without corner bars are the two ways
  the chain silently breaks.**
- Introduce point loads where the receiving member is stiffest: normal load onto a thin shell
  = local buckling/crushing; tangent load = fine. Spread bearing (base plates, elastomeric
  pads, wide washers) — the compression-joint conditions (full-area contact, plane ⊥ force,
  equal strength faces, anti-slide) are all four needed.
- Stagger butt joints between layers; never stack the weak points of structure, insulation,
  airtightness and weather skin in one plane (seismic corollary of the layering doctrine:
  stacked defects propagate).

### 8.3 Mechanical anchors in cracked concrete — concept + VERIFY

**This skill's digested sources contain no seismic anchor capacity tables; nothing numeric is
given here.** Conceptual discipline:

- Seismic anchors sit in **cracked concrete under cyclic/reversed loading**. A post-installed
  anchor in a ring beam, slab edge or wall head is a cracked-concrete, seismic-qualification
  problem — specify fasteners with **ETA approval for cracked concrete and seismic action
  (category C1/C2 per EN 1992-4)**; a general-purpose fastener is not an anchor.
- Keep the failure modes apart when reading any data sheet: **concrete cone** (governed by
  edge distance!), **pull-out** (embedment), **splitting** (spacing), **steel rupture**
  (ductile — the only failure you may want), **pryout** (shear near an edge). Edge distance
  and spacing govern realistic anchor groups far more than the bar size does.
- Design values = declared capacities × seismic modification factors (α_ct for cracked
  concrete, cyclic displacement class, group factors) — **run these with the engineer;
  EN 1992-4 / ETAG/ETA is the source of truth.**
- **Prefer cast-in continuity at concept stage** — starter bars, loops, closed stirrup anchors
  through the Ringbalken — over post-installed, precisely for the edge cases nobody checks on
  site.
- Where insulation is penetrated by fixings, every anchor is also a thermal bridge and a
  sealing breach (digested envelope doctrine): route façade-element fixings to the structure
  through designed brackets, not through the render skin.
- Roof/uplift straps and truss anchors: the same philosophy plus the wind combination — for
  elements with tributary area < 10 m² use the increased façade pressure coefficients
  (digested EN 1991-1-4 anchorage rule).

### 8.4 Bar continuity (EC2 logic the engineer completes)

- Basic anchorage `l_lb = α·(Ø/4)·fyd/fbd`; bond strengths for ribbed B500 in good bond
  (digested table order: fbd ≈ 2.7 N/mm² C25/30, 3.0 C30/37) → required lengths of order
  40–65×Ø; hooks/loops/welded transverse bars cut required length (α factors 0.5–0.7 digested)
  — **all VERIFY vs current EN 1992-1-1/NA tables.**
- Minimum anchorage at direct supports and lap-zone rules (α1…α6 factors, lap ≥ max(0.3·l_lb,
  15Ø, 200 mm) digested structure) — engineer's calculation; the agent's rule is simpler:
  **any bar meant to carry seismic tension must visibly continue and bend into something
  confined — "the chain never ends in mortar."**

---

## Section 9: Non-Structural Elements (Nichttragende Bauteile) — where injuries actually come from

Falling non-structural elements cause a disproportionate share of earthquake injuries, and they
are the cheapest things in the project to fix. EC8 §4.3.5 component-force logic:

```
F_pa = γI · Se,e(Tp) · μ · Wp      (amplified element spectral force, per horizontal direction)
μ    = amplification factor by element type and support ductility — cantilevers anchored at
       the top of a flexible structure get the largest values (order 2.5–3.5+) — VERIFY table
Simplification often permitted for stiff short-period elements: take the element spectrum at
       the rigid-support value (Fp ∝ ag·γI·S·μ·Wp, divided by a component behaviour factor
       where the NA allows) — VERIFY the permitted simplification in DIN EN 1998-1/NA.
```

### 9.1 Component schedule (rules the agent can enforce on a model)

| Element | Rule |
|---|---|
| **Boundary/garden walls** | the classic moderate-quake killer (Emilia 2012: boundary walls). 24 cm wall: max free height **~1.8 m** with piers ≥ ~34 cm at ≤ 3.0 m centres, continuous coping band, foundation tie; **11.5 cm walls: nothing freestanding above ~1.0 m.** Gate piers designed for the gate's dynamic load. |
| **Parapets** | unreinforced max free height **~600 mm**; above that: vertical bars continuous from the roof band + coping beam — and check against §9.2 demand **plus wind** (free-standing solid-wall pressure coefficients run to ~2.3 — digested). A 1.2 m unreinforced parapet is a guillotine at roof level, where μ is largest. |
| **Roof tanks** | over wall/column lines, strapped down, **full** mass in W, never on a slender independent frame. |
| **Water heaters, boilers, LPG** | strapped to structural elements; **flexible connections on all gas lines** (post-earthquake fire is the secondary killer). |
| **WDVS/ETICS façades** | the skin is small dead load, but: (a) its fixings penetrate the insulation plane — **never use the façade as a load path**; forces to the leaf go through designed brackets; (b) anchor design combines §9.1 component force + wind with the small-tributary-area coefficient increase; (c) heavy sill boards, copings, stone-look panels above ~3 m: mechanically anchored, never mortar-adhered alone. (VERIFY combined wind+seismic per NA.) |
| **Chimneys, PV ballast, planters, antennae** | components: anchored, mass counted where on the structure; ballast on flat roofs adds disc mass and wall-head demand. |
| **Suspended ceilings, fans, fixtures** | positive fixings to the structural slab (fans to slab hooks, never to board); services braced where required. |
| **Partitions** | horizontal line loads per DIN 1033-1 logic (digested): **0.5 / 1.0 / 2.0 kN/m at ~0.9–1.2 m** by occupancy category; build **top-down with a sliding head gap** so drift/settlement never loads them; never chase load-bearing walls outside the §6.4 slot rules. |
| **Glazing over circulation** | laminated; edge clearance for design drift (§9.4). |
| **Escape route** | one outward-opening exit never blockable by parapet, boundary wall or tank — check against every row above. |

### 9.2 Wall→diaphragm anchorage and out-of-plane demand (the argument for bands)

Universal logic (form shared by EC8 §4.3.5 and its predecessors): **Fp ∝ mass × height
amplification ÷ element ductility**, floored and capped. Illustration with placeholder numbers
(replace with NA values — do not design from these):

```
24 cm brick wall, top storey: Wp ≈ 0.24 × 19 ≈ 4.6 kN/m² face weight.
A plausible moderate-hazard demand at roof level: w ≈ 2 kN/m².
One-way span 3.2 m between bands:  M = w·L²/8 ≈ 2.6 kNm/m
Z (1 m strip, 24 cm): 1000·240²/6 = 9.6·10⁶ mm³  →  σ ≈ 0.27 MPa flexural tension.
Unreinforced masonry normal to bed joints carries well BELOW this.
```

Conclusion: a perfectly ordinary storey-height brick wall **cannot** span out-of-plane
elastically under earthquake action; it survives only because bands and Randglieder turn it
into a four-side-supported panel. **Never omit the lintel/roof band to save money on a tall
room.** (Cross-check intuition against the digested EN 1996-3 simplified envelope: storey
≤ 2.75 m, live ≤ 5 kN/m², height ≤ 20 m, RC floor span ≤ 6.0 m — outside it, calculate.)

### 9.3 Out-of-plane geometry limits

- H/t ≤ ~25 (1–2 storey) / ≤ ~20 (3 storey); bites on double-height rooms, stairwells, gables.
- Unsupported panel dimension > ~4.5 m in either direction → intermediate confining element,
  ratio be damned.
- Free-standing cantilever height ≈ t × (order 6–8) as gut-feeling cap, then §9.2.

### 9.4 Drift and damage limitation

- SLS drift (frequent earthquake, q = 1): limits order **0.5% for brittle / 1.0% for ductile
  non-structure** of storey height — **VERIFY EN 1998-1 §4.4.2 + NA.** At 3 m storeys that is
  15–30 mm: generous for modern movement joints, brutal for unreinforced masonry infill —
  which is why isolation gaps (§2.4) are a drift provision, not a construction courtesy.
- New unreinforced-masonry (URM)-adjacent detailing should respect the stricter service-level cracking intuition
  (≈ 0.2–0.4%) even where the code's collapse cap is looser.

### 9.5 Joints, separation, pounding

- Movement/seismic joint: full height foundation→roof; compressible filler + flexible sealant
  + slip cover. **A joint bridged by plaster, tiles or a coping is not a joint.**
- Width (practice logic — VERIFY against NA drift rules): within one building ≥ 25 mm +
  ~15 mm per metre of height above ~3 m; between buildings ≥ `√(δ1² + δ2²)` (SRSS of expected
  drifts), unknown neighbour → at least your own design drift. On tight urban plots where a
  real gap is impossible: **align floor levels so slab meets slab, never slab against
  column** (mid-height impact manufactures a short column next door), and record the residual
  risk in writing.

---

## Section 10: Site & Ground — screening summary

- Ground class from boreholes/CPT with measured `vs,30` (§1.4) — **assumed = placeholder;
  say so every time.**
- Class D/E: amplified action → re-check q choice, diaphragm flexibility, foundations; consider
  site-response analysis for taller/important builds (EN 1998-5 — VERIFY).
- Topography: crest/ridge/edge amplification; Hanggrundstück treated one step worse in the
  audit even where the map doesn't, plus landslide check; setback from crest ≥ slope height
  where feasible; retaining structures structurally independent of the house.
- **Liquefaction (Verflüssigung):** saturated loose-to-mid granular soil below the water
  table — screening per EN 1998-5 §4.2 (ground-type/liquefactibility classes; damage-factor
  approach from magnitude, PGA, depth, fines content, plasticity, water table). German
  relevance is local but real: North-German glacial sands, river floodplains (Elbe, Rhine,
  Oder, Danube corridors), mining subsidence ground, hydraulic fills, port reclaim. Where the
  geotechnical report flags susceptibility: no prescriptive shortcut — engineer, possibly
  ground improvement or raft.
- **Seismic earth pressure on retaining walls:** design for static + dynamic increment
  (Mononobe–Okabe logic `ΔKa·γ·H²/2`; for typical geometry the increment is of the order of a
  third of the static wedge — placeholder until the engineer calculates it). A static-only
  retaining wall touching the house is a standing omission.
- Near-fault / mapped-fault provisions (narrow-band pulse effects): **LOOKUP in the NA**;
  rare but the reason "between zones → take the worse side" exists.

---

## Section 11: Foundations (Gründung) — the base of the load path

| Item | Rule |
|---|---|
| Plinth ring beam | continuous both directions under every load-bearing wall/column line (4Ø12-class steel, §6.3 links) — the seismic base of the tension chain |
| Isolated footings | never left untied where the NA applies tie rules: tie beams both directions, sized order **10% of the larger column's design axial force** — VERIFY the NA figure |
| Strip footings under walls | continuous; bars both layers; **stepped, never sloped** at level changes (step ≤ ~600 mm rise, ≥ 1.2 m run) |
| Mixed foundation types | **never** mix pads + strips, or shallow + deep, under one continuous block — differential dynamic response cracks the box |
| Raft / basement box | the natural answer on class D/E, variable ground, high water table, or overlapping strips |
| Split-level / slope | stepped footings + ring beam at every step; no row of varying free lengths (§5.1) |
| Founding depth | below frost (granular filter or depth below frost penetration — digested), below fill/organics; geotechnical recommendation governs |
| Basement | rigid lateral restraint helps, but the diaphragm system (§4) and band system still rule; the "basement wall without calculation" EN 1996-3 bounds are **not** a seismic permission |
| Water near founding level | drainage/waterproofing become structural issues (softening and buoyancy under cyclic load); water-retaining concrete discipline is the engineer's territory |

---

## Section 12: Retrofit of Existing Stock (Bestand)

Most pre-1970s (and many later) Central-European low-rise stock is unconfined masonry on
joist or lightweight floors. **Framework: DIN EN 1998-3 (assessment and retrofit of buildings)
+ NA — VERIFY assessment levels and safety factors; retrofit design is harder than new design
and still needs the engineer.** Universal triage order — every earlier step is cheaper and more
life-saving than every later one:

1. **Remove the hazard:** demolish oversized unreinforced parapets, unbraced boundary walls,
   heavy roof surcharges; heavy roof → light roof. Cheapest and often the single most
   effective act in the whole programme.
2. **Out-of-plane restraint + roof/wall connection:** horizontal bracing plane in the roof,
   wall-head band, straps from roof members into the band, joist heads tied (the historical
   iron anchor did exactly this — modern equivalent: ring beam + strapping).
3. **Box action at corners:** corner stitching (diagonal mesh/rebar across both faces of every
   external corner); through-stones/through-bolts (≤ ~1.2 m × ~0.6 m) to tie leaves of rubble
   or two-leaf walls — delamination is the stone failure mode.
4. **In-plane strength:** mesh-and-mortar overlays ("splint and bandage": welded mesh on
   through-bolts ≤ ~450 mm + 25–40 mm rich plaster/micro-concrete; surface-mounted RC or steel
   eaves band fully anchored); ferrocement/shotcrete overlays (structural change — design it);
   inserted RC walls on own footings tied into each diaphragm level.
5. **Foundation:** plinth ties, tie-beam grid under isolated footings, underpinning where the
   audit shows a soft or mixed base.

**Doing 4 before 2 is the common dangerous inversion: a strengthened wall that still cannot
span out-of-plane fails the same way, with more mass above it.** Short-column cures and
soft-storey fixes apply identically in retrofit; every intervention above cosmetic level needs
statical verification.

---

## Section 13: Quality-Control Mindset (Nachdenken vor Gießen)

- **Self-document the design basis in the model** (property set on the Building object): NA
  zone + map edition + lookup date, `ag·γI`, ground class (and that it is assumed until
  boreholes exist), system, q, ductility class, `T1`, `W`, `V_B`, distribution and
  accidental-eccentricity rules used, analysis eligibility assumed. A model that does not
  record its assumptions will be silently misinterpreted by whoever uses it next.
- Photograph **every reinforcement cage before the pour**, dated and filed; photograph
  toothing/dowels before tie-column formwork (§6.1).
- Walk the ring-beam loop physically: confirm it closes at every door, duct and stair.
- Vibrate concrete (poker space inside the cage), cure ≥ 7 days; measure mortar; full joints;
  dampen units; no post-cast chases.
- Dated site notes whenever a VERIFY-flagged number is actually consumed by a decision — the
  audit trail is worth more than the calculation.

---

## Section 14: Encoding the Design in FreeCAD & Auditing Any Plan

Pairs with the FreeCAD/BIM skill (Site/Building/Storey hierarchy, parametric openings) and the
FreeCAD MCP (`execute_code` via neka-nat/freecad-mcp) for geometry queries. The audit below is
**geometry-level proxy work: it classifies configuration risk; it never replaces analysis.**

### 14.1 Modelling conventions

- Model Randglieder as separate structures (`IfcType = "Column"`), never merged into the wall
  solid — countable, checkable, IFC-exportable.
- Model ring beams as `IfcType = "Beam"` along wall tops; Description =
  `RINGBALKEN PLINTH / LINTEL / FLOOR / ROOF`.
- Load-bearing walls `Width = 0.24 m`; partitions 0.115 m, so scripts exclude them.
- Keep walls axis-aligned; a 45° wall is a nonparallel-system irregularity and both a
  counting problem and a script flag.
- Openings as real parametric Subtractions, so piers net out correctly.
- Model the roof tank with real mass at real location.
- Building object carries the §13 property set.

### 14.2 Plan-quality audit checklist (run on any plan; mark pass/flag per line)

- [ ] Plan aspect ratio ≤ 2:1 (flag > 3:1 → joint or redesign)
- [ ] Re-entrant projection ≤ ~15% of bounding-rectangle area (else jointed blocks)
- [ ] Wall density (counted area / floor area) in **X and Y, every storey** vs project
      requirement set by the engineer (from V_B and the masonry shear capacity he states)
- [ ] X/Y counted-stiffness ratio 0.7–1.4 (proxy `Σt·l³` per direction)
- [ ] Ground-storey counted wall length ≥ storey above × 0.7 (soft-storey proxy; report
      actual ratio)
- [ ] Stiffness-centre ↔ mass-centre eccentricity ≤ ~10% of plan dimension per direction
      (proxy; target 0)
- [ ] Identical wall/column footprint every storey (vertical continuity; in-plane offset =
      instant flag)
- [ ] Randglied at every corner, junction, free end, both jambs of openings > 1.2 m
- [ ] Max Randglied spacing ≤ project value (4.5–6.0 m; ≤ 1.5 × storey height)
- [ ] Ring beams modelled plinth/lintel/floor/roof, closed loops, no gap at doors; gable band
      on gables
- [ ] Openings vs §6.5 table (Σ width, pier ≥ 0.5–0.6 m, corner distance, stacked spacing,
      area %)
- [ ] No short-column geometry (wall end vs column free length)
- [ ] Storey heights ±10%; storey masses ≤ 1.5 × avg; diaphragm openings ≤ 30% + trimming
- [ ] Parapets ≤ 600 mm unreinforced; boundary wall piers/coping modelled; tank with real mass
- [ ] Movement joints modelled at full width, unbridged
- [ ] Design-basis property set present; every exported sheet bears
      **VORABPRÜFUNG — NICHT FÜR AUSFÜHRUNG — TRAGWERKSPLANER ERFORDERLICH**

### 14.3 FreeCAD geometry audit script (Python console / execute_code)

```python
import FreeCAD as App, math

doc = App.ActiveDocument
MIN_T_STRUCT = 200.0        # mm - below this it is a partition
MIN_PIER     = 1200.0       # mm - shorter pier contributes ~nothing in shear
TOL_ANG      = 15.0         # deg - non-orthogonality flag

def storey_walls(storey):
    out = []
    for o in storey.Group:
        if getattr(o, "IfcType", "") != "Wall":
            continue
        t = float(o.Width.Value); L = float(o.Length.Value)
        for sub in getattr(o, "Subtractions", []):          # net off openings
            try: L -= float(sub.Width.Value)
            except Exception: pass
        ang = math.degrees(o.Placement.Rotation.Angle) % 180.0
        d = "X" if (ang < TOL_ANG or ang > 180 - TOL_ANG) else \
            ("Y" if 90 - TOL_ANG < ang < 90 + TOL_ANG else "?")
        out.append((o.Name, t, L, d))
    return out

for st in [o for o in doc.Objects if "IfcBuildingStorey" in str(getattr(o, "Type", ""))
           or getattr(o, "IfcType", "") == "BuildingStorey"]:
    walls = storey_walls(st)
    A = {d: sum(t * L for (_, t, L, dd) in walls if dd == d) for d in "XY"}
    I = {d: sum(t * L**3 / 12.0 for (_, t, L, dd) in walls if dd == d) for d in "XY"}
    counted = [(n, t, L, d) for (n, t, L, d) in walls if t >= MIN_T_STRUCT and L >= MIN_PIER]
    skipped = [w for w in walls if w not in counted]
    flag_nonorth = [w for w in walls if w[3] == "?"]
    area = float(getattr(st, "Area", 0) or 0)   # mm^2; else set from plan
    dx = 100 * A["X"] / area if area else 0
    dy = 100 * A["Y"] / area if area else 0
    bal = I["X"] / I["Y"] if I["Y"] else float("inf")
    print(f"{st.Name}: dX={dx:.2f}%  dY={dy:.2f}%  Ix/Iy={bal:.2f}"
          f"  {'OK' if 0.7 <= bal <= 1.4 else 'TORSION-RISK'}")
    for s in skipped:   print("   skipped:", s)
    for s in flag_nonorth: print("   NON-ORTHOGONAL - IRREGULARITY:", s)

# soft-storey proxy: compare counted wall length per direction, ground vs first upper:
#   ratio < 0.7 -> SOFT STOREY FLAG;  also print per-storey so the engineer sees the table.
# eccentricity proxy: rigidity centre YM = sum(EI_i * y_i)/sum(EI_i) (X analogous) against
#   the mass centre; report e/r against the ~0.25 line (§3.1) once centroids are wired in.
print("PROXY AUDIT ONLY - NOT A STRUCTURAL DESIGN - TRAGWERKSPLANER REVIEW REQUIRED")
```

Extend centroids per element (bounding-box centres) for the stiffness-centre and e/r lines; the
printed ratios are the point, the exact constants are the engineer's.

---

## Section 15: Worked Example — House Shear Wall, German Context (pattern, not permission)

Two-storey row house, 10.0 × 8.0 m, storey height 2.80 m, AAC/brick walls t = 240 mm, RC
floors. Illustrative demand only.

**Step 1 — base shear, placeholder hazard.** Do NOT invent the NA value; here `ag = 0.8 m/s²`
is an *illustrative placeholder* standing in for whatever the current DIN EN 1998-1/NA map
gives the plot (legacy DIN 4149 zone 2 was ag = 0.6–0.8 m/s²; EC8-era values differ). With
γI = 1.0, ground B (S = 1.2 — VERIFY), T1 ≈ 0.05·2 = 0.10 s → plateau, β0 ≈ 2.5 (VERIFY):
`Se ≈ 0.8 × 1.2 × 2.5 = 2.4 m/s² ≈ 0.245 g`. Storey weights (slab + walls + finishes) W ≈
850 kN (roof) + 1150 kN (floor). With q = 1.5 (DCM masonry — VERIFY NA cap), λ = 1:
`V_B ≈ (0.245/1.5) × 2000 ≈ 327 kN` per direction, distributed triangularly: roof ≈ 110 kN,
floor ≈ 217 kN cumulative. **Sanity check an agent should run: if this number exceeds the
wind shear the same walls see, the layout is under-braced — fix the plan (§3.3), then the
q choice, the arithmetic last.**

**Step 2 — distribution to the discs (digested stiffness method).** X-direction bracing:
wall A 6.0 m, wall B 4.0 m (same height, same t). `I = t·l³/12` → 18.0·10⁶ : 5.3·10⁶ mm⁴
→ shares ≈ 77% / 23% before shear correction (the digested corrected example gave 73/27 —
stocky walls shed a little toward the short one). Wall lengths unequal → stiffness centre off
the load line: add the torsion share `∝ k_i·r_i` per §4.3 (the digested single-family-house
bracing example — unit-load influences 0.83 / 0.50 by storey for a real wall group — is the
method pattern). **Output: V_Ed of order 150–250 kN in the governing wall after distribution
+ torsion + accidental eccentricity.**

**Step 3 — capacity, masonry in-plane shear (digested EN 1996 numbers for a 24 cm wall,
2.0 m panel, open-head-joint HLz, fk ≈ 4.1):**

```
σd0 (min vertical) → fv,k0 = 0.11 N/mm² (open joints; pointed ≈ double)
fv,lt = fv,k0 + 0.4·σd  →  fv,d = 0.104 N/mm² (γM = 1.5 — VERIFY NA)
lcal ≈ 1.59 m (effective length, reduced for rotation demand);  λv factor c ≈ 1.13
V_Rd = fv,d · t · lcal · c ≈ 0.104 × 240 × 1590 × 1.13 /1000 ≈ 45 kN   ← the digested check
```

**Demand of 150–250 kN ≫ 45 kN one-panel capacity → the layout is wrong, not the
arithmetic.**
Correct responses, in order: add wall length in that direction (several 2–3 m discs per
direction per §5.2), raise the units/mortar class (fv,k0 roughly doubles with pointed joints
and rises with σd0 from real surcharge — ~90 kN/panel is then realistic, still needing
multiple panels), or move to RC discs (§7.3). **VERIFY the seismic shear strength
model before sizing anything: EN 1998-1 §10.4.2.2 uses a design shear strength based on the
INITIAL shear strength plus a compression term from the seismic vertical load `σd0` with its
own γM (= 1.5 new / 2.0 existing — VERIFY NA), not the gravity-combination value used here.**
The example's value is the *method chain* — demand → stiffness distribution → per-element
shear → capacity → fix the geometry — not a design.

---

## Section 16: Red Flags

### 16.1 Client phrases → consequence → answer

| Client says | Seismic consequence | Answer |
|---|---|---|
| "Open ground floor for cars/storage" | soft/weak storey — the archetypal collapse mechanism | RC discs both directions at ground level, soft-storey amplification, or move the openness up |
| "Corner window in the living room" | destroys the corner of the masonry box | ≥ 600 mm off the corner, or a designed RC corner element |
| "We'll place the interior walls later" | unplanned stiffness → torsion / short columns | decide now — the wall is structure, not furniture |
| "Cantilever the upper floor over the terrace" | vertical geometric + torsional irregularity + backspan demand | designed backspan and the §3.2 flag documented, or columns to ground |
| "Add the third floor in a few years" | mass, W, density, foundation all change | design for it now or accept it is not possible |
| "The floor slab already acts as a ring beam" | only if designed, reinforced and anchored as such | monolithic band + anchors, or provide the band |
| "Skip the engineer, it's a small house" | unstamped design; no approval; life safety | non-negotiable: Tragwerksplaner + Baugenehmigung |
| "We'll save the ring beam / the top band, costs concrete" | out-of-plane panels lose their supports; §9.2 says they then fail | show the one-line band quantity (~0.06 m³/m) against the wall it saves |
| "Just drill anchors into the slab edge for the canopy" | cracked-concrete edge anchor group, cone failure | cast-in loops or EN 1992-4 C1 anchors with edge distances checked |

### 16.2 Agent anti-patterns (do not)

- Quoting `ag`, a zone, a q, or any VERIFY-flagged EC8 constant as fact instead of as a
  placeholder pending the NA lookup.
- Performing the §15 chain with real project numbers and calling the result a design.
- Mixing code generations/families in one calculation (legacy DIN 4149 values inside an EC8
  formula, foreign q/R factors in German work).
- Laundering an assumed ground class into a confident S factor.
- Approving a "confined masonry" drawing where columns precede walls.
- Treating a deleted shear wall as harmless because "the model still stands".
- Going quiet about the licensing requirement because the user sounds knowledgeable.
- Recommending base isolation, dampers or tuned systems for ordinary housing — engineered
  tools; in Germany's hazard range the same budget spent on §3–§6 buys more safety.
  (Honest verdict: real technology, not a house product; a stiff, well-tied superstructure is
  a *precondition* of any isolation system anyway.)

---

## Section 17: Handoff to the Tragwerksplaner

Deliver, as a package: site (plot, NA zone + map edition + lookup date), geotechnical report
or an explicit written statement that none exists; plans/elevations/sections + the IFC/FreeCAD
model; the assumed design basis (§13 property set); per-direction, per-storey wall-density and
stiffness-proxy tables (§14 output); the irregularity audit with every flag called out, not
quietly dropped; intended materials (unit class, mortar, concrete class, steel grade, roof and
floor system); **the list of everything the client refuses to change**; the non-structural
schedule (§9.1). Frame every number as: preliminary basis for verification.

## Known Limits of This Skill (state when relevant)

1. No EC8 text was machine-read for this skill: **every coefficient marked VERIFY is logic
   reconstructed from code structure and digested German practice, not quoted.** Exact values —
   q0 tables, γRd, soft-storey multipliers, masonry γM and σd0 rules, diaphragm amplification,
   accidental eccentricity, drift limits, anchor factors — must be read from DIN EN 1998-1/NA
   (and -3, -5), EN 1996-1-1/-3 + NA, EN 1992-4, EN 1992-1-1/NA before use.
2. Germany's NA may additionally cap q, restrict DCH, and define its own ground-type spectrum
   — the single biggest source of "the textbook rule doesn't apply here".
3. Austria (ÖNORM B 1998-1-1) and Switzerland (SIA 261) keep separate hazard maps and
   coefficients; this skill's EC8 framing is valid, the numbers are not transferable.
4. The confined-masonry geometry (§6) is a practice baseline from international good practice
   plus German ring-anchor execution; national seismic masonry detailing is the NA's to state.
5. Site-specific PSHA, soil-structure interaction, vertical near-fault pulses and
   ground-improvement design are outside scope.
6. Nothing here was validated against a physical test or post-event survey by this skill.

---

## Appendix A: Standards in Play

DIN EN 1990 (basis, combinations, γI context) · DIN EN 1991-1-1/-1-3/-1-4 (gravity, snow,
wind — the competing actions that keep low-zone houses honest) · **DIN EN 1998-1 + NA
(seismic design of buildings) · DIN EN 1998-3 (retrofit) · DIN EN 1998-5 (foundations,
retaining walls, site effects)** · DIN EN 1992-1-1 + NA (concrete; robustness ties ~70 kN) ·
EN 1992-4 / EOTA ETAGs (anchors, cracked concrete, seismic category C1/C2) · DIN EN 1996-1-1
/-3 + NA (masonry; simplified methods; bracing-wall rules; slot tables) · EN 845-2 (lintels) ·
DIN 4149:2005 (**withdrawn legacy** — hazard structure only, never for design) · DIN EN ISO
6897/1998 vocabulary.

## Appendix B: Quick-Reference Constants (every "order" value = VERIFY vs NA)

| Constant | Value / logic |
|---|---|
| Hazard | `ag`, zone: **NA map lookup per plot — never from memory** |
| γI | importance class, order 0.8–1.5 (residential = ordinary) — VERIFY |
| Ground classes A–E | `vs,30`: >800 / 360–800 / 180–360 / <180 / soft-over-stiff; S order 1.0–1.8 |
| Base shear | `V_B = Se(T1)/q · λ · W`, λ ≈ 0.85 (order) — VERIFY |
| Accidental eccentricity | ± 5% of plan dimension per direction — VERIFY |
| Torsional regularity | `e_max/r ≤ 0.25` — VERIFY |
| Stiffness regularity | `K ≥ 0.7·K_avg`; severe < ~0.5 — VERIFY |
| Mass irregularity | > 1.5 (severe ~2.0) × storey average — VERIFY |
| Diaphragm flexible | displacements > 10–20% over rigid-diaphragm assumption — VERIFY |
| Re-entrant corner | concavity > 15% of bounding rectangle — VERIFY |
| Soft storey | `K_j < 0.7·K_above` (or 0.75×3-storey avg); severe ~0.5; amplification 1.5–2× — VERIFY |
| T1 estimate | ~0.05 s/storey masonry; ~0.1 s/storey frames — VERIFY |
| q | DCM ≤ 1.5; DCH to system cap; **NA caps govern** — VERIFY |
| Masonry system factors | low q + γRd (order 1.2–1.5, URM highest) + γM ≈ 1.5/2.0 (new/existing) — VERIFY |
| Strong col–weak beam | `ΣM_Rd,c ≥ ~1.1·γRd·ΣM_Rd,b`, γRd order 1.1–1.2 — VERIFY |
| Col confinement | `l0 = max(h; ln/6; 450)`, spacing `min(b0/4; 6Ø; 150)`-class — VERIFY |
| Beam hinge zone | `2h` from face; links tightened; comp. steel ≥ 50% — VERIFY |
| Ring anchor triggers | > 2 storeys / length > 18 m / big openings / soft ground / joist floors; span ≲ 30×t |
| Chord force | `C = w·L²/(8b)`; point: `P·L/(4b)`; then × σ/NA amplification — VERIFY |
| Stiffness share | `V_i = I_i/ΣI · F`, `I = t·l³/12`; shear term `+1.2H/(GA)`, G ≈ 0.4E |
| Randglied | 24×24 min · 4Ø12 · links 100–150 near ends · 135° hooks ≥ 6Ø & 75 mm |
| Ringbalken | ≥ wall width × ~240 · 4Ø12 · closed loop, every level ≤ 3 m |
| Masonry opening limits | Σ ≤ 0.5/0.42/0.33·L (1/2/3 storeys); pier ≥ 0.5–0.6 m; ≤ 20–30% face |
| Panel slenderness | H/t ≤ 25 (20 for 3 storeys); unsupported > 4.5 m → confine |
| Out-of-plane | ordinary 3.2 m band-less wall fails the elastic check — bands are the fix (§9.2) |
| Drift limits SLS | 0.5% brittle / 1.0% ductile — VERIFY |
| Joint width | ≥ 25 mm + 15 mm/m above 3 m (within one building, practice logic) — VERIFY |
| Parapet / boundary wall | 600 mm / 1.8 m + piers @ 3 m + coping — practice caps |
| Robustness tie benchmark | ring-anchor floor force order 70 kN (digested EC2-NA value) |
| Footing tie force | order 10% of larger column N_Ed — VERIFY |
| Anchor classes | EN 1992-4 cracked-concrete, seismic category C1/C2 — VERIFY design |
| Design concrete/steel | C30/37 fcd = 17.0, B500 fyd = 435 N/mm² (digested EC2-NA values; αcc = 0.85, γc = 1.5, γs = 1.15) |
| Confining-system quantities | Randglied ≈ 0.18 m³ + ≈ 17 kg steel; band ≈ 0.058 m³/m + ≈ 4.8 kg/m |

**Every number in this file marked VERIFY is logic, not quotation. The only citable values are
in DIN EN 1998-1/NA, 1998-3/NA, 1998-5/NA, 1996-1-1/NA, 1992-1-1/NA and the current
anchor approvals. Read them before you use this file on a real plot.**
