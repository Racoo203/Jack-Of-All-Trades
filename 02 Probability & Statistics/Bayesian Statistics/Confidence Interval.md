---
title: "Confidence Interval"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 2 - Classical Methods of Statistics"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, classical-statistics, foundations]
---
## Definition
A $100(1-\alpha)\%$ confidence interval for $\theta$ is a random interval, constructed as a function of the (not-yet-observed) data, that contains the true (fixed) parameter $\theta$ with probability $1-\alpha$ under repeated sampling. It is the frequentist counterpart of the Bayesian [[Credible Interval]].

## Properties
### Derivation via the standardized statistic
For $X_1,\dots,X_n$ i.i.d. $N(\theta,\sigma^2)$, the sample mean $\bar X\sim N(\theta,\sigma^2/n)$, so
$$
\text{std}_X = \frac{\bar X-\theta}{\sigma/\sqrt n} \sim N(0,1)
$$
Choosing $c=\Phi^{-1}(1-\alpha/2)$ so that $P(|\text{std}_X|<c)=1-\alpha$, and rearranging the inequality $-c<\text{std}_X<c$ to isolate $\theta$, gives the $100(1-\alpha)\%$ confidence interval
$$
\left(\bar X - c\frac{\sigma}{\sqrt n},\ \bar X + c\frac{\sigma}{\sqrt n}\right)
$$

### Duality with hypothesis testing
The confidence region $(-c,c)$ for the standardized statistic is precisely the **acceptance region** of the corresponding two-sided test of $H_0:\theta=\theta_0$ at level $\alpha$ (see [[Classical Hypothesis Testing]]): $\theta_0$ lies inside the confidence interval if and only if $H_0:\theta=\theta_0$ is not rejected at level $\alpha$.

### Interpretation
The randomness is in the interval (a function of $X$), not in $\theta$: before the data is observed, $P(\theta \in \text{CI}) = 1-\alpha$; after observing a specific $x$, the realized interval either does or does not contain $\theta$ — see [[Credible interval vs Confidence interval]] for the contrast with the Bayesian interpretation.

## See also
[[Classical Hypothesis Testing]], [[Credible interval vs Confidence interval]], [[Maximum Likelihood Estimate]]
