---
name: quant-research
description: >
  Build quant research tools: alpha discovery, factor/signal construction,
  strategy backtests, and honest research dashboards. Use when the user wants
  a trading research desk, signal lab, factor explorer, Sharpe/IC analytics,
  walk-forward tests, or a strategy notebook. Triggers include "quant",
  "alpha", "signal", "factor", "backtest", "Sharpe", "information coefficient",
  "walk-forward", "strategy dashboard", "alpha discovery", "statistical honesty".
metadata:
  short-description: "Alpha discovery, lagged signals, honest backtests, research dashboards"
user-invocable: true
---

# Quant research — alpha discovery & strategy dashboards

Ship a **research desk**, not a marketing PnL chart. Every signal is lagged.
Every claim is split in-sample vs out-of-sample. Simulated data is labeled as
simulated. A pretty equity curve without IC, turnover, and a reject rule is
incomplete.

**Also load (do not skip):**

| Need | Skill |
| --- | --- |
| IC / overlay / heatmap graphs | `stock-signal-charts` |
| Strategy path, monthly grid, rolling OOS | `stock-strategy-ui` |
| How to generate the chrome | `quant-ui-generation` |
| Visual tokens, anti-slop | `design-ui` |

Read on demand:

- `references/statistical-honesty.md`
- `references/alpha-discovery.md`
- `references/signal-strategy.md`
- `references/dashboard-ui.md`

Stack: TanStack Start, Zustand + `localStorage` (runs only), Recharts,
tokens in `src/styles.css`. Auth/db off unless accounts were asked.

## Non-negotiables

1. **No look-ahead.** `pnl[t+1] = pos[t] * ret[t+1]` with `pos` from lagged z.
2. **Costs on.** Default 5 bps one-way.
3. **IS / OOS always.** 70/30 chronological. Verdict from OOS.
4. **Verdict words:** `REJECT` / `WEAK` / `WATCH` only.
5. **Label simulated universes.**
6. **Tabular nums** on metrics.
7. **Signal graphs + strategy graphs are not optional** on a desk product —
   Discover-only equity is incomplete (see the two chart skills).

## Default product: Signal Desk

| Mode | Job |
| --- | --- |
| Discover | Params + net equity + honesty + book |
| Signals | IC series, lag decay, price+z overlay, heatmap, quantiles |
| Strategy | Monthly heatmap, rolling OOS windows, weights |
| Notebook | Persist experiments |
| Playbook | Rules |

## Anti-patterns

Unlagged plots, IS-only Sharpe, zero-cost hero numbers, live-feed language,
rainbow chrome, "walk-forward optimized" on a fixed rule.
