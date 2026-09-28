# Iranshahr · ایرانشهر

An animated 3D atlas of five thousand years of Iranian history, from Elam (c. 3200 BC) to the Islamic Republic. Territories grow, shrink and change hands on a 3D relief map while the timeline plays through battles, cities, monuments and roads, with optional narration and music.

**Live demo:** <https://mhdvi.github.io/iranshahr/>

## Features

- **Fourteen chapters:** Elam, the Medes, the Achaemenids, Alexander and the Seleucids, the Parthians, the Sasanians, the Caliphs and the Iranian Intermezzo, the Seljuks, the Mongols, Ilkhans and Timurids, the Safavids, the Afsharids and Zands, the Qajars, the Pahlavis, and the Islamic Republic.
- **Historical territories:** 197 dated frames and 1,056 territory entries combine Cliopatria v0.2.0 with cited historical corrections and regional reconstructions. Every scheduled territory has visible geometry; generalized regional cores and cultural regions are distinguished in the evidence. See the [full audit](docs/territory-audit.md), [interactive source report](territory-sources.html), [regional repairs](docs/regional-territories.md), and visual camera comparison (generated locally in docs/map-review.html).
- **3D map:** relief, rivers and lakes (including the pre-1960 Aral Sea), with capitals, events and neighbouring powers labelled.
- **Monuments:** 3D models of sites such as the Behistun inscription.
- **Narration and music:** spoken narration with a generative score in the Persian modes. The music quiets while the narrator speaks.
- **English and Persian:** full Persian translation with a right-to-left layout, Persian digits and dates, and pre-recorded Persian narration.

## Controls

| Action | Input |
| --- | --- |
| Full territory overview | Expand-corners button beside the language control |
| Play / pause | <kbd>Space</kbd> or the play button |
| Previous / next moment | <kbd>←</kbd> / <kbd>→</kbd> |
| Jump anywhere in time | Click or drag the timeline |
| Show / hide the side panel | <kbd>P</kbd> |
| Show / hide the map key | <kbd>K</kbd> |
| Rotate / zoom the map | Drag / scroll |
| Switch language | EN / فا button in the dock |

## Running locally

Everything is static: one HTML file plus the Persian audio clips. Libraries (three.js, polygon-clipping) and fonts load from CDNs, so you need an internet connection.

You can open `index.html` directly in a browser. A local server behaves more like GitHub Pages, though:

```sh
# any static server works, for example:
python -m http.server 8000
# or
npx serve .
```

Then open <http://localhost:8000/>.

## Deploying to GitHub Pages

The repository is ready for GitHub Pages as it is. `index.html` is the app itself, and `.nojekyll` tells Pages to serve the files as they are, without a Jekyll build.

1. Push the repository to GitHub, including the `audio/` folder.
2. On GitHub, open **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
4. Choose the `main` branch and the `/ (root)` folder, then click **Save**.
5. After a minute or two the site is live at <https://mhdvi.github.io/iranshahr/>.

Each push to `main` redeploys the site.

## Project structure

```
index.html         the whole app: map data, chapters, rendering, audio and UI
audio/fa/          Persian narration clips (MP3), named by a hash of the spoken text
audio/fa/index.js  list of the available clips
.nojekyll          serves the files as they are on GitHub Pages
```

## Browser support

The app needs a recent desktop or mobile browser with WebGL. English narration uses the browser's Web Speech API, so the voice depends on your system. Persian narration plays the recorded clips and falls back to a system Persian voice where a clip is missing.

## Credits

- Historical polygons: [Cliopatria v0.2.0](https://doi.org/10.5281/zenodo.20274630), Bennett et al., [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Modified by clipping, coordinate rounding, regrouping and explicitly documented historical corrections; see `data/territory-provenance.json`.
- Base geography: [Natural Earth](https://www.naturalearthdata.com/) (public domain)
- 3D rendering: [three.js](https://threejs.org/)
- Polygon operations: [polygon-clipping](https://github.com/mfogel/polygon-clipping)
- Fonts: Marcellus, Alegreya Sans, IBM Plex Mono and Vazirmatn, from Google Fonts

## Rebuilding historical territories

Run `npm ci`, then `npm run build:territories`. The bundled `data/historical-source.geojson` subset supports offline rebuilding; the timeline, name mappings, provenance and complete audit are in `data/`. The generated app needs no build step to serve.

Run `npm test` for geometry, chronology and narration checks. Run `npm run test:browser` with Chrome installed (or set `CHROME` to its executable); browser checks need internet for CDN dependencies.

The [cross-era review](docs/era-coverage.md) documents the wider Eurasian map and additional event-date corrections. `data/map-view.json` supplies shared land/territory bounds. The bundled public-domain Natural Earth land subset supports offline rebuilding.
