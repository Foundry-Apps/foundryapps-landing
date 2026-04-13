## Enforced Rules (LOAD EVERY SESSION)
- [Enforced Operating Rules](enforced-rules.md) — 7 TIER 1 blocking rules + 5 TIER 2 standards. Read first, every session.

## Company & Infrastructure
- [Operational authority](operational-authority.md) — Full access to add env vars and manage settings on Supabase and Vercel without escalation
- [Legal structure](legal-structure.md) — Foundry Apps is trading entity, legal docs live on foundryapps.co.uk, products are sub-brands
- [Company incorporation](company-incorporation.md) — Emailed Collas Crill 5 Apr for Guernsey incorporation, Sovereign Group unresponsive
- [Supabase Pro](supabase-pro.md) — Upgraded to Supabase Pro April 2026, connection pooler should be enabled
- [Paddle verified](paddle-verified.md) — Paddle identity verification completed April 4 2026, billing fully live
- [Google OAuth](google-oauth-verified.md) — Google OAuth consent screen verified and in production, no user cap
- [Orbit domain](orbit-domain.md) — Site accessible at orbit.foundryapps.co.uk and orbitlaunches.space
- [Orbit repo host path](orbit-repo-path.md) — Repo is at C:\Users\david\apps\orbit, not Projects\orbit

## Agent Definitions
- [DevOps Agent](agent-devops.md) — Infra, deployments, monitoring, EAS build management
- [QA Agent](agent-qa.md) — Test coverage, production quality, regression detection
- [Finance Agent](agent-finance.md) — Revenue tracking, cost monitoring, ODPA compliance
- [Marketing Agent](agent-marketing.md) — SEO, content, analytics, competitive monitoring
- [Reporting Agent](agent-reporting.md) — Management reports, scheduled tasks, CEO_STATE.md
- [Orbit Engineering Agent](agent-orbit-engineering.md) — Feature dev, bug fixes, mobile debugging protocol
- [Orbit Data Agent](agent-orbit-data.md) — External APIs, data freshness, sync reliability

## CEO Playbook & Operations
- [CEO Playbook rules](ceo-playbook-rules.md) — Deployment checklist, repo hygiene, docs maintenance, new product setup
- [CEO restructuring plan](ceo-restructuring-plan.md) — Phase A complete; Phases B-C pending (agent validation, autonomous week)
- [CEO role clarity](ceo-role-clarity.md) — Claude manages agents; David gets progress updates and strategy questions only
- [Token optimisation](token-optimisation.md) — Poll tasks at 5min intervals, batch instructions, minimise transcript reads
- [No parallel builds or duplicate tasks](feedback-no-parallel-builds.md) — Timeout retries queue silently; check list_sessions before retrying

## Mobile Development
- [Google Play app](google-play-app.md) — Orbit app created in Play Console, app ID 4973631684995836934, verification pending
- [Mobile crash diagnosis](mobile-crash-diagnosis-apr11.md) — Two stacked crashes: webidl-conversions v8 + no routes; both fixed
- [Mobile publish plan](mobile-publish-plan.md) — Phase 2-5 plan: 3 EAS builds max, local validation first
- [Expo access token](expo-token.md) — EXPO_TOKEN for EAS CLI, project ID 7d839386, owner foundry-apps
- [Expo token refresh](expo-token-refresh.md) — New token saved to .env.local
- [EAS build learnings](eas-build-learnings.md) — npm monorepo + Expo = broken; pnpm + Turborepo now
- [First build gate](first-build-gate.md) — New platforms must have successful build before feature dev
- [EAS build budget](eas-build-budget.md) — Limited EAS builds/month; always validate locally before cloud build
- [Mobile pipeline plan](mobile-pipeline-plan.md) — Automate EAS builds via GitHub Actions CI
- [pnpm + Turborepo migration](pnpm-turborepo-migration.md) — Repo uses pnpm 9.15.9 + Turborepo

## Technical Debugging Lessons (April 2026 crash week)
- [extraNodeModules is a fallback](feedback-metro-extraNodeModules.md) — Never use for version pinning; use pnpm.overrides instead
- [EAS cache busting needs 3 layers](feedback-eas-cache-busting.md) — cacheVersion + eas.json cache.key + --clear-cache flag
- [Source map decode is step one](feedback-source-map-first.md) — Always decode Hermes bytecode offsets before attempting fixes
- [expo-router routes broken in monorepos](feedback-expo-router-monorepo-routes.md) — Use local ctx.js shim with relative paths
- [Startup crashes stack](feedback-stacked-crashes.md) — Fixing one crash may reveal another; always re-test
- [Local validation pipeline](feedback-local-validation-pipeline.md) — Run standard checks before every EAS build
- [Verify fix in artifact](feedback-verify-fix-landed.md) — Pull APK and inspect bundle before asking user to test
- [Understand tool semantics](feedback-understand-tool-semantics.md) — Read docs on config options before relying on them

## Meta-Lessons & Process
- [Scientific debugging](feedback-scientific-debugging.md) — Observe → hypothesize → predict → test; never skip observation
- [Verify artifact not just code](feedback-verify-before-shipping.md) — Code on master is not code in the user's hands
- [Respect David's time](feedback-respect-user-time.md) — Minimise manual testing rounds; verify via adb before asking
- [Measure before fixing](feedback-measure-before-fixing.md) — Instrument and observe before proposing fixes
- [Never ask David for manual ops](feedback-no-manual-ops.md) — David is owner, Claude is CEO; never escalate operational tasks
- [Verify PR status via API](feedback-verify-pr-status.md) — Never assume PR merged; always check GitHub API
- [Pre-PR code review required](feedback-pre-pr-review.md) — Every code task must self-review before pushing
- [External research mandatory](feedback-external-research.md) — Always web-search before debugging or planning
- [adb logcat is standard debug](feedback-adb-debug-standard.md) — Always use adb logcat to diagnose crashes, never guess
- [Auto-merge body bug](auto-merge-body-bug.md) — PR bodies with backticks break auto-merge; use plain text
- [Auto-merge CI gate](auto-merge-ci-gate.md) — Auto-merge now waits for CI checks before merging
