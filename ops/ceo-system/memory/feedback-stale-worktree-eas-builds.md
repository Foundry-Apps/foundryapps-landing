---
name: EAS builds must run from a worktree synced to master — not from stale feature branches
description: Submitting an EAS build from a feature-branch worktree that pre-dates a merged native-config commit will silently reuse stale native config (app.json, eas.json) — wasting the build credit on a known-bad config
type: feedback
originSessionId: a3a07943-25ea-4687-842b-baa4fad0c808
---
**Rule:** Any EAS build submission must come from a worktree whose `app.json` + `eas.json` match current master (or the intended release branch). For mobile-refresh work specifically, treat each `eas build` as "what version of `app.json` is this submitting?" — not "what branch am I on?"

**Why:** Confirmed 2026-04-20. Spent three EAS builds (`db4b41b6`, `c4461b17`, `9fff5e05`) hitting the exact same `Can't find KSP version for Kotlin version '1.9.25'` Gradle error even after the fix landed on master (commit `25468aea`, PR #384 — bumped `kotlinVersion` to `2.0.21`). Root cause: all three were fired from the `m1-mobile` worktree at commit `0fee5a3e`, which was cut BEFORE the Kotlin fix. The branch never got the fix; `app.json` there still had `"1.9.25"`; EAS read that `app.json`; build died. The one intervening success (`835aa397`) happened because that attempt ran from a commit that included the fix.

**How to apply:**
- Before every `eas build` submission:
  1. Confirm the worktree is in sync with master for all native-config files. `git log -1 origin/master -- apps/mobile/app.json apps/mobile/eas.json apps/mobile/plugins/` — if any of these files have commits on master that your worktree doesn't have, STOP.
  2. Literally `cat apps/mobile/app.json | grep kotlinVersion` (and equivalent key-value gates for whatever native setting is relevant to the current known-good config) before submitting.
- Prefer submitting EAS builds from the main repo at `master` (clean checkout) or a freshly-created worktree cut from current `origin/master`. Never from a long-lived feature-branch worktree unless it's just had `git merge origin/master` run successfully.
- After a native-config-changing PR merges, retire any still-open worktrees that pre-date it. Either rebase them onto master or `git worktree remove` them.
- When Dispatch instructs a code task to submit an EAS build, specify the submission cwd explicitly ("submit from the main repo at `C:\Users\david\apps\orbit`, NOT from any worktree"). Don't assume `apps/mobile/` means the right location — in worktree contexts it doesn't.
- The SessionStart fresh-master hook (PR #378) catches this for NEW sessions. But it doesn't help existing sessions that already have a stale-branch worktree in hand.
