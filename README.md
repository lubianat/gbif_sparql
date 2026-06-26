# Species occurrences in nature reserves

A minimal web tool to explore GBIF species occurrence data spatially filtered to protected areas, powered by a live SPARQL endpoint.

## What it does

Pick a taxon, a country (or the whole world), and choose whether to restrict results to nature reserves. The tool builds a SPARQL query on the fly and embeds the result as an interactive map via [petrimaps](https://qlever.dev/petrimaps2/). A direct link to the same query in the QLever UI is always shown alongside the map.

## How it works

GBIF occurrence data is converted from Parquet to RDF using [gbif_parquet](https://github.com/Micelio/gbif_parquet). The resulting dataset is hosted and queried on [QLever](https://ui.qlever.dev/gbif), a high-performance SPARQL engine. Reserve boundaries come from OpenStreetMap via a federated query to QLever's OSM endpoint, using the GeoSPARQL `sfWithin` predicate to filter occurrences spatially.

## Usage

Just open `index.html` in a browser — no build step, no dependencies, no server required.

1. Type a taxon name (autocompleted from GBIF)
2. Choose **Nature reserves only** or **All areas**
3. Choose **By country** (enter a two-letter ISO code) or **Whole world**
4. Click **Map it**

The map renders inline. Use **Open query in QLever** to inspect, edit, or share the raw SPARQL.

## Notes

- Worldwide + all areas queries can be heavy for common taxa; petrimaps may cap results.
- Reserve geometries larger than 1 MB are excluded to keep queries fast.

## Background

This page was built as a demonstration of the value of a GBIF SPARQL endpoint for the [Ebbe Nielsen Challenge 2026](https://www.gbif.org/ebbe).
