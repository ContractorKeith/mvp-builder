---
name: code-reviewer
description: Review generated code against the PRD, STACK.md decisions, and project conventions before marking a task done. Use this skill after any significant code generation — new files, new modules, API integrations, data models. Trigger before saying "task complete" on anything more than a trivial change.
---

# Code Reviewer

## Purpose
Catch problems before they compound. Review generated code against three things:
scope (PRD), decisions (STACK.md), and quality (conventions). A task isn't done
until it passes this check.

---

## The three-lens review

### Lens 1 — Scope (PRD)
Does this code do what the PRD says, and nothing more?

Checks:
- Does it implement the feature described, not a superset of it?
- Does it avoid anything in the "out of scope" section?
- If it adds something not in the PRD, flag it before committing

### Lens 2 — Decisions (STACK.md)
Does this code honor the technical decisions already made?

Checks:
- Correct language and runtime version?
- Using the approved dependencies, not alternatives?
- Following the chosen architecture pattern?
- Targeting the right data layer?

If the code deviates from STACK.md, flag it:
> "This uses [X] but STACK.md specifies [Y]. Want to update the decision or change the code?"

### Lens 3 — Quality (conventions)
Is this code maintainable and consistent?

Checks:
- Naming consistent with the rest of the project?
- No dead code, commented-out blocks, or debug artifacts?
- Error handling present where it matters?
- No hardcoded values that should be config or constants?
- Functions/methods doing one thing?

---

## How to run the review

1. Read the relevant PRD section
2. Read STACK.md
3. Review the generated code against both
4. List any issues found — one line each, categorized by lens
5. Fix issues or flag them to the user before moving on

Format:
```
Review — [task name]
Scope: ✓ / ⚠ [issue]
Stack: ✓ / ⚠ [issue]
Quality: ✓ / ⚠ [issue]
```

If all three pass: mark the task done and update SESSION.md.
If any flag: resolve before marking done.

---

## What this is NOT

- Not a security audit
- Not a performance review
- Not a style nitpick session

Keep it fast. The goal is catching real problems, not perfection.

---

## Common failure modes

- **Skipping scope check** — The most common way to build the wrong thing correctly.
- **Re-litigating stack decisions** — If STACK.md says SQLite, don't suggest Postgres in review.
- **Blocking on style** — Flag style issues once, then move on. Don't hold up the task.
