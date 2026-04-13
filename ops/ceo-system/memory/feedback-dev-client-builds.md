---
name: Dev client builds crash on physical devices without Metro
description: developmentClient:true in EAS builds requires Metro server; physical devices can't reach it — causes immediate crash
type: feedback
---

Independent code review (10 Apr 2026) identified that Android development client builds (`developmentClient: true` in eas.json profile) require a running Metro server reachable over LAN or tunnel. This works on emulators (localhost) but crashes on physical devices like David's S24 Ultra because Metro isn't reachable.

**Why:** This was likely a contributing factor (alongside Firebase auto-init and .easignore issues) to the persistent crash on David's phone. We spent many builds debugging Firebase when the root cause may have been simpler.

**How to apply:**
- EAS preview/production profiles must have `developmentClient: false` (or omit it, which defaults to false)
- Only use `developmentClient: true` for the `development` profile, which is explicitly for local dev
- When testing on physical devices, always use preview or production profile APKs
- If someone needs to use dev client on a physical device, they must run `expo start --dev-client --host lan` or `--host tunnel`
- Add this check to the EAS pre-build checklist: verify the build profile doesn't have developmentClient:true for device testing
