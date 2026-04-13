---
name: Repo uses pnpm + Turborepo (not yarn)
description: Orbit monorepo migrated to pnpm 9.15.9 + Turborepo, not yarn as CLAUDE.md suggests
type: project
---

The Orbit repo completed a pnpm + Turborepo migration (April 2026). The root `package.json` has `"packageManager": "pnpm@9.15.9"` and uses `pnpm-workspace.yaml` + `pnpm-lock.yaml`. CI workflows correctly use pnpm.

**Why:** CLAUDE.md contains stale references to a yarn classic migration. The actual migration went to pnpm + Turborepo instead. Multiple task sessions ("pnpm Turborepo migration", "pnpm migration Phase 1") confirm this.

**How to apply:** Use `pnpm` commands, not `yarn`. The CLAUDE.md LESSONS LEARNED section about yarn workspaces is historical context only — the current state is pnpm. CI uses `pnpm/action-setup@v4` with version 9.15.9.
