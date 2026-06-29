---
slug: ADAMA
name: ADAMA
category: control-plane
domain: meta
description: >
  Control plane for the workspace. Single source of truth for outpost
  status, priorities, standards, and cross-outpost coordination.
location: workspace/ADAMA/
primary_language: markdown
languages: []
primary_framework: none
frameworks: []
platform: cross-platform
repo_url: https://github.com/aporium-index/ADAMA
repo_type: github
default_branch: master
sensitivity: internal
has_agents_md: true
has_gitignore: true
phase: outpost
status: null
condition: condition-green
priority: P1
criticality: tier-0
owner: josh
owner_type: human
last_active: 2026-06-28
last_checkin: 2026-06-28
timestamp: 2026-06-28
stale_threshold_days: 7
depends_on: []
depended_on_by: [_aporium, basicly, jamboree, quotaz, prosodymaker, mac-optimization-audit, ml-feedback-program]
tags: [control-plane, meta, markdown]
file_version: "1.1"
---

# ADAMA

## Current Focus

Phase model overhaul: replacing starship states with honest brief→survey→outpost pipeline. Migrating description/location to YAML. State files restructured.

## Full Backlog

- [ ] Phase model rollout across all 8 outpost state files
- [ ] Dashboard and index.html updated for phase-based rendering
- [ ] Init prompt aligned with new template
- [ ] AGENTS.md rollout for jamboree and quotaz
- [ ] Dashboard as persistent background service (launchd)

## Blockers

None.

## Compliance Gaps

- **No versioned release process** — standards change often; need CHANGELOG or version bump automation
- **Dashboard requires manual server start** — should be a background service

## Long-Term Direction

Phase 1: Stable state model, consistent outpost files, reliable dashboard.
Phase 2: Self-updating dashboard (watch filesystem, push updates).
Phase 3: Cross-outpost dependency tracking and automated check-in scheduling.

Threshold: when all outposts reach `outpost` phase with condition-green, ADAMA's criticality can drop from tier-0 to tier-1 (infrastructure is stable).

## Open Decisions

- Dashboard as launchd service or stay manual?
- Should ADAMA track opencode configuration as a dependency?

## Decisions

| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-06-28 | sisko → ADAMA | sisko looked like "sicko" |
| 2026-06-28 | Phase model: brief → survey → outpost | Starship metaphors were dishonest — no outpost was operational |
| 2026-06-28 | Description/location moved to YAML | Single-value fields don't belong in narrative body |
| 2026-06-28 | projects/ → outposts/ | Distinct term, no collision with generic project vocabulary |
| 2026-06-28 | Symlinks in outposts/ | Zero duplication. Outpost owns state file. ADAMA points to it. |

## Repo Notes

ADAMA is tier-0 infrastructure. If ADAMA is down, agents lose their bearings.
Keep it minimal: no databases, no APIs, no build steps.
The Serve Dashboard.command runs a local HTTP server — Python 3 required.

## Links

- AGENTS.md
- dashboard.md
- index.html
- standards/
