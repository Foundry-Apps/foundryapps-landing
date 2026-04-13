# Foundry Apps — CEO Bootstrap Guide

How to recreate the CEO operating environment after a machine reset, new install, or Cowork session loss.

---

## Step 1: Set up CLAUDE.md

Copy the contents of `cowork-claude.md` from this directory into your Cowork CLAUDE.md file (`.claude/CLAUDE.md` in the Cowork session, or wherever your Claude Code project-level instructions live).

## Step 2: Set up auto-memory

Copy all files from the `memory/` directory into your Cowork auto-memory directory. The `MEMORY.md` file is the index — it must be present for memories to load at session start.

```bash
cp ops/ceo-system/memory/* /path/to/cowork/.auto-memory/
```

## Step 3: Verify the core setup

Start a new Dispatch session and check:
- The enforced rules appear at the top of context (Research before implementing, Self-review before PR)
- The MEMORY.md index loads with all entries
- Agent definitions are accessible
- Key repos are reachable: orbit and foundryapps-landing

---

## Step 4: Recreate Scheduled Tasks

The following tasks must be recreated in the new Dispatch session using the `create_scheduled_task` tool. Each file in `ops/ceo-system/scheduled-tasks/` contains the exact prompt and config needed.

Active tasks:

| Task ID | Cron | Schedule | Description |
|---|---|---|---|
| `ceo-config-sync` | `0 18 * * 0` | 18:00 UTC Sunday | Sync CEO config from Cowork to git repo |
| `daily-health-check` | `0 7 * * *` | 07:00 UTC daily | Production infrastructure health check |
| `daily-ops-report-v2` | `0 8 * * 1-5` | 08:00 UTC weekdays | Daily ops status report |
| `email-digest` | `0 9 * * *` | 09:00 UTC daily | Gmail scan for important business emails |
| `docs-sync` | `0 20 * * 1,4` | 20:00 UTC Mon + Thu | Sync CEO_STATE.md + check doc freshness |
| `repo-cleanup` | `0 6 * * 0` | 06:00 UTC Sunday | Delete merged branches, clean worktrees |
| `weekly-ceo-brief-v2` | `0 9 * * 1` | 09:00 UTC Monday | Weekly CEO strategic briefing |
| `weekly-infra-review` | `0 9 * * 1` | 09:00 UTC Monday | Weekly infrastructure review |
| `weekly-strategy-report-v2` | `0 9 * * 1` | 09:00 UTC Monday | Strategy and portfolio report |

To recreate each task, open the corresponding file in `ops/ceo-system/scheduled-tasks/` and call `create_scheduled_task` with the `taskId`, `cronExpression`, `description`, and full `prompt` from the file.

Example:
```
create_scheduled_task(
  taskId: "daily-health-check",
  cronExpression: "0 7 * * *",
  description: "Daily health check of Orbit production infrastructure",
  prompt: <contents of ## Prompt section in daily-health-check.md>
)
```

---

## Step 5: Verify Full Recovery

Run through this checklist after completing Steps 1–4:

- [ ] **Enforced rules visible** — Start a session and confirm the Stop hook fires at end of session checking research-before-implementation and self-review-before-PR. Hooks live in `orbit/.claude/settings.json`.
- [ ] **Memories loaded** — MEMORY.md index is present and loads correctly. Check that key memories (enforced-rules, feedback entries, project state) are accessible.
- [ ] **Agent definitions accessible** — Confirm `ops/agents/` in this repo and `orbit/docs/ops-playbook/agents/` are readable. Spot-check orbit-engineering-agent.md and orbit-data-agent.md.
- [ ] **Scheduled tasks running** — List all active tasks and verify each task ID from Step 4 is present with correct cron expression and enabled status.
- [ ] **Repos connected** — Code tasks can reach `C:\Users\david\apps\orbit` (master branch, up to date) and `C:\Users\david\apps\foundryapps-landing` (master branch, up to date).
- [ ] **Hooks active** — `orbit/.claude/settings.json` has PreToolUse hooks for Bash (EAS build gate) and Edit/Write (protected files), plus Stop hooks for research and self-review verification.
- [ ] **Send a test report** — Trigger `daily-health-check` manually and confirm email arrives at david@foundryapps.co.uk.

If any check fails, refer to the relevant file in this directory for the canonical config to restore from.

---

## Quick reference: what goes where

| Config | Location | How to restore |
|---|---|---|
| CEO Operating System CLAUDE.md | `ops/ceo-system/cowork-claude.md` | Copy to `.claude/CLAUDE.md` in Cowork |
| Auto-memory files | `ops/ceo-system/memory/` | Copy to auto-memory dir in Cowork |
| Enforced rules | `ops/ceo-system/enforced-rules.md` | Reference doc; hooks live in orbit settings.json |
| Code hooks (Stop/PreToolUse) | `orbit/.claude/settings.json` | Checked into orbit repo, loads automatically |
| Scheduled task prompts | `ops/ceo-system/scheduled-tasks/` | Use create_scheduled_task to recreate |
| CEO Playbook | `ops/CEO-PLAYBOOK.md` | Checked into this repo, always current |
| Agent definitions | `ops/agents/` | Checked into this repo, always current |

---

## Settings that need manual sync back to this repo

- `.claude/CLAUDE.md` — CEO Operating System (`cowork-claude.md` is the canonical copy here)
- Auto-memory files — `memory/` dir is the canonical copy; Cowork auto-memory is the live version
- The `ceo-config-sync` scheduled task runs weekly to detect drift and create a PR if files have changed
