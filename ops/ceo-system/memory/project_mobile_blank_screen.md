---
name: Mobile Blank Screen Root Cause (multiple layers)
description: Android blank screen had two distinct root causes — React 18/19 Metro split (PR #200) and expo-router empty route context (PR #234)
type: project
---

## Layer 1: React 18/19 Metro split (PR #200)

Build 023256ce showed blank screen because two React instances were in the bundle.
- react@19 hoisted to root (web wins), react@18 in `apps/mobile/node_modules/react`
- With `disableHierarchicalLookup = false`, packages resolve react@19 from root; app gets @18 → silent crash before any component mounts
- **Fix**: `disableHierarchicalLookup = false` is now intentionally set back (safe because root package.json nohoists react-native, leaving root react@18 same as mobile's), and `extraNodeModules` pins react/react-native.

## Layer 2: expo-router empty route context (PR #234)

After PR #200, screen was still blank but for a different reason.

**Root cause chain**:
1. `expo-router/entry` → `entry-classic.js` → `qualified-entry.js` → `expo-router/_ctx.android.js`
2. `_ctx.android.js`: `require.context(process.env.EXPO_ROUTER_APP_ROOT, ...)` — Metro needs a string literal at transform time
3. Babel plugin inlined an absolute path, but if wrong during EAS eager bundling → empty context → ExpoRoot renders nothing
4. `renderRootComponent()` catches errors internally and registers `() => <View />` (blank), re-throwing via `setTimeout` — so `require('expo-router/entry')` NEVER throws synchronously from index.js
5. Diagnostic screen saw "loaded without throwing" but expo-router had silently installed a blank component

**Fix (PR #234)**: Bypass `expo-router/entry` entirely in `index.js`:
```js
import { ExpoRoot } from 'expo-router';
import { renderRootComponent } from 'expo-router/build/renderRootComponent';
const ctx = require.context('./app', true, /regex/, 'sync');
function App() { return <ExpoRoot context={ctx} />; }
renderRootComponent(App);
```
`require.context('./app')` is a string literal relative to `apps/mobile/index.js` — Metro always resolves it to `apps/mobile/app/` correctly.

**Key insight**: `renderRootComponent` always calls `registerRootComponent` (either real app or blank View on error). Errors inside it are swallowed synchronously and re-thrown via setTimeout. Never trust that "require didn't throw" means expo-router succeeded.

**How to apply**: If blank screen recurs after expo-router upgrades, check that index.js still uses direct `require.context('./app')` rather than delegating to expo-router/entry.
