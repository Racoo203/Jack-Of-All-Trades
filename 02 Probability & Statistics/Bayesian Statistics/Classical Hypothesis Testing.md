---
title: "Classical Hypothesis Testing"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 2 - Classical Methods of Statistics"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, classical-statistics, foundations]
---
## Definition
A statistical hypothesis test partitions the parameter space $\Theta$ into $\Theta_0$ (null hypothesis $H_0:\theta\in\Theta_0$) and $\Theta_1$ (alternative $H_1:\theta\in\Theta_1$), with $\Theta_0\cap\Theta_1=\varnothing$ and $\Theta_0\cup\Theta_1=\Theta$. A **decision function** $\delta$ maps the data $x=(x_1,\dots,x_n)$ to a decision $d_0$ (accept $H_0$) or $d_1$ (reject $H_0$).

## Properties
### Type I and Type II error
- **Type I error**: rejecting $H_0$ when it is true, $P_\theta\{\delta(x)=d_1\}$ for $\theta\in\Theta_0$.
- **Type II error**: accepting $H_0$ when it is false, $P_\theta\{\delta(x)=d_0\}$ for $\theta\in\Theta_1$.

Both error probabilities cannot be simultaneously minimized for fixed sample size, so the convention is to fix a **significance level** $\alpha$ (bounding Type I error) and minimize Type II error subject to it:
$$
P_\theta\{\delta(x)=d_1\} \le \alpha \quad \text{for all } \theta \in \Theta_0
$$

### Worked derivation: two-sided Normal test
For $H_0:\theta=\theta_0$ vs. $H_1:\theta\ne\theta_0$ with $X_i\sim N(\theta,1)$ i.i.d. and decision rule $\delta(x) = d_0$ if $\bar x\in[\theta_0-c,\theta_0+c]$, else $d_1$:
$$
P_{\theta=\theta_0}\{\delta(x)=d_1\} = 1-\left[\Phi(c\sqrt n)-\Phi(-c\sqrt n)\right]
$$
Setting this $\le\alpha$ requires $c \ge \Phi^{-1}(1-\alpha/2)/\sqrt n$; taking the smallest such $c$ minimizes Type II error (narrowest acceptance region subject to the Type I constraint).

Equivalently, standardizing $\text{std}_X = \frac{\bar X - \theta_0}{\sigma/\sqrt n}\sim N(0,1)$ under $H_0$, the rule rejects $H_0$ when $|\text{std}_X|>c$ with $c=\Phi^{-1}(1-\alpha/2)$; the acceptance region $(-c,c)$ for $\text{std}_X$ is exactly the classical [[Confidence Interval]] region.

### Not every decision rule is reasonable
A rule that ignores the data entirely (e.g. flipping a coin to decide) can satisfy the Type I error bound but has far worse Type II error than a data-dependent rule — it is a poor test even though it is a valid one.

## Examples
Testing $H_0:\theta=75$kg vs $H_1:\theta\ne75$kg for British men's weight (variance known $=36$), at $\alpha=0.05$: reject if $|\bar x - 75|/(\sigma/\sqrt n) > z_{0.025}$.

## See also
[[Confidence Interval]], [[Likelihood function]], [[Credible interval vs Confidence interval]]
