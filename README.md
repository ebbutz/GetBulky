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
- `ex`: exercise types `{id, name, rest, sides}` (rest = break in seconds, sides = track left and right separately, lower = a lower weight is better (e.g. assisted pull-up), rounds and reps = recommended, as text like `3` and `8–12`)
- `tr`: training types `{id, name, ex: [exerciseIds]}`
- `wt`: workout types `{id, name}` (e.g. Build muscle, CrossFit); every training has a `wt`
- `wu`: warm-up types `{id, name}`
- `oth`: other workouts `{id, wt, name, start, min}` (`min` is optional)
- `ses`: sessions `{start, end, runs: [{exercise, start, end, rest, sets: [{n, w, r, l?, wl?, t}]}]}`

For exercises with `sides`, `r` is reps on the right, `l` reps on the left, and `wl` the left weight if it differs from `w`.

A session also has `wtName` (its workout type) and can have `warmups: [{id, wu, name, sec, km?}]` (`sec` = duration in seconds; older entries have `min`).

The date of the last "Copy backup" is kept on the device only (`localStorage` key `gymlog.lastcopy`), not in the backup text.


After finishing a Build muscle training the summary opens on the "Trends" tab; in Recent activity the "Overview" button opens it on the "Overview" tab. Both tabs are always one tap apart. Trends compare the last 3 trainings of each exercise, split into weight and volume. It is calculated from the stored sessions; nothing extra is saved.
