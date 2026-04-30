---
name: Success = merged AND deployed to production, not PR opened
description: Tasks are only complete when the change is live in production. PR opened ≠ done. PR merged ≠ done. Production-deployed = done.
type: feedback
originSessionId: a3a07943-25ea-4687-842b-baa4fad0c808
---
**Rule:** A task is only successful when its change is live in production. Not when a PR is opened. Not when a PR is merged. When it's deployed and running.

**Why:** Confirmed 19 April 2026 by David. Dispatch was reporting PRs as "landed" when they were only opened with auto-merge expected to squash later. David rightly pointed out: if it doesn't make it to production, the task didn't succeed — it just moved a step closer. An open PR that sits for hours due to a CI flake, reviewer-bot block, or merge conflict is a failure if nobody catches it.

**How to apply:**

- When reporting task completion, verify BOTH:
  1. PR is merged (not just open with auto-merge set). Use the GitHub API: `state === "closed" && merged === true`.
  2. The merge has been deployed to production. For Orbit: Vercel deploy for the main branch's new HEAD succeeded — check Vercel API or deploy status.
- Until both are true, the task state is "in-flight", not "done". Surface this clearly in status messages.
- For each open PR expected to auto-merge: set an active monitoring step. If the PR is still open 15 minutes after CI passed, investigate — don't assume auto-merge will get there eventually.
- When there's a deploy gap (merge happened but deploy pending), say so explicitly: "merged, awaiting Vercel deploy" is different from "merged" is different from "shipped".
- Don't preempt the language — avoid "done", "shipped", "landed" until the production deployment is confirmed green.
- If a PR is blocked (CI fail, reviewer bot, conflict), that is active information David needs — surface it fast, not after he notices.

**Completion checklist for future PR tasks:**
1. PR opened ✓
2. CI green ✓
3. Merged to main ✓
4. Production deploy succeeded ✓
5. Quick smoke (page loads, no obvious regression) ✓
6. → now "shipped"
