---
name: concrete-detailing
description: >
  Reinforcement detailing (Bewehrungsplanung/Bewehrungsführung) for cast-in-place and
  precast reinforced concrete per DIN EN 1992-1-1 + Nationaler Anhang: bar scheduling
  (Stabsatz), concrete cover by exposure class (X0/XC/XD/XS/XF/XA/XM, cmin/Δcdev/cnom),
  anchorage l_b,netzlängen and the fbd/l_b numeric tables for B500 in C20/25–C50/60,
  lap splices (l_0, α-factors, stagger classes), Lagermatten/mesh overlap lengths per
  DIN 488-2, minimum reinforcement As,min = fct,eff·Ac,min/σs (biegezug + quertzug,
  crack-width bar/space limits), bar spacing and congestion checks (bars per layer in
  20–30 cm beams), shear and torsion stirrup detailing (ρw,min, s_max, closed links),
  slab field/support band rules, footing and wall detailing, column link zones,
  welded vs threaded splices, Weiße Wanne (WU) design with BKL/NKL/EGS classes,
  w_k targets 0.15–0.4 mm, waterbar and construction-joint sealing detailing,
  creep/shrinkage values, bar bending schedule format, modelling rebar in FreeCAD
  (Arch.makeRebar — Direction defaults to zero, bounding-box tolerance must include
  bar diameter) and IFC cover/marking export via the freecad-mcp connector
  (neka-nat/freecad-mcp). DACH practice. Not a design tool — see Reality Check.
---

# Concrete Reinforcement Detailing (DIN EN 1992-1-1 + NA)

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

This skill converts Eurocode-2 detailing requirements (German application rules,
Nationaler Anhang) into usable numbers for building-scale reinforced concrete:
slabs, beams, columns, walls, footings, water-retaining basements, and the rebar
model that feeds a FreeCAD/BIM model, a reinforcement schedule (Bewehrungsplan /
Stabsatz), or a bar-bending order. It exists so that a model or schedule produced
during design carries realistic bar diameters, realistic cover, realistic lap and
anchorage geometry, and detailing that a specialist reinforcement planner
(Stahlbaufachplaner) or a responsible structural engineer (Tragwerksplaner) would
not have to redraw from scratch.

Every numeric value below is tagged:

- **[EC2]** / **[NA]** — from DIN EN 1992-1-1 and its German National Anhang as
  carried in the source digests.
- **[DIN 488]** — reinforcing steel product / welded-mesh standards.
- **[WU-RL]** — DAfStb Waterproofing Concrete Guideline (Richtlinie „Wasserdurchlässiger
  Beton"), white-tank design.
- **[practice]** — industry convention, not a code clause.
- **[VERIFY]** — the exact table value or clause must be re-read in the primary
  standard before being quoted to a client, authority, or fabrication shop. Values
  transcribed from secondary tabular sources carry this tag liberally; the standards
  move (NA editions, DIN 1045 restructure 2023/24, WU-RL 2017 → 2023), so re-check
  the current edition of every clause used on a live project.

---

## Reality Check — Haftung & Responsibility

**This skill produces detailing aids and modeling guidance for planning and FreeCAD
modeling ONLY. It is not a structural design and not a reinforcement design.**

- Reinforcement design and detailing (Bewehrungsplanung) for a real structure is
  executed, checked and assumed as own work (eigene Verantwortung, Haftung) by a
  qualified reinforcement planner (Stahlbaufachplaner / Bewehrungsplaner) and is
  part of the Tragwerksplanung carried by a bauvorlageberechtigter Engineer /
  Tragwerksplaner under the applicable state building code (MBO/LBO). In the
  Prüfstatik system the Tragwerksplaner plans, a Prüfingenieur für Standsicherheit
  checks — both sign; nobody downstream can substitute for those signatures.
- Rebar drawn in a BIM model is geometry, not a design check. A member that looks
  right in 3D can still be unsafe. FreeCAD performs **no** Eurocode checks: no
  anchorage, lap, cover or congestion verification runs unless you implement it.
- **Say this unprompted.** If a user starts talking as though the output is final —
  asks for a Stabsatz to hand to a steel-fixing shop (Biegelei), asks "how much
  steel should I order", says "we're pouring next week", asks to send the rebar
  drawing to the contractor, or asks for anything that looks stamped or approved —
  stop and state plainly that a licensed Tragwerksplaner and a specialist
  Bewehrungsplaner must produce and take liability for the reinforcement design.
  Do not wait to be asked.
- **Never fabricate a signature, license number, Prüfstatik reference, ETA/Zulassung
  number, or approval note**, and never format output so it could be mistaken for
  an approved rebar drawing or a stamped schedule.
- Durability, fire and waterproofing detailing shown here are minimum-rule aids.
  Exposure classification of the actual structure (carbonation, chloride, frost,
  chemical attack, groundwater aggressivity per DIN 4030) is a project decision
  with site investigation behind it — never invented from a table.
- Seismic ductile detailing (EC8/NA: confinement, capacity design) is **out of
  scope and not digested here**; where a seismic design exists, its special
  detailing rules override the ordinary spacing/slice rules in this skill.

---

## Tier Structure — What Governs What

Apply in this order; a higher tier may tighten, never silently relax, a lower one.

| Tier | Source | Covers | Trust level for numbers |
|---|---|---|---|
| **T1** | DIN EN 1992-1-1 (EC2) + Nationaler Anhang (NA) | cover, anchorage, laps, min reinforcement, shear detailing, member construction rules, crack widths | code — use as-is only with current edition check |
| **T2** | DIN 488 (Betonstahl B500A/B, Matten, Bewehrungsdraht, Gitterträger) + BMD detail standard (Bewehrungsplan convention) | bar designation, mesh types & lap tables, delivery & bending geometry, schedule format | product standard — exact tables must be read from DIN 488-1/-2 [VERIFY] |
| **T3** | DAfStb rules & guidelines: WU-Richtlinie (waterproof concrete), execution rules DIN EN 13670/DIN 1045-3, (DIN 1045-1000 BBQ classes from 2023/24) | Weiße Wanne, execution tolerances, QA levels | guideline — edition-sensitive [VERIFY] |
| **T4** | Empirical practice: site rules of thumb, typical ratios, FreeCAD modeling conventions | ordering, congestion sanity checks, modeling | labeled **[practice]**, never for proof |

Pick one system and stay in it: a drawing that quotes EC2 cover with legacy
DIN 1045-1 laps, or WU-RL 2017 joint details with WU-RL 2023 crack targets,
fails review not on safety but on internal inconsistency.

---

## Section 1: Materials & Design Values (Rechenwerte)

### 1.1 Concrete — design values ULS (αcc = 0.85, γc = 1.5)

fcd = αcc·fck/γc [EC2 3.1.6]. Dry-storage correction vs. reference curing:
×0.92 normal concrete / ×0.95 high-strength [NA practice, VERIFY].

| Class | fck / fck,cube / fcm [N/mm²] | fctm / fctk,005 / fctk,095 | fcd [N/mm²] | fct,d [N/mm²] | Ecm [MPa] |
|---|---|---|---|---|---|
| C12/15 | 12/15/20 | 1,1/1,1?/2,0 | 6,80 | 0,62 | 27000 |
| C16/20 | 16/20/24 | 1,9/1,3/2,5 | 9,07 | 0,76 | 29000 |
| C20/25 | 20/25/28 | 2,2/1,5/2,9 | 11,33 | 0,88 | 30000 |
| C25/30 | 25/30/33 | 2,6/1,8/3,3 | 14,17 | 1,02 | 31000 |
| C30/37 | 30/37/38 | 2,9/2,0/3,8 | 17,00 | 1,15 | 33000 |
| C35/45 | 35/45/43 | 3,2/2,2/4,2 | 19,83 | 1,27 | 34000 |
| C40/50 | 40/50/48 | 3,5/2,5/4,6 | 22,67 | 1,39 | 35000 |
| C45/55 | 45/55/53 | 3,8/2,7/4,9 | 25,50 | 1,51 | 36000 |
| C50/60 | 50/60/58 | 4,1/2,9/5,3 | 28,33 | 1,62 | 37000 |

(C12/15 fctm cell garbled in source — use 1,1 [VERIFY]. fct,d row label reconstructed
as αcc·fctk,005/γc — matches C12/15 and C25/30 exactly, treat row as [VERIFY].)
Design strains (parabola-rectangle / bilinear): εc2 = 2,0‰, εcu2 = 3,5‰, εc3 = 1,75‰
(all classes ≤ C50/60) [EC2 3.1.7, Table 2.2/NA]. C12/15 permitted only for
predominantly static loading. Unit weights: Beton 24, Stahlbeton 25 kN/m³ [DIN EN 1991-1-1/NA].

### 1.2 Reinforcing steel — DIN 488, B500

| Product | Grade | φ [mm] | fyk | ftk/fyk | εuk | Redistribution (Umlagerung) |
|---|---|---|---|---|---|---|
| Ribbed bar (gerippt), straight & coil | **B500B** | 6–40 (6 8 10 12 14 16 20 25 28 32 40) | 500 | 1,08 | 5,0% | ≤30% [EC2 3.2.1] |
| Ribbed bar, normal ductility | B500A | 6–40 | 500 | 1,05 | 2,5% | ≤15% |
| Welded mesh wire | B500A/B | 4–12 (A) / 4–16 (B) | 500 | as above | — | — |

- Ribbed bars for main reinforcement are **B500B only** in current DIN 488-2 practice;
  smooth round bar is limited to stirrups/wire [DIN 488, VERIFY grade availability].
- Delivery lengths: bars typically 6 m / 12 m, coil straightened-and-cut — order
  length matters for the lap count in [Section 12]. [practice]
- Design values (γs = 1.15): **fyd = 435 N/mm²**, ftd = 456 (B500A) / ~470 (B500B);
  Es = 200 000 MPa; εyd = fyd/Es = 2,175‰; εud design = 25‰/γs → A / 50‰ → B [VERIFY strain limit use].
- Prestressing steel (γp = 1.15): ST 1470/1670 fpk,fpd = 1670/1452; 1570/1770 → 1770/1539;
  1660/1860 → 1860/1617 N/mm²; Ep = 195–205 GPa [DIN 488-4 context, VERIFY].

### 1.3 Partial factors and combinations (context for detailing checks)

γc = 1,5 (1,15 extraordinary; factory-precast member production case NA-permitted
1,15 [VERIFY]), γs = 1,15 (1,0 extraordinary). Actions: γG 1,35/1,00, γQ 1,50/0.
ψ for buildings: A/B 0,7/0,5/0,3; C/D 0,7/0,7/0,6; E 1,0/0,9/0,8; F(≤30kN) 0,7/0,7/0,6;
snow ≤1000 m 0,5/0,2/0; wind 0,6/0,2/0 — quasi-permanent values drive crack-width
(σs,perm) and deflection checks. [EC2/NA 2.4 + EN 1990/NA]

---

## Section 2: Bar Designation System (DIN 488) & Steel Tables

### 2.1 Product families

| German name | EN gloss | DIN 488 part | Use |
|---|---|---|---|
| Betonstabstahl | ribbed reinforcing bar | -1/-2 | main bars, bent bars |
| Betonstahl in Ringen | bar in coils (straightened at fab) | -1/-2 | 6–16 mm economy |
| Betonstahlmatten (Q/R) | welded wire mesh | -2 | slabs, mat footings, wall skins |
| Bewehrungsdraht | reinforcement wire (cold-worked) | -3 | fabricator-made cages, links |
| Gitterträger | open welded girder truss | -5 | half-precast composite slabs |

Mesh codes: **Q** = equal bar area both directions, **R** = different [DIN 488-2].
Suffix A/B denotes which layer is the outer/primary one; bond-zone suffix (e.g.
„A" = Zone 1, „B" = Zone 2 in the classic Q/R nomenclature) changes the required
overlap — never mix A and B variants in one lap decision [VERIFY exact DIN 488-2
suffix meaning before ordering].

### 2.2 Bar areas and unit mass (geometry, computed)

Mass per metre = π/4·φ²·7,85 g/cm³ ≈ φ²/162 (φ in mm) — matches the digested table.

| φ [mm] | 6 | 8 | 10 | 12 | 14 | 16 | 20 | 25 | 28 | 32 |
|---|---|---|---|---|---|---|---|---|---|---|
| A [mm²] | 283 | 503 | 785 | 1131 | 1539 | 2011 | 3142 | 4909 | 6158 | 8042 |
| A [cm²] | 0,283 | 0,503 | 0,785 | 1,131 | 1,54 | 2,01 | 3,14 | 4,91 | 6,16 | 8,04 |
| kg/m | 0,222 | 0,395 | 0,617 | 0,888 | 1,21 | 1,58 | 2,47 | 3,85 | 4,83 | 6,31 |

### 2.3 Slab bar area by spacing (cm²/m, computed)

Full digested grid spans 5–25 cm; the practical rows:

| s [cm] | φ6 | φ8 | φ10 | φ12 | φ14 | φ16 | φ20 | φ25 |
|---|---|---|---|---|---|---|---|---|
| 10 | 2,83 | 5,03 | 7,85 | 11,31 | 15,39 | 20,11 | 31,4 | 49,1 |
| 12,5 | 2,26 | 4,02 | 6,28 | 9,05 | 12,31 | 16,09 | 25,1 | 39,3 |
| 15 | 1,89 | 3,35 | 5,24 | 7,54 | 10,26 | 13,41 | 20,9 | 32,7 |
| 20 | 1,41 | 2,51 | 3,93 | 5,65 | 7,70 | 10,05 | 15,7 | 24,5 |
| 25 | 1,13 | 2,01 | 3,14 | 4,52 | 6,16 | 8,04 | 12,6 | 19,6 |
| 30 | 0,94 | 1,68 | 2,62 | 3,77 | 5,13 | 6,70 | 10,5 | 16,4 |

### 2.4 Welding (EC2-NA 8.10 / DIN 488 context)

Weld types for bars: RA 24 (butt, tension+compression, predominantly static);
E 111 / MAG 135/136 butt & lap/cross with additional conditions; FR 42;
RP 21 lap/cross ≤ 28 mm. **Only RA 24, E 111, MAG 136 may be used in non-
predominantly-static members** (fatigue). Diameter difference max one size.
ISO 4063 process numbers. [NA 3.2.5 / EC2 8.10, VERIFY clause]

---

## Section 3: Concrete Cover (Betondeckung) & Exposure

Cover is measured to the **outermost** steel (link/matte wire, not main bar) and
serves durability, bond and fire simultaneously. In Germany the durability value
is nominal cover cnom = cmin,dur + Δcdev, with cmin,b ≥ φ and ≥ 1,25·dagg.

### 3.1 Exposure classes (DIN EN 206-1/DIN 1045-2; EN 206:2021 not yet introduced in DE at digested edition — VERIFY current status)

| Class | Meaning | Typical building member |
|---|---|---|
| X0 | no corrosion/frost risk | unreinforced footings, very dry interior (RH ≤ 30%) |
| XC1 | dry or permanently wet | interior slabs/beams/columns, immersed surfaces |
| XC2 | wet, seldom dry | water-tank bases, cellar footings |
| XC3 | moderate moisture | exterior with air contact, kitchens/laundries, membrane-covered flat roofs |
| XC4 | alternating wet/dry | rain-exposed façades/edges, splash zones |
| XD1–XD3 | chloride (de-icer/brine), rising severity | garage ramps, de-iced decks |
| XS1–XS3 | sea chloride | coastal, tidal-splash |
| XF1–XF4 | frost without/with de-icer, rising saturation | balconies, paving, bridge decks |
| XA1–XA3 | chemical attack | sewage, slurry, aggressive ground (sulfate > 200/600/3000 mg/l; pH 6,5–5,5/5,5–4,5/4,5–4,0; aggressive CO2 15–40/40–100/>100 mg/l; Mg 300–1000/1000–3000/>3000) |
| XM1–XM3 | abrasion | forklift floors (pneumatic/solid/track) |

Moisture classes for ASR: WO (mostly dry) / WF (frequently wet) / WA (wet + alkali
supply) / WS (only TL Beton-StB). Assignment example: XC1→WO, interiors; exterior
unprotected → WF/WA. [DIN 1045-2]

### 3.2 Minimum cover — durability (EC2-NA cmin,dur values)

| Exposure | cmin,dur [mm] | Δcdev [mm] | cnom (=cmin+Δcdev) |
|---|---|---|---|
| X0 | 10 | 10 | 20 [VERIFY X0 cell — not fully recovered] |
| XC1 | 10 | 10 | 20 |
| XC2 | 20 | 15 | 35 |
| XC3 | 20 | 15 | 35 |
| XC4 | 25 | 15 | 40 |
| XD1/XD2/XD3 | 40 | 15 | 55 |
| XS1/XS2/XS3 | 40 | 15 | 55 |
| XF1/XF2/XF3/XF4 | 25…35 | 10/15 | [VERIFY per NA table 8.36 — cells partially recovered] |
| XA1/XA2/XA3 | 25…40 | 10/15 | [VERIFY] |

Rules:
- Δcdev = 10 mm if cmin ≤ 15 mm, else 15 mm [EC2 4.4.1.2].
- cmin ≥ largest bar φ and ≥ 1,25·max aggregate size [EC2 4.4.1.2].
- **−5 mm reduction permitted if concrete two strength classes above the minimum
  for the class** (not for XC1; plant-controlled QC case) [NA, VERIFY].
- Cover-from-bond alternative (cmin,b on deformed bar = φ) allowed only with
  documented execution control [NA table 8.37, values stripped — VERIFY].
- **Tolerances are NOT in cnom**: execution deviation class 1 standard; the
  construction tolerance (Ausführungsklasse, DIN EN 13670/DIN 1045-3) is a
  separate −/−10 mm/−15 mm allowance — choose per BBQ/DIN 1045-1000 if in force
  [T3, VERIFY].

### 3.3 Practical cnom schedule for buildings [practice, ≥ EC2 minima]

| Element | Exposure | cnom to link/wire | Note |
|---|---|---|---|
| Interior slab (top & bottom) | XC1 | 20 | 15 only with bond-based cmin — risky under cover-block scatter |
| Roof slab / balcony | XC3/XC4 (+XF1) | 35–45 | frost + de-icer salts from sealant failures |
| Beam / column interior | XC1 | 20–25 | 25 typical for fire + handling margin |
| Basement wall outside | XC2 (+XA if aggressive ground) | 35 | WU: 35–50 both skins [WU-RL] |
| Footing bottom on blinding | XC2 | 50 (≥35) | blinding ≥ 5 cm C12/15; never on soil [practice] |
| Garage ramp, exterior paving | XC4/XF3/4 | 40–50 + air-entrained | LP mandatory XF2+ |
| Water-retaining (tank) | XC2/XA | 35–45 | WU rules §9 of this file |

Historical note [T4, baukonstruktion]: pre-modern cover was ≥25 mm; today 30–40 mm
is normal for exposed members — under-cover is the most common defect found on
site and unrecoverable after the pour. Fire: cover also buys time (concrete λ
≈ 2,1–2,3 W/(m·K), steel fails ~600 °C); typical tabular fire a_min values are
25–45 mm — read DIN EN 1992-1-2 tables, do not mix fire and durability cover
without checking which governs (the larger wins).

### 3.4 Cover enforcement (execution)

- Manufactured cover blocks / plastic spacers, correct class, correct thickness;
  never brick chips or offcuts. Spacing: slab ~6–8/m², beam sides ~3/m, column
  faces ~4/m height [practice].
- Top bars need chairs (Hängetragen/Sitter): ≥ 12 mm wire, ~1/m grid; walked-flat
  top steel is the classic support-cracking mechanism [practice].
- Aggregates: max size ≤ 1/3 (better 1/4) of smallest member dimension, and must
  clear bar spacing by ≥ 5 mm [DIN 1045-2] — so 0/16 or 0/8 mixes in congested or
  thin members (WU walls with 0/16 lower several requirements, see §9).

---
## Section 4: Anchorage (Verankerung) — Netzlängen l_b

A bar is only as good as its anchorage. The full chain:

```
l_b,rqd = (φ/4) · (σsd / fbd)            σsd = fyd at full utilization (435 B500)
l_b     = αa · (As,erf/As,vorh) · l_b,rqd   ≥  l_b,min
l_b,min = max(0,3·l_b,rqd ; 10φ ; 100 mm)  (tension)
l_b,min = max(0,6·l_b,rqd ; 10φ)           (compression) [EC2 8.4, VERIFY min cells]
```

The ratio (As,erf/As,vorh) is the permitted area reduction: anchoring more steel
than needed shortens the required net length. Never reduce below the minimum.

### 4.1 Basic bond strength fbd (ribbed B500, φ ≤ 32; η0 = η1 = 1)

Digested table (NA fbd table). NA formula basis: fbd = 2,25·η0·η1·fctk,005/γc
with "good"/"moderate" bond conditions — **the tabulated values below are the
authoritative numbers of this file; the formula reconciliation is [VERIFY]**.

| fck | C12/15 | C16/20 | C20/25 | C25/30 | C30/37 | C35/45 | C40/50 | C45/55 | C50/60 | ≥C55/67→C60 |
|---|---|---|---|---|---|---|---|---|---|---|
| fbd gut [N/mm²] | 1,65 | 2,00 | 2,32 | 2,69 | 3,04 | 3,37 | 3,68 | 3,99 | 4,28 | 4,43 / 4,57 (constant >C60) |
| fbd mäßig [N/mm²] | 1,16 | 1,40 | 1,62 | 1,89 | 2,13 | 2,36 | 2,58 | 2,79 | 2,99 | 3,10 / 3,20 |

- φ > 32 mm: multiply fbd by 32/φ (reduced confinement per rib spacing).
- Bond condition (Verbundbedingungen): "good" = bar with ≤ 30 cm of fresh concrete
  cast beneath it (upward) or ≤ 15 cm in any other direction-of-casting situation;
  otherwise "moderate" [NA bond-condition table, exact cells stripped — VERIFY the 30/15 cm
  wording against EC2 8.4.2 before relying on top-vs-bottom distinctions].
  Practical rule [practice]: slab/beam TOP bars in deep pours and all vertically
  cast "top bars" → use mäßig (× 1/0,7 ≈ 1,4 longer).

### 4.2 Required net anchorage length l_b,rqd = (φ/4)(fyd/fbd) — B500, good bond [cm]

| φ | C20/25 | C25/30 | C30/37 | C35/45 | C40/50 | C50/60 |
|---|---|---|---|---|---|---|
| 6  | 28 | 24 | 21 | 19 | 18 | 15 |
| 8  | 37 | 32 | 29 | 26 | 24 | 20 |
| 10 | 47 | 40 | 36 | 32 | 30 | 25 |
| 12 | 56 | 48 | 43 | 39 | 35 | 31 |
| 14 | 66 | 57 | 50 | 45 | 41 | 36 |
| 16 | 75 | 65 | 57 | 52 | 47 | 41 |
| 20 | 94 | 81 | 71 | 64 | 59 | 51 |
| 25 | 117 | 101 | 89 | 81 | 74 | 64 |
| 28 | 131 | 113 | 100 | 90 | 83 | 71 |

Moderate bond (mäßig) — multiply by ≈ 1,43 [digested mäßig columns]:

| φ | C20/25 | C25/30 | C30/37 | C35/45 | C40/50 | C50/60 |
|---|---|---|---|---|---|---|
| 8  | 54 | 46 | 41 | 37 | 34 | 29 |
| 10 | 67 | 58 | 51 | 46 | 42 | 36 |
| 12 | 80 | 69 | 61 | 55 | 51 | 44 |
| 16 | 107 | 92 | 82 | 74 | 67 | 58 |
| 20 | 134 | 115 | 102 | 92 | 84 | 73 |
| 25 | 167 | 144 | 128 | 115 | 105 | 91 |
| 28 | 187 | 161 | 143 | 129 | 118 | 102 |

Sanity case: slab φ10@12,5 in C30/37, good bond → l_b,rqd = 36 cm — roughly three
bar-lengths of a room; at an interior support that is easily mis-fitted, which is
why end-anchorages and α-reductions below matter.

### 4.3 Anchorage-type factor αa (EC2 8.4.3 / NA detail set)

Canonical EC2 chain for the record: l_b = α1·α2·α3·α4·α5·α6·l_bd,rqd, with
l_bd,rqd = (φ/4)·fyd/fbd; α1 bond quality, α2 spalling cover, α3 transverse
reinforcement, α4 welded transverse bar, α5 confining pressure, α6 bar in
compression. The digested German tables fold α1 into the gut/mäßig fbd rows and
use one αa product per detail — state which convention a drawing follows
[VERIFY clause mapping].

| Detail | αa |
|---|---|
| straight bar, no transverse compression | 1,0 |
| standard hook / bend (≥ 90°, cross-cover ⊥ bend plane ≥ 3φ) | 0,7 |
| loop (Schlaufe), Dmin ≥ 15φ | 0,5 |
| welded transverse bar (≥ 0,6φ, within l_b, e.g. mesh cross wire) | 0,7 |
| hook + welded bar | 0,5 |
| two welded bars (spacing < 10 cm, ≥ 5φ, ≥ 5 cm from ends) | 0,5 |

- **Anchorage slip**: for serviceability-critical or large-stress anchorage,
  90° hooks/loops and welded anchors carry limiting slip values (3 mm standard /
  6 mm for lapped welded anchors) — checked where crack control demands it [EC2 8.4.2(4), VERIFY values].
- **Strain-hardening**: if section design used the σ > fyd plateau (σsd ≤ ftd),
  increase l_b by σsd/fyd ≤ 1,05 [EC2 8.4.2].

### 4.4 Direct and indirect bearing (Auflagerung / indirekte Auflagerung)

- Direct end bearing: anchorage behind the bearing edge l_b,dir = max(⅔·l_b, 6φ)
  [digested: 6φ / 6,7φ — [VERIFY] NA limit]; if the bearing pressure itself is
  high, splitting reinforcement or a spreading plate is needed instead.
- Indirect bearing (beam on beam, slab on wall): vertical tie force
  F_Ed = V_Ed·(a/z)/2 + N_Ed (a = load-transfer height, z ≈ 0,9d), hanger bars
  As,req = F_Ed/fyd, stirrups through the load zone s ≤ 150 mm [EC2 6.7, VERIFY];
  ≥ 25% of field bars must continue through an indirect support [recovered rule].
- At interior/continuous supports: bottom bars pass ≥ 6φ (tension) beyond the axis;
  running bars through is the robust choice against accidental +M [practice].

### 4.5 Bending geometry (Biegerollendurchmesser)

Minimum mandrel Ø for cold bending B500 ribbed [NA bend-roll table — numeric cells stripped]:
common shop values **4φ for φ ≤ 16 mm, 6φ for φ > 16 mm** [VERIFY against DIN 488-2
bending schedule (Biegeformblatt)]; welded mesh: do not bend through the weld —
outside bend zone 4φ / inside 8φ reported [garbled, VERIFY]. Side cover at a bend
≥ half mandrel + bar or spalling occurs [practice]. Re-bending (Hin-/Zurückbiegen):
cold only (or ≤ 500 °C warm), predominantly-static members only, σs ≤ 0,8·fyd —
never a site "straighten and reuse" allowance [EC2 8.4.4, VERIFY].

### 4.6 Bundled bars & bars > 32 mm

Bars φ > 32 mm and bundles need special anchorage (increased cmin, spacing by
d_max, reduced fbd) and are not covered by the tables above — treat as engineer-
designed details [bundling tables, stripped — VERIFY]; do not lap-bundle in houses.

---

## Section 5: Lap Splices (Stöße)

```
l_0 = α1 · α6 · l_b         (bond-quality factor folded as α1: gut 1,0 / mäßig 1,4
                             [notation of digested table; EC2 8.5.2 numbers the same
                             effects as α1..α6 — VERIFY mapping])
l_0,min = max(0,3·α1·α6·l_b,rqd ; 15φ ; 200 mm)
```

Compression laps: α6 = 1,0 (and the l_b itself is shorter via §4.2 compression min);
l_0,min compression = max(0,6·l_b·?; 15φ; 200) [EC2 8.5.2(6), VERIFY].

### 5.1 Lapped-ratio factor α6 (unstaggered laps, clear distance ≤ 4φ or ≤ 65 mm)

| % of bars lapped within l_0 | φ < 16 | φ ≥ 16 |
|---|---|---|
| ≤ 33% | 1,2 | 1,4 |
| > 33% (typical 50–100%) | 1,4 | 2,0 |

Reduction to 1,0 / 1,4 permitted when c_1 ≥ 4φ AND clear spacing ≥ 8φ [digested].
[EC2 8.5.2 Table 8.10N analog — VERIFY thresholds.]

### 5.2 Where to splice — decision tree

```
Bottom bars (positive moment: field tension)   → splice over supports, never mid-span
Top bars (negative moment over supports)        → splice in mid-span third, never at support
Column longitudinal                             → splice in upper third of the storey
                                                (low N-ecc side), stagger ≥ 1,0·l_0,
                                                ≤ 50% at one section
Wall verticals                                  → stagger; not at the base-fibre crack zone
Slab top mesh (support band)                    → lap outside the support band where possible
Any bar inside a plastic-hinge / confinement    → no lap (only with EC8-class detailing —
zone                                            out of scope here)
```

Transverse links (stirrups/loops) continue through every lap: spacing ≤ 100 mm or
≤ 5φ over the splice in congestured cases [practice, mirrors EC2 9.5.4 intent — VERIFY].

### 5.3 Mesh laps (DIN 488-2 / EC2 NA)

Single-layer bed mats (Lagermatten) and two-layer Q/R mats: overlap lengths are
type-specific, tabulated per bond zone (Zone 1/2) and concrete class. Digested
example row (Q 524 A, longitudinal direction, Zone 1):

| C20/25 | C25/30 | C30/37 | C35/45 | C40/50 | C45/55 | C50/60 |
|---|---|---|---|---|---|---|
| 50 | 43 | 39 | 34 | 31 | 29 | 27 [cm] |

General minima from the same table family: end/transverse laps ≥ 15 cm (Zone 1) /
≥ 25 cm (Zone 2) [VERIFY]; number of transverse bars lapped per type is also
tabulated (1..8). **Order laps from the DIN 488-2 table for the exact type —
never carry one type's value to another.** A two-layer-mat construction joint
in the field band needs the mats overlapped AND the top band re-established
across it [practice].

### 5.4 Mechanical splices (Kupplungen) — not digested, generic EC2 8.10 rules [T4]

- Couplers require ETA/abZ (Type B1/B2 per EN 1992-1-1 Table 8.10N logic);
  only for designated bar sizes, manufacturer geometry (cone, washer) governs.
- Where used: treat the coupler as a Class-III/II splice — stagger per §5.2, keep
  the clear spacing, and detail congestion around the coupler barrel (a coupler
  is fatter than the bar — cover and bundling checks change).
- Practical triggers: bar φ ≥ 28–32 in columns where l_0 > available length,
  seismic-class frames (EC8), restricted site (retrofit), precast jointing.
- **Never** let a schedule silently mix welded, lapped and coupler types on the
  same bar mark without stating which — each has different fatigue eligibility (§2.4).

---

## Section 6: Minimum Reinforcement (Mindestbewehrung)

Two independent requirements — both must hold:

1. **No uninhibited cracking (Biegezug, EC2 9.2.1.1):** As,min = M_Rk,s / (z·σs),
   z ≈ 0,9d, σs = fyk/γs → in practice:
   ```
   As,min = fct,eff · Wc,eff / (fyk · 0,9d)      [digested worked form]
   m_cr (slab/m, per metre) = fct,eff · h²/6
   ```
   Examples from the digested office building: C30/37 slab h=22 cm, fctm 2,9 →
   m_cr = 23,4 kNm/m → a_s,min = 23,4/(50·0,9·0,17)/10 ≈ 3,06 cm²/m (provided 4,24 ✓);
   beam 25/45 C25/30 → As,min = 1,28 cm². **Young-concrete fct,eff** at early age
   (restrained cases): upper-bound 0,65·fctm at 3 d / 0,75 at 5 d / 0,85 at 7 d for
   fast hardening; thick members take the higher value [early-age fct table cells stripped — VERIFY].
2. **Crack control against restraint (Zwang, EC2 7.3.2):**
   ```
   As,min = kc · fct,eff · Ac,eff / σs,limit
   σs,limit = min(0,75·fyk/γs ; (2/3)·ftk/γs) → ≈ 300–340 N/mm² for B500 [VERIFY per grade]
   kc: bending ≈ 0,4·(1−(h_c,eff/h)²)·? (garbled in source; pure tension 1,0;
       h* = h if h < 1 m else 1,0) [EC2 7.3.2(3) — compute per clause, VERIFY]
   ```
   Ac,eff = effective tension area = b·(h−x)/2 capped at 2,5·(h−x) ... [formula
   stripped in digests — **use the EC2 7.3.2 geometry directly**] [VERIFY].

**Practical ratio check [practice, one recovered digest figure]:** slab main
reinforcement minimum commonly quoted as **0,15% of Ac** [VERIFY against current
NA 9.1.222/9.6]; distribution steel ≥ 20% of field and ≥ 0,10%·A [recovered].
Do not state ρmin = 0,10–0,15% as code — only the 0,15%-type figure is digested,
with flag.

### 6.1 Crack width without direct calculation — bar/space limitation (∅s*, s*)

For the tabular route (no w_k computation), required steel stress σs (quasi-perm)
gives max bar diameter and spacing per w_k class [NA bar-limitation table, partially recovered]:

| σs [N/mm²] | ∅s* for w_k = 0,4 | 0,3 | 0,2 | s_max for w_k = 0,4 | 0,3 | 0,2 |
|---|---|---|---|---|---|---|
| 320 | 14 | 10 | 7 | — | 150–100 | — |
| (160…450 rows exist: ∅s* 54→7, spacing 150→—) | | | | | | |

[VERIFY rows against DIN EN 1992-1-1/NA Bild NA.6 / 7.3.2(6) before use.]
Modification for actual fct,eff: ∅s = ∅s*·(fct,eff/2,9) (apply term ≥ 1) [digested
WU formula 7.7DE]. Alternative full check: w_k = s_r,max·(ε_sm−ε_cm) with
s_r,max = min(φ/(3,6ρ_p,eff); 1,3φ·σs/(3,6fct,eff)) [digested — VERIFY constants].

### 6.2 w_k limits by exposure (GZG)

| Exposure | w_k,max [mm] | Combination |
|---|---|---|
| X0 / XC1 | 0,4 (optical) / 0,2 | quasi-permanent / frequent |
| XC2–XC4 | 0,3 / 0,2 | " |
| XD1–3 / XS1–3 | 0,2 (prestressed: decompression) | frequent [NA w_k table partially recovered — VERIFY] |
| WU ground side | 0,3 | frequent [WU-RL] |
| WU air side (XC1) | 0,4 (thick parts) / 0,2–0,15 per EGS | [WU-RL §9] |

Stress limits when the NA exemits the permanent-form check (elastic analysis,
redistribution ≤ 15%, min steel + detailing OK): σc quasi-perm 0,45fck / rare 0,60fck;
σs rare 0,80fyk (= 388 N/mm² B500); pure-restraint 1,00fyk [worked-example SLS section — VERIFY NA exemption clause].

---

## Section 7: Shear & Torsion Detailing (Scherbewehrung, Torsion)

### 7.1 Concrete without links (for the detailing decision "links or not")

```
V_Rd,c = [C_Rd,c·k·(100·ρl·fck)^{1/3} + k1·σcp] · bw·d   ≥ v_min·bw·d
C_Rd,c = 0,18/γc = 0,12  [EC2 base]   —   German NA commonly 0,15/γc = 0,10
       (the digested worked examples use 0,15/γc; the tables handbook lists 0,18 —
        **edition conflict: VERIFY against current NA/NDI before any proof**)
k = 1 + (200/d)^{0.5} ≤ 2,0 (d in mm) ; ρl = Asl/(bw·d) ≤ 0,02 ; k1 = 0,15 ; σcp ≤ 2 N/mm²
```

Design shear position: at d from the face of a directly supported member, at the
axis for indirectly supported [EC2 6.4.3/NA — at support check V_Ed,dan with lever].
Load placed within 0,5d…2d of the face may use the reduction a_v/(2d)-type rule [worked example].

### 7.2 Links — detailing values

| Item | Rule | Source |
|---|---|---|
| Truss inclination | 21,8° ≤ θ ≤ 65,8° i.e. 1,0 ≤ cotθ ≤ 2,5 | NA [digested] |
| Inner lever z | 0,9d | EC2 |
| Min link ratio ρ_w,min [‰] | fck: 12→0,51 · 16→0,61 · 20→0,70 · 25→0,83 · 30→0,93 · 35→1,02 · 40→1,12 · 45→1,21 · 50→1,31 | [digested rho_w,min table] |
| (Asw/s)min | = ρ_w,min·bw (sinα = 1 vertical links) | EC2 9.2.2 |
| Link wire/bar Ø | ≥ 6 mm; columns: ≥ max(φl/4; 6 mm) | [practice/NA] |
| s_max light shear (VEd ≤ ~0,5 VRd,max) | ≤ 0,75d and ≤ 600 mm (NA: 500?) | [EC2 9.2.1.3; digested example uses min(0,5h; 300) above ratio 0,3 — **VERIFY the 0,3-vs-0,5 threshold and NA caps**] |
| s_max heavy shear | ≤ 0,5d and ≤ 300 mm | [same flag] |
| Bent-up bars (if used) | ≤ 0,5d spacing, ≤ 300 mm, 30–60° | [fragments recovered — VERIFY] |
| Ductility stirrups in beams (As/Ag high, C≥C50/60) | φ ≥ 8 mm; longitudinal spacing ≤ h (≤ 20 cm?); transverse ≤ 60 cm C50/60 / 40 cm ≥C55/67 | [NA beam-ductility table, cells garbled — VERIFY] |
| Two-leg φ8 link areas | As [cm²/m] = 2·0,503·100/s[cm]: @10 → 10,1 · @15 → 6,7 · @20 → 5,0 · @25 → 4,0 | computed, matches digested grid |

Compression-chord flange joints (T-beams): longitudinal shear across the flange
joint with surface classes (sehr glatt/glatt/rau/verzahnt → αc, f pairs 0/0,5;
0,6/0,2; 0,7/0,5; 0,9?/0,7? [cells partial — VERIFY EC2 6.6.4 table]) needs
transverse flange links split half top / half bottom of the flange [worked example].

### 7.3 Torsion (Torsion) — detailing that actually matters

- **Closed stirrups only** (continuous loop, hooks overlapped/welded ≥ the lap of
  the link wire); open U-links do not carry torsion.
- Interaction: (T_Ed/T_Rd,max)² + (V_Ed/V_Rd,max)² ≤ 1; T_Rd,max = 2·A_k·t_k·ν1·fcd·α_cw·cotθ
  (ν1 = 0,525 pure torsion [digested], 0,6·(1−fck/250) shear).
- Links: A_sw/s = T_Ed·tanθ/(2·A_k·f_ywd); **longitudinal corner+side bars**:
  A_sl = T_Ed·u_k/(2·A_k·f_yd) added to bending steel — side bars each face,
  spacing ≤ min(b, h/2, 300)? [VERIFY EC2 9.5.2].
- Shear+torsion stringer width t_k ≤ min(0,5·…) — take 2·A_k/u_k definition; the
  tube idealization: wall thickness t_k from workable geometry, not less than cover+2φ.
- Equilibrium torsion (cantilever slab into beam — the digested canopy example):
  every bit of the torsion goes to steel; no redistribution unless compatibility
  class allows. Redundant torsion: may redistribute — engineer's call.

### 7.4 Punching (Durchstanzen) — detailing headlines (flat slabs)

β (edge effects): interior 1,10 / edge 1,40 / wall end 1,35 / corner 1,50 / wall
corner 1,20 [worked-example-digested]. Links: first row ≤ 0,5d (NA; EC2 0,5d? [VERIFY]),
row spacing ≤ 2d…; two control perimeters; s_t ≤ 1,5d tangential (NA value [VERIFY]);
dowel legs (Steckbügel) or rails (Dübelleisten) per ETA; v_Rd,cs = 0,75·v_Rd,c +
link term with f_ywd,ef = min(250+d; f_ywd) (d mm) [digested]. Slab min thickness
with punching reinforcement ≥ 20 cm [practice-recovered]. Beyond the last row,
v_Ed ≤ v_Rd,c must hold at u_out — extend the column strip reinforcement out to
there [worked example: links needed to 2,74d in worked case].

---

## Section 8: Member Detailing — Practical Tables

### 8.1 Slabs (Platten)

| Item | Rule | Source |
|---|---|---|
| Min thickness | 120 mm general (150 with bent-up/links, 200 with punching links) | [cells stripped — VERIFY 120/150/200] |
| Main bar spacing s ≤ | min(1,5·h? ; 300/400/450?) h>250: 1,5h ≤ 400 two-way / ≤ 450–500 one-way | [garbled — VERIFY 9.6.2.2; safe practice: ≤ 2h at support band, ≤ 3h field, cap 400 [practice]] |
| Support band | ≥ 50% of field steel carried to/over the support; band width l/4 each side | [50% recovered; l/4 EC2 9.6.2.2 VERIFY] |
| Transverse (distribution) steel | ≥ 20% of main, ≥ 0,10%·A | [recovered] |
| Two-way field steel ratio cap | ≤ 25 cm spacing typical; bars per mat §2.3 grid | [practice] |
| Corners (torsion, freely supported) | top+bottom mesh both directions, l ≥ l_y/5? (≈ 0,2·span) into both faces | [stripped — VERIFY 9.6.2.3: EC2 both faces, each direction, length min(0,2·lx?)] |
| Free edges | edge steel ≥ 0,5·? [stripped] → practice: U-stirrups or doubled edge mesh at balcony/slab edges without support | [VERIFY] |
| Openings > ~300 mm | trim: displaced steel area per side, extended l_b past corner + diagonal bars 2φ per corner | [EC2 9.6.3 analog / practice] |
| Cantilever (balcony) | **main steel TOP**, anchored full l_b (top-bar → mäßig bond!) into backspan ≥ 1,5·cantilever [practice], on chairs | §4.1 |

Minimum-steel worked values (crack-control route governs most residential slabs):
12 cm C20/25 XC1 → As,min ≈ kc·1,5·60000? — instead use §2.3 grid: φ8@20 = 2,51,
φ10@20 = 3,93 cm²/m typical floor mesh bottom; support band φ10@15 = 5,24 [practice].

### 8.2 Beams (Unterzüge)

| Item | Rule |
|---|---|
| Bars per layer, 25 cm wide beam, cnom 25 to link, links φ<8 | φ16 → 3–4, φ20 → 3 [digested table: b=20: φ16→4 (bracket = below min spacing), φ20→3; b=30: φ16→7 — **the 7 implies spacing ≈ 20 mm: only legal with bundled/large-aggregate-exempt case; VERIFY + treat as congestion failure in normal work [practice]**] |
| Min horizontal clear gap | max(1,25·dagg; φ; 20 mm)? [EC2 8.2 — VERIFY exact NA set]; vertical layer gap ≥ 20–25 mm & 1,25dagg [EC2 8.2, VERIFY] |
| Layers | 2nd layer sits over the 1st, not over gaps; d reduction per §8.2 static-depth formulas |
| Continuous top/bottom | ≥ 2 bars each face continuous through the beam (structural integrity, NA 9.10 ties: 70 kN ring/anchor [VERIFY]) |
| Curtailment | every stopped bar: continue ≥ max(l_b,dir/0,3-form; ≥ 200 mm) past the theoretical cut-off AND provide ≥ l_b anchor at face; min section moment end-span 0,65·(g+q)·l_n²/8 / interior ÷12 [digested] |
| Fire-ULS continuity (simple case) | extend support mats ≥ 0,15·l_max into field [digested fire rule, VERIFY clause] |
| Side-face skin bars h > 630 mm | **not in digests** — do not quote numbers; if engineer specifies, typical EC2 7.3.3/9.2.1.3 web-reinforcement concepts apply [VERIFY in code] |

Static depth d [digested formulas]: beam 1 layer d = h − c_nom − φ_link − φ/2;
2 layers d = h − c_nom − φ_link − 1,5φ; slab d = h − c_nom − φ/2. (c_nom measured
to link/mesh outer wire.)

### 8.3 Columns (Stützen)

| Item | Rule |
|---|---|
| Min dimension | ≥ 200 mm EC2 [cell stripped — VERIFY]; NA practice ≥ 250? [practice] |
| As,l min | max(0,10…0,15·N_Ed/f_yd; 0,2%·Ac) [two variants digested — VERIFY 9.5.2] |
| As,max | 4%·Ac general; **≤ 4,5% only where no 100%-lap** (worked: As,max(100% lap) = 0,045·Ac) [worked-example-digested, VERIFY] |
| Long. bar spacing | ≤ 200–300 mm on face; bars per face ≤ 5 between links [recovered fragments — VERIFY 9.5.2(5)] |
| Links φ_w | ≥ max(φ_l/4; 6 mm) [digested] |
| Link zone 1 (hinge region, ±max(b; 400) from joint) | s ≤ min(12·φ_l; smallest section dim; 300 mm) [digested worked example] |
| Zone 2 near laps | s ≤ 0,5·zone1 (=120 in worked case) over l_0 when φ_l > 14 [digested] |
| Middle zone | ≤ min(20·φ_l?; b?; 300?) [stripped — VERIFY 9.5.3] |
| Hook of link | 90° only with core cover ≥ 50 mm? else 135°/welded; alternatives φ_w+2 mm / halved spacing / welded mesh cage [fragments — VERIFY NA 9.5.3 Bild NA.8.5] |
| Every corner + alternate bar laterally supported; no bar > 150 mm clear unsupported along link | [EC2 9.5.3(4) — generic clause, VERIFY number 150] |
| Spiral/duplicate (Wegebügel/Spirale) | NA rules not digested — treat as engineer spec [VERIFY] |
| Dowels into footing | ≥ same number/area as column bars; lap per §5; embedment into footing ≥ l_b,comp + bearing checks §4.4 |

### 8.4 Walls (Wände)

| Item | Rule |
|---|---|
| Min thickness cast-in-place | unreinforced: 140 mm (floor-supported, C12/15) / 200 mm (free); ≥C16/20: 120/140; reinforced ≥C16/20: 100/120; precast 80/100 | [NA wall-thickness table recovered] |
| Vertical & horizontal steel | range ~0,1–1,5% [stripped — VERIFY EC2 9.6.1]; two skins if t > 200 mm? and always both faces in WU [EC2 9.6.3, VERIFY] |
| Bar spacing | ≤ min(2·t?; 300; 450?) [stripped] → safe practice ≤ 300 mm both ways [practice] |
| Transverse links | required where one-side As > 2%·Ac: min 4 S-hooks per m² [digested] |
| Basal restraint region | extra top/bottom restraint steel over height ~ h_w/2? at restrained faces [VERIFY 9.6.2/NA] |
| Openings | trim bars = displaced area both sides + 45° diagonals ≥ l_b past corners [practice] |
| Reinforced retaining/basement wall | verticals main at earth face field (crack side), top at base for fixed base; laps bottom-third staggered; single-bar diameter shift (φ12/13, φ14/12 patterns from WU examples §9) |

### 8.5 Footings (Fundamente)

- Reinforcement mesh both directions; min bar φ10 [stripped-digested — VERIFY];
  spacing ≤ 40 cm [recovered fragment, VERIFY]. Strip distribution for rectangular
  footings (DIN-style 7/10/14/19/19/14/10/7 % over b/8 from worked example) [worked example —
  EC2 9.4 NA strip rules VERIFY].
- **Zerrbalken (tie beams between footings)**: min 2φ10? (φ ≥ 10 recovered) + link
  φ6–8; design vertical release load ≥ 5 kN/m where compaction plant runs over
  [digested]; ties also at base-slab edges for robustness.
- Blinding (Sauberkeitsschicht) ≥ 5 cm; bottom cnom ≥ 50 mm [practice].
- Unreinforced footings: only per EC2 4.4 + NA checks (p ≤ fcd·(...), increased
  fctd α = 1,5 for bearing-splitting? [formulas stripped — VERIFY]); max C35/45;
  frost depth (Frostfreiheit, region-specific 50–80 cm) mandatory [practice/DE].
- Pocket/socket foundations (Köcher): embedment ≥ 1,5·? with joint friction μ
  (0,5 rough / 0,3 smooth) [stripped — VERIFY]; precast column standard, not
  cast-in-place practice.

### 8.6 Robustness ties (Aussteifungsverbände, NA 9.10) [VERIFY — only fragments digested]

Ring/edge anchor: **≥ 70 kN** at ≤ 1,2 m from edge, per NA lower limit [recovered];
interior tie nets in two directions per storey (F = max(2Ft; 70 kN)? [stripped]);
edge columns horizontal tie F ≈ 20 kN per façade column [stripped — VERIFY].
Anchorage of ties uses fyd with splices ≤ 150 mm link spacing [fragments]. Detail
as continuous bar/mesh, not as afterthought — the tie is the reason a progressive
collapse chain stops.

---

## Section 9: Weiße Wanne — Water-Tight Concrete Design (WU-RL [T3])

Design of water-retaining basements with the concrete itself as the seal
(structural waterproofing, „WU"). The guideline is edition-sensitive (2017 →
2023 transitions): everything here flagged to the 2017-era digested content —
**re-verify against the current WU-Richtlinie before a real design** [VERIFY].

### 9.1 Class system

| Class | Meaning | Detailing consequence |
|---|---|---|
| **BKL-1** (Beanspruchungsklasse 1) | hydrostatic water pressure (groundwater, flooding) | stricter min thickness / w/z, crack limits, compression-zone check for NKL-A |
| **BKL-2** | no pressure: soil moisture (kf < 10⁻⁴ m/s), accumulating seepage that drains away, condensation; permanent GW ≥ ~2,2 m below slab + free-draining backfill | relaxed table, EGS[c] usual |
| **NKL-A** (Nutzungsklasse A) | no damp spots tolerated (occupied rooms, technical rooms) | crack control tightest; EGS [a] or [b]+injection |
| **NKL-B** | dark spots / single drops OK (garages, storage, under-building levels) | EGS [b]/[c] with self-sealing conditions |
| **EGS [a]** (Gebrauchstauglichkeit) | crack-free by calculation (Rissbreite 0) | prestress-like restraint checks, Sollriss unbewehrt bands |
| **EGS [b]** | limited w_k, sealing by self-healing (Selbstheilung) | self-healing only NKL-B + BKL-1 + non-aggressive groundwater, Δw ≤ 0,1·w_k |
| **EGS [c]** | planned cracks, surface/injected sealed (default) | crack-width-controlled min steel, injectable joints |

Self-sealing calc: w_k,calc ≤ 0,2? (the digested rule: EGS[b] needs w_k ≤ 0,2 mm
plus the conditions) [VERIFY]; w_k limits: EGS[c] **0,3 mm ground side** /
air side XC1 0,4 mm (thick parts) — EGS[b]: WU-RL w_k table: water head ratio
h_w/h_b < 10 AND h_w ≤ 3 m → **w_k 0,20**; h_w > 3 m → **0,15 mm** [digested].
EGS[c] injection trigger: cracks > 0,2 mm (NKL-A) / 0,3 mm (NKL-B) get injected.

### 9.2 Concrete & minimum dimensions (WU-RL min-dim table, 2017-era)

| Case | Slab | Wall cast-in-place | Wall precast | w/z |
|---|---|---|---|---|
| BKL-2 | ≥ 150 | ≥ 200 | ≥ 240 | ≤ 0,60 |
| BKL-1 (0,55 line) | ≥ 250 | ≥ 240 | — | ≤ 0,55 |
| BKL-1 (0,60 line) | ≥ 288 | ≥ 276 | — | ≤ 0,60 |
| Practice with pressure | — | ≥ 300 (clear gap between skins ≥ 180 for 0/32 → 300/34 wall) | | |

- Concrete ≥ C25/30 (WU min); treated at w/z ≤ 0,55 → assume C30/37 strength for
  checks; consistency class ≥ F3 (weich/flowable side, not stiffer) [VERIFY], low-shrinkage, high
  water-penetration-resistance concrete per DIN 1045-2 5.5.3: w/z ≤ 0,60, z_min
  280 kg/m³ (270 with binder credit), ≤ 400 mm section [recovered].
- XD3/XS3/XA2-type mix demands often overshoot the strength by a class — remember
  for w_k checks (higher fct,eff → more steel) [digested note].
- Exposure: soil side XC2+WF (XA2 with aggressive CO2 > 40 mg/l → min C35/45 +
  w/z ≤ 0,50), air side XC1+WO; stairs XC4/XF1+WF [worked example].
- cnom both faces ≥ 35 (50 where waterbar sits at joint — see §9.5).

### 9.3 Reinforcement for restraint (früher/später Zwang)

```
Thin parts (h small):   as,min = kc·k·fct,eff·a_ct/σs       kc = 1,0 centric tension
                        a_ct = h/2 per metre, k = 1,0 WU-slab (axial restraint,
                        unfavourable rule) ; wall k = 0,8 at h ≤ 300, → 0,52 at
                        h ≥ 800, linear between [digested]
Thick parts (NA 7.5.1): as,min = fct,eff·a_c,eff/σs ≥ k·fct,eff·a_ct/fyk
                        h_c,ef/d1 = 2,5 + 2,5/25·(h/d1 − 5) for h/d1 > 5, cap h/2
                        d1 = cnom + φ/2 (face layer) / + φ + φ/2 (inner layer)
Steel stress for a w_k target:
                        σs = √(6·w_k·fct,eff·Es/φ_l) ≤ fyk/γs
```

fct,eff: early (first restraint phase) upper-bound 0,65/0,75/0,85·fctm at 3/5/7 d
(digested; old 0,7·fctm rule obsolete — bridges keep it) [VERIFY]; late phase:
max(fctm; 3,0) → C30/37 late 3,0, early 2,2 (r<0,5 slow half) [worked example].
Digested σs values (N/mm²): w_k 0,3/φ14/fct2,2 → 238 · same fct3,0 → 278 ·
w_k 0,4/φ14/fct3,0 → 321 · w_k 0,3/φ12/fct3,0 → 300 · w_k 0,2/φ14/fct2,2 → 194 ·
w_k 0,15/φ14 → 168 · φ16 → 157 · w_k 0,2/φ16/fct3,0 → 212.
Slow-hardening concrete (r < 0,3): min steel ×0,85 permitted [NA note, VERIFY] —
trade against longer curing/formwork times.

Worked outcome patterns (24–35 cm walls/slabs, C30/37): EGS[c] w_k 0,3: slabs
φ14/9,5 both faces + wall φ12/10,5+φ12/13 asymmetric; EGS[b] w_k 0,15–0,2: up to
+39% steel on slabs (φ14/8,5, φ16/8,5); EGS[a]: full-section through-reinforcement
with unbonded zones / Sollriss bands. **Relative steel ratio ρ ≈ 1,0–1,9% per face
is normal in WU — that is what makes the white tank expensive; the detailing
decision (EGS class) is a cost decision** [practice].

### 9.4 Restraint models (context for the engineer, not for sizing here)

Friction model n_ct = γ_d·(A_c·γ_c+q)·L_eff, γ_d = 1,25·μ, μ = 1,0 sliding layer
(lean+foil), 0,5? rough; ground-body model with E_B (EB 80 moraine ~ 80 MN/m³
[worked example value]); wall joint-factor k (WU-RL restraint-factor table): L/H 1→0,35; 2→0,50;
3→0,60; 4→0,70; 6→0,85 [digested]; in-situ cast section limit h_w/l_w ≈ 1/2…1/3
→ pour segments ~ 15–30 m (EGS[b]: sealed through-reinforced working joints every
~10 m pour length [digested]). Hydration bay (Hydratationsgasse) and squat 2:1
slab panels reduce restraint [practice]. α_T: 10–13·10⁻⁶/K by aggregate
(basalt 7–9, quartz 11–13, dense limestone 6–8, sandstone 11–13) [WU-RL aggregate-aT table] —
ask the ready-mix plant for the real value on high-restraint jobs. Cooling ΔT
timber formwork (WU-RL cooling table): 30 cm wall summer 13/17/20 K, winter 8/12/15
(slow/med/fast) [digested]. Shrinkage practicals: min ~170 kg/m³ water for
workability; **+10 kg/m³ water → +0,1 mm/m shrinkage; ρ = 1,5% steel → −10%
free shrinkage** [digested].

### 9.5 Joints & waterbars (Fugen & Wasserstop) — the leak-prone detailing

| Joint | Detail |
|---|---|
| Arbeitsfuge (construction) | roughen (expose aggregate, remove laitance, pre-wet) per DIN 1045-3; force transfer needs roughness classes §7.2-joint table; **recommendation: seal every slab–wall joint**, waterbar mandatory when the joint is < ~30 cm above design water level (BWS) [digested] |
| Waterbar (Wasserstop) | coated steel (band) waterbar centred in the joint, embedment 30–50 mm each side → needs local cover increase to ≥ 45–50 or setback of the bar; PVC/Kunstsstoff-bands per abP; welded seams; keep the working plane horizontal [VERIFY embedment per product abP] |
| Injectschlauch (injection hose) | overlaps the waterbar ≥ 50 cm; always on the same face through the job (never alternate inside/outside — the injection ports must be reachable) [digested] |
| Sollrissfuge (planned-crack joint) | sealing lamella cuts ≥ 1/3 of section; reinforcement curtailed/staggered at the same line; EGS[a]: unbonded Sollriss L/H ≤ 1,5 (cast-in-place) / ≤ 2,0 (precast); EGS[c]: L/H ≈ 2,0–2,5; seal plate w_k 0,3/0,4 [digested] |
| Bewegungsfuge (expansion) | full separation: expansion band per DIN 18197 + dowels; only where thermal/movement analysis demands (long wings, existing-structure connections) [T3] |
| Multi-seal junction (wall–slab corner with waterbar+hose+edge) | local thickening (e.g. 30 cm wall step) so the seal layers do not collide — plan bar congestion at 3-way joints in 3D [digested practice] |
| Sealing end | every joint seal terminates ≥ 30 cm above BWS (highest design water level) [digested] |
| Element-wall joints against existing build | single-sided formwork; vertical element joints without horizontal through-bars OK only for simply-supported one-way design without diaphragm forces [digested] |

Compression-zone check (BKL-1 + NKL-A, WU 8.5.2): neutral axis x ≥ max(30; 1,5·d_agg)
mm → 48 mm for 0/32, 30 mm for 0/16 aggregate; ξ = −α_sρ + √((α_sρ)²+2α_sρ),
α_s = Es/Ec (5,9 for C30/37) [digested formula — VERIFY]. Punching zones have
higher ρ → larger x, usually governing.

Parking decks above the WU: OS8 rigid systems conflict with EGS[b] + many cracks
→ prefer EGS[a]/[c] under traffic surfaces [digested]; local crack sealing per
DAfStb Schutz-und-Instandhaltung principles [T3]. Crack injection: PUR low-
viscosity resins injected when the crack is at its max opening (≈ winter, ≤ 6 °C
example) [practice].

---

## Section 10: Creep, Shrinkage & Thermal Values (Kriechen, Schwinden)

Relevant to detailing because restraint cracking, long-term deflection and lap
stiffness all key off these. Full function per EC2 Annex B exists; the digested
tabulated end values (Zement 32,5R/42,5N basis):

### 10.1 End creep φ(∞) — C20/25 (C30/37 bracketed), RH50 / RH80

| t0 [d] \ h0 [cm] | 5 | 25 | 60 | | 5 | 25 | 60 |
|---|---|---|---|---|---|---|---|
| 1 | 6,78 (5,54) | 5,57 (4,59) | 4,54 (3,80)? | | 4,43 | 3,77 | 3,51 |
| 7 | 4,73 (3,89) | 3,89 (3,22)? | 3,17 (2,66)? | | 3,10 | 2,63 | 2,45 |
| 28 | 3,64 (2,99) | 2,99 (2,45)? | 2,44 (2,01)? | | 2,38 | 2,02 | 1,89 |
| 90 | 2,91 (2,34)? | 2,34 | 1,95? | | 1,91 | 1,62 | 1,51 |

[Grid partially garbled in extraction (h0 mapping uncertain) — use for order-of-
magnitude only and **read the current table from the code, never from this file**.]
h0 = 2·A_c/u (notional size, cm); t0 = age at load. RH50 dry interiors, RH80 normal
heated buildings (50% worst-case for prestress loss/shrinkage strain).

### 10.2 End drying shrinkage ε_cs,0 [‰] (RH50 | RH80), h0 = 5/15/60 cm

| Cement class × C20/25 … C50/60 | h0 5 | 15 | 60 | h0 5 | 15 | 60 |
|---|---|---|---|---|---|---|
| R (32,5R/42,5N): C20/25 | 0,77 | 0,71 | 0,53 | 0,44 | 0,36 | 0,32 |
| R: C30/37 | 0,72 | 0,67 | 0,52 | 0,42 | 0,35 | 0,31 |
| R: C40/50 | 0,67 | 0,63 | 0,49 | 0,41 | 0,34 | 0,31 |
| R: C50/60 | 0,64 | 0,60 | 0,48 | 0,40 | 0,34 | 0,31 |
| S (32,5S…): C20/25 | 0,57…0,48 across classes | ≈ −25% vs R | | | | |

[Digest gives full R/N/S × 4-class grid; R row shown as representative — VERIFY.]
Rules of thumb that survive any table change [practice/T4]: water content drives
shrinkage (see §9.4: +10 kg water → +0,1 mm/m); dense reinforcement halves
long-term curling restraint; autogenous negligible in normal-strength concrete.

α_T concrete ≈ 10·10⁻⁶/K, steel ≈ 12·10⁻⁶/K — the compatibility of those two
numbers is what makes RC work at all [fundamental]; E-Moduli: Betonstahl 200 000,
Normalbeton 27 000–37 000 MPa [digested constants].

### 10.3 Timing consequences for the schedule

Early-age cracking is a **detailing + curing** problem: high fct,eff at 3–7 d
(§9.3), restraint from struck formwork/soil friction, and summer casting temps
(max fresh 30 °C; >25 °C demands retarding admix) [DIN 1045-3]. A 12 m restrained
wall panel cooling 17 K with α_T 12·10⁻⁶ develops ≈ 2 mm/m shortening → σct up to
3,8 N/mm² unconstrained (E 34 GPa) — more than fct; only reinforcement (and
relaxation, k ≈ 0,43–0,66) keeps it at 0,3 mm cracks [the WU V3 worked example
logic — recompute per project, VERIFY inputs].

---

## Section 11: Bending Positions, Cut-Offs & Congestion (Versatz, Verzug)

### 11.1 The Versatz rule that shifts every tension line

Internal force in the tension chord is not at the bar's geometric position: the
truss lever shifts it by a = (z/2)·(cotθ − cotα) → **anchor every stopped bar
starting from the shifted moment envelope** [digested; z ≈ 0,9d, cotθ 1,2–2,5].
Support transverse (hanger) steel for the load path F_Ed = V_Ed·(a/z)/2 + N_Ed
(§4.4) is the same geometry seen vertically.

### 11.2 Bend / crank / cut-off rules

```
Stop (cut) a tension bar:  continue ≥ max(1,0·l_b? ; ≥ 200 mm) beyond the theoretical
                           cut-off of the shifted envelope [digested worked values:
                           anchor from theoretical cut-off = 0,3·l_b,rqd ≥ 200 mm]
Bend up a bar (cranked, classic): bend no closer than ~0,15·l from the support,
                           every cranked bar keeps ≥ l_b past the bend, contributes
                           to shear (α = 30–60°) — modern practice: vertical links
                           instead, no Aufbiegungen [T4 — legacy technique, keep
                           out of new work unless the engineer details it]
Top bars over interior supports: extend ≥ l/4 each side AND anchor ≥ 6φ past axis
                           (running straight through is the safe default)
Free end of any bar:        hook, loop, or welded anchor — never a naked short end
Stagger laps/bends:         alternate bars offset ≥ 1,0·l_0; never 3 lines of laps
                            at one section on a small column cage
```

### 11.3 Congestion check (Überschneidungen) — do it in 3D, before fabrication

For every joint/zone: count bars per layer × per face, sum diameters + required
gaps (§8.2 spacing), add link corners, add couplers/waterbars/loops/embeds:

- Column + 2 beams: joint needs hoop access from above → **pre-assemble the cage**
  or use crossties/angled bars; a closed hoop cage cannot be slid over lap-spliced
  column bars.
- WU wall noggings/waterbars + both-face mats + corner U-bars: 30/34 walls leave
  ≥ 180 mm clear for 0/32 — verify each double-layer crossing [digested rule].
- Footing: dowels + both mat directions + wall starter bars + waterbar pocket =
  4 bar lines at one depth → shift dowels to mat gaps, not over wires.
- Rule [practice]: if two bars cannot both keep their c_min, one detail is wrong;
  reroute (smaller bars more of, couplers, corbel, or local section increase) —
  the concrete and vibrator neck (≥ 35–40 mm clear for Ø35 poker) must still pass.
- Vibrator clearance through the cage ≥ 4·d_agg? [stripped — use ≥ 3,5–4 cm clear
  channel per bar layer [practice]].

---

## Section 12: Bar Bending Schedule & Quantities (Bewehrungsplan / Stabsatz)

A German rebar drawing/schedule is a **Bewehrungsplan per DIN 488-100-era
convention (BMD)** with bar marks (Stabnummern), the Biegeform (bar shape) drawn
to a shape-code catalog, dimensions to the bar-surface line, cover stated once
per member, and the lap/anchorage notes ON the drawing (not left to the site).
A digested shape-code standard name is not available — **format below is
generic shop convention** [T4, VERIFY against the current DIN 488-100/BMD
detail standard].

### 12.1 Cutting length — model the geometry

```
cutting length = Σ straight segments
               + Σ hook legs (measured to bar end, per Biegeform: e.g. 90° hook
                 leg ≈ max(12φ?; …) — use the shape-code table, not folklore)
               − Σ bend allowances: per 90° bend ≈ 0,5·φ_inner? [the digested
                 deduction set is not machine-readable → compute centreline length
                 from mandrel radius (4φ/6φ, §4.5) + legs; that is always right]
links: L = 2(a+b) + 2·hook leg + bend terms (a,b = core dims = section − 2·cover − φ_link)
```

For FreeCAD export: the model computes centreline + legs automatically (§13) —
this is the single biggest argument for modelling rebar instead of scheduling it
twice by hand.

### 12.2 Quantity rules

- Mass = Σ length × kg/m (§2.2); delivery 6/12 m → add **waste 2–5%** [practice];
  binding wire ≈ 8–10 kg/t [practice].
- Steel per m³ [practice sanity bands, DE framed houses/offices]: footings 60–100,
  slabs 60–110, beams 100–160, columns 120–200, WU walls 90–160, retainers 80–140 kg/m³.
  Outside these bands, re-check before ordering.
- Always put on the schedule: concrete class + exposure + cnom per member;
  steel grade (B500B); bond condition for the lap table used; the **unstamped —
  not for construction** disclaimer until a licensed engineer has signed.

---

## Section 13: Rebar Modelling in FreeCAD (Arch.makeRebar) + IFC Export

Pair with the project's FreeCAD-BIM skill for the model hierarchy; this section
is reinforcement-specific.

### 13.1 Straight/formed bars via Arch.workbench Rebar

```python
import FreeCAD as App, Part
from FreeCAD import Vector
import Arch

doc = App.getDocument("house")
# host must be a structural object (Arch Structure / Part structural role)
col = Arch.makeStructure(Name="K1", Length=3000, Width=300, Height=300)
col.Role = "Column"

r = Arch.makeRebar(col)          # makeRebar(host) -> Rebar object
r.Diameter = 16
r.Offset   = 35                  # cnom to THIS bar's surface — set per face where
                                 # the object supports it; do not trust defaults
r.Role     = "Vertical"
# --- THE GOTCHA: Direction defaults to Vector(0,0,0) — a zero direction makes
#     the rebar silently degenerate or extend the host bbox. ALWAYS set it:
r.Direction = Vector(0, 0, 1)
r.SegmentLength = Vector(0, 0, 2500)     # or use a Sketch/Path for bent bars
r.Number   = 6
r.Spread   = 100                          # spacing, OR set Distribution
# bounding-box gotcha: the straight-rebar algorithm clips to the host bbox with
# a tolerance — the default tolerance can be smaller than the bar diameter, so
# end bars vanish / corners cut. Widen:
r.Fuzz = r.Diameter / 2.0    # property name varies by version (Fuzz/Tolerance/
                             # RebarShape tolerance) — check doc on YOUR install [VERIFY]
```

Bent shapes: use Sketch (bar centreline at the **inner face** = section − cover;
then the bend allowance is applied by the Reinforcement module's RebarShape,
DIN 488-1 catalogue shapes) or Path (polyline) objects; the Stirrup/Collar type
takes the host section, cover, hook angle (set 135°, legs per §12.1). Top-bar
chairs: model as separate Rebar type "Chairs" or as simple Part cylinders with
the rebar material role — do not let the schedule silently include them.

### 13.2 Checks the model should run (script them; FreeCAD won't)

```
[ ] for each bar: l_modelled ≥ l_b from §4.2/§4.3 (host bbox is not an anchorage check!)
[ ] laps: same-mark overlap ≥ l_0 (§5); ≤ 50% lapped at any section
[ ] cover: rebar Part distance to host face ≥ cnom (use Part distToShape per bar)
[ ] congestion: boolean-common every crossing pair; report collisions incl. links,
    couplers, waterbars (model waterbars as a Part box 1 mm thick — it will clash-check)
[ ] bars-per-layer count vs §8.2 table (parse marks by layer z)
```

Rebar objects are geometry only. State that with every model handover.

### 13.3 IFC export with cover & marking (neka-nat/freecad-mcp / IfcForge route)

- Export the rebar via IFC4 `IfcReinforcingBar` with `BarProfile`,
  `NominalDiameter`, `CrossSectionArea`, `BarLength`, and role
  (`main`/`stirrup`/`distribution`). The FreeCAD IFC exporter maps Rebar →
  IfcReinforcingBar when the Reinforcement workbench objects are used; plain
  Part sweeps are exported as `IfcCovering`/`IfcPlumbingFixture` junk unless you
  assign the right role — check the output in a viewer [VERIFY per FreeCAD
  version].
- **Cover**: carry it as `IfcReinforcementDefinitionProperties` on the host
  `IfcBeam/IfcColumn/IfcSlab` (the IfcReadModel/IfcWriter path used by
  neka-nat/freecad-mcp exposes an `IfcReinforcementDetailProperties`-style
  block; if your build does not, post-process with ifcpatch:
  `IfcRelDefinesByProperties` + a new `IfcReinforcementDefinitionProperties`
  with `CoverRight/Bottom/Left/Top` per surface list) [VERIFY exact attribute
  names against current ifcopenshell schema].
- **Marking**: set `Name`/`Tag` of every IfcReinforcingBar to the bar mark
  (Stabnummer) and `Reference` to the drawing part/sheet — that is what lets the
  BMD shop import and the quantity survey link back. `ObjectType` = shape-code
  (e.g. "01", "0411-5-6" per the BMD shape catalog) so the bending machine reads it.
- Round-trip test one member before mass-exporting: IfcOpenShell `ifc5d`/`validate`
  or a Blender BIM import — a 90% correct rebar IFC that the shop cannot open is 0% correct.

---

## Section 14: Common Detailing Errors That Cause Real Damage

Ordered roughly by frequency-on-site × consequence.

### 14.1 Cantilever main steel in the bottom face
Balcony/stair-flight/chajja-equivalent: the fixer treats the cantilever like a
simply-supported slab. Main steel MUST sit in the **top** face on chairs, fully
anchored into the backspan with the **moderate-bond** net length (§4.2 mäßig —
top bars under >30 cm of fresh concrete are the weaker bond case, the digest's
top-vs-bottom distinction). Failure at the root on striking is sudden and fatal.

### 14.2 Blanket "40d" or "30 cm lap" for every bar
One number for all diameters/classes/positions: §4.2 shows the correct net length
varies from 28 cm (φ6 C20/25 good) to 131 cm (φ28 C20/25 mäßig) — a factor of 4,7.
A blanket lap is simultaneously wasteful and unsafe. Put the actual table on the
drawing per bar mark, with good/moderate bond separated.

### 14.3 All laps at one section / at the moment maximum
Column cages with three bar lines meeting at floor level, beam top bars lapped
over the support. §5.2: stagger ≥ 1,0·l_0, ≤ 50% per section; the splice is the
weakest point of the bar and must sit where the force is small.

### 14.4 Missing α6 / bond-condition penalty on congested laps
Two-layer mats lapped end-to-end with c < 4φ and no stagger run α6 = 1,4–2,0 —
site crews measure the Zone-1 table value and are 40–100% short. Recompute l_0
for the worst actual configuration, not the ideal one.

### 14.5 Cover "on average" / spacers missing on the top face
Bars tied to the soffit formwork, cover blocks only under the bottom mat: side
and top cover vanish; the pour-water side of a slab is then 5–10 mm cover to a
wire that was specified at 35. Count spacers/m² per §3.4 and check all four faces
before the pour; a bend with side cover < mandrel radius spalls (§4.5).

### 14.6 Link spacing right in the middle, wrong at the ends
Shear is maximum at the supports; the schedule says φ8/15, the fixer runs
φ8/25 everywhere because it is faster. The digested beam example steps φ8/15 →
φ8/22,5 → mid-zone by calculation — the zone boundaries must be **dimensioned on
the drawing** (from the face), not estimated.

### 14.7 Open stirrups / hooks not engaging a longitudinal
Single-leg or U-links with 90° hooks that do not close around a bar unwind under
load or handling. Torsion and column links: closed loop, 135° hooks or welded
(§7.3, §8.3) with alternating hook position along the member.

### 14.8 Anchorage "into thin air" at indirect supports
Beam ends on wall/nogging without hanger links through the bearing, top bars not
extended into the support past the axis. §4.4 hanger force + ≥ 6φ past-axis rule;
check the split-crack (Spaltrisse) case where the bearing is narrow.

### 14.9 WU: sealing details that cannot be built
Injection hose alternating faces; waterbar at nominal 35 mm cover with 40 mm
embedment requirements; Sollriss lamella not cutting the section; joint seals
ending below BWS; congested 3-way corner where waterbar+mat+nogging occupy one
layer. Every §9.5 line is a leak that was pre-programmed at the drawing board.

### 14.10 Mesh orientation wrong (A vs B)
Q/R mats ordered one way, laid the other; the "10 cm-wire" direction ends up as
distribution where the design wanted main steel. Mark the laying direction with
an arrow per mat on the plan and mirror it on the delivery list; A/B suffix and
bond-zone suffix carry the lap length too (§2.1, §5.3).

### 14.11 Cutting cast-in steel for later openings
Chasing/core-drilling through placed bars without the engineer's statics for
the trim — §8.1 trimmer bars must be cast in, and any post-cut needs a written
insetting (Nachtrag) by the Tragwerksplaner, not a foreman's decision.

### 14.12 Congestion discovered at the 3rd attempt to close the formwork
Result: bars moved out of position, cover gone, cold-joint concrete left in the
joint. The §11.3 3D check costs one hour in the model; on site it costs the pour.

### 14.13 Mixing code generations in one project
EC2 cover with DIN 1045-1 laps, WU-RL 2017 crack targets with 2023 joint rules,
C25/30 assumed for an exposure that now requires XC3 → C30/37 in the current NA.
One edition set per project; the BBQ/DIN 1045-1000 classes (2023/24) redefine
who-checks-what, not the physics — but they change the QA documentation you owe.

### 14.14 Water added at the pump
w/z is the durability variable (§3.4, §9.2). A slump rescue silently destroys the
WU-concrete guarantee (w/z ≤ 0,55/0,60) before the first crack exists. Reject or
re-dose with superplasticizer by the plant, never on site.

### 14.15 No curing / too early striking
Plastic-shrinkage cracks at 4 mm/m scale (§10.2 context) become the water paths
of a basement that was designed water-tight. Curing duration per class/temperature
(EN 13670/DIN 1045-3 tables), and cantilevers/props on the engineer's date, not
the schedule's pressure.

---

## Section 15: Verification Checklists

### 15.1 Drawing / schedule issue check (before sending to the Biegelei)

```
[ ] Every member: concrete class + exposure class + cnom shown; §3.2 table matches
[ ] Every bar mark: φ, grade B500A/B, shape-code, qty, length, weight consistent
    between plan, schedule and model export
[ ] Lap lengths on the drawing = f(class, φ, bond condition, α6, stagger) per §5,
    NOT one blanket value; mat types A/B + bond-zone correct (§2.1)
[ ] Anchorage at every support: l_b per §4.2 ≥ l_b,min; αa credits only shown
    hooks/welded bars (§4.3)
[ ] Top vs bottom bars distinguished where bond condition differs (§4.1)
[ ] Link zones dimensioned from the face; s_max per §7.2; closed links where §7.3/§8.3
[ ] Curtailment ≥ anchor-past-cut-off per §11.2; Versatz applied to envelopes
[ ] Columns: link zones 1/2/3 per §8.3; no lap in zone-1 without halved spacing
[ ] Congestion 3D check done incl. couplers/waterbars/embeds (§11.3) + vibrator path
[ ] WU: EGS class stated; joint detail per §9.5 at every crossing; injection hose
    same-face rule; seals end ≥30 cm above BWS
[ ] Disclaimer present: geometry/estimation only — no design liability taken
[ ] Someone with Tragwerksplanung Haftung has reviewed and will sign
```

### 15.2 Pre-pour (Bewehrungsabnahme) — highest-leverage 30 minutes

```
GEOMETRY: dimensions/levels vs drawing; formwork tight & oiled; chairs present
IDENTITY: bar φ vernier-checked (coil bar runs thin/fat per supplier), mill cert
  (Abnahmeprüfbescheinigung 2.2) present for the batch; mesh type vs waybill
POSITION: cover blocks all faces incl. sides & top-band; cantilever main steel TOP
  (14.1 check) ← CRITICAL; slab top band on chairs not walked flat
DETAILING: measured lap lengths vs table (top/bottom separated); lap positions vs
  §5.2 tree; ≤50% lapped; link spacing measured in the end zones; hooks closed &
  engaged; dowels in right spot & height; waterbar centred, vertical, seams welded,
  hose in place; Sollriss lamella position; trim bars at all openings; embeds/sleeves
  tied, surveyed; post-tension/loop bars where §4.3 α-credits were taken (no
  phantom α = 0,5!)
CONCRETE: class & w/z on docket = drawing class; consistency F/S class agreed; LP
  where XF/WU; cube/witness samples arranged; curing kit on site BEFORE starting
SIGN-OFF: the responsible Bauleiter/Prüingenieur representative has physically
  approved; without that signature the pour does not start
```

---

## Section 16: What Must Be Re-Read Before Citing Numerically

The digests carry OCR losses. Re-verify in the primary standards (current
editions) before any value leaves the office:

| Item | Where to verify |
|---|---|
| C_Rd,c = 0,15/γc vs 0,18/γc (edition conflict seen in sources) | DIN EN 1992-1-1/NA + NAdI, 6.2.2 |
| fbd table reconciliation with 2,25·η0η1·fctk,005/γc (§4.1) | EC2 8.4.2/NA Bild NA.8.2 |
| l_b,min & direct-bearing 6φ/6,7φ cells (§4.2/4.4) | NA 8.4 |
| Bond-condition 30/15 cm wording (§4.1) | EC2 8.4.2(1)/NA |
| α6 thresholds, c1 ≥ 4φ / 8φ reductions (§5.1) | EC2 8.5.2 / NA Bild NA.8.4 |
| All DIN 488-2 mesh types, bond zones, lap tables incl. §5.3 Q524A row (§5.3) | DIN 488-2 (ordering document!) |
| Biegerollendurchmesser 4φ/6φ + re-bending (§4.5) | DIN 488-1/-100 + EC2 8.4.4 |
| ρmin 0,15%-type slab figure (§6) | NA 9.6 / EC2 9.2.1.1 |
| σs,limit min(0,75fyk/γs; 2/3ftk/γs) & ∅s*/s* table rows (§6) | EC2 7.3.2 / NA Bild NA.6 |
| s_max 0,3-vs-0,5 threshold + NA caps (§7.2) | EC2 9.2.1.3 + NA |
| Column zones 1/2/3 values, link detail options (§8.3) | NA 9.5.3 Bild NA.8.5 |
| Wall thickness/reinforcement-ratio minima (§8.4) | EC2 9.6.1 + NA |
| Footing strip widths 7/10/14/19% (§8.5) | NA 9.4.2 (or DIN-style distribution rules) |
| Robustness 70/20 kN tie values & layout (§8.6) | NA 9.10 |
| EVERY WU number: BKL thresholds, NA table 9.6 dimensions, EGS table, σs formula
  constants, joint rules, compression-zone 1,5·d_agg (§9) | DAfStb WU-Richtlinie
  (current edition — 2017 vs 2023 differences), DBV Merkblätter |
| Creep/shrinkage grid h0 mapping (§10) | EC2 Annex B / NA table as printed |
| Fire a_min & 0,15·l_max rule (§8.2) | DIN EN 1992-1-2 tabular |
| FreeCAD Rebar property names (Fuzz/tolerance) & IfcReinforcementDefinitionProperties
  attribute spelling (§13) | your installed FreeCAD + ifcopenshell versions |
| Aggressivity of the actual groundwater/soil | DIN 4030 analysis on the project, never a table |
| Exposure-class assignment of every member | project durability concept — engineer's decision |

### Standards behind this skill (no commentary — editions per §16)

- DIN EN 1992-1-1 + Nationaler Anhang (EC2), DIN EN 1992-1-2 (fire)
- DIN EN 206 / DIN 1045-2; DIN EN 13670 / DIN 1045-3; DIN 1045-1000 (BBQ)
- DIN 488-1/-2/-3/-5/-100 (Betonstahl, Matten, Draht, Gitterträger, Bewehrungsplanung)
- DAfStb WU-Richtlinie (waterproofing concrete), DBV Merkblätter (joint sealing)
- DIN 18197 (expansion joints) context; DIN 4030 (groundwater aggressivity)

### Companion skills

| Need | Skill |
|---|---|
| Member sizing, system choice, spans | `structural-systems` |
| Foundations/geotech | `geotechnics-foundations` |
| BIM hierarchy & model structure | `construction-freecad-bim` |
| Openings, lintels, wall connections | `openings-windows-doors` |
| Waterproofing build-ups beyond WU (bitumen, membranes) | `roofing-waterproofing` |
| Tolerances/execution QA in concrete | `construction-scheduling-site` |

---

**Closing reminder:** this is a detailing aid. Reinforcement design carries
Haftung — a Tragwerksplaner and a specialist Bewehrungsplaner sign, and their
numbers, not the ones here, build the structure.
