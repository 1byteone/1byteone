# SVG Data Flow Drawing Standard

## Objective

This standard defines how to draw animated SVG data-flow architecture diagrams in this repository so that:

- data flow is visually obvious instead of implied;
- arrow heads land exactly on component boundaries;
- labels do not collide with lines or boxes;
- all project diagrams share one visual language;
- every SVG can be reviewed with a repeatable checklist.

## Scope

Applies to:

- `ruoyi-ai-architecture.svg`
- `ai-passage-creator-architecture.svg`
- `mewpaw-code-architecture.svg`
- `zznursing-architecture.svg`
- future repository-level architecture/data-flow SVGs

## Mandatory Design Principles

1. Every diagram must have a primary flow direction.
2. Every primary flow must be visible as both:
   - a structural arrow path;
   - a motion cue, such as moving signal particles or animated dash offset.
   - moving signal particles must stay hidden until they are attached to the real path; no stray dot may appear at the SVG origin in frame 0.
3. Every arrow must start from a canonical anchor point on the source node edge.
4. Every arrow must end at a canonical anchor point on the target node edge.
5. Decorative lines are forbidden if they do not correspond to a real business, control, or data dependency.

## Canonical Anchor Rules

Each rectangular node must use only these anchor types:

- `N`: top-center
- `S`: bottom-center
- `W`: left-center
- `E`: right-center

For a box at `x, y, width, height`:

- `N = (x + width / 2, y)`
- `S = (x + width / 2, y + height)`
- `W = (x, y + height / 2)`
- `E = (x + width, y + height / 2)`

Strict rules:

- Horizontal flows must connect `E -> W`.
- Vertical flows must connect `S -> N`.
- Return loops must not terminate inside a box.
- A path endpoint may never stop short of the target edge.
- A marker may never visually overlap the target label area.
- Region boundaries are not valid source anchors when the real source is a component box.

## Multi-Exit / Fan-Out Rules

When one node emits more than one flow:

- all flows must begin from the same canonical source anchor;
- branching must happen outside the source box, not by inventing arbitrary `y` offsets along the same edge;
- the split must use either:
  - a shared orthogonal spine in whitespace; or
  - a junction point outside the node body;
- fan-out spines must not sit on top of a region boundary stroke.

Forbidden shortcuts:

- starting one line at `E.y+8` and another at `E.y+24`;
- placing three separate arrows on the same edge without a visible split strategy;
- using a region frame as a fake bus for unresolved routing.

## Routing Rules

Preferred routing order:

1. straight horizontal line;
2. straight vertical line;
3. one-bend orthogonal path;
4. two-bend orthogonal path only when unavoidable.

Forbidden routing:

- freehand diagonal connector lines between ordinary boxes;
- arrow lines crossing through a node body;
- arrow lines hidden underneath text labels;
- connector segments shorter than 16px unless the path is purely vertical.

Recommended path patterns:

```svg
M x1 y1 L x2 y2
M x1 y1 L midX y1 L midX y2 L x2 y2
M x1 y1 L x1 midY L x2 midY L x2 y2
```

## Presentation-Mode Visible Travel Distance

For README/demo-facing animated diagrams, connectors must not collapse into micro-stubs that technically connect but fail to visually communicate motion.

Rules:

- Any animated secondary/support/data lane should provide at least `96px` of visible travel distance.
- Preferred visible travel distance:
  - `120-180px` for secondary taps into a shared spine or bus;
  - `180px+` for hero lanes the viewer should notice immediately.
- If the direct anchor-to-anchor route is too short, reroute through whitespace using:
  - a shared spine;
  - a one-bend orthogonal jog;
  - or a longer bus entry corridor.
- When three or more nodes tap the same provider/service, position the shared spine far enough away that each tap remains visually legible.
- Do not rely on a `30-80px` animated stub as the only visual proof of a dependency.

Preferred correction strategy:

1. keep true node-edge anchors;
2. preserve semantic correctness;
3. lengthen the visible run in whitespace;
4. only then reduce visual weight if the lane is secondary.

Forbidden presentation shortcuts:

- over-compressing a provider tap until the motion cue is barely perceptible;
- replacing a meaningful flow with a tiny decorative dash segment;
- shortening a line so much that animation reads as flicker instead of travel.

## Connector Clearance And Bend Discipline

Connectors must visually live in whitespace, not appear to slide along box walls or fold directly on top of a node boundary.

Rules:

- Every orthogonal bend must happen at least `12px` away from any box edge; `16px+` is preferred for presentation diagrams.
- A connector may touch a box only at:
  - its source anchor;
  - or its target anchor.
- Horizontal or vertical segments must not run flush against a box stroke for decorative convenience.
- If a route needs to pass near a node, keep at least `10px` of visible clearance between the segment and that node’s outer stroke.
- Labels should sit in whitespace near a segment midpoint, never on top of a bend and never on top of a box border.

Forbidden connector behavior:

- folding immediately on the box edge;
- using a box corner as the bend point;
- visually merging a connector with a region frame or component outline;
- letting a label hide the fact that a segment is pressed against a node.

## Routing Corridors And Hidden-Path Ban

Every busy diagram must reserve explicit routing corridors before paths are drawn.

Rules:

- A connector may not pass through a component body even if the component is painted later with an opaque fill.
- Opaque masks are a layering safeguard, not permission to use geometrically invalid routes.
- Keep connector centerlines at least `16px` away from region boundaries; `20px+` is preferred between adjacent regions.
- A routing corridor should carry one semantic lane or one explicitly named shared bus.
- If two independent lanes must run in parallel, keep at least `24px` centerline separation; `32px+` is preferred for different color families.
- When a source-to-target route would cross an occupied corridor, move the route into a new whitespace lane instead of hiding the crossing behind a box.
- Long control/support flows should use perimeter corridors or dedicated lower/upper bands rather than cutting through the primary business chain.

Allowed:

- multiple sources tapping a clearly drawn, semantically named bus;
- a low-opacity secondary lane in a dedicated perimeter corridor;
- a deliberate line crossing only when rerouting would materially distort the architecture, and only when the crossing remains visually unambiguous.

Forbidden:

- routing through boxes and relying on paint order to hide the line;
- using a region outline as a bus;
- stacking unrelated amber, green, and slate lanes on the same axis;
- adding parallel lines less than `16px` apart and hoping color alone will separate them.

## Micro-Jog And Alignment Discipline

Tiny corrective bends usually indicate that peer nodes were not aligned before routing.

Rules:

- Orthogonal correction segments shorter than `16px` are forbidden in presentation diagrams.
- If two peer boxes differ by less than `16px` in center alignment, align the boxes instead of inserting a tiny `V8`, `H10`, or similar jog.
- Same-stage process boxes should share a common centerline whenever their relationship is logically horizontal.
- Linear chains should share one column center whenever their relationship is logically vertical.
- Recalculate all affected anchors, labels, dependent paths, and footer clearance after moving a node.

Preferred correction order:

1. align peer-node centers;
2. increase the inter-node gap;
3. move the shared corridor;
4. use a compact marker only after geometry has been improved.

## Connector Label Exclusion Zone

Arrow labels must occupy their own readable whitespace, not merely avoid literal character-line intersection.

Rules:

- Keep the rendered label glyph box at least `10px` from a connector stroke; `12px+` is preferred.
- Measure clearance from the full text width, not only from the label’s `x` coordinate.
- Do not place labels on the same baseline as a horizontal connector.
- Do not place labels within `16px` of an orthogonal bend or junction.
- A label must not extend into a component body, region title, marker head, or moving signal particle lane.
- If no natural whitespace exists, either:
  - move the route;
  - shorten the wording without losing meaning;
  - or place the text on an opaque label chip with `6-8px` horizontal padding.

Forbidden:

- labels that technically start outside a box but extend across its border;
- text resting directly above a line with less than one text-height of separation;
- labels used to camouflage a crowded or invalid route.

## Arrowhead-To-Segment Proportion

Arrowheads must feel proportionate to the last visible segment they terminate on.

Rules:

- The final straight run into a marked endpoint should usually be at least `4x` the marker width.
- Minimum recommended terminal run:
  - `48px` for standard markers;
  - `36px` for compact markers on local chain links.
- If that proportional run cannot be achieved, use one of:
  - a longer orthogonal route;
  - a compact marker for that local connector;
  - or a shared bus entry that creates a longer visible approach.
- Primary business lanes should prefer route lengthening over shrinking the marker.
- Compact markers are acceptable for dense local filter chains, approval chains, and minor support connectors.
- A compact marker does not make a `20px` terminal run acceptable; improve geometry first.
- The visible terminal run is measured from the last bend or junction to the target anchor, not from the full path length.

## Flow Animation Rules

Every main path must include both:

- animated dashed stroke progression;
- moving signal particles on the same path.
- moving signal particles should default to `opacity: 0` (or equivalent) before motion begins, so the first rendered frame never leaks a stray dot at `(0,0)`.

Recommended pattern:

```svg
<use href="#flow-id" class="flow-main">
  <animate attributeName="stroke-dashoffset" values="0;-36" dur="1.8s" repeatCount="indefinite"/>
</use>

<g class="signal" fill="#58a6ff">
  <circle r="4">
    <animateMotion dur="2.3s" repeatCount="indefinite">
      <mpath href="#flow-id"/>
    </animateMotion>
    <animate attributeName="opacity" values="0;1;1;0" dur="2.3s" repeatCount="indefinite"/>
  </circle>
</g>
```

Rules:

- Motion particles must follow the exact structural path, not a nearby duplicate path.
- Signal direction must match the semantic data direction.
- Animation duration must be consistent within one diagram family.
- `prefers-reduced-motion` must disable moving particles and keep the static flow readable.
- Every primary animated path must contain at least one uninterrupted, unobscured run of `96px+`.
- Connector length hidden beneath component masks does not count as visible animation travel.
- Avoid animating several overlapping paths on the same corridor; animate the shared bus once and animate its source/target taps separately.
- Validate animation using at least two browser captures, such as `t0` and `t3s`, and confirm that the visible signal position changes.

## Layering Rules

SVG paint order must be:

1. background
2. grid
3. region boundaries
4. path definitions rendered by `<use>`
5. animated flow overlays
6. opaque mask rectangles
7. node fills and strokes
8. node text
9. legend
10. title and subtitle

Never place animated particles above the title or legend.

## Box Sizing Rules

Default box sizes:

- standard service box: `180-220w x 72-88h`
- compact utility box: `110-150w x 54-64h`
- decision diamond: `72-88` diagonal half-width

Spacing:

- minimum horizontal node gap: `40px`
- minimum vertical node gap: `36px`
- minimum region padding around contained nodes: `24px`
- minimum label gap from line: `10px`

## viewBox / Footer / Legend Rules

- The lowest business node must end at least `40px` above the legend container.
- The legend container must sit fully below every node, connector, and motion particle.
- The final `viewBox` height/width must include:
  - content bounds;
  - legend/footer height;
  - at least `20px` outer bottom padding;
  - at least `30px` outer right padding when arrowheads terminate near the edge.

Forbidden:

- footer bars overlapping the last row of nodes;
- text baselines landing below the `viewBox`;
- “looks fine in code” layouts that clip in browser render.

## Text Rules

- One box must have at most:
  - one tag line;
  - one primary name line;
  - one secondary meta line.
- If the name is too long, split it across name/meta, not across three lines.
- Arrow labels must describe flow semantics, not restate node names.

Forbidden text behavior:

- text overlapping node borders;
- text overlapping animated particles;
- arrow labels centered directly on a bend corner;
- long subtitles inside narrow boxes.

## Color Semantics

Use one consistent meaning per color family:

- cyan: user/request entry
- green: business processing / asset generation
- violet: orchestration / control / workflow logic
- amber: external provider or gateway dependency
- slate: support, cache, retrieval, secondary runtime
- rose: security checks or risk filters

Never recolor the same semantic path differently in the same diagram.

## Review Checklist

Before accepting a diagram, review all of the following:

### Structure

- [ ] XML parses successfully
- [ ] no `script`
- [ ] no event handler attributes
- [ ] no external runtime dependency except allowed fonts

### Alignment

- [ ] every connector starts exactly on a node edge anchor
- [ ] every connector ends exactly on a node edge anchor
- [ ] no arrow head floats in empty space
- [ ] no arrow head overlaps a box fill
- [ ] no connector crosses node text
- [ ] no connector visually rides along a box stroke except at an anchor
- [ ] no bend is placed directly on a box edge or corner
- [ ] no connector passes through a box body and relies on opaque paint order to hide it
- [ ] no independent connector centerline sits within `16px` of a region boundary
- [ ] no unrelated lanes share the same routing corridor
- [ ] no corrective orthogonal jog is shorter than `16px`
- [ ] horizontally related peer nodes are center-aligned before a straight connector is used

### Flow Readability

- [ ] every primary business flow has visible motion
- [ ] branch direction matches real business semantics
- [ ] dotted lines are reserved for support/secondary relationships
- [ ] animated particles move in the same direction as the marker
- [ ] no presentation-mode animated lane is reduced to an imperceptibly short visible run
- [ ] arrowheads feel proportionate to their final visible segment length
- [ ] every primary animated lane has an unobscured `96px+` visible run
- [ ] overlapping paths are represented as an explicit bus instead of duplicate animated strokes

### Layout

- [ ] no label clipping
- [ ] every arrow label glyph box clears connector strokes by at least `10px`
- [ ] no label overlaps a component even when its anchor point is outside the box
- [ ] no label sits within `16px` of a bend or junction
- [ ] no region title collides with a node
- [ ] no legend overlaps the diagram body
- [ ] viewBox includes full content plus margin

### Render Validation

- [ ] screenshot at early time renders correctly
- [ ] screenshot at later time differs in pixels for animated diagrams
- [ ] reduced-motion fallback remains legible
- [ ] no connector originates from empty space or a region border when a component source exists
- [ ] multi-exit nodes use a visible split spine/junction instead of arbitrary offset ports
- [ ] footer/legend remains outside the data-flow body at all tested viewport sizes

## Common Failure Modes To Avoid

1. Fake data-flow diagram:
   static lines only, no moving signal, no animated dash.

2. Near-miss arrow:
   line ends 4-12px before the target box, making the marker float.

3. Overrun arrow:
   line endpoint enters the box body, so the marker sits on top of text.

4. Center-to-center routing:
   connectors drawn from node center instead of edge anchor.

5. Label-on-bend:
   arrow label placed exactly where the path changes direction.

6. Semantics mismatch:
   signal particle moves right-to-left while the marker points left-to-right.

7. Decorative overdraw:
   too many lines shown without business meaning, making review impossible.

8. Broken hierarchy:
   support dependencies drawn with the same visual weight as primary runtime flow.

9. Offset-port cheat:
   multiple arrows leave the same box from invented, uneven edge coordinates instead of a real shared anchor and split.

10. Region-origin bug:
    a connector begins on a group frame because the source component was not actually wired.

11. Footer collision:
    the legend bar visually cuts into the last row of services or hides moving particles.

12. Micro-stub flow:
    a real dependency is technically connected, but the animated visible segment is so short that users cannot perceive directional travel.

13. Edge-fold bug:
    a connector bends right on a box edge, making the route look collapsed into the node outline.

14. Big-head tiny-tail bug:
    the arrowhead dominates the final segment, so the line looks stubby or toy-like instead of directional.

15. Masked-through-node bug:
    a connector is geometrically routed through a component and only appears valid because the box fill hides it.

16. Boundary-riding lane:
    a connector shares or nearly shares the same axis as a region outline, making the frame look like part of the flow.

17. Micro-jog alignment bug:
    peer nodes are misaligned by a few pixels, producing a distracting `V8` or `H10` corrective fold.

18. Corridor multiplexing bug:
    unrelated semantic paths are stacked into one narrow corridor without an explicit bus abstraction.

19. Label-glyph collision:
    the label’s anchor is outside the path, but the rendered text width still crosses the line, marker, or component.

20. Masked animation illusion:
    an animated path is long in code, but most of its travel is hidden under boxes, so the viewer only sees flicker-sized fragments.

## Repository Convention

- Architecture SVG source lives under `diagrams/`.
- README should embed the SVG source directly when GitHub rendering remains stable.
- Temporary render previews must not be treated as source artifacts.

## Acceptance Standard

A diagram is only considered complete when:

1. the flow is obvious without reading surrounding prose;
2. the arrow anchoring is mechanically consistent;
3. the animation supports the diagram instead of distracting from it;
4. a reviewer can map each major path back to a real project behavior from repo documentation or source-backed notes.
