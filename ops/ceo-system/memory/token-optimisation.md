---
name: Token Optimisation Rules
description: David flagged excessive token usage from polling and repeated transcript reads — optimise all agent interactions
type: feedback
---

David flagged (April 4, 2026) that we're burning tokens too fast from excessive polling of code task transcripts.

**Why:** Each `read_transcript` call consumes tokens. Polling every 2 minutes for a task that takes 15 minutes wastes ~7 calls. Combined with long conversation context, this compounds fast.

**How to apply:**
- Poll code tasks at 5-minute intervals minimum, not every 2 minutes
- Use `sleep 300` between checks instead of back-to-back read_transcript calls
- For tasks expected to take >10 min, use a single long `max_wait_seconds: 300` instead of multiple short waits
- Don't send multiple follow-up messages to the same session — batch instructions
- Keep task prompts concise — the agent has CLAUDE.md for context, don't repeat it
- Avoid spawning duplicate tasks when dispatch times out — check list_sessions first
- Report results to user in one message, not incremental updates
