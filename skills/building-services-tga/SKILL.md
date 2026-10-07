---
name: building-services-tga
description: >
  Technische Gebäudeausrüstung (TGA / building services) for residential and
  office buildings in German (DACH) practice, sized from DIN/DVGW/VDE rules.
  Heat demand heuristics (DIN EN 12831 climate factors, W/m³ and W/m² specific
  loads, 3-Liter/Haus benchmarks) → emitters (underfloor design: ≤100 W/m²,
  loops ≤100 m / 15–20 m², spiral layout, screed ≥45 mm, edge fields, manifolds,
  DIN EN 1264/DIN 18560; radiators: EN 442 exponent, DIN 4703 sizes, low-temp
  enlargement factors ×1.5/×2/×2.5) → heat generation (heat pump sizing with
  COP/SPF anchors, monovalent vs bivalent-alternative/parallel changeover
  −5…−7 °C, changeover-day table, borehole VDI 4640 W/m extraction, collector
  W/m² and field = 1.5–2.5× living area, groundwater m³/h per 10 kW; GEG/GModG
  new-build heating duties incl. solar-DHW and direct-electric gates; condensing
  boiler rules, MFeuVO boiler room sizes/ventilation, AMEV oil storage, TRGI
  gas, DIN 18160 chimneys); DHW (DVGW W551 legionella temperatures: growth
  30–45 °C, stop ≥50, kill minutes 60–65 / seconds ≥70; storage/outlet ≥60,
  never <50; 3-litre dead-leg rule, >400 l Großanlage logic, circulation ≤5 K,
  DIN 4708 sizing, solar fraction); ventilation (natural + DIN 1946-6 dwelling
  rates, windowless room flows, decentral WRG units 30–160 m³/h and central
  ZAB ≥80–90% heat recovery, air rates/CO2 setpoints 1000 ppm & ΔCO2
  550/800/1350, duct A=V̇/v, velocities 4–12 m/s, SFP classes, EN 1366-2 fire
  dampers, DIN 18017/18017 shafts); drainage (DIN 1986-100/EN 12056: slopes
  0.5%/1.0%, Q_ww=K√ΣDU, stack capacities, venting, traps, cleanouts, SML/PP/
  PE materials, Trennsystem, backflow level + Hebeanlage, rain r(5,5) C-values,
  Überflutungsnachweis); water supply (EN 806/DIN 1988 materials, pressures,
  filter, booster, air gap); electrical (DIN VDE 0100 TN-C-S grid forms, RCD
  30 mA, DIN 18015-2 dwelling circuits by area 3–7, DIN 18015-3 installation
  zones, bathroom zones/IP, load planning values, HAK/meters, PV kWh/kWp yields
  + storage, EV charging VDE 0100-722, lighting EN 12464-1 lux/UGR/Ra,
  lightning EN 62305 + SPD, emergency power E30); smoke extraction (RWA) and
  fire interfaces; lifts EN 81 (car sizes, pit/headroom, machine room);
  riser/shaft planning with sizing heuristics and riser stacking rules;
  spatial coordination with structure (chase rules DIN 1053 practice, no ducts
  through beams, ceiling void depths 30/40–60 cm, sleeves, fire stopping of
  penetrations, DIN 4102-4 shaft seals, pipe insulation GEG Anhang 8 driving
  the space budget); plant noise interfaces (DIN 4109/VDI 4100, 220 kg/m²,
  TA Lärm for heat pumps); maintenance access; GEG energy-certificate data
  model; FreeCAD modelling of shafts/risers/sleeves with boolean clash checks
  and IFC system export; one full single-family worked example (heat load →
  HP → underfloor → DHW → ventilation → drainage → PV → DIN 18015 circuits);
  clash checklist, failure patterns, verification checklist.
---

# Building Services Engineering (Technische Gebäudeausrüstung, TGA) — DACH Practice Skill

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

MEP on a German house or office is not one discipline — it is seven (heating, cooling, ventilation, DHW,
cold water, drainage, electrical) plus conveyances, and each has its own rulebook (DIN, DVGW, VDE, GEG).
They collide with each other, with the structure, and with the acoustic and fire-compartment concept.
This skill exists to:

1. give **sizing heuristics with numbers** good enough to design rooms, shafts and ceiling voids before
   any installer exists,
2. carry the **coordination methodology** — routing priority, zone reservation, clash classes, riser
   stacking, penetration scheduling — anchored on German rules instead of generic practice,
3. make the **interfaces explicit**: structure (chases, sleeves, shafts), physics (insulation, dew point
   on cooling surfaces), acoustics (DIN 4109), fire protection (fire dampers, shaft seals, escape
   routes), 4 and keep the FreeCAD model at the level of detail that actually prevents rework: shafts,
   risers, sleeves, maintenance volumes — not every bent pipe.

German terms stay in parentheses because coordination meetings, schedules (Leitungsverzeichnis) and
authorities communicate in German.

## 0. How to use this skill

Use it when the task involves ANY of:

- estimating **heat/cooling loads** before the DIN EN 12831 calculation exists, choosing
  **emitters** (underfloor vs radiator) and design temperatures,
- sizing or siting a **heat generator**: heat pump (source, bivalence, borehole length), condensing
  boiler, CHP, heat-network transfer; judging **GEG/GModG** new-build heating duties,
- **domestic hot water** design with hygiene numbers (DVGW W 551): temperatures, storage sizing, dead
  legs, circulation,
- **ventilation** strategy: natural vs room-by-room units (dezentrale Lüftungsgeräte) vs central
  supply/exhaust with heat recovery (Zu-/Abluftanlage mit WRG); air rates, CO2 criteria, duct sizes,
  fire dampers,
- **sanitary**: drainage slopes, stack sizing (DIN 1986-100), venting, backflow, cold-water
  materials/pressures, rainwater,
- **electrical**: dwelling circuit counts (DIN 18015), installation zones, RCDs, bathroom zones,
  HAK/meters, risers, PV and storage, EV charging, lighting levels, lightning and surge protection,
  emergency power,
- **shaft and riser planning**, technical room sizing, spatial coordination with structural design
  (penetrations, chases, voids), plant noise, maintenance access, energy-certificate data collection,
- modelling any of this in FreeCAD (shafts, risers, sleeves, clash checks, IFC).

**Siblings** (load them when the task crosses over — do not duplicate their scope):

| Skill | Overlap |
|---|---|
| `building-physics-thermal-moisture` | U-values feeding the heat load, Glaser/dew-point method used here for cooling surfaces, n50/blower door |
| `building-acoustics` | Full DIN 4109 / VDI 4100 proofs; here only the plant-noise interface |
| `fire-protection-building` | Compartments, escape routes, shaft fire classes behind the penetrations and fire dampers routed here |
| `structural-systems` / `concrete-detailing` | Whether a beam/slab may take an opening at all — this skill only reserves and schedules it |
| `masonry-construction` | Chase and wall-constructibility rules restated here in service terms |
| `stairs-vertical-circulation` / `openings-windows-doors` | Shaft walls and doors as built architecture |
| `construction-freecad-bim` | Model hierarchy, IFC export mechanics — §24 is the TGA-specific routing |
| `building-regulations-permits` | Submission, specialist attestations (Fachunternehmen), utility procedures |
| `cost-management-din276` | TGA is 35–50 % of build cost — heuristics here are dimensioning, not pricing |

## 1. Reality Check — Who Signs What

**This skill produces planning aids, sizing heuristics and coordination rules for concept/design-stage
studies and FreeCAD modelling. It is not a TGA design in the legal sense.**

- Electrical work requires an **entered installer (eingetragener Elektroinstallateur,
  Handwerksrolle)**; house connection, meter cabinet (HAK) and every grid-parallel PV
  additionally need the utility **TAB** + grid-operator approval. Nothing in §14 replaces the
  designer's load calculation and selective-tripping proof.
- Gas installations (TRGI scope) may only be executed by the network operator's recognised contractor
  (Insta-Gas register); the room/combustion-air and flue gas acceptance is done with the district
  chimney sweep (Schornsteinfeger), who is an authority, not a consultant.
- Water-supply installation work requires a **qualified plumbing business (Fachunternehmen
  nach Landeswasserrecht)** in most Länder; the supplier's W-Netz rules govern the connection.
  Legionella duties (TrinkwV, DVGW W 551) attach to the operator — a designer who ignores
  §10 creates liability for someone else.
- Energy certificates are issued only by persons with **Ausstellungsberechtigung (§ 88 GEG)**; the data
  model in §22 collects inputs, it does not certify.
- Fire-relevant services (smoke dampers, RWA, safety circuits, lift acceptance per EN 81 + state rules)
  are inspected by TÜV/DEKRA-type experts and the building authority. §15 is the interface, not the
  Nachweis — see `fire-protection-building`.
- Every number marked **⚠ VERIFY** is either edition-dependent, garbled in the underlying extraction, or
  Land-specific (LBO, water-byelaw, TAB): confirm against the current standard text / local rules before
  putting it on a drawing. Field rules of thumb here are for **room and shaft design**, not for the
  installer's device sizing.
- If the user is treating output as construction-ready — ordering a heat pump, quoting a shaft width to
  a builder, submitting this to the Netzbetreiber — **say so unprompted in that reply** and name what is
  missing (design load per DIN EN 12831 room-by-room, hydraulic balance, load group calculation per DIN
  VDE 0100-420, Fire-Konzept, TAB agreement).

## 2. Which Standard Supplies Which Number

Cite the standard that carries the number. The GEG/GModG layer (energy law) and the MBO/LBO layer
(building law) overhang everything below.

| Question | Numeric authority | Key anchors used here |
|---|---|---|
| Design room/outdoor temps, heat load method | **DIN EN 12831** (+ DIN/TS 12831 postal-code method for θ_e) | 20 °C living, 24 °C bath; θ_e −5…−22 °C; simplified W/m³ table §7.2 |
| New-build energy duty, envelope, heating duties | **GEG 2024 → GModG (from 2026) ⚠ VERIFY** | wall U ≤ 0.28; 65 % renewable heating rule path; solar DHW §35 logic; direct-electric gates |
| Pipe insulation in unheated zones | **GEG Anlagen 8 (λ = 0.035 rule)** | d_i ≤ 22 mm → 20 mm; ≤ 35 → 30; ≤ 100 → d_i; > 100 → 100 mm; half at crossings |
| Underfloor heating design | **DIN EN 1264 + DIN 18560-2 (screed)** | ≤ 100 W/m², loop ≤ 100 m, screed ≥ 45 mm above pipe, joints ≤ 8 m |
| Radiator rated output | **DIN EN 442** (exponent n ≈ 1.3), sizes **DIN 4703** | enlargement ×1.5/×2/×2.5 down the flow-temp ladder |
| Boiler room, plant rooms | **MFeuVO / FeuVO der Länder, VDI 2050** | > 50 kW own room, 8 m³ min, ≥ 2 m h, 150 cm² vents |
| Oil storage | **AMEV / AwSVO (WHG)** | tank unit ≤ 5 000 l, > 5 000 l separate room, bunding |
| Gas appliances & lines | **DVGW-TRGI + DIN EN 17023/IG 7** | A/B/C appliance types, 4 m³/kW, 150 cm² openings, no chase burial |
| Heat pump sources | **VDI 4640 (boreholes), Landes-Wasserrecht** | 60 W/m normal soil (1 800 h), 5 m spacing, permit |
| Legionella / DHW hygiene | **DVGW W 551/W 552, TrinkwV, DIN 4708 (sizing ⚠ VERIFY)** | 60 °C storage/outlet, ≥ 50 never below, 3-l and 400-l rules |
| Ventilation of dwellings | **DIN 1946-6, DIN 18017/-3** | reduction/nominal/intensified tiers; windowless flows |
| Non-residential air rates | **DIN EN 16798-1/-3 (categories I–IV)** | 4 l/s·person floor, CO2 Δ 550/800/1350 ppm |
| Duct fire safety | **EN 1366-2 (fire dampers), state LüRichtL** | compartment crossings, L30 corridor minimum |
| Drainage sizing & slopes | **DIN 1986-100 + DIN EN 12056-2** | Q_ww = K·√ΣDU, slopes 0.5/1.0 %, stack DN/vent DN table |
| Backwater | **DIN 1986-100, DIN EN 12056-4, DIN EN 13564** | Rückstau-Ebene ≈ kerb; lifts above gravity valves for fecal |
| Flooding proof of the site | **DIN 1986-100 + DWA-A 118/124** | > 800 m² sealed → retention r(5,2)→r(5,30); roofs r(5,5), check r(5,100) |
| Cold water | **DIN 1988 / DIN EN 806 series** | filter 50 µm, 40 mm air gap, ≤ 25 °C CW, 8-step pressure route |
| Fixture categories & sanitary space design | **VDI 6000-1/-3/-4 (replaces DIN 18022), ASR A4.1, MBO §48** | WC 1.5 / shower 2.5 / bath 4 m²; fixture counts and WW demand bands §13.6 |
| Socket/circuit planning of dwellings | **DIN 18015-1/-2/-3** | 3–7 socket-light circuits by area, zones ZW/ZS, riser 1–3 WE 63/80/100 A |
| Installations, protection | **DIN VDE 0100 series (−300, −410, −430, −559, −701, −722, −800)** | TN-C-S, RCD 30 mA, ≤ 16 A circuits, bathroom zones, EVSE RCD type |
| Lighting | **DIN EN 12464-1 (indoor), −2 (outdoor)** | 500 lx office UGR ≤ 19 Ra ≥ 80; MF 0.67–0.8 |
| Emergency lighting | **DIN EN 1838, DIN VDE 0108** | 1 lx escape, ≤ 15 s, 1 h, ≥ 15 lx high-risk |
| Lightning | **DIN EN 62305-1…-4, DIN 18014** | classes I–IV mesh 5/10/15/20 m, foundation electrode, SPD 1/2/3 |
| Lifts | **DIN EN 81-1/-2, -70 (access), -72 (fire), -73 (fire mode), DIN 8989 (sound)** | 630 kg 1.10×1.40 m; pit/headroom by speed; shaft wall masses |
| Plant noise in dwellings | **DIN 4109, VDI 4100, TA Lärm** | 30 dB(A) water install, 220 kg/m² enclosing walls, night 35 dB(A) |
| Service-entry room | **DIN 18012** | ≥ 2.00 m faces, working depth ≥ 1.20 m, ≥ 30 cm between trades |
| Shaft/penetration fire sealing | **DIN 4102-4/-18, MLAnG/LBO practice** | 20 cm mortar cast at every floor with combustible lines |

**Rule 2.1 — one question, one owner.** The installer sizes the device; this skill sizes the **space,
the route and the reservation**: shaft width, room, sleeve, void depth, insulation OD, maintenance
envelope. If a number here and the installer's calculation disagree, the reservation grows — never the
reverse.

---

# Part I — Coordination Methodology

## 3. Routing-First: Who Yields to Whom

When two services want the same volume, the lower priority number wins. This order is
German-practice-specific: gravity drainage is slope-locked, ducts cannot pass beams, and GEG-minimum
insulation makes heating pipe "small" pipes fat.

| Priority | System | Why it holds the lane |
|---|---|---|
| 1 | **Structure** (beams, braces, fire compartments, escape routes) | Immovable; penetrations are exceptions requiring design (§18) |
| 2 | **Gravity drainage** (Abwasser, DN50–DN150, rain stacks) | 0.5–1 % slope is non-negotiable (§12); a DN100 at 0.5 % eats 5 mm per metre forever |
| 3 | **Ventilation ducts** (RLT) | Rigid, bulky, cannot cross beams; tight bend radii; fire dampers fixed per compartment crossing |
| 4 | **Insulated heat/cool pipes** (HN/HT, chilled water) | GEG Anhang 8: DN 20 → 60 mm OD; DN 100 → ~300 mm OD (§20); runs on the slab as trunk lanes |
| 5 | **Pressure water** (Kalt-/Warmwasser, Zirkulation) | Slender (DN 15–25 + 20 mm insulation ≈ 40–50 mm OD), but routing locked to wet walls, W 551 limits dead legs (§10.2) |
| 6 | **Electrical** (trunking, conduits, cable trays) | Most flexible in routing — but **position-locked by DIN 18015-3 zones on walls** and by separation from data (§14.5) |
| 7 | **Telecom/data** | Follows, with ≥ duct separation from power |

**Rule 3.1 — drainage and ducts decide the ceiling.** If a duct must cross a beam line, the answer in
German practice is never "through the beam" but **drop the ceiling, run in the wall shaft, or move the
room** (§18.3). If a DN100 cannot keep 0.5 %, the slab gets a sunk zone or the layout moves — slope
beats elegance.

**Rule 3.2 — pressure services may go under the screed, drainage never.** In-screed pipes must be
jointless (pipe-in-pipe, press-fit) and insulated to the 6 mm reduced rule at transitions; a drainage
pipe under a floor build-up is a Grundleitung decision made in the basement, not in the living floor.

## 4. Zone Reservation: Give Every Service a Lane Before Routing

Routing only works if lanes exist first. Reserve these at spatial design (Entwurfsplanung), on the
plans, as modelled zones:

1. **Wall installation zones (DIN 18015-3)** on every habitable room plan:
   - horizontal band **ZW**: 30 cm below finished ceiling (lighting/switch drops) and 30 cm above
     finished floor (socket band); kitchen work band **ZW-m 90–120 cm**;
   - vertical bands **ZS**: 10–30 cm from the lock-side reveal of doors, both window jambs, room
     corners; switches at 1.05 m (barrier-free 85 cm);
   - rule: **only vertical chases in load-bearing masonry, no horizontal chases away from the slab
     band** (§18.1). Reserving the zones is what makes retrofit drilling findable.
2. **Ceiling voids declared as a depth budget:** ≥ 30 cm suspended ceiling for lights + cable trays;
   **40–60 cm where ventilation ducts run**; corridor voids are the trunk spine of the whole building —
   never sell them to storage. Minimum workspace clear height: **≥ 2.75 m** in rooms 50–100 m², ≥ 2.50 m
   for light/sitting work (ArbStättV) — the void comes out of that budget.
3. **Trunk lanes on the slab** (before the screed): parallel pipe rows ≤ 12 cm wide (20 cm where
   structurally backed), **bearing strips ≥ 20 cm** between rows, ≥ 50 cm from the wall (20 cm in
   corridors), crossings only where unavoidable; ducts and pipes in the same lane are modelled solids
   (§24).
4. **Shafts and risers** reserved in the structural grid from day one (§17). A bathroom group stacks on
   ONE wet wall with ONE shaft; every floor repeats the same grid dimensions from a single plumb
   reference.
5. **Technical room reservation:** Hausanschlussraum (DIN 18012), heating/ plant room, AHU room,
   meter/EDP floors — sized in §17.1/§17.2 with the benchmark that RLT-served administration needs ≈ **6
   m³/(h·m²) NFA of associated technical area ≈ 3–5 % of NFA** ⚠ VERIFY as rule of thumb.
6. **Maintenance envelopes modelled as transparent solids**: 90 cm in front of every meter, distributor,
   pump, filter section, manifold, fire damper actuator, cleanout; lifting space above AHU coils; access
   hatch 60×60 cm minimum over concealed devices.

## 5. Coordination Sequence and the Penetration Schedule

```
1. ARCHITECTURE frozen      → rooms, wet walls, FFL/CLL, ceiling heights,
                               escape route widths
2. STRUCTURE frozen          → grid, beam depths, slab spans, shaft openings,
                               wall types (11.5/17.5/24/36.5), fire concept
3. TGA ZONES declared        → shafts sized, ceiling void budgets, trunk lanes,
                               plant rooms (DIN 18012/VDI 2050), riser positions
4. TGA ROUTED inside zones   → priority order §3: drainage, ducts, insulated
                               pipes, water, electrical, telecom
5. PENETRATION SCHEDULE      → every sleeve/cascade/core, tagged, sized,
                               located, classified, fire-rated where compartment
6. STRUCTURE + FIRE review   → engineer + Brandschutzbeauftragter approve each
                               penetration BEFORE the casting call (Bemessung)
7. CLASH REVIEW on model     → hard/soft/4D/code (§5.3), incl. insulation ODs
8. SHOP/execution drawings   → sleeves cast-in or drilled exact, chases pre-
                               formed — retro-chasing is a defect, not a plan
9. PRE-SLAB / PRE-POUR CHECK → §25.3 checklist physically on site
10. AS-BUILT + commissioning → measurement logs (airflow, pressure tests,
                               drainage water test, electrical E-Check, W 551
                               documentation) feed the energy-data model (§22)
```

Never invert steps 2 and 4: routing MEP before beam depths and wall thicknesses are fixed produces
chases that DIN 1053 practice will not allow.

### 5.1 Penetration schedule format

Tag every opening `P-<floor>-<discipline>-<nn>` with disciplines **H** (Heizung), **K** (Kälte), **L**
(Lüftung), **S** (Sanitär), **E** (Elektro), **F** (Fernmeldetechnik), **A** (Abwasser). Example row:

| Tag | Floor | Host | Host ID | Service | Sleeve/zone | Position (grid, level) | Fire class | Status |
|---|---|---|---|---|---|---|---|---|
| P-OG-S-03 | OG | WU wall | W-210 | 2× insulated DN20 | 2×Ø100 c/c 150 | A3/B2 OKFF+2.60 | F90 cable sleeve set | **Pending** |
| P-DG-A-01 | DG | slab | S-104 | DN100 soil | Ø140 cast | 0.80 from B2 | — mortar filled | Approved |

**Nothing with Pending/Rejected may be cast, chassed or core-drilled.** The schedule is regenerated from
the model (§24), not kept in a parallel spreadsheet.

### 5.2 Core drilling vs cast-in

| | Pre-formed/cast sleeve | Later core drill (Kernbohrung) |
|---|---|---|
| Location | fixed in formwork, verified before pour | free — which is the problem |
| Structure | reinforcement routed by design, documented | rebar risk — scan + engineer approval mandatory |
| Fire seal | planned with the sleeve system | must be re-proven (DIN 4102-4 systems) |
| Cost | a few euro | rig + operator + approval trail; "special service" under VOB — money and time |

The early TGA–structure coordination meeting exists precisely to make the right column win: **everything
that can be pre-formed is pre-formed**; core drilling is the documented exception.

### 5.3 Clash classification (unchanged logic, German examples)

| Class | Definition | Example | Resolution |
|---|---|---|---|
| **Hard** | two solids overlap | DN100 into the 11.5 cm KS wall it was routed in | move to Vorwand 16–23 cm build-up (§17.3) |
| **Soft** | clearance/access/fire envelope violated | damper fits the duct but no 30 cm access hatch for the inspection door | enforce envelopes as modelled solids (§4.6) |
| **4D/sequence** | installable but not in that order | riser pipe crosses the shaft wall that is built first; lift delivered before the façade is closed | delivery/installation sequence review |
| **Code** | geometry fine, rule violated | 30 mm plastic waste pipe through F90 floor without fire cuff/encasement; duct unsealing a compartment | §18.4 fire-stopping; rework before cover |

## 6. Coordination Hot Zones (where 80 % of clashes live)

| Hot zone | Typical conflict | Pre-empt with |
|---|---|---|
| Bathroom wall | DN100 stack + vent + 2 insulated water pairs + Vorwand cistern in one wall | 24–27 cm build-up (§17.3); stack behind the WC offset sideways; light-gauge system with Montagerahmen |
| Kitchen wall | sink waste + hood duct + sockets zone + gas riser (where used) | service void or 24 cm wall; gas **never** in unventored chase (§8.2) |
| Corridor ceiling | duct trunk vs beams vs sprinkler vs lighting band | declare 40–60 cm void (§4.2); ducts along, never through, beams |
| Shaft every floor | alignment drift; seal forgotten at every floor | one grid-tied plan repeated per floor + DIN 4102-4 seal in the schedule |
| Stair enclosure | escape route: only non-combustible lines, no gas, no store rooms | treat as reserved structural volume, services only in adjoining shaft |
| Hausanschluss corner (DIN 18012) | water + electricity + telecom + gas + heat all want the wall | room sized in §17.1, ≥ 30 cm between trades, ≥ 50 cm telecom |
| Roof plane | HP exhaust/air intake, relief vents, rain drains, PV, lightning mesh | penetration + patch-load plan with the roof structure; vent terminals vs openings ≥ 2 m / per §12.4 |
| Plant room boundary | noise to adjacent dwellings (§19), fire door, ventilation louvers | never adjacent to/above protected rooms without acoustic design |
| Lift shaft | pit vs drainage, rails vs walls, DIN 8989 masses, door landing zones | §16.2 before the core is drawn |


---

# Part II — Heat: Demand, Generation, Emitters

## 7. Heat Demand Heuristics (DIN EN 12831 at planning speed)

### 7.1 Normal design temperatures

Interior (Norm-Innentemperatur): living/sleeping, office, meeting, classroom, shop, hotel, main stairs
**20 °C**; bathroom/shower/undressed areas **24 °C**; WC 20 °C; back-up rooms, corridors **15 °C**;
heavy-work halls 12–17 °C ⚠ VERIFY (occupation-class dependent). Heating design outdoor θ_e by region:
Hamburg −12, Berlin −14, München −16, Oberstdorf/Oberwiesenthal −20 °C (use the DIN/TS 12831 postal-code
method for real projects).

### 7.2 Simplified specific heat load (planning grade)

Φ_HL ≈ q_V · V_e · f_climate, with q_V from the envelope-shape class A/V_e:

| A/V_e | q_V (W/m³, base climate) | per m² @ 2.75 m | per m² @ 3.25 m |
|---|---|---|---|
| ≤ 0.2 | 9.1 | 27 | 34.7 |
| 0.3 | 10.0 | 27.5 | 44 ⚠ VERIFY |
| 0.4 | 10.9 | 30 | 41.5 |
| 0.5 | 11.8 | 32.6 | 45 |
| 0.6 | 12.7 | 35 | 48.5 |
| 0.7 | 13.6 | 37.5 | 51.9 |
| 0.8 | 14.5 | 40 | 55.4 |
| 0.9 | 15.5 | 42.6 | 58.8 |
| 1.0 | 16.4 | 45.1 | 62.4 |
| ≥ 1.1 | 17.3 | 47.5 | 65.8 |

Climate factor f: θ_e −10 → 1.00; −12 → 1.07; −14 → 1.13; −16 → 1.20; −18 → 1.26; −20 → 1.33.
(interpolate).

Sanity benchmarks: new efficient dwelling **15–55 W/m²**; "3-Liter-Haus" (≤ 30 kWh/m²a) **25–40 W/m²**
with U_opaque 0.18–0.22, windows < 1.2; Passivhaus ≈ **10 W/m²** (then air-based heat distribution
becomes discussable); unrenovated stock up to 150–200 W/m²-era demand (up to 200 kWh/m²a). Ventilation
shortcut for additions: **0.34 Wh/(m³·K)** → Φ_vent = V̇ · 0.34 · (θ_i − θ_e). Minimum whole-building
air change for tight buildings: 0.5 h⁻¹ — do NOT sum per-room worst-case infiltration; whole-building
value only. Reheat/setback allowance can reach 137 W/m² in EN 12831 — agree explicitly with the client
whether setback is designed for.

### 7.3 Worked heat-load estimate

Two-storey dwelling, living 140 m², clear h 2.5 m → V_e ≈ 350 m³, A_e ≈ 280 m² → A/V ≈ 0.8 → q_V 14.5
W/m³ → 5.08 kW × Berlin 1.13 = **≈ 5.7 kW (≈ 41 W/m²)** — credible for a modern airtight build;
cross-check against the 15–55 W/m² band before believing it.

### 7.4 Cooling quick-check

Internal loads set the game: persons (sensible+latent: 115–120 W light work at 26–20 °C, up to 270 W
heavy), equipment (office workstation ~158 W class, multifunction printer up to ~1 078 W 1-h max per VDI
3804), lighting connected 6–15 W/m² but actual average 0–4 W/m² with LED. Rough extractable-with-air
range 20–80 W/m² (mixing ≤ 60; source-air 25–35 — deeper cooling must go to radiant surfaces, §9.4).
Solar: external shading beats internal — g-value with double solar-control glazing 0.60 falls to
**0.13–0.20 with light external louvers** vs 0.45–0.55 internal; rule-of-thumb against overheating:
2.5–3× heat-storing surface per m² of window, heavy construction + external shading. Real cooling loads
need an hourly simulation — the numbers here are for plant-room and duct reservation only.

## 8. Heat Generation

### 8.1 GEG/GModG duties for new-build heating (⚠ VERIFY edition)

- Reference-building method: primary-energy total + envelope minimum; above-ground external wall **U ≤
  0.28 W/(m²K)** (rooms ≥ 19 °C); airtightness mandatory layer + blower door (n50 per DIN 4108-6/GEG ⚠
  VERIFY; historically ≤ 1.5 / 3.0 residential).
- **65 % renewable rule for new heating** in the path of the municipal heat-planning act
  (Wärmeplanungsgesetz, in force 2024): fulfilment via heat pump, district/bio heat, solar+biomass
  hybrid, or binding step schedule where a network is planned; biogas "Biotreppe" 10 % (2019) → 15
  (2025) → 30 (2030) → 60 (2040); 2026 relaxation in debate ⚠ VERIFY against in-force text.
- **Solar thermal for DHW** in new residential (former § 35 GEG logic) unless the duty is met otherwise
  (HP/district heat); collector + storage data feed §22.
- **Direct electric heating** only where envelope beats the reference ≥ 30 % (≥ 45 % when replacing
  hydronic) + certifier sign-off; replacement-of-like and owner-occupied EFH/ZFH exceptions; infrared
  60–80 % radiant; mats < 2 mm, ~200 W/m².
- Primary factors fp (§22): fossil 1.1 · wood/pellets 0.2 · district heat fossil-CHP ≥ 70 % ≈ 0.7
  (FW-Kappung floor 0.3, check certificate validity) · grid electricity 1.8 (GEG) → 1.5 (GModG ⚠ VERIFY)
  — this flips HP-vs-gas rankings · ambient/self-generated 0; CO2 price 55–60 €/t era raises fossil
  boiler running cost.

### 8.2 Condensing boilers, fuels, plant rooms, chimneys

- Standard (non-condensing) boilers are dead in new build. Dew points gas 45–57 / oil 45–55 / solid
  20–30 °C → condensing needs a moisture-insensitive, overpressure-tight flue (plastic ≤ 120/160 °C,
  glass, stainless, ceramic; forced-flue = height irrelevant) and a condensate drain — **neutralise > 25
  kW gas** unless enough grey water dilutes (≥ 8 dwellings/80 employees per 200 kW; > 200 kW always,
  DWA-A 251); ≈ 1.25 l gas / 0.85 l oil condensate per 10 kWh. Flue losses 1.BImSchV ≤ 11/10/9 %
  (4–25/25–50/> 50 kW); standing losses 1–2 %; full-load hours EFH 1 500–2 100, office 1 500–1 900 h/a;
  heating oil ≈ 10 kWh/l, H-gas 10.5–13.1 kWh/m³.
- **Boiler room (MFeuVO/FeuVO):** ≤ 35 kW room-air-dependent in any room with outside door/window
  + ≥ 4 m³/kW (or air path); **> 50 kW dedicated Heizraum** — ≥ 8 m³, height ≥ 2 m (practice 2.30–2.50),
    no other use, no opening to dwelling/ stair except self-closing tight fire doors, escape door in
    escape direction, upper+lower vents ≥ 150 cm² each, combustion air ≥ 150 cm² + 2 cm²/kW (> 50 kW); >
    100 kW exclusively technical; solid fuel never above ground floor (VDI 2050); shortcut ≈ 0.9 m³ room
    volume per kW, floor ≥ 2×3 m; roof plant room OK with oil-tight trays (10 cm upstand), floating
    screed/resilient mounts + silencers, headroom 2.5–3.5 m, ≥ 2 exits from 350 kW.
- **Oil storage (AMEV):** volume ≈ 1× annual use (≤ 0.1 MW) → 0.15× (> 1 MW); factory PE/PA/GFK units ≤
  5 000 l, clearances 40/25/≥ 5/25 cm (wall/floor/ ceiling), 1 000-l unit 0.72×1.10×1.50 m; **> 5 000 l
  → separate storage room** (WHG) with bunded hatch; buried double-wall + buoyancy proof × 1.3 + expert
  check before start and every 5 y (or permanent leak alarm); fill pipe ≤ 30 m from truck road, overfill
  sensor, vent; ≤ 100 l diesel in living space; oil-proof floor + oil-stop drains.
- **Gas (TRGI):** registered contractor (Insta-Gas) from service valve to terminal; buried cover 0.6–1.0
  m + sand bed + warning strip; **exposed or in vented ducts / own vented I90 shaft only — never buried
  in construction**; forbidden in stairwells (except ≤ 2-dwelling), escape corridors, with flammables;
  appliance A = no flue (cookers ≤ 11 kW, room > 20 m³ ⚠ VERIFY + openable window), B =
  room-air-dependent (never negative-pressure room without interlock; ≥ 4 m³/kW or 2 openings ≥ 150
  cm²), C = sealed (LAS ducts: 6–10 units, ≤ 2/floor); pressure test preliminary 1.0 bar, final 110
  mbar/10 min **before any concealment**.
- **Chimney (DIN 18160/EN 13384):** one-shell pre-1950 solid-only; three-shell standard;
  moisture-insensitive universal for NT/condensing; condensing in shaft → 2–3 cm ventilated gap; EFH
  reference 36.5×36.5 outer, liner 10.5² gas / 12² oil ⚠ VERIFY; mouth ≥ 40 cm over ridge/eaves and + 1
  m over any surface within 1.5 m; combustible distances 40/20 cm; sweep access + 50×30 cm
  non-combustible plate at solid-fuel doors; **chimneys never penetrate beams/slabs — plan the shaft.**

### 8.3 Heat pumps — sizing, bivalence, sources

Anchors: reference COP ≈ 3.3 (air) / 4.2 (brine); SPF/JAZ incl. auxiliaries — groundwater 3.8–4.6, brine
3.6–4.2, air 2.7–3.2. Flow temperature is the annual lever: FBH 35/28 or oversized radiators (§9.1/§9.2)
buy the JAZ; every −1 K lift ≈ +2.5 % JAZ ⚠ VERIFY.

Generator output: Φ_SU = Φ_HL + Φ_DHW + Φ_AS, the heat load plus an allowance for hot water
(sized after DIN 4708-1 to -3) plus other systems such as air heating coils (S.6). A model that
sizes on Φ_HL alone must say that the hot water allowance is missing.

| Mode | Changeover θ | HP size | Boiler size | HP heat share |
|---|---|---|---|---|
| **Monovalent** | none (to ≈ −16 °C without back-up) | 100 % | — | 100 % — realistic only with ground/water source; air mono needs > 3× exchanger, uneconomic |
| **Bivalent-alternative** | ≈ 50 % of design load; changeover days/a: Köln 58 · Stuttgart 73 · Bremen 82 · München 107 | ≈ 60 % annual heat | full Φ_HL | ~60 % (SPF 3 ⇒ ~40 % renewable-share framing) |
| **Bivalent-parallel** | +3…−1 °C | 50–70 % | 30–50 % | +10–20 % annual heat vs alternative |

- **Borehole (VDI 4640):** 40–100 m, spacing ≥ 5 m (≤ 50 m) / ≥ 6 m; extraction per 1 800/2 400 h: poor
  25/20 · **normal 60/50** · high-conductivity 84/70 W/m (sand-gravel water-bearing 65–80, wet clay
  35–50, limestone 55–70, granite 65–85) ⚠ VERIFY site; L = Φ_qu/ε → 5.7 kW ÷ 60 W/m ≈ 95 m → 2× 50 m;
  water authority permit + grouting proof; Thermal Response Test for large fields.
- **Surface collector:** 1.20–1.50 m deep, 20–24 mm PE @ 50–100 cm (1–2 m pipe/ m²), extraction 10–40
  W/m² by soil; **monovalent field = 1.5–2.5× living area** (bivalent ½); bifilar, vented headers, brine
  to −20 °C.
- **Groundwater:** 9–14 °C stable, best SPF; 2 wells (injection ≥ 15 m downstream if flow unknown, pump
  well 5–6 m deeper), ≈ **1.5 m³/h per 10 kW** monovalent; 35-h test pump; the reluctant permit usually
  kills it — no sewer discharge.
- **Air:** ΔT 2–5 K → **≈ 4 000 m³/h per 10 kW**; noise rules the siting (§19.3); concrete pad on gravel
  + resilient mounts; frost-melt latent heat is a gain; top-discharge/hood quietest.
- Rooms & electrics: compression HP **≤ 50 kW (ref. group 1) in any room incl. dwellings/cellar**; > 100
  kW exclusive room + self-closing doors; ≤ 50 kW mostly permit/notification-free ⚠ VERIFY Land;
  condensate + safety-valve drain with trap; separate HP meter under interruptible tariff (§14.2).
- Hydraulics: anti-cycling buffer for non-inverter units, weather curve + room feedback, **hydraulic
balance before commissioning**; per-dwelling heat meters are a billing duty → reserve (§9.3).

### 8.4 Other generators (recognition level)

- **District heat:** new low-temp nets ≤ 140 (max 180) °C, 5–17 bar; 2-pipe keeps ≥ 70 °C for year-round
  DHW; **indirect transfer** (plate exchangers, no primary fittings in dwellings) in the lockable DIN
  18012 room (permanent ventilation, ≤ 30 °C, no bedroom adjacency); compact cabinets ≤ 100 kW; the
  utility owns most of it — agree early, re-tender connection kW after envelope work.
- **CHP (BHKW):** nano 1–2.5 kW_el (EFH) · micro 2.5–20 · mini 20–50 · > 50 klein; size on the heat
  load-duration curve — base unit ≈ 25 % of peak covers ~50 % of annual heat; heat coverage MFH 10–20 %,
  hotel 20–30 %, care/pool 30–40 %, office 10 (40 with cooling); ≈ 4 m² per 5.5 kW_el; noise/exhaust
  like a boiler room. Fuel cells: η_el 40–60 %, 70/55 °C, service intervals 1–2 y.
- **Solar thermal (DHW):** flat plate 1.5–2 m²/person (vacuum −30 % area), tilt 20–45° S ±50–60°; yield
  300–500 kWh/(m²a); storage 80–140 l/person (or 50–70 l/m² collector); ~50 % annual DHW coverage (80
  summer / 10 winter); 20–30 kg/m² roof load = structural case (§18.6).
- **Solid fuel:** < 15 kW untreated natural wood only (1.BImSchV); gasification boiler → **buffer 25
  l/kW legal, makers want 50–70**; beech 2 325 kWh/rm; pellets > 10 m³ / wood > 15 000 kg → separate
  storage room; delivery access or suction lines planned to the truck.

## 9. Emitters and Heat Distribution

### 9.1 Temperature ladders and the NT/condensing logic

Classic 90/70 is obsolete. NT-radiator bases 70/55 (max 75/35–40); condensing wants the return below the
flue dew point → **floor heating 35/28–40/30 is the ideal partner**; design ranges per circuit: static
emitters VL 40–70/RL 30–50, floor 35–55/30–45 (ΔT 5–10 K), ceiling ~30/26, DHW charge 65–85, air heaters
60–80/40–60 ⚠ VERIFY ranges. Radiator enlargement vs 90/70 reference: **×1.5 at 70/55, ×2.0 at 60/50,
×2.5 at 55/45** — in low-load new build the extra area usually fits under windows; in retrofit it drives
the replacement decision (plant-retrofit path: lower flow target first, enlarge emitters, hydraulic
balance, adaptive bypasses on 1-pipe rings).

### 9.2 Radiators

DIN EN 442 rating: output ∝ ΔT^n, n ≈ 1.3 (platt/convector); sizes DIN 4703: heights
300/400/500/600/700/900…, depths 64/101/139/177/215 mm (10/20/21/30/ 33 class types). Placement per VDI
6030-1: under windows (catch down-draught, width ≈ window width), radiant asymmetry < 3.5–5 K, back
insulation U < 1.0 (shield adds 16–30 mm). Fan convectors ≈ 30 % size but need power
+ filters. 2-pipe is the default (each emitter controlled); 1-pipe only with design effort (3-way rings,
  adaptive bypasses). Vertical risers in external walls are dead (insulation + chases) — run
  distribution in ceiling void/floor, top connections, cross-side when L/H ≥ 4/1.

### 9.3 Underfloor heating (Fußbodenheizung, FBH) — the design rules with numbers

- Capacity: **≤ 100 W/m² floor output** (living surface max 29 °C; offices/ workrooms higher band ⚠
  VERIFY 35), cooling on floor **≤ 40 W/m²** (dew point §20.2). Self-regulating: each +1 K of room air
  above the operative baseline costs ≈ 17 % output ⚠ VERIFY anchor — hence "floor systems can't chase
  setback spikes": pair with modest radiator/convector on cold surfaces where fast response is needed.
- Loops: **≤ 100 m pipe per loop, covering 15–20 m²**; spacing field 15 cm / edge zones 10 cm near
  glazing ⚠ VERIFY (practice values; > 30 cm spacing needs conduction plates);
  layout **reverse-meander/spiral (Bifilar)** for even surface temp, meander for simple rooms; edge zone
  denser but its real effect is limited — don't over-pitch it.
- Build-up: insulation per DIN EN 1264 (practical 30–40 mm, more over cold ground/perimeter slab incl.
  side strip), pipes 16×2 PE-X/PE-RT/alu-composite, **wet screed ≥ 45 mm above pipe crown (DIN
  18560-2)**; dry systems (gypsum/wood, low build-up, higher resistance) for renovation; movement joints
  ≤ 8 m spacing, fields ≤ 40 m², ratio ≤ 2:1, 5–10 mm elastic joint material, edge strip 8–10 mm ⚠
  VERIFY; **no pipes under the bathtub** (trap access), joints only at accessible manifolds; pressure
  test logged before AND during screed.
- Manifold (Verteiler): niche ~1 m wide, 12 cm deep, 80 cm high per dwelling (mid-flat or cellar), flow
  meters per loop, actuators for room stats; pipe bundles crossing other dwellings' areas must be
  insulated (metering integrity). **Floor slab as distribution level (Tichelmann/spaghetti) is the
  per-dwelling-metering-friendly choice** — reserve the niche early.
- Check on the schematic: mean specific need Φ/area vs 100 W/m² minus furniture-free fraction; worst
  room individually (bath 24 °C on an external wall often forces extra loops or a towel radiator sized
  as a real emitter).

### 9.4 Ceiling systems and core activation (Bauteilaktivierung)

Hanging panels/metal cassettes/gypsum registers: heating ≤ 40 W/m², cooling ≤ 100 W/m² ceiling capacity;
capillary mats low build-up, drop 15–40 cm by system. Core activation: PE-Xa/HDPE 17–26 mm @ 150–300 mm
in slab neutral zone, 16/19 °C water, slow — baseload only, peaks need fast emitters on top; same pipes
heat and cool (3/4-pipe or seasonal switch) — **dew-point control mandatory, see §20.2**. No individual
room control — plan zones by room use.

### 9.5 Distribution pipes and the space they really take

Steel/Cu/PE-X — ratings below; the coordination fact is the **insulated outside diameter**: DN20 → OD 60
mm, DN 40 → ~120 mm, DN 100 → ~300 mm (§20.1). Pipe-in-pipe absorbs expansion (5 m run, ΔT 40 K → ~40 mm
growth); loops/ compensators beyond ~20 m straight; sleeves at slab crossings with the fire rules of
§18.4; pressure test 1.3× design; expansion fixings ≥ 50 cm from direction changes; **never mortar-set
hot pipes in a chase without padding** (creak + crack, §19.2). Weather-compensated curve + room
feedback; per-room thermostatics standard; heat metering duty per dwelling (§8.3).

## 10. Domestic Hot Water (Trinkwarmwasser) and Hygiene

### 10.1 Demand and systems

Demand at 60–65 °C: dwellings **30–60 l/(person·d)**, hotels/nursing 60–70, restaurants 15–45/seat,
sports 30–50; per fitting: bath 160 l @ 40, shower 5 min ≈ 40 l @ 37, basin 5–20 @ 35, sink 10–20 @ 50.
Flat-size quick table: 1-room 50–95 l/d @60 … 6-room 400–600 l/d @60. Storage sizing calc: DIN 4708 ⚠
VERIFY — practical EFH/HP: **300 l tank**; small units 5–15 l open / 80–120 l closed (6 kW); HP tanks
200–400 l with 0.3–2 kW element + 1.5–2 kW aux, Arbeitszahl 1.4–2.7, periodic 60 °C heat-up, condensate
drain planned.

System choice logic: Einzelversorgung (per-tap instant — good retrofit), Gruppen (cluster heater near
frequent small draws: kitchen!), central (**short pipes mandatory**). Losses = standing loss
+ first-draw cold waste; instantaneous: 12 kW basin+sink, 18–21 kW tub; ≈ l/min ≈ half the kW at 40 °C;
  electronic flow-through 5–27 kW is the only multi-point-stable type; > 4.6 kW needs a 3-phase DIN
  18015 circuit (35 A class) ⚠ VERIFY. Energy anchor: 100 l heated 10→60 °C = 5.6 kWh.

### 10.2 Legionella — the DVGW W 551 temperature ladder

Growth 30–45 °C with stagnation (days–weeks); multiplication stops ≥ 50 °C; dies within **minutes at
60–65 °C, seconds ≥ 70 °C**. Transmission is aerosol (shower, spa) — hence the numbers below are about
what the tap delivers, not what the tank holds. Scalding pain threshold ~40 °C, ≥ 50 °C dangerous —
thermostats lock at 38–40.

| Installation class | Trigger | Temperature duty |
|---|---|---|
| **Großanlage** | storage **> 400 l** and/or pipe volume **> 3 l** between generator and any outlet (circulation excluded) | outlet water **always ≥ 60 °C**; pre-heat stages ≥ 60 °C once daily; risk analysis + regular testing (operator duty, > 100 KBE/100 ml action line per TrinkwV) |
| **Small installation** (any EFH; or ≤ 400 l AND every line ≤ 3 l) | the normal single-family case | generator set **60 °C, never below 50 °C**; operator informed in writing |
| Circulation/trace heating | wherever installed | return **≤ 5 K below** generator outlet (so the loop never sits in the growth band); may sleep 8 h/24 h only if hygiene is proven |

**Design consequences (the coordination-relevant ones):**

1. **3-litre rule = dead-leg budget.** Every branch heater→outlet holding > 3 l water puts you in
   Großanlage discipline: keep DHW branches to single fixtures short (16 mm pipe ≈ 0.2 l/m → ~15 m
   theoretical, in practice keep < 5–8 m and never tee two distant outlets off one stub), or make them
   circulation branches, or take the 60-always strategy.
2. Cold water must stay ≤ **25 °C at the outlet** (TrinkwV) — insulate CW in shafts/ceilings (13 mm rule
   §20.1), keep CW away from hot lines and from sunlit shafts; CW warming is the other half of the
   legionella story.
3. Stratification-free tanks, serial tanks beat one giant tank, clean-out manhole per DIN 4753-1
   (sediment = hotspot); thermosiphon protection (check valve/thermo siphon group) when the tank sits
   above coils.
4. Single-family low-risk ≠ no-risk: commissioning flush, leak test with filtered water, full fill
   before handover (partial fill = three-phase corrosion line), documentation handed to the owner.

### 10.3 Sizing the generator for DHW

Priority charging (DHW first) with summer mode; small generators → longer recharge so a slightly larger
burner/store than the pure heating load demands; combo gas boilers ≤ 24 kW need 18–30 kW DHW branch
(modulating); central flow-through = fresh and hygienic but burner-heavy — the practical German default
in HP houses stays the 300–500 l heat-pump tank with nightly/ daily 60 °C legio load, PV-over-production
charging beats timers (§14.8).

## 11. Ventilation (Raumlufttechnik, RLT)

### 11.1 Natural and window-based

Drivers: wind (DIN 4710 means 2.8–4 m/s; profile exponent 1/7 open → 2/5 dense city; boundary layer
250→520 m) + stack effect; cross ("über Eck") acceptable; **ventilation via stairs/corridors is not
accepted by building law**. Tight windows (DIN 12207 class 2/3) force the DIN 1946-6 question.
Workplaces (ASR A3.6): one-sided depth ≤ 2.5 h (≤ 10 m if h > 4 m), cross ≤ 5 h (≤ 20 m), opening area ≈
0.105 m²/person continuous ⚠ VERIFY (table extraction garbled). CO2 criteria: **< 1000 ppm fine ·
1000–2000 act · > 2000 more measures**; Pettenkofer limit 0.1 Vol%; MAK 0.5 Vol%; RH comfort 30–65 % (≈
50 % at 21–22 °C).

### 11.2 Dwellings (DIN 1946-6) — tiers and systems

Air-change need: living/bed **0.5–1.0 h⁻¹**, internal bath/WC **4–5 h⁻¹**, kitchen shock to 25 ⚠ VERIFY
(conversion per room volume; DIN 1946-6 tables govern). Tiers: **reduction (Feuchteschutz, 24 h) /
nominal / intensified**; humidity-demand control allowed. Windowless rooms per **DIN 18017-3**: kitchen
basic 40–60 m³/h (intensive ≈ 200), bath and WC room 40 m³/h running continuously or 60 m³/h with
demand control (S.5; the 20–30 m³/h printed here before was too low). Systems: **Abluft** (extract +
inlet vents; cheap; extract-air HP makes it a heat source), **ZAB central with plate WRG ≥ 80 %** (90 %
= Passivhaus class; EFH balance example ≈ 125 m³/h), **decentral alternating units** (regenerative core,
~40 s cycles; example unit 990×322×762 mm ≈ 120 m³/h ⚠ VERIFY vendor) = the retrofit standard. Transfer
paths (door undercuts ≥ 8–15 mm ⚠ VERIFY, grilles) belong in the door plan. > 2 storeys: extract shafts
to DIN 18017 — wall fire class L30 (3–5 storeys) → L90 high-rise (8 cm board / 10 cm autoclaved / 11.5
cm brick ⚠ VERIFY), floor seal ≥ 10 cm mortar or intumescent, kitchen riser to roof for hoods
(recirculation keeps moisture — preferred in tight houses). **Never pull against a type-B gas
appliance** (interlock).

### 11.3 When mechanical is mandatory (non-residential)

Noise/odour/dust outside; > 1 h occupancy at < 5 m³ air/person; depth > 8.4 m one-sided (h < 3.4 m) or >
2.5 h under-ventilated; windowless; defined climates (museum, server, OP); high internal loads (§7.4).
Hand architecture early: plant space, ODA/ERA positions, duct routes + voids (§4.2), shafts, terminals,
cooling pairing, shading interplay.

### 11.4 Air rates and CO2 (DIN EN 16798-1/-3)

Comfort categories I–IV; minimum **4 l/s·person** always; person flows by comfort category (2.5 % PPD
tiers ≈ 20/40/60 m³/(h·person) across EN 16798-1 levels 1/2/3 — ⚠ VERIFY the edition's table, extraction
was garbled) — **sober shortcut: dimension by CO2**: emission 20 l/h·person (rest; > 30 heavy work),
targets above outdoor CO2 (≈ 400–450 ppm): **Δ550 ppm ≈ 10 l/s·P, Δ800 ≈ 7, Δ1350 ≈ 4**;
building-emission component 0.15–0.3 l/s·m² by material class; office VDI 3804 cat II ≈ 1 P/10 m² → 0.7
l/s·m² (≈ 2.5 m³/(h·m²)) person + building share. Preselection air changes (rules of thumb only): bath
4–6 · school 4–5 · office 3–6 · dining 5–10 · lecture 8–10 · pool 3–4 · shop 4–8 · theatre 15–20 h⁻¹ ⚠
VERIFY. Targets: summer ≤ 28 °C, heated season from 17 °C (EN 16798-3); head–ankle gradient cat A ≤ 2 K.

### 11.5 Plant and unit sizing

AHU section order: mixing → filter (ISO Coarse/ePM10; Δp fresh **40–80 Pa**) → heating coil → cooling
coil + condensate tray (§20.2) → humidifier (rare) → bypass → **WRG** → after-heater → radial fans.
Recovery classes EN 13055 **H1 ≥ 74 % … H5 < 60 %** (rotary 75–90 incl. latent ~70 % hygroscopic;
cross-plate 50–70; counterflow/enthalpy special 60–85; switch-around 60–90; run-around 30–60). **Specify
SFP class (EN 16798) ≤ 500 W/(m³/s) + VFD** or fan power swamps the recovery gain; casing class V1–V7,
leakage + thermal-bridge classes named. Decentral pairs (§11.2), underfloor units in raised floors,
rooftop Kältesatz for whole zones, air curtains at high-traffic gates.

### 11.6 Duct design numbers

- Section **A = V̇ / v**; velocities low-pressure 4–12 m/s (mains 6–8, branches 3–5), high-pressure
  12–25; residential PLW PE systems ≤ 2.5 m/s for acoustics (Ø 75 room loops, Ø 125–160 mains ⚠ VERIFY
  vendor Δp diagrams).
- Friction band galvanised 0.05–0.2 Pa/m ⚠ VERIFY per diameter (diagrams govern); flat/oval ≈ **double
  area vs round** for same Δp; guide vanes in bends; flex ≤ Ø 400, length ≤ 20×Ø, never across fire
  compartments.
- Insulation 30–80 mm non-combustible; **cold/supply ducts vapour-tight** or the skin sweats (§20.2);
  extract uninsulated unless it feeds the WRG.
- Hygiene: VDI 6022 (planning→operation, cleaning; inspection doors near bends, crawlable 30/10–60/50
  cm), VDI 3803 maintenance; commission = airflow + noise measurement protocol per room; silencers
  against inter-room "phone effect".

### 11.7 Fire protection of ducts (non-negotiable set)

- Every compartment wall/floor crossing: **fire damper DIN EN 1366-2** (melt release; smoke release +
  hold-open magnet from the safety circuit on RWA/ smoke-control ducts), or duct as L30–L90 casing, or
  shaft enclosure. Necessary-corridor ducts ≥ L30.
- Common fresh/exhaust risers: smoke dampers before branching into plant.
- AHU room = own fire compartment: boundaries **F90**, contents non-combustible, doors T30, no direct
  opening into occupied space, exit ≤ 40 m in escape direction ⚠ VERIFY Land rules.
- Steel thermal growth 1.1–1.95 mm/m per 100 K → expansion compensators ~5 m or dampers bind.
  Safety-circuit power to RWA/pressurisation: E30 class (§14.9).

---

# Part III — Water, Air, Electricity, Conveyance, Interfaces

## 12. Drainage (Abwassertechnik — DIN 1986-100 / DIN EN 12056)

### 12.1 Systems and terminology

**Trennsystem** (separate foul + rain) vs **Mischsystem** (combined) — the local byelaw (Ortssatzung)
decides; separate relieves the plant and keeps storm backflow out of foul lines. **Foul and rain always
keep separate stacks inside the building even in a combined system** (combine only outside, to ease
later conversion). Components: Anschlussleitung (EAL single / SAL group branch), Fallleitung (stack,
vented over roof), Grundleitung (under-floor drain), Sammelleitung (basement collection main),
Lüftungsleitung (vent extension), Reinigungsöffnung (cleanout), Kontrollschacht (inspection chamber),
Anschlusskanal (to public sewer). Germany admits EN 12056 design systems I (full branches, h/d 0.5) and
IV (separate stacks).

### 12.2 Design flows — Q_ww = K · √ΣDU

Design units DU per fixture (l/s): basin/bidet 0.5 · shower 0.6 (with plug 0.8) · urinal 0.8 cistern /
0.5 valve · bath 0.8 · sink + dishwasher combined 0.8 · washer ≤ 6 kg 0.8, ≤ 12 kg 1.5 · **WC 6 l → 2.0
(9 l → 2.5; low-flow 4.0/4.5 l → 1.8)** · floor drain DN50 0.8 / DN70 1.5 / DN100 2.0. K = **0.5 dwellings/offices**, 0.7 hospitals/schools/hotels/restaurants, 1.0 public
WCs, 1.2 labs; Q_tot = Q_ww + continuous + pump inflows. Branch DN: basin DN40 · shower/bath
≤ 2 m DN50 (longer DN70) · sink/washer DN50 · WC DN80–100 · cellar drain DN100.

Stack capacity (vented, standard branches): DN70 1.5 · DN80 2.0 · DN90 2.7 · **DN100 4.0** · DN125 5.8 ·
DN150 9.5 · DN200 16 l/s (inner-radius branches ~+30 %, secondary vents more ⚠ VERIFY — DIN 1986-100
tables govern). With 4–6 l WCs a dwelling stack ≥ DN80, DN100 is the house default. Min vent DN: DN50 to
stacks ≤ 100, DN70 (125), DN80 (150), DN100 (200).

### 12.3 Slopes — the non-negotiable set

| Line | Min slope | Note |
|---|---|---|
| Vented branch (EAL/SAL) | **0.5 %** | the workhorse value |
| **Unvented** branch | **1.0 %**, run ≤ 4 m, ≤ 3×90° | 1 WC + basin only, ≤ 4 m drop, straight to under-drain |
| Grundleitung / Sammelleitung inside | 0.5 % | fill ≤ 0.5 (0.7 after pump inflow) |
| Site drain outside the building | ≥ DN 100, slope ≥ 1/DN (DN 100: 1.0 %) | S.1; a ground drain that leaves the house is drawn at 1.0 % throughout |
| DN90 main with 4.5–6 l WCs | 1.5 % | low-flush needs velocity |
| Outdoor rain to ≥ DN250 | 1/d_i | ≤ DN200: 0.5 % at fill 0.7 |
| Velocity window | ~0.7–2.5 m/s | > 2.5 scours, < self-cleansing silts |

Check the **invert budget** before fixing FFL: connection invert − outlet invert ≥ run × slope + chamber
drops; no back-fall, no sags — uniform slope, water-test before closing the floor.

### 12.4 Venting, stack feet, traps, cleanouts

- Stack vented **through the roof**, its mouth at least 15 cm above the roof surface, measured
  vertically, more where snow lies (S.1); termination ≥ 1 m above openings to occupied rooms or ≥ 2 m
  horizontally; vent bends from ~6 storeys at 45°; vent offsets sloped (drip!). Loop/re-ventilation
  (Umlüftung/ Sekundärlüftung) for long or heavily loaded stacks; hotels may merge vents.
- **Stack base:** ≥ 4 storeys or ≥ 10 m drop → spur piece ≥ 25 cm between the bend and the horizontal,
  stack kept 2 m free of connections above the bend; offsets below the top fixture with connected
  appliances → **bypass (Umgehungsleitung) mandatory**, always > 8 storeys / 22 m; fixtures go in the
  bypass, never the main stack.
- **Trap seal (Sperrwasser) ≥ 50 mm** standard (older editions: 60 foul / 100 rain ⚠ VERIFY); evaporation ≈
  1 mm/day → infrequently used drains dry out: trap primers or regular use. Outdoor rain: no trap
  (frost) unless the discharge is < 2 m from occupied openings → trap frost-free at stack foot.
- Cleanout **at the foot of every stack 30–40 cm above floor** (bucket height; better: keep cleanouts
  off occupied zones, on the collection main), at direction changes; outdoor Kontrollschächte minimum
  clear 0.75×1.20 m rect / 0.9×0.9 square / Ø 1.0 round; foul and rain chambers separated (illegal
  cross-connection risk).
- Deflection bends 15/30/45° only in horizontals — **no 90° tees in drainage runs**, two 45° with a
  straight between.

### 12.5 Materials (foul)

| Material | Traits | Coordination note |
|---|---|---|
| PP / PE-HD / ABS-ASA / PVC-C plastics | light, socket push-in **fully then pull 10 mm** for thermal, clamp below socket | B1 (PP, PVC-C) vs B2 (ABS/ASA grey+yellow stripe, PE-HD black+yellow) — fire rules §18.4 |
| Mineral-filled silent pipes | thick wall, quiet (airborne) | chase depth = OD + fixings; heavier |
| **Cast iron SML** | sleeveless, quiet, non-comb, expansion ≈ concrete → embeddable in slabs | A1 — the escape-route and fire-grade choice |
| Steel EN 1123 / fibre cement | small sockets / aggressive | rare in dwellings |

Condensate from boilers is acidic: plastics/stoneware or neutralise before cast iron/fibre cement (DIN
1986-4/DWA-A 251). DN100 outer dimensions: plastics ~11.0–12.5 cm pipe/socket; SML 11.0–13.5 — **size
the chase/shaft to the socket OD, not the nominal DN.**

### 12.6 Rainwater (Dachflächenentwässerung)

**Q_R = r(D,T) · A · C / 10 000 [l/s]**, D = 5 min; design rainfall r(5,5) ⚠ VERIFY your locality
(examples Aachen 266 · Berlin 331 · München 356 · Stuttgart 405 · Rosenheim 440 l/(s·ha)); C: roof
1.0, extensive green ≤ 5° 0.3, paved 0.7–0.9, lawn 0.2–0.3. Gutters ≥ 1 mm/m (3–5 better),
expansion every 12–15 m; flat-roof drains at every low point ≤ 20 m spacing, count n = Q/Q_drain,
stack ≥ drain DN; **leaf guards halve capacity**; internal rain stacks vapour-tight insulated in
top storey; balcony drain + ≥ 4 cm overflow in closed parapet; exposed downpipe feet in cast
iron/steel.

### 12.7 Backflow (Rückstau) — basement defence

Rückstau-Ebene (RSE) ≈ street kerb level. **Every fixture below RSE needs protection.** Options:
automatic backflow preventer **DIN EN 13564 — not for fecal unless approved and a WC exists above RSE**
(battery reserve, maintenance); or **lifting plant (Hebeanlage) discharging through a loop pipe above
RSE = the safe default for fecal below grade**: 2 pumps preferred, alarm, min 60 cm working space in the
pit, tank ≥ 6 l…20 l ⚠ VERIFY (6 l only with approved backflow preventer), room MFH 2–3 m²
(hotels/schools to 8), discharge velocity ≥ 0.7 m/s ⚠ VERIFY, DN80 min without macerator; grinders
banned. Rain inlets below RSE → lift for r(5,100) or sealed + emergency routing.

### 12.8 Site flooding proof, separators, off-sewer sanitation

- **Überflutungsnachweis** (DIN 1986-100/DWA-A 118): sites > 800 m² sealed must retain ΔV between r(5,2)
  and ≥ r(5,30) events on their own ground (roof/ surface retention, throttled outflow drained ≤ 24 h);
  > 70 % roofed → r(5,100) with emergency drainage. Say this early — it eats garden area.
- Petrol/oil separator EN 858 (garages only where fuelling/servicing happens); grease separator DIN EN
  1825/DVFG 4040-100 from gastronomy kitchens, outside, 1–2×/month emptying access.
- Unsewered plots: **DIN 4261 small treatment plant (Kleinkläranlage), multi-chamber ≥ 2 m³,
  watertightness test, EGW sizing** (1 bed hospitality = 1 EGW … office 3 employees = 1), periodic
  inspection duty — percolation-area tests and groundwater rules per local authority; this is
  public-health scope, say so explicitly when a user plans around it.

## 13. Water Supply (Trinkwasser — DIN EN 806 / DIN 1988)

### 13.1 Quality and treatment

Public supply + TrinkwV (2016/2023 tightening ⚠ VERIFY). Hardness 1 °dH = 0.179 mmol/l; scaling > 60 °C (corrosion doubles per 10 K → service 50–60 °C
max); softening sensible ≥ 16 °dH, needed > 21 °dH when > 60 °C; **50 µm filter after the meter**
(DIN 1988-2); pH < 6.5 attacks Cu/Zn; lead pipes (pre-1973) must be replaced; phosphate
dosing only ≤ 17 °dH/≤ 75 °C and flow-proportional; magnetic "conditioning" has no DVGW endorsement.

### 13.2 Materials

Cu (soldered, inner tinning against pitting; **never upstream of galvanised steel** — copper-induced
pitting), stainless (press-fit, di 15–54 mm, ≈ plastic all-in cost), galvanised steel (legacy; malleable
fittings, no bends), PE-X/ PE-X-AL multilayer, **pipe-in-pipe plastic** (bend radius ≥ 15 cm in slab,
storey distributors, replaceable), composite. Selection drivers: wall chase vs drywall, acoustic group,
temperature duty.

### 13.3 Connection, metering, distribution

Utility does the connection — apply early; shortest perpendicular route, never over built
areas, burial 1.0–1.8 m, sleeve gas/watertight-flexible. Meter per dwelling; shaft (≤ DN40)
1.2×1.0 m plan, h ≥ 1.8 m, entry ≥ 70 cm. After the meter: two valves + drain + check valve → **distribution
bank (Verteilerschrank)** with separate off-takes per: dwellings, heating, laundry, garden/frost, AC,
kitchen, fire, flush-valve mains. Risers branch ≥ 1.10 m above floor with per-storey isolation; vent
valves (type E) at riser tops with DN20 drip line to a trap; **40 mm free air gap at every outlet**
backflow category per DIN EN 1717 ⚠ VERIFY detail.

### 13.4 Pressure management

Aim ≥ 1.5 bar flowing at the worst outlet; required flow pressures: 0.5 bar taps, 1.0 bar ≥ 9/18 kW
instantaneous, 1.2 bar flush valves. Static > 4.5–5 bar → PRV (> 6 bar safety valves trip); high-rise =
pressure zones + booster (ventilated, soundproofed, drained room, standby pump + alarm); ≥ 3 bar static
at topmost fire hydrant; sizing per EN 806-3/4 or the 8-step DIN 1988 route (p_min − geostatic − meter
~0.5 bar − filter ~0.2 bar − appliance minima − floor losses − fitting margin; friction by diagram) ⚠ VERIFY.

### 13.5 Routing physics

Hot and cold lines keep distance even insulated (CW ≤ 25 °C duty §10.2); fixings ≥ 50 cm from direction
changes, sliding clamps, bellows/loop compensators; factory-jacketed Cu absorbs ~3 m between bends; **no
mortar-set of hot pipes in chases without padding**; frost protection: drain or heat trace
(self-regulating PTC tape, cut-to-length); frost-proof pillar taps with in-wall valve + auto-drain;
tightness test + filtered-water flush + full fill before handover.

### 13.6 Fixture inventory categories (VDI 6000-1)

Before any pipe is sized, list every wet fitting by room category — **kitchen (Küche), bathroom
(Bad), WC, ancillary** — because the same inventory feeds three separate calculations: cold/hot
water design flow, DHW heat demand (§10.3), and drainage design units DU (§12.2 — those DU values are
**wastewater only**, not to be mixed with water-supply values). Building law sets the minimum
inventory (MBO §48): every dwelling gets bath **or** shower **plus** WC; separate WC room from 5
habitable rooms or 3 bedrooms; second basin from 3 occupants; kitchen counts as a stay room
(Aufenthaltsraum). Min room areas (VDI 6000-1): WC 1.5 m², shower room 2.5 m², tub bath 4 m².

| Fixture (German) | Warm-water per draw, l @ °C | Heat-demand anchor (Wärmeanforderung) | Notes |
|---|---|---|---|
| Basin (Waschbecken) | 5–20 @ 35 | 12 kW instantaneous group w/ sink | flow limiters 5–12 l/min |
| Bidet | 10–20 @ 40 | — | same group |
| Sink (Spüle) + dishwasher | 10–20 @ 50 | 12 kW; cluster heater belongs **near kitchen** | DW own 16 A circuit; drain above trap |
| Shower (Dusche) | ≈ 40 @ 37 in 5 min | 18–21 kW | thermostat lock 38–40; scald ≥ 50 |
| Bath (Badewanne) | 160 @ 40 (120–180 band; +5 K draw-off margin) | 18–21 kW | anchor: 17.5 kW gas throughflow fills 10→40 °C in ~20 min |
| WC | flush 6 or 9 l settable (eco 3; DIN 1986-100 accepts 6/9; low-flow 4.0/4.5) | — | DN80–100 branch |
| Urinal (Urinal) | flush 0.5–1.0 l | — | offices ≥ ⅓ of men's fixtures as WC, rest urinals |

**Per-fitting classic design values (Grundwerte, l/s; heat demand in kW per the old DIN 1988
table — today EN 806-3 qx-method) are not carried in this skill — [VERIFY] against the current
standard before any sizing calculation.** The digested anchors above (instantaneous ratings,
l/draw, kW ≈ 2 × l/min at 40 °C) are planning-grade only.

**Categories → building load:**
- **DHW daily demand** = occupants × use-band @ 60–65 °C: dwellings **30–60 l/(person·d)**,
  hotels/nursing **60–70**, restaurants **15–45/seat**, sports **30–50**; quick flat check 1-room
  50–95 … 6-room 400–600 l/d.
- **Peak heat demand** ≈ sum of simultaneous draws at the kW ≈ 2 × l/min (ΔT to 40 °C) rule, then
  check storage/recharge per DIN 4708 [VERIFY] (§10.3).
- **Energy anchor**: 100 l heated 10→60 °C = **5.6 kWh**.
- **Typical compositions:** dwelling = kitchen + bath (+ separated WC by size); hotel room =
  shower + basin + WC (60–70 l/bed·d); office = basins + WC/urinal banded per employee count
  (ASR A4.1 mandatory, VDI 6000-3 recommended: 1 WC per 5 → 4+ from 51, +1 per further 30 women /
  90 men); assembly VDI 6000-4 (> 200 persons): ≈ 6 women's WC at 100 seats … 18 at 1000.

**Interaction with the legionella ladder (§10.2):** the inventory is what you count against the
hygiene limits — every fitting branch adds its volume to the **3-l rule** (heater→outlet) and
every stored litre to the **400-l Großanlage trigger**. A long hotel corridor run of identical
bathrooms usually crosses both → 60-always regime + circulation (return ≤ 5 K below generator,
may sleep 8 h/24 h); the dwelling below both → small-installation regime, no circulation needed.
So: fix the fixture list **before** choosing Einzelversorgung / Gruppen / central (§10.1).

**Worked mini-example (4-person MFH flat):** inventory = kitchen sink+DW, bath 160 l, shower,
2 basins, WC. DHW: 4 × 45 = **180 l/d @ 60 °C** → ≈ 10 kWh/d (5.6 kWh/100 l). Peak draw = bath
8 l/min @ 40 °C ≈ **16 kW** → covered by an 18–21 kW instantaneous or a 300 l tank (§10.1); all
branches < 3 l → small-installation regime (§10.2). Drainage side, from §12.2: ΣDU = 0.8 + 0.6 +
2×0.5 + 0.8 + 2.0 = 5.2 → Q_ww = 0.5·√5.2 = **1.1 l/s** → DN50–70 vented branches, DN100 stack ✓.

## 14. Electrical Installations (DIN VDE 0100, DIN 18015)

### 14.1 Supply and grid forms

Voltages: NS 230/400 V; MS 10/20 kV via customer transformer > ~100 kW ⚠ VERIFY utility threshold; own
substation for offices/schools/markets (§14.9). **Grid forms (DIN VDE 0100-300/-410):** TN-S (separate
N+PE — standard inside buildings); **TN-C-S** (PEN to the house, split to N+PE in the meter cabinet —
normal German residential; **never extend the combined PEN beyond the cut-out** — "klassische Nullung"
is a lethal legacy, remove on renovation); TT (own electrode + RCD mandatory); IT (isolated + insulation
monitor, special). Colours: L brown/black/grey, **N light-blue, PE green/yellow**; PEN = green/yellow +
blue end rings; pre-1970 legacy (red = PE!) is a renovation danger flag.

### 14.2 House connection, meters, risers

Registered installer applies; utility fixes the route; overhead mast (4–5 m guyed standpipe, ≥ 1 m to
trees/antennae, ≥ 36 mm spare duct) or underground (cover 60–80 cm + yellow warning tape 30 cm above;
sleeve light-falling outward, flexible watertight seal). **HAK = utility boundary** — never in garages,
laundry, boiler rooms ≥ 50 kW, fire-risk rooms. Main fuse D0/Neozed 63 A typical for an EFH. Metering:
per dwelling + separate communal meters > 2 flats (DIN 18015-1); niche centre 95 cm, width 16/23/30 cm
per 1/2/3 meters, depth 13 cm (DIN 18013); riser sized for **1 WE ≤ 63 A, 2 WE ≤ 80 A, 3 WE ≤ 100 A**;
central meter banks for ~8+ flats, decentral floor meters ≤ ~3 storeys; iMSys/smart-gateway rollout per
MsbG/EnWG staged — reserve positions for division and night-storage tariffs. HP with interruptible
tariff: separate meter (TRE/ton-frequency receiver spot).

### 14.3 Dwelling planning — DIN 18015-2 in numbers

| Dwelling floor | Socket+lighting circuits |
|---|---|
| ≤ 50 m² | 3 |
| 50–75 | 4 |
| 75–100 | 5 |
| 100–125 | 6 |
| > 125 | **7** |

plus one extra socket/connection if the kitchen includes dining, **plus own circuits for every special
load**: stove (2-pole 400 V, "3×230 V" legacy wording), micro, washer, dryer, ironing station, DHW unit,
fridge-freezer (own circuit **not behind the shared RCD** — a tripped RCD must not blackout the
freezer), HP, lift, water lift/booster, garage/exterior. Socket counts: kitchen **≥ 5 double sockets**,
telecom/data + each radio/TV socket 1 connection + 1 power per room, 2 lighting outlets; bath 2 sockets
(one may combine with the mirror light) + fan connection. Every lighting+socket circuit ≤ 16 A (3.68
kVA); fixed device connection box ≥ 3.7 kW; most hobs 400 V (induction 3.7–11 kW class; e-stove ~11 kW /
14.5 kW 3~).

### 14.4 Installation zones, wiring methods, bathrooms

**Zones (DIN 18015-3):** horizontal mid-bands ZW 30 cm below ceiling and 30 cm above FFL; kitchen work
band ZW-m 90–120 cm; vertical bands ZS 10–30 cm from lock-side door reveals, window reveals, corners;
switches 1.05 m (barrier-free 85 cm, ≥ 50 cm from corner). Zones are the reason a drill finds the cable
— respect them architecturally (door/window positions shift the verticals). Methods: conduit system
(PA/PP flexible, steel/panzer in concrete; single-core H07V-U pulled) = replaceable, the reference
standard; direct-buried sheathed NYM (not in compacted concrete unprotected, not surface in dwellings
except retrofit); NYIF Stegleitung plaster channels (no wet rooms/ wood). **Bathroom sections (DIN VDE
0100-701):** zone 0 inside tub/tray (IPX7); zone 1 above tub to 2.25 m / around a fixed shower outlet —
radius 1.20 m without enclosure ⚠ VERIFY (0.6 m band readings vary by edition); zone 2 = 0.6 m beyond,
to 2.25 m; **switches/sockets forbidden in 0–2** (SELV ≤ 25 V AC or shaver transformers in 2/3 only);
washer may stand in 2 if IPX4; equipotential bonding of tub, metal pipes, heating circuits — **bonding
coordination before enclosure** (plastic pipes are no longer earths); IP defaults: living IP20, wet-room
fittings IP24, exterior sockets IP44+ on RCD, unheated cellar IP21-X ⚠ VERIFY per room dampness class.

### 14.5 Protection, load, separation

**RCD 30 mA is the only device giving direct-contact protection** — mandatory (new build) on all
bathroom circuits and exterior sockets; types AC from 16 A single-phase / 25 A three-phase; use A as the
floor, F for electronics, **B where DC residual can ride through (EVSE, PV-inverter-side loads)**; RCD
never replaces the LS breaker (it does not see overload) — every RCD group has downstream LS; **one RCD
per group, not the whole house** (nuisance trip + total blackout); 300/500 mA fire-protection RCD
concept optional-⚠ VERIFY. Load estimate at planning: EFH ≈ 8–12 kW connected without HP, +6–12 kW with
HP/EV ⚠ VERIFY — real answer from the load-group calculation (Anschlussleistung + Gleichmäßigkeit/
simultaneous factors; utility asks the table, give ranges with the meter/BSV sizes of §14.2).
Separations: power vs copper data never in one pipe, shared trunk only ≥ 10 mm air gap or metal
partition ⚠ VERIFY; power above water where possible, ≥ 150 mm parallel; **gas ≥ 300 mm and no shared
shaft with power**; crossings at 90°; ≥ 30 % spare conduits
+ draw wire in every riser (retro-chasing RCC/masonry is the failure to prevent).

### 14.6 Lighting (DIN EN 12464-1)

Maintenance-level lux (Em): office reading/writing **500 lx, UGR ≤ 19, Ra ≥ 80**; reception 300;
classrooms 500 (board vertical 500 ⚠ VERIFY); corridors/traffic 100; hospital wards 300; colour-critical
work 750–1 500 Ra ≥ 90; bathroom base ≈ 200 lx + shadow-free mirror-side lights. Vertical wall ≥ 50 lx
(rooms with communication ≥ 75 ⚠ VERIFY); no harsh step down in surrounding zones. Planned new level E_n
= E_m / MF, reference MF ≈ 0.67 clean offices/museums, 0.8 industrial ⚠ VERIFY assumption logged.
**Lumen method:** n = E_m·A/(Φ_L· η_LB·η_R)·(1/MF) with room index k = A/((a+b)·h_m, h above the working
plane (desk 0.75 m)). Efficacy: LED module ≤ 180 lm/W class; light colour rule: low lux warm (< 3300 K),
high lux cool; screens: no luminaires opposite daylight, ≤ 200 cd/m² above 50° (BAP/darklight); daylight
dimming (TEB) + presence control with manual override; DALI/KNX addressing planned with the distributor
grid.

### 14.7 Lightning and overvoltage (DIN EN 62305, DIN 18014)

Average stroke 20 kA (to 300 kA); lightning protection required by the Land/LBO risk assessment (EN
62305-2, economic option) — typical duty: tall/ large-volume buildings, assembly, heritage, explosive
trades; **plain EFH usually not required — but foundation earth + SPD always good practice**. Classes
I–IV: mesh 5/10/15/20 m, rolling sphere 20/30/45/60 m, effectiveness 98/95/90/80 %, down-conductor
spacing 10/10/15/20 m ⚠ VERIFY pairing; > 30 m height: horizontal capture band every ≤ 20 m; natural
components (concrete reinforcement bonded, **never prestressed**) may serve. **Foundation ring electrode
DIN 18014**: Ø10 mm rod / 30×3.5 flat, ≥ 5 cm clear of soffit/sides, grid bays ≤ 20×20 m, expansion
joints bridged outward, **connection tabs and test joints planned at construction — retrofit is
impossible**. Internal: equipotential bar ties LPS + all services + PE; **SPD type 1 (boltage) at the
entry** (before the meter only with utility consent), **type 2 at every sub-distribution**, type 3 at
sensitive IT; cascaded coordination; PV strings: SPD DC at the combiner/inverter (⚠ VERIFY manufacturer
+ type-1/2 by array exposure).

### 14.8 PV, storage, EV charging

- Yields: horizontal global radiation DE 900–1 200 kWh/(m²a); **30° south: N-DE 1 130 / mid 1 200 / S-DE
  1 300 kWh/m²a; × performance ratio 0.8 → 904/960/1 040 kWh/kWp·a**; winter share ≈ 25 %; area per kWp:
  mono-Si 4–5 m² (20–22 % cells), poly 5–7, thin-film 10–20; tilt 10–50°/azimuth ±45° costs ≤ 2–5 %;
  module 70 °C, −0.4 %/K — ventilate, cables 70 °C UV-rated; partial shade kills the string — keep
  chimneys/vents/rails ≥ 60 % shadow distance, optimisers for split roofs; flat-roof ballast frames =
  structural load case (snow-clearance height kept) ⚠ VERIFY uplift per Eurocode wind. Storage: Li-ion η
  80–90 %, residential **5–10 kWh** sizing ≈ 10 % of annual consumption ⚠ VERIFY heuristic; grid
  parallel per VDE-AR-N 4100/4110 (utility form + protection); feed-in at HAK ≤ 30 kWp typical
  single-family ⚠ VERIFY; fire: DC-arc → rapid-shutdown/optimisers per latest guidance ⚠ VERIFY.
- **EV charging (DIN VDE 0100-722, DIN VDE-AR-E 2623-2-2):** charging point (Wallbox) 11 kW 3~16 A is
  the dwelling default (22 kW where loads allow); **own final circuit, own protection**; RCD at the
  charging point: **type A + 6 mA DC residual detection (RCD-A EV variant) or type B — plain household
  type AC is not sufficient**; PV-surplus charging via the wallbox controller + load management
  (Lastmanagement) when several points share a connection; **GEG § 13 logic: new residential buildings
  with parking — each space needs a cable duct/conduit for later charging ⚠ VERIFY current text**;
  garage slab: buried line cover per TAB, not under the slab where drillable. Load math: +11 kW on a 63
  A TN-C-S house connection is manageable (diversity) — 22 kW needs the §14.5 load-group proof.

### 14.9 Emergency power, safety services, substations

Safety services (fire alarm BMA, voice alarm, emergency lighting, escape/ fire-service lifts, fire-water
booster, RWA, smoke dampers) run on the **Ersatznetz** (diesel genset auto-start ≈ 15 s, UPS for
no-break) and their wiring is **functional-maintained E30/E60/E90**: fire-resistant trunking or ≥
defined mineral screed cover on the raw slab (§18.5). Genset room Seip shortcut: 20 kVA ≈ 5.0×4.0 m …
650–1 500 kVA ≈ 10.5×5.0 m; ≥ 24 h fuel, day-tank bottom ≥ 50 cm above the injection pump, oil-tight
floor + 10 cm bunded threshold, ≥ +5 °C, exhaust stack or 1 m³/50 kVA expansion chamber, floating
foundations + silencers, ≥ 2 exits from 350 kW. Battery rooms: gangways ≥ 60 cm, ≥ 2.0 m clear, floor
drain + tap, threshold ≥ 10 cm. Emergency lighting (DIN EN 1838/VDE 0108): **1 lx maintained on escape
routes, 1 h, switch-in ≤ 15 s; anti-panic areas 0.5 lx; high-risk task ≥ 10 % and ≥ 15 lx ≤ 0.5 s**;
exit signs continuously lit. Substation rooms (oil): not above ground floor nor > 4 m below grade; 100 %
oil bund + 20 cm gravel smother layer; room sizes VDE-AR-N 4110: 250–630 kVA ≈ 3–4×2.5–3×2.5–3 m; dry
cast-resin units may sit on upper floors (weight + hum + forced air planned with structure); service
passage 0.7–1.2 m at switchgear.

## 15. RWA and Fire-Service Interfaces (recognition level — sibling skill owns it)

- **RWA (Rauch- und Wärmeabzug):** triggers per MBO/LBO + MIndBauRL (large units, sales/assembly,
  corridors, atria, necessary stairs get smoke ventilation — stair values: 0.5 m² vent + 1 m² smoke
  exhaust per section are the fire-skill's numbers, verify there). Products per **DIN EN 12101 series**
  (natural NRA windows/rooftap, drives, automatic opening), planning **DIN 18232 ⚠ VERIFY**, control
  chain: RWM smoke detectors + ZRN manual call points → RWA central → drives, **BSK smoke dampers
  release, doors close, lift EN 81-73 fire mode, booster start**; power = safety circuit (§14.9); annual
  maintenance/inspection duty (DIN 14676 for natural smoke vents on stairs ⚠ VERIFY). Reserve: opening
  geometry in façade/roof early — a 1 m² flap needs a structural lintel and a 60 cm clear swing.
- **Löschwasser:** Wandhydrant C (DN50, 15–30 m reel) / B (DN80); niche sizes wet 70×74×80 cm / dry
  32×42×14.5 cm (DIN 14461); risers **trocken** (dry, fire brigade fills via Siamese at the access,
  hydrant ≤ 80 m) or nass/nass-trocken; ≥ 3 bar at the topmost outlet (§13.4). Sprinkler (VdS CEA 4001
  classes LH/OH…): head coverage 9–21 m², activation ≈ 30 K over max normal (68 °C typical), tank loads
  up to 200 kN/m² on upper floors = structure case; deluge for bunkers/stages; water mist
  retrofit-friendly. Inert-gas (EN 15004) for server/museum rooms: flood-tight enclosure + O2-deficiency
  safety interlocks.
- **BMA interfaces:** detector positions vs ceilings, panel room (gatekeeper/security), 72 h standby,
  line supervision, release to ventilation fire mode, lift recall, door holders.

## 16. Lifts (EN 81 family)

### 16.1 Duty and sizes

Lift obligation per state building law: generally **> 13 m height of the floor of the highest occupied
storey above the access level** → "in sufficient number" ⚠ VERIFY Land variants (Berlin ≥ 4 storeys,
NRW/RP > 5); high-rise (hochhaus) ≥ 2; **lifts are never escape routes**. Accessible residential min
**630 kg, car 1.10×1.40 m, clear door ≥ 0.90 m** (EN 81-70; ideal 1.10 m two-way); stretcher/furniture
1 000 kg 1.10×2.10 m (≈ 13 persons, covers ~260 users at 20/users); beyond 20 persons +0.115 m²/person.
Waiting area depth ≥ 1.5× car depth (min 1.50×1.50 DIN 18040, 2.30 m stretcher case), never facing a
down-stair.

### 16.2 Shaft geometry and machine rooms

Pit depth by speed: hydraulic ≤ 0.4 m/s ≈ 1.40 m · 1.0 m/s ≈ 1.60 m · 1.6 ≈ 1.75–2.00 · 2.5 m/s to
4.40–5.50 m (anchors ⚠ VERIFY vendor program); headroom 3.6–3.8 m ≤ 1 m/s, MRL 3.70–4.40 m (drive in
shaft wall — reserve pockets); ≥ 3 lifts: shared wall + 20 cm per extra run; base slab ≥ 500 kg/m² ⚠;
under-pit: 1.5–2.5 m ladder, > 2.5 m door ≥ 1.4 m + counterweight arrestor. Machine room: clear ≥ 2.0
m, +5…+40 °C, no through-route, access ≥ 70 cm, **lifting hook ≈ 1 t**; drive on springs over ≥ 25 cm
slab; hydraulic pump room 3–8 m² oil-tight, 10 cm bund, ≤ 150 trips/day, ≤ 10–25 m from shaft.

### 16.3 Acoustics and fire

DIN 8989/VDI 4100: ≤ 30 dB(A) night in adjoining dwellings — single-leaf shaft walls need ~490–740 kg/m²
by situation or decoupled double-leaf (3 cm joint + 380/580 kg/m²); **the structural planner owns the
mass, the lift vendor does not fix site noise**; light-gauge next to the shaft = 580 kg/m² shaft. Fire:
firefighter lift per state high-rise rules + **EN 81-72** (≥ 1 000–1 800 kg class, ≥ 90 cm door,
shaft/cab ventilation, fire-rated supply + genset); **EN 81-73**: alarm → recall floor, doors open, out
of service; car batteries keep only lighting + alarm — plan the intercom (24 h service) and rope-pull
access.

## 17. Riser and Shaft Planning

### 17.1 Service-entry room (Hausanschlussraum DIN 18012)

All entries in one accessible room: water meter/filter/booster, gas valve + meter (never above the water
pipe), district-heat transfer (pumps/exchangers), electricity cables + meter field + main switch,
telecom APL + coax, earth-conductor tab to the lightning ring (§14.7). Working depths: LV 0.60–0.80,
telecom 0.50–0.60, gas 0.50–1.00, water 1.20–1.50, district heat 0.60–1.00 m; **between services ≥ 30
cm, telecom vs others ≥ 50 cm**; headroom ≥ 1.80 m; working space ≥ 1.20 m deep; room faces ≥ 1.80/2.00
m; not a through-room; door ≥ 65 cm/1.95 m; permanent outside-air ventilation where district heat or
gas; 0–30 °C (stored drinking water ≤ 25 °C — else split the DHW transfer). Small houses: niche
0.875×2.00×0.30 m ≤ 3 m from the outside wall (no-basement EFH) or Hausanschlusswand panel (≥ 6 cm
non-comb, ≥ 2.00 m high) to 4 dwellings; **from 5 dwellings a real room: depth & height ≥ 2.00 m, width
≥ 1.50 m (single wall) / ≥ 1.80 m (facing walls)** ⚠ VERIFY Land utility rules.

### 17.2 Technical areas (VDI 2050-1)

Zones SAN / HZ / RLT / KT (cooling) / RWK / ELT / DAT; inventory: water entry, fire-water (tank, valves,
pumps), heat + fuel, cooling, AHU, electrical (> 280 kVA: transformer + MV+LV; else LV main), BMS,
floor distributors, lift machine rooms. Benchmark: administration with RLT ≈ **6 m³/(h·m²)** supply
air, retail with RLT ≈ 12 m³/(h·m²) ↔ associated technical area ⚠ VERIFY (rule of thumb — derive from
plant schedule + §4.6 envelopes, + 20 % spare).

### 17.3 Shaft sizing heuristics

| Shaft duty | Contents (incl. GEG insulation ODs) | Min clear |
|---|---|---|
| Dwelling bath wall (Vorwand) | DN100 stack + Vorwand cistern | 16–23 cm build-up |
| " | + 2 insulated water pairs (≈ 4–5 cm OD each) | **24–27 cm** |
| Foul stack shaft | DN100 + vent DN50–100 + spares | 30×30 cm |
| Combined wet shaft (MFH) | 2×DN100 + vent + 2×4 insulated risers (6–8 cm OD) | 40×60 cm |
| Riser band for heating only | 2×DN20 insulated (2×6 cm) + 2×DN40 (2×12 cm) | 45×45 cm |
| RLT duct pair | 2× duct 40×20 cm + 40 mm skin insulation + sealings | 60×45 cm ⚠ VERIFY per A=V̇/v |
| Electrical | trays/riser ladder + 30 % spare, away from water (Länder: separate shafts) | 40×30 cm |

**Riser stacking rules:** (1) one plumb grid reference repeated on every floor plan — drifting
shafts are the #1 as-built defect; (2) drainage stacks **straight, no offsets** (§12.4); (3)
pressure risers may step at each floor via distributors (branch ≥ 1.10 m above FFL); (4) ducts
step only with swept bends, sealed at every floor; (5) **water ∦ electricity shafts** where the
Land says so (standard in residential high-rise); (6) gas own vented I90 shaft or exposed —
never shared with power or drains; (7) seal every shaft at every slab per §18.4.

### 17.4 Shaft fire sealing (the number that shows up on site)

If combustible pipes or cable insulation occupy the shaft: **horizontal seal of ≥ 20 cm mortar cast at
every floor (DIN 4102-4 §8.6)**; empty conduits passing the seal ≤ 12 cm Ø, ≥ 20 cm long, plugged
class-A. Shaft walls: I30 from 6 full storeys, I60 at the high-rise boundary, I90/I120 by use.
Fire-resistance classes and the MLAR escape-route logic: see `fire-protection-building`.

## 18. Interfaces with Structure and Construction

### 18.1 Chases in masonry (DIN 1053 practice, EN 1996-1-1/NA)

- **Pre-formed vertical chase, 12.5 cm deep: only in load-bearing walls ≥ 24 cm** — order it with the
  masonry drawing; retro-cut verticals ≤ 3 cm without proof (≤ 8 cm allowed if wall ≥ 24 cm and the
  chase ends ≤ 1 m above the floor); **horizontal/sloped retro chases only within ± 40 cm of the slab,
  1–3 cm deep, electrical cables only — never pipes**; total chase width ≤ 26 cm per 2 m of 17.5 cm wall
  (≤ 38.5 cm thicker), proportional for shorter sections; openings in unstressed walls ≤ 3 cm deep and ≤
  1/6 thickness, ≥ 2 m spacing. **Chasing/closing is a billed special service (VOB) — decide at tender,
  not on site.**
- Chase depth = pipe OD + socket + clamp: 12.5 cm chase → plaster bulge + acoustic bridges; > 12.5 cm →
  structural check (DIN 1053); external walls must keep the DIN 4108-2 minimum after the cut ⚠ VERIFY.
- The correct answer to a chase problem is almost always a **drywall service void** — plan the 4–6 cm
  Vorsatzschale instead of fighting the masonry.

### 18.2 Light-gauge / drywall service walls

Studs 6–27 cm; DN100 stack needs 16–23 cm wall, crossing DN100 + insulated water 24–27 cm, horizontal
DN100 in double-boarded stud ≈ 27 cm; GKBI (impregnated) wet rooms, double boarding for WC-rocking
resistance; **no pipes in separating light-gauge walls to protected rooms** (it voids the acoustic
rating — §19). Prefab Montagerahmen/blocks: block projection 15–18 cm, height 90–150 cm, half-height
gives the 1.10–1.20 m ledge (target 15 cm = tile width); pre-assembled pipe packages per bathroom —
order early, they fix your floor levels.

### 18.3 Beams, slabs, voids

**Ducts never cross beams; big pipes only in engineered, scheduled openings** — the decision tree is
always reroute → drop ceiling → designed sleeve; transfer/cantilever: no opening; keep clear of column
faces and support zones. Group the bathroom slab cluster as one designed opening with trimming;
post-tensioned slabs zero tolerance; core drilling = scan + engineer sign + schedule entry (§5.2). Ceiling trunks on
slab ride the §4.3 lane rules; through-wall façade sleeves slope outward 1 %+ (split units, HP lines,
exhaust terminals).

### 18.4 Fire-stopping of service penetrations (NRW-typical practice ⚠ VERIFY per Land)

| Penetration | Requirement |
|---|---|
| Combustible (plastic) water/waste pipes through classified floors/walls | encase ≥ **15 mm mineral plaster on non-comb carrier** (≈ 4 m plaster jacket, ≥ 1 m each side for walls), or **fire cuff on exposed pipes ≥ 32 mm Ø**; pipes < 32 mm treated as non-comb ⚠ VERIFY (some Länder 50) |
| B1 / fibre-cement / Al pipes | fire-cuff duty every 2nd storey; branches inside a compartment exempt |
| Cast-iron (non-comb) pipes | mortar-filled penetration (Al is NOT non-comb here!) |
| Cables/cable bundles | approved composite seals (DIN 4102-4 systems), intumescent packs; wrap melt point ≥ 1 000 °C — stone wool yes, glass wool no; intumescent packs activate ~150 °C; gas/watertight versions exist |
| Shafts | §17.4 (20 cm mortar cast every floor with combustibles inside) |
| Ducts | EN 1366-2 damper or L30/L90 casing at every compartment crossing (§11.7) |
| Escape routes | non-combustible pipes only; combustible lines concealed only per MLAR patterns (F30–F90 ducts, ≥ 15 mm plaster-covered chases, double floor ≤ 20 cm voids); halogen-free cables for occupied routes ⚠ VERIFY project class |

### 18.5 Safety-installation cable protection

BMA, voice alarm, emergency lighting, escape/fire lifts, fire-water booster, RWA, smoke-damper release
circuits: **E30/E60/E90 functional maintenance** — fire-resistant trunking/ducts or cables under ≥ the
specified mineral screed cover on the raw slab (§14.9); never share a shaft that voids the survival
claim; verify class against the fire-protection concept per building.

### 18.6 Concentrated loads, upstands, roof plant

PV ballast frames, water tanks, HP units (concrete pad + gravel + mass ~30–50 kg/kW class ⚠ VERIFY),
gensets, lift machines, flat-roof retention boxes (filled for r(5,100) = water load!) — every one is a
**patch load fixed at structural design stage**, on beams/roots, never mid-slab; roof plant needs
craning/transport routes and service walkways; oil/condensate trays with 10 cm upstands at plant-room
doors (AMEV logic §8.2). Sunk bathroom floors as in the old play: only by structural instruction,
decided early.

## 19. Plant Noise and Acoustic Interfaces (DIN 4109 / VDI 4100)

### 19.1 Room-side limits (foreign protected rooms = living/sleeping/teaching/office)

| Source | Living/sleeping | Teaching/working |
|---|---|---|
| Water supply + drainage | **≤ 30 dB(A)** (draft 4109: 30; legacy 35 ⚠ VERIFY) | ≤ 35 dB(A) |
| Other building services | ≤ 30 | ≤ 35 |
| Ventilation, steady ton-free | +5 dB(A) allowed | +5 |

VDI 4100 (contractual): SSt I/II/III for water in MFH = 35/30/25 dB(A), semi/terraced 35/25/20,
owner-occupied 35/30/30; drainage alone SSt II/III 20/15 (MFH). **Specify the level in the contract — +5
dB ≈ perceived doubling.**

### 19.2 Construction rules the TGA designer must respect

- Pipe-enclosing walls ≥ **220 kg/m² surface mass**; 11.5 cm shell + two-sided lime plaster reaches it
  only with Vollziegel ρ ≥ 1 600 — hollow masonry needs thicker/added mass (building-physics-thermal-moisture/acoustics
  siblings own the proof).
- **Armaturengruppe I (quiet fittings) mandatory** where the plan is acoustically unfavourable (walls
  adjoining/over/under protected rooms); group II only away from protected rooms.
- Install noise is structure-borne: **resilient pipe clamps, no felt strips or open foam** (mortar
  slurry infiltrates → sound bridge; closed-cell water-repellent sleeves OK); chases: plaster carrier
  (Streckmetall) + insulation fill, **mortar must not touch the pipe**; allow expansion
  movement of WW/heating pipes (creak/cracks).
- Exposed stacks in rooms routinely beat 30 dB(A) — enclose or route outside the protected-room wall;
  keep open pipes ≥ 4 cm off the wall face (cleaning/painting); big falls (single-pipe risers, high
  flow) are worst.
- Stack + Vorwand + mass per EN 81-1 lift shaft: §16.3.

### 19.3 Outside units and plant rooms (TA Lärm / rec limits)

Air-source HPs, ERAs, gensets: **night-time limit 35 dB(A) at the nearest protected-room window (pure
AND general residential; day 50/45 resp. 45/40 dB(A) — TA Lärm area class decides ⚠ VERIFY)**;
manufacturer Lp/W data at 1 m + distance drop — a 50 dB(A)/65 dB(A) class HP needs 3–10 m to property
line at night ⚠ VERIFY per spectrum (tonality!); mitigate: gravel bed + concrete mass, resilient mounts,
deflectors/top discharge, silence hoods (they cut airflow → performance), never point at a neighbour
bedroom; AHU/plant rooms: floating screed, resilient mounts, silencers in ventilation paths, doors
closed (own fire compartment §11.7).

## 20. Pipe Insulation and Cooling-Surface Dew Point

### 20.1 Why insulation is a space rule

GEG Anlagen 8 / GModG + DIN 4108 (λ = 0.035 reference) minimum thicknesses for pipes in unheated spaces
and distribution:

| Pipe inner d_i | Insulation thickness | Result OD (approx., DN label) |
|---|---|---|
| ≤ 22 mm | 20 mm | DN20 → **60 mm OD** |
| 22–35 | 30 mm | DN25–32 → 82–95 |
| > 35–100 | = d_i | DN40 → 120 … DN100 → **300 mm** |
| > 100 | 100 mm | DN125+ → 325+ |
| Penetrations, crossings, joints, distributors | **half thickness** allowed | |
| In-screed between different users (metering boundary) / cooling pipes | 6 mm reduced | OD 32–112 |

A heating riser DN15–20 with insulation is **7–8 cm fat**, branch ≤ 8 m runs ~5–6 cm OD (pipe-in-pipe) ⚠
VERIFY — shafts, chases and ceiling voids are dimensioned on the insulated OD, never on the pipe name.
Cold-water lines in shafts/ceilings: 13 mm (25 °C duty); CW in unheated ≤ 20 °C rooms: 9 mm;
in-wall/floor: pipe-in-pipe or 4 mm; hot circulating lines: ≈ 1× OD (> 8 m runs), ≤ 8 m: ½ OD —
GEG-anlage logic.

### 20.2 Dew point on cooling surfaces (the failure mode nobody sees)

Any surface carrying water colder than the room dew point sweats: chilled ceilings, core activation
(16/19 °C), cold-water pipes, chilled-water ducts, even CW in a warm shaft. Control rules:

1. Surface temperature stays **≥ 17 °C** (planning anchor; verify with the room design state — dew point
   of 26 °C/60 % ≈ 17.6 °C: Magnus, see the physics skill) — hence the tight 16/19 or 18/21 bands and
   **dehumidification responsibility on the ventilation** (WRG plants don't dehumidify enough in humid
   peaks — sizing includes a dew-point margin).
2. Vapour-tight insulation on ALL cold lines and chilled-water pipes (diffusion-tight, seam-sealed — a
   0.5 mm gap is a wet spot in year two); cold ducts insulated thicker than heating ducts (§11.6).
3. **Dew-point interlock:** room humidity sensor or supply-air dew-point tracking → flow-temperature
   raise or surface shut-off; core activation without the interlock is a mould claim on the slab soffit.
4. Condensate from coils/trays: trapped, sloped, DN≥25 drain with overflow alarm under AHU sections;
   split-unit indoor condensate to drainage with a siphon and fall (never into the soil stack
   untrapped).
5. Glaser check for embedded coolers (build-up from the warm side!) belongs to
   `building-physics-thermal-moisture` — this skill only enforces the reservation: access for the
   sensor, drain, and the 40–60 cm void.

## 21. Maintenance Access (plan the person, not just the pipe)

| Object | Envelope |
|---|---|
| Meter field / HAK, sub-distribution | ≥ 1.20 m working depth, door opening ≥ 90° ⚠ VERIFY, nothing stored in front |
| Pumps, booster, Hebeanlage, genset | 60 cm front + drainage + power + alarm; oil-tight floor, service sides, ≥ 2 exits > 350 kW |
| AHU filter/coil sections | withdrawal side ≥ coil length + 40 cm; access door to ducts near bends (30/10–60/50 cm) |
| Manifolds (FBH) | full height access, no tiled-over cabinets without removable fronts |
| Fire dampers | **inspection opening at the actuator side, every damper, closable and reachable** (§11.7) |
| Cleanouts / stack bases | 30–40 cm above FFL, no furniture zone |
| Lift pit / roof space | §16.2; ladder or door by depth |
| Solar/battery/roof plant | disconnects visible, extinguishing access (Li-ion ⚠ VERIFY), walkways/pads, cleaning water, snow-clearance kept |

## 22. Energy-Certificate Data Model (what to collect while designing)

The GEG/DIN V 18599 certificate eats these — capture them as model properties (§24.5) from day one,
don't reconstruct them at issue:

- geometry: NEEA/net floor, conditioned volume V_e, A/V_e, storeys, usage split, component years;
- envelope: U per element (+Ψ set or allowance), window Uw/Ug/g incl frame, n50 with blower-door report; thermal-bridge strategy;
- **heat load Φ_HL (DIN EN 12831) or the documented q_V heuristic (§7.2) flagged as heuristic**; heating
  + cooling demand kWh/(m²a);
- generation per station: type, η_s or JAZ/SPF target, nominal/ bivalence capacity + changeover θ,
  emitters (type + design VL/RL), buffer volume, control class, **GA per ISO 52120 class A–D** (non-res
  > 290 kW: class B mandatory + digital energy monitoring, GModG ⚠ VERIFY);
- DHW: storage volume, set temps, circulation yes/no + sleep strategy, DIN 4708 check flag, solar
  fraction (collector area, tilt, yield), TrinkwV/ W 551 documentation status;
- ventilation: system, air rate, WRG η class, SFP class; **PV kWp + tilt/azimuth + kWh/a (§14.8)** + storage kWh, EV points,
  export/self-use assumption;
- factors: fp per carrier (§8.1), CO2 g/kWh per current DIN V 18599-9/UBA ⚠ VERIFY vintage,
  district-heat FW certificate (validity!), pe/e classes of auxiliary;
- meters/monitoring: per-dwelling heat + DHW metering (billing duty), HP meter, iMSys sub-metering ⚠ VERIFY.

## 23. Worked Example — Single-Family House (all systems, this skill's numbers)

Two-storey EFH, living 140 m², clear height 2.5 m, V_e ≈ 350 m³, A_e ≈ 280 m², Berlin (θ_e −14 °C, f =
1.13), 4 occupants, airtight efficient build, garden, electric car later. **Every step re-checkable with
the sections cited.**

1. **Heat load (§7.2/7.3):** A/V ≈ 0.8 → 14.5 W/m³ × 350 = 5.08 kW × 1.13 = **Φ_HL ≈ 5.7 kW ≈ 41 W/m²**
   — inside the new-build band (15–55 W/m²). Bath 24 °C on the load list, stairs/laundry 15.
2. **Emitter (§9.3):** underfloor 35/28 (ΔT_m ≈ 31.5 K), 16×2 pipe, **6–7 loops ≤ 100 m / ≤ 20 m²**,
   spiral, 15/10 cm spacing ⚠ VERIFY, 40 mm insulation + perimeter strip, wet screed ≥ 45 mm over
   pipes, joints ≤ 8 m / ≤ 40 m² / 2:1; bath 24 °C external wall gets an extra band + a towel radiator
   sized as a real emitter; two manifold niches (1 m × 12 cm deep, 80 high); pressure test logged
   before and during screed.
3. **Generator (§8.3):** brine-source HP, **monovalent** (ground source, to −16 fine): 5.7 kW_qu ÷ 60
   W/m (VDI 4640, normal soil, 1 800 h) = 95 m → **2 × 50 m boreholes, 6 m apart**; brine 40 % glycol to
   −20 °C; water authority permit + grouting proof (permit logic, §8.3); HP ≤ 50 kW sits in the cellar
   technical room without special room duty; buffer 60 l anti-cycling + 300 l DHW tank as storage
   (§10.1); heating curve weather-comp, hydraulic balance before handover; JAZ target ≥ 4.2 (SPF anchor
   band 3.6–4.2 ⚠ VERIFY against offer data at 35 °C flow).
4. **DHW (§10.1/10.2):** 4 p × 45 l = 180 l @60; **300 l HP tank, set 60 °C, never < 50**, single daily
   60 °C legio load (PV-surplus window preferred); all DHW branches < 5 m / < 3 l → stays in the
   **small-installation regime** (no 60-always duty, no circulation needed); CW insulated in the shaft
   13 mm (§20.1); storage ≤ 400 l, DIN 4708 check flagged ⚠ VERIFY; clean-out manhole per DIN 4753;
   commissioning flush + operator W551 note handed over.
5. **Ventilation (§11.2/§11.6):** central **ZAB 130 m³/h, counterflow plate ≥ 85 % (H1), SFP ≤ 500
   W/(m³/s)**; bed 30 / living 55 / kitchen+bath 45 extract m³/h ≈ balance 125–130; Ø 75 PE loops
   under the upper screed, mains Ø 150 at ≈ 2 m/s (A = V̇/v = 0.018 m²); transfer via door undercuts +
   kitchen grille; extract terminal ≥ 1.5 m from openings ⚠ VERIFY; ISO Coarse filters + spares;
   per-room airflow + noise logged at commissioning (§25.4).
6. **Drainage (§12):** bathroom stack: **2× WC (6 l) 2.0 + 2.0 · bath 0.8 · 2× basin 0.5 · shower 0.6 ·
   kitchen sink+DW 0.8 · washer 0.8 → ΣDU ≈ 8.0; Q_ww = 0.5√8 = 1.4 l/s → vented DN100 stack (4.0 l/s
   ✓)**, branch DN50–70 vented at 0.5 %, Grundleitung DN100 @ 0.5 % with chamber outside, stack through
   the roof vent; **no fixtures below the RSE** (raised ground floor) → no Hebeanlage; cellar drain
   DN100 kept with trap + primer note; rain: roof 160 m², München-class r(5,5) 356 → Q = 5.7 l/s →
   2×DN90 downpipes (C = 1.0), balcony drain + overflow in the parapet.
7. **Water (§13):** DN25 meter; house line DN32; after meter: filter 50 µm + pressure reducer set 3.5
   bar (street 5.5 ⚠ VERIFY), distribution bank with per-use off-takes (dwelling, HP make-up? closed
   loop, garden/frost, laundry); Cu/stainless risers + PE-X-in-pipe branch; 40 mm air gap at all
   outlets; test + flush documented.
8. **Electrical (§14.3/14.5):** HAK + 63 A main fuse, 1-WE meter field; **140 m² → 7 general circuits +
   specials: stove (400 V), DHW element, HP, washer, dryer, EV-ready conduit** → 12–14 ways → 2-row UP
   sub-distribution (≈ 36×25×14 cm class ⚠ VERIFY) in the cellar technical corner, never on a
   sleeping-room wall; RCD groups: bath circuits + exterior (type A), fridge/HP/lift-free own lines;
   zones DIN 18015-3 drawn into the wall plan (§4.1); EV: 11 kW wallbox on the garage circuit later —
   **RCD A+6mA DC at the box, load management reserved**; ≥ 30 % spare conduits incl. one empty
   top-floor→basement duct.
9. **PV (§14.8):** roof S 30°, 45 m² usable → **10 kWp mono (4.5 m²/kWp)** → 10 × 960 ≈ **9.6 MWh/a**;
   self-use: HP + DHW + battery 10 kWh → ~50–60 % self-consumption ⚠ VERIFY heuristic; grid-feed per TAB
   form; DC SPD at the combiner (§14.7); no penetrations new — clamp rails on flashed hooks, sweep path
   kept (chimney §8.2).
10. **Plant/shafts (§17):** Hausanschluss corner: HAK + water + telecom + heat pump flow/return through
    the wall at the borehole route; wet-wall shaft in the interior: DN100 + vent + insulated heat +
    water pairs = **40×60 cm clear**, one plumb reference on every plan; boiler-room logic not needed (≤
    50 kW electric HP room = any technical room, §8.3), 1.20 m working depth everywhere, door ≥
    0.80/1.90 m.
11. **Certificate pack (§22):** heat load 5.7 kW documented method-flagged, borehole + HP data sheet
    (JAZ), FBH 35/28, ZAB η 85/SFP class, 300 l tank, PV 10 kWp/9.6 MWh, fp 1.5–1.8 electricity, n50
    measured — filed as model properties (§24.5).

## 24. FreeCAD Modelling of TGA (reservation grade)

Companion to `construction-freecad-bim` — reuse the Site/Building/Storey hierarchy and the Subtractions
technique; this is the TGA-specific routing.

### 24.1 What to model — and what not

Model: **shafts (as wall-bounded voids or Part boxes), risers (vertical cylinders), duct trunks,
insulated pipe trunks (as OD cylinders incl. insulation), sleeves/voids (parametric Subtractions),
plant-room equipment solids, maintenance envelopes (transparent solids), penetration schedule anchors.**
Do NOT model every bend, reducer or socket — reservation grade. Heads-up: Arch **Pipe/PipeConnector**
exist and classify as IfcPipeSegment/IfcPipeFittingSegment; treat them as generic cylinders — FreeCAD
has no hydraulic system objects. **`run_fem_analysis` and any solver are structural tools only — never
present an FEM result as a service calculation** (no airflow, no thermal, no voltage-drop FEM here;
those are engineering calculations outside the model).

### 24.2 Model organisation

```
Site → Building → Storey_xx
    ├── BP_Structure (walls, slabs, beams, columns)
    ├── BP_Architecture
    └── BP_TGA
         ├── Grp_Schaechte        (shaft voids + fire seals)
         ├── Grp_Abwasser         (stacks, falls, vents   — slope modelled!)
         ├── Grp_Wasser           (risers, branches)
         ├── Grp_Heizung          (trunk OD incl. insulation, manifolds)
         ├── Grp_Lueftung         (ducts, AHU solid, dampers at seals)
         ├── Grp_Elektro          (HAK, sub-distributor, trays, risers)
         ├── Grp_Anlagen          (HP, tank, boiler, pump — with §21 envelopes)
         └── Grp_Sleeves          (void solids, tag-named P-xx-X-nn)
```

One group per discipline = hide/export/intersect as one body; name every object with its schedule tag +
service + size so the IFC export carries readable properties.

### 24.3 Sleeves as live parametric voids

Model each sleeve/zone as a cylinder/box and put it in the host's **`Subtractions`** list (Arch
property) — same technique as window openings: move the sleeve, the hole moves. Model the **approved
void** (what the structural engineer signs), not the pipe. Rebuild the penetration schedule (§5.1) from
these voids, never in a parallel sheet.

### 24.4 Boolean clash and soft-clash checks

```python
# run via the FreeCAD MCP execute_code path — hard clash = structure ∩ TGA
import FreeCAD as App
doc = App.ActiveDocument

def solids(label):
    grp = doc.getObjectsByLabel(label)[0]
    return [o for o in grp.OutList if hasattr(o, "Shape") and o.Shape.Solids]

TOL = 1e-6
for s in solids("BP_Structure"):
    for m in solids("BP_TGA"):
        c = s.Shape.common(m.Shape)
        if c.Volume > TOL:
            print(f"HARD CLASH {s.Label} <-> {m.Label} {c.Volume/1000:.1f} cm3")
```

Non-zero volume where the host already carries the sleeve in `Subtractions` = the sleeve moved
without the schedule; clash against an approved void = stop and log. **Soft clash:** intersect the
transparent maintenance envelopes (§4.6/§21: 90 cm fronts, damper access, manifold width, ≥ 1.20 m
plant depth) against walls/doors/services — report as soft clash, not noise. **Slope check:** model
every drain at its real 0.5 % fall with invert levels — a horizontal drain hides the failure (§12.3).

### 24.5 IFC export discipline

- Classify: pipes → IfcPipeSegment, ducts → IfcDuctSegment, sleeves/voids → IfcOpeningElement, equipment
  → IfcFlowTerminal/MovingDevice per type; **verify by re-importing the export, not by assuming**.
- Attach properties: service name (German + tag), DN/d_i, insulated OD, material class (A1/B1/B2), slope
  %, design temp; energy data per §22 on their host objects; group systems via IfcSystem where the
  exporter supports it.
- Before export (§27 checklist): real diameters everywhere (1/3-chase and shaft-width checks need them),
  fire seals present as objects at every compartment line, schedule regenerated.

## 25. Coordination Checklists (stage gates)

**5.1 Concept:** wet walls stacked; shafts + DIN 18012 room + plant rooms on the plan with §17 sizes;
ceiling-void budget (30/40–60 cm) fixed with the structural depth; heat-load heuristic + system
decision (§7/§8/§11) recorded; escape-route/compartment rules fed back from `fire-protection-building`.

**5.2 Detail design (before structural freeze):** every duct/pipe route on section through every wet
wall and corridor; slope budget for the whole drainage path computed to the chamber invert (§12.3);
insulated ODs used, not DN labels; DIN 18015-3 zones on every room plan; chase schedule against wall
types (§18.1); fire-stopping type fixed per penetration (§18.4); HP/ plant noise distances (§19.3);
lift/shaft/pit geometry vendor-matched (§16).

**5.3 Pre-cast/pre-pour:** every P-tag cast-in and braced, capped; sleeves ≥ §18.4 seals present; no
un-scheduled holes; drainage invert level-checked (not eyeballed); shaft wall fire class built;
escape-route materials checked; engineer sign on the pour card.

**5.4 Commissioning/handover:** pressure tests (water, heating 1.3×, gas by contractor), drainage water
test, air-flow balance per room + noise spot checks, **W 551 flush + temperature log + operator
documentation**, electrical E-Check/Inspektionsprotokoll incl. RCD trip times, TAB conformity
declaration (grid + PV + HP), meter/heat-meter configuration for billing, as-builts with every
deviation, energy data set (§22) assembled from the logs.

## 26. Common Failure Patterns (German flavour)

| Failure | Rule broken | Correct action |
|---|---|---|
| DN100 stack chased into a 11.5 cm KS wall | §18.1/§19.2 — chase bulge, sound bridge | 16–23 cm Vorwand or the shaft; stack straight |
| Duct "through" the beam on the section | §18.3 | drop ceiling / move the run; ducts never cross beams |
| Horizontal chase cut across a 17.5 cm wall at mid-height for pipes | §18.1 | drywall service void; electrical-only within ±40 cm of slab |
| PEN continued through the installation (Nullung) | §14.1 TN-C-S boundary | rework: split in HAK, PE+N separate from there |
| Single house-wide RCD on everything | §14.5 | per-group RCDs; fridge/HP/lift outside the nuisance zone |
| Bath sockets on the shared circuit without 30 mA | §14.4/14.5 | VDE 0100-701 zones + RCD on every bath circuit |
| Wallbox on a socket circuit behind a type AC RCD | §14.8 | dedicated circuit, RCD A+6mA DC or B, load management |
| Data cable in the same pipe as 230 V | §14.5 | separate ducts, 10 mm air gap/partition in shared trunk |
| DHW stub 12 m to a far guest bath, unflushed | §10.2 (W 551 3-l rule) | shorten / circulate / local instant heater |
| CW risers uninsulated in a warm shaft | §10.2/§20.1 | 13 mm CW insulation — ≤ 25 °C at the outlet |
| Underfloor loop 140 m, no balancing | §9.3 | split ≤ 100 m loops, flow meters at the manifold |
| Screed without joints over a 60 m² open floor | §9.3 | joint fields ≤ 40 m² / ≤ 8 m, 2:1 max |
| Chilled ceiling commissioned without dew-point interlock | §20.2 | sensor + control, ≥ 17 °C surface policy |
| Drainage at 0.3 % "to save the ceiling" | §12.3 | uniform ≥ 0.5 %; sunk zone or lower chamber |
| Fecal lift discharge gravity-loop omitted → storm backflow floods the WC | §12.7 | Hebeanlage with air gap + loop above RSE |
| Fire cuffs skipped on 40 mm PP pipe through the F90 floor | §18.4 | encase ≥ 15 mm plaster or cuff; check every plastic penetration |
| Shaft sealed once at the roof | §17.4 | DIN 4102-4 20 cm mortar cast at every floor |
| Heat pump 2.8 m from the neighbour's bedroom wall | §19.3 | night TA Lärm 35 dB(A) proof at the line, move/mass/silence |
| Sub-distributor on the shared sleeping-room wall with contactors inside | §14.3/§19 | relocate; never switching buzz into a protected room |
| Lift shaft 11.5 cm plasterboard beside a bedroom | §16.3 | DIN 8989 masses / decoupled shaft — structural task, TGA checks it |
| Core-drilled beam sleeve nobody approved | §5.2/§18.3 | scan + engineer sign + schedule entry before, or not at all |
| Certificate reconstructed from memory in year two | §22/§24.5 | capture as properties during design; log at commissioning |

## 27. Verification Checklist (before presenting any TGA design output)

- [ ] Heat load method stated (DIN EN 12831 or §7.2 heuristic flagged as such); bath 24 °C, setback
  agreed; emitter temps keep the generator in band (HP flow low; boiler return < dew point)
- [ ] Underfloor ≤ 100 W/m², loops ≤ 100 m, screed/joints/niches drawn; HP source from extraction
  anchors with soil/permit caveat; bivalence split documented
- [ ] GEG/GModG duties addressed (65 %-path, solar-DHW, direct-electric gate) + boiler/plant rooms
  per MFeuVO/AMEV with chimney-sweep access; quoted ⚠ VERIFY numbers checked against current text
- [ ] W 551 strategy chosen and drawn: storage temp, 3-l dead legs measured on the plan, circulation ΔT,
  CW ≤ 25 °C, documentation duty noted
- [ ] Ventilation tier decided (natural / dezentral / ZAB); rates + CO2 check; WRG + SFP class named;
  door-plan transfer paths; 18017 shafts where windowless; ducts from A = V̇/v; cold-duct insulation;
  damper or casing at every compartment crossing, with access
- [ ] Drainage: slopes ≥ 0.5/1.0 %, Q_ww calc on the drawing, stack/vent DNs, stack feet (spur/
  bypass), cleanouts, traps, vent terminals; Trennsystem per byelaw; rain: r(5,5) locality, drains
  ≤ 20 m, emergency overflow, Überflutungsnachweis at > 800 m² sealed
- [ ] Backflow: RSE located; sub-RSE fixtures protected by the correct device (lift for fecal, EN 13564
  logic elsewhere)
- [ ] Water: pressures at the worst outlet, PRV zones, filter + air gaps, meter/booster room rules,
  expansion + fixation physics
- [ ] Electrical: grid form stated (TN-C-S split at HAK, no PEN extension), DIN 18015-2 circuit count,
  specials on own circuits, zones on the wall plan, bath zones + IP + RCD map, load-group calculation
  flagged, EV circuit + RCD type, PV yield assumption + TAB/storage, emergency/safety circuits
  E30-classed where required
- [ ] Lighting lux/UGR/Ra targets + MF/lumen assumptions logged; emergency lighting where required;
  lightning decision + DIN 18014 electrode planned during construction + SPD cascade 1/2/3
- [ ] RWA/lift/fire-water interfaces reserved with the fire skill; shaft seals + sleeve fire classes on the schedule
- [ ] Shafts on insulated ODs, one plumb reference, seals every floor, water ∦ power, gas own duct;
  chases vertical-only / pre-formed preferred, VOB items agreed
- [ ] Noise: group I fittings, 220 kg/m², resilient clamps, plant distances proven; insulation
  schedule (§20) + dew-point strategy for every cooling surface
- [ ] Maintenance envelopes modelled + reachable; commissioning logs assigned; as-built + §22 data set from the model
- [ ] Every ⚠ VERIFY number either replaced by the current standard value or carried into the
  deliverable text with the flag
- [ ] Honest boundary stated in the output: planning aid, specialist design and signed approvals still
  required (§1)

## 28. Quick Reference Card

```
HEAT LOAD (§7)  Φ=q_V(A/V)·V·f | A/V .5→11.8 .8→14.5 1.1→17.3 W/m³ | f −10→1.00 −14→1.13 −20→1.33
  vent add 0.34 Wh/(m³K)·V̇·ΔT | min 0.5 1/h | new res 15–55 W/m² · 3-Liter 25–40 · PH ~10
HP (§8.3)  COP air 3.3 / brine 4.2 · SPF air 2.7–3.2 brine 3.6–4.2 gw 3.8–4.6 | mono: ground/water to −16
  biv-alt switch ≈50 % peak → HP ~60 % heat · biv-par boiler 50–70 % | changeover d/a: K58 S73 B82 M107
  borehole 60 W/m normal (1800 h) → m=Φ/ε · collector 10–40 W/m², mono 1.5–2.5× living · air 4 000 m³/h
  per 10 kW + noise · ≤50 kW any room
BOILER (§8.2)  >50 kW own room ≥8 m³ h≥2 m, vents 150+150 cm² (+2 cm²/kW) | flue ≤11/10/9 % (1.BImSchV)
  condensate neutralise >25 kW | oil ≤5 000 l/unit, >5 000 l separate room, ~0.9 m³ room/kW
GEG (§8.1)  wall U≤0.28 · 65 % renewable path (WPG stages) · solar-DHW §35-logic · direct-electric 30/45 %
  gates · fp fossil 1.1 / wood 0.2 / DH ~0.7 / elec 1.8→1.5 ⚠ · CO2 price 55–60 €/t era
EMITTERS (§9)  FBH ≤100 W/m² · surf ≤29 °C · loop ≤100 m ≤20 m² · spiral · screed ≥45 mm over pipe ·
  joints ≤8 m/≤40 m²/2:1 · no pipe under bath | rads EN 442 n≈1.3, enlarge ×1.5/×2/×2.5 at 70/55, 60/50,
  55/45 | ceiling cool ≤100 heat ≤40 W/m² · core 16/19 + dew interlock
W551 (§10)  grow 30–45 · stop ≥50 · kill min 60–65/sec ≥70 · set 60 never <50 · Großanlage >400 l or
  >3 l lines → ≥60 always · circ ≤5 K, 8 h sleep · CW ≤25 °C · 300 l HP tank · 30–60 l/p·d @60
VENT (§11)  <1000 ppm ok · Δ550→10 Δ800→7 Δ1350→4 l/s·P · min 4 l/s·P · 20 l/h·P · windowless 18017
  (K 40–60/200 · bath 40 m³/h continuous, 60 demand) · 1946-6 tiers · ZAB WRG ≥80–90 % SFP ≤500 · A=V̇/v · LP 4–12 m/s ·
  flat-duct double area · flex ≤Ø400/20×Ø · EN 1366-2 damper per compartment · AHU room F90
DRAINAGE (§12)  Q=K√ΣDU K 0.5 dwelling · vented 0.5 % unvented 1.0 % · DN100 4.0 l/s · WC6l 2.0 DU ·
  spur ≥25 cm (≥4 sto/10 m) · bypass >8 sto · vent ≥1 m/2 m · trap ≥50 · cleanout 30–40 cm · no 90°
  horizontal · RSE≈kerb → fecal below = lift + loop · rain Q=r(5,5)·A·C/10⁴ (M356 B331 St405) ·
  >800 m² sealed → Überflutungsnachweis r(5,2)→r(5,30)
WATER (§13)  EN 806/DIN 1988 · filter 50 µm · 0.5/1.0/1.2 bar · aim ≥1.5 flowing · PRV >4.5–5 ·
  air gap 40 mm · Cu never above galv · flush+full fill handover
FIXTURES (§13.6)  WW l/(p·d)@60: dwell 30–60 · hotel/nursing 60–70 · rest 15–45/seat · sports 30–50 |
  bath 160@40 · shower 40@37 · basin 5–20@35 · sink 10–20@50 · WC 6/9 l · limiters 5–12 l/min |
  kW≈2×l/min@40 · 12 kW sink-grp / 18–21 kW bath-shower · 5.6 kWh/100 l @10→60 · Grundwerte [VERIFY]
ELECTRIC (§14)  TN-C-S split at HAK, PEN never extended · riser 1/2/3 WE 63/80/100 A · circuits ≤50→3
  …>125→7 + specials · kitchen ≥5 double · circuit ≤16 A (3.68 kVA) · fixed ≥3.7 kW · RCD 30 mA
  per group, bath+outdoor mandatory · EVSE A+6mA DC or B · zones 30/30 + ZS 10–30 cm · bath 0/1/2
  IPX7/X4/X4 no socket 0–2 · fridge own circuit · data ∦ power · 30 % spare · 500 lx office UGR19
  Ra80 · corridor 100 · MF 0.67–0.8 · emergency 1 lx ≤15 s 1 h · LPS I–IV mesh 5/10/15/20 · DIN 18014
  electrode during construction · SPD 1/2/3
PV (§14.8)  30°S 1130/1200/1300 ×0.8 → 904/960/1040 kWh/kWp · mono 4–5 m²/kWp · −0.4 %/K · winter 25 %
  · Li 5–10 kWh · TAB form · GEG §13 duct per parking space
SHAFTS (§17)  DIN 18012 ≥5 WE 2.0×2.0×1.5/1.8 · niche 875/2000/300 · ≥30 cm between trades · head ≥1.8 ·
  work ≥1.2 · bath wall 16–23, +pipes 24–27 · combined 40×60 · 20 cm mortar seal per floor · water∦power
  · gas own I90 · straight stacks, one plumb ref
STRUCTURE (§18)  pre-formed vertical chase 12.5 only in ≥24 cm · cut vert ≤3 (≤8 if ≥24 & end ≤1 m AFF)
  · horizontal ±40 cm slab 1–3 cm cables only · ≤26 cm/2 m · ducts never through beams · plastic ≥32 mm
  → cuff or 15 mm encasement · SML mortar fill · E30 safety circuits · escape routes non-comb
NOISE (§19)  30 dB(A) water living · 220 kg/m² enclosing · fittings grp I · resilient clamps, no felt ·
  open pipes ≥4 cm off wall · HP night 35 dB(A) at line · lift DIN 8989
INSULATION (§20)  d_i≤22→20 · ≤35→30 · ≤100→d_i · >100→100 · half at crossings · riser OD+ins 7–8 cm ·
  cold surfaces ≥17 °C · vapour-tight · dew interlock
PRIORITY  structure > gravity drainage > ducts > insulated trunks > water > electrical > telecom —
  nothing cast, chassed or drilled that is not Approved on the penetration schedule.
```

*End of skill. All numbers are planning aids from German practice standards; the ⚠ VERIFY marks are
load-bearing — replace them with current standard text and project data before any drawing leaves the
office.*

---

## Appendix S: Source Check 2026-10 — values re-read from the literature

Each line below was read again in the source books (`sources/`) in October 2026, with the
place it stands at. "Confirmed" means: a dated book prints the rule and names the standard
or law; it does not mean the current edition of that standard was opened. State law
(LBO) and local rules still override; `VERIFY` tags elsewhere in this skill stay in force
unless a line here names the edition. Where a line here differs from a section of this
skill, that section was corrected and names the line ("S.n"); the appendix governs.

### S.1 Drainage (DIN EN 12056-2, DIN 1986-100)

- Confirmed: discharge units DU in l/s and single connection pipe: basin, bidet 0.5 (DN 40);
  shower without plug 0.6 (DN 50); shower with plug, bath tub, kitchen sink, dishwasher,
  washing machine up to 6 kg 0.8 (DN 50); WC with 6.0 l cistern 2.0 (DN 80 to DN 100). —
  *Gebäudetechnik* Tab. 3.2.
- Confirmed: discharge coefficient K = 0.5 for irregular use (dwellings, guest houses,
  offices); Q_ww = K · √ΣDU. — *Gebäudetechnik* Tab. 3.5 and 3.1.23.
- Confirmed: a foul stack is at least DN 70, with a WC DN 80, DN 90 or DN 100; a DN 100
  stack with main venting carries 4.0 l/s. — *Gebäudetechnik* 3.1.8 and Tab. 3.10.
- Confirmed: unvented single connection pipe: at most 4.0 m long, at most three 90° bends,
  at most 1.0 m drop, slope at least 1.0 %; vented connection pipes 0.5 %; ground and
  collector pipes for foul water inside the building 0.5 %. — *Gebäudetechnik* Tab. 3.6
  and Tab. 3.4.
- Confirmed: site drainage outside the building: at least DN 100, slope at least 1/DN
  (DN 100: 1.0 %). — *Wendehorst Bautechnische Zahlentafeln* 22.3.5.2.2. A ground drain
  that leaves the building is safe on both rules at 1.0 %.
- Confirmed: the stack vent ends at least 15 cm above the roof, measured vertically; more
  where snow lies. — *Gebäudetechnik* 3.1.9.
- Confirmed: inspection chambers from 80 cm depth: rectangular ≥ 0.75 m × 1.20 m, square
  ≥ 0.90 m × 0.90 m, round ≥ 1.00 m diameter. — *Gebäudetechnik* 3.1.13.

### S.2 Water supply and house connection

- Typical: connections of fixtures and storey pipes in dwellings are DN 15, 20, 25; storey
  pipes branch from the risers at least 1.10 m above the floor. — *Gebäudetechnik* 3.4.5.
- Confirmed (DIN 18012): a single-family house without basement may have a connection
  niche of 0.875 m × 2.00 m at 0.30 m depth, at most 3 m from the outside wall. —
  *Gebäudetechnik* 1.3.
- Typical: hot water use in households 30–60 l per person and day, 40 l in the mean, at
  60 °C; store for a single-family house about 80–200 l, two-family house 200–300 l
  (large stand tanks charged once a day). — *Gebäudetechnik* 3.4.10.

### S.3 Sanitary fixtures (VDI 6000-1, as printed)

- Standard sizes width × depth in cm: single basin 60 × 55 (top 85 to 90 above the floor);
  WC with cistern in the wall 40 × 60, with cistern in front of the wall 40 × 75; shower
  tray 80 × 80; bath tub 170 × 75; washing machine or dryer 60 × 60. — *Gebäudetechnik*
  Tab. 2.8.
- Side distance between two fixtures 20–25 cm, between fixture and wall as a rule 20 cm;
  in front of a fixture a free depth of at least 75 cm (after DIN 18022, withdrawn in
  2007 and still used where no barrier-free rule applies). — *Gebäudetechnik* 2.1.3.

### S.4 Underfloor heating

- Confirmed: floor systems heat up to 100 W/m²; a loop should not exceed 100 m of pipe,
  which is 15–20 m² of floor; larger rooms get several loops. — *Gebäudetechnik* 4.4.2
  and 4.4.3.
- Confirmed (DIN 18560-2): screed at least 45 mm plus the pipe diameter. — same 4.4.3.
- Typical: manifold about 1 m wide, in a niche about 12 cm deep and 80 cm high. — same.
- Typical design temperatures, underfloor heating: flow 35–55 °C, return 30–45 °C, spread
  5–10 K. — *Gebäudetechnik* Tab. 4.36.

### S.5 Ventilation

- Confirmed (DIN 18017-3): the minimum extract air flow is 40 m³/h for baths and WC rooms
  with continuous running, or 60 m³/h with demand control; kitchen base ventilation
  40–60 m³/h. — *Gebäudetechnik* 5.4 and Tab. 5.10. This replaces the 20–30 m³/h of §11.2
  for a bath.
- Worked example, single-family house, 125 m³/h in all: living room supply 45, kitchen
  extract 40, shower/WC extract 35, rooms supply 40 and 20 m³/h. — *Gebäudetechnik* Tab. 5.9.
- Typical: air runs in insulated ducts of about 10–15 cm diameter. — *Gebäudetechnik* 5.3.

### S.6 Heat pump and load figures

- Typical: the connected load of a heat pump heating system of a one- or two-family house
  as a rule does not exceed 6 kW. — *Gebäudetechnik* 4.2.5.
- Confirmed: the output of the heat generator is Φ_SU = Φ_HL + Φ_DHW + Φ_AS: the standard heat
  load, where needed the extra output for hot water (sized after DIN 4708-1 to -3) and that
  for other systems (air heating coils, process heat). With static heating and natural
  ventilation the standard heat load alone is the basis. The book gives no number for
  Φ_DHW. — *Gebäudetechnik* 4.1.1.
- Typical, new dwellings: heat load 10 to 70 W/m² (passive house to legal minimum); hot
  water share 12.5 kWh/(m²a). — *Gebäudetechnik* Tab. 8.1; *Allgemeine Grundlagen des
  Bauwesens* 2.14.6.

### S.7 Defaults of this library for a simple house model

**Not from a book.** These are choices of this library, made so that a simple house can be
modelled at all where the literature gives a frame and no number. Tier T4, massing only:
any plan clause, product sheet, engineer's or carpenter's figure replaces them, and nothing
here is a design value.

- Outdoor unit of an air heat pump: 0.30 m of free air between unit and house wall. The
  maker's sheet decides; the distance to the boundary follows the noise check of §19.3.
- Stack vent drawn 0.50 m above the roof surface (the least is the 15 cm of S.1).
- Inspection chamber drawn 1.50 m outside the outer wall.
