---
taskId: daily-health-check
cron: "0 7 * * *"
schedule: 07:00 daily (UTC)
enabled: true
description: Daily health check of Orbit production infrastructure
---

# daily-health-check

Run a daily health check of Orbit production infrastructure. Check:
1. Site availability: curl https://orbit.foundryapps.co.uk and verify HTTP 200 with content
2. SSL/TLS: verify certificate is valid
3. DNS: verify orbit.foundryapps.co.uk, foundryapps.co.uk, orbitlaunches.space all resolve
4. Latest Vercel deployment status
5. Supabase health (check if data is fresh — recent launches synced)
6. Any open GitHub issues or stuck PRs

Compile results into a concise report. Then send it via the API:

curl -X POST https://orbit.foundryapps.co.uk/api/send-report \
  -H "Authorization: Bearer $CRON_SECRET" \
  -H "Content-Type: application/json" \
  -d '{"to":"david@foundryapps.co.uk","subject":"Orbit Daily Health Check — [DATE] — [STATUS]","body":"[REPORT BODY]","contentType":"text/html"}'

Get the CRON_SECRET from the Orbit .env.local file or Vercel env vars. Format the report as clean HTML with a status table. Send the email — do NOT just create a Gmail draft.
