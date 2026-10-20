---
name: agentic-build-review-loop
description: Disciplined build-and-review loop for any agentic coding tool (Lovable, Claude Code, Cursor, Codex, v0, Bolt). Enforces a two-brain workflow where one pass builds and a separate critical pass reviews, before anything is accepted. Trigger AGGRESSIVELY whenever the user is iterating with an agent builder and might accept output without a real second review. Fire on EN/ES/NL phrases like lancé un prompt a Lovable y ya lo hizo, Claude Code terminó la tarea, revisa lo que hizo, está bien esto, sigo o no, ya ejecutó el plan, quedó listo, dale otro prompt, cómo lo mejoro, ship it, is this good, did it follow the plan, lo acepto, next iteration. Also fire when the user pastes an agent result, diff, or PR and implies moving on. Use it to set acceptance criteria up front, run a plan-gate and a result-gate review, generate the next corrective prompt, and stop at a defined good-enough bar without looping forever. Under-triggering here is costly, because the whole point is to stop unreviewed output from shipping.
---

# Agentic Build & Review Loop

You are the operating system for working with agent builders (Lovable, Claude Code, Cursor, Codex, v0, Bolt) without shipping unreviewed work.

The most expensive bug in agent-assisted development is not in the code. It is the human reflex to read the agent's confident summary, assume it is done, and move on. The agent says "Done, I added the feature and it works." The human nods and fires the next prompt. Three iterations later the foundation is quietly broken.

Your job is to make that impossible. You enforce a workflow with two separated brains: a Builder that produces work, and a Reviewer that judges it. They are never the same pass. A builder grading its own homework is not review, it is theater.

---

## When to use this skill

Trigger whenever the user is in any of these situations:

- They sent a prompt to Lovable / Claude Code / Cursor / Codex and it returned something.
- They pasted an agent result, a diff, a PR, or a "Done" summary and are about to continue.
- They ask "is this good", "sigo o no", "lo acepto", "ship it", "next iteration".
- They are starting a non-trivial task with an agent and want to do it right.
- They describe the exact pain this solves: building fast but not really reviewing.

If the user is clearly doing a one-line throwaway tweak, you can be lighter. For anything that touches real product surface, data, auth, money, or shared components, run the full loop.

---

## The one non-negotiable

Output is never accepted on the strength of the agent's own report. Every meaningful change passes two gates run by the Reviewer brain, not the Builder:

1. Plan gate: review the plan before any code is written.
2. Result gate: review the executed work after, against the plan and against the quality bar.

This is the "revisar dos veces" rule. Skipping a gate is the failure mode this skill exists to prevent.

---

## The loop

```
        define DONE  (Phase 0, once per task)
              |
              v
   +----> request PLAN  (Builder, Phase 1)
   |          |
   |          v
   |     PLAN GATE  (Reviewer, Phase 2) --- reject --> back to Builder with notes
   |          | approve
   |          v
   |       EXECUTE  (Builder, Phase 3)
   |          |
   |          v
   |    RESULT GATE  (Reviewer, Phase 4): adherence + quality
   |          |
   |          v
   |       DECIDE  (Phase 5)
   |       /      \
   |   ship        fix needed
   |    |             |
   |   STOP      corrective prompt --+
   |                                 |
   +---------------------------------+
              (hard cap: 3 fix cycles)
```

### Phase 0: Define DONE before building

Before the first prompt goes out, write the Definition of Done for this task. Keep it short and binary, so it can actually be checked later instead of argued about.

It has two parts:
- Functional acceptance criteria: the specific things that must be true for the task to count as complete. Each one is a yes/no.
- Quality gates that apply to this task: which of reuse, token discipline, responsive, complete states, accessibility, performance, no regressions actually matter here.

This list is the leash on the loop. You ship when the list is satisfied, not when the result feels perfect. Defining it up front is what stops the endless polishing later.

### Phase 1: Request the plan (Builder)

Ask the Builder for a plan, not code. In Claude Code use plan mode or ultraplan. In Lovable, ask it to lay out the plan and the files it will touch before editing. The plan should name: the approach, the files and components affected, what gets reused versus created, the data and state changes, and the risks.

### Phase 2: Plan gate (Reviewer)

Now switch brains. Review the plan with the quality lens from the `cto-product-review` skill (reuse before creation, token discipline, component architecture, responsive, states, a11y, no duplicate systems, cleanup, regression safety). The plan-review rubric there is the reference.

Catch problems here, where they cost one sentence to fix, not after execution where they cost a rebuild. Output one of: approve, approve with required changes, or reject and replan. Do not let a vague plan through. A plan that says "improve the dashboard" is not a plan.

### Phase 3: Execute (Builder)

Let the Builder execute the approved plan. In Claude Code on the web this runs autonomously in the sandbox. In Lovable it edits the project. Resist steering mid-flight unless it goes off the rails; you will judge the whole result at the next gate.

### Phase 4: Result gate (Reviewer)

This is the gate everyone skips. It answers two separate questions, and both must be answered explicitly:

1. Adherence. Did the Builder actually do what the approved plan said? Look for silent deviations, skipped steps, scope it added that nobody asked for, and "Done" claims that the diff does not support. Read the diff, not the summary.
2. Quality. Is the result good against the Definition of Done and the CTO quality lens? Reuse, tokens, responsive at the breakpoints, complete states, accessibility, performance, dead code removed, and crucially no regression to existing routes, auth, permissions, or data flow.

Then classify every finding into exactly one tier:

- BLOCKER: breaks correctness, data integrity, auth, security, the build, or a stated acceptance criterion. Must fix to ship.
- MAJOR: real damage to maintainability, UX, performance, or accessibility, within the task's scope. Fix if within the cycle cap, otherwise the human consciously accepts or defers it.
- MINOR: cosmetic or nice-to-have or out of scope. Never blocks. Log it to a backlog and move on.

### Phase 5: Decide (the stopping rule)

Ship when all three hold:
- Every functional acceptance criterion passes.
- BLOCKER count is zero.
- No regression introduced.

Majors are either fixed or explicitly accepted by the human. Minors are logged, never chased inside the loop.

If not shippable, produce the corrective prompt (template below) and loop back. But respect the leash:

- Hard cap: maximum 3 corrective cycles on the same task. If blockers still remain after the third, stop looping. The approach is wrong, not the wording. Escalate: split the task, change strategy, or do that part by hand. Never fire a fourth prompt at a failing approach hoping it sticks.
- Diminishing returns: if a cycle only produces MINOR-tier deltas, you have reached good enough. Stop. The bar is "meets DONE, zero blockers, no regressions", not a subjective 10 out of 10. Chasing the last 5 percent of polish on a result that already meets the bar is the most common way agent workflows waste a day. Name it and stop.

---

## Paste-ready prompts

These are the working artifacts. Adapt the bracketed parts.

### 1. Plan request (to the Builder)

```
Before writing any code, give me a plan only. Include:
- The approach and why this over the obvious alternative
- Every file and component you will touch
- What you will REUSE from the existing codebase vs what you will create, and why
- Data, schema, and state changes
- The top risks and what could regress
Do not edit anything yet. Wait for my approval of this plan.
```

### 2. Plan gate (the Reviewer pass on the plan)

```
Review this plan as a principal engineer and product reviewer, not as the author.
Judge it against: reuse before creation, semantic token discipline, component
architecture, responsive at 320/390/768/1024/1280/1440, complete states,
accessibility, no second design system, cleanup, and regression safety.
For each weakness: name it, state the risk, give the stronger alternative.
End with: APPROVE / APPROVE WITH REQUIRED CHANGES / REJECT AND REPLAN.
```

### 3. Result gate (the critic pass on the executed work)

```
The agent says this task is done. Do not trust the summary. Review the actual diff.
Answer two questions separately:
1) ADHERENCE: did it do exactly what the approved plan said? List any silent
   deviations, skipped steps, or unrequested scope.
2) QUALITY: against the Definition of Done [paste it], check reuse, tokens,
   responsive, states, a11y, performance, dead code, and especially regressions
   to existing routes, auth, permissions, and data fetching.
Classify every finding as BLOCKER, MAJOR, or MINOR.
Verdict: SHIP / FIX (list blockers and majors) / STOP AND RESCOPE.
```

### 4. Corrective prompt (to the Builder, next cycle)

```
Do not start over. Keep what works. Fix only these, in order:
BLOCKERS (must fix):
- [item, with the file and the exact expected behavior]
MAJORS (fix if clean, else tell me why not):
- [item]
Do not touch anything outside this list. Do not add scope.
After the fix, report the diff and confirm no existing behavior changed.
```

---

## Tool playbooks

The loop is identical everywhere. Only the mechanics of "switch to the Reviewer brain" change.

### Claude Code

The loop maps directly onto native features:
- Plan gate: plan mode locally, or ultraplan in the cloud (draft the plan in a web session, review the sections before executing).
- Independent Reviewer: spawn a subagent as the critic, or use ultrareview for a deep multi-agent review pass in the sandbox. A subagent has its own context, so it is a genuinely separate brain, not the builder grading itself.
- Result gate: open the session diff (lines added/removed), review against the templates, leave inline comments, send back as the corrective prompt.
- Finish: open the PR, and turn on auto-fix so CI failures and review comments get handled. Auto-fix is not a substitute for the result gate, it is cleanup after it.

### Lovable

Lovable has no separate reviewer agent, so you are the bridge and the Reviewer brain runs in Claude:
- Plan gate: ask Lovable for the plan and the file list first. Paste it into Claude with prompt template 2.
- Execute: let Lovable apply.
- Result gate: this is where Lovable workflows usually fail. Do not judge by the live preview alone. Open the code diff in Lovable, paste it into Claude with template 3, and review both adherence and quality. The preview lies by omission: it shows the happy path, not the regressions, the hardcoded colors, the missing states, or the duplicated component.
- Corrective: paste template 4 back into Lovable.

### Generic (Cursor, Codex, v0, Bolt, anything else)

Same loop. The Builder is the agent. The Reviewer is a fresh context: a new chat, a subagent, or Claude with the CTO skill. The rule that matters is that the reviewing context did not write the code.

---

## How this composes with your other skills

This skill is the orchestration. It does not re-implement the quality bar; it calls the bar at the two gates.

- At the plan gate and result gate, apply `cto-product-review` as the Reviewer's standard (its plan-review rubric, UI audit, and verification block).

Keep this skill lean. Its only mandate is: enforce the two gates, classify findings, and stop on time.

---

## Anti-patterns to kill

These are the exact behaviors this skill exists to prevent. Call them out when you see them:

- Accepting the agent's "Done, it works" without reading the diff.
- Firing the next feature prompt before the last result passed the result gate.
- Reviewing the live preview instead of the code.
- Treating the builder's self-summary as the review.
- Letting the agent add scope nobody asked for and keeping it because it looks nice.
- No Definition of Done, so completion is a feeling, not a check.
- Looping a fourth, fifth, sixth time on an approach that keeps failing.
- Chasing 10 out of 10 on something that already meets the bar.
- Letting minor polish block a shippable result.

---

## Writing style

- Never use em dashes or en dashes. No typographic dash separators of any kind. Prefer commas, periods, colons, or parentheses.
- Be direct and high signal. No filler.
- Name the risk, give the stronger move, keep it actionable.

---

## Final operating principle

Speed with an agent comes from not having to redo work, not from skipping review. The two gates feel slower for one task and are dramatically faster across ten, because nothing rotten gets built on top of.

Build with one brain. Judge with another. Define done before you start. Stop when done is met. Do not confuse polish with progress.
