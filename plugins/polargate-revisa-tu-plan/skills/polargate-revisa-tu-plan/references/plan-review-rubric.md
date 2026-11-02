# Plan Review Rubric

Read this when the user shares a Lovable plan, Claude Code plan, feature plan, refactor plan, or any other "should I build it like this?" request.

The job here is not to say whether a plan is good. The job is to evaluate it across every dimension that determines whether it survives production, and to return a sharper version the user can paste back into Lovable or Claude Code.

---

## Response structure

Use this scaffold and adapt. Do not skip sections; if a section does not apply, say so explicitly.

```markdown
## Verdict
Clear assessment: Strong / Good but incomplete / Risky / Not acceptable / Needs hardening

## What is good
Concrete strengths.

## Main risks
The most important product, UX, technical, architectural and production risks.

## What I would change
Specific improvements, ordered by impact.

## Missing execution details
What the plan forgot:
- states (loading, empty, error, success, disabled, pending, offline, permission)
- responsive
- accessibility
- tokens
- cleanup
- migration
- tests
- edge cases
- performance
- security
- data consistency
- rollback

## Improved prompt for Lovable / Claude Code
A rewritten, sharper prompt the user can paste directly. (See `references/prompt-rewrite-protocol.md` for the full template.)

## Acceptance criteria
A checklist to validate the implementation.

## Final recommendation
Whether to approve, modify, split into phases, or reject.
```

Be direct. Do not flatter weak plans. Do not approve vague plans. Do not let "premium", "cinematic" or "world-class" language hide missing execution details.

---

## Six review dimensions

Every plan must be evaluated across these six dimensions. Pick the dimensions that matter for the plan and report concretely.

### 1. Product strategy

Check:
- Does this solve the real user problem?
- Is the core user journey clearer after the change?
- Is the scope appropriate?
- Does it reduce friction?
- Does it improve conversion, retention, trust or speed?
- Does it distinguish available features from coming-soon features?
- Is there one clear primary action per screen?
- Does the plan protect the business model?
- Does it avoid overbuilding?
- Does it improve perceived quality?

Red flags:
- "Coming soon" presented as active functionality
- Too many CTAs
- Unclear user journey
- Visual redesign without product purpose
- Features built because they look cool
- Admin features without a permissions model
- MVP scope becoming enterprise build too early
- Lack of analytics or success metrics

### 2. UX/UI quality

Check: hierarchy, spacing, typography, color semantics, component consistency, motion quality, empty/loading/error states, responsive behavior, accessibility, visual coherence, interaction feedback, affordance clarity, information architecture, navigation predictability.

Red flags: decorative animation with no UX purpose, mixed icon styles, mixed radius/shadow systems, hardcoded colors, generic skeletons, dense mobile screens, inaccessible modals, unclear active states, hover-only actions, visual language not matching rest of app.

### 3. Frontend architecture

Check: component boundaries, hooks, state management, routing, data fetching, cache invalidation, optimistic updates, error boundaries, suspense/lazy loading, shared utilities, design token usage, type safety, separation of concerns.

Red flags: page file too large, business logic in UI components, repeated query logic, repeated style strings, manual DOM manipulation, global state for local concerns, local state for cross-screen concerns, useEffect abuse, missing cleanup, untyped API responses, fragile conditional rendering.

### 4. Backend / data / Supabase readiness

Check: RLS policies, database constraints, idempotent migrations, server-side validation, edge function error handling, pagination, indexes, audit logs, multi-tenant isolation, permissions by role, data ownership, optimistic UI consistency, storage access rules, public/private boundary, rate limits, sensitive data leakage, rollback safety.

Red flags: relying only on frontend validation, missing tenant filter, missing `deleted_at` filtering, public reads without justification, raw database errors shown to users, no indexes for new filters/search, no idempotency in migrations, no audit trail for admin actions, service role exposed or implied in client, edge function returns vague errors.

For deep Supabase patterns: `references/supabase-production.md`.

### 5. Performance

Check: initial bundle impact, route-level code splitting, lazy loading, image optimization, font loading, layout shift, scroll performance, animation cost, query waterfalls, caching strategy, list virtualization, responsive image sizes, third-party scripts, prefetch strategy, low-end device behavior.

Red flags: importing heavy libraries on landing page, large images without dimensions, layout shift from async content, animating width/height/top/left, no reduced-motion path, loading all admin code for public pages, no pagination, no memoization where needed, too many realtime subscriptions, no cleanup for listeners/subscriptions.

### 6. Production readiness

Check: TypeScript build clean, lint clean, no console noise, no dead code, no unused imports, proper environment variables, route fallback correct, SEO/OG correct where public, error boundary, analytics where needed, logging where needed, rollback path, migration safety, smoke test plan, cross-device verification.

Red flags: "tested visually" only, no build verification, no mention of states, no mobile validation, no acceptance criteria, no cleanup, no fallback, no monitoring/logging, no rollback plan.

---

## Product / CEO layer

When reviewing product plans, think beyond implementation. Ask:

- What business outcome does this improve?
- Does this reduce acquisition friction?
- Does this improve activation?
- Does this increase trust?
- Does this improve retention?
- Does this reduce support burden?
- Does this create operational leverage?
- Does this protect brand perception?
- Does this make the product easier to sell?
- Does this clarify what exists now vs what is future vision?

Always separate:
- Available now
- Beta
- Coming soon
- Vision

Never let a landing page sell future functionality as current functionality.

For MVPs, protect focus.
For SaaS, protect scalability and tenant isolation.
For admin tools, protect permissions, auditability and data quality.
For landing pages, protect clarity, trust and conversion.

---

## CTO layer

Think like a CTO before approving execution. Check:

- Is the architecture scalable?
- Does it create technical debt?
- Does it centralize or fragment the system?
- Is there a clean migration path?
- Are data boundaries safe?
- Are permissions explicit?
- Are failures recoverable?
- Is the implementation observable?
- Can another developer maintain this?
- Can this grow without rewrite?
- Does this increase or decrease operational risk?

Every recommendation must prefer: fewer systems, clearer ownership, stricter boundaries, better reuse, safer migrations, typed interfaces, explicit state, fewer hidden assumptions, better logs, better fallbacks, cleaner rollback.

---

## Implementation acceptance criteria

Every generated implementation plan must include acceptance criteria. Use this as the template; tailor to the specific feature.

```markdown
## Acceptance Criteria
- Reuses existing `DashboardHeader`, `ContentCard`, `Button`, `Sheet` and token system.
- No hardcoded colors, shadows or arbitrary gradients in the new components.
- Page file remains below 200 lines by extracting feature components/hooks.
- All async states are implemented: loading, empty, error, success and permission denied.
- Mobile layout verified at 320 and 390 px with no horizontal overflow.
- Tablet and desktop verified at 768, 1024, 1280 and 1440 px.
- All interactive controls are keyboard accessible.
- Icon-only controls include `aria-label`.
- Sheets trap focus, close with Escape and restore focus.
- Motion respects `prefers-reduced-motion`.
- TypeScript build passes.
- No unused imports or dead legacy components remain.
```
