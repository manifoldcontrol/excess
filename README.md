# The Excess — S&P 1500 Danger Signal Archive

Free historical output from The Excess pipeline. Per-quarter CSVs
identifying S&P 1500 firms in the danger cohort: sector-relative
margin extremity, sector-dispersion adjusted, with trailing margin
volatility control.

Flagged firms face elevated risk of extreme profit events. The
signal forecasts *variance*, not direction; this is not investment
advice.

## Current version: v12 (April 2026)

Construction: three-feature basis (raw distance from sector median,
inverse sector MAD, trailing four-quarter mean |ΔQ|) scored by a
gradient-boosted tree. Selection: top 42 firms per quarter by score,
maximum 6 per GICS sector.

**Empirical claims (verifiable from data below):**

| Metric | v12 | v10 predecessor |
|---|---|---|
| RR at k=0 (concurrent) | 11.66× | 4.3× |
| RR at k=1 (one quarter forward) | 10.99× | 4.1× |
| RR at k=2 (two quarters forward) | 5.89× | 2.4× |
| Sector HHI | 1,160 | 1,432 |
| OOS AUC (+1Q) | 0.872 | 0.773 |

The v10 paper claimed a *structural* danger threshold at s* ≈ 3.1σ.
Internal review showed RR(s) is monotonically increasing in s with
no shape-based feature at 3.10; the threshold was operational, not
structural. v12 replaces the single-threshold cut with a scored,
sector-capped flag on a validated feature basis. See
[manifoldcontrol.com](https://manifoldcontrol.com) for current
methodology and the full revision log.

## Repository layout

```
excess/
├── README.md                  this file
├── CHANGELOG.md               pipeline version history (v10 → v11 → v12)
├── data/                      v10 archive (16 CSVs, CY2021Q1–CY2024Q4)
└── data/v12/                  v12 archive (18 CSVs, CY2021Q3–CY2025Q4)
```

This repository hosts signal output only. Methodology is on
[manifoldcontrol.com](https://manifoldcontrol.com); the archival
v10 paper is on Zenodo (DOI:
[10.5281/zenodo.19472014](https://doi.org/10.5281/zenodo.19472014)).

v10 CSVs remain at their original flat `data/` path for backward
compatibility with consumers that hardcoded the old location.
v12 CSVs live at `data/v12/`.

## v12 CSV schema

Minimum-disclosure schema (no score, no features, no coefficients):

| Column | Type | Description |
|---|---|---|
| `ticker` | string | Stock symbol |
| `quarter` | string | `CY2024Q1` format |
| `sector` | string | GICS sector |
| `v12_flag` | 0/1 | Top-42 with max 6/sector at v12 score |
| `raw_margin` | float | Net profit margin (NI / revenue) |
| `delta_Q_abs` | float | \|Q[t] − Q[t−1]\| |
| `extreme_event` | 0/1 | `delta_Q_abs` > 90th percentile in this quarter |

Fitted coefficients and the v12 score itself are subscriber-only.
RR, persistence, and sector HHI are all verifiable from the flag
and extreme_event columns.

## v10 CSV schema (legacy)

v10 CSVs in `data/` retain the original schema (ticker, quarter,
sector, z_Q, s_star, above_threshold, Q_raw, delta_Q, extreme_event,
extreme_threshold_90). v10 methodology is archived on Zenodo (DOI:
[10.5281/zenodo.19472014](https://doi.org/10.5281/zenodo.19472014));
its "structural threshold" framing has since been retracted, see
the CHANGELOG for the revision history.

## Verification protocol

1. Pick a v12 CSV (e.g., `data/v12/danger_signal_v12_CY2024Q3.csv`).
2. Partition firms into `v12_flag == 1` (flagged) and `v12_flag == 0`
   (not flagged).
3. In each group, compute the fraction with `extreme_event == 1`.
4. Ratio of fractions is the empirical RR at k=0 for that quarter.
5. To verify forward persistence (k=1, k=2), track each flagged
   firm's `extreme_event` in the next 1–2 quarters using the next
   CSV(s) and take the same ratio.

No proprietary software or pipeline access is required. Everything
is reproducible from the public columns in a spreadsheet.

## Current-quarter data

Live v12 signal (current quarter) and fitted scorer:
[api.manifoldcontrol.com](https://api.manifoldcontrol.com).
Institutional licensing: `james@nurho.tech`.

## Citation

Data archive:

```
Kovalenko, J. (2026). The Excess: S&P 1500 Danger Signal Archive
[Data set]. Manifold Control.
https://github.com/manifoldcontrol/excess
```

For v10 methodology, cite the Zenodo record
(DOI: 10.5281/zenodo.19472014). v12 methodology is documented at
[manifoldcontrol.com](https://manifoldcontrol.com).

## License

Data: CC BY 4.0. The v10 paper (Zenodo record 19472014) carries its
own license on Zenodo. Methodology documentation on
[manifoldcontrol.com](https://manifoldcontrol.com) is
copyright Manifold Control.
