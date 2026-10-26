---
title: "M/M/1 Queue"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [queueing-theory, stochastic-optimization]
---
## Definition
The $(M/M/1)$ queue — full [[Kendall's Notation]] $(M/M/1)/(FCFS/\infty/\infty)$ — is a single-server [[Queueing System]] with Poisson arrivals at rate $\lambda$, exponential service at rate $\mu$, unlimited queueing capacity, and an infinite calling population. As a [[Birth-Death process]] on the number-in-system $n$, over a small interval $\Delta t$ the one-step transition probabilities are: birth (arrival) with probability $\lambda\Delta t$, death (service completion, only possible if $n\ge1$) with probability $\mu\Delta t$, and no change otherwise.

## Properties
### Steady-state balance equations and $P_n = \sigma^n P_0$
Writing the balance equations $P_n = \sum_i P_i P_{i,n}$ from the birth-death transition structure and taking $\Delta t \to 0$ gives, for every $n\ge1$,
$$
P_n = \left(\frac{\lambda}{\mu}\right)^n P_0 = \sigma^n P_0, \qquad \sigma = \lambda/\mu,
$$
and normalizing $\sum_{n=0}^\infty P_n = 1$ (a geometric series, convergent iff $\sigma<1$) gives $P_0 = 1-\sigma$. Hence
$$
P_n = (1-\sigma)\sigma^n, \qquad n = 0, 1, 2, \dots
$$
### Deriving $L$, $L_q$, $W$, $W_q$
$$
L = \sum_{n=0}^\infty nP_n = (1-\sigma)\sum_{n=0}^\infty n\sigma^n = (1-\sigma)\,\sigma\frac{d}{d\sigma}\sum_{n=0}^\infty \sigma^n = (1-\sigma)\,\sigma\frac{d}{d\sigma}\frac{1}{1-\sigma} = \frac{\sigma}{1-\sigma} = \frac{\lambda}{\mu-\lambda}.
$$
By [[Little's Law]] (using $\hat\lambda=\lambda$, since no arrivals are ever blocked here),
$$
W = \frac{L}{\lambda} = \frac{1}{\mu-\lambda}, \qquad W_q = W - \frac1\mu = \frac{1}{\mu-\lambda}-\frac1\mu = \frac{\lambda}{\mu(\mu-\lambda)}, \qquad L_q = \lambda W_q = \frac{\lambda^2}{\mu(\mu-\lambda)}.
$$
All four quantities require $\sigma = \lambda/\mu < 1$ (see [[Traffic Intensity]]) for the steady state to exist.

## Examples
A waiting room with capacity 3 (so $N=4$ including the one being served) receiving $\lambda=8$/hour with $\mu=6$/hour is actually a *finite*-capacity variant — see [[M-M-1-N Queue]] for the corresponding worked balking calculation with these same numbers.

## See also
[[Queueing System]], [[Kendall's Notation]], [[Traffic Intensity]], [[Little's Law]], [[M-M-1-N Queue]], [[M-M-s Queue]]
