---
title: "Loss function"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 4 - Bayesian Decision Theory"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, decision-theory]
---
## Definition
A loss function is any function $L:\Theta\times D\to[0,\infty)$, where $\Theta$ is the set of possible true states of nature (parameter values) and $D$ is the set of possible decisions/actions. $L(\theta,d)$ is the penalty incurred by taking decision $d$ when the true state is $\theta$. Statistical decision theory (estimation, hypothesis testing, ...) is framed as choosing $d\in D$, based on data $x$, to control this loss — see [[Bayes risk]] for how the loss function is turned into a criterion for comparing decision rules, and [[Bayes estimate]] for the resulting optimal decision.

## Properties
### Quadratic (squared error) loss
$L(\theta,d)=(\theta-d)^2$. **Proposition.** The Bayes estimator under squared error loss is the posterior mean:
$$
\delta^\pi(x) = E^\pi[\theta|x] = \frac{\int_\Theta \theta\, f(x|\theta)\pi(\theta)\,d\theta}{\int_\Theta f(x|\theta)\pi(\theta)\,d\theta}
$$
**Proof.** For any random variable $Y$, $E[(Y-a)^2]$ is minimized over $a$ at $a=E[Y]$ (standard calculus: differentiate $E[(Y-a)^2]=E[Y^2]-2aE[Y]+a^2$ w.r.t. $a$). Apply with $Y=\theta|x$.

### Absolute error loss
$L(\theta,d)=|\theta-d|$, a special case ($k_1=k_2=1$) of the asymmetric linear loss
$$
L_{k_1,k_2}(\theta,d) = \begin{cases}k_2(\theta-d) & d<\theta\\ k_1(d-\theta) & d\ge\theta\end{cases}
$$
**Proposition.** The Bayes estimator under $L_{k_1,k_2}$ is the $k_2/(k_1+k_2)$ quantile of $\pi(\theta|x)$. In particular, under absolute error loss ($k_1=k_2$), the Bayes estimator is the **posterior median**.

### 0-1 loss
For testing $H_0:\theta\in\Theta_0$ vs $H_1:\theta\notin\Theta_0$ with $D=\{0,1\}$ ($1=$ accept $H_0$):
$$
L(\theta,d) = \begin{cases}0 & \theta\in\Theta_0, d=1\ \text{or}\ \theta\notin\Theta_0, d=0\\ 1 & \text{otherwise (incorrect decision)}\end{cases}
$$
The associated frequentist risk $R(\theta,\delta)$ equals precisely the Type I / Type II error probabilities of [[Classical Hypothesis Testing]]. The Bayes rule under 0-1 loss is
$$
\delta^\pi(x) = 1 \iff P[\theta\in\Theta_0|x] > P[\theta\notin\Theta_0|x] \iff P[\theta\in\Theta_0|x] > \tfrac12
$$

### Continuous 0-1 (tolerance) loss
$L_b(\theta,\delta(X)) = 0$ if $|\theta-\delta(X)|<b$, else $1$. Minimizing the posterior expected loss is equivalent to **maximizing** $\int_{\delta-b}^{\delta+b}\pi(\theta|X)\,d\theta$ over $\delta$. As $b\to0$, this is maximized by taking $\delta(X)$ to be the **posterior mode**.

## See also
[[Bayes risk]], [[Bayes estimate]], [[Classical Hypothesis Testing]], [[Minimax estimator]]
