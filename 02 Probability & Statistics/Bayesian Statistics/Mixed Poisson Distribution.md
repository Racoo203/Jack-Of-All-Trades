---
title: "Mixed Poisson Distribution"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 8 - Risk Theory"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, actuarial, risk-theory]
---
## Definition
For claim counts $N$, the Poisson distribution (one parameter, $E[N]=\text{Var}[N]=\lambda$) is the natural first choice for rare events. When data show **overdispersion** ($\text{Var}[N]/E[N] > 1$), a **mixed Poisson** model is used: $N|\Lambda=\lambda \sim \text{Poisson}(\lambda)$, with $\Lambda$ itself random, having distribution $U(\lambda)=P[\Lambda\le\lambda]$. This is structurally the same idea as a [[Bayesian Credibility Theory|Bayesian hierarchical/credibility]] setup, with $\Lambda$ playing the role of a random "risk parameter" varying across policyholders.

## Properties
### Marginal moments always show overdispersion
By the law of total expectation/variance:
$$
E[N] = E_\Lambda[E_N[N|\Lambda]] = E[\Lambda]
$$
$$
\text{Var}[N] = E_\Lambda[\Lambda^2+\Lambda] - (E[\Lambda])^2 = E[\Lambda] + \text{Var}[\Lambda] \ge E[N]
$$
with equality only if $\text{Var}[\Lambda]=0$ (i.e. $\Lambda$ is degenerate, recovering the ordinary Poisson). So mixing a Poisson over any non-degenerate $\Lambda$ **always** produces overdispersion relative to a pure Poisson($E[N]$) — this is the mathematical reason mixed-Poisson models are the standard fix when $\text{Var}[N]/E[N]>1$ is observed in claims data.

### Worked example: discrete two-point mixture
If $\Lambda=3$ w.p. $0.6$, $\Lambda=2$ w.p. $0.4$ (e.g. two classes of driver), the marginal pmf of $N$ is
$$
P(N=n) = 0.6\cdot e^{-3}\frac{3^n}{n!} + 0.4\cdot e^{-2}\frac{2^n}{n!}
$$
a weighted mixture of two Poisson pmfs (not itself Poisson).

### Worked example: compound sum with logarithmic severities → Negative Binomial
At an intersection, $N\sim\text{Poisson}(\lambda)$ accidents, each with $L_i\sim\text{Logarithmic}(c)$ casualties, $P[L_i=k]=\frac{c^k}{k\,h(c)}$, $h(c)=-\log(1-c)$. Using $m_L(t) = h(ce^t)/h(c)$ and the compound-sum mgf identity (see [[Collective Risk Model]]):
$$
m_S(t) = m_N(\log m_L(t)) = \exp\{\lambda(m_L(t)-1)\} = \left(\frac{1-c}{1-ce^t}\right)^{\lambda/h(c)}
$$
which is the mgf of a **Negative Binomial** distribution with parameters $\lambda/h(c) = -\lambda/\log(1-c)$ and $1-c$ — showing that compounding a Poisson claim count with a non-trivial severity distribution can itself reproduce a classic overdispersed count distribution for the total.

## See also
[[Collective Risk Model]], [[Bayesian Credibility Theory]], [[Moment Generating Function]]
