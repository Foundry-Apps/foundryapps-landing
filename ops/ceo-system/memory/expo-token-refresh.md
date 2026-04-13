---
name: Expo token refresh
description: EXPO_TOKEN expired again by April 8 2026 — needs refresh in .env.local and GitHub secrets
type: reference
---

EXPO_TOKEN `aneW3Yn29EIXZ5l4RbVo1qLrnnIaiertQBQ2CwHo` was set on 7 April 2026 but expired by 8 April 2026. Needs David to generate a new one at expo.dev and update in both `.env.local` and GitHub repo secrets (`EXPO_TOKEN`).

Also set in Expo dashboard (preview + production environments):
- `EXPO_PUBLIC_SUPABASE_URL` = `https://ujssnmrpxmbujmfugsug.supabase.co`
- `EXPO_PUBLIC_SUPABASE_ANON_KEY` = (matches NEXT_PUBLIC_SUPABASE_ANON_KEY)
- `EXPO_PUBLIC_NASA_API_KEY` = set
- `EXPO_PUBLIC_REVENUECAT_API_KEY` = "placeholder" (needs real key)
