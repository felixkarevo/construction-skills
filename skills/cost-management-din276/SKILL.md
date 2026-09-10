---
name: cost-management-din276
description: >
  Construction cost management for buildings in the DACH region per DIN 276:2018
  (Kostengruppen 100–700 with subgroups 310–390 / 410–490, edition traps),
  Kostenermittlungsstufen and terminology discipline (Kostenrahmen,
  Kostenüberschlag, Kostenschätzung, Kostenberechnung, Kostenanschlag,
  Kostenfeststellung — and the outdated Kostenvoranschlag), benchmark logic
  (derive €/m² BGF / €/m³ BRI from local price levels and own Nachkalkulation —
  never copy foreign rates), unit-price buildup per KLR Bau (Lohngruppen,
  Mittellohn, Lohnzusatzkosten 85–95%, Gerät costs BGL-style, Stoffe, Gemeinkosten
  Zuschläge, BGK/AGK, two calculation methods, p→p′ conversion, Deckungsbeitrag),
  VOB/C ATV numbering (DIN 18299 general + 18300 earthworks … 18451 scaffolds,
  Neben-/Besondere Leistungen, Aufmaß/Abrechnung), quantity takeoff from a
  FreeCAD/BIM model (net volumes vs voids, rebar tonnage via properties,
  no-double-count rules, deduction thresholds), measurement and invoice
  discipline (Leistungsmeldung, prüfbare Schlussrechnung, §2 VOB/B quantity
  cases), offer comparison (Bieterpreisspiegel, Leitpositionen 20/80 rule,
  unusually-low-bid checks, Urkalkulation), contingency/Reserve and escalation
  logic, HOAI honorar (LPH 1–9 phase weights, anrechenbare Kosten, Honorarzonen,
  Zuschläge, post-2021 negotiability), life-cycle costs (operation share of
  total, maintenance intervals per system, static/dynamic cost comparison),
  worked examples (unit price, offer closing sheet, fee calc, model takeoff to
  estimate), failure patterns (BGF vs NF misuse, KG mixups, missing Erschließung
  and Nebenkosten) and checklists.
---

# Cost Management per DIN 276 — Estimating, Pricing, Tendering (DACH)

Cost management for buildings in Germany, Austria and German-speaking Switzerland is
governed by one spine: **DIN 276** structures *what* you count, **VOB/C** structures *how*
you measure and bill it, **KLR Bau** structures *how a unit price is built up*, and **HOAI**
structures *what planning costs itself*. This skill connects all four to a 3D model: the
geometry in a FreeCAD/BIM file becomes measured quantities (Mengen), quantities become
priced positions (Einzelpositionen), positions become Kostengruppen sums, and sums become
a budget you can defend, audit and update through the project lifecycle.

The reference currency is EUR (SI units: m², m³, t, h). Where digested example figures are
at a German price level, they illustrate the **method**, not a current benchmark. The
central rule of this file: **structure and arithmetic are transferable; price levels never
are.**

Values tagged **[VERIFY]** were extracted from tabular sources whose printed values could
be degraded, or are trade conventions rather than a single cited clause — confirm against
the primary standard (DIN 276:2018-12, VOB/C editions, HOAI text) before quoting in a
deliverable. Values tagged **[practice]** are site convention, not code.

---

## Reality Check — Advisory Role & Liability

**This skill produces cost-planning aids, pricing structures and calculation guidance for
budgeting, tender preparation and FreeCAD/BIM modelling ONLY.**

- Every quantity, rate, factor and plausibility band here is a **planning-stage aid**. It
  is not a Kostenberechnung with legal standing, not a tender document, and not a
  prüffähige Abrechnung.
- Binding cost statements for real projects — Baukostenvereinbarung, Förder-Anträge,
  Vergabe-Entscheidungen — must be prepared and signed by a responsible cost planner
  (Kostenplaner/in, Architekt/in or Ingenieur/in) against the **current editions** of
  DIN 276, VOB, HOAI and the applicable state building code. Several digested references
  predate VOB 2019/2024 and HOAI 2021 — paragraph numbering and fee law have moved.
- **HOAI is no longer binding price law.** A 2019 ECJ ruling held the fixed minimum/maximum
  fees incompatible with the Services Directive; since HOAI 2021 fees are freely
  negotiable and the tables are orientation values only. Never present an HOAI-table
  figure as a legally owed amount without checking the contract actually references it.
- A rate copied from another country — even another DACH city — is a different price
  level, a different wage agreement and a different VAT regime. Section 7 explains how to
  derive local benchmarks instead.
- **Behavioural rule:** never present a model export, a Bieterpreisspiegel row or a
  calculated EP as construction- or payment-ready. If the user's language treats output
  as final ("this is what we'll pay", "send this as the invoice"), state plainly, in the
  same reply, that a signed Kostenanschlag/Feststellung and contract-law review are
  required first. Do not bury it in a footnote.

---

## Section 1: The DIN 276 Cost Structure (Kostengruppen)

### 1.1 Levels and logic

DIN 276:2018-12 organises building costs in a strict three-level hierarchy:

```
Level 1   Gesamtkosten des Bauwerks (framework: 100 … 700)
Level 2   Kostengruppen (KG 100 … KG 700)
Level 3   Kostengruppen-Untergruppen (310 … 490 for the building; others per edition)
```

You are only allowed to compare, sum and report **within one level**. The single most
common structural error in student and draft estimates is adding a level-3 figure
("Stahlbeton 320+330") to a level-2 total ("KG 400") and calling the sum a budget.

### 1.2 Kostengruppen table (DIN 276:2018-12)

| Level 2 | Title | Level 3 subgroups (where fixed) | Typical content you must not forget |
|---|---|---|---|
| **100** | Grundstück | 110 Grundstückserwerb; 120 Baureifeschaffung / Herrichten (incl. Abbruch, Kampfmittelräumung) [VERIFY subgroup wording]; 130 Erschließung [VERIFY] | Purchase price, Kaufnebenkosten (Grunderwerbsteuer, Notar, Makler), demolition, ground remediation (Altlasten) |
| **200** | Herrichten und Erschließen | subcodes per standard **[VERIFY exact level-3 codes]** | Kampfmittel, Rodung, Geländeregulierung, **Erschließung bis Grundstücksgrenze** (Ver- und Entsorgungsanschlüsse, provisorisch/endgültig), Baustraßen/Anbindung |
| **300** | Bauwerk – Baukonstruktion | 310 Grubenaushub & Baugruben; 320 Gründungen & Unterbau (incl. Sohlplatte); 330 Außenliegende Bauteile (Fassade, Keller außen); 340 Innenliegende Bauteile (Wände); 350 Decken / Geschossdecken; 360 Dächer; 370 Installationsschächte/-wände, Galerien [VERIFY title]; 380 Einbauteile / sonstige Konstruktion [VERIFY]; 390 Maßhalten, Rückbau, andere | Aushub, Baugrubensicherung, Bodenplatte, Wände, Decken, Treppe, Dach, WDVS/Fassade, Fenster in KG 330 (Baukonstruktion — check project convention) |
| **400** | Bauwerk – Technische Anlagen | 410 Wasser/Abwasser/Gas; 420 Wärme / solar; 430 Lüftung/Klima; 440 Elektro; 450 Nachrichten-/Sicherheitstechnik; 460 Förderung (Aufzüge); 470 Nutzungsspezifisch (Küche, Labor, Bühne); 480 Gebäudeautomation; 490 Sonstiges | Alle TGA incl. Aufzüge (460!), Blitzschutz (440), WP + Speicher (420/430) |
| **500** | Außenanlagen **[VERIFY — extraction lists "Ausbaubereiche" at 500 in one edition]** | per edition; Wege, Grünflächen, Entwässerung, Stellplätze, Bäume | Freiflächen, Retention, Müllplätze, Außenbeleuchtung |
| **600** | Ausbaubereiche / Maßnahmen für den Betrieb **[VERIFY title vs edition]** | room-area driven; nicht dem Gebäude fest zugeordnet | Mieter-/Laborausbau, Innenausbau-Sonderwünsche |
| **700** | Baunebenkosten (Nebenkosten) **[VERIFY mapping — see 1.3]** | Planerhonorare (HOAI/AHO), Prüfstatik, Gutachten, Bauversicherung, Finanzierungszinsen während Bauzeit, Genehmigungsgebühren, Umzüge, MwSt-Differenzposten | **Honorare are a cost, not "free"**: HOAI-LPH 1–9, SiGeKo, Brandschutznachweis, Vermessung |
| beyond | Betriebseinrichtung / projektbezogene oder projektunbezogene Kosten (mobiliare Ausstattung, IT) — numbering (e.g. 710/760-style subcodes, or 800 "projektunbezogen" in older editions) differs | furniture, IT — excluded from "Baukosten" definitions |

> **Edition trap.** The meaning of level-2 codes above 400 changed across DIN
> 276:1990 / 2008 / 2018 (e.g. where Außenanlagen, Betriebseinrichtung and
> Baunebenkosten sit). **Every cost report must name its edition** — comparing a 2008
> "KG 600" with a 2018 "KG 600" silently mixes different contents. [VERIFY]

### 1.3 Anrechenbare Kosten (what HOAI fees are calculated on)

Per the mapping carried into HOAI (DIN 276:2008 numbering still governs): **net costs of
KG 100–700 excluding 110 (Grundstückserwerb), 710 and 760** [VERIFY against current §6
HOAI text]. Practical consequences:

- Fees are calculated on **net** figures — never mix Brutto into anrechenbare Kosten.
- Grundstück (110) and movable Betriebseinrichtung are **not** countable.
- KG 400 (TGA) fully countable only up to its customary share rule — in the worked
  example below TGA at exactly 25 % of construction cost was fully anrechenbar; beyond
  that the anrechenbarkeit of high-TGA buildings is a documented edge case **[VERIFY]**.
- mvB (Maßnahmen an bestehender Bausubstanz): anrechenbar = Menge × KKW (cost index per
  unit of comparable new build) × ZF (time value factor ≤ 1; typical 0.8–1.0 buildings,
  0.6–1.0 structures, 0.5–1.0 TGA) × LF (Leistungsphase factor — reduced in later phases;
  roughly 0.9 for LPH 1–5, 0.6 for LPH 8, 0.5 for LPH 9 per the worked scheme **[VERIFY
  exact LF table]**).

### 1.4 Kostenermittlungsstufen (KSEM) — and the terminology discipline

DIN 276 names a cost **determination stage** per planning phase. Using the wrong word is
using the wrong liability:

```
Bedarfsplanung (DIN 18205)      → Kostenrahmen
LPH 1 Grundlagenermittlung      → Kostenüberschlag      (pure index/benchmark guess)
LPH 2 Vorplanung                → Kostenschätzung       (estimate, ±20–30 %)
LPH 3 Entwurfsplanung           → Kostenberechnung      (basis for Baukostenvereinbarung
                                                          and HOAI anrechenbare Kosten)
LPH 4/5                         → no new stage — control vs Kostenberechnung
LPH 6/7 Vergabe                 → Kostenanschlag        (tendered total from real offers;
                              + "Vertragspreise"         delta vs Berechnung = planning
                                                          drift + price movement)
LPH 8 Ausführung                → Fortschreibung; Abschlagsrechnungen
Abnahme/Schlussrechnung         → Kostenfeststellung    (audited actual cost)
```

- Tolerance narrows from roughly **±20–30 %** (frame) to about **±3–5 %**
  (Anschlag/Feststellung) **[VERIFY bands — typical values]**. A significant deviation
  Kostenschätzung → Kostenberechnung triggers a documented plausibility analysis, not a
  quiet number swap.
- **"Kostenvoranschlag" is outdated DIN 276 vocabulary** (pre-2008 editions). Modern
  German cost planning distinguishes Kostenberechnung (planned, by the designer) from
  Kostenanschlag (offered, by the market). BGB and everyday speech blur them — in a
  deliverable, never mix the two.
- The **Reserve** of DIN 276:2018 (for costs not foreseeable at the time of determination)
  is shown **outside** the KG totals as a separately declared line — it is not a hidden
  7 % baked into each position [VERIFY current presentation convention]. See Section 9.

### 1.5 What "the cost of a house" means — pick your scope before you answer

| Question someone asks | DIN 276 scope to quote |
|---|---|
| "Baukosten" (construction cost) | KG 300 + 400 (+ 500 if asked) — net |
| "Herstellkosten" | KG 200–600, excl. property purchase |
| "Gesamtkosten projektbezogen" | KG 100–700 incl. Grundstück and Nebenkosten |
| "Investition" (developer) | + financing, + Betriebseinrichtung, + Reserve |

Quote the scope label together with the number, every time.

---

## Section 2: The Estimating Pipeline

### 2.1 When to invoke this skill

- Any "what will this building cost" question at any phase (1.4 sets the accuracy you owe)
- Building a Mengen list from drawings or a FreeCAD/BIM model
- Picking apart or comparing contractor offers (Section 8)
- Checking a unit price for plausibility (Section 5)
- Setting Reserve/contingency, escalation, allowances (Section 9)
- Fee questions: HOAI Honorar, anrechenbare Kosten (Section 10)
- Lifecycle decisions: material/variant comparison over 30–50 years (Section 11)

Pair with the structural, construction-detailing and BIM skills for member sizing,
specifications and model-to-quantity mapping.

### 2.2 Ten-step pipeline (method-neutral, DIN 276 output)

```
1.  FIX SCOPE & STAGE     → which Kostenermittlungsstufe (1.4)? which KG boundary (1.5)?
2.  FIX SPEC LEVEL       → simple / standard / premium — drives KG 330/360/400/600, not 320/350
3.  DEFINE AREAS          → BGF/NF per DIN 277; state the denominator (Section 3.4)
4.  MEASURE GROSS         → geometry only from drawings/model, no rates
5.  APPLY DEDUCTIONS      → openings/voids per visible rule, Section 3.1
6.  ASSIGN TO KGs         → every position gets one and only one KG 3xx/4xx code (1.2)
7.  BUILD UNIT PRICES     → Löhne/Geräte/Stoffe + GK + AGK + G (Section 5)
8.  PRICE & SUM           → Menge × EP → GP; roll up to level 2, then level 1
9.  SOFT COSTS            → KG 600/700: fees, surveys, tests, insurance, permits (Section 10)
10. RESERVE + ESCALATION  → separate declared lines sized to maturity & duration (Section 9)
```

**Never skip the step 4/5 separation.** Measuring net "by eye" (deducting while
measuring) is the single biggest source of unreproducible estimates. Gross first,
deductions as a visible line, net as the result — that is also exactly what VOB/C §5
Abrechnung demands.

### 2.3 Three-method triangulation rule

An estimate is only trustworthy when **three independent methods agree within ±10 %**.
If they don't, one is wrong — find which, do not average:

| Method | How | Use as |
|---|---|---|
| **A — Reference rate** | BGF × €/m² from local comparable projects (Section 7) | Fast sanity bound |
| **B — Detailed buildup** | Position takeoff × unit prices, mapped to KG 300/400 | The actual estimate |
| **C — Ratio check** | KG 300 share of total (typically ~60–70 % of 300+400+500+600 for simple buildings) or TGA ≈ 25–35 % of gross construction cost | Independent cross-check |

All three validate **arithmetic consistency**, not price truth — consistently wrong
inputs triangulate just as cleanly as correct ones.

---

## Section 3: Measurement Conventions & Deduction Rules

### 3.1 Deduction thresholds by work type (generic planning convention)

VOB/C ATV (Section 6) fixes what is deducted in the Abrechnung. For **estimating**,
apply the same logic so your Mengen match what you will later pay:

| Work | Deduct | Do NOT deduct | Add |
|---|---|---|---|
| Excavation (Aushub) | — | working space is measured **loose/with Verbau allowance**, not deducted | side allowance per shoring type; bulking on haul-off (+25–30 % loose factor) |
| Blinding (Sauberkeitsschicht) | — | — | plane + margin around foundation |
| Concrete (Beton) | voids > 0.1 m² **[VERIFY ATV 18331 threshold]** | reinforcement volume; openings ≤ threshold; chases/box-outs below threshold | — |
| Masonry (Mauerwerk) | openings > 0.1 m²; at **both** wall faces from > 1.5 m² (typical ATV logic) **[VERIFY]** | small chases; lintel/beam bearings below threshold | — |
| Plaster/Putze | openings — one face for single-face reveal, both faces through | below-threshold openings | reveals/jambs per ATV rules or lump |
| Screed/Estrich | column bases, fixed installations, openings | — | — |
| Formwork/Schalung | — | — | measured as **contact area only** (Berührungsfläche) |
| Paint | openings > threshold | — | grill/railing painted area × 2 for both faces |
| Facade insulation (WDVS) | window reveals per offer logic | — | state whether An-/-Abschluss is included |

**Deducting nothing "to be on the safe side" is not conservative** — it inflates
concrete and masonry 8–20 % on a window-rich façade and destroys your KG 330 plausibility
band.

### 3.2 Practical net factors (when detailed openings are not yet drawn)

| Element | Gross → net factor | Basis |
|---|---|---|
| External wall masonry/facade area | × 0.72 – 0.85 | 15–28 % opening ratio typical residential; offices up to 0.5–0.9 glazed |
| Internal masonry (load-bearing) | × 0.85 – 0.90 | door openings only |
| Partitions | × 0.80 – 0.90 | doors + shafts |
| Internal plaster | wall face gross × 0.80–0.85 + ceilings | applied on face area |
| Floor finishes | × 0.88 – 0.95 of BGF | minus walls; per DIN 277 area base declared |

Flag every net factor as an assumption and replace it with the real opening schedule the
moment elevations are drawn — a 5 % error in opening area is a 3–5 % error in façade cost.

### 3.3 Useful derived-quantity relationships (per m² BGF, compact residential [practice])

| Derived quantity | Multiplier on BGF |
|---|---|
| Internal plaster area (walls both faces + ceilings) | × 2.2 – 2.7 |
| External façade finish area | × 1.0 – 1.3 |
| Total paint/coating area | × 3.0 – 3.6 |
| Schalung contact area (all RC) | × 2.0 – 2.8 |
| Concrete volume incl. foundations | × 0.35 – 0.55 m³/m² (storey height, walls vs frame — wide!) |
| Rebar | × 30 – 60 kg/m² BGF (RC-frame residential; timber/steelframe far lower) |

These are **outcome plausibility bands for a derived takeoff** — never a substitute for
measuring. If your model gives 0.9 m³/m² concrete for a 3-storey house, something is
double-counted.

### 3.4 Area definitions — the denominator law (DIN 277)

| Term | Meaning | Use for |
|---|---|---|
| **BGF** (Bruttogrundfläche / Geschossfläche) | full footprint incl. walls, columns, shafts | DIN 276 reference-size logic, benchmark €/m² |
| **NGF / NF** (Nettogrund-/Nutzbare Fläche) | BGF minus wall/structural share | rents, room-based cost (KG 600) |
| **NRF** (Nettoraumfläche) | strict room surface | acoustic/comfort KPIs (CO₂e/m²·NRF·a) |
| **BRI / BRV** (Brutto-/Nettorauminhalt) | m³ | €/m³ benchmarks (heating, scaffolding, crane logic) |

**State the denominator on every rate.** A €/m² rate without "BGF or NF?" is the DACH
equivalent of a fight waiting to happen: NF/BGF efficiency is typically 0.65–0.80, so a
"per NF" benchmark applied to "per BGF" quantities swings the total by 15–35 %.

### 3.5 Wastage (Verschnitt) discipline

| Material | Allowance [practice] | Notes |
|---|---|---|
| Concrete | 2–5 % over plan volume | pump residue, formwork tolerance |
| Rebar | 3–5 % cutting **+ 4–6 % laps scheduled separately** | laps are not wastage — compute them |
| Masonry units | 3–8 % breakage/cutting | thin-joint precision masonry lower |
| Insulation boards | 5–10 % | more on complex façades |
| Tiles/screed pumps/rubber membranes | 8–15 % | pattern cuts |
| Timber | 10–15 % | section and grade dependent |

Wastage belongs in the **procurement/price calculation**, never added to the measured
Abrechnungsmenge the contractor is paid on. Keep two columns in the model export:
`Measured Qty` and `Procurement Qty`.

---

## Section 4: Takeoff from the FreeCAD/BIM Model

### 4.1 Model hygiene prerequisites

A model only produces a trustworthy Mengen list if it was built to produce one:

- Real spatial hierarchy: Site → Building → Storey → element
- Every element carries a role/type attribute (`Wall`, `Slab`, `Column`, `Beam`,
  `Footing`, `Stair`, `Window`, `Door`, `Roof`) **and** a target DIN 276 code in a custom
  property (e.g. `CostGroup = "330"`)
- Openings are live subtractions (bool/void), not frozen cuts — frozen cuts go silently
  stale when windows move
- No overlapping solids at beam–slab and column–beam junctions (the §4.4 double-count
  trap reappears as geometric overlap)
- Materials assigned per element so grades/systems separate

### 4.2 Volume takeoff bucketed by type + cost group

```python
# FreeCAD Python console — net volume takeoff by element role and CostGroup property
import FreeCAD as App
from collections import defaultdict

doc = App.ActiveDocument
vol = defaultdict(float)   # m³
cnt = defaultdict(int)

for o in doc.Objects:
    if not hasattr(o, "Shape") or o.Shape.isNull() or o.Shape.Volume <= 0:
        continue
    role = (getattr(o, "IfcType", None)
            or getattr(o, "Role", None) or "Unclassified")
    kg = getattr(o, "CostGroup", "unset")        # custom DIN-276 property
    key = f"{role}|KG{kg}"
    vol[key] += o.Shape.Volume / 1e9             # mm³ -> m³
    cnt[key] += 1

print(f"{'role|KG':<28}{'nos':>5}{'m3':>10}")
for k in sorted(vol, key=lambda x: -vol[x]):
    print(f"{k:<28}{cnt[k]:>5}{vol[k]:>10.2f}")

bad = sum(c for k, c in cnt.items()
          if k.endswith("|KGunset") or k.split('|')[0] == "Unclassified")
if bad:
    print(f"\nWARNING: {bad} objects unclassified or without CostGroup — "
          f"their volume is NOT in any Kostengruppe.")
```

### 4.3 Rebar tonnage from the model

Either of two routes — both legitimate, one is honest about its basis:

1. **Explicit rebars:** model bars as objects, mass = Σ Volume × 7850 kg/m³; bar linear
   mass check `W = d²/162 × L` (d in mm, W in kg/m — universal steel geometry, 7850
   kg/m³). Add laps (§3.5) as a visible extra row.
2. **Ratio-backed estimate:** member volume × assumed steel ratio, declared per element
   type:

| Element | kg per m³ concrete | ≈ ratio [practice] |
|---|---|---|
| Strip/isolated footings | 40–70 | 0.5–0.9 % |
| Raft / Bodenplatte | 70–120 | 0.9–1.5 % |
| Suspended slabs | 80–110 | 1.0–1.4 % |
| Beams | 110–140 | 1.4–1.8 % |
| Columns/walls (RC) | 120–200 | 1.5–2.5 % |
| Retaining/basement walls | 100–160 | — |

A tonnage derived from route 2 is an **assumption, not a BBS (Stahlliste)**. A real BBS
comes from the stamped structural design; nominal concrete cover bn per DIN EN 1992-1-1 /
DIN 1045-1 (exposure-class driven — typically 20 mm slabs interior, 30–40 mm
beams/columns **[practice]**) and lap-splice lengths (≥ 40–65 × bar Ø depending on
concrete, coverage and bar Ø) change tonnage by ±15 % more easily than any ratio here.

### 4.4 The double-count traps (model version)

1. **Beam–slab overlap:** either measure beams at full depth and slabs **net of beam
   plan area**, or beams at (D − t_slab) and slabs full. Pick one, write it into the
   script, state it in the notes. Both-full inflates concrete 4–8 %.
2. **Column–beam at joints:** column height clear-between-beams, or full height minus
   beam volumes — once.
3. **Foundation vs excavation:** backfill = excavation − (consumed volume below grade)
   − haul-off; never let the same m³ appear as backfill and as disposal.
4. **Wall vs window/door:** the opening subtraction must be live (§4.1); a "wall with
   holes already cut" plus another deduction row counts twice.

### 4.5 Reconcile model output before use

1. Check derived ratios per m² BGF against §3.3 bands
2. Cross-check at least two elements by hand takeoff (one vertical, one horizontal)
3. Resolve every `Unclassified` / `KGunset` object — unallocated volume is missing money
4. Export with **gross, deductions, net** as three visible columns
5. Never issue a Mengen list from a model that failed steps 1–4

---

## Section 5: Unit Price Buildup (Einheitspreis-Kalkulation, KLR Bau)

This is the core competence the market respects: an EP you can decompose can be
negotiated; an EP you can't is just a number.

### 5.1 The price stack

```
EKT  = Einzelkosten der Teilleistungen
       ├─ Lohnkosten            (crew wage incl. Zuschläge)
       ├─ Materialkosten/Stoffe (delivered, net of discounts, incl. losses)
       ├─ Gerätekosten          (machine time or apportionment)
       ├─ Nachunternehmer (NU)  (priced-in sub-contract scope)
       └─ Sonstige Kosten (SoKo)
     + BGK  Baustellengemeinkosten  (site overhead, % on EKT by cost type)
     + AGK  Allgemeine Geschäftskosten (head-office overhead)
     + G    Gewinn (profit — per KLR Bau 2016 risk "Wagnis" is folded in here, not
                     a separate element; BGB §650c still uses the older wording [VERIFY])
     ────────────────────────────────
     = Angebotspreis netto
     + USt 19 % [DE; AT/CH different]  → brutto
```

Skonto (cash discount) and Nachlass (negotiated reduction) sit **after** the price stack
and are economically different: 3 % Skonto for paying in 10 instead of 30 days is
3·360/20 ≈ **54 % p.a.** — never pay it unless the maths says yes.

### 5.2 Labour (Löhne)

- Construction wage cost = Tariflohn (Lohngruppen of the collective agreement) + Bau-
  zuschläge + overtime/night/Sunday/holiday premiums.
- **Lohnzusatzkosten (social-wage surcharge): 85–95 % on the Grundlohn** in practice —
  sickness, weather downtime, holiday/ALT levy mechanics. Charge it on productive hours
  of actual working days. **[VERIFY band; tariff-dependent]**
- Lohnnebenkosten per §7 BRTV-type rules (travel/meal allowances) are a further charge
  line for workers away from home.
- Symbols convention: `A` base → `AS` +Lohnzusatzkosten → `ASL` +Lohnnebenkosten →
  `AP/APS/APSL` +Polier (foreman) share.
- **Mittellohn:** because you cannot know the exact crew mix at tender time, price the
  **weighted average hourly cost** of the planned crew. Distinguish:
  - *Lohn ASL* — bare crew average (a digested worked example used ≈ 34 €/h),
  - *Kalkulationslohn* — average loaded with overhead and profit so the job recovers its
    Schlüsselkosten (same example: ≈ 64 €/h). **Never compare these two numbers across
    offers without knowing which one is quoted.**
- Aufwandswerte (man-hour values) anchor durations and crew prices — digested BAS-style
  bands **[VERIFY per current table collection]**:

| Task | Man-hours |
|---|---|
| Wall formwork (system) | 0.2 – 1.0 h/m² (conventional up to 1.2; framed 0.3–0.6; large-panel 0.2–0.5) |
| Slab formwork ≤ 25 cm | 0.40 – 1.0 h/m² |
| Column formwork | 0.9 – 1.8 h/m² |
| Rebar placing | footings 8–21, slabs 9–25, walls 12–27, beams 14–28, columns 15–30 h/t (finer bar → higher) |
| Cutting/bending in the shop | Ø<10: 9–11; 10–20: 6–8; >20: 4–6 h/t |
| Concrete placing (pump) | 0.3 – 0.8 h/m³; **+≈ 25 % if skip via tower crane** |
| Excavator trench | 4 – 20 m³/h sustained |

Values scatter strongly with site, crew and weather — validate against your own
Nachkalkulation data, and treat any contractor who claims half these values as either
brilliant or wrong.

### 5.3 Equipment (Geräte)

Machine hour/month cost = **Kapitaldienst + Instandhaltung** (BGL-style logic; price
basis of published lists drifts — re-verify current edition before quoting):

- Linear depreciation a = A / v (A = mean new price, v = Vorhaltemonate planned)
- Imputed interest **6.5 % p.a. fixed by the costing rules regardless of market**
  **[VERIFY current value]**
- Repairs split 30 % maintenance / 70 % repair; cost types ≈ 60 % labour (no social
  surcharges) / 40 % material
- Time units: 1 Vorhaltetag = 8 h; 1 Vorhaltemonat = 30 calendar days = **170
  Vorhaltestunden**
- Standstill (Stillliegezeit): first 10 days full A + V + repairs; from day 11: 75 % of
  A+V plus 8 % maintenance, repairs dropped
- Operators → Lohn group; fuels, transport, assembly/dismantling → SoKo or device rate
- Same machine can be **EKT** (excavator inside an earthworks position) or **BGK** (tower
  crane covering the whole shell phase) — decide per job, don't price it twice

### 5.4 Material (Stoffe)

Material cost = purchase price **after discounts** + freight to site + offloading +
cutting/scatter/break losses (the §3.5 wastage). Small consumables (nails, tie wires —
Hilfsstoffe) go to site overhead, not EKT.

### 5.5 Gemeinkostenzuschläge — the worked digested example (retaining wall)

Predetermined mark-ups applied to EKT by cost type:

| EKT type | GK-Zuschlag | Factor |
|---|---|---|
| Material + Geräte | 18.65 % | 1.1865 |
| Lohn | 40.12 % | 1.4012 |
| SoKo | 17.60 % | 1.1760 |
| NU | 15.50 % | 1.1550 |

**Position example — wall concrete (Wandbeton), EP 133.65 €/m³ @ 120 m³:**

```
Lohn      0.70 h × 34.07 €/h            =  23.85 €   (× 87.25 % BGK on Lohn variant →  34.80 total GK)
Gerät     10.00 €                       =  10.00 €   (× 1.1865)
Material  65.00 €                       =  65.00 €   (× 1.1865)
GK portion (BGK)                        =  34.80 €
──────────────────────────────────────────────────
EP netto                                = 133.65 €/m³   → GP = EP × Menge
```

(The surcharge set on this position differs from the retaining-wall table above — the
point is the **mechanic**: type-specific factors, visible buildup.)

### 5.6 Two calculation methods — and the p → p′ conversion

1. **Verfahren mit vorbestimmten Zuschlägen** (pre-set mark-ups): EKT × factor per type;
   fast; fits simple shell and most fit-out/Technik jobs.
2. **Verfahren über die Angebotsendsumme** (project-specific overhead): build the real
   BGK for *this* job from duration and site set-up, then push AGK + profit onto the
   final sum:

```
p  = (AGK% + G%) of Angebotsendsumme          e.g. 7 % + 5 % = 12 %
p′ = p · 100 / (100 − p)  auf Herstellkosten   e.g. 12 → 13.64 %  (NU-only: 10 → 11.11 %)
```

**Schlüsselkosten logic:** the overhead not directly attributable to positions
(= Angebotssumme − EKT) must be recovered somewhere. Pre-allocate factors on
material/device/SoKo/NU, and push the **residual onto labour** — this is why the
Kalkulationslohn (≈ 64 €/h in the digested job) can double the Mittellohn (≈ 34 €/h).
Consequence: **on a job with reduced labour share, the same absolute overhead costs you
more per unit** — the reason low-concrete, high-NU jobs must be re-loaded, not copy-priced.

Digested lesson from the same job: the pre-set-mark-up variant understated the project's
real BGK by ≈ 20 k€ (126 k vs 147 k) — method check essential, especially for
duration-sensitive shell work.

**Closing sheet (Schlussblatt) of the digested offer:**

```
EKT                  99,006.90 €
BGK                  30,695.40 €  (Einrichten 7,495 L + 2,500 G + standby 1,500
                                    + site mgmt 13,800 + operating 2,400 + AV 3,000)
Herstellkosten      129,702.30 €
AGK 7 % + G 5 % (→ p′ 13.64 % auf HK)   17,144.91 €  (NU parts 3 % only)
Angebotssumme netto ≈ 146,847 €  (+19 % USt)
```

### 5.7 Deckungsbeitrag & price floors

`DB = Erlöse − variable Kosten`. A marginal bid that only covers variable costs can be
rational **only if the job finishes within the fiscal year and fills otherwise idle
capacity** — construction firms typically cross their fixed-cost break-even only in Q4.
Liquiditätsuntergrenze (short-term floor): profit can go to 0 and A+V on owned devices
can be dropped for short jobs; below that you are financing the client.

### 5.8 Universal physical constants for buildup (transferable)

| Item | Value |
|---|---|
| Concrete wet→dry volume factor | × 1.52–1.57 (use 1.54 for mortar-free estimating) |
| Mortar wet→dry factor | × 1.27–1.33 (use 1.30) |
| Steel density | 7,850 kg/m³; bar mass W = d²/162 kg/m |
| Concrete unit weight (RC, for transport/crane) | 25 kN/m³ ≈ 2,500 kg/m³ |
| Fresh concrete lateral pressure | DIN 18218 logic, γ = 25 kN/m³, rise ≤ 7 m/h |
| Excavated soil swell | fS ≈ 1.1–1.3 (loose vs bank); compaction factor fV < 1 |
| Water demand M20-class | ≈ 160–200 l/m³ (admixture-dependent) |
| Binder content guide [practice] | XC2-class slab/footing ≈ 280–340 kg/m³; C30/37+ design mix via ready-mix; exposure class (DIN EN 206: X0/XC/XF/XA/XS) governs minimum, not habit |

---

## Section 6: VOB/C — ATV Numbering, Nebenleistungen, Aufmaß

### 6.1 What VOB/C is for cost people

VOB/C (ATV — Allgemeine Vertragsbedingungen für Bauleistungen) per trade defines *how to
build* and, in its section **5 "Abrechnung"**, *how it is measured and paid*. Ignoring it
is both a defect and a billing error.

- **DIN 18299** = the general ATV, always applies where a trade-specific ATV is silent
  (special prevails). Structure of every ATV: `0 Hinweise (not contract) · 1
  Geltungsbereich · 2 Stoffe/Bauteile · 3 Ausführung · 4 Neben-/Besondere Leistungen ·
  5 Abrechnung/Aufmaß`.
- Trade ATVs run **DIN 183xx–184xx**. Numbering relevant to a house estimate
  (per digested index — confirm current list):

| ATV | Trade | ATV | Trade |
|---|---|---|---|
| 18299 | general rules | 18352 | tiles/slabs |
| 18300 | earthworks (Erdbau) | 18353 | screed |
| 18330 | masonry (Mauerwerk) | 18355 | joinery/cabinets (Tischler) |
| 18331 | concrete works (Beton) | 18356 | parquet |
| 18332 | natural stone masonry | 18357 | sanitary fittings |
| 18334 | carpentry/timber | 18358 | shutters |
| 18335 | steelwork | 18360 | metalwork (Metallbau) |
| 18336 | waterproofing (Abdichtungen) | 18361 | glazing |
| 18338/18339 | roofwork / sheet metal | 18363 | painting & coating |
| 18340 | drywall | 18365 | floorcoverings |
| 18345 | composite insulation (WDVS) | 18366 | wallcoverings |
| 18349 | concrete restoration | 18379–18386 | HVAC, heating, water/gas, electrical, lifts, automation |
| 18350 | plaster | 18451 | scaffolding |

### 6.2 Nebenleistungen vs Besondere Leistungen — where "all incl." really ends

- **Nebenleistungen (ATV §4.1):** trivial extras paid *inside* the EP — offcuts,
  fixing at position, scaffold-level work up to stated height, cleaning.
- **Besondere Leistungen (ATV §4.2):** only paid if **tendered as their own position**
  (or provably ordered): extended scaffold times, special formwork, shop drawings,
  mock-ups (Probeflächen), maintenance handover, extra shifts.

The most expensive tenders are won by bidders who *did* price §4.2 items the client
assumed were "included", then refuses bidders who silently left them out. Audit any offer
for the §4.2 list of the relevant ATVs — it is a standardisation cheat-sheet.

### 6.3 Aufmaß, Leistungsmeldung, Rechnung

- **Aufmaß** = the joint dimensional record (or verifiable unilateral with agreed
  tolerance); it is the *only* quantity that gets paid. Common units per ATV: m³ (concrete,
  earth), m² (wall, floor, façade, formwork as contact area), m (skirtings, pipes, rails),
  St/No. (fixtures, openings sets), t (steel), Psch/Hz (lump/hour).
- **Leistungsmeldung** (progress report for Abschlagsrechnung): measured quantities ×
  EP + agreed claims + approved hourly work (Stundenlohn, needs prior agreement — the
  §2(10) VOB/B rule; deemed-approval fictions are AGB-fragile **[VERIFY current case
  law]**); partially done positions at completion %; material-on-site claimable reduced
  by the cost of installing it; minus deductions.
- **Schlussrechnung must be prüfbar (§14 VOB/B):** follows the LV structure, attach
  Aufmaß and amount computations, highlight Nachträge. The client's Prüfungsfrist
  (typically 30/60 d) runs from receipt of a *prüfbare* bill; objections raised too late
  kill the withholding defence.
- **Quantity deviations §2(3) VOB/B** (unit-price contract) — the four-case logic:
  - ±10 % band: contract EP unchanged (AN's risk / AG's benefit).
  - Qty < 90 %: AN may demand EP increase — lost BGK/AGK/G re-spread over smaller qty
    (unless duration shortened).
  - Qty > 110 %: up to 110 % at contract EP; above, new EP with cost saving typically
    passed on (no capacity strain) unless AG forced acceleration (§2(5)).
  - Offset over/under-recovered Schlüsselkosten across positions at final account —
    agree a global re-spread ("in anderer Weise") to avoid position-by-position repricing.

---

## Section 7: Benchmarks & Plausibility — Derive, Don't Copy

### 7.1 The copying problem

There is **no digested, current, defensible €/m² benchmark table for building types in
this skill** — published national index values drift by region, price year and scope
definition, and copying a rate from another country (or an older handbook) into a live
estimate is the classic failure (Section 13). What transfers is the **derivation method**:

### 7.2 How to derive local unit-rate benchmarks

1. **Nachkalkulation database:** every completed job, roll final costs (Kostenfeststellung
   per KG 300/400) ÷ BGF and ÷ BRI → your own €/m² and €/m³ bands per building type. Two
   comparable projects beat any published table.
2. **Normalise before comparing** — for each figure, force: price year + index adjustment,
   net vs gross, which KGs included (Baukosten vs +NK vs +Grundstück), BGF definition,
   storeys/GB-Klasse, spec tier. Never compare lump sums; only normalised rates.
3. **Bottom-up floor from unit prices:** KG 320+330+350+360 of a plain shell ÷ BGF gives
   the *structural* €/m² your market can actually produce; benchmarks below that floor
   are scope errors, not savings.
4. **Developer-side cross-check (illustrative parameters from a worked valuation model,
   not a benchmark):** construction + side costs ~2,000 €/m² BGF *assumed*, +14 %
   "Unvorhersehbares" on total investment, rents and yields per local market — use the
   residual method only to sanity-test order of magnitude. [VERIFY scope]
5. **Tolerance expectations per stage** (Section 1.4) — a benchmark ±25 % against your
   Kostenberechnung at LPH 3 is not news; the same at LPH 7 is an emergency.

### 7.3 Plausibility toolkit (bid & cost control)

| Check | Rule / band | Source of confidence |
|---|---|---|
| Leitpositionen | ≈ 20 % of LV positions carry ≈ 80 % of the bid sum — the planner must personally verify the Aufwandswerte of exactly those | digested method |
| TGA share | KG 400 ≈ 25–35 % of gross construction cost (high-tech builds beyond) | digested example + method |
| Hülle + Ausbau ≈ Rohbau | modern-cost trend: façade/fit-out ≈ shell cost | digested observation |
| Site power | ≈ 0.6 % of build cost | digested |
| Schalung | ≈ 25 % of shell RC works | digested (region-specific) |
| Rebar ratio | §4.3 kg/m³ bands; whole-building kg/m² BGF (§3.3) | [practice] |
| Concrete ratio | 0.35–0.55 m³/m² BGF compact residential RC frame | [practice] |
| Labour/equipment mix | Kalkulationslohn vs Mittellohn disclosure (§5.2) | digested |
| Wage loading | any Lohnansatz below tariff + 85 % social surcharge → probe it | digested |
| Waste logistics | construction/demolition ≈ >1/3 of EU waste streams; disposal is a real line | digested context |

**Unusually low bids:** public clients have a statutory clarification duty (§16d VOB/A /
§60 VgV-type) — and so should you. The bidder must *prove* the price works; a bid 15–20 %
under the reference line without an explanation is an unpaid change-order generator.

---

## Section 8: Tendering & Offer Comparison (Bieterpreisspiegel)

### 8.1 What must be in the tender pack

1. LV (Leistungsverzeichnis) — positions with §6.2 §4.2 completeness, units per ATV
2. Approved/execution drawings (revision-numbered) handed to bidders
3. Rahmen-/Terminplan with milestones; BE (site setup) responsibilities split
4. Vertragsbedingungen: VOB/B **adopted whole or not at all** (partial adoption loses the
   AGB-privilege — clause-by-clause review applies [VERIFY case law])
5. Bindefrist (binding period) — state it; late award past it shifts Bauzeit and price
6. Urkalkulation submission (public: often required/deposit; private: demand it — see 8.3)

### 8.2 Pre-award bidder checklist (from the digested risk-screen)

Screen every tender for: payment/billing modalities; Vertragsstrafen (LDs — 0.3 %/AT over
completion date with 5 % cap is the admissible pattern, 0.5 % invalid **[VERIFY current
case law]**); Sicherheitseinbehalte; deletion of VOB/B clauses; §4.2 Besondere
Leistungen inclusion; shop-drawing delivery duties; local site conditions. Ask
clarifications **before bidding** (Bieterprüfungspflicht — silence can be priced against
you).

### 8.3 Bieterpreisspiegel structure

```
| Pos | Beschreibung (ATV)          | Einheit | Menge | FH  | BIeter A | B | C | Min | Δ zum Min % | Referenz (eigene KV) | Δ % zur Ref |
|-----|-----------------------------|---------|-------|-----|----------|---|---|-----|-------------|----------------------|-------------|
| 330.01 | WDVS 16 cm, inkl. §4.2   … | m²    | 820   | 1-2 |  96.40   |…  |…  | 92.10 | 4.7 %       | 94.00                | −2.7 %      |
| ...  (Leitpositionen first — top 20 % by value, ~80 % of sum, §7.3)
|      | SUMME Netto (LV)            |         |       |     | 512,300  |…  |…  |     |             | 505,000              |             |
|      | Nachlässe % / Skonto        |         |       |     | 2 / 3-10 |…  |…  |     |             |                      |             |
|      | Angebotssumme netto         |         |       |     |          |   |   |     |             |                      |             |
|      | Bindefrist / Nebenangebote  |         |       |     | yes/no   |   |   |     |             |                      |             |
```

Evaluation discipline:

- Compare **position-wise first, total last** — a "cheapest" total with 30 % overpriced
  early positions is a front-loaded cashflow trap (compare each position's % of total
  against your Kostenberechnung distribution).
- Row minima alone don't award; award to the economically most advantageous offer
  (quality/term/price criteria published in advance; for public: net price basis).
- Deviation bands for a residential shell: **±7 %** normal spread; **+8–15 %** itemise
  and negotiate; **> +15 %** retender; **−8…−15 %** check exclusions/spec cuts;
  **< −15 % red flag** → missing scope or claim-driven bidding. [practice thresholds]
- Insist on the **Urkalkulation** of the intended winner for the Leitpositionen — it
  stops speculative pricing and is your defence line for §2(5)/(6) and §650c BGB
  change-order valuation ("Herkunft der Preisformation").

### 8.4 Payment, retention, securities (contractor-economics literacy)

| Instrument | Basis | Practical value |
|---|---|---|
| Vorauszahlung (advance, e.g. long-lead material) | §16(2) VOB/B | secure it (bank guarantee) |
| Abschlagszahlung | §16(1) VOB/B / §632a BGB; due 21 d after prüfbare Aufstellung | pay against Leistungsmeldung + Aufmaß only |
| Schlusszahlung | ≤ 60 d after receipt (§16(3)) | hold Prüfungsfrist discipline |
| Default | §286 BGB: 30 d after invoice+due; interest +9 pp above base rate (B2B) | date everything |
| Vertragserfüllungssicherheit | ≤ 5 % of award (old §9c VOB/A numbering [VERIFY current]) | guarantee preferred over retention |
| Mängelansprüche-Sicherheit | ≤ 3 % of final account; retention max ~10 % total; client deposits into Sperrkonto within 18 Werktage; interest to contractor | or release against guarantee |
| Aval fee | 0.5–1.0 % p.a. of sum — consumes credit line | cheaper than long retention |
| Verbraucherbauvertrag (private client) | Abschläge ≤ 90 %; first payment needs 5 % performance security; Baubeschreibung + Widerrufsbelehrung | mandatory on consumer builds |

---

## Section 9: Reserve (Contingency), Allowances & Escalation

### 9.1 Reserve by design maturity

| Stage / condition | Reserve | Rationale |
|---|---|---|
| Konzept / Kostenüberschlag | 20–25 % | scope itself uncertain |
| Vorplanung / Kostenschätzung | 15–20 % | quantities ±20 % |
| Entwurfsplanung / Kostenberechnung | 10–15 % | most details unresolved |
| **Execution drawings + known site + tenders in** | **5–10 %** | new-build standard |
| Complete docs + firm prices + documented site | 3–5 % | floor — never below 3 % |
| Retrofit/UMF without as-builts | 10–25 % | hidden conditions; Altlasten risk |

Reserve reduces as certainty increases — carry high early and **formally release** the
difference at each stage; do not silently keep 25 % and spend it as profit. DIN
276:2018 shows the Reserve **outside** the KG sums as its own declared line
[VERIFY presentation], so nobody "finds" it inside a position.

### 9.2 What Reserve does and does not cover

| Covers | Does NOT cover (name it separately) |
|---|---|
| quantity drift within defined scope | client scope change → Nachtrag (§2(5)/(6), §650b) |
| minor unforeseen site conditions | major ground/contamination risk → risk allowance, often KG 100/200 |
| small rate variations | escalation (§9.4) |
| coordination gaps | rework from design error → professional liability, not the client's pot |
| weather within normal range | force majeure / higher force (contract-specific) |

Track drawdown as a visible line: 40 % complete + 80 % of Reserve spent = re-forecast,
don't carry on hoping.

### 9.3 Allowances & PS

| Type | Use | Treatment |
|---|---|---|
| Provisorische Position / PS | scope defined, spec open (kitchen, FA-Branding) | carry at face value; reconcile at actuals |
| PO (Posten mit Unbestimmter Anzahl / loose-sum item) | decision pending (Ausbau, lighting) | state it; overrun is client's |
| Stundenlohnarbeit | small undefined extras | cap it; requires prior agreement, hourly sheets within days |

### 9.4 Escalation (price adjustment)

A separate line from Reserve, sized on the material-weighted part of cost over the
**programme midpoint**:

```
Escalation ≈ Base cost × material share (~0.5–0.6 construction cost)
             × expected p.a. build-price index × (duration_years / 2)
```

| Programme | Typical allowance [practice] |
|---|---|
| ≤ 6 months | 1–3 % |
| 9–12 months | 3–5 % |
| 15–24 months | 6–9 % — and/or a price-adjustment clause (Stoffpreisgleitklausel logic for public work) |
| > 24 months | 10 %+ plus indexed contracts |

Hedge: early procurement/lock-in of the two most volatile bulk goods (cement-class
materials, steel) often beats carrying the allowance — cost the decision (storage,
working capital, deterioration) explicitly.

---

## Section 10: HOAI — Architects' & Engineers' Fees

### 10.1 Status

HOAI is (since 2021, after the ECJ ruling) **orientation, not price law** — fees are
freely negotiable. Without any fee agreement, statutory minimum rates historically apply
(irrefutable §7(5) mechanism **[VERIFY post-2021 effect]**); always put the fee, Leistungsbild,
zone and anrechenbare Kosten in writing at award.

### 10.2 The nine Leistungspflichten (LPH) and phase weights

`1 Grundlagenermittlung · 2 Vorplanung · 3 Entwurfsplanung · 4 Genehmigungsplanung ·
5 Ausführungsplanung · 6 Vergabevorbereitung · 7 Mitwirkung bei der Vergabe ·
8 Objektüberwachung · 9 Objektbetreuung/Dokumentation`

Phase weights for **Objektplanung Gebäude** (HOAI-2013 table, % of full fee — sums 100):

| LPH | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
| % | 2 | 7 | 15 | 3 | 25 | 10 | 4 | 32 | 2 |

Other disciplines have different distributions (IngBauwerke weight LPH 2–3 much higher,
Tragwerk LPH 5 heavy) — **[VERIFY each column against current HOAI annexes before use]**.
Cost truth: **≈ 54 % of the fee is spent by end LPH 5** while ≈ 80–90 % of construction
cost decisions are locked by LPH 3 — which is exactly why cost work concentrates there.

### 10.3 Fee buildup — five steps (worked digested example)

```
1 anrechenbare Kosten (net)      infill 3-storey building: KG300 800k + KG400 200k = 1.0 M€
  (TGA fully countable at exactly 25 % share of construction cost — see 1.3)
2 Honorarzone per Merkmalskatalog 34 pts → HZ IV
3 Grundhonorar from degressive table: HZ IV @ 1.0 M€ → min 144,268 € / max 162,464 €;
  Mittelsatz = (144,268+162,464)/2 = 153,366 €
4 × phase share: LPH 1–4 = 2+7+15+3 = 27 %  → 153,366 × 0.27 = 41,408.82 €
5 + Zuschläge (Umbau +20 % default presumption on mvB; AHO category method up to ≈ 33 %
  for HZ I–III [VERIFY current AHO wording]) + Nebenkosten (expenses) + VAT
```

Zone corridors per the digested catalogue: 6–8 → I, 14–16 → II, 22–28 → III,
34–36 → IV, 42 → V (criteria: Einbindung, Funktionen, Gestaltung, Konstruktion,
techn. Ausrüstung, Ausbau, each 1–9) **[VERIFY against §35 HOAI]**. Table ceilings:
Gebäude/Tragwerk/Verkehr 25/15/25 M€, TGA 4 M€, Freianlagen 1.5 M€; above → free
negotiation (extended degressive tables exist to ~500 M€ by agreement).

### 10.4 Cost-side rules of thumb

- Fee for Besondere Leistungen (extra reports, certification coordination, BIM management
  beyond standard) and for services outside the tables (Brandschutz, SiGeKo,
  Projektsteuerung per AHO, Gutachten) is **free** — quote and contract separately.
- Multiple similar objects: separate fees; essentially-same objects get repeated-phase
  reductions (≈ 50 % LP1–6 for the 1st–4th, 60 % 5th–7th, 90 % beyond) [VERIFY].
- Fee falls due at **Abnahme + prüfbare Honorarschlussrechnung**; time charges (no more
  HOAI hourly rates — internal cost rates): digested office example ≈ 106 €/h for a 12-y
  project engineer using gross-salary × 2.5–3.0 overhead factors.
- A fee agreement is void if it misses: correct Leistungsbild, anrechenbare Kosten per
  DIN 276, zone, rate, performed services, surcharges/deductions.
- §650p BGB Zielfindungsphase (A/I contracts): if goals are essential-undefined, the
  planner first owes a basis + cost estimate **for a fee** — the anti free-pitch rule;
  relevant whenever you are asked for "just a quick number" before contract.

---

## Section 11: Life-Cycle Cost (LCC)

### 11.1 The share logic

```
Herstellung (KG 200–700)  <<  Nutzung (Betrieb + Instandhaltung über 30–80 a)
```

- Greenhouse-gas analogue: offices ≈ **75 %** of lifecycle GHG is operation; residential
  ≈ **60–2/3** — and falling as grids decarbonise, which flips the problem toward
  **grauE Emissionen (embodied)**. **[VERIFY shares; dated studies]**
- Cost analogue from the digested literature: **operating costs equal the purchase
  (construction) cost after roughly 7 years** — a 50-year building therefore carries an
  order of magnitude more operating than construction cost (assumption-dependent; tag
  dated). The planning consequence: **decisions that shift 5 % construction cost but
  15 % operating cost are construction-cheap and LCC-expensive.**
- LCC rail: DIN 276:2018 cost groups (esp. 300/400) + DIN 18960 Nutzungskosten (Energie,
  Wasser/Abwasser, Reinigung) + Inspektion/Wartung/Instandsetzung per DIN 31051 terms
  (Wartung ≠ Instandsetzung ≠ Verbesserung/Modernisierung).

### 11.2 Static cost comparison (the digested floor-covering method)

40-year horizon, 2 % interest, annuity-style (kalk. Abschreibung + half-interest +
cyclic maintenance + cleaning 5–6 €/m²·a):

| Covering | Invest € /m² | Nutzungsdauer a | Cyclic costs | €/m²·a over 40 a |
|---|---|---|---|---|
| Carpet | 10 | 10 | — | 6.10 |
| Parquet | 60 | 40 | seal 8 €/m²/10 a; sand 20 €/m²/20 a | 9.20 |
| Natural stone | 80 | 60 | joints 15 €/m²/20 a | 9.78 |

**Reading:** the 6× cheaper carpet is only ~30 % cheaper *per year* — and that ignores
replacement disruption. Always compare variants on the annualised column, never the
investment row. Extend to building systems: heat-pump vs district-heat vs PV combos;
complexity (Performance Gap: installed systems underperform) counts as a cost, not a spec.

### 11.3 Maintenance intervals & lifetimes (per system, digested)

| System | Use life / interval [VERIFY, dated sources] |
|---|---|
| Building cycle (refurbishment trigger) | 50–80 a; structure far longer, TGA far shorter |
| TGA in stock | ≈ 30 a cycle → **two TGA lifetimes per shell lifetime** — plan access & exchange routes |
| Windows | 40–50 a frames; gasket/hardware/glazing shorter; repair vs replace per condition |
| WDVS | 40–60 a; **< 10 a if defective/unmaintained** — coating cycles are the lever |
| Anchors/adhesives in façades | plan 25 a → 2 cycles over 50 a doubles CO₂ and cost of that layer |
| Clay/brick masonry | 100–150 a; 94 % re-use/recycling paths exist |
| Vented/rainscreen façades | VDI 6200: owner walk-by 2–3 a, expert inspection 4–5 a, full review 12–15 a |
| PV | energy payback vs 25–30 a life; yield up to ~20× production energy over life |
| Maintenance strategy | DIN 31051 (Inspect/Wartung/Instandsetzen/Verbessern); design maintenance access — complex systems avoid |

### 11.4 Green premium — what's actually evidenced

- The premium sits in **rent and asset value**: offices ≈ +6–8 % rent / +14–16 % asset
  value in the digested survey (dated). For **residential construction cost**, the
  digested material gives **no evidence of a systematic green premium** — and the
  low-tech/sufficiency findings point the other way (reduced complexity and
  comfort-standard trimming save ≈ 10 % construction cost in the Gebäudetyp-E logic).
  Plan sustainability with LCC arithmetic, not with premium folklore.
- Carbon pricing for the calculation side: national levy 45 €/t CO₂e (2024, dated); UBA
  shadow price 237 €/t CO₂e (purchasing-power 2022; intergenerational-weighted variants
  809–860 €/t); one state mandates ~250 €/t in LCA for public builds **[VERIFY current
  values/regions]**. EPBD path: mandatory lifecycle-GWP reporting for new buildings
  > 1,000 m² users from 2028, all new from 2030 — an eLCA-style calculation is becoming
  a deliverable adjacent to the Kostenberechnung; model quantities (Section 4) are its
  input.

---

## Section 12: Worked Examples

### 12.1 Model → estimate pipeline (compact residential, illustrative)

Scope: 4-storey RC-frame residential, BGF 1,450 m², BRI 4,200 m³, standard spec, LPH 3.

**Takeoff (model, §4 logic; net = gross − visible deductions):**

| KG | Position (ATV) | Unit | Gross | Deduct | Net |
|---|---|---|---|---|---|
| 310 | excavation incl. shoring allowance (18300) | m³ | 860 | — (loose factor in haul-off line) | 860 |
| 320 | blinding 8 cm (18331) | m³ | 34 | 0 | 34 |
| 320 | foundation slab 30 cm C25/30 XC2 (18331) | m³ | 152 | 2 | 150 |
| 320 | footings/strips | m³ | 96 | 0 | 96 |
| 340 | interior walls RC/stone | m³ | 188 | 14 (open. > thr.) | 174 |
| 330 | exterior walls masonry + WDVS carrier | m³ | 205 | 31 | 174 |
| 350 | slabs 20 cm (18331, net of beam overlap — method stated) | m³ | 290 | 8 | 282 |
| 360 | flat roof structure incl. falls | m² | 390 | 6 | 384 |
| — | **RC total (320+340+350)** | | | | **702 m³ → 0.48 m³/m² BGF ✔ (§3.3 band)** |
| — | **rebar (ratios §4.3: slab 95, wall 150, footing 55)** | t | | | **≈ 58 t → 40 kg/m² BGF ✔** |
| 400 | TGA allowances (410–480, benchmarked) | PSch | — | — | sized to 28 % of KG 300+400 (§7.3 band) |

**Pricing with §5 mechanics** (local price level placeholders — replace every unit rate
from your own data before use):

```
Example EP, slab concrete C25/30 pump (18331):
Lohn 0.55 h × 42 €/h (KalkLohn local)      = 23.10
Gerät 1.20 € + Material 78 €               = 79.20
EKT                                        = 102.30 × GK(≈ 20/40 % split) → ≈ 124 €
AGK+G via p′ (12 % → 13.64 % auf HK)       ≈ +16.9 €
EP ≈ 141 €/m³ → GP = 282 m³ × 141 ≈ 39.7 k€
```

Roll all positions → KG 300 ≈ (illustrative) X; KG 400 ≈ 0.28·(X+Y); KG 200 + 500 + 600
per scope list; KG 700 from Section 10; Reserve per §9.1; output on the §14.2 sheet.

**Plausibility exit:** total ÷ BGF compared **only** against §7.2-derived local bands;
triangulation (§2.3) A/B/C within 10 % or investigate.

### 12.2 Unit price with overhead push-down (the digested retaining wall)

Already built line-by-line in §5.5/§5.6: EKT → GK by type → Herstellkosten → project BGK
table → p′ conversion → Angebotsendsumme. Use the Schlussblatt skeleton for **any** bid:

```
Positions-EKT by type (Lohn / Stoff+Gerät / SoKo / NU)
+ BGK:  Einrichten/Räumen · Vorhaltekosten(duration × monthly standby) · örtliche
        Bauleitung · Betrieb · technische Bearbeitung   ← time-dependent items = duration
+ = Herstellkosten
+ AGK+G  (as p′, or project-derived for long jobs)
+ Wagnis considerations inside G; Skonto/Nachlass at end
= Angebot netto → + USt
```

If the bid is won on labour-pushed rates, keep the **Urkalkulation** — every later
Nachtrag (§650c BGB: actual necessary costs + appropriate AGK/W/G surcharges, or
continuation from the deposited Urkalkulation) is argued from it.

### 12.3 HOAI fee (LPH 1–4) — digested example

See §10.3 worked figure: **1.0 M€ anrechenbar → HZ IV → Mittelsatz 153,366 € → LPH 1–4
(27 %) = 41,408.82 €** before Zuschläge and VAT. Recompute with the current negotiated
rate — the table values are orientation (§10.1).

### 12.4 Quantity-deviation bill correction (§6.3 mechanics)

Slab concrete contracted 120 m³ @ 133.65 €; as-built 160 m³ (+33.15 %):
first 110 % at contract EP; the 33 % surplus portion re-priced with recovered overhead:
(0.3315 − 0.10) × 120 × [0.5·34.07·0.8725 + 10·0.1865 + 65·0.1865] ≈ **801 €** additional
charge in the digested example — i.e. **the client captured most of the saving; only the
AGK/G tail moved**. Same logic, opposite sign, for quantities below 90 %.

---

## Section 13: Failure Patterns

| # | Failure | Consequence | Fix |
|---|---|---|---|
| 1 | Benchmark €/m² **BGF** applied to **NF**-sized areas (or vice versa) | ±15–35 % swing; "copy-paste errors" look like planning genius or fraud | §3.4: denominator law |
| 2 | Mixing Kostenermittlungsstufen — "Kostenvoranschlag/Kostenanschlag" used for a Schätzung | wrong liability; budget promise you never made | §1.4 terminology discipline |
| 3 | KG mixups: lift in 300 not 460; Fenster in 400; Fassade in 350; Betriebseinrichtung inside "Baukosten" | structure unreadable, TGA/facade shares uncheckable | §1.2 assign each position one code |
| 4 | Edition drift (2008 vs 2018 500/600/700) silently mixed | totals non-additive | name the edition in the report |
| 5 | Missing **Erschließung** (KG 200: Anschlusskosten, Herrichten, Kampfmittel) or treating it as "utility's job" | late five-figure surprises | §1.2 content list; ask network operators early |
| 6 | Missing KG 700: HOAI, Prüfstatik, SiGeKo, Vermessung, insurance, interim financing | "over budget" though build cost on target | §10 costs are a real line |
| 7 | Copying foreign/city rates (incl. this file's digested € figures) | systematic error at local price level | §7.2 derive locally |
| 8 | Beam/slab or wall/window double-count in model | concrete +4–8 % | §4.4; script declares the method |
| 9 | Gross measured directly as net; deductions invisible | unreproducible estimate | §2.2 three-column discipline |
| 10 | Wastage inside paid Menge / not in procurement | contractor paid for waste, or you run short | §3.5 two columns |
| 11 | Reserve merged with escalation ("7 % misc") | unmanageable, unreleasable | §9.1/§9.4 separate lines |
| 12 | §4.2 Besondere Leistungen assumed "all incl." | change-order war at Abrechnung | §6.2 audit each offer |
| 13 | Award on position minima alone / unbalanced low bid accepted | recovery via Nachträge; front-loaded drawdown | §8.3 |
| 14 | Paying Abschläge without Aufmaß/Leistungsmeldung | no leverage, overpayment | §6.3/§8.4 |
| 15 | VOB/B partially adopted/modified "to be safer" | AGB control voids the comfort clauses | §8.1 whole-or-none |
| 16 | Kalkulationslohn vs Mittellohn compared across offers | wrong winner | §5.2 |
| 17 | Net/gross (USt) mixing in anrechenbare Kosten / comparisons | fee & benchmark errors | §1.3/§7.2 |
| 18 | Comparing variants on investment row only (carpet vs stone) | LCC blindness | §11.2 annualise |
| 19 | TGA designed without maintenance access, lifetime assumed = shell | 2–3 exchanges you can physically do | §11.3 |
| 20 | Stale rates presented as current; no date stamp | quiet erosion of every % | date every basis; §7.2 |

---

## Section 14: Templates

### 14.1 BOQ/position line (LV-style)

```
| Pos | KG  | Beschreibung (ATV DIN 18xxx, §4.2 stated) | Einheit | Menge | EP netto | GP netto |
|-----|-----|----------------------------------------------|---------|-------|----------|----------|
| 5.1 | 350 | WBK Decken C25/30, XC2, Pumpen, o. S+B,     | m³      | 282   | 141.00   | 39,762   |
|     |     | inkl. Nebenleistungen gem. DIN 18331/18299     |         |       |          |          |
```

### 14.2 Kostenberechnung summary sheet

```
PROJEKT            <name>            ORT            BAUHERR
STAND              Kostenberechnung nach DIN 276:2018-12   DATUM / BEARBEITER
BEZOUGSFLÄCHE      BGF ___ m² (DIN 277)   BRI ___ m³   NF ___ m²
VOM KOSTENTRÄGER   KG 100 __  KG 200 __  KG 300 __  KG 400 __
                   KG 500 __  KG 600 __  KG 700 __   (= Summe Level-2, netto)
RESERVE (DIN 276:2018, outside KG sums)   __ %   __ €
ESKALATION (Basis: Laufzeit __ Mon., Anteil __ %, Index __ %/a)  __ €
= GESAMT (netto)   __ €   → €/m² BGF __   → €/m³ BRI __
TRIANGULATION      A __ €  B __ €  C __ €  max Δ __ %
ANNAHMEN / NICHT ENTHALTEN (Grundstück? Betriebseinrichtung? Möbel?)
HONORAR-BASIS      anrechenbar netto (1.3): __ €   HZ __  Zone-Quelle __
STATUS: Planungsstand — nicht vergabereif; Preise vom __, fortzuschreiben.
```

### 14.3 Offer comparison sheet — see §8.3 block.

### 14.4 Final checklist before issuing any cost figure

- [ ] Stage named (1.4) and tolerance honestly stated
- [ ] Scope label (1.5) + DIN 276 edition + every position one KG
- [ ] Denominator BGF or NF, DIN 277, printed next to each rate
- [ ] Gross/deduct/net visible; model export reconciled (§4.5)
- [ ] Rebar method (BBS vs ratio) disclosed (§4.3)
- [ ] §4.2 items checked per relevant ATVs (§6.2)
- [ ] Unit prices decomposable (§5); Kalkulationslohn disclosed
- [ ] Reserve outside KG sums, escalation separate (§9)
- [ ] KG 200/700 contents not forgotten (§13 #5/#6)
- [ ] HOAI anrechenbar net, zone + table source named (§10)
- [ ] Offers compared position-wise; low outliers probed (§8.3)
- [ ] Date stamp on rate basis; > 6 months → re-verify

---

## Quick Reference Card

```
DIN 276:2018   100 Grundstück(110/120/130) 200 Herrichten/Erschließen
               300 Baukonstruktion 310–390  400 TGA 410–490
               500 Außenanlagen* 600 Ausbau/WE* 700 Baunebenkosten
               (*titles/500–700 mapping edition-dependent — VERIFY + name edition)
STAGES         Rahmen→Überschlag→Schätzung(LPH2)→Berechnung(LPH3=fee+agreement
               basis)→Anschlag(LPH7 tender)→Feststellung  tol ±20-30→±3-5%
               "Kostenvoranschlag" = OLD word; Reserve OUTSIDE KG sums
AREAS          always €/m² BGF or NF (DIN 277) — NF/BGF 0.65-0.80 → rate error!
PRICE STACK    EKT(Lohn/Mat/Gerät/NU/SoKo)+BGK+AGK+G =netto; Wagnis in G; +19% USt
LOHN           +85-95% Lohnzusatzkosten; A/AS/ASL; Mittellohn vs Kalkulationslohn
GERÄT          A/v + 6.5% Zins + R(30/70); Monat=170h; idle>10d: 75%A+V
GK example     Lohn 40.12% Mat+Ger 18.65% SoKo 17.60% NU 15.50%
METHOD 2       p(AGK+G auf Summe) → p′ = p·100/(100-p)   12% → 13.64% auf HK
               Schlüsselkosten residual → push onto Lohn  (20/80 Leitpositionen!)
AUFMASS        gross→deduct→net; §2(3) VOB/B: ±10% band; <90% EP↑; >110% EP↓;
               Schlussrechnung prüfbar §14; Abschlag 21d; Schluss ≤60d; Verzug 30d
               Sicherheit: VE 5%, Mängel 3%, Einbehalt ≤10% Sperrkonto 18WT; Aval 0.5-1%/a
MEASURE        openings: concrete deduct >0.1 m², masonry both-face >1.5 m² [VERIFY ATV]
               concrete 0.35-0.55 m³/m² BGF · rebar slab 80-110 wall 120-200 kg/m³
               laps +4-6% ≠ waste 3-5% · Schalung= contact area · pump 0.3-0.8 h/m³
HOAI           LPH 1-9 = 2/7/15/3/25/10/4/32/2 % (Gebäude); HZ I-V; degressive table;
               anrechenbar NET (110/710/760 excl.); mvB=KKW×ZF×LF; Umbau +20%;
               SINCE 2021: negotiable — tables orientation only!
LCC            operation >> construction (GHG 60-75% use phase; costs ≈ build cost
               after ~7 a); floors: 10€carpet/10a vs 80€stone/60a → 6.1 vs 9.8 €/m²·a;
               TGA ~30a < shell 50-80a; windows 40-50a; WDVS 40-60a (defective <10!);
               green premium: rents +6-8%/value +14-16% — NO construction-cost premium
               proven for residential; CO₂ shadow 237 €/t (UBA), levy 45 €/t(2024)
               (dated/VERIFY); eLCA mandatory 2028 >1000 m² / 2030 all (EPBD)
RESERVE        concept 20-25% | Vorentwurf 15-20% | Entwurf 10-15% |
               complete docs 5-10% | floor 3% | retrofit 10-25%
ESCALATION     base × matl-share(~0.55) × index × duration/2 — separate line
AUDIT          triangulate A/B/C ≤10% · position-wise compare · <-15% bid = RED FLAG ·
               no decomposition = no negotiation · foreign rates NEVER copy
ALWAYS         state stage+scope+denominator+price date · separate Reserve/Escalation ·
               HOAI anrechenbar NET · say unprompted: planning aid, not binding
               Kostenberechnung/Anschlag — signed planner + current-standards check
               (DIN 276/VOB/HOAI editions moved!) required before any commitment.
```
