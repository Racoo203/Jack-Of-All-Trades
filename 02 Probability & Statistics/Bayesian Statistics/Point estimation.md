---
title: "Point estimation"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 2 - Classical Methods of Statistics"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, classical-statistics, foundations]
---
## Definition
In the frequentist perspective, $\theta$ is not random: a distinct distribution $f(x;\theta^*)$, with unknown true value $\theta^*$, generates the observed data. A **point estimate** $\hat\theta \in \Theta$ is a single value, computed as a function of the data, used as the "best guess" of $\theta^*$. The most common way to construct one is the [[Maximum Likelihood Estimate]].

## Properties
### Bias
The bias of an estimator $\hat\theta$ of $\theta$ is
$$
\text{Bias}(\hat\theta,\theta) = E[\hat\theta|\theta] - \theta
$$
$\hat\theta$ is **unbiased** if $\text{Bias}(\hat\theta,\theta)=0$ for all $\theta$.

### Worked example: a biased MLE (Uniform$(0,\theta)$)
Let $X_1,\dots,X_n$ be i.i.d. $\text{Uniform}(0,\theta)$. The [[Maximum Likelihood Estimate]] is $\hat\theta = \max\{X_i\}$ (the likelihood $L(\theta)=\theta^{-n}$ is decreasing in $\theta$, so it is maximized by taking $\theta$ as small as possible subject to $\theta \ge \max\{x_i\}$). The cdf of $\max\{X_i\}$ is $P[\max\{X_i\}\le x] = (x/\theta)^n$, so its density is $n x^{n-1}/\theta^n$, giving
$$
E[\max\{X_i\}] = \int_0^\theta x \cdot n\frac{x^{n-1}}{\theta^n}\,dx = \frac{n\theta}{n+1}
$$
so $\hat\theta$ is **biased** (downward), with bias $-\theta/(n+1)$, though it is asymptotically unbiased as $n\to\infty$.

### Worked example: constructing an unbiased estimator (marathon runner problem)
Given a single observation $T$, the runner's number, uniform on $\{1,\dots,N\}$, the MLE of $N$ is $\hat N = T$. Its expectation is $E[T|N] = \frac{N+1}{2}$, so $\text{Bias}(\hat N,N) = -\frac{N-1}{2}$. Since $E[2T-1|N]=N$, $\tilde N = 2T-1$ is unbiased. This illustrates that the MLE need not be unbiased, and that unbiased estimators are not unique or automatically "best" (an estimator can be unbiased and still take absurd or out-of-range values).

## See also
[[Maximum Likelihood Estimate]], [[Likelihood function]], [[Bayes estimate]]
