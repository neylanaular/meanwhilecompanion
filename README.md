# meanwhilecompanion.com

Public site for Meanwhile Companion: landing page, privacy note, and App Store link.

## What’s here

- `index.html` — one quiet landing composition
- `privacy.html` — privacy note (canonical for the app)
- Contact: [hello@meanwhilecompanion.com](mailto:hello@meanwhilecompanion.com)
- App Store: [apps.apple.com/app/id6791992091](https://apps.apple.com/app/id6791992091)

## Email (GoDaddy)

If GoDaddy already gave you `hello@meanwhilecompanion.com`, leave their **MX / email DNS** alone. Only change the website (A / CNAME) records below. Do not delete MX, TXT (SPF), or Autodiscover records GoDaddy added for mail.

Webmail is usually at [https://email.godaddy.com](https://email.godaddy.com) or via the Microsoft 365 / Workspace Email link in your GoDaddy account.

The site already links `mailto:hello@meanwhilecompanion.com`.

## Deploy (GitHub Pages + GoDaddy DNS)

Recommended: host the static files on GitHub Pages; keep the domain and email at GoDaddy.

### 1. Put the site on GitHub

```bash
cd meanwhile-web
git init
git add .
git commit -m "Add Meanwhile Companion site"
# Create repo on GitHub (e.g. neylanaular/meanwhilecompanion), then:
git branch -M main
git remote add origin git@github.com:YOUR_USER/meanwhilecompanion.git
git push -u origin main
```

GitHub → repo → **Settings → Pages** → Source: **Deploy from a branch** → `main` / `/ (root)`.  
Custom domain: `meanwhilecompanion.com` (this folder already has a `CNAME` file).

### 2. Point the domain in GoDaddy (do not touch email records)

1. GoDaddy → **My Products** → Domains → **meanwhilecompanion.com** → **DNS** (or “Manage DNS”).
2. Turn **off** GoDaddy Website Builder / “Forwarding” for the domain if it is on (forwarding fights custom A records).
3. Under **A** records for `@` (the apex / root):
   - Delete or edit any existing A record that points at GoDaddy parking / a builder IP.
   - Add **four** A records, all with Host `@`, pointing to GitHub Pages:

     | Type | Name | Value | TTL |
     |------|------|-------|-----|
     | A | `@` | `185.199.108.153` | 1 Hour |
     | A | `@` | `185.199.109.153` | 1 Hour |
     | A | `@` | `185.199.110.153` | 1 Hour |
     | A | `@` | `185.199.111.153` | 1 Hour |

4. Optional **www**: add or edit CNAME — Name `www`, Value `YOUR_GITHUB_USER.github.io` (use your GitHub username, with the trailing `.github.io`).
5. **Leave alone:** MX, email-related TXT/SPF, CNAME for `email` / Autodiscover, etc.
6. Save. Wait 15 minutes to a few hours. In the GitHub Pages settings, wait until the domain shows a checkmark, then turn on **Enforce HTTPS**.

If GoDaddy still shows a “coming soon” or parked page, an old A record or domain forwarding is still active — remove those, keep only the four GitHub A records for `@`.

### Preview locally

```bash
cd meanwhile-web
npx --yes serve .
# open http://localhost:3000
```

## When the App Store is live

In `index.html`, replace the soon CTA with something like:

```html
<a class="cta" href="https://apps.apple.com/app/idXXXXXXXXX">
  Download on the App Store
</a>
```

Use Apple’s badge asset if you want the official mark; keep the page one composition (brand + line + one CTA).

## Privacy URL for App Store Connect

Prefer: `https://meanwhilecompanion.com/privacy.html`  
(The older `https://neylanaular.com/meanwhile-privacy.html` can redirect or stay as a mirror.)
