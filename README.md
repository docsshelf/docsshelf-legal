# DocsShelf Legal Pages

Professional hosting for DocsShelf Privacy Policy and Terms of Service.

## 📁 Files

- `index.html` - Landing page with links to legal documents
- `privacy-policy.html` - Complete privacy policy (matches in-app version)
- `terms-of-service.html` - Complete terms of service (matches in-app version)

## 🌐 Hosting Options

### Option 0: Quick decision guide

See `web/HOSTING_GUIDE.md` for GitHub Pages vs Cloudflare Pages.

### Option 1: GitHub Pages (Recommended) ⭐

**Pros:**
- Free forever
- Easy to update via Git
- Reliable (99.9% uptime)
- Custom domain support
- HTTPS included

**Setup Steps:**

1. **Create GitHub Repository**
   ```bash
   # If not already in a git repository
   cd C:\Projects\docsshelf-v7
   git add web/
   git commit -m "Add legal pages for web hosting"
   git push origin main
   ```

2. **Enable GitHub Pages**
   - Go to your repository on GitHub
   - Click **Settings** → **Pages**
   - Under "Source", select branch: `main`
   - Under "Folder", select: `/web`
   - Click **Save**

3. **Wait 2-3 minutes**, then access at:
   - `https://yourusername.github.io/docsshelf-v7/`
   - Privacy Policy: `https://yourusername.github.io/docsshelf-v7/privacy-policy.html`
   - Terms: `https://yourusername.github.io/docsshelf-v7/terms-of-service.html`

### Option 2: Custom Domain (docsshelf.com) 🎯

**Using Your DocsShelf Domain - YES, it's FREE to use!**

#### Cost Breakdown:
- **Domain registration**: You already purchased (typically $10-15/year)
- **GitHub Pages hosting**: **FREE** ✅
- **SSL Certificate**: **FREE** (included with GitHub Pages) ✅
- **Total additional cost**: **$0** 🎉

#### Setup Steps:

1. **Configure DNS (at your domain registrar)**

   Add these DNS records for your domain:

   **Option A: Subdomain (Recommended)**
   ```
   Type: CNAME
   Name: legal (or docs, or www)
   Value: yourusername.github.io
   TTL: 3600
   ```
   
   This creates: `legal.docsshelf.com`

   **Option B: Root Domain**
   ```
   Type: A
   Name: @ (or leave blank)
   Value: 185.199.108.153
   
   Type: A
   Name: @
   Value: 185.199.109.153
   
   Type: A
   Name: @
   Value: 185.199.110.153
   
   Type: A
   Name: @
   Value: 185.199.111.153
   ```
   
   This uses: `docsshelf.com`

2. **Configure GitHub Pages**
   - Go to GitHub repo → Settings → Pages
   - Under "Custom domain", enter: `legal.docsshelf.com` (or your choice)
   - Check "Enforce HTTPS" (wait 10-15 minutes for certificate)
   - Click **Save**

3. **Create CNAME file** (in web directory)
   ```bash
   echo "legal.docsshelf.com" > web/CNAME
   git add web/CNAME
   git commit -m "Add custom domain"
   git push
   ```

4. **Wait for DNS propagation** (15 minutes - 24 hours)
   - Test at: `https://legal.docsshelf.com`

#### Recommended Subdomain Options:
- `legal.docsshelf.com` ⭐ (most professional)
- `docs.docsshelf.com`
- `policy.docsshelf.com`
- `www.docsshelf.com`

### Option 3: Netlify (Alternative)

**Setup:**
1. Create account at netlify.com
2. Drag & drop the `web` folder
3. Custom domain setup included
4. Free SSL certificate

### Option 4: Cloudflare Pages (Recommended if you use Cloudflare DNS) ⭐

See `web/CLOUDFLARE_PAGES_SETUP.md`.

## 🔗 URLs for Google Play Console

Once hosted, use these URLs in Play Console:

**With GitHub Pages (default):**
- Privacy Policy: `https://yourusername.github.io/docsshelf-v7/privacy-policy.html`

**With Custom Domain:**
- Privacy Policy: `https://legal.docsshelf.com/privacy-policy.html`
- Terms of Service: `https://legal.docsshelf.com/terms-of-service.html`

## 📝 Updating Content

### Method 1: Edit Files Directly
1. Edit HTML files in `web/` directory
2. Commit and push changes:
   ```bash
   git add web/
   git commit -m "Update privacy policy"
   git push
   ```
3. Changes appear within 1-2 minutes

### Method 2: GitHub Web Editor
1. Go to GitHub repo
2. Navigate to file (e.g., `web/privacy-policy.html`)
3. Click pencil icon (Edit)
4. Make changes
5. Commit directly to main branch
6. Changes go live automatically

## ✅ Verification Checklist

Before submitting to Play Console:

- [ ] All files uploaded to GitHub
- [ ] GitHub Pages enabled
- [ ] Custom domain configured (optional)
- [ ] HTTPS working (check padlock in browser)
- [ ] Privacy policy loads without errors
- [ ] Terms of service loads without errors
- [ ] Links work between pages
- [ ] Mobile-responsive (test on phone)
- [ ] Content matches in-app versions exactly

## 🎨 Customization

The HTML files use inline CSS for easy customization:

- **Colors**: Change `#667eea` and `#764ba2` to your brand colors
- **Fonts**: Modify the `font-family` property
- **Logo**: Replace emoji in `index.html` with an actual logo image
- **Contact Email**: Update `feedback@docsshelf.com` to your email

## 📱 Mobile Responsive

All pages are fully responsive and optimized for:
- Desktop browsers
- Mobile phones
- Tablets
- Google Play Store web preview

## 🔒 Security

- All pages use semantic HTML5
- No external dependencies or tracking
- HTTPS enforced (on GitHub Pages)
- No JavaScript (faster load times)
- Clean, minimal code

## 📄 License

These legal documents are specific to DocsShelf. The HTML structure can be reused, but update the content for your app.

---

## Quick Start Summary

**Fastest route to get your URLs:**

1. **Push to GitHub** (if not already there):
   ```bash
   git add web/
   git commit -m "Add legal pages"
   git push origin main
   ```

2. **Enable GitHub Pages**:
   - Settings → Pages → Source: main → Folder: /web → Save

3. **Get your URLs** (available in 2-3 minutes):
   - Privacy: `https://yourusername.github.io/docsshelf-v7/privacy-policy.html`
   - Terms: `https://yourusername.github.io/docsshelf-v7/terms-of-service.html`

4. **Add to Play Console**:
   - Go to Store listing
   - Paste Privacy Policy URL
   - Save

**Total time: 5-10 minutes** ⚡

---

Need help? Contact: feedback@docsshelf.com
