h# The Excess — Historical Danger Signal Archive

Free historical data from The Excess v10 pipeline: per-quarter identification
of S&P 1500 firms whose sector-normalized net margin exceeds the danger
threshold s* ≈ 3.1 standard deviations, macro-conditioned by IG credit spreads.

## What this is

A binary, per-quarter flag. Firms above the threshold are in a
structurally unstable region of profit-margin space. The empirical
finding: firms above s* face 4.3× the extreme-event risk concurrently,
4.1× at one-quarter lag, and 2.4× at two-quarter lag
(The Excess v10, April 2026).

The threshold moves with macroeconomic conditions: s*(m) = s₀ + γm,
where γ = −3.44 and m is the IG credit spread. When credit conditions
tighten, the threshold drops and more firms enter the excess region.

## What this is not

This is not a short signal. It is not investment advice. It is a
regime-boundary indicator derived from EVT excess-over-threshold theory.

The signal predicts elevated profit *volatility*, not direction.
Firms above s* are in a region where the conditional variance of profit
changes exhibits a structural jump. Some firms above the threshold will
experience upside extremes. The signal identifies the region, not the outcome.

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
Pipeline code and formal derivation available at [manifoldcontrol.com](https://manifoldcontrol.com).

v10 product tests: 4/4 passed — DW-1 (danger-window relative risk 4.3×),
IG_spread (macro conditioning, γ = −3.44, ΔBIC = −952),
DW-2 (out-of-sample median RR = 4.35×), threshold stability (IQR = 0.11).

## Current-quarter data

The CY2025+ danger signal is available via paid subscription.
Details at [manifoldcontrol.com](https://manifoldcontrol.com).

## Citation

```
Kovalenko, J. (2026). The Excess v10: EVT Danger Threshold in
S&P 1500 Profit Dynamics. Manifold Control. manifoldcontrol.com.
```

## License

Data: CC BY 4.0. Methodology: see paper.
# pf500-danger-signal
PF 500 Danger Signal — CMDP-based retention risk monitor for the S&amp;P 1500
