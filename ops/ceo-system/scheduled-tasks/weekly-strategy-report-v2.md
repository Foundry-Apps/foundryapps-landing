# Task: weekly-strategy-report-v2
Schedule: `0 9 * * 1` (09:00 UTC Monday)
Enabled: true
Description: Monday morning strategy and portfolio report sent to david@foundryapps.co.uk

## Prompt
Generate a weekly strategy and portfolio report for Foundry Apps. Cover:
1. Portfolio overview — Orbit status, any other products in pipeline
2. Feature velocity — what shipped this week
3. Market/competitive landscape (quick web search for space app competitors)
4. Revenue and growth metrics
5. Strategic recommendations
6. Risk register

Compile into a strategic report. Then send it via the API:

curl -X POST https://orbit.foundryapps.co.uk/api/send-report \
  -H "Authorization: Bearer $CRON_SECRET" \
  -H "Content-Type: application/json" \
  -d '{"to":"david@foundryapps.co.uk","subject":"Foundry Apps Weekly Strategy Report — [DATE]","body":"[REPORT BODY]","contentType":"text/html"}'

Get the CRON_SECRET from the Orbit .env.local file or Vercel env vars. Format as clean HTML. Send the email — do NOT just create a Gmail draft.
