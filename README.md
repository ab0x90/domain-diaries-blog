# The Domain Diaries

A Jekyll-powered pentesting blog hosted on GitHub Pages at **thedomaindiaries.com**

---

## 🚀 COMPLETE SETUP GUIDE

Follow these steps in order to get your blog live.

---

### STEP 1: CREATE A GITHUB REPOSITORY

1. Go to [github.com/new](https://github.com/new)
2. Repository name: `domain-diaries` (or anything you want)
3. Make it **Public**
4. **DO NOT** initialize with README, .gitignore, or license (we have files already)
5. Click **Create repository**

---

### STEP 2: PUSH THE CODE TO GITHUB

Open a terminal/PowerShell in the blog folder and run:

```powershell
cd C:\Users\unknown\.openclaw\workspace\domain-diaries-blog

git init
git add .
git commit -m "Initial commit - The Domain Diaries"
git branch -M main
git remote add origin https://github.com/YOURUSERNAME/domain-diaries.git
git push -u origin main
```

**REPLACE `YOURUSERNAME` WITH YOUR ACTUAL GITHUB USERNAME!**

---

### STEP 3: ENABLE GITHUB PAGES

1. Go to your repository on GitHub
2. Click **Settings** (top menu bar)
3. Click **Pages** (left sidebar)
4. Under "Source", select:
   - Branch: **main**
   - Folder: **/ (root)**
5. Click **Save**

Wait 1-2 minutes. GitHub will build your site.

---

### STEP 4: CONFIGURE DNS FOR YOUR CUSTOM DOMAIN

Go to your domain registrar (wherever you bought thedomaindiaries.com) and add these DNS records:

#### A Records (for root domain)

| Type | Name/Host | Value |
|------|-----------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

#### CNAME Record (for www subdomain)

| Type | Name/Host | Value |
|------|-----------|-------|
| CNAME | www | YOURUSERNAME.github.io |

**NOTE:** Replace `YOURUSERNAME` with your GitHub username.

**NOTE:** Some registrars use `@` for the root domain, others want you to leave the Name field blank. Check your registrar's docs if unsure.

---

### STEP 5: CONNECT CUSTOM DOMAIN IN GITHUB

1. Go to your repository → **Settings** → **Pages**
2. Under **Custom domain**, enter: `thedomaindiaries.com`
3. Click **Save**
4. Wait for DNS to propagate (can take 10 minutes to 48 hours, usually fast)
5. Once the DNS check passes, check **Enforce HTTPS**

---

### STEP 6: VERIFY IT'S WORKING

Test your site:

- Visit: **https://thedomaindiaries.com**
- Visit: **https://www.thedomaindiaries.com** (should redirect)

If you see your blog with the logo banner, YOU'RE LIVE! 🎉

---

## 📝 HOW TO ADD NEW BLOG POSTS

### 1. Create a new file in the `_posts` folder

Filename format: `YYYY-MM-DD-your-post-title.md`

Example: `_posts/2026-02-20-kerberoasting-a-bank.md`

### 2. Add the post header (front matter)

Every post needs this at the top:

```markdown
---
layout: post
title: "Your Post Title Here"
date: 2026-02-20
tags: [kerberos, active-directory, credentials]
---
```

### 3. Write your content in Markdown

```markdown
---
layout: post
title: "How I Kerberoasted My Way to Domain Admin"
date: 2026-02-20
tags: [kerberos, AD, windows]
---

This is the intro paragraph. Set the scene.

## The Recon Phase

Start your story here. Explain what you found.

### Finding the Service Account

I ran BloodHound and found an interesting path...

```powershell
Get-ADUser -Filter {ServicePrincipalName -ne "$null"} -Properties ServicePrincipalName
```

The output showed a juicy service account with an SPN...

## The Exploitation

Here's how I popped it.

> **Pro tip:** Always check for weak passwords on service accounts.

## Lessons Learned

- Bullet point one
- Bullet point two
- Bullet point three

---

*Stay curious. Stay ethical.*
```

### 4. Push to GitHub

```powershell
git add .
git commit -m "Add new post: Kerberoasting story"
git push
```

GitHub Pages will automatically rebuild. Your post goes live in ~1-2 minutes.

---

## 📁 FILE STRUCTURE REFERENCE

```
domain-diaries-blog/
├── CNAME                    ← Your custom domain
├── _config.yml              ← Site settings (title, description)
├── _layouts/
│   ├── default.html         ← Main template with banner
│   └── post.html            ← Blog post template
├── _posts/                  ← YOUR BLOG POSTS GO HERE
│   └── 2026-02-17-welcome-to-the-domain-diaries.md
├── assets/
│   ├── css/
│   │   └── style.css        ← All styling (dark theme)
│   └── images/
│       └── domain-diaries-logo.svg  ← Banner logo
├── index.html               ← Homepage (lists all posts)
├── about.md                 ← About page
└── README.md                ← This file
```

---

## 🎨 CUSTOMIZATION

### Change Site Title/Description

Edit `_config.yml`:

```yaml
title: The Domain Diaries
description: Real pentesting stories from the trenches of Active Directory
author: Your Name Here
```

### Change Colors

Edit `assets/css/style.css` and modify the variables at the top:

```css
:root {
    --bg-primary: #0a0a0f;      /* Main background */
    --bg-secondary: #12121a;    /* Header/footer background */
    --accent-cyan: #00d4ff;     /* Headers, links */
    --accent-red: #ff6b6b;      /* Tags, highlights */
    --accent-green: #00ff88;    /* Code, terminal text */
}
```

### Update the Logo

Replace `assets/images/domain-diaries-logo.svg` with your own image.

### Edit the About Page

Edit `about.md` with your own bio and info.

---

## 🔧 LOCAL PREVIEW (OPTIONAL)

If you want to preview changes before pushing:

```powershell
# Install Ruby and Jekyll (one time)
# Download Ruby: https://rubyinstaller.org/

gem install bundler jekyll

# Create Gemfile
echo 'source "https://rubygems.org"' > Gemfile
echo 'gem "jekyll"' >> Gemfile
echo 'gem "webrick"' >> Gemfile

bundle install

# Run local server
bundle exec jekyll serve

# Visit http://localhost:4000
```

---

## 🛠️ TROUBLESHOOTING

### Site not loading?
- Wait 10-30 minutes for DNS propagation
- Check GitHub Pages settings to ensure it's enabled
- Verify DNS records are correct

### CSS not loading?
- Make sure `baseurl` in `_config.yml` is empty: `baseurl: ""`
- Clear browser cache and hard refresh (Ctrl+Shift+R)

### Posts not showing?
- Check filename format: must be `YYYY-MM-DD-title.md`
- Check the date in front matter isn't in the future
- Make sure `layout: post` is in the front matter

### Custom domain not working?
- Verify CNAME file contains exactly: `thedomaindiaries.com`
- Check all 4 A records are added correctly
- Wait for DNS propagation (use `nslookup thedomaindiaries.com` to check)

---

## 📋 QUICK REFERENCE: NEW POST CHECKLIST

1. ☐ Create file: `_posts/YYYY-MM-DD-title.md`
2. ☐ Add front matter (layout, title, date, tags)
3. ☐ Write content in Markdown
4. ☐ `git add .`
5. ☐ `git commit -m "Add post: title"`
6. ☐ `git push`
7. ☐ Wait 1-2 min, check site

---

Happy hacking! 🍌

*— Built with King Ape Energy*
