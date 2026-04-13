---
name: Startup crashes stack — fixing one reveals the next
description: Multiple crashes can hide behind each other during app startup; always assume there may be another crash after fixing one
type: feedback
---

When an app crashes during module loading (before React mounts), it prevents later crashes from ever being reached. Fixing the first crash may reveal a completely different second crash.

**Why:** The webidl-conversions crash fired during require() (module loading phase), which prevented React from mounting, which prevented expo-router's ContextNavigator from running, which hid the "No routes found" error. We only discovered the route issue after fixing the first crash.

**How to apply:** After fixing any startup crash, don't assume the app will work. Run the app again immediately and capture fresh logcat. If a new crash appears at a different bytecode offset, it's a separate issue that was masked by the first one. Budget for at least 2 crash-fix cycles for any app that has never booted successfully.
