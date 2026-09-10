---
name: sustainable-construction
description: >
  Lifecycle-based design and evaluation of buildings for DACH practice
  (Nachhaltiges Bauen): life-cycle thinking with Ökobilanz module model
  (A1–A3 manufacture, A4–A7 construction/installation, B1–B7 use, C1–C4
  end-of-life, D benefits beyond boundary) per DIN EN 15978 / 15804+A2, EPDs
  and generic national/building-epic database data sources, recyclate-content
  and material-passport evidence; embodied-carbon factors per material with
  numeric ranges and a comparison table (concrete ~200 kg CO2e/m³ with
  low-carbon market variants, cement clinker factor ~0.67 and ~530 kg CO2/t,
  SCM substitution potentials, steel/EAF vs BF, brick 94–227 kg/m³ by type,
  timber with biogenic storage −712…−565 kg CO2e/m³ A1–A3, ~1 t CO2 stored per
  m³, recarbonisation caveats); operational energy duties (GEG/GModG reference
  building Qp ≤ 0.55, envelope ladder, heat demand by stock age, efficiency
  house ladder, heat-pump + PV + battery sizing logic, district heat and
  primary-energy factors), CO2 emission factors and pricing/shadow prices
  (45 €/t BEHG, UBA ~250 €/t, 809 €/t intergenerational); resource and land
  rules (sealing, ≥90 % C&D recovery for taxonomy-alignment, ≥70 % KrWG quota,
  recycled-aggregate types and RC-concrete limits, secondary raw materials,
  component reuse < 1 % reality); circularity by design (Design for
  Disassembly, bolted/reversible connections, sortenrein separation, material
  passports and resource pass); indoor environment and health (formaldehyde
  0.06 mg/m³, carcinogenic-VOC 0.001 mg/m³, SVHC 0.1 %, radon ⚠ VERIFY,
  mould-moisture coupling, legionella, CO2/Pettenkofer); comfort (summer heat
  protection, thermal mass/core activation 25–30 W/m², daylight ≥ 1/8 NRF,
  acoustics pointers); DGNB/BNB/QNG/LEED/BREEAM orientation as quality tool
  (criteria families, not marketing); life-cycle costs (operation > 80 % of
  spend, maintenance intervals, repair economy, Modernisierungspflichten and
  Sanierung-vs-Neubau logic, static/dynamic comparison methods); a
  trade-off resolution method (structure vs physics vs carbon vs cost with
  mandatory disclosure) and decision-wise strategy matrices; a per-m²BGF
  carbon-accounting quick template with honest uncertainty flags; common
  greenwashing pitfalls; and phase-wise checklists. Every number carries a
  tier (T1–T4) and time-sensitive values are flagged ⚠ VERIFY.
---

# Sustainable Construction (Nachhaltiges Bauen) — DACH Lifecycle Design

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

Use this skill whenever the agent must judge or shape a design decision against sustainability: material substitution ("wood instead of concrete?"), insulation choice, heating-system choice, envelope standard, embodied-carbon estimates per m²BGF, certification orientation (DGNB/BNB/QNG), reuse/recycling questions, indoor-air and comfort limits, life-cycle cost comparisons, retrofit-vs-demolition verdicts, or customer claims that smell like greenwashing ("climate-neutral house", "CO₂-free concrete"). It is the cross-domain trade-off layer: it does not replace the structural, physics, services, or cost skills — it arbitrates between them and forces the reasoning to be disclosed.

Sibling skills (call them, do not duplicate their scope):
- building-physics-thermal-moisture — U/R/Ψ proofs, Glaser, summer heat index, n50.
- building-services-tga — heat load, HP/boiler/PV/RLT sizing detail, plant rooms, GEG/GModG component duties.
- building-acoustics — DIN 4109/VDI 4100 mass and flanking proofs.
- structural-systems, concrete-detailing, timber-steel-design, masonry-construction — load-bearing decisions.
- building-materials — product-level properties λ/μ/ρ/fc.
- cost-management-din276 — cost groups, estimates, rates.
- fire-protection-building — GK classes, reaction classes, MVV TB constraints.
- roofing-waterproofing, openings-windows-doors, construction-detailing — layer durability and joint rules.
- building-regulations-permits — BauGB/LBO/MBO framing, permits.

Units convention: GWP in kg CO₂e (CO₂-equivalents, GWP100); material GWP density
kg CO₂e/m³ and per mass kg CO₂e/t; building indicators kg CO₂e/m²BGF (DIN 277
gross floor area) or per net usable area; energy kWh/(m²·a); emission factors
g CO₂e/kWh; prices €/t CO₂e. German terms in parentheses at first use. All
numbers carry a tier tag (section 2); edition- and price-dependent numbers carry
⚠ VERIFY — treat them as planning-grade until re-read against current sources.

## 0. How to use this skill

1. Identify which lifecycle question is actually asked: sufficiency (should this
   exist?), embodied carbon, operational energy, resources/waste, health/comfort,
   cost over time, or certification. Route each to the relevant section.
2. Decide before computing: state the system boundary (modules), the reference
   period (DE: 50 a comparison frame, ⚠ ≠ real lifetime), the functional area
   (BGF/NRF/NGF), and the data tier. Never mix tiers in one number chain.
3. Apply the sufficiency-first order of intervention (section 12.2): program
   reduction → compact form → structure choice → envelope → systems → PV/renewables
   → offsets/credits last.
4. Every recommendation must disclose the trade-off it pays for. A timber wall
   that gives up fire/acoustic mass, a compact block that gives up units, a thick
   mineral insulation that gives up floor area — say so explicitly (section 12.4).
5. Where the digested knowledge is silent (explicit gaps below), say "not in
   knowledge base" instead of inventing: per-version DGNB criterion weights, exact
   U-value annexes beyond flagged ranges, current subsidy rates, radon guidance
   specifics, per-product EPD values.

Explicit gaps of the underlying digests — do not fabricate around them:
- DGNB criteria weights/point tables per version (only families and levels known).
- Heat-demand tables by construction-age band (only stock trajectory + HP-suitability by age exist).
- Passivhaus component values beyond the ≤15 kWh/(m²a), n50 ≤ 0.6 anchors.
- Full current GEG/GModG annex values (flag edition!).
- Recycled-content certificate scheme mechanics (referenced generically only).

## 1. Reality check — what this skill can and cannot deliver

1. Sustainability assessments produced here are **planning aids** (Ökobilanz-vorlagen,
   Variantenvergleiche, Kennwert-Schätzungen), not certificates, not an eLCA/Level(s)
   submission, not a QNG proof. A formal building LCA must run in an accepted tool on
   EPD/database data with an accountable practitioner; a certificate requires an
   accredited body and auditor.
2. Regulation is moving fast: EPBD recast (published 2024, national transposition due
   ~2 years), GEG→GModG renaming, CO₂ pricing ladder, subsidy programmes re-cut
   quarterly. Everything money- and law-related here is a snapshot ⚠ VERIFY against
   the text in force at project date.
3. A "sustainable" verdict is always multi-criteria. If the agent optimises the one
   metric it can compute best (usually kg CO₂e), it is wrong by construction. Section 12
   prescribes the disclosure discipline.
4. Embodied-carbon claims on products ("CO₂-neutral") are valid only for module A1–A3
   unless the declaration states otherwise; biogenic storage can flip positive at
   end-of-life. Treat all single-number product claims with the pitfall list (section 15).
5. Long service life is the strongest single lever ("lange Nutzungsdauer = beste
   Bilanz"). Bestandserhalt/Umnutzung before Neubau is the default rule; demolition
   must overcome that presumption with data (LCC+LCA), not taste.

## 2. Evidentiary tiers (never mix tiers in one number chain)

| Tier | Status | Examples (this skill) |
|------|--------|------------------------|
| T1 | Law / binding duties | GEG reference-building duties, KrWG Art. 14(2) ≥70 % quota, EU taxonomy thresholds (≥90 %/≥70 %, SVHC/VOC limits as contract-relevant), EPBD dates once transposed, MindBauRL/MVV TB fire ceilings on insulation, BauGB §9 levers |
| T2 | Standards & calculation models | DIN EN 15978/15643, EN 15804+A2 modules, ISO 14040/44, ISO 20887 (DfD), DIN 18940 (clay), DIN EN 197-1/-5 cements, DAfStb RC rules, DIN 4226-101, DIN EN 16757 (recarbonisation), GEG/DIN V 18599 method |
| T3 | Recognised practice / branch data | industry EPDs and branch averages, national public building-ecology database, public lifecycle-calc tool for federal buildings (Bauteilkatalog), LESS steel label, DGNB-adjacent indices (UMI, ZI, PCDS/ISO 59040, DIN SPEC 91484), component service-life tables |
| T4 | Rules of thumb (plausibility only) | "1 m³ wood ≈ 1 t CO₂ stored", "~200 kg CO₂e/m³ concrete", quick per-m²BGF carbon template (section 14), "operation ≈ 80 %+ of LCC", "retention beats replacement in most residential retrofits" |

A T4 factor may start a conversation; it never closes a T1 duty or an offer with a
CO₂ ceiling clause (section 11.5). If only T4 exists, say so in the output.

## 3. Lifecycle thinking: the framework

### 3.1 Where the number 2045 comes from and what buildings must do

- Germany: climate neutrality 2045 (constitutional rank, KSG ladder: −65 % GHG by 2030,
  −88 % by 2040, both vs 1990 ⚠ VERIFY current KSG target revision). EU: −55 % by 2030,
  climate-neutral buildings stock 2050 (EPBD trajectory).
- Buildings contribute ≈ 40 % of German GHG across operation + building products; the
  construction sector consumes ≈ 90 % of mineral raw materials and generates ≈ 55 % of
  national waste (DE); EU framing: ~50 % of raw materials, >35 % of waste, building-material
  GHG ≈ 5–12 % of national emissions with up to 80 % of that addressable by material
  efficiency (T3, order-of-magnitude).
- Currently the use phase is still ~⅔ of building GHG; as the grid decarbonises,
  **embodied carbon moves to the dominant share** — that is why early structural
  decisions now matter more than the last centimetre of insulation.
- 80–90 % of the buildings in use in 2045 already exist today. Renovation rate must at
  least double from ~0.7–1 %/a to ≥2 %/a ⚠ VERIFY (policy target drift).

### 3.2 The three-pair principle set

Three-pillar model (Ökologie, Soziales, Ökonomie, equal weight — Carlowitz 1713 lineage;
"Nachhaltigkeit 4.0" adds economics-ethics + technology). Operationalised for construction
as four implementation principles — use these four verbs in every recommendation:

- **Suffizienz** (demand avoidance): smaller program, compact form, shared use, no
  over-technologising. "Die Aufgabe hinterfragen."
- **Effizienz** (less impact per unit): better U, better JAZ, less clinker, less steel.
- **Konsistenz** (different, compatible systems): renewables instead of fossil,
  recyclable/bio-based materials, separable constructions.
- **Resilienz** (robust under changed conditions): adaptability, low-tech redundancy,
  heat/flood/price-shock tolerance, simple operable systems.

Low-Trend principle (digest): minimise technical complexity — a reduced-complexity
building is more resilient AND more operable under trade-labour scarcity; use physical
effects (mass, orientation, buoyancy, shading) before machines. "Schlechte Konstruktion
heilt keine Technik." Passive → semi-passive → active is also the mandated TGA ordering
(section 6.5).

### 3.3 Cycle times and the phase-0 lever

| Layer | Typical cycle / service life | Design consequence |
|-------|------------------------------|--------------------|
| Structure (Tragkonstruktion) | >50 a, often several × 50 (brick ~150 a stated technical life; concrete facades >50 a) | decide for the century: material + durability + reserve |
| Envelope/Hülle | 40–60 a (WDVS 40–60, windows 40–50, seals/screws plan-mässig only 25 ⚠ → 2 cycles over 50 a, doubling A+B impacts) | specify ≥50 a for fast-cycling parts or make them exchangeable |
| Services (TGA) | ~30 a (boiler ~20–25, HP ~15–20, chillers 20–25, pumps ~12 ⚠ VERIFY table collapsed in source) | accessibility, simple interfaces, upgrade routes |
| Fit-out/Inneneinbau | 1–5 a short / 5–30 a medium cycles | separability from structure |
| Planning horizon | conventional assessment 50 a (DE comparison frame; CH 60 a) | all LCA/LCC windows here unless told |

Phase 0 (Projektentwicklung, before HOAI LPH 1) is the key phase: the client's five
strategies (climate/financing, planning/procurement, use/operation, maintenance,
recovery/re-use) and the quantified target (e.g. kg CO₂e/(m²·NRF·a) over life, energy
standard, certification level) get fixed here. **Design freeze** from Projektstufe 2
(AHO Heft 9); later changes are a process loop, not an edit. Influenceability is
highest at the start and the cost of change rises steeply — sustainability consulting
that arrives in detail-design stage cannot move the structure, only the finishes.

### 3.4 The pricing frame (why carbon numbers matter commercially now)

- National CO₂ price on heating fuels: 45 €/t CO₂e since Jan 2024, ladder toward
  55–60+/€t by 2027 then market band ⚠ VERIFY current price path.
- Shadow prices for planning/procurement (Umweltbundesamt line): ~237 €/t CO₂e
  (purchasing power 2022) — mandatory hypothetically in Baden-Württemberg LCA (KlimaG
  since 6/2023: 250 €/t binding for state projects); UBA 2023 update: 250 €/t at 1 %
  time-preference rate, 860 €/t at 0 %; intergenerationally equal-weighted: 809 €/t (2022).
  Procurement practice elsewhere: Norway 450 €/t in bid evaluation; UBA suggested
  300 €/t for 2024-emissions (T3, ⚠ VERIFY currency).
- Consequence for LCC and bidding: run every variant twice — with and without a
  shadow price (section 11.4) — and disclose which one "wins".
- Investor/regulator pressure stack (recognition level): CSRD (double materiality,
  >250 employees/€25 M/€50 M thresholds, reporting from FY 2024), EU taxonomy (6
  objectives, DNSH, technical screening for buildings), SFDR Art. 6/8/9 fund classes,
  CRREM pathways per asset class → **stranded-asset date**, SBTi, MaBank: poor energy
  efficiency → higher capital cost. A design that cannot be described in these data
  fields loses financeability (section 10).

### 3.5 Regulatorik timeline that drives design choices (⚠ VERIFY dates as enacted)

- EPBD recast (2024): Nullemissionsgebäude = new-build standard for public buildings
  from 2028, all new builds from 1 Jan 2030; mandatory lifecycle-GWP target values +
  display in energy certificates for new builds (calculation duty from 1.1.2028 for
  new non-residential/large >1000 m², from 1.1.2030 all new builds); minimum energy
  performance (MEPS) step-downs for existing non-residential; renovation roadmaps;
  solar-use duty new + existing (staged, where feasible); no fossil-fuel generation
  at site on pathway; inspection duty HVAC >70 kW; metering of IAQ.
- GEG/GModG: reference-building method persists (section 6.1); heating technology
  openness §§ 71b–71h (grid connection, HP, direct electric gates, solar thermal,
  biomass, hydrogen), communal heat planning (Wärmeplanungsgesetz in force 1.1.2024)
  changes what the local network may require of the plot.
- NKWS (national circular-economy strategy, cabinet 12/2024): digital
  Gebäuderessourcenpass intended mandatory; regionality and secondary-material
  preference via procurement guidelines; durability/sanability/schadstoffarm by decree.
- BauPVO/CPR reform direction: environmental product classes, recyclate share and
  dismantlability information duties; reuse-before-recycling ordering on product level;
  digital building logbooks. Plan documentation to survive that shift.

Regulatory-economics layer (screening values, lease/tariff/stranding mechanics;
T1 values ⚠ VERIFY against delegated acts and the text in force at project date):

- **EU-taxonomy screening (buildings, T1)**: new-build substantial contribution to
  climate mitigation is gated by a **non-renewable primary-energy ceiling of
  ≈ 36.9 kWh/(m²·a)** (biggest known gap: no certification system examined meets the
  taxonomy in full; the German holistic system comes closest at 11 of 13 categories
  ⚠ VERIFY per current delegated regulation 2021/2139 / 2023/2486); besides that:
  mandatory EPC; >5,000 m² → airtightness test + thermography + whole-life-GHG
  disclosure; climate-risk and vulnerability analysis; site-contamination test;
  construction-phase emission reduction; no building on ecologically valuable land;
  circularity gate **≥ 90 Gew.-%** C&D-waste reuse/recycling (substantial
  contribution) with **≥ 70 Gew.-% DNSH** (excl. naturally occurring, waste key
  17 05 04) — binding quotas restated in 7.2; a planned **≥ 50 % recycled-or-renewable
  materials** benchmark for future builds ⚠ VERIFY status.
- **Green lease / ESG lease (T1 contract layer)**: sector guideline current 02/2024 ⚠
  dated; a *real* green lease requires concrete, verifiable, sanctionable obligations
  in all **four base areas** — (1) consumption-data exchange, (2) sustainable energy
  sources, (3) reduce consumption and waste, (4) environmentally friendly construction
  works — best-effort-only clauses are fake leases (and AGB risk); extended set:
  green-modernisation acceptance, energy monitoring, CO₂ accounting,
  certification-protective clauses, mobility, environmental levies, training, PV;
  incentives > sanctions (savings sharing, contests); commercial tenancy flexibility
  makes it workable, residential less so; ESG lease adds CSRD-driven S+G clauses
  (diversity, fair work, anti-corruption, audits, board competence); France has a
  statutory environmental annex for commercial leases since 2013 ⚠ VERIFY article.
- **Mieterstrom and building supply (T1, dated rates)**: §42a EnWG tenant electricity —
  supply inside building/ancillary rooms without grid passage, **Vollversorgungsgebot**
  (residual-power partner or storage required), tariff legally **≥ 10 % below the
  local basic-supplier price** (cf. 6.4), rent cap §42a(4) for residential; the
  Mieterstrom subsidy was extended to commercial use 05/2024 (excluded for affiliated
  companies) and is set by the regulator per commissioning date and size —
  **≤ 1,000 kWp commissioned Jan 2024–Jan 2025: 1.64 ct/kWh ⚠ VERIFY current band**;
  §42b communal building supply (new since 05/2024): same conditions minus the
  full-supply duty (most supplier obligations suspended) — needs a **15-min metering**
  concept with uniform allocation key agreed with the electrical planner; plug-in
  balcony PV per §3 Nr. 43 EEG is the small-sensitisation variant.
- **CRREM stranding clock (T3 tool, T1-adjacent financial consequence)**:
  country/building-type CO₂ and energy baselines with 1.5/2 °C-aligned reduction
  pathways per asset class; an asset above its pathway is a **stranded asset** — still
  usable but costs exceed returns (write-downs, discounted sale/refinancing, MaRisk
  capital hit via the §3.4 stack); required inputs: address, use, net floor area excl.
  parking, vacancy, actual electricity, other carriers, refrigerant losses, on-site
  renewables, district-heat emission factor — low effort from a maintained document
  system; use it in purchase due-diligence and in the Modernisierungsfahrplan (11.4);
  worked case: do-nothing timeline stranded the asset in 2026, stepped retrofits A+B
  deferred stranding to 2036; 1.5 °C-alignment certificates for existing offices exist
  as market products ⚠ VERIFY method acceptance.

## 4. The LCA system model and the data sources (Ökobilanz, EPDs)

### 4.1 Module model (DIN EN 15978 phases; EN 15804+A2 product modules)

| Module | Content | Practice note |
|--------|---------|---------------|
| A1–A3 | Rohstoffe, Transport, Herstellung (production of products incl. upstream) | "embodied carbon" headline; raw-material extraction included |
| A4–A5 | Transport to site, Einbau/Errichtung (incl. loss/waste on site, site energy) | public federal building-lifecycle tool maps A4 via national ecology dataset |
| B1 | Nutzerbedingter Treibhausgasausstoß (occupant transport etc. — informative in many scopes) | keep out unless scope says |
| B2–B4, B6 | Instandhaltung, Reparatur, Austausch (B4!), Betriebenergie (B6) | B4 exchange cycles are where 25-a seals double the score; B6 dominates legacy scores |
| B5, B7 | Instandsetzung, water use | |
| C1–C4 | Rückbau/Abbruch, Transport, Abfallbehandlung (sorting), Beseitigung (landfill/incineration) | C3/C4 are the "honesty modules": wood can turn positive here; design decisions echo |
| D | Wieder Verwertungsgewinne/Lasten beyond boundary (credits/substituted grid heat etc.) | informational; never let D pay for a bad A–C design; system-boundary choice is critical for CCS/carbonation credit claims |
| Reference period | DE comparison 50 a; functional unit e.g. per m²BGF or m²NRF·a | |

Planning practice: two sub-balances — building level (embodied, A1–A5+C/D) and
operation (B6) — iterated **planungsbegleitend**, generic data first, product-specific
later; identify hotspots early (structure, façade, windows, concrete core activation,
insulation thickness trade grey-vs-operational: check the saved B6 against added A1–A3;
for nawaRo insulation the grey-energy case is usually fine, for thick XPS/WDRS it can
turn).

### 4.2 Data sources (generic naming)

- Product level: **EPDs** (Umweltproduktdeklarationen) per DIN EN 15804+A2 on ISO
  14040/44; industry association EPDs and manufacturer EPDs; declared indicators
  include GWP (fossil/biogenic/fossil-lump split), acidification etc. Verify module
  coverage, data age, and whether biogenic carbon is included before comparing numbers.
- Generic level: national public building-ecology dataset (Ökobau.dat lineage),
  platform industry-EPD collections (IBU-type), public-component catalogue of the
  federal lifecycle-calculation web tool (eLCA successor) — modules A1–A3, A4, B6,
  C3/C4, D; **new-build only**: for existing buildings, retained stock = neutral (0),
  only newly inserted materials are charged. That convention is itself the strongest
  formal argument for Bestandserhalt.
- Recyclate-content proofs: recycled-content declarations per product (EPD statement
  of secondary input share); third-party recyclate certificates exist per material
  stream (recognition level ⚠ scheme mechanics not in knowledge base).
- Building level: Gebäuderessourcenpass / material registry exports; circularity
  indices UMI (resource/energy intensity incl. deconstruction cost), DGNB
  Zirkularitätsindex, material-value registries (residual value tracking), CPX-style
  circularity metrics; Pre-Demolition-Audit per DIN SPEC 91484.
- AI/generative variant studies (section 12.6) read from these same datasets;
  keep the source tier visible in every generated comparison.

### 4.3 Benchmark sanity bands (T4, order-of-magnitude, ±50 %)

- New concrete/brick residential 4–5 storeys: A1–A3 typically several hundred
  kg CO₂e/m²BGF (low 200s–400s); timber/hybrid 30–50 % lower; up to ~90–99 % lower
  mid-rise office embodied vs steel-concrete in studies depending on EoL scenario
  (biogenic storage accounting drives the spread — always ask which convention).
- Office operation ≈ 75 % of whole-life GHG (BBSR 2020 line); residential use phase
  ≈ 60 % — both falling as grids decarbonise; embodied share rising.
- QNG/KfW-type funding gates express a lifecycle THG target in kg CO₂e/(m²·a) over
  50 a including operation — check the current class table in the program guidelines
  (⚠ VERIFY rates change per funding period).

## 5. Embodied carbon per material (Graue Energie, with ranges)

### 5.1 The comparison table (T3 branch/EPD averages, planning grade; ⚠ VERIFY with product EPD when specifying)

| Material (per m³ unless noted) | GWP A1–A3 kg CO₂e/m³ | λ W/(mK) | ρ kg/m³ | Strength | Storage? | Notes |
|---|---|---|---|---|---|---|
| Concrete C25/30 (normal HC mix) | ~178–200 (industry ref); market low-carbon ~130 | 1.15–1.65 | 2000–2600 | high | recarb. only | 90–95 % of mix GWP is cement; CSC classes to −60 % (5.3) |
| Unreinforced/lean concrete | 60–80 | — | — | comp. only | — | −~30 % vs RC wall; −50 €/m² wall |
| Reinforcement steel (per t) | ~700 (BF route); ~300 (EAF DE market) | — | 7800 | — | — | 100 kg/m³ RC ≈ 70 kg CO₂e/m³ |
| Steel section EAF (per t, A1–A3) | ~300–700 by scrap/power mix | — | 7850 | — | — | LESS label classes A–E; BF route higher |
| Kalksandstein (silico-calcareous) | 226.8 | 0.5–1.8 | 1010–3600 | 5–75 N/mm² | — | mass/acoustics champion per kg |
| Brick, unfilled masonry | 113 | 0.075–0.96 | 550–2000 | 4–28 | — | fired 850–1000 °C; life ~150 a; >90 % EoL recovery |
| Brick, insulation-filled | 146 | 0.06–0.12 | 550–900 | 6–18 | — | filling mixes materials → separation penalty |
| Porenbeton (AAC) | 166 | 0.07–0.18 | 250–800 | 1.6–10 | — | monolithic, low mass → acoustics/fire caveats |
| Clay brick (unfired, DIN 18945) | 94 (technical drying ~100; dry-dried NEGATIVE) | 0.17–1.4 | 600–2200 | FK 2–5 | none/low | 100 % recyclable, unlimited re-use; water/frost sensitive |
| KVH / timber structural | −712 | 0.12–0.18 | 350–550 | — | ~0.5–1 t CO₂/m³ | becomes positive only via C3/C4 incineration scenario |
| BSH (glulam) | ≈ −650 | ~0.13–0.18 | ~500 | — | yes | more processing (drying/gluing) = more fossil GWP |
| CLT (Brettsperrholz) | ≈ −632 | ~0.13 | ~500 | — | yes | adhesives + fire/acoustic add-ons count too |
| OSB / MDF | −565 / −676 | 0.09–0.14 | 300–900 | — | partial | resin content: health + EoL flags |
| Multilayer parquet (per m³) | +50 | — | — | — | net small | processing-heavy biogenic ≈ neutral |
| Hemp-lime block | ≈ −130 (sink in use) | 0.06–0.1 | 200–400 | 0.1–2 N/mm² (nb) | yes | uptake 70–240 kg/m³ vs ~50 process |
| Glass (float, per t) | energy 12.6 GJ/t; ~1.5–2.5 (⚠ not cleanly in digests) | 1.0 | 2500 | — | — | 75 % furnace gas / 25 % process CO₂; only cullet cuts process share |
| Aluminium primary vs secondary | secondary ≈ 5 % of primary energy | — | 2700 | — | — | 75 % recyclate price-neutral for profiles |
| Natural stone (granite etc.) | low (no thermal process), site-dependent | 2.3–3.5 | 2600–2800 | up to 120 MPa C | — | century lifetimes; transport dominates |

Order-of-magnitude takeaway: **same U-value, very different walls** — RC+EPS vs AAC at equal U can differ by a factor of several in A1–A3; U alone says nothing about sustainability (digest example: Porenbeton wall ≪ Stahlbeton+Dämmung in GWP; note a counter-example exists where aerated concrete scores ~2× the GWP of a RC+EPS composite depending on thickness — compute both metrics, never rank on one).

### 5.2 Cement and the clinker lever (where the biggest single number lives)

- Clinker production: ~0.78–0.83 t CO₂/t clinker implied by ~530 kg CO₂e/t cement at
  average DE clinker factor ≈ 0.67 (2024); process (calcination of limestone) ≈ 60 %
  (40 % combustion fuels; other rendering: ~⅔ process / ~⅓ energy — same order).
- German cement ≈ 18 Mt CO₂e (2022) ≈ 2.5 % national; ~8 % of global cement CO₂ is
  made in DE-market terms (T4 framing).
- Alternative fuels already ≈ 69 % of clinker thermal energy (2024); residual
  combustion emissions allocated to the waste-emitting system per EN 15804.
- Clinker-substitution ladder (DIN EN 197-1 + 197-5):
  - CEM II/A-B (6–35 % SCM: slag S, fly ash V, pozzolan P/Q/T, silica D, limestone L/LL).
  - CEM III/A-B-C (slag 36–95 %; B ≈ 20–34 % clinker).
  - CEM II/C-M (clinker 50–64 %) and CEM VI (35–49 %) per EN 197-5 — in DE need
    abZ/Ü-Zeichen (not yet harmonised) ⚠ VERIFY availability at plant level.
  - "CEM X"/LC3-type lines (limestone + calcined clay) = the research direction;
    availability of good clays and the thermal activation are the constraint.
- SCM ceilings: fly ash ≤ 35 % of cement mass (EN 450); slag in CEM III ≤ 80 %;
  silica fume credit ≤ 11 % (reinforcement protection, DIN EN 206); k-value crediting
  (w/z)eq = w/(z + k·h) with k = 0.4 (slag, national), 0.4 fly ash, 1.0 silica fume
  (T2 werkstoffe digest).
- Scarcity flags: fly ash shrinks with coal phase-out; slag shrinks with H₂-based
  ironmaking → calcined clays/limestone + more primary clinker may be forced; lock
  low-carbon cement by performance specification, not by type name alone.
- Durability trade: low-clinker cements (CEM III/B, LC3-types) give up Ca(OH)₂
  reserve → carbonation advances, cover/curing quality matters MORE. Execution and
  aftercare are part of the carbon case (digest: "klinkerarm ↔ geringere
  Dauerhaftigkeit → Ausführungsqualität hochhalten").

### 5.3 Concrete procurement instruments (T3)

- **Cement-Carbon-Class (CCC) / CSC CO₂ module** — max net GWP kg CO₂e/m³ by class
  (industriean Referenz / EPD-Ø / L1 −30 % / L2 −40 % / L3 −50 % / L4 −60 %):

| Class | C20/25 | C25/30 | C30/37 | C35/40 | C45/55 | C50/60 |
|---|---|---|---|---|---|---|
| Reference | 213 | 237 | 261 | 286 | 312 | 325 |
| EPD average | 157 | 181 | 196 | 220 | 273 | 275 |
| L1 | 149 | 166 | 183 | 200 | 218 | 228 |
| L2 | 128 | 142 | 157 | 172 | 187 | 195 |
| L3 | 107 | 119 | 131 | 143 | 156 | 163 |
| L4 | 85 | 95 | 104 | 114 | 125 | 130 |

  (⚠ VERIFY against the current class table when tendering; tender L2/L3, accept and
  **verify the actual cement delivered** — überwachung includes "the specified
  low-carbon cement was placed".)
- Unreinforced/reduced-steel measures with big GWP leverage: unreinforced strip/
  individual footings (up to −80 % footing GWP), unreinforced ground slabs with
  dummy joints (−100–250 kg steel/m³ = −70–170 kg CO₂e/m³), skip garage-floor
  coating (−30 kg CO₂e/m²), 25-cm unreinforced C25/30 wall: N_Rd ~1800 vs 2400 kN/m
  — check before reflex-reinforcing.
- Hollow-core/prefab decks −40 % concrete / −75 % steel; sandwich decks −40 %
  mass; in-situ voided slabs −35 % concrete; infraleichtbeton < 800 kg/m³ for
  load-bearing walls without added insulation (ZiE route — not under EN 1992);
  carbon/glass-fibre reinforcement: −50 % material, −30 % CO₂ potential, fire and
  recycling caveats (DAfStb guideline 2024; not-mm rebar needs abZ route; recycling:
  optically sorted, not magnetically).
- KPP combined pile-raft + test loading: −30–50 % foundation material via calibrated
  calculation (geotech digest) — deep-foundation carbon lives in the assumptions.

### 5.4 Recycled-aggregate concrete (RC-Beton) — real rules, real limits

- DAfStb line + DIN 1045-2:2023 + DIN 4226-101 (2025-11): types T1 (≥90 % concrete
  origin, brick/KSS ≤10 %), T2 (≥70 %, brick ≤30 %), T3/T4 restricted; coarse RC
  share ≤ **45 Vol.-%** (T1) / ≤ 35 % (T2) up to **C30/37** with usual exposure;
  tighter in aggressive/frost classes (25/20 %); since 2021 first approvals for
  unreinforced/lightly-reinforced RC precast wall panels C20/25, GK ≤ 4.
- Honest carbon note: RC is **not automatically lower-GWP** — higher water uptake →
  often higher cement paste demand; recarbonisation credit at 85 % granulate only
  ~5–10 kg CO₂e/m³. RC's home ground is **raw-material conservation** (up to ~50 Mt/a
  primary aggregate replaceable nationally), not the carbon headline. Check regional
  availability + transport (DE-wide: recycled aggregate 75.3 Mt of 564 Mt used = 13.3 %,
  but only ~20 % of that into concrete/asphalt).
- Pre-wetting, flow admixtures, performance-based mix design mitigate the paste penalty.

### 5.5 Recarbonation (Karbonatisierung) — bookkeeping honesty

- Over the life, carbonation re-binds roughly **~40 % of clinker process CO₂ on
  average globally** (EU up to ~23 %; unbound/weathered crushed concrete EoL
  stock-average ~80 kg CO₂/m³ potential; in-situ bound concrete member-level credit
  per DIN EN 16757 up to ~20 % of the process share, EPD module B1).
- Rules: credits are slow (centuries-scale kinetics dk ∝ √t), undesired in reinforced
  members (depassivation → corrosion), and **never let B1 credits offset a high-A1
  design**. Active carbonation of recycled fines is industrial but emerging; CCS/CCU
  concrete products: scrutinise the module boundary claimed.

### 5.6 Timber specifics (storage, EoL, and where it is actually better)

- Storage: ~1 t CO₂ per m³ (0.5–1 t by species/density); whole harvest chain adds
  only ~5.7 kg CO₂ per Fm + 5.7 per 100 km transport → material stays net-negative
  through A1–A3 for solid products.
- GWP grows with processing depth: KVH < BSH < CLT-with-adhesive < boards; always
  co-account fasteners, connectors, fire/acoustic protection layers, and the
  **joining technology** (screws = re-use upside, glue = separation downside).
- At end-of-life: biogenic balance goes positive under the default thermal-recovery
  C4 scenario until circularity is proven — declare the scenario, don't hide it.
- Building-level: 30–45 % whole-life GHG saving vs mineral construction typical;
  THG-Holzbau study 9–56 % for 1/2-family houses; up to ~50 % (UBA case studies);
  62-study meta average 42.7 % vs RC; mid-rise office 80–99 % below steel-concrete
  depending on EoL and storage convention (T3/T4 spread!).
- Resource frame (DE): forest stock highest in Europe (~3.7 Gm³), increment ~122
  Mm³/a vs use ~80; long-term roundwood availability ~80 Mm³/a (WEHAM 2025) with a
  species shift to broadleaf — **do not assume unlimited timber**; certification PEFC
  ~79 % / FSC ~11 % of forest, chain of custody traceable (ISO 38200), EUDR
  deforestation regulation applies from end 2025 ⚠ VERIFY.
- Best fits: Aufstockung/add-on (low weight saves foundations and keeps donor
  structure's grey energy), infill densification, serial retrofit elements,
  screwed/timber-hybrid demountable frames. Watch: long spans → material intensity,
  missing mass → summer overheating and impact sound (extra layers = partial
  carbon payback), humidity/fire detail discipline.
- Re-use: exposed CLT/BSH/windows/doors re-useable with non-destructive disassembly,
  purity, no old preservatives; grading standards for reused timber exist abroad
  (NS 3691, FWPA G01) — EN grading only for virgin wood; waste wood 7–8 Mt/a DE,
  ~1.5–2 Mt into panel chips, rest mostly burned (AltholzV classes A I–IV route).

### 5.7 Steel, brick, clay, insulation, glass (compact rules)

- **Steel**: emissions/t −15 % 1990–2022; recycling ~97 % but genuine component reuse
  ≈ 0 (law/availability); EAF DE long products power-mix dependent (50–60 % EE),
  ~1/7 of BF route reachable with green power today; LESS classes A–E (D = state of
  art); H₂-DRI arriving (pilot→commercial). Design levers: standardised profiles +
  **bolted** joints = highest reuse potential; thick-welded > rolled section GWP
  (factor >2 with fire coating in one deck example) → hot design/encasement/
  composite encasement as fire alternatives; hot-dip galvanising: protection often
  > 50 a (beyond member life), re-zincable, EAF zinc handled via dust circuit;
  weathering steel = no coating (Cu/Ni/Mo scrap-load caveats); coatings: solvent-based
  VOC → DGNB best classes need water-based systems.
- **Brick/Ziegel**: fired once, kept ~150 a, >90–94 % reused/recycled at EoL (cement
  grinding, brick meal, RC aggregate, road base, sport surfaces) — the quiet circularity
  champion; thin-bed + dry-stacked joints improve deconstruction purity; unburnt
  Kaltziegel and RC-Betonstein are the upcycling variants; total DE masonry + roof-tile
  emissions ≈ 4 Mt CO₂e (<1 % national) — masonry is *not* the sector's carbon
  problem; concrete and steel are.
- **Clay (Lehm)**: DIN 18940:2023 design norm (load-bearing to FK 5, GK 4),
  Muster-EPD +99 kg CO₂e/m³ technical drying, −198 air-dried; hygroscopic buffer
  (stable 45–55 % RH with enough exposed surface), fully re-usable (cross-
  compatibility: fat clay waste + sand → mortar and vice versa), thin-bed dry-joint
  masonry deconstructs sortenrein (ABG end 2025); water/frost demands a protective
  construction (topes Feuchte-/Frostempfindlichkeit); avoid dispersion paint on
  clay (kills hygroscopy + circularity); rammed-earth design norm still in
  development (ZiE/Lehmbauregeln route via MVV 2024).
- **Insulation**: λ design tiers — EPS 0.031–0.052, XPS 0.023–0.046, PUR/PIR
  0.021–0.044, MW 0.031–0.052, wood fibre 0.034–0.063, reed 0.055–0.061, hemp-lime
  0.06–0.1. Fire rules cut options: nawaRo exterior insulation only ≤ GK 4 (≤13 m)
  (MVV TB generic exclusion of class-C-with-smouldering risk ⚠ VERIFY current MVV TB
  issue); erdberührt (in-ground) usually mineral/synthetic — use sparingly, it is
  often the "alternativlos" layer. WDVS: 30 Mio m²/a, market ~80 % EPS, life 40–60 a
  (<10 a if defective/unmaintained), NOT C2C-recyclable (composite + adhesive);
  pre-2014 HBCD boards = hazardous thermal recovery only; biocidal façade paints
  leach — prefer mineral renders/structures; mineral alternative systems (WDF,
  vorgehängte hinterlüftete Fassade, Kern-/Einblasdämmung) trade cost/checkability
  for durability and separation.
- **Glass**: one of the hottest industrial processes (0.65 % of EU industry CO₂);
  75 % combustion / 25 % process (carbonates) — only cullet cuts the process part
  (1 t remelt −300 kg CO₂); EoL recyclate from buildings < 1 %, float lines run
  16–20 a without turnaround; reuse of old IGUs shows no systematic strength loss
  >20 a; refurbish-combining (uncoated panes from several IGUs into new units) up to
  −50 %; flat recycling in renovation ≈ 3.5× cheaper than demolition recovery but
  still ~2.7× landfill cost — economics, not ethics, is the bottleneck.
- **Aluminium**: secondary ≈ 5 % of primary energy; 75 % recyclate in façade profiles
  price-neutral, up to 100 % feasible — specify recyclate share + keep sorts separate
  (downcycling risk); steel frames ≈ 1/10 of Al primary energy with 100 % recyclate
  possible; PVC frames up to 100 % recyclate content market-available.

### 5.8 Bio-based and clay build-ups — Hanfkalk, Miscanthus/Silphie, Paludikultur
(T3 branch/research data, several entries dated ⚠ VERIFY with current product EPD /
ÖKOBAUDAT before specifying; application limits govern, not the headline sink)

- **Hanfkalk (hemp-lime)**: net GWP ≈ **−130 kg CO₂e/m³** in use (acts as a sink;
  dated study — shive carbon uptake **70–240 kg CO₂/m³** vs ~50 kg process+transport;
  the digest states this CO₂-uptake range, **not** a moisture-buffering value in
  g/(m²·%fw) — MBV figures ⚠ VERIFY from tested data sheets). λ 0.06 W/(mK) @
  200–250 kg/m³ (roof), 0.07 @ 340 (block), 0.1 @ 400 (wall); density-by-use: floor
  500 / wall 400 / roof 200–250 kg/m³; PEI 1190 MJ/m³ (block) — below stone wool and
  wood fibre; c ≈ 1000 J/(kg·K); μ = 2.8; sound absorption αw 0.85 (~90 % low-mid);
  latent-heat (PCM-like) effect via evaporation/condensation in the hollow shive cells;
  hygroscopic buffering pairs with clay per 9.2. Limits: compression **0.1–2 N/mm²
  non-loadbearing only**; fire B-s1,d0, F60 proven below 450 kg/m³, plaster improves;
  erdberührt out of scope. Build-ups: cast in situ between **reversible timber
  shuttering** (crane-set timber-hybrid wall elements); tongue-and-groove blocks +
  wooden splines, mortar-less → demountable partition walls replacing gypsum boards;
  loose fill/levelling; spray hemp-lime (lost-formwork lime render on mesh) 28–30 cm →
  U 0.24 W/(m²K) GEG new-build level, 41 m³ in <5 days on a listed half-timbered
  house; double-leaf shive fill against existing masonry. Hemp agronomy: 3–4 m in
  ~100 days, drought-resistant, pesticide-free, rotation-friendly; DE fibre-hemp area
  7,100 ha (2024). EoL: carbonated shive = sellable loadbearing insulation granulate
  (acoustic floor/wall fill); compostability not covered by the fertiliser ordinance →
  plough-down on acidic fields (one state exempts ≤ 2 t/ha·yr ⚠ VERIFY); no chemical
  binders → high dismantlability; standardisation gap: foreign national rules only,
  DIN-spec + ÖKOBAUDAT entry pending ⚠.
- **Clay (Lehm) build-ups, extending 5.7**: clay bricks per DIN 18945:2024 (loadbearing,
  application class II): density classes 1.6–2.2, product strength classes **FK 2–6**,
  extruded/pressed formats up to 16 DF large plan blocks; design per DIN 18940:2023
  loadbearing **to FK 4, GK 4** ⚠ VERIFY the FK ceiling against the norm text (the
  digest's product table and design scope disagree; 5.7 states FK 5); unstabilised
  (no cement). **Dünnbett** (thin-bed) clay mortar: 2 mm bed joints, head joints dry,
  mortar-roller application, enables large formats; general type approval (ABG) for
  plan hollow bricks + clay thin-bed mortar since end 2025, fire-resistance incl.
  hochfeuerhemmend → damage-free sortenrein deconstruction (water-soluble masonry
  mortar still research). Clay boards: light ≤ 1200 / heavy > 1200 kg/m³; stud wall +
  boards → 56 dB single-leaf, 65 dB double-leaf; fire tests to EI 120; used up to
  building class 5 (public reference buildings, one ~20,000 m² boards + timber-clay
  solid floors). Rammed earth (Stampflehm): loadbearing walls 40–60 cm, geogrids
  against settlement cracks, often site-made from pit soil (lean-down/enrichment),
  factory robot-rammed prefab variants crane-assembled with trowelled-invisible
  joints; design norm still in development → ZiE/Lehmbauregeln route. Clay plaster:
  FK 2 recommended, suits splash-free kitchen/bath zones W0-I (DIN 18534-1), prevents
  window/mirror condensation; **earth-moist delivery = no drying energy** (better
  LCA); repair by re-wetting/levelling up to finish quality Q4. Clay heating/cooling
  panels: radiant wall/ceiling, water-based on low-temperature sources (HP), drywall
  install; electric variants combine with PV. **Holz-Lehm-Massivdecke** (timber–clay
  solid floor) industrialising: wood structure + clay for density (fire + acoustics).
  Durability limits unchanged from 5.7: water/frost → protective construction only;
  no dispersion paint; compatibility checks per interface (8.2).
- **Miscanthus & Silphie (perennial grass biomass)**: arable energy-crop area stagnant
  (~2.2 M ha energy vs only ~279,000 ha industrial crops, DE, dated — food-competition
  and EEG-cap framing); Miscanthus (C4 grass): yields **12–30 t DM/ha·yr chopped over
  20–25-yr stands**, harvested April–May at <20 % moisture with a maize forager,
  storage density 150–300 kg/m³, storable **without drying** if dry + weather-covered;
  bound-C claim up to 30 t CO₂/ha·yr is a very old figure ⚠ VERIFY; high lignin +
  silicon (stiffness). Silphie: **15–25 t/ha·yr**, material harvest after senescence,
  deep roots (erosion protection, humus, water storage), late flowering = beneficial
  habitat. Forms: loose chopped fill (packing density drives λ) and blow-in; bale
  construction; whole stems as thatch substitute; **Agrarbeton** (agro-concrete) —
  chopped biomass + clay/lime/cement binder + water, rammed in situ like Stampflehm
  or precast blocks/boards, incl. lightweight concrete in timber-frame infill; boards
  with starch/pMDI binders or binderless via thermoplastic lignin (steam-explosion
  pretreatment: better mechanics, costlier energy). Limits: cement alkalis degrade
  sugars/hemicellulose/lignin → set retardation + strength loss, and high water uptake
  disturbs the w/c ratio → pretreatments (alkaline leaching, water-glass/bio-oil
  coating, silanisation, aerogel passivation, set accelerators); LCA rank: Miscanthus
  and wood fibre = least-impact bio insulations (dated study ⚠); cascade if sorted:
  loose fill → absorbents → rotting or energy recovery; cement-bound blocks crushable
  into bio-based lightweight concrete.
- **Paludikultur (wet-moor farming) materials**: drained organic soils emit
  **30–40 t CO₂e/(ha·yr)** — DE: 1.8 M ha carbon-rich soils, ~92 % drained, >53 Mt
  CO₂e/yr (dated agency figure ⚠); rewetting for paludiculture **avoids up to
  40 t CO₂e/(ha·yr)** (the "40 t/ha·yr" number in circulation is the avoided-emission
  value, not a substrate yield); strategy target rewet 250,000 ha by 2030 ⚠ VERIFY;
  long-term up to ~1 M ha convertible; ~5 % of the DE insulation market would need
  ~120,000 ha rewetted moor (model estimate). Crops: Schilf (reed), Rohrkolben
  (cattail), Rohrglanzgras (reed canary grass), wet-meadow grasses, sedges, sphagnum
  (3–5 a cycles), alder (decades); stem biomass (Halmgut) **3 to >15 t DM/ha·yr**,
  ~50 % of DM is atmospheric carbon → net-negative-material potential with higher
  storage efficiency than timber products; summer or winter harvest, baled/chipped,
  field-dried/redried/silaged for year-round supply. Product data (λ W/(mK) / ρ kg/m³
  / reaction class): reed board 0.055–0.061 / 145–155 / B2; cattail build+insulation
  board 0.044–0.055 / ~270 / **B1 naturally flame-retardant**; blow-in 0.040 /
  80–90 / B2; grass-fibre mat 0.041 / 40 / **E**; mycelium-on-reed board
  0.037–0.043 / 130 / in progress; biomass foam board 0.037–0.040 / 65–97 / passed
  EN 13501-1 flame test (prototypes: plasterboard substitutes, green-roof substrate
  mats, loadbearing composites, sandwich panels, biochar components). Thatch: lifespan
  ~30 a (often more), service interval up to 5× and cost 2–3× a tile roof; ~1,000 new
  thatch roofs/a DE, stock ~30,000, need ~3 M bundles/a, only ~15 % regional reed
  (imports from E/SE Europe + China wreck the LCA; full regional cover ≈ 10,000 ha);
  **old thatch is hazardous waste (Sondermüll) in DE** ⚠ VERIFY current classification
  practice. Cattail fibre = clay-plaster additive; reed stems = acoustic elements;
  late-harvest-grass biochar = stable C sink, tested in concrete without measurable
  loss and in bulk insulation. Limits: **most products lack general building approval**
  → ZiE / project-specific type approval; provenance certification for rewetted-moor
  origin still in preparation; scale bound by regional feedstock and agri-law
  barriers; B2/E reaction classes restrict use to protected/covered build-ups
  (fire rules per 5.7).

## 6. Operational energy: duties, demand, and the systems ladder

### 6.1 What the law requires (GEG 2020/2024 → GModG trajectory, ⚠ VERIFY edition)

- New-build proof via Referenzgebäude: **Qp ≤ 0.55 × Qp,Ref** (residential: heat/DHW/
  ventilation/cooling; non-residential incl. lighting; on conditioned area) AND
  residential **H′_T ≤ H′_T,Ref** (typical achieved 0.25–0.45 W/(m²K) incl.
  ΔU_WB 0.05), non-residential component maxima Ū (opaque 0.28 ≥19 °C etc.,
  GEG Annex 3 line); existing-building component limits on retrofit (wall/roof 0.24
  (0.35), window 1.3 (1.9), glazing 1.1 — parenthesised = GEG-era alternates,
  ⚠ VERIFY current annex); +40 % allowance for existing components in some
  configurations; extensions 1.2×/1.25×; small buildings ≤50 m²: first-installation
  values suffice.
- Reference building (anchor values to reason against): wall U 0.28, roof 0.20,
  window Uw 1.3 (g 0.60), ΔU_WB 0.05, improved condensing-gas heating, central DHW +
  solar, n50 category I; **building automation required by GEG for non-residential
  (GA class B ≥ 290 kW Nennleistung ISO 52120)**, inspection duties HVAC >70 kW come
  with EPBD.
- Heating law 2024 line: 65 % renewable heating duty for new installs with municipal
  heat-planning escape hatches and transitional ladders ⚠ VERIFY current enactment
  (2026 relaxation debate underway; GModG rename).
- PV duties patchwork: state rooftop-solar duties for non-residential (Bavaria since
  2023 >50 m² roof, residential soll-rule 2025; BW stricter; parking-lot PV in some
  Länder), GEIG pre-wiring/charging quotas (1/3 pre-wired + ≥1 charger >6 spaces),
  EPBLD Art. 10 stages a general solar duty ⚠ VERIFY which state clause bites the plot.

### 6.2 Demand by stock age (the honest table — trajectory, not per-band norms)

| Vintage | Specific heat demand kWh/(m²a) | Notes |
|---|---|---|
| ~1980 pre-modern stock | 200–270 (historical) → unretrofitted tail still ~150–200 | class E–H ≈ 42 % of stock; ~60 % of dwellings pre-1979 (first WSchV) |
| Average DE stock today | ≈130 | renovation rate 0.69 % (2024) must ≥ double |
| GEG-compliant new build | ≈40–60 | H′_T 0.25–0.45 |
| EH55/EH40 | ≈ −55 %/−40 % vs reference; EH40 ≈ 30–45 | subsidy tiers |
| Passivhaus-class | ≤15 heat; ~10 W/m² load; n50 ≤ 0.6 | 0.10–0.16 opaque, 0.67–0.8 windows |
| New technical band | 15–50 | electricity share rises as heat falls → PV+storage concepts, not bigger boilers |

Efficiency-house ladder concept: the "EH<nn>" number = share of the GEG reference
primary-energy result; ladder EH100 → 85 → 70 (Jung-kauft-Alt floor) → 55 → 40 →
40 plus (plus-energy: negative annual primary balance incl. exported) → with QNG
seal for the best loan terms (KfN: EH40 + QNG, no oil/gas/biomass; ~100 k€→150 k€/WE
⚠ VERIFY program amounts; KNN low-price tier = EH55 + QNG-Plus + LCC ceiling +
minimum room counts). Rule of thumb for the agent: **each ladder step buys
insulation/windows first, machines second; stop when marginal grey energy of extra
insulation exceeds operational savings** — check section 12.3.

### 6.3 Heat pumps — sizing and operation logic (numbers with building-services-tga)

- Source choice: air ≈ 85 % market (cheapest, −15 to −25 °C models, mostly permit-free,
  noise!), groundwater 8–10 °C constant = best efficiency but Fe 0.2/Mn 0.1 mg/l
  limits + permits (≈5 % market), borehole ≈ 20 m/kW (permit duty), collectors
  ~200 m²/kW at COP 4 (never undersize — icing), Eisspeicher, energy piles
  (up to 50 % cheaper per metre than boreholes; JAZ ≥ 6 achievable with balanced
  seasonal use, >50 a life, 3–10 a amortisation vs 12–15 for boiler+chiller).
- Sizing chain: heat load (two consumption-based methods + DIN EN 12831 check; e.g.
  Hottinger 5.95 vs 12831 6.7 kW on a terraced house — reconcile variance), then
  machine selection from the VWL performance matrix, bivalence point at 55 °C flow
  (target −10 to −12 °C → machine covers 113–145 heating days continuous; smaller
  unit + longer runtime beats big+staccato), DHW: separate store > combo, heating
  heat-pump needs a store, PV-charging of DHW year-round fine, space-heat-PV only
  shoulder season.
- Economics rule that survives price swings: **HP wins when Strompreis ≤ 3 ×
  Brennstoffpreis** (30 ct vs 10 ct example: HP at JAZ 3 = 10 ct/kWh vs 11 ct
  boiler); CO₂ pricing pushes this further every year. Lockable tariff −5 ct/kWh
  needs its own meter + 250–500 l buffer but kills PV self-use on heat — decide
  deliberately (dynamic tariff + AI control case: effective price <0 ct months;
  −64 % cost on a 2-day window; treat as emerging, ⚠ VERIFY tariff products).
- Emissions: DE grid 2022 ≈ 434 g CO₂e/kWh (50 % EE; book factor 560 ⚠ VERIFY → use
  current UBA figure, falling ~5 %/a); oil 266, gas 201 g/kWh; HP at JAZ 3 ≈ 145
  g/kWh ≈ −28 % vs gas; HP + PV (9.96 kWp, measured year) −61 % and 53.6 % autarky
  on a 1969 terraced house (measured COP 3.5; note heat-pump-before case: −26.9 %).
- Retrofit suitability by age: ≥1995 very good (panel radiators present), 1978–1995
  usually good (swap old IGUs, roof air-tightness), pre-1978 often hybrid
  (bivalent-alternative with existing boiler kept for <50 % load hours) — but
  **low-hanging fruits first** (roof, external wall, windows, pipe/armature
  insulation, hydraulic balance), flow ≤55 preferably ≤50 °C, ribbed radiators
  (~75 °C radiant) → panel swap, HT machines 60–75 °C in homes = refuse.
- Noise: ≤35 dB(A) night in pure/general residential (TA Lärm 35/50 band), units
  <55 dB(A), BWP sound calculator, set-back/hood measures; refrigerant: R290
  (propane, GWP 3) preferred — flammability siting rules; R744/R717 commercial.
- Legionella guard: DHW store ≥60 °C capability, weekly auto heat-up; ~1200 cases /
  ~60 deaths DE 2020 (why the duty exists).

### 6.4 PV + storage sizing logic (energy-digest numbers)

- Yield: horizontal 900–1200 kWh/m²a → 30° south: N-DE 1130 / mid 1200 / S-DE 1300;
  performance ratio ~0.8 → **904–1040 kWh/kWp·a**; winter share ≈ 25 % (load-coupled
  with HP); E/W −10–15 %, vertical façade −20–40 %; facade-integrated theoretical
  area > roof area in DE (ifo line). Module temp −0.4 %/K → ventilate; partial shade
  kills string current → layout around chimneys/arrays.
- Area: monocrystalline 4–5 m²/kWp (poly 5–7, thin-film 10–20); life-cycle energy
  output up to ~20× manufacture+install energy.
- Sizing to load, not to roof: base-load rule — size PV to the always-on demand
  (Grundlast ~5 W/m² office) for ~100 % self-consumption; battery extends it:
  residential 5–10 kWh, Li-ion η 80–90 %, ~10 % of annual final energy as buffer for
  grid-friendly operation; economics of battery still price-sensitive (2016-vintage
  lesson: battery killed the annuity until <~400 €/kWh ⚠ VERIFY current €/kWh);
  thermal buffer (Pufferspeicher, Bauteilaktivierung power-to-heat) is often the
  cheaper "battery".
- Contracts/supply: Mieterstrom (sell within building, ≥10 % below basic-supply tariff,
  full-supply duty → residual-power partner or storage), §42b communal building supply
  (no full-supply duty, 15-min metering), balcony PV §3(43) EEG (small lever ecologically,
  strong sensitisation lever), EV charging via GEIG pre-wiring; VPP flexibility potential
  up to ~100 TWh/a ≈ 10 % of 2035 demand (recognition: storage back-feed rules
  currently counterproductive ⚠ VERIFY).
- Agri/surface conflicts: PV vs roof greening reconcilable (biodiversity pairing);
  ground-mount prefer artificial surfaces; agri-PV per state.

### 6.5 District heat and the "passive → semi-passive → active" order

- DH facts: new networks ≤140 (max 180) °C, 2-pipe keep ≥70 °C year-round for DHW;
  indirect transfer (plate exchanger) = no high-pressure fittings in units; fp
  factor 0.7 for fossil-CHP networks (≥70 % CHP share), 0.0 renewable-CHP, published
  site-specific FW 0.0–1.23 (certificate validity 10 a ⚠ VERIFY), GModG floor 0.3
  minus 0.001/% renewable/waste heat; WPG municipal plans → expect connection duties/
  priority zones; **in heat-planned areas, DH or HP+network beats on-site fossil**
  and often beats individual HP on resilience.
- The mandated measure order (never invert it without a simulation to prove it):
  1. passive: form, orientation, shading, glazing g, daylight, mass/air-tightness;
  2. semi-passive/regenerative: demand-controlled ventilation with >85 % heat
     recovery (Lüftungswärmeverlust ≈ 50 % of envelope losses in tight new builds),
     PV, solar thermal, free cooling, store (thermal/battery);
  3. active: HP (sectors-coupling), DH incl. high-temp HP/geothermal, CHP/BHKW/
     fuel cells, anteilige biomass (altbau), Power-to-Gas last; direct electric only
     behind 30–45 % better-than-reference envelope gates (⚠ VERIFY §-numbers).
- Sizing via simulation reduces plant size (and capex + standing losses): dynamic
  simulation is the alternative to worst-case dimensioning (Gebäudetyp-E logic:
  sufficiency parameters + simulation instead of norm-driven overbuild).

## 7. Resources, land, water, and waste (Rohstoffe & Fläche)

### 7.1 Land and sealing (Flächenverbrauch)

- ~52 ha/day new settlement+transport land (DE); anti-sprawl levers: interior
  development §34, brownfield acceleration §13a BauGB, GRZ/OFS caps, densify-existing
  rights (Aufstockung, larger footprint allowances), B-Plan building-line/height tools
  (§§18–23, 1a EFTA quality-scored compensation), Stellplatz reduction via urban
  contracts §11.
- Compactness numerics ("CO₂-Monster" urban study T3): 7-storey blockrand A/B ≈ 67 %
  vs 10 detached 4-storeys ≈ 121 % — same BGF, ~9,900 m² less envelope = grey energy +
  land saved; small-lot commuting penalty ≈ +1.4 t CO₂/(capita·a) and 7–8× sealing vs
  blockrand city; 400 m² plot: weekend house 30 m²/2 persons vs GFZ 1.5 450 m²/11 vs
  Gründerzeit GFZ 3.4 1020 m²/27.
- Sealing duties: BayBO Art. 7 non-built areas permeable+greened; compensatory
  planting clauses; Entsiegelung + retention (Schwammstadt: keep rain on plot —
  note the DIN-flat-roof-drainage-clause conflict ⚠ coordinate with authority).
- Offsetting arithmetic for honest talk: one beech binds ~12.5 kg CO₂/a → 1 t = 80
  trees = ~5,300 m² of managed forest. Per-capita framings: DE 7.2 t CO₂ (2023,
  10.4 t CO₂e all gases), global 37.8 Gt.

### 7.2 Waste and secondary materials (Kreislaufwirtschaft)

- Hierarchy (KrWG): vermeiden → wiederverwenden → stofflich verwerten → energetisch →
  beseitigen; R-strategy ladder puts **R3–R7 (reuse, repair, refurbish, remanufacture,
  repurpose) before technical recycling**; 10R for façades (Refuse…Recover).
- Binding quotas: KrWG Art. 14(2): ≥ **70 Gew.-%** non-hazardous C&D waste prepared
  for reuse/recycling since 2020 (excluding naturally occurring material); EU taxonomy
  substantial-contribution circularity: ≥ **90 Gew.-%** reuse/recycling of C&D waste
  (incl. backfill), DNSH gate ≥ 70 % (waste key 17 05 04 exclusions); DE C&D + spoil
  ≈ 54–55 % of all waste; Bauschutt already >90 % "recovered" — **mostly downcycled**
  to road base/fill, little into real aggregate: the quota is met, the loop isn't.
- Sorted site capture per GewAbfV; **Rückbaukonzept** (deconstruction concept:
  Schadstoffsanierung, Rückbau, Wiederverwendung, Wiederverwertung, Entsorgung) is a
  procurement deliverable; DIN SPEC 91484 Pre-Demolition-Audit standard.
- Secondary raw materials: aggregate RC share 13.3 % and rising (section 5.4); REA
  gypsum ~50 % of DE gypsum demand (declining with coal); GGBS/fly ash availability
  flags (5.2); steel scrap-classification quality gates; paper/plastic/membrane
  streams mostly thermal (microplastics on demolition of bonded EPS = emerging
  pollution flag).
- Reuse reality: **< 1 % of building components** reused today; barriers = legal
  status of taken-down material (waste/product/building law not linked), logistics
  for small volumes, price parity vs primary, quality trust; remedies = take-back
  contracts, exchange platforms (generic: material exchanges), insurance products for
  used components emerging, §18 BauO-type state re-admission rules, LkSG duty-of-care
  on the *original* production of re-used parts. Abbruchverbote (demolition bans)
  counterproductive as a tool; reuse is not an end in itself (for wood and concrete,
  industrial recycling is sometimes the better option — compute).
- Excavation: Aushub = 70–80 % of C&D tonnage by key 17 05 → reuse-first levers:
  compaction piles from rubble, ZFSV self-compacting fill for trenches, landscape
  earthworks, on-site treatment chains (sample → clean/stabilise → lab proof →
  full-scale test → release); DE landfill scarcity (DK0/1 capacity, ~1,000 sites left)
  makes soil circularity a schedule risk, not just an eco topic. Transport reality:
  Hessen example 13.9 Mt/a at 47 km average = 215 kt CO₂/a (≈ 36,000 ha forest
  equivalent) — **material loops must be regional to count**.

### 7.3 Water (recognition; detail in building-services-tga)

Infiltration/retention on plot, green roof/wall retention, rainwater + greywater
(Toiletten-/Bewässerungsnutzung), flow-limited fittings (taxonomy documentation asks
for fitting flow rates + photo evidence), groundwater/water-body impacts checked
early (WRA zones, §35(6) privileged biomass/wind clauses relevant on rural plots).

## 8. Circularity by Design (Kreislaufgerecht planen)

### 8.1 The seven design levers, in impact order

1. **Keep** — Bestand, Umnutzung, Aufstockung (highest save; grey energy of stock = 0
   in the public new-build-only calculation convention → strongest formal argument).
2. **Design for Disassembly (DfD, ISO 20887)** — reversible single-material joints:
   bolt/screw steel and timber (standard!), dry/thin-bed clay and brick joints
   (research: water-soluble masonry mortar), clip/vellcro and pure-mechanical
   fastening trials for façades; avoid glued laminates and cast-in composites where
   the bond prevents separation; Demontageplan + connection details as deliverables.
3. **Separability (Sortenreinheit)** — one-material layers, visible layer order,
   air gaps as peel planes; the composite-equals-downcycle rule (WDVS, HBC glued
   finishes, filled bricks, wood-concrete without separable connectors → those are
   element-reuse objects instead of material-reuse ones); multi-leaf over monolithic
   where cycles differ (repairable, exchangeable).
4. **Long life of what cannot be separated** — couplings/seals/screws rated 25 a are
   the hidden defect of a 50-a balance sheet: specify ≥50 a or accessible exchange;
   water is the killer: "Wasserkonsequent ableiten" costs build-up money and saves
   whole-life money (most frequent rehabilitation cause = water ingress).
5. **Low-carbon, durable, regional materials** (section 5) with verified delivery.
6. **Adaptive structure** — usage-neutral skeletons, load reserves, service routes,
   generous floor-to-floor heights, movable partitions; office→residential change
   over life saves more than any product swap (Betrieb vs Umbau cycles 5–30 a).
7. **Document it** — material registry / Gebäuderessourcenpass / EPD archive /
   PCDS-style circularity sheets / BIM handover (IFC/COBie) so the next cycle gets
   real data, not assumptions; data generated at deconstruction (survey, tests) is
   expensive — pre-generate it at construction.

### 8.2 What NOT to circularise (honesty rules)

- Insulation in practice: EPS/XPS/PUR/MW → thermal recovery mostly (productions
  offcuts ≤5 % clean re-cycle; new separable systems emerging); after-used gypsum and
  mixed mineral wool: site-dependent.
- Hybrids that fight each other: material pairings with incompatible moisture/
  chemical behaviour (Lehm ↔ oil-based coatings; dispersion over clay; bitumen in
  bio loops) — check material compatibility per interface, not per material.
- Concrete reuse: classes 1–5 ladder (same-function demounted member with joints →
  lower-function Weiterverwendung → crushed RC → landfill); cutting methods (saw /
  water-jet best), friction of dry joints lower than codes assume (μ up to ~0.6
  shot-blasted) → component tests, not book values; aged-concrete duration factor
  0.85 questionable (long-term tests 70–75 %).
- Recycling ≠ sustainability (wood: industrial recycling of chips into panels keeps
  ~1 t C stored and is often better than burning a "re-used" beam that fails grading);
  reuse ≠ automatically better — compute both, incl. transport and re-certification.

### 8.3 Procurement instruments that make it real (recognition; contract detail →
building-regulations-permits / cost skill)

- Functional performance descriptions (FLB) + two-stage procedure + dialogue-optimised
  execution; LCA/CO₂ ceiling clauses (AG reference mass, shadow-price bonus/malus per
  KPMG/Bauindustrie line: undershoot → price advantage); minimum eco criteria = EMAS/
  ISO 14001 "or equivalent"; award criteria across life cycle per VgV/§127 GWB + §16d
  EU(2)5 VOB/A external costs; LV-level levers: FSC, Blauer Engel, recyclate-content
  and GWP/m² limit values, one-material reversible-connection text blocks, used-component
  lots (interior doors, RC concrete); contractual duty to deliver material documentation
  (funding payouts increasingly tie to it); integrated project models (IPA/TU/GU)
  lower the interface cost that circular delivery otherwise pays for.

## 9. Indoor environment, health, and comfort (Gesundheit & Behaglichkeit)

### 9.1 Binding/hard pollutant limits (T1-adjacent, taxonomy Annex C DNSH)

- SVHC in products > 0.1 mass-% → not taxonomy-aligned; notify/avoid.
- Interior-relevant products (paints, boards, floorings incl. adhesives/sealants,
  interior insulation, surface treatments): emission < **0.06 mg formaldehyde/m³
  material** and < **0.001 mg/m³** for other category-1A/1B carcinogenic VOCs.
- Wood-based panels: aldehyde-emitting resins (UF/PF) → low-emission grades/
  melamine/PMDI; declare the class, verify by IAQ measurement at handover — a late
  indoor-air measurement failure can sink a certification (test body gate).
- Façade biocides (algae/fungus protection in synthetic renders) = uncontrolled
  emission source → mineral surfaces/structures instead.
- Legacy hazards (renovation): HBCD EPS pre-2014, PCBs, Lindan/DDT (Holzschutzmittel),
  weak-bond asbestos (spray coatings, pipe lagings), PAHs in adhesives, old mineral
  wool with problematic fibres, Pb/Cd cables/windows — Schadstoffgutachten before
  specifying the deconstruction, separate disposal paths (section 7.2).
- **Radon** ⚠ VERIFY (not in digests): StrlSchG reference level 300 Bq/m³ annual
  mean for existing rooms; preventive design where the site is radon-priority-area:
  air-tight floor slab (abZ-duties), under-slab ventilation/compensation layer,
  no unsealed service penetrations — route to the physics skill for the proof.

### 9.2 Moisture, mould, and the physics link

- Mould threshold: surface φ > 80 % for days → the 12.6 °C minimum surface-
  temperature criterion (θi 20 °C/50 %) and fRsi checks live in
  building-physics-thermal-moisture; sustainability angle: diffusion-open,
  capillary-active build-ups over plastic vapour barriers (high PEI/GWP), **but
  health outranks the material score** (digest rule: "Gesundheit geht stets vor").
- Hygroscopic buffers (clay, hemp-lime, cellulose, wood fibre) stabilise 45–55 % RH
  with sufficient exposed surface (still needs user ventilation); PCM effect in
  hemp shives via evaporation/condensation.
- Ventilation hygiene: CO₂ as proxy — Pettenkofer 0.1 Vol% = excellent (MAK 0.5);
  18–72 m³/(h·person) outside air by activity; demand-controlled ventilation;
  ASR/VDI 6022 hygiene duties on RLT (filters #1 sick-building cause).

### 9.3 Comfort parameters (the "sozio-kulturelle" quality that drives longevity)

- Thermal: operative temp summer ≤28 °C (activity-dependent), winter ≥~20/17; PMV
  −3…+3 with PPD; vertical gradient cat A ≤2 K; radiant asymmetry ≤~13.5 K chilled
  ceilings; core activation gives radiator-equivalent comfort at ~2 °C lower air
  temperature (heating 25–30, cooling 30–40 W/m², 60 % radiant) — a genuine
  energy + comfort double-win with low-temperature sources.
- Summer protection: external shading (F_C ≤0.35–0.5 logic; venetian/raffstore
  best), night purge ≥2–5 h⁻¹, mass classification C_wirk — full method belongs to
  the physics skill; sustainability note: the mass-vs-insulation choice is a
  comfort↔carbon trade-off to disclose (light timber needs added mass or active
  cooling; dense construction needs shading discipline).
- Daylight: MBO §47 window ≥ 1/8 NRF (rough build) as legal floor; DIN EN 17037
  target bands; daylight-linked dimming saves 30–75 % office lighting; view-out and
  bird-safe glazing (collision) are the social-ecological pair.
- Acoustics: DIN 4109 is the public-law minimum; BGH 2009: minimum is insufficient
  for comfort new-build → contract VDI 4100 SSt II/III or 4109-5; TGA noise 30/35
  dB(A) duties; pointers to building-acoustics.
- Accessibility/function: DIN 18040 / Design for All / BMI guideline; barrier-free
  concepts agreed with the building authority; long-tenure = sustainability (a
  60-a reference use period only pays if people stay — user satisfaction drives
  length of use).

## 10. Certification orientation (DGNB, BNB, QNG, and friends) — tool, not trophy

### 10.1 What exists

- **DGNB** (German Sustainable Building Council, 2007, >2,800 members): holistic,
  lifecycle-based; criteria families: ecological quality, socio-cultural and
  functional quality, economic quality (life-cycle), technical quality, process
  quality, site quality; quality levels Bronze → Silver → Gold → Platinum by share
  of achieved requirements; application types new/existing/quarter + site/construction
  certificates; auditor-driven (DGNB-Auditor); LCA + deconstruction analysis + LCC +
  bio-ecological supervision are the heavy content (LCA often the single biggest
  score lever); example project achievement levels ~85–86 % = Platinum band (case data).
- **BNB** (federal building standard, coordinator model, public buildings; Silver/
  Gold levels; same family logic).
- **QNG** (quality seal for sustainable buildings, accredited certifiers e.g. DGNB):
  the key that unlocks the best KfW efficiency-house loan tiers; quantitative
  lifecycle-GWP limit classes.
- LEED (US; energy/water/materials/IAQ/site; Certified…Platinum), BREEAM (UK; broadest
  global coverage incl. themes land/waste/pollution/management; new international
  NC adds circularity section, pre-demolition credits), WELL (human health),
  WiredScore; national variants (Minergie CH, ÖGNI/TTQB AT, HQE FR, CASBEE, Green Star,
  PromisE FI) — recognition level; rough comparison from digest: DGNB strongest on
  lifecycle/LCC/documentation/pollutant-input; BREEAM broad themes, strong summer/
  daylight; LEED strong daylight/primary-energy — ⚠ VERIFY per current version.
- Product certificates feeding building scores: EPDs underpin material credits;
  EMICODE (emissions), Blauer Engel, FSC/PEFC, Cradle-to-Cradle, HPD/C2C chemistries.

### 10.2 When it is worth it, when not

- Worth it: institutional/public buildings (BNB), funded projects (QNG gate),
  assets facing finance/exit (taxonomy/GRESB evidence, Green-Lease data base), complex
  stakeholder projects needing a fixed metric set and audits as discipline — and,
  increasingly, as investor assurance rather than marketing.
- Not worth it: single-family homes chasing a plaque; certificate ≠ climate-
  neutrality (DGNB Platinum / BNB Gold guarantee nothing about the 2045/2050 path);
  point-chasing ("cheap high-yield points") can distort design; pre-check variant
  (potential analysis, target corridor) captures most of the steering value at a
  fraction of the audit cost.
- Select by: branch relevance, recognition in the financing market, requirements,
  cost, validity cycle, support depth; budget the certification-management service
  (AHO Heft 33 line) and an early sustainability coordinator (AHO Heft 9/6th ed.
  makes it base service for project steering).

## 11. Life-cycle costs (Lebenszykluskosten, LCC)

### 11.1 The share split that should change minds

- **> 80 % of whole-life costs sit in operation/use** (energy, water, cleaning,
  maintenance, renewal) — construction cost is the small head of the tail (public-
  procurement LCC definition: acquisition + use + maintenance + end-of-life +
  external environmental costs).
- Rule of thumb: operating costs equal the purchase price after ~7 a (2013-vintage
  anchor ⚠ VERIFY with current energy/labour prices) → every design conversation
  about "too expensive" must be about annual cost, not capex.
- Repair-before-replace economics: insurance/asset practice trend; maintenance
  accessibility of TGA planned in (Wartungszugänglichkeit), complexity reduction
  (Performance Gap: more installations → more consumption + failures), and the
  water-first rule (section 8.1/4) all protect the B-cycles.

### 11.2 DIN 31051 vocabulary (German building management, do not translate loosely)

| Term | DIN 31051 | Meaning |
|---|---|---|
| Inspektion | W | condition + wear-cause detection, no function change |
| Wartung | W | slow wear reserve depletion (servicing) |
| Instandsetzung | W | restore function (repair/replace at life end) |
| Verbesserung | W | safety/standard improvement without function change |
| Modernisierung | DIN 32736 / rental law | value/standard/usefulness raise (energy, water, utility) — rent increase legally tied to *Modernisierung*, not to *Sanierung* |
| Sanierung | building mgmt | fixes structural deficits; may extend; energy-savings framing always improvement-oriented |

### 11.3 Static comparison method (worked, 40-a horizon, 2 % interest)

Floor finishes, €/m²·a = kalk. Abschreibung + halbierte Verzinsung + zyklische Kosten
+ Reinigung (5–6 €/m²·a):

| Build-up | Cost €/m² | Use life a | Cycles | €/m²·a |
|---|---|---|---|---|
| Carpet | 10 | 10 | 4× | 6.10 |
| Parquet (seal 8/10 a, sand 20/20 a) | 60 | 40 | 1× + cyc. | 9.20 |
| Natural stone (joints 15/20 a) | 80 | 60 | <1× | 9.78 |

→ the cheap product is only cheap while you accept 10-a cycles; a 50-a certificate
system (or LCA) sees the same reversal (seals 25 a: double the A+B impacts). Always
compare **Nutzungsdauer-adjusted** variants, and run the dynamic methods (annuity,
NPV, IRR — VDI 2067) when interest or price scenarios carry the decision.

### 11.4 Modernisierungspflichten and retrofit finance logic (concept level, ⚠ VERIFY rates)

- Rental-law frame: tenants tolerate Modernisierung (energy improvement etc.); landlord
  may raise rent by the legally apportioned share of cost; **Sanierung (defect
  remediation) does not earn rent**; economic verdict for the holder: Fall 1 harvest +
  watch market (retrofit or divest), Fall 2 optimisation potential (lower opex,
  right-size), Fall 3 no potential → sell frees capital. CRREM stranding date is the
  clock: do-nothing → stranded (hotel case: 2026; retrofits A+B pushed it to 2036).
- Statutory triggers to design around: GEG/GModG retrofit duties on component
  exchange (Anlage-7-type maxima) and (state) heat-supply duties on purchase/
  inheritance (BW: climate-modernisation clauses; tax-deduction instruments for
  inherited-building retrofits planned ⚠ VERIFY); "Worst first" (classes F–H) is both
  the policy target and the hardest client profile (missing foundations,
  half-timbered constraints, single/box windows, harmful-substance surveys, ageing
  owners, local-trust vs tender rules) → plan a Modernisierungsfahrplan: inventory →
  targets → variants → CRREM → costs+subsidies → measures plan (AHO 21-type service).
- Social guardrail (digest, explicit): **sozialverträgliche Sanierung statt
  Verdrängung** — vacancy-phased works, tenant care 2 a before start, relocation
  support, rent-burden windows; displacement is a design failure mode, not a side
  effect.

### 11.5 Contract mechanics that protect the LCC/LCA case (recognition)

- Leistungsziele ladder in planner/contractor contracts: Programmklausel <
  Bemühensklausel < **Beschaffenheitsvereinbarung** (owed characteristic, e.g.
  "planning suitable for DGNB Gold v…") < Garantie; certification target is owed
  as "certificate-ready planning" (auditor dependency does not excuse); CO₂ ceiling
  clauses and taxonomy-alignment duties only owed if contracted (fix the reference
  date!); aaRdT deviations only valid with disclosed client consent (safety-class
  aaRdT never); §650b change orders need Nachhaltigkeits-Folgenabschätzung per
  substitution (material swap changes the Ökobilanz — re-run it).

## 12. Trade-off resolution method (how the agent reasons and discloses)

### 12.1 The four objectives to keep visible

Every meaningful design decision trades among: (1) **structure** (stability, spans,
reserves, buildability), (2) **physics** (thermal/moisture/acoustic/fire — the T1
gate), (3) **carbon** (A1–D whole-life + B6 with the current and projected grid),
(4) **cost** (capex + >80 % operation + exit/stranding). Add (0) **sufficiency** as
the pre-question: does this element/space/system need to exist at all?

### 12.2 Fixed order of intervention

1. Ask the task behind the request (Suffizienz; reuse existing; shrink program).
2. Form/compactness (A/B, A/V, orientation, shading, massing) — biggest lifecycle
   lever, cheapest (urban study: over 50 a, form influences CO₂ more than grey
   energy of materials).
3. Structure + material choice (section 5 matrices) — locks most embodied carbon.
4. Envelope standard + details (water-first, thermal-bridge discipline, ≥50-a parts).
5. Systems ladder passive → semi-passive → active (section 6.5); right-size by
   simulation; low-tech preferred for resilience + operability.
6. Renewables + storage + flexibility (PV/HP/battery/demand response).
7. Credits, offsets, certifications — last, never as substitutes.

### 12.3 Cross-domain arbitration rules (the ones that decide real projects)

- Bestand > Sanierung > Neubau (emission reduction over efficiency optimisation as
  the goal); grey energy in stock is a CO₂ argument — demolition must beat it with
  data (e.g. urban retrofit case: primary energy −15 % below EH40 on existing shell).
- Same-U comparison: compute U **and** PEI/GWP of the wall (section 5.1); a thicker
  cheaper-carbon wall that saves B6 faster than it costs A1–A3 wins; compute the
  crossover on the project's heating profile, don't quote others' "up to 50 %".
- Fire/acoustic/mass constraints overrule carbon aesthetics: nawaRo insulation
  ≤ GK 4, GK 5 needs "feuerbeständig" → timber out; Holzbalkendecken retrofit can
  trigger a mass-cascade (balustrades, pods, lifts) that erases the carbon win —
  check the cascade before the slogan.
- The aaRdT (generally accepted rules of technology) trap: DINs are voluntary
  solution proposals but jurisprudence equates them with the owed standard →
  innovation needs either (a) right-safety path (ZiE/abZ, performance proof +
  simulation instead of worst-case norms), or (b) informed client deviation
  (Gebäudetyp-E logic ~10 % cost saving from dropping non-essential comfort —
  ⚠ VERIFY legislative status); the agent proposes deviations only with explicit
  documentation + specialist sign-off, never silently.
- PV beats almost every insulation thickness debate on cost and CO₂ when the roof
  is available — but check statics/snow/fire (0.5 m boundary zones, non-comb
  distance rules), and pair with HP load-shifting for self-consumption.
- Complexity has a lifecycle cost (section 1.5/3.2): refuse CCF/double-façade
  solutions without a maintenance concept; refuse HT heat pumps in homes; refuse
  un-inspectable concealed dependencies (Beton-Fertigteil Schrägabhängungen) in
  anything meant to survive change.

### 12.4 Disclosure template (use verbatim structure in outputs)

> **Entscheidung:** <variant chosen>
> **Zielgröße & Rechenstand:** modules A1–A5/B4/B6/C/D, 50 a, €/t CO₂e = <0|250>,
> data tier <T1–T4>, sources <EPD/database>, date <…>
> **Gewonnen:** <metric deltas, e.g. −1160 t CO₂, −12 €/m²·a>
> **Bezahlt mit:** <the sacrificed objective, e.g. +4 % span-consumption, GK-limit,
> 4 dB acoustics headroom loss, +3 % floor area, 25-a exchange cycle>
> **Unsicherheit:** ±<%> due to <EoL scenario / grid path / price>
> **Empfehlung prüfen durch:** <lCA tool run / Fachplanung / physics proof>

If two variants win on different objectives, present the Pareto pair and the
decision-relevant tie-break (risk, schedule, financeability), not a hidden blend.

### 12.5 Scenario levers to run (cheap sensitivity that changes verdicts)

- Grid decarbonisation path (B6 factor 2025 vs 2045): flips electric-vs-gas and
  timber-vs-mineral conclusions.
- CO₂ shadow price 0 vs 250 vs 809 €/t: re-ranks structure materials and heating
  systems; run both in tenders (procurement law allows it).
- EoL scenario for biogenic materials: thermal recovery vs storage vs recycling.
- Exchange cycles over the horizon: seals/windows/HP at 25/40/15 a — the B4 test.
- Use-rate/adaptability: occupancy +10 % or office→residential conversion feasibility.

### 12.6 Tooling note (recognition)

Iterative planning-begleitend LCA tools (national public web tool; commercial
LCA/LCC/circularity packages), generative-design Pareto studies on BIM models,
CRREM pathway tools, SNAP/BNB/DGNB pre-checks, KfW LCC tool (KNN requirement),
BBSR SNAP/A1–A5 DIN 18205 checklists, data-quality honesty (30 %+ of project data
rated poor in one large survey — digitise old docs before trusting model outputs).
The agent's job is to keep the metric set honest, not to pick favourite tools.

## 13. Strategy matrices per decision

### 13.1 Structure choice

| Driver | Preferred move (with its paid trade-off) |
|---|---|
| Low/medium-rise housing, no special fire/acoustic demand | Masonry/clay monolith or timber frame; disclose: long spans, masses for summer |
| Large spans, industrial, parking, basement watertight (Weiße Wanne) | Concrete stays (statisch kaum substituierbar); optimise: CSC L2/L3, hollow-core/flat slab, unreinforced footings; disclose fire/embodied residual |
| Height/weak foundation/add-on on existing | Timber/hybrid (weight = foundation + donor relief); disclose fire (GK ≤4 practical), acoustics add-on, EoL storage convention |
| Demountability/saleability of structure | Steel or timber, bolted standard sections; disclose: BF-route steel carbon, corrosion/fire protection lifetime |
| High mass comfort, core activation, durability prestige | Low-carbon concrete variants + KPP/calibrated foundations; disclose: cement-site supply chain, delivery monitoring |
| Wet rooms, moisture exposure | Mineral/clay pairs; avoid gypsum↔cement contacts (ettringite), watch material-compatibility |

### 13.2 Insulation / envelope choice

| Condition | Move | Boundary |
|---|---|---|
| GK ≤ 4, hygroscopy desired, grey energy first | wood fibre / cellulose / reed / hemp (nawaRo, PEI/GWP favourable) | fire class + MVV TB generic exclusions ⚠; moisture construction discipline |
| GK 4–5, erdberührt, WDVS cost | EPS/MW/PUR; MW A1 non-comb; check HBCD legacy & recyclability honestly | WDVS ≠ circular: separable-system trials exist (Aufdopplung retrofit variant) |
| Denkmanl / no exterior change | interior insulation (calcium silicate / wood-fibre foam) | hygrothermal transient proof (WUFI-class), Wohnraumverlust, thermal-bridge cascade |
| 2-leaf existing with cavity | blow-in (perlite/MW/cellulose) | control difficulty; outer-skin load check |
| XPS under slab/Perimeter | unavoidable-but-small | highest grey energy per effect — cap thickness, no gratuitous XPS |

### 13.3 Heating-system choice (decision table)

| Situation | Default | Then |
|---|---|---|
| New build, any sensible envelope | HP (air-water; ground/ GW where plot/permits/payback fit) + PV + (battery or thermal store) | DH if municipal plan says it's efficient/cheaper/required; bivalent only with load-curve proof |
| Retrofit ≥1995, panel rads | HP mono/parallel, flow ≤55 | hydraulic balance, buffer, noise proof first |
| Retrofit 1978–95 | HP bivalent-alternative (switchover ~50 % load), old IGUs + roof first | envelope before plant per §6.3 |
| Pre-1978 / HT emitters, listed shell | Hybrid (HP + existing boiler) or pellet where envelope cannot reach the band; DH connection where offered | direct electric only behind the envelope gate + PV logic; avoid HT-HP |
| Very high DHW/vent loads (hotel, canteen, school) | DH or CHP-with-buffer (KWK base-load sizing, load-duration curve) or Abluft-WP | plant-room/MFeuVO + noise duties apply (see building-services-tga) |

### 13.4 Envelope standard, PV, and storage ladder

- Ladder: GEG-legal → EH55 → EH40 (+QNG) → EH40-plus → plus-Energie/ Aktivplus —
  stop where marginal envelope cost + grey energy exceeds saved B6 + subsidy delta;
  on most plots PV+HP beats adding the next ladder rung.
- PV: ≥ roof-logic kWp from load base; battery only after self-consumption layout;
  Mieterstrom/§42b for multi-owner; parking PV + GEIG where applicable.

## 14. Carbon-accounting quick template (per m²BGF; T4 by design — flag uncertainty)

**Purpose:** early-phase variant steering and honest "about" numbers. Not a
substitute for an EPD-based Ökobilanz; state "±30–50 % typical error" and the module
scope every single time the output leaves the chat.

### 14.1 Workflow

1. Set scope: A1–A3(+A4/A5 with default allowances) per m²BGF; exclude D and
   recarbonation credits unless specifically justified; note 50-a frame.
2. Take-off quantities per m²BGF from the model (concrete m³, steel t, masonry m³,
   timber m³, insulation m³, glazing m², gypsum m², roof m²…).
3. Apply the digested factors (14.2; swap in product EPDs the moment real ones
   exist — same structure).
4. Sum per material → kg CO₂e/m²BGF; split "storage" (biogenic, negative) from
   fossil so the reader can see both conventions.
5. Operation line: Q_H kWh/(m²a) × fuel factor (g/kWh) × 50 a (or discounted ladder)
   + PV credit at grid factor; present separately (never "offset" into the material
   score without saying so).
6. LCC line at shadow price chosen per section 3.4; disclose which.
7. Uncertainty note: EoL scenario, grid path, factor vintage, missing layers
   (transport, fit-out, TGA) — enumerate.

### 14.2 Factor set (A1–A3 unless noted; T3/T4 ⚠ VERIFY with EPD)

| Item | Factor |
|---|---|
| Concrete C25/30 standard / optimized | 178–200 / ~130 kg CO₂e/m³ |
| Unreinforced/lean | 60–80 kg CO₂e/m³ |
| C30/37 L1–L4 CSC | 183 → 131 kg CO₂e/m³ |
| Reinforcing steel | 0.3 (EAF)–0.7 (BF) t CO₂e/t |
| Structural steel sections EAF | 0.3–0.7 t/t (+ fire coating systems ⚠ case) |
| Masonry (KG/m³): KS / brick unfilled / filled / AAC / clay / RC-concrete wall | 227 / 113 / 146 / 166 / 94 / see concrete |
| KVH / BSH / CLT / OSB | −712 / −650 / −632 / −565 kg CO₂e/m³ (biogenic incl.) |
| Aluminium profile, primary / 75 % secondary | high ⚠ / secondary ≈ 5 % of primary energy (GWP needs power-mix factor) |
| Glazing (float, per m² typical 2-pane ≈ 25–35 kg CO₂e/m² ⚠ not cleanly digested) | use product EPD |
| Insulation: EPS/XPS/PUR vs MW vs wood fibre | per EPD; PEI ladder: synthetic high grey, mineral mid, nawaRo lowest (T4) |
| Transport A4 | ~0.1 kg CO₂e/(t·km) road (T4 plausibility) |

### 14.3 Worked example (compact 4-storey MFH, 800 m² BGF, concrete+brick+timber variant, T4)

Assumed quantities/m²BGF (plausible bands for the type, **not measured here**):
RC 0.11 m³ → 20 (optimized: 14); steel 9 kg → 6 (EAF: 2.7); masonry 0.11 m³
(unfilled brick) → 12; timber (roof/inner) 0.03 m³ → −19 (storage); insulation wood
fibre 0.04 m³ → ~2–4 ⚠EPD; gypsum/render/misc → 6; windows+door elements → 8 ⚠;
A4/A5 +10 %; C/D excluded. Result A1–A3 ≈ 35–40 + 10 % ≈ **~40–45 kg CO₂e/m²BGF
"small-structure-only" fraction**, typical all-element totals land in the 200–400
band (section 4.3). Operation at 45 kWh/(m²a) gas × 201 g × 50 a ≈ 450 kg CO₂e/m² —
note the ratio: even today's "green" concrete is dwarfed by 50 years of gas; with HP
on today's grid ≈ 45 × 0.434 × 50 ≈ 975 → ×(1/3) ≈ ~325; with 2045 grid ≈ <100.
Conclusion the template must force: structure choice cuts the rising share, the
heating system cuts the still-dominant one, and the honest answer is "both, this
year, with these caveats".

## 15. Greenwashing pitfalls (claim → reality check)

1. "Klimaneutrales Haus / CO₂-freier Zement" — valid only for A1–A3, often only after
   offsets; check biogenic/fossil split and D-module games; no product is
   climate-neutral across A1–D with current data.
2. "DGNB Platin = climate-ready" — top certificates do not guarantee the 2045/2050
   pathway (digest explicit); check the CRREM/taxonomy fit, not the plaque.
3. Art. 8/9 funds "sustainable" — only 39 % (Art.8) / 67 % (Art.9) of EU funds showed
   a verifiable CO₂-reduction contribution in one 2024 analysis (⚠ dated); demand the
   data fields (consumption, EPC, pathways), not the label.
4. "Timber stores CO₂" — storage is only locked if the loop (reuse/recycling) is
   designed; under default incineration C4 the balance flips positive (declare
   scenario both ways).
5. "Recyclingbeton spart CO₂" — the aggregate loop saves raw material, not carbon
   (paste demand can rise); credit recarbonation only per DIN EN 16757 with module
   boundaries stated.
6. "Green premium guarantees value" — office premiums (+6–8 % rent, +14–16 % value,
   CBRE-2023 line) are market-conditioned, dated ⚠; stranded-asset risk (CRREM) can
   outrun the premium.
7. "Wiederverwenden ist immer besser" — compute the reuse case vs industrial
   recycling (transport, re-certification, failure risk); for some streams (glass,
   wood panels, concrete fines) recycling currently wins.
8. "PV liefert 20× seine graue Energie" — true as life-cycle average, not as annual;
   winter yields, storage and grid autonomy still need HP/DH back-up (Jülich LLEC
   lesson: even full roof+façade PV cannot secure continuous supply).
9. "Dämmung spart bis zu 50 %" (WDVS line) — real only with flawless execution and
   maintenance; defective WDVS <10 a life destroys the B6 case.
10. "Effizienzhaus 40 plus = Null-Emission" — plus standards count exported energy;
    check the primary-factor convention (Strom 1.8→1.5 flips "green" rankings).
11. Insulation without thickness check vs grey energy; solar promise without roof
    statics/fire/permits; "regional" claims without transport computation (Hessen
    47 km average already emits 4 % of a state's forest uptake).
12. Certification point-chasing that standardises away architecture ("billige Punkte
    vs Seele") — set outcome targets first (Phase 0), let the certificate follow them.
13. Sufficiency-free narratives: any "green new build on greenfield" story without
    the Bestand/density question answered (EFH per-capita land/resource outlier;
    commuter +1.4 t/capita·a) is incomplete, whatever its EPC.
14. "Nachhaltigkeit" as a bolt-on consultant in LPH 5–8: influenceability lives in
    Phase 0/LPH 1–2 — late consultants can only re-verify, never rescue (section 3.3).
15. ESG-data theatre: portfolio CO₂ numbers without meter coverage (Mieterstrom data
    gaps), unverified extrapolations, or no external review — ask for the data model
    (BMS submetering, GEFMA-style criteria, CSRD/ESRS fields) before trusting any
    "green portfolio".

## 16. Checklists (phase-wise; the agent's working discipline)

### 16.1 Phase 0 / Bedarfsplanung (DIN 18205, HOAI LPH 0–1)

- [ ] Five client strategies (climate, planning/procurement, use, maintenance, recovery) written down
- [ ] Target metrics fixed: kg CO₂e/(m²·NRF·a), energy standard, certification (or explicit "none + why"), LCC horizon + shadow price
- [ ] Bestand/density/sufficiency questions answered (reuse? conversion? program size? parking key? compactness A/B, A/V)
- [ ] Funding/finance requirements (QNG, taxonomy, Green-Lease data) checked before design freeze
- [ ] Regulatory-economics layer re-verified at project date: taxonomy screening values (36.9 kWh/(m²a) PE-nren, 90/70 % quotas), Mieterstrom/§42b tariff + metering conditions, CRREM stranding date (3.5) ⚠ VERIFY
- [ ] Phase-0 climate roadmap per district/plot (municipal heat plan, PV duty, radon/soil hazards ⚠)
- [ ] Sustainability coordinator + physics/structure/TGA integration from day 1
- [ ] Design-freeze and change-impact (LCA re-run) procedure defined

### 16.2 Planning (LPH 2–5)

- [ ] Variants compared with the 4-objective method (12.1) + disclosure blocks (12.4)
- [ ] Structure: material per 13.1; cement class (L2/L3) + unreinforced measures + RC where regional; KPP/calibrated foundations; steel/timber joints reversible
- [ ] Envelope: ≥50-a parts for seals/fixings; water-first details; nawaRo↔fire-class check (GK); insulation thickness vs grey-energy crossover; U **and** GWP per wall
- [ ] Systems: passive→semi-passive→active; simulation-sized plant; HP source feasibility + noise; PV base-load sizing; storage decision; DH/network priority
- [ ] IAQ/health: product emission classes, no SVHC>0.1 %, low-formaldehyde boards, biocide-free façades, radon/soil file ⚠, legionella concept (60 °C), ventilation plan (DIN 1946-6/EN 16798)
- [ ] Comfort: summer proof (shading+mass/night purge), daylight ≥1/8 NRF + autonomy, acoustic standard contracted above DIN 4109 minimum, accessibility concept
- [ ] Circularity: DfD details, sortenrein layering, separation tests, material registry fields from BIM, Rückbau-/Pre-Demolition concept drafted, reuse-lot candidates identified
- [ ] LCA runs planungsbegleitend (generic → EPD), hotspots re-checked at each freeze; eLCA/public tool parity if federal/funded
- [ ] LCC: annuity comparison with energy/CO₂ price scenarios; maintenance access designed; cycle tables (B2–B4) populated
- [ ] Bio-based/clay spec checked against 5.8 limits: Hanfkalk non-loadbearing + fire class, clay water/frost protection + FK/GK ceiling, paludiculture products via ZiE, current ÖKOBAUDAT/EPD entry and biogenic-C convention ⚠ VERIFY

### 16.3 Execution + commissioning (LPH 6–9)

- [ ] Tender embeds GWP ceilings + eco criteria + documentation duty; EMAS/ISO 14001 suitability gates
- [ ] Delivery verification: the low-carbon cement actually poured; FSC/recyclate certificates collected; material-ecology supervision (product releases, sample checks, IAQ/biobiotic measurements, blower door)
- [ ] Site circularity: sorted capture (GewAbfV), Rückbaukonzept executed, salvage register (re-use items off-site value documented)
- [ ] Lean/quality: rework = emissions — progress monitoring; DGNB-site-variant if funded
- [ ] Inbetriebnahme: fine-tuning/Einregulierung, BMS with all meters, EE plants with nominal performance + maintenance docs, Feinabstimmung after occupancy, FM onboarding
- [ ] User instruction: Lüftungsfibel, hygrometers, low-tech operating reality, deviations from norm communicated/contracted
- [ ] As-built data handover: material registry / Gebäuderessourcenpass, EPD archive, circularity + pollutant data in CAFM-ready formats

### 16.4 Operation / exit

- [ ] Data: submetering, target-actual, GEFMA-160-style PDCA, CRREM refresh, ESG-report fields (CSRD/ESRS-ready if in scope)
- [ ] Quick wins first (pumps, LED, controls, hydraulic balance); retrofit roadmap (Modernisierungsfahrplan) with stranding date
- [ ] Repair-before-replace verified; tenant/occupant programmes for behaviour savings (energy-literacy gaps are the cheapest kWh)
- [ ] At end-of-life: Pre-Demolition Audit (DIN SPEC 91484), salvage-first ordering R3–R7, sorted deconstruction, residual-value exit (registry) — feed the next Phase 0

## 17. Crib sheet (single-glance numbers; all T3/T4 ⚠ unless marked T1/T2)

CARBON PRICE: BEHG 45 €/t ·2024; UBA 237 €/t (2022) / 250 €/t (2023, ZPR 1 %) / 809 €/t
(0 %); BW binding 250 €/t. (T1 state-specific)
OPERATION FACTORS g CO₂e/kWh: oil 266 · gas 201 · grid elec 434 (2022) · gas 1820 g/m³ ·
HP@JAZ3 ≈ 145 · fp: fossil 1.1, wood 0.2, DH-CHP 0.7 (ren. 0.0), Strom 1.8→1.5 GModG ⚠,
own PV/ambient 0, feed-in credit 2.8. (T2 set with ⚠ editions)
STRUCTURE kg CO₂e/m³: concrete 178–200 (130 opt., 60–80 nb) · CSC L3 ~107–163 ·
rebar 700/t (300 EAF) · KS 227 · brick 113/146 · AAC 166 · clay 94 (−198 air-dried) ·
KVH −712 · BSH −650 · CLT −632 · hemp-lime −130 · glass 12.6 GJ/t.
WOOD: ~1 t CO₂/m³ stored; harvest 5.7 kg/Fm; savings vs mineral 30–45 % (meta 42.7 %).
CEMENT: clinker factor ~0.67; ~530 kg/t; ⅔ process/⅓ energy; SCM: FA ≤35 %, GGBS ≤80 %,
SF credit ≤11 %; k = 0.4/1.0; CSC −30…−60 %; recarb ~40 % clinker-CO₂/life (EU ≤23 %),
B1 credit only.
RC CONCRETE: ≤45 Vol.-% T1 up to C30/37 (DAfStb), first re-use approvals C20/35 GK ≤4
⚠; RGK 13.3 % of aggregate; >90 % C&D "recovered", <1 % component reuse.
QUOTAS: KrWG ≥70 % (2020) T1 · taxonomy ≥90 % substantial / ≥70 % DNSH T1 ·
DE waste 54–55 % C&D; soil reuse = biggest stream.
GE/GEBÄUDE duties: Qp ≤0.55·Ref · H′T ≤ Ref (0.25–0.45) · ref U 0.28/0.20/1.3 ·
existing 0.24(0.35)/1.3(1.9) · GA class B ≥290 kW · LCA duty 2028 (>1000 m²)/2030
(all) · NZEB 2028/2030 · IAQ metering + HVAC inspection >70 kW · solar duty staged.
HEAT LADDER: stock 200–270 (1980) → ~130 (today) → 40–60 (GEG) → 15 (PH); EH = % of
Ref; KfN EH40+QNG; retrofit rate 0.69 %→≥2 % needed.
HP: COP air ~3.3 / ground ~4.2; SPF 2.7–4.6; ≤55 (50) °C flow; economic when Strom
≤3× Brennstoff; night noise ≤35 dB(A); R290; age-fit ≥1995/78–95/pre78 hybrid;
borehole ~20 m/kW; air market 85 %.
PV: 30°S 904–1040 kWh/kWp (PR 0.8); winter 25 %; mono 4–5 m²/kWp; vert façade
−20–40 %; li-ion 80–90 %, 5–10 kWh homes; Mieterstrom ≥10 % below Grundversorgung.
LCC: operation >80 % · opex ≈ capex in ~7 a (⚠) · seals/screws 25 a → 50 a ⇒ 2× ·
windows 40–50 a · WDVS 40–60 (<10 if bad) · brick 150 · galvanising >50 · floor
example 6.1/9.2/9.8 €/m²a.
HEALTH (T1): SVHC 0.1 % · HCHO 0.06 mg/m³ · VOC1A/1B 0.001 mg/m³ · mould 12.6 °C/80 % ·
DHW ≥60 °C · CO₂ 0.1 Vol% (Pettenkofer) · radon 300 Bq/m³ ⚠ VERIFY (not digested).
COMFORT: summer ≤28 °C op · mass activation 25–30/30–40 W/m², comfort −2 °C air ·
daylight ≥1/8 NRF, dimming −30–75 % · DIN 4109 min; contract VDI 4100 II/III.
URBAN: A/B 67 % vs 121 %; commuter +1.4 t/capita/a, 7–8× sealing; 52 ha/day land;
parking space saved ≈ 12.7 t CO₂e; beech 12.5 kg/a.
POLICY FRAMES: 2045/2050 neutrality · KSG −65/−88 % · CSRD 250 MA/€25M/€50M ·
taxonomy 6 goals+DNSH · SFDR 6/8/9 (39 %/67 % verified ⚠) · CRREM stranded dates ·
GHG scopes 1/2/3 (SBTi >40 % → mandatory targets) · EPBD 2024/28/30 dates ⚠.

---

*End of skill. Every ⚠ VERIFY is load-bearing: re-check current GEG/GModG annexes,
funding rates, EPD values, MVV TB/MBO editions, radon and taxonomic detail, and the
project's own quantity take-off before any number leaves the planning aid and enters
an offer, permit file, certificate submission, or public claim.*
