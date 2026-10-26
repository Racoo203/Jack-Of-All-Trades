---
title: Renewal process
domain: Stochastic Processes
course: Stochastic Processes
unit: Foundations & Random Walks
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
Consider a lightbulb that is installed and, upon failure, immediately replaced by a new one; the lifetimes of successive lightbulbs are assumed [[Independent and Identically Distributed (i.i.d)|i.i.d.]]. The stochastic process $\{N_t, t \geq 0\}$, where $N_t$ is the number of renewals (replacements) that have occurred up to time $t$, is called a renewal process.

## Properties
### Relation to counting processes
A renewal process is a particular case of a [[Counting Process|counting process]]: it satisfies $N_t \geq 0$, is integer-valued, is non-decreasing in $t$, and $N_t - N_s$ counts the number of renewals in $(s,t]$. What distinguishes a renewal process among counting processes is that the times *between* successive events (the inter-renewal, or inter-arrival, times) are i.i.d.

### Relation to the Poisson process
When the i.i.d. inter-renewal times are further assumed to be exponentially distributed, the renewal process becomes a [[Poisson Process|Poisson process]]. The Poisson process is therefore a special case of a renewal process, which is in turn a special case of a counting process.

## See also
- [[Counting Process]]
- [[Poisson Process]]
- [[Stochastic Process]]
