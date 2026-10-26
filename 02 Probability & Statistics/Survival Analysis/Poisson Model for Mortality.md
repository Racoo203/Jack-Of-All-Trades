---
title: "Poisson Model for Mortality"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 7 - Mortality models"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, poisson-model, mortality-estimation]
---
## Definition
Recall the [[Poisson distribution]]: if the hazard rate $\mu$ is constant over a period of exposure $E$, the number of deaths $d$ in that period is Poisson-distributed with mean $\mu E$, pdf $\dfrac{(\mu E)^d}{d!}\exp(-\mu E)$.

## Properties
### Poisson model for $\mu_x$
Assuming constant force of mortality $\mu_x$ within integer ages, $d_x \sim \text{Poisson}(\mu_x E_x^C)$, where $E_x^C$ is the [[Exposed to Risk|central exposed to risk]]. Likelihood:
$$
L = \frac{\exp(-\mu_x E_x^C)(\mu_x E_x^C)^{d_x}}{d_x!} \quad\Longrightarrow\quad \hat\mu_x = \frac{d_x}{E_x^C}, \qquad \text{Var}(\hat\mu_x) = \frac{\hat\mu_x}{E_x^C}
$$
matching the [[Two-State Model|two-state model]] MLE exactly (both rely on the same constant-force assumption).

## Examples
With $E_x^C=3$, $d_x=2$: $\hat\mu_x = 2/3 = 0.667$, $\text{Var}(\hat\mu_x) = 0.667/3 = 0.222$.

### Binomial vs. Poisson models
- The Poisson model uses the exact exposure time ($E_x^C$); the [[Binomial Model for Mortality|Binomial model]] only uses the count $E_x$.
- The Binomial estimator requires more numerical work to derive under general assumptions than the Poisson estimator (though under UDD both reduce to closed forms).
- The Poisson model assumes constant force of mortality over $[x,x+1)$; the Binomial model typically assumes UDD (linear progression of $l_x$), plus the approximation $E_x^C\approx E_x-\tfrac12 d_x$.

### Two-state vs. Binomial vs. Poisson
The [[Two-State Model]] has a better interpretation than either: it is an exact description of the underlying process, whereas the Poisson model is only an approximation and technically allows the number of deaths to exceed the number under observation. The two-state approach also generalises naturally to non-absorbing multi-state models (e.g. healthy–unhealthy–dead, where healthy and unhealthy can transition to each other).

## See also
[[Two-State Model]], [[Binomial Model for Mortality]], [[Exposed to Risk]]
