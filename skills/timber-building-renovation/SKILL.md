---
name: timber-building-renovation
description: >
  Historical timber construction diagnosis and repair for Bauen im Bestand:
  identifying and dating traditional Zimmermannsverbindungen (Verblattung,
  Verzapfung, Versatz, Verkämmung, Aufklauung and their named variants),
  regional Fachwerk/Blockbau/Umgebindebau typologies with dating tables,
  historic roof (Sparrendach/Pfettendach) and floor construction systems;
  damage diagnosis (Schadensanalyse) for wood-destroying fungi (Echter
  Hausschwamm, Nassfäulepilze, Hausporling, Blättlinge) and insects
  (Hausbock, Nagekäfer) with moisture/temperature thresholds and exit-hole
  identification, mechanical and chemical/corrosion damage, non-destructive
  and semi-destructive diagnostic methods (Bohrwiderstand, Ultraschall,
  Endoskopie, Bohrkern, dendrochronology) with DIN citations; residual
  capacity and damage assessment (Schadensbewertung) including DIN 68800
  Gebrauchsklassen/Dauerhaftigkeitsklassen, safety cutback distances, and
  the historic-timber-grading problem under DIN 4074/DIN EN 1995; and
  repair/Ertüchtigung technique catalogs for roof feet, ridge joints,
  purlins, Fachwerk (Fußschwelle, Ständerfuß, Ausrichtung, Altholz reuse),
  Blockbau and Umgebindebau construction, with a full worked EC5
  verification example. Use whenever a task involves an existing timber
  roof, floor, half-timbered (Fachwerk), log (Blockbau) or Umgebinde
  building — diagnosing damage, dating a connection or construction type,
  or planning a substance-preserving repair — as opposed to sizing new
  timber members, which is `timber-steel-design`, or the general
  structural-assessment/Nachrechnung machinery, which is
  `existing-structures-retrofit`.
---

# Timber Building Renovation (Holzbausanierung im Bestand)

Distilled from Lißner/Rug, *Holzbausanierung beim Bauen im Bestand*
(Springer VDI-Buch). Covers the parts of "Bauen im Bestand" that are
specific to historical timber construction: recognizing what you are
looking at, diagnosing why it failed, judging what is still load-bearing,
and choosing a substance-preserving repair. It does not repeat general
retrofit/Nachrechnung mechanics or EC5 member design — see §9.

## Reality check

- This skill supports triage and preliminary repair planning. A licensed
  Tragwerksplaner with timber-structures experience must verify any
  load-bearing repair before execution, and a Sachverständiger für
  Holzschutz/Holzschäden should confirm fungal/insect diagnosis before
  chemical or destructive intervention is specified.
- Species-, fungus- and connection-specific numbers below (moisture
  thresholds, cutback distances, cross-section reductions) are from a
  single German-language reference and regional field studies cited in
  it. Treat them as planning-stage defaults, not substitutes for an
  on-site survey — confirm before committing to a repair scope or cost
  estimate.
- On a Denkmalschutz object, every repair decision below is subordinate
  to the Denkmalschutzbehörde's approval; "substance-preserving" framing
  throughout this skill reflects that priority, not just cost.
- Historic connection load capacities are order-of-magnitude planning
  aids. A real verification always re-derives forces from the actual
  geometry and current DIN EN 1995-1-1/NA rules (§7.2 shows the method).

## Evidentiary tiers and the [VERIFY] convention

1. **Normative** — a currently valid DIN/DIN EN clause, cited by number.
   Treat as binding unless superseded; confirm current edition before
   use, since editions and National Annexes change.
2. **Standards-of-practice / literature-sourced** — values, thresholds or
   rules-of-thumb from the cited book and the field studies it summarizes
   (e.g. Becker/Tichelmann's 50,000-case survey, ZHD Fulda mapping
   method). Solid planning defaults; state the source when citing them
   to a client or authority.
3. **[VERIFY]** — a claim not traceable to a current standard's text in
   this skill's source; typically because it is empirical/regional or the
   underlying standard has since changed. Re-confirm before relying on it.

## 1. Terminology (Bestandsbau-Begriffe)

German usage distinguishes these terms precisely; using them loosely
invites scope disputes in a Sanierung contract:

- **Instandhaltung** — keeps a building at its Sollzustand; no intervention
  in structure or external form.
- **Instandsetzung** — restores fitness for use; repairs/partial
  replacement of damaged components, substance and geometry largely
  preserved (HOAI §2 Ziffer 8).
- **Sanierung** — umbrella term (used inconsistently in practice) for all
  technical measures restoring a construction's or building's usability;
  starts with removing damage and its causes.
- **Ertüchtigung** — measures that raise properties *above* the original
  level (load capacity, durability, fire resistance, thermal/acoustic
  performance) — not just restoration.
- **Modernisierung** — gives the building a new quality it never had, with
  a durable increase in use value or durable heating/water saving (HOAI
  §2 Ziffer 6).
- **Restaurierung** — repair of culturally significant fabric, preserving
  existing substance (SIA 469).
- **Rekonstruktion** — rebuilding to the original form/type from evidence
  (images, written sources); can extend to full historical rebuild.
- **Bestandsschutz** — a structure lawful when built need not be adapted
  to current building-law rules, unless a substantial change requiring
  permission, or a change of use, is planned — see
  `existing-structures-retrofit` for the full grandfathering mechanics.

## 2. Historical construction typology

### 2.1 Roof systems

Two structurally distinct families developed separately in the German
regions before merging elements later:

- **Sparrendach** (rafter roof) — rafters and ceiling joist form a rigid
  triangle; loads go to the outer walls. Developed mainly in the
  Mittel-/Niederdeutsch region. A **stehender Stuhl** (standing queen/king
  post frame, used from ~1400) or **liegender Stuhl** (raking frame, frees
  usable roof space) provides longitudinal bracing and, on wide spans,
  intermediate rafter support via Kehlbalken (collar ties, introduced
  ~1200–1500) or a Firststütze (ridge post, from the 13th c.).
- **Pfettendach** (purlin roof) — rafters are simply-supported beams on
  purlins parallel to the ridge, spaced every 4–5 m; purlins need a
  Stuhl (queen-post frame) to carry their load down. Developed mainly in
  Süddeutschland (Donau/Alpine region); more adaptable to irregular
  plans, easier to calculate, common from the late 19th/early 20th c.
  onward. Subdivided into **strebenlos** (roof pitch < 30–35°, loads go
  straight to ceiling joists/walls) and **abgestrebt** (> 30°, loads
  diverted to outer walls via struts/Häng-/Sprengwerk).

Historical timeline of typical construction (chapter 3, Tab. 3.1 — use to
date an unknown roof and anticipate what you will find):

| Period | Typical construction |
|---|---|
| Before 1870 | Sparrendach (≤~7 m span, pitch ≥35°, rafter length ≤4.5 m); Kehlbalkendach (rafter length 4.5–8 m, span ≤12 m); multi-stool Kehlbalkendach for wider/heavier cases; Hängewerk (1- or multi-fold); Mansarddach with 2–3-fold stool |
| 1870–1918 | Pfettendach with 1- or multi-fold standing stool (≥1 stool at ridge, mandatory for saddle roofs on purlin framing); Drempelpfettendach; Pultdach with hanging or raking stool(s) |
| 1918–1945 | Pfettendach (standing stool, with/without Drempel); simple Sparrendach/Kehlbalkendach persist |
| After 1945 | Simplified: Pfettendach (1–2-fold standing stool); Sparrendach/Kehlbalkendach, including Gittersparrendach (lattice rafter) |

Kehlbalkendächer use ~20–30% less timber than Sparrendächer without
collar ties — the driving reason they spread after WWI timber shortages.
Historic sizing before ~1920 used carpenter's rules-of-thumb (Faustformeln,
[VERIFY] regional variation), e.g. Sparrenhöhe *H* = *L* + 4 cm (1904,
*L* = clear rafter length in m) vs. *H* = 5 cm + 2·*L* (1920/1939) — a
useful sanity check when an as-built member looks under-sized by modern
standards but has stood for a century.

**Bohlendächer** (plank-arch roofs, de l'Orme 1561, spread in Prussia via
David Gilly from ~1797) economize timber by building arched binders from
short curved planks (1.2–2.0 m long, ≥200–300 mm wide) nailed in 2–3
layers with staggered joints — occasionally still found over halls,
riding arenas, churches; span/ply-count data in the source, [VERIFY]
before reusing as a repair reference since national annex rules for
built-up sections now apply.

### 2.2 Floor systems

Timber floor construction (Holzbalkendecken) followed the same regional
split — joist bearing/anchoring to masonry (Balkenschuh, Mauerlatte,
anchor irons through 3 joists) is the most common Bestandsaufnahme
finding and the most common damage location (balcony/joist-end decay,
§4.3.3.2). [VERIFY] joist spacing/species by direct survey — pre-1945
practice was regionally faustformel-driven like roof sizing above.

### 2.3 Fachwerk, Blockbau, Umgebindebau

Three load-bearing wall systems, each with distinct regional dating
signatures (chapter 7.4 gives period-tagged construction catalogs per
region — use these to date an unknown building from its frame geometry
before opening anything):

- **Niedersächsisches Fachwerk (ländlich)** — Mecklenburg farmhouse forms
  dated by gable/roof form; Strohlehm-auf-Stakung infill typical before
  ~1850.
- **Niedersächsisches Fachwerk (städtisch)** and **Mitteldeutsch-fränkisches
  Fachwerk** — separate regional catalogs, each with its own bracing
  grammar (Streben, Kopfbänder, Fußbänder) and dating range.
- **Blockbau** (log construction) — corner joints (Eckverkämmung) carry
  the wall; U-value already ≈0.5 W/(m²·K) at 200 mm wall thickness from
  the timber alone if joints are wind-tight — usually no added insulation
  needed; fire resistance F30 achieved at 100 mm (single storey) or
  180 mm (two storeys) [VERIFY current DIN EN 1995-1-2 edition].
- **Umgebindebau** — hybrid: a free-standing internal timber frame
  (Säulen, Rähm, Kopfbänder/Knaggen) carries the roof independent of the
  masonry or log outer wall, which is only a weather envelope. Regional
  Silesian/Lusatian form; single- and one-and-a-half-storey (with
  Drempel) variants dated to before/after 1550–1850 in the source
  catalog.

## 3. Historical connections catalog (Holzverbindungen)

### 3.1 Five basic types

Every traditional Zimmermannsverbindung is one of five basic types or a
combination — recognizing which one you have tells you its likely load
path, failure mode and repair options:

1. **Verblattung** (halving/lap joint) — the oldest, originally
   wedge-secured, later peg-secured (Holznagel). Load transfer only by
   contact bearing and friction — no meaningful tension capacity.
2. **Verzapfung** (mortise-and-tenon)
3. **Versatz** (notch/step joint, e.g. strut-to-tie) — transmits
   compression through Vorholz bearing (see §7.2 for the modern EC5
   verification of this joint type).
4. **Verkämmung** (notch/cog joint) — e.g. joist bearing on a wall plate.
5. **Aufklauung** (birdsmouth/notch seat) — rafter seating on a purlin.

Metallic fasteners (nails, Stabdübel, Dübel besonderer Bauart, adhesives)
entered from ~1900 as spans and loads grew, driven by cheaper iron/steel
— see §3.4 for the code timeline. Most Zimmermannsverbindungen were
displaced by engineered fasteners in new construction over the 20th
century, but survive throughout the existing stock and must still be
assessed and often re-executed during repair — DIN EN 1995-1-1/NA:2013
retains design rules for them for exactly this reason.

### 3.2 Verlängerungsverbindungen (splices, along the grain)

| Connection | Typical use | Notes |
|---|---|---|
| Gerader/schräger Stoß | Schwelle, Rähm, Pfette | Needs support at the joint; secured by steel straps, nails, cramps — usually inadequate alone |
| Zapfenstoß | Schwelle, Rähm | Good, easily secured; historic tenon length up to 40 cm |
| Schwalbenschwanzstoß | Schwelle, Rähm, Mauerlatte | Attested from the 1st c. AD |
| Gerader Stoß mit Haken(+Keil)/Schloss | Schwelle, Stiel | **Repair-specific** solution when a timber is too short for a lap |
| Gerades/schräges/Hakenblatt | Schwellen, Rähm, Pfette | Schräges Blatt reduces splitting vs. gerades Blatt; still the most common modern repair splice |
| Zahnverbindung (toothed splice) | Balken, Stützen, Streben, 14th–19th c. | Teeth 8/10–15/10 of member height, tooth depth 1/9 of height (for beams) or teeth 1.5–3.0× height with 1/10–1/8 depth (for columns/struts) |

### 3.3 Cross, corner and angled connections

- **Querverbindungen** (perpendicular members): Blatt variants (gerades,
  schräges, Hakenblatt), Schwalbenschwanz (dovetail, from 1st c. AD),
  Zapfen variants (einfach, Doppel-, Brust-, geächselt, Kreuzzapfen),
  Verkämmung variants (einfach, Doppel-, Schwalbenschwanz-, Kreuzkamm,
  Schwabenkamm mit Dollen Ø20–30 mm).
- **Eckverbindungen** (corners): stumpfer Eckstoß (weak, avoid relying on
  it structurally), gerades/schräges Eckblatt, Scherblatt, Eck-/
  Winkelzapfen (strongly weakens Schwelle/Rähm cross-section — check
  residual section at these points first when assessing an old frame).
- **Schrägverbindungen** (raking members — struts, braces): glatter
  Zapfen abgestirnt (standard for rafter/beam and Fachwerk strut
  connections), Jagdzapfen (good two-sided repair joint for head/foot
  braces), Versatz variants (einfach, doppelt, mit Zapfen).
- **Verstärkungsverbindungen**: dübelverbundene Balken (side-driven dowels
  + bolt), armored beam splices with Schwerter (side plank splints) +
  bolts — common repair pattern for cracked beams/rafters.

Roof- and floor-construction-specific application frequency tables
(preferred/common/limited, by region and period) are in the source's
§7.2–7.3 reference tables — consult before assuming a connection type is
"wrong" for a given building's age and region.

### 3.4 Historic code timeline (for dating and assessing connections)

Knowing which code governed a connection when it was built explains why
its detailing or allowable stresses differ from current EC5 — critical
context before deciding a historic connection is "deficient":

| Year | Code | Key content |
|---|---|---|
| 1920 | DIN 104 Bl.1 | First tables for Kleinhaus timber joists |
| 1926 | DRB provisional rules | Raised allowable tension/compression parallel to grain; ω-method for buckling; bolted-connection rules |
| 1928 | DIN 1990 | Building physics, wood protection, 80-year minimum design life |
| 1933 | DIN 1052 (1st ed.) | First DIN 1052; nail sizing rules (shank 1/6–1/8 of timber thickness in bending) |
| 1938 | DIN 1052 (2nd ed.) | Built-up compression members; uniform deflection limit L/300 |
| 1939 | DIN 4074 (1st ed.) | First visual grading standard (Kantholz only) |
| 1940 | DIN 1052 (3rd ed.) | Grade-differentiated allowable stresses; L/200 deflection for purlins/rafters; Dübel needed police approval |

Dübel besonderer Bauart (special dowel-type connectors) normed
separately from 1925: rectangular dowels (1925 R.B.D. Stuttgart rules) →
1933 rectangular/disc/plate/ring/claw dowels permitted, cast-iron min.
5 mm wall thickness, bearing stress 8 N/mm² (a/t≥5) or 4 N/mm² (a/t<5) →
DIN 1052 Bl.2:1969 names proprietary systems still found in the field
(Ringkeildübel, Appel-Rippendübel, Beier-Ringdübel, Kübler-Dübel,
Tuscherer-Dübel, Geka-, Bulldog-, Alligator-Dübel) → DDR TGL 33135/02:1984
→ DIN 1052-2:1988 Typ A–E. Several of these proprietary types are still
recognized in DIN 1052:2008 — useful when an as-built connector doesn't
match any current catalog part.

## 4. Damage analysis (Schadensanalyse)

### 4.1 Damage statistics and classification

A nationwide survey of >50,000 damage cases (Becker/Tichelmann, 1991/92)
groups timber damage into four causal classes; groups I (biological) and
IV (moisture ingress) dominate and are causally linked — most biological
damage traces back to a moisture-ingress cause. Damage frequency in the
former East German states ran ~10 percentage points higher than in the
West, and differed in character: Western-state damage is mostly
attributable to renovation errors or improper use; Eastern-state damage
to neglected maintenance of the fabric itself. One-third of mechanical-
damage cases trace to load redistribution after a biologically-degraded
member lost capacity — reinforcing why biological and mechanical
assessment must be done together, not sequentially.

### 4.2 Wood-destroying fungi

All cause Braunfäule (brown/destruction rot) unless noted: wood
longitudinal/transverse cracking, browning, residual substance crumbles
to powder (cubical breakdown).

| Fungus | Species | Moisture need | Temp. optimum (°C) | Notes |
|---|---|---|---|---|
| Echter Hausschwamm | *Serpula lacrimans* | Low at onset only; then self-transports water via strand mycelium — can attack dry wood and grow through masonry/fill | 8–26, narrow range | The dangerous one: hides in floor voids/behind cladding, growth often unnoticed until fruiting bodies appear on masonry/skirting/stair treads far from the timber; BGB §633 "erheblicher Sachmangel"; notifiable to the Bauaufsichtsbehörde in most Länder (e.g. SächsBO) alongside Hausbock and termites |
| Brauner Keller-/Warzenschwamm | *Coniophora puteana* | Needs sustained high moisture; survives desiccated >5 years, resumes on rewetting | — | Attacks softwood; thin, pale-to-blackish surface mycelium |
| Weißer Porenschwamm | *Antrodia vaillantii* | As above | — | Attacks softwood; white, frost-flower-pattern surface mycelium |
| Hausporling | *Donkioporia expansa* | Wood moisture >35% | — | Attacks hard- and softwood; does not grow through masonry |
| Blättlinge (3 species) | *Gloeophyllum abietinum/sepiarium/trabeum* | 35–60% wood moisture | — | Often no visible surface mycelium — causes hidden internal rot (Kernfäule/Innenfäule) that can precede sudden collapse of a loaded beam if undetected |

Strength drops fast under active Echter-Hausschwamm attack — bending
strength falls measurably within a few months of infection (source
fig. 4.65, [VERIFY] exact curve by species).

### 4.3 Wood-destroying insects

Table 4.5 — optimal (parenthetical: full development range) conditions:

| Species (DE / Latin) | Attacked part | Preferred wood | Moisture % | Temp °C | Exit hole |
|---|---|---|---|---|---|
| Gewöhnlicher/Gemeiner Nagekäfer, *Anobium punctatum* | whole cross-section | soft- and hardwood | 30 (10–>50) | 22–23 (12–25) | round, 1–2 mm, numerous |
| Hausbock, *Hylotrupes bajulus* | sapwood only | mainly softwood | 30 (10–>50) | 28–30 (10–>35) | oval, ~4×7 mm, wavy larval galleries |
| Brauner Splintholzkäfer, *Lyctus brunneus* | sapwood | hardwood | 15–16 (8–22) | 28 (15–32) | — |
| Mulmbock, *Ergates faber* | mostly sapwood, rarely heartwood | softwood | 50 (20–>50) | 30 (15–>35) | — |
| Trotzkopf, *Anobium pertinax* | mainly sapwood | fungus-damaged soft-/hardwood | >50 (25–>50) | 22–25 (10–30) | round, 2–3 mm |
| Gescheckter/Bunter Nagekäfer, *Xestobium rufovillosum* | sapwood | mainly oak, also other hard-/softwood | >50 (25–>50) | 22–25 (10–30) | round, 3–4 mm |

Hausbock is the most widespread structural pest, found chiefly on roof
carpentry near open dormers/hatches and upper-storey joists. Its exit-hole
pattern lets you estimate cross-section loss directly from the damage
picture with experience; Nagekäfer damage cannot be estimated visually —
assume the member needs opening/testing. Do not assume Hausbock is
inactive just because the timber is old: activity has been documented in
timber >60 years old, so a "historic, therefore dormant" assumption is
not safe without a live-infestation check (stethoscope for feeding
sounds, fresh bore dust, endoscopy).

### 4.4 Mechanical damage

Static overload chiefly comes from load redistribution after another
member's biological failure, section loss, inaccurate original load
assumptions, unqualified interventions (members cut with hand/chain saws
during loft conversions), or unaccounted use-loads (change of use, snow-
sack/ice/water pooling, accumulated storage loads). Timber is proven over
centuries for static loads; dynamic loads (vibration, impact, seismic,
explosion) can still cause cracking, fatigue fracture, deformation and
fastener failure — smooth-shank nails, Einlassdübel and nail plates are
the most vulnerable fastener types under dynamic/impact loading.

### 4.5 Chemical damage and corrosion

- Wood resists weak acids and dilute alkalis; corrosion is generally
  negligible in the pH range 2–11. Softwoods resist chemical corrosion
  better than hardwoods; glulam better than solid timber.
- **Fire-/wood-preservative salt overdose (mazeration)**: repeated
  high-concentration treatment with K/NH₄-salt or phosphate-based
  products produces a wooly, defibered surface layer. Critical total salt
  load: **>20 g/kg wood substance** [source lit. citation]. Mazerated
  layer depth typically ≤5 mm (zero residual strength); the next 3–6 mm
  is not yet defibered but has strongly reduced strength — **when
  assessing capacity, reduce the cross-section by 10 mm on all sides**
  as a planning default for salt-mazerated members; small sections (e.g.
  battens) often have no residual capacity left and must simply be
  replaced. Oak resists these salts less well than softwood. Where PCP
  (pentachlorophenol)-based preservatives are found, the PCP-Richtlinie
  governs health assessment and remediation — treat this as a
  hazardous-materials trigger, not just a structural one.
- **Latten-/Sparren-Korrosion under tile roofing**: sulfates leached from
  tile clay, or calcium hydroxide leached from lime mortar bedding, cause
  a similar (but shallower, ~2–3 mm) surface mazeration on battens and
  rafters — easily mistaken for fungal mycelium; distinguish by testing,
  not appearance alone. Light cases: wire-brush off the salts; battens
  with reduced section and wide rafter spacing: re-batten.
- **Stress corrosion cracking of steel fasteners**: nitrate-ion media
  (ammonium sulfate, calcium ammonium nitrate, urea — common in
  agricultural storage buildings) cause invisible grain-boundary damage
  in loaded steel fasteners leading to *sudden* failure with no warning;
  risk increases with stress level, humidity, temperature and vibration.
  Only detectable metallographically in a lab. Two documented cases make
  the point: turnbuckle bolts from a Fachwerk frame hall after 50 years
  storing Kalkammonsalpeter showed 10–50% surface corrosion loss *and*
  grain-boundary damage to 0.6 mm depth even where surface corrosion was
  comparatively light; a separate bolt exposed to the same medium for
  only **10 years** already showed grain-boundary damage to **0.8 mm**
  depth — worse than the 50-year case despite far less exposure time.
  **Treat any steel connector in a former agricultural/fertilizer/
  chemical-storage building as a stress-corrosion suspect** regardless of
  surface appearance or exposure duration, and sample metallographically
  before relying on it.
- Corrosion protection of steel connectors: DIN EN 1995-1-1:2010 §4.2
  (minimum protection by exposure class) for low corrosivity;
  DIN SPEC 1052-100:2013 Tab. 1 for moderate/severe/very severe.
  Tannin-rich species (oak, Bongossi) and preservative-impregnated timber
  both demand stainless or equivalently resistant fasteners
  (DIN EN 1995-1-1/NA:2013 NCI zu 4.2 (NA.6)).

### 4.6 Damage mapping (Schadenserfassung/-kartierung)

Document on as-built plans before any intervention, both to plan the
repair scope and to support fee/cost estimation. The ZHD Fulda
(Zentrum für Handwerk und Denkmalpflege) system is the standard
methodology: graphic mapping by symbol/color for damage type, extent and
depth, combined with a measurement/sampling log. Feed the result into
Instandsetzungsdringlichkeit triage (which elements need action now vs.
can be monitored) and an overall Zustandsklasse for the structure —
parallels the Zustandsnote system in `existing-structures-retrofit` but
at component rather than whole-structure granularity.

## 5. Diagnostic techniques (Untersuchungsverfahren)

Select method by: investigation goal, likely damage type, accessibility
(occupied building? hidden members?), tolerance for destructive/semi-
destructive testing, and required accuracy. None of these substitute for
an experienced assessor's judgment — they are inputs to it.

| Parameter | Method | DIN / notes |
|---|---|---|
| Overall condition, hidden members | Visual (handnah), Abklopfen, Bebeilen, Eindringwiderstand (Stechbeitel) | Non-destructive to destructive; first pass always |
| Pest ID | Endoskopie (bore Ø5–20 mm), Fraßbild/exit-hole geometry, Stethoskop for live feeding sound | — |
| Geometry/deformation | Messband, Nivellier, 3D-Laserscan, Fotogrammetrie | — |
| Moisture (wood) | Electrical resistance (surface only — real distribution across the section can be very uneven) | DIN EN 13183-2, accuracy ±0.5–1% (u<30%) / ±3–4% (u>30%) |
| Moisture (wood), reference method | Gravimetric (Darr) | DIN EN 13183-1, accuracy 0.1% of sample mass — used to calibrate field readings |
| Moisture (wood), capacitive | — | DIN EN 13183-3 |
| Strength/density/moisture (direct) | Bohrkernentnahme | Ø≥4 mm visual only; Ø15–25 mm for compression strength/density/moisture (practical field standard); Ø≥25 mm dendrochronology; Ø35–50 mm Dynstat (DIN 53435/TGL 1-204 Bl.8) or glulam glue-line shear (DIN EN 14080) |
| Compression strength (core vs. standard specimen ratio σ_core/σ_std) | — | Oak 1.18, spruce 1.09, pine 1.33 (mean); scatter 8% oak, 15% beech, 17.4% spruce, 10% pine |
| Dynamic E-modulus, defect location | Ultraschall (longitudinal for grading; transverse for crack/glue-fault location, usable up to 1 m glulam thickness on a sound, low-crack surface) | — |
| Internal condition profile, semi-destructive | Bohrwiderstandsmessung (1.5 mm drill tip, constant feed/speed) | Good for locating weak zones and active-fungus boundaries |
| Wood species/age | Visual/microscopy; Dendrochronologie (core Ø≥25 mm); Radiokarbonmethode | Lab-grade dating options |
| Coatings | Haftprüfung, thickness/buildup | DIN EN 24624/DIN 53151, DIN 50950/DIN 50986 |
| Active fungus | Vitalitätstest, pH (oxalic acid), DNA analysis, chromatography | — |
| Preservative content/contamination | Extraction | DIN 52161-1/-7, DIN EN 351-2, DIN EN 212 |
| Strength (destructive) | Druckfestigkeit, Biegefestigkeit, Scherfestigkeit, Zugfestigkeit | DIN EN 408 and DIN 52185/52186/52187/52188 |

Bore holes from core sampling can be plugged with matched new-wood
plugs afterward — routine, not a reason to avoid coring where needed.

## 6. Damage/residual-capacity assessment (Schadensbewertung)

### 6.1 DIN 68800 Gebrauchsklassen and species durability

DIN 68800-1 (fully revised 2011/2012) replaced the older Gefährdungsklassen
with Gebrauchsklassen (GK), assigned by exposure and documented per
component:

- **GK 0** — permanently dry, indoors.
- **GK 1** — permanently dry.
- **GK 2** — under roof, not weather-exposed, but can exceed 18–20% moisture
  for up to 6 months.
- **GK 3.1 / 3.2** — additionally weather/condensation exposed
  (occasionally / frequently wet).
- **GK 4** — ground/earth contact; Moderfäule risk in addition to
  Braunfäule, needs specific agents (e.g. copper salts).

Native species can be used **without chemical wood preservative** up to
GK 3.2 if the right species/durability class is chosen (DIN 68800-1
§6.8.2.2, Tab. 5): spruce/fir/beech → GK 0 (heartwood not durable enough
beyond that); pine heartwood → GK 0–2; larch/Douglas fir heartwood →
GK 0–3.1; oak heartwood → GK 0–3.2. For GK 4 with native species, only
Robinie qualifies (durability class 1–2) — but it has no DIN EN 1912
strength-class assignment, so use needs a case-by-case Zustimmung.
Oak heartwood (durability class 2 per DIN EN 350-2) resists fungi well
but is still attacked by Nagekäfer; beech is durable in strength terms
but has essentially no natural fungal resistance untreated.

### 6.2 Safety cutback distances (bekämpfender Holzschutz)

When removing fungus-damaged wood under DIN 68800-4, cut back beyond the
visible infection because hidden strength loss can extend further than
visible damage:

- **Echter Hausschwamm**: 1.0 m beyond visible attack (standard); can be
  reduced to 0.5 m only where microscopy confirms the wood at that
  distance is uninfected — typically needed only where the full 1.0 m
  would compromise an otherwise-sound structural member.
- **Nassfäulepilze** (Coniophora, Antrodia etc.): 0.3 m beyond visible
  attack.
- **Fill/plaster near a Hausschwamm outbreak** (Schüttstoffe, Putz):
  remove 1.5 m beyond the infection boundary — the fungus can travel
  through masonry and fill invisibly, so treating only the timber
  invites reinfection of an already-"repaired" area. This failure mode
  (reinfection because the myzel in masonry/fill was ignored) is common
  enough to flag explicitly in every Hausschwamm repair scope.
- On protected/decorated elements that cannot be removed (painted
  beams, stucco ceilings, panelling), no method guarantees complete kill
  — document the residual reinfection risk in writing to the client.

### 6.3 The historic-timber-grading problem

DIN EN 1995-1-1/NA:2013 NCI Zu 1.1.2 (NA.5) explicitly extends the
current design standard "sinngemäß" (by analogy) to Bauten im Bestand.
But applying DIN 4074 visual grading to existing timber runs into
practical obstacles worth naming explicitly before you rely on an
as-built grade:

1. Grading standards target sawn timber; pre-mid-19th-century members are
   often hand-hewn.
2. Grading is rarely actually performed in practice on existing timber —
   engineers commonly default to S10 without checking whether a higher
   grade is achievable or a lower one is actually present.
3. Visual grading legally requires trained personnel (DIN 4074-1/-2
   §6.1) — a requirement essentially never met for in-situ grading of
   existing members.
4. Members that aren't fully visible can't be checked against the full
   criteria set (knots, grain angle, pith, ring width, cracks, wane,
   curvature).
5. Machine grading requires certified equipment at an approved facility
   — not deployable on built-in members.
6. CE marking under DIN EN 14081-1 (a precondition for the sawn-timber
   regulated-product status) is never present on historic members.
7. Grading references 20% reference moisture (DIN 4074-1/-5 §3.3) —
   existing dry timber often runs below that, [VERIFY] whether this
   yields an unexploited safety margin (not systematically studied per
   the source).

Practical path: density is comparatively easy to determine on built-in
timber (bore cores, §5) and DIN EN 338 now tabulates characteristic and
mean density per strength class — use density-based estimation as the
practical route to a strength class assignment for existing members,
combined with a careful visual pass, rather than either skipping grading
or claiming full DIN 4074 compliance you cannot actually demonstrate.
Historic glulam (pre-1968, e.g. Hetzer, Christoph & Unmack, Kübler
production) cannot be assigned a current DIN EN 14080 class at all —
needs case-specific testing every time. See `timber-steel-design` for
the EC5 member verification once a strength class is established, and
`existing-structures-retrofit` for the general reduced-γM Nachrechnung
framework this feeds into.

### 6.4 Moisture content categories

- darrtrocken (kiln-anhydrous): u = 0%
- trocken (dry): u ≤ 20% (DIN 4074-1/-5 §3.3)
- halbtrocken (semi-dry): 20% < u ≤ 30% (≤35% for sections >200 cm²)
- fasergesättigt (fiber-saturated): u = 22–36%
- nass/saftfrisch (wet/green): u ≥ 30% (≥35% for sections >200 cm²)

Konstruktionsvollholz (KVH) carries a guaranteed u = 15% ± 3%. New
replacement timber should be pre-dried to the expected in-use equilibrium
moisture before installation — documented case: a non-predried oak
replacement sill took **>3 years** for its outer zone to reach in-use
moisture, and the mortise/tenon interior stayed at 20–40% (fungus-
favorable) throughout, because shrinkage gaps kept exposing the joint to
extra moisture. Always specify pre-dried replacement timber in a
Fachwerk/Blockbau repair scope for exactly this reason.

## 7. Repair and retrofit methods (Instandsetzung/Ertüchtigung)

### 7.1 Roof-foot (Dachfuß/Sparrenfuß) repair catalog

The roof foot (rafter/tie-beam bearing) is the single most common damage
hotspot (moisture ingress from delayed maintenance) and therefore the
most-repaired detail. Repair method depends on whether it is a Sparren-/
Kehlbalkendach (rafter carries bending + axial force) or Pfettendach
(rafter carries bending only):

- **Minor section loss at a Versatz/Zapfen foot connection**: Brettlaschen
  (board splints, both sides), additional Simplex bolted connection, or a
  Knagge (corbel block) combined with a Stirn- or Fersenversatz.
- **Longer damaged rafter feet**: two splint boards required (axial force
  must be carried symmetrically), verbindungsmittel count set by the
  calculated force, grouped in two clusters spaced at roughly a fifth of
  the connection length; long-Blatt (lap) splicing is the traditional
  alternative, still common on historic roofs.
- **Local, non-end damage (Merk-Lamellen-Verfahren)**: step-cut back to
  sound wood, glue in matched board lamellae — a material-honest partial
  repair rather than wholesale replacement, preferred where substance
  preservation matters.
- **Combined rafter+joist+purlin damage at the foot**: full three-element
  repair, combining the splint/splice/Merk-Lamellen methods above per
  element. `existing-structures-retrofit` §8.6 identifies embedded beam
  ends (Balkenköpfe) in damp masonry as the classic rot pocket at
  assessment level but explicitly defers the timber-specific repair
  technique to this skill — this is that technique.

### 7.2 Worked example: EC5 verification of a reinforced rafter foot

Demonstrates the general method — re-derive geometry from survey, verify
per current DIN EN 1995-1-1 — that should be applied to any historic
Versatz/Knagge repair, not just this specific case.

**Given**: strut force *N*₍S,d₎ = 23.75 kN at α = 47°; existing rafter and
tie beam: old-growth softwood (pine), visually undamaged, field-sortable
as **S10 per DIN 4074-1**; new corbel (Knagge): new softwood S10, dry-
sorted, NKL 2, KLED short. Rafter/corbel width 160 mm, Aufklauung depth
*t*ₖ, Versatztiefe *t*ᵥ = 40 mm, Anschlusslänge *L*ₐ = 340 mm.

1. **Required Aufklauung depth** from bearing check
   *f*_c,0,k = 21 N/mm² (S10 → C24 per DIN EN 1912/DIN EN 338 Tab.1);
   *f*_c,0,d = k_mod·f_c,0,k/γ_M = 0.9·21/1.3 = **14.54 N/mm²**;
   erf. *t*ₖ > N_S,d /(b·f_c,0,d) = 23.75·10³/(160·14.54) = **10.2 mm** →
   chosen *t*ₖ = 20 mm.
2. **Eccentricity and reaction forces**: *e* = *h*_Knagge − *t*ₖ/2 −
   *t*ᵥ/(2·cos α) = 160 − 10 − 29.3 = **120.7 mm**; lever arm
   *L*ᵥ = ⅚·*L*ₐ = 283.3 mm; from moment equilibrium
   *F*_Z,d = *F*_D,d = N_S,d·e/L_V = **10.12 kN**.
3. **Bearing under the washer** (bolt M16, washer per DIN EN ISO 7094,
   outer Ø56 mm): σ_c,90,d ≈ 4·F_Z,d/(π·(56²−17.5²)) = **4.55 N/mm²**;
   *f*_c,90,d = k_mod·3.0·f_c,90,k/γ_M (contact-face factor 3.0 per
   DIN EN 1995-1-1:2010 §8.5.2(2)) = 0.9·3.0·2.5/1.3 = **5.19 N/mm²**;
   utilization 4.55/(1.0·5.19) = **0.88 < 1.0** — OK.
4. **Fersenversatz (heel notch) check**: effective shear length capped
   at *ℓ*_v,eff = 8·t_v = 320 mm per DIN EN 1995-1-1/NA:2013 NCI NA.12.1
   (NA.4); effective width *b*_ef = k_cr·b with k_cr = 2.0/f_v,k = 0.5
   (f_v,k = 4.0 N/mm²) → *b*_ef = 80 mm; τ_v,d = 16.2·10³/(80·320) =
   **0.63 N/mm²** against *f*_v,d = 0.9·4.0/1.3 = 2.77 N/mm² →
   utilization **0.23 < 1.0**.
5. **Stirnfläche (end-grain bearing at angle α)**: σ_c,α,d = N_S,d/A_Stirn
   = 23.75·10³/6400 = **3.71 N/mm²**; f_c,α,d via Hankinson-type formula
   (DIN EN 1995-1-1/NA:2013 Gl. NA.163) = **5.50 N/mm²** → utilization
   3.71/5.50 = **0.67 < 1.0**.

All checks pass with margin (0.23–0.88) — a repair geometry sized on
constructional/carpentry judgment (round numbers: 20 mm claw depth, 40 mm
notch depth) rather than tight optimization, typical of how these repairs
are actually detailed on site. See `timber-steel-design` for the general
EC5 connection design method this example specializes.

### 7.3 Ridge, collar-tie and purlin repair

- **Firstknoten** (ridge joint, typically Scherzapfen or Blatt +
  Holznagel on old Sparrendächer): repair by applied splints, or —
  denkmalgerecht — by scarfing in matched new wood, combined with
  longitudinal bracing to arrest lateral ridge-line deformation (a common
  secondary symptom of a failed ridge joint).
- **Kehlbalkenanschluss**: corbel + securing screw, partial replacement
  with splints, or an under-set board with nailed splints — all
  relatively simple once the connection is exposed.
- **Pfetten-/Rähmkonstruktion**: historic purlin framing is often
  deliberately under-stiff by modern standards (our forebears accepted
  some flexibility here) — modeling it as a rigid support in a
  Nachrechnung will flag a "deficiency" that reflects the model, not
  necessarily an unsafe structure; discuss with the Tragwerksplaner
  before automatically speccing reinforcement. Where reinforcement is
  genuinely needed: section enlargement (timber, wood-based panel, or
  steel plates) or a static-system change (continuous-beam action,
  Gelenkpfette, or added intermediate support to cut the span).

### 7.4 Fachwerk-specific repair

- **Frame members (Gefüge)**: local defects — trim/chase back
  (Bebeilen/Einstemmen, min. 4 cm) and splice in matched, dry, same-
  species wood, accounting for differential shrink/swell. Larger damage,
  especially at nodes, needs a Tragwerksplaner's calculation and a
  matching temporary shoring design; if the residual section is
  insufficient, use the splice/reinforcement methods of §3.2/§7.1.
- **Fußschwelle** (sill beam): damp sill is caused by a wet plinth in
  nearly 100% of cases — fix the moisture source (horizontal + vertical
  damp-proofing in the plinth masonry) before or alongside any timber
  repair, or the repair will fail again. Partial replacement is possible
  where damage is localized; full replacement is installed from the side
  or from below depending on plinth condition, reusing sound tenons
  where possible; the new plinth must be set back or chamfered so water
  actually drains off it.
- **Ständerfußerneuerung** (post-foot replacement): method matches
  damage extent/type; on heavily loaded wall sections use concealed
  Stabdübel/Passbolzen instead of Holznägel at the joint for extra shear
  security.
- **Holznägel** (timber pegs): primarily positional fixing, not
  necessarily meant to carry load — but oak pegs meeting minimum spacing
  and diameter rules *can* be designed as a load-carrying connection
  (see §6.3 cross-reference to `timber-steel-design`). Square or round in
  section, from oak, pine, hornbeam, acacia, cherry or spruce; bore hole
  1–3 mm undersized vs. the peg; peg size (side length or diameter)
  16–40 mm depending on application. Members are traditionally bored
  "auf Zug" (holes slightly offset) so the peg draws the joint tight —
  understand this before assuming a loose-looking peg joint is defective.
- **Ausrichten** (straightening the whole frame): not every lean needs
  correcting — minor deformation and naturally crooked timber are
  Fachwerk-typical and preserving them keeps the facade's authentic
  appearance and avoids damaging sound infill panels (Gefache). Only
  straighten where standing stability is genuinely compromised (e.g.
  leaning on a neighboring building) and only after full gutting
  (Gefache removed). Use ropes/carpenter's winches, avoid inducing new
  stresses, fix by wedging tenon/lap joints and re-boring pegs; steel
  angle bracing as a last resort, concealed drawn steel pins where
  hidden.
- **Altholz-Wiederverwendung** (reusing old timber): old and new timber
  show no meaningful strength difference — reuse is structurally sound
  where the member is otherwise healthy. But decades-old deflection in a
  reused member cannot be "undone" by reinstalling it differently —
  long-compressed fibers crack quickly and won't regain capacity if
  re-loaded against their set; reinstall with the same deformation and
  matching load orientation it already carries. On full deconstruction:
  dismantle carefully, sort, clean (pressure water/steam works well),
  let dry fully before use, protect from rain/splash in storage, stack
  oriented by cross-section with ventilation gaps, discard any
  pest-infested pieces before restacking.

### 7.5 Blockbau (log construction) repair

- Corner joints (Eckverkämmung) are rebuilt zimmermannsmäßig to the
  historic pattern as a precision fit — this is a load-bearing detail,
  not decorative.
- Replacing whole wall sections: account for shrinkage; new sill
  bearing/height follows the same principles as Fachwerk (§7.4), kept
  above the splash-water zone.
- Localized section loss: repair pieces ≥4 cm thick, oriented core-side
  out to control deformation.
- Wall U-value already ≈0.5 W/(m²·K) at 200 mm if inter-log joints are
  wind-tight — added insulation is usually unnecessary; focus retrofit
  effort on the ground-floor/cellar interface and ceilings to unheated
  spaces instead (cross-ref `building-physics-thermal-moisture`).
- Fire resistance: F30 at 100 mm wall thickness (single storey) or
  180 mm (two storeys) [VERIFY current DIN EN 1995-1-2 edition and
  national annex before citing as compliance evidence].
- Log-course joints: fill with natural materials to the historic
  detail — Werg (tow), coconut fiber, cork, tarred hemp rope, or
  clay-chaff mixes — **never** with permanently-elastic sealants, which
  prevent the intended fiber compression at the joint under wall load.

### 7.6 Umgebindebau repair strategy

Organize the repair scope into the building's four structurally distinct
subsystems, since they behave and fail independently:

1. Blockstube (log room) including its foundation — repair per §7.5.
2. Load-bearing Fachwerk portion — repair per §7.4.
3. Masonry portion (Massivbau) — hand off to `masonry-construction`.
4. The Umgebinde frame itself (columns, Rähm, Kopfbänder/Knaggen) — this
   is the system that actually carries the roof independent of the
   masonry/log walls; treat its members with the roof/floor repair
   methods of §7.1–7.3, and verify it is not being inadvertently loaded
   by settlement or stiffening of the (non-structural) infill walls
   around it.

## 8. Reference: typische Schadbilder (damage-picture catalog)

Condensed from the source's 15-entry catalog — use as a rapid field
checklist; each entry's "measures" column is a starting point, not a
substitute for §4–§7:

| # | Damage picture | Typical cause | First measures |
|---|---|---|---|
| 1 | Durchfeuchtung | Roof/drainage defect, rising damp, poor insulation/ventilation | Eliminate moisture source; assess fungal risk |
| 2 | Verfärbungen | Moisture, temperature, chemical attack, discoloring fungi | Distinguish cosmetic vs. strength-affecting; assess |
| 3 | Bewachsungen | Fungi, moss, plants under moisture | Eliminate moisture; remove growth; check adjacent areas |
| 4 | Strukturveränderung (Fäule) | Wood-destroying fungi + elevated moisture | Species ID, activity test, remove infected wood, assess residual capacity |
| 5 | Fraßbilder (insects) | Wood-destroying insects, sometimes fungus-preconditioned | Species ID, activity test, treat, assess residual capacity |
| 6 | Chemische Korrosion | Aggressive atmosphere/media | Assess strength/stability impact; consider surface treatment |
| 7 | Thermische Schädigung | ≥60°C sustained; ignition ~230°C; self-ignition 350–400°C; aggressive gases | Assess strength/stability impact |
| 8 | Risse | Shrink/swell, heat/moisture, static/dynamic overload, differential settlement | Assess cause, size, location before deciding on repair |
| 9 | Fehlende Bauteile | Overload/total loss, or careless removal during past alterations | Restore original construction or substitute the lost function elsewhere |
| 10 | Form-/Lageveränderung | Use loads, wind, uneven settlement, inadequate bracing, material defects | Assess stability/function impact |
| 11 | Querschnittsschwächungen | Connections, material defects, biological/chemical attack, fire/explosion | Assess per cause; frequently combines with #4–#6 |
| 12 | Gebrochene Bauteile | Static/dynamic overload, often on a pre-weakened section | Replace, or reinforce/relieve per cause |
| 13 | Abnutzung | Use-related wear, impact, weathering, aging | Replace/reinforce below minimum required section |
| 14 | Verbindungs-Veränderungen | Overload, deformation, biological/chemical attack | Restore load/function capacity of the connection |
| 15 | Stahlteil-Korrosion | Moisture, chemical attack, static load | Assess load/function impact; consider §4.5 stress-corrosion risk |

## 9. Cross-references

- **`timber-steel-design`** — EC5 member and connection design for any
  new or replacement timber sized during a repair; this skill supplies
  the historic-material input (grade, residual section, connection
  geometry) that feeds that sizing.
- **`existing-structures-retrofit`** — the general Bestand structural-
  assessment framework: Bestandsschutz/Nachrechnung mechanics, γM
  reduction under qualified-inventory conditions, Zustandsnote system,
  joist-head repair technique this skill's rafter-foot method mirrors.
  Use it for the load-path/Nachrechnung machinery; use this skill for
  timber-specific diagnosis and repair technique.
- **`building-renovation-refurbishment`** — non-structural/whole-building
  renovation planning (survey workflow, GEG energetic retrofit,
  ecological materials, permits) that a timber-structure repair sits
  inside; that skill hands off to this one for anything touching an
  existing timber roof, floor or frame.
- **`structural-systems`** — load-path/grid concept selection if a
  repair also changes the structural concept (e.g. removing a load-
  bearing Fachwerk wall).
- **`construction-freecad-bim`** — the renovation/retrofit modeling
  workflow (status-tagged Bestand/Neu objects, degraded-material property
  override feeding `run_fem_analysis`) for building a repair into a BIM
  model; §6 residual-capacity values above are the direct input to that
  override.
