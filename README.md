# KwikWork Website (US edition) — Getting Live on kwikwork.online

Your complete website is the single file `index.html`. No installs, no build
tools — it works anywhere. This guide gets it live on your Hostinger domain.

---

## Step 0 — Check what you actually bought on Hostinger

Log in at **hpanel.hostinger.com** and look at the dashboard:

- **If you see a "Websites" section** (or an "Add Website" button) → you have a
  hosting plan. Continue with **Option A**.
- **If it only shows your domain** (no website section) → you bought just the
  domain name. You need somewhere to host the site:
  - **Option A (easiest):** buy a Hostinger shared hosting plan (includes free SSL).
  - **Option B (free):** host on GitHub Pages or Netlify and point your domain
    to it — see **Option B**.

---

## Option A — Host on Hostinger (recommended)

1. In hPanel open **Websites → Dashboard** (or **File Manager**).
2. Open the `public_html` folder.
3. Delete the default files Hostinger put there.
4. Click **Upload** and upload `index.html`.
5. Visit **https://kwikwork.online** — done. Free SSL is included automatically
   (if needed: **Security → SSL → Install**, wait ~15 minutes).

## Option B — Free hosting on Netlify (detailed steps)

Your site is one static file, so it hosts free on Netlify forever. Total cost: $0.

1. **Download** `kwikwork-deploy.zip` (from this workspace) and **extract** it —
   you get a folder `kwikwork` containing `index.html`. Don't rename the file.
2. **Sign up free** at **app.netlify.com** (email or Google — no card needed).
3. **Deploy:** on the dashboard click **Add new site → Deploy manually**, then
   drag the whole `kwikwork` FOLDER into the drop zone. Netlify gives you a
   live test URL like `https://something.netlify.app` — check the site loads.
4. **Add your domain:** **Site configuration → Domain management → Add a
   domain** → type `kwikwork.online` → Add.
5. **Point Hostinger DNS** (hPanel → Domains → kwikwork.online → DNS /
   Nameservers → Manage DNS records). Keep Hostinger's nameservers — do NOT
   switch to Netlify DNS (keeps your email forwarding working). Add:

   | Type | Name | Points to |
   |---|---|---|
   | A | @ | 75.2.60.5 |
   | A | @ | 99.83.190.102 |
   | CNAME | www | your-site-name.netlify.app |

   If a record of the same type/name already exists, EDIT it instead of adding
   a duplicate. (Netlify also shows these values in step 4 — use theirs if
   they differ.)
6. **SSL:** back in Netlify → Domain management — it auto-issues a free
   Let's Encrypt certificate once DNS propagates (usually ~30 min, up to 24 h).
7. **Email forwarding (critical):** hPanel → **Emails → Email forwarders** →
   forward `hello@kwikwork.online` → your personal Gmail. Test by clicking
   "Apply by Email" on your live site.

**Common gotchas:** drag the FOLDER, not the zip · `index.html` must sit at the
top level of that folder · the `www` CNAME value must be YOUR netlify.app
subdomain · a Netlify warning about "not using Netlify DNS" is safe to ignore —
records in Hostinger are enough.

## Option C — Free hosting on GitHub Pages (detailed steps)

Pick ONE host (B or C) — the domain can only point to one. GitHub Pages takes
a few more clicks than Netlify but gives you version history (free backup)
and developer skills.

1. **Sign up free** at **github.com**.
2. Click **+ → New repository** → name it `kwikwork` → Public → Create.
3. Click **"uploading an existing file"** → drag `index.html` → **Commit changes**.
4. **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main`,
   folder `/ (root)` → Save. Wait ~1 min → site is live at
   `https://yourusername.github.io/kwikwork/` — verify it loads.
5. Still in **Settings → Pages → Custom domain** → `kwikwork.online` → Save.
6. **Hostinger DNS** (hPanel → Domains → kwikwork.online → DNS → Manage DNS
   records) — keep Hostinger nameservers, add:

   | Type | Name | Points to |
   |---|---|---|
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |
   | CNAME | www | yourusername.github.io |

7. Back in GitHub Pages settings → **Verify**. After DNS propagates
   (~30 min – 24 h) GitHub issues free SSL → tick **Enforce HTTPS**.
8. **Email forwarding (critical):** hPanel → **Emails → Email forwarders** →
   `hello@kwikwork.online` → your Gmail.

**To update the site later:** edit `index.html`, upload it to the repo again
(commit), and the site updates itself in ~a minute. The **Actions** tab shows
each deployment, and you can roll back to any previous version.

---

## ⚠️ Critical for the US edition — set up your email

Every "Apply by Email" button and the contact form sends to
**hello@kwikwork.online**. That mailbox must actually exist or you will never
see an application:

1. Hostinger hPanel → **Emails** (for your domain).
2. Either create a mailbox `hello@kwikwork.online`, **or** (cheaper) set up
   **email forwarding**: `hello@kwikwork.online` → your personal Gmail.
   - Email forwarding is included free with Hostinger domains — you do NOT
     need a hosting plan for it.
3. Test it: open your website, click "Apply by Email" on any job, send the
   email, and confirm it arrives.

## Getting a US phone number (optional but recommended)

The site shows **+1 (555) 000-0000** as a placeholder. If you want a real US
number that rings you anywhere, get a virtual number from a service like
OpenPhone, Sonetel, or Skype Number (a few dollars/month), then replace the
placeholder in the file. If you prefer email-only, just remove the phone cards.

---

## Before you go live — customize these

Open `index.html` in any text editor (Notepad works) and change:

| What | Search for | Replace with |
|---|---|---|
| Application email | `hello@kwikwork.online` (many places) | your real inbox/forwarder |
| Phone number | `+15550000000` and `+1 (555) 000-0000` | your US virtual number |
| Job listings | the `JOBS = [...]` list in the `<script>` section | your real jobs (US salaries) |
| Locations | `New York, NY` etc. in the two `<select>` lists + jobs | cities you actually serve |
| Category counts | the `CATEGORIES = [...]` list | your real numbers |
| Stats (500+ jobs etc.) | the `hero-stats` section | your real stats |
| Testimonials | the testimonials section | real quotes (or remove) |

## How the site works (no backend needed)

- **Applications open the visitor's email app** with everything pre-filled —
  resumes land in your `hello@` inbox. No server or database needed.
- To add a job: copy one entry in the `JOBS` list, change the details, save,
  re-upload. It appears instantly on the site.

## Future upgrades (when you're ready)

- Online resume upload + employer dashboards + accounts → needs a backend
  (phase 2).
- Add an EEO / equal-opportunity statement — standard for US job boards.
- SEO: submit kwikwork.online to Google Search Console after launch.
