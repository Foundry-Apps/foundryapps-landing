# Foundry Apps — CEO State (Last Updated: 30 March 2026)

## Active Products

### Orbit (Space Mission Tracker)
- **Status:** Live at orbit.foundryapps.co.uk
- **Branch:** master
- **Recent changes:** Rate limiting on all API routes, dashboard content widgets, launch detail pages, per-launch notification subscriptions
- **Pending:** Paddle verification (~1-2 April), Vercel Pro payment activation needed
- **Monitoring:** Daily health checks, weekly infra reviews running via scheduled tasks
- **Google OAuth:** Confirmed in production, branding verified

### QuizForge (Pub Quiz Platform) — NEW
- **Status:** Planning complete, repo created
- **Repo:** https://github.com/Foundry-Apps/quizforge (private, master branch)
- **Local:** C:\Users\david\apps\quizforge
- **Strategy:** Consumer-first (solo quiz + gamification + teams), then B2B venue platform after consumer validation
- **Plan:** docs/PLAN.md in the quizforge repo — 13 sections, full technical spec
- **Phase 0 start:** Week of 7 April
- **Phase 1 target:** Late May 2026 (consumer app live)
- **Key dependency:** 500+ quiz questions needed before launch

## Infrastructure

- **GitHub Org:** Foundry-Apps (repos: orbit, quizforge, foundryapps-landing)
- **Vercel:** Team slug `foundry-apps`, Pro plan (payment activation pending)
- **Supabase:** Org `veenppgkjnijwlhfbbte`, EU-West-1, ref `ujssnmrpxmbujmfugsug` (Orbit)
- **Cloudflare:** Zone ID `18c23ab24d4f6c8491c01b1339166e1d`
- **Paddle:** £4.99/month, £49/year for Orbit; verification pending
- **Sentry:** Project "orbit", ID 4511127032234064
- **ODPA:** Registration DPA11561

## Brand Guidelines
- Master brand + sub-brand guidelines in `brand/` directory of this repo
- SVG logos, CSS tokens, AI image prompts, visual preview page
- Both Orbit and QuizForge CLAUDE.md files reference these guidelines

## Scheduled Tasks
- daily-health-check, weekly-infra-review, daily-briefing, daily-ops-report
- site-monitor, orbit-qa-check, weekly-strategy-report
- launch-readiness, weekly-ceo-brief, knowledge-base-sync

## David's Location
- Orlando holiday: 30 March - 14 April 2026
- Standing mandate: Claude handles operational bug fixes without approval

## Next Actions (Week of 30 March)
1. Continue Orbit operations (monitoring, health checks, bug fixes)
2. Housekeeping: clean up Orbit worktrees, close stale PR #51
3. Begin QuizForge Phase 0 preparation

## Next Actions (Week of 7 April)
1. Begin QuizForge Phase 0 (repo scaffolding, infrastructure)
2. Start question content generation (50 questions/day target)
3. Set up new Supabase project for QuizForge
4. Set up Paddle consumer Pro product (£2.99/mo, £29.99/yr)
5. Configure Vercel project and DNS for quiz.foundryapps.co.uk

## Stale Items
- PR #51 on Orbit: duplicate of rate limiting PR, being closed
- CEO state doc previously on Orbit branch — now moved here
