---
title: "Cox Proportional Hazards Model"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 5 - The proportional hazard model"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, cox-model, partial-likelihood, semi-parametric]
---
## Definition
It is often hard to find a parametric distribution that fits the baseline hazard well, and interest often centres on covariate effects rather than the baseline shape. The **Cox model** keeps the [[Proportional Hazards Model|proportional hazards]] structure $h(t\mid x)=h_0(t)\exp(x\beta)$ but leaves $h_0(t)$ **unspecified** (estimated nonparametrically), making it a **semi-parametric** model: nonparametric baseline, parametric covariate effects. It still satisfies the constant hazard-ratio property $h(t\mid x)/h(t\mid x^*) = \exp[(x-x^*)\beta]$.

## Properties
### Partial likelihood
Let $t_1<\cdots<t_D$ be distinct event times and $R(t_i)$ the **risk set** (individuals alive/at risk just before $t_i$). In $[t_i,t_i+\Delta t]$, the probability that any one event in the risk set occurs is $\sum_{j\in R(t_i)} h(t_i\mid z_j)\Delta t$. The conditional probability that it is individual $i$ specifically (given exactly one event occurs in $R(t_i)$) is, taking $\Delta t\to0$:
$$
\frac{h(t_i\mid z_i)}{\sum_{j\in R(t_i)} h(t_i\mid z_j)} = \frac{h_0(t)\exp(z_i\beta)}{\sum_{j\in R(t_i)} h_0(t)\exp(z_j\beta)} = \frac{\exp(z_i\beta)}{\sum_{j\in R(t_i)}\exp(z_j\beta)}
$$
the baseline hazard cancels. **Cox's partial likelihood** multiplies this over all $D$ event times:
$$
L_p(\beta) = \prod_{i=1}^D \frac{\exp(z_i\beta)}{\sum_{j\in R(t_i)}\exp(z_j\beta)}
$$
It is the component of the full likelihood depending on $\beta$ but not on $h_0$.

### Maximum partial likelihood estimation
Log partial likelihood (only over event times; censored times drop out of the product):
$$
l_p(\beta) = \sum_{i=1}^D z_i\beta - \sum_{i=1}^D \ln\left(\sum_{j\in R(t_i)}\exp(z_j\beta)\right)
$$
Score function:
$$
U_p(\beta) = \sum_{i=1}^D z_i - \sum_{i=1}^D \frac{\sum_{j\in R(t_i)} z_j\exp(z_j\beta)}{\sum_{j\in R(t_i)}\exp(z_j\beta)}
$$
Solving $U_p(\beta)=0$ (numerically) gives $\hat\beta$.

### Large-sample distribution and the Wald test
The local (observed) Fisher information from the partial likelihood is $I(\beta) = -\dfrac{d^2\ln L_p(\beta)}{d\beta^2}$, and by the CLT $\hat\beta \sim N(\beta, I(\beta)^{-1})$ as $n\to\infty$. This underlies the [[Wald Test|Wald test]] of $H_0:\beta=0$: $z^2 = \hat\beta^2/\hat V(\hat\beta) = \hat\beta^2 I(\hat\beta) \sim \chi^2_1$ under $H_0$. In software output: `coef` $=\hat\beta$, `exp(coef)` is the hazard ratio, `se(coef)`$=\sqrt{\hat V(\hat\beta)}$, `z = coef/se(coef)`.

### Interpreting the hazard ratio
$\exp(\hat\beta)<1$: the covariate is protective (reduces hazard); $\exp(\hat\beta)>1$: harmful (increases hazard); $=1$: no effect. E.g. from the Rossi recidivism data, $\hat\beta=0.712$ for being unmarried gives hazard ratio $2.038$: unmarried men have roughly double the reconviction hazard of married men (if statistically significant).

### Breslow estimator for the baseline hazard
Given $\hat\beta$ from the partial likelihood, the baseline cumulative hazard is estimated by
$$
\hat H_0(t) = \sum_{t_i\leq t}\frac{d_i}{\sum_{j\in R(t_i)}\exp(z_j\hat\beta)}
$$
so $\hat S_0(t)=\exp[-\hat H_0(t)]$ and, since $S(t\mid x)=\exp(-H_0(t)e^{x\beta}) = S_0(t)^{e^{x\beta}}$, individual survival curves follow as $\hat S(t\mid x)=\hat S_0(t)^{\exp(x\hat\beta)}$.

### Variable selection
- **Forward selection**: start from the null model, add one variable at a time if it is significant by the [[Wald Test|Wald test]] (or by a [[Likelihood Ratio Test|likelihood ratio test]] comparing with/without it).
- **Backward selection**: start from the full model, remove the least-significant variable at a time (by Wald or likelihood ratio test) until all remaining variables are significant.

### Checking the proportional hazards assumption
The PH assumption implies $S(t\mid X) = S_0(t)^{\exp(X\beta)}$. Taking the log twice:
$$
\log(-\log S(t\mid X)) = \log(-\log S_0(t)) + X\beta,
$$
so plotting $\log(-\log\hat S(t))$ — using the [[Kaplan-Meier estimate|Kaplan-Meier estimate]] — against $t$ (or $\log t$) for each level of a covariate: **parallel** curves support proportional hazards (a constant vertical offset $X\beta$); curves that cross or that converge/diverge over time indicate the assumption fails (e.g. a treatment offering strong short-term protection that fades later). When PH fails, options include [[Time-Varying Covariates and Stratified Cox Models|stratifying the Cox model]] by the offending covariate, adding a time-covariate interaction, or switching to an [[Accelerated Failure Time Model|AFT model]].

### R software note
In R's `survival` package, `coxph(Surv(time, event) ~ covariates, data = ...)` fits the model via partial likelihood; `summary()` reports `coef` ($\hat\beta$), `exp(coef)` (hazard ratio), `se(coef)`, the Wald `z` and p-value, plus the overall likelihood ratio, Wald, and score tests. `logLik(fit)` extracts $\ln L_p(\hat\beta)$, useful for building a [[Likelihood Ratio Test|likelihood ratio test]] between nested models (`2*(logLik(full) - logLik(reduced))`, compared against $\chi^2$ via `pchisq`). `survfit(fit, newdata = data.frame(...))` predicts the survival curve for a specific covariate profile using the [[Cox Proportional Hazards Model|Breslow estimator]] above.

## See also
[[Proportional Hazards Model]], [[Wald Test]], [[Likelihood Ratio Test]], [[Likelihood Function for Censored Survival Data]], [[Accelerated Failure Time Model]], [[Time-Varying Covariates and Stratified Cox Models]]
