# Karepoint Website — Non-Technical Guide

This guide walks you through everything you need to manage your website.
No technical experience required. Follow each step exactly as written.

---

## Table of Contents

1. [What You Have](#1-what-you-have)
2. [First-Time Deployment to Cloudflare Pages](#2-first-time-deployment)
3. [How to Update Content](#3-how-to-update-content)
4. [How Blog Articles Work](#4-how-blog-articles-work)
5. [How the Contact Form Works](#5-how-the-contact-form-works)
6. [Rolling Back to a Previous Version](#6-rolling-back)
7. [Frequently Asked Questions](#7-faq)
8. [Who to Contact for Help](#8-who-to-contact)

---

## 1. What You Have

Your website is three pages:

| File | Page | URL |
|------|------|-----|
| `index.html` | Homepage | mykarepoint.com |
| `blog/index.html` | Blog / Insights | mykarepoint.com/blog |
| `privacy/index.html` | Privacy Policy | mykarepoint.com/privacy |

There is also a backup file called `karepoint-website.ROLLBACK.html`
which is an older version of the homepage. Keep this file safe.

Your folder looks like this:
```
karepoint/
├── index.html
├── blog/
│   └── index.html
├── privacy/
│   └── index.html
└── README.md (this file)
```

---

## 2. First-Time Deployment

### Step A: Create a GitHub Account (free)

1. Go to https://github.com
2. Click **Sign up**
3. Use your work email (info@mykarepoint.com or suvraneelm@mykarepoint.com)
4. Choose the **Free** plan
5. Verify your email address

### Step B: Create a Repository

A repository is just a folder on GitHub where your website files live.

1. After logging in, click the **+** button (top right)
2. Click **New repository**
3. Repository name: `karepoint-website` (no spaces)
4. Set it to **Private** (important — keeps your code private)
5. Leave everything else as-is
6. Click **Create repository**

### Step C: Upload Your Files

1. On the repository page, click **uploading an existing file**
2. Drag the entire `karepoint` folder contents into the upload box:
   - `index.html`
   - `blog/index.html` (create the blog folder first — click "create new file", name it `blog/index.html`, paste the content)
   - `privacy/index.html` (same process — create `privacy/index.html`)
3. At the bottom, click **Commit changes**

> **Easier option:** Install GitHub Desktop (https://desktop.github.com) and drag-drop the folder.
> It handles uploads automatically. Recommended for non-technical users.

### Step D: Set Up Cloudflare Pages

Cloudflare Pages is the free hosting service we are using.

1. Go to https://pages.cloudflare.com
2. Click **Sign up** (use the same email as your domain)
3. After logging in, click **Create a project**
4. Click **Connect to Git**
5. Click **Connect GitHub** and authorize Cloudflare
6. Select your `karepoint-website` repository
7. Click **Begin setup**

On the setup screen:
- **Project name:** karepoint (this becomes the preview URL)
- **Production branch:** main
- **Build command:** leave this EMPTY
- **Build output directory:** leave this EMPTY (or type `/`)
- Click **Save and Deploy**

Cloudflare will deploy your site. This takes about 1 minute.
You will get a URL like `karepoint.pages.dev` to preview it.

### Step E: Connect Your Domain

1. In Cloudflare Pages, go to your project
2. Click **Custom domains**
3. Click **Set up a custom domain**
4. Enter: `mykarepoint.com`
5. Cloudflare will show you DNS records to add

Now log in to **Spaceship** (where your domain is registered):
1. Go to https://spaceship.com and log in
2. Go to **DNS settings** for mykarepoint.com
3. Add the records Cloudflare showed you (CNAME or A records)
4. Save

DNS changes take 1 to 24 hours to fully work worldwide.
After that, your site is live at mykarepoint.com.

---

## 3. How to Update Content

### To change text on any page:

1. Open the file you want to edit (e.g., `index.html`) in a text editor
   - Mac: TextEdit (set to Plain Text mode) or download VS Code (free, recommended)
   - Windows: Notepad or download VS Code (free, recommended)
   - VS Code download: https://code.visualstudio.com
2. Use **Find** (Ctrl+F or Cmd+F) to search for the text you want to change
3. Edit the text directly
4. Save the file
5. Upload the changed file to GitHub (see Uploading Changes below)

### Uploading Changes to GitHub (after editing)

**If using GitHub Desktop:**
1. Open GitHub Desktop
2. It shows you what changed (green = added, red = removed)
3. Write a short note in the "Summary" box (e.g., "Updated services section")
4. Click **Commit to main**
5. Click **Push origin**
6. Cloudflare automatically detects the change and updates your live site within 1-2 minutes

**If uploading manually on GitHub.com:**
1. Go to your repository
2. Navigate to the file you changed
3. Click the pencil icon (Edit)
4. Paste your updated content
5. Click **Commit changes**

### Common text changes and where to find them:

| What you want to change | Search for this text |
|------------------------|---------------------|
| Announcement bar text | `Now accepting Q3 2026` |
| Hero headline | `The revenue your` |
| Hero sub-headline | `Verification of benefits and prior authorization` |
| CTA section headline | `Find out where your` |
| Contact email | `info@mykarepoint.com` |
| Company tagline | `Faith Over Fear` |
| Footer copyright year | `2026 Karepoint` |

---

## 4. How Blog Articles Work

### How it works (simple version):

1. You write and publish an article on Medium at https://medium.com/@karepoint
2. Medium automatically adds it to your profile feed
3. Your blog page (mykarepoint.com/blog) fetches your articles from Medium every time someone visits
4. New articles appear automatically — you do not need to update your website

### You do not need to touch the website when you publish a new article.

### To publish an article on Medium:

1. Go to https://medium.com and log in
2. Click **Write** (top right)
3. Write your article
4. Before publishing, click the three dots (...) and select **Add to Publication**
5. Select **Karepoint Insights** (create this publication first — see below)
6. Click **Publish**

### Creating the Karepoint Insights Publication (one time only):

1. On Medium, click your profile photo
2. Click **Manage Publications**
3. Click **New publication**
4. Name: `Karepoint Insights`
5. Description: Expert insights on behavioral health revenue cycle management
6. Upload your Karepoint logo as the publication image
7. Click **Create**

After this, all future articles can be published under Karepoint Insights.

### What happens if the blog shows an error?

The blog page tries to load your articles automatically.
If Medium is temporarily unavailable, visitors see a message with a link to your Medium profile directly.
This is normal and does not require any action from you.

---

## 5. How the Contact Form Works

### What happens when someone fills the form:

1. Visitor fills in: Name, Phone, Business Email, Role, Facility Name, Facility Type, Question
2. They click **Request Discovery Call**
3. The form validates their inputs (checks for valid US phone, blocks Gmail/Yahoo, etc.)
4. If valid, it opens a pre-filled email addressed to info@mykarepoint.com
5. The visitor clicks send in their email client
6. You receive the inquiry in your inbox

### You receive inquiries at: info@mykarepoint.com

### What validation does the form check?

- **Name:** Cannot be empty
- **Phone:** Must be a valid US phone number (with or without +1)
- **Business Email:** Must be a real business email. Gmail, Yahoo, Hotmail, Outlook, iCloud are blocked
- **Role:** Must select from the dropdown
- **Facility Name:** Cannot be empty
- **Facility Type:** Must select from the dropdown
- **Question:** Cannot be empty

### Known limitation:

The form currently uses email (mailto) to deliver submissions.
This means the visitor's own email app opens and they click send.
This works, but some people may not complete that last step.

When you are ready for a more robust solution, ask a developer to connect
the form to Formspree (https://formspree.io) which captures submissions
directly without requiring the visitor to use their email app.
This takes about 15 minutes to set up and has a free tier.

---

## 6. Rolling Back

### If something breaks on the homepage and you need to go back:

You have a rollback file saved at:
`karepoint-website.ROLLBACK.html`

To use it:
1. Rename it to `index.html`
2. Upload it to GitHub in place of the current `index.html`
3. Cloudflare will automatically redeploy the old version
4. Your site is back to the previous version within 1-2 minutes

### Rolling back via GitHub directly:

1. Go to your GitHub repository
2. Click on `index.html`
3. Click **History** (top right of the file view)
4. Find the version you want to restore
5. Click on it, then click **Browse files**
6. Download that version and re-upload as the current `index.html`

---

## 7. Frequently Asked Questions

**Q: How do I add a new service to the Services section?**

Open `index.html` and search for `svc-item act`. You will see the list of services. Copy one of the service items (from `<li class="svc-item">` to the closing `</li>`) and paste it after the last item. Change the number, name, badge, and description text.

---

**Q: How do I change the email address the form sends to?**

Open `index.html` and search for `info@mykarepoint.com`. You will find it in the form JavaScript section. Change it there.

---

**Q: The blog page says "Articles loading" but nothing appears. What do I do?**

This usually means Medium's feed API is temporarily slow. Wait 10-15 minutes and refresh.
If it persists, check that your Medium profile (https://medium.com/@karepoint) is publicly visible.

---

**Q: How do I update the Privacy Policy?**

Open `privacy/index.html` and search for the text you want to update.
The document is divided into numbered sections (01 through 10).
Each section has a `<p>` tag with the content. Edit the text and save.

Look for yellow "To complete" boxes in the file — these are placeholders
that need to be filled in before the privacy policy goes live publicly.

---

**Q: Can I add a new page to the website?**

Yes. Create a new folder (e.g., `about`) and put an `index.html` inside it.
Copy the nav and footer from an existing page, then add your content.
Upload to GitHub and it becomes available at mykarepoint.com/about.

---

**Q: How do I know if my site is working properly?**

Visit these URLs after deployment:
- https://mykarepoint.com — Homepage
- https://mykarepoint.com/blog — Blog page
- https://mykarepoint.com/privacy — Privacy Policy

If any page shows an error, check GitHub to confirm the file was uploaded correctly.

---

**Q: What does "Commit" mean?**

A commit is just saving your changes to GitHub. Think of it like clicking Save,
except it also tracks the history of every change you have ever made,
so you can always go back.

---

**Q: Do I need to renew anything?**

| Service | Renewal | Where |
|---------|---------|-------|
| mykarepoint.com domain | Annually | Spaceship.com |
| Cloudflare Pages hosting | Free (no renewal) | Cloudflare |
| GitHub repository | Free (no renewal) | GitHub |
| Medium account | Free (no renewal) | Medium |

---

## 8. Who to Contact for Help

| Need | Contact |
|------|---------|
| Website code changes | Bring back to this Claude chat |
| Domain issues | Spaceship support: https://spaceship.com/support |
| Hosting issues | Cloudflare support: https://support.cloudflare.com |
| Medium issues | Medium help: https://help.medium.com |
| Form backend upgrade (Formspree) | https://formspree.io/help |

---

*This guide was prepared for Karepoint Billing Service LLP — July 2026.*
*Keep this file in your website folder as a permanent reference.*
