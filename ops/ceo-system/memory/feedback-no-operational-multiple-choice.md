---
name: Don't escalate operational choices to David
description: When hitting operational obstacles, make the call yourself and execute — never present David a multiple-choice menu of routes
type: feedback
originSessionId: c6df3e51-f84e-4319-ac0e-d3d1a055de79
---
Never ask David to pick between operational paths. When a task hits an obstacle — timeout, missing access, ambiguous sub-step, several viable routes — DO NOT send "here are your options, which one?". Make the call, execute, and come back when it's working.

**Why:** David is owner, not operator. Every time I've presented an "option 1 / option 2 / option 3" menu, his response has been "don't ask me what to do, work through it autonomously". Explicitly stated April 2026: "I need you to work through these autonomously, make the call and come back once it's working, keep on top of it."

**How to apply:**
- Hit a spawner timeout? Retry with a smaller prompt or different approach. Don't ask David which.
- Missing an API key? Document what's needed in memory and move on to work that doesn't require it — don't gate all progress on his action unless the ask is genuinely 10 seconds.
- Tool A or Tool B unclear? Pick the simpler/faster one, note it, execute. Revisit if it fails.
- Multiple valid merge orders? Pick the safest, execute, report.
- Don't say "I can do X or Y, which would you like?". Say "Doing X because [reason]. Will report when done."

Applies broadly: deployments, merges, tool selection, error recovery, rebasing, rollbacks, environment issues. Anything operational.

Legitimate reasons to ping David mid-task: (1) genuinely blocked by something only he has — credential, external service signup, legal/compliance decision; (2) significant financial cost about to be incurred; (3) architectural change that warrants his input per the authority matrix; (4) he's already said "ask before X" explicitly in this session.

Everything else: decide, do, report.
