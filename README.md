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

> See [project-planner](https://github.com/ContractorKeith/project-planner) for the planning side of the chain.

---

## Getting started

**Option 1 — Use as a GitHub template** (recommended):
Click the **"Use this template"** button on GitHub to create your own copy.

**Option 2 — Clone directly:**
```bash
git clone https://github.com/ContractorKeith/mvp-builder.git my-project
cd my-project
```

---

## Quickstart

**With a planning handoff:**
1. Copy the files from `templates/new-project/` into the root of this repo.
2. Fill them out with your project's details.
3. Open in your AI coding tool.
4. Say `/init`

> **Note:** The `CONTEXT.md` file in the template is a placeholder. You may still want to bring over context from a `project-planner` run.

**Without a handoff:**
1. Open in your AI coding tool.
2. Say `/init` or describe what you want to build.
3. The AI runs a quick inline planning pass, then builds.

---

## What the AI does

1. Reads your plan files.
2. Works through `TASKS.md` sprint 1, one task at a time.
3. After each task: tells you what was built, what to verify, and marks it done.
4. Saves progress to `outputs/SESSION.md` so any session can pick up mid-sprint.

---

## How to use

The core logic is stored in `skills/orchestrator.md`. But you don't need to do anything manually because we provide proxy files out of the box for the most common tools. Each AI tool will read its respective proxy file automatically:

| Tool | Setup |
|---|---|
| Claude Code | Works out of the box — reads `CLAUDE.md` automatically |
| OpenAI Codex | Works out of the box — reads `AGENTS.md` automatically |
| Gemini CLI | Works out of the box — reads `GEMINI.md` automatically |
| Cursor / Windsurf | Works out of the box — governed by `.cursorrules` / `.windsurfrules` |

---

## Structure

```
mvp-builder/
├── .cursorrules              ← IDE instructions for Cursor
├── .windsurfrules            ← IDE instructions for Windsurf
├── CLAUDE.md                 ← proxy to orchestrator
├── GEMINI.md                 ← proxy to orchestrator
├── AGENTS.md                 ← proxy to orchestrator
├── README.md
├── LICENSE
├── CONTRIBUTING.md
│
├── templates/
│   └── new-project/          ← clean handoff files for a new project
│       ├── PRD.md
│       ├── STACK.md
│       ├── TASKS.md
│       └── CONTEXT.md
│
├── skills/
│   ├── orchestrator.md       ← core orchestrator logic
│   ├── skill-creator.md      ← create new skills mid-session
│   ├── task-breakdown.md     ← break large tasks into steps
│   ├── code-reviewer.md      ← review code against PRD + stack
│   ├── progress-tracker.md   ← update SESSION.md + TASKS.md
│   └── inline-planning.md    ← quick plan when no handoff exists
│
├── examples/
│   └── quickquote/           ← sample handoff + session state
│       ├── PRD.md
│       ├── STACK.md
│       ├── TASKS.md
│       ├── CONTEXT.md
│       └── SESSION.md
│
└── outputs/                  ← session state, generated artifacts
    └── SESSION.md            ← written each session, read on init
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
