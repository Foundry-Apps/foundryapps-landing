---
name: External research is MANDATORY before any implementation
description: ENFORCEMENT FAILURE on 12 April — agent implemented edge-to-edge fix without web search despite this rule existing since April 10. Rule must be a blocking step, not a suggestion.
type: feedback
---

David said (10 Apr): "We should include external research as part of all debugging processes AND planning"
David said (12 Apr): "I thought this was meant to be baked into our processes already" — after the edge-to-edge fix was implemented without any web search, using a deprecated API, when a one-line config flag was the correct solution.

**Why:** This rule existed since April 10 but was not enforced. The agent saw "nav bar visible", pattern-matched to expo-navigation-bar, and started coding. One web search would have found `edgeToEdgeEnabled: true` in app.json — the official Expo-recommended approach. Instead we shipped a deprecated workaround that needed to be replaced.

**The failure mode:** Passive rules in memory get loaded as context but nothing forces compliance. The agent has to actively choose to research first, and under time pressure it defaults to "implement what I already know."

**How to apply — enforcement, not suggestion:**
1. In EVERY agent definition, research is step 1 in the mandatory workflow — not a principle, a numbered step
2. In the Orbit repo CLAUDE.md, the mobile debugging protocol starts with "web search for best practice"
3. When reviewing agent output, check: did it web search before implementing? If not, reject and redo
4. This applies to ALL implementation, not just debugging — new features, config changes, dependency choices
5. The research must produce specific findings (links, version info, compatibility notes) that inform the implementation
