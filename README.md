# California Coast Road Trip — Interactive Map

A single-file, offline-friendly interactive map of California built for a family
road trip down the coast: **San Francisco → Solvang → Los Angeles → San Diego**,
with the Highway 1 stops in between.

It’s one self-contained `index.html` — pure SVG, no libraries, no build step,
no network calls. Open it in any modern browser (or host it on GitHub Pages) and
it just runs.

> Tip: add a `preview.png` screenshot to the repo root and drop an
> `![map](preview.png)` line here so it shows up at the top of the README.

## What it does

- **Hand-projected map of California** with the real coastline, terrain hachures,
  parks, the state highway network, and a dashed Highway 1 route line through the
  trip’s stops.
- **80+ tappable places**, each with a short kid-friendly history, a “wow” fact,
  a practical tip, and a link out (Wikipedia for landmarks, Google Maps for food
  and hidden gems):
  - **Famous spots** — Golden Gate Bridge, Alcatraz, Hearst Castle, Universal,
    the San Diego Zoo, and more.
  - **Hidden gems & oddities** — the Wave Organ, the 16th Ave Tiled Steps, the
    Museum of Jurassic Technology, Watts Towers, a hand-dug sea cave…
  - **Food & treats** — a mix of icons and current hot spots in SF and LA, plus
    a few in San Diego.
- **Slide-out index** with live search and **filter by interest** (Animals,
  Rides & Parks, Beaches, Science & Space, History, Art & Odd, Food, Sweet
  Treats).
- **Trip timeline** — an editable day-by-day plan; tap a day to fly to that leg.
- **“You are here” GPS** that only appears once you’re physically inside
  California (point-in-polygon against the real state outline).
- **Layer toggles** (terrain, roads, route, grid, place names) to keep it light
  on a phone.

## Run it

Just open `index.html` in a browser. That’s it.

To host it for free with **GitHub Pages**: push this repo, then in
**Settings → Pages**, set the source to the `main` branch (root). Your map will
be live at `https://<your-username>.github.io/california-roadtrip-map/`.

> Note: the GPS “You are here” feature requires a secure context, so it works
> over `https://` (including GitHub Pages) but not when opening the file from
> `file://`.

## Customize the trip

The trip is defined in one place — the `ITINERARY` array near the top of the
`<script>` in `index.html`. Each entry is one day:

```js
const ITINERARY = [
  { day:1, date:"Wed 6/17", title:"Arrive in San Francisco", city:"sf" },
  { day:6, date:"Mon 6/22", title:"Universal Studios",        landmark:"universal" },
  { day:3, date:"Fri 6/19", title:"Highway 1 drive south",    bounds:[[34.45,-122.7],[37.7,-119.9]] },
];
```

- `landmark` — an id from the place lists; tapping the day flies to that marker.
- `city` — `"sf"`, `"la"`, or `"sd"`; flies to that city.
- `bounds` — `[[latMin,lonMin],[latMax,lonMax]]` for a custom region (good for
  drive days).

Add your own places by appending to the `LANDMARKS`, `HIDDEN`, or `FOOD` arrays
in the same file — each entry follows the shape already shown there.

## Data & credits

- Place coordinates were gathered from Google Places and cross-checked against
  public sources; history and facts are summarized in the project’s own words.
- The California outline, terrain, and roads are hand-simplified for a stylized,
  hand-drawn look — they are illustrative, not survey-grade.
- Fonts: *IM Fell English* and *Spectral* via Google Fonts.

## License

[MIT](LICENSE) — do whatever you like; attribution appreciated.
