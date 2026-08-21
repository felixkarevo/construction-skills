---
name: architecture-openings-lintels-detailing
description: >
  Structural detailing of door and window openings in houses, calibrated to
  Pakistan (BCP-SP 2007 / BCP 2021) with ACI 318-19, IS 456:2000, IS 1905,
  IS 4326, IRC 2021, ASCE 7-22 and AWC SDPWS 2021 as deep-detail
  cross-references. Covers arching action and the true load on a lintel,
  RCC lintel sizing and reinforcement tables, bearing and anchorage rules,
  precast vs cast-in-situ lintels, combined lintel-chajja detailing, steel
  angle lintels for veneer, header beams over wide openings in RCC frames,
  IRC wood-frame header spans, masonry arches (jack, segmental, semicircular)
  as a lintel alternative including thrust and abutment design, sill and jamb
  detailing, through-wall flashing, DPC/cavity trays and weep holes, the
  lateral-bracing penalty of large openings (perforated shear wall vs Force
  Transfer Around Openings) and how to compensate, cutting new openings in
  existing walls, FreeCAD modelling defaults, and the opening failure modes
  that actually collapse houses.
---

# Openings, Lintels and Structural Detailing (Houses, Pakistan-Calibrated)

An opening is a hole punched in a load path. Every door and window is a place where the wall stops carrying load vertically and has to hand that load sideways into the masonry or frame beside it, then back down. This skill is a **preliminary sizing, detailing and modelling aid** for those handoffs in 1-3 storey houses — the kind actually built on 3, 5, 10 marla and 1 kanal plots in Pakistan, or their equivalents elsewhere. It exists so that a FreeCAD model has *plausible, code-anchored* lintel depths, bearings, bar counts, sill details, arch geometry and pier widths beside a sliding door, rather than arbitrary ones — and so that a wide opening is recognised as a **lateral-system problem**, not just a beam problem.

Pair with `architecture-structural-systems` (§6.3 lintel beams, wall density, load path), `architecture-concrete-reinforcement-detailing` (cover, development length, bar bending schedules), `architecture-seismic-design` (bands, short columns, opening limits), `architecture-roofing-waterproofing` (flashing and DPC materials), `architecture-masonry-materials` where present, and `architecture-freecad-bim` (parametric Subtractions for openings).

## Reality Check - Licensing & Liability

**This skill produces design aids and calculation guidance for planning and FreeCAD modelling ONLY.**

- Every lintel depth, bar count, arch rise, pier width and header span in this file is a **preliminary sizing estimate, a code minimum, or a rule of thumb**. Rules of thumb are calibrated to "typical" spans, wall thicknesses, loads and seismicity. Your opening is not typical until someone has checked it.
- **Any design intended for the actual construction of a real occupied building MUST be reviewed, analysed and stamped by a licensed structural engineer** — in Pakistan, a **PEC-registered (Pakistan Engineering Council) Professional Engineer** in the relevant structural category. Elsewhere, the equivalent locally licensed or chartered structural engineer.
- **The design MUST also go through local authority plan approval before construction** — LDA (Lahore), CDA (Islamabad), RDA (Rawalpindi), SBCA (Karachi), PDA, GDA, or the relevant TMA / Cantonment Board — under their building byelaws, which are *separate* from and *additional to* the structural code.
- **Openings are disproportionately dangerous.** Lintel and opening detailing failures are among the most common causes of masonry cracking, partial collapse in earthquakes and progressive damage in houses. An undersized beam over a bedroom may sag; an unsupported 3.6 m sliding-door opening in a shear wall can lose a storey. Treat every number here as an *input to an engineer's check*, never as the check.
- **Claude / Claude must never present FreeCAD output, a lintel schedule, an arch geometry or a bar count from this skill as construction-ready.** Not as "the lintel schedule", not as "the design", not as "final". The correct framing is always: *"preliminary sizing for coordination — to be verified and stamped by a PEC-registered structural engineer."*
- **Say this unprompted.** If the user starts treating the output as final — asks for a lintel bar bending schedule to hand to a contractor, says "the mason is casting lintels tomorrow", asks to widen a window "since the model still stands", asks whether they can knock out a wall between two rooms, or shares the model with a builder — **stop and state the licensing requirement explicitly before continuing.** Do not wait to be asked.
- **Cutting an opening in an existing wall is a special hazard.** Never give step-by-step demolition guidance for a load-bearing wall in an occupied building without stating, in the same message, that this requires a site inspection, a temporary works (propping/needling) design and a stamp from a licensed engineer. Section 16 is written to be handed to an engineer, not executed by a homeowner.
- **Never certify.** Do not produce anything that resembles a stamped drawing, a structural stability certificate, or an engineer's signature block. Do not attach a PEC number to output.
- **Verbatim code clauses are not reproduced here.** BCP-SP 2007 §9.9.8, BCP 2021 Ch. 21, IS 4326 Table 4, AWC SDPWS Table 4.3.3.5 and BIA Technical Notes 31/31A/31B contain the governing text and tables. Where this skill paraphrases them it says so, and Section 20 lists what must be read from source before any real use.
- **Every numeric table in this file is a paraphrased/reconstructed working value, not a transcription of a code table**, unless the surrounding text says otherwise. Several tables below (§3.3 RCC lintel schedule, §8.1 steel angle sizes, §11.1 opening-ratio limits, §13.2 perforated-wall formula) carry an inline flag plus a pointer to the exact Section 20 item that documents what was paraphrased and from where. Reading only the table, without that flag or Section 20, risks mistaking a rule-of-thumb for a code value — so when quoting any of these four tables to a user or into a drawing note, quote the flag with it.

---

## Section 1: The Opening Decision Tree

### 1.1 Fast answers (use this first, then verify downstream)

| Situation | Answer |
|---|---|
| Any opening in a masonry wall, any width | **Needs a lintel.** No exceptions, even a 600 mm bathroom vent. |
| Door 750-1050 mm, 230 mm brick wall | Precast RCC lintel **230 × 150 mm**, 2 – 10 mm bottom, bearing 230 mm |
| Window 1200-1500 mm, 230 mm wall | RCC lintel **230 × 150 mm**, 2 – 12 mm bottom, bearing 230 mm |
| Window / door 1500-2100 mm | RCC lintel **230 × 200-230 mm**, 3 – 12 mm bottom + 2 – 10 top, bearing 250 mm |
| Opening 2100-3000 mm | **Designed RC beam** — do not fix a single section here; use the §3.3 schedule for the exact span band (section grows from 230 × 230 up to 230 × 380 across this range), stirrups, tie-column each side |
| Opening > 3000 mm (car porch, sliding door) | **Frame problem, not a lintel problem.** RC columns both sides + designed beam. Re-check lateral system. |
| Opening > 3500 mm in load-bearing masonry | Stop. Masonry cannot do this. Convert that bay to an RCC frame. |
| Opening head level | Standardise at **2100 mm** for every door and window on a floor so one continuous lintel band works |
| Bearing each side | Greatest of **150 mm**, the lintel depth, or clear span / 12 |
| Bar anchorage past opening face | **≥ 600 mm** or the full development length Ld, whichever is greater (see §5.3 — 600 mm only covers bars up to 12 mm) |
| Opening within 600 mm of a wall corner | Move it. If it cannot move, RC tie-column at the corner and at the jamb. |
| Pier between two openings | **≥ 600 mm** in seismic zones (450 mm absolute floor), confined by tie-columns if < 900 mm |
| Wall above opening less than 0.866 × span | Arching action is truncated — recompute load, do not use the standard triangle (§2) |
| Any beam, joist or concentrated load landing inside the relief triangle | Arching action is **void** — design the lintel for the full load |
| Cavity / veneer wall | Lintel needs a **cavity tray / DPC above it plus weep holes** or you get damp above the window |
| Sliding door / picture window in a braced wall line | Lateral capacity is lost (§13). Compensate before drawing it. |
| Corner window in load-bearing masonry | **Do not.** Structurally the worst possible location. |

> **Note on the "2100-3000 mm" row above:** this fast-answer table intentionally does NOT give one fixed section for the whole 2.1-3.0 m band, because it is not one section — §3.3's finer table shows the required depth growing from 230 mm at 2.1 m to 300-380 mm as the span approaches 3.0-3.5 m. Always go to §3.3 for the actual number; treat this row as "you're in beam territory," not as a section spec.

### 1.2 Which system carries this opening?

```
START: an opening of clear span L in a wall
│
├─ Q1. What is the wall?
│   ├─ Load-bearing / confined masonry ....... go to Q2
│   ├─ Infill panel in an RCC frame .......... go to Q4
│   ├─ Brick veneer over frame/backup ........ steel angle lintel (§8) + flashing (§12)
│   └─ Light timber / cold-formed steel frame  header (§9)
│
├─ Q2. Clear span L?
│   ├─ L ≤ 1.0 m ....... precast RCC lintel, minimum section, nominal steel
│   ├─ 1.0 < L ≤ 2.1 m . precast or in-situ RCC lintel from §3.3 table
│   ├─ 2.1 < L ≤ 3.0 m . DESIGNED RC beam (not a "lintel"): stirrups, top steel,
│   │                    tie-column both sides full height to foundation
│   ├─ 3.0 < L ≤ 3.5 m . upper practical limit of masonry-supported spans.
│   │                    Designed beam + real RC columns + engineer check.
│   └─ L > 3.5 m ....... masonry has run out. Convert the bay to an RCC frame,
│                        or insert a steel/RC portal. Re-run wall density.
│
├─ Q3. Is the wall a shear wall / braced wall line?  (it usually is in a house)
│   ├─ Opening ≤ 25% of that wall's length ... normally absorbable; check pier widths
│   ├─ 25-50% ............................... capacity drops sharply (§13.2). Compensate.
│   └─ > 50%, or opening reaches the top plate  that wall line no longer braces.
│                                              Add length elsewhere, or FTAO/portal frame.
│
├─ Q4. Infill panel in an RCC frame — is the opening full height of the panel?
│   ├─ Full height (head at beam soffit) ..... the frame beam IS the header. No lintel.
│   ├─ Head below beam soffit by ≤ 1 course .. build up in masonry; no lintel needed
│   ├─ Head below beam soffit by > 1 course .. lintel required, sized from §3.3
│   └─ Partial-height infill beside the opening  SHORT-COLUMN / CAPTIVE-COLUMN RISK.
│                                              See `architecture-seismic-design`. Fix it.
│
└─ Q5. Is an arch wanted (verandah, façade, jaali screen)?
    ├─ Decorative only, Zone 2B/3/4 ......... RC lintel behind, arch as cladding (§10.7)
    ├─ Structural, span ≤ 1.8 m, rise/span ≤ 0.15  jack arch feasible (§10.3)
    ├─ Structural, span ≤ 1.8 m, rise/span 0.15-0.5  segmental arch (§10.4)
    └─ Structural, span > 1.8 m ............. major arch — engineered, thrust analysis,
                                              abutment design. Not a rule-of-thumb job.
```

### 1.3 Standard residential opening sizes (Pakistan practice)

| Opening | Width × height (mm) | Sill (mm) | Head (mm) | Lintel |
|---|---|---|---|---|
| Main entrance door (single) | 1050 × 2100 | — | 2100 | 230 × 150 |
| Main entrance (double leaf) | 1500 × 2400 | — | 2400 | 230 × 200, designed |
| Bedroom / room door | 900 × 2100 | — | 2100 | 230 × 150 |
| Bathroom / store door | 750 × 2100 | — | 2100 | 230 × 115-150 |
| Kitchen door | 900 × 2100 | — | 2100 | 230 × 150 |
| Room window | 1200 × 1350 | 900 | 2250* | 230 × 150 |
| Large / drawing room window | 1800 × 1500 | 750 | 2250 | 230 × 200 |
| Picture window | 2400-3000 × 1500 | 750 | 2250 | designed beam + tie-columns |
| Kitchen window (over counter) | 1200 × 900 | 1200 | 2100 | 230 × 150 |
| Bathroom high-level window | 600 × 450 | 1800 | 2250 | 230 × 115 |
| Ventilator over door | 900 × 300 | 2150 | 2450 | shared with door lintel band |
| Sliding patio door | 2400-3600 × 2100 | — | 2100 | designed beam + RC columns |
| Car porch shutter | 3000-4500 × 2400 | — | 2400 | RC frame beam + columns |

\* Standardise the **head** at one level per storey (2100 or 2250 mm), not the sill. One head level = one continuous lintel band = one soffit line for the plasterer = a real seismic band. Mixed head levels are the single most common reason a "lintel band" on a Pakistani house is actually five disconnected lintels.

Accessibility note: a 750 mm bathroom door gives ~700 mm clear and **fails** the 800-815 mm (32 in) clear-width visitability baseline. See `architecture-accessibility-design` before locking door widths.

---

## Section 2: What the Lintel Actually Carries — Arching Action

### 2.1 The relief triangle

Bonded masonry above an opening self-corbels. Load arches across to the supports and only a **triangular wedge** of masonry directly above the opening ever reaches the lintel.

```
        wall above (arches over, does NOT load the lintel)
   ────────────────────────────────────────────────────────
                        /\
                       /  \      relief triangle
                      /    \     base  = clear span L
              h=0.866L      \    height = 0.866 × L  (60° equilateral)
                    /        \   ONLY this wedge loads the lintel
                   /__________\
   ════════════[  lintel   ]══════════════
   masonry     |            |     masonry
   pier        |  OPENING   |     pier
               |            |
```

- Relief triangle: base = clear span **L**, apex angle 60° each side, height **0.866 L** (some texts use a 45° triangle, height 0.5 L — that is more conservative for the lintel and less conservative for the piers; state which you used).
- Load on lintel from wall = weight of that triangle only:
  `W_tri = 0.5 × L × 0.866L × t × γ  = 0.433 L² t γ`
  where t = wall thickness (m), γ = masonry unit weight (kN/m³).
- Equivalent UDL over the span: `w_tri = W_tri / L = 0.433 L t γ` (kN/m).

Masonry unit weights (indicative, verify locally):

| Masonry | γ (kN/m³) | 230 mm wall, per m² |
|---|---|---|
| Burnt clay brick + cement mortar (Pakistan common) | 19.0 - 20.0 | 4.4 - 4.6 kPa |
| Solid concrete block | 22.0 - 24.0 | 5.1 - 5.5 kPa |
| Hollow concrete block | 13.0 - 16.0 | 3.0 - 3.7 kPa |
| AAC block | 6.0 - 8.0 | 1.4 - 1.8 kPa |
| Plaster, both faces, 12 mm each | — | add 0.5 kPa |

### 2.2 The four conditions that VOID arching action

Arching action is a gift, not a right. Design for full load — no triangle — whenever **any** of these is true:

1. **Insufficient masonry above.** Height of continuous, bonded masonry above the lintel is **less than 0.866 L**. Then the triangle is truncated: take the trapezoid actually present, plus whatever sits on top of it.
2. **A concentrated load lands inside the triangle.** A beam bearing, a joist, a column, a water-tank leg, a roof truss shoe within the wedge → arching cannot form → design for the full reaction plus the wall.
3. **A slab or floor bears within 0.866 L above.** Very common: a window head at 2250 mm with the slab soffit at 2900 mm and a 1.8 m opening (0.866 × 1.8 = 1.56 m > 0.65 m available). The lintel takes slab load.
4. **The masonry is not bonded / not continuous.** A vertical movement joint, a second opening, a chase, a flue, or a change of material inside the wedge breaks the arch. Two windows stacked with < 600 mm between them: no arch.

Also void it if the masonry above is newly built (< 7 days) and being loaded — arching needs cured mortar.

### 2.3 Worked example A — arching action, 1.5 m window

Given: clear span L = 1.5 m; 230 mm brick wall, γ = 19.2 kN/m³; 2.6 m of continuous masonry above the head; no beams or slab within the wedge.

```
Check availability:  0.866 × 1.5 = 1.30 m  <  2.60 m available   → full triangle forms ✔
Triangle load  W_tri = 0.433 × 1.5² × 0.23 × 19.2 = 4.30 kN
Equivalent UDL w_tri = 4.30 / 1.5                 = 2.87 kN/m
Lintel self weight   = 0.23 × 0.15 × 24           = 0.83 kN/m
Plaster on triangle  ≈ 0.5 kPa × (0.5×1.5×1.30)/1.5 = 0.33 kN/m
------------------------------------------------------------------
Service UDL  w  = 2.87 + 0.83 + 0.33  ≈ 4.0 kN/m   (all dead load)
Factored     wu = 1.4 × 4.0 = 5.6 kN/m   (ACI 318-19 §5.3.1, D only)
Moment       Mu = wu L² / 8 = 5.6 × 1.5² / 8 = 1.58 kN·m
Shear        Vu = wu L / 2  = 5.6 × 1.5 / 2  = 4.2 kN
```

Compare: if you had (wrongly) taken the **full wall height** of 2.6 m above the opening,
`w = 2.6 × 0.23 × 19.2 = 11.5 kN/m` — nearly **3× the real load**. That is why masons' oversized lintels "work" and why an engineer's slim lintel is not a mistake.

Compare the other way: if a 4.0 m span RCC slab landed on this wall 0.65 m above the head, the lintel would additionally take roughly `6.5 kPa × 2.0 m tributary = 13 kN/m` — **4× the arching load**. Same window, completely different lintel. Always ask what is above.

---

## Section 3: RCC Lintel Sizing

### 3.1 Depth rules of thumb (use two, take the larger)

- **Span ratio:** `D = L / 12` (simply supported, most lintels) to `L / 15` (well-restrained/continuous). Some texts allow up to `L / 8` for heavily loaded lintels — treat `L/12` as the working default.
- **Field rule:** start at **100 mm** and add **25 mm of depth per 300 mm of clear span** (i.e. +1 inch per foot).
- **Course rule (Pakistan/India):** round the depth **up to a whole number of brick courses** — 115 mm (1½ courses incl. joint), 150 mm (2 courses), 230 mm (3 courses), 300 mm (4 courses). A lintel that is not a course multiple forces the mason to cut, and cut courses above a lintel crack.
- **Width:** `b = full wall thickness`. 230 mm wall → 230 mm lintel. 115 mm partition → 115 mm lintel. Never narrower than the wall; a narrow lintel leaves an unsupported masonry lip that spalls.

### 3.2 Deflection limits (this, not strength, usually governs)

| What the lintel supports | Limit | Source basis |
|---|---|---|
| Roof/floor, no non-structural elements likely to be damaged | L / 180 to L / 240 | ACI 318-19 Table 24.2.2 |
| Plastered masonry, general house condition | L / 360 | ACI 318-19 Table 24.2.2 |
| Brittle finishes / attached elements likely to be damaged | L / 480 | ACI 318-19 Table 24.2.2 |
| **Lintel supporting unreinforced masonry above** | **L / 600**, and often an absolute cap of 3 mm | CMHA TEK/TR 91B; BIA Tech Note 31B |
| Steel angle carrying brick veneer | L / 600 and ≤ 0.3 in (7.6 mm) | BIA Tech Note 31B practice |
| Head of a glazed unit / curtain wall | L / 360 and ≤ 6 mm | glazing-industry practice |

Practical consequence: a masonry-supporting lintel at L/600 needs roughly **twice the stiffness** of one designed to L/240. This is why steel angles over long veneer openings get deep quickly, and why a "strength-adequate" 150 mm lintel over a 2.4 m opening still cracks the brickwork above.

Rough serviceability screen for RCC lintels: keep **span/effective-depth ≤ 20** (simply supported, Fe415, lightly stressed) per IS 456:2000 Cl. 23.2.1. A 230 × 150 lintel over 1.5 m gives 1500/115 ≈ 13 — comfortable. Over 2.4 m it gives 21 — marginal; go to 200 mm.

### 3.3 Preliminary RCC lintel schedule (230 mm wall, M20 / Fe415, arching action valid)

> **Table status:** these sections/bar counts are a paraphrased, internally consistent working schedule for pre-sizing and FreeCAD modelling — not a transcription of BCP-SP 2007 §9.9.8 or IS 456 design tables. See Section 20 item 1/2/11 before quoting a figure from this table in anything other than a preliminary coordination note.

| Clear span L | Section b × D | Bottom steel | Top steel | Stirrups | Bearing each side |
|---|---|---|---|---|---|
| ≤ 0.75 m | 230 × 115 | 2 – 10 mm | — | 6 mm @ 200 | 150 mm |
| 0.75 - 1.0 m | 230 × 115 | 2 – 10 mm | — | 6 mm @ 200 | 150 mm |
| 1.0 - 1.5 m | 230 × 150 | 2 – 12 mm | 2 – 10 mm (nominal) | 6 mm @ 150 | 230 mm |
| 1.5 - 2.0 m | 230 × 200 | 3 – 12 mm | 2 – 10 mm | 8 mm @ 150 | 230 mm |
| 2.0 - 2.5 m | 230 × 230 | 3 – 12 mm | 2 – 12 mm | 8 mm @ 150 | 250 mm |
| 2.5 - 3.0 m | 230 × 300 | 3 – 16 mm | 2 – 12 mm | 8 mm @ 125 | 250 mm |
| 3.0 - 3.5 m | 230 × 380 | 4 – 16 mm | 2 – 16 mm | 8 mm @ 100/150 | 300 mm + tie-columns |
| > 3.5 m | **Not a lintel.** Designed beam + RC columns each side. See §6. |

For a **115 mm partition wall**: halve the width, keep the depth, and use 2 – 10 mm bottom up to 1.2 m. Do not put an opening wider than 1.2 m in a 115 mm wall carrying anything.

For a **300 mm or 345 mm (1½ brick) wall**: b = wall thickness, add one bar to the bottom layer, keep depths as above.

**These are pre-sizing values only.** They assume: arching action valid (§2.2 clear), no slab/beam within the wedge, M20 concrete, Fe415 steel, 25 mm cover (internal) / 40 mm (external), simply supported on masonry, non-seismic gravity check. Any deviation → design it.

### 3.4 Bearing length — the rule that gets ignored on site

`Bearing ≥ greatest of:  150 mm  |  the lintel depth D  |  clear span L / 12`

| Clear span | L/12 | Lintel depth | **Governing bearing** |
|---|---|---|---|
| 0.9 m | 75 mm | 115 mm | **150 mm** |
| 1.5 m | 125 mm | 150 mm | **150 mm** (use 230 = one brick) |
| 2.1 m | 175 mm | 200 mm | **200 mm** (use 230) |
| 2.7 m | 225 mm | 300 mm | **300 mm** |
| 3.4 m | 283 mm | 380 mm | **380 mm** |

**Applicability of this rule:** the "bearing ≥ greatest of…" formula is a **masonry-bearing** rule — it governs a lintel or beam that lands directly on a masonry pier and checks that the pier does not crush under the reaction (§3.4 continues below). Once a member is framing into an **RC column** instead of a masonry pier (as in §6, wide openings), this bearing-length check is no longer the governing calculation — the beam's **longitudinal bar development/anchorage length into the column** and the beam-column joint design take over. Don't carry a "bearing = 460 mm" style number from this table into a column-framed beam without re-deriving it from anchorage length; see the note in §6.3.

Then check the **bearing stress on the masonry**, which is what actually crushes:
`f_bearing = R / (b × bearing length) ≤ 0.25 f'm` (approximately; IS 1905:1987 Cl. 5.4 and ACI/TMS bearing provisions give the governing form).

Worked check — 2.7 m opening, reaction R = 22 kN, 230 mm wall, 300 mm bearing:
```
f = 22,000 N / (230 × 300) = 0.32 MPa
Typical f'm for Pakistani burnt-brick masonry in 1:6 cement mortar ≈ 2.5 - 4.0 MPa
Allowable ≈ 0.25 × 3.0 = 0.75 MPa   →  0.32 < 0.75  ✔
```
If it fails: lengthen the bearing, add a **bearing/padstone** (a 230 × 230 × 100 mm precast concrete pad, or 2 courses of solid engineering brick in 1:3 mortar), or turn the jamb into a tie-column.

Practical site rules:
- Bearing is measured from the **face of the opening**, and the total lintel length = clear span + 2 × bearing. A 1.5 m window with 230 mm bearings needs a **1.96 m** lintel — order 2.0 m.
- The lintel must bear on **whole, solid, well-bonded bricks**, bedded in fresh mortar. Never on a cut brick, never on a hollow block's web-free shell, never on plaster.
- Bear on **at least 2 courses of sound masonry**, not on the top course of a freshly laid pier.

---

## Section 4: Lintel Types — Selection

| Type | Typical span | Section | When to use | Watch out |
|---|---|---|---|---|
| **Precast RCC** | ≤ 2.1 m | 230 × 115/150 | Default in Pakistani house construction; cast in a batch on the ground | **Top/bottom marking** — an upside-down lintel has all the steel in the compression zone and will fail. Mark the top face with paint *while casting*. |
| **Cast-in-situ RCC** | any | as designed | Whenever the lintel must be continuous with a band, chajja, or beam | Needs formwork and 7-14 day strike; slows the wall |
| **Lintel band (continuous RC band)** | whole building | 230 × 75-150 | **Seismic zones — mandatory practice.** One band at head level all around | Must be continuous through corners and junctions; laps 50φ; no gaps at doors |
| **Combined lintel + chajja (sunshade)** | ≤ 2.1 m | lintel + 450-600 cantilever | Standard over Pakistani windows for sun/rain | Cast **monolithically**; top steel in the chajja; torsion on the lintel (§7.4) |
| **Boot lintel** | ≤ 2.4 m | L-shaped RC | Cavity walls — supports both leaves in one member | Cold-bridge and tray detailing (§12) |
| **Steel angle** | ≤ 3.0 m | L 90×90×8 up | Brick veneer over frame/backup; retrofit | Corrosion / rust-jacking. Galvanize. Deflection L/600. |
| **Rolled steel joist (RSJ / I-section)** | 2 - 5 m | ISMB 150-250 | Retrofit openings in existing walls; garage headers | Needs padstones; fire protection; deflection governs |
| **Prestressed / hollow-core plank lintel** | 1 - 4 m | proprietary | Where speed matters and the supplier's tables exist | Follow supplier tables, not this file |
| **Brick / stone arch** | ≤ 1.8 m rule-of-thumb | see §10 | Verandahs, heritage/vernacular façades | Generates **horizontal thrust** — needs abutments |
| **Timber lintel** | ≤ 1.2 m | 100 × 150 deodar | Vernacular / northern Pakistan; also part of Dhajji-Dewari | Rot, termite, fire; keep out of damp walls |
| **Wood-frame header (built-up / LVL)** | ≤ 3.6 m built-up | see §9 | Light-frame construction (rare in Pakistan, common in IRC context) | Jack studs; top-unbraced penalty |

### 4.1 Precast lintel discipline (because this is what actually gets built)

1. Cast on a **level, clean, hard bed** — not on loose earth. A twisted lintel never sits flat.
2. **Mark the top face** with paint or a scored "T" as it is cast, before the crew changes.
3. Provide the **correct cover on the bottom** (25 mm internal, 40 mm external/humid) using cover blocks, not stones or rebar offcuts.
4. **Cure 7 days minimum**, wet, before lifting. Lift at 14 days for anything over 1.5 m.
5. Do **not load** the lintel — i.e. do not build the wall on it — for at least 24 h after placing, and never build more than 1 m of masonry above it on the first day.
6. Bed the lintel in **fresh 1:4 mortar** on both bearings, fully bedded, no gaps under the ends.
7. Never cut a precast lintel to length. Cutting removes the anchorage (§5.3).

---

## Section 5: Lintel Reinforcement Detailing

### 5.1 Minimum and maximum steel

**ACI 318-19 §9.6.1.2** (flexural minimum, SI):
```
As,min = max( 0.25 √f'c · bw · d / fy ,  1.4 · bw · d / fy )        [MPa, mm]
```
Imperial equivalent (the form quoted in masonry lintel literature, CMHA TR 91B):
```
As,min = max( 3 √f'c · b · d / fy ,  200 · b · d / fy )              [psi, in]
```

**IS 456:2000 Cl. 26.5.1.1:**
```
As,min = 0.85 · b · d / fy        As,max = 0.04 · b · D
```

**Maximum tension steel:**
- Legacy ACI / IS practice: `ρmax = 0.75 ρb`.
- **ACI 318-19 uses a strain limit instead:** net tensile strain `εt ≥ 0.004` at nominal strength for flexural members (§9.3.3.1), and `εt ≥ 0.005` for the tension-controlled φ = 0.90. Quote the strain limit when writing for an engineer; quote 0.75ρb only when explaining legacy drawings.

Worked minimum check — 230 × 150 lintel, M20, Fe415, d = 115 mm:
```
0.25√20 × 230 × 115 / 415 = 0.25 × 4.47 × 26450 / 415 =  71 mm²
1.4 × 230 × 115 / 415                                  =  89 mm²   ← governs (ACI)
IS: 0.85 × 230 × 115 / 415                             =  54 mm²
Provide 2 – 10 mm = 157 mm²  ✔   (2 – #3 = 142 mm² also ✔)
```

Worked flexural check for the same lintel under Worked Example A (Mu = 1.58 kN·m):
```
As,req ≈ Mu / (0.87 fy × 0.9 d) = 1.58e6 / (0.87 × 415 × 0.9 × 115)
       = 1.58e6 / 37,367 = 42 mm²    →  minimum steel governs, as it almost always does
Provide 2 – 10 mm bottom.
```
**Insight to state out loud:** for house-scale lintels with valid arching action, **minimum steel governs, not the moment.** The design decisions that matter are depth (deflection), bearing (crushing) and anchorage (§5.3) — not bar area.

### 5.2 Shear and stirrups

- Provide stirrups even where `Vu < φVc`. Nominal **6 mm @ 200 mm** (small lintels) to **8 mm @ 150 mm** (200 mm+ deep) is standard practice and holds the cage together during casting.
- Close the stirrups fully (135° hooks, 6φ ≥ 75 mm extension) on anything in Zone 2B and above; open U-links are for gravity-only interior lintels.
- **Tighten stirrup spacing to 100 mm over a distance of 2D from each face of the support** on spans > 2.0 m — this is where the diagonal crack from the opening corner wants to form.
- ACI 318-19 §9.6.3.4 minimum shear reinforcement: `Av,min = max(0.062√f'c · bw·s/fyt , 0.35 bw·s/fyt)`.

### 5.3 Anchorage — the 600 mm rule and why it is not always enough

The site rule is: **bottom bars extend at least 600 mm beyond each face of the opening into the supporting masonry.** That number is not arbitrary — it is approximately the development length of a 12 mm Fe415 bar in M20 concrete:

```
Ld = φ σs / (4 τbd),  σs = 0.87 fy = 361 MPa
M20 design bond τbd = 1.2 MPa; ×1.6 for deformed bars = 1.92 MPa
Ld = 12 × 361 / (4 × 1.92) = 564 mm  ≈ 47 φ   →  round to 600 mm ✔
```

So the rule holds for bars **up to 12 mm**. It fails for bigger bars:

| Bar φ | Ld (M20, Fe415, ≈47φ) | Ld (M25, ≈40φ) | Minimum extension past opening face |
|---|---|---|---|
| 8 mm | 376 mm | 320 mm | 600 mm (rule governs) |
| 10 mm | 470 mm | 400 mm | 600 mm (rule governs) |
| 12 mm | 564 mm | 480 mm | 600 mm |
| 16 mm | 752 mm | 640 mm | **800 mm** |
| 20 mm | 940 mm | 800 mm | **950 mm** |

If the bearing is too short to run the straight length, provide a **90° bend of 12φ** at the end (the bend counts toward development per ACI 318-19 §25.4.3 standard hook rules), or lap into the tie-column cage. **Never** cut the bar to fit the bearing — a cut bar in a lintel end is a hinge.

This 600 mm / Ld rule is for a bar embedded in **masonry or a tie-column**, i.e. still an anchorage-into-masonry problem. Where a beam's main bars instead run into a poured **RC column** (§6, wide openings), the governing check becomes the bar's development length **inside the column concrete**, plus the beam-column joint detailing — a different (and usually more demanding) calculation than "extend 600 mm past the opening face." See the note in §6.3.

### 5.4 Lintel band (seismic band) detailing

In Zone 2B and above, individual lintels should be replaced by a **continuous RC band at head level around the entire building**, including internal load-bearing walls. This is the single highest-value seismic detail in a masonry house.

| Band | Level | Typical section | Steel (indicative — verify against IS 4326 Table 5 / BCP) |
|---|---|---|---|
| Plinth band | top of plinth | 230 × 150 | 2 – 12 mm + 6 mm links @ 150 |
| **Lintel band** | opening head, 2100/2250 | 230 × 75-150 | 2 – 10 mm (walls ≤ 5 m) / 2 – 12 mm (longer) + 6 mm links @ 150 |
| Sill band | window sill, 900 | 230 × 75 | 2 – 10 mm + 6 mm links @ 150 (Zone 3/4, or many/large openings) |
| Roof / eaves band | slab or wall-plate level | 230 × 150 | 2 – 12 mm + 6 mm links @ 150 |
| Gable band | along gable slope | 230 × 75 | 2 – 10 mm |
| Vertical jamb steel | each side of large openings | in a 230 × 230 tie-column | 4 – 12 mm + 6 mm ties @ 150 (100 near band junctions) |

Non-negotiables for a band:
- **Continuous** — it must turn every corner and pass through every wall junction with L-bars / U-bars lapping ≥ 50φ. A band that stops at a door and restarts on the other side is decoration.
- Cast **monolithically** with lintels at the same level. If the head levels differ, either step the band with a full-depth vertical link, or (better) fix the architecture and use one head level.
- Do not chase electrical conduit through the band. Sleeve it before casting or route it below.
- These steel quantities are **paraphrased practice**, not verbatim IS 4326 Table 5 / BCP-SP 2007 §9.9.8 values — see Section 20.

---

## Section 6: Header Beams Over Wide Openings (RCC and Masonry)

### 6.1 When a "lintel" becomes a "beam"

The moment **any** of these is true, stop calling it a lintel and design a beam:

1. Clear span > 2.1 m.
2. Arching action is void (§2.2) — slab, joist or concentrated load in the wedge.
3. The wall above is more than one storey of masonry with openings in it.
4. The opening is in a shear wall / braced wall line and the header must transfer force around it (§13).
5. The member also carries a cantilever (chajja, balcony) — torsion.
6. Deflection must be held to L/600 for masonry above.

A "beam" means: designed section, top and bottom steel, designed stirrups, real supports (RC columns or tie-columns to foundation), and a deflection check — not a table lookup. **Once real RC columns are the supports (rather than a masonry pier), the beam's end condition is a beam-column joint, not a bearing joint** — see the reconciliation note in §6.3 before quoting any "bearing = X mm" number for a beam framing into a column.

### 6.2 Preliminary header beam sizes (residential loading, M20/Fe415, 230 mm wall)

| Clear span | Loading | Section b × D (total) | Bottom | Top | Stirrups | Supports |
|---|---|---|---|---|---|---|
| 2.4 m | wall only (arching valid) | 230 × 230 | 3 – 12 | 2 – 12 | 8 @ 150 | tie-columns 230² |
| 2.4 m | wall + one-way slab | 230 × 300 | 3 – 16 | 2 – 12 | 8 @ 150 | tie-columns 230² |
| 3.0 m | wall only | 230 × 300 | 3 – 16 | 2 – 12 | 8 @ 150 | tie-columns 230² |
| 3.0 m | wall + slab | 230 × 380 | 4 – 16 | 2 – 16 | 8 @ 125 | RC columns 230 × 300 |
| 3.6 m | wall + slab | 230 × 460 | 4 – 16 | 3 – 16 | 8 @ 125 | RC columns 300² |
| 4.2 m | wall + slab (car porch) | 300 × 530 | 5 – 16 | 3 – 16 | 10 @ 125 | RC columns 300 × 380 |
| 4.8 m | wall + slab | 300 × 600 | 5 – 20 | 4 – 16 | 10 @ 100/150 | RC columns 300 × 450 |
| > 5.0 m | any | engineered; consider a downstand beam, a portal, or a steel section |

Cross-check against `architecture-structural-systems` §6.2 — a header is just a beam whose soffit happens to be the opening head, and the same span/depth logic applies. Where the header is cast monolithically with the slab, quote the **total depth from top of slab**, which is what determines the ceiling height and what FreeCAD needs.

### 6.3 Worked example B — 3.6 m sliding door header, RCC frame, G+1

Given: 3.6 m clear opening in an exterior wall; 125 mm one-way RCC slab spanning 4.0 m onto this wall; 230 mm masonry above to a 3.2 m floor-to-floor; M20 / Fe415; cover 40 mm (external).

```
LOADS (service, per metre of header)
  Slab dead        0.125 × 24                       = 3.00 kPa
  Floor finish + ceiling plaster                    = 1.50 kPa
  Live load (residential, ASCE 7-22 Tbl 4.3-1)      = 2.00 kPa
  Tributary width = 4.0 / 2                         = 2.00 m
    → slab D  = 4.50 × 2.0                          = 9.00 kN/m
    → slab L  = 2.00 × 2.0                          = 4.00 kN/m
  Wall above: check arching  0.866 × 3.6 = 3.12 m needed
    available above head (2100) to slab soffit (3075) = 0.98 m  → TRUNCATED, no arch
    take full strip: 0.98 × 0.23 × 19.2             = 4.33 kN/m  (dead)
  Header self weight 0.23 × 0.46 × 24               = 2.54 kN/m  (dead)
------------------------------------------------------------------------
  D = 9.00 + 4.33 + 2.54 = 15.87 kN/m     L = 4.00 kN/m
  wu = 1.2 D + 1.6 L = 19.04 + 6.40 = 25.4 kN/m       (ACI 318-19 §5.3.1)

FORCES (simply supported — conservative; frame continuity would reduce Mu)
  Mu = wu L² / 8 = 25.4 × 3.6² / 8 = 41.1 kN·m
  Vu = wu L / 2  = 25.4 × 3.6 / 2  = 45.7 kN

SECTION  230 × 460 total, d = 460 − 40 − 8 − 8 = 404 mm
  As,req ≈ Mu / (0.87 fy × 0.9 d) = 41.1e6 / (0.87 × 415 × 364) = 313 mm²
  As,min = 1.4 × 230 × 404 / 415                                = 313 mm²   (equal — telling)
  Provide 4 – 16 mm = 804 mm² bottom  (generous; gives frame robustness + stiffness)
  Top: 3 – 16 mm continuous into the columns

SHEAR   φVc ≈ 0.75 × 0.17 √20 × 230 × 404 / 1000 = 0.75 × 0.17 × 4.47 × 92,920/1000
        = 53.0 kN  >  Vu = 45.7 kN → nominal stirrups suffice,
        but provide 8 mm 2-legged @ 125 c/c throughout (seismic + robustness)

DEFLECTION  span/d = 3600 / 404 = 8.9  ≪ 20  ✔  (very stiff — as required
            because unreinforced masonry sits on it: target L/600 = 6 mm)

MINIMUM MASONRY-BEARING LENGTH (screening check only — see note below)
  greatest of 150 / 460 / 3600/12=300  → 460 mm.
```

**Reconciling the 460 mm number with "RC columns 300 × 300 minimum" — read this before using either figure.** The 460 mm above comes from the §3.4 bearing-length rule (`greatest of 150 / D / L÷12`), which is a **masonry-pier bearing check** — it answers "how much sound brick pier does this reaction need under it so the masonry doesn't crush." That number is NOT what sizes an RC column. It is quoted here only to show *why* a masonry pier can no longer do the job: a 460 mm bearing requirement is already bigger than a normal 230 mm pier, which is the real trigger for going to RC columns in the first place.

Once the decision is "RC columns," the governing checks become entirely different ones, all a genuine structural design exercise and NOT a table lookup:
1. **Column axial + moment capacity** under the beam's end reaction (45.7 kN shear here) plus the frame moment transferred at the joint — sized against the tributary gravity and lateral load on that column, not against the beam's bearing length.
2. **Development/anchorage length of the beam's main bars (4–16 mm bottom, 3–16 mm top) inside the column core** — per ACI 318-19 Ch. 25 development-length provisions, checked against the actual column width available (300 mm here leaves limited straight length, so standard 90° hooks bent into the column are the normal detail, not a straight 460 mm embedment).
3. **Beam-column joint shear** at the connection — ACI 318-19 Ch. 18 (or the BCP-SP 2007 seismic overlay) joint-shear checks, which govern column width, joint confinement (closely spaced ties through the joint), and whether the 300 × 300 column shown is even adequate — it is a **placeholder for an engineer's frame analysis**, not a sized column.

So: "300 × 300 minimum" in this table is a **starting point for coordination and FreeCAD modelling** — enough to draw a plausible column and get bar counts/quantities roughly right — not a substitute for the joint and column design above. **The real finding in this example is not a number at all** — it's that a 3.6 m sliding door needs two columns and a foundation under each, sized by frame analysis, not by extending the lintel bearing-length formula past its masonry-only scope.

Then go to §13: this opening has also just removed 3.6 m of shear wall.

### 6.4 Car porch and garage openings (Pakistan-specific)

Almost every Pakistani house has a 3.0-4.5 m car porch opening, usually in the front wall, usually on the boundary side, usually with a room or terrace above.

- Treat the porch opening as a **portal frame**: two columns + one beam, designed as a frame, not as a wall with a hole.
- The porch beam usually also supports a **cantilevered porch slab** (1.5-3.0 m projection) → the beam is in **bending + torsion**. Provide closed stirrups, extra top steel and check torsion explicitly.
- Cantilever back-span rule: the slab or beam behind the porch beam must run back **≥ 2 × the cantilever projection** with continuous top steel, or the porch tips.
- Porch columns are frequently the **most heavily loaded and least well-founded** columns in the house because they sit outside the main footing grid. Give them their own pad footings, tied back with a plinth beam.
- The front wall containing the porch opening is usually **the weakest wall line in the house** for lateral load, and it faces the street. Check §13.

---

## Section 7: Sill, Jamb, Chajja and Frame-Fixing Detailing

### 7.1 Sills

| Parameter | Value | Note |
|---|---|---|
| Standard window sill height | 900 mm | Rooms; gives furniture clearance |
| Low / view sill | 600-750 mm | Drawing room, picture window; check fall-protection |
| Kitchen sill | 1200 mm | 900 counter + 300 backsplash |
| Bathroom high-level sill | 1800 mm | Privacy |
| Fall protection trigger | sill < 750 mm with a drop > 600 mm outside | Guard or restrictor required by most byelaws/IRC R312.2 |
| Sill slab thickness | 50-75 mm RCC, or 25-40 mm stone/marble | Stone is the Pakistani default |
| Outward slope (weathering) | **1:10 minimum**, 15° preferred | Water must leave, always |
| Projection past wall face | 50-75 mm | Enough to throw water clear |
| Drip groove | **10 × 10 mm**, set back 20-25 mm from the outer edge, continuous | Without it, water tracks back and stains the wall |
| Sill DPC turn-up at jambs | 150 mm each end (end dams) | Stops water running sideways into the jamb |
| Sill bar (RCC sill) | 2 – 8 mm + 6 mm distribution | Anti-crack, not structural |
| Sill band (seismic) | 230 × 75 RC, continuous | Zone 3/4, or where openings are many/large (§5.4) |

**Why sills crack:** the two bottom corners of a window opening are stress concentrations. Under any differential settlement, thermal movement or seismic drift, a diagonal crack starts at the sill corner and runs down at ~45°. Fixes, in order of effectiveness:
1. **Continuous RC sill band** through the pier (best — turns the corner into a beam).
2. Two 8 mm bars, 600 mm longer than the opening each side, in the mortar bed below the sill course.
3. Bed-joint reinforcement (ladder mesh) in the two courses below the sill, extending 600 mm past the jambs.
4. A movement joint (only if the wall length warrants one anyway).

### 7.2 Jambs (the vertical edges)

- **Pier width beside an opening:** ≥ 600 mm in Zone 2B+ (450 mm absolute floor in low-seismic gravity-only cases). Below 600 mm the pier crushes under the lintel reaction before the wall ever fails in shear.
- **Distance from an inside corner to the opening:** ≥ 600 mm, or ≥ 0.25 × storey height, whichever is greater. Openings near corners are why corners fail first in earthquakes.
- **Tie-column at the jamb** is required when: opening > 1.2 m in confined masonry; or pier < 900 mm; or the opening is the outermost in a wall; or bearing stress check (§3.4) fails.
- **Vertical jamb steel** in reinforced masonry / confined masonry: at least 1 – 12 mm bar in a grouted cell or tie-column at each jamb, continuous from plinth band to lintel band, lapped 50φ into both.
- **Jamb verticality** matters for the frame: out-of-plumb jambs are the #1 reason aluminium windows leak — the frame is packed, the packers move, the sealant tears.
- **Reveal / rebate:** a 20-25 mm rebate on the outer face lets the frame sit behind the masonry line, giving a weather check and hiding sealant shrinkage. Very cheap, very effective.

### 7.3 Frame fixing

| Frame type | Fixing | Spacing | Edge distance |
|---|---|---|---|
| Timber door frame (chowkhat) | MS hold-fasts cast into masonry | 3 per jamb minimum for 2100 mm height (at ~1/4 points) | 150-300 mm from top and bottom |
| Timber window frame | hold-fasts / lugs | 2-3 per jamb | 150-300 mm |
| Aluminium / uPVC frame | expansion anchors or fixing lugs into masonry / lintel | **≤ 600 mm c/c** | 150-225 mm from each internal corner |
| Steel frame (pressed) | welded lugs cast in | 3 per jamb | 150 mm |

- Fill the frame-to-masonry gap with **non-shrink grout or mortar**, then seal externally with **backer rod + polyurethane/silicone sealant** in a joint 6-10 mm wide (never sealant alone into a deep void — it fails in cohesion).
- Never fix a frame **into the lintel soffit only** — the head fixing takes the frame's out-of-plane wind load and needs the jamb fixings to work with it.
- Do not fix through a DPC or a cavity tray. Every fixing through a waterproofing layer is a leak.

### 7.4 Chajja (sunshade) integral with the lintel

The standard Pakistani window head: an RCC lintel with a cantilevered sunshade cast monolithically.

| Parameter | Value |
|---|---|
| Projection | 450-600 mm typical; up to 900 mm for west façades |
| Thickness | 75 mm at root, tapering to 50 mm at the tip |
| Main steel | 8 mm @ 150 c/c **TOP** (it is a cantilever — steel goes on top) |
| Distribution steel | 6 mm @ 200 c/c |
| Anchorage into lintel | main bars bent down and anchored ≥ Ld into the lintel/band, i.e. ≥ 400 mm for 8 mm |
| Upstand / drip | 25 mm upstand at the outer edge, or a 10 × 10 drip groove on the soffit 20 mm from the edge |
| Top slope | 1:50 fall away from the wall; waterproof/tile if it doubles as a shelf |
| Casting | **Monolithic with the lintel.** A chajja cast later onto a cold joint has no cantilever anchorage and drops. |

**Torsion:** a 600 mm chajja carrying self weight (0.075 × 24 = 1.8 kPa) plus 0.75 kPa live/maintenance produces a torque on the lintel of roughly `(2.55 kPa × 0.6 m) × (0.6/2 + 0.115) = 1.53 kN/m × 0.415 = 0.63 kN·m per metre`. Small, but real, and it is resisted **only by closed stirrups and adequate bearing**. So: closed stirrups (135° hooks) throughout any lintel with a chajja, and never a chajja on a lintel with 150 mm bearing.

The two classic chajja failures: (1) steel placed at the **bottom** instead of the top — collapses on first load; (2) the chajja cast **after** the lintel — collapses in the first monsoon.

---

## Section 8: Steel Angle Lintels (Veneer and Retrofit)

Used where brick veneer spans an opening over a frame or backup wall, and in retrofit where a precast lintel cannot be threaded in.

### 8.1 Indicative angle selection — brick veneer, ~2.4 m of veneer above

> **Table status:** this is indicative practice for a typical veneer height, reconstructed for feel/coordination — it is explicitly **not** a transcription of BIA Technical Note 31B's published span tables (see Section 20 item 4). Real angle selection depends on veneer height, whether a floor bears on the angle, and the L/600 + 0.3 in deflection cap — read Tech Note 31B directly before specifying a real angle.

| Clear span | Angle (imperial) | Angle (metric equivalent) | Notes |
|---|---|---|---|
| ≤ 1.5 m (5 ft) | L 3½ × 3½ × 5/16 | L 90 × 90 × 8 | |
| 1.5 - 1.8 m (6 ft) | L 4 × 3½ × 5/16 | L 100 × 90 × 8 | long leg vertical |
| 1.8 - 2.4 m (8 ft) | L 5 × 3½ × 5/16 | L 125 × 90 × 8 | |
| 2.4 - 3.0 m (10 ft) | L 6 × 3½ × 5/16 | L 150 × 90 × 8 | deflection starts to govern |
| > 3.0 m | built-up section, W/ISMB shape, or plate + angle | | engineered |

**Treat this table as indicative practice, not as a reproduction of BIA Technical Note 31B's tables.** The real selection depends on the height and weight of veneer carried, whether a floor bears on it, and the L/600 deflection cap. Read Tech Note 31B before specifying.

### 8.2 Steel lintel rules

- **Deflection is the governing limit: L/600, and typically an absolute cap of 0.3 in (7.6 mm).** Masonry above cracks long before steel yields.
- **Minimum thickness for exterior use: 1/4 in (6 mm).** Thinner sections rust through.
- **Bearing: 100 mm (4 in) minimum each end**, 150-200 mm preferred; on a padstone if the backup is masonry.
- **Corrosion protection is structural, not cosmetic.** Hot-dip galvanize to ASTM A123 (or paint to a specified system). Rust expands to ~6× the volume of the parent steel — **rust jacking** lifts the brick course above the angle and cracks the wall. This is the dominant long-term failure of steel lintels in humid Karachi/coastal conditions.
- **Do not run a single angle longer than ~6 m** without a movement break — thermal movement of the steel will crack the veneer.
- **Leave a gap** between the end of the angle and the masonry at one end (soft joint) to allow thermal movement.
- **A steel angle needs a flashing/tray above it** and weeps immediately above the flashing (§12) — the angle is a shelf that collects every drop of water in the cavity.
- Fire: exposed structural steel in a house header needs protection (encasement, boarding) if the local code requires a fire rating for that element. Check byelaws.

---

## Section 9: Wood-Frame Headers (IRC 2021)

Included because the IRC prescriptive tables are the clearest published header data and are frequently the reference point in international projects. **Light timber framing is rare in Pakistan and its supply chain barely exists** — do not transplant these tables into a masonry house.

### 9.1 IRC 2021 Table R602.7(1) — built-up header spans (indicative)

> **Table status — read before using:** this is a **single reduced column** from the full IRC table — roof-and-ceiling-load-only, narrow-building best case (see Section 20 item 7). The real IRC table is multi-dimensional: it varies by supported building width (20/28/36 ft), ground snow load, and whether the header also carries a floor or a second storey. **Do not apply the spans below to a header that also carries floor load** — that is a materially different (shorter-span) row in the real table. Always pull the actual table for the real condition before specifying.

Exterior bearing wall, **roof and ceiling load only**, doubled dimension lumber:

| Header | Maximum span |
|---|---|
| (2) 2×4 | 3'-0" (0.91 m) |
| (2) 2×6 | 5'-0" (1.52 m) |
| (2) 2×8 | 7'-0" (2.13 m) |
| (2) 2×10 | 8'-0" (2.44 m) |
| (3) 2×10 | 10'-0" (3.05 m) |
| (3) 2×12 | 12'-0" (3.66 m) |
| > 12'-0" | engineered LVL / PSL / LSL, engineer review required |

Spans shorten substantially once **floor load**, a second storey, or a wider building width is added — the full IRC table is multi-dimensional (building width 20/28/36 ft, snow load, number of storeys carried). The single-column list above is the *roof-and-ceiling-only, narrow-building* best case. Always read the actual table for the real case.

### 9.2 IRC header rules that get missed

- **Jack studs (trimmers) are required for spans over 4 ft (1.22 m)** — one each side minimum, more for long spans; king studs full height in addition.
- **Top-unbraced headers** (2×8, 2×10, 2×12 with no framing above bracing the top edge) get their tabulated span **multiplied by 0.70** unless specifically designed for the unbraced condition.
- Header **depth may require a wood structural panel face-nailed** to one or both faces for stiffness in single-ply or box-header configurations.
- The header must bear on **solid, continuous framing to the foundation** — jack studs on a bottom plate on blocking on the rim joist, not on a cavity.
- Insulated headers (two plies with rigid foam between) are thermally better but **the foam carries nothing** — count only the lumber.

### 9.3 Metric equivalents for engineered products

| Product | Typical residential header depth for 3.0 m | Note |
|---|---|---|
| LVL (Laminated Veneer Lumber) | 2 ply × 45 × 300 mm | Consistent, kiln-dry, supplier tables govern |
| PSL (Parallel Strand Lumber) | 2 ply × 45 × 300 mm | Higher capacity, higher cost |
| Glulam | 90 × 315 mm | Where exposed/architectural |
| Steel flitch plate (timber-steel-timber) | 2 × 50 mm timber + 8 mm plate × 250 | Retrofit; bolts @ 300 staggered |

---

## Section 10: The Masonry Arch as a Lintel Alternative

### 10.1 The one structural difference that matters

**A lintel pushes down. An arch pushes down AND out.** The horizontal thrust must be resisted by abutments — the masonry either side, a buttress, a tie rod, or an adjacent arch. Put an arch next to a corner, a door, or the end of a wall without an abutment and the thrust will push the wall out. Every arch failure in a house traces back to this.

Approximate horizontal thrust of an arch under a uniform load:
```
H = w L² / (8 f)        w = UDL (kN/m), L = span (m), f = rise (m)
```

Worked demonstration — 1.8 m span carrying w = 6 kN/m:

| Rise f | Rise/span | Thrust H | Comment |
|---|---|---|---|
| 0.90 m | 0.50 (semicircular) | 2.7 kN | Low thrust, easy abutment |
| 0.45 m | 0.25 (segmental) | 5.4 kN | Manageable |
| 0.27 m | 0.15 (shallow segmental) | 9.0 kN | Needs a real abutment |
| 0.09 m | 0.05 (near-flat jack arch) | **27.0 kN** | The flatter it is, the harder it pushes |

**Flatter arch = more thrust, always.** A jack (flat) arch looks like a lintel and behaves like a battering ram.

### 10.2 Arch anatomy and geometry rules

```
              ┌── extrados (outer curve)
              │
        ╭─────┴─────╮  ← crown / keystone
       ╱             ╲   ← voussoirs (wedge units)
      ╱   intrados     ╲
     ╱  (inner curve)   ╲
    ╱                    ╲
   ┼══ springline ════════┼
   │  skewback            │
   │        ABUTMENT      │   ← must resist thrust H
   │                      │
```

| Term | Definition | Rule of thumb |
|---|---|---|
| Span L | clear opening | minor arch ≤ 6 ft (1.8 m) |
| Rise f | springline to intrados at crown | see type table §10.3 |
| Arch depth d | intrados to extrados (radial) | **≈ 1 inch per foot of span (25 mm per 300 mm)**, minimum 4 in (100 mm) for spans < 4 ft |
| Voussoir | wedge-shaped unit | joints radial; joint width 3-13 mm, tapered |
| Skewback | inclined bearing surface at the springing | jack arch: commonly cited as ~1/2 in per ft of span per ft of arch depth |
| Abutment | masonry resisting thrust | jack arch: ≥ 1 × span (one exposed face) or ≥ 0.5 × span (two exposed faces); segmental: ≈ 0.66 × span |
| Wall above springline | provides stabilising load | ≥ 1.3 × arch radius for a semicircular arch |
| Camber | upward pre-set in a jack arch | **1/8 in per foot of span (≈ 10 mm per metre)** |

**Minor vs major arch:** a *minor arch* — span ≤ 6 ft (1.8 m) and rise/span ≤ 0.15 for jack arches — can be proportioned by these empirical rules. Anything larger is a *major arch*: full thrust-line analysis, engineered abutments, engineer's stamp. Do not rule-of-thumb a 3 m arch.

### 10.3 Arch types and their envelopes

| Type | Rise / span | Practical max span (rule-of-thumb tier) | Depth | Comments |
|---|---|---|---|---|
| **Jack (flat)** | 0 - 0.15 (nominally flat) | ~1.8 m (6 ft) | ≥ one full unit length (≈ 200 mm) | Highest thrust. Camber it or it will *look* sagged even when sound. Needs the biggest abutment. |
| **Segmental** | 0.15 - 0.50 | ~1.8 m rule-of-thumb; longer if engineered | ≈ 25 mm per 300 mm span, min 100 mm | The best all-round house arch. Good thrust/appearance balance. |
| **Semicircular** | 0.50 exactly | ~2.4 m if abutments are generous | ≈ 25 mm per 300 mm span | Lowest thrust of the common types; needs wall ≥ 1.3 R above springline |
| **Multi-centred / elliptical** | 0.25 - 0.45 | engineered | as segmental | Visually flatter than semicircular; thrust between the two |
| **Pointed / Gothic / four-centred** | > 0.5 | engineered | as segmental | Very low thrust; the Mughal/vernacular Pakistani vocabulary |
| **Relieving (discharging) arch** | any | any | ≥ 200 mm | Built *above* a lintel to divert load around it. Excellent retrofit device. |

### 10.4 Construction requirements

- **Centring (formwork)** must support the full arch until the mortar has cured. Strike no earlier than **7 days**, 14 days for spans over 1.2 m or in cold weather.
- Ease the centring **gradually** (wedges/sand boxes), never knock it out — a sudden release cracks the crown.
- Build the arch **from both springings simultaneously** toward the keystone, so the centring is loaded symmetrically.
- Do not load the arch (build the wall above) until the centring is struck and the arch has taken its own settlement.
- **Both abutments must exist before the arch is built.** An arch built against a future wall is an arch built against nothing.
- Mortar: richer than the wall (1:4 cement:sand or 1:1:6 cement:lime:sand). Lime improves the joint's ability to accommodate the arch's small movements.
- Joints must be **radial** — every joint line, extended, passes through the arch centre. Non-radial joints slide.

### 10.5 Relieving arch over a lintel (the best of both)

A very useful hybrid, and the correct answer for many Pakistani façades:

```
        ╭─────────────╮  ← relieving arch (segmental, 200 mm deep)
       ╱   loose fill  ╲    diverts wall load into the piers
   ═══[═══ RC LINTEL ═══]═══
      |    OPENING     |
```

- The relieving arch takes the wall load into the piers; the lintel takes only the small wedge below the arch.
- Leave the space between the arch intrados and the lintel top **lightly filled** (not packed solid), so the arch, not the lintel, carries.
- Standard historical retrofit for over-spanned or deteriorated lintels; also the way to get an arched *appearance* with a structurally simple lintel behind.

### 10.6 When NOT to use an arch

- **Seismic Zone 2B / 3 / 4 with unreinforced masonry.** An arch is a thrust mechanism that depends on gravity holding the voussoirs in compression. Under vertical earthquake acceleration the gravity briefly reduces and the arch unlocks. Unreinforced arches over openings are a documented casualty producer.
- **Where the abutment cannot be provided** — near corners, near other openings, at the end of a wall, adjacent to a wide opening.
- **Where the wall above will later be opened up** (a future window in the abutment zone destroys the arch).
- **On soft or differentially settling foundations.** An arch is exquisitely sensitive to support spreading — a few millimetres of abutment movement cracks the crown.
- **Where speed and cost matter.** An arch is 3-5× the labour of a precast lintel.

### 10.7 The safe Pakistani compromise

For an arched verandah, an arched entrance, or an arched jaali screen in a seismic zone:

1. Design and build a **structural RC lintel or band** at the true head level, sized per §3.
2. Build the arch **below or in front of it** as a non-load-bearing feature, tied back to the structure with stainless ties at ≤ 450 mm c/c.
3. Detail so that no path exists for the arch to become load-bearing (soft joint at the crown, or clear separation).
4. Say explicitly on the drawing: *"decorative arch — non-load-bearing; RC lintel above carries all load."*

This is the answer to "I want the Mughal arches but the engineer says no arches."

---

## Section 11: Opening Limits in Load-Bearing and Confined Masonry

Openings do not only need lintels — they need to leave enough wall behind. These limits are what keep the wall a wall.

### 11.1 Commonly cited opening limits (paraphrased from IS 4326 Cl. 8.3 / Table 4 style rules)

> **Table status:** these are **paraphrased, commonly-cited values**, not a transcription of IS 4326:1993 Table 4 or BCP-SP 2007 §9.9.8 — see Section 20 item 2. In particular the seismic Category A-E definitions referenced by the left-hand column must be taken from the actual standard, not assumed from this table's labels.

| Rule | Low seismic (Cat. A-C) | High seismic (Cat. D-E) |
|---|---|---|
| Σ opening widths / wall length — **one storey** | ≤ 0.60 | ≤ 0.50 |
| Σ opening widths / wall length — **two storey** | ≤ 0.50 | ≤ 0.42 |
| Σ opening widths / wall length — **three/four storey** | ≤ 0.42 | ≤ 0.33 |
| Distance from inside wall corner to opening | ≥ 450 mm | ≥ 600 mm |
| Pier width between two openings | ≥ 450 mm | ≥ 600 mm |
| Vertical distance between two stacked openings | ≥ 600 mm | ≥ 600 mm |
| Total opening area / wall area (practical guide) | ≤ 40% | ≤ 30% |

**These are paraphrased, commonly-cited values.** IS 4326:1993 Table 4 and BCP-SP 2007 §9.9.8 contain the governing numbers and the category definitions. Verify against the actual table before use — see Section 20.

### 11.2 Effective pier / shear wall segment

A masonry segment beside an opening only counts as a shear wall if it is stocky enough to work in shear rather than flexure:

| Check | Guide |
|---|---|
| Minimum length to count as a shear wall | ≥ 1/3 of its clear height; commonly ≥ 1.0 m |
| Aspect ratio h/L for a pier to be reliable | ≤ 2.0 preferred; > 3.0 → treat as non-contributing |
| Pier below 600 mm wide | Confine with a tie-column, or discount entirely |
| Wall density (per direction, per storey) | See `architecture-structural-systems` — openings reduce the numerator, so recompute after every opening change |

**Recompute wall density after moving any opening.** A "small" change of widening a window from 1.5 m to 2.4 m in a 4.5 m wall takes the remaining pier from 3.0 m to 2.1 m and can drop that wall out of the count entirely.

### 11.3 Openings in infill walls of RCC frames — the short-column trap

A partial-height infill (e.g. masonry up to a 1.2 m sill with a long ribbon window above, or a stair-adjacent half wall) restrains the column over part of its height. The unrestrained portion becomes a **short column** with drastically increased stiffness, attracting force it was never designed for, and failing in brittle shear.

Rules:
- Never let infill masonry partially brace a column. Either fill the panel full height with a proper gap detail, or **separate the infill from the column with a 25-40 mm soft joint** filled with compressible material.
- If a ribbon window above a half-height wall is architecturally required, detail the half wall as a **structurally separated element** (soft joint both sides and at top) or design the column for the short-column condition (closely spaced ties over the full height, typically 8 mm @ 75-100 mm).
- Flag this to the engineer explicitly. See `architecture-seismic-design`.

---

## Section 12: Flashing, DPC, Cavity Trays and Weep Holes

An opening is also a hole in the weather envelope. The structural detail and the water detail have to be designed together, because they occupy the same 100 mm of wall.

### 12.1 Where through-wall flashing / DPC is mandatory

1. **Base of wall at grade** — first course above the ground/plinth.
2. **Above every window and door head** (over the lintel, catching cavity water).
3. **Below every window and door sill** (under the first course of the sill, turned up at both ends).
4. **At every lintel and shelf angle** — anything that forms a shelf in the cavity.
5. At any interruption of the cavity — floor slab bearing, roof abutment, parapet base.

### 12.2 Detail rules

| Rule | Value |
|---|---|
| Flashing must extend | from the outer face (or 6 mm proud, hemmed drip) through the cavity and **up the backup ≥ 200 mm**, mechanically terminated |
| **End dams** | required at both ends of every flashing over an opening; turn up **≥ 25 mm** and extend **≥ 25 mm past the jamb** |
| Lap in flashing runs | ≥ 150 mm, sealed |
| **Weep hole diameter** | **≥ 3/16 in (5 mm)** for tube/rope weeps |
| Open head joint weeps | ≥ 3/8 in (10 mm) wide |
| **Weep hole spacing** | **≤ 33 in (838 mm) o.c.**, practically **every third brick head joint** |
| Weep location | in the **first course immediately above the flashing**, including immediately above lintels and shelf angles |
| Weeps at end dams | provide one at each end dam so trapped water can escape |
| Cavity drainage | keep the cavity clear of mortar droppings; use a mortar-collection mesh at the flashing |
| Sill flashing | continuous, sloped out, turned up ≥ 150 mm at jambs, sealed to the window's own sill pan |

### 12.3 The lintel-specific detail people get wrong

An RC lintel or steel angle spanning the cavity is a **dam**. All the water running down the inside of the outer leaf reaches it and stops. Without a tray and weeps above it, that water backs up and appears as a damp patch on the internal wall above the window — the single most common damp complaint in cavity-wall houses.

```
          ┌──── outer leaf ────┐  ┌── cavity ──┐  ┌─ inner leaf ─┐
   ────── cavity tray / DPC ──────────────────╱ turn up ≥200 mm
   ● ● ●  weep holes @ ≤838 mm, first course above tray
   ══════ LINTEL (RC boot lintel or steel angle) ══════
          ▲ end dam turned up 25 mm, 25 mm past the jamb, both ends
              O P E N I N G
```

Rules: the tray sits **on top of** the lintel, not below it; it must be **stepped up** across the cavity; the weeps go in the course **immediately above** the tray; and the end dams are not optional — without them water simply runs off the end of the tray into the jamb.

### 12.4 Pakistan-specific note

Most Pakistani houses are **solid 230 mm walls with external plaster**, not cavity walls, so §12.3 does not apply directly. What does apply:

- **Horizontal DPC at plinth level** (bitumen/polythene/1:1½:3 concrete course) is universal practice and required — see `architecture-roofing-waterproofing`.
- **Vertical DPC at jambs** of openings in external walls in high-rainfall areas (Murree, Swat, Azad Kashmir).
- **Sill DPC + drip groove** is the single most cost-effective damp detail on a solid-wall house.
- **Chajja over every external opening** does more for the wall than any coating.
- Where an air-conditioner sleeve is cut through the wall above a window, it needs its own lintel (yes, even at 400 × 400 mm) and its own slope-to-outside and sealant detail.

---

## Section 13: Large Openings and the Lateral System

This is the section that gets skipped and should not be. A sliding door or picture window does not just need a beam — it deletes a length of shear wall.

### 13.1 The problem stated

A wall braces a house against wind and earthquake by acting as a **shear panel**. Punch a large opening in it and:
- the full-height sheathed/masonry segments (**piers**) shrink,
- the force has to travel *around* the opening through the header and the sill strip,
- and the corners of the opening become the crack initiators.

Two design philosophies exist for wood-frame walls, and their masonry analogues follow the same logic:

| Method | What it assumes | Consequence |
|---|---|---|
| **Segmented** | Only full-height segments meeting aspect-ratio limits are shear walls; the opening bay contributes nothing | Simplest, most conservative; needs hold-downs at every segment end |
| **Perforated (AWC SDPWS 2021 §4.3.3.5)** | The whole wall works at a reduced capacity via factor Co | Fewer hold-downs (ends only); large capacity penalty |
| **Force Transfer Around Openings (FTAO)** | Straps and blocking explicitly carry force around the opening | Highest capacity retained; requires engineered straps, blocking and analysis (APA/AWC FTAO methodology) |

### 13.2 The perforated shear wall penalty — worked example C

> **Formula status:** the Co derivation used below is **reconstructed from the Sugiyama empirical basis** (`F/F0 = r/(3−2r)`), not transcribed from AWC SDPWS 2021 Eq. 4.3-5 / Table 4.3.3.5 — see Section 20 item 3. The magnitude of the capacity penalty demonstrated here is reliable and is the point of the example; the exact coefficient and its tabulated values must be checked against the standard before using this in an actual design submission.

A 6.0 m long, 2.75 m high braced wall with a 3.0 m wide × 2.1 m high sliding door centred in it. Piers 1.5 m each side.

```
Ao  (total opening area)      = 3.0 × 2.1                = 6.30 m²
h   (wall height)                                        = 2.75 m
ΣLi (sum of full-height segment widths) = 1.5 + 1.5      = 3.00 m
Wtot (total wall length)                                 = 6.00 m

Sheathing area ratio
  r = 1 / (1 + Ao / (h · ΣLi)) = 1 / (1 + 6.30 / (2.75 × 3.00))
    = 1 / (1 + 6.30/8.25) = 1 / 1.764 = 0.567

Empirical strength ratio (Sugiyama basis, adopted in SDPWS)
  F / F0 = r / (3 − 2r) = 0.567 / (3 − 1.134) = 0.567 / 1.866 = 0.304

→ The perforated wall retains ≈ 30% of the capacity of the same wall fully sheathed.
   Expressed as SDPWS's adjustment on the segment lengths:
   Co ≈ (F/F0) × (Wtot / ΣLi) = 0.304 × 2.00 = 0.61
   Capacity = Co × vs × ΣLi = 0.61 × vs × 3.0 m  =  1.82 vs
   (vs full wall would have been 6.00 vs)
```

**Read that again: one sliding door removed 70% of that wall's bracing capacity.** Check the exact Co form and tabulated values against AWC SDPWS 2021 §4.3.3.5 / Table 4.3.3.5 before using in design — see Section 20. The magnitude of the penalty, however, is the point and it is not sensitive to the formula's exact form.

### 13.3 Aspect ratio limits for the remaining piers

| System | Limit | Note |
|---|---|---|
| Wood structural panel shear wall (SDPWS) | h/w ≤ 3.5:1 | Capacity reduction factor 2w/h applies for w/h between 3.5:1 and 2:1 in some cases |
| Perforated shear wall segments | h/w ≤ 3.5:1 for each full-height segment | Segments failing this are excluded from ΣLi |
| Masonry pier (practical guide) | h/w ≤ 2.0 preferred, ≤ 3.0 absolute | Beyond that the pier rocks/flexes rather than shears |
| Confined masonry wall segment | length ≥ 1/3 clear height, ≥ 1.0 m | Below this, discount it |

In worked example C the piers are 2.75/1.5 = **1.83** — fine on aspect ratio. The capacity loss is from the missing area, not from slender piers.

### 13.4 Force Transfer Around Openings (FTAO)

FTAO is how you keep a large opening *and* keep the wall working. The wall is designed as a continuous panel with an explicit internal load path around the hole.

```
   ┌──────────────────────────────────────────────┐
   │ ══════ strap (TENSION) above opening ═══════ │  ← flat steel strap, both ends
   │  ┌──────────────────────────────────────┐    │     anchored ≥ 600 mm past the
   │  │                                      │    │     opening into the piers
   │P │            O P E N I N G             │ P  │
   │I │                                      │ I  │  ← blocking = COMPRESSION strut
   │E │                                      │ E  │
   │R │                                      │ R  │
   │  └──────────────────────────────────────┘    │
   │ ══════ strap (TENSION) below opening ═══════ │
   └──────────────────────────────────────────────┘
        hold-down                        hold-down
```

Mechanism:
- Sheathing above and below the opening carries shear.
- **Flat steel straps** at the top and bottom of the opening carry the **tension** chord force that develops around the corners.
- **Full-depth blocking** at the same lines carries the **compression**.
- Corner nailing is intensified; the straps are anchored well past the opening into the flanking piers.

Consequences for the architect/modeller:
- Narrower flanking piers can still count, so a wider opening is possible than the segmented or perforated method allows.
- It is an **engineered method** — strap sizes, nail schedules and blocking are analysis outputs, not table lookups (APA and AWC publish the methodology; WoodWorks publishes strap-detailing guidance).
- It requires the contractor to actually install the straps and blocking. FTAO detailing that gets value-engineered out on site leaves a wall with no lateral system at all. Call it out on the drawing as **structural, not optional**.

### 13.5 How to compensate for a large opening — decision tree

```
A large opening is required in a braced wall line.
│
├─ 1. CAN THE OPENING MOVE?
│     Shift it away from corners and toward mid-wall; split one 3.6 m opening
│     into two 1.6 m openings with a 900 mm pier. Cheapest fix by far.
│
├─ 2. ADD BRACING LENGTH ELSEWHERE ON THE SAME LINE
│     Lengthen a return wall, close a nearby small window, add a wall at the
│     other end of the same line. Bracing must be on the SAME line/direction —
│     capacity in the other direction does not help.
│
├─ 3. UPGRADE THE REMAINING PIERS
│     Wood: thicker sheathing, closer nailing, sheathing both faces, hold-downs
│            at each pier end (not just wall ends).
│     Masonry: tie-columns both sides of the opening, increased tie-column steel,
│            ties @ 100 mm within 450 mm of band junctions, confined pier.
│
├─ 4. ENGINEER THE FORCE PATH AROUND THE OPENING
│     Wood: FTAO with straps + blocking (§13.4).
│     Masonry/RCC: make the opening bay a MOMENT FRAME — columns each side +
│     a deep header rigidly connected, designed for the frame action.
│
├─ 5. INSERT A DEDICATED LATERAL ELEMENT
│     Steel portal frame in the opening bay (the standard answer for a
│     garage/car-porch front wall), or an RC shear wall elsewhere in that line.
│
└─ 6. IF NONE OF THE ABOVE CLOSES THE GAP
      The opening is too big for the structural system. Change the system
      (masonry → RCC frame for that bay) or change the architecture.
      Do not "detail around it".
```

### 13.6 The specific case: a wall of glass

A drawing room with a 4.8 m glazed wall to the lawn is a common Pakistani brief.

- That wall line contributes **zero** bracing. Everything must be carried by the other three sides, and the diaphragm must be able to reach them.
- Diaphragm aspect ratio then becomes a governing check (the slab must span from the glass wall back to the braced walls).
- Torsional irregularity: with one open side, the centre of rigidity shifts hard away from the centre of mass. Expect the engineer to require a shear wall or a moment frame in that line anyway.
- Practical fix that preserves the view: **two RC columns** breaking the glazing into three bays, with a deep header — a moment frame that reads as a mullion pattern.
- Flag it at sketch stage. Discovering it after the plan is approved costs a redesign.

---

## Section 14: Coordination — Openings vs Everything Else

| Discipline | Interaction | Rule |
|---|---|---|
| **Slab / beam layout** | A beam landing near an opening voids arching action and may exceed bearing | Keep beam bearings ≥ 0.866 L away from an opening, or design the lintel for the reaction |
| **Columns** | A column too close to a jamb leaves an unusable sliver of masonry | Either merge the jamb into the column, or leave ≥ 600 mm of pier |
| **Stairs** | Openings under a landing beam are a classic short-pier condition | Check pier height and aspect ratio |
| **MEP** | Electrical boxes and conduit chased into a 450 mm pier destroy it | No vertical chase in a pier < 600 mm; see `architecture-mep-coordination` |
| **Plumbing** | A soil stack in the jamb pier is a hidden void | Route stacks in ducts, never in structural piers |
| **AC sleeves** | A 400 mm sleeve above a window head is a second opening in the relief triangle | Give it its own lintel; keep 300 mm clear of the main lintel |
| **Kitchen/bath** | High-level windows above tiled walls need the sill DPC detailed before tiling | Sequence it — see `architecture-construction-sequencing` |
| **Finishes** | Plaster cracks at lintel-to-masonry junctions | Chicken-wire mesh strip 300 mm wide over every lintel/masonry junction before plaster |
| **Byelaws** | Ventilation and light area minima drive window sizes; setbacks limit where openings can face | See `architecture-building-codes-permits`; a window on a boundary wall usually needs consent |
| **Accessibility** | 750 mm doors fail 800-815 mm clear width | See `architecture-accessibility-design` |

---

## Section 15: Failure Modes and Anti-Patterns

Ranked roughly by how often they are actually seen on Pakistani sites.

1. **Precast lintel installed upside down.** All the steel in the compression zone. Cracks immediately, fails under load. *Fix: paint the top face at casting; check before bedding.*
2. **Inadequate bearing** — lintel resting 75 mm on a cut brick. Local crushing, then a diagonal crack from the bearing point. *Fix: §3.4, and a padstone if needed.*
3. **Bar cut to fit the lintel length.** No development length; the lintel end is a hinge. *Fix: §5.3; never cut, use hooks.*
4. **Chajja steel at the bottom instead of the top.** Cantilever with no tension steel. Fails on first load. *Fix: it is a cantilever — steel on top, always.*
5. **Chajja cast after the lintel** onto a cold joint. Falls in the first heavy rain. *Fix: monolithic pour.*
6. **No lintel at all** over a small opening ("it's only a bathroom vent"). Stepped crack up from both corners. *Fix: every opening gets a lintel.*
7. **Lintel band discontinuous** — five separate lintels called a band. No seismic benefit. *Fix: one head level, continuous band, corner laps.*
8. **Opening within 450 mm of a corner.** Corner splits in an earthquake. *Fix: §11.1; move it.*
9. **Pier between two windows < 450 mm.** Crushes under the two lintel reactions. *Fix: merge the openings or widen the pier.*
10. **Wide opening with no tie-columns** — a 2.7 m opening bearing directly on unconfined masonry. *Fix: §6, tie-columns to foundation.*
11. **Sliding door drawn into a shear wall** with no compensation. Lateral system quietly deleted. *Fix: §13.*
12. **Short-column condition** from a half-height infill beside a ribbon window. Brittle column shear failure. *Fix: §11.3.*
13. **No cavity tray / DPC above the lintel** in a cavity wall. Permanent damp patch above the window. *Fix: §12.3.*
14. **Weep holes plastered over** by a finishing crew who thought they were defects. Cavity fills with water. *Fix: mark them; brief the crew; inspect after plaster.*
15. **Sill with no drip groove or no outward slope.** Water tracks back; permanent staining and damp below every window. *Fix: §7.1.*
16. **Ungalvanized steel angle lintel in a humid climate.** Rust jacking lifts the brick course. *Fix: hot-dip galvanize; 6 mm minimum thickness.*
17. **Arch built without an abutment**, or next to a corner. Thrust pushes the wall out. *Fix: §10.1.*
18. **Arch centring struck too early.** Crown cracks. *Fix: 7-14 days, ease gradually.*
19. **Loading a fresh lintel** — a mason building 2 m of wall above a lintel cast that morning. *Fix: 24 h minimum, 1 m maximum on day one.*
20. **Electrical chase cut vertically through a jamb pier** after construction. *Fix: coordinate MEP before masonry; §14.*
21. **Widening an opening "by 6 inches" on site** without telling anyone. Bearing lost, lintel now too short. *Fix: openings are structural dimensions; no site changes.*
22. **Corner window in load-bearing masonry.** Removes the corner — the most important part of a masonry box. *Fix: don't; or put a real RC column at the corner.*
23. **Cutting a new opening in an existing wall without propping.** See §16.
24. **Applying a masonry-pier bearing-length number to a beam framing into an RC column.** The two are different checks (§3.4/§6.3) — carrying the masonry number forward under-informs the real column/joint design. *Fix: re-derive from column and beam-column joint design, not the bearing formula.*

---

## Section 16: Cutting a New Opening in an Existing Wall

**This section is written to be handed to a licensed engineer, not executed from a chat message.** State the licensing and temporary-works requirement every single time this comes up.

### 16.1 Assessment before anything

- [ ] Is the wall load-bearing? Check what runs above and perpendicular: slab span direction, joists, beams, roof, the wall above on the next floor.
- [ ] Is it a shear wall / part of the lateral system? (§13 — this is the question everyone forgets)
- [ ] What is above the proposed opening within 0.866 × the proposed span? Any beam bearing, slab edge, stair landing, water tank?
- [ ] Wall material, thickness, mortar condition, existing cracks, any prior openings infilled.
- [ ] Existing services in the wall — electrical, gas, water, drainage.
- [ ] Foundation under the new jambs — the two new piers will carry more load than the wall did; can the footing take it?
- [ ] Party wall / neighbour / byelaw consent.

### 16.2 Sequence (engineer-designed temporary works)

```
1. Engineer designs: new lintel/beam, new jamb piers or columns, padstones,
   AND the temporary propping ("needling") scheme.
2. Install propping to BOTH faces of the wall, on a spread load-bearing base,
   at the spacing the temporary works design specifies.
3. Cut and install NEEDLES (steel or timber) through the wall above the
   proposed head level, supported on props both sides. Wedge them tight so
   the wall's load transfers to the props BEFORE anything is removed.
4. Cut the opening for the lintel/beam only — a slot, not the full opening.
5. Install the new lintel/beam with full designed bearing, on fresh padstones,
   fully dry-packed/grouted tight to the masonry above (this is critical —
   a gap means the wall settles onto the beam later and cracks).
6. Allow the grout/mortar to gain strength (typically 7 days).
7. Remove the needles, make good the needle holes.
8. Only now remove the masonry below the new lintel to form the opening.
9. Form the jambs, install padstones/tie-columns, make good.
10. Remove props gradually.
```

### 16.3 The three things that go wrong

1. **Removing the wall before the beam is in** — the classic collapse.
2. **Not dry-packing the gap** above the new beam. The wall drops 5-10 mm onto it later and every finish above cracks.
3. **Ignoring the foundation.** The new jamb piers concentrate what was a distributed wall load into two points. On a strip footing this can punch or settle.

---

## Section 17: FreeCAD Modelling Defaults for Openings

Use with `architecture-freecad-bim` — openings must be **live parametric Subtractions** on the `Arch Wall`, never a frozen boolean cut, so widths can be changed when the engineer's check comes back.

| Parameter | Default | Note |
|---|---|---|
| Door opening (room) | 900 × 2100 mm | `Arch Door`, IfcDoor |
| Door opening (main) | 1050 × 2100 mm | |
| Door opening (bath/store) | 750 × 2100 mm | Flag the accessibility failure |
| Window opening (room) | 1200 × 1350 mm, sill 900 | `Arch Window`, IfcWindow |
| Window (drawing room) | 1800 × 1500 mm, sill 750 | |
| Head level (all openings, per storey) | **2100 mm** (or 2250 where windows are taller) | One level — this is what makes the band real |
| Lintel | model as a distinct `Arch Structure`, IfcBeam | b = wall thickness, D per §3.3, **length = clear span + 2 × bearing** |
| Lintel band | one continuous `Arch Structure` around the storey | 230 × 150; model it, or nobody builds it |
| Sill | 40 mm, projecting 50 mm, sloped 1:10 | Model the projection — it changes the elevation |
| Chajja | 600 mm projection, 75 mm at root | Separate object, monolithic in reality, coloured as concrete |
| Tie-column at jambs of openings > 1.2 m | 230 × 230, full height to plinth | **Separate object from the wall** |
| Pier width beside an opening | ≥ 600 mm | Measure it in the model — do not eyeball |
| Arch (decorative) | model as a separate object from the structural lintel | so it is obviously non-load-bearing |
| Cavity tray / DPC | not modelled geometrically | Note it in the model README / a 2D detail |

**Modelling discipline for openings:**
1. **Model every lintel.** The lintel is what makes the wall cut correct and what makes the quantities real. A wall with a hole and no lintel is a drawing, not a model.
2. **Model tie-columns beside wide openings as separate objects**, so the load-path audit can be run visually and so they get counted in the BOQ.
3. **Run a pier-width sweep** on every floor: for each wall, list opening widths and the remaining pier widths. Anything under 600 mm is a finding. This is a 20-line Python loop in the FreeCAD console and it catches the majority of opening errors.
4. **Run an opening-ratio check per wall:** Σ opening widths / wall length, against §11.1. Report per wall, per direction, per storey.
5. **Check the relief triangle is clear:** for each opening, is there a beam, slab edge or column bearing within a 0.866 L high triangle above it? If yes, flag that lintel as "arching void — design for full load".
6. **Never model an opening as a hole with no head member.** If the head is a frame beam, model the frame beam.
7. Annotate the model or its README with the **assumed head level, arching assumption, and which openings are engineer-designed beams rather than table lintels**, so nobody downstream inherits invisible assumptions.
8. If FEM is run (`mcp__freecad__run_fem_analysis`), remember a lintel modelled without its bearing length is a lintel with the wrong span. Model the full member.

---

## Section 18: Worked Example D — Full Opening Schedule, 10-Marla G+1, Lahore

Ground floor, 230 mm burnt-brick confined masonry, M20/Fe415, Zone 2A, head level standardised at 2100 mm, lintel band 230 × 150 continuous.

| Ref | Opening | Clear span | Arching? | Load case | Lintel / header | Bearing | Steel | Notes |
|---|---|---|---|---|---|---|---|---|
| D1 | Main door | 1050 | Yes (2.6 m above) | wall only | 230 × 150 | 230 | 2 – 12 btm | in band |
| D2-D5 | Room doors | 900 | Yes | wall only | 230 × 150 | 230 | 2 – 10 btm | in band |
| D6-D7 | Bath doors | 750 | Yes | wall only | 230 × 115 | 150 | 2 – 10 btm | in band |
| W1-W4 | Room windows | 1200 | Yes | wall only | 230 × 150 | 230 | 2 – 12 btm | + chajja 600 |
| W5 | Drawing rm window | 1800 | Yes | wall only | 230 × 200 | 230 | 3 – 12 btm, 2 – 10 top | + chajja 600, closed stirrups |
| W6 | Kitchen window | 1200 | Yes | wall only | 230 × 150 | 230 | 2 – 12 btm | sill 1200 |
| W7 | Bath window | 600 | Yes | wall only | 230 × 115 | 150 | 2 – 10 btm | sill 1800 |
| **P1** | **Car porch** | **3600** | **No** (slab at 3075) | wall + slab | **300 × 530 beam** | **RC columns 300 × 380** | 5 – 16 btm, 3 – 16 top, 10 @ 125 | portal frame; torsion from 2.1 m porch cantilever; own pad footings |
| **S1** | **Sliding door to lawn** | **3000** | **No** | wall + slab | **230 × 460 beam** | **RC columns 300²** (column-frame design, not a bearing-length figure — see §6.3) | 4 – 16 btm, 3 – 16 top, 8 @ 125 | **§13 check: rear wall bracing recomputed** |
| **W8** | **Picture window** | **2400** | Truncated (0.98 m) | wall strip only | **230 × 300 beam** | 250 + tie-columns 230² | 3 – 16 btm, 2 – 12 top, 8 @ 125 | pier each side 900 mm — at limit |

Findings that came out of building this schedule (this is the value of doing it):

1. **P1 and S1 are not lintels.** They are portal frames with their own columns and footings. Two extra pad footings appeared in the foundation plan.
2. **The rear wall lost 3.0 m of its 7.2 m length** to S1. Perforated-method capacity of that line dropped to roughly a third. Compensation adopted: the two flanking piers were converted to confined piers with 230 × 230 tie-columns and the return wall on the east was lengthened by 900 mm.
3. **W8's piers are 900 mm** — above the 600 mm limit but not comfortable. Tie-columns added both sides.
4. **Head level standardisation to 2100 mm** allowed one continuous 230 × 150 lintel band around the entire storey, absorbing D1-D7, W1-W4, W6, W7 and the head of S1. Only P1 and W5's chajja sit outside it. That single decision was worth more, seismically, than every individual lintel in the table.
5. **Every external opening got a chajja and a sill drip.** Cost: negligible. Damp complaints avoided: all of them.

---

## Section 19: Handoff and Coordination Checklist

### What to give the engineer

- [ ] Floor plans with **every opening dimensioned**: width, height, sill, head, and the wall it sits in
- [ ] The **head level** decision per storey
- [ ] What is above each opening: slab span direction, beam bearings, upper-floor openings, water tank, stair landing
- [ ] Wall thicknesses and materials, with the intended masonry unit and mortar mix
- [ ] Which walls are intended as **bracing/shear walls** in each direction
- [ ] Any opening the client considers non-negotiable (the drawing-room glass wall, the porch width)
- [ ] Confirmed seismic zone, and the site's basic wind speed
- [ ] Whether any arch is intended to be structural or decorative
- [ ] For a retrofit: existing wall condition survey, existing crack map, prior alterations

### Run before the model is called "done"

- [ ] Every opening has a lintel or a designated header beam modelled — no exceptions
- [ ] Bearing = greatest of 150 / depth / span-12 **for masonry-pier bearings only**; where the support is an RC column, that figure is replaced by a column/beam-column-joint design (§6.3) — total lintel length = span + 2 × bearing applies to the masonry case
- [ ] Bar extension past every opening face ≥ 600 mm **or Ld for the actual bar size** (§5.3)
- [ ] Arching action validated per opening; every void case (§2.2) redesigned for full load
- [ ] Head level standardised; lintel band continuous and turning every corner
- [ ] Every pier beside an opening ≥ 600 mm (450 mm absolute); anything below is confined or discounted
- [ ] No opening within 600 mm of an inside corner
- [ ] Σ opening widths / wall length checked against §11.1 for every wall, every storey
- [ ] Openings > 1.2 m have tie-columns; openings > 2.1 m have designed beams; openings > 3.0 m have real columns and footings
- [ ] Wall density recomputed **after** the final opening layout, both directions, every storey
- [ ] Every large opening in a braced line has an explicit compensation from §13.5, written down
- [ ] No short-column / captive-column condition created by a partial-height infill
- [ ] Every cantilever chajja: steel on top, monolithic, drip, closed stirrups in the lintel
- [ ] Every external opening: sill slope ≥ 1:10, projection ≥ 50 mm, drip groove, sill DPC with end dams
- [ ] Cavity-wall openings: tray above the lintel, weeps ≤ 838 mm o.c. in the course above, end dams
- [ ] Steel lintels galvanized, ≥ 6 mm, bearing ≥ 100 mm, deflection L/600
- [ ] Arches: abutment provided and sized, thrust stated, centring/strike programme noted; decorative arches labelled as such
- [ ] MEP coordination done — no chases in piers, AC sleeves have their own lintels
- [ ] **Output labelled: "Preliminary — requires design and stamp by a PEC-registered structural engineer, and local authority approval, before construction."**

---

## Section 20: Known Gaps in This Skill (state these when relevant)

1. **Building Code of Pakistan clause text is not reproduced verbatim.** BCP-SP 2007 §9.9.8 (Lintels) and BCP 2021 Chapter 21 (Masonry) govern Pakistani practice and their exact clause numbers, minimum sections and bearing requirements must be read from the source PDFs (urbanunit.gov.pk for BCP 2007; pec.org.pk for the BCP 2021 draft) before citing them in any submission. The public code portal returned 403 at the time of research. **This also means the §3.3 RCC lintel schedule is a paraphrased working table, not a BCP-SP 2007 transcription** — flagged inline at §3.3.
2. **IS 4326 Table 4 opening-ratio values and Table 5 band-steel values are paraphrased** from commonly cited secondary sources, not transcribed from the standard. Verify against the actual standard before use. The category (A-E) definitions in particular must come from the source. **The §11.1 table carries this same flag inline.**
3. **The AWC SDPWS 2021 Co equation and Table 4.3.3.5 values are reconstructed** from the Sugiyama empirical basis (`F/F0 = r/(3−2r)`). The form used in §13.2 is internally consistent and the magnitude of the capacity penalty is reliable, but the exact SDPWS Eq. 4.3-5 expression and its tabulated Co values must be checked against the standard before design use. **Flagged inline at the top of §13.2.**
4. **BIA Technical Note 31B steel angle span tables are not reproduced.** The angle sizes in §8.1 are indicative practice for a typical veneer height. The real selection depends on veneer height, whether a floor bears, and the L/600 + 0.3 in deflection cap. Read Tech Note 31B. **Flagged inline at the top of §8.1.**
5. **The jack-arch skewback rule** (1/2 in per ft of span per ft of arch depth) is quoted as commonly cited; confirm against BIA Technical Notes 31 and 31A before setting out a real jack arch.
6. **No masonry lintel design in reinforced concrete masonry (grouted bond-beam lintels)** is included in table form. CMHA TEK/TR 91B is the authority for concrete masonry lintels and has full capacity tables — use it directly for CMU construction.
7. **IRC 2021 Table R602.7(1) is presented as a single reduced column** (roof and ceiling load only, narrow building). The real table varies by building width, snow load, and number of storeys carried. Read the full table for any real light-frame work. **Flagged inline at the top of §9.1, with an explicit warning against applying it to a floor-loaded header.**
8. **No fire-resistance rating data for lintels or headers** is included. If a rated separation crosses an opening, the head member's rating and any required protection must come from the local code.
9. **No thermal-bridging or U-value analysis of lintel details** is included. A concrete or steel lintel bridging an insulated wall is a real thermal defect in cold-climate northern Pakistan; get a thermal detail if the project has an energy target.
10. **No sound-rating treatment of openings** is included.
11. **All reinforcement quantities in this skill are indicative for feel and quantity estimating only.** No table here is a bar bending schedule. See `architecture-concrete-reinforcement-detailing` for detailing rules, and an engineer for the actual schedule.
12. **Every "designed beam" row in every table is a placeholder for an engineer's design**, not a design. The sections shown are pre-sizing to make a model plausible and a BOQ approximately right.
13. **The masonry-pier bearing-length rule (§3.4) does not extend to beams framing into RC columns.** Once real RC columns are the support (§6, wide openings), the governing checks are column axial/moment capacity, bar development length into the column core, and beam-column joint shear — not the bearing-length formula. §6.3 shows the reconciliation explicitly; do not carry a bearing-length number forward as if it sized a column.
