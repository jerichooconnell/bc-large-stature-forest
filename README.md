# BC Large-Stature Old Growth

Interactive map of remaining large-stature old-growth forest in British
Columbia's Coastal Western Hemlock (CWH), Coastal Douglas-fir (CDF), and
Interior Cedar-Hemlock (ICH) biogeoclimatic zones — the old growth on the
highest-site-index (best growing capacity) ground. (Interior Douglas-fir
was considered but excluded — its stands are not typically large-stature.)

**Live map:** https://jerichooconnell.github.io/bc-large-stature-forest/

## What it shows

- **Large-stature old growth (current)** — individual VRI stand polygons
  with projected age > 150 yr and `SITE_INDEX` at or above the 75th
  percentile for their BEC zone. Each stand keeps its own exact site index
  and is shaded by percentile tier within its zone — top 25% (≥75th),
  top 15% (≥85th), or top 5% (≥95th) — darker meaning a higher site index
  relative to other stands in the same zone. Click any patch for its exact
  value, age, and area.
- **Historical extent** — the same 75th-percentile-floor land base,
  including stands now logged/regenerating (toggleable, lazy-loaded — it's
  a large province-wide layer; shown as a coarse dissolved background, not
  per-stand).
- **Protected areas** — provincial parks, ecological reserves, conservancies,
  and national parks (BC Data Catalogue).
- **Historical fire perimeters** — BC wildfire history layer.
- **Basemap toggle** — satellite imagery (Esri) or OpenStreetMap street map.
- **Statistics** — current extent vs. a historical baseline (current old
  growth + stands on equivalently high-site ground with an explicit harvest
  record), and the share of current old growth inside protected areas.

## Performance

The current-old-growth layer is ~14,000 individual VRI stand polygons and
the historical layer is a large dissolved province-wide background — both
kept fast with:

- **Overview/detail split** — only patches ≥20ha (`data/current_overview.geojson`,
  ~4MB) load on first paint. Patches down to the 75th-percentile floor
  (`data/current_detail.geojson`, ~10MB) fetch lazily the first time you
  zoom in past level 9. The historical layer (~30MB) only fetches at all
  once you toggle it on.
- **Zoom-dependent thinning** — even after data is loaded, only patches above
  a per-zoom-level area threshold are drawn (smaller patches reveal as you
  zoom in), and all vector layers render on `<canvas>` rather than SVG.

## Data sources

- BC Vegetation Resources Inventory (`VEG_COMP_LYR_R1_POLY`, province-wide)
- BC Data Catalogue protected-lands layers (`TA_PARK_ECORES_PA_SVW`,
  `TA_CONSERVANCY_AREAS_SVW`, `CLAB_NATIONAL_PARKS`)
- BC historical fire perimeters (`PROT_HISTORICAL_FIRE_POLYS_SP`)

Derived from the [yew_project](https://github.com/jerichooconnell/yew_project)
geospatial pipeline. Basemap imagery © Esri, Maxar, Earthstar Geographics.

## Methodology notes

The historical baseline intentionally excludes naturally young, never-logged
stands (identified via VRI `HARVEST_DATE` / opening indicators) so that
natural disturbance history (fire, blowdown) isn't counted as anthropogenic
loss — only the current-old-growth total plus explicitly logged/regenerating
stands on equivalent site quality are included as "historical."

## Running locally

This is a static site — no build step. Serve the directory with any static
file server, e.g.:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`.
