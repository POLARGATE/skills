# Design System Spec

Read this when the user asks to generate, improve, audit or extend a design system. The output must be a complete system, not just a color palette.

A proper design system covers foundations, token architecture, required token categories, component specs and a motion system.

---

## 1. Foundations

Every design system needs explicit positions on:

- Brand personality
- Product personality
- Visual principles
- UX principles
- Accessibility principles
- Motion principles
- Content principles
- Responsive principles

Without these, every later decision is improvised.

---

## 2. Token architecture

Use three layers. Never collapse them.

```
Primitive  raw scales: colors, spacing, radius, shadows, typography, motion
   ↓
Semantic   product meaning: background, foreground, primary, accent, muted, danger, success
   ↓
Component  specific usage: button-bg, card-border, sheet-surface, nav-active, input-ring
```

Components consume **component tokens**. Component tokens reference **semantic tokens**. Semantic tokens reference **primitives**. Never let a component reach into a primitive directly.

For Tailwind + shadcn/ui projects, the tokens must map cleanly through:

- `index.css` (CSS variables)
- `tailwind.config.ts` (theme extension)
- Component variants (`cva`)
- Dark mode mappings

---

## 3. Required token categories

A complete token system covers all of these:

- color
- typography (family, size, weight, line-height, letter-spacing, tabular-nums)
- spacing
- radius
- shadow
- blur
- border
- z-index
- opacity
- motion duration
- motion easing/spring
- icon size
- layout width
- safe area
- chart/data colors
- status colors
- surface/elevation levels

Missing categories tend to produce inconsistency. If `z-index` is not tokenized, you get a stacking war. If `motion duration` is not tokenized, you get UI that feels different on every screen.

---

## 4. Component specs

Every component must have a written spec covering:

- Anatomy (parts of the component)
- Variants (visual flavors)
- Sizes
- States (default, hover, active, focus-visible, disabled, loading, success, error, empty, pending)
- Responsive behavior
- Accessibility requirements
- Motion behavior
- Token usage (which tokens it consumes)
- Examples
- Anti-patterns

### Required component set

A serious system covers at minimum:

- Button
- IconButton
- Card
- Sheet
- Dialog
- Input
- Select
- Textarea
- Checkbox
- Switch
- Tabs
- SegmentedControl
- Badge / Chip
- Toast
- EmptyState
- Skeleton
- Table
- DataCard
- StatCard
- NavItem
- Sidebar
- Header
- Footer
- FormField
- ErrorState
- PermissionState
- LoadingState

Anything beyond this is product-specific and should still follow the same spec discipline.

---

## 5. Motion system

Motion is part of the design system, not an afterthought.

Define:

- Micro-interaction duration
- Page transition duration
- Sheet/dialog motion
- List stagger
- Hover/tap feedback
- Reduced-motion fallback
- Spring presets
- Easing presets
- Transform-only rule (animate `transform` and `opacity`, never `width`/`height`/`top`/`left`)
- Animation budget (max concurrent animated elements)

### Example motion tokens

```ts
export const motionTokens = {
  duration: {
    instant: 0.08,
    fast: 0.16,
    base: 0.24,
    slow: 0.36,
  },
  spring: {
    snappy: { type: "spring", stiffness: 420, damping: 32 },
    smooth: { type: "spring", stiffness: 260, damping: 28 },
    gentle: { type: "spring", stiffness: 180, damping: 24 },
  },
};
```

Whatever values are chosen, they must be referenced consistently. Random `duration: 0.3` calls inside components are a smell.

---

## 6. Token compliance review

When auditing an existing system, look for:

- Hardcoded hex values inside components (`#111`, `#fafafa`, etc.).
- Hardcoded shadow strings (`shadow-[0_8px_40px_rgba(0,0,0,.4)]`).
- Hardcoded radius values (`rounded-[19px]`).
- Inline `rgba(...)` colors.
- Random gradients defined per component instead of in the system.
- Two competing icon families.
- Two competing radius scales.
- Two competing shadow scales.
- Light/dark mode mismatches caused by raw colors instead of tokens.
- Components that bypass `cva` and reinvent their own variant system.

Each of these is a signal that the system has not been enforced. Fix them at the system level, not per component.
