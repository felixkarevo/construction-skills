> **LEGACY WORK LOG — ARCHIVAL RECORD.** Raw log of building the demo model
> (originally a 5-marla house in Rawalpindi). Kept for its honest documentation
> of failures, fixes and FreeCAD API discoveries; the verified findings were
> distilled into `skills/construction-freecad-bim/SKILL.md`. Ignore
> jurisdiction-specific assumptions; do not treat as current guidance.

# House5Marla_Rawalpindi — Work Plan & Log

Goal bar: match the real-BIM completeness/detail level of Yorik van Havre's `house_brenon.FCStd`
(526 objects: real `Space` rooms, `Furniture`, 16 named material layers, `Roof` objects, real
quantities) — downloaded and inspected directly earlier in this project, not just described.

Rule for this plan: FreeCAD is a single live stateful document. Research/spec/critique work is
fanned out to parallel agents. Anything that writes to the live model is applied by the lead
agent (me) sequentially, one item at a time, each verified (bbox/volume/clash-check + full
forced recompute with zero Invalid objects) before moving to the next — same discipline used
for the stair rebuild, the Normal-property fix, and the bathroom-width fix earlier in this
project. No parallel writes to the model, ever.

## Task list and assignment

| # | Task | Assigned to | Status |
|---|---|---|---|
| A | Reinforcement spec for remaining structural members (columns/beams/footings/slabs), ACI min-steel checked | gauntlet worker A (research+build+critic vs house_brenon's real quantity/material rigor) | PENDING |
| B | FEM verification priority list — next 3-5 highest-value unverified members per skill §9.10 | gauntlet worker B | PENDING |
| C | Boundary wall + gate + parking bay design, sized for this 5-marla plot | gauntlet worker C | PENDING |
| D | Real fixture geometry plan (WC/basin/sink) — feasibility of importing real parts vs. building better placeholder geometry | gauntlet worker D | PENDING |
| E | Electrical documentation spec (panel location, circuit list) — no FreeCAD modeling tool exists for this, output is a schedule not geometry | gauntlet worker E | PENDING |
| F | Foundation-upsizing load recalculation for a hypothetical future G+4 — calc only, NOT applied without explicit user confirmation (real cost trade-off) | gauntlet worker F | PENDING |
| G | Apply already-specified gauntlet-loop items (glazing U/SHGC/VLT properties, insulation buildup, night shutters, transfer grilles) | lead agent (direct FreeCAD application) | PENDING |
| H | Stair headroom — run the real raycast measurement (skill §10.5), replacing the current estimate | lead agent (direct FreeCAD application) | PENDING |

## Log

**2026-08-21 — Gauntlet workflow (6 tasks) completed, results verified against live document, not taken at face value.**

- Task A (reinforcement): real spec produced (load takedown, seismic base shear 179.3kN, wall density 4.29%>=2.5% PASS). Rebar objects claimed "added" in the checklist were NOT actually found in the live document on verification (still only 1 rebar object exists). Spec is good; application did not happen — redo as a lead-agent task.
- Task B (FEM priority): **real finding, verified live** — `FEMCheck_RoofBand_Front` document exists with a real solved CCX_Results, max von Mises 56.64 MPa. Investigated the cause directly: RoofBand_Front spans 7620mm between only the 2 corner tie columns (TieColumn_NW_corner, TieColumn_NE_corner), no intermediate column — BUT this band sits on continuous masonry wall for its full length in reality, so the FEM test's "free-spanning beam" idealization is almost certainly wrong/overly conservative, not proof of a real design failure. Open item: re-run with a continuous-support idealization before treating this as a defect requiring intermediate columns.
- Task C (boundary/parking): detailed spec produced (dwarf wall + MS grille + pilasters + double-leaf gate + wicket + parking apron). NOT applied to the live model yet.
- Task D (real fixtures): recommendation produced (improve placeholders rather than import full complex parts). NOT applied yet.
- Task E (electrical): schedule produced. Claimed writing it to a `DB_Panel_Main` object's Description — verified this object does NOT exist in the live document. Redo.
- Task F (foundation upsizing): calculation-only as instructed, correctly did NOT touch the live model. Real geometry cross-checks were done (26 walls, 9 footings, 14 columns confirmed) before the calc — good practice, no application pending (by design).

**Lesson recorded:** workflow agents' own "DONE" checklist claims are not reliable without independent verification against the live document — several claimed actions did not actually persist (likely due to running against a shared live FreeCAD document from parallel pipeline stages). Always verify post-hoc via get_object/execute_code, same as every other claim in this project.

**2026-08-21 — 4 parallel agents dispatched to apply tasks A/C/D/E to the live model, each scoped to disjoint objects, none allowed to call doc.save(). Outcome:**

- **Task A (reinforcement) — DONE, verified.** 81 new rebar objects across 5 members (TieColumn_NW_corner, StripFooting_Front, PlinthBeam_Front, RoofBand_Part_LoungeStair, a Slab_First bay), IFC-confirmed 1→82 IFCREINFORCINGBAR. Found and fixed a genuine new bug independently (bar mis-placement when Direction runs along a centered vs. corner-based host axis — needs folding into the skill's gotcha list). Flagged, not hidden: StripFooting_Front's dowels only get 185mm development length vs a 360mm target (open item), and 2 of 4 column corner dowels oversail into the untouched StripFooting_North (open item, that footing's owner needs to know).
- **Task D (fixtures) — DONE, verified.** All 7 fixtures upgraded from flat boxes to real compound geometry (WC bowl+cistern, basin+pedestal, double-bowl kitchen sink), "Sanitaryware White" material assigned, zero clashes confirmed via actual solid-intersection volumes (not visual), room-envelope containment checked against live wall positions.
- **Task C (boundary/parking) — NOT DONE.** Agent was stopped before building anything. No boundary wall, gate, or parking exists.
- **Task E (electrical) — NOT DONE.** Agent was stopped mid-verification. No DB panel object exists.

Final integrity check: full forced document recompute, 0 invalid objects, single save performed by the lead session (559 total objects). Tasks C and E remain open — did not restart without explicit direction to do so.

**2026-08-21 (later) — user said "don't stop, complete the work". Retried C and E, plus expanded reinforcement (10 more members), FEM-verified 3 more members, and applied the glazing/insulation properties — all 5 as parallel agents on disjoint objects, none allowed to save.**

- Boundary wall/gate/parking (C) — DONE. 20 objects built. Found the requested 9x18ft parking bay genuinely does not fit this plot (veranda + zero side-setbacks leave only ~1.8-2.2m); built the largest real apron that fits (3.89m2) and said so honestly instead of mislabeling it. Gate swing clash found and fixed (both leaves swing outward).
- Reinforcement expansion — DONE. +90 bars across the remaining 10 tie columns (172 total now, was 82). Caught a real Sketcher face-attachment bug (bars landing outside the host on 10 columns despite identical-looking face geometry to a working original) and fixed it before reporting done.
- Glazing/insulation properties — DONE. 15 windows/doors got real U/SHGC/VLT properties, roof got SRI values, 6 walls got insulation buildup notes. Did not touch the corrupted Normal property. Caught that the task's example (Door_VestibuleInner) was wrong about which door has real glass.
- Electrical (E) — DONE. DB_Panel_Main built in the vestibule, verified clear of both door swings, real multi-group RCD/RCBO circuit schedule, 5 real Arch::Space room objects created (didn't exist before).
- FEM verification (B) — INCOMPLETE / caused an incident. One of the 3 planned checks (a chajja cantilever) used an oversized ~560k-node mesh that hung the FreeCAD GUI thread for 20+ minutes and the process crashed. FreeCAD was restarted; crash-recovery preserved all in-memory work from the other 4 agents (verified: 773 objects, 172 rebar, DB_Panel_Main, 15 boundary objects all present) — saved immediately after restart. The chajja FEM check itself was not completed; whatever the other 2 of 3 planned FEM checks in that task achieved is not yet confirmed against the live document.

**Lesson recorded:** always cap FEM mesh CharacteristicLengthMax explicitly for small/thin members (chajjas, fascias) — an unconstrained mesh size on a large thin cantilever can generate an enormous element count and hang the GUI thread with no clean way to cancel. Verify node count is in the expected low-thousands range before letting a solve run to completion.

**2026-08-21 (later still) — finished the pending FEM/headroom work directly (not delegated, to avoid repeating the crash), mesh size explicitly capped and checked before every solve:**

- **StripFooting_North FEM check — PASS.** Real load takedown (118.9 kN/m line load from 4.91m tributary width, the heaviest-loaded footing), mesh capped at 150mm (14,113 nodes, verified sane before solving). Result: 0.132 MPa vs 2.77 MPa concrete cracking stress — large margin. Hand-check (0.091 MPa bearing pressure) within reasonable range of FEM result.
- **TieColumn_NE_corner FEM check — PASS.** Real tributary load (168.9 kN factored axial), mesh capped at 60mm (16,767 nodes, matching the previously-converged density from the SE-corner check). Result: 3.863 MPa vs 11.25 MPa (0.45f'c) screening limit — comfortable margin. Hand-check (3.193 MPa) within 21% of FEM.
- **Stair headroom — measured by real raycast, not estimate.** Cast vertical rays from 5 points across both ground-floor flights and the landing up through the model; every point's first real obstruction is the mumty roof at Z=8600mm, meaning 7,000mm+ clearance everywhere — vastly exceeds the 2,032mm code minimum. This was flagged as "still an estimate" for most of the project; now definitively verified.

Full recompute after all three, 0 invalid objects, saved (773 objects, unchanged count — these were verification-only in separate FEM-check documents, no new objects added to the main house model).

**2026-08-21 (later still) — "don't stop, complete the work" again. Expanded reinforcement to full coverage of all real tie columns/footings/tie beams, done directly (not delegated), each batch verified before moving on:**

- **3 remaining tie columns reinforced** (`TieColumn_S_T_Z1Z2`, `TieColumn_N_T_Z2Z3`, `TieColumn_S_T_Z2Z3`) via global-coordinate wire placement (avoiding the earlier Sketcher face-attachment bug) — all verified inside host bbox. 14/14 tie columns now reinforced.
- **7 remaining footings reinforced** — 2 initially failed the ACI minimum-steel check (533 vs 540 mm²/m required), fixed by incrementing bar `Amount` by 1 each, re-verified PASS. 9/9 footings now reinforced.
- **16 tie beams reinforced** (all `PlinthBeam_*`/`RoofBand_*`, confirmed zero `Subtractions` so a standard cage applies) — batch script triggered a `gui_dispatch: "stuck"` state for ~183s; correctly diagnosed as bounded geometry work (not an unbounded solver loop like the earlier mesh incident) rather than panicking, and it resolved on its own. All 16 confirmed as rebar hosts.
- **Investigated an apparent containment failure on the new tie-beam rebar** — 2 spot-checked beams showed bars extending past the nominal beam bbox. Traced to two separate things: (1) `Arch.makeRebar`'s default `OffsetStart`/`OffsetEnd`=30mm, zeroed out on all 16 beams' bars since 30mm was too short to be a real lap/anchorage length and was just a cosmetic default; (2) after zeroing offsets, containment checks *still* failed by ~4mm — traced this to the closed stirrup bar's own radius (half of an 8mm bar diameter) legitimately poking past the theoretical zero-thickness wire endpoint when the stirrup is drawn flush with the beam end — not a real defect. Re-verified all 16 beams' bars with a bar-radius-aware tolerance: **genuine PASS on all 16**, confirmed via BoundBox, not narrated.
- Full recompute (0 invalid objects), saved: **1003 total objects, 287 reinforcing bar objects** (was 773/172).

**Reinforcement coverage is now complete for all primary structural members**: 14/14 tie columns, 9/9 footings, 16/16 tie beams. Still open: 27 lintels and 10 decorative fascias/fins (lower structural priority, explicitly deferred), FEM verification still only covers ~4-6 members out of ~90 structural objects (small fraction, say so if asked), foundation upsizing for a hypothetical future G+4 remains parked pending the user's explicit go-ahead (not done without asking, per this project's standing rule).

**Lesson recorded:** a bbox-containment check needs a tolerance that accounts for the checked object's own thickness/radius (e.g. bar diameter), not just a flat few-mm fudge factor — otherwise a real, correctly-detailed stirrup drawn flush with a member's end reads as a false "outside host" failure. Added to the running list of FreeCAD/verification gotchas.

**2026-08-21 (later still) — user directly challenged door/stair quality ("is this what great design looks like?"). Investigated live, found a real unresolved defect from earlier in the project, fixed and verified it properly this time:**

- **All 12 door objects (11 interior + vestibule) were lying flat, buried below the floor** — not standing upright in their wall openings. Traced root cause: the earlier "Null Shape" crash fix (reverting `Normal` to its default `(0,0,-1)`) stopped the crash but left doors building as flat horizontal panels, not vertical leaves — this was reported as fixed at the time, but only `Shape.isNull()==False` was checked, not actual sane geometry. That was a real gap in my own verification discipline.
- Diagnosed the actual local-to-world transform empirically (Placement-based, not sketch-based — the sketch's own Placement has zero effect on the built shape): doors whose raw (identity-placement) shape carries `Height` along local X need `Rotation(Y-axis, -90°)`; doors carrying `Height` along local Y need `Rotation(X-axis, +90°)`. Verified this rule on 2 doors by hand before batch-applying.
- A first batch-fix attempt used ambiguous sorted-span matching to pick the rotation and got it wrong for 10 of 12 doors (including re-breaking the 1 door already hand-verified correct) — caught by re-verifying against each door's own `Void_*` object's BoundBox rather than trusting the batch's own success claim, consistent with this project's standing rule.
- Redid it with the deterministic per-axis classification rule above: **all 12 doors now verified standing upright, fully inside their own opening's BoundBox** (5mm tolerance). Full recompute (0 invalid), saved (1003 objects, unchanged count — this was a Placement fix, no new objects).
- Checked windows for the same defect (14 total) — all genuinely fine; 8 initially looked suspicious under a naive Z-span heuristic but turned out to be legitimately small square vent windows with modest real frame depth, not flattened leaves.
- Checked the dog-leg staircase (both flights, both landings) — geometrically continuous, no real gaps. The one apparent 160mm gap between the top flight and the floor level is the last riser (floor edge = final tread, a standard design), confirmed matching the stair object's own declared `RiserHeight=160mm` property exactly, not a defect.

**Lesson recorded:** "shape is not null" is not the same as "shape is geometrically sane" — any fix to a null-shape crash must be re-verified against the object's actual BoundBox/orientation, not just the absence of the crash, before being reported as resolved.
