---
title: Markov Property
domain: Stochastic Processes
course: Stochastic Processes
unit: Foundations & Random Walks
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
Consider a set of time instants $\{t_0, t_1, \dots, t_n\}$ with $t_0 < t_1 < \dots < t_n$ and $t_i \in T$ for $i = 1, \dots, n$. A [[Stochastic Process|stochastic process]] $\{X_t, t \in T\}$ is said to have the Markov property if
$$
Pr(X_{t_n} = x_n \mid X_{t_{n-1}} = x_{n-1}, X_{t_{n-2}} = x_{n-2}, \dots, X_{t_0} = x_0) = Pr(X_{t_n} = x_n \mid X_{t_{n-1}} = x_{n-1})
$$
That is, the conditional distribution of the process at a future time, given the whole past up to the present, depends only on the present state — not on how the process got there.

## Properties
### Interpretation
The Markov property is the simplest non-trivial dependence structure a stochastic process can have: it states that the future evolution of the process depends on its present position only, and not on its past positions. This is a strong simplifying assumption relative to a fully general (non-Markov) dependence structure, where the future could in principle depend on the entire history.

A canonical illustrative example is a Healthy–Sick–Dead (HSD) model for an individual's health, with transition rates $\sigma$ (Healthy → Sick), $\rho$ (Sick → Healthy), $\mu$ (Healthy → Dead) and $\nu$ (Sick → Dead). If there is a full recovery from Sick back to Healthy, then under the Markov property, an individual's past sickness history has no bearing on their future health prospects — only their *current* state (Healthy, Sick, or Dead) determines the transition probabilities going forward.

### Instances
The Markov property holds for, among others:
- every [[Random Walk|random walk]] — see [[Simple Random Walk]] for the proof in the simple case, which generalizes to any random walk with i.i.d. increments;
- every [[Discrete-Time Markov Chain|discrete-time Markov chain]], which is in fact *defined* as a stochastic process on a discrete state space satisfying the Markov property;
- every [[Markov Jump Process|continuous-time Markov (jump) process]].

## See also
- [[Stochastic Process]]
- [[Simple Random Walk]]
- [[Discrete-Time Markov Chain]]
- [[Markov Jump Process]]
