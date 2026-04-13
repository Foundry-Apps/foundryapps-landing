---
name: expo-router/entry silently fails — bypass with direct require.context
description: renderRootComponent swallows errors and registers blank View; fix is require.context('./app') in index.js
type: feedback
---

expo-router/entry's `renderRootComponent()` has a try/catch that catches ALL errors and registers `() => <View />` (blank white screen), re-throwing via `setTimeout`. This means `require('expo-router/entry')` NEVER throws — diagnostic code that wraps it in try/catch will always report success.

The actual failure: `expo-router/_ctx.android.js` calls `require.context(process.env.EXPO_ROUTER_APP_ROOT, ...)`. In EAS eager bundling, the env var may resolve to wrong path, causing `require.context` to return an empty module map (no error). `ExpoRoot` with empty context renders nothing.

**Why:** 2+ days and 15+ builds wasted debugging a silent failure. Reading expo-router source code revealed the hidden try/catch in renderRootComponent.

**How to apply:** Never rely on expo-router/entry in monorepo EAS builds. Instead, bypass it entirely in index.js:
```js
import { ExpoRoot } from 'expo-router';
import { renderRootComponent } from 'expo-router/build/renderRootComponent';
const ctx = require.context('./app');
function App() { return <ExpoRoot context={ctx} />; }
renderRootComponent(App);
```
`require.context('./app')` is a relative string literal — Metro resolves it correctly regardless of EAS CWD.
