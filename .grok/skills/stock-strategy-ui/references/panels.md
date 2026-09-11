# Strategy panels

## Monthly heatmap

Bucket `portRet` by UTC YYYY-MM. Cell = `(1+r).prod() - 1`. Layout: years as
rows, Jan–Dec columns. Missing months = empty cell, not zero. Center color at 0.

Inspired by pyfolio monthly cones and Alpha Engine / CrossTide heatmaps, but
keep chroma to `--color-up` / `--color-down` only.

## Rolling OOS windows

`train=252`, `test=63`, `step=63` on the already-computed `portRet`. Each fold
Sharpe is `stats(test slice)`. Chart: bars. Caption: "Fixed rule, rolling
holdout — not a re-fit."

## Allocation

For each sampled t, plot `pos[i][t]` per ticker. Use a `Line` per name, not a
stacked 100% area (weights can be negative in long-short).
