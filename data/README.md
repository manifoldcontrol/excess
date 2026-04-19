# The Excess: v10 Reference Archive

Historical output from The Excess v10 pipeline. Per-quarter CSVs covering CY2021Q1 through CY2024Q4, a total of sixteen quarters.

Each quarter flags S&P 1500 firms whose sector-normalized net margin sits above a per-quarter operational threshold. The threshold is macro-conditioned on investment-grade credit spreads: `s*(m) = s₀ + γm` with γ = −3.44.

Flagged firms carry elevated probability of extreme profit-margin events at the concurrent quarter (4.3× relative to base rate), at one-quarter lag (4.1×), and at two-quarter lag (2.4×). The signal identifies the heavy tail of a sector-normalized margin distribution where variance is elevated.

## Schema

Per-quarter CSVs under `data/`.

| Column | Type | Description |
|--------|------|-------------|
| `ticker` | string | Stock symbol |
| `quarter` | string | `CY2024Q1` format |
| `sector` | string | GICS sector |
| `z_Q` | float | Sector-normalized net margin (MAD z-score) |
| `s_star` | float | Per-quarter operational threshold |
| `above_threshold` | 0/1 | Flag: `z_Q` above `s_star` |
| `Q_raw` | float | Raw net profit margin |
| `delta_Q` | float | `|Q[t] - Q[t-1]|` |
| `extreme_event` | 0/1 | `delta_Q` above the 90th percentile |

## Methodology

Full methodology for v10: the Zenodo record (DOI [10.5281/zenodo.19472014](https://doi.org/10.5281/zenodo.19472014)).

Current production methodology and the full revision log live at [manifoldcontrol.com](https://manifoldcontrol.com).

## Citation

```
Kovalenko, J. (2026). The Excess v10: S&P 1500 Reference Archive.
Manifold Control. https://github.com/manifoldcontrol/excess
```

## License

Data: CC BY 4.0.
