---
title: "Kendall's Notation"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [queueing-theory, stochastic-optimization]
---
## Definition
**Kendall's notation** classifies a [[Queueing System]] with a slash-separated code, most compactly $A/B/s$ (arrival process / service process / number of servers) and, in full, $A/B/s/(\text{discipline}/\text{capacity}/\text{source size})$. Common symbols: $M$ (Markovian — exponential interarrival or service times, equivalently Poisson arrivals), $D$ (deterministic), $G$ (general). This course works exclusively with $M/M/\cdot$ systems.

## Properties
### Reading a full specification
$(M/M/S)/(FCFS/N/\infty)$ denotes: Poisson arrivals, exponential service, $S$ servers, first-come-first-served discipline, total system capacity $N$ (servers plus queue), and an infinite calling population. Dropping the capacity term (or writing $\infty$ there) gives the infinite-capacity variants; dropping the source-size term similarly assumes an infinite population of potential customers, which is the default assumption throughout this course unless stated otherwise.

### The course's four worked configurations
Combining $s=1$ vs. $s>1$ with finite vs. infinite capacity gives the four models worked in detail: [[M-M-1 Queue]] $= (M/M/1)/(FCFS/\infty/\infty)$, [[M-M-1-N Queue]] $=(M/M/1)/(FCFS/N/\infty)$, [[M-M-s Queue]] $=(M/M/s{>}1)/(-/\infty/-)$, [[M-M-s-N Queue]] $=(M/M/s{>}1)/(-/N/-)$.

## See also
[[Queueing System]], [[M-M-1 Queue]], [[M-M-1-N Queue]], [[M-M-s Queue]], [[M-M-s-N Queue]]
