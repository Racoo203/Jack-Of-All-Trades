---
title: Counting Process
domain: Stochastic Processes
course: Stochastic Processes
unit: Foundations & Random Walks
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A [[Stochastic Process|stochastic process]] $\{N_t, t \geq 0\}$ is a counting process if $N_t$ represents the total number of events that have occurred up to (and including) time $t$. A counting process must satisfy:
- $N_t \geq 0$;
- $N_t$ is integer-valued;
- if $s < t$, then $N_s \leq N_t$ (non-decreasing);
- for $s < t$, $N_t - N_s$ equals the number of events that occurred in the interval $(s, t]$.

## Properties
### Specializations
Two important special cases of a counting process, in increasing order of restrictiveness, are:
- the [[Renewal process|renewal process]], where the inter-event times are i.i.d.;
- the [[Poisson Process|Poisson process]], the further special case where those i.i.d. inter-event times are exponentially distributed (equivalently, where increments over disjoint intervals are independent and Poisson-distributed).

## Examples
Counting processes are used to model, e.g., the number of insurance claims received by a portfolio up to time $t$, or the number of buses that have arrived at a stop up to time $t$.

## See also
- [[Renewal process]]
- [[Poisson Process]]
- [[Stochastic Process]]
