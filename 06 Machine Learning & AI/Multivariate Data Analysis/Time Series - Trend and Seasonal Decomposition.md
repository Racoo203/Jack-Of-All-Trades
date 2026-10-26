---
title: "Time Series - Trend and Seasonal Decomposition"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 6 - Series de Tiempo"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, time-series, forecasting]
---
## Definition
A time series is **non-stationary** when its mean and/or variance depend on time — contrasted with the [[Time Series - Stationarity and Forecast Accuracy|stationary case]] covered previously. Four qualitative patterns combine the two possible sources of non-constancy (mean vs. variance) with the two possible presences (trend, autocorrelation structure): series with trend (mean depends on time), series without trend but with time-dependent variance, series without trend but with non-constant autocorrelation, and the purely stationary case (none of the above). **Seasonality** (recurring calendar-linked cycles within a year) must not be confused with **stationarity** (constant mean/variance/autocorrelation) — a series can be highly seasonal yet still stationary once its seasonal pattern is accounted for, or non-stationary for reasons entirely unrelated to seasonality.

## Properties
### Linear trend regression (without seasonality)
For a series with an apparent linear trend, fit $y_t = \beta_0+\beta_1 t$ by [[Simple Linear Regression and Least Squares|ordinary least squares]] on time $t=1,\dots,n$. Limitation: a pure trend-line fit ignores any seasonal cycling within the year, so it systematically mis-forecasts periods that deviate from trend for seasonal reasons.

### Decomposition of a series with trend and seasonality
The classical (additive/multiplicative) decomposition separates a series into Observed (O) = Trend (T) $\times$/$+$ Seasonal (S) $\times$/$+$ Irregular (I), estimated in stages:
1. **Centered moving averages.** A first smoothing pass (moving average of the series, centered so it aligns with the correct time index) removes short-term/seasonal fluctuation, leaving an estimate of trend $\times$ cycle.
2. **Seasonal-irregular values.** Dividing (multiplicative model) or subtracting (additive model) the centered moving average from the original series isolates the seasonal + irregular components for each individual observation.
3. **Seasonal indices.** Averaging the seasonal-irregular values across all years for each period (e.g. each of the four quarters) gives one seasonal index per period — the estimate of that period's typical deviation from trend.
4. **Deseasonalized series.** Dividing the original series by its corresponding seasonal index removes the seasonal component, leaving trend + irregular — this deseasonalized series is what should be regressed on time, not the raw series.
5. **Forecast.** Fit trend regression to the deseasonalized series, then multiply the trend forecast for a future period by that period's seasonal index to obtain the final forecast.

In R, `decompose()` on a `ts()` object automates steps 1–3 (returning `$trend`, `$seasonal`, `$random`), and `T$x / T$seasonal` gives the deseasonalized series for step 4.

## Examples
**Bicycle sales, 10 years** (21.6, 22.9, 25.5, 21.9, 23.9, 27.5, 31.5, 29.7, 28.6, 31.4): a simple linear trend fit gives $\text{ventas}=20.4+1.1\cdot\text{año}$ — but this ignores within-year seasonal cycling entirely, since the data is annual with no sub-year structure given here; it illustrates the *basic* trend-regression step before seasonality is introduced.

**Quarterly TV sales, 4 years** (16 observations: e.g. Year 1: 4.8, 4.1, 6.0, 6.5; ... Year 4: 6.3, 5.9, 8.0, 8.4): full decomposition via `decompose(ts(ventas, frequency=4))` yields quarterly seasonal indices `T$seasonal`; dividing the series by them gives the deseasonalized series, whose linear-trend regression is $y=5.1080+0.1474\cdot\text{trimestre}$; forecasts for the four quarters of year 5 multiply this trend forecast by each quarter's seasonal index: `f(17)*a1*1000`, ..., `f(20)*a4*1000`.

**Follow-up exercise (Activity 11, textbook problem).** Three years of quarterly textbook sales (e.g. Q1: 1690, 1800, 1850 across the three years; Q2: 940, 900, 1100; Q3: 2625, 2900, 2930; Q4: 2500, 2360, 2615) asks the student to compute four-quarter and centered moving averages, the seasonal indices for each quarter, and to interpret which quarter has the highest seasonal index and whether that is a sensible result for a textbook publisher (plausibly the quarter aligned with the start of an academic term) — a direct test of steps 1–3 above by hand.

## See also
[[Time Series - Stationarity and Forecast Accuracy]], [[Simple Linear Regression and Least Squares]], [[Multiple Linear Regression]]
