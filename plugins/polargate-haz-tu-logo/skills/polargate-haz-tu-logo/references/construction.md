# Construction: turning an idea into a resolved mark

Table of contents
1. Mark types and SVG suitability
2. Gestalt foundations
3. Grid and geometric systems
4. Optical correction
5. Neo-minimalism: the meaningful detail
6. Reduction tests
7. Balance, symmetry, weight
8. Cliché blocklist
9. Differentiation

---

## 1. Mark types and SVG suitability

Pick from the brief, not habit. Suitability is how well generated SVG handles it.

- Lettermark (initials): high. Great for long names; build letters on a shared geometric system.
- Monogram (interlocked initials): high. Premium and heritage feel.
- Abstract mark (non-literal geometric form carrying a property): high. Best fit for generated SVG and for differentiation.
- Symbol / pictorial (simplified object): medium, only if reducible to clean geometry; never a literal scene.
- Wordmark (the name in distinctive type): medium. Mock layout only; finish as outlined paths in Figma (see typography.md).
- Combination (symbol plus wordmark): high for the symbol, wordmark follows the caveat.
- Emblem / badge (name and mark in a contained shape): medium-high if kept geometric, but emblems die small, so always design a symbol-only fallback for favicons.

Default for a digital-first or premium brand with no strong lean: abstract mark or monogram on a geometric grid, with a wordmark outlined later for the lockup.

## 2. Gestalt foundations

The theory behind why marks read. Use deliberately.

- Figure-ground: the eye separates subject from background. Design the negative space as carefully as the positive; the counter can be the mark.
- Closure: the eye completes implied shapes from gaps. Lets a mark feel confident and minimal.
- Continuity: the eye follows a continuous line or curve. A single uninterrupted path reads as resolved.
- Proximity and similarity: near or alike elements group into one perceived unit. Use to make multiple parts read as one mark.
- Common region and connection: enclosing or linking elements binds them. Useful for monograms.

## 3. Grid and geometric systems

Resolved marks are built on a system, not eyeballed.

- Use an underlying grid: overlapping circles of related radii, a square module grid, or a small set of repeated radii and angles. Reuse the same radii and angles so curves and corners feel related.
- Derive everything from one base unit: stroke width, corner radius, gaps, and counters as multiples of that unit. Consistency reads as intention.
- The golden ratio is a sanity check, not magic. Harmony comes from a consistent system plus optical balance, not from forcing 1.618.
- Favor constructions expressible with circles, arcs, straight segments, and a few beziers; this is also what renders cleanly as SVG.

## 4. Optical correction

Mathematically correct is not visually correct. The eye is the client.

- Overshoot: circles and triangles must extend slightly past the cap line of flat shapes to look the same size.
- Visual centering: pointed shapes (triangles, play buttons) sit left of mathematical center to look centered. Center by mass.
- Junction thinning: where strokes meet or cross, thin them slightly so the joint does not read as a dark blob.
- Counter balance: balance enclosed white space by eye; equal math gaps often look unequal.
- Align visually, not to the pixel.

## 5. Neo-minimalism: the meaningful detail

The current bar is minimalism with a hook, not faceless minimalism and not clutter. Keep the form spare, then add exactly one meaningful detail that carries identity:

- A smart negative-space cut.
- A single corner chamfer or asymmetric terminal.
- A custom counter shape.
- A deliberate, controlled asymmetry.
- A single-color dimensional move (an extruded or folded form in one flat color, no shadows or bevels).

One detail, chosen on purpose. Two competing details is noise. The mark must still pass the favicon test with the detail present.

## 6. Reduction tests

Gates, run on every concept.

- Squint test: blur or shrink to 24px. If the silhouette stays distinct and balanced, it holds.
- Favicon test: at 16px, still legible and unmistakable. Detail that vanishes at 16px is weight the mark does not need.
- One-color test: flatten to one flat color. If it only works in gradient or multicolor, it is fragile.
- Reproduction test: imagine it embroidered, etched, stamped, faxed. Thin hairlines and tiny gaps clog or vanish; thicken and simplify.
- Billboard test: blown up, still intentional and not empty.

## 7. Balance, symmetry, weight

- Symmetry reads stable and trustworthy; intentional asymmetry reads dynamic and modern. Choose to match the attributes.
- Distribute visual weight, not just area; a small dense element balances a large airy one.
- Give the mark a clear anchor or axis so the eye knows where to land.
- Avoid accidental tangents; overlap clearly or separate clearly.

## 8. Cliché blocklist

Do not use these unless the user insists, and push back once. They are global, repeated, and legally risky (near-identical marks invite cease-and-desist).

- Globe, orbit rings, or latitude-longitude lines for global or worldwide.
- Lightbulb for ideas or innovation.
- Gear or cog for engineering or settings.
- Swoosh, generic arc, hook, or speed-line for momentum.
- The "person" figure: arms-up human, or the letter i turned into a person.
- Handshake for partnership.
- Location pin for local or maps (differentiate hard even for a real maps product).
- Generic tree, oak silhouette, leaf, or sprout for eco, green, or growth (a generic tree is an illustration, not a mark).
- Gable or roofline over text for real estate.
- Interlocked letters imitating heritage luxury without the heritage; reads as knock-off.
- Chart, graph, or bar shapes for finance or data.
- Speech bubble for chat; shield for security; infinity loop for anything; the three-overlapping-petals app blob.
- Rainbow gradients, glossy bevels, drop shadows, and 3D extrusions of a flat shape.

## 9. Differentiation

A mark lives next to competitors. Before finalizing, mentally line it up with the category's known marks. If it blends in, it has failed. Identify the category's visual defaults (the colors, shapes, and metaphors everyone uses) and deliberately move away from at least one. A distinct silhouette beats pretty detail every time.
