---
name: Mobile business logic + build pipeline audit (queued post-UI-refresh)
description: After the mobile UI refresh is complete and passing audit, run a business-logic + build-pipeline audit on mobile mirroring the web audit pattern from 2026-04-19
type: project
originSessionId: a3a07943-25ea-4687-842b-baa4fad0c808
---
**When:** After Phase M3 of mobile refresh lands AND Dispatch is satisfied the UI work is solid (not just shipped). Do NOT kick off while UI work is still in flight — David explicitly wants UI completed first.

**Why:** David asked 2026-04-19, pattern mirror of the web audit that produced PRs #371 (crons batch), #372 (hygiene), #373 (Paddle race). Mobile has been evolving rapidly with SDK upgrades, expo-router quirks, and crash cycles — accumulated debt likely.

**Scope — two audits, one report each:**

### A. Business logic audit (mirror of `audit/business-logic-audit-2026-04-20.md`)
Hypothesis grid:
- **H1. Duplicate sources of truth** — user/subscription/auth/launches state on mobile vs web API vs cached local store.
- **H2. Sync logic that fights itself** — background fetchers, focus-aware polling, notification handlers touching the same data with different rules.
- **H3. N+1 / inefficient queries** — Supabase calls in render loops, screen mounts, or navigation events.
- **H4. Incoherent module boundaries** — business logic in screen components, fetching layered wrong.
- **H5. Dead code / orphaned screens** — routes in the tree no nav path hits.
- **H6. Duplicate abstractions** — hooks/util functions doing the same job.
- **H7. Config / env sprawl** — EAS profile env vars, Expo dashboard env vars, `.env.local`, `app.json` extra config — drift across these.
- **H8. Pro/Free tier enforcement** — mobile entitlement checks consistent across screens and matching web + Paddle + (eventually) RevenueCat? Any client-only gates with no server backup?

### B. Build pipeline audit (new — mobile-specific)
- **EAS config correctness** — profiles (preview/production), env var injection, build credentials, Android/iOS (if ever enabled) SDK versions, Gradle/Kotlin pins.
- **expo-doctor full run** — every warning understood and either fixed or documented as accepted.
- **OTA update strategy** — `expo-updates` wired? If yes, channels + rollback plan documented. If no, explicit decision.
- **Version management** — `versionCode` handling (`appVersionSource: remote` seems in use — confirm), semver on the JS side, `app.json` version vs native version.
- **Bundle size trend** — is it growing? What's in the bundle that shouldn't be?
- **Pre-flight script** — is there one? Does it match `expo-mobile-debugging-playbook.md`'s recommendation?
- **Release Android credentials** — keystore/signing setup, stored in EAS, rotation strategy.
- **Play Store submission readiness** — once Google Play verification completes, what manual steps remain.

**Deliverable:** one PR adding `audit/mobile-audit-<date>.md` (read-only, no code changes). Ranked findings with severity / effort. Separate follow-up PRs for implementation after David reviews.

**How to apply:** When M3 lands and the UI passes the mobile-adapted 8-hypothesis grid, Dispatch proactively proposes running this audit. Do NOT delegate to an implementation session — this is diagnostic only. No fixes until David reviews.
