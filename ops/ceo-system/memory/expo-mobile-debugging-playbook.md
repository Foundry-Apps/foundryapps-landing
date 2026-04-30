---
name: Expo mobile debugging playbook
description: Consolidated lessons from April 2026 crash week — Metro resolution, EAS caching, source maps, route discovery, validation pipeline
type: feedback
---

Consolidated from 8 separate memory files (April 2026 crash week). These all apply when debugging Expo/React Native issues in the Orbit monorepo.

**Metro resolution:**
- `extraNodeModules` is a fallback, not an override. Use `pnpm.overrides` in root package.json to force package versions.
- `disableHierarchicalLookup` only prevents upward tree walking, not lateral resolution into nested node_modules.
- Always read docs/issues on config options before relying on them — names are misleading.

**EAS caching (3 layers):**
1. Bump `cacheVersion` in metro.config.js
2. Set unique `cache.key` in eas.json profile
3. Pass `--clear-cache` on `eas build`
4. Verify `isCacheHit: None` in build metadata

**Source map decode — always first:**
- For Hermes crashes with bytecode offsets, decode to source file+line before attempting fixes.
- `npx react-native bundle` with `--sourcemap-output`, then use `source-map` package to decode.

**Route discovery in monorepos:**
- expo-router's `_ctx.js` resolves paths relative to node_modules, not the app. Use a local `ctx.js` shim with `require.context('./app', ...)` and a Metro `resolveRequest` override.

**Startup crashes stack:**
- Fixing one module-loading crash may reveal another. Always re-test and capture fresh logcat. Budget 2+ crash-fix cycles.

**Pre-build validation pipeline:**
1. `pnpm install` from root
2. `npx expo export --platform android`
3. Check bundle size vs previous (identical = fix didn't land)
4. Grep bundle for known crash signatures
5. `npx expo-doctor`
6. Only then: `eas build --clear-cache`

**Verify fix in artifact:**
- Merged PR ≠ fix in build. Pull APK, extract bundle, grep for crash signatures. Compare bundle size. Never ask David to test without verifying first.
