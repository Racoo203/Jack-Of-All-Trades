---
title: "Wald Test"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 5 - The proportional hazard model"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, hypothesis-testing, wald-test]
---
## Definition
The **Wald test** tests a hypothesis about a parameter using its maximum-likelihood estimate and the estimate's asymptotic variance, without needing to refit a restricted model. In the context of a [[Cox Proportional Hazards Model|Cox regression]] coefficient $\beta$:
$$
H_0: \beta = 0 \qquad H_1: \beta \neq 0
$$
The test statistic is
$$
z^2 = \frac{\hat\beta^2}{\hat V(\hat\beta)} = \hat\beta^2 I(\hat\beta)
$$
where $I(\hat\beta)$ is the (observed) information matrix evaluated at $\hat\beta$, i.e. minus the second derivative of the log (partial) likelihood.

## Properties
### Distribution under $H_0$
If $H_0$ holds, $z^2 \sim \chi^2_1$ (equivalently $z=\hat\beta/\text{se}(\hat\beta) \sim N(0,1)$), by the large-sample normality of the MLE $\hat\beta\sim N(\beta, I(\beta)^{-1})$.

### Reading software output
Standard regression/Cox output reports `coef` ($\hat\beta$), `exp(coef)` (hazard ratio), `se(coef)` ($\sqrt{\hat V(\hat\beta)}$), `z = coef/se(coef)`, and a p-value $= P(|Z|>|z|)$ under $H_0$. A p-value below the significance level (usually 0.05) is evidence against $H_0:\beta=0$.

## Examples
Given `coef` $=-2.76\times10^{-3}$, `se(coef)` unknown, `z`$=-4.6043$: since $z=\text{coef}/\text{se(coef)}$, $\text{se(coef)} = -0.0027/(-4.6043) \approx 0.00059$. Given `coef`$=-2.80\times10^{-3}$, `se(coef)`$=0.006197$: $z=-0.4512$, $z^2=0.203$; on the $\chi^2_1$ table this falls between $(0.102,0.455)$, so the p-value is between $(0.5,0.75)$ — not significant.

## See also
[[Cox Proportional Hazards Model]], [[Likelihood Ratio Test]], [[Likelihood Function for Censored Survival Data]]
