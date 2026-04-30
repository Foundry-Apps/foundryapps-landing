---
name: SDK upgrade complete — now on Expo 54
description: Expo SDK upgrade 52→54 merged via PR #333 on 13 April 2026. Expo 54.0.33, RN 0.81, React 19, expo-router 6, Metro 0.83.
type: project
---

**Status (13 April 2026):** COMPLETE. PR #333 squash-merged to master.

**What shipped:**
- Expo 52→54.0.33, React Native 0.76→0.81, React 18→19
- expo-router 4→6, Metro 0.81→0.83
- Cleanup: removed redundant sync arg in ctx.js, removed enforceContrast from app.json, removed jscodeshift devDep

**Follow-ups noted in PR (not blocking):**
- `newArchEnabled: false` — enable New Architecture in a dedicated PR
- Production EAS profile needs `cache.key` before first SDK 54 production submission
- `kotlinVersion: "1.9.25"` needs bumping to `2.0.x` when New Arch is enabled
- expo-doctor shows 3 monorepo-related warnings (nested RN copies, React version split, nav package splits) — not build blockers

**How to apply:** SDK upgrade is done. Next step per mobile-publish-plan.md is Phase 2: local Metro export validation, then a preview build.
