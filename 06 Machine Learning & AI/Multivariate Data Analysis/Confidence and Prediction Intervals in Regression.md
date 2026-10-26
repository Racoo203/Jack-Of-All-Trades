---
title: "Confidence and Prediction Intervals in Regression"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo II, Unit 5 - Intervalos de Confianza"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, regression, dependence-analysis]
---
## Definition
Point estimates from a [[Multiple Linear Regression|regression]] fit — a coefficient $\hat\beta_j$, a fitted mean response $\hat y$, or a single future observation — all carry sampling uncertainty. This note covers three related but distinct interval estimates built on the same $t$-distribution machinery.

## Properties
### Confidence interval for a regression coefficient $\beta_j$
With $p$ = number of coefficients in the model and $n$ = number of observations, a $100(1-\alpha)\%$ confidence interval for $\beta_j$ is
$$
\hat\beta_j - t_{\alpha/2,\,n-p}\,s_{\hat\beta_j} \;<\; \beta_j \;<\; \hat\beta_j + t_{\alpha/2,\,n-p}\,s_{\hat\beta_j}
$$
R: `A = lm(y ~ x); confint(A, level = 1-alpha)`. With two predictors, a **confidence ellipse** (rather than two separate intervals) more accurately captures the *joint* uncertainty in a pair of coefficients simultaneously — R: `car::confidenceEllipse(reg, ...)`.

### Confidence interval for the mean response $E(Y\mid \mathbf{x}^*)$
For a fixed predictor value $\mathbf{x}^*=(x_1^*,\dots,x_{p-1}^*)$, the **mean response** is $Y = \beta_0+\beta_1x_1^*+\cdots+\beta_{p-1}x_{p-1}^*$, estimated by $\hat Y = \hat\beta_0+\hat\beta_1x_1^*+\cdots+\hat\beta_{p-1}x_{p-1}^*$. Since $\hat Y \sim N(Y, s_{\hat Y})$ (approximately, with $s_{\hat Y}$ estimated), $\dfrac{\hat Y - Y}{s_{\hat Y}}\sim t_{n-p}$, giving
$$
\hat Y - t_{\alpha/2,\,n-p}\,s_{\hat Y} \;<\; Y \;<\; \hat Y + t_{\alpha/2,\,n-p}\,s_{\hat Y}
$$
R: `predict(object = A, newdata = xe, interval = "confidence", level = 1-alpha)`.

### Prediction interval for a future observation
For predicting a **new, individual observation** $Y$ at $\mathbf{x}^*$ (not the mean response, but one future value), the interval uses $s_Y$ (which additionally accounts for the individual observation's own error variance, not just the estimated mean's variance):
$$
\hat Y - t_{\alpha/2,\,n-p}\,s_Y \;<\; Y \;<\; \hat Y + t_{\alpha/2,\,n-p}\,s_Y
$$
R: `predict(object = A, newdata = xe, interval = "prediction", level = 1-alpha)`. The point estimate $\hat Y$ is identical for both the confidence and the prediction interval — only the margin of error differs.

### Prediction intervals are always wider than confidence intervals
Because $s_Y > s_{\hat Y}$ (predicting one new observation carries strictly more uncertainty than estimating the mean response, which averages that individual variability away), **the prediction interval is always wider than the confidence interval for the mean**, at the same confidence level and the same $\mathbf{x}^*$. Plotted together against $x$, the prediction bands always envelope the (narrower) confidence bands, both widening as $x$ moves away from $\bar x$.

## Examples
R workflow for plotting both interval types together on a simple regression:
```r
A = lm(y ~ x)
Yp = predict(object = A, interval = "prediction", level = 0.97)
datos1 = cbind(datos, Yp)

library(ggplot2)
ggplot(datos1, aes(x=x, y=y)) +
  geom_point() +
  geom_line(aes(y=lwr), color="red", linetype="dashed") +
  geom_line(aes(y=upr), color="red", linetype="dashed") +
  geom_smooth(method=lm, formula=y~x, se=TRUE, level=0.97, col='blue', fill='pink2') +
  theme_light()
```
This reproduces the course's own figure showing prediction bands strictly outside the confidence bands, both narrowest at $\bar x$ and widening toward the extremes of the observed $x$ range.

## See also
[[Simple Linear Regression and Least Squares]], [[Multiple Linear Regression]], [[Regression Diagnostics - Outliers and Influential Observations]]
