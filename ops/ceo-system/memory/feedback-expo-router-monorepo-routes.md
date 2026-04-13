---
name: expo-router route discovery broken in monorepos
description: expo-router _ctx.js uses require.context with paths that don't resolve correctly in monorepos — use a local ctx.js shim
type: feedback
---

expo-router's `_ctx.js` calls `require.context(process.env.EXPO_ROUTER_APP_ROOT)`. The babel plugin inlines this as an absolute path, but `require.context()` resolves relative to the calling file (which is in `node_modules/expo-router/`). In a monorepo, this results in zero routes being discovered.

**Why:** After fixing the webidl-conversions crash, the app hit "Error: No routes found" in ContextNavigator. The bundle contained zero route files despite them existing in `apps/mobile/app/`.

**How to apply:** Create a local `apps/mobile/ctx.js` shim that uses `require.context('./app', ...)` with a correct relative path. Add a Metro `resolveRequest` override that intercepts `expo-router/_ctx` and redirects to the local shim. This ensures route discovery works regardless of where node_modules is hoisted.
