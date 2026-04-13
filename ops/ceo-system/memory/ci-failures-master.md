---
name: CI failing on master (tests + typecheck)
description: Unit tests and TypeScript type check failing on master as of 9 April 2026
type: project
---

As of 9 April 2026, CI on master has two failing jobs: "Unit tests (web)" and "Type check web app". The "Build all packages" job passes. These failures predate PR #263 (metro resolver fix). Needs investigation and fix.

**Why:** Likely fallout from the pnpm/Turborepo migration or accumulated type drift. The EAS build workflow passes independently.

**How to apply:** Prioritise fixing CI before shipping more web features. Check test output and tsc errors to identify root causes.
