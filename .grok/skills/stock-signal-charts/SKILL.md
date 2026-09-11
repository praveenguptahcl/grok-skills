---
name: stock-signal-charts
description: >
  Render stock factor/signal graphs: lagged z overlay on price, daily IC bars,
  rolling IC, quantile spreads, name×time heatmaps, and IC lag-decay. Use when
  the user wants signal viewing, factor tear sheets, IC charts, heatmaps, or
  "show the signal on the stock". Triggers include "signal chart", "IC plot",
  "factor heatmap", "overlay signal", "alphalens", "tear sheet", "lag decay".
metadata:
  short-description: "Alphalens-style signal graphs: IC, overlay, heatmap, decay"
user-invocable: true
---

# Stock signal graph viewing

A signal is not a line on a marketing chart. View **the lagged scalar** against
**next-bar returns**. Copy the Quantopian Alphalens figure set into this stack
(Recharts + CSS grid), not matplotlib.

Load: `references/figure-set.md`, `references/overlay-and-heat.md`.
Sources: `references/SOURCES.md`.

Pair with `quant-research` (math/honesty) and `design-ui` (chrome). Do not
invent live broker candles unless the user supplied data — this workspace
simulates.

## Required figure set (ship all)

| Panel | What | Honest caption |
| --- | --- | --- |
| IC series | Daily Spearman(signal_t, fwd_ret_{t+1}) as signed bars + 21d mean | Zero line; OOS region marked |
| Lag decay | Mean IC at horizons 1, 2, 3, 5, 10 | If h=1 is the only bump, say so |
| Price + z | Close (left) and lagged z (right) for one ticker | Dual axis; z is **lagged** |
| Name heatmap | Sampled z, names × time | Diverging, center 0, no rainbow |
| Quantile paths | Hi vs lo tercile equity of the signal | Spread is the book, not a promise |

Optional later: monthly IC heatmap (Alphalens `plot_monthly_ic_heatmap`).

## Implementation (this app)

- Compute views inside the same pure `runBacktest` so sliders stay in sync.
- Downsample heat/overlay (every 4–8 bars) so Recharts stays smooth.
- Tickers selectable; default first name. Persist selection in Zustand memory only.
- Recharts `Bar` for IC (positive `text-up`, negative `text-down` via Cell).
- Heatmap: CSS grid of `div`s, not a chart library. Color with
  `color-mix` between `--color-down` / surface / `--color-up`.
- Never plot unlagged z vs same-bar return.

## Anti-patterns

- Candlestick clip-art with unexplained arrows
- Heatmaps that use purple-gold palettes
- Overlaying raw (unlagged) oscillator on close and calling it alpha
- Hiding the zero line on IC
