# California Coast Road Trip — Interactive Map

A single-file, offline-friendly interactive map for a family road trip down the
California coast: **San Francisco → Solvang → Los Angeles → San Diego**, with the
Highway 1 stops in between.

Everything is one self-contained `index.html` — pure SVG, no libraries, no build
step. Open it in any modern browser, or view it live on GitHub Pages:

**Live map: https://jonabe.github.io/california-roadtrip/**

## What it does

- **Hand-drawn map of California** with the coastline, terrain, parks, highways,
  and a dashed Highway 1 route line through the trip.
- **Tappable places** — each opens a card with a short, kid-friendly history, a
  “wow” fact, a tip, and links (Wikipedia and/or **Google Maps** to drive there).
- **Three tabs** in the slide-out dock:
  - **Index** — every place, with live search and filter-by-interest.
  - **Plan** — the day-by-day itinerary, grouped into collapsible legs
    (San Francisco · The Coast → Solvang · Los Angeles & Anaheim · San Diego).
    Each day shows its route, reservations, and tappable stops.
  - **Wish list** — “if we have time” picks, grouped per family member
    (E · A · M · J), shown as colored ★ on the map.
- **Layers you can toggle** on the map: famous spots, hidden gems, food, hotels
  (🏠 where we’re staying), and “beyond the trip” cities & landmarks.
- **Measure tool** — tap two points for an approximate distance and drive time.
- **“You are here” GPS** that appears once you’re physically in California.

---

## How to edit and publish

Everything lives in **`index.html`**. The trip data is in plain JavaScript arrays
near the top of the main `<script>`. You edit an array, **bump the version**, then
**commit and push** — GitHub Pages redeploys automatically.

### The 3-step workflow

```bash
# 1. edit index.html (see the data sections below)

# 2. bump BUILD_ID (so everyone's browser auto-refreshes to the new version)
#    find this line near the top of index.html and change the letter/date:
#      var BUILD_ID = "2026-06-11n";   ->   "2026-06-11o"

# 3. commit and push
git add -A
git commit -m "Update the trip plan"
git push
```

The live site updates in ~1–2 minutes (GitHub’s cache can take up to ~10 min).
The `BUILD_ID` bump makes any already-open page refresh itself to the latest.

> **Asking Claude to do it:** tell Claude what to change in plain words
> (“add In-N-Out as a wish for Axel”, “add a stop to the San Diego day”,
> “fix the Solvang dates”). Claude edits `index.html`, bumps `BUILD_ID`, and runs
> the commit + push for you.

> ⚠️ **This repo is public — no personal details.** Never put confirmation
> numbers, PINs, phone numbers, membership/loyalty numbers, or anything private
> into the file. Public info (place names, public addresses, websites) is fine.

### Where the data lives

All near the top of the `<script>` in `index.html`:

| Array | What it is |
|-------|------------|
| `ITINERARY` | the **Plan** — one entry per day |
| `WISH` | the **Wish list** — per-person “want to visit” picks |
| `HOTELS` | where we’re staying |
| `LANDMARKS` | famous map places |
| `FOOD` | food spots |
| `HIDDEN` | quirky hidden gems |
| `CONTEXT` | “beyond the trip” cities & landmarks (Seattle, Yosemite, …) |
| `FAMILY` | the four initials and their colors (E · A · M · J) |

### Editing the Plan (`ITINERARY`)

One object per day:

```js
{ day:5, date:"Sun 6/21", leg:"Los Angeles & Anaheim",
  route:"Los Angeles",                 // the bold line for the day
  note:"Hollywood · the beaches",      // small italic subtitle (optional)
  hotel:"hotel_anaheim",               // which HOTELS id we sleep at (optional)
  city:"la",                           // OR bounds:[[lat,lon],[lat,lon]] OR landmark:"id"
  stops:["hollywood","walkoffame","venice"],   // tappable place ids visited
  res:[{icon:"🍽", name:"Dinner — Malibu Farm", detail:"23000 Pacific Coast Hwy"}] },
```

- **`stops`** are ids from any place list (`LANDMARKS`/`FOOD`/`HIDDEN`/`CONTEXT`).
  Tapping a stop flies to it and opens its card.
- **`leg`** groups consecutive days into one collapsible section.
- **`res`** are reservations — keep them to a place name and public address only.
- The day’s **fly target** is `landmark` (a place id), `city` (`"sf"`/`"la"`/`"sd"`),
  or `bounds` (a region for drive days).

### Adding a wish (`WISH`)

```js
{ id:"innout", who:"A", name:"In-N-Out Burger", cat:"Burgers",
  region:"Fisherman’s Wharf, SF", lat:37.8074, lon:-118.4172,
  about:"Short description…",
  address:"333 Jefferson St, San Francisco, CA",   // public address only
  url:"https://www.in-n-out.com/" },
```

`who` is the family initial: `"E"` (Evelina), `"A"` (Axel), `"M"` (Maura),
`"J"` (Jonas).

### Adding a place to the map (`LANDMARKS` / `FOOD`)

```js
{ id:"uniqueid", city:"la", name:"Place Name", cat:"What it is",
  lat:34.05, lon:-118.24,
  hist:"A sentence or two of history.",
  fact:"A fun fact.",
  tip:"A practical tip (optional)." },
```

`city` is `"sf"`, `"coast"`, `"la"`, or `"sd"` (controls which Index group it
joins). Once added, the place can be used as a `stops` id in the Plan.

---

## Run it locally

Open `index.html` in a browser. (The GPS “You are here” feature needs `https://`,
so it works on GitHub Pages but not from a `file://` path.)

## Credits

- Coordinates gathered from public sources; history and facts are summarized in
  the project’s own words.
- The California outline, terrain, and roads are hand-simplified for a stylized
  look — illustrative, not survey-grade.
- Fonts: *IM Fell English* and *Spectral* via Google Fonts.

## License

[MIT](LICENSE) — do whatever you like; attribution appreciated.
