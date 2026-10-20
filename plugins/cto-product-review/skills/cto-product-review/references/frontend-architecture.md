# Frontend Architecture

Read this when the user asks about React/Vite/Next architecture, Tailwind/shadcn patterns, component structure, forms, sheets/dialogs, state management, data fetching, or wants a code/architecture audit.

The goal: small composable components, thin pages, shared primitives, predictable data flow, and one source of truth for every visual or logical concept.

---

## Component architecture

### Principles

- One file = one responsibility.
- Composition over boolean-prop explosion.
- Slots / children over rigid monoliths.
- `cva` for visual variants.
- Page files are orchestrators, not dumping grounds.
- Business logic lives in hooks.
- Pure derivations live in utilities.
- Repeated UI patterns become shared components.
- Presentational components are mostly stateless.
- Data-fetching at page / container / hook level.
- Side effects are explicit and isolated.

### Avoid

- 700-line page files.
- Components with 15 boolean props.
- Duplicated markup across pages.
- Inline conditional style chaos.
- Business logic inside UI leaf components.
- Unrelated responsibilities in one file.
- Giant `useEffect` blocks doing everything.
- Fragile prop drilling when context/store would be cleaner.
- Premature abstraction that hides simple behavior.

### Preferred folder layout

```
src/
  components/
    ui/
      Button.tsx
      Card.tsx
      Sheet.tsx
      EmptyState.tsx
      StatusBadge.tsx
    dashboard/
      DashboardHeader.tsx
      ManagementCard.tsx
      DataToolbar.tsx
    feature-name/
      FeatureList.tsx
      FeatureCard.tsx
      FeatureSheet.tsx
  hooks/
    useFeatureQuery.ts
    useFeatureMutations.ts
    useFeatureFilters.ts
  lib/
    feature-utils.ts
    formatters.ts
    constants.ts
  pages/
    FeaturePage.tsx
```

---

## React / Vite / Next / SPA

### Required patterns

- Thin page components.
- Feature hooks.
- Shared primitives.
- Route-level lazy loading.
- Error boundaries.
- Suspense boundaries where useful.
- React Query for server state.
- URL search params for shareable filters/tabs/pagination.
- Optimistic mutations only with rollback.
- `keepPreviousData` for paginated lists.
- Proper query keys.
- No duplicate fetch logic.
- No avoidable prop drilling.
- No global state for simple local UI state.
- No local state for cross-route app state.

### Query keys

Preferred:

```ts
queryKeys.feature.list(filters)
queryKeys.feature.detail(id)
queryKeys.feature.stats()
```

Avoid:

```ts
["data"]
["items"]
["list"]
```

These collide and break invalidation.

---

## Tailwind / shadcn/ui

### Required

- Semantic tokens.
- `cva` variants.
- No raw hex.
- No random arbitrary values unless documented.
- Consistent component variants.
- Consistent radius / shadow / elevation.
- No modifying shadcn primitives destructively unless intentional.
- Wrap global primitives when product-specific behavior is needed.

### Preferred

```tsx
<Button variant="primary" size="lg">Save</Button>
```

### Avoid

```tsx
<button className="bg-[#111] text-white rounded-[19px] shadow-[0_8px_40px_rgba(0,0,0,.4)]">
  Save
</button>
```

---

## Forms

### Required

- `react-hook-form` + `zod` where applicable.
- Visible labels.
- Helper text.
- Field errors.
- Submit pending state.
- Disabled duplicate submit.
- Focus first invalid field.
- Server error mapping.
- Optimistic UX only when safe.
- Autosave for long forms.
- Unsaved changes guard for sheets.

---

## Sheets / Dialogs

### Required

- One reusable sheet/dialog primitive.
- Consistent animation.
- Consistent close behavior.
- Focus trap.
- Escape close.
- Swipe-down mobile close where appropriate.
- Safe-area padding.
- Unsaved changes confirmation.
- Scroll lock cleanup on route change.
- No weird diagonal motion.
- No double-close animation.
- No pop-up if app standard is sheet.

All edit flows should use the same primitive unless there is a strong reason not to. Mixing modals and sheets is one of the fastest ways to make an app feel inconsistent.

---

## State management

### Server state vs UI state

- **Server state**: React Query (or equivalent). Cached, invalidated, retried, paginated.
- **UI state**: local `useState` for local UI; URL search params for shareable UI state; context or store only for genuinely cross-route concerns.

Do not put server state in Zustand/Redux. Do not put ephemeral local UI state in global stores.

### Optimistic updates

Only use optimistic updates when:
- The mutation almost always succeeds.
- A failure rollback is implemented.
- The UI clearly indicates pending vs confirmed state where the difference matters.

---

## Cleanup discipline

Every change must leave the codebase cleaner. After any feature or refactor, remove:

- Dead components.
- Old variants.
- Unused imports.
- Unused styles.
- Duplicate files.
- Unused constants.
- Legacy classnames.
- Commented-out code.
- Orphaned hooks.
- Abandoned tokens.
- Replaced components.
- Duplicated visual systems.
- Temporary hacks.

Never keep old code "just in case" unless explicitly required for migration safety.

---

## Architecture review checklist

When auditing existing code, look for:

- Pages over ~300 lines.
- Repeated query logic across files.
- Repeated style strings across components.
- Components reaching into raw hex colors.
- Components owning their own animation constants.
- Effects with missing or wrong dependency arrays.
- Effects without cleanup.
- Multiple sources of truth for the same data.
- Multiple modal/sheet primitives.
- Multiple button/card/input variants.
- Untyped API responses.
- Service-role keys touching the client surface.
- Frontend-only validation for security-sensitive flows.

Each of these is a signal to consolidate, extract, or rewrite at the right layer.
