---
title: "Lifetime Function"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 1 - Concept of survival models"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, lifetime, survival-function]
---
## Definition
Let $T$ be a [[Random Variable|random variable]] measuring **survival time** (time to event) for a subject — in actuarial science, the lifetime of an individual from birth. Since $T$ measures time, it must be positive and continuous, $T > 0$.

The **cumulative distribution function (cdf)** of $T$ is
$$
F(t) = P(T \leq t), \quad t \in \mathbb{R}^+
$$
with the usual properties: $F$ is non-decreasing (for $t_1 < t_2$, $F(t_1) \leq F(t_2)$), $F(0)=0$, $\lim_{t\to\infty} F(t) = 1$, and $F$ is right-continuous.

The **probability density function (pdf)** $f(t)$, $t>0$, is defined by $F(t) = \int_0^t f(u)\,du$, so $f(t) = F'(t)$.

The **survival function** is the probability that an individual survives beyond time $t$:
$$
S(t) = P(T > t) = 1 - F(t) = \int_t^\infty f(u)\,du
$$
$S(t)$ is continuous and strictly decreasing, and
$$
f(t) = -\frac{dS(t)}{dt}
$$

## Properties
### Exponential example
If $T$ has an [[Exponential distribution]] with $f(t) = \lambda e^{-\lambda t}$, $t\geq 0$, $\lambda>0$, then
$$
S(t) = \int_t^\infty \lambda e^{-\lambda u}\,du = e^{-\lambda t}
$$

### Relation to the hazard function
$S(t)$, $F(t)$, $f(t)$ and the [[Hazard Function|hazard function]] $h(t)$ are all equivalent descriptions of the same survival pattern; see [[Hazard Function]] for the identity $h(t) = f(t)/S(t) = -\dfrac{d\ln S(t)}{dt}$.

## See also
[[Hazard Function]], [[Force of Mortality and Actuarial Notation]], [[Mean and Variance of Survival Time]], [[Parametric Survival Models]], [[Cumulative Distribution Function (CDF)]], [[Probability Density Function (PDF)]]
