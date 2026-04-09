# Foundry Apps Agent Organisation Structure

## Overview

Foundry Apps operates with a multi-agent architecture organised into 7 functional departments. Each department has a dedicated mission, owns specific data and workflows, and reports on a defined cadence. All agents run within the Claude Code CEO framework — a master CEO agent coordinates cross-department work and handles escalations.

---

## Departments

### 1. Engineering

**Mission:** Build, maintain, and improve product codebases. Ensure code quality, test coverage, and architectural integrity.

**Ownership:**
- Application source code
- Test suites (Vitest unit tests and Playwright E2E)
- Database migrations
- Build configuration

**Recurring Processes:**
- Review and merge PRs (auto-merge enabled for CEO agent PRs)
- Run test suite before any deploy
- Refactor and technical debt reduction
- Dependency updates

**Execution Environment:** Worktree sandbox (never master directly)

**Scheduled Outputs:**
- Daily: Engineering health summary (build status, test pass rate, open PRs)
- Weekly: Engineering summary (features shipped, debt addressed, blockers)

---

### 2. DevOps / SRE

**Mission:** Maintain deployment pipeline, infrastructure reliability, observability, and incident response.

**Ownership:**
- Vercel project configuration
- Sentry error tracking
- Supabase project settings
- GitHub Actions workflows (`.github/workflows/`)
- Cron job definitions

**Recurring Processes:**
- Monitor Vercel deployments
- Review Sentry error reports
- Manage environment variables (via Vercel REST API)
- Cron job health checks
- Incident triage and postmortem

**Execution Environment:** Host environment (Vercel REST API, Supabase REST API — MCPs broken)

**Scheduled Outputs:**
- Daily: Production health report (uptime, error rate, deploy status)
- Weekly: Infrastructure summary (costs, performance, incidents)
- Monthly: Infrastructure review (scaling decisions, cost optimisation)

**Key Configuration:**
- Vercel team: `foundry-apps`
- Auto-merge workflow: `.github/workflows/auto-merge.yml`

---

### 3. Product

**Mission:** Define product direction, manage feature roadmap, and translate user needs into engineering requirements.

**Ownership:**
- Feature specifications
- Freemium access pattern — free-tier content ungated; Pro gating via product-specific mechanisms
- UX decisions and design tokens
- Roadmap prioritisation

**Recurring Processes:**
- Review user feedback and support tickets
- Write feature specs before engineering picks up work
- Validate shipped features against spec
- Freemium funnel analysis

**Execution Environment:** Agent (research + spec writing), browser (UI validation)

**Scheduled Outputs:**
- Weekly: Product brief (what shipped, what's next, key decisions)
- Monthly: Product review (roadmap progress, conversion metrics, user feedback themes)
- Quarterly: Strategic review (market position, roadmap reset)

---

### 4. Growth / Marketing

**Mission:** Drive user acquisition, conversion to Pro, and retention. Manage public presence and SEO.

**Ownership:**
- Landing page copy
- SEO metadata
- Social media (if applicable)
- Email sequences (billing-triggered)

**Recurring Processes:**
- Monitor signup and conversion metrics
- A/B test upgrade prompts
- Content calendar (product-relevant news tie-ins)
- Referral and launch campaign management

**Execution Environment:** Agent (research, copy drafting), browser (analytics dashboards)

**Scheduled Outputs:**
- Weekly: Growth metrics (signups, Pro conversions, churn)
- Monthly: Marketing report (channel performance, content published, SEO rankings)
- Quarterly: Competitive brief (market landscape, positioning)

---

### 5. Finance / Billing

**Mission:** Manage revenue operations, Paddle billing integration, and financial reporting.

**Ownership:**
- Paddle integration and webhook handlers
- Pro/paid status flag lifecycle (grant/revoke on Paddle events)
- Revenue reporting
- Pricing decisions

**Recurring Processes:**
- Reconcile Paddle webhooks with subscription state
- Monitor failed payments and dunning
- Monthly revenue close
- Paddle tax/VAT compliance (Guernsey jurisdiction)

**Execution Environment:** Agent (reporting), host (Supabase REST API for billing queries)

**Scheduled Outputs:**
- Daily: Revenue snapshot (MRR, new subs, churned)
- Monthly: Financial statements (MRR, ARR, churn rate, LTV)
- Quarterly: Financial review

**Current Status:** Paddle production verified (April 2026) — billing fully operational.

---

### 6. Legal / Compliance

**Mission:** Ensure all products operate within legal requirements for Guernsey jurisdiction. Maintain privacy, terms, and cookie policies.

**Ownership:**
- Legal pages (privacy, terms, cookies)
- ODPA (Guernsey data protection) compliance
- OAuth consent flows
- Cookie banner and consent management

**Recurring Processes:**
- Review policy pages against regulatory changes
- Audit data flows for ODPA compliance
- Review third-party integrations for data processing agreements

**Execution Environment:** Agent (research, drafting)

**Scheduled Outputs:**
- Quarterly: Compliance review (ODPA, cookie policy, third-party DPAs)

**Current Status:**
- Legal pages updated for Guernsey jurisdiction (complete)
- ODPA registration: DPA11561

---

### 7. Customer Support

**Mission:** Respond to user issues, manage Pro subscription problems, and feed insights back to Product.

**Ownership:**
- Support inbox / contact channel
- Known issues documentation
- User-facing status page (if applicable)

**Recurring Processes:**
- Triage support requests
- Handle Pro billing issues (Paddle customer portal)
- Escalate bugs to Engineering
- Summarise feedback themes for Product

**Execution Environment:** Agent (drafting responses), browser (Paddle dashboard for billing issues)

**Scheduled Outputs:**
- Weekly: Support summary (volume, top issues, escalations)
- Monthly: Voice of customer (themes, sentiment, feature requests)

---

## Cross-Department Workflows

### Feature Lifecycle

```
Product (spec) → Engineering (build in worktree) → DevOps (deploy via PR→merge)
→ Growth (announce) → Support (field questions) → Product (measure)
```

1. Product writes a spec in GitHub issue or PR description
2. Engineering creates a feature branch from master, implements in worktree
3. All code changes go via PR → auto-merge → Vercel deploys to production
4. Growth updates any relevant marketing copy or launch comms
5. Support monitors for user issues post-launch
6. Product reviews metrics after 1–2 weeks

### Incident Response

```
DevOps (detect via Sentry/Vercel) → Engineering (hotfix in worktree)
→ DevOps (expedited deploy) → Support (user comms) → Engineering (postmortem)
```

1. Sentry alert or Vercel deployment failure triggers incident
2. DevOps assesses severity; P1 = immediate Engineering page
3. Engineering creates hotfix branch, fixes, and opens PR
4. Merge → Vercel auto-deploys
5. Support drafts any user-facing communication
6. Engineering writes postmortem; DevOps updates runbooks

### User Feedback Loop

```
Support (collect) → Product (synthesise) → Engineering (prioritise) → repeat
```

### Revenue Operations

```
Paddle webhook → DB (status update) → Finance (reconcile)
→ Growth (analyse conversion) → Product (pricing decisions)
```

### Compliance Gate

Before any new data collection or third-party integration:
```
Legal (review) → Engineering (implement consent/DPA) → Legal (sign-off) → DevOps (deploy)
```

---

## Reporting Cadence

### Daily
| Report | Owner | Contents |
|--------|-------|----------|
| Production health | DevOps | Uptime, error rate, deploy status, cron health |
| Revenue snapshot | Finance | MRR, new subs, churned, failed payments |

### Weekly
| Report | Owner | Contents |
|--------|-------|----------|
| CEO brief | CEO agent | Cross-department summary, blockers, decisions needed |
| Engineering summary | Engineering | Features shipped, PRs merged, test coverage, open issues |
| Product brief | Product | Roadmap progress, shipped features, upcoming priorities |
| Growth metrics | Growth | Signups, conversions, churn, top acquisition channel |
| Support summary | Support | Ticket volume, top issues, escalations, feedback themes |

### Monthly
| Report | Owner | Contents |
|--------|-------|----------|
| Financial statements | Finance | MRR, ARR, churn, LTV, Paddle reconciliation |
| Infrastructure review | DevOps | Costs, performance trends, scaling decisions |
| Marketing report | Growth | Channel performance, content, SEO |
| Competitive brief | Growth/Product | Market landscape, positioning |
| Voice of customer | Support/Product | Feedback themes, NPS (if tracked), feature requests |

### Quarterly
| Report | Owner | Contents |
|--------|-------|----------|
| Compliance review | Legal | ODPA status, policy updates, DPA audit |
| Financial review | Finance | Quarterly P&L, budget vs actuals |
| Strategic review | CEO/Product | Roadmap reset, market position, OKRs |

---

## Tool Routing Table

| Department | Task Type | Preferred Tool |
|-----------|-----------|---------------|
| Engineering | Code changes | Worktree sandbox + Edit/Write tools |
| Engineering | DB schema | Supabase REST API directly |
| Engineering | Git/GitHub | `curl` + `git credential fill` |
| DevOps | Deploy management | Vercel REST API directly |
| DevOps | Env vars | Vercel REST API directly |
| DevOps | Error monitoring | Sentry (browser, last resort) |
| Finance | Billing queries | Supabase REST API directly |
| Finance | Paddle management | Browser (Paddle dashboard) |
| Legal | Policy research | Agent (WebSearch) |
| Growth | Analytics | Browser (Vercel Analytics) |
| All | Research tasks | Agent (WebSearch/WebFetch) |
| All | File operations | Read/Write/Edit tools |

---

## Disaster Recovery

All operational state is stored in git:

- **Code**: GitHub repositories under Foundry-Apps org
- **Operational docs**: `foundryapps-landing/ops/` (this folder)
- **Claude config**: `.claude/` per repo (settings, CEO state)
- **DB schema**: `supabase/migrations/` in product repos
- **Secrets**: Vercel environment variables (not in git)

**Recovery procedure:** Any new agent session should:
1. Read the relevant product repo `CLAUDE.md` for product context
2. Read `foundryapps-landing/ops/CEO-PLAYBOOK.md` for operating authority and processes
3. Read `foundryapps-landing/ops/org-structure.md` (this file) for the full operating model
4. Read `.claude/CEO_STATE.md` in the product repo for latest state
