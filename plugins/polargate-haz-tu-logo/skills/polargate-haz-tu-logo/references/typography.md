# Typography: wordmarks, type systems, and the honest seam

A wordmark or lockup lives or dies on type. This file covers how to choose and shape it, and where the vector-tool seam is.

Table of contents
1. The portability seam (read first)
2. Type classification and personality
3. Choosing a typeface
4. What makes a wordmark custom
5. Pairing for the system
6. Lockup typography
7. Recommended typefaces by personality

---

## 1. The portability seam (read first)

A logo built from a live SVG `text` element renders in whatever font the viewer has installed. If the font is missing, it silently falls back and the logo changes. Therefore a `text`-based wordmark is never a finished, portable logo.

How professionals handle this, and how you should:

- In Claude, you may mock a wordmark with `text` and a clearly-labeled fallback only to show layout and proportion. Always say it is a placeholder for outlined type.
- The production wordmark is set in Figma or Illustrator, kerned by hand, customized, then outlined to vector paths and exported as SVG. Those paths are font-independent and portable.
- This is not a limitation of taste, only of file portability. You can still decide the typeface, the customizations, the spacing, and the lockup here; the vector tool just executes the outlining.

State this in handoff every time a wordmark is involved.

## 2. Type classification and personality

Match the typeface class to the brand attributes.

- Geometric sans (e.g. constructed circular forms): modern, precise, neutral-confident. Tech and premium default, but overused, so customize.
- Grotesque / neo-grotesque sans: clean, industrial, trustworthy, Swiss.
- Humanist sans: warm, approachable, readable.
- Transitional / modern serif: editorial, authoritative, refined.
- Old-style / garalde serif: heritage, craft, literary.
- Slab serif: sturdy, mechanical, bold.
- Display / custom: distinctive but reserved for the logo, never body.

## 3. Choosing a typeface

- Personality fit first: the class must carry the attributes from strategy.
- Distinctiveness: avoid the exact faces every startup uses untouched. If you use a common geometric sans, customize at least one letter so it is not stock.
- Legibility at size: the wordmark must read at small sizes and in a browser tab next to the symbol.
- Licensing honesty: tell the user a retail or open-source font needs a proper license for commercial use, and that outlining to paths for a logo is standard practice. Recommend open-source options when budget matters.

## 4. What makes a wordmark custom

A great wordmark is rarely a font typed out. The identity lives in deliberate modifications:

- A single customized letter that carries the idea (a cut, an extension, a tie to the symbol).
- Tightened, hand-tuned kerning (default font spacing is never logo spacing).
- A ligature or shared stroke between two letters.
- A consistent terminal or corner treatment echoing the symbol.
- Optical weight balance so the word reads as one even color.

Decide these here; outline in Figma.

## 5. Pairing for the system

The logo's typeface is not necessarily the brand's UI typeface. For the identity system, recommend:

- A display or brand voice face (may be the wordmark face or a relative).
- A workhorse text face for UI and documents (highly legible across sizes and weights, good language coverage).
- Keep contrast clear between the two so they do not compete, and limit the system to two families plus weights.

## 6. Lockup typography

The lockup is a designed relationship, not a symbol next to text.

- Relate the symbol height to the wordmark: commonly symbol height equals cap height plus a small overshoot, or the full ascender-to-descender height. Choose and state it.
- Set the gap as a unit derived from the symbol (e.g. half the symbol width), then tune optically.
- Align on the optical center, not the bounding box.
- Provide horizontal and stacked lockups, each balanced on its own, not one rotated into the other.
- Lock the relationship: once set, it scales and moves as one unit and users do not re-space it.

## 7. Recommended typefaces by personality

Starting points, not mandates. Always check licensing and consider customizing.

- Modern precise tech: Inter is the overused default, avoid it untouched; prefer something with more character such as a customized geometric sans, or pair a distinctive display with a neutral text face. Open options include Space Grotesk (now common, customize), Geist, or a licensed geometric like a Futura relative.
- Premium and refined: a transitional or modern serif for the wordmark with a clean grotesque for UI.
- Heritage and craft: an old-style serif, hand-kerned.
- Industrial and bold: a slab or a tight neo-grotesque.
- Warm and human: a humanist sans with open apertures.

Do not converge on the same trendy face across projects. Vary deliberately and justify the choice against the attributes.
