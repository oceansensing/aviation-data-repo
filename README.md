# aviation-data-repo

The world's **airports**, from OurAirports, and **the FAA's special-use airspace and military training routes**
(since 2026-11-21): a data repository of the oceansensing ocean map system, with its own Pages site, its own
schedule and its own gigabyte, and no code of its own.

**Publishing since 2026-10-20**, daily at 03:17 UTC, the airports' step reading upstream each week and the
FAA's two once a 56-day charting cycle. `PLAN.md` is the founding plan; `CLAUDE.md` carries what must not be
got wrong and the shared doc doctrine.

## What it publishes

The world's airports, heliports, seaplane bases and balloonports from OurAirports, the closed ones left out: **`airports.json`**, every record — its ident, kind, name, elevation in feet, IATA and ICAO codes, municipality, country and region, whether it has scheduled service, each open runway (`<le>/<he> <length> ft <surface>`, lighted or not, the longest first) and at most eight frequencies (`<type> <MHz>`, the weather's and the tower's first) — and **`land/airports/`**, the same records as a pyramid of Mapbox vector tiles (uncompressed, extent 4096, one point layer `airports`): large airports from zoom 2, medium from 5, small from 8, heliports, seaplane bases and balloonports from 10, every point kept at deeper zooms, to zoom 10; its `index.json` names the version (the tiles' own hash) and every tile to zoom 8. R2's alone.

**`special-use-airspace.json`** (since 2026-11-21): every altitude band of every special-use airspace area on the
FAA's enroute charts — restricted, prohibited, warning and alert areas and military operations areas, 1,539
records on 2026-11-21 (another country's areas the FAA carries for its charts' borders — the Bahamas' six —
withheld, as the FAA says they are no official source) — each with its name, its kind, its floor and ceiling as the charts write them (`SFC`,
`1,500 ft AGL`, `4,000 ft MSL`, `FL 180`, `unlimited`), its times of use, its controlling agency and the FAA's
remarks, and the FAA's own codes beside them; **`land/special-use-airspace/`**, the same as a pyramid of vector tiles
(one polygon layer `airspace`, zooms 3 to 10). **`military-training-routes.json`**: every segment of every IR, VR and
SR military training route, 4,194 segments of 427 routes, each a centerline with its width either side in nautical
miles, its floor and ceiling and its route (`IR-109`); **`land/military-training-routes/`** (one line layer `routes`,
zooms 4 to 9, one feature a route to zoom 7). **Each root says plainly that whether an area or a route is active is
in the NOTAMs, not in the file**, and carries the FAA's own words. R2's alone.

These products are published **operationally but not drawn on the website's map**; the map's status
line still reports them when they fall behind, which is how their health stays visible.

## Where the data comes from

**The FAA's airspace** comes from its Aeronautical Data Delivery Service (ADDS, the Aeronautical Information
Services' ArcGIS layers `Special_Use_Airspace` and `MTRSegment`), a U.S. Government work whose items say *"The data
provided is for public use."* Both are republished every 56 days, and each item names its cycle (*"Current Effective
Date: 0901Z 29 Oct 2026 to 0901Z 24 Dec 2026"*); the site's `scripts/fetch-airspace.py` reads each layer once a
cycle, politely (ADDS answered 429 at 6,000 request units a minute during the research of 2026-11-20).

OurAirports (ourairports.com): `airports.csv`, `runways.csv` and `airport-frequencies.csv`, **read from the GitHub copy of its downloads** (davidmegginson.github.io/ourairports-data, refreshed daily at 01:53 UTC). **Its terms were read before a line was written** (2026-10-20): all of its data is released to the public domain and comes with no guarantee of accuracy or fitness for use; credit is welcome and not required, and the downloads' repository carries the Unlicense. ourairports.com itself answered HTTP 500 that night and its data page listed `airports.csv` at 0 bytes, which is why the GitHub copy is read and a short or empty file is refused.

## How it runs

The orchestrator (the site's private `pipeline/`), the fetchers and the
published-file contract all come from `oceansensing.github.io`, checked out at
run time. This repository carries `pipeline/products.toml` and its publish
workflow, and nothing else executable. Each run publishes to GitHub Pages and
to Cloudflare R2 from one build. Related repositories: `facilities-data-repo` (the other land points, made the same way),
`maritime-data-repo` and `fisheries-data-repo` (polygons and lines on the same machinery).

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
