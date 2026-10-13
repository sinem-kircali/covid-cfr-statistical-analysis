# COVID-19 Case Fatality Rate in Germany: Daily vs Cumulative CFR Across Two Waves

How lethal was COVID-19 in Germany in the first and second waves, and how much does the answer depend on how the case fatality rate (CFR) is measured? This notebook compares the **daily** and the **cumulative** CFR in each wave. It estimates confidence intervals and tests the difference between the waves, checking each statistical assumption along the way.

Built for the *Applied Statistics* course (Industrial Engineering, Koç University).

## Measures
Both measures match deaths on day t with cases reported **15 days earlier**, roughly the time from diagnosis to death.
- **Daily CFR** = new deaths(t) ÷ new cases(t − 15). It reacts immediately but is noisy.
- **Cumulative CFR** = total deaths(t) ÷ total cases(t − 15). It is smooth but slow, and dominated by the past.

## Key results
| | Wave 1 (31 Mar – 13 Jul 2020) | Wave 2 (5 Nov 2020 – 4 Feb 2021) |
|---|---|---|
| Mean daily CFR (95% CI) | 4.73% [4.00, 5.47] | 4.31% [3.15, 5.48] |
| Median daily CFR | 3.84% | 2.29% |
| Case-weighted CFR | 4.66% | 2.85% |
| Mean cumulative CFR | 5.17% | 2.41% |

- **Lethality fell in wave 2.** The median and the case-weighted CFR both drop markedly (Mann–Whitney p = 0.005). A comparison of *means* misses this (Welch p = 0.55).
- **Why the means mislead:** the daily CFR has a **7-day reporting cycle** (lag-7 autocorrelation ≈ 0.4). Low weekend and holiday case counts produce CFR spikes 15 days later, and those spikes inflate the wave 2 mean.
- **Daily vs cumulative:**
  - in wave 1 the difference is not significant;
  - in wave 2 the mean daily CFR is 1.9 pp higher, purely because of how days are weighted, since the medians are almost identical.
- **The cumulative CFR is nearly perfectly autocorrelated** (lag-1 ≈ 0.84–0.96). Its effective sample size is only about 2–9 days, so it is unsuitable for interval estimates that assume independent observations.

## Methods
- Data cleaning:
  - the first 20 days of wave 1 are dropped (limited testing, CFRs up to 100%);
  - negative death corrections are dropped;
  - two data artefacts (75% and 88% CFR days) are dropped.
- Descriptive statistics, histograms, normal Q-Q plots, Shapiro–Wilk tests.
- Confidence intervals:
  - z-intervals for the mean (CLT);
  - chi-square intervals for the variance and SD, compared with **bootstrap** intervals (the chi-square ones are too narrow for these skewed data).
- Autocorrelation (ACF) and an effective-sample-size approximation.
- Daily − cumulative difference: independent two-sample vs paired intervals.
- Wave comparison: Welch t-test, Mann–Whitney test, and case-weighted CFR.

## Data
Daily German cases and deaths from [Our World in Data](https://github.com/owid/covid-19-data) (CC BY 4.0), included in `data/`:
- `wave{1,2}_raw.xlsx`: the original period extracts;
- `wave{1,2}_clean.xlsx`: the cleaned series used in the analysis.

## Running it
```bash
pip install numpy pandas scipy statsmodels matplotlib openpyxl notebook
jupyter notebook covid_cfr_analysis.ipynb
```

## Tech stack
Python · pandas · SciPy · statsmodels · matplotlib
