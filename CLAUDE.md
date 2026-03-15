# Canadian History Timeline — CLAUDE.md

## What this is
An interactive single-page study app for the Canadian citizenship test, based on the official *Discover Canada* guide. Built as a single `index.html` with no build step.

## Repo
- GitHub: https://github.com/Projects-with-Babajide/canadian-history-timeline
- Live (GitHub Pages): https://projects-with-babajide.github.io/canadian-history-timeline/

## Source material
All content is sourced from the official Canadian government citizenship study guide:
- **File:** `discover.pdf` (113 pages, 11MB) — included in this repo
- **Full title:** *Discover Canada: The Rights and Responsibilities of Citizenship*
- **Published by:** Citizenship and Immigration Canada
- The PDF covers: history, government, rights & responsibilities, symbols, regions, and the citizenship test process
- When adding or editing content in `data.json`, verify facts against `discover.pdf`
- Key history section: pages 14–27; Modern Canada: pages 24–27; People: scattered throughout

## File structure
```
discover.pdf — official source guide (Citizenship and Immigration Canada)
index.html   — full app (HTML + CSS + JS logic). No data lives here.
data.json    — ALL content: 10 eras, 60 events, 53 people with connections
data.md      — human-readable extract from discover.pdf (reference)
plan.md      — original build plan (9 chunks)
CLAUDE.md    — this file
```

## Running locally
Must be served from a web server (fetch() won't work over file://):
```bash
python3 -m http.server 7777
# then open http://localhost:7777
```

## Data structure (data.json)
```json
{
  "ERAS":   [ { "id", "name", "color" } ],
  "EVENTS": [ { "id", "year", "era", "title", "description", "people": ["person_id"], "related": ["event_id"] } ],
  "PEOPLE": [ { "id", "name", "era", "role", "description", "events": ["event_id"], "connected": ["person_id"] } ]
}
```
**To add/edit content, only edit `data.json`.** The app fetches it on load and rebuilds all lookup maps in `init()`.

## Era IDs
`pre-european` · `exploration` · `new-france` · `british` · `war-1812` · `confederation` · `ww1` · `interwar` · `ww2` · `modern`

## App features
1. **Timeline** — vertical animated timeline, grouped by era, color-coded
2. **People panel** — grid of all 53 key figures
3. **Quiz mode** — flip cards (Events / People / Mix), progress tracked in localStorage
4. **Era filters** — filter all views to a single era
5. **Search** — live keyword filter across title + description
6. **SVG connection lines** — clicking a card draws animated bezier lines to all connected cards visible in viewport
7. **Progress tracker** — "Mark as studied" persists to localStorage; Quiz "Got it" also marks studied

## Key implementation notes
- `eraMap`, `eventMap`, `personMap` are declared as `let` at top of script and rebuilt inside `init()` after data.json loads — do NOT move them back to module-level `const`.
- Connection lines use a fixed SVG overlay (`#connection-svg`, `pointer-events:none`) with `getBoundingClientRect()` for positioning; redrawn on scroll via `requestAnimationFrame`.
- Quiz deck is shuffled on each start; "Review again" moves the card to end of deck.
- All animations use CSS transitions + IntersectionObserver for scroll-in effects.

## Theme
- Dark background `#0D0D15`, Canadian red `#C8102E`, white text
- Google Fonts: Inter (body) + Playfair Display (headings/quiz years)
- Glassmorphism cards with `backdrop-filter: blur`

## What's left / known issues
- The SVG connection lines work but can't be screenshot-tested headlessly (Playwright font timeout)
- `favicon.ico` 404 is harmless — no favicon added yet
- GitHub Pages deploy takes ~1 min after each push
