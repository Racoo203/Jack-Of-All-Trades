---
title: "Mean and Variance of Survival Time"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 1 - Concept of survival models"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, expected-value, mean-residual-life]
---
## Definition
For the lifetime [[Lifetime Function|$T$]] with pdf $f$ and survival function $S$, the mean and variance of $T$ are
$$
\mathbb{E}(T) = \int_0^\infty u f(u)\,du = \int_0^\infty S(u)\,du
$$
$$
\text{Var}(T) = \mathbb{E}(T^2) - [\mathbb{E}(T)]^2 = 2\int_0^\infty uS(u)\,du - \left(\int_0^\infty S(u)\,du\right)^2
$$
(The identity $\mathbb{E}(T)=\int_0^\infty S(u)\,du$ follows from integration by parts on $\int_0^\infty u f(u)\,du$, using $f(u)=-S'(u)$.)

## Properties
### Mean and variance of $T_x$
Using [[Force of Mortality and Actuarial Notation|$T_x$ and $S_x(t)$]]:
$$
\mathbb{E}(T_x) = \int_0^\infty S_x(u)\,du = \int_0^\infty ({}_up_x)\,du, \qquad \text{Var}(T_x) = 2\int_0^\infty uS_x(u)\,du - \left(\int_0^\infty S_x(u)\,du\right)^2
$$
$\mathbb{E}(T_x)$ is the **(complete) expectation of life at age $x$**, denoted $\overset{\circ}{e}_x$, and also called the **mean residual lifetime** $\text{mrl}(x) = \mathbb{E}(T-x\mid T>x)$. When $x=0$, $\text{mrl}(0)=\mathbb{E}(T)$ is the mean lifetime.

## See also
[[Lifetime Function]], [[Force of Mortality and Actuarial Notation]], [[Curtate Future Lifetime]], [[Life Table]]
