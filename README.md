# BC Large-Stature Old Growth

Interactive map of remaining large-stature old-growth forest in British
Columbia's Coastal Western Hemlock (CWH), Coastal Douglas-fir (CDF), and
Interior Douglas-fir (IDF) biogeoclimatic zones — the old growth on the
highest-site-index (best growing capacity) ground.

**Live map:** GitHub Pages (see repo settings for the URL once enabled).

## What it shows

- **Large-stature old growth** — VRI polygons with projected age > 150 yr
  and `SITE_INDEX` at or above the 75th percentile for their BEC zone
  (CWH ≥ 23.8 m, CDF ≥ 30.1 m, IDF ≥ 16.3 m @ 50 yr breast-height age).
- **Protected areas** — provincial parks, ecological reserves, conservancies,
  and national parks (BC Data Catalogue).
- **Historical fire perimeters** — BC wildfire history layer.
- **Statistics** — current extent vs. a historical baseline (current old
  growth + stands on equivalently high-site ground with an explicit harvest
  record), and the share of current old growth inside protected areas.

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
