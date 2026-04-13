---
name: Google OAuth Production Ready
description: Google OAuth consent screen verified and published to production — no user cap, no verification needed
type: project
---

Confirmed April 4, 2026: Google OAuth is fully production-ready.

- **GCP Project**: foundry-apps-admin
- **Publishing status**: In production
- **User type**: External
- **Branding status**: Verified and shown to users
- **Data access status**: Verification not required (only email + profile scopes)
- **User cap**: 100 cap does NOT apply because we use only non-sensitive scopes

**Why:** Was previously listed as a blocker in CLAUDE.md ("Google OAuth: Currently test mode, 100 user limit"). This is resolved — no limits on production usage.

**How to apply:** Remove the Google OAuth blocker from CLAUDE.md "WAITING ON / BLOCKERS" section. Auth flow supports email/password, Google OAuth, and Apple Sign-In (iOS). All three are production-ready.
