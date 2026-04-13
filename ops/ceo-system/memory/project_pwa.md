---
name: PWA Implementation
description: Full PWA shipped 2026-04-01 — manifest, SW caching, offline page, bottom nav, install prompt, iOS apple-icon
type: project
---

Full PWA implementation merged to master (PR #54, commit 70d814a) on 2026-04-01.

**Components added:**
- `public/manifest.json` — brand manifest with 192/512/maskable icons via `/api/pwa/icon`
- `public/sw.js` (orbit-v2) — cache-first static, network-first API, offline nav fallback
- `public/offline.html` — standalone branded offline page, auto-retries on reconnect
- `public/.well-known/assetlinks.json` — TWA stub (SHA-256 fingerprint needed for Play Store)
- `src/app/api/pwa/icon/route.tsx` — ImageResponse PNG icon generator (size + maskable query params)
- `src/app/apple-icon.tsx` — 180×180 apple-touch-icon
- `src/components/pwa/ServiceWorkerRegistration.tsx` — registers SW on mount
- `src/components/pwa/InstallPrompt.tsx` — branded A2HS banner, respects standalone mode
- `src/components/pwa/BottomNav.tsx` — mobile tab bar (Home/Launches/ISS/Events/More), lg:hidden

**Why:** David wants to launch Orbit TODAY including mobile experience. Phase 1 of mobile strategy.
**How to apply:** For any future PWA changes, build on these components. TWA (Phase 2) needs `.well-known/assetlinks.json` SHA-256 fingerprint added when submitting to Play Store.
