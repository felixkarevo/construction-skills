---
name: structural-analysis
description: >
  Statics and load-bearing verification workflow (Baustatik / Nachweisführung) for DACH/Eurocode
  practice: actions EN 1991 (dead load with digested unit weights, imposed loads by category A–E/T/Z,
  snow zones with altitude formulas, wind zones and exposure with digested qp/cpe values, temperature,
  snow drift and slip, maintenance loads), combinations EN 1990 (ULS γG 1.35/1.0, γQ 1.5, full
  ψ0/ψ1/ψ2 table, EQU 1.1/0.9, SLS characteristic/frequent/quasi-permanent, accidental and fire noted),
  equivalent frame/beam analysis, Gerber-beam layout rules, influence-line load arrangement, moment
  redistribution (δ = 0.85, B500A 15 % / B500B 30 %, δmin = 0.64 + 0.8·x/d), span/depth and l/d rules,
  slab systems (one-way, two-way with Pieper/Martens-type coefficients, flat slab + punching), beam design
  incl. shear stirrup selection (VRd,c, truss model, cotθ, smax), T-beam effective flange widths, columns
  with slenderness λ/λlim and second-order (ei, e2, curvature), buckling curves χ and lateral-torsional
  buckling χLT chain (steel), timber verification σ/fd ≤ 1 with kmod, bracing/stability logic (sway check,
  affine wall distribution, imperfection loads), retaining structures (active/passive/rest earth pressure,
  design-case selection, GLS terms, overturning/sliding/bearing trio), ground-bearing checks (DIN 1054
  simplified σE,d ≤ σR,d), crack width wk ≤ 0.3 mm bar-limitation method, fire/accidental combinations
  (ψfi), failure patterns and a fully checked workflow — with five fully worked numeric examples from
  German practice (two-span slab with redistribution, T-beam office girder, slender column, isolated
  footing, timber beam + steel LTB check).
---

# Structural Analysis — Load-Bearing Verification Workflow (DACH / Eurocode practice)

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

## 1. Purpose, scope, and siblings

This skill covers the **verification chain** for building structures: idealization → actions →
combinations → internal forces → ULS (GZT, Grenzzustand der Tragfähigkeit) → SLS (GZG,
Gebrauchstauglichkeit) → detailing checks → documentation. It is a design-assistant skill: it tells
the agent *which checks to run, in what order, with which digested values, and how a correct worked
solution looks numerically*.

Load-bearing topics that belong to **sibling skills** (cross-referenced, not duplicated):

| Topic | Sibling skill |
|---|---|
| Choosing the structural system, statical determination, bracing concept at scheme level | structural-systems |
| Bar-lift-bar schedules, anchorage/lap detailing drawings, congestion | concrete-detailing |
| Masonry wall design (EC6 simplified method, concentric compression, wall coupling) | masonry-construction |
| Full timber/steel member and connection design (EC5/EC3) beyond verification checks here | timber-steel-design |
| Full geotechnical design (EC7/DIN 1054/4017/4019, piles, excavations) | geotechnics-foundations |
| Seismic actions and ductile detailing (EC8 / DIN 4149 legacy) | seismic-design |
| Compartmentation, fire-resistance classes, tabulated fire members | fire-protection-building |

Language convention: English text, German terms in parentheses for site- and norm-matching.

## 2. Reality check — limits of agent-performed analysis

1. The agent may build **model idealizations** (statical systems, load assumptions, combination
   logic) and run/interpret checks, but in the German/European system the load-bearing verification
   (Standsicherheitsnachweis) of a project requires a licensed/prüfbarer engineer (Tragwerksverfasser;
   bauphysically responsible planer) whose calculation is signable and inspectable. Agent output is a
   draft/companion, never a substitute.
2. **Software output must be plausibilized** (Plausibilitätskontrolle). Mandatory plausibility actions
   from mechanics practice: visualized deformation check, zero-stress test for rigid-body motion
   (spannungsfreie Verformung), patch tests, benchmark cases, mesh convergence study, and at least one
   independent **hand calculation** per load case / per governing member. A model that fails to
   converge on sound geometry should raise doubt on the element, not silent trust.
3. In several German Bundesländer a **type-reviewed statics check (Prüfstatik / Typostatik)** by a
   Prüfingenieur is or was part of the approval process for standardized structures; check and
   combination rules (Kombinationsregeln) are exactly what gets reviewed. VERIFY current state per
   Bundesland — this skill digests no procedural law.
4. Reliability background (for sanity of the factors): partial-factor format is a calibration of
   target reliability indices; ULS target β = 3.8 (normal effort, 50-year reference), SLS β = 1.5
   (DIN 1055-100 / EN 1990 logic as digested). Resistance γM and action γF tables in §5 reflect the
   digested NA editions — **dated NA values must be re-verified against the current NA before use**.
5. All numeric values below are reproduced from worked-example digests; fragments flagged
   **[VERIFY]** were garbled in extraction or edition-dated and must not be used as sole authority.

## 3. Evidence tiers

- **T1 — Normative (recognized rules of technique / anerkannte Regeln der Technik):**
  DIN EN 1990 (Basis), 1991-1-1…-1-6 (actions), 1992-1-1 ( concrete), 1993-1-1 (steel),
  1995-1-1 (timber), 1996-1-1/-3 (masonry), 1997-1 (geotech), each with its National Annex (NA),
  plus DAfStb-Richtlinie WU (waterproof concrete), DIN 4109/4108 (where structural relevance).
  NA values change with editions (e.g., steel γM1, CRd,c for shear) — current NA governs.
- **T2 — Handbook tables and derived design aids:** design-value tables (fcd, fyd, fbd, lb,rqd,
  As-tables, ρw,min), continuous-beam coefficient tables, two-way-slab coefficient tables of the
  Pieper/Martens family, interaction diagrams (BT-type column charts), χ-buckling-curve parameters,
  DIN 1054 allowable base-pressure tables, DIN 4017 bearing-capacity factors, DIN 4085 earth-pressure
  coefficients. Reliable, but check the edition the table was built for.
- **T3 — Empirical span/depth heuristics (from structural conception literature):** slab one-way
  d ≈ l/30…l/25, economical solid-slab limit ~8 m (t ≈ 300 mm), flat slab practical limit ~7 m bay,
  beam h ≈ l/10 (d = l/8…l/12), timber joist spans ≤ ~5 m, ring beam span ≤ 30·t, bracing-wall
  thickness ≥ 1/3 of braced wall and ≥ 115 mm, bracing-wall effective length ≥ h/5 — usable for
  pre-dimensioning, always confirmed by checks.
- **T4 — Rules of thumb without digested pedigree: [VERIFY]** — e.g. "assume h = l/20 for
  two-span RC beams", "office girder l/12", wind force reduction for flexible buildings,
  "1.5 % of vertical load as horizontal force for floor diaphragms". Use for concept only.

## 4. Load model (actions per EN 1991, digested German values)

### 4.1 Permanent actions — unit weights [kN/m³ unless noted]

| Material | γ |
|---|---|
| Reinforced concrete (Stahlbeton) | 25.0 |
| Normal concrete (Normalbeton) | 24.0 |
| Heavy concrete (Schwerbeton) | 28.0 |
| Lightweight concrete, RDK 1.0–2.0 | 9.0–20.0 (+1 fresh/RC) |
| Cement mortar (Zementmörtel) | 19–23 |
| Lime-cement mortar (Kalkzementmörtel) | 18–20 |
| Gypsum mortar | 12–18 |
| Masonry units by dry density class RDK: ≤1.4 → ~16; 1.6–1.8 → 18; 1.81–2.0 → 20; 2.21–2.4 → 24; 2.41–2.6 → 26 (RDK ≤ 1.4 light/thin-joint −1) | 0.31–0.35 → 5.5 … 0.91–1.0 → 12 … 2.41–2.6 → 26 (linear per class) |
| AAC unreinforced plates (DIN 4166): RDK 0.35→4.5 … 0.80→9.0 (−0.5 thin-joint) | 4.5–9.0 |
| Reinforced AAC panels (DIN 4223): 0.40→5.2 … 0.80→9.5 | 5.2–9.5 |
| Plaster [kN/m² per 20 mm unless noted]: gypsum 15 mm 0.18; lime/lime-gypsum/gypsum-sand 20 mm 0.35; lime-cement 20 mm 0.40; cement mortar 20 mm 0.42 (30 mm 0.80); lightweight mortar 20 mm 0.30 | 0.18–0.80 |
| Screed [kN/m² per cm]: cement 0.22; CaS 0.22; mastic asphalt 0.23; industrial 0.24; gypsum 0.20 | 0.20–0.24 |
| Roof covering [kN/m² incl. battens, excl. rafters]: concrete/concrete-clay tile ≤10 pcs/m² 0.50–0.55; deep profile 0.60–0.65; flat interlocking 0.55; monk/nun mortar-fixed 0.90; bitumen shingle 0.25; fibre-cement short-wave 0.24/wave 0.20; metal profile 0.05–0.35; reed/thatch 0.70 | 0.05–0.95 |
| Sealing layers: welded bitumen sheet 0.07; loose DIN 52130/32 0.04 (0.07 bonded); plastic sheet 1.5 mm 0.02; gravel 5 cm ≈ 1.0 kN/m² | — |
| Timber: C24 4.2; C30 4.6; D30 oak 6.4; GL24h 3.7; GL28h 4.0; GL32h 4.2; plywood softwood 5.0; chipboard 7–8; cement-bonded 12.0 | 3.5–12 |
| Steel | 77–78.5 |
| Aluminium | 27–28 |
| Glass | 25 |
| Water | 10 |
| Backfill (compacted sand/gravel Schüttung) | 15–20; angle of repose ~35° |
| Snow, shape-factor/drift formulas (μ3 valley cap, μW wind-drift cap, §4.3) | **2.0** |
| Snow, eave-overhang formula only (§4.3) | **3.0** (denser/wetter snow specifically causes eave overhang — not a conflicting value, a different formula) |

Fresh/reinforced lightweight concrete: +1.0. Rule from worked examples: RC slab self weight =
thickness·25 (e.g. 0.20 m → 5.0 kN/m²; 0.22 m → 5.5 kN/m²).

Note: DIN EN 1991-1-1/NA Annex A does **not** cover steel trapezoidal-deck or
green-roof (Dachbegrünung) self-weights — use manufacturer data and the FLL
*Dachbegrünungsrichtlinie* (2008) respectively (Lastannahmen – Beispiele,
Ch.3 §3.1). Stair-flight self-weight is computed per horizontal projected
(Grundfläche) area, same reference area as the imposed load, so it
superposes directly with qk; steps are a half-triangular add-on over the
sloped RC waist slab (ibid., Ch.3, worked Example 3.9).

### 4.2 Imposed loads, buildings (DIN EN 1991-1-1/NA, characteristic)

qk [kN/m²] on area / Qk [kN] concentrated on 50×50 mm:

| Cat. | Use | qk | Qk |
|---|---|---|---|
| A1 | pitched-roof space ≤ 1.8 m | 1.0 | 1.0 |
| A2 | living rooms with load distribution | 1.5 | – |
| A3 | living rooms without distribution | 2.0 | 1.0 |
| B1 | offices, corridors, practices, no heavy equip. | 2.0 | 2.0 |
| B2 | hospital/corridors, kitchens, cellars | 3.0 | 3.0 |
| B3 | B1/B2 with heavy equipment | 5.0 | 4.0 |
| C1 | table areas (schools, cafés, receptions) | 3.0 | 4.0 |
| C2 | fixed seating (churches, theatres) | 4.0 | 4.0 |
| C3 | freely accessible (museums, lobbies) | 5.0 | 4.0 |
| C4 | sports stages, stages | 5.0 | 7.0 |
| C5 | large gatherings (concert halls, fixed stands) | 5.0 | 4.0 |
| C6 | regular huge crowds, loose stands | 7.5 | 10.0 |
| D1 | retail ≤ 50 m² | 2.0 | 2.0 |
| D2 | retail / department stores | 5.0 | 4.0 |
| D3 | D2 with tall shelving | 5.0 | 7.0 |
| E1.1 | light factories/workshops, cattle stalls | 5.0 | 4.0 |
| E1.2 | general storage incl. libraries (minimum!) | 6.0 | 7.0 |
| E2.1 | medium/heavy industry | 7.5 | 10.0 |
| T1 | stairs dwelling/office | 3.0 | 2.0 |
| T2 | other stairs | 5.0 | 2.0 |
| T3 | stand access/escape stairs | 7.5 | 3.0 |
| Z | balconies, roof terraces, loggias | 4.0 | 2.0 |
| H | roofs, not normally accessible | 2.0 (area), 1.0 (single-person load); no superposition with snow | — |

Partitions (Trennwandzuschlag), DIN EN 1991-1-1 §6.3.1.2(8)/NA — confirmed formula: walls ≤ 3 kN/m
run (incl. plaster) → **Δqk ≥ 0.8 kN/m²**; > 3–≤ 5 kN/m → **Δqk ≥ 1.2 kN/m²**; no add-on if
qk ≥ 5.0 kN/m². Category A3 areas without adequate load-distribution to supporting members may
reduce this by 0.5 kN/m². Digested worked examples use 1.0 kN/m² (assembly slab, above the 0.8
code floor) and 1.2 kN/m² (office 2.0 + 1.2 = 3.2; living 1.5 + 1.2).

Load reduction factors (do not combine the two with each other, and never combine either with
ψ-reduction — use the single most favourable factor):
- Area reduction (secondary members: beams/columns/walls/foundations), tributary area A [m²]:
  categories A/B/Z → **αA = 0.5 + 10/A ≤ 1.0**; categories C–E1.1 → **αA = 0.7 + 10/A ≤ 1.0**.
- Multi-storey reduction (vertical member carrying n > 2 storeys of the same use category):
  categories A–D, Z → **αn = 0.7 + 0.6/n**; categories E1.1, E1.2, E2.1–E2.5, T → **αn = 1.0**
  (no reduction — high/fixed-load categories don't benefit from storey averaging).

Vehicle areas (predominantly static): F1 light vehicles ≤ 30 kN: qk 3.0 (may reduce to 2.5 for load
transfer to columns/walls/foundations), or axle load 20 kN alternative; ramps F2 5.0. Forklifts
FL1–FL6 (total allowable load / point load Qk / area qk): FL1 31/26/12.5 … FL2 46/40/15.0 …
FL3 69/63/17.5 … FL4 100/90/20.0 … FL5 150/140/20.0 … FL6 190/170/20.0 kN(/m²); horizontal
acceleration/braking = 30 % of the point load (0.3·Qk, no dynamic factor applied to this term).
**Dynamic amplification factor φ (general rule, all categories with concentrated Qk under
non-predominantly-static action, §4.3.5.2):** φ = **1.4** by default (no more precise
verification done); for buried/covered structures φ = 1.4 − 0.1·h_ü ≥ 1.0 (h_ü = cover depth,
m). Applies to the **point load Qk only** — the distributed qk is used without φ. FL-class
forklift dimensions (a×b track/wheelbase, m / self-weight / lift load kN): FL1 0.85×1.00/2.60 len,
21/10; FL2 0.95×1.10/3.00, 31/15; FL3 1.00×1.20/3.30, 44/25; FL4 1.20×1.40/4.00, 60/40;
FL5 1.50×1.90/4.60, 90/60; FL6 1.80×2.30/5.10, 110/80 — use for worst-position placement on slabs.
Helicopter-landing-pad point loads also require the φ dynamic factor above
(Lastannahmen – Beispiele, Ch.4 Tab. 4.7). Forklift **impact** (accidental
collision, distinct from the 30 %-braking service load above): F = 5·W [kN]
(W = forklift self-weight + lift load), applied 0.75 m above floor, accidental
combination — see §10.

Horizontal line loads on parapets/partitions at ≤ 1.2 m height: cat. A, B1, H, F1–F4, T1, Z →
0.5 kN/m; B2, B3, C1–C4, D, E, Z, FL, HC, T2 → 1.0 kN/m; C5, C6, T3 → 2.0 kN/m. Full in fall
direction, 50 % (min 0.5) opposite. Diaphragm/bracing horizontal force: braced buildings ≈ 1.5 %
of maximum vertical load **[VERIFY — formula stripped in source; checked against Lastannahmen –
Beispiele (EN 1991 actions companion), which does not cover this topic at all — it belongs to
EN 1993/EN 1992 stability/imperfection rules, a different source family; re-attempt with a
steel/concrete-stability-focused source, not another load-actions book]**; grandstands 1/20 of
vertical live; scaffolding 1/100; overturning of fittings 1/100 of total at centre of gravity.

Garages/warehouse floors planned for vehicles: bridge-load classes per legacy DIN 1072 (16/16,
16–30, 30) as noted; fire-service roofs: class 16/16, one vehicle worst position, one wheel load
110 kN check omitted, "predominantly static" allowed.

### 4.3 Snow (DIN EN 1991-1-3/NA — digested edition; NA maps change, re-verify)

Zone boundary values and altitude formulas — cross-checked and substantially
resolved against Lastannahmen – Beispiele (Springer, worked-examples
companion on EN 1991 actions), Ch.6 "Schneelasten":

- **Zone 1: sk = 0.19 + 0.91·((A + 140)/760)² ≥ 0.65** (RESOLVED — was
  flagged "altitude formula not digested"; valid to ≈ 400 m NN; A = ground
  elevation in m).
- Zone 2: sk = 0.25 + 1.91·((A + 140)/760)² ≥ 0.85 (valid to ≈ 285 m —
  confirmed exactly against the earlier digest).
- Zone 3: sk = 0.31 + 2.91·((A + 140)/760)² ≥ 1.10 (valid to ≈ 255 m —
  confirmed exactly; Garmisch 750 m → 4.30).
- **Zones 1a / 2a:** zone 2a confirmed exactly: sk,2a = 1.25·[0.25+1.91·
  ((A+140)/760)²] ≥ 1.06. **Zone 1a — use sk,1a = 1.25 × the zone-1 formula
  above** (i.e. 1.25·[0.19+0.91·(...)²] ≥ 0.81); the source's own literal
  printed zone-1a formula repeats the 0.19 coefficient instead of 0.91,
  breaking the pattern zone 2a uses — this reads as a publisher erratum, so
  keep the "1.25 × zone-1" construction rather than the literal misprint.
  Both the altitude-formula output AND the floor/Sockelbetrag are scaled by
  1.25 — don't silently treat a 1a/2a site as plain zone 1/2.
- **Norddeutsches Tiefland exceptional snow (RESOLVED, was "expert/authority
  decision"):** sAd = Cesl·sk with **Cesl = 2.3** (confirmed across 5+ worked
  examples), zones 1/2 only, exceptional-action combination (γ=1.0).
- Above 1500 m: still expert/authority decision, exceptional-action treatment.
  Named exceptional Zone-3 high-ground locations (CORRECTED list — swap
  "Bayerischer Wald" for the source's actual names): **Oberharz, Hochlagen
  des Fichtelgebirges, Reit im Winkl, Obernach/Walchensee** — flag these even
  though nominally "just zone 3".
- sd = cc·cf·sk (cc site, cf = 1.0 default); flat roof 0–10°: μ1 = 0.8; **s = μ·sk**.

Shapes (worked numbers cross-checked, see §13/§16 loads chapters and examples):
- Mono-pitch/gable α = 30–60°: μ2 = 0.8·(60−α)/30; α > 60°: μ2 = 0 (sliding off); α ≤ 30°: 0.8.
- Valley/back-to-back roofs: μ3 = 1.6, validity cap μ3 ≤ γ·h/sk + μ2 (γ = 2.0 kN/m³ snow — see
  §4.1 for why this differs from the eave-overhang density below).
- Drift against taller roof (Δh, width b): wedge length ls = 2·Δh, minimum 5 m governs for small
  Δh, cap 15 m; sliding load S = 50 % of total snow load of upper roof over ls; μs = 2S/(ls·sk)
  (algebraically equal to the shortcut μs = 0.8·l/ls); **wind-drift μw = (b1 + b2)/(2·Δh)**
  [CORRECTED — no factor of 2 on b2] with cap μw ≤ γ·Δh/sk; combined μ2 = μw + μs, capped
  **0.8 ≤ μw+μs ≤ 2.4** (lower bound resolved/added; upper bound confirmed). Two further
  special-case caps: open, side-accessible canopies with b2 ≤ 3.0 m →
  0.8 ≤ μw+μs ≤ 2.0; **Alpine region** (DIN EN 1991-1-3 Fig. C.2) with sk ≥ 3.0 kN/m² →
  1.2 ≤ μw+μs ≤ 6.45/sk^0.9 (relevant for DACH alpine/foothill buildings).
- Snow guards/parapets at eaves (RESOLVED, was "formula stripped"):
  **F_S = s·b·sin α** [kN/m] — s = roof snow load computed with **μ = 0.8
  regardless of pitch** (accumulation behind the guard), b = plan distance
  from the guard to the ridge/next upslope obstruction, α = roof pitch.
- Snow overhang at the eave (genuinely new sub-case, distinct from the
  snow-guard case above): S_e = 0.4·s²/γ [kN/m] (γ = 3.0 kN/m³ — see §4.1),
  applied as a line load at the cantilever tip for sizing overhanging
  rafters.
- Local roof obstructions (solar panels/plant/chimneys — genuinely new,
  directly usable for FEM load cases with roof-mounted PV/HVAC equipment):
  μ5 = min{1.0; γ·h/sk}, not less than μ1 or μ2.

### 4.4 Wind (DIN EN 1991-1-4 + NA — digested values)

Basic velocity pressure by zone: WZ1 v0 = 22.5 m/s, qb,0 = 0.32; WZ2 25.0/0.39; WZ3 27.5/0.47;
WZ4 30.0/0.56 kN/m². Annual probability 0.02; structures ≤ 300 m.

Simplified peak velocity pressure qpb [kN/m²], constant with height, buildings ≤ 25 m
(terrain mixed II/III inland; columns: h = 10 m / 10 < h ≤ 20 / 20 < h ≤ 25):

| Zone | inland | coast (Ostsee) | Nordsee |
|---|---|---|---|
| WZ1 | 0.50 / 0.65 / 0.75 | — | — |
| WZ2 | 0.65 / 0.80 / 0.90 | 0.85 / 1.00 / 1.10 | — |
| WZ3 | 0.80 / 0.95 / 1.10 | 1.05 / 1.20 / 1.30 | — |
| WZ4 | 0.95 / 1.15 / 1.30 | 1.25 / 1.40 / 1.55 | 1.40 (h ≤ 10 m) |

Reference height: ze = h + hp (parapet counted); h ≤ b → top pressure, h ≤ 2b → split at b,
h > 2b → bands. Exposure pressure we = cpe·qp (walls/roofs, cp,net = cp,e − cp,i).

Digested pressure coefficients cpe,10 (worked examples; interpolation linear, zones A–E walls,
F/G/H/I roof):
- Flat roof with parapet, hp/h ≈ 0.10: F (corner, width e/4·/10) −1.2, G −0.8, H −0.7,
  I +0.2 / −0.6 (centre overpressure/small suction).
- Mono-pitch α = 10°, b/d = 6.7, Θ = 0° (low eave): A/B/C −1.2/−0.8, D +0.8, E −0.5; roof
  F/G/H −1.3/−1.0/−0.4, pressure side +0.1; Θ = 180° (high eave): roof F/G/H −2.4/−1.3/−0.8;
  Θ = 90° (parallel): walls −1.2/−0.8/−0.5 (A/B/C leeward), +0.7 (D), −0.3 (E); roof
  F(hoch) −2.2 / F(tief) −1.8 / G −1.8 / H −0.7 / I −0.6, transition H–I at e/2; e = min(b, 2h),
  wall zone A width e/5, roof F width e/4, F/G depth e/10.
- Freestanding/parapet walls (solidity φ ≥ 0.8): straight wall zones 2.3 / 1.4 / 1.2 / 1.2;
  angled 2.9 / 1.8 / 1.4 / 1.2; L/a = 10: 3.4 / 2.1 / 1.7 / 1.2 (shading factor for spacing).
- Rule: for anchor-force checks with tributary area < 10 m² (purlin/sparren) use increased
  cpe,1 values.

Force method (cf) for tall buildings ≤ 50 m, non-shaking (cscd = 1): Fw = cf·qp(ze)·Aref,
cf = cf,0·ψr·ψλ; worked example: d/b = 0.33 → cf,0 = 2.16, r/b = 0 → ψr = 1.0, λ = h/b = 1 →
ψλ = 0.63 → cf = 1.36; qp(z) profile (Wendehorst Tab. 4.45, DIN EN 1991-1-4/NA — confirmed):
- Inland (Geländekat. II/III mix): z≤7m → qp=1.5·qb; 7<z≤50m → qp=1.7·qb·(z/10)^0.37;
  50<z≤300m → qp=2.1·qb·(z/10)^0.24.
- Coastal/Ostsee islands (Gel.kat. I/II mix): z≤4m → qp=1.8·qb; 4<z≤50m → qp=2.3·qb·(z/10)^0.27;
  50<z≤300m → qp=2.6·qb·(z/10)^0.19.
- Nordsee islands (Gel.kat. I): z≤2m → qp=1.1 kN/m² (constant); 2<z≤300m → qp=1.5·qb·(z/10)^0.19.

λ ≤ 2 → block behaviour
(full area, Völligkeit φ = 1). Bracing-wall distribution: load to walls with eccentricity
e = b/10; slab as single-span diaphragm → up to 0.6·Fw to one wall; wall as cantilever with
resultant at zs = 0.6·h.

Log decrements (vibration susceptibility): RC 0.10; steel 0.05; mixed 0.08; welded steel bridges
0.02; HS-bolted 0.03; bolted 0.05. Non-vibration-susceptible if dynamic deformation ≤ 110 % of
static. Friction cf for saturated surfaces: smooth 0.01 / rough 0.02 / very rough 0.04.

**Annex NA.C (cs·cd structural factor, RESOLVED)** — use for tall/vibration-
susceptible buildings instead of the cs·cd=1 shortcut above (Lastannahmen –
Beispiele, Ch.5 §5.3, Eq. 5.11): cs·cd = [1+2·kp·Iv(zs)·√(B²+R²)] /
[1+6·Iv(zs)]. Full worked chain (Ch.5 Example 18, h=256.5m coastal RC tower,
b=d=41m — reproduce the method, not literally these constants, for a
different building): n1 = 46/h [Hz] (empirical RC fundamental frequency);
z=0.6h; turbulence length scale L(z)=300·(z/300)^ε, ε=(1/(2000z))^0.15
(valid z_min<z≤300m); mean wind v_m(z)=1.18·v_b·(z/10)^0.12 (coastal/mixed
terrain case); f_L=n1·L(z)/v_m(z); non-resonant spectral density
S_L(z,n)=6.8·f_L/(1+10.2·f_L)^(5/3); background factor
B²=1/[1+0.9·((b+h)/L(z))^0.63]; log decrement δ (table above); resonant
response R²=(π²/2δ)·S_L·R_h(η_h)·R_b(η_b), η_h=4.6h/L(z)·f_L,
η_b=4.6b/L(z)·f_L, R_x=1/η_x−1/(2η_x²)·(1−e^(−2η_x)); peak factor
k_p=max{√(2·ln(νT))+0.6/√(2·ln(νT)); 3}, T=600s, ν=n1·√(R²/(B²+R²))>0.08s⁻¹;
turbulence intensity I_v(z)=0.14·(z/10)^(−0.12) (coastal terrain case, adjust
per terrain category). Worked result of that example: cs·cd = 1.084.

### 4.5 Thermal and other actions

Temperature (non-fire) enters only the ψ-table (0.6 / 0.5 / 0.0). Digested linear vertical ΔT
values exist for bridges only (EN 1991-1-5: steel box +18/−13 K; composite +15/−18; concrete box
+10/−5; girder/slab +15/−8) — building-envelope values below; settlement ψ = 1.0/1.0/1.0; "other"
variable 0.8/0.7/0.5.

**Building-specific temperature actions (substantially RESOLVES the earlier
"[VERIFY for buildings]" gap — Lastannahmen – Beispiele, Ch.10 §10.3.4,
DIN EN 1991-1-5/NA):** temperature is an **indirect action** — only produces
internal forces in statically indeterminate systems; determinate systems just
deform (§10.3.3). Thermal expansion coefficients α_T [×10⁻⁶/K]: aluminium 24;
structural steel 12 (10 for composite construction); concrete 10; timber
along grain 5, across grain 30-70 (species-dependent — see timber-steel-design
§3.5 for the full anisotropy figures); masonry 6-10. Reference temperatures
(Tab. 10.3): interior T_in — summer 20 °C, winter 25 °C (fixed, heated DACH
buildings); exterior T_out for above-ground components, by orientation and
surface finish, NE bright/light/dark → T_max+0/+2/+4 (summer), T_min all
finishes (winter); SW bright/light/dark → T_max+18/+30/+42 (summer), T_min
(winter); below-ground components: fixed +6 °C summer / −4 °C winter,
independent of orientation. Germany reference extremes: **T_max = +37 °C,
T_min = −24 °C** (NDP 5.3(2)). Worked example (south-facing light-coloured
external wall, erection temperature T0=10 °C): constant part TN ≈ **+33.5 K
(summer) / −9.5 K (winter)** [source's printed equation shows TN=0.5·(Tin−Tout);
the worked numbers are only consistent with TN=0.5·(Tin**+**Tout) — treat the
minus-sign form as a likely publisher erratum and use the average form];
linear/through-thickness part TM ≈ **+47 K (summer) / −49 K (winter)**.

Ice (still current: DIN 1991-1-3/NA 2019-04 carries former DIN 1055-5 forward verbatim as NCI
Annex NA.F — **not a dated/superseded source**): two classification families —
- **Glaze ice (Klareis/Glatteis, classes G):** all-round ice sheath, thickness t = class number
  in cm (G1 → 1 cm, G2 → 2 cm; **G1 or G2 govern for Germany**); density ρ_ice = **9 kN/m³**.
- **Rime ice (Raueis, classes R), wind-driven one-sided flag on slender members ⌀ ≤ 300 mm:**
  R1–R5 = 0.005/0.009/0.016/0.028/0.050 kN/m at **10 m height**; density ρ_raueis = **5 kN/m³**
  (lower than glaze — larger volume per unit weight); apply height factor k_z (§4.6.3) for other
  member heights. **R1–R3 govern for German lowland and lower Mittelgebirge** — matches the
  zone map.
- Applicability ceiling for these tabulated values: **≤ 600 m NN and ≤ 50 m structure height**;
  beyond that, or in exposed locations, the ice approach is agreed with the authority
  case-by-case (not a table lookup). For slender/filigree members, check ice load as an
  **alternative** to snow (not combined) — governs where wind area gain from the ice sheath
  matters more than the added weight.

## 5. Combinations of actions (EN 1990 / NA — digested values)

### 5.1 ULS fundamental combination (persistent/transient, STR/GEO eq. 6.10a-b style)

    Ed = γG,sup·Gk  +  γQ,1·Qk,1  +  Σi≥2 γQ,i·ψ0,i·Qk,i        (favourable G: γG,inf)

Partial factors on actions (all digested German-NA values):

| Case | γG unfavourable | γG favourable | γQ unfav. | γQ fav. |
|---|---|---|---|---|
| STR / GEO (ref. system B/C) | **1.35** | **1.00** | **1.50** | 0 |
| persistent, exceptional combo | 1.00 | 1.00 | (1.00) | 0 |
| EQU loss of equilibrium (Eingabe-System A) | 1.10 (dst) / 0.90 (stb); small variation 1.05/0.95; combined G incl. member weight 1.35 dst / 1.15 stb | | 1.50 (dst) / 1.0 (exceptional) | 0 |
| GEO ref. system C (loads from soil side) | 1.00 | 1.00 | 1.30 | 0 |

NOTE: a 2nd-generation EN 1990 factor set (γG,sup = 1.22 / γQ = 1.5 with different ψ) circulates
in newer printings but is **not in the digests** — stick to 1.35/1.0/1.5 **[VERIFY current NA]**.
Destabilising and stabilising permanent actions are **always independent** in EQU (never 1.35 and
0.9 on the same G): check Md,dst < Md,stb.

Combination factors ψ (Tafel 4.3 / EN 1990 NA — complete digested table):

| Action | ψ0 | ψ1 | ψ2 |
|---|---|---|---|
| Imposed A (living), B (offices) | 0.7 | 0.5 | 0.3 |
| C assembly, D retail | 0.7 | 0.7 | 0.6 |
| E storage | 1.0 | 0.9 | 0.8 |
| F traffic ≤ 30 kN | 0.7 | 0.7 | 0.6 |
| G traffic 30–160 kN | 0.7 | 0.5 | 0.3 |
| H roofs | 0 | 0 | 0 |
| snow ≤ 1000 m NN | 0.5 | 0.2 | 0 |
| snow > 1000 m NN | 0.7 | 0.5 | 0.2 |
| wind | 0.6 | 0.2 | 0 |
| temperature (non-fire) | 0.6 | 0.5 | 0 |
| settlement | 1.0 | 1.0 | 1.0 |
| other imposed | 0.8 | 0.7 | 0.5 |

Simplified accompanying factor α (A–D, F, G, snow, wind, temp): 0.7; cat. E / settlement: 1.0
(0.6 for snow/wind/temp accompanying in one NA row — printed "ψ0 = 0.7 & 0.6"; use the table).

**Validity rules (Gültigkeit, German practice — critical):**
- Category-Z rooftop terrace live load and snow are **not combined**: ψ0,S = 0 when Qk,N leading;
  ψ0,N = 0 when Qk,S leading (NABau interpretation — digested).
- Partition allowance Δqk is **not** reduced by ψ2: it remains at full value in quasi-permanent
  combinations (stays 1.2 even when qk itself is multiplied by ψ2 = 0.3).
- Wind influence on internal forces < 1 % → wind combination may be dropped (combination "K2"
  instead of "K1") — engineering shortcut from worked example.
- Imposed load on one-way systems: pattern the live load per influence line (worst field/support);
  on two-way/torsionally-stiff slabs full-area loading is usually governing; mutually exclusive
  wind directions need not be combined with each other; raw combinations (e.g. 240) → envelope.

### 5.2 Accidental / exceptional and fire

- Accidental (fire, impact, explosion): γG = γQ = 1.0, ψ = ψfi (see §12); exceptional action itself
  γA = 1.0. Explosion example (local damage allowed, no collapse): impulse load, dynamic factor —
  see §6.10. Seismic combination rules → sibling seismic-design.
- Fire ULS: Ed,fi = Gk + ψfi·Qk with ψfi = ψ1 (frequent) — worked: ψ1 = 0.5 for living/office;
  ψfi,2 = ψ2 for SLS/fire-use. Link: fire-protection-building.

### 5.3 SLS combinations (γ = 1.0 throughout)

- Characteristic (rare, "selten"): Gk + Qk,1 + Σψ0,i·Qk,i → stress limits, crack wk for short-term.
- Frequent: Gk + Qk,1 + Σψ1,i·Qk,i → quasi-permanent-ish appearance checks (w_k frequent 0.2).
- Quasi-permanent (dauerhaft, "GZG perm"): Gk + Σψ2,i·Qk,i (+ full partition allowance!) → long-term
  stresses, deflection (creep k_def/φ), compression-zone checks. Worked: (g+q)perm = 7.0 + 1.2 +
  0.3·2.0 = 8.8 kN/m² on a flat roof slab (storage-type ψ2 = 0.3 on the 2.0 share, Δqk unreduced).
- Extremal short-cut (digested engineering practice): max/min of a section force = independent
  permanent cases + leading variable arranged per influence line + accompanying × ψ; verify each
  candidate combination, not all permutations.

## 6. Structural analysis aids (equivalent systems, coefficients, stability logic)

### 6.1 Statical-system idealizations

- Continuous beam / frame: supports at **axis** of bearings; effective span l_eff = ln + Σai with
  caps: end support ln + b1/2 + b2/2 ≤ ln + 2·a? — digested rule: l_eff = ln + a/2 per side capped
  by 0.05·ln or a/2, monolithic: interior ln + d1 + d2. Use: l_eff = 4.30 + (0.24+0.115)/2 = 4.48 m
  (beam example ✓).
- Rigid-jointed frames: for braced buildings, frame action for vertical loads + sway check (§6.8).
- Masonry floor systems: joist floors on wall = **single spans, not continuous** (line hinges);
  RC slab full bearing → ρ2 = 0.75 two-sided restraint (EC6 simplified).
- Gerber beams (hinged beams): determinate iff m−1 hinges for m spans; layout rules (digested):
  end span ≤ 1 hinge; interior span ≤ 2 hinges; no two adjacent double-hinge interior spans; an
  end span adjacent to a double-hinge interior span must be hinge-free. Analyse top-down:
  suspended spans first, their end reactions load the cantilever spans.
- Statically determinate vs indeterminate: determinate tolerates settlement/ΔT without stress but
  has no redundancy after one failure; indeterminate: stiffness-dependent forces, Zwang-stresses,
  n−1 remaining load paths — drives robustness and redistribution eligibility (§6.4).

### 6.2 Influence lines and load arrangement

Properties (digested mechanics): response Z to moving P = 1; piecewise linear on each load-chord
disk; **zeros under Hauptpole, kinks under Nebenpole**; at the reference point a virtual unit gap/
offset: reaction → unit displacement, N/Q → unit jump, M → unit kink; ordinates ∝ rotation/slide,
display scale arbitrary (δφ ≈ sin ≈ tan). Load arrangement for maximum effect: load all positive
areas with +q, negative with 0 (or reverse for minimum). Continuous-beam maxima: supports under full
load; fields: leading span + alternate spans (pattern loading, "Schachbrett"). Müller–Breslau:
release the constraint, apply S = 1, scale deflected line so conjugate displacement = −1.
Digested single-span equivalence for extremum search: max field M ≈ arrangement LF(leading span +
neighbours per IL), not all-spans-loaded for unequal spans.

### 6.3 Continuous-beam / slab coefficient aids

- Uniform q on equal-span continuous beam, all loaded (elastic, approximate): end span field
  ≈ 0.07·q·l² (interior support −0.10·q·l², cantilevered end correction per ausrundung); interior
  field ≈ q·l²/16…q·l²/24, interior support −q·l²/12 — **[VERIFY grid mapping garbled in the
  handbook table; the worked values below are the authoritative reference]**.
- Two-way slab (Pieper/Martens family), M = p·lx²/fx,y (f = table coefficients; span y uses ly):
  validity conditions (digested): qd ≤ 2·(gd+qd)/3 AND qd ≤ 2·gd (i.e. live share limited);
  torsionally restrained corners (walls); discontinuous-end supports: no extra action needed when
  7·hf < l < 15·hf; isotropic assumption; openings: local beams under interrupted supports with
  45°/60° tributary (edge share 0.50/0.365/0.29 @45°; 0.865/0.635/0.50 @60°), support beam
  beff = 0.5·l (field) / 0.25·l (support). Worked values (§13a, two-way example): panel 6.50×7.24 m
  μ = 1.114 support type "2.2": fx = 24.17, fy = 34.82 → mfx = 10.62·6.5²/24.17 = 18.55 kNm/m;
  support B: msx = −10.62·6.5²/10.80 = −41.51, combine panels: msx = min{0.5·Σmsxi; 0.75·max}.
- FEM/plate: design strip moments m_x/m_y at supports/fields from output; support band width =
  column/beam axis; d per direction dx/dy, average d = (dx+dy)/2 for mixed checks.

### 6.4 Moment redistribution (Umlagerung) — δ = 0.85 rule

Eligibility: continuous beams/slabs, statically indeterminate, **ductile** reinforcement
(B500B/Tempcore), adjacent-span stiffness ratio 0.5–2.0, x/d limited. Procedure (all digested):

1. Elastic support moment M_Ed,axis; reduce: **M'_Ed = δ·M_Ed,axis**, δ = 0.85 (15 %) for
   high-ductility steel; for B500A the digested DIN 488/NA limit is **15 %** max redistribution
   (B: 30 %, A: 15 %) — the worked example checks δmin = 0.64 + 0.8·(x_u/d) ≤ δ ≤ cap
   (printed caps ambiguous/inverted vs. EC2 5.5(4) — **[VERIFY]**: "≤ 0.7 high / ≤ 0.85 normal"
   garbled; the works consistently apply δ = 0.85 with δmin check).
2. Restore equilibrium in each adjacent span: shears v' from ΣM = 0; new field moments from
   v'²/(2q) — field moment may **not drop below** the elastic one (keep the larger):
   "mF1' = 20.76 < 24.98 → keep 24.98; mF2' = 52.62 > 52.24 → use 52.62".
3. Support-moment rounding at bearing face (ausrundung): M_red = M_Ed,axis − ΔM with
   ΔM = V_Ed·a/2 (monolithic) or C_Ed·a/8 — digested both ways; pinned: ΔM = V·a/8.
4. Minimum end-section moment at bar curtailment: end span 0.65·(g+d)·ln²/8; interior span
   0.65·(g+q)·ln²/12 — must not exceed the used support moment.

### 6.5 T-beam effective flange width (b_eff)

b_eff = bw + Σ b_eff,i ≤ b; per side: b_eff,i = min{0.2·b_i + 0.1·l_0; 0.2·b; b_i} — digested
form "0.2bi + 0.1l0 ≤ 0.2b and ≤ bi"; l_0 = distance between points of contraflexure:
end span l_0 = 0.85·l_eff, interior span 0.70·l_eff (NA-style simplification digested in the
T-beam example: l_0 = 4.25 / 3.50 m → b_eff = 1.94 / 1.64 m for 24-cm web, 5.00 m spans).
Check flange compression stress σ_cd = M/(b_eff·z·hf) ≪ fcd and x < hf (else rect. assumption
invalid → T-iteration).

### 6.6 Column buckling / second-order (slender columns, EN 1992)

- l_0 = β·l_w (β = 1.0 isolated, braced; Table 8.44-type K-values for multi-storey walls digested
  partially: 3-sided h/l 0.2→K 0.26 … 1.0→0.90, 5.0→1.00 **[VERIFY mapping]**).
- λ = l_0/i, i = 0.289·h (rect.), i = 0.2·D (circular). Slender if **λ > λ_lim**,
  λ_lim = max{25; 16/√n_Ed} with n_Ed = N_Ed/(A_c·fcd) (simplified AB·C·D = 1 form; full EC2
  λ_lim = 20·A·B·C·D/√n with A = 1/√(1+2ω)… constants stripped **[VERIFY]** — worked values use
  the max(25; 16/√n) rule).
- If slender: ei = l_0/400 (min h/30? — digested: 7.2 mm at l_0 = 2.88 m ✓) + nominal curvature:
  1/r = ε_yd/(0.45·d), ε_yd = f_yd/E_s = 2.175‰ → e2 = K_1·K_φ·(1/r)·l_0²/10 with K_1 = 1.0
  (low creep), K_φ = (n_eff/(1−n_eff))^0.5? (creep factor — worked values used K_φ = 1.0/0.877
  for quasi-perm n; **[VERIFY exponent]**).
  Worked: 1/r = 0.0022/0.45·0.20 = 0.0244 1/m → e2 = 20.2 mm; e_tot = ei + e2 = 27.4 mm →
  M_Ed = N_Ed·e_tot = 42.44 kNm. Existing-structure variant: Kr = (N_Ed − N_Rd)/(N_Ed − N_bal)
  iteration (worked Kr = 0.16 ✓).
- Section: interaction chart (ν_Ed = N/(b·h·fcd), μ_Ed = M/(b²·h·fcd)) → ω → A_s = ω·b·h·fcd/fyd;
  min A_s = 0.15·N_Ed/fyd? digested "As,min = 0.15·NEd/fyd = 5.34 cm²" **[VERIFY coefficient —
  NA value, usually 0.10–0.20·NEd/fyd band]**; max 0.045·A_c (100 % lap) / 0.08 (general).
- Steel members, second-order: M_Ed = M_I·1/(1 − N_Ed/N_cr); N_cr = π²EI/L_cr²; buckling curves
  a/b/c α = 0.21/0.34/0.49, Φ = 0.5·[1 + α·(λ̄ − 0.2) + 0.75·λ̄²], χ = 1/(Φ + √(Φ² − λ̄²)) ≤ 1.0
  (digested recurring rules). Bracing-column imperfection load: H_f = ΣV·α_M/(200·…): digested
  hall example f = 1/200·(2/√5)·α_M(0.736) = 1/304 → H = ΣV/304.
- Beam lateral-torsional buckling (χ_LT chain, digested complete): λ̄_LT = √(M_pl,y,Rk/M_cr)
  (class 1/2) or √(W_el,y·f_y/M_cr) (class 3); M_cr = C_1·(π²·E·I_z/L²)·√(I_w/I_z +
  (L/π)²·G·I_T/(E·I_z)); curve per h/b: > 2 → b (α_LT = 0.34) or c (0.49); Φ_LT =
  0.5·[1 + α_LT(λ̄_LT − 0.2) + 0.75·λ̄_LT²]; χ_LT = 1/(Φ_LT + √(Φ_LT² − 0.75λ̄_LT²)? ) **[VERIFY
  second term 0.75λ̄² vs λ̄²]**; k_c(ψ) from table (ψ=0 → k_c ≤ 1.33, parabolic 0.94 typical);
  χ_LT,mod = χ_LT/f, f = 1.05·(1 + 0.94·(1 − 0.8)…) → 0.974 (formula garbled **[VERIFY]**);
  M_b,Rd = χ_LT,mod·W_pl·f_y/γ_M1. Coped beam rule (digested): h_a/h ≥ 0.7 & a/h ≈ 0.5 →
  reduce M_cr by interaction factor V (chart) and downgrade buckling curve by one → ~30 % capacity
  loss. Worked values: χ_LT = 0.596, f = 0.974 → χ_LT,mod = 0.612 → M_b,Rd = 222.5 kNm, util
  0.80 ✓.
- SDOF/dynamics spot checks (digested): T = 2π√(m·δ) = 2π/ω; k = 1/δ; explosion short-duration
  (t_d ≪ T): impulse J = ½·p̂·t_d·A, v_0 = J/m, x_max = v_0/ω, equivalent H = k·x_max;
  response-spectrum reading → sibling seismic-design.

### 6.7 Lateral-force / bracing logic (Aussteifung)

- Column/wall sharing (same storey height): V_i = (I_i/ΣI)·F (flexural), M_i = V_i·H.
- Walls with shear deformation: flexibility f = H³/(3EI) + 1.2·H/(G·A), G = E/2(1+μ) = 0.4E
  (μ = 0.25); k_i = 1/f_i; V_i = k_i/Σk·F — shear term matters for stocky walls (worked 73/27 %).
- Rigid-floor (affine) wall groups: system shear centre Y_M = [ΣI_y·Σ(I_z·Z) − ΣI_z·Σ(I_yz·Y)] /
  [ΣI_y·ΣI_z − (ΣI_yz)²] (Z_M analogous); load shares per wall from stiffness × translation +
  rotation terms; equilibrium check Σ(−V_y·ΔZ + V_z·ΔY) = M (worked Σ = 1.0 ✓). Wind storeys:
  F = w·A per diaphragm, M_T = F·e (e from load position vs Y_M); eccentricity e = b/10 default
  for regular towers.
- Non-affine (core + wall): flexure–torsion coupling, 2×2 local stiffness matrices → transform
  with rigid-disc offsets; force-method influence coefficients (digested tables) or full 4×4 solve.
- Sway-uncritical (Unverschieblichkeit) per principal axis (digested EN 1992 form):
  F_V,Ed·L²/(E_cd·ΣI_c) ≤ K_1·(n_S+1)/(n_S+1.6), K_1 = 0.31 (n_S storeys). Torsion-susceptible:
  add ΣF_V·r_j²·[L²/(E·I_w) + L²/(G·I_T)…] term (r_j = column j to system shear centre; approx
  ΣF·r² ≈ F_V·(d²/12 + c²), d plan diagonal, c eccentricity). Example 11 storeys: 0.179 ≤ 0.271 ✓.
- Imperfection for stabilisation (digested): inclination α = 0.008/√(2m) (m braced members) or
  θ = (1/200)·α_h·α_m, α_h = 2/√h, α_m = √(1 + 1/m); storey force H_i = α·(N_a + N_b)/2;
  diaphragm chord moment = H·l/8 (+ wind). Timber bracing load (digested EN 1995 rule set):
  compression-flange force N_d = (1 − 0.5·k_crit)·M_d/h; brace line load = share of N_d per
  stiffness chart (worked q_max,d = 2.31 kN/m incl. wind) — 1–2 % equivalent imperfection load.

### 6.8 Utilization check format (all materials)

    σ_Ed / f_d ≤ 1.00    with f_d = k_mod·f_k/γ_M (timber)   f_d = f_k/γ_M (steel/concrete)

Timber design values (digested EN 1995 + NA): γ_M = 1.3 solid/glulam (fasteners simplified 1.1);
k_mod (NKL1 / NKL2): permanent 0.60/0.50; long 0.70/0.55; medium 0.80/0.65; short 0.90/0.70;
very short 1.10/0.90; **wind = 1.0** (mid of short/very-short, NA); governing combination =
max F_d/k_mod across comparable same-direction combos (check each combo separately for
creep-sensitive members). k_def (solid & glulam): NKL1 0.60 / NKL2 0.80 / NKL3 2.00.
Size factor k_h = (180/h)^0.2 ≤ 1.25 (h < 150: use (150/h)^0.2 ≤ 1.3) digested for tension/bending
softwood; glulam flat-use +20 % (≥ 4 layers); f_c,90 bearing k_c,90 = 1.25 (softwood, continuous,
l_1 ≥ 2h) / 1.75 (single support, glulam), A_eff = (3 + l + 3)·b. Combined checks: biaxial bending
with k_m = 0.7; N+M second-order form; buckling k_c = 1/(k + √(k² − λ̄_rel²)),
k = 0.5·(1 + 0.1·λ + 0.3·λ̄²) — worked values in §13e.

## 7. Reinforced-concrete member design chain (EN 1992, German practice)

### 7.1 Material design values (digested tables — always re-check NA)

Partial factors: γ_c = 1.5 (1.3 exceptional / 1.15 factory-precast permitted by NA **[VERIFY]**);
γ_s = 1.15 (1.0 exceptional). α_cc = 0.85 → **f_cd = 0.85·f_ck/1.5**:

| C12/15 | C16/20 | C20/25 | C25/30 | C30/37 | C35/45 | C40/50 | C45/55 | C50/60 |
|---|---|---|---|---|---|---|---|---|
| 6.8 | 9.1 | 11.3 | 14.2 | 17.0 | 19.8 | 22.7 | 25.5 | 28.3 N/mm² |

f_ctm: 1.6/1.9/2.2/2.6/2.9/3.2/3.5/3.8/4.1; f_ctk,005: 1.1/1.3/1.5/1.8/2.0/2.2/2.5/2.7/2.9;
E_cm: 27…37 GPa (30/37→33, 25/30→31). B500: f_yk = 500 → **f_yd = 435**, f_td = 456 (f_tk,cal
525/540), ε_yd = 2.175‰, ε_ud = 25‰ (A) / 50‰ (B); ductility classes DIN 488: B500A normal
(redistribution 15 %), B500B high (30 %). Ratio f_yd/f_cd = 63.9 (C12/15) … 15.3 (C50/60) — used as
ω-chart constant: A_s [cm²] = ω·b[cm]·d[cm]/(f_yd/f_cd [×0.1?]) — digested shortcut
A_s [cm²] = ω·b·d/25.6 for C30/37+B500 (25.6 = 435/17.0 ✓, b,d in cm, A_s in cm²… **result in
cm²/m or cm² accordingly**).

### 7.2 Bending — ω-method (rectangular section, no compression steel)

1. Design moment about steel centroid: M_Ed,s = M_Ed − N_Ed·z_s (N compression negative if tension).
2. μ_Ed,s = M_Ed,s/(b·d²·f_cd) → read ω from dimensionless chart (rect., C12/15–C50/60, B500,
   γ_s = 1.15); digested anchor pairs: μ 0.011→ω 0.011; 0.041→0.042; 0.045→0.0463; 0.0480→0.0494;
   0.0512→0.0528; 0.0753→0.0785; 0.081→0.085 (x/d 0.108, z/d 0.955); 0.086→0.0902; 0.0882→0.0926;
   0.119→0.1285 (x/d 0.159); 0.140?→0.228→0.264; 0.277→0.335; 0.295→0.3626 (ζ 0.814).
   (μ→ω mapping per chart; internal consistency: ω ≈ μ for small μ; x/d = ω/0.85·? — use chart.)
3. A_s = ω·b·d·f_cd/f_yd. Compression-steels branch: chart x/d = 0.45 limit, μ beyond → two-zone
   ω1/ω2, A_s2 = ω2·b·d·f_cd/f_yd **[VERIFY μ-limit constants printed garbled]**.
4. Quick check (N = 0): z ≈ 0.9d, A_s ≈ M_Ed/(z·f_yd).
5. Minimum flexural steel (anti-brittle): A_s,min = M_cr/(z·f_yk), z ≈ 0.9d;
   slab M_cr = f_ctm·h²/6 per m (worked: 2.9·0.22²·10³/6 = 23.4 kNm/m; f_ct,eff variant 2.2 →
   17.75 **[VERIFY which f_ct to use — EC2: f_ctm,eff at cracking, works both]**); beam
   M_cr = f_ctm·W_c (worked 2.6·4219/(500·0.9·38.2) → A_s,min = 1.28 cm² ✓).

### 7.3 Shear (vertical)

- Without stirrups: V_Ed ≤ V_Rd,c = [C_Rd,c·k·(100·ρ_l·f_ck)^⅓ + 0.15·σ_cp]·b_w·d ≥
  (v_min + 0.15σ_cp)·b_w·d; k = 1 + √(200/d) ≤ 2.0 (d in mm); ρ_l = A_sl/(b_w·d) ≤ 0.02;
  σ_cp = N_Ed/A_c ≤ 0.2f_cd. **C_Rd,c: 0.18/γ_c = 0.12 (EN) vs 0.15/γ_c (worked German examples —
  NA of that edition, [VERIFY current NA])**. v_min: digested variants 0.035·k^1.5·f_ck^⅓ + 0.10σ_cp
  (handbook) / 0.0525·k·√f_ck? (works) — **[VERIFY, fragments garbled]**.
- V_Ed section position: at d from face for direct bearing, at axis for indirect bearing.
- With stirrups (variable-strut NA model, digested): concrete share V_Rd,cc = 0.24·f_ck^⅓·b_w·z;
  cotθ = 1.2/(1 − V_Rd,cc/V_Ed,red), cap cotθ ≤ 3.0 (EN-NA range 1.0–2.5 **[VERIFY which applies —
  the NA edition differs; examples use cap 3.0**]); (A_s/w)/s = V_Ed/(z·f_ywd·cotθ), z = 0.9d max;
  strut crushing V_Rd,max = α_cw·f_cd·b_w·z/(cotθ + tanθ), α_cw = 0.75·(1 − f_ck/500) (worked)
  vs EN ν_1 = 0.6(1 − f_ck/250)·α_cw=1.0 — **[VERIFY edition]**.
- Minimum shear reinforcement ρ_w,min ‰: 0.51/0.61/0.70/0.83/0.93/1.02/1.12/1.21/1.31 for
  f_ck 12→50; (A_sw/s)_min = ρ_w,min·b_w·sinα.
- Max stirrup spacing (worked logic): ratio V_Ed/V_Rd,max ≤ 0.3 → s ≤ min(0.75d, …); else
  s ≤ min(0.5h; 300 mm) **[VERIFY exact thresholds — printed example values: T-beam ratio 0.30 →
  300 governs → 250 ok; beam ratio 0.45 → 0.5h = 22.5]**.
- Concentrated support load with 0.5d ≤ a_v ≤ 2.0d direct bearing: shear reduction a_v/(2d);
  concentrated load beyond 2d from section → no reduction (worked).
- Hanger steel at openings/nodes: A_s,req = F_Ed/f_yd, F_Ed = V_Ed·(a/z)/2 + N_Ed; support
  transverse steel for indirect bearing ≥ V_Ed/(0.8·f_yd)? (detailing → concrete-detailing).

### 7.4 Punching (flat slabs, footings)

v_Ed = β·V_Ed/(u_1·d), β: interior 1.10 / edge 1.40 / wall end 1.35 / corner 1.50 / wall corner
1.20; d = (d_y + d_z)/2; u_1 at 2d from loaded area; u_0/d ≤ 10 → no reduction (worked 5.6 ✓).
Without reinforcement: v_Rd,c = 0.18·k·(100ρ_l f_ck)^⅓ (ρ_l = √(ρ_lx·ρ_ly), ≤ 0.02 and
≤ 0.5·f_cd/f_yd cap **[VERIFY — one worked example applies 0.0195 cap as "governs?" and proceeds
with 0.01347]**; σ_cp ≤ 0.2f_cd); lower bound v_min ≈ 0.10k + 0.10σcp ≥ 0.10 (fragments
garbled **[VERIFY]**; worked numbers: v_Rd,c = 0.824 vs vmin 0.542 — 0.824 governs; footing case
vmin-based 0.729 > 0.558 governs).
Footings: λ = a_λ/d: > 2 → control perimeter at 1.0d; < 2 → iterate most unfavourable; a_λ < d →
no punching check. V_Ed,red = V_Ed − p·A_inside(u_1) (soil-pressure relief, worked: 1549 − 269·1.323
= 1193 kN ✓ — pressure at service? uses σ ≈ 269).
With reinforcement (stud rings, worked full chain): f_ywd,ef = min(250 + d, f_ywd) (d mm) →
292.5 N/mm²; per-ring A_sw from (v_Ed − 0.75v_Rd,c) term × ring κ-factors **row 1 × 2.5, row 2 ×
1.4** (digested as used); layout: ≥ 2 rows, first row ≤ 0.5d from face (worked 0.5d; EN-NA "≤ 0.35d"
**[VERIFY]**), row spacing s_r ≤ 0.75d, tangential s_t ≤ 1.5d (≤ 2d at outer rows); outer control
section u_out at 1.5d beyond last row: v_Ed,out ≤ v_Rd,c,out with u_out from
u_out = β·V_Ed/(v_Rd,c·d) (worked 3.89 m → a = 0.466 m = 2.74d). v_Rd,max ≈ 1.4·v_Rd,c (worked
1.1536) **[VERIFY constant]**. Minimum support moment from eccentricity: m_min = 0.125·V_Ed·(a?) —
worked "0.125·VEd/x = 61.9 < 136 not governing" **[VERIFY form]**.

### 7.5 Serviceability (GZG)

- Stress limits (rare): σ_c ≤ 0.60·f_ck (XD/XF/XS); quasi-permanent: σ_c ≤ 0.45·f_ck (if creep
  relevant); steel rare: 0.8·f_yk (loading) / 1.0·f_yk (pure restraint). German NA: checks **waived**
  under elastic analysis + redistribution ≤ 15 % + detailing/min-steel (NA.3 — digested twice).
- Crack width limits w_k,max: X0/XC1 0.4 (appearance, quasi-perm); XC2–XC4 0.3; XD/XS 0.3
  (quasi-perm) — frequent-combination alternative 0.2; prestressing: de-compression under
  quasi-permanent for XD/XS. Bar-limitation method (no direct w_k): from σ_s,perm = M_perm/(A_s·z),
  z ≈ 0.9d, read required **Ø_s* / s_max** table (digested rows): σ_s 320 N/mm² → Ø_s* = 14/10/7 mm
  and s_max = 150/100/– mm for w_k = 0.4/0.3/0.2; σ_s 240 (footing) → Ø_s* 18 mm at 0.3;
  modification Ø_s = Ø_s*·(f_ct,eff/f_ct,0), f_ct,0 = 2.9 N/mm² (worked: 18·2.5/2.9 = 15.5 > Ø12 ✓;
  13→8 for R335 case **[VERIFY garbled rows]**). Direct: w_k = s_r,max·(ε_sm − ε_cm),
  s_r,max = min(Ø/(3.6·ρ_p,eff); 1.3·Ø·? ) **[VERIFY]**, (ε_sm − ε_cm) = (σ_s − 0.4·f_ct,eff/ρ_p,eff)/
  (1 + α_e·ρ_p,eff)/E_s ≥ 0.6·σ_s/E_s (worked → 0.289 mm ✓).
- Restraint min steel: A_s,min = k_c·k·f_ct,eff·A_ct/σ_s; k_c: pure tension 1.0; web/rectangle
  k_c = 0.4·(1 − (h*/h)²)/… **[VERIFY garbled]**; flanges k_c = 0.9·F_cr/(A_ct·f_ct,eff) ≥ 0.5;
  h* = min(h, 1.0 m); k = 1.0 external restraint, internal 0.80 (h ≤ 300) → 0.52 (h ≥ 800).
- Deflections: f ≤ l/250 general; w ≤ l/500 with increased requirements (brittle partitions) —
  cantilever equivalent l = 2.5·l_k. Span/depth: (l/d)_max = K·[11.1 + 1.5·√f_ck·ρ_0/ρ + 12·(f_ck/
  …)^1.5] for ρ ≤ ρ_0 **[VERIFY exponent fragments]**; ρ_0 = √f_ck·10⁻³; K: single 1.0 / end span
  1.3 / interior 1.5 / flat slab 1.2 / cantilever 0.4. Simplified SLS-driven flat-slab thickness
  rule (worked): l/d ≤ K·150/√l[m] → 1.2·150/√6 → 36 → d_erf = l/36 = 16.7 → h ≈ 21 → 22 cm ✓.
  Beam example used l/d = K·35 = 45.5 (K = 1.3, end span). Timber: w_inst ≤ l/200, w_fin ≤ l/150,
  w_net,fin ≤ l/250 (worked §13e; NA limits partially stripped **[VERIFY]**).

### 7.6 Detailing rules that fail checks if wrong (→ concrete-detailing for drawings)

- Cover: c_min XC1 10 / XC2/XC3 20 / XC4 25 / XD·XS 40 mm; Δc_dev 10 (XC1)/15; c_nom = c_min +
  Δc_dev; c_min ≥ Ø and ≥ 1.25·d_agg; −5 mm if 2 classes higher concrete (not XC1). Static depth:
  beam 1 layer d = h − c_nom − Ø_stirrup − 0.5·Ø_bar; 2 layers − 1.5·Ø; slab d = h − c_nom − 0.5·Ø.
- Basic anchorage: l_b,rqd = (Ø/4)·(σ_sd/f_bd), σ_sd = f_yd; f_bd (ribbed, good/moderate): C20/25
  2.32/1.62; C25/30 2.69/1.89; C30/37 3.04/2.13; C35/45 3.37/2.36; C40/50 3.68/2.58; C50/60
  4.28/2.99 N/mm² (Ø > 32: ×32/Ø; moderate = 0.7·good). l_b = α_a·(A_s,erf/A_s,prov)·l_b,rqd ≥
  l_b,min = max(0.3·l_b,rqd; 10Ø) (tension) / max(0.6·; 10Ø) (compression); α_a: straight 1.0;
  hook/loop with transverse cover ≥ 3Ø 0.7 (loops D ≥ 15Ø: 0.5); welded transverse bar 0.7;
  hook + welded 0.5; two welded bars 0.5. Direct end support: l_bd,dir = max(⅔·l_b; …) ≥ 6Ø
  (NA limit worked as 6.7Ø **[VERIFY 6 vs 6.7Ø]**); indirect: l_b ≥ 10Ø; interior support ≥ 6Ø
  past axis. Lap: l_0 = α_1·α_6·l_b ≥ max(0.3·α_1·α_6·l_b,rqd; 15Ø; 200 mm); α_6 (≤ 33 % lapped):
  1.2 (Ø < 16) / 1.4 (Ø ≥ 16); > 33 %: 1.4/2.0 reducible to 1.0/1.4 if c ≥ 4Ø & clear ≥ 8Ø;
  compression 1.0. Curtailment: tension line shifted by Versatz a = (z/2)·(cotθ − cotα), z ≈ 0.9d;
  ≥ l_bd past theoretical cut-off (min 200 mm worked); extend support mats into field ≥ 0.15·l_max
  for fire.
- Column links: Ø_w ≥ max(Ø_l/4; 6 mm); zone 1 s ≤ min(12·Ø_l; b; 300) → worked 240 → chose 200;
  zone 2 (± max(b; 400) above/below slab): s ≤ half (120); zone 3 lap region (Ø_l > 14): over l_0,
  s ≤ l_0/5? worked 600 → 120 **[VERIFY divisor rule]**.
- Exposure→min concrete class (Tafel 8.35): X0 C12/15; XC1/2 C16/20; XC3 C20/25; XC4 C25/30; XD1
  C30/37; XD2/3, XS2/3 C35/45; XS1 C30/37; XF1/2/3 C25/30 (+LP), XF4 C30/37+LP; XA1 C25/30; XA2/3
  C35/45; WU: min C25/30 (real ≈ C30/37) & min wall 240 cast-in-place / slab 250 (BKL-1, [c]).

## 8. Foundation checks (isolated footings on soil — cross-ref geotechnics-foundations)

### 8.1 Base pressure (German simplified DIN 1054, allowable-stress tables)

σ_E,d = V_d/A′ (A′ reduced for e; rectangular factor ×(a/b<2) → +20 %? worked: table σ_R,d = 274
(stiff–semi-firm, t = 1.2·b) ×1.2 rectangle ×(1 − 0.1) width>2 m = 295.9 vs σ_E,d = 293.4 → util
1.00). V_d = 1.35·V_G + 1.5·V_Q (worked: (1270·1.35 + 500·1.5)/8.4 = 293.4 kN/m² — note G already
includes footing weight). Applicability (all digested): level ground, firm layer thickness
t ≥ 2·b, no dynamic actions/PWP, H_k/V_k ≤ 0.2, e < b/6 (G) or b/3 (G+Q), no groundwater effect.
Linear stress: σ = N/A ± M/W with W = a·b²/6; **kern** limit e ≤ b/6; open joint (klaffende Fuge)
if e > b/6: σ_max = 2·D/(3·a·(b/2 − e)); biaxial: e_res = √(e_y² + e_z²) with effective
(a·b)_eff **[VERIFY LF3 numeric garbled ~345 kN/m²]**.

### 8.2 Full ULS (EN 1997 BS-P/BS-T) — outline, details in sibling

- Design base pressure: σ_E,d ≤ R_d/A′; R_n,k via DIN 4017 three-term (N_γ, N_q, N_c; worked
  N_c 21.4/22.1, N_b 2.7/…) / γ_R,v (1.40 BS-P / 1.30 BS-T — digested values; reduced a′ for e;
  B_k = up to 0.5·E_ph,k may reduce H for bearing check).
- Sliding GEO-2: H_d ≤ (V_d·tanδ′)/γ_R,h (γ_R,h = 1.10) + passive/γ_R,e; worked check:
  345 ≤ 499 + 24 ✓ (BS-P), 305 ≤ 499 ✓ (BS-T, no passive).
- EQU rocking about edge: M_dst = γ_G,dst·Σ(M overturning) vs M_stb = γ_G,stb·(V·lever);
  worked 176 vs 1273 ✓.
- Kern/SLS: e_G < b/6 under permanent (no tension), e_tot < b/3 under G+Q.
- UPL buoyancy: γ_dst 1.05·A_k vs γ_stb 0.95·G_k (+ wall friction δ_a = 2φ′/3 option, + tension
  piles/anchors designed GEO-2+STR with group soil-cone check — worked tank example full chain in
  geotech digest).
- Partial factors set (digested DA practice): γ_G 1.35 (ULS-GEO perm) / 1.20 BS-T? (printed:
  BS-P 1.2/1.3 on earth actions; γ_Q 1.5 BS-P / 1.3 BS-T; γ_R,h 1.10; γ_R,e 1.30–1.40; γ_R,v
  1.40/1.30; piles γ 1.40 calc/1.50 single-test; anchors 1.10 BS-T; anchor steel γ_M 1.15)
  **[VERIFY mixed DIN 1054 old-edition numbering vs EN 1997 DA1/DA2/DA3]**.
- Footing internal forces: bending M_Ed = p·c²/2 cantilever (arm c from column face to edge,
  worked ≈ 1.14 m); minimum design support moment for punching-eccentricity (NA rule, printed
  m_Ed,min = 0.125·N_Ed → 19.4 kNm/m at N_Ed = 1549 kN **[VERIFY units/form]**); strip
  distribution over central width (worked: strips b/8, shares 7/10/14/19/19/14/10/7 %); punching
  per §7.4; C25/30 min (XC3+XA1+WF), cover 50 mm on blinding (worked c_nom 85 → d ≈ 49–51.5).

## 9. Retaining structures — basics (→ geotechnics-foundations for full design)

### 9.1 Earth pressure states and coefficients

States: at-rest (Erdruhedruck, non-yielding; cohesion NOT counted at rest), active (wall yields
away; wedge slips; minimum pressure), passive (wall pushed into soil; maximum). Coefficient
sources: plane case DIN 4085 formulas/tables; spatial case separate. Digested anchors:
φ = 30°, δ = 0 → k_a = 1/3 = 0.333; k_a0 = 0.5 (near-surface minimum for restrained walls).
Curved-surface passive (Caquot/Kérisel, δ = 0/δ>0 series): φ 10°→1.62/1.59; 15°→2.12/2.05;
20°→2.83/2.71; 25°→3.89/3.68; 30°→5.56/5.17; 35°→8.36/7.59; 40°→13.44/11.74; 45°→23.71/19.66.
Simplified with wall friction (plane, e.g. kagh): φ = 30 δ = 20° → 0.28; φ = 32.5 flat → 0.25;
φ = 37.5 → 0.20, k_pgh(φ = 37.5, δ = −25°) = 8.9; φ = 27.5 → k_agh 0.31 (Mindesterddruck k_a = 0.18
comparison governs near surface in cohesive top layer). Slip-plane angles ψ = 0: φ = 30 → 60°.
Wall friction: active δ_a = φ/2 (rough) — diaphragm walls φ/3; construction pit digests use
δ_a = 2φ′/3, δ_p = −2φ′/3; passive mobilization for base friction check δ_p = −φ′/3.
Mindesterddruck: cohesive soils near surface — compare against cohesionless "Ersatzboden"
(c = 0, φ = 40 → k ≈ 0.18–0.20); larger governs. Compaction pressure (Verdichtungserddruck): may
exceed at-rest; triangular DIN 4085 distribution per wall stiffness/backfill width — rigid walls
keep it, flexible yield toward active.
Seepage: active side γ′ → γ′ + i·γ_w; passive side γ′ − i·γ_w (i from shortest flow path).

### 9.2 Design case selection (digested table)

| Case | Wall behaviour |
|---|---|
| Active | unrestrained soldier-pile walls; anchors with ~80 % fixing force; retained walls on soil |
| Increased active (eagh = ½(k_a+k_a0)·γ·z; surcharge ½(k_a+k_a0)·q) | anchored walls fixed ~100 %, multi-strutted, walls in the building structure, underpinning |
| At-rest | rock anchors, covered cut-&-cover, rigid abutment wings, walls on rock |

EB69/EB70 redistribution for strutted walls (h_K/H = 0.2–0.25 → stepped rectangle ratio 1.5;
worked e_h 16.30 → 13.04/19.56) — only with anchor prestress > 60 % (soldier piles) / 30 %
(sheet piles). Strip surcharge: E′ = p·b·sin(θ_a − φ)·cos δ/cos(θ_a − φ − δ) triangular over ~2×
depth; line footing loads: E_a,PG = N_p·sin(θ_a − φ)·cos(α + δ)/cos(θ_a − φ − δ_a − α) over
5.2 m triangle; unlimited-area surcharge near wall: q = 10 kN/m² (road traffic), construction
stacks per table; excavator strip loads 50–150 kN/m² b = 1.5–3.0 m with distance reduction.

### 9.3 Stability trio + verification list (EN 1997-1 terms)

1. **Earth-bearing failure / rotation (GEO-2/STR)**: single strut: B_h,d ≤ E_ph,k/γ; base
   pressure check: passive earth resistance on wall width (E_ph = ½·γ·ω_R·t³, ω_R per Kranz/
   Weißenbach overlap cases; worked: 138.85/1.3 = 106.8 ≥ 99.04 ✓).
2. **Sliding/heave of the supported system (GEO-2)**: mobilised passive friction vertical
   equilibrium V_k > B_v,k (mantelreibung; worked G 119.86 > 60.82 ✓); sink-in (Versinken):
   V_d = G·γ + ΣH·tanδ·γ ≤ R_d = (q_b·A_spur + q_s·A_schaft)/γ **[worked pile FAILS → reduce
   spacing — always check]**.
3. **Bearing / ground check (GEO-2)** + **deep slip surface (GEO-3)** — Kranz method, substitute
   wall at mid load-transfer zone, overall-slope circles (DIN 4084, slice methods Bishop; anchors
   can *reduce* GEO-3 safety if their moment adds to actions); **HYD** heave (Terzaghi block:
   G_k·0.95? vs S_k = i·γ_w·A′·γ, worked 27.1 > 7.8 ✓); **UPL** buoyancy; material checks (profile
   M+N interaction, lagging, anchors steel + bond ≥ tests, γ_M steel 1.15; suitably: Larssen 603
   W_y ≥ 735 cm³/m → choose 1200 ✓).

## 10. Fire / accidental combination at analysis level

Fire design values: R_d,fi = k_fi·f_k/γ_M,fi (timber k_fi = 1.25 bending; γ_M,fi 1.0) with
exceptional combination Ed,fi = G + ψ_fi·Q, ψ_fi = ψ1 (living 0.5; storage ψ1 = 0.9 → check!),
γ_G = γ_Q = 1.0. Charring: d_char,n = β_n·t (β_n = 0.7 mm/min thin linings/0.8–0.65 solid —
digested timber R30 uses 0.8·30 = 24 mm), effective defect d_char = d_char,n + k_0·d_0 (7 mm);
reduced-section check with k_mod,fi = 1 − (1/200)·(A/V)? (worked 0.839 **[VERIFY formula
fragment]**). RC: tabulated (EC2-1-2 T5.2a: μ_fi ≤ 0.7 → b_min 250/a 46 for R60 one-side — worked
350/48 ✓ if l_fi < 3 m and A_s < 0.4·A_c). Full member fire design → sibling
fire-protection-building; this skill only supplies the **load combination** and the reduced
verification format.

### 10.1 Accidental actions (Außergewöhnliche Einwirkungen, EN 1991-1-7) — numeric values

Genuinely new content (Lastannahmen – Beispiele, Ch.12) supplementing
`structural-systems` §13's qualitative robustness/tie-force framing with
actual numbers — cross-reference both when a project needs a real accidental-
action check, not just a robustness narrative.

**Consequence-class triage** (EN 1990 Tab. B.1 + EN 1991-1-7/NA Tab. NA.1.A.1)
by building height h (floor-to-finished-floor of the highest occupiable
storey above mean ground, Musterbauordnung Gebäudeklassen convention):
CC1 (h ≤ 7 m: houses/offices ≤ 2 storeys, halls ≤ 7 m, agricultural
buildings) — no special accidental treatment beyond standard robustness
rules; CC2.1/2a (7 < h ≤ 13 m, e.g. 4-storey apartment/office) — simplified
static-equivalent design; CC2.2/2b (everything else up to 13 m, or CC3-listed
buildings ≤ 13 m); **CC3 (h > 22 m, OR h > 13 m with retail floor area
> 2000 m² / > 200 persons excl. residential/office, OR public-assembly
floors > 1600 m², OR explosive/high-fire-risk storage)** — requires special
investigation, possibly risk analysis and non-linear/dynamic methods.

**Road-vehicle impact force on supporting substructures** (Tab. 12.4,
DIN EN 1991-1-7/NA:2019-09), F_dx (travel direction)/F_dy (transverse), kN:
rural roads 1500/750; urban ≥50 km/h 1000/500; urban <50 km/h at projecting
corners 500/500, elsewhere 250/250; truck-accessible yards or car areas with
vehicles >30 kN (e.g. parking structures) 100/100; car areas ≤10 km/h 15/8,
other 50/25; car-park garages ≤30 kN vehicles — single/double garage & carports
10/10, other 40/25; fuel-station canopies 100/100. Application height/area
(Tab. 12.5): PKW at 0.5 m above pavement, LKW at 1.25 m, contact area
0.5 m × 0.2 m. Separate rule: car-park edge-protection barriers, F=40 kN at
0.5 m height, corresponding to 5.5 kNm impact energy. Forklift impact
(distinct from the routine 30 %-braking service case, §4.2): F = 5·W [kN]
(W = self-weight + lift load), applied 0.75 m above floor.

**Notional tie-force formulas** (EN 1991-1-7 Annex A) — the numbers behind
`structural-systems` §13's qualitative statement: internal ties T_i =
max{0.8·(g_k+ψ·q_k)·s_t·L; 75 kN}; peripheral ties T_p =
max{0.4·(g_k+ψ·q_k)·s_t·L; 75 kN} (s_t = tie spacing, L = tie span, ψ = the
accidental-combination factor). No explosion pressure/impulse figures were
found in this source — it defers fully to the norm for Innenraumexplosion.

### 10.2 Construction-phase actions (Einwirkungen während der Bauausführung,
draft E DIN EN 1991-1-6) — distinct from in-service design

Genuinely new (Lastannahmen – Beispiele, Ch.11); not covered by
`construction-scheduling-site` (which has scaffold load classes and
falsework procurement, but not structural wind/imposed-load reduction during
erection or fresh-concrete casting loads).

**Action classification** (Tab. 11.2): personnel + hand tools Q_ca =
1.0 kN/m² (uniform, worst position); stacked movable goods Q_cb ≥ 0.5 kN/m²
for buildings (formwork/scaffolding/plant); heavy vehicles/mobile temp
structures Q_cd (crane, hoist, generator — per manufacturer); waste
accumulation Q_ce; "other" Q_cf (fresh concrete, temporary prop effects,
prestress, hydration).

**Fresh-concrete casting load** (Tab. 11.3, worked Example 1): outside the
work area, **0.75 kN/m²**; inside a 3.0×3.0 m work area (or the span if
smaller), 10 % of fresh-concrete self-weight but bounded **0.75-1.5 kN/m²**;
over the actual footprint, formwork/falsework self-weight + fresh-concrete
self-weight. Valid for drop height ≤ 1.0 m, local pile-up ≤ 3× slab
thickness over 1 m². Worked: 20 cm slab, γ=26 kN/m³ (25+1 fresh-concrete
allowance) → outside area 0.75 kN/m²; inside area 0.10·26·0.20 = 0.52 <
0.75 → 0.75 kN/m² governs; total-area fresh-concrete self-weight =
5.2 kN/m² — directly usable for a FEM slab-casting load case.

**Climatic-action duration rule** (§11.3.3): ≤5 days → use forecast data for
the actual works window; 5 days–1 yr → standard EN1991 98 %-fractile values,
optionally seasonally reduced; >1 yr → full characteristic values, no
seasonal reduction.

**Reduced construction-phase wind pressure** (Tab. 11.4, per draft E DIN EN
1991-1-4/NA Tab. NA.B.5), by duration × safety-measure class (protective/
strengthening/none): ≤3 days 0.1q/0.2q/0.5q; ≤3 months (May-Aug) 0.2q/0.3q/
0.5q; ≤12 months 0.2q/0.3q/0.6q; ≤24 months 0.2q/0.4q/0.7q. Worked example:
WZ1 inland, h=15m, simplified method → q=0.65 kN/m²; ≤12-month construction,
no securing measures → q_red = 0.6×0.65 = **0.39 kN/m²**.

> Note: this chapter's digest is explicitly based on the 2024-03 **draft** E
> DIN EN 1991-1-6, replacing the 2010 edition — re-check publication status
> before citing on a live project.

## 11. WORKED EXAMPLES (reproduced with all printed steps; decimal commas of source converted)

### 11.a Two-span one-way floor slab with 15 % redistribution (Stahlbeton, C30/37, B500)

**System/data:** Decke über EG, two spans l1 = 4.50 / l2 = 6.00 m effective (ln 4.26/5.76 +
support 0.24), h = 22 cm, C30/37 (f_cd = 17.0, f_ctm 2.9, f_ct,eff 2.2 used later), B500A
(f_yd = 43.5 kN/cm²… consistent set: f_cd = 17, f_yd = 435 N/mm², f_bd = 3.0 good), XC1.
Thickness pre-check: K = 1.3 (end span), (l/d) = 1.3·35.0 = 45.5 → d_erf = 650/45.5 = 14.3 cm
→ h = d + 1.0 + 2.5/2 ≈ 17.3 → **h = 22 chosen** (min h rule 17.0 met).

**Loads:** g_k = 0.22·25 + 1.6 finishes = 7.1 → g_d = 1.35·7.1 = 9.59 kN/m²; q_k = 4.0
(assembly C2/C3) + 1.0 partition = 5.0 → q_d = 1.5·5.0 = 7.50 kN/m². Per metre slab width:
q_G+Q = 17.09 kN/m on each field as UDL combination gd+qd (per-unit-m: ×1 m).

**Elastic ULS section forces (LF table: LF1 all perm, LF2 live field 1, LF3 live field 2):**

    m_B = −62.54 ; m_F1 = +24.98 ; m_F2 = +52.24 kNm/m
    v_A = 28.84 ; v_B,li = −52.36 ; v_B,re = +61.70 ; v_C = −42.19 kN/m

**Redistribution δ = 0.85 (15 %):** m'_B = 0.85·(−62.54) = **−53.16 kNm/m**. Equilibrium in
field 1 (q = 17.09, l1 = 4.5): v'_A = (17.09·4.5²/8 − 53.16)/4.5 = (43.10 − 53.16)/4.5 → as
printed: **v'_A = 26.64**, v'_B,li = −50.27 (ΣV: 26.64 − 17.09·4.5 = −50.27 ✓); field 2:
v'_B,re = +60.13, v'_C = −42.41. New field maxima: m_F1' = 26.64²/(2·17.09) = 20.76 < 24.98
→ **keep 24.98**; m_F2' = 42.41²/(2·17.09) = 52.62 > 52.24 → **use 52.62**. (Rule: never take a
field below elastic; supports reduced.)

**ULS bending (b = 100 cm, d = 22 − 2.5 − ½·2·1.0 = 19.0 cm):**
Support B with bearing-face rounding: Δm = (v'_B,li + v'_B,re)·a/8 = (50.27 + 60.13)·0.24/8 =
3.31 → m_B,red = 53.16 − 3.31 = **49.85 kNm/m** (per m, b = 1 m → 49.85e6 Nmm/m).
μ = 49.85e6/(1000·190²·17) = 0.081 → ω = 0.085 (x/d = 0.108, z/d = 0.955) →
a_s = ω·100·19·(17/43.5) = 6.31 → **provide 2×R335 = 6.70 cm²/m**.
δ-check: δ_min = 0.64 + 0.8·0.108 = 0.73 ≤ 0.85 → **15 % allowed ✓**.
Field 1: μ = 24.98e6/(1000·190²·17) = 0.041 → ω 0.042 → 3.12 → **R335** (3.35).
Field 2: μ = 0.086 → ω 0.0902 → 6.69 → **R524 + R188 = 7.12 cm²/m**.

**Shear:** v_Ed,B,re = 61.70; at d = 0.19 + face 0.12 from axis: v_Ed(d) = 61.70 − 0.31·17.09 =
**56.40 kN/m**. v_Rd,c = (0.15/γ_c)·k·(100ρ_l f_ck)^⅓·d·10³ with k = 1 + √(200/190) = 2.03 → cap
2.0; ρ_l = 6.70/(100·19) = 0.353 % → v_Rd,c = 83.4 kN/m (v_min-term 56 < 83.4) > 56.4 →
**no shear reinforcement** ✓.

**SLS:** stress checks exempt (NA.3: elastic, redistribution ≤ 15 %, min steel + detailing OK).
Quasi-permanent (g+q)_perm = 7.10 + 0.6·5.00 = **10.10 kN/m²** (ψ2 = 0.6 for category C!).
m_Ed,B,perm = 0.1803·10.10·4.5² = 36.86 kNm/m (support coefficient of the *unredistributed*
system); field perm = 0.1417·7.10·4.5² + 0.163·3.0·4.5² = 20.27 + 9.90 = 30.17 kNm/m.
σ_s,perm support = 36.86e6/(770·0.9·190)? → as printed **280 N/mm²** (A_s,prov basis); field
248 N/mm². Bar limitation w_k = 0.3: s_max = 150 mm (R335 ✓) or Ø_s* = 13 modified → 8 ≥ Ø8 of
R335 ✓ → **crack control by table, no direct w_k** ✓.

**Detailing (all digested):** l_b,rqd Ø10 = 36.3 cm, Ø8 = 29.0 (f_bd 3.0). End support C:
F_Ed = v_Ed·(a_1/z) = 42.41·1.0/0.9 = 47.12 kN/m → a_s,erf 1.08; l_b = α_a·(erf/prov)·l_b,rqd ≥
l_b,min = max(0.3·363 = 109; 10Ø) → **l_bd,dir = 10 cm behind face** (≥ ⅔·l_b, ≥ 10Ø ✓). Interior
support: ≥ ½ of field steel through, anchor ≥ 6Ø = 60 mm past axis; no extra top steel needed for
possible +M. Field curtailment: from zero of shifted tension line (Versatz) + l_bd =
0.3·l_b,rqd = 87 mm (Ø8). Fire ULS: support mats run 0.15·l_max = 0.90 m into field.
Minimum ductile steel: m_cr = f_ct,eff·h²/6 = 2.2·0.22²·10³/6 = 17.75 kNm/m →
a_s,min = m_cr/(f_yk·0.9d) = 2.08 < 3.35 provided ✓ **[f_ct,eff = 2.2 vs f_ctm 2.9 — verify
edition]**. End-support restraint steel: 0.25·a_s,field → R188 both fields, length 0.2·l =
0.90/1.20 m.

### 11.b T-beam office girder, 3 equal spans (Unterzug E101, C30/37, B500)

**Geometry:** b_w = 24, h = 75, h_f = 22 (slab); l_n = 4.76 → l_eff = 5.00 m; XC1; min C16/20 →
C30/37; c_nom = 20 but bond ≥ Ø_l = 25 → c_v = 45 mm.
**Loads (from slab chapter):** slab action onto girder g_k = 47.4 kN/m + beam 0.24·0.53·25 =
3.18 → g_d = 1.35·50.58 = 68.3; q_d = 50.1 kN/m → total q_d = 118.4 kN/m.
**Elastic LF table:** M1 = 263.10, M2 = 136.62, M_B = −317.29 kNm; V_A = 249.33,
V_B,li = −359.46, V_B,re = 316.79 kN.

**δ = 0.85:** M'_B = −269.70; ΔM = 47.59 → ΔV = 47.59/5.00 = 9.52 → V'_A = 258.85,
V'_B,li = −349.94, V'_B,re = −307.27 (sign per print); field: M_1' = 258.85²/(2·118.4) =
**282.30 > 263.10 → governs**; M_2' = −269.70 + 118.4·5²/8 = 370.0 − 269.70 = 100.30 < 136.62 →
**keep 136.62**. Min end-section moment: 0.65·118.4·4.76²/8 = 217.96 < 269.70 ✓ (no increase).

**Support B bending (rect. 24/75, d = 75 − 3.5 − 1.0 − ½·2·2.5 = 69 cm):**
rounding ΔM = V'_B,re·a/2 = 307.27·0.24/2 = 36.87 → M_B,red = 268.4 − 36.9 = **231.55 kNm**.
μ = 231.55e6/(240·690²·17) = 0.119 → ω 0.1285 (x/d 0.159, z/d 0.934) →
A_s = ω·b·d/(f_yd/f_cd) = 0.1285·24·69/25.6 = 8.31 cm² → **3Ø20 = 9.42**.
δ_min = 0.64 + 0.8·0.159 = 0.77 ≤ 0.85 ✓.

**Field T-section:** l_0 = 0.85·l_eff = 4.25 (end) / 0.70·l_eff = 3.50 (interior); b_eff,i =
min{0.2·b_i + 0.1·l_0; 0.2·b; b_i} → 0.85 m/side → b_eff = 1.94 m (field 1) / 0.70 → b_eff =
1.64 m (field 2). d = 75 − 3.5 − 1.0 − 1.5·2.5 = 67.0. Field 1 M = 282.30: μ =
282.3e6/(1940·670²·17) = 0.019 → ω 0.0193 (x/d 0.043) → A_s = 9.80 → **4Ø20 = 12.6**; x =
0.043·67 = 2.88 < h_f = 22 → rectangular behaviour OK; flange stress σ_cd =
0.2823/(0.981·0.67·1.94·0.22) ≈ 1.01 MN/m² ≪ 17 ✓. Field 2 M = 136.62: μ 0.011 → ω 0.011 →
4.72 → **3Ø16 = 6.03**.

**Shear (NA extended-truss model):** A: V_Ed,A,red = 258.85 − (0.5·0.24 + 0.67)·118.4 =
**165.31 kN**; V_Rd,cc = 0.24·f_ck^⅓·b_w·z = 107.9 kN; cotθ = 1.2/(1 − 107.9/165.31) = 3.46 →
cap **3.0**; A_sw = V_Ed/(z·f_yd·cotθ) = 165.31e3/(0.9·670·435·3.0) = 2.10 cm²/m;
min ρ_w → 2.26 cm²/m **governs** → **Ø8/25-2g = 4.02 cm²/m**. V_Rd,max = 0.75·f_cd·b_w·z/
(cotθ + tanθ) = 553.6 kN; ratio 0.30 → s_max = min(0.5h = 37.5; 300) → 300 governs → 250 ✓.
Interior support B,li: V_Ed,red = 349.94 − 108.5·1.184·? → **256.40 kN**; cotθ = 2.07 →
A_sw = 4.72 → **Ø8/15 = 6.71 cm²/m**; V_Rd,max(cot 2.07) = 722.7 > 349.94 ✓.

**Flange–web longitudinal shear (Schubfuge):** x_0 = V_Ed,A/(g_d+q_d) = 249.33/118.4 = 2.11 m;
Δx = x_0/2 = 1.06 m; M(Δx) = 197.77 kNm; σ_cd = 0.19777/(0.66·1.94·0.22) = 0.702 MN/m²;
F_cd = 0.702·(1.94 − 0.24)/2·0.22 = **131 kN**; F_ed = 0 at M = 0 → v_Ed,F =
131/(0.22·1.06·10³) = 0.562 MN/m²; required transverse (cotθ_f = 1.2):
a_st = v_Ed,F·h_f·10⁴/(f_yd·1.2·10⁴) = **2.37 cm²/m**; strut check v_Rd,max,f = 6.28 ≫ 0.562 ✓;
half top / half bottom → 1.19 < 6.70 slab-provided → **Ø6/15 bottom** ✓.

### 11.c Slender interior column with second-order verification (centric, 0.24×0.40, l_w 2.88)

**Loads:** N_Ed = 1.35·773.4 + 1.5·336.8 = **1549 kN** (slab reactions OG 241 / EG 241 / KG 278.3
+ self 13.1 permanent; Q 23.4/113/200.4); M_Ed = 0 first order (braced, centric).
**Slenderness:** l_0 = 1.0·l_w = 2.88 m; i = 0.289·h_x? (buckling about weak axis of 0.24×0.40 →
h = 0.240) → i = 0.06936 m → λ = 41.5; n = N_Ed/(A_c·f_cd) = 1549/(0.096·17000) = 0.949 ≥ 0.41
→ λ_lim = 25 (simplified max{25; 16/√n}) → **λ > λ_lim → slender, 2nd order**.
**Eccentricities:** e_i = l_0/400 = 7.2 mm; curvature 1/r = ε_yd/(0.45·d), ε_yd = 435/200000 =
0.0022, d = 0.20 → 1/r = 0.0244 1/m → e_2 = K_1·K_φ·(1/r)·l_0²/10 = 20.2 mm; e_tot = 27.4 mm →
**M_Ed = 1549·0.0274 = 42.44 kNm**.
**Limits:** A_s,min = 0.15·N_Ed/f_yd = 5.34 cm² **[VERIFY coefficient]**;
A_s,max (100 % lap) = 0.045·A_c = 43.2 cm².
**Design chart:** ν_Ed = 0.95, μ_Ed = M/(b²h f_cd) = 42.44e6/(240²·400·17) = 0.108, d_1 = 4.25 cm
(d/h interp 0.25) → ω = 0.25 → A_s,tot = ω·b·h·f_cd/f_yd = 0.25·24·40/25.6 = **9.38 cm²** →
**4Ø20 = 12.6** < 43.2 (100 % lap feasible).
**Lap:** l_b,rqd = (Ø/4)·f_yd/f_bd = 5·435/3.0 = 725 mm; l_0 = 725·(9.38/12.6) = 540 ≥
l_0,min = max(0.3·725 = 218; 15Ø = 300? printed 375 for Ø25 **[VERIFY Ø basis]**; 200) →
**choose l_0 = 600 mm**.
**Links:** Ø_w ≥ max(0.25·Ø_l; 6) → Ø10 used; zone 1 s ≤ min(12Ø_l = 240; 240; 300) → 240 →
chose 200; zone 2 (± max(b; 400) mm above/below slab) s = 120; zone 3 (lap zone, Ø_l > 14) over
l_0 = 600 → s = 120.
**Existing-structure variant (for reference):** cores → EN 13791 → f_ck = 33.5 (C30/37);
l_0 = 0.76·5.2 = 3.95, λ = 45.6 > max(25; 16/√1.08) → slender; e_i = α_h·l_0²/1750? → 0.87 cm;
e_2 = K_r·… = 0.46 (K_r = 0.16, K_φ = 1, K_1 = 1); e_tot = 1.33 → ω 0.205 → chart BT 2c
(d_1/h = 0.15 line, e_d/h = 0.044, ν_Ed = 1.08) → N_Rd = 1844 kN; Kr-verification
(2.058 − 1.844)/(2.058 − 0.683) = 0.156 ≈ 0.16 ✓.

### 11.d Isolated footing 2.40×2.40 m under column 0.24×0.40 (C25/30)

**Data:** N_Ed = 1549 kN (§11.c); soil σ_B,zul = 300 kN/m²; footing 2.40×2.40, h = 60 cm;
C25/30 (XC3 + XA1 + WF; min C25/30), f_cd = 14.2; blinding → c_nom = 20 + 15 + 50 = 85 mm →
d ≈ 51.5 (x) / 49.0 (y).
**Bearing (German simplified):** σ = 1549/5.76 = 269 kN/m²; + concrete self 1.35·(2.4²·0.6·25)/
5.76 → **289 ≤ 300 ✓** (γG = 1.35 on footing weight — digested practice).
**Bending:** cantilever arm c ≈ 1.14 m: m_Ed = σ·c²/2 → printed total M_Ed = 0.418 MNm,
m_Ed = **0.174 MNm/m** [arm/formula partially garbled **[VERIFY]**]; governing **minimum
support moment m_Ed,min = 0.125·N_Ed → 19.4 kNm/m** (NA punching-eccentricity rule **[VERIFY
units]**). μ→ω = 0.0531 → A_s = **21.4 cm²** → **22Ø12 = 24.86 cm² both ways**; strip
distribution 7/10/14/19/19/14/10/7 % over b/8.
**Punching:** λ = a/d = 1.08/0.50 = 2.16 ≥ 2 → control perimeter at 1.0d; u = 4·0.24 + 2π·0.5 =
4.10 m; A_crit = 0.24² + 4·0.24·0.5 + π·0.5² = 1.323 m²; V_Ed,red = 1549 − 269·1.323 =
**1193 kN**; β = 1.10 → v_Ed = 1.10·1193/(4.10·0.5)·10⁻³ = **0.64 N/mm²**; v_Rd,c = 0.558 < v_Ed
but v_min-based **0.729 governs ≥ 0.64 → no punching reinforcement ✓**.
**SLS (XC3 → w_k = 0.3):** N_perm = 773.4 + 0.6·336.8 = 975.5 kN (ψ2 = 0.6, category E-type
storage share; here office 0.3? printed 0.6 — accompanying share per digested case) →
M_perm = 0.263 MNm; σ_s,perm = 235.6 N/mm² → Ø_s* = 18 mm (w_k 0.3, σ_s ≈ 240) → modify
×(f_ct,eff/f_ct,0) = 2.5/2.9 → 15.5 > Ø12 ✓.

### 11.e Timber glulam beam + steel LTB check (from second examples digest)

**(e1) GL28c 16/90, L = 15 m, uni-axial bending, fork supports (Ex. "Biegeträger"):**
q_g,k = 5.0, q_s,k = 3.75 kN/m → q_d = 1.35·5 + 1.5·3.75 = **12.4 kN/m** (governs: 12.4/0.9 =
13.8 > 6.75/0.6 = 11.3 — F_d/k_mod comparison); V_d = 93 kN; M_max = 12.4·15²/8 = **348.8 kNm**.
- Bending: W_y = 16·90²/6 = 21.600 cm³; h = 90 > 60 → no k_h; f_m,d = 0.9·2.8/1.3 = 1.94 kN/cm²
  → σ = 34.880/21.600 = 1.61 ≤ 1.94 → util **0.83** ✓.
- Shear: k_cr = 2.5/f_v,k = 2.5/3.5 = 0.714 → b_ef = 0.714·16 = 11.4 cm; f_v,d = 0.9·0.35/1.3 =
  0.242; τ = 1.5·93/(11.4·90) = 0.136 ≤ 0.242 → 0.56 ✓ (alt. V_red at h from face: 93 − 12.4·1.0
  = 80.6 → 0.49).
- LTB (Kippen): top-flange restraints a = 5.0 m; exact l_ef (formula table): B = E_d·b³h/12 =
  29.55·10⁶, T ≈ G_d·b³h/3 = 6.14·10⁶ (E_mean/γ_M = 962, G_mean/γ_M = 50 kN/cm²), a_z = h/2 = 45
  (load top edge), a1 = 1.13, a2 = 1.44 (UDL, fork) → l_ef = 500·√(1.13·(1 + 1.44·45/500·√(29.55/
  6.14))) = **618 cm**; simplified 0.9·l + 2·h = 630 → use smaller. i_m = √(I_z·I_tor)/W_y,
  I_tor = a1·b³h (a1 = 0.296 at h/b = 5.625) = 109.100 → i_m = 2.68; λ_rel,m = (l_ef/(π·i_m))·
  √(f_m,k/E_0,05) = (618/2.80)·√(2.8/104) = 0.856; k_crit = 1.56 − 0.75·λ_rel = **0.918**
  (linear formula above λ_rel ≈ 0.816); σ = 1.61 ≤ 0.918·1.94 → util **0.91 → LTB governs**.
- Bearing: support l = 20 cm, a = 10 > 3·?; k_c,90 = 1.75; A_ef = 26·16 = 416 cm²;
  93/416 = 0.2236 ≤ 1.75·0.173 = 0.303 → 0.74 ✓.
- **Bracing load continuation:** unrestrained length 15 m → l_ef = 1466, λ_rel = 1.32 → k_crit =
  0.57 → flange force N_d = (1 − 0.5·0.57)·34.880/90 = **166.6 kN** per beam; brace line load
  q_d + wind share → q_max,d = **2.31 kN/m** (stiffness chart k = 1, n/2 = 3 beams, m = 2 braces).
- **Deflections (SLS, continuation):** k_def = 0.6 (CL1 glulam), ψ2 snow = 0; w_inst,g =
  5·0.050·1500⁴/(384·1250·972.000) = 2.71 cm; w_inst,s = 2.03 → w_inst = 4.74 ≤ l/200 = 7.5
  (0.63); w_fin = 2.71·1.6 + 2.03 = 6.37 ≤ l/150 = 10 (0.64); net final 0.34 ≤ l/250 after
  4 cm camber (0.06) ✓.

**(e2) Steel — LTB of a coped beam (Biegedrillknicken, S235):** q_Ed = 20.0 kN/m, L = 4.50 m →
M_y,Ed = 20·4.5²/8 = **50.6 kNm**. Section W_pl,y = 314 cm³, I_z = 604 cm⁴, I_w = 125.9·10⁴ cm⁶?,
I_T = 20.1 cm⁴, h/b = 2/0.61.
1. Without cope: M_pl,y,Rk = W_pl·f_y = 2·314·23.5/100? → printed **147.6 kNm**
   (= 314·23.5/100·2 half? use printed); c₂² = I_w/I_z + (E·I_w)/(G·I_T)·(π/L)⁻² → 471.8 cm²;
   N_cr,z = π²·21.000·604/450² = 618.2 kN; M_cr (C₁-form) = **111 kNm**; λ̄_LT = √(147.6/111) =
   **1.15**; h/b > 2 → curve b; χ_LT,mod = **0.623**; q_Rd = 8·0.623·(147.6/1.1)/4.5² ≈ **33 kN/m**.
2. With cope (h_a/h = 0.8, a/h = 0.5): interaction V = 0.68 (chart) → M_cr = 0.68·107.1 = 72.8
   kNm; downgrade curve b→c; λ̄_LT = √(W_pl·f_y/M_cr) = 1.42 → χ_LT = 0.429; k_c = 0.94, f = 0.99 →
   χ_LT,mod = 0.433; M_b,Rd = χ_LT,mod·W_pl·f_y/γ_M1 = **57.5 kNm**; q_Rd = 22.7 kN/m; check
   50.6/57.5 = **0.88 < 1 ✓**.
3. Verdict: cope reduces capacity 22.7/33.0 = 68.8 % → **≈ 30 % loss**; rule: cope with
   h_a/h ≥ 0.7 & a/h ≈ 0.5 → M_cr·V and curve down one step.

## 12. Workflow checklist (agent execution order)

1. **Idealize:** statical system per member (beams/frames/slabs/walls), supports (Gelenk/Fest/
   Feder), grain/orthotropy, bracing concept & sway classification (§6.7) — hand the system sketch
   to the reader with node/axis dimensions and l_eff rules (§6.1). Flag every determinacy degree.
2. **Actions:** permanent (self-weight via §4.1 unit weights + finishes + linings; parapet/railing
   line loads; façade shares), imposed (§4.2 category!), snow (§4.3 zone + altitude + μ shapes +
   drift), wind (§4.4 zone/exposure/qp + cpe or cf), thermal/settlement where relevant. List per
   load case (LF) with pattern-load subdivisions for live, mutually exclusive wind directions.
3. **Combinations:** ULS persistent (1.35G + 1.5Q₁ + Σ1.5ψ₀Qᵢ), EQU (1.1/0.9/1.5), accidental/fire
   (1.0/1.0/ψ₁), SLS char/frequent/quasi-perm (ψ₂, partition not reduced!) — apply validity rules
   §5.1; drop negligible (<1 %) wind; build envelope of candidates.
4. **Internal forces:** hand methods (§6.2–6.3) or FEM; for FEM: run the model in the FreeCAD MCP
   FEM workbench (`run_fem_analysis`) **only as a spot check** — one simply-supported and one
   continuous case per member type; cross-check reactions ΣV/ΣH/ΣM and moment equilibria against
   the main program; compare with coefficient-hand values within plausibility range (±10–20 %).
5. **ULS members:** bending ω-method (§7.2), shear (§7.3), punching (§7.4), compression/2nd order
   (§6.6), torsion+shear interaction (digested: (T/T_Rd)² + (V/V_Rd)² ≤ 1, thin-tube Bredt chain —
   see examples digest), connections (→ timber-steel-design / concrete-detailing).
6. **SLS:** stresses (NA exemption check), crack w_k (§7.5 bar method or direct), deflections
   (l/d pre-check + f_fin with creep φ/k_def), foundation settlements/rotations (→ geotech sibling).
7. **Detailing verification:** anchorage/laps/curtailment (tension-line coverage with Versatz),
   min/max steel, links, cover vs exposure, fire mat extensions (§11.a listing).
8. **Documentation / BIM metadata:** tag every analysis object in the model with property sets:
   material class (C30/37/B500B…), γ, E, f_cd/f_yd, load case & combination ids of governing
   results, utilization ratio E_d/R_d, l_eff, system id, analysis software + version, date,
   responsible-engineer field. IFC: IfcStructuralAnalysisModel / IfcStructuralResult carry
   combination and result links (ISO 16739); keep IfcLocalPlacement so re-derivation of spans is
   possible; export governing envelope (not per-LF soup). Store hand-check sheets next to the model
   (Nachweis format: action table → combination table → per-member E_d/R_d ≤ 1.0 line).

## 13. Failure patterns (recurring errors) and how to catch them

1. **Wrong ψ applied** — leading variable with ψ₀ < 1, or accompanying with ψ₀ = 1. Check: leading
   is the unfavourable one *per section force* (different leading per member!). Catch: combination
   table lists leading + accompanying factors per case; cross-check against §5.1 table.
2. **Snow + roof-terrace live load combined** — forbidden (validity rule). Catch: §5.1 rule list.
3. **Partition allowance ψ₂-reduced** — must stay full (1.0/1.2 kN/m²). Catch: quasi-perm load
   line prints "g + Δqk + ψ₂·q".
4. **Missing second-order effects** — λ ≤ λ_lim not checked before first-order design. Catch:
   always compute λ = l_0/i, n = N/(A_c·f_cd), λ_lim = max(25; 16/√n) (§6.6).
5. **Support vs field redistribution confusion** — reducing *field* moments by δ (not allowed) or
   letting field moment drop below elastic after support reduction (violates equilibrium). Catch:
   the equilibrium check (v' → m' comparison) in §6.4/§11.a.
6. **Unverified unit weights** — "RC 25" applied to an un-reinforced topping, or finishes counted
   twice (slab + Δg). Catch: build-up table with per-layer γ and thickness, sum check vs. typical
   floor (22 cm RC + 1.5 finishes ≈ 7.0 kN/m²).
7. **Dated NA values silently wrong** — C_Rd,c 0.15/γ_c vs 0.18/γ_c; γ_M1 steel 1.1 vs older;
   NA-edition snow formulas. Catch: §5/§7 VERIFY flags → confirm current NA.
8. **γG = 1.35 on stabilising actions** — overturning must use 0.9 (1.1 dst); applying 1.35·G on
   both sides of Md,dst < Md,stb is a classic. Catch: EQU row in §5.1 + worked balcony example
   (66.7 < 139.4).
9. **Punching control perimeter misuse on footings** — forgetting V_Ed,red (soil relief) or a_λ < d
   exemption; using slab β without eccentricity. Catch: §7.4 decision list.
10. **Effective flange width ignored** — T-beam designed with full physical flange. Catch: b_eff
    formula §6.5 with l_0 from contraflexure.
11. **cpe,1 anchor rule missed** — purlin/sparren anchorage with cpe,10 area values. Catch: <10 m²
    rule §4.4.
12. **Channel-section trench beams** — deck load plane not through shear centre → St. Venant +
    warping torsion, τ ≈ 20.5 kN/cm² failure in worked variant; monolithic RC deck fixes torsion but
    raises deck design moment +14 %. Catch: §6.1/steel note + shear-centre check.
13. **LTB via W_pl only** — no χ_LT check for unrestrained compression flanges (timber k_crit /
    steel χ_LT,mod). Catch: §6.6/§11.e util comparison (0.83 vs 0.91 → LTB governs).
14. **Bracing eccentricity omitted** — wind to walls via diaphragm needs e = b/10 torsion share;
    affine analysis (§6.7). Catch: system shear-centre offset check.
15. **SLS stress exemption misused** — exemption requires elastic analysis, redistribution ≤ 15 %,
    min steel, detailing — all four. Catch: §7.5.
16. **Fire combination with ψ₀ instead of ψ₁** — fire is exceptional combo (γ = 1.0, ψ_fi = ψ₁).
    Catch: §10.

## 14. Quick verification checklist (before delivering any Nachweis)

- [ ] Statical system, supports, l_eff, sway/non-sway decision documented (K₁ = 0.31 check run)
- [ ] Load table: every action traceable to a digested §4 value + exposure/zone source; unit
      weights from §4.1 (no invented values)
- [ ] Combinations: ULS/EQU/SLS/fire each ≥ 1 explicit row; ψ per §5.1 table; validity rules ticked
- [ ] Internal forces: at least one hand-plausibilized case (ΣV = Σload, ΣM = 0 at supports)
- [ ] Redistribution: δ ≤ allowed, δ_min = 0.64 + 0.8x/d checked, field moments ≥ elastic, min
      end-section moment rule checked
- [ ] ULS: μ→ω→A_s chain per member; shear V_Ed at d/a_v positions; punching u₁, β, v_min lower
      bound; compression λ_lim + ei/e2; χ/χ_LT curves per class
- [ ] SLS: w_k path (bar-limitation or direct) + f_fin with creep; NA exemption preconditions named
- [ ] Detailing: l_b/α_a/l_0/α_6, tension-line Versatz coverage, links zones, cover ↔ exposure
- [ ] Foundation: σ_E,d ≤ σ_R,d (method stated: simplified table vs full GEO-2), kern/open-joint
      logic, sliding/rocking/bearing trio each with γ; a_λ < d punching exemption
- [ ] Retaining: design case (active/increased/at-rest) selected per §9.2, δ values, redistribution
      only with stated prestress, trio checks + HYD/UPL/deep-slip referenced
- [ ] Fire/accidental: ψ_fi used, reduced section method (timber d_char, RC tabular) consistent with
      cold design
- [ ] Every **[VERIFY]**-flagged constant replaced from the current NA before signature
- [ ] Documentation: governing envelope, IFC property sets (§12.8), software + version + plausibility
      note recorded for the prüfbarer engineer

## 15. Appendix — digested numeric anchors (spot-value memory table)

| Item | Value (digest source) |
|---|---|
| f_cd C30/37 / C25/30 | 17.0 / 14.2 N/mm² (α_cc 0.85, γ_c 1.5) |
| f_yd B500 | 435 N/mm²; f_yd/f_cd = 25.6 (C30/37) |
| f_bd C30/37 good/moderate | 3.04/2.13 N/mm² |
| Cover c_min XC1/XC2/XC4/XD | 10/20/25/40 mm; Δc_dev 10/15 |
| w_k limits XC1/XC2-4/XD | 0.4 appearance / 0.3 / 0.3 (0.2 frequent) |
| ρ_w,min C25/30 / C30/37 | 0.70 / 0.83 ‰ |
| z = 0.9d; k = 1+√(200/d) ≤ 2.0; ρ_l ≤ 0.02 | EC2 shear constants |
| β punching 1.10/1.40/1.35/1.50/1.20 | int/edge/wall-end/corner/wall-corner |
| f_ywd,ef = min(250+d, f_ywd); rings κ 2.5/1.4; s_r ≤ 0.75d; s_t ≤ 1.5d | stud-ring design (worked) |
| λ_lim = max(25; 16/√n); ei = l_0/400; 1/r = ε_yd/(0.45d); e2 = K₁Kφ(1/r)l₀²/10 | column 2nd order (worked) |
| A_s,min col = 0.15N_Ed/f_yd [VERIFY]; A_s,max = 0.045A_c (100 % lap) / 0.08 | column steel |
| δ = 0.85; δ_min = 0.64+0.8x/d; B500A 15 %/B500B 30 % | redistribution |
| beff,i = min{0.2b_i+0.1l₀; 0.2b; b_i}; l₀ = 0.85/0.70·l_eff | T-flange (worked) |
| K (l/d) = 1.0/1.3/1.5/1.2/0.4; ρ₀ = √f_ck·10⁻³; flat l/d ≤ 1.2·150/√l | span/depth SLS rule |
| f ≤ l/250 (l/500 brittle); cant l = 2.5·l_k; timber l/200 / l/150 / net l/250 | deflection limits |
| σB simplified: ×1.2 rectangle, ×(1−0.1) width>2 m | DIN 1054 table use |
| ka(φ30)=0.333; ka0=0.5; eagh=½(ka+ka0)γz; δa=φ/2 (SW φ/3); δp=−φ′/3 (pit 2φ′/3) | earth pressure |
| γR,v 1.40/1.30 · γR,h 1.10 · γR,e 1.30–1.40 (BS-P/BS-T) | EN 1997/DIN 1054 (dated) |
| kmod 0.6/0.8/0.9/1.0; γM 1.3/1.1; kdef 0.6; kc,90 1.25/1.75; beff = (3+l+3)b | timber (NA) |
| χ curves a/b/c α 0.21/0.34/0.49; Φ = 0.5(1+α(λ̄−0.2)+0.75λ̄²); M = M_I/(1−N/Ncr) | steel stability |
| ψ0/ψ1/ψ2 A,B = 0.7/0.5/0.3; E 1.0/0.9/0.8; S≤1000m 0.5/0.2/0; W 0.6/0.2/0 | combinations |
| γG 1.35/1.0; γQ 1.5/0; EQU 1.1/0.9 | EN 1990 NA (1st gen; 1.22 → VERIFY) |
| Snow: Zone1 0.65; Zone2 0.25+1.91((A+140)/760)²≥0.85; Zone3 0.31+2.91(...)²≥1.10; μ1 0.8; μ2 0.8(60−α)/30; μ3 1.6≤γh/sk+μ2 | DIN EN 1991-1-3/NA (dated) |
| qp WZ1 0.50@10m …; cpe flat roof F−1.2/G−0.8/H−0.7; e=min(b,2h); A e/5; F e/4 | DIN EN 1991-1-4/NA |
| Tower: cf=2.16·1.0·0.63=1.36; Fw=cf·qp·Aref; e=b/10; 0.6Fw/wall; zs=0.6h | worked force method |
| fbd table; lb,min max(0.3lb,rqd;10Ø); l0,min max(0.3α1α6lb,rqd;15Ø;200) | anchorage/lap |
| 0.65(g+q)ln²/8 · 0.65(g+q)ln²/12 | min end-section moments |

## 16. Appendix A — load-derivation worked examples (compact, all digested)

### A.1 Roof slab as continuous beam — Passau, 60×19.5 m, h = 10 m (incl. 1 m parapet), 300 m NN

- g_k = 0.20·25 = 5.0; finishes Δg_k = 2.2; terrace live q_k = 4.0 (cat. Z; local 2.0 kN not
  needed); snow zone 2: s_k = 0.25 + 1.91·((300+140)/760)² = **0.89** ≥ 0.85; flat μ1 = 0.8 →
  s = 0.71 kN/m²; wind zone 1, mixed terrain II/III, z_e = h + h_p = 10 m → q_p = **0.50**
  (simplified); parapet roof cpe,10: F −1.2 / G −0.8 / H −0.7 / I +0.2,−0.6; h_p/h = 1/9.
- Load cases: LF1/LF2 independent permanent (structure/finishes — different γG use when one
  relieves); LF3–LF5 patterned live (combinable); LF6 snow all spans; LF7–LF9 wind per face
  (mutually exclusive) → **240 raw combinations → envelope**; rule of thumb: influence < 1 %
  → drop that wind group.
- SLS quasi-permanent example: max field moment M_2d = 1.0·M_2(g+Δg) + 0.3·M_2(q, LF4).

### A.2 Balcony cantilever — Köln, 22 cm slab, span 6.8 m + cantilever 2.8 m, 50 m NN

g_k = 5.5; Δg_k inside 1.2 / outside 1.8; railing line load G_k = 3.8 kN/m; live inside cat. A2
1.5 + partitions 1.2 (walls ≤ 5 kN/m incl. plaster); balcony cat. Z 4.0; snow zone 1: s_k = 0.65
(min governs) → s = 0.8·0.65 = 0.52.

- ULS support: M_Ad = −1.35·((5.5+1.8)·2.8²/2 + 3.8·2.8) − 1.5·4.0·2.8²/2 = **−76.5 kNm/m**
  (LF1+LF3).
- Shear at B: V_Bd = **−37.6 kN/m** (LF1+LF2; inside/outside finishes independent; relieving
  cantilever part enters with γG,inf = 1.0: 1.35·V(g+Δgᵢ) + 1.0·V(Δg_a+G_k) + 1.5·V(q+Δq)).
- **Overturning (EQU):** M_dst = 1.1·((5.5+1.8)·2.8²/2 + 3.8·2.8) + 1.5·4.0·2.8²/2 = **66.7**;
  M_stb = 0.9·(5.5+1.2)·6.8²/2 = **139.4** → 66.7 < 139.4 ✓.

### A.3 School mono-pitch roof wind — Köln, b 60 / d 9.0 / h 8.6, zone 1, q_p 0.50

Θ = 0° (low eave): e = min(b, 2h) = 17.2; A width e/5 = 3.44, e/d = 1.91, h/d ≈ 1:
cpe A/B −1.2/−0.8 (A zone −1.2, B −0.8), D +0.8, E −0.5; roof F width e/4 = 4.30, F/G depth
e/10 = 1.72: −1.3/−1.0/−0.4, pressure +0.1. Θ = 180°: roof −2.4/−1.3/−0.8. Θ = 90°: e = 9.0,
e/d = 0.15 < 1, A 1.8/B 7.2/C 51, h/d = 0.14 ≤ 0.25: −1.2/−0.8/−0.5 leeward, +0.7 windward,
E −0.3; roof F_hoch −2.2 / F_tief −1.8 / G −1.8 / H −0.7 / I −0.6; H–I transition at 4.5 m.

### A.4 Office tower force method — Hannover, h 36 / b 36 / d 12, zone 2 q_b 0.39

cf,0(d/b = 0.33) = 2.16, ψr(r/b = 0) = 1.0, ψλ(λ = h/b = 1) = 0.63 → cf = 1.36; block
(λ ≤ 2); q_p(36) = 1.7·0.39·(3.6)^0.37 = 1.07 kN/m²; A_ref = 1296 m²; F_w = 1.0·1.36·1.07·1296
= **1886 kN**; two walls, e = b/10 = 3.6 m, single-span diaphragm L = 36 → max 0.6·F_w =
**1132 kN/wall**; cantilever resultant z_s = 0.6h = 21.6 m → base M = **24,450 kNm**.

### A.5 Snow drift — terraced houses + flat garages, Nürnberg (zone 1, 310 m → s_k = 0.65)

Tandem gables 45°: μ2 = 0.8·(60−45)/30 = 0.4 both; valley μ3 = 1.6 ≤ γ·h/s_k + μ2 =
(2·2.5)/0.65 + 0.4 = 8.1 ✓; LF(a) 2×0.4·0.65 = 0.26 + flat 0.52; LF(b) 0.26 + μ3·s_k = **1.04**.
Garage next to 45° roof (Δh, b = 2.5): l_s = 2·Δh = 2 → **min 5 m governs**; sliding
S = 0.5·(0.26·5.0/2) = 0.325 kN/m → μs = 2S/(l_s·s_k) = 0.2; μw = (5.0+2·2.5)/(2·1.0) = 5 → cap
γ·h/s_k = 3.08 → μ2 = 3.28 → **cap 2.4 governs** [cap logic partially garbled, final printed];
final loads μ1·s_k = 0.52, μ2·s_k = **1.56 kN/m²**.
Shed roof Garmisch (zone 3, 750 m): s_k = 4.30; flat 0.8·4.3 = 3.44; μ2(30°) 0.8, μ2(90°) 0;
μ3 = 1.6 ≤ (2·1.45)/4.3 + 0.8 = 1.47 → **1.47 governs** → s3 = 6.32; right flat: drift
0.67 < 0.8 → μ1, no accumulation: 3.44.

## 17. Appendix B — statics worked examples (analysis plausibility)

### B.1 3-span continuous beam, force method (spans 5.6/7.0/5.6, q₁ 52, F 200 in mid BC, q₃ 36)

Primary system: hinges at B, C. Isostatic moments M⁰ = ql²/8 = 203.84 (AB), Fl/4 = 350 (BC),
141.12 (CD). Flexibilities (÷EI): δ₁₁ = δ₂₂ = 4.2000, δ₃₃ = 1.8667, δ₁₂ = 1.1667, δ₂₃ = 0.9333,
δ₁₃ = 0; load terms δ₀₁ = −993.00, δ₀₂ = −875.92, δ₀₃ = −263.42 → **X = −198.3/−137.4/−72.4 kNm**
support moments. Final: V: A 110.2; B −181.0/+108.7; C −91.3/+112.4; D 89.2; R: A 110.2,
B 289.7, C 203.7, D 89.2; ΣV = 692.8 = total load ✓; field maxima M₁ = V_A²/(2q₁) = 116.76,
M₂ = 182.15, M₃ = 38.07 kNm. (Use as FEM cross-check case.)

### B.2 UPE 400 trench-crossing beams (temporary, channel-section torsion)

q = 20·2.75/2 = 27.5 kN/m, l = 7.5 → V = 103.1 kN, M = 193.4 kNm. UPE400: Iy 20981 cm⁴,
y_T = 6.06 cm, e = 2.98, Is = 82.2 cm⁶.
- Variant 5.1 timber planks on bottom flanges: plank span 2.63 m → M' = 17.29 kNm/m; load-line
  offset from torsion axis = 6.06 − 2.98 + 6.00 = 9.08 cm → m_T = 27.5·0.0908 = 2.497 kNm/m;
  M_tA = 9.364 kNm; St. Venant τ = M_t/I_s ≈ 20.5 kN/cm² → **too large, rejected**.
- Variant 5.2 monolithic RC deck: load plane through shear centres, deck span 2.812 m →
  M = 19.77 kNm/m = **+14.3 % vs 5.1** — design deck for it. Rule: channel + off-centre load →
  warping + St. Venant torsion; edge-form decks raise deck moment ~+14 %.

### B.3 Two-hinged portal (L 7.0, h 3.5, q 25 kN/m roof, allowable-stress print)

Self: A = B = 87.5 kN; thrust H = **18.06 kN** (= 5qL/(32(1+k)) classical); M_corner = −H·h =
−63.21 kNm; M_field = M⁰ − |M_corner| ≈ 153.1 − 63.2 = **89.9 kNm** [printed 89.92 ✓].
Imposed 10 kN/m ×0.40 → H = 7.22; wind total 11 kN → H_A = ∓5.50, M_corner 19.25. σ = N/A +
100·M/W: column corner 160 MPa (S235-era allowable check).
Dynamics: m = 175/9.81 = 17.84 t; δ = 6.487·10⁻⁴ m/kN → k = 1541 kN/m; ω = 9.29 s⁻¹;
**T = 0.676 s**. Explosion p̂ 0.4 bar·11 m² = 440 kN, t_d 30 ms ≪ T → J = ½·0.03·440 = 6.6 kNs →
v₀ = 0.370 m/s → x_max = 0.0398 m → H = 61.3 kN → M_corner 107.3 → σ ≈ 24.5 kN/cm² with EG
[final sum garbled]. EQ (DIN 4149-era spectrum, T = 0.676, zone 2, C-T, class III): a = 1.33
m/s² → H = 23.7 kN → σ = 153 MPa incl. EG. → for modern EC8 values use sibling seismic-design.

### B.4 Elastic prop via force method (beam + steel rod at B)

δ₁₁ = 3.1255/EI (+ rod term), δ₁₂ = 0.7776, δ₂₂ = 3.0248; δ₀₁ = −132.11, δ₀₂ = −168.64 →
X₁ = −30.45, X₂ = −47.93 kN → rod N = 94.12 kN, Δl = 0.713 cm. Approximation (digested):
rigid-prop analysis + treat Δl as support settlement and superpose — results close; use for
plausibility of elastically-supported models.

## 18. Appendix C — masonry verification examples (EC6 NA, condensed; details in sibling)

### C.1 Bearing exterior wall (HLz 8-0.9/LM21, t 30, h 2.51, b 4.25, slab l_f 4.48, a 160, fk 2.5)

Simplified (EN 1996-3) applicability: H 9.8 < 20; l_f ≤ 6; t ≥ 240; h < 3.6 = 12t; q_k ≤ 5;
a ≥ 0.5t ✓. N_Ed = 102.56/109.14/115.71 kN/m (head/mid/base; 1.35G+1.5Q; wall G 3.88·h/2..h).
4-sided held (b < 30t = 9 m), α₄ = 1, ρ₂ = 1 → h_ef = **1.86 m**; Φ = min(Φ₁ = (1.6−l_f/6)(a/t)
+ 0.9(a/t)² → 0.455; Φ₂ = 0.85(a/t)[1 − 0.0011(h_ef/t)²]/(h_ef/t) [printed garbled **[VERIFY]**]
→ 0.411); f_d = ζ·f_k/γ_M = 0.85·2.5/1.5 = **1.42 N/mm²**; N_Rd = Φ·t·f_d = 175 kN/m >
115.71 ✓. General rules variant: node moments via NA Annex-C frame analog (stiffness factors
c_i, η = 0.5), e_m = (M½(M_o+M_u)+M_h)/N + (t−a)/2 + e_ini (h_ef/450 = 0.00413 ≥ 0.05t cap?
printed 0.076 governs), Φ_m = 0.414 governs → 176.4 > 108.67 ✓; planned eccentricity ≤ t/3 also
characteristic → exempt.

### C.2 Shear wall (in-plane, PP6/DM open head joints, t 24, h 2.51, l_w 2.0)

V_Ed = 1.35·1.56 + 1.5·10.4 = **17.7 kN** (plumb share with γG); base moment 44.4 kNm; use MIN
vertical N (1.0G = 73.5): in-plane bending e = 0.604 → Φ₁ = 1 − 2e/l_w = 0.396 →
N_Rd = Φ₁·t·l_w·ζf_k/γ_M = 441.6 > 73.5 ✓; edge strain (SLS rare): e < l_w/3 ✓ (no crack to
centroid), l_c = 3(l_w/2 − e) = 1.78, σ_D = 2N/(l_c·t) = 0.344.
Shear: f_v,k0 = 0.5·0.22 = 0.11 (open joints); l_c,lin = (2/3)l_w(1 − 1.5σ_Dd/E_min) = 1.19;
f_v,lt,1 = 0.11 + 0.4·0.257 = 0.213; f_v,lt,2 = 0.45·f_bt,calc·√(1+σ_d/f_bt) = 0.155 governs →
f_v,d = 0.104; l_cal = min(1.125·2.0; 1.333·l_c,lin) = 1.59; c = 1.0 + 0.5(λ_v − 1) = 1.128
(λ_v = h/l = 1.255); **V_Rd = l_cal·f_v,d·t·c = 35.18 > 17.7 ✓**.
Simplified limits (Tafel 1.1): t ≥ 115 → h ≤ 2.75; t ≥ 150: 2.75/3.0/3.3 by f_k; t ≥ 240/300:
"12·t"/none; no interpolation between f_k classes; q_k ≤ 3.0; lightweight 175 only w_k < 1.1.
h_ef = ρ_n·h: ρ₂ 0.75 (t ≤ 175)/0.9 (≤250)/1.0 (>250) two-sided; ρ₃ = 1/(1+(ρ₂h/3l)²) − 0.3
(h ≤ 3.5l); ρ₄ = ρ₂/(1+(ρ₂h/l)²) (h ≤ 1.5l) else 0.5l/h.

### C.3 Basement masonry wall without calculation (EN 1996-3)

Clear height ≤ 2.60 m, t ≥ 200 mm, slab diaphragm, live ≤ 5 kN/m², no single load > 15 kN within
1.5 m, backfill ≤ wall height, no rising ground surface, no permanent groundwater pressure, no
sliding plane through waterproofing. Cellar wall KS example (t 24, h 2.35, b 5.25, backfill 1.05):
arch-model Grenzlasten band: N_Ed,max = (1.35·11.5+1.5·5.0)·5.25 = 120.9 ≤ N_Rd,max = ⅓·t·b·f_d·10³
= 1302 ✓; N_Ed,min = 60.4 ≥ N_Rd,min = γe·b·h_e·(h/t)/β_l = 53.8 ✓ (β_l = 20 one-way, b > 2h;
constants **[VERIFY]** — stable both limits → no earth-pressure/bending/shear checks).

## 19. Appendix D — bracing / second-order examples already embedded

- Non-sway office building check (worked): F_v,Ed = 5.53 MN; ΣI_c = Σ(L³t/12) = 11.515 m⁴ →
  F_v·L²/(E_cd·ΣI_c) = 0.000115 ≤ 0.172 = 0.31·(2+1)/(1+1.6) ✓ → first-order OK; walls
  t = 0.24; imperfection α = 0.008/√(2·2) = 0.004 rad → H = 15.22 kN/storey → diaphragm chord
  M = H·l/8 = 95.14 kNm (+ wind).
- 11-storey sway + torsion variant (worked): F_V,Ed = 42.3 MN; E_cd = 20800 MN/m²; ΣI_y =
  12.40 m⁴ → 0.179 ≤ 0.271 ✓; ΣI_z = 28.73 → 0.077 ✓; remove one 8 m wall → Y_M = 3.29 m,
  combined (I_T = 0 conservative) 0.240 ≤ 0.271 ✓ → 2nd-order analysis may be omitted per axis.
- Stiffness sharing with shear deformation: k₁ = 0.3931·E·t³, k₂ = 0.1429·E·t³ → walls 73/27 %
  (worked; f = H³/3EI + 1.2H/GA, G = 0.4E).
- Steel braced frames: cantilever-column hall bracing f = 1/304 imperfection → H_Ed = ΣV/304 +
  wind, split by stiffness; 2nd order ϑ_II, base moments 130.2/175.2 kNm; σ check vs f_y/γ_M1
  32.27 kN/cm² — **both just satisfied, SLS head displacement h/80 fails → stiffen columns**
  (worked lesson: ULS pass ≠ SLS pass).

---

*Scope reminder: every number above is a digested worked-example or handbook value with its
[VERIFY] flags where the extraction was garbled or the NA edition is dated. The current National
Annexes and the responsible prüfbarer engineer's review govern in all cases.*
