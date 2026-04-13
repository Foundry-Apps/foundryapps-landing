---
name: Verify the fix is actually in the artifact before testing
description: Never assume a merged PR means the fix is in the build — verify the actual binary contains the change
type: feedback
---

A fix being merged to master does NOT mean it's in the build artifact the user is testing. Caching, stale builds, and build pipelines can all serve old code.

**Why:** We burned 3 builds where the fix was on master but EAS served cached bundles. We should have pulled the APK, extracted the bundle, and verified the fix was present before asking David to test.

**How to apply:**
1. After an EAS build finishes, pull the APK via adb or download from EAS
2. Extract the bundle and grep for known crash signatures (e.g. "resizable" for webidl v8)
3. Compare bundle size to previous builds — if identical, the fix didn't land
4. Only then ask the user to test
5. For source-level verification, decode a known offset and confirm it points to fixed code
