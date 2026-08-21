---
name: architecture-stairs-vertical-circulation
description: >
  Stair and vertical circulation design for houses — riser/tread proportioning
  by the Blondel 2R+T rule, code minimum/maximum riser, tread, width, headroom
  and handrail dimensions (IRC 2021, IBC 2021, NBC India 2016, with an explicit
  Pakistan/BCP gap statement), the straight vs L vs U vs winder vs spiral
  selection tree for tight residential plans, winder walkline geometry with
  derived minimum turning radii, spiral stair dimensional envelopes and use
  cases, RCC waist-slab structural detailing (thickness by ACI 318-19
  Table 7.3.1.1 and IS 456 Cl. 33, load take-down, flexural design, bar
  schedules, re-entrant corner detail), handrail and guard structural loads
  per ASCE 7-22 §4.5, and FreeCAD modelling defaults. Includes fully worked
  numeric examples for a 5-marla G+1 house.
---

# Stairs and Vertical Circulation for Houses

This skill is the **stair set-out, code-check and preliminary structural sizing aid** for house-scale vertical circulation — the single stair (occasionally two) that connects ground to first to roof in a 3, 5, 10 marla or 1 kanal house, or its equivalent elsewhere. It exists so that a stair drawn in FreeCAD has a *real* riser count derived from the actual floor-to-floor height, a tread that satisfies both the comfort formula and a code minimum, a floor opening long enough to give real headroom, a waist slab thickness that came from a span/depth rule rather than a guess, and a handrail whose posts have been checked against an actual load. Every number below is either a cited code limit, a derived geometric result, or a labelled rule of thumb.

**Stairs are the single most dimension-sensitive element in a house plan.** Get the riser count wrong by one and every landing level, every door head, and the floor opening are wrong. Get the headroom wrong and the mistake is only discovered when someone hits their head on a poured slab. Unlike a wall, a stair cannot be adjusted by 50 mm after the fact.

---

## Reality Check - Licensing & Liability

**This skill produces design aids and calculation guidance for planning and FreeCAD modelling ONLY.**

- Every dimension, thickness, bar size and load figure here is a **preliminary set-out figure, a code minimum, or a rule of thumb**. A stair is a structural element that carries people at height; a preliminary number is not a design.
- **Any stair intended for actual construction in a real occupied building MUST be reviewed, analysed and stamped by a licensed structural engineer** — in Pakistan a **PEC-registered (Pakistan Engineering Council) Professional Engineer** in the relevant structural category; elsewhere the equivalent locally licensed or chartered structural engineer. This applies to the waist slab, the landing slab, the landing beams, the supporting walls or columns, and the handrail/guard anchorage.
- **The design MUST also go through local authority plan approval before construction** — LDA (Lahore), CDA (Islamabad), RDA (Rawalpindi), SBCA (Karachi), DHA, PDA, GDA, or the relevant TMA/Cantonment Board. Stair width, headroom, mumty, and stair enclosure are byelaw items in most Pakistani authorities and are **separate from and additional to** any structural code.
- **Claude / Claude must never present FreeCAD stair geometry, a riser schedule, a waist-slab thickness, or a bar layout from this skill as construction-ready.** The correct framing is always: *"preliminary stair set-out and sizing for coordination — to be verified and stamped by a PEC-registered structural engineer and approved by the local authority."*
- **Say this unprompted.** If a user starts treating the output as final — asks for a bar bending schedule to hand a steel fixer, asks "how many bags of cement for the stair", says the shuttering is going up this week, asks to shave the waist slab "because it looks thick", or asks whether they can skip the landing beam — **stop and state the licensing requirement explicitly before continuing.** Do not wait to be asked.
- **Never certify.** Do not produce anything resembling a stamped drawing, a structural stability certificate, or an engineer's signature block. Do not put a PEC number on output.
- **Handrails and guards are a life-safety element, not a finish.** A guard that fails at 900 mm above a stairwell drops someone onto a concrete floor. The ASCE 7-22 §4.5 loads in Section 9 are the *minimum* check; the anchorage detail into a 150 mm waist slab must be verified by the engineer, not assumed from a bracket manufacturer's catalogue.
- **Pakistan-specific gap, stated up front:** a clause-level residential stair provision from the **Building Code of Pakistan (BCP 2007 / BCP 2021 draft)** could not be independently verified for this skill (see §3.3 and §20). Where this skill gives a numeric limit it is drawn from **IRC 2021** (the most widely adopted residential numeric baseline, commonly cross-referenced by Pakistani practitioners) and **NBC India 2016 / IS 456:2000** as a regional cross-check. **Every one of those numbers must be confirmed against the Authority Having Jurisdiction before use in Pakistan.** Say so when producing output for a Pakistani project.
- **IRC clause-level citations in this skill were spot-checked, not exhaustively re-derived from the primary code text.** Two numeric errors were found and corrected during review (the spiral-stair walkline tread minimum in §8.1/§8.2, and the R312.1.2 guard-height exception that applies specifically to stairs vs. landings — see §3.1 and §9.1). Treat every clause number and figure in this skill as **a starting point for verification against the current IRC/IBC text, not a substitute for it** — do not let the specificity of a clause citation (e.g. "R311.7.5.1") read as proof it has been checked character-for-character.

---

## Section 1: The Set-Out Algorithm (run this first, every time)

Do not draw a stair before running these eight steps in order. Most stair errors are an out-of-order design: someone drew a stair shape, then tried to fit risers into it.

```
STEP 1 — Get the true floor-to-floor height H.
    H = FINISHED floor level (lower) to FINISHED floor level (upper).
    NOT slab top to slab top. Include:
      + upper structural slab thickness
      + upper floor screed + tile/wood finish
      − lower floor finish thickness
    If the two floors get DIFFERENT finishes, H is not the structural dimension.
    → The single most common site error is measuring slab-to-slab and ending up
      with a first or last riser 15-25 mm off from all the others.

STEP 2 — Choose a target riser R_target and get the riser count n.
    R_target = 175 mm (comfortable house default; 165 mm for aging-in-place)
    n = round(H / R_target)          → n must be an INTEGER
    R = H / n                        → the ACTUAL riser, to 0.1 mm

STEP 3 — Check R against the governing code cap.
    R ≤ 190 mm  (NBC India, one/two-family dwellings) — use as the Pakistan default
    R ≤ 196 mm  (IRC 2021 R311.7.5.1, 7-3/4 in absolute cap)
    If R exceeds the cap, increase n by 1 and recompute.

STEP 4 — Derive the tread T from the Blondel comfort band.
    T = 630 − 2R          (target 2R + T = 630 mm)
    Round T DOWN to the nearest 5 mm, then re-check 2R + T ∈ [600, 650].
    Check T ≥ 250 mm (NBC dwellings) and T ≥ 254 mm (IRC, 10 in with nosing).

STEP 5 — Compute the total going (horizontal run) of a straight flight.
    Going = (n − 1) × T
    (n risers, n−1 treads — the top "tread" IS the upper floor.)

STEP 6 — Test the going against the available plan length.
    Fits with ≥ 900 mm landing at each end? → straight flight, done.
    Doesn't fit? → go to Section 7 selection tree (L / U / winder / spiral).

STEP 7 — Run the headroom / floor-opening check (Section 4.2).
    This determines how LONG the hole in the upper floor must be.
    Skipping this is how you get a 1.8 m soffit over the fourth-from-top step.

STEP 8 — Check flight rules.
    Max vertical rise between landings: 3835 mm (IRC R311.7.3, 151 in)
    Max risers per flight: 12 (NBC India), 16 (Pakistani practice cap)
    Landing depth ≥ 914 mm AND ≥ stair width (IRC R311.7.6)
```

### 1.1 Worked run of the algorithm — H = 3200 mm

| Step | Operation | Result |
|---|---|---|
| 1 | Slab 150 + screed/tile 50 + storey clear 3000 | **H = 3200 mm** |
| 2 | n = round(3200 / 175) = 18.29 → 18 | R = 3200/18 = **177.8 mm** |
| 3 | 177.8 ≤ 190 ✓, ≤ 196 ✓ | pass |
| 4 | T = 630 − 355.6 = 274.4 → **275 mm**; 2R+T = 630.6 | pass (≥250, ≥254) |
| 5 | Going = 17 × 275 | **4675 mm** |
| 6 | Available plan length 3600 mm | **FAILS → dogleg (Section 7)** |
| 7 | Floor opening (Section 4.2) | see §4.2 worked example |
| 8 | Split 9 + 9 risers; rise/flight = 1600 mm ≤ 3835 ✓; 9 ≤ 12 ✓ | pass |

**The lesson embedded in this example:** a 3200 mm floor-to-floor stair at comfortable proportions needs **4.7 metres of straight run**. Almost no 5-marla house has that. The dogleg is not an aesthetic choice in Pakistani house planning; it is arithmetic.

---

## Section 2: Riser/Tread Proportion — the Blondel 2R+T Rule

### 2.1 The formula and where it comes from

**François Blondel** (French architect, *Cours d'architecture*, 1675) observed that a person's stride shortens as they climb, and that the shortening is roughly twice the rise. The rule:

```
        2R + T = 600 to 650 mm        (24 to 26 in)
        Sweet spot: 2R + T = 630 mm   (~25 in) — "the 63 formula" in metric practice
```

R = riser height, T = tread depth (the *going*, nosing-to-nosing horizontal, **not** including nosing overhang).

The physiological basis: a level pace is ~630 mm; each unit of rise consumes two units of that pace. A person's gait locks into a cadence within about two steps — which is also why the **uniformity rule** (§3.1) matters more than the absolute dimension. A stair with all risers 5 mm too tall is fine. A stair with one riser 15 mm different from the rest is a trip hazard, because the body has already committed to the cadence.

**Blondel is not law.** It is a comfort standard that every code implicitly assumes. Codes set the *outer box*; Blondel picks the point inside the box.

### 2.2 The three companion proportioning rules (cross-check with Blondel)

| Rule | Metric band | Imperial band | Use |
|---|---|---|---|
| **Blondel / pace rule** | 2R + T = 600–650 mm | 24–26 in | Primary. Always check this one. |
| **Product rule** | R × T = 46,000–48,500 mm² | 72–75 in² | Cross-check; catches proportions that pass Blondel but feel wrong at the extremes |
| **Sum rule** | R + T = 430–460 mm | 17–18 in | Quick mental check on site |
| **Pitch angle** | 30°–37° comfortable; 42° absolute domestic max | — | tan θ = R / T |

A proportion that satisfies all three plus a pitch in the 30–35° band is very hard to make uncomfortable.

### 2.3 Riser/tread combination table (all satisfy 2R + T ≈ 630 mm)

| Riser R (mm) | Tread T (mm) | 2R+T | R×T (mm²) | Pitch | Feel | Code status |
|---|---|---|---|---|---|---|
| 150 | 330 | 630 | 49,500 | 24.4° | Very generous — grand stair, public feel | IRC ✓ NBC ✓ — but going is long |
| 160 | 310 | 630 | 49,600 | 27.3° | Generous; excellent aging-in-place | IRC ✓ NBC ✓ |
| **165** | **300** | **630** | **49,500** | **28.8°** | **Aging-in-place / accessible-leaning house default** | IRC ✓ NBC ✓ |
| 170 | 290 | 630 | 49,300 | 30.4° | Very comfortable main stair | IRC ✓ NBC ✓ |
| **175** | **280** | **630** | **49,000** | **32.0°** | **Recommended default for a main house stair** | IRC ✓ NBC ✓ |
| 178 | 275 | 631 | 48,950 | 32.9° | Standard result of an 18-riser / 3200 mm storey | IRC ✓ NBC ✓ |
| 180 | 270 | 630 | 48,600 | 33.7° | Common Pakistani practice; comfortable | IRC ✓ NBC ✓ |
| 185 | 260 | 630 | 48,100 | 35.4° | Steep but acceptable; secondary stair | IRC ✓ NBC ✓ |
| **190** | **250** | **630** | **47,500** | **37.2°** | **Steepest fully-compliant residential stair (NBC dwellings)** | IRC ✓ NBC ✓ (at the cap) |
| 196 | 254 | 646 | 49,800 | 37.6° | IRC absolute limit combination | IRC ✓ **NBC tread ✗** (needs 250 min — passes) — but at both caps simultaneously |
| 196 | 240 | 632 | 47,000 | 39.2° | Blondel-compliant but **illegal** | **IRC ✗** (tread < 254) **NBC ✗** (tread < 250) |
| 200 | 230 | 630 | 46,000 | 41.0° | Blondel-compliant but **illegal everywhere** | **✗ ✗** — this is a ladder, not a stair |

**The trap in the last two rows:** Blondel alone will happily approve a stair that no code allows. Blondel is a *comfort* filter applied **inside** the code box, never instead of it. Always run §3 after §2.

### 2.4 What to do when the ideal tread doesn't fit

Ranked, best first:

1. **Add a riser** (n+1). Reduces R, which *increases* the Blondel-derived T — wrong direction if you're short on run. But it flattens the stair.
2. **Reduce the riser count** (n−1). Increases R, allows a smaller T, shortens the going. Only until R hits the 190/196 mm cap.
3. **Take T to the code minimum** (250 mm NBC / 254 mm IRC) and accept 2R+T slightly below 600. A 178/250 stair gives 2R+T = 606 — tight but legal and walkable.
4. **Add a nosing projection.** A 25 mm nosing gives a 275 mm *effective foot area* on a 250 mm going, at no cost in run. IRC R311.7.5.3 requires a **19–32 mm (3/4–1-1/4 in) nosing** where the tread is less than 279 mm (11 in) deep. **Free comfort — always take it.**
5. **Change the plan type** (Section 7) — winders or a second landing buy run.
6. **Never**: vary the riser height along the flight to "make it fit". That is the 9.5 mm uniformity violation and it is the leading cause of stair falls.

---

## Section 3: Code Dimensional Limits

### 3.1 IRC 2021 §R311.7 — residential stairways (primary numeric baseline)

| Item | Limit | Clause |
|---|---|---|
| **Maximum riser height** | **196 mm (7-3/4 in)** | R311.7.5.1 |
| **Riser uniformity** | Largest − smallest riser in a flight ≤ **9.5 mm (3/8 in)** | R311.7.5.1 |
| **Minimum tread depth** | **254 mm (10 in)** measured nosing-to-nosing | R311.7.5.2 |
| Minimum tread depth, **no nosing** (solid riser stair with vertical riser face) | **279 mm (11 in)** | R311.7.5.3 |
| **Tread uniformity** | Largest − smallest tread in a flight ≤ **9.5 mm (3/8 in)** | R311.7.5.2 |
| **Nosing projection** (required where tread < 279 mm) | **19–32 mm (3/4–1-1/4 in)**, uniform within 9.5 mm | R311.7.5.3 |
| **Minimum clear width** | **914 mm (36 in)** above the handrail height and below the headroom line | R311.7.1 |
| Minimum width **at and below** handrail height | **787 mm (31.5 in)** with one handrail; **686 mm (27 in)** with two | R311.7.1 |
| **Minimum headroom** | **2032 mm (6 ft 8 in)** measured vertically from the sloped nosing line | R311.7.2 |
| **Maximum vertical rise between floor levels or landings** | **3835 mm (151 in)** | R311.7.3 |
| **Landing depth** in direction of travel | **≥ 914 mm (36 in)** and ≥ stair width | R311.7.6 |
| **Handrail height** above nosing line | **864–965 mm (34–38 in)** | R311.7.8.1 |
| **Handrail clearance to wall** | **≥ 38 mm (1-1/2 in)** | R311.7.8.3 |
| **Handrail continuity** | Full length of flight, from a point above the top riser to a point above the lowest riser; required where there are **4 or more risers** | R311.7.8.2 |
| **Open riser opening** (where total rise > 762 mm) | Must not pass a **102 mm (4 in) sphere** | R311.7.5.1 |
| **Guard height**, landings, porches, balconies and other open-sided floor surfaces more than 762 mm above grade/floor below | **≥ 914 mm (36 in)** | R312.1.2 |
| **Guard height, the open side of a stair flight itself** (measured vertically from the line of the tread nosings) | **≥ 864 mm (34 in)** — R312.1.2's own exception for stairs is *lower* than the 914 mm landing/floor minimum; do not apply the 914 mm figure to a stair guard as if it were the code floor | R312.1.2, exception |
| **Guard infill opening** | Must not pass a **102 mm (4 in) sphere**; triangular opening at riser/tread/bottom-rail must not pass a **152 mm (6 in) sphere** | R312.1.3 |
| **Illumination** | Light source at each floor level served; **three-way switching** at top and bottom of an interior stair | R303.7 / R311.7.9 |

**Design practice note:** because a house guard usually runs continuously from the stair flight onto the adjoining landing, this skill's default design value is **1000 mm throughout** — it exceeds both the 864 mm stair-specific minimum and the 914 mm landing minimum, so one consistent detail satisfies both conditions without having to step the guard height up at the landing. Do not let the 1000 mm design default be mistaken for "the code minimum is 1000 mm" — it isn't; it's a margin choice.

### 3.2 IBC 2021 §1011 — commercial (relevant only when it's stricter, or a home office / rental use triggers it)

| Item | IBC limit | Note vs IRC |
|---|---|---|
| Riser | 102–178 mm (4–7 in) | **Stricter** than IRC (196 mm) |
| Tread | ≥ 279 mm (11 in) | **Stricter** than IRC (254 mm) |
| Headroom | ≥ **2032 mm (80 in)** | **Identical to IRC** — this is why 2032 mm is a universally safe floor |
| Width | ≥ 1118 mm (44 in) where occupant load ≥ 50; 914 mm below that | Stricter above 50 occupants |
| Handrail | Both sides; 864–965 mm; extensions required at top and bottom | Stricter than IRC (one side, no extensions) |

**Headroom is the one dimension where residential and commercial codes agree exactly: 2032 mm.** Treat it as a hard physical floor, never a negotiable. Design a house to **2100 mm** so a 50 mm finish change doesn't put you in violation.

### 3.3 South Asian baseline — NBC India 2016 / common Pakistani practice

**[regional cross-check — see the gap statement below]**

| Item | General buildings | **One-/two-family dwellings** |
|---|---|---|
| Minimum tread | 300 mm | **250 mm** |
| Maximum riser | 150 mm (ideal) | **190 mm** |
| Maximum risers per flight before a landing | 12 | **12** |
| Minimum clear width | 1000 mm (residential blocks) | **900 mm** (commonly cited; many Pakistani byelaws require 1000 mm for a main house stair) |
| Headroom | 2100 mm typical requirement | 2100 mm; **never below 2032 mm** |

**Pakistani site practice** (observed, not codified): riser **175–190 mm**, tread **250–280 mm**, clear width **900–1200 mm**, waist slab **125–150 mm**, mumty stair to roof frequently steeper than the main flight — which is a code violation in every framework above and should be called out, not copied.

#### The Pakistan gap — state this in every Pakistani deliverable

> A clause-level residential staircase provision from the **Building Code of Pakistan (BCP 2007 Seismic Provisions, or the BCP 2021 IBC-based draft published by PEC)** could not be independently verified for this skill. The BCP source documents exist (pec.org.pk, urbanunit.gov.pk) but a stair-specific clause number and its numeric limits were not extractable. **The numbers used here are IRC 2021 (primary) and NBC India 2016 (regional cross-check).** They are widely referenced by Pakistani practitioners alongside IS 456 for RCC design, but they are **not** a substitute for the governing byelaw. Confirm stair width, headroom, riser/tread and enclosure requirements against the **LDA / CDA / RDA / SBCA / DHA / TMA byelaw** for the specific plot before submission.

### 3.4 Which limit governs — merged worst case

When designing without a confirmed local byelaw, design to the **envelope of the strictest value** you might face:

| Parameter | Safe design value (satisfies IRC + NBC-dwelling + typical byelaw) |
|---|---|
| Riser | **≤ 180 mm** (design 175) |
| Tread | **≥ 275 mm** (design 275–280) |
| Clear width | **≥ 1000 mm** (design 1050–1100 for a main stair) |
| Headroom | **≥ 2100 mm** (never below 2032) |
| Risers per flight | **≤ 12** |
| Landing depth | **≥ stair width, and ≥ 1000 mm** |
| Handrail height | **900 mm** (mid-band of 864–965) |
| Guard height | **1000 mm** (exceeds both the 864 mm stair minimum and the 914 mm landing minimum, matches common byelaw) |
| Baluster gap | **< 100 mm** (satisfies both the 102 mm sphere and the 100 mm European convention) |

A stair built to this column is compliant essentially anywhere and comfortable. **Use it as the default unless a constraint forces a departure — and record the departure.**

---

## Section 4: Headroom, Clear Width, and the Floor Opening

### 4.1 How headroom is measured

Headroom is measured **vertically, from the line joining the tread nosings (the "nosing line"), to the nearest overhead obstruction** — the soffit of the floor slab above, a beam, a duct, a light fitting, or the underside of a flight above. It is **not** measured perpendicular to the flight, and it is **not** measured from the tread surface at the back of the tread.

At a landing it is measured from the finished landing surface.

**Obstructions that are routinely missed and then hit:**
- Down-stand beam at the edge of the floor opening (the most common)
- The soffit of the flight above in a stacked straight-run stair
- The mid-landing soffit of a dogleg, where circulation passes underneath
- An AC duct or a soil pipe crossing above the stairwell
- A pendant light hung over the flight
- The mumty door head at the roof

### 4.2 The floor-opening length calculation (do this every time)

This is the calculation that determines how big the hole in the upper floor must be. It is the step people skip.

```
GIVEN:
  H     = floor-to-floor height                      (mm)
  R     = riser                                      (mm)
  T     = tread/going                                (mm)
  t_f   = upper floor structure + soffit finish      (slab + plaster)  (mm)
  HR    = required headroom (design 2100)            (mm)

DERIVE:
  Soffit level of upper floor above lower FFL:   S = H − t_f
  Maximum nosing height that still clears:       h_max = S − HR
  Number of the last nosing that may sit under the slab:
                                                 n_c = floor(h_max / R)
  Horizontal position of that nosing from the first riser face:
                                                 x_c = (n_c − 1) × T
  REQUIRED OPENING LENGTH (measured from the first riser face
  to the far edge of the upper floor):
                                                 L_open ≥ Going − x_c
```

#### Worked example — the 18-riser, 3200 mm straight flight from §1.1

| Quantity | Value |
|---|---|
| H | 3200 mm |
| R / T | 177.8 / 275 mm |
| Going = 17 × 275 | 4675 mm |
| Upper floor: 150 slab + 20 plaster + 30 screed/tile → structure below FFL | t_f = 170 mm (slab + soffit plaster) |
| Soffit level S = 3200 − 170 | **3030 mm** |
| Required headroom HR | 2100 mm |
| h_max = 3030 − 2100 | **930 mm** |
| n_c = floor(930 / 177.8) = floor(5.23) | **5** |
| x_c = (5 − 1) × 275 | **1100 mm** |
| **Required floor opening length** = 4675 − 1100 | **≥ 3575 mm** |

**Reading of the result:** the upper floor may only extend 1100 mm horizontally over the bottom of the flight. Everything beyond that — 3575 mm of it — must be an open well. On a 5-marla plot that is 3.6 m of first-floor slab you do not get to use. **This is the real cost of a straight stair, and it is invisible on a plan until you run this calculation.**

Repeat with the IRC bare minimum HR = 2032 mm: h_max = 998 → n_c = 5 → identical result. The 68 mm of extra design headroom is free here. **Always design to 2100.**

### 4.3 Clear width — what counts and what steals it

| Element | Width penalty | Rule |
|---|---|---|
| Wall plaster both sides | 25–40 mm | Model the *finished* opening, not the brick-to-brick |
| Handrail on one side | IRC allows handrail projection into the required width by up to **114 mm (4.5 in)** each side | R311.7.1 — so a 1050 mm structural opening with one handrail still gives 1050 mm "clear width" for code purposes |
| Handrail bracket + 38 mm wall gap | ~75–90 mm of *physical* obstruction at hand height | Affects furniture-carrying, not code compliance |
| Stringer / guard newel post | 50–100 mm | Measure clear between finished faces |
| Skirting | 15–20 mm each side | Usually ignorable |

**Practical widths for a house stair:**

| Clear width | What it supports |
|---|---|
| 762 mm | Absolute minimum below handrail with two rails (IRC). Uncomfortable. Secondary/mumty only. |
| 900 mm | Code-minimum-ish single-file stair. A mattress will not go up it. |
| **1000 mm** | Sensible minimum for a main house stair. One person comfortably. |
| **1050–1100 mm** | **Recommended default.** Two people can pass sideways; a double mattress turns. |
| 1200 mm | Generous; two-abreast; needed if a stairlift is a future possibility (Section 14). |
| 1500 mm+ | Feature/grand stair. Costs plan area exponentially — the well grows too. |

### 4.4 Landings

| Rule | Value | Source |
|---|---|---|
| Landing width | ≥ stair width | IRC R311.7.6 |
| Landing depth in direction of travel | ≥ 914 mm (36 in) | IRC R311.7.6 |
| Straight-through landing (flight continues in same direction) | depth ≥ 914 mm; 1000 mm preferred | |
| Quarter-turn (L) landing | square, side = stair width; min 914 × 914 | |
| Half-turn (U/dogleg) landing | depth = stair width; length = 2 × flight width + well | |
| Landing required at top and bottom | Yes — **exception (IRC R311.7.6):** not required at the top of an interior flight provided **a door does not swing over the stairs** | IRC R311.7.6 |
| Door swinging onto a landing | Must not reduce landing depth to less than **half** the required depth when fully open, and not less than 292 mm (11.5 in) when in motion | IRC R311.7.6 |
| Slope of landing | ≤ 2% (1:50) for drainage on external landings; level internally | |

**The door-over-stair rule is the one that bites in Pakistani plans**, where a bedroom door frequently opens directly at the head of the flight. Either provide a 914 mm landing or make the door swing away from the stair.

---

## Section 5: Flight Composition — how many risers before you must break

| Rule | Limit | Source |
|---|---|---|
| Max vertical rise between floor levels or landings | **3835 mm (151 in)** — ≈ 21 risers at 180 mm | IRC R311.7.3 |
| Max risers per flight | **12** | NBC India (dwellings) |
| Practical Pakistani cap | 16 | practice |
| Minimum risers for a "flight" (below which a handrail isn't required) | 4 risers triggers the handrail requirement | IRC R311.7.8.1 |
| **Never** design a flight of exactly | **2 risers** with no handrail and no visual cue | practice — the classic level-change fall |

**Design guidance:** for a 3200 mm storey the natural splits are **9 + 9** (dogleg), **11 + 7** or **10 + 8** (L-shape). Prefer the balanced split for a dogleg (it makes the mid-landing land at exactly half the storey height, which makes any under-landing store and any half-landing window geometrically clean). Prefer an unbalanced split for an L-shape where the corner position is fixed by the plan.

**Single-riser level changes inside a house are a hazard.** If a room drops 150 mm, either make it three risers with a handrail, a ramp at 1:12, or eliminate it.

---

## Section 6: Winder Treads — geometry, code, and the derived minimum radius

A **winder** is a tapered (pie-shaped) tread that turns the stair without a landing. It is the most space-efficient way to change direction — and the most commonly mis-set-out element in house stairs.

### 6.1 IRC 2021 §R311.7.5.2.1 — the three winder rules

| Rule | Limit |
|---|---|
| Tread depth **at the walkline** | **≥ 254 mm (10 in)** |
| Position of the walkline | **305 mm (12 in)** from the **narrow (inside) edge** of the tread |
| Tread depth **at any point within the clear stair width** | **≥ 152 mm (6 in)** |
| Uniformity | Largest winder tread at the walkline may not exceed the smallest by more than **9.5 mm (3/8 in)** in the same flight |

Winders are permitted in dwellings by IRC. They are *not* permitted on required means of egress in most commercial contexts.

### 6.2 The derived geometry — what those rules actually force

Set out winders about an inner radius **r_i** (the radius of the newel post or the inner well, measured to the finished inside face of the stair). Each winder subtends an angle **θ** (radians). Then:

```
Tread depth at the narrow edge  = r_i · θ        must be ≥ 152 mm
Tread depth at the walkline     = (r_i + 305) · θ  must be ≥ 254 mm

⇒  r_i ≥ 152 / θ                  (narrow-edge rule — this one almost always governs)
⇒  r_i ≥ 254/θ − 305              (walkline rule)
```

The narrow-edge rule governs whenever θ < 0.83 rad (47.5°), which is every practical winder arrangement. **So the binding constraint is: r_i ≥ 152 / θ.**

### 6.3 Minimum inner radius by winder arrangement (derived from §6.2)

For a **90° turn**:

| Winders in the 90° turn | θ per winder | **Minimum inner radius r_i** | Walkline tread at that r_i | Verdict |
|---|---|---|---|---|
| **2 winders @ 45°** | 0.7854 rad | **194 mm** | (194+305) × 0.7854 = **392 mm** ✓ | **Best for a tight plan.** Turn about a ~200 mm radius newel/well. |
| **3 winders @ 30°** | 0.5236 rad | **290 mm** | (290+305) × 0.5236 = **312 mm** ✓ | Good. Needs a ~580 mm diameter well — often a duct or a post. |
| **4 winders @ 22.5°** | 0.3927 rad | **387 mm** | (387+305) × 0.3927 = **272 mm** ✓ | Smoothest walk, biggest well. Approaching a curved stair. |
| 3 winders @ 30° about a **point** (r_i = 0) | 0.5236 | — | narrow edge = 0 mm ✗ | **ILLEGAL.** This is what most builders draw. |

For a **180° turn** (U-turn on winders instead of a half-landing), double the winder count at the same θ and the same r_i.

**Claude rule:** when a plan shows winders turning about a point or a 50 mm newel, it is non-compliant regardless of how it looks. The fix is either a bigger well (≥ 194 mm radius for 45° winders), fewer winders, or a landing.

### 6.4 Winder set-out worked example — 90° turn, 2 winders, 1050 mm clear width

| Step | Value |
|---|---|
| Stair clear width | 1050 mm |
| Winders per 90° turn | 2 @ 45° (θ = 0.7854 rad) |
| Minimum inner radius from §6.3 | 194 mm → **adopt r_i = 225 mm** (250 mm dia RCC newel + 100 mm) |
| Narrow-edge tread depth = 225 × 0.7854 | **177 mm** ≥ 152 ✓ |
| Walkline radius = 225 + 305 | 530 mm |
| Walkline tread depth = 530 × 0.7854 | **416 mm** ≥ 254 ✓ (and ≥ the straight-flight 275 mm — a *deeper* step at the walkline) |
| Outer-edge tread depth = (225 + 1050) × 0.7854 | 1001 mm — very deep; the outer corner is effectively a small landing |
| Run saved vs a 914 mm quarter landing | ≈ 914 − (2 winders' plan projection at the walkline ≈ 750) ≈ **165 mm of run, plus the landing width** — the real saving is that the turn happens *within* the flight footprint |

**Honest assessment:** two 45° winders replacing a quarter landing typically saves **0.7–1.0 m² of plan area**. That is meaningful on a 5-marla plot and irrelevant on a kanal. Pay the safety cost only when the area matters.

### 6.5 Winder hazard profile — when NOT to use them

| Do not use winders when… | Because |
|---|---|
| An elderly or mobility-impaired user is a current or foreseeable occupant | The narrow inside edge is where they will place a foot |
| The stair is the route for moving furniture | A wardrobe will not negotiate a winder turn |
| A stairlift is a possibility | Winder stairlift rails cost 2–3× a straight rail and some models refuse the geometry |
| It's the only stair and someone will carry a child down it at night | The tread narrows exactly where the handrail turns |
| The plan can accommodate a 914 mm quarter landing | Take the landing. It is a rest point, a safety break in a long fall, and a place to put a window. |

---

## Section 7: Selecting the Stair Type for a Tight Residential Plan

### 7.1 The selection decision tree

```
START: Going (from §1) is known. Available plan envelope is known.
│
├─ Q1. Does a straight run + 914 mm landing at each end fit in the available length?
│   │   (typical requirement: Going + 1800 mm)
│   ├─ YES → STRAIGHT FLIGHT. Stop here — it is the cheapest, safest, easiest to build,
│   │        and the easiest to move furniture on. Do not "design" a turn you don't need.
│   └─ NO  → continue
│
├─ Q2. Is there a CORNER available (two perpendicular runs, each ≥ half the going)?
│   ├─ YES → L-SHAPE (quarter-turn) with a 914-1000 mm landing.
│   │        Prefer landing over winders unless Q3 forces it.
│   └─ NO  → continue
│
├─ Q3. Is there a compact rectangular stairwell roughly
│       (Going/2 + landing depth) LONG × (2 × width + 100) WIDE?
│       For H=3200: about 3300 × 2300 mm
│   ├─ YES → U-SHAPE / DOGLEG (half-turn). The standard Pakistani house stair.
│   │        Best area efficiency of any landing-based type.
│   └─ NO  → continue
│
├─ Q4. Is the shortfall small (≤ 900 mm of run) and are all users able-bodied?
│   ├─ YES → replace the landing with WINDERS (§6). L-with-winders or U-with-winders.
│   │        Verify r_i ≥ 152/θ. Verify furniture route separately.
│   └─ NO  → continue
│
├─ Q5. Is this a SECONDARY stair (mumty/roof access, loft, basement, servant stair,
│       utility mezzanine) rather than the primary daily circulation?
│   ├─ YES → SPIRAL (§8) — 1524-1626 mm diameter. IRC permits it as the sole means
│   │        of egress WITHIN a dwelling unit. Accept the usability penalty.
│   └─ NO  → continue
│
├─ Q6. Is the level change small (≤ 1 storey in a loft/mezzanine) and the space
│       genuinely minimal?
│   ├─ YES → ALTERNATING TREAD DEVICE / ship's ladder — IRC R311.7.11 permits these
│   │        only for access to lofts/attics/mezzanines ≤ 23 m², not as a required
│   │        stair between occupied storeys. [verify against local byelaw]
│   └─ NO  → the plan is wrong. Go back and re-plan. Steal the space from a room.
│
└─ ALWAYS: the stair is the last thing to compromise. A 200 mm narrower bedroom is
   invisible. A non-compliant stair is a fall.
```

### 7.2 Footprint and performance comparison (H = 3200 mm, 18R @ 177.8, T = 275, width 1050)

| Type | Stairwell footprint (L × W) | Gross area | Upper-floor opening | Build cost index | Safety / comfort | Furniture route | Best for |
|---|---|---|---|---|---|---|---|
| **Straight** | 4675 × 1050 (+ landings) ≈ 6475 × 1050 | **6.8 m²** incl. approaches | 3575 × 1050 = 3.75 m² | **1.00** | ★★★★★ | ★★★★★ | Long narrow plots, ≥ 6.5 m of run available |
| **L-shape (quarter landing)** | 3025 × 2000 approx | **6.1 m²** | ~2.0 m² | 1.10 | ★★★★☆ | ★★★★☆ | A real corner in the plan; entry hall stairs |
| **L-shape with 2 winders** | 2750 × 1900 | **5.2 m²** | ~1.8 m² | 1.20 | ★★★☆☆ | ★★★☆☆ | Corner exists but is 700–900 mm short |
| **U-shape / dogleg** | 3300 × 2200 | **7.3 m²** but **rectangular and stackable** | ~2.4 m² | 1.15 | ★★★★☆ | ★★★☆☆ | **Default for 3–10 marla Pakistani houses.** Stacks identically on every floor; the mid-landing gives a window and a rest. |
| **U-shape with winders** | 3000 × 2100 | **6.3 m²** | ~2.2 m² | 1.30 | ★★☆☆☆ | ★★☆☆☆ | Only when the dogleg is 300 mm too long |
| **Spiral, 1524 mm dia** | 1624 × 1624 (incl. 50 mm clearance) | **2.6 m²** | 2.6 m² (circular well) | 1.60–3.00 (steel/fabricated) | ★★☆☆☆ | ★☆☆☆☆ | Mumty, loft, guest annexe, roof access |
| **Curved / helical** | 3000+ × 2500+ | 7.5 m²+ | large | 4.00+ | ★★★★☆ | ★★★☆☆ | Feature stair only; needs bespoke formwork |

*Cost index is relative construction cost of the stair element itself (RCC straight flight = 1.00); it excludes the value of the plan area consumed.*

### 7.3 The area arithmetic that decides most Pakistani house plans

On a **5 marla (25 ft × 45 ft ≈ 7.62 × 13.72 m ≈ 104 m²) plot**, after setbacks a typical ground floor covered area is 65–80 m². A stair consuming **7.3 m² is 9–11% of the floor** — and it consumes it **on every floor**.

| Plot | Typical stair type | Stair as % of covered area/floor |
|---|---|---|
| 3 marla | Dogleg, 900–1000 mm flights, or winder-U | 12–15% |
| **5 marla** | **Dogleg, 1000–1050 mm flights** | **9–11%** |
| 10 marla | Dogleg or L, 1100–1200 mm flights | 6–8% |
| 1 kanal | Straight or L, 1200–1500 mm, often a feature | 4–6% |

**Implication:** on 3 and 5 marla, put the stair against a party wall, stack it identically on every floor, and use the under-flight volume (Section 13). On 1 kanal, the stair can afford to be a straight run in the entrance hall.

---

## Section 8: Spiral Stairs in Houses

### 8.1 IRC 2021 dimensional envelope (residential spiral)

| Item | Requirement | Note |
|---|---|---|
| **Minimum clear width** at and below the handrail | **660 mm (26 in)** | R311.7.10.1 |
| **Minimum tread depth at the walkline** | **190.5 mm (7-1/2 in)**, walkline **305 mm (12 in)** from the narrow edge | R311.7.10.1 |
| **Maximum riser** | **241 mm (9-1/2 in)** | R311.7.10.1 |
| **Minimum headroom** | **1981 mm (6 ft 6 in / 78 in)** — *less* than the 2032 mm straight-flight requirement | R311.7.10.1 |
| Tread uniformity | All treads identical | R311.7.10.1 |
| **Overall diameter** (practical consequence of the above) | **≥ 1524 mm (60 in)**; **1626 mm (64 in)** commonly required for timber construction because of the thicker centre column and tread roots | practice + manufacturer standard |
| **Permitted as the sole means of egress *within* a dwelling unit** | **YES**, if all of the above are met | IRC — the key reason spirals appear in tight house plans |

### 8.2 Spiral geometry derivation

```
r_c   = radius of the centre column (typically 50-100 mm)
r_o   = outer radius = overall diameter / 2
walkline radius r_w = r_c + 305
tread angle θ (rad) must satisfy:   r_w · θ ≥ 190.5 mm
number of treads per full turn N = 2π / θ  →  N ≤ 2π · r_w / 190.5
```

#### Worked example — 1524 mm diameter spiral, H = 3200 mm

| Quantity | Value |
|---|---|
| Overall diameter | 1524 mm → r_o = 762 mm |
| Centre column diameter | 150 mm → r_c = 75 mm |
| Clear width = r_o − r_c | 687 mm ≥ 660 ✓ |
| Walkline radius r_w = 75 + 305 | 380 mm |
| Minimum tread angle θ = 190.5 / 380 | 0.501 rad = **28.7°** |
| **Maximum treads per 360°** = 360 / 28.7 | **12.5** (use 12 for a clean 30° layout) |
| Adopt θ = 30° → tread depth at walkline = 0.5236 × 380 | **199 mm** ≥ 190.5 ✓ (only 8.5 mm of margin — tight; verify against the actual fabricated walkline dimension before relying on it) |
| Riser count: n = ceil(3200 / 241) | **14 risers** |
| Actual riser R = 3200 / 14 | **228.6 mm** ≤ 241 ✓ |
| Total rotation = 14 × 30° | **420° = 1.17 turns** |
| **Headroom check:** rise per full turn = 12 × 228.6 | 2743 mm |
| Less tread + structure thickness (say 60 mm) | **2683 mm clear** ≥ 1981 ✓ (comfortably) |
| Floor opening (well) | circular, **1624 mm dia** (diameter + 50 mm clearance each side) |
| Footprint | **2.07 m²** (well) / 2.6 m² including approach clearance |

**Note the riser: 228.6 mm.** That is 29% steeper than the 177.8 mm main-stair riser. A spiral is legal, it is compact, and it is genuinely unpleasant. That trade is the whole story.

**A note on the walkline tread margin:** at the 12-tread/30° layout above, the walkline tread comes out to only 8.5 mm above the 190.5 mm minimum. A different spiral layout — more treads per turn, a smaller centre column, or a narrower overall diameter — can easily fall *below* 190.5 mm even though it looked fine against an under-stated minimum. **Always recompute θ_min = 190.5 / r_w for the specific layout in front of you; do not assume the §8.2 worked example's margin carries over.**

### 8.3 Spiral use cases — good, tolerable, and wrong

| Verdict | Use case |
|---|---|
| ✅ **Good** | Roof / mumty access from a first-floor landing where a full stair would eat a bedroom |
| ✅ **Good** | External access to an upper-floor guest annexe or a rented portion (very common in Lahore/Karachi houses) |
| ✅ **Good** | Loft, mezzanine study, or storage attic |
| ✅ **Good** | Basement access to a utility/store, where the main stair doesn't continue down |
| ⚠️ **Tolerable** | Secondary stair in a house that already has a compliant main stair |
| ⚠️ **Tolerable** | Sole stair in a small studio/annexe occupied by able-bodied adults, where IRC's sole-egress allowance applies **and** the local byelaw agrees |
| ❌ **Wrong** | Primary daily stair in a family house |
| ❌ **Wrong** | Any house with a resident who is elderly, pregnant, mobility-impaired, or under 6 |
| ❌ **Wrong** | The only route to bedrooms — you cannot carry an unconscious adult down a spiral, and neither can a paramedic with a stretcher |
| ❌ **Wrong** | The only route by which furniture must reach the upper floor |

**When recommending a spiral, always state the furniture and stretcher limitations explicitly.** Clients consistently underestimate both.

### 8.4 Material and construction notes for spirals

| Type | Typical spec | Note |
|---|---|---|
| Fabricated MS (mild steel) — most common in Pakistan | 150–200 mm dia CHS centre column, 5–6 mm chequered plate treads welded to brackets, MS pipe handrail | Cheap, fast, needs a good fabricator; galvanise or epoxy-paint if external |
| MS frame + timber treads | Same column, hardwood 38–50 mm treads bolted to brackets | Better feel and acoustics indoors |
| Precast concrete | Individual precast treads threaded onto a central RCC or steel column | Heavy; needs a crane or in-situ stacking; excellent durability |
| In-situ RCC helical | Continuous helical waist slab, no centre column | **Engineer-designed only** — a helical slab is a coupled bending/torsion problem, not a one-way slab. Expensive formwork. |

The centre column of an MS spiral **must be founded on its own pad footing or on a slab thickened locally**, and **must be laterally restrained at the top** (bolted to the floor slab edge or the well trimmer). A spiral column that is only fixed at the base sways noticeably and progressively loosens.

---

## Section 9: Handrails and Guards

### 9.1 Dimensional requirements

| Item | Requirement | Source |
|---|---|---|
| Handrail required | Where the flight has **4 or more risers**; at least one side | IRC R311.7.8.1 |
| Handrail height above the nosing line | **864–965 mm (34–38 in)** — design **900 mm** | IRC R311.7.8.1 |
| Handrail height at landings | Same 864–965 mm band, measured above the landing surface | |
| Clearance handrail-to-wall | **≥ 38 mm (1-1/2 in)** | IRC R311.7.8.3 |
| Continuity | Full length of flight, from a point directly above the top riser to a point directly above the lowest riser; ends returned to a wall or terminating in a newel/safety terminal | IRC R311.7.8.2 |
| **Type I graspable, circular** | Outside diameter **32–51 mm (1-1/4 to 2 in)** | IRC R311.7.8.5 |
| **Type I graspable, non-circular** | Perimeter **102–159 mm (4 to 6-1/4 in)**; maximum cross-section dimension **57 mm (2-1/4 in)** | IRC R311.7.8.5 |
| **Type II** (perimeter > 159 mm) | Requires a finger recess on both sides beginning ≤ 19 mm below the widest point, ≥ 8 mm deep | IRC R311.7.8.5 |
| Guard height, **landings/floor openings** (open side more than 762 mm above the floor below) | **≥ 914 mm (36 in)** — design **1000 mm** | IRC R312.1.2 |
| Guard height, **the stair flight itself** (open side, measured from the nosing line) | **≥ 864 mm (34 in)** per R312.1.2's own stair exception — this is *lower* than the 914 mm landing figure; design **1000 mm anyway** so a single continuous guard detail satisfies both conditions without a step-up at the landing | IRC R312.1.2, exception |
| Guard infill | No 102 mm (4 in) sphere may pass; at the triangle formed by riser, tread and bottom rail, no 152 mm (6 in) sphere may pass | IRC R312.1.3 |
| Commercial-style extensions (top: 305 mm horizontal; bottom: one tread depth + 305 mm) | **Not required by IRC** for dwellings — but strongly recommended for aging-in-place | IBC 1014.6 / ADA 505 |

**The most-violated rule in built houses: the flat-top-rail guard.** A 100 × 50 mm timber or a 50 mm square MS section as the handrail is **not graspable** — it fails the 57 mm max cross-section for Type I and has no finger recess for Type II. It is also the least useful thing to grab while falling. Specify a separate 40 mm circular grab rail alongside the guard top rail if the aesthetic demands a flat cap.

### 9.2 Structural loads on handrails and guards — ASCE 7-22 §4.5

*"Loads on Handrails, Guards, Grab Bars, Seats and Vehicle Barriers"*

| Load case | Magnitude | Application |
|---|---|---|
| **Concentrated load** | **0.89 kN (200 lb)** | Any point, **any direction**, on the handrail or top rail |
| **Uniform load** | **0.73 kN/m (50 lb/ft)** | **Any direction**, along the handrail/top rail, transferred through the supports to the structure |
| **Concurrency** | The 0.89 kN concentrated and 0.73 kN/m uniform loads are **NOT required to act simultaneously** — check each separately | ASCE 7-22 §4.5.1 |
| **Infill components** (balusters, panel fillers, any guard component other than the top rail) | **0.22 kN (50 lb)** applied **horizontally** over a **305 × 305 mm (1 ft²)** area | ASCE 7-22 §4.5.2 |
| Infill concurrency | The infill load need not be combined with the top-rail loads | |

These load into the **posts, the post-to-slab anchorage, and the waist slab or stringer locally** — which is the part that actually fails.

### 9.3 Worked handrail post check — MS post on an RCC waist slab

**Given:** guard posts at 1100 mm centres, 1000 mm high above the finished tread, 50 × 50 × 3 mm MS SHS, 150 mm waist slab, fy(steel) = 250 MPa.

| Step | Calculation | Result |
|---|---|---|
| Concentrated case | 0.89 kN at the top | governs vs uniform |
| Uniform case | 0.73 kN/m × 1.100 m tributary | 0.80 kN — **less than 0.89 kN**, so the concentrated case governs |
| Moment at post base | 0.89 kN × 1.000 m | **0.89 kNm** |
| SHS 50×50×3 section modulus | I = (50⁴ − 44⁴)/12 = 208,492 mm⁴; Z = I / 25 | **8,340 mm³** |
| Bending stress | 0.89 × 10⁶ / 8,340 | **107 MPa** |
| Allowable (0.6 fy) | 0.6 × 250 | 150 MPa → **✓ passes** (utilisation 71%) |
| Base plate, 2 bolts at 120 mm lever arm | T = 0.89 / 0.120 | **7.4 kN tension per bolt** |
| Anchor requirement | M12 chemical/expansion anchor, ≥ 100 mm effective embedment, ≥ 100 mm edge distance | **PROBLEM: 100 mm embedment into a 150 mm waist slab with 20 mm cover leaves 30 mm — marginal** |

**Conclusion and the real detail:** post-installed anchors into a 150 mm waist slab are at the edge of viability for a 7.4 kN tension. **The correct detail is to cast starter bars or a threaded sleeve into the waist slab during the pour**, at the post positions marked from the stair setting-out drawing. Retro-drilling a stair guard is the single most common cause of a wobbly, and eventually unsafe, house guard. **Call this out at the shuttering stage, not at the handrail stage.**

Same check for a **wall-mounted handrail bracket**: 0.89 kN at 75 mm from the wall face → 0.067 kNm per bracket plus 0.89 kN shear; brackets at ≤ 900 mm centres into solid masonry (not into hollow block, and never into 12 mm plaster with plastic plugs).

### 9.4 Guard and baluster detailing checklist

- [ ] Guard height ≥ 1000 mm from nosing line (exceeds both the 864 mm stair minimum and the 914 mm landing minimum)
- [ ] Vertical balusters, gap < 100 mm — **vertical, not horizontal**: horizontal rails are a climbing ladder for a toddler
- [ ] No 152 mm sphere passes the riser/tread/bottom-rail triangle
- [ ] Bottom rail ≤ 100 mm above the nosing line, or infill continues to the nosing
- [ ] Handrail is graspable (32–51 mm circular, or Type I non-circular limits)
- [ ] Handrail returns to the wall or a newel at each end — **no free-projecting end** that catches a sleeve or a bag strap
- [ ] Handrail is continuous around the mid-landing of a dogleg (do not stop and restart it)
- [ ] Post anchorage: cast-in starters or sleeves, marked on the shuttering drawing
- [ ] Where the guard runs along a landing or a first-floor void, check the same 0.89 kN / 0.73 kN/m load on the *slab edge* — a 100 mm slab edge with no edge beam is the weak link
- [ ] Glass guards: laminated only, ≥ 2 × 8 mm with a 1.52 mm interlayer **[verify against the specific product's tested capacity for the ASCE 7-22 loads]**

---

## Section 10: RCC Staircase Structural Detailing

The standard Pakistani and South Asian house stair is an **in-situ RCC inclined waist slab spanning longitudinally between the floor beam and the landing beam**, with the steps cast as solid triangles on top of the waist. Everything in this section is for that system unless stated.

### 10.1 Structural type selection

| Type | How it spans | Waist/depth | When to use | Engineer complexity |
|---|---|---|---|---|
| **Longitudinally-spanning waist slab** | One-way inclined slab, floor beam → landing beam | 125–175 mm | **Default for houses.** Any flight 2.5–4.5 m going. | Low |
| **Transversely-spanning waist slab** | Waist spans between the two flanking walls, across the flight width | 100–125 mm | Narrow enclosed stair (≤ 1.2 m) with load-bearing walls both sides | Low — but the walls must be structural on **both** sides, permanently |
| **Cantilever treads** | Each tread cantilevers from a wall or spine beam | tread 150–200 mm root | Feature stair; needs a very stiff supporting wall/beam with cast-in anchorage | **High** |
| **Slabless / folded plate (tread-riser)** | Steps themselves form a folded plate | 100–150 mm plate | Architectural feature; ~40% more steel; complex bar bending | **High** |
| **Spine beam (single central stringer)** | Central RCC or steel beam with cantilevered treads | beam 300–450 deep | Open-feel stairs; torsion in the spine governs | **High** |
| **Steel stringer + timber/steel treads** | Two channels/plates as inclined beams | C150–C250 or 250×12 plate | Fast, dry construction; retrofit; external | Medium |

Anything other than the first two rows must be flagged to the engineer at concept stage, not at detailing.

### 10.2 Waist slab thickness — the span/depth decision

Three sources, three rules. **Use the most conservative that applies, then check deflection.**

| Source | Rule | For a 2.75 m span | For a 3.3 m span | For a 4.2 m span |
|---|---|---|---|---|
| **ACI 318-19 Table 7.3.1.1** — one-way slab, simply supported, not supporting damage-prone partitions | **h ≥ L / 20** | 138 mm | 165 mm | 210 mm |
| ACI 318-19 Table 7.3.1.1 — one end continuous | h ≥ L / 24 | 115 mm | 138 mm | 175 mm |
| ACI 318-19 Table 7.3.1.1 — both ends continuous | h ≥ L / 28 | 98 mm | 118 mm | 150 mm |
| ACI 318-19 Table 7.3.1.1 — cantilever | h ≥ L / 10 | 275 mm | 330 mm | 420 mm |
| **IS 456:2000 Cl. 23.2 / Cl. 33** rule of thumb cited in South Asian practice | h ≈ L / 30, then modified for tension steel % | 92 mm | 110 mm | 140 mm |
| South Asian trade rule of thumb **[practice]** | 40–50 mm per metre of horizontal going | 110–138 mm | 132–165 mm | 168–210 mm |
| **Pakistani site practice [practice]** | 125 mm standard; 150 mm for going > 3.5 m | 125 mm | 150 mm | 175 mm |

**ACI 318-19 correction for steel grade:** if fy ≠ 420 MPa, multiply the tabulated minimum thickness by **(0.4 + fy / 700)**.
- fy = 415 MPa (common Grade 60 equivalent in Pakistan): factor = 0.4 + 415/700 = **0.993** → effectively no change.
- fy = 500 MPa: factor = 0.4 + 500/700 = **1.114** → thickness increases 11%.
- fy = 275 MPa (mild steel): factor = 0.4 + 275/700 = **0.793** → thickness may reduce 21%.

**Claude default:** for a single house flight spanning between a floor beam and a landing beam, treat it as **simply supported (L/20)** unless the engineer confirms continuity — the landing beam usually provides only partial fixity, and a stair with a sagging waist is a permanent, visible, un-fixable defect.

| Going (horizontal span L) | ACI L/20 | **Adopt waist** |
|---|---|---|
| ≤ 2.4 m | 120 mm | **125 mm** |
| 2.4 – 3.0 m | 150 mm | **150 mm** |
| 3.0 – 3.6 m | 180 mm | **175 mm** + verify deflection, or add a landing beam to create continuity |
| 3.6 – 4.5 m | 225 mm | **Do not use a simple waist slab.** Add an intermediate landing, or a spine/stringer beam, or engineer-designed continuity. |

### 10.3 Load take-down on a stair flight (per m² of **horizontal plan projection**)

The two errors here are (a) using the inclined area for self-weight but plan area for live load, and (b) forgetting the triangular step concrete entirely.

```
1. WAIST SLAB SELF-WEIGHT (converted to plan projection)
   w_waist = t_waist × γ_conc × √(R² + T²) / T
   where γ_conc = 24 kN/m³

2. STEPS (solid triangular concrete on top of the waist)
   w_steps = 0.5 × R × γ_conc          (per m² of plan — the ½·R·T triangle over a
                                        T-wide plan strip reduces exactly to ½·R·γ)

3. FINISHES
   Tread + riser tile/marble + bedding + soffit plaster:  1.0 – 1.5 kN/m²  [practice]
   Marble/granite risers and treads with thick bedding:   up to 2.0 kN/m²

4. LIVE LOAD
   ASCE 7-22 Table 4.3-1, one/two-family dwelling stairs: 1.92 kN/m² (40 psf)
   IS 875 Part 2 / common South Asian practice:            3.0 kN/m²
   ASCE 7-22 also requires a concentrated 1.33 kN (300 lb) over a 50×50 mm area
   on stairs/exits, checked separately  [verify the exact ASCE clause for the
   dwelling-unit case before relying on it]
   → USE 3.0 kN/m² for houses. It costs almost nothing and covers a moving day.
```

#### Load table for common stair geometries (t_waist as noted, finishes 1.2 kN/m², LL 3.0 kN/m²)

| R / T (mm) | √(R²+T²)/T | Waist | w_waist | w_steps | Finishes | **Total DL** | **wu = 1.2DL + 1.6LL** |
|---|---|---|---|---|---|---|---|
| 165 / 300 | 1.142 | 125 | 3.43 | 1.98 | 1.20 | **6.61** | **12.7 kN/m²** |
| 175 / 280 | 1.157 | 125 | 3.47 | 2.10 | 1.20 | **6.77** | **12.9 kN/m²** |
| 177.8 / 275 | 1.191 | 150 | 4.29 | 2.13 | 1.20 | **7.62** | **13.9 kN/m²** |
| 177.8 / 275 | 1.191 | 175 | 5.00 | 2.13 | 1.20 | **8.33** | **14.8 kN/m²** |
| 190 / 250 | 1.257 | 150 | 4.53 | 2.28 | 1.20 | **8.01** | **14.4 kN/m²** |
| 190 / 250 (marble) | 1.257 | 150 | 4.53 | 2.28 | 2.00 | **8.81** | **15.4 kN/m²** |

*All values kN/m² on horizontal plan projection. γ_conc = 24 kN/m³.*

### 10.4 Worked flexural design — the 5-marla dogleg flight

**Given:** flight of 9 risers, R = 177.8 mm, T = 275 mm, clear width 1050 mm, going = 8 × 275 = 2200 mm, effective span to the landing beam **L = 2.75 m** (going + half the landing bearing). Concrete **M20 (f'c = 20 MPa)**, steel **fy = 415 MPa**, cover **20 mm** (interior slab, ACI 318-19 Table 20.5.1.3.1).

| Step | Calculation | Result |
|---|---|---|
| **1. Thickness** | ACI 7.3.1.1 simply supported: h ≥ L/20 = 2750/20 = 137.5 mm; × (0.4 + 415/700) = 136.6 mm | **adopt h = 150 mm** |
| **2. Loads** (from the table, 177.8/275, 150 waist) | DL = 7.62 kN/m²; LL = 3.0 kN/m² | |
| **3. Factored load** | wu = 1.2(7.62) + 1.6(3.0) = 9.14 + 4.80 | **13.94 kN/m²** → 13.94 kN/m per metre width |
| **4. Design moment** | Mu = wu L² / 8 = 13.94 × 2.75² / 8 = 13.94 × 7.5625 / 8 | **13.18 kNm/m** |
| **5. Effective depth** | d = 150 − 20 (cover) − 5 (half of a 10 mm bar) | **125 mm** |
| **6. First-pass steel** | As ≈ Mu / (φ fy · 0.95d) = 13.18×10⁶ / (0.9 × 415 × 118.75) | 297 mm²/m |
| **7. Iterate** | a = As·fy/(0.85 f'c b) = 297×415/(0.85×20×1000) = 7.25 mm; d − a/2 = 121.4 mm; As = 13.18×10⁶/(0.9×415×121.4) | **291 mm²/m** |
| **8. Minimum steel** | ACI 318-19 §7.6.1.1: As,min = 0.0018 × 1000 × 150 = 270 mm²/m (×420/415 = 273) | 273 mm²/m — **flexure governs, barely** |
| **9. Provide main steel** | 10 mm @ 200 c/c → 78.5 × 1000/200 = 393 mm²/m | **10 mm Ø @ 200 c/c ✓** (35% reserve) |
| **10. Max spacing** | lesser of 3h = 450 mm and 450 mm → 450 mm; **stair practice caps at 200 mm** | 200 ✓ |
| **11. Distribution steel** | Shrinkage/temperature: 0.0018 × 1000 × 150 = 270 mm²/m | **8 mm Ø @ 175 c/c** = 287 mm²/m ✓ |
| **12. Shear** | Vu = wu L / 2 = 13.94 × 2.75 / 2 = 19.2 kN/m | |
| | φVc = 0.75 × 0.17 λ √f'c · b · d = 0.75 × 0.17 × √20 × 1000 × 125 / 1000 | **71.3 kN/m ≫ 19.2 ✓** (no shear steel — as expected for a slab) |
| **13. Deflection** | h = 150 ≥ 136.6 required → **no explicit deflection calculation needed** per ACI 7.3.1.1 | ✓ |
| **14. Development** | Bottom bars anchored into the landing beam and floor beam: ld for a 10 mm bar in M20 with fy 415 ≈ **475 mm** **[compute properly per ACI 318-19 §25.4.2 — this is an estimate]**; provide a 90° hook where straight embedment is short | flag to engineer |

**Result summary — flight waist slab:**

| Element | Specification |
|---|---|
| Waist slab | **150 mm**, M20 concrete, 20 mm cover |
| Main bars | **10 mm Ø @ 200 c/c**, running **along the slope**, bottom face through mid-span, hooked into the landing and floor beams |
| Top bars over supports | **10 mm Ø @ 200 c/c** for 0.25 L (≈ 700 mm) either side of the landing beam — the landing beam gives partial fixity that the simply-supported design ignored, and unrestrained partial fixity cracks the top face |
| Distribution bars | **8 mm Ø @ 175 c/c**, transverse, placed **above** the main bars |
| Tread nosing bars **[practice]** | 8 mm Ø one per tread, tied to the waist mesh, controls corner spalling |
| Landing slab | 150 mm, 10 mm @ 200 c/c both ways |
| Landing beam | 230 × 300 mm, 2-12 mm top + 2-12 mm bottom, 8 mm stirrups @ 150 c/c **[preliminary — engineer to design]** |

**Practice cross-check:** Pakistani site practice for this flight would typically be *12 mm @ 150 c/c* main (753 mm²/m) — **2.6× the calculated requirement**. That over-provision is common, is not free, and is usually a substitute for having done the calculation. It is also *not* a safety margin against the real risks here (headroom, uniformity, guard anchorage, formwork).

### 10.5 The re-entrant corner detail — the one stair detail everyone gets wrong

```
At the FLIGHT-TO-LANDING junction, where the corner OPENS OUT
(the tension face is on the INSIDE of the kink):

  ✗ WRONG — carry the tension bar continuously around the inside of the corner.
            The resultant of the two bar forces pushes OUTWARD, perpendicular to
            the concrete face. Cover spalls → the bar straightens → the joint
            hinges → the flight drops. This is a brittle, sudden failure.

  ✓ RIGHT — STOP each tension bar and ANCHOR it into the COMPRESSION zone of the
            adjoining member. Cross the bars over: the flight's bottom bar turns up
            and anchors a full ld into the landing's TOP face; the landing's bar
            turns down and anchors a full ld into the flight's soffit. Add a
            diagonal hairpin across the corner.

At a corner that CLOSES (tension face on the OUTSIDE of the kink) the resultant
pushes INTO the concrete and a continuous bar is acceptable — a hairpin remains
good practice.
```

This is the same detail as in `architecture-concrete-reinforcement-detailing` §10.4. **Check every stair drawing for it.** In a dogleg it occurs at **four** locations: bottom of flight 1, top of flight 1 into the landing, bottom of flight 2 out of the landing, top of flight 2 into the floor.

### 10.6 Support conditions and the traps

| Trap | What happens | Fix |
|---|---|---|
| Flight bearing on a 115 mm partition wall that a later owner demolishes | Flight loses a support, collapses or sags | **Never** bear a flight on a non-structural wall. Note the load path on the drawing and in the O&M file. |
| Cantilevered landing or flight with steel in the bottom face | Tension is at the **top** in a cantilever; bottom steel does nothing | Top steel, full ld into the back-span, back-span ≥ 2 × cantilever |
| Landing beam omitted "because the landing sits on walls" | The landing slab then spans the wrong way, and the flight has no support at its top | If the landing has walls on 3 sides it can work — the engineer must confirm and the walls must be permanent structural walls |
| Stair cast **after** the frame, as an afterthought, with dowels drilled in | No moment continuity; drilled dowels in a beam soffit are in the tension zone | Cast the stair with the frame, or provide engineer-specified cast-in starters |
| Waist slab used to carry a wall above | Introduces a line load the design never saw | Never |

### 10.7 The seismic problem — a stair is a stiff diagonal brace

In an RCC frame house, **the staircase is the stiffest element in the building** — an inclined concrete plate rigidly connecting two floors. Under lateral load it acts as a diagonal brace, which has three consequences:

1. **It attracts seismic force** far in excess of its share of mass, and drags that force into the landing beam and the adjacent columns.
2. **It creates a short-column condition.** The mid-landing beam frames into a column at mid-storey height, halving that column's effective length. Its stiffness quadruples, so it takes ~4× the shear — and short columns fail in brittle shear. This is a documented major cause of RC frame damage in earthquakes.
3. **It makes the plan torsionally irregular** if the stair core is off-centre — which it almost always is in a house, being tucked against a party wall.

**What to do:**
- **Tell the engineer the stair exists and where it is.** Do not hand over a model with the stair drawn only as architecture.
- The columns adjacent to the mid-landing beam must be **confined over their full height** with closely spaced ties (ACI 318-19 §18.7.5 spacing over the short-column region), not just at the standard end zones.
- In higher seismic zones (BCP Zone 3/4 — Quetta, Muzaffarabad, Gilgit, and much of northern Pakistan) the engineer may **isolate the stair** with a slip joint at one end so it does not brace the frame. That is a deliberate detail, not a default.
- Cross-reference `architecture-seismic-design` and `architecture-structural-systems` §13 before finalising any RCC frame house with an internal stair core.

### 10.8 Concrete, cover and finish

| Item | Value | Source |
|---|---|---|
| Concrete grade | **M20 minimum** (1:1.5:3) for a house stair; M25 preferred for exposed/external | practice + IS 456 |
| Clear cover, internal waist slab | **20 mm** | ACI 318-19 Table 20.5.1.3.1 (slabs, not exposed) |
| Clear cover, external stair | **40 mm** (50 mm if coastal/Karachi) | ACI 318-19; durability |
| Steps cast | **Monolithic with the waist**, same pour where possible | A cold joint at the waist/step interface is where the tread cracks off |
| Formwork strike, soffit props | **14 days minimum** for a stair soffit; do **not** strike a stair on the 7-day slab rule | practice — the stair carries construction traffic immediately |
| Construction joint | If unavoidable, place it at the **landing**, never mid-flight | |

---

## Section 11: Steel and Timber Stairs (secondary/external/retrofit)

Included because Pakistani houses commonly use a fabricated steel external stair to an upper-floor rental portion or roof.

### 11.1 Steel stringer preliminary sizing **[practice]**

| Clear span between supports | Two-stringer channel (each side) | Single central spine |
|---|---|---|
| ≤ 2.5 m | 2 × C150 × 75 (ISMC 150) | 200 × 100 × 6 RHS |
| 2.5 – 3.5 m | 2 × C200 × 75 (ISMC 200) | 250 × 150 × 8 RHS |
| 3.5 – 4.5 m | 2 × C250 × 82 (ISMC 250) | 300 × 150 × 10 RHS or a plate girder |
| > 4.5 m | Add an intermediate support or a landing | Engineer-designed |

Treads: 5–6 mm chequered plate with a folded 40 mm downstand each edge, or 38–50 mm hardwood on angle cleats. Deflection limit **span/360** for comfort; span/500 if a tiled tread is used (tiles crack at span/360).

**Vibration is the failure mode people actually complain about, not strength.** A steel stair that satisfies strength at span/360 can still feel alarming. Aim for a first natural frequency > 5 Hz, or simply be generous with the stringer.

### 11.2 External steel stair durability (Pakistan)

- Hot-dip galvanise where budget allows; otherwise 2-coat epoxy zinc primer + PU topcoat, re-coated every 5–7 years.
- **Water must not pond on treads.** Chequered plate with a 1:100 cross-fall or perforated/grating treads.
- Isolate the steel base plate from the RCC with a bituminous pad — the base is where every external steel stair in Karachi and Lahore rots first.
- Fixings: stainless or galvanised only. A galvanised stringer with mild steel bolts fails at the bolts.

### 11.3 Timber stairs

Rarely primary in Pakistan, common as a feature. Cut-string or closed-string; treads 32–50 mm hardwood; strings 250–300 × 50 mm. Screwed and glued wedges, not nails. **Squeak is caused by movement at the tread/riser joint** — glue blocks in the internal angle at 200 mm centres solve it, retrofitting them later does not.

---

## Section 12: Finishes, Nosings and Slip Resistance

| Item | Requirement / recommendation |
|---|---|
| **Nosing projection** | 19–32 mm where tread < 279 mm (IRC R311.7.5.3); uniform within 9.5 mm |
| **Nosing profile** | Rounded (radius ≤ 14 mm) or bevelled (≤ 14 mm). **No square projecting nosing** — it catches toes |
| **Under-nosing** | Must not slope more than 30° from vertical (IRC) — a deep undercut catches a shoe |
| **Slip resistance** | Wet DCOF ≥ 0.42 per ANSI A326.3 for tiled treads; **do not use polished marble or porcelain on stair treads** without an anti-slip strip |
| **Anti-slip strip** | Aluminium/brass nosing insert or a carborundum strip set 25 mm back from the nosing — retrofit-able, cheap, and the single highest-value stair safety item |
| **Visual contrast at the nosing** | 50 mm contrasting band on the tread and riser at each nosing. Essential for aging-in-place and for anyone with reduced vision; also just reduces misjudged steps at night |
| **Riser finish** | Closed risers for a main house stair. Open risers are a code case (102 mm sphere rule) and a psychological barrier for elderly users |
| **Finish thickness discipline** | Decide the tread/riser finish build-up **before** setting out the risers (§1 Step 1). A 20 mm marble tread with a 10 mm bed changes the first and last riser by 30 mm if only one floor gets it |
| **Handrail finish** | Timber or PVC-coated over steel indoors — a bare steel handrail is unpleasant to grip in a Lahore January or a Karachi June |

---

## Section 13: The Space Under the Stair

| Configuration | Usable soffit height | Best use |
|---|---|---|
| Straight flight, full length | 0 → 3000 mm, wedge-shaped | Store cupboard at the tall end (≥ 1800 mm), shoe/drawer bank in the middle, sealed void at the low end |
| **Dogleg, under flight 1** | 0 → ~1430 mm (mid-landing soffit) | Under-stair store with a door on the tall face; **not** a WC (see below) |
| **Dogleg, under the mid-landing** | ~1430 mm constant | Storage. **Do not route circulation under it** — 1430 mm is a head injury |
| **Dogleg, under flight 2** | Nothing — flight 2 is over the landing/flight 1 zone, not over the floor | — |
| L-shape, under the long flight | 0 → 2000+ mm | Powder room possible **only if** ≥ 2000 mm at the WC pan position and ≥ 1800 mm at the door |

**The under-stair WC trap:** clients constantly ask for a powder room under the stair. It works under a straight flight of ≥ 4.5 m going, where the tall end gives 2000 mm+. It does **not** work under a dogleg flight 1, where the maximum is ~1430 mm at the mid-landing. Check the soffit height at the actual pan position and at the door swing before agreeing.

**Structural note:** the under-stair void's enclosure walls are non-structural infill. Draw them as 115 mm partitions and make sure the stair does not bear on them (§10.6).

**Fire note:** in many jurisdictions an under-stair store in a house that forms part of the protected escape route must be either fire-separated or omitted. **[verify against local byelaw]** — the principle (don't store the paint tins inside your only escape route) applies regardless of whether the byelaw says so.

---

## Section 14: Accessibility and Aging-in-Place Overlay

Private single-family dwellings are generally exempt from ADA/accessibility law. **They are not exempt from the client getting older.** Cross-reference `architecture-accessibility-design` for the full treatment; this is the stair-specific subset.

| Measure | Standard-house value | **Aging-in-place / ambulant-disabled value** |
|---|---|---|
| Riser | 175–190 mm | **150–170 mm** |
| Tread | 250–280 mm | **≥ 280 mm**, uniform, closed risers |
| Risers per flight | ≤ 12 | **≤ 12**, and prefer 10–11 with a mid-landing |
| Handrails | One side | **Both sides**, 900 mm, continuous |
| Handrail extensions | Not required (IRC) | **305 mm horizontal at the top; one tread depth + 305 mm at the bottom** (ADA 505.10 pattern) |
| Nosing contrast band | Optional | **Required in practice** |
| Clear width | 1000–1050 mm | **≥ 1000 mm clear, with 1200 mm structural opening** so a stairlift rail (typ. 175–200 mm of intrusion) still leaves 800 mm |
| Winders | Permitted | **Avoid entirely** |
| Spiral | Permitted as secondary | **Never** |
| Stair type | Any | **Straight or single-landing L.** Doglegs are acceptable; multi-winder turns are not. Stairlift rails on straight runs cost roughly a third of a curved bespoke rail |
| Lighting | Switch top and bottom | Add **step-level lighting** at the skirting, plus a motion sensor |
| Future through-floor lift | — | If the plan can accommodate a **1000 × 1400 mm** aligned void on both floors (typically stacked cupboards), reserve it now. Retrofitting it later means cutting a slab. |

**Design decision to raise with any client over 50, unprompted:** *"Do you want this to be a stair you can still use at 75, or do you want to reserve space for a lift?"* It changes the riser, the width, and possibly the plan — and it costs nothing at design stage.

---

## Section 15: Fire, Egress and the Stair as an Escape Route

**[Byelaw-dependent — verify. The principles below are code-agnostic.]**

| Item | House-scale guidance |
|---|---|
| Stair as the sole escape route | In a 1–2 storey house this is normal and accepted. In a 3+ storey house many byelaws require the stair to be **enclosed in fire-rated construction** with self-closing doors, or require a **second escape route**. Check LDA/CDA/SBCA byelaws for the storey count trigger. |
| Spiral as sole egress | IRC permits it **within a dwelling unit** if the §8.1 dimensions are met. It is a poor practical escape route. |
| Emergency escape and rescue openings | IRC R310: every sleeping room and every basement needs an openable escape window — **relevant here because a bedroom whose only other exit is the stair is a trap if the stair is the fire** |
| Under-stair storage | Do not store combustibles in the escape route (§13) |
| Smoke alarms | One at the head of the stair on each storey, interconnected — the stair is the smoke chimney of the house |
| Handrail in smoke | The reason continuity (§9.1) matters: in zero visibility the handrail **is** the wayfinding. A handrail that stops at the mid-landing and restarts leaves people groping at exactly the point they must change direction. |
| Stair enclosure doors | If enclosed, doors must be self-closing and must not reduce the landing below the §4.4 depths when open |

---

## Section 16: Failure Modes and Anti-Patterns

| # | Anti-pattern | Consequence | Fix |
|---|---|---|---|
| 1 | **Riser count derived from slab-to-slab, not FFL-to-FFL** | Top or bottom riser off by the finish thickness; > 9.5 mm violation; trip hazard at the most dangerous step | §1 Step 1. Fix the finishes spec before the risers. |
| 2 | **Floor opening sized by eye** | 1.8 m headroom at the fourth-from-top step, discovered after the pour | §4.2 calculation, every time |
| 3 | **Winders turned about a point or a 50 mm newel** | Narrow-edge tread of 20–40 mm; illegal; genuinely dangerous | §6.3 — r_i ≥ 152/θ |
| 4 | **Flat 50 mm square top rail used as the handrail** | Not graspable; useless in a fall; fails IRC R311.7.8.5 | Add a 40 mm circular grab rail, or use a Type I profile |
| 5 | **Guard posts drilled into the finished waist slab** | 7.4 kN anchor tension into 30 mm of remaining concrete; progressive loosening; eventual failure at height | Cast-in starters/sleeves at shuttering stage (§9.3) |
| 6 | **Mumty/roof stair built steeper than the main stair** | Different cadence on the same building; the most common Pakistani stair fall | Same riser/tread as the main stair, or at minimum within code |
| 7 | **Stair drawn as architecture only; engineer never told it's a stiff diagonal** | Short-column shear failure at the mid-landing beam in a seismic event | §10.7 — tell the engineer, confine the columns |
| 8 | **Flight bearing on a 115 mm partition** | Future renovation removes the support | §10.6 — note the load path on the drawing |
| 9 | **Cantilever landing with bottom steel** | Immediate cracking, potential collapse | Top steel, full ld, back-span ≥ 2 × cantilever |
| 10 | **Continuous bar around an opening re-entrant corner** | Cover spalls, joint hinges, flight drops | §10.5 — cross and anchor into the compression zone |
| 11 | **Polished marble treads, no anti-slip** | Wet-foot falls, especially from a bathroom above | Anti-slip nosing insert; DCOF ≥ 0.42 |
| 12 | **Door swinging over the top of the flight** | Person is pushed backwards down the stair | §4.4 — 914 mm landing, or swing the door away |
| 13 | **Handrail stopping at the mid-landing** | Loss of support exactly where direction changes | Continuous around the landing |
| 14 | **Under-stair WC in a dogleg** | 1430 mm soffit over the pan | §13 — check soffit at the pan and the door |
| 15 | **Spiral specified as the primary family stair to save 4 m²** | 228 mm risers, no furniture route, no stretcher route | §8.3 — say no, and say why |
| 16 | **"We'll adjust the last riser on site"** | The 9.5 mm rule is violated by 20–30 mm at the top step | Recompute n. Never adjust one riser. |
| 17 | **Stair soffit props struck at 7 days with the slab** | Sagging waist, permanent visible defect | 14 days minimum (§10.8) |
| 18 | **Balusters horizontal** | Toddler ladder | Vertical, gaps < 100 mm |
| 19 | **Applying a spiral's or a stair's numeric dimensional minimum from memory instead of re-checking it for the layout at hand** | A different tread count, radius or column size can silently fall short of the true minimum even though a previously-worked example passed | §8.2 note — recompute θ_min for the actual layout; don't assume a prior worked example's margin transfers |

---

## Section 17: Full Worked Example — 5-Marla G+1 House, Lahore

**Brief:** 25 ft × 45 ft (7.62 × 13.72 m) plot. Ground + first floor. Stair zone available against the party wall: **3600 mm long × 2400 mm wide**. Floor-to-floor 3200 mm. RCC frame with 150 mm slabs. Family of four; client's parents visit and are in their seventies.

### 17.1 Geometry (§1, §2, §3)

| Step | Result |
|---|---|
| H (FFL to FFL) | 3200 mm |
| n = round(3200/175) = 18 | R = **177.8 mm** ✓ (≤ 190, ≤ 196) |
| T = 630 − 355.6 = 274.4 → | T = **275 mm** ✓ (≥ 250, ≥ 254) |
| 2R + T | 630.6 mm ✓ Blondel |
| R × T | 48,895 mm² ✓ product rule |
| Pitch | 32.9° ✓ comfort band |
| Straight going = 17 × 275 | 4675 mm — **does not fit 3600 mm** |
| §7 tree: Q1 no → Q2 no corner → **Q3 dogleg** | 3300 × 2200 required vs 3600 × 2400 available ✓ |

### 17.2 Adopted layout — dogleg / half-turn

| Item | Value | Check |
|---|---|---|
| Split | 9 risers + 9 risers | 9 ≤ 12 (NBC) ✓ |
| Rise per flight | 9 × 177.8 = **1600 mm** | ≤ 3835 (IRC R311.7.3) ✓ |
| Treads per flight | 8 | going per flight = 8 × 275 = **2200 mm** |
| Mid-landing depth | **1100 mm** | ≥ 914 ✓ and ≥ flight width 1050 ✓ |
| Stairwell length = 2200 + 1100 | **3300 mm** ≤ 3600 ✓ (300 mm spare for the landing beam and plaster) |
| Flight clear width | **1050 mm** each | ≥ 914 IRC ✓, ≥ 1000 target ✓ |
| Stairwell width = 2 × 1050 + 100 (central well/wall) | **2200 mm** ≤ 2400 ✓ |
| Nosing | 25 mm, rounded r = 12 mm | 19–32 ✓ |
| Effective foot area = 275 + 25 | 300 mm | comfortable |

### 17.3 Headroom and the floor opening (§4.2)

| Check | Calculation | Result |
|---|---|---|
| Upper floor soffit above lower FFL | 3200 − 150 slab − 20 plaster | 3030 mm |
| Flight 2 nosings run from 1600 mm to 3200 mm | all above h_max = 3030 − 2100 = 930 mm | **the upper slab must not extend over flight 2 at all** |
| **Floor opening in the first-floor slab** | full plan of flight 2 + 100 mm margin = **2300 × 1150 mm** | this is the well; the landing itself is a slab and is *not* part of the opening |
| Headroom under the mid-landing soffit | 1600 − 150 landing slab − 20 plaster | **1430 mm — storage only, no circulation** ✓ (flagged on the plan) |
| Headroom over flight 1 (to the mid-landing soffit above? none — flights are side by side) | n/a in a dogleg | ✓ **this is the dogleg's structural advantage over a stacked straight run** |
| Headroom over flight 2 to the roof slab | roof soffit at 6200; top nosing at 3200 | 3000 mm ✓ |
| Head clearance at the first-floor doorway adjacent to the well | verify the door head at 2100 does not clash with the landing beam | flag to coordinate |

### 17.4 Structure (§10)

| Element | Design | Basis |
|---|---|---|
| Flight waist slab | **150 mm, M20, 20 mm cover** | ACI 318-19 Table 7.3.1.1: L/20 = 2750/20 = 138 mm; × 0.993 = 137 mm |
| Design load | DL 7.62 + LL 3.0 → **wu = 13.94 kN/m²** | §10.3 table |
| Design moment | Mu = 13.18 kNm/m | wL²/8, L = 2.75 m |
| Main steel | **10 mm Ø @ 200 c/c along the slope** (393 mm²/m provided vs 291 required) | §10.4 |
| Top steel at supports | 10 mm Ø @ 200 c/c over 700 mm each side of the landing beam | partial fixity |
| Distribution steel | **8 mm Ø @ 175 c/c** transverse, above the main bars | 0.0018 Ag |
| Landing slab | 150 mm, 10 mm @ 200 both ways | |
| Landing beam | 230 × 300, 2-12T + 2-12B, 8 mm stirrups @ 150 | **preliminary — engineer to design** |
| Re-entrant corners | Cross-anchored bars + hairpin at **all four** flight/landing junctions | §10.5 |
| Seismic | Lahore ≈ BCP Zone 2A **[verify against the current BCP map]**. Mid-landing beam frames into the party-wall column at 1600 mm → **short column**. Confine that column full height, ties @ 100 c/c. | §10.7 — **flag to engineer explicitly** |
| Formwork | Soffit props struck at 14 days minimum | §10.8 |

### 17.5 Handrail, guard, finishes (§9, §12, §14)

| Item | Specification |
|---|---|
| Handrail | **Both sides** (client's elderly parents — §14), 40 mm circular timber-over-steel, **900 mm** above the nosing line, 40 mm wall clearance, **continuous around the mid-landing**, returned to the wall at both ends |
| Handrail extensions | 305 mm horizontal at the top of each flight; one tread + 305 mm at the bottom — not IRC-required, adopted for aging-in-place |
| Guard to the open well side | **1000 mm** high (exceeds both the 864 mm stair-specific and 914 mm landing minimums), vertical MS balusters at **95 mm** clear gaps, top rail plus a separate 40 mm grab rail |
| Guard/post anchorage | **Cast-in 12 mm starter bars at 1100 mm centres in the waist and landing slabs** — marked on the shuttering drawing (§9.3). Checked for ASCE 7-22 §4.5: 0.89 kN concentrated → 0.89 kNm at the post base → SHS 50×50×3 at 107 MPa, 71% utilisation ✓ |
| Guard along the first-floor well edge | Same spec; **verify the 150 mm slab edge locally** — add an edge beam or thicken to 200 mm at the post line |
| Treads | 20 mm honed (not polished) granite, 25 mm rounded nosing, **brass anti-slip insert 25 mm back from the nosing** |
| Nosing contrast | 50 mm lighter band on the tread edge |
| Risers | Closed, granite-faced |
| Lighting | Ceiling fitting over the well + **skirting-level step lights on flight 1**; three-way switches at ground, mid-landing and first floor |
| Under-stair (flight 1) | Storage cupboard, door on the tall face. **Not a WC** — max soffit 1430 mm (§13) |

### 17.6 Compliance summary sheet for this stair

| Requirement | Required | Provided | ✓ |
|---|---|---|---|
| Riser ≤ 190 / 196 mm | 190 | 177.8 | ✓ |
| Riser uniformity ≤ 9.5 mm | 9.5 | 0.0 (all 18 identical, FFL-derived) | ✓ |
| Tread ≥ 250 / 254 mm | 254 | 275 (+25 nosing) | ✓ |
| 2R + T | 600–650 | 630.6 | ✓ |
| Clear width ≥ 914 mm | 914 | 1050 | ✓ |
| Headroom ≥ 2032 mm | 2032 (design 2100) | 3000 min over flight 2 | ✓ |
| Rise between landings ≤ 3835 mm | 3835 | 1600 | ✓ |
| Risers per flight ≤ 12 | 12 | 9 | ✓ |
| Landing depth ≥ 914 mm and ≥ width | 1050 | 1100 | ✓ |
| Handrail 864–965 mm | 864–965 | 900, both sides | ✓ |
| Handrail wall clearance ≥ 38 mm | 38 | 40 | ✓ |
| Guard ≥ 864 mm (stair) / ≥ 914 mm (landing) | 864 / 914 | 1000 (both conditions) | ✓ |
| Guard opening < 102 mm sphere | 102 | 95 | ✓ |
| Waist slab ≥ L/20 (ACI) | 137 mm | 150 mm | ✓ |
| Main steel ≥ As,req and ≥ As,min | 291 / 273 mm²/m | 393 mm²/m | ✓ |
| Shear φVc ≥ Vu | 19.2 kN/m | 71.3 kN/m | ✓ |
| Handrail post, ASCE 7-22 §4.5 | 0.89 kNm | 107 MPa vs 150 allowable | ✓ |

**Status line to attach to any output of this example:**
> *Preliminary stair set-out and sizing for coordination and FreeCAD modelling. Requires design and stamp by a PEC-registered structural engineer (waist slab, landing beam, guard anchorage, short-column confinement) and LDA plan approval before construction.*

---

## Section 18: FreeCAD Modelling Defaults and Recipe

Pair with the `architecture-freecad-bim` skill for the Site/Building/Storey hierarchy and parametric openings.

### 18.1 Default parameter set

| Parameter | Default | Note |
|---|---|---|
| Floor-to-floor | **3200 mm** | Drives the riser count — set this first |
| Riser | **177.8 mm** (= 3200/18) | Never a round number; a round riser means you rounded the storey height instead |
| Tread / going | **275 mm** | |
| Nosing | **25 mm** | FreeCAD `Nosing` property |
| Number of steps | **18** (9 + 9 for a dogleg) | |
| Clear flight width | **1050 mm** | |
| Waist / structure thickness | **150 mm** | FreeCAD `StructureThickness` |
| Tread thickness (finish) | **50 mm** | FreeCAD `TreadThickness` |
| Landing depth | **1100 mm** | |
| Central well between flights | **100 mm** | Also the handrail zone |
| Handrail height | **900 mm** above nosing line | |
| Guard height | **1000 mm** | |
| Baluster spacing | **95 mm** clear | |
| Floor opening (dogleg) | **2300 × 1150 mm** | Computed in §4.2/§17.3, not eyeballed |
| Headroom target for verification | **2100 mm** | |

### 18.2 Modelling recipe

1. **Set the storey heights first** in the Building/Storey hierarchy. The riser count is a *derived* quantity — if the storey height changes, the stair must be regenerated, not nudged.
2. **Create the stair with `Arch Stairs`**, setting `NumberOfSteps`, `RiserHeight`, `TreadDepth`, `Width`, `Nosing`, `TreadThickness`, `Structure` = *Massive* and `StructureThickness` = the waist. **[Property names vary between FreeCAD versions — verify against the version in use; FreeCAD 1.0's Arch Stairs exposes `Structure`, `StructureThickness`, `Landings`, `Flight` among others.]**
3. **Model the dogleg as two separate `Arch Stairs` objects plus a landing slab**, rather than relying on a single half-turn object. Two objects give you independent control of each flight and make the quantities readable. Group them under a single `Arch BuildingPart` named `Stair_GF_to_FF`.
4. **Cut the floor opening as a real `Subtraction` on the upper `Arch Structure` slab**, using a sketch-driven extrusion — **not** a one-off boolean on a copied solid. The opening must stay parametric so that changing the storey height propagates. (This is the same discipline as parametric wall openings — see `architecture-freecad-bim`.)
5. **Verify headroom in the model, don't assume it.** Draw a construction line along the nosing points, offset it 2100 mm vertically, and check that nothing intersects it. If FreeCAD's measurement tool is available, measure vertically from the topmost nosing that still sits under the slab.
6. **Model the landing beam and the supporting columns** — the mid-landing beam is the object that creates the short-column condition (§10.7), and it will not exist in the model unless you put it there.
7. **Model the guard and handrail as real objects** (`Arch Railing` or a swept profile along a path), not as a 2D annotation. They occupy 100 mm of the width and they are what tells you the stair feels narrow.
8. **IFC classification:** `IfcStair` (the assembly) containing `IfcStairFlight` (each flight) and `IfcSlab` (landing); `IfcRailing` for the handrail/guard; `IfcBeam` for the landing beam. **Verify the classification by exporting to IFC and re-reading it** — an object that exports as `IfcBuildingElementProxy` was never really classified.
9. **Annotate the model or its README** with: the assumed FFL-to-FFL height, the finish thicknesses used to derive it, the code baseline used (IRC 2021 / NBC), the waist thickness basis (ACI L/20), and the licensing status line from §17.6. Nobody downstream should inherit invisible assumptions.

### 18.3 Quick quantity outputs the model should give you

| Quantity | How to derive | Typical for the §17 example |
|---|---|---|
| Concrete volume, flights | (waist area along slope × t) + (step triangles) | 2 × [(2.2 × 1.191 × 1.05 × 0.15) + (8 × 0.5 × 0.1778 × 0.275 × 1.05)] ≈ **1.05 m³** |
| Concrete volume, landing | 2.2 × 1.1 × 0.15 | **0.36 m³** |
| Steel, stair (thumb rule) | 100–130 kg/m³ of stair concrete | **140–185 kg** |
| Formwork area | soffit + risers + edges | ≈ **11 m²** |
| Tread/riser finish area | 17 treads × 1.05 × 0.30 + 18 risers × 1.05 × 0.178 | ≈ **8.7 m²** |
| Handrail length | 2 × (flight sloped length) + landing | 2 × 2.62 + 1.1 ≈ **6.3 m** per side |

Cross-check against `architecture-cost-estimation-boq` for rates.

---

## Section 19: Verification Checklist — run before calling any stair "done"

**Geometry**
- [ ] Riser count derived from **FFL-to-FFL**, with both floors' finish thicknesses stated
- [ ] All risers identical to within 0 mm in the model, ≤ 9.5 mm allowance on site
- [ ] Tread ≥ 254 mm (IRC) / ≥ 250 mm (NBC dwellings); nosing 19–32 mm if tread < 279 mm
- [ ] 2R + T ∈ [600, 650] mm; pitch ≤ 37°
- [ ] Riser ≤ 190 mm (design cap) / ≤ 196 mm (IRC absolute)
- [ ] Clear width ≥ 1000 mm for a main stair, measured **finished face to finished face**
- [ ] Going fits the plan with landings, or a compliant turn type has been selected via §7

**Headroom and openings**
- [ ] §4.2 floor-opening calculation performed and recorded
- [ ] Headroom ≥ 2100 mm (never below 2032) at the **worst** point, checked against slab, beams, ducts, and light fittings
- [ ] Mid-landing soffit height recorded, and no circulation routed beneath it if < 2032 mm
- [ ] Mumty/roof stair uses the **same** riser and tread as the main stair
- [ ] Door swings checked at the top and bottom of every flight

**Landings and flights**
- [ ] Landing depth ≥ 914 mm and ≥ stair width
- [ ] ≤ 12 risers per flight; vertical rise between landings ≤ 3835 mm
- [ ] Winders (if any) satisfy r_i ≥ 152/θ and walkline tread ≥ 254 mm (§6.3)
- [ ] Spiral (if any) satisfies the full §8.1 envelope — **recompute θ_min = 190.5/r_w for the actual layout, do not reuse the §8.2 worked example's numbers for a different tread count or column size** — and its use case is on the ✅ list in §8.3

**Structure**
- [ ] Waist thickness ≥ ACI 318-19 Table 7.3.1.1 minimum for the actual span and steel grade
- [ ] Load take-down includes the **inclination factor** on the waist **and** the triangular step concrete
- [ ] Flexural steel ≥ both the calculated As and As,min = 0.0018 Ag
- [ ] Distribution steel ≥ 0.0018 Ag, placed above the main bars
- [ ] Top steel provided over the landing beam for partial fixity
- [ ] Re-entrant corner detail correct at **every** flight/landing junction
- [ ] Flight does **not** bear on any non-structural wall; load path noted on the drawing
- [ ] Landing beam and its supporting columns modelled and passed to the engineer
- [ ] **Short-column condition at the mid-landing beam explicitly flagged to the engineer**
- [ ] Cover: 20 mm internal / 40 mm external / 50 mm coastal
- [ ] Formwork striking: soffit props ≥ 14 days

**Handrails and guards**
- [ ] Handrail 864–965 mm, ≥ 38 mm wall clearance, continuous, returned at the ends
- [ ] Handrail profile is Type I graspable (32–51 mm circular, or the non-circular limits)
- [ ] Both sides if any occupant is elderly or the width exceeds ~1100 mm
- [ ] Guard ≥ 864 mm on the stair flight itself / ≥ 914 mm on landings (design 1000 mm throughout so one detail covers both), vertical infill, gaps < 100 mm, 152 mm sphere at the tread triangle
- [ ] Guard/post anchorage checked against **ASCE 7-22 §4.5** (0.89 kN concentrated, 0.73 kN/m uniform, 0.22 kN infill)
- [ ] **Cast-in starters or sleeves specified on the shuttering drawing** — not post-drilled anchors
- [ ] Slab edge at the well checked for the guard load; edge beam or local thickening if needed

**Finishes and safety**
- [ ] Tread finish DCOF ≥ 0.42 wet; anti-slip nosing insert specified
- [ ] Nosing contrast band specified
- [ ] Three-way switched lighting at every level served
- [ ] Under-stair space use verified against actual soffit heights

**Handover**
- [ ] Output labelled: *"Preliminary — requires design and stamp by a PEC-registered structural engineer and local authority approval before construction."*
- [ ] Pakistan gap statement (§3.3) included if the project is in Pakistan
- [ ] Assumed code baseline, FFL heights, finish thicknesses and material grades all recorded in the model README

---

## Section 20: Known Gaps in This Skill (state these when relevant)

1. **Building Code of Pakistan stair clause not independently verified.** No clause-level residential staircase provision from BCP 2007 or the BCP 2021 draft was extractable. Every dimensional limit in this skill is IRC 2021 or NBC India 2016. **The governing document for a Pakistani project is the local development-authority byelaw (LDA/CDA/RDA/SBCA/DHA/TMA), which must be read directly.** See `architecture-building-codes-permits` for the byelaw layer.
2. **NBC India 2016 figures are from secondary sources.** The 250 mm tread / 190 mm riser / 12-risers-per-flight values for one- and two-family dwellings were not verified against the primary NBC 2016 document text. Treat them as a regional cross-check, not a citation.
3. **IS 456:2000 Cl. 33 stair provisions are summarised, not reproduced.** The span/30 rule of thumb and the worked-example bar sizes (12 mm @ 180, 8 mm @ 200) circulating in South Asian practice are illustrative — they are not code minimums and they were not derived for your span.
4. **ASCE 7-22 Table 4.3-1 stair live-load values for the one-/two-family dwelling case** (40 psf vs 100 psf, and the 300 lb concentrated load applicability) were not verified clause-by-clause. This skill uses 3.0 kN/m², which is conservative against both.
5. **Development length values are estimated, not computed.** The ld ≈ 475 mm figure in §10.4 step 14 is indicative; compute per ACI 318-19 §25.4.2 with the actual bar size, cover, spacing and modification factors.
6. **No fire-resistance rating design for enclosed stairs.** Where a byelaw requires a fire-rated stair enclosure, the wall/door/slab ratings and the required door closers are outside this skill's scope.
7. **Curved and helical in-situ RCC stairs are out of scope structurally.** A helical waist slab is a coupled bending–torsion problem requiring dedicated analysis. This skill only flags it as engineer-only work.
8. **Steel stringer sizes in §11.1 are practice rules of thumb**, not designed sections. No deflection or vibration calculation underlies them.
9. **Glass guard capacities are not tabulated.** The 2 × 8 mm laminated suggestion is indicative; any glass guard must be selected against a tested capacity for the ASCE 7-22 §4.5 loads, with a post-breakage retention requirement.
10. **Alternating tread devices and ship's ladders (IRC R311.7.11 / R311.7.12)** are mentioned in the §7 selection tree but their dimensional provisions are not reproduced. Verify before using one.
11. **Stairlift and through-floor lift dimensions in §14 are indicative** — confirm against a specific manufacturer's rail intrusion and shaft requirements before reserving space.
12. **Two numeric/citation errors were found and corrected during review, which should lower confidence in any un-re-checked clause elsewhere in this document.** The spiral-stair walkline tread minimum (§8.1/§8.2) had been stated as 171 mm (6-3/4 in) when the correct IRC R311.7.10.1 value is 190.5 mm (7-1/2 in); and the guard-height table (§3.1/§9.1) had applied the 914 mm (36 in) landing/floor minimum uniformly to stairs, when R312.1.2's own exception sets the stair-specific minimum at 864 mm (34 in). Both are now corrected, but **every IRC/IBC clause number and figure elsewhere in this skill should still be independently re-verified against the current code text before being relied on for anything beyond preliminary coordination** — a specific-looking clause citation is not proof of a character-for-character check.

---

## Cross-References

| For… | Use skill |
|---|---|
| Where the stair sits in the plan, room sizes, circulation widths | `architecture-spatial-planning` |
| Whether the house is a frame or masonry, column grid, floor-to-floor heights | `architecture-structural-systems` |
| Rebar detailing conventions, cover, laps, development length, bar bending schedules | `architecture-concrete-reinforcement-detailing` |
| Short-column and stair-as-brace seismic behaviour, zone maps | `architecture-seismic-design` |
| Byelaw stair width/enclosure/mumty rules, plan approval submission | `architecture-building-codes-permits` |
| Ramps, accessible routes, aging-in-place, ambulant-disabled stairs | `architecture-accessibility-design` |
| Stair concrete pour sequencing, formwork striking, finish order | `architecture-construction-sequencing` |
| Stair concrete/steel/finish quantities and rates | `architecture-cost-estimation-boq` |
| Building the stair as a parametric BIM object with verified IFC classification | `architecture-freecad-bim` |
| Drawing the stair set-out as an editable 2D file | `drawio-diagrams` |
</content>
