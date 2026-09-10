---
name: openings-windows-doors
description: >
  Openings, lintels and window/door construction for DACH residential and light
  non-residential building: lintel types (precast concrete U-/Flachsturz, brick
  arch and rolling-course lintels with arch action valid to spans ~3 m, steel
  angle over veneer, bed-joint reinforced lintels per EN 845), bearing lengths,
  edge distances and EN 1996-1-1 §6.2.3 partial-bearing (Teillast) checks with
  spread factor beta; deflection and camber rules; header-to-wall and
  jamb-to-ring-anchor connections; window build-up (frame materials with U_f
  table, glazing Ug/g values, Uw combination formula per DIN EN ISO 10077 with
  warm-edge spacer psi_g corrections and frame-fraction tables, mullion/Sprossen
  correction, box windows), sill/head/jamb detailing under the multi-stage
  sealing principle (Dichtungsstufen / three-joint rule: outer rain-ready and
  vapour-open, middle insulated, inner airtight), mounting classes per EN 12207
  (air) / 12208 (rain) / 12210 (wind), anchor fixing rules, reveal insulation,
  windowsill falls and drip edges, rain flanges and cavity trays for Zweischale,
  roller-shutter boxes (DIN 4108-2 Roka rules); doors (U_D tables, thresholds
  and acoustic combination rules, fire doors cross-referenced, escape widths
  cross-referenced); physical coordination — airtightness-layer continuity
  through the frame, acoustic weak-spot logic (R_w of window vs wall), solar
  gain g and shading factors F_s; schedule management (Fensterliste data model
  and IFC IfcWindow/IfcDoor properties via FreeCAD Arch.makeWindow/Door plus
  verified gotchas: hand-set Window Normal corrupts buildShapes, Base sketch
  Placement has no effect — verify everything with Shape.BoundBox); wall
  openings in timber and steel framing; worked examples (Uw build-up, lintel
  arch action, partial bearing, acoustic combination); failure patterns and
  checklists.
---

# Openings, Windows, Doors and Lintels (DACH Practice)

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

An opening is a hole punched in three things at once: the load path, the
weather envelope and the airtightness layer. A lintel solves only the first —
and it is the *detailing* of the joint between frame and wall that decides
whether the other two survive the first winter. This skill is a
**preliminary sizing, detailing and modelling aid** for openings in 1–5
storey masonry, RC-frame and timber buildings as actually built in Germany,
Austria and Switzerland: which lintel type, how deep, how it bears, how the
window sits in the reveal, how the seal layers are staged, what the whole
opening does to the Uw, Rw and g of the façade, and how to model it all
parametrically without lying to the IFC export.

Pair with `masonry-construction` (wall design, partial bearing, ring anchor,
slotting rules), `concrete-detailing` (lintel reinforcement, anchorage,
cover), `timber-steel-design` (notched members, header design, screw/anchor
groups), `building-physics-thermal-moisture` (U/psi/Glaser/airtightness
background), `building-acoustics` (flanking, combination formulas),
`fire-protection-building` (T-doors, rescue windows, escape routes),
`accessibility-universal-design` (clear widths, zero-step thresholds),
`building-materials` (anchor subcategories), and `construction-freecad-bim`
(void-cut and IFC workflow this skill's modelling section builds on).

## Reality Check — Licensing & Liability

**This skill produces design aids and calculation guidance for planning and
FreeCAD modelling ONLY.**

- Every lintel depth, bearing length, bar count, arch rise, Uw, R_w and g
  value printed here is a **preliminary working value, a rule of thumb, or a
  code reference level**. Your opening is not typical until someone has
  checked it.
- In Germany, load-bearing and stability-relevant design (including lintels,
  ring anchors and the compensation for openings in bracing walls) must be
  prepared by a **statisch verantwortlicher Tragwerksplaner** per the
  applicable Landesbauordnung, and in Prüfsachgebiet buildings reviewed by a
  Prüfingenieur (§ type Prüstatik). Austria: statikverfahrene
  Baubewilligung / befugter Ziviltechniker; Switzerland:
  SIA-qualified Ingenieur/in plus cantonal approval. Nothing replaces that.
- Building permits (Baugenehmigung) additionally require the local authority's
  byelaws (Landesbauordnungen, BauVOs) — room heights, Rettungswege,
  Brüstungshöhen,Abstandsflächen — which are *separate from* the structural
  rules paraphrased here.
- **Say this unprompted** whenever the user starts treating output as final —
  asks for a Bewehrungsplan to hand to the builder, says the Fensterliste goes
  to the window maker as-is, asks whether they can widen the sliding door
  "because the model still stands", or wants to cut a new opening in an
  existing wall. A Fensterliste sent to a manufacturer without a checked
  building-physics-thermal-moisture review (Uw, g, Rw, class) is an expensive mistake; a
  lintel cast from this file's tables without an engineer's check is a life
  safety mistake.
- **Never certify.** No stamped calculation, no "bauphysischer Nachweis", no
  signature block. Label output "preliminary — coordination basis".
- Verbatim norm text is not reproduced here. DIN EN 1996-1-1 + NA (masonry,
  partial bearing, lintels), DIN EN 1992-1-1 (RC lintels), DIN EN 845-1/-2
  (masonry lintels — product standard), DIN EN ISO 10077-1/-2 (windows),
  DIN 4108 (thermal), DIN 4109 + -35 (sound), DIN EN 12207/12208/12210
  (window performance), GEG (energy limits), MBO/LBO (escape, rescue windows)
  contain the governing text.
- Values reconstructed from digested references carry **[VERIFY]**: re-check
  them in the current norm edition before quoting them into a submission.

---

## Section 1: Fast Answers and the Opening Decision Tree

### 1.1 Fast answers (use these first, then verify downstream)

| Situation | Answer |
|---|---|
| Any opening in masonry, any width | **Needs a lintel or proven arch action.** No exceptions — not even a 400 mm bathroom vent. |
| Door 885–1135 mm (common Raumtür Rohbaumaße), 24 cm HLz wall | Precast concrete lintel (U-Profil + Füllbeton) or Flachsturz **h ≥ 115–175 mm**, bearing ≥ 150 mm, orientation marked |
| Window 1200–1500 mm, 24 cm wall | Lintel **175–200 mm**, 2 Ø10/12 bottom, bearing 150–200 mm; or brick rolling-course arch if rules in §4.4 hold |
| Opening 1500–2100 mm | Lintel **200–240 mm** + jamb verticals (Konstruktionsstützen/Ringanker-anschluss), bearing ≥ lintel depth |
| Opening 2100–3000 mm | **Designed beam** — not a catalogue lintel; check deflection L/600 if masonry rests on it |
| Opening > 3000 mm | Load-bearing masonry has run out at this width. RC frame, Stahlbetonfertigteilsturz or steel — engineer's job. Re-check bracing (§10). |
| Head level | Standardise one lintel level per storey across the whole wall — that is what lets individual lintels join into a working **Ringanker/umllaufendes Band** |
| Bearing each side (masonry) | Greatest of **150 mm**, lintel depth, span/12 — then check partial bearing (§5) |
| Arch action (Bogenwirkung) | Only in bonded, continuous masonry, span ≤ ~3 m; void it for point loads in the wedge, fresh masonry, truncated wall above (§4.2) |
| Brüstungsfeld (sill panel under window) | Structurally unloaded — loads bypass via jambs; may go to floor (Bodentür/Französisches Fenster) if enough static depth remains between slab edge and lintel |
| Two stacked openings | Align strictly, equal widths, flush jambs; vertical staggering forces horizontal bends → cracked joints |
| Opening at a corner | Keep a real corner pier (Eckpfeiler); never open directly against the wall end |
| Pier between two openings | ≥ 400–600 mm; below that: vertical joint reinforcement or a Konstruktionsstütze |
| Cavity / Vorsatzschale | Steel angle or double lintel + **cavity tray (Dichtungsband, stepped into the cavity) above it and weep holes (Lotschlitze / open head joints)** or damp above the window |
| Sliding door / glass wall in a bracing wall line | Lateral capacity lost — compensate (§10) before drawing it |
| Full-height opening, head at slab soffit | No separate lintel — the slab edge/edge beam IS the lintel (with local top reinforcement) |
| Window joint build-up | **Three layers, three jobs** (§8): outer rain-ready & vapour-open, middle insulation (airtight), inner airtight & vapour-tight. Montageschaum alone seals nothing |
| Replacement-window retrofit limit (GEG, existing) | Uw ≤ 1.3 (glazing-only exchange: Ug ≤ 1.1); new build reference Uw 1.3, g 0.60 |
| Window air class | EN 12207 class 2 for ≤ 2 storeys, class 3 above (functional joint); with durable replaceable perimeter soft seal a window reaches class 3 anyway |

> **On the 2100–3000 mm row:** this band is *not* one section. Required depth
> grows from ~200 mm at 2.1 m toward 300 mm and more near 3 m; go to §3.3/§6
> for the band you are in and treat "designed beam" as the default answer.

### 1.2 Which system carries this opening?

```
START: opening of clear span l in a wall
│
├─ Q1. What is the wall?
│   ├─ Load-bearing / confining masonry (Mauerwerk, KS, PB, HLz) ....... Q2
│   ├─ Infill in an RC frame (Ausfachung) ............................. Q4
│   ├─ Zweischale / Vormauerschale over backup or WDVS ................ steel angle + tray (§6.4)
│   ├─ Timber frame (Holzrahmen/Tafel) or CLT (Brettsperrholz) ........ §11.1
│   └─ Cold-formed steel stud wall ................................... §11.2
│
├─ Q2. Clear span l?
│   ├─ l ≤ 1.0 m ....... small precast lintel / U-Sturz min depth, or rolling-course arch (§4.4)
│   ├─ 1.0 < l ≤ 2.1 m . precast or in-situ lintel per §3.3 band
│   ├─ 2.1 < l ≤ 3.0 m . DESIGNED lintel beam: top+bottom steel, stirrups, jamb ties, L/600 check
│   ├─ 3.0 < l ≤ 3.5 m . practical limit of masonry-supported lintels; engineered + piers both sides
│   └─ l > 3.5 m ....... convert that bay: RC frame / steel beam / load-bearing window.
│                        Recompute bracing (§10).
│
├─ Q3. Is this wall an aussteifende Scheibe (bracing wall)?
│   ├─ Opening ≤ ~25 % of wall length ...... normally absorbable; check piers & ring anchor
│   ├─ 25–50 % ............................ capacity drops sharply — engineer it
│   └─ > 50 % or head at ring-beam level ... that line stops bracing; add length elsewhere
│
├─ Q4. Infill panel in an RC frame — is the opening full height of the panel?
│   ├─ Head at beam soffit ................ the frame beam IS the header. No lintel.
│   ├─ Head ≤ 1 course below soffit ....... build up in masonry; no lintel
│   ├─ Head > 1 course below soffit ....... lintel required (§3.3)
│   └─ Sill band below a ribbon window .... short-column (Kurze-Stütze-)Risiko — isolate the
│                                          infill with a soft joint or design the column for it
│
└─ Q5. Is an arch wanted (Rundbogen, Segmentbogen, Blendbogen)?
    ├─ Decorative only .................... concrete lintel at true head, arch as
    │                                     Vorblende, labelled non-load-bearing
    ├─ Structural rolling-course arch, l ≤ 1.3 m (24 cm) / 1.6 m (36.5 cm) ... §4.4 rules
    └─ Anything larger / flat / unbalanced abutments ... engineered thrust analysis
```

### 1.3 Standard residential openings (DACH metric defaults)

Model these as *Rohbaumaße* (shell dimensions); the window maker deducts the
mounting gap (Montagefüge) and the mason deducts putty/plaster — carry both
in the Fensterliste (§13).

| Opening | Rohbaumaß B×H (mm) | Brüstung (mm) | Head (mm) | Typical lintel |
|---|---|---|---|---|
| Room door (Zimmertür) | 1010 × 2110 (Licht 885 × 2010) | — | 2125 | 240 × 175 |
| Flat white door to DIN | 885 / 1010 / 1135 widths | — | 2125 | as above |
| Entrance door (Haustür) | 1135 × 2135 | — | 2150 | 240 × 200, designed |
| Bathroom / storage door | 885 × 2110 | — | 2125 | 240 × 150–175 |
| Double room door (Raumtür doppelt) | 1760–1835 × 2110 | — | 2125 | designed beam |
| Room window (standard) | 1200 × 1400 | 900 | 2325 | 240 × 175 |
| Living-room window | 1600–1800 × 1400 | 750–800 | 2200–2325 | 240 × 200 |
| Panorama / sliding (Hebe-Schiebe) | 2400–3600 × 2100–2500 | 0 | designed | designed beam + jambs, §10 |
| Kitchen window over worksurface | 1200 × 1000 | 1000 | 2025 | 240 × 150 |
| Bathroom high window | 600 × 600 | 1600–1800 | 2225–2425 | 240 × 115 |
| Cellar window (Kellerfenster) | 1000 × 600 | ~1500 below FFL | — | wall-over opening, check Teillast (§5) |

Notes:
- One head level per storey beats mixed head levels for exactly the reason it
  always has: one continuous lintel level = a real Ringanker = one soffit line
  = a wall that behaves as a box.
- Rescue openings (Rettungsöffnung, MBO): any room needing a second escape
  route needs an opening ≥ 0.90 × 1.20 m clear (or reachable from a
  Rettungleiter-Anlegerfläche ≤ 8 m height band). That constrains *window*
  sizes and sill heights — cross-check `fire-protection-building` before
  locking the Fensterliste.
- Clear width for accessibility: a 885 mm door gives ~875 mm clear; 900–1010
  is the visitable choice. See `accessibility-universal-design`.
- Brüstungshöhe guard logic (LBO/Tabellen, VERIFY per state): glazing in
  doors and low sills needs safety glass (ESG/TVG/VSG per DIN EN 12600) and,
  outside ground level, fall-prevention measures depending on drop height.

---

## Section 2: Opening Geometry Rules in Masonry (what keeps the wall a wall)

These are the perforated-façade rules of wall construction; they predate the
Eurocodes and still govern what a mason will accept.

| Rule | Value | Why |
|---|---|---|
| Opening area fraction | keep modest; ≤ ~50 % of wall length per storey as working limit (§1.2 Q3) | each opening weakens the disc; too many and the wall degenerates into a frame — with bending in members masonry cannot do |
| Alignment | openings strictly stacked, same width, flush jambs, or ratios **widening upward** | loads accumulate downward — the solid wall you need is lower; horizontal staggering forces horizontal bends → tension in bed joints → cracks (exception: RC walls) |
| Corner distance | never open directly against a corner; keep a full-depth Eckpfeiler | opening at the end = free wall edge = unbraced slender sliver = overturning/buckling |
| Pier between openings | ≥ 400 mm working floor; ≥ 600 mm comfortable; confine below ~600 (vertical joint steel or RC jamb) | pier crushes under two lintel reactions before the wall fails in anything else |
| Sill panel (Brüstungsfeld) | carries no load — may be omitted without structural loss | loads bypass vertically via jambs over the lintel; but keep static depth between slab edge and lintel to redirect the forces around the hole |
| Storey-height openings (full-height glazing) | slab edge acts as lintel — provide local top reinforcement at the opening, and design the remaining piers/ring beam as a transfer system | in RC walls openings are free-form; in masonry a full-height cut splits the panel and halves the lever arm against tipping |
| Horizontal chases/slots (Schlitze) | only in walls t > 11.5 cm, within 400 mm of floor/ceiling lines (installation zones DIN 18015-3), milled not hammered, NOT in horizontally-perforated bricks, NOT in chimney walls, avoid bearing zones | a hammer-cut chase under a lintel end is a pre-made failure plane |
| Ring anchor (Ringanker) | required for > 2 storeys, building length > 18 m, large openings, unfavourable ground; spacing of supports ≲ 30× slab thickness | ties the box together; at head level it doubles as the continuous lintel band |
| Parapet/free wall end above a low roof | support the end of every lintel at a real bearing or a jamb vertical — a lintel ending in a 600 mm sliver is a cantilever nobody detailed | corner blow-out of thin piers is a classic veneer/masonry failure |

**The coordination discipline this enables:** fix the head level, fix the
Brüstung level, stack the jambs, and most lintel problems become small. Mix
the levels and every opening becomes an individual design with a discontinuous
band and five cracked junctions.

---

## Section 3: Lintel Types and Preliminary Sizing

### 3.1 Type selection

| Type | Typical span | How it works | When to use | Watch out |
|---|---|---|---|---|
| **Fertigteil-U-Sturz** (precast U-profile + site Füllbeton) | ≤ 2.4 m | U-shell is the formwork + bottom/side steel; fill C20/25 with continuous bed bar | default in brick/KS walls; supplier tables (e.g. 175/240 mm heights) govern | fill quality, marking top face, bearing on fresh mortar bed |
| **Flachsturz** (precast flat lintel) | ≤ 1.5 m | fully factory element, 115–150 deep | speed, thin walls | **orientation** — upside-down puts all steel in compression; paint-mark at casting |
| **Ortbeton-Sturz** (cast-in-situ) | any | designed beam in wall thickness | continuity with Ringanker/band, wide openings, curved walls | formwork + strike time slows the wall |
| **Rollschichtbogen / brick arch** (rolling course, Segment- oder Flachbogen) | ≤ 1.3 m (24 cm), ≤ 1.6 m (36.5 cm) segmental; jack/flat ≤ 0.9/1.3 m | compression arch in masonry plane; needs skewback + abutment | traditional façades, where you want no concrete in the wall | generates **horizontal thrust**; needs undisturbed piers (§4.4) |
| **Bewehrter Flachsturz aus Mauerwerk** (bed-joint reinforced: arch compression chord + Zugband, EN 845-2) | ≤ ~2.5 m | steel flat bar/tie under a small arch of bricks; the wall's own arch action carries itself | invisible lintel in facing brick | only with continuous bonded masonry above and valid arch action (§4.2); differential movement of steel cracks render |
| **Winkelstahl / flat-steel lintel** (Walzstahl, feuerverzinkt) | ≤ 3 m (veneer), designed beyond | angle carries outer leaf only; inner leaf self-supporting | **Vorsatzschale / brick veneer**, retrofit | corrosion = structural (§6.5), tray + weeps mandatory, deflection governs |
| **Stahlbeton-Fertigteilsturz / beam** | 2–4 m | engineered precast | large openings, industrial walls | bearings on elastomeric pads/Grout, transport |
| **Stahlträger (IPE/HEA) encased** | 2–6 m | retrofit or load-heavy headers | openings in existing walls, car ports | needs Auflager/Tragkonsole, Brandschutz (umbau or Spritzbrandschutz), Bauen-im-Bestand rules (§12.3) |
| **Room-height opening: slab edge as lintel** | full panel | local top steel at opening edge, forces redistribute through piers | full-height glazing in RC walls | engineer's transfer design, not a table |

### 3.2 Depth and section rules of thumb (take the larger)

- **Span ratio:** h ≈ l/12 (simply supported lintel) to l/15 (well restrained).
  Treat l/12 as working default; heavily loaded or masonry-cracking-sensitive
  cases go deeper for stiffness, not strength.
- **Field rule:** start at 150 mm and add ~25 mm depth per 300 mm clear span.
- **Course rule (masonry):** round depth up to whole courses so the head joint
  lands on a bed joint: 65/100/175/240 mm-ish per format (NF/DF/2DF) —
  [VERIFY exact grid for the chosen stone]; a lintel forcing the mason to cut
  courses above the head is a crack generator.
- **Width = full wall thickness.** A narrower lintel leaves an unsupported
  masonry lip that spalls (and leaks into the reveal).

### 3.3 Preliminary lintel schedule (240 mm wall, C20/25, B500A/B, arch action valid)

> **Table status:** paraphrased working values for pre-sizing and FreeCAD
> modelling — not a transcription of any EN 845 / DIN 105 table. Manufacturer
> Fertigteil tables (Sturztabellen) govern real precast selection. **[VERIFY]**

| Clear span l | Section b×h | Bottom steel | Top steel | Links | Bearing each side |
|---|---|---|---|---|---|
| ≤ 0.9 m | 240 × 115 | 2 Ø8 | — | — (Ø6/200 if cast in situ) | 150 mm |
| 0.9–1.5 m | 240 × 150–175 | 2 Ø10 | 2 Ø8 (nominal) | Ø6 @ 200 | 150–200 mm |
| 1.5–2.1 m | 240 × 175–200 | 2–3 Ø12 | 2 Ø10 | Ø8 @ 150 | 200 mm |
| 2.1–2.5 m | 240 × 200–240 | 3 Ø12 | 2 Ø12 | Ø8 @ 150 | 240 mm |
| 2.5–3.0 m | 240 × 240–300 | 3–4 Ø16 | 2 Ø12 | Ø8 @ 125 | 240–300 mm + jamb verticals |
| > 3.0 m | **designed beam**, columns/piers each side | | | | §10 lateral check |

For 11.5 cm single-leaf interior walls: halve width, keep depth, 2 Ø8 up to
1.2 m; do not open a 11.5 cm load path wider than ~1.2 m.

Minimum flexural steel (EC2, SI units, d in mm, fctm in MPa):
`As,min = max(0.26·fctm/fyk · b·d ; 0.0005·b·d)` — C20/25 (fctm 2.2), B500:
first term governs. **[VERIFY current §7.3.2 values].** House-scale lintels
with valid arch action are **minimum-steel-governed**: the real design
decisions are depth (deflection), bearing (crushing) and anchorage (§7), not
bar area.

### 3.4 Worked example A — what a 1.5 m lintel actually carries (arching action)

Given: clear span l = 1.5 m; 240 mm HLz wall (γ ≈ 14 kN/m³ masonry incl.
joints, gross — [VERIFY unit weight of the chosen stone]); 2.6 m continuous
bonded masonry above head; no slab/beam in the wedge.

```
Arch height needed    0.866·1.5 = 1.30 m   <  2.60 m available  → full wedge forms ✔
Wedge load            W = 0.5·l·0.866l·t·γ = 0.433·1.5²·0.24·14 = 3.27 kN
Equivalent UDL        w_tri = 0.433·l·t·γ  = 1.26 kN/m
Lintel self weight    0.24·0.20·25         = 1.20 kN/m
Plaster (both faces)  ~0.4 kPa·wedge area/l≈ 0.30 kN/m
--------------------------------------------------------------
Characteristic      g_k ≈ 2.8 kN/m (dead only)
Design              w_Ed = 1.35·2.8 = 3.8 kN/m  (G leading, no live on lintel)
M_Ed = w·l²/8 = 3.8·2.25/8 = 1.07 kN·m ;  V_Ed = w·l/2 = 2.8 kN
As,req ≈ M/(0.9·d·fyd) = 1.07e6/(0.9·165·435) = 17 mm²  → As,min governs:
As,min = 0.26·2.2/500·240·165 = 45 mm² → 2 Ø8 = 101 mm² ✔
```

If you had (wrongly) taken the full 2.6 m wall strip: w = 2.6·0.24·14 =
8.7 kN/m — **~3× the real load**. If instead a slab bears 0.65 m above the
head, §4.2 voids the arch and the same opening wants a designed beam.
**Always ask what is above.**

---

## Section 4: What the Lintel Actually Carries — Arching Action (Bogenwirkung)

### 4.1 The relief wedge

Bonded masonry above an opening self-corbels: load arches around the opening
into the jambs and only a triangular wedge of wall actually reaches the
lintel. The flat-lintel model of EN 845-2 is exactly this: the lintel is the
**compression chord of a masonry arch + a tie**, and only the equilateral
triangle above the opening (base = opening width, apex up, height 0.866·l)
needs to be carried. **[VERIFY wedge angle convention — some German tables use
45°/height l/2; state which you used.]**

```
        wall above (arches around, does NOT load the lintel)
   ────────────────────────────────────────────────
                       /\
                      /  \      relief wedge
                     /    \     base = l, height 0.866·l
            0.866l /      \
                   /________\
   ═══════════[  lintel  ]═══════════════
   masonry    |          |    masonry
   pier       | OPENING  |    pier
```

- `W_wedge = 0.433·l²·t·γ` ; equivalent `w = W/l = 0.433·l·t·γ` (kN/m).
- Masonry unit weights (gross, indicative, **[VERIFY]** datasheet of chosen
  stone): HLz 12–14 · KS 16–18 · Vollziegel 16–20 · Porenbeton 4–6 ·
  Leichtbeton 8–14 · Normalbeton-Block 22–24 kN/m³; + plaster 12.5 mm/gypsum
  ≈ 0.25–0.3 kPa per face.

### 4.2 The four conditions that VOID arch action

Arching is a gift, not a right. Design for the **full wall strip** (no wedge)
whenever any of these is true:

1. **Not enough wall above.** Continuous bonded masonry above head
   < 0.866·l → take the truncated trapezoid actually present plus anything
   sitting on it.
2. **A point load lands inside the wedge.** Beam bearing, joist, column,
   tank leg, truss shoe → arch cannot form → full reaction plus wall.
3. **A slab/floor bears within 0.866·l above the head.** Very common with
   windows at ~2.3 m head under a slab at 2.5–2.9 m.
4. **The masonry above is not continuous/bonded.** Movement joint, second
   opening, chase, flue within the wedge; two windows stacked with < ~600 mm
   between sill and head → no arch.

Also void it over **green masonry**: arch action needs cured mortar — do not
load a fresh lintel; max ~1 m of wall height above a lintel cast/placed that
day, ≥ 24 h before any loading. Practical ceiling: **treat arch action as
usable for l ≤ ~3 m** in ordinary house walls; beyond that, and in any wall
with more than one storey of openings above, design the beam for real loads.

### 4.3 Partial/edge bearing on the piers

Arch action redirects load into the jambs — which is why **jamb bearing
pressures concentrate exactly where the pier is narrowest**. The pier
under a lintel end must pass §5's Teillast check; a < 400 mm pier under a
2.5 m lintel is a crush mechanism waiting, and the fix is a concrete jamb
(Konstruktionsstütze) or a wider Auflager, not a bigger bar.

### 4.4 Brick arches as their own lintel

Rules collected from EN 845-2 practice and traditional Mauerwerksbau
(all **[VERIFY]** before building one):

| Parameter | Rule |
|---|---|
| Max spans (rule-of-thumb tier) | 24 cm wall: Flach-/Rollschichtbogen ≤ 0.9 m, segmental ≤ 1.3 m; 36.5 cm wall: ≤ 1.3 / ≤ 1.6 m; true arched openings: 24 cm ≤ 2.0 m, 36.5 cm 2.0–5.5 m, > 36.5 cm 3.5–8.5 m — beyond the tier: engineered |
| Wedge joints | 5–20 mm, radial — every joint line extended passes through the arch centre; non-radial joints slide |
| Voussoir count | odd number + crown keystone (setting convenience) |
| Skewback (Anfangsfuge) | inclined springing joint whose line aims at the arch centre — segmental/jack arches need it |
| Extrados | tangent to a bed joint at the crown (the arch must run into level coursing) |
| Camber (Überhöhung) | printed digests: jack arch ≈ 1/50, flat arch ≈ 1/12 of opening — **[VERIFY: these read as very large; confirm against EN 845-2 / Fachbuch before setting out; a flat arch without camber will look sagged even when sound]** |
| Abutment | undisturbed full-height pier resisting the thrust; H ≈ w·l²/(8·f) — flatter arch, harder push |
| Wall above springing | keep loaded and continuous; the vertical surcharge stabilises the arch |
| Centring (Lehrgerüst) | strike ≥ 7 days (14 for > 1.2 m/cold); ease gradually (wedges/sand jacks), build symmetrically from both springings |

Thrust sanity table (uniform w on the arch): `H = w·l²/(8f)`.

| Rise/span f/l | 0.50 (semicircular) | 0.25 (segmental) | 0.15 | 0.05 (near-flat) |
|---|---|---|---|---|
| H/w·l (per unit load) | 0.25·l | 0.50·l | 0.83·l | 2.5·l |

Failure mode: **three-hinge mechanism** — joints open at crown + both
springers when the thrust line escapes the middle third (too flat, spandrel
unloaded, abutment yielded, point load in the arch). Do not use an arch where
the abutment will later be opened, where the foundation may spread a few mm,
or where earthquake sensitivity matters without engineering. The safe
compromise for arched *appearance*: **concrete lintel at true head +
non-load-bearing arch skin tied back**, labelled as such on the drawing.

---

## Section 5: Bearing, Edge Distance and Partial Load (Teillast)

### 5.1 Bearing length rules

```
Bearing a ≥ greatest of:  150 mm  |  lintel depth h  |  clear span l / 12
```
Working rule for lintels/beams landing on a masonry pier **[VERIFY — product
standard EN 845-1/-2 and supplier tables set the floor for precast; German
practice commonly quotes ≥ 100–150 mm for small lintels and h for
Sturztiefen]**. Then measure it from the **face of the opening** and check
the *pier*, not just the number:

- total lintel length = l + 2·a — a 1.5 m window with 2×200 mm bearings wants
  a 1.90 m element;
- bear on **whole, solid, well-bonded units in a fresh full mortar bed** —
  never on a cut brick, never on an unfilled shell, never on plaster;
- at least 2 courses of sound masonry under the end, not the top course of a
  freshly built pier;
- at a RC jamb/column the bearing-length rule no longer governs — the checks
  become bar anchorage into the joint and the joint itself
  (`concrete-detailing`, `structural-analysis`); don't carry an masonry
  bearing number into a frame connection.

### 5.2 Partial-bearing check per EN 1996-1-1 §6.2.3

The bearing stress that actually crushes masonry is a **concentrated load
spread over a loaded area Ab inside a larger effective area Aef**:

```
σmax = N_Ed / Ab ≤ f_d · β ;   β = 1 + 0.1·(Aef/Ab − 1) ≤ 1.25
conditions: centric (e0 < t/6) and Ab/Aef ≤ 0.45
Aef: loaded width spread by the load-distribution angle through the wall
     (digest prints l_ef = l1 + 2·h_c·cot60°, i.e. 30° off vertical per side,
     capped by the wall panel)  [VERIFY current EN 1996-1-1 §6.2.3 figure/form]
```

### 5.3 Worked example B — lintel end on a 15 cm wall (from a digested calculation)

Given: PP4-0.55/DM (thin-joint) wall t = 150 mm; lintel end length
l1 = 200 mm across the wall; centered reaction N_Ed = 19 kN; wall height
above the loaded zone h_c = 2.0 m; fd = 1.7 MPa (fd = 0.85·fk/γM with ζ
long-term factor).

```
Ab   = l1·t = 20·15 = 300 cm²
l_ef = l1 + 2·(h_c/2)·cot60° = 0.20 + 1.0·0.577 = 0.78 m
       (spread to mid-height above the load, 30° off vertical — reproduce the
       standard's own distribution figure before use)  [VERIFY]
Aef  = 0.78·0.15 = 0.117 m²
Ab/Aef = 300/1170 = 0.26 ≤ 0.45 ✔ ;  e0 = 0 < t/6 ✔
β = 1 + 0.1·(Aef/Ab − 1) = 1 + 0.1·2.9 = 1.29 → cap 1.25; source example used
    β ≈ 1.0 (conservative)
N_Rd = β·Ab·fd ≥ 1.0·300·1.7 = 51.0 kN  >  N_Ed = 19 kN ✔
```

If it fails: **lengthen the bearing** (deeper lintel end / wider Auflager),
add a **betonerte Auflagerbank / padstone** (RC block or two courses of
solid engineering units in strong mortar), or turn the jamb into a tied RC
edge member. Note the shape of the result: the reaction is small, the loaded
area controls — crushing is a *geometry* failure, which is why bearings,
bars and arch depth are the lintel design conversation, in that order.

---

## Section 6: Stiffness, Camber, Anchorage and Steel Lintels

### 6.1 Deflection — this, not strength, usually governs

| What the lintel supports | Limit | Basis |
|---|---|---|
| Roof/floor, nothing brittle above | l/200 – l/300 | EC2/EN 1995 practice **[VERIFY]** |
| Plastered masonry wall (house default) | **l/360** | serviceability |
| Masonry above the lintel (arch zone, facing brick) | **l/600** and often an absolute cap ≈ 3 mm | cracking sensitivity — CMHA/EN 845 practice **[VERIFY]** |
| Steel angle under veneer | l/600 and ≤ ~7.6 mm | veneer tables **[VERIFY]** |
| Head of a glazed unit / curtain wall head | l/360 and ≤ 6 mm | glazing practice |

A masonry-supporting lintel at l/600 needs roughly **twice the stiffness** of
one sized to l/300 — which is why a "strength-adequate" 175 mm lintel over a
2.4 m opening still cracks the wall above. Serviceability screen for RC
lintels: keep **l/d ≤ ~20** (simply supported, B500, lightly stressed) —
240×200 over 1.5 m → 1500/165 ≈ 9, comfortable; over 2.4 m → 14.5, marginal;
go deeper, not more steel.

### 6.2 Camber and pre-set

Concrete lintels: no camber needed at house spans; a *sagging* lintel under
load is a deflection problem (§6.1), not a steel problem. Brick flat arches:
camber per §4.4. Steel angles over veneer: pre-camber ~l/300 up so the
finished line reads straight after creep of the masonry shelf **[VERIFY
practice value]**.

### 6.3 Header-to-wall connections (the lintel's own restraints)

- **Anchorage past the opening face:** bottom bars extend ≥ development length
  into the pier — for B500 in C20/25, lb ≈ 40–50·Ø (Ø12 → ~500–600 mm;
  Ø16 → ~800 mm; compute per `concrete-detailing`, do not guess). Where the
  bearing is short of lb: 90° standard hook into the pier or lap the bars
  into the jamb vertical/Ringanker cage. **Never cut a bar to fit the
  bearing** — a cut bar at the lintel end is a hinge.
- **Continuous band:** at the chosen head level join lintels into the
  Ringanker/umlaufendes Band (min 4Ø12 + Ø6/200 typical [VERIFY against NA
  practice]); laps ≥ 50·Ø around corners; a band that stops at a door is
  decoration.
- **U-Sturz fill:** Füllbeton ≥ C20/25 vibrated, continuous bed bar in the
  fill for spans > ~2 m, cover to the precast shell respected.
- **Jamb verticals:** openings > ~1.5 m, piers < 600 mm, failed bearing check
  or seismic/confined design intent → vertical steel in the jamb from plinth
  to band, grouted cavity or RC edge column; ties Ø6–8/200, Ø8/150 near band
  junctions **[VERIFY]**.
- **Precast bearing at RC columns/frame:** pinned, form-fit: elastomeric pad
  or mortar bed + dowel; the joint is then designed as beam-column, not
  bearing.

### 6.4 Steel angles and Zweischale (veneer) lintels

For a brick outer leaf (Vormauerschale) over an opening:

- Indicative sizes (leaf height ~2.4 m above, **[VERIFY — engineered selection
  depends on leaf height, whether a floor bears, and the l/600 cap]**):
  ≤ 1.5 m L 90×90×8; 1.5–2.0 m L 100×90×8 (long leg vertical) or flat bar +
  angle; 2.0–3.0 m L 150×90×8 / flat steel; > 3 m designed.
- Bearing ≥ 100 mm each end (150–200 preferred) **on the backup leaf or a
  padstone** — never on the veneer.
- **Galvanize (fire-dip galvanised, EN ISO 1461) or duplex-coat**: rust
  expands ~6× parent volume — *rust jacking* lifts the course above the angle
  and cracks the wall. This is the dominant long-term steel-lintel failure.
- Thermal movement: steel moves ~5× masonry — a single angle longer than ~6 m
  without a movement break cracks the render around the opening; leave a soft
  joint at one end.
- **The angle is a water shelf.** Cavity tray (Dichtungsband/Tränke) above it
  stepped into the cavity with upstands ≥ ~100 mm at jambs (end dams), weeps
  (Fugen mit Lotschlitzen / open head joints) in the first course above the
  tray, spacing ≤ ~600–900 mm, at every end dam. Without the tray: a permanent
  damp patch above the window — the most common cavity-wall complaint.
- Fire: encased or protected if the element needs a class
  (`fire-protection-building`).

### 6.5 Bed-joint-reinforced lintels (Lagerfugenbewehrung)

Stepped-course lintels (Mauerbogen mit Zugband) and bed-joint ladder/wall-tie
meshes act through the arch model of §4.1 — **valid only where arch action is
valid** (§4.2), never under a point load or on green masonry. The same
bed-joint steel is the correct anti-crack remedy at stress concentrations:
2 courses × 2–3 ladder bars, ≥ 500–600 mm past each jamb, under low sills
and over wide openings, where a diagonal sill-corner crack is being prevented
rather than repaired. Product standard: EN 845-2/-3 for masonry lintels and
bed-joint reinforcement **[VERIFY exact part/edition]**.

---

## Section 7: Window Build-Up and Thermal Performance (DIN EN ISO 10077)

### 7.1 Frames: materials and typical U_f

| Frame | Construction | U_f [W/(m²K)] | Notes |
|---|---|---|---|
| Wood / wood-alu | solid 68–92 mm | 1.4–1.8 | natural hygroscopic movement; alu shell = maintenance-free face |
| PVC | 2-chamber | 2.3–2.8 | budget retrofit |
| PVC | 3-chamber | 1.7–2.2 | standard |
| PVC | 4-chamber | 1.4–1.6 | + steel or foam core |
| PVC | 5-chamber | 1.2–1.3 | |
| PVC | 7-chamber | 0.95–1.1 | Passivhaus-adjacent |
| Alu, thermally broken | polyamide bridge ~30–50 mm | 2.8–3.5 | break is structural *and* thermal — specify it |
| Alu, optimised | multi-chamber break | 1.4–1.5 | |
| Passivhaus frame | foam-filled / composite | 0.7–0.8 | certified components (phi-class) |

**[VERIFY band — typical values from the tabulated digest grid.]** Steel
frames sit at the Alu-without-break end: worst common frames, only with a
dedicated thermal break. A frame *without* break (bare Alu) can exceed
U_f 6–7 and drags Uw above 2.5 even with triple glazing (table §7.3).

### 7.2 Glazing: Ug, g, τ

| Build-up | Ug [W/(m²K)] | g_glass (total) | τ_L |
|---|---|---|---|
| Single (historical) | 5.8 | ~0.85 | ~0.85 |
| Old double IG, air, no coat | 2.7–3.0 | ~0.75 | |
| Double IG low-e, air | 1.1 | ~0.65–0.70 | |
| Double IG low-e, Ar | 1.0 | ~0.60–0.65 | |
| Triple IG low-e, Ar | 0.6–0.7 | ~0.50 | |
| Triple low-e, Kr / warm-edge best | 0.5 | ~0.45–0.55 | |

- GEG reference window: **Uw 1.3 with g 0.60** (residential); roof windows
  1.4; non-residential 1.3/1.9 with τ 0.78; domes/Lichtbänder 2.7 (g 0.64)
  **[VERIFY current GEG text — amendments 2024+ shift the reference building]**.
- Existing-building retrofit (GEG §47 ff., exchanged windows): **Uw ≤ 1.3**;
  glazing-only exchange in box/old frames: **Ug ≤ 1.1** (low-e ε ≤ 0.2);
  lift-slide doors 1.6; special glazing (R'w ≥ 40 dB, bullet, fire ≥ 18 mm):
  window 2.0 / glazing-only 1.6 **[VERIFY current table]**.
- g = solar energy transmittance of the whole window ≈ g_glass·F_frame(≈0.7?
  — GEG uses F_F = 0.7 frame reduction for gains; state which convention)
  · F_s shading · F_C blind.

### 7.3 Uw combination and spacer correction (ψ_g)

```
U_w = (A_g·U_g + A_f·U_f + l_g·Ψ_g) / (A_g + A_f)            [DIN EN ISO 10077-1]

A_g  visible-glazing area      A_f  frame area
l_g  visible edge length glazing/frame   Ψ_g  linear spacer transmittance
```

With glazing bars (Sprossen) inside the cavity add `+ l_gb·Ψ_gb`; with an
integral panel add `+ A_p·U_p + l_p·Ψ_p`. Typical Ψ_g pairs (typical /
improved warm-edge spacer), **[VERIFY against the current 10077-1 annex — the
digest grid pairs are partially garbled for metal spacers]**:

| Spacer | Ψ_g typical [W/(m·K)] | warm-edge |
|---|---|---|
| wood / PVC (thermoplastic) | 0.06 | 0.05 |
| coated plastic composite | 0.08 | 0.06 |
| Alu in broken frame | 0.08–0.11 | 0.06–0.08 |
| bare Alu (no break) | legacy values ≥ ~0.30 — table lost | — |

Warm-edge spacers lower whole-window Uw by roughly **0.1–0.2 W/(m²K)** at
low frame U — and are the cheapest Uw improvement on any triple-glazed job.
Frame fraction matters as much as components: the tabulated grids come in
**30 % and 20 % frame-ratio** versions; a slim 20 %-frame window is ~0.1
better than the same glass in a 30 % frame.

**Tabulated Uw anchors** (frame ratio 30 %, typical spacers) — read from the
reference Uw grid, cells partially degraded **[VERIFY]**:

| Ug ↓ / Uf → | 0.8 | 1.0 | 1.2 | 1.4 | 1.8 | 2.6 | 3.0 | 7.0 |
|---|---|---|---|---|---|---|---|---|
| 5.8 (single) | | 4.3 | | | | | | 6.1? |
| 2.7 | | | | 2.9 | | | | |
| 1.1 | | | ~1.3? | 1.5 | | | 3.1? | |
| 1.0 | | 1.9 | 1.3 (1.2 col) | | | | | |
| 0.7 | 0.9 | | | | | | | |
| 0.5 | | 0.79 | | 1.0 | | | | 2.6 |

Use the formula, not the grid, for real numbers; the grid is for plausibility
checks. Worked build-up in §14-C.

- **Mullion/transom correction (per DIN EN ISO 10077 / reference grid):** glazing bars *in the pane
  plane* (Sprossen) raise Uw via Ψ_gb; the tabulated ΔU grid was not
  recoverable from the digest — compute with 10077-1's Ψ_gb values or the
  manufacturer's system Uw **[VERIFY]**.
- **Box windows (Kastenfenster):** `1/U_w = 1/U_w1 + 1/U_w2 − (1/R_si + R_s +
  1/R_se)` with R_si 0.13 / R_se 0.04 and cavity resistance R_s by gap width
  and emissivity (9 mm clear: ~0.30; ε 0.2 low-e faces: ~0.21; 12 mm:
  ~0.38/0.25) **[VERIFY grid]**. Retrofit logic: an old box window with new
  inner leaf can beat a bad mono window.
- **Combined windows** (two leaves sharing reveals): same reciprocal formula
  with the two Ug terms.
- **Roof windows:** same combination plus additional frame/water-flash area;
  reference Uw 1.4.

### 7.4 Air, rain, wind — window performance classes

| Standard | What it rates | Residential reference |
|---|---|---|
| DIN EN 12207 | air permeability of the *functional joints* | class 2 at ≤ 2 storeys, class 3 above; with durable replaceable soft perimeter seal → class 3 reachable for any proper window; wooden windows without seal ≥ class 2 |
| DIN EN 12208 | rain/watertightness of the joint build-up | class per exposure (driving-rain group I/II/III — wind-driven-rain map; exposed sites ≥ class E750/E900 practice **[VERIFY]**); "Regen dicht vs Auslauf" — first stage may admit water, second stage must not |
| DIN EN 12210 | wind load resistance | design wind pressure from wind zone/terrain/height (`building-physics-thermal-moisture` wind section) |
| Component test | EN 1027 series; joint air-flow limit ≤ 0.1 m³/(h·m·Pa^2/3) for envelope joints | building-level check: blower-door n50 ≤ 1.5 h⁻¹ (no mechanical vent) / ≤ 3 (with) **[VERIFY current GEG/EnEV-era wording]** |

**Never model mounting foam as the air seal** (§8). Blower-door failures
concentrate at window perimeters more than anywhere else in the envelope.

### 7.5 Roller shutters, boxes and external blinds (Rollladen, Klappladen)

- Closed external shutter adds resistance ΔR per withdrawn 10077-1 Annex G
  values (airtight shutter ~0.95·R_sh + 0.17 m²K/W down to very permeable
  0.08) — **[VERIFY: annex withdrawn; do not credit in the design U-value;
  use it only as a qualitative argument]**.
- **The box is the problem, not the shutter.** Box must meet DIN 4108-2:
  as a component R ≥ 1.0 (light construction ≥ ~0.55 at lid — [VERIFY grid]);
  the *junction* must satisfy the Roka model: U_sb ≤ 0.85 W/(m²K) at the
  box/reveal connection and f_Rsi ≥ 0.70 (mould criterion) at the head.
  Prefer **integrated-in-wall insulated boxes (e.g. PB/EPS-shelled)** or
  window-attached boxes ahead of the lintel line; a bare PP box in a cold
  reveal is the classic black-streak ceiling failure.
- Shading design: F_s external roller-shutter/louvre closed ≈ 0.30–0.35,
  canopy 0.50–0.55, internal light blind 0.70–0.80 **[VERIFY]** — this feeds
  the summer overheat check (a_W ratio limits: vertical façades ~10–15 % by
  orientation without proof; more glazing requires F_s·g analysis or dynamic
  simulation, Übertemperatur-gradstunden 1200 K·h residential **[VERIFY
  current GEG/DIN values]**).

---

## Section 8: The Mounting Joint — Multi-Stage Sealing (Dichtungsstufen / Three-Joint Rule)

### 8.1 The principle

The window-to-wall joint is **the worst trade interface in the building**:
one continuous air/water/thermal line must be transferred element-to-element
across four different materials with four different movements. German
practice resolves it in **stages (Stufigkeit)** — the logic behind the
"three-joint rule" (Drei-Ebenen-Anschluss; RAL-GZ 996 mount guideline is the
common quality-assurance anchor):

```
 outside                                    inside
 ────▶ weather                            rain ◀────
┌──────────┬─────────────────────┬───────────────┐
│ OUTER    │ MIDDLE              │ INNER         │
│ schlag-  │ Dämmzone,           │ raumluft-     │
│ regen-   │ diffusionsoffen     │ seitig        │
│ fertig,  │ winddicht           │ LUFTDICHT +   │
│ diffusionsoffen ("atmet aus")  │ dampfdicht    │
│ bremst   │ (Foamband/MinWolle/ │ (Band/bahn    │
│ das Wasser│ Dichtstoff)        │  anschließen) │
└──────────┴─────────────────────┴───────────────┘
   Bremsen → Abführen → Dichten      airtightness line continues IN ONE PLANE
```

- **Outer stage = brake + drain:** rain that passes the first line must be
  caught by the sill drip/frame rebate and *evacuated outward* — so the outer
  joint must be vapour-open. A narrow-deep open joint is a *good* rain brake
  (long path, pressure-equalising, vapour-out) — the classic "open joint"
  design in ventilated claddings; never let differential movement squeeze it
  to capillary width.
- **Middle stage = the insulation, kept dry and draught-free.**
- **Inner stage = the only airtight line** — continuous with the wall's
  Luftdichungsebene (tape welded/collared to the Dampfbremse, or sealed to
  plaster/concrete). Multi-stage outside, **single-stage airtight inside**.
- Layer order and the sealing chain through the frame: *sill drip → reveal cap
  → frame rebate gasket → compression tape → interior airtight tape*. Each
  interface transfers each function; every interface joint gets sealed.

### 8.2 Joint design rules that make or break it

| Rule | Value / form | Why |
|---|---|---|
| Sealant joint geometry | depth ≈ 1/4–1/3 of width; **two-flank adhesion only** — backer rod (Hinterfüllschnur) blocks the third face | three-sided adhesion tears the sealant at the base on movement |
| Movement | joint width = expected movement + tolerance; sealant strain over life (UV, ozone, cycles) → maintainable > buried | chronic cause of torn seals: differential movement masonry vs frame |
| Compression gaskets | pre-compressed foam band needs **residual compression** over life; set at the manufacturer's installation width window | spring force, not adhesion, is the seal |
| Montageschaum (PU foam) | **air-bridging filler only — never the airtight layer** | it is permeable and shrinks; leave it covered by tape/mortar seal |
| Surface prep | smooth render/putty (Dichtspachtel) **before** frame fixing on masonry reveals; dust-free, primed per sealant maker | porous render = no adhesion |
| Capillary protection | hydrophobic lip treatment kills suction in narrow joints only; slope horizontal joints outward; sharp arris = tear-off edge (Tropfkante/Abreißkante) | gravity + breakage of the water film do the weather sealing |
| Airtightness of connections | overlaps/tapes strained-free; penetrations via moulded collars; tape needs continuous backing (batten/flange), not air | convection carries far more water than diffusion |

### 8.3 Gap, fixing and installation rules

- **Montagefüge (installation gap):** planned tolerance zone, not an accident.
  Typical 10–30 mm perimeter in masonry practice (frame sits on setting
  blocks/shims at bearing points, not in the gap seal) **[VERIFY system
  maker's range — the window profile system defines it]**; plan **minus
  dimensions** (Mindermaß) so the opening is never too small; window and
  reveal live in coordination spaces (12.5 cm brick grid / 1 M = 100 mm) so
  the gap stays achievable.
- **Fixing:** frame fastened with anchors/lugs **per the system approval**
  (Verankerungsnachweis des Systems): typical grid ≤ 600 mm centres, ~150 mm
  from each corner, into solid masonry/lintel — never only into the head
  soffit without jamb fixings working with it, never through the seal/DPC
  layers of a cavity tray. Screws in hollow units need perforated-brick
  anchors or chemical/resin anchors sized for the edge distance — the anchor
  class must match the masonry class (see failure #10).
- **Bearings:** glazed units sit on setting blocks at quarter points;
  frame-to-masonry gap behind the sealant line filled with non-shrink
  mortar/grout or sealed backing, never left as an open cold slot.
- **Head detail:** lintel + DPC/tray above it (§6.4) + continuous reveal
  insulation across the head; a bare concrete head inside the reveal is the
  coldest surface in the room → mould streaks. Keep the Dämmebene in **one
  plane** across the junction: frame-insulation + reveal-insulation overlap
  into the wall insulation (no stepped cold path); positive corners get extra
  corner insulation. Target ψ_j for the reveal ≤ 0.01–0.05 W/(m·K) per
  detailed example (DIN 4108 Bbl 2 window-reveal examples) **[VERIFY]**.
- **Jamb verticality** matters: out-of-plumb reveals mean packed fixings,
  moved shims and torn seals — check reveal square/level *before* frame-in.

### 8.4 Sill detail (Fensterbank) — where water actually wins

| Parameter | Value |
|---|---|
| External sill slope | **≥ 2 % weathering minimum; practice 5–10 % (1:20–1:10)**; water must leave, always |
| Projection | ≥ 30–50 mm clear of the wall face, with under-edge **drip groove/arris ≥ 10 mm setback ~20 mm** (Tropfkante) |
| End dams (DPC turn-up at jambs) | ≥ 100–150 mm up each jamb — stops sideways run into the reveal |
| Sill DPC / tray | continuous under the sill course, lapped into the reveal seals and the frame's rain-flange (Aufstands-/Regenleiste) — the flange must sit **on** the drained plane, seal above it |
| Inner sill | overlaps the airtight layer, no gap left open at the frame foot |
| Weep/escape at the sill outer seal | first stage may wet; second stage drains out — never a sealed-in water pocket |

**Why sills crack:** the two lower opening corners are stress concentrations;
under any settlement/thermal movement a ~45° diagonal starts there. Ordered
fixes: continuous sill band / bed-joint reinforcement (§6.5) through the
pier > loose lintel-only solutions. **[VERIFY sill-band trigger against the
chosen system.]**

---

## Section 9: Doors

### 9.1 Thermal

- Solid leaf typical U_D (DIN 4108-4): **wood/wood-based/plastic 2.9,
  metal frame+cladding 4.0** W/(m²K) **[VERIFY current edition]**; GEG
  reference **U_D ≤ 1.8** (new and existing exchange) → thermally broken
  frame + insulated leaf/low-e glazing area needed to show 1.0–1.3.
- Fully glazed door: `U_D = (A_g·U_g + A_f·U_f + l_g·Ψ_g)/(A_g + A_f)` —
  same machinery as windows; glazed+panel adds `A_p·U_p + l_p·Ψ_p`
  (Ψ_p = 0 if both panel faces λ < 0.5 and edge fill λ < 0.5).
- Tabulated door/gate grids exist in the reference tables for Uf×Ug combos — cells
  not recoverable from the digest; compute per formula **[VERIFY]**.
- Lift-slide (Hebe-Schiebe) reference limit 1.6; threshold is *the* weak
  point: use a thermally broken Schwelle or drop to zero-step
  (Nullschwelle) build-ups — zero-step and Uw fight; the certified system
  decides (cross-ref accessibility skill for the threshold/ramp rules).

### 9.2 Acoustic

- Door+wall is a **combination element**: the rated requirement for
  "Wand mit Tür" comes out *lower* than the wall-only value because the door
  dominates (§14-D logic; DIN 4109-1 Tab 2/3 stairwell-wall-with-door rows,
  corridor→room). Catalogue R_w,p of doors: from ~27 dB (plain) to 42+ dB
  (absorber-lined, double-sealed rebate, bottom drop-seal); use the C/Ctr
  triplet per noise type (traffic → Ctr).
- Details that decide it: perimeter seal continuous (drop bar at the floor
  gap), no unsealed cylinder/letterbox, frame bedded not foamed-open,
  gaps around the frame re-sealed to the same R as the leaf. A 42 dB door in
  a 38 dB wall wastes 4 dB and buys nothing — match elements, don't stack
  certificates. **[VERIFY per-door catalogue.]**

### 9.3 Fire and escape

- T30/T40/T90 doors (DIN 4102-5 / DIN EN 16034, EN 13501-2 classes E/Sa/C5
  etc.): self-closing + closer mandatory where they close escape routes;
  smoke-tight (S) variant; **all penetrations and the frame surround must
  hold the class** — door skill: `fire-protection-building`.
- Escape widths (Rettungswege: lichte Durchgangsbreite, necessary stair
  width, door widths in GKL, max travel distances) belong to
  `fire-protection-building` §escape and `accessibility-universal-design`
  — do not size an escape door from this file; carry its Rw/Uw/Ifc class
  through from the door table.

---

## Section 10: Openings and the Lateral System

A large opening does not just need a beam — it deletes a length of bracing
wall (Scheibe). In DACH low-to-moderate seismicity the wind case usually
governs, but the geometry logic is identical to the earthquake case, and in
zones with Erdbebenzone 2–3 (DE) / alpine regions (AT/CH) it governs hard.

- **What is lost:** full-height pier segments shrink; force must travel
  *around* the hole through the lintel zone and sill strip; the opening
  corners are the crack initiators (stair-step diagonal from the corner =
  the visible symptom of a pier that gave out).
- **Quick screen per wall line, per direction:**
  Σ opening widths / wall length ≤ ~0.5 as a working coordination limit
  (§1.2 Q3); piers ≥ 1/3 clear height and ≥ ~1.0 m to count as shear
  segments (masonry pier h/l ≤ ~2 preferred, ≤ 3 absolute before it flexes
  instead of shearing) **[VERIFY — coordination values; design per
  `masonry-construction` / `structural-analysis`]**.
- **Recompute wall density (Wanddichte) after every opening change**, both
  directions, every storey: widening a 1.5 m window to 2.4 m in a 4.5 m wall
  takes the remaining pier from 3.0 to 2.1 m and can drop the line out of
  the count entirely.
- **Compensation ladder** (cheapest first):
  1. Move the opening: off corners, toward mid-wall; split one 3.6 m opening
     into two 1.5 m with a 600+ mm pier.
  2. Add bracing length on the SAME line (longer return wall, close a small
     window). Capacity in the other direction does not help.
  3. Confine the remaining piers (RC jamb columns, ring anchor through).
  4. Make the opening bay a moment frame / load-bearing window element
     (Tragender Fensterstock) with designed connections — the engineered way
     to keep the glass.
  5. Dedicated lateral element elsewhere (RC core/wall, steel brace).
  6. If none closes: the opening is too big for the system. Change the
     system for that bay (RC frame), not the detail around the hole.
- **The short-column trap** (RC frames + infill): a partial-height infill
  under a ribbon window braces the column over part of its height — the
  unbraced length becomes a brittle short column. Either full-height panel
  with a soft joint, or isolate the sill panel (25–40 mm compressible joint
  at the column), or design the column for it (close ties). Flag explicitly
  to the engineer.
- **Wall of glass:** a fully glazed wall line contributes zero bracing — the
  diaphragm must reach the other lines, and torsion shifts the centre of
  rigidity. Practical fix that preserves the view: two slim RC/steel columns
  dividing the glazing into bays = a moment frame that reads as a mullion
  pattern. Decide this at sketch stage.

---

## Section 11: Openings in Timber and Steel Walls

### 11.1 Timber (Holzrahmenbau, Tafelbau, Brettsperrholz)

- **Stud frame:** cut studs land on a header (doubled top/lintel board or
  built-up header) and **jambs get doubled/king studs** — force concentration
  at the jamb scales with opening width. Headers bear on solid continuous
  framing to the foundation, never on a cavity. Where the header is
  load-bearing in the diaphragm line, treat it as a designed member
  (`timber-steel-design`): notched-end rules (k_v) and transverse-tension
  reinforcement at re-entrant corners of cut-outs.
- **CLT (Brettsperrholz):** openings are sawn panel-wise — masonry stacking
  rules dissolve — but corners of rectangular cut-outs are stress
  concentrations: provide corner reinforcement (screw/panel connectors or
  CFRP/grid at the corner, per ETAG/ETA systems) and keep edge distances
  from panel edges; window heads in multi-storey CLT need a **settlement gap
  (Setzungsfuge)** — timber shrinks across the grain, a rigid head detail
  cracks the panel or the frame.
- **Log/block construction (Blockbau):** transverse shrinkage eats storey
  height — every door/window head needs a compressible settlement slot
  (Setzschlitz) with a sliding jamb; openings limited by horizontal-joint
  break at window height.
- Airtightness at the reveal: tape the panel's Dampfbremse continuously to
  the frame's inner seal band (clamp batten), outer wrap vapour-open — same
  three-layer joint, timber version; the frame sits *inside* the airtight
  plane of the wall, never outside it.

### 11.2 Cold-formed steel

- Openings: lipped header (C/U channel hat sections) over the opening, trim
  studs/jambs doubled; laterally restrained compression flange rules apply —
  top edge of wide headers often needs blocking/strapping (`timber-steel-design`
  steel section).
- Steel is a thermal bridge: a bare steel lintel in an insulated wall
  conducts ~50 W/(m·K) across the Dämmebene — use a **thermally broken
  lintel (GFK/PU spacer between inner and outer skin)** in cold climates or
  the Uw/ψ penalty swallows the wall's U-value. Differential thermal movement
  of steel lintels cracks render (§6.4).
- Fixing windows into steel: self-drilling screws into the stud flange with
  the system's fixer; never rely on the sheathing alone for pull-out.

---

## Section 12: Coordination and Existing Buildings

### 12.1 Openings vs everything else

| Discipline | Interaction | Rule |
|---|---|---|
| Slab/beam layout | beam landing in the wedge voids arch action (§4.2) | keep beam bearings out of 0.866·l above heads, or design the lintel for the reaction |
| Columns | column inches from the jamb leaves an unusable sliver | merge jamb into column or keep ≥ 600 mm pier |
| MEP | boxes/conduit in a narrow pier destroy it | chases per §2 limits only; sleeves through lintel zone = void arching; AC/vent sleeve above a head gets its own mini-lintel and outward fall |
| Roof/eaves | window head under a deep eave | still needs its own drip — concentrated runoff is worse than rain; sill + tray carry the water |
| WDVS (ETICS) | window sits in the insulation plane | frame mounted ahead of the masonry face on a cantilever bracket / insulating block; airtight layer taped to the frame *inside* insulation line; box/roll-shutter details per §7.5 |
| Finishes | plaster cracks at lintel-to-masonry junctions | reinforcement mesh strip ~300 mm over every junction before plaster |
| Lifts/cranes during build | lintels load only after the mortar cures | §4.2 green-masonry rule; no props removed early |
| Byelaws | light/air volumes, Abstandsflächen, Fenster formats | local; cross-reference permits skill |

### 12.2 Replacement windows (Bestand) — the U-value and joint traps

- GEG exchange limits §9.2 above; *if you touch more than the glazing, the
  window limit applies to the whole element.* De-minimis: ≤ 10 % of the
  component group (small-window exemption **[VERIFY current wording]**).
- Old box windows: exchange of the inner leaf only → Ug ≤ 1.1 low-e; the
  box cavity then must be vented/dried — sealed wet cavity = rot.
- Retrofit reveal physics: with a thin new frame in a deep old reveal, the
  airtight layer must be *brought to the frame* (insulating reveal block +
  taped flange) — filling the reveal with insulation without re-establishing
  the air seal is the most common retrofit blower-door failure.
- **Bestandsschutz (grandfathering):** a lawful old window may stay; but a
  replacement is a "new installation" → current thermal (GEG) + current
  joint practice apply, and in escape/fire-relevant windows note that a
  repaired element may not simply replicate a since-known-unsafe state (e.g.
  overhead single-safety-glass → VSG expectation in current practice).

### 12.3 Cutting a new opening in an existing wall

**Hand this section to a licensed engineer; do not execute it from a chat
message.** Same warning must appear in the same message as any procedure.

- Assess: is the wall load-bearing *and* bracing? What bears within 0.866·l
  above? Foundations under the two new jambs (load concentrates from a line
  to two points)? Services in the wall? Party/adjacency?
- Sequence (engineer-designed temporary works): props both faces on spread
  bases → needles (Acroya/wood) through above the future head, wedged tight
  → cut slot, install new lintel on full designed bearing + padstones →
  dry-pack/grout tight under the masonry above (a gap = later settlement +
  cracks everywhere above) → cure → remove needles → then remove the wall
  below → jambs/ring-anchor re-connection.
- Masonry compensation for a Durchbruch in a bracing line follows current
  rules even where Bestandsschutz spares the rest of the building.

---

## Section 13: Schedule Management — Fensterliste and IFC

### 13.1 Fensterliste data model (the one table that prevents 90 % of disputes)

Carry **one row per element type** (not per opening — position list
separately):

| Field group | Fields |
|---|---|
| ID/position | Element-Nr (F01, T01…), room, wall ref, storey, quantity, opening coordinates |
| Geometry | Rohbaumaß B×H×T (wall build-up!), lichte Maß, Brüstungshöhe, head level, Scheibenteilung, opening line/rotation, DIN right/left, swing |
| Structure | lintel type + ref (from §3 schedule), bearing, jamb verticals, span class |
| Physics | Uw (target + calc basis), Ug, Uf, ψg, g-value, τ, frame fraction; Rw + C/Ctr + mounting margin (−2 dB); air class EN 12207, rain class 12208, wind 12210; glass make-up + safety class (DIN EN 12600: ESG/TVG/VSG + where) |
| Hardware/joints | Verglasungsart (press glazing?), Beschlag (incl. security RC2/RC3 if required), drive (roller shutter/Raffsoll), sill/threshold type, mounting system + anchor type per masonry subcategory, Dichtungsstufen detail ref (drawing no.) |
| Energy/legal | GEG limit basis (new/exchange), note if Förderprogramm (BEG) U-value requirements tighter, Baugenehmigung reference, rescue-window flag |
| BIM | IfcGUID, IfcType, host wall GUID, Space boundary, Pset mapping (§13.2) |

Rules: the Fensterliste is **the** interface to the window maker — it must
name the *detail*, not just the size (window makers quote per detail);
every element that is load-bearing-glazing (Brustung/Überkopf), rescue, RC,
fire or acoustic gets its own verified column with the standard named.

### 13.2 IFC mapping (IfcWindow / IfcDoor)

- `IfcWindow`/`IfcDoor` carry: `PredefinedType` (WINDOW/DOOR),
  `IsExternal`, `OperationType` (door: SINGLE_SWING_LEFT, LIFT_SLIDE…),
  `PanelCount`, `OverallWidth/Height`, and Part-of wall via
  `IfcRelFillsElement` (opening element from `IfcOpeningElement`).
- Physics properties belong in property sets, not geometry: thermal
  transmittance (Uw), solar factor g, visible transmittance, acoustic
  rating Rw (+C/Ctr), air-tightness class, fire class, RC class — map the
  §13.1 columns onto Pset_WindowCommon / Pset_DoorCommon (+ custom Pset
  for the ψg basis and the mounting detail no.).
- Geometry gotchas that actually bite (verified on FreeCAD 1.x;
  see `construction-freecad-bim` for the full void workflow):
  1. **`Arch.makeWindow`'s `Hosts`/`Subtractions` link does NOT reliably cut
     the wall** in this build — verified by a zero volume-difference test.
     Model the *void* as an explicit boolean (`Part.makeBox` cut from the
     wall shape → `Part::Feature`), and keep a separate `Arch.makeWindow`
     object at the same placement purely for correct IFC classification.
  2. **A hand-set `Normal` on a Window/Door object corrupts `buildShapes`**
     (null/degenerate shape). Leave `Normal` at its default; orient with the
     object's own `Placement.Rotation`.
  3. **The `Base` sketch `Placement` has ZERO effect on the built shape** —
     only the *object's* Placement moves/rotates it. If a door came out
     lying flat after reverting a corrupted Normal (default `(0,0,-1)`
     builds a skylight-facing-down leaf), reset Placement to identity, read
     the raw `Shape.BoundBox`, find which local axis carries `Height`, then
     `Rotation(Vector(0,1,0), -90)` (X case) or `Rotation(Vector(1,0,0), +90)`
     (Y case), then translate to match the void's BoundBox centre.
  4. **Verify every placement with `Shape.BoundBox`, not with "shape is not
     null."** "Not null" is not the same as "geometrically sane"; after any
     fix, confirm the element's BoundBox falls inside the void's BoundBox
     with a small tolerance. Do not batch-apply best-guess rotations — that
     silently misplaces elements with similar spans.
  5. Lintels modelled via `Arch.makeStructure` (IfcType Beam) have
     **IfcType-dependent axis anchoring** (Beam: Length corner-based X,
     Width/Height centred) — print the BoundBox immediately after setting
     Placement or the lintel lands 75 mm low across its own opening.

### 13.3 Modelling discipline for openings

1. Model every lintel as a distinct object (IfcBeam), length =
   clear span + 2× bearing; a wall with a hole and no head member is a
   drawing, not a model.
2. Model the Ringanker as one continuous storey band — or nobody builds it.
3. Run a pier-width sweep per floor (list opening widths + remaining piers;
   anything under your §2 floor is a finding) and an opening-ratio check per
   wall — a 20-line Python loop that catches most opening errors.
4. Check the relief wedge is clear per opening (beam/slab/tank in the
   triangle → flag "arching void — design for full load").
5. Tag in the model or its README: head-level decision, arching assumption,
   which heads are engineer-designed beams, which windows carry
   acoustic/RC/fire duties.
6. If FEM is run, a lintel modelled without its bearing length is a lintel
   with the wrong span — model the full member.

---

## Section 14: Worked Examples

### 14-C: Uw build-up of a 1400 × 1200 mm room window

Frame fraction 30 % → A_w = 1.68 m²; A_f = 0.504; A_g = 1.176;
visible edge length l_g ≈ 2·(1.10 + 0.90) = 4.0 m.

```
case                                   U_w = (A_g·U_g + A_f·U_f + l_g·Ψ_g)/1.68
double low-e, PVC 4-ch, bare-Alu spacer
     Ug 1.1 · Uf 1.4 · Ψg 0.08 → (1.294+0.706+0.320)/1.68 = 1.38  ✗ misses 1.3
same + warm-edge Ψg 0.04          → (1.294+0.706+0.160)/1.68 = 1.29  ✔ GEG exchange limit
triple low-e, PVC 5-ch, warm edge
     Ug 0.6 · Uf 1.2 · Ψg 0.05   → (0.706+0.605+0.200)/1.68 = 0.90  ✔ passivhaus-adjacent
triple low-e, bare Alu frame
     Ug 0.6 · Uf 7.0 · Ψg 0.05   → (0.706+3.528+0.200)/1.68 = 2.64  ✗✗
```

Readings: the warm-edge spacer alone is worth ~0.1 W/(m²K); the frame alone
is worth 1.7. **A good pane cannot rescue a bad frame** — which is why
manufacturer *system Uw* values for the exact profile/glass/spacer
combination, not component averages, go into the Fensterliste.

### 14-D: Acoustic weak-spot logic — window vs wall

Façade 12 m², window 1.5 m² (12.5 %). Energy combination over areas
(τ_i = 10^(−R_i/10), R_res = −10·lg Σ(S_i·τ_i)/ΣS):

| Option | Wall R | Window R | Result |
|---|---|---|---|
| as built | 53 dB | 35 dB | **≈ 44 dB** |
| upgrade wall +7 dB | 60 dB | 35 dB | ≈ 44 dB — 7 dB spent, 0.3 dB gained |
| upgrade window +7 dB | 53 dB | 42 dB | **≈ 49 dB** |

The window *is* the element. Spec from the noise site: required D_np,r from
Lärmpegelbereich L_a (I 55 … VII >80 dB(A), urban planning map) minus room
target, then split the duty — never "wall best possible, window catalogue
standard". Then: traffic noise → rate with **Ctr** (R_w+Ctr), living noise →
C; subtract ~2 dB mounting margin for a standard install (tight reveal,
sealed perimeter); remember tilt/parallel-slide windows only keep 6–12 dB
whatever the pane says — ventilation while "closed" is an acoustic design
decision (heat-recovery ventilation instead). **[VERIFY catalogue rows of
DIN 4109-35 for the specific glass make-ups.]**

### 14-E: Lintel bearing + Teillast in one pass (2.4 m window)

l = 2.4 m, 240 mm HLz, γ 13 kN/m³, arch void (slab 0.7 m above head):
wall strip 0.7·0.24·13 = 2.18 kN/m + slab end reaction ~ tributary strip
(2 m × 5 kPa ≈ 10 kN → treat as line/point, design beam properly) +
self 1.44 kN/m → w_G,d ≈ 4.9 kN/m + concentrated. Bearing rule:
max(150, h=240, l/12=200) → **240 mm** bearing; reaction ≈ 4.9·2.88/2 ≈
7.1 kN per end + concentrated share → σ on 240×240 pad ≈ 0.5–1.2 MPa vs
fd ≈ 0.85·5.0/1.5 ≈ 2.8 MPa with β up to 1.25 → passes as a *check*, but
the moment (≈ w·l²/8 plus point loads) has left lintel-table territory:
designed beam, 3–4 Ø16 + links, L/600 = 4 mm deflection target with
h ≈ l/10 = 240…300 mm. The example pattern: **geometry checks pass cheaply,
deflection and the point load decide the member.**

---

## Section 15: Failure Modes and Anti-Patterns

Ranked by real-world frequency in DACH execution.

1. **Flachsturz installed upside down** — all steel in the compression zone;
   cracks, fails. *Fix: paint-mark the top at casting; check before bed.*
2. **No lintel at all** ("it's only a 0.6 m vent") — stepped diagonal cracks
   from both corners within a year. *Every opening gets a lintel or a proven
   arch (§4).*
3. **Bearing on a cut brick / 75 mm nib / plaster.** Local crush → diagonal
   from the bearing point. *Fix: §5, padstone, fresh full bed.*
4. **Bars cut to fit the lintel length** — the end is a hinge. *≥ lb or hook
   into pier/jamb (§6.3).*
5. **Wall built on green lintel** — 2 m of fresh wall on yesterday's concrete
   or yesterday's arch mortar. *§4.2: ≥ 24 h, ≤ 1 m/day; centring ≥ 7 d.*
6. **Ringanker discontinuous** — five separate lintels called a band.
   *One head level, continuous band, laps around every corner.*
7. **Cold bridge at the head** — bare concrete lintel/reveal left uninsulated
   under the frame: first winter, black mould streaks over the window.
   *Reveal insulation in one plane, overlap into wall insulation (§8.3).*
8. **Missing seal continuity** — PU foam treated as the airtight layer;
   blower door fails at exactly the windows. *Three-layer joint, taped inner
   band continuous with the wall layer (§8).*
9. **Water at the sill** — no fall, no drip arris, no end dams, or the rain
   flange sealed *under* the drainage plane instead of on it. *§8.4.*
10. **Wrong fixing for the masonry class** — a standard frame anchor spun
    into Porenbeton or horizontally-perforated HLz pulls out under wind
    suction; chemical anchors near the edge split the unit. *Anchor type per
    masonry subcategory + edge distances from the ETA; pull-out test the
    job site condition. (§8.3)*
11. **Cavity tray / weeps omitted or plastered over** above a veneer or
    two-leaf lintel — permanent damp above the window, or a water reservoir.
    *§6.4; mark weeps, inspect after plaster.*
12. **Ungalvanised angle in façade service** — rust jacking lifts the course
    above; render map-cracks over the steel because its ΔT movement is 5×
    masonry's. *Fire-dip galvanise; movement break.*
13. **Arch built without skewback/abutment, centring struck early, or next
    to a corner** — thrust spreads, crown cracks (3-hinge). *§4.4.*
14. **Openings not stacked / corner windows in load-bearing masonry** —
    forced horizontal bends, tension cracks, lost corner. *§2 rules.*
15. **Chase hammered through a jamb pier or under a lintel end** —
    pre-made failure plane; also voids arching. *§2 slot limits; coordinate
    MEP before masonry.*
16. **Short column from a partial sill panel beside a ribbon window.**
    *Isolate or design (§10).*
17. **Roller-shutter box as cold bridge + leak** — uninsulated box, untaped
    lid, cold streaks at the ceiling line. *§7.5 Roka criteria.*
18. **Acoustic over-spec on the wrong element** — 42 dB door in a 38 dB
    wall; money burned for 0.3 dB (§14-D).
19. **Fire door without closer/perimeter seal, or cylinder/letter-hole left
    unsealed** — the "T30" is decorative. *`fire-protection-building`.*
20. **Fensterliste quoting sizes only, no detail references** — window maker
    prices the cheapest joint; the site discovers the missing DPC/flange/
    reveal-insulation line items as change orders.
21. **Trusting the model over the BoundBox** — hand-set Normal corrupts
    shapes; Base-sketch Placement silently does nothing; "shape not null"
    hides a door lying flat like a skylight. *§13.2 verify discipline.*

---

## Section 16: Checklists

### 16.1 Before the Fensterliste goes out

- [ ] Head level fixed per storey; openings stacked, piers ≥ §2 floors
- [ ] Every opening has a lintel/arch/slab-edge member assigned (§3 type,
      §3.3 depth, §5 bearing, §6.3 anchorage)
- [ ] Arch-action validity per opening (§4.2) — void cases designed for full load
- [ ] Teillast check at every lintel end (§5.2) or jamb vertical added
- [ ] Deflection target met for the masonry above it (§6.1)
- [ ] Veneer/2-leaf: tray + end dams + weeps on the lintel line (§6.4)
- [ ] Roll-shutter/box detail chosen and Roka criteria noted (§7.5)
- [ ] Per window: Uw computed (formula, §7.3) with *system* values,
      g + F_s shading checked for summer (§7.5), Rw(+C/Ctr) matched to the
      combination element (§14-D), air/rain/wind classes per exposure
- [ ] Joint detail per element: 3-layer build-up, sill slope + drip + end
      dams + flange on the drained plane, reveal insulation continuous,
      anchor type per masonry class (§8)
- [ ] Rescue-window / Brüstung / safety-glass duties flagged (§1.3, §9.3)
- [ ] Fire and accessibility duties cross-checked, not invented here

### 16.2 Before the model is called "done"

- [ ] Every lintel modelled as a member (length = span + 2× bearing),
      Ringanker as one continuous object
- [ ] Void cut verified by **volume difference**, element placement verified
      by **Shape.BoundBox** — not by "not null" (§13.2)
- [ ] Pier-width sweep + opening-ratio check per wall, per direction, per storey
- [ ] Relief-wedge clearance check per opening (point loads flagged)
- [ ] Wall density / bracing recomputed **after** the final opening layout;
      every large opening has a written §10 compensation
- [ ] No chases in piers/bearing zones in the model's MEP pass
- [ ] Output labelled: *preliminary coordination basis — structural design
      and stamp by a qualified Tragwerksplaner, physics by the Bauphysik
      reviewer, before construction / before ordering.*

---

## Section 17: Known Gaps in This Skill (state them when relevant)

1. **Tabulated grids partially lost in the references**: the full Uw (10077)
   Uw matrices, mullion ΔU grid (17.43), door/gate grids (17.46/47),
   DIN 4109-35 window catalogue make-ups and DIN 4109-1 tabulated dB values.
   Anchors printed here are partial readings **[VERIFY]** — compute with the
   formulas, or use manufacturer system data, before quoting numbers.
2. **EN 845-1/-2/-3 (masonry lintels, bed-joint reinforcement) clause text
   and product tables are not reproduced**; precast selection follows the
   supplier's CE/Zulassung tables. The §3.3 schedule is a paraphrased working
   table, not a code transcription.
3. **The camber values for brick arches (1/50 / 1/12) read anomalously
   large** in the digest — flag and verify against EN 845-2 / current
   Fachbuch before setting out a real arch. Same for the exact 30°/60°
   load-distribution angle in the §5.2 Teillast formula.
4. **Metal-spacer Ψ_g column was garbled in the digest** (0.02/0.01 pairs
   printed against "no break" are not physically plausible — bare aluminium
   edge loss is historically the worst case). Treat bare-metal Ψ_g as
   manufacturer data ≥ ~0.3 and **[VERIFY]**.
5. **Rain class (EN 12208) assignment per driving-rain group** and the wind
   zone → design pressure chain are carried in `building-physics-thermal-moisture`;
   this skill only names the classes.
6. **GEG amendment drift**: reference-building and existing-building limit
   values (Uw 1.3/1.1 etc.) move with legislative revisions and interact
   with BEG funding minima — re-check the current text for any submission
   **[VERIFY edition]**.
7. **No RC-lintel design tables for engineered wide heads** beyond the §3.3
   pre-sizing tier — anything flagged "designed beam" is a placeholder for
   the engineer's analysis (`concrete-detailing`, `structural-analysis`).
8. **State-by-state LBO variance** (Brüstungshöhen, Rettungswege dimensions,
   rescue-window rules) is not consolidated here — cite the applicable
   Landesbauordnung per project, cross-refer `fire-protection-building`.
9. **Bautischler/timber-window specific rules** (DIN 68121 wooden-window air
   class without seal, setzungsfuge sizing per species shrinkage) appear only
   as flags; detail work belongs to the timber trades' norms.
10. **All reinforcement quantities are indicative for feel and estimating
    only** — no table here is a Bewehrungsplan.
