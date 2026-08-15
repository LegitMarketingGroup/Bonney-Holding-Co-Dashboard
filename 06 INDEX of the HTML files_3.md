# Index of the HTML files

Every client-facing HTML document produced in the out-of-home workstream, and which of
them carry a live interactive heat map. Sizes are large because the Legit logos and the
county basemap are embedded as base64, which is what makes each file work offline with
no server, no build step and no external assets beyond the Fira Sans webfont.

| File | Size | Live maps | Tables | ZIP records | What it is |
|---|---|---|---|---|---|
| `Big Air + Peter Levi - OOH creative territories.html` | 403 KB | **no** | 1 | 0 | Seven creative routes on the line "Same Family. One Name." |
| `Billboard invoice audit - Bonney and Peter Levi.html` | 401 KB | **no** | 2 | 0 | Every out-of-home invoice, January to May 2026, matched against revenue geography. |
| `Billboard locations - exact register, Clear Channel and Lamar.html` | 509 KB | **no** | 4 | 0 | All 177 boards in one searchable table. Lamar rows carry clickable true coordinates; Clear Channel rows carry cross-street text only. |
| `Billboard package - Bonney Holding Co.html` | 617 KB | **yes, 3** | 6 | 436 | The consolidated package. THREE live heat maps in one file, and the source the map component was extracted from. |
| `Board recommendation against budget - Bonney Holding Co, October 2026.html` | 440 KB | **no** | 12 | 0 | The budget recommendation. SUPERSEDED by the placement document below, which corrected the objective. |
| `Bonney - Sacramento revenue vs Clear Channel coverage.html` | 493 KB | **yes, 1** | 1 | 129 | Sacramento heat map with the 55 Clear Channel panels overlaid. |
| `Bonney Holding Co - complete billboard analysis, all nine documents.html` | 1005 KB | **yes, 6** | 22 | 913 | All nine documents in one tabbed file. SIX live maps. |
| `Commute intercept - can we reach the no-board ZIPs on the road.html` | 399 KB | **no** | 5 | 0 | Whether the no-inventory ZIPs can be reached on the commute instead. NOTE: this is the file carrying the three banned characters. |
| `Gallagher's - Chico-Redding revenue vs Lamar inventory.html` | 506 KB | **yes, 1** | 1 | 150 | Chico-Redding heat map with all 122 Lamar faces plotted individually. Bubble colour is direct-mail revenue per mail job in quartiles. |
| `Peter Levi + Big Air - Bay Area revenue vs Clear Channel coverage.html` | 499 KB | **yes, 1** | 1 | 198 | Bay Area heat map with a brand toggle for Peter Levi, Big Air or combined. |
| `Production guide - Big Air + Peter Levi OOH.html` | 399 KB | **no** | 1 | 0 | How to produce the creative. Written before the real panel dimensions were found. |
| `Where to place the boards - Bonney Holding Co, revised.html` | 442 KB | **no** | 11 | 0 | CURRENT. Placement on the corrected objective: customer base plus momentum, with both candidate lists side by side. |

---

## The map component

Extracted into `map component/` so a heat map can be dropped into the dashboard without
reverse-engineering a 600 KB document.

| File | Size | What it is |
|---|---|---|
| `map component/map-component-demo.html` | 13 KB | Open this first. All three maps running, standalone. |
| `map component/map-engine.js` | 13 KB | The engine, verbatim. Bootstraps every svg.map on the page. |
| `map component/map-data.js` | 153 KB | MAPS plus the shared county basemap, verbatim. |
| `map component/map-styles.css` | 1 KB | Map styles only, no document chrome. |
| `map component/map-markup-template.html` | 3 KB | One map instance. Duplicate and change data-m. |

| `map component/README.md` | 5 KB | Data schema, the three gotchas, how to add a fourth map. |

**Verified running standalone:** 3 maps, 314 revenue bubbles, 55 Clear Channel panels,
122 Lamar faces, 180 county paths, zero console errors. Zoom and layer state are isolated per
map, confirmed by zooming one to 8x and leaving the other two at 1x.

---

## Which file to take for what

| If the dashboard needs | Take |
|---|---|
| A live heat map inside the dashboard | `map component/`, start with the demo |
| The recommendation numbers as data | `01 billboard_and_direct_mail_data.json` |
| A static section to paste in today | `03 dashboard module.html` |
| The full reasoning behind the picks | `05 source document - where to place the boards.html` |
| Three maps already assembled on one page | `Billboard package - Bonney Holding Co.html` |
| Everything, tabbed, for a client to browse | `Bonney Holding Co - complete billboard analysis, all nine documents.html` |

## One caveat on the map data

The maps were built before the objective was corrected. Their bubbles are sized on **revenue**
and coloured on **inventory tier**, which is the customer-base view. They do not carry the
year-over-year growth axis that drives the current recommendation. The growth figures are in
`01 billboard_and_direct_mail_data.json` for every ZIP, so a growth-coloured variant is a data
change rather than an engine change: add a field to each ZIP record and extend the `mode` switch.
