# ChronoAtlas — deploy

This folder contains a single, self-contained `index.html` ready to drop onto any static host.
No build step. No backend. No API keys. Open it in a browser and it works.

Current version inside: **v1.21** (26 snapshots 3000 BCE → 2026 CE; 285 historical fact packs + 176 modern countries; stateless-peoples, trade-route and capital-city overlays; quiz mode with Level 0 (name + capital) and Level 1 (full chain); side-by-side compare mode; mobile-tuned UI).

---

## Deploy in 60 seconds — Netlify Drop (no signup, free)

The fastest path. Gives you a live URL you can open on your phone immediately.

1. Open <https://app.netlify.com/drop> in a browser on your laptop.
2. Drag this `deploy` folder onto the page.
3. Netlify uploads it (takes a few seconds) and gives you a URL like `https://amazing-curie-12345.netlify.app`. Open it on your phone.
4. (Optional) Sign in to claim the site and get a stable URL like `https://chronoatlas-karthik.netlify.app`. Then every future "deploy" is another drag-and-drop on the same site.

Drop-zone trade-offs: URLs auto-expire after a few hours if you don't claim them. Sign in (GitHub / Google / email) to make the site permanent.

---

## Deploy as a project you can iterate — GitHub Pages (10 min setup, free, version-controlled)

This is the better long-term answer. Every iteration becomes a `git push`; the live site updates automatically. Your phone always has the latest.

1. Create a new GitHub repo named `chronoatlas` (private or public — Pages works on both).
2. On your laptop:
   ```bash
   cd "<your History Atlas folder>/deploy"
   git init
   git add index.html README.md
   git commit -m "Initial commit — ChronoAtlas v1.10"
   git branch -M main
   git remote add origin https://github.com/<YOUR-USERNAME>/chronoatlas.git
   git push -u origin main
   ```
3. In the GitHub repo → **Settings → Pages** → "Build and deployment" source: **Deploy from a branch**, branch: `main`, folder: `/ (root)`. Click Save.
4. Wait ~1 minute. Your site is live at `https://<YOUR-USERNAME>.github.io/chronoatlas/`. Open it on your phone.
5. To ship a new version later:
   ```bash
   cp "<your History Atlas folder>/index_v3.html" "<your History Atlas folder>/deploy/index.html"
   cd "<your History Atlas folder>/deploy"
   git add index.html
   git commit -m "v1.11 — <one-line note about what changed>"
   git push
   ```
   GitHub Pages rebuilds in ~30s. Refresh on your phone.

---

## Optional: keep older versions accessible

If you want to be able to load *any past version* alongside the current one (useful for comparing
iterations), commit each release as its own file:

```
deploy/
├── index.html        # always points to the latest
├── v1.10/index.html  # snapshot of v1.10
├── v1.9/index.html
└── ...
```

URLs: `your-site/`, `your-site/v1.10/`, `your-site/v1.9/`, etc.

I can wire this up if you want — just say the word.

---

## Mobile UX

Tuned in v1.21: compact one-row topbar, quiz/info panels open as a bottom sheet with the map
still visible, 44px play button and a larger slider thumb, legend and overlay toggles start
collapsed (tap their headers to expand), and compare mode stacks the two maps vertically.
Pinch-zoom works via Leaflet. If anything still feels broken on your phone, send a screenshot
and we'll polish it in a follow-up iteration.

---

## What's inside `index.html`

- Leaflet 1.9.4 + CartoDB Voyager tiles (loaded from CDN)
- Google Fonts: Source Serif 4 + DM Sans (loaded from CDN)
- 26 historical snapshots, 285 historical fact packs, 176 modern countries — all inline as JS constants
- 12 stateless peoples (hatched overlay) + 8 historical trade routes (dashed polylines) + capital city stars, all toggleable top-right
- Quiz mode with two levels — L0: country + capital; L1: full chain (capital, currency, religion, top-3 languages) — session-only progress tracking per snapshot
- Compare eras: two synced maps side by side, any two snapshots
- Single file, ~865 KB. Loads in seconds even on a slow phone connection.

Attribution to OpenStreetMap and CARTO is shown in the bottom-right corner of the map (required by the CC BY 3.0 / ODbL licensing of the basemap tiles).

---

## Files in the parent folder

- `<your History Atlas folder>/index_v3.html` — the active build (same content as `deploy/index.html`; kept under its versioned name for the development workflow)
- `<your History Atlas folder>/PROJECT_LOG.md` — full iteration history, data source registry, decisions
- `<your History Atlas folder>/index.html` — original Phase 1 prototype (preserved)
- `<your History Atlas folder>/index_v2.html` — end of Batch 1 (preserved)
