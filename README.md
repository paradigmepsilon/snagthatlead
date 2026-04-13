# SnagThatLead Landing Page - Deployment Guide

## Files

- `index.html` - Main landing page (StoryBrand framework, 9 sections)
- `checkout.html` - Checkout/payment page (Stripe placeholder)

## Deploy to Cloudflare Pages

### Option A: Direct Upload (fastest)

1. Go to https://dash.cloudflare.com > Pages > Create a project > Direct Upload
2. Name the project `snagthatlead`
3. Upload both HTML files
4. Deploy

### Option B: GitHub + Auto-Deploy

1. Create a repo (e.g., `snag-that-lead-site`)
2. Push both files to `main`
3. In Cloudflare Pages, connect the GitHub repo
4. Build command: (leave empty, no build needed)
5. Build output directory: `/` (root)
6. Deploy

### Custom Domain (snagthatlead.com)

1. In Cloudflare Pages project settings, go to Custom domains
2. Add `snagthatlead.com` and `www.snagthatlead.com`
3. If the domain is already on Cloudflare DNS:
   - Cloudflare will auto-add the CNAME records
4. If the domain is on an external registrar:
   - Add a CNAME record: `snagthatlead.com` -> `snagthatlead.pages.dev`
   - Add a CNAME record: `www` -> `snagthatlead.pages.dev`
   - Or transfer the domain to Cloudflare for simplest management
5. SSL is automatic with Cloudflare Pages

## Deploy to GitHub Pages (alternative)

1. Create repo `snag-that-lead-site`
2. Push files to `main`
3. Settings > Pages > Source: Deploy from branch `main`, folder `/ (root)`
4. Custom domain: add `snagthatlead.com` in the Pages settings
5. At your DNS provider, add:
   - A records: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - CNAME for `www`: `<username>.github.io`
6. Check "Enforce HTTPS" in GitHub Pages settings

## Stripe Integration (checkout.html)

The checkout page has placeholder comments showing exactly where Stripe code goes. You need:

1. Stripe account with live API keys
2. Two Stripe products:
   - One-time: $497 setup fee
   - Recurring: $397/mo monthly service
3. A backend endpoint to create Checkout Sessions (or use Stripe Payment Links as a simpler option)

### Simplest path: Stripe Payment Links

Skip the custom checkout page entirely:
1. Create a Payment Link in Stripe Dashboard for $497 + $397/mo subscription
2. Change the CTA buttons on `index.html` to point directly to the Payment Link URL
3. No backend needed

### Custom checkout: Backend required

See the detailed comments inside `checkout.html` for Option A (Stripe Checkout redirect) and Option B (Stripe Elements embedded form). Both require a server endpoint.

## Tech Notes

- Single HTML files, no build tools, no dependencies
- Google Fonts (Inter, 400/600/700) - loads async
- Pure CSS responsive design, mobile-first
- FAQ accordion uses minimal vanilla JS
- No external CSS or JS libraries
- Estimated load time: under 1 second on broadband, under 3 seconds on 3G
