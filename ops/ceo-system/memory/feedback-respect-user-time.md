---
name: David's time is the scarcest resource — minimise manual testing rounds
description: Meta-lesson: every time David has to manually test, we've consumed his most valuable resource; verify before asking
type: feedback
---

David's manual testing time is the company's scarcest resource. Every "can you try this build" that fails is a double cost: his time AND his trust in the system.

**Why:** The mobile crash week had David install and test ~6 APKs, most of which crashed with identical errors because the fixes weren't actually in the builds. Each round took 5-10 minutes of his time plus context switching.

**How to apply:**
1. Before asking David to test: verify the fix is in the artifact (pull APK, inspect bundle)
2. Before asking David to test: run the test yourself via adb if the device is connected
3. Batch changes when possible — don't ship 3 separate builds for 3 fixes when they can go in one
4. When reporting results, be honest about confidence level: "verified locally, untested on device" vs "verified on device via adb"
5. Only ask David to test when you've exhausted automated verification
