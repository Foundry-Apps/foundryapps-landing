---
name: EAS build cache busting requires three layers
description: EAS caches aggressively — must bump Metro cacheVersion AND eas.json cache key AND use --clear-cache flag
type: feedback
---

EAS builds cache at multiple levels. Changing metro.config.js `cacheVersion` alone is NOT sufficient — EAS has server-side caching keyed on the build fingerprint.

**Why:** 3 builds shipped identical bytecode despite code fixes being on master. The cacheVersion bump changed the Metro transform cache but EAS reused its own cached build artifact.

**How to apply:** Every EAS build testing a fix must:
1. Bump `cacheVersion` in metro.config.js (use a descriptive suffix like `-wc8`)
2. Set a unique `cache.key` in the eas.json profile (e.g. `"cache": { "key": "v4-ctx-fix" }`)
3. Pass `--clear-cache` on the `eas build` command
4. After the build starts, verify `isCacheHit: None` in the build metadata
