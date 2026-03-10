---
name: task-breakdown
description: Break an oversized or ambiguous task into concrete, implementable steps. Use this skill whenever a task in TASKS.md is too large to complete in one pass, contains multiple distinct actions, or causes uncertainty about where to start. Trigger when a task takes more than ~30 minutes to implement or when the right first move isn't obvious.
---

# Task Breakdown

## Purpose
Turn a task that's too big or too vague into a sequence of steps small enough
to execute and verify one at a time. A well-broken task has a clear done state
at every step.

---

## When a task needs breaking down

Signs a task is too big:
- You're not sure where to start
- It touches more than 2-3 files or systems
- It has multiple "and then" clauses
- Completing it would take more than one focused work session

Signs a task is well-sized:
- One clear output (a function, a file, a passing test)
- You can describe "done" in one sentence
- It doesn't require decisions not already made in STACK.md

---

## How to break it down

### Step 1 — Read the task and the PRD
Make sure you understand what the task is trying to accomplish at the PRD level,
not just the literal task description. Knowing the "why" prevents you from
building the wrong thing correctly.

### Step 2 — Identify the natural seams
Most tasks break along these lines:
- **Data first** — schema, model, or data structure before any logic
- **Logic before UI** — backend/core before interface
- **Happy path before edge cases** — make it work before making it robust
- **Testable units** — if you can test it independently, it should be its own step

### Step 3 — Write the subtask list
Format for TASKS.md:

```markdown
- [ ] [Parent task name]
  - [ ] Step 1: [concrete action — one output]
  - [ ] Step 2: [concrete action — one output]
  - [ ] Step 3: [concrete action — one output]
```

Each step should:
- Start with a verb (Create, Add, Implement, Write, Configure)
- Have one clear output
- Be completable in under 30 minutes

### Step 4 — Confirm before starting
Show the breakdown to the user:
> "I've broken this into [N] steps: [list]. Start with step 1?"

Don't start until confirmed.

---

## Example

**Before:**
- [ ] Build the quote form

**After:**
- [ ] Build the quote form
  - [ ] Create Quote data model with required fields
  - [ ] Add form component with validation
  - [ ] Wire form submission to data layer
  - [ ] Add success/error states
  - [ ] Write basic smoke test

---

## Common failure modes

- **Breaking too small** — If a step takes 2 minutes, it doesn't need to be its own step.
- **Breaking by file** — "Edit file A, then edit file B" is not a breakdown. Break by logical unit.
- **Skipping the PRD check** — If you don't check the PRD, you might build the right steps toward the wrong goal.
