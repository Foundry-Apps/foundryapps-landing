---
name: Conflict resolution is always per-file inspection, never batch rules
description: When resolving merge conflicts across multiple files, never apply a blanket "take ours" or "take theirs" rule — inspect each file individually because each may represent different intent
type: feedback
originSessionId: a3a07943-25ea-4687-842b-baa4fad0c808
---
**Rule:** When resolving merge conflicts across N files, do N independent decisions — not one rule applied N times. Each conflicted file may represent different intent (UI drift, substantive new work, stale import, etc.), and batching the resolution destroys content.

**Why:** 2026-04-19 — Dispatch told the code task "for any UI file conflict, take master's version; for non-UI, inspect." The session applied this correctly for most files, but `packages/types/src/index.ts` conflict was batched with the UI resolution and lost 5 lines that were the **actual substantive work** of PR #372 (adding `inhold`, `holdreason` to `Launch`/`LL2Launch`, `slug` to `Astronaut`). Result: master CI went red with 14 typecheck errors across 7 files, and every subsequent PR's auto-merge was silently blocked until someone opened a PR that couldn't sneak past the CI race.

The damage compounded because:
1. Auto-merge fires on "Co-Authored-By: Claude" in ~30s.
2. Web CI (typecheck/build/tests) takes 1–2 min.
3. Four PRs were already merged before their CI could report the failure.
4. PR #382 (mobile) was the first to block, because its slower CI sequence surfaced the issue.

**How to apply:**
- When giving a code task conflict-resolution instructions, enumerate each file and its resolution rule. Never say "all non-UI files → X".
- The code task should `git diff` each side of each conflict and think about which side is CORRECT for THAT file's intent, not which side is correct for the PR as a whole.
- For "hygiene"-style PRs that touch shared packages (types, config, utils), those shared files are almost always the REAL work — take the PR's version unless there's evidence master has a critical fix.
- After any merge+push+auto-merge flow, DO NOT rely on "auto-merge fired" as confirmation. Wait for CI to report green explicitly. If CI reports red after auto-merge, it's still a broken master — treat as a P0 incident.
