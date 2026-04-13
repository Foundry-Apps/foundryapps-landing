---
taskId: daily-ops-report-v2
cronExpression: "0 8 * * 1-5"
schedule: 08:00 UTC weekdays (Mon–Fri)
enabled: true
description: Weekday operational status report sent to david@foundryapps.co.uk
---

## Prompt

Generate a daily operational status report for Foundry Apps. Cover:
1. Orbit production status (up/down, any errors)
2. Recent deployments (PRs merged in last 24h)
3. Any Sentry errors or alerts
4. Data freshness (are launches syncing?)
5. Key metrics if available
6. Blockers or action items

Compile into a concise report. Then send it via the API:

curl -X POST https://orbit.foundryapps.co.uk/api/send-report \
  -H "Authorization: Bearer $CRON_SECRET" \
  -H "Content-Type: application/json" \
  -d '{"to":"david@foundryapps.co.uk","subject":"Foundry Apps Daily Ops Report — [DATE]","body":"[REPORT BODY]","contentType":"text/html"}'

Get the CRON_SECRET from the Orbit .env.local file or Vercel env vars. Format as clean HTML. Send the email — do NOT just create a Gmail draft.
