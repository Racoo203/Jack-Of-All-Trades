---
title: "Bayes risk"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 4 - Bayesian Decision Theory"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, decision-theory]
---
## Definition
For a decision rule $\delta:\mathcal X\to D$ and [[Loss function]] $L$, the **frequentist risk** is the expected loss over the data distribution, for fixed $\theta$:
$$
R(\theta,\delta) = E_{X|\theta}[L(\theta,\delta(X))] = \int_{\mathcal X} L(\theta,\delta(x))\,f(x|\theta)\,dx
$$
Given a prior $\pi$ on $\Theta$, the **Bayes risk** averages the frequentist risk over the prior:
$$
r(\pi,\delta) = \int_\Theta R(\theta,\delta)\,\pi(\theta)\,d\theta = \int_\Theta\left(\int_{\mathcal X} L(\theta,\delta(x))f(x|\theta)\,dx\right)\pi(\theta)\,d\theta
$$
For observed data $x$, the **posterior expected loss** of decision $d$ is
$$
\rho(\pi,d|x) = \int_\Theta L(\theta,d)\,\pi(\theta|x)\,d\theta
$$

## Properties
### Frequentist risk does not totally order decision rules
$R(\theta,\delta)$ is a function of $\theta$, so comparing two rules $\delta_1,\delta_2$ can give $R(\theta,\delta_1)<R(\theta,\delta_2)$ for some $\theta$ and the reverse for others — risk alone does not decide between them. If $R(\theta,\delta_1)\le R(\theta,\delta_2)$ for *every* $\theta$ (strictly for at least one), $\delta_2$ is called **inadmissible** (dominated by $\delta_1$); otherwise both may be **admissible**.

### Bayes risk gives a total order — minimizing pointwise minimizes it (Proposition 4.1)
Because $r(\pi,\delta)$ is a single real number for fixed $\pi$, it orders decision rules completely: prefer $\delta_1$ to $\delta_2$ iff $r(\pi,\delta_1)\le r(\pi,\delta_2)$.

**Proof.** Swap the order of integration and recognise the [[Prior predictive distribution]] $p(x)=\int_\Theta f(x|\theta)\pi(\theta)\,d\theta$:
$$
r(\pi,\delta) = \int_\Theta\int_{\mathcal X} L(\theta,\delta(x))f(x|\theta)\,dx\,\pi(\theta)\,d\theta
= \int_{\mathcal X} p(x)\left(\int_\Theta L(\theta,\delta(x))\pi(\theta|x)\,d\theta\right)dx
= \int_{\mathcal X} p(x)\,\rho(\pi,\delta(x)|x)\,dx
$$
Since $p(x)\ge 0$, this integral is minimized (over the choice of function $\delta$) by choosing, **independently for each $x$**, the value $\delta(x)$ that minimizes $\rho(\pi,\delta(x)|x)$. This decouples a hard functional-optimization problem (over all functions $\delta$) into a simple pointwise optimization (over $d\in D$ for each fixed $x$) — this is exactly what makes [[Bayes estimate|Bayes estimators]] computable. $\blacksquare$

### Validity for improper priors
The proposition holds for both proper and improper priors, as long as $r(\pi)$ (the Bayes risk of the Bayes rule) is finite. If $r(\pi)=\infty$, the same pointwise-minimization construction still defines a **generalized Bayes estimator**.

### Uniqueness
For strictly convex loss functions (e.g. quadratic loss), Bayes estimators are unique.

## See also
[[Loss function]], [[Bayes estimate]], [[Minimax estimator]], [[Prior predictive distribution]]
