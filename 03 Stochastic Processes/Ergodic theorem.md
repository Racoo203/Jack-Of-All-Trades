---
title: Ergodic theorem
domain: Stochastic Processes
course: Stochastic Processes
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A state $j$ of a [[Discrete-Time Markov Chain|discrete-time Markov chain]] is **ergodic** if it is both positive [[Recurrent State|recurrent]] (finite [[Mean Recurrence Time|mean recurrence time]]) and aperiodic (see [[Period of States]]). A chain is ergodic if it is [[Irreducible Class|irreducible]] and every state is ergodic — since recurrence, positive recurrence, and periodicity are all class properties on an irreducible chain, it suffices for *one* state to be positive recurrent and aperiodic.

A convenient sufficient condition: an irreducible chain is ergodic if it is **regular**, i.e. some power $P^{(n)}$ of its transition matrix has every entry strictly positive.

## Properties
### The ergodic (main limit) theorem for Markov chains
For an irreducible, ergodic chain with finite state space and transition matrix $P$, the full statement and proof of the convergence result — a unique stationary distribution $\pi$ exists, $p_{ij}^{(n)} \to \pi_j$ for every $i,j$ regardless of starting state, $\pi$ equals the chain's [[Equilibrium Distribution|equilibrium distribution]], and $\pi_j = 1/\mu_j$ in terms of the mean recurrence time $\mu_j$ — is given in [[Equilibrium Distribution]] (kept there to avoid duplicating the derivation).

### Ergodicity vs. mere stationarity
Ergodicity is strictly stronger than merely having *a* stationary distribution: a chain can be irreducible with a unique stationary distribution yet fail to converge to it (if it is periodic), and a reducible chain can have infinitely many stationary distributions (no single equilibrium limit). See [[Equilibrium Distribution]] for both worked counter-examples.

### Relation to the optimization-domain notion of ergodicity
This vault also has a note on [[Ergodic Markov Chain]] from a different course's treatment of Markov chains (Stochastic Optimization). The underlying concept is the same standard Markov-chain-theory notion of ergodicity described here; the two notes exist because they were seeded from two different courses' lecture material and have not yet been merged into one canonical note — see that note for a complementary presentation and for the [[Spectral Decomposition of a Transition Matrix|spectral]] point of view on the same convergence result.

## See also
- [[Equilibrium Distribution]]
- [[Stationary Distribution]]
- [[Irreducible Class]]
- [[Period of States]]
- [[Recurrent State]]
- [[Mean Recurrence Time]]
- [[Ergodic Markov Chain]]
