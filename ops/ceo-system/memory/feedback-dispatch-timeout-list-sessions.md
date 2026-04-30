---
name: After start_code_task timeout, always list_sessions before retrying
description: Dispatch start_code_task tool times out on the MCP client side but often the session has still been created on the host — retrying without checking creates duplicate sessions that compete
type: feedback
originSessionId: a3a07943-25ea-4687-842b-baa4fad0c808
---
`mcp__dispatch__start_code_task` has a 60s client-side timeout. When the host is slow to respond, the tool returns a timeout error BUT the session has usually already been created on the host. Retrying without checking produces a second session with the same prompt running in parallel, which can:
- Race each other to open PRs for the same fix
- Consume 2x tokens
- Create conflicting branches/PRs that have to be cleaned up

**Why:** Seen twice in the same session — "Orbit business logic audit" duplicated, then "Fix Paddle race + dedupe Pro checks" duplicated. Both required abort messages to the duplicate to stop them stepping on the primary.

**How to apply:**
- If `start_code_task` returns a timeout error, DO NOT immediately retry.
- First call `list_sessions` (limit 5 is enough) to check whether a session with the intended title is now running or was just created.
- If a matching session exists: that's your task, monitor it with `read_transcript`. Don't spawn again.
- If no matching session: could be one of two things, both legitimate:
  1. **Genuine host-side spawn failure** — retry is safe (with a slightly different title to avoid any race).
  2. **Waiting on David's UI approval** — confirmed 2026-04-20 by David. Even with bypass mode enabled, new code sessions sometimes require a manual workspace-approval click in the Cowork UI. From Dispatch's perspective this looks like a 60s timeout with no session created. It's NOT a host failure; the session will spawn as soon as David clicks approve. Don't over-retry.
- Heuristic: if Dispatch sees 2–3 consecutive `start_code_task` timeouts on the same workspace, don't assume the host is broken. Surface it to David briefly ("approval may be waiting in the UI") and pick one of: wait, fall back to routing via an existing session in that workspace, or ask David to check.
- Same pattern applies to `start_task` (non-code variant) — always list first after a timeout.
