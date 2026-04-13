---
name: Metro resolver must match .js extensions
description: Custom Metro resolveRequest hooks must match both with and without .js extension (historical lesson, resolver removed Apr 2026)
type: feedback
---

When writing custom Metro `resolveRequest` resolvers to intercept and redirect module imports, always match both `'./module'` AND `'./module.js'` variants. Node's `require('./utils.js')` passes the literal string including the `.js` extension.

**Why:** PRs #261-263 showed this pattern. The custom whatwg-url resolver was ultimately removed (9 Apr 2026) along with the entire react-native-url-polyfill dependency, but the lesson applies to any future Metro resolver work.

**How to apply:** Any future Metro resolver intercepts should use: `(moduleName === './foo' || moduleName === './foo.js')`.
