# Sub-skill: Build / update the Voice & Brand Profile

Builds or refreshes `linkedin/voz.md` so every writing guide in
this skill drafts in the user's real voice instead of a generic "human" voice.
It only needs a few posts the user pastes in.

## When this runs

- User says "build my voice profile", "learn my voice", "set up my profile", or
  invokes `quitar-pinta-de-ia --mode profile`.
- Also offer it the first time a writing guide runs and finds `filled: no`.

## Inputs (any one is enough)

1. **Pasted samples (portable default).** Ask for 3-6 of the user's own real
   LinkedIn posts or comments. This alone is enough; no token, no history needed.
2. **Manual.** The user can also just tell you their niche, rules, and links.

## Steps

1. **Gather what the user gives.** With samples: 3+ real posts of theirs, pasted.
   With the manual route: what they tell you about their niche, rules, and links.
2. **Extract the voice fingerprint** from the samples, not from assumptions
   (manual route: skip this step, see step 5):
   - sentence-length rhythm (short/medium/mixed, and how often a long line appears)
   - recurring openers and transitions they actually use
   - punctuation habits (soft `..` pause? never em dashes? line breaks per idea?)
   - vocabulary they lean on, and any words/cliches they clearly avoid
   - emoji and hashtag behavior
3. **Infer niche, ICP, and pillars** from the sample topics (manual route: from
   what the user said); confirm with the user rather than guessing.
4. **Capture hard rules and CTA/link style** the samples reveal or the user states.
5. **Write `linkedin/voz.md`**: fill sections 1-5, copy the 2-4
   strongest lines verbatim into "Signature examples", and set the Status block to
   `filled: yes`, `source: <pasted|manual>`, `updated: <today's date>`.
   With the manual route, fill only what the user stated: write "not enough
   samples yet" in section 1, leave "Signature examples" empty, and never invent
   voice traits.
6. **Show the user the filled profile for approval** before saving, and tell them
   any writing guide will now match it automatically. They can edit the file anytime.

## Hard rules

- Build the fingerprint from the user's ACTUAL samples. Never invent a voice.
- Preserve their quirks (a favorite phrase, an unusual rhythm). Those are the
  point. Only the generic AI-tell scrub still applies to drafts later, not to the
  profile itself.
- Keep it honest about coverage: with 3 samples say the profile is a first pass and
  will sharpen as they add more; suggest re-running after 10+ posts.
- Never put secrets, private data, or anything the user did not provide into the file.

## Related

- The filled profile is read by `escribir-post` and `reutilizar` before they draft.
- Re-run this any time the user's voice or focus shifts to refresh the profile.
