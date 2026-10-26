---
title: "Chebyshev's Theorem"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 1 - Introducción a Métodos Multivariados (Anexos)"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, foundations, probability]
---
## Definition
**Chebyshev's theorem (Chebyshev's inequality)** bounds, for *any* distribution with finite mean $\mu$ and standard deviation $\sigma$ (no normality assumed), the probability that a random variable $X$ falls within $k$ standard deviations of its mean:
$$
P(\mu-k\sigma < X < \mu+k\sigma) \ge 1-\frac{1}{k^2}, \qquad k>1
$$
Equivalently, at least $\left(1-\tfrac{1}{k^2}\right)\times 100\%$ of the probability mass of *any* distribution lies within $k$ standard deviations of the mean.

## Properties
### Distribution-free guarantee
Because no assumption is made on the shape of the distribution, Chebyshev's bound is necessarily loose compared to distribution-specific results — e.g. for a normal distribution, the empirical rule gives $P(\mu-2\sigma<X<\mu+2\sigma)\approx 0.9545$, while Chebyshev only guarantees $P\ge 1-\tfrac14=0.75$ for $k=2$. The value of the theorem is precisely that its bound holds even when normality (or any other specific shape) cannot be assumed — a useful fallback when [[Graphical and Statistical Tests for Normality|normality tests]] reject $H_0$ and no [[Data Transformations for Normality (Box-Cox and Yeo-Johnson)|transformation]] has yet been applied.

### Numeric values
| $k$ | Minimum proportion within $k\sigma$ of $\mu$ |
|---|---|
| 2 | $1-1/4=75\%$ |
| 3 | $1-1/9\approx 88.9\%$ |
| 4 | $1-1/16=93.75\%$ |

## Examples
No numeric worked example beyond the general statement is given in this section of the course; it is presented as a reference tool for judging, from summary statistics alone (mean, standard deviation) and without a distributional assumption, how much of a sample's data should plausibly fall within a stated range — a sanity check to apply before or alongside the formal [[Graphical and Statistical Tests for Normality|normality tests]] later in the unit.

## See also
[[Skewness and Kurtosis]], [[Graphical and Statistical Tests for Normality]], [[The Multivariate Normal Distribution]]
