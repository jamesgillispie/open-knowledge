---
type: reference
title: "Technical Site Audit: Taylor Wessing"
description: AREA 17 technical audit of taylorwessing.com covering platform, stack, integrations, accessibility, SEO, and security.
tags:
  - client
  - winston-taylor
  - area17
---
# Technical Site Audit: Taylor Wessing

**URL:** https://www.taylorwessing.com/en/
**Date:** February 11, 2026
**Prepared by:** AREA 17 Technology
**RFP context:** No RFP context provided. This is a general technical assessment of the current site.

---

## Executive Summary

Taylor Wessing's website runs on Sitecore CMS (.NET) hosted on Microsoft Azure, serving a large international law firm with offices across 15+ European and Asian markets. The site supports four language versions (English, German, French, Traditional Chinese) and contains extensive content across people profiles, legal expertise areas, insights/publications, and office locations. The underlying technology is functional but carries meaningful technical debt: jQuery-dependent front-end code, a monolithic CSS/JS build pipeline, and a Sitecore implementation that shows its age in the markup patterns and asset management approach.

The most significant opportunity for AREA 17 lies in the gap between the firm's brand ambition and the site's execution. The current front-end is template-driven and utilitarian. Navigation is dense but not sophisticated. Content architecture is deep but the presentation layer doesn't do the work justice. A redesign and replatform would be substantial in scope given the multilingual infrastructure, the volume of content (thousands of people profiles, insights articles, and expertise pages), and the integration surface area. The people search alone appears to be a custom Sitecore-powered faceted search system that would need careful migration planning.

Red flags for scoping: the site has empty meta descriptions across key pages (homepage included), several accessibility issues in the navigation markup, and the Sitecore Forms integration carries a noted jQuery conflict that the dev team has worked around with manual script injection. The CSP header is comprehensive but extremely verbose, suggesting incremental policy additions over time rather than principled governance. The overall picture is of a site that works but hasn't received a ground-up technical investment in some time.

---

## Platform and CMS

The site is built on Sitecore XP (Experience Platform), identifiable through multiple signals: the `/sitecore/` and `/sitecore modules/` paths in robots.txt, the Sitecore Experience Forms scripts loaded on every page, Sitecore media library URL patterns (`/-/media/taylor-wessing/...`), and the `.ashx` handler extensions used for sitemaps. The specific version is not exposed in headers, but the markup patterns (Experience Forms v2 scripts, the media handler query string conventions) are consistent with Sitecore 9.x or 10.x.

Hosting is on Microsoft Azure. The response headers include `x-azure-ref` identifiers, Azure Front Door caching headers (`x-cache: CONFIG_NOCACHE`), and the Application Insights JavaScript SDK is embedded on every page with an instrumentation key. The `request-context` header confirms an Azure Application Insights deployment.

The site is explicitly configured with `cache-control: no-cache, no-store` on HTML responses, which means every page load hits the origin. This is unusual for a largely static content site and may indicate either a Sitecore personalization dependency or simply a conservative caching policy that's hurting performance.

## Tech Stack

The front-end is jQuery-based. A custom minified bundle (`jquery.tw.min.js`) is loaded synchronously in the `<head>`, which blocks rendering. jQuery Validate and jQuery Validate Unobtrusive are loaded separately for Sitecore Experience Forms, with an inline HTML comment noting a deliberate workaround for a jQuery version conflict.

CSS is delivered as a single minified bundle (`app.min.css`) with cache-busted query strings based on content hashes. A separate print stylesheet is loaded. The CSS approach uses BEM-style class naming (`.navbar--brand`, `.section--main-wrapper`, `.navbar--dropdown__primary`) that's consistent but suggests a custom build rather than a framework like Bootstrap or Tailwind. SVG assets are inlined for the logo. Images from the Sitecore media library use query-string-based transformation parameters.

There's no evidence of a modern JavaScript framework (React, Vue, etc.) or module bundler output. The asset paths (`/assets/dist/`) suggest a Gulp or Grunt build pipeline. No source maps are exposed. Font loading happens through external services (MyFonts via `hello.myfonts.net`, Google Fonts). The `<head>` is heavy with render-blocking scripts: jQuery, jQuery Validate, Optimizely, GTM, Cookiebot, and a large inline Application Insights snippet all load before any content renders.

## Integrations

The integration footprint is extensive, as visible in both the page source and the very detailed Content Security Policy header:

- **Analytics:** Google Tag Manager (GTM-5HS35NL), Google Analytics (both UA and GA4 endpoints whitelisted), Microsoft Application Insights (Azure Monitor), Siteimprove Analytics
- **A/B testing and personalization:** Optimizely Web (project ID 27617570016)
- **Consent management:** Cookiebot (with auto-blocking mode)
- **Video:** Vimeo player embeds, with Akamai CDN adaptive streaming support
- **Podcasts/audio:** Buzzsprout, Podigee, SoundCloud, Apple Podcasts, Spotify
- **Forms and surveys:** Sitecore Experience Forms, Typeform embeds, Microsoft Forms (Office 365)
- **Maps:** Google Maps (API and static maps)
- **Marketing/CRM:** LinkedIn (LiDAM pixel, Oribi), Google Ads (doubleclick.net, googleadservices), Hotjar (session recordings/heatmaps)
- **Email:** Vuture (sites-taylor-wessing.vuturevx.com), Newsmailservice
- **Interactive content:** BRYTER (decision automation), Fliplet, Foleon, Plotly charts, Livestorm (webinars)
- **Conferencing:** Zoom (embedded meeting/event frames)
- **External content:** Lookerstudio (Google Data Studio) dashboards, YouTube embeds
- **Advertising tracking:** secure.visionary-enterprise-ingenuity.com (likely an ad attribution service)

This is a significant integration surface area. Any replatform would need to account for preserving or migrating each of these connections, and several (BRYTER, Fliplet, Vuture) are niche platforms that may have Sitecore-specific integration patterns.

## Accessibility

The navigation uses some ARIA patterns correctly: dropdown menu buttons have `aria-controls` and `aria-expanded` attributes linking to their corresponding menu panels. The logo link has an `aria-label`. Images in the navigation use `loading="lazy"` and most have `alt` text, though at least one nav icon has an empty `alt` attribute (the Real Estate sector icon).

Several concerns are visible in the source:

The `<body>` tag appears inside the `<head>` section in the HTML source (after `<head>` content but before a closing `</head>` tag), which is an HTML validation error that browsers will auto-correct but indicates sloppy template management. The `<span class="tag">` elements used as section headers within dropdown menus (`Locations`, `Groups & regions`) are not semantically meaningful and aren't associated with the lists they label via ARIA. The skip navigation pattern is absent. Form labels for the people search couldn't be fully assessed from the server-rendered HTML alone, as the search appears to be JavaScript-driven.

Meta descriptions are empty on the homepage, about page, insights page, and people page. While this is primarily an SEO issue, it also affects how screen readers announce page purpose in some contexts.

A more comprehensive accessibility audit with tooling would be needed, but the visible patterns suggest WCAG AA compliance has not been a systematic priority.

## SEO

Canonical URLs are properly set on all pages examined. Hreflang tags are correctly implemented across the four language versions (en, de, fr, zh-Hant) with x-default pointing to the English version. The sitemap infrastructure is functional: a sitemap index at `/sitemapindex.ashx` links to per-language sitemaps, and the robots.txt correctly references it.

The robots.txt is thorough in blocking Sitecore system paths and query-string-based duplicate content (search results, filtered views, locale parameters). This is well-configured.

The critical SEO deficiency is empty meta descriptions on major pages. The homepage `<title>` is simply "Taylor Wessing" with no qualifying text. Open Graph tags are present but minimal (title, type, URL) with no OG images or descriptions. Structured data is limited to a basic Organization schema on every page with just the name, URL, and logo. There's no breadcrumb schema, no Article schema on insights pages, and no Person schema on people profiles, all of which are missed opportunities for a site of this type.

URL structure is clean and hierarchical (`/en/expertise/services/artificial-intelligence`, `/en/global-reach/countries/germany`). The language prefix pattern is standard and correct.

## Security

HTTPS is enforced with `strict-transport-security: max-age=31536000; includeSubDomains`, which is properly configured. `X-Frame-Options: SAMEORIGIN`, `X-XSS-Protection: 1; mode=block`, and `X-Content-Type-Options: nosniff` are all present.

The Content Security Policy is notably comprehensive but extremely permissive in places. The `script-src` directive includes `'unsafe-inline'` and `'unsafe-eval'`, which substantially weakens the CSP's protection against XSS. The `img-src` directive includes a wildcard list of essentially every Google country domain (hundreds of entries), which appears to be a brute-force approach to supporting Google Ads conversion pixels rather than a targeted policy. The CSP also includes a `report-uri` pointing to `taylorwessing.report-uri.com`, indicating they are monitoring violations, which is good practice.

The Application Insights instrumentation key (`83307743-97f5-4c6e-9188-58a442f5bc4a`) is exposed in inline JavaScript. While this is normal for client-side telemetry SDKs, it's worth noting. No other obvious credential exposures were observed.

Cookie consent is managed by Cookiebot in auto-blocking mode, which is the GDPR-compliant approach. The GTM script is explicitly tagged `data-cookieconsent="ignore"` to bypass consent for the initial GTM container load.

## Subdomains and Related Properties

The CSP and page source reveal several related properties:

- **sites-taylor-wessing.vuturevx.com** - Vuture email marketing platform
- **v6.newsmailservice.de** - German email/newsletter service
- **taylorwessing.foleon.com** - Foleon digital publishing platform
- **tw.bryter.io** - BRYTER decision automation tools
- **taylorwessing.report-uri.com** - CSP violation reporting endpoint

The hreflang implementation confirms four language versions all served from the main domain under language prefixes (`/en/`, `/de/`, `/fr/`, `/zh-hant/`). No separate regional subdomains were detected.

The CSP's `frame-src` whitelist suggests content is embedded from a wide range of third-party platforms (Typeform, Livestorm, Fliplet, Podigee, SoundCloud, Spotify, Apple Podcasts), indicating the content team relies heavily on embedded widgets rather than native functionality.

## Content Architecture

The site is organized around a clear information hierarchy:

- **About us** - Firm overview (General Page type)
- **People** - Lawyer directory with faceted search (People Search type)
- **Expertise** - Split into Sectors (15 industry verticals, 4 featured with icons) and Legal services (24 practice areas)
- **Locations** - Geographic directory covering Europe (15 countries), Middle East (3), Asia (5), plus regional groups and desk pages
- **Insights and events** - Publication listing with filtering (Listing Page type)
- **Careers** - Recruitment content

The `data-page-type` attribute on the body tag reveals distinct template types: Home Page, General Page, People Search, Listing Page. This suggests a Sitecore template hierarchy with at least these distinct renderings.

Navigation is dense. The mega-menu packs in all 15 sectors, 24 legal services, 15+ countries, and regional groups. This works functionally but the depth means users face significant cognitive load, particularly on the Expertise dropdown where Legal services is a single flat list of 24 items.

The i18n implementation is solid at the infrastructure level. Four full language versions with proper hreflang tags and a shared URL structure. The Chinese (Traditional) version notably does not have an hreflang entry on the People page, suggesting incomplete translation coverage. The French version is similarly absent from the People page hreflang tags.

Content volume is substantial. The sitemap index points to four language-specific sitemaps, and given the depth of people profiles, insights articles, and expertise pages visible in the navigation, the total page count likely runs into the tens of thousands.

---

## Opportunities

This is a textbook candidate for a ground-up redesign and potential replatform. The content is strong (a major international law firm with deep expertise pages, thousands of lawyer profiles, and an active insights program), but the presentation layer is dated and the technical implementation shows accumulated compromises.

If the scope includes a CMS migration away from Sitecore, Twill/Laravel would be a natural fit. The content model is editorial/institutional at its core: structured people profiles, taxonomy-driven expertise pages, multilingual content with regional variations, and a heavy publication workflow. This maps directly to Twill's strengths in content modeling and AREA 17's deep expertise with the platform. The Vitrine design system would provide a strong foundation for the component library.

If they want to stay on Sitecore or if budget constrains the platform conversation, there's still substantial front-end modernization work: replacing jQuery with a modern JS approach, implementing proper code splitting to eliminate the render-blocking script chain, introducing a design system to replace the ad-hoc component CSS, and addressing the empty-meta-description problem across the site.

The people search is likely the single most complex feature to scope. The current implementation is JavaScript-driven with faceted filtering across multiple dimensions, and any migration would need to preserve or improve this functionality. A headless search service (Algolia, Elasticsearch) would be a significant upgrade over whatever Sitecore is doing now.

The integration surface area creates both complexity and opportunity. Many of the embedded third-party tools (BRYTER, Fliplet, Foleon) could potentially be replaced with native CMS functionality, reducing the external dependency footprint and improving the user experience.

## Red Flags for SOW

**Empty meta descriptions across the entire site.** Every major page examined (homepage, about, people, insights) has an empty `<meta name="Description">` tag. This is a significant SEO deficiency for a site that presumably relies on organic search for business development. It should be flagged as a quick win regardless of the project scope.

**Render-blocking script chain.** jQuery, jQuery Validate, Optimizely, GTM, Cookiebot, and Application Insights all load synchronously or semi-synchronously in the `<head>`. This is measurably harming page load performance. The manually injected Sitecore Forms scripts with the jQuery conflict workaround suggest the front-end is fragile.

**No-cache headers on all HTML.** The `cache-control: no-cache, no-store` policy means Azure Front Door cannot serve cached pages. For a content site with relatively infrequent updates, this is likely leaving significant performance on the table. If this is driven by Sitecore personalization requirements, that dependency needs to be understood before proposing alternatives.

**Integration dependency mapping required.** The 20+ third-party integrations visible in the CSP create a complex dependency graph. The SOW needs to account for discovery work to understand which integrations are actively used, which can be consolidated, and which have Sitecore-specific hooks that would need migration.

**Incomplete i18n coverage.** The People page and possibly other sections are not fully translated across all four languages. If the project scope includes the multilingual infrastructure, the actual translation coverage gaps need to be mapped during discovery.

**HTML validation issues.** The `<body>` tag placement within the `<head>` section, while browsers handle it gracefully, signals template-level quality issues in the Sitecore rendering pipeline that may surface other problems during detailed technical discovery.

**Accessibility gaps.** No skip navigation, inconsistent ARIA labeling in menus, empty alt attributes. For a firm that advises clients on regulatory compliance, the site's own accessibility posture could be a reputational concern. Any redesign should target WCAG 2.1 AA as a baseline.
