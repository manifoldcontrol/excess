# The Excess: Public Reference Archive

Historical output from The Excess v10 pipeline. Per-quarter CSVs flagging S&P 1500 firms in the heavy right tail of sector-normalized profit-margin space. Flagged firms carry elevated probability of extreme margin events in the current quarter and the next.

## What this repository contains

Sixteen quarterly CSVs covering CY2021Q1 through CY2024Q4. Per-quarter selection applies a single-threshold cut on sector-normalized margin distance, macro-conditioned on investment-grade credit spreads.

v10 performance:

| Metric | v10 |
|---|---|
| RR at k=0 (concurrent) | 4.3× |
| RR at k=1 (one quarter forward) | 4.1× |
| RR at k=2 (two quarters forward) | 2.4× |
| OOS median RR | 4.35× |
| Threshold IQR (19 quarters) | 0.11 |

Methodology and formal derivation are in the v10 record on Zenodo: DOI [10.5281/zenodo.19472014](https://doi.org/10.5281/zenodo.19472014).

Current production methodology and licensing live at [manifoldcontrol.com](https://manifoldcontrol.com).

## Repository layout

```
excess/
├── README.md         this file
├── CHANGELOG.md      pipeline version history
└── data/             v10 archive (16 CSVs, CY2021Q1 through CY2024Q4)
```

## CSV schema

Each row is a firm-quarter observation.

| Column | Type | Description |
|---|---|---|
| `ticker` | string | Stock symbol |
| `quarter` | string | `CY2024Q1` format |
| `sector` | string | GICS sector |
| `z_Q` | float | Sector-normalized margin z-score |
| `s_star` | float | Operational threshold for the quarter |
| `above_threshold` | 0/1 | Flag |
| `Q_raw` | float | Net profit margin (NI / revenue) |
| `delta_Q` | float | Q[t] minus Q[t-1] |
| `extreme_event` | 0/1 | `|delta_Q|` above the 90th percentile in this quarter |
| `extreme_threshold_90` | float | 90th-percentile cutoff |

## Verification protocol

1. Pick any CSV from `data/`.
2. Partition firms by `above_threshold`.
3. In each group, compute the fraction with `extreme_event == 1`.
4. The ratio of fractions is the empirical risk ratio at the concurrent horizon.
5. Track each flagged firm across subsequent CSVs to verify lag-k persistence.

Everything is reproducible from the public columns in a spreadsheet.

## Current production signal and licensing

Current methodology, validation, and institutional licensing: [manifoldcontrol.com](https://manifoldcontrol.com). Commercial contact: `james@manifoldcontrol.com`.

## Citation

```
Kovalenko, J. (2026). The Excess: S&P 1500 Public Reference Archive
[Data set]. Manifold Control.
https://github.com/manifoldcontrol/excess
```

For v10 methodology, cite the Zenodo record (DOI: 10.5281/zenodo.19472014).

## License

Data: CC BY 4.0. The v10 Zenodo record carries its own license on Zenodo. Methodology documentation at [manifoldcontrol.com](https://manifoldcontrol.com) is copyright Manifold Control.
