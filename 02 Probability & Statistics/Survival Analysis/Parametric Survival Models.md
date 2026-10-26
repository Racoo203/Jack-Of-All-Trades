---
title: "Parametric Survival Models"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 1 - Concept of survival models"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, parametric-models, hazard-shapes]
---
## Definition
A **parametric survival model** assumes $T$ follows a known distribution family with unknown parameters, giving a closed-form survival function $S(t)$. The three canonical choices covered in this course are the [[Exponential distribution|Exponential]], [[Weibull distribution|Weibull]], and [[Lognormal distribution|Log-normal]] distributions, distinguished by the shape of hazard they induce.

## Properties
### Exponential distribution — constant hazard
$T \sim \text{Exp}(\lambda)$: $f(t) = \lambda e^{-\lambda t}$, $S(t) = e^{-\lambda t}$, $\lambda>0$, $\mathbb{E}(T) = 1/\lambda$, $\text{Var}(T) = 1/\lambda^2$, and
$$
h(t) = \frac{f(t)}{S(t)} = \lambda
$$
a **constant hazard rate over time** — the risk of the event does not depend on age. Used when the risk of failure does not change over time (e.g. call centres, accident rates).

### Memoryless property of the Exponential
The exponential distribution satisfies $P(T > t+s \mid T > s) = P(T>t)$. Proof: by definition of conditional probability,
$$
P(T>t+s \mid T>s) = \frac{P(T>t+s \cap T>s)}{P(T>s)}
$$
Since $T>t+s \implies T>s$ (for $t,s\geq0$), the intersection simplifies to $T>t+s$, so
$$
P(T>t+s\mid T>s) = \frac{P(T>t+s)}{P(T>s)} = \frac{e^{-\lambda(t+s)}}{e^{-\lambda s}} = e^{-\lambda t} = P(T>t)
$$
which proves the property. This is the only continuous distribution with this property, and it is what makes the constant-hazard assumption equivalent to an exponential lifetime.

### Weibull distribution — monotone hazard
$T\sim\text{Weibull}(\alpha,\lambda)$: $f(t) = \alpha\lambda t^{\alpha-1}\exp(-\lambda t^\alpha)$, $S(t)=\exp(-\lambda t^\alpha)$, and
$$
h(t) = \alpha\lambda t^{\alpha-1}
$$
- $\alpha < 1$: decreasing hazard
- $\alpha = 1$: constant hazard $h(t)=\lambda$ (recovers the Exponential distribution)
- $\alpha > 1$: increasing hazard

Useful when there are wear-out effects (e.g. machines).

### Log-normal distribution — non-monotone hazard
$T\sim\text{LogNormal}(\mu,\sigma^2)$:
$$
f(t) = \frac{1}{t\sigma\sqrt{2\pi}}\exp\left(-\frac{(\ln t-\mu)^2}{2\sigma^2}\right), \qquad S(t) = 1-\Phi\left(\frac{\ln t-\mu}{\sigma}\right)
$$
where $\Phi$ is the standard [[Normal distribution|normal]] cdf, and $h(t)=f(t)/S(t)$. The hazard increases, reaches a maximum, then decreases — suitable for modelling early-life failure.

## See also
[[Lifetime Function]], [[Hazard Function]], [[Force of Mortality and Actuarial Notation]], [[Gompertz' Law]]
