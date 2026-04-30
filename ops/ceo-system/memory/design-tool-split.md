---
name: Design tool split — Midjourney vs Stitch vs vector icons
description: Which AI design tool owns which part of the Foundry Apps design stack — don't let them overlap
type: feedback
originSessionId: c6df3e51-f84e-4319-ac0e-d3d1a055de79
---
Each design tool has a lane. Don't let them overlap or you get visual inconsistency and wasted effort.

**Midjourney** — bespoke hero imagery, marketing visuals, social/OG assets, atmospheric illustrations. Used for Orbit's animated rocket-launch landing hero (PR #354). Best for: moody, branded, one-of-a-kind imagery.

**Stitch (Google Labs v2.0)** — layout, component structure, pricing/features/FAQ pages, page-level design. Works from brand tokens. Produces Tailwind/React with ~17% cleanup. Web only, no Expo support. See [Stitch workflow](stitch-workflow.md).

**Vector icons (sourced or commissioned)** — all UI icons. David sources these separately. Do NOT ship raster Midjourney icons or Stitch-generated icon sets in production — they won't hold at small sizes and the style will be inconsistent.

**Why:** learned April 2026 during Orbit landing page refresh. Midjourney raster wordmark was tried, replaced with text fallback (Space Grotesk) because rasters looked soft and AI-generic next to a proper typographic treatment. Stitch generates icon suggestions that look fine at 128px but muddy at 20px.

**How to apply:**
- When David asks for a hero page or marketing visual → Midjourney
- When David asks to redesign a layout/page structure → Stitch (web) or hand-crafted (mobile)
- Never let Stitch regenerate a page that already has a Midjourney hero — carve it out in the prompt
- Never ship AI-generated raster icons — defer to David's vector sourcing
