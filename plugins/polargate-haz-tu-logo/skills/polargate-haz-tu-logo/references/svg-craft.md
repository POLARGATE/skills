# SVG craft: clean, portable, production vectors

Table of contents
1. ViewBox and coordinate system
2. Mono-first with currentColor and theming
3. Path discipline
4. Strokes vs fills
5. Accessibility
6. Optimization (SVGO)
7. Reusable snippets
8. Font and text pitfalls
9. Favicon and app icon: the current set
10. Dark-mode favicon
11. Export pipeline

---

## 1. ViewBox and coordinate system

- Square `viewBox` by default: `viewBox="0 0 100 100"`. Round-number canvas keeps coordinates readable.
- Optically center the content with roughly 10 to 14 percent padding; do not let artwork touch the edges.
- Do not hard-set root `width` and `height` when the mark should scale; let CSS or the container size it. If you must, keep them equal to preserve the square.
- Keep origin and scale consistent across every variant so lockups align predictably.

## 2. Mono-first with currentColor and theming

Build the source-of-truth mark in one color using `currentColor`, so it inherits text color and one file works in any color by setting `color` on a parent.

```html
<svg viewBox="0 0 100 100" role="img" aria-label="Brand mark"
     xmlns="http://www.w3.org/2000/svg" fill="currentColor">
  <title>Brand mark</title>
  <path d="..." />
</svg>
```

- Mono positive: parent `color:#111` (or brand ink). Reversed: parent `color:#fff` on dark.
- For two-color marks, expose colors as CSS custom properties with fallbacks: `fill="var(--mark-accent, #0A84FF)"`.
- Reserve hard-coded fills for the genuinely multi-color final variant.

## 3. Path discipline

- Fewest anchor points that express the idea; every extra point is a wobble and a tell of machine output.
- Prefer primitives (`circle`, `rect rx`, `line`, `polygon`) when they express the form exactly; smaller and easier to tune than paths.
- For curves, deliberate cubic beziers (`C`, `S`), not auto-traced spaghetti.
- Carve counters and negative space with one path using `fill-rule="evenodd"` rather than stacking shapes.
- Round coordinates to whole or half units. Avoid long decimals.
- Add `id` only when a variant or the system references it.

## 4. Strokes vs fills

- Filled shapes scale predictably; safest default.
- Monoline marks: `stroke="currentColor"`, `fill="none"`, `stroke-width` from the base unit, consistent `stroke-linecap` and `stroke-linejoin`.
- Logo strokes should scale with the mark, so do not use `vector-effect="non-scaling-stroke"` unless you specifically want a hairline fixed at all sizes (rare for a logo).
- Thin strokes clog or vanish small; if a monoline fails the favicon test, ship a heavier or filled small-size variant.

## 5. Accessibility

Every delivered standalone mark:

- `role="img"` on the root `svg`.
- `<title>` as the first child (the accessible name), e.g. brand name plus "logo".
- `aria-label` matching the title.
- `<desc>` only if a longer description is needed.
- Where the SVG is decorative and the brand name is already adjacent as text, that instance may use `aria-hidden="true"` instead. Decide per placement; the standalone asset is labeled.

## 6. Optimization (SVGO)

- Strip editor cruft: no `<metadata>`, no editor namespaces, no empty groups, no default attributes.
- Collapse transforms into coordinates where practical.
- Round numbers; one consistent styling approach (attributes or a single `<style>`), not both scattered.
- Recommend SVGO to the user for final minification, but deliver human-readable SVG they can still edit; do not hand over a minified blob.

## 7. Reusable snippets

Monogram carved with evenodd:

```html
<svg viewBox="0 0 100 100" role="img" aria-label="A monogram" fill="currentColor"
     xmlns="http://www.w3.org/2000/svg">
  <title>A monogram</title>
  <path fill-rule="evenodd" d="M50 8 L88 92 H70 L50 44 L30 92 H12 Z" />
</svg>
```

Monoline mark:

```html
<svg viewBox="0 0 100 100" role="img" aria-label="Monoline mark"
     fill="none" stroke="currentColor" stroke-width="10"
     stroke-linecap="round" stroke-linejoin="round"
     xmlns="http://www.w3.org/2000/svg">
  <title>Monoline mark</title>
  <path d="M22 70 L50 26 L78 70" />
</svg>
```

These are scaffolds to adapt, not finished marks.

## 8. Font and text pitfalls

- A live `<text>` wordmark renders in the viewer's font and is not portable. Never deliver it as a finished logo.
- To mock a wordmark for layout only, use `text` with a labeled common fallback and say it is a placeholder.
- The real wordmark is set, kerned, and outlined to paths in Figma or Illustrator, then exported as SVG (see typography.md).
- Do not embed whole font files into an SVG to dodge this; it bloats the file.

## 9. Favicon and app icon: the current set

The modern minimal, robust set (verified against current practice):

```html
<!-- Scalable modern browsers -->
<link rel="icon" href="/favicon.svg" type="image/svg+xml">
<!-- PNG fallbacks (SVG favicons are not universal on Windows/Android) -->
<link rel="icon" type="image/png" sizes="48x48" href="/favicon-48.png">
<link rel="icon" type="image/png" sizes="32x32" href="/favicon-32.png">
<link rel="icon" type="image/png" sizes="16x16" href="/favicon-16.png">
<!-- Legacy -->
<link rel="icon" href="/favicon.ico" sizes="any">
<!-- Apple home screen: single 180, SOLID background, no transparency -->
<link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png">
<!-- PWA / Android via manifest -->
<link rel="manifest" href="/site.webmanifest">
```

Rules:

- Provide an SVG favicon plus PNG fallbacks; do not rely on SVG alone, as Windows and some Android contexts still need PNG.
- Google needs a square PNG of at least 48px, same-domain, for search results.
- Apple touch icon: a single 180x180 PNG on a solid (opaque) background; iOS rounds the corners, so do not pre-round and do not use transparency.
- Android maskable (manifest `192` and `512`, `purpose: "maskable"`): keep key content inside the centered 80 percent safe zone, with padding, because launchers crop to varied shapes.
- iOS app icon (in-app store asset): full-bleed opaque square, mark within the centered ~80 percent safe area, system applies the mask.
- The favicon should be the simplest version of the mark; drop detail meant for large use.
- Do not overload the head with the old long list of sizes; the set above covers modern needs.

## 10. Dark-mode favicon

Provide a dark-mode SVG favicon using a media query inside the SVG so it stays legible on dark browser UI:

```html
<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
  <title>Brand</title>
  <style>
    path { fill: #111; }
    @media (prefers-color-scheme: dark) { path { fill: #fff; } }
  </style>
  <path d="..." />
</svg>
```

Note: dark-theme SVG favicons are honored unevenly across browsers (some only follow the OS theme), so keep the mark legible on both regardless.

## 11. Export pipeline

- Keep the master as vector; raster is always an export, never the source.
- Rasterize to PNG sizes in a script with `resvg`, `rsvg-convert`, or `sharp`, or export from Figma. Do not hand-resize by editing coordinates.
- Generate the favicon set with the source SVG plus a generator (for example RealFaviconGenerator) or your own script; verify on light and dark tabs and at 16px.
