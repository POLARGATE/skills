# Prompt Rewrite Protocol

Read this when the user asks to rewrite, improve, or sharpen a prompt for Lovable, Claude Code, or any AI-assisted development tool.

The job is not just to clean up the wording. The job is to inject reuse-first discipline, design-token discipline, responsive coverage, accessibility, complete states, performance, cleanup, and verification into the prompt, so that the output of the AI tool comes back production-ready instead of a fragmented draft.

---

## Required ingredients in every rewritten prompt

A rewritten prompt must include all of these, even if the original prompt was only one sentence:

1. **Objective**. One paragraph, no fluff.
2. **Scope**. What is in, what is explicitly out.
3. **Existing-system audit requirement**. Force the AI to look first.
4. **Reuse-first instruction**. No new components if equivalents exist.
5. **Design token instruction**. Semantic tokens only, no hardcoded values.
6. **Component architecture instruction**. Small, composable, page files thin.
7. **Responsive breakpoints**. 320, 390, 768, 1024, 1280, 1440 px verified.
8. **Accessibility requirements**. Semantic HTML, keyboard, ARIA, contrast, reduced motion.
9. **State requirements**. Loading, empty, error, success, disabled, pending, permission/session/offline where relevant.
10. **Performance requirements**. Bundle, lazy load, transform-only motion, no waterfalls.
11. **Cleanup requirements**. Remove old/duplicated code.
12. **Files likely affected**. Be specific.
13. **Files explicitly not to touch** if there is a risk of regression.
14. **Acceptance criteria**.
15. **Build/test verification**.
16. **No-regression warning**.

---

## Template (copy and adapt)

```markdown
Act as a senior product engineer, UX/UI designer and frontend architect.

Objective:
[clear objective]

Before changing anything:
- Audit the existing implementation.
- Identify reusable components, hooks, tokens, animation patterns and layout primitives.
- Reuse existing patterns before creating anything new.
- Do not introduce a second visual language.

Implementation requirements:
- Use semantic tokens from `index.css` and `tailwind.config.ts`.
- Do not hardcode colors, shadows, gradients, spacing or z-index values in components.
- Keep components small and composable.
- Extract repeated logic into hooks/utilities.
- Use `cva` for variants where appropriate.
- Keep page files as thin orchestrators.

UX/UI requirements:
- Match the existing app visual language pixel-for-pixel.
- Follow Apple HIG principles: clarity, spacing, hierarchy, native-feeling motion, safe areas and clear feedback.
- One primary action per screen/section.
- All interactive elements must have visible hover, active, disabled and focus-visible states.
- Touch targets must be at least 44x44 px.

Responsive requirements:
- Validate at 320, 390, 768, 1024, 1280 and 1440 px.
- No horizontal overflow.
- No clipping.
- No layout shift.
- Tables/lists must adapt cleanly on mobile.

Accessibility requirements:
- Semantic HTML.
- Keyboard navigation.
- ARIA labels for icon-only controls.
- Focus management for sheets/dialogs.
- Contrast AA minimum.
- Respect prefers-reduced-motion.

States required:
- Loading with layout-matching skeleton.
- Empty state with CTA.
- Error state with retry.
- Success feedback.
- Disabled/pending state.
- Permission/session/offline states where applicable.

Performance requirements:
- Avoid unnecessary bundle growth.
- Lazy-load heavy components.
- Use transform/opacity for animation.
- Reserve image/media dimensions.
- Avoid query waterfalls.
- Clean up listeners/subscriptions.

Cleanup:
- Remove old/duplicated components/styles from the affected scope.
- Remove unused imports and dead code.
- Do not leave legacy variants coexisting with the new implementation.

Verification before final answer:
- State which existing components/tokens/hooks were reused.
- State what duplication was removed.
- Confirm TypeScript build is clean.
- Confirm responsive validation for all listed breakpoints.
- Confirm all required states are implemented.
- Confirm accessibility/focus/reduced-motion support.
- Confirm no visual language divergence was introduced.
```

---

## Output structure when rewriting a prompt

```markdown
Here is the improved prompt:
[copy-paste-ready prompt, fully formed]

Key improvements added:
- reuse-first constraint
- token discipline
- responsive validation
- state coverage
- accessibility
- cleanup
- production verification
- (any other specific improvements)
```

Keep the prompt itself in a single fenced block so the user can copy it cleanly.

---

## When to attach the brutal-quality verification block

If the user asks for "world-class", "premium", "Apple HIG", "design-award level", "best app in the world", or similar, append the brutal-quality verification block from `SKILL.md` to the rewritten prompt. Do not paraphrase it; copy it whole, because the AI tool reads it as a checklist.
