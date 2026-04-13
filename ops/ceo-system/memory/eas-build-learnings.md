---
name: EAS build monorepo learnings
description: Critical lessons from EAS Android builds — npm/yarn issues resolved by pnpm migration, Metro resolution gotchas
type: feedback
---

npm workspaces + Expo monorepo = fundamental friction. After 14 distinct issues across 350+ build attempts, the repo migrated to pnpm 9.15.9 + Turborepo (April 2026). EAS builds now work via GitHub Actions workflow.

**Why:** npm's hoisting strategies all caused problems with Expo's dependency resolution. pnpm's strict node_modules structure resolved these.

**How to apply:**
- Repo now uses pnpm — all commands should use `pnpm` not `yarn` or `npm`
- EAS builds triggered automatically via GitHub Actions on master push (workflow: `.github/workflows/mobile-build.yml`)
- Manual dispatch: use GitHub API `POST /repos/Foundry-Apps/orbit/actions/workflows/mobile-build.yml/dispatches` with `ref: master`
- Auto-merge pushes via GITHUB_TOKEN don't trigger other workflows — must manually dispatch EAS build after merge
- Never delete root lockfile (`pnpm-lock.yaml`) — only root should have one
- EAS `eas.json` rejects empty `env: {}` blocks — remove them
- Only list actually installed config plugins in `app.json` plugins array
- Expo owner field must match exactly (`foundry-apps` not `foundryapps`)
- Always delete `apps/mobile/package-lock.json` — only root should have a lockfile
- pnpm patchedDependencies removed (9 Apr 2026) — whatwg-url-without-unicode no longer a dependency
- react-native-url-polyfill removed — Hermes 0.76+ has native URL support
- `pnpm install` in CI uses `--frozen-lockfile` by default (CI env var set) — lockfile must exactly match package.json config

Full post-mortem: `docs/MOBILE-BUILD-ISSUES.md` (PR #167)
