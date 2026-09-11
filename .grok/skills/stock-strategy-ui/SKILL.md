---
name: stock-strategy-ui
description: >
  Build stock strategy dashboards: net equity vs underwater, monthly return
  heatmap, rolling OOS windows, allocation over time, and a blotter of last
  weights. Use for strategy testers, walk-forward views, portfolio paths.
  Triggers include "strategy dashboard", "walk-forward", "monthly heatmap",
  "allocation", "blotter", "strategy UI", "pyfolio", "tearsheet".
metadata:
  short-description: "Strategy desk UI: equity, monthly grid, rolling OOS, weights"
user-invocable: true
---

# Stock strategy UI

The strategy tab is the **portfolio path** of the current rule, not a second
backtester. Same lagged positions, same costs as Discover.

Load: `references/panels.md`. Sources: `references/SOURCES.md`.
Honesty: `quant-research/references/statistical-honesty.md`.

## Required panels

| Panel | Spec |
| --- | --- |
| Equity + DD | Already on Discover; repeat compactly or skip if visible |
| Monthly heatmap | Calendar grid of net month returns, diverging color, tabular % |
| Rolling windows | Fixed rule, 252d then 63d blocks, Sharpe per block — label **not** "re-optimized WFA" |
| Weights | Downsampled stack of name weights (area or small multiples) |
| Book snapshot | Last-bar weights — reuse universe table |

## Rules

- Costs stay on. Zero-cost ghost line is optional and muted.
- Rolling windows use the **same** signal parameters. Do not grid-search inside
  a window and then report the winner.
- IBM Plex Mono on every % and Sharpe.
- Verdict chip stays global (OOS of the 70/30 split), not the best fold.

## Anti-patterns

- Calling rolling windows "walk-forward optimization"
- Monthly grid without a color legend
- Strategy tab that uses a different cost model than Discover
