# Atoms & Watts website: deployment brief

A finished, static, one-page website. **No build step, no framework, no backend, no third-party requests.** Upload this folder as the site root.

Target domain: **atomsandwatts.com** (also redirect `www.atomsandwatts.com` → `atomsandwatts.com`).

## Contents

```
site/
├── index.html              The landing page (all CSS and JS inline)
├── 404.html                Branded "page not found" page
├── favicon.ico             16/32/48 px favicon
├── site.webmanifest        Icons for Android / "add to home screen"
├── robots.txt              Allows indexing, points to the sitemap
├── sitemap.xml             Single URL: https://atomsandwatts.com/
├── _headers                Security + cache headers (Netlify / Cloudflare Pages only)
└── assets/
    ├── fonts/              Self-hosted web fonts (woff2) + fonts.css
    └── img/                favicon.svg, app icons, og-image.png (social share), logo SVGs
```

All asset paths are **root-relative** (`/assets/...`), so the site must be served from the domain root, not a subfolder. If it ever has to live in a subfolder, change `/assets/` to `assets/` and `/favicon.ico` to `favicon.ico` in `index.html` and `404.html`.

## Deploy (any static host works)

Recommended: **Cloudflare Pages** or **Netlify** (free tier is enough, and both read `_headers`).

1. Create a new project and upload this `site` folder as-is (drag-and-drop or connect the Git repo with the root set to `atoms-and-watts/site`). Build command: none. Output directory: `/` (the folder itself).
2. Add the custom domain `atomsandwatts.com` and `www.atomsandwatts.com`, and set `www` to redirect to the apex domain.
3. At the domain registrar, point DNS to the host as it instructs (usually a CNAME or A/ALIAS record). Enable HTTPS (automatic on both hosts) and "Always use HTTPS".
4. Make sure the host serves `404.html` for missing pages (automatic on Netlify and Cloudflare Pages).

Other hosts (Vercel, GitHub Pages, S3 + CloudFront, a plain Nginx/Apache server) work too; `_headers` is then ignored and the same headers can be set in that host's config if wanted.

## Email (the site depends on it)

The page shows `partners@atomsandwatts.com` as the contact address, and the business cards use `mu@atomsandwatts.com` and `mn@atomsandwatts.com`. Set up mailboxes or forwarding for all three on the domain (e.g. Google Workspace, Microsoft 365, Zoho, or Cloudflare Email Routing for forwarding), with SPF, DKIM and DMARC records so mail is delivered reliably.

## Checks after going live

- `https://atomsandwatts.com/` loads with the serif headings (fonts load from `/assets/fonts/`).
- `https://www.atomsandwatts.com/` redirects to the apex.
- `https://atomsandwatts.com/anything` shows the branded 404 page.
- Paste the URL into a LinkedIn or WhatsApp message: the preview shows `og-image.png` with the title "Atoms & Watts".
- Page works on a phone and in dark mode (it follows the device's light/dark setting).
- Optional: add the domain to Google Search Console and submit `sitemap.xml`.

## Things the owners may still change in the text

Edit directly in `index.html` (plain HTML, search for the text):
- Contact email: `partners@atomsandwatts.com` (appears once in the page).
- Partner name styling "Module Edge" and the MDC2000 figures in the Partners section.
- Footer line `© 2026 Atoms & Watts ...` and the disclaimer wording.

## Notes

- The only script on the page is a small inline "Copy address" button handler. There is no form, analytics or cookies, so no cookie banner is needed. If analytics is added later, use a privacy-friendly option (e.g. Plausible or Cloudflare Web Analytics) to avoid needing a consent banner in the EU.
- Fonts are Cormorant Garamond and Public Sans, self-hosted under the SIL Open Font License (free for commercial use). No requests go to Google.
