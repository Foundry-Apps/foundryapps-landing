---
name: Token efficiency — all rules consolidated
description: All token efficiency rules: polling discipline, duplicate prevention, circuit breakers, scheduled task budgets, worktree limitations
type: feedback
---

**Polling discipline:**
- Wait 60s+ between read_transcript calls. Use max_wait_seconds=120.
- Never poll more than 3 times without sending a redirect message.
- For tasks >10min, use a single long max_wait_seconds=300.
- Report results in one message, not incremental updates.

**Duplicate prevention:**
- If start_code_task times out, check list_sessions before retrying — it likely started.
- One EAS build at a time. Before any eas build, run eas build:list and abort if recent build exists.
- Reuse existing sessions via send_message instead of spawning new ones.

**Circuit breakers:**
- Always include "if this approach fails twice, stop and report back" in task prompts.
- If read_transcript returns the same summary 3 times, send "STOP and do X instead".
- Never let a task loop more than 3 attempts on the same problem.

**Worktree limitations:**
- Code tasks run in git worktrees without node_modules. Tasks needing expo/eas/metro must either run pnpm install first or use Desktop Commander on the main repo.

**Scheduled task budgets:**
- Include "TARGET: under N tool calls" in prompts. Daily reports: 15 calls. Weekly: 25.
- Keep task prompts concise — don't repeat CLAUDE.md context.

**Task prompt efficiency:**
- Front-load the goal. Be specific about what to do, not how to think.
- Don't include enforced rules text if the task is simple (health check, cleanup).
- Only include rules relevant to the specific task type.
