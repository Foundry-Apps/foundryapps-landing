---
name: Mobile agent learnings from Phase 3 and independent review
description: Patterns agents must follow for mobile dev — joins, Play Services, dev client builds, data model knowledge
type: feedback
---

Extracted from Phase 3 implementation (PRs #300-304) and independent code review (10 Apr 2026).

### 1. Dev client builds are NOT for physical device testing
- `developmentClient: true` builds need a live Metro server reachable over LAN/tunnel
- Emulators work (localhost) but physical devices crash if Metro is unreachable
- **Rule:** Always use `preview` or `production` EAS profile for APKs David tests on his S24
- **Rule:** Add to EAS pre-build checklist: verify profile doesn't use developmentClient:true for device testing

### 2. Supabase data model — joins are mandatory for related data
- `launches` table does NOT have `provider_name` as a direct column
- Provider data comes via: `agency:agencies(name, abbrev)` join syntax in Supabase query
- Same pattern for pads, rockets, missions — always check the web app query patterns first
- **Rule:** Before writing Supabase queries in mobile, read the equivalent web app query to get the join pattern right

### 3. No Google Play Services dependencies without google-services.json
- `react-native-maps` on Android requires Google Play Services
- We have a placeholder google-services.json, not a real one
- Firebase already caused crashes for the same reason
- **Rule:** Never add packages that depend on Google Play Services until we have real Firebase/Google config
- Safe alternatives: equirectangular map grid (used for ISS), coordinate display, WebView-based maps

### 4. Focus-aware data fetching is mandatory for polling
- Any screen that polls (ISS position, live data) MUST use `useFocusEffect` not `useEffect`
- Polling with `useEffect` continues when tab is unfocused → battery drain
- Pattern: `useFocusEffect` + `useCallback` with interval setup/cleanup
- This was a P2 Codex finding that we fixed and should never regress on

**How to apply:** These rules should be added to CLAUDE.md's Mobile Rules section. Every mobile code task should reference them. The data model join pattern is especially important — agents waste time guessing column names when the web app already has the correct queries.
