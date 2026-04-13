---
name: Verify the artifact, not just the code
description: Meta-lesson: the code being correct on master is not the same as the fix being in the deployed artifact; verify the actual binary
type: feedback
---

Code on master is not the same as code in the user's hands. Build pipelines have caches, transforms, and optimisations that can silently serve old artifacts.

**Why:** Three separate EAS builds shipped identical bundles despite fixes being merged to master. We asked David to test each time. That's three rounds of "install, launch, crash, capture logcat, share file" that were completely wasted because we never checked the APK.

**How to apply:**
1. After any build: pull the artifact (APK, bundle, deployed page) and verify it contains the fix
2. For mobile: extract the Hermes bundle, grep for known crash strings, compare bundle size
3. For web: curl the deployed page and check for the expected content, not just HTTP 200
4. Never tell the user "try again" without first confirming the fix is in the artifact
5. This is a CEO-level rule: agents must verify artifacts before reporting fixes as shipped
