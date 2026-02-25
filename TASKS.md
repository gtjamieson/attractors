# TASKS.md — Attractors / TEM_sim outstanding work

---

## 1. Responsive scaling — roll out to remaining TEM_sim pages

**Repo:** `gtjamieson/TEM_sim`
**Status:** COMPLETE — all pages done (Feb 2026)

| Page | Type | Approach | Done |
|------|------|---------|------|
| `DIY_enlightenment` | Full page | `width="100%"`, `&responsive=1&v=6`, full postMessage in `ngOnInit` | ✅ |
| `Explainer` | Full page | `width="100%"`, `&responsive=1&v=1`, full postMessage in `ngOnInit` | ✅ |
| `New_Change` | Full page | `width="100%"`, `&responsive=1&v=1`, full postMessage in `ngOnInit` | ✅ |
| `Karma` | Modal | `width="400"`, `&v=1` only — no responsive (iPad modal viewport bug) | ✅ |
| `Samsara` | Modal | `width="400"`, `&v=1` only — no responsive (iPad modal viewport bug) | ✅ |
| `Attachment` | Modal | `width="400"`, `&v=1` only — no responsive (iPad modal viewport bug) | ✅ |
| `Cause_effect` | Full page | 3 hidden iframes deleted — no changes needed | ✅ |

**Key learnings:**
- Modal pages: do NOT use `&responsive=1`. On iPad, `window.innerWidth` inside an iframe in a modal card returns the full device width (~768px) rather than the iframe's rendered width, causing massive upscaling. Native `width="400"` fits iPad modal cards naturally.
- Full-page views: `&responsive=1` works correctly — iframe fills page width and `window.innerWidth` matches.

**Next step:** Enable responsive scaling for native iOS/Android builds — see item 6.

---

## 2. GCS URL replacement (Phase 2 — attractors repo)

**Repo:** `gtjamieson/attractors`
**Status:** Not started

All asset references in the sim still point to GCS hardcoded URLs instead of relative paths. Makes the repo not self-contained — depends on GCS staying live.

**27 occurrences across 3 files:**

| File | Occurrences |
|------|------------|
| `index.html` | 6 |
| `sim/sim.html` | 8 |
| `sim/Attractors.js` | 13 |

**Task:** Replace all instances of:
```
https://storage.googleapis.com/enakr8ia_habitat/source_files/attractors-master/
```
with relative paths (`./` or `../` as appropriate).

**Dependency:** Resolve hosting decision (item 3) first — relative paths only work once the sim is served from a proper host, not opened as a local file.

---

## 3. Hosting decision (Phase 2 — attractors repo)

**Status:** Decision pending

Options under consideration:

| Option | Notes |
|--------|-------|
| **GitHub Pages** | Simplest — `gtjamieson.github.io/attractors`, free, no build step, auto-deploys on push |
| **Netlify** | Free tier, custom domain support, easy setup |
| **Vercel** | Similar to Netlify |
| **Cloudflare Pages** | Similar to Netlify, global CDN |

**Recommendation:** GitHub Pages — zero config, already have the repo, no new accounts needed.

**Once hosting is live and verified:**
- Update all iframe src URLs in TEM_sim to point to the new host instead of GCS
- Decide whether to decommission GCS assets (keep as fallback until native app store updates are deployed)
- Update `CLAUDE.md` with new hosting details

---

## 4. Sound file case mismatch (Phase 2 — attractors repo)

**Status:** Not started — low priority

`sim/Attractors.js` references `d'oh.mp3` but the actual file is `sim/sounds/Doh.mp3`. Silently fails on case-sensitive filesystems (Linux-based hosts). Fix when GCS URL replacement (item 2) is done.

---

## 5. Create CLAUDE.md for TEM_sim repo

**Repo:** `gtjamieson/TEM_sim`
**Status:** Not started — low priority

No equivalent documentation exists for the TEM_sim app. A CLAUDE.md would capture:
- Appery.io architecture overview
- Page inventory (component name → screen title mapping)
- postMessage pattern for responsive scaling
- Build and deployment process for HTML5 / iOS / Android

---

## 6. Enable responsive scaling for native iOS/Android apps

**Status:** Blocked — waiting on items 1 and store submission process

Once all TEM_sim pages are updated and tested (item 1), submit new native builds to App Store and Google Play with `&responsive=1` added to all iframe src URLs.

---
