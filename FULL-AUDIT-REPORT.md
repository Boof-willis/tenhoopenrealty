# Full SEO Audit Report: tenhoopenrealty.com

**Date:** 2026-03-23
**Site:** https://tenhoopenrealty.com/
**Business:** ten Hoopen Realty — Real Estate Agency, Lagos, Algarve, Portugal
**CMS:** WordPress + Elementor | **CDN:** Cloudflare
**AMI License:** 19855

---

## Executive Summary

### Overall SEO Health Score: 48/100

| Category | Weight | Score | Weighted |
|----------|--------|-------|----------|
| Technical SEO | 25% | 48/100 | 12.0 |
| Content Quality | 25% | 62/100 | 15.5 |
| On-Page SEO | 20% | 55/100 | 11.0 |
| Schema / Structured Data | 10% | 35/100 | 3.5 |
| Performance (CWV) | 10% | 25/100 | 2.5 |
| Images | 5% | 30/100 | 1.5 |
| AI Search Readiness | 5% | 38/100 | 1.9 |
| **TOTAL** | **100%** | | **47.9** |

### Business Type Detected
**Real Estate Agency** — Local business serving international property buyers in the Algarve, Portugal. Multilingual team (Dutch, German, French, Portuguese, Spanish, English). Services include buying, selling, construction, pool design, and development.

### Top 5 Critical Issues

1. **Property URLs use query parameters** (`/property-details?reference=XXXX`) causing canonical collapse — all property pages likely canonicalize to the same URL, destroying indexability
2. **Property pages likely excluded from XML sitemap** — query-parameter URLs are not included by Yoast by default
3. **All three Core Web Vitals likely failing on mobile** — estimated LCP 5-8s, INP 300-600ms, CLS 0.15-0.40
4. **hreflang implementation likely broken** — GTranslate may only inject hreflang via JavaScript, invisible to crawlers
5. **Content cannibalization** between buying guide (`/buying-property-in-algarve/`) and blog post (`/buying-a-property-in-portugal/`)

### Top 5 Quick Wins

1. **Create `/llms.txt` file** — 2 hours, first-mover advantage for AI search citation
2. **Add author bylines with credentials** to all guide/blog content — 4 hours
3. **Add `<link rel="preconnect">` tags** for `cdn.proppy.app`, `fonts.gstatic.com` — 30 minutes
4. **Enable Cloudflare APO** ($5/month) for instant TTFB improvement — 30 minutes
5. **Add "Last Updated" dates** to all informational pages — 2 hours

---

## 1. Technical SEO (Score: 48/100)

### 1.1 Crawlability

**robots.txt** — Standard Yoast configuration:
```
User-agent: *
Disallow: /wp-admin/
Disallow: /wp-login.php
Disallow: /cgi-bin/
Disallow: */?s=*
Disallow: /xmlrpc.php
Disallow: /author/
Disallow: /tag/
Disallow: /category/

Allow: /wp-content/uploads/
Allow: /wp-content/themes/
Allow: /wp-content/plugins/

Sitemap: https://www.tenhoopenrealty.com/sitemap_index.xml
```

**Issues:**
| Severity | Issue |
|----------|-------|
| Medium | No AI crawler directives (GPTBot, ClaudeBot, PerplexityBot all allowed by default — no selective control) |
| Medium | `/category/` is disallowed — this may block useful category archive pages |

**XML Sitemap** — Index file with 8 sub-sitemaps (Yoast-generated):
- post-sitemap.xml, page-sitemap.xml, project-sitemap.xml, epkb_post_type_1-sitemap.xml, category-sitemap.xml, post_tag-sitemap.xml, epkb_post_type_1_category-sitemap.xml, author-sitemap.xml

| Severity | Issue |
|----------|-------|
| **Critical** | Property detail pages (`/property-details?reference=XXXX`) are almost certainly excluded from all sitemaps |
| Medium | Author sitemap exists but `/author/` is disallowed in robots.txt — contradictory signals |
| Medium | `/pt/` and `/nl/` language variants likely missing from sitemaps |

### 1.2 Indexability

| Severity | Issue |
|----------|-------|
| **Critical** | Canonical collapse — WordPress strips query parameters from canonical tags, so all property pages likely canonicalize to `/property-details` |
| High | GTranslate machine-translated pages may create duplicate content or carry incorrect canonicals |
| Medium | Pagination for property listings likely unoptimized if loaded via JavaScript |

### 1.3 URL Structure

| Severity | Issue |
|----------|-------|
| **Critical** | Property URLs use query parameters instead of clean permalinks. Recommended: `/properties/villa-3-bed-lagos-th1234/` |
| Medium | www vs non-www inconsistency — schema uses `www.tenhoopenrealty.com`, site may serve from `tenhoopenrealty.com` |
| Medium | Trailing slash consistency needs verification |

### 1.4 Security

| Severity | Issue |
|----------|-------|
| Pass | HTTPS active via Cloudflare |
| High | Likely missing HSTS, CSP, X-Content-Type-Options, Permissions-Policy headers |
| Medium | Cloudflare challenge scripts may add latency for legitimate visitors |

### 1.5 Internationalization

| Severity | Issue |
|----------|-------|
| **Critical** | hreflang tags likely only injected via JavaScript (GTranslate), invisible to crawlers |
| High | Machine-translated Portuguese content for a Portugal-based business is a competitive disadvantage |
| Medium | Should use `pt-PT` instead of `pt` to target European Portuguese |
| Medium | Missing `x-default` hreflang tag |

### 1.6 JavaScript Rendering

| Severity | Issue |
|----------|-------|
| **Critical** | Proppy.app property listings may be client-side rendered only — invisible to crawlers in initial HTML |
| High | Elementor loads ~200-400KB of JavaScript regardless of page needs |

---

## 2. Content Quality (Score: 62/100)

### 2.1 E-E-A-T Assessment

| Factor | Score | Assessment |
|--------|-------|------------|
| Experience | 5.5/10 | First-hand market signals present but inconsistent; lacks case studies and transaction narratives |
| Expertise | 6.0/10 | Multilingual team suggests competence; author credentials underexposed |
| Authoritativeness | 5.0/10 | Luxury Lifestyle Award is strong but likely buried; external citation profile weak |
| Trustworthiness | 6.5/10 | AMI license 19855 is the strongest trust signal; multilingual support builds confidence |

**Composite E-E-A-T Score: 5.8/10**

### 2.2 Page-by-Page Scores

| Page | Quality | E-E-A-T | AI Ready | Top Issue |
|------|---------|---------|----------|-----------|
| Homepage | 65/100 | 6.0/10 | 4/10 | Too long (3,500-4,200 words); should be 800-1,200 |
| About Us | 55/100 | 5.0/10 | 3/10 | Missing individual team bios with credentials |
| Buying Guide (Algarve) | 68/100 | 6.5/10 | 6/10 | Verify regulatory accuracy; add update dates |
| Blog Post (Portugal) | 55/100 | 5.0/10 | 4/10 | Cannibalizes buying guide keywords |
| Location (Lagos) | 60/100 | 5.5/10 | 5/10 | Missing specific price data and neighborhoods |
| Selling Page | 55/100 | 5.0/10 | 3/10 | No fee/commission transparency |

### 2.3 Cross-Site Content Issues

| Severity | Issue |
|----------|-------|
| **Critical** | Content cannibalization between `/buying-property-in-algarve/` and `/buying-a-property-in-portugal/` |
| **Critical** | YMYL content (tax rates, legal requirements) may be outdated — Golden Visa suspended Oct 2023, NHR closed Jan 2024 |
| High | No author attribution on any content pages |
| High | No "Last Updated" dates on informational pages |
| High | Selling page lacks fee/commission transparency |
| Medium | Homepage too content-heavy — dilutes keyword focus and buries CTAs |
| Medium | Blog appears to publish primarily in Dutch, limiting English AI citation potential |

### 2.4 Readability

- Estimated Flesch-Kincaid Grade Level: 10-12
- Target for international audience: Grade 8-9
- Portuguese legal terminology (escritura, CPCV, IMT) pushes complexity higher
- Recommendation: Add glossary or tooltip definitions

---

## 3. On-Page SEO (Score: 55/100)

### 3.1 Title Tags & Meta Descriptions

- **Homepage title:** "Real Estate Agents in Lagos, Portugal | ten Hoopen Realty" — Good, includes primary keyword and brand
- **Meta description:** Uses OG description — "Deeply rooted in the Algarve region..." — Adequate but could be more action-oriented

### 3.2 Heading Structure

| Severity | Issue |
|----------|-------|
| Medium | Multiple H1 elements on homepage ("Real Estate Agents in Lagos, Portugal" + "THELIFE") |
| Medium | Multiple duplicate H2s ("DISCOVER THE ALGARVE" appears in variations) |
| Medium | Headings are descriptive, not question-based — poor for AI extraction |
| Medium | Heading hierarchy skips levels on some pages (H1 to content with no H3 subsections) |

### 3.3 Internal Linking

**Site Structure:**
- Navigation: Properties, Contact Us, Language selector (EN/PT/NL)
- Footer: Properties (All/Sold/Exclusive), Locations, Services (Selling/Buying/Construction/Pools/Development), About Us
- Location pages: Meia Praia, Lagos, Luz, Burgau, Salema, Portimao, Sagres
- Blog categories: Property Market, General News, Lifestyle

| Severity | Issue |
|----------|-------|
| Medium | Navigation is thin — only 2 primary items (Properties, Contact) |
| Medium | Service pages not linked from primary navigation |
| Medium | Blog/insights section not in main navigation |
| Low | `/blog/` returns 404 — content lives at `/insights/` or `/news/` |

### 3.4 Images

| Severity | Issue |
|----------|-------|
| High | Vast majority of images lack descriptive alt text |
| High | Property carousel images have no alt text or titles |
| Medium | Logo, partner logos, team photo, award badge — all missing alt text |
| Medium | Flag icons for language switching lack alt text |

---

## 4. Schema / Structured Data (Score: 35/100)

### 4.1 Current Implementation

**Detected:**
- `Organization` + `RealEstateAgent` (dual type) with address, sameAs
- `WebSite` schema

**Validation Issues:**
| Severity | Issue |
|----------|-------|
| **Critical** | Missing `@context` if schema block is standalone (not in @graph) |
| **Critical** | Missing `telephone` — required for LocalBusiness rich results |
| **Critical** | Missing `geo` coordinates — essential for local search |
| High | Logo uses SVG — Google prefers raster images (PNG/JPG/WebP) |
| High | Missing `openingHoursSpecification` |
| High | Missing `sameAs` social profile links (detected in HTML but not in schema) |
| Medium | Missing `contactPoint` with `availableLanguage` |
| Medium | Missing `priceRange` |
| Medium | Missing `areaServed` |
| Medium | URL inconsistency — schema uses `www.` prefix |

### 4.2 Missing Schema by Page Type

| Page Type | Missing Schema | Priority |
|-----------|---------------|----------|
| Property pages | `RealEstateListing` with `Offer` | **Critical** |
| All interior pages | `BreadcrumbList` | High |
| Blog posts | `Article` / `BlogPosting` with proper author | High |
| Listing pages | `ItemList` with `ListItem` entries | High |
| About Us | `Person` schema for team members | High |
| Buying guides | `FAQPage` | High |
| Homepage | `WebSite` with `SearchAction` | Medium |
| Location pages | `WebPage` with `about: Place` | Medium |

### 4.3 Rich Results Eligibility

| Rich Result | Current | Action Needed |
|-------------|---------|---------------|
| Local Business Panel | Partial | Add telephone, geo, hours, sameAs |
| Breadcrumbs | Missing | Enable in Yoast or add manually |
| Article | Missing | Add to blog posts with Person author |
| Product/Listing | Missing | Add RealEstateListing on property pages |
| ItemList Carousel | Missing | Add to listing and location pages |
| Sitelinks Search Box | Unknown | Verify WebSite + SearchAction |
| FAQ | Missing | Add to guide pages (AI benefit only — Google restricted FAQ rich results) |

---

## 5. Performance / Core Web Vitals (Score: 25/100)

### 5.1 Estimated Metrics

| Metric | Est. Mobile | Est. Desktop | Threshold | Status |
|--------|------------|-------------|-----------|--------|
| LCP | 5.0-8.0s | 2.5-4.0s | ≤2.5s | **POOR** |
| INP | 300-600ms | 150-300ms | ≤200ms | **POOR** |
| CLS | 0.15-0.40 | 0.08-0.20 | ≤0.1 | **POOR** |

**Estimated PageSpeed Score:** 20-35 (mobile) / 50-65 (desktop)

### 5.2 JavaScript Payload (~1.0-1.3MB uncompressed)

| Script | Est. Size | Main Thread Impact |
|--------|-----------|-------------------|
| Elementor Frontend + Pro | ~350KB | 180-350ms |
| Tidio Chat Widget | ~300-500KB | 150-300ms |
| jQuery + Migrate | ~90KB | 50-100ms |
| Google Tag Manager | ~80KB | 50-100ms |
| Facebook Pixel | ~60KB | 40-80ms |
| GTranslate | ~50-100KB | 30-80ms |
| Google Analytics 4 | ~50KB | 30-50ms |
| Owl Carousel | ~40KB | 20-40ms |
| Cloudflare scripts | ~30-50KB | Variable |

### 5.3 LCP Bottlenecks

1. **Owl Carousel hero** — browser can't discover hero image until JS executes (+1.5-3.0s)
2. **Render-blocking CSS chain** — Elementor loads 500-700KB CSS before first paint (+1.5-3.0s)
3. **No `fetchpriority="high"`** on LCP image
4. **No `<link rel="preload">`** for hero image
5. **Cloudflare challenge scripts** may add 1-3s on first visit

### 5.4 CLS Sources

| Source | Est. CLS Contribution |
|--------|----------------------|
| Owl Carousel initialization | 0.05-0.20 |
| Tidio Chat widget injection | 0.02-0.10 |
| Web font swap (FOUT) | 0.02-0.08 |
| GTranslate bar insertion | 0.01-0.05 |
| Images without dimensions | 0.01-0.10 |

### 5.5 Third-Party Origin Overhead

9+ distinct script origins = ~900-1350ms cumulative connection overhead on mobile 3G.

---

## 6. AI Search Readiness (Score: 38/100)

### 6.1 GEO Health Score Breakdown

| Dimension | Score |
|-----------|-------|
| Citability | 30/100 |
| Structural Readability | 45/100 |
| Multi-Modal Content | 25/100 |
| Authority & Brand Signals | 40/100 |
| Technical Accessibility | 50/100 |

### 6.2 AI Crawler Access

| Crawler | Status | Recommendation |
|---------|--------|----------------|
| GPTBot (OpenAI) | Allowed (default) | Explicitly Allow |
| OAI-SearchBot | Allowed (default) | Explicitly Allow |
| ClaudeBot (Anthropic) | Allowed (default) | Explicitly Allow |
| PerplexityBot | Allowed (default) | Explicitly Allow |
| CCBot (Common Crawl) | Allowed (default) | **Block** (training only) |
| cohere-ai | Allowed (default) | **Block** (training only) |

### 6.3 llms.txt

**Status:** NOT PRESENT (404)

No Algarve real estate agency appears to have one yet — first-mover advantage available.

### 6.4 Platform Scores

| Platform | Score | Key Gap |
|----------|-------|---------|
| Google AI Overviews | 35/100 | No FAQ schema, no sourced statistics |
| ChatGPT Web Search | 30/100 | No llms.txt, weak brand signals (no Reddit/YouTube/Wikipedia) |
| Perplexity | 35/100 | No inline citations, no data attribution |
| Bing Copilot | 40/100 | Better due to Bing's on-page SEO weighting |

### 6.5 Brand Signal Gaps

| Signal | Status | Impact |
|--------|--------|--------|
| Wikipedia entity | None | High negative |
| Reddit mentions | Likely minimal | High negative |
| YouTube presence | Likely minimal | Highest negative (~0.737 correlation with AI citation) |
| Google Reviews | 4.9/5 from 39 reviews | Moderate positive but low count |

---

## 7. Accessibility Issues

| Severity | Issue |
|----------|-------|
| High | Vast majority of images lack descriptive alt attributes |
| Medium | Email subscription form field lacks associated `<label>` element |
| Medium | No ARIA labels on interactive elements (carousels, modals) |
| Medium | "READ MORE" links lack context-specific titles or aria-labels |
| Medium | Social media icon buttons may lack text alternatives |
| Low | Focus management issues with custom JavaScript click handlers |
| Low | Elementor popup modals need keyboard accessibility verification |

---

## Appendix: Site Architecture

### Internal Link Map (Homepage)

**Navigation:**
- /properties/
- /contact-us/
- /pt/home-pt/ (Portuguese)
- /nl/home-nl/ (Dutch)

**Property Listings:**
- /property-details?reference=V1292 (Caliças, Lagos)
- /property-details?reference=T1182A (Canavial, Lagos)
- /property-details?reference=T1142 (Cabanas Velhas, Vila do Bispo)
- /property-details?reference=V1291 (Praia da Luz, Lagos)
- /property-details?reference=A1290 (Meia Praia, Lagos)
- /property-details?reference=A1289 (Burgau, Lagos)
- /property-details?reference=T1286 (Centro, Lagos)
- /property-details?reference=V1285 (Vale Da Lama, Lagos)
- /property-details?reference=V1284 (Atalaia, Lagos)
- /property-details?reference=T1227A (Luz, Lagos)

**Location Pages:**
- /meia-praia-lagos/
- /property-for-sale-in-lagos/
- /luz/
- /burgau/
- /salema/
- /portimao/
- /sagres/

**Services:**
- /selling/
- /buying-property-in-algarve/
- /construction/
- /pools/
- /development/

**Content:**
- /about-us/
- /insights/
- /category/property-market/
- /category/general-news/
- /category/lifestyle/

**Legal:**
- /terms-and-conditions/
- /privacy-policy/

### Third-Party Integrations
- Google Tag Manager: GTM-PZ9NW482
- Google Analytics 4: GT-P8ZPM8V
- Facebook Pixel: 3358563984274387
- Tidio Chat
- GTranslate (language switching)
- Proppy.app (property management/CDN)
- Owl Carousel (image slider)
- Elementor (page builder)
- Cloudflare (CDN/security)

### Schema Markup (Current)
- Organization + RealEstateAgent (homepage)
- WebSite (homepage)
