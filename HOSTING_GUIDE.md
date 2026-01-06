# Hosting DocsShelf Legal Pages (GitHub Pages + Cloudflare)

You can absolutely host a website on GitHub — GitHub Pages is a static-site host. It’s ideal for legal pages like Privacy Policy and Terms.

This repo already includes the legal site in `web/`.

## Recommended URL strategy

- Host the legal site at: `https://legal.docsshelf.com/`
- Use these in Play Console:
  - `https://legal.docsshelf.com/privacy-policy/`
  - `https://legal.docsshelf.com/terms-of-service/`

Reason: it keeps `docsshelf.com` available for a future full website.

---

## Files and routes

The legal site is static HTML:
- `web/index.html`
- `web/privacy-policy/index.html`
- `web/terms-of-service/index.html`

So these routes work on most hosts:
- `/privacy-policy/`
- `/terms-of-service/`

(Old `.html` URLs still exist too, if you need them.)

---

## Option 1: Host on GitHub Pages (static hosting)

### What GitHub Pages can/can’t do

- ✅ Static files (HTML/CSS/JS/images)
- ✅ Custom domains + free HTTPS
- ❌ Server code (no Node/Express backend)

### Approach A (recommended): GitHub Pages via GitHub Actions (deploy `web/`)

This avoids the “Pages can only publish from root or /docs” limitation and lets you publish exactly `web/`.

1. In GitHub repo: **Settings → Pages**
2. Under **Build and deployment**, set **Source** to **GitHub Actions**
3. Add a workflow that uploads the `web/` folder and deploys it (see `.github/workflows/pages-legal.yml` if you add one).
4. After it runs, your site will be available at:
   - `https://YOUR_USERNAME.github.io/YOUR_REPO/`

Custom domain (recommended subdomain):
1. Create `web/CNAME` containing `legal.docsshelf.com` (one line)
2. GitHub repo: **Settings → Pages → Custom domain** = `legal.docsshelf.com`
3. In DNS (Cloudflare or your registrar):
   - `CNAME` record: `legal` → `YOUR_USERNAME.github.io` (DNS-only)
4. Enable **Enforce HTTPS** in GitHub Pages

### Approach B: GitHub Pages “Deploy from a branch” (if you publish from /docs)

If you prefer no Actions, GitHub Pages typically supports publishing from:
- `/ (root)` or `/docs`

That means you’d need your site to live in `/docs` (or repo root) instead of `web/`.

---

## Option 2: Host on Cloudflare Pages (recommended)

Cloudflare Pages is also static hosting and works great with GitHub.

Follow: `web/CLOUDFLARE_PAGES_SETUP.md`

---

## Which should you choose?

- Choose **Cloudflare Pages** if you want:
  - easiest custom domain setup (especially since you already own `docsshelf.com`)
  - fast global CDN by default

- Choose **GitHub Pages** if you want:
  - everything hosted directly by GitHub
  - you’re already using GitHub heavily and want fewer vendors
