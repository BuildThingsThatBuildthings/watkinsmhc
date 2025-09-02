# Watkins MHC Website

Static website for Watkins Manufactured Home Community in Watkins, MN.

## Quick Start

### Development Server
```bash
# Using Python (built-in)
python3 -m http.server 8000 --directory public

# Or using Node's http-server
npx http-server public -p 8000
```

Then visit: http://localhost:8000

## Project Structure

```
watkins_mhc/
├── public/           # Production website files
│   ├── index.html   # Main website
│   ├── styles.css   # Compiled styles
│   ├── main.js      # JavaScript functionality
│   └── *.txt/xml    # SEO files
├── design/          # Design system
│   └── tokens.css   # CSS variables
├── data/            # Dynamic data
│   └── comps.json   # Market comparison data
├── qa/              # Quality assurance
│   ├── verification_log.md
│   └── report.md
└── CLAUDE.md        # AI assistant guide
```

## Key Features

- **Pain-Based Marketing**: Compares $1,307/mo apartment rent vs ~$750/mo ownership
- **Single Page Design**: Smooth scroll navigation with anchored sections
- **Mobile Responsive**: Optimized for all devices
- **SEO Optimized**: Long-tail keywords, structured data, sitemap
- **Accessibility**: WCAG 2.1 AA compliant
- **No Dependencies**: Pure HTML/CSS/JS - no frameworks

## Before Launch Checklist

### Required Assets
- [ ] Hero background image (`/assets/hero-bg.jpg`)
- [ ] 6 gallery images
- [ ] Open Graph image (`/assets/og.png`)
- [ ] Favicon files

### Configuration
- [ ] Update Google Maps embed with API key
- [ ] Verify exact location coordinates
- [ ] Set up domain hosting
- [ ] Configure SSL certificate

### Testing
- [ ] Run Lighthouse audit (targets: Performance ≥90, Others ≥95)
- [ ] Cross-browser testing
- [ ] Mobile device testing
- [ ] Form submission testing
- [ ] All CTAs functional

## Maintenance

### Quarterly Updates
- Update 3BR/2BA comparison data in `/data/comps.json`
- Refresh market sources and collection dates

### As Needed
- Update lot rent if it changes (currently $325/mo)
- Refresh gallery images
- Update manager information

## Performance Targets

- Performance: ≥ 90
- Accessibility: ≥ 95
- SEO: ≥ 95
- Best Practices: ≥ 95

## Contact

**Community Contact:**
- Phone: 1-800-209-1533
- Email: TenantHelp@mhcpusa.com

**Manager:** Tom Voigt

## License

© 2024 Watkins MHC. All rights reserved.