# Coach's Card — Baseball Lineup Manager

A single-file web app for managing a youth baseball roster, fielding assignments,
saved fielding configurations, and the batting order. Phone-first, no build step,
no dependencies.

## Deploying to GitHub Pages

1. Create a repo (public or private — Pages works with either on most plans).
2. Drop `index.html` in the repo root and commit.
3. Repo **Settings → Pages → Build and deployment**: Source = *Deploy from a branch*,
   Branch = `main`, folder = `/ (root)`. Save.
4. Wait ~30 seconds. The site appears at `https://<user>.github.io/<repo>/`.
5. On a phone, open that URL and use **Share → Add to Home Screen** so it opens
   like an app.

That's the whole deployment. There is no server component.

## How it works

**Lineup tab** — the field with nine positions.

- Tap a bench player, then tap a position to place them.
- Tap a player already on the field to pick them up, then tap another position
  to swap, or tap an empty spot in the bench area to sit them down.
- Drag-and-drop also works: press and hold a player (about a quarter second on
  touch), drag to a position or to the bench, release.
- The dropdown holds saved configurations. **Save** names the current arrangement
  — it suggests "*Pitcher's first name* pitching" automatically. Saving under an
  existing name updates that configuration.
- The **⋯** button renames, duplicates, or deletes the selected configuration.
- The amber dot next to Save means the field no longer matches the saved
  configuration.

**Batting tab** — one batting order for the game, independent of fielding.
Drag by the handle, or use the arrows. The badge on the right shows each player's
current fielding position (or BN for bench) so you can spot a lineup where four
bench players hit in a row.

**Roster tab** — add, edit, and remove players. A player needs a jersey number
*or* a name; either alone is enough, so you can enter numbers off the back of the
jerseys at a tryout and fill in names later, or the reverse. A player with only a
number shows as "#12"; a player with only a name shows their initial in the circle.
Removing a player pulls them out of every saved configuration too.

## Where the data lives

Everything is stored in the browser's `localStorage`, on that one device, under
the key `coachscard.v1`. It survives closing the tab and restarting the phone; it
does not sync between coaches, and clearing site data erases it. Data saved by an
earlier build under `dugout.v1` is picked up automatically on first load.

**Export backup** / **Import backup** on the Roster tab move the whole dataset as
a JSON file, which is the stopgap until shared storage is added.

## Adding shared storage later

The state is one plain object — roster, order, field, lineups, activeId — read by
`load()` and written by `save()`. Swapping in a backend means replacing those two
functions with calls to Firebase, Supabase, or anything else, plus a subscription
that calls `render()` when remote data changes. `normalize()` already validates
and repairs any incoming payload, so it can be pointed at a server response
unchanged.

Worth deciding at the same time: whether the page should be readable by anyone
who finds the URL, or gated behind a shared team passcode.
