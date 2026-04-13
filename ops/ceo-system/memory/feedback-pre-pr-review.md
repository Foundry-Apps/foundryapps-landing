---
name: Code review before PR submission
description: Every code task must self-review changes before pushing PRs — use engineering:code-review skill or superpowers review
type: feedback
---

Code tasks were pushing PRs without reviewing their own changes. Codex (external GitHub bot) was catching issues that should have been caught locally — including P1 bugs like .easignore missing critical entries and HTTP endpoints.

**Why:** David explicitly flagged this: "there are some great comments being left by the code reviewer on the PRs but I don't see them being taken into consideration." He also said "fix the agent, not just the problem" — the workflow needs to prevent this class of issue, not just fix individual bugs.

**How to apply:**
- Every code task prompt should include instruction to review its own diff before creating a PR
- Use `engineering:code-review` skill (available via Cowork) or superpowers review skill (if available in Claude Code CLI)
- Check: security, correctness, performance, and adherence to CLAUDE.md rules
- Specifically verify .easignore/.gitignore parity, HTTP vs HTTPS, and PR checklist items from CLAUDE.md
- David wants agents to have the right plugins/skills — verify tool availability at task start
