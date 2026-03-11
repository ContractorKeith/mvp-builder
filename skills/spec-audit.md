---
name: spec-audit
description: After a build completes, have a second model (or fresh session) audit what was built against the PRD. Produces a structured PASS/FAIL/PARTIAL verdict with evidence for every requirement. Use before marking any sprint done.
---

# Spec Audit

## Purpose
The builder built it. The builder thinks it's done. The builder is the wrong one
to verify that — the same reasoning that produced the implementation will rationalize
away its own gaps.

A spec audit sends the PRD and build artifacts to a model with no execution history
and asks it to check whether what was built matches what was asked for. Not "does
it look right" — requirement by requirement, with evidence.

---

## When to use

After completing a build sprint and before telling the user it's done.
A sprint isn't done until it passes audit.

---

## How to do it

### Step 1 — Collect audit inputs

Gather these before running the audit:

| Input | What it is |
|---|---|
| **PRD.md** | The original requirements. Use the version the builder worked from. |
| **Completion summary** | What the builder says they built. Bullet list is fine. |
| **Artifacts** | Evidence the build works. See requirements below. |

**Minimum artifacts by task type:**
- Backend / API: diff or key files + a real API response showing the feature works
- Frontend / UI: diff or key files + screenshot of the working UI
- Full-stack: both
- Config or infra: command output showing the change applied

Don't let the builder choose what to show. Require the above.

### Step 2 — Run the audit

Use a different model than the one that built it. If that's not possible, use a
fresh session with no prior context from the build.

Prompt:

```
You are a spec auditor. Your job is to determine whether what was built matches
what was asked for. You have no knowledge of how this was built or what decisions
were made. You see only:

1. THE SPEC — what was asked for
2. THE COMPLETION SUMMARY — what the builder claims they built
3. THE ARTIFACTS — evidence of what was actually built

## Your process

Extract every requirement from the spec. Number them. For each:
- Find concrete evidence in the artifacts
- If a required item has no evidence, mark it MISSING — not "unverifiable"
- Note anywhere the implementation differs from what was specified

## Output format

Produce this exact structure:

# Spec-Audit Report
**Verdict:** PASS / PARTIAL / FAIL
**Coverage:** N/M requirements met

## Requirements
| # | Requirement | Priority | Status | Evidence |
|---|---|---|---|---|
| R1 | [what spec asked for] | MUST | ✅ Met | [proof] |
| R2 | [what spec asked for] | MUST | ❌ Missing | [what's absent] |

## Divergences
[Where implementation differs from spec]

## What to fix
[Specific list, or SHIP if passing]

## Verdict rules
- PASS: all required items have evidence, no blocking differences
- FAIL: any required item lacks evidence, or a fundamental difference exists
- PARTIAL: all required items met, but optional items are missing

[PRD]
[contents of PRD.md]

[COMPLETION SUMMARY]
[builder's completion notes]

[ARTIFACTS]
[paste or describe the artifacts]
```

### Step 3 — Act on the verdict

**PASS** — Mark the sprint done. Ship it.

**PARTIAL** — All required items are met but optional ones are missing.
Decide: ship with documented gaps, or remediate. Tell the user what's missing
either way.

**FAIL** — Do not ship. Write a narrow remediation task covering only the failing
items. Fix, then run the audit again.

If the same required item fails twice — stop. Escalate to the user with options.
Don't silently retry.

---

## Common failure modes

- **Auditing with the same session** — The whole point is fresh eyes. Same context
  = rationalization, not audit.
- **Accepting claims as evidence** — "I implemented X" is not evidence. A working
  API response, a screenshot, a diff — those are evidence.
- **PARTIAL on a required item** — That's a FAIL. Partial coverage of a hard
  requirement means the requirement isn't met.
- **Skipping because the build feels solid** — The builder always thinks it's solid.
  That's not the same as it being solid.
