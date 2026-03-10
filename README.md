# mvp-builder

A build-mode repo. Drop in a planning handoff and start shipping.

Open it in Claude Code, Codex, or Gemini CLI. Drop your `project-planner/outputs/`
files into the root. Say `/init`. The AI reads the plan and starts building.

---

## The chain

```
project-planner  →  outputs/  →  mvp-builder  →  ship
```

`project-planner` produces the plan. `mvp-builder` executes it.
Each repo has one job.

> See [project-planner](https://github.com/ContractorKeith/project-planner) _(coming soon)_ for the planning side of the chain.

---

## Quickstart

**With a planning handoff:**
1. Copy `PRD.md`, `STACK.md`, `TASKS.md`, `CONTEXT.md` from `project-planner/outputs/` into this repo root
2. Open in your AI coding tool
3. Say `/init`

> **Note:** project-planner names the context file based on your tool (`CLAUDE.md`, `AGENTS.md`, etc.).
> Rename it to `CONTEXT.md` before dropping it in — this avoids overwriting the orchestrator.

**Without a handoff:**
1. Open in your AI coding tool
2. Say `/init` or describe what you want to build
3. The AI runs a quick inline planning pass, then builds

---

## What the AI does

1. Reads your plan files
2. Works through `TASKS.md` sprint 1, one task at a time
3. After each task: tells you what was built, what to verify, marks it done
4. Saves progress to `outputs/SESSION.md` so any session can pick up mid-sprint

---

## How to use

The orchestrator file is `CLAUDE.md`. Each AI tool reads it automatically:

| Tool | Setup |
|---|---|
| Claude Code | Works out of the box — reads `CLAUDE.md` automatically |
| OpenAI Codex | Copy or rename `CLAUDE.md` to `AGENTS.md` |
| Gemini CLI | Copy or rename `CLAUDE.md` to `GEMINI.md` |

---

## Structure

```
mvp-builder/
├── CLAUDE.md              ← orchestrator
├── README.md
├── LICENSE
├── CONTRIBUTING.md
│
├── skills/
│   ├── skill-creator.md   ← create new skills mid-session
│   ├── task-breakdown.md  ← break large tasks into steps
│   ├── code-reviewer.md   ← review code against PRD + stack
│   ├── progress-tracker.md← update SESSION.md + TASKS.md
│   └── inline-planning.md ← quick plan when no handoff exists
│
├── examples/
│   └── quickquote/        ← sample handoff + session state
│       ├── PRD.md
│       ├── STACK.md
│       ├── TASKS.md
│       ├── CONTEXT.md
│       └── SESSION.md
│
└── outputs/               ← session state, generated artifacts
    └── SESSION.md         ← written each session, read on init
```

---

## Example outputs

The `examples/quickquote/` folder contains a sample handoff and mid-sprint session state
for a fictional quoting app. Browse it to see what a working build session looks like.

---

## Growing the skill set

If the AI needs a capability not covered by existing skills, ask it to create one:
> "Create a skill for [X]"

It uses `skills/skill-creator.md` and the new skill lands in `/skills/` immediately.

---

## License

MIT
