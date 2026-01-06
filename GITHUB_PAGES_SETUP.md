# GitHub Pages Setup Guide for DocsShelf

Complete step-by-step guide to host your legal pages on GitHub Pages with custom domain.

## Table of Contents
1. [Common Steps (A and B)](#common-steps-a-and-b)
2. [Option A: GitHub Pages with Default URL](#option-a-github-pages-default)
3. [Option B: Custom Domain Setup](#option-b-custom-domain)
4. [Host Only web/ From a Different GitHub Account](#host-only-web-from-a-different-github-account)
5. [DNS Configuration Examples](#dns-configuration)
6. [Troubleshooting](#troubleshooting)

---

## Common Steps (A and B)

Option B (custom domain) builds on Option A.

Steps that are common to BOTH:
1. Make sure the legal site files exist (in this repo, they live in `web/`)
2. Push those files to a GitHub repository
3. Enable GitHub Pages (or GitHub Actions → Pages deployment)
4. Verify the site works on the GitHub Pages URL

Then Option B adds:
- DNS records for your custom domain
- GitHub Pages “Custom domain” configuration
- HTTPS enforcement

---

## Option A: GitHub Pages (Default URL)

### Prerequisites
- GitHub account
- DocsShelf repository on GitHub

### Step-by-Step Instructions

#### 1. Check Your Repository
Your code is at: `C:\Projects\docsshelf-v7`

Open PowerShell and verify:
```powershell
cd C:\Projects\docsshelf-v7
git status
```

#### 2. Commit Web Files
```powershell
git add web/
git commit -m "Add legal pages for web hosting"
git push origin main
```

If you get an error about no remote:
```powershell
# Check if remote exists
git remote -v

# If no remote, add it (replace YOUR_USERNAME and YOUR_REPO)
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main
```

#### 3. Enable GitHub Pages

**In your web browser:**

1. Go to `https://github.com/YOUR_USERNAME/YOUR_REPO`
2. Click **Settings** (gear icon at top)
3. In the left sidebar, click **Pages**
4. Under "Build and deployment":
   - **Source**: Select **GitHub Actions** (recommended)
   - This repo can deploy the `web/` folder directly via an Actions workflow.

**Note:** GitHub’s "Deploy from a branch" mode typically publishes from `/ (root)` or `/docs` only. If you don’t see `/web` as an option, use the GitHub Actions method.

#### 4. Wait for Deployment

GitHub will show:
```
Your site is ready to be published at https://YOUR_USERNAME.github.io/YOUR_REPO/
```

Wait 2-3 minutes for initial deployment.

#### 5. Test Your URLs

Open these in your browser:
- Home: `https://YOUR_USERNAME.github.io/YOUR_REPO/`
- Privacy: `https://YOUR_USERNAME.github.io/YOUR_REPO/privacy-policy/`
- Terms: `https://YOUR_USERNAME.github.io/YOUR_REPO/terms-of-service/`

#### 6. Add to Google Play Console

Copy this URL:
```
https://YOUR_USERNAME.github.io/YOUR_REPO/privacy-policy/
```

In Play Console:
1. Go to **Store presence** → **Main store listing**
2. Scroll to **Privacy Policy**
3. Paste the URL
4. Click **Save**

✅ **Done!** You're ready to publish.

---

## Option B: Custom Domain Setup

### Using Your DocsShelf Domain

#### Cost Analysis
| Item | Cost | Notes |
|------|------|-------|
| Domain (docsshelf.com) | $10-15/year | You already own this ✅ |
| GitHub Pages hosting | FREE | Forever |
| SSL Certificate | FREE | Auto-generated |
| Bandwidth | FREE | Unlimited |
| **Total Additional Cost** | **$0/year** | 🎉 |

#### Benefits of Custom Domain
- Professional appearance: `legal.docsshelf.com`
- Better branding
- Easier to remember
- Looks more trustworthy to users
- No GitHub in the URL

### Setup Instructions

#### Step 1: Choose Your Subdomain

Pick one of these (recommended):
- `legal.docsshelf.com` ⭐ (Most professional)
- `docs.docsshelf.com`
- `policy.docsshelf.com`
- `www.docsshelf.com`

Or use root domain:
- `docsshelf.com`

**Recommendation**: Use a subdomain (`legal.docsshelf.com`) to keep the root domain available for a future website.

#### Step 2: Configure DNS

**Where**: Log in to your domain registrar (where you bought docsshelf.com)

Common registrars: GoDaddy, Namecheap, Google Domains, Cloudflare, Hover

**What to add**:

##### For Subdomain (e.g., legal.docsshelf.com):

```
Record Type: CNAME
Name: legal
Value: YOUR_USERNAME.github.io
TTL: 3600 (or Auto)
```

**Example screenshots of DNS settings:**

**GoDaddy:**
```
Type: CNAME
Name: legal
Value: yourusername.github.io
TTL: 1 Hour
```

**Namecheap:**
```
Type: CNAME Record
Host: legal
Value: yourusername.github.io
TTL: Automatic
```

**Cloudflare:**
```
Type: CNAME
Name: legal
Target: yourusername.github.io
Proxy status: DNS only (gray cloud)
TTL: Auto
```

##### For Root Domain (docsshelf.com):

Add FOUR A records:
```
Type: A
Name: @ (or leave blank)
Value: 185.199.108.153
TTL: 3600

Type: A
Name: @
Value: 185.199.109.153
TTL: 3600

Type: A
Name: @
Value: 185.199.110.153
TTL: 3600

Type: A
Name: @
Value: 185.199.111.153
TTL: 3600
```

#### Step 3: Create CNAME File

**In PowerShell:**

```powershell
cd C:\Projects\docsshelf-v7\web

# Create CNAME file (replace with your subdomain)
"legal.docsshelf.com" | Out-File -FilePath CNAME -Encoding ASCII -NoNewline

# Commit and push
git add CNAME
git commit -m "Add custom domain configuration"
git push origin main
```

#### Step 4: Configure in GitHub

1. Go to GitHub repo → **Settings** → **Pages**
2. Under "Custom domain", enter: `legal.docsshelf.com`
3. Click **Save**
4. Wait 10-15 seconds
5. Check **Enforce HTTPS** (this may take 10-15 minutes to become available)

---

## Host Only web/ From a Different GitHub Account

If you want to host the legal pages using a DIFFERENT GitHub account (and/or keep the legal site separate from the app code), the cleanest approach is to create a separate repository that contains ONLY the static site files.

### Why this is recommended

- Keeps app source code and legal hosting separate
- Lets you use GitHub Pages “Deploy from a branch” without needing Actions
- Makes it easy to give a collaborator access to legal pages without giving them access to the full app repo

### Step-by-step (PowerShell)

#### Step 1: Create a new repo on the other GitHub account

On GitHub (logged into the other account):
1. Create a new repository, for example: `docsshelf-legal`
2. Set it to **Public** (simplest for Pages). Private can work too, but keep it simple for Play Console.
3. Do NOT initialize with README (optional)

Copy the repo URL (example):
`https://github.com/OTHER_ACCOUNT/docsshelf-legal.git`

#### Step 2: Create a local folder and copy ONLY the web/ contents

From your current project root:

```powershell
cd C:\Projects\docsshelf-v7

# Create a new working folder for the legal repo
$legalRepo = "C:\Projects\docsshelf-legal"
New-Item -ItemType Directory -Force -Path $legalRepo | Out-Null

# Copy ONLY the website files into the new repo folder
Copy-Item -Recurse -Force "web\*" $legalRepo

cd $legalRepo
```

#### Step 3: Initialize git and push to the other GitHub account

```powershell
git init
git add .
git commit -m "Initial legal pages"

git branch -M main
git remote add origin https://github.com/OTHER_ACCOUNT/docsshelf-legal.git
git push -u origin main
```

#### Step 4: Enable GitHub Pages on the new repo

In the OTHER_ACCOUNT repo:
1. Settings → Pages
2. Source: Deploy from a branch
3. Branch: `main`
4. Folder: `/ (root)`
5. Save

Your default URLs will be:
- `https://OTHER_ACCOUNT.github.io/docsshelf-legal/`
- `https://OTHER_ACCOUNT.github.io/docsshelf-legal/privacy-policy/`
- `https://OTHER_ACCOUNT.github.io/docsshelf-legal/terms-of-service/`

#### Step 5 (optional): Add your custom domain (legal.docsshelf.com)

Follow Option B, but:
- In DNS, point `legal` to `OTHER_ACCOUNT.github.io`
- In GitHub Pages, set custom domain to `legal.docsshelf.com`

### Updating later

When you edit the legal pages in this repo (`C:\Projects\docsshelf-v7\web`), re-copy and push to the legal repo:

```powershell
Copy-Item -Recurse -Force "C:\Projects\docsshelf-v7\web\*" "C:\Projects\docsshelf-legal"
cd C:\Projects\docsshelf-legal
git add .
git commit -m "Update legal pages"
git push
```

#### Step 5: Wait for DNS Propagation

DNS changes take time:
- **Minimum**: 15 minutes
- **Average**: 1-2 hours
- **Maximum**: 24-48 hours

**Check DNS propagation:**
```powershell
# Check if DNS is working
nslookup legal.docsshelf.com

# Expected output should show GitHub's IP addresses
```

Online tools:
- https://dnschecker.org
- https://www.whatsmydns.net

#### Step 6: Verify HTTPS

After DNS propagates and GitHub enables HTTPS:

1. Visit `https://legal.docsshelf.com`
2. Check for padlock icon 🔒 in browser
3. Verify privacy policy loads
4. Test all links work

#### Step 7: Update Play Console

Your final URLs:
```
Privacy Policy: https://legal.docsshelf.com/privacy-policy.html
Terms of Service: https://legal.docsshelf.com/terms-of-service.html
```

Add the Privacy Policy URL to Google Play Console.

---

## DNS Configuration Examples

### Namecheap DNS Settings

**Advanced DNS Tab:**

| Type | Host | Value | TTL |
|------|------|-------|-----|
| CNAME Record | legal | yourusername.github.io | Automatic |

### GoDaddy DNS Settings

**DNS Management:**

| Type | Name | Value | TTL |
|------|------|-------|-----|
| CNAME | legal | yourusername.github.io | 1 Hour |

### Google Domains DNS Settings

**DNS → Custom records:**

| Host name | Type | TTL | Data |
|-----------|------|-----|------|
| legal | CNAME | 3600 | yourusername.github.io |

### Cloudflare DNS Settings

**DNS → Records:**

| Type | Name | Content | Proxy status | TTL |
|------|------|---------|--------------|-----|
| CNAME | legal | yourusername.github.io | DNS only | Auto |

**Important**: In Cloudflare, set Proxy status to "DNS only" (gray cloud) for GitHub Pages.

---

## Troubleshooting

### Issue 1: GitHub Pages Not Showing

**Symptoms**: 404 error when visiting the URL

**Solutions**:
1. Check that you selected `/web` folder (not root `/`)
2. Verify files are in `web/` directory, not project root
3. Wait 3-5 minutes after enabling Pages
4. Check GitHub Actions tab for deployment status

### Issue 2: Custom Domain Not Working

**Symptoms**: DNS_PROBE_FINISHED_NXDOMAIN error

**Solutions**:
1. Verify CNAME record in DNS settings
2. Wait longer (DNS can take 24-48 hours)
3. Check DNS with: `nslookup legal.docsshelf.com`
4. Ensure CNAME file exists in web/ directory
5. Make sure GitHub Pages shows "Custom domain is properly configured"

### Issue 3: HTTPS Not Available

**Symptoms**: "Not Secure" or "Enforce HTTPS" option grayed out

**Solutions**:
1. Wait 10-15 minutes after adding custom domain
2. Uncheck and re-check the "Enforce HTTPS" box
3. Try removing and re-adding the custom domain
4. Ensure DNS is fully propagated first
5. GitHub needs time to generate SSL certificate

### Issue 4: CNAME File Keeps Disappearing

**Symptom**: Custom domain setting resets after a while

**Solution**: Make sure CNAME file is in the `web/` directory, not project root:
```powershell
# Check location
ls C:\Projects\docsshelf-v7\web\CNAME

# If missing, create it:
"legal.docsshelf.com" | Out-File -FilePath C:\Projects\docsshelf-v7\web\CNAME -Encoding ASCII -NoNewline
git add web/CNAME
git commit -m "Fix CNAME location"
git push
```

### Issue 5: Subdomain vs Root Domain

**Question**: Should I use `legal.docsshelf.com` or `docsshelf.com`?

**Answer**: Use subdomain (`legal.docsshelf.com`) because:
- Keeps root domain available for a main website later
- Easier DNS setup (one CNAME vs four A records)
- More flexible for future changes
- Standard practice for legal pages

### Issue 6: Changes Not Appearing

**Symptom**: Updated HTML but old version still shows

**Solutions**:
1. Hard refresh browser: `Ctrl+F5` (Windows) or `Cmd+Shift+R` (Mac)
2. Clear browser cache
3. Check GitHub Actions completed successfully
4. Wait 1-2 minutes for GitHub Pages to rebuild
5. Try incognito/private browsing mode

---

## Updating Legal Pages

### Quick Update Process

1. **Edit files locally**:
   ```powershell
   cd C:\Projects\docsshelf-v7\web
   notepad privacy-policy.html  # Or use VS Code
   ```

2. **Commit and push**:
   ```powershell
   git add .
   git commit -m "Update privacy policy"
   git push
   ```

3. **Wait 1-2 minutes** for changes to go live

### Edit on GitHub Web

1. Go to your repo on GitHub
2. Navigate to `web/privacy-policy.html`
3. Click pencil icon (✏️ Edit)
4. Make changes
5. Scroll down, add commit message
6. Click "Commit changes"
7. Changes go live automatically in 1-2 minutes

---

## Maintenance

### Regular Checks (Monthly)

- [ ] Verify URLs still work
- [ ] Check HTTPS certificate is valid
- [ ] Ensure content matches in-app versions
- [ ] Test on mobile devices
- [ ] Verify all links work

### When to Update

Update your legal pages when:
- App functionality changes
- Data collection practices change
- Privacy laws change
- User rights or policies change
- New features are added

**Important**: Keep in-app and web versions identical!

---

## Security Best Practices

1. **Always use HTTPS**
   - Never use `http://` for legal pages
   - Google Play requires HTTPS

2. **Keep content updated**
   - Match in-app versions exactly
   - Update "Last Updated" date when changing

3. **Test thoroughly**
   - Check on multiple devices
   - Verify all links work
   - Ensure mobile responsive

4. **Monitor access**
   - Check GitHub Pages analytics
   - Watch for broken links
   - Verify uptime

---

## Costs Summary

### One-Time Costs
- Domain registration: $10-15/year (already paid ✅)
- Everything else: **FREE**

### Ongoing Costs
- Domain renewal: $10-15/year
- GitHub Pages: **FREE**
- SSL Certificate: **FREE**
- Bandwidth: **FREE** (unlimited)
- Storage: **FREE**

### Total Annual Cost
**$10-15/year** (just the domain renewal)

---

## Support Resources

### GitHub Pages
- Documentation: https://docs.github.com/pages
- Community Forum: https://github.community

### DNS Help
- DNS Checker: https://dnschecker.org
- What's My DNS: https://www.whatsmydns.net
- DNS Propagation: https://www.whatsmydns.net

### Google Play
- Play Console Help: https://support.google.com/googleplay/android-developer
- Policy Center: https://play.google.com/about/developer-content-policy/

---

## Next Steps

After your legal pages are live:

1. ✅ Copy Privacy Policy URL
2. ✅ Add to Google Play Console
3. ✅ Test the URL in Play Console preview
4. ✅ Complete rest of Play Console setup
5. ✅ Submit app for review

**Your privacy policy is ready for Play Store submission!** 🚀

---

Need help? Create an issue in your GitHub repository or contact feedback@docsshelf.com
