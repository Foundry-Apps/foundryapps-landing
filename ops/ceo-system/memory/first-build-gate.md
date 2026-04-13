---
name: First build gate rule
description: New platform targets must have a successful production build before feature development starts
type: feedback
---

Any new platform target (mobile app, desktop app, new deployment target) must have a successful end-to-end build and deploy BEFORE feature development begins. No point building screens if we can't ship them.

**Why:** During Orbit mobile development, 6+ screens were built before attempting the first EAS build. The build failed due to npm workspace + Expo monorepo incompatibility — a known community issue that would have been caught immediately with a "hello world" build on day one. This wasted significant effort.

**How to apply:**
1. When planning a new platform/target, the FIRST task is: scaffold minimal app → run production build → confirm artifact (APK, IPA, bundle) is generated
2. Only after build succeeds: begin feature development
3. Architecture review must include "can we actually build and deploy this?" as a hard requirement
4. Add to project planning checklist in CLAUDE.md
