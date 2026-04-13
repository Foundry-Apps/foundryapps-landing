---
name: Verify agent plugins and skills
description: Code task agents must have access to required plugins (superpowers, etc) — check before spawning
type: feedback
---

David has superpowers plugin v5.0.7 installed globally via claude-plugins-official marketplace. It's in `~/.claude/settings.json` and loads for ALL Claude Code sessions, including code tasks spawned by Cowork.

**Why:** David asked "do our agents have the right plugins/skills?" The agents were operating without leveraging available tools. David's principle: "fix the agent, not just the problem."

**Superpowers skills available to all code tasks:**
- `superpowers:requesting-code-review` — code review workflow
- `superpowers:receiving-code-review` — handling review feedback
- `superpowers:writing-plans` — structured planning
- `superpowers:executing-plans` — plan execution
- `superpowers:subagent-driven-development` — parallel agent work
- `superpowers:systematic-debugging` — structured debugging
- `superpowers:test-driven-development` — TDD workflow
- `superpowers:verification-before-completion` — final verification

**How to apply:**
- Code tasks automatically have superpowers — reference skills by name in prompts when relevant
- For code changes: include `superpowers:requesting-code-review` in task instructions
- For debugging: reference `superpowers:systematic-debugging`
- For complex features: reference `superpowers:writing-plans` + `superpowers:executing-plans`
