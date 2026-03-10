---
name: skill-creator
description: Create a new skill file and add it to /skills/. Use this whenever the user or orchestrator identifies a capability gap mid-build — something that would be useful now and in future sessions. Trigger when someone says "we need a skill for X", "can you learn how to do Y", or when a repeated workflow pattern emerges that isn't covered by an existing skill.
---

# Skill Creator

## Purpose
Capture a reusable build capability as a skill file in `/skills/` so it's available
for this session and every future one. Skills are how this repo gets smarter over time.

---

## When to create a skill

Create a new skill when:
- A workflow step is repeated more than twice in a session
- The orchestrator or user identifies a gap in current capabilities
- A domain-specific pattern emerges (e.g., "how to scaffold this framework's modules")
- The user explicitly asks for one

Don't create a skill for a one-off task. Skills are for recurring patterns.

---

## How to create a skill

### Step 1 — Capture intent
Ask (or infer from context):
1. What should this skill enable the AI to do?
2. When should it trigger?
3. What does a good output look like?

Extract answers from the current session before asking. If the session already
demonstrates the capability, use that as your reference.

### Step 2 — Write the skill file

```markdown
---
name: skill-name-kebab-case
description: [What it does + when to trigger. Be specific. Include the exact
             phrases or situations that should activate it. Be a little pushy —
             err toward over-specifying the trigger conditions.]
---

# Skill Title

## Purpose
[One sentence. What problem does this solve?]

---

## [Main content]
[Instructions, patterns, decision logic, examples]

---

## Output format
[What should the AI produce when this skill runs?]

---

## Common failure modes
[Easy ways to get this wrong — and how to avoid them]
```

**Key rules:**
- The `description` frontmatter is the trigger. Vague = won't fire.
- Keep body under 300 lines
- Use imperative instructions
- Always include a failure modes section

### Step 3 — Save and confirm

Save to `/skills/[name].md`.

Tell the user:
> "Created `skills/[name].md`. Available for the rest of this session and future ones."

---

## Quality check before saving

- [ ] Description is specific enough to trigger correctly
- [ ] Single, clear purpose
- [ ] Imperative instructions throughout
- [ ] Doesn't substantially overlap an existing skill
- [ ] Will be useful in future sessions
