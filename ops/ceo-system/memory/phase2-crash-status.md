---
name: Mobile crash - expo-router ContextNavigator TypeError
description: App crashes on S24 with TypeError in expo-router ContextNavigator useMemo/getValue — JS navigation bug, not Firebase
type: project
---

**Status (10 Apr 2026):** App still crashes on David's S24 Ultra. Phase 2 gate NOT passed.

**Real crash cause (from adb logcat):**
```
FATAL EXCEPTION: mqt_native_modules
Process: co.uk.foundryapps.orbit
com.facebook.react.common.JavascriptException: TypeError: Cannot read property 'get' of undefined
Stack: ContextNavigator@1:829441 → useMemo → getValue@1:62968
```

This is a JS-level error in expo-router's navigation context initialization — `ContextNavigator` calls `useMemo` which calls `getValue` which tries to `.get` on an undefined object. NOT Firebase, NOT .easignore (those were fixed but weren't the crash cause).

**Previous fixes applied (necessary but not sufficient):**
- .easignore fixed (PR #298)
- Firebase auto-init disabled (PR #297)
- Phase 3 screens built (PRs #300-304)
- Mobile rules added to CLAUDE.md (PR #306)

**How to apply:** Must investigate expo-router navigation setup in `apps/mobile/app/_layout.tsx`, check for version mismatches between expo-router and React Navigation, and verify route context providers are correctly initialized.
