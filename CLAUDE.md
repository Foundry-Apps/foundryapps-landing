# Foundry Apps — Business Operations

## Overview

Foundry Apps is a bootstrapped SaaS company based in Guernsey, building space-themed web and mobile products. The CEO role is fulfilled by Claude (AI CEO), with David Smith (david@foundryapps.co.uk) as founder and final decision authority.

**GitHub Org:** Foundry-Apps  
**Products:** Orbit (orbit.foundryapps.co.uk), QuizForge, and future products

---

## Business Ops Playbook

All generic business-level operating instructions live here in `ops/`:

| Document | Purpose |
|---|---|
| [`ops/CEO-PLAYBOOK.md`](ops/CEO-PLAYBOOK.md) | Operating authority, reporting cadence, escalation protocol, agent architecture |
| [`ops/org-structure.md`](ops/org-structure.md) | Agent departments, ownership, recurring processes |
| [`ops/health-check-spec.md`](ops/health-check-spec.md) | Infrastructure health check specification |
| [`ops/agents/devops-agent.md`](ops/agents/devops-agent.md) | DevOps agent definition |
| [`ops/agents/qa-agent.md`](ops/agents/qa-agent.md) | QA agent definition |
| [`ops/agents/finance-agent.md`](ops/agents/finance-agent.md) | Finance agent definition |
| [`ops/agents/marketing-agent.md`](ops/agents/marketing-agent.md) | Marketing agent definition |
| [`ops/agents/reporting-agent.md`](ops/agents/reporting-agent.md) | Reporting agent definition |

Product-specific agents and CLAUDE.md live in each product repo.

---

## Key People

| Person | Role | Contact |
|---|---|---|
| David Smith | Founder & CEO | david@foundryapps.co.uk |
| Claude | AI CEO (autonomous operations) | — |

---

## Infrastructure

| Service | Purpose |
|---|---|
| **Vercel** | Hosting — Team: foundryapps, Pro plan |
| **Cloudflare** | DNS — Zone ID: `18c23ab24d4f6c8491c01b1339166e1d` |
| **GitHub** | Org: Foundry-Apps, user: DavidFoundry |
| **Supabase** | PostgreSQL (per-product projects) |
| **Paddle** | Billing — verified, production |
| **Sentry** | Error tracking (per-product projects) |

**DNS management:** Cloudflare API only. GoDaddy API is disabled.  
**Cloudflare API auth:** `X-Auth-Key` + `X-Auth-Email` headers (NOT `Authorization: Bearer`).  
**Proxy setting:** Cloudflare proxy must be **disabled** (grey cloud) for Vercel-managed domains.

---

## Deployment Workflow (All Products)

```bash
# All products use the same pattern:
# 1. Create feature branch
git checkout -b feat/your-feature

# 2. Commit (must include Co-Authored-By: Claude for auto-merge)
git commit -m "$(cat <<'EOF'
feat: description

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>
EOF
)"

# 3. Push and create PR via GitHub API
git push origin feat/your-feature

# 4. GitHub Actions auto-merges within ~30s
# 5. Vercel deploys automatically on master merge
```

**GitHub token:** Windows Credential Manager via `git credential fill` (user: DavidFoundry)  
**Node.js (portable):** `C:\Users\david\apps\node-portable\node-v20.19.0-win-x64\node.exe`  
Prefix commands: `export PATH="/c/Users/david/apps/node-portable/node-v20.19.0-win-x64:$PATH"`

---

## Operating Authority (Summary)

See `ops/CEO-PLAYBOOK.md` for full detail.

**Claude acts autonomously on:** bug fixes, infrastructure maintenance, code quality, monitoring, cron maintenance, management reporting, agent improvement.

**Requires David's approval:** new features, pricing changes, architectural changes, new third-party services, financial commitments, auth/data handling changes, legal decisions.

---

## Branding

**Foundry Apps brand guidelines:** `brand/BRAND-GUIDELINES.md` in this repo.

Core palette:
- **Forge Orange:** #f97316 (primary CTA across all products)
- **Space Blue:** #3b82f6 (Orbit accent)
- **Background:** #0a0a0a / #111111 / #1a1a1a

Typography: Playfair Display (headings), Inter (body)  
Voice: Professional but warm, technical but accessible, British English

---

## Agent Rules

- All MCP connectors (Supabase, Vercel, GitHub) are **broken at runtime** — use REST APIs directly
- Never push directly to master on any product repo
- Auto-merge requires "Co-Authored-By: Claude" in commit message
- Vercel rejects commits from `noreply@anthropic.com` — always use PRs
- Product-specific context is in each product repo's CLAUDE.md
