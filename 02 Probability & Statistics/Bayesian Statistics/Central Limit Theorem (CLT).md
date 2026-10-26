---
title: "Central Limit Theorem (CLT)"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 7 - Reinsurance, Convolution and Central Limit Theory (CLT)"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, actuarial, risk-theory]
---
## Definition
**Theorem (CLT).** If $X_1,\dots,X_n$ are i.i.d. with mean $\mu$ and variance $\sigma^2<\infty$, then
$$
\lim_{n\to\infty} P\left[\sum_{i=1}^n X_i \le n\mu + x\sigma\sqrt n\right] = \Phi(x)
$$
i.e. the standardized sum $\frac{\sum_i X_i - n\mu}{\sigma\sqrt n}$ converges in distribution to $N(0,1)$.

## Properties
### Practical role: approximating the individual risk model
In the individual risk model $S=X_1+\cdots+X_n$ (total claims across $n$ policies, see [[Convolution]]), computing the exact distribution of $S$ via repeated convolution is often intractable. The CLT gives a tractable Normal approximation
$$
S \overset{\text{approx}}{\sim} N(n\mu,\ n\sigma^2)
$$
for large $n$, avoiding the need for an exact (and possibly unavailable) closed form for the sum's distribution — in contrast with special cases like the Poisson (see [[Convolution]]) or exponential/gamma family (see [[Moment Generating Function]]) where the exact distribution of the sum is available.

## See also
[[Convolution]], [[Moment Generating Function]], [[Normal distribution]]
