---
name: simple-first-building
description: >
  GOVERNING skill of the library: the simple-first principle and its German civil-law
  machinery. Default every building decision to the simplest proven solution at the
  agreed standard tier; escalate complexity only on explicit client request. Owns the
  § 633 BGB three-step defect test, the implied promise of "allgemein anerkannte Regeln
  der Technik" (aarRdT), the DIN presumption and its rebuttal, lawful downward
  deviation ("Beschaffenheitsvereinbarung nach unten", Beweislast, insurance exclusion,
  Gleichwertigkeit/Unverhältnismäßigkeit), liability through the Kauf-/Miet-kette,
  Gebäudetyp E (BGB-Eckpunkte Nov 2025, what is/isn't relaxed, the public-vs-private
  trap), and the Bavaria/Hamburg/Schleswig-Holstein pilot standards with their numbers.
  Provides the complexity ladder every other skill defaults to and the contract
  checklist that makes "einfach bauen" legally survivable.
---

# Simple-First Building — Governing Principle & Civil-Law Machinery

> **This skill governs how every other skill in the library is applied.** Read it
> first in any new project. Its core rule: **the first design answer is the simplest
> proven one; demanding construction is an explicit, priced, documented decision —
> never a default.**

## 0. The two problems this skill solves

**(1) Cost/complexity drift.** German building is expensive partly because two
independent legal engines push standards upward without anyone deciding to:

- *Public law*: Landesbauordnungen + incorporated technical Baubestimmungen set
  growing requirements.
- *Civil law (the silent engine)*: BGH case law treats planners/contractors as
  **impliedly promising ("stillschweigend zugesichert")** the usual quality/comfort
  standard of comparable, contemporaneously completed buildings and the
  **allgemein anerkannten Regeln der Technik (aarRdT)** — so every designer plans
  defensively high to avoid later Haftungsvorwürfe ("lieber mit zu hohen Standards
  geplant"). Rising standards therefore = defensive over-engineering, embedded in
  private law, invisible to the client's budget conversation.

**(2) The mirror risk — "simplification ≠ safety collapse".** A design culture of
simplicity that quietly under-builds gets destroyed by the same machinery: an
aarRdT-deviation without proper agreement is an automatic Mangel even with zero
symptoms. This skill's job is to let simplicity be chosen **knowingly and
lawfully**, upward or downward, instead of either drifting up by default or
dropping down by accident.

**Timeline of the political answer (status knowledge — re-verify before use):**
2022 "Gebäudetyp e" initiative (Bayerische Architektenkammer; "e" = einfach/
experimentell) → 2024 Referentenentwurf → Nov 2024 "Gebäudetyp-E-Gesetz" draft
(BT-Drs. 20/13959) — failed with the end of the Wahlperiode → 05.05.2025 coalition
agreement safeguards Gebäudetyp E → **Nov 2025 BMJV + BMWSB "Gemeinsame Eckpunkte
Gebäudetyp E"** (civil-law amendments to the BGB Bauvertragsrecht; § 6 of D).
Legislative status must be checked current [VERIFY before relying].

---

## 1. THE COMPLEXITY LADDER — simple first, per discipline

### 1.1 The gate rule

For every design axis below, the library's default answer is **Level 0**.
Moving up a level requires **all three**:

1. an **explicit client wish** (named in the program of requirements / contract —
   not inferred from "quality expectations"),
2. a **cost and schedule impact statement** to the client before commitment
   (rough figures below; market-dependent [VERIFY per project]),
3. where the escalation changes structural physics, **a design review against the
   owning skill** (e.g. wide spans → `structural-systems`/`structural-analysis`).

Moving **down below the usual standard/aarRdT** requires the § 3 machinery
(documented downward Beschaffenheitsvereinbarung) — public-law permission is not
enough (§ 2.6 central trap).

### 1.2 Escalation axes, defaults and triggers

| # | Axis | Level 0 default (simple & proven) | Escalations (only on explicit wish) | Typical impact of leaving L0 | Owning skill for detail |
|---|---|---|---|---|---|
| A1 | Geometry | compact rectangle, one volume, gable or shed roof, no split levels | L/U shape, cantilevers, Kink, Staffel, split-level, Sonderform | each bend of the envelope ≈ +5–15 % KG300/400 (α = A/V worsens; see `building-physics` compactness bands) [VERIFY project] | `building-typology`, `construction-detailing` |
| A2 | Storeys/basement | Erdgeschoss + 1–2 OG on slab, no UG; Kellerverzicht as default question | full UG, partial UG with reduced ceiling, Tiefgarage | UG ≈ +300–600 €/m² NF vs. slab solution; Hamburg pilot: Verzicht on UG/Fassade/Aussenanlagen alone ≈ 1,000 €/m² (§ 6.2) | `geotechnics-foundations`, `cost-management-din276` |
| A3 | Structure | loadbearing masonry + precast or RC floor slabs on simple grid (spans ≈ 3.5–6.5 m), standard footings | wide spans, flat decks, point supports, long cantilevers, exposed concrete, timber hybrid on non-standard grid, special systems (Aussteifungskern variants beyond standard) | flat deck/cantilever premium on KG300–302 ≈ 10–30 % + detailing risk; every jump = full EC2/EC5/EC6 re-check | `structural-systems`, `concrete-detailing`, `masonry-construction`, `timber-steel-design` |
| A4 | Envelope | monolithic or masonry + WDVS, standard Putz surface | ventilated RVS, Naturstein, Sonderbeschichtungen, memory/special formats, double skin | RVS ≈ +80–200 €/m² WNF; specialisation raises both cost and execution-error surface (§ 1.4 "Komplexitätssteuer") | `construction-detailing`, `building-materials` |
| A5 | Roof | pitched, standard tile/small-form, simple geometry, no dormers | flat roof (+ strict DIN 18195/18531 regime), Gründach, Photovoltaik-Integration, Faltungen, Dachfenster instead of Gaupen | flat-roof build-up cost ≈ 1.5–2× pitched per m² and higher maintenance; every fold = detail + water risk | `roofing-waterproofing` |
| A6 | Openings | series-typical window sizes, standard turn-tilt, no special formats | large glass, Hebe-Schiebe, Sonderformen, brandabschnitte doors, special shading | lifting equipment + statik + Einbruch/Brandschutz consequences; U-Wert/Glas cost non-linear from ≈ 2.5 m width [VERIFY] | `openings-windows-doors` |
| A7 | Stairs/circulation | straight single-flight or standard U-flight, off-the-shelf landing | spindless winding, freitragend, Balustradensonderlösungen, Raumspartreppe | bespoke stairs ≈ 2–4× series price; every special statics case needs its own calc | `stairs-vertical-circulation` |
| A8 | Services (TGA) | heat pump + FBH (or simplest compliant heating per GEG), window ventilation, standard electrical per DIN 18015 | additional Lüftungsanlage (only where Schallschutz/BSK/airtightness logic demands it), Kälte, RWA beyond requirement, full AVS, smart building, dezentrale WL | each added system ≈ +1.5–4 % total cost + maintenance annuity; Bayern pilot ran WITHOUT Lüftung in multi-storey (§ 6.1) — proof of L0 feasibility with agreed comfort | `building-services-tga` |
| A9 | Comfort tiers (vereinbar!) | normaler Standard: DIN 4109-1 Mindestschallschutz, DIN 18040-2 (barrier-reduced where funding demands), standard room heights 2.50–2.70 m | erhöhter Schallschutz (Exec), gehobene Ausstattung, Raumhöhe ≥ 2.80, Wellness-/Sonderbereiche | tier choice = the FIRST cost lever; note the tier also re-anchors which aarRdT are owed (§ 2.3) | `building-acoustics`, `accessibility-universal-design` |
| A10 | Water/site | surface drainage to street per Satzung, standard versickerungsfrei | Retention/Zisterne, Schwammstadt-Bausteine, begrüntes Versickerungsmodell, grauwasser | each ≈ four- to five-figure € + Pflegevertrag; often B-Plan-driven (then not optional) | `construction-scheduling-site`, `building-regulations-permits` |
| A11 | Process/delivery | one-off craft execution, classical Hochbau plan | serielles Bauen/Typologie, **Typengenehmigung**, Taktplanung, BIM full-LoIN, AVP generalplanerisch | serialisation amortises the § 3 documentation effort across N objects; single-object = keep documentation lean | `construction-scheduling-site`, `bim-management` |

**Reading the ladder:** a "simple" house (EFH/DHH at L0 across all axes) is not a
lesser building — it is the compact rectangle on a slab, masonry + WDVS, tiled
gable roof, series windows, straight stairs, heat-pump + FBH, normal tier,
surface-drained, one-off delivery. **Every departure from that description is a
named, priced decision.** Put the ladder in the client conversation at
Leistungsphase 1–2, not at detail design.

### 1.3 Simplicity checks the ladder must pass

Before proposing L0, verify it is *actually* sufficient (function governs, § 2.2):

- site loads/water → `geotechnics-foundations` (a WU slab where groundwater demands
  it IS the simple solution; "schwarze Wanne" then needs § 3.6 machinery, not a shrug);
- span needs → `structural-systems` (L0 grid must fit the program; forcing L0
  geometry onto a program that needs spans manufactures complexity later at worse cost);
- fire/egress → `fire-protection-building` (Gebäudeklasse thresholds are hard
  gates: L0 MFH ≠ L0 EFH — GK 4/5 add second routes, Wände, Bekleidungsklassen);
- acoustics floor → `building-acoustics` (DIN 4109 minimum is aarRdT; anything
  below needs § 3 machinery);
- energy floor → current GEG requirements are law; "simple" never means "below GEG"
  unless the client accepts it as a *contracted tier statement* (see § 3, and note
  Typ-E proposals anchor exactly at the Länder Baubestimmungen).

### 1.4 Komplexitätssteuer — hidden cost of every extra level

Complexity taxes: more trades with mutual interfaces (Schnittstellen = where the
BGH sees coordination defects), more unique details = more abZ/Ingenieurtext
surface, longer coordination, higher execution-error probability, maintenance
annuity. Rule of thumb for client conversation: **each non-L0 axis multiplies the
number of failure-relevant junctions ≈ +1–3 per axis on top of the price delta.**
Process speed (Hamburg field 3: ≈ 400 €/m², § 6.2) is available to everyone
*without* touching standards — exhaust it before buying complexity.

### 1.5 When complexity pays — legitimate escalations

Escalation is right when L0 fails a hard constraint or the client's explicit
programme demands otherwise: poor soil + no UG (mat vs pile → `geotechnics`),
B-Plan wall-height/roof-band conflicts resolved by flat-roof variants,
Innenbereichsschutz noise forcing Lüftungsanlage instead of open windows
(`building-services-tga`), accessibility programme (DIN 18040-1 lifts), heritage
or city-representative façade. Document WHY (a one-paragraph Entwurfsbegründung
per escalated axis) — it is the cheapest liability insurance and the input for § 3.4 templates.

---

## 2. CIVIL-LAW DEFAULT MECHANICS — what "built simply" legally means

### 2.1 § 633 BGB three-step defect test

Mangel = Ist-Beschaffenheit negatively deviates from Soll-Beschaffenheit.
Assessment order (§ 633 Abs. 2 S. 2 BGB):

1. **vereinbarte Beschaffenheit** — express agreement dominates absolutely
   (including an agreed standard label: "einfach"/"normal"/"gehoben").
2. **Eignung für die nach dem Vertrag vorausgesetzte Verwendung** — fitness for
   the contractually presupposed purpose.
3. **gewöhnliche Verwendung + übliche Beschaffenheit** — ordinary-use fitness
   PLUS "quality the customer of works of the same kind can expect."

Interpretation via the whole contract body (BGH NJW 2012, 518); public
procurement = objective bidder view (BGH NZBau 2014, 185) and a silent LV may be
supplementally construed **against** the bidder (BGH NZBau 2002, 324).

### 2.2 The functional concept — why specs never exhaust duty

The contractor always owes a **working result** for the recognised purpose —
independently of wording. Bridge case (→ § 5.1): agreed Tragfähigkeit formally
met, contractor knows heavy vehicles will cross → Mangel despite spec-conformity.
Contractor's exit: advise, offer sufficient design against Nachtrag; if the
informed client insists → freed of liability to that extent. Compliance with
aarRdT does NOT immunise against the functional test (BGH NJW-RR 2011, 1240);
the two limbs coexist: *functionally deficient work = mangelhaft even if
DIN-perfect; aarRdT-deficient work = mangelhaft even if presently functional.*

### 2.3 aarRdT — the impliedly owed minimum

- **Definition** (OLG Hamm NZBau 2020, 29; consensus): technical rules for
  Entwurf/Ausführung that are (i) scientifically recognised ("wissenschaftliche
  Durchdringung"; no fundamental Meinungsstreit) AND (ii) proven in practice
  ("praktische Bewährung"), durchweg known among and accepted by the "Träger der
  Praxis". Exist even without a written rule (BGH NJW-RR 1995, 472); unwritten
  ones count (BGH NJW 2014, 620).
- **Gradient ladder:** aarRdT (scientifically accepted + proven — the civil
  minimum) < **Stand der Technik** (highest currently feasible; no proof needed)
  < **Stand von Wissenschaft und Technik** (newest science; e.g. § 7 Abs. 2 Nr. 3
  AtG). Only the middle floor is impliedly owed; higher floors only if expressly
  agreed.
- **Implied promise (BGH NJW 2013, 1226; NJW-RR 2011, 1240):** the customer may
  redlich expect the Qualitäts-/Komfortstandards of comparable, contemporaneously
  completed and accepted buildings; the contractor "sichert diesen Standard
  üblicherweise stillschweigend zu". Consequence in VII. Zivilsenat doctrine:
  **every deviation = Mangel, automatically.**
- **Tier relativity:** which aarRdT are owed follows the agreed/interpretable
  standard tier — "gehobener Standard" → its rules; "normaler Standard" →
  correspondingly (BGH NJW 1998, 2814; VII ZS BauR 2024, 1725, 1726). **The
  contractual tier label is therefore the first cost lever — choose it explicitly.**
- **Defect without damage:** mere deviation suffices — no symptoms needed.
  Schaufenster case: execution "das Risiko eines Schadens in sich birgt" = Mangel
  (BGH NJW 1981, 2801); confirmed OLG Stuttgart NJW-RR 2023, 1317
  (aarRdT breach + Schadensneigung = Mangel ohne Mangelsymptome). Durability
  proxies actionable (asphalt deck: ~16 y usual life; shortened = Mangel even if
  extent unquantifiable → § 5.3).
- **Systemic rationale:** warranty 5 y (§ 634a Abs. 1 Nr. 2 BGB) / 4 y
  (§ 13 Abs. 4 S. 1 VOB/B) vs > 60 y real service life — aarRdT compliance is the
  proxy that keeps buildings usable beyond the warranty window. A defect surfacing
  in year 10 is time-barred; the rules exist precisely to prevent year-7 disasters.
- **Timing:** decisive = state of aarRdT **at Abnahme**; mid-project rule changes
  shift the owed standard, contractor must instruct, client decides, adaptation
  earns Mehrvergütung (BGH NJW 2018, 391). Keep a rule-change radar on long projects.
- **BGB vs VOB/B:** VOB/B writes it down (§ 4 Abs. 2 Nr. 1 S. 2 — duty already
  during execution; § 13 Abs. 1 — defect definition includes aarRdT at Abnahme).
  Pure BGB has no express clause — yet aarRdT are owed identically via the
  implied promise. Cumulative minimum: agreed Beschaffenheit + function + aarRdT
  (tier-matched) + übliche Beschaffenheit of Zeitgebäude.
- **Critique noted for honesty:** some doctrine would limit the implied promise
  to safety standards (Standsicherheit, Brandschutz, Feuchteschutz, ggf. Schallschutz —
  Zöller 2024, 443 [IBR/BauR pages vary, VERIFY]); comfort vs safety may not be
  cleanly separable (BeckOK/Voit). Leupertz: Schallschutz and "Anzahl Steckdosen"
  are **verhandelbarer Komfortstandard** — "sollte vertraglich vereinbart werden",
  not litigated after the fact.

### 2.4 The DIN presumption — and its rebuttal

- Written vehicles that can carry aarRdT: DIN (incl. VOB Teil C), Einheiten
  Technische Baubestimmungen (ETB, via Institut für Bautechnik), VDI-Richtlinien,
  VDE, Flachdachrichtlinien. Scale: **> 3,300 private technical norms already in
  2015** (BMU/Baukostensenkungskommission) — unüberblickbar; this mass is itself
  the reason full downward deviation agreements are doctrinally "kaum rechtssicher
  darstellbar" (Popescu BauR 2024, 1585, 1589; Leupertz BauR 2025, 378).
- **Prevailing construction-law view:** widerlegliche Vermutung that DIN reflect
  aarRdT → breach of DIN → defect PRESUMED → with the implied promise this
  produces "DIN-Hörigkeit": over-satisfying feels safer than under-satisfying —
  the engine of defensive over-standardisation.
- **Foundation cases:** BGHZ 103, 338 (341 f.) — DIN are anerkannte Regeln;
  breach in excavation support → presumption of causation for neighbour damage
  (defendant must prove the damage would have occurred anyway — in tort the
  presumption doubles); OLG Hamm NJW-RR 1995, 17: "tatsächliche, jederzeit
  widerlegbare Vermutung", but the concept *übersteigt* DIN (DIN subordinate);
  OLG Brandenburg NJW-RR 2009, 1468: regional craft practice "im Norden" cannot
  remove the defect — not DIN-gerecht ⇒ aarRdT disregarded; client may demand
  "sichere Gewähr der Ordnungsmäßigkeit". DIN 820-1 (2022-12) Ziff. 8.1 self-describes:
  norms must first *establish themselves* as aarRdT; only sicherheitstechnische
  Festlegungen carry a concrete Vermutung of Fachgerechtigkeit.
- **THE SENATE CONFLICT:** the VII. Zivilsenat des BGH (competent for
  Werkvertrags-/Architektenrecht) states **no such Vermutung exists** — DIN are
  private "technische Regelungen mit Empfehlungscharakter" (Stellungnahme on the
  Typ-E draft, BauR 2024, 1725, 1727). Older presumption cases came from other
  senates/divisions and non-construction matters. Plan around the *worse* case
  (presumption alive) until legislation settles it.
- **Rebuttal evidence that worked:** OLG Hamm NZBau 2020, 29 — DIN 4109 sound
  values presumed aarRdT **but rebutted**: where wirtschaftlich akzeptable,
  aarRdT-conforming Bauweisen reach 63/67 dB, fixed private-rule Schalldämm-Maße
  are not aarRdT; sound requirements are "dynamisch". Newer softening:
  OLG Düsseldorf IBR 2025, 280 (Vermutung not "in allen Fällen"); OLG Brandenburg
  IBR 2026, 60 (rebutted where neither function nor appearance impaired);
  NJW 2024, 839 (no actionable breach without Gebrauchsnachteile). Critique of
  procedure: closed-door committee work, manufacturer capture (Ritter-Höll/Vogel
  BauR 2019, 1681 ff.; Steffen NJW-Spezial 2023, 492); 10. Deutscher
  Baugerichtstag (Mai 2025, Hamm; Thesen BauR 2025, 18 ff., AK V/VI) demands
  transparent standardisation.

### 2.5 Public-law permission ≠ civil-law compliance

> Compliance with aarRdT is owed "unabhängig davon, ob öffentlich-rechtlich
> geringere Anforderungen … gestellt werden" — a publicly permitted, usable
> building can still be mangelhaft (appellate ruling on § 13 Nr. 1 VOB/B (2006)
> in that tradition [court unnamed in material, VERIFY]).

This is the axis on which every "simple building" programme (Befreiungen,
pilot standards, Typ E) must be read: see § 4.5 central trap.

### 2.6 Defenses menu when an "einfach" build is attacked

Contractor/planner facing an aarRdT-based claim (in practice the only three exits):

1. prove an **effective downward Beschaffenheitsvereinbarung** (§ 3);
2. prove **Gleichwertigkeit** — execution achieves the functionally equivalent
   result by other means (the OLG Hamm 63/67 dB logic inverted: show the better
   or equal economical construction was used);
3. **Unverhältnismäßigkeit** of cure (§ 635 Abs. 3; BGH NJW-RR 2015, 1300;
   OLG Düsseldorf IBR 2021/3, 125) — a defense, never a design strategy.

---

## 3. DEVIATING DOWNWARD, LAWFULLY — the "Beschaffenheitsvereinbarung nach unten"

### 3.1 Doctrine

Downward deviation from (a) the übliche Qualitäts-/Komfortstandards of Zeitgebäude
and (b) the tier-matched aarRdT is **possible in principle** (VII ZS, BauR 2024,
1725, 1726) — the parties may agree it. But case law sets hurdles, for the client's
protection: the vehicle is a **rechtsgeschäftliche Risikoübernahme** — a
"besondere Absprache" (BGH NJW 1984, 2457), termed "Beschaffenheitsvereinbarung
nach unten" (Langen/Berger/Dauner-Lieb/Langen § 633 Rn. 83).

### 3.2 Cumulative validity requirements

1. **Disclose the usual standard** — what would be owed WITHOUT the deviation,
   in concrete, not abstract, terms.
2. **Disclose the concrete deviation** — what will actually be built instead.
3. **Make it understandable to a layperson** — "Fachkunde" cannot be presumed;
   to a client without it the deviation must be MADE understandable
   (BGH NJW 2018, 391); full disclosure of Unsuitability + ensuing disadvantages
   (OLG Brandenburg NJW 2024, 839); client must grasp "vollständige Tragweite".
4. **Express, unambiguous agreement** — "ausdrücklich und eindeutig", not from
   fine print, not by silence; the deviation itself must be the named,
   negotiated object.
5. **Client consent provable** — Unterschrift or zustimmende E-Mail (Textform);
   the contractor bears the **Beweislast** for the agreement
   (OLG Hamm NJW-RR 1995, 17 → he must plead and prove it).

### 3.3 What courts rejected (study these — they are how projects die)

- **"Einschalige Haustrennwand" in the Baubeschreibung** of terraced houses sold
  to lay buyers: no effective deviation — buyers could not deduce without
  Fachkunde that aarRdT Schallschutz is missed (BGHZ 181, 225 [230] = NJW 2009, 2439).
- **Express 40 mm stair-stringer dimension**, below aarRdT: even an explicit
  DIMENSION is not an agreement to fall below the owed minimum when its
  significance was never pointed out (BGH NJW 2013, 1226).
- **DIN references / dB figures / "Schallschutzfenster gewünscht?"** — none can
  describe usual vs lower standard to a layperson (OLG Saarbrücken NJW-RR 2021, 149).
  Binding descriptions contrast **perceptual experience**: what one hears —
  conversations, music, footsteps, from which direction, whether "in Ruhe wohnen"
  is possible (BGH NJW 2009, 2439).
- **Regional market practice** ("im Norden macht man das so") — irrelevant
  against the presumption chain (NJW-RR 1995, 17; NJW-RR 2009, 1468).
- **Bloße Kenntnis** of the risk — not enough; for risky/non-permittable
  planning even the client's known willingness needs "eingehende und umfassende
  Beratung über das Risiko" + agreement (BGH NJW 2013, 3442; OLG Celle NJW 2024, 2542).
- **Limit of the limits:** the true minima for Standsicherheit, Brandschutz,
  Feuchteschutz, (a Schallschutz-Minimum) are **seriously doubtful to be waivable
  at all** without destroying function (Zöller 2024, 443 [VERIFY locus]) — and the
  functional concept (§ 2.2) binds regardless. Realistic deviation fields: comfort
  tiers, execution choices with preserved end-function (e.g. black vs white tub),
  above-GEG energy levels, Untergeschosse, Fassade, Außenanlagen, "sicherheitstechnische
  Anlagen" as in Bayern pilots — each per-case.

### 3.4 Documentation architecture (what actually works)

- **Entscheidungsvorlagen** per deviation: usual/aarRdT solution + est. cost →
  chosen deviating solution + est. saving → consequences/risks incl. the
  durability horizon that is NOT guaranteed → client's signed decision reference.
  Make them **Vertragsbestandteil**.
- **Präambel** in planner + construction contract: project to be built simpler/
  cost-efficiently, deviation from übliche standards INTENDED — necessary but not
  sufficient alone (the per-item documents do the work).
- **Explicit tier definition** ("einfacher Standard"/label) — imports the tier's
  aarRdT as the minimum (BGH NJW 1998, 2814). Today's-law approximation of Typ E:
  anchor the owed minimum **by reference to the applicable technical
  Baubestimmungen of the Land** — already possible without the new statute.
- **Model scripts** — Feuchteschutz: "Due to site soil conditions only a
  WU-Konstruktion meets the aarRdT ⇒ building should stay tight for its whole
  life ⇒ cost X. Alternative Bitumenabdichtung ⇒ estimated saving Y ⇒ risk: not
  tight for whole life; moisture damage possible after [stated horizon]."
  Schallschutz: "Comparable recent buildings achieve [usual level]; you would hear
  [list]. Our option achieves [level]; you would hear [list]. Cost difference:
  [X]. Do you want the lower standard?" — client signs.
- **No universal recipe** — the more areas deviate, the harder the naming duty
  gets (you must name the aarRdT you leave); **limit deviations to überschaubare
  Bereiche** (Popescu). Residual litigation risk never reaches zero; exhaustiveness
  is the only de-risker — and Privatautonomie ("geschlossene Verträge gelten")
  is real too.
- **Serialisation amortises documentation:** one deviation-legal documentation →
  Typengenehmigung/serielles Bauen → reused across N objects (§ 1.2 A11).
- **HOAI trap:** lowering standard lowers anrechenbare Kosten → fee can FALL
  despite extra advisory effort (advising deviations is often NOT a Besondere
  Leistung). Fix contractually: effort-mirroring fee or synergy pricing after the
  first object; ask "ab wann lohnt das?" per project size.
- **Early executor involvement** (analogue Last Planner): cheaper alternative
  designs must survive the ausführende Gewerk's veto — involve them in planning,
  not on site.

### 3.5 Insurance — before, not after

Berufshaftpflicht (AVB BHV) typically **excludes** damage from "bewusst gesetz-,
vorschrifts- oder sonst pflichtwidriges Verhalten" (cf. OLG Hamm BauR 2007, 1290)
→ deliberate deviation can equal an uninsured gap. **Action rule: written carrier
position BEFORE the deviation decision meeting.** This step is non-optional.

### 3.6 Worked example of a VALID design (the black-tub model)

Cellar where aarRdT demand "weiße Wanne"; parties want "schwarze Wanne". Holds if
(i) the intended use "trockener Keller" is **initially secured**, (ii) contractor
comprehensively instructs — black tub **not proven** for this Wasserlastfall,
dryness over **50–60 y** not ensurable — and (iii) client **expressly agrees**.
Then "one can hardly construe an implied promise of the white tub". Counter-case
(F.2, Leupertz): black tub chosen WITHOUT agreement, cellar dry after 4.5 y →
still MANGEL; costly remediation owed; sole defense Unverhältnismäßigkeit —
because dryness must hold 45–55 more years and year-7 dampness would be
time-barred. **The risk horizon, not the symptom, is the measure.**

---

## 4. GEBÄUDETYP E — legislative vehicle & assessment

### 4.1 Vehicle

NOT a Musterbauordnung/LBO provision: the Typ-E route amends **civil law** —
BGB Bauvertragsrecht (failed GebT-E-Gesetz Nov 2024, BT-Drs. 20/13959; Eckpunkte
Nov 2025). Design: a new opt-in contract type **"Gebäudetyp E-Vertrag"** alongside
Bauvertrag/Verbraucherbauvertrag/Architekten- und Ingenieurvertrag/Bauträgervertrag
in Werkvertragsrecht, **anchored to the technical Baubestimmungen der Länder**.
Without the express Typ-E agreement, the previous default machinery (§§ 2–3 above)
applies unchanged.

### 4.2 The Gemeinsame Eckpunkte (Nov 2025), itemised

1. Statutory provisions for the new "Gebäudetyp E".
2. Express opt-in contract type; without it, previous law stays.
3. Under Typ E only an **"einfacher Standard"** is owed:
   - areas covered by the Land's technical Baubestimmungen → owed minimum = only
     the aarRdT **embedded in those Baubestimmungen**; deviations from the
     Baubestimmungen no longer automatic Mangel, admitted where the LBO admits a
     **"gleichwertige Lösung"**;
   - content NOT covered by Baubestimmungen (quality/comfort) → "einfacher
     Standard" = "einen Standard, mit dem beim kostenreduzierten und einfachen
     Bauen vom 'üblichen Standard' nach unten abgewichen wird … bestimmte
     Ausstattungs- und Komfortmerkmale reduziert …, wobei die zeitgemäße
     Gebrauchstauglichkeit sichergestellt bleibt" — only its tier-matched aarRdT
     are owed.
4. Deviation from aarRdT allowed where no risk to **dauerhafte
   Gebrauchstauglichkeit** (Gleichwertigkeit principle).
5. **Aufklärung:** contractor must explain the MEANING of the Typ-E contract —
   esp. that only "einfacher Standard" is owed; general instruction suffices vs
   Unternehmern; **vs Verbrauchern: Textform** incl. consequences + risks.
6. **Cost advantage shown in general terms** (überschlägiger Schätzwert).
7. **Downstream information:** later Kauf-/Mietvertrags-partners must be informed
   the building was made only to the Baubestimmungen-minimum / "einfacher Standard".
8. **DIN clarification by statute:** DIN are private technical rules with
   recommendation character, not legal norms; **no per-se Vermutung** of
   reflecting aarRdT — it must be found per rule whether aarRdT are reflected.

### 4.3 What is / is NOT relaxed

**Relaxed (if Typ E chosen):** the civil minimum in Baubestimmungen-covered
areas; non-covered comfort → tier-matched "einfacher Standard"; deviations with
Gleichwertigkeit; the DIN presumption killed by statute.
**NOT relaxed:** the public-law minima themselves (Typ E is a civil contract
type; its Baubestimmungen deviation gate runs through the LBO's own
"gleichwertige Lösung" admission); zeitgemäße/dauerhafte Gebrauchstauglichkeit;
the safety core (Standsicherheit/Brandschutz/Feuchteschutz/Schallschutz-minimum)
via function concept + LBO; everything if the contract is not chosen. No
Bauregelliste/A-Liste/abZ or Feuerlöscheinrichtung specifics appear in the
material — do not attribute any.

### 4.4 Assessment (doctrinal, with the critique currents)

- Consistent with VII ZS position (no DIN Vermutung, deviation possible) and
  with criticism lines (Leupertz BauR 2025, 365; Schettler NZBau 2024, 587;
  Baureis/Dressel IBR 2024 [VERIFY pages]; Rehbein PrivBauR-HdB § 15 Rn. 106a).
- **Critique:** a dedicated new contract type cuts against the BGB's idea of
  abstract, generally applicable rules; must first be "filled with life" by
  practice/courts — doubtful contribution to Rechtssicherheit. Points 3–7 largely
  **restate today's law** (anchoring Baubestimmungen as owed minimum, disclosure
  incl. onward chain — already possible). No tangible relief visible on the
  actually-painful Aufklärungspflichten — templates/aids for the instruction and
  for Beschaffenheitsvereinbarungen would help more (plus real Normgebungsverfahren
  transparency). Mere buyer/tenant INFORMATION (point 7) vs the negative-
  Beschaffenheitsvereinbarung case law = fragil [own note: the statute would need
  to override that line explicitly]. Point 8 "sinnvoll" but not requiring
  legislation per VII ZS.

### 4.5 THE CENTRAL TRAP (memorise)

**Public-law easing ≠ private-law relief.** Befreiungen/reduced pilot standards
make the building *permitted*; they do not make a sub-standard build
*vereinbart*. A publicly approved building remains zivilrechtlich mangelhaft when
it misses the implied aarRdT/Zeitgebäude standard (§ 2.5; F.13 — even a missing
Baugenehmigung is itself a Sachmangel at the sale tier, BGH NJW 2013, 2182).
Typ E attacks the PRIVATE side — opt-in only, simpler-standard only, disclosure
hurdles only partly eased. Therefore: **every simplification decision lives twice
— in the Baugenehmigungsakte AND in the contract text; only the second one
deters the warranty claim.**

---

## 5. LIABILITY CHAIN — Werk → Kauf → Miete

### 5.1 Delivery chain (Werkvertragsrecht recap for routing)

- Remedies ladder once Mangel: § 634 menu → § 635 Nacherfüllung (contractor
  chooses repair/new; bears costs; may refuse as unverhältnismäßig) → § 636
  Rücktritt/Schadensersatz after Fristsetzung (or dispensable/failed/unreasonable)
  → § 637 Selbstvornahme + Kostenvorschuss → § 638 Minderung.
- Planner/overseer liability: § 650q Abs. 2 BGB applies the Bauvertragsrecht
  machinery to Architekten-/Ingenieurverträge → Planungsfehler = Haftung; a
  planning error realised in construction = zugleich Baumangel.
- Gesamtschuld client↔architect↔contractor (§ 426: client elects either; internal
  Ausgleich/Regress); § 650t: supervising architect may refuse damages where the
  executing contractor is also liable and no Nacherfüllung-Frist has failed yet.
- Bauträger: §§ 631 ff. apply to Errichtung/Umbau (§ 650u Abs. 1 S. 2).
- Limitations: buildings 5 y (§ 634a Abs. 1 Nr. 2 BGB) / VOB/B 4 y
  (§ 13 Abs. 4 S. 1) — vs > 60 y life (the asymmetry driving everything).

### 5.2 Kaufvertrag (selling the result)

§§ 433/434 BGB mirror § 633 (2022 reform): agreed Beschaffenheit → presupposed
use → ordinary use + übliche Beschaffenheit by **vernünftiger Durchschnittskäufer**
view at contract conclusion, incl. public statements/advertising
(BeckOK/Faust § 434 Rn. 75; MüKo/Maultzsch § 434 Rn. 56). Condo: buyer may
expect the Beschaffenheit of equal, simultaneous units. Missing Baugenehmigung =
regularly Sachmangel of sold WEG (BGH NJW 2013, 2182). Compliance with usual
standards AND aarRdT belongs to expectable Beschaffenheit of housing (LG Köln
IBRRS 2023, 2844). Downward deviation from **objective** requirements toward
consumers = **negative Beschaffenheitsvereinbarung**, "verschärfte formelle"
prerequisites: **"vor Vertragsschluss von der konkreten Abweichung eigens in
Kenntnis gesetzt und gesondert zugestimmt"**. § 476 I 1: seller cannot rely on a
liability limitation agreed before defect notification — the negative agreement,
not the waiver clause, is the instrument. **The Bauherr who accepted a reduced
standard upstream must replicate the same instruction + consent downstream, or
the "simplified" building re-emerges as his own defect liability.**

### 5.3 Mietvertrag (renting the result)

§ 535 Abs. 1 S. 1, 2 BGB: grant + KEEP use-fit condition. § 536 Abs. 1: Mangel →
Miete gemindert/befreit ("unerheblich" excepted). Without party agreement, the
"zum vertragsgemäßen Gebrauch geeignete Zustand" = standard of comparable
Wohnungen — Alter/Ausstattung/Art/Miete/Ortssitte — and **"Gibt es … technische
Normen, ist jedenfalls deren Einhaltung geschuldet … grundsätzlich der bei
Errichtung des Gebäudes geltende Maßstab"** (settled BGH Wohnraummietrecht line:
NZM 2004, 736; NZM 2009, 855; NZM 2010, 618; NZM 2012, 611; NZM 2013, 575;
NZM 2014, 163; NZM 2017, 256; NJW 2005, 218; NJW 2009, 2441). Trittschall: DIN
applicable at **Ausbau** deemed contract content (NJW 2005, 218; NJW 1998, 2814).
**The one favourable limit:** it is NOT material that at construction time
elevated insulation beyond DIN 4109 was technically easily possible — the
construction-law "higher possible standard" case law is NOT transferable to
tenancy (BGH NZBau 2010, 701). Downward deviation in the tenancy contract:
possible only "eindeutig" with tenant's declared Einverständnis (NJW 2004, 3174;
NZM 2010, 356); transparency bar same as elsewhere; **absolute hard limit
§ 536 Abs. 4: no advance waiver/exclusion of the Minderung rights to the tenant's
detriment** — only the owed STANDARD itself may be transparently fixed.
Rent-reduction losses caused by Baumängel within the construction warranty
window = Mangelfolgeschaden the landlord can pass through to contractor/planner.

### 5.4 Who bears what, for a deliberately lowered standard

| Actor | Bears | Mitigation |
|---|---|---|
| Contractor/planner | Beweislast for the downward agreement; Gesamtschuld (§§ 426, 650t); insurance exclusion for deliberate rule-breaking | § 3.4 decision templates signed as Vertragsbestandteil; § 3.5 carrier sign-off; Gleichwertigkeit evidence file |
| Bauherr/developer | residual standard risk if documents fail; downstream Kauf-/Miet exposure | replicate instruction + consent at every sale/lease (negative Beschaffenheitsvereinbarung; eindeutige Zustandsvereinbarung) |
| Buyer | reduced reality only after eigens informed + gesondert consented | — (consumer-side protection is the doctrine) |
| Tenant | nothing below owed standard unless eindeutige condition clause; § 536 IV floor intact | — |

**Net:** explicit, replicated contractual documentation is the ONE protective
instrument across the whole chain — it converts "simplified" from defect into
agreed condition at every tier.

---

## 6. FALLBEISPIELE — the 24 cases as a lessons table

| # | Case (court) | Facts → holding | Lesson for the ladder |
|---|---|---|---|
| F.1 | Bridge rating (Fallbeispiel 1.1) | agreed Tragfähigkeit + known heavy vehicles → Mangel despite spec | specs never exhaust function duty; advise-or-upgrade |
| F.2 | schwarze vs weiße Wanne (Leupertz) | dry after 4.5 y → still Mangel; remediation owed; Unverhältnismäßigkeit sole defense | risk horizon, not symptoms; documentation = only clean exit |
| F.3 | Asphalt deck (BGH [VERIFY cite]) | ~16 y usual life; aarRdT breach → "Gebrauchstauglichkeit gemindert", extent open | durability proxies actionable without quantified damage |
| F.4 | Schaufenster/Regelwasser (NJW 1981, 2801; Stuttgart NJW-RR 2023, 1317) | risk-bearing execution = Mangel; need not wait for damage | risk-embedded design = present defect from Abnahme |
| F.5 | einschalige Haustrennwand (BGHZ 181, 225) | technical wording in Baubeschreibung ≠ instruction to lay buyers | describe what will be HEARD, not what is built |
| F.6 | 40 mm Treppenwange (NJW 2013, 1226) | express dimension ≠ agreement to drop standard | the STANDARD, not the measurement, must be the negotiated object |
| F.7 | Schallschutz communication (NJW 2009, 2439; Saarbrücken NJW-RR 2021, 149) | DIN/dB/Schallschutzfenster-question all insufficient; lay perception governs | instruction contrasts usual vs reduced in perceptual terms, both directions |
| F.8 | DIN 4109 rebutted (OLG Hamm NZBau 2020, 29) | 63/67 dB economically attainable → presumption rebutted | norms are evidence, not verdicts — attack AND shield |
| F.9 | "im Norden" roof trade (NJW-RR 1995, 17; 2009, 1468) | regional practice loses to presumption chain | market custom ≠ defence |
| F.10 | Baugrube→Neuschaden (BGHZ 103, 338) | DIN breach → presumption of causation in tort | presumption doubles outside contract law |
| F.11 | Spielgeräte (NJW 1987, 2222; DIN 7926-1/18034) | voluntary DIN concretize Verkehrssicherungspflichten | simplification re-enters via third-party duties |
| F.12 | Sanierung/DIN-gerecht (Werner/Pastor line) | proper management only if DIN-gerecht | owners/managers inherit the chain |
| F.13 | missing Baugenehmigung (NJW 2013, 2182) | public-law shortcut → Sachmangel at sale tier | approvals ≠ private compliance |
| F.14 | tender silence (NZBau 2014, 185; 2002, 324; Celle VPR 2022/1) | bidder view; LV construed against drafter | simple scope must be WRITTEN |
| F.15 | tier relativity (NJW 1998, 2814; VII ZS BauR 2024, 1725) | owed aarRdT follow agreed tier | tier label = first cost lever |
| F.16 | mid-project rule change (NJW 2018, 391) | Abnahme state governs; instruct; Mehrvergütung | regulatory calendar = priceable joint decision |
| F.17 | risky/non-permittable takeover (NJW 2013, 3442; Celle NJW 2024, 2542) | bloße Kenntnis ≠ Einwilligung; extensive Beratung + agreement required | draft deviation agreements against the strictest template |
| F.18 | Unverhältnismäßigkeit valve (NJW-RR 2015, 1300; Düsseldorf IBR 2021/3, 125) | harmless deviations → cure disproportionate | defense, not strategy |
| F.19 | presumption softening (Düsseldorf IBR 2025, 280; Brandenburg IBR 2026, 60; NJW 2024, 839) | not "in allen Fällen"; no functional/optical harm → rebutted | harmless small deviations increasingly survive |
| F.20 | insurance exclusion (Hamm BauR 2007, 1290; AVB BHV) | deliberate rule-breaking uninsured | carrier sign-off BEFORE decision |
| F.21 | "Das große kleine Haus" (Bayern) | ≈ 4,000 m² BGF coop; B-Plan-Befreiungen, Holzhybrid, reduced Schallschutz, no Lüftung, no sicherheitstechnische Anlagen, re-used steel; ≤ 200,000 € Holzbau-Förderung | public-law path already delivers real simple building; civil tier still needs § 3/§ 4 machinery |
| F.22 | "Haus fast ohne Heizung" (Ingolstadt) | first completed/occupied Bayern pilot, near-zero heating | energy-standard reduction pilot-provable |
| F.23 | Hamburg-Standard numbers | ≈ ⅓ ≈ 2,000 €/m² (KG 200–700) via 39 standard levers ≤ 600 + Verzicht UG/Fassade/Außenanlagen ≤ 1,000 + Prozesse ≤ 400; nothing above GEG energy | big levers are programmatic, pre-validated; speed is real but smaller |
| F.24 | SH Regelstandard Erleichtertes Bauen | ARGE e.V. (Mitteilungsblatt 263, 2024): ≤ 25 % in Konstruktion + technischer Ausbau, WITHIN valid norms, funding-anchored | define the tier → tier-matched aarRdT are what's owed |

---

## 7. PILOT STANDARDS IN NUMBERS (the proof of concept)

### 7.1 Bayern — "Gebäudetyp-e" Modellvorhaben

- Driver: Bauwirtschaft crisis (costs, bureaucracy, falling project numbers);
  goals: explore requirement leeway, cut bureaucracy, generate industry knowledge
  (Bayerisches StMB 2025).
- Flagship F.21 (above). Pipeline: 3 further pilots building; first occupied:
  F.22; **19 pilots scientifically monitored**; public buildings included
  (Ellis-Kaut-Grundschule Germering — first school project; findings feed future
  economical/sustainable school builds).
- Lessons: Befreiungen vom B-Plan are used deliberately (geometry), material
  reuse (Stahlbauteile) and comfort reductions (Schallschutz, no Lüftung) are the
  real cost levers; subsidy stack works (Holzbau-Förderprogramm ≤ 200 k €).

### 7.2 Hamburg-Standard — Initiative "kostenreduziertes Bauen"

- Headline: **cost reduction up to one third — ≈ 2,000 €/m² brutto Wohnfläche in
  KG 200–700** shown possible; systematic analysis, plausibilised + monetarily
  evaluated by external scientific assessors.
- Three Handlungsfelder: (1) kostenreduzierende Baustandards — 39 identified
  simplification options across Baukonstruktion, Gebäudetechnik, Barrierefreiheit,
  Schall-/Brandschutz, ≤ ≈ 600 €/m²; (2) Verzicht/Vereinfachung selected
  technical/structural requirements — Untergeschosse, Fassadengestaltung,
  Außenanlagen — ≤ ≈ 1,000 €/m²; (3) Planung-/Genehmigungsprozesse — early
  planning, fewer Schnittstellen, delay avoidance — ≤ ≈ 400 €/m².
  (4th position: energetische Anforderungen — forgo standards ABOVE GEG; policy rec.)
- Continuous process: current results = baseline for reducing valid standards in
  affordable rental new-build. [Not in material: Hamburg-specific dB/storey/
  Stellplatz values — do not fabricate.]

### 7.3 Schleswig-Holstein — "Regelstandard Erleichtertes Bauen"

- Author: Arbeitsgemeinschaft für zeitgemäßes Bauen e.V. ("ARGE e.V."),
  interdisciplinary (housing companies, planners, industry, science, public hand);
  Regelstandard published in ARGE e.V. Mitteilungsblatt Nr. 263 (2024).
- Concept: conscious reduction of bauliche/technische/ausstattungsbezogene
  Anforderungen for cost-optimised building WITHOUT undercutting Sicherheit,
  Gebrauchstauglichkeit, Dauerhaftigkeit, Wohnqualität.
- Hook: defines the **förderfähige Maßnahmen of sozialen Wohnraumförderung SH** —
  economical implementation ON THE BASIS OF VALID norms (compliant reduction, not
  norm suspension).
- Numbers: consistent application → up to **25 %** savings esp. in
  Bauwerkskonstruktion and technischer Ausbau vs previous common practice, plus
  lower resource use/GHG. [Not in material: ErprobungsVO/storey caps/€/m² — none.]

**Pilot meta-lesson:** all three ride public-law/funding-level simplification;
none touches the civil default — which is exactly why § 3 documentation remains
mandatory for private projects, and why Typ E's civil anchoring matters.

---

## 8. WORKING THE LIBRARY WITH THIS SKILL

### 8.1 Routing order for every project

1. **Set the tier + the ladder profile with the client** (this skill § 1): which
   axes at L0, which explicitly escalated, which deviation machinery needed (§ 3).
   Output: two-page **Komplexitäts- und Standardvereinbarung** → Vertragsbestandteil.
2. Plan with all other skills **at that tier**: e.g. `building-typology` chooses
   type within L0 geometry logic; `structural-systems` picks the L0 system unless
   A3 escalated; `construction-detailing` draws the ordinary details first;
   `building-services-tga` sizes the minimal compliant system.
3. **Pre-submission audit** against § 2/§ 3: every below-usual item has a signed
   Entscheidungsvorlage; every above-GEG/DIN item has a signed "why".
4. `bim-management` carries tier + deviations as data (BIM property set
   `Standard- und Komplexitätsvereinbarung`, deviation log); `construction-freecad-bim`
   models L0 members unless the escalated axis is signed.
5. Downstream replication at every Kauf/Miet tier (§ 5.2/§ 5.3).

### 8.2 Per-skill "simple first" implications (the escalation map)

- `building-planning-spatial` / `building-typology`: L0 = compact, regular;
  typological Sonderformen are escalations with α/Ψ penalties priced.
- `structural-systems` / `structural-analysis` / `concrete-detailing` /
  `masonry-construction` / `timber-steel-design`: L0 = loadbearing walls +
  standard decks; every system jump triggers the full check chain, never a
  detail-library copy from an escalated project.
- `geotechnics-foundations`: "no basement" is the simplest foundation; a WU
  slab is still L0 where groundwater demands — function first (§ 1.3).
- `building-physics-thermal-moisture` / `building-acoustics` / `fire-protection-building`:
  law/GEG/LBO floors are hard; above-floor comfort (Ersschallschutz,
  comfortlüftung) is escalation territory; below-floor is § 3 territory.
- `construction-detailing` / `roofing-waterproofing` / `openings-windows-doors` /
  `stairs-vertical-circulation`: L0 = standard detail library of the trade;
  every unique detail = complexity tax (§ 1.4) + § 3 machinery if below aarRdT.
- `building-services-tga`: L0 = minimal compliant system set; "sicherheitstechnische
  Anlagen" beyond requirement are escalations (Bayern proof).
- `accessibility-universal-design`: DIN 18040-1 programme = explicit client
  decision; 18040-2/barrier-reduced = L0 where funding demands.
- `sustainable-construction`: sufficiency (reducing demand: size, storeys,
  systems) IS the simplest sustainability lever — ladder aligns with
  "Vermeidung vor Optimierung"; GEG-over-standard (EH40/55) = escalation decision.
- `construction-scheduling-site` / `bim-management`: L0 delivery = classical;
  serial/Typengenehmigung/Takt = escalations that PAY when they amortise § 3.4
  documentation across objects.
- `cost-management-din276` / `building-regulations-permits`: tier profile feeds KG
  budgets; pilot numbers (§ 7) as cost-reduction evidence for the client decision;
  permit strategy = public layer only (§ 4.5 trap).
- `existing-structures-retrofit`: simplest option = leave what works untouched
  (Nachrechnung per its own tier rules); every "make it new" is escalation.
- `construction-freecad-bim`: model gate — a non-L0 object needs the signed
  escalation reference in its name/property, else it is a design defect in the
  data, not just the drawing.
- `construction-drawing-sketching`: draw L0 first; escalate the drawing only when
  the decision is made.

### 8.3 Pre-planning checklist (condensed)

- [ ] Standard tier chosen and NAMED (label) — § 2.3 tier relativity.
- [ ] Ladder profile per § 1.2: L0 default; every escalation listed with reason +
      price/schedule impact.
- [ ] Deviation list: below-usual items only where § 3.3 limits respected
      (Standsicherheit/Brandschutz/Feuchteschutz/function are off the table).
- [ ] Insurance carrier position obtained BEFORE deviation decisions (§ 3.5).
- [ ] Entscheidungsvorlagen drafted per deviation (§ 3.4 templates) → signature.
- [ ] HOAI/fee effect of tier reduction solved contractually (§ 3.4).
- [ ] Rule-change radar + Abnahme-date logic understood (§ 2.3 timing).
- [ ] Downstream: sale/lease templates carry the replicated instruction clauses (§ 5).
- [ ] Public-law route checked AND known to be insufficient alone (§ 4.5).
- [ ] Serialisation/Typengenehmigung considered when ≥ 2 similar objects (§ 3.4).

### 8.4 Reality check

This skill is **planning and contract-practice knowledge, not legal advice and
not construction-law counsel.** Statutes/case law change; state law (BauO der
Länder, introduced Baubestimmungen) differs; the VII-ZS-vs-h.M. conflict on the
DIN presumption is live until a statute settles it; Typ-E legislation is
**pending per the Nov 2025 status of this skill [VERIFY before every project].**
A deliberately simplified project MUST be walked through with a lawyer specialising
in Bauvertragsrecht + the Berufshaftpflicht carrier before signing deviation
agreements — the § 3 hurdles are individually fatal when missed, and no template
(including this skill's) guarantees enforceability (Beweislast on the contractor).

### 8.5 Evidentiary tiers used here

- **T1 law/case-law anchors:** §§ 633/634/635/636/637/638/634a/650q/650t/650u/
  426/433/434/476/535/536 BGB; § 4 Abs. 2 Nr. 1 S. 2, § 13 Abs. 1/4 VOB/B; BGH
  decisions as cited; DIN 820-1; ETB/Baubestimmungen anchoring — quoted/paraphrased
  from the doctrinal record, current text prevails.
- **T2 settled doctrine:** aarRdT definition, tier relativity, presumption
  controversy, pilot programme facts (public sources, 2024–2026 publications).
- **T3 [VERIFY]:** every cost-delta percentage/€ in § 1 and § 7 (market- and
  location-dependent), the pending legislative status, citation-year variants the
  material flags, and Zöller/Baureis loci. Never quote § 1 deltas as market
  figures; re-price per project via `cost-management-din276`.

### 8.6 Glossary (terms of art, retained German)

"aarRdT" — allgemein anerkannte Regeln der Technik (scientific recognition +
practical proof). "Stand der Technik" / "Stand von Wissenschaft und Technik" —
higher floors, express agreement required. "Beschaffenheitsvereinbarung (nach
unten)" / "negative Beschaffenheitsvereinbarung" — downward deviation agreement
(construction/sales). "funktionaler Mangelbegriff" — purpose-failure defect limb.
"Abnahme" — acceptance, pins the owed standard date. "stillschweigende Zusage" —
implied promise (BGH's vehicle). "rechtsgeschäftliche Risikoübernahme" — the
agreed risk shift. "Gleichwertigkeit" — equal-value deviation gateway.
"Beweislast" — contractor bears it for the deviation. "AVB BHV" — insurance
conditions excluding deliberate rule-breaking. "technische Baubestimmungen der
Länder"/ETB — administrative incorporated rules; Typ E's anchoring layer.
"Befreiung" — public-law waiver (necessary, never sufficient).
"Typengenehmigung"/"serielles Bauen" — the documentation-amortising delivery
models. "Gebäudetyp E"/"einfacher Standard" — the proposed opt-in contract type
and its owed tier.

---

## 9. KEY-NUMBERS REGISTER (memorisation block)

- Warranty: **5 y** BGB buildings / **4 y** VOB/B; building life **> 60 y** —
  the asymmetry behind aarRdT doctrine; black-tub: dry at 4.5 y = still Mangel;
  dampness in y 7 escapes liability; required dryness horizon 45–55 y.
- Norm mass: **> 3,300** private technical DIN/VDI/etc. (2015, BMU).
- Sound rebuttal values: DIN 4109 presumption REBUTTED where **63/67 dB**
  economically attainable (OLG Hamm NZBau 2020, 29).
- Failed-agreement classics: 40 mm stringer; "einschalige Haustrennwand" clause.
- Hamburg: ≈ **⅓ ≈ 2,000 €/m²** (KG 200–700) = 600 (39 levers) + 1,000
  (UG/Fassade/Aussenanlagen) + 400 (Prozesse) €/m²; energy: nothing above GEG.
- SH: **≤ 25 %** (Konstruktion + technischer Ausbau), ARGE e.V. MBl. **263/2024**,
  within valid law via Wohnraumförderung.
- Bayern: flagship **≈ 4,000 m² BGF**, subsidy **≤ 200 k €**, **19** monitored
  pilots (1 occupied, 3 under construction at material date).
- Legislation: RefE 2024 · BT-Drs. **20/13959** Nov 2024 (failed) ·
  Koalitionsvertrag **05.05.2025** · Eckpunkte **11/2025**.
- Limitation of waivers: § 476 I 1 BGB (sale), § 536 IV BGB (tenancy).
- Senate conflict: VII ZS (BauR 2024, 1725): **no DIN Vermutung** — vs h.M.
  construction-law view (widerlegliche Vermutung).
