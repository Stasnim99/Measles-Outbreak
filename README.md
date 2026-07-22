# U.S. Measles Outbreak Report (2026)

A single-page website summarizing the 2026 U.S. measles outbreak, based on CDC data and public health reporting.

## Contents

- **`index.html`** — the website itself. It's a single file with the HTML, CSS, and JavaScript all included, so it needs no internet connection or external files to run. Double-click it to open it in a browser.
- **`README.md`** — this file.

## What the page covers

The page opens with a set of summary statistics: total confirmed cases for 2026, the number of states and jurisdictions affected, the share of cases tied to a known outbreak, vaccination status among cases, hospitalization rate, and age breakdown.

Below that is an outbreak map. Rather than a traditional geographic map, it's a tile-grid layout, one equal-sized square per state, arranged in roughly its real position, shaded by how many cases that state has reported. This keeps smaller states like Rhode Island as visible as larger ones like Texas, and it can be built entirely in CSS without a mapping library, so the page has no external dependencies. Hovering or tapping a tile shows the case count in a tooltip.

Following the map is a table of the ten states with the highest case counts, then a section on measles itself (symptoms, how contagious it is, possible complications, and how 2026 compares with past outbreak years), and a section on prevention covering MMR vaccine effectiveness and why vaccination status is driving where this outbreak spreads. A sources section at the end links directly to the CDC and the other public health outlets the figures were drawn from.

## Where the numbers came from

- CDC, [Measles Cases and Outbreaks](https://www.cdc.gov/measles/data-research/index.html) — the official case totals, updated every Thursday
- CDC, [Measles (Rubeola)](https://www.cdc.gov/measles/index.html), [About Measles](https://www.cdc.gov/measles/about/index.html), and [Measles Vaccination](https://www.cdc.gov/measles/vaccines/index.html) — symptoms, complications, and MMR effectiveness figures
- [Mappr, 2026 U.S. Measles Outbreak Map by State](https://www.mappr.co/us-measles-outbreak-map/) — the per-state case counts and rates used in the map and table
- [CIDRAP](https://www.cidrap.umn.edu/measles/us-measles-total-surpasses-1700-cases) — hospitalization rate, vaccination status, and age distribution
- [Johns Hopkins IVAC U.S. Measles Tracker](https://publichealth.jhu.edu/ivac/resources/us-measles-tracker) — used to cross-check outbreak figures
- Individual state health department press releases and dashboards (for example, the Idaho Department of Health and Welfare, Wyoming Department of Health, New York State and NYC Departments of Health, Maryland Department of Health, and about two dozen others) — used to fill in exact case counts for states the aggregator sites above only listed as "affected" without a number

A word of caution on the numbers: the CDC revises its counts weekly, and different outlets capture a snapshot at different times, so exact totals vary slightly depending on the source and date. The topline figure of 2,231+ cases reflects a CDC update from July 9, 2026. The state-level figures were pulled state by state, mostly from each state's own health department, and each is dated to when it was published, since not every state updates its count on the same schedule; the map's tooltip and hover notes show that date where it matters. A few jurisdictions (Alaska, Illinois, Wisconsin, Nebraska, Missouri, Kansas, and D.C.) are still shown without an exact number because no state-published total could be found; rather than estimate, the page leaves those as "cases reported" until a real figure turns up. For the current count, the CDC link above is the authoritative source.

## How it was built

The CDC's own data page blocks automated access, so the underlying figures were gathered through web searches of CDC pages and recent public health reporting (CIDRAP, Mappr, and Johns Hopkins IVAC), then cross-checked against each other before being written into the page.

The layout is a light, card-based design, an off-white background, a muted red used for outbreak severity, and a green used for prevention and safety guidance, organized into sections: summary statistics, map, state table, about measles, prevention, and sources. The map itself is a CSS Grid tile cartogram covering all 50 states plus D.C., built without any mapping library so the page works fully offline; a small script handles the hover tooltip and populates the table.

Since the figures shift from week to week, the page includes a visible "as of" date near the top and a longer data note in the footer, along with the source links, so anyone reading it can judge how current the numbers are.

## Updating the numbers later

The CDC refreshes its measles dashboard every Thursday. To bring this page up to date:

1. Check [cdc.gov/measles/data-research](https://www.cdc.gov/measles/data-research/index.html) for the latest totals and jurisdiction list.
2. Update the stat cards near the top of `index.html` (the `<div class="stats" id="stats">` block).
3. Update the `states` and `topStates` arrays near the bottom of `index.html`, inside the `<script>` tag, with the new case counts.
4. Update the "as of" date near the top of the page and in the footer disclaimer.
