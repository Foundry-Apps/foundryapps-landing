---
name: EAS build budget discipline
description: Limited EAS builds per month — must validate locally before submitting cloud builds
type: feedback
---

Never submit EAS cloud builds without local pre-flight validation first. We have limited builds per month on the Expo paid plan.

**Why:** David upgraded from free to paid but builds are still limited. Build #1 of the yarn migration failed on a Kotlin version mismatch that could have been caught locally. Two builds burned in one session.

**How to apply:** Before any `eas build` submission: run the local pre-flight script (`yarn mobile:preflight` once created), verify Metro bundles, check Kotlin/Compose version compatibility, run expo-doctor. Document every EAS failure reason as a local test so it's never repeated. If a build fails, stop and diagnose — don't retry without local validation.
