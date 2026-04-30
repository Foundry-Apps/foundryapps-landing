---
name: Stitch workflow for Orbit web redesigns
description: How to use Google Stitch v2.0 for web page redesigns on Orbit — install, auth, prompt pattern, expected cleanup ratio
type: reference
originSessionId: c6df3e51-f84e-4319-ac0e-d3d1a055de79
---
Google Stitch v2.0 (released 19 March 2026) is the adopted tool for web-only design refreshes on Orbit. Tested on `/pricing` page April 2026 (PR #355) — passed all 5 success gates with ~17% post-export cleanup.

## Access

- Product page: stitch.withgoogle.com
- SDK: `@google/stitch-sdk` on npm (v0.1.0 as of April 2026)
- Auth: `STITCH_API_KEY` env var (generate at Settings → API on stitch.withgoogle.com)
- Key stored in Orbit repo's `.env.local` (gitignored)

## What works

- Use the SDK directly via `@google/stitch-sdk`, not the MCP server. The SDK integration is cleaner and produces the same output.
- Supply brand tokens (from `tailwind.config.js`), existing copy, and layout constraints in the prompt. The more specific the prompt, the less rework.
- Stitch nails: card layouts, billing toggles, FAQ sections, glass morphism, star-field CSS, typography rhythm, badge positioning.
- Stitch struggles with: page-level chrome (generates generic nav/footer — strip these), icon systems (outputs Material Symbols — convert to Lucide), generic color token names (map to Orbit's).

## What Stitch is NOT for

- Bespoke hero imagery — use Midjourney instead. Don't have Stitch regenerate pages that already have Midjourney video/image heroes.
- Mobile (Expo/React Native) — no official export. Community skills exist but are patchwork.
- Animation-heavy sections — Stitch produces static layouts; motion/video is hand-integrated afterwards.
- **Data-dense product UI components** — dashboard surfaces with launch data, stats, lists, countdown timers. Tested April 2026 on Orbit dashboard (PR #359): 50% success rate (2/4 Tier 1 components) vs. 100% on marketing pages. Stitch's `generate_screen_from_text` returns `expected object at projection path` errors on complex prompts describing data-bound UI — not rate-limited, content-specific. The two that did generate (DashboardStats, RecentLaunches) had low cleanup (6%, 14%) but contributed only subtle polish, not the full visual rethink you get on marketing pages.

## Workflow steps

1. Pull brand tokens from `tailwind.config.js`
2. Read the current page structure + copy
3. Write a detailed prompt: layout goals, tokens, copy, out-of-scope constraints
4. Call Stitch SDK, get HTML output
5. Convert to React: swap Material Symbols → Lucide, generic colors → Orbit tokens, strip generated nav/footer
6. Expect ~17% of lines to need touching
7. Verify: TypeScript clean, tests pass, Lighthouse a11y ≥90, brand tokens preserved
