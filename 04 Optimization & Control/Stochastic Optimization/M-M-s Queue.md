---
title: "M/M/s Queue"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [queueing-theory, stochastic-optimization]
---
## Definition
The $(M/M/s{>}1)/(-/\infty/-)$ queue generalizes [[M-M-1 Queue]] to $s$ identical parallel servers, each serving at rate $\mu$, infinite waiting capacity, Poisson arrivals at rate $\lambda$. As a [[Birth-Death process]], the death rate depends on how many servers are busy: $n\mu$ while $n<s$ (not all servers occupied), and $s\mu$ once $n\ge s$ (all servers busy, extra customers queue).

## Properties
### Steady-state probabilities
Solving the birth-death balance equations with state-dependent death rates gives, with $\sigma = \lambda/\mu$,
$$
P_n = \begin{cases} \dfrac{\sigma^n}{n!}P_0 & 0\le n < s \\[4pt] \dfrac{\sigma^n}{s!\,s^{\,n-s}}P_0 & n \ge s \end{cases}, \qquad
P_0 = \left(\sum_{n=0}^{s-1}\frac{\sigma^n}{n!} + \frac{\sigma^s}{s!}\cdot\frac{1}{1-\sigma/s}\right)^{-1},
$$
where the second term of $P_0$'s sum is the closed form of $\sum_{n=s}^\infty \sigma^n/(s!s^{n-s})$, a geometric series in $\sigma/s$, convergent iff $\sigma/s<1$ (the multi-server stability condition — see [[Traffic Intensity]]).

### $L$, $L_q$, $W$, $W_q$
Since capacity is infinite, no customer is ever blocked, so $\hat\lambda=\lambda$ and $\rho = \sigma/s = \lambda/(s\mu)$ is the utilization per server. By [[Little's Law]], $L = W\lambda$, and the closed-form expression for the average number waiting (excluding those in service) is
$$
L_q = \sum_{n=s}^\infty (n-s)P_n = P_0\,\frac{\sigma^{s+1}}{(s-1)!\,(s-\sigma)^2},
$$
from which $W_q = L_q/\lambda$, $W = W_q + 1/\mu$, and $L=\lambda W$.

## Examples
Two taxi companies, each with 2 taxis, receive 8 calls/hour with average trip time 12 minutes ($\mu=5$/hr); consolidating into one office with $s=4$ taxis and $\lambda=16$/hr is compared against keeping $s=2$ — the exercise computes $\hat\lambda, P_0, L, W, L_q, W_q$ for both configurations side by side to evaluate whether consolidation improves service.

## See also
[[M-M-1 Queue]], [[M-M-s-N Queue]], [[Kendall's Notation]], [[Little's Law]], [[Traffic Intensity]]
