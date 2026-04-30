---
name: Dispatch should check in proactively on long-running tasks
description: When orchestrating code/cowork tasks that run long, don't wait passively for completion — send periodic status updates to David
type: feedback
originSessionId: a3a07943-25ea-4687-842b-baa4fad0c808
---
When Dispatch spawns a task and waits for it to finish, David has flagged silence as a recurring pattern. Dispatch defaulted to "wait for task to notify back", which feels passive from his side — he had to ping to find out the state.

**Why:** David explicitly tied this to the broader review of why work stalls and tokens get burned — passive orchestration is part of the same problem family. He said: *"it's been a while since you've responded which seemed to be a theme, part of the reason I requested a review."*

**How to apply:**
- For any task expected to run more than a few minutes, send a proactive check-in via SendUserMessage every ~5–10 minutes of real time, even if just "task X still running, at step Y".
- When multiple tasks are in flight, batch updates rather than silencing.
- If a task goes idle or stuck, surface it to David before he asks.
- The goal is that David never has to send "how's it going" to find out — he should already know.
- Use `read_transcript` with a short `max_wait_seconds` periodically on long runs, not just "when notified complete".
