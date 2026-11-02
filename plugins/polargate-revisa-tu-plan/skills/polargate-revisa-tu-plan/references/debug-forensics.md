# Debug & Forensics

Read this when the user reports a bug, runtime error, build failure, strange UI behavior, stale data, cache suspicion, race condition, hydration mismatch, or any "why is this happening" question.

The goal: find the source of truth, verify with direct evidence, fix minimally, prevent regression.

---

## Core principles

- One direct query to the source of truth beats ten hypotheses.
- The visual may lie. The query, log, or build output does not.
- Verify before acting.
- Never assume cache.
- Never assume a race condition.
- Never assume runtime issue.
- Never assume the UI is the source of truth.
- Backup before touching critical models or production data.

---

## Debug flow

1. Identify the symptom precisely.
2. Identify the source of truth (database query, server log, build artifact, network response).
3. Reproduce minimally.
4. Inspect actual data / log / query / build result.
5. Isolate the smallest failing unit.
6. Compare expected vs actual.
7. Test one hypothesis at a time.
8. Patch minimally.
9. Verify with direct evidence (not just visual confirmation).
10. Clean up after the fix (no leftover debug code, no commented-out fallback).

---

## Forensics checklist

Ask, in this order:

- What is the exact failing screen / query / build / flow?
- What changed recently? (commits, migrations, dependency updates, infra changes)
- Is the problem visual, data, cache, permission, runtime, build, route, or state?
- Is the UI showing stale data?
- Is the query returning correct data?
- Is the cache invalidated correctly?
- Is there an optimistic update mismatch?
- Is the route rendering the wrong component?
- Is there a duplicated source of truth?
- Is there a hidden RLS / permission issue?
- Is there a type mismatch between API and frontend?
- Is there a race condition?
- Is there a stale closure?
- Is there a broken dependency array?
- Is there a CSS / `z-index` / `overflow` issue?
- Is there a hydration / prerender mismatch?
- Is the production build different from dev (env vars, tree shaking, minification)?

Most "weird" bugs land in one of these buckets. Walk the list before speculating.

---

## Before changing critical code

Always recommend:

- Backup.
- Branch.
- Migration snapshot if a DB change is involved.
- Minimal reproducible test.
- Direct source-of-truth verification.
- Rollback plan.

---

## Debug output format

```markdown
## Likely root cause
[one or two sentences naming the most probable cause based on evidence]

## Evidence needed
[what to query/log/inspect to confirm or rule out]

## Fastest verification
[the cheapest way to prove the hypothesis right or wrong]

## Minimal fix
[the smallest change that resolves it]

## Safer long-term fix
[the structural change that prevents the bug class from recurring]

## Regression checks
[what to verify after the fix is applied]
```

If the user is in panic mode (production is down), keep the output sharp: root cause, fastest verification, minimal fix. Save the long-term fix for after the fire is out.

---

## Common bug categories and where to look first

| Symptom | Look first at |
|---------|---------------|
| UI shows stale data after mutation | Query invalidation, optimistic update rollback |
| "Works in dev, breaks in prod" | Env vars, build config, tree shaking, SSR/CSR boundary |
| Hydration mismatch warning | Server vs client conditional rendering, time/locale-dependent code |
| `z-index` not respected | Stacking context (transform, opacity, will-change creates new context) |
| Modal not closing | Focus trap, scroll lock, route change cleanup |
| Form loses input on error | Form library reset behavior, server error mapping |
| Realtime subscription duplicates | Missing cleanup in `useEffect`, multiple instances mounted |
| Permission denied where expected access | RLS policy, JWT claims, tenant scope in query |
| Slow page on first load | Bundle size, font loading, render-blocking scripts, missing `loading="lazy"` |
| Layout shift | Missing `width`/`height` on images, async content without reserved space |
| Touch target unresponsive on iOS | Safe-area inset, overlapping fixed element, `pointer-events: none` higher up |

---

