# PitWall Companion

An **offline-first**, phone-installable Progressive Web App (PWA) for tracking
your **F1 Clash** driver and component **levels** and **card counts**. It turns
the community *F1 Clash 2026 Resource Sheet (v1.0 by TR The Flash)* into a
living tracker you can update on the go.

- 📴 **Works fully offline** after the first load (service worker precache).
- 📱 **Installable** to your home screen on Android and iOS; runs standalone.
- 📲 **Get the app on another device in one scan** — the Season tab has a
  built-in QR code and copy-link button for the live URL.
- 🔒 **All data stays on your device** — nothing is sent anywhere, no accounts,
  no analytics, no network calls at runtime.
- ⚙️ **No build step, no framework, no server** — just static files.

> Unofficial fan tool. Not affiliated with F1, Formula 1, or Hutch Games.

## Features

- Five tabs: **Drivers**, **Parts** (components), **Tools**, **Season**, and
  **Rewards**.
- **Drivers** tab grouped into six collections — Common, Rare, Epic,
  Legendary, **Paddock Picks** and **Paddock Picks: Turbo** — and a
  **Parts** tab grouped by category (Front Wing, Brakes, Suspension, Rear
  Wing, Gearbox, Engine, Battery). The two Paddock Picks collections are
  separate in-game (8 cards each) and share one rarity, **Special**.
- Each card shows a **rarity badge**, then either a **Series badge** (e.g. *S3*
  — the Series that first unlocks the card) or, for cards that state their own
  GP Event floor instead, an **availability badge** (e.g. *Contender+*), a
  **Level** with −/+ steppers, an
  **editable card count**, and a **progress bar toward the next level** (or
  **★ MAX** when the card is at its rarity cap). The bar label shows the
  **coin cost** to the next level alongside the card cost.
- **Stats & costs** panel per card (tap to expand): the card's per-level stats
  (drivers: Overtaking / Defending / Qualifying / Race Start / Tyre Use;
  components: Speed / Cornering / Power Unit / … as applicable), its
  **Total Value** and **Team Score**, and the **cards + coins remaining to
  reach max**.
- **“If upgraded” preview** in the same panel: the per-stat change from the
  current level to the next, the new Total / Team Score, and the exact
  **card + coin cost** to get there.
- **Boosted +10% toggle** per card: models the game's "boosted" card slot by
  scaling that card's displayed stats and Total / Team Score by +10%. (See
  *Data notes* for how Pit Time is handled.)
- **Series filter + sort** bar on the Drivers/Parts tabs: filter to a single
  unlock Series and sort by Series, Level, Total, Team Score or Name.
- **Collection "to max" summary** at the top of each tab: total cards left,
  total coins left, and how many cards are already maxed.
- **Asset Trading surplus** — once a card is maxed, the cards you keep piling up
  become tradeable surplus. Each maxed card shows a **♻ *N* to trade** chip and,
  in its Stats & costs panel, the surplus count and how many Asset Trades it's
  worth (Common ×1000, Rare ×100, Epic ×10, Legendary ×3 surplus per trade). The
  collection summary totals the surplus and trades available across the tab, and
  it all recomputes live as you edit card counts.
- **Search** by name and **filter chips** (All + each group of the active tab).
- **Export** / **Import** a JSON backup, and **Reset** to the built-in defaults.
- **Dark mode by default**, honoring `prefers-color-scheme`.

### Tools tab (coach)

Suggested Drivers, Loadouts, and Compare are all **computed live** from your
current card levels — nothing stored beyond your Loadouts preferences. The
Boosts tab is the one exception: quantities you enter there (and any Boosts
you add) are stored, since there's no other source for that data.

- **Suggested Drivers** — for each attribute (Overtaking, Defending, Qualifying,
  Race Start, Tyre Mgmt) your best-owned drivers ranked by that stat at their
  current level, with rarity, level, Total / Team Score and the *→ next level*
  value. Cards you've flagged **Boosted +10%** are ranked with their boosted
  numbers.
- **Loadouts** — two modes, switchable at the top of the tab:
  - **By Attribute** — tap any combination of attribute buttons (Speed,
    Cornering, Power Unit, Qualifying) to pick what to optimize for; one
    loadout card shows the best pick from **your owned components** for that
    combination — one part per category chosen to maximise the selected
    stat(s), with the resulting aggregate stats, Total / Team Score, and an
    *if each part +1 level* projection.
  - **By Track** — pick one of the **21 in-game circuits** from a dropdown to
    see: your best **2 owned drivers** for that track's spotlighted driver
    stat (side by side), a **Suggested Boost** — the top 3 owned consumable
    Boosts ranked by that driver stat first and the track's component stat as
    tiebreak — and the same full loadout card as By Attribute, built for the
    track's component stat.

  Your mode, attribute selection, and last-viewed track are all remembered
  across visits.
- **Compare** — a sortable, side-by-side stat table of your drivers or your
  components at their current levels. Tap any column header to sort; the wide
  component table scrolls inside its own container.
- **Boosts** — set how many of each consumable Boost you currently own (used
  by Loadouts → By Track's Suggested Boost). A dropdown picker shows one
  Boost's stats and a quantity-owned field at a time, rather than scrolling a
  list of 69. A **New Boost** form below it lets you add Boosts the game has
  added that this app doesn't know about yet — enter a name and any of the 13
  known stat fields; it's blocked from reusing a built-in Boost's name, and
  once added it behaves exactly like a built-in one (shows in the picker,
  counts toward Suggested Boost rankings).

### Season tab (progress dashboard)

A live snapshot of your season. A new install starts at a beginner state
(Rookie, Series 1, zero races and counts); the milestone scales themselves come
from the workbook's **CC Tracker**:

- **Season countdown** — a *days-left* counter plus editable **Season start**
  and **Season end** dates and a *season elapsed* bar (today is read live from
  the device clock).
- **Collection & race progress** — **current ÷ target** counts for Drivers,
  Driver Upgrades, Parts and Part Upgrades, counted straight off your Drivers
  and Parts tabs and so read-only here: cards at level 1+ out of every card in
  the game, and level-ups banked out of every level-up available. Custom cards
  you add are included automatically. Below them are milestone pickers for
  Weekly League, GP Medals (total & best), Highest Series, Races Done and Races
  Won, which are yours to set. Each row shows a progress bar and a live
  percentage.
- **CC Score** — **Base Asset Progress**, **CC Rank** (/20), **CC Points**
  (/500) and **Total CC** (/650), all **recomputed live** exactly as the
  workbook does (average of the ten base metrics → rank → points → plus the
  coin-bank contribution). Editing any input updates the score instantly.
- **Now vs potential** — each CC figure also shows a **▲ potential** value
  underneath: what your score becomes if every count metric reaches its target
  (the workbook's *Potential Completion* projection) — i.e. a fully maxed
  collection on top of the milestones you have selected.

The milestone inputs are saved separately in `localStorage` under
**`f1sheet.season.v1`** (schema-guarded). The four collection counts are stored
nowhere — they are derived from your collection every time the tab renders, so
they cannot drift out of step with it. Nothing leaves the device.

### Rewards tab (reference tables)

Read-only, searchable reference tables embedded from the community sheet:

- **Boosts** — all **69 named consumable boosts** (the original 65 from the
  workbook plus 4 discovered in-game since) and the flat per-race stat bonus
  each applies. Search by boost name *or* by a stat (e.g. type `cornering` to
  see every boost that helps cornering). This table only covers the built-in
  list — any Boost you add yourself via Tools → Boosts → New Boost shows up
  there and in Suggested Boost rankings, but not in this read-only table.
- **Series Unlocks** — how many drivers and parts first unlock at each Series.
- **Race Medal Payout** — medal-pot share by tier and finishing position.
- **Weekly League** — completion weight by final standing.
- **Races & Wins Milestones** — completion weight by total races/wins.
- **Series Progress** — completion weight by highest Series reached.
- **GP Medal Quality** — best-medal scoring scale.
- **Coins → CC** — coin-bank milestone to CC contribution.

The percentages are the same completion weights the Season tab uses for CC
scoring. Type in the search box to filter tables and rows.

### Reference data (stats & coin costs)

Per-level **stats**, **Total / Team Score**, **coin/card upgrade costs** and the
**unlock Series** are baked into the app from the *F1 Clash 2026 Resource Sheet
v1.1* (`DriverStats` and `ComponentStats` sheets). This covers **88 driver
cards** (Common, Rare, Epic and Legendary) and **all 46 components** across the
seven categories — every card the source sheet publishes. (An earlier build only
carried 13 drivers and 11 components; the full per-level dataset is embedded as
of this release.)

**17 further driver cards come from in-game screenshots, not the sheet** —
Johnny Herbert (the 23rd Legendary) and the 16 Paddock Picks / Paddock Picks:
Turbo cards — bringing the app to **105 drivers**. The sheet has not been
updated for them, so their data is deliberately partial rather than guessed:

- The 16 **Special** cards carry **level 1 only** — that is what a locked card's
  compare view shows. (The *Stats at Max Level* chip on those cards is an
  un-pressed toggle, not a description of the numbers below it; this was
  verified against Senna, whose locked card resolves to exactly his level-1 row
  in the sheet.) No level curve above 1, no coin costs, and no Asset Trade rate
  are claimed for them. `CAP.Special` is **7 provisionally**, mirroring
  Legendary — no Paddock Picks card's real cap has been observed yet, so
  cards-to-max for those 16 rests on that assumption.
- **Herbert** carries a full level 1–7 curve. His level-1 line is a permutation
  of the Fisichella / G.Villeneuve / McLaren cohort's, and that cohort shares one
  stat/cost curve, so his remaining levels are cloned from it — the same
  cohort rule the app already applies to user-added drivers. Coin costs come
  from the cohort too and were confirmed against the in-game upgrade price.

Cards still at **level 0** (not yet unlocked) show a "unlock to see stats"
hint — that's expected; the numbers appear as soon as the card reaches level 1.

> **Cards-to-max**, **coins-to-max**, **stats**, **Series** and the
> **if-upgraded** preview are available for every card.

### Rules used for progress

```js
// cards needed to reach the NEXT level, keyed by current level
const COST = {1:4,2:10,3:20,4:50,5:100,6:200,7:400,8:1000,9:2000,10:4000,11:8000};
// max level per rarity (from the workbook stat sheets)
const CAP  = {Common:11, Rare:9, Epic:8, Legendary:7, Special:7};
// per-card "boosted" slot scales stats by +10%
const BOOST_PCT = 0.10;
```

Progress toward the next level is `min(amount / COST[level], 1)`; at
`level >= CAP[rarity]` the card shows **★ MAX** instead of a bar.

## Run locally

Because a service worker is used, open the app over `http://` rather than a
`file://` path. From the repo root:

```bash
# Python 3
python3 -m http.server 8000
# then visit http://localhost:8000/
```

Any static file server works. First load caches everything; after that you can
go offline and it keeps working.

## How your data is stored

- Card levels/counts live in `localStorage` under the key **`f1sheet.v1`**.
- Only values you **change** are stored (as *overrides* keyed by card id), so
  future seed-data updates still flow through to cards you haven't touched.
- **A fresh install starts every card at level 0 with 0 cards** — the app ships
  the card *catalogue*, not anyone's collection. Up to v16 the seed carried the
  author's own progress, which meant a new download opened onto someone else's
  levels.
- Because overrides are diffs, zeroing that seed would have silently reset any
  card a existing user had left at its seeded value. `SCHEMA` is therefore now
  **2**: a stored schema-1 payload is migrated on first load, writing the old
  seed values back as real overrides (`LEGACY_SEED` / `migrateLegacySeed`), so
  upgrading users keep exactly what the app was already showing them. An
  explicit schema-1 override always wins, including one that set a card to 0.
- Season-dashboard values live under a separate key **`f1sheet.season.v1`** —
  the milestone metrics and the season dates only. The four collection counts
  are *not* stored: they are counted from the collection above on every render.
  (They used to be stored, and stored numbers that nothing updated is exactly
  why the dashboard read 0% for collections that were well underway.)
- Per-card **Boosted +10%** toggles live under **`f1sheet.boosted.v1`**.
- Loadouts preferences (mode, selected attributes, last-viewed track) live
  under **`f1sheet.loadoutAttrs.v1`**.
- Boost quantities owned (and which Boost the picker last showed) live under
  **`f1sheet.boostOwned.v1`**.
- Boosts you've added yourself via New Boost live under
  **`f1sheet.customBoosts.v1`**.
- A `schema` field is stored on each for safe future migrations.
- Card id format: `d:<Rarity>:<Name>` for drivers, `c:<Category>:<Name>` for
  components.

> **Note:** Export / Import currently covers the card overrides (`f1sheet.v1`).
> Season inputs, Loadouts preferences, Boost quantities, and custom Boosts all
> persist locally but aren't yet part of the backup file.

### Data notes / limitations

- The **Race Medal Payout**, **Weekly League**, **Races/Wins**, **Series**,
  **GP Medal** and **Coins → CC** tables are byte-identical in the v1.0 and
  v1.1 workbooks, so they're treated as stable game constants.
- **GP Medals Total** counts toward the CC score as complete once you hold at
  least one GP medal (mirroring the workbook's `IF(total>1, 1, total)` rule).
- **Per-Series unlocks are now included.** The v1.1 workbook carries a *Series*
  column on each card's stat rows (DriverStats col L, ComponentStats col O),
  read from each card's level-1 row. That drives the **Series badge**, the
  **Series filter/sort**, and the **Series Unlocks** reference table. The
  **Legendary drivers carry Series 0** in the sheet (they unlock from sources
  other than Series progression), so they show **no Series badge**.
- **Some cards state a GP Event tier instead of a Series.** Every Paddock Picks
  card prints an *Event availability: <tier> or higher* line, and so do the
  Legendaries — and they do **not** agree with each other: Herbert and
  Fisichella read *Junior or higher*, while Senna reads *Champion*. That means
  the app's blanket "Legendary drivers allowed" toggle is wrong for Legendaries
  as a group. Where a card declares a tier it is authoritative for GP Event
  eligibility; every other card keeps the old Series/Legendary behaviour.
  **All 23 Legendaries** have now been read off their in-game cards: Junior+ for
  the 110-total cohort, Challenger+ at 200–245, Contender+ at 265–290, and
  Champion from 335 up. Tier tracks level-1 power monotonically, and no power
  cohort spans two tiers.
- Because every Legendary now states its own tier, the **"Legendary drivers
  allowed"** toggle no longer changes anything. It is kept as the fallback for
  any Legendary the game adds before its card has been read — a new one arrives
  with no tier, exactly as Herbert did — and its label now says so.
- **Boosts: 65 unique named boosts from the workbook, plus 4 added since.** The
  workbook's *Boosts* sheet spans ~214 rows, but that count includes blank
  separator rows and repeated header rows, and each boost is listed several
  times across rarity sections. De-duplicated, there are **65 distinct named
  boosts**, all with identical values across their repeats. **Livewire Plus**,
  **Midnight**, **Mushroom**, and **Succession** were added later — the game
  keeps adding new boosts faster than the workbook does, so these were
  transcribed by hand from in-game screenshots (cross-checked against known
  boosts' icon shapes to decode their stat values), not sourced from either
  workbook version. The in-app **New Boost** form (Tools → Boosts) exists for
  the same reason: to add boosts as the game introduces them without waiting
  on a code update.
- **Track Stats are hand-transcribed, not from the workbook.** Neither
  workbook version has a per-circuit "which stat matters here" table — the 21
  tracks and their driver-stat/component-stat pairing (used by Loadouts → By
  Track) were transcribed directly from the in-game Track Stats screens.
- **"Boosted +10%" interpretation.** The workbook's *Data Input* sheet exposes a
  single global **Boost %** of `0.10` and a per-card **Boosted** boolean, i.e. a
  clean +10% "boosted slot" (distinct from the named consumable Boosts, which
  give flat bonuses). The toggle scales each of a card's positive stats and its
  Total / Team Score by +10% and rounds. **Pit Time is left unscaled** because
  it's a lower-is-better duration, not an additive stat — flagged here rather
  than guessed.
- **Loadouts are computed from your collection.** The workbook's *Suggested
  Loadouts* sheet is a large, formula-driven grid whose picks depend on the
  author's own owned components (mostly starter parts in the shared snapshot).
  Rather than embed those stale, author-specific values, the Tools → Loadouts
  view recomputes the best loadout **from your owned components** live for
  whichever attributes you toggle on — the same intent, kept live and useful
  as you level up.

Use **Export** to save a JSON backup and **Import** to restore it on another
device or after clearing browser data.

## Deploy to GitHub Pages

1. Commit all files to the repo **root**.
2. **Settings → Pages → Build and deployment → Deploy from a branch →
   `main` / `(root)`**.
3. Keep the **`.nojekyll`** file present so Pages serves paths verbatim
   (otherwise files/folders starting with `_` and some paths can be skipped).
4. The app uses **relative URLs** and registers the service worker with a
   relative path, so it works correctly under `https://<user>.github.io/<repo>/`.

> Private repos need **GitHub Pro** to publish Pages. Otherwise make the repo
> public, or host the folder on any static host (Netlify, Cloudflare Pages, an
> S3 bucket, etc.) — no server-side code is required.

## Cache-busting when you change a file

The service worker precaches the app for offline use. **Whenever you change any
cached file** (`index.html`, `sw.js`, `manifest.webmanifest`, or an icon),
bump the single version constant at the top of `sw.js`:

```js
const CACHE_VERSION = "f1sheet-v1";   // -> "f1sheet-v2", etc.
```

On the next visit the service worker installs the new cache and deletes the old
one, so users get the updated files instead of a stale copy.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app: markup + inline CSS + inline JS (with seed data). |
| `sw.js` | Service worker: precache + offline navigation fallback. |
| `manifest.webmanifest` | PWA manifest (standalone, icons, theme colors). |
| `icons/icon-192.png`, `icon-512.png` | App icons (512 also serves as maskable). |
| `icons/apple-touch-icon.png` | 180×180 icon for iOS home screen. |
| `.nojekyll` | Tells GitHub Pages to serve paths verbatim. |

## Credits

Card catalogue drawn from the community **F1 Clash 2026 Resource Sheet
v1.0**; per-level stats, costs, Series, boosts and reference tables from the
author's updated **v1.1** template — both by **TR The Flash**. Track Stats
data and the 4 most recently added Boosts are transcribed directly from
in-game screens, independent of either workbook version.
