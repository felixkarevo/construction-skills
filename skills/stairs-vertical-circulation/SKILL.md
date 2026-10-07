---
name: stairs-vertical-circulation
description: >
  Stairs, ramps and lifts (Treppen, Rampen, Aufzüge) for DACH design — stair
  set-out from OKFF-to-OKFF height, Steigungsverhältnis 2s+a=60–65 cm
  (Schrittmaß/Blondel), tread ≥26 cm, rise ≤19(–21) cm as German practice
  values (VERIFY against DIN 18065 current), lichte Durchgangshöhe ≥2.00 m (design 2.10 m),
  floor-opening length algorithm, Gehlinie winder geometry with derived
  minimum inner radius, flight/Podest/door rules (no door onto flight, Podest
  ≥ door width, escape width ≥1.00 m per digested MBO/LBO), type selection
  tree (straight/L/U-Halbwendung/winders/Spindeltreppe), structural forms
  (Laufplatte slab, landing-beam, cantilever, folded plate, spine, precast,
  steel, timber), EC2 preliminary design (C20/25 + B500, EN 1991-1-1 stair
  loads 3.0 kN/m² + 2.0 kN point, slenderness bound, anchorage tables,
  re-entrant corner, Arbeitsfugen), seismic stair-brace/short-column, stair
  acoustics (DIN 4109-32 bearing table 63→35 dB, Trennfuge ≥30 mm, DIN 8989
  shaft masses ≥410–740 kg/m²), fire/escape function (notwendige Treppe,
  enclosure walls by Gebäudeklasse, 0.5/1.0 m² vents, 35 m,
  Sicherheitstreppenraum), ramps (DIN 18040 gradients, VERIFY), two-sided
  handrails ≥90 cm, 12 cm sphere child-safety (VERIFY), lifts per
  EN 81-1/ISO 8100-30 (cars 320–1000 kg, pit 1.4–2.5 m, headroom 3.6–4.4 m,
  machine-room vs MRL, firefighter lift EN 81-72, fire mode EN 81-73,
  platform lift EN 81-41), traffic heuristics, stair+lift core coordination
  order, FreeCAD Arch Stairs / Arch.makeStairs recipe with BoundBox
  rotation-convention check. Planning and verification aid — not an approval.
---

# Stairs and Vertical Circulation (Treppen, Rampen, Aufzüge) — DACH Practice Skill

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

The **stair set-out, code-check, lift-sizing and preliminary structural
coordination skill** for vertical circulation: the one (or two) stairs
connecting Keller → EG → OG → DG in a one/two-family house or
Mehrfamilienhaus, the Rampe that joins or replaces them, and the Aufzug that
takes the traffic when the building gets tall enough to require one. It
exists so that a stair drawn in FreeCAD has a *real* riser count derived from
the true floor-to-floor height, a going satisfying both the comfort formula
and the governing German dimensional rules, a floor opening long enough for
real headroom, a Treppenlaufplatte whose thickness came from a span/depth
rule, and a Geländer whose anchorage was decided before the pour.

**Stairs are the most dimension-sensitive element in a plan.** Get the riser
count wrong by one and every landing level, door head and Treppenöffnung is
wrong. Get the headroom wrong and the mistake surfaces when someone hits their
head on a poured slab. Unlike a wall, a stair cannot be adjusted 50 mm later.

German regulatory terms are kept in parentheses: submissions, drawings and
authorities communicate in German.

## 0. How to use this skill

Use it when the task involves: setting out a stair from a storey height (rise,
going, Lauf length, Podeste, opening, headroom); choosing the type for a tight
plan; checking the escape function of a Treppenraum; preliminary RC stair
design for coordination with the Tragwerksplaner; acoustic separation of
stair/lift from protected rooms; ramp gradients; lift car/shaft/pit sizing;
modelling any of it in FreeCAD.

Read §1 (reality check) and §2 (evidence tiers) before quoting any number.

| Sibling skill | Overlap |
|---|---|
| `fire-protection-building` | Full Brandschutzkonzept — here only the stair/lift interface |
| `building-acoustics` | Complete Trittschall/Luftschall method — here the stair/shaft specifics |
| `concrete-detailing` | General anchorage, laps, cover, joints — here stair applications |
| `structural-systems` / `seismic-design` | Frame, storey heights, stair brace + short columns |
| `building-services-tga` | Lift as equipment, machine-room ventilation, emergency power |
| accessibility (DIN 18040) library skill | Full barrierefrei route design — here ramps/lift minimums |
| `building-planning-spatial` / `building-regulations-permits` | Core location; LBO per Bundesland, Genehmigung |

## 1. Reality check — licensing and liability

**This skill produces design aids for planning and FreeCAD modelling ONLY.**

- Every dimension, thickness, bar size and load here is a **preliminary
  set-out figure, code minimum, or labelled rule of thumb**. A stair carries
  people at height; a preliminary number is not a design.
- **Any stair for real construction must be reviewed, analysed and signed by
  a qualified structural engineer (Tragwerksplaner)** under the
  Prüfstatik/Prüfingenieur regime of the relevant Bundesland (or the
  equivalent licensed engineer in Austria/Switzerland): Laufplatte, Podest,
  Podestträger, supporting walls/columns, Geländer anchorage.
- **The design must pass the local Bauamt (Baugenehmigung).** Stair width,
  enclosure, Rettungsweg geometry and lift requirements are LBO items —
  separate from and additional to any structural standard.
- Never present output as construction-ready; the framing is always
  *"preliminary set-out and sizing for coordination — to be verified and
  signed by the Tragwerksplaner and approved by the Bauaufsichtsbehörde."*
  Say it unprompted when a user asks for a Biegelehre list for the fixer,
  wants to shave the plate "because it looks thick", or asks to skip the
  Podest beam this week.
- **Never certify** — no stamped drawings, no Standsicherheitsnachweis, no
  signature block.
- **Guards are life-safety, not finish.** A Geländer failing at 900 mm over a
  stairwell drops someone onto concrete; the §19 loads are the *minimum*
  check and the anchorage is the engineer's, not a catalogue's.
- **Standards move; state law differs.** German anchors not carried in the
  project's verified source digests (most DIN 18065 category values, DIN
  18040 gradients, some EN 1991/1992 constants) are tagged **VERIFY against
  the current standard**. The MBO is framework law — the LBO of the
  Bundesland governs.

## 2. Evidentiary tiers

| Tier | Status | Content | Consequence |
|---|---|---|---|
| **T1** | Legal anchor | MBO/LBO duty that buildings be arranged so use is ordnungsgemäß and Rettungswege function → makes the allgemein anerkannten Regeln der Technik (DIN 18065, DIN 18040, Eurocodes via VVB/TB) binding | Public-law minimum; downward deviation needs an Abweichung |
| **T2** | Normative texts | DIN 18065 (Treppen), DIN 18040-1/-2, EN 1991-1-1, EN 1992-1-1/NA, EN 1998-1/NA, DIN 4109 series, DIN 8989, EN 81 series, ASR A2.3 | Quote with edition; values here are excerpts |
| **T3** | Digested excerpts | Escape-stair rules/widths from the digested MBO/LBO fire chapter; lift car/pit/headroom/DIN 8989 data from the digested building-services-tga chapter; DIN 4109-32 stair table; EN 1991 stair loads + EN 1992 anchorage/cover/slenderness/crack tables from the digested structural tables | Usable for iteration; final proof re-derived from the norm |
| **T4** | Practice / carried-over values | Proportion bands, footprint numbers, site defaults kept from prior practice where they align with German norms | Pre-design only; label as estimate |

Any row whose exact normative value is *not* in the digested sources carries
**VERIFY against DIN/EN … current** — the value may be right, but it was not
re-derived from the standard text.

## 3. The set-out algorithm (run first, every time)

Never draw a stair before running these eight steps in order. Most stair
errors are out-of-order: someone drew a stair shape, then fit risers into it.

```
STEP 1 — True floor-to-floor height H (Geschosshöhe):
    OKFF to OKFF (finished to finished), NOT slab-top to slab-top.
    + upper slab build-up + upper screed/finish − lower finish thickness.
    Different finishes per floor ⇒ H ≠ structural dimension.
    → classic site error: slab-to-slab → first/last rise off by 15–25 mm.
STEP 2 — Target rise s_target = 175 mm (165 mm altengerecht) [T4];
    n = round(H / s_target) → INTEGER; s = H / n to 0.1 mm.
STEP 3 — s ≤ 190 mm main dwelling stair / ≤ 210 mm secondary
    [T4 German practice — VERIFY against DIN 18065 current category table].
    Exceeded → n+1, recompute.
STEP 4 — Going from the Schrittmaß band: a = 630 − 2s; round DOWN to 5 mm;
    re-check 2s + a ∈ [600, 650]; a ≥ 260 mm
    [VERIFY exact step pairs against DIN 18065 current].
STEP 5 — Straight-flight going (Auftrittslänge) = (n − 1) × a
    (n rises, n−1 treads — the top "tread" is the upper floor).
STEP 6 — Fits with ≥ 900–1000 mm Podest at each end? → gerader Lauf.
    Else → §8 selection tree.
STEP 7 — Headroom / floor-opening check (§5). lichte Durchgangshöhe
    ≥ 2.00 m by MBO and DIN 18065 (S.2); design to 2.10 m. Skipping this is how you get a 1.8 m soffit
    over the fourth-from-top step.
STEP 8 — Flight rules (§5.4, §6): ≤ ~18 rises per Lauf [VERIFY]; Podest
    depth ≥ stair width and ≥ door leaf width; no door onto the flight [T3].
```

### 3.1 Worked run — H = 3200 mm

| Step | Operation | Result |
|---|---|---|
| 1 | Slab 200 + screed/finish 60 + clear height | **H = 3200 mm** |
| 2 | n = round(3200/175) = 18.29 → 18 | s = **177.8 mm** |
| 3 | 177.8 ≤ 190 ✓ [VERIFY] | pass |
| 4 | a = 630 − 355.6 = 274.4 → **275**; 2s+a = 630.6 | pass (≥ 260) |
| 5 | Going = 17 × 275 | **4675 mm** |
| 6 | Available plan length 3600 mm | **FAILS → Halbwendung (§8)** |
| 7 | Floor opening | see §5.2 |
| 8 | Split 9 + 9; rise per Lauf = 1600 mm | pass |

**Lesson:** a 3200 mm storey at comfortable proportions needs **4.7 m of
straight run**. Almost no standard urban house has it in one room — the
Halbwendung is arithmetic, not aesthetics.

## 4. Rise/going proportion — Schrittmaß (Steigungsverhältnis)

### 4.1 The formula

**François Blondel** (1675) observed that stride shortens when climbing by
roughly twice the rise. German stair practice carries this as the
**Schrittmaß**, and DIN 18065 as the Steigungsverhältnis:

```
    2s + a = 600 to 650 mm      (Schrittmaß 60–65 cm, German practice band)
    Sweet spot 630 mm           [VERIFY exact DIN 18065 pairs — digested
                                 sources give the formula family, not the table]
```

s = Steigung (rise), a = Auftritt (going, nosing-to-nosing, without
Überstand). A level pace ≈ 630 mm; each rise unit consumes two pace units.
Gait locks into cadence within two steps — which is why **uniformity matters
more than the absolute value**: all rises 5 mm tall is fine; one rise 15 mm
off is a trip hazard. Schrittmaß is a comfort filter **inside** the code box,
never instead of it.

### 4.2 Companion checks

| Rule | Band | Use |
|---|---|---|
| Product (Treppenregel) | s·a ≈ 46,000–48,500 mm² | Catches extremes that pass 2s+a [T4] |
| Sum | s + a ≈ 450–470 mm | Site mental check [T4] |
| Neigungswinkel | 30–37° comfortable; ~37–38° domestic max | tan α = s/a [T4/VERIFY per category] |

### 4.3 Combination table (2s + a ≈ 630 mm)

| s (mm) | a (mm) | 2s+a | s·a (mm²) | Pitch | Feel | Status |
|---|---|---|---|---|---|---|
| 150 | 330 | 630 | 49,500 | 24.4° | Grand/public feel | ✓ — long going |
| **165** | **300** | **630** | 49,500 | **28.8°** | **altengerecht default** | ✓ |
| 170 | 290 | 630 | 49,300 | 30.4° | Very comfortable | ✓ |
| **175** | **280** | **630** | 49,000 | **32.0°** | **Main-house default** | ✓ |
| 178 | 275 | 631 | 48,950 | 32.9° | The 18-step/3200 result | ✓ |
| 180 | 270 | 630 | 48,600 | 33.7° | Common practice | ✓ |
| 185 | 260 | 630 | 48,100 | 35.4° | Steep, secondary | ✓ at the going floor |
| 190 | 250 | 630 | 47,500 | 37.2° | **Going below 260 practice floor** | ✗ without VERIFY-waiver |
| 200 | 230 | 630 | 46,000 | 41.0° | A ladder, not a stair | ✗ ✗ |

### 4.4 Uniformity and the code box

| Item | Limit | Basis |
|---|---|---|
| Rise/going uniformity in a Lauf | equal within ~5 mm design intent; never "adjust the last step" on site | [T4 — tolerancing per DIN 18202 family; VERIFY stair-specific clause] |
| Steigung cap | ≤ 190 main / ≤ 210 secondary | [T4 German practice, VERIFY DIN 18065 category table] |
| Auftritt floor | ≥ 260 dwelling main (the old generic 250/254 is below current German practice — don't use without VERIFY) | [VERIFY] |
| Nosing (Überstand) | 20–30 mm where a is tight, radiused/bevelled ≤ 15 mm, uniform | [T4/VERIFY] |
| Open riser / baluster openings | must not pass a **120 mm sphere** (German child-safety practice; old skill carried 100 mm — design default stays ≤ 100 mm) | [VERIFY against DIN 18065 current] |

### 4.5 When the ideal going doesn't fit

1. **n−1** (bigger s, smaller a) until s hits 190.
2. Take **a = 260** and accept 2s+a slightly below 600 (178/260 = 616 —
   tight, legal, walkable).
3. **Nosing** +25 mm buys 25 mm of foot area free.
4. **n+1** flattens but lengthens — only when run is to spare.
5. **Change type** (§8): wendelPodest or second Podest buys run.
6. **Never** vary one rise to make it fit.

## 5. Headroom, lichte Breite, floor opening (Treppenöffnung)

### 5.1 Measurement

Headroom is measured **vertically from the Setzgerade (line joining the step
nosings)** to the nearest obstruction — slab soffit, Unterzug, duct, fitting,
soffit of the Lauf above — never perpendicular to the flight, never from the
back of a tread. At Podeste: from the finished surface. Floor: **2.00 m
(MBO and DIN 18065, S.2)**; design to 2.10 m. Routinely-hit obstructions: opening-edge
downstand beam, soffit of the upper Lauf (stacked straight runs), mid-Podest
soffit of a dogleg with circulation beneath, Lüftungsduct/Fallleitung above
the Treppenraum, pendant lights, Dachausstieg head.

### 5.2 The floor-opening calculation (every time)

```
GIVEN  H, s, a;  t_f = upper floor structure + soffit finish below its OKFF;
       HR = required headroom (2100)
S   = H − t_f                 h_max = S − HR
n_c = floor(h_max / s)        x_c  = (n_c − 1) × a
L_open ≥ Going − x_c          (first riser face → far edge of upper floor)
```

Worked (§3.1 geometry, t_f = 220): S = 2980; h_max = 880; n_c = floor(880/177.8)
= 4; x_c = 3 × 275 = 825; **L_open ≥ 4675 − 825 = 3850 mm.** The upper floor
may overhang the bottom of the flight by only 825 mm; the remaining 3.85 m is
open well. **This is the real cost of a straight stair, invisible on a plan
until computed.**

### 5.3 Lichte Breite — what steals it

Wall putz 25–40 mm; Handlauf projection (German practice counts the required
width with handrail intrusion up to ~90 mm/side [VERIFY DIN 18065 current]);
Geländer post/stringer 50–100 mm; skirting ignorable. Measure finished-face
to finished-face.

| Clear width | Supports | Basis |
|---|---|---|
| < 800 mm | Nothing legal as escape stair | — |
| 900 mm | Private single-file; furniture pain | [T4] |
| **1000 mm** | **Minimum notwendige Treppe (escape stair)** — digested rule *Breite ≥ 100 cm (DIN 18065; ASR A2.3)* | [T3] |
| 1200 mm | Passing; higher user counts (ASR A2.3 categories) | [VERIFY] |
| 1500 mm+ | Representative; Treppenauge grows with it | [T4] |

MFH with several units per Geschoss steps escape widths up (often 1.20–1.50 m)
— **the digest anchors only the 1.00 m floor; verify state LBO + DIN 18065
use category + ASR A2.3.**

### 5.4 Podeste (landings)

| Rule | Value | Basis |
|---|---|---|
| Width / depth | ≥ stair width; depth ≥ 900 mm practice | [T4/VERIFY] |
| **Door onto Podest** | **no door opening directly onto the flight; Podest depth ≥ door leaf width** | [T3 digested escape-stair rule] |
| Viertel-Podest | square, side ≥ stair width | practice |
| Halb-Podest | depth = Laufbreite; length = 2×Laufbreite + Auge | geometry |
| Level | internal level; external ≤ 2 % | practice |
| Richtungswechsel | Podest or compliant winders (§7) | [VERIFY DIN 18065] |

The door-over-stair rule is the one that bites: provide the Podest depth or
swing the door away.

## 6. Lauf composition

| Rule | Value | Basis |
|---|---|---|
| Max rise between Podeste | at most 18 steps (≈ 3.3 m), at least three | confirmed in a book (S.2) |
| Min "flight" | < 4 steps = stumbling hazard | practice |
| Antritt/Austritt | unmistakable: same rise, contrast nosing, good light | practice |

**Small level changes (1–2 steps) are a hazard.** For a 150–350 mm drop:
three steps with cues/handrail, a Rampe ≤ 6 %, or remove it. **Splits:** for
3200 mm prefer 9+9 (balanced → clean Podest window + under-Podest store);
11+7 or 10+8 when the corner is fixed by the plan.

## 7. Winders (Wendelungen) — geometry and minimum radius

A winder is a tapered tread that turns without a full Podest — the
space-efficient turn and the most mis-set-out element in house stairs.

### 7.1 Governing rules [all T4/VERIFY against DIN 18065 current]

| Rule | Adopted value |
|---|---|
| Going at the **Gehlinie (walkline)** | ≥ straight-flight minimum (use 260) |
| Gehlinie position | 300 mm from the narrow inside edge (widths ≤ ~1 m; centre line when wider) |
| Narrow-end going | ≥ 120 mm (old generic value 152 mm — both fix the same geometry problem; use the governing one) |
| Uniformity | winders identical at the Gehlinie |
| Necessary stairs | winders restricted on many escape stairs — Podest per turn [VERIFY state LBO] |

### 7.2 Derived geometry

About inner radius r_i, subtended angle θ (rad): narrow-end = r_i·θ ≥ 120;
Gehlinie = (r_i+300)·θ ≥ 260 ⇒ **r_i ≥ 120/θ** (governs for θ < 43.3°, i.e.
almost always; with the 152 mm basis: r_i ≥ 152/θ — recompute for the layout
at hand, never reuse a prior margin).

### 7.3 Minimum inner radius, 90° turn

| Layout | θ | r_i ≥ 120/θ | (152/θ basis) | Gehlinie going at r_i | Verdict |
|---|---|---|---|---|---|
| 2 winders @ 45° | 0.785 | **153 mm** | 194 mm | 356 mm ✓ | Best for tight plans; ~200 mm newel/well |
| 3 winders @ 30° | 0.524 | **229 mm** | 290 mm | 277 mm ✓ | ~460 mm well — often a duct/post |
| 4 winders @ 22.5° | 0.393 | 306 mm | 387 mm | 238 mm ✗ → r_i ≥ 361 | Smooth, big well; curved-stair territory |
| winders about a point (r_i = 0) | any | — | — | narrow end = 0 ✗ | **Non-compliant** — what most builders draw |

**Rule to enforce:** winders turning about a point or ≤ 50 mm newel are
non-compliant however they look. Fix: bigger well, fewer winders, or Podest.

### 7.4 When NOT to wind

Elderly/mobility-impaired users; furniture route; future stairlift; sole
night route with a child; **whenever a 900–1000 mm Podest fits** — take the
Podest (rest point, safety break, window place). Two 45° winders replacing a
quarter landing save ≈ 0.7–1.0 m² [T4]; pay the safety cost only when area
actually matters.

## 8. Type selection for a tight plan

### 8.1 Decision tree

```
START: Going (§3) and plan envelope known.
Q1 Straight run + ~1 m Podeste fits (≈ Going + 1800–2000 mm)?
   YES → GERADER LAUF. Cheapest, safest, best furniture route. Stop.
Q2 Corner with two perpendicular runs ≥ half the going?
   YES → VIERTELWENDUNG (L) with 900–1000 mm quarter Podest.
Q3 Rectangle ≈ (Going/2 + Podest depth) × (2×width + 100)?
   (H=3200: ~3300 × 2300 mm)
   YES → HALBWENDUNG (dogleg) — the German stacking default; mid-Podest
        gives window + rest. Best area efficiency of landing types.
Q4 Shortfall ≤ ~900 mm, able-bodied users, LBO allows winders?
   YES → WENDLUNGEN (§7): verify r_i ≥ 120/θ; check furniture separately.
Q5 Secondary route only (Dachzugang, Keller, Loft, utility)?
   YES → SPINDELTREPPE (§9) Ø 1500–1650; accept usability penalty; sole
        escape only if LBO/DIN 18065 category explicitly allows [VERIFY].
Q6 Loft-level change in minimal space?
   YES → Raumspartreppe/Leiter — maintenance/loft access only, never the
        required Treppe between occupied floors [VERIFY LBO].
NO → the plan is wrong. Steal space from a room, not the stair.
ALWAYS: a 200 mm narrower bedroom is invisible; a bad stair is a fall.
```

### 8.2 Footprint / performance (H = 3200, 18s@177.8, a = 275, width 1050)

| Type | Footprint L×W | Area | Opening | Cost idx | Comfort | Furniture | Best for |
|---|---|---|---|---|---|---|---|
| Gerade | 4675×1050 + Podeste ≈ 6475×1050 | 6.8 m² | 3.85×1.05 = 4.0 m² | 1.00 | ★★★★★ | ★★★★★ | ≥ 6.5 m of run available |
| Viertelwendung | 3025×2000 | 6.1 m² | ~2.0 m² | 1.10 | ★★★★☆ | ★★★★☆ | Real corner; entry halls |
| L + 2 winders | 2750×1900 | 5.2 m² | ~1.8 m² | 1.20 | ★★★☆☆ | ★★★☆☆ | Corner ~700–900 mm short |
| **Halbwendung** | **3300×2200** | **7.3 m²**, stackable | ~2.4 m² | 1.15 | ★★★★☆ | ★★★☆☆ | **Default house stair** |
| U + winders | 3000×2100 | 6.3 m² | ~2.2 m² | 1.30 | ★★☆☆☆ | ★★☆☆☆ | Dogleg ~300 mm too long |
| Spindel Ø 1524 | 1624×1624 | 2.6 m² | 2.6 m² | 1.6–3.0 | ★★☆☆☆ | ★☆☆☆☆ | Dachzugang, Loft, annex |
| Curved/helical | 3000×2500+ | 7.5+ m² | large | 4.0+ | ★★★★☆ | ★★★☆☆ | Feature; bespoke formwork |

*Cost index = stair element only (in-situ RC straight = 1.00), excludes plan
area consumed.* [T4]

### 8.3 The area arithmetic

A 6.5–7.3 m² stair is **6–12 % of every floor**. EFH: Halbwendung/Viertel at
900–1000 mm; Reihenhaus: Halbwendung 1000–1200; MFH: notwendiger Treppenraum
≥ 1000 (often 1200–1500) stacked identically with shafts and the lift. Put
the stair against a shared wall, use the Untertreppe (§21), reserve the
Aufzug void from sketch one (§18).

## 9. Spindeltreppen (spiral stairs)

### 9.1 Envelope — carried-over practice values, all VERIFY

The digested sources contain no clause-level spiral table. Values below kept
from the prior skill where consistent with German practice, retagged to
DIN 18065 (Wendeltreppe) / state rules:

| Item | Practice value |
|---|---|
| Clear walking width at/below handrail | ≥ 660 mm [VERIFY] |
| Going at Gehlinie (300 mm from narrow edge) | ≥ 190–210 mm [VERIFY] |
| Max rise | ≤ 220 mm secondary-stair envelope [VERIFY] |
| Headroom | ≥ 2100 mm (§5 floor) |
| Overall Ø | ≥ 1500; 1600–1650 with chunky column (consequence) |
| Use | secondary dwelling routes unless LBO says otherwise [VERIFY] |

### 9.2 Geometry + worked Ø 1524, H = 3200

```
r_c column radius; r_w = r_c + 300 (Gehlinie); θ·r_w ≥ a_Gehlinie,min;
N ≤ 2π·r_w/a_min per turn.
```

| Quantity | Value |
|---|---|
| r_o = 762; column Ø 150 → r_c = 75 | clear width 687 |
| r_w = 375 → adopt 12 treads/turn (θ = 30°) | Gehlinie going = 196 mm (tight vs 190 — recompute for the *actual* column Ø) |
| n = ceil(3200/220) = 15 | **s = 213.3 mm** — secondary-stair territory [VERIFY] |
| Rotation ≈ 1.25 turns; opening Ø 1624; footprint ≈ 2.07 m² well | |

**The honest note:** s ≈ 213 mm is ~20 % steeper than a 177.8 main stair —
legal-ish, compact, genuinely unpleasant. Always recompute θ_min for the
layout in front of you; margins from examples do not transfer.

### 9.3 Verdicts

✅ Good: roof/Loft access where a full stair would eat a room; external annex
entry; cellar utility. ⚠️ Tolerable: secondary stair with a compliant main
stair; sole stair of a studio annexe for able-bodied adults *if* the LBO
agrees [VERIFY]. ❌ Wrong: primary family stair; households with
elderly/children/mobility limits; sole bedroom escape (no Trage route);
sole furniture route. State furniture + stretcher limits explicitly — clients
underestimate both.

### 9.4 Materials

Staged steel (CHS column, folded-sheet/chequer treads — retrofit default);
steel + hardwood treads; precast sectional; in-situ RC helical =
**engineer-designed only** (coupled bending/torsion). The column needs its own
footing or thickened bearing **and top lateral restraint**; base-only columns
sway and loosen.

## 10. Construction types — structural form

Default: **in-situ RC Treppenlaufplatte spanning floor-edge beam → Podest
beam, steps cast on top** — everything in §11 designs that system.

| Type | Spans | Depth | When | Complexity |
|---|---|---|---|---|
| **Laufplatte longitudinal** | one-way inclined slab | 120–200 mm | **Default.** Läufe 2.5–4.5 m going | Low |
| **Laufplatte transverse** | between flanking walls across the flight | 100–160 mm | Narrow enclosed ≤ 1.2 m, walls both sides | Low — both walls permanently structural |
| **Kragstufen (cantilever)** | each tread from wall/spine | 150–200 root | Feature; stiff wall + cast-in anchors | **High** |
| **Faltwerk (folded plate)** | the steps themselves | 100–150 | Expressive; ~40 % more steel | **High** |
| **Spine (Rückgrat)** | central RCC/steel beam | 300–450 | Open feel; torsion governs | **High** |
| **Stahlzweitangertreppe** | two inclined stringers + wood/steel treads | 120–250 | Dry, fast, retrofit, external | Medium |
| **Fertigtreppe (precast)** | bolted/grouted units to bearings | system | MFH/parking; programme wins, no props | Bearing/anchor detail per supplier + engineer |
| **Holztreppe** | Wangen (open/cut string) | Wange 250–300×50 | Timber houses | Medium; joinery + structural check |

Anything beyond rows 1–2 goes to the engineer at concept stage. Precast:
transport/strength-at-demould/lifting points are factory items; the **site
interface (grouted bearings, dowels, wet joints)** is what the planner draws
[digested precast-drawing requirements, T3]. A precast Lauf that must also be
an acoustic element cannot be cast into the stair wall at both ends (§14).

## 11. Stahlbeton-Treppenlauf — preliminary EC2 design

### 11.1 Loads (per m² horizontal plan)

| Action | Value | Basis |
|---|---|---|
| Imposed, dwelling/office stairs | **q_k = 3.0 kN/m² + 2.0 kN point** checked separately | [T3 digested load table "Treppen Wohn/Büro", EN 1991-1-1 cat. A] |
| Crowded stairs | 5.0 kN/m² + 2.0 kN | [T3 "sonst. Treppen"] |
| Inclined plate self-weight | t·25·√(s²+a²)/a | γ_conc 25 [T3 digested] + slope factor |
| Step triangles | 0.5·s·25 per m² plan (exact) | geometry |
| Finishes | 1.0–1.5 (stone to 2.0) | [T4] |
| Combination | **p_Ed = 1.35·G + 1.5·Q** | [T3 digested γ-factors] |

| s/a (mm) | slope f. | t (mm) | plate | steps | **G** | **p_Ed** |
|---|---|---|---|---|---|---|
| 165/300 | 1.142 | 120 | 3.29 | 2.06 | 6.55 | 14.0 kN/m² |
| 175/280 | 1.157 | 130 | 3.76 | 2.19 | 7.15 | 14.6 |
| 177.8/275 | 1.191 | 150 | 4.47 | 2.22 | 7.89 | 15.2 |
| 190/260 | 1.240 | 150 | 4.65 | 2.38 | 8.23 | 15.6 |

The two classic errors: forgetting the slope factor, forgetting the steps.

### 11.2 Plate depth

Slenderness bound: **h ≥ l₀/30** (slabs l < 7 m, lightly loaded; heavily
loaded l₀/23; l₀ = β_l·l with β_l 1.0 simply supported / 0.8 continuous end /
2.5 cantilever) [T3 digested K-tables] — **practice floor 120 mm absolute,
140–180 typical** [T4]. A sagging stair soffit is permanent; err up.

| Horizontal span | l₀/30 | Adopt |
|---|---|---|
| ≤ 2.4 m | 80 | **120** |
| 2.4–3.0 m | 100 | **140–150** |
| 3.0–3.6 m | 120 | **160–180** or add a Podest |
| > 3.6 m | — | **No simple span** — Podest, spine, or wall bearing |

### 11.3 Worked design — §3.1 flight

Given: 9 steps, s = 177.8, a = 275, width 1050, l₀ = 2.75 m; **C20/25, B500
(f_yd = 435 MPa)**, cover 20 (XC1) [T3].

| Step | Calculation | Result |
|---|---|---|
| Depth | max(l₀/30 = 92; practice) | **h = 150** |
| Load | G 7.89 + Q 3.0 | p_Ed = **15.15 kN/m²** |
| Moment | 15.15·2.75²/8 | **M_Ed = 14.33 kNm/m** |
| d | 150 − 20 − 5 | **125 mm** |
| Steel | f_cd = 0.85·20/1.5 = 11.33 [T3]; A_s = M/(f_yd·z), iterate z ≈ d − A_s f_yd/(2 f_cd b) | **A_s ≈ 275 mm²/m** |
| Minimum | ≈ 0.15 %·A_c = 225 (digested slab rule — VERIFY) | flexure governs |
| Provide | **Ø 10/200 = 393 mm²/m** (digested area grid) | 43 % reserve |
| Shear | V_Ed = 20.8; V_Rd,c = C_Rd,c·k·(100ρf_ck)^⅓·b·d; **C_Rd,c = 0.12 (NA)**, k = 2.0 cap, ρ = 0.0022 | **≈ 49 kN/m ✓** no shear steel |
| Point load | 2.0 kN local check + dispersion | flag to engineer [T3] |
| Deflection | h ≥ l₀/30 | covered by bound |

Summary: plate 150 C20/25; main **Ø 10/200 along the slope, bottom**; top
steel Ø 10/200 over 0.25·l₀ each side of the Podest beam (partial fixity will
crack an unreinforced top face); distribution **Ø 8/150 above the main**
(≈ 20 %) [T3 digested slab rules]; **w_k ≤ 0.4 mm** quasi-permanent XC1
[T3 digested crack table]. Site crews will ask for Ø 12/150 (754 mm²/m, 2.7×)
— over-provision is common, not free, and not a margin against the real
risks (headroom, uniformity, guard anchorage, formwork).

### 11.4 Anchorage into Podest/floor beam (digested values)

f_bd C20/25 good bond **2.32 N/mm²** (moderate 1.62 — assume moderate for
poorly vibrated sofits/permanent formwork [VERIFY]); **l_b = (Ø/4)(f_yd/f_bd):
Ø10 → 468 mm** ✓ matches digested table (47 cm); hook α = 0.7 → ≥ 328;
absolute minimum 300 mm tension [T3 digested α/modification rows — VERIFY];
direct bearing max(0.5 l_b, 150) ≈ 235 [T3 flagged print]. **Consequence:** a
150 mm plate end cannot hide a straight Ø10 anchorage — bend bars up into the
Podest (cross-anchorage, §12.2) or provide hooks; on the Bewehrungszeichnung,
not improvised on site.

### 11.5 Support traps

| Trap | Consequence | Fix |
|---|---|---|
| Lauf on a 100–115 mm partition later demolished | lost support | Never; note Lastabtragung on the drawing |
| Cantilever with bottom steel | cracks/collapses | Top steel, full l_b, back-span ≥ 2× cantilever |
| "Podest sits on walls" without Podest beam | Lauf unsupported at top; wrong span direction | Only with engineer-confirmed permanent structural walls both sides |
| Drilled dowels after frame pour | no continuity; tension-zone anchors | Cast with the deck or cast-in connectors |
| Wall on the Lauf soffit | unknown line load | Never / designed Unterzug |

## 12. Detailing and joints

### 12.1 Material, cover, pour

| Item | Value | Basis |
|---|---|---|
| Grade | C20/25 min interior; C25/30 exterior | [T3 digested exposure→grade table (XC3 C20/25, XF C25/30)] |
| Cover | 20 internal (c_min 10 + Δ_dev 10); 35–40 XF/XD | [T3 digested cover table; VERIFY per exposure] |
| Steps | monolithic with plate | cold joint at plate/step line = cracking tread |
| Props | soffit props **≥ 14 d**; not the 7-day slab rule | [T4 — stairs carry construction traffic] |
| Arbeitsfuge | at Podest only, never mid-flight; per DIN 1045-3 remove cement film, expose aggregate, roughen, pre-wet | [T3 digested joint rules] |
| Bewegungsfuge | DIN 18197 where long slabs demand it; core sits between joints | [T3 digested] |

### 12.2 Re-entrant corner — the stair detail everyone gets wrong

```
FLIGHT→PODEST where the corner OPENS OUT (tension face INSIDE the kink):
 ✗ Continuous bar around the inside corner: bar-force resultant pushes the
   cover OUT → spalling → bar straightens → joint hinges → flight drops.
   Brittle. Sudden.
 ✓ STOP each tension bar and ANCHOR into the COMPRESSION zone of the
   adjoining member: flight bottom bars bend UP into the Podest TOP face
   (full l_b); Podest bars bend DOWN into the flight soffit. Diagonal
   hairpin across the corner.
Corners that CLOSE: continuous bar acceptable; hairpin still good practice.
In a Halbwendung the open-out case occurs at ALL FOUR Lauf/Podest junctions.
```

See `concrete-detailing` for bend radii, bond conditions, α-factors.

## 13. Seismic — the stair is a stiff diagonal brace

An inclined concrete plate rigidly linking two floors is among the stiffest
elements in the building. Consequences: **(1)** it attracts seismic force far
above its mass share and drags it into the Podest beam and adjacent columns;
**(2)** the mid-Podest beam creates a **short column** (effective length
halved → stiffness ≈ 4× → shear demand ↑, brittle shear failure — classic
observed damage); **(3)** an off-centre core adds torsional irregularity.
**Do:** tell the Tragwerksplaner the stair exists, where, and how it bears —
never "architecture only" in the model; confine/ductile-detail the columns at
the Podest beam per EN 1998-1 capacity design [VERIFY zone per
DIN EN 1998-1/NA map]; where unwanted, **isolate the Lauf with a slip joint**
— an engineered detail, never a default. Cross-ref `seismic-design`.

## 14. Acoustic separation (Trittschall im Treppenhaus)

The digested DIN 4109-32 table for massive stairs (plate ≥ 120 mm) owns this
section — **the bearing detail, not the covering, decides** [T3]:

| Lauf/Podest detail | L_n,eq,0,w | L′_n,w (dB) |
|---|---|---|
| Podest cast into stiff single-leaf stair wall (m′ ≥ 380 kg/m²) | 63 | 67 |
| Lauf bonded (fest) into same wall | 63 | 67 |
| Lauf abgesetzt (set back, unbonded) | 60 | 64 |
| Podest with full building separation joint | ≤ 50 | ≤ 47 |
| Lauf decoupled + separation joint | ≤ 43 | ≤ 40 |
| **Lauf elastically supported on the Podest** | **35** | **39** |

Requirements (DIN 4109-1, digested [T3]): flights/landings in a dwelling
L′_n,w ≤ 53; floor over Keller/Hall/Treppen unter Aufenthaltsräumen ≤ 50;
Treppenhauswände R′_w ≥ 53 (wall with door: erf R′_w = R_w,door + 15);
row-house stairs ≤ 46; DIN 4109-5 (erhöht) stairs ≤ 47; VDI 4100 separated
stair 53/46. **Stair wall ≥ 410 kg/m² where a lift abuts (§17.6).**

Rules [T3 digested]: **Schalltrennfugen ≥ 30 mm**; elastic Lauf bearings;
Podest meets the requirement on its own (floating screed — floating screed
*on* flights is impractical); covering with ΔL_w → compute like any floor,
bare → table value; **fire rules often bar resilient coverings in notwendige
Treppenräume** (§15) — the classic acoustics-vs-Brandschutz clash, resolve
early. Full method: `building-acoustics`.

## 15. Fire and escape function (notwendige Treppe, Rettungswege)

Digested MBO/LBO fire chapter — **state LBO governs; VERIFY per Bundesland**
[T3]:

| Item | Rule |
|---|---|
| Routes | Every Geschoss with Aufenthaltsräume via a **notwendige Treppe**; every residence unit: **2 independent escape routes** (up to 2 storeys may share the notwendige Flur); first = notwendige Treppe; second = another stair, **or** appliance access (sill > 8 m needs suitable device), **or** waived by a **Sicherheitstreppenraum** |
| Exemptions | GK1–3 / ≤ 2 storeys ≤ 200 m² with different route per floor; stairs within one dwelling need no enclosure |
| Types | ramps allowed in escape stairs; folding stairs/escalators **not**; GK1–2 loft ladder only to unoccupied roof |
| Width | **≥ 100 cm** (DIN 18065; ASR A2.3) [T3]; wider per use [VERIFY] |
| Handrails | **both sides + intermediate rail on wide stairs**; **no door onto the flight**; Podest depth ≥ door width [T3] |
| Structure | GK5 fh + non-comb; GK4 non-comb; GK3 non-comb or fh; external stairs GK3–5 non-comb [T3] |
| Enclosure | own continuous shaft; walls GK5 Brandwand-type / GK4 hfh (under load) / GK3 fh; linings + insulation non-combustible; floors ≥ B1/schwerentflammbar; openings from Keller/ungedecktes Dach/storage > 200 m²: **fh + rauchdicht + selbstschließend**; to notwendige Flure: rsT; to dwellings: dT; glazing in/above fire+smoke doors ≤ 2.50 m wide [T3] |
| Ventilation | **≥ 0.5 m² openable per upper floor or ≥ 1 m² top exhaust** (GK5: both), operable from EG + top landing; safety lighting > 13 m [T3] |
| Travel | exit to stair/outside ≤ **35 m** from any dwelling point; stacked basements ≥ 2 exits; Vorraum: ≥ stair width, rsT doors to corridors, no other openings [T3] |
| Rescue window | clear **0.9 × 1.2 m**, sill ≤ 1.2 m [T3] |
| Lift | **never an escape route**; shaft walls GK5 fb+noncomb/GK4 hfh/GK3 fh; shaft smoke vent ≥ 2.5 % area & ≥ 0.10 m²; ≤ 3 lifts/shaft [T3] |
| Untertreppe store | no combustibles in the escape route; fh+rsT separation per enclosure row (§21) |

The continuous Handlauf has a smoke rationale: in zero visibility it *is* the
wayfinding — it must not stop and restart at the turn. Full system:
`fire-protection-building`.

## 16. Ramps (Rampen)

A Rampe serves who cannot step: wheelchairs, rollators, handcarts. Digested
escape-stair rule: **"ramps ok" as Rettungsweg**, folding/escalator types not
[T3]. **Gradient values are NOT in the digests** — DIN 18040 practice, all
VERIFY against the current edition:

| Item | Design value |
|---|---|
| Barrierefrei standard gradient | **≤ 6 %** (1:16.7) |
| Short steep exception | ≤ 10 %, both-side Handlauf, non-slip |
| Zwischenpodest | every ~6 m of run |
| Start/end field | ≥ 150 × 150 cm manoeuvre (120 × 120 barrierefrei w/ overlap) [T3 digested DIN 18040 areas] |
| Width | ≥ stair logic: 100 min / 120 recommended [VERIFY] |
| Surface | slip-resistant; tactile warning strips top/bottom |
| Old generic 1:12 (8.3 %) | inside "walkable" but outside DIN 18040 barrierefrei — the stair-adjacent ramp rule of thumb only [VERIFY] |
| ≥ 1:6 (16.7 %) | no longer a Rampe — steps or lift |

Ramp cost in area: ~1 m length per 17 cm rise, twice (plus landings). In a
MFH or any foreseeable mobility need, the answer is usually **stair + lift**,
not a long ramp. Full routes/handles/counters: accessibility skill
(DIN 18040-1 public, -2 dwellings).

## 17. Lifts (Aufzüge) — EN 81 sizing, shafts, fire mode

All data: digested building-services-tga chapter [T3]; verify against current
EN 81-1/ISO 8100-30 and state rules.

### 17.1 Requirement triggers

- **Height:** > 13 m (relevant storeys above entrance) → lifts "in
  ausreichender Anzahl" in most Länder; state variants: Berlin ≥ 4 OG,
  Bremen > 10.25 m, Niedersachsen > 12.25 m, NRW/RP > 5 storeys [VERIFY].
- **Barrierefrei:** unit-count/threshold triggers per state LBO →
  barrierefreier Aufzug (DIN 18040/EN 81-70) [VERIFY].
- **Hochhaus (> 22 m):** ≥ 2 (redundancy + firefighter lift per concept).
- **Escape:** a lift is never an escape route [T3].

### 17.2 Car sizes (EN 81-1 / ISO 8100-30)

| Load | Car W×D (m) | Pers. | Use |
|---|---|---|---|
| 320 kg | 0.90 × 1.00 | 1–2 | goods-grade only |
| 450 kg | 1.00 × 1.20 | 4 | tight existing shafts |
| **630 kg** | **1.10 × 1.40** | 8 | **stroller + wheelchair; accessibility minimum (EN 81-70)** |
| **1000 kg** | **1.10 × 2.10** | 13 | **stretcher + furniture; MFH standard** — covers ~260 users at the digested 20-persons traffic rule |
| > 20 pers. | +0.115 m²/person | — | beyond 1000 kg |
| Area caps | 1000 ≤ 2.40 m² · 1275 ≤ 2.95 · 1600 ≤ 3.56 · 2000 ≤ 4.20 · 2500 ≤ 5.00 (+0.16 m²/100 kg) | | max car height 2.20 m; door height 2.0/2.1 m |
| Doors | accessible clear ≥ 0.90 m (EN 81-70); ideal ≥ 1.10 m two-way | | |
| Pre-door | depth ≥ 1.5 × car depth (max 4.5 facing doors), min 1.5 m; stretchers 2.30 m; **never facing directly down stairs/ramp**; ≥ 0.5 m from corners | | [T3] |

### 17.3 Shaft: pit (Grube) and headroom (Schachtkopf)

- **Pit by speed:** hydraulic ≤ 0.4 m/s → **1.40 m**; 1.0 → **1.60**; 1.6 →
  **1.75**; 2.5 → 2.30–2.50; classes run 3.2–5.5 m (digested anchor ladder
  1.40/1.60/1.75/2.00/2.30/2.40/3.20/3.40/4.00/4.20/4.40/5.20/5.50)
  [VERIFY pairing vs EN 81-1].
- **Headroom:** ≤ 1.0 m/s → **3.6–3.8 m** above top OKFF; MRL →
  **3.70–4.40**; overrun = brake space + roof maintenance space.
- ≥ 3 lifts in one shaft: allowed, **+20 cm** per divider; sohl load ≥ 500
  kg/m² for below-pit access; accessible space under the pit → counterweight
  prop/arrester; below-pit access: 1.5–2.5 m ladder, > 2.5 m door ≥ 1.4 m.
- **Plan impact:** 1.4–1.6 m pit kills a Keller room under the shaft — bear
  the shaft on the cellar wall or lose the room; 3.7–4.4 m headroom pierces
  the roof — resolve with Dachausstieg/Technikraum (§18).

### 17.4 Drive systems

| System | Data [T3] |
|---|---|
| Machine room | lichte height ≥ 2.0 m; +5…+40 °C ventilated; exclusive (no through-route); access stair ≥ 70 cm; lifting hook ~1 t; drive/cabinet on springs; slab ≥ 25 cm + heavy walls + absorptive ceiling |
| MRL | drive in shaft wall; saves head/penthouse; slightly higher head (§17.3) |
| Hydraulic | pump ≤ 10 (max 25) m from shaft; room 3–8 m²; oil-tight floor + 10 cm threshold bunding + visible leak channel; hand-lowering (dead-man); ≤ ~150 trips/day (heat); backpack ≤ 10 m; avoid in public buildings (oil) |
| Traction | ropes: safety 16 (2 ropes)/12 (3); governor + progressive safeties; expert inspections ~2-yearly (DE) — vendor access from day 1 |
| Small goods | EN 81-31 goods-only anchors (car ≤ 2.5 m², ≤ 12 m thumb); **platform lift EN 81-41**: ≤ 0.15 m/s, ≤ 300 kg, ≥ 0.9 × 1.0 m (≤ 2 m²), 0.9 m rail, ≥ 1 m guarding; **stair lift EN 81-40**: ≤ 300 kg, folded intrusion 20–40 cm — recheck escape width + headroom (2.75 m storeys get tight) |

### 17.5 Firefighter lift and fire mode

- **Firefighter lift** (state high-rise rules + **EN 81-72**): car ≥ 1.10 ×
  2.10, mass **≥ 1800 kg** [digested print — VERIFY vs standard], door ≥ 90
  cm, stop every floor, set distance from every occupied-room door; cab +
  shaft ventilation (pressure-differential possible); fire-protected cables
  (E30) + emergency generator; Feuerwehr-Sperrschalter.
- **Recall & mode:** groups recall to entrance on mains failure (needs
  standby); **EN 81-73**: on alarm → designated landing (EG; alternate if
  alarmed), doors open, out of service until fire-service reset; car/plant
  batteries keep lighting + alarm only; 24 h emergency intercom; powerpack
  rescue where no genset.
- Shaft fire rating §15; machine room never a through-route.

### 17.6 Sound protection (DIN 8989 + DIN 4109)

Owned by the structural/acoustic planner — **the lift vendor is not liable**
[digested]:

- L_AF,max,n ≤ **30 dB(A)** in rooms ≤ 125 m³ (VDI 4100 30/27/24); night
  30 dB(A) lifts in dwellings/hotels/wards (DIN 4109).
- Structure-borne acceleration limit 90 dB @ 63 Hz (situation A).
- Single-leaf shaft wall masses by situation: **490/580/670/740 kg/m²**; or
  two-leaf + mineral-wool joint; **fully decoupled shaft = 30 mm joint +
  380/580 kg/m²**; light partition beside shaft → shaft to 580 kg/m²;
  plant-room walls 580–740; **stair wall ≥ 410**; flanking walls ≥ 220–260.
- **Never put the shaft against a bedroom/Wohnraum wall** — back it onto the
  Treppenhaus or Flur; otherwise the decoupled detail applies in full.

## 18. Stair + lift coordination — planning order

The core (Treppe + Aufzug + Schächte) is fixed **before** apartment layouts:

1. **Storey grid and OKFFs first** (§3 Step 1) — rises and lift stops inherit
   it; a late 50 mm finish moves 18 risers and every landing door head.
2. **Stair by its arithmetic** (§3.1/§8) — Halbwendung stacks per floor; the
   Treppenauge takes the first Installationsschacht.
3. **Shaft against the stair wall**, never a protected room (§17.6): pit vs
   Keller (§17.3), headroom vs roof + Dachausstieg, ≥ 1.5 m waiting area per
   landing (§17.2).
4. **Fire:** stair = escape (notwendiger Treppenraum at GK4/5); lift never
   escape; firefighter lift per concept; shared machine room with plant is an
   access yes / acoustics no without a real wall.
5. **Acoustics:** every Lauf bearing elastic or jointed (§14); every shaft
   wall a mass decision (§17.6) — resolve in the Rohbau, not the complaint
   meeting.
6. **Structure:** stair brace + shaft shear walls + opening trimmers to the
   Tragwerksplaner together.
7. **Accessibility:** 630 kg EN 81-70 minimum car; 1000 kg with Trage/stretcher
   demand; doors ≥ 90; level landings (DIN 18040).
8. Then let the Wohnungen breathe. A 200 mm narrower room is invisible; a
   relocated core is a year of planning.

## 19. Handrails and guards (Handlauf, Geländer, Brüstung)

### 19.1 Dimensional rules

| Item | Requirement | Basis |
|---|---|---|
| Where | both sides on the notwendige Treppe + intermediate rail on wide stairs | [T3 digested] |
| Handrail height | **90 cm** above the Setzgerade; Geländer 110 cm at large fall heights | [T4 German practice; VERIFY vs DIN 18065/LBO — old generic band was 864–965 mm] |
| Graspable | circular **30–45 mm**, wall gap ≥ 40–50 mm, continuous, returned at ends | [T4; old skill 32–51 mm carried] |
| Flat top rail ≠ Handlauf | 100×50 or 50 mm square cap not graspable — add a separate 40 mm grab rail | the most-violated rule |
| Geländer height design | ≥ 90 cm; **design 100 cm throughout** so one detail covers Lauf + Podeste | MBO § 38: 0.90 m for a fall height of 1 to 12 m, 1.10 m above; BGI 561: 1.00 m (S.3). State law decides |
| Window parapet (Brüstung) | ≥ 0.80 m up to 12 m fall height, ≥ 0.90 m above | MBO § 38 (S.3); state law decides |
| Openings | **no 120 mm sphere** [VERIFY vs DIN 18065; old 100 mm sphere carried]; design baluster gaps ≤ 100 mm; **vertical bars only** | child head rule |
| Bottom triangle | rail ≤ 100 mm above nosing line or infill down to it | practice |
| Extensions | +30 cm beyond Antritt/Austritt (altengerecht) | [T4] |
| Glass | laminated build-up per DIN 18008-4/-6, tested w/ post-breakage retention | VERIFY |

### 19.2 Design loads

No digested Geländer table. Use **EN 1991-1-1 §4.8** (line + point loads by
category, not concurrent) — **VERIFY current clause + NA.** The carried
old-skill envelope (**0.89 kN concentrated any direction; 0.73 kN/m uniform;
infill 0.22 kN on ~0.3 m square; not concurrent**) sits inside that family
and is the design envelope below.

### 19.3 Worked post check — steel post on RC plate

Posts @ 1100, height 1000, SHS 50×50×3, S235, C20/25 plate 150:
0.89 kN point governs (vs 0.73 × 1.1 = 0.80 kN uniform, not concurrent) →
M_base = **0.89 kNm**; Z = 8,340 mm³ → σ = 107 MPa vs f_y/γ_M0 = 235 →
**46 % ✓**; base plate 2 bolts @ 120 mm lever → **7.4 kN tension/bolt**; M12
post-installed, 100 mm embed + 100 mm edge into a 150 mm plate with 20 mm
cover → 30 mm behind the head → **marginal — PROBLEM**. **The detail:**
cast-in starters/sleeves at post positions, on the Schalplan, at the pour.
Post-drilling stair guards is the standard cause of wobbly — eventually
unsafe — guards. Same logic for wall brackets: ≤ 900 mm centres into solid
masonry/concrete, never hollow block or 12 mm Putz. Check the same loads on
the **slab edge** along the opening — a 150 mm edge without Randbalken is the
weak link.

## 20. Finishes, nosings, slip resistance (Stufenbelag)

| Item | Rule |
|---|---|
| Nosing | 20–30 mm Überstand, radius/bevel ≤ 15 mm; no square projecting nose; uniform |
| Under-nosing | ≤ 30° from vertical (shoe catch) |
| Slip | anti-slip inserts at stone/marble noses; wet/external: recognised class [VERIFY applicable use class] |
| Step cues | **50 mm contrast band at every nosing**; unmistakbarer Antritt/Austritt |
| Risers | closed on main stairs; open → 120 mm sphere + child argument (§19) |
| Build-up discipline | finish thickness fixed **before** §3 Step 1; a 35 mm change on one floor moves every level |
| Handlauf finish | wood/soft coat over steel |
| Escape stair flooring | ≥ schwerentflammbar im notwendige Treppenraum [T3 §15] — often blocks §14 resilient coverings |

## 21. Under-stair space (Untertreppe)

| Configuration | Soffit | Use |
|---|---|---|
| Straight flight | 0 → H wedge | store ≥ 2000 mm tall end; shoe bank mid; sealed void low end |
| **Dogleg, under Lauf 1** | 0 → ~1430 | store with door on tall face; **not a Bad/WC** |
| Under mid-Podest | ~1430 const | storage only — **never circulation under it** |
| L long leg | 0 → 2000+ | WC only if ≥ 2000 at fixture AND door swing |

Untertreppe-WC trap: works under a straight flight ≥ 4.5 m going, never under
a dogleg first leg. Enclosure walls = non-loadbearing Trennwände; the Lauf
must not bear on them (§11.5). Fire: a store inside the escape route needs
fh+rsT separation per §15 — regardless of byelaw, no combustibles in your
only escape route.

## 22. Accessibility / aging-in-place overlay (Barrierefreiheit)

Private dwellings aren't automatically under DIN 18040-1 (public space) — but
they are under *the client getting older* and newer LBO barrierefrei triggers
(§17.1). All DIN 18040 numbers **VERIFY current edition**:

| Measure | Standard | altengerecht/barrierearm |
|---|---|---|
| Rise | 175–190 | **160–170**, uniform, closed risers |
| Going | 260–280 | **≥ 300**, contrast nosing |
| Steps/Lauf | as designed | ≤ 12, Podest per run |
| Handrails | one side ok privately | **both sides, continuous, +30 cm ends**, high contrast |
| Width | 900–1050 | **≥ 1200 clear** — stairlift rail intrusion 200–400 mm folded (§17.4) still passes |
| Winders / spiral | allowed / secondary | **avoid / never** |
| Type | any | gerade or single-Podest L; curved stairlift rails cost multiples of straight |
| Lighting | switch both ends | step lights + presence sensors; level markings |
| Future home lift | — | reserve **≥ 1000 × 1400 mm** aligned void, both floors — retrofit = cutting the deck |
| Lift | optional | 630 kg EN 81-70 minimum car (§17.2) |

Ask any client over 50, unprompted: *"Stair you can use at 75 — or the
lift?"* It changes rise, width, possibly the plan; at design stage it is free.

## 23. Failure modes and anti-patterns

| # | Anti-pattern | Consequence | Fix |
|---|---|---|---|
| 1 | Riser count slab-to-slab | first/last step off; uniformity break | §3 Step 1 |
| 2 | Opening sized by eye | 1.8 m headroom after the pour | §5.2 every time |
| 3 | Winders about a point | narrow end ≈ 0 mm | §7.3 r_i ≥ 120/θ |
| 4 | Flat square top rail as Handlauf | not graspable in a fall | §19.1 grab rail |
| 5 | Guard posts drilled into finished plate | 7.4 kN into 30 mm concrete | §19.3 cast-in |
| 6 | Steeper roof stair | cadence break in one building | same s/a (§4) |
| 7 | Stair as construction-only model | short-column shear unseen | §13 |
| 8 | Lauf on partition / cantilever bottom steel / continuous open-corner bar | lost support / cracking / hinge-failure | §11.5, §12.2 |
| 9 | Door over the flight top | pushed backwards downstairs | §5.4 [T3] |
| 10 | Handlauf stops at mid-Podest | no support at the turn; lost in smoke | §15/§19 |
| 11 | Bad/WC under dogleg leg 1 | 1.43 m soffit | §21 |
| 12 | Spindeltreppe to save 4 m² | 213 mm rises; no Trage route | §9.3 say no |
| 13 | Polished treads | wet falls | §20 |
| 14 | Props struck at 7 d | sagging soffit forever | §12.1 ≥ 14 d |
| 15 | Horizontal balusters | toddler ladder | §19.1 vertical ≤ 100 |
| 16 | Rigid cast-in stair + "covering will fix it" | 67 dB drum under bedrooms [T3 §14] | §14 bearings |
| 17 | Shaft against bedroom | 30 dB(A) night limit lost | §17.6 |
| 18 | Reusing a worked example's winder/spiral margin | silently non-compliant layout | recompute §7.2/§9.2 |
| 19 | "We'll fix the last riser on site" | the §4.4 violation by 20–30 mm | recompute n; never |

## 24. Full worked example — Zweifamilienhaus stair, H = 3200 mm

Brief: EG + OG + DG; stair zone 3600 × 2400 against the shared wall; RC
frame, 200 mm decks; owners aging in place; later home-lift void wanted.

### 24.1 Geometry + layout (§3–§5, §8)

| Item | Value | Check |
|---|---|---|
| H OKFF→OKFF | 3200 | finishes stated |
| n = 18 → s = **177.8** | ≤ 190 ✓ [VERIFY] | 2s+a = 630.6; s·a = 48,895; pitch 32.9° |
| a = **275** | ≥ 260 ✓ [VERIFY] | +25 Überstand → 300 foot area |
| Going 4675 vs 3600 available | → **Halbwendung** (tree Q3) | 3300×2200 ≤ 3600×2400 ✓ |
| Split 9 + 9; rise/Lauf 1600; Lauf going 2200 | ≤ 12 ✓ | |
| Halb-Podest | 1050 (= Laufbreite) ≥ door width ✓ | [T3 door rule] |
| Lichte Breite | **1050** per Lauf (2×1050 + 100 Auge = 2200) | ≥ 1000 [T3] ✓ |
| Handrails both sides 900, continuous, wood-over-steel; wall gap 40 | §19 | |
| Geländer Auge-side 1000; vertical balusters 95 clear; no 120 sphere | §19 [VERIFY] | |
| Home-lift void | aligned 1000 × 1400, kitchen stack, both floors | §22 |

### 24.2 Headroom and openings (§5.2)

| Check | Result |
|---|---|
| OG soffit over lower OKFF | 3200 − 220 = 2980 |
| Lauf 2 runs 1600→3200 | **deck may not overhang Lauf 2 at all** |
| Treppenöffnung | full Lauf-2 plan + 100 = **2300 × 1150** (computed) |
| Under mid-Podest | 1600 − 220 = **1380 → storage only, marked on plan** |
| DG access | same s/a; ladder only if never an escape route |
| Door heads at opening | Podestträger upstand clash — coordinate |

### 24.3 Structure (§11–§14)

| Element | Design |
|---|---|
| Laufplatte | 150, C20/25, cover 20 XC1; p_Ed 15.15 → M_Ed 14.33 kNm/m |
| Main Ø 10/200 along slope (393 vs 275 req / 225 min); distribution Ø 8/150; support top steel Ø 10/200 over 0.25 l₀ | §11.3 |
| Anchorage | l_b φ10 468 good / 670 moderate; hook α 0.7; min 300 — cross-anchored into Podest |
| Re-entrant | cross-anchor + hairpin at **all four** junctions (§12.2) |
| Podest | 150, Ø 10/200 both ways, on 230 × 300 Podestträger [preliminary — engineer] |
| Seismic | **short column at 1600 flagged to Tragwerksplaner**; EN 1998 confinement (§13) |
| Acoustic | Läufe **elastically seated**, 30 mm Trennfugen to walls → 35/39 dB line (§14) |
| Pour | monolithic; Arbeitsfuge at Podest only; props ≥ 14 d |

### 24.4 Compliance summary

| Req | Required | Provided | ✓ |
|---|---|---|---|
| Steigung / Auftritt / 2s+a | ≤190 / ≥260 / 600–650 [VERIFY] | 177.8 / 275 / 630.6 | ✓ |
| Uniformity | equal | 18 identical from OKFF | ✓ |
| Breite | ≥ 1000 | 1050 × 2 | ✓ |
| Headroom | ≥ 2100 [VERIFY] | opening computed; worst > 2100 | ✓ |
| Podest depth / door rule | ≥ width & door width | 1050; door beside flight | ✓ |
| Steps per Lauf | ≤ 12 | 9 | ✓ |
| Plate / A_s / shear | ≥ 92; ≥ 275/225 mm²/m; V_Ed 20.8 | 150; 393; 49 | ✓ |
| Handrails / Geländer / sphere | both ≥ 90; no 120 sphere | 90 both; 100; 95 gaps | ✓ |
| Post anchorage | cast-in on Schalplan | §19.3 | ✓ |

> *Status line: preliminary stair set-out and sizing for coordination and
> FreeCAD modelling — requires Tragwerksplaner design/signature (Laufplatte,
> Podestträger, guard anchorage, short-column confinement) and Baugenehmigung
> under the applicable LBO before construction.*

## 25. FreeCAD modelling defaults and recipe

### 25.1 Defaults (metric)

| Parameter | Default | | Parameter | Default |
|---|---|---|---|---|
| OKFF→OKFF | **3200** | | Plate `StructureThickness` | **150** |
| Steigung | **177.8** (never round) | | TreadThickness | 50 |
| Auftritt / Nosing | **275 / 25 (r 12)** | | Podest depth | **1100** |
| Steps | **18 (9+9)** | | Treppenauge | **100** |
| Lichte Breite | **1050** | | Handrail / Geländer | **900 / 1000** |
| OG opening | **2300 × 1150** (§24.2) | | Baluster gap / HR target | **95 / 2100** |

### 25.2 Arch.makeStairs gotcha — rotation convention

```python
import Arch
st = Arch.makeStairs(4675, 3200, 1050)   # (length, height, width, ...)
```

The `rotated`/rotation arguments decide which horizontal axis the flight
climbs along, and the convention is **not stable across FreeCAD versions**.
**After every creation or rotation change, check `st.Shape.BoundBox`
(XLength/YLength/ZLength) and confirm the rise axis and footprint before
trusting the object.** Re-verify against the version in use. [VERIFY]

### 25.3 Recipe

1. Storey heights **first**; regenerate the stair if H changes — never nudge
   risers.
2. **Arch Stairs** object: `NumberOfSteps`, `RiserHeight`, `TreadDepth`,
   `Width`, `Nosing`, `TreadThickness`, `Structure` = Massive,
   `StructureThickness` = 150. Property names vary by version — verify.
3. Halbwendung = **two Arch Stairs + Podest slab**, grouped as one
   BuildingPart `Stair_EG_OG`.
4. Deck opening = **parametric Subtraction** (sketch-driven) on the upper
   slab, sized by §5.2 — must propagate with H.
5. **Verify headroom in the model:** nosing-line construction line offset
   +2100 mm; nothing intersects (soffit, beams, ducts).
6. **Model the Podest beam + columns** — the short-column object (§13) must
   exist or the engineer never sees it.
7. **Geländer/Handlauf as real objects** (Arch Railing along a path) — they
   eat 100 mm of width and reveal the true feel.
8. IFC: `IfcStair` > `IfcStairFlight` (per Lauf) + `IfcSlab` (Podest);
   `IfcRailing`; `IfcBeam` (Podestträger); lift shaft via wall elements.
   **Verify by export + re-read** — `IfcBuildingElementProxy` = never
   classified.
9. Model README: OKFF assumptions + finish build-ups, standards set (DIN
   18065/18040/LBO state, VERIFY tags), slab-depth basis (§11.2), §24.4
   status line.

### 25.4 Quantities (this example)

Concrete Läufe 2 × [(2.2 × 1.191 × 1.05 × 0.15) + (8 × ½·0.1778·0.275·1.05)]
≈ **1.15 m³**; Podest 2.2 × 1.05 × 0.15 ≈ **0.35 m³**; steel thumb rule
100–130 kg/m³ ≈ 150–200 kg; formwork ≈ 11 m²; Belag ≈ 9 m²; Handlauf
≈ 2 × 6.3 m both sides.

## 26. Verification checklist

**Geometry** — [ ] n from OKFF-to-OKFF, finishes stated [ ] all rises equal
[ ] a ≥ 260 / s ≤ 190 / 2s+a ∈ 600–650 [VERIFY DIN 18065] [ ] Breite ≥ 1000
on escape stairs, finished-face measured [ ] going fits with Podeste or
compliant turn via §8. **Headroom/opening** — [ ] §5.2 computed + recorded
[ ] ≥ 2.10 worst point vs slab/beams/ducts/lights [ ] mid-Podest soffit
noted; no circulation beneath if < 2.10 [ ] Dachzugang same s/a [ ] door
swings at both flight heads. **Flights/Podeste** — [ ] Podest ≥ width and ≥
door width; no door onto flight [ ] ≤ ~18/Lauf [ ] winders r_i ≥ 120/θ +
Gehlinie check recomputed *for this layout* [ ] spiral use case on §9.3 ✅
list. **Structure** — [ ] plate ≥ l₀/30 + practice floor; spans > 3.6 m
re-structured [ ] slope factor + step triangles in loads; 3.0 kN/m² + 2.0 kN
point [ ] A_s ≥ calc & min; distribution ≥ 20 %; top steel over Podest beam
[ ] l_b/hook/300 checked at supports [ ] re-entrant cross-anchorage at every
open-out corner [ ] no Lauf on non-structural walls; load path noted [ ]
Podest beam + columns modelled; **short column flagged to engineer** [ ]
Arbeitsfuge at Podest; props ≥ 14 d. **Acoustics** — [ ] elastic/jointed
bearings, Trennfuge ≥ 30 [ ] Podest floats alone [ ] DIN 8989 masses checked
[ ] covering-vs-fire conflict resolved. **Handrails/guards** — [ ] both sides
where required; 90/100 heights; graspable; continuous, returned [ ] vertical
infill ≤ 100 gaps, no 120 sphere [ ] §19.2 loads on posts + **slab edge at
the opening** [ ] cast-in starters on Schalplan. **Fire/escape** — [ ]
enclosure class per Gebäudeklasse; rsT doors [ ] 0.5/1.0 m² vent rule
[VERIFY state] [ ] no unprotected store opening [ ] 35 m travel; second-route
or Sicherheitstreppenraum decision [ ] lift never counted as escape.
**Lifts** — [ ] car/door/waiting-area per §17.2 [ ] pit vs Keller, headroom
vs roof [ ] ≥ 3/shaft +20 cm; sohl/under-pit access [ ] EN 81-72/-73 scope
with Brandschutz plan [ ] vendor shaft layout before fixing walls.
**Handover** — [ ] *preliminary — Tragwerksplaner + Baugenehmigung* label
[ ] every VERIFY tag re-opened against the current DIN/EN/LBO edition
[ ] assumptions in model README.

## 27. Known gaps (state when relevant)

1. **DIN 18065 clause values not in the digests** — only the ≥ 100 cm width
   anchor and terminology (Gehlinie etc.) are carried. Every step/width/
   headroom/handrail/120 mm-sphere figure tagged VERIFY must be re-read from
   current DIN 18065; the previous skill's values came from non-German codes
   and are kept only where aligned with German practice.
2. **State-LBO divergence** — escape widths by users, winders on escape
   stairs, enclosure triggers, lift-obigation heights (13 m vs 4 OG vs 5
   OG…), barrierefrei thresholds: verify the Bundesland's LBO.
3. **DIN 18040 ramp gradients are practice values here** — none digested.
4. **EN 1991-1-1 §4.8 guard loads not digested** — the 0.89 kN / 0.73 kN/m /
   0.22 kN envelope is carried-over; compute from the clause.
5. **Lift data is a planning digest, not a vendor layout** — the digested
   print itself flags uncertainty (firefighter-car mass, low-speed pit
   anchors); get the vendor shaft drawing before fixing the shaft.
6. **EN 81-72 trigger thresholds + shaft ventilation sizing** — fire-concept
   items, `fire-protection-building` + Brandschutzfachplaner.
7. **Helical/curved in-situ stairs** — structurally out of scope
   (bending + torsion), engineer-only.
8. **Winder narrow-end value (120 vs 152 mm) and Gehlinie position per width
   class** — carried at two practice levels; resolve per DIN 18065.
9. **Timber/steel stairs** — system selection + practice sizes only;
   `timber-steel-design` for verification.
10. **Stairlift/home-lift intrusion figures** — indicative; confirm per
    product before reserving space.

## Cross-references

| For… | Skill |
|---|---|
| Escape routes, ratings, Sicherheitstreppenraum, Hochhaus | `fire-protection-building` |
| Trittschall/Luftschall proofs, flanking | `building-acoustics` |
| Anchorage, laps, cover, bending, joints | `concrete-detailing` |
| Frames, storey grids, Podest beams | `structural-systems` |
| Stair brace, short columns, ductile detail | `seismic-design` |
| Lift plant, machine-room ventilation, Ersatzstrom | `building-services-tga` |
| DIN 18040 route design in depth | accessibility (DIN 18040) library skill |
| Core placement, circulation | `building-planning-spatial` |
| LBO per Bundesland, Genehmigung, Abweichungen | `building-regulations-permits` |
| Parametric BIM objects, IFC checks | the FreeCAD/BIM library skill |
| Quantities, rates | cost-management-din276 library skill |

*End of skill. When a number decides a submission or a signed Nachweis, open
the current DIN 18065 / state LBO / Eurocode NA and re-derive it there.*

---

## Appendix S: Source Check 2026-10 — values re-read from the literature

Each line below was read again in the source books (`sources/`) in October 2026, with the
place it stands at. "Confirmed" means: a dated book prints the rule and names the standard
or law; it does not mean the current edition of that standard was opened. State law
(LBO) and local rules still override; `VERIFY` tags elsewhere in this skill stay in force
unless a line here names the edition. Where a line here differs from a section of this
skill, that section was corrected and names the line ("S.n"); the appendix governs.

### S.1 DIN 18065 — limits by building (table as printed in the book)

| Building | Stair | Rise mm | Going mm | Usable width cm |
|---|---|---|---|---|
| Dwelling house with at most 2 dwellings | necessary stair | 140 to 200 | 230 to 370 | 80 |
| Dwelling house with at most 2 dwellings | not necessary | 140 to 210 | 210 to 370 | 50 |
| Other buildings | necessary stair | 140 to 190 | 260 to 370 | 100 |
| Other buildings | not necessary | 140 to 210 | 210 to 370 | 50 |

— *Bausanierung* Tab. 13.1. The targets of §3 and §4 (rise 175, at most 190; going from
260) are the comfort values of this skill and lie inside the table.

### S.2 Headroom, flights, width

- Confirmed: clear headroom of a stair at least 2.00 m (MBO and DIN 18065). — *Bausanierung*
  13.1.3. The 2.10 m of §5.1 is a design target, not the standard.
- Confirmed: a flight has at most 18 steps and at least three; the usable width in dwelling
  houses is taken as at least 1.0 m, small-house straight stairs down to 0.85 m. —
  *Bausanierung* 13.2.1.

### S.3 Guards and window parapets

- Confirmed (MBO 2016-05 § 38): window parapets with a fall height up to 12 m at least
  0.80 m high, above 12 m at least 0.90 m; guards of areas with a fall height of 1 m to
  12 m must be 0.90 m high, above 12 m 1.10 m. — *Bausanierung* 14.6.5.
- Confirmed (BGI 561, workplaces): guard height at least 1.00 m up to a fall height of
  12 m, 1.10 m above; horizontal force at least 500 N/m. — *Bausanierung* 13.6.1.
