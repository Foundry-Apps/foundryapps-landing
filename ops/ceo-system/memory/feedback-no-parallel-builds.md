---
name: No parallel EAS builds or duplicate tasks
description: Never submit multiple EAS builds or spawn duplicate code tasks for the same work — timeout retries queue up silently
type: feedback
---

Never spawn duplicate code tasks when start_code_task times out. The timeout does NOT mean the task failed — it often queued and started anyway. On 7 April 2026, four "clean EAS build" tasks all ran in parallel, each submitting builds independently, wasting EAS build credits and creating confusion.

**Why:** David was frustrated by 7+ failed builds from the same commit, all submitted within minutes. EAS builds cost money and time. The host machine also became overloaded with 100+ idle sessions, causing further timeouts.

**How to apply:**
- If `start_code_task` times out, check `list_sessions` before retrying — the task may already be running.
- For EAS builds specifically: one build at a time, batch PRs first, verify locally, then one cloud build.
- **MANDATORY pre-build check**: Before any `eas build` command, run `eas build:list --limit 3 --json` and abort if any build from the same commit is IN_PROGRESS or FINISHED within the last 30 minutes.
- When multiple tasks are in flight, coordinate — only one triggers the build.
- Keep task count low. Reuse existing sessions via `send_message` instead of spawning new ones.
- **9 Apr 2026 repeat incident**: 2 duplicate builds triggered from same c1bd65b commit, all 3 finished (wasted 2 builds). Cause: task timeout → retry → duplicate build commands.
