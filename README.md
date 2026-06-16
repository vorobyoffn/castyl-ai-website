# Castyl — castyl.ai website

The live marketing site for **Castyl** — "Your AI workforce, done for you."
A self-contained static site (no build step). This repo is ready to push to GitHub
and deploy to any static host, then pointed at **castyl.ai**.

```
index.html        ← the entire site (HTML + CSS + JS, zero dependencies)
brand.html        ← logo & color sheet
404.html          ← branded not-found page
assets/           ← logo SVGs + og-image.png (social share card)
CNAME             ← custom domain for GitHub Pages (castyl.ai)
robots.txt        ← SEO
sitemap.xml       ← SEO
netlify.toml      ← Netlify config (no build)
vercel.json       ← Vercel config (no build)
```

## Preview locally
No build needed — just open `index.html`, or serve the folder:
```bash
python3 -m http.server 4599
# then visit http://localhost:4599
```

---

## Step 1 — Put it on GitHub

**Option A · GitHub CLI** (fastest)
```bash
cd castyl-ai-website
gh auth login                 # sign in to your GitHub
gh repo create castyl-ai-website --public --source=. --remote=origin --push
```

**Option B · Git + github.com**
1. Create a new empty repo on github.com (e.g. `castyl-ai-website`).
2. Then:
```bash
cd castyl-ai-website
git remote add origin https://github.com/<your-username>/castyl-ai-website.git
git branch -M main
git push -u origin main
```

**Option C · No terminal** — on github.com create a repo → "uploading an existing file"
→ drag in everything from this folder → Commit.

> This folder is already a git repo with an initial commit, so Options A/B work immediately.

---

## Step 2 — Deploy (pick one)

### 🟢 Vercel — easiest, recommended
1. [vercel.com](https://vercel.com) → **Add New → Project** → import the GitHub repo.
2. Framework preset: **Other** · Build command: *(none)* · Output dir: `./`. Deploy.
3. You get a live `*.vercel.app` URL in ~20s.

### 🟢 Netlify — also great
1. [app.netlify.com](https://app.netlify.com) → **Add new site → Import an existing project** → pick the repo.
2. Build command: *(empty)* · Publish directory: `.`. Deploy.

### 🟢 GitHub Pages — free, no extra account
1. Repo → **Settings → Pages** → Source: **Deploy from a branch** → `main` / `/ (root)` → Save.
2. The included `CNAME` sets the custom domain to **castyl.ai** automatically.
3. Tick **Enforce HTTPS** once the domain verifies.

### 🟣 Lovable — if you want to keep editing it with AI
1. In Lovable, create/open a project and **connect GitHub** → select this repo
   (Lovable ↔ GitHub two-way sync).
2. Edit visually in Lovable; changes sync back to GitHub and redeploy.
3. Custom domain (castyl.ai) is set in Lovable's project settings on a paid plan.
> Note: Lovable is built around Vite/React projects. This is a hand-built static
> site, so it imports and hosts fine, but Lovable's component editing works best on
> its own React scaffolding — Vercel/Netlify/Pages are the simplest path to "just live."

---

## Step 3 — Point **castyl.ai** at it

In your domain registrar's DNS settings, add the records for the host you chose:

**Vercel**
| Type | Name | Value |
|------|------|-------|
| A | `@` | `76.76.21.21` |
| CNAME | `www` | `cname.vercel-dns.com` |
(then add `castyl.ai` under the project's **Domains** tab)

**Netlify**
| Type | Name | Value |
|------|------|-------|
| A | `@` | `75.2.60.5` |
| CNAME | `www` | `<your-site>.netlify.app` |
(or use Netlify DNS / an `ALIAS` of `apex-loadbalancer.netlify.com`)

**GitHub Pages**
| Type | Name | Value |
|------|------|-------|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `<your-username>.github.io` |

DNS can take 10 min–24 h to propagate. After it resolves, enable HTTPS in your host
(automatic on Vercel/Netlify; one checkbox on GitHub Pages).

---

## Notes
- The "Book a call" buttons point to `https://calendly.com/idan-castyl/30min`.
- To edit copy, colors, or the demo: everything is inline in `index.html`
  (CSS variables live in the `:root { … }` block near the top).
- `og-image.png` is the 1200×630 social preview shown when the link is shared.
