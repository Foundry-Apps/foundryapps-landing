---
name: GitHub Actions org write permissions required for auto-merge
description: Foundry-Apps org must have write workflow permissions enabled or auto-merge fails with 0 jobs
type: feedback
---

If GitHub Actions runs fail with 0 jobs, check org-level workflow permissions first: github.com/organizations/Foundry-Apps/settings/actions → "Workflow permissions" must be "Read and write permissions".

**Why:** In March 2026, the org was locked to read-only workflow permissions, blocking GITHUB_TOKEN from getting contents:write and pull-requests:write. Every run failed with 0 jobs and no error message in the job logs (because no jobs ran). The YAML syntax error (unindented Co-Authored-By line breaking the literal block) was the secondary cause.

**How to apply:** Two things needed for auto-merge to work: (1) org write permissions enabled, (2) workflow YAML must not have unindented content inside run: | blocks. Check both if auto-merge stops working.
