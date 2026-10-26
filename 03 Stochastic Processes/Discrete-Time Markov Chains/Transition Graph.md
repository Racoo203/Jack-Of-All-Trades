---
title: Transition Graph
domain: Stochastic Processes
course: Stochastic Processes
unit: Discrete-Time Markov Chains
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A **transition graph** (or **transition diagram**) of a [[Discrete-Time Markov Chain]] with state space $S$ and [[Transition Matrix]] $P$ is a directed, weighted graph $(S, E)$ where
- the vertices are the states of $S$;
- there is a directed edge $i \to j$ whenever $p_{ij} > 0$, labelled with the transition probability $p_{ij}$;
- a self-loop at $i$ (edge $i \to i$) is drawn whenever $p_{ii} > 0$.

Since every row of $P$ sums to $1$, the edges leaving any vertex $i$ (including its self-loop, if present) always have weights summing to $1$. The transition graph is a pictorial encoding of $P$, and every property of $P$ that depends only on which entries are positive (as opposed to their exact values) can be read directly off the graph.

## Properties
### Accessibility read off the graph
State $j$ is **accessible** from state $i$ (written $i \to j$) if $p_{ij}^{(n)} > 0$ for some $n \ge 0$. On the transition graph this happens exactly when there is a directed path from $i$ to $j$ — because $p_{ij}^{(n)} > 0$ iff some length-$n$ walk from $i$ to $j$ has every step-probability positive, which is exactly a directed path of length $n$ in the graph. Two states **communicate** ($i \leftrightarrow j$) iff $i \to j$ and $j \to i$, i.e. iff $i$ and $j$ lie on a common directed cycle (or are the same state). See [[Irreducible Class]] for how this partitions $S$.

### Balance equations as a flow condition on the graph
Writing the [[Stationary Distribution]] equation $\pi = \pi P$ componentwise gives the **general balance equations**
$$
\pi_i = \sum_{j \in S} \pi_i p_{ij} = \sum_{j \in S} \pi_j p_{ji} \quad \text{for all } i \in S,
$$
i.e. for every state $i$, the total probability *flow out* of $i$ equals the total probability *flow into* $i$. On the transition graph this is a literal flow-balance condition at each vertex, which is why a stationary $\pi$ is often found by "cutting" the graph and balancing flow across the cut.

The stronger **detailed balance equations**, $\pi_i p_{ij} = \pi_j p_{ji}$ for all $i,j \in S$, require the flow along *each individual edge pair* $i \leftrightarrow j$ to balance, not just the total flow at each vertex. A $\pi$ satisfying detailed balance always satisfies general balance (summing over $j$ recovers it), but not conversely: e.g. for the cyclic chain $P=\begin{bmatrix}0&1/4&3/4\\3/4&0&1/4\\1/4&3/4&0\end{bmatrix}$, $\pi=(1/3,1/3,1/3)$ satisfies general balance but not detailed balance ($\pi_1 p_{12}=1/12 \ne 1/4 = \pi_2 p_{21}$), and in fact no probability vector satisfies detailed balance for this $P$ (see [[Stationary Distribution]] for the full derivation).

## Examples
The **Bonus-Malus** premium-class chain (insurance no-claims-discount schemes) is a standard transition-graph example: states are premium classes, and edges move a policyholder up one class on a claim-free period and down (by 1, 2, or more classes) after one or more claims, with edge weights $\alpha_k = e^{-\lambda}\lambda^k/k!$ given by a Poisson claim count. E.g. for a 4-class scheme with claim probabilities $\alpha_0, \alpha_1, \alpha_2$,
$$
P = \begin{bmatrix}
\alpha_0 & \alpha_1 & \alpha_2 & 1-\alpha_0-\alpha_1-\alpha_2 \\
\alpha_0 & 0 & \alpha_1 & 1-\alpha_0-\alpha_1 \\
0 & \alpha_0 & 0 & 1-\alpha_0 \\
0 & 0 & \alpha_0 & 1-\alpha_0
\end{bmatrix},
$$
drawn as a graph with mostly-forward edges (toward the top discount class) and a few "reset toward the bottom" edges after a bad claim year.

The **Ehrenfest model** (two urns, $m$ balls, one ball moved at random each step) gives a transition graph that is a simple path $0 \leftrightarrow 1 \leftrightarrow 2 \leftrightarrow \cdots \leftrightarrow m$ with no self-loops — every edge changes the state by exactly $\pm1$. This bipartite structure (even states can only reach odd states in one step, and vice versa) is what makes the chain irreducible yet [[Period of States|periodic]] with period 2 (see that note).

## See also
- [[Discrete-Time Markov Chain]]
- [[Transition Matrix]]
- [[Chapman-Kolmogorov Equation]]
- [[Irreducible Class]]
- [[Stationary Distribution]]
- [[Period of States]]
