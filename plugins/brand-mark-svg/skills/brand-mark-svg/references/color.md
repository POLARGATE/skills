# Color: build a system, do not pick swatches

Color is the last decision in a mark, not the first. The mark must already work in one flat color. Then color adds meaning and differentiation. Read in phases 4 and 7.

Table of contents
1. Mono first, always
2. Building the palette
3. oklch and why
4. Accessibility and contrast
5. Sector meaning without cliché
6. Light and dark behavior
7. The token set to deliver

---

## 1. Mono first, always

Build and approve the mark in a single flat color (`currentColor`). If it needs color to work, the form is not resolved. Color is applied to a mark that already holds in black and white.

## 2. Building the palette

- Keep the symbol to one or two colors. More colors means more reproduction cost and more ways to fail.
- Choose a single brand seed color for meaning and differentiation, then derive a small, controlled palette around it: a dark ink, a light paper, one or two neutrals, and at most one accent.
- Derive tints and shades by stepping lightness while holding hue, rather than picking unrelated swatches. This keeps the palette coherent.
- A common distribution for applications is roughly 60 percent dominant neutral, 30 percent secondary, 10 percent accent. The accent is where the brand color earns attention.
- Do not invent clashing colors. Harmony comes from controlled steps off one or two seeds.

## 3. oklch and why

Define and extend palettes in oklch (lightness, chroma, hue) because it is perceptually uniform: equal lightness steps look equally different, and you can hold hue while changing lightness or chroma without the shifts you get in HSL or RGB. This makes consistent tint and shade ramps and accessible contrast tuning straightforward. Always also provide HEX for handoff, since most tools and developers expect it. RGB optionally.

## 4. Accessibility and contrast

- Any color used behind text or as text must meet contrast guidance. Check WCAG contrast ratios; for finer perceptual accuracy on text, APCA is the modern approach. State the contrast result for text usages.
- The mark itself should have a defined behavior on low-contrast and busy backgrounds: switch to the reversed or mono variant rather than forcing the color version.
- Never rely on color alone to carry meaning; the mark must still read in mono.

## 5. Sector meaning without cliché

Color carries associations, but the category default makes you invisible. If every competitor is blue (fintech, tech, health often are), blue is camouflage. Use association as a starting point, then differentiate:

- Decide what the color should signal (trust, energy, premium, calm, precision).
- Check the category's default colors. If you would land on the default, move deliberately: a different hue, an unexpected pairing, or a distinctive neutral.
- Differentiation through color is one of the cheapest ways to stand out in a crowded category.

## 6. Light and dark behavior

- Define the mark on both a light and a dark field, and confirm both in the gallery.
- For favicons, provide a dark-mode SVG variant via a `prefers-color-scheme` media query inside the SVG (see svg-craft.md), so the mark stays legible on dark browser UI.
- Ensure the accent color has enough contrast on both paper and ink backgrounds, or define a separate on-dark accent.

## 7. The token set to deliver

In the identity system, deliver a clean token table. For each color: a semantic name, HEX, RGB, and oklch.

Example shape (replace with the real palette):

- Brand / Ink: `#0B1F3A`, oklch(0.27 0.06 255)
- Brand / Accent: `#4FA3FF`, oklch(0.72 0.13 250)
- Neutral / Paper: `#FFFFFF`
- Neutral / Graphite: `#1A1D21`
- Mono positive: Ink on Paper
- Mono reversed: Paper on Ink or Graphite

Include the on-light and on-dark rules and any contrast notes.
