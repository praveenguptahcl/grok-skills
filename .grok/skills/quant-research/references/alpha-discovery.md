# Alpha discovery pipeline

## Loop

1. **Universe** — seeded synthetic bars unless the user brings data.
2. **Hypothesis** — one sentence ("5-day residual mean-reverts after costs").
3. **Signal** — scalar per name per day, then lag 1.
4. **Portfolio** — map signal → position (signed rank or clip).
5. **Path** — next-bar return minus cost × |Δpos|.
6. **Split** — chronological IS / OOS (and optional walk-forward folds).
7. **Verdict** — honesty rules. Save the run. Do not re-tune on OOS.

## Metrics to compute (minimum)

| Metric | Definition |
| --- | --- |
| Sharpe | `mean(r)/std(r) * sqrt(252)` on **net** daily portfolio returns |
| Sortino | Downside deviation of negative days only |
| Max DD | Peak-to-trough on equity |
| Calmar | Ann. return / \|max DD\| |
| Hit rate | P(daily pnl > 0) |
| Turnover | Mean of 0.5 * Σ\|Δpos\| per day, annualized × 252 |
| IC | Spearman(signal_t, fwd_ret_{t+1}) per day, then mean / t |
| IR | mean(IC) / std(IC) * sqrt(252) |
| PSR | Bailey probabilistic Sharpe vs 0 (per-period SR, skew, kurtosis) |

## Planted structure (for demos)

Synthetic markets should include **weak, decaying** structure so a mean-reversion
or momentum knob can sometimes pass IS and fail OOS. Do not plant an obvious
constant drift that every long-only signal harvests. Mix:

- GBM + regime vol
- A slow mean-reverting residual on a subset of names
- Occasional gap days

The desk exists to **reject** as often as it watches.

## Walk-forward (optional fold)

Expanding or rolling: train 252d, test 63d, step 63d. Report the distribution
of OOS Sharpes, not the best fold.
