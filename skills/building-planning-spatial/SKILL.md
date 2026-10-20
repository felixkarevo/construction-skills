---
name: building-planning-spatial
description: >
  Turn a plot into a dimensionally defensible house plan in the German regulatory
  context (DACH): B-Plan / §34 BauGB read (Maß der Nutzung: GRZ, GFZ, OWZ,
  Bauweise, Zahl der Vollgeschosse, Wandhöhe; Baufenster; setbacks via
  Abstandsflächen der LBO — B-Plan-dependent figures marked VERIFY), envelope test
  (coverage vs. plot-ratio vs. setback bindingness), brief fitting at generic
  international room minimums (retagged, not German law) plus family-house /
  single / duplex / multifamily sizing heuristics, Neufert anthropometric body-
  dimension and movement-envelope tables backing furniture/circulation
  clearances, orientation and sun geometry
  (solar altitude h = 90 − φ ± 23.5°, shading formulas, winter/summer contrast,
  DACH latitude table Berlin/München/Hamburg/Frankfurt), circulation % and NTG
  targets, wet-zone stacking and structural-grid coordination (span rules tagged to
  conception digest), staircase-first and courtyard/light-well placement,
  privacy/noise adjacencies (sleeping-side quiet, cross-ref building-acoustics),
  room-to-room quality checks, one worked example on a generic 600 m² B-Plan site
  (GRZ 0.4 shown as explicit placeholder), compute-don't-eyeball plan verification
  checklist, FreeCAD/BIM handoff (site object, storeys via Arch.makeFloor —
  Elevation-vs-Placement.Base.z gotcha, IFC Site>Building>Storey hierarchy), and
  sibling routing (building-typology, structural-systems, stairs, accessibility,
  building-regulations-permits).
---

# Site and Spatial Planning for Houses (German / DACH Context)

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

This skill turns a plot in the German planning system into a house plan whose
every dimension can be defended: how big the buildable envelope really is under
the Bebauungsplan (or §34 BauGB where none exists), whether the brief fits it,
how large each room should be, how wide passages and stairs must be, where the
staircase and any courtyard go, and which way the house faces for winter sun
and summer shade. Every number carries an evidentiary tier (Section 0): the
*binding* figures are per-parcel (the B-Plan); this document demonstrates the
**method** with clearly-flagged placeholders.

Use it before modelling (handoff Section 14), alongside siblings:
`building-regulations-permits` (authoritative regulatory read — B-Plan text,
state LBO, Genehmigung procedure; this skill **cannot** stand alone there —
Sections 0/9.5), `structural-systems` (spans/grids/load-bearing logic),
`building-typology` (house form, unit configuration), `stairs` (design beyond
5's placement arithmetic), `accessibility-universal-design` (DIN 18040-2),
`building-acoustics` + `building-physics-thermal-moisture` (noise adjacencies,
summer-heat proof).

---

## Reality Check — Licensing & Liability

**This skill produces design aids and calculation guidance for planning and
FreeCAD/BIM modelling ONLY.** Nothing here is a construction document, a
statical calculation, or an approvable planning drawing (genehmigungsfähiger
Entwurf).

- **Bauvorlageberechtigung** (who may sign in/submit Bauvorlagen) is **state
  law** (LBO per Bundesland, MBO-derived: Entwurfsverfasser in the
  Architektenkammer, Tragwerksplaner for stability, limited procedures for
  small buildings in some states). The digested fundamentals source explicitly
  does NOT cover it — treat every licensing statement as VERIFY via
  `building-regulations-permits`.
- A real building needs a **Baugenehmigungsverfahren** (or state exemption/
  notification procedure — VERIFY) proving conformity with the B-Plan or §34/§35
  BauGB, the LBO (Abstandsflächen, Rettungswege, Rauchmelder, Stellplätze) and
  GEG/DIN 4108. **The B-Plan of THIS parcel overrides every GRZ/GFZ/setback
  number printed here — especially the VERIFY-flagged ones.**
- If a user treats output as final (Bauantrag, ordering precast, earthworks),
  say so unprompted: *"Planning study — binding figures come from the parcel's
  Bebauungsplan and the state LBO; a Bauvorlageberechtigter signs and the
  authority approves before anyone builds."*
- Out of scope here: structural design (`structural-systems`,
  `structural-analysis`), seismic (mostly Erdbebenzone 0 per DIN EN 1998-1/NA,
  non-zero at Oberrheingraben + Alpine fringe — VERIFY map; `seismic-design`),
  ground (`geotechnics-foundations`), fire (`fire-protection-building`),
  services. Plan-configuration regularity (2.6) stays here — plan shape is
  decided here.

---

## Section 0: Evidentiary Tiers — Which Numbers Are Law

German residential building law does **not** codify minimum bedroom areas,
kitchen sizes or corridor widths. Binding are (a) the **land-use plan for this
exact parcel** (B-Plan, else §34 context) and (b) the **state building code**
(Abstandsflächen, egress, smoke alarms…). Room sizes are market norms or, for
subsidised/rental stock, programme definitions. State the tier when quoting.

| Tier | Label | Source | Status | Use for |
|---|---|---|---|---|
| **T1** | **Legally binding for THIS parcel** | Bebauungsplan (text + plan), örtliche Bauvorschriften, Erschließungsvertrag; state LBO | Enforceable; approval fails against it | GRZ, GFZ, OWZ, Bauweise, Zahl der Vollgeschosse, Wandhöhe, Baufenster, setbacks, Stellplatzsatzung |
| **T1-V** | **Legally binding in kind, but UNVERIFIED placeholder in this file** | Same category, but this document could not check the figure against a specific B-Plan/LBO text | **Planning placeholder only. Confirm from the parcel's own B-Plan extract / state LBO before anything beyond first-pass massing** | Everything in Sections 1.6, 2, 5.1 that carries a VERIFY tag |
| **T2** | **Codified technical rules (DIN / Eurocode / MBO §-level)** | MBO §§ (Abstandsflächen, Treppen §35), DIN 4108, DIN 4109, DIN 18040, DIN 1986 | Law by reference (Verwaltungsvorschrift) or recognised rules of technology — but **state adoption varies**; digest sources cover only parts | Stair step bands, minimum thermal R-values, sound classes, drainage gradients — VERIFY per state/standard edition |
| **T3** | **International reference floor** | Generic habitable-room minimums (7.5/9.5 m² lineage), openable-window 1/10 practice (German pattern: rough window opening ≥ 1/8 of the floor area, MBO § 47, S.1) | **Not German law.** Sanity floor only | Proving a tight room is not absurd; daylight/vent sanity checks |
| **T4** | **Built practice / market norm** | German housing market: Neufert-derived furniture clearances, common EFH/DHH/MFH sizes | No legal force; reflects buyer/tenant expectation | All room sizes you quote clients; unit-mix sizing |
| **T5** | **Physics / study-backed** | Solar geometry (exact), thermal/moisture research | Geometry is certain; performance numbers are study-specific | Sun altitudes, overhang math, courtyard daylight, overheating logic |

**Hard rules:**

1. **Never present a T3/T4 room-size number as German law.** Say: *"7.5 m² is a
   generic international floor, not a German requirement; the market builds
   12–16 m² bedrooms and buyers expect that."*
2. **Never present a T1-V figure (any GRZ/GFZ/setback in this file) as if it
   had the standing of the parcel's actual B-Plan.** Say *"B-Plan-dependent —
   typical range, VERIFY"* every single time you quote one.
3. **Design to T4; test against T1/T1-V; cite T2/T3 only as a floor.** German
   market reality: a plan built to reference minimums reads as a social-housing
   unit, not a family home, and will resell badly even if it is "compliant."

**What the digested fundamentals do and do not cover** (so you know where this
file stands alone): the source handbook digested for this library covers the
technical basic disciplines (surveying, building physics, construction chemistry,
construction IT/CAD/BIM, structural mechanics, reliability) and **explicitly
does not contain** the Bauleitplanung procedure, Bauvorlageberechtigung, HOAI
phase logic, or the permitting process. Where Section 1.1 sketches the FNP →
B-Plan chain, it is common-knowledge framework for orientation — **VERIFY the
procedure and every §-citation against `building-regulations-permits`.**

---

## Section 0.5: The Working Sequence

In order. Skipping steps 1–2 wastes every later decision: the envelope
determines the brief, never the reverse.

```
1. READ THE PLAN      B-Plan? get text + key plan; else §34 (1.7). Extract Art
                      der Nutzung, GRZ, GFZ, OWZ/Vollgeschosse, Wandhöhe,
                      Bauweise, Baufenster, setbacks. Anything not read from
                      the parcel's own plan = VERIFY placeholder, said aloud. → §1
2. FIX THE ENVELOPE   footprint vs GRZ vs Baufenster vs Abstandsflächen; floors
                      vs GFZ; height vs clause. Adopt the most restrictive. → §2
3. TEST THE BRIEF     rooms at T4 sizes vs available NRF. If it doesn't fit,
                      resolve NOW, not in plan. → 3.8
4. FIX ORIENTATION    φ → sun altitudes; street/noise side; shading geometry.
                      Free now, impossible later. → §6–7
5. PICK THE ARCHETYPE Bauweise + frontage + brief + depth. → 8.8 tree
6. PLACE THE STAIR    before any room; compute risers from the real F2F. → §5
7. PLACE COURT/WELL   W/H vs winter sun altitude at THIS φ; roof/floor cut =
                      diaphragm item (2.6). Tight row → Lichtschacht, honestly
                      named. → §6
8. LAY OUT ROOMS      T4 sizes, wet stacks, quiet-to-quiet, buffers to street/
                      north. → §3, 9, 11
9. VERIFY             GRZ/GFZ/height/setbacks/circ%/NTG/openable/W-H/regularity.
                      Compute; do not eyeball. → §10, 12, 13
10. STATE THE CAVEAT  study status + named unverified placeholders + per-decision
                      2.6 flags, attached to the decisions, not as boilerplate.
```

**Rule:** never reach step 5 with step 1 unresolved — *"assume GRZ 0.4"* is how
plans die after they are drawn.

---

## Section 1: The German Planning Read — FNP, B-Plan, §34

### 1.1 The Bauleitplanung chain (framework — VERIFY procedure against `building-regulations-permits`)

Two-tier statutory land-use planning (BauGB):

```
Flächennutzungsplan (FNP)          preparatory land-use plan, municipality-wide,
        │                          not binding on the citizen — binds the
        ↓                          administration
Bebauungsplan (B-Plan, Bebauungsplan der Innenentwicklung §13a /
        │            Regel-Plan §12)   qualified urban development plan: legally
        ↓                            binding for every parcel it covers
Bauvorlage + Baugenehmigung        the individual building permit checks the
                                   project against the B-Plan (§30 BauGB:
                                   "zulässig", wenn nicht die Festsetzungen
                                   widersprochen wird)
```

- **Inside a B-Plan → §30 BauGB:** every Festsetzung governs: use type, measure
  (GRZ/GFZ/OWZ), Bauweise, Vollgeschosse/Wandhöhe, überbaubare Fläche
  (Baufenster/Baugrenze), street setback — sometimes roof form, wall caps,
  planting duties.
- **No B-Plan, parcel inside a zusammenhängende Bebauung → §34 BauGB
  ("im Innenbereich"):** the project is to be approved if it *fits the
  surrounding character* (Eigenart der näheren Umgebung) in use-type, measure
  and construction method and Erschließung is secured. **§34 has no numbers** —
  you *derive* the envelope by measuring what is built around you (1.7).
- **Außenbereich → §35 BauGB:** building outside settled areas is in principle
  not permitted (privileged uses excepted). If a user's plot is Außenbereich,
  stop and route to `building-regulations-permits` — spatial design is moot.

### 1.2 Art der baulichen Nutzung — what the plan lets you build

BauNVO area types you will meet on residential plots (the B-Plan states one;
VERIFY per plan):

| Code | Type | What it allows |
|---|---|---|
| **WA** | Allgemeines Wohngebiet | Dwelling-dominated; small businesses run by residents tolerated |
| **WR** | Reihenhausgebiet | Row houses only — single/duplex row typology forced |
| **W**   | Allgemeines Wohngebiet (old plans) / **Kleinsiedlungsgebiet KS** | Small-lot housing; often tighter GRZ |
| **M**    | Mischgebiet | Living + non-disturbing trade — noise exposure from the trade side, see 7.6 |
| **MD/MI**| Hochhaus-/Urbanisierungsbereiche, Sondergebiete | Dense/urban variants — special rules, pull the plan |
| **S**    | Sondergebiet | Purpose-specific (e.g. "Wohnen und Gastronomie") — read the text, nothing standard applies |

**Consequence:** WR = row segment; WA+offen = single or duplex ("Einzel- und
Doppelhäuser" — plan text); WA+geschlossen = row segment even on wide plots.
**Section 8's tree starts from Bauweise, not taste.**

### 1.3 Maß der baulichen Nutzung I — GRZ (Grundflächenzahl)

**GRZ = buildable ground area ÷ plot area** (§17 BauNVO; the measure includes
*all* covered ground surfaces — see the trap below).

- B-Plan-dependent, typical WA/WR range roughly **0.2 – 0.6** (common row-house
  plans 0.25–0.4; dense urban quarters up to ~0.6). **VERIFY — these are ranges
  remembered from typical plans, not from the digested sources, which contain no
  GRZ values at all.**
- **What counts (the trap):** footprint + garages/Carports + Stellplätze +
  Zufahrten + befestigte Wege + terraces (plan wording) + Aufschüttungen —
  the B-Plan text defines the list and may grant half-credit ("Minderanrechnung"
  — VERIFY). A 150 m² house on 600 m² is GRZ 0.25 until drive + carport push
  0.38. **Tally the whole plot's paved surfaces, not just the house.**

### 1.4 Maß der baulichen Nutzung II — GFZ and OWZ

**GFZ = total gross floor area of all storeys ÷ plot area** (§19 BauNVO,
measured to the outer face of the enclosing walls, per storey, in principle
*above ground*).

- B-Plan-dependent; typical residential range roughly **0.2 – 1.2**
  (EFH/EFH-Reihen plans commonly 0.25–0.6; row-house plans ~0.4–0.8; dense
  blocks higher). **VERIFY — no GFZ value exists in the digested sources; every
  number here is a placeholder for demonstration.**
- **What counts (rule-of-thumb — the local calculation ordinance governs,
  VERIFY):** fully-served storeys count; the **Keller usually does not** if it
  lies below the terrain line it is measured from (a walk-out basement on sloping
  ground can count on its daylit face — the single most common §34-argument in
  German practice); **Dachgeschoss/Renaissance counts where rooms are
  habitable-served**, plan-text dependent; balconies/loggias commonly only a
  fraction (e.g. half) in modern plans — **always the plan text.**
- **OWZ (Obergeschosszahl / Zahl der baulichen Anlagen — some plans) vs "Zahl
  der Vollgeschosse":** the plan expresses height either as a fixed number of
  full storeys (with eaves height limits, often "2-Vollgeschosse, Wandhöhe
  7,00 m" style — placeholders) or as a maximum wall height. A Vollgeschoss is
  classically a storey whose ceiling is ≥ half above the adjoining terrain
  (plan-text definitions vary — VERIFY).

### 1.5 Height and roof: Wandhöhe, Vollgeschosse, Dachform

- **Wandhöhe**: height of the exterior wall up to the eaves/roof edge, measured
  from the *determined* terrain (often "Mittelgelände" or the street-side
  sidewalk line — **the plan states its own measure line; VERIFY; this decides
  whether a "2½-storey-looking" house is 2 or 3 full storeys on paper**).
- **Dachform/Dachneigung**: many WA/WR plans fix flat / dual-pitch / hip and a
  pitch band (e.g. 22°–38° — plan-dependent). This forces roof volume and
  usable DG area; some newer plans additionally set a PV clause or
  Solarpflicht (state law) — **VERIFY plan graphics before shaping the roof.**
- If the plan says nothing on roof: fit the neighbours under §34.

### 1.6 Where you may stand: Baufenster, Bauweise, Abstandsflächen

Three independent controls that each can bind — run all three, adopt the
smallest buildable rectangle:

1. **Baufenster / überbaubare Fläche (B-Plan).** The plan draws a buildable
   window: front distance from the street boundary (commonly ~5–10 m —
   placeholder), lateral reach, sometimes depth. **Outside the Baufenster you may
   not build** except minor exemptions the plan text lists (porches, single-
   storey annexes ≤ x m² — VERIFY per plan).
2. **Bauweise (BauNVO §16).** *offen*: single/double houses, touching only at
   short sides; *geschlossen*: segments built together at the front line. The
   classical offen side-gap (3.0 m/side ⇒ 6 m between houses) is older-rule/
   plan-dependent, VERIFY — and usually superseded by (3).
3. **Abstandsflächen (state LBO, from MBO §6).** Even inside the Baufenster you
   must keep a setback from each boundary: the common formula family is
   **A ≥ 3.00 m and A ≥ 0.4 × H** (H = wall/storey height relevant per state
   definition — some states 0.4H to eaves/roof top, some count only storeys;
   **state law, VERIFY; digested sources do NOT contain the formula — only the
   concept that these legal distances must hold in setting-out**). A reduced or
   zero setback needs the neighbour's documented *Abstandsflächenerklärung /
   Grenzerleichterung* (BauNN). **Boundary walls/garages: many states allow
   low ancillary structures directly on the boundary up to a length/height cap
   (e.g. ~3 m wall, ~9 m length, ~3 m height — classic MBO-derived figures,
   VERIFY in your state).**

**Setback-vs-coverage interaction (universal logic, kept):** On a 24×25 m plot
with 3 m side setbacks, setback-buildable width is 18 m; a GRZ 0.4 cap of
240 m² may bind instead (18 × 13.4 = 240). **Always run all three and adopt the
smaller footprint; always re-confirm which of them binds in the plan text.**

### 1.7 §34 fallback — deriving the envelope without a plan

No B-Plan (typical for Baulücken in old quarters, village insets, outer suburban
streets): you must document the *Umgebungsanalyse*:

```
1. Map the 3–5 nearest comparable parcels (same side, similar width): build
   depth off street, storeys, eaves height, footprint/plot ratio, Bauweise, roof.
2. Form the range (e.g. neighbours 6.5–9 m off street, 2+ADG, eaves 6.8–7.4,
   footprint 0.28–0.42 of plot).
3. Sit inside the range; the middle is the defensible claim, extremes invite
   objections. 4. Write the derivation down BEFORE designing — the Bauamt
   asks (Bauvorlagen → building-regulations-permits).
```

**Numbers from this method are survey facts (measured), not law — they are as
citable as a §34 opinion can be. VERIFY with the authority in a
Bauvorbescheid (pre-decision, §72-BauGB-analog state provision — VERIFY) when
the envelope is tight.** A Bauvorbescheid before designing a full plan is the
German equivalent of "ask first" — recommend it whenever §34 ranges are wide.

### 1.8 Plot geometry — metric, and frontage is still the binding constraint

German plots are metric — but the *frontage trap* is universal and sharper in
Baugebiete, because parcels of identical area differ wildly in shape (300 m²
at 10 × 30 m vs 17 × 18 m are different buildings).

| Frontage (B-Plan row plots) | What fits across the width (after 3 m setbacks or party walls) | Plan structure forced |
|---|---|---|
| 5.5–7 m (WR row segment) | one 3.5–4.5 m room bay + 1.25 m circulation/core | Row segment: rooms front/back, stair along one side |
| 8–10 m (DHH half-plot, one side built to boundary) | 5.5 m room + 1.0 m stair on shared line, or 2 bays | Duplex: stair on party side, garden axis to the open side |
| 12–15 m (offene Bauweise EFH) | 6 m living + 1 m gap + 5.5 m room, or room+Flur+room | Freistehend: full room-to-room plans possible |
| 16–20 m (large EFH / small MFH) | 3 bays: 5.5 + core 1.5 + 5.5 + ... | MFH starting point: 2 units per floor back-to-back |

Deduct: two 24–36.5 cm external walls ≈ 0.5–0.7 m gross-to-clear across the
width (wall thickness Section 9.3), plus ~12 cm per crossed internal wall.
**When a client can choose a 15 × 40 m parcel or a 20 × 30 m parcel of equal
area, the wider one is materially more plannable — frontage, not area, binds
the section of the plan.**

### 1.9 Orientation nomenclature

Parcels are described by street/garden side: "Südgarten" (garden south) is the
market premium; north street + south garden is ideal and common in rows. Street
side = entrance + noise side (7.6); garden side = winter-gain facade. **West-
garden plots need the shading + buffer strategy from day one (7.2–7.4).**

---

## Section 2: The Envelope Test — GRZ, GFZ, Height, Setbacks

### 2.1 Placeholder schedule for the worked example (T1-V — NOT a real plan)

The generic 600 m² site used in Sections 2.2 and 12.5 assumes:

```
Bebauungsplan (hypothetical, method demonstration ONLY):
  Nutzung     WA, offene Bauweise (Einzel- + Doppelhäuser)
  GRZ 0.4 · GFZ 0.8 · VGS 2 (+ ausgebautes DG? — placeholders, VERIFY)
  Wandhöhe bis 7,10 m (placeholder); Baufenster ab Straße 8 m, hinten ≥ 3 m
  Side setbacks per LBO: A = max(3.0 m, 0.4·H) — formula family, VERIFY
  2 Stellplätze/WE; garages/Carports count (full or half) against GRZ per
  plan text — VERIFY.
```

Replace every line with the parcel's actual plan before the study leaves the
drafting table — the arithmetic below is the product; the numbers are props.

### 2.2 What the placeholders permit — the arithmetic, method-valid regardless

600 m² site, GRZ 0.4 / GFZ 0.8, 2 full storeys (+optional DG):

| Quantity | Calc | Result |
|---|---|---|
| Max ground area (whole-plot, incl. paving!) | 600 × 0.4 | **240 m²** |
| House footprint if driveway+carport eat 60 m² | 240 − 60 | **180 m² house** |
| Max gross above-ground floors (GFZ) | 600 × 0.8 | **480 m²** |
| → floors at full 240 plate | 480 / 240 | 2.0 → **exactly 2 storeys** |
| → floors at 180 plate (realistic) | 480 / 180 | 2.7 → 2 floors + DG ~100 m² |
| Keller (walk-in, under house, plan-exempt — VERIFY) | excluded from GFZ per placeholder reading | − |

**Reading it (method holds for any confirmed figures):** GRZ binds the ground
(every paved m²); GFZ binds total floors; the height clause binds the storey
number; the Keller lever (if plan-exempt AND buildable, 2.4) is the German
version of "the biggest lever on a tight plot".

**Massing decision tree:**

```
Client wants N m² gross above-ground on plot A with (GRZ, GFZ):
 ├─ N ≤ A×GRZ_eff        → single storey; garden maximised; done.
 ├─ N ≤ 2×plate & ≤ A×GFZ → 1.5–2 storeys at full plate.
 ├─ N ≤ A×GFZ, > 2×plate  → 2 storeys + DG — DG counts GFZ only if the plan
 │                           says so: VERIFY before banking it.
 └─ N > A×GFZ             → not permissible as drawn: (a) cut brief (3.8),
                            (b) Keller if plan-exempt + soil OK, (c) larger
                            plot/zone, (d) §34 measured-surroundings argument
                            or Bauvorbescheid before designing more.
```

### 2.3 Setback check worked on the placeholders

House 18.0 × 10.0 m, Wandhöhe (eaves, flat roof) 6.30 m, plot 24 wide × 25 deep:

```
Side:   A = max(3.00, 0.4×6.30 = 2.52) → 3.00 m per side (formula family VERIFY)
        buildable width 18.00 ≥ 10.00 house width ✓
Front:  Baufenster at 8.0 m street setback → rear gap 25 − 8 − 10 = 7.0 ≥ 3 ✓
GRZ:    house 100 + drive 40 + paths/carport 35 = 175 ≤ 240 ✓
VERDICT: here the Baufenster binds position and GRZ the paving budget; on
         narrower plots the setbacks bind. RUN ALL THREE; state which binds.
```

### 2.4 Basement caveats (German)

- GFZ/GRZ treatment of the Keller is **plan-text law**: recurring clause
  families cap the exposed basement wall height above mean terrain (≈ 1.0 m
  class) or count daylit faces — **VERIFY the wording.**
- Physical: water table/flooding (Hochwassergefahrenkarten — state maps; since
  2021 "HQ-extrem" is a standard question; `geotechnics-foundations`): legal
  and buildable are different tests; run both before recommending the Keller lever.
- Cost is volatile — never quote a Keller price from memory; but relative
  logic holds: a GFZ-exempt Keller often buys more legal area than the next
  plot band.

### 2.5 Non-negotiable open space, whatever the plan allows

Even at GRZ 0.6 legal ceilings, reserve:

- **Rear open depth ≥ 3 m** behind south-glazed living: without it the terrace
  is a light-well and the winter-gain facade gains nothing.
- **One buildable-free strip to a boundary** unless the plan's Abstandsflächen
  are formally waived — neighbours later build to the line; windows at 3 m face
  windows (privacy: Section 7.6).
- **Stellplätze + manoeuvring** (3.7) with GRZ accounting of ALL paved m².
- **Haustechnik-Zugang**: tank/plant access, rainwater cistern (many plans
  require retention — Rückhaltung nach Entwässerungssatzung, VERIFY),
  Kelleraußentreppe egress.

### 2.6 Plan-configuration risk — what THIS skill controls

Full seismic design is `seismic-design`'s and the Tragwerksplaner's (Germany:
mostly DIN EN 1998-1/NA zone 0; Oberrheingraben + Alpine fringe non-zero —
VERIFY the map for the site). But German practice regularity issues that get
decided HERE and cannot be undone later are the same physics everywhere:

| Plan decision made here | Risk if careless | Mitigation at planning stage |
|---|---|---|
| L-shape / re-entrant corner | torsional concentration at the inner corner (seismic AND differential-settlement AND rendering-crack classic) | wings ≤ 1:3 aspect; movement joint or slip joint at the re-entrant; tell `structural-systems` explicitly |
| Courtyard / Atrium cut | diaphragm hole: floor load redistribution around the void | centre the cut; edge beams all four sides; flag as design intent, not detail afterthought |
| Long single-bay wing (Galerie, "Haus am Hang") | soft/weak axis, big eccentricities | keep width:length ≤ ~1:4; intermediate cross walls per `structural-systems` |
| Split levels on slope | discontinuous shear path at every offset | on zones 0: usually acceptable, watch crack control; on 1–2: prefer terraced full floors — route to `seismic-design` |
| Columns stranded off grid | irregular load path, cost | 9.4 rule 1 |

**Handoff rule:** whenever Section 8's tree lands on an L, a court, a long wing
or a split level, write the specific note into the model handoff — "re-entrant
corner at grid C/4 — check for seismic zone per national annex + settlement
joint", not a generic disclaimer.

---

## Section 3: Room Program — Generic Minimums vs What the German Market Builds

### 3.1 Generic international reference minimums (T3 — NOT German law, VERIFY never needed because nothing here binds)

German public building law sets **no minimum room sizes** for owner-occupied
houses. The table below is the generic international habitable-room lineage
(metric restatement) — keep it only as a sanity floor:

| Space | Generic floor | Note |
|---|---|---|
| Habitable room, single-room dwelling | 9.5 m² | absolute floor |
| Other habitable rooms (bed, living, dining) | 7.5 m² | ≈ 2.7×2.8 m |
| Kitchen, separate | 5.0 m² | |
| Bathroom (bath only) | 1.8 m² | |
| WC only | 1.1 m² | |
| Combined bath + WC | 2.8 m² | ≈ 1.5×1.9 m |
| Window openable sanity | ≥ 1/10 of floor area | practice rule, not DIN |
| Window size, German pattern | rough opening ≥ 1/8 of the net floor area | MBO § 47, read again in three books (S.1); some states accept 1/10. Governs where the two differ |
| Ceiling height | 2.50 m | state LBOs commonly require "angemessene Höhe"; many fix ≥ 2.40–2.50 m for Wohnräume — **T2, state-specific, VERIFY**. MBO: at least 2.40 m clear (S.1) |

**German-law adjacents you must not confuse with these:** DIN 18040-2
(barrier-free — binding only if claimed/subsidised), state Wohnraum definitions
and the **Zweckentfremdungs-/Ortspolizeirecht** of tight housing markets (a
too-small or windowless room may not count as a lettable bedroom — city-
specific, VERIFY). None of them make 7.5 m² a marketable bedroom anywhere in
DACH practice — see 3.2.

### 3.2 German built-practice targets (T4) — design to these

Interior clear, single/duplex house (EFH/DHH/Reihenmittelhaus), typical new-build
band (market convention — no legal force; verify against the buyer's expectations
and the resale norm):

| Space | Compact (row/DHH) | Comfortable (freistehend) | Generous |
|---|---|---|---|
| Wohnen (living) | 22–26 | 28–36 | 40–55 |
| Essen (dining, incl. open to kitchen) | within Wohnen | 12–16 | 16–20 |
| Kochen (kitchen) | 7–9 | 10–14 | 14–20 (Wohnküche) |
| Schlafen Eltern | 12–14 | 15–18 | 18–24 (+Ankleide 5–8) |
| Kinderzimmer | 10–12 | 12–15 | 15–18 |
| Arbeits-/Gästezimmer | 9–11 | 12–14 | 14–18 |
| Bad ( Eltern, Wanne+Du+WC+2 Waschtische) | 5.5–6.5 | 7–9 | 10–14 |
| Bad (Kinder, Du+WC+WT) | 4–5 | 5.5–7 | 7–9 |
| Gäste-WC | 2.2–3 | 3–4 | 4–6 |
| Diele/Flur (EG circulation) | 6–9 | 9–14 | 14–20 |
| Hauswirtschaftsraum (HWR, waschen+heizen) | 5–6 | 7–9 | 10–14 |
| Abstellraum | 2–3 | 3–5 | 5–8 |
| Treppenhaus WF-Anteil (EG+OG combined) | 8–11 | 11–14 | 14–20 |
| Technik/Anschluss (within Keller or HWR) | 3–5 | 5–8 | 8–12 |

All areas in **m²** (Wohnfläche logic: 100 % floor area; under a DG slope floor with a
clear height of at least 2 m counts in full, between 1 m and 2 m at half, below 1 m not at
all — Wohnflächenverordnung, **T2, VERIFY when the number is sold as WFL**; §3.4).

**The gap between 3.1 and 3.2 is the point.** 7.5 m² is not a German bedroom —
it is a child's room from the 1960s. Quote 3.2 to clients; keep 3.1 only to
defend a squeeze.

### 3.3 Furniture-driven minimums (why 3.2 is what it is — universal geometry)

**Bedroom** — German bed formats 180×200 / 140×200 / 90×200. Clearance
(Neufert-lineage, T4): side circulation **750 comfortable / 600 absolute** one
long side, 600 the other; foot-of-bed to swinging wardrobe **900** (700
sliding/no door); Schrank 600 deep + 900 standing zone. Minimum workable
parents' room: 1.80+0.75+0.60 = **3.15 m** × 2.00+0.90+0.60 = **3.50 m** ≈
**11 m² clear** → why 12–14 m² is the compact market floor, 15–18 comfortable.

**Kitchen** — counter 600 deep, wall cabinets 350–400; aisle **1000–1200**
(two-cook 1200+); work-triangle perimeter **4.0–8.0 m**; island needs 1000+
clear all working sides; dishwasher door + 900 in front; German kitchen sill
standard **1000 mm** over a 900 counter.

**Bathroom** — WC **600 mm** side clearance to obstacle, ≥500 (comfort 600)
front (DIN 18040-2 accessible = 900×1200 + side transfer — route
`accessibility-universal-design`); Waschtisch ≥500/700 front; Dusche **90×90 min**,
100×120 comfort, bodengleich = value + ageing; minimum honest 3-fixture bath
1.8×3.0 ≈ **5.5 m²** — below that, split the WC out.

**Dining** — 600 per seated person, **≥900** behind chairs to pass (700 to
pull out); 6-seat 1.60×1.90 + 0.9 all round → 9.2 m² core, the 12–16 band adds
circulation overlap + sideboard.

**Wohnen** — 3-seater + armchair + TV wall ≈ 3.5×4.5 m clear minimum liveable
(16 m² hard floor); 25–35 m² is the norm because German Wohnen also carries
the Essplatz or a desk corner.

**Where these numbers come from:** every clearance above is a derived rule; the
raw anthropometric body-posture and reach envelopes underneath it (the actual
Neufert "little man" pages) are tabulated in **3.9** — use that table when a
brief squeezes a clearance below what's printed here and you need the body
geometry it will violate, not just the market convention.

### 3.4 Ceiling heights and floor-to-floor (German defaults)

| Space | LBO-ish floor (T2, VERIFY per state) | Market practice (T4) |
|---|---|---|
| Wohnräume | ≥ 2.40–2.50 | **2.60–2.80** (KfW-efficiency houses often 2.60–2.70 to cut envelope volume) |
| Bad/HWR/Flur | — | 2.30–2.60 (often lowered for installation level) |
| Unterzug clear at escapes/doors | ≥ 2.00 (MBO lineages, VERIFY) | keep ≥ 2.10 |

**Attic storey under a pitched roof (Dachgeschoss, Kniestock/Drempel).** The knee wall is
the outer wall along the eaves that rises above the attic floor before the roof starts; it
lifts the slope and with it the floor one can stand on. Under the slope the clear height
falls towards the knee wall, so a room there has no single height. Bavaria asks 2.40 m clear
for a habitable room, in the attic 2.20 m over half of its floor, where parts lower than
1.50 m are not counted; this does not hold for habitable rooms of residential buildings of
classes 1 and 2 (S.1). For the living area, floor under a clear height of at least 2 m
counts in full, between 1 m and 2 m at half, below 1 m not at all (Wohnflächenverordnung,
**T2, VERIFY**). A local design statute may cap the knee wall (S.4); how the model draws one:
S.3.

**F2F default:** clear 2.70 + RC buildup 0.20 (or timber 0.30–0.38) →
**F2F 2.90–3.05; use 2.90** as worked default. Every +100 mm costs façade,
stairs and (on many plans) the next Vollgeschoss reading — check 1.4 first.

### 3.5 Program elements the German market expects (T4) that foreign manuals omit

Omitting these reads as amateur on a DACH resale:

| Element | What it is | Planning rule |
|---|---|---|
| **Gäste-WC** | Half-bath off Diele | 2.2–4 m², window or Belüftung, NOT off the open Wohnbereich sightline; under-stair location classic (headroom rule 5.2) |
| **HWR** | Hauswirtschaftsraum | washer+dryer+boiler/heizung+circ pump; adjacent to kitchen and to the Keller stair; stack wet-on-wet (9.1) |
| **Kellertreppe within Diele** | basement access | inside the thermal envelope; landing ≥ door width; headroom to door |
| **Abstellkammer** | pantry/storage near kitchen or Diele | 2–4 m² at 350–400 depth fits the vacuum/shelves |
| **Hausanschluss** | utility entry (Strom-KH, Wasser, Abwasser revision, Telecom, PV backup) | 1.0–1.5 m² wall of the Diele/Keller; NEVER a finished room's wall face; coordinate `building-services-tga` |
| **Geschossübergang TGA-Schacht** | stacked wet/installation duct | 9.1 |
| **Kaminofen / herd** | stove flue | early: flue line through floors + roof, non-combustible floor zone — route `building-services-tga`/fire |
| **PV + Speicher/Wallbox** | energy | roof zoning (9.6) + wallbox circuit at Stellplatz |
| **Gartengeräte-/Fahrradraum** | garden/storage | 4–8 m², external door, floor drain; plan vs GRZ (annex counting!) |

### 3.6 Bedroom count and unit mix heuristics (T4)

```
Bedrooms = parents + 1 per child + guest/office if space (+1 Arbeitszimmer
per remote-working adult, or double-duty guest).
EFH/DHH family (2+2): 3–4 SZ + 2 Bad + GWC + Wohn 30–40 + offenes Koch-Ess
→ WFL 110–145 → gross ×~1.35 (walls/stair/Flur) → 150–195 m² → at placeholder
GRZ 0.4 needs two storeys from ~300–350 m² plot up (Section 2.2 math).
Single/2-person ("Seniorengerecht"): 2 SZ + barrier-leaning Bad + Wohn-Koch
35–50 → EG-only or 1.5-storey.
DHH: EFH × ~0.85; mirror with the neighbour — stair + wet zones on the party
line so each half's baths sit on baths (9.1).
MFH (3–8 units) market bands (VERIFY local demand): 1-ZKB 32–45 · 2-ZKB 52–65 ·
3-ZKB 68–85 · 4-ZKB 88–110 m² WFL; every unit 2 aspects or corner
(single-aspect only ≤ 50 m²); depth/economics → `building-typology`.
```

### 3.7 Parking (Stellplatz — dimensions + the GRZ trap)

- Bay **2.50×5.00 min / 2.75×5.50 comfort**; SUV 2.75×6.00; between adjacent
  cars +0.75 for doors (garage box 3.0×6.0 single / 5.0×6.0 double class).
- Garage clear height ≥ 2.00 under the door; sectional heads 300–500 (product).
- Drive ≥ 3.00 m; reversing into a 2.5 m bay from a 5 m drive needs ~6 m
  behind — on narrow plots make it one-way or pull the garage INTO the house
  (hits GFZ-free wall area, spares GRZ paving).
- **Every paved m² is GRZ money (1.3): count Stellplätze FIRST, then design
  the house with what remains.**

### 3.8 Area budgeting — does the brief fit the envelope?

Do this **before drawing anything**. Arithmetic; two minutes; prevents the classic
failure: a plan that "fits" only because every room was quietly shrunk 12 %.

```
STEP 1  Available gross above-ground = A × GFZ           (Section 2 — PLACEHOLDER
                                                         figures; re-run with the
                                                         parcel's own plan)
STEP 2  Available usable (NRF/WFL)   = gross × NTG      (Section 10.2 targets)
STEP 3  Required                     = Σ T4 room areas (3.2) + circ allowances
STEP 4  Compare:
        Required ≤ 0.95 × Available  → comfortable, proceed
        0.95–1.05                    → tight; lose a store or a room NOW
        > 1.05                       → does not fit. Resolve:
          (a) drop/merge a room  (b) DG/Renaissance if height clause allows
          (c) Keller (GFZ-exempt? plan-text law — VERIFY)
          (d) bigger plate via different plan zone / §34 argument
```

**Worked — the generic 600 m² family brief (4-person household):**

```
Envelope (placeholders): gross above-ground = 600 × 0.8 = 480 m²
NTG 0.75 → usable ≈ 360 m² over 1.5–2 storeys.
Required at T4 (comfortable band): Wohnen 32 + Essen 14 + Kochen 12 +
Eltern 16 + Ankleide 6 + 2× Kinder 13 + Arbeits 12 + Bäder 8+6 + GWC 3 +
HWR 8 + Abstell 4 ≈ 137 m² of rooms + Diele/Flur 14 + Treppe 12 ≈ 163 m².
Ratio 163 / 360 = 0.45 → fits on TWO floors with ~55 % margin — but the real
binding constraint here is GRZ (house footprint + ALL paving, 1.3) and the
height clause (DG legality), not GFZ area. Client summary: "floor area is
legal; the ground is the limit." If the brief had scored > 1.05 instead,
that would be resolved HERE (drop/merge/plot), never by shrinking every room.
```

**Rule:** when a brief scores > 1.05, put this arithmetic in front of the
client in exactly this form. It converts a taste argument into a numbers
argument, and the numbers win.

### 3.9 Anthropometric basis — body dimensions and movement envelopes (T4, Neufert Measurement-Basis chapter)

3.2's room bands and 3.3's furniture clearances are *derived* numbers. This
subsection tabulates the primary anthropometric data they were derived from —
the "Man: Dimensions and Space Requirements" plates of Neufert's
Measurement-Basis chapter (English ed., Neufert_2002.pdf excerpt, pp. 16–17;
the classic "little man diagram" lineage referenced generically at 3.3 and in
the tier table, Section 0). **These are body-and-movement geometry, not a
DIN standard and not German law** — where DIN 18040-2 (barrier-free) requires
a larger clearance, DIN 18040-2 wins; route `accessibility-universal-design`.
Use this table when a brief pushes a clearance below the 3.2/3.3 market band
and you need to show the client the body it will no longer fit, not just the
convention it violates.

**Static body-posture envelopes** (p.16, figs 1–12 — average adult, normal
dress):

| Posture | Plan envelope | Height | Planning use |
|---|---|---|---|
| Standing, arms at side (profile) | 300 mm | — | baseline silhouette; cf. Modulor 1.75 m figure (Section 0/p.15) |
| Standing, arms akimbo / hands on hips | 875 mm | — | dressing-area, WC-cubicle sizing |
| Standing, one arm raised overhead | 875 mm | reach to 1.50–1.75 m | wall-cupboard top shelf |
| Standing, both arms spread sideways | 1125 mm sweep (500 mm shoulder box) | to 1.75 m | wardrobe/workbench full-reach arc |
| Bending forward, hands to floor | 875 mm | 1.375 m | bed-making, cleaning-access strip |
| Kneeling upright, sitting on heels | 875 mm | 1.00 m | floor-level storage/work |
| Squatting, full crouch | 625 mm | — | low-shelf/low-cupboard access |
| Sitting cross-legged on the floor | 750 mm | 0.875 m | — |
| Sitting cross-legged, upright | 700 mm | 1.125 m | — |

**Furniture-envelope dimensions** (p.16, figs 13–20):

| Item / task | Plan footprint or reach | Heights | Cross-ref |
|---|---|---|---|
| Work table, seated | 875 mm width | seat 450–480; table 750–800; overhead reach 1350 | validates 3.3's desk/table sizing |
| Dining/side chair, pulled out | 875 mm depth | seat 400–450; back 750 | ≈ 3.3's dining "≥900 behind chairs / 700 to pull out" |
| Small easy chair | 900–1000 mm depth | seat 375–400; arm 600; back 700 | Wohnen seating footprint (3.2's 25–35 m²) |
| Armchair | 1250 mm depth | seat 250–350; arm 625 | — |
| Standing work-counter, forward reach | 660 mm | counter 900; overhead shelf 1500; standing eye ~1930 | validates the 900/1000 mm kitchen-counter/sill pair (3.3) |
| Kneeling reach (low unit) | 710 mm depth | reach band 460–1220 | |
| Seated reach | 860 mm | to 1450 | |
| Squatting reach | 710 mm | 300–1020 | |

**Bed and sleeping-zone envelopes** (p.16, figs 21–24 — read together with
3.3's bed-clearance arithmetic):

| Activity at the bed | Zone | Clear height | Cross-ref |
|---|---|---|---|
| Sitting on the edge, reaching a bedside shelf | 1250 mm | 875 mm to shelf | underlies 3.3's foot-of-bed 900 mm swing zone |
| Reclining, reading | 1500 mm | 750 mm to any overhead obstruction | headboard-side shelf clearance |
| Sitting up in bed | 1625 mm | 625 mm | matches a 1.60 m-wide bed + one-side reach |
| Lying full length, arm extended | 2000 mm envelope; 1875 mm clear length; 300 mm past the feet | — | sets the **minimum clear depth behind a bed at ≈2.0 m**, before 3.3's 750/600 mm side clearances are even added |

**Circulation and passing widths** (p.17, "Space Requirements" plate — captioned
explicitly: **"for moving people, add >10 % to widths"**):

| Configuration | Width | DACH cross-ref (this skill) |
|---|---|---|
| One person, sideways/profile | 375 mm | — |
| One person, facing | 625 mm | ≈ the T3 absolute-floor corridor width (4.1) |
| One person, arms akimbo | 875 mm | — |
| Two people passing | 1000 mm | = the T4 "Flur serving 1–2 rooms" 1000 mm width (4.1) |
| Two people abreast | 1150 mm | ≈ the 1100–1250 mm "Flur serving 3+ rooms" band (4.1) |
| Three people abreast | 1700 mm | Diele/entrance-hall scale (4.4's 1400–1800 mm) |
| Four people abreast | 2250 mm | public-corridor/landing scale, not residential Flur |
| Closely packed standing row | 1250 mm/person-row | crowd reference only |
| Waiting queue | 2125 mm | — |
| Pace length, walking in step | 750 mm | stride cross-check against the stair tread band (5.1, 260–300 mm) |
| Reach, kneeling down | 1125 mm | under-stair storage clearance cross-check (5.2) |
| Reach, standing at full stretch | to 2250 mm | ceiling/top-shelf planning |
| Person carrying one case | 800–1000 mm | Diele shoe/coat niche depth (4.4) |
| Person with an open umbrella (two together 2375 mm) | 1125 mm | entrance canopy / vestibule depth (7.5 Windschutz) |

**Reading it for this skill:** none of this table overrides 3.2's market
targets or 4.1's Flur widths — it is the body-geometry floor those numbers
were built on, and it is what to show a client who wants to cut a passage to
700 mm or a bed clearance to 400 mm: below the one-person-facing envelope
(625 mm) or the two-people-passing envelope (1000 mm), the room stops working
as a room, independent of any code minimum. **Cite as:** Neufert, Architects'
Data (English ed., Neufert_2002.pdf excerpt), p.16 (body measurements/
furniture) or p.17 (space requirements/circulation).

### 3.10 Outdoor space on a storey — loggia, balcony, roof terrace

A **loggia** is a covered outdoor space recessed into the outline of the house: walls
on the sides it shares with rooms, open on the others. A **balcony** projects beyond
the outline; a **roof terrace** lies on the roof of a room below. All three are
outdoor space, not rooms: not heated, not habitable, no daylight or minimum-area rule
of their own.

- **Envelope.** The walls between an outdoor space and a heated room are outer walls
  of the thermal envelope (`building-physics-thermal-moisture`); the open sides get no
  wall. A window or door onto a loggia is a window or door to the outside.
- **Floor.** The floor of a loggia is an ordinary floor slab, carried like the others
  (`structural-systems`), for the imposed load of category Z (`roofing-waterproofing`
  §8, S.4). Over a heated room it is that room's roof: insulation, waterproofing and
  falls as on a flat roof (`roofing-waterproofing` §8). A slab that runs from inside
  the envelope out into a balcony is a thermal bridge and needs one of the breaks of
  `construction-detailing` §4.7; a loggia inside the outline needs none of them when
  its floor is insulated on top as a roof.
- **Guard.** Every open side gets a guard, a parapet or a railing, where the floor lies
  more than 0.50 m above the ground or the surface below (Bavaria, BayBO Art. 36;
  `stairs-vertical-circulation` S.3). Its height comes from the same section: 0.90 m
  for a fall height up to 12 m, 1.10 m above. The law of the state decides.
- **Depth.** Usable depth at least 1.50 m from the wall to the guard (S.3, a default of
  this library; no book gives a depth).
- **Counting.** Outdoor space is listed apart from the living area: the
  Wohnflächenverordnung counts balconies and loggias at a quarter, at most a half
  (`building-typology`). For GRZ/GFZ the plan text decides (1.4). The window rule of a
  room behind a glazed loggia counts the loggia's floor with the room's (S.1).
- **Distance to the boundary.** A loggia lies inside the outline and is measured with
  the house; a balcony may stay out of the setback depth only within the limits of the
  state law (S.2).

---

## Section 4: Circulation — Flurs, Doors, Windows

Circulation in a well-planned German house should be **8–14 % of gross covered
area**. Over 18 % means the plan is fighting itself — usually a misplaced stair
or a Flur serving two doors.

### 4.1 Passage (Flur) widths

| Situation | Absolute floor (T3) | German practice (T4) | Recommend |
|---|---|---|---|
| Any residential corridor | 900 mm | — | never below |
| Flur serving 1–2 rooms | 900 | 1000 | **1000 mm** |
| Flur serving 3+ rooms / main | 900 | 1100–1250 | **1100–1250 mm** |
| Diele (coat + pass-through) | 900 | 1200–1800 | 1400 with 600-deep wardrobe wall |

**Body geometry behind these widths:** one person facing = 625 mm, two people
passing = 1000 mm, two abreast = 1150 mm (Neufert space-requirement plate,
add >10 % for movement) — see 3.9 for the full anthropometric table this and
3.3's furniture clearances are built on.

**Mechanics:** widths are finished-surface to finished-surface (frame rough
+30–60 mm); keep 1200 mm + 885 clear doors as **barrier-free reserve** (90°
turns need more — `accessibility-universal-design`, DIN 18040-2 binding only if claimed).

### 4.2 Doors (T2/T4 — legacy DIN 4161 leaf vs DIN EN 101 light widths; pick one family, VERIFY)

| Door | Leaf (mm) | Clear | Notes |
|---|---|---|---|
| Eingangstür EFH | 1010–1135 | ~900–1000 | side light widens |
| Room doors | 861–986 (legacy) / 835–985 (DIN EN 101) | ~710–875 | 985/885 class = resale standard |
| Bad / HWR / Abstell | 611/736 | ~585–710 | outward or sliding under 4 m² baths (fall-inside blocked-door logic) |
| Kellertür | 861–985 | ≥800 + landing | |
| Terrasse | element ≥ 2.40 | — | slide/lift 2–3 m = value move |

### 4.3 Window and opening sizes (T4 practice; geometry universal)

| Opening | Typical W×H (m) | Sill (m) | Notes |
|---|---|---|---|
| Schlafzimmer | 1.2–1.6 × 1.25 | 0.80–1.00 | openable sanity + escape (4.5) |
| Wohnen | 2.4–3.6 × 1.75–2.25 | 0.40–0.60 | low sill = garden sightline; fall-guard duty at ≥0.5 sill states vary (VERIFY) |
| Küche | band over counter | **1.00** | 0.90 counter + 0.10 splash |
| Treppe | landing window | 0.90–1.20 | stops the unlit-stair defect |
| Bad | 0.8–1.2 × 0.6–1.0 | 1.60–1.90 | privacy; openable in practice |
| Keller-Lichtschacht | ≥ 0.8 × 1.2 clear | — | doubles as cellar-room egress! |

**Window head:** align with the door-head band (2.00–2.25 finished) → one
lintel line, calmer façade, continuous shading line (7.3).

**Size first:** the rough opening of the windows is at least 1/8 of the net floor
area of the room (MBO § 47, S.1); the openable 1/10 below is the second, weaker test.
**Two arithmetic traps:** 1. **Openable ≥ 1/10 floor-area bites on big rooms**
— 32 m² Wohn, 2.4×1.75 glazed → openable half = 2.1 m² = 6.6 %; add a second
leaf; compute. 2. **Sliders halve openable; Kipp is not full ventilation.**
DG roof-window rooms pass air but pay **summer overheating** (7.3/7.4): the
digest's S-index + F_C table (Raffstore ≈ 0.25–0.35 external) prices the fix —
proof: `building-physics-thermal-moisture`.

### 4.4 Entrance sequence (Diele)

Diele ≥ 5 m² (8–12 comfort). **Visual break** front door ↔ Wohnen (wall turn,
cupboard screen, closed door) — the "man sieht beim Öffnen alles" complaint is
the privacy rule; Gäste-WC off the Diele, never through the family zone; a
350–400-deep shoe niche at the door — universally needed, never built.

### 4.5 Egress logic (T2/T3 — VERIFY state versions, `building-regulations-permits`)

- MBO-lineage: every storey needs first + second Rettungsweg; within dwellings
  the escape class is met by openings **≥ 0.90 × 1.20 m clear** — a normal
  1.2×1.25 casement passes, a 0.6 m bathroom window does NOT and is no escape.
- **Rauchwarnmelder** Wohnräume/Flur/DG (state duty incl. existing — VERIFY).
- Never lock the only stair inside the kitchen/cellar room. DG: passable escape
  window per sleeping room, reachable sill (figures = state/fire, VERIFY).

---

## Section 5: Staircase — Geometry and Placement First

### 5.1 The bands (T2 — MBO §35 family; **state LBOs amend, VERIFY**)

| Parameter | General (MBO-derived, VERIFY) | Within dwelling | Comfort target |
|---|---|---|---|
| Riser S | 140–180 (up to 190 legacy) | ≤ 190 | **160–180** |
| Tread A | 250–300 | ≥ 210–230 floor | **260–300** |
| Comfort rule | 2S + A = 620–640 | | |
| Clear width | ≥ 1000 common stairs | **≥ 500** legal floor (!) | 900–1100 |
| Headroom | ≥ 2000 | ≥ 2000 | ≥ 2100 |
| Risers per flight | ≤ 18 | | land at ≤ 12–15 |
| Landing | ≥ flight width | | ≥ 1.0 m + turn |
| Handrail / balusters | ≥ 900 (fall duty, state-VERIFY); no climbable pattern; sphere ≤ 120 (applied 10 — VERIFY) | | both sides > 1100 |

**Never quote the 500 mm legal floor as a target — the market sells ≥ 850 and
a sofa must pass.**

### 5.2 Worked stair calculation (default EFH stair)

```
F2F 2900 (2700 clear + 200 slab, 3.4)
Risers: 2900/170 = 17.06 → 17 R @ 170.6 ✓ band
Treads: 16; comfort 620 − 2·170.6 = 278.8 → A = 280 ✓
Straight: 16×280 = 4480 → needs a 4.6 m wall run (whole room length on row plots)
Dog-leg ½-Wendung: 9+8 risers; 8×280 + Podest 1100 = 3340 run ×
  (2×900 + 200 well = 2000 wide) ≈ **3.34 × 2.0 m slot** — the "Treppe needs
  2 × 3.5 m" figure is arithmetic, not convention.
```

- Odd split 9+8 fine; **one riser height everywhere** (#1 trip + claim cause).
- F2F 3.05 → 17 R @ 179.4, 16 A @ 261 — taller storeys eat stair length.
- **Headroom, the skipped check:** at the half-landing, clear = F2F/2 − slab −
  finish = 1450 − 250 = 1200, +170.6/tread → 2000 cleared **5 treads back from
  the landing nosing**. A 3-tread under-stair store will hit heads; the under-
  stair Gäste-WC needs ≥ 2 m over the whole fixture+move zone — usually the
  **upper** flight's underside, not the lower.

### 5.3 Type selection

| Type | Slot | Use | Avoid |
|---|---|---|---|
| Straight flight | 1.0 × ~4.6 m | long row segment, side wall | short plots |
| **Dog-leg** | ~2.0 × 3.4 m | **default EFH/DHH** | slot < 2 m |
| Quarter-turn | ~2.1 × 3.5 m | Diele corner | tight plots |
| Open well | +0.3 m | showpiece, light | small houses; acoustics → `building-acoustics` |
| Winders (no landing) | 1.0 m | last resort | children/elderly; MBO width conditions VERIFY |
| Spiral | Ø1.6–2.0 | cellar/bonus stair | primary — furniture cannot pass |

### 5.4 Placement rules

1. **Stack exactly** (misaligned = slab cut + transfer + void).
2. Land in **circulation on both floors**, never in a bedroom.
3. **On the party/gable side** in row/DHH — a central stair splits a 5.5–6 m
   living zone in half.
4. **Light it**: landing window to gable/shacht, or rooflight over an internal
   eye — the unlit stair is serial housing's most common defect.
5. Under-stair space only with 5.2 headroom math.
6. **Separate-let unit (Einlieger/Zweitwohnung):** its stair must be reachable
   **without crossing the main unit** — decide before the first sketch; also
   own Stellplätze + "number of Wohneinheiten" allowed by the plan (VERIFY).

---

## Section 6: Sun Geometry, Courtyards and Light Wells

### 6.1 Solar altitude — the formulas (T5: geometry, exact for noon sun)

Noon sun altitude from latitude φ (declination ±23.44°, used as 23.5 here):

```
summer solstice (21 June):  h_s = 90° − φ + 23.5°
equinox                    :  h_e = 90° − φ
winter solstice (21 Dec):   h_w = 90° − φ − 23.5°
courtyard W/H needed for winter noon sun to reach the floor = 1 / tan(h_w)
horizontal overhang to fully shade a south window of height H at noon:
                            D = H / tan(h)     (shadow drop = D·tan(h))
```

Applied to DACH cities (the geometric consequence of latitude — this table
*replaces* any city-specific handbook table; regenerate for any other site):

| City | φ | h_s (Jun) | h_e | h_w (Dec) | winter W/H for sun to floor |
|---|---|---|---|---|---|
| Berlin | 52.5° | 61.0° | 37.5° | 14.0° | **4.01** |
| Hamburg | 53.6° | 60.1° | 36.4° | 12.9° | 4.36 |
| Frankfurt | 50.1° | 63.4° | 39.9° | 16.4° | 3.40 |
| München | 48.1° | 65.4° | 41.9° | 18.4° | 3.01 |
| (Wien ~48.2°, Zürich ~47.4° — same math) | | | | | |

**The honest DACH conclusion (inverts the hot-climate courtyard logic):** at
~14° winter noon sun (Berlin) a court needs W/H ≈ 4 for sun on its floor — a
2-storey court (H ≈ 6.4 m) needs ≈ 26 m width; sun onto the north wall at 2 m
floor height still needs ~17.6 m; single-storey (H 3.3) ~13.2 m — **garden
scale, not courtyard.** So the garden + south facade do the winter-gain work;
an Atrium/Hof is chosen for daylight, privacy and outdoor value, accepted as
winter-shadowed (heating penalty = `building-physics-thermal-moisture`); summer
shading is mostly a morning/evening/oblique-sun task since 60–65° noon sun
already clears most horizontal devices.

### 6.2 Sizing bands (retagged for the heating-dominated climate)

| Type | Plan size | W/H at 2 storeys | Function |
|---|---|---|---|
| **Lichtschacht** (light well) | 1.2×1.2 up to 2.0×2.5 | < 0.35 | bath/stair/cellar ventilation + code light only — **call it that, not a courtyard** |
| Lichtof / narrow air shaft between row gardens | 1.5–3 m wide slot | 0.3–0.6 | daylight to a side room, borrowed air; privacy-glass |
| Small court (Sitzhof, Vorgartenhof) | 3×4 – 4×5 | 0.6–0.9 | usable outdoor room off the Diele; wind shelter; **the DACH value move on a 5.5–7 m row segment** |
| Atrium / Innenhof of MFH | 8×10 up | 1.2+ | daylight to inner units; **diaphragm-cut flag (2.6)**; winter sun irrelevant, summer self-shade pleasant |

**Aspect:** 1:1–1:2 (long axis E–W for midday sun on the north face); <0.3 =
shaft; >1.2 = yard, not court.

### 6.3 Making the court actually work in DACH

1. **Drain and frost-proof it:** slope ≥ 1:50 to a frost-protected drain
   (Entsorgungssatzung/Rückstau considerations — route `building-services-tga`);
   never toward the house; a court below the backflow level (Rückstauebene)
   needs a Hebeanlage — hard legal+physical check, **VERIFY with the
   Entwässerungsgenehmigung**.
2. **Glazing it** (Wintergarten/Loggia) makes a heat buffer but changes
   GRZ/GFZ/Abstandsflächen counting — plan text, VERIFY.
3. **Openable connection to every surrounding room** — night purge of the mass
   (Nachtabkühlung, 7.5/DIN 4108-2) is the summer half of the mechanism.
4. **Plant/water at least partially** — an all-paved court is a GRZ-counted
   heat radiator (1.3) with nothing to show.
5. **Overlooking:** stagger sightlines / partial screens (neighbour privacy
   claims under Nachbarrecht are real design constraints — VERIFY).

### 6.4 Light wells and windowless rooms

- Internal bathrooms need mechanical Lüftung (WRG/extract): "Fensterpflicht"
  is habit, not law — windowless Wohnräume are LBO-possible with proper
  ventilation/light, but market + lenders punish them (T4, VERIFY financing).
- Shaft depth: below ~1:6 W:H delivers daylight, treat as light + vent; design
  the artificial light regardless.
- **Never cap a shaft that serves as a second escape route or a cellar room's
  only opening** — the opening must stay passable (≥ 0.9×1.2 clear class).

### 6.5 Court vs light well vs none — decision tree (DACH)

```
Is there ≥ 3.5 m of spare plan width after the room budget (3.8)?
  └─ NO  → Lichtschacht or none. Mechanical bath ventilation. Stop.
  └─ YES ↓
Is the plan deep (>14 m) without a garden aspect on two floors?
  └─ NO  → none; daylight the Flur from the Diele/OG slot instead.
  └─ YES ↓
Row/DHH segment with 5.5–7 m width?
  └─ YES → SITZHOF 3×4 off the Diele or between house and garage (the classic
           Reihenhaus "Vorhof/Innenhof" move) — privacy + daylight + the value
           of an outdoor room; winter sun not promised.
  └─ NO (MFH / deep free-standing) → ATRIUM/HOF, centred (2.6 diaphragm flag),
           edge beams all four sides, ≥ 1:1.2 plan, E–W long axis;
           inner units' windows onto it: acoustic reflection check
           (`building-acoustics`) + overlooking check 6.3(5).
```

---

## Section 7: Orientation, Sun, Wind and Noise (DACH)

### 7.1 The headline

DACH is **heating-dominated**: the free moves are **capturing low winter sun
on the south facade**, **excluding summer sun**, and **night purging** (DIN
4108-2 sommerlicher Wärmeschutz, climate regions A/B/C + S-index — both in the
digest; a room failing S ≤ S_zul is a legal Nachweis problem later, so fix
orientation early — formal proof: `building-physics-thermal-moisture`).

**Core rules:**
- **Long glazed facade south** (±~45° acceptable before gain drops off — SE/SW
  still good; multiple E/S/W-glazed rooms worsen the S-index, digest design
  heuristic).
- **East/West: real but manageable** (low-angle sun; vertical shading works;
  the hot-country "zero west glazing" rule does NOT apply — in DACH a west
  terrace is a valuable summer-evening asset *if* shaded).
- **North: daylight without gain** — put unheated/buffer rooms there
  (Garage, HWR, Abstell, Treppe), exactly the old buffer logic, rotated 180°.
- **Roof = biggest gain surface** (digest roof-window S-terms/tilt factors);
  PV south 30–36° (yield band — verify with a calculator); roof zoning 9.6.

### 7.2 Room-by-room orientation (retargeted table)

| Room | Best | Why |
|---|---|---|
| Wohnen | **S / SW** | winter gain + garden; deep overhang/balcony for summer |
| Essen/Wohnküche | S–SE | morning-to-day light |
| Schlafzimmer | **O / NO / SO** | morning warm, afternoon cool (sleeping = coolest room preference) |
| Kinder | SE/O | light; avoid W (late heat → bed-time) |
| Arbeitszimmer | N–NW acceptable | diffuse light, less glare; W needs shading |
| Bad | any daylight, often N | |
| HWR/Küche-technik, Kellerabgang, Garage | **N / W strip** | buffer principle |
| Diele | N entrance typical | vestibule double-door mitigates winter drafts |
| Terrasse | S/SW | the value facade |
| Sitzhof/Atrium | centre | 6.x |

### 7.3 Winter vs summer contrast — the worked shading numbers (T5 geometry)

South window, height H = 2.1 m (living, near-flat roof shading line):

```
München:  h_s = 65.4° → D = 2.1 / tan(65.4°) = 0.96 m
          shadow drop at winter h_w = 18.4°: 0.96 × 0.333 = 0.32 m
          → 1.78 of the 2.1 m in full winter sun ✓ — one 0.95–1.00 m balcony
          slab/roof projection is a complete seasonal solution.
Berlin:   h_s = 61.0° → D = 2.1 / 1.804 = 1.16 m; winter drop 0.29 m → 1.81 m
          of sun ✓. Same logic, deeper projection (≈ roof-overhang or first
          balcony plate).
```

**Same window, west, July ~18:00 (altitude ≈ 25–30°):** D = 2.1/tan 27° ≈ 4 m
— **no sane horizontal overhang shades a west window.** Working devices:
vertical fins, Raffstore, loggia recess, planting — or move the window. The
digest's F_C table prices them for the S-index proof (external Raffstore 45°
0.25–0.30; canopies 0.50–0.55; roller ¾-closed 0.30–0.35) — formal Nachweis:
`building-physics-thermal-moisture`.

### 7.4 Facade glazing strategy (WWR — retagged; DACH is a *balance*, not a
minimisation)

| Facade | Practical band | Logic |
|---|---|---|
| S | 25–40 % of that wall, shaded | winter gain is wanted; unshaded S glazing becomes a summer liability (S-index +0.10 term for N-share, F_C table) |
| O/W | 10–20 %, device-shaded | low-angle; fins/Raffstore/loggia |
| N | 10–20 % | daylight only; keep on buffer rooms |
| DG roof windows | ≤ ~15 % of floor, g_tot low | overheating risk class; openable + shading mandatory in practice |

(These are design bands, T4/T5-flavoured; the *legal* check is DIN 4108-2 S ≤
S_zul per room, with the digest's S_1…S_6 terms — `building-physics-thermal-moisture`.)

### 7.5 Wind, climate-adaptive notes (replaces the hot-country wind-rose tables)

**Wind exposure is local** (coastal Hamburg vs Alpine foreland vs Oberrheingraben,
neighbour shelter, terrain, B-Plan plantings) — apply generically:

- Summer comfort = **Nachtabkühlung**: night purge through the mass (the digest
  S_1 table prices night-vent classes n≥2 / n≥5 h⁻¹); openable low windward,
  high leeward/stack via Treppe/Atrium; doors undercut 10–15 mm.
- Winter comfort = vestibule/Windschutz or double door on exposed entries; n50
  is a construction job (digest n50 ≤ 3 / 1.5 — `building-physics-thermal-moisture`).
- **Coastal/exposed sites:** driving-rain exposure group III in the digest
  (rainy/windy/coastal) triggers the façade-detail review — not a plan change.

### 7.6 Noise and privacy adjacencies (T2 — TA Lärm/DIN values, cross-ref
`building-acoustics`)

- **Street/mixed side:** Diele, Treppe, HWR, Abstell, Garage as the acoustic
  buffer before sleeping/living rooms (buffer principle again).
- **Quiet-side sleeping** — digest TA-Lärm guide values: general residential
  55/40 dB(A) day/night, pure residential 50/35; **indoor protected rooms
  ~35 day / 25 night**. A bedroom window to a street above night values cannot
  meet 25 dB(A) open → plan sleep-ventilation via the other facade or a
  Lüftungskonzept (DIN 1946-2, VERIFY); the Rw stack is `building-acoustics`.
- Decide here: bedroom walls off the Diele/Treppenhaus side; bath pipes not
  behind a shared headboard wall; **Wärmepumpe-Außengerät position vs
  neighbours' bedroom windows (immission distance — a plan-position decision)**;
  Mischgebiet (1.2) trade noise — some newer B-Pläne carry "Lärmschutz /
  Raumanordnung" clauses: VERIFY plan text.
- Overlooking: 6.3(5) + the 3 m-side habit → opposing windows ~6 m apart
  (eye-contact distance); hedges/screens where the plan allows.

---

## Section 8: House Typologies for German Plots

The archetype fixes structure, servicing, daylight and resale; the tree starts
at **Bauweise** (plan law), then frontage, then brief. Depth → `building-
typology`; here: plan consequences only.

### 8.1 Reihenmittelhaus / row segment (WR or closed WA)

Frontage 5.5–7 m, party walls both sides, garden axis fixed by plan; depth
11–14 m: 2-room band + 1.2 m stair/circulation strip; floor span = plot width
5.5–6.5 m (9.4, cross-wall logic); stair on one party side, full-width living
to the garden; middle dark → Lichtschacht/Sitzhof (6.5); circ 12–16 %. The
standard B-Plan product — you win on the section (DG? height clause!), not plan.

### 8.2 Doppelhaushälfte (DHH, offene Bauweise, one party wall)

Plot 250–400 m² (band), frontage 8–11 m, one open garden side. **Mirror with
the neighbour early:** stair + wet zones on the party line, living to the open
side; party wall = continuous cross wall (cheap). Best area-efficiency; detail
the open-side reveals for the day the neighbour builds out (7.6).

### 8.3 Freistehendes EFH (offene Bauweise, both sides free)

Plot 450–700 m², frontage ≥ 12–16 m; 2–3-bay plans; *usable* garden is the S
side — don't spend GRZ paving all round (1.3). Test 1.5-storey / 2 / 2+DG
against GFZ AND the Vollgeschoss/Wandhöhe clause (a flat-roof DG often reads
as 3 storeys on terrain where a Satteldach hides the same area legally —
plan-text game, 1.4/1.5). This is the generic 600 m² case of Sections 2/12.

### 8.4 Zweifamilienhaus / two stacked units

Second entry must not cross the main unit (5.4(6)); two mirrored wet stacks,
meters/tech per unit; the party floor is now a **DIN 4109 legal-minimum case**
(unrelated dwellings — VERIFY state adoption) → `building-acoustics`; plan
consequence: no stair beneath the other unit's Wohnen, buildup 300–400 class.
Workhorse at GFZ ≥ 0.7–0.8 placeholders.

### 8.5 Kleines Mehrfamilienhaus (3–6 units)

Frontage ≥ 12–14 m or depth ≥ 25 m; units back-to-back on a Flur/Treppenhaus
spine; reserve Aufzug ≥ 1.10×1.40 + machine space now (shaft = GRZ area —
VERIFY vendor dims); every unit 2 aspects; Stellplätze under/on building
(Tiefgarage shifts the Keller/GFZ reading — plan text). Depth on unit mix →
`building-typology`.

### 8.6 Bungalow / slope variants

Bungalow: full GRZ at GFZ ≤ GRZ — check the clause isn't *forcing* 2 storeys
("min. 2 Vollgeschosse" exists in some WR plans — VERIFY) and roof/PV duties.
Slope (Hanggrundstück): terraced full floors beat split levels (2.6 + cost —
`geotechnics-foundations`); the walk-in downhill Keller is the German classic.

### 8.7 Infill / Baulücke (§34 read 1.7)

Match Bauweise, eaves line, roof form, window rhythm (1.7). Frontage fixed;
narrow-front plans go *sectional*: stair one side, rooms single-loaded to the
garden, Lichthof past 14 m depth (6.5).

### 8.8 Archetype selection tree

```
B-Plan Bauweise?
 ├─ geschlossen / WR ────────────→ 8.1 row segment (+Sitzhof 6.5). Stop.
 ├─ offen, "Einzel- u. Doppelhäuser" →
 │     Frontage ≤ 11 m & client wants max area/unit ─→ 8.2 DHH (mirror stacks)
 │     Frontage ≥ 12 m & one household ─────────────→ 8.3 freistehendes EFH
 │     Two households / rental unit ────────────────→ 8.4 2-FH
 │     ≥ 3 units wanted / GFZ ≥ 1.0 ───────────────→ 8.5 small MFH
 ├─ kein B-Plan (§34) ──→ 1.7 measure the surroundings, then match to their
 │                         Bauweise → re-enter the branch above.
 └─ slope > ~5°? ───────→ 8.6 terraced variant of the chosen type (2.6 note).
Height clause (1.4) or GFZ (1.4) blocks the DG? → drop to 8.6 bungalow / 1.5-
storey before shrinking every room (3.8 rule).
```

---

## Section 9: Stacking, Services and the Structural Grid

The house-scale core. A single house has no "core", but it has wet zones, a
stair, installation ducts and column/wall lines — and they must line up.

### 9.1 The stacking rules

1. **Wet-on-wet.** Every upper bath sits over a bath, kitchen, HWR or Flur —
   never over a bedroom or Wohnen. (Universal; the leak-damage claim is the
   same in every market.)
2. **Kitchens stacked** where two units exist; otherwise kitchen over
   kitchen/HWR/garage.
3. **Stair stacks exactly** (5.4).
4. **Wände tragen durch** — a load-bearing wall stops at no floor without a
   transfer beam (2–3× cost; house-scale, almost never worth it). Frame
   columns (if Skelettbau) run to foundation.
5. **Abwasser vertical:** Installations-/Leitungsschacht stacked over the wet
   zones; DN 100 per bath group; offsets with putztürmchen/revision. Gradients:
   DIN-1986-family practice ~**1 cm/m for small lines, ≥ 0.5 cm/m for DN ≥ 100,
   self-cleansing band ~1:50–1:100 — T2, VERIFY current edition** (digest
   sources carry none of it).
6. **Horizontal drain distance** from furthest bath to stack ≤ ~4–6 m or the
   floor buildup fights the heating/terrace level — the old "deep buildup"
   logic is metric and universal.
7. **Haustechnik stack:** HT + Warmwasser on one wall (Keller/HWR); PV
   counter/storage by the HWR; riser by the stair; gas only where a mains
   line exists (most new builds: none — `building-services-tga`).
 8. **Fresh-air/WRG concept decides ducts early** (KWL: duct runs in the
    Deckenaufbau or along the Flur ceiling → ceiling-height loss; DIN 1946-2
    VERIFY): reserve duct routes before the first room wall.
9. **Rainwater retention** (cistern) often mandatory per municipality
   (Entwässerungssatzung — VERIFY): reserve its Keller corner/garden strip now.

### 9.2 Typical 2-storey EFH stack (retargeted from G+1)

```
DG (if clause allows)   2–3 Kinder-/Arbeitszimmer + Bad; Kniestock logic (1.5)
OG                      Eltern SZ + Ankleide + Bad | 1–2 further SZ + Bad | Flur
EG                      Diele + GWC | Wohn-Ess-Koch open to garden | HWR |
                        (one guest/Arbeitszimmer SZ + Bad on EG — ageing-in-place:
                        most-requested, most-often-omitted item)
Keller                  HT + WRG + tanks + Hausanschluss | workshop | storage
                        (GFZ-exempt per plan wording — VERIFY 2.4)
Site                    Stellplätze, Zufahrt — ALL GRZ-counted (1.3)
```

### 9.3 Wall/buildup thicknesses (German, metric)

| Element | Buildup | Note |
|---|---|---|
| External masonry | **30–36.5 cm** KS/brick + WDVS, or monolithic 36.5–42.5 | timber external wall 30–34 assembly |
| Load-bearing internal | 11.5–17.5 cm | |
| Non-load partition (Trockenbau) | 75–100 mm + boards ≈ 100–125 | sound class → `building-acoustics` |
| Wet wall with DN 100 stack | ≥ 200 mm chase or Vorwand-Ständer + Verkleidung | 11.5 solid cannot take pipe + isolation |
| Decke RC | 180–250 + Estrich 50–65 | F2F 2.90–3.05 (3.4) |
| Timber deck / wood beam | 300–380 with diffusion layer | acoustics + vibration — route |
| Putz/finish | 15–20 each face — **deduct from clear dims** | the plaster trap, metric |

**FreeCAD default set (metric):** exterior 365, interior 115, partition 100,
slab 250, F2F 2900, door leaf 985/736/611 (885/611 light — pick a catalogue and
stick to it), sill 900/1000, head 2095/2250, roof pitch per plan clause.

### 9.4 Structural-grid coordination (digest-supported — conception; verify
final with `structural-systems`)

The plan and the structure are decided together; rooms sized first and "the
engineer will catch it" is how a Stütze ends up mid-bedroom.

| Decision | Preliminary rule | Plan consequence |
|---|---|---|
| **cross-wall masonry (Querverband)** | floor spans = unit width, **RC solid slab 5–7 m; timber ~4.5 m economic** (conception) | room widths ARE the grid; party + 2–3 cross walls line up through all floors |
| **longitudinal band / Ständer** | façade columns 2.5–3.5× room bands | every column inside a wall line; open side = the free façade |
| **one-way slab depth** | **span/30, economical to ~8 m (~300 mm)** (conception) | 6.5 m row span → ~220 mm class + buildup; > 7 m: two-way or beams (2-way action only ≈square, aspect ~1:1.5 → one-way behaviour — conception) |
| **ring beam / Scheibe** | edge ring ≤ ~30× slab thickness; > 2 Vollgeschosse / length > 18 m / big openings trigger anchorage (conception — verify per Eurocode 6 national annex) | continuous Flur-deck edge & gable tie; wall openings align |
| **lintels over windows** | flat brick lintel self-carries the triangle load zone; 24 cm wall spans ≤ ~2.0 m, 36.5 cm ≤ ~2.0–5.5 m without RC lintel (conception) | window band width is a structural decision at ~5 m+ openings |
| **non-load partitions** | built top-down, floor-deflection slot ≥ 10 mm, DIN 4103 line load 0.5 kN/m at 0.9 m (conception) | bathroom walls on floating detail; never carry deck onto a partition |
| **timber frame** | stud grid 0.625 m (62.5/125 cm); panel formats to joints (conception 187–188) | window reveals & Electo-routes land on stud rhythm — set room widths in multiples of 62.5 |
| **DG trusses** | Kniestock height vs span; liveable band = ridge ≥ ~2.0–2.2 m — structural choice, route | the "hidden 3rd floor" (1.5) is won or lost on the truss |

**Rules:** grid before furniture; grid lines = the continuous party/Flur/stair
walls; rooms > 7 m wide are a structural decision (deck depth/two-way/beam);
a court = diaphragm hole (2.6) — edge beam all four sides on grid; this table
is preliminary — final members from `structural-systems` + the Tragwerksplaner.

### 9.5 Cross-reference — where this skill must NOT stand alone

This skill (a) flags plan-configuration risk originating here (2.6) and (b)
tags every regulatory number VERIFY. It does **not** perform structural design,
the Wärmeschutznachweis (→ `building-physics-thermal-moisture`), Schallschutz
nachweise (→ `building-acoustics`), accessibility design (→ `accessibility-
design`), or the authoritative legal read (→ `building-regulations-permits`:
B-Plan text, state LBO/MBO §§, Stellplatz-/Abstandsflächen ordinance, GEG).
**Treat every GRZ/GFZ/Abstands number in this file as a placeholder to be
replaced by the parcel's own documents — never as a citation.**

### 9.6 Roof-level coordination: PV, flue, units, and the "Dach" clause

The roof hosts PV (S band 30–36°), flue line (must clear the PV field — route
fire/services), HT/fresh-air terminals, service access — and some B-Pläne set
PV zones on the roof drawing itself (VERIFY plan graphics!). **Zone the roof in
the model** (PV / terminals / access / flue shadow) — Section 14 checklist slot.

---

## Section 10: Efficiency — NTG and Circulation

### 10.1 Definitions (metric)

- **Gross (GRZ/GFZ language):** areas to outer wall faces per the state's
  calculation directive (VERIFY). **NRF** = room areas inside finishes;
  **WFL** = Wohnflächenverordnung bands (balcony 25/50 %, DG slope bands —
  VERIFY when sold/leased as WFL). **NTG = NRF ÷ gross.**

### 10.2 Targets

| Type | Poor | Typical | Good |
|---|---|---|---|
| EFH/DHH 1.5–2 storeys | < 70 % | 72–78 % | 78–82 % |
| 2–3-unit house with common stair | < 70 % | 72–78 % | 78–80 % |
| small MFH (8.5) | < 68 % | 70–76 % | 76–80 % (Aufzug reserve eats it — plan the shaft once, 8.5) |

Walls 8–12 %, circulation 8–14 % (§4), stair 5–8 % of gross. **Efficiency is
not the goal** — Sitzhof and Diele score badly and buy real value; NTG catches
*waste* (Flur with two doors, duplicated lobby, unstacked bath — 10.3).

### 10.3 German-specific leak list (trimmed)

Passage serving < 3 doors · stair mid-plan on a 6 m row · unstacked baths ·
two separate entrances where a combined Diele serves (two-unit!) · 11.5 walls
where 10 Trockenbau carries nothing · a dead re-entrant corner from a bad stair
· carport + full-length drive eaten by GRZ where an integrated garage would
have hit GFZ for free · **Wohnen under the unlit DG slope where a Kniestock
would give full height** (then the room is 60 % WFL per WoFlV bands — VERIFY).

---

## Section 11: Legibility (Lynch, kept short)

- **Path:** one clear Diele→Treppenhaus→Garten sequence; a guest never faces
  three identical doors. **Edge:** the Diele threshold = public/private line.
- **District:** guests front (Diele+GWC+Arbeitszimmer), family centre
  (Wohn-Ess-Koch), sleeping quiet rear/OG, service band (HWR/Keller/Technik).
- **Node:** Diele + stair landing — lit, visible from entry. **Landmark:** the
  Treppenauge, a Sitzhof view, the open kitchen — one event orients the plan.
- Front-door sightline must not reach a bedroom door; light passage ends;
  height hierarchy Diele 2.70 > Flur 2.60 > lowered Bad/HWR — compression
  before the Wohnen makes arrival.

---

## Section 12: Verification Checklist + Worked Example

### 12.1 Compute, don't eyeball — the model check list

- [ ] Plot area/frontage/depth from the Kataster extract / Amtlicher Lageplan,
      not satellite estimates
- [ ] B-Plan figures transcribed with §-numbers (or §34 survey 1.7 attached);
      **any number still a placeholder = study marked non-submittable**
- [ ] GRZ: house + carport/garage + drive + paths + terraces **tallied from the
      model**, ≤ A × GRZ (incl. any Minderanrechnung the plan grants — VERIFY)
- [ ] GFZ: sum of storey gross areas ≤ A × GFZ; DG/Loggia/Keller counting per
      plan text applied, not per habit
- [ ] Height: storey count + Wandhöhe vs clause (1.4/1.5 measure line!)
- [ ] Baufenster + Abstandsflächen: minimum boundary distances model-measured
      (all 4 sides), incl. eaves/roof overshoot (many states count the roof
      projection into H — VERIFY)
- [ ] Stair: riser/tread/2S+A computed from the real F2F; headroom ≥ 2000
      checked under the flight; landings ≥ width
- [ ] Every bath over a bath/kitchen/HWR; stacks model-traced
- [ ] Bedrooms ≥ 10 m² (never below T3 7.5 m²); rough window opening ≥ 1/8 floor (S.1), openable window ≥ 1/10 floor,
      **openable counted**; escape geometry per sleeping room (4.5)
- [ ] Circulation % and NTG computed from areas, not vibes (10.2)
- [ ] Court/Lichthof W/H stated (6.2 band) and *not sold as* winter-sun tech
- [ ] S-index sanity: S-glassed rooms have a shading concept; DG rooms list F_C
      device (7.3/7.4); formal proof = `building-physics-thermal-moisture`
- [ ] Noise: sleeping rooms face the quiet side or have a Lüftungskonzept plan
      (7.6); Wärmepumpe position checked vs neighbour bedroom distance
- [ ] Plan regularity flags (2.6): L/court/wing/split annotated in handoff
- [ ] Section 13 red-flag list run end to end

### 12.2 The generic 600 m² site — EFH, 4-person family (all plan figures
**T1-V placeholders**)

```
SITE     25.0 × 24.0 m = 600 m², street NW, garden SE. φ = 50° (generic central
         DACH city → h_s 63.5, h_e 40.0, h_w 16.5 — recompute per 6.1).
PLAN     WA, offen. GRZ 0.4 · GFZ 0.8 · "2 VGS, Wandhöhe bis 7.10 m, DG
         zulässig (counts GFZ? → plan text: counts at 100 %? ASSUMED NOT fully —
         PLACEHOLDER both readings, VERIFY)". Baufenster: 8 m street setback,
         full side span; rear ≥ 3 m. Stp: 2.
ENVELOPE GRZ: 240 − (drive 30 + paths/carport-class 28 = 58) → house 182 m².
         GFZ: 480. 2 floors × 182 = 364 gross; DG up to 480−364 = 116 gross
         (≈ 80–90 NRF) fits the assumed reading. Height: 2×2.90 + DG within
         7.10 wall + roof clause ✓ (measure-line check!).
SETBACKS A = max(3.0, 0.4×~6.5 = 2.6) → 3.0 m sides ✓ (long side 18.2 runs
         parallel to the 25 m frontage ≤ 25−6 ✓; depth 10.0 inside the 8 m
         Baufenster line + ≥3 m rear ✓; long facade faces the SE garden).
BUDGET   usable EG ~150 + OG ~150 + DG ~85 → ≈ 385 NRF vs 163 m² room need
         (3.8): FIT — binding constraint named for the client: GRZ/height, GFZ
         has slack.
ARCHETYPE 8.3 freistehend; L-shape rejected (2.6 re-entrant + GRZ paving):
         one 18.2 × 10.0 m block, long axis E–W parallel to the 25 m frontage,
         garden side S. Plan depth 10 m → no Lichthof needed; Flur daylighted
         from Diele + Treppe window (6.5: none).
ORIENT   Wohn-Ess-Koch at SE facade, 2.1 m windows; summer h_s 63.5 → canopy
         D = 2.1/2.01 = 1.05 m; winter drop 1.05·tan16.5 = 0.31 → 1.79 m lit ✓
         (6.1 math). N strip: Diele, GWC, HWR, Treppe, Technik (buffer stack).
STAIR    17 R @ 170.6, A 280, dog-leg 3.34×2.0 well (5.2); window on landing;
         stacked EG→OG→DG exactly.
STACK    baths over baths on the stair wall; kitchen over HWR; WPL-Außengerät
         N gable, off the neighbour-bedroom side (7.6); PV S band, flue N
         corner (9.6).
ROOMS    EG: Diele 12 · Wohn 32 + Ess 14 + Koch 13 (offen, together 55 clear)
         · AR/Gäste 13 · HWR 8 · GWC 3 · Treppe 12 → gross 182 ✓
         OG: Eltern 17+Ankl 6+Bad 8 · Kind 13×2 · Bad 6 · Flur 10 → gross 182
         DG: Studio 30 NRF (Kniestock 1.2 — WFL bands per WoFlV — VERIFY) +
         Abstell 8.
CHECKS   GRZ: 182+58 = 240/600 = 0.400 ✓ (= placeholder exactly — re-run on the
         real plan!) · GFZ: 364+~116 = ≤ 480 ✓ · NTG ≈ 0.77 ✓ · circ ~11 % ✓ ·
         4.3 openable sanity per room ✓ · 2.6: rectangular, no irregularity
         flag needed · escape windows each SZ ✓ · wet-on-wet ✓.
CAVEAT   GRZ/GFZ/VGS/Wandhöhe/Baufenster/DG-counting/measure-line/GRZ-anrechnung
         = T1-V placeholders — VERIFY against the parcel's own documents; study
         for a Bauvorlagen professional, never one (Reality Check).
```

---

## Section 13: Red-Flag Checklist (each = a recurring real defect)

| # | Failure | Fix |
|---|---|---|
| 1 | GRZ tallied with house only | count drive + paths + terraces + carport (1.3) |
| 2 | GFZ "basement is free" assumed | plan-text law; walk-out faces count (1.4/2.4) |
| 3 | DG banked without height-clause read | Vollgeschoss definition + measure line (1.4/1.5) |
| 4 | Bauweise ignored, detached drawn in WR | tree starts at plan law (8.8) |
| 5 | Built outside the Baufenster "just 40 cm" | window is window; minor-annex list only (1.6/1) |
| 6 | Abstandsflächen assumed 3 m everywhere | 0.4·H governs above ~7.5 m walls; state variants (1.6/3) |
| 7 | Boundary garage/wall drawn without Grenzerleichterung | state cap + neighbour declaration (1.6/3) |
| 8 | §34 drawn from vibes | measured surroundings dossier (1.7) + Bauvorbescheid |
| 9 | Brief never tested (3.8) | the two-minute arithmetic |
| 10 | Every room quietly shrunk to fit | drop a room; state it |
| 11 | No EG room for ageing / guests | 9.2 kept rule — the most-omitted item |
| 12 | Bad over Wohnen | restack wet-on-wet (9.1) |
| 13 | Stair not stacked; different risers between runs | 5.2/5.4 |
| 14 | Unlit stair | landing window/rooflight (5.4) |
| 15 | Under-stair WC with < 2 m head over the whole move zone | 5.2 headroom math |
| 16 | Flur 850 mm "because code says so" | market sells 1000–1250; 4.1 |
| 17 | Window sized by eye | compute rough opening ≥ 1/8 floor (S.1) and openable ≥ 1/10 floor; sliders halve (4.3) |
| 18 | Winter sun promised to an Atrium floor at φ>48° | 6.1/6.2 math says no; reframe as daylight+privacy |
| 19 | Lichtschacht sold as Innenhof | 6.5 naming honesty |
| 20 | Atrium off-centre, edge beams "later" | 2.6/9.4: centre + continuous edge, flag engineer |
| 21 | Court drains toward the house / no Rückstau check | 6.3(1) |
| 22 | Sleeping rooms to the street, "windows stay closed in summer" | 7.6 buffer or Lüftungskonzept |
| 23 | Wärmepumpe on the neighbour's property line | 7.6 immission distance |
| 24 | PV laid before the flue/roof-clause check | 9.6 zoning + plan PV clauses |
| 25 | Column stranded mid-room / 8 m span with 200 slab | 9.4 |
| 26 | Zweitwohnung stair crossing the main unit | 5.4(6)/8.4 |
| 27 | Circulation > 18 % | misplaced stair first (10.3) |
| 28 | A VERIFY placeholder quoted to client/authority as fact | say "B-Plan-dependent, VERIFY" in the same sentence (Section 0) |
| 29 | Output presented submission-ready / L/court/split handed off without the 2.6 note | Reality-Check sentence + per-decision 2.6 annotation, unprompted |

---

## Section 14: FreeCAD / BIM Handoff

(Objects and code patterns: the FreeCAD/BIM skill of this library; what follows
is the *planning* content to model and the hierarchy gotchas that bite.)

**Confirmed inputs** — 12.1's first boxes; then: plot as **IfcSite** from the
Kataster outline in a local cartesian project system (origin near the object;
UTM/ETRS89 ties via IfcMapConversion — digested geodesy practice; legal
distances must hold in the *real* system), building under site, storeys above.

**Storeys — the makeFloor gotcha (kept from the predecessor skill):**
`Arch.makeFloor()` — `Elevation` is **derived from `Placement.Base.z`**, not the
reverse: setting `floor.Elevation` alone silently reverts on recompute. Set
`p = floor.Placement; p.Base.z = 2900; floor.Placement = p` (mm → model units),
then read back. Hierarchy: `Site > Building > Storey(KG? EG, OG, DG) > Walls/Slabs/Stairs/
Windows`; rooms as **Spaces** with `freeArea`/`grossArea` so GRZ/GFZ/NTG/circ%
are *scheduled from the model* (12.1 = compute from data, never eyeball);
storey gross sums give the GFZ reading, Elevation/height values drive the
Wandhöhe check.

**Dimensional defaults to set (from 9.3):** exterior 365 · interior loadbearing
150 · partition 100 · slab 250(+50 Estrich shown in buildup) · F2F 2900 ·
door leaves 985/736/611 · heads 2095/2250 · sills 900/1000 · stair riser
170.6 / tread 280 · roof pitch per plan clause.

**Verify in the model before presenting:** everything in 12.1 is
model-computable (area-plot the sealed surfaces for GRZ; boundary-offset the
envelope for setbacks; schedule rooms for 3.1/3.2 floors) — plus:
[ ] stair footprint identical per floor + DG eye [ ] roof zones (9.6) not
overlapping flue/ladder [ ] the two VERIFY-marked readings of 12.2 (DG counts
GFZ yes/no) both modelled so the client sees the consequence.

**Then say it, per decision:** *"Planning model — not genehmigungsfähig;
envelope figures are placeholders (list them); approval needs the parcel's
Festsetzungen + Bauvorlagen signed by a Bauvorlageberechtigten (state LBO);
Atrium/L/split items (2.6) need explicit Tragwerksplaner review."*

---

## Appendix A — Standards map (verify current editions; names not numbers where the digests are silent)

| Source | Scope here | Tier |
|---|---|---|
| **BauGB** §§ 1, 12, 12a, 13a, 30, 34, 35 | Bauleitplanung; Zulässigkeit (FNP→B-Plan→§34/35) — *framework; procedure NOT in the digested sources, VERIFY* | T1 law |
| **BauNVO** §16 Bauweise, §17 GRZ, §19 GFZ/OWZ, area types WA/WR/M/S | the measure-of-use machinery — **every numeric range in this file is a remembered placeholder, VERIFY per B-Plan** | T1 instrument |
| **MBO §6 Abstandsflächen / state LBOs** (e.g. §6 family; 3 m/0.4H) | setbacks | T2, state-amended, VERIFY |
| **MBO Rettungswege/Treppen/Rauchmelder §§** | egress/stair/fire minima | T2, state versions, VERIFY |
| **Stellplatz-/Abstandsflächensatzungen, Entwässerungssatzung, Hochwasserschutzkarten** | site duties, retention, hazards | T1 municipal, VERIFY |
| **GEG + DIN 4108-2/-6, DIN V 18599** | energy + sommerlicher Wärmeschutz (S-index, F_C — *in the digested physics source: kept bands quoted there*) | T2 |
| **DIN 4109 / VDI 4100; TA Lärm** | Schallschutz; immission guide values (digest has the TA-Lärm table + DIN 4109-1 minimums) | T2 |
| **DIN 18040-2; DIN 1946-2; DIN 1986-100** | barrier-free (claimed-only); Lüftungskonzept / drainage gradients | T2, VERIFY editions |
| **DIN EN 1998-1/NA** | seismic zones (mostly 0; Oberrheingraben/Alpine fringe) | T2, VERIFY |
| **conception digest (structural rules)** | spans 5–7 m, one-way/30, 62.5 cm stud grid, ring-beam anchors, lintel spans | T2-rules-of-thumb, VERIFY |
| **Neufert Architects' Data / market norms** | furniture clearances, room-size bands (3.2–3.3); body-dimension/movement-envelope tables, English ed. Neufert_2002.pdf pp.16–17 (3.9) | T4 |
| WoFlV; generic international habitable minimums (7.5/9.5 m²) | WFL bands; sanity floor ONLY | T1 / T3 |

## Appendix B — Rules of thumb (metric)

| Parameter | Value |
|---|---|
| GRZ / GFZ / VGS / Wandhöhe / Baufenster | **B-Plan of THIS parcel — the ranges here are placeholders, VERIFY** |
| Abstandsfläche family | max(3.0 m, 0.4·H) — state law, VERIFY |
| GFZ↔floors quick check | floors ≈ GFZ ÷ GRZ_eff (2.2) |
| NTG target EFH | 72–80 % |
| Circulation | 8–14 %; > 18 % = misplaced stair |
| Flur / Diele | ≥ 1000 / entry 1400 · door clear ~860 (885/985 leaves) |
| Bedroom market floor | 12 m² (T3 absolute 7.5 — never sell that) |
| Eltern SZ · Kinder · Wohn-Ess-Koch · HWR · GWC | 15–18 · 12–15 · 45–60 · 7–9 · 3 |
| F2F default | 2900 mm (2700 + 200) |
| Stair | 17 R @ ~170 / A ~280 (2S+A≈620); dog-leg well ~2.0×3.4 m |
| South canopy | D ≈ H/tan(h_s); DACH 2.1 m window → ~1.0–1.2 m (6.1/7.3) |
| Court winter sun to floor | W/H = 1/tan(90−φ−23.5°) ≈ 3.0–4.4 (DACH) — garden-scale |
| Lichtschacht min | 1.2×1.2; rough window opening ≥ 1/8 floor (S.1), openable ≥ 1/10 floor (sliders halve) |
| Cross-vent | outlet:inlet ≥ 1.25:1, low-in/high-out; night purge = summer strategy |
| Car bay / drive | 2.5×5.0 / 3.0 — GRZ-counted! |
| RC span economics | ≤ ~6–8 m one-way (conception) |
| Wet stack | DN 100, ~1:50–1:100 (VERIFY DIN 1986), stacked baths |
| Brief-fit | Σ T4 rooms ÷ (GFZ·A·NTG) ≤ 0.95 (3.8) |
| EVERYTHING in Sections 1–2 numbers | **T1-V — replace with the parcel's B-Plan before the model leaves study status** |

## Appendix C — Client / authority intake (ask before Section 0.5)

**Parcel & law:** 1 B-Plan exists? §34 otherwise? → get the text plan +
Plan-zeichenteil; 2 which GRZ/GFZ/VGS/Wandhöhe/Baufenster/Bauweise — transcribe
with § numbers (never from memory, never from this file); 3 number of permitted
Wohneinheiten; 4 Stellplatzsatzung + GRZ-anrechnung of garages/paths; 5
Entwässerungssatzung (retention?); Hochwasser/Gefahrenkarte; 6 state LBO (which
Bundesland — Abstandsflächen + Melder +(height) versions differ); 7 Amtlicher
Lageplan / Liegenschaftskataster extract (area, boundaries, easements
Leitungs-/Wegerechte!); 8 Altlasten/Belastung, Kampfmittel? 9 Erschließung
already paid/beitragsrechtlich secured (the German "no permit without
Erschließung" gate).

**Brief:** 10 household now + in 10 years (Arbeitszimmer? Kinder? Alterssitz?);
11 units / Vermietung (decides stair + two entries, 5.4(6)/8.4); 12 rooms:
HWR, Ankleide, Gäste-WC, workshop, Gartenraum; 13 sleeping-side sensitivity
(street/Misch); 14 barrier-reduction ambitions (Dusch-WC, Aufzugsschacht
reserve — `accessibility-universal-design`); 15 KfW/Energie-Standard (affects envelope
massing + roof zone; route physics); 16 PV + Wallbox + Wärmepumpe positions.

**Context:** 17 city → φ (sun math 6.1) + climate region (DIN 4108-2 A/B/C —
digest); 18 neighbours' windows/noise on all four boundaries (7.6 — go look,
measure); 19 slope (8.6/2.6); 20 budget band (Keller yes/no, DHH vs freistehend trade-off). **Then start Section 0.5 Step 1.**

---

## Appendix S: Source Check 2026-10 — values re-read from the literature

Each line below was read again in the source books (`sources/`) in October 2026, with the
place it stands at. "Confirmed" means: a dated book prints the rule and names the standard
or law; it does not mean the current edition of that standard was opened. State law
(LBO) and local rules still override; `VERIFY` tags elsewhere in this skill stay in force
unless a line here names the edition. Where a line here differs from a section of this
skill, that section was corrected and names the line ("S.n"); the appendix governs.

### S.1 Habitable rooms in the model building code (MBO)

- Confirmed: a habitable room needs a clear height of at least 2.40 m (MBO); building
  classes 1 and 2 and attics may deviate (most state codes: 2.30 m, attics 2.20 m). —
  *Formeln und Tabellen Bauphysik* 2.7.4 (p. 150); *Gebäudetechnik* 2.1.1.
- Confirmed: the rough opening of the windows of a habitable room is at least 1/8 of the
  net floor area of the room (MBO § 47); some states accept 1/10. — *Bausanierung* 14.4.2;
  *Kompendium Nachhaltige Bauwerke* 12.7.2; *Gebäudetechnik* 2.1.1. The "1/10 openable"
  of §3.1 and §4.3 is the weaker practice rule; where the two differ, 1/8 of the rough
  opening governs.
- Confirmed (BayBO Art. 45 (1), version in force from 2026-05-01): habitable rooms need a
  clear height of at least 2.40 m, in the attic 2.20 m over half of their floor, "wobei
  Raumteile mit einer lichten Höhe unter 1,50 m außer Betracht bleiben"; the sentence does
  not hold for habitable rooms in residential buildings of building classes 1 and 2. —
  `sources/text/baybo/part-007.md`.
- Confirmed (BayBO Art. 35 (4), version in force from 2026-05-01): a window that serves as
  a way out is at least 0.60 m wide and 1 m high, opens from inside and lies no higher than
  1.20 m above the floor; in a roof slope or a dormer its lower edge, or a landing in front
  of it, is no more than 1 m from the eaves edge, measured horizontally. —
  `sources/text/baybo/part-005.md`.
- Confirmed (BayBO Art. 45 (2), version in force from 2026-05-01): the rough opening of
  the windows is at least 1/8 of the net floor area of the room "einschließlich der
  Netto-Grundfläche verglaster Vorbauten und Loggien": the floor of a glazed porch or
  loggia in front of the window is added to the room's. — `sources/text/baybo/part-007.md`.

### S.2 Distance to the boundary (MBO 2019 § 6)

- Confirmed: the depth of the setback area is 0.4 H, at least 3 m (0.2 H, at least 3 m in
  commercial and industrial areas). — *Bauphysik* 4.2. State codes deviate; VERIFY per state.
- Confirmed (BayBO Art. 6 (6) Nr. 2, version in force from 2026-05-01): balconies and
  one-storey oriels are left out of the setback depth when together they take at most a
  third of the width of the outer wall, at most 5 m each, project at most 1.50 m from the
  wall and stay at least 2 m from the opposite boundary. — `sources/text/baybo/part-002.md`.
  A loggia inside the outline is no projection: the wall behind its open side is measured.

### S.3 Defaults of this library for a simple house model

**Not from a book.** These are choices of this library, made so that a simple house can be
modelled at all where the literature gives a frame and no number. Tier T4, massing only:
any plan clause, product sheet, engineer's or carpenter's figure replaces them, and nothing
here is a design value.

- Least width of a living room: 3.5 m. §3.1 and §3.3 give widths for bedroom, bath and hall
  only.
- Finished ground floor 5 cm above the highest ground at the house: the entrance stays
  step-free and the ground can fall away from the building. The plinth and the door
  threshold then need their waterproofing detail (`roofing-waterproofing`).
- Base slab drawn 250 mm thick: the "slab 250" of the default set in §9.3.
- Basement storey drawn 2.60 m from floor to floor: with the 200 mm floor slab above it
  the rooms are 2.40 m clear, the least height of a habitable room (S.1), and the wall
  stays inside the 2.60 m clear height of a masonry basement wall without calculation
  (`masonry-construction` §9.5).
- Outer wall of a basement drawn as 240 mm reinforced concrete with 120 mm perimeter
  insulation outside: while ground and ground water are not known the model draws the safe
  side, the least cast-in-place wall of a watertight concrete structure under pressing water
  at w/z ≤ 0.55 (`concrete-detailing` §9.2, row "BKL-1 (0,55 line)"; the same figures in
  `geotechnics-foundations` §10.3), with the perimeter insulation of the worked cellar wall
  in `construction-detailing` §7.1. The ground report decides the real wall: masonry may do
  on dry, draining ground (`masonry-construction` §9.5), practice asks for 300 mm and more
  under a real head of water (`concrete-detailing` §9.2), and the earth pressure on the wall
  is the engineer's in every case (`geotechnics-foundations` §8.3).
- Base slab under a basement drawn 250 mm thick, as a raft without strip footings: slab and
  walls form one tank (`geotechnics-foundations` §6.4), and 250 mm is the slab of the same
  pressing-water row (`concrete-detailing` §9.2). The same number as the "slab 250" above,
  for another reason; the two may part.
- Knee wall of an attic storey: drawn between 0.30 m and 1.80 m high, from the attic floor to
  where the underside of the roof meets the outer face of the eaves wall. Above 1.80 m a
  local design statute no longer counts the wall as a knee wall (S.4); below 0.30 m the slope
  leaves no room at the wall, and the roof is drawn on the storey height instead.
- Under a roof with a knee wall the outer walls of the attic reach up to the underside of the
  roof and the inner walls up to the storey height, all of them cut by the slope. The storey
  height is then the height of a flat ceiling in the middle of the attic (a collar-beam
  ceiling), which the model does not draw; a room open to the ridge takes a storey height up
  to the ridge.
- Usable depth of a loggia or balcony: at least 1.50 m from the wall to the guard. A small
  table with a chair pulled out from it fits across that depth (§3.3, Dining: 700 to pull a
  chair out); the books give no depth of their own. The same 1.50 m is what a balcony may
  project in Bavaria and still stay out of the setback depth (S.2).

### S.4 Attic storey under a pitched roof

- Typical (local law, one example; Oberstaufen, Ortsgestaltungssatzung 2018, § 5 (2) and
  (3), `sources/text/dachgauben/part-005.md`): knee walls of buildings of two and more
  storeys no higher than 0.80 m from the raw attic floor to the top of the eaves purlin;
  "Wandhöhen unter der Dachschräge (Rohdecke bis OK-Fußpfette) mit mehr als 1,80 m gelten
  nicht mehr als Kniestock". Other towns set other numbers or none; the B-Plan rules first.
- Typical (Neufert 2002 p. 181, `roofing-waterproofing` S.5): a roof window at the knee wall
  has its lower edge 0.90–1.10 m above the floor.

