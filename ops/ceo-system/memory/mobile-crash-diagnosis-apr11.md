---
name: Mobile crash root cause — two layered crashes fixed
description: App had two crashes: webidl-conversions v8 (ES2024 on Hermes) fixed via pnpm.overrides, then "No routes found" fixed via local ctx.js shim
type: project
---

**Status (11 April 2026):** Two crashes diagnosed and fixed in one session.

**Crash 1 — webidl-conversions v8 (FIXED, PR #315 merged):**
`webidl-conversions@8.0.1` calls `Object.getOwnPropertyDescriptor(ArrayBuffer.prototype, "resizable").get` at module load time. Hermes doesn't support ES2024 `ArrayBuffer.resizable`, so it returns undefined and `.get` crashes.

Fix: `pnpm.overrides` in root package.json forces v5.0.0. Metro `extraNodeModules` does NOT work as an override — it's a fallback that's never consulted when the package exists in nodeModulesPaths. Only pnpm.overrides (or npm overrides/yarn resolutions) actually force version replacement.

**Crash 2 — "No routes found" (FIXED, PR #316):**
expo-router's `_ctx.js` uses `require.context(process.env.EXPO_ROUTER_APP_ROOT)`. Babel inlines this as an absolute path. But `require.context()` resolves relative to the calling file (`node_modules/expo-router/`), so it finds zero routes.

Fix: Local `ctx.js` shim in `apps/mobile/` with correct relative path `./app`, plus Metro `resolveRequest` to intercept `expo-router/_ctx` and redirect to the local shim. Verified locally: bundle went from 1.42 MB (zero routes) to 1.75 MB (all routes present).

**Key learnings:**
1. `extraNodeModules` is a FALLBACK, not an override — never use it to force package versions
2. Use `pnpm.overrides` to force package versions at install time
3. EAS builds cache aggressively — always bump cacheVersion AND use --clear-cache
4. Source map decoding is the definitive way to find crash locations in Hermes bytecode
5. Multiple crashes can stack — fix one and a different one appears

**How to apply:** For any future dependency compatibility issue, use pnpm.overrides not Metro config. For expo-router route discovery issues in monorepos, use a local ctx.js shim with relative paths.
