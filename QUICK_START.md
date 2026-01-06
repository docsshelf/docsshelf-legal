# 🚀 Quick Setup - DocsShelf Legal Pages

## For the Impatient Developer (5 minutes)

### What You Just Got
✅ Professional privacy policy (HTML)
✅ Professional terms of service (HTML)  
✅ Beautiful landing page
✅ Mobile-responsive design
✅ Ready for Google Play Store

---

## Fastest Path to Live URLs

### Step 1: Push to GitHub (2 min)
```powershell
cd C:\Projects\docsshelf-v7
git add web/
git commit -m "Add legal pages for web hosting"
git push origin main
```

### Step 2: Enable GitHub Pages (1 min)
1. Go to GitHub.com → Your repo → **Settings** → **Pages**
2. Source: `main` → Folder: `/web` → **Save**
3. Done!

### Step 3: Get Your URL (2 min)
Wait 2-3 minutes, then use:
```
https://YOUR_USERNAME.github.io/YOUR_REPO/privacy-policy.html
```

### Step 4: Add to Play Console (30 sec)
Paste URL into Play Console → Store listing → Privacy Policy

---

## Want Custom Domain? (Additional 10 minutes)

### Setup
```powershell
# Create CNAME file
"legal.docsshelf.com" | Out-File -FilePath web/CNAME -Encoding ASCII -NoNewline
git add web/CNAME
git commit -m "Add custom domain"
git push
```

### Configure DNS (at your domain registrar)
```
Type: CNAME
Name: legal
Value: yourusername.github.io
TTL: 3600
```

### Enable in GitHub
Settings → Pages → Custom domain: `legal.docsshelf.com` → Save → ✅ Enforce HTTPS

### Your New URL (after DNS propagates)
```
https://legal.docsshelf.com/privacy-policy.html
```

---

## Cost Breakdown

| Item | Cost | Notes |
|------|------|-------|
| Domain (you own) | $10-15/year | Already paid ✅ |
| Hosting | **FREE** | GitHub Pages |
| SSL | **FREE** | Auto-generated |
| Bandwidth | **FREE** | Unlimited |
| **TOTAL** | **$0** | 🎉 |

---

## URLs You Need

**For Play Console:**
- Privacy Policy: `https://[YOUR-DOMAIN]/privacy-policy.html`

**Optional (also available):**
- Terms of Service: `https://[YOUR-DOMAIN]/terms-of-service.html`
- Home: `https://[YOUR-DOMAIN]/`

---

## Troubleshooting One-Liners

**GitHub Pages not working?**
```powershell
# Check if web folder exists
ls web/
# Should show: index.html, privacy-policy.html, terms-of-service.html
```

**Custom domain not working?**
```powershell
# Check DNS
nslookup legal.docsshelf.com
# Wait 15min-24hrs for DNS propagation
```

**Need to update content?**
```powershell
# Edit, commit, push - changes live in 1-2 minutes
git add web/
git commit -m "Update privacy policy"
git push
```

---

## Content Policy ⚠️

✅ **DO**: Keep web version identical to in-app version  
❌ **DON'T**: Have different versions (Google Play violation)

---

## Full Documentation

- [README.md](README.md) - Complete guide with all options
- [GITHUB_PAGES_SETUP.md](GITHUB_PAGES_SETUP.md) - Detailed step-by-step
- [Android Publishing Guide](../documents/ANDROID_PLAY_STORE_PUBLISHING_GUIDE.md) - Full Play Store guide

---

## Questions?

1. Check [GITHUB_PAGES_SETUP.md](GITHUB_PAGES_SETUP.md) troubleshooting section
2. GitHub Pages docs: https://docs.github.com/pages
3. Email: feedback@docsshelf.com

---

**You're ready to publish! 🚀**
