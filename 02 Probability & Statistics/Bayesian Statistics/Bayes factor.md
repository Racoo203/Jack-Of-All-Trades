---
title: "Bayes factor"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 5 - Bayesian Hypothesis Testing"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, decision-theory]
---
## Definition
For $H_0:\theta\in\Theta_0$ vs $H_1:\theta\in\Theta_1$, the Bayes factor is the ratio of posterior odds to prior odds of $H_0$ vs $H_1$:
$$
B^\pi(x) = \frac{P^\pi(\theta\in\Theta_0|x)/P^\pi(\theta\in\Theta_1|x)}{P^\pi(\theta\in\Theta_0)/P^\pi(\theta\in\Theta_1)}
$$
$B^\pi(x)>1$: the data favour $H_0$. $B^\pi(x)<1$: the data favour $H_1$. $B^\pi(x)=1$: the data are uninformative between the hypotheses. Unlike the raw posterior probability, the Bayes factor isolates the *effect of the data* on the odds, though it still depends on the prior through the weighting inside $\Theta_0,\Theta_1$.

## Properties
### Reduces to the likelihood ratio for simple vs. simple hypotheses
If $\Theta_0=\{\theta_0\}$, $\Theta_1=\{\theta_1\}$:
$$
B^\pi(x) = \frac{f(x|\theta_0)}{f(x|\theta_1)}
$$

### General formula
$$
B^\pi(x) = \frac{\int_{\Theta_0}\pi(\theta)f(x|\theta)\,d\theta \big/ \int_{\Theta_0}\pi(\theta)\,d\theta}{\int_{\Theta_1}\pi(\theta)f(x|\theta)\,d\theta \big/ \int_{\Theta_1}\pi(\theta)\,d\theta} = \frac{p(x|\theta\in\Theta_0)}{p(x|\theta\in\Theta_1)}
$$
the ratio of the (prior-weighted) predictive density of $x$ under each hypothesis — contrast with the purely frequentist likelihood ratio $R(x)=\sup_{\theta\in\Theta_0}f(x|\theta)\big/\sup_{\theta\in\Theta_1}f(x|\theta)$, which uses the *maximized* likelihood rather than an *integrated* one.

### Point-null construction: a prior with an atom
To test $H_0:\theta=\theta_0$ against a composite $H_1$, use a prior with an atom at $\theta_0$:
$$
\pi(\theta) = \rho_0\,\mathbb 1[\theta=\theta_0] + (1-\rho_0)\,g(\theta)\,\mathbb 1[\theta\ne\theta_0]
$$
Then
$$
B^\pi(x) = \frac{f(x|\theta_0)}{\int_\Theta g(\theta)f(x|\theta)\,d\theta}
$$

## Examples
### Worked example: Uniform waiting time, Pareto prior
$X_i \sim U(0,\theta)$ i.i.d., $H_0:0<\theta<15$ vs $H_1:\theta>15$, prior $\theta\sim\text{Pareto}(5,3)$ (pdf $f(\theta)=\frac{\alpha x_0^\alpha}{\theta^{\alpha+1}}\mathbb 1_{\theta>x_0}$). With data $(10,3,2,5,14)$ (max $=14$), the posterior is $\propto \theta^{-9}\mathbb 1_{\theta>14}$, giving $P^\pi(\theta<15|x)=1-(15/14)^{-8}=0.4242$, hence $P^\pi(\theta>15|x)=0.5758$. The prior probabilities are $P^\pi(\theta<15)=0.9630$, $P^\pi(\theta>15)=0.0370$. So
$$
B^\pi(x) = \frac{0.4242/0.5758}{0.9630/0.0370} = 0.0283 \ll 1
$$
strongly favouring $H_1$ — despite the prior heavily favouring $\Theta_0$, the data (max observation $=14$, close to the boundary $15$) shift belief decisively toward $H_1$.

### Worked example: Binomial point null with atom prior
$X\sim\text{Binomial}(n,p)$, $H_0:p=1/2$, prior with atom $\rho_0$ at $1/2$ and otherwise uniform. Then $B^\pi(x) = \binom{n}{x}(1/2)^n \big/ \left[\binom{n}{x}B(x+1,n-x+1)\right]$. For $\rho_0=1/2$, $n=5$, $x=3$: $B^\pi(x)=15/8$ and $P(p=1/2|x)=15/23\approx0.652$ — larger than the prior $\rho_0=0.5$, so the data support $H_0$.

## See also
[[Bayesian hypothesis testing]], [[Likelihood function]], [[Prior distribution]], [[Posterior distribution]]
