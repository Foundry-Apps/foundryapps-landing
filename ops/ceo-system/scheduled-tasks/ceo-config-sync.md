---
taskId: ceo-config-sync
cronExpression: "0 18 * * 0"
schedule: 18:00 UTC Sunday (weekly)
enabled: true
description: Sync CEO Operating System files (CLAUDE.md, enforced rules, memory files) from Cowork to the foundryapps-landing git repo
---

## Prompt

Sync the CEO Operating System configuration from Cowork's local storage to the foundryapps-landing git repository. This ensures all settings are version-controlled and recoverable from any machine.

Steps:

1. Read all files from the Cowork auto-memory directory. These are the current working memory files that define the CEO agent.

2. Access the foundryapps-landing repo at C:\Users\david\apps\foundryapps-landing using a code task.

3. Compare the Cowork memory files against ops/ceo-system/memory/ in the repo. For each file:
   - If the Cowork version is newer or different, update the repo copy
   - If a new memory file exists in Cowork that isn't in the repo, add it
   - If a memory file was deleted from Cowork, note it but don't delete from repo (flag for review)

4. Compare the Cowork CLAUDE.md (.claude/CLAUDE.md) against ops/ceo-system/cowork-claude.md in the repo. Update if different.

5. Compare the enforced-rules.md against ops/ceo-system/enforced-rules.md. Update if different.

6. If ANY files changed, create a PR on the foundryapps-landing repo with the updates. PR title: "chore: sync CEO config [DATE]". Plain text body listing what changed.

7. If nothing changed, report "CEO config in sync, no updates needed" and exit.

8. Send a summary to david@foundryapps.co.uk via Gmail draft if there were changes, noting which files were updated.

Success criteria: All CEO Operating System files in the git repo match the current Cowork session state. Changes are tracked via git history.
