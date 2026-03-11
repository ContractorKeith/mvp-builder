---
name: pre-build-checklist
description: A quick mental check to run before starting any task. Confirms you have what you need before writing a line of code. Prevents the "just start coding" impulse that produces misaligned work.
---

# Pre-Build Checklist

## Purpose
The most common way to build the wrong thing is to start building before you
fully understand what "right" looks like. This checklist takes two minutes and
prevents hours of rework.

Run it before every task. Not every session — every task.

---

## The checklist

### Do you have the spec?
- [ ] Have you read `PRD.md` for this task specifically, not just at session start?
- [ ] Do you know which PRD section this task is implementing?
- [ ] If the PRD is ambiguous on this task, have you resolved the ambiguity?

If you can't map this task to a specific PRD requirement, stop. Either the task
doesn't belong in this sprint, or the PRD needs clarification before you build.

### Do you know what "done" looks like?
- [ ] Can you describe done in one concrete sentence?
- [ ] Is done something you can actually verify — not just "it works" but
  "user does X, system does Y"?
- [ ] Do you know what a passing test for this task looks like?

"Done" is not "I've written the code." Done means the behavior matches the spec
and you can prove it.

### Are there dependencies?
- [ ] Does this task depend on anything that isn't built yet?
- [ ] Does anything else depend on this task finishing before it can start?
- [ ] Are there any decisions in `STACK.md` that affect how you implement this?

If there's a dependency that's not ready, don't start. Flag it and move to a
task that can proceed.

### Is anything ambiguous?
- [ ] Is there anything in this task you'd have to guess at?
- [ ] Is there anything that could reasonably be interpreted two different ways?
- [ ] Is there a decision the user needs to make before you can implement this correctly?

If yes to any of these — ask first. Don't guess and build. A 30-second question
saves a full re-implementation.

---

## When the checklist passes

Say what you're about to do in one sentence, then do it.

---

## When the checklist fails

**Missing spec context** — Read the relevant PRD section before starting.

**Ambiguous "done"** — Write out what done looks like and confirm it with the user
before building. One sentence: "Done means [X]. Sound right?"

**Unresolved dependency** — Flag it explicitly and move to a task that's unblocked.

**Needs a user decision** — Ask the question directly. Don't assume. Don't build
around it.

---

## Common failure modes

- **Running the checklist mentally without actually checking** — Write it out. The
  act of writing forces real answers, not assumed ones.
- **Starting on the interesting parts first** — Dependencies and spec ambiguity get
  worse the deeper you are into a task. Catch them before you start.
- **Treating "it seems obvious" as a substitute for a clear spec** — Obvious
  things are the most common source of misaligned implementations. Obvious to whom?
- **Skipping this on small tasks** — Small tasks are the ones where assumptions
  sneak in unchecked. The checklist is fast. Do it anyway.
