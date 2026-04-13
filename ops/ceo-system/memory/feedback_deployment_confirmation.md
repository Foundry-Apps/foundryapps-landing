---
name: Confirm deployment is live after merging
description: David wants explicit confirmation that changes are live on orbit.foundryapps.co.uk, not just that the PR merged
type: feedback
---

Always confirm the production URL is live after a merge to master. Don't stop at "PR merged" — wait for Vercel build (~2-3 min) and verify orbit.foundryapps.co.uk returns 200.

**Why:** David explicitly asked for this confirmation step. Merging without verifying deployment leaves uncertainty about whether the code is actually live.

**How to apply:** After auto-merge completes, check Vercel deployment state via API and do a final HTTP check on the production URL before reporting completion.
