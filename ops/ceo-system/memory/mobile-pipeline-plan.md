---
name: Mobile pipeline self-sufficiency plan
description: Plan to automate EAS builds via GitHub Actions CI, eliminate manual terminal work for David
type: project
---

Mobile app blank screen debugging has taken 2+ days with 15+ builds and excessive manual work by David. He's frustrated and rightly so.

**Why:** David should never run terminal commands, submit builds, or check logcat. That's CEO (Claude) operational work.

**How to apply:**
1. Create `.github/workflows/mobile-ci.yml` — triggers on push to master, runs preflight, submits EAS build, tracks result
2. Store EXPO_TOKEN in GitHub repo secrets (David needs to do this one-time)
3. Script to clean up 80+ stale worktrees causing session timeouts
4. Build history tracker (`.claude/build-history.json`) for querying without Expo dashboard
5. Never ask David to run terminal commands for operational tasks
