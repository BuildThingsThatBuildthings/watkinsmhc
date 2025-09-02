# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static website project for Watkins MHC (Manufactured Home Community) in Watkins, MN. The project creates a luxury, high-taste marketing website that positions manufactured home living as an affordable alternative to apartment rentals.

## Key Project Variables

- **Community**: Watkins MHC (MNWAT)
- **Location**: 2nd St., Watkins, MN 55389
- **Domain**: watkinsmhc.com
- **Lot Rent**: $325.00/month
- **Community Type**: All-Ages
- **Sites**: ~20
- **Contact**: 1-800-209-1533 / TenantHelp@mhcpusa.com
- **Manager**: Tom Voigt
- **Portal**: https://mhcpusa.app.doorloop.com/

## Build Commands

```bash
# Development server (if using a simple HTTP server)
python3 -m http.server 8000 --directory public

# Or using Node's http-server (if installed)
npx http-server public -p 8000

# Run Lighthouse performance tests
npx lighthouse http://localhost:8000 --output json --output-path ./qa/lighthouse.json
```

## Project Structure

```
/public              # Production-ready static files
  index.html        # Single-page application with anchor navigation
  styles.css        # Main stylesheet importing design tokens
  main.js          # Minimal JavaScript for smooth scroll and form validation
  /assets          # Images, SVG icons, favicons
  robots.txt       # SEO robots file
  sitemap.xml      # XML sitemap
  llm.txt         # LLM manifest for AI agents
  
/design            # Design system files
  tokens.css      # CSS variables for colors, spacing, typography
  
/data             # Dynamic data
  comps.json      # Local 3BR/2BA apartment comparison data
  
/qa              # Quality assurance
  verification_log.md  # Factual accuracy tracking
  report.md           # QA findings and TODOs
```

## Critical Requirements

### Visual & Brand Standards
- **Color Palette**: Red/White/Blue with Gold accent
- **Icons**: SVG line icons only (1.5px stroke) - NO EMOJIS
- **Typography**: Modern sans-serif with ample white space

### Content Rules
- **Hero Hook**: Must include pain-based comparison using local 3BR/2BA apartment rent
- **Pet Policy**: Must state exactly: "We follow PetScreening.com's policies and approval process."
- **Contact**: Only display 1-800-209-1533 and TenantHelp@mhcpusa.com
- **Portal Links**: All resident login buttons must link to https://mhcpusa.app.doorloop.com/

### Verification Requirements
- Only use facts from the PRD variables or client-provided documents
- Do NOT pull community information from external sources
- Market comparison data (3BR/2BA apartments) must cite sources and collection dates
- Generate verification_log.md mapping every fact to its source

### SEO Implementation
- Focus on long-tail local keywords:
  - "mobile home park in Watkins MN"
  - "manufactured homes Watkins Minnesota"  
  - "lot rent Watkins MN"
  - "affordable housing near St. Cloud"
- Title format: "Watkins MHC — Manufactured Home Community in Watkins, MN 55389 | Lot Rent $325"
- Include JSON-LD structured data for LocalBusiness

### Performance Targets
- Lighthouse scores (mobile & desktop):
  - Performance ≥ 90
  - Accessibility ≥ 95
  - SEO ≥ 95
  - Best Practices ≥ 95

## Development Workflow

1. **Content First**: Start with copy.md and verify all facts against PRD variables
2. **Design Tokens**: Set up CSS variables in tokens.css before styling
3. **Semantic HTML**: Build accessible structure with proper landmarks
4. **Progressive Enhancement**: Add CSS styling, then minimal JavaScript
5. **QA Process**: 
   - Run verification against PRD
   - Test accessibility with screen readers
   - Run Lighthouse audits
   - Check all CTAs and links

## Key Implementation Notes

- This is a static HTML/CSS/JS project - no frameworks required
- Single-page design with smooth scroll anchors
- Comparison section must compute and display local 3BR/2BA apartment costs with transparent methodology
- All images should be lazy-loaded for performance
- Forms should submit to TenantHelp@mhcpusa.com or approved handler

## Testing Checklist

- [ ] All variables from PRD correctly implemented
- [ ] Hero contains pain-based hook with apartment comparison
- [ ] PetScreening.com policy language exact
- [ ] DoorLoop portal links working
- [ ] No emojis present (SVG icons only)
- [ ] Verification log complete
- [ ] Lighthouse scores meet targets
- [ ] WCAG 2.1 AA compliance verified
- [ ] llm.txt manifest present and accurate