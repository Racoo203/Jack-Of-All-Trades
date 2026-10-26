---
title: "Queueing System"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [queueing-theory, stochastic-optimization]
---
## Definition
A **queueing system** (línea de espera) models customers arriving to compete for a limited number of servers, waiting when all servers are busy, and eventually being served and leaving. Formally, the number of customers present at time $t$ is a stochastic process on state space $\Omega_S \subseteq \mathbb{N} = \{0,1,\dots,N\}$ with associated occurrence probabilities $\{P_0, P_1,\dots,P_N\}$ — a [[Birth-Death process|birth-death process]]: transitions only ever move the state up by one (an arrival) or down by one (a service completion), never by more than one at a time.

A system is fully specified by: the arrival process, the service process, the number of servers $s$, the queue discipline (e.g. FCFS — first-come-first-served), the system's total capacity $N = s + c$ (servers plus waiting room $c$), and the size of the source population — see [[Kendall's Notation]] for the standard shorthand encoding these.

## Properties
### Steady-state probabilities from transition data
Given a one-step transition matrix $P$ estimated from observed data (e.g. counting how often the system moved from $n$ customers to $n'$ customers between consecutive observations), the steady-state probabilities solve the same balance equations as any [[Stationary Distribution]]: $P_j = \sum_i P_i P_{ij}\ \forall j$, together with $\sum_j P_j = 1$.

### Worked example: doctor's office
From 73 observations spaced 5 minutes apart, classifying transitions between $\{0,1,2,3,4\}$ patients present gives an empirical transition matrix $P_{01}$; solving $\pi = \pi P_{01}$ gives $\pi \approx (0.3548, 0.3104, 0.1219, 0.0399, 0.1729)$, from which the average queue length (excluding whoever is being served, $s=1$) is
$$
L_q = \sum_{n=1}^{N}(n-1)P_n = 0.7204 \text{ patients}.
$$
(Note: $W = L/\lambda$ could not be completed in this example since $\lambda$ — the arrival rate — was not separately estimated from the data; this is exactly what [[Little's Law]] needs.)

## Examples
The gas-station, taxi-dispatch, and carwash examples throughout this course (see [[M-M-1 Queue]] through [[M-M-s-N Queue]]) are all instances of this general birth-death framework, specialized to Markovian (exponential) arrivals and service times.

## See also
[[Kendall's Notation]], [[Traffic Intensity]], [[Little's Law]], [[M-M-1 Queue]], [[M-M-1-N Queue]], [[M-M-s Queue]], [[M-M-s-N Queue]], [[Birth-Death process]]
