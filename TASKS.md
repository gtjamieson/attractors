# TASKS.md — Attractors / TEM_sim outstanding work

---

## 1. Responsive scaling — roll out to remaining TEM_sim pages

**Repo:** `gtjamieson/TEM_sim`
**Status:** In progress — `DIY_enlightenment` done, 6 pages remaining

For each page: change iframe `width="400"` → `width="100%"`, add `&responsive=1` to src URL, add postMessage code to `ngOnInit` in the companion `.ts` file. See `CLAUDE.md` for the code patterns.

| Page | Mode | iframe height | Type | HTML | TS | Done |
|------|------|--------------|------|------|----|------|
| `Explainer` | 0 | 340 | Full page | [ ] | [ ] | [ ] |
| `New_Change` | 3 | 400 | Full page | [ ] | [ ] | [ ] |
| `Karma` | 1 | 380 | Modal | [ ] | [ ] | [ ] |
| `Samsara` | 2 | 340 | Modal | [ ] | [ ] | [ ] |
| `Attachment` | 0 | 340 | Modal | [ ] | [ ] | [ ] |
| `Cause_effect` | 0, 1, 2 | 340/380/340 | Full page — 3 iframes | [ ] | [ ] | [ ] |

**Notes:**
- `Cause_effect` has 3 iframes (one visible at a time). Use `querySelectorAll('iframe')` — see CLAUDE.md for the specific code pattern.
- Modal pages (`Karma`, `Samsara`, `Attachment`) — `window.innerHeight` reflects modal height, `ion-header` is the modal's own header. Same code pattern applies.
- After completing all pages, enable responsive scaling for native iOS/Android builds by adding `&responsive=1` to their iframe URLs and submitting new store versions.

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

## 5. Enable responsive scaling for native iOS/Android apps

**Status:** Blocked — waiting on items 1 and store submission process

Once all TEM_sim pages are updated and tested (item 1), submit new native builds to App Store and Google Play with `&responsive=1` added to all iframe src URLs.

---
