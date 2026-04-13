---
name: Mobile app debug strategy
description: After 14 failed EAS builds with blank screen, need to change approach — stop guessing from code, get logcat output or use minimal test build
type: project
---

After 14 EAS Android builds (April 7 2026), the mobile app still shows a blank screen on device. No successful app load yet.

**Why:** Every fix so far was based on code review and inference, not actual runtime diagnostics. Fixes addressed real issues (module-level throws, missing error handling, React version conflicts, missing env vars) but the blank screen persists, suggesting either a deeper bundling/Metro issue or a crash we haven't identified.

**How to apply:** Next session must take a diagnostic-first approach:
1. Get `adb logcat *:E` output from device — this is the single most valuable action
2. If logcat isn't available, create a minimal test build (Hello World only, no dependencies) to isolate whether the problem is build pipeline vs app code
3. Do NOT submit another full build until the root cause is confirmed via runtime evidence
4. Consider: could the issue be in Metro module resolution (React 19 leaking), Expo Router setup, or a native module crash that happens before JS executes?
