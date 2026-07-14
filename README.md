# Clima Catalunya

A self-taught geospatial data science roadmap, applied to one real question: how has temperature changed across Catalonia, and how does it relate to the territory (land use, hydrology, geological risk).

This repo is my build-in-public log for the *Modern GIS* roadmap — one module at a time, each producing a small, complete, public artifact. I write and debug the code myself; AI is used as a tutor (hints before solutions, verified execution before trusting a result), not as an autopilot.

## Roadmap & mini-project index

| Module | Topic | Status | Mini-project | Published |
|---|---|---|---|---|
| 0 | Terminal, git, environments, Docker | done | Repo setup, clean structure | 2026-06-30 |
| R | Research & sourcing | done | Foundation sheet (dataset + norm + method) | 2026-07-02 |
| 1 | Python + pandas | in progress | Temperature trend pipeline (Open-Meteo) + Leaflet showcase map | — |
| 2 | SQL + Supabase | not started | — | — |
| 3 | PostGIS | not started | — | — |
| 4 | GeoPandas + raster | not started | — | — |
| 5 | GDAL / QGIS | not started | — | — |
| 6 | Web mapping (MapLibre + PMTiles) | not started | — | — |
| 7 | Cloud-native (optional) | undecided | — | — |
| — | Capstone | not started | — | — |

This table gets updated as each module actually closes — it's a record of real progress, not a plan dressed up as one.

## What's a "showcase" piece?

Alongside the formal module deliverable, some modules also produce a small, deliberately simple Leaflet map: one static HTML file, no backend, published as-is. These are showcase, not mastery — they make results visible early. They don't replace the real web-mapping module (Module 6, built on MapLibre + PMTiles).

## Data & sources

Climate data: [Open-Meteo](https://open-meteo.com), CC BY 4.0. Every analysis in this repo cites its data source and license before any number gets published.