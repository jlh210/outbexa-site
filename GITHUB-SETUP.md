# Connect Outbexa to GitHub → auto-deploy on Cloudflare Pages

One-time setup, ~10 minutes, no command line. After this, any change I make gets committed to GitHub and Cloudflare rebuilds outbexa.com automatically.

The 5 files that go in the repo:
`index.html` · `checkout.html` · `sitemap.xml` · `robots.txt` · `_headers`
(Skip the `.md` guide files — they don't need to ship.)

---

## Step 1 — Create the GitHub repo (3 min)

1. Go to **github.com** → sign in → click the **+** (top right) → **New repository**.
2. Repository name: **`outbexa-site`**
3. Set it to **Public** (Cloudflare Pages connects to public repos with zero extra config; private works too but public is simplest).
4. Leave "Add a README" **unchecked**.
5. Click **Create repository**.

## Step 2 — Upload the site files (2 min)

1. On the new empty repo page, click the link **"uploading an existing file"** (in the quick-setup text), or go to **Add file → Upload files**.
2. Drag in the **5 files** listed above (download them from the file cards I share in chat first).
   - Important: upload the **files themselves** at the top level — not a folder containing them. `index.html` must sit at the repo root.
3. At the bottom, **Commit changes** (green button).

## Step 3 — Connect Cloudflare Pages to the repo (4 min)

> Note: your site is currently a **Workers** upload (`outbexa`). This creates a **Pages** project instead — the modern Git-connected way. We'll point the domain to the new Pages project and retire the old Worker.

1. In Cloudflare dash → **Workers & Pages** → **Create** → **Pages** tab → **Connect to Git**.
2. Authorize GitHub, pick the **`outbexa-site`** repo.
3. Build settings — this is a plain static site, so **leave build command EMPTY** and set **Build output directory** to **`/`** (root). Framework preset: **None**.
4. **Save and Deploy.** Cloudflare builds it and gives you a `outbexa-site.pages.dev` URL. Open it, confirm the film + effects play.

## Step 4 — Move outbexa.com to the Pages project (2 min)

1. First, on the **old `outbexa` Worker** → Domains → remove the `outbexa.com` custom domain (so it's free to reassign).
2. On the new **`outbexa-site` Pages** project → **Custom domains** → **Set up a custom domain** → `outbexa.com` → confirm. Add `www.outbexa.com` too.
3. Cloudflare re-points DNS automatically (it already runs your DNS). HTTPS re-issues in a minute.

That's it — outbexa.com now serves from GitHub.

---

## From now on

When I make a change, I hand you the updated file(s). You do a 20-second update:
- GitHub repo → click the file (e.g. `index.html`) → pencil **Edit** icon → paste the new content → **Commit changes**.
- Or **Add file → Upload files** → drag the new version → Commit.

Cloudflare sees the commit and **auto-rebuilds outbexa.com within ~30 seconds.** No dragging folders, no dashboard uploads.

> Even better: if you ever connect a GitHub MCP to me, I can commit directly and you'd do nothing at all. For now, the copy-paste-commit above is the whole workflow.

---

## Quick reference — what each file does
- **index.html** — the entire landing page (film, copy, everything).
- **checkout.html** — the branded Stripe checkout page.
- **sitemap.xml / robots.txt** — SEO; submit sitemap in Google Search Console once live.
- **_headers** — tells Cloudflare to always serve the freshest HTML (so updates show immediately, no stale cache).
