---
title: State space and time classification
domain: Stochastic Processes
course: Stochastic Processes
unit: Foundations & Random Walks
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A [[Stochastic Process|stochastic process]] $\{X_t : t \in T\}$ can be classified along two independent axes: whether its state space $S$ is discrete or continuous, and whether its index (time) set $T$ is discrete or continuous. Combining these gives four basic types, plus a fifth "mixed type" for processes that combine discrete- and continuous-time behaviour.

## Properties
### The four basic combinations
1. **Discrete state space, discrete time.** Both $S$ and $T$ are discrete (e.g. $T = \{0, 1, 2, \dots\}$).
2. **Discrete state space, continuous time.** $S$ is discrete but $T$ is a continuous interval (e.g. $T = [0, \infty)$).
3. **Continuous state space, discrete time.** $S$ is a continuous set (e.g. $[0,\infty)$) but $T$ is discrete.
4. **Continuous state space, continuous time.** Both $S$ and $T$ are continuous.

### Mixed type
A process can also operate in discrete time while additionally changing value at random (continuously-indexed) time points — a combination, or mixture, of a discrete-time and a continuous-time process. Such a process is said to be of **mixed type**.

## Examples
- *Discrete/discrete:* A motor insurer reviews each customer's discount level (0%, 25%, 40%) yearly based on their accident record; the number of claims of a policyholder is a process with state space $S = \{0, 1, 2, \dots\}$ and time set $T = \{0, 1, 2, \dots\}$ (years).
- *Discrete/continuous:* A pension plan classifies pensioners as Alive (A), Sick (S), or Dead (D); the state space is discrete, $S = \{A, S, D\}$, but the time set is continuous, $T = [0, \infty)$, since a transition (e.g. death) can occur at any time.
- *Continuous/discrete:* The daily closing value $P_t$ of a stock portfolio has a continuous state space $S = [0,\infty)$ but a discrete time set $T = \{0,1,2,\dots\}$ (trading days). Many financial and economic time series (stock prices and returns, interest rates, inflation) share this structure.
- *Continuous/continuous:* The total claim amount $X_t$ up to time $t$ for a portfolio of third-party liability policies has continuous state space $S = [0,\infty)$ and continuous time set $T = [0,\infty)$, since accidents (and hence claims) can occur at any time.
- *Mixed type:* The payments made by a life insurer for a health policy combine (i) an annual check-up cost, a discrete-time process with continuous state space $S=[0,\infty)$, $T=\{1,2,3,\dots\}$, and (ii) medical-treatment costs incurred at random times when the policyholder falls sick, a continuous-time process with $S = [0,\infty)$, $T = [0,\infty)$.

## See also
- [[Stochastic Process]]
- [[Random Walk]]
