---
layout: section
class: text-center
---

# Hands-on 2

Build a subagent · Package it as a plugin

[45 min · 1:45 → 2:30]{.text-sm .opacity-60}

<!--
This is the "ship it for the team" round. Everyone walks out with something a teammate could
install with one command.
-->

---

# Goals

By the end you'll have:

- A **custom subagent** in `.claude/agents/` that does one thing well
- A **plugin** that bundles it (plus your skill / command from Hands-on 1)
- Tested locally with `--plugin-dir`
- Pushed to a Git repo so a teammate could install it

<!--
Quality bar: a teammate could clone the plugin repo, install it, and use the subagent
without asking you a single question.
-->

---

# Pick a subagent idea (5 min)

Good subagent candidates:

- **Floods context** — search-heavy, log-diving, audit work
- **Specialist** — one persona, repeatable system prompt
- **Restricted tools** — read-only review, no write access
- **Run-in-parallel** — N independent investigations

Examples:

- `pr-reviewer` — read-only review of `git diff` against team rules
- `dep-auditor` — scan deps for CVEs, return punch-list
- `test-writer` — generate tests for a target module
- `log-detective` — investigate a stack trace across services
- `migration-checker` — verify a migration is safe under load

[Park ambition. 30 min of build time means *one* clear job.]{.text-sm .opacity-70}

---

# Step 1 · Build the subagent (15 min)

Use `/agents` to scaffold interactively, or by hand:

```bash
mkdir -p .claude/agents
$EDITOR .claude/agents/pr-reviewer.md
```

```yaml
---
name: pr-reviewer
description: |
  Reviews staged diffs for bugs, missing tests, and style issues.
  Use PROACTIVELY when the user asks for a review or before commits.
tools: Read, Grep, Glob, Bash
model: sonnet
---

You are a senior reviewer for this team. When invoked:
1. Run `git diff --staged` and `git status`.
2. Group findings as Bugs / Tests / Style / Nits.
3. Cite file:line for every finding.
4. End with a one-line verdict: ship / fix-then-ship / block.
```

Test it: `> use pr-reviewer to review my staged changes`. Iterate.

---

# Step 2 · Package as a plugin (15 min)

Promote `~/.claude/skills/<your-skill>/` and `.claude/agents/<your-subagent>.md` into a plugin repo:

```
my-team-plugin/
├── .claude-plugin/
│   └── plugin.json              ← {name, version, description}
├── agents/
│   └── pr-reviewer.md           ← (moved from .claude/agents/)
├── skills/
│   └── release-notes/SKILL.md   ← (moved from ~/.claude/skills/)
├── commands/
│   └── review-diff.md           ← (optional, from Hands-on 1)
└── README.md                    ← how to install + what it does
```

```json
// .claude-plugin/plugin.json
{ "name": "my-team-plugin", "version": "0.1.0",
  "description": "Team review + release-notes workflow" }
```

---

# Step 3 · Test locally (5 min)

Load your plugin without publishing:

```bash
claude --plugin-dir ./my-team-plugin
```

Inside the session:

- `/agents` — does `pr-reviewer` show up?
- Trigger your skill on a real input — does it load?
- Make a small change to a file → `/reload-plugins` → see it pick up

[💡 If something doesn't load, check `/context` and the plugin path — most issues are typos in `plugin.json` or wrong directory placement.]{.text-sm .opacity-70}

---

# Step 4 · Ship + demo (5 min)

Final checks:

- ✅ `README.md` says **what it does** and **how to install**
- ✅ No secrets in any file (audit `.mcp.json`, hooks, agent prompts)
- ✅ `tools:` list is **least-privilege** (does `pr-reviewer` really need `Write`?)
- ✅ Pushed to Git (team repo, personal GitHub, gist...)

```bash
git init && git add . && git commit -m "feat: pr-reviewer plugin"
git remote add origin <your-repo> && git push -u origin main
```

Volunteers — 1-min demos:

- What does the subagent do? Why a subagent vs a skill?

<!--
The "why a subagent vs a skill" question is the actual learning moment of the workshop.
Most ideas can be either — the answer reveals whether they internalized the trade-offs.
-->
