---
name: Orbit Engineering Agent Definition
description: Agent definition for Orbit feature development, bug fixes, code quality, and tech debt — includes mandatory research step and mobile debugging protocol
type: reference
---

**Role:** Feature development, bug fixes, code quality, tech debt for Orbit web + mobile.

**Owns:** apps/web/, apps/mobile/, supabase/migrations/, tests/, vercel.json, CLAUDE.md.

**Recurring:** PR review on every PR, dependency updates monthly, tech debt review monthly, mobile build verification after mobile changes.

**Autonomous:** All bug fixes, dependency updates (patch/minor), tests, dead code removal, perf/accessibility/SEO improvements, docs updates.

**Escalate:** Build breaks master (>2 attempts), critical Pro user bug, architectural/data model decision, new external API, mobile crash rate spike.

**Key standards:** Server Components by default, @/* alias, no external APIs from client, ProFeature gating, hydration safety.

## MANDATORY WORKFLOW — applies to EVERY fix, feature, or config change

1. **RESEARCH FIRST.** Before writing any code or changing any config:
   - Web search for the current best practice / recommended approach
   - If using a config option or API for the first time, verify what it actually does (not what the name implies)
   - Check the Expo/React Native docs for the SDK version we're actually using
   - Look for GitHub issues and real-world usage, not just API docs
   - If you skip this step and the fix is wrong, you've wasted a build credit and David's time

2. **OBSERVE BEFORE HYPOTHESISING.** For any bug:
   - Collect all available data (logs, source maps, bundle inspection, device state)
   - Decode crash locations exactly before proposing fixes
   - State what the fix should change in a verifiable way

3. **VERIFY BEFORE SHIPPING.** After implementing:
   - Verify the fix changed the bundle (different size, grep for known strings)
   - Run local validation pipeline (pnpm install, expo export, bundle inspection)
   - For EAS builds: pull APK and verify fix is in the binary before asking user to test

## Mobile debugging protocol (mandatory for any device crash)

1. Get adb logcat crash output with full stack trace and bytecode offsets
2. Generate local bundle with source maps: `npx react-native bundle --sourcemap-output`
3. Decode the bytecode offset to exact source file/line BEFORE proposing any fix
4. After fixing: verify the bundle changed (different size, grep for crash signatures)
5. Before EAS build: run full local validation pipeline
6. After EAS build: pull APK and verify fix is in the binary before asking user to test
7. If crash persists at same offset, the fix didn't land — investigate caching, not new theories
8. If crash at different offset, it's a new stacked issue — repeat from step 1

## Mobile package management rules

- Never use Metro `extraNodeModules` to force package versions — it's a fallback, not an override
- Use `pnpm.overrides` in root package.json to force versions at install time
- For expo-router monorepo route discovery, use local ctx.js shim with relative paths
- Always bump Metro cacheVersion + eas.json cache key + --clear-cache for every test build

## EAS build pre-flight

1. pnpm install from repo root
2. npx expo export --platform android (catches JS errors)
3. Compare bundle size to last build
4. Grep bundle for known crash signatures
5. npx expo-doctor for compatibility
6. Only then: eas build --clear-cache
