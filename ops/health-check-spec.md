# Health Check System — Specification

**Status:** Draft
**Author:** DevOps / SRE
**Date:** 2026-03-29
**Applies to:** All Foundry Apps products (Orbit-specific endpoints noted where relevant)

---

## Overview

This document specifies the design of a structured health check system for Foundry Apps products. The system replaces ad-hoc monitoring with a scheduled "health check team" concept: a set of discrete checks against all critical services, producing a categorised management report that distinguishes between issues the agent resolved automatically, issues that require human attention, and informational metrics.

### Goals

- Single daily report covering all external services and internal app health
- Weekly rollup report for trend analysis
- Categorised output (auto-fixed / needs-attention / informational) so the founder can act on reports in under 2 minutes
- Fully automated — no manual triggering required
- Stored in Supabase for history + trend analysis

### Non-goals

- Real-time alerting (not required until paid user base exists; Sentry handles error alerting already)
- User-facing status page (future work)
- Synthetic transaction testing (future work)

---

## Relationship to Existing Scheduled Tasks

The existing `orbit-qa-check` scheduled task is **kept** — it handles periodic quality and functionality checks for the app (e.g. verifying UI flows, data correctness, feature behaviour). The health check system is a **separate concern** focused on infrastructure monitoring and alerting: service uptime, platform status, SSL, DNS, cron data freshness, and alerting configuration. The two systems complement each other and should not be merged.

---

## Architecture

```
Vercel Cron (daily 07:00 UTC)
  └── GET /api/cron/health-check
        ├── Run all health checks in parallel (Promise.all)
        ├── Determine auto-fixable issues → apply fixes
        ├── Build management report (markdown)
        ├── Store report in Supabase health_reports table
        └── Return 200

Vercel Cron (Monday 09:00 UTC)
  └── GET /api/cron/health-summary
        ├── Query last 7 health_reports from Supabase
        ├── Compute trend data (degradation frequency, recurring issues)
        ├── Build weekly summary report
        └── Store in Supabase health_reports (type='weekly')
```

All checks run server-side within a Vercel Function. Results are stored in Supabase. No external alerting service is needed initially.

---

## Services Checked

### 1. App Health — `/api/health`

**What:** HTTP GET to the production app's own health endpoint.
**Auth:** None (public endpoint)

**Health definitions:**

| Status | Condition |
|--------|-----------|
| `healthy` | HTTP 200, response time < 2000ms |
| `degraded` | HTTP 200, response time 2000–5000ms |
| `down` | Non-200 response, timeout, or response time > 5000ms |

**Auto-fix:** None.
**Escalation trigger:** Any non-healthy status.

---

### 2. Vercel Platform Status

**What:** Vercel's public Statuspage.io API.
**URL:** `https://www.vercel-status.com/api/v2/summary.json`
**Auth:** None

**Health definitions:**

| Status | Condition |
|--------|-----------|
| `healthy` | `indicator === "none"` |
| `degraded` | `indicator === "minor"` |
| `down` | `indicator === "major"` or `"critical"` |

**Auto-fix:** None — platform issues are outside our control.
**Escalation trigger:** `degraded` or `down` with active incident affecting deployments or Edge Network.

---

### 3. Vercel Deployment Status

**What:** Latest production deployment state.
**Auth:** `Authorization: Bearer $VERCEL_TOKEN`

**Health definitions:**

| Status | Condition |
|--------|-----------|
| `healthy` | Latest production deployment `readyState === "READY"` |
| `degraded` | Latest deployment is `BUILDING` or `QUEUED` |
| `down` | Latest deployment `readyState === "ERROR"` or `"CANCELED"` |

**Auto-fix:** None.
**Escalation trigger:** `down` (ERROR state).

---

### 4. Supabase Platform Status

**What:** Supabase's public Statuspage.io API.
**URL:** `https://status.supabase.com/api/v2/summary.json`
**Auth:** None

**Health definitions:**

| Status | Condition |
|--------|-----------|
| `healthy` | `indicator === "none"` |
| `degraded` | `indicator === "minor"` |
| `down` | `indicator === "major"` or `"critical"` |

**Auto-fix:** None.
**Escalation trigger:** Any degradation of Database, Auth, or REST API components.

---

### 5. Supabase Project Health

**What:** Per-service health for the Supabase project.
**Auth:** `Authorization: Bearer $SUPABASE_MANAGEMENT_TOKEN`

**Services checked:** `auth`, `db`, `realtime`, `rest`, `storage`

**Health definitions:**

| Status | Condition |
|--------|-----------|
| `healthy` | All services `ACTIVE_HEALTHY` |
| `degraded` | One or more services not `ACTIVE_HEALTHY` but `db` and `rest` are healthy |
| `down` | `db` or `rest` not `ACTIVE_HEALTHY` |

**Auto-fix:** None.
**Escalation trigger:** `db` or `rest` not healthy.

---

### 6. Supabase Data Freshness

**What:** Checks that cron sync jobs are keeping data current.

**Expected freshness thresholds (Orbit):**

| Table | Staleness threshold |
|-------|-------------------|
| `launches` | > 30 minutes |
| `events` | > 90 minutes |
| `astronauts` | > 3 hours |

**Auto-fix:** If data is stale, trigger an immediate re-sync via the cron endpoint.
**Escalation trigger:** `down` state (cron appears to have stopped entirely).

---

### 7. Paddle Billing Status

**What:** Paddle's public Statuspage.io API.
**URL:** `https://status.paddle.com/api/v2/summary.json`
**Auth:** None

**Auto-fix:** None.
**Escalation trigger:** Production - Billing degraded or down.

---

### 8. Sentry Error Monitoring

**What:** Sentry platform status + unresolved error count.
**Auth:** `Authorization: Bearer $SENTRY_AUTH_TOKEN`

**Health definitions — error rate:**

| Status | Condition |
|--------|-----------|
| `healthy` | Unresolved issues ≤ 5, no new issues in past 24h |
| `degraded` | 6–20 unresolved issues, or any issue with `firstSeen` in past 24h |
| `down` | > 20 unresolved issues, or any `level === "fatal"` issue in past 24h |

**Auto-fix:** None.
**Escalation trigger:** Any fatal-level issue; any new issue spike (> 5 new in 24h).

---

### 9. GitHub CI/CD Status

**What:** GitHub platform status + auto-merge workflow health.
**Auth:** `Authorization: Bearer $GITHUB_HEALTH_TOKEN`

**Health definitions — workflow:**

| Status | Condition |
|--------|-----------|
| `healthy` | Last 3 workflow runs all `conclusion === "success"` |
| `degraded` | 1 of last 3 runs failed |
| `down` | 2+ of last 3 runs failed, or last run failed |

**Auto-fix:** None.
**Escalation trigger:** `down` state (PR deployments are broken).

---

### 10. SSL Certificate

**How:** Node.js `tls.connect()` to inspect certificate expiry.

**Health definitions:**

| Status | Condition |
|--------|-----------|
| `healthy` | Certificate valid, expires > 30 days |
| `degraded` | Certificate valid, expires 7–30 days |
| `down` | Certificate expired, invalid, or hostname mismatch |

**Auto-fix:** None — certificate renewal is handled by Vercel automatically.
**Escalation trigger:** `degraded` (< 30 days) or `down`.

---

### 11. DNS Health

**How:** Node.js `dns.promises.resolveCname()` — runs server-side.

**Expected:** `<product-domain>` CNAME → `cname.vercel-dns.com`

**Auto-fix:** None.
**Escalation trigger:** Any non-healthy status.

---

### 12. Alerting Verification

**What:** Verifies that alerting configuration is in place across all systems.

Sub-checks:
- **12a. Vercel Notifications** — at least one active notification webhook
- **12b. Supabase Resource Alerts** — at least one resource alert enabled (disk, CPU, memory)
- **12c. Sentry Alert Rules** — at least one enabled alert rule
- **12d. Cloudflare Security Alerts** — at least one enabled security alert policy
- **12e. GitHub Dependabot + Secret Scanning** — both enabled

If any token is missing, that sub-check reports "unable to check — token not configured" (informational, not a failure).

---

## Escalation Tiers

| Tier | Condition | Response | Push notification? |
|------|-----------|----------|-------------------|
| **P1 — Critical** | App down, database down, SSL expired, DNS broken | Immediate — check within 1 hour | Yes — Dispatch |
| **P2 — High** | Vercel deployment ERROR, Supabase db/rest unhealthy, GitHub Actions broken | Same day — check within 4 hours | No |
| **P3 — Medium** | SSL expiring < 30 days, cron data stale after auto-fix, Sentry fatal errors, Paddle production degraded | Next business day | No |
| **P4 — Low** | Platform minor degradation, Sentry new issues, deployment > 14 days old, alerting not configured | Review at next weekly summary | No |

---

## New Environment Variables Required

| Variable | Purpose |
|----------|---------|
| `SUPABASE_MANAGEMENT_TOKEN` | Supabase project health endpoint + resource alerts |
| `SENTRY_AUTH_TOKEN` | Sentry issues API + alert rules (scope: `project:read`) |
| `SENTRY_ORG_SLUG` | Sentry org identifier |
| `GITHUB_HEALTH_TOKEN` | GitHub Actions API + repo security settings (scope: `repo:read`) |
| `CLOUDFLARE_API_TOKEN` | Cloudflare notification policies (scope: `Zone:Notifications:Read`) |

All new checks degrade gracefully if tokens are missing.

---

## Scheduled Task Configuration

```json
{ "path": "/api/cron/health-check", "schedule": "0 7 * * *" },
{ "path": "/api/cron/health-summary", "schedule": "0 9 * * 1" }
```

**Daily health check:** 07:00 UTC — catches overnight issues before the working day.
**Weekly summary:** 09:00 UTC Monday — start-of-week rollup report.
