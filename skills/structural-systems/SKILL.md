---
name: structural-systems
description: >
  Choose and pre-design the structural concept of a building (DACH / Eurocode practice, German
  terms in parentheses): vertical and horizontal load paths roof-to-soil, system families with
  load-path chains (load-bearing masonry + slab, confined masonry as Eurocode-8-relevant practice,
  RC frame with flat/ribbed slab, composite deck, timber platform/ballon and solid-timber, steel
  frame/brace/portal, precast panel houses), the structural-cell and span-first logic, span/depth
  pre-design ladders (beam 1:10, slab 1:30, shell 1:500, flat slab ≤7 m, ribbed/hollow-core,
  timber joist, truss, EC2-type l/d and beta values), grid coordination with architecture
  (12.5 cm module, wet stacks, stair/lift cores as bracing, 2-dwelling/3-office/7.5 m parking
  grids), stability systems (diaphragms, shear walls, cores, braced bays, rigid vs pinned nodes,
  ring beam/ring anchor 70 kN, bracing triggers), design loads retagged to EN 1990/1991 (unit
  weights, imposed categories A-E/T/Z, partition surcharge, snow/wind zone pointers), a storey-by-storey
  load take-down template with a worked 5-storey residential chain, foundation interface (loads to
  ground, presumptive DIN 1054 resistances, kern rule, link to geotechnics-foundations), robustness
  and continuity (notional tie forces per EN 1991-1-7, key elements, alternate load path), seismic
  configuration pointers (EC8, behaviour factors, soft storey, masonry no-calculation conditions),
  material choice matrix (cost, speed, span, physics, carbon cross-reference), case patterns
  (2-storey MFH masonry+slab, 5-storey RC, hall steel, 4-storey timber), anti-pattern catalogue,
  BIM defaults, and handoffs to structural-analysis, concrete-detailing, masonry-construction,
  timber-steel-design, geotechnics-foundations, seismic-design.
---

# Structural Systems — Choosing the Load-Bearing Concept (Tragsystem, Tragwerk)

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

This skill exists so that an early architectural design carries a **plausible structural concept**
rather than an arbitrary one: the right system family for the storey count and spans, a grid the
structure can live on, wall/slab/column/footing sizes in the right order of magnitude, a bracing
strategy, a continuous load path from every bearing point down to the ground, and a tie/robustness
logic. Everything here is **pre-design**: rules of thumb, code-anchored dimensions, and hand
calculation. Nothing here is a substitute for the analysis and design (Nachweis) by a competent
structural engineer.

Framing: **DACH practice under the Eurocodes** — DIN EN 1990/1991/1992/1993/1995/1996/1997/1998
with National Annexes (NA) in Germany, ÖNORM B 199x in Austria, and the parallel SIA 26x series in
Switzerland. Where a number is German-NA-specific it is labelled as such; Austria/Switzerland values
differ in detail and must be re-read from the applicable national documents (VERIFY).

## Reality Check — Licensing & Liability

**This skill produces design aids and calculation guidance for planning and modelling ONLY.**

- Every number is a **preliminary sizing estimate, a code minimum, or a rule of thumb**. Rules of
  thumb are calibrated to "typical" loads, spans and soils. This project is not typical until
  someone has checked it.
- **Any design intended for real construction of an occupied building must be planned, analysed and
  signed by a qualified structural engineer** (Tragwerksplaner/in; Germany: Nachweis der
  Standsicherheit by a locally authorised engineer, Prüfstatik in the qualified-scope Länder;
  Austria: STATIK; Switzerland: Sicherheitsnachweis nach SIA 260/261). Elsewhere the equivalent
  licensed/chartered engineer.
- **Never present a model output, a sizing table, or a hand calculation here as
  construction-ready.** Frame it always: "preliminary concept for coordination — to be verified
  and signed by the structural engineer of record." Say this unprompted when a user talks as though
  the output is final ("how much concrete do I order", "we pour next week", "delete this wall, the
  model stands").
- **Never certify.** No engineer's name, registration number or signature block on any output.
- **Ground is never assumed.** Every foundation number here is conditional on a **site-specific
  geotechnical investigation** (Erkundung, DIN 4020). "Presume 200 kPa" is a model placeholder,
  never a design input.
- **Seismic action is never guessed.** Hazard values come from the current national hazard map /
  reference-acceleration list for the exact municipality — not from memory or a neighbouring town.
- **A converged FEM result validates the model you built, not the building.**

---

## Section 0: How to Use This Skill

### 0.1 Route by question type

| The user asks… | Go to |
|---|---|
| "What structural system should this building use?" | §2.1 decision tree → §2.2 catalogue → §2.3 matrix → §2.4 hybrids |
| "Where do the loads go?" | §1 load paths, §1.4 continuity audit |
| "How thick is the slab / how deep the beam?" | §4.2 slab, §4.3 beams/cols, §4.4 l/d |
| "What grid should the architecture be on?" | §3 structural cells and grid coordination |
| "How do we stand it up? What loads?" | §5 stability/bracing · §6 design loads (EN 1990/1991) |
| "What size are the columns/walls/footings?" | §7 take-down template → §12 foundation interface |
| "Seismic OK?" / "which material?" | §8 + §14 → `seismic-design` / §2.3 + §9–§11 + §15 |
| "What if something fails?" | §13 robustness and continuity |
| "Draw/model this" | §19 BIM defaults |
| "Is it done?" | §20 checklist + Reality Check, unprompted |

### 0.2 The 60-second defaults

When someone needs *a* plausible answer immediately:

**Detached/terraced house (EFH/DH), 2 storeys, pitched roof, spans ≤ 6.5 m, soil ≥ 200 kPa:**

```
System        load-bearing masonry (tragende Wand): 30–36.5 cm KS/HLz (24–30 + ETICS),
              internal bearing 11.5–15 cm (≤3 kN/m walls → 1.0 kN/m² surcharge covers them)
Floors        Holzbalkendecke or RC 20–22 cm · Roof: trusses/rafters on plate, tied (§5.6)
Bracing       walls both directions + floor discs · Ringanker every floor + gable ≥ 70 kN (NA)
Foundation    strip ~0.8 × 0.3 below frost (≥ 0.80 m by DIN 1054, S.1; practice 0.8–1.2 m, VERIFY region) · storey 2.70–2.90 m
```

**Multi-storey residential (MFH), 4–6 storeys, parking basement, spans 5–7 m:**

```
System            RC: WU basement + load-bearing wall or frame + flat/ribbed slab
Grid              5–6.5 m residential / parking 3 × 2.5 = 7.5 m bays
Slab              22–28 cm flat (check punching!) or ribbed/hollow-core for ≥ 6 m
Cols/walls        take-down governs (§7); screening νEd = NEd/(Ac·fcd) ≤ ~0.5
Bracing           stair/lift core + wall bands both directions; non-sway check
Foundation        pad/strip or raft; ground slab (Weiße Wanne below water table)
```

Then say immediately: *preliminary, subject to ground investigation, seismic-hazard lookup, and the
structural engineer's design.*

### 0.3 Sibling skills — hand off rather than duplicate

This skill selects and pre-sizes concepts; every verification-grade calculation belongs to its
domain skill (routing table at §20.3). Hard rule: masonry/beam/slab *check* maths →
`structural-analysis` + `masonry-construction` + `concrete-detailing`; ground →
`geotechnics-foundations`; earthquake numbers → `seismic-design`; carbon →
`sustainable-construction`; sequence → `construction-scheduling-site`.

### 0.4 Units and module convention

Metric primary: loads kN and kN/m², stresses MPa (N/mm²), ground resistance kPa (kN/m²), dimensions
mm/cm where noted. German terms in parentheses at first use. The dimensional game in DACH is the
module: masonry planning dimensions run on **12.5 cm steps (Kopfzahl × 12.5 cm, DIN 4172 lineage)**
— room planning dimension 4.00 m becomes wall-centre 4.01/4.02 m once the leaves are added; concrete
coordination dimensions prefer multiples of 12.5/25 cm. Set the architectural grid on the structural
module from day one (§3.3).

---

## Section 1: Load Paths (Lastabtrag)

### 1.1 The two permanent questions

Every structural concept answers two questions, and answers them **before** choosing material:

1. **Vertical:** every load — people, snow, walls, roof, finishes — must reach the ground through a
   continuous chain of elements in compression/bending/tension. If any element in the chain is
   missing, the load takes a detour (slab spanning the wrong way, torsion edge beam) or the element
   fails.
2. **Horizontal:** wind (and earthquake, snow drift not, temperature) must be collected at floor
   and roof levels by **diaphragms (Scheiben)**, delivered by collectors to **bracing elements
   (Aussteifung)** — walls, cores, frames, trusses — which cantilever down to the foundation, which
   transfers shear and overturning into the ground.

**The load-path rule (non-negotiable):** a bearing point above implies a bearing point below.
Every column lands on a column, every wall on a wall, every wall on a footing, every footing on
inspected ground. A load that "stops" mid-chain is a design error waiting to be discovered.

### 1.2 Gravity chain by system

```
Masonry:      roof → wall plate → wall panel → ring beam → wall panel → plinth/foundation beam
                (Sockel) → strip footing → ground
RC frame:     slab → beams → columns → next storey… → foundation beam/raft → pads/piles → ground
Cross-wall:   hollow-core on bearing ledges → wall panel → grouted base/sleeve → ground beam → ground
Timber:       deck → joists → rim + studs → sole plate → foundation plate → ground
Steel hall:   sheeting → purlins → rafters/trusses → columns → base plates + anchors → pads → ground
```

In each chain note who carries **only self-weight** (non-loadbearing infill, Vorhangwand) versus who
carries **stacked load** — confusing the two is how partitions end up under a slab (§18).

### 1.3 Lateral chain

```
Wind pressure/suction on face (or seismic mass at each floor)
  → wall/cladding spanning between floors (out-of-plane)
  → floor/roof diaphragm in its plane (rigid disc,ebene Scheibe)
  → collectors at diaphragm edges/openings
  → bracing elements in load direction (in-plane shear walls, cores, frames, trusses)
  → vertical cantilever over full height: base shear + overturning
  → foundation: base friction (τ ≤ μ·N), passive resistance, moment into bearing pressure
  → ground
```

Diaphragm quality by floor type — the concept, not a calculation:

| Floor type | Diaphragm? | What makes it one |
|---|---|---|
| Cast-in-place RC slab | yes, by default | monolithic; edge members still good practice |
| Hollow-core / plank + topping | **no** until made one | 40–60 mm C20/25 topping + mesh + transverse keyed joints + edge tie into ring anchor |
| Ribbed/unitized slab | yes with topping | topping + bond between units |
| Timber joist floor | **no** unless sheathed | structural boards + joints offset + edge members + diagonal strapping or panel walls |
| CLT/X-lam floor | yes | plate action, chord members at edges |
| Trapezoidal steel deck (roof) | yes | sheeting + shear connectors + perimeter members |
| Purlin roof on tiles | **no** | needs plan bracing (diagonals/plates) or a ceiling-level diaphragm |

### 1.4 Load-path continuity audit (run on every model)

- [ ] Every column/tie-column continues to the level below, to the foundation — no floating columns
      without a designed transfer element (§18); every wall stands on wall/beam/wall-slab; non-
      loadbearing partitions never appear as supports
- [ ] Ring anchor/Ringanker is a **closed ring** at every relevant level (§5.5), tied into diaphragms
- [ ] Diaphragm is continuous at each level; collectors around every void (stair, shaft, atrium)
- [ ] Bracing exists in **both** orthogonal directions on **non-intersecting axes** (§5.4)
- [ ] Bracing walls are vertically loaded (shear capacity of masonry grows with compression) and
      rotated storey-to-storey if floor spanning direction rotates
- [ ] Stair and lift cores modelled as what they are: stiff bracing that attracts force
- [ ] Cantilever back-spans ≥ 2 × cantilever and held down (overturning, §18)
- [ ] Roof thrust tied (pitched) and held down (light roofs, wind suction)
- [ ] Heavy point loads (tanks, lifts, plant, stoves) sit on a line, not mid-span
- [ ] Nothing structural is chased, notched or drilled through without a check

---

## Section 2: Choosing the Structural System

### 2.1 Decision tree

```
START: building type + storeys + spans + site
│
├─ Q1 Storeys above ground?
│   ├─ 1–2 (EFH/DH) ......... masonry systems, timber, RC frame, precast all viable
│   ├─ 3–5 (MFH small) ....... masonry + slab (EN 1996-3 range), timber (4–5 storeys,
│   │                          settlement/transverse-compression limits §9.4), RC, precast panel
│   ├─ 5–7 (MFH typical) ..... RC wall/frame + flat or ribbed slab; precast panel house;
│   │                          timber possible with mixed WCC/hybrid — engineer territory
│   └─ >7 .................... RC core+wall or frame, composite/steel, precast; masonry only
│                              with verification beyond simplified methods (VERIFY, EC6/EC8)
│
├─ Q2 Largest clear span?
│   ├─ ≤ 5 m ................. anything; solid slab economical
│   ├─ 5–7 m ................. solid slab deepening / ribbed / hollow-core / flat slab
│   │                          (punching governs, §4.2)
│   ├─ 7–12 m ................ ribbed or hollow-core floor, steel/conc beams, timber
│   │                          beams/lVL at reduced live load, precast single span
│   └─ > 12 m ................ hall: trusses/portal/beam grid (§10.4), long-span precast/PT
│
├─ Q3 Regularity of plan & vertical stacking?
│   ├─ compact, walls/columns aligned storey on storey ... simple wall or column systems fine
│   ├─ re-entrant (L/T/U), cantilevered wings, setbacks .... frame or explicit joints (§13.6)
│   └─ open ground storey (shopfronts, parking, "pilotis") . frame + designed bracing;
│                                                          soft-storey risk §14.4
│
├─ Q4 Seismic hazard of the site (read the current national map — never from memory)?
│   ├─ low ........................ the systems above all work with normal detailing
│   ├─ moderate .................. confined masonry needs full confinement detail (§8.3),
│   │                              walls reasonably symmetric; RC needs ductile class
│   │                              detailing; timber panel and ductile steel very good
│   └─ high ...................... configuration rules dominate: compact plan, doubled
│                                  bracing, symmetric walls, continuous tie; masonry
│                                  limited to CM with verification — route to seismic-design
│
├─ Q5 Site & programme logic?
│   ├─ narrow urban infill, party walls, quiet required .. masonry/RC (mass = acoustics + fire)
│   ├─ fast watertight shell, winter build .............. precast panel or timber modular
│   ├─ basement under footprint, groundwater ............. WU RC (Weiße Wanne) basically mandatory
│   ├─ future conversion/extension likely ................ frame frees the walls (skeletal);
│   │                                                     wall systems lock the plan
│   └─ car-independent hall / industry ................. steel portal (§10.4)
│
└─ Q6 Mixed triggers on one building (hall bay in a masonry house? column-free room over parking)?
    → HYBRID, but only under §2.4 rules — or accept a transfer beam as a designed key element
```

### 2.2 System catalogue — load-path chains and pre-design data

#### System A — Load-bearing masonry + slab (Mauerwerksbau mit Decken, wall construction)

The wall carries and encloses; floor slabs span wall-to-wall. The classic DACH EFH/MFH system.

| Parameter | Value |
|---|---|
| Storeys | 1–3 comfortably in the EN 1996-3 simplified range (≤ 3 storeys, ≤ 20 m, see §8.2); more with full EC6 verification |
| Wall thickness | 24–36.5 cm bearing (KS/HLz/PB per load); ≥ 11.5 cm minimum bearing leaf |
| Floor span wall-to-wall | RC solid slab **5–7 m economical** (plate spanning on ≥ 2 opposite walls); timber floor **≤ ~4.5 m** |
| Grid | cross-wall (walls at apartment width 2.5–3.5 m) or perforated-plate typology, §8.1 |
| Bracing | walls in both directions, floor diaphragms, ring anchor (§5.5) |
| Openings | pier + stacking rules, §8.4 |
| Relative cost | **1.0× baseline** for 2–4 storey residential (DACH grey structure, rough band — VERIFY locally) |
| Fire/acoustic | inherent mass: best party-wall and REI behaviour for the euro invested |
| Fails when | ring anchor missing; bracing axes intersect in one point; walls unstacked; future open-plan ambitions |

#### System B — Confined masonry (Confined Masonry / "Duktil gemauertes Tragwerk")

Masonry panels carry gravity and shear, but each panel is **confined** on all four sides by small
RC tie-columns and tie-beams cast against toothed (verzahnt) wall edges. It is the masonry system
that behaves well in earthquakes, and it is addressed in **Eurocode 8 practice for masonry buildings
(EN 1998-3 covers confined masonry; national seismic practice for one- to three-storey masonry
generally points at it wherever the hazard warrants, VERIFY the applicable NA/EC8 edition)**.
Sequencing is the whole idea: **build the wall first with toothed edges, then pour the confinement
against it** — the opposite of an RC frame with infill.

| Parameter | Value (EC8-relevant masonry practice) |
|---|---|
| Storeys | 1–3 (simplified range); 3 with full detail + check |
| Tie-columns | ≥ wall thickness × 20–25 cm; typical 4Ø12, Ø8/15–20 links; every corner, every junction, both sides of openings > 1.2–1.5 m, free wall ends, spacing ≤ ~4 m and ≤ 1.5 × storey height (VERIFY against EC8-3 detail values in use locally) |
| Tie-beams/Ringbalken | at every floor + roof level, closed ring, ≥ wall width; cast with slab edge |
| Panel limits | panel length ≤ 1.5 × storey height region rule of thumb; h/t ≤ ~25; opening area per storey ≤ ~40–50 % of façade |
| Wall ratio screening | bracing wall area / floor area per direction: roughly **2 % (1 storey, low hazard) → ~6 % (3 storeys, higher hazard)**; German legacy no-calculation masonry rules sit in this band (DIN 4149 era, superseded by EC8 maps — values indicative, VERIFY) |
| Where it fails | tie-column poured before the wall; confinement not continuous to foundation; smooth (untoothed) joints; wall ratio deficit "fixed" with more slab steel |

#### System C — RC frame or wall structure with flat / ribbed slab (Stahlbeton)

Skeleton with columns + beams (rahmenartig) or punched walls; floors as flat slab (Flachdecke),
mushroom on columns, or ribbed (Rippendecke/Rasterdecke). The DACH MFH and office default.

| Parameter | Value |
|---|---|
| Storeys | effectively unlimited with cores/walls; 4–7 for typical MFH/office |
| Flat slab limits | **bay ≤ ~7 m economical** (punching governs, not bending); h ≈ 22–28 cm at 6 m, punching reinforcement or drop columns otherwise (§17) |
| Ribbed (two-way Raster) | grid 60–70 cm ribs 10–12 cm + 4–5 cm topping; depth ≈ l/20–l/25 (VERIFY); good 7–10 m |
| Beams | h ≈ l/10 SS, l/12–l/15 continuous (§4.3) |
| Column grid economy | offices ~ 3 room-widths ≈ 7.2–8.4 m; parking **3 × 2.5 = 7.5 m** bays; residential 2 dwelling widths (§3.2) |
| Bracing | cores (stairs/lifts) + wall bands; non-sway check; frame alone needs rigid nodes (economy suffers) |
| Relative cost | **1.15–1.4× masonry** same storeys (grey structure band, VERIFY) |
| Where it fails | punching at flat-slab columns; short columns from partial-height infill; rigid-frame corners with no bracing budget; two-way flat slab without cores (no bracing left) |

#### System D — Composite deck + steel or RC frame (Verbunddecke)

Profiled steel sheet as permanent formwork + shear-studded RC topping over steel sections; the
efficient mid-rise/office alternative, and the standard for hall mezzanines.

| Parameter | Value |
|---|---|
| Deck | trapezoidal sheet 50–80 mm, topping 12–16 cm, total ≈ l/15–l/20 between beams (typical 20 cm decks at 3–3.5 m beam spacing, VERIFY supplier tables) |
| Beam spacing | secondary 3–4 m typical with 2–4 span continuous deck; main 6–9 m |
| Slim-floor variant | flush beam with lower-flange shelf carrying precast units — flat soffit, free services zone (§10.3) |
| Fast | deck is formwork + working platform; ~ 1 floor/week shell cycle realistic at scale |
| Fire/corrosion | protection strategy priced in from day one (paint/cladding/sprinklers); fine open sections worst |
| Where it fails | acoustics (needs screed/mass for residential), services coordination assumed free, bracing forgotten |

#### System E — Timber: platform, balloon, solid timber (Holztafelbau, Point- / Geschossweiser Abbund, Brettsperrholz)

Prefabricated panel system: dense slender studs carry gravity along grain; **wood-based sheathing in
the panel plane carries the shear** — bracing comes from the panels themselves, so no reliance on
mass or ground friction (timber must be raised off ground on a mineral base — the plinth/Soockel
rule, §9.1).

| Parameter | Value |
|---|---|
| Storeys | platform 2–3; solid timber (Brettsperrholz/CLT, end-grain to end-grain stacking) 4–5+ (settlement and node fire details govern higher) |
| Stud spacing | 400–625 mm typical; panel format: large up to ~10 m (transport-limited) — fewer joints = better wind + air tightness; small 1.0–1.25 m panels obsolete (joint count) |
| Floors | joist floors ≤ ~5 m; box/trough timber elements to ~14 m; CLT spans to ~5–6 m solid, more with ribs |
| Platform vs balloon | platform (Geschossweise): storey-high walls, joists on top plate, deck on joists, next storey's walls on the deck. Balloon (Zweigeschossige Ständerwände, durchgehend): studs run two storeys, joists on let-in ledgers (spans 4–5 m) — fewer vertical joints, continuous stud line, fire-stopping care |
| Bracing | shear panels + diaphragms; hold-downs at panel ends + tie chain to foundation (wind uplift is the design case, §18) |
| Relative cost | **1.0–1.3× masonry** in DACH today with a real trade base (VERIFY market) |
| Where it fails | rot at ground contact, acoustic mass under-spec, stacking force through end-grain/sleeper settlement, node fire detail |

#### System F — Steel frame / braced frame / portal (Stahlbau)

Tough material: tension *and* compression, slender sections, factory tolerances that let fit-out sit
directly off the structure. Design culture splits **pinned members + explicit bracing** (fast bolted
site work, cheap nodes, needs bracing space) vs **rigid frames** (portal halls, moment nodes are
factory or heavy site welds).

| Parameter | Value |
|---|---|
| Halls | portal frames ~ 12–15 m bays on standard hot-rolled sections; trusses 10 → > 100 m; purlins 1.2–1.5 m along slope |
| Multi-storey | braced frames (cross/vierendeel/chevron) or frames + cores; **unbraced multi-storey steel frames are flexible → mid-rise limit without extra bracing** |
| Nodes | hinged: fin-plate/flush end-plate, base plate + anchors (pinned foot), welded lugs in factory; rigid: welded/bolted moment, haunched portal corners — keep the rigid erection joint away from max moment (contraflexure point) |
| Bracing | roof diaphragm (sheeting + field members) + vertical bracing in end bays (short load paths) or facade zones; bracing lines must not intersect at one point |
| Longevity | dismantlable, recyclable; weaknesses = fire + corrosion, both detailable |
| Where it fails | bracing not reserved architecturally; fire protection discovered at cost stage; buckling of slender compression web in high shear (bearing stiffeners) |

#### System G — Precast panel houses (Fertigteilbau, Plate Bauweise)

Factory-cast RC (or sandwich) wall panels + hollow-core floors: the industrialised version of the
cross-wall house — and the postwar row-house/Großsiedlung system family across DACH/Central Europe.

| Parameter | Value |
|---|---|
| Systems | solid wall panels (Vollwand) or sandwich elements (two wythes + factory insulation core); floors hollow-core or double-tee on bearing ledges |
| Nodes | mostly **pinned/gravity**: cleats (Auflagerschenkel on elastomeric pad, centring pin), pocket/tooth tilt-locks, grouted couplers (Muffen) for vertical continuity, sleeve foundations (Mantelfundament) — self-stable immediately on release, statically determinate overall, hence **insensitive to settlement but dependent on ties** (§13.4) |
| Floors | hollow-core 160–500 mm deep, ~ 30–40 span/depth, 1200 wide (VERIFY supplier); side grooves + transverse grout key = plate interaction; topping for diaphragm |
| Transport | upright panels ≤ ~ 4.0 m storey height; uniform element weights = crane economy |
| Speed | erection ~ 1 floor/2–4 days at scale; 24-h plant cycle; long planning lead time and grid discipline upstream |
| Relative cost | 1.0–1.2× cast-in-place with repetitive grid; worse the more bespoke (formwork amortisation) |
| Where it fails | diaphragm/tie design (untied planks are boards, not a disc); thermal bridges at plates/walls; joint sealing programme; crane/site access |

### 2.3 System comparison matrix

| Criterion | Masonry+slab | Confined masonry | RC frame/slab | Composite deck | Timber panel | Steel frame | Precast panel |
|---|---|---|---|---|---|---|---|
| Storeys (economic) | 1–5 | 1–3 | any | 3–10 | 1–5 | any | 1–6 (typical row) |
| Clear span sweet spot | ≤ 6.5 m | ≤ 5 m | ≤ 7 m (flat) | 8–12 m frame | ≤ 5 m (joist) | 12–25 m hall | ≤ 7 m floors |
| Grey-structure cost band (relative) | 1.0 | 1.05–1.2 | 1.15–1.4 | 1.2–1.4 + fire | 1.0–1.3 | 1.2–1.6 + fire/corr | 1.0–1.2 (repeat) |
| Speed on site | slow-mid | slow-mid | mid (weekly cycle possible) | fast | **fast** (dry, prefab) | fast (dry) | **fastest** (erection) |
| Seismic behaviour | weak unless confined | **good with detail** | good if ductile | very good (light, ductile) | very good (light) | good with bracing design | good if tied & verified |
| Self-weight | high | high | high | mid | **low** | low | high |
| Thermal mass | good | good | good | low (needs screed) | low | low | mid |
| Acoustic (party walls) | **best** | good | good | needs mass | needs build-up | needs build-up | good (solid) |
| Fire | inherent | inherent | cover-dependent | protection needed | charring design | protection needed | inherent |
| Carbon (qualitative) | mid | mid | high-cem → SCM/eco-conc levers | steel high but recyclable | **stored biomass** (see `sustainable-construction`) | high | eco-concrete possible |
| Foundation load | high, dispersed | high | concentrated pads | mid | low | low | high |
| Typical fit | EFH/DH/MFH to 5 | 1–3 storey seismic | MFH, office, TG | office/mezz/industrial | EFH to MFH | hall, multi-storey shell | row MFH, hotels, TG |

### 2.4 Hybrid systems (Mischsysteme)

Common and legitimate — masonry wing + frame bay over the open room; timber upper storeys on RC
plinth/parking; precast walls + cast-in-place cores. It fails in predictable ways without rules:

1. **Stiffness truth.** A 24–30 cm masonry shear wall is orders of magnitude stiffer in-plane than
   an RC frame of the same length. In a shared line the wall takes all the shear until it cracks,
   then dumps it on the frame. Never assume proportional sharing.
2. **Separate the load paths in plan.** Masonry resists within its own footprint; the frame within
   its own. Do not put a shear wall and a braced frame in the same line "for redundancy".
3. **Continuous diaphragm across the junction.** Slab cast (or tied) monolithic across the boundary,
   collector along the line linking frame beams into the ring anchor.
4. **Match foundations at the junction.** A pad at −2.0 m beside a strip at −0.8 m with 30 cm of air
   between is a differential-settlement crack waiting; step 1:2 max and keep the tie continuous, or
   found both at one level.
5. **The frame part must be self-stable.** After the masonry cracks in a strong shake, it is briefly
   not there.
6. **Infill in frames:** decide and detail — **isolated infill** (20–30 mm gaps, compressible
   filler, out-of-plane restraint; frame carries all lateral load — honest) or **integral infill
   designed as confined struts**. Never build tight infill and analyse a bare frame: that pairing
   breeds surprise torsion, short columns and soft storeys.
7. **Full-storey height/stiffness step** between blocks: separate with a movement/seismic joint
   (§13.6), don't stitch.

---
## Section 3: Structural Cells and Grid Coordination with Architecture

### 3.1 The structural cell (Zelle) — span first, then the other dimension

The elementary volume of any building is **enclosure + covering**. The covering's span is the
constrained dimension: fix the span you are willing to carry (and its depth follows, §4), then choose
the perpendicular room dimension **larger** — compact for dwellings, extreme for halls. Cells add:

- **Horizontally:** rectangles adjoin gap-free (angled/round cells = residual space, angled slabs,
  oblique beams with longer effective spans); rectilinear cuboid is the economic default, corners
  and edges concentrate the physics detail.
- **Vertically:** floors stay flat and level; stacking is how the building pays for land — each
  stack brings take-down (§7) and continued bracing (rotate the floor spanning direction
  storey-to-storey to keep loading the shear walls). **A/V ratio** governs envelope economy and
  energy; compact plans are structurally cheaper too (less façade to anchor, less edge to tie).

### 3.2 Grid economics by use

| Use | Grid logic | Typical |
|---|---|---|
| Dwelling | 2 dwelling widths deep; cross walls at party/room width | spans 4.5–6.5 m; unit width 2.5–3.5 m |
| Office | 3 room widths across | 7.2–8.4 m depth → flat/ribbed/composite |
| Parking (TG) | 3 bay lengths as one span | **3 × 2.5 = 7.5 m** between column lines; one-way ramps and drives read this |
| Hotel/care | corridor + room = two spans | 2.5–3.5 + 4.5–6 m, repeating bathroom stack |
| Hall | span overrides grid; bracing goes to the ends | truss/portal 12–25 m (§10.4) |

**Span direction discipline:** a slab always spans the short way unless forced; two-way action is
only genuinely exploited on ≈ square panels — **at side ratio ~1:1.5 the slab already behaves almost
one-way** and the "two-way" design is fiction. Put the supporting elements where the short span is.

Load cross-distribution is what makes structures usable. Relative mid-span deflection of a square
panel under central point load, by composition: independent one-way strips = 1 (edge 0); strips with
shear-keyed distribution = 1/3 (edge 1/30); one-way + transverse plate bending = 1/7 (edge 1/10);
true two-way = 1/15 (edge 0; uniform full-area load 1/42). Pure one-way systems accept no local or
asymmetric load without help — hence toppings, keys, and rib grids exist.

### 3.3 Coordinating the architectural grid with the structure

- Set the **axes on the module** (12.5 cm multiples for masonry coordination; 25 cm for concrete).
  Dimension walls **axis-referenced** (Achse), not as afterthought thicknesses.
- Columns disappear inside wall thicknesses (30×45 in a 30 wall, long axis to the bigger moment;
  > ~10 cm into a room = architectural bug). **One grid serves both directions** whenever possible;
  any storey-to-storey offset is a transfer element (§18).
- Repeating dimension = repeating formwork = money. The weekly floor cycle (Wochentakt) of RC
  multi-storey works only with re-used table/panel formwork on a constant grid (§4 of
  `construction-scheduling-site`).
- **Wet stacks and risers:** bathrooms/kitchens stacked wall-to-wall vertically so waste and supply
  run inside a single band, ideally along a bracing line; drains through slabs need sleeve/
  penetration coordination (route penetrations at flat-slab design time — punching zones and rib
  lines do not tolerate random holes). Show shafts in the structural grid from day one.
- **Stair and lift cores as bracing:** place them near the **plan centre of stiffness**, symmetric,
  full height, unbroken. A core is much stiffer than the walls around it — it attracts the storey
  shear and controls torsion. Long buildings: cores at the ends restrain the slab and cause
  cracking — put an expansion joint near the core or release the slab in one direction (§13.6).
  A fire-enclosed stair core can contribute structurally unless deliberately decoupled.
- Double-height spaces, galleries, and atria **punch the diaphragm**: edge them with collectors and
  re-verify the force still reaches bracing (§5.3).

## Section 4: Pre-Design — Spans, Depths, and Member Sizes

### 4.1 The slenderness ladder (from conception)

Bending is inefficient; the deeper the lever arm, the less material. The ladder: beam ≈ **1:10**,
solid one-way slab ≈ **1:30**; ribbed/hollow-core effectively 1:20–1:40 (weight moves to the
chords); two-way flat slab ~1:27–1:32 → practical bay cap ~7 m; shells to 1:500 (formwork-limited);
arches/cables buy rise ≫ beam depth to avoid bending. Economic limit of a plain one-way solid slab
≈ **8 m (~300 mm)** — beyond it dead weight eats the benefit: switch to ribs, hollow-core, beams.

### 4.2 Slab pre-design (Decken)

```
ly/lx ≥ 2 (or supported on two opposite edges only) → ONE-WAY: main steel short span
ly/lx < 2                                            → TWO-WAY both directions, corner steel
At ~1.5:1 already treat as one-way (§3.2).
```

Preliminary thickness, residential/office normal loads, cast-in-place (retagged to EC2-type l/d
logic — for verification-grade l/d use the `structural-analysis` K/β method):

| System | Simply supported | One/both ends continuous | Cantilever | Notes |
|---|---|---|---|---|
| One-way solid slab | l/24–l/28 | l/28–l/32 | l/10 | min h ≥ ~12 cm one-way, ≥ 15 cm two-way (constructive + fire) |
| Two-way slab on walls/beams all round | l/30 | l/35–l/40 | — | lx governs |
| Flat slab on columns (no beams) | ~l/28–l/30 | same | l/6–l/8 (edge) | **bay ≤ 7 m; punching governs (§17 STEP 4)**; min h ~ 20 cm |
| Ribbed / grid (Raster) | l/20–l/25 total | same | — | ribs 10–12 × 4–5 cm topping; verify torsion edge beams |
| Precast hollow-core + topping | ~l/30–l/40 | (single span — pretensioned) | small only | ~200–400 mm deep, 4–15 m span band (VERIFY supplier span tables) |
| Composite trapezoidal deck | l/15–l/20 total | same | — | between secondary beams ≤ ~3.5–4 m (VERIFY pro dataset) |
| Timber joist floor | l/16–l/20 (joist depth) | — | — | C24 ~600 oc: 4 m → ~20/22 cm, 5 m → ~24–26 cm (VERIFY span tables per load class) |
| CLT plate floor | l/25–l/30 one-way main direction | — | l/5–l/6 | X-lam: outer plies set main direction |

Residential outcome (g+q ≈ 9–11 kN/m²): ≤ 4.5 m → 20 cm solid; 4.5–5.5 → 22–24; 5.5–6.5 → 24–26
or hollow-core 200–250; 6.5–8 → 26+/beams or hollow-core 250–320 (rib l/22); > 8 → beams/PT/double-tee.

**Top steel over every internal support** — continuous slab has hogging over each line; the classic
site failure is a bottom-mesh-only slab cracking in a straight line over every wall. Cantilever
(balcony/Kragplatte): tension on top, depth ≈ l/5–l/10 (see §4.1), back-span ≥ 2× cantilever,
overturning check with partial factors (stabilising 1.0/0.9 — see §6.6), thermally decoupled or
detailed for the bridge.

### 4.3 Beam / column pre-design (Unterzug, Stütze)

**Beams:** depth `h ≈ l/10` (simply supported, one-way framing), `l/12–l/15` continuous; width
`b ≈ h/2.5–h/3` rounded to ≥ 20–25 cm for buildability (congested 18 cm beams are unpourable —
bar pitch 10–15 cm minimum vs vibrator 6–8 cm). Cantilever beam: total h from l/8-ish, tension top.
T-beam action: slab cast monolithic on top makes the beam cheaper — quote **total depth from top of
slab** (it is what sets the ceiling height).

| Clear span | Beam depth (total) | Typical b×h |
|---|---|---|
| ≤ 3.5 | 25–30 | 25×30 |
| 4–5 | 35–45 | 25×40 |
| 5–6 | 45–55 | 30×50 |
| 7 | 60–70 | 30×60 |
| 8 | 70–85 | 35×75 |
| 9–10 | 90–110 | 40×90+ — steel often cheaper here |

Adjust upward when the beam carries a full-height wall (a 3 m 24 cm KS wall ≈ 14 kN/m — often more
than the slab), a point load (hanging column — engineer it, don't table it), or vehicle load.

**Hidden beams (Taschenunterzug, beam flush with slab):** depth halved → stiffness quartered.
Never span > ~3.5 m with one, never as transfer. If architecture wants a flat soffit over a long
span: thicker slab, ribbed, hollow-core, or slim-floor — not a shallow wide beam.

**Columns:** size by take-down (§7) screened against `νEd = NEd/(Ac·fcd)`:

```
fcd(C25/30) = 14.2 N/mm², C30/37 = 17.0 (αcc 0.85, γc 1.5)
screening: νEd ≤ ~0.5 house/office low-rise; ≤ 0.65 upper bound (2nd-order grows fast beyond)
⇒ e.g. NEd = 2200 kN, C25/30 → Ac ≥ ~260,000 mm² → 50×50 or 40×60 with margin (§17)
```

Hard minimums before any arithmetic: least dimension ≥ 20 cm (VERIFY current EC2 detailing floor;
30 cm is the practical minimum in DACH MFH for congestion + cover + buckling), clear-height/least
dimension ≲ 10–12 in braced frames (unbraced: slenderness check, `structural-analysis`), orient the
long side against the bigger moment/less-braced direction. **Strength almost never governs the
tabled size in housing — minimum dimensions, detailing space, slenderness and wall-alignment do.
State that when quoting sizes.**

**Walls as deep beams (Scheiben, Wandträger):** a storey-high RC wall point-loaded at the top
transfers by deep action across its full height — exploited at transfer levels (parking below tower:
column-on-wall stops need explicit verification, not the §4.3 table).

### 4.4 l/d verification anchors (EC2-type, for the pre-design sanity band)

From the German EC2 tables (retagged; use `structural-analysis` for the full formula):

- l/d = K + corrections; **K ≈ 30** for lightly loaded slabs < 7 m, 24 (7–12 m), 19 (>12 m);
  **K ≈ 28→13** for beams by span band; flat slab K ≈ 21 (heavily loaded) — the practical reading:
  residential slabs land at l/d 28–36, beams 13–20.
- effective span β: simply supported 1.00, continuous end span 0.80, interior 0.70, **cantilever
  2.50**, flat slab 0.85 × larger span.
- deflection: final **≤ l/250** general, **≤ l/500** under brittle finishes/partitions (DIN 4103
  lineage); cantilever effective l = 2.5 × geometric. Concrete creeps — long-term ≈ 2–3×
  immediate with no compression steel; this, not strength, sets most house slabs.

---

## Section 5: Stability and Bracing (Aussteifung)

### 5.1 Where horizontal force comes from

Wind on faces (pressure + suction, zone-dependent — German v0 = 22.5–30 m/s bands, simplified
qpb ≈ 0.5–1.0 kN/m² for low buildings, §6.5), seismic inertia (§14), imperfection/notional forces
(verticality deviation θ ≈ 1/200 family, applied by the engineer), and user loads (parapet/railing,
partition push 0.5–1.0 kN/m at 0.9–1.2 m — DIN 4103 lineage). For low-rise buildings wind usually
scales with exposure, not height; **uplift on light roofs and suction on free walls/parapets
(cp up to ~2.3 on corner zones of free walls) are the checks people skip.**

### 5.2 The bracing menu (choose, then reserve the space)

| Bracing type | Where it lives | Notes |
|---|---|---|
| Shear wall panels (Scheiben) | staircase walls, party walls, perimeter bands | masonry or RC; needs vertical load on it (§5.7) |
| Core (Kern) | stair/lift box | closed box = high torsional stiffness; best single element |
| Braced bay (Verbund) | end bays of halls, façade lines | cross/chevron/portal bracing; end bays give shortest load paths, mid-bay bracing allows thermal movement |
| Rigid frame (Rahmen) | where diagonals are unacceptable (shops, glass) | portal (steel/timber/glulam) or RC moment frame; node cost |
| Horizontal bracing / self-bracing disc | roof planes, floors that are not plates | diagonal/ring pattern in plane; cast plates and CLT are discs if edge members carry them |

**Layout rules that prevent most stability errors:**

- Bracing in **both** directions; element axes **must not all intersect in one point** (free
  torsion otherwise); aim for redundancy (more than three non-parallel/non-concurrent lines).
- Keep the **stiffness centre near the mass centre** — all the solid walls on the party-wall side
  and glazing on the other = torsion (classic corner-plow MFH, §18).
- Distribute storey shear **by stiffness**, not by length or goodwill: a long stiff wall takes far
  more than its share; shear-deformation matters on stocky walls (concept; numbers in
  `structural-analysis` / bracing chapter).
- A bracing wall must be **loaded vertically** to develop shear (friction + compression zone);
  rotate floor spanning direction across storeys so bracing walls keep receiving load.
- Central core → free radial slab movement (good); end cores on a long building → restraint
  cracking → expansion joint near the core releasing the slab in one direction.

### 5.3 Diaphragms and collectors

- A diaphragm is only as good as its **boundaries**: edge members/tie beams, chord forces at the
  perimeter of the bracing zones, and collectors that gather floor forces and deliver them into
  walls/cores.
- Every opening larger than roughly a sixth of the floor dimension gets a **collector all round**.
- Sloped roofs are not diaphragms unless braced (diagonal boarding, panels, or ties); purlin roofs
  need the plan-bracing pattern (or the ceiling below acts as disc — with its own bracing).
- Bar systems (joists, rafters, grids) always need one of: triangulated mesh, diagonals engaged at
  nodes crossing the longitudinal members, shear sheathing with a tension ring anchor around it, or
  frame action. Repeated node connections = an equivalent rigid panel (effective diaphragm).

### 5.4 Nodes: rigid vs pinned (Gelenk vs Rahmeneck) — the concept choice

- **Pinned nodes + bracing** = statically determinate chains: forces independent of stiffness,
  settlement-tolerant (precast loves this), but **zero redundancy** — one missing element =
  mechanism, so ties (§13) are the price of determinacy.
- **Rigid nodes** = redistribution, redundancy, monolithic robustness — but the forces then depend
  on stiffness ratios, temperature/settlement cause secondary moments (Zwang), and the joints cost
  money/welds/formwork.
- Steel/portal: put the rigid corner where moment is small (or accept haunched moment corner);
  erection joints near contraflexure; three-hinged halves halve transport for tall portals (≤ ~4 m
  per half on road transport, classic limit).
- Timber: node ductility is in the fasteners — steel brackets/angled cleats; **never bear timber
  across grain in a long-term node** (creep settlement); end-grain to end-grain for stacked columns.
- Precast: cleat = pin; grouted sleeve/PT = moment; "rigid precast nodes exist but cost" — design
  the system as you detail it.

### 5.5 Ring beam and ring anchor (Ringbalken / Ringanker) — masonry logic

The element that makes a wall house act like one box:

- **Function:** tie the diaphragm edges + wall heads into a closed horizontal loop → distributes
  bracing forces, holds walls together at corners, prevents out-of-plane peel-off, carries
  membrane tension around openings/voids.
- **Requirement triggers (DACH practice):** more than 2 storeys; building length > ~18 m; large
  openings/weak façades; unfavourable ground; **always in seismic regions** (§14).
- **Capacity concept:** designed as a tie, German NA practice floor ≈ **70 kN** force capacity per
  ring anchor, within ≤ 1.2 m of the wall edge; RC ring ≤ ~30× slab thickness span ratio band.
- **Cantilever/slab edge rule:** ring beam must close around cantilevered floor edges; the
  connection (wall ties, Lagerfuganker) is what makes a two-leaf wall act compositely (design
  forces per element type in `masonry-construction`).
- Gables are **not** tied by gravity: confine them (posts + raking beam or light timber gable),
  brace them against wind (suction tears gables outward).

### 5.6 Bracing by roof type (pitched, DACH default for EFH)

```
Purlin roof (Pfettendach):    rafters bending, H≈0 — system needs own stability (wind posts/
                              diagonals, braced end bays); rafter spacing ← laths ← tile+overlap.
Rafter roof (Sparrendach) untied: ridge without tie = arch → thrust into wall head — NEVER on
                              unrestrained masonry; use collar/ceiling tie (Zugband), truss, or
                              designed ridge beam (rafters simple, H=0).
Truss roof (Bundt):           self-equilibrating, vertical reactions only; brace the plane and
                              anchor EVERY truss to the ring beam (uplift chain).
Snow (Alpine): valley/parapet drift μ 1.6–2.5+; design the unshed case.
```

### 5.7 Non-sway is a choice, not a default

Braced by walls/cores → near-nondeformable, second order small; pinned precast and flat slabs work.
Unbraced skeleton → moment from every imperfection: the "cheap frame" becomes the expensive
one. Want the open plan? **Buy the bracing explicitly** (core, wall band, braced bay, PT);
verify θ/K1 in `structural-analysis`.

---

## Section 6: Design Loads (Einwirkungen — EN 1990/1991 essentials)

### 6.1 Unit weights (Wichte, kN/m³ — EN 1991-1-1 / DIN 1055 tradition)

| Material | γ |
|---|---|
| Steel | 78.5 |
| Reinforced concrete (Stahlbeton) | 25 |
| Plain concrete | 24 |
| Lightweight concrete by class | 9–20 |
| Cement/lime-cement mortar | 19–23 |
| Masonry: normal units RDK 1.4–1.8 | 16–18 (e.g. KS 24 ≈ 18 with plaster allowance; HLz 12 ≈ 14) |
| AAC (Porenbeton, unreinforced slab) | 5–9 by RDK |
| Roof coverings kN/m² incl. battens | clay/concrete tile 0.45–0.95 (standard 0.50–0.65);
  fibre-cement 0.2–0.4; trapezoidal steel ~0.15–0.30 (manufacturer) |
| Plasterboard / plaster | GK ~10; plaster KZ 20 mm ≈ 0.40 kN/m² face |
| Screed (Zementestrich) | 22 → 0.22 kN/m² per cm; anhydrite 0.20 |
| Tiles/natural stone floor | 0.22–0.30 kN/m² per cm |
| Timber solid / board products | 3.7–10.8 (C-classes 3.7–5, D-classes 6.4–10.8, OSB ~7) |
| Water | 10 |
| Backfill (compacted) | 18–20 |

**Quick build-ups** (kN/m²): slab 20 cm → 5.0, 25 cm → 6.25; screed 5 cm + tile 1.3–1.5; flat-roof
insulation+membrane 0.6–1.2; ceiling+services 0.25–0.4; pitched tile roof (no rafters) 0.9–1.3.

### 6.2 Imposed loads (Nutzl last, EN 1991-1-1/NA characteristic qk | Qk)

| Category | Use | qk kN/m² | Qk kN |
|---|---|---|---|
| A2 | living rooms **with** cross-distribution (ribbed/plate) | 1.5 | — |
| A3 | living without cross-distribution (one-way strips) | 2.0 | 1.0 |
| B1/B2 | offices, corridors, practices / heavier kitchen-corridor use | 2.0 / 3.0 | 2.0/3.0 |
| C1–C4 | assembly (cafés 3.0; fixed seating 4.0; museums 5.0; sports/stage 5.0) | 3–5 | 4–7 |
| D1/D2 · E1.1/E1.2 | retail small/large · light workshop / storage (minimum!) | 2.0/5.0 · 5.0/6.0 | 2/4 · 4/7 |
| F1 | garages, cars ≤ 30 kN (Q: 20 kN axle alt.) | 3.0 (→ ≤2.5 allowed for load take-down to foundations) | — |
| T1 / T2 | stairs dwelling-office / others | 3.0 / 5.0 | 2.0 |
| Z | balconies, roof terraces, loggias | 4.0 | 2.0 |
| H | roof — non-accessible (maintenance) / accessible as terrace | 1.0 person load | terraces take Z 4.0; terrace live and snow are **not** combined (German NA validity rule); no maintenance-person superposition with snow |

**Partition surcharge (Trennwandzuschlag):** movable/undefined light walls ≤ 3 kN/m → add
**1.0 kN/m²** to qk; heavier partitions → own line load; no surcharge needed where qk ≥ 5.0. This is
the DACH way to handle "future walls" — use it instead of guessing wall positions.

Multi-storey reduction of imposed load toward the foundations exists in the NA (factor by number of
loaded storeys and category — concept only here; **VERIFY** current formula with the engineer).
Do not combine reduction with ψ-reduction for the same action.

Forgotten permanent loads: thick screed (+0.2/cm), stoves, roof plant, PV (0.15–0.30 + uplift
surface), water tanks, parapet lines, soil on raised slabs (18–20 kN/m³), snow drift.

### 6.3 Snow (Schneelast, EN 1991-1-3 + NA) — the Alpine differentiator

```
sd = ce · ct · μ · sk
sk: zone base value + altitude correction. German NA altitude form (examples recovered):
    zone 2: sk = 0.25 + 1.91·((A+140)/760)²   → 300 m: 0.89 (min 0.85 governs)
    zone 3: sk = 0.31 + 2.91·((A+140)/760)²   → 750 m: 4.30 kN/m²
    (A = altitude m; map/NA must be read per site — VERIFY; AT/CH differ entirely, SIA 261)
μ1 flat ≤ 10° = 0.8 (many NA give 1.0 small-cold — VERIFY); μ3 valley = 1.6 (cap γ·h/sk + μ2);
slip on slopes ≥ ~40–45° → μ2 falls but valley + eaves drift (Schneefang) stay;
adjacent higher roof sheds onto lower: drift width min(5 m…15 m), μ up to cap 2γh/sk (worked
examples exist in `structural-analysis`).
Terrace live load Z and snow are NOT combined (German NA).
```

### 6.4 Wind (EN 1991-1-4 + NA)

```
German wind zones WZ1–4: v0 = 22.5 / 25 / 27.5 / 30 m/s (q0 ≈ 0.32–0.56 kN/m²).
Simplified constant qp for low buildings ≤25 m (inland): WZ1 h≤10 m: 0.50; WZ2 0.65;
WZ3 0.80; WZ4 0.95 kN/m² (+coastal steps up to 1.25–1.40) — VERIFY current NA table & exposure.
cp: walls +0.8 windward / −0.5…−0.8 leeward/side (zones A–E with corner suction); flat roof
corner zones F/G −1.2…−2.0 with parapet geometry; free-standing walls/parapets up to ~2.3
(zones A/B/C/D). Internal pressure ci for "close to open" buildings can flip the sign on roofs.
Uplift chain for LIGHT roofs: sheeting→purlin→brace→truss→anchor into ring beam→wall→foundation
hold-down. Corner/edge fixings closer than field. Overhangs see pressure both faces.
```

A heavy RC roof (5–8 kN/m² dead) essentially never uplifts; a tile/sheet roof on timber must be
checked as a held-down structure (and is the reason the truss-to-ring-anchor connection is a
designed joint, not a nail).

### 6.5 Combinations (EN 1990) — carry these two bands everywhere

```
ULS persistent (STR):    Ed = 1.35·Gk (+ 1.35·other perm) + 1.50·Qk,1 + 1.50·ψ0,i·Qk,i
Overturning (EQU):       destabilising 1.10·Gk + 1.5·Qk ≤ stabilising 0.90·Gk   (never mix the two Gs)
SLS characteristic:      Gk + Qk,1 (+ ψ0 Qki) · frequent: Gk + ψ1 Qk,1 · quasi-perm: Gk + ψ2 Qki
ψ (buildings): A/B 0.7/0.5/0.3 · C/D 0.7/0.7/0.6 · E 1.0/0.9/0.8 · F 0.7/0.7/0.6 · snow ≤1000 m
               0.5/0.2/0.0 · wind 0.6/0.2/0.0 · H 0/0/0
Partial factors (material, German NA): concrete γc 1.5 · steel rebar γs 1.15 · structural steel
γM0 1.0/γM1 1.1 · timber γM 1.3 · masonry γM 1.5 (1.3 favourable) · exceptional γ 1.0-family
```

**Factored (ULS) for member strength; service/unfactored for ground bearing and deformation.**
Write which one sits next to every number you produce — mixing them is the most common hand-calc
error in every country.

### 6.6 Design values of materials (retag anchors)

| Material | Useful design values |
|---|---|
| Concrete | fcd = αcc·fck/γc: C20/25 → 11.3; **C25/30 → 14.2; C30/37 → 17.0**; C35/45 → 19.8 N/mm²; Ecm 30–33 GPa |
| Rebar | B500A/B: fyd = **435 N/mm²**; ductility: B (ribbed) for redistribution |
| Masonry | fk by unit+mortar (e.g. HLz 12/M10 ≈ 5.6 → fd = 0.85·fk/1.5 ≈ 3.2 N/mm²); Ec ≈ 850–1100·fk |
| Timber | C24: fm,k 24, fc0,k 21, E0,mean 11 GPa; **kmod** cuts strength long-term 0.50–0.60 (NKL1) |
| Steel | S235/S355 fy 235/355; E = 200–210 GPa; fire + corrosion = detail decisions |
| Unit strain αT | steel 12, concrete 10, masonry 6–10, timber ⊥ grain 25–60 (×10⁻⁶/K) — differential movement joint spacing follows (§13.6) |

---
## Section 7: Storey Load Take-Down Template (Lastzusammenrechnung)

The procedure behind every column, wall and footing number. Run it explicitly whenever "will this
carry" is asked.

### 7.1 The six steps

```
STEP 1 — Tributary area of the element at each level
   interior column: half-span to each neighbour both ways; edge: half inward, edge outward;
   wall line: (left span/2 + right span/2) per metre run; beams: catch the slab areas.
STEP 2 — AREA loads per level (from §6 tables):
   floors: slab + build-up + surcharge;  roof: slab + waterproofing + insulation (+snow own case)
STEP 3 — LINE and POINT loads sitting on/near the element: over-wall self-weight × height,
   beam weight (b·h·25), façade weight, tank/plant point loads, stair flight reactions.
STEP 4 — Element's own weight per storey: column b·h·H·25; wall t·H·γmasonry.
STEP 5 — Accumulate DOWNWARD storey by storey; different qk per storey stays separate until
   the combination step (do not pre-sum ψ).
STEP 6 — Produce and LABEL both numbers:
   N_Ed = 1.35·G + 1.5·Q(+ψ) → member strength   |   N_serv = G + Q → soil bearing & masonry
   Sanity band: residential floors land ≈ 9–12 kN/m² factored, ≈ 7–10 service per storey.
   A 36 m² tributary MFH floor column ≈ +350–450 kN/storey factored. 3× → double-counted;
   ⅓ → forgotten finishes or walls.
```

### 7.2 Per-storey quick loads (typical bands)

| Level | gk (slab + finishes + walls averaged) | qk | service g+q | ULS 1.35g+1.5q |
|---|---|---|---|---|
| MFH dwelling floor (22 cm) | 7.0–8.0 | 2.5 (A2+surcharge) | 9.5–10.5 | 13.0–14.5 |
| MFH roof (20 cm + build-up) | 7.0–7.8 | snow own case (never with Z) | ~8.5 | 11.5–12 |
| Office floor (22 cm) | 7.0–7.8 | 3.2 (B1+1.2 partition) | 10.2–11.0 | 14.0–15.5 |
| TG ceiling (25 cm) | 8.25–8.75 | 2.5 (reduced take-down ok) | 10.75–11.25 | 14.7–15.4 |
| Stair well landings | +0.6–1.0 over flight plan | T1 3.0 | — | — |

(Office example from German practice: 25.0 × 10.5 m storey → Gk ≈ 2280 kN, i.e. ≈ 8.7 kN/m² —
in-band with the table. Add the bracing self-weight separately when cores count on it.)

### 7.3 Screening formulas you may quote (label: preliminary)

```
Column:   νEd = N_Ed / (Ac·fcd) ≤ ~0.5 → section OK for preliminary, else grow or upgrade class
          (fcd: C25/30 = 14.2 N/mm² ⇒ capacity ≈ 14.2·ν·Ac: 40×40 C25/30 ≈ 1250 kN "easy")
Wall:     design via EC6 simplified (σRd = cA·fd) — masonry-construction skill; preliminary:
          24 cm KS/M5 carries ≈ 200–300 kN/m per storey stack band comfortably to 3 storeys
Footing:  A ≥ N_serv / σR,d (presumptive, DIN 1054, §12.3); keep e ≤ b/6 (kern) under all combos
Punching: every flat slab column, both directions of load take-down (interior β = 1.10, edge 1.40,
          corner 1.50 — moment-transfer factors) — flat slab is a punching design wearing a floor.
```

---

## Section 8: Masonry Systems in Detail (handoff to `masonry-construction`)

### 8.1 Wall-building typologies (the plan decides the structure)

| Typology | Load path | Plan freedom | Notes |
|---|---|---|---|
| Cross-wall / box (Zeilenbau) | floor spans across, bears on parallel walls (box = closed cells, all walls equally loaded) | outer wall openable; walls = apartment width; least plan freedom in box form | heavy party walls (acoustic + fire gold); free gable ends need edge restraint: floor disc + bonded piers; decouple between units |
| Perforated-façade (lochscheibe) | plate floors on grid of walls + piers | good | pier minimums §8.4; needs ring anchor + collectors |
| Detached shear plate (Plattenbau frei) | RC piers at free panel ends | high | tensile-capable panels; concrete does what masonry cannot |

### 8.2 The three checks a concept designer runs (then hands on)

1. **Does the wall stack?** Bearing walls vertical, storey on storey; floor spans rotated to keep
   load on bracing walls.
2. **Crushing at the critical level** (plinth/ground): service stress vs capacity — for 1–2 storeys
   this is comfortable and thickness is set by slenderness/buildability; **the 3rd storey is where
   masonry gravity starts to bite** (thicker/stronger units at ground floor) — the reason EC6
   simplified stops around 3 storeys (h ≤ 2.75–3.6 m per table, t ≥ 11.5–24 cm, qk ≤ 5, slab span
   ≤ 6 m, ≤ 20 m tall — VERIFY table pairings in `masonry-construction`).
3. **Enough wall in both directions?** Ratio of bracing wall area to floor area per direction,
   checked per storey; symmetric layout. Low-hazard simple house: ≳ 2–3 %; confined-masonry in
   moderate seismic: ≳ 4–6 % (§2.2.B band — screening only, VERIFY vs EC8-3/seismic-design).

### 8.3 Confined-masonry buildability checklist (the system lives or dies here)

1. **Wall first, confinement second** — toothed (verzahnt) vertical edges, then pour the tie-column
   against the toothing. Smooth cold joint = you paid for CM and built URM.
2. Tie-columns **continuous from foundation to roof ring**, starter bars from the slab-on-grade/
   footing; a tie-column starting at first floor is decoration.
3. Tie-column at every corner, junction, free end, both sides of openings > ~1.2 m, spacing ≤ ~4 m
   / ≤ 1.5·storey height.
4. Ring/tie beam at **every** floor and roof, closed loop, internal walls too — a perimeter-only
   ring cannot deliver floor force to interior shear plates.
5. Slab bears on the ring beam, not on brick at confined levels; 11.5 cm partitions carry nothing —
   never show them under a bearing.
6. Mortar class per statics (no lime-only in bearing walls where the NA demands MG II+); full
   bed-joint filling; braced fresh walls ≤ ~1.2–1.5 m lift/day.
7. Parapets and gables get the same confinement; an unconfined 1 m parapet is a roof-edge
   projectile.
8. Bed-joint reinforcement (ladder wire) every few courses is the cheap upgrade where the NA/EC8
   detailing asks for it — stitches diagonal cracks after they form.

### 8.4 Openings and piers (perforated façade rules)

| Rule | Value |
|---|---|
| Min pier between two openings | ≥ 600 mm and ≥ ~¼ of adjacent opening height |
| Opening edge to corner/tie-column | ≥ 600 mm (else corner pier fails in shear; put the column there) |
| Opening area per storey per wall | ≤ ~40–50 % of length; stack openings floor-to-floor (offsets = shear breaks) |
| Window height | free *if* the parapet strip keeps plate/rack action — keep the strip, then the height is architecture's |
| Full-height glazed line | splits panel — two halves levering against tipping; needs piers or frame |
| Lintels | flat brick lintel = arch-compression-chord + steel tie (carries only the ~triangle above within EN 845-2 logic); RC/steel lintels as beams concentrate reveal stress and crack render under thermal delta; room-height openings: slab edge acts as lintel with local top steel |
| Chases/slots | milled not hammered; within installation zones; never in horizontally-perforated units or near bearing; a 10 cm vertical chase in a 24 cm wall removes 40 % of its section exactly where shear lives |

---

### 8.5 Basement logic

Prescriptive EN 1996-3 masonry basement band exists (h ≤ 2.60 m, t ≥ 20 cm, slab as
diaphragm, no groundwater — VERIFY in `masonry-construction`); water or deeper → RC Weiße
Wanne (`concrete-detailing`). Timber: mineral plinth ≥ 30–50 cm up, drained, splash-zone detail.

## Section 9: Timber Systems in Detail (handoff to `timber-steel-design`)

### 9.1 The ground rule

Timber rises off the ground on a mineral base (elevated plinth/Sockel) → rot protection. Consequence:
**bracing against horizontal load cannot rely on footing friction or mass — the structure itself
must rack.** Every system below has an explicit shear-panel or core answer plus a hold-down chain.

### 9.2 The five wall systems by bracing principle

| System | Vertical | Bracing | Where |
|---|---|---|---|
| Log / post-and-plank | stacked members or corner posts | corner notches, lacing, applied angle braces (post-plank) | alpine vernacular / transitional |
| Half-timbered (Fachwerk) | storey trusses, infill non-structural | integral diagonals (lap joints + pegs); upright grid ≈ 1.25 m so a door+window fit without removing a post | heritage, infill urban |
| Timber-frame panel (Ständerwerk) | dense slender studs along grain | **shear-stiff board sheathing replaces diagonals** | the DACH standard |
| Solid timber (Massivholz) | full-section plates, end-grain stacked | plate in-plane shear (CLT excellent as disc and as wall) | 3–5+ storeys |

### 9.3 Platform vs balloon vs solid — pick the section logic

- **Platform (US-style Geschossweiser Tafelbau):** storey-high walls → joists on top plate → rim
  joist anti-tilt → deck → next storey's walls stand on the deck. No continuous stud; fire-stop
  at each floor line; wall height = one storey → transport-friendly; the default for industrialised
  DACH housing (Fertighaus).
- **Balloon (through-storey studs):** studs run two storeys, joists on let-in ledger (spans 4–5 m);
  continuous vertical line, fewer storey joints, but two-storey panels on trucks and careful
  service/fire detailing at the ledger.
- **Solid (CLT/Brettsperrholz EN 16351):** odd plies, outer layers one way → defined main span
  direction; only ~50 % of section effective along grain in walls; superb diaphragms; elements to
  16–20 m; TBE (technisch bebilderte Elemente) plant pre-cut; stack forces **end grain to end
  grain** (no transverse compression) — that is what lifts timber above the 4–5-storey sleeper-
  settlement ceiling of joist-on-plate stacking.
- Board-stacking (BSP): racking only via glued edges; LVL: strongly one-way, linear supports.
- Panel formats: large-format to ~10 m (transport) → few joints → wind + air tightness nearly free.

### 9.4 Nodes, settlement, and the storey ceiling

- Force through **sleeper + head plate = transverse compression = long-term creep settlement** —
  that stack limits traditional joist floors to ~4–5 storeys; end-grain stacking (solid timber),
  steel inserts, or bearing on the lower column segment are the high-rise answers.
- Wall-floor node menu (design vocabulary): steel Z-cleat on wall (load along wall grain — good for
  height, protect fire); timber ledge/trimmer; recess in wall head (weakens section, low-rise);
  slab embedded in wall plane (low-rise unless concrete dowels); wood-concrete nodes (protruding
  concrete flange or edge beam — load path through concrete, no timber perpendicular-to-grain).
- **WCC floors (Holz-Beton-Hybrid):** timber tension chord + concrete compression chord via pins/
  notches/flat-steel in saw cuts; concrete gives fire, mass, acoustic, stiffness; timber is the
  formwork; watch moment reversal at continuous supports (bonded composite resists badly).
- Bracing chains: panel → hold-down at each end → sole plate → foundation tie; roof disc
  (boarding/CLT) + rake braces; gable triangles need their own plane bracing.
- Fire: add char allowance (≈ 0.7 mm/min superficially — detail in `timber-steel-design`) to the
  static section; planar CLT soffits reach high REI with board skins, no ceiling needed.
- Acoustic: mass is missing by nature — floating screed on CLT / loose-bound chippings / WCC are the
  standard fixes (see `building-acoustics`).

---

## Section 10: Steel and Composite in Detail (handoff to `timber-steel-design`)

### 10.1 Why steel is chosen (and why it becomes expensive)

Slender, tough, precise, prefabricated, dry, demountable, fully recyclable. The two taxes are
**fire** (strength collapses at temperature — protection: intumescent, board cladding, sprinklers,
water-filled or concrete-encased profiles) and **corrosion** (open fine sections worst, closed tubes
best; hot-dip + duplex coatings). Price the taxes at concept stage or they arrive at tender.

### 10.2 Connection culture = structural system

```
Pinned + braced:  fin-plate / flush end-plate bolted; base plate + anchors = pinned foot;
                  lugs cast/fabricated; two-shear beats single-shear for eccentricity
                  → fast site, cheap nodes, needs bracing space + ties for robustness
Rigid/portal:     welded or bolted moment corners; haunches where M is big; erection joint at
                  contraflexure to dodge the worst corner moment; needs sway/frame analysis
Semi-rigid:       real behaviour between — only with verified rotational capacity, don't assume free
```

Multi-storey unbraced steel frames are **pliable** (Vierendeel-type action) → without extra bracing
they suit mid-rise only; rigid nodes then serve to couple twin cores and limit drift/vibration.

### 10.3 Composite floors (Verbund) — the mid-rise workhorse

- Trapezoidal sheet = permanent formwork + lateral restraint to beam bottom flange + working deck;
  shear studs make slab+beam one unit: concrete compression chord, steel tension → shallower beams
  at mid-spans; EN 1994 logic.
- **Slim-floor:** flush (shallow) beam whose lower flange carries precast units on a shelf — flat
  soffit, services run freely below the structure (service renewal is faster than structure —
  let the services win).
- Multi-storey office rhythm: sheet span 3–4 m between secondaries, secondary beams 6–9 m,
  braced bays or cores at regular grid, concrete-topped deck as diaphragm with perimeter members.
- Roof of halls: plain trapezoid sheeting for low loads (with the build-up of `roofing-waterproofing`
  — gravel ballast / foil / mineral wool cross-laminated layers).

### 10.4 Halls: portal frames and trusses (Einhallen-/Mehrfachhallen)

| Parameter | Value |
|---|---|
| Portal bay | ~ 12–15 m on standard hot-rolled, haunched; deeper with cranes |
| Frame action | 2-hinged (feet pinned; needs rigid corner node), 3-hinged (apex pin: erect from two ≤ ~4 m halves), fixed (crane halls), asymmetric |
| End façade | portal plane needs no bracing → open glazed gables; the **tipping direction** braced by roof diagonals + wall vertical bracing in the same bays |
| Trusses | triangulate (quads need rigid nodes = Vierendeel: heavier, only where openings demand); load at nodes only; compression bars short; tension diagonals preferred; no twin compression bars; avoid acute angles; axes concurrent |
| Purlins | 1.2–1.5 m along the slope, C/Z cold-formed 150–250; pitch: sheet lap ≥ 3° (metal), tile ≥ ~20–22°, snow-shed ≥ 30° |
| 3-chord tubular trusses | torsion-stiff, tilt-resistant, buckling-friendly — the honest long-span answer |
| Bracing zones | vertical cross-bracing end bays (short load paths), mid-bay when thermal movement matters; ridge/belt ties between frames until cladding makes them compositely stiff |

---

## Section 11: Precast & Industrialised Systems (handoff to `concrete-detailing`/`construction-scheduling-site`)

### 11.1 Why precast changes the statics, not just the schedule

Factory: weather-independent, controlled quality, HPC/fibre possible, reusable formwork amortised,
24-h cycle with heat treatment. Consequences the concept designer inherits:

- **Mostly pinned = statically determinate**: settlement-insensitive, no redistribution — every
  load case has a path *today*, and robustness comes from **ties, not redundancy** (§13.4).
- Rigid erected joints are expensive → do not design the building as a frame if you erect it as
  a stack of pins.
- Smaller tolerances, higher planning cost and lead time: the **grid is contractual** — modularity
  ripples through every trade; variants after shop drawings cost real money.

### 11.2 The element kit

| Element | Data |
|---|---|
| Hollow-core floor (Hohlplatte) | 160–500 mm, 1200 wide; span/depth ~ 30–40 (VERIFY supplier); side grooves + cement grout key = transverse shear; bearing on ledges ≥ ~70–100 mm; **not a diaphragm until topped/tied** |
| Double-tee / channel | long floor/roof spans, exposed soffit |
| Solid wall panel (Vollwand) | storey-height 12–16 cm basement/shear walls; grouted sleeve couplers (Muffen) for vertical bars |
| Sandwich element | wythes + factory core; connectors (insul GFRP/SS) carry shear only; wythe design per EN 14992 logic — service lives differ inside one element |
| Columns | continuous multi-storey bars or grouted couplers; cast lying then tilted → **transport/erection cases ≠ service cases**, erection may crack the top fibre (pretension closes it later) |
| Stair flights | factory, pinned landings, still contribute to bracing if grouted — assume nothing, ask |

Formwork physics worth knowing: lying-cast gives the best compaction but one rough screeded flat
face (no protrusions there); cleats on 3–4 sides force upright cast; extraction formwork needs
draft angles and chamfers; pretensioned bed-cast = **single spans, no cantilevers, no coffered
ribs** (strip jamming); post-tensioning restores continuity and lets segmental stitching build
long girders on site.

### 11.3 Erection axioms

Self-stable the moment the hook is off: form-fit gravity bearing (cleat on elastomeric pad +
centring pin; tooth/pocket tilt-locks; CG below the bearing plane). Uniform element weights → even
crane utilisation. Braced/shored until the moment frame of the *erected state* is complete — the
building is a mechanism for its first days; write the temporary-bracing plan as part of the system
(`construction-scheduling-site`). Panel upright transport ≤ ~4.0 m storey height.

### 11.4 Precast vs cast-in-place decision (and hybrid honesty)

| Driver | Choose |
|---|---|
| repetitive grid, ≥ ~200 same floors, speed, weather | precast |
| bespoke plan, transfers, watertight complex basement, sculptural soffit | cast-in-place (monolithic redundancy is real: integral RC handles local damage best) |
| both | hybrid: precast floors + cast cores, sandwich walls + cast plinth — then detail the junctions as designed collectors/ties, not as hope |
| unitized/half-precast (Halbfertigteil) floor: precast bottom shell as permanent form + cast topping | the compromise that keeps formwork labour out and monolithic behaviour in |

---

## Section 12: Foundation Interface (Gründungsflächen — handoff to `geotechnics-foundations`)

The structure's last metres: convert line/point loads into an area the inspected ground accepts,
with a path for horizontal force and overturning, and with movement tolerance.

### 12.1 Selection tree

```
Geotechnical report exists? ──NO──► STOP. DIN 4020 exploration (GK 1–3 difficulty class).
│
├─ σR,d (DIN 1054 simplified, presumptive band) at planned depth:
│   ≥ ~300 kPa   dense sand/gravel, stiff clay, weathered rock → strip (walls) / pad (cols), min sizes govern
│   150–300      medium ground (most DACH buildable till)      → strip/pad sized by calculation
│   80–150       soft/loose                                     → widening footings start overlapping → raft or
│                                                                improvement (compaction, replacement, cement columns)
│   < 80 / peat / fill / artesian water                        → piles or raft+improvement; no shallow bets
├─ Water table above slab formation → waterproof slab: Weiße Wanne (WU-RL) or tanked (Blaue
│   Wanne); buoyancy (UPL) check the raft: 1 m head = 10 kPa up
├─ Basement + neighbours → excavation support (spund/wall/anchors) — separate design topic
└─ Seismic → found all units at one level where possible; tie the base slab/ring; storey mass
     change (steps) needs the foundation stepped too
```

### 12.2 The ground is also a load

Ground moves (frost heave where water can't drain — found below frost, at least 0.80 m by DIN 1054 (S.1), DACH practice ~0.8–1.2 m VERIFY
region, or drained/filtered), pushes (at-rest/active/passive earth pressure →
`geotechnics-foundations`), and loses strength when saturated. σz spreads ~1:1.5–1:2 bulbs; soft
lenses → tilt; settlement = immediate + consolidation + creep.

### 12.3 Presumptive bearing — the DIN 1054 anchor (Table 1/2 family, kN/m²)

Non-cohesive, settlement-insensitive, d = 1.0 m, width 0.5 → 3.0 m band: **~ 280–520**;
d = 2.0 m: ~ 340–700; cohesive stiff (UL): 180–210 at d = 0.5 m rising with depth. Saturation at
base **−40 %**; investigate rather than trust the table. These are screening numbers for concept
massing (TG vs pads vs raft decision) — **the design resistance is the engineer's, from the
site report**. (Full grid + reduction rules live in `geotechnics-foundations`; VERIFY editions,
AT/CH differ.)

### 12.4 The three checks every footing carries (concept-level)

1. **Bearing** service: σ = N/A (±M/W) ≤ σR,d; eccentric load: uniform if e ≤ b/6 (kern),
   edge zero at e = b/6, **tipping risk beyond e = b/3**; e = M/N; outside kern → σmax =
   2N/(3·(b/2−e)·a) on the compressed length.
2. **Overturning/uplift**: 1.10·G_dst + 1.5·Q ≤ 0.90·G_stb (EQU factors — corner pads of frames in
   seismic zones can go into tension: they need mass or tie-down, not hope).
3. **Shear + moment into soil**: base friction μ ≈ tan φd′ (cohesion-free interface is the safe
   assumption); passive wedge only if the footing can actually move. Reinforcement geometry and
   one/two-way pedestal action: `concrete-detailing`/`structural-analysis`; strip projection
   ≤ its depth or design the bending strip.

### 12.5 Ties at foundation level

The footing system is part of the tie chain: ground-bearing slab or foundation ring beam
(Grundzugsbalken) tying every pad to its neighbours, strip under every wall, matched founding
depths across any material boundary (§2.4-4); legacy seismic practice floors: foundation beams and
wall footings with ≥ 4Ø12 continuous bars (DIN-era figure, indicative — VERIFY current NA/EC8).

---
## Section 13: Robustness and Continuity (Robustheit, Verbund)

### 13.1 What robustness means at concept stage

A robust structure survives the unexpected: a removed wall panel (impact, explosion, progressive
local failure), an underestimated load, a construction error. Two families of response:

- **Redundancy / alternate load path (Ersatzlastweg):** after local loss the load finds another
  way — needs continuity + ductility; determinate systems have none. **Redundant + sufficiently
  ductile** is what unlocks redistribution (and relaxed partial factors, EN 1990 logic).
- **Notional ties:** explicit minimum tie forces in every direction through every level, whether or
  not analysis "needs" them — the cheap insurance turning a pile of elements into one box.
- System truth: brittle fibres gain (or lose) little from repetition; plastic ones scale — **ductile
  behaviour is the precondition for robustness**, hence codes redistribute ductile systems and stand
  brittle ones on determinacy + ties.

### 13.2 The tie-force concept (EN 1991-1-7, presented generally — VERIFY table values)

Minimum tie forces in buildings, as a force each tie element must resist:

```
internal horizontal ties   grid ≤ ~1.5 m from free edges, ≤ ~4.5 m spacing, Ft ~20–70 kN (floors)
peripheral ties            every floor/roof edge + around openings, ≥ internal (ring-anchor
                           practice: 70 kN at floor level, German NA)
vertical + transverse ties perimeter/vertical joints, full height; adjacent elements tied together
key elements               where no alternate path is practicable: accidental combination (notional
                           ~100 kN point family) without collapse
```

The exact magnitudes are code-table values — present them conceptually here; the engineer picks
them from the current EN 1991-1-7 + NA (the 70 kN ring-anchor figure and the ≥ 1.2 m edge-distance
convention are the German-NA anchors this skill actually carries). For the actual EN 1991-1-7
Annex A formulas behind this (T_i = max{0.8·(g_k+ψ·q_k)·s_t·L; 75 kN} internal,
T_p = max{0.4·(g_k+ψ·q_k)·s_t·L; 75 kN} peripheral), plus numeric accidental-action values
(consequence-class height thresholds, vehicle/forklift impact forces), see `structural-analysis`
§10.1.

### 13.3 Continuity details that make the concept true

- Cast-in-place monolith: the slab is the tie by default — top-and-bottom steel continuous over
  supports, edge members with real bar continuity (lap/anchor, not butt).
- Masonry: ring anchor closed at corners (bent bars, not butt ends), walls bonded/toothed at
  junctions (Zahnverband) or with bed-joint anchors; a toothing acts compositely, a butt joint
  needs connectors.
- Timber: hold-down + chord splices at panel ends, deck diaphragm nailing pattern designed,
  bottom-plate anchors into the ring.
- Steel: continuity in the deck (studs), bracing engaged at nodes with the members, base plates
  with anchor groups designed for tension not just shear.
- Precast: the determinacy trade — **every joint is the design**: bearing + mechanical connector +
  vertical tie through stacked elements + floor-to-wall connection + roof diaphragm ties. Untied
  planks behave like loose boards in the one event that tests them.

### 13.4 Robustness in determinate (pinned/precast) systems

Pinned systems are settlement-tolerant and honest about forces — but have no second path: the tie
hierarchy is **mandatory, not optional**, and the bracing layout must stay analysable after one
element is hypothetically removed (a designer conversation, not always a code box).

### 13.5 Geometry habits for disproportionate-collapse resistance

- Avoid single-supported "hero" spans; give every element two credible supports.
- Transfer elements (beams carrying stopped columns/walls, Wandträger) = key elements: extra ductile
  detailing, redundancy or the accidental combination, and never hidden in the architecture.
- Columns not beams: let beams be the sacrificial ductile part (strong column – weak beam as a
  *concept*; numbers in `seismic-design`).
- Storeys support storeys: any vertical interruption of the bracing (open floor, setback) is a
  discontinuity to design, not detail away.

### 13.6 Movement and separation joints

| Joint type | Trigger | Practical spacing/width |
|---|---|---|
| Expansion (Dehnungsfuge) | restrained thermal/shrinkage movement | RC ~ 25–45 m (VERIFY current NA guidance); unreinforced masonry crack-control far tighter: Ziegel ~12 m, KS ~8, concrete-block ~6 m; thin-joint AAC bands differ |
| Settlement (Setzungsfuge) | different founding depths/loads side by side (tower vs wing, extension vs existing) | full height separation incl. foundation; step foundations 1:2 if same dig |
| Seismic (seismische Fuge) | adjacent blocks of different height/stiffness | width ≥ sum of expected drifts, realistically ≥ ~5–10 cm between low-rise blocks (VERIFY per EC8/site) |
| Construction (Arbeitsfuge) | pour logistics | planned + roughened + tied through (Halfen/rebar starters), never "wherever the crew stopped" |

αT mismatch is real: steel 12, concrete 10, masonry 6–10, cladding systems differ — an unrestrained
cladding fixed to a long wall bows; fix-points radiate, joint them.

---

## Section 14: Seismic Configuration Pointers (handoff to `seismic-design`)

### 14.1 What this skill decides, what it hands on

Concept-ownable: system choice, plan/elevation regularity, wall-density screening (§8.2),
diaphragm/tie completeness, soft-storey/short-column avoidance, foundation uniformity. Engineer-own:
hazard values (pgBV per municipality in Germany via the EC8 NA building-stock lists; RD3/R2017 in
Austria, SIA 261 in CH — **read the current source for the site**), spectral analysis, q/R factors,
capacity design.

### 14.2 Behaviour-factor logic (why detailing is the whole story)

Ductility lets the building absorb cycling without elastic strength: low-ductility (DL/DCM)
conservative force, high-ductility (DCH) lower force + demanding detailing. For the systems here the
banding (EC8 tradition, VERIFY values): braced ductile wall systems and frames get the largest
behaviour factors; **unreinforced masonry gets the smallest and is barred at higher hazard**;
confined masonry sits between, precisely because its confinement turns brittle panels into a
coherent ductile-ish system. A system "designed elastically without ductility" is the most expensive
version of every system.

### 14.3 Configuration rules that pay before any analysis

1. **Compact, symmetric plan**; stiffness ≈ mass centre; avoid single-side wall concentration.
2. **Continuous vertical elements**; walls over walls, columns over columns; equal storey heights
   (setback floors break the stiffness line).
3. **Floors as discs**: full diaphragm action including precast/timber cases (§1.3); collectors
   around voids.
4. **Rotate floor spanning direction** storey-to-storey so bracing walls stay loaded.
5. Openings ≤ ~40 % per storey, stacked; piers ≥ ~0.6 m; confined gables/parapets.
6. Foundations one level where possible, tied; avoid split-level without a designed step.

### 14.4 The irregularities houses actually hit (generic, not catalogue)

soft/open ground storey (parking, shopfronts) · torsion from party-wall asymmetry · re-entrant
L/T/U without joint · diaphragm cut by atrium/double-height · short columns from partial-height
infill or window sills · mass on top (tank, heavy roof) on light frame · out-of-plane offsets of
the wall line. Each is a configuration decision first, a detail second.

### 14.5 Masonry no-calculation logic (legacy + EC8-3 successor)

The German DIN 4149-era exemption family (still the right *shape* of thinking, superseded as code —
VERIFY against EC8 + NA and `seismic-design`): low zone + firm ground → up to ~4 storeys;
moderate → ~3; higher → ~2; requirements: compact plan (b/l ratio bound), storey height ≤ ~3.5 m,
**≥ 2 shear walls ≥ ~2 m long per direction**, majority (>50 %) of bracing length from those long
walls, minimum wall thickness/area ratios per zone/storey band (~2–6.5 % wall area — grid alignment
in source ambiguous, VERIFY), foundation beams and wall footings with ≥ 4Ø12 continuous ties.
Where the hazard map says "verify seismically", confined-masonry detailing (§8.3) plus wall-ratio
screening is the minimum credible concept; beyond that, the frame or CM verified per EN 1998-3.

---

## Section 15: Material Choice Matrix (cost · speed · span · physics · carbon)

Decision table for the concept conversation — qualitative bands, DACH market reality, prices move:

| Criterion | Masonry | RC cast-in-place | Precast | Timber | Steel/Composite |
|---|---|---|---|---|---|
| Grey-structure cost (MFH 4–5 st.) | ●●●● | ●●● | ●●● (grid repeat) / ●● (bespoke) | ●●● (dry trade, short programme) | ●● office / ●●● halls |
| Schedule | slow-mid | 1 floor/week with table formwork | erection-fast, planning-slow | frame-fast, planning-mid | erect-fast, procurement long-lead |
| Span ability | ●● (≤6.5 m) | ●●● (≤7 m flat; ribs 10+) | ●●●● (hollow-core to ~15 m, DT to 20+) | ●● (5 m) → ●●● (glulam/LVL 10+) | ●●●● (halls, long beams) |
| Fire | ●●●● inherent | ●●●● cover | ●●●● | ●●● char design | ●–●● protection $ |
| Acoustic (residential) | ●●●● | ●●●● | ●●●● | ●● (build-up needed) | ●● (build-up needed) |
| Wall-thickness efficiency | ●●● | ●● (thin strong) | ●●● | ●●● (thin + insulation inside build-up) | ●● (columns in walls) |
| Site constraints (tight urban, no crane) | ●●●● | ●●● | ● (crane essential) | ●● (small crane/tower) | ●● (deliver in pieces) |
| Weather window | ●● (dry works matter) | ●●● | ●●●● (plant indoor) | ●●●● (dry system, protect stored) | ●●●● |
| Carbon + circularity (qualitative) | ●●● embodied mid, no clinker-heavy | ●● cement intensity — levers: SCM/eco-cement classes, design optimisation | ●●● factory efficiency + same levers | ● stored carbon + renewable; biogenic storage | ●● high primary but fully recyclable, demountable |
| Local trade base (DACH) | universal | universal | plant-dependent | strong and growing | strong |

Carbon: the ranking above is *directional*; get real numbers (EN 15804 EPDs, DIN EN 15978 modules)
from `sustainable-construction`. The concept-stage levers are: system swap (timber/hybrid for
housing ≤ 5–6), cement reduction (SCM classes CEM II/III), material-optimised slabs (hollow-core
uses ~ half the concrete of solid at 6–7 m), and designing for disassembly.

---

## Section 16: Case Patterns (typical DACH projects, as pre-designed)

### 16.1 EFH / DH — 2-storey, pitched roof (Mauerwerk + Decke)

```
System     A: load-bearing masonry (KS 24–30 ground / HLz upper band), timber floors or thin RC
           20–22 cm ≤ 5–6 m; Holzbalkendecke ≤ 4.5–5 m; grid: walls stacked on walls, ≤ 6 m spans;
           garage bay → one RC frame element (§2.4)
Roof       tile-module spacing; trusses 1.0–1.5 m onto wall lines, every truss anchored into the
           ring beam (uplift chain); confined gables
Bracing    walls both directions (≥2 long ones per direction) + floor discs + closed ring anchor
           (triggered >2 storeys or L >18 m); Foundation: strip 0.6–0.9 × 0.3 ≥150 kPa presumptive
Seismic    low/moderate → this pattern + confinement detail (→ CM, §2.2.B); high → CM verified or frame
```

### 16.2 MFH — 5 storeys + TG, RC (WU) frame/wall + flat or ribbed slab

```
System     C+G: WU basement (30–40 cm walls, base slab 40–60 cm), above: bearing-wall or column-grid
           structure; bracing = stair/lift core + end wall bands
Grid       living 2 dwelling widths ≈ 5.5–6.5 m; TG 7.5 m; bathroom stacks along core band
Slab       flat 24–26 cm @ 6 m → punching governs → studs/drop or switch to beam grid/ribbed
Columns    take-down §7: ~2200 kN ULS at 5th→ground ⇒ 40–50 cm, C30/37 (§17 walkthrough)
Bracing    core near plan centre; non-sway check (structural-analysis); collect voids
Foundation pads+strip ring or raft under TG; matched founding; UPL check vs water table
Stairs     RC flight = extra brace; isolate or model it (it will attract shear)
```

### 16.3 Logistics hall — single-storey steel (portal)

```
System     F: 2-/3-hinged portals, 12–15 m bays × 6–8 m field spacing; S235/S355
Envelope   trapezoid roof disc + wall sheeting; roof daylight strips; snow μ on drift lines
Bracing    roof plane diagonals/field members + vertical cross bracing end bays; tipping direction
           by same bays + base anchors/thrust blocks
Pinned     column feet pinned + explicit bracing; gantry/crane loads push to fixed or stiffened
Fire/corr  painted + board protection at occupied zones; hot-dip for durability class
Foundation pads + tie beam strip between all feet; crane hall → stiffer, consider monolithic
```

---

## Section 17: Worked Pre-Design Walk-Through — 5-Storey MFH, RC, 6.0 × 6.0 m Grid

**Brief.** 24 × 12 m footprint, 5 storeys dwelling + flat roof, no basement (ground slab), site:
firm soil (presumed σR = 250 kPa — conditional on report), low-moderate seismic, German NA framing.
Concept-level only; every step is "then verify".

```
STEP 1 — SYSTEM & GRID
  5 storeys, parking not required, unit depth 12 m → RC. Bearing-wall option rejected: open-plan
  requirement. Column grid 6.0 × 6.0 (2 dwelling widths), 4 × 2 columns; stair+lift core 4.0 × 2.5 m
  near plan centre (brace + access). Floors span two-way to the grid.

STEP 2 — LOADS (§6)
  floors: slab h (iter. below), finishes 1.5, partitions via surcharge 1.0 → qk = 1.5+1.0 = 2.5
  roof:   slab + build-up 1.5, snow governs variable (s = μ·sk, no terrace-combo)
  ULS area floor: 1.35·(25·h + 1.5) + 1.5·2.5    roof: 1.35·(25·h + 1.5) + 1.5·s

STEP 3 — SLAB DEPTH (flat slab first guess)
  band ~ l/27 → 6.0/27 ≈ 22 cm → try h = 25 cm (d ≈ 20 cm both ways, cv 35/45).
  gd = 1.35·(6.25+1.5) = 10.46 ; qd = 3.75 → p_d = 14.2 kN/m²

STEP 4 — PUNCHING SCREENING (the flat-slab verdict, §4.2/§12.4/structural-analysis)
  interior col 35×35, tributary 36 m²: V_Ed ≈ 14.2·36 ≈ 511 kN (+wall misc.)
  u1 = 4c + 4πd = 4·0.35 + 4π·0.20 ≈ 3.91 m ; v_Ed = β·V/(u1·d) = 1.10·511/(3.91·0.20) ≈ 0.72 MPa
  v_Rd,c (C30/37, ρl ≈ 0.4 %): 0.12·2.0·(100·0.004·30)^⅓ ≈ 0.55 MPa → v_Ed ≈ 130 % of capacity
  ⇒ PUNCHING GOVERNS: need Studbügel (2 rows) or drop panels/heads — or revert to a beam grid.
  Choose beam grid 6.0×6.0 + 22 cm two-way panels (T-beams l/12–l/15 ≈ 45 cm) → beams 25×45.
  (This mirrors the recovered German office flat-slab chain, which also ended at punching links:
  the flat slab "saves depth" only until punching bills for it.)

STEP 5 — TAKE-DOWN (§7) — column C3 (interior)
  service per floor: gk = 6.25 (25 cm slab) + 1.5 = 7.75; qk = 2.5 (A2 + surcharge) → 10.25
  → floors 4 × (10.25·36 ≈ 369) = 1476 kN; roof (7.75·36 + snow ≈ 315) = 315 kN
  + self-weight/wall/beam misc ≈ 160 kN → N_serv ≈ 1950 kN
  N_Ed ≈ 1.35·1555 + 1.5·396 ≈ 2700 kN
  screening νEd = N_Ed/(Ac·fcd): 40×40 C25/30 → νEd = 1.19 ✗ ; 60×60 C30/37 → νEd = 0.44 ✓
  l0/h = 2.8/0.6 ≈ 4.7 (braced, λlim comfortably met) → OK; edge columns 30×60 in the wall line;
  core + end wall bands carry their own tributary strips.
  Lesson stated: strength did not govern — νEd margin, detailing space, and the wall line did.

STEP 6 — BRACING (§5, structural-analysis verifies)
  core (25 cm, full height) + 2 end wall bands; non-sway check on ΣIc (θ/K1 0.31 family); storey
  shear by stiffness; collectors at voids; ring anchor every slab edge ≥70 kN band.

STEP 7 — FOUNDATION (§12)
  N_serv ≈ 1950 kN → A ≥ 1950/250 = 7.8 m² → 2.8 × 2.8 m pad, h 60 cm, C25/30, XC2 cover
  (≈ 8.5 cm on blinding); kern e ≤ b/6 under wind moment ✓ by inspection at this height;
  uplift: 0.9·G ≈ 1420 kN stabilising vs 1.1Gdst + 1.5Wdst (W small at pad scale) → no tension.
  Core + end bands on strip 0.9×0.5; all pads tied by foundation ring beam; ground slab as
  diaphragm + water-tightness decision deferred to report (capillary vs pressure).


STEP 9 — SANITY BANDS
  14.2 kN/m² floor ULS ✓ in-band; νEd 0.44 ✓; pads 2.8 < ½ spacing 6.0 (no overlap) ✓;
  covered slab area 1440 m²: concrete ~ 330–390 m³ (0.20–0.24 m³/m² + footings), steel ~ 58–86 t
  (40–60 kg/m²) — inside the DACH MFH experience band
  (relative-cost and quantity bands indicative — VERIFY).
STATUS ⚠ PRELIMINARY: geotechnical report, hazard lookup, engineer's analysis + detail design.
```

---

## Section 18: Anti-Patterns (system-level failure modes)

| # | Anti-pattern | Why it fails | Fix |
|---|---|---|---|
| 1 | Soft/open ground storey (parking, shopfront) | drift concentrates at the weak floor — the pancake | designed bracing bays/walls at that level, bigger + confined columns; never lean on the infill above |
| 2 | Short column (partial-height sill/landing) | free length shortens, stiffness ↑, brittle shear X-crack | full-height restraint or isolate + close ties |
| 3 | "Confined masonry" cast frame-first then infilled | no toothing bond → confinement doesn't confine | build wall, then pour (§8.3-1) |
| 4 | Tight masonry infill + bare-frame analysis | real stiffness ≫ model: torsion, short cols, soft storey | isolated infill *or* designed integral strut system (§2.4-6) |
| 5 | All bracing one side / L-T-U plan unjointed | stiffness–mass offset → torsion; re-entrant stress | rebalance bands; joint or heavy collectors + verification |
| 6 | Untied precast planks / joist floor as bracing | loose boards, no disc | topping+keys+edge ties / sheathing+chords |
| 7 | Long hidden beam | quarter depth = sixteenth stiffness | downstand, thicker slab, ribbed |
| 8 | Rafter pair on untied wall head | arch thrust pushes masonry out (± snow) | collar tie/truss/ridge beam |
| 9 | Light roof without hold-down chain | corner/edge suction peels it | anchor chain designed, closer edge fixings |
| 10 | Missing ring anchor / open (non-closing) ring | forces can't circulate; corner separation | closed loop ≥70 kN band, bent bars at corners |
| 11 | Heavy tank/plant mid-span | point load ≫ slab + seismic mass at top | move onto a line, or designed pedestal frame |
| 12 | Cantilever top steel "forgotten" or back-span short | tension face un-armed → sudden drop | chair + mark + back-span ≥ 2× + hold-down |
| 13 | No plinth/foundation ring; mixed founding depths stepped <1:2 | differential rotation cracks brittle masonry at 1/500 | tie the base, match/step levels |
| 14 | Building "for now", extending "later" | existing footings/columns ~50 % short | size the final storey count on day one — marginal cost at build, brutal at retrofit |
| 15 | Chases/holes in structural walls & punching zones | section/ shear capacity gone where force peaks | routes in partitions/ducts; documented + verified penetrations |
| 16 | Grid offsets storey-to-storey without transfer story | every misalignment is a deep-beam moment nobody sized | keep the grid; else design the transfer plate/wall |
| 17 | Steel "cheap frame" without fire/corrosion budget | the tax arrives later, unreduced | protection strategy at concept (§10.1) |
| 18 | Precast designed as a monolithic frame on paper | erected pins can't do what the model assumes | design the system you erect: ties + braced bays (§11.1) |
| 19 | Snow ignored on a "small" lower roof next to a tall one | drift wedges are the failure, not the balanced load | μ3 valley + drift cases (§6.4) |

---

## Section 19: BIM / FreeCAD Modelling Defaults (DACH)

Use these so the first model pass is dimensionally honest. Pair with the BIM-Modelling habits skill
in this library for the Site/Building/Storey hierarchy and parametric openings.

| Parameter | Default | Note |
|---|---|---|
| Bearing wall (KS/HLz) | 240 / 300 / 365 mm | ground floor of taller stacks thicker |
| Partition | 100–125 mm + skin | **non-structural — never a support** |
| Ring beam/anchor | 240 × 200 band, closed ring | model as own object per wall line |
| RC column MFH | 400×400 → 500×500 | §7 screening; IfcColumn |
| RC beam | 250×450 → 300×600 | quote total depth from slab top; IfcBeam |
| Slab MFH | 220–250 mm | flat slab → model punching studs where planned |
| Hollow-core / ribbed | HC 200–250×1200 (bearing ≥ 90, joints visible); rib 600–700 @ 200–300 | |
| Composite deck | sheet 60 + topping 140 | |
| Timber wall / CLT wall | 160 stud + 2× board / 120–180 | platform storey-high; label ply direction |
| Timber floor joist | 60/220 @ 600 oc | rim joist modelled |
| Steel hall column/rafter | HEA/HEB 200–300 band | pinned feet + bracing members modelled explicitly |
| Storey height | 2.80–3.00 MFH / 3.40 office | |
| Floor build-up zone | 200–300 mm | services below slab |
| Footings | strip 800×300 (blind 10+5/side); pad 1600–2600 sq × 500–600 | from take-down §7/§17 |
| Door/window/lintel | 900×2100 / 1200×1000 @ 800 sill; lintel own object | parametric openings keep §8 checks re-runnable |
| Stair core | 25 cm RC walls | model as brace object |

**Modelling discipline:** (1) columns/tie-columns/walls/cores as distinct objects, not fused — the
§1.4 audit must be visible; (2) model ring anchor + plinth beams + footings even schematically —
overlapping pads on plan *is* the signal to switch to raft; (3) show the load-bearing/non-bearing
classification in properties (IFC class); (4) annotate model or README with assumed σR, hazard
value source, material classes, "preliminary" status — no invisible inherited assumptions;
(5) any FEM run recorded with its load cases, BCs, materials — and stated plainly as validating the
model.

---

## Section 20: Checklist and Handoffs

### 20.1 Concept checklist (run before calling the design done)

- [ ] System chosen against §2.1 tree with the reason recorded (one sentence)
- [ ] Gravity chain written out for this building (§1.2 style) — no bearing lands on air
- [ ] Lateral chain: diaphragm → collector → brace → foundation → ground exists in **both**
      directions, axes not concurrent (§5.2)
- [ ] Grid on the module; spans in the slab/beam band chosen (§4); no >7 m flat slab, no long
      hidden beam, no floating column
- [ ] Wall ratios / brace stiffness screened (§8.2); ring anchor closed where required; ties §13
- [ ] Openings: piers, stacking, ≤ ~40–50 %, confined edges > 1.2 m (§8.4)
- [ ] Take-down run (§7): factored + service both produced, νEd ≤ ~0.5, sanity bands pass
- [ ] Foundations from presumptive band ONLY with "geotechnical report pending" on the print;
      kern/EQU checks visible (§12.4)
- [ ] Movement/settlement/seismic joint decisions made (§13.6)
- [ ] Snow, wind-uplift, parapet, tank, PV, plant all on the load list (§6)
- [ ] Robustness stance stated: redundancy system or determinate+tie system (§13)
- [ ] Seismic hazard source for the site named (map/list read — not remembered); irregularities
      from §14.4 resolved at configuration level
- [ ] Hybrid junctions follow §2.4 if mixed
- [ ] Quantities smell-tested (§17 step 9 band); costs as *relative* multipliers only
- [ ] Output labelled: **preliminary — requires analysis, design and signature by the structural
      engineer of record + geotechnical report; authority process separate.**

### 20.2 Handoff package to the engineer

architectural plans (dimensioned, final storey count incl. wishes) · site/levels/neighbour
foundations · geotechnical report (σR, water, GK, soils) · hazard value + source · wind/snow site
values · intended system + preliminary sizings labelled as such · grid, service stacks, core
positions fixed · material classes (exposure, WU, XC) · non-negotiables (spans, column-free room,
roof terrace) · every assumption made here, listed explicitly.

### 20.3 Route map (which skill next)

| After this skill, go to | When |
|---|---|
| `structural-analysis` | real combinations, frame/slab models, punching, slenderness, crack checks |
| `concrete-detailing` | bars, anchorage/lap, links, bar bending schedules |
| `masonry-construction` | unit/mortar choice, fmk, EC6 wall verification, ring anchor detail |
| `timber-steel-design` | joists/panels/profiles, connections, fire char calc |
| `geotechnics-foundations` | soil report reading, DIN 1054/4017 bearing, settlement, piles, retaining |
| `seismic-design` | hazard values, q-factors, ductile detailing, CM verification |
| `construction-scheduling-site` | formwork cycles, erection order, temporary bracing |
| `sustainable-construction` | LCA of the chosen system, substitution studies |

---

## Section 21: Known Gaps and VERIFY Register (state when relevant)


1. **EN 1991-1-7 tie-force table values** presented as concept + bands (70 kN ring anchor is the
   German-NA anchor actually carried); exact table per current EN/NA — engineer.
2. **Seismic hazard**: Germany pgBV lists (EC8-1/NA), Austria ÖNORM/ÖKraft, Switzerland SIA 261 —
   nothing here substitutes for reading the site's current value; DIN 4149 figures are legacy.
3. **Wall-ratio screening numbers** (§2.2.B, §8.2, §14.5) are bands recovered from practice
   tradition with ambiguous grids in source — screening only, never a verification.
4. **Presumptive ground resistance** (§12.3): DIN 1054 table family; reductions (saturation −40 %)
   and applicability limits (GK 1–2, small footings) — `geotechnics-foundations` owns it.
5. **Snow/wind NA formulas and zone maps** (§6.3/§6.5) and the **imposed-load multi-storey
   reduction**: German altitude formulas are one edition's; AT/CH differ entirely; the reduction
   formula's owner is `structural-analysis`/NA — read the current document for the site.
6. **Hollow-core / composite-deck span-depth rows**: supplier-product data, ranges given,
   verify against the chosen manufacturer's tables.
7. **Relative cost bands** (§2.3, §15): multipliers only, deliberately no €/m² — markets go stale
   within months; quantity surveyor only.
8. **Confined masonry** has thin tabulation in EN 1998-1 itself; its home is EN 1998-3 §7 +
   national practice — the §2.2.B numbers are practice bands (VERIFY).
9. **Fire durations, acoustic build-ups, and all reinforcement figures** are referenced only as
    decision drivers / order-of-magnitude for modelling — not schedules or ratings; those live in
    their own skills (`concrete-detailing`, `fire-protection-building`, `building-acoustics`). **Liquefaction, slopes, excavation support, existing buildings
    and retrofit** are out of scope entirely: report + inspection + engineer, always.

---

## Appendix S: Source Check 2026-10 — values re-read from the literature

Each line below was read again in the source books (`sources/`) in October 2026, with the
place it stands at. "Confirmed" means: a dated book prints the rule and names the standard
or law; it does not mean the current edition of that standard was opened. State law
(LBO) and local rules still override; `VERIFY` tags elsewhere in this skill stay in force
unless a line here names the edition. Where a line here differs from a section of this
skill, that section was corrected and names the line ("S.n"); the appendix governs.

### S.1 Frost depth of a foundation

- Confirmed: unless frost safety is proven otherwise, the distance from the frost-exposed
  surface to the footing base is at least 0.80 m (DIN 1054). — *Formeln und Tabellen
  Bauphysik* 2.6.6 (p. 138); *Wendehorst Bautechnische Zahlentafeln* 14.7.1; *Werkstoffe im
  Bauwesen* 1.6.1 (p. 170).
- Method (DIN EN ISO 13793): the frost penetration depth of undisturbed ground is taken from
  national maps or tables, or estimated as H0 = √(7200 · Fd · λf / (L + C · θe,m)), with Fd the
  design frost index in K·h, λf = 2.5 W/(mK), L = 150·10⁶ J/m³ and C = 3·10⁶ J/(m³K) where
  nothing better is known, θe,m the mean annual outside air temperature. — *Formeln und
  Tabellen Bauphysik* 2.6.6 (p. 140), Gl. (2.6.6-5). Read the root in the printed formula
  before use (VERIFY: the scan does not show it clearly).
- Practice: often set to a minimum depth of 100 cm. — *Building Construction Design: From
  Principle to Detail*, vol. 2, 6.2.4.2. Buried water lines lie deeper (1.0 to 1.8 m cover).

### S.2 One-way or two-way slab

- Confirmed (EC2-1-1 5.3): a slab supported on all sides may be taken as one-way when
  lmax/lmin > 2. — *Wendehorst Bautechnische Zahlentafeln* Tab. 8.15. The 1.5:1 of §4.2 is
  the earlier, conservative switch of this skill.

### S.3 Solid slab thickness by span — what the cost books assume

- Typical, dwellings: span 3.0 / 4.0 / 5.0 / 6.0 m → slab 12–13 / 13–15 / 14–18 / 16–20 cm.
  — *Zahlentafeln für den Baubetrieb* Tab. 12.18. Favourable thickness to span about 1:30,
  solid slabs reasonable up to about 8 m at about 30 cm. — *Building Construction Design*,
  vol. 2, 4.2.1.1.4.
- Reading: the schedule of §4.2 (20 cm to 4.5 m, 24 cm to 6.5 m) is thicker than these
  and stays the default: it also covers sound and fire without a check.

### S.4 Defaults of this library for a simple house model

**Not from a book.** These are choices of this library, made so that a simple house can be
modelled at all where the literature gives a frame and no number. Tier T4, massing only:
any plan clause, product sheet, engineer's or carpenter's figure replaces them, and nothing
here is a design value.

- Which wall bears, where no engineer has said: a slab field spans the short way of the room
  below it (§3.2), and a wall counts as a support of that field when it runs along at least
  half (0.5) of the field's edge. The other walls are drawn as partitions.
