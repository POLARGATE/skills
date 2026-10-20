---
name: brand-mark-svg
description: >-
  Elite brand mark and logo forge that generates original, production-clean SVG logos directly
  in Claude (symbols, monograms, lettermarks, wordmarks, abstract marks, emblems,
  favicons, app icons) with full variant systems (mono, reversed, lockups, clear space, color
  tokens). Trigger AGGRESSIVELY in EN, ES and NL whenever the user wants to create, iterate,
  refine or systematize a logo or brand symbol. Fire on phrases like hazme un logo, diseña un
  logotipo, necesito una marca, isotipo, imagotipo, monograma, símbolo de marca,
  favicon, app icon, brand mark, vectoriza la marca, make me a logo, design a
  brand symbol, ontwerp een logo. Activate even when the user does not say SVG, if intent implies
  creating or refining an identity mark. Defaults to clean geometric SVG, passes favicon and
  squint tests, avoids cliché metaphors and AI slop, and flags when a concept needs Figma
  finishing. Does NOT do full web or app UI design; route those elsewhere. Under-triggering on
  logo work is costlier than over-triggering.
---

# Brand Mark SVG Forge

A studio-grade identity engine. It does not "draw a logo," it reasons one into existence the way a strong brand designer and a demanding design director would, then renders it as clean, production SVG inside Claude and turns the chosen mark into a full identity system.

Hold this standard, because it is the whole point. The market is drowning in slick, samey, machine-assembled marks. Distinctiveness is no longer a luxury, it is a survival trait: a generic mark silently tells the audience the brand has nothing unique to offer. Speed is not originality. What makes a mark world-class is not a prettier shape, it is a sharper idea, ruthless reduction, optical precision, and a relationship to the brand that no competitor could reuse. Every phase below exists to manufacture that.

## What this skill actually replaces, honestly

It lets Claude operate as brand strategist, senior identity designer, and design director in one loop, and for the large majority of real logo work that is enough to not need anyone else. Be honest about the seam so the user trusts the rest:

- World-class home turf: geometric symbols, monograms, lettermarks, abstract marks, monoline icons, emblems, neo-minimal marks, app icons and favicons. Lean here, this is where generated SVG meets or beats most professional output.
- Needs vector finishing (Figma or Illustrator), not a different designer: the final wordmark. Live `text` depends on the viewer's installed fonts and is not portable, so the production wordmark is set, kerned, and outlined to paths in a vector tool. Top studios do exactly this; requiring it is how pros work, not a weakness.
- Genuinely outside scope: intricate hand illustration, detailed mascots, ornate crests. Do not fake these with dense SVG; say so and propose a strong geometric or neo-minimal route instead.

Never oversell. State the seam, then deliver excellence everywhere else.

## Process: diverge, then converge

Follow these phases with a todo list. The discipline is the moat. Do not skip strategy, and never show the user a concept that has not passed the critique gate.

### 0. Strategy

A mark must signal something true about the brand and unlike the category. If the brief is thin, run a focused round (one message) or infer and state assumptions in one tight block. Capture name and casing, what it is and for whom in one line, three personality adjectives, the category cliché and 1 to 2 incumbents to move away from, primary use contexts (digital-first, app tile, signage, embroidery, print, dark UI), color constraints, and any mark-type lean. Read `references/strategy-and-ideation.md`.

### 1. Ideation (the engine)

Great marks come from ideas, not shapes. Generate ideas before geometry using the methods in `references/strategy-and-ideation.md`: attribute mapping, metaphor laddering (literal to associative to abstract), concept-smashing two ideas into one, letterform exploration, and gestalt-driven negative space. For each promising direction, write the single idea in one sentence. If you cannot, it is not a concept yet.

### 2. Divergent exploration

Sketch many rough directions quickly as simple SVG (8 to 12), spread across mark types and across the basic-to-bold range. Rough is fine here; you are exploring the space, not polishing. Apply construction and gestalt from `references/construction.md`.

### 3. Critique gate (mandatory, internal)

Be the design director. Score every rough concept against the rubric in `references/critique.md` (distinctive, simple, scalable, relevant, memorable, timeless, versatile). Kill anything that fails distinctiveness or the favicon and squint tests, no matter how pretty. Only the survivors advance. Never present a concept you would score low on distinctiveness or scalability.

### 4. Develop

Take the 5 to 7 survivors to clean, production SVG: square `viewBox` (default `0 0 100 100`), optically centered with roughly 10 to 14 percent padding, mono-first using `currentColor` so the monochrome version is the source of truth, fewest anchor points, even-odd negative space. Color only where it earns its place. See `references/svg-craft.md` and `references/color.md`.

### 5. Present

Show concepts in the gallery, never as raw SVG. Clone `assets/concept-gallery.html` and fill `CONCEPTS`. The gallery renders each mark large on light and dark, at 64, 32, 24 and 16px, inside real in-context mockups (browser tab, phone app tile, business card, signage, embroidery patch), with a mono toggle, the one-line rationale, the critique scores, and a copy-SVG button. Presenting in context is how studios sell work and how you stress-test it.

### 6. Iterate the winner

The user picks one (or asks to cross two). Refine along one axis at a time (weight, proportion, counter spacing, corner treatment, optical balance), producing 3 to 5 micro-variations. Apply optical correction (overshoot, visual centering, junction thinning) from `references/construction.md`. Tune, do not restart.

### 7. Identity system

Build the brand mark sheet as an HTML artifact per `references/brand-system.md`: symbol, horizontal and stacked lockups, mono positive and reversed, single-color print, color tokens (HEX and oklch), type system, clear space in mark units, minimum sizes, motion note, misuse, and application mockups. Wordmark and type guidance in `references/typography.md`.

### 8. Production handoff

Deliver each variant as clean, copyable SVG (`role="img"`, `title`, `aria-label`). Produce the full current favicon and app-icon set (SVG with dark-mode media query, 48px PNG for search, 16 and 32 PNG, 180 Apple touch on a solid background, 192 and 512 maskable with an 80 percent safe zone) per `references/svg-craft.md`. Note what to finish in Figma (outline and kern the wordmark) and how to export raster sizes.

## Hard rules (the spine)

- One idea per mark. Decoration is not an idea. If it needs a paragraph to explain, it is too complex.
- The critique gate is mandatory. You are the design director; kill your own weak work before the user sees it.
- Beat the category. If the mark could belong to any competitor, it has failed. Move away from at least one of the category's visual defaults on purpose.
- Neo-minimal, not sterile. Simple form plus one meaningful detail (a negative-space cut, a single chamfer, a custom counter, a deliberate asymmetry) beats both clutter and faceless minimalism.
- Mono before color. The mark must hold in one flat color first.
- Squint test and favicon test are pass-or-fail gates, run on every concept.
- No cliché metaphors, no gradients as a crutch, no bevels, drop shadows, faux 3D, photorealism, emoji, or stock-icon look. Full blocklist in `references/construction.md`.
- Tell the truth about Figma finishing. Never present a font-dependent `text` wordmark as a finished, portable logo.

## Reference files (read on demand, do not preload all)

- `references/strategy-and-ideation.md`, positioning front-end and the idea-generation engine. Read in phases 0 to 1, the highest-leverage file.
- `references/construction.md`, mark types and SVG suitability, gestalt, grid systems, optical correction, neo-minimalism, cliché blocklist, differentiation. Phases 1 to 6.
- `references/critique.md`, the 7-axis scoring rubric and design-director critique protocol. Phase 3 and before any presentation.
- `references/typography.md`, wordmark craft, type classification and pairing, recommended typefaces, the outline-in-Figma seam. Phases 1, 6, 7.
- `references/color.md`, palette construction, oklch, contrast and accessibility, sector meaning without cliché, dark and light behavior. Phases 4 and 7.
- `references/svg-craft.md`, production SVG, accessibility, optimization, dark-mode favicon and the full current favicon and app-icon set, export pipeline. Phases 4 and 8.
- `references/brand-system.md`, the identity system deliverable spec. Phase 7.

- `assets/concept-gallery.html`, gallery template with size grid and in-context mockups. Clone and fill `CONCEPTS`.
- `assets/brand-sheet.html`, one-page identity system template for phase 7. Clone and fill.
