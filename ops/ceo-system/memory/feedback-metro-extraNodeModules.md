---
name: extraNodeModules is a fallback not an override
description: Metro extraNodeModules never overrides packages found via nodeModulesPaths — use pnpm.overrides to force package versions
type: feedback
---

Never use Metro `extraNodeModules` to force a specific package version. It is a **fallback** — Metro only consults it when the package is NOT found via `nodeModulesPaths`. If the package exists anywhere in the normal resolution chain, `extraNodeModules` is never reached.

**Why:** Spent 4 EAS builds trying to pin webidl-conversions to v5 via extraNodeModules. Metro found v8 via nodeModulesPaths every time and never consulted the fallback. The fix only worked when we used `pnpm.overrides` in root package.json, which forces the version at install time before Metro runs.

**How to apply:** To force a package version in a pnpm monorepo, add it to `pnpm.overrides` in root package.json and run `pnpm install` to update the lockfile. For npm use `overrides`, for yarn use `resolutions`. Never rely on Metro config for version pinning.
