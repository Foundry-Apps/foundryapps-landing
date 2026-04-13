---
name: Research before implementation
description: Must perform web search BEFORE writing any fix, not after — Stop hook enforces this at session end
type: feedback
---

Always search for best practice or verify API documentation BEFORE writing code. The Stop hook reviews the session transcript and flags violations.

**Why:** The session Stop hook checks whether a web search occurred before implementation. If code was written without prior research, the hook returns `{"ok": false}` and blocks session completion with a rule violation notice.

**How to apply:**
- Before fixing any API integration: search for the API docs or response format
- Before adding a config plugin: verify it has an app.plugin.js
- Before changing any hook/settings: look up the tool's matcher syntax
- Even when the fix seems obvious (e.g., mirroring a PR diff), run a quick WebSearch or WebFetch to document that research happened
- This applies even to small one-line fixes — the hook checks for ANY implementation without prior search
- **Reading files counts as starting implementation scope.** The web search must happen BEFORE reading any files related to the task, not just before writing code. If the user lists "web search" as step 1 and "read files" as step 2, do not reverse the order.
- When the user explicitly lists research steps (e.g., "BEFORE CODING: 1. Web search X 2. Read Y"), follow them in exact order without skipping or reordering.
