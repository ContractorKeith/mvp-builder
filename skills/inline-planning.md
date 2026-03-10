---
name: inline-planning
description: Run a lightweight planning pass when no project-planner handoff exists. Use this skill when the user opens mvp-builder without PRD.md, STACK.md, or TASKS.md — and wants to plan quickly before building. This is a fast-track version of the full project-planner workflow, covering the minimum needed to start building safely. Trigger when handoff files are missing and user wants to proceed.
---

# Inline Planning

## Purpose
Get from "I want to build X" to a working build context in 10-15 exchanges,
without the full project-planner workflow. The output is the minimum viable set
of handoff files so the build loop can start.

This is the shortcut. For complex projects, use `project-planner` instead.

---

## When to use this vs project-planner

| Use inline-planning | Use project-planner |
|---|---|
| Small, well-understood project | Complex or ambiguous problem |
| Solo builder, no stakeholders | Multiple users or stakeholders |
| Clear tech already in mind | Stack needs real evaluation |
| Want to start building today | Worth spending a session planning |

When in doubt, ask the user:
> "This will take about 10 minutes inline. If you want a deeper plan, you can run
> `project-planner` first. Which do you prefer?"

---

## The fast-track interview

Ask these in order. One at a time. Stop when you have enough.

1. **"What are you building?"** — Get the one-liner.
2. **"Who is this for — just you, a small team, or customers?"** — Determines scale.
3. **"What does done look like? How will you know it works?"** — Success criteria.
4. **"What's out of scope? What should this NOT do?"** — Non-negotiable.
5. **"Any tech constraints? Preferred language, must-use tools, must-avoid tools?"** — Unlocks stack.
6. **"Rough timeline — days, weeks, or 'whenever'?"** — Affects scope discipline.

Stop at 6 if you have what you need. Ask follow-ups only if something is unclear.

---

## Outputs to generate

Create these files before starting the build loop:

**PRD.md** (minimal version):
```markdown
# [Project Name]

## Problem
[one sentence]

## User
[who]

## Success Criteria
- [criterion]

## Out of Scope
- [item]
```

**STACK.md** (minimal version):
```markdown
# Stack

- Language: [x]
- Architecture: [pattern]
- Data: [layer]
- Deploy: [target]
```

**TASKS.md** (sprint 1 only):
```markdown
# Tasks

## Sprint 1
- [ ] [first task]
- [ ] [second task]
```

**CONTEXT.md** (generated, not templated):
```markdown
# [Project Name]

[2-3 sentences summarizing the project for a cold-start AI.]
```

---

## After generating files

Say:
> "Quick plan is set. Here's sprint 1: [task list]. Ready to start with [first task]?"

Then hand off to the normal build loop in `CLAUDE.md`.

---

## Common failure modes

- **Skipping out-of-scope** — The one question most people want to skip. Don't.
- **Over-planning inline** — If the interview is going past 15 exchanges, stop and suggest `project-planner`.
- **Generating too many tasks** — Sprint 1 should be 3-7 tasks. More than that is not a sprint.
