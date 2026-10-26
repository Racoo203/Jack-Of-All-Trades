---
title: "Discrete-Event Simulation of a Poisson Process"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [simulation, pseudorandom-numbers, stochastic-optimization]
---
## Definition
This note records the course's worked technique for simulating counts from a [[Poisson Process]] using [[Inverse Transform Sampling]] with a discretized (tabulated) inverse CDF, applied via a [[Pseudorandom Number Generator]]: build a cumulative-probability lookup table for $X \sim \text{Poisson}(\lambda)$, draw $U \sim U(0,1)$, and read off the smallest $x$ such that $F(x) = P(X\le x) \ge U$.

## Properties
### Worked example: arrivals of parts to a system
Parts arrive $\sim \text{Poisson}(\lambda=2)$ per hour, with $P(X=x) = e^{-\lambda}\lambda^x/x!$. Tabulating $p(x)$ and its cumulative sum:

| $x$ | $p(x)$ | cumulative |
|---|---|---|
| 0 | 0.13534 | 0.13534 |
| 1 | 0.27067 | 0.40601 |
| 2 | 0.27067 | 0.67668 |
| 3 | 0.18045 | 0.85712 |
| 4 | 0.09022 | 0.94735 |
| 5 | 0.03609 | 0.98344 |
| 6 | 0.01203 | 0.99547 |
| 7 | 0.00344 | 0.99890 |
| 8 | 0.00086 | 0.99976 |
| 9 | 0.00019 | 0.99995 |
| 10 | 0.00004 | 0.99999 |

To simulate one hour's arrivals: draw $U\sim U(0,1)$ from a [[Pseudorandom Number Generator]] and find the row where the cumulative probability first exceeds $U$. E.g. $U=0.374540 \Rightarrow$ falls in the $x=1$ row (cumulative jumps from $0.13534$ to $0.40601$), so 1 part arrives that hour. Running this for 8 hours with draws $0.374540,\ 0.950714,\ 0.731994,\ 0.598658,\ 0.156019,\ 0.155995,\ 0.058084,\ 0.866176$ gives simulated arrivals $1,5,3,2,1,1,0,4$.

### Validating the simulation at scale
The course exercise scales this up to $10{,}000$ simulated 300-day working years, and asks for: the resulting average arrival rate; the empirical probabilities $\hat p(x)$; and a direct comparison of $\hat p(x)$ against the theoretical $p(x) = e^{-\lambda}\lambda^x/x!$ table above — the large-sample empirical frequencies should converge to the theoretical table by the same Law of Large Numbers argument that justifies the [[Monte Carlo Method]] generally.

### A second application: call-center arrivals
Calls arrive one every two minutes on average (i.e. $\lambda = 0.5$/min $= 2.5$ per 5 minutes). Without simulating, the same Poisson formula answers: $P(3\text{ calls in }5\text{ min}) = P(X{=}3 \mid X\sim\text{Poisson}(2.5)) = 0.214$, and $P(\text{no calls in }5\text{ min}) = P(X{=}0) = 0.0843$ — included here because the course pairs this direct-calculation exercise with the simulate-10,000-periods exercise, i.e. simulation is checked against exact Poisson probabilities wherever both are tractable.

## See also
[[Poisson Process]], [[Inverse Transform Sampling]], [[Monte Carlo Method]], [[Pseudorandom Number Generator]]
