# SEO Action Plan: tenhoopenrealty.com

**Date:** 2026-03-23
**Current Score:** 48/100
**Target Score:** 75-85/100

---

## Priority Definitions

- **Critical**: Blocks indexing or causes penalties — fix immediately
- **High**: Significantly impacts rankings — fix within 1-2 weeks
- **Medium**: Optimization opportunity — fix within 1 month
- **Low**: Nice to have — backlog

---

## CRITICAL (Fix Immediately)

### 1. Migrate Property URLs to Clean Permalinks
**Impact:** Technical SEO, Indexability, Schema | **Effort:** High (1-2 weeks)

**Problem:** Property URLs use `/property-details?reference=XXXX`. WordPress/Yoast strips query parameters from canonical tags, so all property pages likely canonicalize to the same URL — effectively de-indexing your entire property inventory.

**Action:**
- Check if Proppy.app supports clean URL output or custom permalink structures
- Create WordPress rewrite rules mapping `/properties/{slug}/` to property detail template
- Implement 301 redirects from old `?reference=` URLs to new clean URLs
- Update internal links and XML sitemap
- Target URL format: `/properties/villa-3-bedroom-lagos-v1292/`

**Verification:** View source on any property page → check `<link rel="canonical">` includes full URL with property identifier.

---

### 2. Add Property Pages to XML Sitemap
**Impact:** Indexability | **Effort:** Medium (2-4 hours)

**Problem:** Query-parameter URLs are excluded from Yoast sitemaps by default. Property pages are the site's most valuable content and likely aren't being submitted to Google.

**Action:**
- After URL migration (item 1), property pages will naturally appear in sitemaps
- If URL migration is delayed: configure a custom sitemap that explicitly includes property URLs
- Add hreflang annotations to sitemap entries for `/pt/` and `/nl/` variants

---

### 3. Fix hreflang Implementation
**Impact:** International SEO | **Effort:** Medium (4-8 hours)

**Problem:** GTranslate likely injects hreflang tags via JavaScript only — invisible to crawlers.

**Action:**
- Verify by viewing raw HTML source (not DevTools) for `hreflang` tags
- If JS-only: add hreflang tags manually via theme `<head>` or Yoast hreflang module
- Required on every page:
  ```html
  <link rel="alternate" hreflang="en" href="https://tenhoopenrealty.com/{path}" />
  <link rel="alternate" hreflang="pt-PT" href="https://tenhoopenrealty.com/pt/{path}" />
  <link rel="alternate" hreflang="nl" href="https://tenhoopenrealty.com/nl/{path}" />
  <link rel="alternate" hreflang="x-default" href="https://tenhoopenrealty.com/{path}" />
  ```
- Add hreflang annotations to XML sitemap as well

---

### 4. Verify Proppy.app Server-Side Rendering
**Impact:** Indexability | **Effort:** Medium (2-4 hours investigation)

**Problem:** If Proppy.app loads property data via JavaScript, property content is invisible to crawlers.

**Action:**
- View page source (not Inspect Element) on `/property-details?reference=V1292`
- If property details appear in HTML: pass (server-rendered)
- If only an empty container div: investigate Proppy.app SSR options or implement dynamic rendering (Prerender.io)

---

### 5. Resolve Content Cannibalization
**Impact:** Content Quality, Rankings | **Effort:** Low (2-4 hours)

**Problem:** `/buying-property-in-algarve/` and `/buying-a-property-in-portugal/` target nearly identical keywords, splitting authority.

**Action (choose one):**
- **Option A (Recommended):** Keep buying guide as the definitive pillar. 301 redirect blog post to guide, incorporating any unique content.
- **Option B:** Differentiate by scope — guide = Algarve-specific process, blog = Portugal-wide overview. Add clear internal cross-links.

---

### 6. Audit YMYL Content for Regulatory Accuracy
**Impact:** Trust, Compliance | **Effort:** Medium (1-2 days)

**Problem:** Portuguese property regulations changed significantly in 2023-2025. Outdated YMYL content is actively harmful.

**Action:**
- Verify Golden Visa status (real estate route suspended Oct 2023)
- Verify NHR regime status (closed to new applicants Jan 2024)
- Update IMT tax brackets to current rates
- Add "Last Updated: [Month Year]" to all informational pages
- Commit to quarterly content reviews

---

## HIGH (Fix Within 1-2 Weeks)

### 7. Enhance Organization/RealEstateAgent Schema
**Effort:** Low (2-4 hours)

Add missing fields to existing schema:
- `telephone` (required for local business results)
- `geo` coordinates (latitude: 37.1028, longitude: -8.6731)
- `openingHoursSpecification`
- `sameAs` (Facebook, Instagram, LinkedIn URLs)
- `contactPoint` with `availableLanguage`
- `priceRange`
- `areaServed`
- Convert logo to `ImageObject` with raster format (PNG/JPG)

---

### 8. Add RealEstateListing Schema to Property Pages
**Effort:** Medium (4-8 hours for template)

Implement on every property detail page:
```json
{
  "@context": "https://schema.org",
  "@type": "RealEstateListing",
  "name": "...",
  "url": "...",
  "datePosted": "...",
  "image": ["..."],
  "offers": {
    "@type": "Offer",
    "price": "...",
    "priceCurrency": "EUR"
  },
  "address": { ... },
  "geo": { ... },
  "numberOfRooms": ...,
  "floorSize": { ... }
}
```

---

### 9. Add Author Bylines and Article Schema
**Effort:** Low (1 day)

- Add author names with credentials to all guide and blog content
- Format: "By [Name], Licensed Real Estate Agent (AMI 19855), [X] years in Algarve property market"
- Implement `Article` / `BlogPosting` schema with `Person` author type
- Add `datePublished` and `dateModified` (ISO 8601) to all content

---

### 10. Build Out About Us Page
**Effort:** Medium (1-2 days)

- Add individual team member bios with photos, credentials, languages, professional backgrounds
- Implement `Person` schema for each team member
- Include founding year, transaction count, countries served
- Link AMI license to IMPIC verification portal
- Add founder narrative about connection to Algarve market

---

### 11. Defer Non-Critical Third-Party Scripts
**Effort:** Medium (4-8 hours)

- Load Tidio Chat only on user click (add static chat icon that triggers full widget)
- Delay GTM tag firing for GA4 and Facebook Pixel by 5 seconds or until idle
- Defer GTranslate until after load event
- Add `async` attribute to GTM script
- Consider WP Rocket or FlyingPress for automated JS deferral

**Expected impact:** LCP improvement of 1.5-3.0s, INP improvement of 200-400ms

---

### 12. Fix LCP — Replace Carousel Hero
**Effort:** Medium (4-8 hours)

- Replace Owl Carousel hero with static `<img>` element
- Add `fetchpriority="high"` to LCP image
- Add `<link rel="preload">` for hero image in `<head>`
- Serve hero image in AVIF/WebP format
- Ensure LCP image does NOT have `loading="lazy"`

---

### 13. Add Image Alt Text Sitewide
**Effort:** Medium (1-2 days)

- Add descriptive alt text to all images (critical for accessibility and SEO)
- Property images: include property type, location, key features
- Logo: "ten Hoopen Realty logo"
- Team photo: "ten Hoopen Realty team at Lagos office"
- Partner logos: "[Company name] logo"

---

### 14. Add Security Headers
**Effort:** Low (1-2 hours via Cloudflare)

Add via Cloudflare Transform Rules:
```
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=(), geolocation=(self)
```

---

### 15. Create /llms.txt File
**Effort:** Low (2 hours)

Create file declaring:
- Company description and expertise areas
- AMI license and regulatory standing
- Key content pages for AI systems to prioritize
- Content licensing terms for AI citation
- Contact information for AI-related queries

First-mover advantage — no Algarve real estate agency likely has one yet.

---

### 16. Source All Statistics and Legal Claims
**Effort:** Medium (2-3 days)

- Link IMI rates to Autoridade Tributaria e Aduaneira
- Link IMT rates to official government schedules
- Link legal process steps to Portuguese Civil Code references
- Add "Last verified: [date]" to all data points
- Critical for AI citation — unsourced claims treated as opinions, not facts

---

## MEDIUM (Fix Within 1 Month)

### 17. Add FAQ Schema to Key Pages
**Effort:** Medium (1-2 days)

Add FAQ sections with `FAQPage` schema to:
- `/buying-property-in-algarve/` — buying process questions
- `/property-for-sale-in-lagos/` — Lagos market questions
- `/selling/` — selling process questions

Each answer: 134-167 words, direct answer first, include sourced statistics.

---

### 18. Restructure Headings as Questions
**Effort:** Low (1 day)

Convert across all guide pages:
- "Legal and Tax Requirements" → "What Are the Legal and Tax Requirements for Buying Property in Portugal?"
- "The Buying Process" → "What Are the Steps to Buying Property in the Algarve?"

Question headings directly match AI system queries.

---

### 19. Add BreadcrumbList Schema
**Effort:** Low (2-4 hours)

Enable in Yoast settings or add manually. Example:
Home > Properties > Lagos > [Property Name]

---

### 20. Add Price Data to Location Pages
**Effort:** Medium (1-2 days)

- Add specific price ranges by property type and neighborhood to `/property-for-sale-in-lagos/`
- Add neighborhood-level content with distinct H2/H3 sections
- Include dynamic property listing feed for freshness signals
- Replicate for other location pages

---

### 21. Add Fee Transparency to Selling Page
**Effort:** Low (2-4 hours)

- Explain commission/fee structure (even if ranges require consultation)
- Add specific selling process steps with timeline estimates
- Add seller-specific testimonials
- Add capital gains tax overview for non-resident sellers

---

### 22. Fix CLS Issues
**Effort:** Low-Medium (4-8 hours)

- Set explicit `min-height` on carousel container
- Add `width` and `height` attributes to all `<img>` tags
- Reserve space for GTranslate bar with CSS placeholder
- Use `font-display: optional` for decorative fonts
- Add `aspect-ratio: 4/3` to property image containers

---

### 23. Enable Cloudflare APO + Image Optimization
**Effort:** Low (1-2 hours)

- Enable Cloudflare APO ($5/month) — caches full HTML at edge, TTFB drops to 50-150ms
- Enable Cloudflare Polish with WebP/AVIF conversion
- Add `<link rel="preconnect">` for `cdn.proppy.app` and `fonts.gstatic.com`

---

### 24. Add AI Crawler Directives to robots.txt
**Effort:** Low (1 hour)

```
# AI Search Crawlers - Allowed
User-agent: GPTBot
Allow: /

User-agent: OAI-SearchBot
Allow: /

User-agent: ClaudeBot
Allow: /

User-agent: PerplexityBot
Allow: /

# AI Training-Only Crawlers - Blocked
User-agent: CCBot
Disallow: /

User-agent: cohere-ai
Disallow: /
```

---

### 25. Optimize Elementor Asset Loading
**Effort:** Low (2-4 hours)

- Enable "Improved Asset Loading" in Elementor Settings > Performance
- Enable "Improved CSS Loading" experiment
- Disable unused Elementor widgets
- Consider Perfmatters or Asset CleanUp Pro for per-page script management

---

### 26. Publish English-Language Blog Content
**Effort:** High (ongoing)

- Publish market analysis articles in English first, Dutch as translated version
- Target: "Lagos Portugal property market 2026", "Algarve real estate prices 2026"
- Each article: 2-3 citable data points with sources
- Fix `/blog/` URL (currently 404) — redirect to `/insights/` or `/news/`

---

## LOW (Backlog)

### 27. Implement IndexNow Protocol
**Effort:** Low (2-4 hours)

Enables instant URL submission to Bing/Yandex when listings change. Use Rank Math's built-in support or Microsoft's IndexNow plugin.

### 28. Create Market Data Page
**Effort:** High (1 week initial, quarterly updates)

Create `/algarve-property-market-data/` with average prices by municipality, YoY changes, transaction volumes, rental yields. Sourced from INE and Confidencial Imobiliario. Extremely high AI citation potential.

### 29. Build Reddit and YouTube Presence
**Effort:** High (ongoing)

- Reddit: participate in r/portugal, r/expats, r/digitalnomad with helpful answers
- YouTube: property tour videos, Algarve lifestyle content, buying process walkthroughs
- YouTube mentions have ~0.737 correlation with AI citation

### 30. Add Person Schema for Team Members
**Effort:** Low (2-4 hours)

Implement on About Us page linked to Organization schema.

### 31. Add ItemList Schema to Listing Pages
**Effort:** Medium (4-8 hours)

Add `ItemList` with `ListItem` entries on `/properties/` and location pages for carousel rich result eligibility.

### 32. Create Neighborhood Sub-Pages
**Effort:** High (ongoing)

If search volume justifies: `/property-for-sale-in-praia-da-luz/`, `/property-for-sale-in-burgau/`, etc.

### 33. Consider Native Portuguese Content
**Effort:** Very High (ongoing)

Replace machine-translated `/pt/` content with human-written Portuguese. A Portugal-based business should have native Portuguese as primary content for local search.

### 34. Investigate Elementor Alternatives for Key Pages
**Effort:** Very High

For landing pages with high traffic: consider rebuilding with lighter builder (GenerateBlocks, Kadence) to reduce JS payload by 60-80%.

---

## Implementation Timeline

### Week 1-2 (Critical + Quick Wins)
- Items 1-6 (critical fixes)
- Items 9, 14, 15, 23 (quick wins from High priority)
- **Expected score improvement: 48 → 58-62**

### Week 3-4 (High Priority)
- Items 7, 8, 10, 11, 12, 13, 16
- **Expected score improvement: 62 → 68-72**

### Month 2 (Medium Priority)
- Items 17-26
- **Expected score improvement: 72 → 75-80**

### Month 3+ (Low Priority + Ongoing)
- Items 27-34
- **Expected score improvement: 80 → 85+**

---

## Verification Resources

- **PageSpeed Insights:** https://pagespeed.web.dev/
- **Rich Results Test:** https://search.google.com/test/rich-results
- **Schema Validator:** https://validator.schema.org/
- **CrUX Dashboard:** https://cruxvis.withgoogle.com
- **Google Search Console:** Monitor indexing, CWV, and rich results
- **WebPageTest:** https://www.webpagetest.org/ (test from EU location)
