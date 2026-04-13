---
name: Below-fold framer-motion animations
description: Using initial opacity:0 + animate on elements rendered below the viewport fold causes Chrome GPU compositor to cache the invisible state — use whileInView instead
type: feedback
---

Never use `initial={{ opacity: 0 }}` + `animate={{ opacity: 1 }}` (or `initial="hidden"` + `animate="visible"` with opacity:0 variant) on elements that are rendered below the viewport fold on page load.

**Why:** Chrome's GPU compositor caches the painted state of compositing layers (elements with opacity/transform animations). When a layer is initially below the fold with opacity:0, Chrome paints it as invisible and caches that. When the user scrolls to it, Chrome serves the cached invisible layer instead of repainting — the element is in the DOM with correct CSS (getComputedStyle returns opacity:1 after animation) but is visually blank. This is a confirmed compositor bug, not a React/framer-motion bug.

**How to apply:** For any `motion.div` in DashboardContent's grid section (or any below-fold content on the dashboard), use `whileInView` with `viewport={{ once: true, amount: 0.1 }}` instead of `animate`. This triggers the animation only when the element enters the viewport, forcing Chrome to repaint at that point.

Pattern to use:
```tsx
// WRONG for below-fold content:
<motion.div initial={{ opacity: 0, y: 15 }} animate={{ opacity: 1, y: 0 }}>

// CORRECT for below-fold content:
<motion.div initial={{ opacity: 0, y: 15 }} whileInView={{ opacity: 1, y: 0 }} viewport={{ once: true, amount: 0.1 }}>
```

This was the root cause of the dashboard grid being blank (PR #132 fix). The bug was introduced when the Live Mission Panel grew tall enough (5 active missions) to push the grid below the 1031px viewport fold, triggering Chrome's deferred compositor caching.
