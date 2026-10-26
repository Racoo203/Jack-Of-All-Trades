---
title: Generator Matrix
domain: Stochastic Processes
course: Stochastic Processes
unit: Continuous-Time & Jump Processes
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
For a time-homogeneous [[Markov Jump Process|continuous-time Markov chain]] with transition probabilities $p_{ij}(t)$, suppose $P(t)$ is continuous at $t=0$ and the entries
$$
q_{ij} := p_{ij}'(0) = \lim_{t \to 0} \frac{p_{ij}(t) - p_{ij}(0)}{t}
$$
exist and are finite for all $i, j$. The matrix $Q = (q_{ij})$ is the **generator matrix** (or **rate matrix** / **intensity matrix**) of the chain. Equivalently, $Q$ arises from the small-$t$ expansion
$$
P(t) = I + Qt + o(t) \qquad (t \to 0).
$$

## Properties
### Row sums and sign pattern
Since $\sum_j p_{ij}(t) = 1$ for every $t \geq 0$, differentiating (or substituting the expansion above) at $t=0$ gives $\sum_j q_{ij} = 0$ for every row $i$, i.e.
$$
q_{ii} = -\sum_{j \neq i} q_{ij}.
$$
Off-diagonal entries are non-negative, $q_{ij} \geq 0$ for $j \neq i$ (they are instantaneous transition *rates*, not probabilities), and diagonal entries are non-positive, $q_{ii} \leq 0$. An absorbing state $i$ (one the chain never leaves) has an entirely zero row, $q_{ij} = 0$ for all $j$, including $q_{ii} = 0$ — note this is a transition *rate* of zero, even though the transition *probability* $p_{ii}(t) = 1$ for all $t$.

### Role: the continuous-time analogue of the transition matrix
$Q$ plays the role for a continuous-time chain that the one-step [[Transition Matrix|transition matrix]] $P$ plays for a [[Discrete-Time Markov Chain|discrete-time chain]]: a homogeneous CTMC is fully determined by its initial distribution together with $Q$, exactly as a DTMC is determined by its initial distribution together with $P$. The [[Kolmogorov Forward Equations|Kolmogorov forward and backward equations]], $P'(t) = P(t)Q$ and $P'(t) = QP(t)$, recover the whole family $\{P(t)\}_{t \geq 0}$ from $Q$ alone (formally, $P(t) = e^{Qt}$).

### Holding times and jump probabilities
The generator matrix's entries have a direct probabilistic meaning for the chain's behaviour: the time spent in state $i$ before leaving (the *holding time*) is exponentially distributed with rate $-q_{ii} = \sum_{j \neq i} q_{ij}$, and upon leaving $i$, the chain jumps to state $j \neq i$ with probability $q_{ij} / (-q_{ii})$. See [[Markov Jump Process]] for the full derivations and a maximum-likelihood method for estimating the $q_{ij}$ from observed holding times.

## Examples
### The Poisson process
The [[Poisson Process|Poisson process]] with rate $\lambda$ is the continuous-time chain on $S = \{0, 1, 2, \dots\}$ with generator matrix entries $q_{i,i+1} = \lambda$, $q_{ii} = -\lambda$, and $q_{ij} = 0$ otherwise — i.e. from any state the chain can only move one step up, at rate $\lambda$.

## See also
- [[Markov Jump Process]]
- [[Kolmogorov Forward Equations]]
- [[Poisson Process]]
- [[Transition Matrix]]
- [[Discrete-Time Markov Chain]]
