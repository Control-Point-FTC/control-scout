# Control Scout: everything done (Oct 14–15, 2026)

**All live on controlscout.org** (release `f84c101`, checked on the live site). 15 PRs merged: #63 through #77.

Every item went through its own PR. Each was merged only at **Greptile 5/5 on the latest commit with 0 open threads**, and merging deploys automatically to controlscout.org (with Render as backup). Bruno still does the live-site QA. Nothing here is self-certified.

---

## Search

- **"New Jersey" finds NJ events** (#65).
  - FIRST stores states as codes (NJ), so typing the full name only matched events with "New Jersey" in their title.
  - Full names now work for US states, Canadian provinces, Australian states and UK nations, looked up per country (MT is Montana in the US but Mato Grosso in Brazil).
  - Country aliases also work: United States / US / America, UK / Great Britain, UAE, Turkey, Korea.
- **"All events in New Jersey · 42 this season"** appears first when you type a state or province (full name, the start of one, or a code like "NJ"). It opens the Events page filtered to that state.
- **No more "doubles" in search results.**
  - The repeats were really the same event from different seasons, plus Parkway/Turnpike divisions whose names were cut off.
  - Each event code now shows once, from its newest season. Type a year ("2025 new jersey championship") to get older ones.
  - Division events still show, because they are separate events.
- **Search rows are two lines.** The full name wraps instead of being cut off, with a season tag (2025–26), code, date and place underneath. The second line now shows on phones too.
- **Older seasons dropped everywhere in search,** including the typo-tolerant fallback.

## Events pages, fully reworked (#74)

- **Events list:**
  - One filter bar with Season (every season with its game name), Place (full names, searchable), Event type, Date range and a text search.
  - Status chips: All / Live now / Upcoming / Finished, with counts.
  - The whole filter state is in the URL.
  - Cards are colour-coded by event type and grouped by week. "This week" is tagged.
- **Event page tabs:** Matches / Rankings / Insights / Teams (N) / Playoffs / Awards / Odds. Odds only shows for seasons with predictions.
- **Rankings and Insights** are now full stat tables with the toolbar built in: **Statistics**, **Filters**, **preset chips** and **Export CSV**.
- **Live events:** the official live standings come first, followed by the full stats table with an "as of HH:MM" note.
- **New `/teams` page:** records for every team, as team-at-event rows or whole-season rows.
- **New `/matches` page:** match records you can filter and sort by red/blue total, auto, driver-controlled, endgame, winning margin, event and date.
- **"Teams" entry in the sidebar.**
- **Live tables keep up:** during a live event, Rankings and Insights reload whenever results are checked or stats are rebuilt.
- **Shared links don't lose a broken filter:** it stays visible with its error until you clear or replace it.
- **A page number past the end** jumps to the last page with results.
- **Unticking every column, then exporting,** gives a CSV with just the fixed columns.

## Tables and panels, after your feedback (#76, #77)

- **Roomier tables:** more space in every cell, and stronger lines between rows and columns.
- **Column labels stay visible while you scroll** down the page, on desktop and phone. They line up exactly with their columns, even after you add or remove one.
- **A fade at the right edge** shows when there are more columns to scroll to.
- **Statistics and Filters open in a side panel on the right** instead of a popup over everything.
  - On wide screens the page makes room, so you can keep sorting and scrolling the table while the panel is open.
  - On narrower screens the panel sits over the right side, with no dimming.
  - On phones it's a sheet over the lower part of the screen.
  - Every feature is still there. The six stat toggles (TOT, AVG, OPR, MIN, MAX, DEV) now stack so they all fit.
  - Opening one panel closes the other, Esc closes it, and focus goes back to the button you clicked.
  - The filter match count updates if you change season, region, type or dates while the panel is open.
- **No more comparisons with other sites in the app's wording.** The hints now read "Who the team is: number, name, region, rookie year and school." and "From Control Scout predictions."

## Live sync reliability (#75)

- **The "database is locked" errors are gone.** During the overnight backfill, the 60-second live check sometimes logged this error 16 times. It now skips quietly while the backfill writes, and if a check is cut short, the next one finishes the job, so results never get stuck. There have been 0 errors since the deploy.

## Filters: built to beat FTC Scout

- **Filter editor:**
  - All/Any groups nested as deep as you like, with Add Condition, Add Group and × to remove.
  - A plain-English preview of the filter, e.g. "penalties under 2 and (OPR at least 55 or auto avg at least 30)".
  - A live result count while editing.
  - A searchable stat picker grouped by category, with descriptions, and per-condition validation.
- **On phones** the editor opens as a bottom sheet.
- **Operators:** = ≠ > ≥ < ≤, plus "contains" for text.
- **Text filters ignore case and accents,** so "equipe" finds "Équipe".
- **Stats you can filter by that FTC Scout's picker doesn't have:** team number, team name, region, rookie year and school.
- **Control Scout-only stats:** predicted win %, advancement odds and predicted score. These only appear for 2023 onward, the seasons with predictions.
- **Score stats** come with every aggregate: total, average, OPR, min, max and standard deviation, for total, non-penalty, auto, driver-controlled, endgame, penalties committed and opponent penalties.
- **Statistics button** shows or hides any stat as a column, and is remembered per table.
- **Sort** by any column, either direction, server-side, together with filters.
- **Export CSV** gives exactly the filtered, sorted rows with your visible columns. Large exports stream in bounded chunks.
- **Shareable links:** the filter lives in the URL in FTC Scout's own format, and **FTC Scout's filter links work on Control Scout unchanged.**
- **Saved filters:** save, use, rename and delete. They're stored on your device, so no login is needed.
- **One-tap preset chips:** Elite OPR, Clean drivers (penalties < 2), Auto specialists, Strong endgame and Favourites.
  - Thresholds are taken from the data (about the top 10% each season).
  - All presets live in one file, `src/config/filterPresets.ts`, so you can edit them.
- **Compare selected:** tick up to 4 teams in a table, then press Compare.
- **Accuracy check against FTC Scout:**
  - The brief's example (penalties < 2 AND (OPR ≥ 55 OR auto avg ≥ 30)) returns **137 team-events on both sites, identical**.
  - 2024: 1,404 vs 1,406. One scrimmage has no match data, and a few FIRST scores differ.
- **Speed:** filtered pages answer in about **12–90 ms**. A full-season CSV takes about 2 s.
- **Correct counting:** league meets count each meet's own matches. FIRST's league standings include earlier meets, which would double-count.
- **Stats never go blank during a refresh.**

## Past seasons: 2019 Skystone to now (#70)

- **Four new seasons:** 2019 SKYSTONE, 2020 ULTIMATE GOAL, 2021 FREIGHT FRENZY and 2022 POWERPLAY, with teams, events, matches and score breakdowns, rankings, alliances, awards, OPR, averages and records.
- **Team pages only list seasons the team actually played.** The current season is always listed. Registration-only years are hidden.
- **Season switcher:** recent seasons are buttons, and 2019–2022 sit in an "Earlier" menu so it fits on phones.
- **Old seasons are history only:**
  - No ratings, no Predict or Advancement buttons, no Odds tab and no what-if lab link.
  - No "no prediction" placeholders, and no Predict button on Compare.
  - Each page shows a short note: "predictions start with 2023–24".
- **2020 remote events:** rankings and awards are kept. Solo "remote matches" aren't shown as alliance matches.
- **A team with only remote results** opens on that season, not on an empty current season.
- **Predictions for 2023–2026 are byte-identical** to before (checked across 109,182 predictions).
- **Checked against FTC Scout:** 639 of 644 team averages match exactly.
- **Production filled them in automatically overnight:** 2022, 2021, 2020 and 2019 were all finished by 07:09 UTC, with no manual server steps. Team 4215 now lists every season from 2019 to 2026.
  - If a run is interrupted, the season's stats get retried.

## Live events: as fast as FTC Events (#71)

- **Live events check FIRST every 60 s** instead of every 15 minutes.
  - Only events happening today are checked.
  - It uses cheap "has anything changed?" requests, so each tick costs about 3 small requests per event.
- **"Refresh results" button** on live event pages, with "Results updated 40 s ago".
  - Anyone can press it, with no login.
  - It does one real refresh per event every 20 s, so crowds can't hammer FIRST.
- **Open live event pages update on their own** every minute while you're looking at them.
- **New results update** OPR, season rows and pre-match calls right away. The filter and CSV tables follow within 5 minutes.
- **Does it help prediction accuracy?** Measured on all 36,842 matches from 2025:
  - Prediction quality improves only slightly (Brier 0.1795 → 0.1791).
  - The big gain is the track record: **playoff calls logged before the match go from about 76% to 98%**.
- **Honest freshness:** "updated" only moves after a real check, and the page doesn't promise automatic checks when they're switched off.
- **Robust:** one failing FIRST endpoint, a rate limit, or a corrected lineup or withdrawn result no longer leaves stale or missing results.

## Faster pages (#67)

- **Fixed the ~8-second event page load** you hit at 11:47 PM.
  - **Cause:** after every sync (every 15 minutes on event days), the first visitor waited while the server rebuilt its prediction ratings, and everyone else froze for about 4.5 s.
  - I reproduced it on production: 7.5 s for the first request, then about 0.1 s.
- **Now:**
  - Pages always answer at once from the previous ratings while new ones build in the background.
  - Finished seasons are cached, so a rebuild takes **0.5 s instead of 8.5 s**.
  - The longest freeze went from **4.5 s to 27 ms**.
  - Predictions are identical to before.
- **The server starts answering within about half a second** after a deploy.

## Match lists you can follow (#69)

- **One column** in time order. Long schedules used to zig-zag across two columns.
- **Alliance boxes:** each alliance's teams and score are together. The winner's box is stronger and the loser fades.
- **Your team:** a gold outline, a gold stripe on its rows, and a **"4215 won" / "4215 lost"** badge.
- **A summary line:** "4215 in these matches: 8 won · 0 lost". It counts the same way as the season record.
- **The call in plain words:** "Picked Red 83%", then "✓ Right" or "✕ Upset", plus the confidence.
- **"No call · a robot sat out"** replaces "Robot missing — not predicted".
- **Full times** like "Sun 11:50 AM", no longer cut off.
- **Headings:** Qualifications / Playoffs on events. Team pages group matches under each event's full name.
- **Phones:** each match is a two-line scoreboard.

## Shortlist rework (#72)

- **Rows open in place** with no page change. The panel shows:
  - an auto / driver-controlled / endgame bar
  - an event-by-event chart
  - win chances and advancement odds
  - the last 5 matches
  - quick actions
- **Drag to rank your picks** with mouse, touch or keyboard (arrow keys), announced for screen readers.
- **"Order picks"** by OPR, rating, auto or endgame, with undo.
- **A private note per team,** saved as you type and synced to your account.
- **An OPR trend sparkline on every row.**
- **List / Grid views.** Grid is the default on phones, and your choice is remembered.
- **CSV export** in pick order with your notes. "Compare selected" or "Compare top 4".

## Offline seasons: no wifi, no SQLite tools (#68, #64)

- **"Save offline"** on each season on the Download page, with a progress bar.
  - It then shows Saved · size, Remove, and Update when a newer release is out.
  - The raw SQLite file is still offered as a small link.
- **With no connection,** a saved season's team pages, event pages and search all work, including teams never opened before.
  - Tested on the real production build with the network off.
  - Offline search now also matches cities, state names and years.
- **Settings › Offline data** lists your saved seasons.
- **Reliability:**
  - Saving on your very first visit still works offline.
  - Two tabs saving at once can't leave a hidden file.
  - A failed save or removal leaves things as they were.
  - Only the season you're looking at is opened, which keeps memory low.
- **The offline app was broken on the live site,** and that's fixed (#64). Since the SEO change the server redirected `/index.html`, so the offline cache stored a redirect and the app could fail to open with no signal.

## Animations (#66)

- Match details unfold and fold under the row.
- The account / sign-in panel fades and scales in from its corner.
- The sun/moon theme icon turns and cross-fades.
- The search results drop in.
- All under 0.3 s. With reduce-motion turned on, the movement is switched off.

## Sidebar (#63)

- Bigger text (13 → 15 px), icons (16 → 20 px), rows (32 → 40 px), brand mark and footer.

## Smaller fixes along the way

- The test that hung for hours (the "venue with no signal" flow) now fails with a clear message instead of hanging.
- `npm run audit:flows -- --only "<name>"` runs selected flows, and refuses a typo.
- `npm run shots` got `--storage` (pre-fill saved data), `--steps` and `--name` (scripted clicks).
- New `GET /api/records/:season/regions` feeds the Place dropdown.
- New batched `GET /api/shortlist` loads the whole shortlist in one request.

## Found, not changed (left for you to decide)

- **Possible 2023+ penalty mix-up:** when FIRST has no score breakdown for a match, the fallback may credit penalties to the wrong alliance. It's rare, and I left it untouched so 2023+ predictions stayed identical. **A one-click task chip is waiting for it.**
- **"Top 91%" wording:** on team pages a low rank reads like a good one (e.g. #4,138 of 4,572 shows as "Top 91%" in gold). This was there before. Something like "Bottom 10%" or "#4,138 of 4,572" might read better.
- **Still on your list:** rotating the VM poller's GitHub token (you said "later"), the Search Console sitemap submission, and Bruno's QA on the live site.
