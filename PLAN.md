# aviation-data-repo: the founding plan and running record

The world's **airports**, from OurAirports. Created on GitHub by the owner and given its documents by the site's
`pipeline/scaffold/new-origin.py`. **Nothing is published yet.**

## What it is for

The world's airports, heliports, seaplane bases and balloonports from OurAirports, the closed ones left out: **`airports.json`**, every record — its ident, kind, name, elevation in feet, IATA and ICAO codes, municipality, country and region, whether it has scheduled service, each open runway (`<le>/<he> <length> ft <surface>`, lighted or not, the longest first) and at most eight frequencies (`<type> <MHz>`, the weather's and the tower's first) — and **`land/airports/`**, the same records as a pyramid of Mapbox vector tiles (uncompressed, extent 4096, one point layer `airports`): large airports from zoom 2, medium from 5, small from 8, heliports, seaplane bases and balloonports from 10, every point kept at deeper zooms, to zoom 10; its `index.json` names the version (the tiles' own hash) and every tile to zoom 8. R2's alone.

## Where the data comes from

OurAirports (ourairports.com): `airports.csv`, `runways.csv` and `airport-frequencies.csv`, **read from the GitHub copy of its downloads** (davidmegginson.github.io/ourairports-data, refreshed daily at 01:53 UTC). **Its terms were read before a line was written** (2026-10-20): all of its data is released to the public domain and comes with no guarantee of accuracy or fitness for use; credit is welcome and not required, and the downloads' repository carries the Unlicense. ourairports.com itself answered HTTP 500 that night and its data page listed `airports.csv` at 0 bytes, which is why the GitHub copy is read and a short or empty file is refused.

## 2026-10-20: the first run, and the schedule

The first dispatched run (`39397791578`) was cancelled at its R2 job's fifteen minutes, its 56,491 tiles going up ten at a time; the site's R2 publish has sent 64 at a time since, and the job has an hour. The second (`39402269318`, 09:39 UTC on) was green: 72,684 open airports, 56,491 tiles in `land/airports/`, R2's alone. The schedule set then: daily at 03:17 UTC, the step reading upstream each week.

## Open

1. A second run the next day: not due, the same version, nothing uploaded.
2. Then the daily schedule.
3. A month of runs read: the budget against the source's real lateness.
