---
name: Yarn Workspaces Migration
description: Monorepo migrated from npm to yarn classic 1.22.22 workspaces on 6 April 2026 to fix Metro transformFile crash in EAS builds
type: project
---

Migration complete as of 6 April 2026. Repo now uses `yarn@1.22.22` (`packageManager` field in root `package.json`).

**Why:** npm workspaces couldn't hoist `@expo/metro-config` alongside `metro@0.81.5` for EAS Android builds. Metro's `transformFile` crashed with `this._transformer` undefined.

**Key config in root package.json:**
- `workspaces.packages`: includes `apps/mobile`
- `workspaces.nohoist`: `["**/@sentry/nextjs", "**/@sentry/nextjs/**"]` — keeps sentry alongside next.js in apps/web (React 18/19 conflict)
- `resolutions`: `{ "@asamuzakjp/css-color/lru-cache": "^10.4.3" }` — prevents ESM TLA crash in vitest
- `devDependencies`: includes `"next": "16.2.1"` — required for Vercel framework detection (reads root package.json)

**EAS build status:** First successful APK built 6 April 2026 (build 3ae4c724). Second successful APK built 6 April 2026 (build 471dd963, finished 22:49). Two-part fix required:
1. `kotlinVersion: "1.9.25"` in `expo-build-properties` android config (sets buildscript classpath)
2. Custom plugin `apps/mobile/plugins/withKotlinVersion.js` (sets project-level `ext.kotlinVersion`) — ExpoModulesCorePlugin checks `project.rootProject.ext` (not buildscript.ext) to select Compose Compiler; without project-level ext, it falls back to 1.9.24, selecting Compose Compiler 1.5.14 UNLESS something else sets it to 1.9.25 causing a mismatch.

Command: `EXPO_TOKEN=... EAS_SKIP_AUTO_FINGERPRINT=1 npx eas-cli build --platform android --profile preview --non-interactive` from `apps/mobile`.

**Lint notes:** Yarn resolves newer eslint-plugin-react-hooks with stricter rules (set-state-in-effect, purity, refs, preserve-manual-memoization) and stricter eslint-plugin-react (no-unescaped-entities). These are disabled in eslint.config.mjs to maintain parity with master. Pattern B hydration safety (useState + useEffect) is the prescribed approach per CLAUDE.md and intentionally conflicts with set-state-in-effect.

**expo-asset/tools/hashAssetFiles cannot be found in EAGER_BUNDLE (7 April 2026):** Metro's `Assets.js` resolves `assetPlugins` via a plain Node `require()` from its own location (`root/node_modules/metro/src/Assets.js`). `@expo/metro-config` passes the bare specifier `'expo-asset/tools/hashAssetFiles'` — which Metro can only resolve if `expo-asset` is at the monorepo root `node_modules/`. If yarn hoists it to `apps/mobile/node_modules/` instead, the require fails. Fix: override `config.transformer.assetPlugins` in `metro.config.js` with `[require.resolve('expo-asset/tools/hashAssetFiles')]` — `require.resolve` runs in `apps/mobile/` context and returns an absolute path, bypassing Metro's native require resolution entirely. Build `84aef9dd` confirmed fix (production AAB, 7 April 2026).

**How to apply:** Use `yarn install --ignore-engines` for all installs. Install commands use yarn, not npm.
