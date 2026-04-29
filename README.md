# MW Landworks — Site Files

A modern, single-page static site for MW Landworks. Hand-built HTML + CSS + vanilla JS. No build step required.

## Files

```
site/
├── index.html        # The whole site (HTML + CSS + JS in one file)
├── netlify.toml      # Netlify config (caching, security headers)
└── images/           # All photography + logo variants (≈15 MB)
```

## Deploy in 60 seconds — Netlify Drop

The fastest path:

1. Go to **https://app.netlify.com/drop**
2. Drag the entire `site/` folder onto the page
3. Done. You'll get a `*.netlify.app` URL immediately.
4. To connect a real domain (e.g. `mwlandwork.com`): click the site → **Domain settings** → **Add custom domain**.

## ⚠️ Before going live: wire the contact form

The form currently points to a placeholder. Pick one of these two options:

### Option A — Netlify Forms (recommended; zero setup)

In `index.html`, find this line (near the bottom of the contact section):

```html
<form class="contact-form reveal" id="quote-form" action="https://formspree.io/f/YOUR_ID_HERE" method="POST">
```

Change to:

```html
<form class="contact-form reveal" id="quote-form" name="quote" method="POST" data-netlify="true" netlify-honeypot="bot-field">
  <input type="hidden" name="form-name" value="quote">
  <p style="display:none"><label>Don't fill this out: <input name="bot-field"></label></p>
```

Submissions will appear in your Netlify dashboard under **Forms**, and you can configure email notifications from there.

### Option B — Formspree

1. Go to https://formspree.io and create a free account
2. Create a new form, copy your endpoint (looks like `https://formspree.io/f/abcd1234`)
3. In `index.html`, replace `YOUR_ID_HERE` with your Formspree ID

Also delete or update the alert in the `<script>` at the bottom that says "Form is ready to deploy..."

## Other deployment options

- **Vercel**: drag the folder at https://vercel.com/new (works the same as Netlify)
- **GitHub Pages**: push the `site/` contents to a repo, enable Pages in settings
- **Cloudflare Pages**: similar drag-and-drop flow at https://pages.cloudflare.com
- **Any static host**: it's just HTML + images. Upload via FTP/SFTP and you're done.

## Local preview

```bash
cd site
python3 -m http.server 8000
# Open http://localhost:8000 in your browser
```

## What's included

- **Hero** with branded excavator photo, animated zoom, dual CTAs (call + estimate)
- **Trust strip** — Licensed/Insured · Free Estimates · Northern NJ · 24hr Response
- **Brand pillars** — the four words (Reliable / Trustworthy / Responsive / Adaptable) wired into copy
- **Services** — three cards: Excavation, Hardscaping, Septic/Drainage/Snow
- **Featured action shot** with editorial pull-quote and stats
- **Gallery** — 9-tile asymmetric magazine-style grid with click-to-lightbox (keyboard nav)
- **About** — tiered boulder wall photo + capability checks
- **Contact** — split layout with direct contact info + structured form
- **Footer** with Instagram and Facebook social links
- **Sticky mobile bottom bar** — Call + Get Quote always visible

## Browser support

Tested on the latest Chrome, Safari, Firefox, and mobile Safari/Chrome. Uses modern CSS (variables, grid, backdrop-filter) — works on anything from the last 4 years. Gracefully degrades for `prefers-reduced-motion`.

## Editing content

- **Phone number**: search for `(201) 874-0254` in `index.html` — appears in header, hero CTA, contact section, footer, sticky mobile bar
- **Email**: search for `info@mwlandwork.com`
- **Address**: search for `Franklin Lakes`
- **Service list bullets**: in the "services-grid" section, each `<ul class="service-list">` block
- **Gallery captions**: each `<figure class="gallery-item">` has `data-title` and a `<figcaption>` block
- **Adding more gallery photos**: drop image in `images/`, add a new `<figure>` block following the pattern. Adjust the `g1-g9` grid placement classes (defined in CSS).

## Performance notes

- Images are pre-optimized (~85% JPEG quality, progressive)
- Total page weight: ~15 MB (mostly photography)
- Loading: inline CSS, lazy-loaded gallery images, system + Google fonts
- Lighthouse score expectation: 90+ on Performance, 100 on SEO and Best Practices

## Suggested next steps after launch

1. **Google Business Profile** — claim it, add the same photos, list service categories. The Map Pack drives more leads than the website itself in this category.
2. **Google Tag Manager / GA4** — drop the script into `<head>` to track conversions
3. **Schema.org markup** — add a `LocalBusiness` JSON-LD block for better SEO
4. **Real testimonials** — add a testimonials section once 3–5 reviews are collected
5. **Service-specific landing pages** — when running Google Ads, each service should have its own deep page

---

Built with care. Deploy clean.
