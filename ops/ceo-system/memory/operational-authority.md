---
name: Operational Authority
description: David has granted full access to manage Supabase and Vercel settings including env vars, without needing approval
type: feedback
---

David confirmed (April 4, 2026) that I have full authority to add/modify environment variables and complete any administrative actions on both Supabase and Vercel without escalating to him.

**Why:** Previously CLAUDE.md required escalation for "adding third-party services or integrations" and "any commitment with financial cost." David clarified that managing existing infrastructure settings (env vars, connection pooler, build config) does not require approval.

**How to apply:** When a new API integration needs an env var added to Vercel, or a Supabase setting needs changing (connection pooler, RLS policies, migrations), proceed directly. Only escalate for new paid service subscriptions or architectural changes.

Specific platforms with full access:
- Supabase (Pro plan): migrations, RLS, connection pooler, extensions, env vars
- Vercel (Pro plan): env vars, domain config, build settings, deployment management
- Cloudflare: DNS records
- GitHub (Foundry-Apps org): repos, workflows, PRs
