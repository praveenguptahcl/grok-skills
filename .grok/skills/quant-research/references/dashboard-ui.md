# Quant dashboard UI

Follow `design-ui`. Extra rules for research desks:

## Layout

```
┌ header: product · SIMULATED · verdict chip ──────────────┐
│ metric strip (6 tabular KPIs)                            │
├ lab (narrow) ┼ equity + underwater ┼ honesty panel      │
├ universe table ──────────────────────────────────────────┤
```

On ~390px: header, verdict, metrics 2×3, lab, charts, table.

## Visual language

- Near-black field, hairline borders, one ice/steel accent
- Green/red **only** on PnL deltas and verdict chips — never on panels
- IBM Plex Sans + IBM Plex Mono (or equivalent display + mono). Not Inter-only.
- No candlestick clipart, no gold, no purple, no emoji

## Copy

- Header badge: `SIMULATED UNIVERSE`
- Honesty panel title: `Do not claim an edge`
- Verdict words: `REJECT` / `WEAK` / `WATCH` — never `PROFITABLE` / `ALPHA`

## Charts

Recharts. Equity as a step-ish monotone line; drawdown as an area in muted
danger. Tooltip shows date + equity + dd. Empty state if lookback > sample.

## Controls

Lookback, holding, cost bps, long-short. Changing a control recomputes
synchronously (universe is small). Save-to-notebook is explicit, not on every
keystroke.
