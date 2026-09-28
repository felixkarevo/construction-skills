---
name: construction-detailing
description: >
  Baukonstruktionsdetails — the joint- and layer-grammar that connects every building system
  into continuous build-ups (Schichtaufbauten). Layer logic: Trag-, Dämm-, Dicht-, Schutz- and
  Nutzungsschichten; Schale vs Schicht; ordering rules (vapour control warm-inside / weather
  tight outside, insulation always outside the load-bearing shell, capillary breaks, staggered
  layer joints / Entflechtung); multi-stage vs single-stage sealing (Stufigkeit). Connection
  grammar: Form-/Stoff-/Kraftschluss per direction, joint alphabet (butt, lap, rebate, tongue,
  raised/Aufkantung), the three closed-joint sealing principles (bond, flank-adherent sealant,
  compressed gasket), capillary-joint hazard. Movement and structural joints: expansion-joint
  spacing and width logic, waterstops at construction joints (Arbeitsfuge/Dichtungsband),
  outer-leaf joints at corners. Tolerances and setting-out: Achsmaß/Rohbaumaß, modular grid
  (12.5 cm / 1 M = 100 mm), planned adjustment zones, DIN 18202/18203 flags. Junction
  detailing: wall-footing/plinth (30–50 cm splash continuation, horizontal barrier,
  Perimeterdämmung, black/white tub transition), wall-slab (bearing + ring anchor + acoustic
  flanking), wall-window (Dichtungsstufen inside-airtight/outside-rain-open logic, mounting
  depth, flank insulation), wall-roof (eave, knee-wall gable, parapet), roof-wall upstands and
  ballast terminations, floor-screed (floating build-up, edge strips, joint grid, heating
  screed), balcony/loggia (thermal break strategies, falls, drainage redundancy), internal
  walls (bond, lintels, top-down erection, installation zones), penetrations (sleeves, sealing
  collars). Buildability sequencing (what must exist before what), worked junction
  walk-throughs with numbers, detail QC checklists, FreeCAD modelling of layered walls (void
  extrusions + layer objects, IFC Pset propagation), failure gallery (thermal bridges, trapped
  moisture, acoustic flanking, joint failures) with fixes. Cross-referenced to
  roofing-waterproofing, openings-windows-doors, building-physics-thermal-moisture,
  building-acoustics, masonry-construction, concrete-detailing, structural-systems.
---

# Construction Detailing — Build-Up Logic and Junction Grammar (DACH)

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

A building does not leak, freeze or go quiet "in general" — it fails **at a specific line where
two planes meet**, and it succeeds only if every functional layer survives that line. This skill
is the connective tissue of the library: the other skills each own a system (roofs, windows,
masonry, concrete, structure, physics); **this one owns the junctions between them** — the
300–1000 mm zone where the wall build-up must hand its vapour control, airtightness, thermal
continuity, rain staging and acoustic mass over to the roof, the window, the plinth, the screed
or a pipe — without breaking a single function.

Detailing here follows the DACH (German/Austrian/Swiss) construction culture: layered
build-ups, modular coordination, DIN/DIN EN norms and trade rules, executed against tolerances
(DIN 18202/18203). The physics is universal; the numbers are DACH-practice numbers.

Use this skill **before drawing any junction**, before freezing a wall build-up in the model,
and whenever a review question is "but is the layer continuous *there*?"

---

## Reality Check — Liability and Approval

**This skill produces design aids, detailing logic and coordination checklists — not a stamped
execution plan.**

- Detailing in the German sense is HOAI service phase 5 (Ausführungsplanung) work: every drawn
  junction here is a **proposal to be verified** by the responsible designer/architect against
  the current norm edition, the product approvals (allgemeines bauaufsichtliches Prüfzeugnis /
  ETA where applicable) and the manufacturer system guidelines it belongs to.
- Structural consequences of joints (ring anchor continuity, bearing lengths, waterstop design
  pressures, movement force take-down) belong to the structural designer; see
  `structural-systems` and `concrete-detailing`.
- Waterproofing layer counts, upstand heights and pressure classes must be confirmed against
  the current DIN 18531–18535 series (the legacy DIN 18195 scheme survives only in habit);
  airtightness numbers against current DIN 4108-7/GEG practice; tolerance tables against the
  current DIN 18202/18203 issues. **[VERIFY before quoting a clause or table value in a
  submittal.]**
- Products marked here with a rule of thumb (sealant joint depth ratios, mounting levels,
  screed field sizes, upstand minimums) are **principle-level guidance**; the binding values
  are the manufacturer's system data sheet and the applicable norm at the project's contract
  date.
- When a junction is safety-relevant (fire compartment wall penetrations, guard rail anchorages
  into waterproofing, balcony overturning), never resolve it by copying a catalogue detail —
  write the performance requirement and have the specialist detail it.
- If the user intends to build or price from an output of this skill, state plainly: this is a
  planning model; licensed sign-off and the building-authority process are required first.

---

## Section 0: Scope — and Which Sibling Skill Owns What

Detailing touches everything; to avoid duplicate and contradictory guidance, this library
divides the territory:

| Territory | Owner | What THIS skill adds |
|---|---|---|
| Roof layers, drainage classes, waterproofing stacks, upstands | `roofing-waterproofing` | How the roof stack **terminates into** wall/parapet/window-opening and how its layers continue at the junction |
| Window/door units, lintels, sills, the Dichtungsstufen system | `openings-windows-doors` | Junction-zone build-up: mounting depth, insulation-plane continuity, reveal flanks, tolerance gaps around the fixed unit |
| Masonry units, fmk design, bonds, ring beams, plinth/DPC | `masonry-construction` | Layer continuity across masonry-to-other-systems lines; movement-joint layout |
| Rebar, cover, WU design, waterstops numerics | `concrete-detailing` | Where joints sit, why (buildability/movement), and what the sealing layer must survive |
| U-values, Ψ, fRsi, Glaser, airtightness numbers | `building-physics-thermal-moisture` | The **constructive measures** that produce the assumed Ψ/n50 — geometry, layer stops, tapes, overlap directions |
| Rw/L'n,w design, flanking classes | `building-acoustics` | The joint geometry (bearing + decoupling + flank sealing) that makes the acoustic model true at walls/floors |
| Statical systems, bracing, load paths | `structural-systems` | Connection technology at element level (Schlussarten, bearings, tension chords) and its detailing consequences |
| FreeCAD BIM hierarchy, void cuts, FEM | `construction-freecad-bim` | Layer-object modelling convention + IFC property propagation for build-ups |

If a task is *inside* one system, route to its skill. If it is a **line where two systems
meet**, this skill leads.

---

## Section 1: The Grammar of Build-Ups (Schichtaufbau)

### 1.1 What a detail must satisfy simultaneously (function hierarchy)

Every building element serves three main functions — Tragen (load-bearing), Einhüllen
(enclosing), Ver-/Entsorgen (media supply) — and the envelope carries seven named sub-functions
(bauliche Teilfunktionen) that a single junction must all survive:

1. **Feuchteschutz** — moisture protection (rain, driven rain, splash-back, ground moisture,
   pressing water, capillary moisture, vapour, condensate, ice/snow/wind-blown snow — each has
   its own control path)
2. **Wärmeschutz** — thermal (continuous insulation plane, no bridge paths, surface
   temperatures above mould limit)
3. **Luft-/Winddichtheit** — air/wind tightness (continuous surface, mechanically protected)
4. **Schallschutz** — acoustic (mass continuity or clean double-leaf, no rigid flanks)
5. **Brandschutz** — fire (load-bearing duration + Raumabschluss; joints as weak as the element)
6. **Dauerhaftigkeit** — durability (cross-cutting: drainage of water, protection of layers from
   UV, frost, mechanical attack, erosion)
7. **Kraftleiten** — force transmission (support forces, tie forces, anchor pulls through or
   around the build-up without destroying 1–5)

The designer's conflict table, stated once and true everywhere:

- **Load-bearing wants dense/stiff material = thermally conductive; insulation wants porous =
  carries nothing, is vapour-open, water-sensitive and acoustically poor.** Both compete for the
  same thickness. Resolve by (a) strict plane separation (insulation in its own layer, outside
  the structure) or (b) a compromise material (masonry with pores; wood, λ ≈ 0.15 W/(m·K), the
  only structural material that nearly does both — still not Passivhaus-grade alone).
- Water destroys insulation instantly: λ_water 0.6 vs λ_air 0.025 (≈ 24×) — a wet mat has lost
  its function; a material that is perfectly **watertight and vapour-open does not exist** (no
  "Gore-Tex principle" in building sheets). Every build-up is therefore a *strategy* about
  which of the two the outer skin plays.
- Cracks = loss of tightness function: cracking is material-immanent in concrete/masonry and
  mostly harmless for load, **but must be controlled in sealing layers and at joints.**

**Terminology discipline (use these consistently in drawings and BIM labels):**

- **Schale** (shell) = a layer with enough strength/stiffness to carry load (masonry wythe,
  concrete wall, cladding panel acting as shell).
- **Schicht** (layer) = any material position with an assigned function regardless of stiffness
  (a vapour foil is a Schicht, never a Schale).
- **Aufbau** (build-up) = the sequence of functional layers stacked in the thickness. Colloquially
  "Dämm-Aufbau" = a layer package containing thermal insulation, not mere render/coating.
- Every layer sits at a **fixed position** because the gradients across the thickness —
  temperature, vapour pressure, sound level, saturation — are directional. Moving a layer
  changes its function.

### 1.2 The five layer roles (functional classification of every position)

Read every build-up as five functional roles, however many physical sheets it contains:

| Role (German) | Function | Typical members | Failure if missing |
|---|---|---|---|
| **Tragschicht** (structural layer) | Kraftleiten, fire mass | RC, masonry wythe, timber frame/CLT, steel deck | collapse, buckling of build-up |
| **Dämmschicht** (insulation layer) | Wärmeschutz, acoustic spring | EPS/XPS/PIR, mineral wool, foam glass, cell glass | high Ψ/U, cold inner surfaces, single-leaf acoustic |
| **Dicht-/Steuerungsschicht** (air/barrier layer) | Luftdichtheit + vapour control | Dampfbremse/-sperre foils, taped boards, airtight plaster, WU concrete itself | convective moisture damage, drafts, noise leakage |
| **Schutz-/Wetterseite** (weather layer(s)) | Feuchteschutz + durability | render/ETICS skin, cladding + substructure, roof covering, tanking sheet, protection/filt layers | wetting, UV, frost, erosion, mechanical damage |
| **Nutzungsschicht** (finish/wearing layer) | use + room physics | floor finish, screed, tiles, plaster, panelling, paving | abrasion, splash, cleanability, appearance |

**Ordering rules (the laws of layer sequence):**

1. **Vapour control warm-inside, weather protection cold-outside, insulation between.**
   Diffusion design law: diffusion resistance HIGH on the interior (warm) side, LOW on the
   exterior side; never trap insulation between two near-closed skins without a purpose and a
   drying path (the double-bitumen flat roof "tanks" only because a full Dampfsperre makes the
   warm side the closed one). A ventilated cold-side air path replaces part of the
   diffusion design by export.
2. **The insulation layer package of exterior elements goes ALWAYS OUTSIDE the load-bearing
   shell.** Inside placement would require mechanical connections penetrating the insulation
   between shell and structure = thermal bridges + condensation on cold metal anchors, worse the
   thicker the insulation. Consequence of rule: modern high-insulation architecture is "thin
   skin"; a massive look is a concealed build-up behind it.
3. **Capillary breaks where ground/standing water meets porous material**: horizontal barrier
   (Querschnittsabdichtung) at the base course of masonry; dense plinth under porous wall; gravel
   drainage layer under slabs; timber always raised off damp ground. Rising damp is capillary
   suction in fine pores — a continuous barrier cuts it; salts then concentrate *at* the barrier
   line, so protect that zone.
4. **Watertight layers protected, never exposed or point-loaded**; drainage and ventilation
   layers sacrificial and replaceable; the wearing layer loose or renewable above the sealed
   ones (re-roofing, re-screeding and re-cladding are planned maintenance events, not damage).
5. **Joints of different layers never stacked at one point ("entflechten")**: stagger
   (cross-joint avoid) butt joints of adjacent layers within a multi-layer element; offsets and
   steps in layer planes multiply terminations — run planes through.
6. **Overlap (lap) direction follows water flow** (shingle principle): every lap faces so
   gravity drains it immediately; never a lap upstand catching inflow; never a flap that wind
   pressure can press open.
7. **Multifunktional vs monofunktional decision is first-order, not aesthetic.** A homogeneous
   single leaf (massive, one material doing everything) = fewer interfaces, compromise
   properties; a layered build-up (one layer per function) = best per-layer performance but more
   joints, more material mix, harder recycling, and **every joint is a defect waiting for a
   lazy installer.** The more functions you separate, the more junction continuity you must
   detail.

### 1.3 Staging of protection (Stufigkeit) — one line of defence or two

- **Einstufig (single-stage):** one layer alone performs the protection (fully-pitched tile
  roofs aside, the flat-roof sealing, the tanking sheet, the airtightness layer). Cheap,
  zero redundancy — the joint must be perfect and stay perfect.
- **Mehrstufig (multi-stage):** first stage **brakes** (Bremsen: catches most water/wind,
  sacrificial, ventilated/drainable), final stage seals. Open joint outer skins, rainscreen
  claddings, pitched-roof coverings, cavity walls all work this way.
- Rule of composition: **the outer stage is allowed to leak and must be able to dry; the inner
  stage must be tight and must never be the only layer exposed to sun, frost or abrasion.**
- Vertical elements with sporadic wetting → prefer multi-stage (outer rainproof + inner
  air/wind-tight + insulation); horizontal elements with standing water → single-stage
  waterproof but multiply protected (ballast, layers, mats).
- On steep pitches the first stage need not seal; at shallow pitch the first stage stops working
  → the second stage must become fully watertight (Unterdach logic — numbers and classes in
  `roofing-waterproofing`), and outward drying is then lost: the build-up becomes a
  single-stage + design-vapour-control problem.

### 1.4 Reference build-ups (memorise the sequence, not the product)

Sequences below are the canonical digested stacks; thickness/products are project choices.
Direction: warm → cold unless noted.

- **Warm flat roof on RC deck:** reinforced slab with structural or tapered falls → primer →
  **vapour barrier (mandatory — the weather skin is necessarily vapour-tight)** → spot-bonded
  separating/vapour-pressure-equalisation perforated layer → insulation (arbitrarily thick —
  horizontal plane prevents sliding) → bonding → 2–3 sealing layers fully bonded, laps
  staggered, in water-flow direction → protection → **gravel ballast 16/32** (UV + mechanical +
  fire + wind uplift). Liquid-applied sealing = quasi-continuous alternative; renders
  self-crack microscopically, seals shrink — hence "raise the joint out of the water plane"
  (§3.2).
- **Inverted roof (Umkehrdach):** sealing becomes simultaneously the vapour barrier and is
  *protected under* the insulation: substrate → relaxation/protection fleece → sealing →
  protection fleece → **closed-cell water-insensitive insulation (XPS perimeter boards, foam
  glass), lap-jointed, gradient-cut** → filter fleece (silt stop) → gravel. Removes the
  double-sealed-insulation dilemma entirely.
- **Earth-contact wall (heated basement), outside → inside:** soil → filter fleece →
  **drainage board** → Perimeterdämmung (closed-cell: XPS/foam glass — must survive wet, cold,
  earth pressure and point loads) → slip/protection fleece → **sealing on the protected inside
  face** → structural wall. (Sealing over soft insulation under backfill point loads = damage
  certain; the "reverse" logic of the warm roof is forced here.)
- **Black tub (Schwarze Wanne):** tanking between structural wall and protective inner backup
  wall (Wandrücklage cast smooth both sides, embeds + presses the sheet against point load and
  uncontrolled pressure swings); under-slab tanking bonded to wall sheeting above footing level;
  lean concrete → protection slab → sheet → sliding layer → RC wall → inner backup wall.
- **White tub (Weiße Wanne):** the WU-concrete itself is the seal, uncoated; tolerated residual
  seepage must dry **inward** (low-humidity use); requires dense crack-controlled concrete +
  tight construction joints: **waterstop strip in every Arbeitsfuge**, because rebar continuity
  makes a cross-section seal impossible there. Design is crack-width driven (see
  `concrete-detailing`).
- **Timber frame wall, warm → cold:** gypsum board → services cavity + 2nd insulation layer
  (protects the air barrier from socket perforation) → **vapour check/air barrier taped** →
  stud layer + cavity insulation → vapour-open structural sheathing/rain-screen board →
  counter-batten (Konterlattung) → ventilated cavity → cross-batten (Querlattung, optional 2nd
  insulation) → weather cladding (horizontal boards drain best).
- **Solid timber (CLT) exterior wall, example mm:** larch T&G rainscreen 21 + counter-batten
  ventilation + vapour-open membrane + insulation + airtight layer + plasterboard 2×12.5 +
  CLT 120 + plasterboard 2×12.5. Thermal insulation almost always OUTSIDE solid-wood elements
  (static thickness ≠ U-value thickness).
- **Two-leaf masonry:** inner structural wythe + cavity (Kerndämmung filled, or ventilated —
  air insulates only a few cm before convection) + outer weather wythe on anchors (wire anchors
  in the wall, bracket anchors at least every storey — and on its own support ledge where
  non-loadbearing, ≥ 2/3 brick width). Outer leaf takes the biggest thermal swings →
  **expansion joints required, including at corners** (corner movement against stiff anchors
  spalls the wythe — the mimetic paradox of pretending a two-leaf wall is monolithic).
- **Sandwich panel (industrial envelope):** two metal skins + rigid core as an I-section —
  no anchors through insulation; joints: in-plane raised standing seam above water path + cover
  cap; airtight closed package, so **moisture from either side is fatal (no drying) → joint
  sealing critical**; minimum pitch, never flat; concealed fixings clip formed panel edges (no
  face penetrations).
- **ETICS/WDVS (render on insulation):** insulation bonded full-face + disc anchors only where
  pull-off demands; reinforced render skin directly on insulation = no fixing penetrations =
  no point bridges; base drip profile + beaded terminations; plinth zone protected separately
  (§4.1).
- **Rainscreen façade over insulation:** substructure through-fixings (each one a point bridge +
  condensation risk — keep sparse, stainless or plastic) OR crossed double substructure so the
  outer rib layer touches the inner at small contact surfaces only (bridge reduced to points,
  acoustic spring preserved); water-repellent but vapour-open sheet at the insulation/ventilation
  interface; cavity = drainage + evaporation, kept clear of obstructions.

### 1.5 Where the functions get handed over (function transfer at material changes)

Continuity is *serial*, not local. The weather skin of a façade must pass protection hand to
hand around an opening: masonry face → jamb cover → outer frame → sash frame → glazing —
**every interface joint is a link; the seal fails at the weakest link, not the average.** Same
for airtightness (plaster → tape → foil → grommet → socket), for thermal (wall insulation plane
→ reveal strip overlap → frame cavity → head/level continuity) and for acoustic (wythe →
flanking-stopping layer). Detail a handover as: *arrival geometry, overlap/lap dimension,
compression or adhesion, protection, and the tolerance gap that absorbs the assembly slack.*

**Scheibe (disc/diaphragm) logic behind all of it:** a homogeneous shell has huge in-plane
stiffness (length enters squared) and carries vertical load AND wind shear — that is why walls
work as bracing discs and floors as diaphragms (§ structural-systems). Rib systems, multi-layer
composites and perforated façades **lose the disc action** unless recovered by stiff sheet
cladding or diagonal bracing — and every lost disc has to be re-formed at the junction with
chords, tie strips and ring beams (the junction IS the chord connection).

---

## Section 2: Joint Grammar (Fugen)

A joint is a **physical gap through otherwise continuous layers** — it must transfer every one
of those layers' functions across air. Buildings are too big to fabricate jointless (only
cast-in-place RC approximates a monolith), so joints are the default condition, and their
design follows a fixed hierarchy.

### 2.1 Joint avoidance first

1. **Bigger elements** (transport-limited); **prefer factory joints over site joints**
   (Werksverbindung vs Montageverbindung — shop quality is always higher).
2. **Continuous geometry without corners/edges** where possible; positive/negative corners are
   singularities that multiply terminations.
3. **Reduce joint exposure**: raise the joint out of the water-carrying plane (folded-up layer
   edges — Aufkantung/standing seam), shield with overlaps (Wetterschenkel, roof overhang,
   caps), orient so gravity drains it immediately.
4. **Never stack butt joints of several layers at one point** — stagger/entangle (entflechten).
5. **Put unavoidable joints in sheltered spots**: behind overlaps, under caps, above drips —
   never in the running water film; and let *same build-ups meet same build-ups* (layer-plane
   match at every junction; mismatched offsets are the chronic defect).

### 2.2 Open vs closed joints

- **Press/butt joints are NOT watertight**; milled flush stone joints actively **wick**
  (Kapillarfuge: gap narrower than the water meniscus + hydrophil faces = suction). Only
  elastic compressed faces can seal a butt joint — rare.
- **Open joints are useful** in multi-stage skins: narrow + deep = good rain brake (few-cm slit,
  long path), pressure-equalising, vapour-open. Two hazards: the joint must not sit where
  differential movement can **close it to capillary width**, and behind it the actual
  air/water/wind barrier must exist (open joints carry no thermal/air closure).
- Joint width **varies over time** (temperature/moisture cycles); the seal must survive the
  cyclic width change for years between maintenance rounds → **movement capacity of the seal >
  total predicted movement**, with renewal access planned.

### 2.3 The three sealing principles for closed joints (the complete set)

| Principle | Mechanism | Movement | Force transfer | Typical |
|---|---|---|---|---|
| **Stoffschluss** (material bond) | weld/glue continuum | blocked → Zwängungen | yes | welded seams, glued laps; airtight+tight if sound; irreversible |
| **Dichtstoff** (elastic sealant, flank adhesion) | wet-plastic cures elastic, bonds to both lips | absorbed by sealant strain | no | needs backing rod for hourglass shape (avoid 3-sided adhesion), compatible flanks, depth ≈ 1/3–1/4 of width **[VERIFY ratio vs product data]** |
| **Dichtung** (gasket under compression) | pre-compressed profile springs against lips | sliding tolerated | no | glazing pressure plates, compression tapes, oversize foam profiles; spring force must persist for life; pressure direction must be ⟂ to movement (impossible on straight butt joints) |

Helpers that make any of them work: **hydrophobic treatment** of joint lips (kills capillary
suction in narrow joints only); **slope horizontal joints outward** (gravity opposes driving
rain; one-sided slope already helps; sharp upper arris = tear-off edge);
**Entspannungskammern** (relaxation chambers) interrupting capillary flow and de-pressurising
wind — chambers in series add up.

### 2.4 Joint cross-section alphabet (choose geometry before product)

| Geometry | Path | Movement absorption | Watch for |
|---|---|---|---|
| Straight butt | short, depth = layer thickness | none usable | capillary wicking; thin foils impossible to seal this way |
| Inclined | longer path | small | sharp edges fragile; slope sheds outward |
| Covered (cap strip) | T-path; seals on the two parallel-to-layer faces | sliding in hidden slit | fasten cap to **one** leaf; cap must shed, never pond |
| Overlap (shingle) | unlimited in-plane length | sliding; fixings allow slide | lap direction in water-flow; step stagger or tilt courses |
| Rebate (Falz) | flush faces + long parallel seals | limited by narrowest square segment | put open slot on the UNDERSIDE of horizontal joints; tip outer lips down |
| Tongue-and-groove | two parallel legs + built-in relaxation chamber + self-positioning | good | tolerance void at groove bottom is the seal's friend |
| Raised/flanged (Aufkantung, standing seam) | joint gap lifted ABOVE the draining plane | folded legs bend ⟂ to motion (compliant) | the fold also stiffens thin sheet (why 0.5–0.8 mm standing seams work); clip-fix the seam |

### 2.5 Movement joints, structural joints and waterstops

**Why movement happens (design input for every joint width):** thermal expansion
α ≈ 10·10⁻⁶ 1/K concrete, 12·10⁻⁶ 1/K steel (close compatibility = prerequisite of RC
composite; different α = differential movement at fixings/bimetals); **shrinkage** of concrete
(irreversible, continuous; controlled by fine Schwindbewehrung + avoiding restraint in the
bearing layout — let it move so it does not crack what holds it); creep; hygric wood movement
(across grain ≈ 10× along grain — joints/gaps must absorb transverse movement; delivery ≈ 20 %
MC drying to ≈ 7–12 % Gleichgewichtsfeuchte with irreversible shrinkage + warp; fast drying =
more distortion); support rotation/settlement; wind sway.
**Design stance per element: allow the movement (joint) or resist the force (Zwängung) —
never leave it undecided, the material will choose cracking.**

- **Expansion joints (Dehnfugen)** subdivide surfaces — classically the two-leaf outer skin
  (biggest thermal swings), **mandatory at corners**; they penetrate the full build-up but NOT
  the structure where free movement is wanted. Spacing: set from α·ΔT·L vs crack or joint
  capacity; for cast-in-place RC wall/slab grids this is a structural decision — see
  `concrete-detailing` (typical building practice 20–40 m **[VERIFY project-specific]**) — and
  for screeds §4.6. Joint width must **exceed** the calculated movement with margin; fix the
  joint to one side, slide on the other (sliding contacts PTFE/stiff caps; the seal is a
  separate layer).
- **Twin cores / restraint zones:** between two bracing cores, give the floor a sliding or
  jointed bearing, else shrinkage/thermal restraint cracks the slab; put a releasing joint near
  a stiff core at the end of a long diaphragm so the slab can move in one direction.
- **Construction joints (Arbeitsfugen)** in water-tight RC: **waterstop strip (Dichtungsband)
  in every cold joint** — rebar continuity forbids a cross-section seal there; keyed/dowelled
  form, vibration access at the joint face, and plan joint placement (fair-faced: joints
  visible; a shadow-gap joint line conceals tolerance scatter). DIN 18197 (waterstop formwork)
  and DIN 18540 (joint sealing) are the norm anchors **[VERIFY editions]**.
- **Structural separation joints** (setzbare Fugen between building parts/bays): full-height
  double wall or double column line, each part statical self-contained; width ≥ differential
  settlement + thermal + construction allowance — generous (≥ 50–150 mm **[VERIFY]**); every
  layer gets its own termination (two sealing skins, not one stretched over the gap).
- **Cavity/ventilation joints:** segment ventilated cavities per storey (fire + acoustic
  telephony + wind pressure control): **fire stops in ventilated cavities ≈ every 50 cm of
  height** (digest case: WoodCUBE Brandriegel) **[VERIFY vs current MHolzBauRL/Land rules]**;
  per-floor vent openings.

### 2.6 Sealant/gasket service reality

Elastic seals age under UV, ozone and cyclic strain → they are **maintenance items**: accessible
joints beat buried ones; protect gaskets from UV (metal skins shade them) and from running dry/
hot; avoid three-sided adhesion; design joints to shed water so the seal is drained, not
submerged; renewal cycles belong in the handover documentation.

---

## Section 3: Connections, Bearings and Tolerances

### 3.1 Schlussarten — specify every connection per direction

Every connection must be classified **in all 12 senses** (6 translations + 6 rotations) —
saying "the joint is kraftschlüssig" describes one direction and hides the rest:

- **Formschluss** (form-fit): load ⟂ onto the contact pair; needs loose play in the assembly
  direction (one DOF stays free to build; the last direction closes by gravity or a small
  element → demountable = recycling-friendly); force only after slip.
- **Stoffschluss** (material bond): true continuum (welding); rigid in all senses, blocks
  deformation → Zwängungen; irreversible.
- **Kraftschluss** (force-fit): clamp preload (no play) or friction (Reibschluss, μ·N);
  adhesion (gluing) grouped here — joins dissimilar materials, weaker than cohesion.
  Masonry bed joints live on tangential force-fit: horizontal force resisted by surcharge —
  light-block walls without floor loads would topple in wind (⇒ every "wall" wants its
  superimposed load; see `structural-systems`).

**Fastener consequence list (detailing-relevant):** indirect bolted joints dominate steel
(oversize holes absorb tolerance at both partners, smooth shank bears over full grip); GV
preloaded = true friction, replaces site welding; SL bearing-type tolerates slip and rotation
groups; nails never for pull-out, always groups, never into end grain; weld = shop process
(residual stress/distortion; avoid weld cruxes); glue full-area but hates peel (protect free
edges, chamfer, symmetric laps, end-grain not gluable → scarf ≤ 1:10, finger joints multiply
area); grout pockets act by form-fit, not adhesion; rebar-concrete bond final stage = rib
form-fit. **Bimetallic rule for fixings: fasteners must be nobler than the base they clamp
(or isolate) — else the baser partner corrodes; stainless also = lower λ = lesser bridge.**

### 3.2 Compression bearings (the most benign joint — everything else converts into it)

Four conditions for pressure contact to act like continuum:

1. **Full-area contact** — plastic mortar bed compensates stone roughness; non-shrink grout
   under machined baseplates; **elastomeric pads** where movement/unevenness must be absorbed
   (a purlin base plate = equalisation layer for wall/roof tolerance mismatch, not structure).
2. **Joint plane ⟂ force axis** — an inclined joint = parasitic sliding (arch stones cut
   radially to the thrust line).
3. **Equal strength both faces, else spread the area** — steel onto concrete needs a widened
   plate (steel ≈ 10× concrete bearing); timber beams loaded ⊥ grain need Sattelholz/dense
   hardwood pad; in wood, avoid losing the compression: if the load can vanish (uplift, wind,
   traffic, chord shrinkage pulling off a post's end grain) divert it into a tension route
   (straps/through-bolts) — a gap = zero stiffness.
4. **Anti-slide** — friction from the compression itself (masonry) or mechanical key/bolts
   (baseplate anchors take only the minor transverse share; the shear key/Schubknagge takes the
   main one so anchors see uplift only).

Bearing lengths at wall heads, lintel bearings, corbels and precast cleats: numeric rules live
in `masonry-construction` (lintels/arches) and `structural-systems` (precast bearings, cleats);
this skill's demand: **every bearing needs a drainage/ventilation escape at its edges and
never sits in the damp zone** (embedded beam ends historically killed by trapped moisture —
project the bearing out or ventilate it).

### 3.3 Design-connection axioms (from force-path discipline)

- **Shortest force path — "don't take forces for a walk."** Align member axes coincident (2
  members) or concurrent at ONE point (>2); else eccentricity = bending you did not design.
- Introduce point loads where the receiving member is stiffest (normal load into a thin tube
  wall = buckling; tangent load fine — geometry, not material).
- Avoid acute angles (waisted cuts, no tool/bolt room); no skimming cuts; leave **movement +
  tool access space** at every joint; keep joints maintainable/reachable.
- Where possible make members **continuous across storeys** instead of splicing at the worst
  point (secondary beam over primary top = no splice; column splices at zero-moment points).
- **Stagger the functions**: separate the load path from the seal path where possible
  (point-fixed glass: sealant joint carries nothing); where layers must shift, plan the shift
  at the joint, never in the field.

### 3.4 Tolerances, setting-out and dimensional coordination

**Two strategies, one chosen per project:** (a) rework on site — traditional, impossible in
industrial build (cast-in anchors vs later steel = the classic collision and liability fight);
(b) **plan the slack**: design tolerances as adjustment zones. This skill mandates (b):

- **Planned minus-dimensions (Mindermaß)** so nothing is ever too big: thick historic mortar
  beds absorbed brick scatter; loose bolt holes; slotted holes; compressible bedding layers.
  As generous as needed, as tight as affordable — **precision is expensive; tolerance planning
  is safety planning.**
- **Coordination spaces:** a component fits inside its coordination volume, never into the
  neighbour's; the margin between component and space = the tolerance. Brick-derived
  octametric grid 12.5 cm (Handgreifmaß; NF brick 240×115×71 + 10/12 mm joints → 25 cm module);
  ISO 1006/2848 basic module 1 M = 100 mm; two product grids coexist (plasterboard 1250 vs
  600/900 stud grids — the junction of a 625-stud wall and a 500-module window is a planned
  tolerance problem, solve it on paper).
- **Achsmaß vs Rohbaumaß:** set-out from the **axis** (Achsmaß: wall axis at half thickness —
  240 wythe axis = 120 from face), fabrication from **Rohbaumaß** (finished opening/face
  dimension), always with the layer build-up allowance + adjustment gap. Fix per drawing which
  reference line the layer stack grows from (innen-lotschlag vs achse-lotschlag) — mixing the
  two is how reveal insulation "disappears" and how window cappings miss the frame.
- **Tolerance classes clash between trades** (steel = precision champion of primary structures;
  cast concrete = scatter; masonry = bed-joint absorption; timber = shrinkage drift). Between
  two accuracy classes there must be an **adjustment layer in the detail** (grout pad, shim
  zone, slotted holes, variable render bed) — never let the two hard classes touch directly.
- Governing standards: **DIN 18202** (deviations/tolerances in building construction —
  the flatness + height tolerance tables **[VERIFY current issue — not reproduced in the
  digest]**) and **DIN 18203** (execution tolerances for components; −3 timber named in the
  digest). Flag on drawings which tolerance zone (A/B) per DIN 18202 is contractually demanded
  — tighter zones cost money at every preceding trade.
- **Service-state allowances are distinct from fabrication tolerances:** expansion gaps at
  dissimilar fixings, sliding bearings, compression travel of seals — mark them in the detail
  so site does not "helpfully" grout them solid.

### 3.5 Modular coordinate system — vocabulary and a worked example (digest-backed)

The basic module is **M = 100 mm**; multi-modules in DACH/international practice run 3M
(300 mm), 6M (600 mm), 12M (1200 mm) — the same 1 M = 100 mm anchor already used in §3.4 and
Appendix A (ISO 1006/2848, DIN 4172), restated here with the reference-point vocabulary that
resolves *where inside its coordination space* a component sits (Neufert, *Architects' Data*
(Neufert_2002.pdf excerpt), p.34):

- **Coordinate space:** a coordinate system is a set of planes at right angles to each other,
  spaced per the coordinate dimensions; a component's nominal size, plus the joint/tolerance
  allowance to its neighbours, is what fills one coordinate dimension.
- **Boundary reference:** the component is specified **fully by its size and position at once**
  — it is arranged to exactly fill the space between two parallel coordinate planes, joints and
  tolerance included. This is the default for repeating trade components (panels, blockwork
  courses, window/door coordination zones per §4.3).
- **Axis reference:** the component's **central axis coincides with one coordination plane**;
  the component is specified with reference to that axis **in position only** — its size is
  independent information. This is the same logic as the Achsmaß set-out rule already stated
  above (wall axis at half thickness) generalised to any component, not only walls.
- **Non-modular zone:** components that are not worth modularising individually (an individual
  stair tread, a window, a door) are grouped into a **non-modular zone**, which splits the
  coordinate system into two sub-systems either side of it. The assumption is that the
  component's dimension inside that zone is already fully known and fixed at the time the
  surrounding coordinate system is set out — so the modular grid on either side does not need to
  "solve for" the non-modular component's exact size, only for the zone's outer boundaries.

**Worked example — sizing a precast RC staircase unit inside a fixed 30M floor-to-floor module**
(digest, p.34): floor-to-floor height 300 cm = 30 M.

```
Provisional riser ≈ 19 cm (assumed comfortable riser) → n = 300/19 = 15.8 → round UP to 16 risers
Actual riser:      h = 300 cm / 16 = 18.75 cm  (fixed by the modular floor height, not chosen freely)
Provisional going: 16 risers × ≈26 cm assumed going ≈ 416 cm → round UP to the next module,
                   420 cm = 42 M (the staircase's own plan-length module)
Actual going:      b = (420 − 1 cm joint) / 16 = 419/16 = 26.2 cm
```

Reading the method, not just the numbers: the **floor-to-floor module (30 M) is fixed and
non-negotiable** (it is set by the storey-height coordinate system of the whole building); the
riser count is chosen to divide it evenly (round to a whole number of risers first, THEN compute
the exact riser height — never the reverse); the going is sized second, against its own 6M/12M-
style modular plan length, with the standard 1 cm joint/tolerance allowance subtracted before
dividing by the riser count. This is boundary reference applied twice in series (floor-to-floor
height, then plan length) with the stair unit itself treated as one non-modular component sized
to fit exactly between two coordination planes. Sanity-check any hand-run stair against the
step-safety formula 2h + b ≈ 59–65 cm (`structural-systems`/ergonomics literature) — the modular
fit and the ergonomic fit are two independent constraints that must both pass; a module-driven
riser/going pair that fails 2h+b needs a different riser count, not a fudged tread.

---

## Section 4: The Junctions (Anschlüsse) — Detail-by-Detail

For each junction: **what hands over what**, the build-up rules, the numbers, and the classic
failure. Run every junction through the §1.1 function list — a junction that solves moisture
but breaks airtightness has failed.

### 4.1 Wall–footing / plinth (Sockel) — the three-water collision

The plinth is where splash-back (Schlagregen reflection off paving), ground capillary reach and
mechanical damage collide; it is a **different exposure class than the wall above** and gets a
**different build-up**, not a continuation of it.

**Core rules:**

1. **Bring the below-grade package 30–50 cm up above finished ground** (Oberkante
   Gelände/Fußboden). The drainage board, perimeter insulation and sealing all run up past the
   splash zone; the wall sealing overlaps the horizontal barrier. Splash zone height grows with
   paving type (rough paving throws farther **[VERIFY practice band]**).
2. **Horizontal barrier (Querschnittsabdichtung)** in the bed joint at base-of-wall level cuts
   rising damp — **possible in masonry, impossible in RC walls** (rebar continuity) → there the
   joint waterstop at the footing Arbeitsfuge substitutes (and WU crack control is the sealing).
   Dense plinth material under porous wall = the traditional capillary break + mechanical
   protection in one; the plinth render (hydrophobic) forms the transition to the wall sealing.
3. **Ground moisture classes decide the sealing grade** (legacy scheme, still the design logic):
   Bodenfeuchte (permeable sand, non-pressing → tight coating class ok), stauendes Sickerwasser
   (cohesive clay backing up → full waterproofing), drückendes Wasser (below design GW →
   hydrostatic all directions + buoyancy → reinforced, **protected** waterproofing per DIN 18533
   **[VERIFY class→layer mapping in current issue]**). Repairability near zero (excavate!) →
   double precautions: protection board against backfill, filter layer, drainage.
4. **Drainage package, outside → in:** soil → filter fleece (silt block) → drainage board/
   dimple mat (channels water down, relieves pressure, protects the sheet) → Perimeterdämmung
   (closed-cell only — XPS/foam glass: no water uptake, no loss of λ, crush-resistant) → slip/
   protection fleece → sealing → structural wall. Drain pipe at footing on falling gradient to
   soakaway/separator: **pipe invert ≥ 0.20 m below top of foundation slab; inspection shafts
   DN300 at ≤ 20 m spacing and at every direction change; design infiltration allowance before
   walls ≈ 0.30 l/(s·m²) non-mineral elements (DIN 4095 practice figures [VERIFY edition])**.
   Under-slab area drain where required; gravel bed under slab kills capillary rise AND frost
   heave (open granular packing gives ice the void space to expand into).
5. **Black/white tub transition** at the slab edge is the critical line: the vertical tanking
   train runs **down to meet the horizontal one on the footing** — overlap + bond (wall sheet ↔
   slab sheet ↔ any cross-section seal at floor level). White tub: waterstop strip at the
   wall–baseplate cold joint, separation foil + lean concrete under the base slab. Where the
   two systems mix (WU wall + taped sheet at an opening), the sheet termination gets a
   clamping profile + sealant bead — detail it, do not "tape it on site".
6. **Backfill is a construction-stage load case:** compaction earth pressure often EXCEEDS
   at-rest pressure (DIN 4085 practice) → unprotected waterproofing/insulation is at risk from
   the first lift. Keep compactors ≥ ~1.0–2.0 m from the wall (traffic-distance logic of
   trench-support practice), backfill in ≤ 30 cm lifts both sides, protection board continuous,
   and no frost-susceptible cohesive soil (class F3) in the immediate wrap — granular F1 envelope.
7. **Timber above the plinth:** never on damp ground — sole plates on the sealed plinth top
   over a waterproof isolation strip (which also spreads bearing); end-grain suction of a post
   standing in a groove = the classic rot hotspot; keep ≥ 30 cm clearance from splash zone to
   any timber.

**Failure classics:** sealing stopped at grade (splash wicks above it); perimeter insulation
left exposed to UV/mechanical damage; light-block plinth with no barrier → efflorescence +
salt-spalled render band; drain pipe laid *above* slab invert → soaked blinding; WDVS boards
running to grade without a beaded, splash-protected base.

### 4.2 Wall–slab / floor–wall (Auflager + Ringanker + Flanke)

Three jobs at one line — **bear, tie, and decouple** — in this order of permanence:

1. **Bear (vertical):** slab seated on wall head (masonry: full-area mortar bed — §3.2;
   precast: seat length + bedding + centering sleeve/dowel; timber: platform on top plate or
   ledger; solid timber wall–floor nodes A–F per `timber-steel-design`/digest — prefer load
   along grain of the wall, never rely on transverse compression of end grain for storey
   stacking). The slab's two-way action loads all four walls of a cell ~equally — keep bracing
   walls loaded (never "rob" a bracing wall by swapping in a column beside it; replace the
   column WITH the wall).
2. **Tie (horizontal + uplift):** floor diaphragm chord forces end HERE: **Ringanker/Ringbalken**
   (ring anchor/beam at floor level) must run through the junction with dowelled/stirrupred
   continuity; triggers from masonry practice: > 2 storeys, building length > ~18 m, large
   openings, unfavourable ground **[VERIFY per EN 1996/NA]**; ring beam max span ≈ 30× slab
   thickness. Uplift couple arm = wall length — the tie-down force at the windward wall base is
   a serviceability-grade fact of life at this junction; anchor per calculated hold-down,
   not by catalogue habit.
3. **Decouple (movement + acoustics):** slab shrinkage/creep/rotation shortens and turns at the
   wall head → allow a sliding/rotating bearing or accept controlled cracking in the wall
   (fine distributed Schwindbewehrung). Acoustically the same line is the main **flanking path**
   (Kij of the T/cross joint):
   - floating screed must **continue over the junction and up past the wall with the edge
     insulation strip** (Randdämmstreifen), covered by skirting — never pinched by the wall;
   - partitions either run **to the structural slab** or the screed is **cut under the wall** —
     a partition standing on floating screed is a rigid sound bridge and a crack-maker;
   - elastic joint factors are cheap and real: a 15 mm rubber-granulate layer (E_dyn ≈ 0.6 N/
     mm³) at a cross joint lifts R_Ff into the low 70 dB range (digest worked case); fully
     separated joint > partial elastic > rigid (same wall, stiff vs elastic edge: measured
     ≈ 0.1 dB when direct path governs, decisive when flanks govern — compute the case);
   - vertically slotted/grooved wall–floor supports (ZIS-type sliding connections) reduce
     flanking AND absorb settlement (non-loadbearing partitions: build **top-down**, floor
     deflection ≤ l/500, never let the slab land on the partition).
4. **Layer continuity across the line:** the airtight layer of a timber/CLT floor-to-wall joint
   = taped plywood/CLT rim + tape to wall air barrier; the vapour check of the wall must not be
   bridged by a warm-side concrete flange without hygrothermal check; MEP pipes crossing the
   junction go in sleeves before the screed date (§4.9).

### 4.3 Wall–window (Anschluss) — the worst trade interface in the building

A window meets a layered wall in one 100 mm-wide band; the whole continuous air/water/thermal
line must transfer wythe→reveal→frame→sash→glass in series (§1.5). Full system ownership:
`openings-windows-doors` (unit, lintel, sill, Dichtungsstufen numerics); the junction-side laws:

1. **Three sealing levels (Dichtungsstufen / Drei-Ebenen-Anschluss), one memory rule:
   "innen dichter als außen" — inside airtight, middle thermally effective + wind-tight,
   outside rain-braking and vapour-open.** Outside = multi-stage (bremsen + drain + dry),
   inside = single-stage airtight band (taped, continuous, protected). RAL-GZ 996 mounting
   guideline is the practical anchor **[VERIFY current edition]**. Sequence at the sill: sill
   drip/oversail → frame rebate gasket → compression tape → interior airtight tape — each link
   laps the previous in water-flow direction.
2. **Mount in the insulation plane** (or as close as the wall allows): frame centered in the
   insulation layer (timber: Fenster in Dämm-Ebene; masonry+WDVS: bracket/cantilever the frame
   out onto the insulation plane) → the isotherm stays in the insulation, Ψ collapses toward
   zero, interior surface stays above mould limit; recessed mounting keeps the cold frame nose
   → reveal condensation. When the plane cannot coincide, **overlap the insulation layers**
   (reveal insulating strip lapping into façade insulation) so there is no cold path at the
   step — level offsets without overlap are the failure mode.
3. **Flank insulation (Laibungsdämmung)** continuous on all three sides; head zone respects
   arch-action limits for masonry (load in the wedge above the head = design the lintel fully —
   see `openings-windows-doors`); reveal depth dimensioned so the sill falls and the capping
   can shed ≥ 40 mm beyond the frame face **[VERIFY practice band]**.
4. **Anchors are bridges — concentrate them to points:** fixings through insulation = point
   thermal bridges + condensation seeds (a WDVS field shows ≈ +0.02 W/m²K U-penalty for a
   2.8/m² dowel pattern, λ_f = 50 — digest case); use stainless (λ 17–30) or plastic (λ ≈ 0.25
   ≈ no bridge), at static minimum count, at bearing lines; thermally broken fix brackets.
5. **Tolerance gap is a designed layer:** frame-to-opening gap = adjustment zone for
   construction scatter (§3.4) — filled by compression tape/backer rod + sealant (never empty,
   never pure foam as the seal), sized so the sealant depth:width ratio survives the ± movement
   of the two build-ups (render shrinks, frames cycle hot/cold — differential movement is the
   chronic cause of torn reveal sealants; accommodate with soft backing + wide joint + primer).
6. **Numbers to sanity-check the detail** (digest worked cases): reveals Ψ ≈ 0.065, sill ≈
   0.068, head ≈ 0.068 W/(m·K) for average work vs much better for insulated-plane mounting;
   frame-area share is a lever: Uw = (Ag·Ug + Af·Uf + lg·Ψg)/Aw — e.g. target Uw 1.1 with Ug
   0.9, Uf 1.4, Ψg 0.05 at 4.1 m glazing edge → max frame area 0.39 m² = 19.5 % of a 2.0 m²
   window; a mixed façade with U_wall 0.30 vs Uw 1.4 allows only ~14 % window area at an
   energy balance U_mix of 0.45 — the junction quality decides whether these budgets survive.
7. **Acoustic copy of the same line:** the window joint is a leak path (Rs,w joint penalty on
   the whole element — digest shutter-box case: the weakest 1 m² killed a 40 dB façade); double
   rebates + two continuous seals + airtight taped flanks are also the acoustic fix.

### 4.4 Wall–roof — eave, knee wall, gable, parapet

The roof stack (§1.4) arrives at the wall; ownership of roof internals:
`roofing-waterproofing`. Junction-side:

- **Eave (Traufe):** the wall/roof Ψ can be *negative* when detailed right — digest FE case:
  L2D 0.453 W/(m·K) minus 1D references (U_w 0.22 × 1.235 m + U_roof 0.18 × 1.325 m) = **Ψ =
  −0.057 W/(m·K)** (the roof insulation cap over the wall head warms the junction). Rule:
  run the insulation plane THROUGH the junction as one continuous dome — no level step;
  ventilation gap of the pitched roof passes the eave unobstructed (soffit vents / continuous
  eave strip; bird mesh), air barrier of roof overlaps air barrier of top plate/wall head with
  ≥ 50 mm lap + tape **[VERIFY vs product]**; drip: gutter or deep overhang — a gutterless
  deep eave blows roof water concentrated onto the wall = classic scour damage; the top wall
  course/edge is a dense, drained, drip-edged element (Abreißkante).
- **Attic/knee wall (Kniestock/Drempel) + gable:** three build-ups meet (wall, attic-floor
  ceiling, roof): the airtight layer makes the round trip without pinching; the attic-floor
  insulation extends ≥ 240 mm up the knee wall (blow-in overlap at minimum **[VERIFY practice
  value]**); the gable's weather skin laps the roof covering in flow direction (verge detail —
  `roofing-waterproofing`); gable tied to truss for wind bracing (suction can be ≥ own weight —
  structural note to `structural-systems`).
- **Flat-roof-to-wall (Attika/parapet):** upstand (Aufkantung) minimum ≥ 150 mm above finished
  roof surface, higher where wave/splash from drains is possible **[VERIFY vs current
  flat-roof rules]**; joint folded up = lifted out of the water plane (§2.4); **Ausrundung/
  Hohlkehle** fillet (insulation wedge, ≈ 5 cm radius class) so the sheet bends on a radius,
  not a crease; release strip (Trennstreifen) in the corner so slab rotation does not tear the
  upstand; cover strip/pressure profile mechanically fixed ABOVE the sheet top edge with the
  fastener line shielded by the parapet coping drip; parapet coping sloped with joints sealed
  against capillary inflow. Parapet Ψ digest value 0.092 W/(m·K) = what uninsulated parapets
  cost; insulating the parapet on all sides (attika-dämmer) brings it near zero — and note
  wall–flat-roof junction Ψ −0.012 in the same table: good detailing pays twice.
- **Openings through the roof plane (uplight/roof window):** kerb with the sealing layer
  lapped up the kerb, gutter flashing below, step flashing sides — every lap in flow direction
  (ownership: `roofing-waterproofing` §roof-window; junction law: same as §4.3 staging).
- **Two-leaf wall at roof edge:** outer wythe terminates in a weepable, vented closure; the
  bracket anchor at the top storey takes the accumulated outer-leaf weight — spacing ≤ every
  storey; cavity stays clear of mortar droppings up to the last course (a droppings bridge at
  the eave = wicking lane into the inner wythe).

### 4.5 Roof/wall top and edge terminations (Aufkantung, cover strips, ballast)

Where a sealing layer must END (roof edge, balcony door head, duct penetration upstand, trench
gutter cover):

- **Fold up, don't stop:** the raised edge (Aufkantung / standing seam / "floating upstand")
  removes the joint from the water film; movement absorbed by bending the upstand legs
  (compliant ⟂ to motion) — the folded fins also stiffen the thin sheet (why 0.5–0.8 mm metal
  standing seams are structurally usable).
- **Termination ladder (prefer top):** clamp profile under a mechanically-fixed, drained cover
  strip (seal not exposed to UV); → compression bar + gasket; → sealed undercut edge
  (Wetterschenkel + Tropfkante so the sheet's lower edge tears the water film off away from the
  wall). Never: bare cut edge of sheet in the water plane.
- **Bekiesung / ballast termination:** gravel 16/32 (≈ 50 mm bed) runs to a **Kiesfang** (gravel
  stop: perforated edge profile keeping ballast off the drainage path while letting water
  through); ballast kept ≥ 300 mm clear of drains, outlets and expansion-joint strips
  **[VERIFY vs drainage plan]**; on inverted roofs the filter fleece laps UP the edge strip —
  fleece-to-fleece lap ≥ 100 mm, never a bare XPS skin at the edge (UV + wind flutter).
- **Abscheiter/drip-diverter logic at every horizontal-to-vertical exit:** slope the top face
  outward ≥ 5 %, sharp arris below = tear-off; a cover strip laid flat against the wall must
  tip ≥ 3 mm off the wall face so capillary contact cannot draw water up **[VERIFY value —
  principle-level]**.

### 4.6 Floor–screed–structure (schwimmender Estrich and its honest limits)

The floor is a horizontal double-leaf: screed (mass) on insulation (spring) on slab (base) —
plus pipes, plus flanking walls. Rules:

1. **Floating, never pinned:** screed on separating/insulating layer with **edge insulation
   strip** full perimeter (dressed so the finished floor/skirting covers it, the strip is not
   a gap filler but a designed movement joint); no mortar fins bridging to the slab, no anchor
   through the screed into services without a sleeve (§4.9). The "onion" build-up (each layer
   loose on the previous, movement absorbed plane-by-plane — Zwiebelprinzip) is the default
   for impact-sound and crack-tolerance **[VERIFY: use as coordination concept, not a norm
   term]**.
2. **Where bonded is required:** flat-slab buildings with partitions placed late/freely need a
   BONDED screed (Verbundestrich) so partition movement does not crack a floating layer —
   decide before fit-out freedom is sold; a bonded screed gives up the acoustic spring (use
   underlay + finished floor instead).
3. **Joint grid:** screed shrinkage cracks unless cut — sawn joints at door thresholds, aspect
   ratio ≤ 1:1.5 per field, field size ≈ 30–40× thickness for cement screed, heating screed
   fields tighter **[VERIFY all three vs DIN 18560 + slab-heating guideline — the digested
   tables did not carry them]**; for bonded concrete topping/outdoor slabs the digest-backed
   figure: transverse sawn joints ≤ 5.0 m spacing (roadway practice) is the same physics.
4. **Heating screed:** pipe cover ≥ 45 mm above pipe crown, edge insulation at heated perimeter
   strips, expansion joint at every threshold + around embedded bodies, and the build-up under
   the pipe layer must not puncture the separating layer below (foil-faced boards taped)
   **[VERIFY thickness per DIN 18560-2 / system data]**.
5. **Acoustic sizing loop** (from `building-acoustics`, the construction-side duties): f0 of the
   mass-spring < 100 Hz via screed mass (≈ 90 kg/m² typical cement, more for stone-chip dry
   screeds) and soft mat (s' low: ΔLw = 13 + 14.2·lg m'_screed − 20.8·lg s' — digest); keep
   dynamic stiffness s' after the load case (EPS under floating screed creeps → doubled s'
   killed a designed +6 dB improvement in the digest case S41b); impact improvement ΔR of the
   floor build-up has to be counted into the flanking joints, not only the field.
6. **Layer order over ground-contact slabs:** sealing normally ON TOP of slab under a protecting
   screed (protect from construction traffic!); drainage/gravel UNDER the slab cuts capillary
   rise; where heavy point loads rule (industrial), move the sealing BELOW the slab instead.
   Frost heave under ground floors: granular filter or footings below frost depth (soil classes
   F1/F2/F3 — cohesive silts/clays F3 = heave candidates; `geotechnics-foundations` owns the
   calc, the detail obeys it).

### 4.7 Balcony / loggia — cantilever, thermal break, drainage redundancy

The balcony is a cold bridge + a water tank + a railing anchor + a movement joint in one.
Waterproofing stack ownership: `roofing-waterproofing`; construction-side laws:

1. **Thermal break — pick one of four strategies (ladder of quality):**
   (a) wrap the cantilever fully in insulation (inside the warm envelope — bulky underside,
   zero bridge); (b) insulate partway along its length (lengthened path ≈ bridge removed —
   upstand insulation collar at the root); (c) **cut the section and reconnect through the
   insulation with minimal low-λ connectors** (stainless λ 17–30 + corrosion-safe, plastic λ ≈
   0.25) — the standard prefabricated balcony connector principle (specify by λ, load capacity
   and fire behaviour, not by brand name); (d) give the balcony its own ground
   support = no connection at all (best physics, needs structure + settlement clearance).
   Steel through-cantilevers (λ 50–60) and concrete roots (λ 2.3) are absolute bridges —
   digest equivalence: 23 cm steel plate R = 0.1 = 4 mm of insulation.
2. **Water sequencing:** falls ≥ 1.5–2 % away from the door **[VERIFY vs DIN 18195-successor/
   flat-roof rules]**; waterproofing runs UP the parapet/threshold side and laps the wall
   sealing (door threshold = highest wear point: drip slot + sealed upstand); surface water
   cannot reach the thermal-break zone — if a drainage-failure can immerse the connector zone,
   the design is wrong (connector materials are not waterproofing).
3. **Drainage redundancy:** primary drain/scupper sized for the rainfall + an independent
   overflow (threshold lowering or overflow gap ≥ 1.5 cm below finished sill) — a blocked drain
   must not flood the flat roof surface adjacent to the door; where the drain crosses the
   sealing, the outlet is an upstand with a clamped collar, never a hole in a horizontal lap.
4. **Railing/guard posts:** anchor **through a raised, watertight upstand sleeve or on the
   structure beyond the sealing plane**, with the collar lapped by the field sheet; posts
   bolted onto the waterproofing with face-flush anchors = punctured pan; glass-clamp bases on
   the topping with load-spreading discs (§ below).
5. **Raised paving on the balcony = horizontal double-leaf:** point bearings on the waterproofing
   are the enemy — wide disc feet spread the load; open joints drain to the sealing below which
   must therefore be smooth-drainable; the paving plane is sacrificial, accessible, and never
   bonded to the sealed layers.
6. **Movement:** the cantilever rotates at the break line under live load, cycles thermally at
   the connector; screed/topping over the balcony is jointed off the room floor (separate field,
   compressible edge), and the joint at the door line gets a drainage bay (spillway) behind the
   visible cover strip.

### 4.8 Internal walls — bond, lintels, bearings, installation zones

- **Wall–wall (corner/T):** true wall construction = **Einbinden** (toothed corner built
  simultaneously — the bond turns the corner because the orthogonal module allows it; 6 brick
  positions per unit); substitutes: bed-joint anchors (Bewehrungsstäbe/connector strips) where
  sequences differ; cooperating flange widths per EN 1996-1-1 tables when a cross wall leans on
  a longitudinal one — the bracing-wall minimums (effective height ≥ h/5, t ≥ 1/3 of braced
  wall, ≥ 115 mm) decide which T-joints are structure — `structural-systems`/`masonry-construction`.
- **Lintels/openings:** arch vs bending logic, bearing lengths, relieving arches:
  `openings-windows-doors` owns numerics; the junction rule here: **jambs of openings are force
  concentrations that grow with opening width** (double jamb studs/headers in timber; pier
  widths in masonry), and sill panels (Brüstungsfelder) carry nothing (loads bypass via jambs) —
  a structural freedom that must not be sold as a free penetration.
- **Wall–floor (top):** non-loadbearing partitions build **top-down** (slab settlement must not
  load them; vault action to ≤ 7 m spans, thrust must be caught at side bearings; DIN 4103
  line-load cases 0.5 kN/m at 0.9 m); the head gap: compressible packing + sliding groove
  (also −3 dB flanking when both vertical edges elastically decoupled and m' > 150 kg/m²);
  acoustically, **the wall must stop the flanking path it creates** — mass discontinuity at the
  upper wall edge is the standard hidden defect (digest S38).
- **Double-leaf partitions:** cavity ≥ 60 mm (40 mm only if flush-mortared one side); separate
  stud rows = optimum; unequal leaf masses + full mineral fill + no rigid ties (two-leaf party
  wall maths: `building-acoustics`).
- **Installation zones (Schlitze):** vertical chases only within the zone logic, horizontal/
  inclined slots **only in walls t > 115 mm, within 400 mm of floor/ceiling lines (installation
  zones, DIN 18015-3), milled never hammered, never in horizontally-perforated bricks, never in
  chimney walls, never in bearing zones** (digest EN 1996-1-1/NA practice list — VERIFY tables);
  on the airtight side: put services in a dedicated inner counter-stud layer so sockets never
  perforate the single-stage air barrier (§1.1 air-tightness logic; socket leaks = classic).

### 4.9 Penetrations — sleeves, collars, and the discipline of grouping

Every pipe/cable/duct crossing a wall, slab or sealing layer is a layer-discontinuity by
construction — budget them, group them, detail them once each:

1. **Cast them, don't core them:** **sleeves (bewehrte Einbauhülsen / Armiermanschetten)** and
   box-outs go into the formwork/rebar stage (see `concrete-detailing` — through-joint bars);
   cast-in anchors vs late sleeves is the classic trade collision (§3.4). Large duct groups:
   structural opening with lintel design, not a Swiss-cheese wall.
2. **Sleeve detailing law:** sleeve Ø ≥ pipe + insulation + movement; **slope horizontal
   sleeves in external walls outward** (≥ 2 % **[VERIFY practice]**) so rain cannot lie in the
   bore; end of sleeve flush or proud, never a water shelf; annulus sealed by compressible
   filler + sealant (interior air-tape to the sleeve, not the pipe — pipes move/rotate)
   or a proper **flexible penetration seal (Dichtmanschette/collar)** where movement or
   vibration is expected.
3. **Through tanked walls:** waterstop ring bonded to the sheet at the sleeve outer face
   (factory flange preferred), for pressure water a **metal sleeve with sealing collar**
   (incl. approved flexible pipe seals for plastic pipes — system approvals govern
   **[VERIFY: name the product's abZ/ETA in the spec, this skill lists none]**); the drain
   through the plinth per §4.1 invert rule.
4. **Through roofs/flat-roof sealing:** penetration as raised kerb (Aufkantung) with the sheet
   up-turned and clamped (never a flat lap around a pipe at low points — ice-lens lifting);
   snow-melt slide paths (Schneeabrutsch) protected by snow guards above; wire/cable laps over
   sealing = walkway-protection mats.
5. **Acoustic/fire copies:** a penetration with a loose annulus is a tuned flanking duct (the
   digest pipe-seal logic: sealing must reach R of the element or better); fire stops at
   compartment lines per rated collar/mastic system (ownership `fire-protection-building`);
   installation cavities in partition lines get per-storey fire stops in ventilated paths (§2.5).
6. **Fixings that must penetrate insulation** (handrails, façade brackets, sun-shading): by the
   bridge ladder — small section × low λ × short embedment × few in number, on the structural
   line, never in the reveal edge zone of a window; count them into the Ψ/U audit.

---

## Section 5: Buildability and Sequencing — What Must Exist Before What

A detail is only good if the layer order can be *built* in the order the trades arrive. The
sequencing laws follow the build-up logic of §1 and the tolerance logic of §3.4.

### 5.1 The universal layer chronology (exterior element)

```
structure (with planned minus-dimensions + cast-in sleeves)
  → falls layer (screed/tapered insulation) — falls before ANY plane layer, never after
  → warm-side control layer: vapour/air barrier — taped, tested, PROTECTED before covering
  → insulation (plane layer; joints staggered vs the layer below)
  → separating/equalisation layer where the concept needs one
  → cold-side protection: drainage/ventilation cavity, filter, ballast/paving
  → wearing layer (accessible/replaceable above sealed ones)
```
**Never bury an untested function.** The airtightness layer disappears under insulation and
services; if it is not inspected/tape-tested (blower-door interim stage — targets:
`building-physics-thermal-moisture`) before closure, the defect is permanent. Every junction
drawn here carries a **"hand-over inspection"** mark: who checks this line, at which date,
against what reference photo in the object documentation.

### 5.2 Construction-stage rules that decide junction quality

- **Weather-tight the building before the wet trades start** (roof skin + window interim):
  air-lime plasters harden by carbonation (slow, releases build-up moisture), hydraulic binders
  by hydration (work under water/inside cores); cement build-up moisture trapped by early
  vapour-tight finishes = the classic "first winter, wet corners" complaint. Winter
  construction: heated temporary envelope + drying plan, or shift the closing layers later.
- **Protect before you continue:** finished sealing layers get protection boards before any
  wheelbarrow; plinth insulation before backfill (compaction pressure! §4.1-6); window frames
  masked before render; the upstand sheet before the gravel delivery drops on it.
- **Sequencing of the two-leaf / rainscreen trades:** outer wythe and inner wythe rise together
  where anchors are in-course (simultaneous bond = no pinned-anchor retrofit); a later-applied
  outer skin needs its own support (veneer ledge ≥ 2/3 brick width) + bracket anchors per
  storey.
- **Precast logic inverts site order:** elements self-stable on release (form-fit gravity
  supports, centering pins, elastomeric pads, CG below bearing); site joints pinned + form-fit
  because they must be QUICK (moment frames are impossible on cranes); sealing layers of
  sandwich elements applied in the factory (dry, clean), site work limited to lap + tape;
  storey panels ≈ 3 m tall / ≤ ~4 m wide transport envelope → the **joint pattern of the
  build-up is fixed on the shop drawing, which is the tolerances drawing** (§3.4).
- **Tolerance stack goes into one designed adjustment layer, not spread over all:** bedding
  mortars, grout pads, shim zones, slotted holes; every additional "little gap everyone
  absorbs" multiplies scatter into the junction.
- **Concealment rule:** anything that cannot be inspected after completion must be either
  (a) redundant (multi-stage) or (b) factory-jointed. Field-buried single-stage seals in
  inaccessible zones are how litigation starts.

### 5.3 Coordination instruments

Detail catalogue by junction type (not by product!), layer-stops schedule (every layer: where
it starts, ends, laps, tapes), tolerance allocation sheet per trade pair, and the **build-up
continuity test** per sub-function (§1.1 list: protection functions need CONTINUOUS surface
action; storage mass needs area but may be discontinuous; load path may concentrate).
Copying catalogue details fails on non-standard junctions — the method is: task → problem
list → physical effect (Wirkprinzip) → solution principle (Lösungsprinzip) → variant →
definition (that is the detailing curriculum; a catalogue is its answer sheet, usable only
where the question matched).

---

## Section 6: Critical-Dimension Cheat Sheet (digest-backed values)

| Quantity | Value | Where / flag |
|---|---|---|
| Plinth continuation above grade | 30–50 cm | §4.1; splash class decides |
| Min surface fall (drainage) | ≥ 2 % | flat roofs/terraces; aim higher; §4.6/roofing |
| Gravel ballast grade | 16/32 mm, ≈ 50 mm bed | warm/inverted roofs §1.4 |
| Double-leaf cavity (masonry) | ≥ 60 mm; ≥ 40 mm if flush-mortared one side | §1.4/`masonry-construction` |
| Veneer support ledge | ≥ 2/3 brick width | §1.4 |
| Outer-wythe anchors | every storey (bracket at slab, wire in wall) | §1.4/§4.4 |
| Fire stop spacing, ventilated cavities | ≈ every 50 cm height | §2.5 [VERIFY] |
| Ring beam max span | ≤ 30 × slab thickness | §4.2 |
| Ring anchor triggers | >2 storeys, L > 18 m, big openings, bad ground | §4.2 [VERIFY per NA] |
| Bracing-wall minimums | eff. h ≥ h/5·(length), t ≥ 1/3 braced wall, ≥ 115 mm | §4.8 |
| Partition design line load | 0.5 kN/m @ 0.9 m (DIN 4103 case 1) | §4.8 |
| Slab deflection limit for partitions | ≤ l/500 | §4.8 |
| Horizontal chases | walls t > 115 mm, ≤ 400 mm from floor/ceiling, milled | §4.8 |
| Concrete cover (durability era) | 30–40 mm (was ≥ 25 hist.) | `concrete-detailing` |
| Rebar bar pitch / vibrator head | 100–150 mm / Ø 60–80 mm | `concrete-detailing` |
| RC vs steel α_T | 10 vs 12 ×10⁻⁶ 1/K | §2.5 |
| Wood delivery / service MC | ≈ 20 % → 7–12 % equilibrium; keep < 15–18 % vs rot | §2.5/`timber-steel-design` |
| Water λ vs air λ | 0.6 vs 0.025 W/(m·K) (≈ 24×) — wet insulation = dead insulation | §1.1 |
| λ bridges: steel / alu / stainless / plastic | ≈50–60 / ≈200 / 17–30 / ≈0.25 W/(m·K) | §4.3/§4.7 |
| Fastener U-penalty, WDVS | ≈ +0.02 W/m²K at ~2.8 dowels/m² Ø 6.3 λ50 | §4.3 digest case |
| Eave junction achievable Ψ | −0.057 W/(m·K) (good detail) / parapet bad 0.092 | §4.4 digest FE |
| Reveal / sill / head Ψ (average work) | 0.065 / 0.068 / 0.068 W/(m·K) | §4.3 digest table |
| Sealant depth:width | ≈ 1:3–1:4 | §2.3 [VERIFY product] |
| Upstand above finished roof | ≥ 150 mm | §4.4 [VERIFY norm value] |
| Fillet radius at upstand | ≈ 5 cm (Ausrundung) | §4.4 [VERIFY product min] |
| Drain invert below slab top | ≥ 0.20 m | §4.1 DIN 4095 practice |
| Inspection shaft spacing | DN300, ≤ 20 m + every turn | §4.1 |
| Backfill lift / compactor distance | ≤ 30 cm lifts / ≥ ~1–2 m from wall | §4.1 |
| Pipe sleeve annulus | sloped outward ≥ 2 % external | §4.9 [VERIFY] |
| Screed sawn-joint grid (concrete topping ref.) | transverse ≤ 5.0 m | §4.6 (roadway-ref) |
| Heating-screed pipe cover | ≥ 45 mm crown | §4.6 [VERIFY] |
| Basic module | 1 M = 100 mm; brick grid 12.5/25 cm | §3.4 |
| Precast panel height (transport) | ≈ storey ~3 m; ≤ ~4 m upright | §5.2 |
| Concrete fresh pressure vs formwork | ≈ 2.5 × hydrostatic water | `concrete-detailing` |
| Fire classes in tables | F30/F60/F90 legacy ↔ EN R/E(I) | `fire-protection-building` [VERIFY edition] |
| Surface-mould criterion | fRsi ≥ 0.70 (new issues 0.71/0.67 by class), θsi,min 12.6 °C @ 20/−5/50 % | `building-physics-thermal-moisture` |
| Glaser condensation caps | 500/1000 g/m²; wood-based 3 M-%, wood 5 M-% | `building-physics-thermal-moisture` [VERIFY 68800-2 note] |
| Two-leaf acoustic target | f0 < 100 Hz (masses unequal, soft fill, wide gap) | §4.2/`building-acoustics` |
| Elastic-edge partition bonus | −3 dB flanking (decoupled edges, m' > 150 kg/m²) | §4.2 digest S38 |

---

## Section 7: Worked Junction Walk-Throughs (numbers from the digested examples)

### 7.1 Plinth + box-wall transition (KS 36.5 + XPS perimeter, heated cellar)

**Task:** exterior cellar wall, permeable-to-cohesive soil, no pressure water assumed.
**Build-up outside→in** (§1.4 box-wall): soil → filter fleece → drainage board → **XPS
Perimeterdämmung 120 mm (λ 0.035)** → slip fleece → sealing (protected, inside face) → KS
365 mm (λ 0.79) → gypsum 10 mm (λ 0.51).
**Thermal check** (digest W8a): R = 0.13 (Rsi) + 0.365/0.79 + 0.01/0.51 + 0.12/0.035 =
0.13 + 0.462 + 0.020 + 3.429 ≈ 4.04 → **U ≈ 0.25 W/(m²K)** with earth-side Rse = 0 — the
perimeter layer alone carries 85 % of the resistance (this is why Perimeterdämmung thickness is
never "value-engineered" at the junction).
**Junction choreography:**
1. footing slab: horizontal sealing train runs from under the slab UP the wall face; overlap
   zone at the wall–footing cold joint gets the **waterstop** (if WU) or bonded sheet lap.
2. Querschnittsabdichtung (masonry): bed-joint barrier at lowest course — under the first KS
   row; the vertical sealing meets it, never stops below.
3. Both packages run **≥ 500 mm above finished grade** (generous end of the 30–50 band: paved
   courtyard throws hard); transition to above-grade WDVS/sealing via beaded, hydrophobic
   plinth render; drainage board + fleece stop at the bead line.
4. Drain pipe: invert 200 mm below slab top, fall to shaft (≤ 20 m), shafts at turns; check the
   infiltration allowance vs soil kf (clay = the 0.05–0.30 l/s·m² class table decides pipe
   spacing, `geotechnics-foundations`).
5. Backfill sequence: wall + sealing cured → protection board → XPS butted (no gaps: a gap
   here is a cold strip at the corner line — corner gets extra 100 mm butt strips, geometric
   bridge) → filter fleece → granular F1 lift by lift, compactor ≥ 1 m off the face.
**QC gate:** photo-log the sealing overlaps before fleece — nothing above is inspectable later.

### 7.2 Eave junction, RC wall + warm pitched roof (Ψ audit proof that detailing pays)

FE 2D result (digest): line transmittance **L2D = 0.453 W/(m·K)**. Subtract the 1D references:
wall U 0.22 over l_W = 1.235 m; roof U 0.18 over l_D = 1.325 m →
**Ψ = 0.453 − 0.272 − 0.239 = −0.057 W/(m·K)**.
What produced the negative value (geometry, in build order): continuous insulation cap carried
from the roof plane OVER the wall head (roof insulation laps the wall insulation plane, no
step); airtight layer runs roof→top-plate→wall with taped ≥ 50 mm lap; ventilation slot kept
clear at the eave so the wall never cools the head; wall top edge dense + dripped.
**Surface check:** with U_wall 0.22 the interior surface stays warm (θsi > 12.6 °C with margin
at 20/−5/50 %), and the Ψ credit counts into the building audit (ΣΨ·l — digest house case:
eaves 0.044 category, ridge −0.012, corners −0.004 — negative values legitimate; the full-audit
ΣΨ·l = 20.88 W/K over A = 1153 m² → ΔU_WB = 0.018 ≪ the +0.10 flat rate: detailed junctions
unlock the energy balance). **Lesson for the model:** carry these junction objects in the BIM
as real layer stacks (§10) so the Ψ list can be re-audited when any build-up changes.

### 7.3 Floating screed over slab with party-wall line (acoustic + movement loop)

**Field:** slab 528 kg/m², cement screed 110 kg/m² (≈ 55 mm) on TSD with s' ≈ 3 MN/m³-class mat.
Digest case S20: airborne of the slab+build-up R ≈ 30.9 + 22.2·lg(528) = 61.9 dB, f0 =
60·√((1/110 + 1/528)/0.06) ≈ 36 Hz (< 100 Hz ✓) → ΔRw bonus ≈ 3.4–7.3 → R_Dd,w ≈ 65 dB;
impact L'n,w ≈ 46 dB after ΔLw ≈ 30 dB (90 kg/m² screed, s' 15 MN/m³) + flanking K ≈ 1.6.
**Junction duties at the wall line (where the calculation meets the trowel):**
1. screed floats OVER the party-wall line with edge strip upturned; the wall continues to slab
   (never on screed) — else a rigid flank + a crack.
2. cross joint at the wall/floor line gets the elastic interlayer: 15 mm rubber granulate,
   E_dyn 0.63 → s' ≈ 42 MN/m³, joint factor K ≈ 18 → R_Ff ≈ 73 dB / R_Fd ≈ 82 dB (digest S62)
   — i.e. the flank stops governing; the direct path does, as designed.
3. screed field: cut or door-line joint at the flat (aspect ≤ 1:1.5); heating loops keep 45 mm
   cover; skirting covers the edge strip without pinching it.
4. movement allowance: slab creep/deflection under the party wall is absorbed by the floating
   bed + head-slot of the partition above (top-down, ≤ l/500 deflection) — the same line that
   decouples acoustically decouples statically.

### 7.4 Window in the WDVS insulation plane (three-stage handover + U budget)

**Geometry:** 175 mm KS + 160 mm EPS-WDVS (λ 0.04; digest W5 sizing: GEG-era U 0.24 needs
≈ 16 cm on 24 cm Vollziegel analog) → frame mounted on cantilever brackets in the insulation
plane, rear 40 mm insulation strip behind the frame bed (overlap rule: reveal strip laps the
façade insulation — cold path broken).
**Seal train, outside→in (water direction left→right):** sill capping sloped, lapped UP into
the frame rebate gasket → compression tape (pre-compressed foam, spring force for life — the
"Druckdichtung" of §2.3) → middle wind-tight plane (tape to airtight board) → interior: taped
air barrier continuing into the plaster/counter-stud layer. Each lap in water-flow direction;
the airtight single-stage line never exposed to sun.
**Anchor bridges:** 4 brackets, stainless shanks through 160 mm EPS — points not lines; verify
θsi at the reveal by fRsi check (if reveal mounted warm-side of insulation, 12.6 °C criterion
survives; recessed cold-nose mounting fails at same U).
**Energy budget check** (digest arithmetic): Uw from (Ag·Ug + Af·Uf + lg·Ψg)/Aw — with
Ψg 0.05, Ug 0.9, Uf 1.4 the frame share cap for Uw 1.1 is 19.5 %; whole-façade mixed limit:
wall 0.30, windows 1.4 → at balance target 0.45 window fraction ≤ 13.6 % — so the *junction*
(Ψ reveal 0.065 typical vs better near zero in-plane) is often the difference between passing
and re-quoting the windows.

### 7.5 Two-leaf clinker wall that traps water (Glaser post-mortem, digest F11)

**Stack (warm→cold):** gypsum 10 mm (μ 4? as digest-listed) / KS hollow 240 (μ 15) / MW 120
(μ 1) / clinker 115 (μ 100). Winter 20 °C/50 % vs −5 °C/80 %, 2160 h condensing period:
R_T = 3.636, Σsd = 15.26 m; vapour pressure line crosses saturation line **at the MW/clinker
interface** (p 446 > ps 411 Pa): in-flow 0.1383 − out-flow 0.0078 g/(m²h) × 2160 h →
**M_c = 282 g/m² ≤ 500 → check 1 passes**; evaporation capacity ≈ 274 g/m² < 282 →
**check 2 FAILS** (drying out insufficient).
**Fixes by principle (not product):** (a) lower outer-leaf sd: lime-based open joint/ render
instead of dense clinker band, (b) raise inner-side sd: denser carrier/added retarder so less
vapour reaches the cold interface, (c) ventilate the cavity (convert to rear-ventilated — the
digest double-leaf strategy (c)) — or (d) hygrothermal simulation credit. **Detailing law
restated: never place the vapour-tightest layer where condensation collects at the COLD side —
the tight layer belongs warm-side (§1.2 rule 1), and every cold dense skin (clinker, tile,
dense render, bitumen) over insulation is a trap until proven otherwise.**

---

## Section 8: Detail QC Checklist (run before issuing any junction)

**A. Layer continuity per function (the §1.1 test, per junction):**
- [ ] Tragschicht: load path explicit through the joint (bearing area, tie chord, anchor group);
      compression guaranteed or tension route provided; no invisible "shared" load.
- [ ] Dämmschicht: insulation plane continuous THROUGH the junction or deliberately overlapped;
      no level step without overlap; anchors/concentrated to points, material λ checked.
- [ ] Luft-/Dampfebene: single continuous airtight line, laps ≥ product value, tape/clone to
      every sister layer (foil→plaster, foil→frame tape, grommets at services); protected from
      perforation (services behind a second insulation/counter-latt layer where dense sockets).
- [ ] Weather staging: outer stage brakes + drains + dries; inner stage tight + shielded;
      every lap faces down-flow; no butt joint in the water film; no open joint where movement
      can close it to capillary width.
- [ ] Acoustic: mass continuity or clean double-leaf (f0 < 100 Hz logic intact); flanking joint
      elastic or heavy-with-spring; no rigid pins across floating layers; penetrations sealed to
      element class.
- [ ] Fire: joint rated as the element; cavity fire stops per spacing; no concealed flue path
      (cavity/vent channel between compartments).
- [ ] Durability: drip/tear-off edges, ≥ 2 % drains, splash-zone materials, UV-shielded seals,
      replaceable wearing layer, maintenance access to every joint that ages.

**B. Geometry/tolerance:**
- [ ] Reference line stated (Achse/inne/außen lotschlag) + Rohbaumaß with Mindermaß;
      adjustment layer located (which trade eats which mm).
- [ ] Movement joint width > computed movement (α·ΔT + shrink + creep + rotation) with margin;
      fix/slide assignment marked per side; waterstop specified at every tanked cold joint.
- [ ] Component in its coordination space; neighbour layers never share a plane edge
      (joints staggered/entflochten across the stack).

**C. Buildability:**
- [ ] Layer chronology buildable (falls before planes; planes before protection; test gates
      before burial); tool access at the joint (drill/tensioner envelope); vibration space at
      cast-in items; no trade collision (sleeve vs bar vs anchor — resolve in model, not on
      site).
- [ ] Every sealed junction has a named inspection stage + document type (photo-log,
      blower-door, water test, backfill permit).

**D. Numbers:**
- [ ] U/Ψ of the junction audited into the building ΣΨ·l list; fRsi/mould check at the worst
      inner surface of the detail; Glaser/13788 at any new cold dense skin; acoustic flanking
      class per joint type assigned (T/cross/elastic/rigid).

---

## Section 9: Failure Gallery — Symptom → Cause → Fix (all digest-backed classes)

### 9.1 Thermal bridges

| Failure | Signature | Cause | Fix |
|---|---|---|---|
| Balcony root streak, black mould | vertical dark band at ceiling/wall at every slab line | through-cantilever = absolute bridge (steel 50–60× MW; 23 cm RC plate ≈ 4 mm insulation R) | §4.7 break ladder: collar insulation / connector plate / freestanding |
| Reveal corners mould (window recess) | winter spotting on frame flank | frame mounted in cold plane; isotherm bent inward | mount in insulation plane + lapped reveal strip (§7.4) |
| Skeleton-column stripes | wall U "0.25" measures 0.29, cold columns | concrete columns carrying in the envelope plane (digest W11 case) | move columns inside, wrap or step them out of the insulation plane (§1.2 rule 2) |
| Anchor-point freckles | dot pattern of stains on insulated façade | steel fixings through insulation | fewer points, stainless/plastic discs, subframe rails, ETICS where possible |
| Parapet/attika loss | ΣΨ·l blows the energy audit (Ψ 0.09 class) | uninsulated protruding edge | full wrap of parapet (wrap ≈ worst but only safe legacy option), or insulated cap + connector |
| Corner geometric bridge | cold inside corner despite good U | isotherm compression at positive corner | corner insulation panels/strips; keep wall count orthogonal and continuous |

### 9.2 Trapped / migrating moisture

| Failure | Signature | Cause | Fix |
|---|---|---|---|
| Wet insulation under flat roof | sagging, blisters, frozen patches | no vapour barrier under sealed warm build-up; or barrier punctured at services | mandatory Dampfsperre warm-side + taped penetrations; invert roof where retrofit impossible (§1.4) |
| Clinker-wall interstitial condensation | hidden, years late | vapour-tightest layer on the cold side (F11 case) | raise inner sd / open outer / ventilate cavity (§7.5) |
| Rising damp band + salt spalling | 0.3–1 m damp band, efflorescence | missing/bypassed Querschnittsabdichtung; sealing stopped below splash zone | barrier injection/dpc retrofit + plinth rebuild per §4.1 rules |
| Black tub squeezed up at joints | local seepage at slab wall line | sheet lapped wrong way / no clamp under backfill pressure | overlap direction down-flow + clamp profile + protection backup wall; keep drainage clear |
| Screed stays wet first winter | curled parquet, musty air | build-up moisture sealed in by early tight finishes (carbonation lime slow; cement hydration water) | drying plan, interim ventilation, layer chronology §5.2 |
| Beam-end rot at wall pockets | localized structural decay | timber bearing in damp masonry without ventilation | ventilated projection (ashlar ledge) or steel shoe off the damp plane (§3.2) |
| Eave scour streaks | stained/eroded wall under gutterless eave | concentrated roof discharge blown onto wall | gutter/drip throw; deep eaves only with drained, toughened facade band |

### 9.3 Acoustic flanking and joint leaks

| Failure | Signature | Cause | Fix |
|---|---|---|---|
| Party-wall on floating screed | speech/bass passes despite 60 dB wall | partition pinned through the spring layer = bridge + crack risk | wall to slab, or screed cut + elastic joint (§7.3) |
| Shutter-box collapses façade Rw | mixed element measured far below wall | weakest 1 m² governs energy mix (digest S12) | box to element class or move it outside the envelope line |
| "Improved" windows worsen room levels | replaced box windows 37→34 dB, façade mix now fails | single-element upgrade ignoring mix | audit composite before swap (S11 lesson); seals/rebates before glass thickness |
| Impact sound at wall line | drumming near perimeter only | rigid floor-to-wall joint, edge strip pinched by skirting/tile | elastic joint (15 mm granulate class) + protected edge strip (§7.3) |
| Two-leaf telephony between storeys | voice carries vertically | through-cavity links + unsegmented ventilation cavity | segment cavity per floor, per-floor vents; no rigid ties; separate stud rows |
| Stud-wall on slab 3 dB lost | heavy wall, light measurement | elastic decoupling bonus only applies if edges actually decoupled & m' > 150 | detail the KE case (top/head slot, resilient base track, no screw-through flanks) |

### 9.4 Joint and connection failures

| Failure | Signature | Cause | Fix |
|---|---|---|---|
| Torn reveal sealants (annual) | cracked/split mastic at frame flank | differential movement (render shrink vs frame cycles) sealed rigid, 3-sided adhesion | backer rod, width ≥ movement, primer-compatible flanks, soft layer |
| Spalled outer-wythe corners | corner cracks + flaking at anchors | expansion joint omitted at inside corner of two-leaf skin | corner movement joint (accept the visual break — §1.4) |
| Leaking cold joint in cellar | drip line at footing-upstand height | no waterstop; honeycombed joint face | planned Dichtungsband + vibration access; repair: injected seal + internal drainage channel |
| Capillary-wicking stone joint | damp seam at flush milled joints | press joint under meniscus width (§2.2) | open joint with chambers or compressed gasket — never bare tight butt |
| Loosened bolt groups in timber | rattling connections after 1 season | wood transverse shrinkage relaxed clamps | re-tension cycle planned, or dowels/straps that don't rely on clamp; slotted holes |
| Screed edge cracks | perimeter crack band, tile lippage at walls | missing/no exposed edge strip, fields too big, joints not cut | §4.6 grid + strip + cut joints; retrofit saw-cuts at field corners |
| Balcony connector zone corrosion | rust jacking at break joint | dissimilar metals wet + no drainage at the collar | nobler-fastener rule, drained collar, inspectable detail |
| Frozen/burst drain at deck | ice lens at outlet | no heat trace/clearance, ballast over drain | keep ballast/plant clear of outlets; drip-cone; redundancy per §4.7-3 |

**Meta-lesson (the digests' own conclusion, restated for detailing practice):** almost every
entry above is a **decision not taken** — the movement was left undecided (§2.5), the layer was
buried untested (§5.1), the joint was copied without checking the question (§5.3). The
detailer's job is not drawing lines; it is **deciding, per layer and per direction, how the
function crosses the line.**

---

## Section 10: FreeCAD Modelling of Layered Walls and Junctions

Model the build-up as **layers, not a single wall with a paint name**. The void-cut workflow
(openings as explicit void objects, parametric Subtractions, volume-difference verification) is
defined in `construction-freecad-bim` and `openings-windows-doors` — reuse it unchanged; what
follows is the layer/junction convention this skill requires.

### 10.1 Layer-object convention

- One reference plane per wall (inside face or axis — set once per project, §3.4); each layer =
  its own solid extruded from the wall footprint, offset cumulatively along the normal.
- Naming: `Wall-A03|L03-Daemm-EPS160` (wall id | layer order + role + product + thickness mm).
- Functional role in property `LayerFunction` ∈ {Trag, Daemm, LuftDampf, Wetter, Schutz,
  Nutzung, Hohlraum/Luftschicht, Fugenzone} — the continuity audit (§10.3) keys on it.
- Cavities: explicit void-class layers (`AirLayer`), never "the gap between objects".
- Junction zones: model the **detail volume itself** (plinth band, eave block, window surround,
  balcony root) as its own stack of layer objects at true local thickness (incl. tapes as 0.5 mm
  planes only where the review needs them visible — otherwise carry them as properties).
- Tolerances: model NOMINAL geometry; record the consumption in Pset fields
  (`ToleranceZone`, `AdjustmentLayer`) — the model is the coordination picture, not the
  as-measured scatter.

```python
import FreeCAD as App, Part

LAYERS = [  # (order, role, name, thickness_m, material)
    (1, "Nutzung", "Gipsputz",      0.010, "gypsum"),
    (2, "Trag",    "KS-365",        0.365, "ks"),
    (3, "Daemm",   "EPS-WDVS",      0.160, "eps"),
    (4, "Wetter",  "Oberputz",      0.003, "render"),
]

def build_layered_wall(doc, footprint_wire, origin, normal, layers=LAYERS,
                       wall_id="W-A03", height=2.75):
    """Extrude each functional layer from the shared footprint; offset along normal."""
    objs, t = [], 0.0
    for order, role, name, d, mat in layers:
        face = Part.Face(footprint_wire)
        solid = face.extrude(App.Vector(*normal).multiply(d))
        solid.translate(App.Vector(*origin) + App.Vector(*normal).multiply(t))
        t += d
        o = doc.addObject("Part::Feature", f"{wall_id}|L{order:02d}-{role}-{name}{int(d*1000)}")
        o.Shape = solid
        for prop, val in (("LayerFunction", role), ("Material", mat),
                          ("Thickness_mm", d * 1000.0), ("DetailRef", "")):
            if not hasattr(o, prop):
                o.addProperty("App::PropertyString" if not isinstance(val, float)
                              else "App::PropertyFloat", prop, "Pset_ConstructionDetail")
            setattr(o, prop, val)
        objs.append(o)
    return objs
```

### 10.2 IFC Pset propagation

Custom property **groups named `Pset_*` export as IfcPropertySets** with the standard importer —
keep the group discipline: `Pset_ConstructionDetail` (LayerFunction, Thickness_mm, Material,
Psi_Design, sD_mm, ReactionToFire_Class, DetailRef drawing no.) on layer objects;
`Pset_Masonry` style sets stay owned by their skills; junction volumes carry the **assumed
calculation basis** (Ψ source: catalogue/FE/hatched-slab rule — the physics skill needs to know
which layers' Ψ values are model promises, not measurements). Export, re-import into a clean
document, and spot-check 5 layer objects keep both group + values before trusting a full export
**[VERIFY against the FreeCAD version actually installed]**.

### 10.3 Layer-continuity audit (the junction QC in the model)

```python
def continuity_audit(doc, roles=("Trag", "Daemm", "LuftDampf", "Wetter")):
    """Per enclosing-loop heuristic: every functional role present at both sides of a
    junction must exist as >=1 layer object per wall; flag missing air-barrier layers."""
    walls = {}
    for o in doc.Objects:
        if hasattr(o, "LayerFunction") and "|" in o.Name:
            walls.setdefault(o.Name.split("|")[0], set()).add(o.LayerFunction)
    return {w: [r for r in roles if r not in s] for w, s in walls.items()
            if [r for r in roles if r not in s]}
```
Run it before any export: an empty result means "no whole layer was forgotten", not "the
junction works" — the geometric overlap/lap logic (§1.2 rules 5/6) still needs eyes, so pair
the audit with the §8 checklist per drawn junction, and keep void cuts parametric so a build-up
change propagates instead of silently orphaning a cut.

---

## Appendix A: Standards and Rules Index (scope + currency flags)

- **Coordination/tolerances:** ISO 1006 / ISO 2848 + DIN 4172 (modular coordination, 1 M = 100 mm);
  **DIN 18202** (building-construction deviations — tables not reproduced here, VERIFY issue);
  DIN 18203-1..-4 (component execution tolerances; -3 timber seen in digest); DIN 18015-3
  (installation zones).
- **Moisture/waterproofing:** DIN 18531–18535 (current waterproofing series; **DIN 18195 legacy
  scheme still in habit — flag in texts**); DIN 18533 classes (Bodenfeuchte / stauendes
  Sickerwasser / drückendes Wasser logic); DIN 18534 indoor; DIN 18540 joint sealing; DIN 18197
  waterstop formwork; DIN 4095 drainage (protecting structures); EN 13967/13970 sheets;
  EN 15812/-15814 thick coatings.
- **Physics:** DIN 4108-2/-3/-4/-7 (thermal/moisture/design values/airtightness — see
  `building-physics-thermal-moisture` for the numeric ownership and GEG transitions);
  DIN EN ISO 6946/13370/13788/13786 (methods).
- **Acoustics/fire:** DIN 4109 (+ -33 flanking calculation); DIN EN 13501-1/-2 ↔ DIN 4102 F/W/T
  notation (both seen in digests — VERIFY edition); DIN 4103 (partitions).
- **Construction systems:** EN 1996-1-1/-1-2/-3 + EN 771 + EN 845-2 (masonry/lintels);
  EN 1992 + DIN 488 (RC/rebar — `concrete-detailing`); EN 1995 family (timber);
  EN 14509 (sandwich panels); DIN 7863 (window gaskets); EN 15651 (façade sealants); IVD-Merkblatt
  22 + RAL-GZ 996 (sealants/mounting practice); Flachdachrichtlinien-lineage rules (trade
  guidelines — VERIFY current edition before citing); ZTV E-StB compaction (backfill near
  basement wraps).

## Appendix B: Items Flagged [VERIFY] / Known Gaps of This Skill

All bracketed VERIFY tags above are principle-level or edition-uncertain (upstand ≥ 150 mm,
sealant 1:3–1:4, joint grids per DIN 18560 (tables not in the digests), heating-screed cover,
ring-anchor trigger list, fire-stop spacing, RAL edition, DIN 18202 zone tables, splash-zone
band, sleeve slopes, reveal capping overshoot). Not covered here by design: lintel arch-action
numerics (`openings-windows-doors`), waterstop/w_k design (`concrete-detailing`), roof covering
classes (`roofing-waterproofing`), flanking K tables (`building-acoustics`), n50/ΔU_WB energy
audit (`building-physics-thermal-moisture`), excavation support (`geotechnics-foundations`).
Existing-building (Bauen im Bestand) detailing — pollutant eras, grandfathering, underpinning —
is a separate competence; junction rules here still apply to retrofit sequencing.

## Appendix C: Glossary (detail short-hand)

Abreißkante/Tropfkante tear-off/drip edge · Arbeitsfuge construction (cold) joint ·
Aufkantung upstand/turned-up edge · Ausrundung/Hohlkehle fillet at plane change ·
Aussteifung lateral bracing · Bekiesung gravel ballast · Bremse braking (first) water stage ·
Brandriegel fire stop in cavity · Drahtanker/Konsolanker wire/bracket wall-ties ·
Dampfbremse/-sperre vapour check/barrier · Dampfdruckausgleich vapour-pressure equalisation ·
Dehnfuge expansion joint · Punktuelle Wärmebrücke point thermal bridge ·
Einbinden toothing (interlocking masonry corner) · Entflechten staggering of layer joints ·
Entspannungskammer pressure-relief chamber · Fassade/Verblendung rainscreen/veneer ·
Flanking Übertragung von Nebenwegen · Gleitschicht sliding layer ·
drückendes Wasser pressing groundwater · Kiesfang gravel arrestor · Kerndämmung cavity-fill insulation · Kniestock/Drempel knee wall ·
Konterlattung/Querlattung counter/cross battens · Lasteinzugsfeld tributary area ·
Luftdichtheitsschicht air-barrier layer · Mindermaß planned minus-dimension ·
Oberkante Fertigfußboden (OKFF) top of finished floor · Perimeterdämmung below-grade insulation ·
Querschnittsabdichtung cross-section (horizontal) barrier · Randdämmstreifen edge insulation strip ·
Regendichtheit vs Wasserdichtheit rain-tight vs water-tight · Ringanker/Ringbalken ring anchor/beam ·
Schalung/Formwork formwork · Schlagregen wind-driven rain · Schwitzwasser/Tauwasser condensate ·
Schwimmender Estrich floating screed · Sockel plinth · Unterspannbahn/Unterdeckbahn/Unterdach
breather/covering/secondary watertight roof layer · Verbund bond/composite · Verband masonry bond ·
Wasserschenkel drip leg/overhang lip · Wärmebrücke (Ψ, λ) thermal bridge · Zwängungen restraint
forces · schwarze/weiße Wanne black/white tub · zweischalig/einschalig single vs two-leaf.

**End of skill. When any output of this skill meets a specialist system, hand off with the
hand-over note: layer roles, the assumed junction numbers (Ψ, fRsi, joint factors), and the
inspection stage that proves them on site.**






