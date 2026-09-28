# Portfolio — Manthan Rajesh Patil

Fresh rebuild of the personal portfolio (previously at `manthanpatil.surge.sh`).
Dark cinematic single-page site. Vanilla HTML + CSS + JS. **Zero external
requests** — no CDNs, no fonts, no trackers — so it loads fast and cannot break
because a third party went down.

## Structure

```
portfolio/
├── index.html          # All content (semantic, accessible markup)
├── css/styles.css      # Theme, layout, responsive breakpoints (960px / 640px)
├── js/main.js          # Mobile nav, scroll reveal, active-link spy, footer year
├── assets/portrait.webp# Profile photo (700px, 42 KB)
├── resume.pdf          # Resume file behind the "Download Resume" buttons
└── README.md           # This file
```

## Updating content

- **Text:** edit `index.html` directly — sections are commented (`HERO`, `ABOUT`, …).
- **Styling:** design tokens (colors, fonts, spacing) live in `:root` at the top of
  `css/styles.css`. Change once, apply everywhere.
- **Photo:** replace `assets/portrait.webp` (keep it under ~200 KB; WebP or JPG).
- **Resume:** replace `resume.pdf` with the latest CV (keep the filename).
- **Behavior:** `js/main.js` is commented per feature; no build step, no bundler.

## Preview locally

```bash
cd portfolio
python3 -m http.server 8000
# open http://localhost:8000
```

## Deploy

### Option A — GitHub Pages (recommended: free, stable, professional URL)

```bash
cd portfolio
git init && git add -A && git commit -m "Portfolio"
gh repo create portfolio --public --source=. --push
gh api -X POST /repos/<your-username>/portfolio/pages \
  -f source[branch]=main -f source[path]=/
# Live in ~1–2 min at: https://<your-username>.github.io/portfolio/
```

To update later: edit files, `git add -A && git commit -m "update" && git push`.

### Option B — Netlify (no terminal needed)

1. Go to https://app.netlify.com/drop (free account)
2. Drag the entire `portfolio` folder onto the page
3. You get a live URL instantly; rename the site under Site settings

### Option C — Vercel

```bash
cd portfolio
npx -y vercel --prod
# follow the prompts; live URL printed at the end
```

## Why the old site went down

`manthanpatil.surge.sh` returned **HTTP 503 "No server is available to handle
this request"** on every path, and `surge.sh` itself was unreachable (empty
reply) — a **platform-side Surge outage/failure**, not a DNS or file problem.
DNS resolved fine and the deployed files were intact in the local backup. The
fix is hosting the same content on infrastructure with real uptime guarantees,
which is what this rebuild targets.
