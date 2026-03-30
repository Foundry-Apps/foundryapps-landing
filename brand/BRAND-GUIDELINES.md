# Foundry Apps — Brand Guidelines

> **Version 1.0 · March 2026**
> Maintained by David Smith · david@foundryapps.co.uk

---

## Contents

1. [Brand Story & Positioning](#1-brand-story--positioning)
2. [Mission, Vision & Values](#2-mission-vision--values)
3. [Voice & Tone](#3-voice--tone)
4. [Logo System](#4-logo-system)
5. [Colour Palette](#5-colour-palette)
6. [Typography](#6-typography)
7. [Iconography](#7-iconography)
8. [Photography & Imagery](#8-photography--imagery)
9. [Grid & Spacing](#9-grid--spacing)
10. [UI Component Principles](#10-ui-component-principles)
11. [Sub-Brand System](#11-sub-brand-system)
12. [Writing Style Guide](#12-writing-style-guide)

---

## 1. Brand Story & Positioning

### The Forge Metaphor

A forge is where raw metal meets fire, hammer, and skill. Nothing comes out by accident. Every tool that leaves a forge has been tested under real pressure, refined through iteration, and shaped by the knowledge of the craftsman who built it.

Foundry Apps is that forge for software. We are a small, independent studio based in Guernsey, building specialist digital tools for niche communities. We don't chase scale for its own sake — we chase quality. We make things that work correctly, hold up under use, and earn the trust of the people who rely on them.

The forge metaphor runs through everything:
- **Anvil** — the foundational platform everything is built on
- **Sparks** — ideas, early prototypes, the first signs of something new
- **Tempering** — the testing process that hardens software under stress
- **Forged** — the finished product: strong, purposeful, lasting

### Positioning Statement

**Foundry Apps** crafts high-quality digital products for specialist communities — tools built with the same care and intent a skilled craftsman brings to their work.

We occupy the space between the generic SaaS platform and the bespoke enterprise build: opinionated enough to be excellent, focused enough to be trusted.

### Tagline

> **Software, Forged to Last.**

Use the full tagline in marketing contexts. The shortened form **"Forged to Last"** may be used in space-constrained UI contexts (e.g. social bios, app store subtitles).

---

## 2. Mission, Vision & Values

### Mission

To build specialist software that communities can rely on — crafted with the same intent and durability a blacksmith brings to their tools.

### Vision

A world where niche communities have purpose-built digital tools as good as anything used by large enterprises.

### Core Values

#### Built to Last
We choose durability over shortcuts. Code is written with long-term maintainability in mind. Features ship when they're ready, not when they're merely done.

#### Fired by Feedback
Real users reveal what specs miss. We ship early, listen carefully, and iterate. Feedback from the community is the fire that shapes the product.

#### Tempered by Testing
Quality is baked in, not bolted on. Every feature is stress-tested before it reaches users. Confidence in the product is earned, not assumed.

#### Community-Focused
We build for specific communities, not everyone at once. Deep focus on a real audience beats shallow appeal to a generic one.

#### Honest Craft
We don't oversell, pad metrics, or use dark patterns. Our products do what they say, and our marketing describes what our products do.

---

## 3. Voice & Tone

### Brand Personality

| Dimension | We Are | We Are Not |
|-----------|--------|------------|
| Expertise | Confident, knowledgeable | Arrogant, jargon-heavy |
| Warmth | Genuine, approachable | Casual, slangy |
| Clarity | Direct, plain English | Dumbed-down, vague |
| Passion | Enthusiastic about craft | Hyperbolic, breathless |
| Honesty | Transparent about limitations | Self-deprecating to a fault |

### Voice Principles

**1. Confident but not boastful.**
We know our work is good. We don't need to shout about it. Let the product speak.

> ✅ "Orbit tracks every launch in real time, so you never miss a window."
> ❌ "Orbit is the most powerful space tracker ever built."

**2. Technical but accessible.**
We're building for enthusiasts and specialists, not casual users. Don't shy away from technical language — but always give context.

> ✅ "Live telemetry data updated every 30 seconds via the SpaceX API."
> ❌ "We use APIs and stuff to get the data."

**3. Forge metaphors: welcome, not forced.**
The forge metaphor is a thread, not a cage. Use it when it fits naturally. Don't strain for it.

> ✅ "We've been forging the next version of QuizForge behind the scenes."
> ✅ "Every feature is tempered through real-world testing."
> ❌ "Our customer support is the anvil on which your problems are hammered flat."

**4. British English throughout.**
Foundry Apps is registered in Guernsey (Channel Islands). All copy uses British English conventions.

> colour, organisation, centre, licence (noun), license (verb), realise, catalogue

**5. Warmth without fluff.**
We like people. We're building for communities we respect. But we don't pad copy with empty phrases.

> ✅ "Questions? Drop us a line."
> ❌ "We'd be absolutely thrilled and delighted to hear from you!"

### Tone by Context

| Context | Tone |
|---------|------|
| Marketing / landing pages | Ambitious, warm, purposeful |
| Product UI | Clear, efficient, helpful |
| Error messages | Honest, calm, constructive |
| Documentation | Precise, patient, thorough |
| Social media | Human, direct, occasionally playful |
| Legal / privacy | Plain, honest, no legalese where avoidable |

---

## 4. Logo System

### Master Logo Files

| File | Use Case |
|------|----------|
| `logos/foundry-apps-logo.svg` | Primary: icon + wordmark + tagline |
| `logos/foundry-apps-icon.svg` | Favicon, app icon, avatar |
| `logos/foundry-apps-wordmark.svg` | Text-only contexts, document headers |

### The Icon

The Foundry Apps icon is a stylised **anvil** with a glowing ember on the working surface and rising sparks. It represents:
- The forge/metalwork metaphor
- Heat and energy (sparks = active development)
- Stability and craft (the anvil = reliable foundation)

The icon uses a warm dark background (`#1c1917`) that connects to the brand's dark canvas. The ember uses the primary forge orange (`#f97316`) via a radial gradient.

### Clear Space

Maintain clear space equal to the height of the letter "F" in the wordmark on all sides of the logo. Nothing — text, imagery, other logos — should intrude on this zone.

### Minimum Sizes

| Format | Minimum Size |
|--------|-------------|
| Icon only | 16×16px (favicon); 32×32px recommended minimum |
| Full logo (icon + wordmark) | 160px wide |
| Wordmark only | 120px wide |

### Colour Variants

**On dark backgrounds (primary use)**
- Icon: as designed (warm dark bg, orange glow)
- Wordmark: "Foundry" in orange gradient, "Apps" in `#e7e5e4`

**On light backgrounds**
- Icon: replace background rect with `#f5f4f0` (warm off-white); keep anvil and sparks unchanged
- Wordmark: "Foundry" in `#f97316`, "Apps" in `#1c1917`

**Single colour (e.g. embroidery, engraving)**
- Use `#f97316` on dark, or `#1c1917` on light
- The icon simplifies to: anvil outline + ember dot. Drop the sparks.

### Do's and Don'ts

✅ Use the logo on dark backgrounds as primary application
✅ Use the icon alone when space is limited
✅ Maintain aspect ratio — never stretch or squash
✅ Use SVG format wherever possible

❌ Don't recolour the logo outside the approved variants
❌ Don't place the logo on busy photographic backgrounds without a dark overlay
❌ Don't add drop shadows, outlines, or glows to the logo
❌ Don't reproduce the wordmark in a different typeface
❌ Don't use the logo at sizes below the minimums listed above
❌ Don't rotate or skew the logo

---

## 5. Colour Palette

All colours are defined as CSS custom properties in `brand/colors.css`.

### Master Brand Colours

#### Backgrounds

| Name | Token | Hex | RGB | HSL | Use |
|------|-------|-----|-----|-----|-----|
| Deep | `--foundry-bg-deep` | `#0c0a09` | 12, 10, 9 | 20°, 14%, 4% | Page canvas |
| Surface | `--foundry-bg-surface` | `#1c1917` | 28, 25, 23 | 20°, 10%, 10% | Sections, sidebars |
| Card | `--foundry-bg-card` | `#292524` | 41, 37, 36 | 10°, 7%, 15% | Cards, panels |
| Hover | `--foundry-bg-hover` | `#3c3836` | 60, 56, 54 | 15°, 5%, 22% | Interactive hover |

#### Borders

| Name | Token | Hex | RGB | HSL |
|------|-------|-----|-----|-----|
| Default | `--foundry-border` | `#44403c` | 68, 64, 60 | 30°, 6%, 25% |
| Light | `--foundry-border-lt` | `#57534e` | 87, 83, 78 | 30°, 6%, 32% |

#### Text

| Name | Token | Hex | RGB | HSL | Use |
|------|-------|-----|-----|-----|-----|
| Primary | `--foundry-text` | `#e7e5e4` | 231, 229, 228 | 20°, 8%, 90% | Body copy |
| Muted | `--foundry-text-muted` | `#a8a29e` | 168, 162, 158 | 20°, 4%, 64% | Secondary copy |
| Faint | `--foundry-text-faint` | `#78716c` | 120, 113, 108 | 20°, 5%, 45% | Placeholder, disabled |

#### Forge Orange (Primary Accent)

| Name | Token | Hex | RGB | HSL | WCAG on `#0c0a09` |
|------|-------|-----|-----|-----|-------------------|
| Orange 300 | `--foundry-orange-300` | `#fdba74` | 253, 186, 116 | 30°, 97%, 72% | 7.2:1 (AAA) |
| Orange 400 | `--foundry-orange-400` | `#fb923c` | 251, 146, 60 | 27°, 96%, 61% | 5.1:1 (AA) |
| **Orange 500** | `--foundry-orange-500` | `#f97316` | 249, 115, 22 | 24°, 95%, 53% | 3.8:1 (AA Large) |
| Orange 600 | `--foundry-orange-600` | `#ea580c` | 234, 88, 12 | 21°, 90%, 48% | 2.9:1 |
| Orange 700 | `--foundry-orange-700` | `#c2410c` | 194, 65, 12 | 20°, 88%, 40% | 2.0:1 |

> **Accessibility note:** Orange 500 (`#f97316`) does not meet WCAG AA for small text on dark backgrounds. Use Orange 300 or 400 for body-size interactive text. Orange 500 is approved for large headings (18pt+), icons, and decorative elements.

#### Semantic Colours

| Name | Token | Hex | RGB | HSL |
|------|-------|-----|-----|-----|
| Success | `--foundry-success` | `#22c55e` | 34, 197, 94 | 142°, 71%, 45% |
| Warning | `--foundry-warning` | `#f59e0b` | 245, 158, 11 | 38°, 92%, 50% |
| Error | `--foundry-error` | `#ef4444` | 239, 68, 68 | 0°, 84%, 60% |
| Info | `--foundry-info` | `#38bdf8` | 56, 189, 248 | 199°, 92%, 60% |

### Colour Usage Principles

1. **Dark-first.** All products default to dark backgrounds. Light mode is not currently supported.
2. **Orange is active.** The forge orange signals interactivity, importance, or brand identity. Don't dilute it by using it for decoration.
3. **Warmth in the darks.** The background colours have a warm stone/charcoal undertone — this is intentional. Avoid pure `#000000` black.
4. **Sub-brand accents augment, not replace.** Sub-brand colours (Orbit blue, QuizForge violet) work alongside forge orange, never instead of it.

---

## 6. Typography

### Type Stack

| Role | Family | Weights | Source |
|------|--------|---------|--------|
| **Display / Headings** | Playfair Display | 700, 900 | Google Fonts |
| **Body / UI** | Inter | 400, 500, 600 | Google Fonts |
| **Code / Monospace** | JetBrains Mono | 400, 500 | Google Fonts |

### Import

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
```

### Why These Fonts

**Playfair Display** is a high-contrast serif with editorial character — it evokes craftsmanship, quality printing, and permanence. It connects the brand to its "forged to last" positioning and gives headings genuine personality.

**Inter** is the gold standard for UI legibility. Designed specifically for screens, it is highly readable at small sizes, neutral enough to not compete with Playfair Display's character, and available at variable weights.

**JetBrains Mono** — developer-friendly, legible, and from a company (JetBrains) that also builds specialist tools for specialist communities. The ligatures add a premium feel to code samples.

### Type Scale

| Step | Size | Line Height | Letter Spacing | Usage |
|------|------|-------------|---------------|-------|
| `xs` | 0.75rem (12px) | 1.4 | 0.05em | Labels, overlines |
| `sm` | 0.875rem (14px) | 1.5 | 0.01em | Small UI text, captions |
| `base` | 1rem (16px) | 1.6 | 0 | Body copy |
| `lg` | 1.125rem (18px) | 1.5 | 0 | Lead paragraphs |
| `xl` | 1.25rem (20px) | 1.4 | -0.01em | Card titles |
| `2xl` | 1.5rem (24px) | 1.3 | -0.01em | Section subtitles |
| `3xl` | 1.875rem (30px) | 1.2 | -0.02em | Section headings |
| `4xl` | 2.25rem (36px) | 1.15 | -0.02em | Page titles |
| `5xl` | 3rem (48px) | 1.1 | -0.03em | Hero headings |
| `6xl` | 3.75rem (60px) | 1.05 | -0.04em | Display (clamp-responsive) |

### Responsive Headline Clamp

Hero and major section headings use `clamp()` to scale gracefully:

```css
.hero-headline  { font-size: clamp(2.8rem, 7vw, 5.5rem); }
.section-title  { font-size: clamp(1.9rem, 4vw, 3rem); }
```

### Eyebrow / Label Treatment

Section labels (e.g. "Our Products", "The Forge") use:
- Font: Inter, 600
- Size: 0.75rem (12px)
- Letter spacing: 0.15em
- Text transform: uppercase
- Colour: `--foundry-orange-500`

This creates a strong visual hierarchy anchor before section headings.

### Code Blocks

```css
code, pre {
  font-family: 'JetBrains Mono', 'Fira Code', 'Cascadia Code', monospace;
  font-size: 0.875rem;
  background: var(--foundry-bg-card);
  border: 1px solid var(--foundry-border);
  border-radius: 6px;
  color: var(--foundry-text);
}
pre { padding: 1.25rem; overflow-x: auto; }
code { padding: 0.15em 0.4em; }
```

---

## 7. Iconography

### Style

- **Line icons** (stroke-based), not filled, for UI contexts
- Stroke width: **1.8px** at 24×24px viewBox
- Rounded `stroke-linecap` and `stroke-linejoin`
- No decorative effects (no drop shadows, gradients on line icons)
- Colour: `currentColor` — inherits from parent element's `color` property

### Sizing

| Context | Size |
|---------|------|
| Inline with body text | 16×16px |
| UI icons (buttons, inputs) | 20×20px |
| Feature/section icons | 24×24px |
| Card icons | 32×32px |
| Illustration icons | 48px+ |

### Icon Backgrounds (Cards)

Feature icons displayed on cards use a coloured background:

```css
.icon-wrap {
  width: 48px;
  height: 48px;
  background: rgba(249, 115, 22, 0.12);  /* orange-glow-md */
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--foundry-orange);
}
```

For sub-brands, replace the rgba colour with the product's own glow variable (e.g. `--orbit-glow-md`).

### Recommended Icon Library

Use **Lucide Icons** (MIT licence) as the primary icon set. The stroke-based style, consistent geometry, and comprehensive coverage make it the best fit for the brand.

Avoid mixing icon sets — Heroicons, Phosphor, and Tabler are acceptable as secondary sources if a specific icon is missing from Lucide, but mixing should be minimised.

---

## 8. Photography & Imagery

### Style Principles

1. **Dark, moody, high-contrast.** All photography and generated imagery should work on dark backgrounds. Avoid bright white or pastel-heavy imagery.

2. **Warm orange accent lighting.** Where lighting is visible in an image, the key light or accent should carry amber/orange warmth — consistent with the forge aesthetic. Cold blue-only lighting feels off-brand.

3. **Craft and precision.** Imagery should suggest skilled human work — close-ups of tools, materials, screens, or hands at work. Avoid stock-photo cheerfulness.

4. **Real, not generic.** Avoid clichéd "business" or "tech" imagery (handshakes, vague blue circuitry, stock-photo laptops). Prefer atmospheric, editorial photography.

5. **Space imagery (Orbit).** For Orbit, NASA/ESA photography is acceptable (public domain). Choose images that emphasise the scale and clarity of space — not cartoon-style illustrations.

6. **Quiz/pub atmosphere (QuizForge).** Warm pub lighting, close-ups of quiz cards and pints, competitive groups around a table. Golden/amber-lit rather than harsh fluorescent.

### Overlay Treatment

When using photography as a background, always apply a dark overlay to maintain text legibility:

```css
.photo-bg::after {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(
    180deg,
    rgba(12, 10, 9, 0.6) 0%,
    rgba(12, 10, 9, 0.85) 100%
  );
}
```

### Aspect Ratios

| Use case | Ratio |
|----------|-------|
| Hero / full-bleed | 16:9 or 21:9 |
| Social share (OG) | 1200×630px (1.91:1) |
| Blog header | 3:1 |
| Product card preview | 16:9 |
| Square (social avatar) | 1:1 |
| App Store screenshot | 9:19.5 (iPhone) |

---

## 9. Grid & Spacing

### Container

```css
.container {
  max-width: 1120px;
  margin: 0 auto;
  padding: 0 1.5rem;
}
```

At viewport ≥ 1152px, content is centred with auto margins.

### Spacing Scale

Uses a base-8 scale (Tailwind compatible):

| Token | Value | Pixels |
|-------|-------|--------|
| `space-1` | 0.25rem | 4px |
| `space-2` | 0.5rem | 8px |
| `space-3` | 0.75rem | 12px |
| `space-4` | 1rem | 16px |
| `space-6` | 1.5rem | 24px |
| `space-8` | 2rem | 32px |
| `space-10` | 2.5rem | 40px |
| `space-12` | 3rem | 48px |
| `space-16` | 4rem | 64px |
| `space-24` | 6rem | 96px |
| `space-28` | 7rem | 112px |

### Section Padding

Major page sections use `padding: 7rem 0` (112px top and bottom). This creates deliberate, breathing space between content blocks.

### Grid Breakpoints

| Name | Width |
|------|-------|
| `sm` | 640px |
| `md` | 768px |
| `lg` | 1024px |
| `xl` | 1280px |

### Card Grids

```css
/* Auto-fit card grid */
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
}

/* Product card grid (larger minimum) */
.product-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 2rem;
}
```

---

## 10. UI Component Principles

### Design Philosophy

**Dark-first.** The entire UI system is designed for dark backgrounds. The charcoal/stone palette (`#0c0a09` → `#292524`) provides the foundation. Light mode is not currently in scope.

**Borders define structure, not colour.** Cards and panels are delineated by `1px solid var(--foundry-border)` rather than colour fills. This maintains visual weight without visual noise.

**Subtle depth.** Use border glow (`box-shadow: 0 0 32px rgba(249, 115, 22, 0.1)`) rather than heavy shadows to indicate hover/focus state.

**Rounded but not soft.** Border radius values:
- Small elements (badges, tags): `border-radius: 99px` (pill)
- Buttons, inputs: `border-radius: 6px`
- Cards: `border-radius: 10–14px`
- Icon wraps: `border-radius: 8–12px`

### Buttons

**Primary (CTA)**
```css
.btn-primary {
  background: var(--foundry-orange-500);
  color: #fff;
  font-weight: 600;
  font-size: 0.95rem;
  padding: 0.8rem 2rem;
  border-radius: 6px;
  border: none;
  transition: background 0.2s, transform 0.15s;
}
.btn-primary:hover {
  background: var(--foundry-orange-400);
  transform: translateY(-1px);
}
```

**Secondary (Ghost)**
```css
.btn-secondary {
  background: transparent;
  color: var(--foundry-orange-500);
  font-weight: 600;
  padding: 0.7rem 1.5rem;
  border-radius: 6px;
  border: 1px solid var(--foundry-orange-500);
  transition: background 0.2s;
}
.btn-secondary:hover {
  background: rgba(249, 115, 22, 0.1);
}
```

### Cards

Cards use:
- Background: `var(--foundry-bg-card)` (`#292524`)
- Border: `1px solid var(--foundry-border)`
- Border-radius: 10–14px
- Hover: border transitions to `var(--foundry-orange)` with `transform: translateY(-3px)`
- Hover glow: `box-shadow: 0 0 32px rgba(249, 115, 22, 0.1)`

### Badges / Tags

```css
.badge-live {
  font-size: 0.65rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: #4ade80;
  background: rgba(74, 222, 128, 0.12);
  border: 1px solid rgba(74, 222, 128, 0.30);
  padding: 0.15rem 0.5rem;
  border-radius: 99px;
}

.tag {
  font-size: 0.72rem;
  font-weight: 600;
  padding: 0.25rem 0.65rem;
  border-radius: 99px;
  background: rgba(249, 115, 22, 0.10);
  color: var(--foundry-orange-300);
  border: 1px solid rgba(249, 115, 22, 0.20);
}
```

### Navigation

- Fixed, top-mounted
- Background: `rgba(12, 10, 9, 0.85)` with `backdrop-filter: blur(12px)`
- Height: 64px
- Border-bottom: `1px solid var(--foundry-border)`
- Logo: Playfair Display, 1.2rem, 700
- Links: Inter, 0.9rem, 500, colour `var(--foundry-text-muted)`, hover `var(--foundry-orange)`

### Focus States

All interactive elements must have a visible focus ring for keyboard navigation:
```css
:focus-visible {
  outline: 2px solid var(--foundry-orange-400);
  outline-offset: 2px;
  border-radius: 4px;
}
```

### Animation

Keep animations purposeful and brief:
- Fade-up on scroll: `opacity 0.6s ease, transform 0.6s ease`
- Hover transitions: 0.2s for colour/background, 0.15s for transform
- No animation for users who prefer reduced motion:

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## 11. Sub-Brand System

### Philosophy

Each Foundry Apps product is a distinct brand, but they are clearly siblings. Think of the sub-brands as **forged from the same stock** — same foundational metal, different shapes for different purposes.

### What Is Shared Across All Products

| Element | Shared Value |
|---------|-------------|
| Dark background system | Same `--foundry-bg-*` variables |
| Typography | Playfair Display + Inter |
| Forge orange | Always present as secondary accent |
| Border radius & spacing | Same scale |
| Animation timing | Same values |
| Voice & tone | Same principles, product-appropriate vocabulary |
| Foundry Apps attribution | "by Foundry Apps" or "A Foundry Apps Product" |

### What Differs Per Product

| Element | Per-Product |
|---------|------------|
| Primary accent colour | Each product has its own |
| Background dark tint | Subtle hue shift (Orbit: navy-tinged, QuizForge: purple-tinged) |
| Icon/logo | Product-specific icon, same logo format |
| Imagery style | Product-appropriate (space, pub, etc.) |

### Naming Conventions

Product names should be:
- **Short** (1–2 syllables preferred): Orbit, QuizForge, Forge (hypothetical)
- **Descriptive or evocative** of the product domain
- **Memorable** without requiring explanation
- **Scalable** — works as `[Name].foundryapps.co.uk`

The "Forge" suffix is available as a naming device where it genuinely fits (QuizForge). It shouldn't be forced onto products where it doesn't apply.

### Logo Format

Every product logo follows the same format:
```
[Product Icon] + [Product Name]  (large)
                by Foundry Apps  (small, muted)
```

The "by Foundry Apps" attribution should always be present in full-logo usage. Icon-only usage does not require attribution.

### Sub-Brand: Orbit

**Domain:** Space mission tracking
**Accent colour:** `#3b82f6` (sky blue — Tailwind `blue-500`)
**Background tint:** Deep navy (`#06090f`, `#0d1526`)
**Secondary accent:** Forge orange (used for ring/orbit elements — a visual metaphor)
**Mood:** Expansive, precise, awe-inspiring

Orbit's visual language evokes deep space: dark navy backgrounds, blue planet-glow, the forge-orange ring connecting the space product back to the parent brand. The ring detail on the planet icon is a deliberate visual bridge.

**Orbit-specific colour tokens:** See `brand/colors.css` → `--orbit-*`

### Sub-Brand: QuizForge

**Domain:** Pub quiz / trivia platform
**Accent colour:** `#8b5cf6` (violet — Tailwind `violet-500`)
**Background tint:** Deep purple-black (`#0d0717`, `#180d2e`)
**Secondary accent:** Forge orange (used for the lightning bolt in the icon)
**Mood:** Energetic, competitive, warm, social

QuizForge's icon uses a speech bubble (quiz/knowledge exchange) with a lightning bolt inside (the forge). The bolt gradient runs from violet (top) to orange (bottom) — visually unifying the QuizForge accent with the parent brand.

**QuizForge-specific colour tokens:** See `brand/colors.css` → `--quizforge-*`

### Future Products

When adding a new product:

1. **Choose an accent colour** that doesn't conflict with existing products (avoid pure orange, deep blue, or violet — these are taken)
2. **Create a background tint** by darkening the accent colour significantly (85–95% dark)
3. **Design an icon** that uses the accent as primary and forge orange as secondary
4. **Name the CSS token group** `--[productname]-*` and add to `colors.css`
5. **Add logo files** to `brand/logos/` following existing naming conventions
6. **Update these guidelines** with the new sub-brand section

---

## 12. Writing Style Guide

### British English

Always use British English spellings and conventions:

| British | Avoid |
|---------|-------|
| colour, colour scheme | color |
| organisation | organization |
| centre | center |
| licence (noun) | license (noun) |
| realise, recognise | realize, recognize |
| programme | program (except software: "computer program" is correct) |
| catalogue | catalog |
| whilst | while (while is acceptable but whilst preferred) |
| practise (verb) | practice (verb) |

**Date format:** Day Month Year — e.g. "30 March 2026" (not "March 30, 2026")

**Quotes:** Use 'single' for primary quotation marks, "double" for nested.

**Oxford comma:** Not standard in British English, but use it where it aids clarity.

### Referring to the Company

| Context | Usage |
|---------|-------|
| Formal | Foundry Apps Ltd |
| Standard | Foundry Apps |
| Informal | Foundry (acceptable in social media only) |
| Possessive | Foundry Apps's (not Foundry Apps') |
| Pronoun | "we" and "our" — never "it" |

### Referring to Products

**Full name on first mention in copy, shortened thereafter:**
- "Orbit, the space mission tracker" → then just "Orbit"
- "QuizForge, the pub quiz platform" → then just "QuizForge"

**Product pronouns:** Use "it" for products. ("Orbit shows you live launch data. It updates every 30 seconds.")

**Features:** Capitalise proper feature names (Pro Tier, Live Countdowns, ISS Tracker). Don't capitalise generic descriptions ("the live feed", "the countdown timer").

### Error Messages

Error messages should be:
1. **Honest** — say what happened
2. **Calm** — don't alarm users unnecessarily
3. **Actionable** — tell them what to do next

> ✅ "We couldn't load the latest launch data. Check your connection and try again."
> ❌ "ERROR 503: Service unavailable."
> ❌ "Something went terribly wrong! 😱"

### Marketing Copy Patterns

**Hero headlines:** Subject + verb + benefit. The tagline format.
> "Track every mission to the stars." (Orbit)
> "Never lose a round again." (QuizForge — hypothetical)

**Feature descriptions:** Lead with the user benefit, not the technical feature.
> ✅ "Never miss a launch window — live countdowns update in real time."
> ❌ "Real-time API polling with 30-second refresh intervals."

**CTAs:** Active, specific, and confidence-inspiring.
> ✅ "Launch Orbit" / "Start Tracking" / "Explore the Catalogue"
> ❌ "Click Here" / "Submit" / "Learn More"

### Numbers and Data

- Spell out numbers one to nine; use numerals for 10 and above
- Use commas for thousands: 1,000 not 1000
- Percentages: use the % symbol (not "per cent") in UI and marketing copy
- "50+ launches" not "50 launches or more"

### Punctuation

- Em dash (—) for asides and breaks in copy. No spaces either side: "Software—Forged to Last"
- Ellipsis (…) for trailing off, not three periods
- Bullet points: end with no punctuation for short phrases; end with a full stop for complete sentences
