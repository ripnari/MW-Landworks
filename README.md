# MW Landworks — Site Files

Production-ready static site. Hand-built HTML + CSS + vanilla JS. No build step required.

## Files

```
site/
├── index.html              # Homepage
├── gallery.html            # Full project gallery page
├── netlify.toml            # Netlify config (caching, security headers)
├── vercel.json             # Vercel config (caching, security headers, clean URLs)
├── README.md               # This file
├── README-GALLERY.md       # How the owner adds new project photos via Cloudinary
└── images/                 # All photography + logo variants (≈13 MB)
```

## Deploy to Vercel

**Option 1 — Drag & drop (no Vercel CLI needed):**
1. Go to **https://vercel.com/new**
2. Drag the entire `site/` folder onto the page
3. Hit deploy. You'll get a `*.vercel.app` URL in 30 seconds.

**Option 2 — From a Git repo (recommended for ongoing updates):**
1. Push the contents of `site/` to a GitHub/GitLab/Bitbucket repo
2. In Vercel, click **Import Project** → connect to the repo
3. Framework preset: **Other** (it's a static site)
4. Build command: leave empty
5. Output directory: `.` (or empty)
6. Deploy

Either way, the included `vercel.json` configures clean URLs (`/gallery` instead of `/gallery.html`), security headers, and aggressive caching for the `/images/` directory.

**Custom domain:** Once deployed, Settings → Domains → Add `mwlandwork.com` (or whichever domain). Vercel handles SSL automatically.

## ✅ Already wired

- **Contact form** — posts to Formspree at `https://formspree.io/f/xrejzopk`. Submissions go straight to the inbox configured in Formspree.
- **Phone numbers / email / address** — all set throughout the site
- **Social links** — Instagram and Facebook in footer
- **SEO meta tags** — Open Graph + descriptions on both pages

## 🔧 To set up after deploy: Cloudinary auto-syncing gallery

The gallery section on the homepage and the dedicated gallery page **auto-update** whenever Rick uploads a new project photo to Cloudinary — no rebuild, no developer needed. This is configured separately in `README-GALLERY.md`. Until it's set up, the gallery shows the 9 hardcoded photos that ship with the site.

Quick version:
1. Sign up at https://cloudinary.com (free tier)
2. In Cloudinary → Settings → Security, uncheck "Resource list"
3. In **both** `index.html` and `gallery.html`, find `window.GALLERY_CONFIG` and set `CLOUD_NAME` to your Cloudinary cloud name
4. Tag photos in Cloudinary with `mwlandworks-gallery`. They appear on the site within a minute.

Hand `README-GALLERY.md` to Rick — it's written for the business owner, not developers.

## Other deployment options

- **Netlify**: drag the folder to https://app.netlify.com/drop (`netlify.toml` is included)
- **Cloudflare Pages**: similar drag-and-drop at https://pages.cloudflare.com
- **GitHub Pages**: push contents to a repo, enable Pages in settings
- **Any static host**: it's just HTML + images. FTP/SFTP works fine.

## Local preview

```bash
cd site
python3 -m http.server 8000
# Open http://localhost:8000
```

## What's included

- **Hero** with branded excavator photo, animated zoom, dual CTAs
- **Trust strip** — Licensed/Insured · Free Estimates · Northern NJ · 24hr Response
- **Brand pillars** — Reliable / Trustworthy / Responsive / Adaptable
- **Services** — Excavation & Site Work (incl. septic/drainage), Hardscaping & Masonry, Snow Removal
- **Featured action shot** with editorial pull-quote and stats
- **Gallery section** on homepage (9 most recent) with "See More Projects" CTA
- **Dedicated gallery page** showing the full archive
- **About** — tiered boulder wall photo + capability checks
- **Contact** — split layout: direct contact info + Formspree-wired form
- **Footer** with Instagram + Facebook
- **Sticky mobile bottom bar** — Call + Get Quote always visible
- **Lightbox** — keyboard navigation, click-outside-to-close

## Browser support

Tested on the latest Chrome, Safari, Firefox, and mobile browsers. Uses modern CSS (variables, grid, backdrop-filter) — works on anything from the last 4 years. Gracefully degrades for `prefers-reduced-motion`.

## Editing content

- **Phone number**: search for `(201) 874-0254` (in both `index.html` and `gallery.html`)
- **Email**: search for `info@mwlandwork.com`
- **Address**: search for `Franklin Lakes`
- **Service list bullets**: each `<ul class="service-list">` block in the services-grid section
- **Gallery photos**: see `README-GALLERY.md` — Rick manages these via Cloudinary

## Performance

- Total weight: ~13 MB initial (mostly photography), much less after gzip
- Lazy-loaded gallery images, inlined CSS, no build step
- Once Cloudinary is configured, gallery thumbnails are auto-optimized to AVIF/WebP from a CDN
- Vercel adds its own edge caching on top

## Suggested next steps after launch

1. **Google Business Profile** — claim, add photos, list service categories. Map Pack drives more leads than the website in this category.
2. **GA4 / GTM** — drop the script in `<head>` to track form conversions
3. **LocalBusiness schema** — JSON-LD block for richer search results
4. **Testimonials section** — once 3–5 reviews are collected
5. **Service-specific landing pages** — when running Google Ads, each service deserves its own page

---

Built with care. Deploy clean.
