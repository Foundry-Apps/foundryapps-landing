---
taskId: email-digest
cron: "0 9 * * *"
schedule: 09:00 daily (UTC)
enabled: true
description: Daily scan of Gmail for important business emails
---

# email-digest

Scan Gmail for important business emails received in the last 24 hours. Look for:
1. Replies from service providers (Paddle, Supabase, Vercel, Cloudflare, Sovereign Group, Collas Crill)
2. Customer enquiries or support requests
3. Security alerts or account notifications
4. Anything requiring David's attention

Compile a digest of important items with sender, subject, and a 1-line summary of each. Then send it via the API:

curl -X POST https://orbit.foundryapps.co.uk/api/send-report \
  -H "Authorization: Bearer $CRON_SECRET" \
  -H "Content-Type: application/json" \
  -d '{"to":"david@foundryapps.co.uk","subject":"Foundry Apps Email Digest — [DATE]","body":"[DIGEST BODY]","contentType":"text/html"}'

Get the CRON_SECRET from the Orbit .env.local file or Vercel env vars. Format as clean HTML. Send the email — do NOT just create a Gmail draft.
