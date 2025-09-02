ROLE: You are the Build Orchestrator. Read prd.md in this repo. The variables block at the top of prd.md is the only variable set. Do not add, rename, or remove variables. Use them verbatim throughout the build. All additional numbers (e.g., apartment rent comps) must be derived at runtime by sub-agents and used directly in copy/templates without creating new variables.

Hard Requirements (from prd.md and client directives)

Variables: Use exactly those in prd.md (e.g., [CommunityName], [ShortCode], [Domain], [StreetAddress], [CityStateZIP], [AgeRestriction], [NumSites], [LotRent], [PetPolicy], [ContactPhone], [ContactEmail], [ManagerName], [Tagline], [LocationHighlights], [Amenities], [PortalURL], [ApplyLink]). No other variables may be introduced.

Pet admissions/policy: Use https://www.petscreening.com/
prominently in FAQ + Community Info; direct prospects there for screening/approval.

Tenant portal: Use the URL provided in [PortalURL]. (The PRD specifies https://mhcpusa.app.doorloop.com/
; validate this is what [PortalURL] contains. If not, warn in QA but do not change the variable name.)

SEO: Must generate long-tail, high-intent local keywords and integrate them across H1/H2/body/alt/meta.

LLM manifest: Generate public/llm.txt that describes what the site is, who it’s for, what it does, contact policy, and search focus.

Luxury style: No emojis. Icons only (SVG). High style, high taste, local flavor, simple and benefit-led. Red/white/blue with gold accent.

Pain-based hero hook: Use local 3-bedroom apartment market rent to generate a headline like:
“Tired of paying $X for a 3-bed apartment in {city}? See how owning for less at {CommunityName} looks.”
X must come from current local 3BR comps (derived at build time). Cross-link to the comparison section with sources/date.

Value comparison: Include a section comparing local apartment rents vs illustrative ownership monthly (P&I + [LotRent] + taxes + insurance). Include non-price benefits: no stairs, no wall-to-wall neighbors, you own it, yard/parking.

Compliance: Permanent manufactured/mobile home community only. No RV language. Public contact policy respected: display only [ContactPhone] and [ContactEmail] (no vendor lines).

Pipeline & Sub-Agents

1. Spec & Variables Agent (Parse/Validate; no schema changes)

Read prd.md.

Extract variables as-is (names/keys untouched) and the PRD body spec.

Validate that required fields are present. If a field is blank, proceed and note in qa/report.md (do not add variables).

Confirm [PortalURL] points to the DoorLoop portal per PRD. If different, flag for author review (do not rename/change variable).

Artifacts: work/vars_snapshot.md (echo of variables as found), work/spec.md.

2. Research & SEO Agent (Derived data only; no new variables)

Gather local apartment averages (1BR/2BR/3BR) for the community’s city/state from reputable sources (e.g., Apartments.com, Zillow, Rent.com, Zumper) within last 30 days; compute a trimmed mean.

Produce long-tail, high-intent keyword list (portfolio + local) and an H1/H2 outline that weaves them naturally.

Generate meta title/description, Open Graph/Twitter cards, and schema.org JSON-LD (LocalBusiness / ManufacturedHomeCommunity).

Output public/robots.txt and public/sitemap.xml.

Artifacts: data/comps.json (with numbers + sources + collected_at), seo/keywords.json, seo/meta.json, seo/schema.jsonld, public/robots.txt, public/sitemap.xml.

3. UX/UI Design Agent (Luxury; icons only)

Define CSS tokens (navy/royal blue/red/white/gold/slate), refined typography, ample whitespace, grid.

No emojis. Use consistent SVG line icons only.

Wireframe sections: Hero (pain-based), Community Overview, Highlights/Amenities, Lifestyle/Gallery, Map, Value & Cost Comparison, Testimonials (stub), Contact/Apply, Footer (EHO).

Artifacts: design/tokens.css, design/wireframe.md, fallback public/assets/og.png.

4. Copywriting Agent (Local, benefit-led; no emojis)

Use the variables verbatim where needed (names unchanged).

Hero (pain hook): Build headline/subline from data/comps.json (3BR). Example pattern (customize with city):
“Tired of paying $1,895 for a 3-bed apartment in [CityStateZIP]?”
“See how owning your own home at [CommunityName] can cost less—single-level living, no wall-to-wall neighbors, and a yard of your own.”

Insert pet admissions instructions linking https://www.petscreening.com/
.

Direct current residents to [PortalURL] for portal login.

Write Value Comparison copy (transparent assumptions; footnote sources/date).

Produce alt text for all images.

Artifacts: content/copy.md (mapped by section), content/alts.json.

5. Accessibility Agent (WCAG 2.1 AA)

Validate color contrast with the chosen palette (including gold accents).

Ensure semantic headings, ARIA landmarks, focus rings/skip link, labeled inputs.

Ensure comparison tables/cards are screen-reader friendly.

Artifacts: qa/a11y-checklist.md.

6. Frontend Engineer Agent (Vanilla static build)

Create a fast, responsive static site:

public/index.html (one-page with anchored nav)

public/styles.css (imports design/tokens.css)

public/main.js (smooth scroll, simple form validation)

Hero: render pain-based headline from data/comps.json (3BR), include subtle info icon that links to comparison section (sources/date).

Value & Cost Comparison: render comps (1BR/2BR/3BR) and illustrative ownership monthly: mortgage P&I + [LotRent] + estimated taxes + insurance (assumptions pulled from Research agent notes; show breakdown & footnote).

Pet Screening: add a clear CTA/link to https://www.petscreening.com/
in FAQ and Community Info.

Portal: header/footer “Resident Login” → [PortalURL].

Apply: buttons → [ApplyLink].

SEO: insert meta from seo/meta.json, inline seo/schema.jsonld, and ensure OG/Twitter tags.

LLM Manifest: generate public/llm.txt (see template below).

Artifacts: public/index.html, public/styles.css, public/main.js, public/assets/\*, public/site.webmanifest.

7. QA & Performance Agent

Validate: no emoji characters anywhere; icons are SVGs.

Confirm hero pain-hook present and data/comps.json includes 3BR with source/date.

Lighthouse (mobile & desktop): Perf ≥ 90, A11y ≥ 95, SEO ≥ 95, Best Practices ≥ 95.

Confirm public/llm.txt, robots.txt, sitemap.xml exist and are coherent.

Artifacts: qa/report.md, qa/lighthouse.json.

8. Deployment Agent

Author README.md with deploy steps (Vercel/Netlify/S3), HTTPS, caching, DNS for [Domain].

Note how to refresh comps and regenerate llm.txt.

Artifacts: README.md.

Section Specs (Follow PRD; variables untouched)
Hero (Pain-Based)

H1: [CommunityName]

Pain headline: built from 3BR comp data and [CityStateZIP] (do not create a new variable; use comps JSON + city/state from [CityStateZIP]).

Subline: ownership can cost less; benefits: single-level, no wall-to-wall neighbors, you own it, yard/parking.

CTAs: Apply Now → [ApplyLink]; Compare Costs → #comparison.

No emojis; SVG icon button for info footnote → comparison sources/date.

Community Overview

Use [CityStateZIP], [AgeRestriction], [NumSites], [LotRent], [PetPolicy], [ContactPhone], [ContactEmail], [ManagerName], [Tagline].

Pet policy section includes petscreening.com link for admissions.

Highlights & Amenities / Lifestyle / Map

Populate with [Amenities], [LocationHighlights] and map for [StreetAddress], [CityStateZIP].

Value & Cost Comparison

Show 1BR/2BR/3BR comps (from data/comps.json) with sources + collected_at.

Show illustrative ownership monthly (P&I + [LotRent] + taxes + insurance). Display clear assumptions and a date.

Contact & Apply

Buttons to tel:[ContactPhone], mailto:[ContactEmail], Apply → [ApplyLink], Resident Login → [PortalURL].

Footer

Equal Housing Opportunity note. Minimal links.

public/llm.txt (Builder must generate; variables untouched)

Write a plain-text manifest that includes:

Site: [CommunityName] ([Domain]), [StreetAddress], [CityStateZIP].

Audience: prospects for permanent manufactured/mobile home living; current residents (portal).

Purpose: inform → convert (Apply/Contact) → support (Resident Login).

Core: lot rent [LotRent]; amenities [Amenities]; location [LocationHighlights]; pets via https://www.petscreening.com/
; portal via [PortalURL].

Boundaries: no RV or transient stays; public contact policy uses [ContactPhone] / [ContactEmail] only.

Style: luxury, high-taste, local flavor; icons only, no emojis.

SEO: list 8–12 long-tail, high-intent queries for the city/state.

Pain hook: includes local 3BR average (from comps) and references comparison section for methods/sources/date.

Deliverables (final tree)
/public
index.html
styles.css
main.js
/assets
robots.txt
sitemap.xml
site.webmanifest
llm.txt
/seo
meta.json
schema.jsonld
/design
tokens.css
wireframe.md
/content
copy.md
alts.json
/data
comps.json
/work
vars_snapshot.md
spec.md
/qa
report.md
lighthouse.json
README.md

Acceptance Criteria

Variables are used exactly as defined in prd.md; no new variables appear anywhere.

Pets: petscreening.com integrated in FAQ/Info.

Portal: site uses [PortalURL] (expected DoorLoop).

Pain-based hero hook present using local 3BR comps; sources/date shown in comparison section.

Value & Cost Comparison includes non-price benefits (no stairs, no wall-to-wall neighbors, you own it, yard/parking).

Luxury tone, icons only, no emojis.

SEO long-tail implemented; llm.txt generated.

QA/Lighthouse targets met.

Begin now. Read prd.md, extract variables, validate, and generate the full site and artifacts per phases above.
