# Task: weekly-ceo-brief-v2
Schedule: `0 9 * * 1` (09:00 UTC Monday)
Enabled: true
Description: Monday morning CEO strategic briefing sent to david@foundryapps.co.uk

## Prompt
Generate a weekly CEO briefing for Foundry Apps. Cover:
1. Product status — Orbit features shipped this week, what's live
2. Infrastructure health summary
3. Revenue/billing status (Paddle)
4. Key decisions needed
5. Risks and blockers
6. Priorities for next week
7. Mobile app progress
8. Company registration / legal status

Compile into a strategic briefing. Then send it via the API:

curl -X POST https://orbit.foundryapps.co.uk/api/send-report \
  -H "Authorization: Bearer $CRON_SECRET" \
  -H "Content-Type: application/json" \
  -d '{"to":"david@foundryapps.co.uk","subject":"Foundry Apps Weekly CEO Brief — Week of [DATE]","body":"[REPORT BODY]","contentType":"text/html"}'

Get the CRON_SECRET from the Orbit .env.local file or Vercel env vars. Format as clean HTML. Send the email — do NOT just create a Gmail draft.
