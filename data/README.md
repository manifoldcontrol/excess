# The Excess — Historical Danger Signal Archive

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
