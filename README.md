# World Map — Economic & Demographic Explorer

An interactive world map: hover or tap any country to see its economy, markets, and
society at a glance — GDP, income, growth, inflation, markets, debt, population,
energy, and more — each shown against a **World / regional / income-group benchmark**
and with a trend line back to the 1960s.

**Live demo:** _(GitHub Pages URL will appear here once Pages is enabled — see below)_

## What it does

- **22 live indicators** from the World Bank, grouped (Economic, Markets & finance,
  Demographic & social, Energy & environment), selectable to recolour the map.
- **Click/tap a country** for a full snapshot: capital, every available indicator with
  its source code, GDP composition (by sector and by demand), age structure, and — for
  the US — a party-coloured head-of-state timeline.
- **Benchmarks:** each metric shows the country's percentile and how it compares to the
  population-weighted average, switchable between the whole World, the country's region,
  and its World Bank income group. Trends show that benchmark through time.
- **Currency & year controls:** convert money metrics to 160+ currencies at live rates,
  and step back through past years.
- Works on desktop and mobile (touch scrubbing on trends, pinch-zoom on the map).

## How it works

A single self-contained `index.html`. All data is fetched **client-side** at runtime:

- Indicators: World Bank Open Data API (`api.worldbank.org`)
- Exchange rates: open.er-api.com
- Region / income-group metadata: World Bank country API
- Map shapes: Natural Earth via `world-atlas`; rendering with D3 + TopoJSON (CDN)

There is **no backend and no build step** — it runs anywhere static files are served.

## Fast loading — the data snapshot

By default the app fetches ~45 live endpoints per visit, which is slow and can hit
World Bank rate limits. To make it load instantly and scale to traffic, it will use a
pre-built `snapshot.json` (every metric's latest value + region/income metadata in one
file) if that file sits next to `index.html`. If the snapshot is absent, it falls back
to live fetching automatically.

To (re)build the snapshot — do this whenever you want to refresh the numbers:

1. Make sure `index.html` and `build-snapshot.html` are pushed and live.
2. Open `https://<your-username>.github.io/world-map/build-snapshot.html` and click
   **Build snapshot.json** (takes ~1 minute; keep the tab focused). It downloads `snapshot.json`.
3. Move `snapshot.json` into this folder (next to `index.html`), then `git add -A`,
   `git commit -m "refresh snapshot"`, `git push`.

The map + all tiles then load from that one static file (served off GitHub's CDN);
trend lines still load live in the background. Re-run monthly or whenever you want fresh data.

## Run locally

Just open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000   # then visit http://localhost:8000
```

## Deploy on GitHub Pages

1. Create a new GitHub repo and push this folder (see commands below).
2. In the repo: **Settings → Pages → Build and deployment → Source: Deploy from a branch**,
   branch **main**, folder **/ (root)**, then **Save**.
3. Your site goes live at `https://<your-username>.github.io/<repo-name>/` within a minute.

## Data sources

World Bank Open Data is CC BY 4.0. Natural Earth is public domain. This is an independent
project and is not affiliated with or endorsed by the World Bank.

## License

© 2026 JK. All rights reserved. This code is published for demonstration only; it may not be
copied, modified, redistributed, or used commercially without permission.
