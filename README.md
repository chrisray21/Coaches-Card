# Fall Ball Lineup Generator

A single-file web app for building fielding lineups for a development-focused fall baseball season. You pick who pitches each inning; it fills the other eight positions from each player's primary and secondary lists, keeps bench innings even, and tracks the whole season.

**File:** `index.html` (same app, also saved as `Fall Ball Lineup Generator.html`) — double-click to open in any browser. No install, no internet needed, nothing to sign into.

**Live site:** publish with GitHub Pages — see "Sharing it with other coaches" below.

---

## Quick start

1. Open the file. The roster is already loaded with all 12 players and their positions.
2. Go to the **Lineup** tab.
3. Set the number of **Innings** (defaults to 5).
4. Tap any player who didn't show up to mark them **absent**.
5. Tap any **priority players** — they'll be locked to their primary positions that game.
6. Pick a **pitcher for each inning**. This is the only assignment you make by hand.
7. Click **Generate Lineup**.
8. Adjust anything you want from the dropdowns, then **Print Card** for the dugout.

---

## The five tabs

**Lineup** — game setup and the position grid. Rows are positions (P, C, 1B, 2B, 3B, SS, LF, CF, RF) plus a bench row; columns are innings. Every cell is a dropdown you can override. Below the grid, a check panel confirms bench fairness and flags problems, and a player detail table shows each kid's bench innings, innings played, innings at a primary, and which positions they saw.

**Batting Order** — a continuous order: every available player bats whether or not they're on the field. Drag names or use the arrows. Absent players drop out automatically. Each game flips the previous game's order — see below.

**Roster** — click a position box to cycle through **PRI** (primary) → **SEC** (secondary) → **OUT** (lock-out) → blank. Blank means the generator will only use that spot as a last resort. Add or remove players any time. The **Position Coverage** table underneath shows how many players can legally fill each spot; a red number means you're thin there.

**Season** — bench innings per player per game, season totals, and innings by position. These totals feed the next lineup automatically.

**How to Save** — backup and restore, explained below.

---

## Rules the generator follows

Hard rules, never broken:

- A player is **never** placed at a lock-out position.
- Bench innings stay within **1** of each other — nobody sits two more innings than anybody else.
- Nobody sits two innings back to back.
- Priority players get a primary position every inning they're on the field.
- The pitcher you chose for an inning pitches that inning, period.

Preferences, applied as strongly as the hard rules allow:

- Primary positions where possible, secondary where needed.
- Repeats of the same position are discouraged, so players move around during the game.
- Season bench totals carry forward — whoever has sat the most is the last to sit again.

Soft rule:

- The next inning's pitcher sits the inning before so he can warm up. This bends when honoring it would break bench fairness. In testing it was satisfied about 80% of the time.

**Shuffle Again** produces a different arrangement that obeys all the same rules — useful if a valid lineup just doesn't feel right.

---

## Saving your work

**Everything saves by itself.** Every change — roster edits, attendance, pitchers, generated lineups, batting order — is written to your device the moment you make it. The small **Saved** tag in the bottom corner confirms it. There is no save button and you never re-enter the roster.

**The save is tied to one browser on one device.** If you open the file in Chrome, your season lives in Chrome. Opening the same file in Edge starts a blank season. Pick one browser and stay with it.

**Back it up.** On the **How to Save** tab, click **Download backup** to get a small `.json` file. Keep it in this folder or email it to yourself. To restore — on a new device, after clearing browsing data, or to hand the season to another coach — click **Restore from backup** and pick that file. Worth doing after each game so the season tracker is never more than one game out of date.

---

## How the batting order rotates

Set the order however you like for your first game. After that, **every game flips the previous game's order** — whoever batted last now bats first, second-to-last bats second, on down the card. Over a season that evens out plate appearances with nothing to track by hand.

It fills in automatically the first time you open a game's Batting Order tab, and it's only a starting point — drag anyone anywhere. The *next* game flips whatever you finish with, hand edits included. Each name shows where it batted last game (`was #7 in G2`) so you can eyeball the flip.

**Absences.** Anyone missing today drops out of the order. When they return they **lead off**, ahead of the flipped order, to make up some of the at-bats they missed. If several players return at once, whoever missed more games hits first.

**Corrected an earlier game?** Open the later game and click **Re-flip** to rebuild its order from the corrected one.

The **Batting Slot by Game** table on the Season tab shows every player's slot in each game plus their season average. That average column is the one to watch — over six games with strict flipping, everyone lands on the same number.

## When the game runs long or short

Games don't respect the plan, and the season tracker counts bench innings from whatever is saved here — so if the card says 5 innings and only 4 were played, every later game gets balanced off bad numbers. Fix it right after the game with **+ Add Inning** and **− Drop Inning**, which appear under the setup panel once a lineup exists. (Changing the Innings dropdown does the same thing, but asks first whether you meant to adjust or to start over with a brand-new lineup.)

**Game ended early.** Drop the innings that weren't played. Innings 1 through the last one played are kept *exactly* as they were — nothing is reshuffled. The dropped innings are parked, not deleted.

**Game went long.** Add an inning, pick who's pitching it, and the other eight spots fill in around whoever has already sat that game. Played innings are never touched. Add again for each additional inning. Bench fairness is recalculated across the longer game, so if you go to 6 or 7 innings the extra bench time lands on whoever has sat least.

**Changed your mind.** Trimmed an inning and then the game kept going? Adding it back restores the parked inning exactly as it was, as long as the same players are still available. If someone has since been marked absent, a fresh inning is built instead.

**Uneven bench innings after a short game** are just what happened — you'll see a note rather than an error, and the season tracker automatically gives the shorted players first claim on playing time in the next game.

## Sharing it with other coaches

Publish it free with **GitHub Pages**:

1. Push `index.html` to the repo (the app must be named `index.html` for the short URL to work).
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Pick branch `main` and folder `/ (root)`, then **Save**.
5. Wait a minute or two, then refresh the Pages settings page — it shows your live URL:
   `https://<your-username>.github.io/<repo-name>/`

Share that link. Anyone who opens it gets the app in their own browser, with their own private save. Nothing anyone enters is uploaded anywhere or visible to you.

**Things to know:**

- On a free GitHub account the repo must be **public** for Pages to work, and the published site is public either way. Player first names are in the file, so if that's a concern, blank the roster before pushing and let each coach enter their own.
- To update the site later, push a new `index.html` — the live site refreshes in about a minute.
- Coaches can add it to a phone home screen (Share → Add to Home Screen in Safari, or the install icon in Chrome) and it opens like an app, dugout-friendly.

## Notes on this roster

- **Catcher is thin.** Only Beau, Jacob, and Theo list C as a primary, and seven players lock it out. If two of those three are absent, expect the generator to lean hard on whoever's left.
- **Theo** had 2B listed as both primary and secondary in the original roster; it's kept as primary.
- Pitching isn't a roster attribute — you choose pitchers by hand each inning, so no primary/secondary/lock-out setting applies to it.

## If a lineup can't be built

You'll get a message rather than a bad lineup. It almost always means too many lock-outs at a thin position for the players available. Check **Position Coverage** on the Roster tab, then either loosen a lock-out or mark more players present.
