# Cloudflare Pages Setup Guide (DocsShelf Legal Pages)

This guide hosts the legal pages in `web/` on Cloudflare Pages and connects them to your `docsshelf.com` domain.

## What you will get

- `https://legal.docsshelf.com/privacy-policy/`
- `https://legal.docsshelf.com/terms-of-service/`

(You can also use the root domain `docsshelf.com`, but a subdomain is usually better so you can use `docsshelf.com` later for a full marketing site.)

---

## Step 0: Confirm the files exist

These should be present in the repo:
- `web/index.html`
- `web/privacy-policy/index.html`
- `web/terms-of-service/index.html`

---

## Option A (recommended): Cloudflare Pages via GitHub (auto-deploy)

### Step 1: Add your domain to Cloudflare (DNS)

If your domain is not already on Cloudflare:
1. Create/Log in to Cloudflare
2. Add site: `docsshelf.com`
3. Cloudflare will provide 2 nameservers
4. Update nameservers at your registrar to the Cloudflare ones
5. Wait until Cloudflare shows the site as “Active”

### Step 2: Create a Pages project

1. Cloudflare Dashboard → **Workers & Pages** → **Pages**
2. **Create a project** → **Connect to Git**
3. Authorize GitHub (if prompted)
4. Select the repo: `jmjoshi/docsshelf-v7`

### Step 3: Configure build settings (static)

In the Pages setup:
- **Framework preset**: `None`
- **Build command**: (leave empty)
- **Build output directory**: `web`

Click **Save and Deploy**.

### Step 4: Add your custom domain

In the Pages project:
1. Go to **Custom domains**
2. Click **Set up a custom domain**
3. Use: `legal.docsshelf.com`

Cloudflare will create the required DNS records for you.

### Step 5: Verify URLs

- `https://legal.docsshelf.com/` (legal home)
- `https://legal.docsshelf.com/privacy-policy/`
- `https://legal.docsshelf.com/terms-of-service/`

Use these in Google Play Console.

---

## Option B: Use the root domain paths (docsshelf.com/privacy-policy)

If you want:
- `https://docsshelf.com/privacy-policy/`
- `https://docsshelf.com/terms-of-service/`

You have two common approaches:

### B1) Host the entire Pages project on the root domain

In Pages → Custom domains, add `docsshelf.com` (apex). Cloudflare will point the site root at the Pages project.

This is simplest if you do not have another site on `docsshelf.com` yet.

### B2) Keep `legal.docsshelf.com` as the site, and redirect

If you want to keep `docsshelf.com` free for a future site:
1. Keep Pages on `legal.docsshelf.com`
2. In Cloudflare → **Rules** → **Redirect Rules**, add redirects:
   - `/privacy-policy` and `/privacy-policy/*` → `https://legal.docsshelf.com/privacy-policy/$1`
   - `/terms-of-service` and `/terms-of-service/*` → `https://legal.docsshelf.com/terms-of-service/$1`

This way Play Console can use either domain.

---

## Notes

- Cloudflare Pages serves static sites. That’s perfect for legal pages.
- Changes deploy automatically on every push to the connected branch.
