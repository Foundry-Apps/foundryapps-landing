---
name: Always verify PR merge status via GitHub API
description: Never assume a PR merged — always check GitHub API with authenticated request to confirm open/merged/closed state
type: feedback
---

Always verify PR merge status directly via the GitHub API — never infer from Vercel deployments or assume.

**Why:** PR #283 was closed without merging but I told David it was merged based on Vercel deployment data. David had to correct me. He stressed he won't always be watching PRs — I need to detect this independently.

**How to apply:**
- Route all GitHub API checks through code tasks on the host (which can use `git credential fill` for auth)
- After creating any PR, check its actual state (open/merged/closed) before reporting to David
- Never use Vercel deployment data as a proxy for GitHub PR status
- The `state` and `merged` fields from `GET /repos/{owner}/{repo}/pulls/{number}` are the only reliable source
- Long-term: set up a GITHUB_TOKEN env var on the host so all task types can authenticate
