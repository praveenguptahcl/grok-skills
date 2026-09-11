---
name: quant-ui-generation
description: >
  Generate quant research UI in this TanStack Start app: tokens, tabbed desk
  chrome, Recharts recipes, metric strips, heatmap grids, dual-axis overlays.
  Use when creating or restyling trading/research dashboards. Triggers include
  "quant UI", "generate dashboard", "research chrome", "signal UI", "strategy UI",
  "tear sheet layout".
metadata:
  short-description: "Generate tokenized quant dashboards (Recharts, tabs, strips)"
user-invocable: true
---

# Quant UI generation

Compose `design-ui` + `stock-signal-charts` + `stock-strategy-ui`. This skill
is the **layout compiler** — not a second visual language.

Load: `references/recipes.md`.

## Shell

```
header: mark · title · SIMULATED · verdict · tabs
main: metric strip
      lab | primary chart | honesty
      secondary figures (2-col)
      table
```

Tabs wrap on 390px. Tap targets ≥ 36px (tab) / 44px (primary).

## Tokens (already in `src/styles.css`)

Use `bg-bg`, `bg-surface`, `text-fg`, `text-muted`, `text-subtle`,
`border-border`, `text-up`, `text-down`, `text-watch` / `text-weak` /
`text-reject`. No new hues. IBM Plex Sans + Mono.

## Chart recipe (copy)

- `ResponsiveContainer` height 220–280
- Grid: `stroke` at 8% fg, vertical false
- Tooltip: `bg-surface-2`, `rounded-xl`, 12px type
- Lines: 1.5–1.75px, no dots
- Dual axis: price left, z right; never scale z onto price

## Generation order

1. Tokens exist.
2. Pure engine returns series.
3. Panels consume series — no fetch.
4. Empty/loading: skeleton text, not blank.
5. Mobile stack: lab → charts → honesty → table.

## Do not generate

Purple gradients, emoji, gold "alpha" badges, TradingView embeds, live ticker
walls, fake order-book heatmaps without depth data.
