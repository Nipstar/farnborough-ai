# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is **AI Automation Farnborough** — a satellite site in a network of local SEO sites targeting different Hampshire cities. Part of Antek Automation's "Hampshire Domination" strategy for local market penetration.

**Live site:** [aiautomationfarnborough.co.uk](https://aiautomationfarnborough.co.uk)

**Parent company:** Antek Automation (Andover, Hampshire)

**Sister sites:** Andover, Portsmouth, Southampton, Basingstoke, Winchester, Hampshire-wide

## Tech Stack & Deployment

- **Zero build process** — pure HTML/CSS/JS
- No frameworks, no dependencies, no package.json
- Vanilla JavaScript for all interactions
- Google Fonts: Sora (headings) + DM Sans (body)
- Deploy by uploading files directly to static host (GitHub Pages, Netlify, Vercel, etc.)

## Architecture: Satellite Site System

### Core Principle: Content Uniqueness

**Critical for SEO:** Google penalizes duplicate content. Each satellite site must have:

1. **Identical design/structure** (CSS, animations, layout)
2. **City-specific branded content** (different wording, same information)
3. **Shared universal elements** (Antek Automation branding, Retell AI partnership, phone number)

### What Must Be Unique Per Site

These sections require completely rewritten content with city-specific context:

- Hero subheadline (reference local landmarks, business vibe)
- Pain points subtitle and card descriptions
- Services subtitle (local industry examples)
- Industries subtitle (local business context)
- "Why Choose Us" local card (use BUSINESS_VIBE)
- **All FAQ answers** (same questions, different wording/structure)
- GEO/AI statement above footer

### What Can Be Universal

These stay identical across all satellites:

- Service card bullet points (feature lists)
- Demo section (Bolt Electrical case study)
- "How It Works" 3-step process
- Industry cards (8 standard industries)
- Stats (universal metrics)
- Why Us cards (except local card)

### Brand Architecture

Each satellite maintains connection to parent:

- Footer: "Powered by Antek Automation"
- Trust bar: "Certified Retell AI Partner"
- Schema: `parentOrganization` pointing to Antek Automation
- All sites link to antekautomation.com and retellai.com/partner/antek-automation
- Shared phone: 0333 038 9960
- Unique email per site: hello@[domain]

## Key Files & Responsibilities

### index.html

Single-page site with inline CSS and JavaScript:

- **Structure:** Semantic HTML5 with proper heading hierarchy
- **SEO:** Meta tags, JSON-LD structured data (LocalBusiness, Organization, FAQPage)
- **Forms:** Contact form POSTs to n8n webhook with hidden city/source fields
- **Integrations:** Cal.com booking widget, live chatbot, AI voice demo numbers
- **JavaScript:** IntersectionObserver animations, accordion, smooth scroll nav

### Structured Data (JSON-LD)

Three schema blocks in `<head>`:

1. **LocalBusiness** — includes geo coordinates, areas served, services, parentOrganization
2. **Organization** — brand identity, links to Antek + Retell AI
3. **FAQPage** — all FAQ Q&A pairs for rich snippets

### SEO Files

- **robots.txt** — Allow all, sitemap reference
- **sitemap.xml** — Homepage + privacy + terms pages, update lastmod dates
- **Privacy/Terms pages** — Brand-specific versions of privacy-policy.html and terms.html

### Documentation

- **SATELLITE_BUILD_INSTRUCTIONS.md** — Master playbook for creating new satellite sites
  - Step-by-step transformation process
  - Variable replacement system
  - Content uniqueness checklist
  - Git workflow
  - Quality control checklist

## Common Workflows

### Editing Content

Since there's no build step, edit index.html directly:

1. Find the relevant section (e.g., hero, services, FAQ)
2. Update text while preserving HTML structure
3. Maintain city-specific branding (Farnborough references)
4. Keep Antek Automation references intact

**Example — Update hero subheadline:**
```html
<p class="hero__subheadline">
  [New Farnborough-specific description with local landmarks]
</p>
```

### Updating SEO Metadata

Update `<head>` section in index.html:

- Title (under 60 chars)
- Meta description (under 155 chars)
- Canonical URL
- OG tags (title ~55 chars, description ~130 chars)
- Twitter Card tags
- Geo tags (GB-HAM, Farnborough, lat/lng)

### Modifying JSON-LD Schema

Edit the three `<script type="application/ld+json">` blocks:

- LocalBusiness: Update address, geo coordinates, areaServed
- Organization: Update name, URL
- FAQPage: Update all 10+ FAQ Q&A pairs

**Always validate JSON-LD** after changes (use Google's Rich Results Test).

### Adding/Updating FAQs

FAQ answers must be unique across all satellites. When updating:

1. Keep the same question text
2. Rewrite answer with different sentence structure
3. Include city-specific context naturally
4. Update both the HTML accordion AND JSON-LD FAQPage schema

### Cross-Linking Between Satellites

Footer includes links to sister sites. When adding new satellite:

1. Add link in footer `.footer__satellite-links` section
2. Exclude current site from its own footer
3. Update all existing satellites to include new site

### Updating Sitemap

When adding pages, update sitemap.xml:

```xml
<url>
  <loc>https://aiautomationfarnborough.co.uk/[new-page].html</loc>
  <lastmod>2026-02-15</lastmod>
  <changefreq>monthly</changefreq>
  <priority>0.8</priority>
</url>
```

Always update lastmod dates to current date when making content changes.

## Content Strategy

### Local SEO Variables (Farnborough)

These should be woven naturally throughout content:

- **City:** Farnborough
- **Region:** Hampshire
- **Nearby towns:** Aldershot, Fleet, Camberley
- **Local landmarks:** Farnborough Aerospace Centre, Farnborough Airport, Farnborough Business Park
- **Business vibe:** Aviation/aerospace heritage, tech sector, commuter town
- **Target keywords:** AI automation Farnborough, AI voice agents Farnborough, chatbots Farnborough

### Writing Unique Content

When rewriting sections to avoid duplicate content:

1. Start sentences differently
2. Use different examples (local businesses, neighborhoods)
3. Vary sentence length and structure
4. Same information, different expression
5. Reference local landmarks naturally
6. Use Farnborough-specific context

**Bad (templated):**
> "We help businesses in [City] with AI automation."

**Good (unique):**
> "From aerospace firms at Farnborough Business Park to Fleet hospitality venues — we bring enterprise AI to Hampshire businesses."

## Testing & Validation

### Pre-Deployment Checks

- [ ] No [VARIABLE] placeholders remaining in any file
- [ ] Brand name consistent (AI Automation Farnborough)
- [ ] Domain correct in all meta tags, schema, sitemap
- [ ] Geo coordinates match Farnborough (51.2928, -0.7565)
- [ ] Email is hello@aiautomationfarnborough.co.uk
- [ ] Phone number is 0333 038 9960
- [ ] Antek Automation links intact (footer, trust bar, schema)
- [ ] Retell AI links intact
- [ ] Cross-links to sister sites (excluding current site)
- [ ] All FAQ answers rewritten (not copy-pasted from other satellites)
- [ ] Content reads uniquely, not templated
- [ ] Mobile responsive (test 320px to 1440px+)
- [ ] JSON-LD validates (Google Rich Results Test)
- [ ] Contact form hidden fields: source="aiautomationfarnborough.co.uk", city="Farnborough"

### Manual Testing

```bash
# Local preview (if using Python)
python3 -m http.server 8000

# Or use any static file server
npx serve .
```

Visit http://localhost:8000 and verify:
- Smooth scroll navigation
- FAQ accordion (single-open-at-a-time)
- Contact form validation
- Cal.com widget loads
- Stat counter animations trigger on scroll
- Mobile menu works
- All links functional

## Git Workflow

This project is **not** currently in git. To initialize:

```bash
git init
git add .
git commit -m "Initial commit: Farnborough satellite site

- Farnborough-specific branding and content
- Unique copy to avoid duplicate content penalties
- SEO optimized for Farnborough, Aldershot, Fleet
- JSON-LD structured data with Farnborough coordinates
- Cross-links to Hampshire satellite network
- Contact form with Farnborough tracking

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"

# Add remote (create GitHub repo first)
git remote add origin https://github.com/[username]/aiautomationfarnborough.co.uk.git
git branch -M main
git push -u origin main
```

### Future Commits

When making content updates:

```bash
git add index.html
git commit -m "Update [section]: [brief description]"
git push
```

For SEO updates:

```bash
git add index.html sitemap.xml
git commit -m "SEO: Update meta descriptions and lastmod dates"
git push
```

## Project-Specific Rules

### Never Change

- Antek Automation branding and links (it's the parent company)
- Retell AI partner references and links
- Shared phone number: 0333 038 9960
- Design, CSS, animations (must stay identical across satellites)
- Universal content sections (see "What Can Be Universal" above)

### Always Preserve

- UK English spelling (optimise, colour, organisation)
- JSON-LD structured data (critical for SEO)
- Semantic HTML5 structure
- Accessibility attributes (ARIA labels, alt text)
- Responsive design breakpoints

### SEO Best Practices

- Titles under 60 characters
- Meta descriptions under 155 characters
- OG titles ~55 characters, descriptions ~130 characters
- Twitter Card titles ~55 characters, descriptions ~105 characters
- H1 once per page, proper heading hierarchy
- Alt text for all images
- Internal linking structure

## Satellite Network Reference

Build order (from Hampshire Domination plan):

1. Andover (base site) — COMPLETE
2. Portsmouth (Priority 2) — COMPLETE
3. Southampton (Priority 1, 252k pop) — COMPLETE
4. Basingstoke (Priority 3, 113k pop) — COMPLETE
5. Winchester (Priority 4, 48k pop) — COMPLETE
6. **Farnborough (Priority 5, 65k pop)** — THIS SITE

Hampshire-wide site: aiserviceshampshire.co.uk

## Post-Launch Checklist

After deployment:

1. Submit to Google Search Console
2. Submit sitemap
3. Request indexing for homepage
4. Set up Google Business Profile (if possible for virtual business)
5. Submit to Bing Webmaster Tools
6. Add link from antekautomation.com
7. Monitor rankings in GSC
8. Check for keyword cannibalization between satellites

## Contact & Support

**Project Owner:** Antek Automation
**Email:** hello@antekautomation.com
**Phone:** 0333 038 9960

For detailed satellite site creation process, see SATELLITE_BUILD_INSTRUCTIONS.md.
