---
name: adb logcat is the standard mobile crash debugging method
description: Always use adb logcat (clear → launch → dump) to diagnose mobile crashes instead of guessing from build config
type: feedback
---

David explicitly said: "This is a much better manual debug approach, ensure we always use an approach like this" after we used adb logcat to find the real crash cause (expo-router ContextNavigator TypeError) instead of guessing it was Firebase.

**Why:** We spent many builds and PRs debugging Firebase auto-init when the actual crash was a JS-level TypeError in expo-router navigation. adb logcat revealed the real cause in minutes.

**How to apply:**
1. When the app crashes on device, FIRST get a logcat: `adb logcat -c` → launch app → `adb logcat -d > crash.txt`
2. Filter for the app package: `grep -i "co.uk.foundryapps.orbit\|FATAL\|JavascriptException\|TypeError\|Error" crash.txt`
3. Find the FATAL EXCEPTION block — it contains the actual stack trace
4. Never guess at crash causes from build config alone
5. This applies to ALL future mobile crash diagnosis, not just this one bug
6. The package name on device is `co.uk.foundryapps.orbit` (not com.foundryapps.orbit)
