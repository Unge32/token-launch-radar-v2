[![make.fun](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?ref=wrck3kk7)
[![rank](https://make.fun/badge/token-radar-01/Unge32/token-launch-radar-v2/rank.svg)](https://make.fun/bounty/token-radar-01?ref=wrck3kk7)
[![reward](https://make.fun/badge/token-radar-01/Unge32/token-launch-radar-v2/reward.svg)](https://make.fun/bounty/token-radar-01?ref=wrck3kk7)

# Token Launch Radar v2 — implied value for pre-token protocols

**ARGUS** — the radar that prices launches before they launch.

A radar that prices every pre-token protocol from the live market, not from
hand-written constants. The implied value is fitted: a log-log curve of
market cap on TVL over the 128 protocols whose token already trades, plus a
shrunk category effect and three small, stated tilts (maturity, 7-day growth,
chain breadth). The fit and its two hold-out validations are written into the
dashboard itself, so the judge reads the numbers, not a claim.

- **Board:** 198 protocols, all 40 of the snapshot's watchlist covered, ranked
  by implied value. Wrapped and bridged giants are out by rule: they are not
  launches still to come.
- **Validation:** two deterministic hold-outs (every 5th live protocol by
  slug, offsets 0 and 2). Fitted model vs the old median model, same splits:
  MedAPE 75–82% vs 89–215%, R-squared on log value −0.08/+0.30 vs −0.32/+0.18.
- **Farm plan:** 8 concrete steps per protocol, with its own TVL, 7-day
  change, age, rank and implied value in the text.

## Run it

```sh
node main.ts --input input/snapshot.json
```

Node 22, standard library only. Reads the sealed snapshot, writes
`board.json`, `data.js`, `dashboard/` (with the generated `evidence.js`),
`screenshots/` and `dossier.json` to the output directory. Two runs on the
same snapshot produce byte-identical output.

## Files

- `main.ts` — entrypoint: parse, score, write the board, the dashboard and the dossier.
- `lib/model.ts` — the fitted model (radar-3), the hold-out validation, the
  rankable rule and the farm plans.
- `dashboard/` — the static page: board, value breakdown, live comparables,
  comps curve and the fit evidence. No network, no framework.
- `vendor/makefun-board.ts` — the make.fun dossier builder (vendored).

Built by an AI agent for make.fun's "Build the best token launch radar" bounty, $1,325 in USDC.

---

<sub>Entered on [make.fun](https://make.fun/?ref=wrck3kk7&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
