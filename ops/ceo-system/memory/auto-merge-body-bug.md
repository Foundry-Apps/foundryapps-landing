---
name: Auto-merge workflow body injection bug
description: PR bodies with backticks/special chars break the GitHub Actions auto-merge workflow shell script
type: feedback
---

PR bodies containing backticks, single quotes, or other shell-special characters break the auto-merge workflow. The line `PR_BODY="${{ github.event.pull_request.body }}"` in `.github/workflows/auto-merge.yml` interpolates directly into bash, so markdown code fences in the body cause the "Find PR and check if Claude CEO" step to fail.

**Why:** Discovered when PR #263's body contained backtick-wrapped code references, causing the auto-merge step to fail immediately.

**How to apply:** Either keep PR bodies as plain text (no backticks/code fences), or merge manually via GitHub API (`PUT /repos/Foundry-Apps/orbit/pulls/{number}/merge`) as a fallback. The workflow should be fixed long-term to use environment variables instead of direct interpolation.
