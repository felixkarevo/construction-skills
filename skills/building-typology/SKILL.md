---
name: building-typology
description: >
  Select and configure the right building form for a DACH site: Einfamilienhaus
  (detached), Doppelhaushälfte/Doppelhaus, Reihenhaus/Zeile, Geschosswohnungsbau
  (MFH — Zeile, offener Block, Blockrand, Punkt, Staffel, Hochhaus), Maisonette
  and Atelier, Atrium-/Hofhaus, mixed-use Gewerbe+Wohnen stacking. Covers the
  typological decision ladder (household, budget, plot geometry, B-Plan envelope
  GRZ/GFZ/Geschossigkeit/Bauweise, density target), plan-depth and daylight logic
  (usable depth ≈ 2× room height, limit 3×, single- vs dual-aspect, courtyard/
  Lichthof rules), orientation strategies by type (row = one-sided garden aspect,
  MFH = orientation mix, west-overheat discipline), compactness: α = A/V bands
  per type and the GEG/EnEV H'T type ladder (0.40/0.50/0.45/0.65), DIN V 18599
  typology-dependent gains (EFH 45 vs MFH 90 Wh/m²d; a_tb 0.25 vs 0.15), unit
  mix & circulation theory (stair cores per units, second escape route by
  Gebäudeklasse, Aufzug triggers, corridor economics, NTG 0.70–0.84, skip-stop
  maisonettes), construction-system fit per type (Mauerwerk+WDVS, monolithisch,
  Kalksandstein+Vormauer cross-wall, Holztafel, Stahlbeton-Skelett, Fertigteile,
  CLT/Holzhybrid, Aufstockung) cross-referencing masonry-construction /
  timber-steel-design / structural-systems, expansion & later-floor reserves,
  privacy/daylight by typology, density spectrum (10→250+ WE/ha) with land-take
  and sealing consequences, a worked decision tree, anti-pattern catalogue and
  pre-handoff checklist. Market figures are T4/T5 — verify locally and by date;
  legal numbers are MBO/LBO patterns — the Landesbauordnung and B-Plan govern.
---

# Building Typology — Choosing & Configuring the Building Form (DACH)

Typology is the decision that comes *after* the site is known and *before* room sizing begins. Get it wrong and no amount of good plan-making rescues the project: a 14 m-wide plot laid out as a free-standing house with 3 m side setbacks produces a windowless side face; a 45 m-deep interior-block lot laid out as a single bar produces flats nobody lets; a 1,200 m² urban infill site built as one EFH surrenders most of the legally permitted floor area. In Germany the typology question is strongly determined — but by a different pre-quantisation than the Anglo-American literature assumes: the **Bebauungsplan (B-Plan)** fixes the envelope (GRZ, GFZ, Zahl der Vollgeschosse, Bauweise offen/geschlossen, Wandhöhe/roof geometry, sometimes unit caps and street-facing wall positions), the **Landesbauordnung (LBO)** fixes the fire and circulation consequences of whatever you choose (Gebäudeklasse), and the **plot geometry** fixes the plan depth and therefore the daylight. This skill encodes that ladder: plot + plan + household + budget + density target → 2–3 plausible archetypes with construction-system recommendations — then hands every candidate back to be re-tested against the actual B-Plan and LBO before anything is drawn.

This is the **typology-selection layer**. It deliberately does **not** re-derive room minimums, stair geometry, Abstandsflächen law, fire-compartment sizing or energy-balance procedures — those are cross-referenced, not duplicated.

## Reality Check — Liability & Approvals

**This skill produces design aids, typological envelopes and calculation guidance for planning and 3D modelling ONLY.**

- Nothing in this file is a construction document. No typology table, floor plate, unit mix, wall thickness, span limit or cost band printed here is buildable as-is.
- Any design intended for a real, occupied building requires **Bauvorlageberechtigung** (Entwurfsverfasser authorised to submit, Land-dependent), a **Standsicherheitsnachweis** by a qualified engineer / Nachweisberechtigter, a **Brandschutznachweis** per the Landesbauordnung, and a **GEG energy proof** by authorised Fachunternehmer. Their current text overrides every number printed here.
- The design **MUST pass the Baugenehmigungsverfahren of the local Bauaufsicht** — and any B-Plan, Gestaltungssatzung or Erhaltungssatzung binds before you draw. *Their schedule governs; this file is a decision aid.*
- Structural guidance here (wall logic vs grid logic, span envelopes, the EN 1996-3 simplified-design envelope) is a **preliminary plausibility check that a typology fits its site and budget**, not a structural design. Member sizing, reinforcement, seismic and foundation design belong to `masonry-construction`, `timber-steel-design`, `structural-systems`, `concrete-detailing`, `geotechnics-foundations` and ultimately the engineer of record.
- **Never present model output or these calculations as permit-ready, approved or buildable** without that human sign-off. If the user appears to treat the output as final — ordering materials, briefing a contractor, "so we can submit" — say so unprompted at the top of the reply: *"This is a typology and planning study, not a stamped submission. A bauvorlageberechtigter Entwurfsverfasser and a Standsicherheitsnachweis-Prüfer must review it, and it needs a Baugenehmigung before anyone breaks ground."*
- Cost figures are dated 2026 market bands, not quotations. They move with labour and material indices and by region. Never present them as a budget without a dated caveat.

---

## Section 0: How to Use This Skill

### 0.1 Relationship to the sibling skills

| Question | Skill that owns it |
|---|---|
| *"Which building form? How many units? What floor plate? What core? What unit mix? What density?"* | **This skill** |
| *"What wall thickness, what masonry unit, what two-leaf wall?"* | `masonry-construction` |
| *"Timber or steel members, CLT layout, connections, charring?"* | `timber-steel-design` |
| *"What grid, what span, wall vs skeleton, lateral system?"* | `structural-systems`, `structural-analysis` |
| *"Escape routes, second stair, Hochhaus rules, fire compartments?"* | `fire-protection-building` |
| *"Party-wall R'w, impact sound L'n,w, VDI 4100 classes?"* | `building-acoustics` |
| *"α = A/V, U-values, H'T, overheating Kh/a, airtightness n50?"* | `building-physics-thermal-moisture` |
| *"Window sizes, g-value, shading, rescue openings?"* | `openings-windows-doors` |
| *"Flat vs pitched roof, terrace waterproofing by storey count?"* | `roofing-waterproofing` |
| *"Basement/TG viability, groundwater, bearing?"* | `geotechnics-foundations` |
| *"Material GWP, circularity, system life cycles?"* | `building-materials` |
| *"Rebar, slabs, punching shear?"* | `concrete-detailing` |

**Routing rule:** if the question is *"which building form"*, start here. If it is *"is this buildable/approvable as drawn"*, hand to the code/calculation skills. Every typology decision made here must be re-tested against the actual B-Plan and LBO envelope.

### 0.2 Evidentiary tiers

Never present a T4/T5 number as law; never present a T1 *pattern* as the current text of a specific Bundesland.

| Tier | Label | Meaning | Status |
|---|---|---|---|
| **T1** | Legally binding | Landesbauordnung, B-Plan/FNP (BauNVO), GEG, DIN embedded in the Technische Baubestimmung | Enforceable — approval fails without it. **Edition varies by Land — VERIFY.** |
| **T2** | Cited standard | DIN not introduced as law (DIN 18040-2, DIN 18065, DIN 18017-3, VDI 4100), DIN V 18599/4108-2 methods, Eurocode envelopes (EN 1996-3 limits) | Contract/de-facto reference; not automatically permit law |
| **T3** | International baseline | Unit-mix and core theory (skip-stop, scissor, NTG logic), typological exemplars | Rigor benchmark |
| **T4** | Market / built practice (DACH) | Wohnflächen bands, room programs, cost bands, Stellplatz expectations | No legal force — *this is what clients and investors actually expect*. Re-verify by region and date. |
| **T5** | Research-derived figures | Density/A:B comparisons, internal-gain parameters, embodied-carbon orders of magnitude | Indicative study data; VERIFY before quoting |

Typology work lives overwhelmingly in **T2/T4**. That is not a weakness — household shapes, ownership models and market unit mixes are cultural facts, and T4 is the correct evidence class for them. State the tier when quoting.

### 0.3 The five questions to answer before selecting a typology

Never propose a typology without all five. If one is unknown, say which decisions are blocked on it.

1. **Plot area *and* dimensions** — width governs Bauweise (free-standing needs ≈14–16 m once two 3 m Abstandsflächen are subtracted from a ~6 m room depth; see 2.3), depth governs whether flats can be dual-aspect without a courtyard, and both govern the Abstandsflächen outcome. Also: sun orientation, slope, access situation, Altlasten (contaminated-land) flag, nearby noise source.
2. **Zoning** — area type per BauNVO (WA, WR, ALG, M, MI, CM, MD…), and the B-Plan text: **GRZ, GFZ, number of Vollgeschosse, offene vs geschlossene Bauweise, Wandhöhe / roof-pitch band (WR), straßenseitige Bauflucht, possibly unit caps**. Where there is no B-Plan, §34 BauGB (innerer Zusammenhang) governs — in practice "match the neighbours", which is far less predictable. This is a **T1 gate: read the actual B-Plan, never infer it.**
3. **Occupancy model** — single family? family + rented Einliegerwohnung? two related households with parity (generationenwohnen)? pure rental? Eigentumswohnanlage (WEG) to sell? Genossenschaft / Baugruppe? mixed-use ground floor?
4. **Budget class** — and *which* cost groups: KG 300–400 shell only vs full KG 300–600 incl. TG and Außenanlagen drives typology as hard as the plot. A site that could legally carry 6 WE is not an argument for building 6 WE on a self-builder budget.
5. **Rooms/bedrooms now and in 10 years** — plus the accessibility question (altersgerecht? rollstuhlgerecht share? Aufzug yes/no). The single strongest predictor of whether a plot band works is the required room count, the same question in 10 years is what kills "cheapest-fit" plans later.

---

## Section 1: Typology Selection Decision Tree

```
START: plot dimensions + B-Plan envelope + occupancy + budget known?
  ├─ NO  → ask the five questions (0.3). Do not guess.
  └─ YES ↓

One household, owner-occupied?
  ├─ Plot width < 12–14 m, or GRZ ≥ 0.25 on a small lot
  │     → DOPPELHAUSHÄLFTE (DHH) — free-standing EFH is geometrically
  │       impossible (two side setbacks + full room depth won't fit).
  │       Twin plot → DOPPELHAUS: two mirrored halves, one shared wall.
  ├─ Plot 350–600 m², WA/WR, offene Bauweise, GFZ ≤ 0.4–0.6
  │     → EINFAMILIENHAUS, 1.5–2 Vollgeschosse + DG + Keller
  │       Structure: Mauerwerk + WDVS / monolithic / Holztafel (Section 11)
  │       Program: 4–5 Zi ≈ 130–160 m² WFL + reserved DG/KG expansion
  │       Do NOT attempt: a 190 m² footprint on a 400 m² plot — the GRZ says no
  ├─ Plot 600–1,000 m², or B-Plan forces attached/at-line
  │     → REIHENHAUS (own build on a 5.5–7 m parcel), EFH + Einlieger,
  │       or two-household DOPPELHAUS / Gruppenhaus
  └─ Plot > 1,000 m², large household, or compound
        → EFH as pavilion/L-bar, land as the asset — but the legal envelope
          (GRZ/GFZ; §35 Außenbereich at the fringe!) is checked FIRST, never
          assumed. Design below the legal maximum on purpose where the garden
          is the product.

Rental / investment / institutional client?
  ├─ Density target ≥ 60 WE/ha, or urban plot > 800 m² with GFZ ≥ 1.2
  │     → GESCHOSSWOHNUNGSBAU 3–5 storeys. Now the CORE, the escape logic and
  │        the unit mix — not the room program — are the governing design
  │        problem (Sections 5, 12).
  ├─ Interior-block lot (Baulücke), plot depth > 25 m
  │     → HOF-/BLOCKRAND type: wings wrap a courtyard; the courtyard is the
  │        daylight machine, not decoration (Section 6).
  ├─ Gewerbe EG + Wohnen above, or M/MI area type
  │     → MIXED-USE stack (Section 7): own cores per use, acoustic buffers,
  │        system-change floor.
  ├─ Very high density target (>120 WE/ha) or extreme land price
  │     → Hochhaus / Staffelbau / townhouse-hybrid — check the LBO Hochhaus
  │        rules (Rettungstreppe, FeuerwehrAufzug) before falling in love.
  └─ Small urban plot, senior/student product
        → compact MFH 3–4 storeys; Aufzug required by MBO pattern above
          2 WE (VERIFY Land) — design it in, never onto.

Baugruppe / cooperative?
  └─ Geschosswohnungsbau or Reihenhaus-Ensemble with cluster commons
     (Section 8): private WFL −10–15 m²/WE, shared rooms added; unit mix and
     stair count are negotiation objects — design them as such.
```

### 1.1 Overriding constraints that beat the tree

Apply these *after* the tree and let them override it:

| Constraint | Override |
|---|---|
| B-Plan "geschlossene Bauweise" / fixed Bauflucht | Free-standing branch is dead on that strip — DHH/row/Zeile only, even if the plot is wide. |
| B-Plan unit cap (e.g. WA "max. 2 WE") | The MFH yield branch is dead regardless of plot size. Fall back to EFH + Einlieger. |
| No B-Plan (§34 BauGB) | Precedent survey of the block becomes your B-Plan — typology is borrowed, not chosen. Expect the Nachbarkonsens fight over anything bigger than the street norm. |
| Altlasten-/Verdachtsfläche (contaminated-land register) | Basement/TG = soil-contact works = possible Sanierungspflicht. Route to `geotechnics-foundations` **before** committing the program to underground space. |
| High groundwater | White/green tanking decisions dominate cost; urban Zeile without TG loses Stellplätze — check the municipal Stellplatzvo first, then the water table. |
| Noise source (road/rail/flight) at/above the area type's TA-Lärm day limit | Living rooms cannot face the source → orientation strategy flips (Section 13), courtyard typologies strengthen. |
| Slope > ~10% | Split-level / hanggeschoss types; retaining structures often cost more than the floors they enable — model the slope before choosing or rejecting the basement typology. |
| Denkmalschutz / Erhaltungssatzung | Form, roof and openings constrained; extension and Aufstockung become case-by-case conversations. |
| Feuerwehrzufahrt / access widths (LBO + fire-service requirements) | Building position and TG ramp geometry must clear this before unit counts are fixed. |
| Client budget below the typology's *quality floor* (~€1,900/m² for a 4–5-storey rental product incl. Aufzug + TG) | Do not propose a typology whose standard the budget cannot carry. Build less area well, or phase — a half-finished MFH is worth less than a full EFH. |

---

## Section 2: The German Site Envelope — GRZ, GFZ, Bauweise, Abstandsflächen

### 2.1 The ladder — plot band → conventional typology (T4)

"Buildable" below assumes a typical WR/WA single-family B-Plan (GRZ 0.2, GFZ 0.4, II-Vollgeschosse + DG allowed) or a typical MI urban plan (GFZ 1.4–2.4). **These are patterns; the B-Plan is the truth.**

| Plot | Area (m²) | Typical width × depth (m) | Conventional typology | Storeys | WE | Buildable WFL (m²) | Structure |
|---|---|---|---|---|---|---|---|
| Row parcel | 180–350 | 5.5–7 × 16–25 | Reihenhaus (attached) | 2 + DG | 1 | 100–140 | Mauerwerk EG + OG, or Holztafel on KG slab |
| DHH parcel | 300–500 | 10–14 × 20–25 | Doppelhaushälfte / Doppelhaus | 1.5–2 | 1 (+Einlieger) | 110–160 | as above |
| Standard EFH plot | 400–700 | 16–20 × 25–35 | Freistehendes EFH | 1.5–2 + Keller | 1–2 | 130–190 | Mauerwerk+WDVS / monolith / Holztafel |
| Large / corner plot | 700–1,200 | 25–35 × 28–45 | EFH + Einlieger, two houses, or Gruppenhaus | 2–2.5 | 2–3 | 200–320 | + Keller; Skelett where open floors wanted |
| Urban infill (Baulücke) | 800–2,500 | 15–30 × 25–50 | Geschosswohnungsbau Zeile / offener Block | 3–5 | 8–30 | 50–95 m²/WE avg | KS+Vormauer cross-wall / Stahlbeton / Holzhybrid |
| Interior-block lot | 1,500–4,000 | 25–45 × 35–60 | Hof-/Blockrandtype with courtyard | 3–5 | 15–50 | as above | cross-wall or skeleton+infill |
| Development parcel | 2,500–10,000 | ensemble | Wohnanlage (Zeilen/Höfe) | 2–5 | 25–100 | mixed | series systems; Fertigteile at the top end |

**The width trap:** a "free-standing house" on a 12 m-wide plot is a myth — two Abstandsflächen (pattern 0.4×H, min 3 m per side; some Länder 0.5×H) plus a 5.5–6.5 m room band need ≈14–16 m width *before* any garden ambition. **Always confirm the plot in metres, never from "it's 500 m²".** A 500 m² parcel that is 10 × 50 is a row-house site, not an EFH site — and "1,200 m²" on a 15 m frontage in a closed-development strip is a Zeile segment, not a compound.

### 2.2 GRZ/GFZ arithmetic — the footprint ladder

- **GRZ** (Grundflächenzahl) caps the *footprint* incl. garages, carports and hard-sealed terraces (per §19/§21a BauNVO with local inclusion rules — VERIFY what your municipality counts).
- **GFZ** caps *total floor area of full storeys*; DG is typically excluded (the classic German loophole). GRZ and GFZ bind **jointly**: GRZ caps the footprint, GFZ caps the total. A generous GFZ is useless if GRZ caps your footprint and the height cap limits your storeys.

```
Worked check — 600 m² plot, WR zone, GRZ 0.2, GFZ 0.4, II VG:
  Allowed footprint           600 × 0.2  = 120 m²
  Allowed total floor area    600 × 0.4  = 240 m²
  Desired EFH: 120 EG + 120 OG           = 240 ✓ GFZ exactly at limit
  + carport 20 m² in GRZ                 → 140 m² footprint ✗ OVER by 20
  → shrink the house to ~10.5 × 9.5, or move the carport into the
    building volume (Garage im VG = footprint already counted), or
    accept a 1.5-storey bar + full DG.
Conclusion to state to clients: the canonical German single-family form
"2 Vollgeschosse + DG + Keller" exists because GFZ limits the plates,
GRZ limits the footprint, and the DG is the reserve nobody can take away.
```

When a client or agent quotes an "already approved area", ask **which of GRZ, GFZ or overbaute Fläche it counts** before designing to it. **Never quietly design to a number the B-Plan does not permit** — it fails at approval, not on site.

### 2.3 Abstandsflächen and the geometry they impose (T1 — patterns; LBO governs)

MBO pattern §6: depth of Abstandsfläche = **0.4 × wall height H, minimum 3.0 m**, from all window-bearing exterior walls; gable walls without openings relax (often to 0.25×H min 3 m); in geschlossene/satzungsgemäße Grenzbebauung the sides collapse to the boundary; the front-yard line is a B-Plan parameter, not your choice; some Länder (e.g. BW, Berlin) use 0.5×H or different minima — **VERIFY the actual LBO.**

Typological consequences that *always* hold regardless of the Land:
- Free-standing EFH → plot width ≈ room band + ~6 m of setbacks + garden. Width < 14 m → attached or at-line form.
- Attached rows (sides waived) → only front and rear pay setbacks → **depth becomes the scarce resource** → plan depth 10–12 m max for dual aspect, else courtyard.
- Interior-block lots (depth 35–60 m) → the middle 15–20 m of any bar is **unlightable without a Hof or Lichthof** (Section 6).
- The Abstandsfläche is not dead land: it is the fire-service access, the light for the neighbour, and increasingly the climate corridor — plant it, don't parking-strip it.

### 2.4 Honesty note on marketed areas

Developer Wohnfläche claims and net diagnostics measure different things. **Wohnfläche per WoFlV** excludes Keller, counts loggias/balconies at 25–50%, DG at 100/50/0 by head height; **BGF per DIN 277** includes walls and cores. Worked plausibility check for a marketed "Reihenhaus 145 m² Wohnfläche":

```
Parcel 260 m², 5.6 m × ~14 m bebaubar (attached sides)
Footprint 5.6 × 10.2                          ≈ 57 m² WFl
+ OG same                                     ≈ 57 m²
+ DG, knee-wall, counted 0.5–1.0 by height    ≈ 30–55 m²
+ Loggia at 25–50%                            ≈  6 m²
= WoFlV total                                 ≈ 130–155 ✓ plausible
```
…provided the DG is finished near full room height across most of the plate. Ask which counting rules produced any quoted number before designing to it, and state your own convention in writing on every drawing.

---

## Section 3: The Detached House (Einfamilienhaus) — Default Typology

The detached single-family house remains the modal German owner-occupied product. Its typological variables interact tightly: **plot width** governs Bauweise, **plan depth** governs whether rooms are daylit, **coverage** governs how much of that is legally usable.

### 3.1 Three canonical configurations (T4 — universal archetype theory)

| Configuration | Plot width | How it works | Fails when |
|---|---|---|---|
| **Front-entry bar** (entry + working rooms to street, living to garden) | 14–20 m | Single stack EG/OG(+DG); stair band splits front (service) from rear (living); one long section, no corridors doing nothing | Depth > 11–12 m (middle rooms go dark); noisy or overlooked street front |
| **L-/U-wing wrapping the garden side** | 16–25 m | Wings screen wind/noise, create a court-garden microclimate; entry in the notch; each wing one-room-deep and daylit both sides | Footprint inflates against GRZ; inner corners need setback discipline |
| **Courtyard / atrium house** (Section 6.3) | 20 m+ (or any width when depth > ~2× width) | Rooms wrap a central court; every room gets an external *and* a court face | Plot < ~600 m² — the court's minimum useful size exceeds what the plot can spare |

### 3.2 Daylight-depth rule — the plan-quality law of this skill

- A room is usefully daylit from one side up to depth **≈ 2× room height** (2.6 m → ~5.2 m; double-height → ~10 m). The DIN 4108-2 summer-proof convention already treats **3× clear height as the maximum room depth** for the simplified method, and splits façades beyond 6×h into separate zones (T2). Take **2× as the comfort rule, 3× as the hard limit.**
- Therefore: single-loaded houses ≤ ~6 m room band; double-loaded MFH ≤ ~12–13 m total (plus corridor). **Beyond ~14 m plan depth without an intermediate light source (Hof, Lichtriss, Galerie) the middle of the plan is artificial-lit living — an anti-pattern, not a style choice** (Section 17).
- North-only living rooms and windowless kitchens are market failures before they are code questions (windowless bad/Küche need mechanical exhaust per DIN 18017-3 — T2; but no Wohnraum without a window lets, sells or lives well).

### 3.3 Program by household (T4, DACH market norms — VERIFY region/date)

| Space | 2-pers EFH | 4-pers EFH | EFH + Einlieger | Notes |
|---|---|---|---|---|
| Wohnfläche | 90–120 m² | 130–160 m² | +45–65 m² | German new EFH median ≈ 140–150 m² |
| Wohnen/Essen/Kochen | 35–45 | 50–65 | own kitchen per unit | open plan only with defined zones |
| Sleeping/study rooms | 2–3 | 3–4 | +1 | Zimmer-counting trap — see 4.1 |
| Bathrooms | 1 Wannen + 1 DU | 2 | each unit own DU | 4 Zi: 2. Bad is a resale argument |
| Gäste-WC | 1 | 1 | — | ground floor |
| HWR/Abstell | 6–10 | 10–16 | Keller carries | HWR beside Keller/TGL stair |
| Car | 1.5–2 | 2 | +1 | counts into GRZ |
| Keller | standard | standard | standard | near-mandatory DACH norm: utility + storage + reserve (Sec. 14) |

Bedroom-count reality check (T4): clients routinely ask for one more room than the plot band conventionally carries. The honest response is the trade, not a refusal: *"Five full-height rooms at 160 m² BGF is possible with a compressed DG, but each drops to ~11 m² with a sloped ceiling and the second Bad disappears. On the larger plate you get five at comfortable size with the lounge intact. Which matters more?"*

### 3.4 Compactness — the α = A/V law and the energy ladder

The **α ratio (transferring envelope area A / heated volume V)** is the single strongest cost-and-energy predictor by type. The bands below are **derived geometric diagnostics, not a standard** — use them to compare *your own* options, never as an industry citation:

| Typology | α ≈ A/V [1/m] | Envelope/floor-area (A/B) | Why |
|---|---|---|---|
| EFH freistehend 1–2 VG | 0.30–0.50 | 80–110% | four free faces + roof |
| Doppelhaushälfte | 0.22–0.32 | 60–85% | one wall lost to pairing |
| Reihenmittelhaus | 0.16–0.24 | 45–65% | two walls lost |
| Zeile 4–5 Gesch. | 0.13–0.19 | 35–55% | height does the rest |
| Offener Block / Punkt | 0.10–0.16 | — | |
| Blockrand (7 Gesch., model) | 0.08–0.13 | **67% in a published Berlin model** | huge floor, modest shell |
| Hochhaus slab | 0.06–0.10 | — | |

Three anchors that encode the same physics:

1. **The GEG/EnEV H'T type ladder** (specific transmission-loss maxima for the Existing-building/extension proof, T1/T2 — VERIFY current annex): free-standing ≤350 m² AN **0.40**; free-standing >350 m² **0.50**; one-side-attached (DHH/RH) **0.45**; all other residential (MFH) **0.65 W/(m²K)**. *The law itself relaxes as the typology compactens — the attached house may run leakier per m² because it has less envelope to be leaky through.*
2. **DIN V 18599-10 residential boundary conditions differ by type** (T2): internal gains **45 Wh/(m²·d) for EFH vs 90 for MFH**; part-heating area factor a_tb **0.25 EFH vs 0.15 MFH**; DHW demand rises as average unit shrinks (Q_w = max[16.5 − 0.05·A_NGF,WE,m; 8.5] kWh/(m²·a)). **A denser type is not only less surface — it runs on its neighbours' heat and gains.** (Consequence for design: MFH party walls and floors transfer real energy; the airtightness layer must be continuous *between* units, not just at the shell.)
3. **Urban-form carbon comparison (T5, single German study — verify):** the same floor area as a 7-storey blockrand (A/B 67%) spread as ten detached 4-storey bars needs **≈121% A/B** — ~80% more envelope = more embodied carbon and more transmission; and low-rise dispersed settlement carries **~+1.4 t CO₂e/person·a commuting** and **7–8× more land sealing** vs the blockrand city. Density is a climate argument before it is a planning one.

**The trade, stated plainly:** compactness improves with attachment and height (good for energy, envelope cost, land) while plan depth and orientation conflicts grow (bad for daylight, single-aspect share, privacy — then costly Lichthöfe/Aufzug/TG). The 3–5-storey Zeile/Block at 12–14 m depth with dual-aspect units is the classic sweet spot of German Wohnbaupraxis for exactly this reason.

### 3.5 Worked fit check — does the wish list actually fit the plot?

```
Plot 20 × 32 = 640 m², WR, GRZ 0.2 → 128 m² footprint; GFZ 0.4 → 256 m² plates.
Client wish: Wohnen/Essen/Kochen 55, 4 sleeping rooms, 2 Bäder, HWR, Diele,
             Doppel-Garage, "and a real DG office".
Footprint maths (EG): W/E/K 55 + Diele/HWR 14 + Arbeitszimmer 12 + Gäste-WC 3
                      + Treppenlauf/Wandverlust ≈ 15          = 99 m² ✓ ≤ 128
OG: 3 sleeping rooms (13+12+11) + Flur 8 + Bad 7 + HWR 5
    + internal walls ≈ 12                                  = 68 m² used of
      ~99 m² plate → the spare band becomes the 4th Zi or a family bathroom —
      the plate is adequate, the program is what flexes.
Garage: 2-car closed garage ≈ 35 m² counts into GRZ → 99 + 35 = 134 > 128 ✗
    → drop to a 2-car Carport at the gable (still GRZ if roofed) or shrink
      the plate to 90 m². THE GARAGE, NOT THE BEDROOM, IS WHAT FAILS HERE.
Conclusion to state: 4 Zi + DG office + double garage fits on 640 m² at
GRZ 0.2 only as 2-VG + DG at ~115 m² plates with the garage as Carport;
the marketed "160 m² Wohnen plus GG on 400 m²" brochures are GFZ/GRZ
arithmetic that was never done.
```

---

## Section 4: Doppelhaus & Reihenhaus / Zeile — the Attached Row

### 4.1 Terminology (T4 — get this right before answering)

| Term | German meaning | False-friend / wrong reading |
|---|---|---|
| **Doppelhaushälfte (DHH)** | One half of a twin house; the building type you buy or sell | "duplex" (US) = stacked units — wrong |
| **Doppelhaus** | The whole paired building — one wall, two households | |
| **Reihenmittelhaus (RMH)** | Middle unit of a row: only front + rear faces | end-of-terrace is a different product |
| **Reihenendhaus (REH)** | End unit with one free side face | |
| **Kettenhaus** | Row of staggered/rotated units (A/T/L forms), garden on 2–3 sides | |
| **Hausgruppe** | 3–6 units clustered around a shared threshold space | |
| **Maisonette** | 2-storey unit **within** a larger building, internal stair | "duplex apartment" (US) |
| **Atelier** | Single high-ceiling storey, often gallery; not a maisonette | "studio" ≠ atelier |
| **Einliegerwohnung** | Second, subordinate unit within an EFH | "granny flat" is close; legal independence differs |

**Hard rule 1:** German listings count **"Zimmer" as all rooms except kitchen and sanitary** — a "3-Zimmer-Wohnung" is typically a 2-bedroom. Never translate a bedroom count across without re-asking. **Hard rule 2:** "Doppelhaushälfte" is not a "half house you can extend into a whole" — the second half belongs to someone else, and the shared wall fixes your plan forever. Confirm both before designing.

### 4.2 Row geometry (T4 patterns)

| Metric | Value |
|---|---|
| Unit width | 5.0–6.5 m (RMH); 3-bed comfort 5.5–6.0+; below 5.0 m rooms stop working |
| Built depth | 8–12 m (two bands + stair). Beyond 12 m the middle is dark — split levels or Hof |
| Garden depth | ≥ 10 m behind the house before the neighbour's terrace faces yours — less reads as "green, not private" |
| Storeys | 2 Vollgeschosse + DG, uniform across the row (structural and image coherence) |
| Party wall | One structural principle, two build-ups: single shared wall (twin leaf with separation joint, each house founded/braced independently) or one massive wall. It is a **load path, fire barrier and acoustic object** — coordinate openings, risers and roof drainage across the line before the plans freeze. Target per DIN 4109-1 (T2): Hauswände between row/detached units **R'w ≥ 62 dB where a floor passes through (≥ 59 dB at the lowest storey)**; the *minimum* is the permit level — for higher-standard sale, contract VDI 4100 elevated protection explicitly (case law: minimum ≠ "as agreed") → `building-acoustics` |
| Access | Each unit its own front door; rows served by footpath + private Fahrgasse (pattern ~5.5–6.0 m, per Erschließungssatzung — VERIFY) or by TG; no shared internal stair (that would make it an MFH) |
| Parking | 1 spot per unit minimum (1.5 comfortable): Carport or garage row at the rear, or TG; a car in the front garden kills the row's street character |
| Facade control | Gestaltungssatzung or developer design rules bind materials, roof pitch, fence height |
| Density | 30–70 WE/ha — the rung between the detached suburb and the urban MFH |

### 4.3 Orientation strategy — the row is a one-sided typology (T4/T5)

A row unit has **one good face (garden) and one neutral face (street)**:
- **Living eats the garden aspect.** Wohnen + Küche full-width to the rear; working rooms, stair, bad stack to the street. A row house with living to the street is the type's most common self-inflicted failure.
- Front band = service: entry, stair, storage, bath — daylight through the hall and modest openings; this band also buffers street noise from the living zone behind.
- **End units get a third face** — treat them as a different product: wider kitchen, side light, optionally a separate entrance for a future Einlieger or home office. Do not repeat one plan blindly down the row.
- Summer comfort: full-width glazing to S/W on a single-aspect section concentrates solar gain; external shading (Raffstore/ Rollladen, F_C ≤ 0.30 pattern per DIN 4108-2 — T2) is part of the *type*, not an add-on. Site in summer-hot climate region C? The one-sided west row without shading will fail the 1,200 Kh/a residential overheating limit that the simplified method can no longer forgive → `building-physics-thermal-moisture` owns the proof, the typology chooses the difficulty.
- Energy: the attached band sits at H'T ≤ 0.45 (Section 3.4) — the row is the cheapest route to very low demand on a family budget *without* a full Passivhaus package, provided airtightness (n50 ≤ 1.5 h⁻¹ with ventilation system / ≤ 3.0 without — GEG/DIN 4108-7, T1/T2) actually gets executed: each unit is an envelope junction with two neighbours, so flanking and joint details matter → `building-acoustics`, `masonry-construction`.

### 4.4 The stacked pair alternative (Doppelhaus with parity)

Where a family wants two independent households with parity (both grade access, both garden, no "who gets the roof" dispute): split a ~500–700 m² plot into two mirrored DHH on 12–16 m-wide half-parcels: each half gets porch + entry + stair on its own street face (plans mirrored), party wall at the shared line. Advantage over an EFH-with-Einlieger: clean separation, own addresses, own meters, own PV roof ridge. Disadvantage: each half is ~13 m wide — the frontage-competition problem (porch + entry + stair) now happens twice, just mirrored.

---

## Section 5: Geschosswohnungsbau (MFH) — Multi-Storey Residential

### 5.1 Urban forms and density bands (T4/T5 planning practice — VERIFY)

| Form | Pattern | WE/ha | Strength | Watch |
|---|---|---|---|---|
| **Zeile (row block)** | 25–40 m long, 12–14 m deep, 3–5 storeys, 2 stair cores | 50–90 | all units dual-aspect; cheap cross-wall structure; no corridor waste beyond one band | long facades need relief (axes, slight setbacks, re-entrant corners); parking court in front |
| **Offener Block / Punkt** | free-standing slabs/points in green | 40–80 | daylight 2–3 sides, views | exposed corners (α penalty); courtyard surveillance |
| **Blockrand (perimeter block)** | 3–6 storeys wrapping a Hof 10–25 m | 120–250 | lowest α, urban edge, protected Hof, commercial EG | Hof quality is everything; reflected noise; escape-route distances across courts |
| **Staffelbau / Atriumhaus** | terraced storeys, roof garden per unit | 40–80 | EFH-quality life at MFH density | waterproofing per terrace unit; WEG maintenance rules |
| **Hochhaus (residential)** | MBO pattern: top occupied-floor level > 22 m; lifts + Rettungstreppe | 120–400+ | land economy, views | Hochhaus-Brandschutzkonzept, FeuerwehrAufzug, wind, structure cost curve bends up; German rental market is cautious |

### 5.2 Unit mix theory (T4, DACH market — VERIFY per city segment)

| Segment | 1–2 Zi | 3 Zi | 4+ Zi | Notes |
|---|---|---|---|---|
| Inner-city rental | **40–55%** | 30–40% | 10–20% | the German urban mix peaks at 2–3 Zimmer — NOT at studios |
| Suburban family product | 15–25% | **35–45%** | 35–45% | Aufzug + Loggia + Kita proximity |
| Senior / altersgerecht | **45–60%** | 30–40% | ≤10% | rollstuhlgerecht quota per funding program (II. BV lineage — VERIFY) |
| Student / micro | **60–80%** at 12–25 m² | 10–20% | — | own kitchenette vs shared-kitchen = product decision |
| Baugruppe | negotiated | — | — | the mix *is* the concept — Section 8 |

Size bands (T4): 1-Zi 28–45; 2-Zi 50–65; 3-Zi 70–90; 4-Zi 90–115; 5-Zi/maisonette 110–160 m² WFL.

**Honesty flag:** "3 Zimmer" is a market label, not a household size. A 68 m² "3-Zi" with one bedroom serves a couple or single parent + child; an 82 m² "3-Zi" with two bedrooms serves four people. **When anyone cites a Zimmer count, get target m² and sleeping-room count too** — the compressed top of the band ("4 Zimmer = same area as 3") is the German analogue of the source market's compressed 4-bed problem.

### 5.3 Cores, circulation and escape logic (T1/T2 patterns — LBO + `fire-protection-building` govern)

The core is the typology's skeleton. Configurations and their efficiency (T3, universal theory):

| Core scheme | Access | NTG (WFL/BGF) | Use when |
|---|---|---|---|
| **Landing access, no corridor** | stair lobby serves 2–4 WE directly | 0.78–0.84 | point houses, small Zeilen — the efficiency champion |
| **Single-loaded corridor** | units on one side; depth 6–8 m | 0.75–0.82 | slab blocks on noise edges; corridor gets façade = daylight + escape quality |
| **Double-loaded corridor** | units both sides; total depth 12–14 m | 0.72–0.80 | the workhorse MFH; corridor daylit at ends, never a windowless tube |
| **Scissor stairs** | two interleaved stairs, one shaft | 0.72–0.78 | two independent escape routes at compact core width, taller stock |
| **Skip-stop + maisonettes** | corridor every 2nd floor | **0.75–0.84** | raises NTG *and* gives house-like dual-aspect units — the Unité / Alexandra Road lesson |

Escape and lift triggers by typology (MBO patterns, **edition + Land vary — VERIFY**; details owned by `fire-protection-building`):
- **EFH/DHH/RH (Gebäudeklasse 1–3):** one stair; the **second escape route may be a window/opening** for rooms with floor level below ~6.5 m (some Länder 8 m) above grade — opening pattern ≥ 0.90 × 1.20 m clear, low sill. The DG-conversion reserve *must* size these openings from day one (Section 14).
- **GK 4 and most >2 WE/floor situations:** **two independent escape routes** (second stair / second core or LBO-sanctioned alternative); within-building escape-route length limited (~25–35 m to the next safe place, patterns vary) — which is why Zeilen carry **2 cores per ~15–20 WE**, and why "one stair, 12 flats, 40 m corridor" dies in review *and* in use.
- **Hochhaus (>22 m residential):** required Rettungstreppe, FeuerwehrAufzug, full Brandschutzkonzept — fire engineer at the table before the typology is chosen, not after.
- **Aufzug (lift):** MBO pattern — in buildings with **more than 2 WE**, at least one escape route serving the upper floors must be lift-accessible (VERIFY Land + edition — several Länder have tightened this). Public funding adds barrierefrei/rollstuhlgerecht quotas. Treat the lift as part of the typology: shaft ≈ 2.2 × 2.2 m + lobby, cost band €45–70k (T4, dated); a 3-storey walk-up rental product without one ages out of the market before its first renovation.
- **Accessibility layer:** "barrierefrei" (DIN 18040-1/2 level) vs "rollstuhlgerecht" (funding grade: 150 × 150 cm manoeuvring, clear door ≥ ~90.5 cm pattern, level thresholds, accessible bathroom per unit) — decide **which units, how many, on which floors** at typology stage; retro-fitting rollstuhlgerecht into a frozen stack plan is the single most common MFH rework → cross-ref accessibility guidance.

### 5.4 Worked floor-plate check (T4/T3)

```
Zeile: 36.0 m × 13.2 m plate, 4 Vollgeschosse, 2 cores.
Gross plate                              36.0 × 13.2       = 475 m²
− external wall (KS 24 + Vormauer ≈ 0.36 m × 98.4 m)       ≈ 35 m²
− 2 cores (stair ≥ 100 cm + lobby + Aufzug + HWR)          = 68 m²
− corridor (1.20 m clear × ~27 m net)                      = 32 m²
− internal walls (≈ 6% of remainder)                       ≈ 25 m²
= Wohnfläche available per floor                           ≈ 315 m²
→ 4 WE avg 79 m² (2×68 + 2×95) or 5 WE avg 63 m²
Strict NTG = 315/475 ≈ 0.66; with loggia counting (25–50%)
marketed WFL lands at 0.72–0.78 ✓ inside the band.
Building: 4 × 4 = 16 WE; 4 WE/floor > 2 WE/floor →
two escape routes required → 2 cores at opposite ends ✓.
Diagnostic rules: strict NTG < 0.60 → corridor too long/wide,
core over-sized, or plate too deep (see 5.5); > 0.80 with
1.00 m corridors → check that furniture can actually turn.
Parking: 16 WE × 1.2 = 20 spots → TG (~32 m²/spot ≈ 640 m²)
= 1.35 plates underground — decide TG-vs-groundspots NOW, it
reshapes the whole ground storey (Section 9).
```

### 5.5 Plan depth and the orientation mix (T4)

- Double-loaded depth **12–13 m** (2 × 5.8–6.2 m bands + 1.2 m corridor) is the daylit limit without tricks. 14–16 m needs **Lichtrisse or a courtyard notch** — past that you are letting dark rooms and wondering why the mix stalls.
- **Minimum 2 dual-aspect corner units per floor**; pure-North stacks and pure-West stacks are the slow-selling inventory.
- Living-side priority: S/SW (with shading) > W (shading mandatory, region C worst) > E (ideal for sleeping/kids) > N (kitchen/bad/storage bands only).
- Maisonette: 2 storeys, depth 8–14 m, internal stair consumes 3–4 m² but deletes corridor area — **net NTG gain** plus house-like quality; access skip-stop; living below (loggia aspect), sleeping above; the internal stair belongs to a hall or the space's spine — a stair slicing a Wohnen in half is the type's classic failure.
- Exemplars worth re-reading (T3): **Unité d'Habitation (Le Corbusier, Marseille 1952)** — internal gallery street, skip-stop maisonettes; **Weissenhof Siedlung (Stuttgart 1927)** — series row logic, RMH width economics, flat-roof terrace types; **Alexandra Road Estate (Neave Brown, London 1978)** — stepped maisonettes with street-level entries; **Borneo Sporenburg (Amsterdam, ~100 WE/ha)** — narrow-row width economy; **Goldsmith Street (Norwich 2019)** — what airtightness discipline does to a row's energy ledger (Stirling Prize terrace).

---

## Section 6: Atrium- & Courtyard Houses (Hofhaus, Atriumhaustypologie)

The courtyard is the answer when the plot is **deep, aspect-conflicted, or urban-with-no-view**: it manufactures an outside from nothing. Same archetype at three scales:

### 6.1 Blockrand / Hoftype (city scale)

- Perimeter wings 3–6 storeys; Hof **10–25 m** across. The Hof's floor (play/garden/sitting), its edges (loggias, exits, bins *somewhere else*) and its proportion (height-to-width H/W ≈ 0.6–1.0) *are* the design. Below ~6 m width it is a light shaft with windows, not a courtyard; above ~25 m hard-surfaced it is a wind and noise drum.
- Daylight: Hof width ≥ ~0.8–1.0 × flanking height for genuine sun on the opposite face at least seasonally (50°N: a court flanked by 6 m walls only sees low winter sun well; N-face court rooms get reflected light, not sun).
- Abstandsflächen across a Hof follow LBO special rules (some Länder reduce the requirement between opposite room-bearing walls within a Baugebiet — **VERIFY**; do not assume the neighbour's wall can sit 2 m from your bedroom window).
- Privacy: every Hof window overlooks every other — the fix is programmatic (kitchens/baths/cores to the Hof, living corners angled off, loggia screens, staggered storeys), never a fence.
- Noise: hard faces at 12–16 m **reflect** conversation and play; soften the floor (planting, sand, timber), cap wing length, avoid re-entrant corners that focus sound.

### 6.2 House-with-courtyard (plot scale — the two-household / small-MFH answer)

L- or U-wing wrapping a 6–12 m court + service band to the street; every unit two-sided (court + garden). This is the generationenwohnen configuration: two households, shared court, separate entrances, parity — both get grade access and outdoor space, no "who gets the roof" dispute. Watch: the court microclimate (cold N pocket, wind funnel through the gap) and drainage/snow storage inside the court.

### 6.3 Atriumhaus (single household, land-locked or wide plot)

Rooms wrap a roofed/open internal court (~10–25 m², ≥2.5 m per side); the bungalow-with-court variant buys privacy on an overlooked plot without surrendering single-level living. Costs: every room gets a second (court) face = **more envelope per WFL than the bar** (the α penalty of the shape), and the court needs water/drain/snow logic from `roofing-waterproofing`. A **roofed** atrium is a heat trap without stack ventilation: high-level opening + low cool-air inlets, designed, not hoped for.

### 6.4 The large-plot rule — land as asset, envelope gate first

Everything above also covers the German "large garden plot" case (800–2,500 m², often at the settlement fringe or a subdivided Altbesitz): **first gate = is it even buildable at the assumed coverage** — inside a B-Plan/§34 area: normal GRZ/GFZ bands apply; at the fringe: **§35 BauGB Außenbereich usually means no claim to build at all** unless privileged (landuse) or an existing Bauleitplan applies. **T1 gate — check it before quoting any footprint.** Second rule: design *below* the legal maximum on purpose where the garden is the product (pavilion/L-bar, deep arrival forecourt, one generous private rear garden instead of four leftover strips). Present legal envelope and design recommendation as **two separate numbers** the client weighs: *"Your plan allows ~200 m² footprint and ~380 m² floor area here. I'd recommend 160 m² to keep the south garden a room outdoors. Here's the cost difference of each."*

---

## Section 7: Mixed Use (Gewerbe EG + Wohnen OG)

German inner-block and street-edge product: retail/praxis/office at grade, flats above. The stacking order and the interface details are the whole design.

| Interface | Rule (pattern) |
|---|---|
| Vertical order | Parking/Anlieferung → retail/gastronomy → office/praxis → Wohnen. Heavier + noisier low, quieter private high. Residential entrance distinct address, **not through the shop arcade** unless designed as a real lobby. |
| Own cores per use | Residential and commercial escape routes **independent to grade** — no shared stairs/corridors between uses → `fire-protection-building`. |
| Floor heights | Retail EG 3.8–4.5 m; office 2.8–3.5 m; Wohnen OG 2.6–2.8 m; the interface floor carries the section strain — decide it once, honestly. |
| Acoustics | Workroom↔dwelling: DIN 4109-1 minima (walls ≥ 53–55 dB, floors ≥ 54 dB class patterns — T2) and **contracted elevated protection (VDI 4100)** for anything sold as quality stock; gastronomy noise (extraction fans, deliveries, closing hours) is a *site-selection* question first — TA-Lärm fit of the area type governs what may operate → cross-ref codes/fire. |
| Structure | Commercial wants 6.5–8 m column grid; housing economy wants 5–6.5 m cross walls → **system-change floor** (transfer slab/beam at the interface) — flag to `structural-systems` before the unit mix freezes. A fully flexible empty retail shell under fixed housing walls is the standard product; the transfer is its price. |
| Services | Risers, extraction ducts, grease traps, separate Zähler districts for F&B want their shaft **now** — a 50 cm duct cannot be threaded through a finished beam zone later. |
| Waste & supply | Per-use container bays at a defined collection point; the Hof that daylights 18 flats must not double as 6 bin parks and a delivery stand — the Blockrand's most common ground-floor failure. |

---

## Section 8: Ownership & Tenure Models as Typology Drivers (T4)

| Model | What it forces typologically |
|---|---|
| **Owner-occupied EFH/DHH/RH** | one or no core; DG/KG **reserve** for children (Section 14); Stellplatz ≥ 1.5; Keller near-mandatory; energy standard as lifetime-cost argument |
| **Eigentumswohnanlage (WEG)** | the common-property lines *are* the design: Aufzug (lifetime + value), Schallschutz class, terrace/roof waterproofing accessibility, TG ramps, Gemeinschaftsraum — over-build the shared parts now or the Eigentümerversammlung will do it expensively later; Teilungserklärung fixes what owners may change (façade, loggia glazing) |
| **Institutional rental** | NTG discipline, 2–3-Zi mix, repeatable cores and units, low-maintenance envelope (Vormauer, putzarm), contracted acoustics; **age-out hedge**: flex/Anpassungswohnrooms + Aufzug so the stock still lets in 20 years |
| **Genossenschaft / Baugruppe** | cluster commons (10–15 m²/WE of *shared* area lets private WFL drop ~10%), 1–2 negotiated cores, roof terrace/ Waschküche/ Werkstatt/Gästeräume as program; phasing reserve; the mix and the stair count **are** the participation process — design options, not verdicts |
| **Erbbau (ground lease)** | term (typically 99 a) + Heimfall shape the exit: compact, well-maintainable, possibly demountable systems (serial timber) fit; premium land ≠ premium finish — reserve money for the building's second life |

---

## Section 9: Density Spectrum — Land Take, Sealing and the Carbon Ledger (T5/T4)

| WE/ha | Type zone | GFZ ~ | α ≈ | Typical sealed share | Verdict |
|---|---|---|---|---|---|
| 10–30 | freistehendes EFH | 0.2–0.4 | 0.30–0.50 | 35–55% | land + mobility loser; only defensible as true infill or deliberately *small* house with a real garden |
| 30–70 | DHH/RH/Kettenhaus | 0.4–0.8 | 0.16–0.32 | 40–55% | the sustainable family-density band: garden + attachment + short rows |
| 60–120 | Zeile / offener Block 3–5 Gesch. | 0.8–1.6 | 0.10–0.19 | 45–65% | sweet spot for car-light living with shared TG |
| 120–250 | Blockrand / dichter MFH | 1.6–3.0 | 0.08–0.15 | 55–75% | needs Hof + quarter quality to pay for the sealing |
| 250+ | Hochhaus / townhouse-hybrid | >3.0 | 0.05–0.10 | high | structure + fire + lift cost curve bends up; only where land price and transit justify |

Anchors (T5, German study values — verify before quoting): a Berlin-model 400 m² lot compared as weekend-house pattern (30 m² floor, 2 persons) vs modernist GFZ 1.5 (450 m² floor, 11 persons) vs Gründerzeit GFZ 3.4 (1,020 m² floor, 27 persons) — same land, **an order of magnitude of housing capacity**; dispersed low-rise adds ≈ +1.4 t CO₂e/person·a in commuting and 7–8× sealing vs the blockrand (Section 3.4).

Typology-level levers regardless of density (cross-ref `building-physics-thermal-moisture`, `roofing-waterproofing`, `building-materials`):
- **Sealing ≠ GRZ:** a GRZ-0.2 plot can still be 60% sealed by driveways and patios. Measure actual Versiegelung; minimise asphalt courts; **Retentionsdach** on every flat roof (reserve the statics + fall now) and Fassadenbegrünung where the substrate allows.
- **PV is a typology decision, not an MEP one:** roof pitch/azimuth/standoff and the EG switch-room are fixed at form stage; several Länder already impose PV on new residential roofs (BW-style GEIG lineage — VERIFY current), and some areas still fight it on gestalt grounds — resolve in the B-Plan conversation, not at permit submission.
- **Graue Energie per WE tracks α × structure mass:** the cross-wall Zeile or Holzhybrid on a shared TG beats detached bars on single-storey slabs by a wide margin; the *shared* basement is the type's biggest carbon gift and biggest cost risk (groundworks!) — decide it with `geotechnics-foundations` early.
- **Bestand first:** conversion, DG-Ausbau and Aufstockung of existing MFH usually beat demolition on LCC, CO₂e *and* permit speed; where the market will not carry the existing quality, the addition typology (Section 14) is the bridge.

---

## Section 10: Unit Configuration & Program Reference (consolidated, T4)

Room-level sizing belongs downstream; the typology table is what rooms *exist* at each rung:

| Space | EFH | DHH/RMH | 2-Zi WE | 3-Zi WE | 4-Zi WE | Maisonette | Senior WE |
|---|---|---|---|---|---|---|---|
| Wohnen+Essen | 35–55 | 30–45 | 22–30 | 28–36 | 32–40 | split 2 levels | 25–35 + Loggia |
| Küche | own + HWR | open or sep. | 7–10 | 8–11 separable | open + pantry | open EG + pantry | open, reachable |
| Sleeping/study | 3–4 | 3 | 1 | 2 | 3 | up | 1–2 |
| Bad | 1–2 | 1–2 | 1 DU/Wanne | Wanne + DU | 2 | 1 per level | 1 **rollstuhlgerecht** |
| Gäste-WC | 1 | 1 | — | — | 1 | — | — |
| Abstell inner | 6–12 | 4–8 | 2–4 | 3–5 | 5–7 | 4–8 | 3–5 + Keller |
| Outdoor | garden + TGL | garden 2-sided | Balkon/Loggia | Loggia | Loggia (+Garten EG) | roof/private | level Loggia |
| Storage/heating | Keller + HWR | Keller | Kellerraum ~4–6 m²/WE | +Waschküche prog. | — | — | + Gemeinschaftsfl. |

**The bathroom rule (T4 German expectation):**
```
Bad ≈ 1 Wannenbad per unit (2 ab 4 Zi) + separate DU ab 3 Zi
    + Gäste-WC in EFH/DHH
    + rollstuhlgerecht share per funding quota (VERIFY program)
Windowless bathroom is survivable (mechanical exhaust per DIN 18017-3, T2);
windowless kitchen is tolerated; windowless WOHNEN is a dead unit.
```

**Stellplatz rule (T1+T4 mix):** pattern per Land/municipality: EFH ≈ 1–1.5 per unit; MFH 1 per WE + ~10% guest, often reducible near ÖPNV (many LBOs now *allow* reduction — VERIFY). TG ≈ 30–35 m² area per spot incl. aisles/ramp → 6–8 spots eat a whole ground-floor plate-equivalent; **count parking as typology, not detail** — the TG decides the ground storey, the Hof layout and the unit count. Surface courts: max ½ the plot's open space before the quarter reads as a car park.

**Vertical program per building size (T4):** EFH: 1 stair. DHH pair: 2. RMH row: 1 stair per unit (the row's point). MFH: see 5.3 (2 cores above 2 WE/floor pattern; lift ≥ 1 per core ≥ 3–4 storeys by rule + comfort; Müll-/Fahrradräume per core at EG/U). **Bicycle rooms: 0.25–0.35 m²/WE at the bike-critical German city (plus outdoor racks) — under-programming them is the modern equivalent of forgetting the cellar.**

---

## Section 11: Construction System Fit per Typology

Typology and structure are not separable: **the type selects the load-bearing logic, the logic caps the spans, the spans cap plan depth and room widths.** Two structural worldviews:

- **Wall logic (Wandbauweise / Querverbauung):** floors span ~4.5–6.5 m between load-bearing cross walls; walls carry vertical *and* horizontal load (shear-plate action — the bracing system is the apartment layout). Cheap, stiff, great mass and acoustics; but the layout is frozen into the wall grid for the building's life, and openings stack strictly (perforated-façade rules → `masonry-construction`).
- **Grid logic (Skelettbau):** columns on a grid — residential economy 5–7.5 m; **parking 5.0 m bay depth ≈ 2.5 m × 3 bays = 7.5 m**; office 7.2–9.0 m — non-loadbearing infill/partitions. Freedom and later conversion (the same floor serves Praxis or Wohnen), at +10–20% structure cost and less summer storage mass (check the S-method/simulation, 13.4).

### 11.1 Fit table (T2/T4 — verify against the calculation skills)

| Typology | System pattern | Why this fit | Cross-ref |
|---|---|---|---|
| **EFH / DHH / RH ≤ 2 VG + DG** | **Mauerwerk + WDVS** (HLz 30–36.5 / KS), or **monolithisch** (Porenbeton ≥ 36.5, or gefüllte Planziegel ~36.5–42.5 — no external insulation), or **Holztafelbau** on a RC Keller slab; pitched roof in timber | spans ≤ room band; self-braced wall construction; GK 1–3 fire trivial at these heights; monolith route buys low-maintenance + mass, WDVS route buys U-value headroom and future-proofing | `masonry-construction`, `timber-steel-design` |
| **Reihenhaus / Kettenhaus series** | RC or stone Keller + repeated superstructure module (Holztafel OG or massive) — one typical bay, arrayed along the row | repetition *is* the economy; party wall = real coordinated twin wall (4.2); roof continuity over the row needs movement-joint discipline | `masonry-construction`, `concrete-detailing` |
| **MFH 3–5 VG, 12–13 m deep, dual-aspect** | **Cross-wall masonry: KS 17.5–24 (+ Vormauerschale Klinker for the urban skin) or Hochlochziegel**, RC or timber floors spanning the unit width (4.5–6.5 m); partly inside the **EN 1996-3 simplified-design envelope** (≤ 2.75 m storey height, live load ≤ 5 kN/m², building ≤ 20 m, floor span ≤ 6.0 m — T2) | the workhorse German MFH: cheapest durable wall+bracing logic, Vormauer = low-maintenance face, deep cross walls carry both aspects; apartment width sets the wall grid, wall grid sets the unit mix | `masonry-construction`, `structural-systems` |
| **MFH/mixed with flexible EG** | **Stahlbeton-Skelett or -Wand + Platte** (Ribbed/Halbfertigteil; flat slab practical limit ~7 m with punching checks), masonry infill above; **system-change floor** at the commerce/housing boundary | open grid below, economical wall logic above — the transfer is the mixed-use tax (Section 7) | `structural-systems`, `concrete-detailing` |
| **Large series / Wohnanlage** | **Fertigteile** (precast sandwich/single walls + hollow-core or half-slab floors) or serial Holztafel/CLT | repetition buys the prefab premium; tolerances, joint airtightness and acoustic flanking at connections are the managed risk | `building-materials`, `masonry-construction` |
| **Holzhybrid / CLT 4–5 Gesch. (GK 3–4)** | CLT or timber-frame walls + timber/wood-concrete composite floors; RC or braced-timber core; **two gates decide feasibility: Brandschutz (burn-off + exposure plan) and Schallschutz (mass: ≥ ~20 cm effective floors, floating screed, chippings fill)** | speed, dry execution, carbon; weak long spans → draw the plan on the timber wall grid from day one | `timber-steel-design` |
| **Aufstockung / DG-Ausbau** | **CLT / timber frame on existing** — low self-weight is the entire argument (T4: light addition beats foundation reinforcement); existing walls + founded checked first | see Section 14 | `timber-steel-design`, `geotechnics-foundations` |

### 11.2 Span envelope by system (T2 planning aids — the engineer sizes, not this table)

| System | Economic span | Consequence for the plan |
|---|---|---|
| One-way RC slab | ≤ ~5–6 m (depth ~span/25–30; ribbed to ~7–8 m) | room band = span: MFH depth 6.0–6.5 m bands |
| Two-way / flat slab | practical ≤ ~7 m + punching checks | needs cores for bracing → grid logic + wall cores |
| Masonry cross-wall floors (RC/timber) | ≤ 6.0 m (EN 1996-3 envelope) | unit width 4.5–6.0 m; party wall sits *on* the load path |
| Timber joist/panel | ~4–6.5 m (deeper engineered members to ~8) | row/maisonette stairs and galleries integrate structurally |
| CLT floor | ~4–5 m one-way typical; ribbed/box elements beyond | wall grid every ~4 m or accept ribbed decks |
| Steel/glulam frame | 6–10+ m | halls, EG commercial, parking decks |

**The fitting rule (source lesson, retained):** *the grid comes before the plan.* A double-height living bay, a 24 m² open kitchen-dining across a 6 m span, or a future-Praxis EG all break the wall logic of an otherwise masonry house — they force an RC beam-and-column bay inside it. Decide at typology stage which rooms exceed the system, give them their own structural bay, and price it; do not let a "big open room" wish discover the transfer at detail stage.

### 11.3 Storey heights (T4 design targets + T1 minima)

- **Min headroom for Aufenthaltsräume is LBO territory (pattern: 2.50 m; Länder relax to 2.30–2.40 in defined cases — VERIFY)**; sloped-ceiling DG counted by surface/height fractions (Bremen-style full-height rules differ — VERIFY).
- Comfortable German practice: **floor-to-floor 2.75–2.90 m for MFH** (2.60 clear + 15–25 cm construction: screed + HI + install level), **EFH 2.70–2.80**; senior/funding product and any barrierefrei claim → plan the install level and ceiling heights for it once, not by accident; Gewerbe EG 3.5–4.5 (Section 7).
- Timber: +1–2 cm per exposed-soffit honesty; concrete: the flat-slab temptation eats the install zone — coordinate with `openings-windows-doors` reveals and `building-physics-thermal-moisture` surface-temperature margins at slab edges.

---

## Section 12: Circulation, Escape & Accessibility Dimensions by Type (T2/T3, VERIFY per LBO/DIN)

| Element | Pattern | Typological consequence |
|---|---|---|
| Required stair clear width | **≥ 80 cm** (EFH/RH, small MFH); **≥ 100 cm** with Aufzug / more units / escape-route duty | stair width × runs sets the core footprint: a 100 cm two-run stair + lift + lobby ≈ 30–36 m²/floor — budget it per plate before cutting units |
| Stair geometry | DIN 18065: step 14–19 cm, **63 cm G = 2s+a** (60–65), landing ≥ stair width (~1.05+), headroom ≥ 2.00 m pattern | maisonette internal stairs may go 19–21 cm steps only in-unit patterns (VERIFY); a 21 cm "space-saving" stair in the common core is a rework, not a design |
| Corridor | ≥ 1.00 m clear to one escape function, 1.20–1.50 for MFH comfort; **no dead-end corridor tubes**; daylit at ends | corridor length ≤ ~25–35 m pattern to a stair (5.3) decides core spacing → decides plate length → decides the whole Zeile module |
| Unit doors / common doors | ≥ 0.90 m leaf common; rollstuhlgerecht pattern 1.005 m (= ~90.5 cm clear) | the 88.5 cm "cost-optimized" flat door ages the stock out — Section 5.3 |
| Rescue openings (2. Rettungsweg via window) | ≥ 0.90 × 1.20 m clear, sill ≤ ~1.20 m, room ≤ ~6.5 m above grade (pattern) | every sleeping room needs one — a DG without compliant openings is an illegal future bedroom (Section 14 reserve) |
| Lift | >2 WE/floor pattern per MBO (5.3); Kabinen ≥ 1.00 × 1.40 m (stretcher/funding pattern), 1.10 × 1.70 m "large" | shaft + pit + head + machine-room-less top: reserve 2.6 × 2.3 m + 1.2 m lobby — draw it at typology stage |
| Basement/TG escape | TG: two exits pattern (ramp + second escape), lift/stair from TG to all floors in MFH; ramp ≤ 6% straight / 15–17% curved patterns, headroom ≥ 2.0 m | the TG second escape + ramp eats ~40–60 m² of plate/plot — part of the Section 5.4 parking arithmetic |
| Keller & HWR | Keller rooms ≥ 6 m²/WE pattern; Waschküche or in-unit laundry; HWR ≥ 4 m² in EFH | the cellar is the type's third life (storage/plant/reserve) — never "optional" in DACH market |

→ Fire-compartment sizes, Brandwand rules, Hochhaus specifics and all escape *requirements*: `fire-protection-building`. Accessibility detail dimensions: DIN 18040-2 level via `building-physics-thermal-moisture`-adjacent skills and the funding guide of the Land.

---

## Section 13: Privacy, Daylight and Orientation by Typology

### 13.1 Orientation strategy is type-specific — the summary table

| Type | Good faces | Living goes | Services go | The trap |
|---|---|---|---|---|
| EFH bar | 2 (front/rear) | garden side | street side | north-only kitchen on a "cheap" lot |
| DHH/RMH | 2 | full-width rear | front band | mirror-flipping a plan without flipping the sun |
| REH / Kettenhaus | 3 | garden + free side | front | end-unit bonus sold away by repeating the middle plan |
| Zeile MFH | 2 per unit | S/SW band | N band | double-loaded depth creeping past 13 m |
| Blockrand | 2 (street + Hof) | Hof side | street side where noisy | Hof as bin court / echo drum |
| Atriumhaus | court + outside | court side | service band | unshaded glazed court = greenhouse |
| Maisonette | 2 per level | living down, sleeping up | stair spine | stair through the middle of Wohnen |
| Mixed stack | n/a | Wohnen above buffer | Gewerbe below | shop extraction under the new S-W loggia |

### 13.2 Privacy mechanics (T4 patterns, cross-check LBO/Abstand)

- **Distances:** 3 m Abstandsfläche is a light/air/fire rule, **not a privacy rule** — two facing windows at 3 m read as a confessional. Usable living-to-living overlook distance ≈ **≥ 8–10 m**, court edges ≥ 6 m; between gardens of a row, stagger terraces or accept the 1.8–2.0 m fence (Ortsrecht caps fence heights — VERIFY Satzung).
- **Programmatic screening beats screens:** service bands, loggia depth (≥ 1.6 m screens what it shelters), staggered DG set-backs, and one *defensible* half-private threshold per unit (step + porch, not a hedge wall) are the row/court quality levers.
- **Ground floors of MFH/Blockrand:** the flat with window at 0.6 m above a public path has no interior life without a 3–5 m private strip, change-level (Terrasse +0.30 vs path −0.20 reads occupied) or loggia band — otherwise the windows stay shuttered and the street face dies.
- **DG conversions across the row:** roof windows opposite neighbour windows create the classic Nachbarschaftsstreit — angle dormers, limit to the room-bearing side, check the B-Plan's roof-window allowances before promising the office.

### 13.3 Daylight by typology — the depth ledger restated

Usable daylight depth ≈ 2× room height per side (3.2). Consequences:
- EFH/RH bands 5.2–6.2 m deep read bright to the middle of the room; open kitchen-dining can eat the full 6.2 m rear band if glazed full width.
- MFH 12–13 m double-loaded = two bright bands + a lit corridor — **the plate depth is the typology's contract with daylight**; break it and you pay in Lichthöfe (each costing 30–60 m² of plate without rent).
- North-band units on dense urban sites work *if* the quarter compensates (loggias, bright cores, shared roof); they do not work in a row of all-N with no outdoor rooms — that configuration is the mix killer (anti-patterns, 17).
- Interior courts: see 6.1 proportions; light-coloured surfaces + reflecting floors raise the deep Hof's useful range; the DIN 4108-2 S-value system (solar gain) and the 2×/3× depth rules assume unobstructed sky — shaded courts need the simulation path → `building-physics-thermal-moisture`.

### 13.4 Summer comfort by type (T2 anchors — proof in `building-physics-thermal-moisture`)

- Residential overheating limit **1,200 Kh/a** against region-dependent reference temperature (A 25 / B 26 / C 27 °C — DIN 4108-2 map, VERIFY site region); the simplified proof's credits depend on **construction mass class** (leicht/mittel/schwer) and **night ventilation** — which the typology decides:
  - massive cross-wall MFH = "mittel/schwer" + easy cross-vent via dual aspect → the type *earns* its S-values;
  - lightweight single-aspect Holztafel row with sealed north band = poor night purge → shading area and FC discipline carry everything;
  - Atrium/atrium-roofed plans = stack-ventilation machines **if** the high openings exist;
  - skeleton offices/retail above shops lose the mass benefit → add it deliberately (TABS or exposed concrete) or pay in cooling (and the EPBD-era efficiency paperwork).
- **Orientation × shading:** the S-façade's winter gain is welcome (vertical irradiation peaks in winter low sun — a *benefit* for passive heating), the W/E façades' summer gain is the killer: external FC ≤ 0.30 devices on O/W by default in regions B/C; internal blinds do not count toward the proof.

---

## Section 14: Expansion & Later-Floor Logic (Erweiterungsreserve / Aufstockung)

The German stock argument in one line: **a house is built once and changed three times.** Design the change in.

### 14.1 Reserves by typology (T4/T2)

| Typology | The reserve to design now | What freezes it if forgotten |
|---|---|---|
| EFH | **DG to full-count height** (2.30–2.50 m at the standing line), compliant rescue openings (0.90 × 1.20), floor for partitions (LL allowance), a stair position + wall opening reserved, riser routed past it, sufficient B-Plan GFZ headroom confirmed | a dormer-less low eave; the "spitzes Dach" that is legally a third Vollgeschoss the B-Plan won't allow |
| EFH/DHH | KG ceiling + footings sized for +1 storey *if* the client might add one later — cost of the reserve is ~rebar %; cost of retro-check is a Statik + possible Unterfangung | single-storey strip footings on sand with a new family arriving |
| Einlieger track | a second address-capable entrance (from the front path, not through the Diele), a second meter position, kitchen riser stub | the 2-unit life that needs the owner's hallway |
| Doppelhaus / two-household | both halves mirror-capable utilities; roof ridge split for two PV strings; joint at the party for future solar thermal | shared meter, shared ridge — the parity breaks at the first dispute |
| RH series | garage → workspace conversion floor + window; side strip for a future annex under GRZ headroom | GRZ at 100% the day you want the office |
| MFH | **structural + shaft reserve for one staffaged or set-back DG storey**, flat-roof statics for PV + Retention, stair tower for DG units, TG ceiling heights +15 cm for future ventilation runs | B-Plan height cap discovered after the client asks for the Aufstockung |
| Bestand MFH → Aufstockung | see 14.2 | |

### 14.2 Aufstockung logic (adding floors to existing stock)

1. **Two legal gates before any statics:** (a) does the B-Plan/§34 still permit the added volume/height (VG count, Wandhöhe, GRZ unchanged — a set-back storey often slips where a full one doesn't)? (b) **Abstandsflächen to neighbours re-trigger for the added storey** — the classic Aufstockung killer; a 4°-setback line or roof-flat disguise is not a legal strategy.
2. **Statics:** existing wall/foundation capacity check (`masonry-construction`, `geotechnics-foundations`); load path down through the old ceiling diaphragm; **timber/CLT addition chosen for weight (T4: the standard German move), bracing via new core or shear walls tied into the old plan**; the added storey's fire class can escalate the *whole* building (GK3→4 pattern: second escape, materials) — budget the Brandschutzkonzept with it, that is where Aufstockung projects die.
3. **Program:** added storeys read best set-back (roof terrace as the price of the new volume — and it settles the flat-roof-vs-neighbour-dust argument), units on it as Maisonette back into the old top floor (skip-stop access) or as one clean new penthouse; service risers extended in a new Schacht, not chased through the old façades.
4. **DG-Ausbau (conversion within the existing roof) is the cheap sister:** check floor loading for partitioned bedrooms, headroom counting rules (WoFlV fractions), and the rescue openings; often the *only* reserve the B-Plan never counted against you.

---

## Section 15: Cost Logic by Typology (T4, 2026 bands — dated, VERIFY before quoting)

### 15.1 The conversion rule

When a client gives a budget, **convert it to area before discussing typology**, not after:
```
Budget €480k build costs (KG 300–600, no land) at the EFH standard band
  ~€2,300/m² WFL  →  ~210 m² WFL  →  a 2-VG EFH + Keller or a DHH,
  NOT a 6-WE house — say so in the first reply.
Same €480k at the MFH institutional band ~€1,900/m² → ~250 m² ≈ 3 WE —
  still not a development; the development question starts at ~€2M+,
  where ~1,100 m² WFL ≈ 14 WE becomes real. Which world the budget lives
  in (living in it / renting it out / selling it) decides the typology
  before the plot does.
```

### 15.2 Bands (KG 300–400 build-up + typical KG 500/600 adders; €/m² WFL or BGF, 2026, dated)

| Product | Band €/m² | Notes |
|---|---|---|
| EFH massive, standard finish, incl. Keller | **2,100–2,800** | Holztafel similar −10/0%; WDVS vs monolith ≈ cost-neutral life-cycle trade |
| EFH premium | 2,800–3,800+ | finish and geometry drive it, not the type |
| DHH / RH (series, single developer) | 1,800–2,400 | repetition is the discount; party-wall coordination is the fee line |
| MFH 3–5 VG, KfW-efficient, incl. Aufzug | **1,700–2,200** | the institutional reference ≈ €2,000/m² BGF Bau+NBK used in developer models (T5 example — verify live) |
| MFH with TG (KG 300 UG share) | +350–600 €/m² or **38–55k €/Stellplatz TG** | the single biggest typology-level swing — run the parking count *before* the unit count (5.4) |
| Aufstockung 1 timber storey incl. fire package | 1,900–2,700 €/m² added WFL | + Brandschutzkonzept and existing-structure survey lines |
| Mixed-use EG fit-out shell | +400–800 €/m² EG | the transfer floor cost sits in KG 300 — Section 7 |

**Typology-driven modifiers (apply on top of the band):**
| Feature | Effect | Why |
|---|---|---|
| Keller vs slab-on-grade | +250–450 €/m² KGM | excavation, tanking (DIN 18533 load class!), waterproof floor |
| High groundwater / Altlasten | +∞ until assessed | `geotechnics-foundations` gate — the basement typology can evaporate a whole project |
| WEG division | + small % | separation joints, sound classes, technical documentation |
| VDI 4100 elevated acoustic class | +3–8% | mass, decoupling, twin walls (contract it — BGH lesson) |
| Balcony/loggia per unit | +6–12k €/unit | cantilever thermal-bridge discipline (DIN 4108-2 forbids plain cantilever without decoupling — T1/T2) → `openings-windows-doors`/`building-physics-thermal-moisture` |
| Set-back/terraced massing | +% envelope per m² | the α penalty of form (3.4) |
| Timber-hybrid at GK4 | ≈ parity, −programme time | +fire/sound engineering lines; the win is schedule and carbon |

### 15.3 The rental viability quick-check (T5 developer arithmetic)

The source's developer model pattern, translated: annual net cold rent × (1 − management/vacancy ~15–20%) × yield-factor (≈ 1 / property yield, e.g. LZS 4% → factor 25) = gross capital value; minus construction + side costs + land = trading margin. **The typology sits inside this on two levers: achievable rent €/m² (mix, Aufzug, Loggia, quarter) and WFL-per-BGF (NTG 5.3).** A "nicer" building at NTG 0.70 vs 0.78 on the same plate loses ~10% of the lettable product — typology discipline is yield discipline.

---

## Section 16: Worked Examples (the decision tree, filled)

### 16.1 "Family of four, 480 m² plot in WR, build budget €480k"

```
1. Plot        16 × 30 m, south garden rear. Width 16 = free-standing barely
               works (2×3 setback + ~10 m depth = 16) ✓ EFH allowed by geometry.
2. Envelope    B-Plan (hypothetical): GRZ 0.2 → 96 m² footprint; GFZ 0.4 → 192 m²
               (2 VG × 96) + DG typically outside GFZ + WR 30–45° or flat per plan.
3. Budget      480k / ~2,300 €/m² (incl. Keller, mid finish) ≈ 210 m² WFL target
               → footprint 96 + OG 96 + DG reserve.
4. Typology    EFH 2 VG, 96 m² plates: EG Wohnen/Kochen 45 + entry/util 20 +
               Arbeitszimmer 12 + Gäste; OG 3 Zi + Bad; DG = reserve (Section 14).
               Alternative kept alive: split twin plot with one neighbour later
               (DHH) if the Gemeinde allows — NOT needed, geometry says free-standing OK.
5. Structure   KGS WU or stone; EG+OG Mauerwerk HLz 36.5 + WDVS (or monolith),
               DG timber roof with full-height reserve; spans ≤ room band 6 m ✓ wall logic.
6. Energy      α ≈ 0.35–0.40 (freistehend) → H'T reference target ≤ 0.40 (≤350 m² AN):
               ~0.20–0.24 envelope mean needed → compact form, ≤ 25–30% glazing,
               external shading S/W, either Luft-WP+PV or Fernwärme.
7. Say         planning study; B-Plan + LBO check; Entwurfsverfasser + Nachweis;
               DG reserve and rescue openings already sized.
```

### 16.2 "Two households, 650 m² corner plot, parity wanted"

```
Corner plot = two street faces → both halves get grade entries without
sharing a corridor: DOPPELHAUS, two mirrored 13–14 m halves, party wall 4.2.
GRZ check: 2 × ~70 m² footprint + 1 Carport pair ≈ GRZ 0.25 → 163 m² ✓.
Each half: EG Wohnen/Küche garden side, OG 3 Zi, DG Ausbaureserve — same
as 16.1 but the frontage problem (entry+stair+porch) is solved by the corner,
which is why the corner plot *is* the DHH plot.
Structure: two independent building halves on one shared wall (twin leaf +
separation joint), two roofs, two PV strings, two meters — parity down to
the Grundbuch. Flag: Schallschutz party ≥ 62 dB + fire separation wall.
```

### 16.3 "Developer, 2,800 m² urban-edge plot, target ~28 WE, GFZ 1.8"

```
1. Envelope    GFZ 1.8 → 5,040 m² floor plates; GRZ 0.4 → 1,120 m² footprint
               → 4–5 VG with footprint ~1,000 m² total. Noise edge? If road rail
               ≥ limit → living away from source → double Zeile parallel to source
               screens the quiet Hof → typology = the noise answer.
2. Form        Two Zeilen 36 × 13.2 m (5.4 pattern) + one 24 m Zeile, or one
               60 m Zeile split by 2 expansion-jointed cores. ~26–30 WE at 65–85 m².
3. Cores       3 cores × 2 Treppenhäuser? no — each Zeile: 2 cores per 4–5 WE/floor,
               Aufzug per core (MBO >2 WE), 16 WE/Zeile ✓ escape lengths ≤ 35 m.
4. Structure   Cross-wall KS + Vormauer, 17.5–24 cm walls, RC floors 5.85 m span
               (within EN 1996-3 envelope), shared TG 36 spots (~1,250 m²) —
               run 5.4 arithmetic: TG = ground storey redesign, Hof above.
               Value alternative: 5 VG Holzhybrid CLT — same walls logic, faster,
               lighter TG; both priced, one chosen for schedule.
5. Mix         45% 3-Zi / 35% 2-Zi / 20% 4-Zi EG-garden — inner-city rental table (5.2);
               ≥ 2 dual-aspect corners per floor; no pure-N unit > 1 per floor.
6. Density     28 WE / 0.28 ha = 100 WE/ha ✓ band 60–120; sealed share discipline:
               flat-roof Retention + PV (α per 3.4 row-band ~0.15 → H'T ≤ 0.65 class
               comfortably) — the compact type is why the EPC works.
7. Say         NTG per plate checked (≥0.75 WFL/BGF incl. loggia counting),
               acoustic VDI 4100 level contractual, TG second escape sized.
```

### 16.4 "Baulücke 900 m², 20 m wide × 45 m deep"

```
Depth 45 m > 2.2× width → single bar = dead middle. Hof type (6.1):
EG + 4 VG wings 12–13 m deep, entrance wing at street (Hoftor + cores),
rear garden wing; Hof 12 × 18 m ≥ 0.9× height ✓ sun reaches opposite face
at low winter angles, summer shade = the Hof's comfort bonus.
Units: street side = work rooms + loggia band (noise), Hof side = living;
2 cores serve 3–4 WE/floor... arithmetic: 2 wings × 4 × 2 units ≈ 16–18 WE,
WFL 65–95 m², NTG 0.72–0.78. Structure: cross-wall both bands → the Hof
notch is the structural joint line — expansion joint at the re-entrant corner
(masonry opening rules, `masonry-construction`).
Abstandsflächen within the Hof per LBO Hof rules — VERIFY before fixing wing
height × width; the 12 m Hof at 5 storeys (15 m walls) sits right on the
comfort boundary of both sun and noise.
```

### 16.5 "GK3, 2-storey 1960s MFH — one added storey worth it?"

```
Gates: B-Plan (height/VG? §34 precedent?); Aufstandsflächen re-check with
neighbours (15 m walls now need new depth at the added level); existing
masonry + foundation reserve (Typenstatik era — likely 2 VG designed, check
drawings/`masonry-construction`), fire class: still ≤ 7 m after addition?
(4th VG → GK4 territory → second escape + materials → the cost that decides).
Structural answer usually: CLT/timber 1 storey, new core for second escape
or roof-exit onto Nachbardach per concept; +6 WE of 55–75 m² = 420 m² WFL
at ~2,300 €/m² + Brandschutz + TG-lift if required — compare vs new-build
on the same land price. Bestand first (9): if it clears, it wins.
```

---

## Section 17: Anti-Patterns

| Anti-pattern | Why it fails | Fix |
|---|---|---|
| **Deep flats without light source** (plate > 14–15 m, or 16 m double-loaded corridor without end light) | middle of every unit is artificial-lit living; lettings stall; DIN 18017-3 exhaust becomes de facto habitability kit | split the plate (Lichtriss ≥ 2–2.5 m wide, or notch the corridor end), go single-loaded, or accept 12–13 m and resize the units |
| Windowless Wohn-/Schlafraum | dead product; not a "studio character" | kitchen/bath only, ever |
| Row house with living to the street | noise + overlook make the good rooms the bad ones | flip: living full-width to garden; if both sides noisy → atrium/court type |
| End units identical to middle units | third face + value discarded | design REH as its own product |
| MFH: 12–16 WE down one 40 m corridor on one stair | fails escape rules and daily life | core count per 5.3; split into 2 buildings before it becomes one long building |
| Maisonettes with the access corridor on every floor | you paid the corridor AND the internal stair | skip-stop the corridor |
| All-North (or all-West) unit stack | slow units, overheated West in region C | orientation mix per floor ≥ 2 dual-aspect corners; shading discipline |
| Aufzug "not now" on 3–4 VG sale/rent product | stock ages out at the first demographic check; retrofit = core surgery | lift from the plate, shaft from day one |
| Blockrand with the Hof as bin yard + asphalt | the type's entire asset deleted | waste elsewhere, soft floor, edges with program |
| Basement/TG committed before groundwater/Altlasten | 6-figure surprises or a dead program | the 1.1 gate; `geotechnics-foundations` |
| Parking courts that eat the open space | GRZ-fine, quarter-dead | TG or carport rows screened; measure sealing not coverage (9) |
| GFZ-maxed massing on a family budget | the type the money can't finish | 0.3: build the smaller envelope well + reserve |
| "Open living" wish breaking wall logic silently | 24 m² span discovered at detail stage → transfer beam, +cost, +depth | pre-assign long-span bays to a grid bay (11.2) at typology stage |
| Party wall as a drawing line, not a construction | acoustic/fire/legal disputes after handover | twin-wall built-up + coordinated penetrations (4.2) |
| Schallschutz assumed at permit minimum for premium sale | case-law disappointment (BGH line) | VDI 4100 class contracted (`building-acoustics`) |
| DG added without rescue openings / headroom reserve | the extra storey never becomes a bedroom | Section 14 reserve checklist |
| Atrium/roofed court with no high vent | heat trap | stack openings designed (6.3) |
| Mixed-use: shared residential/commercial core | approval + both worlds' complaints | independent escape routes, lobbies (7) |
| Single-aspect west full-height glazing, region C, no shading | fails 1,200 Kh/a; retrofits external shading at the owner's expense | FC ≤ 0.30 external from day one (13.4) |

---

## Section 18: Checklists & Answer Templates

### 18.1 Standard opening for a typology question

```
Before I pick a form I need five things:
1. Plot area AND dimensions (width decides attached vs free-standing —
   "500 m²" on 10 m frontage is a row house, not a villa)
2. The B-Plan (area type, GRZ/GFZ, Vollgeschosse, open/closed Bauweise,
   Wandhöhe/roof, any unit cap) or "no B-Plan" — with §34 this changes everything
3. Who lives/uses it: one household, two with parity, rental, WEG sale,
   Baugruppe, mixed ground floor?
4. Budget — and whether it includes Keller/TG/Außenanlagen (no land)
5. Rooms needed now and in 10 years; accessibility intention (Aufzug?
   rollstuhlgerecht share?)
Tell me what you have; I'll say which decisions are blocked without the rest.
```

### 18.2 Pre-handoff checklist — before presenting any typology proposal

- [ ] Plot confirmed **in metres** (width, depth, level difference, orientation)
- [ ] **B-Plan read** (area type, GRZ, GFZ, VG count, Bauweise, wall-height/roof band, unit caps) or §34 precedent analysed — never quoted from assumption
- [ ] Abstandsflächen applied (0.4×H min 3 m pattern, Land variant) incl. **across-courtyard** checks
- [ ] Buildable footprint + plates calculated **and the program demonstrably fits inside them** (do the arithmetic, 2.2/5.4 — do not eyeball)
- [ ] Plan depth ≤ 2×/3× room height respected; every unit ≥ 1 dual-aspect or court face; orientation mix per floor checked
- [ ] Cores sized: stairs + Aufzug + Müll/Fahrrad + HWR; second-escape count/lengths per LBO pattern; **NTG computed and sanity-checked (0.70–0.84)**
- [ ] Accessibility decision explicit (barrierefrei vs rollstuhlgerecht units/quotas) — not defaulted
- [ ] Structural system chosen per Section 11 with reason; long-span/"open" rooms assigned their own grid bay; wall-vs-grid logic stated
- [ ] Acoustic level per DIN 4109-1 minima **plus** contracted VDI 4100 class where premium; party walls detailed as construction, not line
- [ ] Energy read: α band + H'T class for the type; summer-proof difficulty (region, mass, night vent) flagged at typology level
- [ ] Density/sealing stated (WE/ha, sealed share vs GRZ), Retentionsdach/PV reserve confirmed
- [ ] Expansion reserve (DG/KG/Aufstockung/Einlieger) decided per Section 14
- [ ] Parking count → TG arithmetic done before unit count frozen
- [ ] Cost stated as area × dated 2026 band **with** modifiers (Keller/TG/Schall/class) — not the bare rate
- [ ] Evidentiary tier on every number a client might act on
- [ ] **Disclaimer given**: planning study — Entwurfsverfasser + Standsicherheitsnachweis + Brandschutznachweis + Baugenehmigung before ground-breaking; restated unprompted if the user sounds ready to build

### 18.3 Phrases to use verbatim

| Situation | Say |
|---|---|
| Client cites an area/room figure | *"Which count is that — Wohnfläche per WoFlV with loggias at 50%, or BGF? I don't design to a number until I know its ruler."* |
| "Zimmer" ambiguity | *"Quick check — when you say 4 Zimmer, do you mean 4 rooms total (German count) or 4 bedrooms? That's a 30 m² difference and a different plot."* |
| Coverage wish exceeds plan | *"Your B-Plan allows ~X m² footprint and ~Y m² floor area. What you've asked for is ~1.3Y. Either the plates shrink, the DG comes into play, or we open a B-Plan conversation — but I won't draw to the optimistic number."* |
| Legal vs desirable massing | *"The plan would let you build to Z. On a plot like this I'd recommend building below it so the garden stays a room outdoors. Here's the cost delta of both."* |
| Big open room on wall logic | *"That span needs a beam-and-column bay inside the masonry house — visible, and priced. Cheapest option is a slightly smaller room; say the word and I'll design the frame bay instead."* |
| Client cites a GEG/DIN figure back to you | *"Those are the 2026 patterns from this library's tier system — your Land's current LBO edition and the B-Plan text govern. Verify before submission."* |
| Client about to build | *"This is a planning study, not a stamped submission. A bauvorlageberechtigter Entwurfsverfasser, a Standsicherheitsnachweis and the Baugenehmigung have to stand between this model and the excavator."* |

---

## Section 19: 3D/IFC Modelling Integration by Typology

Load the modelling/BIM skill of this library **before** writing any wall/window/door code. This section is the typology-specific overlay:

| Typology | Model hierarchy | Notes |
|---|---|---|
| EFH/DHH/RH | 1 Site (plot + Bauflucht + Abstandsflächen wires as Draft geometry) · 1 Building · Storeys KG/EG/OG/DG | **model the setbacks and the buildable envelope as a translucent box first** — every wall must live inside it; catches GRZ overshoot at model time instead of approval time |
| Row ensemble | 1 Site · 1 Building per unit + shared Site group; or 1 Building with N named unit groups | model one typical unit, then array along the party axis; the party wall object must be explicitly named/shared |
| MFH Zeile/Block | 1 Site · 1 Building · Parking/EG/Typ×N/DG | **model ONE typical floor properly then array**; name cores as separate storey-spanning groups — they are the typology's governing objects |
| Mixed use | Site · Building · groups per use + interface floor explicit | the transfer/system-change floor as its own visible object → structural review |
| Aufstockung | Bestand model (as-surveyed) · new-storey group · *deviation objects* | never mix survey and design in one wall — the reserve/uncertainty flag matters to the checker |

Gotchas that bite typology studies specifically: keep unit/core/Hof naming stable across exports (WoFlV vs DIN 277 area take-offs both key off object names); give the DG-reserve storey its own (zero-opex) group so the client can toggle "with/without"; model the Abstandsflächen box with **real Land coefficients** (0.4 vs 0.5×H differs by Bundesland) — a wrong envelope box validates wrong designs for the whole project.

---

## References

### Law & standards (T1/T2 — editions vary by Land and year; always verify)

- **Landesbauordnungen** (MBO pattern: Gebäudeklassen §2, Abstandsflächen §6, Rettungswege/Treppen/Aufzüge in the §33–39 range, Hochhaus definition §2 — **section numbers and editions differ by Land; always the state text, not this pattern**)
- **BauNVO** (area types, GRZ/GFZ caps, Bauweisen §16–23), **§34/§35 BauGB** (without-B-Plan / Außenbereich)
- **GEG 2020+** (Referenzgebäudeverfahren, H'T type ladder, ΔU_WB surcharges 0.03–0.10, airtightness n50 ≤ 3.0/1.5) — annex figures **VERIFY current version**
- **DIN 4108-2** (Mindestwärmeschutz, R minima, summer S-method, climate regions A/B/C), **DIN V 18599 parts 1/2/10** (typology parameters: EFH/MFH gains, a_tb, DHW), **DIN EN ISO 6946** (U) → methods in `building-physics-thermal-moisture`
- **DIN 4109-1/-31…-36** (Schallschutz minima incl. Haustrennwand values), **VDI 4100** (elevated classes) → `building-acoustics`
- **DIN 18065** (building stairs), **DIN 18040-2** (barrier-free dwellings), **DIN 18017-3** (windowless room ventilation), **II. BV lineage / WoFlV** (area counting & funding)
- **EN 1996-1-1/-3 + NA** (masonry, simplified-design envelope values quoted in 11.1), **EN 1992/1993/1995** per system → `masonry-construction`, `timber-steel-design`
- **TA Lärm area-type day/night limits** for mixed-use siting; municipal **Stellplatz-/Garagenverordnungen** and **Gestaltungssatzungen**; state PV/charging obligations (BW GEIG lineage as pattern — VERIFY yours)

### Typology & density (T3/T5)

- Neufert *Architects' Data*; *Metric Handbook*; Firley & Stahl *The Urban Housing Handbook*; Mozas & Fernández Per *Density: New Collective Housing* — density/plate/core theory layer
- German urban-form carbon comparisons (blockrand vs dispersed; sealing + commuting deltas) — single-study figures, **T5 verify**
- Exemplars: Weissenhof (Stuttgart 1927) · Unité d'Habitation (Marseille 1952) · Alexandra Road (London 1978) · Borneo Sporenburg (Amsterdam) · Goldsmith Street (Norwich 2019) — each illustrating one typology lesson named in 5.5/6

### Internal cross-references

`masonry-construction` · `timber-steel-design` · `structural-systems` · `structural-analysis` · `concrete-detailing` · `fire-protection-building` · `building-acoustics` · `building-physics-thermal-moisture` · `openings-windows-doors` · `roofing-waterproofing` · `geotechnics-foundations` · `building-materials` · `seismic-design` (DACH: low-seismic zones, Eurocode 8 map check)

**Market data (T4):** Wohnflächen, unit-size bands, mix tables, cost bands and Stellplatz expectations reflect DACH 2026 market convention from plan sets, developer standards and construction-cost references; they are **not law**, they overlap and drift — re-verify against current local sources before any client-facing quote.
