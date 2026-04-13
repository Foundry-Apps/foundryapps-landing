---
name: Auto-merge CI gate
description: Auto-merge workflow updated to wait for CI checks before merging PRs — prevents silent CI failures landing on master
type: project
---

Auto-merge workflow (.github/workflows/auto-merge.yml) now waits for CI checks to pass before merging (polls up to 5 min). No review approval gate — the PR reviewer comments but doesn't approve/merge, so gating on approval would block everything.

**Why:** In April 2026, CI was broken for 20+ consecutive PRs because the auto-merge workflow didn't gate on CI status. Tests and typecheck were failing but PRs kept merging.

**How to apply:** All future Claude CEO PRs will be held until CI passes (up to 5 min). If CI fails, auto-merge fails and the PR stays open. Reviewer comments are informational for David to scan — they don't block merge.
