---
title: Birth-Death process
domain: Stochastic Processes
course: Stochastic Processes
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A birth-death process $\{N(t), t\geq 0\}$ is a continuous-time homogeneous [[Markov Jump Process|Markov chain]] with state space $\{0,1,2,\dots\}$ such that, as $h\to 0$,
$$
\begin{aligned}
Pr(N(t+h)=n+1 \mid N(t)=n) &= \lambda_n h + o(h), \\
Pr(N(t+h)=n-1 \mid N(t)=n) &= \mu_n h + o(h), \\
Pr(N(t+h)=n \mid N(t)=n) &= 1-(\lambda_n+\mu_n)h + o(h), \\
Pr(N(t+h)=k \mid N(t)=n) &= o(h) \quad\text{for any } k\leq n-2 \text{ or } k\geq n+2.
\end{aligned}
$$
That is: (a) gives the probability of exactly one birth in $(t,t+h]$; (b) exactly one death; (c) no change; (d) more than one birth or death is $o(h)$ (negligible), matching the general infinitesimal structure of any [[Markov Jump Process|Markov jump process]].

This implies the generator matrix (see [[Markov Jump Process]]) is tridiagonal:
$$
Q = \begin{pmatrix}
-\lambda_0 & \lambda_0 & 0 & 0 & \cdots \\
\mu_1 & -(\lambda_1+\mu_1) & \lambda_1 & 0 & \cdots \\
0 & \mu_2 & -(\lambda_2+\mu_2) & \lambda_2 & \cdots \\
0 & 0 & \mu_3 & -(\lambda_3+\mu_3) & \ddots \\
\vdots & \vdots & \vdots & \ddots & \ddots
\end{pmatrix}.
$$
If $\lambda_0=0$, the first row of $Q$ is a zero vector, so state $0$ is an [[Absorbing State|absorbing state]]: once the population hits $0$, it stays there forever (extinction).

## Properties
### Special cases
- **Pure birth process:** $\mu_n=0$ for all $n\geq 1$.
- **Pure death process:** $\lambda_n=0$ for all $n\geq 0$.
- **Linear (simple) birth process:** $\lambda_n = n\lambda$ for all $n\geq 0$, i.e. births occur independently at rate $\lambda$ per individual.
- **Linear (simple) death process:** $\mu_n = n\mu$ for all $n\geq 1$, i.e. deaths occur independently at rate $\mu$ per individual.
- **Linear (simple) birth-death process:** simultaneously a linear birth and a linear death process.

### Linear birth process — derivation of the rate
In a linear birth process, individuals give birth independently at rate $\lambda$. For $n=1,2,3,\dots$,
$$
Pr(N(t+h)=n+1\mid N(t)=n) = Pr(\text{exactly one birth in } (t,t+h]) + o(h) = \binom{n}{1}(\lambda h)^1(1-\lambda h)^{n-1} + o(h).
$$
Since $\binom{n}{1}=n$ and, for $n\geq 2$, $(1-\lambda h)^{n-1}$ expands as $1+a_1(\lambda h)+\cdots+a_{n-1}(\lambda h)^{n-1}$ with the $h^m$ ($m\geq 2$) terms being $o(h)$, this simplifies to $n\lambda h + o(h)$, confirming $\lambda_n = n\lambda$. (The linear death process rate $\mu_n=n\mu$ is derived identically, replacing births with deaths.)

### Stationary distribution
As for any continuous-time Markov chain (see [[Markov Jump Process]] and [[Stationary Distribution]]), the stationary row vector $\pi$ satisfies $\pi Q = 0$ (the continuous-time analogue of $\pi = \pi P$ in discrete time).

## Examples
### Example 1: two-state chain
For $Q = \begin{pmatrix} -\alpha & \alpha \\ \beta & -\beta \end{pmatrix}$, solving $\pi Q=0$ together with $\pi_0+\pi_1=1$ gives $-\alpha\pi_0+\beta\pi_1=0 \Rightarrow \pi_0=\frac{\beta}{\alpha+\beta}$, $\pi_1=\frac{\alpha}{\alpha+\beta}$.

### Example 2: machine repair model
$M$ machines operate independently; each breaks down at rate $\mu$. A single engineer repairs machines one at a time, with i.i.d. repair time $R\sim\text{Exp}(\lambda)$. Letting $X(t)$ = number of *working* machines, "birth" = a repair completing (rate $\lambda_n=\lambda$ for $n=0,\dots,M-1$, $\lambda_M=0$) and "death" = a breakdown (rate $\mu_n = n\mu$, since each of the $n$ working machines can break down independently). For $M=3$,
$$
Q = \begin{pmatrix}
-\lambda & \lambda & 0 & 0 \\
\mu & -\mu-\lambda & \lambda & 0 \\
0 & 2\mu & -2\mu-\lambda & \lambda \\
0 & 0 & 3\mu & -3\mu
\end{pmatrix}.
$$
Solving $\pi Q=0$ with $\sum_{i=0}^3 \pi_i=1$ gives, expressing each $\pi_i$ in terms of $\pi_0$,
$$
\pi_i = \frac{1}{i!}\left(\frac{\lambda}{\mu}\right)^i \pi_0, \qquad \pi_0 = \left(\sum_{i=0}^3 \frac{1}{i!}\left(\frac{\lambda}{\mu}\right)^i\right)^{-1}.
$$
This generalizes to arbitrary $M=m$: $\pi_i = \frac{1}{i!}(\lambda/\mu)^i \pi_0$ for $i=1,\dots,m$, with $\pi_0$ the normalizing constant — a truncated, Poisson-shaped (factorial-denominator) stationary distribution. This arises here because the *death* rate $\mu_n=n\mu$ grows with the state (more working machines means more chances of breakdown), unlike the constant service rate of the vault's [[M-M-1 Queue|M/M/1]]-family notes (which instead give a *geometric* $P_n=\sigma^n P_0$); this machine-repair setup is a finite-source ("repairman problem") variant, related to but distinct from those infinite-source queueing models — see [[Queueing System]] and [[Kendall's Notation]] for the general birth-death view of queues. <!-- UNVERIFIED: the vault's Stochastic Optimization queueing notes don't yet cover the finite-source/repairman-problem case explicitly, so this cross-reference is by analogy, not by a matching vault note. -->

### Example 3: identifying birth/death rates in queueing-style problems (exercise)
A shop has a single owner who serves one customer at a time; customers arrive singly as a Poisson process with rate $0.5$, service times are i.i.d. $\text{Exp}(0.4)$, and the queue has capacity $2$ (so at most $3$ customers total in the shop; arrivals when full balk). Modelling $X(t)$ = number of customers in the shop as a birth-death process: "birth" = a customer arrival (rate $\lambda_n = 0.5$ for $n=0,1,2$, $\lambda_3=0$, since a full queue turns arrivals away), "death" = a service completion (rate $\mu_n = 0.4$ for $n=1,2,3$, since only one customer is served at a time regardless of queue length). This is precisely the birth-death structure underlying the [[M-M-1-N Queue|M/M/1/N queue]]. (A variant of the same exercise, where the owner can serve up to two customers simultaneously, gives death rate $\mu_n = 0.4\min(n,2)$ — an $M/M/2/N$-type queue.)

## See also
- [[Markov Jump Process]]
- [[Kolmogorov Forward Equations]]
- [[Stationary Distribution]]
- [[Absorbing State]]
- [[Poisson Process]]
- [[M-M-1 Queue]]
- [[M-M-1-N Queue]]
- [[M-M-s Queue]]
- [[M-M-s-N Queue]]
- [[Queueing System]]
- [[Kendall's Notation]]
- [[Exponential distribution]]
