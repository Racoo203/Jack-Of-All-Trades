---
title: "Likelihood Ratio Test"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 5 - The proportional hazard model"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, hypothesis-testing, likelihood-ratio-test, nested-models]
---
## Definition
The **likelihood ratio test** compares the goodness of fit of two **nested models**: model 1's parameters are a subset of model 2's, and model 2 has additional parameter(s).
$$
H_0: \text{model 1} = \text{model 2} \quad(\text{the additional parameters are zero}) \qquad H_1: \text{model 1}\neq\text{model 2}
$$
The test statistic is twice the (absolute) difference in log-likelihoods of the two fitted models, $\text{LL.diff} = 2|\ln L_2 - \ln L_1|$. Under $H_0$, $\text{LL.diff} \sim \chi^2_k$, where $k$ is the difference in the number of parameters between the two models. Reject $H_0$ if the statistic exceeds the critical value at the chosen significance level (usually 0.05).

## Properties
### Relationship to the Wald test
For a single added covariate, the likelihood ratio test and the [[Wald Test]] typically agree in conclusion (both test whether that covariate's coefficient is zero), though they can occasionally disagree in finite samples since they use different approximations to the same asymptotic $\chi^2$ theory.

### Application to variable selection
Used symmetrically to the [[Wald Test]] in [[Cox Proportional Hazards Model|Cox regression]] variable selection: in forward selection, a variable is added if the likelihood ratio test comparing the models with/without it is significant; in backward selection, a variable is dropped if the test is not significant.

## Examples
Rossi data: model 1 (financial aid only) has $\ln L_1=-673.4621$; model 2 (financial aid + age) has $\ln L_2=-666.2358$. $\text{LL.diff}=2\times(673.4621-666.2358)=14.45257$, with $1$ degree of freedom (one extra parameter, age). The p-value ($P(\chi^2_1 > 14.45257)$) is $\approx 0.000144 < 0.05$, so $H_0$ is rejected: age's coefficient is not zero — matching the conclusion of the Wald test on the same coefficient ($p=0.000614$).

## See also
[[Cox Proportional Hazards Model]], [[Wald Test]], [[Statistical Tests for Graduation]]
