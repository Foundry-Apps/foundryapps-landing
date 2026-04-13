# Foundry Apps — CEO Bootstrap Guide

## How to recreate the CEO Dispatch environment

When starting Claude Dispatch (Cowork) on a new machine or after a reset:

### Step 1: Set up CLAUDE.md
Copy the contents of `cowork-claude.md` from this directory into your Cowork CLAUDE.md file (`.claude/CLAUDE.md` in the Cowork session, or wherever your Claude Code project-level instructions live).

### Step 2: Set up auto-memory
Copy all files from the `memory/` directory into `.auto-memory/` in your Cowork session. The `MEMORY.md` file is the index — it must be present for memories to load at session start.

```bash
cp ops/ceo-system/memory/* /path/to/cowork/.auto-memory/
```

### Step 3: Verify the setup
Start a new Dispatch session and check:
- The enforced rules appear at the top of context (Research before implementing, Self-review before PR)
- The MEMORY.md index loads with all entries
- Agent definitions are accessible
- Key repos are reachable: orbit + foundryapps-landing

### Step 4: Recreate Scheduled Tasks

The following scheduled tasks must be configured in the new Dispatch session. Each file in `ops/ceo-system/scheduled-tasks/` contains the full prompt needed to recreate it using the `create_scheduled_task` tool.

Active tasks:

| Task ID | Schedule | Description |
|---|---|---|
| `ceo-config-sync` | `0 2 * * *` (02:00 UTC daily) | Sync CEO config from Cowork to git repo |
| `daily-health-check` | `0 7 * * *` (07:00 UTC daily) | Production infrastructure health check |
| `daily-ops-report-v2` | `0 8 * * 1-5` (08:00 UTC weekdays) | Daily ops status report |
| `email-digest` | `0 9 * * *` (09:00 UTC daily) | Gmail scan for important business emails |
| `docs-sync` | `0 20 * * 1,4` (20:00 UTC Mon + Thu) | Sync CEO_STATE.md + check doc freshness |
| `repo-cleanup` | `0 6 * * 0` (06:00 UTC Sunday) | Delete merged branches, clean worktrees |
| `weekly-ceo-brief-v2` | `0 9 * * 1` (09:00 UTC Monday) | Weekly CEO strategic briefing |
| `weekly-infra-review` | `0 9 * * 1` (09:00 UTC Monday) | Infrastructure review |
| `weekly-strategy-report-v2` | `0 9 * * 1` (09:00 UTC Monday) | Strategy and portfolio report |

To recreate: open each file in `ops/ceo-system/scheduled-tasks/` and use the `create_scheduled_task` tool with the `taskId`, `cronExpression`, `description`, and `prompt` from the file.

### Step 5: Connect repos
Ensure code tasks can access:
- `C:\Users\david\apps\orbit` — Orbit product repo
- `C:\Users\david\apps\foundryapps-landing` — Business ops repo

### Settings that live in repos (auto-sync via git):
- **Orbit CLAUDE.md** — coding standards, mobile debugging protocol, PR checklist
- **`orbit/.claude/settings.json`** — Claude Code hooks (pre-build gate, protected files, research + review enforcement via Stop hooks)
- **CEO Playbook** — `ops/CEO-PLAYBOOK.md` (this repo)
- **Agent definitions** — `ops/agents/` (this repo) + `orbit/docs/ops-playbook/agents/`
- **CEO state** — `docs/ceo-state.md` (this repo, master branch)

### Settings that live in Cowork (need manual sync back to this directory):
- `.claude/CLAUDE.md` — CEO Operating System (`cowork-claude.md` is the canonical copy)
- `.auto-memory/*` — all operational memories, feedback, project state (`memory/` is the canonical copy)

### Daily sync task
A scheduled task should run daily to compare Cowork memory files against the repo copies. If memory files are newer, the task updates the repo and creates a PR. This ensures continuity across machine resets.

### Enforced rules
The Stop hooks in `orbit/.claude/settings.json` enforce:
1. **Research before implementing** — web search must happen before any code change
2. **Self-review before PR** — `git diff master...HEAD` must run before `git push`

These are deterministic: the hook blocks session completion if violated. The full rule set (including Tier 2 rules) is in `enforced-rules.md`.

---

## Quick reference: what goes where

| Config | Location | How to restore |
|---|---|---|
| CEO Operating System CLAUDE.md | `ops/ceo-system/cowork-claude.md` | Copy to `.claude/CLAUDE.md` in Cowork |
| Auto-memory files | `ops/ceo-system/memory/` | Copy to `.auto-memory/` in Cowork |
| Enforced rules | `ops/ceo-system/enforced-rules.md` | Reference doc; hooks live in orbit settings.json |
| Code hooks (Stop/PreToolUse) | `orbit/.claude/settings.json` | Checked into orbit repo, loads automatically |
| CEO Playbook | `ops/CEO-PLAYBOOK.md` | Checked into this repo, always current |
| Agent definitions | `ops/agents/` | Checked into this repo |
| Orbit coding standards | `orbit/CLAUDE.md` | Checked into orbit repo |
| CEO state | `docs/ceo-state.md` | Checked into this repo |
