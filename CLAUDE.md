# CLAUDE.md — Attractors (GJ Customized Version)

## What this project is

A fork of Nicky Case's [An Interactive Introduction to Attractor Landscapes](https://ncase.me/attractors/) (MIT licensed, originally May 2018). The GJ version replaces the fish/population metaphor with a Fear/Desire/Doing attractor model using Buddha images, muted audio, and a single full-sim embed (mode=4).

**GitHub:** `https://github.com/gtjamieson/attractors`
**GCS bucket:** `gs://enakr8ia_habitat` (source files under `source_files/attractors-master/`)
**Local:** `/Users/enkr8ia/Documents/GitHub/attractors-master/`

---

## Key customizations vs the Nicky Case original

| File | Customization |
|------|--------------|
| `sim/Attractors.js:447` | Button label changed to `"Doing"` |
| `sim/Attractors.js:897` | Under-button label changed to `"Fear"` |
| `sim/Attractors.js:902` | Over-button label changed to `"Desire"` |
| `sim/Attractors.js:1025-1026` | `water1`/`water2` images point to `laughingBuddha.png` / `surprisedBuddha.png` |
| `sim/sim.html` | Howler globally muted (`Howler.mute(true)`) after load |
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

## History

- **Jan 2020:** GitHub repo created with original Nicky Case version (never updated)
- **~2020–2025:** GJ customizations made locally and deployed to GCS
- **Sep 2 2025:** Last modification to local files (identical to GCS)
- **Feb 2026:** Phase 1 complete — GitHub now holds the canonical GJ version, local and GCS are all in sync
