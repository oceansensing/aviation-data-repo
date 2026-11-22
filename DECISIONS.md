# Decisions

Dated, irreversible-leaning decisions, one entry each, newest last. The
reasoning lives in `PLAN.md`.

**What counts as one-way in a data repository**: a decision that puts bytes in
readers' hands under a shape they will code against; a decision about which
repository owns a product, since moving one costs a migration in two places;
and a decision that forecloses an upstream.

## D1 — 2026-10-20 — Its own repository, R2 alone, its tiles made from its root every run

The world's airports get a repository of their own (2026-10-20) and **publish to Cloudflare R2 alone**, as every new product since the site pipeline's D13: Pages carries the status alone, and the website's map draws nothing of it. The records are the root, banked on the `published` branch; the tile pyramid beside it is made from them on every run, since a folder is never banked, and the source is read weekly.

## D2 — 2026-11-21 — The FAA's special-use airspace and training routes live here, once, read once a cycle

The FAA's special-use airspace and military training routes join this repository (2026-11-21): the special-use
airspace is both a military and an aviation product, so its data lives once, here, beside the airports,
and the training routes with it. Both R2's alone. **Read once a 56-day charting cycle**, the cycle's first moment the
products' hour: the FAA's ADDS is asked for a layer only once the published cycle has ended and its item names a new
one, since ADDS refuses heavier use. Every root says that whether an area or a route is active is in the NOTAMs.
