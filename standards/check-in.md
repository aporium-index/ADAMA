---
type: standard
tags: [check-in, agent-prompt, universal]
timestamp: 2026-06-28
---

# Standard: Universal Check-In Prompt

Copy this entire block into any outpost. The agent will self-orient, audit the repo against sisko standards, update the state file, and report gaps.

```
You are an agent running in this outpost repo. Your job is a sisko check-in.

## Phase 1 — Orient to the Control Plane

Read these files to understand the workspace:
1. `workspace/sisko/AGENTS.md` — control plane overview
2. `workspace/sisko/dashboard.md` — current state of all outposts
3. `workspace/sisko/standards/outpost-state.md` — the state file template
4. `workspace/sisko/standards/agents.md` — agent behavior rules
5. `workspace/sisko/standards/git.md` — git conventions
6. `workspace/sisko/standards/okf.md` — frontmatter convention

## Phase 2 — Familiarize Yourself with This Repo

Explore the repo you are in:
- Read `AGENTS.md` if it exists
- Read any README, docs, or handoff files
- Check `git log --oneline -10` for recent activity
- Check `git status --short` for dirty state
- Identify: primary language, frameworks, build tools, package manager
- Identify: test commands, lint commands, typecheck commands
- Identify: any scripts/ or bin/ directories
- Note: anything unusual or surprising about this repo

## Phase 3 — Audit Against Standards

Compare this repo against sisko requirements. Check each:

| Standard | Requirement | Check |
|----------|-------------|-------|
| AGENTS.md | File exists in repo root | `ls AGENTS.md` |
| .gitignore | Exists, covers `.DS_Store`, `node_modules/`, `.venv/`, `__pycache__/`, `.tmp/` | `cat .gitignore` |
| state file | `<slug>-state.md` exists with valid OKF frontmatter | Read and validate |
| git | On default branch, no stale stashes, recent push | `git branch`, `git log` |
| OKF | Frontmatter in state file has `---` fences with `type: outpost-state` | Parse frontmatter |
| Three actions | State file has exactly 3 next actions | Count `- [ ]` items |

For each missing or non-compliant item, note it — you will write these into the state file body.

Identify any special considerations for this repo:
- Unusual git setup (bare repo, gitdir pointer, iCloud constraints)
- Build tooling that differs from standard
- Dependencies on other outposts
- Files or dirs that should be in .gitignore but aren't
- Dirty working tree that blocks clean commits
- Anything that would surprise a new agent

## Phase 4 — Update the State File

Update these frontmatter fields:
- `last_active`: today's date
- `timestamp`: today's date
- `has_agents_md`: true/false based on audit
- `has_gitignore`: true/false based on audit
- `languages`, `frameworks`, `primary_language`, `primary_framework`: from exploration
- `platform`: from exploration
- `state`, `condition`, `criticality`: do NOT set (sisko sets these)
- `priority`: do NOT set (sisko sets this)

Update these body sections:
- `## Current Focus` — what is actually being worked on, based on git log and dirty files
- `## Next Actions` — exactly 3 items, prioritized. First item should address the biggest gap found in the audit.
- `## Blockers` — anything preventing progress
- `## Compliance Gaps` — NEW section. List every standard that is not met, with a one-line fix.
  ```
  - **AGENTS.md missing** — create with `touch AGENTS.md` and populate
  - **.gitignore missing .venv/** — add `.venv/` to .gitignore
  - **Only 1 next action** — need exactly 3
  ```
- `## Repo Notes` — NEW section. Special considerations, gotchas, surprises.
- `## Template Feedback` — NEW section. Suggestions for improving the state template, standards, or control plane. What was confusing? What's missing? What's overkill?

## Phase 5 — Git Commit + Push

After updating the state file:
```
git add <slug>-state.md
git commit -m "maintenance: sisko check-in — audit, update state, flag gaps"
git push
```

If the audit fixed other files (added .gitignore, created AGENTS.md), commit those too.

## Phase 6 — Report

Return a concise summary:

```
## Check-in: <outpost name>

### Gaps Found
- item 1
- item 2

### Fixed
- item 1

### State Updated
- Current focus: <one line>
- Next actions: 3 items

### Template Feedback
- suggestion 1
```
```
