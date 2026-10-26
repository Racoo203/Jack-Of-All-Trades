---
title: "Time Series - Stationarity and Forecast Accuracy"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 6 - Series de Tiempo"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, time-series, forecasting]
---
## Definition
A **time series** is a sequence of observations of a (quantitative) variable collected at regular time intervals (daily, weekly, annually, etc.); visually, a curve that evolves over time. Applications span meteorology, telecommunications, economics, demography, marketing, geophysics, electronics, and astronomy, among others.

A time series is **stationary** if it has no trend and its statistical properties do not depend on time:
$$
E(x_t) = \mu \ (\text{constant mean}), \qquad \operatorname{Var}(x_t)=\sigma^2\ (\text{constant variance}), \qquad \operatorname{Cov}(x_t,x_{t+k})=V_k\ (\text{depends only on the lag } k,\text{ not on }t)
$$
Formally tested via the **Dickey–Fuller test** (unit-root test): $H_0$: the series is *not* stationary (has a unit root) vs. $H_1$: the series is stationary.

## Properties
### Autocorrelation
**Autocorrelation** — correlation of a series with its own past values — arises from cycles/trends not captured by an explanatory model (the cyclical pattern ends up in the residuals), from omitted relevant variables that are themselves correlated, or from an incorrectly specified functional form (which can produce runs of same-signed residuals). The same phenomenon can occur in cross-sectional data measured repeatedly on the same subject, where it is called *spatial* autocorrelation.

### Components of a time series
Four basic sources of variation combine to give a series its overall (often erratic-looking) pattern:
- **Trend.** A gradual, consistent pattern of change — long-run variation.
- **Seasonal variation.** Recurs every year in the same months/periods, with roughly the same intensity.
- **Cyclical variation.** Recurs over periods longer than a year, driven by factors other than the calendar (e.g. business cycles).
- **Irregular variation.** Unpredictable, non-recurring fluctuation.

### Forecast accuracy measures
Forecast error is $e_t = \text{actual value} - \text{forecast}$. Two standard summary measures:
$$
\text{CME (MSE)} = \frac{1}{n}\sum_t e_t^2 \qquad\qquad \text{EPAM (MAPE)} = \frac{1}{n}\sum_t \left|\frac{e_t}{\text{actual}_t}\right|\times 100\%
$$
CME (cuadrado medio del error, mean squared error) depends on the scale of the data, so it is only meaningful for comparing forecasts of the *same* series; EPAM (error porcentual absoluto medio, mean absolute percentage error) is scale-free and comparable across series.

### Forecasting methods (smoothing family)
- **Most-recent-value method.** Forecast for period $t+1$ is simply the observed value at period $t$. Simple but typically inaccurate (highest CME/EPAM of the methods compared below).
- **Historical average method.** Forecast for period $t+1$ is the average of all observed values up through period $t$. A good baseline specifically for *stationary* series (no trend to average away).
- **Moving average.** Forecast for period $t+1$ is the average of the $k$ most recent observations (e.g. $k=3$): $\hat y_{t+1} = \frac{1}{k}(y_{t-k+1}+\cdots+y_t)$. Smooths short-term noise; the choice of window $k$ is typically tuned by trial and error to minimize CME/EPAM.
- **Weighted moving average.** As above, but with unequal weights on the $k$ most recent observations — typically decreasing weight for older observations, e.g. weights $1/6,2/6,3/6$ for the three most recent points (most weight on the most recent).
- **Exponential smoothing.** A weighted average of *all* past values with exponentially decaying weight, computed recursively:
$$
F_{t+1} = \alpha Y_t + (1-\alpha)F_t, \qquad 0\le\alpha\le1
$$
$F_{t+1}$ is the forecast for period $t+1$, $Y_t$ the actual value at $t$, $F_t$ the previous forecast, and $\alpha$ the smoothing constant (larger $\alpha$ weights recent observations more heavily and makes the forecast more reactive; smaller $\alpha$ smooths more and reacts more slowly). The value of $\alpha$ is typically chosen by trying several candidates and picking the one that minimizes CME.

### Trend-projection methods (for non-stationary series)
When the mean itself drifts with time (see [[Time Series - Trend and Seasonal Decomposition]] for the full non-stationary case), linear or non-linear trend regression is used instead of the smoothing methods above, since averaging methods implicitly assume a constant mean.

## Examples
**Gasoline sales, 12 weeks** (17, 21, 19, 23, 18, 16, 20, 18, 22, 20, 15, 22 thousand gallons): visually flat, no trend — judged stationary. Comparing methods by CME/EPAM:

| Method | CME | EPAM |
|---|---|---|
| Most recent value | 16.27 | 19.24% |
| Historical average | 8.10 | 12.85% |
| Moving average ($k=3$) | 10.22 | 14.36% |

The historical average method gives the best fit here — consistent with the guidance above that it is well-suited to stationary series specifically. Exponential smoothing is then tried with $\alpha=0.2$ and $\alpha=0.3$; in this particular dataset neither beats the historical-average method's CME, illustrating that no single method dominates and the choice must be validated empirically per series.

## See also
[[Time Series - Trend and Seasonal Decomposition]], [[Multiple Linear Regression]]
