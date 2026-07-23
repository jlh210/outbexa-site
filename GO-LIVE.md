# Take Outbexa live on outbexa.com

Your site is 4 files, all ready in this folder:
`index.html` · `checkout.html` · `sitemap.xml` · `robots.txt`

The plan: host the files free on **Netlify**, then point your **GoDaddy** domain at it. ~15 minutes, no code.

---

## Step 1 — Put the files on Netlify (5 min)

1. Go to **app.netlify.com** and sign up (free — use Google/email).
2. On the dashboard, find the **"Add new site" → "Deploy manually"** area (a drag-and-drop box that says *"Drag and drop your site output folder here"*).
3. Drag this entire folder (the one containing `index.html`) onto that box.
4. Netlify uploads it and gives you a live URL like `random-name-123.netlify.app`. **Click it — your site is already live.** Test the film, the buttons, checkout.

> Netlify serves your exact files unchanged, so it looks identical to what you've been reviewing.

## Step 2 — Add your domain in Netlify (2 min)

1. In your new site: **Domain management** (or **Site configuration → Domains**) → **Add a domain**.
2. Type **outbexa.com** → Add. Netlify will say it's not pointing here yet and show you DNS records — that's Step 3.
3. Also add **www.outbexa.com** when prompted (Netlify sets up the redirect for you).

## Step 3 — Point GoDaddy at Netlify (5 min + wait)

1. Log in to **GoDaddy** → **My Products** → next to **outbexa.com** click **DNS** (or **Manage DNS**).
2. You'll edit two records:

   **A record (the root domain):**
   - Type: `A` · Name: `@` · Value: **`75.2.60.5`** · TTL: default
   - (This is Netlify's load-balancer IP. If Netlify shows a *different* IP in your dashboard, use theirs.)

   **CNAME record (the www version):**
   - Type: `CNAME` · Name: `www` · Value: **your Netlify subdomain**, e.g. `random-name-123.netlify.app` · TTL: default

3. If GoDaddy already has an existing `A @` record or a `CNAME www` (parked page), **edit those instead of adding duplicates**.
4. Save.

## Step 4 — Wait, then confirm HTTPS

- DNS takes anywhere from 10 minutes to a few hours to propagate (GoDaddy often ~30 min).
- Back in Netlify → Domains, once it detects the change it **auto-issues a free SSL certificate** (the padlock). You don't do anything — just check back; when it says "Netlify DNS / HTTPS enabled," visit **https://outbexa.com**.

---

## Step 5 — Turn on Google (do this once you're live)

1. Go to **Google Search Console** (search.google.com/search-console) → add property **outbexa.com** → verify (easiest: the DNS TXT method, added in GoDaddy the same way as above).
2. Submit your sitemap: in Search Console → **Sitemaps** → enter `sitemap.xml` → Submit.
3. That's what gets you indexed and eligible for the sitelinks/FAQ rich results already built into the page.

---

## Before you flip it on — 3 quick checks

- **Stripe:** confirm your Stripe product price is **$389/mo** (the page says $389; Stripe charges whatever the product is set to).
- **Stripe confirmation page:** in the Payment Link settings, set the post-payment redirect to your **Calendly onboarding link** — makes the "book your onboarding call from the confirmation page" copy literally true.
- **Calendly:** the discovery-call link is already wired (`jackie-jackie-ai/outbexa-discovery-call`) — just click a "Book a Call" on the live site once to confirm.

---

## If you'd rather not touch DNS yourself
Netlify can also **buy/manage the DNS for you** — in Domains, choose "Set up Netlify DNS" and it gives you 4 nameservers to paste into GoDaddy (GoDaddy → DNS → Nameservers → Change → "I'll use my own"). That replaces Step 3 entirely and Netlify handles the rest. Either path works; the A/CNAME method above keeps GoDaddy in control.

Cloudflare Pages and Vercel work the same way if you prefer them — same drag-or-connect, same "add domain + edit GoDaddy DNS" flow.
