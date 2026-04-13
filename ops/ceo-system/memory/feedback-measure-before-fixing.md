---
name: Measure before fixing — don't guess at root causes
description: Always instrument and observe before proposing fixes; hypotheses without data waste builds and time
type: feedback
---

Don't propose fixes based on plausible-sounding theories. Measure first, fix second.

**Why:** We spent a week on this mobile crash. The first hypothesis (duplicate React Navigation) was plausible but wrong — the packages weren't actually duplicated. The second (webidl-conversions via Metro pin) identified the right file but used the wrong fix mechanism. Only when we decoded the source map and inspected the actual bundle did we find the real cause and the right fix level.

**How to apply:**
1. Before fixing: decode the crash location exactly (source maps, adb logcat, etc.)
2. Before building: verify the fix changed the bundle (different size, different content at crash offset)
3. Before testing: verify the build artifact contains the fix (pull APK, grep bundle)
4. After testing: if same crash, check if it's the same offset — if yes, the fix didn't land; if different, it's a new issue

This is the scientific method applied to debugging: observe → hypothesize → predict → test. Skipping observation led to wasted builds.
