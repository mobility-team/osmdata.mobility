# osmdata.mobility

`osmdata.mobility` is a Mobility-oriented fork of
[`ropensci/osmdata`](https://github.com/ropensci/osmdata).

The R package name is `osmdata.mobility` to avoid confusion with the upstream
CRAN package `osmdata`. It keeps the original osmdata API; exported functions
such as `opq()`, `add_osm_feature()`, `osmdata_sf()`, and `osmdata_xml()` are
unchanged.

For the full upstream package presentation, examples, and original
OpenStreetMap/Overpass documentation, see the original osmdata README:

https://github.com/ropensci/osmdata#readme

## What This Fork Changes

This fork carries Mobility packaging and integration changes for workflows that
reuse downloaded OpenStreetMap data across model runs.

The current changes are:

- The package is renamed to `osmdata.mobility`.
- The fork is published from `mobility-team/osmdata.mobility`.
- File-based Overpass XML input is validated, then kept as raw XML text so
  downstream Mobility code can reuse the exact downloaded OSM XML payload.
- The package is listed in the Mobility R-universe registry.

## Installation

From Mobility R-universe:

```r
install.packages(
  "osmdata.mobility",
  repos = c("https://mobility-team.r-universe.dev", "https://cloud.r-project.org")
)
```

From GitHub:

```r
install.packages("remotes")
remotes::install_github("mobility-team/osmdata.mobility")
```

## Basic Usage

```r
library(osmdata.mobility)

q <- opq("Geneva, Switzerland") |>
  add_osm_feature(key = "highway")

roads <- osmdata_sf(q)
```

## Reusing Saved OSM XML

For Mobility workflows, download OSM XML once and reuse the saved file in later
steps:

```r
q <- opq("Geneva, Switzerland") |>
  add_osm_feature(key = "highway")

osmdata_xml(q, filename = "geneva-roads.osm")

roads <- osmdata_sf(doc = "geneva-roads.osm")
```

## Versioning

This fork currently publishes `osmdata.mobility` version `0.2.5.005`, based on
upstream osmdata plus the Mobility XML reuse change.

## License

This fork follows the upstream osmdata license: GPL-3.
