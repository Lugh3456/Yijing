# Yijing Insights — Site Audit Report
**Standard:** WCAG 2.1 AA + SEO Best Practices | **Date:** 2026-04-01
**Pages audited:** index.html + all 64 hexagram detail pages (66 total)

---

## Executive Summary

The Yijing site has a solid visual foundation — clean typography, a warm consistent colour scheme, and well-structured hexagram content. However, **every single page** (all 66) is missing meta descriptions, a `<main>` landmark, focus styles, and `lang` attributes on Chinese text. Three of the five luck-level colours also fail WCAG contrast requirements, and the Listen buttons are too small to meet touch-target minimums. Fixing these issues will both improve accessibility for all users and make the site ready for public search indexing once it is hosted.

**Top 3 priorities:**
1. Add `lang="zh"` to all Chinese text elements (screen readers currently mispronounce every 爻辞)
2. Fix colour contrast on Excellent (gold), Good (green), and Caution (amber) luck labels
3. Add meta descriptions and a `<title>` keyword strategy across all 66 pages

---

## Part 1 — Accessibility Audit (WCAG 2.1 AA)

**Issues found: 9 | Critical: 3 | Major: 4 | Minor: 2**

---

### Perceivable

| # | Issue | WCAG | Severity | Fix |
|---|-------|------|----------|-----|
| 1 | `#b8860b` (Excellent gold) on `#fff5e0` card background — contrast ratio ≈ **2.87:1**, needs 4.5:1 | 1.4.3 | 🔴 Critical | Darken to `#7a5900` or similar (ratio ≥ 4.5:1) |
| 2 | `#cc6600` (Caution amber) on `#fff5e0` — contrast ratio ≈ **3.57:1** | 1.4.3 | 🔴 Critical | Darken to `#994d00` or similar |
| 3 | `#2d8a4e` (Good green) on `#fff5e0` — contrast ratio ≈ **3.79:1** | 1.4.3 | 🔴 Critical | Darken to `#1e6b3a` or similar |
| 4 | `#888` pinyin text on `#fff8f0` — contrast ratio ≈ **3.34:1** | 1.4.3 | 🟡 Major | Change to `#666` or darker |
| 5 | All 64 hexagram pages: `<p class="chinese">` has no `lang="zh"` — screen readers use English phonics on Chinese characters | 1.3.1 | 🟡 Major | Add `lang="zh"` to every `<p class="chinese">` element |

### Colour Contrast Check

| Element | Foreground | Background | Ratio | Required | Pass? |
|---------|-----------|------------|-------|----------|-------|
| Body text (#222) | `#222` | `#fff8f0` | ~14.0:1 | 4.5:1 | ✅ |
| Header h1 (white) | `#fff` | `#b22222` | ~6.6:1 | 4.5:1 | ✅ |
| Card h3 (#b22222) | `#b22222` | `#fff5e0` | ~6.1:1 | 4.5:1 | ✅ |
| Luck: Neutral (#555) | `#555` | `#fff5e0` | ~6.8:1 | 4.5:1 | ✅ |
| Luck: Misfortune (#b22222) | `#b22222` | `#fff5e0` | ~6.1:1 | 4.5:1 | ✅ |
| Luck: Good (#2d8a4e) | `#2d8a4e` | `#fff5e0` | ~3.79:1 | 4.5:1 | ❌ |
| Luck: Caution (#cc6600) | `#cc6600` | `#fff5e0` | ~3.57:1 | 4.5:1 | ❌ |
| Luck: Excellent (#b8860b) | `#b8860b` | `#fff5e0` | ~2.87:1 | 4.5:1 | ❌ |
| Pinyin (#888) | `#888` | `#fff8f0` | ~3.34:1 | 4.5:1 | ❌ |

---

### Operable

| # | Issue | WCAG | Severity | Fix |
|---|-------|------|----------|-----|
| 6 | No `:focus` or `:focus-visible` styles in style.css — keyboard users have no visible indicator of where focus is | 2.4.7 | 🟡 Major | Add `.hex-card-link:focus-visible, .listen-btn:focus-visible, .back-link:focus-visible { outline: 3px solid #b22222; outline-offset: 2px; }` |
| 7 | Listen buttons: `padding: 4px 8px` produces ~24px height — well below the 44×44 CSS px touch target minimum | 2.5.5 | 🟡 Major | Increase to `padding: 12px 16px; min-height: 44px;` |
| 8 | No skip navigation link — users must tab through all 64 hexagram cards to reach the footer | 2.4.1 | 🟠 Minor | Add `<a href="#hexagrams" class="skip-link">Skip to hexagrams</a>` as first element in `<body>` |

### Keyboard Navigation

| Element | Tab accessible? | Behaviour | Issue |
|---------|----------------|-----------|-------|
| Hexagram cards (index) | ✅ | `<a>` wraps card, Enter navigates | OK |
| Back to Home link | ✅ | Standard link | OK |
| Listen buttons | ✅ | Button activates TTS | No visible focus ring |
| Bagua cards (index) | ❌ | Plain `<div>` — not focusable | Non-interactive, OK for now |

---

### Robust

| # | Issue | WCAG | Severity | Fix |
|---|-------|------|----------|-----|
| 9 | All 66 pages missing `<main>` landmark — assistive tech users cannot jump directly to page content | 4.1.2 | 🟠 Minor | Wrap primary content in `<main>` on every page |
| 10 | Listen buttons have no `aria-label` — screen reader just says "Listen" 6 times with no context | 4.1.2 | 🟡 Major | Add `aria-label="Listen to [yao position]"` e.g. `aria-label="Listen to 1st Yao"` |

---

## Part 2 — SEO Audit

**Issues found: 10 | Critical: 4 | High: 3 | Medium: 2 | Low: 1**

---

### On-Page Issues

| Page | Issue | Severity | Fix |
|------|-------|----------|-----|
| All 66 pages | No `<meta name="description">` | Critical | Add unique 150-160 char description to every page |
| All 66 pages | No Open Graph tags (og:title, og:description, og:image) | High | Add OG block to `<head>` for social sharing |
| All 66 pages | No favicon | Medium | Add `<link rel="icon">` |
| index.html | Title "Yijing Insights – 64 Hexagrams" omits key search terms like "I Ching" | High | "I Ching (Yijing) – All 64 Hexagrams with Meanings" |
| hexagram-*.html | Titles like "1. 乾 Qián – The Creative" omit "I Ching" | High | "I Ching Hexagram 1: 乾 Qián – The Creative \| Yijing Insights" |
| All pages | No `<html lang>` refinement — page is `lang="en"` but contains significant Chinese content | Medium | Keep `lang="en"` on `<html>`, add `lang="zh"` at element level |
| All pages | No canonical `<link rel="canonical">` tags | Low | Add once site is hosted, to prevent duplicate indexing |
| Site root | No sitemap.xml | Critical | Generate sitemap listing all 66 URLs |
| Site root | No robots.txt | Critical | Add robots.txt (even a permissive one) |
| hexagram pages | Zero cross-links between hexagrams — no "Related hexagrams" or "Next/Previous" navigation | Critical | Add next/previous links and 2-3 thematically related hexagram links per page |

---

### Keyword Opportunity Table

| Keyword | Est. Difficulty | Opportunity | Intent | Recommended Content |
|---------|----------------|-------------|--------|---------------------|
| I Ching hexagram meanings | Medium | 🔴 High | Informational | Index page optimisation |
| I Ching hexagram 1 (…64) | Low | 🔴 High | Informational | Each hexagram detail page |
| Yijing 64 hexagrams | Low | 🔴 High | Informational | Index page |
| I Ching reading guide | Medium | 🟡 Medium | Informational | New "How to Use" page |
| I Ching 乾 meaning | Low | 🟡 Medium | Informational | hexagram-1.html |
| I Ching bagua trigrams | Low | 🟡 Medium | Informational | Bagua section / standalone page |
| I Ching luck forecast | Low | 🟡 Medium | Commercial | Future feature |
| 易经 online | Medium | 🟠 Low | Navigational | Chinese audience, future |
| I Ching daily reading | High | 🟠 Low | Transactional | Future feature |

---

### Content Gaps

| Gap | Why it matters | Format | Priority | Effort |
|-----|---------------|--------|----------|--------|
| "How to read the I Ching" intro page | Captures top-of-funnel informational traffic; competitors rank heavily for this | Guide/landing page | High | Moderate (half day) |
| Hexagram index with filter/search | 64 cards with no search makes it hard for returning users to find a specific hexagram | Interactive HTML | High | Moderate |
| "Related hexagrams" section on each detail page | Increases time-on-site, adds internal links, improves crawl depth | 2-3 links per page | High | Quick win (script) |
| Next / Previous hexagram navigation | Standard expectation; competitors all have it | Nav links | Medium | Quick win |
| Bagua trigram detail pages | 8 trigram cards link nowhere; wasted opportunity | 8 standalone pages | Medium | Substantial |
| Glossary of I Ching terms | 吉, 凶, 爻, 卦 etc — good for SEO long-tail and user education | Glossary page | Low | Moderate |

---

### Technical SEO Checklist

| Check | Status | Detail |
|-------|--------|--------|
| HTTPS | ⚠️ N/A | Local only — must be HTTPS when hosted |
| Mobile-friendly viewport | ✅ Pass | `<meta name="viewport">` present on all pages |
| Responsive grid | ✅ Pass | `auto-fit` grid adapts to screen width |
| Sitemap.xml | ❌ Fail | Missing — needs to be created before hosting |
| robots.txt | ❌ Fail | Missing |
| Meta descriptions | ❌ Fail | Missing on all 66 pages |
| Canonical tags | ❌ Fail | Missing — add when hosted |
| Open Graph / Twitter Card | ❌ Fail | Missing on all pages |
| Favicon | ❌ Fail | Missing |
| Structured data (schema.org) | ❌ Fail | No markup — Article or Book schema would help |
| Title tags | ⚠️ Warning | Present but don't include "I Ching" on detail pages |
| Internal linking | ⚠️ Warning | No cross-links between hexagram pages |
| Broken links | ✅ Pass | All 64 hexagram links are valid |
| Image alt text | ✅ Pass | No images used (no risk) |
| Heading hierarchy (H1→H2→H3) | ✅ Pass | Correct structure on all pages |
| Unique page titles | ✅ Pass | Each page has a distinct title |
| Font sizes readable | ✅ Pass | Base font is legible; no sub-10px text |

---

## Prioritised Action Plan

### Quick Wins — do this week

| Action | Impact | Effort |
|--------|--------|--------|
| Fix 3 failing luck-level colours (Excellent, Good, Caution) | High — fixes WCAG Critical failures | ~30 min (CSS only) |
| Add `lang="zh"` to all `<p class="chinese">` across 64 files | High — screen reader pronunciation | ~15 min (Python script) |
| Add `aria-label` to all Listen buttons | High — screen reader context | ~15 min (Python script) |
| Increase Listen button padding to meet 44px touch target | High — mobile usability | ~10 min (CSS only) |
| Add `:focus-visible` outline styles in CSS | High — keyboard navigation | ~10 min (CSS only) |
| Wrap content in `<main>` on all pages | Medium — landmark navigation | ~20 min (Python script) |
| Add meta descriptions to all 66 pages | Critical SEO | ~1 hour (Python script) |
| Add "I Ching" to page title pattern on hexagram pages | High SEO | ~15 min (Python script) |
| Add next/previous hexagram nav links | Medium — UX + internal linking | ~30 min (Python script) |
| Add favicon | Low — polish | ~15 min |

### Strategic Investments — plan for this quarter

| Action | Impact | Effort |
|--------|--------|--------|
| Generate sitemap.xml once hosted | Critical for indexing | Moderate |
| Add Open Graph tags for social sharing | High — shareability | Moderate |
| Add schema.org Article markup per hexagram page | Medium SEO | Moderate |
| Add related hexagrams section (3 per page) | High — engagement + internal links | Substantial |
| Build "How to read the I Ching" landing page | High — top-of-funnel SEO | Substantial |
| Add hexagram search/filter on index | High — UX | Substantial |
| Build 8 Bagua trigram detail pages | Medium — completes site architecture | Substantial |

---

*Report generated by Claude (Cowork mode) · Yijing Insights v1.0 · 2026-04-01*
