# Gallery Setup — How to Update Project Photos

Your website's gallery section auto-syncs with a Cloudinary folder. Once it's set up, **adding a new project photo takes about 30 seconds** and the website updates within a minute. No coding, no rebuilding, no waiting.

---

## One-time setup (≈10 minutes)

### Step 1 — Create a free Cloudinary account

1. Go to **https://cloudinary.com** and click **Sign Up Free**
2. Use your business email
3. When asked for a "Cloud Name", pick something memorable like `mwlandworks` (this becomes part of your image URLs — you can't easily change it later)
4. Skip the "developer" questions if asked — pick "I'm just exploring" or similar

### Step 2 — Enable the resource list (one toggle)

Cloudinary has this disabled by default for security; we need it on so the website can read which photos are in your gallery.

1. In the Cloudinary dashboard, click **Settings** (gear icon, top-right)
2. Click the **Security** tab
3. Find the section called **Restricted media types**
4. **Uncheck** the box next to **Resource list**
5. Click **Save** at the bottom

That's it for security. The website still can't modify your account — only read photos that are tagged for the gallery.

### Step 3 — Tell the website your cloud name

Open your `index.html` file (or ask your developer/Netlify to do this once). Find this block, near the bottom of the file:

```javascript
window.GALLERY_CONFIG = {
  CLOUD_NAME: '',                    // e.g. 'mwlandworks'
  TAG: 'mwlandworks-gallery',
  ...
};
```

Change `CLOUD_NAME: ''` to your cloud name from Step 1, like:

```javascript
CLOUD_NAME: 'mwlandworks',
```

**Then do the same in `gallery.html`** — it has an identical config block (the gallery page uses it too).

Save both files and re-deploy (drag the folder back to Netlify Drop, or push to your repo).

**You're done with setup.** From here on, you only touch Cloudinary.

---

## Daily use — adding new project photos

Every time you finish a project and want it on the site:

### 1. Upload the photo to Cloudinary

- Open https://console.cloudinary.com
- Click the big **Upload** button in the Media Library
- Drag your photo (or photos) in
- They'll appear in the library

### 2. Tag the photo

This is the only step that matters — tagging is what tells the website "show this on the gallery."

- Click the photo you just uploaded
- In the side panel, find the **Tags** field
- Type `mwlandworks-gallery` and press Enter
- (Or select multiple photos at once and use the bulk **Add tags** action)

That's it. Within ~60 seconds, the photo appears on your website's gallery, **at the top** (newest photos always appear first).

### 3. (Optional) Add a caption

If you want a custom caption like "Boulder retaining wall — Wyckoff, NJ" instead of the auto-generated one:

- With the photo selected, click the **Add metadata** button (or **Context** field, depending on UI version)
- Add a key called `caption` with your desired caption text
- Save

The website reads this and displays it.

---

## Removing a photo from the gallery

Two options:
- **Hide it but keep it in Cloudinary**: remove the `mwlandworks-gallery` tag
- **Delete it permanently**: select the photo and click Delete

Either way, the website updates within a minute.

---

## Reordering

Newest uploads appear first by default. If you want a specific photo to lead the gallery, the simplest approach: re-upload it (it gets a new upload date and floats to the top).

---

## How many photos can I add?

The free Cloudinary plan gives you **25 GB of storage and 25 GB of monthly delivery bandwidth** — that's enough for thousands of project photos and tens of thousands of monthly visitors before you'd ever see a charge.

The website has **two gallery views**:
- **Homepage** — shows the **9 most recent photos** in an editorial magazine-style grid. There's a "See More Projects" button that links to the full gallery.
- **Gallery page** (`/gallery.html`) — shows **all** of your photos in a clean uniform grid. No cap.

This way the homepage stays fast and curated, and visitors who want to see your full portfolio can click through.

---

## What happens if Cloudinary is down or I haven't set it up yet?

The website automatically falls back to showing the original 9 hardcoded gallery photos that came with the build. So nothing ever breaks visually — it just won't auto-update until Cloudinary is configured.

---

## Common questions

**"Will my photos load slowly?"**
Cloudinary auto-optimizes images for whoever's looking — phone visitors get smaller versions, desktop visitors get larger ones, modern browsers get next-gen formats (AVIF/WebP). Loads are typically faster than self-hosted images.

**"Can I see how the gallery looks before publishing?"**
Yes — anything tagged `mwlandworks-gallery` shows up live, period. To stage photos before they go live, use a different tag (e.g. `mwlandworks-staging`) for not-yet-ready photos and only switch to the gallery tag when you're ready.

**"Do my photos get watermarked or have a Cloudinary logo?"**
No. Free tier delivers your photos cleanly with no overlays.

**"Can I have multiple galleries (e.g. 'Excavation', 'Hardscape', 'Snow Removal')?"**
Yes — use different tags. Future site update: we'd add filter buttons that switch which tag is being fetched. Talk to your developer when you're ready for this.

---

## Getting help

If something stops working: the most common cause is the **Resource list** security setting being re-enabled by Cloudinary (they sometimes reset this on plan changes). Re-check Step 2 of the setup above.

If photos aren't appearing within 2 minutes:
1. Confirm the photo has the exact tag `mwlandworks-gallery` (case-sensitive, no spaces)
2. Confirm `CLOUD_NAME` in the website code matches your Cloudinary cloud name exactly
3. Try a hard browser refresh (Ctrl+Shift+R or Cmd+Shift+R) — Cloudinary caches the JSON for 60 seconds
