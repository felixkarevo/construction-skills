---
name: masonry-construction
description: >
  Load-bearing and enclosing masonry design and detailing per DIN EN 1996-1-1/-2/-3
  (Eurocode 6) with the German National Annex: masonry unit groups (Hochlochziegel
  HLz, Vollziegel, Kalksandstein KS, Porenbeton PB, Leicht-/Normalbeton LB/NB) with
  gross sizes, density classes (RDK) and the fmk characteristic-compression-strength
  grids per unit group x mortar group; mortar groups (Normalmörtel M2.5-M20,
  Dünnbettmörtel DM, Leichtmörtel LM21/36); ULS design by the simplified method
  (centered and eccentric compression, reduction factor cA/Phi, effective height
  hef = rho*h, restraint classes, slenderness hef/tef <= 21, 3-storey applicability
  limits) and general rules; shear walls (bond shear fv = fvk0 + 0.4*sigma_d with
  friction + stock contribution, unpointed-joint reduction); partial/local bearing
  (loaded-area spreading, confinement factor beta); bracing systems (cross walls,
  diaphragms, ring anchor, plumbness imperfection); wall typologies (single-leaf
  monolithic, two-leaf with cavity/Vormauerschale/Verblendschale, Kernschaal
  <=15 cm, WDVS/ETICS, double wall, cellar wall prescriptive EN 1996-3); detailing
  rules (bond and lap, joint thickness, ring beam position <=0.5 m from axis,
  flat-lintel arch model, wall-tie density, movement-joint spacing 6-12 m per
  unit type, plinth 30-50 cm above ground, cavity keep-clean rule); seismic
  confinement routed to seismic-design; masonry physical-property tables
  (lambda, RDK density classes, vapour mu, sound mass kg/m2, EI/REI fire
  thicknesses); execution, labour and quantity figures; typical damage
  catalogue; FreeCAD/IFC modelling notes; verification checklist.
---

# Masonry Construction (Mauerwerksbau) — EN 1996 + German NA

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

This skill turns "an masonry wall" into an actual design aid: which unit group,
which mortar group, what characteristic masonry strength fmk follows from the
pair, what the wall may be asked to carry under the simplified method, how shear
resistance and bracing are built up, which wall typology and which detailing
rules apply, and what has to be true on site before the next trade covers it.
It covers DACH/Eurocode practice: metric unit formats, DIN EN 1996 with the
German National Annex (NA), EN 771 product families, EN 998 mortars, DIN 4172
dimensional coordination.

Masonry carries the gravity load, the wind, the earth pressure and — if the
building is braced by it — the seismic force, through the same wall that must
simultaneously keep out rain, carry plaster, insulate and satisfy fire and sound
requirements. Every decision here is therefore a materials decision, a structural
decision and a physics decision at once. This file keeps the numeric grids
together so that a specification, a calculation note or a FreeCAD model uses real
fmk values, real effective-height rules and real detailing limits instead of
plausible-sounding numbers invented on the spot.

Every numeric value is tagged with its source digest as **[VERIFY]** where it was
OCR-degraded in the underlying tabular handbook and must be read from the primary
standard before being quoted in a submission. Values that are trade practice
rather than a code clause are labelled **[practice]**. Values computed from the
digest data are labelled **[derived]**.

---

## Reality Check — Liability and Approval

**This skill produces design aids and calculation guidance for planning and
FreeCAD/BIM modelling ONLY.**

- Nothing in this file is a structural design. Load-bearing masonry, shear-wall
  design, cellar-wall design and any masonry carrying a slab or roof are design
  decisions reserved to a qualified engineer (Tragwerksplaner; in Germany
  statically relevant masonry in the regular procedure is checked by a
  Prüfingenieur, and masonry outside the simplified/native rules generally needs
  an approved type or expert review, allgemeine bauartgenehmigung / Zustimmung im
  Einzelfall).
- **The design MUST pass the local building authority (Baugenehmigung) before
  construction**, with the Bundesland building code (MBO/LBO) and the linked
  technical building rules (TVV, Bauregellisten) applying locally.
- Never present a FreeCAD wall object, an fmk value or a calculation aid in this
  file as construction-ready. A wall modelled at 240 mm is geometry, not a
  verification.
- If the user starts treating output as final — orders material, says the
  Maurerkolonne starts Monday, asks whether a wall "can take" the slab — stop and
  state plainly that a licensed engineer must run and stamp the analysis and that
  authority approval is required.
- Never fabricate a test certificate, CE/DoP declaration, factory-production-control
  document, mortar-group classification or approval reference.
- Masonry in seismic regions (Germany seismic zones 0-3 per DIN EN 1998-1/NA,
  ÖNORM B 1996-1-1 Annex, Swiss SIA 261/5) is out of scope for a design aid —
  see §11 and route to the `seismic-design` skill.

---

## Section 0: Scope, and Which Sibling Skill Owns What

| Question | Owned by |
|---|---|
| Seismic zone, ductility class, confinement elements, wall-density and diaphragm rules for EC8 | `seismic-design` |
| Concrete grade, reinforcement, ring beam / Ringanker bar schedules, padstones, precast lintel design | `concrete-detailing` |
| Rising damp, waterproofing build-ups (Frisch-, Schwarz-, Weißesperrschicht), Kellerabdichtung systems | `waterproofing` |
| U-values, hygrothermal verification (GLASER / WUFI), DIN 4109 acoustic design in detail | `building-physics-thermal-moisture` |
| Quantities, unit counts and rates for a cost plan (DIN 276 KG 300) | `cost-management-din276` |
| Site logistics, wall-build sequences, curing durations in a programme | `construction-scheduling-site` |
| Bearing capacity, sulphate attack on foundation masonry, Kellerwannen variants | `geotechnics` |

**This skill owns:** the masonry *unit* and its classification, the *mortar
groups*, the *fmk grids*, the *EC6/NA design rules* (compression, shear, local
bearing, effective height, slenderness), the *wall typologies* (single-leaf,
two-leaf, cavity rules, WDVS), the *masonry-side detailing* (bond, joints, ring
beam, lintels, ties, movement joints, plinth), the *masonry physical properties*,
*execution tolerances and labour figures*, the *defect catalogue*. Where a numeric
conflict appears with a sibling, the owner wins and this file is corrected.

---

## Section 1: Which Standard Governs What

| Topic | Standard | Used here for |
|---|---|---|
| Masonry design (design of unreinforced, reinforced, confined masonry) | **DIN EN 1996-1-1** + **National Annex DIN EN 1996-1-1/NA** | fmk via k/alpha/beta grids, gammaM, effective-height and reduction-factor rules, shear, local compression, slenderness limits |
| Masonry — seismic design | DIN EN 1996-1-1/NA §3.2 + DIN EN 1998 | routed to `seismic-design` (§11) |
| Masonry — simplified calculation method | **DIN EN 1996-3** + NA | cellar walls without calculation, low-rise wall design, applicability tables |
| Masonry — fire design | **DIN EN 1996-1-2** | EI/REI thickness tables (§12.4) |
| Masonry units (product) | **EN 771-1** (clay, + DIN 105-100 / DIN EN 105 forms), **EN 771-2** (lime-sandstone KS, + DIN V 106), **EN 771-3** (aggregate concrete LB/NB, + DIN EN 771-3 + DIN V 18151-153), **EN 771-4** (AAC PB, + DIN EN 771-4 + DIN V 20000-404), DIN 20000-401..404 application standards | unit groups, declaration of compressive strength fb, density class RDK, gross dimensions |
| Masonry mortars | **EN 998-2** + DIN V 18580 / DIN EN 19918 series (Werkmörtel), DIN EN 998-1 (render mortar) | mortar groups M/DM/LM, declared fm, downgrade rule when CE marking lacks extra properties |
| Dimensional coordination | **DIN 4172** (building grid, BM 12.5 cm), DIN 323 series R5/R10/R20 small sizes | Richtmass/Nennmass, wall nominal thicknesses |
| Vapour/physical properties | DIN 4108-4 (design-value catalogue), EN ISO 1046/EN 1745 | lambda, mu, cp values used in §12 |
| Sound insulation | **DIN 4109-33** (design values catalogue, mass-law curves, two-leaf formulas) | Rw estimates, partition masses (§12.3) |
| Fire (national classification route) | DIN 4102-4 (Baustoffklasse tabulated wall data); EC6 route per DIN EN 1996-1-2/NA | wall thickness for EI/REI (§12.4) |
| Render/plaster | **EN 998-1**, DIN 18550 groups, DIN EN 13914 (application), DIN 18550-2 quality levels Q1-Q4 | plaster spec (§10.9) |
| Works contract / execution | **VOB/C ATV DIN 18330** (Mauerarbeiten), DIN 18202 (tolerances Table 3), DIN 18203 (execution of masonry — not digested, see §13.4) | execution rules, tolerances |
| Actions | DIN EN 1990/1991-1-1/-1-3/-1-4 + NA | gammaG 1.35 / gammaQ 1.5, partition surcharge, wind, snow (§5.1) |

**Honesty note on the digest basis:** the numeric grids below were taken from a
tabular-handbook extraction whose text layer lost some superscripts and cell
pairings. Every table that is partially degraded carries a **[VERIFY]** flag;
read the actual NA table before putting the number in a statics submission.
DIN 18202/18203 tolerance tables were NOT present in the digests (§13.4).

---

## Section 2: Masonry Units — Groups, Formats, Properties

### 2.1 Product families and German unit designations

| Group | Abbrev. | Product standard | Typical German names | Note |
|---|---|---|---|---|
| Clay masonry (Mauerziegel) | Z | EN 771-1 + DIN 105-100 | Vollziegel VZ, Hochlochziegel **HLz**, Verbundziegel VMz, Voll-HLz VMz/VHLz, Kermauerziegel KMz, Planziegel **HLzW/HLzP** (grinded, thin-joint), hinterlüftete Vorsatzschalensteine | strength class fb 4-100 on gross area; groups A/B/E/T1/T2-T4/LL by Lochanteil and use |
| Lime-sandstone (Kalksandstein) | KS | EN 771-2 + DIN V 106 | KS-Vollstein, KS-Hochloch, **KS XL** (thin-joint large block), KS-Planstone | dense (1.8-2.2), good sound mass; thin-joint DM only |
| autoclaved aerated concrete (Porenbeton) | PB | EN 771-4 + DIN V 20000-404 | Plansteine PP, Planblöcke, Porenbeton-Sturz elements (PP + U-Schalen) | low density 0.35-0.8 RDK; thin-joint DM 1-3 mm |
| Light-weight aggregate concrete (Leichtbeton) | LB | EN 771-3 + DIN V 18151-153 | Hohlblocksteine **Hbl** (1K-6K chamber classes), Vollblocksteine Vbl, Plan-LSB | chambered granulate/brick-porite; also LM mortar variants |
| Normal-weight concrete (Beton) | NB | EN 771-3 | Hochblock-/Betonstein, block formats | dense, foundations and aggressive exposure |
| Natural stone (Naturstein) | — | EN 771-6 + NA Annex L | Bruchsteine, Werksteine, Schichten | design per NA.L; movement joints up to 12 m |

Lochanteil (gross-area void ratio) classes that drive unit grouping: **Vollstein**
< 12.5 %; **Hochloch** ~15-50 % of bed face (vertical perforation,
"mit Kammern"); large-format elements <= 1 m length. The void pattern decides
fb declaration basis, shear contribution (§7) and slotting limits (§10.8). **[VERIFY — class boundaries per current EN 771-1]**

### 2.2 Formats and dimensional coordination (DIN 4172)

- Grid basic module **BM = 12.5 cm**; work sizes (Arbeitsmaße) of masonry =
  stone + joint. Richtmaß example from the digest: nominal wall **25 cm grid →
  stone 24 cm + 1 cm joint (Nennmaß 24)**; room width 400 cm → 401 cm
  dimension line with plaster. Concrete keeps 25 → 25. **[VERIFY]**
- Theoretical stone sizes from BM 25 - 1 cm joint: length 24 cm, width 11.5 cm
  (= 25/2 - 1), height NF = 25/3 x 2 - joint ≈ 11.3 cm (normal format).
  Thin formats 2DF/DF give storey heights as multiples of the layer (Schicht)
  height: common stone heights 52 / 71 / 113 / 155 / 175 / 238 mm feed the
  planning grid (Tafel 10.3: Kopfzahl n -> length 0.615/1.240/1.990 m ... for
  n = 5/10/16 units at 12.5 cm module, joint 1 cm). **[VERIFY exact grid]**
- Wall nominal thicknesses in use: **11.5, 15, 17.5, 24, 30, 36.5, 42.5, 49 cm**
  (single-leaf); two-leaf totals add cavity 4-15 cm + outer leaf 9-11.5 cm.
- Small-format KS (thin-joint system units, from the labour digest):
  4DF (248x115x238) for t = 11.5 cm; 5DF for t = 15 cm; 4DF (248x240x113)
  for t = 24 cm; 5DF for t = 30 cm. Unit counts: 16 St/m² (t 11.5), 16 St/m²
  (t 15), 31 St/m² (t 24), 32.5 St/m² (t 30); mortar demand 7-9 l/m². **[VERIFY pairings]**

### 2.3 Density classes (Rohdichteklassen, RDK) and unit weight

Artificial-stone masonry incl. joints, built dry **[from DIN EN 1991-1-1/NA + DIN 1055 digest]**:

| RDK of unit | gamma kN/m³ | RDK | gamma kN/m³ | RDK | gamma kN/m³ |
|---|---|---|---|---|---|
| 0.31-0.35 | 5.5 | 0.81-0.90 | 11.0 | 1.41-1.6 | 16.0 |
| 0.36-0.40 | 6.0 | 0.91-1.00 | 12.0 | 1.61-1.8 | 18.0 |
| 0.41-0.45 | 6.5 | 1.01-1.20 | 14.0 | 1.81-2.0 | 20.0 |
| 0.46-0.50 | 7.0 | 1.21-1.40 | 16.0 | 2.01-2.2 | 22.0 |
| 0.51-0.55 | 7.5 | — | — | 2.21-2.4 | 24.0 |
| 0.56-0.60 | 8.0 | — | — | 2.41-2.6 | 26.0 |
| 0.61-0.65 | 8.5 | 0.66-0.70 | 9.0 | 0.71-0.75 | 9.5 |
| 0.76-0.80 | 10.0 | — | — | — | — |

Corrections: RDK <= 1.4 with **light-weight or thin-joint mortar: -1 kN/m³**.
Mortar unit weights for self-weight: Zementmörtel 19-23, Kalkzementmörtel 18-20,
Kalkmörtel 12-18, Gipsmörtel 12-18 kN/m³. Plaster surface loads per DIN 1055:
Kalk/Zement 20 mm ≈ 0.36-0.42 kN/m² per face; Gips 15 mm ≈ 0.18 kN/m²;
WDVS (armoured render 15 mm) ≈ 0.30 kN/m². **[VERIFY grid cells partially merged in digest]**

Built-wall density formulas from the physics digest **[derived]**:

| Mortar type | rho_wall formula | Applies |
|---|---|---|
| Normal mortar | rho = 900*RDK + 100 kg/m³ | RDK 0.35-2.2 |
| Light-weight mortar | rho = 900*RDK + 50 | RDK <= 1.0 |
| Thin-joint | rho = 1000*RDK - 100 (RDK > 1.0); 1000*RDK - 50 or -25 (<= 1.0) | plan units |
| Sand-filled turned hollow blocks | rho = 1000*(RDK + 0.4) | Kerndämmung variant |

### 2.4 Unit-selection decision tree

```
Is the wall load-bearing (slab/roof/storey above) or bracing?
|
+-- YES, up to 2-3 storeys, single-leaf, no insulation dilemma wanted
|     -> HLz (Hochlochziegel) 24-36.5 cm with LM21/LM36 light mortar,
|        or PB (Porenbeton) 24-36.5 cm Planstein with DM thin-joint,
|        or KS 12 DF thin-joint where sound mass governs (dense inner leaf).
|        fb class from fmk tables §3 — never choose fb < 4 for bracing walls.
|
+-- YES, high sound mass / exposed / basement / aggressive
|     -> KS normal or LB/NB solid 11.5-24 cm (dense, high mass),
|        or Vollziegel where the tradition/details demand it.
|        Cellar exterior: KS-HL or LB Hbl >= 20 cm + EN 1996-3 rules (§9.5).
|
+-- YES + real U-value wanted without extra system
|     -> two-leaf: inner leaf KS/PB/HLz + cavity 40-60 mm ventilated
|        or Kernschaal filled (cavity <= 15 cm) — see §9.2;
|        or single-leaf + WDVS — see §9.3.
|
+-- YES + seismic demand present (zone >= 1, EC8)
|     -> STOP: confinement, ring beam and wall-density design go to
|        `seismic-design` FIRST; this skill then supplies material and
|        EC6 gravity/wind checks only.
|
+-- NO (partition, infill, non-loadbearing veneer)
      -> t >= 6.6 cm PB / KS / HLz small units per DIN 4103 stability
         (§10.7), non-loadbearing single-leaf infill areas per §9.1
         table, or Verblendschale on its own support ledge (§9.4).
```

### 2.5 Acceptance at delivery (product level)

- CE marking + DoP per EN 771-x: declared **fb** (N/mm², gross area), declared
  initial bond shear **fvk0** or the fv,lt value, density class, water-vapour
  coefficient mu, net/gross dimensions. If the CE declaration lacks the EC6
  additional properties, the mortar/design route is downgraded (Werkmörtel rule
  of the digest — missing extra properties → one mortar group lower when used
  in NA design). **[VERIFY — exact downgrade clause]**
- Tolerance: units of the same nominal format in one wall must come from one
  production batch family; ground (geschliffene) plan units are identified by
  the manufacturer's thin-joint system approval (abZ), not by eyeballing flatness.
- Storage: pallets flat, off ground, covered (AAC and KS absorb; freeze/thaw on
  saturated units during winter storage damages exposed faces).

---

## Section 3: Characteristic Masonry Compression Strength fmk (NA.D)

The German NA computes fmk from unit strength fb and mortar fm with unit-group
coefficients k (and exponents alpha, beta): the digests list parameter sets —
HLz A/B/E + T1 + KS-Loch: k = 0.68 (M2.5/M5) / 0.70 (M10/M20), alpha = 0.605,
beta = 0.189; thin-joint rows 0.69/0.585/0.162; HLz W / T2-4 / LLz:
k = 0.54/0.56, etc. Vollziegel/KS-Voll/Block k = 0.95; LB V/Vbl k = 0.67-0.79;
PB DM k = 0.90. **Because parameter-row to mortar-row pairing was partially lost
in extraction, use the finished fmk tables below and read NA.Tafel for anything
off-grid. [VERIFY]**

All values N/mm², normal storey-height walls, coarse grading unless noted.
Rows = unit strength class fb; columns = mortar group.

### 3.1 Hochlochziegel groups A/B/E + T1, and KS-Hohlblock/Hochloch (Normalmörtel)

| fb | M2.5 | M5 | M10 | M20 |
|---|---|---|---|---|
| 4 | 2.1 | 2.4 | 2.9 | — |
| 6 | 2.7 | 3.1 | 3.7 | — |
| 8 | 3.1 | 3.9 | 4.4 | — |
| 10 | 3.5 | 4.5 | 5.0 | 5.6 |
| 12 | 3.9 | 5.0 | 5.6 | 6.3 |
| 16 | 4.6 | 5.9 | 6.6 | 7.4 |
| 20 | 5.3 | 6.7 | 7.5 | 8.4 |
| 28 | 5.3 | 6.7 | 9.2 | 10.3 |
| 36 | 5.3 | 6.7 | 10.6 | 11.9 |
| 48 | 5.3 | 6.7 | 12.5 | 14.1 |
| 60 | 5.3 | 6.7 | 14.3 | 16.0 |

Caps at M2.5/M5 are real (weak mortar governs); do not extrapolate beyond fb 28
in low mortar groups.

### 3.2 Hochlochziegel W / T2-T4 / LLz (thin-joint-capable and lighter clay units)

| fb | M2.5 | M5 | M10 | M20 |
|---|---|---|---|---|
| 4 | 1.7 | 2.0 | 2.3 | 2.6 |
| 6 | 2.2 | 2.5 | 2.9 | 3.3 |
| 8 | 2.5 | 3.2 | 3.5 | 4.0 |
| 10 | 2.8 | 3.6 | 4.0 | 4.5 |
| 12 | 3.1 | 4.0 | 4.5 | 5.0 |
| 16 | 3.7 | 4.7 | 5.3 | 5.9 |
| 20 | 4.2 | 5.4 | 6.0 | 6.7 |

(For HLzW and T4 the bracketed lower NA values 3.1/4.0/4.5/5.0 at fb 16-20
apply in some columns — **[VERIFY which]**.)

### 3.3 Vollziegel / KS-Voll / KS-Block (Normalmörtel)

| fb | M2.5 | M5 | M10 | M20 |
|---|---|---|---|---|
| 4 | 2.8 | — | — | — |
| 6 | 3.6 | 4.0 | — | — |
| 8 | 4.2 | 4.7 | — | — |
| 10 | 4.8 | 5.4 | 6.0 | — |
| 12 | 5.4 | 6.0 | 6.7 | 7.5 |
| 16 | 6.4 | 7.1 | 8.0 | 8.9 |
| 20 | 7.2 | 8.1 | 9.1 | 10.1 |
| 28 | 8.8 | 9.9 | 11.0 | 12.4 |
| 36 | 10.2 | 11.4 | 12.7 | 14.3 |
| 48/60 | 10.2 | 11.4 | 15.1 | 16.9 |

### 3.4 KS thin-joint system (Dünnbettmörtel, columns = KS XL / KS-N/E / KS-P)

| fb | col 1 | col 2 | col 3 |
|---|---|---|---|
| 4 | 2.9 | — | — |
| 6 | 4.0 | 3.7 | — |
| 8 | 5.0 | 4.4 | — |
| 10 | 6.0 | 5.0 | — |
| 12 | 9.4 | 7.0 | 5.6 |
| 16 | 11.2 | 8.8 | 6.6 |
| 20 | 12.9 | 10.5 | 7.6 |
| 28 | 16.0 | 13.8 | 7.6 |
| 36-60 | 16.0 | 13.8 | 16.8 / 7.6 |

**[VERIFY column mapping — digest merged the XL / N-E / P rows; read NA.D
before using fb > 16 with thin-joint KS.]**

### 3.5 Light-weight-mortar masonry (LM21 / LM36) and remaining groups

| Unit group | mortar | 2 | 4 | 6 | 8 | 10 | 12-28 |
|---|---|---|---|---|---|---|---|
| Ziegel / KS + LM | LM21 / LM36 | 1.2 / 1.3 | 1.6 / 2.2 | 2.2 / 2.9 | 2.5 / 3.3 | 2.8 / 3.3 | 3.0 / 3.3 |
| LB Hohlblock/Hbn | M2.5 / M5 / M10-20 | 1.4/1.5/1.7 | 2.2/2.4/2.6 | 2.9/3.1/3.3 | 2.9/3.7/4.0 | 2.9/4.3/4.6 | 2.9/4.8/5.1 |
| LB Voll/Vbl | M2.5 / M5 / M10-20 | 1.5/1.6/1.8 | 2.5/2.7/3.0 | 3.4/3.7/4.0 | 3.4/4.5/5.0 | 3.4/5.4/5.9 | 3.4/6.1/6.7 (16: 3.4/6.1/8.3; 20: 3.4/6.1/9.8) |
| LB Vn/Vm/Vbn/Vmb | M5 / M10-20 | — | 2.8/2.9 | 3.6/4.0 | 3.6/4.7/5.0 | 3.6/5.4/6.0 | 3.6/6.0/6.7 (16: 3.6/6.0/8.0; 20: 3.6/6.0/9.1) |
| Beton | MG II / IIa / III+IIIa | 1.4/1.6/1.8 | 2.1/2.4/2.9 | 2.7/3.1/3.7 | 2.7/3.9/4.4 | 2.7/4.5/5.0 | 2.7/5.0/5.6 |
| LB + LM | LM21/LM36 | 1.4 | 2.3 | 3.0 | 3.6 | — | — |
| PBC (AAC) | DM | 1.8 | 3.0 | 4.1 | 5.1 | — | — |
| PHLz B/E | DM classes | 0.75/0.70 ... per DM class **[VERIFY]** | | | | | |

### 3.6 Design values built on fmk

- **fd = zeta * fmk / gammaM** — NA long-term factor **zeta = 0.85**, partial
  factor **gammaM = 1.5** (simplified method uses fmd = 0.85*fmk/1.5; design
  example computes fd = 0.85*fk/1.5 = 1.42 for fmk = 2.5). **[VERIFY gammaM NA cell]**
- Elastic modulus **Ec,calc = Kennzahl * fk**: Mauerziegel **1100** (range
  950-1250); KS **950** (800-1250); LB **950** (800-1100); Beton **2400**
  (2050-2700); PBC **550** (500-650). Used for stiff-centre bracing arithmetic
  (§8) — e.g. AAC wall fk 1.8 -> E = 550*1.8 = 990 MN/m² (digest example).
- Initial shear strength for design (§7): **fvk0 = 0.08 (M2.5) / 0.18 (M5) /
  0.22 (M10) / 0.26 (M20) / 0.22 (DM) / 0.18 (LM) N/mm²**.

---
## Section 4: Mortar (Mörtel)

### 4.1 Groups and use

| Group | Designation | Nominal fm (N/mm²) | Joint | Typical use |
|---|---|---|---|---|
| Normalmörtel | **M2.5 / M5 / M10 / M20** | >= 2.5 / 5 / 10 / 20 | 6-15 mm (nominal 10-12) | general; M5 min for exposed, below-plinth per NA; M10/M20 high loads, KS not with M2.5 |
| Dünnbettmörtel | **DM** (DM 0.5/1.5/2.5 per class) | — | **1-3 mm** | ground plan units only: HLzW/Planziegel, KS XL/P, PB Plansteine, filled-head-joint variants |
| Leichtmörtel | **LM 21 / LM 36** | >= 2.1 / >= 3.6 (light, insulating) | 10-15 (up to 20) | single-leaf clay/LB walls where lambda of joint matters |
| Werkmörtel | EN 998-2 declared | per DoP | — | factory dry mortar; downgrade rule §2.5 if declared properties incomplete |
| Füllbeton | C12/15 - C25/30+ | — | — | grouted cell / reinforced masonry (§10.10), fk <= 12 for unreinforced use cases per NA |

Old-to-new mortar-group mapping (still printed on many details/ATV texts):
MG I ≈ M1-M2.5, **MG II ≈ M5**, **MG IIa ≈ M10**, MG III ≈ M12.5-M20.
Two-leaf outer-leaf rule references "MG >= IIa" — in new notation M10;
verify the exact intent of the source text used. **[VERIFY]**

### 4.2 Mortar selection logic

- **The mortar should not be stronger than needed.** Higher mortar group raises
  fmk only to the cap columns in §3 (fb 4-10 rows show M10/M20 gains of a few
  tenths only) but worsens crack pattern and thermal-joint penalty. Default
  load-bearing: M5 or M10; thin-joint where system-approved; LM for single-leaf
  thermal walls.
- Below-grade and plinth masonry, cellar walls: **M5 minimum, M10 where
  exposure or fb demands**; never M2.5 below the Abdichtung level. **[practice]**
- Head joints of Hochloch units: grouted (Vermörtung) unless the system uses the
  unpointed (offene Stoßfuge) design route — which multiplies through §7 shear
  (2/3 factor) and needs per-face wind caution. Thin-joint DM: bed joint only,
  head joints dry-fit per system (the fvk DM = 0.22 row already assumes the
  system bond).
- Mixing and placement follows the binder rules: cement/lime mortars usable
  within ~2-3 h of mixing, never retempered; do not lay below +5 °C without
  measures; protect fresh beds from rain and drying (§13).

### 4.3 Mortar quantity quick figures

From the KS thin-joint labour digest (§2.2): mortar demand **7-9 l/m² of wall
face** (11.5-15 cm small formats, 29-36 l/m² per m³). For normal-joint brickwork
the joint share of volume is ~ 10-15 % (single-leaf modern formats) — take the
supplier's system figure; **[VERIFY per format]**.

---

## Section 5: ULS Design — Vertical Compression (Centric and Eccentric)

### 5.1 Verification format (simplified, 1996-3 style)

```
NEd <= NRd = Phi * A * fd      (per unit length: NRd = Phi * t * fd * 10^3 [N/m])
fd  = zeta * fmk / gammaM      (0.85 * fmk / 1.5)
Phi = cA  table value (bearing + slenderness reduction), <= 1
```

Load combinations: NEd = 1.35 G + 1.5 Q (NA); the digest allows the alternative
**NEd = 1.4 (G + Q)** only with RC slabs and qk <= 3 kN/m². psi0: live A/B 0.7,
snow <= 1000 m 0.5, wind 0.6 (§ actions digest). Partition allowance to floors:
walls incl. plaster <= 3 kN/m → +1.0 kN/m² surcharge (higher steps for 3-5 kN/m;
none above) — exact NA formula degraded, **[VERIFY]**.

### 5.2 Effective height hef = rho * h

Restraint from slabs/beams at top and bottom; h = clear storey height:

| Restraint | Rule (NA/simplified) |
|---|---|
| 2 sides (top+bottom) | rho2 = **0.75 for t <= 175; 0.9 for 175 < t <= 250; 1.0 for t > 250** — only when head eccentricity <= 0.25t AND bearing depth a >= 2/3 t; timber/ joist floors rho2 = 1.0 with a >= 2/3 t and >= 85 mm; full-bearing RC slab: 0.75 if e <= t/6, 1.0 if e >= t/3 |
| 3 sides | h <= 3.5l: rho3 = 1/(1 + (rho2 h / 3l)^2) - 0.3; h > 3.5l: rho3 = 1.5 l/h - 0.3 |
| 4 sides | h <= 1.5l: rho4 = rho2 / (1 + (rho2 h / l)^2); h > 1.5l: rho4 = 0.5 l/h |
| Free (top unrestrained) | rho free per NA amplification (garbled in digest) — **[VERIFY]**; parapets: cantilever model, wind surcharge below |
| Element masonry lol/hu < 0.4 | hef = alpha * rho * sqrt(1 + (1/3)(rho2 h/b)^2) * h (3-sided) or sqrt(1 + (1/4)... ) (4-sided); alpha3/alpha4 = 1.0 / 0.90/0.75 / 0.83/0.67 / 0.75/0.60 for hu/lu = 0.5 / 0.625 / 1 / 2 |

Bearing-depth conditions (digest set): a >= 100 mm for t < 125 mm; a >= 2/3 t
for t >= 125 mm; simplified method needs a >= max(2/3 t; 85 mm) and t >= 36.5 cm
exception rules — read NA 5.2 with the applicability list before use. **[VERIFY]**

### 5.3 Reduction factor Phi (simplified NA tables)

One-sided end bearing (slab on one side of wall), with a = bearing depth,
lf = slab span, t = wall thickness:

- Ends: **Phi1 = (1.6 - lf/6)(a/t) + 0.9(a/t)^2** (fk >= 1.8);
  **Phi1 = (1.6 - lf/5)(a/t) + 0.9(a/t)^2** (fk < 1.8); roof slabs:
  **Phi = 0.333 a/t**; floor below: Phi1 = a/t.
- Mid-height: **Phi2** table — digest form 0.85(a/t)[1 - 0.0011(hef/t)^2]/(hef/t),
  OCR-garbled. Worked example values: Phi2 = 0.41 governs at hef/t = 62 for
  a/t = 0.53. Use the printed NA.Tafel 2 value; never interpolate between fk
  classes. **[VERIFY]**
- General rules (1996-1-1/NA): capacity factor cA with model
  e = ei + ed + ehc; **ehc = hef/450** (creep), **ed = 0.002 hef** (accidental,
  form partially garbled), **minimum e = 0.05 t** at edges; mid-height
  em = (0.5(Mo+Mu) + Mh)/N + (t - a)/2 axis-shift rule for partial slab bearing;
  end-zone bearing check on the loaded strip: Phi_o = max(1 - 2|eo|/a; 0.9).
  Simplified-method native bounds: cA = **0.40 for hef/tef <= 18; 0.33 for
  18-21**; roof slabs 0.333 a/t. Biaxial: Phi = Phi_y * Phi_z. **[VERIFY]**

### 5.4 Applicability of the simplified method (house-scale)

All must hold (digest-recovered values; some cells stripped):

- <= 3 storeys; uniform storey geometry; plan dimensions >= height/3 rule;
- clear height per Tafel 1.1 by t and fk: t >= 11.5 cm -> 2.75 m; t >= 15 cm ->
  2.75 (3.0 fk>=5; 3.3 fk>=10); t >= 17.5 -> 2.75 (AAC)/3.0/3.3/3.6; t >= 20 ->
  3.3-3.6; t >= 24/30 -> "12t"/unlimited. Single-leaf 11.5 cm exterior only for
  garages (<= 2 storeys, as inner leaf, cross-wall spacing b <= 4.5 m or wall-to-
  window-edge >= 2.0 m). No interpolation between fk classes. **[VERIFY]**
- qk <= 5 kN/m² (living 3.0 incl. partition surcharge in the 1996-3 variant);
  slab span lf <= 6.0 m; roof <= 5 m (light-weight 7 m) — partially stripped;
  bearing a >= t with >= 85 mm floor rules; hef/tef <= 21; full-bearing RC slab
  >= C20/25, >= 180 mm with EC2 7.4.2 compliance and wk <= 1.25 (paired footnote
  d: wk 1.25-2.2 permits h up to 3.0). LB 17.5 only with wk < 1.1; KS 15 cm/3.0 m
  only fk >= 5.5; Ziegel 17.5/3.0 also fk >= 4.7.
- Non-sway bracing per §8; wind eccentricity bounded: end-wall minimum
  surcharge NEd >= 3 qEwd h^2 b / (16 a) * (1 - h/300) when uplift/tension
  threatens (formula as printed, **[VERIFY]**).

### 5.5 Worked check — bearing exterior wall (digest example 2.1, condensed)

HLz 8-0.9/LM21, t = 30 cm, h = 2.51 m, bay b = 4.25 m, partial RC slab
lf = 4.48 m, a = 160 mm. Applicability: H 9.8 < 20 m, lf <= 6, t >= 24, h <=
3.6 = 12t, qk 2.75 <= 5, a = 160 >= 0.5t... all pass. fmk table §3.5 (LM):
fb 8/LM -> fmk = 2.5 -> fd = 0.85*2.5/1.5 = **1.42 N/mm²**. hef (4-sided,
alpha4 = 1): **1.86 m**; Phi1 = 0.455, Phi2 = 0.411 -> Phi = **0.41**.
NRd = 0.41 * 300 * 1.42 * 10^3 = **175 kN/m** > NEd = 115.7 kN/m (1.35G+1.5Q
with wall self 3.88*2.51). Utilisation 66 %. **[VERIFY — example constants]**

General-rules cross-check in the same example produced mid-height Phi_m = 0.41
and end-strip NRd 192-205 kN > NEd 102-115: same order. Rule kept from it:
planned eccentricity should stay <= t/3 even under characteristic loads
(kernel t/6 is the elastic no-tension limit).

---

## Section 6: Local Compression / Partial Bearing (Lokale Druckspannung)

When a beam, lintel or padstone loads an area Ab smaller than the wall section:

```
NEd <= NRd = beta * Ab * fd
Ab   = loaded area (l1 * t)
Aef  = effective spreading area, load spread <= 60 degrees from vertical
       through masonry above/below: lef,m = l1 + 2 * hc * cot 60deg ... (digest
       example computes lef,m = 0.78 m for l1 = 0.20, hc = 2.0) — exact NA
       geometry per 1996-1-1 6.10 [VERIFY]
beta = confinement increase from Aef/Ab (digest example: Ab/Aef = 0.256,
       beta ~ 1.0; EC6 form 1 + sqrt(A2/A1) capped at 3 — [VERIFY cap])
condition used in example: Ab/Aef <= 0.45 and e0 <= t/6
```

**Worked example (digest 2.4):** lintel on PP4-0.55/DM wall t = 15 cm,
bearing l1 = 20 cm, wall height above 2.0 m, NEd = 19 kN. fd = 1.7 N/mm².
NRd = 1.0 * 0.03 m^2-scale * ... = **51.0 kN > 19 kN** pass. The point: a narrow
bearing on a thin plan-stone wall is a first-order check that must be done per
opening — average wall stress proves nothing locally (§5.5 covers the wall, §6
covers the pad).

Practical consequences:

- Every concentrated support (RC beam end, steel beam end, trussed rafter,
  preload anchor) needs either a **padstone (Druckplatte/Auflager) sized by §6**
  or a ring beam that distributes it (§8.3).
- Eccentric bearings (beam butting only the outer shell, wall axis offset) add
  (t - a)/2 to mid-height eccentricity — carry it into §5.3 general rules, not
  into the simplified Phi.
- Bearing stress on the support strip itself: check the end-zone Phi_o rule of
  §5.3 with eo = sum M / N on the depth a.

---

## Section 7: In-Plane Shear (Scheibenbeanspruchung) and Out-of-Plane

### 7.1 Design shear strength

```
fv,d = fv,k0 / gammaM   (gammaM 1.5)
fv,k0 = fv,lt,0 + 0.4 * sigma_d        (mortared head joints — friction + stock)
fv,k0 = (2/3) * fv,lt,0 + 0.4 * sigma_d (open/unpointed vertical joints)
sigma_d = NEd / A  (design compression on the shear section)
```

fv,lt,0 = initial bond shear from §3.6 (0.08-0.26 N/mm² by mortar; DM 0.22;
LM 0.18). Alternative NA route uses the block friction+stock value
**fv,lt,2 = 0.45 * fbt,calc * sqrt(1 + sigma_d / fbt,calc)** with
**fbt,calc = fst * ... 0.032 * fst?** — digest gives fst coefficients by unit:
Hohlblock 0.020 / Hochloch+Grifflöcher 0.026 / Voll ohne Grifflöcher 0.032 /
Voll (other) 0.082, and fbt,calc = 0.032*fst = 0.24 N/mm² appears in the worked
example for fst = 7.5 fb-class — mapping OCR-degraded. **[VERIFY formula]**

Out-of-plane shear (line-supported panels under wind): use the same forms with
**0.6 sigma_d** instead of 0.4 (digest row: mortared fvk0 + 0.6 sigma_d;
unpointed 2/3 fvk0 + 0.6 sigma_d). **[VERIFY pairing]**

### 7.2 Resistance

```
VRd = fv,d * t * lcal * c
lcal = min(1.25 * lc ; lc * (1 - (2/3) * we/lc))  with cantilever-wind terms;
       lc = compression length from eccentricity: lc = 3(lw/2 - e) (no tension)
c    = 1.0 + 0.5*(lambda_v - 1) for lambda_v = h/l > 1 (digest example 1.128)
VRd = (fv,k0 + 0.4 sigma_d)/gammaM * t * lcal   (simplified form)
```

### 7.3 Worked check — shear wall (digest example 2.3, condensed)

PP6/DM (fmk 4.1), t = 24, lw = 2.0 m, h = 2.51, open head joints.
VEd = 1.35*1.56 + 1.5*10.4 = **17.7 kN**. Minimum vertical load (gammaG = 1.0!)
= 73.5 kN: bending e = 0.604 m -> Phi1 = 1 - 2e/lw = 0.396 ->
NRd = 0.396*240*0.85*4.1/1.5*10^3 ≈ **442 kN > 73.5** pass; SLS edge strain
check: e = 0.408 < lw/3 (compression only), lc = 1.78, sigma_D = 0.344,
edge fibre strain below NA limit. Shear: fv,k0 = 0.5*0.22 = 0.11 (open joints);
lc,lin = (2/3) lw (1 - 1.5 sigma_D d / Ed,min)... = 1.19; fv,lt,1 = 0.11 +
0.4*0.257 = 0.213; fv,lt,2 = 0.155 governs -> fv,d = 0.104; lcal = min(1.125 l,
1.333 lc,lin) = 1.59; VRd = 1.59*0.104*240*1.128... = **35.2 kN > 17.7** pass.
**[VERIFY — several formula cells garbled; redo from NA before use]**

### 7.4 Rules of thumb for shear-wall layout

- Shear utilisation is governed by **compression**: a lightly loaded wall is a
  weak wall. Keep floors' tributary loads onto bracing walls (§8), and never
  "relieve" a shear wall by putting a column next to it.
- Walls need the **aspect-ravity discipline**: stocky panels (h/l <= 1) use the
  full friction+stock capacity; slender cantilever cores bend, not shear — check
  bending + Phi1 with the eccentricity and the tension-crack limit lw/3.
- Open-head-joint (unfilled perpend) thin-joint systems reduce shear bond to
  2/3 — the choice saves mortar and lambda through the joint, and buys it back
  in shear design. Make it deliberately, with the §7.1 line in the calc.
- Diaphragm and chord forces at the slab edges must reach the walls through
  the ring beam (§8.3) — shear-wall capacity without load collection is fiction.

---
## Section 8: Bracing Systems (Aussteifung) of Masonry Buildings

### 8.1 Load path, from the digests

- Wall buildings are braced by **cross walls (Querscheiben)**: mutually
  supporting vertical planes with no hierarchy; the corner bond (Einbinden,
  toothing) or an equivalent dowelled joint must carry contact, tension and
  shear — the corner is the touchstone of real wall construction.
- **Floors are the horizontal braces.** A solid RC slab is a true diaphragm:
  four-edge-supported walls, two-way action loads all four walls, positive
  top-edge restraint, chord forces (tie + strut in the slab) delivered into the
  bracing walls. A timber joist floor is NOT a disc — it needs **Ringanker
  (ring anchor/beam)** or historic Schlauder iron ties to gain diaphragm action;
  a joist floor butted and anchored still reduces the wall's buckling length
  from the historic 8H to one storey H.
- Box construction (Wandbau, cell-by-cell) has bracing built into every room;
  cross-wall (row) construction spaces load-bearing walls one dwelling width
  apart; free wall ends of cross walls need edge restraint (diaphragm + bonded
  piers at gables). Frame-with-cores construction hands bracing to RC — masonry
  is then non-load-bearing or lightly loaded, and the masonry rules below shrink
  to out-of-plane checks.

### 8.2 Stiffness distribution (worked digest method, example 2.5)

Procedure for a small masonry house, floors modelled as line hinges
(each bracing wall = chain of single spans, NOT continuous):

1. Wind to wall: load at storey i proportional to the tributary height
   (h/2 above + below). Wind pressure from the NA simplified values
   (digest: q = 0.65 kN/m², H < 10 m, zone 2) with cpe +1.0/-0.5
   (h/d <= 0.25). **[VERIFY current NA.B values]**
2. **Stiffness centre**: ym = sum(E Iy y)/sum(E Iy) per axis, Iy = t*l^3/12 per
   wall; torsion from load eccentricity to that centre. Digest numbers:
   OG ym0 = -3.49 m, sum EIy = 5016.9 (unit set), influence per wall e.g.
   0.83 (OG) / 0.70 (EG).
3. Translation share Sy = EIy_i / sum EIy; rotation share
   Sy,rot = -m * EI_i * e_i / sum(E(I^2 e^2 ...)) per digest form **[VERIFY]**.
4. **Plumbness (verticality) design force**: alpha = theta0 * alphaH * alphaM
   with theta0 = 1/200, alphaH = 2/sqrt(H_total) (digest example: 1/200 * 2/
   sqrt(8.8) = 0.00337), Fi = alpha * Nk,i (permanent and variable separately
   factored). Tributary N per wall from DAfStb-Heft 240 triangle/trapezoid areas.
5. Combinations: wind gammaF 1.5 leading; **plumb/vertical share with gammaG
   = 1.0 on N for shear (minimum vertical)**; the maximum-vertical case must
   also be run (bending governs there).

### 8.3 Ring beam / Ringanker (tension ring)

- Function: hoop that binds walls together, collects diaphragm chord forces,
  distributes lintel-level loads, ties cross walls to exterior walls, and
  suppresses spread at supports. Historic form: iron straps in mortar beds;
  modern: RC beam or U-block/lintel-block system filled with concrete + bars.
- Digest triggers **[practice/conception]**: more than 2 storeys; wall length
  > 18 m; large openings; poor ground; joist floors without structural topping.
- Position: **within 0.5 m of the wall axis** (NA digest: ring anchor tie zone
  <= 0.5 m from wall centreline); continuous around the building — a band that
  stops at a door is not a band. Reinforcement/section design ->
  `concrete-detailing`; keep it on the masonry-side schedule.
- Ring beams at plinth, every floor/lintel level, and roof (parapet rules
  separately). Veneer and Vormauerschale: supported and tied per §9.4/§10.4.

### 8.4 Stability checks that stay in masonry hands

- Out-of-plane of each wall panel between restraints: §5 effective height +
  §7.1 out-of-plane shear + wind bending; the free-top case (unrestrained
  parapet/partition) uses rho free [VERIFY] and the cantilever model with
  minimum surcharge (§5.4 rule) — a free-standing 11.5 cm wall over ~ 0.6-1.2 m
  is a defect waiting for the first gust **[practice]**.
- Wall-overturning at the completed-building level: keep bracing walls loaded;
  uplift Z of the diaphragm couple must be anchored by surcharge — never
  "find" light walls for heavy diaphragm forces.
- Seismic: ductility classes, confinement members, wall-density minima,
  diaphragm detailing under EC8 -> `seismic-design`. Do not port the gravity/wind
  rules above into an earthquake design.

---

## Section 9: Wall Typologies (Wandaufbauten)

### 9.1 Single-leaf (einschalig, monolithic)

- One structural leaf carries, weathers (with render) and insulates (with LM/PB/
  LB units). Joint thickness is a thermal variable: continuous mortar joints are
  linear thermal bridges and the perpend pattern matters for lambda — hence
  thin-joint plan systems and grouted/light mortars for this typology.
- Usual stack-up (warm to cold): internal plaster 10-15 mm / structural leaf
  17.5-49 cm (unit choice §2.4) / external render or exposure-appropriate face.
- Max clear heights by t and fk per §5.4 table; single-leaf 11.5 cm exterior is
  a garage exception only.
- Non-loadbearing single-leaf infill walls (Ausfachungsflächen, unreinforced,
  max area m² by wall height rows ~2.5/3.0/3.5/4.0 m — column pairing
  **[VERIFY]**): t 11.5: 12/8/—; t 15: 12/8/5; t 17.5: 20/14/13/9;
  t 24: 36/25/23/16; t 30/36.5: 50/33/35/23/16. Interpolate by aspect ratio;
  WZ4 note applies.

### 9.2 Two-leaf with cavity (zweischalig)

| Variant | Cavity | Structure |
|---|---|---|
| **Ventilated** | **40-60 mm** (digest NA: 40-60; open air gap insulates only a few cm — beyond that convection kills it; membrane rule: keep air gaps <= 10-15 mm to suppress convection where sealing rather than draining) | inner leaf (structure) + drainage/evaporation gap + outer leaf (weather skin); vents per floor, drain at sill/lintel sills with weeps |
| **Kernschaal / filled cavity (Kerndämmung)** | **<= 15 cm** (digest baukonstruktion rule; fill with hydrophobic mineral wool or loose fill pumped) | no through-connections after fill; ties stay exposed in the vented variant |
| **Cavity ≥ 60 mm rule from conception** | ≥ 40 mm if struck/flush pointed on one face, otherwise **≥ 60 mm** | rain-off + capillary break logic |

- The outer leaf carries its own weight and wind; it is tied back through or
  beside the insulation: **Drahtanker (wire ties) in the bed joints** for wind,
  **Konsolanker (bracket/cantilever anchors) at slab level** for self-weight —
  at least every storey; inner shell connected to primary structure at every
  floor and every bracing wall.
- The thicker the insulation, the larger the eccentric moment of the outer leaf
  (Versatzmoment) → stronger anchors → worse thermal bridges: the two-leaf
  downward spiral; keep brackets at storey height to minimise the eccentricity.
- The outer leaf sees the biggest thermal swings → **subdivide with sealed
  expansion joints**; joints REQUIRED at re-entrant corners (corner movement
  against wire ties spalls corners). Movement-joint spacing of the outer leaf:
  treat as non-loadbearing unreinforced clay = 12 m max (§10.5), and less at
  returns.
- Double-leaf without ventilation (insulation filled, diffusion route):
  condensation risk on the inner face of the cold outer leaf — hygrothermal
  check belongs to `building-physics-thermal-moisture`.
- Sandwich precast (two wythes factory-bonded with core) uses
  Traganker/Verbundbügel taking the same eccentric force — detail per producer.

### 9.3 WDVS / ETICS (Wärmedämmverbundsystem — render-on-insulation)

- Logic: weather skin (reinforced render) bonded directly to insulation boards,
  no penetrations → no fixings thermal bridges; the wall behind can be any flat,
  sound masonry (LB plan blocks, PB, KS, HLz with full-bed adhesive rules).
- Load transfer through the core: bonded surface + local **disc anchors**;
  outer skin must stay light on vertical builds — thicker boards increase the
  offset moment and the slip risk.
- Detailing minima from the digests: base drip + beaded reinforcement;
  armoured top render 3-5 mm with mesh over boards; **plinth zone: continue the
  below-grade waterproofing 30-50 cm above finished ground and protect the
  WDVS plinth with a hydrophobic/render transition (§10.6)**; full-surface bond
  mandatory for airtightness; rear ventilation impossible by design → the
  build-up must tolerate its own moisture (vapour-open boards/render or a
  verified diffusion balance — `building-physics-thermal-moisture`).
- Render system thickness: exterior multi-layer mean 20 mm of which UP ~15 +
  armierung 3-5 + OP by type; WDPS (insulating render system) UP 20-100 mm
  lambda 0.06-0.16 W/(m·K), OP 8 mm (incl 4 mm levelling, min 6 max 12).

### 9.4 Verblendschale / Vormauerblatt (non-loadbearing outer wythe)

- Facing-brick (Verblender) or clinker wythe, **>= 90 mm** thick (NA digest:
  outer leaf >= 90; mortar >= MG IIa), on its own support: **ledges every two
  storeys** with support depth >= **2/3 brick width** (conception digest);
  wire ties horizontally into every bed joint pattern per §10.4.
- Cavity behind facing: vented 40-60 mm; coordination of drain/vent per floor;
  never bridge with mortar droppings (§10.4 keep-clean rule).

### 9.5 Cellar / basement walls

- **Prescriptive route (EN 1996-3, no separate earth-pressure calculation)** —
  limits from the digests: clear height **<= 2.60 m** (2.75 in the Tafel 1.1
  variant), thickness **>= 200 mm** (KS-HL/LB/HLz systems per NA), floor slab
  acting as diaphragm, imposed **<= 5 kN/m²**, no single load > 15 kN within
  1.5 m, **backfill height <= wall height**, no rising ground surface, no
  permanent groundwater pressure, no sliding plane through the waterproofing.
  **[VERIFY list against EN 1996-3/NA]**
- Design route (digest 2.2 form, arch/Bogen model): check BOTH limits —
  max vertical load NRd,max = (1/3) t b fd (arch capacity to the slab) and min
  vertical load NRd,min = gamma_e b he (h/t)/beta_l with beta_l = 20 (one-way,
  b > 2h) to keep the wall in compression under earth pressure. Constants
  partially garbled **[VERIFY]**; worked example: KS R12/M2.5 t24 h2.35 he1.05
  -> NEd 60-121 kN vs NRd 53.8 (min) and 1302 kN (max): pass.
- Execution: expose one side fully or design as retained; backfill only after
  waterproofing cured + protection board laid; weep/drainage plan from
  `waterproofing`; DPC (Querschnittsabdichtung) below the first course above
  the footing AND lap into the floor slab DPC — continuity rule §10.6.

### 9.6 Double wall (Doppelwand) and Vorhalteschale notes

- **Doppelwand**: two mutually independent leaves (e.g. two 11.5-15 cm leaves
  with a narrow air/insulation gap) — acts as two separately-restrained panels:
  each leaf's own bending stiffness counts (arithmetic sum only where a web is
  provided); no composite I-effect. Design each leaf for its restraints; ties
  only where wind/drainage logic allows. Good for acoustics (mass-spring-mass,
  §12.3) when decoupled; bad if rigidly cross-tied.
- **Vormauerschale** (non-loadbearing single wythe in front of a structural
  wall, e.g. 11.5 cm clay facing on a PB/KS inner wall): own foundations or
  ledgers, tied per §10.4, spans vertically between slab supports — treat as a
  braced panel (§8.4), not as part of the load-bearing section, unless the
  design explicitly composites it (then: same mortar, continuous bond, and an
  engineered check).

---
## Section 10: Detailing Rules (Konstruktionsregeln)

### 10.1 Bond, lap and joints (Verband, Überbindung, Fugen)

- **Bed joints continuous and strictly horizontal; head joints staggered per
  course.** The lap (Überbindung, modular offset) is the load-bearing essence:
  horizontal shear travels by friction in the bed joints (activated by the
  normal load), vertical by the interlock — which is why §7's friction+stock
  formula only works if the bond is real. A through-joint (no lap) is a
  mechanical AND thermal weak line: never allowed as a recurring pattern.
- Named bond positions: **Läufer** (stretcher), **Binder** (header),
  **Rollschicht** (soldier course, brick on edge), **Grenadierschicht** (standing
  course). Corners: the same unit rotated — the orthogonal module turns the bond
  around corners without singularities; six orientations per brick (180° about
  each axis). Stretcher (running) bond with half-length offset is the standard
  for modern plan formats; headers needed only at corners/returns/piers.
- Larger formats reduce labour and joint share (joints are the weak points);
  hand-grip slots (Grifflöcher) change the shear group (§7.1 fst list) and
  forbid some unpointed assumptions.
- **Joint thickness:** normal mortar nominal **10-12 mm** (allowed ~6-15 per
  unit family; keep one value per wall); thin-joint **1-3 mm**; LM up to 20 mm
  per product rules. Head joints of HLz: filled (Vollmortel) or deliberately
  open per a system that accounts for the 2/3 shear reduction. **[VERIFY
  current EN 998-2/NA allowed band]**
- Toothing vs. dowels at stops and returns: rack back (raked joints) or tooth
  at future structural connections; where the build order cannot bond corners
  simultaneously, use helical/bed-joint ties or the system's corner dowels —
  designed, not improvised.

### 10.2 Storey-height and layer coordination

- Pick the unit height so storey height = integer layers * (stone + joint):
  8 layers of 71/113 mm formats give the digest planning-grid heights 0.50/
  0.667/1.00/1.333/1.50/2.00 m family (§2.2 grid). Get this wrong and every
  storey ends in a cut course at the soffit — the chronic source of the
  masonry-to-soffit defect (§10.7).

### 10.3 Openings in load-bearing walls — the five classic rules (digest)

1. **Limit opening area fraction** of the wall disc; too much glass turns the
   wall into a forbidden bending frame.
2. **Never open directly against a corner** — it creates a free unbraced
   slender sliver; keep a real pier (Mauerpfeiler) at the corner.
3. **Align openings strictly vertically** (same widths, flush jambs) or let the
   opening ratio grow upward; horizontal staggering forces bending and joint
   tension → diagonal cracks.
4. **Window width is limited by the lintel** (§10.9): every metre of width
   multiplies lintel load and jamb bearing concentration.
5. **Sill panels (Brüstungsfelder) carry nothing** — loads bypass via jambs and
   over the lintel; they may be dropped (french windows) provided enough static
   depth remains between slab edge and lintel.

### 10.4 Wall ties, anchors, ledgers (two-leaf and veneer)

| Item | Rule (digest) | Flag |
|---|---|---|
| Wire ties (Drahtanker) | stainless, **Ø 4 mm** wire, placed in bed joints; density **>= 5 per m²** of leaf, wind-zone rows of 7-9/m² in the NA grid | **[VERIFY exact grid rows]** |
| Tie spacing limits | vertical <= 0.15 (unit set) / horizontal <= 0.85 m (NA forms) | **[VERIFY]** |
| Cavity | **40-60 mm** ventilated; >= 40 mm if flush-pointed one side else >= 60 mm; filled Kern <= 15 cm | — |
| Outer leaf | >= 90 mm; mortar >= M5 (old MG IIa) | **[VERIFY]** |
| Brackets (Konsolanker) | carry outer-leaf self-weight **at slab level, at least every storey; veneer ledges every 2 storeys, ledge depth >= 2/3 brick width** | conception + baukonstruktion |
| Vent openings | per-m² vent requirement for open cavities (value stripped) **[VERIFY]**; keep anchors out of the flow path | — |
| Cavity keep-clean | **no mortar droppings / no bridging**: cavity is a drainage + capillary break — bridging defeats it; strike joints flush on the cavity face, clean every ~ 1 m of lift, lintel/sill drips + weeps maintained | **[practice]** (digest logic: joint = most water-sensitive part; capillary joints wick) |
| Corner movement | expansion joint or articulation at re-entrant corners of the outer leaf | §10.5 |

### 10.5 Movement joints (Dehnungs-/Trennfugen)

Maximum spacing, **non-loadbearing, unreinforced** masonry (NA digest):

| Unit material | Max spacing |
|---|---|
| Clay brick (Ziegel) | **12 m** |
| Lime-sandstone (KS) | **8 m** |
| Concrete / LB | **6 m** |
| AAC (PBC) | **6 m** |
| Natural stone | **12 m** |

- Loadbearing walls, storey-height and long-facade cases: check thermal +
  moisture movement and restraint per project; clay expands irreversibly
  (moisture) while KS/concrete shrink on drying — never couple them without a
  joint; changes of height, thickness, stiffness (RC elements abutting masonry)
  get a joint or a designed flexible tie regardless of run length. **[practice]**
- Joint detail: compressible filler full section + sealant both faces; a
  mortar-filled "joint" is not a joint — it relocates the crack.
- Settlement vs expansion: separations where a light wall lands on a structure
  that deflects (top-down partition rule §10.7; slot zones §10.8).

### 10.6 Plinth, DPC and splash zone (Sockel, Querschnittsabdichtung)

- **Plinth (Sockel):** splash-back + dirt + mechanical damage + capillary reach
  → distinct build-up: dense plinth stone (or the waterproofed package) under a
  porous wall = capillary break + protection; **continue the below-grade
  waterproofing up 30-50 cm above finished ground**, then a hydrophobic plinth
  render as transition to the wall sealing; protect WDVS plinth zones (base
  profile, drip). **[digest baukonstruktion]**
- DPC (horizontal Querschnittsabdichtung) position: in the wall below or at
  finished ground per the waterproofing system, **full wall width, continuous,
  lapped and connected to the floor slab's DPC/membrane** — a wall DPC that
  stops at the floor edge leaves a bypass; never bridge it with aprons, planters
  or backfill laps. System build-ups -> `waterproofing`.
- Below-DPC masonry: dense units (KS-Voll, LB NB, clinker), mortar >= M5 (M10
  where fb demands), no PB below the sealing without a verified drained detail.

### 10.7 Partitions (Nichttragende innenwände, DIN 4103)

- Design line load: **0.5 kN/m at 0.9 m height** (case 1 living/office/hotel;
  case 2 assembly/exhibition/commercial — same 0.5 with different
  combinations); self-weight + finish.
- **Build partitions top-down** (floor settlement must never land on them):
  leave a head slot and fill per system (compressible packing), or mill the
  slot; partitions standing ON floating screed transmit flanking sound — run
  them to the structural slab or cut the screed under the wall.
- Non-loadbearing masonry partitions may span by vault (arch) action up to
  **7 m** between side supports — thrust must be caught at the side connections
  (no free jambs); limit supported floor deflection to l/500.
- Minimum thickness / slenderness of unrestrained partitions: 6.6 cm system
  walls with top restraint are the practical floor **[practice]**; free-standing
  tall slivers follow §8.4 (never open directly against a corner).

### 10.8 Chases and slots (Schlitze) in masonry

Digest grid (NA/Tafel 10.x — row pairing OCR-degraded, **[VERIFY before use]**):

| Wall t | Vertical slot max depth | max width | remaining wall | min spacing |
|---|---|---|---|---|
| 11.5-14.9 cm | 10-20 mm | 100 mm | — | >= 260 mm |
| 15-17.4 cm | 20 mm | 100 mm | >= 115 mm | >= 300 mm |
| 17.5-23.9 cm | 30 mm | 100-125 mm | >= 115-175 mm | >= 385 mm |
| >= 24 cm | 30 mm | 150-200 mm | >= 175-240 mm | >= 385 mm |

- **Horizontal slots: only in walls t > 11.5 cm; never in Hochloch (perforated
  clay) walls** (conception digest rule); limited lengths (~25-30 cm) and
  staggering; no slotting of KS-XL/plan systems outside their approval;
  **mill (fräsen), never hammer-chisel** — impact shatters unit webs and kills
  the local bearing capacity checked in §6.
- Keep slot zones >= 400 mm from wall edges/joints and from corners; never run
  services through ring beams, lintels or grouted cells without the engineer
  (→ `concrete-detailing`).
- Repair: fill with matching mortar; over chases on plaster routes use the
  reinforcement-mesh rule of the finish specification.

### 10.9 Lintels, arches and flat lintels (Stürze)

- **Flat lintel (Flachsturz) arch model** (NA digest): an overbuilt flat lintel
  may be designed by the arch/Bogen model **for spans <= 3 m** when: loading
  only predominantly static, no point loads in the span, lintel reinforcement
  light-weight concrete >= LC 20/22 or B500 bars, **cover >= 20 mm**,
  compression-zone head-joints mortared, units >= fb 12 (HLz diagonal webs >=
  20 mm) or no grip holes, mortar >= MG II, steel strain limited, fk <= ~C20/25
  equivalent, gammaM per EC2-NA. **Partially garbled — [VERIFY the abZ/NA
  conditions line by line].** Reinforced flat lintels otherwise per abZ /
  type statics (Typenstatik) of the system.
- **Masonry arches/jacks:** flat/jack arch (Rollschicht) camber
  **1/50 - 1/12 of span** (digest rule of thumb); wedge joints at the crown
  **5-20 mm**; arch guide spans: 24 cm wall <= 2 m; 36.5 cm wall 2-5.5 m
  **[conception]**; springings need undisturbed piers to take the thrust
  (Rule 4 §10.3); EN 845-2 for the metal/stone lintel products.
- **Bearing:** the digest did not preserve a numeric lintel end-bearing length
  rule — do not invent one; use the system approval / type-statics document of
  the chosen lintel, and check §6 local compression under the jamb
  concentration. (Where a precast concrete lintel is used, its abZ states the
  minimum Auflagerlänge.) **[VERIFY per product]**
- Padstones under concentrated bearings: §6; U-block/PB lintel systems follow
  their abZ span tables.

### 10.10 Reinforced / confined masonry (Bewehrtes Mauerwerk) — pointer

NA digest conditions: mortar >= M5 [garbled], Füllbeton C12/15-C25/30+,
bond-length design l0 + anchoring a per NA, shear VRd = A fvcd + (omega1 +
omega2) form, reinforcement stress limits. Grouted cells, bed-joint ladders,
ring beams and seismic confinement are **designed systems** — sizing, bar
schedules and ductility rules live in `concrete-detailing` / `seismic-design`.
This skill only guarantees the masonry that hosts them is buildable to §10.1
and the mortar group used is on the fmk table it was designed with.

### 10.11 Render / plaster on masonry (Putz, EN 998-1 / DIN 18550)

- Strength classes CS I >= 0.4-2.5 / CS II 1.5-5.0 / CS III 3.5-7.5 /
  CS IV >= 6.0 N/mm²; the **render must stay weaker than the substrate**
  (capillary + stiffness logic): high-strength cement render on PB/LM masonry
  is a cracking machine. **[VERIFY class bands]**
- Water uptake: Wc1 <= 0.5 / Wc2 <= 2 kg/(m²·min^0.5); thermal groups
  WdT T1 <= 0.1 / T2 <= 0.2 W/(m·K); Leichtputz I rho ~1000-1300, II ~600-1100
  kg/m³; insulating render <= 100 mm, lambda 0.06-0.16.
- Thicknesses: exterior multilayer **20 mm mean** (base ~15 + armour 3-5 +
  finish); interior **15 mm** (single-coat factory TM 10 mm); thin-layer 3-5 mm
  (ground plan units, DM system); renovation (Sanierputz) >= 20 mm.
- **Standzeiten (curing between coats): 1 day per mm** of base coat; armour
  layer >= 7 days before finish; WD putz 1 d/10 mm and >= 7 d. Quality levels
  Q1-Q4 per DIN 18550-2/EN 13914-2. Tile substrate: f >= 2.0 N/mm² and
  rho >= 1000 kg/m³ (air lime/earth render NOT tileable).

---
## Section 11: Seismic Confinement — Pointer, Not a Design

Masonry in German seismic zones 1-3 (DIN EN 1998-1/-5 + NA, EC8 per
DIN EN 1998-1/NA Annex for masonry): ductility class, wall-density minima,
confinement members (Stirnzonen), diaphragm action, torsion rules and the
no-calculation prescriptive limits for compact plans (storey count/height,
>= 2 shear walls >= 1.99 m per direction, >= 50 % of wall area from long
walls, minimum thicknesses and wall-area ratios by zone — digest Tafel
4.85-4.87 partially garbled, **never quote them**) are owned by
**`seismic-design`**. What this skill contributes to that conversation:
unit/mortar fmk pairs that satisfy the engineer's chosen fb >= ... floor,
bond quality (§10.1) that makes the friction-shear assumption real, ring-beam
buildability (§8.3), and the EC6 gravity checks that must ALSO pass. The
simplified EC6 method of §5 is NOT valid as the seismic verification.

---

## Section 12: Physical Performance of Masonry (from digests)

### 12.1 Thermal conductivity lambda and vapour mu, by unit family

lambda in W/(m·K), first number = with normal mortar unless a group is named;
mu (vapour diffusion resistance coefficient) in brackets per material digest:

| Unit family | rho kg/m³ → lambda (mu) |
|---|---|
| Clinker / facing brick (dense) | 1800→0.81 · 2000→0.96 · 2200→1.20 · 2400→1.40 (μ 50/100) |
| Solid/hollow/filled clay brick | 1200→0.50 · 1800→0.81 · 2000→0.96 · 2400→1.40 (μ 5/10) |
| **HLz A/B (LM21 / LM36 mortar)** | 550→0.27/0.32 · 700→0.31/0.36 · 900→0.37/0.42 · 1000→0.40/0.45 (μ 5/10) |
| HLz W (filled, thin-joint) | 550→0.19/0.22 … 1000→0.26/0.29 |
| Sand-lime KS | 1000→0.50 · 1200→0.56 · 1400→0.70 · 1600→0.79 · 1800→0.99 · 2000→1.1 · 2200→1.3 · 2400→1.6 · 2600→1.8 (μ 15/25) |
| AAC Planblock | 350→0.11 … 800→0.25 (μ 5/10) |
| LB hollow group 1 (LM21/LM36/NM) | 450→0.20/0.21/0.24 · 600→0.24/0.25/0.29 · 800→0.31/0.32/0.35 · 1000→0.45 · 1200→0.53 · 1400→0.65 · 1600→0.74 (μ 5/10) |
| LB hollow group 2 | 450→0.22/0.23/0.28 · 700→0.30/0.32/0.36 · 900→0.37/0.40/0.46 · … · 1600→0.76 |
| LB solid Vbl (with slits) | 450→0.14/0.16/0.18 … 1000→0.28/0.29/0.32 |
| LB solid other light agg. | 450→0.22/0.23/0.28 … 1000→0.34/0.35/0.42 · 1600→0.62 (μ 10/15) |
| LB solid V | 450→0.21/0.22/0.31 … 1200→0.54 · 1600→0.74 (μ 10/15) |
| EN 771-3 concrete units | 800→0.60 … 2000→1.3 · 2400→2.0 (μ 5/15-20/30) |

Quartz-sand aggregate correction: **+20 % lambda for 2-chamber, +15 % for
3-6-chamber hollow blocks**. Plaster lambdas: gypsum/thin 0.25 · lime/
lime-cement 0.70 · cement 0.90-1.13 · light 0.30-0.50 · insulating 0.06-0.16
W/(m·K) [design-value catalogue route; values from physics digest].
Semi-homogeneous porous masonry (lambda design-value route) applies only for:
HL <= 24 cm any RDK, > 24 cm only RDK >= 1.0; LB hollow <= 24 & RDK >= 0.8;
KS holes <= 50 % round not staggered — otherwise manufacturer-tested values or
abZ needed. **[VERIFY]**

### 12.2 Unit weights for load takedown

Use §2.3 tables; plaster surcharges per face: Kalkzement 20 mm ≈ 0.36 kN/m²,
Zement 20 mm ≈ 0.42, Gips 15 mm ≈ 0.18; WDVS ≈ 0.30 kN/m².

### 12.3 Sound — masses and mass-law curves (DIN 4109 route)

Areal mass m' = t * rho_wall (plaster ~ +24 kg/m² per face lime-cement,
+15 gypsum) **[derived]**:

| Wall | rho_wall | t | m' bare | m' + 2 plasters |
|---|---|---|---|---|
| KS normal 1.8-2.0 | ~1800 | 11.5 cm | 207 | ~255 |
| KS 1.8 | 1800 | 17.5 cm | 315 | ~363 |
| KS 1.8 | 1800 | 24 cm | 432 | ~480 |
| KS 2.0 | 2000 | 30 cm | 600 | ~648 |
| KS 2.0 | 2000 | 36.5 cm | 730 | ~778 |
| HLz 1.4 | 1360 | 24 cm | 326 | ~374 |
| HLz 1.4 | 1360 | 30 cm | 408 | ~456 |
| HLz 1.4 | 1360 | 36.5 cm | 496 | ~544 |
| HLz 0.9 + LM21 | ~910 | 30 cm | 273 | ~321 |
| PB2 0.55 | ~590 | 17.5 cm | 103 | ~151 |
| PB2 0.55 | ~590 | 36.5 cm | 215 | ~263 |
| LB Hbl 1.2 | ~1180 | 24 cm | 283 | ~331 |

Mass-law design curves (physics digest): **mineral masonry R_w = 30.9·lg(m') −
22.2 dB**; **LB: R_w = 30.9·lg(m') − 20.2**; **AAC: R_w = 32.6·lg(m') − 26.1**
(approximate single-leaf pre-design; coincidence and stiffness reduce the
heavy end — plateaus exist). Two-leaf walls:
R_w,2 = 28 + 18·lg(m'1·m'2/(m'1+m'2)) + dR_w,Tr − K, with improvement
dR_w,Tr up to +12…+17 dB depending on joint >= 30/50 mm, filling, and base
separation (grid in physics digest; **[VERIFY]**). Decoupling rule: never run
floors through a two-leaf partition; fill air gaps with soft fibre; rigid links
= acoustic flanking.

### 12.4 Fire resistance (EC6 / DIN 4102-4 tabulated, digest rows)

Non-loadbearing (E) walls, min thickness mm for EI 30/60/90/120/180/240:

| Unit group | EI30 | EI60 | EI90 | EI120 | EI180 | EI240 |
|---|---|---|---|---|---|---|
| Clay brick (500-2400 kg/m³) | 100 | 100 (70 skim) | 140 (100) | 170 (140) | 190 (140) | 210 (170) |
| KS (600-2400) | 70 | 90 | 100 | 140 | 170 | 200 |
| Concrete group 1 LB (400-1600) | 50 | 90 | 140 | 140 | 140 | 190 |
| AAC (350-500) | 70 | 75 | 100 | 100 | 150 | 190 |

Loadbearing (R) walls, REI 30/60/90/120/180/240:
brick g1 (500-800, fb <= 25, alpha <= 0.6): 100/170/200/365/365/370;
KS (1400-2400): 100/100/100/140/200/200; AAC (350-500): 115/115/150/175/
200/200; stricter columns apply for alpha <= 1.0. Utilisation
**mu_fi = N_Ed,fi / N_Rd** must stay in the tabulated range; plaster skim
reduces required thickness per the (parentheses) columns. **[VERIFY —
digest rows compressed; the current DIN 4102-4 / EC6-1-2 tables govern, and
party-wall minima (>= 200 unreinforced / >= 140 reinforced load-bearing /
>= 120 reinforced non-loadbearing with a >= 25) come from the same source.]**

### 12.5 Fire-adjacent detailing that is masonry-side

- Joints and penetrations are as fire-resisting as the wall: no open cavities
  as flues; fire stops in ventilated cavities per compartment; lintel/sill
  penetrations need rated closures (→ sibling skills for products).
- Unprotected cavities behind rainscreens carry flashover risk: horizontal
  Brandschott at plinth/storey line **[baukonstruktion]**.

---

## Section 13: Execution, Tolerances and Quantities

### 13.1 Build rules (masonry-side specification)

| Rule | Value |
|---|---|
| Max daily lift | **1.2-1.5 m** of fresh wall **[practice]** — lower with lean mortar or heat |
| Level difference between adjacent panels | <= 1.0 m; raise uniformly |
| Bed-joint alignment | continuous, horizontal; no spreading of joints to absorb tolerance — step courses at planned layers (§10.2) |
| Head joints HLz | filled per chosen design route; open-joint systems only with the §7.2/2-3 assumption in the calc |
| Thin-joint (DM) | butter full bed length, 1-3 mm, no head mortar, clean soffit bearing; do NOT wet plan units |
| Wetting | clay units surface-damped in hot wind; KS/PB/LB: **not soaked** — dampen bedding face only (binder digest: too-saturated units dry in the wall and pull joints) |
| Protection | cover wall top at day's end; no loading green masonry; protect against rain washout and frost < +5 °C (heated enclosure or stop) |
| Curing | keep mortar damp ~2-3 days minimum in heat; mortar cubes per project spec **[practice]** |
| Stop-ends | rack back raked; tooth only at designed future connections |

### 13.2 Labour and material figures (KS thin-joint system, digest)

Wall height <= ~3 m, full masonry (Arbeitswerte h):

| t | units | St/m² | St/m³ | h/m² | h/m³ | mortar l/m² |
|---|---|---|---|---|---|---|
| 11.5 | 4DF (248x115x238) | 16 | 139.5 | 0.55 | 4.80 | 7.0 |
| 15 | 5DF | 16 | 107 | 0.60 | 4.00 | 9 |
| 24 | 4DF (248x240x113) | 31 | 128 | 0.47 | 1.95 | (pairing garbled **[VERIFY]**) |
| 30 | 5DF | 32.5 | 107 | 0.59 | 1.95 | (as above) |

Grouted/pointed variants add ~ 0.05-0.10 h/m². These are planning values for
a site crew of average skill, single-storey panel, no scaffolding time;
wastage allowance on materials 2-5 % (digest).

### 13.3 Tolerances

**DIN 18202 (Table 3, deviations of building components) and DIN 18203
(execution of masonry works) were NOT present in the digests. Do not quote
tolerance figures from memory.** State in the spec: "deviations per DIN 18202
Tab. 3 (survey) and DIN 18203/ATV DIN 18330 (execution); acceptance measured
against the nominal module lines, not against adjacent trades' averages."
The ATV DIN 18330 structure itself IS digested: Geltungsbereich / Stoffe /
Ausführung / Nebenleistungen / Abrechnung (§1 Baubetrieb digest) — use it to
write the works description, and pull numbers from the standard text.

### 13.4 ATV DIN 18330 scope notes

Masonry works are ATV DIN 18330 within VOB/C (2019 list): natural stone
18332/18333 separate; WDVS is 18345; render is 18350 — spec each layer with
its own ATV so measurement and objections are clean. **[digest Baubetrieb]**

---

## Section 14: Typical Damages — Cause → Prevention

| Damage | Root cause | Prevention (this skill's clause) |
|---|---|---|
| Random vertical/diagonal cracks in long single-leaf runs | thermal + moisture movement with no movement joints | §10.5 spacings per material; joint at stiffness changes |
| Stepped cracks following joints at returns | no lap / through-joints, weak bond | §10.1 Überbindung discipline |
| Corner spalls on outer leaf / veneer | thermal movement fighting fixed wire ties | §9.2/§10.4 corner expansion joints, tie density per wind zone |
| Damp bands above plinth, salt (efflorescence) | DPC bridged by aprons/backfill; brackish mixing/curing water | §10.6 continuity, full-width DPC; potable water; keep cavity clean §10.4 |
| Penetrating damp at sill/lintel of cavitor | mortar droppings bridging cavity; no drip/weep | §10.4 keep-clean; sills with overfall and drips |
| Cracks over windows/doors | flat-lintel without arch capacity, missing statical depth, point loads in arch zone | §10.9 conditions incl. "no point loads"; §6 under bearings |
| Local crushing under beam ends | narrow bearing without padstone | §6 worked-check habit |
| Shear cracks at building corners, diaphragm tears | joist floors acting without Ringanker; unbraced free wall ends | §8.1/§8.3 ring anchor + pier rules |
| Bulging/buckled thin partitions | top not restrained, built bottom-up into settlement | §10.7 top-down + head slot |
| Plaster crazing/debonding on PB | render stronger than substrate, coats too thick, no Standzeit | §10.11 CS-class match, 1 d/mm |
| Thermal-bridge stripes/mould at ring beam, lintel, corner, anchor points | insulation plane broken by structure/fixings | §9.2 bracket placement, continuous plane, WDVS logic; → `building-physics-thermal-moisture` |
| Frost spalling of exposed units | saturated units, no drip, porous unit in splash zone | §2.5/§10.6 dense units where exposed; drips; covered tops |
| Corroded ties staining/ejecting outer leaf | carbon steel in unventilated wet cavity | stainless ties, correct cavity class §10.4 |
| Through-crack continuing into RC column line | dissimilar stiffness bonded without slip/articulation | §10.5 joints; DIN 4103 partition rules |

---

## Section 15: FreeCAD / BIM Encoding

### 15.1 Modelling conventions

- Model **real nominal thicknesses** from §2.2 (115/150/175/240/300/365 mm,
  plus cavity and leaf additions); build-ups via **Arch MultiMaterial** so the
  model reports structure + cavity + insulation + render separately; keep the
  structural leaf as the reference line.
- `Arch.makeWall(base, height, width)` with explicit `Width`; openings as live
  boolean `Subtractions` (never frozen); wall layers named per §9 typologies
  ("KS 240", "Kerndämmung 120", "Verblender 115").
- Assign materials with real densities from §2.3 (KS 1800-2000, LB Hbl 800-
  1400, PB 500-650, HLz 900-1400, clinker 1800-2000 kg/m³) so mass and
  self-weight takeoffs mean something.
- IFC mapping: `IfcWall` with `PredefinedType` **LOADBEARING / NONLOADBEARING /
  PARTITION / PARAPET / SHEAR / RETAINING_WALL / PLUMBINGWALL**; two-leaf walls
  as `IfcWall` + `IfcMaterialLayerSetUsage` (layer order inner→outer, cavity as
  AirLayer or Void); fire/masonry properties as custom `Pset_Masonry`
  (`fb_class`, `fmk_MPa`, `mortar_group`, `RDK`, `wall_typology`). A structural
  export consumer needs fmk and mortar group as properties — geometry alone
  loses the design. **[practice]**
- Cell filling / grout / ring beams: model as separate `IfcBeam`/`IfcMember`
  objects on the wall axis, not as thickened wall — they are a different
  material and a different trade.
- Tag bracing walls `SHEAR` and keep their lengths honest: a wall cut by a
  door is two piers for §8.2 purposes — model the cut, don't hide it.

### 15.2 Quantity takeoff script (FreeCAD Python console)

```python
# Masonry takeoff by nominal thickness: volume, units, mortar, mass.
# Planning aid only — verify against the system supplier's per-format table.
import FreeCAD as App

STONES_PER_M2 = {115: 16, 150: 16, 240: 31, 300: 32.5}   # KS thin-joint, §13.2
STONES_PER_M3 = {115: 139.5, 150: 107, 240: 128, 300: 107}
MORTAR_L_M2   = {115: 7.0, 150: 9.0}                      # thin-joint only [VERIFY t24+]
RHO_WALL      = {115: 1800, 150: 1800, 240: 1800, 300: 1800}  # KS 1.8 default

doc = App.ActiveDocument
tot = {}
for o in doc.Objects:
    if getattr(o, "IfcType", "") != "Wall" and "Wall" not in o.Name:
        continue
    try:
        t = int(round(float(o.Width.getValueAs("mm"))))
        v = o.Shape.Volume / 1e9
    except Exception:
        continue
    tot[t] = tot.get(t, 0.0) + v

print(f"{'t':>5} {'V m3':>8} {'mass t':>8} {'St/m3':>7} {'units':>9} {'mortar l':>9}")
for t, v in sorted(tot.items()):
    m  = v * RHO_WALL.get(t, 1600) / 1000.0
    spm = STONES_PER_M3.get(t, 100)
    mor = v * (t / 1000.0) * 0  # thin-joint l/m2 only for listed rows below
    if t in STONES_PER_M2:
        mor = (v / (t / 1000.0)) * MORTAR_L_M2.get(t, 0)
    print(f"{t:>5} {v:>8.2f} {m:>8.2f} {spm:>7} {v*spm:>9.0f} {mor:>9.0f}")
print("PLANNING AID ONLY — not a construction quantity.")
```

### 15.3 Model-level checklist before any export

- [ ] Every wall has a §2.2 nominal thickness and a §9 typology it can be built as.
- [ ] Load-bearing walls: thickness + fmk pair exist in §3 (no off-table inventing).
- [ ] Bracing directions have continuous walls with modelled openings (§8.2).
- [ ] Ring beam objects exist at plinth/floor/roof, within 0.5 m of axes (§8.3).
- [ ] Cavity widths from §9.2/§10.4 grids; outer leaf >= 90 mm where veneer.
- [ ] Movement joint gaps modelled where §10.5 spacing is exceeded.
- [ ] Materials carry real densities; `PredefinedType` set; Pset with fmk/mortar.
- [ ] Fire table §12.4 thickness respected for compartment/REI walls.
- [ ] Output text states this is a planning model needing engineer sign-off.

---

## Section 16: Verification Checklist (run before issuing any masonry output)

1. Applicability proven: <= 3 storeys / heights per Tafel 1.1 band / qk and
   bearing-depth conditions (§5.4) — or the design left the simplified method.
2. fmk read from §3 for the EXACT fb-mortar pair; no interpolation; zeta 0.85,
   gammaM 1.5 applied (§3.6).
3. hef with the correct rho and restraint class; bearing depth a and slab type
   matched (§5.2).
4. Phi from the NA tables re-checked against the printed standard — every Phi
   cell flagged [VERIFY] in §5.3 was looked up, not guessed.
5. Minimum-vertical case run for shear (gammaG 1.0) AND max-vertical for
   bending (§7.3/§8.2); open-joint reduction applied where specified.
6. Local compression done at every concentrated bearing (§6).
7. Bracing: stiffness centre + plumbness alpha + ring beam continuity (§8).
8. Two-leaf: tie type/density/spacing, ledge depth >= 2/3 brick, cavity clean
   rule stated (§9.2/§10.4).
9. Movement joints where §10.5 spacing is exceeded; at corners and stiffness
   changes.
10. Plinth 30-50 cm above grade; DPC full-width and continuous with floor;
    no bridging (§10.6).
11. Lintel route (arch model vs abZ product) conditions met incl. no point
    loads; bearing checked §6; spans within guide (§10.9).
12. Fire: EI/REI thickness from §12.4 or EC6-1-2 table actually quoted.
13. Sound: mass + curve estimate sanity-checked (no 11.5 KS promised 50 dB).
14. Seismic demand present → `seismic-design` involved; EC6 simplified used
    only for gravity/wind (§11).
15. Every [VERIFY] number in the output either replaced from the primary
    standard or still labelled [VERIFY].

---

## Appendix A: Standards Cited

| Standard | Scope | Used for |
|---|---|---|
| **DIN EN 1996-1-1 + NA (2010/2012 editions in digests)** | Design of unreinforced/reinforced masonry | fmk k/alpha/beta grids, fd, Phi/cA, e rules, shear forms, local compression, NA.D tables §3.6-§7 |
| **DIN EN 1996-3 + NA** | Simplified calculation methods (1996-3) | Tafel 1.1 heights, applicability, cellar-wall arch model, flat-lintel arch model |
| **DIN EN 1996-1-1/-2 (fire) + DIN 4102-4** | Fire resistance of masonry | EI/REI thickness rows §12.4 |
| **EN 771-1/-2/-3/-4/-6 + DIN 105-100, V 106, V 18151-153, V 20000-401..404** | Masonry unit products | unit groups, fb, RDK, formats, DoP data §2 |
| **EN 998-2 / Werkmörtel + DIN EN 19918 series** | Masonry mortars | M/DM/LM groups, downgrade rule §4 |
| **DIN 4172** | Dimensional coordination (BM 12.5 cm) | Richtmaß/Nennmaß, planning grid §2.2 |
| **DIN EN 1990 / 1991-1-1/-1-3/-1-4 + NA** | Actions | combinations, partition surcharge, wind/snow §5.1, §8.2 |
| **DIN EN 1998-1 + NA** | Seismic | routed — `seismic-design` §11 |
| **DIN 4108-4 / DIN 4109-33** | Physical design values / sound design values | lambda/mu, mass-law curves §12 |
| **DIN 4103-1** | Stability of non-loadbearing walls | 0.5 kN/m line load, top-down rule §10.7 |
| **VOB/C ATV DIN 18330 (18332/33, 18345, 18350)** | Contract execution scopes | spec assembly §13.4 |
| **DIN 18202 / DIN 18203** | Tolerances / masonry execution | referenced, NOT digested §13.3 |
| **DIN 18550 / EN 13914 / EN 998-1** | Render | CS classes, thicknesses, Standzeiten §10.11 |
| **DIN EN 1055 / EN 1991-1-1/NA weight tables** | Unit weights | gamma by RDK §2.3 |

## Appendix B: Items to VERIFY Against the Primary Standards Before Citing

| # | Item |
|---|---|
| 1 | NA.D fmk tables §3.1-§3.5 — every column/pairing flagged (esp. KS thin-joint cols, HLzW bracket cells, LM rows) |
| 2 | k/alpha/beta parameter sets per unit group (§3 intro) |
| 3 | gammaM NA value (1.5 used; cell stripped) and simplified combination 1.4(G+Q) conditions |
| 4 | Phi2 mid-height table and free-top rho (§5.2/§5.3) |
| 5 | cA general-rules forms, ed formula, e_min 0.05t application (§5.3) |
| 6 | Tafel 1.1 storey-height band incl. footnote-d pairings and 11.5 cm garage exception (§5.4) |
| 7 | Minimum-surcharge wind formula §5.4 (as printed) |
| 8 | Local-compression: exact Aef geometry (60° spread form) and beta cap (§6) |
| 9 | fv,lt,2 block formula + fst coefficient mapping (§7.1) |
| 10 | lcal/c-factor formulas and out-of-plane 0.6 sigma_d pairing (§7) |
| 11 | Bracing torsion-share formula + NA.B wind simplification values (§8.2) |
| 12 | Cellar arch-model constants (1/3, 7.8/20, two-way 0.5) (§9.5) |
| 13 | EN 1996-3 prescriptive cellar list wording (§9.5) |
| 14 | Two-leaf tie density rows by wind zone + tie spacing limits + vent rate (§10.4) |
| 15 | Slot grids §10.8 row pairing; horizontal-slot length/spacing rules |
| 16 | Flat-lintel arch-model condition list and span limits; lintel bearing length from the chosen product's abZ/Typenstatik (§10.9) |
| 17 | Movement-joint loadbearing variants and joint widths (§10.5) |
| 18 | Fire table full columns incl. alpha and mu_fi ranges (§12.4) |
| 19 | Semi-homogeneity limits and quartz-sand lambda corrections (§12.1) |
| 20 | Tolerances from DIN 18202 Tab.3 / 18203 (absent in digests) (§13.3) |
| 21 | KS 24/30 cm mortar and labour pairings (§13.2) |
| 22 | Mortar-group downgrade rule for CE-markings lacking EC6 properties (§2.5) |
| 23 | Ausfachungsflächen column-to-height mapping (§9.1) |
| 24 | Current NA editions (digests reflect ~2021/22 state: EC6 2010/NA 2012, EN 1991/NA 2011-2019) |
