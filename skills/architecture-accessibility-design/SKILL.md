---
name: architecture-accessibility-design
description: >
  Practical accessibility design for single-family houses — the visitability
  baseline (zero-step entry, 32 in clear doors, one main-floor accessible
  bathroom), ramp geometry and slope math, hallway and door clear-width rules,
  accessible bathroom and kitchen layouts, lever hardware and reach ranges,
  aging-in-place blocking and future-proofing, retrofit decision trees, and
  FreeCAD clear-width/turning-circle verification. Includes a condensed
  full-compliance reference tier (ADA 2010 Standards, ICC A117.1-2017 Type A/B
  dwelling units, HUD Fair Housing Act Design Manual, BS 8300, DIN 18040,
  AS 1428, NBC India) to load only when a project crosses into 4+ unit
  multifamily, commercial conversion, or a client explicitly requires certified
  legal accessibility compliance.
---

# Accessibility Design for Houses

This skill is sized for **single-family residential work**. The default answer to
"make this house accessible" is not the ADA — the ADA does not legally apply to a
private detached home — it is the **visitability** baseline plus a handful of
dimensional numbers borrowed from ADA/ICC A117.1 that builders use informally
because they are the numbers that actually work for a wheelchair.

Full institutional/commercial depth is preserved but **demoted to Section 11**.
Load Section 11 only when the project is genuinely a compliance project (4+ unit
building, assisted-living conversion, public/commercial facility, or a client who
has said the words "ADA compliant" and means it contractually).

All dimensions are given metric-first with imperial equivalents, because
Pakistani residential drawings are dimensioned in feet-inches while the source
standards are in inches and the FreeCAD model is in millimetres.

---

## Reality Check — Licensing & Liability

**This skill produces design aids and planning/FreeCAD-modelling guidance ONLY.**

1. **Nothing here is a construction document.** Every dimension, ramp run, grab-bar
   height, and cost figure is for preliminary layout, feasibility, cost
   orientation, and 3D/BIM modelling.
2. **Any design intended for the actual construction of a real, occupied building
   MUST be reviewed, sealed and stamped by a licensed structural engineer** — in
   Pakistan a **PEC-registered** Professional Engineer (and a **PCATP-registered**
   architect for the architectural drawings); elsewhere the equivalent registered
   professional. This applies the moment a ramp becomes a cantilevered/suspended
   structure, a wall is widened for a door, a lift pit is excavated, or ceiling
   structure is loaded by a hoist.
3. **The design MUST go through local authority plan approval before
   construction** — LDA (Lahore), CDA (Islamabad), SBCA (Karachi), RDA
   (Rawalpindi), DHA, TMA or Cantonment Board — under their byelaws for setback,
   coverage, plinth level, ramp encroachment into setback, and structural vetting.
   A ramp that solves accessibility but projects into the mandatory front setback
   can be refused approval or demolished.
4. **Widening a doorway is a structural act until proven otherwise.** Any opening
   enlarged in a load-bearing masonry wall or shear wall needs a new lintel/header
   sized by the engineer. Never present a "just widen the door" instruction without
   flagging this.
5. **Claude / Claude must never present FreeCAD output or these dimensions as
   construction-ready.** Label deliverables
   `PRELIMINARY — NOT FOR CONSTRUCTION — requires licensed engineer/architect review`.
6. **Say this unprompted.** If the user's language suggests they are treating output
   as final ("send this to the contractor", "so we can start the ramp tomorrow",
   "is this ADA certified?"), stop and state the stamping + approval requirement in
   that message, not in a footnote.
7. **Never claim legal compliance.** This skill can say a design *follows the
   dimensional guidance of* ADA/A117.1. Only an accessibility consultant / plan
   reviewer / authority having jurisdiction can certify compliance. If a client
   needs a certificate, that is a human specialist referral, full stop.
8. **Cost figures in Section 9 are illustrative US 2026 market data.** They are
   order-of-magnitude only and must be re-scaled to local market and currency
   before appearing in any client-facing estimate — use
   `architecture-cost-estimation-boq` for real Pakistan rates.

---

## Section 1: Scope Decision Tree — Which Tier Applies

Run this **first**. It decides whether you stay in Sections 2–10 (cheap, fast,
sensible) or must load Section 11 (heavy, legal, expensive).

```
What is the building?
│
├─ Private detached / semi-detached single-family house, owner-occupied
│  → TIER 1 — VISITABILITY DEFAULT (Sections 2–10)
│    No ADA legal obligation. No A117.1 obligation. IRC 2021 has no residential
│    accessibility chapter. Design to the visitability triad + the dimensional
│    numbers in Section 3–7. Cost impact at design stage: ~0–1.5% of build cost.
│
├─ Same house, but a specific occupant is a wheelchair user / will be
│  → TIER 1+ — FULL-TIME WHEELCHAIR HOUSE (Sections 2–8, upper bound of every
│    range, plus Section 6.4 turning-space audit in EVERY room they use)
│    Design to the person, not the code. Measure their actual chair
│    (width, length, turning radius, seat height, reach) — power chairs need
│    materially more than the 1525 mm circle; a mid-wheel-drive power chair is
│    fine in 1525 mm, a rear-wheel-drive chair with elevating legrests is not.
│
├─ House being converted to a guest house / clinic / school / office / shop
│  → TIER 3 — COMMERCIAL. Section 11 applies in full. This is now a public
│    accommodation; ADA-equivalent obligations and local byelaw accessibility
│    clauses attach. Escalate to a human accessibility consultant.
│
├─ Residential building with 4+ dwelling units (apartments, rental block)
│  → TIER 2 — FHA / A117.1 TYPE B. Section 11.3. Type B "adaptable" units are
│    the coordinated minimum. Not optional in the US; in Pakistan check the
│    development authority's byelaw for its own accessibility clause.
│
└─ 4+ storey Group R-2 with elevator service
   → TIER 2+ — 2% of units must be Type A (fully accessible, not just
     adaptable). Section 11.3. Definitely a consultant project.
```

**Rule: default to Tier 1.** Do not impose commercial ADA depth on a family house
— it inflates cost, produces institutional-looking rooms, and is the single most
common way this skill can be used badly. If asked for "ADA compliance" on a
private home, ask once what is actually driving the request (a specific occupant?
resale? a grant? a rental plan?) before escalating tiers.

---

## Section 2: The Visitability Baseline (Tier 1 Default)

**Visitability** (Concrete Change / Eleanor Smith; adopted as a voluntary
ordinance in a number of US municipalities, and as the concept behind UK Part M
M4(1) "visitable dwellings") is the residential-scale answer. It is deliberately
minimal: a house is *visitable* if a wheelchair user can get in, move around the
main floor, and use a toilet — not necessarily live there.

### 2.1 The Triad — three requirements, non-negotiable for Tier 1

| # | Requirement | Numeric target | Cost if designed in | Cost if retrofitted |
|---|---|---|---|---|
| 1 | **At least one zero-step entrance** from driveway, garage, or street | ≤ 13 mm (0.5 in) threshold, on a route with ≤ 1:20 running slope, or a compliant 1:12 ramp | Near zero (grading + plinth decision) | High (Section 3.5) |
| 2 | **All main-floor doorways ≥ 815 mm (32 in) clear** | 915 mm (3'-0") leaf minimum to guarantee it | ~1–3% of door budget | Moderate–high (structural) |
| 3 | **At least a half-bath (WC + basin) on the entry floor, usable from a chair** | Section 5.2 minimum layout | Low (plan-stage decision) | Very high |

**Why the triad and not more:** these three are the ones that are *impossible or
brutally expensive to add later*. Grab bars, lever handles, and raised outlets can
be retrofitted any Saturday. A 762 mm door in a load-bearing wall and a first-floor-
only toilet cannot.

### 2.2 Tier 1 full checklist (the pragmatic house list)

| Item | Target | Section |
|---|---|---|
| Zero-step entry (≥1) | ≤13 mm threshold | 3 |
| Approach route slope | ≤1:20 preferred, 1:12 max as ramp | 3.2 |
| Exterior route clear width | 915 mm (36 in) min, 1220 mm (48 in) preferred | 3.1 |
| Main-floor door clear width | 815 mm (32 in) min → 915 mm leaf | 4.1 |
| Main-floor hallway clear width | 915 mm (36 in) min, 1065 mm (42 in) preferred | 4.3 |
| One main-floor accessible bath | Section 5 layout | 5 |
| Grab-bar blocking in ALL bathrooms | 33–36 in AFF plywood backing | 8.1 |
| Lever handles throughout | Closed-fist operable | 7.1 |
| Rocker light switches at 1120 mm | vs 1370 mm standard | 7.2 |
| Outlets raised to 460 mm | vs 305 mm standard | 7.2 |
| Main-floor bedroom (or convertible room) | 3.0 × 3.6 m usable | 8.3 |
| Stacked closets for future lift | 1525 × 1525 mm footprint | 8.4 |

Items 7–12 cost almost nothing at design stage and are what turn a *visitable*
house into a *liveable-for-life* house.

---

## Section 3: Entry and Approach — Getting In Without a Step

### 3.1 Route dimensions (residential)

These are practical numbers, not legal citations — a private house owes no code
body compliance. Full citation trail (for a Tier 2/3 project) is in Section 11.2.

| Element | Minimum | Preferred (residential) |
|---|---|---|
| Exterior accessible route clear width | 915 mm (36 in) | 1220 mm (48 in) |
| Running slope, "not a ramp" | ≤1:20 (5%) | ≤1:25 (4%) |
| Running slope, ramp | ≤1:12 (8.33%) | 1:16 to 1:20 if space allows |
| Cross slope (all routes) | ≤1:48 (2%) | 1:60 for drainage without tipping |
| Surface | Firm, stable, slip-resistant | Broom-finish concrete or unglazed tile; NOT loose gravel, NOT polished stone |
| Gaps/grating openings | ≤13 mm (0.5 in) in direction of travel | Perpendicular orientation |
| Change in level | ≤6 mm vertical; 6–13 mm bevelled at 1:2; >13 mm needs ramp | 0 mm |

### 3.2 The single most useful trick: regrade instead of ramping

**A slope of 1:20 or flatter is not legally a ramp.** No handrails, no edge
protection, no 1525 mm landings, no institutional look. If you have run available,
grading the approach at 1:20 is almost always the better answer than building a
1:12 ramp with rails.

```
Plinth rise 450 mm (1'-6")   → 1:20 needs  9.0 m of run   → 1:12 needs  5.4 m + landings + rails
Plinth rise 600 mm (2'-0")   → 1:20 needs 12.0 m of run   → 1:12 needs  7.2 m + landings + rails
Plinth rise 300 mm (1'-0")   → 1:20 needs  6.0 m of run   → 1:12 needs  3.6 m + landings (no rails if rise ≤150 mm)
```

**Pakistani plinth problem — read this before ramping any local house.** Local
practice sets the plinth 450–600 mm (1'-6" to 2'-0") above natural ground for
monsoon drainage and street-level rise. That is a *large* rise to overcome. Options
in order of preference:

1. **Slope the driveway/forecourt itself** at 1:20 toward the entry over 9–12 m —
   the car park doubles as the accessible route. Costs only earthwork.
2. **Enter from the car porch/garage side**, where the finished slab is usually
   only 150–225 mm below plinth — a 3–4.5 m run at 1:20, or a short 1:12 ramp with
   no handrails if rise ≤150 mm.
3. **Split the rise:** raise the approach path 300 mm with fill at 1:20, then a
   short 1:12 ramp for the last 300 mm (3.6 m run).
4. **Ramp the full rise** — last resort, Section 3.3.
5. **Vertical platform lift** — only where run is genuinely unavailable (tight
   urban 3–5 marla plot). Adds a mechanical maintenance item; needs power and a
   rain hood.

### 3.3 Ramp geometry (when you must)

| Parameter | Value | Notes |
|---|---|---|
| Max running slope | 1:12 (8.33%) | 1:15–1:20 much easier to self-propel |
| Max cross slope | 1:48 (2%) | Tipping hazard above this |
| Max rise per run | 760 mm (30 in) | Then a landing is mandatory |
| Max run length before landing | 9.0 m (30 ft) at 1:12 | = 760 mm rise |
| Min clear width between rails | 915 mm (36 in) | 1100 mm if two-way / caregiver alongside |
| Landing at top and bottom | 1525 × 1525 mm (60 × 60 in) | Full ramp width if wider |
| Landing at direction change | 1525 × 1525 mm | Non-negotiable for a 90°/180° turn |
| Landing slope | ≤1:48 all directions | A sloped landing defeats the landing |
| Edge protection | 50 mm (2 in) curb, wall, or rail extension | Stops a castor dropping off the edge |
| Handrails required when | Rise > 150 mm (6 in) OR slope steeper than 1:20 | Both sides |
| Handrail height | 865–965 mm (34–38 in) above ramp surface | Continuous over landings |
| Handrail extensions | 305 mm (12 in) horizontal beyond top and bottom | Warns of run end by feel |
| Handrail grip | 32–51 mm (1.25–2 in) circular, 38 mm clear of wall | Must be graspable, not a flat plank |
| Second (child/low) rail | 600–700 mm, optional | Useful for children and short-stature users |

**Worked example — 600 mm plinth, 1:12 ramp with a 180° turn (typical 10-marla
front court):**

```
Rise total                 = 600 mm
Max rise per run           = 760 mm  → 600 mm fits in ONE run, but…
Run at 1:12                = 600 × 12 = 7200 mm straight
Straight length needed     = 1525 (bottom landing) + 7200 + 1525 (top landing) = 10.25 m
Available front court      = 6.0 m  → straight ramp does not fit
→ Switchback: two runs of 300 mm rise = 3600 mm each
  Length per leg           = 1525 + 3600 + 1525(turn landing) = but legs share the turn landing
  Footprint                = 3600 + 1525 = 5.13 m long × (915 + 915 + 150 wall) = 1.98 m wide
  Plus bottom landing 1525 mm and top landing 1525 mm at the ends of the legs
  Total footprint          ≈ 5.2 m × 2.0 m — FITS in a 6.0 m court
Handrails                  = both sides of both legs, continuous around the turn landing,
                             305 mm extensions at the two open ends
Edge protection            = 50 mm upstand curb both sides, both legs
```

Sanity check every ramp against: *rise ÷ slope + landings ≤ available run*. If it
fails, go back to Section 3.2 before making the ramp steeper. **Never** design
residential ramps at the old 1:10 / 1:8 "constrained existing construction"
exceptions unless the client is told explicitly they are unsafe to self-propel and
require an assistant.

### 3.4 The threshold detail (the part that actually gets built wrong)

```
Target: ≤13 mm (0.5 in) total, bevelled at 1:2 above 6 mm. Best: 0 mm.

Working detail for a Pakistani main door on a 600 mm plinth:
  · Outside: paved landing set 15 mm BELOW finished floor level, sloped 1:60 away
  · Threshold: aluminium low-profile sill, 10 mm upstand, bevelled both faces
  · Drainage: 100 mm wide linear channel/slot drain immediately outside the sill,
    grated with ≤13 mm slots perpendicular to travel — this is what lets you go
    flush without water tracking in
  · Door bottom: brush/drop seal, not a raised timber weather bar
  · Canopy/overhang ≥1200 mm projection over the landing to keep driving rain off
```

Without the slot drain, the zero-step entry floods. That is why builders default to
a step; give them the drain and the objection disappears.

### 3.5 Retrofit decision tree — existing house, no zero-step entry

```
Is there ANY door with rise ≤ 150 mm from a paved area?
├─ YES → Ramp it: ≤1.8 m run at 1:12, no handrails required. Cheapest possible fix.
└─ NO
   ├─ Is there ≥ (rise × 20) of run available on any approach? → Regrade at 1:20.
   ├─ Is there ≥ (rise × 12) + 3.05 m? → Straight 1:12 ramp.
   ├─ Is there a ~5 × 2 m rectangle? → Switchback 1:12 ramp.
   ├─ Garage/car porch slab within 225 mm of floor level? → Convert garage door
   │   route to primary accessible entry; short internal ramp.
   └─ None of the above → vertical platform lift (750 mm rise class) or,
       if rise ≤ 300 mm and budget is tight, a modular aluminium ramp
       (removable, no foundation, usually no permit — but check byelaw setback).
```

---

## Section 4: Doors, Hallways and Circulation

### 4.1 Door clear width — the number everyone gets wrong

**32 in (815 mm) is the CLEAR width, not the door size.** Clear width is measured
from the face of the open door leaf (at 90°) to the opposite stop. A leaf loses
roughly 60–100 mm to the leaf thickness, stop, and hinge offset.

| Door leaf size | Approx. clear opening | Verdict |
|---|---|---|
| 610 mm (2'-0") | ~530 mm | Fails badly — closets only |
| 762 mm (2'-6") — **Pakistani interior default** | ~680 mm | **FAILS.** Standard local interior door is not visitable. |
| 838 mm (2'-9") | ~755 mm | Fails (marginal manual chair only, scrapes knuckles) |
| **915 mm (3'-0")** | **~815–840 mm** | **PASSES — specify this as the residential minimum** |
| 1067 mm (3'-6") — typical local main door | ~975 mm | Comfortable; good for main entry |
| Double leaf 2 × 610 mm | ~530 mm per leaf | **FAILS** — one active leaf must give 815 mm alone |

**Action rule: on any Tier 1 house, specify 3'-0" (915 mm) leaves for every
main-floor door including the bathroom.** The upcharge over 2'-6" is trivial at
build time and unrecoverable later.

Tricks when 915 mm will not fit:
- **Swing-clear (offset) hinges** recover 40–50 mm by swinging the leaf fully clear
  of the opening. Turns a marginal 838 mm door into a passing one.
- **Pocket / barn / sliding door** — clear width = the full rough opening minus
  ~25 mm. Best answer for tight bathrooms; also removes the swing conflict in
  Section 5. Specify a **D-pull, not a recessed finger cup** (a recessed cup fails
  the closed-fist test).
- **Remove the door entirely** — a cased opening at 915 mm passes and costs nothing.

### 4.2 Maneuvering clearance at doors

The clear width is useless if a chair cannot line up on the latch side.

**Residential shortcut (use this for Tier 1 — it covers the case that actually
occurs in a house):** provide **460 mm (18 in) of free wall on the latch side of
the pull face** of every main-floor door, with **1525 mm (60 in) of clear floor**
in front of it. That single rule satisfies the approach that matters; the classic
residential failure is a bathroom door hinged so it opens into a 900 mm corner
with zero latch-side wall. The full five-approach-condition breakdown (push
side, hinge side, latch-side push/pull, each with its own clearance and depth)
is ADA §404.2.4 / A117.1 §404.2.3 territory — pull it from the primary standard
directly if you are auditing an unusual door condition; a house rarely needs
more than the shortcut above.

Other door items:
- Threshold at interior doors: **0 mm**. No timber saddles between rooms. If flooring
  materials change, use a flush transition strip.
- Opening force: ≤22 N (5 lbf) interior. Residential doors rarely have closers —
  if one is fitted, it must take ≥5 s to swing from 90° to 12°.
- Hardware height: 865–1220 mm (34–48 in) AFF. Local standard ~1000 mm is fine.

### 4.3 Hallways and circulation

| Element | Minimum | Preferred | Note |
|---|---|---|---|
| Hallway clear width | 915 mm (36 in) | 1065–1220 mm (42–48 in) | 915 mm is a *straight* pass only |
| Narrowing at a door jamb | 815 mm (32 in), max 610 mm (24 in) of length | avoid | — |
| Hallway with a 90° turn into a door | 1065 mm (42 in) hall + 915 mm door approach, or 1220 mm hall | 1220 mm | This is where 915 mm halls fail |
| Passing space (two chairs) | 1525 mm (60 in) at intervals | at each hall junction | Rarely needed in a house |
| Turning space (any room they must turn in) | 1525 mm (60 in) diameter circle | 1675 mm for power chairs | — |
| T-turn alternative | 1525 × 1525 mm T; arms ≥915 mm wide × 1525 mm long; base ≥610 mm deep | — | Use where a full circle will not fit |
| Clear floor space (parked chair) | 760 × 1220 mm (30 × 48 in) | — | At every fixture, appliance, control |

**Corridor rule of thumb:** a 915 mm hallway that ends in a 90° turn into a 915 mm
door **does not work** for most chairs. Either widen the hall to 1065–1220 mm at
the turn, or make the door 1067 mm, or approach the door head-on. Model this in
FreeCAD (Section 10.3) rather than eyeballing it.

Also:
- Protruding objects (wall lights, shelves, open stair soffits) may not project
  more than 100 mm into a route between 685 and 2030 mm AFF. Below 685 mm a cane
  detects them; above 2030 mm they are clear.
- Under-stair space: box it in or rail it off below 2030 mm headroom — the classic
  head-strike hazard for a blind user in a house.
- Flooring: firm and low-pile. **Carpet pile ≤13 mm with firm pad**; deep pile,
  loose rugs and thick door mats are the most common in-house mobility hazard.

---

## Section 5: The Accessible Bathroom (One, on the Entry Floor)

Tier 1 requires **one**. Do not make every bathroom accessible in a family house —
it is expensive and produces clinical rooms.

### 5.1 Which bathroom

- Entry/main floor, on the accessible route, reachable without passing through a
  bedroom if it is the visitable-guest WC.
- If the house has a main-floor bedroom (Section 8.3), the ideal is one bathroom
  that serves both as the guest WC and that bedroom's ensuite — a single accessible
  room doing two jobs.

### 5.2 Minimum viable half-bath (visitability floor)

The absolute Tier 1 minimum is a **WC + basin the user can enter, close the door,
transfer, and exit**.

```
Minimum internal clear: 1525 mm × 1525 mm (5'-0" × 5'-0")   ← with an OUT-swinging
                                                              or sliding door
Alternative accepted layout: 915 mm × 1525 mm (3'-0" × 5'-0") "parallel approach"
   half-bath — chair enters, does NOT turn, transfers sideways, backs out.
   Only acceptable where the door is at the END of the 1525 mm dimension.

WC:      centreline 405–455 mm (16–18 in) from the side wall/partition
         seat height 430–485 mm (17–19 in) — i.e. a "comfort height" pan
Basin:   rim ≤865 mm (34 in) AFF; wall-hung or with removable vanity base
Door:    915 mm leaf, OUT-swinging or sliding/pocket
Clear floor at WC: 760 × 1220 mm minimum for a side transfer
```

**Do not confuse this with the ambulatory-compartment number.** The 430–485 mm
(17–19 in) figure above is the *seat height*, not the centreline offset. A
different fixture configuration — the ambulatory accessible compartment used
alongside a bank of standard stalls in a commercial washroom, Section 11.3 — uses
its own 17–19 in centreline convention. Do not borrow that number for the single
wheelchair-accessible WC this skill describes; use 405–455 mm (16–18 in) from the
side wall/partition to the WC centreline, full stop.

**Door swing rule:** the door must not swing into the required clear floor space
unless there is 915 mm of additional clearance beyond the swing. In a small house
bathroom there never is — so **out-swing or slide**. Out-swing has a second benefit:
if someone falls against the inside of the door, it can still be opened.

### 5.3 Full accessible bathroom (Tier 1+, wheelchair occupant)

| Element | Requirement |
|---|---|
| Turning space | 1525 mm (60 in) diameter circle clear of the door swing and fixtures |
| WC centreline | 405–455 mm (16–18 in) from side wall/partition — NOT the 17–19 in ambulatory-compartment figure, see Section 5.2 |
| WC seat height | 430–485 mm (17–19 in) AFF |
| Clear space beside WC | 760 mm (30 in) wide × 1220 mm (48 in) transfer space, one side |
| Side grab bar | ≥1065 mm (42 in) long, starting ≤305 mm (12 in) from rear wall, **833–915 mm (33–36 in) AFF to top of bar** |
| Rear grab bar | ≥915 mm (36 in) long, centred on WC (min 305 mm on the far side of centreline), same 33–36 in height. **A ≥610 mm (24 in) bar is a narrow exception only** — permitted solely where a tank-type WC prevents the full-length bar on the tank side; do not use 610 mm as the default. |
| Grab bar diameter / clearance | 32–38 mm (1.25–1.5 in) dia; 38 mm (1.5 in) clear of wall |
| Grab bar load | Must resist **1.1 kN (250 lbf)** in any direction — this is why blocking matters (Section 8.1) |
| Toilet paper | 190–230 mm (7–9 in) in front of WC, ≥380 mm (15 in) AFF |
| Basin | Rim ≤865 mm; knee clearance 685 mm high × 205 mm deep at 230 mm above floor; toe 230 mm high × 355 mm deep; **insulate/box the P-trap and hot supply** (leg burns are a real injury here) |
| Tap | Single lever or wrist-blade; ≤22 N operating force |
| Mirror | Bottom of reflective surface ≤1015 mm (40 in) AFF, or tilt |
| Shower — preferred | **Curbless/roll-in, 1525 × 915 mm (60 × 36 in)**, floor graded 1:50 to a linear drain, waterproof membrane turned up 150 mm, wet-room threshold 0 mm |
| Shower — transfer type | 915 × 915 mm (36 × 36 in), curb ≤13 mm, seat on wall opposite controls at 430–485 mm |
| Shower seat | Folding, 460 mm deep × 610 mm long, 430–485 mm AFF, load 1.1 kN |
| Shower controls | Offset toward the entry/seat, 380–1220 mm AFF, lever type, **thermostatic anti-scald** |
| Hand shower | On a 1525 mm (60 in) hose, slide bar reachable from seated position |
| Flooring | Slip-resistant when wet — **PTV ≥36 / R10–R11** unglazed porcelain or textured vinyl. Polished tile in an accessible bathroom is a design failure. |
| Bath (if retained) | Not accessible. If the client insists, add a 380 mm wide × full-length transfer seat at the head end plus horizontal + vertical grab bars — and tell them a curbless shower is the actually-usable option. |

**Sanity-check worked example — do this arithmetic every time, the way ramp runs
are checked in Section 3.3, so a wrong reference number gets caught before it is
built:**

```
Bathroom internal width available: 1525 mm (5'-0")
WC centreline from side wall: 405-455 mm       → WC bowl sits mostly against that wall
Transfer space required beside WC: 760 mm wide  → must fit in the REMAINING width
Remaining width = 1525 - (centreline offset, ~230 mm half-bowl allowance) ≈ 1070-1120 mm
760 mm transfer space fits inside that remainder → PASSES

If the centreline were wrongly placed at 460-480 mm (an 18-19 in figure borrowed
from the wrong fixture type), the WC pulls further from the wall, eating into the
760 mm transfer strip and crowding the side grab bar's 305 mm rear-wall start
point — the error compounds instead of staying a rounding difference. Re-run this
check whenever a plan dimension changes; don't assume the reference number is
right just because it looks close to the ADA figures quoted elsewhere.
```

### 5.4 Curbless shower in a Pakistani slab — the buildability note

A roll-in shower needs the wet area's finished floor **level with the room** while
still draining. Achieved by one of:

1. **Recessed slab / dropped shutter** — form the shower zone slab 50–75 mm lower
   at casting stage, then build the screed fall back up. Free if planned; impossible
   after casting. **This is a design-stage decision that must reach the structural
   drawings.**
2. **Raise the whole bathroom floor** 50–75 mm on screed and manage the level change
   at the door with a 1:50 ramped screed inside the room. Eats headroom, but works
   as a retrofit.
3. **Linear channel drain** at the far wall with a single-direction 1:50 fall — the
   cleanest look, and easier to keep flush than a centre point-drain that needs a
   four-way fall.

Membrane: full tanking of the wet zone, turned 150 mm up all walls and 1000 mm up
in the spray zone, dressed into the drain flange. Falls: **1:50 (2%) minimum,
1:40 preferred** in the shower zone; ≤1:50 elsewhere so a chair does not drift.

---

## Section 6: Kitchen (Light Touch)

Full A117.1 kitchen compliance is a Tier 2/3 topic. For a house, these are the
high-value, low-cost moves:

| Item | Target | Cost impact |
|---|---|---|
| Clear floor between opposing counters | ≥1015 mm (40 in); **1525 mm (60 in) if the kitchen is U-shaped** (a chair must turn) | Layout only |
| Turning space | 1525 mm circle somewhere in the kitchen | Layout only |
| One work surface at 730–865 mm (29–34 in) AFF | With 685 mm high × 480 mm deep knee clearance | Low — one cabinet run left open or a removable base |
| Sink | Rim ≤865 mm; shallow bowl (≤165 mm deep) so knees fit under; insulate the trap | Low |
| Tap | Single lever, pull-out spray | Trivial |
| Hob | Front or side controls (**never** controls behind the burners — reaching over a flame from a seated position is a burn injury waiting to happen); staggered burners | Trivial at spec stage |
| Oven | Wall oven at 760–860 mm with an adjacent landing surface, side-hinged door preferred | Moderate |
| Storage | Pull-out drawers instead of deep base cupboards; **D-pull handles**, not knobs; one full-extension pantry pull-out | Low |
| Reach | Keep daily-use items in the 380–1220 mm (15–48 in) band | Free |
| Outlets | On the front face of the counter apron, or 460 mm AFF on the wall | Trivial |

---

## Section 7: Hardware, Controls and Lighting

### 7.1 The closed-fist test

**Every control must be operable with one hand, with a closed fist, without tight
grasping, pinching, or twisting the wrist. Maximum force 22 N (5 lbf).**

| Passes | Fails |
|---|---|
| Lever door handles | Round door knobs |
| D-pull cabinet handles | Small knobs, recessed finger cups |
| Single-lever mixer taps | Twin cross-head/pillar taps |
| Rocker light switches | Small toggle/dolly switches, dimmer twist knobs |
| Push-button / touch controls | Key-operated devices, tight thumb-turns |
| Loop-pull window handles | Standard casement twist catches |

This is the cheapest whole-house accessibility upgrade that exists — at
specification stage, lever hardware costs roughly the same as knobs.

### 7.2 Mounting heights (residential, aging-in-place tuned)

| Control | Standard local practice | Accessible target |
|---|---|---|
| Light switch | ~1370 mm (4'-6") | **1015–1220 mm (40–48 in)**; 1120 mm is a good single answer |
| Power outlet | 305 mm (12 in) | **460 mm (18 in)** min AFF to the *bottom* of the box |
| Thermostat / AC control | Wherever | ≤1220 mm (48 in) |
| Door hardware | ~1000 mm | 865–1220 mm — already fine |
| Window operator | Wherever | ≤1220 mm forward reach |
| Consumer unit / breaker panel | High | ≤1220 mm to the highest breaker |
| Intercom / doorbell / video panel | Varies | 865–1220 mm |
| Curtain/blind controls | Cord | Motorised or wand at ≤1220 mm |

### 7.3 Reach ranges (memorise these two)

- **Forward, unobstructed: 380–1220 mm (15–48 in) AFF.**
- **Side, unobstructed: 380–1220 mm (15–48 in) AFF.**

That covers virtually every residential control (switches, outlets, thermostats,
window operators, D-pulls). The obstruction-adjusted variants (reach over a
counter apron or similar deep obstruction, forward vs side, by obstruction depth)
are a Tier 2/3 commercial-fixture concern — full table in Section 11.3.

### 7.4 Lighting and contrast (low-cost, high-impact for aging eyes)

A 60-year-old needs roughly **2×** the light of a 20-year-old for the same task; an
80-year-old around 3×.

- Task lighting at the kitchen counter, stair, bathroom mirror, and reading chair —
  do not rely on a single ceiling point.
- Stair lighting: switched at **both** top and bottom, and light the treads without
  glare into the descending eye.
- Night route: low-level LED strip / motion sensors from bedroom → bathroom. This
  single intervention prevents a large share of elderly night falls.
- Contrast: aim for a **Light Reflectance Value (LRV) difference ≥30 points**
  between (a) door leaf vs wall, (b) switch plate vs wall, (c) sanitaryware vs wall
  and floor, (d) grab bar vs wall, (e) stair nosing vs tread, (f) counter edge vs
  counter face. White sanitaryware on white tile in a white room is functionally
  invisible to a low-vision user.
- Avoid: high-gloss floors (read as wet/slippery), busy high-contrast floor patterns
  (read as level changes), and mirrors facing a doorway.

---

## Section 8: Aging in Place and Future-Proofing

The Tier 1 house should assume its occupants will get older in it. These are the
cheap-now / impossible-later items.

### 8.1 Grab-bar blocking (do this in EVERY bathroom, always)

```
Continuous 19 mm plywood backing (or a 100 × 50 timber noggin run, or in
Pakistani block/brick construction, a full-height solid-grouted band) at:
  · 810–970 mm AFF band, minimum 200 mm tall — covers the 33–36 in grab-bar zone
  · around the WC: rear wall full width + side wall 1200 mm from rear wall
  · around the shower/bath: all wet-zone walls, full length
  · beside the basin
Load target: any 100 mm-wide point on that band must take 1.1 kN (250 lbf).
```

Cost at construction: negligible. Cost later: opening tiled walls. **Never omit
this because "they don't need bars yet".** Note also: suction-cup grab bars are
not grab bars — they are a fall waiting to happen and must never be specified.

### 8.2 Stairs (make the existing stair as safe as it can be)

An accessible route never uses stairs — but the house has them anyway.

**These are comfort/safety targets, not a legal minimum for this stair.** The
table below borrows its riser/tread/nosing numbers from ADA §504 commercial
accessible-stair figures because they happen to be safer and more comfortable
than a bare code minimum — they are **not** what Pakistani residential stairs are
legally required to meet. The actual governing residential rule is the local
BCP/byelaw stair clause (see `architecture-building-codes-permits`), which
permits a taller riser and shorter tread than an ADA commercial stair. Use this
table as the aging-in-place upgrade target when the client wants it; do not tell
a contractor or authority reviewer that these numbers are "the code."

| Element | Comfort/safety target (voluntary upgrade, not a code minimum) |
|---|---|
| Riser | Uniform, 102–178 mm (4–7 in); 150–175 mm typical residential |
| Tread (going) | Uniform, ≥279 mm (11 in) |
| Riser + 2×going | 600–640 mm (comfort rule) |
| Open risers | Avoid — a toe/cane catches |
| Nosing | ≤38 mm (1.5 in) projection, curved or bevelled underside; no square overhang |
| Handrail | **Both sides**, 865–965 mm above nosing, continuous |
| Handrail extension | 305 mm horizontal beyond top riser; one tread depth + 305 mm at bottom |
| Handrail grip | 32–51 mm dia circular; 38 mm clear of wall; returns to wall at ends |
| Nosing contrast | 50–65 mm contrasting strip on tread edge, LRV difference ≥30 |
| Winders | Avoid on the primary stair; if unavoidable, ≥125 mm going at the narrow end |
| Landing | At least every 16 risers |

For the legally binding riser/tread/headroom envelope for a Pakistani residential
stair, use `architecture-stairs-vertical-circulation` and
`architecture-building-codes-permits` — do not derive a compliance claim from
this table.

### 8.3 Main-floor bedroom / convertible room

Provide one main-floor room of **≥3.0 × 3.6 m (10 × 12 ft) usable**, adjacent or
near the accessible bathroom, that can serve as a study/guest room now and a
bedroom later. Give it a 915 mm door, a window with a sill ≤1100 mm for outlook
from a bed, and a data + power outlet cluster at 460 mm on two walls.

### 8.4 Future lift / stairlift provision

- **Stacked closets:** align a 1525 × 1525 mm (5 × 5 ft) closet on the ground and
  first floors, with a removable (non-structural) floor panel between. That is a
  future residential lift shaft for the cost of drawing it in the right place.
- **Stair geometry:** a straight-flight stair ≥915 mm wide takes a cheap straight
  stairlift; a curved/winder stair needs a bespoke rail at 3–5× the cost. Prefer
  straight flights.
- **Power:** run a spare 20 A circuit and a conduit to the stacked-closet location.
- **Structure:** if a lift is plausible, tell the engineer at design stage — the
  pit and the header beam are trivial to design in, invasive to add.

### 8.5 Other future-proofing

- Level or minimal-fall garage/porch slab → the second zero-step route.
- Wide-format switches and pre-wiring for voice/smart control.
- Bedroom-to-bathroom route: keep it ≤6 m, straight, and unobstructed.
- Doorways on the **first** floor also at 915 mm where it costs nothing.
- Reinforce one ceiling area over the primary bed and over the WC for a possible
  ceiling track hoist (flag to the engineer: ~1.5 kN point load with impact).

---

## Section 9: Cost Orientation — Illustrative Only

> **DO NOT put these numbers in a client estimate.** They are **US 2026 market**
> figures, useful only as order-of-magnitude and for relative comparison between
> options. For a real Pakistani estimate, derive quantities from the design and
> price them with `architecture-cost-estimation-boq` against current local rates.

| Item | US 2026 illustrative range | Relative cost signal |
|---|---|---|
| Wheelchair ramp, timber | USD 100–150 / linear ft installed | Cheapest built ramp |
| Wheelchair ramp, aluminium modular | USD 150–250 / linear ft | Removable, often permit-free |
| Wheelchair ramp, concrete | USD 300+ / linear ft | Permanent, highest |
| Typical whole ramp project | USD 1,500–5,000 | — |
| Handrails on a ramp | + USD 20–50 / linear ft | ~15–25% of ramp cost |
| Permit fees (ramp) | USD 50–300 | Local authority equivalent applies |
| Widen a doorway, non-structural | USD 600–1,200 | — |
| Widen a doorway, typical | USD 1,200–3,000 | — |
| Widen a doorway in a load-bearing wall (new header) | up to USD 6,000 | **~5× the non-structural case** |
| Curbless / walk-in shower conversion (32×60) | USD 6,000–12,000 | — |
| Full accessible bathroom remodel | USD 8,000–25,000 (mid-scope ≈ 8,400) | — |
| Grab-bar blocking at construction | ≈ 0 | vs USD 300–800 each to retrofit into tiled walls |
| Lever hardware vs knobs at spec stage | ≈ 0 | The free win |

**The ratio that matters and does transfer across markets:** designing the triad in
at plan stage costs **roughly 0–1.5% of build cost**; retrofitting the same three
things into a finished house costs **roughly 15–40× more** and often cannot achieve
the same result at all. Lead with this ratio, not with a currency figure.

**Re-scaling method for a local estimate:** decompose each item into
material + labour + plant, price materials at local market rate, price labour at
local daily wage × the crew-days implied, and never scale a foreign total by a
single exchange-rate or PPP factor — the labour/material ratio differs too much
(US ≈ 60/40 labour-heavy; Pakistan ≈ 25/75 material-heavy). A Pakistani ramp is
proportionally *cheaper* than a US one; a Pakistani imported thermostatic shower
valve is proportionally *more expensive*.

---

## Section 10: FreeCAD Modelling and Verification

Pair with `architecture-freecad-bim` for the modelling mechanics. This section is
the accessibility-specific verification you run **inside** the model.

### 10.1 Model doors by clear opening, not by leaf

Parametrise the check, do not eyeball it:

```
clear_width = rough_opening − frame_jamb_both_sides − leaf_thickness − stop_projection
            ≈ leaf_width − 60 to 100 mm  (side-hung, 90° open, standard butt hinges)
            ≈ rough_opening − 25 mm      (pocket / sliding)
            ≈ leaf_width − 15 to 25 mm   (swing-clear / offset hinges)

ASSERT clear_width ≥ 815 mm for every main-floor door on the accessible route.
```

Store `clear_width` as a spreadsheet-driven property on each `Arch Window`/door so
the check is re-run every time a leaf size changes, rather than being verified once
and silently broken later.

### 10.2 Turning-circle clash test (the useful trick)

Drop a **Part Cylinder, radius 762.5 mm (Ø1525 mm), height 500 mm**, at floor level
in each room the wheelchair user must turn in. Run a boolean intersection / clash
check against the wall and fixture solids. Any non-empty intersection = the turning
space fails. Repeat at 1675 mm diameter for a power chair.

Do the same with a **760 × 1220 × 500 mm box** for parked clear floor space at each
fixture, appliance, and control.

### 10.3 Route sweep test

Model the accessible route as a swept solid: a **915 mm wide × 2030 mm high**
profile swept along the route polyline from the street/driveway through the entry,
hall, accessible bathroom, and main-floor bedroom. Clash it against everything.
This catches, in one operation: narrow halls, protruding objects between 685 and
2030 mm, door swings, under-stair head strikes, and radiator/AC-unit intrusions.

### 10.4 Ramp modelling checklist

- Model the ramp as a real sloped `Arch Structure`, not a flat slab with a note.
- Verify slope numerically: `rise / run ≤ 1/12` (0.08333) — do not trust the view.
- Model landings as separate flat solids and confirm each is ≥1525 × 1525 mm.
- Model handrails as real swept solids at 865–965 mm above the *sloped* surface,
  including the 305 mm horizontal extensions — the extensions are what get omitted.
- Model the 50 mm edge curb.
- Verify the ramp footprint against the authority setback line (Reality Check #3).

### 10.5 Level and threshold audit

Query every `Arch` floor/slab object's Z placement along the route. Any Δ >13 mm
between adjacent route surfaces is a defect. Report the list, do not fix silently.

### 10.6 Deliverable labelling

Every exported view, plan, or render from this workflow gets:
`PRELIMINARY — NOT FOR CONSTRUCTION — accessibility dimensions per ADA/A117.1 guidance,
not a compliance certification — requires licensed architect/engineer review and
local authority approval.`

---

## Section 11: CONDENSED FULL-COMPLIANCE REFERENCE

> **Load this section only for Tier 2 / Tier 3** (4+ dwelling units, commercial or
> institutional use, or a contractual compliance requirement). It is deliberately
> compressed; for a real compliance project, go to the primary documents and engage
> an accessibility consultant. Do not apply this section to a family house.

### 11.1 What legally applies where (US framing, the source of most numbers)

| Building | Governing instrument | Applies? |
|---|---|---|
| Private detached single-family home | none (IRC 2021 has no accessibility chapter) | **No** — unless a local visitability ordinance or the client requires it |
| Multifamily, 4+ dwelling units | **Fair Housing Act** + ICC A117.1 **Type B** | Yes |
| Group R-2, 4+ storeys with elevator | ICC A117.1 **Type A** in ≥2% of units | Yes |
| Public accommodation / commercial | **ADA 2010 Standards for Accessible Design** | Yes |
| Federally funded facility | **ABA Standards** | Yes |

Key trigger thresholds: **Type B** = adaptable, required in residential buildings
with **4+ dwelling/sleeping units** (the FHA/A117.1 coordinated minimum).
**Type A** = fully accessible, required in **2% of units in Group R-2 buildings of
4+ storeys with elevator service**.

### 11.2 Primary citations to pull when you need real depth

| Topic | Citation |
|---|---|
| Accessible routes, general | ADA 2010 Standards Ch. 4, §§402–406; A117.1-2017 Ch. 4 |
| Doors and doorways | ADA §404; A117.1-2017 §404; HUD FHA Design Manual **Ch. 3** (Usable Doors) |
| Ramps | ADA §405; A117.1-2017 **§405** |
| Route into and through a covered unit | HUD FHA Design Manual **Ch. 4** |
| Turning space / clear floor space | A117.1-2017 **§304**, §305 |
| Route width incl. 48 in exterior | A117.1-2017 **§1003** |
| Water closets, grab bars, lavatories | ADA 2010 Ch. 6, §§603–609; A117.1-2017 **§603** |
| Bathrooms / reinforced walls in covered units | HUD FHA Design Manual **Ch. 7** |
| Type A / Type B dwelling units | A117.1-2017 Ch. 10 (Type A §1003, Type B §1004) |
| Reach ranges | ADA §308 |
| Signage | ADA §703 |
| Elevators | ADA §407; ASME A17.1 |
| Classroom acoustics | ANSI S12.60 |
| Hearing induction loops | IEC 60118-4 |
| Playground surfacing | ASTM F1292 (impact), ASTM F1951 (wheelchair access) |

### 11.3 Compressed dimensional table (commercial/institutional)

| Element | ADA 2010 requirement |
|---|---|
| Clear floor space | 760 × 1220 mm (30 × 48 in); alcove >380 mm deep → widen to 915 mm (forward) / lengthen to 1525 mm (parallel) |
| Turning space | Ø1525 mm, or T-shape 1525 × 1525 with 915 mm arms and 610 mm base |
| Accessible route width | 915 mm continuous; passing space 1525 mm at ≤61 m intervals |
| Door clear width | 815 mm (32 in) |
| Ramp | 1:12 max; 760 mm max rise/run; 915 mm min width; 1525 × 1525 landings; handrails both sides 865–965 mm with 305 mm extensions; 50 mm edge protection |
| Stairs | Riser 102–178 mm; tread ≥279 mm; no open risers; handrails both sides 865–965 mm |
| Elevator cab | 1370 × 1730 mm centre-opening, or 1370 × 1295 mm side-opening; door ≥915 mm; car controls ≤1220 mm forward / ≤1370 mm side reach; reopening device sensing 127–635 mm AFF; audible + visual position indicators |
| Accessible toilet room | Ø1525 turning; WC centreline 405–455 mm (16–18 in); seat 430–485 mm; side bar ≥1065 mm at 840–915 mm AFF, ≤305 mm from rear wall; rear bar ≥915 mm (36 in; the 610 mm/24 in figure is a tank-type-WC exception only); lavatory rim ≤865 mm with 685 mm knee / 230 mm toe clearance; mirror bottom ≤1015 mm |
| WC compartment | 1525 × 1525 mm (wall-hung WC) or 1525 × 1420 mm (floor-mounted); door ≥815 mm, out-swing or sliding |
| Ambulant WC compartment | 915 mm wide × 1525 mm deep; grab bars both sides at 840–915 mm; self-closing out-swing door |
| Roll-in shower | 1525 × 760 mm (or 915 × 915 mm alt); ≤13 mm bevelled threshold; folding seat 460 × 610 mm at 430–485 mm; hand shower on 1525 mm hose; offset lever controls |
| Transfer shower | 915 × 915 mm; seat opposite controls; 1220 × 915 mm clear floor at the open side; L-shaped grab bars |
| Reach — forward | 380–1220 mm unobstructed; 1120 mm over a 510–635 mm deep obstruction |
| Reach — side | 380–1220 mm unobstructed; 1370 mm over a ≤255 mm obstruction; 1170 mm over 255–610 mm |
| Signage | Raised chars 16–51 mm, uppercase sans-serif, raised ≥0.8 mm; Grade 2 Braille below; centreline of topmost tactile char at 1220 mm AFF; on latch side, ≥460 mm from the 90°-open door |
| Protruding objects | ≤100 mm projection between 685–2030 mm AFF |

**Accessible parking counts (ADA):**

| Total spaces | Min accessible | | Total spaces | Min accessible |
|---|---|---|---|---|
| 1–25 | 1 | | 201–300 | 7 |
| 26–50 | 2 | | 301–400 | 8 |
| 51–75 | 3 | | 401–500 | 9 |
| 76–100 | 4 | | 501–1000 | 2% of total |
| 101–150 | 5 | | >1000 | 20 + 1 per 100 over 1000 |
| 151–200 | 6 | | | |

Space 2440 mm wide + 1525 mm access aisle; van space 2440 + 2440 aisle **or**
3505 + 1525; 1 van space per 6 accessible spaces; vertical clearance 2490 mm on
the van route; ISA signage ≥1525 mm above ground.

### 11.4 Sensory accessibility (condensed)

**Vision:**
- Tactile Ground Surface Indicators — warning (truncated domes, 5 mm high, 25 mm
  dia, 50–60 mm centres) 300–600 mm deep at stair heads, crossings, platform edges,
  ramp bases; directional (bars aligned to travel) ≥400 mm wide across open space.
- Stair nosing contrast strip 50–65 mm on tread, LRV difference ≥30.
- LRV difference ≥30 (BS 8300) between door/wall, leaf/frame, fixture/wall,
  handrail/wall, sign/background.
- Tactile + Braille at room IDs, exits, stair-landing floor numbers, lift controls.
- Emergency alarm audible ≥75 dBA, or ambient +15 dBA.

**Hearing:**
- Induction loops (IEC 60118-4) in auditoria, worship spaces, counters, meeting
  rooms; field strength −400 to +400 mA/m at 1 kHz; signed with the ear+T symbol.
- Visual alarm devices ≥75 cd in rooms up to 6.1 × 6.1 m; flash 1–3 Hz,
  synchronised to avoid photosensitive seizure; mounted 2030 mm AFF or 150 mm
  below ceiling, whichever is lower.
- Acoustics: RT60 ≤0.6–0.8 s classrooms, ≤0.5–0.6 s small meeting rooms;
  background ≤35 dBA classrooms (ANSI S12.60), ≤40 dBA offices; speech S/N ≥ +15 dB.
- Assistive listening for ≥4% of seats (IBC), minimum 2 systems.

**Neurodiversity (~15–20% of population):** one low-stimulation quiet room per
floor in public buildings, ≥9 m², away from noise; consistent wayfinding
vocabulary; clear sightlines from decision points; LED drivers >100 Hz to kill
visible flicker; mechanical noise NC 25–30; matte surfaces; avoid high-contrast
geometric floor patterns (read as level changes).

**Changing Places / adult changing facility** (BS 8300, Changing Places
Consortium): ≥12 m² (3.0 × 4.0 m); ceiling track hoist covering WC + bench + clear
floor; height-adjustable adult bench 1800 × 900 mm adjustable 600–1000 mm;
peninsular WC ≥1000 mm from the nearest wall; ≥1000 mm clear door.

### 11.5 Universal design — Ron Mace's 7 principles (condensed)

Center for Universal Design, NC State, 1997. Codes are minimums; these are the
design intent behind them.

| # | Principle | One-line architectural test |
|---|---|---|
| 1 | **Equitable use** | Does everyone use the *same* entrance and the *same* route? A separate "accessible entrance" at the back passes code and fails this. |
| 2 | **Flexibility in use** | Does it work left- and right-handed, fast and slow, standing and seated? (lever handles, dual push-plate + pull) |
| 3 | **Simple and intuitive** | Can a first-time visitor with no shared language find the way without signage? |
| 4 | **Perceptible information** | Is every essential message delivered in ≥2 modes — visual, tactile, audible? |
| 5 | **Tolerance for error** | What happens when someone misjudges? (contrasting nosings, slip-resistant wet-area floors, door closers, edge protection) |
| 6 | **Low physical effort** | Neutral body position, ≤22 N operating force, no repetitive strain, minimal sustained effort. |
| 7 | **Size and space for approach and use** | Clear sightlines, comfortable reach, adequate clear floor for an assistive device or an assistant — seated or standing. |

### 11.6 International comparison (when the project is not in the US)

| Requirement | ADA (US) | BS 8300 / ADM (UK) | DIN 18040 (DE) | AS 1428 (AU) | NBC 2016 (IN) |
|---|---|---|---|---|---|
| Route clear width | 915 mm | 1000–1200 mm | 1200 mm | 1000–1200 mm | 1200 mm |
| Turning space | Ø1525 mm | Ø1500 mm | Ø1500 mm | Ø1540 mm | Ø1500 mm |
| Ramp max slope | 1:12 | 1:12–1:15 | 1:12 (1:16 preferred) | 1:14 (1:8 short) | 1:12 |
| Door clear width | 815 mm | 800–850 mm | 900 mm | 850 mm | 900 mm |
| WC grab bar height | 840–915 mm | 680–700 mm* | 850 mm | 810–830 mm | ~800 mm |
| Parking space width | 2440 mm | 2400 mm+ | 3500 mm | 2400 mm | 3600 mm |
| Applies to private dwellings? | No | **Yes** — Part M M4(1)/M4(2)/M4(3) | Yes — DIN 18040-2 | Via NCC, limited | Via RPwD Act 2016, enforcement gap |

(*UK grab bars are measured to a different reference and are set from different
user research — do not mix UK and US grab-bar heights in one drawing set.)

**UK Part M dwelling categories are the most directly useful foreign framework for
residential work:** M4(1) *visitable* ≈ this skill's Tier 1; M4(2) *accessible and
adaptable* ≈ Tier 1+ / A117.1 Type B; M4(3) *wheelchair user dwelling* ≈ A117.1
Type A. If a client asks "how accessible should the house be?", offering these
three named tiers is a faster conversation than reciting dimensions.

**Pakistan:** there is no residential accessibility chapter in the Building Code of
Pakistan. Accessibility clauses, where they exist, sit in development-authority
byelaws (LDA/CDA/SBCA) and mostly cover public buildings. For residential work,
Tier 1 in this skill *is* the standard — there is nothing local to comply with, so
the design intent has to come from the designer. Say this plainly rather than
implying a Pakistani code requirement exists.

---

## Section 12: Common Failures and Final Checklist

### 12.1 The failure list (what actually goes wrong on houses)

1. **Specifying a 2'-6" (762 mm) interior door** because it is the local default —
   gives ~680 mm clear, fails by 135 mm. The single most common defect.
2. **Measuring the door leaf instead of the clear opening.** A "3-foot door" that
   is really a 3-foot *rough opening* gives ~840 mm; a 3-foot *leaf* gives ~815 mm;
   a 3-foot opening with a thick frame can drop below 815 mm.
3. **A ramp with no landing** at the top, so the user must hold position on the
   slope while operating the door.
4. **An in-swinging bathroom door** eating the clear floor space — and trapping a
   fallen occupant.
5. **A 915 mm hallway turning 90° into a 915 mm door.** Geometrically fails; needs
   1065–1220 mm at the turn.
6. **Grab bars screwed into plasterboard or hollow block** with no blocking —
   they pull out under load, causing exactly the fall they were meant to prevent.
7. **Polished tile in the accessible bathroom.** Specify PTV ≥36 / R10–R11.
8. **A curbless shower decided after the slab is cast** — then either a 50 mm lip
   appears or the whole floor is raised and headroom is lost.
9. **Uninsulated lavatory P-trap and hot supply** burning a seated user's legs.
10. **Hob controls behind the burners.**
11. **Zero-step entry with no drainage** → water enters the house → the owner adds
    a step back → accessibility lost.
12. **Ramp built into the mandatory setback** without checking the byelaw, then
    ordered removed.
13. **Claiming "ADA compliant"** on a private house. It is neither required nor
    something this skill can certify.

### 12.2 Tier 1 sign-off checklist

```
ENTRY
[ ] ≥1 zero-step entrance, threshold ≤13 mm, bevelled above 6 mm
[ ] Approach route ≤1:20, or a compliant 1:12 ramp with landings + handrails
[ ] Route clear width ≥915 mm (1220 mm preferred), cross slope ≤1:48
[ ] Slot drain outside the flush threshold + ≥1200 mm canopy
[ ] Ramp (if any) clears the authority setback line

CIRCULATION
[ ] Every main-floor door leaf ≥915 mm → verified clear width ≥815 mm
[ ] 460 mm latch-side clearance + 1525 mm depth on the pull side of key doors
[ ] Hallways ≥915 mm; ≥1065 mm at any 90° turn into a door
[ ] No protruding object >100 mm between 685–2030 mm AFF on the route
[ ] Zero interior thresholds; carpet pile ≤13 mm; no loose rugs on the route

BATHROOM (main floor)
[ ] Internal clear ≥1525 × 1525 mm, or an accepted 915 × 1525 mm parallel layout
[ ] Door out-swings or slides; 915 mm leaf
[ ] WC centreline 405–455 mm (16–18 in) from side wall/partition; seat 430–485 mm
[ ] 760 × 1220 mm transfer space beside the WC
[ ] Grab bars: side ≥1065 mm + rear ≥915 mm (36 in; 610 mm only for the tank-type-WC exception), both at 833–915 mm AFF
[ ] Blocking behind ALL bathroom walls in the 810–970 mm band, 1.1 kN capable
[ ] Basin rim ≤865 mm; knee 685 mm / toe 230 mm clearance; trap insulated
[ ] Curbless shower 1525 × 915 mm, linear drain, 1:50 fall, membrane 150 mm up
[ ] Slip-resistant floor PTV ≥36 / R10–R11; thermostatic anti-scald valve

FIXTURES AND CONTROLS
[ ] Lever handles / D-pulls / single-lever taps / rocker switches throughout
[ ] Switches 1015–1220 mm; outlets ≥460 mm; breaker panel ≤1220 mm
[ ] All daily-use items land in the 380–1220 mm reach band
[ ] LRV difference ≥30 at door/wall, fixture/wall, grab bar/wall, stair nosing

FUTURE-PROOFING
[ ] Main-floor bedroom or convertible room ≥3.0 × 3.6 m
[ ] Stacked 1525 × 1525 mm closets for a future lift + spare circuit + conduit
[ ] Straight-flight stair ≥915 mm, handrails both sides with 305 mm extensions
[ ] Night-route low-level lighting bedroom → bathroom

MODEL AND DELIVERABLE
[ ] FreeCAD Ø1525 mm turning-cylinder clash test passed in every required room
[ ] 915 × 2030 mm route sweep clash test passed end to end
[ ] Every ramp verified numerically at ≤1/12, landings ≥1525 × 1525 mm
[ ] Output labelled PRELIMINARY — NOT FOR CONSTRUCTION
[ ] Structural implications of any widened opening / lift pit / hoist flagged to
    the engineer, in writing
```

---

*This skill is design guidance for single-family residential accessibility. It does
not certify compliance with any code. Tier 2 and Tier 3 projects require a
qualified accessibility consultant and the primary standards documents. Every
built design requires a licensed engineer's/architect's stamp and local authority
approval before construction.*
