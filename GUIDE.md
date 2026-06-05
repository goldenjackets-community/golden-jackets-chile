# Golden Jackets — Chapter Leader Operations Guide

## Welcome, Chapter Leader! 🐝

This guide covers everything you need to manage your Golden Jackets chapter site. Follow these instructions carefully to avoid breaking the site.

---

## Table of Contents

1. [How the Site Works](#1-how-the-site-works)
2. [How to Edit Files](#2-how-to-edit-files)
3. [Approving Applications](#3-approving-applications-most-common-task)
4. [Adding a New Member (Manual)](#4-adding-a-new-member-manual-method)
5. [Adding an Event](#5-adding-an-event)
6. [Adding an Article/Talk](#6-adding-an-articletalk)
7. [Translating Content](#7-translating-content)
8. [Admin Panel — All Tools](#8-admin-panel--all-tools)
9. [DO NOT TOUCH — Protected Files](#9-do-not-touch--protected-files-)
10. [Troubleshooting](#10-troubleshooting)

---

## 1. How the Site Works

```
You edit files on GitHub
        ↓
GitHub Actions deploys automatically (~1 min)
        ↓
Site updates on your domain
```

- **Repository:** `github.com/goldenjackets-community/golden-jackets-[country]`
- **Branch:** `master` (Poland) or `main` (Brazil)
- **Every push triggers:** S3 upload → CloudFront cache clear → Smoke test
- **If smoke test fails:** site stays on previous version (safe)

---

## 2. How to Edit Files

### On GitHub (recommended for small changes)

1. Go to your repo on GitHub
2. Click the file you want to edit (e.g., `index.html`)
3. Click the **pencil icon** ✏️ (top right)
4. Make your changes
5. Scroll down → write a short description of what you changed
6. Click **"Commit changes"**
7. Wait ~1 minute for deploy
8. Refresh your site to verify

### Locally (for bigger changes)

```bash
git clone https://github.com/goldenjackets-community/golden-jackets-[country].git
cd golden-jackets-[country]
# make your changes
git add .
git commit -m "short description of change"
git push origin master
```

---

## 3. Approving Applications (Most Common Task!)

When someone applies via your chapter site, a Pull Request is created automatically. You approve it from the Admin panel — no coding needed.

### How it works

```
Person fills form on your site
        ↓
Lambda creates PR with their card + photo
        ↓
You get an email notification
        ↓
You approve in Admin panel
        ↓
Site deploys automatically with new member
```

### Steps to Approve

1. Go to your Admin panel (⚙️ button after login)
2. Click **"Pending Members"**
3. You'll see applications with name, city, LinkedIn, photo
4. Click **"Approve & Merge"** to accept
5. Click **"Reject"** to decline (with optional reason)
6. Site auto-deploys in ~1 minute after approval

### Tips
- You have **full autonomy** — approve or reject based on your judgment
- Golden Jacket = all 12 certs active, Alumni = some expired, Challenger = 10-11 certs
- If you see "Pending Articles" — those are blog post submissions from members (same flow: approve/reject)
- If a PR has conflicts, click Approve anyway — the system auto-rebuilds it

---

## 4. Adding a New Member (Manual Method)

> ⚠️ **You usually don't need this!** Members apply via the form and you approve via Admin panel. This section is only for cases where you need to add someone manually.

### Step 1: Add their card to `index.html`

Find the section `🏆 Golden Jackets` and locate the last member card. Copy this template and paste it **before** the Alumni section:

```html
            <div class="member-card" data-state="XX">
                <img src="assets/members/firstname-lastname.jpg" alt="Full Name" style="width:100%;aspect-ratio:1;object-fit:cover;border-radius:12px 12px 0 0;">
                <h3>Full Name</h3>
                <p class="location">City, State, Country</p>
                <span class="tag">Golden Jacket</span>
                <span class="tag">Member</span>
                <p style="color:var(--text-muted);font-size:0.75em;line-height:1.6;">Certified on YYYY-MM-DD</p>
                <a href="https://linkedin.com/in/username" target="_blank" rel="noopener noreferrer" style="color:var(--gold);font-size:1.2em;text-decoration:none;">in</a>
            </div>
```

**Replace:**
- `XX` → State/Voivodeship code (e.g., `SP`, `SL`, `MZ`)
- `firstname-lastname.jpg` → their photo filename
- `Full Name` → their name
- `City, State, Country` → their location
- `YYYY-MM-DD` → certification date
- `linkedin.com/in/username` → their LinkedIn URL

### Step 2: Add their photo

- Upload a square photo (min 200x200px) to `assets/members/`
- Name it: `firstname-lastname.jpg` (lowercase, no spaces)

### Step 3: Update the stats in the ticker

Find the ticker section and update the member count:

```html
<span>🏆 XX Members</span>
```

### Step 4: Create their Lounge access

Go to your Admin panel → **Create User** → enter their email.

---

## 5. Adding an Event

Find the `Upcoming Events` section in `index.html`. Copy this template:

```html
            <div style="background:var(--card);border:1px solid var(--border);border-radius:16px;padding:24px;min-width:250px;max-width:300px;text-align:center;">
                <div style="font-size:2em;margin-bottom:8px;">🇵🇱</div>
                <h3 style="color:white;font-size:1em;margin-bottom:8px;">Event Name</h3>
                <p style="color:var(--text-muted);font-size:0.85em;">📅 Month DD, YYYY</p>
                <p style="color:var(--text-muted);font-size:0.8em;margin-top:8px;">City, Country</p>
                <a href="https://event-url.com" target="_blank" style="color:var(--gold);font-size:0.85em;text-decoration:none;margin-top:12px;display:inline-block;">Learn more →</a>
            </div>
```

---

## 6. Adding an Article/Talk

Find the `Articles & Talks` section. Copy this template:

```html
            <div style="background:var(--card);border:1px solid var(--border);border-radius:12px;padding:20px;text-align:left;">
                <span style="color:var(--gold);font-size:0.8em;">📝 Article</span>
                <span style="color:var(--text-muted);font-size:0.75em;margin-left:8px;">Mon DD, YYYY · Author Name</span>
                <h4 style="color:white;margin:8px 0 6px;font-size:0.95em;">
                    <a href="https://article-url.com" target="_blank" style="color:white;text-decoration:none;">Article Title</a>
                </h4>
                <p style="color:var(--text-muted);font-size:0.8em;line-height:1.5;">Short description of the article.</p>
            </div>
```

---

## 7. Translating Content

The site has a translation system. When the user clicks the flag icon, text switches between English and your local language.

### How it works

In `index.html`, find the `var translations = {` object. It contains key-value pairs:

```javascript
'English text': 'Translated text',
```

### To add a new translation

Add a new line inside the translations object:

```javascript
'Text you want to translate': 'Your translation here',
```

### Important rules

- The English key must match the **exact text** shown on the page
- Don't change the structure (quotes, commas, colons)
- Test after every change — a missing comma breaks everything

---

## 8. Admin Panel — All Tools

### Access the Admin Panel

1. Go to `your-domain.com/members.html`
2. Log in with your admin email
3. Click the **⚙️ Admin** button (top right)

### 📋 List Users

Shows all Lounge members in your chapter with their status (Confirmed or Pending).

### 🌍 All Chapters (Global Admin only)

Shows users from ALL chapters. Only visible to the Founder.

### ➕ Create User

1. Click **Create User**
2. Enter their name and email
3. Click **Create & Send Invite**
4. They receive an email with a temporary password
5. On first login, they set their own password

### 🔄 Resend Pending

Resends invitation emails to all users who haven't logged in yet (status: FORCE_CHANGE_PASSWORD). Useful when someone lost their invite email.

### 🗑️ Delete User

1. Click **Delete User**
2. Enter the email of the user to remove
3. Confirm — this permanently removes their Lounge access

### 💾 Backup Status

Shows the latest backups of your chapter's S3 bucket. Backups run daily (7-day retention). Statuses:
- **COMPLETED** — backup successful
- **RUNNING** — backup in progress
- **FAILED** — check with Ricardo

### 🔄 Restore Backup (Global Admin only)

Restores the site from the latest backup. Use only if the site is broken and you need to roll back. Only the Founder can execute this.

### 📊 Export CSV

Exports the list of all Lounge users in your chapter as a CSV file (email, status, creation date). Useful for reporting.

### 📈 Show Metrics

Displays site visitor metrics (total visits, unique visitors). Data comes from the visitor counter on the site.

### ⬆️ Promote Challenger

Promotes a Challenger (11/12 certs) to Golden Jacket status. Enter their email — this updates their role in the system.

### 🔀 Move Member

Moves a member between categories (Golden Jacket ↔ Alumni ↔ Challenger). Use when a member's certification status changes.

### 📷 Change Photo

Updates a member's photo. Select the member from the dropdown, upload the new photo, and it gets pushed to the repo automatically.

### 📋 Backlog

Shows the project backlog (from `BACKLOG.md` in your repo). Use this to track what's done and what's pending for your chapter.

---

## 9. DO NOT TOUCH — Protected Files ⚠️

These files control infrastructure and authentication. **Do not edit them:**

| File | Why |
|------|-----|
| `config.js` | Admin authentication settings |
| `.github/workflows/` | Deployment pipeline |
| `members.html` | Lounge authentication logic |
| `admin.html` | Admin panel logic |

**If you accidentally break something:**

1. Don't panic
2. Go to GitHub → your repo → the file you changed
3. Click "History" → find the previous version → "Revert"
4. Or message Ricardo (Founder) for help

---

## 10. Troubleshooting

### Site not updating after commit

- Wait 1-2 minutes (deploy takes time)
- Hard refresh: `Ctrl + Shift + R`
- Check GitHub Actions tab for errors

### Deploy failed (red X in Actions)

- Click the failed run → read the error
- Most common: syntax error in HTML (missing quote or bracket)
- Fix the error and push again

### Translation not working

- Check for missing commas in the translations object
- The English key must match **exactly** (including spaces and punctuation)
- Open browser console (F12) to check for JS errors

### Can't access Admin panel

- Make sure you're logged into the Lounge first
- Hard refresh (`Ctrl + Shift + R`)
- If still broken, contact Ricardo

---

## Quick Reference

| Task | How |
|------|-----|
| Add member | Edit `index.html` → copy card template → upload photo |
| Add event | Edit `index.html` → copy event template |
| Add article | Edit `index.html` → copy article template |
| Create Lounge user | Admin panel → Create User |
| Delete Lounge user | Admin panel → Delete User |
| Translate text | Edit `index.html` → add to translations object |
| Check deploy | GitHub → Actions tab |

---

## Need Help?

Contact **Ricardo Gulias** (Founder & Global Lead):
- Email: ricardo.gulias@goldenjacketsbrazil.com
- LinkedIn: /in/yourprofile

---

*Golden Jackets Community · Operations Guide v1.0 · May 2026*
