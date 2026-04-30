## Enforced Rules (LOAD EVERY SESSION)
- [Enforced Operating Rules](enforced-rules.md) — 7 TIER 1 blocking rules + 5 TIER 2 standards

## Token Efficiency (LOAD EVERY SESSION)
- [Token efficiency rules](token-efficiency-all.md) — Polling, duplicates, circuit breakers, task budgets

## Backup
- [CEO config backup repo](ceo-config-backup.md) — Foundry-Apps/ceo-config (private); restore procedure + manual sync cadence

## Company & Infrastructure
- [Operational authority](operational-authority.md) — Full access to Supabase and Vercel env vars/settings
- [Legal structure](legal-structure.md) — Foundry Apps = trading entity, products are sub-brands
- [Company incorporation](company-incorporation.md) — Emailed Collas Crill 5 Apr for Guernsey incorporation
- [Supabase Pro](supabase-pro.md) — Pro plan, connection pooler enabled
- [Paddle verified](paddle-verified.md) — Identity verified April 2026, billing live
- [Google OAuth](google-oauth-verified.md) — Consent screen verified, in production
- [Orbit domain](orbit-domain.md) — orbit.foundryapps.co.uk and orbitlaunches.space
- [Orbit repo path](orbit-repo-path.md) — C:\Users\david\apps\orbit

## Agent Definitions
- [DevOps](agent-devops.md) — Infra, deployments, monitoring, EAS builds
- [QA](agent-qa.md) — Test coverage, production quality
- [Finance](agent-finance.md) — Revenue, cost monitoring, ODPA
- [Marketing](agent-marketing.md) — SEO, content, analytics
- [Reporting](agent-reporting.md) — Reports, scheduled tasks, CEO_STATE.md
- [Orbit Engineering](agent-orbit-engineering.md) — Feature dev, bug fixes, mobile debugging
- [Orbit Data](agent-orbit-data.md) — External APIs, data freshness

## CEO Operations
- [Playbook rules](ceo-playbook-rules.md) — Deployment checklist, repo hygiene, new product setup
- [Role clarity](ceo-role-clarity.md) — Claude manages agents; David gets updates + strategy questions only
- [No operational multiple-choice](feedback-no-operational-multiple-choice.md) — Never present David "option 1/2/3" menus for operational obstacles. Decide, execute, report.
- [Pushback welcome](feedback-pushback-welcome.md) — David explicitly wants counter-arguments on strategy/scope. Evaluate premise first, counter if warranted.
- [Success = shipped to prod](feedback-success-means-shipped.md) — A task is only done when merged AND deployed. PR opened ≠ done. Auto-merge pending ≠ done. Production-green = done.
- [Conflict resolution is per-file](feedback-conflict-resolution-per-file.md) — Never batch "take ours/theirs" across multiple files. Each conflict = independent decision. Shared-package files are usually the PR's real work.
- [Stale worktree EAS builds](feedback-stale-worktree-eas-builds.md) — EAS builds must run from a worktree synced to master, never from long-lived feature-branch worktrees predating a native-config fix.
- [Process rules](process-rules.md) — Scientific debugging, artifact verification, respecting David's time
- [Agent plugins](feedback-agent-plugins.md) — Superpowers v5.0.7 available globally; reference skills by name in code task prompts
- [Dispatch proactive check-ins](feedback-dispatch-proactive-checkins.md) — Don't wait passively for long tasks; send periodic updates so David never has to ask "how's it going"
- [Dispatch timeout handling](feedback-dispatch-timeout-list-sessions.md) — After start_code_task timeout, always list_sessions BEFORE retrying — the session often actually started

## Design Workflow
- [Stitch workflow](stitch-workflow.md) — How to use Google Stitch v2.0 SDK for Orbit web redesigns, ~17% cleanup
- [Design tool split](design-tool-split.md) — Midjourney for heroes, Stitch for layout, vectors for icons — don't overlap

## Mobile Development
- [Mobile publish plan](mobile-publish-plan.md) — Phase 2-5: 3 EAS builds max, local validation first
- [Google Play app](google-play-app.md) — App ID 4973631684995836934, verification pending (identity + phone)
- [First build gate](first-build-gate.md) — New platform targets must have a working production build before feature dev starts
- [Expo token](expo-token.md) — EXPO_TOKEN, project ID 7d839386, owner foundry-apps (refresh if builds fail)
- [EAS build budget](eas-build-budget.md) — Paid plan, limited builds/month — always local pre-flight before cloud submission
- [EAS build learnings](eas-build-learnings.md) — pnpm + Turborepo, GitHub Actions workflow
- [Expo debugging playbook](expo-mobile-debugging-playbook.md) — Metro, caching, source maps, routes, validation pipeline
- [Expo-router monorepo bypass](expo-router-bypass.md) — bypass expo-router/entry with direct require.context in index.js
- [Mobile agent rules](feedback-mobile-agent-learnings-apr10.md) — dev clients, Supabase joins, Play Services gate, focus-aware polling

## Strategic Framing
- [Products are workflow POCs](foundry-products-are-workflow-pocs.md) — Orbit/QuizForge are tests for a reusable anti-generic AI design workflow, not standalone goals
- [New products start with Claude Design PoC](new-product-starts-with-design-poc.md) — Every new product begins with a Claude Design PoC → distilled into canonical design-system.md in the repo, drives all subsequent UI work

## Active Work
- [SDK upgrade complete](sdk-upgrade-progress.md) — Expo 54 merged (PR #333). Next: EAS preview build.
- [Mobile refresh deferred items](mobile-refresh-deferred-items.md) — iOS out of scope; RevenueCat signup + integration after M3; Google Play verification when David's ready
- [Mobile post-UI audit queued](mobile-post-ui-audit-queued.md) — After M3 + UI solid: run business-logic + build-pipeline audit mirroring the 2026-04-19 web audit pattern

## Auto-merge
- [Body bug](auto-merge-body-bug.md) — PR bodies with backticks break auto-merge
- [CI gate](auto-merge-ci-gate.md) — Auto-merge waits for CI checks
