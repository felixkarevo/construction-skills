---
name: roofing-waterproofing
description: >
  Dach- und Abdichtungskonstruktionen (roof and waterproofing construction) for houses in the
  DACH norms frame. Pitched roofs (Steildach): covering logic and Regeldachneigung, ZVDH
  Unterdeckung/Unterspannung/Unterdach class tables, batten/counter-batten stacking, eave,
  verge, ridge, valley and penetration detailing, wind-driven-rain exposure groups, snow loads
  incl. slide and snow-guard (Schneefanggitter) logic, covering dead-load tables. Flat roofs
  (Flachdach): warm roof (Warmdach) and inverted roof (Umkehrdach) layer stacks complete with
  layer functions, minimum falls (2 % / 3 % timber), upstands (Aufkantung) and fillets, joint
  terminations, primary + emergency drainage, separation and protection layers, single-ply vs
  multi-ply bituminous waterproofing per DIN 18531-18535 (DIN 18195 superseded - flagged).
  Balconies, loggias and roof terraces on waterproofing; wet-room tanking (DIN 18534);
  below-grade waterproofing - white tub (Weiße Wanne / WU-concrete) and black tub (Schwarze
  Wanne) per DIN 18533 load cases; roof windows, light domes and daylight openings; PV on roof
  (loads, fire separations, BIPV watertightness proof); green/retention roofs. Airtightness
  layer continuity (DIN 4108-7, GEG, n50); hygrothermal design (Glaser/DIN 4108-3 period
  balance, roof sd-ratio rule, inverted-roof U surcharge, tapered-insulation U, timber flat-roof
  state-of-the-art rules); maintenance/durability; worked examples; ranked failure patterns;
  critical-dimension cheat sheet; design-review checklist; FreeCAD/BIM modelling guidance.
---

# Roofing & Waterproofing for Houses (DACH)

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

Water is the most destructive agent acting on a building, and almost every water failure is a
**detailing failure, not a materials failure**. Claim experience in the roofing trade
consistently puts junctions, flashings and terminations - not the membrane field - at the top
of leak causes. This skill is the design-side counterpart to the structural-systems and
building-physics-thermal-moisture skills of this library: it covers how roofs are shaped, sloped, sealed,
layered, drained and terminated so the envelope keeps its functions for its design life. It is
written for **residential construction under the German/EU norms regime** (DIN, DIN EN, ZVDH
trade rules, GEG), with the physics kept universal: rain, snow, vapour and thermal logic apply
wherever the climate delivers them.

Use this skill **before** modelling any roof, parapet, balcony, wet area or basement in
FreeCAD, and **before** writing any roofing or waterproofing specification or detail drawing.

---

## Reality Check - Licensing & Liability

**This skill produces design aids and calculation guidance for planning and FreeCAD modelling
only.**

- Every number, layer stack, fall, upstand and class table here is a **preliminary sizing and
  coordination aid**. None of it is a construction-ready design.
- Structural design (roof slab, rafters, trusses, parapet anchorage, snow drift on PV arrays)
  must be calculated and confirmed by a licensed designer (Tragwerksplaner; Prüfstatik where
  the Landesbauordnung requires a Prüfingenieur). Waterproofing design for critical roofs and
  below-grade structures should additionally be coordinated with the membrane manufacturer's
  system department - system warranties are void without their sign-off.
- The project must pass the **building authority (Bauordnungsamt)** process per
  Landesbauordnung; parapet heights, roof geometry, fire separations (harte Bedachung,
  Brandwand-Abstände) and drainage discharges are publicly regulated and vary by Bundesland.
- Norms cited here (DIN 18531-18535, DIN 4108 series, GEG, Eurocodes) superseded predecessors
  (DIN 18195, EnEV). **Where this file flags [VERIFY], the value is principle-level or the
  exact clause/table was not confirmable in the digested data - read the current norm text
  before citing a clause number in a submission.** Do not cite a clause that has not actually
  been read, and do not assume which edition introduced a provision.
- If a user starts treating the output as final - asks a contractor to price it or says "so we
  can build this" - say so **unprompted**, in plain language: this is a planning model; it
  needs engineer sign-off and building-authority approval before anything is built.
- Waterproofing failures are expensive, appear slowly and are hard to reverse. When uncertainty
  exists, state it and recommend the conservative detail. Never invent a code clause, warranty
  term, product value or unit rate.

---

## Section 1: Roof System Selection

### 1.1 What the roof must do (function hierarchy)

The envelope element "roof" carries all envelope sub-functions at once
(bauliche Teilfunktionen): Feuchteschutz (moisture protection), Wärmeschutz (thermal),
Luft-/Winddichtheit (air/wind tightness), Schallschutz (acoustic), Brandschutz (fire),
Dauerhaftigkeit (durability, cross-cutting) and Kraftleiten (force transmission). Moisture
reaches the roof as: Niederschlag (rain), Schlagregen (driven rain), Schnee/Eis/Flugschnee
(snow, ice, snow blown under laps), Tauwasser (condensate) and internal Wasserdampf (vapour) -
each needs its own control path, and the internal vapour budget must be regulated too.

**Exposure gradient:** plinth (Sockel, splash zone) < facade (runs off quickly) < **roof (most
severe - horizontal planes can hold standing water)**. A flat roof is the hardest moisture task
in the building; a pitched roof is a drainage task. This single difference explains the entire
construction split:

- **Pitched (Steildach):** multi-stage by design. The open/overlapped covering is only
  *rain-proof* (Regendichtheit); a second stage (underlay) backs it up. Overlap joints in the
  water-flow direction; steep enough pitch to drain fast; top layer replaceable (re-roofing is
  normal maintenance).
- **Flat (Flachdach):** single-stage *waterproof* (Wasserdichtheit) sealed surface, which must
  be protected (ballast, multi-ply, topping) because it carries the water film itself.

A material that is perfectly waterproof **and** vapour-open does not exist (no "Gore-Tex
principle" in sheets). That constraint drives every roof build-up below.

### 1.2 Decision tree

```
1. Will the roof surface be USED (roof terrace, plant, PV, green roof, maintenance)?
   ├─ YES → flat/low-slope build-up, accessible grade: waterproofing protected by
   │         ballast / separation + paving, never left exposed as wearing surface. §3-§5.
   └─ NO  → continue
2. Span and structure already chosen?
   ├─ RC slab or timber rafters to tiles, normal domestic geometry → pitched §2
   ├─ Long-span hall, trapezoidal deck, industrial → low-slope single-ply on deck §6
   └─ Both possible → climate + energy target + use decide (table 1.3)
3. Snow region / heavy driven rain (Schlagregen group III) / exposed site?
   → pitched with raised underlay class (ZVDH table 2.2) or flat with full waterproofing;
     snow guards and drift loads on anything steep §2.6.
4. Energy target (GEG reference / efficiency house)?
   → warm roof (insulation above deck, below sealing) or Umkehrdach (above sealing);
     avoid uninsulated or cold construction on flat roofs §3-§5, §12.
```

**Rule: never call a roof "flat".** Every "flat" roof is a low-slope roof with a designed
minimum fall of **≥ 2 %** (§3.2). A truly level roof is a defect - the "flat roof is either
tight or not" argument is refuted by practice: standing water is a load, an accelerator of UV
and frost attack, and the trade rules allow zero fall only with compensating measures
(flat-roof guidelines) **[VERIFY current edition]**.

### 1.3 Pitched vs flat - comparison

| Criterion | Pitched (tiles/slate/metal) | Flat warm roof (bitumen/single-ply) | Umkehrdach (inverted) |
|---|---|---|---|
| Water action | sheds; multi-stage backup | stands - single-stage waterproof | stands - waterproof under insulation |
| Usable surface | no (room-in-roof instead) | yes, with protection layer | yes - terrace, PV, green roof |
| Waterproofing criticality | lower (underlay is 2nd line) | **critical** (detailing + falls) | critical, but membrane UV/shock protected |
| Membrane service exposure | n/a | sun, rain, thermal cycling, foot traffic | shielded - longest membrane life |
| Insulation position | between/above rafters | above vapour barrier, below sealing | above sealing (XPS/foam glass only) |
| Condensation strategy | outward drying + ventilation, or sd-rule warm roof | full vapour barrier mandatory (top skin vapour-tight) | barrier = the sealing itself |
| Typical build-up height | rafters + battens + covering | 250-450 mm | 300-500 mm |
| Repairability of field | covering renewed course by course | open up, patch, flood test | lift pavers/XPS - membrane accessible |
| Typical failure | slipped tiles, lap failure at eaves/valley, snow | ponding, bridged laps, missing upstand, blisters | displaced ballast, floating XPS, edge/root failures |

---

## Section 2: Pitched Roofs (Steildächer)

### 2.1 Rain-shedding logic (why pitch and overlap work)

Derived rules that hold universally:

1. **Overlap in the water-flow direction** (shingle principle) - every joint of a lower element
   is covered by the element above; gravity drains the joint immediately.
2. **Minimum fall for fast drainage** - below the covering's standard pitch the first stage no
   longer sheds reliably → a second, water-blocking stage is required (Unterdach), which loses
   outward drying through the joints - compensate per §2.2.
3. **Raise joints out of the water plane where possible** - folded-up edges (standing seam,
   Aufkantung) put the joint above the draining surface; the folded fins also stiffen thin
   sheet (0.5-0.8 mm metal acts structurally in a double standing-seam roof).
4. **Never stack butt joints of several layers at one point** - stagger ("entflechten") layer
   joints; one joint line through underlay + battens + covering is one leak path.
5. **Top layer replaceable** - detail so the weather skin can be renewed without touching the
   air/water layers below.
6. **Even a small overhang keeps walls nearly dry** - but a deep eave *without gutter* blows
   roof water onto the wall = concentrated damage, worse than rain. Interrupt the water film:
   gutters, drip edges (Abreiß-/Tropfkante), sharp arrises under mouldings; concentrated
   discharge (gargoyles/waterspouts) must throw clear of the facade, downpipes to ground.

### 2.2 Regeldachneigung and required underlay (ZVDH)

The roofers' association rules (ZVDH Fachregeln) define, per covering product, a **standard
pitch (Regeldachneigung)** - the pitch from which the covering alone is rain-safe ("normal
case"). Below it, or under extreme exposure (Treibregen = wind-driven rain, Flugschnee = snow
blown under laps), or with "increased requirements", an underlay system is required.

**Increased requirements (erhöhte Anforderungen)** stack - count them:
- higher-value use — **residential use counts as TWO increased requirements**;
- construction peculiarities (strongly articulated roofs, special shapes, long rafter runs);
- climate (snow-rich, exposed/windy sites);
- special legal (Denkmalschutz, Landesbauordnung extras).

**Required underlay class by pitch deficit below Regeldachneigung × number of other increased
requirements (0/1/2/3):**

| Deficit below standard pitch | 0 extra req. | 1 | 2 | 3 |
|---|---|---|---|---|
| 0° (at standard pitch) | Kl. 6 | 6 | 5 | 4 |
| ≤ 4° | 4 | 4 | 3 | 3 |
| 4-8° | 3 | 3 | 3* | 3* |
| 8-12° | 2 | 2 | 1 | 1 |

*classes at 4-8° with 2-3 extra requirements carry additional product-test conditions.
Unterdächer become necessary for deficits > 8° (up to 12° for clay/concrete tiles) or with
> 3 increased requirements. **A house is normally "2 extra" - read columns 1/2 accordingly.**

**Construction type → class (ZVDH Merkblatt):**

| Construction | Class |
|---|---|
| watertight under-roof on deck (wasserdichtes Unterdach) | 1 (Z 1.1) |
| rain-safe under-roof (regensicheres Unterdach) | 2 (Z 1.2) |
| seam- and perforation-sealed underlay on deck (Unterdeckung) | 3 (Z 2.1) |
| welded/bonded Unterdeckung | 4 (Z 2.2) |
| covered Unterdeckung with bitumen sheets | 4 (Z 2.3) |
| lapped/crimped Unterdeckung | 5 (Z 2.4) |
| seam- and perforation-sealed stretched sarking (Unterspannung) | 3 (Z 3.1) |
| seam-sealed Unterspannung | 4 (Z 3.2) |
| lapped Unterspannung | 6 (Z 3.3) |

Terms: **Unterdeckung** = membrane lying on a load-bearing deck; **Unterspannung** = membrane
stretched without deck (planned sag, sarking); materials: UDB/USB sheets, wood-fibre boards
(UDP) per ZVDH product data sheets. In rain-safe/watertight types the counter-batten is
integrated into the sealed layer; in lesser types fixings must be nail-sealed with tapes.

**Temporary weather cover during construction (Behelfsdeckung):** only UDB-A, UDB-B, USB-A with
proven impermeability under direct driven rain, with manufacturer release incl. system
accessories.

**Minimum pitch by covering:** the numerical Regeldachneigung lives per product in the ZVDH
Fachregeln and the manufacturer data — not all values were recoverable from the digested data
**[VERIFY per product]**. Direction of magnitude: deep-profile clay/concrete tiles sit
comfortably at low pitches; small-format flat products (slate, fibre-cement flats) need
steeper pitches; double standing-seam metal and lapped sheets work at very low slopes because
their seams are raised/water-bridged. When the pitch drops, add classes, not hope.

### 2.3 Battens, counter-battens and tiling geometry

- Load-path stack (warm→cold in timber): rafters → **counter-battens (Konterlattung)** along
  rafters forming the ventilation gap → **cross battens (Querlattung)** at the tile gauge →
  covering. The plane change creates the drainage + drying cavity for anything that gets past
  the tiles.
- **Rafter spacing ← batten spacing ← tile length minus overlap** - the covering module drives
  the whole timber grid (purlin/rafter logic: rafter spacing is set by lath spacing, which is
  set by tile format).
- Plates/sheets on linear supports: joints must sit on supports - transverse offset v = support
  spacing a (or a multiple); point/asymmetric loads lift unsupported edges → support or fix
  edges against sliding/uplift.
- Lap direction always downhill; head laps staggered course by course.
- Ventilated-cavity logic applies to the whole pitched assembly: the cavity is the drainage +
  evaporation zone; ventilation effectiveness grows with inclination from vertical (a nearly
  flat pitched roof ventilates worst - raise the pitch or seal the construction properly).

### 2.4 Eaves, verge, ridge, valley, penetrations

Universal detailing rules (product numbers per Fachregeln - planning values):

| Junction | Rule | Typical failure if wrong |
|---|---|---|
| Eaves (Traufe) | water enters gutter, not behind it: gutter front edge below the extended roof plane; ventilated eaves strip keeps the cavity intake open; drip directs water clear of the fascia | wind-driven rain behind the fascia; blocked ventilation inlet |
| Verge (Ort) | closed (dry-verge or bedded undercloak); battens run to edge; no open end-grain at the border | snow and rain sucked under the verge by wind |
| Ridge (First) | raised/ventilated ridge keeps the top of the ventilation cavity free; hip/ridge tiles mechanically fixed and sealed | unvented ridge = condensation under the crown |
| Valley (Kehle) | highest-volume flow path: wide lined valley (min ~300 mm each side of centreline **[VERIFY]**), seams away from the valley floor, snow/debris catch handled by clearance | ice dam / debris dam; lined valley bridged by tile coursing |
| Roof-to-wall abutment | step-flashing pieces per course; counter-flashing chased in above, lapping the base; joints sealed but sealant never the only barrier | water driven behind a single continuous strip |
| Penetrations (vents, flues, PV cabling) | collar/clamped flashing bonded to the underlay + mechanically closed curb ≥ ~150 mm above the covering **[VERIFY]**; flues: soot-fire + clearance rules (chimney norms) | sealant-only collar ages and cracks (5-10 a life) |
| Skylight / roof window | kerbed flashing integrated into the underlay; see §11.1 | flat-mounted light dome on a slope = ponding collar |
| Gable/head wall | tie the gable to the structure (wind bracing); flashing behind cladding onto the underlay | cracked render at the slope junction |

Airtightness note: on warm pitched roofs the **Dampfbremse/Luftdichungsebene is one continuous
taped layer** - every penetration above it is also an airtightness penetration (§12.5).

### 2.5 Warm pitched roof without ventilation (modern)

Thick insulation lifts the dew point safely only if the build-up is engineered: the external
membrane must be **rain-impermeable yet sufficiently vapour-open** (relative to the internal
retarder, §12.3 sd-ratio), and condensation must be verified, not assumed. Modern warm steep
roofs often have no ventilation under the sarking because insulation depth blocks the gap -
then the membrane doubles as weather backup and the drying margin shrinks. Verify per DIN
4108-3 deemed-to-satisfy lists, else transient model.

### 2.6 Snow: loads, slide, snow guards

**Characteristic ground snow load** sk: zoning map + altitude correction
`sk = sk1 · [1 + (A − A0)/350]²` for altitude A above the zone base altitude A0 (zone
boundaries/map values **[VERIFY]** - maps were not machine-readable in the source); above
1500 m the authority sets sk; northern lowland regions: exceptional snow loads (multiples of
sk) possible → treat as **exceptional action** there. Design snow load on roof:
**sd = cc · cf · sk**; shape coefficient μ1 = 1.0 up to 10°, 0.8 for 10°-45°, decreasing to 0
above 60° (sliding off) **[VERIFY - source values garbled]**.

Digest-checked numbers:
- **Roof imposed load category H (not normally accessible): single-person maintenance load
  1.0 kN point; the small area load is NOT superimposed with snow.** No superposition of roof
  walk load and snow - design the two actions separately.
- Snow density for **slip loads 2.0 kN/m³** (slid/compacted); unit weight ≈ 3.0 kN/m³ used as
  design value for overhang/drift surcharge in the worked tables **[VERIFY]**.
- **Slide (Rutschschnee):** a steep upper roof discharging onto a lower flat roof creates a
  drift wedge + slip load. Worked example (terraced houses beside flat-roof garages): slide
  contribution S = 50 % of the max total snow load on the adjacent upper roof; drift
  coefficient μ2 = μw + μs, capped per the snow code (example capped at 2.4). Model the drop
  height (roof step) and lower-roof width when placing dormers, setbacks and garage roofs.
- **Slip restraint:** where sliding snow must be held (above entrances, neighbouring property,
  ground occupied by people): snow guards (Schneefanggitter) at the eaves; with a parapet or
  snow guard the slip-reduction credit is void (cf ≥ 1.0). Guard load scales with
  `F = μmax · sk · A …` (retained sliding mass per row) - exact formula stripped in the source
  **[VERIFY per snow code + product approval]**. Fix guards into rafters/purlins, never into
  battens.
- **Flugschnee:** wind drives snow under overlaps at any pitch - one of the reasons the second
  underlay stage exists (§2.2), independent of rain.
- Combination factors: snow ψ0 = 0.5, ψ2 = 0 (≤ 1000 m); above 1000 m ψ0 = 0.7 / ψ2 = 0.2;
  **roofs (category H): ψ = 0/0/0** - never treat roof imposed load as quasi-permanent.

### 2.7 Dead loads of coverings (planning values, incl. battens, excl. rafters)

kN/m²; add **+0.1** where bedded/mortared (vermörtelt). Use for structural pre-sizing and
build-up weight budgets; confirm against the actual product system.

| Covering | gk kN/m² | Covering | gk kN/m² |
|---|---|---|---|
| concrete/clay flat tiles ≤10/m² | 0.50 | slate old-German/template, single on 24 mm boarding | 0.50 |
| concrete/clay tiles >10/m² | 0.55 | slate double coverage | 0.60 |
| deep-profile concrete/clay tiles | 0.60-0.65 | fibre cement, German bond on boarding | 0.40 |
| beaver-tail tiles (Spießdach) | 0.60 | fibre cement short-wave/corrugated | 0.20-0.24 |
| beaver-tail double/crown bond | 0.75 | TiZn/copper double standing seam + boarding | 0.35 |
| folded/reform tiles | 0.55 | steel pan tiles on battens | 0.15 |
| monk/nun tiles, mortared | 0.90 | steel pan + cover strip/boarding | 0.30 |
| Strangfalzziegel | 0.60 | galvanised corrugated steel | 0.25 |
| small-format/special beaver | 0.95 | aluminium sheet 0.7 + boarding | 0.25 |
| Kremp/hollow pan tiles | 0.45-0.55 | alu corrugated/trapezoidal/clamped rib | 0.05 |
| reed/thatch roof | 0.70 | wooden shingle | 0.25 |
| profiled glass single/double | 0.27 / 0.54 | plastic corrugated 1 mm / 3 mm | 0.03 / 0.08 |

Sealing/layer weights (flat roofs): polymer-bitumen welded sheet 0.07; glass-fibre-bitumen
sheet 0.03-0.05; loose bitumen sheet 0.01-0.04; vapour barrier ~0.07; 1.5 mm plastic sheet
0.02; **gravel ballast 16/32 ≈ 1.0 kN/m² per 5 cm** (≈ 20 kN/m³). Insulation bulk: foam
plastics ~0.01 kN/m² per cm, mineral wool ~0.01, wood-fibre boards ~0.02-0.03, cement-bonded
wood wool ~0.04-0.05.

### 2.8 Wind-driven rain exposure (whole envelope, incl. roof)

DIN 4108-3 exposure groups by mean annual rainfall and site exposure:
**I gering** < 600 mm/yr (or specially sheltered in a wetter region); **II mittel** 600-800 mm
(or exposed in a low-rain region; sheltered in a high-rain region); **III stark** > 800 mm, or
coastal/mountain wind exposure with less rain. Driven rain arrives with ~10× the kinetic
energy of calm rain (drop velocity 5.4 → 17 m/s) - this is why low-pitch and flat junctions
get backup stages and why joint design (§3.3) matters more than material choice.
Windows/doors: rain tightness classes EN 12208 (50 → 600 Pa and above); select per DIN 18055
from wind zone + terrain + geometry, not from rainfall alone.

---

## Section 3: Flat Roofs - Governing Rules

### 3.1 The four functions of a flat-roof build-up

Draw the stack bottom-up; every layer has exactly one job:

1. **Substrate** (RC slab, timber deck, trapezoidal sheet) - structure + falls if built in.
2. **Vapour control** - on heated buildings: a **full vapour barrier (Dampfsperre) below the
   insulation is mandatory** in warm-roof build-ups, because the top skin is necessarily
   vapour-tight. Bituminous or synthetic barriers (EN 13970 class family); s_d classes:
   s_d ≤ 0.5 m diffusion-open / ≤ 2 m resisting / 10-100 m strong retarder / 100-400 m
   barrier / ≥ 1500 m vapour-tight.
3. **Thermal insulation** - must be protected from wind (infiltration strips away the
   still-air benefit), moisture, UV and impact; compression/application class per DIN
   4108-10: codes **DAD/DAA/DUK** (flat-roof uses; DUK = inverted roof), load classes
   dk/dg/dm/dh/ds/dx (**dh = used roofs, terraces, PV**), water classes wk/wf/wd
   (**wd = perimeter & inverted**), tensile zk/zg/zh (**zh = under bonded sealing**).
4. **Waterproofing + protection** - continuous, laid to falls, dressed up all upstands; then
   ballast, fleece, paving or vegetation so the membrane never *is* the wearing surface.

**Staging principle (Stufigkeit):** einstufig (one barrier - the flat-roof sealing) vs
mehrstufig (a braking stage + a sealing stage - pitched covering + underlay). A flat roof has
one stage → it gains robustness from **detailing quality and protection**, not from extra
stages; multi-ply laminated sealing adds material redundancy instead.

### 3.2 Falls and drainage geometry

- **Minimum design fall 2 %** for dependable drainage at normal surface roughness - aim
  higher. The trade flat-roof rules permit smaller/zero falls only with compensating
  measures **[VERIFY current guideline]**.
- Timber flat roofs (state-of-the-art rule): **fall ≥ 3 %** (§12.3).
- Create falls in the **substrate, a screed, or a tapered insulation layer** - never by
  shimming the membrane; the membrane bridges slope, it does not create it.
- Flow paths short and orthogonal to outlets; no back-falls; outlets at true low points.
  Build-up thickness at the high point grows with flow-path length → **split drainage zones
  (shallow valleys, more outlets) before thickening the stack.**
- Tapered insulation (Gefälledämmung) is a legitimate alternative to a screed: lighter and it
  keeps the insulation plane continuous; its U-value is computed differently (§12.2 wedge
  rule) and it saves roughly a thick screed's dead load (a 10 cm average screed ≈ 2 kN/m²).

### 3.3 Joints, upstands and terminations (Schlussarten applied)

The joint vocabulary of construction theory, at the roof:

- **Raise the joint out of the water-carrying plane**: fold edges up (standing seam,
  Aufkantung; at upstands this is the "floating/loose joint" principle). A joint gap above the
  draining surface is dramatically less wetted, and differential movement is absorbed by
  bending the compliant upstand legs instead of tearing a bond.
- **Butt/press joints are never watertight**; narrow deep joints actively *wick*
  (Kapillarfuge - capillary suction is strongest in gaps thinner than the water meniscus with
  hydrophilic faces). Closed joints seal by exactly three principles: (1) material bond
  (weld/glue - seals like the material but blocks movement), (2) elastic sealant in
  **two-sided flank adhesion** with a backing rod (never 3-sided adhesion; hourglass shape),
  (3) compression gasket (pre-compressed profile, no chemical bond needed).
- **Upstands / parapet terminations (Aufkantung, Attika):** the sealing runs continuously from
  the field, over a rounded **fillet (Kehlenausbildung/Ausrundung, ≈ 50 mm radius)**, up the
  vertical, terminating in a chase + clamping bar with sealant closure - the mechanical fixing
  is the primary restraint, sealant secondary. Numerical heights are set by DIN 18531-x and
  the trade flat-roof rules; conventional planning values: **≥ 150 mm above the finished roof
  surface; ≥ 250 mm above any anticipated ponding/retention water level; raised above a door
  threshold** **[VERIFY against current DIN 18531-x]**.
- **Negative corners are singularities** - chamfer/fillet every horizontal-to-vertical
  transition (insulation wedges at upstands); **never a field seam across an internal corner.**
- Perimeter free edges: drip edge / gravel stop set flush or below the membrane plane; a
  raised lip dams water at the weakest strip of the roof.
- Movement/expansion joints: penetrate the full build-up over structural joints; bellows loop
  between raised twin curbs - flat-taped joints tear on the first thermal cycle.
- **Never stack layer joints:** stagger vapour-barrier, insulation and sheet laps; multi-ply
  bituminous laps are fully bonded and offset ply by ply; butt-jointed insulation boards get
  rebate/staggered joints.
- Copings/cover plates must shed water: slope their edges, drip grooves both faces, and their
  joints are designed sealed movement joints (backer rod), never open butt joints; the coping
  DPC sits above the wall and laps the upstand termination as separate, coordinated layers.

### 3.4 Vapour and thermal design of flat roofs (rules before numbers)

- Design law: diffusion resistance **high inside, low outside**; the dew point must fall
  *inside the insulation* toward the cold side, where condensate either evaporates in summer
  or remains minor.
- Failure pattern to design against: warm + humid indoor air → condensation in the cold outer
  insulation → insulation gets wet (λ of water ≈ 0.6 vs still air 0.025 - about 24× →
  near-instant function loss), then rot, then frost damage. The better the insulation, the
  colder any bridge tip - risk grows with U-improvement.
- Flat roof on a deck = **always a full vapour barrier under the insulation** (§3.1): the top
  skin is necessarily vapour-tight and there is no ventilation option. Ventilated pitched
  roofs may instead dry outward - that route does not exist above a sealed flat roof.
- Components with waterproofing: compute thermal resistance **only for layers on the dry side**
  of the membrane; wet-side layers are normally neglected (§12.1).

---

## Section 4: Warm Roof Build-Up (Konventionelles Warmdach)

Classical layup bottom→up (mineral substrate, bituminous multi-ply), functions annotated:

| # | Layer (DE) | Function | Typical make | Weight |
|---|---|---|---|---|
| 1 | bewehrte Decke mit Gefälle | structure + falls | RC cast to fall or screeded | slab |
| 2 | Grundierung | bonding key/priming | bitumen primer | ~0 |
| 3 | **Dampfsperre** | stops indoor vapour reaching the insulation | bitumen/synthetic barrier, laps sealed | 0.07 |
| 4 | Trenn-/Dampfdruckausgleichsschicht | perforated glass-fleece, spot-bonded: equalises vapour pressure, decouples sealing from substrate movement | 1 layer | 0.03 |
| 5 | Gefälleschicht | design fall ≥ 2 % | tapered insulation or lightweight screed | see §2.7 |
| 6 | Dämmung | thermal function | EPS-T/PIR/mineral wool λ ≈ 0.035; classes DAD, zh/dg as used | ~0.01/cm |
| 7 | (Teilverhaftung) | partial bonding lets the stack relax over the deck | - | - |
| 8 | **Abdichtung 2-3-lagig** | the waterproofing itself: polymer-bitumen sheets fully welded, laps offset ply by ply (single-ply FPO/PVC/EPDM also possible, §6) | 2 × 3-4 mm or 1.5-2 mm single-ply | 0.07-0.15 |
| 9 | Schutzschicht | UV, mechanical, wind hold, fire shielding | **gravel 16/32 ≈ 50 mm**, paving, or vegetation | 1.0 per 5 cm gravel |

Notes:
- The horizontal plane prevents sliding → insulation can be thick with **no anchor
  penetrations** (the ideal for the sealed box); that freedom is exactly why the outer skin is
  vapour-tight and the barrier mandatory.
- Gravel ballast protects against UV and mechanical attack and weights the sheets in wind
  suction zones; it is *not* a drainage layer - falls must already exist beneath it.
- Accessible variant (roof terrace): swap gravel for separation fleece + protection screed or
  pedestal pavers (§8). **Loose-laid protective layers beat bonded skins** for drainage and
  thermal movement; a bonded topping cracks with the deck below and telegraphs every slab
  crack into the wear surface.
- On a single-leaf uninsulated flat deck (industrial, low-humidity use only), condensation
  under the vapour-tight skin must be allowed to dry **inward** - the only available route;
  do not replicate this in a dwelling.

---

## Section 5: Inverted / Protected-Membrane Roof (Umkehrdach)

Insulation **above** the waterproofing. This removes the dilemma of sealing a moisture-
sensitive insulation from a vapour-tight top: the waterproofing *is* the vapour barrier and
lives shielded from UV, thermal shock and foot traffic.

Layup top→down:

| # | Layer | Requirement |
|---|---|---|
| 1 | Kiesschüttung / paving / vegetation | ballast holds insulation against wind uplift and against buoyancy from retained water; insulation class dh if loaded/used |
| 2 | Filtervlies | silt protection - keeps fines out of the board joints |
| 3 | **XPS, gefällegt (gradient-cut), lap-jointed** | closed-cell water-insensitive only: XPS (EN 13164, DIN 4108-10 **DUK**, class **wd**) or foam glass (CG); **EPS/PIR/mineral wool are not valid above the sealing**; joints staggered so water cannot jet to the membrane |
| 4 | Schutz-/Trennvlies | protects the membrane from XPS abrasion |
| 5 | Abdichtung | the single continuous waterproofing = vapour barrier (§4 layer 8) |
| 6 | Entspannungs-/Trennlage | relaxation/separation over the substrate |
| 7 | gefälliger Untergrund | structure or screed to ≥ 2 % |

Rules:
- Free water percolating down to the membrane is **designed-in**: the insulation stays wet at
  its edges - hence the run-off-cooling **U surcharge ΔU (§12.1)** and a membrane rated for
  permanent standing water.
- XPS boards can float; the system depends on ballast and edge restraint - edge rows at
  upstands need counter-pressure/termination.
- **Lightweight roofs** (areal mass < 250 kg/m², e.g. timber decks): require R ≥ 0.15
  (m²K)/W **below** the sealing so the barrier's warm-side surface stays above the dew risk;
  ΔU = 0 only for approved systems with a water-draining separation layer.

---

## Section 6: Waterproofing Materials & Layer Logic

### 6.1 Norm frame (supersession flagged)

- **DIN 18531-18535** is the current waterproofing series; the legacy **DIN 18195 parts are
  withdrawn - cite 1853x in new specs [VERIFY part-by-part applicability]**. The old load-case
  vocabulary (Bodenfeuchte / stauendes Sickerwasser / drückendes Wasser) survives conceptually
  inside DIN 18533 (§10).
- Product norms seen in the digested data: EN 13967 (plastic/rubber damp-proof and tanking
  sheets), EN 13970 (bituminous vapour control sheets), EN 15812/EN 15814 (polymer-modified
  bituminous thick coatings incl. crack-bridging classes), DIN 18540 (joint sealing with
  sealants). Per-product European approval/CE routes **[VERIFY per product]**.

### 6.2 System families

| System | Constitution | Where it wins | Watch out |
|---|---|---|---|
| bitumen multi-ply (2-3 layers, polymer-modified, torch/weld) | 0.07 kN/m² per sheet; fully bonded; offset laps | warm roofs; ply redundancy; crack bridging via staggered plies | hot work near vents/combustibles; **laps are the joints** - QC every seam; bitumen melts/flows on sun-exposed dark surfaces and embrittles under UV → protect it |
| single-ply synthetic (FPO/PVC ~1.5 mm; EPDM 1.2-2 mm) | loose-laid + ballasted, mechanically fixed, or fully bonded; welded seams | large simple areas; fast; PV-ready decks | seam welding QC; puncture protection under traffic; plasticiser migration (PVC) and bitumen-contact incompatibility with EPDM |
| liquid-applied (PMMA/PU/bitumen-polymer thick coat) | 1.5-4 mm with joint reinforcement fleece | complex geometry, many penetrations - seamless | substrate cure/moisture; dry-film-thickness QC; movement joints need bonded reinforcement strips |
| vapour barriers (Dampfsperre/-bremse) | bitumen/synthetic sheets, self-adhesive butyl; full barrier ≈ s_d ≥ 1500 m | continuous taped plane under insulation | punctures at fixings; lap and perimeter detailing; must survive the concrete/fixing phase |

### 6.3 Substrate and material rules (universal, digested principles)

- **Cracks open the door to every decay process.** Cracking is material-immanent in concrete
  and masonry and mostly harmless for load capacity - **but must be controlled in sealing
  layers**: separation/relaxation layers under bonded sheets; crack-bridging classes for
  coatings; shrinkage reinforcement to keep cracks fine and distributed.
- Differential movement of dissimilar layers (insulation vs masonry vs metal vs sealing) is
  the chronic cause of cracked renders and torn sealants - accommodate with soft layers,
  generous joint widths, primers; design joints to shed water; slope horizontal joints outward.
- Thermal movement: α concrete ≈ 10·10⁻⁶ 1/K, steel ≈ 12 (nearly compatible - the basis of
  RC); aluminium ≈ 200, steel λ ≈ 50-60 W/(m·K) vs insulation 0.035 → **any steel/aluminium
  fixing through insulation is an absolute thermal bridge and a condensation seed.** Use
  stainless (λ 17-30) or plastic connectors; concentrate unavoidable bridges into points,
  never lines.
- Elastic deformation restrained → constraint forces (Zwängungskräfte): either the detail
  allows movement (joints, loose folds, relaxation layers) or the construction resists the
  force. A membrane rigidly glued over a moving joint does both badly.
- Tolerances: plan adjustment zones (planned minus-dimensions, slotted fixings, coordination
  gaps); membranes cannot be reworked on site like brickwork - **tolerance planning is safety
  planning.**
- Bitumen-based materials melt/flow under sun on exposed dark roofs; protect (mineral
  surface, reflective coating, ballast, or bury it under the Umkehrdach stack).

---

## Section 7: Flat-Roof Drainage, Overflows and Rainwater Design

### 7.1 Layout rules

- Primary outlets: invert at the true low point, domed leaf guard, sized for the local design
  rainfall (short-duration intensity / IDF data; rational-type `Q = ψ · r(n) · A` per the
  DWA-A 118 principle - coefficients §7.2). **Never rely on a single outlet on any roof.**
- **Emergency (secondary) drainage is required on enclosed, parapeted roofs:** an overflow
  (parapet notch/scupper or second inverted drain with higher invert) that takes over when
  the primary is blocked, discharging somewhere **visible** - water weeping down the facade is
  the intended alarm to the owner. Balconies/loggias behind closed parapets: overflow opening
  **≥ 4 cm clear** (drainage practice). Minimum one overflow per enclosed drainage zone;
  keep the overflow invert below the threshold/upstand top.
- Internal drains: the stack passing through warm rooms must be **vapour-tightly insulated on
  the room side** to the top storey, else condensation runs down the outside of the pipe and
  wets ceilings that have nothing to do with rain.
- Gutters (Dachrinnen): fall ≥ 1 mm/m toward outlets (3-5 mm/m better); front edge set ~8 mm
  lower than the back so overflow leaves outward, not behind the facade; expansion allowance
  every ≤ 15 m (metal) / ≤ 12 m (plastic) → effectively one downpipe per 12-15 m gutter run;
  provide an overflow where blockage could flood an opening.
- Downpipes discharge to a splash pad or soakaway clear of the foundation; at the plinth use a
  robust foot (cast-iron/steel standpipe ≤ 1 m above grade - required in some Bundesländer).
  Never soak rainwater at the wall base (§10.4 plinth logic).
- External paving and planted ground fall **away** from the building at the plinth; keep
  splash-back off waterproofing upstand bases.

### 7.2 Runoff coefficients (planning means, DWA-type)

| Surface | ψ |
|---|---|
| pitched metal/glass/slate/fibre cement | 0.9-1.0 |
| pitched tile / bitumen sheet | 0.8-1.0 |
| flat ≤ 5°: metal/glass/fibre cement | 0.9-1.0 |
| flat: bitumen sheeting | 0.9 |
| flat: gravel ballast | 0.7 |
| **green roof, extensive (humus depth dependent)** | 0.3-0.5 |
| asphalt / jointless concrete paving | 0.9 |
| tight setts | 0.75 |
| open-joint setts | 0.5 |
| loose gravel / green strips | 0.3 |
| turf-gravel grids (Rasengitter) | 0.15 |
| infiltrating blocks/stone | 0.25 |

### 7.3 Ponding physics (universal)

- **100 mm of standing water = 0.98 kN/m² (~1.0 kN/m²).** The whole maintenance allowance of a
  "not normally accessible" roof (category H, 1.0 kN point load) is consumed by centimetres of
  trapped water - and deflection under water attracts more water (deflection → ponding → more
  deflection). Where flow paths are long and deck stiffness low, check the deck for ponding
  instability *before* accepting a nominal 2 % fall.
- Standing water > 48 h: biofilm growth, accelerated UV/thermal cycling of exposed sheeting,
  and - in cold seasons - **freeze-thaw cycles**: water→ice expansion is a spalling force in
  saturated porous material; ponded films at terminations destroy edges, coping joints and
  paving.
- Retention/attenuation roofs (§11.3) deliberately store water - then the structure must carry
  the retention depth as load and the sealing must tolerate permanent immersion; note the
  known conflict: the **drainage-based flat-roof design case cannot be satisfied with a
  throttled retention outlet** - reconcile the sponge-city intent with the flat-roof rules
  explicitly and document it **[VERIFY current rules]**.

---

## Section 8: Balconies, Loggias and Roof Terraces on Waterproofing

Same stack physics as flat roofs (§4/§5) with stricter use loads and details:

- **Imposed loads:** category **Z (balconies / roof terraces / loggias): qk = 4.0 kN/m²**
  (companion value 2.0 kN/m in the source table - line load for the parapet/railing zone
  **[VERIFY]**); parapet/partition line loads applied at ≤ 1.2 m height by use category:
  A, B1, H, F1-F4, T1, Z → 0.5 kN/m; B2/B3, C1-C4, D, E, FL, HC, T2 → 1.0 kN/m; C5, C6, T3 →
  2.0 kN/m - full magnitude in the fall direction, 50 % opposite (min 0.5). Sound protection
  over rooms below: impact sound limits apply to terrace build-ups (DIN 4109-1 rows "unter
  Terrassen/Loggien" - use the catalogue values **[VERIFY]**).
- Build-up: sealing → protection/separation fleece → **loose protective layer (raised paving on
  pedestals, or protection screed)** → wearing surface. The membrane is never the wearing
  surface; the drainage plane sits above the sealing with ≥ 2 % falls under the paving.
- **Point bearings are the killer:** pedestal feet, furniture legs and screen posts concentrate
  load onto the sealing. Spread the load (wide-base pedestals, load-spreading protection
  boards); note that anchoring pergolas/screens through the sealing punctures it - fix into
  upstand curbs or use ballasted frames; never raw-penetrate a finished terrace.
- Thresholds to terraces: prefer a drained threshold channel; the upstand below/behind a door
  must still clear any design water level (§3.3) **[VERIFY]**.
- **Balcony slabs are the canonical linear thermal bridge** (cantilever punched through the
  insulation plane). Remedies ladder (worst → best): wrap the whole cantilever in insulation;
  insulate partway along its length (lengthen the path); sever the section and reconnect
  through the insulation with minimal low-λ connectors (stainless/plastic balcony elements);
  give the cantilever its own support off the ground (no connection at all). Un-insulated
  concrete balconies additionally crack their waterproofing at the wall junction through
  restrained thermal movement - detail a movement joint with a reinforced membrane loop.
- Balcony/loggia walls (two-leaf zones): sealing protected and bonded to the structure,
  drainage + filter layers outside; continue the ground-contact package 30-50 cm above the
  finished paving (plinth logic §10.4).
- Open-joint paving over the membrane lets most rain through to the drainage plane - design
  the sealing for it (it is the second, hidden roof).

---

## Section 9: Wet Areas - Indoor Waterproofing (DIN 18534)

Indoor tanking under tile follows DIN 18534 (successor to the old 18195 wet-room part) with
water-resistance classes **W0-I (no direct splash) … W4-I (high pressure / hot water)**;
domestic shower zones sit mid-range **[VERIFY exact class map per DIN 18534-1/-3]**. Design
rules (digested trade practice):

| Item | Rule |
|---|---|
| rooms with floor drain (Nassräume) | at least a one-layer sheet or bonded composite system; **upstands ≥ 15 cm above the floor; ≥ 20 cm above water outlets / spray sources (shower head height band)** |
| bath without floor drain | not a Nassraum - the splash zone behind bath and basin is still sealed |
| sealing under tile | bonded waterproofing (liquid + embedded fleece, "Verbundabdichtung") with thin-set tile bonded through it is accepted; sheets need screed/board protection |
| falls to drain | 1 % (light use) / 2 % normal / 3 % heavy spray; drain ≥ 10 cm from the wall |
| penetrations | sealing flanges/collars at every pipe; reinforcement/bonding tapes in all corners and plane changes |
| drain connection | membrane **clamped into a bonding-flange drain** - a membrane that stops beside the drain is not waterproof |
| tile field sizes | ≤ 40 m² per field and side ≤ 8 m; movement joints over screed joints 8-10 mm wide, edge joints ≥ 5 mm - flexible sealant over backer rod, not grout |
| tile joints | ≤ 10 cm tiles: 1-3 mm; ≥ 10 cm tiles: 2-8 mm |
| floor tiles | abrasion class ≥ 2 (private); slip behaviour class R9 or better |
| grout cure before load | thick-bed 7-14 d; thin-bed 1-3 d |
| test | flood test before tiling: plug the drain, fill above the high point of the membrane, mark the level, hold 24 h, inspect the room below |

Sunken-slab bathroom sequence (where this build type is used): sealed sunken slab dressed up
all sides → **flood test #1** → plumbing with collared penetrations → **lightweight fill only**
(EPS/foam concrete/aircrete - never water-holding mineral fill under a sealed floor) → capping
screed to falls → **second waterproofing clamped to the drain** → flood test #2 → tile. Two
zones, two tests, two lines of defence; a leak into a saturated fill reservoir is permanent.

---

## Section 10: Below-Grade Waterproofing - White Tub and Black Tub

### 10.1 Load cases decide the system (DIN 18533 logic; old classes survive in practice)

| Ground-water condition | Where it occurs | Requirement |
|---|---|---|
| **Bodenfeuchte** (soil moisture, capillary) | permeable coarse soils (gravel/sand; water content 3-8 %) | simple tight coating/system |
| **Sickerwasser** (percolating/infiltrating) | intermittently wetted slopes above low-permeability layers | full waterproofing design |
| **Stauendes Sickerwasser** (perched water) | cohesive clays (water content 20-70 %), backing-up on low-k layers | full waterproofing, drained or tanked |
| **drückendes Wasser** (groundwater, hydrostatic) | below the design GW table; pressure from all directions + buoyancy | reinforced, protected waterproofing or WU design; uplift check |

Repairability below grade is near zero (you would have to excavate) → **double precautions are
the default** for habitable basements: combine systems (structure + applied tanking, or tanking
+ drained protection). Capillary rise must be cut by a cross-section seal or the wall kept
free of bridging.

### 10.2 Black tub (Schwarze Wanne / Außenhautabdichtung)

Tanking **between** the structural wall and a protective cast backup wall (Wandrücklage): the
sheet is embedded/pressed by the backup concrete → protected against point loads and
uncontrolled pressure change. Sequence: blinding concrete → protection/leveling layer → tanking
sheet (EN 13967 type, welded/bonded laps, dressed onto the footing) → slip/protection layer →
RC wall → inner backup wall cast smooth against the membrane; under-slab tanking bonded/lapped
into the wall sheeting **above footing level** - a continuous wrap. Drainage package outside
(soil → wall): filter fleece (silt block) → dimpled drainage board (channels water down,
relieves pressure, protects the sheet during backfill) → drainage pipe at the footing on a
falling gradient to soakaway/separator; free-draining granular backfill for ≥ 300 mm - never
packed clay directly against the sheeting.

### 10.3 White tub (Weiße Wanne - watertight concrete)

The **concrete itself** is the sealing element, uncoated. Conditions:
- dense, **crack-controlled** concrete with minimum wall thickness: fine distributed cracks are
  acceptable, wide ones are not (shrinkage reinforcement, low w/c, compaction, long wet
  curing); tolerated residual seepage must diffuse **inward** and be dried by ventilation -
  acceptable for low-humidity storage use, not for comfortable rooms without measures;
- **construction joints are the weak line: a waterstop (Dichtungsband) in every cold joint** -
  rebar continuity makes a cross-section seal impossible in concrete (unlike masonry);
- separation foil + blinding under the base slab; joint-form/waterstop systems per the
  relevant DIN (18197-type joint formwork) **[VERIFY current]**;
- explicit crack-width design values live in the current concrete/WU rules
  **[VERIFY - not recovered from the digested data]**.

### 10.4 Cross-section seal, plinth, rising damp

- **Querschnittsabdichtung** (horizontal seal cut in the bed joint at base level) blocks
  capillary rising damp **in masonry only**; in concrete walls substitute the joint
  waterstop / WU logic.
- Vertical continuity of the tanking train: overlap + bond wall sheet ↔ slab sheet ↔
  cross-section seal at floor level; the wall sealing runs down to the horizontal one at the
  footing - **continuity at the junction, not adjacency.** The wall-to-slab junction is the
  most common basement leak point.
- **Plinth (Sockel):** splash-back + dirt + mechanical damage + capillary reach = its own
  build-up: continue the ground-contact package **30-50 cm above finished ground**; dense/
  hydrophobic plinth band; stop external render above the seal line (bell-cast) so no mortar
  bridge; a correct seal still shows damp to ~300 mm if paving splashes back - keep a gravel
  margin or drip detail.
- Basement walls in unreinforced/simple masonry may run prescriptively (EN 1996-3 type
  envelope): clear height ≤ 2.60 m, t ≥ 200 mm, floor slab acting as diaphragm for earth
  pressure, qk ≤ 5 kN/m², no single load > 15 kN within 1.5 m, backfill height ≤ wall height,
  no rising ground surface, **no permanent water pressure, and no sliding plane through the
  waterproofing** - outside these limits: design it.
- Rising damp physics: fine capillaries pull hardest; salts + evaporation destroy the surface
  (efflorescence, spalling) above the wet front; the fix is a cut (seal) or drainage, never a
  decorative re-render over an active bridge.

---

## Section 11: Daylight Openings, PV, Green Roofs

### 11.1 Roof windows, light domes, glass roofs (Tageslicht)

- **U-value targets** (energy-regulation lineage EnEV → **GEG - verify current figures**):
  reference-building roof window 1.4 W/(m²K); existing-building retrofit caps roof window
  1.3-1.4 (1.9 in relaxed legacy rows); glass roof 2.0 (2.7); **domes/light bands ≈ 2.5-2.7**
  (non-residential GEG-type limits: skylights/glazed roofs 2.5 at ≥ 19 °C, 3.1 at 12-<19 °C);
  reference dome g-value 0.64. A dedicated **dome/light-band correction table exists in the
  numeric-tables literature (Tafel "Kuppeln/Lichtbänder") but its cells were not readable in
  the digested source - consult the table directly [VERIFY]**.
- Inclined glazing is a surface-moisture hot spot: worse U at the pane + stronger outward
  radiation → extra condensation at reveals. Optimise reveal geometry (sill), prefer external
  shading, keep panes small for shock ventilation, place the heater below the window, and
  **never put a bathtub under a roof window** (steam + cold glass = drip field).
- **Walk-on vs fragile - fall hazard:** fatal fall statistics single out missing protection at
  roofs and **light domes** (fragile covers). Maintenance routes need either walk-rated
  covers/grids over openings or planned restraint systems (anchor points, access routes) -
  design for safety in the model from the start, not as a site improvisation.
- Horizontal glazing/structural glass (atriums, walk-on lights): design per the structural
  glass rules (DIN 18008 series: impact categories, walk-on 1.5 kN point load, span/100
  deflection, residual-capacity constructive rules) - a glazing-engineer task; flag and
  verify per part **[VERIFY]**.

### 11.2 PV on the roof (loads, fire, integration)

- **Loads:** an array is permanent extra dead load on the roof structure (module + frame +
  ballast - feed the structural load case before sizing anything); snow **drifts against and
  piles under** elevated rows - the slide/drift logic of §2.6 applies at module rows, and the
  slip-restraint question ("who is below?") must be re-answered with the array in place;
  maintenance access must not be assumed onto membranes - walkway pads/pedestals.
- **Insulation class:** under a loaded terrace/PV deck use DIN 4108-10 class **dh** (used
  roofs/terraces/PV) - not a board chosen by happenstance.
- **Fire (qualified/hard roofing regime, harte Bedachung - DIN 4102-7 test lineage, current
  classification per EN 13501-5 [VERIFY]):** where the LBO/B-Plan demands a hard roof
  covering, distances apply for soft coverings (order: ≥ 12 m to the boundary, reduced for
  minor buildings/garages per the tables **[VERIFY per Land]**); **PV: ≥ 0.5 m non-combustible
  band at array edges/ridge; combustible build-ups ≥ 1.25 m from the party wall (unless the
  wall rises 0.3 m above the roof); combustible lights/PV on otherwise-qualified roofs only
  with no ignition risk or shielding; green roofs under the same proviso.**
- **BIPV used as the roof covering itself (no lap):** then rain tightness of the *joints* must
  be proven by product testing under realistic driven-rain simulation - BIPV is not exempt
  from §2.1/§2.2 logic; below the system's standard pitch the underlay-class rule still runs.
- **Planning context (dated 2024/25 - verify):** federal build-out targets put at least half
  of new PV capacity on roofs; some Länder mandate PV on new non-residential roofs (> ~50 m²)
  with residential "Soll" rules arriving; tenant-electricity (Mieterstrom) makes roofs revenue
  space; PV and extensive greening are compatible (biodiversity interplay). If the roof is
  leased to an operator, the owner still prepares structure, membrane condition, statics and
  fall protection.
- Never raw-penetrate a finished waterproofing for mounts: curb-flash or ballast only; plan
  cable penetrations as collared/flanged details *before* the sealing date.

### 11.3 Green / retention roofs (Gründach)

- Build-up: sealing → root protection where the plant layer attacks it (root-resistant sheet or
  protected system) → separation fleece → drainage/storage profile (dimple mat, expanded clay,
  pumice) → filter fleece → substrate (extensive ≈ 80-200 mm; intensive = §8 terrace rules +
  tree restraint). Saturated substrate + retained water adds ~1.0+ kN/m² per 10 cm of wet
  substrate - **retention depth goes into the load case, not into the plant spec.**
- Runoff benefit: ψ drops to 0.3-0.5 (§7.2); but see the design-case conflict of §7.3 -
  document throttle vs standard drainage intent explicitly.
- Falls ≥ 2 % under the layer (drainage must work through the profile); anti-slide measures
  on steeper slopes **[VERIFY]**; upstands per §3.3 with the substrate kept below the sealing
  termination line; perimeters and outlets kept clear of granules.

---

## Section 12: Building-Physics Design of Roofs - Methods and Worked Examples

### 12.1 U-value rules for roof build-ups

- R = d/λ per layer; U = 1/(Rsi + ΣR + Rse); heat-flow-up roof: Rsi = 0.10, Rse = 0.04
  (m²K)/W (ISO 6946); DIN 4108 hygric/mould verification instead uses Rsi = 0.25.
- Inhomogeneous layers (rafters in a Gefach): two-bound ISO 6946 method - upper bound =
  parallel-flow area-weighted, lower bound = series with isothermal-line layer resistance;
  take the mean of the bounds. Air-gap and fastener corrections: ΔU for poorly contacted
  single layers (+0.01 level / +0.04 poor contact); fastener penetration correction χ per ISO
  10211 or the approximate α = 0.8 rule (skip if λ_f < 1.0; forbidden when both ends are
  metal-plated).
- **Membrane rule:** layers on the wet side of the sealing do not count (§3.4).
- **Inverted-roof surcharge** (cooling by run-off water under the insulation, DIN 4108-2
  lineage):

| Ratio of room-side (below-membrane) R to total R | ΔU W/(m²K) |
|---|---|
| < 10 % | +0.05 |
| 10-50 % | +0.03 |
| > 50 % | 0 |

  ΔU = 0 also for approved systems with water-draining separation layer; surcharge counts in
  the heating case; single XPS layer, rebate joints, offset layout per approval.
- **Minimum thermal protection** (Mindestwärmeschutz, DIN 4108-2): roof R_min = **1.75
  (m²K)/W in the field (Gefach)** and ≥ **1.0 overall** for inhomogeneous build-ups; surface
  mould criterion fRsi ≥ 0.7 (θsi,min = 12.6 °C at 20/-5 °C standard climate).
- **Energy-regulation targets (EnEV lineage → GEG, verify current):** reference-building roof/
  top-floor ceiling against outside U = 0.20 (walls/ceilings 0.28); existing-building caps:
  pitched roof/top-floor 0.24 (0.35 relaxed row); **flat roof 0.20 when the waterproofing is
  renewed (0.24/0.35 otherwise)**; non-residential mean U 0.28 (0.50 at 12-<19 °C); extensions
  allowed 1.2× (residential) / 1.25× (non-residential) of new-build maxima; ≤ 50 m² or ≤ 10 %
  of a component group → first-installation values suffice. Thermal-bridge flat surcharge
  ΔU_WB: 0.10 default; 0.05/0.03 with Beiblatt-2 category A/B equivalence; 0.15 with internal
  insulation on embedded solid floors.

### 12.2 Worked example - tapered (wedge) insulation layer U

Flat-roof stack with a **Gefälledämmung wedge 0-40 mm, λ = 0.035 W/(m·K)**, above a base whose
total resistance (without the wedge) is R0 = 5.058 (m²K)/W from the two-bound method:

- wedge resistance at maximum thickness: R2 = 0.040/0.035 = **1.143 (m²K)/W**;
- **tapered-layer rule: U = (1/R2) · ln(1 + R2/R0)** = (1/1.143) · ln(1 + 1.143/5.058)
  = **U ≈ 0.18 W/(m²K)**.

Lesson: a wedge layer is worth far more than its *average* thickness suggests (logarithmic
thickness averaging), which is why tapered insulation often beats screed on both U-value and
dead load - and why the 0 mm edge of a wedge must still be treated as a real zone in detailing
(barrier continuity, no cold strip at the outlet).

### 12.3 Vapour design of pitched roofs - s_d rules (DIN 4108-3)

**Roof s_d-ratio rule** (required internal retarder s_d,i vs external s_d,e above the
insulation):

| external s_d,e | required internal s_d,i |
|---|---|
| ≤ 0.1 m | ≥ 1.0 m |
| ≤ 0.3 m | ≥ 2.0 m |
| 0.3-2.0 m | ≥ 6 · s_d,e |
| > 2.0 m | ≥ 6 · s_d,e (valid only if no wood/wood-based layer sits between the two functional layers) |

Deemed-to-satisfy pitched cases (no Glaser proof; DIN 4108-2 + 4108-7 compliance still
required; residential climate ≤ 20 °C, no humidification):
- **ventilated roofs ≥ 5°:** ventilation opening 0.05 % of the area, min **50 cm²/m** at eaves
  AND ridge (for sealed/sarking-backed layers: 0.2 %, min **200 cm²/m**); gap depth ≥ 2 cm;
  s_d,i ≥ 2 m; layers below the retarder ≤ 20 % of total R (dew point stays in the insulation);
- vented but < 5°: batten runs ≤ 10 m; free area ≥ 2 ‰ (≥ 200 cm²/m); gap height ≥ 2 ‰
  (≥ 5 cm);
- **non-ventilated (warm) roofs:** s_d pair rule above; above-rafter PU/PF boards:
  s_d,e ≤ 0.5, s_d,i 0.1-10 m, R-limits: mineral wool ≤ 5.2 / wood-fibre ≤ 4.0 (m²K)/W;
- vapour-tight deck elements (s_d ≥ 1500 m) over wood-based underlays ≤ 25 (absorption class
  of the covering ≥ 0.6, medium/dark colour) **[VERIFY row reading]**;
- retrofit: humidity-adaptive membranes (s_d moist ≤ 0.5-1 m; dry 2-10, or ≥ 4).

**Timber flat roofs - state-of-the-art rules (post-damage practice):** 1) fall ≥ 3 %;
2) dark, unshaded membrane (solar heating drives the summer drying reserve); 3) **no topping**
(ballast, green roof, deck) over the build-up; 4) smart moisture-variable vapour control
layer; 5) no uncontrolled cavities on the cold side of the insulation; 6) verified airtightness;
7) initial moisture limits: wood-based panels u ≤ 12 ± 3 M-%, solid timber ≤ 15 ± 3 M-%.
Flat roofs *with* toppings: put the insulation directly under the top layer so condensate
cannot form in statically relevant layers below. The drying reserve (250 g/m²·a) is customary
but its adequacy is research-questioned - assess thick stacks transiently (§12.4).

### 12.4 Worked examples - Glaser / period balance (DIN 4108-3)

Climate constants: condensation period Dec-Feb = 2160 h: θi 20 °C / 50 % → p_i = 1168 Pa;
θe −5 °C / 80 % → p_e = 321 Pa. Evaporation period Jun-Aug = 2160 h: p_i = p_e = 1200 Pa;
saturation pressure at the condensation plane 1700 Pa - **2000 Pa for roofs** (solar heating
of the dark outer surface). Limits: annual condensate M_c ≤ **0.5 kg/(m²·a)** where adjacent
layers are water-repellent/impervious (1.0 for sucking layers); drying reserve ≥ **250
g/(m²·a) roofs / 100 walls**; moisture increase Δu ≤ **5 M-% solid wood / 3 M-% wood-based
panels**. s_d = μ·d per layer; the vapour-pressure line scaled on cumulative s_d may not
cross the saturation line without a mass balance.

**Example A - warm flat roof, bitumen double skin (the dark-membrane drying case):**
gypsum + RC 180 (μ70) + butyl barrier s_d 6.0 + EPS 160 (μ20 → s_d 3.2) + 2-ply bitumen
(μ2·10⁴ → s_d 120): Σs_d = 143.6 m; R_T = 5.72 → **U = 0.175**. Condensation plane between
barrier and EPS (p_s ≈ 407 Pa): diffusion inflow minus outflow → **M_c ≈ 49 g/(m²·a) ≤ 500 ✓**.
Drying: dark roof surface heats in summer → saturation pressure at the plane taken as
2000 Pa → **M_ev ≈ 63 g/(m²·a) ≥ M_c ✓ → passes.** The absorbed solar heat that suppresses
the winter risk *is* the heat that powers the summer evaporation reserve - exactly why §12.3
demands a dark, unshaded membrane on timber warm flat roofs (and why shading it with PV or a
deck changes the physics and must be re-proved).

**Example B - RC warm flat roof, single barrier (simplified):** RC 180 (μ70) + barrier 2 mm
(μ10⁴) + EPS 140 (μ30) + membrane 6 mm (μ10⁵): Σs_d = 636.8 m → M_c = 0.029 kg/m² ≤ 0.5;
M_ev = 0.033 > M_c → **OK.** The barrier's huge s_d keeps the diffusion flow (and thus any
condensate) tiny - the proof is trivial *because the barrier was installed*; remove it and
the same stack fails at the EPS/skin interface.

**Failure mirror (same physics, roof-adjacent wall case):** timber-frame bay with diffusive
outer layers and only s_d,i ≈ 0.45-0.95 m total → M_c = 1287 g/(m²·a) > 750 (the 3 M-%
wood-panel cap converted to mass) - **the drying surplus could not rescue it; the condensate
cap governs.** Fix: raise s_d,i to the required 0.91 m minus existing → ≈ 0.46 m (e.g. 30 mm
OSB, μ30). Do not repeat this pattern under a vapour-tight top skin without ventilation.

- Glaser limits: stationary, no construction moisture, summer reverse diffusion
  underrepresented → for critical builds (timber flat roofs, internal insulation, PV-shaded
  dark membranes) run transient coupled heat-moisture simulation (DIN EN ISO 15026;
  WUFI/DELPHIN-class tools; DWD test-reference-year climate data). Flag any roof where the
  stationary proof is marginal.

### 12.5 Airtightness layer continuity

- Legal: heat-transferring envelope incl. joints **permanently air-impermeable per recognised
  rules of technique = DIN 4108-7** (EnEV §6(1) lineage ≈ GEG §26). Blower-door at 50 Pa
  (Verfahren B, envelope test): **n50 ≤ 3.0 h⁻¹** without mechanical ventilation,
  **≤ 1.5 h⁻¹** with; for air volumes > 1500 m³: envelope-related q_E50 ≤ 4.5 /
  2.5 m³/(h·m² envelope); DIN 4108-7 recommends n50 ≤ 1.0 when MVHR exists; Passivhaus
  ≤ 0.6. **Meeting n50 does not replace the qualitative layer rules - which dominate:**
  continuous, jointed/overlapped, taped, protected.
- Roof specifics: the Dampfbremse usually **doubles as the Luftdichungsebene** - one continuous
  plane: taped laps; sealed around every penetration (pipes, cables, lights); protected from
  damage by a second insulation layer inside the services plane (services crammed into the
  airtight layer at socket boxes = the classic leak); transferred at wall junctions and
  upstands by bonded/clamped details, never by adjacency.
- Convection carries far more water per hour than diffusion through the same gap - one open
  joint behind a roof light can wet a whole insulation bay (§12.4 failure mirror); wind
  infiltration also strips the still-air value out of any cavity it can circulate through.
- Draw the airtight layer as its own object/line in plans and the FreeCAD model so no trade
  "routes a duct through it" on site, and commission the blower-door test as a hold point
  before the sealing date.

---

## Section 13: Durability, Maintenance & Inspection

**Ageing agents (digested):** UV embrittles bitumen and sealants and greys wood (lignin loss -
wood kept under an eave stays near-intact; overlaps/eaves are the protection); PVC plasticiser
migration; bitumen melts/flows on sun-exposed dark roofs; galvanic/contact corrosion - in a
dissimilar-metal pair the **baser** metal dies (fasteners nobler than the part, or break the
contact; galvanising works because zinc is sacrificial); carbonation + chlorides destroy the
alkaline passivation → rebar rusts (expansive) → cover spalls in layers (cover today 30-40 mm,
was 25); frost spalls only saturated fine-pored material (dense, air-entrained, or open
granular with room for ice survives); water→ice expansion is a spalling force at every
saturated termination; rot fungi need wood moisture > ~18-20 %.

**Constructive protection ladder (works before chemicals):** no water-holding geometries
(concave traps, upward-facing end grain, narrow capillary slits); slopes; overhangs; raise
timber ≥ 30 cm above splash zones; ventilate behind cladding; protect end grain (caps,
bevels); isolate timber from masonry's construction moisture with a waterproof gasket line;
never trap moisture inside by an external vapour barrier (diffusion design!). Keep timber at
15-18 % service moisture or fully saturated - never the intermediate damp zone.

**Component lives vs building life:** buildings run 50-100+ a; sealings, sealants, exposed
sheetings and wearing layers are shorter renewal cycles. Design so the **consumable**
(sealant, wearing surface) is accessible and the **buried layer** (air/water barrier, sealing)
is protected and redundant. Up to 80-85 % of lifecycle cost arises after construction - the
maintenance access you detail now is the cheapest inspection you will ever buy.

**O&M schedule to hand over:**
- before/after each heavy-rain and snowmelt season: clear outlets, gutters, scuppers,
  overflows; verify the emergency overflow is unobstructed;
- annually: inspect flashings, coping joints, upstands, sealants; re-seal adhesion loss;
- every 5 years: renew exposed sealants as a matter of course (5-10 a lifespan); every 5-8:
  re-coat exposed membranes;
- after storms, hail or nearby fires (ember load): special inspection (damage categories
  include pitched roofs - missing tiles, leaky chimneys/roof windows, blocked gutters; flat
  roofs - **ponding, ice, wet insulation, added ballast from PV/greening, deflection,
  missing emergency drainage**);
- snow guards, fall-protection anchors: check fixings/corrosion on a cycle;
- never: drill, fix or place new plant on a finished roof without a flashed curb or ballast
  base.

---

## Section 14: Failure Patterns - Ranked, and How to Detail Against Them

Walk this list top-down in every design review. Mechanisms are digested physics;
counter-measures point back to the rules above.

| Rank | Pattern | Mechanism | Counter-measure (→ section) |
|---|---|---|---|
| 1 | **Junction/termination leak** (flashings, upstands, penetrations) | the discontinuity in an otherwise continuous surface; sealant-only versions age 5-10 a and crack | mechanical termination + material bond; sealant secondary only; no field seam at a corner (§2.4, §3.3) |
| 2 | **Ponding / inadequate fall** | water stands > 48 h; deflection attracts more water (0.98 kN/m² per 100 mm); frost + UV cycles attack the film | design ≥ 2 % (timber 3 %); outlets at low points; short flow paths; ponding check (§3.2, §7.3) |
| 3 | **Bridged vapour / wet insulation** | missing or punctured barrier; convection through an airtightness gap; dew point left in the insulation | continuous taped Dampfsperre; s_d-ratio design; protect layer from trades; dew point inside insulation (§3.4, §12.3-12.5) |
| 4 | **Missing/too-low upstand; joint inside the water plane** | the water film reaches the vertical joint; butt joints wick (Kapillarfuge) | raise joints out of the water plane (Aufkantung); fillets; height above any ponding level (§3.3) |
| 5 | **Lap/seam failure, multi-ply bitumen** | cold/unheated laps; laps up-slope; stacked layer joints | fully bonded laps offset ply-to-ply; lay low→high; probe every seam at QC (§4, §6.2) |
| 6 | **Membrane punctured by later work** | PV mounts, terrace bearings, services drilled after tanking | pre-planned curbs/ballast; wide pedestals; hold-point sign-off before any fixing (§8) |
| 7 | **Blocked outlet without working overflow** | leaves, debris, nests; single outlet; hidden discharge | leaf guards; mandatory visible emergency overflow per enclosed zone (§7.1) |
| 8 | **Moisture trapped in a sealed sandwich** | no drying path either side; construction moisture never leaves | dry-in-time discipline; ventilated or smart-VCL alternatives; transient proof for critical stacks (§12.3-12.4) |
| 9 | **Thermal-bridge condensation at fixings/penetrations** | metal through insulation (λ 50-5700× insulation) = cold tip + wet spot | stainless/plastic connectors; continuous insulation plane; bridges as points not lines (§6.3, §8) |
| 10 | **Slide-snow damage** | upper roof sheds onto lower (drift wedge + 50 % slip load); no guards; people/entrances below | drift & slip load design; guards into primary structure; keep openings out of slide zones (§2.6) |
| 11 | **Freeze damage at saturated terminations** | ice expansion spalls porous edges; repeated ponded-film cycles | fast drainage at edges; frost-resistant materials in wet zones; no water-holding geometries (§7.3, §13) |
| 12 | **Bridged plinth / rising damp** | raised paving or render reconnects ground above the seal | plinth package 30-50 cm above grade; Querschnittsabdichtung logic; render stop detail (§10.4) |
| 13 | **Wet-area drain/flange leak** | membrane stops beside the drain; sealant-only pipe collars | clamped bonding-flange drains; puddle flanges; two flood tests (§9) |
| 14 | **Condensation on/behind fragile roof lights** | cold dome + warm room; plus fall hazard at the cover | vapour-tight insulated drain stacks; insulated frames; walk-rated covers + restraint design (§11.1) |

**The seven universal counter-rules:**
1. **Continuity** of each functional layer (water, vapour, air) through every plane change.
2. **Redundancy where repair is impossible:** staged pitched roofs; double systems below grade
   and under wet floors.
3. **Mechanical termination first, sealant second** - at every edge and upstand.
4. **Get the joint out of the water plane** - fold up, raise, or overlap in flow direction.
5. **Fall + verified drainage** (≥ 2 % / 3 % timber; visible emergency overflow).
6. **Protect the protection** - UV, foot, thermal shock, frost: ballast, topping, dark-surface
   drying logic; an exposed membrane is a membrane on a countdown.
7. **High resistance inside, low outside** for diffusion; dew point lands in the insulation;
   the airtight layer is the same plane - taped, protected from trades.

---

## Section 15: Critical Dimensions Cheat Sheet

Values flagged **[VERIFY]** are convention/planning values, not clause-confirmed from the
digested norms; the rest are digested.

| Dimension | Value | Applies to |
|---|---|---|
| flat-roof design fall | **≥ 2 %** (aim more) | all flat/low-slope roofs |
| timber flat-roof fall | **≥ 3 %** | wood decks (§12.3) |
| pitched ventilation ≥ 5° | 50 cm²/m eaves + ridge (200 cm²/m with sealed sarking) | ventilated pitched roofs |
| pitched ventilation < 5° | free area ≥ 2 ‰ ≥ 200 cm²/m; gap ≥ 2 ‰ ≥ 5 cm | low pitched roofs |
| upstand above finished surface | ≥ 150 mm **[VERIFY]** | sealing terminations (§3.3) |
| upstand above ponding/retention level | ≥ 250 mm **[VERIFY]** | flat roofs, terraces |
| wet-area upstand | ≥ 150 mm at floor junction; ≥ 200 mm over outlets | §9 |
| corner fillet (Kehle) | radius ≈ 50 mm | every H/V junction |
| plinth seal continuation | 30-50 cm above finished ground | §10.4 |
| balcony overflow opening | ≥ 4 cm clear behind closed parapet | §7.1, §8 |
| gutter fall | ≥ 1 mm/m (3-5 better); front edge 8 mm lower | §7.1 |
| downpipe spacing (gutter) | one per 12-15 m run | §7.1 |
| vapour barrier (full) | s_d ≥ 1500 m; continuous + taped | warm roofs |
| roof R_min (DIN 4108-2) | 1.75 field / 1.0 overall (m²K)/W | §12.1 |
| inverted-roof ΔU | +0.05 / +0.03 / 0 by below-membrane R share | §12.1 |
| R below membrane, lightweight inverted roof | ≥ 0.15 (m²K)/W | §5 |
| Glaser limits | M_c 0.5 / 1.0 kg/m²·a; reserve 250 g (roofs); Δu 5/3 M-% wood | §12.4 |
| Glaser climate | winter 1168/321 Pa; summer 1200/1200 Pa; p_s,c 1700 (2000 roofs) Pa | §12.4 |
| roof Rsi thermal / hygric | 0.10 / 0.25 (m²K)/W | §12 |
| standing water load | 0.98 kN/m² per 100 mm depth | §7.3 |
| gravel ballast load | ≈ 1.0 kN/m² per 5 cm (16/32) | §2.7, §4 |
| snow μ1 | 1.0 ≤ 10°; 0.8 ≤ 45°; →0 at 60° **[VERIFY]** | §2.6 |
| snow density | 2.0 kN/m³ slip loads; 3.0 design unit weight (worked tables) **[VERIFY]** | §2.6 |
| roof load category H | 1.0 kN point (person); not superimposed with snow | §2.6 |
| terrace/balcony load category Z | qk 4.0 kN/m² (+2.0 companion **[VERIFY]**) | §8 |
| parapet line load ≤ 1.2 m | 0.5 / 1.0 / 2.0 kN/m by use class | §8 |
| wet-area tile field | ≤ 40 m², side ≤ 8 m; joints over screed joints 8-10 mm | §9 |
| n50 limits (50 Pa, Verfahren B) | ≤ 3.0 (≤ 1.5 with MVHR); Passivhaus ≤ 0.6 | §12.5 |
| PV edge/ridge non-comb. band | ≥ 0.5 m; combustible build-up ≥ 1.25 m from party wall **[VERIFY]** | §11.2 |
| flood test | 24 h with marked level; inspect below | §9, §14 |

---

## Section 16: FreeCAD / BIM Modelling Guidance

Use with the FreeCAD/BIM modelling skill of this library (Site → Building → Storey hierarchy).

### 16.1 What to model vs what to annotate

| Element | Model as solid? | Notes |
|---|---|---|
| roof slab / deck | **yes** - IfcSlab (ROOF) or Arch Structure | true structural thickness = datum |
| screed/tapered insulation to falls | **yes** - loft/wedge per drainage zone | gives real volumes + real junctions at upstands |
| vapour barrier, sealing sheets | **no solid** - 1-3 mm faces only in detail views; else annotate | modelling mm-layers across the house bloats the file; carry them in the material/assembly data |
| insulation | **yes** where it drives dimensions (Umkehrdach stack, U schedule) | IfcCovering/IfcPlate + class code (DAD/DUK...) as property |
| paving/pedestals, gravel | yes as one combined topping solid | keeps terrace level vs threshold honest |
| rafters/battens | **yes** - members at real gauges | batten grid = tile module (§2.3); shows counter-batten cavity |
| covering | model as a coursing-checked surface + pitch | pitch is the design argument - make it a parameter |
| parapet + coping | **yes**; coping with its own slope + overhang | structural adequacy from the structural skill, not this table |
| outlets/overflows | **yes** - cylinders; overflow as subtraction void in parapet | proves invert levels graphically |
| roof windows/domes | **yes** with kerb flashing envelope | check reveal headroom + maintenance access |
| PV array | yes as load blocks on pedestals/frame | carry added dead load + drift zones into the structural model |
| upstand fillet | detail-drawing only | sub-100 mm features do not belong in the house model |

### 16.2 Modelling recipe (falls + stack)

1. Model the flat deck at true level; sketch roof outline; second sketch at high-point level.
2. Build the screed/wedge zones as `Part::Loft` or wedges per outlet zone; union at valleys;
   name `Roof_Screed_Falls_Z1..Zn`.
3. Verify falls by measurement: outlet invert → high point / plan distance ≥ design value.
4. Apply the stack as named face-offsets or an assembly (barrier / insulation / sealing /
   protection) so quantity take-off returns volumes per layer (§2.7 weights).
5. Attach an **airtight-layer flag** to the barrier component and check it forms a closed
   surface in the model (a quick volume-seal sanity check).
6. Set IFC classes: IfcSlab ROOF / IfcRoof / IfcCovering (membrane, insulation,
   waterproofing) / IfcWall PARAPET / IfcFlowTerminal (outlet) / IfcFlowSegment (downpipe).
7. Model checks before presenting: every enclosed zone has outlet **and** overflow; terrace
   finish ≥ upstand height below any threshold; no raw penetration outside a curb; snow-guard
   line at eaves where people stand below; PV load included; planning-model note in the file.

---

## Section 17: Standards & Rules Referenced

| Norm / rule | Scope | Used here for |
|---|---|---|
| **DIN 18531-18535** | waterproofing series (roofs/terraces; 18533 ground contact; 18534 indoor wet areas; 18532 water-holding structures) | the current waterproofing frame; **DIN 18195 withdrawn/superseded [VERIFY dates per part]** |
| **ZVDH Fachregeln / Grundregeln / Merkblätter / Produktdatenblätter** | roofing trade rules (Regeldachneigung, Unterdeckungsklassen, Behelfsdeckung) | §2.2 class tables; product pitch values **[VERIFY per product]** |
| **DIN 4108-2** | minimum thermal insulation | R_min, fRsi 0.7, Umkehrdach ΔU, reference U's |
| **DIN 4108-3** | climate-driven moisture (period balance) | Glaser, s_d pairs, deemed-to-satisfy roof cases, driving-rain groups |
| **DIN 4108-4 / -10** | hygrothermal design values; application classes | μ/λ values; DAD/DAA/DUK, dh/wd/zh classes |
| **DIN 4108-7 / GEG §26 lineage** | airtight construction | §12.5 continuity + n50 |
| **DIN EN ISO 6946 / 10211 / 13788 / 15026** | thermal resistance; bridge calc; monthly balance; transient HM | §12 methods |
| **DIN EN 12207 / 12208 / 12154-55** | air/rain tightness of windows, doors, curtain walls | §2.8, §11.1 |
| **Eurocode EN 1991-1-1/-1-3 (+NA)** | imposed loads; snow | §2.6, §2.7, §8 load tables |
| **DIN 18008 series** | structural glass | §11.1 flags |
| **DIN 4102-7 / EN 13501-5 (+LBO)** | roof fire performance (harte Bedachung) | §11.2 distances **[VERIFY current]** |
| **DIN 18160 / chimney sealing norms** | flues through roofs/ceilings | §2.4 penetration flags |
| **DWA-A 118 (type) rainfall/runoff rules** | site drainage | §7.2 coefficients |
| **EN 13967 / EN 13970 / EN 15812-14 / DIN 18540 / DIN 18197** | tanking sheets; VCLs; thick coatings; joint sealing; joint formwork | §6, §10 product frame |

**Do not cite a clause number from this table without reading the current text** - several
lineages (18195 → 1853x; EnEV → GEG; 4102 F-notation → EN 13501; 13829 → ISO 9972) were in
transition in the digested sources.

---

## Section 18: Design Review Checklist

**Pitched roof**
- [ ] covering + pitch ≥ product Regeldachneigung, or underlay class raised per ZVDH table
      (residential = 2 increased requirements counted)
- [ ] eaves gutter with ≥ 1 mm/m fall, front edge lower than back, overflow where blocked
      gutter floods an opening
- [ ] verge closed; ridge ventilated/sealed coherently; valley lined generously, seams off
      the valley floor
- [ ] counter-batten ventilation cavity continuous eaves→ridge (50/200 cm²/m rule matched to
      the build-up); no uninsulated cold-spot strips
- [ ] penetrations curbed ≥ ~150 mm and bonded to the underlay; no sealant-only collars
- [ ] snow: sk with altitude correction, μ1/μ2 incl. drift from upper roofs; slide load onto
      every lower surface; snow guards where people/openings are below
- [ ] covering dead load (§2.7) + insulation in the structural case; gable tied against wind
- [ ] airtight layer drawn as one continuous taped plane through every roof penetration

**Flat roof**
- [ ] fall ≥ 2 % (≥ 3 % timber) verified in the model; no back-fall; outlets at low points
- [ ] full vapour barrier under insulation (warm roof) - or Umkehrdach with XPS/foam glass
      only, class DUK/wd (+dh when loaded)
- [ ] multi-ply laps fully bonded and staggered; layer joints entangled, never stacked
- [ ] upstands: continuous sheet over ≈ 50 mm fillet, height over finished + ponding levels
      **[VERIFY]**, mechanical termination + sealant secondary; no field seam at a corner
- [ ] emergency overflow per enclosed zone, invert visible on the facade, ≥ 4 cm balcony
      overflow
- [ ] protection layer chosen per use (gravel/pavers/vegetation); loose tops over bonded;
      membrane never the wearing surface
- [ ] ponding/deflection check at long spans; standing-water load converted (1.0 kN/m²/10 cm)
- [ ] U verified per §12.1 (dry-side layers, ΔU if inverted, wedge formula if tapered)
      and Glaser/transient proof kept for timber decks with toppings

**Terraces/balconies**
- [ ] category Z loads + parapet line loads in the structural case
- [ ] pedestals/bearings spread point loads; no field anchoring through sealing
- [ ] threshold channel/drain detail; falls under paving; movement joints at plane changes
- [ ] balcony thermal-bridge strategy chosen (wrap / lengthen / connector / column)

**Wet areas & below grade**
- [ ] Nassraum class → system + 15/20 cm upstands; clamped drains; bonding tapes; two flood
      tests where two zones exist
- [ ] load case named (Bodenfeuchte … drückendes Wasser) and system matched; repairability
      assumed zero → two systems for habitable basements
- [ ] white tub: waterstops at all cold joints, crack-control regime stated, or black tub:
      continuous wrap with wall↔slab lap detail drawn
- [ ] plinth package 30-50 cm above grade; render stops above the seal; ground falls away;
      downpipes clear of the foundation

**PV / daylight / green**
- [ ] array + retention loads in the structural case; drift/slide re-checked with the array
- [ ] fire separation bands (0.5 / 1.25 m rules) or qualified-covering proof **[VERIFY]**
- [ ] BIPV-as-covering: joint watertightness tested under driven-rain simulation
- [ ] fragile lights: walk-rated or guarded; maintenance route + anchor points modelled
- [ ] roof window U + reveal condensation strategy (heater, shading, small panes)
- [ ] green roof: saturated weight + retention depth as load; drainage conflict documented

**Governance**
- [ ] user told plainly this is a planning-stage package
- [ ] Tragwerksplaner / Prüfingenieur review flagged where statics or fire are concerned
- [ ] Bauordnungsamt approval path flagged (LBO, B-Plan, harte Bedachung by Land)
- [ ] every [VERIFY] item either resolved against the current norm or left visibly flagged
- [ ] no superseded norm (18195/EnEV-era) cited as if current

