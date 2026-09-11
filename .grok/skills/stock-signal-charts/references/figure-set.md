# Figure set (Alphalens → web)

Alphalens `create_full_tear_sheet` groups: Returns, Information Coefficient,
Turnover, Grouped. For a browser desk, compress to five panels that still
answer: *does the lagged signal rank next returns?*

## IC series

Daily IC can be noisy with N=8 names. Always overlay a 21-session mean and a
horizontal 0. Color bars by sign. Shade OOS.

Vibe-Trading (HKUDS, 2026) factor tab: IC bars + mean line + quantile equity +
IC correlation. We skip correlation until ≥3 saved factors exist.

## Lag decay

Mean IC(h) for h in {1,2,3,5,10} using `spearman(z_t, r_{t+h})`.
A real short-horizon factor decays. A look-ahead bug **peaks at h=0** — we do
not plot h=0.

## Quantiles

Each day, rank names by lagged z into terciles. Equal-weight the next return
of the top vs bottom tercile, accumulate from 1. Label "Hi tercile" / "Lo
tercile", not "alpha long/short product".
