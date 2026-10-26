---
title: "Little's Law"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [queueing-theory, stochastic-optimization]
---
## Definition
**Little's Law** relates the average number of customers in a [[Queueing System]] to the average rate at which they arrive and the average time each spends in the system:
$$
L = \hat\lambda\, W, \qquad L_q = \hat\lambda\, W_q,
$$
where $L$ is the average number in the system (including whoever is being served), $L_q$ the average number waiting (excluding those in service), $W$ the average time in the system, $W_q$ the average waiting time, and $\hat\lambda$ the **effective** arrival rate (the rate at which customers actually enter the system — equal to the nominal arrival rate $\lambda$ whenever no one is ever blocked, i.e. for infinite-capacity systems).

## Properties
### The four quantities are only two degrees of freedom
Once $L$ (or $L_q$) is computed directly from the steady-state distribution $P_n$ (e.g. $L=\sum_n nP_n$), Little's Law immediately gives $W = L/\hat\lambda$ without any further modeling — and $W = W_q + 1/\mu$ relates waiting time to time in service, so any one of $\{L, L_q, W, W_q\}$ together with $\hat\lambda$ and $\mu$ determines the rest. This is exactly the shortcut used throughout [[M-M-1 Queue]] through [[M-M-s-N Queue]].

### Requires the *effective* arrival rate
Using the nominal $\lambda$ instead of $\hat\lambda$ in a finite-capacity (blocking) system silently overstates $W$ and $W_q$, since some arrivals never actually join the system and so shouldn't count toward the rate driving $L = \hat\lambda W$.

## See also
[[Queueing System]], [[Traffic Intensity]], [[M-M-1 Queue]], [[M-M-1-N Queue]], [[M-M-s Queue]], [[M-M-s-N Queue]]
