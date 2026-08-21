---
name: architecture-building-codes-permits
description: >
  Building codes, byelaws and the plan-approval process for residential
  construction in Pakistan. Covers the two-layer regulatory model (national
  Building Code of Pakistan — BCP 2007 Seismic Provisions and BCP 2021
  IBC-based — versus local development-authority byelaws from LDA, DHA, CDA,
  SBCA, RDA and TMAs), setback/coverage/height/parking tables by authority and
  plot size, CDA space standards, height-datum and projection rules, the full
  map-approval lifecycle with documents, NOCs, fees, timelines, completion
  certificates and deviation/regularisation, structural drawing and PEC/PCATP
  stamping requirements, and disciplined cross-referencing to US
  IBC/IRC/ACI/ASCE numeric defaults where Pakistani documentation is thin.
---

# Building Codes & Permits — Pakistan Residential Construction

Pakistan does not have one building rulebook. It has two bodies of law, issued by two different institutions, that govern two non-overlapping domains — and almost every regulatory error in Pakistani residential work comes from confusing them. The **Building Code of Pakistan** (Pakistan Engineering Council + Ministry of Housing & Works / Ministry of Science & Technology) governs *structure, seismic resistance and life safety*. It says nothing at all about setbacks, plot coverage, height limits or parking. Those are governed 100% by the **byelaws of whichever local development authority owns the scheme the plot sits in** — LDA in Lahore, CDA in Islamabad, SBCA in Karachi, RDA in Rawalpindi, DHA in cantonment-style private schemes, and TMA / Municipal Committee / Cantonment Board everywhere else. Byelaw numbers differ meaningfully by city, and even by *phase* within a single city's DHA. This skill models both layers, keeps them cited separately, walks the approval lifecycle from first drawing to completion certificate, and gives an explicit protocol for the many cases where Pakistani residential detailing is undocumented and a US IRC/ACI value is the closest defensible analog.

## Reality Check - Licensing & Liability

**This skill produces design aids, dimensional envelopes and calculation guidance for planning and FreeCAD modeling ONLY.**

- Nothing produced with this skill — no setback envelope, no coverage calculation, no footing size, no rebar note, no seismic zone factor, no FreeCAD model, no drawing exported from one — is a construction document, a permit document, or an approval.
- Any design intended for the actual construction of a real, occupied building **MUST** be reviewed, sealed and stamped by a **licensed structural engineer registered with the Pakistan Engineering Council (PEC)** — a Professional Engineer holding a valid PEC registration number in the relevant discipline — and the architectural drawings signed by a **PCATP-registered architect** (Pakistan Council of Architects and Town Planners, under the Architects and Town Planners Ordinance 1983).
- The design **MUST** additionally go through the relevant local authority's plan/map approval (LDA / CDA / SBCA / RDA / DHA / TMA / Cantonment Board byelaws) and hold a stamped approved map **before** any construction starts. Building without an approved map exposes the owner to stop-work and demolition notices, compounding/regularisation penalties, and refusal of utility connections (WASA / LESCO-IESCO-KE / SNGPL).
- Claude **must never** present FreeCAD output, byelaw tables, or any calculation from this skill as construction-ready, permit-ready, submission-ready, or "approved" without that human sign-off.
- If a user appears to be treating this output as final — asking to send it to a contractor, to start excavation, to submit it to the authority as-is, asking "how much steel do I buy", or saying "so we're good to build" — **say so unprompted, in that turn, before answering anything else**: *"This is a planning model, not a stamped drawing. A PEC-registered structural engineer has to review and stamp this, and [authority] has to approve the map, before anyone breaks ground."*
- **Never certify.** Do not produce anything resembling a stamped drawing, an engineer's certificate, a structural stability certificate, a completion certificate, or a soil report. Never place an engineer's name, PEC number, PCATP number, or signature block on output.
- **Byelaw numbers change.** Every table here carries a source and a vintage. Before quoting a number to a user as authoritative, state the source and the year, and recommend verification against the authority's current published regulations.
- **Never invent a number to be helpful.** A fabricated setback becomes a demolition notice. "That figure has to come off the authority's published table — here is where to find it" is a correct and complete answer.

---

## Section 0: Fast Path — If You Read Nothing Else

```
1. Is the question STRUCTURAL or PLANNING?
     structural → BCP 2021 Ch.16/Ch.19 → ASCE 7-16 / ACI 318-19; seismic zone from BCP 2007 Table 2.2
     planning   → local byelaw ONLY. BCP is silent. Ask: city / authority / scheme / phase / plot size / land use.
2. Never quote a "Pakistan setback". There is no such thing. Name the authority or ask.
3. Height is measured from ROAD LEVEL / ROAD CROWN, not finished floor level.
4. Any US IRC/ACI/IBC value must be labelled inline as a US reference value (Section 12), and checked
   for scope before quoting — several commonly-cited IRC/ACI clauses are conditional (seismic design
   category, occupancy, span), not universal minimums. Quote the condition, not just the number.
5. A plot that straddles two jurisdictions (Section 4.3) is BLOCKED on a single answer — name both
   authorities and say the stricter governs until confirmed otherwise.
6. Every answer ends with the licensing gate: PCATP architect signs, PEC engineer stamps,
   authority approves the map — before construction.
```

---

## Section 1: The Two-Layer Regulatory Model

The single most important structural fact about Pakistani building regulation:

| | Layer 1 — "The Code" | Layer 2 — "The Byelaws" |
|---|---|---|
| **Name** | Building Code of Pakistan (BCP) | Building & Zoning Regulations / Building Control Regulations / Bylaws |
| **Issued by** | Pakistan Engineering Council (PEC), with Ministry of Housing & Works (2007) / Ministry of Science & Technology (2021) | Local development authority — LDA, CDA, SBCA, RDA, DHA, TMA, MDA, FDA, GDA, Cantonment Board |
| **Scope** | Structural design, seismic, wind, snow, flood, concrete, steel, masonry, fire & life safety, interior environment, materials | Zoning, land use, setbacks, plot coverage, FAR, height limit, storeys, parking, basements, projections, boundary walls, sub-division, plan approval procedure, completion certificates |
| **Geographic reach** | National | City / authority / scheme / phase-specific |
| **Enforced by** | PEC-registered engineer's stamp + the authority's structural vetting cell | The authority's Building Control / Town Planning Directorate at map approval and site inspection |
| **Does it set setbacks?** | **NO** | **YES — exclusively** |
| **Does it set rebar / seismic detailing?** | **YES** | No (defers to the code) |
| **Typical failure mode when confused** | Owner cites "BCP" for a setback and gets a rejection | Owner treats an approved map as proof the structure is safe |

### 1.1 The Routing Rule

```
Question arrives
  ├─ Is it about STRUCTURE (loads, seismic, footing, rebar, slab, column,
  │  wall thickness for strength, foundation depth)?
  │     → BCP 2021 (Ch.16 Structural Design, Ch.19 Concrete) → ASCE 7-16 / ACI 318-19 by reference
  │     → BCP 2007 Seismic Provisions for zone / PGA
  │     → if still silent: US IRC 2021 / ACI 318-19 as a FLAGGED reference value (Section 12)
  │
  ├─ Is it about PLANNING (setback, coverage, FAR, height, storeys, parking,
  │  basement, projection, room size, boundary wall, land use)?
  │     → ASK FIRST: "Which city, which authority, which scheme, which phase?"
  │     → then the specific byelaw table (Sections 4–7)
  │     → NEVER quote a generic "Pakistan setback" — there is no such thing
  │
  ├─ Is it about APPROVAL (documents, NOCs, fees, timeline, who stamps,
  │  completion certificate, deviations)?
  │     → Sections 8–11
  │
  └─ Is it about LIFE SAFETY DIMENSIONS (stair width, riser/tread, headroom,
     door width, window area for light/ventilation, party-wall fire rating)?
        → BOTH layers apply. The byelaw planning minimum (e.g. CDA stair 3'-3")
          and the code egress/fire-separation minimum (BCP 2021 Ch.10, Ch.7,
          paralleling IBC 2021) are separate tests. Satisfy the stricter of the
          two, and say which governed.
```

### 1.2 Mandatory First Question

Before quoting any planning number, establish all six:

1. **City** — Lahore / Islamabad / Karachi / Rawalpindi / other
2. **Authority** — LDA, DHA, CDA, SBCA, RDA, TMA, Cantonment Board, or a private housing society approved by one of them
3. **Scheme & phase** — DHA Lahore Phase 3 ≠ Phase 6; a CDA sector ≠ a CDA-approved private society
4. **Plot size in marla/kanal AND in feet** — the marla is not a fixed unit (Section 17)
5. **Land use category** — single-family residential / apartment / medium-rise / commercial / mixed-use
6. **Abutting road width and plot condition** — corner, two-road frontage, park-facing, on a widening reservation (Section 5.8), or straddling two jurisdictions (Section 4.3)

If any is unknown, say explicitly *which numbers are blocked on it* rather than picking a plausible default.

---

## Section 2: Building Code of Pakistan 2007 — Seismic Provisions

BCP 2007 is a **narrow document**: it is the *Seismic Provisions* volume, not a full building code. It exists because of the October 2005 Kashmir earthquake. It gives Pakistan its seismic hazard map, zone factors and seismic design requirements — and essentially nothing else.

**Source:** `https://urbanunit.gov.pk/Download/publications/Files/8/2021/Pakistan%20Building%20Code%202007.pdf`

### 2.1 Seismic Zones and Peak Ground Acceleration

| Zone | PGA range (g) | Hazard descriptor | Design consequence for houses |
|---|---|---|---|
| Zone 1 | 0.05 – 0.08 | Low | Minimal seismic detailing; wind often governs lateral design |
| Zone 2A | 0.08 – 0.16 | Moderate | Ordinary detailing acceptable for low-rise RC; simple box-plan masonry viable |
| Zone 2B | 0.16 – 0.24 | Moderate–high | Intermediate detailing; **confined** masonry strongly preferred over unreinforced |
| Zone 3 | 0.24 – 0.32 | High | Special/intermediate detailing; unreinforced masonry effectively ruled out |
| Zone 4 | > 0.32 | Very high | Special moment-resisting frames / special shear walls; full ductile detailing |

**Design basis:** 10% probability of exceedance in 50 years ≈ 475–500 year return period (BCP 2007, consistent with the UBC-97 / IBC framing the document was built on).

**Zone assignment is by TEHSIL, listed in BCP 2007 Table 2.2.** Do not interpolate from a map image, and do not assume a district-wide zone.

### 2.2 Commonly-cited zone assignments — VERIFY against Table 2.2 before use

These are the values most frequently repeated in Pakistani practice. Treat them as a starting hypothesis to confirm, never as a citation:

| City | Commonly cited zone | Verify against |
|---|---|---|
| Lahore | 2A | Table 2.2, Lahore tehsil |
| Faisalabad / Multan / Bahawalpur | 2A | Table 2.2 |
| Islamabad / Rawalpindi | 2B | Table 2.2 |
| Karachi | 2B | Table 2.2 |
| Peshawar | 2B | Table 2.2 |
| Abbottabad / Murree / Mansehra | 3 | Table 2.2 |
| Quetta | 4 | Table 2.2 |
| Muzaffarabad / Balakot | 4 | Table 2.2 |
| Gilgit / Chitral | 3–4 | Table 2.2 — genuinely varies by tehsil |

> **Honesty rule:** if asked "what seismic zone is X in?" and X is not on this list, say the zone must be read off BCP 2007 Table 2.2 by tehsil name, and offer to look it up rather than guessing from a neighbouring city. Getting a zone wrong by one band changes the base shear by roughly a factor of two.

### 2.3 What BCP 2007 does NOT contain

No setbacks. No coverage. No height limits. No parking. No room sizes. No plan-approval process. No comprehensive concrete, steel or masonry design chapters. **If someone cites "BCP 2007" for any of those, they are wrong — the number they mean is a local byelaw.**

---

## Section 3: Building Code of Pakistan 2021 — The IBC-Based Full Code

BCP 2021 is the real change. Developed **jointly by PEC and the International Code Council (ICC)**, it is built on the **IBC 2021** framework, reviewed by ICC and approved by PEC's governing body — the final draft on record is dated **26 October 2021**, and the PEC think-tank references a **2 February** approval milestone; **the exact year of that specific approval step is not independently confirmed here — verify the precise adoption date directly with PEC before citing it as a fixed fact.** The draft was routed through the Ministry of Science & Technology. It supersedes/supplements BCP 2007 by wrapping the seismic provisions inside a complete code.

**Sources:**
- `https://codes.iccsafe.org/content/PKBC2021P1/preface`
- `https://www.pec.org.pk/wp-content/uploads/2024/09/BCP2021-Final-Draft-dated-26.10.2021.pdf`
- `https://www.pec.org.pk/thinktank/building-code-of-pakistan-thinktank/`

### 3.1 What BCP 2021 adopts by reference

| Referenced standard | Used for |
|---|---|
| **ASCE 7-16** | Load combinations (LRFD & ASD), dead/live/wind/seismic/snow/rain load derivation, seismic design categories, drift limits |
| **ACI 318-19** | Reinforced concrete design — flexure, shear, development length, cover, detailing, seismic detailing (Ch.18) |
| **IBC 2021** | Overall code architecture, chapter numbering, occupancy classification, fire and life-safety framework, interior environment |

### 3.2 Pakistan-specific modifications layered on top of IBC 2021

1. **Updated PSHA** (probabilistic seismic hazard analysis) — Pakistan-specific ground-motion parameters replacing US hazard maps
2. **Pakistan wind-speed map** — basic wind speeds by region replacing ASCE 7 US wind maps
3. **Snow and rain load** provisions for the northern regions (Murree, Galiyat, Gilgit-Baltistan, Azad Kashmir, Swat)
4. **Flood-resistant construction** — a direct response to Pakistan's recurring riverine and flash-flood exposure
5. Local material and construction-practice allowances (brick masonry dominance, local concrete practice)

### 3.3 Chapter map (mirrors IBC 2021 numbering)

| Chapter | Subject | Residential relevance |
|---|---|---|
| Ch. 1–2 | Administration, definitions | Permit framework, terminology |
| Ch. 3 | Occupancy classification | Single-family = Group R-3 analog; apartments = R-2 (**sourcing caveat below**) |
| Ch. 4–5 | Special detailed requirements; general heights & areas | Rarely governs single houses |
| Ch. 6 | Types of construction | Combustibility / fire-resistance construction type |
| Ch. 7 | Fire and smoke protection features | Party-wall and separation ratings (row houses, semi-detached — Section 3.5) |
| Ch. 9 | Fire protection systems | Sprinkler thresholds (rarely triggered by houses; relevant for apartments) |
| **Ch. 10** | **Means of egress** | **Stair width, riser/tread, headroom, door swing, exit count** |
| Ch. 11 | Accessibility | Rarely mandatory for private houses; use for aging-in-place design |
| **Ch. 12** | **Interior environment** | **Natural light and ventilation glazing areas, minimum room dimensions/ceiling heights** |
| Ch. 15 | Roof assemblies | Roof covering, drainage, parapet |
| **Ch. 16** | **Structural Design** | **Loads, load combinations, seismic, wind, snow — the core residential structural chapter** |
| Ch. 17 | Special inspections & tests | Concrete cube/cylinder testing regime |
| Ch. 18 | Soils and foundations | Bearing capacity, footing depth, soil investigation trigger |
| **Ch. 19** | **Concrete** | **RC design via ACI 318-19; cover, detailing, mixes** |
| Ch. 21 | Masonry | Brick/block walls — the dominant residential material in Pakistan |
| Ch. 22 | Steel | Steel framing, cold-formed sections |
| Ch. 23 | Wood | Rarely used structurally in Pakistani houses |
| Ch. 24 | Glass and glazing | Safety glazing at doors, low sills, stair-adjacent panels |
| Ch. 33 | Safeguards during construction | Site protection, excavation adjacent to neighbours |
| Ch. 35 | Referenced standards | The formal list that binds ASCE 7-16 and ACI 318-19 into the code |

**Occupancy classification sourcing caveat:** the Group R-3 / R-2 mapping in the Ch.3 row above is **Claude's analogy from the IBC 2021 framework BCP 2021 is built on** — no Pakistani authority document has been located here that confirms LDA/CDA/SBCA/DHA vetting cells actually apply the IBC Group-letter classification scheme in practice, as opposed to their own plain-language "residential/commercial/mixed-use" land-use categories from the zoning schedule. Use the R-3/R-2 mapping as an internal reasoning aid for which chapter provisions should apply by analogy (fire separation, occupant load), **never** as a term to put in front of a vetting cell as if it were the authority's own classification.

**Citation form to use:** *"BCP 2021 Ch. 16 (Structural Design), which parallels IBC 2021 Ch. 16 and adopts ASCE 7-16 load combinations"* — always name both the BCP chapter and the referenced standard, so an engineer can trace it.

### 3.4 Adoption status caveat — what "uneven enforcement" actually means

BCP 2021 exists and is published, but **enforcement is uneven, and the unevenness is load-bearing for the approval process, not a footnote**:

- **What is documented:** BCP 2021 is a completed, published draft (26 October 2021) developed jointly with ICC and endorsed by PEC. It has not been shown here to have a single, uniform, province-wide statutory notification date that supersedes BCP 2007 everywhere at once — Pakistani building regulation is federated across provinces and authorities, and each authority's own building-control rules (not BCP itself) are what a vetting cell is legally bound to check against until that authority formally references BCP 2021.
- **What that means in practice for a submission:** the authority's structural vetting cell may still be reviewing against **BCP 2007 plus established local practice** for seismic/structural sign-off, even where BCP 2021 is the technically superior and more complete basis. Do not assume BCP 2021 is what a specific authority will actually check the drawings against.
- **What to actually do:** (1) design the structure to **BCP 2021 / ACI 318-19 / ASCE 7-16** — the stricter, more complete basis, so the design is defensible regardless of which document the vetting cell uses; (2) **at submission time, ask the authority's structural vetting cell directly which code edition and standard set they currently check against**, and cite the design-basis note (Section 11.3) in the terms that cell recognises; (3) never tell a user "BCP 2021 is mandatory in your city" without that direct confirmation — say instead "BCP 2021 is the technically current national code; whether [authority]'s vetting cell has formally adopted it yet needs to be confirmed with them at submission, and the design should be sound under either edition."

---

## Section 3.5: Fire Separation and Party Walls — Semi-Detached & Row Houses

Semi-detached ("portion") houses and row/terrace houses sharing a common wall are extremely common in Pakistani schemes — most DHA and LDA-society "5 marla" and "10 marla" product is built as attached pairs or short terraces, not free-standing villas. **Pakistani byelaws are silent on fire-separation ratings for these shared walls** — none of the authority documents cited in Section 19.1 specify a numeric fire-resistance rating or a physical-separation distance for a common party wall between two dwelling units. This is a genuine documentation gap, not an oversight in this skill.

Because BCP 2021 Ch.7 (Fire and smoke protection features) is built on IBC 2021, the closest defensible analog — **flagged exactly per the Section 12 protocol** — is:

| Item | US reference value | Source | Status |
|---|---|---|---|
| Fire-resistance rating, common/party wall between two single-family (R-3-analog) dwelling units | **1-hour fire-resistance rated**, tested wall assembly, no openings permitted in the wall | IBC 2021 Table 302.1(2) / IRC 2021 §R302.2 | **US reference value — Pakistani byelaws are silent on this. Flag explicitly; do not present as a Pakistani requirement.** |
| Continuity of the rated wall | Party wall extends full height, roof deck to foundation, with no penetrations for ducts/pipes that break the rating | IRC 2021 §R302.2 | Same status |
| Structural independence | Each unit's structure should be capable of being demolished independently without collapsing the neighbour's structure (a structural, not just fire, requirement) | Sound structural practice; ACI 318-19 does not state this as a residential party-wall rule directly | Engineering judgement — verify with the PEC-registered engineer of record |

**Practical guidance pending authority clarification:** where a Pakistani residential drawing shows a shared masonry party wall (commonly 9 in / 230 mm solid brick between units), that thickness is driven by the structural/acoustic norm of local practice, not a fire-rating calculation — say so plainly if asked "does this wall meet fire code", because the honest answer is that no Pakistani fire-rating figure exists to check it against, and the US 1-hour analog is offered only as an engineering reference point, subject to the PEC engineer's judgement. Never state a Pakistani semi-detached/row house design "meets fire code" for the party wall — say instead that no Pakistani numeric standard was found, offer the flagged US analog, and recommend the engineer of record confirm treatment with the authority's vetting cell.

---

## Section 4: Local Development Authority Byelaws — Institutional Map

### 4.1 Who writes which byelaws

| Authority | City / jurisdiction | Governing document | Source |
|---|---|---|---|
| **LDA** — Lahore Development Authority | Lahore + LDA-approved private societies | LDA Building & Zoning Regulations 2019 (amended to 2021) | `lda.gop.pk` |
| **DHA Lahore** | DHA Lahore Phases 1–13 | Revised DHA Bylaws (phase-differentiated) | DHA Lahore; DHA Karachi analog at `dhakarachi.org` |
| **CDA** — Capital Development Authority | Islamabad sectors | Islamabad Residential Sector Building Control Regulations; Schedules 1–5 | `cda.gov.pk/lawsAndRegulations` |
| **SBCA** — Sindh Building Control Authority | Karachi and Sindh | Karachi Building & Town Planning Regulations 2002, amended 2005 & 2017 | `sbca.gos.pk` |
| **RDA** — Rawalpindi Development Authority | Rawalpindi | RDA Building Regulations | `cbrechs.org.pk/documents/RDA_Building_Regulations.pdf` |
| **TMA / Municipal Committee** | Smaller cities & tehsils | Local building byelaws, usually adapted from the provincial authority | Varies — frequently not published online |
| **Cantonment Board** | Cantonment areas (Lahore, Rawalpindi, Karachi, Multan, etc.) | Cantonment Board building byelaws | Board-specific |
| **MDA / FDA / GDA / PDA** | Multan / Faisalabad / Gujranwala / Peshawar | Authority-specific building regulations | Authority website |

### 4.2 Which authority governs this plot — decision tree

```
Where is the plot?
├─ Inside a DHA phase ................................. DHA byelaws (phase-specific). DHA is NOT LDA.
├─ Inside a Cantonment Board area ..................... Cantonment Board byelaws
├─ Inside an Islamabad CDA sector ..................... CDA Building Control Regulations
├─ Inside a private society in Islamabad .............. CDA-approved society: CDA regs + society covenant
├─ Inside Lahore municipal limits ..................... LDA Building & Zoning Regulations 2019
├─ Inside an LDA-approved private society ............. LDA regs + the society's approved layout plan
│                                                        (setbacks often come off the LAYOUT PLAN, not a table)
├─ Karachi / Sindh urban ............................. SBCA (Karachi Building & Town Planning Regs)
├─ Rawalpindi (non-cantonment) ....................... RDA Building Regulations
├─ Small town / tehsil ............................... TMA byelaws — usually offline; the user must
│                                                        physically collect them from the TMA office
└─ Straddles two of the above, OR the boundary itself is ambiguous ...... STOP. See Section 4.3.
                                                        Do NOT default to whichever authority is more
                                                        familiar or more convenient to answer for.
```

**Key trap:** a "DHA" plot and an "LDA-approved society" plot in the same city follow different tables. A private society *approved by* LDA follows LDA regulations **plus** any society-specific covenant, and its setbacks are often fixed on the society's approved layout plan rather than a published byelaw table. Ask which — and if it's a society, ask for the approved layout/zoning plan.

### 4.3 Plots that straddle two jurisdictions or whose jurisdiction has changed

This is a real and recurring situation that a clean single-authority answer cannot cover, and this skill does not have a general resolution rule for it — only a protocol for how to handle it honestly:

| Scenario | Why it's genuinely ambiguous | What to do |
|---|---|---|
| A plot fronting a road that is the boundary between a DHA phase and an adjoining Cantonment Board area | The two authorities can have materially different setback/height/coverage tables, and the road itself may be under a third jurisdiction (the cantonment, typically) for its width and any encroachment rules | Do not average or pick the more permissive table. State both authorities' figures side by side, flag that the frontage road's own jurisdiction may separately control what can be built facing it (projections, boundary wall, gate), and say the plot needs a jurisdiction determination letter from both authorities — usually obtained by writing to each Town Planning wing — before a byelaw table can be relied on |
| An LDA-approved private society later absorbed into Lahore's expanded municipal limits | The society's original approved layout plan and covenant may pre-date the current LDA regulations; LDA's own 2019/2021 amendments may or may not be stated to apply retroactively to pre-existing approved societies | Treat the ORIGINAL approved layout plan as controlling for setbacks/building line unless the society or LDA has issued a specific notification updating it; flag this explicitly as something to confirm with LDA's Town Planning wing, not something to assume either way |
| A plot where the surrounding scheme's authority is disputed or under litigation (common with some peripheral housing schemes) | Byelaw applicability is genuinely undetermined until the dispute resolves | Say plainly that no byelaw table can be quoted with confidence until the jurisdiction question is settled, and that proceeding to design against either authority's table carries the risk of being wrong if the dispute resolves the other way |

**The one hard rule that does generalise:** never silently pick one authority's table when two plausibly apply. Name both, say why it's ambiguous, and push the resolution back to the authorities themselves (a written jurisdiction query) rather than resolving it by assumption.

---

## Section 5: Setbacks, Coverage, Height — Numeric Tables by Authority

### 5.1 DHA Lahore — Setback table by plot size

Source: DHA Lahore construction bylaws (`zameen.com/blog/construction-bylaws-dha-lahore.html`, reflecting the Revised DHA Bylaws).

| Plot size | Typical dims | Front setback | Rear setback | Side setback(s) |
|---|---|---|---|---|
| 5 marla | 25' × 45' | 5'-0" | 3'-0" | 3'-0" |
| 7 marla | — | 7'-0" | 3'-0" | 3'-0" |
| 8 marla | — | 8'-0" | 4'-0" | 4'-0" |
| 10 marla | 35' × 65' | 10'-9" | 5'-4½" | 5'-4½" |
| 1 kanal | 50' × 90' | 15'-9" | 5'-4½" | 5'-4½" (both sides) |
| 2 kanal | 100' × 90' | 15'-9" | 8'-4½" | 5'-4½" |
| 2 kanal | 75' × 120' | 20'-9" | 8'-4½" | 5'-4½" |

The half-inch dimensions (5'-4½", 8'-4½", 10'-9", 15'-9", 20'-9") are not typos — they are the actual published values and should be modelled exactly, not rounded. Rounding 5'-4½" down to 5'-0" is a setback encroachment.

**10-marla area flag:** 35' × 65' = **2,275 sq ft**, which is 25 sq ft (about 1.1%) more than the nominal 10 marla × 225 sq ft/marla = **2,250 sq ft** used as the round figure elsewhere in this skill (e.g. the RDA worked example at §5.4). Both figures are legitimately in use — 35' × 65' is the commonly-published scheme dimension, 2,250 sq ft is the clean nominal-area figure — but they do not reconcile exactly, and this skill does not resolve that by rounding one to match the other. **Always use the actual dimensioned plot size from the site plan / title documents for a real coverage or FAR calculation, and treat the nominal marla-area figure as an order-of-magnitude planning number only.**

### 5.2 DHA Lahore — Heights, coverage and element limits

| Item | Limit |
|---|---|
| Max building height, Phases 1–4 | 30'-0" measured from road level |
| Max building height, Phases 5 and above | 35'-0" measured from road level |
| Living-room ceiling height | 9'-6" to 12'-0" |
| Basement ceiling height | 9'-0" to 10'-0" |
| Basement storeys | Single-storey basement only; **no basement beneath a car porch** |
| Car porch height | Min 9'-0", not exceeding ground-floor height |
| Car porch depth | Min 12'-0" (excluding 2'-0" projection), max 18'-0" |
| Boundary wall | Max 7'-0" |
| Swimming pool | Permitted on 1 kanal and above only |
| First-floor coverage, 5 marla | May equal 100% of the ground-floor permissible covered area |
| First-floor coverage, 10 marla / 1 kanal / 2 kanal | Limited to 75% of ground-floor covered area |

> **Phase check is mandatory.** A 30' vs 35' limit is the difference between a legal and an illegal second floor. Always ask the phase number before quoting a DHA height.

### 5.3 LDA Lahore — 2019 Regulations (as amended)

Source: `lda.gop.pk` Amended Building Regulations 2019 (amendments approved to 28-01-2020) and the 22-06-2021 draft final.

| Plot / building category | Max height | Storeys |
|---|---|---|
| Plots ≤ 10 marla and < 1 kanal | 48'-0" | Ground + 3 |
| Plots ≥ 1 kanal and < 2 kanal | 90'-0" | Ground + 6 |
| Apartment Medium-Rise-I on a 30'-wide road | 90'-0" | — |
| Apartment Medium-Rise-II on a 30'-wide road | 160'-0" | — |

**Medium-rise setback consent rule:** Medium-Rise-I/II apartment buildings on a 30'-wide road require a **5'-0" setback per abutting plot owner** — the setback obligation scales with the number of adjoining plots.

**LDA parking rules (2019 amendments):**
- Parking provision is **optional for plots under 10 marla**
- Parking is **NOT permitted within mandatory setback areas** — those must be pedestrian walkway or green/soft landscape
- Design consequence: on a 10-marla-plus plot you cannot count the front setback as your parking bay. The porch must sit **inside** the buildable envelope (consuming covered area) or in a permitted projection.

> **Do not design a single-family house to the LDA maximum just because it is allowed.** A 1-kanal plot permitting 90 ft / G+6 does not mean a house should be six storeys. For a house, coverage, setbacks, budget and structure govern long before the height cap does.

### 5.4 RDA Rawalpindi

| Item | Value |
|---|---|
| Maximum ground coverage | 65% of plot area |
| FAR (floor area ratio) | Up to 1 : 1.4 for buildings up to 38'-0" (11.58 m) height |

Source: `cbrechs.org.pk/documents/RDA_Building_Regulations.pdf`

**Worked FAR check (RDA, 10 marla — illustrative nominal area, NOT a specific dimensioned plot):**
```
Nominal area used here = 10 × 225 sq ft/marla = 2,250 sq ft — a round planning figure.
(NOTE: an actual 35'×65' plot as tabulated for DHA in §5.1 is 2,275 sq ft, about 1.1%
 larger. This worked example uses the clean 2,250 sq ft nominal figure to keep the
 arithmetic legible; for a real plot, substitute its ACTUAL surveyed dimensions —
 the 1% difference moves every number below by the same 1%, which will matter at
 the margin of a compliance check but not to the illustrative method.)

Ground coverage cap  = 0.65 × 2,250 = 1,462 sq ft footprint maximum
FAR cap              = 1.4  × 2,250 = 3,150 sq ft TOTAL floor area, all storeys
At 1,462 sq ft/floor → 3,150 / 1,462 = 2.15 floors' worth of area
→ G+1 full-footprint (2,924 sq ft) fits with 226 sq ft spare;
  a full G+2 (4,386 sq ft) does NOT. The FAR binds before the height limit.
```
This is the standard trap: coverage and FAR are two independent tests, and FAR is the one people forget. It is compounded by the fact that "10 marla" itself is not one exact area until you know the actual scheme dimensions — always substitute the real surveyed plot size for a genuine compliance check, never the nominal marla-area figure.

### 5.5 SBCA Karachi

Karachi height limits are **tiered by plot area and total floor area**, not a flat citywide cap.

| Condition | Max height |
|---|---|
| Plots up to 120 sq yd | 33'-0" (10 m) |
| Where total floor area reaches 20,000 sq ft | 50'-0" (15.2 m) |

Regulation vintages to cite precisely: **Karachi Building & Town Planning Regulations 2002**, amended **4 Aug 2005** (`R-AM-4-Aug-2005`) and **28 Aug 2017** (`R-AM-28-Aug-2017`), both at `sbca.gos.pk/pdf/`. Always cite which amendment you are quoting from — the 2002 base text alone is out of date.

### 5.6 Generic "5 marla" figures found in circulation — and why they conflict

A widely-repeated generic 5-marla byelaw set:

| Item | Generic figure |
|---|---|
| Plot dimensions | 25' × 45' |
| Front setback | 5'-0" |
| Rear setback | 5'-0" |
| Side setback | None mandatory |
| Ground floor coverage | 75% |
| First floor coverage | 75% |
| Max height from road crown | 38'-0" |
| Boundary wall | 7'-0" |

**This conflicts with the DHA Lahore 5-marla row above** (DHA: rear 3'-0", sides 3'-0", height 30–35'). Both are "real" — they belong to different authorities.

> **Rule derived from this conflict: never quote a Pakistani setback or height number without naming the authority and scheme it came from.** If the user has not told you, ask. If they will not specify, present two or three authority-specific rows **side by side and labelled**, rather than collapsing them into one fake national figure.

### 5.7 Height datum and what counts toward the cap

| Question | Answer / discipline |
|---|---|
| Measured from where? | **Road level / road crown** at the plot frontage — not from finished floor level, not from natural ground level |
| Does plinth height count? | **Yes** — plinth above road level consumes the cap. A 2'-6" plinth on a 35' cap leaves 32'-6" of building |
| Does the parapet count? | Usually yes to some extent — **verify per authority**; some exclude a parapet up to a stated height |
| Does the stair mumty / stair tower count? | **Commonly excluded or partially excluded — VERIFY.** This is one of the most authority-specific and most abused exclusions |
| Overhead water tank, lift machine room, solar frame? | Commonly treated as permitted rooftop appurtenances within limits — **verify**; never assume free height |
| Sloped site — which point? | Authority-specific (crown of abutting road, mean level, or lowest point). **Ask; do not average silently** |

**Modelling rule:** in FreeCAD, place a named datum `ROAD_LEVEL` at z = 0 and dimension the compliance height from it. Never dimension the height cap off the ground-floor finished level.

### 5.8 Special plot conditions that change the numbers

| Condition | Typical effect | Status |
|---|---|---|
| **Corner plot** | Often an additional setback on the second road frontage; sometimes a splayed/chamfered corner for sight lines | Common practice — **verify per authority** |
| **Two-road frontage (through plot)** | Both frontages may be treated as "front", giving two front setbacks | Verify |
| **Plot abutting a park / green belt** | Rear or side setback may be reduced or increased; projections onto the green belt normally prohibited | Verify |
| **Plot on a road-widening reservation** | The **building line** sits behind the plot boundary; the reserved strip is unbuildable even though you own it | Verify against the approved layout plan |
| **Narrow abutting road** | Height and projection limits scale with road width (CDA projections tie to ≤20 ft streets; LDA medium-rise tiers tie to 30 ft roads) | Cited for CDA/LDA; verify elsewhere |
| **Amalgamated plots** | Setbacks apply to the amalgamated boundary, but amalgamation itself needs authority approval first | Verify |
| **Sub-divided plot** | Sub-division usually requires separate approval and may change the applicable plot-size row | Verify |
| **Plot straddling two jurisdictions** | No single byelaw table applies cleanly | See Section 4.3 — do not resolve by assumption |

**Terminology note:** *setback* is a distance measured from the plot boundary; *building line* is a line fixed on the approved layout plan, often set back further than the byelaw setback where road widening is reserved. **Where both exist, the building line governs.**

---

## Section 6: Space Standards, Light and Ventilation

### 6.1 CDA Islamabad Schedule-2 — the usable Pakistani baseline

CDA is the only major Pakistani authority publishing an explicit minimum-space schedule usable as a residential design constraint set. Use it as the Pakistani baseline for room sizing even outside Islamabad — **flagged as CDA-derived**, not as a national rule.

Source: CDA Islamabad Residential Building Control Regulations, Schedule-2 (via `primarcstudio.com` byelaw digest and `cda.gov.pk/lawsAndRegulations`).

| Element | Minimum | Relaxation permitted |
|---|---|---|
| Living unit (dwelling), excluding stairs | 600 sq ft | 10% |
| Habitable room | 100 sq ft | 10% |
| Kitchen | 45 sq ft | 10% |
| Bathroom / toilet | 24 sq ft | 10% |
| Door height | 7'-0" standard | Relaxable to 6'-6" without penalty |
| Stair flight width | 3'-3" standard | Relaxable to 2'-9" |

### 6.2 CDA projection rules (Schedules 1–5)

| Projection type | Limit |
|---|---|
| Roof projection over streets ≤ 20'-0" wide | Max 1'-6" |
| Ground / first floor projection into setback | Max 3'-0" |

### 6.3 Applying the 10% relaxation correctly

The relaxation is a *tolerance the authority may accept at its discretion*, not a design target.

```
Habitable bedroom, 100 sq ft minimum
  Proposed: 9'-6" × 10'-0" = 95 sq ft
  Shortfall: 5 sq ft = 5.0% → inside the 10% band → likely acceptable, but discretionary
  Better:    10'-0" × 10'-6" = 105 sq ft → no relaxation needed, no reviewer discretion involved

DESIGN DECISION: take the 105 sq ft. Relaxations are a rescue for a plan that is
otherwise good and lands 3–8% short on one dimension. Do not spend them on rooms
you can simply size correctly, and never spend two of them in the same submission.
```

### 6.4 Light and ventilation — code layer, flagged

Pakistani residential byelaws are thin on glazing area. BCP 2021 Ch. 12 (Interior Environment) parallels IBC 2021 Ch. 12, which gives:

| Requirement | Value | Status |
|---|---|---|
| Natural light — glazed area per habitable room | ≥ **8%** of the room's floor area | **IBC 2021 Ch.12 reference value**, mirrored by BCP 2021 Ch.12 — confirm the BCP text |
| Natural ventilation — openable area per habitable room | ≥ **4%** of the room's floor area | Same status |
| Alternative | Mechanical ventilation / artificial light where the above cannot be met | Same status |

Worked check: a 12' × 12' bedroom = 144 sq ft → glazing ≥ 11.5 sq ft (e.g. a 4'-0" × 3'-0" window = 12 sq ft ✓), openable ≥ 5.8 sq ft. In Pakistani practice a 5' × 4' window (20 sq ft) is the norm and clears both comfortably — the constraint bites only on internal bathrooms, box rooms and courtyard-facing kitchens.

### 6.5 Egress dimensions — code layer, flagged, vs byelaw stair width

| Item | IBC 2021 Ch.10 / IRC 2021 residential value | Status vs the Pakistani planning rule |
|---|---|---|
| Stair width (residential) | ≥ 36 in (3'-0") | **CDA's 3'-3" planning minimum is STRICTER — CDA governs in Islamabad** |
| Max riser | 7¾ in (≈197 mm) | US reference; use as the design ceiling — Pakistani site practice often builds 7"–7½" |
| Min tread (run) | 10 in (254 mm) | US reference |
| Headroom over stairs | ≥ 6'-8" (2.03 m) | US reference; the number most often violated by a mumty landing |
| Handrail height | 34–38 in | US reference |
| Guard height (residential) | ≥ 36 in | US reference; Pakistani balcony practice commonly 3'-0"–3'-6" |

**Resolution rule:** where a byelaw planning minimum and a code egress minimum both exist, satisfy the stricter and **state which governed**. In Islamabad the stair is 3'-3" because CDA says so, not because IBC says 36 in.

---

## Section 7: Parking, Basements, Boundary Walls, Projections

### 7.1 Parking

| Authority | Rule |
|---|---|
| LDA | Optional for plots < 10 marla; **prohibited inside mandatory setbacks** (setback must be pedestrian walkway / green space) |
| DHA Lahore | Car porch min depth 12'-0" (excluding a 2'-0" projection), max 18'-0"; porch height min 9'-0" and ≤ ground-floor height |
| CDA | Parking to be provided within the plot for sector houses; projections into setback capped at 3'-0" |
| SBCA | Parking requirement scales with the floor-area tier |

**Design implication:** model the car porch as a *distinct volume* with its own height parameter, because DHA caps porch height independently of building height and forbids a basement under it. A single lumped "ground floor" solid hides both violations.

**Practical sizing (not a byelaw — design guidance):** one car bay 8'-6" × 18'-0" clear; two side-by-side 17'-0" × 18'-0" clear. A DHA porch at the 12'-0" minimum depth will not park a Corolla-length car plus a 2'-0" walk-around — use 16'-0"–18'-0" where the coverage budget allows.

### 7.2 Basements

| Rule | Authority |
|---|---|
| Single-storey basement only | DHA Lahore |
| No basement beneath a car porch | DHA Lahore |
| Basement ceiling height 9'-0" to 10'-0" | DHA Lahore |
| Basement typically excluded from FAR if used for parking/services | Common across authorities — **verify per authority; this is the single most abused exclusion** |
| Basement extent beyond the building footprint | Frequently restricted or prohibited under setbacks — **verify before modelling a full-plot basement** |
| Soil investigation | Effectively mandatory wherever a basement is proposed (and always for DHA) |

### 7.3 Boundary walls

| Authority | Max height |
|---|---|
| DHA Lahore | 7'-0" |
| Generic 5-marla byelaw set | 7'-0" |

7'-0" is the de facto Pakistani residential norm. Grills, railings and hedges above the solid wall are often treated separately — **verify locally before modelling a 9'-0" compound wall.** Gate piers and a gate leaf above wall height are also authority-specific.

### 7.4 Projection decision tree

```
Is the projection over a PUBLIC STREET?
  ├─ YES → street width ≤ 20 ft?  → max 1'-6" (CDA)
  │                                → wider street: check the authority's schedule
  └─ NO (into your own setback)
        ├─ Ground or first floor ....... max 3'-0" (CDA)
        ├─ Car porch (DHA) ............. 2'-0" projection allowed in addition to the 12–18 ft depth
        ├─ Above first floor ........... generally not permitted into setback; verify
        └─ Sunshade / chajja over a window
                                         usually permitted as a minor projection; verify the depth cap
```

**Never let a projection be the thing that makes a plan work.** If the design only fits because a balcony cantilevers 3'-0" into the setback, it is one reviewer's opinion away from rejection.

---

## Section 8: Map / Plan Approval Process

### 8.1 Documents required (LDA / DHA typical set)

1. **Architectural drawings** signed by a **PCATP-registered architect** — site plan, floor plans, elevations, sections, key/location plan
2. **Structural drawings** — mandatory for commercial and large projects; increasingly required for residential above a size/storey threshold; **always** required where a basement or 3+ storeys is proposed
3. **Owner CNIC copies** (all owners; plus power-of-attorney documents where applicable)
4. **Proof of ownership** — allotment/transfer letter, registry, or DHA membership documents
5. **NOC from relevant departments** — WASA, environment, and any scheme-level NOC (Section 10)
6. **Undertaking / affidavit** on stamp paper attesting byelaw compliance
7. **Soil investigation report** — **mandatory for DHA**; recommended everywhere; effectively required where a basement is proposed
8. **Fee challans** — paid through the designated bank (Bank of Punjab for LDA), receipts attached
9. **Demarcation certificate / site plan** from the authority where the scheme requires it before drawings

### 8.2 Submission workflow

**LDA / DHA (online portal route):**
```
1. Register on the authority portal (CNIC + mobile OTP)
2. Upload the scanned document set (drawings as PDF, usually to a page-size/DPI spec)
3. Pay fee challans (Bank of Punjab for LDA) → upload paid challan scans
4. Scrutiny: town-planning check (setbacks / coverage / height) — the most common rejection stage
5. Structural vetting (where structural drawings are required)
6. Query / objection cycle → resubmit corrected drawings
7. Approval issued → stamped/approved map downloadable or collected
Typical timeline: 3–6 weeks, assuming a clean first submission.
A single objection cycle typically adds 1–3 weeks.
```

**CDA Islamabad (One Window Operation route):**
```
1. Document preparation (drawings, CNICs, ownership, NOCs)
2. OWO (One Window Operation) counter submission
3. Technical review — building control + town planning
4. Environmental compliance verification
5. Approval / objection letter
```

### 8.3 Indicative fee envelope

**5 marla house, Lahore (LDA/DHA) — approximately PKR 60,000 – 120,000 all-in**, comprising:

| Component | Notes |
|---|---|
| LDA scrutiny fee | Scales with covered area |
| Structural vetting fee | Where structural drawings are required |
| WASA charges | Water/sewerage connection and infrastructure |
| FBR tax | Applicable withholding/advance tax at approval |
| Architect fees | Drawing preparation + submission handling |

Payment via **Bank of Punjab challans** for LDA. Fees are revised periodically — quote this as a **dated, order-of-magnitude planning figure, never a quotation**. Larger plots, basements and commercial use move the total substantially.

### 8.4 Common rejection reasons (design for these upfront)

| Rejection cause | Prevention |
|---|---|
| Setback encroached by porch, stair, projection or boundary-wall return | Model setbacks as hard solids in FreeCAD and boolean-check (Section 14) |
| Coverage exceeds the permitted % | Compute covered area per floor explicitly; **ask which elements count** before computing |
| Height exceeds the phase limit | Measure from **road level / road crown**, not finished floor level; include plinth |
| First-floor area exceeds the ground-floor-linked cap | DHA: 75% for 10 marla+, 100% for 5 marla |
| FAR exceeded even though coverage passes | Run coverage and FAR as two separate tests (RDA worked example, §5.4) |
| Basement under the car porch | Prohibited outright (DHA) |
| Parking shown inside a mandatory setback | Prohibited (LDA) |
| Missing soil investigation report | Mandatory for DHA; required for basements everywhere |
| Drawings unsigned, or architect not PCATP-registered | Engage a registered architect before drawing, not after rejection |
| Room below minimum area with no relaxation basis | Size to CDA Schedule-2 minima (or the local equivalent) |
| Drawings inconsistent — plan, elevation and section disagree | Generate elevations/sections from the same model, never hand-drawn separately |
| Building line ignored on a widening reservation | Read the approved layout plan, not just the byelaw setback table |
| Plot jurisdiction assumed instead of confirmed | Where two authorities plausibly apply (Section 4.3), get a written jurisdiction determination before submitting anywhere |

---

## Section 9: After Approval — The Rest of the Lifecycle

Approval of the map is the middle of the process, not the end. The stages below are standard Pakistani practice; **specific validity periods, penalty rates and certificate names are authority-specific — state them as "verify with the authority", never as fixed numbers.**

```
Approved map issued
   │
   ├─ 1. COMMENCEMENT NOTICE — many authorities require written intimation before
   │      starting work, and approval typically LAPSES if construction does not
   │      commence within a stated validity period (commonly quoted as ~2 years,
   │      often extendable on application). VERIFY the period and the extension route.
   │
   ├─ 2. SITE INSPECTIONS — the authority's building inspector may visit at
   │      plinth level, at each slab, and at completion. Keep the stamped map,
   │      the approval letter and the structural drawings on site.
   │
   ├─ 3. DEVIATIONS — any change from the approved map (extra room, deeper porch,
   │      converted setback, extra storey) requires a REVISED MAP submitted and
   │      approved BEFORE building it. Deviations found on inspection lead to
   │      stop-work notices, sealing, compounding/regularisation fees, or demolition
   │      of the deviating portion.
   │
   ├─ 4. COMPLETION / OCCUPANCY CERTIFICATE — applied for after construction,
   │      certifying the built work matches the approved map. Frequently required
   │      before permanent utility connections, before resale/transfer in managed
   │      schemes (DHA especially), and before mortgage disbursement.
   │
   └─ 5. UTILITY CONNECTIONS — WASA (water/sewerage), the local DISCO
          (LESCO/IESCO/K-Electric etc.), SNGPL/SSGC gas. These generally want to
          see the approved map, and sometimes the completion certificate.
```

**Regularisation is not a plan.** Building first and regularising later is common practice and a genuinely bad strategy: the fee is discretionary, the authority may refuse, and an unregularised deviation surfaces at resale, at transfer, or at the moment a neighbour complains. If a user proposes it, say plainly that it converts a fixed cost (design correctly now) into an open-ended risk.

**Appeals.** Rejections and objections are normally appealable within the authority (Director → Director General → Appellate/Building Committee). The practical route is almost always to fix the drawing rather than to litigate the byelaw.

---

## Section 10: NOCs and Clearances

| NOC / clearance | Issued by | When triggered |
|---|---|---|
| **Scheme / society NOC** | The housing society or DHA | Plot dues clear, membership/transfer in order — usually a prerequisite to submitting at all |
| **WASA NOC / connection** | WASA (or the local water & sanitation agency) | Water and sewerage connection; drainage discharge point |
| **Environmental clearance** | Provincial EPA / CDA environment wing | Larger projects; CDA runs an explicit environmental compliance verification step. Single houses are usually exempt — **verify threshold** |
| **Fire safety NOC** | Provincial/city fire authority (Rescue 1122 / civil defence, authority-specific) | Apartments and multi-storey buildings; generally not single-family houses — verify |
| **Cantonment Board NOC** | Cantonment Board | Any plot inside a cantonment |
| **Highway / road authority NOC** | NHA or provincial highway dept | Plots abutting a national/provincial highway with access from it |
| **Aviation height clearance** | Civil Aviation Authority | Building near an airport approach path — height-critical; rarely triggered by houses but binding when it is |
| **Utility clearances** | DISCO (LESCO/IESCO/K-Electric), SNGPL/SSGC | Connections; also relevant where an overhead HT line crosses the plot (clearance distances) |

**Sequencing rule:** society/scheme NOC and demarcation come **before** drawings are finalised, because they can change the buildable boundary. Environmental and fire NOCs, where triggered, run in parallel with technical review. Utility connections come last.

---

## Section 11: Structural Drawings, Stamping and Professional Registration

### 11.1 Who must stamp what

| Deliverable | Required professional | Registering body |
|---|---|---|
| Architectural drawings (plans, elevations, sections) | Registered Architect | **PCATP** — Pakistan Council of Architects and Town Planners (Architects & Town Planners Ordinance 1983) |
| Structural drawings, calculations, seismic design | Registered Professional Engineer (Civil/Structural) | **PEC** — Pakistan Engineering Council |
| Structural vetting / proof-check at the authority | The authority's structural cell, or an empanelled PEC-registered consultant | Authority + PEC |
| Soil investigation report | Geotechnical consultant / testing lab | PEC-registered firm |
| Concrete cube testing during construction | Approved materials-testing lab | Per BCP 2021 Ch.17 special inspections |

**PEC is the body that writes the national code AND licenses the engineers who stamp against it.** The local authority (LDA/CDA/SBCA/TMA) writes the byelaws and approves the map, but does not license engineers. Keeping these two institutional roles distinct is the mark of a correct answer.

### 11.2 Structural drawing set — minimum content for a residential submission

| Drawing | Content |
|---|---|
| General notes | Design code basis (BCP 2021 / ACI 318-19 / ASCE 7-16), concrete grade, steel grade, cover, seismic zone & zone factor, allowable bearing pressure, live loads used |
| Foundation plan | Footing layout, sizes, levels, reinforcement schedule, column grid with dimensions |
| Footing details | Section, depth below NGL, bar size/spacing, cover, plinth beam |
| Column schedule | Sizes, reinforcement, tie/stirrup spacing, splice zones and lap lengths |
| Slab plans (per floor) | Thickness, main/distribution steel, spacing, top/bottom, openings, cantilever reinforcement |
| Beam schedule | Sizes, reinforcement, stirrup spacing including seismic confinement zones at supports |
| Stair details | Waist thickness, reinforcement, landing details, bar anchorage at kinks |
| Retaining / basement wall details | Where a basement or a level change exists; drainage and waterproofing interface |
| Typical detailing sheet | Development lengths, laps, corner and beam-column junction detailing, 135° seismic hooks per ACI 318-19 Ch.18 where applicable |
| Water tank details | Underground and overhead tanks — frequently omitted and frequently the crack source |

### 11.3 The design-basis note — copy this pattern

```
STRUCTURAL DESIGN BASIS
  Code:            Building Code of Pakistan 2021 (Ch. 16 Structural Design, Ch. 19 Concrete)
                   [confirm with the vetting cell whether BCP 2007 + local practice is what will
                    actually be checked against — see Section 3.4]
  Loads:           ASCE 7-16 (adopted by reference in BCP 2021)
  Concrete design: ACI 318-19
  Seismic:         BCP seismic zone [__], PGA range [__] g, per BCP 2007 Table 2.2 (tehsil: [__])
                   Design basis: 10% probability of exceedance in 50 years
  Wind:            ASCE 7-16 method with BCP 2021 Pakistan basic wind speed [__]
  Soil:            Allowable bearing pressure [__] per soil investigation report dated [__]
  Concrete:        f'c = [__]   |   Steel: fy = [__]   |   Clear cover: [__]
  NOTE: Design to be reviewed and stamped by a PEC-registered Professional Engineer
        prior to submission and construction.
```

Every blank in that note that Claude cannot fill from a real source stays blank and is called out as blocked. **Do not populate `[__]` with a plausible number.**

---

## Section 12: Cross-Referencing US IBC / IRC / ACI Where Pakistani Documentation Is Thin

BCP 2021 is *built on* IBC 2021 and *references* ASCE 7-16 and ACI 318-19. That makes US values the closest legitimate analog when Pakistani residential documentation is silent — which it frequently is for small-house detailing (footing rebar for a 5-marla house, slab bar spacing, minimum footing depth, span-to-depth rules of thumb, glazing area).

### 12.1 The Flagging Protocol — mandatory

Every time a US value is used, it must be labelled inline, **and its actual scope of applicability must be checked before quoting it** — several commonly-cited IRC/ACI clauses are conditional (triggered only above a stated Seismic Design Category, occupancy class, or span), not universal minimums, and presenting a conditional clause as a blanket rule is its own flagging failure. Use exactly this form:

> *"[value] — **US IRC 2021 / ACI 318-19 reference value, not a Pakistan-mandated figure, [and applicable only where: state the actual condition, e.g. 'Seismic Design Category D0–D2']**. Use where the local drawing or byelaw is silent; the PEC-registered engineer of record must confirm or override — including confirming whether the condition that triggers this clause actually applies to this building."*

Never present an IRC or ACI number as "the Pakistani requirement". Never silently blend a US figure into a Pakistani table. Never import a US **planning** figure at all. Never strip a conditional US clause of its condition when quoting it.

### 12.2 Fallback value table (status column is the whole point)

| Item | US reference value | Source | Status |
|---|---|---|---|
| Max reinforcement spacing in slabs | Lesser of **3 × slab thickness** or **18 in** | ACI 318-19 | Referenced by BCP 2021 Ch.19 — strongest claim to applicability |
| Residential footing seismic reinforcement | Min **4 No.4 bars**, longitudinal | IRC 2021 §R403.1.3 | **Conditional, not universal — IRC §R403.1.3 applies this minimum specifically in higher Seismic Design Categories (per the IRC's own SDC trigger table), not to every footing everywhere.** US reference only; state the SDC condition when quoting it, and have the PEC engineer confirm the equivalent Pakistani seismic zone actually corresponds to that trigger level before applying it as a minimum |
| Residential footing transverse bar spacing | **12–18 in** | IRC 2021 §R403.1.3 | Same conditional status as above — US reference only, condition on SDC applies |
| Cover from footing bottom (cast against earth) | **~3 in** | IRC §R403.1.3 / ACI 318-19 cover table | ACI portion referenced by BCP 2021; the ACI cover requirement itself is not seismic-conditional, unlike the reinforcement-quantity rows above |
| Load combinations (LRFD / ASD) | ASCE 7-16 Ch. 2 | ASCE 7-16 | **Adopted by BCP 2021 — a direct requirement, not a fallback** |
| Wind loads | ASCE 7-16 Ch. 26–30 **with the Pakistan wind-speed map** | ASCE 7-16 + BCP 2021 | Method adopted; speeds are Pakistan-specific |
| Seismic loads | ASCE 7-16 Ch. 11–12 **with Pakistan PSHA** | ASCE 7-16 + BCP 2021 | Method adopted; hazard is Pakistan-specific |
| Snow / rain loads | ASCE 7-16 Ch. 7–8 with BCP 2021 northern-region provisions | BCP 2021 | Pakistan-modified |
| Natural light / ventilation glazing | 8% / 4% of floor area | IBC 2021 Ch.12 | BCP 2021 Ch.12 parallels it — confirm the BCP text |
| Egress stair riser/tread, headroom, door width | IBC 2021 Ch.10 / IRC 2021 | IBC/IRC 2021 | BCP 2021 Ch.10 parallels it; **but CDA's 3'-3" stair width is the local planning rule and is stricter** |
| Party-wall fire-resistance rating | 1-hour rated, IRC §R302.2 | IBC 2021 Table 302.1(2) / IRC 2021 §R302.2 | US reference only — Pakistani byelaws are silent (Section 3.5) |
| Setbacks, coverage, FAR, height, parking counts | — | — | **NO US ANALOG IS ADMISSIBLE. Local byelaw only.** |

### 12.3 Precedence order when values conflict

```
1. Local authority byelaw          → for ANY planning dimension (setback, coverage, FAR, height,
                                      room size, stair width as a planning minimum, parking, projections)
2. BCP 2021 (+ ASCE 7-16, ACI 318-19 as adopted by reference)
                                   → for ANY structural or life-safety requirement
3. BCP 2007 Table 2.2              → for seismic zone / PGA specifically
4. IRC 2021 / IBC 2021 / ACI 318-19 direct
                                   → ONLY where 1–3 are silent, ONLY with the flag above,
                                     AND only after checking the clause's actual condition/scope
5. Engineering judgement of the PEC-registered engineer of record
                                   → always final, always overrides this skill
```

**Never let 4 override 1.** A US IRC setback or height figure is meaningless in Pakistan — the planning layer has no US analog worth importing.

---

## Section 13: Worked Examples

### 13.1 Worked Example 1 — 5 marla house, DHA Lahore Phase 6

```
INPUTS
  Plot: 5 marla = 25'-0" × 45'-0" = 1,125 sq ft
  Authority: DHA Lahore, Phase 6 (Phase >= 5 → 35 ft height band)

SETBACKS (DHA 5 marla row)
  Front 5'-0"  |  Rear 3'-0"  |  Sides 3'-0" each

BUILDABLE FOOTPRINT
  Width  = 25'-0" − (3'-0" + 3'-0")  = 19'-0"
  Depth  = 45'-0" − (5'-0" + 3'-0")  = 37'-0"
  Envelope = 19 × 37 = 703 sq ft = 62.5% of plot

FLOOR COVERAGE
  Ground floor: up to the 703 sq ft envelope (subject to the DHA covered-area
                definition — confirm whether porch / terrace / mumty count)
  First floor:  5 marla → may equal 100% of the ground-floor permissible area → 703 sq ft
                (contrast: at 10 marla this would be capped at 75%)

HEIGHT
  Max 35'-0" from ROAD LEVEL (Phase >= 5)
  Allocation: plinth 2'-0" + GF 11'-0" + FF 11'-0" = 24'-0";
              11'-0" remains for a mumty/stair block and parapet
              → confirm whether the mumty counts toward the cap in this phase
  Living-room clear ceiling must land in the 9'-6"–12'-0" band → 10'-6" clear works

CAR PORCH
  Depth 12'-0" min, 18'-0" max, plus a 2'-0" projection allowed
  Height >= 9'-0" and <= ground-floor height (11'-0") → set 9'-6"
  NO BASEMENT beneath the porch
  Reality check: a 12'-0" porch will not comfortably park a sedan with walk-around;
                 take 16'-0" if the coverage budget allows

BOUNDARY WALL
  7'-0" max

STRUCTURE
  Lahore ~ BCP seismic Zone 2A (VERIFY Table 2.2, Lahore tehsil)
  Design per BCP 2021 Ch.16/19 → ACI 318-19
  Slab bar spacing <= min(3t, 18 in) — ACI 318-19, referenced by BCP 2021 Ch.19
  Footing reinforcement: engineer to size. Where the drawing is silent, IRC §R403.1.3's
    4 No.4 longitudinal + 12–18 in transverse + ~3 in bottom cover is a US IRC reference
    value tied to higher Seismic Design Categories in the IRC's own framework, NOT a
    universal minimum and NOT a Pakistan-mandated figure — PEC engineer confirms both
    the applicability of the SDC condition and the final sizing

GATE
  Drawings signed by a PCATP architect; structure stamped by a PEC engineer;
  soil report (DHA mandatory); submit via the DHA portal; expect 3–6 weeks;
  then commencement notice, inspections, and a completion certificate at the end.
```

### 13.2 Worked Example 2 — 1 kanal house, LDA Lahore (non-DHA society)

```
INPUTS
  Plot: 1 kanal = 50'-0" × 90'-0" = 4,500 sq ft
  Authority: LDA (LDA-approved private society)

HEIGHT (LDA 2019, as amended)
  Plot >= 1 kanal and < 2 kanal → up to 90'-0", Ground + 6
  → the height limit is NOT the binding constraint for a single-family house;
    coverage, setbacks and budget are. Do not design to 90 ft because it is "allowed".

PARKING (LDA 2019 amendment — the constraint people miss)
  Parking NOT permitted within mandatory setback areas
  → the setback strip must be walkway / green space
  → the car porch must sit inside the buildable envelope, consuming ground-floor
    covered area, OR use a permitted projection — verify with LDA
  Design consequence: ~200–250 sq ft of the ground floor is spent on the porch
  before a single room is placed.

SETBACKS
  LDA setbacks are scheme-specific — the DHA table does NOT apply.
  → BLOCKED: read the specific society's APPROVED LAYOUT / ZONING PLAN.
  → Check for a BUILDING LINE on that plan; if a road-widening reservation exists,
    the building line sits behind the plot boundary and governs.
  → Do NOT substitute the DHA 1-kanal row (15'-9" / 5'-4½" / 5'-4½") as if it were LDA's.
  → If the society was later absorbed into expanded municipal limits or its jurisdiction
    is otherwise unclear, treat this as a Section 4.3 case and get it confirmed in writing
    before relying on either the original covenant or current LDA regs.

STRUCTURE
  Same BCP 2021 basis as Example 1. Zone 2A (verify by tehsil).
```

### 13.3 Worked Example 3 — Sector house, CDA Islamabad

```
INPUTS
  Authority: CDA, Islamabad sector plot
  Seismic: Zone 2B commonly cited for Islamabad — VERIFY BCP 2007 Table 2.2

SPACE STANDARDS (Schedule-2) — hard planning minima
  Dwelling unit >= 600 sq ft excl. stairs      (10% relaxable)
  Every habitable room >= 100 sq ft            (10% relaxable)
  Kitchen >= 45 sq ft                          (10% relaxable)
  Each bathroom >= 24 sq ft                    (10% relaxable)
  Door height 7'-0" (6'-6" tolerated)
  Stair flight width 3'-3" (2'-9" tolerated)

PROJECTIONS
  Roof projection over a <= 20 ft street: max 1'-6"
  GF/FF projection into setback: max 3'-0"

SANITY CHECK on a proposed plan
  3 bedrooms at 11'×12' = 132 sq ft each       → PASS (>100)
  Kitchen 8'×7' = 56 sq ft                     → PASS (>45)
  Bath 5'×5' = 25 sq ft                        → PASS (>24) but by 1 sq ft → go to 5'×5'-6" = 27.5
  Stair 3'-0" clear flight                     → 3 in short of 3'-3"; inside the tolerance band
                                                  but DISCRETIONARY → widen to 3'-3", remove the risk
  Bedroom glazing 11'×12' = 132 sq ft → needs >= 10.6 sq ft glazed (IBC Ch.12 8% reference value)
                                        a 5'×4' window = 20 sq ft → PASS comfortably

PROCESS
  OWO submission → technical review → environmental compliance verification → approval
```

### 13.4 Worked Example 4 — Deciding between conflicting numbers

```
USER: "What's the setback for a 5 marla plot in Pakistan?"

WRONG ANSWER: "5 ft front, 5 ft rear, no side setback."
  (That is the generic circulating figure. It contradicts DHA Lahore's 5/3/3.)

CORRECT ANSWER:
  "There is no national setback rule — BCP doesn't set setbacks at all; the local
   authority does. Which city and scheme is the plot in?
     • DHA Lahore, 5 marla:  front 5'-0", rear 3'-0", sides 3'-0"
     • Generic LDA-type 5 marla figures in circulation: front 5'-0", rear 5'-0",
       no mandatory side setback, coverage 75% GF / 75% FF, height 38'-0" from road crown
   These conflict because they are different authorities. Tell me the scheme and I'll
   use the right one — and either way this needs verification against the authority's
   current published regulations before you build to it."
```

### 13.5 Worked Example 5 — Adding a storey to an existing house

```
USER: "I want to add a first floor to my existing 10 marla single-storey house in Lahore."

REGULATORY LAYER (byelaw)
  • This is a DEVIATION from the approved map → a REVISED MAP must be submitted and
    approved BEFORE construction. It is not a "minor addition".
  • Re-test coverage AND the first-floor cap: DHA 10 marla → first floor limited to
    75% of ground-floor covered area. The existing ground floor may already be at the
    coverage limit, which caps the new floor at 75% of it, not 100%.
  • Re-test height from ROAD LEVEL including the existing plinth, the existing GF height,
    the new FF height, and the mumty. Existing plinth is often the reason the addition
    breaks the cap.
  • Check setbacks of the NEW floor: it may not project beyond the ground floor into
    a setback even if the ground floor was approved under older rules.
  • Older approvals may have been granted under a SUPERSEDED byelaw. The new work is
    judged against the CURRENT regulations. Grandfathering protects what exists, not
    what you add.

STRUCTURAL LAYER (code) — this is where people get hurt
  • The existing foundations were sized for one storey. Adding a storey increases
    footing pressure roughly proportionally. A PEC-registered engineer must verify the
    EXISTING footings and columns against the new loads — this requires trial pits to
    expose footing size and depth, plus a soil investigation.
  • If the existing house is UNREINFORCED MASONRY, adding a storey in Zone 2B/3/4 is
    the classic fatal configuration. Say so explicitly.
  • Existing column reinforcement and lap positions are unknown until exposed.
    Assume nothing.
  • Seismic re-check of the whole (now taller, possibly softer) building is required,
    not just a design of the new floor.

CORRECT RESPONSE SHAPE
  "Two separate gates here. Regulatory: this needs a revised map approved before you
   build, and the new floor is judged against current byelaws, not the ones your
   original map was approved under. Structural: the existing foundations were designed
   for one storey — a PEC-registered engineer has to expose and verify them before
   anything goes up. I can help you plan the envelope; I cannot tell you the existing
   structure can take it, and neither can anyone who hasn't dug a trial pit."
```

---

## Section 14: FreeCAD Modelling Integration

Pair this skill with `architecture-freecad-bim`. Model the regulatory envelope as *geometry*, so violations are visible rather than arithmetic.

### 14.1 Build the byelaw envelope first, the house second

```python
# Pseudocode / FreeCAD parametric intent — NOT construction geometry
PLOT_W, PLOT_D   = 25.0, 45.0      # ft — 5 marla, DHA Lahore
SETBACK_FRONT    = 5.0
SETBACK_REAR     = 3.0
SETBACK_SIDE     = 3.0
HEIGHT_MAX       = 35.0            # DHA Phase >= 5, measured from ROAD LEVEL
BOUNDARY_WALL_H  = 7.0
PORCH_D_MIN, PORCH_D_MAX = 12.0, 18.0
PORCH_H_MAX      = 11.0            # = ground-floor height

# 1. Plot solid                → visual reference, z=0 at ROAD_LEVEL datum
# 2. Setback solids            → red, semi-transparent, LOCKED. These are NO-BUILD volumes.
# 3. Buildable envelope        = plot extruded to HEIGHT_MAX, minus the setback solids
# 4. Model the house INSIDE the envelope
# 5. COMPLIANCE ASSERTIONS — run them, do not eyeball them:
#      Common(house, setback_solids).Volume        == 0
#      house.BoundBox.ZMax - ROAD_LEVEL            <= HEIGHT_MAX
#      porch.Height                                <= PORCH_H_MAX  and >= 9.0
#      PORCH_D_MIN <= porch.Depth <= PORCH_D_MAX
#      Common(basement, porch_footprint).Volume    == 0      # DHA: no basement under porch
#      boundary_wall.Height                        <= BOUNDARY_WALL_H
#    If any assertion fails, REPORT the violating volume and its location.
#    Never round a violation away, never adjust the limit to match the design.
#    Use the plot's ACTUAL dimensioned size, not a nominal marla-area figure —
#    see the Section 5.1 area/dimension flag for why the two can differ by ~1%.
```

### 14.2 Objects to model separately (each carries an independent limit)

| Object | Independent limit it carries |
|---|---|
| Car porch | Own height cap (>= 9'-0", <= GF height), own depth range 12–18 ft, no basement under |
| Boundary wall | 7'-0" cap, independent of building height |
| Basement | Single storey only; 9'-0"–10'-0" ceiling; extent under setbacks restricted |
| Roof / eave projection | 1'-6" over a <= 20 ft street (CDA), separate from the wall face |
| Balcony / cantilever | <= 3'-0" into setback (CDA) |
| Stair core / mumty | Flight width 3'-3" (CDA); may or may not count toward the height cap — verify |
| Overhead water tank | Rooftop appurtenance; verify whether it counts toward height |
| Plinth | Counts toward the height cap; model it, do not fold it into "ground floor" |
| Party/shared wall (semi-detached, row houses) | No Pakistani numeric fire rating exists — model the wall thickness per structural/local practice, and flag fire-separation as unresolved per Section 3.5, not as "compliant" |

### 14.3 Height datum discipline

Byelaw heights are measured **from road level / road crown**, not from finished floor level and not from the plot's natural ground level. In FreeCAD, place a named datum plane `ROAD_LEVEL` at z = 0 and measure the compliance dimension from it. Plinth height above road level *counts* toward the cap. This is a routine cause of a legal-on-paper, illegal-in-fact second floor.

### 14.4 Coverage computation

```
covered_area(floor) = sum of enclosed floor-plate areas

QUESTIONS TO RESOLVE WITH THE AUTHORITY BEFORE COMPUTING (or flag as unresolved):
  Does covered area include — car porch? open terrace? projected balcony?
  cantilevered slab? stair mumty? servant quarter? basement?
  Is it measured to the outside face of wall or to the wall centreline?

Definitions differ by authority and materially change whether a plan passes.
NEVER report a coverage percentage without stating which definition you used.
Report it as: "62.5% using [definition] — confirm the definition with [authority],
because counting the porch would take this to 71%."
```

### 14.5 What the model is and is not

The FreeCAD output of this workflow is a **compliance envelope plus a massing study**. It is not a submission drawing, not a structural model, and not evidence of approval. Say this in the same message that delivers the model — not in a footnote.

---

## Section 15: Pre-Submission Compliance Checklist

Run this before telling a user a design "should be fine".

**Planning layer (local byelaw)**
- [ ] Authority, scheme and phase identified and named in the answer
- [ ] Plot jurisdiction confirmed as single and unambiguous — not straddling two authorities (Section 4.3)
- [ ] Approved layout plan checked for a building line / road-widening reservation
- [ ] Front / rear / side setbacks satisfied — verified by boolean, not by eye
- [ ] Corner / two-road / park-facing conditions checked for extra setbacks
- [ ] Ground-floor coverage % within limit, **with the coverage definition stated**
- [ ] First-floor coverage within the ground-floor-linked cap (DHA: 75% at 10 marla+, 100% at 5 marla)
- [ ] FAR within limit where the authority uses FAR (RDA: 1 : 1.4 up to 38 ft) — a separate test from coverage, computed from the plot's ACTUAL dimensioned area, not a nominal marla figure
- [ ] Total height <= limit, measured from **road level**, plinth included
- [ ] Mumty / parapet / water tank treatment confirmed with the authority
- [ ] Storey count within limit
- [ ] Car porch depth/height within range; no basement beneath it
- [ ] Parking not placed inside a mandatory setback (LDA)
- [ ] Basement single-storey; ceiling 9'-0"–10'-0"; extent under setbacks checked
- [ ] Boundary wall <= 7'-0"
- [ ] Projections within limits (1'-6" over a <= 20 ft street; 3'-0" into setback)
- [ ] All habitable rooms >= 100 sq ft; kitchen >= 45; bath >= 24; unit >= 600 (CDA baseline)
- [ ] Stair flight >= 3'-3"; door height 7'-0"
- [ ] Glazing >= 8% and openable >= 4% of floor area per habitable room (IBC Ch.12 reference — flagged)
- [ ] Party/shared wall fire-separation flagged as an unresolved Pakistani-documentation gap, not asserted compliant (Section 3.5)

**Structural / code layer (BCP)**
- [ ] Seismic zone read from BCP 2007 Table 2.2 by **tehsil**, not guessed from a nearby city
- [ ] Design-basis note written naming BCP 2021 Ch.16/19, ASCE 7-16, ACI 318-19
- [ ] Which code edition the specific vetting cell actually checks against has been confirmed, not assumed (Section 3.4)
- [ ] Soil investigation report obtained (mandatory DHA; required for any basement)
- [ ] Allowable bearing pressure taken from the report, not assumed
- [ ] Slab bar spacing <= min(3t, 18 in) — ACI 318-19
- [ ] Seismic detailing appropriate to the zone (135° hooks, confinement zones) where applicable
- [ ] Every US IRC/ACI/IBC fallback value explicitly flagged as a US reference, **with its actual conditional scope (e.g. SDC trigger) stated, not stripped off**

**Approval layer**
- [ ] Architectural drawings signed by a PCATP-registered architect
- [ ] Structural drawings stamped by a PEC-registered Professional Engineer
- [ ] CNICs, ownership documents, society NOC, WASA/other NOCs, affidavit assembled
- [ ] Fee challans computed and paid through the designated bank
- [ ] Realistic timeline communicated: 3–6 weeks for a clean submission, +1–3 weeks per objection cycle
- [ ] Post-approval lifecycle explained: commencement notice, inspections, revised map for any deviation, completion certificate

**Liability layer**
- [ ] The user has been told, in plain words, that this is not construction-ready without PEC stamping and authority approval

---

## Section 16: Answer Templates

### 16.1 When the authority is unknown

> "Before I give you a number: BCP — the national code — doesn't set setbacks, coverage or height. Those come entirely from your local authority, and they differ by city and even by DHA phase. Which city, which authority (LDA/CDA/SBCA/DHA/TMA), and which scheme and phase? Once I know that I can give you the actual table instead of an average that matches nowhere."

### 16.2 When Pakistani documentation is genuinely thin

> "Pakistani residential byelaws don't publish a figure for this. BCP 2021 is built on IBC 2021 and adopts ACI 318-19 by reference, so the closest defensible analog is [value] from [ACI 318-19 §x / IRC 2021 §Rx] — [state the condition, e.g. 'this specific value applies in the IRC's higher Seismic Design Categories, not universally']. **Flagging that clearly: that's a US reference value, not a Pakistan-mandated figure, and it may not even apply universally in its own code.** Use it where the local drawing is silent, and have the PEC-registered engineer of record confirm or override it."

### 16.3 When the user treats output as final

> "Stop — this is a planning model, not a stamped drawing. Before anything gets built: a PEC-registered structural engineer has to review and stamp the structural design, a PCATP-registered architect has to sign the architectural set, and [authority] has to approve the map. What I've given you is a compliant *envelope* to design inside, which is a different thing from an approval."

### 16.4 When the user proposes building first and regularising later

> "That's common and it's a bad trade. Regularisation is discretionary — the authority can refuse, the fee isn't fixed, and the deviation resurfaces at resale, at transfer, and the first time a neighbour complains. Designing inside the byelaw now is a fixed, known cost. Regularising later is an open-ended one. If the plan only works by breaking a setback, the plan needs to change."

### 16.5 When two authority tables conflict

> "Both numbers are real; they're just from different authorities. [Authority A] says [X], [Authority B] says [Y]. There is no national figure that reconciles them, and averaging them would produce a number that's wrong everywhere. Tell me the scheme and phase and I'll use the right row."

### 16.6 When the plot straddles two jurisdictions

> "This plot sits where [Authority A] and [Authority B] both plausibly apply, and I don't have a rule that resolves that cleanly. [Authority A] says [X]; [Authority B] says [Y]. Rather than guess, the right move is a written jurisdiction query to both authorities' Town Planning wings — proceeding on an assumption here risks designing to the wrong table entirely."

---

## Section 17: Units and Conversions

The marla is **not a fixed unit**. Two systems are in live use, and using the wrong one mis-sizes a plot by 21%.

| Unit | Modern scheme standard (DHA, most LDA schemes) | Legacy / revenue standard |
|---|---|---|
| 1 marla | 25 sq yd = **225 sq ft** = 20.9 m² | 30.25 sq yd = **272.25 sq ft** = 25.3 m² |
| 1 kanal (= 20 marla) | 500 sq yd = **4,500 sq ft** = 418 m² | 605 sq yd = **5,445 sq ft** = 506 m² |
| 1 acre | 8 kanal | 8 kanal |

**Consistency check against the DHA plot dimensions in Section 5:** 5 marla = 25'×45' = 1,125 sq ft = 5 × 225 ✓; 1 kanal = 50'×90' = 4,500 sq ft ✓; 2 kanal = 100'×90' and 75'×120' = 9,000 sq ft ✓. **The DHA/LDA scheme tables use the 225 sq ft marla for most plot sizes** — with one documented exception: DHA's own commonly-published 10-marla dimension of 35'×65' multiplies to 2,275 sq ft, not the nominal 10 × 225 = 2,250 sq ft (a 25 sq ft / ~1.1% difference — see the flag in Section 5.1). Use the 225 sq ft/marla figure as the default planning approximation for modern urban schemes, but **always substitute a plot's actual surveyed/scheme dimensions for any real coverage, FAR or setback-envelope calculation** — the nominal marla-area figure is for order-of-magnitude sizing only, not for a compliance check.

**Common plot dimensions (scheme convention, verify per scheme — dimensions and the nominal marla × 225 sq ft area do not always multiply to the identical figure; where they differ by a small margin, the actual dimensioned size on the site plan governs):**

| Nominal size | sq yd | Nominal area (marla × 225 sq ft) | Typical dims | Dims × area check |
|---|---|---|---|---|
| 3 marla | 75 | 675 sq ft | 22'-6" × 30'-0" | 22.5 × 30 = 675 ✓ |
| 5 marla | 125 | 1,125 sq ft | 25' × 45' | 25 × 45 = 1,125 ✓ |
| 7 marla | 175 | 1,575 sq ft | 35' × 45' | 35 × 45 = 1,575 ✓ |
| 8 marla | 200 | 1,800 sq ft | 30' × 60' | 30 × 60 = 1,800 ✓ |
| 10 marla | 250 | 2,250 sq ft (nominal) | 35' × 65' (commonly published — see flag) | 35 × 65 = **2,275**, not 2,250 — use the actual scheme dims, not the nominal figure, for any real calculation |
| 1 kanal | 500 | 4,500 sq ft | 50' × 90' | 50 × 90 = 4,500 ✓ |
| 2 kanal | 1,000 | 9,000 sq ft | 100' × 90' or 75' × 120' | 100 × 90 = 9,000 ✓ / 75 × 120 = 9,000 ✓ |

| Other conversions | |
|---|---|
| 1 ft | 0.3048 m |
| 1 sq ft | 0.0929 m² |
| 1 in | 25.4 mm |
| 1 sq yd | 9 sq ft = 0.836 m² |
| 30 ft | 9.14 m |
| 35 ft | 10.67 m |
| 38 ft | 11.58 m |
| 48 ft | 14.63 m |
| 90 ft | 27.43 m |
| 160 ft | 48.77 m |

---

## Section 18: Glossary — Pakistani Permit Vocabulary

| Term | Meaning |
|---|---|
| **Naqsha / map** | The architectural drawing set submitted for approval; "map approval" = building permit |
| **Byelaws** | The local authority's building regulations (planning layer) — never the national code |
| **Code** | The Building Code of Pakistan (structural / life-safety layer) |
| **Setback** | Mandatory unbuilt distance measured from the plot boundary |
| **Building line** | A line fixed on the approved layout plan behind which building must stay; governs over the byelaw setback where both exist |
| **Covered area** | Enclosed floor-plate area counted toward coverage — the definition is authority-specific |
| **Ground coverage** | Footprint area as a % of plot area |
| **FAR / FSI** | Floor area ratio — total floor area across all storeys ÷ plot area |
| **Road crown / road level** | The datum from which building height is measured |
| **Plinth** | The raised base of the building above ground; counts toward the height cap |
| **Mumty** | The stair enclosure projecting above the roof slab |
| **Chajja / sunshade** | Projecting slab over a window |
| **DPC** | Damp-proof course at plinth level |
| **Challan** | The bank payment slip through which authority fees are paid (Bank of Punjab for LDA) |
| **CNIC** | National identity card — required from every owner |
| **NOC** | No Objection Certificate from a department or the scheme |
| **OWO** | One Window Operation — CDA's single-counter submission route |
| **Demarcation** | The authority's official marking of the plot boundary on site |
| **Jurisdiction determination** | A written finding from an authority (or authorities) confirming which byelaws govern a specific plot — needed where two authorities plausibly apply (Section 4.3) |
| **Compounding / regularisation fee** | Penalty paid to legalise unapproved or deviating construction — discretionary, not a right |
| **Completion certificate** | Certificate that the built work matches the approved map; often needed for utilities and transfer |
| **PEC** | Pakistan Engineering Council — licenses engineers, writes the national code |
| **PCATP** | Pakistan Council of Architects & Town Planners — licenses architects |
| **Katcha / pucca** | Temporary/informal vs permanent masonry construction |

---

## Section 19: Citation Discipline

1. **Name the layer.** Say "byelaw" for planning and "code" for structure. Never call a setback a "code requirement".
2. **Name the institution.** PEC writes the code; LDA/CDA/SBCA/RDA/DHA/TMA write the byelaws. They are different bodies with different powers.
3. **Name the document and vintage.** "LDA Building & Zoning Regulations 2019, amended to 2021" — not "LDA rules".
4. **Name the table.** "BCP 2007 Table 2.2" for seismic zone; "CDA Schedule-2" for space standards; "the DHA setback table by plot size".
5. **Flag every US value — including its actual scope.** Section 12's protocol is not optional, and a flagged value stripped of its real trigger condition (e.g. quoting a seismic-conditional IRC clause as if it were universal) is still a citation failure.
6. **State the vintage risk.** Byelaws are amended frequently (LDA 2019 → 2020 → 2021 draft; Karachi 2002 → 2005 → 2017). Recommend verification against the current published regulation every time.
7. **Separate cited from inferred.** If a number came from a byelaw PDF, say so. If it is common practice, say "commonly applied — verify". If it is a US analog, flag it. Three different confidence levels, three different labels.
8. **Say "I don't know" over inventing a plausible number.** A wrong setback becomes a demolition notice. "That figure has to come off the authority's published table — I can tell you exactly where to find it" is a correct and useful answer. The same applies to institutional facts: if an exact adoption date, enforcement status, or jurisdiction cannot be confirmed from a real source, say so rather than filling the gap.
9. **Reconcile arithmetic before publishing it, and disclose it when it doesn't reconcile.** Where a nominal unit conversion and a commonly-cited scheme dimension disagree (Section 5.1, Section 17), say so explicitly rather than presenting only one figure or silently rounding one to match the other.

### 19.1 Primary sources

| Source | URL |
|---|---|
| BCP 2007 (Seismic Provisions) | `https://urbanunit.gov.pk/Download/publications/Files/8/2021/Pakistan%20Building%20Code%202007.pdf` |
| BCP 2021 final draft (PEC) | `https://www.pec.org.pk/wp-content/uploads/2024/09/BCP2021-Final-Draft-dated-26.10.2021.pdf` |
| BCP 2021 Ch.16 Structural Design (ICC) | `https://codes.iccsafe.org/content/PKBC2021P1/chapter-16-structural-design` |
| BCP 2021 Ch.19 Concrete (ICC) | `https://codes.iccsafe.org/content/PKBC2021P1/chapter-19-concrete` |
| BCP 2021 Preface (ICC) | `https://codes.iccsafe.org/content/PKBC2021P1/preface` |
| PEC Building Code think tank | `https://www.pec.org.pk/thinktank/building-code-of-pakistan-thinktank/` |
| ICC–PEC partnership announcement | `https://www.phcppros.com/articles/14469-international-code-council-partners-pakistan-engineering-council-to-develop-building-code-of-pakistan` |
| LDA Amended Building Regulations 2019 | `https://lda.gop.pk/website/images/Amended_Building_Regulations_2019_with_amendment_approved_till_28_01_2020.pdf` |
| LDA Draft Final Building Regulations 2021 | `https://lda.gop.pk/website/images/DRAFT_FINAL_BUILDING_REGULATIONS_22_06_2021.pdf` |
| RDA Building Regulations | `https://www.cbrechs.org.pk/documents/RDA_Building_Regulations.pdf` |
| CDA laws & regulations | `https://www.cda.gov.pk/lawsAndRegulations` |
| Karachi B&TP Regulations, 2005 amendment | `https://www.sbca.gos.pk/pdf/R-AM-4-Aug-2005.pdf` |
| Karachi B&TP Regulations, 2017 amendment | `https://www.sbca.gos.pk/pdf/R-AM-28-Aug-2017.pdf` |
| SBCA height/regulation extract | `http://www.ksez.com.pk/PDF/sbca/ss10.pdf` |
| DHA Karachi Revised Bylaws 2020 | `https://www.dhakarachi.org/wp-content/uploads/2022/07/Revised-DHA-ByLaws-2020-New.pdf` |
| DHA Lahore construction bylaws digest | `https://www.zameen.com/blog/construction-bylaws-dha-lahore.html` |
| LDA new building regulations digest | `https://www.zameen.com/blog/new-lda-building-regulations.html` |
| CDA residential bylaws digest | `https://primarcstudio.com/bylaws/cda-bylaws-houses-flats-plots-residentials-other-than-diplomatic-enclave/` |
| Islamabad building regulations / approval guide | `https://www.arcodesk.com/islamabad-building-regulations-2026-complete-updated-cda-rules-for-building-approval/` |
| House map approval, Lahore (process/fees) | `https://aqsonsgroupofcompanies.com/house-map-approval-lahore/` |
| Documents required for LDA/DHA map approval | `https://www.aimsbuilder.com/blog/documents-required-for-map-approval-from-lda-dha/` |
| Map approval overview, Pakistan | `https://landsolvedin.com/map-approval-house-construction-pakistan/` |
| Pakistan Accord Building Standard v1.1 | `https://internationalaccord.org/wp-content/uploads/2023/09/Pakistan-Accord-Building-Standard-Version-1-1.pdf` |
| ACI 318-19 footing guidance | `https://calcs.com/blog/concrete-footings-aci-318-19` |
| IRC 2021 §R302.2 (fire-resistant construction, party walls) | `https://codes.iccsafe.org/content/IRC2021P1` |
| IRC 2021 §R403.1.3 (seismic reinforcing for footings, conditional on SDC) | `https://codes.iccsafe.org/content/IRC2021P1` |

**Source-quality note:** the `zameen.com`, `primarcstudio.com`, `arcodesk.com`, `aimsbuilder.com` and similar entries are **secondary digests**, not the regulation itself. They are cited here because several authority PDFs are unindexed or offline, and their numeric tables are the most widely used in practice. Always present them as "as digested from the DHA/LDA bylaws — verify against the authority's published document", never as a primary citation.

### 19.2 Related skills

`architecture-structural-systems` (system selection, span-to-depth, foundations) · `architecture-seismic-design` (zone factors, base shear, detailing) · `architecture-geotechnical-foundations` (soil investigation, bearing capacity, footing depth) · `architecture-concrete-reinforcement-detailing` (rebar, cover, laps to ACI 318-19 + BCP) · `architecture-spatial-planning` (plan layout, circulation, room sizing) · `architecture-building-typology` (residential typologies) · `architecture-accessibility-design` (accessible routes — ADA/BS 8300 are non-binding in Pakistan; use as best practice) · `architecture-cost-estimation-boq` (fees, BOQ, approval cost lines) · `architecture-construction-sequencing` (post-approval build order and inspection hold points) · `architecture-freecad-bim` (building the model) · `drawio-diagrams` (2D submission-style plans)
