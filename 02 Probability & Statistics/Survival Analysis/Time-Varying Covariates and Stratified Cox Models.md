---
title: "Time-Varying Covariates and Stratified Cox Models"
domain: Probability & Statistics
course: Survival Analysis
unit: "PGT Lectures"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, cox-model, stratification, time-varying-covariates, pgt-extension]
---
## Definition
When neither the [[Proportional Hazards Model|PH assumption]] nor the [[Accelerated Failure Time Model|AFT assumption]] holds for some covariate(s), the basic [[Cox Proportional Hazards Model|Cox model]] must be extended. Two standard extensions are the **stratified Cox model** (allowing the baseline hazard to differ across groups) and the **time-dependent Cox model** (allowing the covariate effect itself to change over time).

## Properties

### Stratified Cox model
Suppose covariates $Z_1,\dots,Z_k$ do **not** satisfy the PH assumption, while covariates $X_1,\dots,X_p$ do. Rather than modelling the $Z$'s through the linear predictor, form the $g$ **strata** defined by all combinations of values of $Z_1,\dots,Z_k$, and fit a separate baseline hazard per stratum while sharing the regression coefficients:
$$
h_g(t\mid X) = h_{0g}(t)\exp(\beta_1 X_1 + \cdots + \beta_p X_p), \qquad g=1,\dots,G.
$$
Each stratum's baseline hazard $h_{0g}(t)$ is left completely unspecified (as in the ordinary [[Cox Proportional Hazards Model|Cox partial likelihood]]) and is allowed to have an arbitrary, stratum-specific shape, while the $\beta$'s — and hence the hazard ratios for $X_1,\dots,X_p$ — are assumed common across strata. This removes the need for the non-PH covariates $Z$ to satisfy proportionality, at the cost of not estimating their effect directly.

### Time-dependent Cox model
Alternatively, allow some covariates to vary with time, $X_i(t)$. The hazard takes the form
$$
h(t\mid X(t)) = h_0(t)\exp\left(\sum_{i=1}^{p_1}\beta_i X_i(t) + \sum_{i=1}^{p_2}\delta_i X_i(t)\right),
$$
where the second sum collects covariates whose *effect* is itself time-varying. Comparing two covariate paths $X(t)$ and $X^*(t)$, the hazard ratio becomes
$$
\frac{h(t\mid X^*(t))}{h(t\mid X(t))} = \exp\left(\sum_{i=1}^{p_1}\beta_i\big(X_i^*(t)-X_i(t)\big) + \sum_{i=1}^{p_2}\delta_i\big(X_i^*(t)-X_i(t)\big)\right),
$$
which is **no longer constant in $t$** — the defining departure from proportional hazards.

#### When to use a time-dependent effect
A genuinely time-varying *effect* (not just a time-varying covariate value) is appropriate when:
- **Treatment effects change over time** — e.g. chemotherapy that is highly effective initially but loses effect later.
- **Vaccine protection wanes** over time since administration.
- **Gradual-onset effects**, such as obesity, whose impact on hazard develops progressively rather than instantaneously.
- **Time-varying exposures**, where a patient starts, stops, or switches medication at essentially random times (the covariate $X_i(t)$ itself changes value during follow-up, independent of whether its *coefficient* also changes).

#### Modelling a changing effect via interaction with $\log(t)$
A common parametrisation for a treatment effect that strengthens or weakens over time adds an interaction between the covariate and $\log(t)$:
$$
h(t\mid X) = h_0(t)\exp\big(\beta_1 X + \beta_2(X\times\log t)\big).
$$
Here $\beta_1$ is the effect at $t=1$ (where $\log t = 0$) and $\beta_2$ governs how the log-hazard-ratio drifts with $\log t$: if the treatment effect **increases** in protectiveness over time, $\beta_2<0$ (further reducing the hazard ratio as $t$ grows), and conversely $\beta_2>0$ if protection fades.

## See also
- [[Cox Proportional Hazards Model]]
- [[Proportional Hazards Model]]
- [[Accelerated Failure Time Model]]
