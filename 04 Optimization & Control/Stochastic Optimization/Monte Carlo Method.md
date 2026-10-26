---
title: "Monte Carlo Method"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [simulation, stochastic-optimization]
---
## Definition
The **Monte Carlo method** estimates a quantity $\varphi = E[X]$ — for a random variable $X$ with distribution $F_X$ that cannot easily be computed analytically — by drawing $n$ independent samples $X_1,\dots,X_n \sim F_X$ (via a [[Pseudorandom Number Generator]] and, e.g., [[Inverse Transform Sampling]]) and using the sample mean
$$
\hat\varphi = \bar X_n = \frac{S_n}{n}, \qquad S_n = X_1 + \cdots + X_n
$$
as an approximation. Monte Carlo never gives the exact value of $\varphi$ — only an approximation with some error, which shrinks (in a precise probabilistic sense) as $n$ grows.

## Properties
### Justification via the Weak Law of Large Numbers and the CLT
For i.i.d. $X_1, X_2,\dots$ with $\mu = E[X_i]$, the **Weak Law of Large Numbers** states that for every $\epsilon > 0$,
$$
P\!\left(\left|\frac{S_n}{n} - \mu\right| > \epsilon\right) \to 0 \quad \text{as } n \to \infty,
$$
i.e. the (normalized) sum concentrates around the true mean as $n$ grows. If additionally $\sigma^2 = E[(X_i-\mu)^2] < \infty$, the **Central Limit Theorem** gives the asymptotic distribution of $S_n - n\mu$ (Gaussian, scale $\sigma\sqrt n$), which lets the error and the probability of exceeding it be quantified simultaneously via the normal distribution.

### Practical caveats
Real implementations don't strictly satisfy either theorem's hypotheses: computational limits cap the achievable $n$ (and pseudorandom generators are cyclic, so truly independent samples run out eventually — see [[Pseudorandom Number Generator]]), and the CLT's error estimate is only asymptotically valid, with its quality at finite $n$ depending on the (unknown, problem-specific) rate of convergence to normality — an additional source of error beyond the sampling error itself.

### Basic pseudocode
To estimate $\varphi = E[X]$: (1) obtain a source of i.i.d. $U(0,1)$ draws (a pseudorandom number generator with a **seed** initializing the sequence and a **draw function** producing the next value); (2) transform each uniform draw into a sample of $X$'s actual distribution (see [[Inverse Transform Sampling]]); (3) repeat $n$ times and average.

## Examples
### Reliability: satellite mean time to failure (MTTF)
A satellite needs $\ge 2$ of 5 solar panels working; each panel's lifetime is $U(1000,5000)$ hours (mean 3000h). $\varphi$ = expected time until the satellite fails (i.e., until the 4th of 5 panels has failed — since only 2 must survive, failure occurs at the 4th panel failure). Each of $n$ experiments draws 5 panel lifetimes and records the time of the 4th failure; averaging over $n=6$ trial experiments gave $\hat\varphi = 3683$ hours with sample standard deviation $\approx 297$ (an indicator of the estimator's own error).

### Reliability: two computers and a transmitter
A satellite functions while $\ge 1$ of 2 computers (each $U(0,500)$h) *and* its transmitter ($U(0,1500)$h) both work; each experiment draws all three lifetimes, computes the resulting system lifetime, and this is repeated (e.g. 1000 times) to estimate expected system lifetime.

### Project scheduling (PERT-style)
Building a house involves 8 tasks $T_1,\dots,T_8$, each with a uniformly distributed random duration and a precedence structure (e.g. $T_2, T_3$ depend on $T_1$; $T_8$ depends on $T_4,T_5,T_6,T_7$). A Monte Carlo estimate of the total project time draws all 8 task durations per replication, computes the critical-path completion time respecting precedence, and repeats for $n = 10, 100, 1000, 10000$ replications — tabulating how the estimated mean, standard deviation, and computation time change with $n$.

## See also
[[Problem-Solving Cycle for Mathematical Modeling]], [[Pseudorandom Number Generator]], [[Inverse Transform Sampling]], [[Discrete-Event Simulation of a Poisson Process]]
