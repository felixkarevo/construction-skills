> **LEGACY WORKED EXAMPLE — ARCHIVAL RECORD.** This document is the original
> design study for the demo model `example-house.FCStd`, produced on a
> South-Asian (Pakistan) 5-marla plot. Its jurisdiction-specific content is kept
> only as a historical record of how the modeling workflow was developed. It is
> **not** part of the DACH/European skill library and must not be used as
> regulatory guidance. The durable engineering knowledge from this exercise was
> distilled into the `skills/` directory.

# Climate-Responsive 5-Marla House — Rawalpindi, Pakistan

**Plot:** 25 ft × 45 ft (1,125 sq ft, 5 marla @ 225 sq ft/marla) · **Configuration:** G+1 · **Primary orientation case:** East-open (assumed — verify on site)

---

## ⚠ Reality Check — read this before anything else

**Everything in this document is a conceptual design and planning study.** All dimensions, coverage/FAR figures, structural member sizes, seismic zone assumptions, and cost bands are preliminary, or explicitly flagged as unverified secondary-source placeholders (tier T1-U, per `architecture-spatial-planning`'s evidentiary tiers). Nothing here is a construction document and nothing here should be built from directly.

Before any excavation this design requires:

1. A **PEC-registered structural engineer's** calculation and stamped drawings.
2. A **PCATP-registered architect's** drawings.
3. **RDA (Rawalpindi Development Authority)** plan approval against its current, dated bylaw schedule — which overrides every coverage/setback/FAR number used here.
4. A **site-specific soil report** (trial pits/boreholes with SPT, plus a soaked oedometer test — see Section 8, the Potohar loess-collapse risk).
5. Confirmation of the **actual site orientation and party-wall condition** — this document assumes an east-open, corner/side-open plot as its primary working case (see Sections 1 and 3.0) and flags throughout what changes if the real plot is mid-row or a different orientation.

Treat every number below as a starting point for that professional process, not a substitute for it.

---

# Part I — Design Narrative (Sections 1–13)

## 1. Plot and Basic Requirements

**Verified plot match:** the brief's 25 ft × 45 ft = 1,125 sq ft plot matches **5 marla on the 225 sq ft/marla basis** exactly (`architecture-spatial-planning` §1.2). Flag: Rawalpindi sits directly adjacent to Islamabad, where the standard marla basis is 272.25 sq ft, not 225 — **confirm the deed/allotment-letter basis before proceeding**; if the real basis is 272.25, the plot is larger than assumed and every downstream number (coverage, room budget, light-well size) should be re-run.

**Orientation assumption (primary case):** this design takes an **east-open** plot as the primary case — road and main entrance on the east 25 ft frontage, 45 ft depth running north–south — and treats it as a **corner/side-open** plot (only one long face is a shared party wall), not a fully enclosed mid-row lot. This is a stated assumption, not a site fact (see the load-bearing caveat in Section 3.0 and the party-wall reality check in Section 9/Output H) — confirm the real road-facing edge and the real party-wall condition on both long faces before this plan is used.

Full plot verification, buildable-envelope arithmetic (coverage vs. setback), parking, light-well sizing, prevailing-wind assumption, and the labeled site plan are given in **Output B — Site Strategy** below. Full adaptation notes for north-, south-, and west-open variants of this same 25×45 rectangle are given there too (§ Output B / A.5).

## 2. Design Philosophy / Architectural Form

At 25 ft of frontage, two 9 in perimeter walls leave only **23.5 ft of internal clear width** — enough for one 12–14 ft room, a 4 ft passage, and a 5 ft bath side by side, and nothing more (`architecture-spatial-planning` §1.3/1.4). Running the plan-archetype decision tree against this frontage lands on one answer: **Linear / Side-Passage** is the only archetype the numbers support. A true central courtyard needs roughly 10+ ft of spare plan width beyond the room budget — this plot has none.

Rather than force a courtyard the brief doesn't have room for, the honest move is to **fuse the light/vent well with the staircase void into a single vertical ventilation shaft** — a scaled-down, honestly-sized descendant of the badgir/courtyard stack-effect principle, sized as a light-and-vent well rather than dressed up as a courtyard it structurally cannot be. This shaft does three jobs traditionally split across a courtyard, a windcatcher, and a stairwell: it lights the two blind middle rooms of the linear plan, it draws cool air in low and vents hot air high, and it houses the stair itself so no separate volume is spent on vertical circulation.

**Design priorities, in order:** (1) get the long 45 ft walls facing north and south — free on the east-open case; (2) treat the stair and light/vent well as one shared passive-cooling device, not two problems; (3) push every low-occupancy/heat-tolerant room (stair, bath, store) onto the harder facades so bedrooms and living space get the good ones; (4) lead with traditional passive devices (jali, deep reveals, chajjas, roshandans) as the primary climate strategy, with mechanical cooling as occupant-controlled backup, not the default.

Full form-exploration reasoning and the north/south/west-open adaptation notes for this philosophy are given in **Output A — Design Concept** below.

## 3. Traditional Passive Cooling Techniques

### 3.0 Plot orientation assumption — load-bearing, read before the rest of this section

Everything downstream in Sections 3–6 and Output diagrams E/F depends on which two faces of the 25×45 plot are open air and which are shared party walls. This has to be stated explicitly, because two things this design wants — a south-facing window for winter solar gain (Section 4/5) and a north-facing window for cross-ventilation (Section 6) — are only both possible under one specific plot configuration.

**Working assumption used throughout this document:** the 25 ft dimension is the street frontage (east); of the two 45 ft long sides, **only the south side is a shared party wall** — i.e. a **corner or side-open plot**, not a fully enclosed mid-row plot. That gives three open faces (east/street, north, west/rear) and one party wall (south).

**This is an assumption, not a site fact, and must be verified before construction.** The realistic alternative — a true mid-row plot enclosed on both long sides — is common in dense 5-marla row schemes (see the separate party-wall reality check in Section 9/Output H, which flags the *opposite* default: zero side setback on both long faces is the typical row-house condition). If the plot is actually mid-row:
- The Section 5 chajja/solar-gain arithmetic would need to move to whichever face (east or west) is actually open, recalculated for that face's own angles — it does not transfer unmodified from the south-facing numbers below.
- The Section 6 cross-ventilation path collapses to **single-aspect ventilation**: one inlet (east) feeding the stairwell stack alone. The stairwell-as-chimney mechanism still works (buoyancy-driven, unaffected by which walls are party walls) — only the cross-flow portion is lost.

Every "primary strategy" and diagram below should be read with this assumption attached, with its fallback noted at the relevant point. **The single fact to hold onto: this document reads as if north, south, and east are all simultaneously available for windows — that is only true for a corner/side-open plot, and must be confirmed on survey before the design proceeds.**

### 3.1 Technique-by-technique evaluation for Rawalpindi's humid-subtropical climate

Rawalpindi/Islamabad's climate differs meaningfully from the hot-arid belt (Multan/Bahawalpur) that most classic passive-cooling literature targets: a real monsoon (July–September), higher relative humidity, cooler winters, lower peak dry-bulb temperatures. Each traditional technique is evaluated on that basis, not assumed:

| Technique | Physics | Appropriate for Rawalpindi? |
|---|---|---|
| **Courtyard** | Cool night air pools low; stack effect pulls warm air up and out; shaded floor is a cool-air reservoir | **Not achievable at true scale here** — plot cannot give the floor area/proportions needed; see the honest downgrade to a light/vent well below |
| **Light/vent well** (the achievable substitute) | Same stack-effect principle, scaled to a vertical shaft | **Primary strategy.** Realistic at 4–10 ft in width depending on which draft's arithmetic is used (see Output B/C reconciliation), width-to-height ratio well under 0.3 — a chimney, not a court |
| **Badgir/windcatcher** | Raised shaft catches wind at roof height, channels it down by dynamic pressure | **Secondary, opportunistic.** Rawalpindi's prevailing wind (N/SE, T1-U — see 3.0/6) is real but not as constant as the desert wind badgirs are tuned for. Folded into the mumty as a wind-assisted top vent, not a standalone tower |
| **Stack effect/high-level exhaust (roshandan)** | Hot air rises, exits above neutral pressure level; works with zero outdoor wind | **Primary mechanism, under either plot configuration in §3.0** — the stairwell itself is the main chimney regardless of which walls turn out to be party walls |
| **Jali (perforated screen)** | Diffuses direct solar radiation and glare; reduces free opening area | **Yes for privacy and solar diffusion — not asserted as a ventilation accelerator.** Shrinking free area can raise local velocity through remaining gaps but typically reduces *total volumetric* flow — net effect on room air-change is a wash at best. Used on street-facing openings, the light-well rooflight, and the mumty vent for privacy/glare, not as a flow-boosting device |
| **Chajja/deep reveals** | Horizontal projection blocks high summer sun, admits low winter sun | **Yes, essential — recalculated for this latitude, not copied from Lahore, and depends on the south face actually being open** (§3.0). Full arithmetic in Section 5 |
| **Shaded verandas** | Unconditioned buffer absorbs solar heat before it reaches habitable space | **Plot-constrained** — no room for full veranda depth on all sides; a shallow 3–4 ft covered entry porch on the east front is the realistic version, doubling as entry privacy |
| **Roof ventilation/double-roof** | Air gap lets solar-heated air escape by convection before conducting through the ceiling | **Correction from an earlier draft of this table: NOT the build-up actually used.** A ventilated air-gap ("cold") roof is the theoretically strongest single move in a dry climate, but Section 10 rejects it for Rawalpindi specifically — the humid monsoon condenses on the underside of an unventilated-feeling void's deck, trading a solar-gain problem for a rot/mould problem. **The highest-value roof move actually adopted here is the Inverted/Protected Membrane build-up in Section 10** (insulation above the membrane, reflective/light paver finish) — same solar-gain-blocking goal, without the condensation risk. Treat this row as a technique that loses to a same-climate alternative, not one that was implemented. |
| **Thermal mass** | Two distinct mechanisms — see note below | See note below |
| **Lime/cement plaster** | Affects thermal absorptivity and moisture behaviour | Cement plaster is the realistic default (durability, monsoon resistance); lime plaster a nice-to-have on south/west mass walls, not load-bearing |
| **Shaded/buffer walls** | Non-habitable buffer absorbs solar heat instead of a living space | **Yes, on the west face specifically** — holds regardless of §3.0's outcome, since west is buffer either way |
| **Vegetation/evaporative cooling** | Evaporation absorbs latent heat, cooling air | **Weaker here than Multan/Karachi** — loses effectiveness as humidity rises, and monsoon (when cooling is most wanted) is when humidity is highest. Potted vegetation in the light well for shading/aesthetics only |
| **Cross ventilation** | Low inlet on windward face, high/opposite outlet on leeward face | **Contingent on §3.0.** Uses north and east openings as drawn; collapses to single-aspect off the east frontage if mid-row |
| **Night flushing** | Full night opening purges the day's stored heat before it reradiates | **Yes — genuinely free, high-value.** Rawalpindi's summer nights cool appreciably, unlike Karachi's coastal humidity holding heat overnight. Works under either §3.0 configuration, through fewer openings in the mid-row fallback |

**Note on thermal mass — two mechanisms, not one:**
1. **Time-lag/decrement damping** (any thick masonry wall, any orientation) — delays and flattens conducted heat reaching the interior. Applies generally, including the west buffer wall.
2. **Direct interior solar-gain absorption** (specifically the south wall/floor receiving direct beam sun through south glazing in winter) — a different mechanism requiring direct-beam access to interior mass. Only works for the south wall/floor combination (Sections 4 and F), contingent on that face being open per §3.0.

## 4. Winter Heating / Solar Gain Strategy

*(Everything below assumes the south face is open per §3.0 — if the plot is mid-row with south as a party wall, this entire mechanism does not exist and must be re-derived for whichever face is actually open.)*

The house is designed around one clean distinction: **fixed geometry vs. occupant-operable control.**

**Fixed geometry** (cannot change once built): chajja depth over south windows, sized to block high summer sun while admitting low winter sun (Section 5 arithmetic); placement of the west buffer zone (stair/store/bath), a permanent decision independent of §3.0; wall mass and plaster finish, present on any exposed wall for the time-lag benefit, but the direct-gain benefit only on the south wall.

**Occupant-operable controls** (the seasonal switch the household throws): light-well rooflight and mumty vent — open/louvred in summer, closed/throttled in winter, stated explicitly to occupants, not left implicit; hinged/sliding jali panels rather than fixed perforated panels, to allow winter shut-down; south-facing curtains opened in winter daytime to maximize gain, drawn in summer afternoon if the chajja underperforms.

This design is tuned toward **more winter solar gain and a shallower overhang than a Lahore reference case would use** — a design decision calculated directly from the altitude figures in Section 5, not copied from an external table. The thermal-mass wall (9 in brick, cement-plastered) behind south glazing is the "winter heating system" of this house in the passive sense: direct winter sun strikes floor and lower wall, is absorbed, and releases slowly through the evening — a genuine no-cost heating contribution on clear days, with mechanical space heaters as occupant-controlled backup on overcast days only.

## 5. Sunlight Strategy — Solar Angles and the West-Wall Problem

Islamabad/Rawalpindi solar altitude at solar noon (33.7°N proxy):

| Condition | Solar altitude |
|---|---|
| Summer solstice | 79.7° |
| Equinox | 56.3° |
| Winter solstice | 32.9° |

**South-facing chajja sizing** (D = H/tan(altitude), H = 2.1 m window height, contingent on south being open per §3.0):
- Summer noon: D = 2.1/tan(79.7°) = **0.39 m (≈15.5 in)** — fully shades the window at the harshest sun angle of the year.
- Winter noon: the same 0.39 m overhang at 32.9° altitude drops a shadow of only ≈0.25 m down the window — **≈88% of the window still receives direct winter sun.** Full summer shade and near-full winter gain from one fixed chajja.

**The west-wall problem — no horizontal overhang solves this.** West exposure occurs at low altitude but large azimuth swing; using a representative afternoon altitude of 27°:

D = 2.1/tan(27°) = **4.1 m (13+ ft)** — not buildable on a 25 ft-wide plot, and essentially **latitude-independent** (driven by the low afternoon angle common to any west face, not this city's specific latitude). It also holds regardless of the §3.0 plot configuration, since west is buffer either way. The only real solutions:
1. No windows, or minimal high/small windows only, on the west wall (0–8% WWR target — the lowest of any orientation).
2. A solid buffer zone (stair, storage, bathroom) absorbing the west exposure instead of a habitable room.
3. Vertical fins or a jali screen, which block low-angle side-on sun far more effectively than a horizontal projection ever can.

This is why the floor plan (Output C) deliberately stacks the stair, store, and a bathroom against the west wall — a direct consequence of this arithmetic, independent of §3.0.

**Window-to-wall ratio targets by face** (assumes corner/side-open plot per §3.0):
- North 20–30% (safest face for larger glazing, if north is open)
- South 15–25% (upper end justified by the winter-gain arithmetic above, if south is open)
- East 8–12% (street frontage/entry — kept modest for privacy and morning-heat control, paired with the covered porch)
- West 0–8% (per the west-wall problem, unaffected by §3.0)

A separate reveal-based analysis (used in Output J's climate table) shows a 15 in deep window reveal only *fully* shades sun above ≈74.5° altitude, occurring within roughly ±1.5 hours of solar noon at summer solstice — at any lower angle (morning or afternoon, east or west) the same reveal gives **partial**, not full, shading. East and west are still handled differently not because reveals behave differently on the two facades (they don't), but because morning low sun on the east coincides with cooler ambient temperatures while afternoon low sun on the west coincides with the day's peak-heat hours — see Output J for the full reasoning.

## 6. Natural Ventilation Strategy

*(This entire section assumes the corner/side-open configuration from §3.0. If the plot is mid-row instead, only the stairwell-stack portion below still applies — see the single-aspect fallback in §3.0.)*

**Prevailing wind assumption (T1-U, unverified):** north and southeast — commonly cited descriptions instead describe a seasonal shift (northwesterly in winter, southeasterly in summer monsoon) rather than one constant direction, a further reason not to treat "north and SE" as settled. Pending real station data or a wind rose, this design assumes inlets on north and east/southeast faces, feeding the central shaft, exhaust at roof/mumty level.

**Complete airflow path, room by room:**
- **Low-level inlets:** cool air enters through operable windows on the north face (living/dining, ground floor) and east face (entry, kitchen) — the two faces with real frontage under the §3.0 assumption. Air also enters at low level into the light/vent well, where a small shaded/planted pocket keeps it slightly cooler.
- **Ground-floor cross-path:** air drawn at the north window moves across the open living/dining volume toward the stair core — no partition walls interrupt this path.
- **Vertical draw — the stairwell as chimney:** air is pulled upward by stack effect at the stair base. The stairwell is a partially open shaft (not sealed by solid doors at every level), functioning as a continuous exhaust chimney ground floor to roof. **This is the primary ventilation mechanism, and the one part of this section that holds under either §3.0 configuration** — it works with zero outdoor wind and even under the mid-row fallback.
- **First-floor path:** air rising through the stair core is joined by air through roshandans (2 ft × 1 ft 6 in) above door heads between bedrooms and the central circulation space — bedroom air participates in the stack flow at night without doors standing open.
- **Light/vent well as a secondary buoyancy shaft:** pulls air upward from its ground-floor opening past first-floor windows facing it, out through a louvred, openable rooflight — never sealed, even above an internal bathroom, because a sealed well over a wet-area shaft becomes a moisture/odour trap.
- **High-level exhaust — the mumty:** both the stairwell and light well terminate near the mumty, fitted with a high-level louvred vent oriented to catch the prevailing wind — a simplified badgir-principle device without a standalone tower's cost.
- **Outlet-to-inlet ratio:** free area at high-level exhausts (mumty vent + light-well rooflight + roshandans) sized at **1.25:1 to 1.5:1** relative to low-level inlet area — a bottlenecked exhaust chokes the whole stack flow regardless of inlet generosity.

**With little or no outdoor wind:** the stairwell stack continues on solar heating of the mumty and roof alone — sufficient to sustain a slow continuous draw even in still conditions. This is why the stairwell (always active) is primary and the wind-assisted mumty vent is secondary/opportunistic.

**Winter shut-down:** the same high-level vents become a heat-loss liability in winter — mumty louvres and light-well rooflight throttled/closed, roshandans fitted with sliding covers, converting the house to a closed winter mode so the thermal-mass south wall and controlled solar gain (Section 4) can do their work without being undercut by continuous stack-driven heat loss.

## 7. Structural Engineering Concept

**Everything below is conceptual/preliminary.** No dimension, load, or material spec is a substitute for a site-specific geotechnical investigation, a confirmed seismic-zone determination, or a design stamped by a PEC-registered structural engineer.

**Area-figure discipline:** this section distinguishes **plot area** (1,125 sq ft ≈ 104.5 m², the legal parcel) from **covered footprint** (actual built-up ground-floor area after byelaw setbacks — realistically **~800–1,000 sq ft ≈ 74–93 m²**, matching the setback-bound figure derived in Output C). Every floor-area-dependent calculation below uses the covered-footprint range, not the plot area, and is flagged illustrative until checked against the final architectural plan.

**7.1 System choice: Confined Masonry (CM), not RCC frame, not URM.** Running the plot through `architecture-structural-systems`'s decision tree — no open span near 5 m, G+1 only, no basement, no floating columns — none of the hard triggers forcing an RCC frame apply. Do not propose URM in Zone 2B/3/4 (Rawalpindi is one of those zones, see 7.2), which leaves CM as the recommended default: **1.10–1.20× the URM baseline cost vs. 1.30–1.55× for a full RCC frame**; more forgiving of average site supervision than RCC; load-bearing masonry gives the thermal mass the climate strategy (Sections 3–4, Output J) depends on; max height for CM is 3 storeys, comfortably covering G+1. Caveat: the light-well/stairwell diaphragm opening (7.4/Section 8.5) must pass the wall-density check below before this pick is final.

**7.2 The seismic zone problem — stated honestly.** The structural-systems and geotechnical skill references list Rawalpindi/Islamabad as **Zone 2B**; the seismic-design skill's own city table instead lists **Zone 3**, while explicitly flagging that some official BCP SP-2007 sources place this city pair at 2B and instructing not to trust either table blindly — pull the actual zone from the current BCP SP-2007 map/RDA submission form, and design one zone higher if near Margalla/MBT-MFT fault structures. **This document's resolution:** illustrated using the higher, more conservative Zone 3 requirement where the two conflict (per the seismic skill's own risk-averse instruction not to guess downward), with Zone 2B as the commonly-cited alternate — this is a deliberate erring-safe choice, not a substitute for the real answer required before construction.

**7.3 Baseline preliminary member sizes** (CM, ≤4.5 m spans, Zone ~2B–3 — starting sizes for the engineer to verify):

| Element | Preliminary size |
|---|---|
| Structural (external) wall | 230mm (9") |
| Partition wall | 115mm (4.5") |
| Tie-columns | 230×230mm at every corner, wall junction, free end, opening jamb >1.2m; spaced ≤4.0m (the flat limit governs over 1.5× storey height at this 3200mm storey) |
| Tie-beams | 230×230mm, continuous ring at every floor and roof |
| Slab | 125mm (5") two-way solid; step to 150mm (6") beyond 4.3m span |
| Lintels | 150–230mm deep, 230mm bearing each side |
| Plinth beam | 230×230mm on every wall line — mandatory in Zone 2B+ |
| Strip footing | 600mm wide × 300mm thick, founded 1.2–1.5m below NGL (width subject to real soil bearing, see 7.6) |
| Floor-to-floor height | 3200mm (10'-6"), 2750mm clear ceiling |

Tie-columns get 4 bars of 12mm diameter with 10mm ties at 150mm centres (100mm near joints); walls built first with toothed edges, tie-columns cast into the pocket afterward ("wall-first-then-confinement") — getting this sequence backward defeats the confinement mechanism. Mortar ≥1:6, tightened to 1:4 at ground storey if Zone 3 confirmed. **No mud mortar anywhere, in any zone.** Any open RC-frame bay (e.g. the car-porch edge) needs its own sizing: columns ≈300×300mm at ≤12 m² tributary area, beams ≈230×300mm at 3.0–4.5m spans, still tied into the CM ring — not a structurally isolated insert.

**7.4 The wall-density check — governs whether the light-well works.** `d = Σ(wall cross-section area in direction) / floor area`, checked at ground storey. Required minimum 2.5% (Zone 2B) to 3.5% (Zone 3). Against the corrected 74–93 m² covered footprint: Zone 3 needs **2.6–3.3 m²** (≈11.3–14.2 linear m of 230mm wall per direction); Zone 2B needs **1.9–2.3 m²** (≈8.0–10.1 linear m). Both the zone uncertainty (7.2) and footprint uncertainty compound here — this is illustrative order-of-magnitude only, not a validated pass/fail.

**Where this fails on this specific plan:** the parking opening and the light-well cut are precisely the geometry that most commonly drops effective wall length below the requirement in one direction, driving torsional response under seismic load. **Fixes, in order:** (1) short return walls (1.5–2.0m) at the parking-bay ends; (2) convert the open bay to an RC shear wall/moment-frame line; (3) move the open feature to the upper floor; (4) reduce opening width and add a tie column; (5) document as an exception for the structural engineer's real lateral analysis. **This check has not been run against the actual floor plan in Output C** — presented here as method and illustrative range only; running it against the real, setback-corrected layout is a required next step. First-floor footprint is not assumed identical to ground floor without saying so — if they differ, recompute separately (feeds directly into the 70% ratio check in Section 8.3).

**7.5 Base shear order of magnitude:** roughly **12–20% of building weight**, applied horizontally, independently in each direction — the house must resist a sideways shove equal to a fifth to a sixth of its own weight at every floor. This is why wall density, tie-beam continuity, and avoiding soft storeys aren't cosmetic.

**7.6 Foundation concept:** strip footings under CM wall lines (not isolated pads — CM transmits continuous line load). Presumptive bearing capacity for the Rawalpindi/Potohar plateau: stiff residual clay over Murree Formation shale, **150–250 kPa** at 1.2–1.5m depth; shattered rock/hard shale, **440–880 kPa**. **Complication: Potohar loess pockets are collapsible-on-wetting** — adequate dry, loses bearing capacity when saturated (real risk given monsoon behaviour, Section 10/Output J). A soaked oedometer test is required to rule this in or out before footing sizes are finalized. Indicative footing width ≈0.60m at SBC ≥150 kPa, widening to 0.75–1.35m toward 50 kPa — over 2× swing depending on which end of the presumptive range the real soil falls in. Founding depth 1.2–1.5m, and specifically below any identified collapsible loess layer.

**7.7 Structural cost/quantity sanity check** (cross-reference Output K): CM structural cost ≈25–40% of total house cost; concrete ≈0.18–0.25 m³/m² covered area; reinforcement steel for CM (tie-columns/beams only, not a full RC frame) ≈**12–20 kg/m²** — a directionally-corrected illustrative figure needing verification against a real bar-bending schedule before use in a BOQ conversation.

**Three tiers of confidence** (repeated for clarity): (1) **conceptual recommendations** safe to plan around — CM as the system, tie-column philosophy, avoiding soft storeys/short columns, a small double-ringed light-well; (2) **preliminary assumptions** needing site data — member sizes above, bearing capacity, footing widths, base shear estimate, steel-quantity placeholder; (3) **requires real engineering, no exceptions** — the actual wall-density and 70%-ratio checks against final setback-corrected floor plans, real footing sizing from soil test results, the real seismic zone off the current BCP SP-2007 map, full lateral analysis of the light-well/stairwell diaphragm condition.

## 8. Earthquake / Seismic Considerations

**8.1 Regular geometry as the first line of defense.** This plot's aspect ratio, 25×45 ft ≈ 1:1.8, passes `architecture-seismic-design`'s target of ≤2:1. A more elongated or L-shaped plan would need seismic separation into distinct blocks — this plot doesn't need that, and the design should not introduce it by carving an L-shape or deep notch for aesthetic reasons alone.

**8.2 Column/tie-beam continuity and load path.** Every tie-column must land on a footing via the plinth beam and connect continuously through every tie-beam ring to the roof-level ring beam — a broken load path anywhere concentrates seismic force at the break. The same wall/column grid should repeat at both storeys; shifting a wall position between floors creates a **vertical irregularity** treated as a serious defect, not a minor tweak.

**8.3 Avoiding soft/weak storeys — the parking-opening risk, named explicitly.** The single-car parking opening is the classic soft-storey trigger: a ground floor with less wall stiffness than the floor above concentrates seismic drift and damage at that storey — responsible for a large share of masonry-building collapses region-wide in real earthquakes. Numeric guard: **ground-storey wall length must not drop below 70% of upper-storey wall length**, in either direction — a distinct check from the wall-density check in 7.4 (that's absolute area vs. floor area; this is ground vs. first floor relative to each other). Both must pass. **This ratio check assumes ground- and first-floor footprints/wall layouts are actually comparable — not yet verified here.** If the first floor differs (upper-storey setback, terrace, cantilever), recompute against the real first-floor wall lengths. If the parking bay pushes ground-storey wall length below 70%, the fixes are the same list as 7.4.

**8.4 Short-column effect around the light-well.** If the light-well/vent-shaft design includes any partial-height parapet or sill wall around its edge, that wall can inadvertently brace a column over only part of its height, stiffening that short segment far more than the rest — under shaking, the stiffened segment attracts disproportionate lateral force and can fail in shear before the rest of the structure engages. Any parapet around the light-well opening must be structurally isolated from the adjacent column (a gap, not a bonded joint), or the column must be designed for the full short-column shear demand — flagged explicitly to the structural engineer, not assumed fine.

**8.5 Diaphragm-opening irregularity — the light-well's real seismic classification.** A courtyard/light-well/vent-shaft cut into a floor plate is a **diaphragm opening** — it weakens the floor/roof's rigid-diaphragm role exactly where the hole is. Per ASCE 7-22 Table 12.3-1 (referenced by `architecture-seismic-design`), a cutout **greater than 50% of the gross enclosed diaphragm area** is an extreme diaphragm-opening irregularity triggering more demanding analysis. The seismic-design skill treats courtyard/light-well houses as a **ring-diaphragm case**: instead of one continuous slab tied by one perimeter tie-beam ring, this house effectively has two concentric rings — the outer building perimeter and the inner light-well edge — each needing its own continuous tie-beam ring, plus trimming beams and chord (edge) reinforcement around the opening.

**What this means for this brief:** the light-well/vent-shaft must stay genuinely small — comfortably under the 50% threshold, with a working target well below that (a small fraction of the ~74–93 m² covered footprint, given how little floor area this plot has to spare). This document specifies: a **double tie-beam ring** (outer perimeter 230×230mm plus a second, separate ring at the light-well's inner edge, at every floor and roof level); trimming beams and additional chord steel at the light-well opening corners; and the stairwell, where it doubles as ventilation chimney, enclosed within confined-masonry stairwell walls where possible so those walls contribute to the lateral force-resisting system rather than being a second, separate diaphragm penetration — where the stair flight can't be fully enclosed, it must still be positively tied into the surrounding structure at both ends.

**8.6 Roof-to-wall connection.** The roof-level tie-beam ring is the connection most exposed to whip/uplift forces during shaking (furthest from ground, moving most under lateral acceleration) and most often shortchanged on site (last pour before finishing). Same 230×230mm spec and continuity requirement as every other level — no gaps at parapet corners, no skipping the ring over the light-well edge.

**Reality Check for this section:** a PEC-registered structural engineer must review the actual seismic zone, confirm the actual covered footprint after setbacks for both storeys, run the actual wall-density and soft-storey checks against the final architectural plan, commission a real geotechnical investigation, and stamp final structural drawings before any footing is excavated.

## 9. Thermal Envelope — Assembly Options Compared

**Party-wall reality check — resolve this before any façade design below is treated as final.** A 25×45 ft (5-marla) plot is the standard row-house lot size in Rawalpindi housing schemes, and the **default condition on that plot size is zero side setback** — the two long (45 ft) faces are shared party walls with neighbouring plots. This document has been given only an "east-open" assumption and, per Section 3.0, has additionally assumed south alone is the party wall (a corner/side-open condition) to make the ventilation and solar-gain strategies work. **These two framings must be reconciled against the actual approved site plan for this specific plot before construction drawings are finalised:**
- If a side is a legal party wall: no windows, chajjas, or jaali are permitted on that face — the daylighting/passive-solar strategies described for it are void, and it reverts to a plain 230mm brick structural wall, sized only for load-bearing and fire-separation.
- If a side does carry a setback (confirm against the approved site plan / RDA byelaw), the strategies in Sections 3–6 and Output D/E/F/H apply as written.
- **Action required before construction drawings are finalised:** confirm setback status for north and south against the approved site plan for this specific plot.

**Comparison table (conceptual, per m² of finished wall):**

| Property | 230mm burnt clay brick | 200mm solid concrete block | 200mm hollow concrete block | 200mm AAC block |
|---|---|---|---|---|
| Unit compressive strength | 7–14 N/mm² (design at f'b=7 unless lab-proven) | 4–8 N/mm² | 3.5–5 N/mm² (Grade B) | 3–5 N/mm² (min 3.0, Grade 1) |
| Thermal conductivity (λ) | ≈0.81 W/m·K | ≈1.0 W/m·K | lower than solid, but ungrouted cells short-circuit thermally | ≈0.16 W/m·K — **~5× better insulator than brick** |
| Dry density | 1,900–2,000 kg/m³ | — | — | 550–650 kg/m³ (~⅓ of brick) |
| Wall self-weight | ≈4.9 kN/m² | ≈4.4 kN/m² | ≈3.3 kN/m² (only if grouted/reinforced) | ≈1.7 kN/m² |
| Load-bearing role (G+1) | Yes — default, CM | Yes, with full seismic banding | Only if cells grouted + reinforced | No by default — infill only, unless engineered for load-bearing |
| Mason familiarity | Universal | High | Moderate | Low-to-moderate |
| Local supply | Universal | Widely cast locally | Widely cast locally | Plant/stockist-dependent — verify before specifying |
| Wet-area suitability | Good | Good | Fair | Poor unless fully tanked |
| Special handling | Soak before laying | Age 28 days; do not soak, surface-dampen only | Same as solid block | Do not soak — light misting only; thin-bed polymer adhesive (2–4mm joint) |

**Governing thermal number, humidity-qualified:** brick's λ≈0.81 vs. AAC's λ≈0.16 is a ~5× conductivity difference, and with no separate insulation layer budgeted into the wall, the block choice is doing the thermal-envelope work an insulation layer would do elsewhere. But Rawalpindi/Islamabad is humid-subtropical, not hot-dry Punjab: smaller diurnal swing means less benefit from mass buffering overnight, and monsoon humidity (RH 70–90%, June–Sept) means vapour-permeability matters as much as raw λ. AAC is more vapour-open than dense brick but far more capillary-absorptive if the external render is breached — the cement plaster over SBR bonding slurry specified below is the monsoon moisture-management layer for this wall type, not just a bonding requirement, and should not be value-engineered down to a thinner coat. The conductivity advantage is a real, smaller (not hot-dry-climate-maximum) net comfort win here, most valuable on the west face during the hot pre-monsoon (May–June) window.

**AAC's structural side-benefit (worked, preliminary):** swapping 200mm AAC for 230mm brick saves ≈3.2 kN/m² of wall self-weight per face. At ≈260 m² of total wall area [conceptual estimate], applied uniformly (not the actual recommendation) that is ≈832 kN ≈ **85 tonnes** of dead load removed — proportionally less seismic base shear too (mass-driven), a real benefit on top of the thermal gain, though not a reason to use AAC everywhere.

**Four-point Pakistan supply-reality checklist for AAC (all four must be YES, or default to brick):** (1) AAC plant/authorized stockist within economical haulage distance; (2) thin-bed polymer adhesive actually available locally; (3) mason crew has prior AAC experience; (4) gypsum plaster or SBR/acrylic bonding agent available locally. If any answer is NO, build the whole house in confined brick masonry — a badly-detailed AAC wall loses most of its thermal advantage and gains a cracking problem.

**Recommendation for this house** (pending the checklist above AND the party-wall confirmation): ground-storey structural walls **230mm burnt clay brick, confined masonry**, 1:4 mortar; first-floor non-structural infill, specifically the west-facing bay **if confirmed genuinely openable**, **200mm AAC block** with thin-bed adhesive and SBR-bonded cement plaster externally / gypsum internally, only if the checklist passes; wet-area walls **115mm brick** regardless of what's chosen elsewhere (AAC's capillary suction is a poor fit next to plumbing); internal partitions **115mm brick or 100mm AAC**, whichever the confirmed crew is faster/more confident with; any confirmed party wall reverts to plain 230mm confined brick, no openings.

**Seismic zoning, made internally consistent with Section 7/8:** Rawalpindi/Islamabad is conventionally **Zone 2B** under BCP-SP 2007 for the purposes of this envelope's mortar table (a single, consistent zone basis for the envelope decisions below — note Section 7.2 illustrates member sizing conservatively against Zone 3 where the two references disagree; both should be reconciled once the real zone is confirmed).

**Mortar summary (single Zone 2B basis):**

| Location | Mix | Strength | Why |
|---|---|---|---|
| Ground-storey load-bearing, plinth, soil contact | 1:4 | 7.5–10 N/mm² | Zone 2B confined-masonry minimum, ground storey |
| First-floor load-bearing/general 230mm walls | 1:5 | 5–7.5 N/mm² | Upper-storey default |
| Internal non-load-bearing/upper partitions | 1:6 | 3–5 N/mm² | Minimum acceptable — never weaker |
| Anything weaker (1:8, mud, cement-free) | **Prohibited** | — | Not usable in Zone 2B+ |

Governing principle: mortar must always be *weaker* than the unit, so future cracking runs along the repairable joint, not through the unit.

## 10. Roof Design as a Passive Climate System

**10.1 Roof type decision.** Flat, accessible RCC roof, not pitched. Rawalpindi's climate does not cross the thresholds (heavy snow, extreme monsoon intensity) that would force a pitched roof, and the brief wants a *usable* roof: drying, an OHT, solar panels, a pergola-shaded sitting area, and the mumty — all needing a walkable flat surface. A pitched roof would forfeit every one of these for a marginal water-shedding benefit this climate doesn't demand.

**10.2 Roof build-up — Inverted/Protected Membrane Roof (IRMA/PMR):** insulation above the waterproofing membrane, protected by a screed/paver layer — the correct hot-climate choice because it roughly doubles membrane service life (shielded from UV and daily thermal cycling; unprotected bitumen can swing 40–50°C/day in Rawalpindi summer sun, buried under insulation+screed it barely moves).

Bottom to top: (1) **RCC structural slab**, 125–150mm (conceptual, span-dependent, see Section 7); (2) **screed to falls**, design fall **1:40 (25mm/m)** — stricter than the commonly-quoted 1:50, because ordinary site screeding tolerance (±10–15mm) can flatten 1:50 to near-zero in patches; (3) **waterproofing membrane**, 2-ply modified bitumen or single-ply APP, turned up ≥150mm at every parapet/upstand; (4) **XPS insulation, 50–75mm** — specifically extruded (not EPS/PIR), because this layer sits in a wet exposed position and XPS is closed-cell; (5) **filter fabric + protection/paver layer**, precast pavers on pedestals or a high-albedo tile finish, min 40–50mm, taking all foot traffic so the membrane/insulation are never walked on directly.

**Dead-load arithmetic, shown layer by layer:**

| Layer | Basis | Load |
|---|---|---|
| Screed to falls | 40–100mm avg × ~20–21 kN/m³ | ≈0.8–2.1 kN/m² |
| Waterproofing membrane | 2-ply modified bitumen | ≈0.05 kN/m² |
| XPS insulation, 50–75mm | ~30–40 kg/m³ | ≈<0.05 kN/m² |
| Paver/tile protection, 40–50mm | ~24 kN/m³ precast | ≈1.0–1.2 kN/m² |
| **Total added dead load** | | **≈2.0–3.5 kN/m²** |

This ≈2.0–3.5 kN/m² is the figure that must be carried into slab/beam design (Section 7) as additional superimposed dead load. Total build-up ≈300–500mm from slab top to finished walking surface. **Reflective finish:** the top layer should be light-coloured (white/light grey/light ceramic), the single cheapest roof passive-cooling move available (Output K rates it low-cost/high-benefit) because it directly cuts solar heat load hitting the insulation.

**A traditional brick-bat coba build-up** (75–115mm broken-brick bedding, 1:50 falls over a torch-on membrane) is a valid, more locally-repairable alternative, but heavier (≈1.8–2.3 kN/m² for that layer alone) and must be carried in the structural load case from day one if chosen instead. **Cold-roof construction (insulation at ceiling only, ventilated void above) is explicitly not recommended** — in a humid-subtropical climate an unventilated cold-roof void condenses on the deck's underside, a maintenance problem this house does not need.

**10.3 Roof drainage.** Never a single outlet, on redundancy grounds alone regardless of capacity math. A 100mm downpipe's typical full-bore discharge capacity is **4–6 L/s**; at 76mm/hr rainfall intensity (≈0.0211 L/m²/s), area drained ≈4–6 ÷ 0.0211 ≈ **190–285 m²** per outlet (call it ≈200 m² working figure). This house's roof (≈93–98 m² after the light-well cut) is well under what even one outlet could carry by capacity — **the case for multiple outlets is entirely redundancy** (a blocked downpipe is a real, frequent maintenance event, not an edge case): minimum **2 outlets** at opposite low corners, 3 more comfortable if the plan allows.

**Design rainfall intensity:** 75–100mm/hr taken conceptually for the outlet-count logic, but this bracket is not already conservative — the 23 July 2001 Islamabad/Rawalpindi flash flood recorded ≈620mm in ≈10 hours, with short-burst intensities far exceeding this design bracket. Flag to the civil engineer: a parapet-top overflow scupper (secondary, unplumbed emergency outlet) as a low-cost safeguard against a repeat of a 2001-scale event, pending PMD/WASA historical-extreme data for this site.

**10.4 Roof zoning — every rooftop object is a designed patch load, not free space.** **OHT zone:** a standard 1,000-imperial-gallon tank holds 4,546 L = 4.55 tonnes = 44.6 kN on a ≈2.16 m² stand footprint — a **20.6 kN/m² patch load**, against a typical roof live-load design of only 1.5–2.0 kN/m² — **10–14× the load the bare slab was designed for at that spot** if not specifically accounted for. Locate the OHT stand directly above a column, on a short RCC plinth transferring load straight down the column line, and flag this to the structural engineer as a fixed input, not a "wherever's convenient" terrace decision. **Solar PV zone:** lightweight (12–20 kg/m² incl. racking/ballast), can sit on general slab away from beam lines, south-facing at roughly local-latitude tilt, walking clearance maintained for cleaning (dust is a real Rawalpindi issue — see Output J). **Solar geyser zone:** similar light load, close to the bathroom/kitchen wet stack below for short pipe runs. **Split-AC condensers:** each 50–120 kg point load, on 25mm neoprene isolators, minimum 150mm clear of any beam/column face. **Mumty + pergola zone:** the stairwell's roof exit is a small enclosed structure at roof level (also the top of the ventilation chimney, Section 6/Output E); a light bamboo/timber/steel pergola gives shaded seating without a full green roof (not recommended here — added dead load, waterproofing risk, and irrigation demand disproportionate to the benefit on this budget). **Parapet + jali zone:** see Section 12 — also the primary privacy device on this roof.

**10.5 Maintenance access.** The stairwell continues straight to roof level (no separate ladder/hatch) so the OHT float valve, PV panels, and geyser are all reachable — dust accumulation is a real, frequent Rawalpindi maintenance item, and an access route requiring a ladder gets skipped in practice.

## 11. Interior Floor Plan

The full room-by-room layout, approximate dimensions, and the area-budget arithmetic proving this brief fits the real 1,125 sq ft / 5-marla envelope are given in **Output C — Floor Plan** below (this is where the load-bearing detail lives; this section exists only as the numbered-brief placeholder the sections above point back to).

## 12. Privacy

The core tension — privacy without sacrificing ventilation or daylight — is resolved the way traditional courtyard houses resolved it: **screen the view, not the air.** A jali or high-level window blocks sightlines while passing airflow and diffuse daylight; a solid wall blocks all three at once. Every device below is chosen because it keeps at least one of ventilation/daylight working while it blocks sightline.

**Street privacy (ground floor, public side):** boundary wall at the front setback with a solid lower zone (~1.2–1.5m, conceptual, subject to the development authority's height limit) and a **jali/pierced-screen upper zone** above — keeps street-lived-on visibility (safety) while screening the ground-floor window sightline. Street-facing windows get a deep reveal (Section 5/9) and, where they face directly onto a footpath, a fixed external jali panel rather than plain clear glazing. **Entry sequence:** door → small entry lobby/foyer (not directly into the living room) → living area — a visitor never has a direct sightline into family space, at almost no extra area cost (captured from circulation space already needed for the stair/hallway).

**Gender-zoned/guest-vs-family separation:** on a 5-marla plot there is not enough area to fully separate a formal male-guest zone from family space — stated honestly rather than pretended away. The achievable compromise: living/drawing room nearest the entry, kitchen/family sitting/all bedrooms on the far side of the circulation spine, upstairs and toward the back. Partial zoning, not full — a real constraint of plot size, not a design failure.

**Bedroom and bathroom privacy:** bedrooms on the first floor only wherever the plan allows — vertical separation is the single strongest, essentially free privacy move once the stair location is fixed. All bathroom windows are **high-level** (sill ≈1.8m+ off finished floor), standard Pakistani practice because side setbacks on a 5-marla plot are narrow (often under 5 ft) and a standard-height window would face almost directly into the neighbour's equivalent window — still gets stack-effect exhaust without the sightline problem. Where a window faces the light-well rather than a neighbour, a fixed jali or frosted/textured panel is used instead of clear glass, since the light-well is shared visual space between floors and rooms.

**Light-well/internal-courtyard privacy:** surrounded on 3–4 sides by the house's own rooms rather than street or neighbour, the light well is inherently the most private outdoor-feeling space in the house — mirroring the traditional courtyard-house logic of turning "open" family life inward. Rooms facing the light-well use ordinary clear glazing and full-height openings without a privacy penalty, which is also where most of the daylight and cross-ventilation strategy is concentrated.

**Roof/terrace privacy:** parapet **1.0–1.1m solid**, with jali/pierced-screen infill above to a comfortable eye-blocking height (≈1.5–1.65m total) on sides facing directly into a neighbour's upper-floor windows/roof. **Flag:** parapet out-of-plane seismic capacity (a cantilevered, top-heavy element and known earthquake failure mode — see Section 8) must be verified by the structural engineer, not assumed adequate from a privacy-driven height decision alone.

**What was deliberately not attempted:** a full physical courtyard with true four-sided privacy is not achievable on this footprint once G+1, parking, and circulation are accounted for — flagged honestly in Sections 1–2 and Output C. The light-well delivers most of the *privacy* benefit of a courtyard even though it can't deliver the full daylight/ventilation volume a true courtyard would.

## 13. Water and Energy

**Water supply and storage:** design demand 135–200 L/person/day (family of 5–6 ≈ 675–1,200 L/day). **OHT** sized at ≈1/3–1/2 of one day's demand by ratio (~500–600L), but the practical market minimum is the standard **1,000-imperial-gallon (4,546L) tank** — used here, both because it's what suppliers stock/plumb for and because it buffers Rawalpindi's frequent municipal supply interruptions. Its 20.6 kN/m² patch load (Section 10.4) is the largest single structural/roof coordination point in the house — repeated here because it's easy to treat as "just plumbing" when it's really a structural decision. **Underground/ground-level storage tank** feeding a pump to the OHT, sized ≈1,000–1,200L, recommended given supply variability.

**Rainwater harvesting:** roof rainwater, via the 2–3 downpipes sized in Section 10.3, routed through a first-flush diverter to the underground tank (non-potable uses) or a soak pit for groundwater recharge. **Septic/soak-pit reality check:** standard on-site septic setbacks (15m from any well, 3m from foundations, 5m from plot boundary, 8m from large trees) are essentially impossible on a 7.6m×13.7m plot — stated plainly rather than drawing a septic system that doesn't fit. **Assume connection to the municipal sewer**, standard for urban Rawalpindi plots this size; any on-site pit is limited to a small rainwater soak pit for stormwater only, sited as far from foundations as the plot allows, flagged for WASA/TMA drainage-authority input.

**Greywater reuse:** full treatment/reuse plumbing is a stretch on this budget/area — nice-to-have, not core. The one low-cost move worth including: route washing-machine and one bathroom's greywater through a basic sand/gravel filter box to the garden/plant strip along the light-well or front setback, for free irrigation water, without a dual-plumbing system throughout.

**Low-flow fixtures:** dual-flush WC cisterns (4.5L/3L or 6L single-flush vs. older 9–13L), low-flow shower heads, aerator taps — readily available at normal cost premiums, the single cheapest water-saving line item in the whole brief.

**Solar energy:** roof-mounted PV per Section 10.4, sized conceptually for baseline loads (lighting, fans, fridge, TV, routers) plus a share of daytime AC backup — exact kW needs a real load audit, flagged preliminary. Solar water heater, roof-mounted, covers hot water for most of the year with electric backup on cloudy winter days — a strong fit for Rawalpindi's clear-sky-dominant climate, directly reducing one of the largest year-round electricity loads (electric geysers are a heavy winter draw).

**Lighting and mechanical backup, in priority order:** (1) daylight first — the light-well and window placements from Sections 5/6/11 are the real first line of "lighting strategy"; (2) LED throughout, non-negotiable baseline; (3) ceiling fans as the primary cooling appliance in every room, pairing with the cross-ventilation strategy — open windows + fan on breezy days; (4) high-efficiency split AC as backup only (bedrooms primarily, sized to the smallest capacity that covers the room, used only when passive strategies aren't enough — a minority of summer nights per Section 6, not the default).

**Net picture:** the passive building (Sections 3–10) does most of the thermal work for free; the active systems here (PV, solar geyser, fans-before-AC, low-flow fixtures) are sized to *support* that baseline, not compensate for a leaky, unshaded building. A well-executed passive envelope with modest PV and a solar geyser can plausibly cut the electricity bill by a large fraction versus an unshaded box running AC as default — but that claim needs a real load calculation against actual tariff/usage data before it's quoted as a number to a client, not asserted here as measured fact.

---

# Part II — Output Sections A–K

## A. Design Concept

### A.1 Orientation assumption

This design takes an **east-open** 25 ft × 45 ft plot as the primary design case: road and main entrance on the east 25 ft frontage, 45 ft depth running north–south. This is stated as an assumption, not a fact about the actual site — confirm the real road-facing edge before use. A.5 below gives adaptation notes for north-, south-, and west-open variants.

### A.2 Plot verification

25 ft × 45 ft = 1,125 sq ft matches **5 marla on the 225 sq ft/marla basis** exactly (`architecture-spatial-planning` §1.2). Rawalpindi sits adjacent to Islamabad, where the standard basis is 272.25 sq ft — confirm the deed basis before proceeding; do not assume.

### A.3 Why not a plain rectangular box

At 25 ft frontage, two 9 in perimeter walls consume 1.5 ft, leaving **23.5 ft of internal clear width** — enough for one 12–14 ft room, a 4 ft passage, and a 5 ft bath side by side, and nothing more. The plan-archetype decision tree and the frontage lookup table both land on **Linear/Side-Passage** as the only supportable archetype. A true central-courtyard or U-shaped plan needs roughly 10+ ft of spare plan width beyond the room budget — this plot has none.

The honest, physically real move: **fuse the light/vent well with the staircase void into a single vertical ventilation shaft**, sized as a light-and-vent well (6×8 ft to 8×10 ft) rather than dressed up as a courtyard it structurally cannot be. This shaft lights the two blind middle rooms of the linear plan, draws cool air in low and vents hot air high, and houses the stair — no separate volume spent on vertical circulation. Per plan-archetype guidance, a light shaft earns its cost precisely at the weakest-daylight point of a linear plan, exactly where it sits here: the mid-plan boundary between entry/living and rear bedroom zones.

### A.4 Design priorities, in order

1. Get the long 45 ft walls facing north and south, short 25 ft walls (east entrance, west rear) absorbing sun — free on the east-open case, a consequence of the plot's own proportions.
2. Treat the stair and light/vent well as one shared passive-cooling device, not two separate problems.
3. Push every low-occupancy or heat-tolerant room (stair, bath, store, rear wall generally) onto the harder facades so bedrooms and living space get the good ones.
4. Lead with traditional passive devices (jali, deep reveals, chajjas, roshandans) as the primary climate strategy — mechanical cooling is occupant-controllable supplementary capacity, not the default.

### A.5 Adaptation notes — other orientations of the same 25×45 rectangle

- **West-open (hardest case):** frontage still the 25 ft edge, long walls still N/S. Entrance now sits on the worst-sun facade — mitigate with a deep-set entrance behind a verandah/jali screen, zero bedroom/living glazing on the west wall, entry foyer as the thermal buffer.
- **North-open:** frontage moves to the north 25 ft edge, flipping the 45 ft depth to run E-W — long walls now face **east and west**, the less favorable alignment. Mitigate by minimizing glazing on both long walls, stacking stair/bath/store along the west long wall, vertical fins/jali (not horizontal chajjas — don't work on E/W) on the east long wall. The entrance itself is favorable — one of the most planning-friendly orientations available.
- **South-open:** same E/W long-wall exposure problem as north-open, but the entrance facade (south) is the easiest of all four to shade with a simple 12 in chajja, doubling as the living room's facade — partially offsetting the long-wall penalty.

### A.6 Why east-open was chosen as primary

On this specific geometry, east-open is the only one of the four orientations that gets the favorable long-wall alignment *and* keeps the entrance off the hardest facade (west) *and* leaves the easiest-to-shade facade (south, or close to it) available for living space. That combination doesn't hold for north-, south-, or west-open — each trades away at least one of the three.

---

## B. Site Strategy

### B.1 Plot and orientation

- **Plot:** 25 ft (frontage) × 45 ft (depth) = 1,125 sq ft = 5 marla, 225 sq ft/marla basis (confirm against the actual deed).
- **Orientation (assumed, primary case):** east-open, corner/side-open (see §3.0) — long facades north and south, favorable alignment "for free."

### B.2 Labeled site plan (plan view, north up, ASCII)

```
                       NORTH  (45 ft long wall — bedroom zone, minimal glazing on this
                               wall's western portion; buffer rooms tucked into NW corner)
        ┌───────────────────────────────────────────────────────┐
        │  [stair / store / bath cluster — rear buffer, NW]     │
        │                                                        │
        │        ┌───────────────────────┐                      │
   W    │        │ LIGHT + VENT WELL     │                      │    E   <- ROAD
 (rear, │        │  6-8 ft x 8-10 ft,    │                      │        FRONTAGE
 buffer │        │  fused with stair     │                      │        (25 ft)
  wall, │        │  void = combined      │                      │        ENTRANCE
  no    │        │  stack-effect shaft   │                      │        + PORCH
 horiz. │        └───────────────────────┘                      │        HERE
overhang│                                                        │
 works) │  [living / kitchen zone — south wall, shallow chajja] │
        └───────────────────────────────────────────────────────┘
                       SOUTH  (45 ft long wall — living zone, 12-24 in chajja
                               handles this wall's sun load year-round;
                               ASSUMED PARTY WALL under the corner/side-open
                               reading in §3.0 — confirm on survey)

   Car porch: 9 ft x 18 ft, east side near entrance, within/overlapping the
   front setback zone — kept light, open-sided, low-thermal-mass, not an
   enclosed garage.

   Prevailing wind (ASSUMED, T1-U — unverified against real station data):
   inlets planned from NORTH and SOUTHEAST faces feeding the central shaft;
   exhaust at roof/mumty level.
```

### B.3 Street, entry, and privacy sequence

Gate and porch on the east 25 ft frontage. Front setback taken as **≈5 ft** (T1-U placeholder for the 5-marla band — reconfirm against RDA's current bylaw). The entrance turns immediately into a small foyer/screened transition rather than a direct sightline into the family lounge (Section 12).

### B.4 Footprint, coverage, and FAR (all figures T1-U, unverified pending RDA confirmation)

- Coverage cap assumption (5–10 marla band): **≈80%** of 1,125 sq ft ≈ **900 sq ft**.
- Setback-bound buildable envelope (5 ft front + rear setbacks, side walls as party-wall, 0 ft — a construction-practice assumption, not a legal claim): 25 ft × 35 ft = **875 sq ft**.
- **Setbacks bind, not coverage (875 < 900)** — this is the figure carried through the rest of this document (matching the reconciled arithmetic in Output C): **covered area per floor = 875 sq ft** (byelaw definition, external-wall-face to external-wall-face). G+1 total covered = 875 × 2 = **1,750 sq ft**, comfortably inside a FAR cap of 1:1.8 × 1,125 = **2,025 sq ft**.
- Mumty allowance: **9–13% of plot ≈ 101–146 sq ft** — enough for a stair-head enclosure plus a small covered roof landing without threatening the FAR cap.

### B.5 Parking

One small-car bay, **9 ft × 18 ft**. Ideal practice puts the garage/porch on the west/southwest face as a thermal buffer, but on this plot the entrance (and porch) is fixed to the road-facing east side — the porch is kept deliberately light and open-sided, and the thermal-buffer role a west-facing garage would normally play is reassigned to the stair/bath/store cluster on the rear (west) wall instead.

### B.6 Light/vent well — sizing and honest function

Sized at **6×8 ft up to 8×10 ft**, W/H ratio 0.27–0.36 — note this overlaps the low end of the 0.3–0.7+ range associated with true-courtyard thermal-mass performance, so ratio alone doesn't cleanly separate "light well" from "courtyard." The real basis for calling this a light-and-vent well rather than a courtyard is **absolute size and geometry**: at 48–80 sq ft, sharing its volume with the stair run, with no full-depth sky opening independent of the stair landings, it does not have the exposed thermal mass or usable open floor a courtyard needs. Confirmed function: cross-ventilation, daylight to the kitchen/bath zone, stack-effect exhaust — not courtyard-grade thermal performance.

Even at this small size the well is a **diaphragm cut** flagged to the structural engineer (Section 8.5: centered position, continuous edge beam around the opening) — real seismic territory, not a cosmetic note.

**Monsoon detailing (mandatory, not optional, in this humid subtropical climate):** floor drain to a small sump pit (min. 300×300×300mm) discharging to stormwater, floor sloped 1:80 toward the drain, a **150mm upstand (splash kerb)** at every bathroom/stair-landing opening onto the well. The roof-level cowl is a **louvred, rain-hooded vent cowl**, not a plain open top.

### B.7 Outdoor area

No rear garden is realistic inside a ≈875 sq ft footprint on a 1,125 sq ft plot. The real outdoor room is the **roof terrace** (Section 10) — also the single largest solar-gain surface on the house and the highest-value shading target in the whole design.

### B.8 Solar exposure by facade

- **South (45 ft long wall, assumed party wall — see §3.0 caveat and Section 9's party-wall reality check):** *if open*, manageable with a modest 12–24 in chajja — Islamabad's winter noon sun (≈33°) is shallower than Lahore's (≈35°), which argues for a slightly shorter overhang so low winter sun still reaches the glazing (see Section 5's D=H/tan(altitude) arithmetic).
- **East (25 ft entrance wall):** low-angle morning sun only, manageable with vertical fins/jali.
- **West (25 ft rear wall):** the hard facade — no horizontal overhang works (Section 5). Assigned to the stair/bath/store buffer cluster.

### B.9 Prevailing wind assumption (T1-U, unverified)

No station data or wind rose is cited — only a generic climate-zone reference. Commonly cited descriptions instead describe a seasonal shift (NW winter, SE summer monsoon). Pending real verification, this design assumes inlets on north and east/southeast faces feeding the central shaft, exhaust at roof/mumty level (full airflow path in Section 6/Output E).

---

## C. Floor Plan

**Envelope arithmetic (method — every figure here MUST be replaced with RDA's current published bylaw before any submission drawing):**

- Plot: 25 ft × 45 ft = 1,125 sq ft.
- Setbacks (T1-U placeholder): front 5 ft, rear 5 ft; sides party-wall (0 ft construction practice, not a confirmed legal minimum).
- Setback-buildable = 25 ft × 35 ft = 875 sq ft. Coverage cap (≈80% band) ≈900 sq ft. **Setbacks bind (875 < 900) — covered area per floor = 875 sq ft**, measured external-wall-face to external-wall-face, not reduced a second time for wall thickness. G+1 total covered = **1,750 sq ft**.

**Three area categories, kept distinct:**

1. **Covered area** (byelaw term): 875 sq ft/floor, 1,750 sq ft G+1 — the figure a coverage/setback check runs against.
2. **Internal clear box** (inside face of external walls only): 25 − 1.5 ft (two 9 in walls) = **23.5 ft** frontage × ≈33.5 ft depth (35 ft less front/rear wall allowance) = **787 sq ft/floor**, **1,574 sq ft** G+1. (Check: 875 − 787 = 88 sq ft external-wall footprint/floor, against a 120 ft perimeter × 0.75 ft ≈ 90 sq ft — consistent within rounding.)
3. **Carpet area** (internal clear box less internal-partition loss — the number actually used against the room budget): internal partitions here cost roughly **3%** of the internal clear box at this layout's partition lengths, not the 65–75% "net-to-gross" figure a generic tower/apartment rule of thumb would suggest (that figure nets out shared cores/lobbies/corridors that don't exist in a 5-marla detached house — dropped here as inapplicable). **Carpet area ≈ 1,574 × 0.97 ≈ 1,527 sq ft for G+1.**

**What the 23.5 ft frontage forces:** only one 12–14 ft room plus a 4 ft passage plus a 5 ft bath fit side by side — a **Linear/Side-Passage plan archetype**, the honest default for a 25 ft-frontage 5-marla plot, not the two-bay layout a wider plot could support.

**Light well, not a courtyard:** with only ~23.5 ft of width to divide, there is no spare 10 ft block for a true courtyard. The target is a **light/vent well of 4 ft × 6 ft**, centered against the party wall, serving the stair half-landing and internal bathrooms on both floors. At two-storey height (≈6.7 m) its W/H ratio is well under 0.3 — a daylight-and-ventilation shaft, explicitly not a thermal-mass courtyard.

**Monsoon detailing at the light well** (Rawalpindi is humid subtropical — not optional): floor drain to a sump pit (min. 300×300×300mm), floor sloped 1:80, 150mm splash-kerb upstand at every bathroom/stair-landing opening. Roof-level cowl: **louvred, rain-hooded**, not a plain open top — louvre blades pitched to exclude driving rain while passing the stack-ventilation air column.

**Moisture and humidity management:** 230mm solid brick in a humid climate needs a vapour-permeable (lime-based or lime-cement) external finish, not a fully sealed cement-rich render, which traps diffused moisture and drives internal damp/efflorescence over a monsoon cycle. A second moisture line is needed at the roof/parapet junction (proper roof DPC/flashing) in addition to the plinth DPC — humid-climate parapets are a common damp-ingress point missed by hot-dry detailing. A horizontal chajja blocks direct-beam radiation but **not diffuse/hazy-sky radiation**, materially larger here than in a hot-dry sky — so window-to-wall ratio and glazing choice on north/east faces still matter, not just south/west overhang sizing.

### Ground Floor (≈875 sq ft covered)

| Space | Approx. size | Notes |
|---|---|---|
| Porch (uncovered, in front setback) | 9 ft × 18 ft | One small car |
| Foyer + entry screen | 5 ft × 6 ft | Jaali/solid screen breaks the street-to-lounge sightline |
| Drawing/guest room | 12 ft × 12 ft | Front, east-facing — tolerable morning sun only |
| Powder room | 3 ft × 5 ft | Off the foyer, for guests |
| Lounge + dining (merged) | 12 ft × 14 ft | Merging is deliberate — the area budget can't sustain two separate formal rooms |
| Kitchen | 7 ft 0 in × 9 ft 6 in | Single-run galley, 42 in aisle; rear, north/east — never west |
| Bedroom 1 + attached bath | 11 ft × 12 ft + 5 ft × 8 ft | Rear, north side (coolest); ground-floor bedroom for an elderly parent or guest |
| Stair (dog-leg) | 7 ft × 12 ft well | Against the party wall, west side |
| Light/vent well | 4 ft × 6 ft | Centre-west, beside the stair; lights the stair half-landing and ground bath; floor drain + sump |
| Store | 4 ft × 6 ft | Under the upper stair flight (headroom permitting) |
| Rear open strip (mandatory) | ≥25 ft × 5 ft | Kitchen light/vent, washing area, water tank access, sewer chamber |

### First Floor (≈875 sq ft covered)

| Space | Approx. size | Notes |
|---|---|---|
| Master bedroom + attached bath | 12 ft × 14 ft + 5 ft × 8 ft | North side — coolest orientation |
| Bedroom 2 + common bath | 11 ft × 12 ft + 5 ft × 7 ft | North-east; flexible room — shrink to 10 ft × 11 ft first if budget is tight |
| Family lounge/TV nook | 10 ft × 12 ft | Over the ground-floor drawing room |
| Front terrace | 9 ft × 12 ft | Over the porch, shaded by the upper chajja |
| Stair | 7 ft × 12 ft | Stacked exactly on the ground-floor footprint — non-negotiable |
| Light/vent well | 4 ft × 6 ft | Stacked; lights Bedroom 2's bath, continues ventilation stack toward the roof; splash upstand |

### Roof

Mumty (~7 ft × 10 ft) sited north/east so its shadow clears any future south-facing solar-panel zone; the rest is terrace (drying/sitting, insulated, partly shaded); overhead water tank on the party-wall line, never mid-span, clear of the panel-mounting zone (Section 10.4).

### Carpet-Budget Check

Ground floor required: Foyer 30 + Drawing 144 + Powder 15 + Lounge/dining 168 + Kitchen 67 + Bed 1 132 + Bath 1 40 + Stair 84 + Store 24 = **704 sq ft**. First floor required: Master 168 + Master bath 40 + Bed 2 132 + Bath 2 35 + Family lounge 120 + Stair 84 = **579 sq ft**. Total required ≈ **1,283 sq ft** against ≈**1,527 sq ft** available → ratio ≈ **0.84** — a comfortable fit with ≈16% margin. Bedroom 2 is flagged flexible (10 ft × 11 ft if the client wants a larger terrace/store/bathroom elsewhere) as good construction-tolerance practice, not because the budget is marginal.

**Circulation check:** stair (84+84=168 sq ft) + foyer (30 sq ft) = **198 sq ft** of 1,750 sq ft total ≈ **11.3%** — inside the healthy 8–14% band, using only named spaces from the schedule above (no generic padding added).

### Orientation Adaptation Notes (cross-reference — full reasoning in Output A.5)

- **East-open (as designed):** morning sun on entrance tolerable; west is the thermal-buffer zone; bedrooms sit north.
- **North-open:** rotate 90°; entrance/drawing-room façade becomes the *best* daylight façade (WWR 20–30%) with almost no direct-gain penalty — though diffuse/hazy-sky radiation still argues for a moderate rather than maximal WWR even here.
- **South-open:** drawing room and lounge on the entrance/south façade behind a 12–24 in chajja; bedrooms stay north.
- **West-open (hardest):** entrance takes unshadable afternoon sun — push the drawing room to minimal-glazing street presence (WWR 0–8%, jaali/vertical fins only), let the porch act as the shading buffer.

---

## D. Section

*One representative building section, cut through the stair/light-well spine, looking north.*

**Vertical datums:** plinth +450mm (1'-6") above road crown (raise to 760mm if the street is low-lying); ground floor-to-floor 3,200mm; first floor-to-floor 3,200mm; mumty floor-to-floor 2,400–2,700mm; RCC slab 150mm one-way at both levels (every span ≤14 ft); external wall 230mm brick throughout, load-bearing cross-walls at 11–14 ft centres.

**Reading the section left to right, bottom to top:**

1. **Foundation.** Strip footing under load-bearing cross-walls (conceptual — confirm against a real soil report and licensed engineer's design). Plinth beam at +450mm ties all footings, DPC above it.
2. **Ground floor slab.** 100–150mm RCC on compacted sub-base, floor finish over.
3. **Ground floor room** (e.g. Bedroom 1). 3,200mm floor-to-floor, sill 900mm, head 2,134mm. A 12 in chajja on the north face is mainly a rain deflector here, since north has little direct-gain problem.
4. **Stair + light well.** Dog-leg stair in a 3,585mm × 2,150mm well: total rise 3,200mm as **two flights of 10 risers @ 160mm** (1,600mm/flight); each flight **9 treads @ 265mm** (2,385mm going) — **18 treads total** (a dog-leg's two flights each start/end at a flat landing, so each carries risers-minus-one treads: 9+9=18, not the 19 a single straight run would need). Flight 1 occupies 2,385mm of run within the 3,585mm well, leaving **1,200mm for the half-landing**; flight 2 returns above/beside flight 1 within the 2,150mm width. The 4×6 ft light well runs continuous from ground floor to roof beside the stair, glazed/louvred at bath levels (splash upstands per the monsoon note), with a window at the stair's half-landing. **This shaft is the house's ventilation chimney** — one uninterrupted vertical path, open at top to a **louvred, rain-hooded vent cowl** in the mumty wall, never sealed over as a skylight above a WC route.
5. **First floor slab, +3,200mm.** 150mm RCC. Stair lands in the first-floor passage — never inside a bedroom — stacked exactly on the ground-floor footprint.
6. **First floor room** (e.g. Master bedroom). 3,200mm floor-to-floor, sill 900mm, head 2,134mm, opening sized to an escape-egress reference target of ≥5.7 sq ft clear opening (US IRC figure cited as reference only — confirm applicable local egress requirement).
7. **Roof slab, +6,400mm.** 150mm RCC, insulated (50–75mm minimum) and finished in a reflective, light-coloured surface (Section 10). Drainage slope maintained to the rainwater outlets, independent of the light-well drainage in item 4.
8. **Mumty.** Stacked exactly on the stair below, floor-to-floor ~2,400–2,700mm, north/east on the roof plate. Carries a **louvred, rain-hooded vent cowl** at head height — the **high-level outlet** for the whole house's stack-ventilation path (low-level inlet at ground-floor windows and the light well).
9. **Sunlight penetration.** A north-facing window admits shallow, low-heat daylight year-round (diffuse radiation still argues for moderate glazing, per the humidity note in Output C). A south-facing opening shows the 12 in chajja fully shading the June solar-noon ray (altitude ≈80°) while admitting the shallow December noon ray (≈33–35°) almost to the sill — the chajja blocks direct-beam only; glazing spec (tint/low-E) handles diffuse radiation separately.
10. **Hot-air exhaust path**, a single labelled arrow: warm, humid air rises through the light well and stairwell void and exits through the mumty's louvred, rain-hooded vent cowl — the section's summary of the whole passive-cooling strategy, called out directly on the drawing.

**Key traceable numbers:** 1 marla (225 basis) = 225 sq ft; 5 marla = 1,125 sq ft — matches the brief exactly. 25 ft frontage → 23.5 ft internal clear width. Coverage ≈80% (T1-U) vs. setback-bound 875 sq ft footprint — setbacks govern. Area accounting: covered 875 sq ft/floor → internal clear box 787 sq ft/floor → carpet ≈1,527 sq ft G+1 (≈3% partition loss; generic tower net-to-gross rule dropped as inapplicable). Stair: 3,200mm → 20 risers @ 160mm, two flights of 9 treads @ 265mm (18 total), well 3,585×2,150mm, half-landing 1,200mm; headroom target 2,100mm minimum, above the 2,032mm IRC 2021 reference floor (US figure, reference only). Light well vs. courtyard: honest target 4×6 ft to 6×8 ft, W/H under 0.3 — ventilation/daylight only. Shading arithmetic: D=H/tan(altitude) — 12 in overhang fully shades a 7 ft south window at ~80–82° summer altitude, admits ~90% at ~33–35° winter altitude; on west, the same math needs >4m — no ordinary projection solves the west problem, only minimizing glazing does. Solar altitude for this latitude band: summer ≈79.7°, equinox ≈56.3°, winter ≈32.9°. Circulation target 8–14%, achieved at ≈11.3%. Area-budget check: required ≈1,283 sq ft vs. available ≈1,527 sq ft, ratio ≈0.84.

**Not covered here** (owned elsewhere in this document): final structural member sizing (Section 7/Output G), seismic detailing (Section 8), envelope/material selection (Section 9/Output H/I), cost tiering (Output K).

---

## E. Passive Cooling Diagram

*Airflow path, described with directional arrows — drawn for the corner/side-open plot assumption in §3.0. If the plot proves mid-row, delete the north-inlet branch and route all ground-floor air through the east inlet only — the stairwell-chimney portion is unaffected either way.*

```
                         ROOF / MUMTY
                    ┌───────────────────┐
                    │  ↑ HIGH-LEVEL      │  ← louvred vent, wind-assisted
                    │    EXHAUST         │    (catches N / SE prevailing wind)
                    └─────────△──────────┘
                              │
              ┌───────────────┴───────────────┐
              │↑                               │↑
     LIGHT/VENT WELL                    STAIRWELL (primary chimney —
     (rooflight, louvred,               works under either plot config,
      never sealed)                      wind or no wind)
              │↑                               │↑
   ── 1ST FLOOR ── ─────────────────────────────────────────
              │↑           roshandan →│↑        │↑
        (bath/bedrm         BEDROOMS  │    stair void
         light source)                │
   ── GROUND FLOOR ── ────────────────────────────────────
              │↑                               │↑
     light well inlet              stair base draws
     (shaded, planted             cross-flow air from
      pocket, cooler air)          living/dining

   N-FACING WINDOW →→→ LIVING/DINING →→→ (unobstructed path to stair core)
   (low-level inlet — ONLY IF NORTH IS OPEN; see §3.0 fallback if mid-row)

   E-FACING WINDOW/DOOR →→→ KITCHEN →→→ (secondary inlet, entry-adjacent —
   (low-level inlet, entry porch shades it)   exists under EITHER config)

   SOUTH WALL: assumed party wall in this configuration — no openings
   WEST WALL: no openings of consequence — buffer zone (stair/store/bath)
              absorbs west solar load instead of ventilating through it
```

**Reading the diagram:** two low-level inlets (north living-area window, east kitchen/entry opening) feed the ground floor under the §3.0 assumption — if survey shows otherwise, only the east inlet exists and the house runs single-aspect. Air crosses the unpartitioned living/dining volume to the stair base, where buoyancy pulls it upward past each floor, gathering roshandan air on the way. The light/vent well runs its own parallel buoyancy path. Both converge at roof level near the mumty, whose wind-assisted vent gives extra pull whenever prevailing wind is present — but the system does not depend on it: solar heating of the roof and stair-head sustains the draw on still days, the one piece of the diagram unchanged even in the mid-row fallback. Outlet free area is kept at 1.25–1.5× inlet free area so the exhaust never bottlenecks the flow. Night-flush operation is simply this same path left fully open after sunset, purging the day's stored heat before it reradiates the next day.

---

## F. Passive Heating Diagram

*Winter sunlight path + thermal mass retention — contingent on the south face being genuinely open per §3.0. If the plot proves mid-row with south as a party wall, this mechanism does not exist and must be re-derived for whichever face is actually open.*

```
   WINTER SUN (32.9° altitude at solar noon, low angle)
        ╲
         ╲
          ╲
           ╲   0.39 m chajja — shadow drops only ~0.25 m
            ╲  down the window face at this low angle
             ╲
   ┌───────────╲─────────────────────┐
   │  SOUTH WINDOW (2.1 m tall)       │  ← ~88% of window admits direct
   │  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │    sun onto the room at winter noon
   │  ░░  sun strikes floor + lower   │
   │  ░░  wall directly, deep into    │
   │  ░░  the room                    │
   └───────────────────────────────────┘
              │
              ▼
   ┌─────────────────────────────────┐
   │  9 in (230 mm) BRICK MASS WALL   │  ← this SOUTH wall specifically does
   │  + FLOOR SLAB (thermal mass)     │    the direct-gain mechanism — not
   │                                  │    true of the party/buffer walls,
   │  Day: mass warms as sun strikes  │    which at most get the separate
   │  Evening/night: stored heat      │    time-lag benefit (Section 3)
   │  releases slowly into the room   │
   └─────────────────────────────────┘  ← the "night-time heating effect,"
                                            specific to this wall only

   MEANWHILE, OVERHEAD:
   Mumty vent + light-well rooflight → THROTTLED / CLOSED in winter
   (same shaft that vents summer heat would otherwise bleed the
    stored winter heat straight out through the roof)

   COMPARE — SUMMER SUN (79.7° altitude, steep, nearly overhead):
        │
        │
        ▼
   ┌───────────│─────────────────────┐
   │  SOUTH WINDOW                    │  ← same 0.39 m chajja fully blocks
   │  (fully shaded — no direct sun   │    this steep summer sun; window
   │   reaches the glass)             │    stays in shadow all day
   └─────────────────────────────────┘
```

**Reading the diagram:** the single fixed 0.39 m chajja does two opposite jobs with one piece of geometry — full summer shade at 79.7°, ≈88% winter exposure at 32.9°. Winter sun strikes the floor and lower brick wall directly; because brick has enough thermal mass to absorb heat slowly through the day, the wall keeps releasing it through the evening and into the night. This is specifically the south wall's mechanism — it does not apply to the west buffer wall or to the assumed south party-wall condition in the mid-row fallback. This is the house's actual passive winter heating system, but it only works if the occupant closes down the same stack vents that are summer assets each winter; otherwise the continuous buoyancy draw keeps pulling this stored heat straight out through the roof, defeating the strategy. This seasonal switch is an occupant action, not a mechanical one, and should be stated plainly at handover — along with the fact that the whole diagram depends on the §3.0 orientation assumption, which must be confirmed against survey before construction.

---

## G. Structural Concept (CONCEPTUAL ONLY)

*Full reasoning, worked wall-density and base-shear arithmetic, and the seismic-zone conflict resolution are in Section 7 above. This is the condensed load-path summary.*

- **System:** confined masonry (CM), not URM, not RCC frame — see Section 7.1 for why. Max height 3 storeys; G+1 fits with margin.
- **Foundation:** strip footings under CM wall lines, 600mm × 300mm, founded 1.2–1.5m below NGL — subject to a real soil report (presumptive bearing 150–250 kPa; loess-collapse risk flagged, Section 7.6).
- **Columns:** 230×230mm RC tie-columns at every corner, wall junction, free end, and opening jamb >1.2m, spaced ≤4.0m — not moment-frame columns; confinement elements within CM walls, wall-first-then-cast sequence.
- **Beams:** 230×230mm RC tie-beams, continuous ring at every floor and roof level — plus a **second, separate tie-beam ring at the light-well's inner edge** (Section 8.5's ring-diaphragm requirement).
- **Slabs:** 125mm two-way (150mm beyond 4.3m span), preliminary.
- **Shear/bracing:** confined masonry walls themselves are the lateral force-resisting system; the parking-opening bay may need a converted RC shear-wall/moment-frame line if the wall-density check (Section 7.4) fails there.
- **Load path:** footing → plinth beam → tie-column → tie-beam ring at each floor → roof ring beam, continuous with no breaks — a shifted wall between floors or a tie-column stopping short is a real defect (Section 8.2).
- **Governing open item:** the wall-density check (2.5–3.5% depending on confirmed zone) has **not been run against the actual floor plan** — this is a required next step before treating the layout as structurally settled, and it is what actually decides whether the parking opening and light-well as currently sized are acceptable.

**Flagged as CONCEPTUAL ONLY**, per Section 7's three-tier confidence framing: nothing above may be built from without a PEC-registered structural engineer's stamped calculation, a real soil report, and the actual seismic zone confirmed against the current BCP SP-2007 map for these coordinates.

---

## H. Building Envelope

**Party-wall reality check — resolve before any facade below is treated as final.** The default condition on a 25×45 ft plot in Rawalpindi housing schemes is zero side setback (both long faces as party walls) — this document's §3.0 assumption (only south is a party wall) has not been confirmed against the actual approved site plan for this plot. Where a face turns out to be a party wall, substitute a plain 230mm confined-brick wall with no openings and skip the rest of that face's bullet below.

**Wall build-up, by façade:**

- **East (primary open/glazed face):** 230mm confined brick, larger openings permitted (low-heat morning daylight), deep 600mm verandah/chajja shading the ground floor, standard 900mm sills.
- **West (hardest thermal problem, if openable):** minimum openings, high-level only (1800mm sill, small area), 200mm AAC infill (if the four-point checklist in Section 9 passes), **750–900mm deep chajja** combined with **vertical jaali fins** — a chajja alone cannot intercept a sun angle that's nearly horizontal at 5–6pm in summer; vertical fins are the only element that blocks low-angle lateral sun. West is also a side wall subject to the party-wall check.
- **North (only if setback confirmed, otherwise blank party wall):** brick masonry, moderate openings — north light is the most stable, glare-free, lowest-heat-gain light available; simple 450mm chajjas as rain protection, not serious solar shading.
- **South (only if setback confirmed, otherwise blank party wall):** brick masonry, 450–600mm chajja sized to Section 5's arithmetic — summer self-shading, winter solar gain simultaneously, the one facade where passive winter heating is genuinely free (Section 4/F), provided this face is not a party wall.

**Windows and openings:** standard sill 900mm; high-level bathroom windows 1800mm sill (privacy + envelope performance, Section 12). **Chajja structural sizing, span-banded** (not one detail for every span): up to 450–600mm projection, root ≈75mm tapering to ≈50mm (north/south/east); 750–900mm projection (west), root **≈100–125mm** tapering to ≈50–65mm, top-face reinforcement sized to the actual moment at that span — a 900mm cantilever at a 75mm root is under-proportioned and should not be built without the engineer's calculation. All chajjas cast **monolithically** with the lintel (a cold-jointed chajja cracks and eventually drops), with its own 1:50 fall away from the wall. Jali screens (west facade, stairwell, street-facing private rooms) do triple duty — solar shading, privacy, and (being perforated) not blocking the ventilation pressure differences the natural-ventilation strategy depends on.

**Roof envelope** (see Section 10 for full build-up): flat, accessible RCC roof — the right choice for a usable roof (panels, tank, pergola, terrace) with monsoon drainage properly designed, not assumed away. Inverted/protected membrane build-up, ≈260–360mm total, ≈4.9–7.5 kN/m² self-weight (per-layer breakdown in Section 10.2) — the membrane sitting under insulation roughly doubles its realistic service life versus a traditional cold-roof arrangement, which is explicitly not recommended here. **Parapet:** waterproofing upstand ≥150mm, coping overhang ≥40mm with a ≥5mm drip groove, coping falling inward; height 1.0–1.1m for an accessible terrace [confirm against RDA byelaw]. A free-standing masonry parapet with no out-of-plane restraint is a documented earthquake failure mode — the tie-back to the roof diaphragm is a structural/seismic item (Section 8.4), not a waterproofing detail. **Ponding safety:** 100mm of standing water on a blocked drain adds ≈0.98 kN/m² unbudgeted load — a secondary/overflow outlet set higher than the primary, sized for full roof flow, is required, not optional.

---

## I. Materials — Practical Palette for Pakistani Sourcing

| Element | Primary material | Why | Cost/availability note |
|---|---|---|---|
| Ground-storey structural walls | Burnt clay brick, 230mm, confined masonry | Universal availability, strong seismic track record in CM form | Cheapest load-bearing option; zero supply-chain risk |
| Upper-storey west-facing infill (if west confirmed openable) | AAC block, 200mm | 5× better insulator than brick, ⅓ the weight (humidity-qualified, Section 9) | **Conditional** — only if the 4-point local-supply checklist passes AND the party-wall check confirms this face is openable; otherwise substitute brick |
| Wet-area walls | Brick, 115mm | Handles capillary moisture without extra tanking cost | Universal |
| Mortar | Cement-sand, graded 1:4/1:5/1:6 by location (Zone 2B basis) | Must stay weaker than the unit; governs crack location | Cement is the main cost driver — do not over-specify |
| External plaster | Cement plaster 1:6 over bonding slurry (AAC); standard cement plaster (brick) | Matches substrate; on AAC this coat is the monsoon moisture-management layer | Fibre-mesh reinforcement at every AAC-to-brick/RCC junction, 150mm chicken mesh lapped 75mm each side |
| Internal plaster | Gypsum plaster (AAC, no curing needed); cement plaster (brick) | Gypsum is the correct AAC-compatible internal finish | Availability part of the same local checklist as the AAC decision |
| Roof waterproofing | 2-ply modified bitumen membrane | Standard, repairable, well understood locally | Widely available in urban Punjab |
| Roof insulation | XPS, 50–75mm, closed-cell | Only insulation type safe in the inverted/wet position | More expensive than EPS but the position mandates it |
| Roof structure | RCC slab, 125–175mm (preliminary) | Standard Pakistani flat-roof practice, matches Section 7's structural system | — |
| Chajjas/sunshades | Cast-in-place RCC, monolithic with lintel, root span-banded | Must be monolithic; longer spans need a heavier root | Standard detail; engineer sign-off required on the west span |
| Shading screens | Precast or brick jaali | Traditional, buildable, doubles as privacy screen and vent-permeable shading | Locally cast, low cost |
| Optional plinth facing | Local stone (Rawalpindi/Potohar-sourced) | Durable, resists rising damp better than plaster alone | Regional availability — verify sourcing, not assumed |
| Concrete block (alternative to brick, boundary walls) | Solid concrete block, 400×200×200mm | Alternative for boundary walls/plinth stems | Must age ≥28 days, must **not** be soaked (opposite rule to brick — a common site error worth flagging) |

**Deliberately avoided:** hollow concrete block used ungrouted as load-bearing (a reject-list item in this seismic zone); any masonry unit specified on a market "grade" label without a real test report; any mortar mix weaker than 1:6 anywhere; and — pending the party-wall confirmation — any openings, chajjas, or jaali specified on a face that turns out to be a shared party wall.

---

## J. Climate Strategy Table

**Basis:** Rawalpindi/Islamabad — humid subtropical (Köppen Cwa), latitude ≈33.6°N. Four seasonal regimes: a short severe-hot pre-monsoon window (May–June, up to 40–42°C), a humid monsoon (July–Sept), a cool dry winter (Dec–Feb, night lows 2–5°C, occasional frost), and dusty pre-monsoon westerly wind events. The passive systems (Sections 3–10) are fixed geometry; what changes hour to hour and season to season is which system the occupant activates.

**Dimensional basis:** solar altitude summer solstice ≈80°, winter solstice ≈33°, equinox ≈56°. A 15 in (1.25 ft) deep reveal fully shades only sun above ≈74.5° altitude (tan⁻¹(4.5/1.25) for a 4.5 ft window head) — occurring within roughly ±1.5 hours of solar noon at summer solstice. At any lower angle, on either facade, the same reveal gives **partial**, not full, shading — reveals of buildable depth cannot fully block low-angle sun on either east or west. West window-to-wall ratio minimized to 8–10% vs. 20–25% on east/south. Stack-effect shaft cross-section ≈3×4 ft (12 sq ft); high-level vent 4–6 sq ft operable louvre; total operable cross-vent area 55–90 sq ft (5–8% of floor area).

**Why east and west are still handled differently, correctly stated:** the identical low solar altitude occurs on both facades (morning on east, afternoon on west), and a 15 in reveal partially shades both equally. What differs is (1) **ambient-temperature coincidence** — morning low sun lands 8–12°C below the day's peak; afternoon low sun lands during the 2–5pm peak-ambient window, stacking on the hottest air of the day plus accumulated fabric heat; and (2) **program tolerance** — east rooms (kitchen/breakfast) are used in the morning, a cooler-hour trade worth making for daylight; west rooms have no equivalent trade to justify the same exposure at the worst hour. So: east keeps normal glazing (20–25% WWR) with the reveal accepted as partial mitigation; west relies on minimizing glazed area itself (8–10% WWR), since reveal depth alone was never going to solve the west problem at any buildable dimension.

**Roof insulation is baseline, not upgrade** — the insulated roof assembly (Section 10) is what every heat-gain resistance claim below refers to; there is no "plain slab" version of this house.

**Thermal mass vs. wall material — the tension made explicit:** night-flush and winter-retention (below) depend on **exposed high-mass construction** (RCC soffit, 9 in solid brick). AAC (Section 9/I) is a low-density, low-thermal-mass material chosen specifically to insulate rather than store heat — it works against the night-flush strategy, not with it. These are two different strategies, not a stackable upgrade; this document's baseline wall is 9 in solid brick/plastered masonry/RCC, because the whole climate strategy below is built on it. AAC is discussed only as an explicitly flagged alternative-strategy trade-off (Output K), not an add-on.

| Condition | What's happening outside | House response (which passive system is "on") | Occupant action |
|---|---|---|---|
| **Summer day** (May–Sept, 32–42°C) | Sun high/hot; east gets a moderate morning hit (partially reveal-shaded, cooler hour); west gets a low afternoon hit at the hottest hour, largely unmitigated by reveal geometry | East 20–25% WWR with partial reveal shading; west minimized to 8–10% WWR; insulated roof resists the largest sun-facing surface; stairwell/light-well stack (12 sq ft shaft, 4–6 sq ft top vent) pulls hot air out at roof/mumty level | Cross-vent openings open morning/evening; close the small west sash 2–5pm; stairwell top vent open continuously; ceiling fans on, AC only as backup in the worst 4–6 weeks |
| **Summer night** (24–28°C) | Ambient drops well below the day's absorbed mass temperature | **Night flushing:** all vents + top vent opened wide to purge heat the exposed masonry/RCC mass absorbed during the day | Open all operable jali/vents before sleeping (jali makes this safe, Section 12); highest-leverage free cooling action, costs nothing |
| **Winter day** (8–18°C, clear skies) | Sun much lower (≈33° solstice, ≈56° equinox), useful heat not a threat; short days | Sun-facing glazing left unshaded — winter's ≈33° sun sits well below the reveal's 74.5° full-shade threshold, penetrating deep and striking the floor/exposed masonry; stack vents throttled down | Keep curtains open on sun-facing glazing during the day; stairwell top vent mostly closed; let low sun do the free heating |
| **Winter night** (2–5°C, near frost) | House needs to hold onto daytime gain | Exposed thermal mass re-radiates absorbed heat after sunset — the same mechanism as summer night-flushing, run in reverse; insulated roof prevents the biggest night heat-loss path | Close all vents and the stairwell top opening fully after dark; heavy curtains at night — a controls/behavior cost, not a construction cost |
| **Monsoon/rain** (July–Sept) | Cross-ventilation less effective (humidity limits evaporative comfort); wind-driven rain risk at open jali/light-well | Roof falls + parapet upturns keep the shaft and roof dry; light-well drainage sized for monsoon intensity; deep reveals double as rain screens | Close light-well/jali operable panels during active rain; ceiling fans over cross-vent for humid-day comfort; check roof drain/downpipe before monsoon onset |
| **Dusty/hot wind events** (April–June) | Wind-driven dust, often from the west — already the minimized-glazing face | Low WWR on west is naturally low-dust-load too; jali screens filter coarse dust without blocking airflow | Close windward (typically west) openings during dust events, keep leeward (east) cross-vent open |

**Cross-cutting note:** every "occupant action" above is a zero-construction-cost control decision. This is deliberate — the passive performance is designed to be free to operate, but it is not automatic. A passive house with the vents left shut all summer performs like a plain sealed box.

---

## K. Cost Strategy

### Reality Check for this section

All figures below are **conceptual, schematic-stage cost bands (Tier C confidence)** — a market-rate snapshot, not a quotation. Before any of these numbers are used to commit money: a PEC-registered structural engineer must produce calculated member sizes and a real BOQ; local rates must be re-verified in Rawalpindi at time of tendering; RDA map approval and NOCs are a real cost/schedule line item, not a rounding error.

### Headline cost bands — 5 marla, G+1

| Build tier | Cost (PKR) | What it buys |
|---|---|---|
| Grey structure only | 42–52 Lac | Foundation, RCC frame, masonry, plaster, insulated roof + waterproofing — no finishes |
| Turnkey, economy finish | 70–90 Lac | Grey structure + basic tiling, standard sanitary/electrical, standard doors/windows |
| Turnkey, A-category finish | 90 Lac – 1.10 Cr | Better tile/fixture grade, branded sanitary ware, upgraded woodwork — **realistic target tier for this brief** |
| Turnkey, premium finish | 1.10 – 1.50 Cr | High-end finishes throughout — not necessary to achieve this design's climate goals |

Because this brief is G+1, the double-storey band applies directly — foundation/site costs amortize over more covered area than a single-storey version of the same footprint would (assuming comparable soil/foundation conditions; a PEC engineer's actual footing design, not this document, confirms whether that holds).

### Grey vs. finishing split

**Grey structure: 55–65%** of total cost — preliminaries 2–4%, earthwork/substructure 6–10%, RCC concrete 14–18%, reinforcement steel 14–19%, masonry 6–9%, plaster 4–6%, insulated roof + waterproofing 2–3%, MEP rough-in 4–6%. **Finishing: 35–45%** — flooring 8–12%, woodwork 7–11%, paint/false ceiling 4–7%, sanitary/kitchen fixtures 4–7%, elevation/facade 3–6%, external works 2–5%, windows/glazing 2–4%, steel grills/gates 2–4%, electrical finishing 3–5%, plumbing finishing 1–3%. Total MEP ≈**8–14%** of the whole build — the Section 13 solar PV/hot-water items sit inside this envelope, not on top of it.

**Pareto five** (≈80% of build value): reinforcement steel (14–19%), RCC concrete (14–18%), flooring (8–12%), masonry+plaster (10–15%), woodwork (7–11%). Cost-control effort should focus here — value-engineering light switches/paint brand barely moves the needle by comparison.

**Accuracy flag, not an add-on:** kitchen fit-out, elevation/facade, and external works (already inside the 35–45% finishing band, ≈9–18% combined) are the sub-items clients most often *under-tier* — pricing them at the bottom of the band when this brief's A-category target calls for the top. Do not add this 9–18% a second time to a total that already contains it.

### Contingency, escalation, and soft costs

| Item | % of build cost | Why |
|---|---|---|
| Contingency (schematic stage) | 15–25% | Low design maturity — drops to 5–10% with full construction documents, 3–5% with firm subcontract prices |
| Escalation (6–9 month build) | 2–5% | Base × material share (0.55–0.62) × annual inflation (10–15%) × (duration/2) |
| Soft costs | 5–9% (6% default) | Architectural design 3–6%, structural design + BBS 0.5–1.5% (non-negotiable, PEC-stamped), site supervision 3–6% |

**Combined, additive:** ≈**22–39%** over base build cost at schematic stage. Worked example on the A-category band (90 Lac–1.10 Cr): all-in schematic-stage budget ≈**1.10 Cr–1.53 Cr**. This range compresses toward ≈9–20% once construction documents exist (contingency alone drops to 5–10%) — state both numbers to the client so neither is read as the only figure that matters.

### Cost tier of the specific passive-climate decisions in this design

**Near-zero incremental cost (pure geometry, embedded in a building being built anyway):** orientation/window placement controlling east/west exposure; cross-ventilation room layout; stairwell-as-stack-effect chimney (12 sq ft shaft, 4–6 sq ft top vent) — no extra structure, just left open at the top; 15 in deep reveals (a detailing choice, understood per Output J as partial shading only, which is exactly why it's free); minimizing west glazing to 8–10% WWR (also cheaper — the rare case where climate-correct and cheap coincide); roof falls/parapet upturns (mandatory regardless of climate intent).

**Baseline, not upgrade:** insulated roof assembly — already priced inside the 2–3% roof-treatment share of grey cost, estimated PKR 40–70/sq ft roof-area delta over an uninsulated slab.

**Low cost:** external lime/cement plaster upgrade (~PKR 95–130/sq ft delta); operable high-level vents and jali screens (MS grill PKR 700–1,200/sq ft over the vent-opening area only); **Grade 60 vs. Grade 40 reinforcement steel** — <2% price delta for a ~50% strength gain, the single best-value structural decision in the project.

**Medium cost — a genuine trade-off, not a straightforward upgrade:** **AAC block or insulated cavity wall in place of 9 in solid brick.** ⚠ This design's night-flush/winter-retention mechanism (Output J) depends on **exposed high-mass** walls — 9 in brick is the baseline for that reason, not an oversight. AAC reduces conductive gain but undercuts the night-flush strategy this document is built around; if explored, it should be scoped as an **alternative wall strategy**, not adopted as a drop-in upgrade. Masonry+plaster is 10–15% of build — any change moves real money regardless of direction. Upgraded window glazing (PKR 750–1,400/sq ft) is a genuine optional upgrade, since the passive strategy already works with standard glazing given the WWR/reveal strategy above.

**Higher cost/explicitly optional backup layer:** solar PV (inside the 3–5% electrical finishing line, a later add-on once passive load reduction is achieved); solar water heating (inside the 1–3% plumbing finishing line); high-efficiency split AC as **backup only** for the 4–6 peak summer weeks the passive system can't fully cover — deliberately the last line item to spend on, not the first.

### Bottom line

Nearly every genuinely climate-responsive decision here — orientation, the stairwell vent, the reveals (honestly stated as partial-shading), minimal west glazing, night-flush-capable openings, the baseline insulated roof — sits in the near-zero or already-baseline cost tier, because it's a geometry/detailing decision made once at design stage, not equipment purchased repeatedly at operating stage. AAC-vs-mass-walls and upgraded glazing are flagged as genuine trade-offs/optional spend rather than folded in as free wins, and solar PV/hot water/AC are explicitly positioned as backup. This is the core argument for building this way at 1.10 Cr–1.53 Cr all-in schematic-stage cost rather than treating climate response as something only a premium house can afford.

---

# 5 Most Important Design Decisions

Ranked by effect on thermal comfort and energy consumption, with reasoning.

**1. Orientation-driven massing — long walls north/south, short walls east/west.**
On this 25×45 ft geometry, the east-open case gets this alignment for free (Section 2/Output A.6): the two largest wall areas face the climatically favorable directions, and the two facades absorbing direct low-angle sun are only 25 ft wide each. Every other passive strategy in the document (chajja sizing, WWR targets, buffer-zone placement) is downstream of this one geometric fact, and it costs nothing — it's a consequence of how the plot was entered, not a purchased feature. Get this wrong (e.g. by choosing north- or south-open without re-checking Output A.5's adaptation notes) and the long walls flip to east/west, the harder alignment, and every downstream WWR/shading number needs re-deriving.

**2. Minimizing west-facing glazing and placing the stair/bath/store buffer on the west wall.**
Section 5's D=H/tan(altitude) arithmetic shows no horizontal overhang can shade a west window at any buildable depth (the math demands >4m at this latitude's afternoon sun angle). This is the single largest avoidable heat-gain path on the house if ignored, and the fix (8–10% WWR, low-occupancy buffer rooms absorbing the exposure) is near-zero incremental cost per Output K — it is a placement decision, not a purchase. Getting this wrong means every bedroom/living room on the west wall inherits an unshadeable afternoon heat load for the life of the building.

**3. The insulated, reflective, inverted-membrane roof assembly (Section 10) — not a ventilated air-gap roof.**
The roof is the single largest solar-gain surface on a low-rise house this size. The inverted/protected-membrane build-up (XPS above the membrane, reflective top finish) resists ≈2.0–3.5 kN/m² of added dead load's worth of thermal performance for a modest cost premium already folded into baseline grey-structure cost (Output K) — it is not optional finishing, it is the mechanism that keeps the first-floor ceiling from radiating stored daytime heat into the rooms below all summer evening. Skipping it (a plain uninsulated slab) would undo a large share of every other passive strategy in the document, regardless of how well orientation and shading are handled.

**4. The stairwell/light-well fused stack-effect ventilation chimney (Sections 2, 6, Output E).**
This is the one mechanism in the entire design that works under either plot-orientation outcome from §3.0 (corner/side-open or mid-row fallback) and with zero outdoor wind — it is buoyancy-driven, powered by solar heating of the mumty and roof alone. It delivers cross-ventilation, daylight, and exhaust from a single small (4×6 ft to 8×10 ft) volume that would otherwise cost circulation area twice over. Its effectiveness is entirely occupant-operated, though (open in summer, throttled in winter, per Section 4) — the mechanism only works if the household actually operates the vents, which is why this is flagged as a behavioral commitment, not a fire-and-forget feature.

**5. Exposed internal thermal mass (9 in solid brick/RCC, not AAC, on the walls doing the night-flush/winter-retention work).**
Section 3's two-mechanism thermal-mass note and Output J's explicit tension with AAC make this the decision most likely to be silently undone by a well-intentioned material substitution. Night flushing (free summer cooling) and winter heat retention (free winter heating, contingent on the south face being open per §3.0) both depend on dense, exposed masonry absorbing and slow-releasing heat on a daily cycle. Swapping the primary mass walls for a low-mass insulator like AAC — even though AAC reduces conductive gain — would trade away this entire mechanism, which is why Output K flags AAC explicitly as an alternative strategy rather than a compatible upgrade. Getting this one wrong doesn't just reduce performance at the margin; it removes an entire free heating/cooling system the rest of the document assumes is present.
