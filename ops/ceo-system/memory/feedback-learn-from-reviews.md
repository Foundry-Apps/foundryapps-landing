---
name: Learn from external code review findings
description: When David shares code reviewer findings, fix issues AND add patterns to agent instructions so they don't recur
type: feedback
---

David kicks off independent code reviews (via GitHub PR reviewer bot and sometimes manual reviews) and shares findings. When he does:

1. Fix all identified issues in code
2. Extract patterns/rules from the findings
3. Add those rules to CLAUDE.md or agent instructions so future code tasks avoid the same mistakes
4. Update memory if the finding reveals a systemic gap

**Why:** David said "we should ensure the agents learn from the findings." This is the "fix the agent, not just the problem" principle applied to code review feedback. The goal is compound improvement — each review makes the agents better.

**How to apply:**
- When David pastes review findings, treat them as both a bug list AND a training signal
- Fix the bugs, then ask: "what rule would have prevented this?"
- Add that rule to the appropriate place (CLAUDE.md, PR checklist, agent rules, or memory)
