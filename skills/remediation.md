---
name: remediation
description: Turn accumulated feedback into a structured fix pass. Collects all feedback, groups it by theme, classifies and prioritizes it, then executes as a single cohesive batch. Use when feedback has piled up after a build — not for single bug fixes.
---

# Remediation

## Purpose
When feedback comes in — bugs, things that don't behave as expected, user complaints,
failed tests — the instinct is to fix them one at a time. That instinct causes
regressions. Fix A breaks B. Fix B breaks C. You're chasing problems in circles.

Remediation is the alternative: collect everything first, plan once, execute once.

---

## When to use

- After a build ships and feedback has accumulated
- When a pattern of failures is showing up across multiple areas
- When the user says "here's my feedback" or "let's clean this up"

**When NOT to use:**
- Single bug that's clearly isolated → just fix it
- New feature that wasn't in the original scope → that's a new build task, not remediation

---

## Phase 1 — Collect everything first

Before fixing anything, gather all feedback into one place.

Ask the user:
> "Dump everything. What's broken, what's frustrating, what doesn't match what
> you expected. Don't filter — I'll sort it."

Also pull in:
- Test failures (what's failing and what the failure message says)
- Console errors or runtime issues
- Any known shortcuts or debt from the original build

Save it all to `outputs/feedback.md`. Do not start fixing until this is complete.

---

## Phase 2 — Organize and classify

Group the feedback by theme, not by source. "Login is broken" might show up in
the user's feedback, a test failure, AND a console error — that's one theme.

Classify each item:
- 🔴 **Broken** — Doesn't work as designed. Fix before anything else.
- 🟡 **Wrong** — Works, but doesn't match what was intended. Fix after broken items.
- 🟢 **Polish** — Works and matches intent, but could be better. Fix last, or defer.

Sequence into tasks — each task small enough to complete in one focused session.

**Present the plan to the user before executing:**
> "Here's what I'm seeing: [X] broken items, [Y] wrong items, [Z] polish items.
> My plan is to address them in this order: [list]. Does this capture everything?"

Wait for confirmation.

---

## Phase 3 — Execute in order

Work through the plan: 🔴 first, then 🟡, then 🟢.

**Critical rule:** After every single fix, run the full test suite — not just tests
related to that fix. The whole point of batching remediation is to catch regressions.
A fix that breaks something else is worse than the original problem.

After each fix:
> "✅ Fixed [item]. All existing tests still passing. Next: [item]. Ready?"

Don't batch tasks without confirmation between them unless the user explicitly
asks you to run through the list autonomously.

---

## Phase 4 — Validate the full pass

When all items are addressed:
- Run every test one final time
- Walk through the core user flows manually
- Confirm each 🔴 and 🟡 item is actually resolved

Present results:
> "Remediation complete. [N] items fixed. Test suite passing. Here's what changed: [summary]."

If anything was deferred (🟢 polish items, things out of scope), document them
explicitly so they don't get lost.

---

## Common failure modes

- **Fixing piecemeal** — Starting fixes before you've collected all feedback means
  you'll fix things in the wrong order and miss patterns.
- **Skipping the full test suite** — Running only new tests after a fix is how
  regressions hide. Run everything after every change.
- **Treating polish as urgent** — 🟢 items feel satisfying to fix but they're not
  blocking. Do 🔴 first. Always.
- **Re-opening scope** — Remediation is not the time to add features that weren't
  in the original build. Flag those separately and handle them as new tasks.
- **Skipping confirmation before execution** — The user may have different priorities
  than your classification suggests. Always show the plan and wait for a yes.
