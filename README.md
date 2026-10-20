# aviation-data-repo

The world's **airports**, from OurAirports: a data repository of the oceansensing ocean map system, with its own
Pages site, its own schedule and its own gigabyte, and no code of its own.

**Publishing since 2026-10-20**, daily at 03:17 UTC, the step reading upstream each week. `PLAN.md` is the founding plan; `CLAUDE.md` carries what must not be
got wrong and the shared doc doctrine.

## What it publishes

The world's airports, heliports, seaplane bases and balloonports from OurAirports, the closed ones left out: **`airports.json`**, every record — its ident, kind, name, elevation in feet, IATA and ICAO codes, municipality, country and region, whether it has scheduled service, each open runway (`<le>/<he> <length> ft <surface>`, lighted or not, the longest first) and at most eight frequencies (`<type> <MHz>`, the weather's and the tower's first) — and **`land/airports/`**, the same records as a pyramid of Mapbox vector tiles (uncompressed, extent 4096, one point layer `airports`): large airports from zoom 2, medium from 5, small from 8, heliports, seaplane bases and balloonports from 10, every point kept at deeper zooms, to zoom 10; its `index.json` names the version (the tiles' own hash) and every tile to zoom 8. R2's alone.

These products are published **operationally but not drawn on the website's map**; the map's status
line still reports them when they fall behind, which is how their health stays visible.

## Where the data comes from

OurAirports (ourairports.com): `airports.csv`, `runways.csv` and `airport-frequencies.csv`, **read from the GitHub copy of its downloads** (davidmegginson.github.io/ourairports-data, refreshed daily at 01:53 UTC). **Its terms were read before a line was written** (2026-10-20): all of its data is released to the public domain and comes with no guarantee of accuracy or fitness for use; credit is welcome and not required, and the downloads' repository carries the Unlicense. ourairports.com itself answered HTTP 500 that night and its data page listed `airports.csv` at 0 bytes, which is why the GitHub copy is read and a short or empty file is refused.

## How it runs

The orchestrator (the site's private `pipeline/`), the fetchers and the
published-file contract all come from `oceansensing.github.io`, checked out at
run time. This repository carries `pipeline/products.toml` and its publish
workflow, and nothing else executable. Each run publishes to GitHub Pages and
to Cloudflare R2 from one build. Related repositories: `facilities-data-repo` (the other land points, made the same way).

**Which document gets what, and what "update docs" means across all
thirty-one repositories, is the doctrine block at the top of `CLAUDE.md`**: the
same text in all thirty-one, held equal by the site's `check:docs`.

## Structure

```
README.md       what this is
CLAUDE.md       what must not be got wrong, and the shared doc doctrine
PLAN.md         the founding plan and running record
DECISIONS.md    dated one-way decisions, D1 onward
pipeline/       products.toml, the declaration the orchestrator reads
.github/        the publish workflow
```
