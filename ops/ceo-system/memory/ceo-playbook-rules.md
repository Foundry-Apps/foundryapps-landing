---
name: CEO Playbook operational rules
description: Deployment checklist, repo hygiene, documentation maintenance, new product setup standards, and self-audit cadence
type: reference
---

## New Product Setup Standard
1. Create GitHub repo under Foundry-Apps org — default branch master, .gitignore, README.md, LICENSE (MIT)
2. Connect to Vercel via GitHub integration — never CLI-only
3. Configure domain — Cloudflare CNAME → cname.vercel-dns.com (proxy: false)
4. Set env vars in Vercel (Production + Preview + Development); pull locally with vercel env pull .env.local
5. Copy .github/workflows/auto-merge.yml from orbit
6. Create product CLAUDE.md
7. Verify end-to-end

## Repo Hygiene
- Delete remote branch after every PR merge
- Remove worktree after use
- Max 3 active worktrees
- repo-cleanup runs Sunday 06:00 as safety net

## Documentation Maintenance
Update docs BEFORE reporting task complete when: after every 5th PR merged in a session, after any milestone, after resolving a blocker, after discovering a new gotcha.
Files to check: CEO_STATE.md (under 60 lines), CLAUDE.md, docs/TECHNICAL-NOTES.md, CEO Playbook.

## Deployment Workflow
Branch → commit with Co-Authored-By: Claude → PR → auto-merge → Vercel deploy.
GitHub token: Windows Credential Manager via git credential fill (user: DavidFoundry).
Node.js portable: C:\Users\david\apps\node-portable\node-v20.19.0-win-x64\node.exe

## Self-Audit
Monthly: review agent effectiveness, check for stale scheduled tasks, verify all reports delivering.
Quarterly: full portfolio review, agent architecture audit, cost/revenue trend analysis.
