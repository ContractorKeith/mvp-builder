---
name: progress-tracker
description: Update TASKS.md and outputs/SESSION.md to reflect current build state. Use this skill after completing any task, at the end of every session, or when the user asks "where are we?" or "what's left?". Trigger any time session state needs to be written or read.
---

# Progress Tracker

## Purpose
Keep TASKS.md and SESSION.md accurate so any AI tool — or the user — can pick
up exactly where things left off. The session state is the memory between sessions.

---

## Two files to maintain

### TASKS.md
The sprint board. Update it as tasks are completed.

- Mark done: `- [ ]` → `- [x]`
- Add new tasks to backlog if scope was added and approved
- Move completed items to the `## Done` section at end of sprint

### outputs/SESSION.md
The state file. Written at the end of every session, read at the start of the next.

---

## SESSION.md format

```markdown
# Session State

**Project:** [name from PRD]  
**Last updated:** [date]  
**Tool used:** [Claude Code / Codex / Gemini CLI]

---

## Status

- **Sprint 1 progress:** [X of N tasks complete]
- **Currently working on:** [task name or "—"]
- **Blocked on:** [blocker or "nothing"]

## Completed This Session

- [task name] — [one line on what was built]
- [task name] — [one line on what was built]

## Next Up

- [next task from TASKS.md]
- [task after that]

## Notes

[Anything the next session needs to know. Decisions made. Gotchas found. Config that matters.]
```

---

## When to update

| Trigger | Action |
|---|---|
| Task completed | Mark `[x]` in TASKS.md, add to SESSION.md completed list |
| Session ending | Full SESSION.md write — status, completed, next up, notes |
| User asks "where are we?" | Read SESSION.md and TASKS.md, summarize in 3-5 sentences |
| New task added | Add to TASKS.md backlog, note in SESSION.md |
| Blocker found | Note in SESSION.md "Blocked on:" field |

---

## End-of-session routine

Before closing:
1. Mark all completed tasks in TASKS.md
2. Write SESSION.md with full current state
3. Say: **"Session state saved to `outputs/SESSION.md`. Next session will pick up with: [next task]."**

---

## Start-of-session routine

At `/init` or session open:
1. Read SESSION.md if it exists
2. Read TASKS.md
3. Report: **"Last session: [date]. [X of N] tasks done. Picking up with: [next task]."**
