# Overlay and heatmap

## Price + lagged z

Two Y axes. Price is a thin line (`--color-accent`). z is a muted line
(`--color-muted`). Tooltip: date, close, z. Switching ticker must not
recompute the whole book — slice overlay from the existing lagged matrix.

## Name × time heatmap

Rows = tickers (stable order). Columns = downsampled sessions. Cell color
maps z in [-2, 2] clipped. Include a 3-stop legend (−, 0, +).

Do not use TradingView heatmap widgets (blank, off-brand, network). Native
grid keeps the desk offline and tokenized.
