---
name: Read the docs on tool semantics before using them
description: Don't assume what a config option does — verify its actual behavior, especially for Metro/bundler config which has many non-obvious semantics
type: feedback
---

Configuration options often don't do what their names suggest. Read the actual implementation or docs before relying on them.

**Why:** `extraNodeModules` sounds like it overrides module resolution. It doesn't — it's a fallback. `disableHierarchicalLookup` sounds like it prevents all upward resolution. It doesn't — it only prevents walking up the directory tree, not lateral resolution into nested node_modules. `cacheVersion` in Metro sounds like it controls all caching. It doesn't — EAS has its own cache layer.

**How to apply:** When using a bundler/build config option for the first time:
1. Web search for its actual behavior (not just the docs — look for GitHub issues and Stack Overflow)
2. Verify it does what you think by testing locally (e.g. add a console.log and check the bundle)
3. Don't chain multiple config options hoping one of them works — understand each one individually
