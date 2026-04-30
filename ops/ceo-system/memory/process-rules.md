---
name: Process rules — debugging, verification, and David's time
description: Consolidated meta-lessons: scientific debugging method, artifact verification, respecting David's time, measure-before-fix
type: feedback
---

**Scientific debugging (mandatory for all non-trivial bugs):**
Observe → hypothesize → predict → test. Never skip observation. Decode exact crash location (source maps, logcat) before proposing any fix. If prediction fails, observe again — don't retry blindly.

**Verify the artifact, not the code:**
Code on master ≠ code in the user's hands. After any build, pull the artifact and verify it contains the fix. For mobile: extract bundle, grep for crash signatures, compare size. For web: curl the page and check content. Never report a fix as shipped without artifact verification.

**David's time is the scarcest resource:**
Every failed manual test costs his time AND trust. Before asking David to test: verify fix is in artifact, run test via adb if device connected, batch changes into one build. Only ask David to test after exhausting automated verification.

**Measure before fixing:**
Don't propose fixes from plausible theories. Decode crash location exactly, verify fix changed the bundle, verify build artifact contains the fix. If same crash after fix, check if same offset (fix didn't land) vs different offset (new issue).
