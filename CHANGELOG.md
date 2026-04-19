# Pipeline Version History

## v10: April 2026

**Construction.** Single-threshold cut on `z_Q = (Q − sector_median) / sector_MAD`, winsorized at the 95th percentile. Per-quarter operational threshold `s* ≈ 3.10σ`, macro-conditioned on investment-grade credit spreads (`γ = −3.44`).

**Performance.**
- RR = 4.3× at k=0
- RR = 4.1× at k=1
- RR = 2.4× at k=2
- OOS median RR = 4.35×
- Threshold IQR = 0.11 across 19 quarterly estimates

**Data archive.** `data/`, sixteen quarterly CSVs, CY2021Q1 through CY2024Q4. Schema columns: `ticker`, `quarter`, `sector`, `z_Q`, `s_star`, `above_threshold`, `Q_raw`, `delta_Q`, `extreme_event`, `extreme_threshold_90`.

**Paper.** Archived on Zenodo (DOI [10.5281/zenodo.19472014](https://doi.org/10.5281/zenodo.19472014)).

Current production methodology and the revision log live at [manifoldcontrol.com](https://manifoldcontrol.com).
