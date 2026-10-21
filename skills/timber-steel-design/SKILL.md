---
name: timber-steel-design
description: >
  Structural design of timber (Nadel- und Laubholz) and steel building systems to
  Eurocode 5 and Eurocode 3 for DACH practice: timber products and strength classes
  C14-C40 / D30-D70 / GL24h-GL36h plus CLT, LVL, duo/trio beams with fm,k / ft,0,k /
  fc,0,k / fv,k / E0,05 tables, kmod by load duration + service (use) class, kdef,
  gamma_M = 1.3 members / 1.1 simplified fastener check / reduced gamma_M,fi in
  fire; member design (bending incl. lateral-torsional buckling k_crit chain, axial
  buckling kc chain, shear cracked-section b_ef, bearing perpendicular to grain
  kc,90, biaxial bending km = 0.7/1.0, deflection + vibration serviceability,
  notched ends kv and transverse tension reinforcement); joints (nails with
  penetration t >= 9d, screws with f_ax,k and glued-in rods fg,k = 4.0 N/mm2,
  dowels/bolts via the yield model with spacing rules a1 = (3+2|cos a|)d etc., ring
  and shear connectors, DIN 436/440 plates, effective number n_ef); DIN 68800 use
  classes GK0-GK5 and constructional wood protection; steel: profile families
  (IPE, HEA/HEB/HEM, channels, hollow sections) with an A/I/W excerpt table,
  cross-section classes 1-4 + EN 1993-1-5 effective widths, tension, Mpl,Rd bending
  with MV/MN interaction, shear Av, web bearing, bolted connections (grades
  4.6-10.9, preloaded HRSG, Fv,Rd/Fb,Rd, spacing limits, T-stub, block shear),
  welded connections via fw with beta_w, buckling curves a-d with the chi chain,
  lateral-torsional buckling Mcr -> chi_LT,mod, imperfection and bracing loads;
  combined checks in sigma/fd <= 1 format; corrosion protection classes +
  galvanizing; fire (timber charring rate beta_n + notional layer 7 mm; steel
  critical temperature and protection menu); framing systems in practice (stud and
  panel, solid timber/CLT multi-storey, glulam portals and trusses, steel portals,
  trusses and composite beams) with span/depth rules, plus FreeCAD/IFC modelling
  defaults. Use when selecting, sizing, checking or modelling timber or steel
  load-bearing structures for buildings.
---

# Timber & Steel Design for Buildings (EN 1995 / EN 1993, DACH practice)

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

This skill covers the **design logic, code values and detailing rules** for the two
linear-material systems of European building construction: timber construction
(Holzbau) to **Eurocode 5 (DIN EN 1995-1-1 + National Annex)** and steel
construction (Stahlbau) to **Eurocode 3 (DIN EN 1993-1-1 + National Annex)**,
including the fire parts (EN 1995-1-2 / EN 1993-1-2) and the connection rules
(EN 1993-1-8 / -1-5, EN 1995-1-1 §8 with fastener ETAs/abZ). It is the
design-level companion to the framing-systems skill (which answers *which system*)
and to `building-materials` (which answers *what the product is*).

**In scope:** material/design values, member verification chains, fastener and
welded connection checks, stability (buckling / lateral-torsional buckling),
serviceability (deflection, vibration), durability and use classes, structural
fire design, practical framing systems with span/depth rules, worked calculation
chains, FreeCAD/IFC modelling defaults.

**Out of scope:** whole-building action tables and combinations (→ a
loads/structural-systems skill), seismic design (→ seismic-design), foundation
design under column feet and hold-downs (→ geotechnics-foundations), execution and
contract logic (→ construction-detailing), concrete and masonry design
(→ concrete-detailing, masonry-construction).

## Sibling skills

| Skill | Where this file hands off |
|---|---|
| structural-systems | system choice at building level (massive vs timber vs steel) |
| building-materials | product standards, densities, λ/μ data, CE/DoP status of sections & boards |
| fire-protection-building | building classes GK1-GK5, required F/R durations, escape routes |
| construction-detailing | joint geometry, water-shedding, layer sequences, tolerance strategy |
| concrete-detailing | steel/timber-to-concrete interfaces: anchors, base plates, WCC topping |
| seismic-design | horizontal actions, ductility, bracing system choice |
| geotechnics-foundations | uplift and thrust into ground; column feet |

---

## Reality check — read before using any number

1. **This skill produces design aids and calculation guidance for planning,
   pre-dimensioning and FreeCAD modelling ONLY.** Every span, section, bolt count,
   screw spacing and charring rate below is a preliminary sizing aid, a code
   minimum, a table excerpt, or a rule of thumb.
2. **Any design intended for construction of a real occupied building must be
   analysed, designed and signed by a qualified structural engineer** (in Germany:
   Tragwerksplaner per Landesbauordnung, plus Prüfstatik where required; in
   Austria/Switzerland the locally licensed equivalent). This is *more* true for
   timber and steel than for massive construction: these systems are
   **connection-governed, stability-governed and uplift-governed**. A missed
   hold-down, an unbraced compression flange or an under-designed bolt group is a
   collapse mechanism, not a crack.
3. **National Annex (NA) differences are the rule, not the exception.** gamma_M
   values, kmod wind rules, lateral-torsional buckling parameters, buckling curve
   assignments and deflection recommendations differ DE/AT/CH and move with every
   code edition. The digests behind this file reflect **EC5 2010-12 + German NA
   2013-08 (+ A2 2014)** and **EC3 + German NA, early-2020s handbook state** —
   VERIFY the currently introduced edition per project.
4. **Values reconstructed from source digests carry a** `VERIFY` **flag.** Treat
   the flags as binding. Several table columns were transposed or garbled during
   extraction (flagged where detected). Never quote a flagged number to a
   fabricator.
5. **Never present model output, a span-table lookup or a calculation from this
   file as construction-ready.** The correct framing is always "preliminary
   sizing and coordination geometry — requires design and signature by a qualified
   structural engineer". Say it unprompted when a user starts ordering steel,
   sending cutting lists to a timber workshop, or deleting a brace "because the
   model still stands".
6. **Never certify.** No stamped drawing, no stability certificate, no
   fabrication drawing presented as approved-for-construction.
7. **Loads are never assumed.** Basic wind speed, snow zone, site elevation, use
   category and (where relevant) seismic zone come from the current maps and the
   project brief. Lightweight structures are frequently **uplift-governed rather
   than gravity-governed** — the reverse of massive construction.

### Evidence tiers

| Tier | Meaning | Examples here | Use |
|---|---|---|---|
| T1 | EN + NA design value formulas and tables | fm,k, kmod, gamma_M, chi-curves, Fv,Rd | citable after edition check |
| T2 | Product-standard geometry (EN 10365, EN 336, EN 14080, EN 16351) | profile nominal sizes, tolerances | spec-grade after lookup |
| T3 | Handbook tables and worked-example digests | section property excerpts, Rk of nails, bolt capacities | guidance; flagged cells |
| T4 | Rules of thumb | span/depth ratios, 1-2 % bracing force | massing only |

---

## Section 1: Code basis — what governs what

### 1.1 Standards map

| Topic | Timber | Steel |
|---|---|---|
| Basis / actions | DIN EN 1990, EN 1991-1-1…-1-6 + NAs | same |
| Design (ULS/SLS) | **DIN EN 1995-1-1 + NA** | **DIN EN 1993-1-1 + NA** |
| Fire | DIN EN 1995-1-2 + NA | DIN EN 1993-1-2 + NA |
| Connections | EN 1995-1-1 §8 + fastener ETAs / abZ | **EN 1993-1-8** (bolts, welds), EN 1993-1-5 §6 (web bearing/stiff panels) |
| Plates / class 4 | EN 1995-1-1 §6.2 (cracked-section shear) | **EN 1993-1-5** (effective widths, patch loading, shear buckling) |
| Buckling / LTB | EN 1995-1-1 §6.3 | EN 1993-1-1 §6.3 |
| Composite floors | wood–concrete (WCC) via ETA pin connectors | **EN 1994-1-1 / -1-2** (head studs, trapezoidal sheet) |
| Material products | EN 338 (strength classes), EN 336 (sizes & deviations), EN 408 (test/strength), DIN 4074-1 (visual/machine grading S7/S10/S13), EN 1194 + EN 14080 (BSH/glulam), EN 16351 (CLT/Brettsperrholz), EN 14374 (LVL), EN 15497 (finger-jointed solid), (duo/trio beams: Balkenschichtholz via EN 14080), EN 636 (plywood), EN 300 (OSB) | EN 10025 (hot-rolled grades S235…S700), EN 10210/-10219 (hollow sections), EN 10365 (nominal sizes & designation), EN 10218 (welded sections) |
| Fasteners | EN 14592 (dowels, nails, screws, bolts — strength & stiffness), EN 10230-1 (nail dimensions), EN 14566 (ring & shear plate connectors), EN 14545 (screw-in inserts), ETAs for structural screws and glued-in rods | EN 15048 (fit bolts), **EN 14399 (preloaded HRSG 8.8/10.9)**, ISO 4063 + ISO 2553 (weld process/symbols), EN 1090-2 (execution) |
| Durability | **DIN 68800-1 (Gebrauchsklassen GK0-GK5), -2 (chemical + constructional protection)**, DIN 4074-1, EN 350 (natural durability) | EN ISO 12944 (corrosivity categories C1-C5 + immersion), EN ISO 1461 (hot-dip galvanizing), EN 10346 (continuously coated strip) |
| Execution | DIN 18334 (ATV timber works), trade rules of the roof/carpentry trades | **EN 1090-1/-2 (EXC 0-4)**, DIN 18335 (ATV steel works) |
| Fire classification | DIN 4102 / DIN EN 13501-2 (F30-F180 ↔ R/E/I) | same |

> ⚠ **VERIFY** editions and NA currency per Bundesland/country before citing.
> Fastener approvals are time-limited: a handbook may list a punched-plate/angle
> connector approval (abZ) whose validity expired years earlier — never carry an
> approval number from a table into a project without checking its current status.

### 1.2 Partial factors and combinations (starting point, German NA of the digest edition)

**Actions (persistent/transient, STR):** γ_G unfavourable 1.35 / favourable 1.00;
γ_Q 1.50. ψ0/ψ1/ψ2 for buildings: living/office A,B 0.7/0.5/0.3; assembly C
0.7/0.7/0.6; retail D 0.7/0.7/0.6; storage E 1.0/0.9/0.8; roof (non-accessible) H
0/0/0; snow ≤ 1000 m NN 0.5/0.2/0.0; wind 0.6/0.2/0.0.

**Timber resistances:** γ_M = **1.3** members (solid, BSH, and most wood-based
panels incl. CLT/Balkenschichtholz); γ_M = **1.1** dowel-type connections by the
simplified verification; **1.3** exact yield-theory check; **1.3** ring/
shear-plate connectors (§5.7 — different failure mode from dowel bending, do
not reuse 1.1); steel connector parts in tension/shear 1.3; nail-plate
(Nagelplatte) plate check 1.25.

**Fire design — CORRECTED, the earlier "γ_M,fi table" was a mislabelling, not
a real contradiction with the worked example** (Neuhaus, Ingenieurholzbau,
4th ed. 2017, p.155/159-160/174-176, Tab. 4.12, EN 1995-1-2 Tab. 2.1 +
DIN EN 1995-1-2/NA NDP to 2.3(2) Note 1): the differentiated table (solid
1.25, glulam 1.15, panels 1.15, **LVL 1.1** — resolves the "1.0 (1.1 in the
digest)" ambiguity in favour of **1.1**, shear connections timber-side 1.15 /
outer-steel-plate 1.05, pull-out 1.05) is actually **k_fi**, the coefficient
converting the 5 %-characteristic value to the 20 %-quantile fire strength:
f_20 = k_fi·f_k. **γ_M,fi itself is 1.0, uniformly, for ALL timber materials
and connections** — so the correct fire design equation is
f_d,fi = k_mod,fi·(k_fi·f_k)/1.0, with k_fi in the *numerator*, not a γ_M in
the denominator. The worked fire example (which applies 1.0 to member
bending) was already right; only the general statement needed relabelling
and moving k_fi to the correct place in the equation.

**Steel resistances:** γ_M0 = 1.0 (cross-section), γ_M1 = 1.1 (stability:
buckling, LTB, patch loading per 1993-1-5), γ_M2 = 1.25 (net sections, bolt
bearing, welds) — as used in the worked example chains of this file.
> ⚠ **VERIFY** NA state (γ_M1 was 1.0 for section checks in the example chain for
> tension M-N interaction; treat 1.0/1.1 split as edition-dependent).

**Timber combination rule (the classic trap):** design value
X_d = X_k · k_mod / γ_M sits in the *denominator*, so the governing load case is
the one with maximum **F_d / k_mod**, not maximum F_d. Example (solid/BSH, CL1):
1.35G + 1.5S → F_d = 12.4 kN/m over k_mod 0.6 → 20.7; 1.35G + 1.5W → k_mod 1.0.
Always run the division for every combination (permanent 0.6, snow short 0.9,
wind NA 1.0, medium 0.8, very short 1.1).

**Fire combination (both materials):** γ_G = γ_Q = 1.0, variables at ψ1
(worked timber R30: 0.5); exceptional design situation.

---

## Section 2: Framing-system taxonomy (generic)

### 2.1 Timber systems

| ID | System | Load path | Lateral system | Design consequence |
|---|---|---|---|---|
| T1 | **Stud-and-panel frame (Holzrahmenbau)** — platform (storey-high walls on deck) or balloon (2-storey studs + let-in band) | sheathing → studs → top/sill plate → deck/plate → foundation | shear-stiff board sheathing (nail/screw line spacing = capacity) or crossed braces; hold-downs at panel ends | every chord force is a fastener-group design; studs must sit under joists (in-line framing); platform settlement = cumulative perpendicular compression (limit storeys or use T2) |
| T2 | **Solid timber (Massivholz)** — board stack (BSP), CLT (Brettsperrholz), X-lam LVL | gravity end-grain → end-grain (no transverse compression), so stacking is settlement-free | glued/dowel-laminated panels act as diaphragms and disc plates | CLT outer plies define span direction; ~50 % of section effective along grain in walls; large sawn openings possible; few joints = easy airtightness |
| T3 | **Post-and-beam / frame (Ständerwerk, Skelett)** — glulam/LVL columns + beams | beam → column via steel insert, slotted plate, saddle timber, or pincer detail | braced bays, cores, or moment frames | node = perpendicular-tension (splitting) problem; twin beams either side of column halve eccentricity; interposed horizontal timber in compression path = long-term settlement |
| T4 | **Roof systems** — purlin roof (Pfettendach), rafter roof (Sparrendach), truss/binder roof | purlins on trusses/posts; rafter+tie triangle; binder with diagonals | triangulated truss planes, sheathing, ridge/purlin bracing | purlin roof = bending structure, lightest depth; rafter roof needs a real tie (tie beam suspended against sag, collar in upper third); binder = slender chords, large depth |
| T5 | **Traditional/hybrid** — log (Blockbau), half-timber (Fachwerk), timber-laced masonry, timber beams in masonry houses | stacked members / storey-high trusses with braced panels | integral diagonals (Kopf-/Fußband), sheathing | settlement and shrinkage must be absorbed in details; beam ends into masonry: ventilated, GK class rises; Fachwerk grid ≈ 1.25 m Alemannic canon; solid floor beams ≤ ~5 m |
| T6 | **Wood–concrete composite (WCC)** floor | concrete compression chord + timber tension chord via shear connectors | slab diaphragm | connector pattern governs; moment reversal in continuous/cantilever systems swaps chords; concrete gives mass (acoustics) + fire + protection |

### 2.2 Steel systems

| ID | System | Load path | Notes |
|---|---|---|---|
| S1 | **Portal frame** (2- or 3-hinged, haunched) | rafter–column moment frame → base plate → footing | in-plane stiff → open end façades; longitudinal bracing still needed; 3-hinged apex pin lets halves be transported if frame height ≤ ~4 m |
| S2 | **Trusses (Fachwerkträger)** — parallel-chord, pitched, bow | chords carry the moment as a couple; diagonals shear | load at nodes only; tension diagonals preferred; short compression diagonals; avoid twin slender compression bars, acute angles; non-triangulated quads = Vierendeel = heavier |
| S3 | **Braced/multi-storey frame + composite floors** | beams → columns → core/braces → foundation | head studs make the slab a compression flange; slim-floor keeps services below a flat soffit; pinned default (fin plate), moment where drift demands |
| S4 | **Grid shells / space frames / cable systems** | membrane-like in-surface forces | triangulation = pure axial; quad grids need diagonal bracing; cables use steel's tension fully (no buckling); node cost, not member cost, rules |
| S5 | **Cold-formed light-gauge framing** | stud-and-panel analogue in steel | design to EN 1993-1-3/-1-5 (class 4 always, stiffened plates) — system logic in the framing-systems skill |

### 2.3 Span/depth working limits (T4 — massing only)

| Element | Preliminary depth | Practical band |
|---|---|---|
| Steel rolled beam | h ≈ L/10 … L/18 | rolled to ~20 m; beyond → welded girder h ≈ L/8 … L/12 |
| Steel portal rafter | depth ≈ L/40 … L/55 (haunch: 1.5-2× rafter depth, length L/10 … L/7) | clear spans 12-35 m economical |
| Composite beam | h ≈ L/18 … L/22 | office grids 6-12 m |
| Truss (steel) | depth ≈ L/10 … L/16 | 10 m → >100 m |
| Timber binder (truss) | depth ≈ L/6 … L/12 | 8-25 m |
| Glulam beam | h ≈ L/15 … L/20 | ~20 m practical with restraint |
| Timber joist | h ≈ L/18 … L/24 | 3-6 m; box/trough elements to 14 m; rafters and purlins of a house: spacings and preferred sections in S.1 to S.3 |
| CLT one-way floor | t ≈ L/30 … L/35 | 3-6 m (5-ply typical) |

> ⚠ **VERIFY** at analysis: at the ends of every band, buckling, LTB, deflection,
> vibration, fire or the connection governs — not bending strength.

### 2.4 Non-negotiable conceptual rules (both materials)

1. **A frame is stiff in its plane only.** Portal/skeleton systems need an
   explicit bracing system in both directions; without it the building is a
   mechanism longitudinally. Show the bracing on the model.
2. **Buckling length = spacing of the restraints you designed,** not the member
   length. Unrestrained compression flange (rafter soffit at eaves, column inner
   flange, truss top chord) → fly braces, knee braces, sheetingdiaphragm
   attachments. Missing fly-bracing is the classic portal failure.
3. **Uplift must reach the ground in a designed chain:** cladding fasteners →
   purlin → cleat → rafter/truss → clip → plate → stud → anchor/hold-down →
   foundation. Every link designed; no "bedding friction".
4. **The connection IS the structure.** Timber: dowel group + perpendicular
   tension path. Steel: bolt group, weld, plate bending, block shear, web
   crippling, column-flange deformation — checked separately.
5. **Bearing needs area and a path around weakness:** timber perpendicular
   compression (k_c,90 + (3+l+3)·b spreading), steel unstiffened web (crippling
   check), base plate on grout with a shear key (Schubknagge) so anchors take
   uplift, not shear.
6. **Horizontal thrust of a pitched frame goes into a tie or a moment base —
   never "the slab".** Hand check H ≈ w·L²/(8f) (three-hinged, conservative).
7. **Shop-weld, site-bolt.** Field welding means no procedure control, no NDT,
   damaged coating; redesign the detail instead.

---

## Section 3: Timber material and characteristic values

### 3.1 Solid softwood classes (Nadel-Vollholz, DIN EN 338 / EN 1995-1-1 Table 3.1)

Characteristic values N/mm² at reference moisture 12 % (sizes per EN 336). Grading
per DIN 4074-1: S7 → C16/C18 (fir/larch/Douglasie C16; Fichte/Kiefer C18),
S10 → C24, S13 → C30/C35 (Douglasie C35); dry-graded (TS) ≤ 20 % MC.

| Class | f_m,k | f_t,0,k | f_t,90,k | f_c,0,k | f_c,90,k | f_v,k | f_r,k | E_0,05 | E_0,mean | E_90,mean | G_mean/G_0,05 | ρ_k | ρ_mean |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| C18 | 18 | 10 | 0.4 | 18 | 2.2 | 3.4 | 0.8 | 6000 | 9000 | 300 | 560 / 375 | 320 | 380 |
| C24 | 24 | 14.5 | 0.4 | 21 | 2.5 | 4.0 | 0.8 | 7400 | 11000 | 370 | 690 / 460 | 350 | 420 |
| C30 | 30 | 19 | 0.4 | 24 | 2.7 | 4.0 | 0.8 | 8000 | 12000 | 400 | 750 / 500 | 380 | 460 |
| C35 | 35 | 22.5 | 0.4 | 25 | 2.7 | 4.0 | 0.8 | 8700 | 13000 | 430 | 810 / 540 | 390 | 470 |
| C40 | 40 | 26 | 0.4 | 27 | 2.8 | 4.0 | 0.8 | 9400 | 14000 | 470 | 880 / 590 | 400 | 480 |

**CONFIRMED against Wendehorst Bautechnische Zahlentafeln (37th ed.) Tab. 12.1,
itself citing DIN EN 1995-1-1:2016-07 Tab. 3.2 / DIN EN 338:2010-02 Tab. 1** —
the table above is correct as printed (E_0,05 < E_0,mean, not transposed;
G_05 = 2/3·G_mean per NA). Two cells corrected against that source: C24 f_v,k
is **4.0** (not 3.5 — only C18 sits at 3.4, all of C24-C40 are flat at 4.0),
and C35 f_c,90,k is **2.7** (not 2.8). E_90,mean column added from the same
table (was previously only a single ⊥-grain estimate in §3.5).

### 3.2 Solid hardwood (Laubholz, DIN EN 338)

| Class | f_m,k | f_t,0,k | f_t,90,k | f_c,0,k | f_c,90,k | f_v,k | E_0,mean | E_0,05 | E_90,mean | G_mean/G_0,05 | ρ_k | ρ_mean | typical species |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| D30 | 30 | 18 | 0.6 | 24 | 5.3 | 3.9 | 11000 | 9200 | 730 | 690 / 460 | 530 | 640 | Eiche (oak), LS10 |
| D35 | 35 | 21 | 0.6 | 25 | 5.4 | 4.1 | 12000 | 10100 | 800 | 750 / 500 | 540 | 650 | Buche (beech), LS10 |
| D40 | 40 | 24 | 0.6 | 27 | 5.5 | 4.2 | 13000 | 10900 | 870 | 810 / 540 | 550 | 660 | Buche, LS13 |
| D60 | 60 | 36 | 0.6 | 33 | 10.5 | 4.8 | 17000 | 14300 | 1130 | 1060 / 710 | 700 | 840 | Buche (high grade) |

f_r,k ≈ 1.2. **CONFIRMED against Wendehorst Tab. 12.2** (DIN EN 338:2016-07
Tab. 3) — D60 f_t,90,k and f_v,k are exactly 0.6 / 4.8 as printed, not
uncertain; E/G/ρ columns not transposed. G_mean/G_0,05 and E_90,mean columns
added from the same source (previously missing for hardwood).

### 3.3 Glulam / BSH (DIN EN 1194/14080, combined "c" and homogeneous "h" strength)

| Class | f_m,k | f_t,0,k | f_t,90,k | f_c,0,k | f_c,90,k | f_v,k | f_r,k | E_0,mean | E_0,05 | E_90,mean/05 | G_mean/G_05 | G_r,mean/G_r,05 | ρ_k | ρ_mean |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| GL24c (combined) | 24 | 17.0 | 0.5 | 21.5 | 2.5 | 3.5 | 1.2 | 11000 | 9100 | 300/250 | 650/540 | 65/54 | 365 | 400 |
| GL28c | 28 | 19.5 | 0.5 | 24.0 | 2.5 | 3.5 | 1.2 | 12500 | 10400 | 300/250 | 650/540 | 65/54 | 390 | 420 |
| GL30c | 30 | 19.5 | 0.5 | 24.5 | 2.5 | 3.5 | 1.2 | 13000 | 10800 | 300/250 | 650/540 | 65/54 | 400 | 430 |
| GL32c | 32 | 19.5 | 0.5 | 24.5 | 2.5 | 3.5 | 1.2 | 13500 | 11200 | 300/250 | 650/540 | 65/54 | 400 | 440 |
| GL24h (homogeneous) | 24 | 19.2 | 0.5 | 24 | 2.5 | 3.5 | 1.2 | 11500 | 9600 | 300/250 | 650/540 | 65/54 | 385 | 420 |
| GL28h | 28 | 22.3 | 0.5 | 28 | 2.5 | 3.5 | 1.2 | 12600 | 10500 | 300/250 | 650/540 | 65/54 | 425 | 460 |
| GL30h | 30 | 24.0 | 0.5 | 30 | 2.5 | 3.5 | 1.2 | 13600 | 11300 | 300/250 | 650/540 | 65/54 | 430 | 480 |
| GL32h | 32 | 25.6 | 0.5 | 32 | 2.5 | 3.5 | 1.2 | 14200 | 11800 | 300/250 | 650/540 | 65/54 | 440 | 490 |

Corrected against Wendehorst Tab. 12.3/12.4 (DIN EN 14080:2013-09), two fixes:
1) "c" tension values f_t,0,k are **17.0/19.5/19.5/19.5**, not the 0.6·f_m,k
approximation previously shown — GL28c/30c/32c share the same 19.5 ceiling
(the formula understated all three). 2) The "h" table previously had a
**row/class mislabelling**: what was printed as "GL32h" actually carried
GL30h's values, and what was printed as "GL36h" (not a class in this DIN EN
14080 table at all) actually carried the real GL32h values — both now fixed;
**GL36h is not in this source table** and should be re-sourced (Studiengem.
Holzleimbau extended range) before use, not assumed as a linear extrapolation.
The "h" tension values (higher, edge lamellae of tension grade) vs "c"
(lower) is the real design difference — homogeneous lay-up buys the higher
tension strength and is the bending-member default; combined for
columns/frames. **E_90 and G/G_r are constant across every GL grade** (both
c and h) — E_90,mean/05 = 300/250 N/mm², G_mean/G_05 = 650/540 N/mm²,
**rolling-shear modulus G_r,mean/G_r,05 = 65/54 N/mm²** (≈1/10 of in-plane G
— this is the property that governs CLT out-of-plane shear stiffness/failure
in a plate FEM model, not the normal shear modulus; missing it silently
over-stiffens a CLT plate/shell element in the through-thickness direction).
Rolling-shear strength f_r,k = 1.2 for all grades shown (softwood solid
timber §3.1: f_r,k = 0.8 — lower than glulam).

**BSH trade rules:** ≥ 3 (typ. 5+) lamellae of 14-45 mm, tension-zone lamellae
of higher grade; finger joints (Keilzinken) factory only; flat-use (querused)
bending with NA uplift ≥ 4 lamellae — VERIFY; wide sections (lamella width
≤ ~28 cm practice) need tilt restraint at supports (forked foot, steel shoe).

### 3.4 Design value and modification factors

```
X_d = X_k · k_mod / γ_M          (ULS)
k_h (size) — two DIFFERENT formulas, do not conflate them (Neuhaus,
  Ingenieurholzbau, 4th ed. 2017, p.313/316-317, EN 1995-1-1 §3.2/§3.3):
  solid timber (softwood AND hardwood alike), ρ_k ≤ 700: k_h = min[(150/h)^0.2 ; 1.3],
    h/b in mm, applied to bending (h < 150 mm) and tension (max(h,b) < 150 mm)
  glulam (both combined "c" and homogeneous "h" grades): k_h = min[(600/h)^0.1 ; 1.1],
    applied to bending (h < 600 mm, flat/Flachkant loading only) and tension (b < 600 mm)
  (worked example "C24 14/14 → k_h = 1.014" uses the SOLID-timber formula:
   (150/140)^0.2 = 1.014 — resolves the earlier ambiguity, not a separate
   "hardwood variant")
k_ℓ: homogeneous glulam ONLY (GL·h, not "c" grades), Hochkant/edge-loaded
  bending, ≥ 4 lamellae side-by-side → +20 % on f_m,k (k_ℓ = 1.2)
```

**k_mod — load duration × service/use class (NKL / Nutzungsklasse, EN 1995-1-1
Table 3.1; CL1/CL2/CL3 = equilibrium moisture ≤ 12 % / ≤ 20 % / > 20 %):**

| Duration (example actions) | CL1 | CL2 | CL3 |
|---|---|---|---|
| permanent (self weight) | 0.60 | 0.60 | 0.50 |
| long (6 mo-10 a) | 0.70 | 0.70 | 0.55 |
| medium (1 wk-6 mo; storage E) | 0.80 | 0.80 | 0.65 |
| short (< 1 wk; snow, live A/B) | 0.90 | 0.90 | 0.70 |
| very short (< 1 min; wind, impact) | 1.10 | 1.10 | 0.90 |

**CONFIRMED against Wendehorst Tab. 12.5** (DIN EN 1995-1-1:2010-12 Tab. 3.1 +
NA Tab. NA.4) for solid timber, glulam, LVL/3 and CLT-equivalent panels — CL1
and CL2 columns are **identical** for these products (only CL3 drops); the
previous CL2 column here understated capacity at every duration tier. Panel
products take their own lower columns: LVL/1 and Sperrholz EN 636-1 (dry use
only) 0.60/0.70/0.80/0.90/1.10 (CL1 only, CL2/3 = "–" not permitted); OSB/2
(dry) 0.30/0.45/0.65/0.85/1.10 (CL1 only); OSB/3-4 and Sperrholz EN 636-2/3,
LVL/2 (dry+humid) same run as solid timber's CL1/CL2 columns, CL3 not
permitted. German NA wind: k_mod = mean(short, very short) = **1.00** (CL1/2
solid/BSH), **0.80** (CL3).

**k_def — creep (final deformation, EN 1995-1-1 Table 3.2 + NA Table NA.5),
CORRECTED and complete (Neuhaus, Ingenieurholzbau, 4th ed. 2017, p.334-335,
Tab. 7.17):**

| Product | CL1 | CL2 | CL3 |
|---|---|---|---|
| Solid timber, glulam (BSH), LVL | 0.60 | 0.80 | **2.00** |
| Balkenschichtholz (duo/trio), CLT (Brettsperrholz), Massivholzplatten, finger-jointed solid | 0.60 | 0.80 | **not permitted** |
| Plywood, "Trocken"/dry (NKL1 only) | 0.80 | — | — |
| Plywood, "Feucht"/humid | 0.80 | 1.00 | — |
| Plywood, "Außen"/exterior (all 3 NKL) | 0.80 | 1.00 | **2.50** |
| OSB/2 (NKL1 only) | 2.25 | — | — |
| OSB/3-4 | 1.50 | 2.25 | not permitted |
| Particleboard P4 (NKL1 only) | 2.25 | — | — |
| Particleboard P5 | 2.25 | 3.00 | not permitted |
| Particleboard P6 (NKL1 only) | 1.50 | — | — |
| Particleboard P7 | 1.50 | 2.25 | not permitted |
| Cement-bonded particleboard | 2.25 | 3.00 | not permitted |
| Fibreboard, medium-hard MBH.LA2 (NKL1 only) | 3.00 | — | — |
| Fibreboard, hard HB.HLA2 | 2.25 | 3.00 | not permitted |
| Gypsum board GKB/GKF (NKL1 only) | 3.00 | — | — |
| Gypsum board GKBI/GKFI, gypsum-fibreboard | 3.00 | 4.00 | not permitted |

**Correction to the earlier digest:** Balkenschichtholz/CLT/Massivholzplatten/
finger-jointed solid are a **separate row from solid timber/glulam** — they
share the same CL1/CL2 values but are **not permitted in NKL3 at all** (the
earlier digest lumped them into the same row as solid/glulam with kdef = 2.0
in CL3). Plywood's "Außen" (exterior) kdef,CL3 is **2.50**, not 2.0.

### 3.5 Physical behaviour relevant to detailing

- **Shrink/swell across grain ≈ 10× along grain:** Δu of 1 % → Δd/d = **0.25 %
  (softwood) / 0.35 % (hardwood)**, both directions. Worked: C24 18/20 drying
  20→10 % MC → Δh = 5 mm. Above fibre saturation (~30 %) no further shrinkage.
  Consequences: slotted/oversize holes, no cumulative cross-grain shrinkage in
  a gravity path, never fast green timber tight, cladding gaps sized for the
  MC swing.
- **Moisture at installation:** framing ≤ 20 % (KD typical 12-15 %); interior
  joinery ≈ 6-8 %; heated-room equilibrium can drop to ~7 % — fast drying =
  more warp (Verwerfen, Schüsseln, end-checks).
- **Density → self weight (kN/m³):** C14 3.5 · C16 3.7 · C18 3.8 · C22 4.1 ·
  C24 4.2 · C27 4.5 · C30 4.6 · C35 4.8 · C40 5.0; D30 6.4 · D35 6.7 · D40 7.0 ·
  D50 7.8 · D60 8.4 · D70 10.8; BSH GL24h-GL36h 3.7-4.4; plywood (soft/birch)
  5.0/7.0; laminate/Tischlerplatte 4.5; particleboard 7.0-8.0; MDF 8.0;
  cement-bonded 12.0; lightweight fibreboard 4.0.
- **E-modulus orientation:** E ∥ ≈ 11000 (softwood) / 12000 (oak/beech) MPa
  mean-ish, E ⊥ ≈ 370 / 800 MPa — a factor ~30. Thermal: α ∥ 2.5-5·10⁻⁶/K,
  ⊥ 25-60·10⁻⁶/K (steel 12·10⁻⁶, concrete 10·10⁻⁶).

### 3.6 Sizes and tolerances (EN 336 / EN 14080)

- Nominal solid-timber sizes are quoted at **12 % reference moisture** (15 %
  for hardwood); planing stock adds the MTK1/MTK2 machining allowance (table
  cells lost in digest — VERIFY EN 336). BSH deviations (EN 14080, digest
  readable subset): width ± 2 mm; bow 4 mm per 2000 mm; set/twist and length
  bands garbled — VERIFY; curved elements: set per m by lamella count.
- Visual grading limits (DIN 4074-1) are t-/d-relative percentages of knots,
  slope of grain, warp, shakes — **not machine-readable in the digest; read
  the standard.** Reject on site: large knots in the tension face at
  mid-span, wane at bearings, shakes, insect attack, staining.

### 3.7 Engineered products used in buildings

| Product | Standard | Behaviour / use rule |
|---|---|---|
| BSH / glulam | EN 1194/14080 | beams, frames, columns; **no code limit on section size** — width in practice to b ≈ 24 cm routine (≤ 2 boards side-by-side per lamella), b ≈ 30 cm as practical max; depth h ≈ 200 cm routine, h_max ≈ 250 cm (limited by planer working width, not strength — beyond ~2.5 m a trussed member usually beats a solid web economically); length effectively unlimited via finger-jointing, practically capped by **transport (~35-40 m standard, ~50-60 m special transport, field-spliced >100 m executed on site)**, not the earlier "~1.2 m / 18-20 m" ceiling (Neuhaus, Ingenieurholzbau, 4th ed. 2017, p.109-110); design values §3.3 |
| CLT / Brettsperrholz | EN 16351 | odd layers ≥ 3, outer same grain → defined span dir.; walls ~50 % section along grain; floor t ≈ 140-260 mm for 3-6 m; excellent diaphragm; element fabrication with TBE/CAD-CAM cut-outs |
| LVL | EN 14374 | strongly anisotropic one-way; rib/edge members; k_mod/kdef slightly below solid (LVL-1/2/3 categories) |
| Balkenschichtholz (duo/trio, parallel laminations) | EN 14080 | beams/sills; total cross-section ≤ 280 mm; 2-5 parallel-grain laminations of the **same** strength class, each lamination > 45 mm to ≤ 85 mm thick (Neuhaus p.308, Tab. 7.1); settlement like solid; **NKL3 not permitted at all** (§3.4 kdef table) — do not specify duo/trio beams in permanently-wet exposure |
| Finger-jointed solid (Keilgezinkt) | EN 15497 | continuous sections, columns; joints ≤ 15 % of section length? (VERIFY) |
| I-joists / wood-based composite beams (mechanically-jointed built-up sections) | ETA / EN 1995-1-1 Annex B | web = board/steel, flange = LVL — bearing stiffeners at supports mandatory (web crippling); **effective stiffness by the γ-("gamma") method**: (EI)_ef = Σ(E_i·I_i + γ_i·E_i·A_i·a_i²), with γ_i = 1/(1+π²·E_i·A_i·s_i/(K_i·l²)) for the mechanically-jointed outer (flange) members and γ=1 for a rigidly-glued middle member; per-fastener design force F_i,d = (V_max,d/(EI)_ef)·(γ_i·E_i·A_i·a_i·s_i); web-buckling limit h_w + 0.5·(h_f,c+h_f,t) ≤ 70·b_w (Neuhaus, Ingenieurholzbau, p.786-789, Tab. 22.5/22.6) — engineered I-joists/box beams are normally bought to a manufacturer ETA rather than hand-designed, but this is the underlying method if a bespoke nailed/screwed built-up section is being modelled |
| Wood-fibre / particle / OSB / plywood boards as structure | EN 13169?/EN 300/EN 636 | shear diaphragms and diaphragm floors; nailing edge distance rules of §5.8; k_mod/kdef of board type |
| Nail plates (Nagelplatten), punched-plate connectors | EN 912 + abZ/ETA | truss plates factory only; plate γM 1.25; approved type tables (e.g. 120/10 → 12.5 kN up to 240/22 → 31.8 kN characteristic, with group-reduction by screwed-in pairs; "predominantly static only, wood moisture limit") — **approval validity expired in the digest source — re-check current ETA/abZ** |

**Glued connections (Geklebte Holzverbindungen, EN 1995-1-1 §10, Neuhaus p.301-305)
— when member continuity is glued rather than mechanically jointed:**
- **Schäftung (scarf joint):** glue-face slope ≤ 1/10 (α ≤ 5.7°); thin
  members/veneers only; MC ≤ 15 % at gluing (Δu ≤ 4 % between the two parts);
  **NKL1+2 only**.
- **Keilzinkung (finger joint), two forms:** ordinary lamella joints (finger
  length ℓ_j ≥ 10 mm, typ. 15/20/30 mm, flank angle α ≤ 7.1°, strength
  reduction factor ν ≤ 0.18 → effective section A_ef = (1−ν)·A) used inside
  glulam/Balkenschichtholz/finger-jointed-solid laminations — **glulam with
  ordinary lamella finger joints may be used in all 3 NKL**; and "Universal"
  full-cross-section splices (ℓ_j ≥ 45 mm) used at frame corners (below) and
  full-depth member splices — **Balkenschichtholz and full-section Universal
  finger joints are NKL1+2 only**. Never place a full-section finger splice,
  or a Balkenschichtholz member of any kind, in continuously-wet (NKL3)
  exposure.

**Frame corners (Rahmenecken) — moment-resisting corner joints, currently the
biggest geometric gap for portal-frame/haunch FreeCAD detailing (Neuhaus
p.663-671, Tab. 17.14-17.16):**
- **Dowelled (verdübelte) corners:** per-dowel force from the corner moment
  F_M,Ed = M_d·r/(n·r²) on a single dowel circle, or M_d·r_1/(n_1·r_1²+n_2·r_2²)
  on a double circle, vector-superposed with the axial/shear share and checked
  against F_v,Rd (§5.1-5.3); **a double dowel-circle loses 15 % per-dowel
  capacity (n_ef factor 0.85) unless a splitting reinforcement (Ecksicherung)
  is added**, in which case n_ef = 1.0 — size the reinforcement for a tie force
  equal to the outer circle's 30°-sector shear share. Corner-specific min.
  spacings (no equivalent in the general §5.2 table): within-circle ≥ 6d,
  between circles ≥ 5d, to end grain ≥ 7d (≥ 80 mm), to loaded/unloaded edge
  ≥ 3d. **Avoid positive corner moments** (high transverse tension); brace the
  inner corner against the compression-zone LTB failure mode (Kopfband).
- **Finger-jointed (keilgezinkte) corners:** interaction check
  f_c,0,d/f_c,α,d·(σ_c,0,d/(k_c·f_c,0,d) + σ_m,d/f_m,d) ≤ 1 for a **negative**
  corner moment, but ≤ **0.2 only** for a positive moment (transverse tension
  at the joint is the governing risk); f_c,α,d taken from the angle-dependent
  Versatz compression table (§5.10) using the glulam grade values; net section
  at the joint = **80 %** of gross (20 % finger-joint reduction); **GL28 and
  higher: ft,0,d/fc,0,d/fm,d further reduced 15 %** (knot risk near the joint);
  **NKL1+2 only**, no exterior exposure. Joint angle α = β/2 (single zinking)
  or β/4 (double zinking), β = 90°−γ (γ = frame corner opening angle).

---

## Section 4: Timber member design (verification chains)

All checks in the form σ/τ ≤ f_d (utilization = action-effect / resistance ≤ 1.0).
Design values: f_d = k_mod·f_k/γ_M (γ_M = 1.3). Cross-section gross/net per
EN 1995-1-1 §5.2 (weakenings: deduct notches/screw groups in tension; compression
with small eccentricity may ignore local weakening outside the middle third).

### 4.1 Tension parallel to grain (Zug)

```
σ_t,0,d = F_t,d / A_net ≤ f_t,0,d          (A_net = (b−weakening)·h)
size increase k_h — see §3.4 for the correct, product-split formula: solid
  timber k_h = min[(150/h)^0.2; 1.3] (worked C24 14/14 → 1.014); glulam
  k_h = min[(600/h)^0.1; 1.1]
connection: σ on net section through the fastener line; net-section deduction
  by fastener type (Neuhaus, Ingenieurholzbau, 4th ed. 2017, p.557, Tab. 15.1):
  nails ΔA ≈ 0.10·A; bolts/dowels/fit bolts ΔA ≈ 0.15·A; ring/shear-plate
  connectors ΔA ≈ 0.25·A; single traditional scarf (Versatz, §5.10) ΔA ≈ 0.25·A.
  Staggered-hole 50 %-of-spacing rule not confirmed against this source —
  VERIFY EN 1995-1-1 §5.1.3 directly.
```
Worked (C24 14/14, F_t,g=50 + F_t,s=50 kN): F_d = 1.35·50+1.5·50 = 142.5 kN
(governs: compare F_d/k_mod: 142.5/0.9 = 158 vs snow-only
67.5/0.6 = 112); A_net = 157.6 cm² (bolt holes); f_t,0,d = 1.47·0.9/1.3 ≈ 1.02
→ utilization 0.89 ✓.

### 4.2 Compression parallel + buckling (Druck, Ersatzstab)

```
λ = L_cr / i      (rectangle: i = 0.289·h about the axis; weak axis governs)
λ_rel = (λ/π)·√(f_c,0,k / E_0,05)
k_c = 1 / (k + √(k² − λ_rel²)),  k = 0.5·[1 + β_c·(λ_rel − 0.3) + λ_rel²]
    β_c = 0.2 (solid timber) ; 0.1 (glulam, LVL)   [CORRECTED — product-
    dependent imperfection factor, not the earlier fixed "0.1·λ+0.3·λ²" form;
    Neuhaus, Ingenieurholzbau, 4th ed. 2017, p.583-584, Tab. 16.6]
σ_c,0,d ≤ k_c · f_c,0,d
```
**Effective (buckling) length l_ef — reference table** (Neuhaus p.588-593,
Tab. 16.10, digesting NCI NA.13.2 Tab. NA.24): Euler cases as usual —
fixed-free β=2, pinned-pinned (Pendelstütze) β=1, fixed-pinned β=0.707,
fixed-fixed β=0.5, l_ef=β·L. Truss members: chords take the system-line
(node-to-node) length unless a refined buckling check is done; web/diagonal
members take the system-line length out-of-plane, a pin-dependent length
in-plane. 2-/3-hinge arches/frames and elastic-spring-base columns have their
own β_R/β_S expressions (function of E·I, N, spring stiffness K_φ) — read the
table directly for these, not worth digesting a formula here. A frame corner
modelled as an elastic (not rigid) spring adds a moment M = N·h/6·(1/k_c − 1)
at the column head — include this if the corner stiffness (§3.7 Rahmenecken)
is less than fully rigid.
Worked (GL28c 16/32, L = 5 m pinned, F_d = 180 kN permanent → k_mod 0.6,
f_c,0,d = 0.6·2.4/1.3 = 1.11 kN/cm²): y-axis λ = 500/(0.289·32) = 54 → λ_rel
0.826 → k_c 0.883 → util 0.36; z-axis λ = 108 → λ_rel 1.65 → k_c 0.341 →
**util 0.93 governs** ✓. Rules: weak axis controls; section check only for
weakenings in the compressed zone outside the middle third (then net area +
second-order from eccentricity). Intermediate restraint between parallel beams
(purlins/bracing) shortens L_cr about the weak axis — show restraint points on
the model.

### 4.3 Bending + lateral torsional buckling (Biegung, Kippen)

```
σ_m,d = M_d / W_y ≤ k_crit · f_m,d
effective laterally unrestrained length l_ef (fork supports, top-flange load):
  exact (NA effective-length formula):  l_ef = a·√( a1·(1 + a2·(a_z/a)·√(B/T)) )
     B = E_d·b³h/12 ; T ≈ G_d·b³h/3 (G_mean/γ_M ≈ 50 kN/cm²); a_z = load
     height above shear centre (top edge a_z = +h/2, centre 0, bottom −h/2)
     a1, a2 from support/loading table (UDL fork: 1.13 / 1.44)
  simplified: l_ef = 0.9·L + 2·h (use the smaller)
i_m = √(I_z·I_tor)/W_y   (I_tor = a1'·b³h, a1' from h/b table; rectangular
   sections: i_m simplifies to b²/h)
λ_rel,m = (l_ef/(π·i_m))·√(f_m,k/E_0,05)   — **glulam only: multiply the
   product E_0,05·G_05 by 1.4 before taking the root** (NCI zu 6.3.3(2) Anm.1,
   Neuhaus, Ingenieurholzbau, 4th ed. 2017, p.630); this lowers λ_rel,m
   (raises k_crit) materially for BSH beams — omitting it under-predicts LTB
   capacity of every glulam beam check.
k_crit = 1.0 (λ_rel,m ≤ 0.75) ; 1.56 − 0.75·λ_rel,m (0.75 < λ_rel,m ≤ 1.4) ;
         1/λ_rel,m²  (λ_rel,m > 1.4)
   [CORRECTED thresholds and 3rd-branch form — was 0.2/1.1/"1.11/λ_rel²?";
   confirmed against the book's own numeric verification table, Neuhaus
   p.630-632, Tab. 17.3/17.4]
```
**l_ef (Kipplänge) exact NA formula — extraction of this specific equation
was unreliable (repeated √-symbol loss in both this digest and the new
source); do not trust either version blindly, re-derive from EN 1995-1-1/NA
NCI NA.13.3 Table NA.25 directly before a governing LTB check.** The a1/a2
coefficient table, however, is independently confirmed (Neuhaus p.640-641,
Tab. 17.9/17.10) and safe to use as printed: fork-supported single span,
UDL → a1/a2 = **1.13/1.44** (matches the worked example below); constant
moment → 1.77/0; point load at midspan → 1.35/1.74; cantilever UDL →
1.27/1.03, tip load → 2.05/1.50; fixed-fixed → 6.81/0.40 or 5.12/0.40;
continuous-beam midspan → 1.70/1.60 or 1.30/1.60.
Worked (GL28c 16/90, L = 15 m, q_d = 12.4 kN/m, restraint at ends + mid-thirds,
a = 5 m, top-edge load): W = 21 600 cm³, M = 348.8 kNm → σ = 1.61 kN/cm²;
f_m,d = 0.9·2.8/1.3 = 1.94; single bending util 0.83 ✓. LTB: l_ef = 618 cm
(exact) < 630 (simple) → use 618; i_m = 2.68 cm; λ_rel,m = 0.856 → k_crit
0.918 → util **0.91 governs** → the beam is kip- (LTB-) critical, not
strength-critical: **add restraint or increase b**. Bearing pressure at the
20 cm support with k_c,90 = 1.75 (glulam, single support) and A_c,ef =
(3+20+3)·16 = 416 cm² → util 0.74 ✓.

**Bracing/fly-brace forces for the restrained compression edge** (EC5-specific
refinement of the generic "1-2 % bracing force" rule of thumb — Neuhaus,
Ingenieurholzbau, 4th ed. 2017, p.870-873, Tab. 26.4/26.5): individual
restraint (fly-brace) design force F_d = N_d/50 (solid timber, Balkenschichtholz)
or N_d/80 (glulam, LVL), where N_d = (1−k_crit)·M_d/h is the destabilising
force at the restraint; distributed bracing-system load q_d = k_ℓ·n·N_d/(30·l),
k_ℓ = min(1, √(15/l)) (l in m); permissible in-plane deflection of the bracing
system u ≤ l/500; minimum restraint spring stiffness C = 4·N_d/a (a = restraint
spacing). Use this instead of the generic 1-2 % figure whenever the member and
its k_crit are already known from the LTB check above.

### 4.4 Shear (Schub) with cracked section

```
τ_d = V_d·S/(I·b) ≤ f_v,d;  rectangle τ = 1.5·V/(b_eff·h)
cracking at interior supports/continuous beams: b_eff = k_cr·b
Take V at h from support face where bearing is direct.
```
**k_cr by product (CORRECTED/complete — NDP zu 6.1.7(2), Neuhaus,
Ingenieurholzbau, 4th ed. 2017, p.685, Tab. 18.1):**

| Product | k_cr |
|---|---|
| Solid softwood (Nadelvollholz) | **2.0/f_v,k** |
| Balkenschichtholz aus Nadelholz (duo/trio) | **2.0/f_v,k** (paired with solid softwood, NOT glulam) |
| Glulam (Brettschichtholz) | **2.5/f_v,k** (worked below: 2.5/3.5 = 0.714) |
| CLT (Brettsperrholz) | **1.0** |
| Solid hardwood (Laubvollholz) | **0.67** (fixed value, not a formula) |
| Other wood-based products (LVL etc., EN 13986/14374) | **1.0** |

Solid-**softwood-only** bonus: k_cr may be increased **30 %** in zones ≥ 1.5 m
from the end grain (shrinkage cracks concentrate near member ends) — **not
permitted for glulam**; can meaningfully relax an over-conservative shear
check away from bearing zones in solid joists/rafters.
Worked (same GL28c beam): k_cr = 2.5/f_v,k = 0.714 → b_eff = 11.4 cm;
f_v,d = 0.9·0.35/1.3 = 0.242 kN/cm²; τ = 1.5·93/(11.4·90) = 0.136 → util 0.56 ✓
(0.49 with V reduced at h from face).

### 4.5 Bearing perpendicular to grain (Flächenpressung ⊥ Faser)

```
σ_c,90,d = F_c,90,d / A_c,ef ≤ k_c,90 · f_c,90,d
```
**k_c,90 (CONFIRMED against Wendehorst Tab. — DIN EN 1995-1-1/NA 6.1.5), by
support condition and product** — default is **1.0** for any l_1 < 2h:

| Product | l_1 < 2h (default) | l_1 ≥ 2h, continuous support (Schwellendruck) | l_1 ≥ 2h, single/discrete support (Auflagerdruck) |
|---|---|---|---|
| Hardwood solid (Laubvollholz) | 1.0 | 1.0 (no elevated value) | 1.0 |
| Softwood solid (Nadelvollholz) | 1.0 | 1.25 | 1.5 |
| Glulam, softwood (BSH aus Nadelholz) | 1.0 | 1.5 | **1.75** (also applies for bearing length > 400 mm) |
| Truss node, indirect connection | — | — | 1.5 (NA 6.1.5, all products) |

(Corrects the earlier flagged guess: hardwood does **not** get an elevated
k_c,90 — it stays at 1.0. The worked example's 1.25 solid-continuous /
1.75 glulam-single values were both right.)
```
A_c,ef = (3 + l_bearing + 3)·b   [cm]  load spreading 3 cm each side along grain
edge distance a > 3 cm each side required for spreading; otherwise A = b·l
```
Worked (post C24 8/12 on sill, F_d = 20.25 kN permanent, k_mod 0.6): f_c,90,d =
0.6·0.25/1.3 = 0.115 kN/cm²; A_ef = (3+12+3)·8 = 144 cm²; 20.25/144 = 0.141 ≤
1.25·0.115 = 0.144 → util 0.98 ✓ (tight — this is the classic hidden failure;
widen the bearing plate).

### 4.6 Biaxial bending

```
σ_my/f_my,d + k_m·σ_mz/f_mz,d ≤ 1.0   with k_m = 0.7 (one-axis plast.
redistribution possible) or 1.0 (conservative alternative, symmetric)
work: purlin GL24h 18/36: k_m = 0.7 → util 0.84 + 0.7·0.16 = 0.95 ✓;
k_h (bending about y, h < 60? → (60/36)^0.1 = 1.052) and k_ℓ = 1.2 (flat/edge
use ≥ 4 lamellae) applied to the respective f_m,d.
```

### 4.7 Combined axial + bending (simplified NA "Ersatzstab" chain)

```
(σ_c/σ_c,crit,y)² + σ_my/(f_m,y,d·(1−σ_c/σ_crit,y))
                 + (σ_mz/(f_m,z,d·(1−σ_c/σ_crit,z)))² ≤ 1
(EN 1995-1-1 6.2.1 + 6.3; tension + bending drops the first term; use the full
NA formulas or software for anything close to 1.0 — VERIFY form per edition.)
```

### 4.8 Serviceability — deflection (Biegung GZG)

```
w_final = w_g,perm·(1 + k_def) + w_g,qp? + Σ w_q,i·(1 + ψ_2,i·k_def)
net (against camber w_c): w_net = w_final − w_c
worked GL28c L=15 m, k_def 0.6 (CL1), ψ2 snow = 0:
  w_inst,g = 2.71 cm ≤; w_inst = 4.74 ≤ l/200 = 7.5 (0.63)
  w_fin = 4.34 + 2.03 = 6.37 ≤ l/150 = 10 (0.64)
  w_net,fin = 4.34 − 4.0 = 0.34 ≤ l/250? = 6.0 (0.06) ✓
deflection limits (CORRECTED — NDP zu 7.2(2), Neuhaus, Ingenieurholzbau, 4th
ed. 2017, p.848, Tab. 25.4; classified by member importance/camber status,
**not** by "brittle finishes present" — that split is an old DIN 1052-era
concept, not what the current NA table actually uses):
  general members: w_inst ≤ l/300, w_net,fin ≤ l/300, w_fin ≤ l/200
    (cantilever: l_k/150, l_k/150, l_k/100)
  cambered/secondary members (überhöhte Bauteile; agricultural buildings;
  Sparren/Pfetten rafters+purlins): w_inst ≤ l/200, w_net,fin ≤ l/250,
    w_fin ≤ l/150 (cantilever: l_k/100, l_k/125, l_k/75)
```
**Vibration (floors, EN 1995-1-1/NA §7.3.3) — three-part check, f1 > 8 Hz
floors (replaces the earlier a(n)-curve digest, which reflected a different/
older method; Neuhaus, Ingenieurholzbau, 4th ed. 2017, p.854-858):**
1. **Stiffness:** w/F ≤ a [mm/kN] under a 1 kN point load; recommended
   0.5 ≤ a ≤ 1.5, a = 1.0 as default.
2. **Frequency:** f1 = k_f·(π/2l²)·√((EI)_ℓ/m) > 8 Hz (k_f from a continuity
   table, = 1.0 for a single span).
3. **Velocity response:** v ≤ b·(f1·ζ)⁻¹, with a tabulated a↔b linkage
   (anchor points: a=0.5→b=150 … a=1.5→b=100 … a=4.0→b=50, interpolate for
   intermediate a; ζ = 1 % default damping — read the NA table for the exact
   curve, these are anchor points not a formula).
Long-span timber floors almost always need closer joists, a deeper section,
or a structural topping to pass check 3.

### 4.9 Notched ends and perpendicular tension (Ausklinkung)

```
notched shear (support/loaded side, sloped notch): τ_d ≤ k_v·f_v,d with
  k_v = min{1 ; k_n·(1+1.1·i^1.5/√h) / [√h·(√(α(1−α)) + 0.8·(x/h)·√(1/α−α²))]}
  (square notch: drop the i-term); k_n = 5.0 (solid timber) / 6.5 (glulam) /
  4.5 (LVL/Furnierschichtholz); α = h_ef/h; x = distance from support reaction
  line to the notch corner; i = notch-slope ratio (0 for square notch)
  [Neuhaus, Ingenieurholzbau, 4th ed. 2017, p.743, Tab. 21.1 — kn values and
  formula structure confirmed, incl. the previously-missing LVL value 4.5]
top-side (unloaded-edge) notch: k_v = 1 by default; if the load point falls
  within h_ef of the notch, k_v = (h/h_ef)·[1 − (h−h_ef)·x/(h·h_ef)] instead
transverse tension force (CORRECTED — was structurally wrong):
  F_t,90,d = 1.3·V_d·[3(1−α)² − 2(1−α)³]      [Neuhaus p.746, Tab. 21.2]
practice: unreinforced notches NKL1-2 only; NKL3 always requires
  reinforcement
```
Worked (GL28h 14/110, h_ef = 90, V_d = 120 kN): un-notched util 0.88 ✓; notched
k_v = 0.358 → util **2.6 → fails → reinforcement required**; F_t,90 = 13.6 kN →
glued-in M10 4.8 bars (2 near faces, l_ad = 200 mm, bond line f_g,k = 4.0 N/mm²,
F_t,Rd = 0.9·A_s·f_u,k/1.25 = 16.7 kN/bar → 2 bars util 0.41 ✓) or full-threaded
screws Ø8×600 (pull-out 19.6 kN? govern shank tension 17.0 kN, n_eff = 1.87 →
util 0.69 ✓); with reinforcement k_v → 1.0 → util 0.93 ✓. Detailing rule:
≥ 2 reinforcement elements near the edges; bar diameter ≤ 20 mm; effective bond
length ≤ 8·d? (worked used 200 mm) — VERIFY ETA values.

> **Notching design principles (traditional Zimmerer rules + EN 1995-1-1 6.1.5):**
> every notch creates (a) a shear bottleneck, (b) a splitting risk (σ ⊥ grain),
> (c) a lever for horizontal tie. Keep notches shallow and far from mid-span;
> avoid re-entrant corners (drill relief holes); rule of thumb h_ef/h ≥ 0.6 for
> un-reinforced — VERIFY per case.

### 4.10 Holes through beams (Durchbrüche) — glulam/LVL only

Genuinely new geometric ruleset (Neuhaus, Ingenieurholzbau, 4th ed. 2017,
p.751-753, Tab. 21.3, digesting NCI NA.6.7) — the correct reference for
sizing/placing a service duct penetration through a glulam or LVL roof
binder/floor beam. Applies only to **rectangular glulam or LVL beams**, hole
clear dimension **d > 50 mm** (smaller holes are ordinary local weakening
per §8.3.3, ignore this ruleset).

**Geometric limits:** end-distance from support l_v ≥ h; hole-to-hole spacing
l_z ≥ 1.5h and ≥ 300 mm; hole-to-point-load distance l_A ≥ h/2; edge margin
top/bottom h_ro, h_ru ≥ 0.35h each (i.e. hole confined to the central 30 % of
the depth); rectangular-hole length a ≤ 0.4h; hole height h_d ≤ 0.15h.

**Transverse tension check** (the hole splits the beam locally, same failure
mode as a notch): F_t,90,d = F_t,V,d + F_t,M,d, with F_t,V,d = (V_d·h_d/4h)·
(3−h_d²/h²) (use 0.7·h_d in place of h_d for round holes) and F_t,M,d =
0.008·M_d/h_r; check against 0.5·l_t,90·b·k_t,90·f_t,90,d.

**NKL1-2 unreinforced only; NKL3 always needs reinforcement** (same logic as
notches, §4.9). Directly usable in a FreeCAD/BIM model to validate where an
MEP duct or cable route is allowed to cross a glulam member without a
strengthening detail.

---

## Section 5: Timber connections (Verbindungen)

### 5.1 The yield model (Eurocode 5, "Y-Modell") for dowel-type fasteners

Every nail/screw/dowel/bolt is a beam in two embedments; characteristic
single-shear capacity (simplified, α = 0):

```
f_h,k = 0.082·(1 − 0.01·d)·ρ_k      [N/mm²] (ρ in kg/m³, d in mm)
f_h,α,k = f_h,0,k / (k_90·sin²α + cos²α);  k_90: softwood 1.35 + 0.015d,
   hardwood 0.90 + 0.015d, LVL 1.30 + 0.015d
M_y,Rk = 0.3·f_u,k·d^2.6  — CORRECTED: applies uniformly to dowels, bolts
   AND nails (round-shank nails factor 0.3, profiled/square-ish-shank nails
   factor 0.45). The elastic-section-modulus form "f_u,k·d³/6" does not
   appear in EC5's simplified method at all — it is DIN 1052 (superseded)
   leaking into the earlier digest. [Neuhaus, Ingenieurholzbau, 4th ed. 2017,
   p.413, Tab. 11.3]
f_u,k (N/mm²): dowel S235/S275/S355 → 360/410/470 (p.413); bolt/threaded-rod
   property class 4.6/4.8/5.6/5.8/8.8 → 400/400/500/500/800 (p.425, Tab. 11.9);
   nail/wire ≥ 600
γ_M = 1.1 for bending-stressed dowel-type fasteners — derived as the
   "worst-case envelope" combining γ_M,Steel=1.1 and γ_M,Holz=1.3 through the
   k_mod reconciliation (p.407, Gl. 11.19/11.20); this is the basis for the
   γ_M used throughout §5.1-5.6, but does NOT apply to ring/shear-plate
   connectors (§5.7 uses γ_M=1.3 — different failure mode, wood embedment
   governs there, not steel bending).
F_v,Rk = √(2β/(1+β))·d·√(2·M_y,Rk·f_h,1,k)  single shear; β = f_h,1/f_h,2
   for dissimilar members; double shear: middle-member factor on F_v,Rk
embedment: side  t_1,req = 1.15·√((2β/(1+β))·M_y,Rk/f_h,1,k) + d/2
            middle t_2,req = 1.15·√(M_y,Rk/(4·f_h,1,k)) + d/2
   (worked: Ø12 S235 dowel in C24 → F_v,Rk 6.08 kN/shear plane; t_req 58 mm)
```

### 5.2 Minimum spacing and edge distances (dowels/bolts, EN 1995-1-1 T8.2/T8.4)

**CORRECTED — the a₁/a₂ rows have NO tension/compression split; only a₃/a₄
do** (Neuhaus, Ingenieurholzbau, 4th ed. 2017, p.416, Tab. 11.5, EC5 Tab. 8.5,
for Stabdübel/Passbolzen — d = fastener diameter, α = load-to-grain angle,
0-360° unless noted):

| Spacing | Formula |
|---|---|
| a₁ (parallel to grain, all α) | (3 + 2·\|cos α\|)·d |
| a₂ (perpendicular, all α) | 3·d (no angle dependence) |
| a₃,t (loaded end, −90°≤α≤90°) | max(7d; 80 mm) |
| a₃,c (unloaded end, 90–150° & 210–270°) | a₃,t·\|sin α\| |
| a₃,c (unloaded end, 150–210°) | max(3.5d; 40 mm) |
| a₄,t (loaded edge, 0–180°) | max[(2+2·sin α)d; 3d] |
| a₄,c (unloaded edge, 180–360°) | 3·d |

(worked Ø12 example: a₁ 60 → 71 provided; a₂ 36 → 50; a₃,t 84 → 99 ✓.)

**Bolts and threaded rods use a separate, larger table** (Neuhaus p.427,
Tab. 11.12, EC5 Tab. 8.4) — do not reuse the dowel table above for bolts:
a₁ = (4+\|cos α\|)d; a₂ = 4d; a₃,t = max(7d; 80 mm); a₃,c = (1+6·sin α)d
[90–150°] / 4d [150–210°] / (1+6·\|sin α\|)d [210–270°]; a₄,t = max[(2+2·sin α)d;
3d]; a₄,c = 3d.

### 5.3 Effective number of fasteners n_ef (group effect)

```
parallel to grain (α=0):  n_ef = min[ n ; n^0.9·⁴√(a₁/(13·d)) ]   — CORRECTED:
   fourth root, and n raised to the 0.9 power (not "0.9·n·√(...)"); worked
   check n=3, a₁=71, d=12 → n^0.9=2.688, (a₁/13d)^0.25=0.821 → n_ef=2.21 ✓
   matches the pre-existing worked number exactly [Neuhaus, Ingenieurholzbau,
   4th ed. 2017, p.415, Gl. 11.21a]
perpendicular (α=90°):    n_ef = n   — CORRECTED: full count, no reduction
   (no splitting risk perpendicular to grain), NOT "min(n; n^0.9)"
0° < α < 90°: linear interpolation between the α=0 value above and n_ef=n
   (the earlier "45° → 1.77" worked number could not be reconciled against
   any plausible input combination — treat as unresolved, don't reuse it)
nails: n_ef = n·k_ef, k_ef = 1.0 (a₁≥14d) / 0.85 (a₁=10d) / 0.7 (a₁=7d) /
   0.5 (a₁=4d, pre-drilled only) — CONFIRMS the tier grid exactly, now with
   the a₁-thresholds attached [Neuhaus p.438, Tab. 11.16]
ring/shear-plate connectors have their own n_eff rule — see §5.7a
F_v,Rd = k_mod·n_ef·F_v,Rk/γ_M   (simplified γ_M = 1.1 — see §5.1 basis)
```

### 5.4 Nails (Nägel, EN 14592 + EN 10230-1)

- Shank: ductile wire, f_u,k ≥ 600 N/mm². **Never design a nail for pull-out**
  as the primary load path (withdrawal is a real, code-checkable capacity in
  EC5, unlike screws it just shouldn't be *relied on* for a primary
  connection): **CORRECTED — the "N per mm penetration" framing was itself a
  misdigest; EC5's real method is density-quadratic, not a diameter lookup**
  (Neuhaus, Ingenieurholzbau, 4th ed. 2017, p.453-454, Tab. 11.23):
  smooth-shank f_ax,k = 20×10⁻⁶·ρ_k² [N/mm²]; head pull-through f_head,k =
  70×10⁻⁶·ρ_k²; profiled/special nails (3 load-bearing classes) f_ax,k =
  30/40/50×10⁻⁶·ρ_k²; **head pull-through classes A–F** (resolves the
  "classes A-F lost in extraction" flag): f_head,k = 60/80/100/120/140/160
  ×10⁻⁶·ρ_k² respectively. F_ax,Rk = min{f_ax,k·d·t_pen ; f_ax,k·d·t +
  f_head,k·d²_h} (smooth) or min{f_ax,k·d·t_pen ; f_head,k·d²_h} (profiled).
- Characteristic single-shear R_k: 320 N (18 mm) up to ~4120 N (long profile
  specials), un-predrilled vs predrilled sets differ — digest grid garbled,
  **read EN 14592/manufacturer tables.** Worked 3.4×90 (f_u,k 600, C24):
  F_v,Rk = 765 N/shear plane; group n_ef = 29.44/side → F_v,Rd (k_mod 0.6,
  γ_M 1.1) = 12.3 kN; util 0.95 ✓.
- **Penetration rule: t ≥ 9d** for full capacity (round nails; profiled nails
  6-8d); 4d < t < 9d → **F_v,Rk,red = F_v,Rk·t/(9d)** — CONFIRMED linear;
  t < 4d not permitted [Neuhaus p.~448].
- Pre-drill when t < max(7d; density term) — split-prone species (spruce):
  t < max(14d; (13d−30)·ρk/200) → drill; edge a₄ ≥ 10d (ρk ≤ 420) / 14d
  (420 < ρk ≤ 500); nail across grain into side faces, never into end grain;
  min member thickness 24 mm (worked). Spacing (un-pre-drilled, ρk ≤ 420,
  d < 5): a₁ = (5+5cosα)d; a₂ = 5d; a₃,t = (10+5cosα)d; a₄,t = (5+2sinα)d;
  a₄,c = 3d. Diagonal nailing carries NA reductions (−25 %? — VERIFY);
  nails from both sides in one plane need ≥ 4d overlap.

### 5.5 Structural screws (Holzschrauben) and glued-in rods

- **Withdrawal — CORRECTED formula (the earlier `k_1·d²·(ρ_k/350)^0.8` form
  does not appear in this book edition and is likely a fragment of a
  different/draft source):** (Neuhaus, Ingenieurholzbau, 4th ed. 2017,
  p.475-476, Tab. 11.28, EC5 §8.7.2, for 6≤d≤12mm, 0.6≤d₁/d≤0.75):
  `f_ax,k = 0.52·d^(−0.5)·l_ef^(−0.1)·ρ_k^0.8` [N/mm²]; `k_d = min(d/8, 1)`;
  `F_ax,α,Rk = (n_ef·f_ax,k·d·l_ef·k_d) / (1.2·cos²α + sin²α)`. Head
  pull-through: `F_ax,α,Rk = n_ef·f_head,k·d_h²·(ρ_k/ρ_a)^0.8`. **Steel
  tension** (governs when the head/withdrawal don't): `F_t,Rk = n_ef·f_tens,k`
  with `f_tens,k = 300·π·d₁²/4` [N] (d₁ = core/thread-root diameter) — a
  concrete formula replacing the earlier bare worked number. n_ef = n^0.9
  (confirmed). Spacing (Neuhaus p.477-478, Tab. 11.29): a₁ = 7d (row spacing
  along grain), a₂ = 5d, **a₁,CG = 10d** (end distance to thread centroid —
  corrects the earlier "a₃,c ≥ 5d", which used the wrong label and value),
  **a₂,CG = 4d** (edge distance, corrects "a₄,c ≥ 4d" label), t ≥ 12d. Screws
  take **withdrawal design forces**; nails do not. Torque window matters —
  over-torque crushes fibres.
- **Full-thread screws (Vollgewindeschrauben)** — book's own preface names
  this a major new-edition topic; **no generalized EC5/NA design table
  exists — capacity is entirely ETA/abZ-bound per product** (matches the
  existing framing below). Qualitative guidance worth applying in a FreeCAD
  detail even without a numeric table (Neuhaus p.479-496): a full-thread
  screw placed perpendicular to grain behind a "thick" fastener group lets
  n_ef = n be taken without the §5.3 reduction, sized to carry roughly 30 %
  of the fastener group's design load in withdrawal; inclined/crossed screw
  pairs transferring axial tension at a member-to-member joint must be
  angled so each screw is in **tension**, not compression (wrong inclination
  reverses this); misplacing the crossing point in a main-beam/secondary-beam
  joint induces unintended torsion in the connection — model the crossing
  point deliberately, don't let it fall wherever geometry is convenient.
- **Glued-in threaded bars (Eingeklebte Gewindestangen)** — **CORRECTED: this
  is NOT purely ETA-bound; the bond strength has a National-Annex-normed,
  length-dependent formula** (Neuhaus p.324, Tab. 7.11, DIN EN 1995-1-1/NA
  NCI NA.6.8.5, Tab. NA.12): l_ad ≤ 250 mm → f_k1,k = **4.0 N/mm²** (matches
  the earlier digest value, but only in this length band); 250 < l_ad ≤
  500 mm → f_k1,k = 5.25 − 0.005·l_ad; 500 < l_ad ≤ 1000 mm → f_k1,k =
  3.5 − 0.0015·l_ad. γ_M,H = 1.3; f_k1,d = k_mod·f_k1,k/γ_M,H. Design:
  F_ax,Rd = min{f_y,d·A_ef ; π·d·l_ad·f_k1,d}; **the NA explicitly recommends
  sizing so the steel governs** (F_ax,S,Rd < F_ax,F,Rd) for a ductile,
  non-brittle failure mode. **l_ad,min = max(0.5·d² , 10·d)** mm; **max
  effective wood tension area per rod A_ef,max = 36·d²**. (Surface-bonding
  variants: f_k2,k = 0.75 N/mm² FRP, f_k3,k = 1.50 N/mm² steel plate — same
  table, different application.) The bar-diameter/pre-drill/edge-distance
  parameters remain ETA-bound as before — only the bond-strength formula is
  now normative rather than a single flagged digest value.

### 5.6 Bolts and dowels (Schrauben, Stabdübel, Passschrauben)

- Steel grades S235/S275/S355 dowels; M-threads property classes 4.6-8.8
  (f_u,k 400-800); threaded rod 5.8. Yield model §5.1 with M_y = f_u·d³/6.
- **Washers/plates — CORRECTED sequence** (Neuhaus, Ingenieurholzbau, 4th ed.
  2017, p.427, Tab. 11.11, DIN 1052:2008-12 Anhang G.3.4 preferred sizes;
  general sizing rule EC5 §10.4.3: d_a ≥ 3d, s ≥ 0.3d): **M12→Ø58, M16→Ø68,
  M20→Ø80, M22→Ø92, M24→Ø105** — the earlier digest kept the right diameter
  progression but wrongly labelled it M12/16/20/**24**/**30**: the real table
  stops at **M24** and the second-to-last size is **M22**, not M24; there is
  no M30 row. Thickness s = 6 mm (M12/M16), s = 8 mm (M20/M22/M24); inner
  diameter 14/18/22/25/27 mm. Purpose: spread head/nut pressure f_h,d,
  prevent embedment losses on shrinkage; **re-tension after drying shrinkage**
  of members loaded across the bolt group.
- Bolts are SL-analogues (bearing after slip); in timber they need big plates
  because wood crushes ⊥ grain under nuts. End-grain bearing of a bolt is fine;
  loading the timber in bearing ⊥ grain at the plate is the check.

### 5.7 Ring and shear-plate connectors (Ring-/Scheibendübel, EN 14566 types
A/B; toothed plate types C)

**Diameters and base capacity — CORRECTED (the earlier Ø grid was
fabricated/from a mismatched catalogue).** Real product sizes (Neuhaus,
Ingenieurholzbau, 4th ed. 2017, p.510-511, Tab. 12.6, DIN EN 1995-1-1:2010-12
§8.9): **Type A1 (Ringdübel, two-sided) Ø 65, 80, 95, 126, 128, 160, 190 mm**;
**Type B1 (Scheibendübel, one-sided) Ø 65, 80, 95, 128, 160 mm**. The earlier
diameters 50/75/117/140/165 do not exist in this table — drop them.

Characteristic resistance per unit, per shear plane, ρ_k = 350, k_i = 1.0 (N):

| Ø | 65 | 80 | 95 | 126 | 128 | 160 | 190 |
|---|---|---|---|---|---|---|---|
| A1/B1 | 18 300 | 25 000 | 32 400 | 49 500 | 50 700 | 70 800 | 91 700 |

**No separate ρ_k = 420 table exists** — density is a single multiplicative
factor k₃ (below), monotonically non-decreasing with ρ_k, so higher density
can never lower capacity; the earlier "ρk=420" row with cells sometimes
*below* the ρk=350 row was a fabrication/misalignment artifact — discard it.

Base formula (constants confirmed): F_v,0,Rk = min{k1·k2·k3·k4·35·d_c^1.5 ;
k1·k3·31.5·d_c·h_e} (worked A1-Ø65, h_e≈15mm: min(18.34; 30.7) = 18.3 kN ✓).

**k1-k4 factors — CORRECTED (Neuhaus p.509-510):**
- k1 (thickness) = **min{1 ; t1/(3·h_e) ; t2/(5·h_e)}** — a continuous ratio,
  not a binary "t ≥ t_min+h_e" cutoff.
- k2 (end distance, −30°≤α≤30°) = min{k_a ; a₃,t/(2·d_c)}, k_a = 1.25
  (single connector/shear plane) or 1.0 (multiple); k2 = 1.0 outside that
  α range.
- k3 = min{1.75 ; ρ_k/350} (confirmed as before).
- **k4 is NOT a direction factor — it is a material-pairing factor**: k4=1.0
  timber-timber, **k4=1.1 steel-plate-timber**. Angle/direction dependence is
  handled separately: F_v,α,Rk = F_v,0,Rk/(k₉₀·sin²α+cos²α), k₉₀=1.3+0.001·d_c.

**Spacing / edge distances** (d_c = connector Ø): a₁ = (1.2 + 0.8·|cos α|)·d_c;
a₂ = 1.2·d_c; a₃,t = 2.0·d_c; a₃,c = (0.4+1.6·|sin α|)·d_c [90-150°,
210-270°] / 1.2·d_c [150-210°]; a₄,t = (0.6+0.2·|sin α|)·d_c; a₄,c = 0.6·d_c
(worked check: 130<150; 78<80; 130<150; 39<60 ✓ — matches the earlier
a₁/a₂/a₃,t/a₄,c figures, now with the previously-missing a₃,c/a₄,t angle
forms added).

**γ_M = 1.3** for ring/shear-plate connectors — CONFIRMED decisively as the
book's own consistently-used value (p.510, Gl. 12.3), a *different* row from
the dowel-type-fastener bending value (γ_M=1.1, §5.1) because failure here is
governed by wood embedment/crushing, not steel bending. **Never apply the
§5.3 default γ_M=1.1 to ring/shear-plate connectors.**

### 5.7a Ring connectors & surface dowels (Ringverbinder, Flächendübel /
Scheibendübel) — n_eff and worked design

Terminology: Ringdübel/Ringverbinder = ring connector; Scheiben-/Flächendübel
= shear plate; toothed plate = type C (Tabelle 12.10/12.11, p.512-521 —
diameter/h_e/capacity columns exist analogous to A1/B1 above but were not
extracted in this pass; add if a Type-C project comes up).

**Effective number n_eff (ring connectors parallel to grain — own rule, NOT
the §5.3 dowel form) — CORRECTED formula:**

```
n_eff = 2 + (1 − n/20)·(n−2)        (2 < n ≤ 20; max 20 connectors/row)
```

[Neuhaus p.511, Gl. 12.5, Tab. 12.4] Lookup: n=1→1, 2→2, 3→2.85 (confirms
the earlier worked digest), 4→3.60, 5→4.25, 6→4.80, 7→5.25, 8→5.60, 9→5.85,
10→6.00, 11→6.05 (peak), 12→6.00, …, 20→2.00 (symmetric decline). **A row of
12 connectors gives n_eff = 6.00, not 11.4** — the earlier "4 groups → 11.4
of 12" combined two parallel rows of 6 (2×6.00=12.0, not a literal 4-group
sum); re-derive any multi-row worked example from this table rather than
reusing the old shortcut.

**Worked tension splice (C30 ρ_k 380, 12× A1 Ø65 in two rows of 6, single
shear, F_d 101.3 kN permanent, k_mod 0.6):**
1. spacing/edges ✓ (above);
2. k3 = min(1.75; 380/350) = 1.086 → F_v,Rk = 18.3·1.086 = 19.9 kN per unit;
3. F_v,Rd per unit = 0.6·19.9/1.3 (γ_M = 1.3, confirmed above) = 9.18 kN;
4. n_eff per row of 6 = 4.80; two rows → n_eff,total = 9.60 → capacity =
   9.60·9.18 = 88.1 kN → **util 101.3/88.1 = 1.15 — fails at this row
   count/diameter; add connectors or step up to Ø80** (this re-derivation
   supersedes the earlier "0.97 ✓" result, which used the wrong n_eff).
Detailing: matched rings on both faces (Gegenring), central bolt + DIN 440
plates, full clamping at assembly, re-tension after shrinkage (§5.6 logic).

**Passholz / steel-plate pairing (practice note, not part of the table
digest):** every splice with a middle steel plate creates two shear planes
per connector line — each timber face needs its own matched ring line and
its own n_eff; a timber insert (Passholz) between steel plates is designed
as an independent member (own edge distances, own bearing zone at the plate
end); steel plate and bolt group to EN 1993 with the timber embedment
governing; a₃,t end distance measured from BOTH facing elements.

### 5.8 Metal connector plates and standard detailing rules

- **Nail plates (Nagelplatten)**: factory truss plates only; plate check γ_M
  1.25; minimum member thickness; plate overlap at splices; no field
  nail-plating.
- **Punched/embossed plate & angle connectors (abZ/ETA type tables)**: use
  the approved characteristic values only; group reduction tables per approved
  pair count; predominantly static load + moisture limits per approval; the
  digest's example approval list was already expired — re-check.
- Framing principles from connection physics (EN-agnostic):
  1. shortest force path; axes aligned (2 members) or concurrent (≥ 3) —
     eccentricity = unplanned bending;
  2. no acute angles between members (jam + splitting + no tool access);
  3. introduce point loads where the receiving member is stiff (axial into
     end grain, not transverse into a thin edge);
  4. stagger (entflechten) fastener rows of adjacent layers; provide slip
     capacity where shrinkage is expected (oversize/slotted holes);
  5. classify all 12 senses per joint (6 translations + 6 rotations) —
     form-fit/material-fit/force-fit per direction, not "the joint is rigid";
  6. never rely on a compression joint whose compression can vanish
     (uplift/shrinkage) — provide a tension route (strap, through-bolt);
  7. notch only where stress is low (near inflection points), never in the
     tension zone.
- **Typical joints (practice, EN-checkable):** rafter-to-plate = designed
  uplift strap + nails for position only; joist-to-beam = hanger with full
  manufacturer nail/screw pattern (a ledger strip alone is not a connection);
  beam-to-column pincer = twin beams, connectors at min edge distances with
  shear length in front of the group to stop splitting; slotted-in steel plate
  with dowels through the column; steel saddle (Sattelholz) at perpendicular
  compression.
- **Corrosive pairing:** copper-based preservatives attack plain steel — use
  hot-dip galvanized (thick class) or stainless; aluminium against treated
  spruce corrodes: isolate.

### 5.9 Timber-to-steel and column-foot notes

Raise structural timber off the pedestal (see §6.2), isolate from
masonry/concrete with a DPC under the sill, and take uplift with a hold-down on
a designed anchor group (concrete-edge check → concrete-detailing); steel shoes
and fork columns bear on plates sized for f_c,90,d with shear keys so anchors
carry uplift only.

### 5.10 Traditional carpentry joints (Zimmermannsmäßige Verbindungen)

Not folklore — **Versätze, Zapfen and Holznägel are normed under DIN EN
1995-1-1/NA:2013-08, NCI NA.12**, with real design formulas (Neuhaus,
Ingenieurholzbau, 4th ed. 2017, p.543-556, Ch.14 — confidence high on
normative status, medium-high on exact constant transcription, light re-check
recommended before publishing exact numbers). Relevant to heritage/exposed-
timber-frame FreeCAD modelling where mechanical fasteners would be visually
or historically wrong.

- **Versätze (notched/step joints, p.543-551):** compression-only —
  decompose the force into normal (N_d) and diagonal (D_d) components and
  check bearing stress on the notch face; Stirnversatz (frontal notch),
  Fersenversatz (heel notch), Brustversatz variants. **Always needs a
  secondary connection against sliding** — a Versatz alone never resists
  tension or lateral slip.
- **Zapfen (mortise-tenon, p.551-554), Tab. 14.2 (NCI NA.12.2):** for beams
  h ≤ 300 mm, shear capacity F_Rk = min{(1/k_z)·b_ef·h_e·k_z·k_v·f_v,k ;
  1.7·b·l_z,ef·f_c,90,k} (checks both wood shear and end-bearing); own
  min/max tenon geometry table; own splitting/cross-grain-tension check
  (§4.10-style).
- **Holznägel (oak dowels, p.554-556), Tab. 14.3:** simple shear formula
  **F_Rk = 9.5·d²** [N, d in mm], single or double shear; own (smaller than
  Stabdübel) spacing table, independent of grain direction.

---

## Section 6: Timber durability — DIN 68800 use classes and constructional protection

### 6.1 Gebrauchsklassen (use classes, DIN 68800-1:2019-06)

| GK | Exposure | Examples | Moisture regime |
|---|---|---|---|
| 0 | visible, dry interior, above ground | exposed interior columns/beams | ≤ ~12 % short-term wetting |
| 1 | concealed/protected interior, above ground | rafters/beams under the roof covering (not GK0), interior walls | occasional condensation allowed |
| 2 | interior against damp masonry; covered exterior with splash-water protection | old-building beam heads, covered bridges, carports | short wetting, slow drying |
| 3.1 | above ground, permanent weather exposure; splash water at member feet | open facade members, fence posts with splash, balconies (damp) | frequent wetting |
| 3.2 | as 3.1 but with water accumulation/stau or high organic attack | flat-hung boards, wet zones | long wetting |
| 4 | permanent fresh-water contact | hydraulic structures, bank protection | saturated |
| 5 | permanent seawater contact | piles, dikes, jetties | saturated |

**Species natural durability (core/Kernholz unless noted):** Fichte (spruce, no
core) → GK 0; Kiefer (pine) core → 0-2; Lärche/Douglasie core → 0-3.1; Eiche
core → up to 3.2; Buche → 0 only (not durable, never outside); tropical/very
durable (teak, Afzelia) → up to 4; Azobé → 5; lapacho (Ipe) → 4. Sapwood (Splint)
of all species is not durable → treat or avoid.

**CONFIRMS this matrix against the primary source** (Neuhaus, Ingenieurholzbau,
4th ed. 2017, p.220-221, Tab. 5.8, DIN 68800-1:2011-10 Tab. 5 — the table for
which GK a species may be used in *without* chemical preservative): the
species×GK assignments above are essentially correct as written. Refinements:
plantation-grown teak is explicitly **excluded** from the GK4 allowance
(natural-forest teak only); Azobé heartwood reaches **GK5**, Ipe heartwood
**GK4**; **Siberian larch (Larix sibirica, a distinct species from European
larch) gets an extra allowance to GK3.2 if ρ > 700 kg/m³** (p.221, fn.8) —
worth specifying explicitly since ordinary European Lärche/Douglasie tops out
at GK3.1. Several allowances (Kiefer→GK2, Lärche/Douglasie→GK2/3.1) are
*empirical/practice-based exceptions* under DIN 68800-1 §6.8.2.3, not a
strength-of-durability-class argument — treat them as fixed rule-book
entries, not something to extrapolate to an untested species.

> ⚠ **VERIFY remains open**: the preservative-class table (Iv/P/W/E hazard
> levels, DIN 68800-3) was not found cleanly in this source's scoped chapters
> (a related but different table — Tränkbarkeitsklassen/treatability class —
> exists further in the book, outside the mined range); read DIN 68800-3
> directly before specifying a chemical treatment retention value.

**Chemical wood protection (Präparieren):** only after the constructional
concept (§6.2) has done its best; use-class ↔ required retention/penetration
per DIN 68800-3; framing for GK2+ in dry-climate DACH is often fully
constructionally solvable (that is the point of the standard's hierarchy).

### 6.2 Constructional wood protection (Konstruktiver Holzschutz) — the rule set

Rot fungi need MC ≳ 20 % + oxygen + temperature; the design goal is not
"dryness" but **no persistent moisture** — occasional wetting plus a
guaranteed drying path. Decay of structural section is progressive and silent
(at hidden beam heads) → these rules are structural rules:

1. **Keep structural timber out of the splash zone:** ≥ 30 cm above finished
   ground (plinth/sockel of massive material ≥ 300 mm; 40 cm is the safer
   trade rule — VERIFY with local practice), no timber-to-soil contact ever,
   no timber buried in masonry.
2. **Shed water fast:** vertical faces stay drier than inclined; every
   horizontal-ish timber face either slopes (≥ ~5°; flat end grain collects
   water) or is covered; rain-proof overhangs (deep eaves keep walls nearly
   dry); drip edges/Tropfkanten under every shelf; no water-holding concave
   geometries; open joints/shingles overlapped in the flow direction.
3. **Ventilate:** back-ventilated cladding; beam heads in walls get an air
   gap + DPC wrap (old-building rule for GK2); ridge/eave ventilation of roof
   cavities; no vapour-tight wrap on the cold side of a damp-prone member.
4. **Protect end grain** (capillary suction climbs it): metal caps, sloped
   cuts, side-board covers, wax/sealant on cut ends.
5. **Isolate from other materials:** PE/bitumen strip under sills and posts
   (also spreads bearing), no direct concrete contact, stainless/galvanized
   connectors compatible with the preservative.
6. **Design the moisture budget:** diffusion-high-inside/low-outside (never
   trap a damp layer between two near-closed skins), airtight layer protected,
   service leaks must be detectable/drainable.
7. **Maintenance zones declared at handover:** exposed facade timber needs a
   coating cycle (state it), horizontal members are the hardest detail on
   every building.

---

## Section 7: Timber fire design (DIN EN 1995-1-2 + NA)

### 7.1 Why timber is a fire-friendly structure

Charring forms an insulating layer (≈ 0.65-0.8 mm/min) that protects the
surviving core, while unprotected steel loses most strength by ~600 °C within
minutes. Heavy timber reaches feuerhemmend/hochfeuerhemmend analogues (F30-F60;
F60-BA/F90-BA with non-combustible linings per the DIN 4102-17 melting-point
logic; MHolzBauRL for special buildings) **by oversizing alone**; planar CLT
soffits + burn-off allowance reach F90 without a suspended ceiling.

### 7.2 Two verification methods

**Method A — reduced characteristic lines:** d_char,n = β_n·t_n; effective
d_eff = d_char,n + k_0·d_0 (notional layer d_0 = 7 mm lost strength). **k_0/d_0
branch CONFIRMED** (Neuhaus, Ingenieurholzbau, 4th ed. 2017, p.166-167,
Tab. 4.13): **unprotected surfaces** — k_0 = t/20 for t < 20 min, **k_0 = 1.0
for t ≥ 20 min**; **protected surfaces** — if the lining's char-onset time
t_ch ≤ 20 min, k_0 = t/20 (t = t_ch); if t_ch > 20 min, k_0 interpolates
linearly between 0 and 1 over 0 ≤ t ≤ t_ch.

**β_n charring rate — CORRECTED table** (Neuhaus p.141-142, Tab. 4.8, = EN
1995-1-2 Tab. 3.1), mm/min:

| Product | β_0 | β_n |
|---|---|---|
| Softwood **and beech**, glulam, ρ_k ≥ 290 | 0.65 | **0.70** |
| Softwood **and beech**, solid, ρ_k ≥ 290 | 0.65 | **0.80** (resolves "worked R30 used 0.8" — this is simply the correct standard value for solid softwood, not a conservative NA add-on) |
| Hardwood except beech, ρ_k ≥ 290 | 0.65 | 0.70 |
| Hardwood except beech, ρ_k ≥ 450 | 0.50 | 0.55 (linear interpolation 290<ρ_k<450 permitted) |
| LVL, ρ_k ≥ 480 | 0.65 | 0.70 |
| Wood cladding boards, ρ=450, 20mm | 0.90 | — |
| Plywood, ρ=450, 20mm | 1.00 | — |
| Other wood-based panels (OSB, particleboard, fibreboard), ρ=450, 20mm | 0.90 | — |

For other density/thickness board products: β_0,ρ,t = β_0·(450/ρ_k)·(20/h_p).
Minimum width for the 1-D charring method: b_min = 2·d_char,0+80 (if
d_char,0 ≥ 13mm) or 8.15·d_char,0 (below) — otherwise use β_n instead of β_0.
Then run §4 checks on the reduced section with γ_M,fi = 1.0 and k_fi (§1.2).

**Method B — reduced properties:** gross section, **k_fi (not γ_M,fi — see
§1.2) = 1.25 on f_m,k** (bending; compression/E factors per EN 1995-1-2
Tab. 2.1/NA — not independently re-verified this pass); k_mod,fi =
1 − (1/200)·(p/A). Buckling/LTB per EN 1995-1-1 §6.3 with fire-time restraint
layout.

**Protective linings (gypsum EN 520 type A/F/H) — CORRECTED, onset-time
formula now given** (Neuhaus p.151-152, Tab. 4.10): t_ch [min] = onset of
charring under a protective layer. Wood cladding/board layers: t_ch =
h_p/β_0. **Single gypsum layer type A/F/H**: t_ch = 2.8·h_p − 14 (taped
joints, or open joints ≤ 2mm); t_ch = 2.8·h_p − 23 (open joints > 2mm).
**Two layers type A or H**: t_ch = 2.8·h_p − 14, h_p = outer thickness + 50 %
of inner. **Two layers type F**: same formula, h_p = outer + **80 %** of
inner (confirms the earlier 80 %/50 % split, now with the base equation).
Mineral wool (≥20mm, ρ≥26 kg/m³, melting point ≥1000°C): t_ch =
0.07·(h_ins−20)·√ρ_ins (matches `fire-protection-building` §9.1's formula
independently). Minimum fastener anchorage into unburnt wood l_a ≥ 10mm;
required fastener length l_f,req = h_p + d_char,0 + l_a. Staggered joints.
Cavity fire-stops in ventilated constructions per trade rules — see
fire-protection-building.

**Post-failure charring behaviour (genuinely new, Neuhaus p.148-150,
Tab. 4.9)** — optional depth beyond the load-bearing fixes above: between
t_ch and lining failure t_f, type-F gypsum and mineral wool give a *reduced*
rate via k₂ (gypsum type F: k₂=1−0.018·h_p [inner thickness]; mineral wool:
k₂=1 at h_ins=20mm down to 0.6 at h_ins≥45mm, interpolate). After lining
failure (t_f ≤ t ≤ t_a, char depth < 25mm) the rate **doubles**, k₃=2; once
char depth reaches 25mm, k₃ returns to 1.

**Connection fire resistance (genuinely new, Neuhaus p.194-196, Tab. 4.19,
EN 1995-1-2 §6.2.2.1)** — more precise than the flat k_fi table above for
unprotected dowel-type fasteners in shear: F_v,Rk,fi = η·F_v,Rk·k_fi,
η = e^(−k·t_d,fi), k by fastener type: nails/screws 0.08; bolts wood-wood
0.065; bolts steel-wood 0.085; dowels wood-wood **0.04** (best-surviving);
dowels steel-wood **0.085** (worst-surviving). At t_d,fi = 30min,
**steel-side-plate dowel connections retain only ~9 % of ambient capacity**,
while wood-wood dowel connections retain ~35 % — materially changes which
connection type to specify for a fire-rated timber joint: prefer wood-wood
dowels over steel-side-plate dowels wherever a connection must survive a
fire rating unprotected.

### 7.3 Worked example — R30 beam, four-sided exposed

C24 14/24, l = 5 m, e = 0.60 m tributary; g_k 1.5, q_k 2.0 kN/m²; fire
combination γG = γQ = 1.0, ψ1 = 0.5 → q_fi = 1.5 kN/m → M_fi = 4.69 kNm.

- **Method A:** d_char,n = β_n·t = 0.8·30 = 24 mm; notional +7 → section
  7.8/17.8 cm; W = 411.9 cm³ → σ = 11.39 N/mm²; f_m,fi = k_fi·f_m,k = 1.25·24
  = 30 N/mm² (k_fi resolved above, not γ_M,fi); f_md,fi = k_mod,fi·f_m,fi/γ_M,fi
  = 1.0·30/1.0 = 30 → LTB: σ_crit = 0.78·b²/(h·l)·E_eff → 39.5; λ_rel =
  √(24/39.5) = 0.78 → k_crit = 1.56−0.75·0.78 = 0.975 → util
  11.39/(0.975·30) = **0.39 ✓**
- **Method B:** residual 9.2/19.2, W = 565 cm³, σ = 8.30;
  k_mod,fi = 1−(1/200)(p/A) = 0.839 → f_d = 25.2; λ_rel = 0.69 < 0.75 →
  k_crit = 1 → util **0.33 ✓**

### 7.4 Fire detailing rules that decide the outcome

- Connections: fastener steel chars faster than timber → shield the connection
  zone or limit contribution; hold-downs/straps need their own protection.
- Linings must survive wall/floor movement (slotted fixings; no brittle board
  joints over shrinkage-loaded stud lines).
- Ventilated cavities = chimney effect → fire-stops; non-combustible cavity
  fill in concealed lines per class.
- **Effective width of a charred member is measured between notional lines** —
  never "the core looks fine".

---

## Section 8: Steel — material, sections, member checks

### 8.0 Elastic constants (all structural steel grades, EN 1993-1-1 §3.2.6 — for FEM)

E = **210,000 N/mm²**, G = **81,000 N/mm²**, ν (Poisson) = **0.3**, α_T (thermal
expansion) = **12·10⁻⁶/K**, ρ = **7850 kg/m³** — grade-independent (S235 through
S460 share the same elastic constants; only f_y/f_u change). Use these directly
as the isotropic material definition for a steel member/plate FEM model; do not
substitute a design f_yd for E — stiffness and strength are separate inputs.

### 8.1 Grades (EN 10025; nominal f_y for t ≤ 16 mm)

| Grade | f_y [N/mm²] | f_u [N/mm²] | ε = √(235/f_y) | Typical use |
|---|---|---|---|---|
| S235 (JR/J2) | 235 | 360 | 1.00 | trusses, secondary, light frames |
| S275 | 275 | 410 | 0.92 | — |
| S355 (JR/J2/K1…) | 355 | 470 | 0.81 | portals, heavy frames, welded |
| S420/S460 | 420/460 | 530/550 | 0.75/0.71 | special (thinner plates, buckling limits) |

**f_y/f_u drop with nominal product thickness t (CONFIRMED against Wendehorst
Tab. 11.4, N/mm², t ≤ 40 mm / 40 < t ≤ 80 mm — read EN 10025-2 direct for
t > 80 mm or other delivery conditions):**

| Grade (EN 10025-2) | f_y, t≤40 | f_u, t≤40 | f_y, 40<t≤80 | f_u, 40<t≤80 |
|---|---|---|---|---|
| S235 | 235 | 360 | 215 | 360 |
| S275 | 275 | 430 | 255 | 410 |
| S355 | 355 | 490 | 335 | 470 |
| S460 | 460 | 550 | 420 | 550 |

(EN 10025-3 normalized N/NL, -4 thermomech M/ML, -5 weathering W and
-6 quenched Q/QL run a few N/mm² apart from the -2 values above at the same
nominal grade — use the -2 table for ordinary hot-rolled sections, switch
tables only if the mill certificate names a different product standard.)
Ductility check (EN 10025, all grades to S460): f_u/f_y ≥ 1.10, elongation
≥ 15 %, uniform elongation ε_u ≥ 15·f_y/E — needed for plastic (Mpl) design
to be valid; grades > S460 to S700 relax to 1.05 / 10 %.
> ⚠ **VERIFY**: delivery condition/impact-energy class (JR/J0/J2/K1-K2) is a
> toughness-and-weldability decision, not a strength one — winter sites and
> thick welded plates need J2/K. Weldability: carbon-equivalent limits of
> EN 1090-2; preheat by thickness.

### 8.2 Profile families (EN 10365 designation)

| Family | Designation | Notes |
|---|---|---|
| Parallel-flange I/H | **IPE 300** (thin economic web), **HEA/HEB/HEM 300** (HEB = heavier; M deepest), **IPAA/IPAR?** (uncommon) | workhorses: beams IPE, columns HE; h/b ≈ 1.5 (IPE) to 1.0 (HEM) |
| Tapered-flange I/U | UPN 80-400, UPE 300 | legacy channels, UPE thicker; channel section: load plane off the shear/torsion centre induces St. Venant + warping torsion (worked UPE400 trench plank: rejected) |
| Angle | L 50×50×5 … 200×200×20? | braces, gussets, battens; singly symmetric → torsional-flexural buckling check |
| Hollow | **CHS 168.3×6.3** etc., **RHS/SHS** per EN 10219/10210 | torsion-stiff, better fire/corrosion surface-per-mass than open thin sections; CHS = best for compression+torsion (crane, lattice) |
| Plate/welded | t × b, welded girders S235/S355 | welded I: h/b > 2 → LTB curve c; plate girder stiffener layout → EN 1993-1-5 |
| Cold-formed sheet | trapezoidal sheeting; Z/C purlins 150-250 × 1.5-2.5 mm galv | Z-purlins sleeved over frames; sag rods > ~6 m runs |

**Excerpt of section properties as used in the worked examples of this file
(digest values, unverified — READ producer/EN 10365 tables for anything real):**

| Section | A cm² | Wel,y cm³ | Wpl,y cm³ | i_y cm | i_z cm | I_y cm⁴ | I_z cm⁴ | I_w cm⁶ | I_T cm⁴ | notes |
|---|---|---|---|---|---|---|---|---|---|---|
| IPE 270 | 45.9 | 429 | — | 11.2 | 3.02 | 5790 | 420 | 70 580 | 15.9 | tf 10.2; S355 example |
| IPE 360 | — | — | 1019 | — | — | — | — | — | — | Vpl 476 kN; Mpl S235 239.5; IPE330 (189) fails the same check |
| IPE 450 | **98.8** | 1500 | **1702** | 18.5 | 4.12 | 33740 | 1676 | 791 (×10³ cm⁶) | 66.9 | LTB example, S235; **A and W_pl,y confirmed against Wendehorst's IPE profile table (row h=450)** — the earlier "363.6" cell was a mis-extraction, real W_pl,y = 1702 cm³. Other columns are standard EN 10365 catalogue values, not individually re-parsed from the source digest this pass |
| UPE 400 | 91.9 | — | — | — | — | 20 981 | — | — | I_s 82.2 | channel: y_T = 6.06 cm |
| HE 240 B / HE 280 A | — | — | — | — | — | — | — | — | — | frame-column and two-span-beam examples (HE280A util 0.95 elastic; Mpl,Rd 261.3; A_v 31.8?) |
| HE 300 B | — | — | — | — | — | — | — | — | — | S235: Mpl 439, Npl 3502 kN, Vpl 642 kN, b/h? 7.5/5? |
| HE 340 A | — | 1680 | — | — | — | 27 690 | — | 1.824·10⁶ | 127 | canopy example |
| HE 500 A | — | — | — | — | — | — | — | — | — | S235: Npl 4641, Vpl 1013, Mpl 927.8 |
| HE 700 B | 344.4 | — | — | — | — | 290 200 | 33 685 | 7.01·10⁶ | 844 | crane girder example |
| CHS 355.6×8 | — | 742 | — | — | — | 13 201 | — | 0 (closed) | — | the torsion-stiff answer |
| RHS/box 500×… | — | — | — | — | — | — | — | — | — | (section factor for fire: A/V) |

> ⚠ **VERIFY every row** against DIN EN 10365 + producer tables (e.g. the IPE 450
> Wpl = 363.6 figure cannot be right for a 450-deep I — most likely a mis-extract;
> real Wpl,y ≈ 1702 cm³). These excerpt rows exist so the worked example chains
> in §9-§10 can be followed, not as a section catalogue.

### 8.3 Cross-section classes (EN 1993-1-1 Table 5.2, ε = √(235/f_y))

| Element | Cl. 1 | Cl. 2 | Cl. 3 | Cl. 4 (slender) |
|---|---|---|---|---|
| Flange outstand (compression) | c/t ≤ 9ε | ≤ 10ε | ≤ 14ε | > 14ε |
| Web, bending | ≤ 72ε | ≤ 83ε (α?; ≤ 95ε? for α → real 83ε/95ε pair — VERIFY) | ≤ 124ε | > 124ε |
| Web, uniform compression | ≤ 33ε | ≤ 38ε | ≤ 42ε | > 42ε |
| Internal part, compression grad. ψ | per α = (1+ψ)/2 forms | — | — | — |

Class → which resistance formula applies: 1/2 plastic (Mpl), 3 elastic (Wel),
4 effective (EN 1993-1-5 ρ·b_eff; ρ = 0.776?/ρ = (λ̄_p − 0.055(3+ψ))/λ̄_p²? —
use EC3 5.4 λ̄_p = √(f_y/σ_cr); σ_cr = k_σ·18.98·(t/b)²·? [kN/cm² form] with
k_σ: 4.0 (uniform compression, both edges supported), 23.9 (pure bending, ψ=−1),
0.43 (outstand), 8.2−… (ψ gradient; a/b influence) — **worked class-4 column:
λ̄_p ≈ 1.03 → ρ ≈ 0.79; worked class-4 column in §8.3**).
**Class-4 member:** N_b,Rd = χ·A_eff·f_y/γ_M1 with λ̄ from gross-section N_cr
(worked welded box example: A_eff 80.48 cm², χ 0.833 (curve c) → N_b,Rd 1432 kN).

### 8.4 Tension members

```
N_t,Rd (gross yield) = A·f_y/γ_M0
net fracture: 0.9·A_net·f_u/γ_M2 ; angles/tees: shear-lag β (worked: β2 = 0.5
   for 2 bolts — EC3 3.10.3 formula; 1 bolt: 2(e_2−d_0/2)·t·f_u/γ_M2)
staggered holes: zig-zag net section; bolt holes d_0 = d + 2 mm (normal)
```
Example: Ø24 S235 bar: N_pl,Rd = 106.3 kN (A·23.5); hybrid built-up: ΣA_i·f_yi.

### 8.5 Bending

```
M_c,Rd = W_pl·f_y/γ_M0 ≤ W_el·f_y/γ_M0·1.5 (class 1/2 plastic, capped)
shear-reduced (V_Ed > 0.5·V_pl,Rd): ρ = (2V/V_pl)²−1;
   M_V,Rd = (W_pl − A_w²/(4t_w))·(1−ρ)·f_y/γ_M0   (A_w = h_w·t_w)
N-M class 1/2: if n = N_Ed/N_pl,Rd > 0.25 →
   M_N,Rd = M_pl,Rd·(1−n)/(1−0.5a) ≤ M_pl,Rd,  a = web area share (A−2·b·t_f)/A
   (worked a = 0.283/0.235/0.425 variants — VERIFY a-definition, EC3 6.2.9(3))
```
Worked: IPE360 V 287.5/476.3 = 0.604 → ρ 0.043 → M_V,Rd 237.2 vs 190 → util 0.80 ✓
(IPE330 fails); HE300B M-N chain MN,Rd 249.5 ✓; U-section asymmetric M-N region
formulas per plastic-axis zone (tables) — VERIFY.
**Plastic vs elastic economy (worked two-span, q 50 kN/m, L 6 m, S235):** elastic
→ HE280A util 0.95; mechanism design with hinge at a = 0.414·L → HE240A, **21 %
lighter**, needs class 1 + rotation capacity; redistribution ≤ 15 % for continuous
beams (class 1/2).

### 8.6 Shear and web bearing

```
V_pl,Rd = A_v·(f_y/√3)/γ_M0;  A_v = A − 2b·t_f + (t_w + 2r)·t_f ≥ h_w·t_w
  (worked HE280A: A_v 31.8? cm² → V_pl 431.5 kN)
unstiffened transverse bearing (1993-1-5 §6 / 1-8 6.2.6):
   F_cr = k_F·π²E·t_w³/(12(1−ν²))·s̄²/h_w²;  k_F = 6 + 2·s_s/h_w (stiff end:
   6; with intermediate stiffener 3.97→6 range)
   l_y = s_s + 2(t_f + r) + m_1 + m_2;  m_i = 0.14·(b_f… )·(235/f_y) (31.4/17.9)
   λ̄_F = √(A_w·f_y/F_cr) ≤ 0.5 → χ_F = 1; else χ_F curve (0.72? class) →
   F_Rd = χ_F·l_y·t_w·f_y/γ_M1 (worked min-of-three 166 governs)
   alt 1993-1-8 form: b_eff = s_s + 2.5(t_f + r); ω = 1/√(1 + 3(b_eff/b_w)²·
   t_f/A_v-type term) = 0.903 (digest formula garbled — VERIFY 6.2.6.2);
   F_Rd = ω·β·b_eff·t_w·f_y/γ_M0 (183)
bearing stiffeners: design as strut/panel; stiffen at every concentrated load
> capacity — the classic unstiffened web failure under a beam reaction.
```

---

## Section 9: Steel stability — buckling and lateral-torsional buckling

### 9.1 Flexural buckling of members (Biegeknicken)

```
L_cr = β·L (β from frame: pinned 1.0; fixed-free 2.0; fixed-pinned 0.7;
    two-hinged frame column β from alignment chart / eigenvalue — worked:
    β_cr = 2.32 from c = (I_c/h)/(I_r/L) = 0.974 via the alignment chart — VERIFY)
N_cr = π²·E·I / L_cr²
λ̄ = √(A·f_y/N_cr) = (L_cr/i)/(93.9·ε)   (worked: S355 → /(76.4))
Φ = 0.5·[1 + α·(λ̄ − 0.2) + 0.75·λ̄²]
χ = 1/(Φ + √(Φ² − λ̄²)) ≤ 1.0
N_b,Rd = χ·A·f_y/γ_M1  (class 4: A_eff)
Buckling curve α: a 0.21 · b 0.34 · c 0.49 · d 0.76
   rolled I about y: b (h/b ≤ 1.2, t_f ≤ 40) / c; about z: c (t_f ≤ 40) / d?;
   welded: c/d depending flange edge prep — VERIFY EN 1993-1-1 Table 6.2;
   the examples used: HE160A strong-axis b; class-4 welded box c;
   lattice chords c (U-sections); IPE450 LTB about? c (h/b > 2, welded-analogue)
```
Worked (K-braced column HE160A S355, L_cr 8 m out-of-plane): λ̄ = 1.19 → curve b
χ = 0.31 → N_b,Rd 388 kN > 375 ✓; TF mode λ̄_T 0.86 not governing.
**Torsional-flexural (singly symmetric / class 3-4 / angles, channels):**
c² = I_w/I_z + (E·I_w)/(G·I_z)·(L/π)²; N_cr,TF = π²EI_z/(c²L²)·1/(1−i_p²/i_M²)
(worked: N_cr,TF 3263 ≪ 75175 → TF governs; λ̄ 1.023 → curve c about the
rotation axis, χ 0.53, N_Rd = χ·A_eff·f_y/γ_M1, util 0.97).
**Battened/lattice struts:** shear-deformable: S_v from batten/lacing
flexibility; EI_eff with 1/(1+(π²EI/(S_v L²))); e₀ = a/5 between panel points;
M = N·e₀/(1−N/N_cr); chord and lacing-bar checks separately (worked: global
util 0.74, chord 0.92, lacing bar 0.33; battened frame-strut ≈ equivalent).

### 9.2 Frame second-order and bracing rules

```
Imperfection: θ = (1/200)·α_h·α_m; α_h = 2/√h (0.5-1.0); α_m = √(1+1/m);
   worked h = 5 m → θ = 1/258; bracing force H = θ·ΣV per storey.
Method comparison (worked hall frame HE240B/IPE400, F_d 1200 kN): plumb force
   alone → 1500 kN (+25 % too generous when L_cr long); scaled eigenmode /
   substitute member (Ersatzstab) → 1204-1205 kN ✓ — use substitute-member or
   GMNIA, not bare plumb. Second-order: M = M_I/(1 − N_Ed/N_cr) (worked
   195 = 150 + 45 kNm).
Non-sway: 2nd-order effects ignorable if moment increase < 10 % (θ ≤ 0.1 form
   per EC3 5.2.1; the K1 = 0.31 check in the digest is the EC2 analogue —
   VERIFY the EC3 form). Bracing stiffness practice: ≥ 1.5-2 % of the max
   chord force restrained (timber worked case: 1.11 + wind = 2.31 kN/m line
   load). Sway SLS limit (worked): head displacement h/80 — VERIFY NA.
```

### 9.3 Lateral-torsional buckling (Biegedrillknicken) — full chain

```
M_cr = C_1·(π²E·I_z/L²)·√( I_w/I_z + (L/π)²·G·I_T/(E·I_z) )   (C_1 from
   moment shape & load height; worked parabola C_1 = 1.13; Iw/IT from tables)
λ̄_LT = √(W_pl·f_y/M_cr) (class 1/2) = √(W_el·f_y/M_cr) (class 3)
curve (rolled, h/b ≤ 2: b α 0.34; welded/h/b > 2: c α 0.49 — worked IPE450 c);
Φ_LT = 0.5[1 + α_LT(λ̄ − 0.2) + 0.75λ̄²]; χ_LT ≤ 1.0
modifier (uniform-moment basis → actual diagram): k_c from moment ratio ψ
   (ψ = 0 reverse curvature: k_c up to 1.33; ψ = 1: 1.0; parabolic 0.94);
   f from the modifier formula (worked f = 0.974 — VERIFY form); χ_LT,mod = χ_LT/f
   (alternative: compression-flange method if,z, λ̄_f — worked showed it can
   FAIL where full LTB passes; use full method + kc)
M_b,Rd = χ_LT,mod·W_pl·f_y/γ_M1 ≤ M_pl,Rd? (≤1.0·)
```
**Worked LTB (IPE450 S235, L = 6 m, fork ends, unrestrained, parabolic M,
M_Ed = 177.5 kNm):** M_cr = 350.9 kNm → λ̄ = 1.07 → χ_LT 0.596 (curve c) →
k_c 0.94 → χ_LT,mod = 0.612 → M_b,Rd = 0.612·W_pl,y·23.5/100. With the
confirmed W_pl,y = 1702 cm³ (§8.2) this gives M_b,Rd ≈ **245 kNm** → util
177.5/245 ≈ **0.72** — recompute this chain with 1702 (not the earlier
"363.6" mis-extraction) before quoting the utilization.
**Coped beam rule (worked):** cope with h_a/h ≥ 0.7 and a/h ≈ 0.5 → reduce
M_cr by V ≈ 0.68 (interaction chart) and downgrade the buckling curve one
letter; capacity drop ≈ 30 % → prefer a bolted web-cleat or a smaller cope.
**Restrained axis (worked hall column IPE270 on rotational spring from
sheeting):** torsional-flexural about the rotation axis D: I_w,D = I_w + I_z·
z_D²; half-wave number m from (L/π)(c_θ/EI_w,D)^¼ → N_cr,TF; M_cr with
I_T,id = I_T + c_θ·L⁴/(π⁴·G)?? (worked 47.56 cm⁴) and k-chart → util TF-check
**1.08 → FAIL** — conclusion in the source: increase section or improve the
rotational restraint (self-tapping density/screw class), don't just thicken
the web.
**Torsion (warping, thin-open sections):** B (bimoment) + T_t (St. Venant)
superposition; κ = (G·I_T/E·I_w)^0.25; fork support: ϑ = 0, B = 0;
σ = M_y/W + 0.75·B·ω/I_w + 0.75·σ_local (25 % local reduction allowed when
superposed); **a CHS of the same mass is torsionally ~5-20× stiffer — for
eccentrically loaded canopy edges, choose closed sections** (worked: I-defl
69.8 cm vs CHS 5.1 cm).

### 9.4 Web plate buckling (Plattenbeulen, EN 1993-1-5) & warping torsion
(Wölbkrafttorsion)

**When it governs:** welded plate girders (Vollwandträger) and class-4 welded
I-sections — the web is almost always slender (c/t > 124ε in bending; under
shear the limit drops to ≈ 48.6·ε/√(τ_Ed/(f_y/√3)) — digest form garbled,
**VERIFY**), so the web is post-buckling: elastic, no plastic reserve,
γ_M1 = 1.1, via effective widths (ρ·c) or the reduced-stress method.

**Buckling-stress and reduction chain (numbers as worked, S235):**
σ_cr = k_σ·18.98·(t/c)² [kN/cm²] (**VERIFY constant form**);
λ̄_p = √(f_y/σ_cr); ρ = (λ̄_p − 0.055·(3+ψ))/λ̄_p² ≤ 1.0 (**digest shows two
branches — (λ̄_p−0.188)/λ̄_p² and (λ̄_p−0.055)/λ̄_p² — VERIFY**);
b_eff = ρ·c split b_c1 = 0.4·b_eff at the compression edge / b_c2 = rest.
k_σ: 0.43 outstand (one edge free), 4.0 uniform compression, 23.9 pure
bending (ψ = −1), 8.2 − 1.05ψ gradient (worked ψ = 0.2 prints 6.56 — the
arithmetic does not close, **VERIFY**); shear: k_τ = 5.34 + 4/(a/b)²
(sub-field a/b = 2.02 → 6.32 ✓), whole panel with intermediate stiffener
3.4 + stiffener-rigidity term (garbled **VERIFY**).

**Class-4 welded I-column (worked: 8 m, L_cr = 0.7·L, flanges 400×20,
web 360×6 — VERIFY web size):** flange outstand c/t 19.28 > 14ε and web
> 42ε → class 4 both; flange k_σ 0.43 → σ_cr 21.96 → λ̄_p 1.035 → ρ 0.791
→ A_eff,f 31.94 cm²; web k_σ 4 → σ_cr 22.12 → ρ 0.763 → A_eff,w 16.60 cm²;
ΣA_eff = **80.48 cm²**; λ̄ from GROSS-section N_cr 7050 kN → 0.518 → curve c
χ 0.833 → **N_b,Rd = χ·A_eff·f_y/γ_M1 = 1432 kN** (class-4 rule: A_eff in
resistance, gross I in slenderness).

**Plate girder with longitudinal stiffener (worked: S355, web 1000×8 →
c/t 123.6, M_Ed 2240 kNm, V_Ed 640 kN, σ_x,Ed 29.23 / τ_Ed 7.84 kN/cm²):**
1. **Stiffener layout from reduced-stress charts:** unstiffened web allowed
   within ≈ 2.0 m of the supports (chart coordinate x ≈ 0.39·? — cell lost,
   **VERIFY**); design section at 0.5·b from the edge (**VERIFY**);
   longitudinal stiffener (L80×40×6, single-side — VERIFY) at the upper
   4/10 of web depth near the highly stressed flange.
2. **Field 3 — bending zone (ψ = −1, k_σ 23.9):** σ_cr 29.70 → λ̄_p 1.093
   → ρ 0.823 → b_eff 40.69 (16.27 + 24.42) → ΔA 7.0 cm² → A_eff 193 cm²,
   W_y,eff 7027 cm³ → η₁ = 31.88/35.5 = 0.898 ✓ (example used γ 1.0 —
   §1.2 flag).
3. **Field 1 — σ + τ combined, reduced-stress method (deformable bearing
   stiffener):** σ_v,Ed = √(σ² + 3τ²) = 18.50; f_a,ult,k/σ_v,Ed = 35.5/18.5
   = 1.92; ā_x = σ_cr,x/σ_x,Ed = 2.35, ā_τ = 1.00 → combined ā_cr = 0.92
   (combination form garbled **VERIFY**); λ̄_p = √(1.92/0.92) = 1.445 →
   χ_w = 0.83/λ̄_p = 0.574; check σ_v,Ed ≤ χ_w·f_y/γ_M1 → util **0.999 —
   governs, the girder is just adequate**.
4. **Field 2 — longitudinally stiffened (effective widths):** sub-fields
   ψ 0.2 (ρ 0.945) and ψ −0.5 (ρ 1.0 — no reduction); stiffener + plate
   group σ_cr,sl 70.48 kN/cm² → plate-vs-global interaction ξ (printed
   sqrt goes negative; digest took 0.064 — **VERIFY formula**); ρ_c 0.933
   → W_y,eff 7237 cm³ → η₁ 0.749 ✓.
5. **Shear resistance V_b,Rd:** panel λ̄_w = 1.25 (whole field governs over
   sub-fields) → χ_w 0.664 → V_bw,Rd 979 kN; flange contribution
   V_bf,Rd ≈ 20 kN (from M_f,Rd 2173 vs M_Ed 1924) → V_b,Rd ≈ 947 kN →
   η₃ 0.676 ✓; no extra M–V interaction once the flange-moment effect is
   included.
6. **Stiffener torsional (drill) buckling:** I_T = Σb·t³/3 = 0.82 cm⁴; the
   criterion prints garbled but the worked conclusion is **check mandatory
   for single-side stiffeners** — **VERIFY** against EN 1993-1-5.

**Warping torsion of open thin-walled sections (extends the §9.3 torsion
paragraph):**
- T = T_t (St. Venant) + T_w = −B′ (bimoment); warping slenderness
  κ = (G·I_T/E·I_w)^¼ (**digest prints a square root — VERIFY root order**;
  worked κ 7.50 / 5.18 1/m); restraint offset axis:
  I_D = I_w + I_z·z_D² (worked 505·10³ cm⁶? — suspect cell **VERIFY**);
  bimoment under distributed twist m: B ≈ (m/(2κ))·tanh-type form (Gl. 11.39
  — **VERIFY**).
- σ_x = M_y/W_y + 0.75·B·ω/I_w + 0.75·σ_0,local (worked 10.97 + 3.77 +
  4.53 = 19.27 < 23.5 ✓; the 25 % local-wheel-load reduction applies only
  in superposition); τ = T_t-form/I_T·t + T_w·S_ω/(I_w·t) (St. Venant term
  printed "1.65·?/I_T" — **VERIFY**; worked τ_total 11.62 < f_y/√3 =
  13.57 ✓).
- Boundary conditions: fork support (Gabel) = ϑ = 0, B = 0 — **VERIFY
  pairing per support type**; multi-span / crane girders by the
  initial-parameter 6×6 matrix per segment (worked HE700B: eccentric
  lateral load T_A = H·z_M with z_M ≈ 14.3 cm; B_Ed,max ≈ 178.4·10³ kNcm²;
  σ_x,Ed −21.63 kN/cm² governs).
- First-order waiver (rule of thumb): M_cr/M_Ed ≥ 10 → Th. I sufficient
  (**VERIFY form**); for torsion-governed edges choose closed sections —
  thickening the web never fixes warping flexibility.

---

## Section 10: Steel connections (EN 1993-1-8)

### 10.1 Bolts

| Item | Value / rule |
|---|---|
| Property classes | 4.6/4.8 (ordinary), 5.6/5.8/6.8, **8.8/10.9** (preloaded HRSG per EN 14399, "HV"), proof stress f_ub 400/420/500/600/640/800/1040? MPa (worked: 8.8 f_ub = 800, 10.9 = 1000) |
| Stress area | M16 A_s 157 mm²; M20 245 mm² (worked: M20 11.9 HRSG A_s 2.45 cm² — A_s,nom 3.03? **VERIFY tensile vs nominal shear area, threaded vs unthreaded position**) |
| Shear (bearing-type SL) | F_v,Rd = α_v·f_ub·A/γ_M2. **α_v is set by WHICH cross-section sits in the shear plane, not by grade tier alone (CONFIRMED against Wendehorst Tab. 11.175 = EN 1993-1-8 Table 3.4):** shank in shear plane → **α_v = 0.6 for every grade** 4.6/5.6/8.8/10.9 (A = shank area); thread in shear plane → α_v = 0.6 for 4.6/5.6/8.8, **α_v = 0.5 only for 10.9** (A = A_s, stress area). The worked 60.3 kN @M16 8.8 with α_v 0.6 is correct (thread-in-plane, 8.8 keeps 0.6). |
| Tension | F_t,Rd = k_2·f_ub·A_s/γ_M2, k_2 = 0.9 (0.63 for countersunk). **F_t,Rd table (kN, CONFIRMED against Wendehorst Tab. 11.178):** M12/M16/M20/M22/M24/M27/M30/M36 — grade 4.6: 24.3/45.2/70.6/87.3/101.7/132.2/161.6/235.3; grade 8.8: 48.6/90.4/141.1/174.5/203.3/264.4/323.1/470.6; grade 10.9: 60.7/113.0/176.4/218.2/254.2/330.5/403.9/588.2 |
| Bearing | F_b,Rd = [min(2.8·e_1/d_0; 1.4·p_1/d_0; α_b)] · [min(2.8·e_2/d_0−1.7; 1.4·p_2/d_0−1.7; 2.5)] · d·t·f_u/γ_M2, α_b = min(f_u,b/f_u; 1.0) |
| Eccentric group | component method: resolve F_x/F_z; vector check √((F_E,x/F_Rd,x)² + (F_E,z/F_Rd,z)²) ≤ 1; or polar I_p method for torsion (worked double-angle: F_v,i = F·(1/n ± e·z/I_p)) |
| Spacing | min: e_1,e_2 = 1.2·d_0; p_1 = 2.2·d_0 (end, static; 1.6·d_0?); p_2 = 2.4·d_0; max: e_1,e_2 ≤ 4t+40 (≤ 200 mm?); p ≤ 14t (≤ 200 mm compression; VERIFY) |
| Combined V+T | (F_v/F_v,Rd)² + (1.4·F_t/F_t,Rd)² ≤ 1.0 (worked 1.05 → "marginal, acceptable because plate mode governs" — do not copy this leniency; VERIFY per EN 1993-1-8 6.3.2.3) |
| Preloaded HRSG | slip resistance µ·F_{p,C}/γ_M3 (slip classes A/B/C/D by surface); pretension 0.7·f_ub·A_s (verified torque/slip-indicating); GV = true force-fit, replaces site welding, stiff; **no painted surface in a slip-critical class unless tested** |
| Block shear | F = f_u·A_nt/γ_M2 + f_y·A_nv/(√3·γ_M0) (worked end-plate 278 kN) |
| T-stub (end plate/cleat) | mode 1: F_T,1 = 4·M_pl/m per leff; mode 2: F_T,2 = (2M_pl + ΣF_t,Rd?·n)/(…) (worked form (2Mpl+5nFt)/(4m+5)); mode 3: bolt failure ΣF_t,Rd (2 per bolt row?) ; M_pl = 0.25·l_eff·t²·f_y/γ_M0; leff min circular/linear patterns (worked: FT,2 governs 667 kN); prying Q included; anchor-row analogue → concrete-detailing |

### 10.2 Welds

| Item | Value / rule |
|---|---|
| Directional method | σ_v = √(σ_⊥² + 3·(τ_⊥² + τ_∥²)) ≤ f_u/(β_w·γ_M2); σ_⊥ compressive normal to throat needs no check (6.2.3?; worked also quotes a τ ≤ 0.9·f_u/γ_M2? side check — VERIFY exact clause pair) |
| β_w | 0.80 (S235) / 0.90 (S355) / 1.00 (S420) / 1.10 (S460) |
| Simplified | F_w,Rd = a·l_eff·f_v,w,d with f_v,w,d = f_u/(√3·β_w·γ_M2); a_min = 3 mm (and ≥ (t_max−4)/2?); a_max by 1993-1-8 4.7 (worked derived a ≥ 5 mm from τ demand) |
| Full-penetration butt | parent-metal governed (no separate check if executed to quality) |
| Quality | NDTR (non-destructive testing rules) per EN ISO 5817 level B/C/D; shop-weld/site-bolt doctrine; **field welding on site = last resort: no procedure control, no NDT, coating damage → redesign the detail** |

### 10.3 Standard connection anatomy (portal + skeleton)

| Connection | Detail (worked values) |
|---|---|
| Eaves (rafter-to-column) | extended end plate through haunch, 20-25 mm, 8-12× M20/M24 8.8, tension bolts in top rows; check: bolts, plate bending (T-stub), column-flange deformation (stiffeners at flange lines), web panel shear, compression zone |
| Apex | end-plate splice 4-8× M20/M24; site splice located for crane + transport length |
| Base | plate 20-30 mm, 4× HD M20-M24, embedment ~375-450 mm + anchor plate/washer, grout 25-40 mm; **shear key (Schubknagge) under the plate so anchors carry only uplift**; nominally-pinned design, but a real 4-bolt base has 10-20 % fixity — the engineer states which assumption is used for strength vs deflection |
| Beam-to-column (pinned) | fin plate / double web angle, SL bolts (worked M16 4.6 double-angle: slip at column governs 171 kN); contact pressure on column flange check F_k = b_D·h_D·f_yd, h_D ≈ 3 cm (worked rule) |
| Purlin/rail cleats | 2× M12/M16; setting the roof plane — model it |
| Fly brace | angle purlin/side-rail → inner compression flange, bolted both ends — never omit |
| Splices | column splice above floor line near inflection point; beam splice where M small; machined bearing faces + shell plates against slip (compression splices), bolts for handling only |

---

## Section 11: Verification summary — the sigma/fd ≤ 1 table

| Check | Verification | Governing subtlety |
|---|---|---|
| Timber tension | σ_t,0,d ≤ f_t,0,d | net section at fastener line; k_h small-section increase |
| Timber compression | σ_c,0,d ≤ k_c·f_c,0,d | weak axis; restraints define L_cr |
| Timber bending | σ_m,d ≤ k_crit·f_m,d | **LTB (k_crit) often governs before strength** |
| Timber shear | τ_d ≤ f_v,d | cracked width k_cr·b at interior supports |
| Timber bearing ⊥ | σ_c,90,d ≤ k_c,90·f_c,90,d | spreading (3+l+3)·b; edge distance |
| Timber combined N+M | (σc/σc,crit)² + σm/(fm(1−σc/σc,crit)) ≤ 1 | both axes; substitute-column form |
| Timber deflection / vibration | w_fin ≤ limit; w1 ≤ a(n) | k_def, ψ2, camber; NA tables |
| Fastener group | F_v,Ed ≤ k_mod·n_ef·F_v,Rk/γ_M | spacing → n_ef → embedment depth |
| Glued-in rod | bond + steel + splitting | every parameter is ETA-bound |
| Steel tension | N ≤ min(N_pl,Rd; 0.9A_net·fu/γM2) | shear-lag, holes d+2 |
| Steel bending | M ≤ χ_LT,mod·Wpl·fy/γM1; M ≤ Mpl; class | restraint = LTB length |
| Steel shear | V ≤ Av·fy/(√3γM0) | 0.5 Vpl → reduce M |
| Steel buckling | N ≤ χ·A·fy/γM1 | curve assignment + class 4 A_eff |
| Steel combined | MN (n>0.25) + interaction kyy/kzy | TF mode for singly symmetric |
| Web bearing | F ≤ χ_F·l_y·t_w·f_y/γM1 | unstiffened = local first failure |
| Bolts | Fv/Fb/VT/block/T-stub per mode | group eccentricity; preload class |
| Welds | σ_v ≤ fu/(βwγM2) | throat size + quality level |
| Fire timber | M_fi ≤ χ_mod·W_reduced·f_fi | β_n, notional 7 mm, linings |
| Fire steel | E_d,fi/R_d,fi,t ≤ 1 | A/V → θ_a,cr via μ0; protection |

---

## Section 12: Steel durability — corrosion protection

| ISO 12944 class | Environment | Typical building case |
|---|---|---|
| C1-C2 | dry heated interior / low humidity | office interiors (paint only) |
| C3 | urban/atmospheric + moderate humidity | unheated halls, pool buildings (aggressive atmosphere, C3-C4) |
| C4 | industrial + coastal moderate | parking decks, moderate coastal exposure |
| C5-I/C5-M | industrial heavy / coastal-marine high | hall near sea, chemical zones |
| CX/Im2 | immersion | water-contact elements (special systems) |

**Strategy hierarchy (physics of a steel section):** danger scales with surface
per volume — fine open sections (thin L, slender trusses) corrode structurally
fastest; closed hollows are the best shape; every water-holding orientation,
capillary gap and crevice is a trap → hollows drainable and ventilable or fully
sealed (welded end closures), no downward-facing open tubes, no moisture
pockets at splices.
- **Hot-dip galvanizing (EN ISO 1461):** sacrificial + barrier; layer thickness
  scales with section thickness (thin sections thinner layers — design for it);
  duplex (galv + paint) extends interval; cut edges/drilled holes need
  zinc-rich repair.
- **Bimetallic rule:** fasteners nobler than (or isolated from) the base —
  steel against Zn/Al/Cr sacrificial-safe, against Cu bad. **Weathering steel:**
  stable layer only with true wet/dry cycles + drainage; runoff stains.
- **Maintenance:** coatings have renewal cycles; design access or accept a
  lifecycle line item; inspect bolt heads and bearing zones (damage indicator
  tables: loose/missing bolts, torn plates, streak rust).

---

## Section 13: Steel fire design (DIN EN 1993-1-2)

```
member: E_d,fi / R_d,fi,t ≤ 1.0
material: k_y,θ = f_y,θ/f_y = 1.0 up to θ_a ≈ 350 °C then falling (≈50 % at
   ~600 °C); NA floor: below ~350 °C no reduction (EU.2.3).
heating: unprotected steel rate ∝ (k_w·A/V)/(c_a·ρ_a) — Profilfaktor A/V:
   open thin I ≈ 150-250 m⁻¹ (fastest), HE ≈ 80-150, filled CHS slowest.
critical temperature: θ_a,cr from utilization μ0 = N_fi,Ed/N_pl,Rd
   (nomograph/table: μ0 ≈ 0.5 → ~600 °C, μ0 ≈ 1 → ~470-500 °C — VERIFY the
   NA table); low utilization is itself fire protection.
protection menu: concrete encasement / composite column; slab-supported beams
   (slab = heat sink); fire boards (dry zones); intumescent paint (system +
   inspection); water-filled hollows; stocky sections (A/V as design input).
tension: θ_a,lim only if elongation harms the structure; compression/flexure:
   full θ-dependent χ check.
```
**GKL requirement mapping (Germany):** GKL4 load-bearing timber = F60-BA
(lining concept), GKL5 = F90-AB → a steel house/facade structure at GK4+ needs
a protection package from day one; unprotected steel frames are realistically
≤ F30 at best for stocky sections — state this at system choice.

---

## Section 14: The systems in practice

### 14.1 Timber practice lines

- **Stud/panel (T1):** DACH panel grids run on the 62.5 cm module to suit
  joist/panel formats; platform storey-high; shear design = nail/screw line
  spacing of the sheathing (edge spacing IS the capacity); chord forces at
  panel ends → hold-downs into a designed anchor group; double top
  plate/sill continuity = the ring that ties the box; noggings/blocking
  scheduled at every wall-hung load before boards go on.
- **Solid/CLT (T2):** wall-floor nodes must keep the gravity path **along
  grain into grain** (steel angle/z-cleat on wall, ledge/trimmer, concrete
  dowel or WCC edge beam at higher storeys); perpendicular-bearing floors
  cap the stack at ~4-5 storeys (settlement) — above that switch node type.
  Insulation outside the static section (thickness ≠ U-value); airtightness
  via the few panel joints; acoustics need mass-spring (floating screed,
  loose-bound chippings/concrete topping). **CLT high-rise:** end-grain
  stacked walls + steel inserts at columns (Brock Commons-type detail: CLT on
  steel telescopic tube columns with plywood diaphragm strips across the butt
  joints) — tall-timber is a connection + core + acoustics + fire-duration
  exercise, not a span exercise.
- **Glulam halls (T3/T4):** portal corners have no perpendicular-compression
  path → mitre + diagonal block or factory-curved finger-jointed corner; 3-hinged
  apex pin splits transport to halves ≤ ~4 m; fork feet around columns; roof
  diaphragm ring (perimeter diagonals) + end-bay vertical bracing (mid-bay
  variant releases thermal movement).
- **Trusses/binders (T4):** depth ≈ L/6-L/12; pitch 15-45°; load at nodes only
  (purlins must land on joints or add struts); tie at eaves unless the support
  takes thrust; collar in upper third; connectors: gussets, plate rings §5.7.
- **WCC floors (T6):** pin count = interface shear / pin capacity; transverse
  tie steel in the slab over supports; connector reversal at cantilevers is
  the weak point — detail symmetric or avoid.

### 14.2 Steel practice lines

- **Portal:** bays 4.5-7.5 (6.0 typical) m; rafter depth L/40-55; haunch
  depth 1.5-2× rafter, length L/10-L/7 — **the haunch eats eaves headroom,
  model it before placing doors/windows**; fly braces inside flange at
  eaves + first purlins; purlins Z 150-200 × 1.5-2.5 galv @ 1.2-1.8 m
  sleeved, sag rods > ~6 m; roof + wall cross-bracing in end bays and at
  ≤ ~5-bay intervals; base thrust H ≈ w·L²/(8f) three-hinged hand check:

  | pitch | H per base @ L=12 m, w=9 kN/m |
  |---|---|
  | 6° | ≈ 257 kN |
  | 10° | ≈ 153 |
  | 15° | ≈ 101 |
  | 20° | ≈ 74 |

  → pitch 15-25° is free structural performance; resolve thrust into a tie
  rod/beam under the slab (protected, on the services drawing so nobody
  trenches it), moment pads, or a stiff ground ring — never the unreinforced
  slab.
- **Trusses:** 10 m → >100 m; welded or bolted plate nodes; crown/ridge
  splice at the site transport limit; camber preset for deflection and
  drainage; chord restraint = the purlin/brace line — design the
  sheeting-to-purlin screw group for the chord-force fraction; lattice
  girders double as floor diaphragm substitutes.
- **Multi-storey skeleton:** pinned beam→column default (fin plate); moment
  where drift demands; braced by cores + K/X bracing (tension-only X needs
  both diagonals; single tension diagonal cannot reverse); column splices
  above floor at the inflection point; base plates as §10.3; composite slab:
  head studs φ19 P_cRd concrete-governed (worked 61.4 kN) → n =
  V_L = N_pl,a/P_cRd, equidistant if M_pl,comp/M_pl,a ≤ ~2; b_eff per
  EC4 (worked: outer field 3.40 m of 5.0 m bay; inner 2.80; support 2.0);
  longitudinal shear: tie reinforcement in flange v_Ed·cot β/h·f_sd; camber
  for dead-load deflection (worked 2.8 cm); slim-floor shelf beams where
  services must run flat.
- **Hybrids:** steel beam inside masonry/RC → isolate (soft joint), corrosion
  protection at the pocket, bearing plate; timber floor on steel = perpendicular
  compression solved with a saddle or top-flange plate + elastomer; transfer
  girder logic at platform interfaces (concrete).

### 14.3 Anti-pattern quick list (both materials)

| Anti-pattern | Consequence |
|---|---|
| fly-brace / flange restraint omitted | LTB collapse of the "complete-looking" frame |
| no longitudinal bracing on a portal building | mechanism in the long direction |
| base thrust left to the floor slab | frame spreads, slab cracks, ridge sags |
| hold-down missing at shear-panel end | panel overturns; bracing does nothing |
| nails relied on for uplift/withdrawal | roof leaves in the first storm |
| field welding thin sections / field punch-outs | destroyed capacity + coating |
| timber in splash zone / buried end grain / beam head in damp masonry | GK exceeded → silent decay at the bearing |
| bolt group checked for one load direction only | angled loads need the component check |
| slip-critical joint built with ordinary bearing bolts | slip, deflections, fatigue |
| unstiffened web under a beam reaction | local web crippling (first failure) |
| unprotected slender steel promised F90 | not credible — change section or protection |
| cross-grain shrinkage put into a bearing/stack line | gaps, loosened bolts, sagging roof |
| masonry infill built tight into a frame, unanalysed | short-column/stiffness trap |
| supplier calculation accepted as the engineering | nobody checked foundation, thrust, uplift |

---

## Section 15: FreeCAD modelling + IFC

Pair with the FreeCAD-BIM skill for the Site/Building/Storey hierarchy,
parametric openings and FEM handoff.

### 15.1 Defaults

| Item | Default | IFC class / note |
|---|---|---|
| Steel beam/column | `Arch Structure` with profile from the profile library — **name it by the EN 10365 designation** (`IPE 300`, `HEB 240`, `HSS 200x100x8`) | IfcBeam / IfcColumn; profile name + grade (S235/S355) in the type description; Pset `Pset_BeamCommon`/`Pset_ColumnCommon` |
| Haunch, base plate, fin plate | model explicitly as small solids/plates | IfcMechanicalFastener / IfcPlate; never "implied" |
| Bracing/struts/purlins | IfcMember, model the braced bays at least | if invisible in the model, invisible on site |
| Tie rod / sag rods | model them — the item most often value-engineered out | IfcMember |
| Glulam/timber member | rectangular Part b×h at nominal size (EN 336); camber as swept profile only if the file carries it | IfcBeam/IfcColumn/IfcMember; material class ("GL28h" / "C24") + service class + DIN 68800 GK class in properties |
| Stud wall | model as Arch Wall, overall 140-240 mm + finish; do **not** model every stud whole-house — one representative bay only | IfcWall (LoadBearing = True), framing depth in metadata |
| CLT panel | IfcSlab/IfcWall with layer set (plies + top/bottom), span direction marked | store lay-up `3s 20/40/20` in properties |
| Shear-panel fastener lines | represent as notes/types, not individual nails | IfcMechanicalFastener type rows where a count matters |
| Hold-down / anchor | small explicit object at panel ends + anchor position schedule | IfcMechanicalFastener |
| Foundation | model it — timber/steel concentrate uplift + thrust + point loads | IfcFooting |
| Storey heights | timber: 2.80/3.00 m; CLT grid from panel format; steel halls: eaves height incl. haunch check | |
| Tolerances | +10 mm interface gaps at material boundaries (steel vs concrete accuracy classes differ); slotted holes modelled where movement is designed | DIN 18202 classes |

### 15.2 Modelling discipline

1. **The lateral system, the haunch, the tie rod and the plinth are modelled
   or they do not exist.** These are the four value-engineering casualties.
2. Annotate the model README with: system, code basis (EC5/EC3 + NA edition),
   assumed wind/snow/use loads, restraint layout (LTB lengths you assumed),
   section list with grades, fastener types with approval source, and the
   sentence "preliminary sizing — requires design and signature by a
   qualified structural engineer".
3. FEM caveat: a solved member stress verifies none of: a bolt group, a T-stub
   mode, a dowel yield pattern, n_ef group reduction, an unstiffened web, an
   LTB mode or a connection's perpendicular-tension path. Report that when
   exporting results.
4. Export IFC4 (Reference View or Design Transfer); check the profile strings
   survive (ifcopenshell), the storey aggregation is clean and the
   LoadBearing flags are set — fabricators cut quantities from these.
5. Cutting lists / bar schedules may be produced from the model **as
   planning aids only**, marked preliminary, never as shop drawings.

---

## Section 16: Known gaps — state these when relevant

1. **§3.1/3.2 solid timber tables, §3.4 k_mod, §4.5 k_c,90, §8.1 steel grade
   thickness table, §8.2 IPE 450 row and §10.1 bolt α_v/F_t,Rd were
   cross-checked against Wendehorst Bautechnische Zahlentafeln (37th ed.)
   and corrected/confirmed in place** (2026 pass) — the E_0,05/E_0,mean
   columns were NOT transposed after all; the real errors were a few
   individual cells (C24 f_v,k, C35 f_c,90,k, the CL2 k_mod column, the
   hardwood k_c,90 default, the IPE450 Wpl,y mis-extraction, and the bolt
   α_v grade-vs-shear-plane rule). The rest of the §8.2 property excerpt (all
   rows except IPE 450) is chain-illustration, not a verified catalogue.
2. **Timber Sections 3-7 received a second, deep cross-check against Neuhaus,
   Ingenieurholzbau, 4th ed. 2017 (2026 pass)** — this resolved the large
   majority of the timber VERIFY flags that survived pass 1: k_h/k_ℓ/k_cr
   size and cracked-width formulas (§3.4), the full k_def panel table (§3.4),
   BSH size/length limits (§3.7), M_y,Rk exponent and γ_M basis for dowel
   connections (§5.1), the a₁-a₄ spacing tables incl. a separate bolt/
   threaded-rod table (§5.2), the n_ef formula incl. the α=90° special case
   (§5.3), nail withdrawal (now density-quadratic, not a diameter grid) and
   penetration reduction (§5.4), screw withdrawal formula and spacing (§5.5),
   the glued-in-rod bond-strength formula (now NA-normed, not purely ETA-
   bound, §5.5), the washer table (§5.6), the ring/shear-plate connector
   diameters/capacities/factors/n_eff formula — the single largest VERIFY
   block in the file (§5.7/5.7a), buckling k_c's β_c factor and l_ef table
   (§4.2), LTB k_crit thresholds and the glulam 1.4 stiffness factor (§4.3),
   shear k_cr by product (§4.4), the deflection-limit table and the
   vibration check method (§4.8), the notch k_v/F_t,90 formulas (§4.9), fire
   β_n/k_0/gypsum-onset-time/connection-fire-resistance (§7.2), and the
   γ_M,fi-vs-k_fi relabelling (§1.2). New subsections added: glued
   connections/finger joints and frame corners (§3.7), a holes-through-beams
   ruleset (§4.10), traditional carpentry joints (§5.10), and an EC5-specific
   fly-brace force formula (§4.3). **Still open, not resolved by either
   pass:** plate-buckling k_σ/ρ formula branches (§9.4), warping-torsion κ
   root order, T-stub mode-2 formula (steel, unaffected by the timber
   source), the LTB effective-length l_ef exact algebraic form (§4.3 — table
   of a1/a2 coefficients is solid, the equation structure is not), the
   "45°→1.77" n_ef interpolation worked number (§5.3), diagonal-nailing NA
   reduction percentage (§5.4), staggered-hole net-section rule (§4.1), and
   the DIN 68800-3 preservative-class/hazard-level table (§6.1).
3. No seismic (EN 1998) content; connection ductility for dissipative systems
   is a specialist check. Nothing here is a fabrication drawing, cutting list
   or connection design; NA/revision state must be re-verified per project.

---

## Section 17: Cross-references

| Need | Skill |
|---|---|
| system choice, loads, massing of the building | structural-systems |
| product classes, densities, CE/DoP, section standards | building-materials |
| GK classes, required fire durations, escape | fire-protection-building |
| anchors into concrete, base-plate grout, WCC topping | concrete-detailing |
| uplift/bracing forces from wind & seismic | seismic-design / a loads skill |
| footing under columns/hold-downs | geotechnics-foundations |
| layer build-up, joints, water-shedding of timber/steel envelopes | construction-detailing |
| modelling workflow, IFC QA, FEM pipeline | construction-freecad-bim |
| framing-system alternatives catalogue (which system, spans, costs) | timber-steel-design |

---

## Appendix S: Source Check 2026-10 — values re-read from the literature

Each line below was read again in the source books (`sources/`) in October 2026, with the
place it stands at. "Confirmed" means: a dated book prints the rule and names the standard
or law; it does not mean the current edition of that standard was opened. State law
(LBO) and local rules still override; `VERIFY` tags elsewhere in this skill stay in force
unless a line here names the edition. Where a line here differs from a section of this
skill, that section was corrected and names the line ("S.n"); the appendix governs.

### S.1 Purlin roof of a house — spacings

- Typical: purlins are needed every 4 to 5 m across the building to support the rafters;
  the plain rafter roof was built with rafter lengths up to 4.5 m, longer rafters got a
  collar beam or purlins. — *Holzbausanierung beim Bauen im Bestand* 3.2.1.1 and Tab. 3.1
  (a typology of built roofs, not a design rule).
- Typical: purlins, posts and rafters form a frame (Gebinde); the frames stand about 3.5 to
  4.5 m apart. — same book 5.4.4.
- Confirmed (DIN EN 1995-1-1/NA, NA.13.2): battens may be taken to brace rafters only with
  rafter spacing e ≤ 1.25 m, rafter width b ≥ 40 mm and depth h ≤ 4·b. — *Wendehorst
  Bautechnische Zahlentafeln* Tab. 12.24. An example build-up uses rafters 16/8 at a rafter
  spacing of 60 cm. — *Bausanierung* Abb. 10.1.

### S.2 Sections

- Preferred sections of structural solid timber (KVH, C24), width b: depths h in cm —
  6: 10/12/14/16/18/20/22/24; 8: 12/16/18/20/22/24; 10: 10/16/20/24; 12: 12/16/20/24;
  14: 14. — *Wendehorst Bautechnische Zahlentafeln* Tab. 12.111 (state 09/2015).
- Rule of thumb: sections of good static use have b/h = 1:2; squared timber has sides
  of at least 6 cm. — *Zahlentafeln für den Baubetrieb* 1.6.2 (p. 32).
- Typical: for insulation between and under the rafters choose a rafter depth of 16 to
  20 cm. — *Sanierung von baulichen Anlagen* 4.3.5.2.

### S.3 Defaults of this library for the purlin roof of a simple house

**Not from a book.** These are choices of this library, made so that a simple house can be
modelled at all where the literature gives a frame and no number. Tier T4, massing only:
any plan clause, product sheet, engineer's or carpenter's figure replaces them, and nothing
here is a design value.

- Rafter spacing 0.80 m: between the 60 cm of the example and the 1.25 m bracing limit of S.1.
- Rafter depth from the joist ratio of §2.3, rounded up in steps of 2 cm from 16 cm (the
  depths of the row of width 8 in S.2).
- Purlin of width 12 cm: depth from the glulam ratio of §2.3, at least 16 cm, rounded up in
  steps of 4 cm (the row of width 12 in S.2).
- Posts 12/12 cm and eaves plate (Fußpfette) 12/12 cm: a preferred section of S.2.
- Collar beams (Kehlbalken) under a ceiling to the loft (`building-planning-spatial` 3.4): one
  on every rafter, at the level of that ceiling, as wide as the rafters, the depth by the same
  rule as theirs over the span between the two slopes.
