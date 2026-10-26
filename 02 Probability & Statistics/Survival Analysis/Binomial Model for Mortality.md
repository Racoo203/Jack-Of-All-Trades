---
title: "Binomial Model for Mortality"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 7 - Mortality models"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, binomial-model, mortality-estimation]
---
## Definition
Recall the [[Bernoulli distribution|Bernoulli]]/[[Binomial distribution|Binomial]] setup: for one person, $\delta=1$ if dead at age $[x,x+1)$ with $q=P(\delta=1)$, pdf $q^\delta(1-q)^{1-\delta}$; for $n$ people, $d=\sum_i\delta_i \sim \text{Binomial}(n,q)$.

## Properties
### Naive binomial model
Assume every individual is observed for the whole year of age $[x,x+1)$, with sample size the [[Exposed to Risk|initial exposed to risk]] $E_x$ (number alive on their $x$th birthday), and a completely closed sample ($E_{x+1}=E_x-d_x$). Then $d_x \sim \text{Binomial}(E_x,q_x)$, with likelihood
$$
L = \binom{E_x}{d_x}q_x^{d_x}(1-q_x)^{E_x-d_x} \quad\Longrightarrow\quad \hat q_x = \frac{d_x}{E_x}, \qquad \text{Var}(\hat q_x) = \frac{\hat q_x(1-\hat q_x)}{E_x}
$$
This is impractical: it requires everyone to be observed for the full year and allows no censoring — in practice individuals enter/exit at arbitrary ages.

### Practical binomial model
Each individual $i$ is observed over $[x+a_i,x+b_i]$, $0\leq a_i\leq b_i\leq1$. The likelihood for a sample of size $n$ is
$$
L = \prod_{i=1}^n \left({}_{b_i-a_i}q_{x+a_i}\right)^{\delta_i}\left(1-{}_{b_i-a_i}q_{x+a_i}\right)^{1-\delta_i}
$$
Estimating ${}_tq_x$ separately for every $(t,x)$ is impractical, so an assumption reducing the dimensionality is needed. Possible choices: [[Uniform Distribution of Deaths (UDD)|uniform distribution of deaths]] (${}_tq_x=tq_x$), the **Balducci assumption** ($1-{}_{1-t}q_{x+t}=(1-t)q_x$), or constant force of mortality (${}_tq_x=1-e^{-\mu t}$).

### Estimator under UDD
Under UDD, ${}_{b_i-a_i}q_{x+a_i} = (b_i-a_i)q_x$, giving
$$
\hat q_x = \frac{\sum_{i=1}^n \delta_i}{\sum_{i=1}^n(b_i-a_i)} = \frac{d_x}{E_x}, \qquad \text{Var}(\hat q_x) = \frac{\hat q_x(1-\hat q_x)}{E_x} \approx \frac{\hat q_x}{E_x}
$$

### Actuarial estimator (via central exposed to risk)
Since $E_x^C$ is typically easier to compute than $E_x$ (see [[Exposed to Risk]]), and $E_x^C \approx E_x - \tfrac12 d_x$, substituting into the binomial estimator gives the **actuarial estimator**
$$
\tilde q_x = \frac{d_x}{E_x^C + \tfrac12 d_x}
$$

## Examples
With $E_x=43/12$, $d_x=2$: $\hat q_x = 2/(43/12) = 0.558$, $\text{Var}(\hat q_x) = \dfrac{0.558(1-0.558)}{43/12} = 0.0688$. With $E_x^C=3$, $d_x=2$: $\tilde q_x = \dfrac{2}{3+1} = 0.5$.

## See also
[[Exposed to Risk]], [[Poisson Model for Mortality]], [[Uniform Distribution of Deaths (UDD)]], [[Two-State Model]]
