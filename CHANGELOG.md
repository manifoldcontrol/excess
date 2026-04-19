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
# Pipeline Version History

## v12 — 2026-04-16 (current)

**Construction.** Gradient-boosted tree on three features:
- Raw distance from sector median margin
- Inverse sector MAD (additive dispersion control)
- Trailing four-quarter mean |ΔQ| (persistence control)

Sector median and sector MAD computed per quarter (no look-ahead).
Top 42 firms per quarter by score, maximum 6 per GICS sector.

**Performance (leakage-corrected OOS).**
- RR = 11.66× at k=0, 10.99× at k=1, 5.89× at k=2
- OOS AUC (+1Q forward) = 0.872
- Sector HHI = 1,160
- Production battery: 5/5 (leakage audit, rolling-window stability,
  calibration, feature-importance, hyperparameter sensitivity)
- GBM > linear logit in 5/5 rolling time-block windows

**Why v12.** Internal methodological review of v10 found three
failures: the 3.10σ threshold is not structural (RR(s) monotonic
in s); the linear combination underperforms out-of-sample; the
multiplicative z_Q = raw_dist/MAD form is misspecified. v11
validated the additive three-feature basis with a linear scorer;
v12 keeps that basis and replaces the linear scorer with a GBM,
recovering ~6 pp OOS AUC. v12 is the first construction in this
pipeline to match or exceed the strongest naïve benchmark
(DistNoMAD) on predictive RR while delivering a diversified flag.

**Data archive.** `data/v12/`, 18 quarterly CSVs,
CY2021Q3–CY2025Q4. Minimum-disclosure schema: ticker, quarter,
sector, v12_flag, raw_margin, delta_Q_abs, extreme_event. Score
and coefficients subscriber-only.

**Full methodology.** [manifoldcontrol.com](https://manifoldcontrol.com).

## v11 — 2026-04-16 (interim, not released to archive)

Linear logit on the three-feature basis. OOS AUC = 0.818, RR at
k=1 = 10.29× with sector cap. Superseded by v12 before any public
archive release. Retained as methodological milestone: v11
validated the feature basis and the sector-cap selection rule;
v12 upgraded the scorer.

## v10 — April 2026 (legacy)

**Construction.** Single-threshold cut on $z_Q = (Q −
\text{sector\_median}) / \text{sector\_MAD}$, winsorized at 95th
percentile. Danger threshold $s^* \approx 3.10\sigma$
macro-conditioned by IG credit spread ($\gamma = -3.44$).

**Performance.**
- RR = 4.3× at k=0, 4.1× at k=1, 2.4× at k=2
- OOS median RR = 4.35×
- Threshold IQR = 0.11 across 19 quarterly estimates
- 4/4 product battery (DW-1, DW-2, M1 IG-spread significance,
  threshold stability)

**Data archive.** `data/` (flat, at original location for backward
compatibility), 16 quarterly CSVs, CY2021Q1–CY2024Q4. Legacy
schema with `z_Q`, `s_star`, `above_threshold`.

**Paper.** Archived on Zenodo (DOI:
[10.5281/zenodo.19472014](https://doi.org/10.5281/zenodo.19472014)).

**Status.** Methodological concerns documented at
[manifoldcontrol.com](https://manifoldcontrol.com). The v10
empirical numbers are correct on their own terms; the "structural
threshold" framing was retracted after shape tests. The v10 data
archive remains public here for reproducibility but should not be
cited for current-state claims about the signal.
