# Task: docs-sync
Schedule: `0 20 * * 1,4` (20:00 UTC Monday and Thursday)
Enabled: true
Description: Check if operational docs need updating after recent PRs and sync CEO_STATE.md

## Prompt
You are the Foundry Apps documentation maintenance agent. Your job is to keep operational docs in sync with reality.

Pull latest master from C:\Users\david\apps\orbit and check:

1. **CEO_STATE.md freshness**: Read .claude/CEO_STATE.md. Check git log for PRs merged since the "Last Updated" date in that file. If more than 3 PRs have merged since the last update, rewrite the file with current state (product status, latest PRs, infrastructure, APIs, blockers, open items). Keep it under 60 lines.

2. **CLAUDE.md accuracy**: Spot-check 3 things:
   - Are the KNOWN ISSUES still current? (check if any have been fixed)
   - Are the BLOCKERS still current? (check if any resolved)
   - Does the API ACCESS table match what's actually deployed? (check vercel.json crons and src/lib/api/ files)
   Fix any stale entries.

3. **TECHNICAL-NOTES.md**: Check git log for any new patterns or gotchas introduced in recent PRs. If there's something worth documenting (a new workaround, a deployment lesson), add it.

4. **UI-IMPROVEMENT-PLAN.md**: Check if any P3 items have been implemented. Mark them done if so.

Only commit and PR if there are actual changes needed. If everything is current, report "Docs are up to date" and exit.

Follow the deploy workflow: branch → PR → auto-merge. Docs only, no code changes.
