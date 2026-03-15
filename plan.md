# Canadian History Timeline — Build Plan

## Stack
- Single `index.html` file (HTML + CSS + vanilla JS, no build step)
- Google Fonts: Inter + Playfair Display
- SVG overlay for connection lines

## Chunks

### Chunk 1 — HTML skeleton + CSS foundation
- `<head>` with fonts, meta
- App shell: header, tab nav, era filters, search bar, main content area, SVG overlay placeholder
- CSS custom properties (colors, spacing, typography)
- Base layout (grid/flex structure)
- Dark background + red/white theme variables
- **Done when:** page loads with correct layout, no content yet

---

### Chunk 2 — Data file (inline JS)
- `ERAS` array (10 eras with id, name, color)
- `EVENTS` array (~60 events with id, year, era, title, description, people[], related[])
- `PEOPLE` array (~53 people with id, name, era, role, description, events[], connected[])
- **Done when:** data is fully defined and console.log shows correct structure

---

### Chunk 3 — Timeline view
- Render events as vertical timeline cards
- Year badge + vertical line + era-colored dot + card
- Cards slide in on scroll (Intersection Observer)
- Era color left border on each card
- Click to expand card (show full description, people chips, related event chips)
- **Done when:** full timeline renders, scroll animations work, cards expand/collapse

---

### Chunk 4 — Era filters + Search
- Era filter pills (All + one per era)
- Active filter highlights, inactive dims
- Search bar filters events + people live
- Smooth filter transitions (cards animate out/in)
- **Done when:** filtering and searching update the timeline in real time

---

### Chunk 5 — People panel (tab)
- Grid of person cards (name, era, role)
- Click to expand: full description, events they were part of, connected people
- Filterable by era (reuses same filter pills)
- **Done when:** People tab shows all 53 people, cards expand correctly

---

### Chunk 6 — Visual connection lines (SVG overlay)
- Fixed SVG overlay covering the full viewport
- When an event or person card is clicked/selected:
  - Find all connected cards currently visible in the DOM
  - Draw animated quadratic bezier curves between them
  - Lines colored by era of target card
  - Glow effect on active cards
- Lines redraw on scroll (requestAnimationFrame)
- Click elsewhere to clear connections
- **Done when:** clicking a card draws animated lines to all visible connected cards

---

### Chunk 7 — Quiz / flashcard mode (tab)
- Flip card animation (3D perspective rotateY)
- Front: year (events) or name (people) + era badge
- Back: full details + key connections
- Controls: "Got it ✓" (move to next) / "Review again ↺" (keep in deck)
- Progress bar showing deck completion
- Filter quiz by era or type (Events / People / Mix)
- **Done when:** full quiz flow works, flip animation is smooth

---

### Chunk 8 — Progress tracker
- "Mark as studied" button on each expanded card
- Studied state persisted in `localStorage`
- Progress counters in header (e.g. "12 / 60 events studied")
- Studied cards get a subtle checkmark badge
- **Done when:** studied state persists across page reloads

---

### Chunk 9 — Polish & animations
- Card entrance animations (slide in from right)
- Staggered load animation on initial render
- Era filter transition (smooth pill slide)
- Hover effects (card lift, glow)
- Mobile responsive tweaks
- Empty state for search with no results
- **Done when:** app feels polished, smooth and modern on desktop and mobile

---

## File structure
```
canadian-history-timeline/
  index.html    ← the entire app
  data.md       ← source data (reference only)
  plan.md       ← this file
```

## Color palette
| Token | Value | Usage |
|---|---|---|
| `--red` | `#C8102E` | Primary accent, Canadian red |
| `--red-dark` | `#8B0000` | Hover states, deep accents |
| `--red-glow` | `rgba(200,16,46,0.3)` | Glow effects |
| `--bg` | `#0D0D15` | App background |
| `--surface` | `#13131F` | Card background |
| `--surface-hover` | `#1A1A2E` | Card hover |
| `--border` | `rgba(255,255,255,0.08)` | Card borders |
| `--text` | `#F0F0F5` | Primary text |
| `--text-muted` | `#7777AA` | Secondary text |
| `--white` | `#FFFFFF` | Headings, highlights |

## Era colors
| Era | Color |
|---|---|
| Pre-European | `#8B6914` |
| Exploration | `#2E7D32` |
| New France | `#1565C0` |
| British Rule | `#6A1B9A` |
| War of 1812 | `#B71C1C` |
| Confederation | `#E65100` |
| First World War | `#37474F` |
| Between the Wars | `#558B2F` |
| Second World War | `#4E342E` |
| Modern Canada | `#00695C` |
