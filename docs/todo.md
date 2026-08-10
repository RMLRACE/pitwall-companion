# todo.md — pitwall-companion

Task list for this repo. Update after every completed task; one task = one
commit. Items scoped inside this project live here, not in the hub's
`docs/todo.md` — per the hub-and-spoke rule, a project's own todo is
authoritative for its own work.

## Open

- [ ] **Confirm the real level cap for Special (Paddock Picks) cards.**
      `CAP.Special` is **7**, chosen to mirror Legendary (the nearest
      analogue: premium, no Series, mostly Champion-tier). No Paddock Picks
      card's actual cap has ever been observed, so cards-to-max on all 16
      rests on that assumption. One card's upgrade view settles it; it is a
      one-line change in `index.html`. Flagged in the code comment on `CAP`
      and in README's "Partial data" section. (raised 2026-08-10)

- [ ] **Fill in the Special level curve above level 1.** The 16 Paddock
      Picks cards carry level-1 stats only — that is all a locked card's
      compare view shows. No stats above level 1, no coin costs (`cu`/`ct`
      are deliberately empty so the app reports "unknown" rather than 0),
      and no Asset Trade rate (`TRADE.Special` is 0). Needs an owned,
      upgraded Special card to extend. (raised 2026-08-10)

- [ ] **Let a new user bring in their own workbook data.** Import today accepts
      only the app's own backup JSON — an `.xlsx`, a CSV, or workbook-shaped
      JSON is rejected — so a new user's only route is typing 151 cards in by
      hand. Two candidate routes, to be explored in a later session: a CSV
      upload with a column-mapping + name-matching step (the workbook uses full
      names, the app uses surnames with `G.Villeneuve`-style disambiguation), or
      a one-off converter script in this repo that emits backup JSON the
      existing Import already accepts. The converter is the smaller change and
      adds no new failure modes to the app. (raised 2026-08-10)

- [ ] **Watch the schema 1 → 2 migration on a real install.** Zeroing the
      seed made every pre-existing install depend on `migrateLegacySeed()`
      writing `LEGACY_SEED` back as real overrides on first load. It is
      verified card-by-card across all 151 in a harness — including an
      explicitly-zeroed card, a re-load no-op, a fresh install and an
      unknown future schema, and end-to-end through the real Import handler —
      but has not yet run against real `localStorage` on a device that holds a
      real collection. The first load after v19 (or whichever build the device
      picks up first) is the moment to check. (raised 2026-08-10)

## Done

- [x] Fix the Season tab scoring nothing a real collection had done. The four
      asset metrics were hand-typed numbers in `SEASON_KEY`, never once written
      from the collection in `f1sheet.v1` — so a fully played account sat at
      0 / 0% forever and the four zeros held Base Asset Progress under 60% no
      matter what. Their stored targets were stale too, from the v1.0 workbook:
      Drivers 66 of an actual 105, Parts **53 of only 46**, a bar that could
      never reach 100%. All four are now counted live by `collectionCounts()`
      (cards at level 1+, and level-ups banked out of the rarity caps), so they
      track the collection and take in custom cards on their own; the rows are
      read-only and the four stored keys are gone from `SEASON_DEFAULT`. Old
      payloads just carry the dead keys, so no schema bump. Verified end-to-end
      in a real browser: levelling a driver moves the Season bars and survives a
      reload. (2026-08-10)

- [x] Add the Paddock Picks and Paddock Picks: Turbo collections (16
      "Special" cards) and Johnny Herbert as the 23rd Legendary; introduce
      per-card GP Event availability badges — PR #23 (2026-08-10)
- [x] Correct the Special stats from "max level" to level 1 (a locked
      card's *Stats at Max Level* chip is an un-pressed toggle, not a label
      for the numbers below it — verified against Senna, whose locked card
      resolves to exactly his level-1 row in the sheet), and derive
      Herbert's full level 1–7 curve from his stat cohort — PR #23
      (2026-08-10)
- [x] Start new installs at level 0 across all 151 cards and reset the
      Season dashboard to a beginner state, with a schema 1 → 2 migration
      so existing installs keep everything they had — PR #24 (2026-08-10)
- [x] Fix Import bypassing the schema 1 → 2 migration. `load()` migrated old
      payloads but the Import handler did not, so restoring a backup exported
      before the level-0 change silently reset 73 of 74 cards — every one the
      user had not explicitly edited. Import now takes the same path as
      `load()`, and only a genuinely unrecognised schema prompts. Covered by an
      end-to-end test driving the real file input, verified to fail against the
      pre-fix code — PR #26 (2026-08-10)
- [x] Read GP Event availability off the in-game cards for all 23
      Legendary drivers (4 Junior+ / 5 Challenger+ / 6 Contender+ /
      8 Champion). Tier rises monotonically with level-1 total and no power
      cohort spans two tiers; both are asserted. The "Legendary drivers
      allowed" toggle is now inert and kept only as the fallback for a
      Legendary added before its card has been read — PR #24 (2026-08-10)
