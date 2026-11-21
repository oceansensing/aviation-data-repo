# aviation-data-repo: the founding plan and running record

The world's **airports**, from OurAirports. Created on GitHub by the owner and given its documents by the site's
`pipeline/scaffold/new-origin.py`. **Nothing is published yet.**

## What it is for

The world's airports, heliports, seaplane bases and balloonports from OurAirports, the closed ones left out: **`airports.json`**, every record — its ident, kind, name, elevation in feet, IATA and ICAO codes, municipality, country and region, whether it has scheduled service, each open runway (`<le>/<he> <length> ft <surface>`, lighted or not, the longest first) and at most eight frequencies (`<type> <MHz>`, the weather's and the tower's first) — and **`land/airports/`**, the same records as a pyramid of Mapbox vector tiles (uncompressed, extent 4096, one point layer `airports`): large airports from zoom 2, medium from 5, small from 8, heliports, seaplane bases and balloonports from 10, every point kept at deeper zooms, to zoom 10; its `index.json` names the version (the tiles' own hash) and every tile to zoom 8. R2's alone.

## Where the data comes from

OurAirports (ourairports.com): `airports.csv`, `runways.csv` and `airport-frequencies.csv`, **read from the GitHub copy of its downloads** (davidmegginson.github.io/ourairports-data, refreshed daily at 01:53 UTC). **Its terms were read before a line was written** (2026-10-20): all of its data is released to the public domain and comes with no guarantee of accuracy or fitness for use; credit is welcome and not required, and the downloads' repository carries the Unlicense. ourairports.com itself answered HTTP 500 that night and its data page listed `airports.csv` at 0 bytes, which is why the GitHub copy is read and a short or empty file is refused.

## 2026-10-20: the first run, and the schedule

The first dispatched run (`39397791578`) was cancelled at its R2 job's fifteen minutes, its 56,491 tiles going up ten at a time; the site's R2 publish has sent 64 at a time since, and the job has an hour. The second (`39402269318`, 09:39 UTC on) was green: 72,684 open airports, 56,491 tiles in `land/airports/`, R2's alone. The schedule set then: daily at 03:17 UTC, the step reading upstream each week.

## 2026-11-21: the FAA's special-use airspace and military training routes

Two products joined (the owner's rulings of 2026-11-20 on the military layers: special-use airspace under both
Military and Aviation, one layer, so its data lives here once): **`special-use-airspace`** (the FAA's ADDS
`Special_Use_Airspace`, 1,539 altitude bands of the United States' areas — restricted 555, MOA 720, warning 212,
alert 39, prohibited 13 — a pyramid of 10,983 tiles, 5.8 MB, zooms 3 to 10; the Bahamas' five danger areas and one
prohibited area, which the FAA carries for its charts' borders and calls no official source, withheld and named) and **`military-training-routes`** (`MTRSegment`, 4,194
segments of 427 routes — IR 2,561, VR 1,102, SR 531 segments — 2,221 tiles, 1.0 MB, zooms 4 to 9), each read once a
56-day cycle (the cycle of 2026-10-29 09:01 UTC to 2026-12-24 09:01 UTC on the first read), measured by the site's
`scripts/fetch-airspace.py` on 2026-11-21. Rehearsed with the published branch as the last publish (a copy of the site's
`pipeline/scaffold/rehearse.sh` that checks out `origin/published` before the seed, as the workflow does): all three products fresh, `deploy=True`, and
**the airports unchanged** — not due, made again from the published root: `airports.json` byte for byte the
published one, version `9ec30524fc08`, 56,496 tiles. The workflow now installs `requirements-lands.txt` (Shapely and
numpy for the polygons) and carries the two trees in its cache as the airports' is.

## Open

1. A second run the next day: not due, the same version, nothing uploaded.
2. Then the daily schedule.
3. A month of runs read: the budget against the source's real lateness.
4. The first dispatched run with the FAA's products (`due=special-use-airspace,military-training-routes` is not needed: no root is published, so both are read), read: two products fresh, 13,204 new tiles on R2, the airports' version unchanged.
5. 2026-12-24 09:01 UTC, the next cycle: the run after it reads the item, then the layers, once.
