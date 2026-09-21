---
name: ifc-model-validation
description: >
  Maschinelle Prüfung und Absicherung von IFC-Modellen (DACH-Hochbau) — die
  Verifikationsschleife für automatisiert bzw. skriptgesteuert erzeugte
  Gebäudemodelle: vierstufige Prüfkette (STEP-Syntax → EXPRESS-Schema →
  normative buildingSMART-Regeln → IDS-Informationsanforderungen) mit der
  Angabe, was jede Stufe fängt und was sie nicht fängt; vollständige
  IDS-1.0-Referenz (ids.xsd-Struktur, Metadaten, die sechs Facets Entity /
  Attribute / Classification / Property / Material / PartOf mit ihren
  Parametern, Kardinalität in Applicability und Requirements, Complex
  Restrictions, dataType-Liste, SI-Einheitenzwang, Gleichheitstoleranz
  1.0e-6) samt fertigem DACH-Startsatz an Spezifikationen; Regelfamilien der
  buildingSMART-Gherkin-Regeln (ALB/ALS/SPS/GEM/BLT/PSE/QTY/PJS/OJT/GRF …)
  mit Hochbau-Filter und den Regeln, an denen generierte Modelle typisch
  scheitern; Werkzeugkette und Aufrufe (ifcopenshell.validate, ifctester mit
  Console-/Json-/Html-/Ods-/Bcf-Reporter, IDS-Audit-Tool, ifcpatch-Rezepte,
  bS Validation Service); Befund→Reparatur-Zuordnung; Abbruch- und
  Freigabekriterien (Quality Gates) für den Autorenzyklus Modellieren →
  Exportieren → Prüfen → Reparieren. Use when an IFC export must be proven
  correct rather than assumed correct, when writing or reading an .ids file,
  when a model checker reports failures, or when building an automated
  author-check-repair loop around FreeCAD/IFC model generation.
---

# IFC-Modellprüfung und Prüfwerkzeuge

## Reality Check — was dieses Skill leistet und was nicht

Dieses Skill macht Aussagen über ein IFC-Modell **messbar**. Es ersetzt keine
fachliche Prüfung.

- **Eine bestandene Prüfkette heißt: das Modell ist schemakonform und enthält die
  vereinbarten Informationen.** Sie heißt **nicht**, dass das Bauwerk tragfähig,
  genehmigungsfähig, brandschutzkonform oder wirtschaftlich ist. Ein Modell, in dem
  jede Wand ein `FireRating` trägt, kann trotzdem das falsche `FireRating` tragen.
  IDS prüft Vorhandensein, Datentyp und Wertebereich — nicht die Richtigkeit der
  Bemessung.
- **Grün heißt nicht freigegeben.** Die Freigabe ist ein Vorgang nach ISO 19650
  (Statusmodell, Verlassensgrad) und liegt bei `bim-management`; dieses Skill
  liefert die technische Evidenz, auf die sich eine Freigabe stützen kann.
- **Die Prüfkette prüft das exportierte Modell, nicht das Autorenmodell.** Was im
  Autorenwerkzeug richtig aussieht und beim Export verloren geht, findet nur die
  Prüfung des Exportergebnisses. Das ist der Zweck der Schleife.
- **Geometrische Richtigkeit wird nur formal geprüft.** Die normativen Regeln
  fangen Selbstdurchdringungen, nicht-ebene Flächen und fehlerhafte Schalen; sie
  fangen nicht, dass eine Wand an der falschen Stelle steht.
- Lastannahmen, Bemessung und Nachweise bleiben bei `structural-analysis` und den
  Fachskills; ein Prüfbericht ersetzt keinen Prüfingenieur.

## Warum dieses Skill existiert

Die Skill-Bibliothek dient der **rechnergestützten Erzeugung von Gebäudemodellen**
(CAD-Geometrie, BIM-Semantik, IFC-Austausch, FEM-Nachweis). Erzeugung ohne
Verifikation ist das Kernproblem dieses Vorgehens: Ein generiertes Modell sieht im
Viewer plausibel aus und ist trotzdem unbrauchbar, weil die Geschosshierarchie fehlt,
Bauteile als Proxy exportiert wurden, GUIDs ungültig sind, Mengen null sind oder die
Psets leer bleiben. Diese Fehler sind **stumm**: kein Werkzeug meldet sie von selbst,
und sie fallen erst beim Empfänger auf.

Dieses Skill schließt die Schleife: **Modellieren → Exportieren → Maschinell prüfen →
Gezielt reparieren → Erneut exportieren**, mit expliziten Abbruch- und
Freigabekriterien. Die Erzeugungsmechanik liegt bei `construction-freecad-bim`
(§ 4.3 BIM Preflight, § 4.4 Export-und-Grep), die Prozess- und Vertragsseite bei
`bim-management` (§ 8 Schema/Psets, § 10 Modellprüfung, § 11 BCF); dieses Skill
liefert das Stück dazwischen, das beide benennen und keines ausführt: die
maschinelle, wiederholbare, versionierbare Prüfung.

## Evidenzstufen in diesem Skill

| Stufe | Bedeutung | Beispiel |
|---|---|---|
| **Norm/Standard** | ISO 16739 (IFC), IDS 1.0 als offizieller buildingSMART-Standard (Release `v1.0.0`, 3. Juni 2024) | `ids.xsd`-Struktur, Facet-Parameter, Kardinalitätsregeln |
| **Implementer Agreement** | von buildingSMART maschinell geprüfte Vereinbarung; verbindlich für Zertifizierung | `SPS001`, `PJS003`, `IFC102`, `PSE001` |
| **Industry Practice** | breit akzeptierte Praxis, nicht normativ; Verstoß ist Warnung, kein Fehler | `GEM051`, `BLT003` |
| **Projektvereinbarung** | was AIA/BAP festlegen; hier als IDS formuliert | der Startsatz in § 5 |
| `VERIFY` | gegen die aktuelle Fassung prüfen, ändert sich ohne Ankündigung | Versions-, Verfügbarkeits- und Sperrverhaltensangaben |

---

## Abschnitt 1: Die vierstufige Prüfkette

Vier Stufen, aufsteigend. **Eine Stufe kann erst sinnvoll laufen, wenn die
vorhergehende sauber ist** — IDS setzt ausdrücklich voraus, dass das Modell syntaktisch
und schematisch gültig ist, sonst ist das Ergebnis nicht aussagekräftig.

| Stufe | Prüft | Fängt | Fängt **nicht** | Werkzeug |
|---|---|---|---|---|
| **1 — STEP-Syntax** | ISO 10303-21-Physical-File | abgeschnittene Datei, kaputte Referenzen, Kodierungsfehler | alles Inhaltliche | `ifcopenshell.validate`, bS Validation Service |
| **2 — EXPRESS-Schema** | Entitäten, Attributtypen, `WHERE`-Regeln, Kardinalitäten des Schemas | falscher Attributtyp, fehlendes Pflichtattribut, Schemaverletzung, ungültige Enumeration | fehlende Psets, fehlende Hierarchie, fachliche Lücken | `ifcopenshell.validate --rules` |
| **3 — Normative Regeln** | Implementer Agreements + Industry Practices (Gherkin-Regelsatz) | fehlende Geschosshierarchie, ungültige GUIDs, veraltete Entitäten, `Pset_`-Missbrauch, kaputte Repräsentationen, Selbstdurchdringungen | projektspezifische Informationsanforderungen | bS Validation Service; Regelsatz lokal per `pytest` |
| **4 — IDS** | die **projekt**spezifischen Informationsanforderungen aus AIA/BAP | fehlende/leere/falsch typisierte Merkmale, falsche Klasse, fehlende Klassifikation, fehlende Beziehung | Geometrie, berechnete Werte, Modellübergreifendes, Eindeutigkeit | `ifctester`, IDS-fähige Modellprüfer |

**Merksatz:** Stufe 1–3 prüfen, ob es ein gültiges IFC ist. Stufe 4 prüft, ob es
**dieses Projekts** IFC ist. Wer nur Stufe 4 fährt, prüft Inhalte in einer Datei, deren
Grundlage er nicht geprüft hat; wer nur Stufe 1–3 fährt, hat ein formal einwandfreies
Modell ohne die Daten, für die es gebaut wurde.

### 1.1 Einordnung in den Autorenzyklus

```
   Modellieren (construction-freecad-bim)
        │
        ├─ § 1.6 Verbindungs-Preflight, § 4.3 BIM Preflight   ← autorenseitig, advisory
        ▼
   IFC exportieren
        │
        ▼
   Stufe 1+2  ifcopenshell.validate --rules          ← harter Abbruch bei Fehlern
        │
        ▼
   Stufe 3    normative Regeln                        ← Abbruch bei implementer-agreement
        │
        ▼
   Stufe 4    ifctester <projekt>.ids <modell>.ifc    ← Abbruch bei required-Verletzung
        │
        ├─ Befund → § 9 Reparaturzuordnung → zurück ins Autorenmodell
        ▼
   Freigabe-Evidenz (Bericht + BCF) → bim-management § 10/§ 11
```

Regel: **Reparatur immer im Autorenmodell**, nicht in der IFC-Datei. Direkte Eingriffe
in das Exportergebnis (per `ifcpatch` oder Hand) sind zulässig als letzte Stufe für
Dinge, die das Autorenwerkzeug nachweislich nicht kann — und dann dokumentiert und
reproduzierbar als Skript, nie interaktiv. Sonst reißt derselbe Fehler beim nächsten
Export wieder auf. Das ist die Modellprüfungs-Fassung der Regel Nr. 1 aus
`bim-management` § 9.1 („Änderung nie im Koordinationsmodell").

---

## Abschnitt 2: Stufe 1 und 2 — Syntax und Schema

Erste Stufe, billigste Stufe, häufigster stummer Ausfall. Ohne Parameter nur Syntax +
Typprüfung; `--rules` schaltet zusätzlich die im EXPRESS-Schema kodierten
`WHERE`-Regeln und Funktionen ein.

```bash
python -m ifcopenshell.validate modell.ifc --rules
python -m ifcopenshell.validate modell.ifc --rules --json --fields   # maschinenlesbar
```

Optionen (Stand `ifcopenshell` 0.8.x [VERIFY Version]): `--rules` EXPRESS-Regeln,
`--json` JSON-Ausgabe, `--fields` detaillierte Angaben zu fehlgeschlagenen Entitäten
(nur mit `--json`), `--spf` Ausgabe der Entitäten im SPF-Format (nur mit `--json`).
Mehrere Dateien in einem Aufruf sind zulässig.

**Was hier auffällt und sonst nirgends:**

- Attribute mit falschem Datentyp (Zahl, wo `IfcLabel` verlangt ist) — bricht später
  jede Auswertung, ohne dass ein Viewer etwas meldet.
- Fehlende Pflichtattribute, ungültige Enumerationswerte.
- Verletzte `WHERE`-Regeln des Schemas, z. B. Einheiten- und Kontextbedingungen.
- Referenzen ins Leere nach Teilexport oder Nachbearbeitung.

**Automatisierungsregel:** Stufe 1/2 ist ein **harter Gate**. Solange hier Fehler
stehen, sind alle weiteren Befunde Rauschen — Regel- und IDS-Prüfer dürfen dann
beliebig falsch liegen.

---

## Abschnitt 3: Stufe 3 — Normative buildingSMART-Regeln

### 3.1 Was der Regelsatz ist

Der offizielle Regelsatz ist in Gherkin (`.feature`-Dateien) formuliert, maschinell
ausführbar und die Grundlage des bS Validation Service. Umfang im geprüften Stand:
**104 Regeldateien in 34 Regelfamilien**; die Regeln tragen Gültigkeitsstufen als Tags
— im geprüften Stand **76 `@implementer-agreement`, 16 `@industry-practice`, 11
`@informal-proposition`, 9 `@disabled`** (Mehrfachvergabe möglich, daher Summe > Zahl
der Dateien) [VERIFY, der Satz wächst].

Die Stufe entscheidet die Härte des Befunds:

| Tag | Verbindlichkeit | Umgang im Autorenzyklus |
|---|---|---|
| `@implementer-agreement` | maschinell geprüfte Vereinbarung, zertifizierungsrelevant | **Abbruch** — reparieren, nicht wegdiskutieren |
| `@industry-practice` | breite Praxis, nicht normativ | Warnung; Abweichung begründen und im BAP festhalten |
| `@informal-proposition` | Hinweis aus der Spezifikation | protokollieren |
| `@disabled` | zurzeit nicht aktiv | ignorieren, nicht als „bestanden" werten |

### 3.2 Regelfamilien und Hochbau-Filter

| Familie | Thema | Hochbau relevant? |
|---|---|---|
| `PJS` | Projekt, Einheiten (`PJS001` Conversion-Based Units), Elementbezug, **`PJS003` GUID-Format** | **ja, zentral** |
| `SPS` | Räumliche Struktur: `SPS001` Grundstruktur, `SPS002` erlaubte Aggregation, `SPS003` Baugruppen-Zuordnung, `SPS004` keine Mischung aus Containment und Positionierung, `SPS005`/`SPS007` Containment, `SPS008` Container-Repräsentationen | **ja, zentral** |
| `GEM` | Geometrie und Repräsentation: `GEM051` Vorhandensein des geometrischen Kontexts, `GEM052` Subkontexte, `GEM003`/`GEM004` Repräsentationskennungen, `GEM001` Schalenkanten, `GEM002` Raumrepräsentation, `GEM111`–`GEM113` doppelte/kollineare Punkte | **ja** |
| `BLT` | Bauteilspezifika: `BLT001` Türen-`OperationType`, `BLT002` Fenster-`PartitioningType`, `BLT003` Treppen-Zerlegung | **ja** |
| `OJT` | `OJT001` korrekte Verwendung von `PredefinedType`/`USERDEFINED` | **ja** |
| `PSE` | `PSE001` standardisierte `Pset_`, `PSE002` benutzerdefinierte Psets | **ja** |
| `QTY` | `QTY000` Mengen am Objekt, `QTY001` standardisierte `Qto_` | **ja** |
| `MAT`, `CLS`, `DOC`, `LAY`, `CTX` | Material, Klassifikation, Dokumente, Layer, Darstellung | ja, je nach Lieferumfang |
| `BRP`, `SWE`, `TAS` | Selbstdurchdringungen, Ebenheit, Profilränder, Spiegelung in `IfcDerivedProfileDef` | **ja — die Geometriefallen erzeugter Modelle** |
| `LOP`, `OJP`, `GDP`, `BBX`, `AXG` | Platzierung, Achsen, Bounding-Box | ja |
| `GRF` | Georeferenzierung, EPSG, CRS-Einheiten | ja, sobald Lagebezug vereinbart ist |
| `IFC` | `IFC101` nur offizielle IFC-Versionen, `IFC102` keine veralteten Entitäten, `IFC105`/`IFC106` Referenzierung von Resource-Entitäten, `IFC430`/`IFC431` MVD-Umfang | **ja** |
| `GRP`, `SYS`, `POR`, `ASM`, `SPA`, `ANN`, `VRT`, `VER` | Gruppen, Systeme, Ports, Baugruppen, Räume, Annotationen, virtuelle Elemente, Versionierung | je nach Disziplin |
| `ALB`, `ALS`, `LIP`, `MPD` | **Achsen/Alignment, lineare Platzierung — Infrastruktur** | **nein** — 26 der 104 Regeln betreffen Trassierung und sind im Hochbau nie anwendbar; sie als „nicht anwendbar" zu erwarten ist normal, nicht verdächtig |

### 3.3 Die Regeln, an denen erzeugte Modelle typisch scheitern

| Regel | Inhalt (verifiziert aus dem Regeltext) | Warum ein generiertes Modell scheitert |
|---|---|---|
| **`PJS003`** | `GlobalId` muss **exakt 22 Zeichen** lang sein, nur Zeichen aus `0123456789A–Za–z_$`, und das **erste Zeichen muss `0`, `1`, `2` oder `3`** sein | Selbstgebaute oder aus UUID-Hex umkodierte IDs verletzen Länge oder Anfangszeichen; das bricht anschließend jede BCF- und CAFM-Verknüpfung (`bim-management` § 8.4) |
| **`SPS001`** | höchstens **1** `IfcSite`; mindestens **1** `IfcBuilding`; das `IfcBuilding` muss der `IfcSite` zugeordnet sein — gibt es keine `IfcSite`, dem `IfcProject` | Skriptgenerierte Modelle erzeugen Bauteile ohne vollständige Kette `Project → Site → Building → Storey` |
| **`SPS002`** | jedes `IfcSpatialElement` muss gemäß Kompositionstabelle aggregiert sein (Auszug Hochbau: `IfcBuilding` unter `IfcProject`/`IfcSite`/`IfcBuilding`; `IfcBuildingStorey` **nur** unter `IfcBuilding` oder `IfcBuildingStorey`; `IfcSite` unter `IfcProject`/`IfcSite`; `IfcSpace` unter `IfcProject`/`IfcSite`/`IfcBuilding`/`IfcBuildingStorey`/`IfcSpace`) | Geschoss direkt unter `IfcSite` gehängt, Raum unter dem Bauteil statt unter dem Geschoss |
| **`SPS004`** | keine Kombination aus Containment und Positionierung | doppelte Verortung desselben Objekts |
| **`OJT001`** | ist `PredefinedType` = `USERDEFINED`, **muss** `ObjectType` (am Vorkommnis) bzw. `ElementType` (am Typobjekt) gefüllt sein; ein `IfcTypeObject` darf nicht mit `NOTDEFINED` beginnen | Generator setzt `USERDEFINED` als Ausweichwert und lässt den Klartext leer |
| **`GEM051`/`GEM052`** | mindestens ein `IfcGeometricRepresentationContext`; `ContextType` muss `Model`, `Plan` oder `NotDefined` sein | Kontext fehlt oder trägt Fantasie-`ContextType` |
| **`GEM003`/`GEM004`** | eindeutige und gültige Repräsentationskennungen; gültige `RepresentationIdentifier` sind u. a. `Body`, `Body-Fallback`, `Axis`, `Box`, `FootPrint`, `Profile`, `Surface`, `Reference`, `Clearance`, `CoG`, `Annotation`, `Lighting`; gültige `RepresentationType` u. a. `SweptSolid`, `AdvancedSweptSolid`, `Brep`, `AdvancedBrep`, `CSG`, `Clipping`, `Tessellation`, `SurfaceModel`, `BoundingBox`, `MappedRepresentation` | freie Benennung („Geometry", „Solid") oder Doppelvergabe |
| **`BRP003` / `BRP001` / `SWE001` / `TAS001`** | ebene Flächen müssen eben sein; Polyeder-Ränder, Profilränder und Polygonflächen dürfen sich nicht selbst schneiden | Boolesche Operationen und Tessellierung erzeugen entartete Flächen, die kein Viewer anzeigt |
| **`IFC102`** | veraltete Entitäten dürfen **nicht exportiert** werden — betrifft im Hochbau u. a. `IfcWallStandardCase`, `IfcSlabStandardCase`, `IfcDoorStandardCase`, `IfcWindowStandardCase`, `IfcBeamStandardCase`, `IfcColumnStandardCase`, `IfcMemberStandardCase`, `IfcPlateStandardCase`, `IfcOpeningStandardCase`, `IfcWallElementedCase`, `IfcSlabElementedCase`, `IfcProxy`, `IfcDoorStyle`/`IfcWindowStyle`, `IfcDoorLiningProperties`/`IfcWindowLiningProperties`, `IfcDoorPanelProperties`/`IfcWindowPanelProperties`, `IfcPostalAddress`, `IfcTextLiteral`, `IfcMaterialList`, `IfcFaceBasedSurfaceModel`, `IfcBuildingSystem`, `IfcTrapeziumProfileDef`; außerdem einzelne `PredefinedType`-Werte wie `IfcWall`/`STANDARD`, `IfcWall`/`POLYGONAL`, `IfcSpace`/`INTERNAL`, `IfcSpace`/`EXTERNAL` | ältere Exporter und ältere Vorlagen schreiben genau diese Klassen; deckt sich mit der Deprecation-Tabelle in `bim-management` § 8.8 |
| **`PSE001`/`PSE002`** | ein Pset, dessen Name mit `Pset_` beginnt, muss der Standarddefinition entsprechen: gültiger Name, gültige Merkmalsnamen, zulässige Objektklasse, richtiger Merkmalstyp, richtiger Datentyp | **der häufigste Fehler überhaupt**: eigene Merkmale in ein `Pset_…` geschrieben. Der Präfix `Pset_`/`Qto_` ist reserviert — eigene Merkmale gehören in ein eigenes Pset mit Projektpräfix (`bim-management` § 8.6) |
| **`BLT003`** | `IfcStair` darf nur aus `IfcStairFlight`, `IfcSlab` und `IfcRailing` aggregiert werden | Treppe als ein einziger Solid ohne Zerlegung |
| **`QTY000`/`QTY001`** | Mengen am Objekt, standardisierte `Qto_`-Definitionen | Mengen gar nicht exportiert oder frei benannt — siehe `bim-management` § 8.7 |

### 3.4 Ausführung

Öffentlicher Dienst: **buildingSMART Validation Service**, `https://validate.buildingsmart.org/`
— Anmeldung erforderlich, akzeptiert **unkomprimierte STEP-Dateien mit Endung `.ifc`
bis 256 MB**; prüft STEP-Syntax, IFC-Schema und normative Regeln. bSDD-Prüfung ist im
Dienst **deaktiviert** (Stand der Dokumentation zu v0.6.6) [VERIFY]. IDS wird dort
nicht geprüft — Stufe 4 läuft separat.

Lokal reproduzierbar (für den automatisierten Zyklus die einzige brauchbare Variante):
Regelsatz-Repository klonen und

```bash
pytest -sv                       # alle Regeln
python test/test_main.py sps001  # eine Regel gezielt debuggen
```

**Datenschutz-/Vertraulichkeitshinweis:** Der Validation Service ist ein externer Dienst
— eine Modelldatei dorthin zu laden ist eine Veröffentlichung gegenüber Dritten. Bei
vertraulichen Projekten nur die lokale Variante verwenden; das ist in der AIA zu
regeln.

---

## Abschnitt 4: Stufe 4 — IDS (Information Delivery Specification)

### 4.1 Was IDS ist und wo es hingehört

IDS ist der buildingSMART-Standard, um Informationsanforderungen so zu formulieren,
dass sie **gleichzeitig von Menschen gelesen und von Maschinen geprüft** werden
können. Dateiendung `.ids`, XML, Namensraum `http://standards.buildingsmart.org/IDS`,
Schema `ids.xsd` in der Fassung **1.0.0**, offizieller Standard seit Release `v1.0.0`
vom 3. Juni 2024.

Prozessuale Einordnung (Anschluss `bim-management` § 8.1): Die Kette ist
`Anwendungsfall → Process Map → Exchange Requirements → maschinenlesbare Prüfregel`.
**IDS besetzt die letzte Stufe und ersetzt die Element-/Attributmatrix als
Lieferbeschreibung.** Eine AIA-Anlage „Pflichtattribute je Objektklasse je Data Drop"
als Tabelle ist nicht prüfbar; dieselbe Anlage als `.ids` ist es. Praktische Folge: die
AIA liefert eine `.ids` mit, jeder Planungsbeteiligte prüft sein Fachmodell vor dem
Hochladen selbst, und die Prüfstelle prüft mit **derselben Datei**.

IDS ist **kein Ersatz für MVD**: die MVD legt fest, welche Schema-Teilmenge überhaupt
transportiert wird; IDS legt fest, welche Inhalte darin gefüllt sein müssen. Beides
gehört in die AIA.

### 4.2 Aufbau einer `.ids`-Datei

```
ids
├── info                         (Metadaten der Datei)
│   ├── title                    PFLICHT
│   ├── copyright, version, description, author, date, purpose, milestone   optional
└── specifications
    └── specification            1..n
        ├── @name                PFLICHT
        ├── @ifcVersion          PFLICHT — Liste aus IFC2X3 | IFC4 | IFC4X3_ADD2
        ├── @identifier, @description, @instructions    optional
        ├── applicability        (worauf es zutrifft)   @minOccurs/@maxOccurs
        │   ├── entity           0..1
        │   ├── partOf           0..n
        │   ├── classification   0..n
        │   ├── attribute        0..n
        │   ├── property         0..n
        │   └── material         0..n
        └── requirements         (was dann gelten muss)  @description
            └── dieselben sechs Facets, je mit @cardinality und @instructions
```

Regeln, die aus dem Schema folgen und regelmäßig verletzt werden:

- `title` ist das **einzige** Pflichtfeld in `info`. `author` ist, wenn gesetzt, auf ein
  E-Mail-Muster eingeschränkt (`[^@]+@[^\.]+\..+`) — ein Name statt einer Adresse macht
  die Datei schema-ungültig.
- `ifcVersion` ist eine **Liste**: `ifcVersion="IFC4 IFC4X3_ADD2"` ist zulässig. Andere
  Werte als die drei genannten sind ungültig — insbesondere gibt es **kein `IFC4X3`
  ohne `_ADD2`**.
- In `applicability` ist `entity` auf **höchstens eines** beschränkt, alle anderen
  Facets sind beliebig oft erlaubt.
- Die `entity`-Facet in `requirements` hat **keine** `cardinality` — sie gilt immer als
  `required`. Einschränkungen werden dort positiv über `xs:enumeration`/`xs:pattern`
  formuliert, nicht über eine Verbotsform.
- `partOf` kennt in `requirements` nur `required` und `prohibited`, **nicht**
  `optional`. Alle übrigen Facets kennen alle drei.
- `instructions` ist an jeder Facet und an der Spezifikation zulässig und **soll**
  gefüllt werden: der Text ist dafür gedacht, im Autorenwerkzeug angezeigt zu werden —
  er ist die Anleitung an die modellierende Seite, nicht Dekoration.

### 4.3 Kardinalität — die zwei Ebenen, die verwechselt werden

**Ebene 1 — Kardinalität der Applicability** (`minOccurs`/`maxOccurs` am
`applicability`-Element): Wie viele passende Objekte im Modell erwartet werden.

| `minOccurs` | `maxOccurs` | Bedeutung | Auslegung |
|---|---|---|---|
| 1 | unbounded | **required** | Mindestens ein passendes Objekt **muss** vorhanden sein, und alle müssen die Anforderungen erfüllen |
| 0 | unbounded | **optional** | Passende Objekte dürfen fehlen; sind welche da, müssen alle die Anforderungen erfüllen |
| 0 | 0 | **prohibited** | Es darf **kein** passendes Objekt geben; die Anforderungen werden dann gar nicht ausgewertet |

`prohibited` ist das Werkzeug für Negativanforderungen: „im Modell darf keine tragende
Wand vorkommen", „keine Platzhalter-Proxys mehr im Abgabestand".

**Ebene 2 — Kardinalität der einzelnen Anforderung** (`cardinality` an der Facet in
`requirements`):

| Wert | Erfolgskriterium |
|---|---|
| `required` | Merkmal ist vorhanden, hat den erwarteten Datentyp und einen **nicht leeren** Wert |
| `prohibited` | Merkmal darf am passenden Objekt **nicht** vorhanden sein |
| `optional` | Merkmal darf fehlen; ist es da, muss es Datentyp und Wertebedingung erfüllen |

Der übliche Fehler: „optional" zu schreiben, wo „darf fehlen, aber wenn vorhanden dann
richtig" gemeint ist — das ist korrekt —, und dann zu erwarten, dass ein fehlendes
Merkmal gemeldet wird. Wird es nicht.

### 4.4 Die sechs Facets

| Facet | Parameter | Pflicht | Restrictions erlaubt |
|---|---|---|---|
| **Entity** | `name` (IFC-Klasse, **GROSSBUCHSTABEN**, exakte Übereinstimmung) | ✔ | ✔ |
| | `predefinedType` (GROSSBUCHSTABEN, Schemawert oder eigener Text) | ✘ | ✔ |
| **Attribute** | `name` (gültiger Attributname aus dem Schema) | ✔ | ✔ |
| | `value` | ✘ | ✔ |
| **Classification** | `system` | ✔ | ✔ |
| | `value` | ✘ | ✔ |
| **Property** | `propertySet` | ✔ | ✔ |
| | `baseName` (Merkmalsname **wie in der IFC-Datei gespeichert**, nicht die übersetzte Anzeigeform) | ✔ | ✔ |
| | `value` | ✘ | ✔ |
| | `@dataType` (IFC-Defined-Type, GROSSBUCHSTABEN) | ✘ | — |
| **Material** | `value` | ✘ | ✔ |
| **PartOf** | verschachtelte `entity`-Facet (GROSSBUCHSTABEN) | ✔ | ✔ |
| | `@relation` | ✘ | — |

Wichtige Einzelheiten:

- **`baseName`, nicht Anzeigename.** Der Name im Modell ist `FireRating`, nicht
  „Feuerwiderstandsklasse". Die deutschen Benennungen aus bSDD
  (`bim-management` § 8.9) sind für Menschen, nicht für die Prüfregel.
- **Nur Vorkommnis-/Typauflösung wie im Schema.** Für `predefinedType` gilt die
  Auflösungskette: ist das Objekt durch einen Typ definiert (`IfcRelDefinesByType`) und
  hat der Typ `PredefinedType = USERDEFINED`, gilt dessen `ElementType`; hat er einen
  anderen Wert, gilt dieser; sonst wird am Vorkommnis weitergesucht, wo bei
  `USERDEFINED` der `ObjectType` gilt.
- **`partOf` navigiert rekursiv.** Zulässige Werte für `@relation`:
  `IFCRELAGGREGATES`, `IFCRELASSIGNSTOGROUP`, `IFCRELCONTAINEDINSPATIALSTRUCTURE`,
  `IFCRELNESTS` sowie das Paar `IFCRELVOIDSELEMENT IFCRELFILLSELEMENT` (als **ein**
  Enumerationswert mit Leerzeichen geschrieben). Ohne `@relation` werden **alle**
  Beziehungsarten rekursiv ausgewertet — das ist mächtiger und unschärfer; für
  Lieferprüfungen die Relation immer angeben.
- **Property-Typen.** IDS kann `IfcPropertySingleValue`, `IfcPropertyBoundedValue`,
  `IfcPropertyListValue`, `IfcPropertyTableValue` und `IfcPropertyEnumeratedValue`
  prüfen. **Nicht unterstützt: `IfcComplexProperty` und `IfcPropertyReferenceValue`.**
  Wer Dokumentverweise (etwa `Pset_ManufacturerTypeInformation`
  `PerformanceCertificate`) per IDS erzwingen will, kann das nicht — das bleibt
  organisatorische Prüfung.
- Bei Listen-/Tabellenwerten gilt: ein **einfacher** IDS-Wert ist erfüllt, wenn
  **mindestens einer** der IFC-Werte passt; eine **Bereichs**-Restriction muss von
  **allen** IFC-Werten eingehalten werden.
- **Quantities werden wie Properties geprüft** — `Qto_WallBaseQuantities` steht im
  `propertySet`, `NetVolume` im `baseName`.

### 4.5 Complex Restrictions

Statt eines festen Werts (`simpleValue`) kann jeder Parameter eine `xs:restriction`
tragen. Vier Formen:

| Form | Wofür | Knoten |
|---|---|---|
| **Enumeration** | Auswahlliste zulässiger Werte | `xs:enumeration` |
| **Pattern** | Benennungskonvention als Regex | `xs:pattern` |
| **Bounds** | Zahlenbereich | `xs:minInclusive`, `xs:maxInclusive`, `xs:minExclusive`, `xs:maxExclusive` |
| **Length** | Zeichenlänge | `xs:length`, `xs:minLength`, `xs:maxLength` |

Der `base`-Typ der Restriction muss zum `dataType` passen: `xs:string` für Text- und
Enumerationstypen, `xs:double` für Maßtypen, `xs:boolean`, `xs:integer`, `xs:date`,
`xs:dateTime`, `xs:time`, `xs:duration`. Nicht jeder Knoten ist bei jedem Basistyp
erlaubt — `xs:boolean` kennt nur `xs:pattern`, Längenknoten gibt es nur bei
`xs:string`, Bereichsknoten nur bei den numerischen und Datums-/Zeittypen.

Schreibweisen, die sonst still fehlschlagen:

- Zahlen mit **Punkt** als Dezimaltrenner, **kein** Tausendertrenner: `4.2` gültig,
  `1.234,5` ungültig. Wissenschaftliche Notation (`1e3`) ist zulässig.
- Booleans: `true`, `false`, `0` oder `1` — **kleingeschrieben**. `TRUE` in einer
  `xs:boolean`-Restriction ist ungültig.
- Regex ist die XML-Schema-Variante, nicht der volle Perl-Umfang. Nützliche Muster:
  `WT[0-9]{2}` (genau zwei Ziffern), `DT.*` (Präfix), `.*DT.*` (enthält),
  `[0-9]{2}\.[0-9]{2}` (Kostengruppe zweistufig).

### 4.6 Einheiten und Toleranz — die zwei stillen Killer

**Einheiten:** IDS drückt Maßwerte **immer in SI-Basiseinheiten** aus: Länge in
**Metern**, Fläche in m², Volumen in m³, Kraft in N, Masse in kg, Temperatur in K,
Winkel in rad. Das Modell darf beliebige Einheiten führen (`IfcUnitAssignment`); der
Prüfer muss vor dem Vergleich umrechnen. **Konsequenz für Autorenwerkzeuge, die in
Millimetern arbeiten:** Eine Anforderung „Wanddicke mindestens 240 mm" heißt in IDS
`minInclusive = 0.24`. Wer `240` schreibt, prüft auf 240 Meter und bekommt eine
Spezifikation, die nie erfüllt wird — oder, bei `maxInclusive`, eine, die immer erfüllt
ist und nie etwas findet. **Das ist der häufigste stumme Fehler in selbstgeschriebenen
IDS-Dateien.** Umgekehrt gilt: IDS kann **nicht** verlangen, dass eine Länge in einer
bestimmten Einheit gespeichert ist — nur, welchen Wert sie in SI hat.

**Gleichheitstoleranz:** Fließkommavergleiche laufen mit einer festen, **nicht
konfigurierbaren** Toleranz `ε = 1.0e-6` nach

```
x == v  ⇔  (v − |v|·ε − ε) < x < (v + |v|·ε + ε)
```

Das ergibt bei `v = 1.0` eine Bandbreite von ±2e-6, bei `v = 100000.0` von ±0.1.
**Auf Bereiche (`minInclusive` usw.) wird die Toleranz nicht angewandt** — dort wird
exakt verglichen. Wer eine Bautoleranz abbilden will, muss sie deshalb **explizit als
Bereich** schreiben; die eingebaute Toleranz ist ausschließlich für Rundungsfehler
gedacht, nicht für Maßtoleranzen nach DIN 18202. Umgekehrt lässt sich mit
`v <= x <= v` ein toleranzfreier Vergleich erzwingen.

### 4.7 Was IDS nicht kann

Aus der Spezifikation selbst, wörtlich als Abgrenzung geführt — und deshalb die Liste,
die in die AIA gehört, damit niemand diese Prüfungen von der IDS erwartet:

| Nicht prüfbar | Zuständig stattdessen |
|---|---|
| Kollisionen zwischen Bauteilen | Clash-Detection-Werkzeug — `bim-management` § 12 |
| Geometrische Bedingungen („3 m Abstand zur Grundstücksgrenze") | Regelprüfwerkzeug/Skript; Grundlagen `building-planning-spatial` |
| Summen und Aggregate („alle Büroflächen zusammen > 300 m²") | Auswertung/Mengenwerkzeug, z. B. `ifccsv`/`ifc5d` |
| Eindeutigkeit („alle Türtypnamen verschieden") | Skript über das Modell |
| Berechnete oder dynamische Werte | Fachrechnung, FEM — `structural-analysis`, `construction-freecad-bim` § 7 |
| Abgleich mit Daten außerhalb des Modells (CDE-Revisionsstand, Lieferantenlisten) | CDE-/Prozessprüfung — `bim-management` § 3 |
| Modellierungsart („Bewehrung als parametrischer Sweep") | Modellierungsrichtlinie als BAP-Anlage |
| `IfcComplexProperty`, `IfcPropertyReferenceValue` | organisatorische Prüfung |
| Geometrie überhaupt | Stufe 3 (BRP/SWE/TAS/GEM) und Fachprüfung |

---

## Abschnitt 5: Einen DACH-Startsatz an Spezifikationen schreiben

### 5.1 Vorlage

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ids:ids xmlns:ids="http://standards.buildingsmart.org/IDS"
         xmlns:xs="http://www.w3.org/2001/XMLSchema"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://standards.buildingsmart.org/IDS
                             http://standards.buildingsmart.org/IDS/1.0/ids.xsd">
  <ids:info>
    <ids:title>Mindestlieferumfang Architektur — Data Drop LPH 3</ids:title>
    <ids:version>1.0</ids:version>
    <ids:date>2026-09-21</ids:date>
    <ids:purpose>Koordination, Mengenermittlung, Nachweisvorbereitung</ids:purpose>
    <ids:milestone>LPH 3 Entwurfsplanung</ids:milestone>
  </ids:info>
  <ids:specifications>

    <ids:specification name="Aussenwaende: U-Wert und Feuerwiderstand"
                       ifcVersion="IFC4"
                       identifier="ARC-WALL-01"
                       description="U-Wert und Feuerwiderstand der Aussenwaende sind
                                    Grundlage des GEG-Nachweises und des Brandschutzkonzepts."
                       instructions="Architektur traegt die Werte am Wandtyp ein.
                                     U-Wert in W/(m2K), Feuerwiderstand als Klasse nach DIN EN 13501-2.">
      <ids:applicability minOccurs="1" maxOccurs="unbounded">
        <ids:entity>
          <ids:name><ids:simpleValue>IFCWALL</ids:simpleValue></ids:name>
        </ids:entity>
        <ids:property>
          <ids:propertySet><ids:simpleValue>Pset_WallCommon</ids:simpleValue></ids:propertySet>
          <ids:baseName><ids:simpleValue>IsExternal</ids:simpleValue></ids:baseName>
          <ids:value><ids:simpleValue>TRUE</ids:simpleValue></ids:value>
        </ids:property>
      </ids:applicability>
      <ids:requirements>
        <ids:property dataType="IFCTHERMALTRANSMITTANCEMEASURE" cardinality="required">
          <ids:propertySet><ids:simpleValue>Pset_WallCommon</ids:simpleValue></ids:propertySet>
          <ids:baseName><ids:simpleValue>ThermalTransmittance</ids:simpleValue></ids:baseName>
          <ids:value>
            <xs:restriction base="xs:double">
              <xs:maxInclusive value="0.24"/>
            </xs:restriction>
          </ids:value>
        </ids:property>
        <ids:property dataType="IFCLABEL" cardinality="required">
          <ids:propertySet><ids:simpleValue>Pset_WallCommon</ids:simpleValue></ids:propertySet>
          <ids:baseName><ids:simpleValue>FireRating</ids:simpleValue></ids:baseName>
          <ids:value>
            <xs:restriction base="xs:string">
              <xs:enumeration value="F30"/>
              <xs:enumeration value="F60"/>
              <xs:enumeration value="F90"/>
              <xs:enumeration value="REI 30"/>
              <xs:enumeration value="REI 60"/>
              <xs:enumeration value="REI 90"/>
            </xs:restriction>
          </ids:value>
        </ids:property>
      </ids:requirements>
    </ids:specification>

    <ids:specification name="Keine Platzhalter-Proxys im Abgabestand"
                       ifcVersion="IFC4"
                       identifier="ARC-PROXY-01"
                       description="IfcBuildingElementProxy ist unklassifiziert und damit
                                    weder mengen- noch regelpruefbar.">
      <ids:applicability minOccurs="0" maxOccurs="0">
        <ids:entity>
          <ids:name><ids:simpleValue>IFCBUILDINGELEMENTPROXY</ids:simpleValue></ids:name>
        </ids:entity>
      </ids:applicability>
    </ids:specification>

  </ids:specifications>
</ids:ids>
```

Beachte an der Vorlage: `maxInclusive value="0.24"` ist ein **U-Wert** in W/(m²K), also
zufällig einheitenneutral — eine Wanddicke von 240 mm wäre ebenfalls `0.24`, dann aber
in **Metern** (§ 4.6). Die zweite Spezifikation nutzt `minOccurs="0" maxOccurs="0"`,
hat deshalb **keine** `requirements` und ist die kompakteste Form einer
Negativanforderung.

### 5.2 Startsatz — was in fast jede DACH-Hochbau-IDS gehört

Abgeleitet aus den Common Psets in `bim-management` § 8.6; die Merkmalsnamen sind dort
belegt. Ein Startsatz ersetzt nicht die projektspezifische AIA, er verhindert nur, dass
man bei null anfängt.

| # | Applicability | Anforderung | Begründung / Anschluss |
|---|---|---|---|
| 1 | `IFCBUILDINGSTOREY` | Attribut `Name` nach Muster (z. B. `(UG\|EG\|[0-9]{1,2}\.OG\|DG)`), `Elevation` vorhanden | Geschosslogik, reale Höhenlage — `construction-freecad-bim` § 2.1 |
| 2 | alle Bauteile | `partOf` `relation="IFCRELCONTAINEDINSPATIALSTRUCTURE"` `entity=IFCBUILDINGSTOREY`, `cardinality="required"` | kein Bauteil ohne Geschoss; ergänzt `SPS001`/`SPS002` projektseitig |
| 3 | `IFCWALL` mit `IsExternal=TRUE` | `ThermalTransmittance` (`IFCTHERMALTRANSMITTANCEMEASURE`), `FireRating`, `LoadBearing` | GEG-Nachweis, Brandschutz, Lastabtrag — `building-physics-thermal-moisture`, `fire-protection-building` |
| 4 | `IFCWALL` mit `LoadBearing=TRUE` | `Pset_ConcreteElementGeneral` `StrengthClass` und `ExposureClass` (falls Beton) | `concrete-detailing` |
| 5 | `IFCSLAB` `PredefinedType=FLOOR` | `Qto_SlabBaseQuantities` `NetVolume` und `NetArea`, `LoadBearing`, `AcousticRating` | Mengen und Schallschutz — `bim-management` § 8.7, `building-acoustics` |
| 6 | `IFCDOOR` | `FireRating`, `SelfClosing`, `FireExit`, `HandicapAccessible`, Attribut `Name` nach Türkennzeichen-Muster | Flucht- und Rettungswege, Barrierefreiheit — `fire-protection-building`, `accessibility-universal-design` |
| 7 | `IFCWINDOW` | `ThermalTransmittance`, `GlazingAreaFraction`, `IsExternal` | `openings-windows-doors` |
| 8 | `IFCSPACE` | `Qto_SpaceBaseQuantities` `NetFloorArea` und `Height`; Attribut `Name` und `LongName` gefüllt | Raumbuch, Flächenermittlung — Ableitung auf DIN 277 bleibt Rechenvorschrift im BAP |
| 9 | `IFCSITE` | `Pset_SiteCommon` `SiteCoverageRatio` (GRZ) und `FloorAreaRatio` (GFZ) | B-Plan-Kennwerte am Modell — `building-planning-spatial` |
| 10 | `IFCBUILDING` | `Pset_BuildingCommon` `NumberOfStoreys`, `YearOfConstruction`, `IsLandmarked` | Stammdaten; im Bestand zwingend — `building-renovation-refurbishment` |
| 11 | alle Bauteile, Bestandsprojekt | `Pset_*Common` `Status` aus `NEW\|EXISTING\|DEMOLISH\|TEMPORARY` | Bestand/Neu/Abbruch maschinell unterscheidbar — `existing-structures-retrofit` |
| 12 | `IFCBUILDINGELEMENTPROXY` | `minOccurs=0 maxOccurs=0` (verboten) | Klassifizierbarkeit erzwingen |
| 13 | alle Bauteile | `material` `cardinality="required"` | Grundlage für Mengen, LCA, Ressourcenpass — `sustainable-construction` |
| 14 | alle Bauteile | `classification` `system` = vereinbartes System, `value` nach Muster | Kosten-/FM-Anschluss — `cost-management-din276` |

**Reihenfolge der Einführung:** 1, 2, 12 zuerst — Struktur und Klassifizierbarkeit.
Erst wenn die grün sind, haben 3–11 überhaupt Aussagekraft, weil sie sonst auf zu
wenigen oder falsch eingeordneten Objekten greifen.

### 5.3 Die IDS-Datei selbst prüfen

Eine fehlerhafte `.ids` meldet keine Fehler — sie findet nichts und sieht damit aus wie
ein bestandener Test. **Jede selbst geschriebene oder generierte IDS vor dem Einsatz
gegen das Schema prüfen** (offizielles IDS-Audit-Tool von buildingSMART, oder
mindestens XSD-Validierung gegen `ids.xsd`) und anschließend **gegen ein Modell, von
dem bekannt ist, dass es durchfallen muss**. Der Regeltest ohne Negativfall ist kein
Test — der offizielle IDS-Testfallsatz folgt genau dieser Logik und führt
**374 `pass`-, 240 `fail`- und 54 `invalid`-Fälle**.

```bash
python -c "
import lxml.etree as ET
schema = ET.XMLSchema(ET.parse('ids.xsd'))
doc = ET.parse('projekt.ids')
schema.assertValid(doc)
print('IDS schema-gueltig')
"
```

---

## Abschnitt 6: Werkzeugkette

### 6.1 Aufrufe

```bash
# Stufe 1+2 — Syntax und Schema
python -m ifcopenshell.validate modell.ifc --rules
python -m ifcopenshell.validate modell.ifc --rules --json --fields > schema.json

# Stufe 4 — IDS
python -m ifctester projekt.ids modell.ifc                        # Konsole
python -m ifctester projekt.ids modell.ifc -r Json -o bericht.json
python -m ifctester projekt.ids modell.ifc -r Html -o bericht.html
python -m ifctester projekt.ids modell.ifc -r Bcf  -o befunde.bcf
python -m ifctester projekt.ids modell.ifc -r Ods  -o bericht.ods --excel-safe
```

Reporter: `Console` (Vorgabe, `--no-color` für Protokolle), `Txt`, `Json`, `Html`,
`Ods`, `Bcf`. **`-r Bcf` ist der wichtigste**: der Befund wird damit zum
BCF-Issue mit GUID-Referenz und läuft ohne Bruch in das Issue-Management aus
`bim-management` § 11 — kein Abtippen, keine Screenshots, keine Modellkopie.

### 6.2 Programmatisch (für den automatisierten Zyklus)

```python
import ifcopenshell
from ifctester import ids, reporter

specs = ids.open("projekt.ids")
model = ifcopenshell.open("modell.ifc")
specs.validate(model)

engine = reporter.Json(specs)
engine.report()
engine.to_file("bericht.json")
```

Eine IDS lässt sich auch im Code aufbauen (`ids.Ids`, `ids.Specification`,
`ids.Entity`, `ids.Property`, …) — nützlich, um die Lieferanforderung **aus derselben
Quelle** zu erzeugen, aus der das Modell erzeugt wird, statt sie doppelt zu pflegen.

### 6.3 Werkzeugübersicht

| Werkzeug | Rolle | Anmerkung |
|---|---|---|
| `ifcopenshell.validate` | Stufe 1+2 | Teil von `ifcopenshell`; Kernbibliothek liegt auch dem FreeCAD-BIM-Arbeitsbereich zugrunde |
| `ifctester` | Stufe 4, IDS-Prüfung und IDS-Erzeugung | CLI, Python-API, Webanwendung |
| IDS-Audit-Tool (buildingSMART) | prüft die **`.ids`-Datei** gegen den vollen IDSxml-Standard | die Prüfung der Prüfung (§ 5.3) |
| bS Validation Service | Stufe 1–3 als Dienst | `.ifc` unkomprimiert, ≤ 256 MB, Anmeldung; externer Dienst — Vertraulichkeit beachten |
| Gherkin-Regelsatz | Stufe 3 lokal | `pytest -sv`, Einzelregel über `test_main.py` |
| `ifcpatch` | gezielte Reparatur am Exportergebnis | s. § 9 |
| `ifccsv`, `ifc5d` | Auswertung/Mengen für das, was IDS nicht kann (§ 4.7) | |
| `ifcdiff` | Modellvergleich zweier Stände | Revisionsnachweis, Anschluss `bim-management` § 3.3 |
| `bcf` | BCF-Erzeugung und -Verarbeitung | Anschluss `bim-management` § 11 |

[VERIFY Paketnamen und Optionen gegen die installierte Fassung — die Werkzeugkette
entwickelt sich schnell.]

---

## Abschnitt 7: Der Prüfzyklus für erzeugte Modelle

### 7.1 Gates

| Gate | Bedingung für „weiter" | Bei Verletzung |
|---|---|---|
| **G0 — Autorenseite** | Preflight des Autorenwerkzeugs ohne offene Strukturbefunde (`construction-freecad-bim` § 4.3) | im Modell beheben, **vor** dem Export |
| **G1 — Syntax/Schema** | `ifcopenshell.validate --rules` ohne Fehler | harter Abbruch; alle weiteren Befunde sind ungültig |
| **G2 — Normativ** | keine Verletzung mit Tag `@implementer-agreement` | Abbruch; `@industry-practice` nur protokollieren |
| **G3 — IDS** | keine Verletzung einer `required`-Anforderung | Abbruch; `optional`-Befunde protokollieren |
| **G4 — Evidenz** | Berichte (Schema-JSON, Regelbericht, IDS-Bericht, BCF) archiviert und dem Modellstand zugeordnet | ohne Evidenz keine Freigabe — die Prüfung ist sonst nicht nachvollziehbar |

### 7.2 Abbruchkriterien für eine automatisierte Schleife

Ohne Abbruchkriterien dreht eine Reparaturschleife endlos oder verschlimmbessert.

1. **Kein Fortschritt:** Zwei aufeinanderfolgende Durchläufe mit identischer
   Befundmenge → anhalten und den Befund an einen Menschen geben. Dasselbe Symptom
   zweimal zu behandeln heißt, die Ursache nicht verstanden zu haben.
2. **Neue Befunde durch die Reparatur:** Die Befundmenge wächst → letzte Änderung
   zurücknehmen. Reparaturen an Geometrie und Platzierung erzeugen regelmäßig neue
   Verstöße an anderer Stelle.
3. **Befund außerhalb des Zuständigkeitsbereichs:** Verstöße, die eine fachliche
   Entscheidung verlangen (welcher Feuerwiderstand? welche Betongüte?), werden **nicht
   geraten**. Ein Platzhalterwert, der eine Prüfung grün macht, ist schlimmer als ein
   roter Befund — er täuscht Vollständigkeit vor, und § 8.6 aus `bim-management` sagt
   genau dafür `VERIFY`.
4. **Obergrenze:** feste maximale Anzahl Durchläufe; danach Zwischenstand, Bericht,
   offene Punkte — wie der Statusblock in `construction-freecad-bim` § 7.3.
5. **FEM-Invalidierung:** Jede geometrische Reparatur entwertet eine zuvor gerechnete
   FEM — siehe `construction-freecad-bim` § 7.4. Die Reihenfolge ist deshalb: erst
   Geometrie und Struktur bereinigen, **dann** rechnen, nicht umgekehrt.

### 7.3 Typische Befundmuster eines generierten Modells

| Symptom im Bericht | Wahrscheinliche Ursache im Erzeugungsschritt |
|---|---|
| Sehr viele `IFCBUILDINGELEMENTPROXY` | Objekte ohne BIM-Typ erzeugt; im Autorenwerkzeug nur `Part`/`Draft`-Formen |
| Alle Bauteile in einem Geschoss oder in keinem | Hierarchie nach dem Erzeugen nicht zugeordnet; Containment-Beziehung fehlt |
| `PJS003`-Verstöße in Masse | GUIDs selbst erzeugt statt vom Werkzeug vergeben |
| Mengen fehlen oder sind 0 | Mengen nicht für den Export markiert (`construction-freecad-bim` § 4.3) — Geometrie kann trotzdem korrekt sein |
| Psets vorhanden, aber Werte leer | Pset angelegt und nicht gefüllt; `required` in IDS verlangt **nicht leer** |
| `PSE001`-Verstöße | eigene Merkmale in ein `Pset_…` geschrieben |
| `BRP003`/`SWE001` | boolesche Operationen oder Tessellierung erzeugen entartete Flächen |
| IDS meldet null Treffer, obwohl Objekte da sind | Applicability greift nicht: Klasse klein statt groß geschrieben, falsches `propertySet`, Einheitenfehler (§ 4.6) |
| Alles grün, Empfänger meldet trotzdem Lücken | die AIA war nicht vollständig in IDS übersetzt — Prüflücke, nicht Modellfehler |

Der letzte Punkt ist der wichtigste: **Eine grüne Prüfung beweist nur die Abdeckung der
geschriebenen Regeln.** Die Vollständigkeit des Regelsatzes ist selbst eine
Projektleistung und gehört in das AIA-Review (`bim-management` § 17).

---

## Abschnitt 8: Befund → Reparatur

| Befund | Reparatur im Autorenmodell | Notfalls am Exportergebnis |
|---|---|---|
| Falsche/fehlende Klasse (Proxy) | BIM-Typ am Objekt setzen, neu exportieren | — (nicht sinnvoll nachträglich) |
| Fehlende Geschosszuordnung | Objekt im Strukturbaum unter das Geschoss hängen | `ResetSpatialElementLocations`, `SplitByBuildingStorey` |
| Falsche Einheit im Modell | Einheiteneinstellung im Projekt korrigieren | `ConvertLengthUnit` |
| Ungültige GUIDs | Erzeugung dem Werkzeug überlassen | `RegenerateGlobalIds` — **bricht bestehende BCF-/CAFM-Verknüpfungen**, nur bei Erstlieferung zulässig |
| Falscher Nullpunkt / Koordinatenlage | Projektnullpunkt korrigieren | `SetWorldCoordinateSystem`, `OffsetObjectPlacements`, `ResetAbsoluteCoordinates`, `SetFalseOrigin` |
| Geschosshöhen falsch | Geschosshöhen im Modell | `OffsetStoreyElevations`, `SetRefElevation` |
| Mengen fehlen | Mengen für Export markieren | `ConvertPropertiesToQuantities` |
| Psets am Typ statt am Vorkommnis (oder umgekehrt) benötigt | Vorkommnis-/Typstrategie klären (`bim-management` § 8.4) | `UnsharePsets` |
| Geometrie entartet / Boolesche Reste | Geometrie im Autorenmodell neu aufbauen | `TessellateElements` — macht das Modell **unbearbeitbar**, nur für reine Ansichts-/Koordinationslieferungen |
| Datei zu groß / Altlasten | — | `Optimise`, `PurgeData`, `RecycleNonRootedElements` |
| Falsche Schemaversion beim Empfänger | Export in der vereinbarten Fassung | `Migrate` — Verluste dokumentieren, siehe `bim-management` § 8.8 |

**Regel zu `ifcpatch`:** Jeder Eingriff am Exportergebnis ist eine **Abweichung
zwischen Autorenmodell und Lieferung** und damit ein Risiko für den nächsten Zyklus.
Zulässig, wenn (a) das Autorenwerkzeug die Anforderung nachweislich nicht erfüllen
kann, (b) der Eingriff als Skript versioniert ist, (c) er im Lieferprotokoll steht.
Sonst gehört die Ursache ins Modell.

---

## Abschnitt 9: Checklisten

### 9.1 IDS-Datei schreiben

- [ ] `info/title` gesetzt; `version`, `date`, `purpose`, `milestone` gefüllt
- [ ] `author`, falls gesetzt, ist eine E-Mail-Adresse
- [ ] `ifcVersion` je Spezifikation gesetzt und passt zur vereinbarten Exportfassung
- [ ] `identifier` je Spezifikation vergeben und innerhalb der Datei eindeutig
- [ ] `description` erklärt das **Warum**, `instructions` sagt, **wer** es **wie** liefert
- [ ] Klassen-, PredefinedType- und Relationsnamen in GROSSBUCHSTABEN
- [ ] `baseName` ist der IFC-Merkmalsname, nicht die deutsche Anzeigeform
- [ ] `dataType` gesetzt, wo ein Typ erzwungen werden soll; `base` der Restriction passt dazu
- [ ] **Alle Maßwerte in SI** (Länge in Metern) geprüft
- [ ] Bautoleranzen explizit als Bereich, nicht auf die eingebaute Toleranz verlassen
- [ ] Negativanforderungen über `minOccurs=0 maxOccurs=0` bzw. `cardinality="prohibited"`
- [ ] `.ids` gegen `ids.xsd` validiert
- [ ] gegen ein **absichtlich fehlerhaftes** Modell geprüft: fällt sie durch?

### 9.2 Vor der Lieferung eines Modells

- [ ] G0 Autoren-Preflight ohne offene Strukturbefunde
- [ ] G1 `ifcopenshell.validate --rules` fehlerfrei
- [ ] G2 keine `@implementer-agreement`-Verletzung
- [ ] G3 keine `required`-Verletzung gegen die Projekt-IDS
- [ ] Schemaversion, MVD und Einheiten entsprechen der AIA
- [ ] Nullpunkt/Georeferenzierung wie vereinbart
- [ ] Berichte erzeugt und dem Modellstand zugeordnet (G4)
- [ ] Offene, bewusst nicht behobene Punkte als BCF übergeben statt verschwiegen

### 9.3 Beim Aufsetzen der Projektprüfung (AIA-Seite)

- [ ] AIA-Informationsanforderungen als `.ids` je Disziplin **und** je Data Drop
- [ ] Prüfstelle und Planungsbeteiligte nutzen **dieselbe** Datei
- [ ] Festgelegt, welche Regelstufe zum Abbruch führt (§ 3.1)
- [ ] Festgelegt, ob extern (Validation Service) oder lokal geprüft wird — Vertraulichkeit
- [ ] Festgelegt, was **nicht** per IDS geprüft wird (§ 4.7) und wer das dann prüft
- [ ] IDS-Versionierung geregelt (semantisch: X = Ergebnis kann kippen, Y = redaktionell)

---

## Abschnitt 10: Zusammenspiel & Verhaltensregeln

| Situation | Zuständiges Skill |
|---|---|
| Entity-/Pset-/Qto-Definition nachschlagen, Schemaversionen vergleichen | `bim-management` § 8.4–8.9 |
| AIA/BAP, Data Drops, Freigabe, Statusmodell, BCF-Prozess, Clash-Detection | `bim-management` |
| Modell erzeugen, Geometrie, Hierarchie, Export, FEM | `construction-freecad-bim` |
| Fachliche Richtigkeit eines geprüften Werts | das jeweilige Fachskill |
| Standardtiefe: wie viel Prüfung ist angemessen | `simple-first-building` |

**Verhaltensregeln:**

1. **Messen statt behaupten.** „Das Modell ist korrekt" ist ohne Bericht keine Aussage.
   Ein Export ist ein Messinstrument — dieselbe Haltung wie die Volumendifferenz und
   der Export-Grep in `construction-freecad-bim` § 2.4/§ 4.4.
2. **Reihenfolge einhalten.** Stufe 4 vor Stufe 1 auszuführen erzeugt Scheinbefunde.
3. **Nie raten, um grün zu werden.** Fehlende Fachwerte bleiben offen und werden
   berichtet. Ein erfundener U-Wert ist ein Sachmangel, kein Fortschritt.
4. **Reparatur an der Ursache**, im Autorenmodell; Eingriffe am Exportergebnis nur
   begründet, skriptiert und protokolliert.
5. **Prüflücke ist kein Modellfehler und umgekehrt.** Wenn der Empfänger etwas
   vermisst, das grün war, ist die Regel unvollständig — das gehört ins AIA-Review,
   nicht in eine Schuldzuweisung an das Modell.
6. **Die Prüfmittel selbst versionieren.** `.ids`, Regelstand und Werkzeugfassungen
   gehören mit dem Modellstand archiviert; ohne sie ist ein alter Bericht nicht
   reproduzierbar (Anschluss Langzeitarchivierung, `bim-management` § 3.6).

---

## Anhang: Normen-, Standard- und Quellenindex

**Normativ/Standard:** DIN EN ISO 16739 (IFC); **IDS 1.0** (buildingSMART-Standard,
Release `v1.0.0` vom 3. Juni 2024, Schema `ids.xsd` Version 1.0.0, Namensraum
`http://standards.buildingsmart.org/IDS`); DIN EN ISO 29481 (IDM — IDS besetzt darin
die maschinenlesbare Stufe); DIN EN ISO 19650-1/-2 (Prüfung als Teil des
Informationsmanagements); DIN EN ISO 23386/23387 (Merkmale, Datenvorlagen);
ISO 10303-21 (STEP-Physical-File); DIN EN 17412 (LOIN). VDI 2552 (BIM-Blätter,
Prüfung/Fertigstellungsgrad) [VERIFY Blattzuordnung].

**Quellen (maschinenlesbar, offen):**

| Inhalt | Ort |
|---|---|
| IDS-Standard, Schema, Nutzerhandbuch, Implementierungsdokumentation, Beispiele, Testfälle | `https://github.com/buildingSMART/IDS` (Zweig `development`; Schema unter `Schema/ids.xsd`, Handbuch unter `Documentation/UserManual/`) |
| IDS-Datei prüfen | `https://github.com/buildingSMART/IDS-Audit-tool` |
| Normative Regeln (Stufe 3) | `https://github.com/buildingSMART/ifc-gherkin-rules` (Regeln unter `features/rules/<FAMILIE>/`, Hilfstabellen unter `features/resources/`) |
| Prüfdienst und dessen Quelltext | `https://validate.buildingsmart.org/` bzw. `https://github.com/buildingSMART/validate`; Nutzerhandbuch `https://buildingsmart.github.io/validate/user/index.html` |
| Werkzeugkette | `https://github.com/IfcOpenShell/IfcOpenShell` (`src/ifctester`, `src/ifcpatch`, `src/ifccsv`, `src/ifc5d`, `src/ifcdiff`, `src/bcf`); Dokumentation `https://docs.ifcopenshell.org/` |
| IFC-Schema, Psets, deutsche Benennungen | siehe `bim-management` § 8.9 |

**Abrufhinweis:** Die Webauftritte von buildingSMART (`buildingsmart.org`,
`standards.buildingsmart.org`, `technical.buildingsmart.org`) antworten auf
automatisierte Abrufe mit **HTTP 403** (Bot-Abwehr). Die Inhalte dieses Anhangs sind
über die genannten Quelltext-Repositories und über `buildingsmart.github.io` ohne
Sperre erreichbar — dasselbe Muster wie in `bim-management` § 8.9 [VERIFY, das
Sperrverhalten ändert sich ohne Ankündigung].

*Ende — dieses Skill prüft Modelle; es erzeugt sie nicht (`construction-freecad-bim`)
und es regelt nicht den Prozess darum (`bim-management`). Ein bestandener Prüflauf ist
Evidenz, keine Freigabe.*
