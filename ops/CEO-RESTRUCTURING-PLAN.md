# Foundry Apps — CEO Restructuring Plan

**Date:** 9 April 2026
**Author:** Claude CEO
**Status:** DRAFT — Pending David's review
**Gate:** Mobile app Phase 5 complete (store submission)

---

## 1. Purpose

This plan defines how Foundry Apps transitions from the current model — where David handles significant operational work and Claude acts as a task executor with CEO-level CLAUDE.md instructions — to a fully autonomous CEO model where Claude runs day-to-day operations through specialist agents, and David's involvement is limited to strategic decisions, vision, and critical escalations.

The plan covers four pillars:
1. Separate business logic from project logic
2. Define and deploy agentic employees
3. Establish periodic review cadence
4. Shift the interaction model

---

## 2. Business Logic Separation

### Problem

Currently, the Orbit repo contains both Orbit-specific product logic AND generic business operations. The CLAUDE.md file is 1,000+ lines mixing product architecture with operational patterns. When Foundry Apps launches a second product, there's no reusable operational layer to build on.

### What moves where

**Stay in each product repo (product-specific):**
- Product CLAUDE.md (tech stack, routes, data model, design tokens, deploy workflow)
- Application code
- Database migrations and schema
- Product-specific cron jobs (launch sync, data refresh)
- `docs/ARCHITECTURE.md`, `docs/TECHNICAL-NOTES.md`
- `.claude/CEO_STATE.md` (product state only)
- Product-specific agent definitions (e.g. `orbit-engineering-agent.md`, `orbit-data-agent.md`)

**Live in foundryapps-landing (business-level):**
- `ops/CEO-PLAYBOOK.md` — operating authority, reporting cadence, escalation protocol
- `ops/org-structure.md` — 7-department model (applies to any product)
- `ops/health-check-spec.md` — monitoring architecture, escalation tiers
- `ops/agents/` — generic business agent definitions (DevOps, QA, Finance, Marketing, Reporting)
- `ops/CEO-RESTRUCTURING-PLAN.md` — this file
- New project setup standard
- Token efficiency rules
- Management reporting templates and cadence
- Memory system policies

### Implementation

Phase A — Create the business-level ops structure: ✅ DONE
1. Created `foundryapps-landing/ops/` with CEO-PLAYBOOK.md, org-structure.md, health-check-spec.md
2. Created 5 generic agent definition files
3. Created business-level `CLAUDE.md` in foundryapps-landing
4. Moved generic docs from Orbit to foundryapps-landing

Phase B — Slim down Orbit's CLAUDE.md:
1. Remove all generic business operations content
2. Remove stale LESSONS LEARNED entries (keep only Orbit-specific ones)
3. Target: under 500 lines, purely Orbit product context
4. Add a pointer to foundryapps-landing for generic rules

Phase C — Validate:
1. Start a fresh Claude session with only the slimmed Orbit CLAUDE.md
2. Verify it can still ship a feature end-to-end
3. Start a fresh session with the business-level CLAUDE.md
4. Verify it understands reporting, monitoring, and operational duties

---

## 3. Agentic Employees

### Design Principles

- Agents are defined at the **business level** unless they need product-specific context
- Each agent has: a role description, owned files/systems, recurring processes, escalation criteria
- When an agent fails, **fix the agent** (improve its instructions, tooling, or context) — not just the specific issue
- Agents should be composable: the CEO coordinates them, not micromanages them

### Agent Roster

#### Business-Level Agents (in foundryapps-landing/ops/agents/)

1. **DevOps Agent** — Infrastructure reliability, deployment pipeline, monitoring
2. **QA Agent** — Test coverage, production quality, regression detection
3. **Finance & Compliance Agent** — Revenue tracking, cost monitoring, regulatory compliance
4. **Marketing & Growth Agent** — SEO, content, analytics, user acquisition
5. **Reporting Agent** — Generate and deliver management reports

#### Product-Level Agents (defined per product repo)

6. **Orbit Engineering Agent** — Feature development, bug fixes, code quality for Orbit
7. **Orbit Data Agent** — External API integrations, data freshness, sync reliability

### Agent Implementation

Agents aren't separate running processes — they're **instruction sets** that Claude loads contextually. Each agent is a markdown file with:

```
# Agent: [Name]
## Role
## Owned files and systems
## Recurring processes (with cron-style schedule)
## Decision authority (what it can do without escalation)
## Escalation criteria (when to involve CEO or David)
## Tooling requirements
## Success metrics
```

---

## 4. Periodic Structure Review

### Monthly Review (CEO self-audit)
- Are all agents producing their recurring outputs on schedule?
- Are escalation criteria still calibrated correctly?
- Is the business-level CLAUDE.md still accurate?
- Are memory files current? Any stale entries?
- Are scheduled tasks still producing value?

### Quarterly Review (present to David)
- Portfolio performance: revenue, costs, growth trajectory
- Agent effectiveness: which agents are working well, which need improvement
- Tooling audit: are we using the right tools?
- Strategic alignment: are we building the right things?

---

## 5. Interaction Model

### Target Model

**David handles:**
- Strategic vision and direction
- Go/no-go on new product launches and major features
- Legal/compliance decisions
- Critical escalations

**Claude handles (autonomously):**
- All day-to-day development and operations
- Bug fixes, infrastructure maintenance, dependency updates
- Monitoring, alerting, incident response (within guardrails)
- Management reporting (delivered to David's email)
- Agent creation, improvement, and coordination

---

## 6. Success Criteria

The restructuring is complete when:
1. Orbit CLAUDE.md is <500 lines and contains only product context
2. Business-level ops repo has agent definitions for all 7 roles
3. Claude can ship a bug fix, deploy, verify, and report — without any David involvement
4. Weekly CEO brief arrives in David's inbox with actionable content
5. A new product (e.g., QuizForge) can be spun up using the business-level playbook without duplicating operational logic
6. David's involvement is genuinely limited to strategic decisions for 2+ consecutive weeks

---

## 7. Risks

- **Context window limits:** Agent definitions add tokens. May need to be selective about which agents are loaded per session.
- **Stale agents:** Agent definitions will drift if not reviewed. Monthly self-audit mitigates this.
- **Over-autonomy:** Claude making decisions David would want input on. Escalation criteria must be well-calibrated.
- **Tool limitations:** Some operations still require David (e.g., Apple Developer account setup, bank transfers). These should be explicitly listed as David-only actions.

---

## 8. Current State Baseline

As of 9 April 2026:
- 1 live product (Orbit web app)
- 1 in-progress mobile app (Phase 2 — build verification)
- 1 dormant product (QuizForge)
- 12 scheduled tasks
- Revenue: Pro subscriptions live via Paddle (£4.99/mo, £49/yr)
- Infrastructure: Supabase Pro, Vercel Pro, Cloudflare, Sentry
