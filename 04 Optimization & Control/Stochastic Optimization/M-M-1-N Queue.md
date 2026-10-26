---
title: "M/M/1/N Queue"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [queueing-theory, stochastic-optimization]
---
## Definition
The $(M/M/1)/(FCFS/N/\infty)$ queue is the finite-capacity version of [[M-M-1 Queue]]: a single server, Poisson arrivals at rate $\lambda$, exponential service at rate $\mu$, but total system capacity $N$ (server plus waiting room). An arrival that finds the system already at capacity $N$ **balks** — leaves without entering — so the nominal arrival rate $\lambda$ and the *effective* arrival rate $\hat\lambda$ (the rate at which customers actually enter) differ.

## Properties
### Finite-sum steady state (no stability condition needed)
The same birth-death balance equations as [[M-M-1 Queue]] apply for $0\le n<N$, but the state space is now finite, so $P_n = \sigma^n P_0$ still holds but the normalizing sum is finite:
$$
P_0 = \left(\sum_{n=0}^N \sigma^n\right)^{-1} = \frac{1-\sigma}{1-\sigma^{N+1}} \quad (\sigma\ne1).
$$
Because the sum is always finite, a steady state exists for **any** $\sigma=\lambda/\mu$, including $\sigma\ge1$ — unlike the infinite-capacity case.

### Effective arrival rate, utilization, and $L$, $L_q$, $W$, $W_q$
$$
\hat\lambda = \sum_{n=0}^{N-1}\lambda P_n = \lambda(1-\sigma^N P_0), \qquad \rho = \frac{\hat\lambda}{\mu} = \sigma(1-\sigma^N P_0),
$$
$$
L=\sum_{n=0}^N nP_n, \qquad L_q = \sum_{n=1}^N (n-1)P_n, \qquad W = \frac{L}{\hat\lambda}, \qquad W_q = \frac{L_q}{\hat\lambda}
$$
(using [[Little's Law]] with $\hat\lambda$, not the nominal $\lambda$, since blocked customers never enter the system).

### Worked example: waiting room with capacity 3
A doctor's waiting room holds up to 3 people (so $N=4$ counting the one being served, $s=1$), $\lambda=8$/hr, $\mu=6$/hr, $\sigma=4/3$:
$$
P_0 = \left(\sum_{n=0}^4 (4/3)^n\right)^{-1} = \frac{81}{781}, \quad P_1=\frac{108}{781},\ P_2=\frac{144}{781},\ P_3=\frac{192}{781},\ P_4=\frac{256}{781}.
$$
Then $L=\sum_{n=0}^4 nP_n \approx 2.5557$, $L_q = \sum_{n=1}^4(n-1)P_n \approx 1.6594$, $\hat\lambda = \mu\!\left(\frac{781-256}{781}\right)\approx5.3777$/hr (people who actually enter), $W = L/\hat\lambda \approx 28.54$ minutes, $W_q = L_q/\hat\lambda \approx 18.51$ minutes.

### Worked example: gas station with two pumps (finite, multi-server case)
See [[M-M-s-N Queue]] for the analogous finite-capacity derivation when $s>1$ (e.g. the two-pump "Eat & Gas" gas station).

## See also
[[M-M-1 Queue]], [[Kendall's Notation]], [[Little's Law]], [[Traffic Intensity]]
