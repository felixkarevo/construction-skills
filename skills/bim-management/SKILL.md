---
name: bim-management
description: >
  BIM-Abwicklung und Informationsmanagement (DACH) nach DIN EN ISO 19650 und VDI 2552:
  Anforderungskette OIR/PIR/AIR → EIR(AIA) → BAP (Angebots-/Projekt-BAP, MIDP/TIDP,
  Data Drops) plus FM-seitige LIA; CDE-Workflow mit Statusmodell (WIP → Shared →
  Published → Archived), Freigaben, Versionierung/Revision, GUID-Disziplin,
  Langzeitarchivierung; Dateinamen-/Plancodierung als Facetten-Struktur; LOIN
  (EN 17412) und LoD/LOD-Tabellen (BIMForum 100–500, HOAI-MDG-Mapping, VDI 2552-4
  inkl. LOD 600, Element-/Attributmatrizen); Anwendungsfall-Katalog je
  Lebenszyklusphase mit Auswahlregeln (modellgestützt/modellbasiert,
  Mindestinformationsprinzip); Rollen nach VDI 2552-7 (BIM-Management, Gesamt-/
  Fachkoordination, Modellautor, Nutzende, BIM in Bauleitung und Betrieb);
  föderierte Modelle und Koordinationszyklen; Modellprüfung (MVD-/Attribut-/
  Regel-/ACCC-Checks, Quality Gates) und BCF-Issue-/Mängelmanagement;
  Clash-Detection-Workflow mit Kollisionsmatrix und Servicezonen; IFC-/MVD-/
  Pset-Anforderungen je Disziplin inkl. Versionspindung IFC2x3/IFC4,
  Klassifikation (ISO 12006, DIN SPEC 91400, CAFM-Connect) und Nachbarformaten
  (BCF, COBie, gbXML, GAEB); Vergabe und Vertrag (AIA als Vertragsbestandteil,
  Eignungs-/Zuschlagskriterien, Angebots-BAP-Wertung, HOAI Besondere Leistung,
  BIM-BVB-Muster, Datenrechte/UrhG, Haftung, reliance level, Herstellerdaten);
  digitale Objektübergabe (PIM→AIM, As-Built-QA, Betriebsmodell-Reduktion,
  AKS/KKS-IDs, Raumbuch/Anlagenliste, drei CAFM-Integrationsszenarien,
  Fortschreibungs-Loop, Scan-to-X, Wirtschaftlichkeit); 4D/5D-
  Datenvoraussetzungen mit Querreferenzen zu construction-scheduling-site und
  cost-management-din276; Pilotprojekt-Regeln; Checklisten (EIR-Review,
  BAP-Audit, CDE-Setup, Data-Drop-Abnahme, Handover-Abnahme) und Glossar.
  Modellierungs-Mechanik liegt NICHT hier, sondern im FreeCAD-Authoring-Skill —
  dieses Skill regelt Prozess und Daten. Use when planning, tendering,
  contracting, coordinating, checking or handing over BIM deliverables.
---

# BIM-Management & Informationsmanagement (DACH)

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

Dieses Skill behandelt **Prozess und Datenmanagement** der BIM-Methode: welche
Anforderungen vor Projektstart feststehen müssen, wie Modelle über eine CDE organisiert,
geprüft, koordiniert und übergeben werden, und was in Verträge und Ausschreibungen gehört.
Es beantwortet nicht, *wie* Geometrie erzeugt wird — dafür existiert
`construction-freecad-bim` (Modellierungs-Mechanik, IFC-Export). Die Grenze ist bewusst:
ein technisch sauber gebautes Modell, das vereinbarte Attribute zum falschen Zeitpunkt
nicht liefert, ist ein Management-Problem — und umgekehrt.

**Zeitstand:** Quellenlage ≈ Stand 2020–2021 (Stufenplan, BIM4INFRA2020,
DB-/DEGES-Programme, Normnummern); Bezeichnungen und Normausgaben können heute abweichen
[VERIFY gegen gültige Fassungen]. Rechtsstände (HOAI, VOB, UrhG, Landesrecht) vor
Vertragsaussagen aktuell prüfen — kein Ersatz für Rechtsberatung. **[VERIFY]** =
verdichtete Tabelle/Datiierungsrisiko, vor Vertrags-/Abnahmeverwendung gegen Primärquelle
prüfen; **[Praxis]** = Üblichkeit, keine Normforderung.

## Reality Check — Rolle & Verantwortung

**Das Skill liefert Struktur, Checklisten und Prüflogik — keine rechtsverbindlichen
Aussagen.** AIA/EIR, BAP und Vertragsanlagen bleiben individuelle Projekte; das Skill gibt
Gerüst und Prüffragen, nicht das ausgefüllte Dokument. BIM erzwingt **kein neues
Haftungsregime**: jede/r Beteiligte haftet weiter für den eigenen Beitrag, Nutzung von
Fremdmodellen erfolgt im vereinbarten Verlassensgrad; eine stillschweigende
Garantieübernahme existiert nicht. Nutzungsrechte an Modell-/Datenbeständen müssen
**ausdrücklich und zweckbezogen** eingeräumt werden (13).

**Verhaltensregel:** Verlangt der Nutzer ein „unterschriftsreifes“ Dokument, dem
projektbezogene Festlegungen (Koordinaten, Termine, Verantwortliche, LoD-Matrizen) fehlen,
werden diese Stellen als **Lücke mit Hinweis** ausgegeben, nie als erfüllt erfunden.
Erfundene Firmennamen, Aktenzeichen oder Norm-Passagen sind tabu.

---

## Abschnitt 1: Warum Prozess vor Software

### 1.1 Grundlogik

- **BIM (Building Information Modeling / Bauwerksdatenmodellierung)** = durchgängige,
  konsistente Nutzung digitaler Bauwerksinformationen über den Lebenszyklus (Entwurf → Planung
  → Ausführung → Betrieb → Rückbau); die deutsche Stufenplan-Definition (BMVI 2015) fasst es
  als *kooperative Arbeitsmethodik* mit konsistenter Erfassung, Verwaltung und transparentem
  Austausch/Übergabe lebenszyklusrelevanter Daten.
- Kernproblem konventioneller Abläufe: **Informationsbrüche** — Pläne nicht
  maschineninterpretierbar, Konsistenz nur manuell prüfbar, Änderungen als „Revisionswolke“
  (revision cloud); Fehler zeigen sich spät, in der Ausführung, teuer. BIM ist **Methode,
  nicht Software**: Werkzeuglandschaft (Autorssoftware, CDE, Model Checker, Simulations-, 4D-,
  AVA-, FM-Tools) ist Mittel; die Leistung ist der **durchgängige Datenfluss mit minimalem
  Datenverlust**. Semantik neben Geometrie (Elemente als Instanzen definierter Klassen) ist
  Voraussetzung für normgerechte Planableitung, Simulation und maschinelle Prüfung.
- **MacLeamy-Kurve**: Aufwand verlagert sich in frühe Phasen, wo Änderungen billig sind —
  Hebel ist Vorverlagerung von Entscheidungsqualität, nicht das 3D-Bild. Wirtschaftlicher
  Hintergrund [VERIFY Zahlen zitiert nach Stand der Quelle, US-Daten 2002]: mangelnde
  Interoperabilität kostete ~15,8 Mrd. US-D/Jahr; Eigentümer/Betreiber trugen ~68 %, 85 %
  davon in der Betriebsphase — FM-Datenqualität ist der eigentliche Business Case.

### 1.2 Nutzungsstufen und Reifgrade

- **little BIM vs. BIG BIM**: Insellösung eines Fachplaners (Modell → Pläne, keine
  modellbasierte Koordination nach außen) vs. konsequent modellbasierte Kommunikation aller
  über alle Phasen. **Closed vs. Open BIM**: proprietäres Ökosystem vs. herstellerneutrale
  Formate (v. a. IFC); Ziel für Lebenszyklus-Datenhaltung = Big Open BIM.
- **Maturity Level 0–3**: 0 = 2D-CAD/PDF; 1 = 3D koexistent mit 2D, Einzeldateien; 2 = native
  Fachmodelle, vertraglich geregeltes föderiertes Koordinationsmodell + Kollisionsprüfung (PAS
  1192-2 → ISO 19650; in DE Basis der Stufenplan-Leistungsstufe 1); 3 = integriertes
  objektgranulares Modell — nirgends verbindlich eingeführt. Praxis-Korrektiv: auch in
  Level-3-Projekten hat sich das Mono-Gemeinschaftsmodell nicht durchgesetzt (Organisation +
  Haftung) — Realität = Fachmodelle, regelmäßig zu Koordinationsmodellen zusammengeführt.

### 1.3 Warum herstellerneutrale Formate + Mandatslage

- Fragmentierung: ~93 % der EU-Bauunternehmen < 10 Beschäftigte; Planung ≠ Ausführung;
  wechselnde Büros; Ad-hoc-Partnerschaften. **Öffentliche Vergabe** darf wettbewerbsrechtlich
  keine Software erzwingen; EU-RL 2014/24/EU (Art. 22) erlaubt die Pflicht zu elektronischen
  Werkzeugen (inkl. BIM) — dann mit gleichwertigen offenen Formaten. DXF/DWG = Pseudo-Standard
  (2D + Layer-Rudimente), für BIG BIM unzureichend.
- Mandatslage DACH (datiert): DE Stufenplan 2015 (Leistungsstufe 1 = Level 2), BIM4INFRA2020
  mit AIA-/BAP-Vorlagen + Muster-BIM-BVB, BIM Deutschland (2019/20), Masterpläne
  Bundeshochbau/-fernstraßen 2021, Prüfpflicht-Schwelle 5 Mio. € Einzelbaukosten (Erlass 2017,
  eingeschränkt umgesetzt); AT ÖNORM A 7010-6; CH „Bauen Digital Schweiz“. Vergleich
  (Schwellen-Logik): UK Level-2-Pflicht 2016, FI > 1 Mio. € 2007, KR > 50 Mrd. Won 2016, SG
  Pflicht-Einreichung 2004 inkl. maschineller Code-Prüfung. [VERIFY Programm-/Rechtsstand]

---

## Abschnitt 2: Die Anforderungskette — OIR/PIR/AIR → EIR(AIA) → BAP (+LIA)

### 2.1 Pyramide und Dokumentlogik

```
OIR (organisatorische Informationsanforderungen — strategisch: Asset-/
    Portfolio-Management, Regularien)
 ├→ PIR (Projekt-Informationsanforderungen — Projektziele)
 ├→ AIR (Asset-Informationsanforderungen — Betriebsbedarf → AIM)
 └→ EIR = AIA (Exchange Information Requirements ≙
    Auftraggeber-Informations-Anforderungen) — LASTENHEFT, i. d. R.
    Vertragsbestandteil
        ↓
    BAP ≙ BEP (BIM-Abwicklungsplan / BIM Execution Plan) — PFLICHTENHEFT
    des AN: WIE wird geliefert
        ↓
    Lieferungen = Informationscontainer (Modelle + Dokumente) zu
    Datenübergabepunkten (Data Drops), geprüft → freigegeben → archiviert;
    PIM (Projekt) → AIM (Asset) bei Objektübergabe
```

- ISO 19650 trennt **Informationsbesteller** (requester) / **Informationsbereitsteller**
  (provider); AG-Dokument formal EIR, DACH-üblich AIA — in grenzüberschreitenden Dokumenten
  beide nennen. **AIA ↔ BAP = Lastenheft/Pflichtenheft** (VDI 2552-10): AIA unveränderlich
  (Ziele, Anwendungsfälle, Modellinhalte, Formate, Übergabetermine, Rollen, Prüfprozesse); BAP
  die Antwort: Software, Modellaufteilung, Verantwortliche, Prozesse, Koordinationszyklen.
- **Angebots-BAP vs. Projekt-BAP**: vor Vergabe grobes Vor-/Angebots-BAP als
  Bewertungs-/Zuschlagskriterium (zweistufiges Verfahren), nach Zuschlag fortgeschrieben zum
  **Projekt-BAP** (kollaborativ, Federführung Gesamtkoordination). Zunehmende Regel: BAP
  entsteht **nach** Beauftragung aller Beteiligten („Planung der Planung“) — dann müssen
  wesentliche AG-Vorgaben bereits in der AIA stehen (ein Bauvertrag ohne Terminplan ist auch
  nicht fertig). Vertraglich klären, ob der BAP geschlossene Regelungen ändern kann [VERIFY
  Musterformulierung der Vergabearchitektur].
- Internationale Vertragsanker als Vergleichsmaterial: BIM-Addenda/-Protokollformulare regeln
  Datenhoheit, Zweck, Nutzung, Vertraulichkeit — Muster immer checklistenartig anpassen, nie
  schematisch übernehmen.

### 2.2 AIA-Inhalte (Gliederung nach VDI 2552, sinngemäß)

| Block | Inhalt | Prüffrage |
|---|---|---|
| Formalien | Geltung, Querverträge, Glossar | eineindeutig ohne projektbezogene Definitionen? |
| Projektdaten | Ziel, Meilensteine, Struktur | Data Drops = echte Entscheidungs-/Zahlungstermine? |
| Ziele → Anwendungsfälle | BIM-Ziele, Use-Catalog, Übersetzungsmatrix | jeder Fall mit Nutzen-Empfänger? |
| Rollen | Besetzung, Qualifikation, Schulung | als Eignungskriterium in der Vergabe? |
| Datenmanagement | Formate, Schnittstellen, open/closed BIM, Data Drops, CDE | Versionierung/Freigabe/Ablage geregelt? |
| Modellinhalte | LOG/LOI(/DOC), Element-/Attributmatrizen | je Objekttyp je Termin konkret? |
| QA/Prüfprozesse | Modellprüfung, Kollision, Freigabeabläufe | wer prüft wann gegen welche Regelbasis? |
| Leistungsfeststellung | AIA-Konformität bei Abschlagszahlung/Phasenende | Zahlung ↔ geprüfte Lieferung verknüpft? |

**Über-Spezifikation vermeiden** (explizite VDI-2552-10-Regel): Funktions- statt
Detallbeschreibung, wo möglich; maschinenlesbar formulieren (Objekt-/Attributlisten je
Phase); Detailtiefe, die niemand braucht, wird bezahlt und nicht gepflegt. Umgekehrt: Was
der Betrieb braucht, muss **früh** rein — späte Datennacherfassung ist der teuerste
Fehler. Mehrere AIA über Projektphasen sind zulässig und bei Phasenvergabe üblich.

### 2.3 BAP-Inhalte (Kernblöcke)

- Personen + Qualifikation je Rolle (inkl. Vertretung); Organigramm; Modellerzeugung + interne
  QA; **Herangehensweise je Anwendungsfall** (Kernstück).
- **Föderationsstrategie**: Teilmodelle je Gewerk/Zone/Bauabschnitt, Modellgrenzen, wer führt
  zusammen; Verantwortlichkeiten (RACI je Lieferung); Bereitstellung/Freigabe über CDE
  („Single Source of Truth“); Austausch mit Dritten (vertragsbezogen, 13).
- Softwarelandschaft: Erzeugnisse, Versionen, Schnittstellen, IT-Infra (Versionspinung der
  Austauschformate!); Lieferpläne **MIDP** (alle Lieferungen zu Meilensteinen) + **TIDP** (je
  Akteur — Zuordnung und Verantwortungsübergabe je Arbeitsergebnis).
- Herausforderungen: Fortschreibung ist **Dauerleistung** (kalkulatorisch im Angebot
  berücksichtigen); AIA-Konformität vs. kontrollierte Abweichung (abgestimmt dokumentieren);
  Widerspruchsfreiheit mit Projekthandbuch.

### 2.4 LIA — FM-seitige Erweiterung (DACH-Praxis)

**LIA (Liegenschafts-Informations-Anforderungen)** = gebündelte, portfolioübergreifende
Betriebs-Anforderungen von Eigentümer/Betreiber; speist die AIA jedes Einzelprojekts. Neun
Blöcke: 1 BIM-Anwendungsfälle, 2 bereitgestellte digitale Grundlagen, 3 digitale
Liefergegenstände, 4 Organisation/Rollen, 5 Zusammenarbeit, 6 Lieferzeitpunkte, 7
Qualität, 8 Modellstruktur/-inhalte, 9 Technologie. **Regel:** aus den FM-Prozessen heraus
formulieren (Wartung ≠ Flächenmanagement ≠ Reinigung), über Projekte hinweg
wiederverwenden, als Anlage in die AIA integrieren — sonst bleibt Betreibervision Papier.
[VERIFY LIA = Praxis-/Verbandsniveau, keine Norm.]

### 2.5 Mindestinformationsprinzip

LEITREGEL (aus der Straßenbau-Praxis, übertragbar): Informationsgrad je Objekt = die
**kleinste Menge, die den Anwendungsfall erfüllt**; alles darüber ist Verschwendung
(lean). Datengranularität ist mindestens so wichtig wie Geometrie-Granularität; beide
unabhängig definierbar. Wirksamstes Mittel gegen den häufigsten Scheiterungsmodus:
„Datenmüll“ — ein Modell, das mehr enthält, als gepflegt werden kann.

---

## Abschnitt 3: CDE-Workflow — Statusmodell, Freigaben, Versionierung

### 3.1 Zweck und Grundprinzipien

- **CDE (Common Data Environment / Datenumgebung)** = zentrale Umgebung zum Sammeln,
  Verwalten, Auswerten, Teilen; jede/r holt Eingaben heraus, legt Ausgaben hinein; reduziert
  Redundanz, zentrale Aggregation + Archiv. Quellen: BSI PAS 1192 → DIN EN ISO 19650-1/-2, DIN
  SPEC 91391 (Funktionen, CDE-übergreifender Austausch), VDI 2552-5 [VERIFY Nummern].
  Auswahlkriterien: Angemessenheit (Ziel-Aufwand-Nutzen), Neutralität (produktunabhängige
  Prozesse), Anwendbarkeit (Kontext-universell).
- **Kleinste verwaltete Einheit nach ISO = Informationscontainer** (benannte Datei-Gruppe +
  Metadaten; strukturiert = Modelle/Pläne, unstrukturiert = Dokumente/Medien) — nicht das
  Einzelobjekt. CDE ≠ BIM-Server/-Datenbank (3.5).
- Grundsatz: **kein monolithisches Gemeinschaftsmodell** (Parallelbearbeitung,
  Haftungs-/Urheberschaftszuordnung) → föderierte, lose gekoppelte Fachmodelle mit klarer
  Autorenschaft je Element; viele Schnittstellen ⇒ Koordination nötig. **Austausch
  ausschließlich über die CDE** — kein bilateraler Austausch „am Projekt vorbei“, sonst bricht
  die Single Source of Truth.

### 3.2 Das Statusmodell (ISO 19650) — Kern des Workflows

```
[IN BEARBEITUNG / Work in Progress] — nur Urheber-Team sichtbar
     │ Prüfen/Bewerten/Freigeben: Abgleich gegen Informationslieferplan
     │ + vereinbarte Standards; nur bei Erfolg Statuswechsel
     ▼
[GETEILT / Shared] — für AG und Beteiligte SICHTBAR, nicht editierbar;
     dient Koordination + Vollständigkeits-/Genauigkeitsprüfung;
     bei Sicherheits-/Verteilungsanforderungen trennbar („Shared“ vs.
     „Shared with Client“)
     │ Überprüfung/Autorisierung: Korrektheit/Vollständigkeit/Genauigkeit
     ▼
[VERÖFFENTLICHT / Published] — zur Ausführung/Weiterplanung freigegeben;
     PIM am Projektende und AIM im Betrieb enthalten NUR Published-Daten
     ▼
[ARCHIVIERT / Archived] — vollständige Aufzeichnung aller je
     veröffentlichten Stände (Dokumentations-/Beweiszweck)
```

- Nicht bestanden → zurück auf „In Bearbeitung“; kein „halb-freigegeben“. Unterzustände aus
  PAS-1192-2-Zeit („Shared for coordination“, „Published for construction“, „as-built“) sind
  üblich — erlaubt, aber im BAP explizit definieren, sonst scheitern Automatisierungen an
  Zustands-Inflation.
- Je Übergang festlegen: **wer** setzt den Status, **welche** Prüfung ist Pflicht (Model
  Checker / manuell / Fachkoordination), **wann** fällig (Data Drop). Ohne diese Tabelle ist
  die CDE ein Laufwerk. PIM endet mit einem **Published-Stand**; alles andere ist Projektmüll
  oder Archivmaterial.

### 3.3 Versionierung, Revision, Freigabe

- Metadaten-Pflichtfunktionen je Ressource: identifizieren (ID/GUID, Autor), inhaltlich
  beschreiben, technisch (Format/Größe), funktional (Version/Revision/Status), konservieren
  (Backup/Archiv/Migration).
- **GUID/UUID-Disziplin**: Systeme müssen GUIDs **erhalten**, statt sie bei
  Export/Re-Konvertierung neu zu generieren — Neuguide zerstört Kollisions-, BCF-, Mängel- und
  CAFM-Referenzen (häufigste Bruchstelle; 14.3).
- **Versionsgraph** statt Liste: Version = Bearbeitungsstand; **Revision** = gebündelte,
  abgestimmte Stände nach Prüfung/Freigabe (Koordinationsmodell = Revision des Gesamtmodells);
  Alternative = parallel gepflegte Option. Freigabe = Signatur eines Berechtigten über eine
  **revisionierte** Ressource; digital: elektronische Signatur. Wird der Papierplan noch
  unterschrieben, muss die Modellfreigabe parallel und gleichwertig laufen — sonst gilt am
  Ende Papier.
- Nebenläufigkeit: **pessimistisch** (Sperre beim Auschecken, Sperrgranularität
  Modell/Layer/Element — innerbetrieblich) vs. **optimistisch** (Konflikttoleranz + Merge mit
  Abhängigkeits-Propagation — unternehmensübergreifend). GIT/SVN-artig nur für Text
  (Binärmodelle = Vollkopie); Dateivarianten erzeugen doppelte GUIDs → Referenzinkonsistenz.

### 3.4 Strukturvorbereitung (5 Schritte)

1. BIM-Anwendungsfälle definieren. 2. Datenstruktur aus Fall-Kombination ableiten. 3.
   Tool-/Formatkonzepte prüfen (Statusautomatik, Prüfserver). 4. **vertragliche Festlegung**
   (BAP/Modellierungsrichtlinie/AGB). 5. regelmäßige Konformitätsprüfung der **Ablage** (nicht
   nur der Modelle). Ordnungskriterien: **Bereiche** (Gewerkgruppen), **Phasen**, **Zonen**
   (Bauabschnitt/Geschoss), **Systeme** — metadatenbasiert, nicht nur Ordnerbaum; UID je
   Ressource unveränderlich (Referenz statt Datenkopie). Redundanz ok, Inkonsistenz nicht —
   Redundanz kennzeichnen + Zweck dokumentieren.

### 3.5 Reifegrad & Betriebs-CDE

- Stufe 1 = reine Dateiablage; Stufe 2 = Containerverwaltung mit Metadaten (CDE „blind“ für
  Inhalte); Stufe 3 = objektbasiert (Elemente einzeln adressierbar — BIM-Server/-Datenbank).
  Kommerziell meist Stufe 2; Stufe 3 oft proprietär. CDE-Produkte untereinander kaum
  interoperabel → CDE-zu-CDE-Austausch über IFC/CAFM-Connect/COBie/OSCRE vereinbaren. [VERIFY
  Marktstand 2026]
- **Nach der Objektübergabe** meist unadressiert: wer betreibt die Datenumgebung im Betrieb
  (Eigentümer/Betreiber/FM-Dienstleistung, wessen System)? Fortschreibungspflicht gehört in
  den FM-Vertrag. Moderne CAFM-Systeme decken Stufe 2/3 bereits ab — natürlicher Kandidat für
  die Betriebs-CDE.

### 3.6 Langzeitarchivierung

- Gebäudelebensdauer vs. Format-Halbwertszeit = „digitale Amnesie“. Gegenmittel:
  herstellerunabhängige, selbstdokumentierende Klartextformate (STEP/SPFF, XML) +
  Archivierungsplan in der AIA (Format, Turnus, Migrationsverantwortung) — für Eigentümer, die
  30–50 Jahre auf dieselben Daten zurückgreifen wollen.

---

## Abschnitt 4: Benennungskonvention & Projektkodierung

### 4.1 Stellenwert und Facetten

Der Dateiname ist in Level-2-Welt die einzige durchgängige Metadatenquelle:
CDE-Funktionen, Prüfautomatik, BCF-/Archiv-/Abrechnungslogik hängen daran; die Konvention
muss von der Autorensoftware über die CDE bis ins CAFM **übersetzungsverlustfrei**
durchhaltbar und als AIA/BAP-Bestandteil vertraglich verbindlich sein.

Bausteine (Reihenfolge + Trennzeichen je Projekt festlegen, dann nie mehr ändern):
**Projektkennung** → **Ersteller/Beteiligter** (Firmen-/Rollenkürzel) → **Struktur/Ort**
(Bauwerk/Teilprojekt, Geschoss, Zone, Achse) → **Fachrichtung/Gewerk** (z. B. ARCH, STA,
HKLS…) → **Dokument-/Modellart** (Modell, Plan, Berechnung, Protokoll) →
**Nummer/Alternative** → **Stand (Version + Revision)**.

- Musterlogik: `PROJ-ERSTELLER-BEREICH-FACH-TYP-NR_V###R##` — Feldlängen, Zeichensätze,
  Trennzeichen sind Projektentscheidung; maschinelle Prüfbarkeit (Regex auf Dateinamenebene)
  im BAP vereinbaren. [VERIFY Musterform = Üblichkeit, keine zitierte Norm.]
- Stand-Kürzel: `V11_R2_A1` = Version 11, Revision 2, Alternative 1; **Status
  (WIP/Shared/Published) nicht in den Dateinamen**, sondern in der CDE führen — sonst
  Status-Drift in jeder Kopie. **Eineindeutigkeit**: jeder Code genau einmal; keine
  „final_final2“-Kette.

### 4.2 Was zusätzlich zu fixieren ist (Kodierung allein reicht nicht)

- **Projektkoordinatensystem + Projekt-Nullpunkt** in der AIA (Einheit mm,
  Rechts-/Linkssystem, Höhenbezug; Hochbau lokal achsparallel, Infrastruktur übergeordnet —
  9.3); Einheiten und Schreibweisen (Punkt/Komma-Fallen in CSV-/Mengenexporten).
- Geschoss-/Raumnummern (Belegungs-/Raumnummern werden später Schilder, Inventar,
  CAFM-Schlüssel — früh einfrieren!); Anlagen-/Objektkennzeichnungsschlüssel **AKS/KKS**
  (14.2); Ebenen-/Darstellungslogik und Farbschema der Fachmodelle.

---

## Abschnitt 5: Ausarbeitungsgrade — LOIN, LoD/LOD, LOG/LOI/DOC

### 5.1 Begriffstrias

- **LoD (reiner Visualisierungs-Detaillierungsgrad) ≠ LOD (Level of Development)**: LOD
  umfasst Reife/Zuverlässigkeit + Umfang; Zerlegung **LOG** (Level of Geometry) + **LOI**
  (Level of Information) [+ **DOC** = Dokumentationsanteil nach EN 17412].
- **LOIN (Level of Information Need, DIN EN 17412-1)** = europäischer Rahmen: zweck-
  (Anwendungsfall-) und meilensteinbezogen je Objekttyp im Strukturplan; **keine** festen
  Stufen; Geometrie über Aspekte (Detailgrad, Dimensionalität, Ort, Aussehen, parametrisches
  Verhalten), Semantik als Required-Attributliste, dazu Dokumentvorgaben. Vorteil: präzise,
  verhindert Datenballast; Nachteil: projektspezifische Vielfalt; beschreibt anders als LOD
  keine Verlässlichkeit/Entwurfsreife. [VERIFY Normstand]
- Konsens: LOD/LOIN-Anforderungen gehören in die **AIA** und werden als Element-/Phasenmatrix
  Vertragsbestandteil.

### 5.2 BIMForum-LOD-Tabelle (Element-bezogen, De-facto-Standard)

| Stufe | Geometrie | Information | Typische Nutzung |
|---|---|---|---|
| LOD 100 | Symbol/generisch | approximativ abgeleitet (z. B. Kosten/m²) | Varianten, Flächen |
| LOD 200 | generisches Objekt, ungefähre Maße/Lage/Orientierung | generisch, approximativ | Systementscheid, TGA-Platzhalter |
| LOD 300 | spezifisch; Größe/Form/Position messbar ohne Sekundärquelle | objektscharf anhängbar | Ausschreibungsreife |
| LOD 350 | wie 300 + Schnittstellen zu anderen Systemen (Anschlüsse, Lager) | wie 300 | Koordination, Kollision |
| LOD 400 | fertigungs-/montagereif | fabricationsreif | Werkstatt-/Montageplanung |
| LOD 500 | Wie-Gebaut, verifiziert (keine Geometrie-Mehrdetaillierung ggü. 400) | As-Built | Abnahme, FM-Übergabe |

- Kernregel: **„es gibt kein LOD-###-Modell“** — ein Modell enthält Elemente auf gemischten
  Stufen; keine 1:1-Zuordnung Stufe↔Phase; Gewerke entwickeln unterschiedlich schnell.
  Übersetzungsfalle: die Stufen entstanden ohne klare Planungsphasen — **deutsches
  HOAI-Mapping ist in Breite nicht durchgesetzt** und bleibt Projektentscheidung (5.3).

### 5.3 Deutsche Modelle: MDG, Fertigstellungsgrad, getrennte Tabellen

- **VBI-Modellldetaillierungsgrad (MDG)** — an HOAI-Leistungsphasen verankert; 100er-Schritte
  = geometrische Entwicklung, 10er-Zwischenschritte = alphanumerische Anreicherung ohne neue
  Geometrie [VERIFY — vereinfachte Synthese, im Projekt gegen Originaltafel prüfen]:

| MDG | HOAI-Phase | Inhalt |
|---|---|---|
| 010 | LP1 | kein 3D-Modell |
| 100 | LP2 | LOD-100-analog, Volumen/Konzept |
| 200 | LP3 | Entwurfsmodell |
| 210 | LP4 | keine Extra-Geometrie; Infoanreicherung (Genehmigung) |
| 300 | LP5 | Ausführungsplanungsmodell, messbar |
| 310 | LP6/7 | Mengen→LV (Mengenkonsistenz) |
| 400 | LP5/7–8 | werk-/montagereif |
| 500 | LP8 | As-Built verifiziert |
| 510 | LP9 | Mängelverfolgung im Modell |
| 600 | Betrieb | schlankes Betriebsmodell (Geometrie-Defizit aktiv bereinigen!) |

- **VDI 2552** trennt: *Modelldetaillierungsgrad* (kontinuierliche Zunahme) vs.
  **Modellfertigstellungsgrad** (= LOD, an Meilensteinen zu erreichender Grad; Bezug BIMForum;
  inkl. **LOD 600 für Facility Management**); Empfehlung: Modellentwicklungsmatrix +
  Bauteiltyptabelle als AIA/BAP-Anlagen; HOAI-Mapping möglich. [VERIFY Blattnummer/-stand]
- **DB**: getrennte LoD- und LoI-Tabellen je Phase. **DEGES**: LOG + LOI + DOC je Objekttyp,
  zweck-/meilensteinbezogen. **BIM4INFRA**: LOD = LOG + LOI, HOAI-verknüpft.
  Projektspezifische LOI-Tabellen sind Normalfall: geometrische Anforderungen sind
  AG-übergreifend ähnlich, **Informationsanforderungen fast immer projektspezifisch** — nie
  kopieren ohne Zweckprüfung (2.5).

### 5.4 Die Elementmatrix (Arbeitsmittel)

Kernstück jeder AIA/BAP: **Modell-Elemente-Matrix** — Zeilen = Objekttypen (nach
Klassifikation des Strukturplans), Spalten = Meilensteine/Data Drops; Zelle = LOG + LOI (+
DOC) + Verantwortlichkeit je Rolle. Regeln: nur tatsächlich zu liefernde Objekttypen
aufnehmen; Attributbedarf über eigene Attributliste lösen — Matrix verlinkt statt
wiederholt; die Matrix **ist der Prüfmaßstab** der Data-Drop-Abnahme (10.4) — fehlt sie,
fehlt die Abnahmegrundlage.

---

## Abschnitt 6: Anwendungsfall-Katalog nach Lebenszyklus

### 6.1 Katalog

| # | Anwendungsfall | Phase | Nutzen-Empfänger | Datengrundlage |
|---|---|---|---|---|
| 1 | Technische Visualisierung / Kommunikation | alle | AG, Öffentlichkeit | LOG genügt |
| 2 | Fachkoordination / Kollisionsprüfung | LP3–8 | alle Planenden | föderierte Modelle, LOD 300+ |
| 3 | Planableitung (2D aus 3D) | LP3–6 | Planende | konsistente Modellgeometrie |
| 4 | Mengenermittlung / Kostenschätzung | LP2–6 | Kostenplanung | QTO-MVD, Mengenattribute |
| 5 | LV / Ausschreibung / Vergabe | LP6–7 | AVA | VOB-prüfbare Mengen |
| 6 | Tragwerksplanung / Nachweis | LP2–5 | TWP | Analyse-/Konstruktionsmodell |
| 7 | 4D-Bauablauf / -prüfung | LP5–8, Ausführung | Bauleitung | Modell↔Vorgangs-IDs |
| 8 | 5D (Kostenzeitverlauf) | LP6–8 | Projektsteuerung | 4D + Kostengruppen |
| 9 | Baufortschrittskontrolle / Soll-Ist | Ausführung | Bauleitung, AG | 4D-Ist-Modell |
| 10 | Abrechnung / Controlling | Ausführung | AVA, Controlling | Mengen-/Objektzuordnung |
| 11 | Mängelmanagement | LP8, Gewährleistung | Bauleitung, FM | objektscharf (BCF) |
| 12 | Betrieb/Erhaltung, CAFM-Übernahme | Betrieb | Betreiber, FM | As-Built + Anlagenliste |
| 13 | Wartungs-/Garantiedatenpflege | Betrieb | FM | Prüffristen/Dokumente am Objekt |
| 14 | Rückbau / Materialauskunft | Ende | Kreislaufwirtschaft | Materialdeklaration |
| 15 | Genehmigungs-/Regelprüfung (ACCC) | LP4 | Behörde, AG | regelkonforme Semantik |

FM-Besonderheit: Wartungsintervalle/Garantiebedingungen technischer Geräte;
kontinuierliche Pflege (real → digital nachführen); Rückbau braucht Materialauskunft für
Entsorgung/Reuse.

### 6.2 Auswahlregeln

- Anwendungsfälle **vor** Modellstart wählen; je Fall → benötigte Objekte + Attribute +
  Zeitpunkt → Elementmatrix + Data Drops. Ein Anwendungsfall ohne Datenplan ist Zusatzaufgabe
  ohne Nutzen. **Modell-Erstellung ist kein Anwendungsfall**, sondern Voraussetzung — eine
  AIA-Zeile „Modell liefern“ ohne Zweck ist Über-Spezifikation.
- Zwei Reifestufen je Fall: **modellgestützt** (Prozess bleibt, Information wird digital
  genutzt — schnelle Erfolge, wenig Standardisierung) vs. **modellbasiert** (Prozess für
  Automatisierung umgebaut — hoher Standardisierungsgrad). Neustarts: modellgestützt beginnen.
- **Anfangfehler**: „mehr Anwendungsfälle = mehr BIM“. Parallel geführte 2D-Planung
  („doppeltes Netz“) lässt modellbasiertes Arbeiten verhungern → konsequent modellbasiert
  **oder** Fall bewusst modellgestützt anbinden. Bewertungsraster: Eingangsdatenqualität?
  Partner einbindbar? Qualifikation? Aufwand vs. Mehrwert? Kundennutzen?
  Prozess-/Systemvernetzung? Normenkompatibilität?
- Reduktion ist Normalfall: DB wertete 28 Pilot-Anwendungsfälle auf 19 (Planungsphase);
  BIM4INFRA identifizierte ~20 praxisrelevante Fälle inkl. „Bestandserfassung“ als eigenem
  Fall. [VERIFY Zahlenstand]

### 6.3 Übersetzung Ziel → Fall → Daten (Arbeitsweise)

1. BIM-Ziel benennen (z. B. „Nachträge −20 %“). 2. Anwendungsfall(n) zuordnen. 3. Datenbedarf
   ableiten (welche Objekte/Attribute, welcher LOG/LOI zu welchem Termin). 4. Rollen +
   Prüfprozesse + Vertragsanlagen festschreiben. 5. Messgröße definieren (sonst kein Nachweis
   — 15.2, 17.4).

---

## Abschnitt 7: Rollen, Organisation, Qualifikation

### 7.1 Kernrollen (VDI 2552-7 ≙ ISO 19650)

| Rolle | ISO-Logik | Kern | typisch bei |
|---|---|---|---|
| **BIM-Management** | Informationsmanagement (AG-/Projektleitungsseite) | AIA erstellen + Konformität überwachen, BAP prüfen, QA-Monitoring, Freigabeprozesse, modellbasierte Meetings; **kein** klassisches PM | große AGs, Büros, ausführende Firmen |
| **BIM-Gesamtkoordination** | Koordinationsmanagement (AG- oder AN-Seite, je Vergabemodell) | Fachmodelle zusammenführen, Kollisionen/Konflikte, Konfliktauflösung inkl. moderierter Planungs-/Baubesprechung + Nachverfolgung (BCF) | führende Disziplin (Hochbau: Architektur; Infrastruktur: Verkehrsanlagen) |
| **BIM-Fachkoordination** | je Disziplin | Qualität + Frist des eigenen Fachmodells, AIA-Konformität Geometrie + Semantik, Konflikte im Fachteam; koordiniert eigene Autoren | jedes Fachplanungsbüro |
| **BIM-Modellautor** | Informationsautorenschaft | Geometrie im vorgegebenen Ausarbeitungsgrad + semantische Anreicherung | Fachplanende, Bauzeichnende |
| **BIM-Nutzende** | Informationsnutzende | lesende Nutzung, Ableitungen (Zeit/Kost/Antrag), Prüffunktion mit Rückmeldung | Ausführung, Behörden, Sachverständige |

- Gesamtkoordination **AN-seitig** bei Generalunternehmer-/Totalnutzung,
  **AG-/Projektsteuerungs-seitig** bei gewerkeweiser Einzelvergabe — vor Vergabe entscheiden
  (ändert die Vertragsarchitektur); AN-seitig i. d. R. Eignungsnachweis schon in der Vergabe.
  Deutscher Sonderweg: **Rollentrennung Koordination (Planungsebene) vs. Management
  (steuerungsnah, AG-seitig)** wegen HOAI-Grundleistungen + AHO-Leistungsbild
  Projektsteuerung; international heißt vieles „BIM-Management“ — Terminologie in Verträgen
  explizit klären.
- BIM-Management als Vertragsleistung ist in DE **Besondere Leistung** (HOAI-Logik + AHO-Heft
  9/11; 13.2). **Modellautoren/Urheber haften weiterhin für den eigenen Planungsbeitrag**; BIM
  verschiebt keine Verantwortung auf Koordination oder Modell.
- BIM in **Bauleitung/Ausführung**: modellbasierte Fortschritts-/Mengensteuerung,
  Mängel-/Abnahmeprozesse, Bautagebuch am Modell (11.2, 12, 15); AG-seitig spiegelbildlich
  **BIM-/LIA-Informationsmanager** (Betriebs-Datenbedarf im Projekt) und
  **BIM-FM-Datenmanager** (Quality Owner der Übergabedaten im Betrieb; 14.6).

### 7.2 Qualifikation & Einführung

- Rollenprofile + **Eignungskriterien in der Vergabe** (Nachweise, Referenzprojekte,
  Ausstattung) + Schulung **aller** Beteiligten vor Projektstart (Format „CDE-Führerschein“).
  Ausbildungsstufen: Basis → anwendungsspezifisch je Rolle → Experte; akkreditierte
  Zertifikate (Verbands-/Richtlinienstufen) als Wertungsmerkmal nutzbar [VERIFY
  Programmstand].
- **People = kritischster Erfolgsfaktor**; Software-Qualifikation weniger kritisch als
  Kulturwandel. Wirksam belegt: intrinsische Motivation statt Stichtags-Zwang (Pull-Prinzip:
  Führungssignal + Angebote + Freiwilligkeit), gelebte Fehlerkultur, Multiplikatoren-System.
- Büro-Einführungsreihenfolge: erst little open BIM intern mit **einem** Anwendungsfall mit
  direktem Mehrwert (kein Selbstzweck), dann Big-BIM-Projekte; eigene Prozesslandkarte real
  abbilden; Umstellung dauert — früh kommunizieren. BIM-Einführung ist
  Organisations-/Prozessneuordnung, nicht Softwarekauf.

---

## Abschnitt 8: Datenaustausch — IFC, MVD, BCF, Formatlandschaft

### 8.1 Formatrollen

- **IFC (ISO 16739)** = offenes herstellerneutrales Modell für Koordination und Übergabe.
  **Version strikt pinnen**: IFC4 ist **nicht** abwärtskompatibel zu IFC2x3; in der AIA immer
  Version + MVD + Serialisierung (SPFF/ifcXML/ZIP-Varianten) festlegen; HEADER-Deklaration mit
  MVD-Name = Prüfhilfe.
- **MVD (Model View Definition)** = maschinenlesbare Teilmenge für einen Austauschfall
  (Klassen, Attribute, Psets, Beziehungen, erlaubte Geometrietypen;
  required/optional/prohibited): **Coordination View** (Fachmodellaustausch); **Quantity
  Take-Off** (explizite Mengenattribute); **Space Boundary** (Raumgrenzen 2. Grades,
  Energiesimulation); **Structural Analysis View** (physikalisches Modell + Lasten); **Basic
  FM Handover View** (Betriebsdaten-Reduktion); **Reference View** (nur
  koordinieren/kollidieren) vs. **Design Transfer View** (Weiterbearbeitung) — die
  Refer/Design-Scheidung ist die häufigste fehlende Zeile in Formattabellen.
- **IDM-Methode (ISO 29481)** = Prozessklärung vor Format: Use Case → Process Map
  (BPMN-Swimlane: wer/wann/was) → Exchange Requirements (tabellarisches
  Informationspflichtenheft je Objekttyp) → MVD. Für die AIA: pro Data Drop ER-Tabelle + MVD —
  sonst ist „Lieferung als IFC“ nicht prüfbar.
- **Psets/Attribute**: standardisierte Pset_* nutzen, Lücken über projektdefinierte Psets;
  Merkmalsverwaltung nach ISO 23386, Datenvorlagen nach ISO 23387; Referenzierung über
  Wörterbuchdienste (bSDD, nationale Merkmalsserver) statt Freierfindung [VERIFY
  Verfügbarkeit]. **Klassifikation**: Rahmen ISO 12006; DE: DIN SPEC 91400
  (STLB-Bau-/DIN-276-Logik, IFC-verknüpft — Mengen/LV-Anschluss), für FM CAFM-Connect; ohne
  Klassifikation kein automatisierter Mengen-/CAFM-Layer.
- **Nachbarformate nur einplanen, wenn betroffen**: BCF (Issues), COBie (tabellarischer
  nicht-grafischer FM-Datensatz), CAFM-Connect (DACH-FM) mit BIM-Profilen, gbXML (Energie),
  GAEB (LV), XPlanung/OKSTRA/CityGML (GIS/Behörde).

### 8.2 Austauschqualität managen

- Parametrik (Constraints/Abhängigkeiten) geht über IFC **verloren**; gleiche Semantik darf
  unterschiedlich modelliert sein (durchlaufende vs. geschossweise Wand) →
  **Modellierungsrichtlinie** mit einfachen Regeln je Objekttyp als BAP-Anlage; Konventionen
  absprechen statt hoffen.
- bS-IFC-Zertifizierung der Werkzeuge (Test gegen MVD) nutzen — **Zertifizierung ≠
  Fehlerfreiheit**, Abdeckung nur zertifizierte Fälle; kritische Objekte (Tür, Fenster,
  Raumgrenze) über Konsensregeln (Implementers'-Agreement-Logik) absichern [VERIFY
  Zugänglichkeit der Regel-Datenbanken]. Geometrie-Zwecktrennung: Mesh/Tessellation für
  Viewer, B-rep/CSG für Weiterbearbeitung; Konsistenzerhaltung ist Herstellerverantwortung.

### 8.3 IFC-Datenanforderungen je Disziplin (Prozesssicht)

| Disziplin | Bedarf | MVD/Attribute | Typische Stolperfallen |
|---|---|---|---|
| Architektur | Koordination, Planableitung, Raumbezug | Coordination View; Raumobjekte, Raumgrenzen, Geschosshierarchie | Raumgrenzen 1. vs. 2. Grad; Wandvarianz |
| Tragwerk | Referenzgeometrie → Analysenmodell | Structural Analysis View; schalkantenbezogene Geometrie, Auflager, Lastfälle | Schalkante ≠ Systemlinie; „automatisches“ Tragwerksmodell ist ein Mythos — Checkliste vorab an Architektur |
| TGA | Durchbrüche/Aussparungen, Wartungsräume, Lichträume | Coordination View; Aussparungen als **separate referenzierte Objekte** | Leitungsbestand semantisch uneinheitlich; Platzhalter zu früh entfernt |
| Mengen/Kosten | prüfbare Mengen je Position | QTO-MVD; explizite Mengenattribute (z. B. Wandhöhe), Einheiten | Einheitenabgleich Modell↔AVA; Übermaß-Sonderregeln |
| Energie | Zonengeometrie + Hülle | Space-Boundary-MVD (2nd level), gbXML-Export | Anlagentechnik unvollständig; Zonen nicht automatisch |
| Betrieb/FM | Anlagen-/Raumdaten, Dokumente am Objekt | FM-Handover-View; projektspezifische Psets, Klassifikation | Standard-Psets reichen nicht; GUID-Verlust bei Konvertierung |
| AVA/LV | Positionsbezug, Mengenverteilung | DIN SPEC 91400, GAEB-Ausleitung | frühe Mengen ≠ Vergabereife (Warnung + Version) |

---

## Abschnitt 9: Föderierte Modelle, Koordination, Besprechungswesen

### 9.1 Modellkette

```
Fachmodelle (je Disziplin, Besitz des Urhebers)
  → Koordinationsmodell (Zusammenführung, Prüfung, „Freeze“ je Phase)
    → As-Built-Modell (verifiziert „wie gebaut“, LOD 500)
      → Betriebsmodell (reduziert auf Nutzung → AIM/CAFM)
```

- Änderung **nie** im Koordinationsmodell — zurück ins Fachmodell, dann neu zusammenführen
  (Regel Nr. 1; bricht die Kette, ist das Koordinationsmodell wertlos). Fertigstellungsgrad
  wird am Koordinationsmodell je BAP geprüft. Koordinationsmodell dauerhaft oder temporär je
  Zyklus; wird wie jedes Fachmodell in der CDE geführt (Status, Revision).
- Nach Phasenende: Stand **einfrieren**, daraus neues Referenzmodell (IFC) für die Folgephase.
  Plannableitung bleibt Pflichtprodukt (Ausführung arbeitet 2D) — 3D-Ausschnitte als Beigabe
  zu Konfliktpunkten.

### 9.2 Koordinationszyklus (iterativ, vertraglich getaktet)

1. Teilmodelle bis Stichtag in die CDE (Fachkoordination bestätigt Lieferstatus).
2. Automatische Vorprüfungen: Konvention/Attribut + Kollision — Ergebnisse **vor** der
   Besprechung, nicht live.
3. Konflikte **strukturieren**: nach Gewerken/räumlichen Clustern/Achsraster sortieren,
   Duplikate zusammenfassen (gegen Mehrfachdiskussion).
4. Besprechung: Entscheidung je Konflikt; Verantwortliche + Fristen sofort als Issue (BCF)
   hinterlegen.
5. Nachverfolgung im Aufgabenmanagement; nächster Zyklus prüft Behebung **und** neue Konflikte
   (Regression).
6. Freigabe des Koordinationsstands (Revision) → nächste Phase.

Zykluslänge Projektentscheidung [Praxis: zweiwöchig in Feinkoordination/Ausführung];
Lieferstichtage ≠ Besprechungstermin (Vorlauf im BAP-Terminplan). Setting: Großdisplay +
Online-Teilnahme, Navigation zu Konfliktpunkten, papierlos; Protokoll = Issues +
Beschlüsse.

### 9.3 Koordinationsfestlegungen (BAP-Kern) und Koordinaten

- Vor Projektstart festlegen: Teilmodellaufteilung + Zyklen; **einheitliches
  Koordinatensystem**, Modellstruktur, Detailtiefe, Farbschema; Kollisionsregeln + Ausnahmen
  vorab gemeinsam erstellen und **vertraglich festhalten**; früh Platzhalter, später real (z.
  B. Sprinklerkopf), originalgetreue Kleinteilegeometrie vermeiden (Performanz);
  Konfliktklassifikation vor dem ersten Lauf.
- Hochbau: locales, achsparalleles System (1:1), Anschluss ans Landessystem über koordinierten
  Punkt + Drehwinkel; Infrastruktur: übergeordnet (ETRS89/UTM, Höhenbezug DHHN) mit lagiger
  Verzerrung → Mittelmeridian/Projektmaßstab bewusst wählen (Modellmaß ≠ Realmaß bei
  Absteckung); BIM-Software kann geodätische Transformationen nur eingeschränkt — Vermessung +
  BIM-Management vor Modellstart einigen; Projektnullpunkt in AIA. [VERIFY je
  Bundesland/Träger]
- Bestand/Scan: Punktwolke als Modellreferenz; Registrierung ≥ ~25 % Überlappung; Befund vs.
  Interpretation trennen (Vagheits-Kennzeichnung); Modell ↔ Originalwolke verknüpfbar halten.
  Trassengebundene Modelle: „Scheingenauigkeit“ nur durch verbindliche LOG/LOI-Vorgaben
  bändigen; Kontrollpunkte zur Verifikation. Baugrund/Leitungsbestand: Unsicherheitsobjekte
  mit Hüllkörpern/Toleranzvolumen statt Scheinlage.

---

## Abschnitt 10: Modellprüfung (Model Checking) & Quality Gates

### 10.1 Prüfstufen

| Stufe | Prüfung | Mittel |
|---|---|---|
| visuell | Plausibilität, Vollständigkeit am Bildschirm | Viewer, Review |
| halbautomatisch | Attribut vorhanden/plausibel? Fehlklassifizierung? | Model Checker (Regeln) |
| automatisch formal | Schema-/MVD-Konformität, GUID-Stabilität | Validator gegen MVD |
| automatisch fachlich | Kollision, Raum-/Flächenregeln, Code-Regeln | Regel-Engine, ACCC |
| Soll-Ist | Modell ↔ Vermessung/Fortschritt | Abgleich-Werkzeuge |

### 10.2 Was vertraglich geprüft wird

- Standardprüfliste: **Projektnullpunkt, Einheiten, Dateinamenskonvention,
  Dokumentverknüpfungen (Vollständigkeit), LOG/LOI je Objekt, Objektparameter**. Prüftiefe je
  Data Drop: Phasen-Gates (nur wenn fachlich **und** modelltechnisch vollständig —
  ISO-Freigabelogik) + AIA-Konformität bei Abschlagszahlung/Phasenende.
- Regelbasis = **dieselben Regeln für alle** (AG wie AN); veröffentlichte
  Prüfregel-Bibliotheken (AG-/Behördenseite) schlagen projektindividuelle Blackbox-Regeln;
  Transparenz der Regel (White-Box vs. Parameter-Blackbox) ist Vergabe-/Prüfkriterium.
  Werkzeuge müssen die AIA-Regelsätze **ausführen** können: vorab testen, ob gelieferte
  Attribute aus dem Export auslesbar sind (Konvertierungsverluste machen jede Prüfung blind).
- Prüfergebnisse verlassen die CDE nicht als Datei-Anhang, sondern als referenzierte Issues
  (11).

### 10.3 ACCC (automatisierte Regelwerksprüfung) — Realismus

- Maschinell prüfbare Regelwerke existieren punktuell (Barrierefreiheit, Flucht-/Rettungswege,
  Brandschutzgeometrie; Vorreiter: SG e-PlanCheck; DE-Forschung BIM-Bauantrag; UK
  D-Com-Logik); der Rechtsrahmen („anerkannter Stand der Technik“) bleibt menschlich
  interpretiert. [VERIFY Verfahrensstand je Bundesland]
- Vorbedingung: Detailgrad + Korrektheit — **keine verlässlichen Ergebnisse aus fehlerhaften
  Modellen** (Garbage in, violation out). Eigene Projekte: kleine, klare Regelsets (10–30
  Prüfungen) sind mehrwertbringender als die Vollautomatik-Vision; Regeln wiederverwenden
  (Regression bei jedem Data Drop).

### 10.4 Quality Gate pro Datenübergabepunkt

1. Lieferung im vereinbarten Status (3.2). 2. CDE-Automatik:
   Benennung/Metadaten/Format/Schema. 3. Model Checker gegen MVD + Elementmatrix (fehlende
   Attribute, LOG/LOI, Klassifikation). 4. Kollisionslauf gegen Vorrevision (Delta zur
   Konfliktliste). 5. Fachkoordination gibt Fachmodell frei → Gesamtkoordination prüft
   Koordinationsmodell. 6. Protokoll + Issues + Statusübergang; Abweichungen dokumentiert und
   **zeit-/umfangsbegrenzt zugelassen** (kontrollierte Abweichung, nicht stiller
   Vertragsbruch). 7. Ergebnis = Grundlage der Leistungs-/Zahlungsfeststellung.

### 10.5 Prüfregeln als Asset

Jede durchlaufene Prüfung → Regelfall-Kandidat: wiederkehrende Fehler (falsches
Koordinatensystem, Klassenverwechslung, fehlende Mengen) als Regel + Schulungsthema.
AG-seitig ist eine unternehmensweite Regelbibliothek über Projekte hinweg der eigentliche
Lernkurven-Hebel.

---

## Abschnitt 11: BCF — Issue-Management & Mängelverwaltung

### 11.1 Was BCF ist (und nicht)

- **BCF (BIM Collaboration Format)** = offenes Format (XML/ZIP oder Webservice-API) für
  Themen/Mängel/Kommentare **herstellerübergreifend**: trägt keine Modelle, nur Referenzen
  (IFC-GUIDs betroffener Objekte) + Inhalt — Äquivalent zur Revisionswolke für 3D; der Kanal
  zwischen Model Checker, Koordination und Baustelle.
- Inhalt: Themen-Metadaten (Titel, Beschreibung, GUIDs, Geschoss, Datum, Autor, Priorität,
  Zugewiesene/r, Status, Links zu Mängelbericht/Abnahme) + Visualisierung (Kameraposition,
  Markierungsfarbe, Screenshot) + optional Modellbeigabe — einfache Tools ohne 3D können BCF
  anzeigen.

### 11.2 Issue-Workflow (Minimalzustände, an BAP anpassen)

```
neu → zugewiesen → in Bearbeitung → zur Prüfung gelöst → geschlossen
     ↖ zurückgewiesen/abgelehnt (jeweils mit Begründung)
```

- Pflichtripel je Issue: **Objekt-Referenz (GUID), Verantwortliche/r, Frist**. Ein Issue ohne
  Frist ist ein Protokollsatz, kein Arbeitspaket. Kategorien im BAP definieren (Kollision,
  fehlendes Attribut, Regelverstoß, Planungslücke, Ausführungsmangel) — Auswertung je
  Kategorie = Planungsqualitäts-Kennzahl.
- Baustellen-/Gewährleistungsmängel: gleiche Spur — Mängelprotokoll objektscharf via BCF,
  Behebungsnachweis (Foto/Dokument) am Issue; die Mängelliste wird zum Abnahmeprotokoll.
  Eskalation: überfällige Issues = erster TOP der Koordinationssitzung; bei 4D-Einsatz Issue ↔
  Vorgang koppelbar (15.1).
- BCF-Datenbestand ist Nachweisinstrument (wer wusste wann was): Issue-Historie mit dem
  Modellarchiv sichern (3.6). **Aber**: Änderungswünsche über Issues sind **keine**
  Vertragsänderung — Nachträge laufen über den vertraglichen Weg. Diese Trennung vor
  Projektstart allen klar sagen.

---

## Abschnitt 12: Clash-Detection-Workflow

### 12.1 Konfliktarten und Kollisionsmatrix

- **Hard clash**: geometrische Überschneidung (Kanal ∩ Träger). **Soft clash / clearance**:
  Abstands-/Montage-/Wartungsräume (Hängerplatz, Öffnungsradius, Dämmung, Ausschwenkbereich).
  **Duplicate clash**: identisches Objekt doppelt (Übergabefehler). **Zeitkonflikt (4D)**:
  räumlich ok, zeitlich unmöglich (Bauzustände, Kranbewegung).
- Kollisionsmatrix Gewerkepaar × Prüftiefe × Toleranz × Ausnahme — Tabelle in
  AIA/Modellierungsrichtlinie (Toleranzen je Projekt festlegen [Praxis]):

| Paar (Beispiel) | Regel | Toleranz-Logik |
|---|---|---|
| TGA ↔ Tragwerk | Leitung/Trasse ∩ Öffnung/Aussparung | 0 mm hart; Dämmung einrechnen |
| TGA ↔ Architektur | Deckenhöhe/Unterzug, Durchbrüche | Wartungsraum separat prüfen |
| Tragwerk ↔ Tragwerk | Bewehrung ∩ Vorspannung, Knoten | Montagefolge beachten |
| Brandschutz ↔ TGA | Abschottungen, Klappen-Anschluss | Funktionsraum |
| alle ↔ Platzhalter | Montage-/Wartungsräume, Lichtraumprofil, Baustelleneinrichtung | als Soft-Clash-Objekte führen |

- **Service Dummies** (Platzhalter für Arbeits-/Wartungsräume, Lichtraumprofile, temporäre
  Elemente) sind reguläre, klar benannte Modellelemente — Wartungszugänglichkeit wird sonst
  erst auf der Baustelle entdeckt. Toleranzen nie global „0“: Konfliktschwemme → Liste wird
  ignoriert; je Paar begründen (Bautoleranzen nach DIN 18202 höhenrelevant [VERIFY]).

### 12.2 Zyklus (Betriebsanleitung, 10 Schritte)

1. Modelle aktuell in CDE (Status „geteilt zur Koordination“). 2. Selektion je Gewerkepaar
   gemäß Matrix. 3. Run automatisiert, **Setup identisch jede Runde** (Vergleichbarkeit). 4.
   Bereinigen: Duplikate, Irrelevanzregeln, Gruppierung. 5. Clustern nach Lage
   (Achse/Geschoss) + Gewerk. 6. Priorisieren (Funktion/Sicherheit vor Ästhetik/Ordnung). 7.
   Zuweisen mit Frist (Issue-System). 8. Abarbeitung **im Fachmodell**, Rückmeldung per
   Status. 9. Re-Run: Behebung prüfen + neue Konflikte. 10. Bericht: Konfliktzahl/Trend je
   Gewerk (Kennzahl, 15.2).

### 12.3 Typische Fehler

Kleinteilegeometrie in Läufen (Last ohne Erkenntnis — Hüllen verwenden); Kollisionen ohne
Zuständigkeitsklärung (Ping-Pong); Korrektur im Koordinationsmodell (verboten, 9.1);
Ergebnisse als PDF-Mail statt Issue (Nachverfolgungsverlust); **Kollisionsfreiheit als
Abnahmekriterium: nie** — „null Kollisionen“ ist je Toleranzdefinition beliebig;
Abnahmekriterium = **abgearbeitete, geschlossene Konflikte je Datenübergabepunkt**.

---

## Abschnitt 13: Vergabe, Vertrag, Haftung & Datenrechte

### 13.1 BIM in der Vergabe

- AIA/EIR **als Anlage an alle Bietenden**; Leistungsbeschreibung BIM = Anwendungsfälle, Data
  Drops (Turnus/Termine), Organisationsvorgaben (Rollen, Besprechungen, CDE),
  Modellierungstiefe (LOG/LOI), Dateiformate. BIM-Leistungen sind Vertragspflichten, keine
  Kulanz.
- Eignungs-/Zuschlagskriterien: Personalqualifikation je Rolle, Referenzprojekt mit
  vergleichbarem Umfang, Ausstattung (spezifizierter HW/SW-Arbeitsplatz),
  **Angebots-BAP-Qualität als bewertetes Merkmal** (zweistufiges Verfahren); bei öffentlicher
  Vergabe Wertungskriterien transparent + nachvollziehbar.
- Vertragsarchitektur-Muster (DE): **Einzel-/Paketverträge + BIM-Vertragsanlagen** (AIA/BAP
  technisch; **BIM-BVB** = Besondere Vertragsbedingungen BIM als Muster des
  Infrastrukturprogramms) statt neuem Vertragsparadigma. Mehrparteien-/IPD-Modelle
  (Allianz-/Teamlogik, Rahmenvertrag + zweistufige Beauftragung mit Zielkostenlogik) sind
  möglich, aber verhandlungskomplex und DE nicht Regelfall; Erfahrung: Kollaboration **vor**
  Vertragsabschluss in Use-Case-Workshops statt nur über Klauseln.
- Musterverwendung = Checklistenfunktion; keine schematische Übernahme. Hinweis: eine
  vertragsrechtliche VDI-2552-Reihe (-2.x) war zum Quellenzeitraum nicht verdaut — verifiziert
  sind hier nur die Grundlagen-/Prozessblätter [VERIFY eigenständig gegen die VDI-Reihe
  prüfen].

### 13.2 Vergütung (DE, HOAI — Rechtsstandsvorbehalt)

- HOAI ist **methodenneutral** (schreibt kein Werkzeug vor); BIM-Mehraufwand ist nicht
  automatisch Mehrvergütung. BIM als **Besondere Leistung** (Vereinbarung in Textform):
  LP-Logik „3D-/4D-Gebäudemodellbearbeitung (BIM)“, frei vereinbar, auf andere
  Phasen/Leistungsbilder übertragbar. EuGH 2019 (C-377/17) → Mindest-/Höchstsätze nicht mehr
  zwingend; Tabellenwerte = Orientierung, frei vereinbar [VERIFY Wortlaut/Fassung + Rechtslage
  seit 2021]. Phasenverschiebung ohne Honorarfolge; Wegfall von Teilleistungen → anteilige
  Anpassung.
- Vorverlagerung des Aufwands in frühe Phasen bei **stufenweiser Beauftragung** abbilden,
  sonst wird die Vorleistung verweigert. „Nur die HOAI-Tiefe schulden“: nicht mehr liefern,
  nur weil die Software kann — Abgrenzung/Haftung; geforderte Mehr-Tiefe = besondere Leistung.
  Automatisierte Mengen ersetzen kein prüffähiges Aufmaß nach VOB; Rationalisierungseffekte
  preisrechtlich grds. nicht erfasst — Einsparbeteiligung ggf. vertraglich regeln.

### 13.3 Datenrechte / Urheberrecht

- **Urheberrecht**: Planunterlagen sind Schutzgegenstand („persönliche geistige Schöpfung“);
  Objektplanung regelmäßig geschützt (schlichte Zweckbauten Ausnahme), Fachplanung/Ausführung
  regelmäßig nur bei entsprechender Schöpfungshöhe; Miturheberschaft an föderierten Modellen
  möglich — praktisch ungelöst, vertraglich adressieren.
- **Nutzungsrechte ausdrücklich, zweckbezogen, lebenszyklusgerecht** einräumen: Weitergabe an
  Dritte (Beteiligte, Behörden, Betreiber), Nutzungsänderung/Umplanung am Modell, Reichweite
  zeitlich/trunkiert; Vertraulichkeit (Betriebs-/Geschäftsgeheimnis) für Bibliotheken/Details.
  Lizenzentzug bei Nichtzahlung ist formulierbar (international geübte Widerrufsklausel) —
  DE-Fassung juristisch absichern.
- **AG-Zugriff jederzeit + bei vorzeitiger Beendigung** sichern, besonders wenn Plattform/CDE
  bei einem Dritten liegt (Exit-/Datenherausgaberegel in der CDE-Beschaffung!).
  Fortschreibungs-/Änderungsrechte am Modell nach Meilenstein getrennt regeln (darf AG mit
  Dritten weiterarbeiten? Änderungsverbot vs. Weiterentwicklungs-Lizenz —
  Urheberpersönlichkeitsrecht beachten).

### 13.4 Haftung — die zu regelnden Punkte

Grundsatz unverändert: eigene Haftung je Beitrag; **Nutzung ≠ Haftung**: Verlassen nur auf
Daten im definierten Meilenstein-Detaillierungsgrad (**reliance level**, unabhängig vom
tatsächlichen Inhalt). In BIM-Vertragsanlagen zu regeln:

- Prüfung/Rüge von Mängeln aus Vorarbeiten nur im gebotenen Umfang — nicht jedes Fremdobjekt
  im Detail, aber Plausibilität.
- **Software-/Übertragungsrisiko**: wer stellt Software (AG-Vorgabe → AG-Risiko, Bedienfehler
  ausgenommen); Konvertierungs-/Übertragungsverluste; Pflicht zur unverzüglichen Fehlermeldung
  (Issue-System = Nachweis); Behinderungsansprüche bei Softwarestörungen.
- **Hersteller-/Katalogdaten** in Bauteilbibliotheken: bei verbindlicher AG-Vorgabe nicht dem
  Planer zurechenbar; ohne Vorgabe + ohne Regelung ggf. Planende für falsche Fremddaten
  verantwortlich → Datenqualität der Hersteller vertraglich adressieren; Weiterbearbeitung
  fremder Daten und Bereitstellung fremder Modelle durch Dritte separat regeln.
- Keine automatische Haftungsminderung durch BIM; Haftungsbeschränkungs-/Folgeschadensklauseln
  nur mit Rechtsprüfung [VERIFY Wirksamkeit nach deutschem Recht]. Mängelbeweisführung
  verbessert durch modelldokumentierte Historie — Verjährung + Archivierung (3.6) zusammen
  denken.

### 13.5 Vertragscheckliste

→ siehe 17.1 (EIR/AIA-Review inkl. Vertragsanlage) und 17.2 (BAP-Audit). Kernpunkte: AIA
referenziert + widerspruchsfrei; Rollen mit Nachweis; Data Drops ↔ Zahlungen;
Formate/Nullpunkt/Einheiten/Benennung fixiert; CDE inkl. Exit; Nutzungsrechte-Cluster;
Haftungsliste 13.4 abgearbeitet; Nachtrags-/Änderungsprozess; Schulungspflichten;
Archivierung.

---

## Abschnitt 14: Digitale Objektübergabe an den Betrieb (BIM → FM)

### 14.1 Warum hier der Business Case liegt

- Die Nutzungsphase dominiert den Lebenszykluswert; Wiederverwendung der
  Planungs-/Errichtungsdaten im Betrieb ist der Kernnutzen (häufigst belegte Nutzen:
  Zeitersparnis, Produktivität, Kostensenkung, Datenqualität). Häufigstes Adoption-Hindernis =
  fehlende Bauherren-/Betreibernachfrage [VERIFY 64 % nach Marktstudie, Stand der Quelle] —
  obwohl Eigentümer/Betreiber am meisten profitieren.
- Kostenbeleg: mangelhafte Übergabe erzeugt Folgekosten — dokumentierter Fall: > 400
  Personentage nur für Daten-Aufbereitung/-prüfung bei der Abnahme eines Gebäudes ohne
  strukturierte Übergabe; branchenweite Interoperabilitätskosten der Betreiber in
  Milliardenhöhe (US-Zahlen der Quelle). Zahlen sind Begründung, nicht Maßeinheit — eigenen
  Business Case rechnen (14.8).

### 14.2 Übergaberegeln (digitaler Handover)

- **As-Built-Qualität ist eine Dauerprüfung, kein Endspurt**: FM-Anforderungen via LIA→AIA in
  **jeder** Phase prüfen, sonst ist der As-Built-Stand nicht glaubwürdig. As-Planned ≠
  As-Built ist Normalfall (Bemusterungsrecht der Errichter, Lieferengpässe, Feldänderungen
  ohne Rückfluss, Herstellerdaten erst nach Bestellung) — As-Built-Führung ist eine eigene
  vereinbarte Leistung (Inbetriebnahmemanagement-Logik).
- **Mindestinhalt der Übergabe** [Praxis-Konsens]: Gebäude/Geschosse/Räume mit Nummern +
  Typen; Flächen je Nutzungskategorie (DIN-277); Grundrissableitungen; **Raumbuch** +
  **Anlagenliste** (Anlagen/Inventar/Ausstattung je mit Hersteller, Typ, Leistungswerten);
  Wartungspläne, Garantie-/Gewährleistungsfristen, Prüfpflichten, technische Dokumente **am
  Objekt referenziert**; Material-/Rückbauinfos; Import-/Fehlerprotokolle der Datenübernahme.
- **Objekt-IDs (Nadelöhr)**: durchgängiger Kennzeichnungsschlüssel (**AKS/KKS**: Liegenschaft
  → Gebäude → Geschoss → Raum → Anlage), **identisch in Modell und CAFM** — ID-Alignment ist
  Vorbedingung, nachträglich fast unrettbar; Schlüssel **vor** Modellstart festlegen.
- **Betriebsmodell-Reduktion**: FM-Relevantes behalten, Konstruktions-/Ausführungsdetails
  entfernen (reduzierter LOG, „BIM light“); große Objekte: Spezialmodelle separat mit Links;
  bemaßte Raumnummern = Betriebs-/Schilder-Raumnummern; TGA-Elemente mit Asset-IDs;
  2D-Ableitungen (Schnitte) als CAFM-Grafikbasis mitliefern.
- Data-Drop-Plan bis As-Built: wartungsrelevante Metadaten **vor** Fertigstellung;
  vollständiges As-Built-Modell + Revisionsdokumente einige Monate nach Bauende [Praxis: 3–4
  Monate — verhandeln].
- Vertragslogik: LOG-/LOI-Vorgaben spiegeln die CAFM-Schnittstellenbedarfe (inkl.
  2D-Ableitungen); LOI-Best-Practice = (1) fortgeführte standardisierte Objektklassifikation
  (CAFM-Connect o. ä.), (2) Required-Content je Prozess/Objekt als Pset-Spezifikation
  („welcher Anwendungsfall, welches Objekt, welche Eigenschaft, welches Format, wann, durch
  wen“).

### 14.3 CAFM-Integrationsszenarien (vor dem Datenfluss wählen)

| Szenario | Mechanik | Folge |
|---|---|---|
| **1 — Handover by Extraction** | alphanumerische PIM-Daten werden Bau-Ende extrahiert + importiert (COBie/COBie-Lite, CAFM-Connect); AIM im CAFM; natives As-Built friert als Referenz ein | billigste Lösung; Modell lebt im Betrieb nicht |
| **2 — bidirektionale Synchronisation** | CAFM führt alphanumerisch, Sync zurück ins Quellmodell (nativ oder IFC als Integrationsobjekt) | Autorkompetenz im Betrieb nötig; Modell-Migration je Softwareversion; **GUID-Stabilität bei Re-Konvertierung** ist das Risiko (Bruch von CAFM-Links) |
| **3 — Kollaborationsplattform im Betrieb** | Modellserver + Middleware; DB-Objektverknüpfung Modell↔CAFM/ERP; einheitliche Abfrage; IoT-Anbindung | teuer; Basis Digital Twin; CDE-Interoperabilität ungelöst |

- Entscheidungshilfe: Zielbild „digitale Akte + Anlagenstamm“ → Szenario 1 reicht häufig;
  „Digital Twin / Predictive Maintenance“ → 2/3 mit kalkulierten Pflegekosten. IoT-Bindung
  (nur bei 2/3): jeder Messpunkt einem BIM-/CAFM-Objekt zuordenbar machen; Event →
  automatische Instandhaltungsaktion nur mit stabilen IDs.
- Import-Disziplin: **Filter beim Import** vereinbaren (Datenflut macht das CAFM unbenutzbar);
  Worst-Cases: identische Objekte pro Raum ohne unterscheidende ID; manuelle
  Mismatch-Auflösung einkalkulieren (Beispiel: ~59 % Elemente automatisch positionierbar —
  Rest per Koordination) [VERIFY Fallzahl].

### 14.4 Übergabeformate

- **COBie**: 16 verknüpfte Tabellenblätter (Räume, Anlagen, Teile, Ersatzteile, Garantien,
  Wartung, Dokumente…); nicht-grafisch, Excel-offen; exportiert **nur, was das Modell
  enthält** → FM-Attribute gezielt pflegen, bewusstes Weglassen steuert Kosten; definiert
  **keine** Kennzeichnungssystematik (AKS/KKS) und keine Leistungskennwerte — vorher
  definieren.
- **CAFM-Connect**: DACH-Schnittstelle alphanumerischer FM-Daten (Räume → Anlagen/Ausstattung
  → Dokumente/Dateien, ifcZIP-konform); **BIM-Profile** je Anwendungsfall = maschinenlesbare
  Daten-Vorlagen (z. B. Glasreinigung, Türwartung) — zugleich EIR-Abbildung, Prüfregel und
  Importvorlage. **IFC-FM-Sicht**: Standard-Psets + Common-FM-View reichen selten —
  projektspezifische Psets **bindend über LIA/AIA** definieren; keine harmonisierte
  FM-Parameterwelt über Initiativen hinweg (Reinigungsparameter, Prüfpflichten fehlen
  regelmäßig) → Lücken mit UDA-Logik schließen.
- **Schlüsselregel**: FM-relevante Attribute **aus dem Zielsystem (CAFM) heraus** definieren,
  mit IFC-basiertem Standard abgleichen, Restlücken projektseitig schließen; das
  Ergebnis-Schema (inkl. eindeutiger Referenz-/Hierarchie-IDs) wird **Anlage der AIA** und
  Vertragsgrundlage.

### 14.5 Betreiberdatenbedarf je Prozess

| Prozess | Bedarf | Merkposten |
|---|---|---|
| Flächenmanagement | Räume, Flächen je Kategorie, Nutzung, Belegung | Raumstempel → ERP-Kopie erlaubt |
| Instandhaltung | Fabrikat/Typ/Leistung, Versorgungsbereich, Wartungsplan | Wartungszugänglichkeit = Planungskriterium |
| Störung/Service | Objektlokalisierung, Dokumente am Objekt | mobile Erfassung offlinefähig |
| Reinigung | Beläge, Glasflächen, Höhen | Profil-Import möglich |
| Betreiberverantwortung | Prüfpflichten, Nachweise, Fristen | Compliance-Nachweis = Datenqualität |
| Gewährleistung | Herstellerdaten, Fristen am Objekt | Errichter hinterlegen bei Abnahme |
| Umbau/Sanierung | aktuelles Bestandsmodell für Ausschreibung | Rückspielung Betrieb → Planung |

### 14.6 Fortschreibungs-Loop & Zuständigkeit

- Ohne Change-Prozess verfällt As-Built-Korrektheit. **Regel von Anfang an**:
  Abweichungserkennung (Servicearbeit, Begehung, Rückmeldung) → Meldung im Workflow → zentrale
  Fortschreibung (CDE/DMS/CAFM nach Szenario) → QA nach Dokumentationsrichtlinie →
  Verknüpfungen aktualisieren. Ohne Regel: Modell-Drift → Misstrauen → parallele Datenwelten →
  Rückfall in Papier.
- **BIM-FM-Datenmanager** = verantwortliche Person für zentrale, aktuelle, vollständige
  Bestandsdaten (intern/extern; Aufgaben: Datenpflichtenhefte in Bauprojekte einbringen,
  Übergabedaten übernehmen + prüfen, Defizite reklamieren, Import/Verknüpfung ins CAFM,
  Änderungsprozess etablieren, Modelle für Sanierung an Planung zurückgeben). Kapazität
  skaliert mit Projekt-/Änderungszahl [Praxis: in mittleren Organisationen Kombination mit
  Flächenmanagement].
- Daten-Governance-Trias (unternehmensseitig): (1) strukturierte interne Regeln (ID-Systeme,
  Pflichtdaten), (2) Verankerung in Beschaffungs-/Vertragswerken, (3) kontinuierliche
  Konformitätsprüfung bis zur Betriebsübernahme; unternehmensweite Dokumentationsrichtlinie in
  die AIA integrieren (GEFMA-artige Leitlinien als Hilfsmittel [VERIFY Ausgaben]).

### 14.7 Bestandserfassung ohne BIM-Vorlage (Scan-to-X)

- Bestandsdominanz: > 90 % verwalteter Bestandsbauten ohne verlässliches digitales Modell
  [VERIFY Studie]; Strategie: einheitliche Portfolio-BIM-Strategie + Template-Modelle je
  Bautyp; Erfassung **nur wo Nutzen besteht** — wirtschaftlichster Pfad oft „360°-Fotos auf
  bestehende Pläne“.
- Methoden: Altplan-Digitalisierung (nur bei Aktualität), Handaufmaß/Tachymetrie (global nur
  dezimetergenau → Ergänzung), TLS (mm–cm, Sichtlinienproblem hinter Verkleidungen),
  Drohnen-Photogrammetrie (Genauigkeitsabfall am Gebäudefuß), mobile SLAM-Systeme (relativ
  cm), Scan2BIM (teuer, Fachdaten immer manuell), **Scan2CAFM** (Maße direkt, Typenschilder zu
  fein — mit Fotos kombinieren), **Scan2Dataset** (segmentierte Wolken DB-fähig machen →
  Hybridmodell, Modellierung on-demand). LOG/LOI auf Betriebsbedarf reduzieren =
  Hauptkostenhebel.

### 14.8 Wirtschaftlichkeit der Objektübergabe

- Business Case in 3 Schritten: Kosten schätzen → Nutzen je Anwendungsfall ableiten →
  Wirtschaftlichkeit rechnen (statische ROI-Betrachtung; Amortisation 2–3 Jahre gilt in der
  Fachsoftware-Branche als Spitzenwert [Praxis]). Drei Nutzen-Kanäle: Prozesslaufzeit ↓;
  externe Kosten ↓ (Fehlerkosten, Nachträge, bedarfsgerechte Dimensionierung);
  Ertrag/Vermögenswert ↑ (vollständige Dokumentation, kein Nutzungs-/Mietverlust,
  Transaktionswert).
- Bewertungslogik (Balanced-Scorecard-Muster): Finanz / Kunde / Prozess / Lernen+Innovation;
  Schritte: Nutzen-Treiber sammeln → je Fall operationalisieren (Ziel, Rollen,
  Informationsobjekte, Risiken) → Perspektive zuordnen → KPI je Nutzen (überwiegend qualitativ
  außer Finanz) → Maßnahmen in AIA + Data Drops übersetzen. Skepsis am Lebenszyklus-ROI ist
  Hauptblocker; belastbare Betriebs-BIM-ROI-Zahlen fehlen überwiegend — konservativ rechnen,
  Messgrößen **vorher** definieren.

---

## Abschnitt 15: 4D/5D — Datenvoraussetzungen (Querreferenzen)

Terminlogik gehört zu `construction-scheduling-site`, Kosten-/LV-/Aufmaßlogik zu
`cost-management-din276`. Hier nur die **Prozess-/Datenpflichten**, die BIM-Management
stellen muss:

### 15.1 4D braucht aus dem Modell

- **Stabile Objekt-IDs** über Bauteile + Gruppen (Element-IDs brechen gern bei
  Phasen-/Softwarewechsel; Persistent-ID-Konvention + Strukturattribute Geschoss/Bauabschnitt
  als Fallback).
- Granularitäts-Kompatibilität 3D ↔ Vorgang (Deckenplatte ≠ Betonierabschnitt →
  Nachunterteilung oder geteilte Mengenverknüpfung); **regelbasierte Verknüpfung** über
  Attribute (Attribut als Filterregel → automatische Re-Zuordnung bei Updates).
- Terminplan-Updates enthalten unmarkierte Strukturänderungen
  (neu/gelöscht/umbenannt/hierarchieverschoben) → Änderungsprozess im BAP definieren. Lineare
  Strukturen: Weg-Zeit-/Line-of-Balance-Logik erlaubt automatisch erzeugbare Verknüpfung. Kein
  etabliertes 4D-Austauschformat (IFC-4D technisch möglich, praktisch Support-Lücke) →
  proprietäre Kopplung akzeptieren, Verknüpfungshistorie in der CDE sichern.

### 15.2 5D/Mengen braucht aus dem Modell

- Mengen brauchen **Sonderregeln** (Übermaß-/Abzugskörper, Schichtungen, Kontaktflächen,
  Einbauteilanzahl) — Modellgeometrie allein ist nicht VOB-prüfbar; QTO-MVD + explizite
  Mengenattribute. Kosten-/Positionsbezug über Klassifikation (DIN 276 / DIN SPEC 91400 /
  STLB-Bau); **Einheitenabgleich Modell ↔ AVA** als eigene Fehlerquelle.
- Mengen nie vor Reifegrad freigeben (Erwartungsschaden bei Dritten); Versionshinweis an jede
  exportierte Liste. Abrechnungslogik: modellbasiert „so einfach wie nötig (Abschlag), so
  genau wie möglich (Schluss)“ — Regel ins Vertragswerk.
- Steuerungskennzahlen (Fortschrittsgrad je Gewerk, Closed-Issue-Quote, Konflikttrend,
  Attribut-Vollständigkeit je Data Drop, Earned-Value-Abgleich) leben von derselben
  Objekt-ID-Hierarchie wie Mängel: **einmalige ID-Hierarchie, überall verknüpfbar**.

---

## Abschnitt 16: Übertragbare Regeln aus Pilotprojekten

Verdichtung aus DACH-/europäischen BIM-Piloten (Hochbau, Infrastruktur, Betreiber) —
Lernkurven, keine Naturgesetze:

1. **Anwendungsfälle + Erwartungen vor Vertragsabschluss klären**; nachträglich über Nutzen
   reden heißt Nachträge verhandeln.
2. **Kein doppeltes Netz**: Parallel-2D tötet modellbasiertes Arbeiten.
3. **AIA-Konformität ist Daueraufgabe**: Angebots-BAP prüfen, Projekt-BAP fortschreiben,
   kontrollierte Abweichung dokumentieren.
4. **CDE-Disziplin schlägt Tool-Vielfalt**: Externe mit Element-/Modellrechten einbinden statt
   Dateien tauschen (Rücklauf zerstört Konformität).
5. **ID-Konsistenz vor Inhalt**: GUID-Erhalt + Modell↔CAFM-Alignment sind die häufigsten
   eingebrochenen Integrationen — nachträglich fast unheilbar.
6. **Frühe Betreiber-Einbindung ist Datenplan, nicht Wunsch**: LIA→AIA von Anfang — sonst
   Hunderte Personentage bei der Abnahme.
7. **Schulung vor Leistungsabruf**: fehlende Qualifikation trifft Termin, Qualität und Budget
   gleichzeitig.
8. **Modellhygiene ist Führungsaufgabe**: nur so viel modellieren wie der Fall braucht;
   Datenmüll-Vermeidung ist die beste Pflegeversicherung.
9. **Review-Rhythmus**: kurze Zyklen + Bauwerks-Reviews mit stichtagsgenauen Ist-Terminen im
   4D-Modell — Steuerungsqualität ist nachträglich nicht kaufbar.
10. **Import filtern**: Zielsysteme mit Selektionsregeln versorgen; unfilterte Modellmassen
    machen Betriebsdatenbanken unbenutzbar.
11. **Performance im Betrieb ernst nehmen**: Detailgeometrie vereinfachen, 2D-/Foto-Fallbacks,
    Visualisierungsgeschwindigkeit als AIA-Anforderung.
12. **Hybride Modelle sind erwachsen**: Punktwolke + wenige parametrische Objekte („BIM
    light“, Scan2Dataset) schlagen oft das Vollmodell im Bestand.
13. **Kennzahlen führen** (Konflikt-/Issue-Trend, Attribut-Vollständigkeit, Closed-Quote):
    ohne Messung keine Steuerung und kein Business Case.
14. **AG-seitige Harmonisierung wirkt**: unternehmensweite Standards mit gleichen
    Auswerteroutinen für AG + AN skalieren; projektindividuelle AIA ohne Referenz nicht.
15. **Rechtliches früh regeln** (Nutzungsrechte, Haftung, Fortschreibung, Exit) — nach dem
    Schaden ist jede Klausel teurer.

---

## Abschnitt 17: Checklisten

### 17.1 EIR-/AIA-Review (vor Versand/Vergabe)

- [ ] OIR/PIR/AIR-Linien dokumentiert; jede Anforderung mit Ziel + Empfänger
- [ ] Anwendungsfälle ausgewählt (Ziel↔Fall↔Daten-Matrix), keiner ohne Nutzer
- [ ] Über-Spezifikation geprüft (Mindestinformation; Detail- vs. Funktionsbeschreibung
      bewusst gewählt)
- [ ] LOG/LOI(/DOC) als Elementmatrix je Datenübergabepunkt vorhanden
- [ ] Data Drops = echte Termin-/Entscheidungs-/Zahlungspunkte
- [ ] Rollen + Eignungskriterien + Schulungspflichten
- [ ] Formate fixiert: IFC-Version + MVD + Serialisierung, BCF, PDF/A, Einheiten, Nullpunkt,
      Benennung, Klassifikation
- [ ] CDE: Statusmodell, Freigaben, Rechte, Archivierung, Langzeitformat,
      **Exit/Datenherausgabe**
- [ ] QA: Prüfprozesse, Quality Gates, Kollisions-/Regelbasis, Ausnahmen
- [ ] Leistungsfeststellung: Konformität ↔ Abschlagszahlung/Phasenende
- [ ] Vertragsanlagen: Nutzungsrechte, Haftungspunkte 13.4, Besondere-Leistung-Einordnung,
      Nachtragsprozess für Modellstände
- [ ] FM-Anforderungen (LIA) eingearbeitet; Zielsystem + Schema bekannt
- [ ] Widersprüche zu übrigen Vertragsbestandteilen (BAP-Vorbehalt)

### 17.2 BAP-Audit (laufend)

- [ ] Rollen besetzt + nachgewiesen (inkl. Vertretung); Organigramm aktuell
- [ ] Föderationsstrategie = real gelieferte Modelle (Grenzen, Zonen)
- [ ] MIDP/TIDP vollständig je Data Drop; Lieferstichtage eingehalten
- [ ] keine bilateralen Datentransfers außerhalb der CDE (Stichprobe)
- [ ] Benennung + Metadaten + Status konsistent (Stichprobe + Regex)
- [ ] Koordinationszyklus läuft (Termine, Protokolle, Issue-Konsequenz)
- [ ] Elementmatrix-Abweichungen dokumentiert + freigegeben
- [ ] Modellierungsrichtlinie gelebt; Versionspinung gehalten; Konvertierungsverluste erfasst
- [ ] BAP selbst in aktueller, versionierter Fassung

### 17.3 CDE-Setup-Review

- [ ] Struktur (Bereiche/Phasen/Zonen/Systeme) aus Anwendungsfällen
- [ ] Statusmodell + Übergangsregeln + Rechte hierarchisch/granular
- [ ] UID/GUID-Regime (unveränderlich; GUID-Erhalt im Roundtrip getestet)
- [ ] Freigabe-/Signaturlauf digital; Versions-/Revisionslogik + Archiv + Export für Dritte
- [ ] Anbindung Prüfsystem (Model Checker) + Issue-Server (BCF)
- [ ] Benennungskonvention + automatisierte Prüfung verknüpft
- [ ] Backup/Verfügbarkeit/Datenschutz/Betreiber/Kosten + **Exit-Szenario**
- [ ] Schulung („Führerschein“) vor Freischaltung absolviert

### 17.4 Data-Drop-Abnahme

- [ ] fristgerechte Lieferung, Status korrekt
- [ ] Format/Schema/MVD-Konformität (automatisiert)
- [ ] Benennung/Metadaten/Koordinaten/Einheiten
- [ ] Elementmatrix erfüllt (LOG/LOI je Objekttyp)
- [ ] Kollisionslauf; Konflikte gemäß Matrix zugewiesen/geschlossen
- [ ] Issue-Historie vollständig; Zuständigkeiten/Fristen sichtbar
- [ ] Abweichungen dokumentiert + genehmigt + nachverfolgt
- [ ] Freigabeprotokoll + Statusübergang + Zahlungsfeststellung

### 17.5 Handover-Abnahme an den Betrieb

- [ ] LIA-/AIA-Pfandliste abgearbeitet: Raumbuch, Anlagenliste, Hersteller/Typ/Leistung,
      Dokumente am Objekt, Wartungs-/Prüfpläne, Gewährleistungsfristen, Rückbau-/Materialinfo
- [ ] As-Built-Kennzeichnung (LOD 500 bzw. MDG 500/600) + Import-Logs
- [ ] AKS/KKS durchgängig; Modell↔CAFM-Abgleich mit Mismatch-Report
- [ ] Betriebsmodell reduziert; Raumnummern übernommen; 2D-Ableitungen für CAFM vorhanden
- [ ] Formatpaket: IFC (FM-Sicht) + CAFM-Connect/COBie + Dokumente; Schema-Anlage dokumentiert
- [ ] Fortschreibungsprozess übergeben: Change-Loop + Zuständigkeit (Datenmanager) +
      Richtlinie + Werkzeuge
- [ ] Betriebs-CDE/-Plattform + Rechte/Exit; Archiv + Langzeitformat
- [ ] Restabweichungen: Mängelliste mit Fristen (keine „Hinweise“)

---

## Abschnitt 18: Glossar (DE ↔ EN, unterscheidungsrelevant)

| DE | EN | Merkposten |
|---|---|---|
| AIA / BAP / LIA | EIR / BEP / (Betreiber-AIR) | Lastenheft / Pflichtenheft / FM-Blöcke |
| OIR / PIR / AIR | OIR / PIR / AIR | Organisation / Projekt / Asset |
| CDE / Datenumgebung | Common Data Environment | Container-Stufe, SSOT |
| Datenübergabepunkt | Data Drop | vertragsrelevanter Liefertermin |
| Koordinations-/föderiertes Modell | coordination / federated model | Revision des Gesamtmodells; lose Kopplung, klare Autorenschaft |
| PIM / AIM | PIM / AIM | Projekt- vs. Asset-Informationsmodell |
| Ausarbeitungsgrad / Detaillierungsgrad | LOD / LoD | LOG + LOI (+ DOC); LoD ≠ LOD |
| LOIN / Grad des Informationsbedarfs | Level of Information Need | EN 17412, zweck-/meilensteinbezogen |
| Modellfertigstellungsgrad | milestone maturity | VDI 2552, ≠ Dauerzunahme |
| IDM / MVD / Pset | Information Delivery Manual / Model View Definition / property set | Use Case → Process → ER → MVD; IFC-Teilmenge + Regeln |
| BCF | BIM Collaboration Format | Issue-Referenz ohne Modellkopie |
| COBie | COBie | 16 Tabellen, nicht-grafisch |
| KKS / AKS | tag scheme | Anlagen-/allg. Kennzeichnung |
| Mengenermittlung / LV | QTO / BoQ | VOB-prüfbare Mengen |
| Modellprüfung / Kollisionsprüfung | model checking (ACCC) / clash detection | hard / soft / duplicate / 4D |
| Verlassensgrad | reliance level | Haftung, Meilenstein-Tiefe |
| Revisionswolke | revision cloud | Papier-Äquivalent zu BCF |
| Wie-Gebaut / Bestandsmodell | as-built | ≠ as-planned; verifiziert |
| Föderationsstrategie | federation strategy | BAP-Kernblock |
| Raumbuch / Anlagenliste | room book / asset register | Übergabe-Mindestinhalt |
| Arbeitsraum-Platzhalter | service space dummy | Soft-Clash-Objekt |
| Informationscontainer | information container | kleinste CDE-Einheit (ISO) |
| Elementmatrix | element/LOD matrix | Prüfmaßstab der Abnahme |

---

## Abschnitt 19: Zusammenspiel & Verhaltensregeln

| Situation | Zuständiges Skill |
|---|---|
| Modell/Geometrie in FreeCAD erzeugen, IFC exportieren | `construction-freecad-bim` |
| TGA-Inhaltskoordination (Leitungen, Schächte, Wartungsräume) | `building-services-tga`, `building-services-tga` |
| Kostengruppen, LV, Aufmaß/Abrechnung | `cost-management-din276` |
| Bauablauf, Takt, CPM, Baustelleneinrichtung, Fortschritt | `construction-scheduling-site` |
| Regelwerksinhalte Genehmigung | `building-regulations-permits`, `building-regulations-permits` |
| Brandschutz-Inhalte | `fire-protection-building` |

**Verhaltensregeln:** (1) Erst Anwendungsfall/Nutzerfrage klären, dann
Format-/LOD-/Rollenfragen — nie mit Namenskonventions-Debatten starten. (2) Abgeleitete
Vorgaben (LOD, Zyklus, Konvention) als **Projektentscheidung** kennzeichnen, nie als „Norm
so“, wenn die Quelle nur Üblichkeit zeigt ([Praxis]/[VERIFY] respektieren). (3)
Vertrags-/Haftungs-/Urheberrechtsthemen: Musterbausteine + ausdrücklicher Hinweis auf
juristische Prüfung. (4) Handover-/FM-Empfehlungen erst nach Zielbild-Abfrage (Szenario
1/2/3, Zielsystem) — „einfach COBie liefern“ ohne Zielsystem ist keine Antwort. (5) Wird
eine Prüfung verlangt (Kollision, Konformität, Modell-Check) ohne Regelbasis: zuerst
Regelbasis liefern (Elementmatrix + Kollisionsmatrix + Benennungsregeln) — ohne Messlatte
ist jede Prüfaussage Schein.

---

## Anhang: Normen-/Regelwerk-Index

Rahmen: DIN EN ISO 19650-1/-2 (Informationsmanagement, CDE, Rollen, Statusmodell) + -3
Betriebsphase [VERIFY -3-Stand]; DIN EN ISO 16739 (IFC); DIN EN ISO 29481 (IDM); DIN EN
17412 (LOIN); DIN EN ISO 23386/23387 (Merkmale/Datenvorlagen); ISO 12006 (Klassifikation);
ISO 21597 (ICDD); DIN SPEC 91391 (CDE-Funktionen/-austausch); DIN SPEC 91400
(STLB-Klassifikation); VDI 2552 Blätter 1/3/4/5/7/8/10/11 (Grundlagen, Mengenermittlung,
Fertigstellungsgrad inkl. LOD 600, Datenmanagement, Prozesse/Rollen, Qualifikation,
AIA/BAP, IDM-Anwendungsblätter wie Schlitz-/Durchbruchs- und Schalungs-/Gerüsttechnik)
[VERIFY Nummerierung + neue Blätter]; BSI PAS 1192 (Historie); BCF; COBie; CAFM-Connect
(BIM-Profile); GEFMA 400/410/430/444 (Zertifizierung inkl. BIM-Katalog A15)/460/198/926
[VERIFY Ausgaben]; DIN 276/277 (Kosten-/Flächenanker für IDs und Übergabelisten); HOAI +
AHO-Heft 9/11; VOB/C-GAEB; UrhG § 2; EU 2014/24/EU Art. 22; DIN 18202 (Toleranzen,
Soft-Clash-Bezug); EN 15221 (FM-Prozesskategorien); ÖNORM A 7010-6 (AT);
XPlanung/OKSTRA/CityGML/gbXML (Nachbarformate).

*Ende — dieses Skill regelt Prozess und Daten; Geometrie-Erzeugung siehe Autors-Skill
`construction-freecad-bim`. Bei Norm-/Rechtsfragen immer gegen die aktuelle Fassung
prüfen.*
