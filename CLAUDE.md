# CLAUDE.md — Attractors (GJ Customized Version)

## What this project is

A fork of Nicky Case's [An Interactive Introduction to Attractor Landscapes](https://ncase.me/attractors/) (MIT licensed, originally May 2018). The GJ version replaces the fish/population metaphor with a Fear/Desire/Doing attractor model using Buddha images, muted audio, and a single full-sim embed (mode=4).

**GitHub:** `https://github.com/gtjamieson/attractors`
**GCS bucket:** `gs://enakr8ia_habitat` (source files under `source_files/attractors-master/`)
**Local:** `/Users/enkr8ia/Library/Mobile Documents/com~apple~CloudDocs/Claude agent/attractors-master/`

---

## Key customizations vs the Nicky Case original

| File | Customization |
|------|--------------|
| `sim/Attractors.js:447` | Button label changed to `"Doing"` |
| `sim/Attractors.js:897` | Under-button label changed to `"Fear"` |
| `sim/Attractors.js:902` | Over-button label changed to `"Desire"` |
| `sim/Attractors.js:1025-1026` | `water1`/`water2` images point to `laughingBuddha.png` / `surprisedBuddha.png` |
| `sim/sim.html` | Howler globally muted (`Howler.mute(true)`) after load |
| `sim/sim.html` | `Attractors.js` script tag has `?v=11` for cache busting |
| `index.html` | Only mode=4 iframe active (full sim); modes 1–3 commented out |

---

## GCS URL problem (Phase 2 work remaining)

All asset references in the code currently point to GCS instead of relative paths. This makes the repo not self-contained — it depends on GCS staying live.

**27 occurrences across 3 files:**
- `index.html` — 6 occurrences
- `sim/sim.html` — 8 occurrences
- `sim/Attractors.js` — 13 occurrences

**Phase 2 task:** Replace all `https://storage.googleapis.com/enakr8ia_habitat/source_files/attractors-master/` with relative paths (e.g. `./`, `../`).

---

## Known issue: sound file case mismatch

`sim/Attractors.js` references `d'oh.mp3` but the actual file is `sim/sounds/Doh.mp3`. This will silently fail on case-sensitive filesystems. Resolve in Phase 2.

---

## Hosting (decision pending)

Options under consideration for Phase 2:
- **GitHub Pages** — `gtjamieson.github.io/attractors` (simplest, free, no build step)
- Netlify / Vercel / Cloudflare Pages

Once a new host is live and verified, decide whether to decommission GCS assets.

---

## GCS / gcloud tooling

The old SDK at `~/Documents/Google-cloud/google-cloud-sdk/` (v258, 2019) is broken on Python 3.9+ — do not use it.

Use the Homebrew-installed SDK (v557+):

```bash
# List bucket
CLOUDSDK_PYTHON=/usr/local/bin/python3.13 gsutil ls gs://enakr8ia_habitat/

# Copy files from GCS
CLOUDSDK_PYTHON=/usr/local/bin/python3.13 gsutil cp gs://enakr8ia_habitat/source_files/attractors-master/sim/img/<file> sim/img/
```

Auth: `gcloud auth login` (uses Homebrew gcloud at `/usr/local/bin/gcloud`)

---

## Project structure

```
attractors-master/
├── index.html          # Main article page (mode=4 only, other modes commented out)
├── index.css           # Article styles
├── index.js            # Article JS
├── sim/
│   ├── sim.html        # Simulation shell (Howler muted globally)
│   ├── sim.css
│   ├── Attractors.js   # Core sim logic — Fear/Desire/Doing labels, Buddha images
│   ├── Mouse.js
│   ├── helpers.js
│   ├── howler.min.js
│   ├── img/            # All 8 images including the 3 GJ custom ones
│   │   ├── laughingBuddha.png
│   │   ├── surprisedBuddha.png
│   │   ├── sim_wave.png
│   │   └── fish.png, water1.png, water2.png, ui_click.png, ui_slide.png
│   ├── sounds/         # MP3s + applause_sim.m4a
│   └── splash/
├── icons/              # Landscape/ball/mountain/valley/slopes/speed icons
├── img/                # Article images (epigenetics, neuroscience, peace, polisci)
├── social/             # thumbnail.png
└── de.html, es.html, es2.html, fr.html  # Translation stubs
```

---

## Deployment procedure (local → GitHub → GCS)

For any change to sim files, follow this sequence:

### 1. Edit locally
Make changes in:
`/Users/enkr8ia/Library/Mobile Documents/com~apple~CloudDocs/Claude agent/attractors-master/`

### 2. Backup current production file on GCS (before overwriting)
```bash
CLOUDSDK_PYTHON=/usr/local/bin/python3.13 gsutil cp \
  gs://enakr8ia_habitat/source_files/attractors-master/sim/<file> \
  gs://enakr8ia_habitat/source_files/attractors-master/sim/<file>.bak
```

### 3. Commit & push to GitHub
```bash
git add <file>
git commit -m "description"
git push
```

### 4. Copy updated file to GCS (goes live immediately)
```bash
CLOUDSDK_PYTHON=/usr/local/bin/python3.13 gsutil cp \
  "/Users/enkr8ia/Library/Mobile Documents/com~apple~CloudDocs/Claude agent/attractors-master/sim/<file>" \
  gs://enakr8ia_habitat/source_files/attractors-master/sim/<file>
```

### 5. Restore public access (gsutil cp strips ACL — must do this every time)
```bash
CLOUDSDK_PYTHON=/usr/local/bin/python3.13 gsutil acl ch -u AllUsers:R \
  gs://enakr8ia_habitat/source_files/attractors-master/sim/<file>
```

### Rollback
```bash
CLOUDSDK_PYTHON=/usr/local/bin/python3.13 gsutil cp \
  gs://enakr8ia_habitat/source_files/attractors-master/sim/<file>.bak \
  gs://enakr8ia_habitat/source_files/attractors-master/sim/<file>
```

---

## Responsive scaling — URL parameter

The sim supports responsive scaling via a URL parameter. This allows the HTML5 web app to opt in while native iOS/Android apps remain unaffected until new store versions are ready.

| Platform | iframe URL | Scaling |
|----------|-----------|---------|
| HTML5 web app | `...sim.html?mode=4&responsive=1` | Active — fit-to-screen scaling |
| Native iOS | `...sim.html?mode=4` | Inactive — renders at native 400px, no change |
| Native Android | `...sim.html?mode=4` | Inactive — renders at native 400px, no change |

**Works for all modes** (0–6). Width is always 400px; height is read dynamically per mode (340/380/340/400/600/380/400px).

**To enable for native apps:** add `&responsive=1` to the iframe URL in the Appery.io native build and deploy new store versions.

### How it works

Scale is calculated as `Math.min(innerWidth/400, gjAvailH/canvasHeight)` — the sim fills available width or height, whichever is the tighter constraint. This ensures the full sim is always visible without scrolling on any device or orientation.

**Verified results:**

| Device | Orientation | Result |
|--------|------------|--------|
| iPhone | Portrait | Full width, perfect fit |
| iPad | Portrait | Full width, perfect fit |
| iPad | Landscape | Full height, grey space to right (correct — height is constraining dimension) |

### Touch coordinate fix

CSS `transform: scale()` changes visual size but does not remap touch event coordinates. `gjFixTouchCoords()` adds capture-phase touch listeners that intercept events before `Mouse.js`, correct coordinates using `getBoundingClientRect() / gjScale`, then call `Mouse.ondown`/`Mouse.onmove` directly. Without this, buttons and sliders are unresponsive at any scale other than 1.0.

### Bidirectional postMessage

**App → Sim:** parent page sends available height on load and on every resize/rotation:
```javascript
function gjSendAvailHeight() {
  var iframe = document.querySelector('iframe');
  if (iframe && iframe.contentWindow) {
    var header = document.querySelector('ion-header') as HTMLElement;
    var headerH = header ? header.offsetHeight : 60;
    iframe.contentWindow.postMessage({
      type: 'gjAvailHeight',
      availH: window.innerHeight - headerH - 20  // -20 safety buffer for ion-content padding
    }, '*');
  }
}
setTimeout(gjSendAvailHeight, 800);   // delay allows iframe to initialise
window.addEventListener('resize', gjSendAvailHeight);
```

**Sim → App:** after each scale, sim reports its actual rendered height so the iframe resizes to fit:
```javascript
window.parent.postMessage({ type: 'gjSimHeight', height: scaledHeight }, '*');
```

**App listens:**
```javascript
window.addEventListener('message', function(e) {
  if (e.data && e.data.type === 'gjSimHeight') {
    var iframe = document.querySelector('iframe');
    if (iframe) { iframe.style.height = e.data.height + 'px'; }
  }
});
```

**Placement in Appery.io:** `ngOnInit` (fires once on component creation). Do not use `ionViewWillEnter` — it fires on every navigation and causes duplicate listeners.

### iframe setup in Appery.io
```html
<iframe src="...sim.html?mode=4&responsive=1" width="100%" height="600"></iframe>
```
The `height="600"` is the initial value only — it is overridden dynamically by the `gjSimHeight` postMessage.

---

## Custom sim modes

| Mode | Canvas H | Components | Notes |
|------|----------|-----------|-------|
| 0 | 340px | PopulationSlider (NO_GROWTH), fish, less/moreButton | Population locked, hint visible |
| 1 | 380px | PopulationSlider (SHOW_LABELS), fish, less/moreButton | Standard interactive |
| 2 | 340px | PopulationSlider (SHOW_LABELS), hill | Mouse offset (0,-200) |
| 3 | 400px | PopulationSlider, hill, HillShaper | Mouse offset (0,-200); HillShaper hints visible |
| 4 | 600px | PopulationSlider (SHOW_LABELS), fish, less/moreButton, hill, HillShaper | Full sim |
| 5 | 380px | PopulationSlider (SHOW_LABELS), fish, less/moreButton | Mode 1 minus threshold lines, velocity arrow, direction arrows in slider |
| 6 | 400px | PopulationSlider (SHOW_LABELS), hill | Mouse offset (0,-200); no HillShaper; auto-animation: thresholdUnder 200→350 after 500ms |

### Mode 6 auto-animation detail
`gjMode6Animating` starts false, set true after 500ms delay. Each frame: `thresholdUnder += (350 - thresholdUnder) * 0.012`. Stops and locks at 350. Hill recalculates each frame so landscape shifts organically.

---

## Cache-busting protocol

`sim/sim.html` loads `Attractors.js` with a `?v=N` query string to bust browser cache:
```html
<script src="https://storage.googleapis.com/...sim/Attractors.js?v=11"></script>
```

**Whenever Attractors.js changes, bump the version in BOTH places:**
1. `sim/sim.html` — the `?v=N` on the script tag
2. TEM_lite iframe src — the `?v=N` on the `sim.html` URL

Both must move together and use the same number. Current version: **v=11**.

**Production risk from adding `?v=N` to Attractors.js: none.** GCS ignores query strings on static file requests — `Attractors.js?v=11` serves identical content to `Attractors.js`. Existing apps without a `?v=N` on their `sim.html` URL are unaffected: users with a cached `sim.html` stay on the old version (same behaviour as before), and new users loading `sim.html` fresh get the correct updated file. Verified Feb 2026 against TEM_lite and TEM_sim (modes 0–4 unaffected; Mode 5/6 code fully gated by `SIM_MODE` checks).

---

## GJ Changes log

| Date | File | Change |
|------|------|--------|
| Feb 2026 | `sim/sim.html` | Viewport: `width=640` → `width=device-width, initial-scale=1` |
| Feb 2026 | `sim/sim.html` | Added `gjScaleCanvas()` — fit-to-screen scaling via CSS transform, gated behind `?responsive=1` |
| Feb 2026 | `sim/sim.html` | Added `gjFixTouchCoords()` — fixes touch coordinate mapping broken by CSS transform |
| Feb 2026 | `sim/sim.html` | Bidirectional postMessage: sim reports scaled height to app; app sends available height on load and rotation |
| Feb 2026 | `sim/Attractors.js` | Added Mode 5 — Mode 1 without threshold lines, velocity arrow, direction arrows |
| Feb 2026 | `sim/Attractors.js` | Added Mode 6 — Mode 3 without HillShaper; auto-animation thresholdUnder 200→350 |
| Feb 2026 | `sim/sim.html` | Added `?v=11` to Attractors.js script tag for cache busting |

---

## History

- **Jan 2020:** GitHub repo created with original Nicky Case version (never updated)
- **~2020–2025:** GJ customizations made locally and deployed to GCS
- **Sep 2 2025:** Last modification to local files (identical to GCS)
- **Feb 2026:** Phase 1 complete — GitHub now holds the canonical GJ version, local and GCS are all in sync
- **Feb 2026:** Responsive scaling implemented — sim fits iPhone, iPad portrait and landscape correctly via bidirectional postMessage
- **Feb 2026:** Modes 5 and 6 added; cache-busting `?v=11` added to Attractors.js script tag in sim.html

---

## TEM_sim — Retired Feb 2026

TEM_sim was an Ionic/Angular app wrapping the attractor sim with explanatory pages. It has been retired — TEM_lite is now the sole app. The attractors sim is embedded directly within TEM_lite's Patterns (mode 1) and Encounter (mode 3) pages.

Repo `gtjamieson/tem_sim` is archived. No further development.

See `TEM_lite/STRATEGY.md` for the architecture decision and rationale.

### Obsidian Vault Context (TEM Theory)

Source of truth for TEM theory — load with the Read tool only when relevant to the current task.

Base path: `/Users/enkr8ia/Documents/Obsidian Vault/Claude_agent/TEM_lite/Context/`

| File | When to load |
|------|-------------|
| `The Enlightenment Method (TEM) - A Dantean Blueprint for modern transformation.md` | TEM theory, Virgil/Beatrice framework, journey structure |
| `A modern map for inner transformation - Dantes ancient allegory ..md` | Pattern philosophy, ego/resistance framing, Hell taxonomy |
| `Curved nature of reality.md` | TEM cosmology, attractor/curve concepts, concave/convex model |
| `Dantes ancient journey of the soul reinterpreted - lifes metagame.md` | Journey stage design, passive→active participant arc |
| `Guides_ Human vs AI Catalysts.md` | Virgil/AI guide role, empty presence, LH/RH distinction |
| `Pattern Language.md` | Pattern formats, somatic design principles, Dantean circle mapping |
