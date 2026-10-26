---
title: "Convolution"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 7 - Reinsurance, Convolution and Central Limit Theory (CLT)"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, actuarial, risk-theory]
---
## Definition
For independent random variables $X,Y$, the distribution of $S=X+Y$ (used throughout the **individual risk model** $S=X_1+\cdots+X_n$ for total claims on $n$ policies) is given by the convolution of their cdfs:
$$
F_{X+Y}(s) = P[X+Y\le s] = \int_{-\infty}^\infty P[Y\le s-x]\,dF_X(x) = \int_{-\infty}^\infty F_Y(s-x)\,dF_X(x) =: F_X * F_Y(s)
$$
**Derivation.** Condition on $X=x$: $P[X+Y\le s] = \int P[X+Y\le s\mid X=x]\,dF_X(x) = \int P[Y\le s-x]\,dF_X(x)$.

## Properties
### Discrete analogue
For independent discrete $X,Y$, $P(X+Y=z) = \sum_x P(Y=z-x)P(X=x)$ — the discrete convolution sum, used below for the Poisson sum.

### Convolution of two Uniforms
For $X\sim U(0,1)$, $Y\sim U(0,2)$ independent, applying the convolution formula and splitting the range of $s=x+y \in [0,3)$ into $[0,1),[1,2),[2,3)$ gives (by direct integration of the density pieces):
$$
F_{X+Y}(s) = \frac14 s^2\,\mathbb 1_{[0,1)}(s) + \frac14(2s-1)\,\mathbb 1_{[1,2)}(s) + \frac{(s-1)(5-s)}{4}\,\mathbb 1_{[2,3]}(s)
$$
a piecewise-quadratic (trapezoidal-density) cdf — the density of a sum of two uniforms is the classic "tent"/trapezoid shape.

### Poisson + Poisson = Poisson (via discrete convolution)
For $X\sim\text{Poisson}(\lambda)$, $Y\sim\text{Poisson}(\mu)$ independent:
$$
P(X+Y=z) = \sum_{x=0}^z \frac{\mu^{z-x}}{(z-x)!}e^{-\mu}\cdot\frac{\lambda^x}{x!}e^{-\lambda}
= \frac{(\lambda+\mu)^z}{z!}e^{-(\lambda+\mu)}\sum_{x=0}^z\binom{z}{x}\left(\frac{\mu}{\lambda+\mu}\right)^{z-x}\left(\frac{\lambda}{\lambda+\mu}\right)^x
$$
The sum is $1$ by the Binomial theorem, so $X+Y\sim\text{Poisson}(\lambda+\mu)$ — the **reproductive property** of the Poisson distribution under summation.

## See also
[[Central Limit Theorem (CLT)]], [[Moment Generating Function]], [[Reinsurance]], [[Distribution of a Function of a Random Variable]]
