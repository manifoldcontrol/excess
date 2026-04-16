# The Excess: Historical Danger Signal Archive

Free historical output from The Excess v10 pipeline. Per-quarter CSVs
identifying S&P 1500 firms whose sector-normalized net margin exceeds
s* ≈ 3.1σ, macro-conditioned by IG credit spreads.

Firms above the threshold face 4.3× the base rate of extreme profit
events (concurrent), 4.1× at one-quarter lag, 2.4× at two-quarter lag.
The threshold moves: s*(m) = s₀ + γm, where γ = −3.44 and m is the IG
credit spread. When spreads widen, s* drops and more firms enter the
excess regime.

The signal predicts elevated profit *volatility*, not direction. Some
firms above s* will experience upside extremes. This is a variance
forecast, not a short signal, and not investment advice.

## Data

Per-quarter CSVs in `data/`. Coverage: CY2021Q1 through CY2024Q4 (16 quarters).

| Column | Type | Description |
|--------|------|-------------|
| `ticker` | string | Stock symbol |
| `quarter` | string | CY2024Q1 format |
| `sector` | string | GICS sector |
| `z_Q` | float | Sector-normalized net margin (MAD z-score) |
| `s_star` | float | Danger threshold for this quarter |
| `above_threshold` | 0/1 | Danger flag: z_Q > s* |
| `Q_raw` | float | Raw net profit margin |
| `delta_Q` | float | |Q[t] - Q[t-1]| |
| `extreme_event` | 0/1 | delta_Q > 90th percentile |

## Methodology

Full methodology: The Excess v10 Results (Kovalenko, April 2026).
Pipeline code and formal derivation at [manifoldcontrol.com](https://manifoldcontrol.com).

v10 product tests: 4/4 passed. DW-1 (4.3× RR), IG_spread (γ = −3.44,
ΔBIC = −952), DW-2 (OOS median RR = 4.35×), threshold stability
(IQR = 0.11 across 19 quarters).

## Current-quarter data

CY2025+ signal available via subscription at [manifoldcontrol.com](https://manifoldcontrol.com).

## Citation

```
Kovalenko, J. (2026). The Excess v10: EVT Danger Threshold in
S&P 1500 Profit Dynamics. Manifold Control. manifoldcontrol.com.
```

## License

Data: CC BY 4.0. Methodology: see paper.


## Methodology note

v10 is the currently published construction; its output remains reproducible from the archive. Internal review has identified refinements to the scoring function and to the threshold interpretation. These are under development and will be released as a follow-up publication. The results on this page are unchanged by the review.

## Open questions (under investigation)

**Implied vs. realized volatility on flagged names.** The 4.3× excess rate must survive adjustment for options-implied vol before long-volatility strategies extract edge.

**Directional asymmetry above s\*.** The downside vs. upside split of extreme events determines the value available to directional strategies beyond the variance forecast.

**Threshold interpretation.** Shape-based evidence for a discontinuity at s\* ≈ 3.1σ has not been produced; operational calibration on a heavy-tailed margin distribution is the alternative framing under evaluation.

**Scoring form.** The v10 scoring function is linear in features; comparison against more flexible scorers on the same feature set is in progress.

Release timing: next publication. No scheduled date.
