---
name: Local validation pipeline before every EAS build
description: Run a standard set of local checks before every EAS build to catch issues without burning build credits
type: feedback
---

EAS builds cost money and take 10-15 minutes. Every build should be preceded by local validation.

**Why:** Multiple builds wasted on issues that could have been caught locally (missing packages, unchanged bundles, absent route files).

**How to apply — pre-build checklist:**
1. `pnpm install` from repo root (ensures lockfile is applied)
2. `npx expo export --platform android` from apps/mobile (catches JS bundle errors)
3. Check bundle size — if it matches the previous build exactly, the fix didn't change anything
4. Grep the bundle for known crash signatures (e.g. "resizable", "No routes found")
5. If fixing a specific file, grep the bundle to confirm the fixed code is present
6. `npx expo-doctor` for version compatibility
7. Only then: `eas build --clear-cache`
