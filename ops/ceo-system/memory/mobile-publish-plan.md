---
name: Mobile publish plan
description: Phase 2-5 plan to get Orbit mobile app to Google Play Store — minimal builds, local validation first
type: project
---

**Objective:** Get Orbit Android app published on Google Play Store.

**Current state (9 Apr 2026):**
- Screens: 3 placeholder tabs (Home, Launches, ISS) — no real data
- Infrastructure: babel fix, metro config, auth provider, supabase client, billing module all in place
- EAS: project ID configured but `eas init` may need re-running
- google-services.json: PLACEHOLDER (project_number: 000000000000)
- Store assets: icon, splash, adaptive-icon exist; store metadata (description, keywords) exist
- RevenueCat API key: NOT SET
- No real-device verification yet

**Plan (build-minimal approach):**

Phase 2 (Gate: app launches on real device):
1. Run local Metro export to validate bundle compiles
2. Run eas init + one preview build
3. David tests ARM64 APK on phone
4. Gate: app shows Home tab without crashing

Phase 3 (Real content — no build needed, code changes only):
1. Build Launches screen with Supabase data
2. Build ISS tracker screen
3. Build Events tab
4. Build Missions tab  
5. Local Metro export validation after each

Phase 4 (Auth + billing — needs one build):
1. Wire up auth flows (Google, email)
2. Wire up RevenueCat (needs API key from David)
3. Pro gating on premium content
4. One preview build + device test

Phase 5 (Store submission):
1. Real google-services.json (Firebase project)
2. Production build (AAB)
3. Store listing screenshots
4. EAS Submit to Play Console internal track
5. David reviews and publishes

**Build budget:** Maximum 3 EAS builds total (Phase 2 preview, Phase 4 preview, Phase 5 production)
