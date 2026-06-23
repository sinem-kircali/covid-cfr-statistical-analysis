# COVID-19 CFR: Daily vs Cumulative Case Fatality Rate Analysis

Statistical comparison of daily and cumulative Case Fatality Rates (CFR) across two pandemic periods — testing whether the two measures differ significantly and how CFR evolved over time.

## What is CFR and why does the measurement method matter?

- **Daily CFR** = new deaths / new cases on a given day — captures immediate lethality but is noisy
- **Cumulative CFR** = total deaths / total cases — smoother but lags behind real trends

The two measures diverge systematically during epidemic growth or decline phases, making the choice of metric consequential for policy decisions.

## Methods

- Computed daily and cumulative CFR for two distinct pandemic periods
- Confidence intervals for the difference in population means (large-sample z-interval at α = 0.01, 0.05, 0.10)
- Q-Q plots and normality diagnostics (chi-squared goodness-of-fit) for both CFR distributions

## Tech Stack
- Python 3
- `numpy` · `scipy` · `statsmodels` · `pandas` · `matplotlib`

## Data
Two-period COVID-19 dataset with daily new cases, new deaths, total cases, and total deaths — not included. Place your CSV/Excel files in the working directory and update the filenames in the notebook.
