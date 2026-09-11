# Signals and strategy mapping

## Families (implement these first)

| Id | Formula (all trailing, then lag) | Bias |
| --- | --- | --- |
| `mom` | Close / close[lookback] − 1, z-scored in time | Trend |
| `mr` | −(close / sma(lookback) − 1), z-scored | Reversion |
| `volsurprise` | volume / median(volume, lookback) − 1 | Attention |
| `breakout` | (close − max(high, lookback)) / atr | Continuation |
| `gapfade` | −(open/prevClose − 1) when \|gap\| > k·atr | Fade |
| `xs_mom` | Cross-sectional rank of `mom` mapped to −1…1 | LS book |

Cross-sectional ranks beat raw z when the book is the product.

## Position map

- **Long-short:** rank signals across names each day → affine map to `[−1, 1]`,
  dollar-neutral-ish (weights sum ~ 0).
- **Long-only:** `max(0, tanh(z))`, then L1-normalize to 1.

Clip gross leverage to 1 unless the user asks otherwise.

## Costs

`cost = (costBps / 1e4) * Σ |pos_i,t − pos_i,t−1|`

One-way. Equity is `cumprod(1 + r_net)` starting at 1.

## Holding

If holding `H > 1`, do not peek. Recompute signal every `H` days and hold
positions constant in between (still charged when they change).
