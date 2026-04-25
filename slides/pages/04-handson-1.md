---
layout: section
class: text-center
---

# Hands-on 1

Discovery + Build a skill

[30 min · 0:30 → 1:15]{.text-sm .opacity-60}

<!--
Switch gears: from theory to practice. Two parts back-to-back —
discovery first (poke the harness), then build (a real skill they'll keep).
-->

---

# What we'll do

Two passes, same project:

::div{.parts}

:::div
### A · Discover (15 min)
Inspect the harness · curate `CLAUDE.md` · ship a slash command
:::

:::div
### B · Build (30 min)
Scaffold a skill · iterate until it triggers · harden + demo
:::

::

By the end you'll have:

- A `CLAUDE.md` that **actually shapes** Claude's behavior
- A slash command in `.claude/commands/`
- A working skill in `~/.claude/skills/` that **you'd reach for next week**

<style scoped>
.parts { display: grid; grid-template-columns: repeat(2, 1fr); gap: 1.5rem; margin-top: 1rem; }
.parts > div { border: 1px solid rgb(55, 65, 81); border-radius: 0.5rem; padding: 1rem; }
.parts h3 { color: rgb(251, 146, 60); margin: 0 0 0.5rem 0; }
</style>

---
layout: section
class: text-center
---

# Part A · Discover

`/context` · `/memory` · `CLAUDE.md` · slash commands

[15 min]{.text-sm .opacity-60}

---

# Setup (5 min)

```bash
# Pick any repo you know well (or clone a small one)
cd ~/your-project
claude
```

Inside Claude Code, run:

```
/context
/memory
```

Take a screenshot or note what's loaded by default.

[💡 If `/context` shows a near-empty window, start there. If it's already busy, that's a smell.]{.text-sm .opacity-70}

---

# Step 1 · Memory hierarchy (5 min)

1. Create a project-level `CLAUDE.md` at the repo root.
2. Add 3–5 rules that reflect *real* conventions of the project
   (testing, naming, "don't do X here", etc.).
3. Re-run `/memory` and verify the file is picked up.
4. Ask Claude something that should trigger one of those rules — confirm it follows.

[💡 Keep rules short, specific, and tied to a *why*. Vague rules get ignored.]{.text-sm .opacity-70}

---

# Step 2 · Custom slash command (5 min)

Build a project-scoped slash command in `.claude/commands/`.

Suggested examples:

- `/review-diff` — review the staged diff against the project's style rules
- `/test-touched` — run only tests for files changed since `main`
- `/explain-module <path>` — onboarding-style walkthrough of a module

Test it, iterate on the prompt, commit it.

Run `/context` again — what changed? Compare with a teammate.

[💡 If the command fits a *trigger condition* ("when X, do Y"), it's actually a Skill in disguise — see Part B.]{.text-sm .opacity-70}

---
layout: section
class: text-center
---

# Part B · Build a skill

A skill you'd actually use again next week

[30 min]{.text-sm .opacity-60}

---

# Pick an idea (5 min)

Good skill candidates are:

- **Repetitive** — you do it more than once a week
- **Multi-step** — too much for a single prompt or slash command
- **Opinionated** — there's a "right way" for *your* context

Examples:

- `release-notes` — turn a range of commits into a changelog entry
- `incident-postmortem` — scaffold a postmortem from an incident channel
- `migrate-to-v2` — codemod-ish migration for an internal API
- `code-review-strict` — review with your team's specific style rules

[Park the "too ambitious" ideas. Aim for something demoable in 30 min.]{.text-sm .opacity-70}

---

# Anatomy reminder

```
~/.claude/skills/my-skill/
├── SKILL.md           # name, description, triggers, instructions
├── scripts/           # optional helpers (bash, python, ...)
└── references/        # optional context docs the skill can read
```

Frontmatter that matters:

```yaml
---
name: my-skill
description: When to use this — be specific, this is the trigger
---
```

[The `description` is what Claude reads to decide whether to load the skill. Write it like a trigger condition.]{.text-sm .opacity-70}

---

# Step 1 · Scaffold (5 min)

Use the `skill-creator` skill to bootstrap:

```
> use skill-creator to build a new skill called "release-notes"
```

Or do it by hand:

```bash
mkdir -p ~/.claude/skills/release-notes
$EDITOR ~/.claude/skills/release-notes/SKILL.md
```

Write a **first draft** of `SKILL.md`. Don't polish yet — get something runnable.

---

# Step 2 · Iterate (15 min)

Tight loop:

1. Trigger the skill on a real input
2. Inspect what Claude actually did vs what you wanted
3. Sharpen the `description` (trigger) and the body (instructions)
4. Add helper scripts or reference docs if the skill needs determinism
5. Repeat until it works on **2 different inputs** without hand-holding

[⚠️ A skill that only works on the example you tested is not done.]{.text-sm .opacity-70}

---

# Step 3 · Harden + demo (5 min)

Before calling it done:

- ✅ Description is **specific enough** that Claude won't load it spuriously
- ✅ Skill works on a fresh session (no leftover context from your testing)
- ✅ Any scripts have execute permissions and explicit error messages
- ✅ No secrets, tokens, or company-confidential data in the skill files
- ✅ Committed somewhere (dotfiles repo, team repo, gist…)

Volunteers — quick demo (1 min each, 3–4 demos):

- What does it do? What was the hardest part to get right?

<!--
Security reminder: skills run code. Treat them like any other piece of automation.
-->
