# token-launch-radar

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/tiarnoap05/token-launch-radar/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/tiarnoap05/token-launch-radar/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

Token Radar ranks every protocol that records no token in a sealed DefiLlama snapshot by an implied value calibrated from the snapshot's own live protocols: the median market-cap-to-TVL ratio, per category where the category holds enough live protocols, else the global median, adjusted for seven-day growth and for how long the protocol has run with no token. The board covers all 40 watchlist protocols plus every rankable pre-token protocol below the $50M floor, and each row carries a concrete farm plan with costs and times. The dashboard is a static, offline page: sortable, filterable, with a detail view per protocol and the full calibration table.

## Run it

Requires Node.js 22.18+ (standard library only, nothing to install).

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input path/to/snapshot.json
```

The program writes `board.json`, `data.js`, `dashboard/`, `screenshots/` and `dossier.json` to the output directory.

## How it works

- `lib/model.ts` — the radar-2 model: `calibrateMultiples` (the median market-cap-to-TVL ratio of the snapshot's live, non-CEX protocols), `impliedValue` (TVL x multiple x growth x maturity), `buildBoard` (all 40 watchlist rows plus every rankable early row, no cap), and `farmSteps` (six costed, timed steps derived from each protocol's own category, chains, TVL and age).
- `main.ts` — reads the snapshot, scores the board, writes the outputs and the dossier with the vendored make.fun library.
- `dashboard/` — the static page: `index.html`, `app.css`, `app.js`. It recomputes every row's implied value in `impliedOf` and shows the calibration table, so the page and the board are visibly the same arithmetic.
- `screenshots/` — the board, a detail view and a filtered view, captured from the dashboard.

Implied values are this entry's own model, never a price and never a claim make.fun makes. A protocol is shown as recording no token when its DefiLlama record carries no market cap, CoinGecko id or symbol; that record is not proof it has none.

---

<sub>Entered on [make.fun](https://make.fun/?ref=310ssgcx&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
