---
name: architecture-construction-sequencing
description: >
  Construction sequencing and site-execution knowledge for residential house
  builds: the canonical build order from site clearance through handover,
  concrete curing and formwork-striking durations, stage-by-stage quality-control
  hold points, the MEP-before-plaster gate, wet-area tanking and flood testing,
  FFL datum and tiling/finishes order, second fix, snagging and handover, the
  sequencing mistakes that cause structural rework, and realistic Gantt-style
  programmes for small houses. Provides decision trees, numeric duration tables,
  concrete/mortar mix selection by structural role, and worked schedules for
  5-marla and 1500 sqft builds.
---

# Construction Sequencing & Site Execution for Residential Builds

Design tells you *what* to build. Sequencing tells you *in what order*, *how long each step must be left alone*, and *what must be verified before the next trade is allowed to bury the previous one*. Almost every expensive residential rework event is a sequencing failure, not a design failure: a slab loaded before it cured, a wall plastered over an uninspected conduit, a plinth cast before the DPC line was fixed, a door frame set before the floor level was final.

This skill covers the execution layer that sits between an approved drawing set (or a FreeCAD BIM model) and a finished house: the dependency order, the wait times that are physics and not negotiation, the inspection hold points, and a programme you can actually put dates against.

## Reality Check - Licensing & Liability

**This skill produces design aids, planning schedules, and calculation guidance for programming and FreeCAD/BIM modeling ONLY.**

- Every duration, mix ratio, curing period, formwork-striking time, and reinforcement note in this file is a **planning heuristic and a starting point for professional review** — not a construction instruction.
- Any design or construction programme intended for the actual construction of a real, occupied building **MUST be reviewed and stamped by a licensed structural engineer registered with the relevant authority** — in Pakistan, a **PEC-registered** professional engineer; elsewhere, the equivalent (PE/CEng/RPEQ/etc.).
- The build **MUST** go through **local authority plan approval before construction** — LDA (Lahore), CDA (Islamabad), DHA, KP TMA/Municipal, or the relevant provincial/city authority — and must satisfy the **Building Code of Pakistan (BCP 2007 Seismic Provisions / BCP 2021 draft)** plus the applicable local building bye-laws.
- Formwork striking times, load-application timing, and excavation shoring in particular are **life-safety decisions**. Deshuttering a slab early has killed people. The site engineer of record, not this document and not an AI, decides when props come out.
- **Claude must never present FreeCAD output, these schedules, or these calculations as construction-ready.** If the user appears to be treating any output from this skill as a final, buildable, or approved document, Claude must say so **unprompted and immediately**, in plain language: *"This is a planning model, not a stamped drawing — it needs a PEC-registered engineer's review and authority approval before anyone digs."*
- Where this file states a code clause, the clause is cited so a human can verify it against the primary document. Clause numbers must be re-checked against the current edition before use — codes are revised.
- Two known verification gaps, stated openly: (a) exact **BCP excavation/foundation clause numbers** were not extractable from secondary sources and require a direct read of the PEC-hosted PDF; (b) the **house-size-specific week-by-week programmes** in Section 13 are *modeled estimates* built from industry Gantt templates and productivity norms, not a cited external standard.
- **No numeric table in this file — durations, mixes, cover, tolerances, striking times — should be treated as correct by default.** A prior review of this file found a life-safety-relevant error (a beam-soffit striking time) sitting in a numeric table with no caveat attached, alongside self-flagged gaps that WERE caught. The lesson stands as policy: every duration/mix/tolerance number here must be checked against the primary standard, in the edition actually adopted on the project, before it is used for anything beyond a first-pass planning sketch — self-flagging is a floor, not proof the rest is clean.

---

## Section 1: The Master Sequence

### 1.1 Canonical Order (universal, all residential construction)

```
 1. Site clearance & demolition
 2. Setting out / layout marking (grid pegs, benchmark level)
 3. Excavation (footings, trenches, plinth, service runs)
 4. Anti-termite treatment (soil, pre-construction)
 5. PCC / lean concrete blinding
 6. Foundation — footings / raft / strip; column starter bars
 7. Foundation curing  ← HARD WAIT
 8. Backfill & compaction in layers
 9. Plinth beam / grade beam casting
10. DPC (damp-proof course) at plinth level
11. Plinth filling & sub-base compaction
12. Superstructure — columns → beams → slab (per storey)
13. Slab curing  ← HARD WAIT (longest single wait on the programme)
14. Roof / roof slab / roof treatment & waterproofing
15. Brickwork / masonry infill (per storey, follows that storey's slab)
16. Door/window frame fixing (chowkats) — set with masonry, not after plaster
17. Electrical + plumbing + HVAC rough-in (concealed conduits, pipes, boxes)
18. MEP INSPECTION & PRESSURE TEST  ← HARD GATE, no exceptions
19. Internal plaster + external plaster/rendering
20. Waterproofing of wet areas (bath, kitchen, terrace) + flood test
21. Flooring & tiling (floors before walls in wet areas; screed levels final)
22. False ceiling / gypsum / POP
23. Woodwork — doors, shutters, cabinetry, wardrobes
24. Painting (primer → putty → 2 coats finish)
25. Electrical & plumbing second fix (fixtures, switches, sanitaryware)
26. External works — boundary wall, driveway, drainage, landscaping
27. Snagging / punch list → cleaning → testing & commissioning → handover
```

### 1.2 The Four Dependency Types

Not all "A before B" relationships are equal. Classify every link before compressing a programme.

| Type | Meaning | Can it be compressed? | Examples |
|---|---|---|---|
| **Physical** | B is physically impossible until A exists | Never | Can't cast a column without a footing; can't plaster a wall that isn't built |
| **Material/chemical** | B must wait for A to gain strength or cure | Never — this is chemistry, not scheduling | Slab curing, mortar set, waterproofing membrane cure, paint recoat interval |
| **Verification** | B buries A, so A must be inspected first | Only by inspecting faster, never by skipping | MEP rough-in before plaster; reinforcement before pour; DPC before plinth fill |
| **Preferential** | Conventional order, driven by damage-avoidance and trade efficiency | Yes, with deliberate protection measures | Flooring before painting vs. painting before flooring; joinery before or after paint |

**Rule:** when a client or contractor asks to "run these in parallel to save time", identify the dependency type first. Only *preferential* links are negotiable. Compressing a material/chemical link is how slabs deflect and crack; compressing a verification link is how walls get reopened.

### 1.3 Decision Tree — Can Stage B Start?

```
Is Stage A complete?
├── NO → Can B start on a completed *portion* of A? (zone-based / segmented working)
│         ├── YES → Split into zones. Zone 1 A-complete → Zone 1 B starts.
│         │          Requires: clear zone boundaries, no shared curing element,
│         │          no shared prop/formwork system.
│         └── NO  → B waits. Full stop.
└── YES → Has A's minimum curing/strength period elapsed?
          ├── NO → Is B a *loading* activity (adds weight, vibration, drilling)?
          │        ├── YES → WAIT. Non-negotiable. See Section 5.
          │        └── NO  → Non-loading prep may proceed (marking, setting out,
          │                   material staging) but nothing that imposes load.
          └── YES → Has A passed its QC hold point / inspection sign-off?
                    ├── NO → STOP. Inspect. This is the rework gate.
                    └── YES → Will B conceal A permanently?
                              ├── YES → Photograph + as-built record FIRST,
                              │          then proceed.
                              └── NO  → Proceed.
```

---

## Section 2: Stage 1-2 — Site Clearance & Setting Out

### 2.1 Site Clearance

| Activity | Typical duration (small plot ≤ 2250 sqft) | Notes |
|---|---|---|
| Vegetation & topsoil strip (150-300mm) | 1-2 days | Topsoil stockpiled separately for landscaping — do not mix with spoil |
| Demolition of existing structure | 3-10 days | Requires separate authority permission in most Pakistani jurisdictions |
| Debris removal | 1-2 days | Budget by truckloads, not days |
| Site fencing, gate, signage | 1 day | Statutory in DHA/LDA controlled areas |
| Temporary water + electricity connection | 3-15 days (utility lead time) | **Start this in week -4. It is the most common cause of a stalled week 1.** |
| Site office / store / labour shed | 2-3 days | |
| Soil investigation (if not already done) | 3-7 days incl. lab report | **Should precede design, not construction** |

**QC hold point HP-01:** Written confirmation of (a) plot boundary against the authority-approved site plan, (b) benchmark/datum level agreed and physically marked on a permanent object outside the excavation zone, (c) neighbouring structure condition survey photographed (dilapidation survey) before any excavation.

### 2.2 Setting Out

- Establish a **permanent benchmark** (BM) on an immovable object — a boundary wall, a road kerb, a driven pipe in concrete — outside the excavation footprint. Every level on the job derives from this. If the BM is inside the dig, you will lose it in week 2.
- **Batter boards / profile boards** set 1.0-1.5 m clear of the excavation edge, with string lines marking grid lines and wall faces.
- Check diagonals on every rectangle. A 10 m x 12 m rectangle must have equal diagonals of √(10²+12²) = 15.620 m. Tolerance ±10 mm.
- Grid reference: use the same grid IDs as the drawings and the FreeCAD model (A/B/C x 1/2/3). Do not invent site-only naming.

| Setting-out tolerance | Value |
|---|---|
| Overall building position on plot | ±25 mm |
| Grid line spacing | ±10 mm over any bay; ±15 mm cumulative |
| Diagonal / squareness | ±10 mm |
| Level of benchmark transfer | ±5 mm |
| Column starter bar position (from grid) | ±10 mm |

---

## Section 3: Stage 3-4 — Excavation & Earthwork

### 3.1 Foundation Depth Decision Tree

```
What controls foundation depth at this site?
├── Frost line (cold climates, IRC 2021 R403)
│    → Bottom of footing BELOW local frost depth per IRC Table R301.2
│    → Absolute minimum in all cases: 12 in (305 mm) below undisturbed grade
│    → Alternative: Frost-Protected Shallow Foundation (FPSF) per ASCE 32,
│      insulated, 12-16 in depth — only where an engineer has designed it
├── Bearing stratum (most of Pakistan / warm climates)
│    → Excavate to the stratum named in the geotechnical report
│    → Typical residential in firm soil: 1.2-1.8 m (4-6 ft) below NGL
│    → Expansive/black cotton clay: deeper, or under-reamed piles — engineer call
├── Water table
│    → Footing above water table where possible; otherwise dewatering +
│      waterproofing + uplift check by engineer
└── Adjacent structure
     → Never undermine a neighbour's footing. Excavate in a stepped/benched
       profile, or underpin. This is a legal exposure, not just technical.
```

### 3.2 Excavation Data

| Item | Value / rule |
|---|---|
| Minimum footing depth (IRC 2021, R403) | 12 in / 305 mm below undisturbed ground surface, **and** below the frost line per Table R301.2 |
| Typical residential depth, firm soil (Pakistan practice) | 1.2-1.8 m below natural ground level, confirmed by geotech |
| Working space each side of footing | 300-450 mm beyond footing face for formwork + workers |
| Safe unsupported vertical cut, firm cohesive soil | ≤ 1.2 m. Beyond that: batter the sides or shore. |
| Batter slope, loose/sandy soil | 1:1 (45°) or flatter |
| Batter slope, stiff clay | 1:0.25 to 1:0.5 |
| Spoil stockpile setback from trench edge | ≥ 1.0 m, minimum equal to trench depth for deep cuts |
| Over-excavation remedy | **Never backfill loose soil under a footing.** Fill the over-dig with lean concrete (PCC) up to the design underside. |

**Critical rule:** the bottom of an excavation must be **undisturbed natural ground or engineered compacted fill**. Soft spots, roots, old services, or backfilled pits found at formation level get excavated out and replaced with PCC or compacted granular fill — they never get "levelled off".

### 3.3 Trench & Excavation Worker Safety

This is a **life-safety topic in its own right**, not a subset of the depth/batter table above — trench collapse kills residential-site labourers in Pakistan every year, almost always in a cut that "looked stable yesterday." Treat every point below as mandatory, not aspirational.

| Requirement | Rule |
|---|---|
| Shoring trigger | Any trench **≥ 1.2 m deep** that cannot be safely battered (tight plot, adjacent structure, restricted width) **must be shored** — timber sheeting + walings + struts, hydraulic shoring, or a trench box/shield. Batter angle alone (Section 3.2) is not a substitute for shoring where there isn't room to batter. |
| Daily pre-entry inspection | A competent person re-inspects the cut **every single day before anyone enters**, and again after rain, after a nearby vibration source (compactor, passing truck), or after any visible crack/tension crack appears at the crest. Yesterday's stable cut is not evidence about today's cut. |
| No-entry conditions | Do not enter an unshored cut deeper than 1.2 m under any programme pressure. This is the rule most often broken "just to save the shoring hire cost for one day." |
| Spoil and plant surcharge | Spoil stockpiles, site plant, material stacks, and vehicle trafficking are kept **back from the crest by at least the excavation depth** (ties to the ≥1.0 m / equal-to-depth setback in Section 3.2) — a loaded truck or a spoil heap at the edge adds surcharge load exactly where the cut is weakest. |
| Access/egress | A ladder or ramp within 8 m of any worker in a trench ≥1.2 m deep, so nobody has to run along the trench floor to get out. |
| Utility strike precautions | **Before any digging**, obtain as-built service drawings (water, gas, sewer, electrical, telecom) from the relevant utility and the site's own record if previously built on; hand-dig (not machine-dig) trial pits/potholes at any point a service is expected, to expose it before the excavator gets near; mark confirmed services physically on the ground (paint/flags) and keep the marking current as the dig progresses; treat every unidentified buried line as live until proven otherwise — this covers gas strikes (fire/explosion), electrical strikes (electrocution), and water/sewer strikes (undermining the excavation itself). |
| Excavator/plant proximity | Keep tracked plant back from the crest by the same surcharge setback; never let the machine work with one track over the edge to "reach" the far side. |
| Confined-space / gas check | Deep pits and any trench where stagnant water or organic decay is present get an atmosphere check before entry, not an assumption of safety. |

### 3.4 Anti-Termite Treatment (pre-construction, warm climates)

Sequence: applied **after excavation, before PCC** — soil in the trench bottom and sides, then again on the levelled plinth fill before the ground-floor slab, then at the wall-floor junction.
- 3 stages: (1) trench bottom + sides, (2) backfill soil around foundation, (3) plinth fill top surface before slab.
- Must be complete before any concrete covers the treated soil. Once PCC is down, the chance is gone until post-construction drill-and-inject (more expensive, less effective).

### 3.5 Backfill & Compaction

| Parameter | Value |
|---|---|
| Layer thickness (loose) | 150-225 mm max per layer |
| Compaction | Each layer compacted before the next; plate compactor or rammer |
| Target density (granular fill under slab) | ≥ 95% Modified Proctor (engineer to specify) |
| Moisture | At or near optimum moisture content — dry fill will not compact, saturated fill pumps |
| Prohibited fill material | Organic soil, topsoil, construction debris, expansive clay under slabs |

**Do not backfill against a foundation/basement wall until the wall has cured AND, where the design relies on it, the slab or floor that props the wall is in place.** Backfilling early against an unpropped retaining/basement wall is a classic collapse mode.

---

## Section 4: Stage 5-7 — Foundation, Concrete Grades & Reinforcement

### 4.1 Concrete Grade Selection by Structural Role

| Grade | Nominal mix (cement:sand:aggregate) | Characteristic strength f'c / fck | Where used in a house |
|---|---|---|---|
| M7.5 / M10 | 1:4:8 / 1:3:6 | 7.5 / 10 N/mm² | Mass fill, over-dig replacement, non-structural blinding |
| **M15** | **1:2:4** | **15 N/mm²** | **PCC blinding under footings, fence/garden wall footings, mass fill, floor sub-base — NON-STRUCTURAL only** |
| **M20** | **1:1.5:3** | **20 N/mm²** | **The default residential structural grade — footings, plinth beams, columns, beams, suspended slabs, retaining walls** |
| **M25** | **1:1:2** | **25 N/mm²** | **Heavily loaded columns/beams, transfer elements, multi-storey ground-floor columns, rigid pavement/driveway** |
| M30+ | Design mix only | ≥ 30 N/mm² | Design-mix territory — not nominal-mix, not site-batched by eye |

**Rules:**
1. Nominal (volumetric) mixes are acceptable up to **M20-M25 for small residential work** in most codes; anything above must be a **designed mix with trial cubes**.
2. Never substitute grades "up" casually to feel safe — richer concrete shrinks more and cracks more. M25 in a slab designed for M20 buys cracking, not safety.
3. Water-cement ratio governs strength far more than cement quantity. Target **w/c 0.45-0.55** for structural concrete. Site staff adding water at the mixer for workability is the single most common quiet cause of under-strength concrete — use a plasticiser instead.
4. Cover to reinforcement (typical residential, non-aggressive exposure): footings **50 mm** (cast against blinding) or **75 mm** (cast against earth), columns **40 mm**, beams **25-40 mm**, slabs **20-25 mm**. Verify against the stamped structural drawing — the drawing wins.

### 4.2 Foundation Type vs. Sequence Implications

| Foundation type | Sequence note | Typical residential use |
|---|---|---|
| Isolated pad footings + columns | Fastest; each pad independent; allows zoned working | RC frame house — the Pakistani default |
| Strip footing | Continuous pour; single sequence chain, less zoning freedom | Load-bearing masonry house |
| Raft / mat | Single large pour — needs pour planning, construction joints, possibly a concrete pump | Weak soil, high water table, basement |
| Pile + pile cap | Adds 1-3 weeks and a specialist subcontractor at the front of the programme | Very weak soil, expansive clay |

### 4.3 Foundation Sequence Detail

```
Excavate to formation level
   → Inspect formation (HP-02: bearing stratum confirmed, no soft spots)
   → Anti-termite treatment stage 1
   → PCC blinding M15, 75-100 mm thick, cured 24 h
   → Mark footing outline on the blinding
   → Place bottom reinforcement mesh on cover blocks (never on brick bats or steel chairs
     touching the soil)
   → Place column starter bars / cage, tied, plumbed, braced
   → Formwork to footing edges, oiled, braced, checked for line and level
   → HP-03: PRE-POUR INSPECTION (see Section 11.1) ← sign-off required
   → Pour, vibrate (do not over-vibrate — segregation), finish
   → Start curing within 2-4 h of finishing (or as soon as the surface takes
     no damage from water)
```

### 4.4 Reinforcement Placement Rules That Affect Sequence

- **Cover blocks are structural.** Concrete cover is the only thing protecting the steel. Use manufactured cover blocks of the correct thickness, not stone chips.
- **Lap lengths:** typically 50 x bar diameter for tension laps in residential work (confirm against the structural drawing; codes vary). Laps must be staggered — no more than 50% of bars lapped at one section.
- **Column starter bars must be plumbed and braced before the pour**, not straightened afterwards. Bending a cast-in bar to line is a defect, not a fix.
- **Never cut or reposition reinforcement on site to suit a service penetration.** That is an engineer's decision. This is the number-one field improvisation that destroys design capacity.

---

## Section 5: Curing — The Wait Times That Are Physics

Concrete gains strength through hydration, and hydration needs water and temperature. Curing is not "letting it dry" — drying is the failure mode. **Every schedule-compression conversation collides with this section, and this section always wins.**

### 5.1 Minimum Curing Periods

| Cement / condition | Minimum curing period | Source |
|---|---|---|
| Ordinary Portland Cement (OPC), normal conditions | **7 days** | IS 456:2000, Cl. 13.5.1 |
| Blended cement (PPC / PSC / fly ash / slag) | **10 days** | IS 456:2000, Cl. 13.5.1 |
| Hot / dry / arid conditions, OPC | **10-14 days** | IS 456:2000, Cl. 13.5.1 (extended-condition provision) |
| Hot / dry / arid conditions, blended cement | **14 days** | IS 456:2000, Cl. 13.5.1 |
| General duration + condition requirement | Duration governed by temperature and moisture conditions maintained | ACI 318-19, Ch. 26 (curing/construction requirements, §26.5.3-26.5.5) |
| Early curing termination | Curing may stop once concrete reaches **70-80% of specified fck** — verified by cube/cylinder test, **not by opinion** | IS 456:2000, Cl. 13.5.1 |
| Full design strength (loading reference) | **28 days** | ACI 318-19 / general practice |

**Critical clarification, because it is misunderstood on every site:**
- *Curing period* (7-14 days) = how long you keep it wet.
- *Formwork striking* (see 5.2) = when you take the shutters off.
- *Full design strength* (28 days) = when it is allowed to take full design load.

These are three different clocks. Removing formwork at 7 days does not mean the slab is finished curing, and finishing curing at 14 days does not mean the slab can take full load at 14 days.

### 5.2 Formwork Striking / Deshuttering Times (IS 456:2000)

| Formwork element | Minimum time before striking |
|---|---|
| Vertical formwork to columns, walls, beam sides | **16-24 hours** |
| Slab soffit forms (props left in place) | **3 days** |
| Beam soffit forms (props left in place) | **7 days** (props stay) |
| Props to slabs, span ≤ 4.5 m | **7 days** |
| Props to slabs, span > 4.5 m | **14 days** |
| Props to beams & arches, span ≤ 6 m | **14 days** |
| Props to beams & arches, span > 6 m | **21 days** |

**Do not confuse the slab soffit row with the beam soffit row.** IS 456:2000 Table 12A gives slab-soffit-with-props-left-in-place as 3 days but beam-soffit-with-props-left-in-place as **7 days** — a beam carries load through a much stiffer, more concentrated span-to-depth relationship than a slab, so it needs longer before even the propped soffit can be struck. Treating a beam like a slab and pulling its soffit at 3 days is exactly the kind of numeric mix-up this table exists to prevent.

**Rules:**
1. These are **minimums for OPC in normal temperature**. Blended cements and cold weather extend them. Hot weather does *not* license shortening them without cube evidence.
2. **Back-propping:** where props are removed early on a multi-storey pour cycle, back-props must be installed to spread construction load through 2-3 floors below. This is an engineered arrangement, not a site improvisation.
3. **The controlling factor is measured strength, not elapsed days.** Where the programme depends on early striking, take extra cubes cured alongside the element and strike on test results with the engineer's written approval.
4. Never strike props under a slab that is currently carrying stacked material (bricks, tiles, sand). Construction load frequently exceeds design live load.

### 5.3 Curing Methods & Suitability

| Method | Suitable for | Notes |
|---|---|---|
| Ponding (water retained by mud/sand bunds) | Horizontal slabs, footings, plinths | Most effective for slabs; needs a watertight bund and continuous water |
| Wet hessian / jute covering, kept damp | Columns, beams, walls, slabs | Must never be allowed to dry — dry hessian actively wicks water OUT |
| Continuous sprinkling / soaker hose | Slabs, walls | Labour-dependent; fails on Sundays and holidays — the most common curing failure window |
| Polythene sheeting (moisture retention) | Slabs, columns | Seal edges; secondary to wet curing in hot climates |
| Curing compound (membrane-forming) | Large slabs, remote sites, water-scarce sites | **Do not use where a bonded topping, screed, tile adhesive, or waterproofing membrane will follow** — the compound is a bond breaker. Must be removed by mechanical abrasion if a bond is needed. |
| Formwork left in place | Columns, beams | Only counts as curing while forms are tight and the surface stays damp |

### 5.4 Hot-Weather Concreting (directly relevant to Pakistani summers)

| Control | Guidance |
|---|---|
| Concrete placement temperature | Keep as low as practical; use chilled mixing water, shade aggregate stockpiles, ice in extreme cases |
| Pour timing | Early morning or night pours in peak summer (Lahore/Karachi May-August) |
| Time from mixing to placing | Minimise; hot concrete stiffens fast — plan the pour route before starting |
| Curing start | **Immediately** after finishing — plastic shrinkage cracking happens in the first hours, before the concrete is even hard |
| Evaporation control | Wind breaks, fog spray, evaporation retarder, immediate covering |
| Curing duration | Extend to 10-14 days per IS 456 Cl. 13.5.1 hot/arid provision |

### 5.5 Curing of Non-Concrete Elements

| Element | Wait before next stage |
|---|---|
| Brick masonry mortar | Cure 7 days (sprinkle 2-3x/day); do not plaster over green masonry |
| Masonry wall before plaster | **Minimum 7 days after the last course** — allows shrinkage/settlement; 14 days preferable |
| Internal plaster before painting | **7-21 days** to dry out; moisture meter or a taped-plastic-patch test before priming |
| Cement screed before tiling | 7 days cure + drying; thick screeds need longer |
| Waterproofing membrane before screed/tile | Per manufacturer, typically 24-72 h + a 24-48 h flood test |
| Paint recoat interval | Per manufacturer, typically 4-6 h (emulsion) / 16-24 h (enamel) |

---

## Section 6: Stage 9-11 — Plinth Beam, DPC & Plinth Filling

### 6.1 Plinth Height

| Requirement | Value | Source |
|---|---|---|
| Minimum plinth height | **2 ft / 610 mm** above surrounding ground level | KP Model Building Bye-Laws 2017; consistent across DHA Bye-Laws 2020, LDA Building & Zoning Regulations 2019, Islamabad Residential Sectors Zoning Regulation 1993 |
| Maximum plinth height | **4.5 ft / 1372 mm** | Same bye-laws |
| Practical driver | Must clear the crown of the adjacent road and the design flood/monsoon runoff level | Site-specific — check the actual road level, not the drawing |

Always verify the **specific authority's current bye-law** for the plot (LDA vs. CDA vs. DHA vs. TMA differ), and take the road crown level as a measured site fact.

### 6.2 Damp-Proof Course (DPC)

| Requirement | Value | Source |
|---|---|---|
| DPC height above finished external ground level | **Minimum 150 mm (approx. 6 in)** | UK Building Regs Approved Document C, Sec. 5.5; NHBC Standards 5.1.19 |
| Cavity wall — cavity extension below DPC | **≥ 225 mm below DPC**, or a cavity tray must be used | Approved Doc C / NHBC 5.1.19 |
| Weep holes (cavity wall / cavity tray) | **Every 900 mm** | NHBC 5.1.19 |
| Typical Pakistani residential DPC | 40-50 mm dense cement concrete (1:1.5:3) with integral waterproofing compound, or 2 layers of polythene/bitumen membrane, full wall width | Common practice — specify explicitly |
| Continuity | DPC must be **continuous and lapped** with the floor DPM (damp-proof membrane), and lapped at every junction | |

**Sequencing rules for DPC — these are where houses get permanent rising damp:**
1. DPC goes in **before** plinth filling and **before** any masonry above plinth. Retrofit is not realistic.
2. DPC must **lap with the ground-floor DPM** so there is no path from soil to wall. A DPC and a DPM that don't touch are two half-solutions.
3. **Never bridge the DPC.** Bridging happens when: external plaster runs down past the DPC to the ground; a paved driveway or planter is later built above the DPC line; mortar droppings fill the cavity at DPC level. Plaster stop-bead below the DPC line must be detailed *now*, not discovered later.
4. Finished external ground level (including any future paving build-up) must be at least 150 mm below the DPC. **Ask what the final paving/landscape level will be before setting the DPC** — landscaping added a year later is the classic bridging event.

### 6.3 Plinth Filling Sequence

```
Plinth beam cast + cured (min 7 days)
  → DPC laid at plinth beam top / first course level
  → Backfill inside plinth in 150-225 mm compacted layers
  → Anti-termite treatment stage 3 on top of fill
  → Granular sub-base (crushed stone / brick ballast), compacted
  → DPM (polythene sheet, min 500 gauge / 0.125 mm, lapped 150 mm and taped,
    turned up at edges to lap the DPC)
  → PCC / sub-floor slab
  → HP-05 sign-off before the ground floor slab
```

---

## Section 7: Stage 12-14 — Superstructure & Roof

### 7.1 Per-Storey Cycle (RC frame — the standard Pakistani residential system)

```
Column starter bars exposed and cleaned (laitance removed, roughened)
 → Column reinforcement cage tied, spliced, plumbed
 → HP-06 column steel inspection (bar count, dia, tie spacing, cover, plumb)
 → Column formwork, plumbed, braced, tight at base to prevent grout loss
 → Column pour (in lifts if tall — max free-fall 1.5 m or use a tremie/chute)
 → Strike column forms 16-24 h → cure columns 7 days
 → Beam & slab formwork erected, propped, cambered where specified, levelled
 → Beam reinforcement, then slab bottom mesh, chairs, top mesh
 → Conduits and sleeves cast INTO the slab now (see 7.3)
 → HP-07 PRE-POUR INSPECTION — the single most important checkpoint on the job
 → Slab pour, vibrated, screeded, floated
 → Curing starts within hours; continues 7-14 days
 → Strike slab soffit 3 days (props stay); strike beam soffit 7 days (props
   stay) — the beam soffit is NOT the same clock as the slab soffit
 → Props out at 7 days (slab ≤4.5 m span) or 14 days (slab >4.5 m span);
   beam props stay to 14 days (≤6 m span) or 21 days (>6 m span)
 → Next storey columns begin only when the engineer confirms the slab can
   take construction load
```

### 7.2 Realistic Storey Cycle Times (small residential, conventional timber/steel formwork)

| Activity | Duration (small house, ~1000-1500 sqft footprint) |
|---|---|
| Column steel + formwork + pour | 3-5 days |
| Column cure + strike | 1-2 days (forms), curing continues |
| Beam/slab formwork erection | 4-7 days |
| Slab reinforcement + MEP sleeves/conduits | 3-5 days |
| Pre-pour inspection + rectification | 1 day |
| Slab pour | 1 day (single pour strongly preferred) |
| Curing before next storey columns | 7-14 days |
| **Total per storey** | **18-28 days (≈ 3-4 weeks)** |

### 7.3 Cast-In Items — The Non-Negotiable "Now or Never" List

Everything on this list must be placed **before the pour**. Retrofitting any of it means core-drilling or chasing structural concrete, which is a defect requiring engineer approval.

- Electrical conduits crossing the slab; ceiling light/fan boxes; fan hooks
- Plumbing sleeves through beams and slabs (waste stacks, vents, rainwater outlets)
- Drainage outlets, roof/terrace floor traps set to falls
- HVAC / duct sleeves; refrigerant and drain pipe sleeves for split ACs
- Lift/hoist pockets, staircase nosing inserts
- Structural anchors, base plates, holding-down bolts
- Waterproofing puddle flanges at wet-area penetrations
- Earthing/lightning-protection conductors and bonds
- Solar mount inserts / water-tank support plinth starter bars

**Rule: never drill or chase a structural beam or column afterwards.** Chasing a masonry infill wall is bad practice; chasing a structural element is a structural modification.

### 7.4 Roof & Waterproofing Sequence

```
Roof slab cast + cured
 → Surface prepared (clean, laitance removed, cracks routed and filled)
 → Screed to falls — minimum 1:100 (1%), 1:80 preferred, toward outlets
 → Outlets and puddle flanges set to the LOW points (check with a hose test
   before waterproofing, not after)
 → Waterproofing membrane, turned up 150-300 mm at all parapets and
   penetrations, terminated into a chase or under a flashing
 → FLOOD TEST 24-48 h — mandatory hold point HP-11
 → Protection screed / tile / insulation board
 → Parapet coping with drip detail
```

**Sequencing trap:** waterproofing applied *before* the parapet wall is built means the upturn is missing at the most important joint. Build the parapet, then waterproof, then tile.

---

## Section 8: Stage 15-16 — Masonry Infill & Frames

### 8.1 Mortar Mix Selection

| Mortar ratio (cement:sand) | Use case |
|---|---|
| **1:3** | Generally **avoided** — high shrinkage for minimal strength gain; only for specific repair/structural grouting where specified |
| **1:4** | **9-inch (230 mm) load-bearing walls; multi-storey walls; earthquake-zone masonry; ground-floor walls needing higher strength**; below-DPC masonry |
| **1:5** | Intermediate — 9-inch walls in moderate conditions |
| **1:6** | **Medium-strength walls up to 3 storeys**; standard 4.5-inch (115 mm) partition walls and non-load-bearing infill above ground floor |
| **1:8** | Very lean — internal non-load-bearing partitions only, low-load conditions |

Pakistan seismic context: **BCP 2007 Seismic Provisions** classify the country into seismic zones; masonry in higher zones requires richer mortar, confining elements (RC bands/columns), and reinforcement detailing. Zone-specific requirements must come from the stamped structural drawing.

### 8.2 Masonry Rules That Are Sequence-Critical

| Rule | Reason |
|---|---|
| Wet the bricks before laying (soak, don't dunk-and-lay) | Dry bricks suck water out of the mortar and starve hydration → weak joints |
| Max lift height per day: **1.0-1.2 m (about 12-14 courses)** | Green mortar in lower courses squeezes out and the wall bulges/leans |
| Mortar joint thickness: **10-12 mm**, uniform | Thick joints = weak wall; the joints are the weak link, not the brick |
| Rake joints 10-15 mm deep when plaster follows | Provides mechanical key for plaster. Do it while mortar is green, not after it cures. |
| Cure masonry 7 days | Same chemistry as concrete |
| Leave a gap or use a slip joint at the top of infill under the beam soffit | Slab deflection onto rigid infill cracks the wall — pack after the slab has taken its deflection, typically with a non-shrink or a soft joint per the design |
| Provide RC lintels over ALL openings, min bearing 150-230 mm each side | |
| **Set door/window frames (chowkats) with the masonry, plumbed and braced** | Fitting frames after plaster means either chasing back the finished plaster or an ugly gap — and the frame's holdfasts have nowhere to go |

### 8.3 Wall Chasing Rules

| Element | Chasing allowed? |
|---|---|
| RC column, beam, slab | **NO.** Never. Route around it or use a surface conduit. |
| 9-inch (230 mm) masonry wall | Vertical chases yes; depth ≤ 1/3 wall thickness. Horizontal chases: avoid; if unavoidable, ≤ 1/6 thickness, short runs, never near a lintel bearing |
| 4.5-inch (115 mm) partition | Vertical only, shallow; a horizontal chase in a 4.5-inch wall effectively cuts it in half |
| Near an opening / lintel bearing | No chases within 300 mm of a jamb or under a lintel bearing |
| Back-to-back chases (same location both faces) | **Never** — this creates a full-depth cut |

---

## Section 9: Stage 17-19 — MEP Rough-In & Plaster (THE Critical Gate)

### 9.1 Why This Is The Number One Rework Cause

Across every contractor and industry source reviewed, the single most-cited sequencing failure in residential construction is:

> **Plastering / drywalling over MEP rough-in that has not been fully installed AND inspected.**

The mechanism is simple and always the same: plaster is a finished substrate. Once cured, opening it means breaking it out, re-chasing, re-plastering, waiting for it to dry again, and re-painting — and the patch is visible under raking light forever. The pressure to "just close the wall so the plasterers can keep moving" is exactly the pressure that produces the reopening.

### 9.2 The MEP Gate — Mandatory Checklist Before Any Plaster

Nothing gets plastered until **every** line below is signed off:

**Electrical**
- [ ] All conduits installed, continuous, no crushed or kinked sections
- [ ] Draw wires present in every conduit (test-pull each one — a blocked conduit found after plaster is a wall reopened)
- [ ] All back boxes fixed, level, plumb, set to the **finished** plaster/tile line (not the blockwork line)
- [ ] Distribution board position/size final; sub-main routes complete
- [ ] Earthing conductors and bonds in place
- [ ] Layout checked against the **furniture plan** — sockets behind a fixed wardrobe or a headboard are a design failure discovered too late
- [ ] Continuity test on installed cabling where cable is pulled at rough-in stage
- [ ] Photographic as-built record of every wall, with a tape/scale visible

**Plumbing**
- [ ] All supply pipework installed, jointed, fixed
- [ ] All drainage installed at correct falls (min 1:40 for 100 mm soil, 1:40-1:80 as designed for wastes)
- [ ] **Pressure test on supply lines** held per spec (typically 1.5x working pressure, 1-2 h, no drop) — signed record
- [ ] **Water/air test on drainage** — signed record
- [ ] Fixture rough-in dimensions verified against actual sanitaryware model numbers (not generic centres)
- [ ] Shower valve depth set for the final tile + adhesive thickness
- [ ] Concealed cistern frames fixed and levelled
- [ ] Photographic as-built record

**HVAC / other**
- [ ] AC refrigerant/drain pipe sleeves and routes complete, drain to fall
- [ ] Data/TV/intercom/CCTV conduits and boxes complete
- [ ] Any concealed structural fixings for wall-hung items (TV brackets, wall-hung WC, grab rails, heavy mirrors) installed as noggins/plates — **these are always forgotten and always require reopening**

**Sign-off**
- [ ] Client / architect / engineer walkthrough with the drawings in hand
- [ ] Photographic record complete and filed, indexed by room and wall
- [ ] Written HP-08 sign-off before the first plaster is mixed

### 9.3 Plaster Sequence

| Step | Detail |
|---|---|
| Substrate prep | Clean, rake joints, remove dust/oil, wet the wall; chicken-wire mesh over every chase and at every dissimilar-material junction (concrete-to-brick) |
| Level pegs / dots and screeds | Establish plumb and thickness before starting; ensures uniform thickness |
| Internal plaster thickness | 12-15 mm (single coat on brick); 6-10 mm on RC surfaces |
| External plaster thickness | 15-20 mm, usually two coats (rough + finish) |
| Mortar for plaster | 1:4 (external, wet areas), 1:5 or 1:6 (internal) |
| Ceiling plaster | Before wall plaster |
| Order within a room | Ceiling → walls → floor screed |
| Curing | 7 days minimum, keep damp |
| Drying before paint | 7-21 days; test for moisture before priming |

**Order rule:** external plaster generally follows the roof being watertight, and internal plaster follows the building being weather-tight (openings glazed or temporarily sealed). Plastering into a building that still takes rain is throwing money at a wall.

---

## Section 10: Stage 20-27 — Wet Areas, Finishes, Second Fix & Handover

The structure is forgiving; the finishes are not. From here on, every dependency is either a *drying* wait or a *damage-avoidance* order, and every mistake is visible in the handover photographs.

### 10.1 Wet-Area Waterproofing (bathrooms, kitchens, terraces, laundry)

```
Plaster complete and cured in the wet room
 → Floor screed laid to falls FIRST (waterproofing follows the falls,
   it does not create them)
 → Floor trap / gully set at the LOW point, rim at screed level
 → Substrate primed per the membrane manufacturer
 → Membrane applied: floor + upturns + all penetrations
 → Reinforcing tape / fillet at EVERY floor-wall junction and internal corner
 → Membrane cure per manufacturer (typically 24-72 h)
 → FLOOD TEST 24-48 h  ← HP-11: water 25 mm above the highest floor point,
   trap plugged, inspect the ceiling below AND the far face of every adjacent wall
 → Photograph the test with the water level visible
 → Protection screed / tile bedding
 → Tiling
```

| Waterproofing upturn | Height |
|---|---|
| General wet-room wall upturn | **150-300 mm** above finished floor level (FFL) |
| Shower enclosure walls | **1800 mm** above FFL (full wet zone), or full height to ceiling |
| Behind a bath | **150 mm above the bath rim** |
| Kitchen sink / laundry splash zone | **300 mm** above the counter |
| Around a floor trap | Membrane dressed **into** the puddle flange, never stopped at it |
| Door threshold | Membrane returns **150 mm beyond** the opening both sides; hob/upstand or a fall-back gradient at the threshold |
| Pipe penetrations | Individually collared and sealed — penetrations are where most failed bathrooms leaked |

| Falls in wet areas | Value |
|---|---|
| Bathroom floor to trap | **1:80 to 1:100** (min 1%) |
| Shower area to waste | **1:50 to 1:60** (steeper, contained zone) |
| Terrace / balcony to outlet | **1:80 minimum**, 1:60 preferred |
| External FFL vs adjacent internal FFL | External **≥ 25 mm lower** (50 mm preferred), plus a threshold upstand |

**Wet-area sequencing traps**
1. **Membrane before the falls are formed** — the membrane then holds water in every flat spot permanently. Falls first, membrane second.
2. **Flood test skipped "because it looks fine"** — a membrane defect is invisible dry. HP-11 costs 48 hours; a failure costs a two-week strip-out plus the ceiling below.
3. **Drilling through a tanked surface at second fix** (shower screen, grab rail, heavy mirror) — every such fixing must be sealed, and heavy items should land on noggins/plates installed back at MEP rough-in (HP-08).
4. **Wall-hung WC frames fitted late**, breaking the upturn. Concealed frames are rough-in items, not second-fix items.

### 10.2 The Finished Floor Level (FFL) Datum — set once, before any screed

Before the first screed or tile anywhere in the house, publish a single **FFL datum** for the whole building and mark it on every wall as a level line — traditionally the **"1 metre line"**, 1000 mm above FFL, because a mark at floor level gets buried by the screed.

Every downstream trade works off that line: screed thickness, tile setting-out, door-frame cut-down, skirting, socket heights, shower-valve depth, thresholds, kitchen counter height.

| Build-up below FFL | Typical thickness |
|---|---|
| Bonded screed on slab | 25-40 mm |
| Unbonded screed (on DPM/membrane) | ≥ 50 mm |
| Floating screed (over insulation) | 65-75 mm |
| Thin-bed tile adhesive | 3-6 mm |
| Thick-bed / traditional mortar bedding | 20-40 mm |
| Ceramic / porcelain tile | 8-12 mm |
| Natural stone (marble / granite slab) | 18-25 mm |
| Wood / laminate + underlay | 12-20 mm |

**Rule:** rooms with different finishes need **different screed levels** so their *finished* levels agree at the threshold. A marble room and a laminate room only meet flush if someone did that arithmetic before the screed went down — and nobody ever does it afterwards.

| Screed drying before the finish | Rule of thumb |
|---|---|
| Cement:sand screed drying rate | **~1 mm/day for the first 50 mm**, slower beyond |
| 50 mm screed before vinyl / wood / any impermeable finish | ~50+ days in good drying conditions |
| 50 mm screed before ceramic tile (permeable adhesive) | 7-14 days cure commonly accepted |
| Acceptance test | Hygrometer RH ≤ 75% (≤ 65% for timber), or an overnight taped-plastic-sheet test |

Tile can go down far earlier than timber. Confusing the two is why wood floors cup and lift six months after handover.

### 10.3 Tiling Order — Decision Tree

```
Which goes first, wall tile or floor tile?
├── WET ROOM with a tiled skirting / cove detail
│    → FLOOR first, walls tiled down onto it (protects the cove, hides the joint)
├── WET ROOM with wall tile running to the floor
│    → WALLS first, started one tile-height + joint above FFL on a batten;
│      floor tiled last and butted up — protects the floor from droppings and
│      lets the floor tile hide the cut
├── DRY ROOM with tiled or timber skirting
│    → Floor first, skirting last
└── Behind fixed items (bath, shower tray, vanity, kitchen units)
     → Tile BEHIND them before installation. Tiling up to a fitted bath is a
       leak path and a permanent resale complaint.
```

| Tiling rule | Value |
|---|---|
| Setting-out origin | Start from the **most visible line** (door-facing wall / room centre), never a corner — push cuts to hidden edges |
| Minimum cut-tile width | ≥ **half a tile**; if the layout forces a sliver, shift the whole grid |
| Joint width, ceramic wall tile | 2-3 mm |
| Joint width, porcelain floor tile | 3-5 mm |
| Movement joint spacing, internal floor | Every **8-10 m**, and at every room-to-room threshold |
| Movement joint spacing, external / sun-exposed | Every **4-5 m**, and over every structural joint |
| Perimeter joint | **Always** — tile is never hard-butted to a wall; the joint hides under the skirting |
| Hollow-tile acceptance | Tap-test every tile; **zero** hollow tiles in traffic areas (HP-12) |
| Grouting | ≥ 24 h after tiling; wet areas use additive-modified cementitious grout, epoxy in showers |
| Silicone (not grout) | At every **change of plane** — floor-to-wall, internal corners, around sanitaryware |

### 10.4 The Finishes Order — the one genuinely negotiable sequence

Painting, flooring and joinery form a *preferential* dependency triangle (Section 1.2). Both accepted orders work; choosing one deliberately and holding it is what matters.

| Order | Sequence | Advantages | Risks | Best for |
|---|---|---|---|---|
| **A — Floor last** | Plaster → paint 1st coat → joinery → flooring → paint final coat | Floor never takes paint splatter or trolley damage; final coat covers all making-good | Needs a second painting mobilisation; floor still exposed during second fix | High-value floors (marble, timber) |
| **B — Floor first** | Plaster → flooring → joinery → paint | Single painting mobilisation; skirting and doors scribe to a real floor | Floor must stay sheeted and protected for weeks; high damage risk | Tiled floors, compressed programmes |

**Non-negotiable inside either order:**
- **Door leaves are hung after the floor finish is down** (or after the exact build-up is confirmed in writing) — undercut clearance depends on it: typically 8-12 mm over a hard floor, more over carpet.
- **Skirting after the floor**, always, and after the wall's final making-good.
- **Kitchen and wardrobe carcasses after the floor** in wet-prone rooms — appliances get replaced, floors do not.
- **The final paint coat is the last wet trade in the room**, after every making-good from second fix.

### 10.5 Painting

| Step | Rule |
|---|---|
| Substrate moisture before primer | Plaster dry-out **7-21 days**; verify with a moisture meter or taped-sheet test, not by touch |
| Alkalinity | New cement plaster is strongly alkaline — use an **alkali-resistant primer** or the finish burns and discolours |
| System, internal | Primer → 2 coats putty (sanded between) → sealer/primer → 2 coats emulsion |
| System, external | Alkali-resistant primer → 2 coats exterior weatherproof emulsion; **no interior putty externally** |
| Recoat interval, emulsion | **4-6 h** (per manufacturer) |
| Recoat interval, enamel / oil-based | **16-24 h** |
| Inspection method | **Raking light** at HP-13 — hold a torch flat against the wall; defects invisible under flat light are obvious under grazing light |
| Order within a room | Ceiling → walls → woodwork/metalwork → trim |
| Ambient limits | Never onto a sun-hot wall face, in rain, or below the manufacturer's minimum temperature |

**Sequencing trap:** painting before the plaster has dried (Mistake #12, Section 12) produces peeling, blistering, efflorescence and alkali burn — all of which come back through any coat painted over them.

### 10.6 Second Fix (MEP finishing)

Second fix follows painting, or is interleaved with it — the switch plate goes on after the wall behind it is painted, not before.

```
Electrical second fix                       Plumbing second fix
──────────────────────                      ─────────────────────
Pull / terminate cabling                    Install sanitaryware (WC, basin, bath, tray)
Fit switches, sockets, faceplates            Fit taps, mixers, shower sets
Fit light fittings, fans                     Connect traps and wastes
Fit and label every DB circuit                Fill, vent and flush the system
Test: continuity, insulation resistance,     Test: every outlet, every drain, every
  polarity, earth loop impedance, RCD trip     overflow; check every joint for weeping
Energise                                     Commission geyser / heater / pump
```

| Second-fix rule | Reason |
|---|---|
| Sanitaryware only after wall and floor tiling is grouted and cured | Fitting first forces tiling *around* it — a leak path and a visible bodge |
| Silicone sealing is the **last** operation in a wet room | Anything done after it damages it |
| Circuit labelling + as-built DB schedule are deliverables, not a courtesy | Every future electrician depends on them |
| Test **every** circuit and **every** outlet, not a sample | HP-14 — a snag the client finds first is a credibility loss, not just a defect |

### 10.7 External Works

Runs parallel to internal finishes from the weather-tight milestone onward — but these items sit on the *internal* critical path and are routinely missed:

| Item | Constraint |
|---|---|
| Final external ground / paving level | Must not bridge the DPC (Section 6.2) — **≥ 150 mm below DPC after all paving and landscaping build-up** |
| Surface drainage falls | Slope **away** from the building, typically 1:40 to 1:60 for the first 1.5-2 m |
| Boundary wall foundation | Independent of the house foundation — never tie an unengineered boundary wall into the building structure |
| Driveway slab | M25, jointed; schedule **after** heavy material deliveries finish or it cracks under a loaded truck |
| Septic tank / sewer connection | Authority approval and invert levels confirmed **before** internal drainage is buried |
| Underground water tank | Water-tightness tested before backfilling around it |
| Rainwater downpipe discharge | Must reach a drain, channel or soakaway — never the base of the wall |

### 10.8 Commissioning, Snagging & Handover

```
Building complete
 → CONTRACTOR's own snag list first (never hand a raw building to the client)
 → Rectification
 → Builders' clean, then final clean
 → Client / architect snagging inspection → punch list issued in writing,
   numbered, photographed, referenced by room
 → Rectification + re-inspection of EVERY item, closed one by one
 → Commissioning: electrical tests, water flush and test, geyser, pumps,
   every door and window operated, locks keyed
 → Handover pack issued  ← HP-15
 → Defects liability period begins
```

**Handover pack — minimum contents**

| Item | Why it matters |
|---|---|
| As-built drawings (architectural / structural / electrical / plumbing) | Every future repair depends on them |
| **The concealed-services photo record** (Section 9.2 / HP-08) | The single most valuable document in the pack |
| DB schedule and circuit labelling record | |
| Test certificates: concrete cubes, pressure tests, flood tests, electrical tests | Proof of quality, and the evidence base in any later dispute |
| Product warranties (waterproofing, paint, tiles, sanitaryware, appliances) | Many are void without registration inside a fixed window |
| O&M instructions for geyser, pumps, filters, any automation | |
| Maintenance schedule (roof waterproofing inspection, gutter clearing, silicone renewal, repaint cycle) | |
| Meter readings, keys register, authority completion certificate | |

| Post-handover milestone | Typical period |
|---|---|
| Defects liability / maintenance period | **6-12 months** from handover (per contract) |
| First-monsoon / first-winter inspection | Book it explicitly — roof and drainage are only truly tested by real weather |
| Shrinkage-crack making-good | Deliberately deferred to the end of the defects period; doing it at month 1 means doing it twice |
| Retention release | Typically 50% at handover, 50% at end of the defects period |

**Sequencing trap:** handing over with the punch list merely *issued* rather than *closed*. Once the client occupies, every open item becomes a negotiation, and the contractor has lost the uninterrupted access needed to fix it.

---

## Section 11: Quality-Control Hold Points

A **hold point (HP)** stops work until signed off. A **witness point (WP)** requires notification but work may proceed if the inspector doesn't attend. On a small residential job, treat everything below as a hold point — the cost of a 30-minute inspection is nothing against the cost of the corresponding rework.

### 11.1 Full Hold-Point Register

| ID | Stage | What is checked | Who signs | Cost of missing it |
|---|---|---|---|---|
| HP-01 | Setting out | Boundary vs. approved plan, benchmark, diagonals, neighbour dilapidation survey | Architect + surveyor | Building in the setback → demolition order |
| HP-02 | Excavation formation | Depth, bearing stratum matches geotech, no soft spots, no water, sides stable | Structural engineer | Differential settlement, cracked house |
| HP-03 | Pre-pour: foundation | Bar dia/count/spacing, laps, cover blocks, starter bars plumb, formwork line/level/tight, no debris in forms | Structural engineer | Under-strength or unbuildable foundation |
| HP-04 | Post-pour: foundation | Cube samples taken and labelled, curing started, no honeycombing | Site engineer | No evidence of strength; unprovable concrete |
| HP-05 | Plinth/DPC | DPC height ≥150 mm above final external GL, continuous, lapped to DPM, not bridged; plinth height within bye-law | Architect | Rising damp for the life of the building |
| HP-06 | Column steel | Cage, ties, spacing (reduced spacing at ends), cover, plumb, splice locations | Structural engineer | Column failure mode in an earthquake |
| HP-07 | Pre-pour: slab/beam | Reinforcement (bottom + top mesh, chairs, extra bars at openings), cover, **all cast-in items present**, props/formwork adequacy, camber, pour route planned | Structural engineer | The most expensive inspection to skip — everything is permanently buried |
| HP-08 | **MEP rough-in before plaster** | Full checklist §9.2, pressure tests, photo record | Architect + MEP + client | **The #1 rework event** |
| HP-09 | Masonry | Plumb (±10 mm/storey), line, joint thickness, mortar mix, lintels, curing | Site engineer | Bulging walls, cracked plaster |
| HP-10 | Plaster | Thickness, plumb, mesh over chases and junctions, hollow-sounding areas tapped, corners square | Architect | Wavy walls; visible after paint, unfixable cheaply |
| HP-11 | Waterproofing | Continuity, upturns, penetrations, **24-48 h flood test** | Architect + specialist | Leaks into the storey below after handover |
| HP-12 | Tiling/screed | Levels, falls to drains, no hollow tiles (tap test), joint alignment, threshold levels | Architect | Ponding water in bathrooms |
| HP-13 | Pre-paint | Surface moisture, putty finish under raking light, all making-good complete | Architect | Peeling paint / visible defects |
| HP-14 | Second fix & commissioning | Every circuit tested, earth loop, RCD trip test, every tap/drain run, every door swing | Engineer + client | Snag list explosion at handover |
| HP-15 | Handover | Punch list closed, as-builts, warranties, O&M, meter readings, keys | Client | Disputes |

### 11.2 Testing Register (residential minimum)

| Test | When | Acceptance |
|---|---|---|
| Concrete cube test (set of 6 per pour: 3 @ 7 days, 3 @ 28 days) | Every structural pour | 7-day ≈ 65-70% of fck; 28-day ≥ fck per the code's acceptance criteria |
| Slump test | Every batch/truck | Within specified range (typically 75-125 mm for reinforced residential work) |
| Steel test certificates | On delivery | Mill certificate matching grade specified |
| Brick compressive strength + water absorption | On delivery, per batch | Per specification |
| Soil compaction (field density) | Each fill layer / at completion of fill | ≥ 95% Modified Proctor or as specified |
| Plumbing pressure test | Before plaster (HP-08) | No pressure drop over the hold period |
| Drainage water/air test | Before plaster + before handover | No leakage |
| Waterproofing flood test | Before protection screed (HP-11) | No leak after 24-48 h |
| Electrical: insulation resistance, continuity, earth loop, RCD | Second fix, before handover | Per the applicable wiring regulation |

**Independent verification of cube tests — don't skip this:** "cubes taken" is not the same thing as "strength proven." The cube-testing chain has to be independent of the pouring crew to mean anything:

1. **Sampling** is witnessed by the site engineer (or client's representative), not left to the concrete gang — record the pour it came from, the time, and the batch/truck ticket.
2. **Curing of the test cubes themselves** happens in a proper curing tank or immersion bath at controlled temperature, not on a windowsill or under a tarp on site — cubes cured wrong give a false-passing result on concrete that's actually weaker.
3. **Testing is done by an accredited/independent laboratory** — a lab with a recognised accreditation (e.g. PEC-recognised or an equivalent national accreditation body), not an in-house crusher with no calibration record. A contractor-run test on a contractor-supplied machine is not independent evidence in a dispute.
4. **The signed test report — with the machine calibration reference, sample ID, and pour cross-reference — goes into the handover pack (Section 10.8)**, not just a verbal "it passed."
5. **A failed cube is an engineer decision, not a site decision.** Core testing (extracting and testing an actual core from the structure) or a structural reassessment follows a failed cube — never a shrug and a re-pour of a different area.

Treat "the cubes will be tested" as an open item until you can name which lab, on what date, with what report number — the same discipline as HP-08's "basically done is not a state" (Section 14.1).

---

## Section 12: Common Sequencing Mistakes

Ranked by frequency-x-cost in residential work.

| # | Mistake | Why it happens | Consequence | Prevention |
|---|---|---|---|---|
| 1 | **Plastering over uninspected MEP rough-in** | Plaster crew is on site and idle; "we'll test it later" | Walls reopened, plaster patched, programme slips 1-3 weeks, patches visible forever | HP-08 as a written, signed gate. No plaster mix on site until it's signed. |
| 2 | **Deshuttering / loading a slab early** | Formwork needed for the next floor; programme pressure | Excessive deflection, cracking, permanent sag, in the worst case collapse | Section 5.2 table on the wall; strike on cube results with engineer sign-off |
| 3 | **Curing stopped over a weekend or holiday** | The person who wets it isn't there | Surface strength loss, crazing, dusting, reduced durability | Name a curing-responsible person with weekend cover; ponding or membrane rather than sprinkling |
| 4 | **DPC bridged by later paving or landscaping** | Landscape designed/added after the house | Rising damp, blown plaster at skirting level | Fix the final external levels BEFORE setting DPC; record them on the drawing |
| 5 | **Frames (chowkats) fitted after plaster** | Frames not ordered in time | Chased-back plaster, gaps, poor fixing, out-of-plumb doors | Frames on site before masonry reaches lintel level |
| 6 | **Cast-in sleeves/conduits forgotten in a slab** | Nobody coordinated MEP with the pre-pour inspection | Core-drilling a structural slab; possible reinforcement cut | HP-07 checklist explicitly lists cast-in items; MEP contractor signs the pre-pour |
| 7 | **Chasing a structural column/beam for a conduit** | Conduit routed by a mason, not designed | Structural capacity reduced; may require engineered repair | Rule stated to the crew at induction; route drawings issued to the electrician |
| 8 | **Backfilling against an unpropped basement/retaining wall** | Wall done, excavation open, tempting to close it | Wall cracks or overturns | Backfill only after the propping slab is in place and cured |
| 9 | **Masonry raised more than ~1.2 m in a day** | Piece-rate masons chasing output | Wall bulges/leans, joints squeeze | Marked lift limit; daily plumb check (HP-09) |
| 10 | **Waterproofing done before the parapet is built** | Roof slab done, waterproofer available | No upturn at the parapet junction — the exact place it leaks | Sequence: parapet → screed to falls → waterproof → flood test → protect |
| 11 | **No flood test before the protection screed** | "It looks fine" | Leak discovered after tiling; full bathroom stripped | HP-11 mandatory, 24-48 h, witnessed and photographed |
| 12 | **Painting before plaster has dried** | Programme pressure at the end | Peeling, blistering, efflorescence, alkali burn | 7-21 day dry-out; moisture check before primer |
| 13 | **Tiling before final floor levels/thresholds resolved** | Levels never coordinated between rooms | Level mismatches at every door, water flowing the wrong way | Set finished-floor-level (FFL) datum for the whole house before the first tile |
| 14 | **Adding water at the mixer for workability** | Concrete "too stiff" in the heat | Silent 20-30% strength loss across the whole pour | Plasticiser, not water; slump test each batch |
| 15 | **Electrical socket layout not checked against furniture plan** | Furniture plan produced later | Sockets behind wardrobes/beds; new chases through finished walls | Overlay the furniture plan at HP-08 |
| 16 | **Over-excavation "levelled off" with loose soil** | Digger went too deep | Differential settlement under the footing | Fill over-dig with PCC only |
| 17 | **Rebar cut on site to clear a pipe** | Field improvisation | Direct loss of designed capacity | Absolute prohibition; engineer decides all penetrations |
| 18 | **Skipping the anti-termite stages** | Not on the critical path, easy to drop | Post-construction treatment is costlier and less effective | Put all three stages on the programme with their own line items |
| 19 | **Starting internal finishes before the building is weather-tight** | Programme pressure | Rain damage to plaster, joinery, and painted surfaces | Weather-tight milestone as a programme gate |
| 20 | **No as-built photo record before concealment** | Nobody's job | Every future repair or renovation becomes exploratory demolition | Photograph every wall/slab before it's covered; file by room |

---

## Section 13: Programme / Gantt for a Small House

> **Basis and honesty statement:** the schedules below are **modeled estimates**, built from standard industry Gantt templates (a commonly used residential reference programme runs ~165 days / ~5.5 months from tendering to finishing) combined with the curing and formwork durations from Sections 5 and 7. **No authoritative house-size-specific week-by-week standard was found**, so these must be treated as planning baselines to be adjusted for local labour productivity, weather, cash flow, and material lead times — not as a cited external standard.

### 13.1 Programme A — Single-Storey ~1500 sqft, RC Frame, Normal Soil

| Wk | Activity | Duration | Predecessor | Critical? | Notes |
|---|---|---|---|---|---|
| 0 | Approvals, contractor mobilisation, utility applications | (pre-start) | — | Yes | Utility lead time is the hidden critical path |
| 1 | Site clearance, fencing, site office, setting out | 5 d | — | Yes | HP-01 |
| 1-2 | Excavation for footings + trenches | 5-7 d | Setting out | Yes | HP-02 |
| 2 | Anti-termite stage 1 + PCC blinding | 2 d | Excavation | Yes | |
| 2-3 | Footing reinforcement + formwork | 4-5 d | PCC | Yes | HP-03 |
| 3 | Footing pour | 1 d | HP-03 | Yes | HP-04, cubes taken |
| 3-4 | **Footing curing** | 7 d | Pour | Yes | Non-compressible |
| 4 | Backfill + compaction, anti-termite stage 2 | 3 d | Curing | Yes | |
| 4-5 | Plinth beam steel, formwork, pour | 4 d | Backfill | Yes | |
| 5-6 | Plinth beam curing (7 d) + DPC | 8 d | Pour | Yes | HP-05 |
| 6-7 | Plinth filling, sub-base, DPM, anti-termite stage 3 | 5 d | DPC | Yes | |
| 7 | Ground floor sub-slab pour + cure | 4 d | DPM | Yes | |
| 7-8 | Column steel + formwork + pour | 5 d | Plinth beam | Yes | HP-06 |
| 8-9 | Roof beam/slab formwork + propping | 6 d | Columns | Yes | |
| 9-10 | Slab reinforcement + cast-in MEP sleeves/conduits | 5 d | Formwork | Yes | HP-07 |
| 10 | Roof slab pour | 1 d | HP-07 | Yes | Single pour |
| 10-12 | **Slab curing 14 d; soffit strike @3 d; props out @7-14 d by span** | 14 d | Pour | Yes | Non-compressible |
| 11-13 | Masonry infill walls (can start once props allow safe access) | 12-15 d | Slab (partial) | Yes | HP-09; frames set with masonry |
| 13-14 | Parapet, roof screed to falls, waterproofing | 6 d | Masonry | Partly | HP-11 flood test |
| 13-15 | **Electrical + plumbing rough-in** | 10-12 d | Masonry | Yes | Overlaps masonry by zone |
| 15 | **MEP inspection + pressure tests + photo record** | 2 d | Rough-in | Yes | **HP-08 — the gate** |
| 15-17 | Internal plaster (ceilings then walls) | 10-12 d | HP-08 | Yes | HP-10 |
| 16-18 | External plaster | 8-10 d | Roof watertight | No (parallel) | |
| 17-18 | Plaster curing + dry-out | 7-14 d | Plaster | Yes | Non-compressible |
| 18-19 | Wet-area waterproofing + flood test | 4 d | Plaster | Yes | HP-11 |
| 19-21 | Flooring, tiling, skirting | 12-14 d | Waterproofing | Yes | HP-12; FFL datum set first |
| 20-21 | False ceiling / POP | 6 d | Plaster | No (parallel) | |
| 21-22 | Woodwork — door shutters, wardrobes, kitchen | 10-12 d | Flooring | Partly | |
| 22-24 | Painting: primer, putty, 2 coats | 10-14 d | Woodwork + HP-13 | Yes | |
| 23-24 | Electrical + plumbing second fix, fixtures | 7 d | Painting (coordinate) | Yes | HP-14 |
| 24-25 | External works: boundary wall, driveway, drainage | 10 d | — | No (parallel from wk 18) | |
| 25-26 | Snagging, cleaning, commissioning, handover | 7 d | All | Yes | HP-15 |

**Total: ~26 weeks / ~6 months** for a single-storey 1500 sqft RC-frame house under normal conditions with continuous funding and no monsoon shutdown.

### 13.2 Programme B — Double-Storey 5 Marla (~1125 sqft plot, ~2000 sqft covered), Lahore/Pakistan Context

Add to Programme A's structure a second storey cycle:

| Extra activity | Duration | Where it inserts |
|---|---|---|
| First-floor column steel/formwork/pour | 5 d | After GF slab props released |
| First-floor beam/slab formwork | 6-7 d | |
| First-floor slab steel + cast-ins + HP-07 | 5 d | |
| First-floor slab pour + 14 d cure | 15 d | |
| Staircase (cast with, or immediately after, the slab) | 4-6 d | Do NOT leave the stair to the end — it is the site's own access route |
| First-floor masonry, MEP, plaster | Repeats GF durations, overlapping GF finishes by zone | |

**Total: ~34-40 weeks / ~8-9.5 months.** The second storey does not double the programme, because finishes on the ground floor overlap structure on the first floor — but the two slab-curing periods are serial and cannot overlap.

### 13.3 Critical-Path Summary

The critical path on a small house is almost always:

```
Setting out → Excavation → Foundation pour → [7 d cure] → Plinth →
Columns → Slab pour → [14 d cure] → Masonry → MEP rough-in →
[HP-08 GATE] → Plaster → [dry-out] → Flooring → Painting → Handover
```

**Of a ~26-week programme, roughly 5-6 weeks is pure curing and drying wait.** That is ~20% of the programme spent waiting on chemistry. Any "we'll finish in 3 months" claim for a house of this size is either compressing a chemical dependency or skipping an inspection.

### 13.4 What Can Legitimately Be Parallelised

| Parallel pair | Condition |
|---|---|
| External plaster ∥ internal plaster | Different crews, roof watertight |
| Boundary wall / external works ∥ internal finishes | Separate crew, doesn't cross the building |
| False ceiling ∥ flooring | Protect the floor; or do ceiling first |
| MEP rough-in ∥ masonry, by zone | Zone must be fully built out before its rough-in starts |
| Joinery fabrication (offsite) ∥ everything | Measure from as-built openings, not drawings |
| Woodwork/kitchen procurement ∥ structure | **Start procurement in week 1** — lead times, not site work, cause the end-of-job stall |

### 13.5 Weather & Seasonal Adjustment (Pakistan)

| Season | Impact | Programme adjustment |
|---|---|---|
| Monsoon (Jul-Sep) | Excavation floods; pours washed out; plaster and paint won't dry | Avoid scheduling excavation/foundation in monsoon; add 15-25% float; get the roof on before it starts |
| Peak summer (May-Aug) | Hot-weather concreting risk; rapid evaporation; labour productivity drops | Night/early-morning pours; extend curing to 10-14 d; +10-15% duration on labour-intensive activities |
| Winter (Dec-Jan) | Slower strength gain; longer paint drying | Extend striking times; blended cements slower still |
| Ramadan / Eid / harvest | Labour availability drops sharply | Explicit non-working periods in the programme, not optimistic float |

---

## Section 14: Worked Examples

### 14.1 Worked Example — "Can we plaster on Monday?"

**Situation:** Slab poured Monday week 10. Masonry finished Friday week 12. Electrician says rough-in will be "basically done" Saturday week 13. Contractor wants plasterers in Monday week 14.

**Analysis:**
1. Masonry curing: last course Friday wk 12 → 7 days minimum → earliest plaster **Friday wk 13**. ✅ Monday wk 14 clears this.
2. MEP rough-in: "basically done" is not a state. HP-08 requires *complete* + draw wires pulled + pressure test held + photo record + signed walkthrough. That is **2 further days minimum** after actual completion.
3. Pressure test hold period alone: 1-2 h supply test + drainage test, plus rectification time if it fails.
4. Also unresolved: are the concealed fixings for the wall-hung WC and the TV bracket in? Is the shower valve set to the *tiled* face depth, not the plaster face?

**Answer:** No. Earliest realistic plaster start is **Wednesday week 14**, and only if the rough-in genuinely completes Saturday and HP-08 passes first time. Plastering Monday buys 2 days and risks a 2-week reopening. **The correct call is to hold.**

### 14.2 Worked Example — Slab Prop Removal, 5.2 m Span

**Situation:** Slab with a 5.2 m clear span, poured with OPC, ambient 38 °C. Site wants props out at day 7 to start the next storey's columns.

**Analysis:**
- Span > 4.5 m → IS 456 minimum for prop removal is **14 days**, not 7.
- Hot conditions (38 °C) → curing period itself extends to 10-14 days per IS 456 Cl. 13.5.1.
- Day-7 cubes typically read ~65-70% of fck — below the 70-80% threshold that would justify early curing termination, and prop removal is a *loading* decision requiring more margin than curing termination.
- Next-storey columns impose construction load (formwork, wet concrete, workers, stacked material) on the slab.

**Answer:** Props stay to **day 14 minimum**. If the programme genuinely cannot absorb it, the only legitimate route is: cast extra cubes cured alongside the slab, test at day 10, and obtain the **structural engineer's written approval** for early striking with **back-propping** designed by them. Not a site decision.

### 14.3 Worked Example — DPC Level Setting

**Situation:** Road crown level measured at +0.00. Plot natural ground at -0.15 m. Client intends to lay 100 mm driveway paving on 150 mm sub-base later, and to raise the front garden by 200 mm.

**Analysis:**
- Future finished external ground level at the front = natural ground (-0.15) + garden raise (0.20) = **+0.05 m**.
- Future driveway finished level = subgrade + 0.15 sub-base + 0.10 paving, set to drain from the house.
- DPC must be **≥ 150 mm above the *final* external ground level**, per Approved Doc C 5.5 → DPC ≥ +0.05 + 0.15 = **+0.20 m minimum**.
- Plinth height must also satisfy the bye-law: **≥ 2 ft (0.61 m) and ≤ 4.5 ft (1.37 m)** above surrounding ground (KP Model Bye-Laws 2017 / DHA / LDA).
- Plinth must clear the road crown for drainage → set plinth top at **+0.61 to +0.75 m** above the surrounding ground.

**Answer:** Set the plinth top (and DPC) at around **+0.60 to +0.70 m** relative to road crown, which satisfies both the bye-law minimum and the 150 mm DPC clearance with generous margin against the future garden raise. **Record the assumed future landscape levels on the drawing** so that whoever does the landscaping a year later doesn't bridge the DPC.

### 14.4 Worked Example — Mix Selection Across One House

| Element | Grade / ratio | Why |
|---|---|---|
| Blinding under footings | M15 (1:2:4) | Non-structural levelling layer |
| Isolated footings | M20 (1:1.5:3) | Standard residential structural grade |
| Ground-floor columns (double storey) | M20, or M25 if heavily loaded / engineer specifies | Accumulated load at base |
| Plinth beam | M20 | |
| Slabs and beams | M20 | |
| Boundary wall footing | M15 | Non-structural |
| Driveway slab | M25 | Rigid pavement, point loads from vehicles |
| 9-inch load-bearing / ground-floor / seismic masonry | Mortar 1:4 | Higher strength requirement |
| 4.5-inch upper-floor partitions | Mortar 1:6 | Medium-strength, up to 3 storeys |
| Internal plaster | 1:5 or 1:6 | |
| External plaster & wet areas | 1:4 | Weather and moisture exposure |

---

## Section 15: Integration with FreeCAD / BIM (4D Sequencing)

When this skill is used alongside `architecture-freecad-bim`:

1. **Model in construction order, not drawing order.** Build the FreeCAD model as Site → Building → Storey → element, and create elements in the sequence of Section 1.1. This surfaces sequencing conflicts (a beam that can't be formed, a wall built before its supporting slab) while they're still free to fix.
2. **Tag every object with a construction stage.** Add a custom property (e.g. `ConstructionStage = "12-Superstructure-GF"`) so the model can be filtered/coloured by stage and exported as a 4D sequence.
3. **Model the cast-in items.** Sleeves, conduit runs through slabs, and puddle flanges should exist as real void objects in the BIM model. If they only exist in the MEP drawing, they will be missed at HP-07.
4. **Model the plaster/tile thickness.** Back boxes, shower valves, and door frames are set to *finished* faces. A model that omits the 15 mm plaster and 10 mm tile produces boxes set to the wrong depth.
5. **Model the future external ground level**, so the DPC clearance (Section 6.2) can be verified visually rather than assumed.
6. **Export a stage-filtered set of views** as the site's stage-by-stage build guide — far more useful to a mason than a full drawing set.
7. **Never label the export as construction-ready.** See the Reality Check section — it is a planning model until a PEC-registered engineer stamps it and the authority approves it.

---

## Section 16: Standards Citation Index

| Standard | Clause / section | What it governs here |
|---|---|---|
| **ACI 318-19** | Ch. 26, §26.5.3-26.5.5 | Concrete curing — required duration, temperature and moisture conditions. *Note: "Sec. 5.11" is the CORRECT clause only under the pre-2019 ACI 318 chapter numbering (where Ch. 5 = "Concrete Quality, Mixing and Placing"); in the current ACI 318-19 structure Ch. 5 is "Loads" and curing moved to Ch. 26 "Construction Documents and Inspection" — always confirm which edition's numbering a source is using before quoting a clause.* |
| **IS 456:2000** | Cl. 13.5.1 | Minimum curing period: 7 d OPC / 10 d blended; 10-14 d hot/arid; termination at 70-80% fck |
| **IS 456:2000** | Table 12A (formwork/deshuttering) | Vertical forms 16-24 h; slab soffit (props left) 3 d; **beam soffit (props left) 7 d** — not the same figure as the slab soffit; props to slab 7 d (≤4.5 m) / 14 d (>4.5 m); props to beams/arches 14-21 d by span |
| **IRC 2021** | Ch. 4 / R403, Table R301.2 | Footing depth — min 12 in (305 mm) below undisturbed grade, and below the frost line |
| **ASCE 32** | (referenced by IRC 2021) | Frost-protected shallow foundation design method |
| **ASCE 7-22** | (referenced by IRC 2021) | Wind and seismic loads — *numeric load values not verified in this pass; run a dedicated check before using load numbers* |
| **UK Building Regs, Approved Document C** | Sec. 5.5 | DPC ≥ 150 mm above finished external ground level |
| **NHBC Standards** | 5.1.19 | DPC detailing; cavity ≥ 225 mm below DPC or cavity tray; weep holes every 900 mm |
| **Building Code of Pakistan (BCP) 2007 — Seismic Provisions** | Approved 9 Aug 2007, notified 8 Sep 2008; hosted at pec.org.pk / urbanunit.gov.pk | Seismic zoning, masonry confinement, detailing. *Exact excavation/foundation clause numbers require a direct PDF read — not resolvable from secondary sources.* |
| **BCP 2021 (final draft, 26.10.2021)** | pec.org.pk | Updated national provisions — check adoption status in the relevant jurisdiction |
| **KP Model Building Bye-Laws 2017** | Plinth provisions | Plinth height min 2 ft / max 4.5 ft |
| **DHA Bye-Laws 2020** | Plinth & setback provisions | Consistent with the 2 ft / 4.5 ft range |
| **LDA Building & Zoning Regulations 2019** | Plinth & setback provisions | Lahore jurisdiction |
| **Islamabad Residential Sectors Zoning Regulation 1993** | Plinth & setback provisions | CDA jurisdiction |

**Verification protocol:** before using any clause number in a document a human will act on, open the primary standard and confirm the clause against the current edition. Where this file flags a gap (BCP clause numbers, ASCE 7-22 load values), state the gap rather than inventing a number.

---

## Section 17: Quick Reference Card

**The five wait times you cannot argue with**
| Wait | Duration |
|---|---|
| Concrete curing, OPC / blended / hot-arid | 7 d / 10 d / 10-14 d |
| Slab props out, span ≤4.5 m / >4.5 m | 7 d / 14 d |
| Beam props out, span ≤6 m / >6 m | 14 d / 21 d |
| Masonry before plaster | 7 d (14 d better) |
| Plaster before paint | 7-21 d dry-out |

**The five numbers you set once and live with**
| Item | Value |
|---|---|
| DPC above final external ground level | ≥ 150 mm |
| Plinth height (Pakistan bye-laws) | 2 ft min / 4.5 ft max |
| Footing depth (IRC minimum) | ≥ 305 mm below undisturbed grade, and below frost line |
| Structural concrete, residential default | M20 (1:1.5:3) |
| Load-bearing masonry mortar | 1:4 (1:6 for non-load-bearing above ground floor) |

**The one gate that matters most**
> **HP-08 — MEP rough-in complete, tested, photographed, and signed off BEFORE any plaster.** Every other gate protects a stage. This one protects the whole finishing programme.

**The sentence to say when someone wants to compress the schedule**
> "Which dependency are we compressing — physical, chemical, verification, or preferential? Only the last one is negotiable."

**The sentence to say when someone treats this output as final**
> "This is a planning model, not a stamped drawing — it needs a PEC-registered engineer's review and local authority approval before anyone digs."
