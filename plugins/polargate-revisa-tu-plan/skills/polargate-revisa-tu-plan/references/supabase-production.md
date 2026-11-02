# Supabase Production / SEO / Security

Read this when the user is working on a Supabase-backed product, multi-tenant SaaS, admin portal, public landing page, or anything where data ownership, permissions, or production safety are at stake.

This reference is opinionated about Supabase because that is the user's primary stack. The patterns generalize to any Postgres-backed multi-tenant system.

---

## 1. Database

Required:

- Tenant / company / project / wedding scope present on every multi-tenant table.
- RLS enabled on every multi-tenant table.
- Policies correct (read, insert, update, delete each evaluated independently).
- Constraints enforce business rules at the database level.
- Unique indexes where business uniqueness must be guaranteed.
- Partial indexes for soft deletes (`WHERE deleted_at IS NULL`).
- `created_at` / `updated_at` timestamps.
- Audit logs for admin actions.
- Idempotent migrations.
- Safe rollback path for every migration.
- Foreign keys.
- Cascade behavior intentional and documented.

---

## 2. Edge functions

Required:

- Server-side validation (never trust the client).
- No client-trusted permissions logic.
- No service-role exposure.
- Structured error responses (typed, no stack traces leaked).
- Logs without sensitive leakage (no tokens, no PII in logs).
- Rate limiting where the function is exposed publicly.
- Clear CORS strategy.
- Typed request and response.
- Safe handling of missing environment variables (fail loud, not silent).

---

## 3. Storage

Required:

- Bucket privacy correct (default to private, justify public).
- Signed URLs where access control is needed.
- Upload size and type validation.
- Path includes tenant/user scope where needed.
- No cross-tenant leakage through path conventions.

---

## 4. RLS red flags

Never accept:

- Frontend-only tenant filtering.
- Broad `public` SELECT without justification.
- User can update records without ownership check.
- Service role assumed in client flow.
- No policy for soft-deleted records (records reappear after "delete").
- Policies that expose other tenants through joins.
- Missing INSERT policy that lets anyone write.

The mental model: the database is the security boundary. The frontend is convenience. Frontend filters are a UX optimization, not a security control.

---

## 5. Migration safety

Every migration should:

- Be idempotent (re-running it does not break things).
- Have a documented rollback.
- Avoid destructive operations on production data without backup.
- Be tested against a copy of production schema first.
- Be applied during a known maintenance window for risky changes.

For risky changes (column drops, type changes, large data backfills), prefer a multi-step migration: add new column → backfill → swap reads → swap writes → drop old column. This is slower but reversible at every step.

---

## 6. SEO checklist (public sites)

For public websites and landing pages, verify:

- Title.
- Description.
- Canonical.
- OG tags.
- Twitter tags.
- Favicon / PWA icons.
- Sitemap.
- `robots.txt`.
- Structured data where applicable.
- Language alternates if multilingual.
- Static OG for crawlers if SPA.
- Correct Vercel rewrites (or equivalent).
- No private/admin content indexed.
- Good heading hierarchy.
- Image alt text.
- Fast LCP.
- No massive JS required for basic content.
- Content distinguishes "available now" vs "coming soon".

This is a checklist, not an SEO strategy. For deeper SEO work (keyword research, content strategy, link building, schema specifics) a dedicated SEO skill or specialist is the right tool.

---

## 7. Security checklist

For implementation plans, detect obvious risks:

- Exposed API keys.
- Service role in client.
- Weak auth redirects.
- Missing role checks.
- Raw database errors shown to users.
- File upload abuse (unbounded size, no type check, executable types).
- Unsafe HTML rendering (`dangerouslySetInnerHTML` from user content).
- XSS via user content.
- Missing CSRF strategy where relevant.
- Open redirects.
- Tenant data leakage through URLs or query params.
- Insecure public routes.
- Missing rate limits on auth or expensive endpoints.
- Missing audit logs for admin/destructive actions.

Do not turn every UI review into a security review, but never ignore visible security risks. For deeper security work (threat modeling, pentest, compliance), a dedicated security skill or specialist is the right tool.

---

## 8. Production-readiness questions for Supabase plans

Before approving any Supabase-backed plan, answer these explicitly:

1. Which tables are multi-tenant? Do they all have tenant scope and RLS?
2. Which routes are public? What policies allow that?
3. What happens if RLS denies a query? Does the UI degrade gracefully?
4. What is the migration strategy? Idempotent? Rollback?
5. Where does validation live? Frontend, edge function, database constraints, or all three?
6. What does the audit trail look like for admin actions?
7. Are there indexes for the new filters/sorts/searches?
8. Are realtime subscriptions cleaned up on unmount?
9. What is the rate-limit story for public edge functions?
10. Are storage buckets private by default?

If any of these is "we will figure it out", the plan is not production-ready yet.
