---
name: construction-drawing-sketching
description: >
  Technical representation for construction design (DACH practice, German terms
  in parentheses): freehand sketch workflow (tools, 6-step build-up, line/area
  technique, tracing variants, execution levels); projection families with
  working angles (orthographic Normalriss, cavalier/cabinet, isometric/dimetric/
  trimetric, 1-/2-/3-point perspective incl. VP-distance rules 40-50 deg -> ~2.5x
  crop width, 70 deg -> ~1.5x); ellipse and cylinder construction (1:1.7 iso
  template ratio, major-axis-perpendicular-to-vanishing rule), cast-shadow
  construction (6 steps, 10-15 deg shadow / 15-20 deg light lines), division
  methods (Diagonalmethode, Strahlenmethode), Einschneideverfahren section-cut
  method, human proportion anchors (head = 1/8 height); CAD & drawing
  conventions - line type/width to meaning mapping (0.13-2 mm series, 1:2:4
  ratio), section conventions and material hatch families (Beton, Mauerwerk,
  Holz, Daemmstoff, Metall per DIN 919/EN ISO 128 scope), dimensioning
  discipline (units per trade: Beton m / Holz cm / Stahl mm, level symbols
  Rohbau solid vs Fertigmaß open triangle, +0,00 = finished ground floor),
  scale series (ISO 5455) and plot sizes (A0-A4, margins, title block), layer
  and text conventions, BIM/IFC/CDE pointers; plan-set types and purposes
  (Vorplanung through Bestandsplan with their standard scales); reading and
  producing sections and details (layer-stack thinking, Stiftregel continuity);
  the sketch -> model -> screenshot communication loop with FreeCAD via
  neka-nat/freecad-mcp (get_view with view_name Isometric/Front/Top/Right,
  include_screenshot false for intermediate iterations); drawing QA checklist,
  common mistakes, and a DE<->EN term bank. Design guidance, not a normative
  substitute - all standard numbers carry VERIFY tags where the compiled
  reference material did not state them verbatim.
---

# Construction Drawing & Sketching (Bauzeichnung / Skizzieren)

> **Simple-first gate (governs how this skill is applied).** Default every choice here to
> the *simplest proven* solution at the agreed standard tier — see the governing skill
> `simple-first-building` (complexity ladder §1). Escalate to more demanding construction
> (innovative systems, one-off details, higher comfort tiers) only when the client
> **explicitly** asks for it, with cost/schedule impact stated; deviate **below** the usual
> standard or the aarRdT only via the documented risk-acceptance machinery
> (`simple-first-building` §3) — public permission never cures the private default.

## 0. When to load this skill

Load when the task involves any of:

- Communicating a design idea before or alongside CAD: concept sketches, presentation
  sketches, variant comparisons, site instructions, RFI markups.
- Choosing a representation form: "Do I draw this as a floor plan, a section, an
  isometric, or a two-point perspective?"
- Freehand technique: placing ellipses, constructing cast shadows, dividing facades
  in perspective, drawing people or scale figures, linework quality.
- Producing or reading conventional construction drawings: line weights, hatching,
  dimensioning, scales, sheet layout, title blocks, plan sets (Planarten).
- Working with the FreeCAD MCP: turning sketches into models and back into pictures
  (sketch -> model -> screenshot loop, section 10); QA of any drawing before it
  leaves the workspace.

Not for: structural calculation, fire/thermal design, or legal compliance - those
live in their own skills. This skill owns *representation*: how a design is seen,
drawn, and read.

## 1. Mental model: three registers of representation

| Register | German | Goal | Exactness | Speed |
|---|---|---|---|---|
| Sketch | Skizze | capture/think/communicate an idea | approximation, essentials only | seconds-minutes |
| Drawing | Zeichnung | unambiguous instruction for execution | geometrically and normatively correct | hours-days |
| Model | Modell (CAD/BIM) | consistent data, derived views, quantities | parametric, checked | iterative |

A sketch per classical definition is a "drawing thrown off with coarse strokes,
limited to the essentials, serving as a draft" (mit groben Strichen hingeworfene,
sich auf das Wesentliche beschränkende Zeichnung, die als Entwurf dient). Boundaries
are fluid; the key deliberate decision at the start of every representation task:

1. **What** do I show? (message, not object)
2. **For whom**? (customer, executing trades, own thinking, authority)
3. **In which form**? (representation family, section 3)
4. **At which level of detail**? (execution level, section 2.6)

Purpose spectrum: find solutions, compare variants, optimize, communicate, analyze,
understand spatial/functional relationships, structure information, document,
think on paper. Early-phase sketches are the cheapest place to fix decisions -
once the design is in CAD, changes get expensive.

## 2. Freehand workflow: tools, technique, sequence

### 2.1 Materials and tools (principles, brands optional)

- **Paper**: plain white ~80 g/m² printer grade, **A4 landscape** default; A3 when
  more space is needed or vanishing points must sit on the sheet; cheap ~50 g/m²
  sheets are more transparent - best for tracing (Durchpausen) and copier/scanner
  feeds. Grid/dot paper for 2D orthographic sketches.
- **Construction lines**: hard, light pencil (medium hardness, e.g. B2-class) - never
  for final linework: graphite is gray/silvery and fades in copies and scans, which
  is exactly what construction lines should do.
- **Final lines**: dark, sharp colored pencil or fineliner; sharpening angle controls
  stroke character. Dark hues for lines (light-colored lines read unclearly); don't
  make technical sketches overly colorful.
- **Markers**: brush markers in transparent grades for cast shadows - one dark, one
  mid gray, one light gray (the light gray reads through glass-shadow interiors).
- **Templates/underlays (Vorlagen/Unterlagen)**: printed sheets with pre-drawn
  isometric axis grids or 2-point setups (horizon at top edge with VPs just outside
  the side edges; VPs in upper corners with divided base plane; mid-height horizon
  with VPs at side edges). Use when VPs fall off-sheet; draw lighter than the guides.
- **Color semantics** (convention, not normative): blue = metal, cool, water,
  pneumatics/hydraulics, fluids; red shades = important/critical/dangerous/hot;
  green = safe/done; orange = active/robotic; brown = wood.
- **Digital**: pressure-sensitive stylus + paper-feel foil, graphics tablets, sketch
  apps. Manual pen/paper is a deliberate counter-rhythm (do -> see -> do); combine:
  scan paper, annotate digitally.

### 2.2 Line and surface technique

- *Linie* (line) = visible form/contour; *Strich* (stroke) = the way a line is drawn.
  Character comes from stroke weight, swing, rhythm, tool.
- The eye is picky about learned expectations: parallelism, equal divisions, verticals.
  Deviations are instantly noticed - use ruler/compass/templates where needed, then
  **retrace final lines by hand** to keep sketch character. Construction lines may
  stay visible.
- Long generous strokes tend straighter than short nervous ones. Don't erase a wrong
  stroke - redraw until direction fits; a sketch tolerates incidental strokes. For
  long target-precise lines, interrupt the stroke to correct direction; brace the
  hand on the table edge for the first horizontal/vertical lines.
- Practice drill: horizontal/vertical/diagonal, parallel, converging-to-point lines;
  thin construction, retrace, thick direct; straight, curved, exact ends, flowing
  ends; surfaces angular/round/free-form, hatched (Schraffuren), patterned, filled.
- Areas: fill solid, or hatch/pattern in varying directions. Hatching = dynamic;
  patterns = structure; fills = volume. Edge/transition lines stay black or dark so
  forms remain readable under coloring. Fillet/rounded-edge lines **thin** (thin
  continuous line reads best), main contours strong - graded weights stay legible.

### 2.3 The standard 6-step build-up

1. Thin pencil construction lines - generous and as long as possible (they control
   directions toward the vanishing points and parallelism).
2. Lightly emphasize the first contours of the reference space (Bezugsraum) /
   primary geometries.
3. More detailed contours (pencil or colored pencil).
4. Final contours retraced with colored pencil; work **front to back** so hidden
   edges are not accidentally thickened. Save a copy/scan before and after retracing.
5. Add form shadow (Eigenschatten).
6. Add textures, text, cast shadow (Schlagschatten), other additions.

Fast sketchers may go straight to final pen; stepwise build-up is usually better.
If the start collapses (line soup, sloppy verticals): retrace essentials onto a
translucent sheet and restart rather than rescue. 2-point setup order variant:
horizon per desired eye height -> VPs + basic Bezugsraum proportions -> rough
contours -> emphasize essentials -> final.

### 2.4 Tracing, copies, variants

Durchpausen (tracing/overlay) is a workflow, not a shortcut. Use it to: make variants,
rescue cluttered or wrong sketches, replace erasing, produce a clean version without
construction lines, merge elements from several sheets, recover when construction
lines show too weakly (hold sheet against a window, use 50 g/m² paper, or a light
box). Copier/scanner uses: variants, securing intermediate steps, **before** adding
text or shadow, combining with digital. Keep each sketch element at the same sheet
position when merging via tracing.

### 2.5 Simplification devices

- Profile tubes drawn as single thick strokes; sheet-plate end faces as thick lines only.
- Break lines where foreground geometry hides background profiles - keeps readability.
- Full solid -> "box with lid" by emphasizing a few lines.
- Reduce patterns/divisions to the suggestive minimum (big efficiency gain; bold
  strokes for the reduced set).
- Schematic motion units naming the axes instead of full kinematics.
- "Sketching means simplifying": detail level strictly per task and audience.
- Hint, don't resolve: unclear areas may stay rough - the sketch is finished in the
  viewer's imagination.

### 2.6 Execution levels and perspective psychology

Raise completion only as the message requires: 1 outline; 2 + filled colored-pencil
base tone (usually enough to communicate a solution); 3 + form shadow (cheap 3D
boost - recommended at every level); 4 + cast shadow (presentation grade - copy
before adding); 5 + textures/text; 6 marker rendering grade. Success criterion is
NOT finish for its own sake: meeting the audience's expectations.

Same object, different message: isometric = factual/technical/compact/neutral;
2-point with high horizon + wide VP distance = natural eye-level impression;
mid horizon + narrow VPs = close, examining/analytical gaze; low viewpoint =
dynamic; 3-point bird's-eye = towers exceptionally tall; deep horizon = massive
machine; omit scale figures when size should stay open; "focus" simulation = render
the functional main area sharp, hint backgrounds.

## 3. Projection families and their angles

### 3.1 Foreshortening factor (Verkürzungsfaktor) - the underlying principle

Projected length = true length x foreshortening factor. At infinite viewing distance:
factor 1 for lines parallel to the picture plane, 0 for perpendicular lines (they
collapse to a point); range 0..1; the steeper a line's angle to the projection plane,
the shorter it appears. At finite viewing distance the factor can exceed 1 for object
parts in front of the plane (analogy: a shadow cast onto a wall by a point light).
In sketching, factors are never calculated - proportions are estimated or found by
simple methods - but the principle drives every choice below.

Scale (Maßstab) in technical drawings is chosen deliberately; in sketching it arises
from context. In 2D views, proportions run at the chosen scale and dimensioning is
directly applicable.

### 3.2 Orthographic normal views (Normalriss / Normalansicht)

The viewer looks "from infinite distance" perpendicular onto the object; principal
axes run horizontally, vertically, and normal (into the sheet); foreshortening factor
= 1 everywhere. Views: front elevation (Vorderansicht), side elevation (Seitenansicht),
plan (Draufsicht). Complex objects need further views, sections (Schnitte), hidden
lines. Normal views are the basis of technical drawings and the **easy, unambiguous
carrier of dimensions** - agree them with customer/production before CAD.

View arrangement and the first-angle vs third-angle convention (DIN EN ISO 5456-2/-3,
named in the drawing-standards ruleset): Europe/DACH practice is **first-angle
projection** (Erste Tafel: the top view sits *below* the front view, the left-side
view *right* of it). VERIFY the placement figure and the projection-symbol
convention against the standard itself before teaching or checking sheet layouts.

### 3.3 Oblique pictorials (Schrägbild / Parallelperspektiven, schiefe Variante)

- **Cavalier (Kavalierperspektive)**: front face true shape, receding axes drawn at
  ~45 degrees near full length - strong, slightly odd depth.
- **Cabinet (Kabinettperspektive)**: same but receding axis halved - the classic
  "pleasant" oblique cube.
Both keep cube edges parallel (parallel projection); fast for quick 3D blocks;
not the DACH construction default - axonometric and normal views dominate.

### 3.4 Axonometric (parallel projection, viewing distance "infinite")

- **Isometric (Isometrie)**: ONE foreshortening factor for all three axes ->
  proportions preserved; ellipses keep the same axis ratio in all three face
  directions; conditions identical across the whole sheet - a sketch is extendable
  uniformly in any direction; no horizon needed; CAD systems (including FreeCAD's
  Isometric view) use isometric as the standard principal-axes orientation. The
  default choice for exact-geometry technical/constructive sketches and for
  dimensioned 3D.
- **Dimetric / Trimetric (Dimetrie/Trimetrie)**: cube shown with differing axis
  inclinations (classical texts illustrate, no fixed angles stated). Trimetric arises
  naturally when swinging a body about an edge in isometric (section 5.6).
- The Bezugsraum (reference space) of normal views and parallel projections is
  theoretically infinite - the frame of reference gives constant geometric
  conditions everywhere.

### 3.5 Vanishing-point perspectives (Fluchtpunktperspektiven, finite viewing distance)

More realistic, limited Bezugsraum. Core vocabulary: viewpoint/eye point (Augenpunkt
AP); horizon = eye level, carries the vanishing points (FP); center of vision /
principal point (Blickzentrum/Hauptpunkt); picture plane (Darstellungsebene) -
usually between viewer and objects, may also cut through or sit behind them;
reference box (Bezugsraum); sketching crop (Skizzierbereich) = the visible area like
a photo crop - the Blickzentrum may lie outside it. The Bezugsraum may be drawn
visibly (often open toward the viewer), hinted with construction lines, or kept
purely virtual.

- **Two-point / corner view (Übereckperspektive)**: two horizontal axis families
  converge to two VPs; verticals stay parallel. Shorter VP distance relative to the
  crop = wider-angle look and stronger distortion (photo analogy: ~24 mm lens at
  ~70 degrees display angle). Distortion grows when objects sit near VPs laterally
  or far above/below the horizon, especially combined; shrinks when VPs move out
  relative to display width. Objects may slide along sight rays unchanged while
  eyepoint distance and display angle hold. If VPs go effectively to infinity,
  lines run parallel - the smooth transition into parallel projection.
- **One-point / central perspective (Ein-Punkt-/Zentralperspektive)**: special case
  of two-point with one face parallel to the picture plane; all depth lines converge
  at the Blickzentrum (the central VP); the second VP at infinity; faces parallel to
  the plane appear UNDISTORTED (only size changes with distance). Strongest depth/
  focus effect; for interiors, corridors, operator/cockpit views, extruding flat
  2D shapes with small depth.
- **Three-point (Drei-Punktperspektive)**: verticals also converge to a third VP -
  worm's-eye (Froschperspektive) from below, bird's-eye (Vogelperspektive) from
  above. Emphasizes height; suits towers, shafts, vertically dominant objects;
  more exact than 2-point but harder freehand.
- **Four-point/fisheye (Vier-Punkt-/Fischaugenperspektive)**: curved edges;
  perception is theoretically slightly curved but negligible in drawing; relevant
  only for extreme wide-angle statements about relative size vs viewing distance.
  Completeness note only - rarely draw.
- **Thales circle (Thaleskreis)**: possible eyepoint positions (in plan) lie on the
  semicircle over the segment between two VPs (constant right viewing angle on the
  VP pair). Use to derive a shared Blickzentrum / central 2-point perspective from
  two existing cube perspectives.
- **Central/symmetric two-point case**: horizontal principal axes at 45 degrees to
  the view direction; VPs symmetric about the Blickzentrum.
- **Measurement vertical (Maßvertikale)**: a vertical edge lying in the picture
  plane, shown true size and undistorted, used as height reference - take vertical
  proportions off it directly without an auxiliary plan view.

### 3.6 Quantitative setup rules for perspective (the working numbers)

- Natural-looking central two-point box: horizontal display angle **40-50 degrees**
  -> distance between the two VPs approx **2.5x** the horizontal display-area width.
- Wide-angle look: display angle approx **70 degrees** (~24 mm lens equivalent)
  -> VP distance approx **1.5x** horizontal display width; stronger distortion,
  usable deliberately for effect.
- Practical free sketching with VPs on/near sheet: use about **two thirds of the
  sheet width** as the horizontal display area (wide-angle style).
- Reference boxes are published for DIN-A4 landscape (likewise A5, A3,
  A2...) with VP distance approx 2.5x sheet width.
- Horizon placement: upper area, middle, or upper third examples given. High horizon
  = view from above; low = from below; if the object is shown entirely from above/
  below, the top/bottom sheet edge itself can serve as the horizon.
- If a face is parallel to the picture plane, all its receding edges converge
  exactly at the Blickzentrum regardless of the object's position in the scene.

### 3.7 Choosing the form (decision table)

| Task | Preferred form | Why |
|---|---|---|
| Convey extensive technical content | Isometric | uniform conditions, extendable, CAD-standard |
| Spatial immersion / "walk through" | 1-/2-point perspective | eye-level realism |
| Dimensions to be read/checked | Normal views (2D) + dimensioned iso | unambiguous carriers |
| Size impression, basic shape, operation | 2-point | natural scale |
| Degrees of freedom, kinematics | Isometric | undistorted axes |
| Section detail + text | Normal/section view | hatching + annotation space |
| Tall/vertical drama | 3-point | converging verticals |
| Process/data-flow diagrams | Isometric | extend in any direction, equal conditions |
| Interior views | 1-point (or mixed 1/2-point) | undistorted parallel faces |

Combining forms on one sheet is often best: dimensioned 2D + perspective sketch
beside each other. Role-of-form cheat sheet (multi-view object): 2-point = size
impression/basic shape/operation; isometric = degrees of freedom; normal view =
section detail + text. Per-role readability: engineers may parse a bare 2D with
arrows; customers need the perspective too - always design for the audience.

## 4. Methodical sketch workflows by representation

### 4.1 Isometric workflow

1. Lay axes: three directions 120 degrees apart (standard CAD isometric orientation);
   use an iso-grid underlay for long runs.
2. Block the subject into a cuboid Bezugsraum first; everything else is "anbauen"
   (adding) or "wegschnitzen" (carving away) off it.
3. Regular repetitions are trivially parallel along axes.
4. Ellipses: 1:1.7 template or the rotation technique (section 5.1).
5. Retrace final contours front-to-back; form shadow; cast shadow (same clock-position
   logic as 2-point).

### 4.2 Two-point workflow

1. Fix horizon at the chosen eye height (adult standing: the horizontal running
   through the object corresponds to that eye height).
2. Set the two VPs per the 2.5x/1.5x rules (or off-sheet with an underlay template).
3. Rough the Bezugsraum contours in pencil; verticals stay strictly vertical.
4. Divide horizontals with ray/diagonal methods (section 5.4); verticals need no
   correction (they stay parallel and equally spaced if taken from a known face).
5. Emphasize essentials, retrace, shadow, annotate.

If verticals drift or lines multiply: stop, trace essentials to a fresh translucent
sheet, continue there.

### 4.3 People, scenes, grounding

- Adult proportions: head approx **1/8** of body height; thigh approx equal to lower
  leg; elbow at about waist height standing; eyes at about mid-height of the head.
- Stick figures / simplified people suffice - the goal is coherence, not realism;
  more articulation to stress posture/build; faces usually omitted (eyes + mouth for
  basic emotion).
- Figures take orientation from the perspective box; **one horizon serves all
  figures at any depth** (it is the eye height); it may instead sit at a child's or
  wheelchair user's eye level; low viewpoint makes figures look big/strong.
- 2D figures are fine for quick activity/workstation sketches. Physical space
  anchoring: show the full room, hint the floor plane, or a few edges only - a
  couple of strokes ground a scene. A hinted floor gives stability, vital for non-
  compact or spread-out objects (conveyors) and whenever people are included. A
  road hint can create motion. Rooms are the central subject in interior work.

### 4.4 Arrows, motion, forces

- Proven arrowhead proportion: like traffic-sign arrows (long triangular head on a
  shaft) - fast, unambiguous. Isometric: cubic, cylindrical or simplified arrows;
  2-point: full bodies whose vanishing lines share the scene's VPs - aligning the
  base line hints the 3D orientation of the tip.
- Semantic color: red = rotation; blue = centrifugal/gripping forces; plus
  degrees-of-freedom markers, material-flow arrows on conveyors, flow + cylinder
  motion in pneumatics/hydraulics.
- Dynamics without arrows (learn from comics): hinted start point + streak lines;
  resting vs moving belt; motion carried by stroke direction in 1-point; a slight
  cast shadow lifts a jumping figure off the ground.

## 5. Geometry technique library

### 5.1 Ellipses and circles

- Geometric truth: a circle's perspective image is an ellipse constructed via its
  circumscribing square (tangent points from vanishing lines through the diagonal
  center; extra points from circle/diagonal intersections in plan transferred
  perspectively; ellipse center deviates from square center with distortion).
- Three placement methods: (a) **sketch rule** - major axis perpendicular to the
  face's vanishing direction; easy, works up to moderate distortion, fails at strong
  distortion; preferred freehand (no auxiliary squares). (b) **tangent method** -
  ellipse touches the midpoints of the distorted square's sides; closest to true
  projection, but axes appear rotated and a row of ellipses on one revolution axis
  can look wrong. (c) **geometric construction** from plan view, for exact work.
- Working rule for ALL representation forms: major ellipse axis perpendicular to the
  axis of revolution. Standing cylinder: long axes horizontal; lying cylinder:
  perpendicular to its axis toward its VP.
- Roundness cue: rounder farther from the horizon, flatter closer to it.
- Isometric templates: axis ratio **1:1.7**; pre-draw as construction lines, trace
  by hand.
- Freehand circles: "search the circle with the pen" - rotate the pencil around the
  intended form to build a line cloud, then trace clean inside it; or compass-
  pre-draw and retrace by hand (correct yet sketchy).
- Standing cylinder in 2-point: fit an ellipse to 3 tangents of a square face so the
  normal at mid long-axis points roughly to the other VP; tangents give the 4th side
  and proportions; top ellipse horizontal major axis. For multiple ellipses derive
  one, rest by feel; many lying ellipses -> less distortion (VPs farther out).
  Cube-with-ellipses: base = 3 lines of two side planes, fit, add 4th tangent +
  vanishing line of top square, complete.
- Angle division on round objects (irregularities instantly noticed): project a
  circle - which carries the true undistorted division - into the drawing plane and
  transfer points onto the perspective ELLIPSE; blade widths read off each blade's
  own ellipse. Heavily distorted lying bodies with 16-fold division read uneven -
  correct by feel, refine via tracing.

### 5.2 Shadows

- Light aids perception; **form shadow (Eigenschatten) is always recommended** - the
  cheapest 3D boost. Techniques: hatching in varying directions, patterns, filled
  tones; graded/running shadow on curved surfaces (cylinders, cones).
- **Cast shadow (Schlagschatten)**: first decide light character - sun (parallel
  rays, distance assumed infinite) vs point source (artificial; rays radiate,
  construction differs, ray-by-ray).
- Recommended default light: slightly from the front, relatively steep from above
  (vivid). Direction via the "clock position" metaphor (light from about 11 o'clock).
- Six-step cuboid cast-shadow on ground, 2-point, parallel light front-steep:
  1. horizontal helper line at the lowest point of the cuboid;
  2. shadow line at approx **10-15 degrees**;
  3. light line from the upper corner at approx **15-20 degrees measured from the
     vertical**;
  4. shadow line from intersection (2+3) toward the RIGHT vanishing point;
  5. light line parallel to (3) from the upper right corner;
  6. shadow line from intersection (4+5) toward the LEFT vanishing point.
  Fill with dark pen - sun shadows are usually very dark, commonly filled black.
- Reading the construction: shadow line (2) ABOVE horizontal (1) = light source in
  FRONT of the object; below = BEHIND; coincident/horizontal = light exactly from
  the side; tilt of light lines (3/5) = sun height (steeper = higher sun). Method
  transfers to other light directions/heights, other solids, and isometric.
- Shadow cases library: standing/lying cylinder on floor; open object with shadows
  on floor AND faces of another body; floating objects with offset floor shadow;
  where two shadow areas meet, redraw the boundary line with white colored pencil
  so contours survive; if a dark cast shadow swallows important elements, make it
  transparent (mid-gray brush marker) or lift it; orient objects so important
  elements face the light ("Sonnenseite"), or adapt the light. Behind glass: keep
  transparency - glass-door cast shadows in gray marker, varied intensity, copy
  before adding. Sometimes shadows ARE the message: combine normal views, isometric
  and the operator's central perspective on one sheet.

### 5.3 Divisions and patterns - terminology

Teilung/Unterteilung (division) = total length/area known, split into parts;
Muster/Wiederholung (pattern/repeat) = first spacing known, repeated onward (same
sense as a CAD "pattern"). Perception tolerance is LOW: non-parallel louvers, wrong
spacings, off-vertical edges are instantly seen through - fix by tracing over with
helpers on critical zones; long flat converging lines: use a long ruler.

### 5.4 Diagonalmethode (diagonal/bisection method)

- Needs a rectangular face. Bisect via the diagonals; halve successive sub-rectangles
  repeatedly; verticals through diagonal centers give the division. Applied directly
  in the geometry, no extra construction.
- Limited to even divisions (powers of 2 via repeated halving).
- Pattern repetition variant: draw a vanishing line through the rectangle center to
  the VP; then a ray from the bottom-left corner through the intersection with the
  first vertical; the next vertical rises where that ray crosses the top vanishing
  line; repeat.

### 5.5 Strahlenmethode (ray method with helper VP)

- Arbitrary division count. Step off the true (undistorted) spacing on a helper
  line, connect to a helper vanishing point (Hilfsfluchtpunkt), project down into
  the perspective.
- For results EXACTLY matching true division, two conditions must hold: the helper
  VP lies **on the horizon**, and the helper line carrying the true spacing runs
  **horizontally (parallel to the horizon)**. Otherwise the helper VP position is
  free.
- Choose arrangements with favorable crossing angles (accuracy), keep construction
  clear of the object (clarity), fit sheet space; to limit clutter, reuse the
  perspective's own VPs as helper VPs.
- Both methods agree and combine (e.g. push-button panel: ray + diagonal to divide
  the face, then diagonals inside each button hint the embossed key contour).
  Horizontal (lying) faces: divide both edge directions accordingly; checkerboard =
  classic 64-field division; floor quartered via diagonals, then 16 fields; with
  farther-out VPs the field-size difference reads smaller.
- Stairs in 2-point (the classic combo): vertical risers stepped off on the
  Maßvertikale (= front edge of the Bezugsraum); shortening along the horizontal
  axis to the VP via the ray method; step profile from the intersection points;
  complete step-by-step to the far side.
- Division methods also serve freehand as mental support without full construction.

### 5.6 Swing/rotation of bodies

- **Isometric swing about an edge** (lid, joint): 1) base body; 2) swing ellipse
  (Schwenkellipse) tangent at the point being swung; 3) pick the swing point at the
  desired angle on it; 4) body edge tangent at the swing point; 5) complete the
  swung cuboid. Result is a TRIMETRIC parallel geometry (edges still parallel); for
  the second top edge add a second ellipse to read its foreshortening; the 1:1.7
  iso template is usable for iso swing ellipses.
- **Swinging in 2-point**: rotating a cuboid about a vertical edge moves its
  receding VPs ALONG the horizon - they can leave the sheet and re-enter from the
  other side; a hinge edge and lid lines may share the same left VP. Do the helper
  construction on a separate sheet and trace the actual sketch onto it (tidy result).
- Governing principles of horizontal rotation in 2-point:
  - ONE horizon per sketch (= eye height, valid for all objects);
  - VPs of horizontally rotated bodies shift only along the horizon, independent of
    object height; both VPs travel in the SAME direction, accelerating outward as
    rotation grows (their lines flatten);
  - ONE shared Blickzentrum on the horizon = main viewing direction;
  - rotate a face until parallel to the picture plane -> its horizontal VP goes to
    infinity, depth lines converge at the Blickzentrum = the 1-point case (the
    Blickzentrum IS that object's second VP);
  - very flat lines meet outside the sheet; verticals stay vertical;
  - intersection points of flat lines travel faster along the horizon the flatter
    the lines;
  - same geometry at different depths = same proportions, different size only;
  - all horizontal edges of stacked rotated objects converge at the horizon VPs
    regardless of height.
- **Free spatial rotation**: rotate cuboids successively edge-to-edge from a fixed
  base (e.g. SCARA robot axes at arbitrary swing angles); pick a convenient
  envelope box (Hüllquader) - e.g. wheel steering: envelope covers half the wheel
  up to the steering axis, swing the envelope per method, mirror to the back to fit
  the whole wheel. If initial and swung geometry overlap confusingly, retrace the
  essentials.
- Discipline: use constructive methods only until rough proportions/directions are
  clear, then finish freehand; skip a method step once the gist is fixed.

### 5.7 Einschneideverfahren (section/intercut method) - isometric

Standard technique for architectural sketches, technical drawings, complex geometry:
spatial properties are rendered 2D via cutting planes -> projection + section views.

- Projection-plane axes placed symmetrically to the main isometric axis; interior /
  hidden information appears in the projected section planes.
- The foreshortening factor is geometrically derivable for isometric, and it equals
  **1 in all projection views** - so a dimension h transfers directly from front
  view into the auxiliary projection; dimensions a, b transfer from the floor plan
  (Grundriss) into the front view (Vorderansicht), generating further
  intersections/lines.
- Roof example (the classic case): a roof-valley (Dachkehle) intersection point is
  NOT uniquely fixable in the isometric view alone -> add the projection view,
  construct the intersection there, transfer it back with red arrows.
- Prism/cylinder/rotated-box penetrations: shift projections along projection lines
  to save paper; few well-defined points suffice to hint a coherent intersection
  curve; flat crossing-angle inaccuracies are absorbed by neighboring points;
  distances transferred with compass or ruler; finish by tracing a clean copy.

### 5.8 Exact 2-point construction (when freehand must be checked)

- Base = plan view (Draufsicht) + side view, or plan view + height data.
- VPs and Blickzentrum found in the plan view: extend lines parallel to the main
  axes from the eyepoint onto the picture plane, transfer those intersections onto
  the horizon.
- Verticals via side view OR the Maßvertikale (true-length vertical in the picture
  plane as height reference); irregular horizontal spacings projected from plan;
  irregular heights taken off the Maßvertikale; rotated boxes: points projected
  from side views onto the Maßvertikale.
- Recommendation hierarchy: freehand FIRST, directly in perspective, ideally without
  auxiliary views; constructive methods for understanding and checking critical
  spots; many division/rotation methods work freehand as mental support.

### 5.9 Free-form solids: Schichttechnik (layer technique)

For airplane/handle/submarine-class forms (curved in all three dimensions):

1. Subdivide the Bezugsraum into reference geometries (Bezugsgeometrien).
2. Define several cross-sections in planes perpendicular to the main axis.
3. The "corners" of the cross-sections are the spatial anchors.
4. Connect anchors with freehand fairing/flow lines (Verlaufslinien) - the surfaces
   between are NOT constructed, they emerge.
5. Shading reinforces the form; fine continuous contour lines (fineliner); final
   clean drawing via tracing of combined geometries.
- Helper surfaces may "meander"/"taper" along the form; a water surface can serve as
  the horizon.

### 5.10 Intersections (Verschneidung/Durchdringung) and tricky transitions

- Intersection/penetration of solids = the shared region when bodies cut through
  each other; analyze in CAD first if needed; often only roughly hinted is enough -
  function stays legible (e.g. isometric multi-pipe fittings with coarse junctions).
- Cube-cylinder transition case study: pure 2D views leave geometry unclear;
  ellipses fitted along vanishing direction fail at strong distortion (no
  side-midpoint contact). Options: "geometric camouflage" = let ellipses follow the
  vanishing direction AND share a continuous common tangent; larger VP distance
  reduces distortion and eases fitting; modified geometry with deliberate gaps
  defuses critical transitions; individually tangent-fitted ellipses look
  inconsistent where a common tangent would be possible; 3-point perspective gives
  the geometrically consistent solution (provable in CAD) but costs drawing effort.
  Choose by purpose/detail/time. Keep viewing the WHOLE sketch in sensitive areas:
  the visual overall impression outranks exact correctness.
- Chamfers (Fasen) are oriented off cuboid lines/faces; pyramids/frustums as
  support elements; pitched roofs (Dachschrägen) off a base cuboid with auxiliary
  lines oriented to it; dormers (Dachgauben) added onto the slope grid.
- Tire-on-rim type problems: define the contour in one isometric plane, place
  rotation ellipses at corresponding points.
- Exploded views (Explosionszeichnung) of assemblies work well in 2-point.

## 6. Text, annotation and dimensioning practice (in sketches)

### 6.1 Annotation toolbox (free choice)

- Marker (colored pencil or fineliner) for what must stand out; leader lines
  (Bezugslinien): straight, wavy, with arrow, or with a dot.
- Lettering: all caps (Blockschrift) or upper+lower case; straight baselines via
  ruler, text aligned to follow the perspective, or digital text on copies;
  signature + date can carry meaning; keywords rescue an imprecise sketch.
- **Back up / scan BEFORE adding annotations** - "annotations have spoiled many a
  fine sketch". Text as hero (presentation only): letter shadows or letters as
  full solids with shading - test the effect, it can also harm.
- Dense schemata: digital text beats handwriting. Floor-sitting safety-zone text
  follows the perspective. Symbols are compact semantic carriers (e.g. lock
  open/closed beside a drawer shows interlock logic) - but do not invent full
  electrical/sanitary symbol sets; their standards are outside this skill's scope.

### 6.2 Dimensioning practice in sketches

- Normal/2D views are the easy, unambiguous dimension carrier; agree dimensions
  ("abgestimmt") with customer/production BEFORE CAD. 3D alone rarely suffices -
  combine dimensioned 2D with perspective sketches.
- IF dimensions go into a perspective, **isometric is preferred** (uniform
  foreshortening); dimensions may be split between iso and normal/section views.
- A sketch may reach production detail including tolerances (Toleranzen; marking
  per DIN ISO 6284). Dimensioned exploded views with handwritten part names
  communicate assembly intent. 3D data-flow diagrams work best isometric.
- Abbreviations used around machine-safety sketches: ERP = business-process
  planning/steering; PLM = product life-cycle management; CAD = computer-aided
  creation/modification/optimization of drawings and models; Risikobeurteilung =
  structured hazard identification + risk evaluation + risk reduction underpinning
  machine safety within CE certification. VERIFY the current directive text before
  quoting numbers.

## 7. CAD drafting conventions (Bauinformatik layer)

### 7.1 What a CAD drawing is made of

- All 2D drawings compose 0/1/2-D primitives: points (marks, traverse corners),
  lines (edges, polylines, curves), areas (rectangles, polygons, circles), text
  blocks. Attributes: points -> symbol+colour; lines -> **Strichstärke (width),
  Strichfarbe (colour), Linientyp (type)**; areas -> Schraffur, colour, fill; text
  -> Schrifthöhe (height), character set, colour, direction.
- Interaction: pick via snap radius (Fangradius) or window; geometry ops
  (intersection, perpendicular, tangent-to-circle); manipulation (move, rotate,
  mirror, scale, copy, boolean); aids (grid, ruler, measure distance/angle/area).
- Sheet organisation + **layer technique (Folientechnik)**; productivity via reuse
  (variant technique, block/complex-part reuse) - requires pre-planned model
  decomposition recognising identical/similar elements.
- Construction symbols are **scale- and plan-type dependent** (Maßstab + Plantyp):
  the same door depicted differently at 1:500 vs 1:20. Dimensioning: chained /
  stacked / free; **associative dimensioning + hatching update with the model**.
- In conventional practice the 2D plan remains the legally binding execution basis
  ("rechtsverbindliche Grundlage für die Ausführung"). (CAD term coined 1957;
  2D-only production today is honestly called Computer-Aided Drafting.)

### 7.2 Line widths and the line-type -> meaning matrix

Width series (drawing-standards ruleset, ISO 128 scope):
**0.13 / 0.18 / 0.25 / 0.35 / 0.5 / 0.7 / 1 / 1.4 / 2 mm**; three groups narrow :
wide : extra-wide in ratio **1 : 2 : 4**. Application matrix (condensed; line
group number, type, weight class -> meaning). Rule of thumb: **what is cut gets
the thickest line; what is seen thin; what is hidden dashed; what orients (axes,
section planes) dash-dot; what refers (dimension, leader, auxiliary) thinnest.**
A zigzag break line may cut any view to save sheet space.

| Line | Weight | Meaning (construction drawings) |
|---|---|---|
| Continuous thin | 0.13-0.5 | material boundaries, hatching, opening diagonals, stair tread arrows, short centre lines, dimension & auxiliary lines, leader lines, existing contours (landscape), visible contours, simplified doors/windows/stairs, detail outlines |
| Continuous thick | 0.25-1 | contours of HATCHED section cuts |
| Continuous very thick | 0.5-2 | contours of UN-hatched section cuts, reinforcement bars, special emphasis |
| Dashed thin | 0.13-0.5 | existing level lines, planting subdivision, invisible contours |
| Dashed thick | 0.25-1 | hidden contours |
| Dashed very thick | 0.5-2 | lower-layer reinforcement in plan / rear layer in elevation |
| Dash-dot thin | 0.13-0.5 | section planes, centre/symmetry lines, detail frames, reference lines |
| Dash-dot wide | 0.25-1 | section-plane ends, contours visible before the section |
| Dash-dot very wide | 0.5-2 | secondary orientation, contract/boundary lines |
| Dash-dot-dot thin | 0.13-0.5 | alternative positions, centre-of-gravity lines (Schwerlinien), adjacent-part contours |
| Dash-dot-dot wide | 0.25-1 | hidden contours before section |
| Dash-dot-dot very wide | 0.5-2 | prestressing bars/cables |
| Dotted thin | - | contours of NOT-projected (future/other-phase) parts |
| Graphic symbols | 0.18-0.7 | symbol linework |
| Zigzag thin | - | break lines |

### 7.3 Section conventions and hatch families

- Section cut contours: thick if hatched, very thick if left unhatched (matrix above);
  section-plane position shown as dash-dot with wide end strokes (04.1/04.2);
  arrows/letters name the section (A-A, B-B).
- Material hatch families are defined graphically in the standards plates (names machine-
  readable, patterns graphical - VERIFY pattern geometry against the standard
  plates): soil (Boden), gravel (Kies), sand (Sand), concrete unreinforced/reinforced
  (Beton unbewehrt/bewehrt), masonry (Mauerwerk), concrete of increased strength,
  timber across grain / along grain (Holz quer/parallel), insulation (Dämmstoff),
  sealant (Dichtstoff), metals (Metalle), plus lightweight concrete (Leichtbeton),
  watertight concrete (WU-Beton), lightweight brick (Leichtziegel), pumice (Bims),
  glass (Glas), wood-based board (Holzwerkstoff), plasterboard (Gipsplatte), filler
  (Füllstoff), water (Wasser), gases (Gase). Timber detail per DIN 919: solid timber
  (Vollholz), end grain (Hirnholz), longitudinal grain (Längsholz).
- Hatch discipline: keep hatch lines PARALLEL within one material field (a ruler
  helps - also true in freehand); different materials = different patterns, never
  rely on colour alone (drawings get photocopied).
- Section-vs-view in sketches: normal views with cut sections (Schnittdarstellungen);
  section face shown in isometric; partial cuts; broken-away areas along free break
  lines; components at differing transparency.

### 7.4 Dimensioning discipline (Bemaßung) on drawings

- Governing ruleset named: DIN 406-11/-1 and DIN EN ISO 3098 (lettering)
  within the drawing-standards ruleset. Do not quote clause numbers from
  memory - VERIFY.
- **Units by trade (DIN 1356-1)**: reinforced-concrete drawings in
  metres, timber in centimetres, steel in millimetres. Notation examples: metres
  only (<1 m written like "5; 24; 88,5 | 313,5" - decimal comma or point per sheet
  convention); m+cm form "5 | 24 | 313"; mm form "50; 240 | 885 | 3135". Keep ONE
  unit convention per drawing set.
- **Level marks (Höhen)**: solid triangle = structural/raw shell level (Rohbau);
  open triangle = finished dimension (Fertigmaß). **+0.00 = finished floor of the
  ground storey**; storey heights measured FF-to-FF (finished-floor to finished-
  floor); parapet heights from structural slab to opening soffit.
- Dimension chain logic: several Bemaßungsarten - chained (Kettenmaß), stacked
  (Treppenmaß), free - choose per readability; dimension the THREE coordinates of
  every element across plan + section + elevation without duplication conflicts;
  VERIFY full arrow-size/spacing/text-height mechanics against DIN EN ISO 30600-
  series/406 (not stated here).
- Stair depiction (DIN 18065 terms + DIN 1356-1): walking line with circle at the
  bottom step and 45-degree arrow at the top; "Nische" (opening) = single diagonal
  bottom-left to top-right; "Durchbruch" (full penetration) = double diagonals;
  ceiling-opening shadow hint. Door/window simplified depiction is plan-type
  dependent (VERIFY swings per DIN 1356-10 plates - patterns are graphics).
- Element coding in DACH practice: IDs like C201 S201 W201 B201 - first digit =
  storey, letter = element class; VERIFY the letter canon against the project's own
  legend - never assume across offices.
- Reinforcement marks (ISO 3766): position mark e.g. circled number +
  "19Ø20-200-T-13" = count, bar Ø mm, spacing mm, position letter (B/T/1/2/N/F),
  form code; mesh code per DIN 488-4 (e.g. R257A), orientation diagonal bottom-left
  to top-right, main bars outside (bottom = positive, top = negative moment);
  bending-form codes: 2-digit (1st = number/type of bends 0-7/9, 2nd =
  direction/normalisation; end hooks 0/1/2/3 = none/90°/90-180°/180°; 99 = non-
  standard); dimensions >0, inner diameters/radii inside, others outside; example
  bar weights Ø10 = 0.617, Ø16 = 1.58, Ø25 = 3.85 kg/m (confirmed verbatim against
  Wendehorst Tab. 25.x, VERIFY tag dropped for these three).
  Legacy layer-position codes (DIN 1356-10:1992, older/existing drawings still use
  these letters) map to the current ISO 3766 set: u=unten(bottom)/o=oben(top)/
  1.Lage/2.Lage/V=vorn(front)/H=hinten(back) ↔ B/T/1/2/N/F.
- Demolition/rebuilding symbols per DIN ISO 7518 (VERIFY plate geometry); tolerance
  markings per DIN ISO 6284 (also usable on detail sketches).

### 7.5 Scales and plot sizes

- Recommended scale series (ISO 5455): enlarged 50:1 20:1 10:1 5:1
  2:1; natural 1:1; reduced 1:2 1:5 1:10 1:20 1:50 1:100 1:200 1:500 1:1000 1:2000
  1:5000 1:10000; the 1:2.5 / 1:25 / 1:250 intermediate series allowed.
- Practice pairing (see 8): site 1:500-1:2000; concept/authorisation 1:100-1:200;
  execution 1:50-1:20; details 1:20-1:1 (even 5:1, 10:1 for junctions). Always
  check printed output against a known length (druckmaßstab): a 100 mm plot line
  must read 100 mm at 1:1.
- Sheet formats DIN A0-A4 (DIN EN ISO 5457 + folding per DIN 824), confirmed
  against Wendehorst Tab. 25.1/25.2: sheet sizes A0 841x1189, A1 594x841,
  A2 420x594, A3 297x420, A4 210x297 mm; drawing area (Zeichenfläche) within
  the sheet: A0 821x1159, A1 574x811, A2 400x564, A3 277x390, A4 180x277 mm —
  the difference is the border/fold margin.
- Title block (Schriftfeld / Titelblock) content per DIN EN ISO 5457 (source
  does not cite DIN 6771-1 by number — keep that citation VERIFY, but the
  field set itself is confirmed, Tab. 25.3): client/Bauherr name; project or
  component designation; date; name of person responsible for the drawing
  with check/approval marks; type and content of the drawing; scale(s);
  revision note with date.
- Text height / line width by drawing scale (DIN EN ISO 3098 series,
  confirmed against Wendehorst Tab. 25.12, VERIFY tag dropped): scale 1:50
  and larger (e.g. 1:20) -> text height 5.0 mm, line width 0.35 mm; scale
  1:100 and smaller (e.g. 1:200) -> text height 3.5 mm, line width 0.25 mm.

### 7.6 BIM context pointers (what the drawing hands over)

- BIM = continuous use + lossless handover of a digital building model across the
  life cycle; tools = 3D modelling + construction-object catalogue -> consistent
  DERIVED 2D plans (Grundrisse, Schnitte) + DIN-compliant sheets. Pure geometry is
  insufficient - analysis needs SEMANTICS (evacuation sim: door/stair identities;
  static calc: load-bearing flag + material data). Parametric constraints:
  alignment, orthogonality, parallelism, connection, fixed distance, EQ.
- Maturity (UK Task Group after Bew & Richards 2008): Level 2 =
  Common Data Environment holding identity-preserving discipline (federation)
  models + linked coordination model; + linked info -> nD (4D schedule, 5D cost);
  higher levels = integrated total model, open standards, IoT. Little BIM =
  partial model-based work with file exchange; BIG BIM = all participants, all
  phases; Open BIM = vendor-neutral IFC vs Closed = single-vendor.
- IFC (buildingSMART): lossless geometry+semantics exchange, ISO 16739 (cited at
  2013 and DIN EN ISO 16739:2017-04 - VERIFY current edition); layers Resource ->
  Core -> Interoperability -> Domain; geometry via triangulation / BRep / CSG /
  sweep-extrude; IfcLocalPlacement + IfcMapConversion + CRS entities tie local
  model coords to state CRS (EPSG codes, e.g. ETRS89/UTM).
- CDE status cycle Work in Progress -> Shared -> Published -> Archived with
  mandatory checks at each transition; scope/timing in the BIM execution plan
  (BAP); client requirements = AIA; clash coordination issues tracked in BCF;
  organisation per ISO 19650 (dated citation - VERIFY). LOD ladder: 100 concept
  (symbol geometry) -> 200/300 generic-to-exact position+quantity -> 400
  manufacturing -> 500 as-built/operational. After completion the model must
  mirror built reality (significant as-built deviation -> model update).
- Site-data note: planning starts from digital cadastral map (ETRS89/UTM) + DTM +
  aerial images; plan distances from cadastral files are NOT field distances
  (projection + height reduction - Projektmaßstab, cm-per-100 m magnitudes across
  a Bundesland); agree project coordinate system + plan level in writing; local
  BIM models sit in a local cartesian system, origin near object, scale 1 -
  georeference on export.

## 8. Plan-set types and purposes (Plantypen, HOAI design drawing tiers)

Standard scales per German practice tiers:

| Tier | German | Purpose | Typical scale |
|---|---|---|---|
| Preliminary concept | Vorentwurf | idea, massing, feasibility | 1:500 / 1:200 |
| Design | Entwurf | developed design, client + authorities dialogue | 1:100 (/1:200) |
| Building-application drawings | Bauvorlagen | permit submission (Genehmigung) | 1:100 |
| Execution/shop | Ausführungs-/Werkplanung | buildable information | 1:50 / 1:20 |
| Details | Details | junctions, layers, fittings | 1:20 / 1:10 / 1:5 / 1:1 |
| Measurement/as-built billing | Abrechnungs-/Ausmaßpläne | quantities for invoicing | follows execution |
| Inventory | Baubestandsplan | built reality documentation | 1:50–1:100 |

Statik track (structural drawing tiers): Position plans; formwork/foun-
dation plans (Schal-/Fundamentpläne, 1:50 - construction joints, layers, cut-outs,
bearings, embeds, surface finishes, material classes); structural-shell drawings
(Rohbauzeichnungen); reinforcement drawings (Bewehrungszeichnungen, regular scales
1:50/1:20, 1:25 too; mats 1:50, bars 1:25, large areas 1:100, details 1:5/1:1);
precast-element drawings (Fertigteilzeichnungen 1:20/1:25 - + strength at transport,
self-weight, tolerances, lifting/support points, quantities); laying/installation
drawings (Verlegezeichnungen 1:50 - positions, assembly sequence, tolerances,
bearings, connections, falsework, site reinforcement, materials). Difficulty tiers:
simple = object + reinforcement drawings; medium = + formwork plans; high =
Rohbauzeichnungen by the structural engineer.

Steel shop tier (DIN ISO 5261 + EN 1090/EN ISO 2553/ISO 5845-1): design
drawings 1:10 (or 1:15), details 1:5/1:2.5/1:1; overview 1:50/1:100; shop drawings
up to profile 500 mm: 1:10 + line group 0.5, larger 1:15 + 0.35; A0 preferred; mm
everywhere; distinguish single pieces / assemblies / shipping parts (Versandteile)
vs add-on parts (Anbauteile); weld symbols (basic I/V/DV/HV/... + supplementary
flush/convex/concave/root-reinforcement/all-around/site) and bolt symbols (plain vs
countersunk/counterbore, shop- vs site-drilled) - glyph geometry: VERIFY plates.

Existing-building survey types (Bauaufnahme per DIN 1356-6): Baubestandsplan
(as-built), Aufmaßskizze (measure sketch), Baualterplan (construction-age),
Sanierungsplan, Abrissplan (demolition), Rekonstruktions-, Demontage-/
Wiederherstellungsplan, Bauschadenzeichnung (damage plan). Info levels: I =
1:500/1:100/1:100/1:100 (site/plan/section/elevation); II min 1:500/1:50/1:50/1:50.
Abbreviation keys (RB BM ABR AL BS RM EM UM OM TM HM SM WV ZERST DOKU) + a 34-key
damage catalogue exist - use the project legend; VERIFY edition. Deformation-true
measured survey (verformungsgerechtes Aufmaß) by total station or laser scan into
CAD/BIM is the existing-building baseline. (Naming: Grundriss = floor plan, Schnitt
= section, Ansicht = elevation, Lageplan = site plan - see term bank, section 13.)

## 9. Reading and producing sections and details

Think in sections: a component is a STACK of functional layers, and every detail is
the same stack resolved at an edge.

- Canonical layer sequence (wall/roof envelope): load-bearing structure + insulation
  + vapour control (barrier/retarder) + airtightness layer + weather skin (1st/2nd
  moisture protection stage). Each as a CONTINUOUS functional surface; stagger the
  seams of successive layers.
- Stiftregel (pen rule, DIN 4108-7 scope): the airtight layer must be drawable
  without lifting the pen - when checking your own section, trace the airtight
  line through every junction; where the pen lifts, there is a detail to draw.
- Reading order for a foreign section: identify cut vs seen lines by weight (7.2),
  hatch families (7.3), layer thicknesses (the dimension carriers of build-ups),
  fasteners/anchors (each = potential thermal/acoustic bridge), and continuity of
  each functional line around corners.
- Producing one: cut plane straight through, hatch every material, outline the cut
  very thick/thick per convention, seen-behind lines thin (dashed only for hidden),
  dimension each layer, call out materials by hatch + label, zoom the critical node
  to 1:5/1:2/1:1 beside it (detail frame dash-dot thin, lettered).
- Envelope conflicts to show explicitly in details: anchors through insulation
  (thermal bridge), stiff insulation vs acoustic leaf performance, cavity flow
  obstruction, base drainage (drip flashing, plinth profile, sealing tapes), rear-
  ventilation routes; in isometric use the Einschneideverfahren (5.7) when the
  section plane itself must appear in 3D. Section face in isometric, partial cuts,
  broken-away areas and varying transparency are legitimate SKETCH devices;
  normative drawings stick to straight section cuts.

## 10. Sketch -> model -> screenshot loop (FreeCAD via neka-nat/freecad-mcp)

The loop closes the gap between loose intent and checked geometry. Tools below are
the MCP server's (`create_box`/`create_cylinder`/sketch+Part ops, `get_view`,
`send_log`); if names differ in your deployment, check its tool list first.

1. **Paper first.** Rough the idea as a cuboid Bezugsraum sketch (iso or 2-point,
   section 4); decide message + view set before touching CAD.
2. **Block out.** Primitives + booleans ("anbauen/wegschnitzen") mirror the sketch
   decomposition; keep it coarse - intermediate geometry is cheap.
3. **Cheap camera pull.** `get_view` with `view_name` = `Isometric` / `Front` /
   `Top` / `Right` and **`include_screenshot: false` for intermediate iterations**
   - don't burn context on images while the geometry is still wrong.
4. **Checkpoint screenshot.** When the block-out matches intent, ONE `get_view`
   with `include_screenshot: true` per view: Isometric for massing; Front/Top/Right
   = the Normalriss trio for proportions (Top doubles as plan underlay for
   division checks).
5. **Compare against the sketch.** The model's Isometric view is true isometric
   (uniform foreshortening) - a 2-point sketch's distortion is a CHOICE; check
   proportions in the orthographic views only.
6. **Dimension normal views**, not the perspective (6.2); annotate screenshots
   only AFTER copying the clean view (annotations spoil pictures - same rule).
7. **Iterate:** mark up the printed screenshot -> model edit -> new screenshot at
   the next real checkpoint.
8. **Hand off:** BIM context -> IFC export (Open BIM); drawing context -> derived
   plan/section/elevation sheets (7.5/8); presentation -> one dimensioned iso +
   one perspective + the normal trio.

Rule of thumb: treat every screenshot as a deliverable - clean view, scale note,
no construction clutter. FreeCAD's iso view shares the uniform-foreshortening
logic of iso paper templates, so iso dimension callouts read consistently in both.

## 11. Drawing QA checklist (before anything leaves the workspace)

Sketch QA:
- [ ] Message clear from across the room? Title/keywords rescue ambiguity?
- [ ] Right representation form for the audience (3.7 table)?
- [ ] Horizon consistent; ONE per perspective; eye height deliberate?
- [ ] Verticals truly vertical; VPs per 2.5x/1.5x rules if checkable?
- [ ] Ellipses: major axis perpendicular to revolution axis; roundness vs horizon?
- [ ] Shadow: light direction single & stated (clock position); contours survive
      where shadows meet?
- [ ] Divisions: even spacings even, hatches parallel, pattern repeats true?
- [ ] Scale figure present (or deliberately omitted)?
- [ ] Clean copy saved before annotations/shadow?

Drawing QA:
- [ ] Line-weight logic: cut > seen > hidden > reference; nothing "all thick"?
- [ ] Hatch = material identity, parallel lines, no colour-only coding?
- [ ] Units consistent per trade (m/cm/mm); one decimal style per sheet?
- [ ] Levels: +0.00 = finished ground floor; solid Rohbau vs open Fertigmaß
      triangles; FF-to-FF storey heights?
- [ ] Every point three-dimensionable across plan/section/elevation without conflict?
- [ ] Scale stated AND plot-scale verified (known-length print check)?
- [ ] Sheet: format, margins, title block complete (project, number, sheet n/N,
      scale, date, revision status, signatures), fold-safe margins for delivery?
- [ ] Section arrows/labels match the sections actually present?
- [ ] Detail frames referenced from parent views (and back)?
- [ ] Symbol legend included where scale-dependent symbols are used?
- [ ] Revision status explicit; superseded sheets marked (DIN ISO 7518 logic)?
- [ ] Derived from model? Then consistency model<->sheet checked (BIM) and CDE
      status transition (WIP->Shared->Published) respected.

Reinforcement drawing (Bewehrungsplan) minimum content — a drawing-deliverable
checklist, cross-reference `concrete-detailing` for the design values behind
each item: main dimensions of each RC/PT member; concrete strength + exposure
class; rebar/prestressing steel grade; position numbers, count, diameter,
shape, location of bars; bar spacing, vibration gaps (Rüttelgassen), location
of concreting openings; lap/anchorage lengths at supports; weld locations +
filler material; cover c_v; position-securing measures (spacer type/
arrangement, top-bar support details); minimum bending-roller diameter; joint
detailing; embedded parts not tied to rebar; for prestressed elements:
prestressing method, tendon count/type/location, anchorage/coupling locations.

## 12. Common mistakes

1. Dimensioning a perspective that isn't isometric - read-off lengths are wrong;
   dimension normal views or iso only.
2. Two horizons in one scene / figures at the wrong eye-height for the horizon.
3. VPs too close "to save space" -> accidental wide-angle distortion a client
   reads as design error.
4. Erasing instead of retracing - loses speed, keeps the line anxious.
5. Final linework in pencil -> gray fading scans; construction lines in pen ->
   clutter that can't be traced away.
6. All lines one weight: section cuts, hidden lines, dimensions scream equally.
7. Colour-only coding (hatch or status) - photocopies flatten it.
8. Mixed unit conventions on one drawing (concrete metres beside steel mm without
   notes) - the classic wrong-part-ordered source.
9. Solid/open level triangles swapped -> site builds to the wrong completion stage.
10. Empty title block / missing scale: an unscaled print is not a drawing.
11. Over-detailing early: full marker render of an idea that will die at the next
    review - spend surface effort proportional to message relevance.
12. Annotations added to the only copy (no backup scan first).
13. Trusting "looks right" at strong distortion (ellipse/cylinder transitions) -
    check with Einschneideverfahren or CAD before freezing.
14. Skipping the model-derived dimension pass and letting a beautiful perspective
    smuggle wrong proportions into execution.
15. Inventing standards numbers on drawings - cite only what you verified,
    otherwise note "conventions per project legend".

## 13. DE <-> EN term bank

| DE | EN |
|---|---|
| die Skizze / das Skizzieren | sketch / sketching |
| der Normalriss, die Normalansicht | orthographic view |
| die Vorder-/Seiten-/Draufsicht | front / side elevation, top view (plan) |
| der Grundriss | floor plan |
| der Schnitt, die Schnittdarstellung / die Schnittebene | section, cut view / section plane |
| die Verkürzung / der Verkürzungsfaktor | foreshortening / foreshortening factor |
| die Darstellungsebene / Projektionsebene | picture / projection plane |
| das Bezugssystem / der Bezugsraum | frame of reference / reference box |
| die Maßvertikale | true-length vertical reference edge |
| die Parallelperspektive / Axonometrie | parallel projection / axonometry |
| die Kavalier-/Kabinettperspektive / das Schrägbild | cavalier / cabinet projection, oblique pictorial |
| die Isometrie / Dimetrie / Trimetrie | isometric / dimetric / trimetric |
| die Fluchtpunktperspektive / der Fluchtpunkt | vanishing-point perspective / vanishing point |
| der Augenpunkt / das Blickzentrum (Hauptpunkt) | eye point / center of vision (principal point) |
| der Horizont | horizon (eye level) |
| die Übereckperspektive / Frosch-/Vogelperspektive / der Skizzierbereich | corner-view (two-point) / worm's-eye / bird's-eye / sketching crop |
| das Durchpausen / die Vorlage (Unterlage) | tracing-overlay / template (underlay) |
| der Zylinder / der Quader / der Grundkörper | cylinder / cuboid / basic solid |
| die Schwenkellipse / der Hüllquader | swing ellipse / enveloping box |
| die Verschneidung / Durchdringung | intersection / penetration of solids |
| das Einschneideverfahren | section/intercut construction method |
| die Diagonal-/Strahlenmethode | diagonal (bisection) / ray method |
| die Teilung / das Muster | division / pattern (repeat) |
| der Eigenschatten / Schlagschatten | form shadow / cast shadow |
| der Strich / die Strichstärke / die Strichart (Linientyp) / die Schraffur | stroke / line weight / line type / hatching |
| die Bemaßung / die Toleranzen | dimensioning / tolerances |
| die Fase / die Verrundung / die Kante / verdeckte Kanten | chamfer / fillet / edge / hidden edges |
| die Linienwolke | line cloud (circle-search technique) |
| die Explosionszeichnung | exploded view |
| die Dachkehle / Dachgaube / Dachschräge | roof valley / dormer / roof slope |
| das Schriftfeld / das Blattformat A0-A4 / der Maßstab | title block zone / sheet format / scale |
| die Höhe +0,00 / Rohbau / Fertigmaß | level datum +0.00 / structural shell / finished dimension |
| das Kettenmaß / Treppenmaß / freie Bemaßung | chained / stacked / free dimensioning |
| der Plan / der Lageplan / die Bauvorlagen | plan / site plan / building-application drawings |
| die Werk-/Ausführungsplanung / der Bestandsplan / das Aufmaß | shop-execution design / as-built plan / measured survey |
| das verformungsgerechte Aufmaß | deformation-true measured drawing |
| die Bewehrungszeichnung / die Position (Bewehrung) | reinforcement drawing / bar mark |
| der Schalplan / Fundamentplan | formwork / foundation plan |
| die Schweißnaht / der Bolzen | weld seam / bolt (VERIFY symbol geometry) |
| das Bauwerksmodell / das Fachmodell / der Datenaustausch (IFC/BCF) | building model / discipline model / data exchange |

Source-faithfulness note: quantitative values (VP ratios, angles, head=1/8,
1:1.7, line series 0.13-2 mm 1:2:4, ISO 5455 scale series, unit-by-trade rules,
HOAI-tier scales, section-hatch family names, CDE statuses, LOD ladder) are taken
verbatim from the compiled reference material. Anything marked VERIFY - exact sheet-border mm,
title-block field canon, first/third-angle figures, hatching pattern geometry,
clause numbers - must be checked against the current standard edition before use
in normative work products. This skill guides representation decisions; it does
not replace the standards themselves.
