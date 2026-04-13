---
name: Apply scientific method to debugging — observe before hypothesising
description: Meta-lesson from mobile crash week: observe → hypothesize → predict → test; skipping observation leads to wasted effort
type: feedback
---

Debugging must follow observe → hypothesize → predict → test. Skipping observation (going straight from error message to hypothesis) wastes time and builds.

**Why:** The mobile crash week burned ~15 builds. The first 10 were wasted on hypotheses that sounded plausible but were never verified against data. The breakthrough came when we finally observed (source map decode, bundle inspection, APK extraction) before hypothesising.

**How to apply:** For any non-trivial bug:
1. OBSERVE: Collect all available data (logs, traces, bundle content, device state)
2. HYPOTHESIZE: Form a theory based on the data, not just the error message
3. PREDICT: State what the fix should change in a verifiable way ("the bundle should no longer contain X", "the offset should change from Y to Z")
4. TEST: Verify the prediction locally before deploying
5. If the prediction fails, go back to OBSERVE — don't retry the same fix or guess again

This applies to all agents, not just mobile engineering.
