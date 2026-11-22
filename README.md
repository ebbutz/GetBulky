# Gym Log

A small offline-capable web app to log gym trainings: training types, exercise types with break times, weight / reps / sets, an automatic break timer, and progress over time.

- Plain HTML, CSS and JavaScript, no build step, no dependencies
- Data stays in the browser (`localStorage`); backup and restore via the Setup tab
- Written for older browsers (tested target: iOS 15 Safari on iPhone 7)

## Run locally
Open `index.html` in a browser, or run `python3 -m http.server` in this folder.

## Deploy on GitHub Pages (free)
1. Push these files to a GitHub repository
2. Settings > Pages > Source: "Deploy from a branch", branch `main`, folder `/ (root)`
3. Open `https://<your-user>.github.io/<repo>/` on your phone, then Share > Add to Home Screen

## Data model
- `ex`: exercise types `{id, name, rest, sides}` (rest = break in seconds, sides = track left and right separately)
- `tr`: training types `{id, name, ex: [exerciseIds]}`
- `ses`: sessions `{start, end, runs: [{exercise, start, end, rest, sets: [{n, w, r, l?, wl?, t}]}]}`

For exercises with `sides`, `r` is reps on the right, `l` reps on the left, and `wl` the left weight if it differs from `w`.
