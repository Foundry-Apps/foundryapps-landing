---
name: Mobile refresh — deferred items
description: Three items deferred from the current mobile refresh scope (2026-04-19), to be picked up later in specific order
type: project
originSessionId: a3a07943-25ea-4687-842b-baa4fad0c808
---
Mobile refresh plan (`docs/mobile-refresh-plan.md`, PR #379) is scoped to Android only for now. David's decisions 2026-04-19:

1. **iOS — out of scope.** Separate effort later, not Phase M5 of the current refresh. Do NOT attempt to make the refresh cross-platform; keep focused on Android.

2. **RevenueCat integration — deferred.** David needs to sign up for RevenueCat first. Queue the integration as the NEXT work item AFTER M0/M1/M2/M3 are complete (the Android refresh fully landed). The `hasMobileIap` stub structure in the Paddle webhook handler (PR #373) is ready to activate once the RevenueCat account + API keys exist.

3. **Google Play identity verification — deferred.** David will complete it later on his own. M4 (production build + Play Store submission) is blocked on this, but M0–M3 can proceed independently since they don't require Play Store publication.

**How to apply:**
- Proceed with M0 → M1 → M2 → M3 unblocked, Android-only.
- When M3 lands, prompt David to start RevenueCat signup before any IAP wiring begins.
- When Google Play verification completes, proceed to M4.
- Do NOT spend any cycles on iOS parity or fixing iOS-specific issues during M0–M3.
