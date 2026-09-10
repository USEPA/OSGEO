GeoParquet cloud-native slides (Quarto + Jupyter)

Delivered 2026-08-31: two parallel slide decks demonstrating GeoParquet as a cloud-optimized format, built for the blog / a workshop.

geoparquet-cloud-native-slides.qmd — Quarto revealjs, Python via jupyter: python3
geoparquet-cloud-native-slides.ipynb — same content as a Jupyter slideshow (cell slideshow.slide_type metadata; renders with jupyter nbconvert --to slides or RISE)

Both were sent to the user via chat, not saved to a connected folder (none was connected this session).

Outline
Cloud-optimized-for-vectors framing (COG analogy: row groups + column stats + bbox covering metadata + HTTP range requests)
Hands-on: write a small GeoParquet (PNW cities) with GeoPandas, inspect the "geo" metadata JSON and bbox struct column — actually executed, real output
What's new for 2026: Parquet 2.11 added native GEOMETRY/GEOGRAPHY logical types (March 2025); GeoParquet 2.0.0-rc.1 re-anchors on those native types (WKB on BYTE_ARRAY only, CRS lives on the logical type, GeoArrow encodings dropped). GDAL/OGR ≥3.12 supports native types; GeoPandas 1.1.4 still tops out at GeoParquet schema_version 1.1.0 (verified via SUPPORTED_VERSIONS)
geoparquet-io (beta CLI/lib): bbox + Hilbert sort + ZSTD optimization, validation/repair, cloud I/O
Live cloud query example: Overture Maps GeoParquet on public S3 (s3://overturemaps-us-west-2/release/{release}/theme={theme}/type={type}/*), queried with DuckDB spatial+httpfs, bbox-filtered to a Corvallis, OR AOI (places + buildings) — code copied verbatim from docs.overturemaps.org, current release used: 2026-08-19.0
Application: GeoLibre (opengeos/GeoLibre) — cross-platform cloud-native GIS (MapLibre + DuckDB-WASM + deck.gl + Tauri v2), Python package (from geolibre import Map, m.add_geoparquet(url_or_path, name=, **style)) and R package geolibre-r for Quarto/RStudio/Shiny. Verified real API by installing the PyPI package and introspecting it (not from docs alone).
Cheat-sheet table of tool support + wrap-up + resource links
Verification notes (for reruns / future edits)
This sandbox's egress policy blocks S3 (overturemaps-us-west-2...) and extensions.duckdb.org, so the DuckDB/Overture cells could not be executed here — they're left unexecuted in the notebook (reverted after erroring) and marked eval: false in the qmd. They should run fine on a normal machine with internet access.
Everything else (GeoParquet write/inspect, ecosystem version check, GeoLibre map construction) was actually executed and produced real output before delivery.
Sources used
https://geoparquet.org/releases/v1.1.0/ · https://geoparquet.org/releases/v2.0.0-rc.1/
https://parquet.apache.org/blog/2026/02/13/native-geospatial-types-in-apache-parquet/
https://medium.com/radiant-earth-insights/geoparquet-parquet-geospatial-types-a-time-of-transition-a42e391cdab2
https://rednegra.net/blog/20250925-parquet-with-geometry-type-is-not-geoparquet/
https://cloudnativegeo.org/blog/2026/03/introducing-geoparquet-io/
https://docs.overturemaps.org/getting-data/duckdb/
https://geolibre.app · https://github.com/opengeos/GeoLibre · https://r.geolibre.app
Possible follow-ups
A second AOI/dataset (e.g., NOAA/USGS hydrography) if a hydro-flavored example is wanted instead of/alongside Overture
An actual rendered HTML export (quarto render) or nbconvert --to slides output for direct blog publishing once run on a machine with internet access