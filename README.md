# The Edge

A racing app with one rule, mined from every GB/IE runner of the season
(97,739 of them, walk-forward), and run as full perms on a rolling bank.

**https://jobsaboba.github.io/the-edge/**

## The rule

Everything is walk-forward — when a runner is judged, only the days *before*
it count:

- **race:** 2 miles 2 furlongs or farther (staying races)
- **field:** 9 runners or fewer
- **jockey:** has won 2+ times at today's course in the last 60 days (3+ rides)
- **trainer:** hot — 3+ wins at 25%+ strike in the last 14 days
- **cap:** max 4 picks a day, shortest prices first

## The money

£10 starting bank. The day's picks run as a **full perm** — every single,
every double, every treble up to the 4-fold — but never two horses from the
same race (they can't both win). Each line stakes **1% of the rolling bank**,
placed at its first leg's off, settled at its last. Win-only. Non-runners and
void races refund. When the bank's gone, the lines stop.

## The walk

Replayed over the whole season with those exact settings:

- 191 picks → 238 lines · 70 won · £120.00 staked → £172.30 returned
- **bank £10 → £62.30 · ROI +43.6%** · never below £9.27
- by fold: singles +40.3% · doubles +45.4% · trebles +67.5%
- 5-fold perms never landed all season — the perm stops at the 4-fold

Flat-stake, the same rule hits **+57.7%** (in-sample +46.4%,
out-of-sample Sep–Nov +93.7%).

## Where the edge comes from

| flat ROI (all runners) | −22% |
|---|---|
| staying races 2m2f+ | −8% |
| + jockey won at the course (60d) | +9.5% |
| + hot trainer (3 wins, 25%+, 14d) | +57.7% |
| big fields 14+ | −33% |
| class 1-3 vs class 6-7 | −9% vs −24% |

## How it runs

- `racing-scripts/the_edge.py` — the engine. Reads the full-racing store
  (`ult_store/`), replays the season day by day, publishes every day's races
  (odds + results, picks flagged), the perm lines, the bank and the season
  stats into `data/`.
- `racing-scripts/the_edge_mine.py` — the miner that found the rule.
- 06:50 cron: backfill the store, publish. `results-refresh.sh` settles
  results race by race through the afternoon and republishes.
- The site is a static viewer over `data/*.json` — no backend, installable,
  works offline once loaded.
