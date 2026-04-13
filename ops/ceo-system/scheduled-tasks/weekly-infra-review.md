# Task: weekly-infra-review
Schedule: `0 9 * * 1` (09:00 UTC Monday)
Enabled: true
Description: Weekly Monday infrastructure review with alerting verification

## Prompt
Run a weekly infrastructure review for Foundry Apps. Check:
1. Vercel deployment health and build times
2. Supabase database stats (table sizes, connection pool, RLS status)
3. Cloudflare DNS and SSL status
4. Sentry error rates for the past week
5. Cron job health (are all sync jobs running?)
6. Dependency updates available (check for security advisories)
7. Alerting verification — confirm monitoring is active

Compile into an infrastructure report. Then send it via the API:

curl -X POST https://orbit.foundryapps.co.uk/api/send-report \
  -H "Authorization: Bearer $CRON_SECRET" \
  -H "Content-Type: application/json" \
  -d '{"to":"david@foundryapps.co.uk","subject":"Foundry Apps Weekly Infra Review — [DATE]","body":"[REPORT BODY]","contentType":"text/html"}'

Get the CRON_SECRET from the Orbit .env.local file or Vercel env vars. Format as clean HTML. Send the email — do NOT just create a Gmail draft.
