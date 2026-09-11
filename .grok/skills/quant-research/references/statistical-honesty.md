# Statistical honesty

This is the skill's spine. Pretty charts without these rules are toys.

## Claims you may make

- "In this simulated universe, lagged signal X had OOS Sharpe Y after Z bps."
- "IS and OOS disagree" (the useful sentence).
- "PSR vs 0 is P — under Gaussian-ish returns, this is / is not distinguishable from luck."

## Claims you must not make

- "This is an edge." / "Prints money." / "Live alpha."
- Any implication the path is a real ticker unless the user supplied real data.
- Significance from IS Sharpe, from one asset, or after unlogged parameter search.

## Default reject rule (encode in the UI)

A run is **WATCH** only if all hold on the **out-of-sample** slice:

- OOS Sharpe ≥ 0.6 (annualized)
- Mean IC t-stat ≥ 2.0
- PSR(SR* = 0) ≥ 0.95
- Annualized turnover not insane relative to gross (flag if turnover > 50 and Sharpe < 1)

Else **WEAK** if OOS Sharpe > 0 and IC t-stat > 1.0.

Else **REJECT**.

Never let IS Sharpe upgrade a REJECT.

## Multiple testing

Each saved notebook run is a trial. Haircut:

```
PSR* uses SR* = 0
If N trials > 1, show: "N experiments in the notebook — expect false positives."
```

Do not invent a Nobel. A simple trial counter plus PSR is enough for a desk MVP.

## Costs and capacity

Zero-cost Sharpe is a diagnostic, not a result. The displayed headline metrics
must include the user-set cost. Show a ghost zero-cost Sharpe in muted type
if you want, never as the hero number.

## Look-ahead checklist (code review)

- Rolling mean/std at `t` uses `slice(t-L, t)` exclusive of future
- Cross-sectional ranks at `t` use only that bar's known fields
- Gap signals use overnight that is known at open, applied to remaining session
  or next close — pick one, document it, don't mix
- Volume surprise uses a trailing median, not a centered window
