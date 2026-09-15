---
name: building-renovation-refurbishment
description: >
  Bausanierung/Modernisierung (component-level building renovation and refurbishment)
  for DACH residential/small-commercial practice: Bestandsaufnahme and Sanierungskonzept
  workflow (Bauzustandsstufen BZS 1–4, checklist-driven survey, HOAI Leistungsphasen
  fee shares, DIN 276 Kostengruppen, "konventionell vs. behutsam" comparison method);
  building-fabric repair by component — Naturstein restoration (weathering/salt/frost
  damage catalog, Mohs test, consolidation), Beton/Stahlbeton Instandsetzung (DIN EN
  1504 protection/repair principles 1–11 with RM/RC/SRM/SRC material classes,
  reinforcement passivation), Metallbauteile (corrosion classes DIN EN ISO 12944,
  contact-corrosion pairing table, Titanzink/Coil-Coating roofing), Bauteile im
  Erdreich (DIN 18533 water-exposure classes, horizontal/vertical Mauerwerksentfeuchtung
  methods with cost/lifespan comparison, DIN 4095 drainage), Fassade/Mauerwerk
  (historic brick formats, U-value tables per wall build-up, WDVS/Innendämmung
  trade-offs, Klinkerriemchen systems), Dächer (Aufsparren-/Zwischensparren-/
  Untersparrendämmung, Kalt-/Warmdach, Gründach layer build-ups, Dachgeschossausbau),
  Decken/Fußböden (balcony-head repair, DIN 18534 wet-room waterproofing, impact-sound
  decoupling), Feuerungsanlagen/Schornsteine (lining/cross-section-adaptation methods),
  Treppen (DIN 18065 geometry for retrofit stairs), Fenster/Türen/Tore (historic
  profile repair vs. replace, RC burglary classes, GEG component U-max table Anlage 7),
  Fugen (DIN 18540 sealants/bands), Putze/Beschichtungen (Sanierputz WTA, mortar groups
  DIN EN 998-1); renovation-specific energetic retrofit (GEG § 46–56 Bestand duties,
  Nachrüstpflichten, thermal-bridge surcharges, energy-standard ladder Altbau→Passivhaus);
  ecological material selection and pollutant screening for existing buildings;
  renewable-energy retrofit integration constraints; selective deconstruction/Rückbau
  sequencing; bautechnischer Artenschutz (species-protection duties triggered by
  renovation permits — bats, swifts, nesting season); renovation-specific contract/
  liability points (BGB/VOB Mangel remedies, HOAI, Sicherheiten) plus an ÖNORMEN
  supplement. Use for "renovate this house", "Altbausanierung", "modernize/refurbish
  a building", "what to do with this old facade/roof/basement", "adapt an existing
  building/BIM model for renovation" — load alongside `existing-structures-retrofit`
  (structural condition assessment/Nachrechnung engineering), `timber-building-renovation`
  (deep historical-timber diagnosis/repair), `building-physics-thermal-moisture` (GEG
  calculation methodology), and `sustainable-construction` (LCA/circularity figures) —
  this skill supplies the renovation-specific survey/repair/execution layer, not a
  duplicate of those skills' numbers.
---

# Building Renovation & Refurbishment (Bausanierung) — DACH Practice Skill

> **Simple-first gate (governs how this skill is applied).** Default every renovation
> choice to the *simplest proven, substance-preserving* repair at the agreed standard
> tier — see the governing skill `simple-first-building` (complexity ladder §1). A
> "behutsame Sanierung" (careful/substance-preserving repair) that keeps functioning
> historic fabric is the default; a "konventionelle Sanierung" (wholesale strip-and-
> replace) is the escalation, justified only by genuine irreparability, explicit
> client request, or a code-driven Nachrüstpflicht — not by habit or trade convenience.

Agent-neutral reference for renovating and refurbishing existing residential and
small-commercial buildings in DACH practice: how to survey a building before touching
it, how to decide repair-vs-replace per component, and the concrete repair techniques,
numbers and standard citations for the building fabric itself (masonry, stone,
concrete, metal, roof, floors, openings, joints, renders, coatings). It sits one layer
below `existing-structures-retrofit` (which owns the structural-engineering assessment
and Nachrechnung machinery) and one layer above the physics/materials/services skills
it repeatedly hands off to.

**Primary sources.** Distilled from *Bausanierung* (Stahr, Hrsg., Springer 2022) and
*Sanierung von baulichen Anlagen* (Stahr, Springer 2019) — both DACH-practice compendia
covering assessment through execution for building-fabric renovation. Timber-specific
historical construction, damage diagnosis and repair sits in the companion skill
`timber-building-renovation`, sourced from *Holzbausanierung beim Bauen im Bestand*
(Lißner/Rug, Springer 2023) — use that skill for anything beyond the brief timber
overview in §4 here.

## 0. Reality check and the [VERIFY] convention

This skill produces **planning-stage renovation guidance**, not construction-ready
detailing. Before any of it is built:

1. A **Bausachverständiger/Architekt/Tragwerksplaner** must survey the actual building —
   every number here is a typical/illustrative value from the source literature, not a
   substitute for on-site Bestandsaufnahme.
2. **Denkmalschutz** (heritage protection), where it applies, overrides default repair
   choices in this skill — always check with the Untere Denkmalschutzbehörde before
   planning irreversible interventions on a protected building.
3. **Current legal/normative texts prevail.** DIN/EN editions, GEG duties, and
   Landesbauordnung requirements change; every cited edition date is the one the source
   literature used and must be re-verified against the current text before use in a
   report or calculation.
4. Anything flagged **[VERIFY]** is a figure the source gave without a traceable current
   normative citation (superseded EnEV-era numbers, historic cost figures, manufacturer
   claims) — treat as illustrative order-of-magnitude only, re-derive from the current
   standard or a current price book before using it in a real project.

Use this skill when the task involves ANY of: surveying an existing building before
renovation, choosing repair vs. replace for a building component, planning a
"behutsame" vs. "konventionelle" Sanierung, sizing an energetic retrofit measure at
component level, sequencing a demolition/selective-deconstruction, checking
species-protection duties before starting work, or adapting a FreeCAD/BIM model of an
existing building to emulate a renovation (see `construction-freecad-bim` §
"Renovation & retrofit modeling").

## 1. Bestandsaufnahme & Sanierungskonzept

### 1.1 What "Sanierung" covers, and how it differs from Modernisierung

- **Sanierung** = primary Rohbau measures needed to restore original Standsicherheit
  and Funktions-/Betriebsfähigkeit.
- **Modernisierung** = secondary Ausbau measures needed to meet *current* use
  expectations (a building can be "saniert" without being "modernisiert").
- Typical named sub-sanierungen: Kellersanierung (vertical/horizontal damp-proofing),
  Mauerwerksanierung, Fenstersanierung, Dachsanierung, Deckenbalkensanierung,
  Betonsanierung, energetische Sanierung, Asbestsanierung — each routes to a §
  below.

### 1.2 Bauzustandsstufen (BZS) — condition classification

| BZS | Average wear | Rating |
|---|---|---|
| 1 | 0–10 % | Sehr gut |
| 2 | 11–25 % | Gut |
| 3 | 26–50 % | Befriedigend |
| 3/4 | 51–80 % | Mangelhaft — unqualified continued use becomes questionable at this stage |
| 4 | 81–100 % | Ungenügend |

Time spent in a BZS is driven by preventive Instandhaltung; regular upkeep is the
single biggest lever on a building's economic life beyond the often-cited ~90-year
Bestandsdauer assumption used in financial guidelines [VERIFY — check current
Afa/valuation guideline].

### 1.3 Component life expectancy (planning reference, DIN-adjacent survey table)

Use for renovation lifecycle costing (component due for replacement now vs. still
inside its expected life). Ranges, not guarantees — actual life depends on execution
quality, exposure and maintenance.

| Component | Material | Years |
|---|---|---|
| Innenputz (Wand) | KM/KZM/ZM | 90–100 |
| Holzfußboden | Weichholz / Hartholz | 40–60 / 100 |
| Außenputz | KM/KZM / Edelputz | 40–60 / 50–60 |
| Holzfenster | Weichholz / Hartholz | 40–80 / 50–80 |
| Dachdeckung | Ziegel / Faserzement / Betondachstein / Stahlblech verzinkt / Kupferblech / Bitumenbahn | 90–110 / 70–80 / 40–50 / 25–30 / 90–100 / 6–10 |
| Rinnen/Fallrohre | Stahlblech verzinkt / Zinkblech / Kupferblech | 15–20 / 40 / 90–100 |
| Vertikalabdichtung | Heißanstrich (Bitumen) | 15–40 |

### 1.4 Schadensverursacher — where renovation-triggering defects come from

Roughly even split across Planer, Bauausführende, Nutzer (varying source estimates
20/30/50 % by group); Bauausführung alone accounts for >40 % of documented defects.
**By exposure**: the weathered building envelope (Außenwände, Dächer, Fenster) accounts
for ≈61 % of defects/mängel; including erdberührte Bauteile brings the whole envelope
to ≈78 %.

### 1.5 The Bestandsaufnahme sequence

1. **Object survey**: walk every room including Dachboden/Keller; open windows/doors,
   test switches and taps, knock on timber elements, note humidity/mould smell/
   creaking floors.
2. **Baugeschichtliche Daten**: Erbauungszeit, ownership history, prior Umbaumaßnahmen
   and their materials, plan/facade changes, prior use changes — cross-check against
   `existing-structures-retrofit` §3 for the deeper archival/testing programme when
   structural re-verification is also in scope.
3. **Document**: notes, sketches, photographs (including detail shots — not video/
   Polaroid); compare against surviving Bauakten, Schnitte/Risse, old photos.
4. **Interview**: prior owners, neighbours, authorities.
5. **Decide the Wohnwertstandard**: the two governing decisions in any renovation are
   the Sanierungsverfahren and the target comfort standard — a simple standard is not
   the same as poor quality/execution (this is the `simple-first-building` default
   made concrete). Define priorities deliberately: raising standard in one area (e.g.
   modern TGA) can justify reducing effort elsewhere (e.g. minimal Kellersanierung) —
   see §1.7.

### 1.6 Participants and authorities to clear before planning

Bauherr, Planer (bauvorlageberechtigt, usually Architekt), Fachplaner/Statiker,
Bauaufsichtsbehörde, Stadtplanungsamt, Denkmalschutzbehörde (untere, at
Gemeinde/Kreis level — first point of contact for protected buildings),
Brandschutzbehörde (for changes to Brandwände/Rettungswege/Dachausbau/Holztreppen),
Gewerbeaufsichtsamt (commercial use). Clear scope and constraints with these *before*
detailed planning to avoid costly re-work.

### 1.7 Konventionelle vs. behutsame Sanierung — the method choice, worked by component

This is the single most consequential decision axis in this skill. The source
literature tabulates it component-by-component; the pattern generalizes:

| Component / damage | Konventionell (strip & replace) | Behutsam (substance-preserving) |
|---|---|---|
| Kellermauerwerk, defekte Sperrung | Full excavation, new horizontal/vertical seals, Sanierputz throughout | Assess whether a "dry" cellar is actually required for the intended use; ventilate instead; clean and leave brick unplastered to allow drying |
| Kellerfußboden, nasse/uneben Ziegel | Strip, new gravel + concrete slab (fully sealed) | Clean and re-lay the original brick in a sand bed — preserves the "evaporation cellar" function |
| Kastendoppelfenster, feuchtegeschädigt | Demolish, replace with new insulated-glass units | Repair timber damage (Wetterschenkel, Rahmen), refit hardware, mill in gasket grooves, fit insulating glass in the existing sash |
| Hauseingangstür, feuchtegeschädigt | Replace with new plastic/aluminium door | Restauratorische Instandsetzung: new matched timber inserts, protective coating, refurbished hardware |
| Straßenfassade Putz/Stuck/Naturstein | Strip all render, dispersion-paint refinish, ornament in GRC/EPS replicas | Strip only loose render; repair with historically matched breathable (lime) render; reconstruct missing ornament in matching material; sheet-metal flashing at sills/cornices |
| Dachdeckung, teilweise defekt | Full strip and re-roof | If no loft conversion planned: "Nachstecken" of missing tiles, clean tiles, renew mortar pointing at ridge/valley |
| Alte Fußböden (Dielung/Parkett) | Partial removal, dry-screed floating floor system | Repair, infill and sand the existing boards/parquet, finish with breathable wax/oil/lacquer |
| Innenputz | Full strip and re-plaster | Consolidate sound breathable render, patch only damaged areas with matching material |
| Stuckdecken | Clad over with plasterboard or EPS profiles | Strip old paint carefully, repair stucco, refinish with washable glue/casein paint |
| Holzschutz, Schädlingsbefall | Remove affected timber, chemically treat all remaining timber and adjacent masonry | Remove affected timber; maximize *constructive* wood protection (detailing that keeps timber dry) to avoid unnecessary chemical treatment; reuse sound reclaimed timber |

The behutsame column is the `simple-first-building` default; the konventionell column
is the escalation and should be priced and justified explicitly, not defaulted into.

### 1.8 Sanierungswürdigkeit — go/no-go documentation

State explicitly whether the object is **sanierungswürdig** or not, and whether works
can proceed safely with the building occupied. Flag supporting reports still needed:
Holzschutzgutachten, Schallschutzgutachten, hydrologisches Gutachten,
Baugrundgutachten.

### 1.9 Planning process and fees (HOAI)

Renovation planning follows the same 9 HOAI Leistungsphasen (LP) as new build, split
into planning (LP 1–5) and execution support (LP 6–9). A ~20 % surcharge on the base
fee is customary for Modernisierungsvorhaben at Altbauten [VERIFY current HOAI
edition — the 2013 percentage table below is illustrative of proportion, not current
minimum/maximum fee law, which has changed since the 2019 EuGH ruling, see §11].

| LP | Leistung | Share of total fee (%) |
|---|---|---|
| 1 | Grundlagenermittlung | 3 |
| 2 | Vorplanung | 7 |
| 3 | Entwurfsplanung | 11 |
| 4 | Genehmigungsplanung | 6 |
| 5 | Ausführungsplanung | 25 |
| 6 | Vorbereitung der Vergabe | 10 |
| 7 | Mitwirkung bei der Vergabe | 4 |
| 8 | Bauüberwachung | 31 |
| 9 | Objektbetreuung | 3 |

A careful Kostenschätzung (LP 2 Grundleistung) achieves roughly ±5 % accuracy when
quantities are itemized properly — undercutting planning fees to "save money" on a
renovation reliably costs more in downstream Baukostenerhöhung than the saved
planning fee.

### 1.10 Cost structure (DIN 276)

Renovation costs are grouped exactly as new-build costs, per DIN 276 (2018-12)
Kostengruppen (KG): 100 Grundstück, 200 Herrichten/Erschließen, 300 Bauwerk-
Baukonstruktionen, 400 Bauwerk-Technische Anlagen, 500 Außenanlagen, 600 Ausstattung/
Kunstwerke, 700 Baunebenkosten. See `cost-management-din276` for the full unit-price
buildup methodology — this skill only flags which renovation measures land in which
KG for budgeting purposes.

### 1.11 Historical materials for repair-in-kind

| Category | Typical historic materials |
|---|---|
| Holz | Fachwerk, hand-adzed/sawn Gebälk, floorboards, parquet, panelling, doors/windows, stairs |
| Naturstein | Foundations, window/door surrounds, arches, paving, troughs, columns, stairs |
| Keramik | Steinzeug, Klinker, Ziegel, Terrakotta, Fayence, tiles, roof coverings, tile stoves |
| Metall | Fittings, locks, hinges, window grilles, gates, weathervanes |

Selecting a genuinely ecological repair material means checking actual toxicity/
emission data, not the marketing words "natural" or "biological" — e.g. fired brick is
not "natural" (its chemistry is transformed by firing), and granite, though a natural
stone, can carry meaningful indoor radon risk from its radioactivity. Cross-ref
`building-materials` and `sustainable-construction` for the full material property/LCA
tables — this skill flags the renovation-specific selection question, not the
underlying data.

## 2. Naturstein-Restaurierung (natural stone)

### 2.1 Weathering mechanisms and damage patterns

| Process | Mechanism | Typical damage |
|---|---|---|
| Chemische Verwitterung | Carbonate breakdown in acidic conditions; gypsum/salt formation; microbial attack | Absanden (sanding), Absprengungen (spalling), Rissbildung, Gipskrustenbildung |
| Physikalische Verwitterung | Frost-thaw cycling, salt crystallization, thermal cycling, wind erosion, hygroscopic swelling/shrinkage | Krusten-/Schalenbildung, Rissbildung, Gefügelockerung |
| Biologische Verwitterung | Lichen/bacteria/algae acid production | Discoloration, greening, root damage |

Damage catalog: Absanden/Abmehlen, Aushöhlungen/Alveolarbildung, Schalen-/
Schuppenbildung, Rissbildung, Verfärbungen, Ausblühungen, Anlösungsstrukturen,
Verschmutzung/Krustenbildung.

### 2.2 Common causes and remedies (selection)

- **Absanden/Abmehlen** (esp. tonig-gebundene Sandsteine): unsuitable for exterior use
  in acidic-emission areas if calcareous; protect from over-wetting; treat with dilute
  Kaliwasserglas (potassium silicate) solution after dry brushing, following
  Voruntersuchung.
- **Absprengungen**: from water/aggressive-substance ingress at poorly detailed
  cornices/sills; avoid plastic/tin/zinc capping that traps moisture — use
  constructive detailing (correct falls, drip edges) instead; use stainless or
  galvanized steel ties bedded in plasticized/lead mortar to avoid rust-jacking.
- **Ausblühungen**: from rising ground moisture (sulfates/chlorides/nitrates) or from
  SO₂/CO₂ atmospheric attack on calcareous stone; prevent moisture ingress
  (Sperrschicht/Elektroosmose); dry-brush existing efflorescence after drying.
- **Durchfeuchtung**: without a damp course, moisture can rise up to ~2 m above grade;
  sealing the *outside* face can drive moisture *higher* — remedy is freeing/venting
  the wall base, perimeter drainage, and inserting a Sperrschicht, not just external
  sealing.
- **Krustenbildung/Treiben**: combustion-derived CO₂/SO₂ attack calcareous stone,
  forming porous crusts that continue to destroy substance underneath — remove and
  apply object-appropriate protection after removal, don't just leave crusts in place.

### 2.3 Hardness reference (Mohs, field test)

| Mohs | Mineral | Field test |
|---|---|---|
| 1–2 | Talc/Gypsum | Scratches with fingernail |
| 3–4 | Calcite/Fluorite | Scratches with copper coin / knife easily |
| 5–6 | Apatite/Feldspar | Scratches with knife / steel file |
| 7–9 | Quartz/Topaz/Corundum | Scratches window glass |

### 2.4 Bestandsaufnahme for stone — question checklist

Origin and date of the element; how long at its current location; special material/
working characteristics; prior alterations or treatments (what, when, with what);
constructive integration (removable?); tool marks/artistic finishing present;
surface/edge features from working; render/paint layers present and their condition;
significance to the monument as a whole; whether damage requires specialist
restoration treatment.

### 2.5 Repair technique thresholds

- **Vierung** (replacement insert, "four right-angle edges"): minimum 10 cm edge
  length, minimum 8–11 cm embedment; must not bridge existing joints or change the
  joint pattern; produced and set by a trained Steinmetz.
- **An-/Aufspachtelung** (mineral/resin/silica-gel-bound repair mortar): only once
  whole-stone or Vierung repair is no longer economical, or the defect area is
  ≤80 cm²; follow manufacturer processing instructions closely (spalling risk); cut
  back to sound substrate; trial panels before contract award.
- Naturstein-specific standards: designate stone strictly per **DIN EN 12440**
  (petrographic family, colour, structure, texture, technical grade, quarry origin) —
  trade names alone are not a reliable specification.

Full Bestandsaufnahme/Untersuchung methodology (probes, lab tests, standort factors,
Immissionsbelastung) is covered in the source at length and mirrors
`existing-structures-retrofit` §3's material-testing programme — use that skill's
testing catalog for anything beyond stone-specific field identification here.

## 3. Beton- und Stahlbeton-Instandsetzung

### 3.1 Governing framework (current)

Since 01.01.2009, **DIN EN 1504** ("Products and systems for the protection and
repair of concrete structures") applies alongside the DAfStb Richtlinie
"Schutz und Instandsetzung von Betonbauteilen" (RiLi SIB); as of 2021 the DIBt
Technical Rule **"Instandhaltung von Betonbauwerken" (TR Instandhaltung)** largely
supersedes RiLi SIB and should be used together with DIN EN 1504 going forward.
Historic material classes (pre-EC2 DIN 1045 generations back to 1904) for dating and
assessing existing reinforced concrete are covered by `existing-structures-retrofit`
§4 — do not re-derive them here.

### 3.2 Protection and repair principles per DIN EN 1504 (the decision framework)

| Principle | Purpose | Methods (selection) |
|---|---|---|
| 1 | Schutz gegen Eindringen von Stoffen | Hydrophobierung, Versiegelung, Beschichtung, Rissbandagen, Rissfüllung, Rissumwandlung in Dehnfugen, Vorsatzplatten, Membranen |
| 2 | Regulierung des Wasserhaushalts | Hydrophobierung, Versiegelung, Beschichtung, Vorsatzplatten, elektrochemische Behandlung |
| 3 | Betonersatz | Mörtelauftrag von Hand, Querschnittsergänzung durch Betonieren, Spritzverfahren, Bauteilaustausch |
| 4 | Verstärkung des Betontragwerks | Zusatz-/Austauschbewehrung, Verbundlaschen, Querschnittsergänzung, Riss-/Hohlraumverpressung, nachträgliche Vorspannung |
| 5 | Erhöhung des physikalischen Widerstands | Beschichtung, Versiegelung, Mörtel-/Betonauftrag |
| 6 | Erhöhung des Chemikalienwiderstands | Beschichtung, Versiegelung, Mörtel-/Betonauftrag |
| 7 | Erhalt/Wiederherstellung der Passivität | Betondeckungserhöhung/-teilersatz, Ersatz von chlorid-/karbonatisiertem Beton, Realkalisierung durch Diffusion |
| 8 | Erhöhung des elektrischen Widerstands | (elektro-physikalisch) |
| 9 | Kontrolle kathodischer Bereiche (Cathodic Control) | Begrenzung Sauerstoffgehalt an der Kathode durch Sättigung/Beschichtung |
| 10 | Kathodischer Schutz (Cathodic Protection) | Anlegen eines elektrischen Potenzials — see `existing-structures-retrofit` for KKS detail |
| 11 | Kontrolle anodischer Bereiche (Control of Anodic Areas) | Anstrich der Bewehrung mit aktiv pigmentierten Beschichtungen |

Principles 1–6 apply to damage *not* linked to carbonation-/chloride-driven
reinforcement corrosion; where corrosion *is* the driver, use principles 7–11
instead (§3.3). The TR Instandhaltung selects the subset of DIN EN 1504's methods
that suit predominantly handwerklich execution for the most common damage patterns;
DIN EN 1504 itself is broader (including specialist/contested electro-physical
methods) — pick the simpler TR Instandhaltung path unless the damage genuinely needs
the extra machinery.

### 3.3 Material classes used across the repair principles

Repair materials are specified per **DIN EN 206-1 / DIN 1045-2** (Beton, incl.
Trockenbeton), **DIN EN 14487 / DIN 18551** (Spritzbeton), and the DAfStb
Vergussbetonrichtlinie for Verguss applications, using the abbreviation classes
RM/RC (repair mortar/concrete), SRM/SRC (sprayed repair mortar/concrete), PRM/PRC
(polymer repair mortar/concrete, i.e. polymer-bound rather than cementitious repair
material), F-I/F-V (Füllen durch Injektion/Füllen durch Vergießen — fill by
injection/fill by casting, suffix P=plastic-elastic, H=hard/rigid).

### 3.4 Damage-cause chain (why reinforced concrete fails)

- Manufacturing-stage defects → target Festbetoneigenschaften not met → reduced
  bond strength / load capacity from the outset.
- Reinforcement corrosion → loss of Tragsicherheit of the element — the dominant
  in-service damage mechanism; diagnosis and γM treatment for the re-check sit in
  `existing-structures-retrofit` §4.

### 3.5 Instandsetzungskonzept workflow

1. Orientierende Begutachtung → 2. Untersuchungsplanung → 3. Bestands- und
Schadensaufnahme → 4. Objekt-/Laboruntersuchungen → 5. Auswertung → 6.
Sanierungskonzept. This mirrors the Bestandsaufnahme sequence in §1.5 and the
structural condition-assessment sequence in `existing-structures-retrofit` §1 —
run them as one combined survey on a real project rather than three separate visits.

## 4. Holzkonstruktionen (brief — see `timber-building-renovation` for depth)

This section is a bridging summary only. Historical timber typologies, connection
identification, fungal/insect damage diagnosis, residual-strength assessment and the
full repair-technique catalog (splicing, resin consolidation, Fachwerk/Umgebindebau
specifics) live in `timber-building-renovation`; EC5 sizing of new or replacement
members lives in `timber-steel-design`.

- **Tierische Schädlinge** (Holzwurm, Hausbock): bore galleries, producing Holzmehl,
  reducing cross-section capacity.
- **Pflanzliche Schädlinge** (decay fungi): Hausfäule, Blätterschwammfäule,
  Kellerschwamm, and the most dangerous — **Echter Hausschwamm** (Serpula
  lacrymans), which develops in enclosed damp spaces and can spread its mycelium
  through masonry across an entire building.
- **Steel corrosion adjacent to timber**: unprotected embedded steel that rusts
  changes its section modulus, reducing load capacity — check steel-timber
  interfaces (beam shoes, straps) during any timber survey.
- Constructive wood protection (details that keep timber dry) is preferred over
  chemical treatment wherever the detail can be fixed — see §1.7's Holzschutz row.

## 5. Metallbauteile

### 5.1 Corrosion basics and material groups

Per **DIN EN ISO 8044** (formerly DIN 50900): corrosion is surface-originating
destruction of a metal by unintended chemical/electrochemical reaction with the
environment. Building-relevant groups: unalloyed steels (RC/steel construction),
high-alloy steels (corrosion-resistant cladding), cast iron (drainage, radiators),
aluminium alloys (lightweight cladding/roofing), zinc/galvanized steel and copper
(roofing, gutters, downpipes — copper especially on sakral buildings).

### 5.2 Corrosion protection classes

**DIN EN ISO 12944-2** defines corrosion protection classes for atmospheric (C) and
water/soil (Im) exposure — specify the class from actual exposure, not by habit.

### 5.3 Contact corrosion — metals/materials to keep apart

| Metals/materials in contact | Reaction | Fix |
|---|---|---|
| Eisen/Stahl + Kupfer/Messing | Eisen/Stahl corrodes | Separate; coatings; stainless fixings |
| Eisen/Stahl + Gips | Contact corrosion at fixings, gips discolours | Stainless fixings, continuous welded/soldered seams |
| Eisen/Stahl/Kupfer + Holz | Metal corrodes, timber discolours | Stainless or Cr/Sn/Ni-plated steel fixings |
| Aluminium/Zink + alkaline materials (lime, cement) | Aluminium/Zink corrodes | Replace zinc with Titanzink; barrier coatings |

### 5.4 Metal roofing/facade renovation

- **Titanzink** (alloyed zinc per **EN 988**, ≥99.995 % electrolytic Feinzink) is the
  standard renovation roofing metal: low thermal expansion, reduced cold-brittleness,
  good workability regardless of rolling direction, recrystallization only above
  ~300 °C (important for soldering). Sheet thickness generally >0.8 mm for
  aesthetic/durability reasons.
- Modern Colordachrinnen use coil-coated aluminium (RAL/NCS colour systems),
  temperature-stable −30 °C to +80 °C, quality-controlled via salt-spray and
  weathering tests.
- Facade cladding fixings: undersized/too-thin washers, over-torqued screws, and
  mismatched fastener dimensions are the dominant *planning* failure modes for
  panel/cassette facades (not material defects) — press-hole clearance of ~2 mm for
  rivets accommodates thermal movement.
- Sanierung von Schornsteinmauerwerk: reline with cement-bound Ausschleifmasse or
  Ausziehmasse (with/without inner glaze); service life ≈60+ years brick, 30–40
  years steel liners [VERIFY current product data].

## 6. Bauteile im Erdreich (below-grade components)

### 6.1 Water exposure classification

**DIN 18533** "Abdichtung erdberührter Bauteile" defines Wassereinwirkungsklassen —
but note the standard's boundary conditions are largely tailored to new build; a
genuinely norm-conform Bestand retrofit is rarely achievable in practice, so WTA
Merkblätter (Referat 4, Mauerwerk/Bauwerksabdichtung) govern most real renovation
design, with DIN 18533 consulted mainly for classifying the water exposure and for
vertical sealing systems.

### 6.2 Foundations and frost depth

Flachgründung (Einzel-/Streifen-/Plattenfundament): must sit below the frost line —
typical German frost depth **0.80–1.20 m**; foundations shallower than ~80 cm risk
frost-crack damage.

### 6.3 Horizontal Mauerwerksentfeuchtung — method comparison (illustrative costs [VERIFY current price book])

| Method | Applicability | Cost (per m², wall 60–80 cm)[VERIFY] | Lifespan | Notes |
|---|---|---|---|---|
| Maschinelle Mauertrennung | Natural stone/brick, feuchtebelastet | ≈300 €/m² | 40–50 yr | Watch for Gewölbeschub |
| Handmauertrennung | As above, tighter access | ≈500 €/m² | 30–50 yr | Settlement-crack risk |
| Einrammen von Edelstahlblechen | Continuous-joint brick | ≈400 €/m² | 20–50 yr (salt-dependent) | Vibration-crack risk |
| Injektion drucklos | Universal | ≈200 €/m² | 10–25 yr | Distribution hard to verify; can raise salt load |
| Injektion Niederdruck/Hochdruck | Stone/brick | ≈250 €/m² | 10–25 yr | Higher reliability than drucklos |
| Elektroosmotische Verfahren | Per Herstellerangaben | ≈700 €/m² | ~10 yr | Contested in the profession; passive variants have essentially no evidence base |

Injection bore spacing per WTA guidance (10–12.5 cm) is not universally validated by
reproducible research — spacing must be matched to actual absorption behavior,
achieved Durchfeuchtungsgrad, injection medium and method rather than applied
mechanically.

### 6.4 Vertical sealing systems (by DIN 18533 part)

- **Teil 2** (Bitumen-/Polymerbitumenbahnen): all water-exposure classes with the
  correct bahn/Bauart; aarRdT-conforming; harder to apply on heavily profiled walls.
- **Teil 3** (PMBC — kunststoffmodifizierte Bitumendickbeschichtung, formerly KMB —
  and mineralische Dichtungsschlämmen MDS): suited to structured/profiled walls;
  needs a suitable protective layer over the seal.
- **Flexible polymer-modified thick coating (FPD)**: increasingly used, faster
  rain-resistance, but not yet covered by current DIN text — agree its use with the
  client explicitly.
- A vertical seal alone reduces the water-absorbing erdberührte area by **up to 80 %**
  and can be sufficient on its own for low-grade-use cellars, avoiding a horizontal
  seal entirely.

### 6.5 Drainage

**DIN 4095** (1990, due an update to match the 2017 Abdichtungsnorm [VERIFY]) governs
Dränanlagen — sized on Bemessungswasserstand, site conditions and soil.

### 6.6 Freestanding walls / verdunstungszone strategy

Where a horizontal seal is not economical, accepting an evaporation zone at the wall
base combined with a **Sanierputzsystem** (sacrificial render, 3–15-year maintenance
cycle [VERIFY]) is often the more economical, equally durable choice.

## 7. Fassaden – Mauerwerk – Wände

### 7.1 Historic brick format and wall build-up

Normalformat (NF) full brick ≈ 24 × 11.5 × 7.1 cm, joints 1–2 cm. A typical 1½-brick
wall (~40 cm incl. render):
Außenputz 2.0 cm + Vollziegel 1 Stein 24.0 cm + Fuge 1.0 cm + Vollziegel ½ Stein
11.5 cm + Innenputz 1.5 cm ≈ **40 cm total**, R ≈ **0.49 m²K/W** as-built (unimproved).

### 7.2 U-values by wall thickness/insulation (DIN 4108 reference table, illustrative)

| Wall (cm) | With 40 mm Isolierklinker | With 74 mm | With 94 mm | With 114 mm |
|---|---|---|---|---|
| 24 | 0.78 | 0.44 | 0.35 | 0.29 |
| 30 | 0.74 | 0.43 | 0.34 | 0.28 |
| 36 | — | — | 0.28 | 0.24 |

U in W/(m²K); outer render 2.0 cm Kalkzementputz, inner 2.0 cm Kalkputz [VERIFY
against current manufacturer/standard data — illustrative of *magnitude*, not a
design table].

### 7.3 Damage diagnosis chain (structured survey)

Follow the six-step method: 1. Orientierende Bauwerksbesichtigung → 2. Bestands-/
Schadensaufnahme (Anamnese) → 3. Untersuchungsplanung → 4. Untersuchungen vor Ort/im
Labor → 5. Bewertung/Diagnose → 6. Instandsetzungsplanung. Classify findings by
symptom (Oberfläche vs. Querschnitt vs. Formänderung vs. Durchfeuchtung) crossed with
cause (mechanical, moisture-source, frost, settlement, war damage, ageing) crossed
with the underlying Mangel (inadequate foundation, inadequate waterproofing,
inadequate thermal bridge control, etc.) — the source's Problemstellung/Ursache/
Mangel matrix is the template for a defensible Schadensgutachten.

### 7.4 Repair technique selection

The method depends on **wall material** (soft brick vs. hard granite need different
approaches), **Durchfeuchtungsgrad** (>50 % complicates sawing and reduces injection
uptake), and **static conditions** (horizontal thrust at a vault foot or from
retained earth can rule out mauertrennende methods entirely — the propping cost
would exceed the method's value). See §6.3 for the horizontal-seal method
comparison.

### 7.5 Rissinstandsetzung

- Widen the crack, prime edges with a consolidating impregnation, fill with an
  elastic organically-bound fine mortar (silicone-resin spachtel) for active/moving
  cracks.
- For structural crack repair with re-plastering: strip render ~20 cm either side,
  decouple with a separating layer, add a wire-mesh Putzträger, apply render in two
  layers.
- Injektionsleim for filling/pressure-grouting crack runs and voids; Rissspachtel
  for cosmetic near-surface sealing of fine cracks; spiral-anchor systems for
  force-transmitting flank connection across facade/masonry cracks.

### 7.6 Innendämmung (interior insulation — the fallback where facade character must be kept)

- A diffusion-open, capillary-active interior insulation buffers indoor humidity
  spikes and speeds winter drying, reducing mould risk versus a diffusion-tight
  system.
- Typical premium system λ ≈ 0.031 W/(mK); do not tape/wallpaper the inner face —
  finish with a mineral, diffusion-open coating only.
- Where facade ornament (Gesimse, Fenstergewände, Bauzier) or Denkmalschutz rules
  out exterior insulation, interior insulation is often the only remaining path to
  meaningfully improve thermal performance — but watch **Holzbalkenköpfe** embedded
  in the wall: interior insulation lowers wall temperature at the embedment, and
  sustained timber moisture content above ~20 % risks fungal decay there. Detail the
  balcony-head zone specially (see §9.3) rather than insulating through it uniformly.

### 7.7 Klinkerriemchen / Isolierklinker facade renovation systems

Thin-brick-faced insulation panels (EPS core + ~17 mm real clinker facing, tongue &
groove + Überfalz jointing, stainless fixings) — U-values e.g. 25 mm insulation ≈
1.07 W/(m²K), 60 mm ≈ 0.53 W/(m²K), 80 mm ≈ 0.40 W/(m²K) [VERIFY current product
range]. A renovation-scale alternative to full WDVS where a masonry-look facade must
be kept.

### 7.8 Standards index for this section

DIN 1053-1 (Mauerwerk), DIN 4108 (Wärmeschutz), DIN 18195/18533 (Bauwerksabdichtung),
DIN EN 771 (Mauersteine), DIN EN 1996/EC6 (Mauerwerksbemessung — see
`masonry-construction` for design), DIN V 18599 (energetische Bewertung), WTA
Referate 1/3/4/6/8 (Holz/Naturstein/Mauerwerk/Bauphysik/Fachwerk).

## 8. Dächer (roofs)

### 8.1 Insulation position — three systems

Aufsparrendämmung, Zwischensparrendämmung, Untersparrendämmung — pick by objective
constraint (sparren height, whether timber stays exposed internally, whether the
roof is being fully stripped anyway), not by habit:

- **Aufsparrendämmung**: continuous homogeneous insulation layer, best thermal/
  acoustic/fire performance, protects the structure from thermal stress and
  moisture, rational to install (all layers worked from above on a continuous
  substrate), suitable for both new build and retrofit (installable without
  disturbing the interior), integrated as a "second roof" for water management.
- **Zwischensparrendämmung**: full sparren depth available for insulation
  (advantageous where sparren height is limited); moisture/airflow only safe if the
  inner Dampfbremse is executed with full care — an equivalent thermal-resistance
  comparison: 0.16 m Holzfaserplatte (λ=0.040) ≈ 0.10 m PUR (λ≈0.025), both giving
  U≈0.25 W/(m²K).
- **Untersparrendämmung**: supplementary layer under the sparren, e.g. via a
  Dämmkeil system filling old sparren fields with a hinterlüftung gap ≥2 cm
  maintained; typical performance WLG 035/040, non-combustible (A1 per DIN 4102),
  water-repellent via hydrophobing.

### 8.2 Ventilated vs. unventilated roof

- **Kaltdach** (ventilated): Durchlüftungsraum between insulation and Unterdach must
  be **40–80 mm** (sparren-length/pitch dependent); between Unterdach and covering,
  **≥45 mm**; Dampfbremse minimum diffusion resistance R_D ≈ 2 m²hPa/mg.
- **Warmdach** (unventilated): preferred over long spans, at complex geometries,
  windy/exposed sites, or over extremely cold spaces where a Kaltdach's function
  would be compromised; full sparren depth available for insulation; airtightness
  depends entirely on a carefully executed inner air/vapour barrier.

### 8.3 GEG-era U-value targets (component method, Altbau context)

Roof retrofit U-target ≈ **0.30 W/(m²K)** (Altbau minimum) to **0.22 W/(m²K)**
(Neubau/Bauteilverfahren) or better, tunable by insulation thickness and position
(Aufsparren + interior layer combinations) [VERIFY against current GEG Anlage 7 — see
§16 for the current statutory table].

### 8.4 Flachdach types

Umkehrdach (insulation above the seal, using closed-cell non-absorbent insulation —
typically EPS — with the seal itself acting as the vapour barrier; installation is
largely weather-independent and the seal is protected from thermal cycling, but
rainwater flowing under the insulation can cause lateral heat loss);
begehbar/befahrbar/begrünt variants per intended use.

### 8.5 Gründach (green roof) build-up

| Vegetation type | Layer thickness |
|---|---|
| Moos-Sedum (flat roof) | 5–8 cm |
| Moos-Sedum-Kraut | 8–12 cm |
| Gras-Kraut | >15 cm |

Roof pitch ≤20° for adequate light on the north side; extensive greening retains
**50–70 %** of annual precipitation on site (can reduce stormwater fees); keep
plants ≥50 cm from penetrations/edges via gravel or paving strips; run edge
upstands ≥15 cm.

### 8.6 Dachgeschossausbau (loft conversion) checklist

Planning-law headroom: GFZ/GRZ overrun, Denkmalschutz constraints, Stellplatz-
nachweis, Abstandsflächen, Rettungswege; technical: Diagnose des Dachwerks
(construction type, load capacity, pest-freedom), Tragfähigkeit of the supporting
structure/floor/masonry, access (stair widening if only an Einschubtreppe exists),
TGA routing, and daylighting — Musterbauordnung minimum window area is **1/10 of the
room's net floor area** in most Länder (older rule: 1/8) [VERIFY current
Landesbauordnung]; DIN 5034-1 recommends the transparent window area reach **≥55 %**
of the room's width for a genuinely daylit result, well above the statutory minimum.

### 8.7 Dachdeckendämmung (top-floor ceiling insulation)

Insulate **from above** wherever possible (insulating from below reduces clear
ceiling height and is more disruptive). Dämmmaßnahmen at the Dachdecke must not
reduce impact-sound performance — do not simply swap existing Schüttung fill for
insulation without checking the acoustic consequence. This duty (top-floor-ceiling
or roof insulation, whichever is warmer-side) is one of the GEG's standing
Nachrüstpflichten — see §16.2.

### 8.8 Standards index

DIN 4102 (Brandverhalten), DIN 18531 (Dachabdichtungen), DIN 4108 (incl. Teil 10
insulation-product short codes, e.g. `040 DAD dm` = Wärmeleitfähigkeitsgruppe/
Dach-Deckendämmung/mittlere Druckbelastbarkeit), DIN EN 13162 (Faserdämmstoffe), DIN
EN 12056 (Flachdachentwässerung).

## 9. Decken und Fußböden

### 9.1 Construction types found in Bestand

Stahl: Stahlbetonplatten auf/zwischen Stahlprofilen. Stahlbeton: Platten,
Stahlsteindecken, Rippendecken, Fertigteildecken. Holz: Vollholzbalken, verleimte
I-Balken. Gewölbe/Kappendecken: Mauerziegel/Beton auf Mauerwerk or between
Stahlprofilen.

### 9.2 Survey method for timber balcony/joist decks

Lift a **30–40 cm** strip of flooring at the external walls (removing 2–3
floorboards is usually enough width) and inspect every Balkenkopf in the loft and in
moisture-risk zones — freeing the bearing area for inspection. **Spot checks are not
sufficient** for a defensible renovation-scope decision; every accessible bearing
needs checking.

### 9.3 Balkenkopf (joist-end) repair options

- Anlaschen: side or underside timber splints/laminations bolted to the sound
  section of a worn beam.
- Prefabricated steel elements (e.g. paired U-profiles) for stiffening/supplementing
  capacity.
- Replacing the bearing section (the Balkenkopf itself) with reinforced synthetic
  resin.
- See `timber-building-renovation` for the residual-strength assessment that
  precedes choosing between these.

### 9.4 Acoustic performance

Geschossdecke below **350 kg/m²** areal weight needs added impact/airborne-sound
measures. A schall bridge as small as ~1 cm² of render contact between screed and
masonry wall can cut sound insulation by **≈3 dB** — decouple floor build-ups from
walls cleanly at every renovation.

### 9.5 Wet-room waterproofing

Horizontal seals (rising damp, splash zones, sanitary areas) follow **DIN 18533**
(e.g. slabs) and especially **DIN 18534** (Abdichtung von Innenräumen) plus ZDB
Merkblätter. DIN 18534's sheet-/panel-bonded systems used with tile/slab finishes
are the more contested part of the standard — treat as needing case-by-case
judgement; liquid-applied systems (dispersion, reaction resin, mineral
polymer-modified) are the uncontested aarRdT choice. On a timber-joist floor (bath
etc.), prefer **DIN 18534 Teil 2 or 3** given the expected deflection under use.

### 9.6 Standards index

DIN 4108 Teil 2/7 (Wärmeschutz/Luftdichtheit), DIN 4108 Beiblatt 2 (Wärmebrücken),
DIN 4159 (Ziegel für Ziegeldecken), DIN 18533/18534, DIN 4109 (Schallschutz), WTA
4-3-98 (Instandsetzung von Mauerwerk), WTA 4-5-99 (Mauerwerksdiagnose).

## 10. Feuerungsanlagen und Schornsteine

### 10.1 Governing framework

MFeuV (Musterfeuerungsverordnung) plus each Land's Feuerungsverordnung; GEG;
1. BImSchV; Landesbauordnung; DIN V 18160-1 (Abgasanlagen — Planung und
Ausführung), DIN EN 1443, product standards DIN EN 13229/13240; schornstein sizing
per **DIN EN 13384-1** (single feuerstätte) / **-2** (multiple).

### 10.2 Efficiency reference by Feuerstättentyp (planning order-of-magnitude)

| Type | Typical efficiency |
|---|---|
| Offener Kamin, Bauart A | ~30–60 % |
| Offener Kamin, Bauart B | ~8–20 % |
| Heizkamin | ~75 % |
| Kaminofen/Raumheizer (per DIN EN 13240) | ≥50 % norm minimum, up to ~80 % closed operation |
| Grundofen | ≥76 % |
| Warmluftofen | Lower (heavily convective, less efficient use of fuel energy) |
| Speicherofen/-kamin (Austrian type) | typically >78 %, up to ~90 % per Herstellerangaben [VERIFY] |

### 10.3 Schornstein renovation methods

- Relining with cement-bound Ausschleifmasse or Ausziehmasse (with/without inner
  glaze) for masonry chimneys — mortar group IIa repair mortars, prewet
  strongly-absorbent brick, avoid accelerators/retarders in the mix, avoid working
  in rain, maintain full joints (~1 cm Stoßfuge, ~1.2 cm Lagerfuge).
- Querschnittsanpassung is increasingly needed because modern condensing/low-
  temperature boilers produce cooler, wetter, lower-volume flue gas than the
  chimney's original masonry-era design assumed — verify against the *actual* new
  Feuerstätte's data, not the chimney's age/original sizing.
- **LAS-Systeme** (raumluftunabhängig): concentric stainless inner tube (0.6 mm,
  DN113–350) inside the existing shaft — needed where facade airtightening has cut
  off the combustion-air supply a room-air-dependent appliance needs.
- Mehrschalige Keramikschornsteinsysteme with Hinterlüftung suit condensing gas/oil
  appliances (<100 °C flue gas, glazed liner below 60 °C); AT-Keramikrohre (rated to
  ~650 °C sustained, surviving ~1000 °C chimney-fire spikes) suit solid-fuel
  appliances.
- Kunststoff-/Polyabgasleitungen suit low-temperature (condensing) appliances,
  flue-gas temperature capped at ≤160 °C, corrosion-free, retrofittable into
  existing masonry shafts, and convert an under-pressure (Sog) chimney to
  over-pressure operation as required by low-temperature/condensing technology.
- Any schornstein alteration needs **Schornsteinfegermeister** sign-off before and
  after — a Bauantrag/Bauanzeige may also be required.

## 11. Treppen (stairs — renovation-relevant subset)

See `stairs-vertical-circulation` for full new-build geometry design; this is the
renovation-repair-relevant subset:

- **DIN 18065** governs Gebäudetreppen geometry. Comfortable residential range:
  Steigung 160–180 mm, ideal 170 mm; Auftritt ideal 290 mm (Bequemlichkeitsregel
  A−S≈120 mm, subordinate to the Sicherheitsregel A+S=460±10 mm and Schrittmaßregel
  A+2S=630±30 mm / 590–650 mm per DIN 18065).
  Existing-stair tolerance: step-to-step deviation ≤5 mm; no averaging tolerance is
  permitted below the code minimum/above the code maximum.
- Lichte Durchgangshöhe ≥2.00 m (Musterbauordnung and DIN 18065).
- Typical renovation repair menu: strip and refinish, Aufdopplung of worn
  Trittstufen, metal/plastic nosing profiles at tread edges.
- Timber stair member sizing found in Bestand (planning reference, not a design
  rule): Trittstufen 3.5–6 cm, Setzstufen 2–4 cm, Wangen 5–7 cm (eingeschoben/
  eingestemmt) or 7 cm (aufgesattelt).
- Geländer: openings ≤12 cm; a Knieleistengeländer (if used at all) needs its top
  rail inclined ≥15 cm inward to deter climbing. Handlauf height 80–115 cm
  (ergonomic optimum ≈90 cm), grippable width 2.5–6.0 cm, extending ≈30 cm past the
  first/last step.

## 12. Fenster, Türen, Tore

### 12.1 Repair vs. replace — the default decision

Most timber-cased double windows (Kastendoppelfenster) and panelled doors can be
repaired rather than replaced: refurbishment is usually cheaper (no incidental
Maurer-/Malerarbeiten, no change to the surrounding building physics) and an old,
slightly imperfect timber unit can still deliver another century of service — a new
DIN-standard unit's actual service life is unproven by comparison. Repair menu:
strip old paint, replace only damaged timber sections, adjust hardware, mill in
gasket grooves in the inner sash, fit insulating glass into the existing frame.

### 12.2 GEG component U-max table (Anlage 7, current — use these, not the historic EnEV figures elsewhere in this skill)

| Component | Wohngebäude / Zonen ≥19 °C | Zonen 12–<19 °C |
|---|---|---|
| Außenwand (Ersatz/Erstmaliger Einbau) | U = 0.24 W/(m²K) | U = 0.35 |
| Außenwand (Bekleidung/Putzerneuerung) | U = 0.24 | U = 0.35 |
| Fenster/Fenstertüren | U_w = 1.3 | U_w = 1.9 |
| Dachflächenfenster | U_w = 1.4 | U_w = 1.9 |
| Vorhangfassade | U_c = 1.5 | U_c = 1.9 |
| Außentüren | U = 1.8 (Türfläche) | U = 1.8 |
| Dach/oberste Geschossdecke/Abseitenwände | U = 0.24 | U = 0.35 |
| Wand/Decke gg. Erdreich, unbeheizt | U = 0.30 | keine Anforderung |
| Verglasungsersatz allein | U_g = 1.1 | keine Anforderung |

[VERIFY the current GEG edition/Anlage numbering — cited here from GEG 2020, Anlage
7; the exemption for changes affecting ≤10 % of a Bauteilgruppe's area, and the
Nachrüstpflichten of §47/§72, are covered in §16.]

### 12.3 Historic timber window profiles

**DIN 68121-1** fixes Holzfensterprofile (Blendrahmen, Flügelrahmen, Pfosten,
Riegel, Sprosse dimensions) — match new/replacement sections to it when
reconstructing a historic profile. Replaceable gasket profiles (not weather-exposed
in a well-detailed frame) are mandatory for long-term serviceability.

### 12.4 Security (Einbruchhemmung)

**DIN EN 1627** defines resistance classes RC 1N–RC6 (superseding the older WK1–WK6
scale). From **RC 2** upward, the combination of Sicherheitsverglasung + certified
Beschlag is mandatory; RC1N/RC2N need no security glass. Glazing classified per
**DIN EN 356**: durchwurfhemmend P1A–P5A, durchbruchhemmend P6B–P8B (axe-strike
count to breach a 400 mm square).

### 12.5 Condensation at window reveals

Tauwasser at the lower Glashalteleiste of a modern insulated-glass unit is
**expected and permitted** under **DIN 4108-2** normal-climate assumptions
(φ_i=50 %, θ_i=20 °C) — it is not automatically a defect. Ensure convective heat
reaches the glass (radiator below the window, no continuous horizontal sill
shelving) to minimize it in practice; this matters most at Dachflächenfenster.

### 12.6 Tore

**DIN EN 13241** (Tore-Produktnorm) and **DIN EN 12424** (Windlast) govern garage/
industrial door renovation and replacement.

### 12.7 Standards index

DIN 4108 (Wärmeschutz), DIN 4109-1 (Schallschutz — outdoor noise level per
Lärmschutzkarte/Nomogramm/measurement, elevated requirements near airports/rail/
Schnellstraßen), DIN 18008 (Glas im Bauwesen), DIN 18101 (Türen Wohnungsbau), DIN
18355/18357/18360 (VOB Teil C Tischler-/Beschlag-/Metallarbeiten), DIN 18545
(Verglasungsabdichtung), DIN EN 12207/12208 (Fugendurchlässigkeit/
Schlagregendichtheit).

## 13. Fugen (joints)

### 13.1 Framework

**DIN 52460** defines Fugen and related terms; **DIN 18540** governs
Außenwandfugendichtstoffe (excludes Gas-/Schaumbeton joints, erdberührte joints, and
Bewegungsfugen — those need different systems).

### 13.2 Geometry rules

Fugenflanken must run parallel to a depth **t = 2b** (minimum 30 mm) to give the
backfill material adequate grip; arris edges chamfered **a > 10 mm** to reduce
Umläufigkeit risk. Total dichtstoff deformation (compression + extension) capped at
**25 %** of the joint width at 10 °C. Minimum joint width **15 mm** at up to 2 m
joint spacing (DIN 18540) — a frequently under-executed figure worth checking during
renovation of defective joints.

### 13.3 Execution discipline

Don't seal above 40 °C substrate surface temperature; work vertical joints top-down
to avoid trapping rainwater behind partially completed seals; multi-component
sealants mixed exactly per manufacturer ratio; apply the sealant only after the
primer's flash-off time (too early traps solvent-condensation moisture under the
sealant, too late exceeds the manufacturer's open time); minimize smoothing agent
use; avoid painting over sealants unless compatibility is lab-confirmed.

### 13.4 Common renovation-specific failure

Gips-based Mauermörtel reacting with mineral Verfugmörtel can cause spalling — check
substrate mortar chemistry (WTA 2-11-07) before selecting a repointing mortar,
especially in older repointing campaigns.

## 14. Putze und Beschichtungen (renders and coatings)

### 14.1 Mortar group framework

Pre-Feb-2005: **DIN 18550 PI–PIV** (no strength requirement tied to the group).
Current: **DIN EN 998-1** classifies Putzmörtel by compressive strength, capillary
water absorption and thermal conductivity instead — composition/binder ratio is no
longer the classifying criterion. Quality levels for interior render finish: **Q1–Q4**
per DIN V 18550 Anhang B (abgezogen/glatt/gefilzt variants).

### 14.2 Sanierputz (salt-laden/damp masonry render)

**DIN EN 998-1** and the WTA Referat "Sanierputz" govern principles/requirements/
execution. WTA-classified Sanierputz systems (1/2/3-WTA) carry defined minimum
compressive-strength-to-water-vapour-permeability ratios — specify the WTA class,
not just "Sanierputz" generically. Illustrative product data point: porenhydropher
Sanierputz, Mörtelgruppe PII (>2.5 N/mm²), minimum coat thickness 10 mm at
chloride/sulfate salt loading, ~10-day careful drying for crack-free curing
[VERIFY current product datasheet].

### 14.3 Wärmedämmputz / WDVS via render

Classed as Wärmedämmputz per DIN 18550/DIN EN 998-1 when calculated thermal
conductivity ≤0.20 W/(mK), equivalent to dry bulk density ≤600 kg/m³. Both layers of
a two-coat WDVS render system must come from one matched Werktrockenmörtel system
(DIN 18557) — mixing manufacturers/systems within one build-up voids the system
warranty and risks incompatibility failures.

### 14.4 Beschichtungen (coatings/paints)

- **DIN 55945** defines Beschichtung/Anstrichmittel/Anstrich terminology.
- Haftfestigkeitsprüfung (adhesion test, **DIN 53151** Gitterschnitt) before any
  re-coat: a new coat does *not* improve a failing old coat's adhesion, and can make
  overall delamination worse — Gt2 or better required; Gt3–5 triggers further
  investigation before recoating.
- Colour specification via **DIN 5033** (Farbmessung) / **DIN 6164** (DIN-Farbkarte,
  Buntton/Sättigung/Dunkelstufe).

### 14.5 Standards index

DIN 18550/DIN EN 998-1 (Putz), DIN EN 13279 (Gipsbinder), DIN 52170 (Druckfestigkeit
Putz), DIN 4108 Teil 5 (Wärme-/Tauwasserschutzberechnung Putz), DIN EN ISO 12944
(Beschichtungssysteme), DIN EN ISO 7783 (Wasserdampfdurchlässigkeit).

## 15. Ökologisches Sanieren und gesundes Bauen/Wohnen

### 15.1 Selection criteria for ecological renovation materials

Positive wellbeing/health effect; low-energy, pollutant-free production; local
(dezentral) production reducing transport; Gleichwertigkeit of requirement vs.
material property (don't over-specify high-energy materials where a simpler one
performs equivalently — the `simple-first-building` principle applied to material
choice); regenerability at eventual demolition.

Evaluate across the whole chain: raw-material extraction impact, production
emissions/waste, processing emissions, in-use emissions (toxic substances,
lung-penetrating dust, fibrous carcinogens like asbestos, radioactive emission from
some stones — e.g. granite's natural radioactivity can raise indoor radon), and
end-of-life behaviour (EAK/European Waste Catalogue classification, recyclability,
deconstruction cost). Cross-ref `sustainable-construction` for the full LCA/EPD
methodology and GWP figures — this skill only flags the renovation-material
selection question and pollutant screening.

### 15.2 Pollutant/health screening before renovation

Screen for: fibres (Asbest, künstliche Mineralfasern/KMF), schwer-flüchtige
substances (PCP, DDT, PCB, PAK, Weichmacher, Formaldehyd), leicht-flüchtige
substances (VOC, MVOC, Isocyanate), Baugrund-Radon, Schwermetalle (Blei), and
biological hazards (Legionellen, Schimmelpilz). Match method to hazard:
Auflichtmikroskopie (fibres), Gaschromatografie/Massenspektrometrie
(schwer-/leicht-flüchtig), Abklatsch-/Wischproben, Staubanalysen,
trocken-/nasschemische Analyse.

### 15.3 Combined survey structure (all disciplines in one pass)

Run architektonisch-konstruktiv, statisch-konstruktiv, abdichtungstechnisch,
energetisch, schalltechnisch and Gefahrstoffe strands together as one coordinated
Bestandsaufnahme campaign (matching §1.5/§3.5's sequence) rather than as separate,
uncoordinated site visits.

### 15.4 Energy-standard ladder (context for setting the renovation target)

| Standard | U opaque (W/m²K) | U window (W/m²K) | Max Jahresheizwärmebedarf |
|---|---|---|---|
| Altbau (WSVO 1977) | 1.4 | 5.2 (Einfach-/Doppelfenster) | 280–180 kWh/m²a |
| WSVO 1995 | 0.8–0.6 | 1.8–3.1 | 100–54 kWh/m²a |
| Niedrigenergiehaus | 0.4–0.2 | 1.3 | 70–50 kWh/m²a |
| Passivhaus | <0.15 | <0.7 (Fenster gesamt), U_f ≤0.75 | <15 kWh/m²a |

Passivhaus design detail: opaque U typically targeted ≈0.10 W/(m²K) (better than the
<0.15 threshold), window U_w/D_U ≤0.8 W/(m²K), airtightness n50 <0.6 h⁻¹, PHPP
(based on EN 832) as the governing balance tool [VERIFY current PHPP/EN edition —
EN 832 is a superseded reference, current practice uses EN ISO 52016-1 methodology].
This table is historical-context scaffolding for judging *how far* a renovation
target sits from current statutory minima — always design to the current GEG figures
in §16, not to this ladder's numbers directly.

## 16. Energetische Sanierung (GEG, renovation-specific layer)

*Calculation methodology (U/Ψ-value derivation, Glaser diagrams, n50 measurement)
lives in `building-physics-thermal-moisture` — this section covers only the
renovation-specific survey/decision layer that sits in front of that calculation.*

### 16.1 What GEG governs for Bestand

Current German Gebäudeenergiegesetz (GEG, in force since 01.11.2020, replacing
EnEV/EnEG/EEWärmeG) governs — for existing buildings — Energieausweise, minimum
requirements for Modernisierung/Umbau/Ausbau/Erweiterung, minimum requirements for
heating/cooling/ventilation/DHW systems, and periodic AC-system inspection. §2(2):
applies to heated *or cooled* residential buildings occupied ≥4 months/year (or
≥25 % of annual consumption); non-residential buildings with internal temperature
≥12 °C, or heated ≥4 months / cooled ≥2 months. Violations are Ordnungswidrigkeiten
(fine up to €50,000) — e.g. issuing an Energieausweis without qualification,
withholding an existing one, non-compliant Wärmeschutz, false Energieausweis data.
[VERIFY current GEG edition and fine schedule.]

### 16.2 The §48 component-U mechanism (renovation trigger logic)

Any change to a heated/cooled envelope component must not exceed the Anlage 7 U-max
values (§12.2 above) **unless** the change affects ≤10 % of that Bauteilgruppe's
total area — in which case no thermal-performance proof is required for that change
(though §46 still forbids making the *overall* energetic quality worse, and the
DIN 4108-2 hygienic minimum still applies regardless).

Standing **Nachrüstpflichten** (retrofit duties independent of any planned
renovation) include: accessible top-floor ceilings between heated space and
unheated loft must be insulated to U ≤0.24 W/(m²K) if not already compliant with
DIN 4108-2 (satisfied instead by insulating the roof above, per §47); and phased
Heizkessel-Außerbetriebnahme duties for older oil/gas boilers (pre-1991 units, and
post-1991 units once they reach 30 years' service), with exemptions for
low-temperature/Brennwertkessel and units outside the 4–400 kW band. [VERIFY current
GEG §/Anlage numbering before citing in a report — the source predates at least one
GEG amendment cycle.]

### 16.3 Wärmebrücken (thermal bridges) — the renovation surcharge choices

Four compliance routes: (a) detailed proof per DIN V 4108-6 and aarRdT; (b) a
ΔU_WB = **0.05 W/(m²K)** surcharge for normed low-thermal-bridge details per DIN
4108 Beiblatt 2; (c) a flat ΔU_WB = **0.10 W/(m²K)** surcharge with no further
Wärmebrücken proof at all; (d) for Bestand buildings with **interior** insulation on
**>50 %** of the external wall area, a ΔU_WB = **0.15 W/(m²K)** surcharge — this last
route is specifically a renovation case and matters when §7.6's interior-insulation
fallback is used at scale.

### 16.4 Existing-wall survey-to-retrofit worked example (order-of-magnitude, illustrative)

A ~1900-era mehrgeschossiges Wohnhaus with 40 cm Vollziegel walls (as §7.1):
unimproved R≈0.49 m²K/W. To reach GEG U_max≈0.24 W/(m²K) (R_T=4.17 m²K/W) needs
*added* insulation with ΔR≥3.51 m²K/W on top of the existing build-up — **8 cm
WLG 035 (ΔR=2.29 m²K/W) falls short**; **12 cm WLG 030 (ΔR=4.00 m²K/W) clears it**.
Don't average the two trial thicknesses into "8–12 cm is fine" — the added-R
threshold is a hard cutoff, not a range, and undersizing by even 1–2 cm can flip a
compliant build-up into a non-compliant one. This is the kind of back-of-envelope
check to run *before* committing to a WDVS thickness in the
Vorplanung stage; confirm with a full DIN 4108-4 calculation before specifying.

### 16.5 Vor-Ort-Energieberatung workflow

Compare every energetic parameter of the actual Bestand (Ausgangssituation) against
each candidate Sanierungsvariante individually, then compare the variants against
each other — not just against a single "do everything" baseline. This variant-vs-
variant comparison discipline is what lets a client make an informed, staged
retrofit decision rather than an all-or-nothing one.

### 16.6 Energieausweis obligations specific to renovation

A Bestand Energieausweis issued *after* a §48 change must be Bedarfsausweis-based
(calculated, not consumption-based) once the planner has run the full-building GEG
§50 calculation. Validity: 10 years. Renovation, sale, new letting or new leasing all
trigger a fresh Energieausweis requirement if the existing one predates the
transaction by more than the validity window or the building has since changed.
[VERIFY current thresholds — the sourced dates (2008/2009 phase-in) are historical
EnEV-era milestones, not current deadlines.]

## 17. Erneuerbare Energien im Bestand

*Sizing/hydraulics of heat pumps, solar thermal, and system integration live in
`building-services-tga` — this section covers only the renovation-specific
constraints on retrofitting these systems into existing fabric.*

- **Solarthermie retrofit constraints**: roof structural capacity for
  collector/frame loads, pipe routing across existing finishes, junction detailing
  between the collector field and the existing insulation/render (a frequent
  renovation-specific leak point), shading from neighbouring structures/mature
  trees not present when the roof was designed, and available plant-room space for
  the storage vessel (typical domestic storage 300–400 l per §15.4-scale examples
  [VERIFY]).
- **Photovoltaik retrofit**: roughly 10 m² of roof area per kWp of installed
  capacity as a planning rule of thumb; renovation-relevant failure mode is
  penetration/flashing detail at the roof skin — dach-integrated PV variants (tiles,
  shingles, Indach systems) avoid a second penetration layer versus Aufdach mounting
  but complicate future re-roofing.
- **Geothermie/Wärmepumpe retrofit**: shallow horizontal collectors (typically laid
  80–160 cm deep) need garden/site area not always available on a tight urban plot;
  vertical probes avoid the area constraint but need a drilling permit and
  hydrogeological check. See `building-services-tga` for heat-pump flow-temperature
  strategy against existing (often oversized-radiator, high-flow-temperature)
  distribution systems — a genuinely renovation-specific compatibility question.
- **Schornstein interaction**: adding a modern low-temperature heat source
  (heat pump, condensing boiler) to a building with an existing solid-fuel chimney
  often needs the chimney requalified or relined per §10.3, not just the heat
  source swapped.
- **Kachelofen/Pelletheizung retrofit**: modern modular systems (e.g. 5 mm steel
  round-body construction) can be ≥95 % reused/upgraded across a renovation
  generation — worth checking before demolishing an existing masonry stove
  installation outright.

## 18. Abbruch – Abfall – Rückbau (demolition / selective deconstruction)

### 18.1 Scales of Rückbau decision

Strategisch/konzeptionell (Städtebau level — density thinning, partial-area
clearance, edge-inward deconstruction, full Entkernung/Komplettabriss),
technisch/branchenseitig (Hochbau level — this section), wohnungswirtschaftlich
(policy/ownership level). Match the deconstruction *sequence* to which of these
scales is actually driving the decision.

### 18.2 Selective deconstruction sequence (hazardous-materials-led)

1. Collect/sort loose surface waste.
2. Remove asbestos dust hazards.
3. Extract heavy-metal-laden dust from floors/machine parts/pipework/roof
   structures.
4. Dismount production equipment (where applicable — industrial reuse).
5. Extract residual oil from machine parts.
6. Dismount transformer installations, extract cooling fluids.
7. Dismount phenolic-resin-crusted pipework.
8. Remove asbestos-containing gaskets from steam pipework.
9. Chisel out slag/linings from casting vessels/furnaces (industrial only).
10. Core out production halls/workshops.
11. Route out contaminated chimney linings.
12. Mill off heavy-metal-contaminated masonry / oil-contaminated concrete slabs;
    extract the resulting dust.
13. Dismount *contaminated* reclaimed materials (AZ-panels, tar paper, treated
    insulation, impregnated timber) — separately from —
14. Dismount *uncontaminated* reclaimed materials (doors, window glass, gates) for
    reuse.
15. Only then demolish (grab/knock-in/push) the decontaminated, cored-out shell.

The ordering matters: contaminant removal and material-grade separation happen
*before* structural demolition, not as a sort-afterward step — this is what makes
deconstruction genuinely "selective" rather than demolition with a recycling
afterthought. Cross-ref `sustainable-construction` for circularity economics and
material-passport documentation of what's recovered.

### 18.3 Standards/legal index

BNatSchG (species protection during Rückbau — see §19), GEG (energetic duties don't
disappear mid-demolition if part of the building remains occupied), local Bauordnung
demolition-permit requirements.

## 19. Bautechnischer Artenschutz (species protection during renovation)

### 19.1 Why this belongs in every renovation scope

Renovation and roof/facade work routinely destroys nesting/roosting sites for
legally protected species (bats, swifts, house martins, sparrows and others) — this
is a genuine legal constraint on renovation *timing and method*, not an optional
environmental nicety.

### 19.2 Typical affected locations

Hauptgesimsbereich, Drempel (knee-wall void), behind Lüftungslöcher and within the
Außendämmung of Plattenbauten, and window reveals/shutters boxes — survey these
specifically before scaffolding/facade work begins, not after.

### 19.3 Workflow

1. Establish the legal basis and which species/protections apply to the specific
   building and region.
2. Identify nesting/roosting features and species needs at the specific locations
   in §19.2.
3. Assess artenschutz-related cost/risk before pricing the renovation — a required
   mitigation or a seasonal work-timing constraint changes both cost and schedule.
4. Design artenschutzgerechte details for the affected components (replacement
   nest boxes integrated at the cornice, Drempel access panels, etc.) rather than
   simply sealing the openings.
5. Build the argument for client/Denkmalpflege: species-protection features are
   compatible with historic-facade aesthetics and with thermal-bridge-conscious
   detailing when planned in from the start, not retrofitted as an afterthought
   after a wärmebrücken-driven redesign.
6. If deterrence (Vergrämung) rather than accommodation is genuinely necessary,
   use only artenschutzgerecht methods (visual/acoustic/electrical/mechanical, per
   current guidance) and document the legal basis for doing so.

### 19.4 Cross-reference

Schedule constraints from nesting seasons interact directly with
`construction-scheduling-site` sequencing — flag the artenschutz survey as a
schedule-critical early task, not a late-stage permit checkbox.

## 20. Rechtliche Rahmenbedingungen der Bausanierung

*Full contract/permit mechanics (VOB/BGB basics, Bauleitplanung, HOAI
Leistungsphasen, Bestandsschutz grandfathering) live in
`building-regulations-permits` and `existing-structures-retrofit` §2 — this section
flags only the points that are distinctly sharper in a renovation context.*

### 20.1 Zivilrechtliche Grundlagen (contract)

A Sanierungsvertrag needs the same elements as any Bauvertrag: described scope
(here, specifically the renovation scope and its boundary against untouched
existing fabric), referenced documents (Angebot, Verhandlungsprotokoll, LV/LB, ZVB,
BVB, ZTV, VOB Teile B/C), Vergütung, Leistungszeit, Abrechnung/Zahlungsmodalitäten,
Abnahme, Mängelrechtsfolgen, Sicherheiten.

### 20.2 Mangel remedies (BGB/VOB)

Nacherfüllung (§635 BGB / §13(5)Nr.1 VOB/B); Ersatzvornahme auf Kosten des
Unternehmers (§637 BGB / §13(5)Nr.2 VOB/B); Minderung (§638 BGB / §13(6) VOB/B —
where Mangelbeseitigung is unreasonable, especially disproportionately expensive or
impossible); Rücktritt (§636 BGB); Schadensersatz (§636 BGB / §13(7) VOB/B). See
`existing-structures-retrofit` §2 for the § 633 BGB defect-test machinery this
plugs into.

### 20.3 Sicherheiten relevant to renovation contracts

- Vertragserfüllungsbürgschaft: typically capped at **10 %** of contract sum; a
  higher cap in AGB-based contracts is void.
- Mängelansprüchebürgschaft: covers the (often 5-year) Gewährleistungszeit,
  typically capped at **5 %** of the final invoice sum.
- Bauhandwerkersicherung (§650f BGB): owed to the contractor on request, sized at
  the expected remuneration + 10 % Nebenkosten; cannot be contracted away — *except*
  it does not apply to public-sector clients or private clients building/renovating
  their own single-family home. Security cost to the contractor capped at 2 % p.a.
  [VERIFY current §].

### 20.4 Technical-standard reference in contracts

VOB Teil C's DIN 18299 (general provisions for all Bauarbeiten) plus the relevant
gewerkspezifische DIN (e.g. DIN 18350 Putz-/Stuckarbeiten, DIN 18195/18533
Bauwerksabdichtung) is the usual anchor for "state of the art" execution quality in
a renovation contract — cite the specific gewerk DIN, not just "VOB", when writing
scope/quality clauses.

### 20.5 Kündigung specific to renovation projects

Freie Kündigung (§8(1) VOB/B, §648 BGB) is common on renovation projects once
opened-up conditions reveal the scope was mis-estimated — the contractor is
entitled to be made whole for the unexecuted portion (§648 satz 3 BGB presumes 5 %
of the unexecuted contract value absent other proof), so an early, honest
Bestandsaufnahme (§1) is the cheapest way to avoid this outcome, not a contractual
afterthought.

### 20.6 ÖNORMEN supplement (Austria)

Austrian practice runs on **ÖNORM**/ÖTR (Österreichische Technische Regeln) plus
adopted ISO/EN/ENV/HD/EN ISO and ÖNORM-DIN standards, administered by
Österreichisches Normungsinstitut (ON), Vienna. ÖNORMEN are indexed both
alphanumerically and by ICS (International Classification for Standards) sachgruppe.
[VERIFY current status] — where a DACH renovation project spans Austria, confirm
whether the applicable technical rule is the ÖNORM or an adopted EN/ISO text before
citing a German DIN number; do not assume DIN-only citation is sufficient for an
Austrian building authority.

## 21. Decision matrix — component → assessment → repair → owning skill

| Component | Typical damage | Assessment method | Repair options (behutsam → konventionell) | Deep-dive skill |
|---|---|---|---|---|
| Naturstein | Absanden, Absprengung, Krustenbildung, Durchfeuchtung | Petrographic ID (DIN EN 12440), Mohs test, moisture/salt survey | Kaliwasserglas consolidation → Vierung → full replacement | §2 here |
| Stahlbeton | Carbonation/chloride corrosion, spalling | Half-cell potential, carbonation depth, chloride profile | EN 1504 principles 1–6 (surface) or 7–11 (corrosion) | §3 here; `existing-structures-retrofit` §4 |
| Timber structure | Fungal/insect decay, moisture damage | Visual + resistograph + species ID | Constructive protection → splicing/resin repair → member replacement | `timber-building-renovation` |
| Metal roofing/facade | Corrosion, contact corrosion | DIN EN ISO 12944 class review, metal-pairing check | Recoat/replace flashings → Titanzink re-cladding | §5 here |
| Below-grade masonry | Rising damp, salt loading | Durchfeuchtungsgrad, salt analysis | Ventilate/accept evaporation zone + Sanierputz → vertical seal → horizontal seal (mechanical/injection/electrophysical) | §6 here |
| Facade masonry | Cracks, render failure, damp | 6-step diagnosis chain (§7.3) | Consolidate/patch-repair → interior insulation → WDVS/Klinkerriemchen | §7 here; `masonry-construction` |
| Roof | Missing/damaged covering, uninsulated | Diagnose Dachwerk (§8.6) | Nachstecken/re-point → insulate in place → full strip-and-rebuild | §8 here; `roofing-waterproofing` |
| Floors/ceilings | Balkenkopf decay, acoustic failure | Lift flooring strip, inspect all bearings | Anlaschen/steel splints → resin bearing replacement → full replacement | §9 here |
| Chimney/flue | Undersized for new appliance, lining failure | Schornsteinfeger inspection, EN 13384 check | Reline/Ausschleifmasse → Querschnittsanpassung → LAS/Kunststoff retrofit | §10 here |
| Windows/doors | Timber decay, poor U-value, weak security | Visual + U-value estimate + RC class check | Refurbish sash/hardware → glazing upgrade → full replacement | §12 here; `openings-windows-doors` |
| Joints | Sealant failure, umläufigkeit | Visual + geometry check vs. DIN 18540 | Reseal/rebond → full joint rebuild | §13 here |
| Render/coating | Cracking, delamination, salt damage | Haftfestigkeitsprüfung, salt survey | Consolidate + Sanierputz (WTA class) → strip and re-render | §14 here |
| Building energy performance | Non-compliant U-values, thermal bridges | GEG §48/§50 calculation | Component-by-component upgrade to Anlage 7 → WDVS/Innendämmung campaign | §16 here; `building-physics-thermal-moisture` |

## 22. Cross-reference summary

- `simple-first-building` — governing complexity/liability default for every choice
  above.
- `existing-structures-retrofit` — structural condition assessment, Nachrechnung,
  strengthening engineering, historic material strength classes, Bestandsschutz
  legal mechanics.
- `timber-building-renovation` — historical timber construction, damage diagnosis,
  residual-strength assessment, Fachwerk/Umgebindebau repair.
- `timber-steel-design`, `masonry-construction`, `concrete-detailing` — new/
  replacement member design once the renovation decision is made.
- `building-physics-thermal-moisture` — GEG calculation methodology, Glaser
  diagrams, n50 measurement.
- `sustainable-construction` — LCA/EPD figures, circularity/material-passport
  documentation, GEG whole-building energy duties.
- `building-services-tga` — heat pump/solar/ventilation sizing and hydraulics.
- `building-regulations-permits` — full permit/contract-law mechanics.
- `construction-scheduling-site` — sequencing, incl. Artenschutz-driven timing
  constraints.
- `roofing-waterproofing`, `openings-windows-doors`, `stairs-vertical-circulation`,
  `construction-detailing`, `building-materials` — component-level design detail
  once the renovation scope is fixed.
- `construction-freecad-bim` — modeling a renovation: Bestand baseline, status
  tagging (Bestand-erhalten/-rückbau/Neu), delta tracking, degraded-material FEM
  overrides (see its "Renovation & retrofit modeling" section).
- `bim-management` — LOD/LOI implications of a survey-grade Bestand model.
