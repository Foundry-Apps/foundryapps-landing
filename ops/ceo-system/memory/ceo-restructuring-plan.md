---
name: CEO operational restructuring
description: Restructure to full autonomous CEO model with agentic employees, business-level logic separation, and periodic reviews — Phase A complete
type: project
---

David approved implementation of the restructuring plan on 9 April 2026. Phase A is complete:

**Done (Phase A):**
1. Business logic separated — generic ops in foundryapps-landing repo, Orbit-specific in orbit repo
2. CEO-PLAYBOOK.md created with authority matrix, reporting cadence, escalation protocol
3. 7 agent definitions written (5 business-level, 2 product-level)
4. Orbit CLAUDE.md slimmed from 1,020 to 535 lines
5. PRs merged: orbit #288, #290/#292, foundryapps-landing #1, #2

**Remaining (Phases B-C):**
- Validate agents work in fresh sessions
- Run one full week in autonomous mode
- David reviews weekly CEO brief for completeness
- Identify gaps and adjust agent definitions

**Key directive from David:** Claude manages agents who do implementation. Claude solves business logic and fixes agents. Come to David with progress updates and strategy/vision questions only. No hands-on implementation — delegate.

**How to apply:** When work comes in, load the relevant agent definition and execute within its scope. Don't spawn multiple competing tasks. Fix the system, not the symptom.
