---
name: fire-protection-building
description: >
  Preventive structural fire protection (baulicher Brandschutz) for buildings in DACH
  practice. Building classes GK1-GK5 per MBO with heights, usage-unit areas, storey and
  Kellergeschoss/Attikageschoss rules; Hochhaus >22 m; fire resistance classes F30-F180 /
  T30-T180 / K-duct classes per DIN 4102 vs Euroclasses per DIN EN 13501-2 (R/E/I/W/M/S/C),
  reaction-to-fire classes A1/A2/B-F with s/d smoke-drop additives (EN 13501-1), national
  Baustoffklassen A1/A2/B1/B2 and MVV TB mapping; burning-behaviour tests (oven EN ISO 1182,
  calorific value EN ISO 1716, small flame EN ISO 11925-2, SBI EN 13823, Brandschacht,
  radiant panel for floors) with numeric pass criteria; escape and rescue (Rettungswege):
  two escape routes, notwendiger Treppenraum rules (width, handrails, Vorraum, smoke
  sections 30/15 m, 200 m2 opening rule, 0.50 m2 vent / 1 m2 smoke exhaust, 35 m travel,
  rescue windows 0.9x1.2 m, 8 m appliance rule, safety lighting >13 m), corridors, lift
  shafts; fire walls (Brandwaende): 40 m compartment length, farm 10 000 m3, 0.30 m
  upstand / 0.50 m slab, corner 5 m, opening and cladding rules; setback (Abstandsflaechen)
  0.4H/3 m and harte Bedachung distances 12/15/24/5 m; fire load concept (t2 fires,
  DIN 18230 framing, MIndBauRL safety categories K1-K4, compartment sizing, smoke-and-heat
  venting DIN 18232); Eurocode fire design (EN 1991-1-2 standard curve, EN 1992-1-2 tabular
  concrete, EN 1993-1-2 steel critical temperature and cladding, EN 1995-1-2 timber
  charring rates beta_n, EN 1996-1-2 masonry) with worked verification examples;
  fire-stopping and anlagentechnischer Brandschutz basics (RWA, wall hydrants/Steigleitungen,
  sprinkler classes, BMA, Loeschwasser per DIN EN 12845/W 405, emergency power).
  Provides concept-stage checks and tabular verifications, NOT approval.
---

# Fire Protection for Buildings (Baulicher Brandschutz) — DACH Practice Skill

Agent-neutral procedure skill for concept design, draft verification and review of
preventive fire protection under German building law (MBO/LBO framework, Eurocodes,
DIN 4102 / DIN EN 13501 series, MIndBauRL). German regulatory terms are kept in
parentheses because submissions, notices and authorities communicate in German.

## 0. How to use this skill

Use this skill when the task involves ANY of:

- classifying a building into a building class (Gebäudeklasse GK1–GK5), deciding whether
  it is a special building (Sonderbau) or high-rise (Hochhaus),
- deriving required fire resistance of walls, slabs, columns, stairs, shafts, doors,
- checking escape-route layout (first/second means of rescue, Treppenraum, Flur, lengths),
- sizing timber/steel/concrete sections for a required fire resistance class
  (F30…F180 / R30…R120 / REI…) with tabular or simplified Eurocode methods,
- fire walls (Brandwand), compartmentation (Brandabschnitt), roof/fire spreading
  (harte Bedachung, Abstände),
- reaction-to-fire questions: which Baustoffklasse / Euroclass a lining, insulation,
  façade or floor covering must reach, and which test proves it,
- industrial building concepts per Industriebaurichtlinie (MIndBauRL): safety category,
  compartment size, smoke-and-heat vents (WA/RWA),
- first sizing of technical fire protection interfaces: Löschwasser, Wandhydranten,
  sprinkler, BMA, RWA, emergency power, fire-stopping of penetrations.

**Siblings** (load them when the task crosses over):

| Skill | Overlap |
|---|---|
| `building-regulations-permits` | Submission procedure, Vorlageberechtigung, Abweichungen §67 MBO, LBO of the specific Bundesland, Baugenehmigung workflow |
| `structural-systems` | Loadbearing concept behind μfi utilisation, bracing, robustness/redundancy that reduces required fire resistance |
| `building-materials` | λ/ρ/c_p data, product proofs (AbZ/AbP/EAD/CE), Durability, material burning behaviour at source level |
| `building-services-tga` | Full design of TGA systems (Sprinkler, BMA, RWA, Lüftung) — here only the fire-protection interface |
| `stairs-vertical-circulation` | Dimensioning of stair flights/landings — here only the brandschutzrechtlich notwendige requirements |
| `openings-windows-doors` | Door/window build-up — here only T-RS/RA classification, closing behaviour, glazing width limits, rescue windows |

## 1. Reality check (read before producing anything)

1. The fire protection verification (**Brandschutznachweis**, §15 Bauprüfvorlagen) is a
   **submission to the building authority** prepared by a person entitled to submit plans
   (**Vorlageberechtiger**, Landesarchitektengesetz); for GK4 a planner with proven fire
   knowledge or a Prüfingenieur, for GK5/Sonderbauten a specially qualified
   Vorlageberechtigter plus review by Bauaufsicht or Prüfingenieur certificate (§66 MBO).
   **Agent output is a concept aid only.** It can prepare, structure and pre-check —
   it never substitutes the signed Nachweis.
2. Building law is **Land law**. The MBO (Musterbauordnung) is only a model; each
   Bundesland's LBO deviates (names of sections, GK relaxations, small-building rules,
   Gaeschoss definitions). All LBO-flavoured numbers below are anchored on the **MBO
   text plus an NRW-flavoured LBO digest — VERIFY against the actual Landesrecht**
   before citing in a real project.
3. Eurocode fire parts (EN 199x-1-2) + their National Annexes are introduced via the
   **Technischen Bauregeln / MVV TB** — but product use in the German system still runs
   through Leistungserklärung + application rules; DIN 4102-4 abstrahierte
   Bauteilkataloge and general test certificates remain the practical route for
   standard components.
4. Never claim, imply or draft language suggesting **approval, conformity or code
   compliance in a legal sense**. Output states: "consistent with digested rules at
   concept stage; to be verified by authorised person".
5. **MBO 2024/2025 discussions changed the Gebäudeklassen definitions** (and some
   Länder adopted faster buildings rules). GK table below is the classical
   2019-scheme — flag every GK assignment with "check current Landesbauordnung edition".

## 2. Knowledge tiers

| Tier | Authority | Content | Trust |
|---|---|---|---|
| T1 | MBO / LBO (Land) | Gebäudeklassen, Rettungswege, Brandwände, Abstände, Sonderbau-Definitionen | Verbatim digested; state deviations likely — VERIFY per Bundesland |
| T2 | DIN 4102 (national), DIN EN 13501-1/-2/-5 + MVV TB mapping, MIndBauRL 05/2019, DIN 18230, DIN 18232, Baustofflisten | Classification criteria, test programme, compartment tables | Numerically digested; MVV TB annexes get updated — VERIFY edition |
| T3 | Eurocodes fire parts EN 1991-1-2, 1992-1-2, 1993-1-2, 1995-1-2, 1996-1-2 (+NA) + design aids (DIN 4102-4 tabulated components) | Tabular dimension tables, charring rates, critical temperature, simplified methods | Tables transcribed from digest; some OCR-blurred cells — VERIFY against norm before use in Nachweis |
| T4 | Heuristics / rules of thumb | "800 rule" board thickness, char + corner allowance + standard size rounding, 5 m fire-wall corner, ladder-vs-turntable reading | Concept-stage only, never cite as proof |

Symbols used throughout: θ temperature, t time (min), β_n notional charring rate,
A_p/V ratio of heated section perimeter to volume (Profilfaktor) [m⁻¹], μ0 / μfi
utilisation ratio, R resistance, E action.

## 3. Legal structure and verification routes

### 3.1 Hierarchy (Germany)

```
Gesetz (BauO des Landes, based on MBO)
  > Verordnung (bindend; Erleichterungen claims; deviation = Antrag, §67 MBO)
      e.g. GaragenVO, VersammlungsstättenVO, IndBauRL as eingeführte Richtlinie
  > Richtlinie / Verwaltungsvorschrift (bindend only if as ETB introduced;
      deviation = equal-safety proof, §3(3) MVV TB)
      MVV TB, MIndBauRL, MHolzBauRL, M-LüAR ...
  > Technical rules: Eurocodes via Liste der Technischen Baubestimmungen;
    product route: hEN+CE+Leistungserklärung (CPR 305/2011) OR national proof:
    allgemeine bauaufsichtliche Zulassung (AbZ, DIBt) / allgemeine bauaufsichtliche
    Prüfzeugnis (AbP) / Zustimmung im Einzelfall (ZiE, Bauaufsicht).
```

- Bauregellisten were abolished 1 Apr 2019 and replaced by **MVV TB**
  (Muster-Verwaltungsvorschrift Technische Baubestimmungen, DIBt) — cite accordingly.
- MBO §1 basic duty: buildings must be sit/erected/kept so that fire or smoke
  **origin and spread are prevented**, rescue of humans and animals and effective
  firefighting (Löschangriff) are possible.
- CPR 305/2011 basic requirement "Safety and security in case of fire" (5 sub-goals):
  1) loadbearing for a defined period, 2) limited fire+smoke spread WITHIN the
  building, 3) limited spread to adjacent constructions, 4) occupants can escape or be
  rescued by other means, 5) rescue-team safety considered.
- MBO §14 protective objectives (Schutzziele): prevention; reliable rescue +
  effective firefighting; orderly structural behaviour limiting Tragverhalten,
  Raumabschluss, smoke propagation; escape for users during firefighting/rescue.
- The MBO **standard building concept assumes NO active technical systems**
  (sprinkler/BMA/RWA count only where an ordinance or an agreed Abweichung lets them
  substitute structural measures).
- Sonderbau ordinances (special buildings): MVkVO (sales), MGarVO (garages),
  MVStättVO (assembly), MBeVO (exhibitions), **MIndBauRL (industrial)**,
  MSchulBauRL (schools), MHHR (hospitals), MFlBauR, M-LüAR (HVAC), MSysBöR (raised
  floors), MLTB — state versions differ.

### 3.2 Who may prove what (§66 MBO, digested)

| Case | Verification responsibility |
|---|---|
| GK1–GK3 | Creating planner (§65(2)); nominal comparison against tabulated LBO requirements |
| GK4 | Planner with **proven fire-protection knowledge** or listed Prüfingenieur |
| GK5, Sonderbauten, Mittel-/Großgaragen | §66(1) specially qualified planner + review by Bauaufsicht or Prüfingenieur certificate |
| Deviations (Abweichungen §67) | Individual concept; for recognized systems: protective-target concept; Ingenieurmethoden require model **validation/verification + prior agreement with authority**; MIndBauRL, DIN 18230-1 and Eurocodes are pre-accepted routes |

### 3.3 Content of a Brandschutznachweis for complex buildings (BauPrüfVO §9-type list)

Concept contents (18 items, digested): fire-service access/turnaround/deployment areas;
extinguishing-water quantity and supply; extinguishing-water retention (Löschwasserrückhalt,
MLöRüRL); outer/inner compartmentation and smoke-section system incl. openings and their
closures; escape routes (layout, lengths, marking, lighting, power-operated/sliding door
behaviour); maximum user numbers; building-services-tga routing through escape routes; fire
rating of ventilation systems; NRA openings/flow rates + overpressure systems; alarm and
emergency lighting (ELA); extinguishing installations, risers (Steigleitungen), hydrants
with protection zones and special agents; standby power (batteries, gensets, circuit
integrity); hydrant plan; fire alarm panel (BMA) with sub-centres/fire-brigade panel and
trigger points; fire-brigade plan (Feuerwehrplan); operational prevention/organisation
(factory brigade, fire order, drills); deviations + compensating measures; fire-engineering
calculation methods.

---

## 4. Building classes (Gebäudeklassen, MBO §2) and storey rules

### 4.1 GK table (classical MBO 2019 scheme — VERIFY current Land edition)

| GK | Definition (digested) | Fire appliance (Rettungsgerät) assumption |
|---|---|---|
| GK1 | **free-standing** (freistehend), height ≤ 7 m, ≤ 2 usage units (Nutzungseinheiten, NE) with combined ≤ 400 m²; plus free-standing agricultural/forestry buildings | Hand ladder |
| GK2 | ≤ 7 m, ≤ 2 NE, combined ≤ 400 m² (not necessarily free-standing) | Hand ladder |
| GK3 | other buildings ≤ 7 m (i.e. > 2 NE or NE > 400 m² or ≥ 3 storeys within 7 m) | Hand ladder |
| GK4 | ≤ 13 m, each NE ≤ 400 m² (typically 3–5 storeys) | Hubretter (turntable ladder) |
| GK5 | all others — including buildings > 13 m, NE > 400 m², and **underground structures** (underground/multi-storey car parks, tunnels count via GK5 or their ordinance) | Turntable ladder / platform |

- **Height** = top **occupied** floor (hochste zu begehende/Genutztung aufweisende
  Geschoss) above the average level of the adjacent ground (gelaendeangrenzende
  Oberflaeche). Basements count toward storeys, not toward the 7/13 m if not "occupied
  floor" in the sense of the code — Land definitions differ, VERIFY.
- Quick classification logic (also digested exercise version): top occupied floor
  > 7 m → GK4 territory; > 13 m → GK5; any NE > 400 m² → GK5; ≤ 7 m decides GK1–3.
- **Hochhaus (high-rise)**: top occupied floor **> 22 m** above ground → Sonderbau →
  Hochhausrichtlinie (MHHR / Land version): Sicherheitstreppenraum (safety stairroom with
  overpressure + vestibule), Aufzug für Feuerwehr (fire-service lift), Brandmeldeanlage
  usually required. Between 13 m and 22 m: still GK5 + turntable-ladder regime, no
  Hochhaus ordinance. VERIFY threshold 22 m against Land HBauRO/HVO edition.
- Structures > 30 m height and footprints > 1600 m² (storey area per Land list) push
  into Sonderbau regardless of GK.

### 4.2 Storey definitions relevant to fire protection

| Storey | Fire-relevant treatment (digested) |
|---|---|
| Kellergeschoss (basement, KG) | Loadbearing walls/columns requirements step UP one level vs ground floors (e.g. GK3: KG feuerbeständig fb/F90 while OG feuerhemmend fh/F30); basement slabs fb from GK3; rescue: basements with ≥ 2 storeys need ≥ 2 exits; openings from stair to KG need fh + rauchdicht + selbstschließend; storage rooms in required corridors: fh + dichtschließend |
| Erdgeschoss / Obergeschosse (OG) | Standard GK table values; escape distance to stair/outside ≤ 35 m from any point of a NE |
| Dachgeschoss / Attikageschoss (top storey under/behind parapet) | Loadbearing walls: "none" only if **no occupancy above**; if dwellings/rooms in attic: normal OG values apply; top-attic walls/ceilings: GK1 none, GK2–3 fh, GK4 hfh, GK5 fb; open corridors serving the top storey: none/fh/fh/hfh/fb across GK1–5 |
| Ausgebautes vs nicht ausgebautes Dach | Unconverted roof space = storage category: partition to it fh + rsT; stairs into it may end below roof deck in GK1–3 (see 5.6) |

### 4.3 Sonderbau trigger list (NRW-flavoured, digested — VERIFY state numbering)

High-rise > 22 m; structures > 30 m; storey/floor area > 1600 m²; retail sales areas
> 800 m² (or arcades); office rooms > 400 m²; rooms with > 100 persons; assembly
establishments > 200 visitors sharing routes; grandstands > 1000 seats; gastronomy
> 40 seats (open-air > 1000); hotels/guesthouses > 12 beds; gambling halls > 150 m²;
hospitals and care units (> 6 persons per care unit / > 12 shared route); childcare,
schools, universities; prisons; campsites; amusement facilities; fliegende Bauten
(fairground rides, permit); **rack storage with goods top > 7.50 m**; storage of
fire/explosion-hazardous loads (TRGS/TRbF); "comparable" catch-all. Regulated via
SBauVO-type ordinance (assembly/hotel/sales/garage/high-rise), MIndBauRL, SchulBauR;
unregulated types → individual concept agreed with authority.

## 5. Escape and rescue (Rettungswege, first + second means of rescue)

### 5.1 Two-independent-routes principle

- Every **Nutzungseinheit (NE)** with residence rooms: **2 independent escape routes per
  storey**; both may share the same notwendiger Flur (required corridor).
- **Erster Rettungsweg** = via the notwendige Treppe (required stair) or direct outside exit.
- **Zweiter Rettungsweg** options: second stair; OR access point of fire-service rescue
  appliance (Hubrettungsgerät) — allowed only if the brigade is equipped for it and sill
  of the climbable opening **≤ 8 m** above appliance access area (above 8 m the appliance
  route is not accepted — > 8 m rule); OR waived entirely for a **Sicherheitstreppenraum**
  (fire/smoke-protected stair, high-rise regime).
- Ground-floor NE: direct exit ≤ 15 m to outside replaces stair route (digested).
- Balcony/loggia as escape element: ≥ 1.5 m lateral passable depth; separation to
  appliance area ≥ 3 m (variant with safety shaft overpressure: 1.5/3 m, distance > 3 m,
  angle > 120° — digested variant table, VERIFY exact scheme in Land rule).

### 5.2 Required stair (notwendige Treppe) — dimensional rules

| Item | Rule (digested LBO/MBO) |
|---|---|
| Coverage | Every full storey + usable roof served by a required stair; ramps allowed; folding ladders, escalators, step-hoists NOT; GK1–2 loft ladders ok to **unoccupied** roof |
| Width | Running width **≥ 100 cm** (state law; workplace regime ASR A2.3 / DIN 18065 give 120–180 cm at higher occupancy — cross-check usage) |
| Handrails | Both sides + intermediate handrail (Zwischengeländer) where needed; no door swinging directly onto a flight; landing depth ≥ door leaf width (+ swing zone) |
| Continuity | Continuous from bottom to top; different escape direction per storey allowed as exemption (GK1–3, ≤ 2 floors, ≤ 200 m²) |
| Structure | GK5: feuerbeständig + non-combustible; GK4: non-combustible; GK3: non-combustible or F30; external stairs GK3–5: non-combustible |

### 5.3 Stair enclosure (notwendiger Treppenraum)

- Own continuous shaft (Schacht); without shaft only: GK1–2, small buildings
  (≤ 2 floors ≤ 200 m²), or demonstrably safe external stair.
- **Enclosure wall quality**: GK3 fh (F30) · GK4 hochfeuerhemmend under load (F60-M) ·
  GK5 build-up of a Brandwand (F90-M).
- Linings, plasters, insulation, suspended ceilings, fixtures inside: **non-combustible**;
  combustible structure needs non-combustible lining of sufficient thickness
  (GK4-F60-BA route with linings per DIN 4102-17 melting-point mineral fibre).
- Floor coverings inside ≥ schwerentflammbar (B1 / class-C route); anti-slip profiles excepted.
- **Openings into the stairroom**:
  - to basements, unconverted roofs, workrooms/shops/storage **units > 200 m²**:
    at least feuerhemmend **rauchdicht + selbstschließend** (T30-RS),
  - to notwendige Flure: rauchdicht + selbstschließend (RS-Türen),
  - other rooms (dwellings): at least **dicht- und selbstschließend** (dT),
  - light panels in/above fire/smoke doors: total width **≤ 2.50 m**.
- **Ventilation / smoke control**: openable opening to outside **≥ 0.50 m² free area
  on every upper floor** (Obergeschoss) OR top exhaust opening (Abschlussöffnung) at
  highest point **≥ 1 m²**; for GK5/high-rise regime both + operation from ground floor
  and top landing. (0.50 m² per floor and the ≥1 m² top vent are digested values.)
- **Safety lighting** (Sicherheitsbeleuchtung) required in windowless stairwells of
  buildings with occupied floors **> 13 m**.
- **Vorraum (vestibule)** as stair continuation toward exit: width ≥ stair width; wall
  quality = stair-enclosure quality; rauchdicht-selbstschließend closures toward corridors;
  **no other openings** allowed into it.

### 5.4 Corridors and smoke sections (notwendige Flure, Rauchabschnitte)

- Corridor required: per floor with **> 4 dwellings**, and generally whenever an escape
  route runs through a corridor; exemptions ≤ 200 m² NE (residential) and ≤ 400 m² office
  NE with §29-compliant partitions + independent §33 routes; basement corridors when
  serving dwellings/NE > 200 m² or office > 400 m².
- **Rauchabschnitt (smoke section)**: corridors subdivided by rauchdicht-selbstschließend
  closures at ≤ **30 m**; dead-end (blind) corridors ≤ **15 m**; blind corridor to a
  Sicherheitstreppenraum ≤ 15 m variant.
- Corridor walls: fh (basement fb) up to rough slab (or fh ceiling if equivalent);
  doors ≥ dT (to KG storage: fh + dT); floors ≥ B1 with non-combustible linings.
- Open walkways (offene Gänge) as escape route: closure quality as doors; windows above
  them sill ≥ 0.9 m; serving-corridor wall requirements step up per GK: none/fh/fh/hfh/fb.

### 5.5 Travel distances and rescue openings

- From any point of a dwelling/storey: exit to stair or outside within **35 m**
  (straight-line per most LBO; some Land rules cap walked route — VERIFY per state).
- Stacked basements (≥ 2 KG): **≥ 2 exits each**.
- Basement room without window: needs ≥ 1 opening for smoke venting (no shared light
  wells); **Rettungsfenster**: clear opening **≥ 0.9 × 1.2 m**, sill **≤ 1.2 m** above
  floor; sloped-roof conversion: tread ≤ 1 m from eave (extendable by agreement);
  signalling toward assembly area must be possible.

### 5.6 Lifts (Aufzüge) and rescue

- Lifts are NOT escape routes. They need own shafts (≤ 3 per unit); exceptions: inside
  stair enclosure (not high-rise), spanning rooms, open storey connections, GK1–2.
- Shaft walls: GK5 fb + non-combustible · GK4 hfh (F60) · GK3 fh (F30); combustible shaft
  → non-combustible lining; shaft doors = fire-rated equivalents.
- Shaft ventilation: opening + smoke vent **≥ 2.5 % of shaft cross-section, ≥ 0.10 m²**,
  automatic release actuated from one point; wind-insensitive siting recommended.
- **Feuerwehraufs**zug (fire-service lift, EN 81-72 regime) mandatory for Hochhaus —
  details in Hochhausrichtlinie, VERIFY.

### 5.7 Fire-service access (Zufahrt, Aufstellflächen)

| Item | Rule (digested) |
|---|---|
| Rear buildings | Straight passage (Durchgang) ≥ 1.25 m wide (door 1.0 m), clearance ≥ 2.2 m (2.0 m at doors) |
| Drive-through | Needed where sill of climbable windows > 8 m and building > 50 m from street (Zu-/Durchfahrt) |
|/fire lane | Clear width ≥ 3 m, ≥ 3.5 m if enclosed along > 12 m; vertical clearance 3.5 m; turning areas per MRFlFw/DIN 14090; load class for appliances; keep clear + sign |
| Adjacent elements | fb wall quality alongside route |
| Aufstellflächen | Hub-retter deployment area per brigade equipment; off-site secured where plot cannot hold it |

## 6. Required fire resistance per building class (MBO §§26–38 / LBO table)

National labels: **fh = feuerhemmend = F30/REI30 · hfh = hochfeuerhemmend =
F60/REI60(+K260 for combustible cores) · fb = feuerbeständig = F90/REI90**.
Suffixes: -A / -AB / -B = material class of essential parts (A = non-combustible,
B = combustible permitted); "-M" = additional mechanical load (fire walls, stair walls).
"Wesentliche Teile" = all loadbearing/bracing parts + continuous closing layer
(ceilings ≥ 50 mm). VERIFY exact letter usage per DIN 4102-4 edition.

### 6.1 Loadbearing walls and columns (tragende Wände/Stützen)

| Position | GK1 | GK2 | GK3 | GK4 | GK5 |
|---|---|---|---|---|---|
| Upper floors (OG) | none | fh (F30-B) | fh (F30-B) | hfh (F60-BA) | fb (F90-AB) |
| Basement (KG) | fh (F30-B) | fh | fb (F90-AB) | fb (F90-AB) | fb |
| Top attic above occupied storeys | none | fh | fh | hfh | fb |
| Attic with no occupancy above | none | none/fh | fh | hfh | fb |

### 6.2 Slabs (Decken)

| Position | GK1 | GK2 | GK3 | GK4 | GK5 |
|---|---|---|---|---|---|
| General OG | none | fh | fh | hfh | fb |
| Basement | fh | fh | fb | fb | fb |
| Attic above occupied | none | fh | fh | hfh | fb |
| Open corridor serving as escape | none | fh | fh | hfh | fb |

- fb required under/over rooms with **explosion risk** and between farm-building and
  living use; GK1 farm/residential split slab F90-AB (non-residential).
- Openings (shafts, stairs) in slabs: GK1–2 free; within one NE ≤ 400 m² over ≤ 2
  storeys free; otherwise closures = slab's own FR class (DIN 4102-11 shafts, -5 doors).

### 6.3 Partitions, external walls, shafts, stairs (summary)

| Element | Requirement (digested) |
|---|---|
| NE-separating / dwelling-separation walls (Wohnungstrennwand) | FR of the floor but ≥ fh (F30); explosion risk → fb; KG-occupancy vs others ≥ fh; vs roof-space apartments fh; closures fh + selbstschließend |
| External walls GK4/5 | Non-loadbearing parts A1 (or fh if part of compartment); linings incl. insulation + substructure ≥ B1, **no burning drips**; balcony cladding above parapet & PV spanning > 2 storeys ≥ B1; ventilated/double-skin across storeys → special fire-spread precautions (§28(4) type), applies to GK3 double-skin too |
| Lift shafts | GK3 F30-B, GK4 F60-BA, GK5 F90-AB (see 5.6) |
| Necessary stair enclosure | GK3 F30-B · GK4 F60-BA-M · GK5 = Brandwand build-up |
| Corridor walls | GK3–4 OG F30-B; KG F90-AB; doors T30-RS to stair, T30 to KG storage |
| Roofs | **harte Bedachung** (hard roofing): resistant to flying sparks + radiant heat (DIN 4102-7 / EN 13501-5 BROOF(t1)); see 7.3 distances for soft-roof exemptions |

### 6.4 DIN 4102-4 abstrahierter Bauteilkatalog (representative rows, T3)

The tabulated component catalogue (abstrahierte Bauteile) is the practical German
verification route: for each build-up family it gives minimum thickness with/without
protective covering (Putz/beplankung). Representative values (digested; **VERIFY the
exact rows against DIN 4102-4:2016 + MVV TB introduction**):

| Component | F30 | F60 | F90 |
|---|---|---|---|
| Concrete wall, reinforced, one-sided exposed | ≥ 120 mm (or 80–100 mm with ≥15 mm plaster both sides) | ≥ 120 mm | ≥ 140–180 mm per exposure/utilisation |
| RC slab | ≥ 60 mm (+15 mm Putz routes) | ≥ 80 mm | ≥ 100 mm (or 120 with reduced cover rules) |
| RC column | ≥ 200 mm × 200 mm, a ≥ 25–30 mm | ≥ 250 mm (μ-dependent) | ≥ 300 mm (μ ≤ 0.5 route) |
| Steel column/beam | board/spray encasement per Zulassung | encasement | encasement / concrete-filled |
| Timber wall/ceiling (skeleton) | board lining layers per type A/F/H (see 8.5) | 2–3 layers | lined + oversize section |
| Masonry (calcium silicate, ρ ≥ 600) | ≥ 115 mm | ≥ 150 mm | ≥ 175–200 mm |

Rule of thumb hierarchy: covered components exploit the covering's mass/screed; the
"mit Putz / ohne Putz" columns of the catalogue differ by 20–40 mm — always state
which route (with/without covering, single/double-sided exposure) you used.

## 7. Compartmentation: fire walls (Brandwände), roofs, distances

### 7.1 When a Brandwand is required (digested)

- As **Gebäudeabschlusswand** (building-end wall): where the gable stands close to the
  boundary — digested threshold: boundary distance < 2.5 m unless ≥ 5 m of the
  adjoining wall is secured (NRW-flavoured — VERIFY per Land; many Länder instead
  require fb outer wall + no openings).
- To subdivide into **Brandabschnitte**: maximum compartment length **40 m**
  (⇒ with typical widths ≤ 40 m ⇒ compartment ≤ 1600 m² per 40 m rule of the digest).
- Agricultural: internal fire walls divide compartments **≤ 10 000 m³**; between
  dwelling and attached farm building: fb (GK1-3 farm living volume ≤ 2000 m³: fh enough).
- GK1 exemption style (two end walls): internal leaf fh + external leaf fb
  ("directional wall"/Richtungswand) accepted instead of one fb wall; fire wall may
  end below the deck in GK1–3 (conflicts with thermal/moisture detailing → recommend
  carrying it through the roof anyway).

### 7.2 Fire-wall construction requirements

| Requirement | Value (digested) |
|---|---|
| Resistance | feuerbeständig **also under additional mechanical load** (F90-M / REI90-M, A2-s1,d0 lining), non-combustible materials |
| Alignment | Through all storeys, in one plane, continuous to roof covering |
| Roof termination | Upstand **≥ 0.30 m** above roof covering OR roof-level fire-resistant slab overhanging **≥ 0.50 m each side**; no combustible roof parts crossing the wall line |
| Corners | Wall must stand **≥ 5 m** from the inner corner of an L-plan (variant > 3 m with fb flanks + angle > 120° options, digested — VERIFY state text) |
| Openings | External fire wall: **inadmissible**; internal: only where operationally needed, with feuerbeständige **dicht- und selbstschließende** closures (F90 T doors); fb glazing similarly restricted |
| Party-wall roof join | Openable roof lights ≥ 2 m horizontally from wall; eaves-connected roofs: roof facing in→out ≥ fh |
| Off-set storeys (Versatz) | fb walls + fb slab + fb external wall strip of width b at the offset (geometry conditions digested partially — VERIFY) |
| Claddings | Rear-ventilated claddings/double skins must not bridge the wall — fire-spread precautions; building-closure-wall cladding incl. insulation + substructure **non-combustible** |
| PV on roof near wall | ≥ 0.5 m clearance (non-combustible PV ≥ 0.5 m; combustible build-up ≥ 1.25 m) unless wall rises 0.30 m above — digested roof-neighborhood rule |
| Concrete minima | Normal aggregate: **200 mm unreinforced / 140 mm reinforced loadbearing / 120 mm non-loadbearing; a ≥ 25 mm** (loadbearing); see 8.3 |

### 7.3 Distances and harte Bedachung (soft-roof allowances, digested)

If a roof is NOT harte Bedachung (allowed only GK1–3 per digest), minimum distances:

| To | Hard-roofed neighbour | Soft-roofed neighbour |
|---|---|---|
| Boundary | **12 m** (WG1/2-type zones: 6 m) | **15 m** (9 m) if neighbour hard / **24 m** (12 m) if soft |
| Same-plot building | 15 m | 24 m |
| Small accessory building (no residence rooms, no fire appliance, ≤ 50 m³) | — | 5 m |

Exemptions: unoccupied < 50 m³ buildings; non-combustible skylights; roof windows on
own dwelling; entrance canopies non-combustible (combustible only toward own dwelling);
combustible roof lights/PV on otherwise qualified roof if no ignition risk or shielded;
green roofs same proviso.

### 7.4 Abstandsflächen (setbacks, building-law geometry, digested)

- Depth = **0.4 × H** (H = wall/eave height measured perpendicular to wall face),
  minimum **3 m**; on own plot, may extend over public street/green/water areas to
  their centre; no overlapping.
- Gewerbe-/Industriegebiete: 0.2 × H ≥ 3 m; residential GK1–2 ≤ 3 storeys: flat 3 m suffices.
- **For fire-wall gables the setback is not the fire protection** — the wall quality
  rules (7.1/7.2) apply in addition; a 3 m setback does NOT replace a Brandwand when
  the boundary-distance trigger is met.

## 8. Classification systems and burning behaviour

### 8.1 National materials (DIN 4102-1) — legacy but still in Zulassungen/wording

| Class | Meaning | Core tests (digested) |
|---|---|---|
| A1 | nicht brennbar (fully) | Ofenprüfung + Heizwert + Brandschacht + Rauchprüfung |
| A2 | nicht brennbar (substantially) | Ofenprüfung + Heizwert/Wärmeentwicklung + Brandschacht + Rauch |
| B1 | schwer entflammbar | Schachtofenprüfung (box fire, vertical spread limited) + Kleinprüfstand |
| B2 | normal entflammbar | Kleinprüfstand (small burner); B3 deprecated |
| Components | F30/F60/F90/F120/F180; T30–T180 doors; RS (rauchdicht selbstschließend) / dT (dicht + selbstschließend) door suffixes; ducts Lüftungsleitungen K30–K90 (DIN 4102-6/-21); cable penetrations S30–S180 (-9); pipe/shaft seals R30–R120, I30–I120 (-11); cable function maintenance E30–E90 (-12); fire glazing G30–G120 (-13) | — |

**Ofenprüfung**: furnace 750 °C; specimen until max furnace temperature, ≥ 15 min,
≤ 90 min; PASS = no ignition in any specimen AND furnace temperature rise ≤ 50 K.
**EN ISO 1182** (Nichtbrennbarkeit): 5 cylinders Ø 45 × 50 mm, 30–60 min, max
temperature rise ΔT governs. **Brandschacht** (DIN 4102-15/-16) evaluates smouldering;
the SBI does NOT (glowing gap — new EU glowing test under development). **Floors**:
DIN 4102-14 / EN ISO 9239-1 radiant panel: flame spread length vs time, critical
radiant flux at extinction, smoke density.

### 8.2 Euroclass reaction (DIN EN 13501-1) — numeric criteria (digested)

| Class | Criteria |
|---|---|
| A1 | EN ISO 1182 **ΔT ≤ 30 K, Δm ≤ 50 %**, no sustained flaming; EN ISO 1716 **PCS ≤ 2.0 MJ/kg** (homogeneous; alt ≤ 1.4 MJ/m² footnotes) |
| A2 | 1182: **ΔT ≤ 50 K, Δm ≤ 50 %**, tf ≤ 20 s; 1716: **PCS ≤ 3.0 (kg, non-uniform 4.0) MJ/kg / ≤ 4.0 MJ/m²**; EN 13823 SBI: **FIGRA ≤ 120 W/s, LFS < edge, THR600s ≤ 7.5 MJ** (+ 11925-2 no flashover) |
| B | SBI FIGRA ≤ 120 W/s, LFS < edge, THR ≤ 7.5 MJ + EN ISO 11925-2 (30 s flame) |
| C | FIGRA ≤ 250 W/s, LFS < edge, THR ≤ 15 MJ + 11925-2 |
| D | FIGRA ≤ 750 W/s + 11925-2 |
| E | only EN ISO 11925-2 passed (mark not reached ≥ 20 s after 15 s flame; Fs ≤ 150 mm/60 s) |
| F | fails E / no performance |
| Smoke | s1: SMOGRA ≤ 30 m²/s² AND TSP₆₀₀ ≤ 50 m² · s2: ≤ 180 / ≤ 200 · s3: rest |
| Droplets | d0: none 600 s · d1: none burning > 10 s · d2: fails/ignites filter in 11925-2 |

Test map: EN ISO 1182 oven, EN ISO 1716 PCS calorific value, EN ISO 11925-2 small
flame (=Brennkasten equivalent; DIN pass → E), EN 13823 SBI (single burning item,
sand-bed burner) — the DIN Brennkasten itself gives the B2↔E bridge. (Source printed
"THR500s"; standard index is THR600s — corrected, VERIFY edition.)

### 8.3 MVV TB mapping Euroclass → national acceptance (digested)

```
A1 → A1           A2-s1,d0 → A2
B-s1,d0 / B-s2,d0 / C-s1,d0 (variants) → B1 (with product-specific s/d data in proof)
D-s1,d0/d1/s2… , E → B2        F → B3 (deprecated)
feuerhemmend → R30 / REI30 / E-d2 (A2-s1,d0 for non-comb variant)
hochfeuerhemmend (combustible structure) → R60 + K260-REI / lining A2-s1,d0
Brandwand-equivalent party wall in wall type → REI60-M (incl. mechanical) /
   full Brandwand → REI90-M, A2-s1,d0
REI120 = 120 min; non-loadbearing internal EI30…; external E30(i→o) / EI30-ef(0→i),
   "-ef" = external-fire exposure.
Roofs: harte Bedachung ≈ BROOF(t1) pass (spark + radiant); FRoof(t1) = soft.
```

### 8.4 EN 13501-2 resistance classes (format and criteria letters)

Format `R E I W t (M S) C…`. **R** loadbearing · **E** Raumabschluss (integrity: no
flame/cotton-wool ignition; mean unexposed rise ≤ 140 K, single point ≤ 180 K; wall
pendulum impact 20 Nm) · **I** Dämmung (insulation) · **W** radiation (glazing) ·
**M** mechanical impact · **S** smoke (S, S₂₀₀ = ambient + 200 °C) · **C** self-closing
(+ cycle class) · **P** circuit integrity (cables). Loadbearing criteria = design use
load or self-weight + deflection-rate limit (Δf/Δt)_lim = l²/(9000·h) [l, h in m].
National ↔ EN component shorthand: fh = R30/REI30 · hfh = R60(+K260)/REI60 · fb = R90/REI90.

### 8.5 Eurocode fire design — design philosophy

Three verification levels (digested): **1 tabulated** (EC2/EC6 tables, DIN 4102-4),
**2 simplified calculation** (EC3 temperature level +5× / charring methods EC5),
**3 advanced/general** (thermal + structural transient analysis — must be validated,
authority agreement for building-law use). Hot design always needs the cold
part-1-1 design as basis. Binding parts list (digested editions): EN 1991-1-2:2010,
1992-1-2:2010/A1:2019+NA, 1993-1-2+NA, 1994-1-2/A1, 1995-1-2+NA, 1996-1-2, 1999-1-2.

**Standard temperature–time curve (ETK, ISO 834 / EN 1991-1-2 §4.2):**

```
Δθg = 345 · log10(8 t + 1)   [K; t in min]   (θg = θ0 + Δθg)
```

θg(30) ≈ 678 °C, θg(60) ≈ 842 °C, θg(90) ≈ 945 °C, θg(120) ≈ 1029 °C — sanity anchors.
The curve is the basis of component tests (DIN 4102-2/-3/-5/-6/-9/-11) and of tabulated
FR classes. Real compartment fires deviate (ventilation-controlled, shorter hotter or
longer cooler) → reason for parametric/area-specific curves in Ingenieurmethoden (10.2).

## 9. Eurocode fire design by material

### 9.1 Timber (EN 1995-1-2, reduced cross-section method)

Charring is predictable; the char layer insulates the residual core. Design steps:

```
d_char,n = β_n · t                                  (notional charring depth)
d_ef     = d_char,n + k0 · d0 ,  d0 = 7 mm,
           k0 = min(1 ; t/20)                        (corner/protective-zone allowance)
residual section = gross − d_ef on every charred face
```

Design charring rates β_n [mm/min] (digested EC5 table + NA):

| Product | β0 | β_n |
|---|---|---|
| Softwood solid/glulam ρk ≥ 290–330 | 0.65–0.70 | **0.70** |
| Sawn softwood ρk ≥ 290 (NA route incl. residual-zone) | — | **0.80** |
| Hardwood ρk ≥ 290 / ≥ 450 | — | **0.70 / 0.55** |
| LVL ρk ≥ 480 | — | **0.70** |
| Wood-based panels: panelling/boards 0.9, plywood 1.0 (ρ 450, d 20 basis) | — | 0.9–1.0 |

Strength in fire: f_k,fi = k_mod,fi·f_k/γ_M,fi with γ_M,fi (digested): solid 1.25,
glulam 1.15, panels 1.15, LVL 1.1; shear connections wood-side plates 1.15, outer
steel plates 1.05, pull-out 1.05; k_mod per cold classification (or the digested
worked-example shortcut k_mod,fi = 1 − (1/200)·(humid-share indicator)). Reductions
for bending/compression/strength at temperature apply via the k_fi factors of
EN 1995-1-2 3.1 (digested values partly lost — VERIFY before numeric use).

- Protective gypsum linings (type A/F/H to EN 520): onset time t_prot from
  insulation-thickness/density chart; add **outer layer + 80 % of inner** (type F) or
  + 50 % (A/H); joints offset, inner fixings ≤ outer.
- Buckling / LTB: check per part 1-1 §6.3 **with the fire-time bracing layout**.
- Loadbearing timber to F60/F90 is feasible via oversized sections + linings
  (MHolzBauRL governs the building-law route for timber buildings; VERIFY state adoption).

### 9.2 Steel (EN 1993-1-2)

Bare steel = max ~R30 at best (yield collapse ~500–600 °C; the digested basis:
strength loss starts > 500 °C, 5 %-strain criterion; θ_a ≥ 350 °C already reduces
capacity per NA). Protection: concrete encasement, spray/plaster, boards, intumescent.

**Temperature-level method** (deformation/stability irrelevant):

```
check:  θ_a,cr ≥ θ_a,t                       (9.2-1)
μ0    = E_d,fi / R_d,fi,0                    (utilisation at t = 0, fire combination)
θ_a,cr = 39.19 · ln[ 1/(0.9674 · μ0^3.833) − 1 ] + 482   [°C]     (9.2-2)
        valid μ0 ≥ 0.013 (below: θ_a,cr ≈ 1000 °C)
```

Anchor values (computed with 9.2-2, matching digested examples): μ0 0.52 → 578 °C ·
0.59 → 557 °C · 0.65 → ~543 °C · 0.70 → ~534 °C. (The source printed a garbled variant
of this formula — the canonical equation 9.2-2 reproduces both examples; VERIFY vs
NA edition.) Alternative route: read θ_a,cr from the k_y,θ reduction curve.

**Section factor A_p/V** [m⁻¹] (heated perimeter / steel volume, digested geometry rules):

| Encasement | A_p/V |
|---|---|
| Box (full surround) | 2(b + h)/A |
| U-shape lining (3 sides) | (2h + b)/A − gap corrections (gaps c ≤ h/4 still treated closed) |
| Open profile all sides | real perimeter/A (I-sections per class table) |

**Protected heating (simplified, EC3 4.2.3/8.4)**: incremental form with time step
Δt ≤ 30 s; the practical board design reduces to the digested **"800 rule"** (T4):

```
(A_p/V) / (d_P/λ_P) ≤ 800 m⁻¹·m·K/W ... → d_P ≥ λ_P · (A_p/V) / 800
(basis: 90 min at θ_a,cr = 557 °C, i.e. μ0 ≈ 0.59; other durations shift the limit —
use the manufacturer chart/nomograph for R120 etc.)
```

Protection material data (digested, typical): insulating mortar/plaster (vermiculite/
perlite) λ_P ≈ 0.12 W/mK, c ≈ 1100 J/kgK, ρ ≈ 550 kg/m³ · fire-rated gypsum board
λ_P ≈ 0.20–0.25 W/mK, c ≈ 1700, ρ ≈ 945. (λ of boards differs between digests 0.20 vs
0.25 — VERIFY product λ_P from its Zulassung/DoP; use the certified value.)

Tension members: limit θ_a,lim if excessive elongation harms the structure. Member
check general: E_d,fi/R_d,fi,t ≤ 1 with k_y,θ = f_y,θ/f_y (S235/S355).

### 9.3 Concrete (EN 1992-1-2 tabular — T3)

μfi = N_Ed,fi/N_Rd,fi,0 (9.3-1). Normal-weight quartz aggregate 2000–2600 kg/m³,
exposure 1-sided unless noted; h_min = min dimension, a_min = bar axis distance [mm]:

**Columns (braced frames; method B unusable in Germany per NA)** — rows = increasing μfi
(≈0.2 / 0.5 / 0.7) + circular reference:

| Class | b_min/a_min (rect., 1-sided) | circular |
|---|---|---|
| R30 | 200/25 · 200/25 · 200/32 | 155/25, 300/27 |
| R60 | 200/25 · 200/36 · 250/46 | 155/25, 300/31, 350/40 |
| R90 | 200/31 · 300/45 · 350/53 | 155/25, 300/25, 400/38 |
| R120 | 250/40 · 350/45ᵃ · 350/57ᵃ | 175/35, 350/35, 450/40ᵃ |
| R180 | 350/45ᵃ · 350/63ᵃ · 450/70ᵃ | 230/55 |
(ᵃ ≥ 8 bars; prestressed: increase a per 5.2(5); slenderness limits + l_o < 3 m
conditions of Tab 5.2 apply — check them whenever the table is invoked.)

**Loadbearing walls (h/a_i, two-sided exposure pairs, μfi 0.35 / 0.70):**
REI30 120/10·120/10 | 120/10·120/10 · REI60 130/10·140/10 · REI90 140/25·170/25 ·
REI120 160/35·220/35 · REI180 210/50·270/55 (μfi 0.35/0.70; 1-sided values 100–180 mm
in the first pairs — VERIFY cells against Tab 5.4; OCR-compressed).

**Non-loadbearing closing walls (EI, h/l ≤ 40):** 30:60 · 60:80 · 90:100 · 120:120 ·
180:150 · 240:175 mm (limestone aggregate −10 %). **Brandwand concrete minima: 200
unreinforced / 140 reinforced loadbearing / 120 non-loadbearing; a ≥ 25.**

**Slabs (two-way/one-way simply supported, t/a 1-way/a 2-way):** REI30 60/10 ·
REI60 80/20 · REI90 100/30 · REI120 120/40 · REI180 150/55 · REI240 175/65;
flat slab: 30:150/10 · 60:180/15 · 90:200/25 · 120:200/35 · 180:200/45 · 240:200/50.

**Beams simply supported (b_min WA/WB/WC; a_min):** R30 120/160/200 t_w 80 a 15/15/20ᵃ ·
R60 160/200/300 t_w 80–100 a 25–35 · R90 200/300/400 t_w 100–110 a 35–45 ·
R120 240/300/500 t_w 120–130 a 50–60 · R180 300/400/600 a 60–70 (continuous beams:
milder tables — Tab 5.6; redistribution ≤ 15 %; ≥ REI90 keep 20 % of required top
rebar continuous over supports; span-reduction rule h = 0.3·l_eff for cutting field bars).

Spalling: normal concrete ok on standard ETK; lightweight/aggregate-sensitive cases
and siliceous round-aggregate concrete → VERIFY aggregate group adjustments.

### 9.4 Masonry (EN 1996-1-2, summary rows — VERIFY)

Non-loadbearing EI t_F [mm] (brick 500–2400 kg/m³, with/without putty): 30:100(70) ·
60:140(100) · 90:170(140) · 120:190(140) · 180:210(170). Silico-calcaire (KS 600–2400):
70/90/100/140/170/200. AAC 350–500: 70/75/100/100/150/190. Loadbearing rows stricter
(e.g. brick fb≤25, α ≤ 0.6: REI30 100 → REI180 365–370). Putty (beidseitiger Putz)
reduces required thickness. α = e/h eccentricity ratio limits applicability.

### 9.5 Fire-stopping of services and joints (qualitative + class names)

- Pipe/shaft seals: **R30–R120** (DIN 4102-11: fire-resistant closures around pipes),
  **I30–I120** for insulations; cable penetrations **S30–S180** (DIN 4102-9);
  cable function maintenance **E30–E90** (DIN 4102-12 / EN 50200 regime) for
  safety circuits (RWA, alarm, pumps, lift).
- Ducts crossing compartments: fire dampers (BSK, DIN EN 1366-2 regime) or
  fire-resistant ducts **K30–K90** (DIN 4102-6/-21); BSK released by BMA and fusible link.
- Ventilated cavity: **Brandriegel every ≤ 50 cm of cavity depth** (digested façade
  example); horizontal **Brandriegel at façade base/parapet line** to stop inter-storey
  flashover; ACP panels: non-combustible cores only at escape-facing façades (post-
  Grenfell-era Baustofflisten/MVV TB requirement — VERIFY current MVV TB clause).
- Penetration principle: the seal must reach the **FR class of the component it
  penetrates**; the classification covers annular gap size + pipe material/diameter
  range — match the certificate, don't extrapolate.

## 10. Fire load, concepts, industrial buildings

### 10.1 Fire development and design fires

- Phases (digested): ignition (Entzündung) → smouldering/growth (Entstehungsbrand;
  **flashover** when hot gases ignite the whole load — liquids: no smouldering phase)
  → fully developed (Vollbrand, O₂-controlled; insulated envelopes reach hotter gas
  temperatures attacking structure) → decay (fuel out, heat flows back from elements).
- Fire triangle: fuel + oxygen + heat. Ignition sources near combustible façades
  (waste containers!) need clearance/enclosure.
- **t² design fire**: Q̇(t) = α·t² (α growth constant [kW/s²]; digested real children's-
  room full-scale test followed a FAST-curve t² growth; room fire load there:
  **462 MJ/m²**, contents 307 kg / 6335 MJ — plastics 83 kg → 2460 MJ, wood 224 kg →
  3875 MJ). Typical α values (slow 0.003 / medium 0.0125 / fast 0.047 / ultra-fast
  0.188 kW/s²) are general fire-engineering constants — VERIFY against EN 1991-1-2
  Annex E before use.
- Designers should note: the ETK (§8.5) is a **test** curve, not a prediction;
  compartment fires are ventilation/fuel dependent.

### 10.2 Ingenieurmethoden (performance-based design)

Allowed via building codes where tabulated routes cannot be met (complex geometry,
attractive architecture, deviations). Proof chain (digested): define **Schutzziel**
(safety objective) → acceptance criteria (e.g. tenability times, required FR duration
from heating analysis) → verified calculation. Tools: zone models, CFD, thermal-
structural analysis, evacuation models. Models must be validated/verified per
**ISO 16730-1…-5**; software choice fits the question; users need fire-physics +
numerical competence (vfdb Leitfaden Ingenieurmethoden, TB 04-01 series).
Pre-accepted special routes: MIndBauRL, DIN 18230-1, EN 199x fire parts. Agreement
with the authority **beforehand** is mandatory in practice.

### 10.3 DIN 18230 fire-load method (framing)

- Purpose: compute required FR duration of components from the **specific fire load**
  q_B instead of the standard ETK — component-wise only (no overall-structure rules;
  expansion joints/static systems/fuse points need separate treatment).
- Inputs (digested): use, structure, fire load (specific, MJ/m²), thermal insulation +
  vent openings (Abzugöffnungen), infrastructure. Required time uses the "Ausnutzungsgrad"
  of the compartment vs its venting.
- **The explicit q_B formula and DIN 18230-3 tables are NOT in the digested material**
  (only referenced). Standard definition to verify against the norm:
  q_B = Σ(b_f,i · q_r,i · A_i)/A with combustion factor b_f and calorific value q_r —
  **VERIFY in DIN 18230-1 before use**.
- Worked anchor from digest: machinery hall **q_R ≈ 83 kWh/m²** (= 299 MJ/m²) treated as
  high fire load class in MIndBauRL compartment tables.

### 10.4 MIndBauRL (Industriebaurichtlinie 05/2019 — VERIFY current edition)

- Scope: production/storage buildings; **exclusions**: enclosure-only uses,
  predominantly open buildings, rack storage > 9 m; TRGS/TRbF/LöRüRL/MKAR untouched.
- Compartment (Abschnitt) = between external/fire walls; firefighting compartment =
  designed for the critical fire.
- Escape (digested): main aisles ≥ **2 m** straight to exits; rooms > 200 m² → ≥ 2 exits;
  ≤ **15 m** to aisle; ≤ **35 m** to exit (ceiling ≤ 5 m) / ≤ 50 m (≥ 10 m);
  extensions to 50/70 m with automatic flame/smoke detection or extinguishing
  (printed "+15 m each?" — VERIFY).
- **Safety categories K1–K4** drive allowed compartment size × FR class:
  K1 none · K2 automatic fire alarm · K3.1 fire brigade on duty in shifts ·
  K3.2 team · K3.3 two shifts · K3.4 three shifts · K4 automatic extinguishing
  (sprinkler). Digested anchor: single storey, non-combustible no-flame-work K1,
  WAB ≥ 5 % and width ≤ 40 m ⇒ compartment ≤ **1800 m²** without component FR;
  with F30-B components ≤ **3000 m²** (steel then needs R30 protection — boards or
  intumescent) — **VERIFY table 1 cells in current edition**.
- Smoke-and-heat vents (WAB, WA): geometric vent area **≥ 5 % of compartment floor**
  (digested example: 2050 m² → 102.5 m² required); **smoke-exhaust openings (SMA/AW)
  ≥ 1.5 m² each, one per ≤ 400 m²** (variant "per ≤ 200 m² + 10 %" also noted — VERIFY);
  supply air ≥ ~50 %?/lower third on ≥ 2 sides (example required 12 m² — derive from
  current §, don't copy); wall vents upper zone.
- Three proof procedures — simplified (no fire load), DIN 18230 (with fire load),
  performance-based — **mixing prohibited**.

### 10.5 Smoke-and-heat extraction design basics (DIN 18232 series)

- Tenability targets (digested): keep smoke-free layer **≥ 2.50 m** high;
  layer gas **< 300 °C during incipient phase**; vent sections < 1600 m²
  (smoke curtains/screens h_sch); **supply air ≥ 1.5 × effective vent area A_AW**;
  dimensions via design fire release rate, computation fire area, design groups;
  design time ≈ 10 min detection + 10 min response; vents evenly distributed;
  plume geometry z = h − d.
- NRA = natural (buoyancy, auto/manual), MRA = mechanical fan, RDA = pressure-differential
  (Δp-controlled incl. leakage), AV = heat vents. EN 12101 product series (only triggers
  present in digested TGA material — keep dimensions at concept level, VERIFY).

## 11. Anlagentechnischer Brandschutz (active systems — interface level)

Assume **none** for the standard MBO building; where systems are installed/required
(Sonderbau ordinances, MIndBauRL K2/K4, agreed Abweichungen), hand detailed design to
the services skill. Key digested anchors:

| System | Anchors (digested) |
|---|---|
| Löschwasser (fire water, DVGW W 405) | network pressure ≥ **1.5 bar at every node during withdrawal**, duration **2 h**; base load = max hourly demand of average day; demand by use + spread risk: kleine 48 / mittlere 96 / große **192 l/min** classes (matrix by Bauart partially lost — VERIFY W 405 table) |
| Wandhydranten (wall hydrants) | shut-off + 15–30 m form-stable hose; **C (DN50) / B (DN80)** couplings; niche sizes wet 70–74/80/25 cm, dry 32/42/14.5–16 cm (DIN 14461) |
| Steigleitungen (risers) | **nass** always pressurised (usable before brigade arrives; freeze risk) · **trocken** filled by brigade via Siamese at access (hydrant ≤ 80 m from building, feeder vehicle reachable) · nass/trocken auto-fill on alarm + drain; ≥ 1 hydrant per ≤ 80 m; expose above ground beats recessed (parking blocks) |
| Sprinkler (VdS CEA 4001 / EN 12845 regime) | bulb actuation ~30–50 K above ambient (typ. 68–78 °C); coverage 9–21 m²/head by hazard class **LH/OH/HHP/HHS**; water sources art 1–4 (office LH ≤ 1000 heads → art 1 elevated/pressurised tank); 75 % of room fires controlled by 1–4 heads; dry zones dry-pipe; deluge for rapid-flame (rubbish bunkers, stages); water curtains as separation (> 8 m hall height questionable); mist variants; tank load up to 200 kN/m² on structure! Engine drive to emergency power; enables Abweichungen (rarely on escape routes); insurance discounts via VdS |
| BMA (fire alarm, DIN 14675 Kategorie 1/2) | detectors: ionisation (early gas, avoid cold/draft), optical scatter (PVC smoke reliable), flame, thermal max 70 °C / rate-of-rise 10 K/min ≥ 2 min, multi-sensor 3D/4D; manual call points per storey/stair; panel dials brigade + feeds deployment plans; standby **72 h** batteries; releases BSK dampers, doors, sprinkler alarm valve, boosters, genset |
| RWA triggers | BMA/MA + emergency power + smoke duct dampers + lift EN 81-73 recall + stairwell pressure ventilation (see 10.5) |
| Löschwasserrückhalt | extinguishing-water retention per LöRüRL/MLöRüRL (oil separators, dams at ramp edges); quantity concept per site — only named in digests, design in services skill, VERIFY |
| Ersatzstrom (safety loads) | corridor/smoke-duct dampers, fire-water boosting, stair ventilation, RWA, firefighter lifts → function-maintaining wiring **E30–E90**: fire-resistant ducts/board trunking or defined screed cover on raw slab; ≥ 3 h or 72 h logic per object type |
| Cables in escape routes | only non-combustible pipes in notwendige Flure/Treppenräume; cable heat values kWh/m: PVCC 6.4, PVC 7.75, PP 11.8, PE-HD 14.6–17.8 — halogen-free = self-extinguishing, low smoke, no corrosive halogens |
| Lüftung (MLüAR/M-LüAR) | ducts through compartments per 9.5; kitchen/garbage exhaust codes (DIN 18869/TRGS) thin in digests — VERIFY |

## 12. Worked examples (full arithmetic, digested)

### 12.1 Timber beam R30, four-sided char (C24, 14/24, bay e = 0.60 m, l = 5.00 m)

Loads (accidental fire combination, γG = γQ = 1.0, ψ1 = 0.5):
g_k = 1.5 kN/m², q_k = 2.0 kN/m² → q_fi = 1.0·1.5·0.6 + 0.5·2.0·0.6 = **1.50 kN/m**
M_fi = q·l²/8 = 1.5·25/8 = **4.69 kNm**.

Reduced section (sawn softwood β_n = 0.80 mm/min; t = 30 min; k0 = min(1, 30/20) = 1):
d_char,n = 0.8·30 = 24 mm; d_ef = 24 + 7 = 31 mm per charred face →
b_ef = 140 − 2·31 = 78 mm; h_ef = 240 − 2·31 = 178 mm → W_y = 7.8·17.8²/6 = **411.9 cm³**.

Stress: σ_m,fi = 4.69·10⁶/411.9·10³ = **11.39 N/mm²**.
Strength: k_fi = 1.25 → f_m,0,k,fi = 1.25·24 = 30; f_m,d,fi = k_mod,fi·30/γ: with
γ_M,fi = 1.25·(1.0/0.839…) — digested run used k_mod,fi ≈ 0.839, γ_M,fi 1.0 route →
f = 30·0.839/0.84 ≈ 30 → util 11.39/30 = **0.38 ✔** (source: 0.39 OK).
LTB (unbraced bottom flange in fire): σ_cr ≈ 0.78·(b²/h)/l·E0,05,fi → λ_rel =
√(24/39.46) = 0.78 → k_crit = 1.56 − 0.75·0.78 = **0.975** → util = 11.39/(30·0.975)
= **0.39 ≤ 1 ✔**. Idealised reduced-variant (10 mm lost-strength zone instead of k0
rule) gave 0.33 — either route passes; R30 on 14/24 C24 has margin.

### 12.2 Timber column sizing F60, four-sided (sawn softwood β_n = 0.80)

Demand: residual core ≥ 100 × 100 mm to carry the load (concept-stage assumption —
replace with real 12.1-style check).
d_char,n = 0.8·60 = 48 mm; k0 = 1 (t ≥ 20) → d_ef = 48 + 7 = 55 mm.
a_req = 2·d_ef + 100 = 2·55 + 100 = **210 mm** → specify **22/22 cm** standard section.
(Hardwood ρ ≥ 450 with β_n 0.55: d_ef = 33+7 = 40 → a ≥ 180 → 18/18 suffices —
the density/β_n choice drives the section!)

### 12.3 Steel column HEB400 + gypsum-box lining, R120, μ0 = 0.52

θ_a,cr = 39.19·ln[1/(0.9674·0.52^3.833) − 1] + 482 = **578 °C** (9.2-2, matches digest).
Section factor (box envelope 400×300 about A = 198 cm²): A_p/V = 2(0.4+0.3)/0.0198 =
**70.8 m⁻¹**. Lining 2×12.5 mm fire-rated gypsum, d_P = 25 mm, λ_P = 0.25:
chart/nomograph at 120 min → θ_a(120) ≈ **630 °C > 578 °C → FAIL** — needs thicker/
denser board or 3 layers (chart values VERIFY against product nomograph).
Contrast with the 800-rule at 90 min/557 °C: d_P ≥ λ_P·(A_p/V)/800 →
- IPE360 vermiculite mortar (λ_P 0.12, A_p/V 163): d_P ≥ 163·0.12/800 = 24.5 mm → **25 mm**,
- HEA180 gypsum box (λ_P 0.20, A_p/V 155): d_P ≥ 155·0.20/800 = 38.8 mm → **2×20 mm boards**,
  envelope 26×26 cm beats an RC equivalent ~35 cm — slimness argument for protection.

### 12.4 RC column R60, 350/350, a₁ = 48 mm, C20/25, B500, A_s = 45.2 cm²

Actions G_k = 350 kN, Q_k = 150 kN; fire combination (ψ-type 0.5…) → digested result
η/μfi = **0.7**. Geometry limits met: braced, l_o < 3 m, A_s < 0.4·A_c.
Tab 5.2a row R60, μfi ≤ 0.7 (one-sided): b_min **250 mm**, a_min **46 mm**.
Check: 350 ≥ 250 ✔ · 48 ≥ 46 ✔ → **R60 by table, no further action**.
(At μfi 0.5 → 200/36 would even allow 300/30; the utilisation class drives everything.)

### 12.5 Concrete elements quick-checks (tabular, 1-sided/standard exposure)

- Non-loadbearing EI90 closing wall: h ≥ **100 mm** (quartz concrete; limestone −10 →
  110 mm); h/l ≤ 40.
- Loadbearing REI90 wall μfi ≤ 0.7, two-sided: **h ≥ 170 mm, a ≥ 25 mm**.
- Brandwand: reinforced loadbearing ≥ **140 mm**, a ≥ **25 mm**; unreinforced ≥ **200 mm**.
- Flat slab REI60: h ≥ **180 mm**, a ≥ **15 mm**; REI90: h ≥ 200, a ≥ 25.
  All VERIFY cells against EN 1992-1-2 + NA tables before citing.

### 12.6 Compartment venting concept check (MIndBauRL hall, 50×41 = 2050 m²)

q_R ≈ 83 kWh/m² (machining). Route I (component FR): K1 ground floor, non-combustible
no hot work ⇒ ≤ 1800 m² — exceeded ⇒ either F30-B components ⇒ ≤ 3000 m² (steel gets
board/intumescent R30 per 12.3) **or** route II: WAB ≥ 5 %·2050 = **102.5 m²**;
provided: roof vents 103.33·0.9 = 93.0 + geometric wall RWA 6·(1.25·2.5 = 3.125→)
6·1.875 = 11.25… digested total **111.75 m² > 102.5 ✔**.
Smoke clearance (MIndBauRL 5.7.1.1): 1 SMA per 400 m² with A_w ≥ 1.5 m² → 5·1.5 = 7.5;
provided 6·2.11 = 12.66 ✔; supply air ≥ 12 m² in lower third on ≥ 2 sides → 19.06 ✔.
(Variant rule "1.5 m² per ≤ 200 m² + 10 %" noted in source — VERIFY which applies.)

## 13. Per-building-type concept table (derived from digested GK/LBO rows)

| Type (typical GK) | Loadbearing OG / KG | Slabs | Stair | Corridor | Special triggers |
|---|---|---|---|---|---|
| Single house (GK1) | none / F30-B | none / F30-B | none required | none required | harte Bedachung or 12/15/24 m distances; gable → Brandwand if boundary < 2.5 m (VERIFY Land); loft ladder ok |
| Two-family house (GK2) | F30-B all / F30-B | F30-B (attic if rooms above) | F30 enclosure variant, no shaft needed ≤ rules | only basement big units | second escape per NE (appliance ≤ 8 m or 2nd stair) |
| Row/duplex terraces (GK2–3) | party wall = Richtungswand/Brandwand route: inner fh + outer fb, or full fb | FB between units on slab line | per unit | — | roof continuity at party line; openable lights ≥ 2 m from wall |
| Multi-unit ≤ 7 m (GK3) | F30-B / F90-AB | F30 / F90 KG | F30-B shaft, fh walls, 0.5 m² vent/floor, T30-RS to KG | required > 4 dwellings, 30 m smoke sections, F30 walls (KG F90) | NE > 400 m² pushes GK5! |
| Apartment ≤ 13 m (GK4) | F60-BA / F90-AB | F60 / F90 | F60-BA-M enclosure, noncomb structure, safety light ≤ >13 m n/a but check | F30 OG / F90 KG, T30 | turntable regime; external wall linings B1 no drips; balcony cladding B1 |
| > 13 m or big units (GK5) | F90 everywhere | F90 | Brandwand-quality enclosure; vent 0.5 m²/floor AND 1 m² top; safety lighting | F30 OG/F90 KG | Prüfingenieur route; lift shaft F90 |
| Hochhaus > 22 m (Sonderbau) | F90 + robustness | F90 | **Sicherheitstreppenraum + Vorraum + Überdruckanlage**, Feuerwehraufzug | F30/F90 + rsT | BMA typically; HBauRO/HHVO details VERIFY |
| Hotel / boarding > 12 beds (Sonderbau) | per GK + VStätt/hotel ordinance add-ons | — | second route per room wing; room-of-stay doors | smoke sections | sprinkler/BMA often via ordinance |
| Sales store > 800 m² / atrium > 1600 m² | fb compartments | fb | multiple exits, widths by occupancy (VERIFY state) | 30 m rule | MVkVO; open floors need Rauchabschnitt concept |
| School / Kita (Sonderbau) | per GK + SchulBauR | — | wide stairs (occupancy), 2 routes | — | MSchulbauR escape widths VERIFY |
| Industrial hall (MIndBauRL) | table per K-category (K1: F30 at 3000 m²; > 1800 m² even without, via WAB 5 %) | roof class per table | per MIndBauRL | main aisle 2 m, 35/50 m | q_R/DIN 18230 alternative; racks > 7.5 m → Sonderbau |
| Garage (MVGarVO) | small ≤ 100 m² relaxed; medium/large: fb per ordinance | fb | per GarVO (noescape-stair relaxations, ramps) | exit counts per GarVO | **garage-specific ordinance governs — this skill's GK rows NOT sufficient; VERIFY GarVO edition** |
| Agricultural (fire/wall) | fh living / farm per GK | fb between | — | — | compartment ≤ 10 000 m³; dwelling-farm wall fb |

## 14. Typical failure patterns (from digested examples + rule traps)

1. **GK misassignment**: forgetting the per-NE 400 m² cap (GK4→GK5 trap), free-standing
   condition of GK1, or that underground structures are GK5. Also the MBO GK definitions
   were under revision (2024/2025) — stale scheme risk.
2. **Wood section without corner allowance/rounding**: d_ef = β_n·t + k0·7 must apply to
   every charred face, then round UP to standard sizes; using β0 (test) instead of
   β_n (design) underestimates depth; using panel β 0.9–1.0 for solid sawn overestimates.
3. **Steel assumed "thick = safe"**: bare sections often fail even R30 at high μ0;
   critical temperature falls as utilisation rises (0.7 → ~534 °C); encasement thickness
   must come from λ_P-certified product values — the two digests gave 0.20 vs 0.25 W/mK
   for "gypsum boards", proving product-specific data are mandatory.
4. **Chart/nomograph values read for wrong duration**: the "800" limit is the
   90-min/557 °C basis; R120 examples fail exactly by ignoring this.
5. **Concrete table misuse**: reading columns for the wrong μfi class or exposure side;
   ignoring b_min vs circular Ø values; missing ≥ 8-bar notes; flat-slab punching
   (shear) at fire not covered by the moment table.
6. **Fire wall terminated below roof** "because GK allows it" — moisture/thermal
   conflicts + hidden combustible bypass; recommend over-roof continuation (0.30/0.50).
7. **Combustible linings in stair/escape corridors** (lost-formwork timber, wood wool,
   old PVC) — classic real-fire accelerator (digested five-storey case: lost-formwork
   timber lining accelerated the fire; zone-model computed vs actual compared).
8. **Missing self-closers/smoke-tightness** on stair and corridor doors (RS vs dT vs T
   mix-up); light panels > 2.5 m in fire doors; door held open by wedges (electromagnets
   on BMA missing).
9. **Ventilated façade as chimney**: no Brandriegel per 50 cm cavity, no horizontal
   barrier at floor line, combustible ACP/EPS core on escape-facing wall; combustible
   balcony cladding above parapet in GK4/5.
10. **PV too close to party/fire wall** (0.5/1.25 m rules ignored); combustible roof
    build-up near boundary vs harte Bedachung distances (12/15/24/5 m).
11. **Openings into stair from > 200 m² storage/shop without T30-RS**; apartment doors
    without dT; shaft closures weaker than the slab pierced.
12. **Second escape assumed = window forever**: > 8 m sill kills the appliance route;
    brigade-equipment precondition never checked with the authority.
13. **Systems as silent assumptions**: sprinkler/BMA credited in the standard-building
    concept; standby power / function-maintained cabling (E30–E90) omitted for RWA,
    hydrant booster, firefighter lift.
14. **Citing obsolete frames**: Bauregellisten (abolished 2019 → MVV TB), DIN 4102-6
    withdrawn edition, B3 class, EnEV-era wording; DIN 18230 q-formula quoted from memory
    instead of the norm.
15. **Copying NRW numbers into another Bundesland** (LBO differs — §-numbers, some
    dimensions, small-building relaxations); or treating MIndBauRL 2019 anchors as
    current edition without check.
16. **Class-suffix confusion**: F vs T vs REI vs EI-ef direction (external fire E30(i→o));
    K260 only relevant for combustible-core hochfeuerhemmend routes.

## 15. Checklist

**Classification**
- [ ] Height = top occupied floor vs average ground; free-standing? NE count + areas → GK1–5
- [ ] > 13 m / > 22 m / > 30 m / area & occupancy Sonderbau triggers scanned (4.3)
- [ ] Land LBO edition + ordinance versions identified; GK-scheme currency checked
- [ ] Verification route + planner qualification (§66) assigned

**Compartmentation & boundary**
- [ ] Gebäudeabschlusswand / Brandwand triggers (boundary distance, 40 m, 10 000 m³ farm)
- [ ] Fire-wall build-up: F90-M, non-comb, aligned, 0.30/0.50 roof, corner 5 m, openings
- [ ] Roof: harte Bedachung? if soft → 12/15/24/5 m distances met
- [ ] Setbacks 0.4H ≥ 3 m (zone variants)
- [ ] Cladding/ façade: A1/B1 rules per GK, Brandriegel spacing, PV clearances
- [ ] Shafts & penetrations: closure class = component class; R/S/I/E classes named

**Structure**
- [ ] Required classes per 6.1–6.3 tabulated onto the element schedule
- [ ] Every element: proof route marked (DIN 4102-4 row / EC tabular / EC simplified /
      test/AbZ / general) — no "assumed OK"
- [ ] Timber: β_n source + d_ef + residual check incl. LTB at fire-time bracing
- [ ] Steel: μ0 from fire combination → θ_cr → heating check or 800-rule (only 90/557)
- [ ] Concrete: μfi class, exposure, a₁ ≥ table, bar count/slenderness conditions
- [ ] Joints/ bearing continuity survive single-element loss? (redundancy note)

**Escape & rescue**
- [ ] 2 routes per NE per storey; first via notwendige Treppe or ≤ 15 m direct exit
- [ ] Travel ≤ 35 m; dead-end ≤ 15 m; smoke sections ≤ 30 m with rsT
- [ ] Stair: width, handrails, enclosure class per GK, linings non-comb, floors ≥ B1
- [ ] Stair openings classified (200 m² rule; T30-RS/RS/dT); glazing ≤ 2.5 m
- [ ] Vent: 0.50 m²/floor openable + ≥ 1 m² top (GK5 both); operation points
- [ ] Rescue windows 0.9×1.2, sill ≤ 1.2 m; appliance ≤ 8 m precondition confirmed
- [ ] Safety lighting > 13 m; lifts not counted; shaft classes; FW-lift for Hochhaus
- [ ] Access road 3/3.5 m, clearance, turning, Aufstellfläche, hydrants ≤ 80 m

**Services interfaces**
- [ ] Löschwasser 1.5 bar/2 h + 48–192 l/min demand class fixed with water supplier
- [ ] Risers nass/trocken decided; Wandhydranten in required regimes (Garagen etc.)
- [ ] Sprinkler/BMA only where ordinance/agreed deviation; standby power + E30–E90 listed
- [ ] RWA concept: tenability 2.5 m/<300 °C, vent areas, supply air ≥ 1.5·A_AW, sections
- [ ] Fire load q_B (DIN 18230) or design fire (t²/EN 16730-validated model) documented
- [ ] Löschwasserrückhalt noted (ramps, dams, separators) where volume demands

## 16. Agent workflow

```
INPUTS  usage mix, plan + sections, heights, NE areas, plot/boundary, Land
STEP 1  Classify: GK + Sonderbau/Hochhaus (4.x); state the definition used + VERIFY flag
STEP 2  Element schedule: required classes (6.x) per wall/column/slab/door/shaft/roof
STEP 3  Escape graph: routes, stair(es), corridor lengths, openings, vents (5.x)
STEP 4  Compartment map: Brandwand lines (40 m / 10 000 m³ / boundary), roof class,
        distances/setbacks (7.x)
STEP 5  Material proofs: for each non-trivial element run the right route from 9.x
        (§12 patterns) — tag every number as tabulated/simplified/assumed
STEP 6  Services interfaces: list what the concept DEPENDS on (10.4/11.x); if the
        standard concept survives without systems, say so explicitly
STEP 7  Output: concept note = assumptions table, GK logic, class schedule, escape
        diagram checklist, open VERIFY list, and the disclaimer (1.x) — routed to the
        authorised verifier; never an approval claim
```

Escalation rule: if STEP 1 already trips Sonderbau, GK5, > 8 m appliance sill, or any
deviation, STOP tabular reasoning for those aspects and hand to a Brandschutzplaner —
the digested tables stop at the standard building.

---

## Appendix A — Uncertain items (carried VERIFY flags)

| Item | Status |
|---|---|
| LBO numbers throughout | NRW-anchored digest; all §/values VERIFY per Bundesland edition |
| MBO GK definitions 2024/2025 revision | scheme flagged possibly superseded |
| THR600s vs printed "THR500s" (A2/B/C) | corrected to THR600s per standard — VERIFY edition |
| ETK constants | Δθ = 345·log₁₀(8t+1) verified; older print "125t+1" was figure-guess |
| DIN 4102-4 catalogue rows §6.4 | representative values reconstructed — VERIFY exact rows |
| EC2 Tab 5.4 wall pairs, beam a-values | OCR-compressed cells — VERIFY |
| DIN 18230 q_B formula + tables | NOT in digests; definition-only — VERIFY norm |
| MIndBauRL Tab 1 compartment sizes (1800/3000 m²), SMA density, exit-length +15 m | single-example anchors — VERIFY |
| Steel protection λ_P 0.20 vs 0.25; 800-rule duration basis | product-specific — use certified data |
| Sicherheitstreppenraum overpressure figures (1.5/3) | garbled in digest — VERIFY |
| Garage/hotel/school ordinance specifics | not digested — outside this skill's guarantee |
| Rescue-window sloped-roof "tread ≤ 1 m from eave" variant | extension by agreement noted — VERIFY |
