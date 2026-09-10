---
name: building-regulations-permits
description: >
  Baurecht & Genehmigung workflow for residential construction in Germany
  (framework portable to DACH with per-country VERIFY): public building law
  two-tier model — Bauleitplanung (Flächennutzungsplan → Bebauungsplan) and the
  BauGB admissibility norms (§30 plan-conforming, §31 Ausnahmen/Befreiungen,
  §34 intra ursem / §35 extra ursem concepts; VERIFY current wording per Land);
  B-Plan reading checklist (Art der Nutzung, GRZ/GFZ/OWZ, Bauweise, Zahl der
  Vollgeschosse, Wand-/Firsthöhe, überbaubare Flächen, Sondergebiete, textliche
  Festsetzungen); Bauvorlagen & procedure types (Baugenehmigungs-, vereinfachtes,
  Anzeigeverfahren, Genehmigungsfreistellung — conceptual, VERIFY by Bundesland);
  Bauvorlageberechtigung and the signature chain (Entwurfsverfasser, Tragwerksplaner,
  Brandschutznachweisberechtigte, Prüfstatik — Bundesland differences); the
  technical-requirement web (MBO → LBO → Technische Baubestimmungen / Bauregelliste
  A/B/C; DIN/EN/Eurocode+NA becoming "allgemein anerkannte Regeln der Technik";
  GEG energy duties incl. Energieausweis/EWS checks, Landesenergiegesetze,
  DIN 4109 / 18040 / TA Lärm status); Nachweispaket structure (which plans and
  calculations accompany which submission); private building law quick map (BGB
  Werkvertrag, VOB/B if wholly contracted, Abnahme effects, §634a Verjährung 5 y,
  Abschlagszahlungen, Sicherheiten/Einbehalt); HOAI Leistungsphasen 1–9 as service
  framework with fee logic (anrechenbare Kosten, Honorarzonen, verhandelbar since
  ECJ 2019 — VERIFY); insurance/liability role map; tendering (VOB/A vs BGB/VgV
  Vergabe, application types, BIM contract per VDI 2552 AIA/BAP, ISO 19650);
  Abweichungen/Ausnahmen/Befreiungen; neighbor law (Abstandsflächen formula
  family a = 0.4·H / min 3 m MBO pattern, roof add-on, privileged projections,
  Grenzbebauung, Baulasten — VERIFY per Bundesland); typical agent failure
  patterns (quoting superseded EnEV values as law, treating DIN as binding
  without Bauregelliste/introduction status, mixing Bundesländer) and a
  "how to answer regulatory questions" playbook with checklists. Produces
  planning envelopes and submission-readiness checklists, NOT approvals.
---

# Building Regulations & Permits — Germany (DACH-Portable Framework)

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

Germany does not have one building rulebook either — it has **four stacks of law that answer four different questions**, and almost every regulatory error in German residential work comes from confusing them. *Was darf ich hier bauen?* (what may I build here) is answered by planning law (BauGB + the parcel's Bebauungsplan, or §34/§35 BauGB where there is none). *Wie muss ich es bauen?* (how must I build it) is answered by public building law proper — the state building code (Landesbauordnung, LBO) of the **specific Bundesland**, plus the technical rules introduced through it. *Wann muss ich wofür welchen Nachweis führen und wer darf unterschreiben?* is answered by the Verfahren and Vorlage rules of that same LBO — which differ meaningfully from state to state. *Was schulde ich wem, wann und bis wann?* is private law: BGB Werkvertragsrecht, plus VOB/B only if it was actually and wholly contracted. The Musterbauordnung (MBO) that everyone cites is a **model, not law** — no citizen is ever judged against the MBO itself, only against the LBO that (mostly) follows it, in whichever variant that Land chose. Austria adds a further complication: there is no federal building code at all — Bauordnungsrecht is purely Landessache (nine different Bauordnungen), plus flat-law and Bautechnik rules; Switzerland decides at cantonal and municipal level (Bau- und Zonenordnungen, Baubewilligungsdekret). This skill models all four stacks, keeps them cited separately, walks the German submission lifecycle from B-Plan read to completion, and gives the routing protocol for Austria and Switzerland — but its numeric baseline is Germany, and every Bundesland-specific figure carries a VERIFY tag because state law changes more often than this document is revised.

## Reality Check — Licensing & Liability

**This skill produces design envelopes, regulatory navigation aids and submission-readiness checklists for planning and FreeCAD modeling ONLY.**

- Nothing produced with this skill — no buildable-envelope calculation, no B-Plan reading, no Abstandsfläche figure, no Nachweis list, no FreeCAD model, no drawing exported from one — is a construction document, a permit application, or an approval.
- A building project in Germany requires a **Baugenehmigung** (or a documented Freistellung/Anzeige where the state code exempts it) **before** construction starts, and the drawings must be prepared and signed by persons who hold the relevant **Bauvorlageberechtigung** (entry in the state Architects'/Engineers' Chamber list). Building without the required permit exposes the owner to a Baustopp (construction stop), orders to demolish or regularize, loss of insurance coverage, and refusal of utility connections.
- The agent **must never** present FreeCAD output, envelope calculations, or any figure from this skill as construction-ready, permit-ready, submission-ready, or "genehmigungsfähig" without that human sign-off.
- If a user appears to treat output as final — "can I hand this to the builder", "so we're approved", "is this genehmigungsfähig?" — **say so unprompted, in that turn, before answering anything else**: *"This is a planning envelope, not a permit. A vorlageberechtigter Entwurfsverfasser has to prepare and sign the submission, the Tragwerksplaner the statics, and the untere Bauaufsichtsbehörde has to issue the Baugenehmigung before anyone breaks ground."*
- **Never certify.** Do not produce anything resembling a Unterschriftsblock, a Prüfsachverständigen-Feststellung, a Brandschutznachweis, a Energieausweis, or an engineer's certificate. Never place an architect's name, Kammer-Registrierungsnummer, Prüfingenieur number or signature on output. An Energieausweis in particular may only be issued by persons with the specific GEG §88 drawing entitlement — never by a design aid.
- **The law changes; the edition matters.** Every figure here names its statute (MBO §, BauGB §, BauNVO §, GEG, DIN number). Before quoting any of them to a user as current, state the statute, the version this skill assumes, and that the current text and the specific Bundesland's variant must be verified. Superseded law (EnEV, old HOAI fee bindings, pre-2018 Werkvertragsrecht, DIN 4109:2002) quoted as current is a defect generator.
- **Never invent a number to be helpful.** A fabricated GRZ or a guessed 3-m setback becomes a rejected application or a neighbour's Widerspruch. "That figure is in the parcel's B-Plan text / the Land's LBO § — here is how to read it" is a correct and complete answer.

---

## Section 0: Fast Path — If You Read Nothing Else

```
1. Which of the FOUR questions is being asked?
   "Darf ich das hier bauen?" ............ Bauplanungsrecht: B-Plan (§30 BauGB) or §34/§35. → §3, §4
   "Wie muss ich es bauen?" .............. Bauordnungsrecht: LBO of THIS Bundesland + introduced rules. → §5–§8
   "Wer unterschreibt, was reichen wir ein?" Verfahren + Bauvorlagen + Berechtigungen. → §5, §6, §9
   "Was schuldet wem bis wann?" ........... Privates Baurecht: BGB, VOB/B nur wenn vereinbart. → §12, §13
2. ALWAYS establish before quoting ANY number:
      (a) Bundesland (Bauordnungen, Verfahren, Freistellung, Prüfstatik, Abstandsflächen all differ),
      (b) the parcel's own governing plan (B-Plan nr. + version, else §34/§35),
      (c) the edition/year of the rule being quoted.
   If any is unknown, say WHICH answers are blocked on it. Do not pick a plausible default.
3. The MBO is a model, never the binding text. Cite it only as "MBO-Muster; Landesrecht
   prüfen — VERIFY". Never say "laut MBO müssen Sie..." as if it were law.
4. A DIN is binding only if (a) introduced as Technische Baubestimmung in this Land,
   (b) referenced by a Zulassung/abP, or (c) it states the allgemein anerkannten Regeln
   der Technik. Otherwise it is a recognized technical reference, not law. Say which
   case applies. → §7
5. Never quote EnEV (withdrawn 2021→GEG), HOAI Mindestsätze (EUGH 2019 → fees negotiable),
   or BauNVO numbers from memory as current law. EnEV-era U-values in a 2020s answer =
   the single most common AI regulatory failure. → §18
6. Abstandsflächen and B-Plan setbacks are TWO independent tests; both must pass.
   The stricter controls. A B-Plan that allows Grenzbebauung does NOT delete the LBO
   requirement — it satisfies it (§6 Abs. 1 Nr. 1 MBO pattern). → §11
7. Every answer ends with the gate: chamber-registered designer signs, building permit
   (or documented exemption) exists, then — not before — construction starts.
```

---

## Section 1: Evidentiary Tiers — How a Technical Rule Becomes Binding in Germany

The single most important methodology fact about German construction regulation: **"DIN" and "law" are different things, and the distance between them is crossed by a named legal act.** Knowing which tier a number sits in is more useful than knowing the number.

| Tier | Label | How it binds | Examples | Failure mode when confused |
|---|---|---|---|---|
| **T0** | **Parliamentary statute** | Directly, as cited (federal) | BauGB, BGB, Bauleitpläne as Satzung, GEG, VOB as *contracted* terms never as law | Citing "the Bauordnung" without naming which Land's |
| **T1** | **Parcel-specific binding plan** | The B-Plan (or örtliche Bauvorschrift, Erhaltungssatzung, Veränderungssperre) binds this plot like a statute (Satzung) | GRZ, GFZ, Vollgeschosse, Wandhöhe, Bauweise, Baufenster, textliche Festsetzungen | Quoting a "typical" GRZ as if it were the parcel's |
| **T2** | **State building code** | LBO of the Bundesland; the MBO only as its model | Abstandsflächen §5/§6 (numbering differs), Verfahren, Vorlageberechtigung, Gebäudeklassen | Applying Bayern's rule in NRW, or citing the MBO itself |
| **T3** | **Introduced technical rules (Technische Baubestimmungen)** | LBO §83-type clause + the Land's Verwaltungsvorschrift "Liste der Technischen Baubestimmungen" | Introduced DIN 4109, 4108, Eurocodes with national annex, MVV TB, MIndBauRL-type RLs | "DIN says so" — without checking whether *this Land* introduced *this edition* |
| **T4** | **General type approval / product rules** | allgemeine bauartenehmigung, Zulassung, CE per EU construction-products regulation + Bauregelliste A/B/C | Fenster mit abP, WDVS-Zulassungen, DIBt listings | Treating a Z-approval as valid nationally without expiry check |
| **T5** | **Allgemein anerkannte Regeln der Technik (aRdT)** | Catch-all clause in LBOs and in private law (§13 VOB/B / §633 BGB "übliche Beschaffenheit"); proven practice, not necessarily a published norm | VOB/C ATVs, WTA-Merkblätter, Fachregeln des ZVDH | Either extreme: "no norm → no obligation" OR "every DIN is aRdT" |
| **T6** | **Contract-agreed standard above law** | Only by agreement; higher market standards are NOT public-law minima | VDI 4100 sound classes, DEGA certificate, QNG sustainability level, KfW standard | Presenting the statutory acoustic minimum as what a buyer may expect (or vice versa) |

### 1.1 The three-step test for any technical number

```
Question: "Is [requirement R] legally binding for this project?"
  Step 1 — Is R in the LBO or a Rechtsverordnung of THIS Land?        → directly binding. T2
  Step 2 — Is the norm containing R introduced as Technische Baubestimmung
           in THIS Land, at THIS edition? (Liste der Technischen Baubestimmungen)
           → binding as public-law minimum, usually with transition periods. T3
           OR covered by abP/Zulassung/Bauregelliste reference?            → binding for that product. T4
  Step 3 — If not introduced: is it an allgemein anerkannte Regel der Technik
           (established in science/practice, generally applied)?
           → binding via the catch-all clauses and via contract law (BGB/VOB),
             with the date that matters being the time of Abnahme (BGH case law) —
             NOT via public building law. T5
  If none apply: R is best practice or marketing. Quote it as such. T6
```

**Worked contrast (memorize this pattern, not the numbers):** DIN 4109 (Schallschutz) is introduced in the LBO states as the public-law *minimum* between foreign usage units — but the Federal Court of Justice (BGH, 2009) held that the DIN 4109 minimum is **not** what a higher-standard new-build sale contract owes: "gehobene/zeitgemäße Ausstattung" wording pulls the contractual duty toward VDI 4100/DEGA levels. Same norm, two answers, because tier ≠ tier. Any answer about sound, fire behaviour classes, or barrier-free design that does not separate public-law tier from contract tier is incomplete.

### 1.2 Mandatory first questions before any number

1. **Bundesland** — decides LBO, Verfahren type, Freistellung existence, Prüfstatik duty, Abstandsflächen formula parameters, Nachbarbeteiligung, Kammer laws, Landesenergiegesetz.
2. **Community and parcel** — which B-Plan (name, Nr., date of Ausfertigung/Bekanntmachung) or §34/§35 status; local statutes (Stellplatz-, Erhaltungssatzung; Gestaltungssatzung).
3. **Building class and use** — Gebäudeklasse (GK) per the state list in §5.2; residential vs mixed vs Sondergebiet.
4. **New build vs existing** — Bestandsschutz vs new requirements (GEG existing-building duties, Abstandsflächen of the existing state, change of use).
5. **Date/edition** — of the rule being quoted. State it.

If any is unknown, say explicitly *which numbers are blocked on it* rather than picking a plausible default. **Never answer a regulatory question with a single number and no statute name.**

---

## Section 2: The Routing Map — Which Law Answers Which Question

### 2.1 The institutional stack

| | Bauplanungsrecht | Bauordnungsrecht | Technische Regeln | Privates Baurecht |
|---|---|---|---|---|
| **Question** | Ob und was gebaut werden darf (if, what, where on the plot in planning terms) | Wie gebaut werden darf (safety, order, usability of the structure) | Mit welchen nachweisbaren Eigenschaften (how to prove compliance technically) | Wer was wann zahlt/leistet (contract, payment, defects) |
| **Primary texts** | BauGB, BauNVO; the parcel's B-Plan | MBO (model) → LBO of the Land + Landesbauverordnungen (Verfahren, Vorlagen, Gebäudeklassen, Abstandsflächen variant) | Liste der Technischen Baubestimmungen (VV), MVV TB, Bauregelliste A/B/C, DIN/EN/Eurocodes+NA, Zulassungen/abP, VOB/C ATVs | BGB §§631, 650a–650v; VOB/B if wholly contracted; HOAI framework; VgV/VOB/A for public clients |
| **Does it set GRZ/GFZ?** | **YES — exclusively** (B-Plan) | No | No | No |
| **Does it set Abstandsflächen?** | Indirectly (can fix Baugrenzen; Grenzbebauung permission) | **YES — the LBO, per Land** | Fire-rule distances to boundaries (harte Bedachung etc.) | Private Grenzabstände (Nachbarrechtsgesetze) separately |
| **Does it set U-values?** | No | No | **GEG + introduced DIN 4107/4108/EN ISO 13789 family** | No |
| **Who enforces** | Gemeinde / Bauaufsicht at Baugenehmigung | Bauaufsichtsbehörde (Untere Bauaufsicht), im Bestand partly Ordnungsamt | Same, via the Nachweise in the submission + Prüfstatik/Brandschutz review | Civil courts; Schieds-/Gutachterkommissionen der Architektenkammern; VOB: none automatically |
| **Typical confusion error** | "The B-Plan allows it, so the house is legal" | "The LBO decides what I may build here" (it doesn't decide *use*) | "This DIN is the law" / "this DIN is optional" | "VOB/B applies anyway, it's standard" |

### 2.2 The routing decision tree

```
Question arrives
  ├─ About ALLOWABILITY / use / density (was darf ich bauen, wie viel, wofür)?
  │     → B-Plan exists?  YES → §30 BauGB test against every Festsetzung (§4 reading list)
  │                       NO  → within Ortsdurchfahrt/built-up? §34 (type & measure from the
  │                             nähere Umgebung — a DERIVED envelope, see §3.5)
  │                             else §35 (outside settlement: privileged uses only)
  │     → conflicts of two rules? Both apply; stricter governs. No averaging.
  ├─ About the BUILDING itself (rooms, stairs, heights inside, fire, sound, energy, barrier)?
  │     → LBO of the named Bundesland → §3 of that state's list of introduced technical rules
  │     → buildings/systems beyond the standard LBO concept → Sonderbau RLs (Versammlungsstätten,
  │       Gaststätten, Verkaufsstätten, Hochhaus, Garagen, IndBauRL, SchulBauRL...) VERIFY trigger.
  ├─ About PROCEDURE (genehmigungspflichtig? Freistellung? Anzeige? Wer unterschreibt? Fristen?)
  │     → §5 (procedures), §6 (who signs), §9 (document package). ALL state-specific — VERIFY.
  ├─ About a DEVIATION (zu hoch, zu dicht, Grenzüberschreitung, Zweckentfremdung)?
  │     → §10: Abweichung (LBO) vs Ausnahme/Befreiung (B-Plan) — different doors, different tests.
  ├─ About COSTS/FEES/SERVICES of planners?
  │     → §13 HOAI framework (LPH 1–9, anrechenbare Kosten, negotiability after ECJ 2019).
  ├─ About CONTRACT/PAYMENT/DEFECTS with a builder?
  │     → §12 private law map, then to a lawyer for anything contested. This skill maps, not advises.
  ├─ About TENDERING by a public client?
  │     → §15 VOB/A vs VgV, application types, BIM contract documents.
  └─ Austria / Switzerland?
        → §11.6: same four questions, different institutions (Länder-Bauordnungen AT;
          Kantone/Zonenreglemente + Baubewilligung CH). Re-route; keep the tiers.
```

---

## Section 3: Public Building Law, Tier A — Bauleitplanung and BauGB Admissibility

### 3.1 The two-tier land-use plan chain

```
Raumordnung (Bund/Land) — space-planning guidelines, bind the tiers below
        │
Flächennutzungsplan (FNP) — Flächennutzungsplan, municipality-wide,
        │                 preparatory: shows the intended use of the whole territory
        │                 (Wohnbauflächen, gemischte, Gewerbe, Grün, Verkehrsflächen...).
        │                 Binds the administration, NOT the citizen. No one obtains a
        │                 building right from the FNP; but it is the Entwicklungsmaßstab
        │                 for the B-Plan (§§1, 8, 12–13 BauGB concepts — VERIFY procedure).
        ▼
Bebauungsplan (B-Plan) — a bylaw (Rechtsverordnung/Satzung). It binds every parcel in its
        │              scope directly, like a statute. Simple plans for inward development
        │              and Vorhaben- und Erschließungspläne (BauGB §9/§12/§13a family) can
        │              be drafted without an FNP change ("dem FNP darf nicht
        │              widersprechen" softening — VERIFY current text).
        ▼
Baugenehmigung — checks the individual project against the B-Plan (and everything else).
```

**Practical consequences that agents get wrong:**

- The FNP is not citable as "what may be built on this plot" — only the B-Plan (or §34/§35) is. If the only evidence is an FNP colour swatch, the answer is *blocked*, not "Wohnbaufläche means you can build".
- A B-Plan can be **vorhabenbezogen** (VBeB-Plan, §12 BauGB): the plan exists *for* one project, with a feasibility/extraction agreement (Durchführungsvertrag) and often project-specific overridings — read the contract family, not just the plan.
- A **B-Plan can be invalid** (unwirksam — procedural defect, stale) without anyone having said so; then §34 applies instead. Invalidation happens via the norm-control route (Normenkontrolle OVG) or incidentally. Never design on the assumption that either "valid" or "invalid" is certain — flag and route to counsel when the plan's age or an open challenge is material.
- **Satzungstypen beyond the B-Plan** bind the same way once validly enacted: örtliche Bauvorschriften (Landesrecht, e.g. Gestaltungs-/Abweichungssatzungen), Erhaltungssatzungen (change-permit for demolition/modernization), Veränderungssperre (freezes planning for up to ~2 years, extendable — VERIFY), Stellplatzsatzungen, Entwässerungssatzungen, Gestaltungssatzungen mit PV-/Materialgrenzen (the energy-vs-design conflict is real — see §8.3).

### 3.2 The admissibility norms (concepts — VERIFY against current BauGB text)

| Norm | Situation | Test | Agent's job |
|---|---|---|---|
| **§30 BauGB** | Qualified B-Plan exists | Project is *zulässig* if it meets the Festsetzungen (type, measure, site, construction method) and does not conflict with other public requirements; plus Erschließung gesichert (connected or assured) | Full §4 plan read; every Festsetzung checked one by one |
| **§30(2) "einfacher" B-Plan** | Plan without full §9(1) Nr. 16–23 Festsetzungs catalog | Admissibility = not contradicting the rule contents it does have; remainder falls back to §34 logic | State which parts came from the plan and which derived |
| **§31(1) Ausnahme** | Plan reserves "Ausnahmen sind zulässig" | Authority discretion at the municipality's seat; only if exception's conditions met and compatibility retained | Do not design *on* an Ausnahme unless the reservation is visibly in the plan text |
| **§31(2) Befreiung** | Conflict with a Festsetzung | Discretionary; only where individual circumstances + public interests (incl. plan intent) permit — "planrelevante Belange" may not simply be set aside | Never present a Befreiung as a fix for an avoidable breach; a design that only passes via Befreiung is a rejected design waiting to happen |
| **§34(1) intra ursem** | inside a built-up district, no plan | Zulässig if it fits the *Eigenart der näheren Umgebung* in Art (usage type by BauNVO analogy) + Maß (building's nature/size/closure) + Bauweise, and Erschließung gesichert | Derive envelope by measurement — §3.5 |
| **§34(2)+(3)** | within a B-Plan's area outside its scope / Lückenschluss | B-Plan-adjacent infill, Befreiungen easier | Rare; flag as §34(3)-territory, VERIFY |
| **§35 extra ursem** | outside the settlement | Privileged uses (landwirtschaft, Gartenbaubetrieb, supply/disposal facilities, energy, power lines, public tasks, research...) are privilegiert if no public interests oppose and Erschließung gesichert; other uses are only "ermessen" where no Träger öffentlicher Belange objections — a single-house plot that is not privileged is **not** buildable in Germany | First question for any rural plot: is it §35? If yes and the use is not privileged, the answer is BLOCKED, full stop. |
| **§36/§37** | Mitwirkung/ Einvernehmen Gemeinde-vs-Behörde | procedural — matters for timing, not design | Mention in the timeline answer only |

**Hard rule:** §34 has no numbers. Any §34 answer must name *which neighbouring parcels* supply the reference (type, Vollgeschosse count, GRZ/GFZ of that stretch, Bauweise) — "the area looks like two storeys" is not a derivation. The comparison group is the *nähere Umgebung*, not the postcode, and a row of detached bungalows does not entitle you to infer four storeys.

### 3.3 Erschließung — the gate people forget

Admissibility in §30/§34/§35 all require that Erschließung (access + utilities) is *gesichert*. In German practice this gates on:

1. **Herstellung der Erschließungsanlagen or rechtliche Absicherung** (Erschließungsbeitragsrecht BauGB §§123 ff. — VERIFY; many communities demand payment/assurance before or alongside the permit),
2. **Entwässerung** (public sewer connection & contribution statute; where none: retention/ Versickerung per local statute or water authority — rainwater and blackwater separately),
3. **access** (public street or secured private way — the latter needs an actual, registrable right of way (Grunddienstbarkeit/ Nießbrauch/ personal) and its survival across resale),
4. for large/industrial uses: **Immission side** (TA Lärm / BImSchV — §8.2) as a check that the neighbouring use doesn't exclude the dwelling and vice versa.

A plot that is *theoretically* B-Plan-conforming but where Erschließung is unpaid/unsecured is a blocked answer, not a "yes, but".

### 3.4 Change of use (Nutzungsänderung)

Converting a barn, office or retail unit to living, or a unit to two units, is a **genehmigungspflichtige Nutzungsänderung** in most states (and in a B-Plan can breach the Festsetzung even if the fabric is untouched). Checks: planning permission (usage type, number of WE if capped), LBO requirements for the new usage (retention, second escape route, sound, smoke alarms, parking per Stellplatzsatzung), existing-building GEG duties, Immission conflicts (living next to its own permitted commercial noise = TA Lärm problem from the *inward* direction). Never assume "no construction work → no procedure".

### 3.5 Worked derivation — the §34 method (placeholders, never parcel truth)

```
SITE: no B-Plan; street strip "Am Sande" inside the Ortslage; state = needs VERIFY
DERIVE (what a planner actually does — do not simulate the conclusion):
  1. Define the Eigenart of the *unified* neighbouring development — which
     buildings visibly, durably characterise the strip (usually a side of the
     street + opposite frontage), excluding: §35 fringe, Temp Bauten, buildings
     whose use already breaks the character, planned/never-built.
  2. Record for each: usage type (BauNVO category by function, not name),
     GFZ/GRZ by measurement, Zahl der Vollgeschosse, Bauweise (offen/geschlossen),
     roof type if held by local practice, First-/Traufhöhe range.
  3. The permissible Maß is the *mittlerer* range of the reference strip; the
     project must "passen" (fit) — it may not push the ensemble to its ceiling.
  4. Erschließung check (§3.3) + Immission check (noise from the adjacent
     commercial row → TA Lärm, §8.2).
  5. Document the derivation (photos, plan mark-ups, measurement table).
     The Bauaufsicht will ask "which parcels give your number?" — that table IS
     the application's §34 argument.
BLOCKED without items 1–4: the answer is a method, never "usually 2 storeys".
```

---

## Section 4: B-Plan Reading Checklist — Extracting the Envelope

The B-Plan's text part (textliche Festsetzungen) is where the binding numbers live; the coloured plan part (Zeichenteil, usually 1:500/1:1000) is where their *geometry* lives (Baufenster, Grenzen, Sondergebiete). Read both against this checklist, quote Festsetzung numbers verbatim into the project record, and mark every figure not actually read from *this* parcel's plan as **T1-V placeholder — VERIFY**. Many plans are published as **XPlanung** data (machine-readable plans via WFS/geo-portal), and planning practice increasingly starts from the Liegenschaftskataster extract in ETRS89/UTM — where available, that beats reading a scanned PDF, but the official satzungsmäßiger text governs over any GIS copy.

### 4.1 The reading order and what each item controls

| # | Festsetzung | What it really controls | Trap |
|---|---|---|---|
| 1 | **Art der baulichen Nutzung** (WA, WR, WD; MI, MK, MU, M, CM, GE… BauNVO) | which *uses* are zulässig | "WA" may still allow small shops under §14/§15 BauNVO (Ausnahmen); MU vs MK differ in residential permission ratio; **Sondergebiete** (§11 BauNVO — e.g. Wohnen, "Urbanes Gebiet" MA after 2017 — VERIFY the Land/BauNVO edition) follow their plan-defined purpose, not the generic catalog |
| 2 | **GRZ** (Grundflächenzahl) | max *unversiegelte Grundfläche-related coverage*: sum of footprints (incl. garages, sometimes paths — read the plan's definition!) ÷ parcel area | Car ports, garden sheds, terraces may or may not count — the plan or §19(4) BauNVO (Anrechnungsregeln) decides; counting wrong is the classic rejected application |
| 3 | **GFZ** (Geschossflächenzahl) | max total floor area (per state measurement rules — GRZ/GFZ calculation rules come from §20 BauNVO: floor area of *all* Vollgeschosse, rules for DCH etc. — VERIFY current edition) | GFZ, not Wohnfläche; attic floors with low ceiling heights may still be Vollgeschosse (see item 6) |
| 4 | **Zahl der Vollgeschosse / OWZ** (the "open/OG count" notation is plan-specific; read the legend) | storey *count* via the legal Vollgeschoss definition (a floor whose covering lies more than half above the natural/average terrain = Vollgeschoss — the exact LBO/BauNVO §20 definition governs, VERIFY) | "2,5" notations, staffelbare GK, "Zahl der Vollgeschosse als Zulässigkeitsobergrenze vs Mindestanteil" — the plan chooses max or min! |
| 5 | **Wandhöhe / Firsthöhe / Dachform / Dachneigung** | max height of external wall (definition per plan!) and ridge; sometimes prescribed roof pitch band, tile colour/type | Wandhöhe ≠ building height ≠ Firsthöhe — three different datums; a Gestaltungssatzung can prescribe roof covering so tightly that PV is restricted (§8.3 conflict) |
| 6 | **Bauweise** (offen / offen mit Bebauung mit Gruppen u. Hausgruppen / geschlossen / Grenzbauweise) | detachment, wall on boundary, row/twin combinations | "Open with single/double houses" still permits twin = Grenzbebauung; a closed-structure Festsetzung can *compel* boundary walls |
| 7 | **Überbaubare Flächen: Baufenster / Baugrenze / Linie** | where on the plot the building may sit | Everything *outside* the Baufenster needs a Befreiung (except §23 BauNVO-privileged minor parts, VERIFY); a building line (Baugrenze) is stricter than the Abstandsflächen line — both must pass (§11.2) |
| 8 | **textliche Festsetzungen of the second rank** | Stellplatz rules if plan-based (else Satzung), Fahrrad-Stellplätze, Bäume/Festsetzungen to planting, Zisternen, "Dachbegrünungspflicht", Schallschutzauflagen (active/passive allocation per noise map), Überschwemmungs-/Hochwasserschutz, Abweichungssatzungen, Höchstzahl der Wohneinheiten, Größe der Wohnungen | A WE-cap or min-size Festsetzung kills investor plans; noise-allocation Festsetzungen dictate window order (acoustic skill `building-acoustics`) |
| 9 | **Flächen/ Linien (Zeichenteil)** | Verkehrsfläche, Grünfläche, public-use area, leitungsrecht, Vorrangfläche | A street-widening reservation can push the *real* building line behind the parcel boundary — same trap as the building line everywhere |
| 10 | **Hinweise vs Festsetzungen** | the plan's notes text that is *not* binding (e.g. "Hinweis auf Baulasten") | Never design to a "Hinweis"; never ignore it either (it warns you where to look) |

### 4.2 The envelope arithmetic the plan forces (all three tests, every time)

```
A_plot        = parcel area (amtlicher Lageplan / Liegenschaftskataster, NOT tape measure)
GRZ-test      : Σ footprints (per plan's definition)          ≤ GRZ·A_plot
GFZ-test      : Σ floor areas (Vollgeschosse per §20 BauNVO)  ≤ GFZ·A_plot
Height-test   : Wandhöhe ≤ plan max  AND  Firsthöhe ≤ plan max
                AND  Zahl der VG ≤ plan max          (three separate ceilings)
Site-test     : every part of the building inside Baufenster (boolean, §20 of this doc)
                AND every LBO Abstandsfläche satisfied (§11)   ← two independent tests
Use-test      : usage (incl. home office, guest suites, units) inside the
                Art-der-Nutzung permission; WE count inside caps.
Erschließung  : §3.3 gate.
```

Run **coverage and floor-area as separate tests** — the classic rejection is a plan that clears GRZ at 45% and blows GFZ because a third floor was added "since the footprint still fits". The two caps bind in different geometries; which one bites first is a fact about the plan, not a guess.

---

## Section 5: Bauordnungsrecht and the Procedure — Which Track, Which Documents

### 5.1 The four procedure tracks (concepts — every Land varies; VERIFY)

| Track | German name | Typical trigger | What the authority examines | Notes |
|---|---|---|---|---|
| Full permit | **Baugenehmigungsverfahren** | anything not covered by a lighter track; larger/complex projects; Sonderbau | completeness + public-law conformity, discretionary parts | longest; Nachbarbeteiligung differs by Land (some: objections possible; some: none for conforming infill) |
| Simplified | **vereinfachtes Baugenehmigungsverfahren** | most normal residential within a B-Plan or §34 area in many Länder | limited check: essentially §30/§34 conformity, Abweichungen, *not* a full individual review of all technical safety (responsibility shifts to the signatures) | where it exists, the *Entwurfsverfasser carries more liability* — that is the deal |
| Exemption-with-notification | **Genehmigungsfreistellung** ("Freistellungsverfahren") | small residential (typically GK1–2 houses) inside a qualified B-Plan, meeting the Festsetzungen, in several Länder (e.g. the classic "Typenhaus-/EFH-Freistellung" family) | no permit issued; instead a filed dossier + municipal objection window (often four weeks); builds *lawfully only if* all conditions genuinely met (B-Plan conformity, LBO standard compliance, no area of statutes that disable it) | the trap: Freistellung ≠ "anything goes" — the project must independently satisfy the full LBO + GEG without an authority ever checking it; and one changed dimension (extra storey, terrace into the setback) can destroy the prerequisites retroactively |
| Notification | **Anzeigeverfahren** | defined small structures (typ. small garages, car ports, some fences/walls up to a height, small GK1 annexes — the catalogue is the Land's, VERIFY) | authority may still order compliance/conditions within a period | "anzeigepflichtig, nicht genehmigungsfrei" — silence ≠ approval everywhere |

Below all four sits the **verfahrensfrei/genehmigungsfrei catalogue** (small structures by size/height per LBO list — e.g. garden sheds within stated footprint/height, fences under a state height (often 2 m in built areas, higher outside — VERIFY each Land)). Two permanent traps: (a) verfahrensfrei never means *rule*-free — the LBO, B-Plan, Gestaltungs-/Erhaltungssatzung, tree statutes and Abstandsflächen all still bind, a change-of-use approval can still be owed, and in Baudenkmäler/denkmalgeschützten Anlagen nearly everything is permit-bearing again; (b) the *combined* building can cross the threshold even if each part alone would not.

### 5.2 Gebäudeklassen — the master switch of the LBO

German residential fire/egress/structural law mostly does **not** argue in dwelling counts; it argues in **Gebäudeklassen (GK 1–5)** defined by the *height of the topmost occupied floor's upper edge above the average natural ground level* + floor area of usage units + storeys. MBO pattern (adopted near-identically by most Länder — VERIFY the specific LBO and its current edition):

| GK | Pattern (MBO §2 Abs. 2 — VERIFY Land) | Rough housing translation |
|---|---|---|
| GK 1 | ≤ 7 m, ≤ 1 usage unit, ≤ 400 m², ≤ 2 storeys (as LBO storeys) | detached house, small duplex-one-unit |
| GK 2 | ≤ 7 m, ≤ 2 usage units, ≤ 400 m² each | Zweifamilienhaus |
| GK 3 | ≤ 7 m, more than GK 2 units, **or** ≥ 3 storeys (each ≤ 7 m) | row houses, small MFH |
| GK 4 | > 7 m and ≤ 13 m, ≤ 400 m² per unit, typically 3–5 OG | mid MFH |
| GK 5 | > 13 m **or** > 400 m² units **or** more storeys → and above all: Sonderbau/Hochhaus rules > 22 m (High-Rise Directive) | tower-adjacent MFH, larger blocks |

Every requirement family (loadbearing fire resistance F30/F60/F90 by GK, notwendiger Treppenraum rules, stair width, flat-roof permission, harte Bedachung, Aufzugs-/Rettungswege duties) keys off this table — see `fire-protection-building` for the substance. **Getting the GK wrong at the boundary (7.00 m vs 7.10 m; a Kellergeschoss counted or not; a "Geschossfläche" of 400 m² + 1 m²) silently reclassifies the whole project.** Model the datum explicitly: *Oberkante Fußboden der letzten nutzbaren Etage über Geländeoberfläche* — not roof ridge, not parapet, not the architect's lobby floor. (The pattern above follows the LBO NRW edition family; other Länder's height bands and the Attikageschoss rules differ — VERIFY.)

### 5.3 The Bauvorlagen — what a submission physically contains

The state **Bauvorlagenverordnung** (BauVorLVO) fixes the set, copies and scales; the table is the MBO-pattern common core (VERIFY per Land; digital submission via **XBau** message standard + e-Bau portal [BAIAnet family] is in force or rolling out in all Länder — the XBau object catalogue carries exactly this document taxonomy: Lageplan, Bauzeichnungen, Baubeschreibung, Berechnungen, Nachweise, Beteiligungsschritte):

| Dokument | Content | Notes |
|---|---|---|
| **Antragsschein / Bauantrag** | signed by Bauherr + Entwurfsverfasser | the two signatures that make the dossier formal |
| **Lageplan** (qualifiziert/amtlich) | on the official map extract (Liegenschaftskataster), showing parcel, boundaries, existing + planned building, **Abstandsflächen with dimensions, GRZ/GFZ figures, building data block, street relationship, sometimes neighbouring buildings** | "qualifiziert" = the surveyor/Architekt fills the building data; the boundary positions come from the surveying authority |
| **Bauzeichnungen** | Grundrisse, Schnitte, Ansichten, usually 1:100, all floors + roof, with room names/uses, dimensions, storey heights, GFZ/GRZ math on the sheets | the sheets are where the checks are *readable*: missing room-use labelling or missing Schnitt lines = query |
| **Baubeschreibung** | construction methods, materials, usage, technical equipment, declared standards | feeds the Nachweise |
| **Berechnungen** | Grundflächen-,umbauter Raum-/Geschossflächenberechnung, Wohn-/Nutzflächen (usage of the respective norms — Wohnflächenverordnung; DIN 277 for NF), Stellplatzberechnung | must reconcile *sheet by sheet* with the drawings |
| **Nachweise** | Standschutznachweis (Tragwerksnachweis), Brandschutznachweis, Wärmeschutz-/GEG-Nachweis, Schallschutznachweis (where owed), Nachweis barrierefreies Bauen / barrierearme Wohnungen (where owed), sometimes Immission/Geruch/Emission notes, Betriebsanlagenteil (special systems) | §9 expands the package structure |
| **Sonstige** | Baulastnachweise, Ablösungs-/Kostenvoranschläge, artenschutzrechtliche Beiträge, Abweichungsanträge with Begründung + compensation, statistics forms (Amtliche Bau- und Wohnstatistik), sometimes energy-consultation confirmations | the "also-ran" items that stall dossiers |

**The plan-consistency law:** elevations and sections must be *derived from the same model* as the plans; any disagreement between plan/elevation/section (window count, storey height, parapet, ridge) is the most common formal query and the most avoidable one. This skill's companion FreeCAD rule (§20) exists exactly to enforce it.

### 5.4 Procedure timeline (indicative — VERIFY per Land and authority)

```
Bauvorlagen complete & signed
  → Gemeinde: Einvernehmen §36 (municipality's veto rights on plan conformity/Befreiung)
  → Fachbehörden/Beteiligte (Denkmal, Wasser, Naturschutz, Straße, Gesundheit je nach Verfahren)
  → Nachbarbeteiligung (where the Land provides it: objections within a stated period)
  → Prüfung; Rückfragen (Nachforderungen) — each cycle adds weeks
  → Baugenehmigung issued (valid typically 3 or 5 years depending on Land; lapse rules,
     extension possible; VERIFY — some Länder count from Zustellung, some from
     Wirksamkeit against neighbours)
  → Baubeginnsanzeige to the authority (most Länder)
  → some Länder: some kind of Rohbau-/Bestandsprüfung or a "Feuerwehrzufahrt"-check
  → Fertigstellungsmeldung; some states require/allow a completion-confirmation
     clause (Bauzustandsbestätigung / Verwendbarkeitsnachweis pattern for
     brandschutz- and standschutz-relevant execution — VERIFY by Land)
  → utility final connections; EWS (Energieausweis) handover / existing-building checks.
```

A common legal effect worth knowing: several Länder run a **Genehmigungsfiktion** (permit deemed granted after a statutory period of authority silence, e.g. the "drei-Monats-Frist" family — VERIFY per Land; it does *not* cure material illegality and is suspended by a lawful query). Never *promise* the user one; mention it only as a Land-specific pressure valve with conditions.

---

## Section 6: Who Signs — Bauvorlageberechtigung and the Responsibility Chain

### 6.1 The offices and their legal function (MBO §51–§55 pattern — VERIFY numbering per Land)

| Role | German | Function | Qualification |
|---|---|---|---|
| Client | **Bauherr** | responsible that everything is done per permission & law; commissions the roles; keeps the approved documents on site | the owner (or a titled developer — Bauträger carries *more*: Verbraucherbauvertrag §§650i–n, MaBV-family staged payments) |
| Design author | **Entwurfsverfasser(in)** | signs the whole design's conformity with public law; "the" applicant-side responsibility bearer | **Bauvorlageberechtigt**: entry in the state Architektenkammer's list (architects, interior architects, city planners per each Kammergesetz; "qualifying examination"/ equivalence for EU citizens — the chamber laws implement the professional-qualification recognition regime, VERIFY edition) |
| Structural designer | **Vorlageberechtigte(r) Tragwerksplaner(in)** | signs the Standsicherheitsnachweis; separate, *scope-limited* Vorlageberechtigung (engineer of " Tragwerksplanung" per Ingenieurkammer laws) | Ingenieurkammer entry; "Nachweisberechtigt" in some Land formulations |
| Fire-protection designer | **Brandvorlage-/Nachweisberechtigte(r)** | Brandschutznachweis; in many Länder a special "nachweisberechtigt" status beyond ordinary Vorlageberechtigung (Architekt or special-listed engineer) | Land-specific; some Länder restrict who may do a Sonderbau concept (Prüfsachverständige) |
| Site supervisor | **Bauleiter(in)** | on-site execution responsibility; coordinates the contractors' own duties; site diary, safety coordination trigger | usually the Entwurfsverfasser or a named vorlageberechtigten Bauleiter per Land (some Länder: separate Bauleiter requirement/qualification) |
| Specialist designers | **Fachplaner** (TGA, Verbauen...) | sign their scope | per scope |
| Statics checker | **Prügingenieur / Prüfsachverständiger** | independent check of the Standsicherheitsnachweis where the Land orders it | listed by the state; issues Prüfbescheinigung + stamps |
| Fire checker | **Prüfsachverständiger Brandschutz** (Sonderbau) | where required | Land-specific |
| Safety & health coordinator | **SiGeKo** | Baustellenverordnung: *always* owed when employees of more than one employer will work on site (even sequentially); SiGePlan (RAB 31) / Vorankündigung / Unterlage für spätere Arbeiten (RAB 32) | qualification per RAB 30 — client-side duty, not contractor |

### 6.2 The liability chain, stated plainly (MBO §51-style — VERIFY)

Public law puts responsibility on *individuals who sign*, not on the "authority that approved": the Bauherr, Entwurfsverfasser, Bauleiter, Fachplaner and Unternehmer each answer for their sphere **whether or not a permission was granted** (the permission protects *plan conformity*, not *execution*). Consequences for the agent's answers: (a) "the Bauamt won't notice" is legally irrelevant once someone has signed; (b) a Prüfstatik approval does not relieve the Tragwerksplaner; (c) the Nachbarbeteiligung objection window is *not* a licence to breach — an unobjected breach can still be enforced later by the authority in some configurations and always endangers the civil-law position (§11.5).

### 6.3 Prüfstatik — the Bundesland minefield

The pattern of the Länder (VERIFY the *current* state list, edition and GK thresholds; the model below is *illustrative structure*, not a citation):

- **Full Prüfpflicht by GK tiers** (e.g. the classic Berlin/Bremen/other city-state style: Prüfsachverständiger for all buildings of higher GK; type/statik review scope defined by Verordnung).
- **Stufen model with exemptions for GK1–2** — many Flächenländer exempt small residential (one/two-family houses) wholly or partly from third-party statics review, often with the condition that the Tragwerksplaner accepts extended liability ("erweiterte responsibility des Tragwerksplaners" — the old §68-style "Prüfverzicht gegen Haftungsausweitung"), or that standard soil/ground assumptions hold (no basement in groundwater, no special loads).
- **Type-approved / standard constructions** (Typenstatik, BZA listings) can drop the Prüfer even where it would otherwise apply.
- **Sonderbau/Hochhaus** — nearly everywhere, a Brandschutz-Prüfsachverständiger and/or fire-service concept is added.

The agent's rule: **never answer "Prüfstatik is/isn't needed" without the Land named, the GK fixed, and the current Prüfsachverständigenverordnung checked — and then still say "confirm with the Baukammer/architects' engineer list".** Wrong exemption = the submission is formally incomplete and the whole dossier stalls.

### 6.4 Chambers, lists and the practical lookup

Bauvorlageberechtigung is *list-based*, not degree-based: the register of the state chamber (Architektenliste / Ingenieurliste) is what the authority checks — the *list entry itself*, in the right Land, is the qualification. Foreign-trained designers need the recognition route (chamber decision, EU professional-qualification regime). For the user: "find the right signatory" = find a professional *listed in the correct Bundesland with the correct scope (Gebäude- vs Tragwerks- vs Brandschutznachweis)*. That is a real filter — an Architekt without Tragwerks-Scope cannot sign the statics, and an Ingenieur whose list entry is "Tragwerksplanung only" cannot be the general Entwurfsverfasser.

---

## Section 7: The Technical-Requirement Web — How a DIN Becomes Law

### 7.1 The full chain (memorize this; it is the core methodology of this skill)

```
EU level:      construction-products regulation (EU 305/2011) → harmonised standards
               (hEN, e.g. EN 1990…199x Eurocodes; EN 13501 classes) → CE marking
               + European Assessment Documents/EADs → ETAs.
Model level:   MBO — Musterbauordnung; the Bauministerkonferenz's model. Maintains:
               - the "Technical Building Regulations" model list (Muster-Liste der
                 Technischen Baubestimmungen) — the list of DIN/EN introduced as law,
               - the Bauregelliste A (products needing approval-type proof: zulassungs-
                 und prüfpflichtig), B (harmonised products/ hEN — CE route),
                 C (other standards/ products, neither — VERIFY current structure:
                 DIBt publishes these lists; MVV TB replaced parts of the old system
                 for fire-relevant products — the exact Bauregelliste status is a
                 detail agents should quote carefully or not at all).
National law:  EACH Land issues its own Verwaltungsvorschrift "Liste der Technischen
               Baubestimmungen" (LTVtb) introducing model list + its own additions,
               with edition dates and transition periods. *That act* — not the DIN —
               makes a standard public-law binding in that Land.
Catch-all:     where no introduced rule exists, the LBO's general clause
               ("allgemein anerkannte Regeln der Technik") + contract law fill it.
               aRdT = the dominant, practically proven state of knowledge — a norm is
               *evidence* of aRdT, not automatically identical with it (BGH doctrine:
               a norm's application date, market practice, and technical dispute all
               weigh). VOB/C ATVs (DIN 18299 + 18300-series) are the written
               concretization of aRdT for execution & billing: Nebenleistungen
               (in the unit price) vs Besondere Leistungen (extra pay) is a
               *contract* tier question built on the aRdT tier.
```

**Therefore, the agent must answer "is DIN X binding?" in exactly this shape:**

> "DIN X is (a) introduced in [Land]'s Liste der Technischen Baubestimmungen at edition [Y] → public-law minimum for [scope], or (b) referenced by a allgemeine bauartenehmigung/Zulassung for the product → binding for that product, or (c) not introduced → evidence of aRdT → relevant for contract quality (§633 BGB / §13 VOB/B at the time of Abnahme) and as the accepted method of *proving* an LBO requirement, but you may also prove compliance by another recognised way (equivalenznachweis)."

Case (c) is where whole fields sit (much of residential execution practice, room standards, DIN 18040 except where the LBO's §50-type barrier clause pulls parts of it in for certain usage/municipal funding).

### 7.2 The Eurocode + national-annex example (pattern recognition)

The structural field shows the mechanism at its clearest, and the partial-factor logic behind them is the content: the Eurocodes (DIN EN 1990 ff.) were introduced as Technische Baubestimmungen **together with their National Annexes (NA)** — the NA is where Germany set the nationally determined parameters (γM values, snow/wind zone maps, ψ-combination factors per usage category, target β levels 3.8 normal ULS for 50-a reference period, the JCSS-calibrated partial factors), and the NAs have *changed* (2022+ reissue wave: e.g. γM1 for steel = 1.0 in the reissued NA — verify current edition!). The practical rule for this skill: a structural figure is only quotable with **standard + NA + edition + snow/wind/wind zone + climate region**, and the *calculation itself* belongs to `structural-analysis`/`timber-steel-design`/`masonry-construction`/`concrete-detailing` — this skill only routes and states bindingness. The same logic governs the DIN EN ISO 6946/10077/13789 family under GEG (energy balance methods *are* introduced norms with national annex-style value tables in DIN V 18599).

### 7.3 Product-level rules for designers (the Bauregelliste layer)

For residential detailing, the product tier decides *what may be installed and where*: classified reaction-to-fire/performance products (Baustoffklassen A1/A2/B1/B2 ↔ EN classes via the MVV TB mapping), window/door products needing abP or CE per DIN EN 14351, smoke/heat-protection closures (DIN 4102-5/-6 + Zulassung family), drainage/backflow products, exterior-wall-buildup systems (Zulassungen for ETICS thicknesses etc.). Rule for the agent: **a system detail that crosses a certified build-up (WDVS plug pattern, floating-screed decoupling, fire-stopping arrangement) may only be changed as a system if the change is inside the approval's stated tolerance; otherwise re-approval or equivalenznachweis.** This maps to `building-materials` and `construction-detailing`.

### 7.4 The standard-hierarchy note

The unifying logic of the norm system: **ISO (international) → EN (European, adopted identically as DIN EN, with NA where allowed) → DIN (national)**; the purpose of adopting them is comparable, verifiable technical proof, not uniformity of every value. Where a DIN EN contradicts an introduced German value table (a NA "de-nationalises" a parameter), the introduced pair (DIN EN …/NA) is what the Prüfer checks.

---

## Section 8: The Energy, Acoustic, Immission and Barrier Web Around the LBO

### 8.1 GEG — Gebäudeenergiegesetz (the energy law; heavily amended — VERIFY current wording each time)

The EnEV was withdrawn into the **GEG (2020)**; the 2023/24 amendments (heating-law rewrite) changed *who may install what heating* — the "65 %-Erneuerbare-Energie für neue Heizungen" entry point is staged and municipality-heat-planning dependent (Wärmeplanungsgesetz family + Land transition rules), with a long list of exceptions and municipal-heat-plan trigger dates. **The most important single anti-error rule of this skill: EnEV-era numbers (GEG's predecessors' tables) are historical.** The structural shape of the GEG (which does not change with amendments):

```
NEW BUILD (residential):
  Two ceilings, both to prove:  Qp ≤ 0.55 × reference-building primary energy
                                H'T ≤ 1.0 × reference-building transmission loss
  (GEG 2024 pattern — VERIFY; the reference building's fixed U-value set
   [wall 0.28, roof/top ceiling 0.20, windows 1.3, ΔU_WB 0.05, n50-...] is the
   object the real building is balanced against via DIN V 18599 or the allowed
   simplified method).
  + summer heat protection per DIN 4108-2 (the S/S_zul method or dynamic sim)
  + airtightness proof (blower door n50 ≤ 3 / 1.5 with ventilation — the
    introduced airtightness value pattern)
  + Wärmeschutznachweis as a Bauvorlage (§9), by a qualified person.
HEATING CHOICE (the 2024-era layer — VERIFY each Land's application dates):
  new heaters in new buildings in municipalities with a final heat plan: 98%-EE-family
  rule with the listed exceptions; elsewhere the staged rules; the local-heating
  survey + Beratungspflichten (chimney-sweep network) for existing buildings.
EXISTING BUILDINGS — the duties that survive every government (the "after-sales"
  obligations an AI must not lose track of):
   • Betriebsverbot/Austauschpflicht for old standard-/low-temp-boilers beyond the
     stated age bands (gas and oil, with the age bands — installed before a stated
     mid-Eighties/1990s year, "older than 30 years" — and exemptions for
     owner-occupied 1–2-family houses of the same vintage; the exact bands ARE
     the current text — VERIFY; the 2024 heating-law wave added inspection duties)
   • Dämmpflicht of oberste Geschossdecken/roofs (owner before the mid-90s,
     accessible ceiling — the "Dämm- oder Nachrüstpflicht" family; VERIFY current).
   • Heizungs-/Lüftungs-/Klima inspection and the **EWS duty**: every
     Verkäufer/Vermieter/Vermietungs-Verwalter must *provide* an
     Energieausweis at Besichtigung, *unprompted* (Bereitstellen ab Besichtigungstermin —
     since the "bestellen-principle" was replaced; the insert is in the
     Makler-/Exposé duty: energy carriers, year, main energy use, class letter/
     number, CO₂, construction year, unit, Heizverfahren — "Energieangaben im
     Immobilienanzeigen"-Pflicht §88-family, VERIFY edition).
   • Energieberater/Bewirtschaftungs documentation for larger buildings.
  EWS types: Bedarfsausweis (calculated, required for small pre-1977 unmodernised
  stock — the "WSchVO 1977" trigger — and always new build) vs Verbrauchsausweis
  (meter-based) where the choice is open (5+ dwellings / already modernised to
  at least WSchVO-1977 level — VERIFY current thresholds).
  **An Energieausweis contains NO retrofit obligation** — a classic scare-error.
LAND LAYER: Landesenergiegesetze (e.g. the legacy solar duties: the "Solarpflicht"
  for new flat roofs/ roofs, NRW-family, BW-family — several Länder; and the former
  Bavarian 10H-style distance rule for wind — now federalised, VERIFY), plus
  kommunale Wärmeplanung (each municipality's plan changes what heater you may install —
  the single most volatile fact in the whole field; ask for the municipality's plan status).
```

**Agent rule:** whenever a thermal figure is quoted (U-value, GEG factor, n50, ΔU_WB, a boiler rule), state: **statute + edition year + "existing or new?" + "which heating carrier?" + VERIFY**. "U ≤ 0,24 W/(m²K) because EnEV" is *always* wrong as a law claim today (0.24 survives as the existing-building Bauteilverfahren *family value* in the GEG annex — say that, with the amendment caveat, or defer to `building-physics-thermal-moisture`).

### 8.2 Sound, immission and neighbour-protection rules and their tiers

- **DIN 4109** — introduced (as LBO technical rule in the Länder) for the *public-law minimum* between foreign usage units/workplaces; the 2016→2018/2020 edition restructured the proof (simplified DIN EN ISO 12354 method + catalogues 4109-31…-36; the safety-deduction logic u_prog = 2 dB / impact +3 dB). Higher levels (VDI 4100, DEGA "Schallschutzausweis", DIN 4109-5) are **contract-tier** — sold with the words "gehoben" in the notary contract or the Teilungserklärung, not by the Bauamt. Route: `building-acoustics`.
- **TA Lärm** (instruction of the immission-protection ordinance family, Verwaltungsvorschrift) — governs *commercial/industrial* noise toward dwellings (the day/night matrix: general residential 55/40, pure residential 50/35, spa/hospital 45/35 dB(A) day 6–22/night 22–6; calm periods add +6; indoor protected-room target 35/25) — decides whether the *neighbour's* bakery can exist near your dwelling and whether *your* home workshop's heat pump/compressor may run at night (heat-pump emission per TA Lärm at the 0.5-m-before-open-window reference point — `building-acoustics` computes it). **16. BImSchV** governs *traffic* noise bands (57/47 for sensitive uses … 64/54 core areas); **18. BImSchV** sports facilities; **DIN 18005** (Schallschutz im Städtebau) is the *orientation* layer used in B-Plan noise-mapping (the Lärmpegelbereiche I–VI that pull the DIN 4109 façade requirement) — a B-Plan Festsetzung "passiver Schallschutz bei WB, LPB III" makes façade design a *T1 plan duty* (window order, bedroom side).
- **DIN 18040-1/-2 (barrier-free)** — public law only via the LBO §50/§55-family clauses (usually for publicly-reachable buildings; for residential: many Länder require a share of **barrierearme** dwellings in multi-unit new builds — the exact trigger (e.g. >2 or >4 units with lifts), the standard (18040-2 vs the reduced "barrierearm" definition), and Förderprogramme (Bauherrenmodel/"Wohnraum modernisieren" KfW families) differ per Land and year — VERIFY). Route: `accessibility-universal-design`. The agent's tier rule: KfW-442/443 "altersgemäss" funding = contract/tier-6 duty unless the B-Plan/LBO pulls it in.
- **Smoke alarms** (Rauchwarnmelderpflicht, LBO § ~46/48-family: dwellings + bedrooms + flur, per state transition dates ending fully by 2017 everywhere; DIN EN 14604 product + DIN 14676 operation/ maintenance duty for landlord-let units) — small, frequently forgotten, purely T2, state-numbered.
- **DIN 1946-6** (residential ventilation — aRdT for Feuchteschutz; the "Mindestwärmeschutz + nutzbare Lüftung" clause of DIN 4108-100-style rules: where the airtight build demands it, the ventilation concept is a duty), **DIN 57133/14676**, **DIN VDE 0100** etc. — all case-(c)/aRdT tier unless pulled in.

### 8.3 The "requirements that exist only to protect the plan" list

When asked "can the Bauamt reject this?", also check: Gestaltungs-/Erhaltungssatzung (§17/§39-model family — facade, roof pitch, materials), Veränderungssperre, Milieuschutz (Umwandlungsverbote for WE creation in some cities — *conversion*, not construction, but it kills investor briefs), Zweckentfremdungsverbotsgebote (big cities), tree-protection statutes (Baumschutzsatzung: felling-permit for trunk-circumference-threshold trees — an actual construction-blocking item), Kampfmittel/ Altlast/ waterschutzgebiet (WSSG II/III: heating-tank & rainwater rules), and Denkmalschutz (Ensembleschutz can block windows, PV, insulation at the street façade; the energy-vs-monument conflict is resolved by the authority's discretion, not by physics — VERIFY).

---

## Section 9: The Nachweispaket — Structure of a Submission's Evidence Set

The Nachweise are *named documents in the BauVorlagen catalogue*; the table is the assembly map (who prepares, what proves, when owed — VERIFY each Land's duty list):

| Nachweis / document | Proves | Prepared/signed by | Owed when |
|---|---|---|---|
| **Standsicherheitsnachweis** (Tragwerksnachweis: model, loads per introduced DIN EN 1991 + NA, design per material EC, detail drawings, foundation doc incl. soil report (Geotechnische Kategorie 1–3 per DIN EN 1997 + the introduction of the Geotech rules — VERIFY; ground category 1 "simple" small houses can drop the full Baugrundgutachten but not the founder's duty of diligence)) | §2 LBO safety: standsicher | Tragwerksplaner (vorlageberechtigt) | all structural projects; reduced in Freistellung states |
| **Prüfstatik** (Prüfbescheinigung + stamped models where Prüfpflicht) | third-party review where ordered | Prüfingenieur/Prüfsachverständiger | per §6.3 — Land-specific |
| **Brandschutznachweis** (simplified: Baubeschreibung + plan labelling [F30/T30/R30…] + GK argument; full: qualified Brandschutznachweis incl. Rettungswege overview, sometimes fire-brigade access/ water concept for Sonderbau; Sonderbau + Brandschutzaufteilungskonzept by recognized expert) | §12–§16 LBO family | nachweisberechtigt person; concept via anerkannte Prüfingenieur/Sachverständiger for Sonderbau | every project above the smallest; Sonderbau always |
| **Wärmeschutznachweis GEG** (§80/§81-style — the GEG's own "Betriebs-/Zustands-" family) | GEG new-build + existing duties when changing >10 % of a component class | qualified person per GEG §88 (the named "Handwerker/Energieberater/…" entitlement list) | new build + substantial renovation |
| **Sommerlicher Wärmeschutz** — part of the above or DIN 4108-2 proof | §14 GEG duty | same | where window fractions trigger it |
| **Schallschutznachweis** | introduced DIN 4109-1/-2 (where the Land orders it as own document) | TGA/physic planner | MFH mostly; EFH often "plan note only" — VERIFY |
| **Emissions-/Immissionsprognose** (TA Lärm) | neighbour/ self-conflict | Fachplaner | commercial adjacency or own commercial part |
| **Barrierefreiheit/-armut documentation** | LBO §-clause / Förderprogramm | planner | where owed (public buildings; MFH shares per Land; KfW if claimed) |
| **Stellplatz-/Fahrradnachweis** | Stellplatzsatzung | planner | nearly always for MFH/ commercial |
| **Bauzeiten-/Termingründung, Entwässerungsantrag, Leitungsrechte, Baulastverträge** | ancillary | surveyor/lawyer/ utility | parcel-dependent |
| **Abweichungs-/Befreiungsanträge with Begründung + Kompensationsdarstellung** | §67/§68 (LBO) & §31 (BauGB) | Entwurfsverfasser | every intentional deviation — see §10 |

**Packaging rules that save query cycles:**

1. **One numbering, everywhere.** Same storey numbers, same Achsen (grid axes A–F/1–n), same room names in plan, section, Brandschutznachweis and Wohnflächenberechnung; the Prüfer reads across sheets, not per discipline.
2. **The dimensions that prove compliance must be *on the drawing*:** Abstandsflächen with their depth values and H math (ground → wall top → roof share), GRZ/GFZ figures next to the floor they belong to, Wand-/Firsthöhe in the section with the *Geländeoberfläche* datum drawn.
3. **Every deviation appears in the Antrag, never hidden.** A discovered undeclared deviation is the worst kind of rejected application; a declared one with a compensating concept is negotiable (§10).
4. **Consistency = model-derived.** Generate the drawing set from one model (the companion skill exists for this) — plan/elevation/section disagreement is formal incompleteness.
5. The GEG/Brandschutz numbers in the submission must reconcile with the Baubeschreibung's declared standard (a submitted "KfW-40" that the Wärmeschutznachweis misses is a *certification* problem after construction, not just a planning one).

---

## Section 10: Deviations — Abweichung, Ausnahme, Befreiung (Three Different Doors)

### 10.1 The routing of an intentional rule-breach

```
Which rule does the wish breach?
  ├─ a Festsetzung of the B-Plan ................ §31(2) BauGB BEFREIUNG (discretionary;
  │    only if the deviation is "inzelnen situations" justified, public interests —
  │    especially the plan's basic intent — not opposed; some Festsetzungen are
  │    "befreiungsfest", e.g. core Art-der-Nutzung & Zahl der VG in many plans)
  │    or §31(1) AUSNAHME if the plan itself reserved it.
  ├─ the LBO or an introduced Technische Baubestimmung ... §67/§68 MBO-pattern ABWEICHUNG:
  │    allowed via the Baugenehmigung if (a) the requirement's *protected aim* is met by
  │    other means (compensating design), or (b) the requirement is clearly not
  │    applicable in the given situation (the "offensichtlich" case). The protected
  │    aims: life/safety of users & neighbours, orderliness, function — fire/egress
  │    deviations need a concept (extra width, sprinkler, brandschutztechnische
  │    Kompensation), never a wish.
  ├─ a local Satzung (Gestaltung/Erhaltung) ............ its own deviation clause — VERIFY.
  └─ a contract/agreed standard (VDI 4100, KfW...) ..... not a legal procedure at all —
       it is a renegotiation, not an application.
```

### 10.2 How deviations are argued (the format that survives review)

State: (1) rule + edition + Land, (2) precise extent of the deviation (a number, not "etwas"), (3) the *protected aim* of the rule, (4) the compensating measure or the "offensichtlich"-argument, (5) why third parties are not worsened (neighbour's light/air/noise/fire — the same goods the rule guards). Authorities grant deviations against *reasoned compensation*, never against *necessity created by the design itself* ("der Plan geht nur so" is the confession of a bad plan). **The agent designs inside the rules first; the deviation is the exception path, and an answer that treats Befreiung as a plan-improvement tool inverts the logic — say so.**

### 10.3 Bestandsschutz — the rule for everything existing

Passive Bestandsschutz protects a *lawfully created and maintained* condition against rule changes (the building may stand; it may normally be maintained and repaired *in its built state*). It **does not** extend to: new construction (fully current law), substantial alteration/extension (current law for the new part, plus in some configurations a whole-building re-check — e.g. a raised storey triggers the *new* Abstandsflächen for its walls), change of use (new usage's requirements apply fully), removal of the protected condition (disrepair, partial demolition), or *public-interest orders* (danger, remediation duties — the GEG existing-building duties apply *against* Bestand, they are not "new law"). The most common user-side question — "my house was built in 1968, must I comply today?" — answers with exactly this split, plus the named *Nachrüstpflichten* (§8.1) that were created *to bite existing stock*.

---

## Section 11: Abstandsflächen and Neighbour Law (the Formula Family)

### 11.1 The public-law distance (Abstandsflächen) — structure, with VERIFY

Every German LBO has an Abstandsflächen clause (§5/§6 numbering differs). The **MBO pattern** (post-reform family; the LBO NRW edition is the concrete instance; VERIFY for each Land):

```
Required in front of exterior walls of buildings, toward: neighbouring parcels that
are not properly built, and public traffic/green/water areas (to their middle),
railways, certain Sonderbau boundaries...

DEPTH:   a = 0.4 · H,   minimum 3.00 m                     (MBO §6 Abs. 5 pattern)
         GE/PI areas:  0.2 · H, min 3.00 m
         residential GK1/GK2 with ≤ 3 OG in front of the
         relevant walls: flat 3.00 m allowed (the "pauschal" rule — read the exact wording)
         (some Länder historically: 0.5·H, or the old A = H + d + a family;
          some now add a reduced rule for walls ≤ 2 OG/… — the factor
          and its caps ARE the Bundesland difference. VERIFY the Land's §.)

WALL HEIGHT H:   from Geländeoberfläche (as defined — the *average* of the
                 relevant terrain, the exact formula per Land, VERIFY sloped-site rules)
                 to the wall/roof-skin intersection or wall top
                 + roof-height add-on: roofs pitched < 70°: ⅓ of the roof height
                   added; steeper: the full roof height; Dachaufbauten analogous.
                 (Some Länder skip the roof add-on or compute H per wall segment —
                  the BbgBO-style segmented variant; VERIFY.)

WIDTH:   the width of the wall concerned; staggered/angled walls → segmentwise
         with fiktive Wände (imaginary closing walls) for setbacks/returns.

WHAT IS IGNORED / PRIVILEGED (the §6 Abs. 6/7 pattern — VERIFY per Land):
   - projecting elements such as cornices, roof overhangs (no own distance;
     some Länder set a cap, e.g. 1.00 m, before a fiktive Außenwand appears),
   - Vorbaue (oriel/balcony-type): if ≤ ⅓ of wall width, projection ≤ 1.50 m,
     and ≥ 2.00 m clear to the opposite boundary — then no own Abstandsfläche;
     some Länder split balcony/orangery caps (2 m / 3 m variants — the
     exact numbers ARE the state edition; VERIFY).
   - energy-retrofit layers ≤ 0.25 m with ≥ 2.50 m to the boundary (existing buildings).
INSIDE the Abstandsfläche allowed anyway (§6 Abs. 8 pattern):
   - garages & buildings without Aufenthaltsräume/fireplaces: mittlere Wandhöhe ≤ 3.00 m,
     total length per boundary 9.00 m, per parcel max 15.00 m of such non-compliant siting;
   - free-standing PV ≤ 3 m height/9 m length (state variants),
   - fences/retaining walls ≤ 2.00 m outside GI (lower in some inner areas — VERIFY).
NO Abstandsfläche required (the boundary-construction door, §6 Abs. 1 pattern):
   - where *planning law compels or permits* building at the boundary
     (Grenzbebauung via B-Plan — this is why §4's Bauweise/overlapping checks matter),
   - or where the surrounding development per §34 permits a different distance;
   - plus the special small-border structure family (LBO's "grenzständige
     Nebenanlagen" clause: e.g. walls ≤ 3.00 m mittlere Wandhöhe on the boundary —
     some Länder say "bis 3 m" without length limits for *existing* patterns — VERIFY).
Neighbour consent route: Abstandsflächen may extend over the boundary ONLY if
   publicly secured — via Baulast (§11.3), not a handshake.
```

### 11.2 Worked H example (method-valid; the factor is the Land's — VERIFY)

```
Two-storey house, GK1, flat-roof, wall top OK 6.20 m above avg terrain;
terrain avg taken per the Land's defined formula; roof parapet 0.60 m counts as wall top.
H = 6.80 m  (no pitched-roof add-on for flat roofs; Dachaufbauten (Kniestock/PV-frame
    — checked separately: PV not counted if within the privileged elements list).
a = 0.4·6.80 = 2.72 m → but MINIMUM 3.00 m governs. (0.4H only bites above H = 7.5 m.)
With pitched roof 38°, roof height 2.40 m: H = 6.20 + ⅓·2.40 = 7.00 m → a = 2.80 m
    → min 3.00 m again governs.
A third storey pushed OK to 9.10 m + ⅓·2.40 = 9.90 m → a = 3.96 m.
The jump at the minimum-value band (0.4H crossing 3.00 m exactly at H = 7.50 m) is
the most common modelling surprise: measure H like the authority does, from the
defined terrain datum, to the defined wall top.
```

**Both distance regimes must pass:** the B-Plan's Baugrenze (T1) and the LBO's Abstandsfläche (T2). They are not alternatives; the stricter geometry binds. And neither equals the *civil-law* distance claim (§11.5).

### 11.3 Baulasten — the public-law neighbour contract

A **Baulast** (§85-style MBO; the *Verzeichnis* is at the Bauaufsicht) is a publicly-secured building burden on a parcel — typical types: **Abstandsbaulast** (the neighbour accepts the encroaching distance), **Anbaubaulast** (fire-wall-side later attachment), **Überbaubaulast** (a part over the boundary), **Zufahrts-/Geh-, Leitungs- and Stellplatzbaulasten**. Key facts: it runs with the land (binds successors — unlike a schuldrechtlicher Nachbarschaftsvertrag, which must *additionally* be secured, typically via Auflassungsvormerkung-robust *dingliche* arrangement or by being mirrored into a Baulast); it is entered on application within the permit file; **always query the Baulastenverzeichnis before designing near boundaries** (in some Länder it is only accessible with a concrete interest, and in some it is incomplete/negative — a "no entry" answer is only as good as the register's completeness). An unsatisfied distance without a Baulast is the single classic "planned on borrowed land" failure.

### 11.4 Grenzbebauung and the corner problem

Where Grenzbebauung is plan-permitted: walls at boundary usually come with **fire-service consequences** — Brandwand/gebäude end-wall logic (a wall within < 2.50 m of the boundary behaves as a Brandwand: no openings (or fb-class closures), through-roof upstand 0.30 m or the double 0.50 m slab pattern — the *fire* skill owns these numbers; route), corner cases at angle changes (> 120°-style relaxations), and the "no openings on the neighbour side, ever" default if a wall stands *in* the boundary line without a securing Anbaurecht for the future. Also: two Länder's rules can meet at a border parcel, and some states' rules on *bestehende* Grenzbebauung differ from new — re-attaching to an existing boundary wall is not automatically "Bestand".

### 11.5 Civil-law neighbour law (separate claims — never conflated)

Public permission does not extinguish private claims (§906/§907 BGB-style: immittances; boundary distances for *plantings* and some structures are in the **Nachbarrechtsgesetze of the Länder** (e.g. the classic 2-m/3-m hedge and tree bands with the age-exemption families — VERIFY state), and the *Überbau* §912/§915 route, Notweg §917, and the *Nachbarwehransprüche* (Abwehransprüche from the public distances as *third-party protection*: a neighbour can often attack an approved building civilly if the Abstandsfläche rule protects *their* light/air). Practical consequence: **a Baugenehmigung with Nachbarbeteiligung and no objection still does not guarantee the neighbour's civil claim died** — that is why experienced designers secure distances or contracts, not only permissions.

### 11.6 Austria and Switzerland (route, don't transplant)

- **Austria**: no MBO equivalent — Bauordnung is purely Land (9 codes); the distance family is usually a *fixed-depth or fraction-of-height* system per Land (many eastern Länder: Abstandsfläche = building height, min 3–4 m; Vorarlberg/Tirol patterns differ), plus flächige Widmung (Widmungsplan, Flächenumwidmung), Grundverkehrsgesetze, and a separate Bauprodukte/EU-CPR layer; the "Bauleitplanung" analogue is Örtliches Raumordnungskonzept/Flächenwidmungsplan → Bebauungsplan (mostly *verbindlich* via der Bebauungsplan in most states — but its legal role differs). VERIFY per Bundesland; nothing from Germany may be copied.
- **Switzerland**: no state examination of design conformity in the German sense for most single-family houses — the *Bau- und Zonenordnung* of the commune + cantonal Baugesetz/Baubewilligungsdekret define the usable geometry (Ziffer "Zonenziffer/Ausnutzungsziffer" = the plot-coverage-ratio equivalent, often 20–50 % by zone; setbacks (Vorschriften) frequently 3–5 m or a fraction of the street width; Grenzabstände per canton with *Grenzbau*-permissions for small parts; Denkmal-/Erschließungszonen). Approval procedure = Baubewilligung/Eingabe with Einsprachefrist (municipal), the technical fire/energy rules via the VKF/AEAI (Modellgesetze/Programme) — a different stack. Route any CH project to the commune's Baukontrolle texts.
- In both: the tier logic (plan > order > introduced rule > aRdT > contract) still applies; the *sources* do not.

---

## Section 12: Private Construction Law — Quick Map (BGB & VOB/B)

**Scope note: this maps the framework; it never advises on a live dispute.** The builder-owner relationship is a Werkvertrag (§§631 ff. BGB) with the special **Bauvertrag** rules §§650a ff. (since 2018) — success owed, not work. VOB/B (DIN 1961) is *contractual private rules* — AGB-privilege survives only if it is **adopted wholly and unmodified** (any partial adoption → full individual-clause review); vs consumers/where AGB control applies, clauses fall back to BGB. Check which one is actually in the contract *first* — the two regimes differ on almost everything below (numbers here follow the pre-2024 edition era — VERIFY current editions/case law):

| Topic | BGB (Bauvertrag 2018+) | VOB/B if wholly contracted |
|---|---|---|
| Payment on account | **Abschläge für den Wert der geleisteten Arbeit** §632a; AG may withhold appropriate part for defects | §16(1): Abschlag on prüfbare Aufmaß/Zustandsbericht; due 21 days; final invoice payable ≤ 60 days |
| Advance payment | negotiated | §16(2) — only by agreement |
| Security for the contractor | §650f Bauhandwerkersicherung (demand security, deadline, refuse/terminate; +10% Nebenforderungen; not vs consumer/public-law AG); §650e Sicherungshypothek | same statutory fallback |
| Client's securities | — | Vertragserfüllungsbürgschaft ~5%, Sicherheitseinbehalt for Mängelansprüche up to ~5→3% (release mechanics; old §17 VOB/B / §9c VOB/A caps — VERIFY current numbering); combined excessive security can void the whole arrangement (BGH 2016) |
| Changes | §650b: client's unilateral change right + contractor pricing duty; dispute → court-ordered interim; §650c default: cost + agreed mark-ups (actual required costs + AGK/W/G), or from hinterlegte Urkalkulation | §2(5) (anordnete Änderung) / §2(6) (zusätzliche Leistungen) / §2(3) quantity deviations ±10% band logic; §2(10) hourly work needs prior agreement |
| **Abnahme** | §640: essential conformity; effects; fingierte Abnahme after deadline w/ defect-naming refusal; verweigern + Zustandsfeststellung §640(2)/§650g | §12: formlos/förmlich/konkludent; Fertigstellungsanzeige + 12 Werktage fiction (the fiction-clause is not always AGB-safe) |
| Defect rights | §633 (deviation from agreed Beschaffenheit, else customary + **aRdT at time of Abnahme** — BGH); §634 ladder: Nacherfüllung → after deadline: Selbstvornahme/Rücktritt/Minderung/Schadensersatz | §13 with the same ladder + §13(5) rüge-restart of limitation for the complained defect |
| **Verjährung Mängel** | §634a: **5 years for Bauwerk**, 2 y for maintenance plans etc.; from Abnahme | §13(4): 4 y Bauwerke, 2 y fire-exposed parts of firing plants/wartungsbedürftige; +rüge rule |
| Retention | by agreement (model: 5% interest-free, guarantee-releasable) | §17 mechanics |
| Vertragsstrafe | AGB-controlled | needs explicit clause; ~0.2–0.3%/werktag overage with 5% net cap is the tolerated pattern (BGH); must be **reserved at Abnahme** |
| Consumer build contract | §§650i–n: Baubeschreibung in Textform, binding completion date, 14-day Widerruf, **Abschläge ≤ 90% total, first payment against 5% performance security**, delivery of permit-supporting docs | — (VOB/B not recommended vs consumers) |
| Off-the-books work | whole contract void (§138) — no pay, no restitution | same |
| Architect/engineer contract | Dienstvertrag in principle, success-oriented elements; §650q/p (Zielfindungsphase, change pricing analog) | — |
| Dispute resolution | courts ~15 months first instance; ADR menu: Mediation, Schlichtung (Kammern), Adjudikation/DAB, Schiedsgutachten, Schiedsgericht; "Streitlöser" expert+lawyer tandem | same + Güteausschuss patterns |

**The three agent-critical concepts:** (1) **Abnahme ≠ completion ≠ Schlussrechnung** — limitation, payment due-ness and burden-of-proof flip at the *acceptance event*; never say "the warranty starts when it's finished". (2) **A known defect not reserved at Abnahme loses §634 Nr.1–3 rights** — "the Bauleiter noticed it and said nothing" is a claim-killer. (3) **VOB/B never applies "by default"** — "that's VOB" is not an answer; look at the contract.

## Section 13: HOAI — The Fee and Service Framework (Status-Critical)

**Status first:** HOAI (Verordnung über die Honorare für Architekten- und Ingenieurleistungen) is a *price law by regulation*, not a service law: it defines **Leistungsbilder** (what phases/services exist) and, historically, **fixed min/max fee bands**. The ECJ (04.07.2019) held the binding price bands incompatible with the Services Directive; **HOAI 2021 removed the mandatory price law → fees are freely negotiable** (tables survive as market orientation; the *Leistungsbilder* remain the definition of what was bought). Anything quoting "HOAI Mindestsatz" as claimable law today needs the case-law caveat — VERIFY the current HOAI edition and case-law position; and *written (text-form) fee agreement at/with the order* remains the practical anchor (§7-family: without agreement, the statutory *Mindestsatz* consequence is gone — the default is now the negotiated/or-§631 logic; say "verify" and never build a business case on a Mindestsatz).

### 13.1 The service framework — Objektplanung Gebäude, LPH 1–9 (one-liners; weights = HOAI 2013, VERIFY 2021 table)

| Phase | Name | Core deliverable | Weight (2013 OP-Gebäude) |
|---|---|---|---|
| 1 | Grundlagenermittlung | brief, site feasibility statement, cost frame | 2 % |
| 2 | Vorplanung | concept + studies, Kostenschätzung | 7 % |
| 3 | Entwurfsplanung | designed solution with integration of all planners, **Kostenberechnung**, presentation plans | 15 % |
| 4 | Genehmigungsplanung | the submission dossier (§5, §9), Nachweise to permit-ready depth | 3 % |
| 5 | Ausführungsplanung | execute-ready detail (plan- und detail-reif, the model work) | 25 % |
| 6 | Vorbereitung der Vergabe | LV (GAEB), time schedule, cost estimate for tender | 10 % |
| 7 | Mitwirkung bei der Vergabe | tendering, Prüfen, Zuschlag preparation, contract drafts | 4 % |
| 8 | **Objektüberwachung** (Bauüberwachung) | site supervision, Bautagebuch, Rechnungsprüfung, Mängel management, documentation | 32 % |
| 9 | Objektbetreuung | documentation handover, hidden-defect review (1–4 y), object care | 2 % |

(Specialist Leistungsbilder run parallel: Tragwerksplanung its own phase set incl. detailed "Nachweis" phases; TGA; Freianlagen; Ingenieurbauwerke; each with own weights — the Tragwerk/TGA weight columns are edition-sensitive; **VERIFY against the HOAI annex before quoting**.) Phases can be **unbundled** (partial commissioning priced by these percentages — the "missing LPH 4 means the submission isn't bought" reading is the default rule); **Besondere Leistungen** (listed per phase in the HOAI annexes: Örtliche Bauüberwachung for civil works, Brandschutz-, Wärmeschutz-, Schallschutznachweise as *separate* commissioned services, BIM management, SiGeKo, type-simulation…) are **extra fee** and must be explicitly contracted — a classic client surprise and an agent blind spot.

### 13.2 Fee logic in five steps (all figures negotiable post-ECJ; structure still HOAI's)

```
1. Anrechenbare Kosten — net construction cost (KG 300+400 (+500 for the right
   Leistungsbild) per DIN 276; exclusions e.g. KG 110 land, 710/760 — VERIFY
   the current mapping; existing buildings: mvB = hypothetical-cost logic
   (Menge × comparison cost × condition factor), not the real invoice.)
2. Honorarzone (Gebäude 1–5) from the Merkmalskatalog: anbindung, funkionsbereiche,
   gestaltung, konstruktion, technische ausrüstung, ausbau — scored; the zones
   decide the band.
3. Grundhonorar from the Honorartafel (strongly degressive €/per €; ceilings
   ~25 M€ for Gebäude → beyond free negotiation).
4. × phase percentages (full 100 % only when all Grundleistungen of all phases
   were rendered).
5. + Zuschläge (Umbau/Instandhaltung default 20 % presumable; existing-building
   mvB) + Nebenkosten + VAT.
Fee falls due on ABNAHME of the *building* (not on plan delivery) + prüfbare
Honorarschlussrechnung; Abschlagsrechnungen per phase progress.
Services OUTSIDE HOAI entirely (free-priced): Projektsteuerung (AHO-Markheft 9),
BIM-Management (AHO 11 pattern), Bauphysik, Brandschutz engineering,
Gutachten, Vermessung (AHO 14), UVS — contracting them needs their own scope
paper (and the §650p Zielfindungsphase rule guards against unpaid pitch work).
```

## Section 14: Insurance & Liability — the Role Map (informational, not advice)

| Risk | Instrument | Who needs it |
|---|---|---|
| Design error → third-party/personal damage | **Berufshaftpflicht** of the Kammer professionals (statutorily required for Kammer-listed members — VERIFY; sums per Kammer rules) | Architekt/Ingenieur of every signed scope |
| Fire/theft/weather damage *to the construction* | Bauleistungs-/ Feuerrohbauversicherung | usually contractor + client jointly; check contract |
| Injury on site / duty-of-care breach | **Bauherrenhaftpflicht** + the *Verkehrssicherungspflicht*: runs to the executing contractor during construction, **reverts at Abnahme** (established case law) — fences, winter service, visitor safety; Bauleiter who ignores a missing guardrail takes *Mitverschulden* personally (criminal exposure when the Gefährdungsbeurteilung/Unterweisung/monitoring duties were never run) | Bauherr + Bauleiter |
| Contractual defect claims | the AN's liability; Bürgschaft/ Sicherheitseinbehalt (§12) | contractor |
| Authority-process risk (delayed/refused permit) | not insurable in design — this is *design discipline* (read the plan; declare deviations) | designer |
| Natural disaster/ Hochwasser | Elementarschadenversicherung; the state funding fragments | Bauherr |
| Public-client projects | additional Vergaberecht liability (Nebenangebote formal errors; property of the Urkalkulation inspection duty) | bidder |

**Agent rule:** liability answers end at the map + "the professional's insurance and the Kammer rules apply — verify"; never opine on coverage, and never reassure a user that "insurance will cover it" instead of stating the compliance duty.

## Section 15: Tendering and Contracting Construction & Planning Services

### 15.1 Public clients (Vergaberecht — thresholds and paragraph numbers drift; VERIFY edition)

```
Which regime?
 ├─ Planning/architectural services → VgV (EU-level > ~221k€-class thresholds
 │    (biennial revision — quote the CURRENT EUR threshold, not this file's),
 │    below: national rules + the Land's VgV-analogues):
 │    Leistungswettbewerb: quality-vs-price; planners' price may be weighted
 │    0 % (§58(2) pattern); with prior Wettbewerb (§§69 ff.) for facades/campus;
 │    references must be comparable; stepped phase award (§34 HOAI logic →
 │    threshold counting).
 ├─ Construction services above EU threshold (Bauauftrag — 5.28/5.54 M€-family,
 │    UPDATED biennially — 2024/25: ~5.538 M€ at this file's vintage; ALWAYS re-read the
 │    current Bundesanzeiger publication) → GWB part 4 + VOB/A **EU-section**:
 │    procedures: offen / nicht offen / Verhandlungsverfahren m. Wettbewerblichem
 │    Ziel / Innovationspartnerschaft; Eignung (Fachkunde/Leistungsfählichkeit/
 │    Zuverlässigkeit, Präqualifizierung), Gleichbehandlung §2(2)-style,
 │    Wirtschaftlichkeit (best price/perf), Transparenz (Vergabevermerk),
 │    Fachlose/Mittelstand (§15(2) pattern), unusually-low-bid clarification
 │    duty (§16d/§60), Bindefrist, Zuschlag = contract formation,
 │    Rechtsschutz: Rüge (10 days) → Nachprüfungsverfahren (Vergabekammer,
 │    Standstill 15 days, Kammer ~5 weeks; de-facto-award → up to
 │    Unwirksamkeit). Below threshold → VOB/A Abschnitt 1 (national).
 └─ Private client → Vergabefreiheit; but a "public-ish" corporate group or
      Fördermittel can pull the rules in (ZW-structure, funding conditions).
Contract types: EP-Vertrag (VOB/A default), Detail-/Global-Pauschal (scope
frozen — quantity risk moves to AN), Nachunternehmer vs Fremdunternehmer
(with/without warranty — the Nachunternehmer/Fremdunternehmer distinction), GU/TU, Teilbare Vergabe.
```

### 15.2 Tender documents that decide the project (the anti-claim checklist decides the project)

Full-and-unambiguous LV description (no "1 psch. Wasserhaltung"-style clauses — §7 VOB/A completeness), order of precedence (BVB/ZVB/LV/ZTV/VTB per §1 VOB/B), Basisterminplan + Zwischenfristen, **payment/billing clauses, LDs (Vertragsstrafe), retention rules, removal-of-VOB/B traps** (any modification → AGB review), Besondere-Leistungen list, Urkalkulation handling (public: Einsicht for award verification — §16a-style), **Vergabe of BIM services as part of the LV vs Besondere Leistung (§13.1)**.

### 15.3 BIM contracting (the contract-document layer)

- **AIA — Auftraggeber-Informationsanforderungen** = the client's requirements document (= ISO 19650 *EIR*): BIM goals → use cases → per-milestone **Data Drops**, Modellinhalte (LOD/LOIN per object), delivery formats (IFC per the Land's/Bund's mandates — Stufenplan DB BMVI-level: Level-2-equivalent baseline for public infrastructure; BIM-Erlass check-duty > 5 M€-family — VERIFY current status), Rollen (BIM-Manager AG-side; BIM-Gesamtkoordinator/Gesamtkoordinatorin; Fachkoordinator; Modellautor per VDI 2552-Blatt 7 role set), QA rules (model checking against AIA as *payment condition* — the "AIA-Konformität bei Abschlagszahlungen" pattern).
- **BAP — BIM-Abwicklungsplan** = the contractor-side execution answer (= *BEP*): software/ formats/ processes/ CDE organisation, the information- delivery matrix (which model/ document, who, when, which exchange level per EN 17412-1 **LOIN** — use-case-and-milestone-bound, in three parts: LOG geometry, LOI information, documentation; VDI 2552/LOD concepts and BIMForum LOD 100–500 where the project uses them). VDI 2552-Blatt 10: AIA/BAP are *complementary* (Lasten-/Pflichtenheft pair); a Vor-/Angebots-BAP is evaluated in two-stage tenders; the Projekt-BAP is the contractually live, iteratively updated handbook.
- **CDE workflow**: status model Work in Progress → Shared → Published → Archived (PAS 1192-2 lineage → ISO 19650), single point of exchange = the CDE; contract clause needed for it.
- Contract mechanics: Muster-**BIM-BVB** (BIM4INFRA-era special contract conditions) attach the AIA/BAP + ISO-19650 duties to the HOAI/AHO service package; model-IP and model-purity/ liability allocation belong in them; BIM-Mehraufwand = Besondere Leistung; BIM-as-method within the contracted Grundleistungen adds no fee by itself.
- Machine-checkable rules layer (why it matters for *permits*): the code-checking research field (DesignCheck/mvdXML/SPARQL/VCCL-class rule languages, XPlanung for plans, **XBau for the submission route**, BIM-import into the digital Bauantrag of the future) — the agent's realistic use: *deliver models whose attributes carry the proof* (fire class, U-value, GK, Raumname) so the dossier reconciles itself — §20.

---

## Section 16: After the Permit — the Rest of the Administrative Lifecycle

The Baugenehmigung is the middle, not the end. Standard German sequence (validity periods and confirmation duties are Land-specific — VERIFY each):

```
Baugenehmigung (befristet gültig: commonly 3 or 5 years to start+finish; Verlängerung
   on application; Erlöschen if work abandoned — VERIFY the Land's clause)
  │
  ├─ BAUBEGINNSANZEIGE (start-of-construction notice to the authority — most Länder;
  │    the clock on the validity runs from a *reported* start)
  ├─ Site duties: keep the approved documents + genehmigte Pläne available on site;
  │    SiGeKo deliverables live (SiGePlan updates); Nachbarschafts-communication
  │    (the civil-law layer §11.5 does not lapse with the permit).
  ├─ DEVIATIONS DURING CONSTRUCTION — a change from the approved plan (extra room,
  │    deeper basement, moved wall, more storey) is only lawful if it is *not*
  │    genehmigungserforderlich (small, within the approved scope, no new
  │    requirements touched — the Land's "genehmigungsänderung"/"Änderung der
  │    Bauvorlage" clause decides — VERIFY) or after a changed approval
  │    (Änderungsgenehmigung). The classic failure: the "just a slightly taller
  │    attic" discovered by the inspector → Baustopp → Nachtrag → in worst case
  │    Rückbau. There is no German "regularisation fee" as a plan; deviation
  │    management is a *legal* procedure, and an unapproved deviation surfaces at
  │    the Fertigstellungsmeldung, at the utility final hookup, at the
  │    Grundsteuer/Wohnungsübergabe, and at every resale inventory.
  ├─ ROHDOP/BEGONNENEN-Bauen checks, Feuerwehrzufahrt kept usable,
  │    Immissionsschutz during build (TA Lärm does not apply to the construction
  │    site itself — that is the BaumaschinenLärmschutz-Verordnung + community
  │    police orders: the "Ruhezeiten" family — VERIFY).
  ├─ FERTIGSTELLUNG: some Länder: a confirmation procedure by the
  │    Entwurfsverfasser/Prüfsachverständige that the execution matches the
  │    permit for the safety-relevant parts (the "bauartenehmlich freigegeben" /
  │    usage-confirmation family); others rely on the authorities' random
  │    controls. Either way: the as-built must *match* the approved dossier.
  ├─ Nutzungsänderung duties satisfied; Rauchwarnmelder installed & receipted.
  └─ POST-COMPLETION: Energieausweis as-built for sale/let (§8.1), Wohnflächen-
       angaben consistent, final utility contracts, Grunddaten (Gebäude-/
       Wohnungszählung-type statistics where owed), Wartungs-/Überwachungs-
       bindungen (Prüfungen for Sonderbau: wiederkehrende Begehungen; Aufzugs-
       prüfungen; Brandschutztür-Inspektionen — the continuing duties list).
```

**The answer-shape rule:** when a user asks "do we need a permit for X", the complete answer is always **permit question → procedure track → signature requirement → deviation/change rule → continuing duty** — five gates, not one. "Small, therefore free" answers only the first gate and fail at the third.

---

## Section 17: Worked Examples (method-valid; every parcel figure is a placeholder)

### 17.1 "Can I build this house here?" — the two-tier gate check

```
INPUT: Bundesland = need to be named; plot in B-Plan "Am Sande 3. BA"; WA;
       GRZ 0.4 (T1-V PLACEHOLDER — read the plan!), GFZ 1.2 (placeholder),
       "2 Vollgeschosse + DG als Vollgeschoss möglich?" (read the wording:
       Obergrenze? staffelbar?), Wandhöhe max 8.50 m (placeholder), offene
       Bauweise mit Einzel-/Doppelhaus, Baufenster drawn, "Flachdach zulässig?"
       (text Festsetzung often: "Dachneigung 22–38°" — a pitched-roof duty that
       kills a flat-roof design at T1 level), StellplatzSatzung: 1.5/WE.

GATE 1 — Plan: usage WA ✓ (but home office ≤49 %-family rules, guest-WC counts,
        let-able unit: "Wohnen" allowed, "Beherbergung" maybe not — BauNVO §13
        family argument needed for a Ferienwohnung); GRZ check incl. garage
        (counts per §19(4)-style rules if plan says so); GFZ with the DG question
        (DG = Vollgeschoss? apply the >½-aber-<⅔ logic via the plan's own VG
        definition or §20 BauNVO — the height datum is the *average terrain*);
        Wandhöhe measured per plan definition; Baufenster boolean; Dachform
        Festsetzung vs the design's roof.
GATE 2 — LBO: GK by height → here GK1/2 → Abstandsflächen (0.4H/min3 family —
        Land's factor) vs plot depths: the north wall 2.60 m from the boundary
        with H 7.90 m → 0.4H = 3.16 m → FAIL → options: move wall, reduce
        height, lower-storey logic, or the Land's GK1/2 3-m flat rule if it
        exists and applies to THIS wall; Grenzbebauung only if the B-Plan
        permits grenzständig (the plan here says "offen" — so boundary wall
        would need Befreiung AND the fire consequences).
GATE 3 — Verfahren: Freistellung state? Does the project meet ALL Freistellung
        preconditions (GK band, within Baufenster, no deviation needed)?
        The 3.16-m failure already destroyed Freistellung → permit route.
GATE 4 — Signatures: vorlageberechtiger Entwurfsverfasser; Tragwerksplaner;
        Prüfstatik for GK1/2 in this Land? VERIFY; Wärmeschutznachweiser;
        Brandschutz in simplified form.
GATE 5 — Erschließung + fees (Herstellungs-/Beitragslage) + Baulasten query.
OUTPUT SHAPE: a *numbered list of what passes, what fails, what is blocked on a
missing document* — never "genehmigungsfähig".
```

### 17.2 Converting two units into one, adding a storey (the layered answer)

```
Two GK3-adjacent moves in one question → split the answer:
  BAUPPLANUNG: WE count caps? Erhaltungssatzung/Milieuschutz (conversion rules —
    not permit but *Verbot with Genehmigungspflicht*); §34-area? B-Plan?
  ORDER: extra storey = new construction → FULL current law for it:
    Abstandsflächen recomputed with the new H (the minimum-3m band jumps to
    0.4H above H = 7.5 m — §11.2 math), Brandschutz: new GK band possible
    (7.00→7.10 m trap §5.2), second escape route question, smoke alarms retrofit,
    GEG existing-component duties on the touched components (>10 % rule),
    sound: new storey's flank paths vs 4109 minimums, lift question for barrierearm.
  STATIK: existing foundations verified for the added load = a full
    Bestandserkundung (trial pits, materials survey, possibly a Baudenkmal-style
    documentation); no honest agent says "a steel frame will do" — the
    Tragwerksplaner decides after inspection.
  NEIGHBOUR: civil claims survive the permit (§11.5); Nachbarbeteiligung if
    the Land's procedure provides it.
ANSWER: five gates again, each with its own blocker. The user's "but my
  grandfather built it like that" = Bestandsschutz question §10.3.
```

### 17.3 "My AI plan-check said U = 0.24 because EnEV" — the correction pattern

```
Recognise the failure class (superseded-law citation — §18 pattern 1):
  1. Name the withdrawn statute (EnEV last edition 2014/16-family, superseded by
     GEG 2020+; U-value tables moved into GEG annexes/reference-building logic).
  2. Replace with the current test: Qp ≤ 0.55× & H'T ≤ 1.0× reference building
     (GEG 2024 pattern — VERIFY edition), component-level 0.24/0.20/1.3/1.4
     survive as *reference-building and existing-building Bauteil* values, not
     as the new-build single test.
  3. State who proves it: the Wärmeschutznachweis (GEG §80-family) at submission;
     the as-built EWS for resale — and that both bind the *signing* persons.
  4. Re-run the envelope numbers via `building-physics-thermal-moisture`.
Never answer "EnEV is fine now" — answer with the statute chain, once, cleanly.
```

---

## Section 18: Typical Agent Failure Patterns (learn to smell these — including your own)

1. **Superseded-law citation as current.** EnEV U-values "as law"; HOAI Mindestsätze as binding post-ECJ; pre-2018 Werkvertragsrecht ("Werklohn ohne Abschlagsregel"); old VOB/A paragraph numbers; DIN 4109:2002 tables; "WSchVO 1977" thresholds quoted without noting they define the *Bedarfsausweis trigger*, not a design value. **Countermeasure: every figure carries statute + edition + tier, or it stays unquoted.**
2. **DIN-as-law without the introduction test.** "Laut DIN muss..." as if a standard bound the citizen. Check the three-step test (§1.1) — introduced? referenced product rule? aRdT? else it is a *method of proof*, not a commandment. The mirror error: "DIN is voluntary, so nothing binds" — the catch-all clauses and §633/§13 VOB/B make aRdT contractually enforceable.
3. **Bundesland mixing.** Citing the MBO §6 as if directly applicable, applying the Bavarian distance rule in NRW, a Freistellung that only three Länder have, a 10 m Prüfstatik exemption from another state, the wrong §-numbering (§5 vs §6 Abstandsflächen), the smoke-alarm transition dates from the wrong Land, applying one Land's height bands verbatim in another. **Countermeasure: name the Land first, the Land's norm second; when unsure, show the MBO pattern *and* the divergence warning.**
4. **Conflating the four stacks.** "The B-Plan allows it → legal" (ignores LBO + Erschließung); "the permit is approved → the neighbour has no claim"; "the Abnahme happened → warranty clock started for the *architect's* services too" (different duties); "verfahrensfrei → rule-free".
5. **Treating derived §34 figures as read from a plan.** §34 produces *arguments*, never certificates. Any §34 number without the reference-parcel table behind it is a guess with formatting.
6. **Deviation-by-hope.** Designing over the boundary "because a Befreiung comes" or "because nobody checks a Freistellung". Befreiung is discretionary, the Freistellung conditions are *objective*, and the discovery moment (inspection, resale, neighbour) is outside the designer's control.
7. **Abstandsflächen datum errors.** H from finished floor instead of defined terrain; forgetting the roof add-on; forgetting the minimum-3-m band's non-linearity; ignoring the fiktive-Wand/segment logic of staggered walls; "the garage is small → free" (the §6(8)-family privilege has *length and total* caps: the 9/15-m pattern — VERIFY).
8. **Energieausweis = Sanierungspflicht scare.** The Ausweis informs; the *duties* are the named Nachrüst-/Betriebsverbots clauses. Quoting a "class H" verdict as a legal retrofit command is alarmism and wrong.
9. **Verjährung confusion.** BGB 5 y vs VOB/B 4 y vs the rüge-restart vs the *Architekten* HOAI-service Verjährung vs the claim-securing moments; and "Gewährleistung starts at handover". Starts at **Abnahme**, and only the applicable regime's length applies — say which.
10. **HOAI phase arithmetic as delivery promise.** "LPH 4 included" ≠ the planner *may* submit (they must be vorlageberechtigt) and ≠ Besondere Leistungen (Nachweise, ÖBA) are included.
11. **Fire/energy number import from a neighbouring skill without the tier tag** — e.g. quoting a Brandschutznachweis number for another Land's GK bands. Cross-reference instead of duplicating: `fire-protection-building`, `building-acoustics`, `building-physics-thermal-moisture` own the numbers; this skill owns *bindingness and package structure*.
12. **Silence about the signature chain.** A technically perfect answer that never says *who signs* the submission is incomplete — the Berechtigung question is the legal load-bearing wall of the whole procedure.
13. **Austria/Switzerland transplant.** German §-numbers and GK logic presented as if federal/ cantonal-neutral (Austria has no federal building code and Switzerland no federal building permit; §11.6).

## Section 19: How to Answer Regulatory Questions — the Playbook

### 19.1 The six-step method

```
1. CLASSIFY  — which of the four questions (§2.2 tree)? Often several at once:
   split the answer visibly by stack.
2. ESTABLISH — Bundesland, parcel, plan status, GK, new/existing, date. Missing
   fact → say WHICH conclusion it blocks ("no GRZ answer until the plan text is
   read; here is the read-out method meanwhile").
3. NAVIGATE  — name the binding documents in order: B-Plan (text Nr. + sheet),
   LBO § of THAT Land, introduced-rule list, GEG §, Satzung, BauNVO §.
   Cite per this skill's Section 22 discipline — statute,
   provision, edition. If you cannot name it, you are not allowed to conclude it.
4. APPLY     — compute the envelope (coverage/floor-area/height/distance tests);
   run the tier test for every technical figure; route physics/fire/acoustics/
   accessibility computations to the owning skill and *carry the tier label through*.
5. PACKAGE   — output = what passes / what fails / what is blocked, with the
   documents the user must obtain (B-Planauszug, Liegenschaftskarte, Baulasten-
   auskunft, Satzungstexte) and the persons they must engage (Entwurfsverfasser,
   Tragwerksplaner, nachweisberechtigter Brandschutz, Energieberater-class).
6. GATE      — end with: chamber signatures + permit/exemption before building;
   deviations declared; continuing duties (Prüfungen, EWS, Melder) named.
```

### 19.2 Answer templates

**Unknown Land/parcel:** *"Before any number: which Bundesland, and is there a B-Plan for the parcel? The distance rule, the procedure track, the exemption for small houses and the statics-review duty all change at the state border — and the density figures live only in your parcel's plan text. Here is how to get each in one page (§4, §5)... meanwhile the method you can apply is..."*

**Two states' rules conflict (user quotes a different Land):** *"Both are real — they're from different states. [Land A]'s LBO §… says X; [Land B]'s equivalent is Y; the MBO §… is only the model, it binds nobody directly. Your parcel is in [B], so Y governs — verify against the current state law portal text."*

**§34 derivation:** *"There is no numeric rule here — the envelope is derived from the surrounding development. Which buildings face your street within ~100 m, at what height and use? Photographs + a measurement table, not a vibe. I can structure the derivation; the Bauaufsicht will demand the table."*

**"Is the plan genehmigungsfähig?":** *"I can check it against every document I've seen (plan text, LBO §…), and I list what passes, fails and is unverified. But genehmigungsfähigkeit is a signature with chamber standing — hand this compliance matrix to your Entwurfsverfasser for the sign-off, and the authority decides, not the model."*

**"We'll just get a Befreiung later":** *"Befreiung/Abweichung is a discretionary exception requiring an individual-case justification and often compensation; it is not a correction channel for avoidable breaches, and in a Freistellung the exception route doesn't even exist — the project must simply conform. If the plan only works via an exception, the plan needs to change."*

**Contract-regime question:** *"First: is VOB/B adopted wholly in the contract? The Abnahme effects, the 4- vs 5-year warranty and the deviation-pricing rules depend on nothing else more. I map the differences (§12); for a live claim this needs a Fachanwalt or the Kammer's Schlichtungsstelle."*

**"The neighbour says the setback is too small":** *"Three separate layers: the LBO distance rule for THIS Land (recompute H from the defined terrain), whether the B-Plan/Baulast secures the line, and the civil-law claim, which the permit does not extinguish. Start with the Baulastenauskunft and the Abstandsflächen math on the approved plan; escalate to counsel if the private claim is asserted."*

---

## Section 20: FreeCAD / BIM Integration — Modelling the Legal Envelope

Pair this skill with the modelling siblings. The German-specific discipline differs from other jurisdictions in one datum rule: **the binding vertical datum is the LBO-defined Geländeoberfläche, not the road crown** — heights, H for Abstandsflächen and the Vollgeschoss test all key off the defined terrain model. Build the compliance envelope as geometry so violations are visible, not arithmetic:

```python
# Parametric intent — NOT construction geometry. All plan figures come from the
# parcel's own B-Plan; placeholders here are T1-V examples only.
GRZ, GFZ           = 0.4, 1.2        # VERIFY from plan text; test footprint & floor-area separately
VG_MAX             = 2               # "Vollgeschosse" per plan definition
WANDH_MAX          = 8.5             # plan definition of Wandhöhe
ERDOBERFLAECHE     = ...             # named datum: defined avg terrain per the Land's H formula
ABSTAND_FAKTOR     = 0.4             # LBO of THIS Land — VERIFY (some 0.5; some segmented-H)
ABSTAND_MIN        = 3.0             # MBO-family minimum; the 0.4H band crosses it at H = 7.5 m

# 1. Baufenster polygon(s) → extruded to height test: BUILDABLE = prism ∩ height
# 2. No-build volumes: everything outside Baufenster + all Abstandsflächen solids
#    (build per wall SEGMENT: H_segment + roof add-on, then extrude a·segment_length)
# 3. Compliance assertions — run, do not eyeball:
#      house ⊆ Baufenster-prism
#      common(house, abstands_volume) volume == 0
#      Σ footprint / A_plot ≤ GRZ        (with the plan's counting definition as a parameter)
#      Σ floorarea / A_plot ≤ GFZ        (Vollgeschoss logic, not "nice floors")
#      wandhoehe (terrain→wall top) ≤ WANDH_MAX; firsthoehe ≤ plan max; VG count ≤ VG_MAX
#      roof pitch within the Festsetzung band if a pitched-roof duty exists
# 4. Datum objects in the model: GELANDEOBERFLAECHEN_DURCHSCHNITT, each wall segment's
#    H measurement line, the VG test line ("covered > ½ but < ⅔ above terrain").
# 5. Tolerancing honesty: legal distances must hold in REAL distance — when a survey
#    coordinate system is involved (ETRS89/UTM with projection reduction), set out and
#    verify at the object scale (the project-measure/Projektmassstab rule from surveying
#    practice): never let a "−4 cm/100 m" projection distortion shorten an Abstandsfläche
#    or a Grenzmaß — those are *legal* distances.
```

**Attribute discipline (why a house model should carry its tier tags).** Tag model objects with the fields the dossier and the future digital submission (XBau/XPlanung-style message layers, LOIN per EN 17412: LOG + LOI + documentation) will demand: Raumname + usage, Geschoss + VG-status, Wandhöhe + H datum, Feuerwiderstandsklasse (introduced product class), U-value per GEG component, Stellplatz count. A model whose attributes reconcile with the Berechnungen sheets is what makes the §5.3 "sheet-to-sheet consistency" rule executable instead of aspirational.

**Objects that each carry independent limits (model separately, assert separately):** the DG/Vollgeschoss question (its own height test), basement vs terrain datum (it can *become* a Vollgeschoss on sloped sites), garage/Nebenanlage length along the boundary (the 9/15-m family caps), PV/heat-pump placement vs boundary and vs the Nachbarschutz emission logic, the Feuerwehrzufahrt band (width/height/turning), Brandwand openings, Baufenster-included vs -excluded projections (the privileged-projection math §11.1), trees under a Baumschutzsatzung, and the smoke-alarm coverage graph.

**What the model is and is not:** a compliance envelope + massing study + attribute base for the dossier. Not a Bauvorlage, not a Nachweis, not evidence of approval. Say this in the same message that delivers the model.

---

## Section 21: Pre-Submission Compliance Checklist

Run before ever telling a user a design "sollte genehmigungsfähig sein" — and attach it to the handoff to the signing designer as the *compliance matrix*, not as a claim of approval.

**Plan layer (BauGB / B-Plan — T1)**
- [ ] B-Plan nr., plan-text date, and validity status identified; if none: §34 reference table built (or §35 → blocked)
- [ ] Usage type (incl. WE count, home office, guest unit, Ferienwohnung) inside the Art-der-Nutzung permission
- [ ] GRZ with the plan's counting definition stated (garage? paths? terraces? overhangs?) — computed, not estimated
- [ ] GFZ computed on the legal floor-area rule with the Vollgeschoss classification of every floor (DG question answered explicitly)
- [ ] Wandhöhe / Firsthöhe / VG-count / Dachform / Dachneigung each checked against their own Festsetzung
- [ ] Baufenster satisfied by boolean, per storey; projections privileged or declared
- [ ] Sondergebiet purpose / WE-cap / min-size / Stellplatzschlüssel / Fahrrad / Grün / Entwässerung / Lärm-coverage Festsetzungen each ticked
- [ ] Erschließung secured (access right, sewer/storm plan, contributions clarified)
- [ ] Baulastenauskunft pulled and respected; Zufahrts-/Leitungsrechte real
- [ ] Erhaltungssatzung / Veränderungssperre / Milieuschutz / Denkmalliste / Kampfmittel / Wasserschutz checked as area screens

**Order layer (LBO of the named Land — T2)**
- [ ] Gebäudeklasse determined on the terrain datum, boundary cases argued (§5.2)
- [ ] Procedure track fixed: permit / simplified / Freistellung / Anzeige / verfahrensfrei — with the Freistellung *preconditions* individually proven or the track abandoned
- [ ] Abstandsflächen recomputed with the Land's factor + minimums + roof add-on + segment/fiktive-Wand logic; both B-Plan and LBO lines on the same drawing
- [ ] Rettungswege, notwendiger Treppenraum (if GK4+), Brandwand at boundary, Melder, small-building fire family — from `fire-protection-building`, with the LBO § cited
- [ ] Verfahrensfrei catalogue not abused (size caps per part AND combined); Baudenkmal override considered
- [ ] Nachbarbeteiligung requirements of this Land met (objections, consents, Baulast where distance crosses)
- [ ] Abweichungen: none hidden — each declared with §10.2 five-part argumentation

**Technical-proof layer (T3–T5)**
- [ ] Every introduced-norm figure: Land + Liste der Technischen Baubestimmungen edition + norm edition stated
- [ ] Wärmeschutznachweis (GEG current edition; heating-carrier rules for the municipality's heat-plan status) by a person with GEG §88 entitlement
- [ ] Schallschutznachweis to DIN 4109 (introduced minimum) AND the contract standard (VDI 4100/DEGA) identified separately if sold/let at higher standard
- [ ] Immission direction: TA Lärm/16. BImSchV/DIN 18005 interlock done for sensitive adjacency (heat pump, Lüftung, neighbours' trade)
- [ ] Barrierefrei/-armut duty or Förder condition named; Stellplatz/ Fahrrad counts reconciled with satzung
- [ ] Prüfpflichten: Prüfstatik trigger checked for this Land + GK; brandschutz concept for any Sonderbau trigger; SiGeKo duty noted (multi-employer rule)

**Package & signature layer**
- [ ] Bauvorlagen per Land BauVorLVO complete: Lageplan (qualified), all sheets, Berechnungen reconciled, Baubeschreibung, Nachweise, statistics forms
- [ ] Every signing person's *list entry in the correct Kammer with the correct scope* verified (Entwurf / Tragwerk / Brandschutz / Energie)
- [ ] Deviation/Befreiung/Abweichung applications + Begründung attached, not "explained later"
- [ ] Timeline communicated: Einvernehmen + authority + any Nachbarfrist; validity/extension clause of the coming permit noted
- [ ] Post-permit duties handed over: Baubeginnsanzeige, change-deviation rule, Fertigstellungsmeldung/confirmation pattern, as-built EWS, continuing Prüfungen
- [ ] Liability layer stated to the user in plain words: this is a planning envelope; the signatures and the permit are someone else's professional act, and they come before any ground is broken

## Section 22: Citation Discipline and the Verification Protocol

1. **Name the stack first** (plan / order / technical rule / contract), then the statute, then the provision, then the edition. "§6" without "welches Landes, welche Fassung" is not a citation.
2. **MBO ≠ law; LBO = law.** Every MBO-derived statement carries "Muster; Landesfassung prüfen".
3. **DIN ≠ law by itself.** State the bindingness route (introduced / Zulassung / aRdT / none) per §1.1 before any DIN figure; quote edition years (DIN 4109-1:2018-01, DIN EN ISO 6946:2018-03 family — the edition years named here are anchors, not guarantees).
4. **Date everything volatile:** GEG amendments (2023/24 heating-law wave), HOAI 2021 + ECJ 2019 status, VOB (2019/2024-era editions), Eurocode NA reissue wave (2022+), EU thresholds (biennial), each LBO reform. A rule without a vintage is a rumor.
5. **Separate cited / derived / placeholder.** B-Plan figures read from the parcel's text = T1. Figures "typical" = T1-V, spoken aloud as unverified. §34 figures = argued, never asserted. US/international analogs = never admissible for German planning tests at all.
6. **Reconcile arithmetic before publishing** (GRZ vs the survey area; H vs the terrain datum; VG vs the ½/⅔ test; the 3-m-minimum crossover at H = 7.5 m) — and disclose the *definition* used for each computed quantity (floor area by which rule? footprint counting the porch?).
7. **Say "blocked" over guessing.** A wrong Abstandsflächen factor becomes a stilling; the honest answer names the lookup: **"the current consolidated text of [Land]s Bauordnung and its Liste der Technischen Baubestimmungen is published on the state's law-information portal (Gesetze-und-Verordnungen platform / Ministerialblatt / Justizportal des Bundes und der Länder); the B-Plan text and any örtliche Satzungen at the Gemeinde (often their GIS/XPlanung geo-portal); Baulasten at the untere Bauaufsichtsbehörde on request; introduced-norm editions via the Beuth/DIN portal; Zulassungen/abP via DIBt's public site; HOAI/VOB current editions via the respective publisher; and the binding reading in every individual case is the Kammer professional's or Fachanwalt's."** Then offer to structure the documents once the user supplies them.
8. **Never let output look official.** No signature blocks, no "Antrag" with fabricated Aktenzeichen, no Prüfstempel styling, no Energieausweis layout — those are the professional acts the gate exists to protect.

## Section 23: Glossary — German Permit Vocabulary (EN glosses)

| Term | Meaning |
|---|---|
| **BauGB / Baugesetzbuch** | Federal building code (planning law framework; BauNVO = its usage/measure ordinance) |
| **FNP** | Flächennutzungsplan — preparatory municipal land-use plan; binds administration, not citizens |
| **B-Plan / Bebauungsplan** | binding qualified development plan (Satzung) for a defined area |
| **Festsetzung** | a binding plan provision (text or drawing); "Hinweise" are not Festsetzungen |
| **GRZ / GFZ / OWZ** | site coverage / floor-area / storey-count numerals; OWZ = the plan's above-ground-full-storey count notation — read the legend |
| **Bauweise** | offen / geschlossen / Gruppenbauweise / Grenzbauweise — detachment & boundary-build rule |
| **Baufenster / Baugrenze / Linie** | buildable polygon / outer boundary line / alignment line |
| **Vollgeschoss** | floor whose covering lies > ½ (full) above the defined average terrain — legal definition per §20 BauNVO/plan |
| **Wand-/First-/Traufhöhe** | plan-defined heights of wall top / ridge / eaves — three different datums |
| **Sondergebiet (SO)** | plan-designated special area (§11 BauNVO) with its own purpose definition |
| **Baugenehmigung** | the building permit; **Bauvorlagen** the submission set; **Bauvorlageberechtigung** the right to file it |
| **vereinfachtes Verfahren / Genehmigungsfreistellung / Anzeigeverfahren** | the three lighter procedure tracks (state-specific!) |
| **Entwurfsverfasser / Bauleiter / Tragwerksplaner** | design author / site supervisor / structural designer — the signature chain |
| **Prüfstatik / Prüfsachverständiger** | third-party statics (and fire) review, trigger differs by Land |
| **Abstandsfläche (a) / Wandhöhe (H)** | required boundary setback depth / its measuring height |
| **Grenzbebauung / Baulast** | building on the boundary where planning law permits it / a publicly registered land burden securing neighbourly conditions |
| **Abweichung / Ausnahme / Befreiung** | LBO deviation / plan-reserved exception / plan waiver (discretionary) |
| **Bestandsschutz** | protection of a lawfully created existing condition (not of future additions) |
| **aRdT** | allgemein anerkannte Regeln der Technik — proven state of technical knowledge |
| **Technische Baubestimmungen** | the Land's VV-list of introduced (legally binding) technical rules |
| **Bauregelliste A/B/C** | the construction-products rule lists (approval-type vs CE/hEN vs neither) — quote carefully, MVV TB overlaps |
| **MVV TB / abP / Zulassung** | fire product/administrative regulation / general type approval / technical approval |
| **MBO / LBO / LBauO** | model / state building code(s) |
| **GEG / EWS** | building energy act / Energieausweis (energy performance certificate) |
| **TA Lärm / BImSchV** | noise instruction / federal immission-control ordinance (+16./18. traffic & sport) |
| **HOAI / LPH / anrechenbare Kosten / Honorarzone** | fee ordinance / its service phases / assessable net construction cost / fee band |
| **BGB-Werkvertrag / VOB/B / VOB/C (ATV) / VOB/A** | civil code contract / contractual construction terms / execution-and-billing rules / tender rules |
| **Abnahme / Mangel / Verjährung / Abschlag** | acceptance / defect / limitation / progress payment |
| **Bauträger / Verbraucherbauvertrag / MaBV** | developer sale model / consumer build contract (staged-payment law family) |
| **VgV / GWB / Schwellenwert** | award ordinance / competition part of the act / EU threshold (biennial!) |
| **AIA / BAP / CDE / Data Drop / LOIN** | BIM requirements / BIM execution plan / common data environment / contractual model handovers / level of information need (EN 17412) |
| **XBau / XPlanung** | digital submission message standard / exchange format for plans |
| **SiGeKo / BaustellV / RAB** | site safety & health coordinator / site ordinance / the coordinator rules |
| **Untere Bauaufsicht / Bauamt / Gemeinde** | the permit-grading authority (Land-level!) vs municipality (planning + Einvernehmen) |

## Section 24: Related Skills and Where Each Question Leaves This File

| Question type | Route to |
|---|---|
| Plot-to-envelope arithmetic, brief fitting, room program | `building-planning-spatial` |
| Fire resistance, escape routes, Brandschutznachweis content | `fire-protection-building` |
| Sound proof (DIN 4109 math, VDI 4100/DEGA contract levels, TA Lärm/heat-pump emission) | `building-acoustics` |
| U-values, GEG balancing, moisture, summer heat | `building-physics-thermal-moisture` |
| Barrier-free layout (18040), lift, ramps | `accessibility-universal-design` |
| Stair geometry per LBO bands | `stairs-vertical-circulation` |
| Structural verification & Eurocode/NA computation | `structural-analysis`, `concrete-detailing`, `timber-steel-design`, `masonry-construction`, `geotechnics-foundations` |
| Roof/wall/window make-up compliance | `roofing-waterproofing`, `openings-windows-doors`, `construction-detailing`, `masonry-construction`, `building-materials` |
| Typology & unit mix | `building-typology` |
| Model & drawing production of the envelope | `construction-freecad-bim` / the modelling siblings |
| Cost planning DIN 276, fee comparison | the cost/estimation skill (`construction-cost-management-din276`) |

---

## Appendix A — The Numbers Worth Re-Verifying First (highest-churn list)

| Item | Why it moves | Re-check at |
|---|---|---|
| GEG heating rules & existing-building duties | amended 2023/24 onward; municipality heat plans stage them per town | GEG current text + the Gemeinde's Wärmeplan status |
| Abstandsflächen factor/minimums/privileges per Land | LBO reforms (e.g. the 0.4H/3-m family, segment-H variants, projection bands) | that Land's LBO §5/§6 + its latest reform |
| Prüfstatik/Prüfsachverständige triggers | periodic liberalisation waves (GK1–3 exemptions with liability shift) | Land's Prüfsachverständigen-VO |
| Freistellung preconditions (GK bands, area types) | touched by almost every LBO reform | Land's procedures clause |
| EU award thresholds + VOB/A paragraph numbers | biennial EU revision | current Bundesanzeiger/EU publication |
| HOAI default-fee effect | post-ECJ; edition checks; AHO sheets for non-HOAI services | HOAI current annexes + case law summary |
| Eurocode national annexes (γM, snow/wind zones) | 2022+ NA reissue wave; climate maps drift | current DIN EN 199x/NA + zone maps |
| Introduced-rule editions (DIN 4109, 4108, 18040, 1946-6...) | the Land's Liste der Technischen Baubestimmungen per edition | that VV, current issue |
| Stell-/Abstellplatz and Entwässerung statutes | municipal — change per resolution | the Gemeinde's Satzung database |
| Melder / smoke-alarm transition tails | expired nearly everywhere; product & maintenance duty remains | Land clause + DIN EN 14604/14676 |

**End state of every answer from this skill:** a tiered, statute-named, state-named, edition-dated position; the documents the user must obtain; the professionals who must sign; and one sentence that decides everything downstream — *build nothing before the permission is in hand and every deviation in it is declared.*
