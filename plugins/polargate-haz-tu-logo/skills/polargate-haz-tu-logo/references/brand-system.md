# Brand identity system: from a chosen mark to a usable identity

The phase-7 deliverable. Build it as a single clean HTML artifact (clone `assets/brand-sheet.html`). A logo alone is not an identity; the system is what lets a non-designer apply it correctly forever.

Table of contents
1. Variant matrix
2. Clear space
3. Minimum sizes
4. Color tokens
5. Type system
6. Lockup construction
7. Favicon and app icon
8. Motion note
9. Misuse rules
10. Application mockups
11. Deliverable checklist

---

## 1. Variant matrix

Produce and show every applicable cell:

- Primary mark (symbol, full color).
- Symbol-only, for app icons, favicons, avatars.
- Horizontal lockup (symbol left, wordmark right).
- Stacked lockup (symbol above, wordmark below), for square and narrow contexts.
- Mono positive (brand ink or black).
- Mono reversed (white) on dark.
- Single-color print (one ink, for stamping or embroidery).

If the mark is an emblem, also ship a simplified symbol-only fallback for small sizes.

## 2. Clear space

Define the exclusion zone in mark units so it scales: e.g. clear space on all sides equals the height of the symbol's counter, or the symbol's key stroke width, called X. Show it with guide rules. Nothing intrudes into the zone.

## 3. Minimum sizes

- Digital: minimum symbol size in px (e.g. no smaller than 24px; favicon uses the dedicated small variant), minimum lockup width in px.
- Print: minimum width in mm.
- State which variant takes over below which threshold (below 24px drop the wordmark, use symbol-only; favicon uses the simplified mark).

## 4. Color tokens

Token table per `references/color.md`: each color with a semantic name, HEX, RGB, and oklch, plus neutrals and the mono and reversed definitions. Include contrast notes for any text usage.

## 5. Type system

Per `references/typography.md`: the logo typeface (with custom modifications noted), a display or voice face, and a workhorse text face for UI and documents, with weights. Keep to two families plus weights. Note licensing and that the wordmark ships as outlined paths.

## 6. Lockup construction

A designed relationship, not a symbol shoved next to text:

- Relate symbol height to wordmark cap height (state the rule).
- Set the gap as a symbol-derived unit, tuned optically.
- Align on optical center.
- Provide horizontal and stacked, each balanced on its own.
- Lock it: it scales and moves as one unit; users do not re-space it.
- Wordmark shown as outlined paths, or labeled as a placeholder if still mocked.

## 7. Favicon and app icon

Per `references/svg-craft.md`: SVG favicon with dark-mode variant, PNG fallbacks (48, 32, 16), 180 Apple touch on a solid background, 192 and 512 maskable with the 80 percent safe zone. Preview the icon at real small sizes and inside a rounded mask in the sheet.

## 8. Motion note

Marks increasingly live in motion (loaders, intros, app launch). Give one short, on-brand motion idea: how the mark builds, reveals, or loops, derived from its construction (e.g. the continuous path draws on; the counter rotates open). Keep it simple and true to the form; do not over-specify.

## 9. Misuse rules

A do-not panel with crossed-out examples:

- Do not stretch or distort proportions.
- Do not recolor outside the palette.
- Do not rotate the mark.
- Do not add effects (shadow, glow, bevel, gradient where the mark is flat).
- Do not place the color mark on low-contrast or busy backgrounds; use reversed or mono.
- Do not re-space or rebuild the lockup.
- Do not crop the symbol or violate clear space.

## 10. Application mockups

Show the mark living in the world; this is how studios prove a mark works and how the user sees its range: app icon on a phone, favicon in a browser tab, business card, signage or a wall, embroidery patch, social avatar. The concept gallery already includes these for selection; the system sheet shows them for the final mark.

## 11. Deliverable checklist

Before done:

- All variant-matrix cells present and correct.
- Mono positive and reversed tested on their backgrounds.
- Clear space and minimum sizes in mark units and concrete values.
- Color tokens with HEX and oklch, contrast checked.
- Type system with licensing and outlined-wordmark note.
- Lockups locked and balanced; wordmark outlined or labeled.
- Favicon and app-icon set with safe areas shown at real sizes.
- Motion note present.
- Misuse panel present.
- Application mockups present.
- Each final SVG delivered as clean, copyable code with `role="img"`, `title`, `aria-label`.
- Handoff note: what to finish in Figma and how to export raster sizes.
