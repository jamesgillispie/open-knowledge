---
type: note
title: Project Meridian — Launch Checklist
description: Phased launch tracker for winstontaylor.com with A17, WT IT, and Other WT ownership columns.
tags:
  - client
  - winston-taylor
  - area17
---
# Project Meridian — Launch Checklist

Internal working doc, A17. Status: first-draft sweep, owners and dates to be assigned. Living document.

## What this is

A single tracker for everything that needs to be true on launch day for winstontaylor.com to actually launch, plus the immediate post-launch monitoring window. Organised by phase (pre-launch / launch / post-launch) with three ownership columns: A17 (us), WT IT (Sunil, Frank — technical infrastructure), and Other WT (Jenny on WS content, Sara on TW, Holly on consent, WT legal on policies, etc.).

Conventions:

- `[]` open, `[x]` done, `[~]` in progress, `[!]` blocked
- Owner shown inline as → name. Multiple names = shared
- Timing shown inline as T-Xw (weeks before launch) or T+Xd (days after launch)
- Items marked CRITICAL are launch blockers

Launch target is June 1. Markdown tables get wide with this much content — for daily use, this should move to Notion where the three columns render naturally as a kanban or database view. The structure below is built to import cleanly.

---

## Pre-launch

### A17

**SEO, indexing, content discovery**
- [ ] sitemap.xml live on production → Quentin → T-2w
- [ ] robots.txt configured for production → Quentin → T-2w
- [ ] robots.txt on staging confirmed still blocking → Quentin → ongoing
- [!] Empty `<title>` tags populated sitewide (CRITICAL) → Quentin → T-3w
- [ ] Canonical URL set per page → Quentin → T-3w
- [ ] Trailing-slash canonical 301 rule (Fastly VCL) → Quentin → T-2w
- [ ] `/insights-and-events` vs `/articles` canonical decision → Settie, Quentin → T-3w
- [ ] Structured data implemented (Organization, Person, Article, BreadcrumbList) → Quentin → T-3w
- [ ] Open Graph and Twitter Card meta → David, Quentin → T-3w
- [ ] 404 page designed and built with site search → David, Quentin → T-2w
- [ ] 410 handling implemented → Quentin → T-2w

**Redirects and URL handling**
- [x] WS-side architectural foundation: Fastly stays as edge → Luis (confirmed)
- [ ] WS-side pattern decision locked: Pattern 2 recommended → James, Quentin, Ashley → T-3w
- [ ] Quentin's purging strategy answer → Quentin → T-2w
- [ ] Redirect rules source-of-truth committed → Quentin → T-2w
- [ ] Twill redirects capsule built → Joyce, Quentin → T-2w
- [ ] Floor-level mappings written → A17 → T-2w
- [ ] Redirect test harness in CI → Quentin → T-1w
- [ ] `?nocache` bypass rule in Fastly VCL → Quentin → T-2w
- [ ] Crawl winston.com to extract bio and article URLs → James, Quentin → T-3w
- [ ] Joyce confirms slug normalization rules → Joyce → T-3w

**Cache and performance**
- [ ] Surrogate-key purging tied to Twill model events → Quentin → T-2w
- [ ] Core Web Vitals budget met → Quentin → T-2w
- [ ] Image optimization pipeline confirmed → Quentin → T-2w
- [ ] CDN warmup script for post-deploy → Quentin → T-1w

**Security and monitoring**
- [ ] Fastly WAF rules configured → Quentin, Luis → T-2w
- [ ] Rate limiting on form endpoints → Quentin → T-2w
- [ ] HTTPS / HSTS → Quentin → T-3w
- [ ] Security headers (CSP, X-Frame-Options, etc.) → Quentin → T-2w
- [ ] Sentry error tracking → Quentin → T-2w
- [ ] Uptime monitoring → Quentin → T-1w
- [ ] On-call rota for launch day and T+1 week → Luis, Ashley → T-1w
- [ ] A17 application-layer monitoring scope documented → Luis, Ashley → T-2w

**Search**
- [ ] Meilisearch indexed and live → Quentin → T-2w
- [ ] Search relevance tested on real queries → Settie, Joyce → T-2w
- [ ] Algolia abstraction layer in place → Quentin → T-3w
- [ ] Search analytics wired up → Quentin → T-1w

**Integrations**
- [ ] SSO providers configured → Quentin → T-2w
- [ ] Careers routing live (bridging page) → Quentin → T-2w
- [ ] WS careers (viRecruit) link tested → Joyce → T-2w
- [ ] TW careers link tested → Joyce → T-2w

**Analytics build**
- [ ] GTM container deployed → A17 → T-2w
- [ ] GA4 configured with cross-domain tracking → A17 → T-2w
- [ ] Consent Mode v2 wired to OneTrust → A17 → T-1w
- [ ] Conversion events firing → A17, Holly → T-1w
- [ ] SRA badge HTML embed in CMS-editable region → Quentin → T-1w
- [ ] OneTrust cookie scan run, cookies categorized → A17 → T-1w

**Accessibility**
- [ ] WCAG 2.1 AA audit complete → David, Quentin → T-2w
- [ ] Keyboard navigation tested → David → T-2w
- [ ] Screen reader tested → David → T-2w

**Navigation and core UX gaps**
- [!] Site search wired up (CRITICAL) → Quentin → T-2w
- [!] `/contact-us` page exists (CRITICAL) → Joyce, Quentin → T-2w
- [ ] Header vs footer nav reconciled → Settie, David → T-3w
- [ ] `/people` facet URLs decision → Settie, Quentin → T-3w

**CMS build**
- [!] Capabilities detail pages decision (CRITICAL) → Settie, Quentin
- [ ] Twill user access provisioned for client editors → James, Joyce → ongoing
- [ ] Sara Sartorius's CMS access issue resolved → James → in progress
- [ ] Editorial workflow / publishing roles documented → Joyce → T-1w
- [ ] File download block scoped (Quentin's proposal) → Quentin, David → T-3w

**CI/CD and deployment**
- [!] GitLab → Upsun SSH key auth unblocked → Quentin → blocking
- [ ] Manual deploy fallback documented → Quentin → T-2w
- [ ] Environment promotion path documented → Quentin → T-2w
- [ ] Rollback procedure documented and tested → Quentin → T-1w

**Cutover planning**
- [ ] Launch coordination meeting scheduled → Ashley, James → T-2w
- [ ] DNS records mapped out (which change, what order, what TTLs) → James, Quentin → T-3w
- [ ] Cutover runbook written → James, Quentin → T-1w

**IA decisions (A17-owned, blocking)**
- [!] New IA / URL structure locked for capabilities, people, insights, about, locations, careers → Settie, Quentin → blocking

### WT IT

**Cloudflare and DNS**
- [ ] Cloudflare access provisioning for A17 per access proposal → Sunil, Frank → T-3w
- [ ] CF access extended to winston.com zone → Sunil, Frank → T-3w
- [ ] TTLs lowered on critical DNS records (1h or less) → WT IT → T-1w
- [ ] Winston-Taylor placeholder microsite — decommissioning plan → WT IT → T-1w

**Email and integration DNS**
- [ ] Email sending domain records: SPF, DKIM, DMARC → WT IT (with Joyce) → T-3w
- [ ] Vuture CNAMEs configured → WT IT (with Joyce) → T-3w
- [ ] Vanity URLs for Vuture (preference center, unsubscribe) under winstontaylor.com subdomain → WT IT (with Joyce) → T-3w

**SSO**
- [ ] OAuth client IDs / secrets from WS IT → WT IT → T-3w
- [ ] OAuth client IDs / secrets from TW IT → WT IT → T-3w

**Platform**
- [ ] Upsun 24/7 SOC coverage confirmed (P1 at 30-min response) — Luis to confirm with Upsun → T-3w

### Other WT

**WS content (Jenny)**
- [ ] All WS bios migrated and reviewed → Jenny → T-2w
- [ ] Final WS content batch from 4/15–5/15 imported → Jenny → T-1w
- [ ] WS staff email migration CSV provided (due May 15) → Jenny → T-2w
- [ ] Departed individuals removed → Jenny → T-2w
- [ ] 301/410 triage on Jenny's 800 WS URLs → Jenny → T-2w
- [ ] Departed-individual bios mapped to 410 → Jenny → T-2w
- [ ] Bio and article inventory extended (or A17 crawls) → Jenny → T-3w
- [ ] Test/placeholder articles culled (`/articles/test-123` etc.) → Jenny → T-2w

**TW content (Sara)**
- [ ] All TW UK bios migrated → Sara → T-2w
- [ ] Test/placeholder events removed and replaced → Sara, Jenny → T-2w
- [ ] About page placeholder copy replaced ("XX practice areas") → Sara, Jenny → T-2w
- [ ] Jo Joyce duplicate URLs resolved → Jenny, Sara → T-2w
- [ ] Honorific slug rule codified → Jenny, Sara → T-2w

**TW UK SEO migration**
- [!] TSA clarification on taylorwessing.com URL handling → Sara, WT legal → blocking
- [!] Content rights negotiation with TW EU parent → Sara, WT legal → blocking
- [ ] TW UK content inventory built → Sara → T-3w
- [ ] Unpublish coordination plan with EU parent → Sara → T-2w
- [ ] GSC access on taylorwessing.com confirmed → Sara → T-3w
- [ ] Manual recrawl trigger list (top 100 TW UK URLs) → Sara → T-1w
- [ ] External link outreach plan: scope, owner, target list → TBD → T-2w (unowned)

**Consent and analytics**
- [!] OneTrust CMP provisioned (CRITICAL, May 18) → Holly, Claire Bussey
- [ ] analytics@area17.com access granted on OneTrust → Holly → T-2w
- [ ] Yoshki's GA usage flagged for Holly's consent review → James → T-2w

**Marketing infrastructure**
- [ ] Vuture HTML export workflow validated → Rose, Joyce → T-2w
- [ ] Vuture platform access for Joyce → Rose → T-3w
- [ ] Vuture → OnePlace form routing tested (TW) → Sara, Joyce → T-2w
- [ ] Nexl form routing tested (WS) → Jenny, Joyce → T-2w
- [ ] DealCloud role in TW form data flow clarified → Sara → T-3w

**Regulatory (SRA)**
- [ ] SRA registration via mySRA portal → Sarah, Kirsty → T-2w

**Legal and policy content**
- [!] Footer policy links wired to real pages (CRITICAL) → WT legal, Quentin → T-1w
- [ ] Privacy policy content provided → WT legal → T-1w
- [ ] Terms of use content provided → WT legal → T-1w
- [ ] Cookie policy content provided → WT legal → T-1w
- [ ] Legal disclaimer content provided → WT legal → T-1w
- [ ] Fraud & scams content provided → WT legal → T-1w
- [ ] Accessibility statement content provided → WT legal → T-1w
- [ ] Modern Slavery statement (UK) content provided → WT legal → T-1w

---

## Launch (T-day)

The minute-by-minute runbook expands closer to the date out of the launch coordination meeting with Sunil and Frank. Below is the structural sequence by side.

### A17
- [ ] Cache warmup script executed → Quentin → T+0
- [ ] Smoke tests on production (homepage, sections, forms, search, login) → A17 → T+0
- [ ] Redirect test harness run against live production → Quentin → T+0
- [ ] OneTrust cookie banner verified live and functional → A17 → T+0
- [ ] GSC sitemap submitted → James → T+0
- [ ] Bing Webmaster Tools submission → James → T+0
- [ ] SRA Digital Badge verified rendering on live URL → A17 → T+0
- [ ] On-call standby for first 4 hours post-cutover → Quentin, Luis → T+0
- [ ] Comms standby: error alerts piped to launch-day channel → Quentin → T+0

### WT IT
- [ ] DNS cutover executed in defined sequence → Sunil, Frank → T+0
- [ ] Legacy DNS records confirmed in expected state (winston.com handoff, etc.) → Sunil, Frank → T+0

### Other WT
- [ ] Pre-cutover content freeze on legacy WS → Jenny → T-1d
- [ ] Pre-cutover content freeze on TW UK → Sara → T-1d
- [ ] Pre-cutover backup snapshots of legacy systems → Jenny, Sara → T-1d
- [ ] Comms: launch announcement to WT internal stakeholders → Ashley, Colleen → T+0
- [ ] Comms: external press if applicable → WT marketing → T+0 (separate plan)

---

## Post-launch

### A17
**T+1 day**
- [ ] 404 monitoring review → A17 → T+1d
- [ ] Form submission spot check → Joyce → T+1d
- [ ] GA4 / GTM sanity check → A17 → T+1d
- [ ] Error tracking review (Sentry) → Quentin → T+1d

**T+1 week**
- [ ] Search Console crawl status review → James → T+1w
- [ ] Core Web Vitals real-user data review → Quentin → T+1w
- [ ] Inbound link 404 audit (legacy URLs still being hit) → A17 → T+1w
- [ ] Redirect map gap review based on observed traffic → A17 → T+1w

**T+1 month**
- [ ] Search rankings comparison vs pre-launch baseline → A17 → T+1m
- [ ] Redirect rules audit based on observed traffic → A17 → T+1m
- [ ] Performance baseline review → Quentin → T+1m

### WT IT
**T+1 week**
- [ ] DNS record cleanup (any legacy records that can be retired) → WT IT → T+1w
- [ ] TTLs restored to standard values after cutover stability → WT IT → T+1w

### Other WT
**T+1 day**
- [ ] Internal stakeholder feedback collection → Ashley, Colleen → T+1d

**T+1 week**
- [ ] Fastly console familiarisation (via Upsun) for WT marketing/IT → Holly → T+1w
- [ ] Twill CMS familiarisation review (how editors are getting on) → Joyce → T+1w

**T+1 month**
- [ ] TW UK URL de-indexing progress check (from taylorwessing.com) → Sara → T+1m
- [ ] External link outreach progress check → TBD (unowned) → T+1m

---

## Cross-cutting items

These don't belong to a single phase or column — standing concerns to track through.

- [ ] Ashley's redirect strategy spreadsheet from May 5 — fold in once it lands → Ashley
- [ ] Stakeholder launch sign-off gate: who explicitly signs go/no-go (Holly on consent, WT legal on policies, Ashley/Colleen on commercial, Luis on engineering, James on overall) → Ashley to define → T-1w
- [ ] Incident comms plan: if P1 fires on launch day, who calls who in what order → Luis, Ashley → T-1w

---

## Things explicitly NOT in this list

These came up in scope conversations but aren't launch blockers:

- Algolia migration (Phase 2)
- Cloudinary for DAM (Phase 2)
- Multilingual support: German, French, Traditional Chinese (Phase 2)
- Entegrata sync (Phase 2)
- DealCloud direct API integration (deferred)
- Bio data long-term source-of-truth decision (future conversation)

---

## Currently unowned items

Items above with no clear owner that need one assigned before T-2w:

- External link outreach workstream for TW UK side
- Stakeholder launch sign-off gate definition
- Launch day external comms plan (if any)

---

## How to use this

Move to Notion this week. The three-column structure becomes a kanban board or a database with an owner property — same shape, much more workable than a markdown table. The phase + column structure should travel cleanly. Once we have owners on everything, the `[!]` blocked items become the standing weekly conversation, and the rest is execution.
