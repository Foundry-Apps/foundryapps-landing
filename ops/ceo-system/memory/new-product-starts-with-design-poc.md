---
name: Start every new product with a Claude Design PoC
description: Standing rule — new Foundry Apps products begin with a Claude Design PoC that sets branding and design. Every product maintains a living design reference doc used to drive all subsequent development.
type: feedback
originSessionId: a3a07943-25ea-4687-842b-baa4fad0c808
---
**Rule:** Every new Foundry Apps product (website or app) MUST start with a Claude Design PoC before any feature work begins. The PoC establishes the brand and design language. A canonical design-system / branding reference doc is then distilled from the PoC and maintained inside the product's repo — this doc is the source of truth for all future UI, marketing, and component decisions.

**Why:**
- Confirmed 19 April 2026. The Orbit PoC → refresh workflow (Claude Design PoC → DESIGN_BRIEF.md → PR #374 audit-driven refresh) produced a visual result David described as "incredible" and the biggest quality jump we've had. Starting products without a design foundation leads to generic UI, inconsistent visual language, and expensive cosmetic rework later.
- Having a living design reference prevents design drift as features are added. Without one, each new feature reinvents its own styling and the product fragments visually.

**How to apply:**

1. **New product kickoff (before any feature code):**
   - Step 1: Brief Claude Design with product concept, positioning, audience. Request a PoC (live HTML prototype preferred — easier to extract exact token values than static images).
   - Step 2: Run the PoC through a Design Brief analysis (like `/sessions/.../outputs/orbit-poc/DESIGN_BRIEF.md`): extract colour system, typography, layout patterns, signature moves, PoC-isms to avoid.
   - Step 3: Distill the brief into a canonical `docs/design-system.md` (or `design/README.md`) in the product repo. Include: brand pillars, colour tokens (hex + OKLCH + when-to-use), typography (families, sizes, tracking, hierarchy), spacing scale, component inventory with visual spec, motion/interaction rules, signature moves, explicit "don't-do" list.
   - Step 4: Wire the tokens into the product's styling system (Tailwind theme, CSS vars, etc.) matching the design-system.md values EXACTLY.
   - Step 5: Only then start feature work. Every new surface audits against the design-system.md before shipping.

2. **Existing products (retrofit):**
   - Orbit: design-system.md distillation task is tracked to follow PR #374 (post-refresh cleanup). Captures the actual tokens + primitives + rules from the shipped refresh so future feature work stays true to what was shipped.
   - QuizForge (not yet launched): MUST follow the new-product-kickoff flow above when it launches.

3. **Completion metric for design work:**
   Every page/surface audits against the 8-hypothesis grid (colour system / typography / structure / signature moves / PoC-isms removed / hero preservation / WCAG AA / responsive) scored P0/P1/P2. Shipping requires all P0s cleared. See PR #374 for the reference audit format.

4. **Going forward — operating rhythm:**
   - When a feature adds UI, the spec must reference the relevant design-system.md sections.
   - When someone (David, a code task, an agent) proposes UI that drifts from design-system.md, Dispatch should push back and route to revisit either the spec or the design-system.md — not silently absorb the drift.
   - Design-system.md is a versioned doc. Major visual changes require an intentional design-system.md update, not an ad-hoc deviation in a feature PR.
