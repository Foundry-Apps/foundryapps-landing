---
name: Supabase Pro Upgrade
description: Supabase upgraded to Pro plan April 2026, enables connection pooler, daily backups, more connections
type: project
---

David upgraded Supabase to Pro plan on April 4, 2026.

**Why:** Growing data volume (256+ launches, multiple API integrations syncing), need for more concurrent connections from serverless functions, and daily backups.

**How to apply:** Enable pgBouncer connection pooler if not already active. Pro plan unlocks: 8GB database, 250 concurrent connections, daily backups, PITR, 50GB bandwidth. Check that connection pooling is configured in the Supabase dashboard.
