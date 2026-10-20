# UI/UX Priorities

Read this when the user asks to audit a UI, evaluate a screen, review interaction quality, or push something toward "premium" or "world-class" feel.

The categories are ordered by priority. Priority 1 problems must be fixed before Priority 10 polish. Do not let a beautiful animation system distract from broken accessibility or unreadable mobile layouts.

---

## Apple HIG precision (foundational)

Apply these principles before applying any priority category.

- Clarity over density.
- One dominant visual element per card/section.
- Generous, consistent spacing.
- Large touch targets.
- Immediate tap feedback.
- Native-feeling sheet/dialog behavior.
- Subtle depth via material, blur, shadow and hierarchy.
- Motion with purpose.
- Spatial continuity.
- Springs over generic easing where appropriate.
- Predictable navigation.
- Clear escape routes.
- Respect for safe areas.
- Reduced motion support.
- Legible typography.
- Visual calm around important decisions.

Avoid: excessive decorative animation, crowded cards, multiple primary CTAs, random glows, tiny icon buttons, overdesigned empty states, artificial "wow" that harms usability, non-native modal behavior, janky parallax, broken scroll locking, overlapping fixed elements.

Premium does not mean more decoration. Premium means more control, clarity, hierarchy and restraint.

---

## Priority 1: Accessibility

Verify:
- Contrast 4.5:1 for normal text.
- Contrast 3:1 for large text and icons.
- `focus-visible` state on every interactive element.
- Keyboard navigation reaches every interactive element.
- ARIA labels on icon-only controls.
- Semantic headings (one `h1`, ordered `h2`/`h3`).
- Alt text strategy.
- Skip links where relevant.
- Reduced motion respected.
- No color-only meaning.
- Sensible screen reader order.
- Form labels.
- Accessible errors (associated, not just colored).

Avoid: removing focus rings, icon-only buttons without labels, placeholder-only forms, decorative images without alt strategy, keyboard traps, unreachable controls.

---

## Priority 2: Touch and interaction

Verify:
- 44x44 px minimum tap target.
- Clear tap/press feedback.
- No hover-only interactions.
- Disabled states are semantic (not just visual).
- Loading buttons prevent duplicate submits.
- Gestures have visible alternatives.
- Safe-area awareness.
- Feedback within 100 ms.

Avoid: hidden swipe actions without affordance, overlapping gestures, invisible tap zones, layout-shifting press states, buttons that look active but do nothing.

---

## Priority 3: Performance

Verify:
- Optimized images.
- Dimensions / aspect-ratio reserved (no CLS).
- Lazy loading below the fold.
- Route-level code splitting.
- No unnecessary third-party scripts.
- No layout thrashing.
- No heavy animation on layout properties.
- List virtualization for large lists.
- Query caching.
- No request waterfalls.
- Degraded mode for slow network.

Avoid: loading admin dependencies on public landing, huge hero video without fallback, unbounded realtime listeners, giant bundles, excessive `framer-motion` on low-end devices, unoptimized background images.

---

## Priority 4: Style selection

Verify:
- Visual style matches product type.
- One icon family.
- One shadow / elevation scale.
- One radius system.
- One spacing system.
- Light/dark parity.
- Semantic color system.
- Primary action clarity.

Avoid: mixing flat / glass / clay / brutalist randomly, emojis as structural icons, random gradients, random glows, duplicate visual languages, over-customizing native controls.

---

## Priority 5: Layout and responsive

Verify:
- Mobile-first layout.
- Viewport meta correct.
- No horizontal scroll.
- Readable type.
- Proper line length.
- Adaptive gutters.
- Safe sticky / fixed elements.
- No nested scroll traps.
- Orientation support.
- Content priority on mobile.

Avoid: fixed pixel widths, desktop tables on mobile, disabling zoom, edge-to-edge long text on desktop, hidden content behind bottom bars, `100vh` mobile bugs.

### Required breakpoints to verify

320, 390, 768, 1024, 1280, 1440 px. Plus landscape on mobile where relevant.

### Responsive rules of thumb

- Use `min-h-dvh` instead of `100vh` on mobile.
- Use `safe-area-inset` for sticky/fixed UI on iOS.
- Use `max-w-*` containers.
- Use responsive grid and fluid typography.
- Use `aspect-ratio` to reserve media space.
- Use `overflow-hidden` only when intentional.

---

## Priority 6: Typography and color

Verify:
- Type scale.
- Line height.
- Weight hierarchy.
- Semantic colors (not raw hex).
- Dark mode contrast.
- Readable measure.
- Tabular numbers for data.
- Truncation strategy.
- Consistent labels.

Avoid: tiny body text, gray-on-gray, hardcoded colors, too many font weights, decorative type harming legibility, truncating critical info without expansion path.

---

## Priority 7: Animation

Verify:
- Motion has meaning.
- Duration 150 to 300 ms for micro-interactions.
- Transform / opacity only.
- Reduced-motion support.
- Interruptible animations.
- Consistent motion tokens.
- Exit faster than enter.
- Spatial continuity.
- No input blocking.

Avoid: animation for decoration only, animating `width`/`height`/`top`/`left`, long animations above 500 ms, janky parallax, motion that causes layout shift, multiple competing animated elements.

---

## Priority 8: Forms and feedback

Verify:
- Visible labels.
- Helper text.
- Inline validation on blur.
- Errors near fields.
- Error summary for complex forms.
- Loading state.
- Success state.
- Retry path.
- Destructive confirmation.
- Undo where useful.
- Draft autosave for long forms.
- Focus first invalid field.
- `aria-live` for errors and toasts.

Avoid: placeholder-only labels, generic "Invalid input", errors only at top, no submit feedback, destructive actions next to primary actions, losing user input after failure.

---

## Priority 9: Navigation

Verify:
- Clear hierarchy.
- Active state.
- Predictable back behavior.
- State preservation.
- Deep links.
- Breadcrumbs for deep web hierarchy.
- Adaptive nav by screen size.
- Persistent access to core nav.
- Destructive nav separated.
- Focus on route change.

Avoid: mixed nav patterns at the same hierarchy level, modal as primary navigation, overloaded sidebar, icon-only nav without labels, broken back stack, hidden navigation on deep pages.

---

## Priority 10: Charts and data

Verify:
- Correct chart type.
- Accessible colors.
- Legends.
- Tooltips.
- Table alternative.
- Responsive chart simplification.
- Empty / loading / error chart state.
- Number / date formatting.
- Keyboard-reachable chart interactions.
- Screen reader summary.
- Export option for data-heavy products.

Avoid: pie charts with too many categories, color-only meaning, unreadable axes, cramped labels, decorative gradients over data, rendering thousands of points without aggregation.

---

## Visual QA checklist (final pass)

Before approving a UI implementation, run this end-to-end checklist.

### Structure
- Clear hierarchy.
- One primary CTA.
- Consistent layout.
- Consistent page header.
- Consistent card anatomy.
- Consistent navigation.
- No orphan elements.

### Styling
- Semantic tokens only.
- No hardcoded colors.
- One icon system.
- One shadow system.
- One radius system.
- One spacing system.
- No random gradients/glows.
- Dark mode parity if supported.

### Interaction
- Hover, active, focus-visible, disabled, loading, success, error, empty.
- Keyboard.
- Touch.
- Reduced motion.

### Responsive
- 320, 390, 768, 1024, 1280, 1440 px.
- Landscape where relevant.
- No overflow.
- No clipping.
- Safe areas.
- Mobile nav / table behavior.

### Production
- TypeScript build clean.
- Lint clean.
- No console errors.
- No dead code.
- No unused imports.
- No duplicate components.
- No visual regressions.
- No route regressions.
- No broken permissions.
- No raw errors shown to users.
