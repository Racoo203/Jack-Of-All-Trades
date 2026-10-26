---
title: Absorbing State
domain: Stochastic Processes
course: Stochastic Processes
unit: State Classification & Periodicity
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A state $i$ is an **absorbing state** if it forms a closed class of size one on its own, i.e. $p_{ii} = 1$ (equivalently, $p_{ij}=0$ for every $j \ne i$): once the chain hits $i$, it stays in $i$ forever. Equivalently, $i$ is absorbing iff it is a single-state [[Irreducible Class|irreducible closed class]].

## Properties
### Expected time to absorption (first-step analysis)
Let $T_i$ be the number of steps until absorption, given the chain starts in state $i$, and $E(T_i)$ its expectation. If $i$ is itself absorbing, $E(T_i) = 0$. For a transient state $i$, condition on the first move $Z$ (the state reached after one step):
$$
E(T_i) = \sum_{j \in S} \big(1 + E(T_j)\big)\, p_{ij} = 1 + \sum_{j \in S} p_{ij}\, E(T_j),
$$
using $\sum_j p_{ij} = 1$ and $E(T_j) = 0$ for every absorbing $j$. This gives one linear equation per transient state, solved simultaneously for all the $E(T_i)$.

**Worked example.** For $S=\{1,2,3\}$ with
$$
P = \begin{bmatrix} 1/3 & 1/3 & 1/3 \\ 0 & 1/2 & 1/2 \\ 0 & 0 & 1 \end{bmatrix},
$$
state 3 is absorbing ($p_{33}=1$, $p_{31}=p_{32}=0$). Writing $E(T_3)=0$, first-step analysis gives
$$
E(T_1) = 1 + \tfrac13 E(T_1) + \tfrac13 E(T_2), \qquad E(T_2) = 1 + \tfrac12 E(T_2).
$$
The second equation gives $E(T_2) = 2$; substituting into the first, $\tfrac23 E(T_1) = 1 + \tfrac13(2) = \tfrac53$, so $E(T_1) = \tfrac52$. Starting from state 1, the chain is expected to take $2.5$ steps before it is absorbed into state 3.

### Relation to recurrence
An absorbing state is automatically [[Recurrent State|recurrent]] with $f_i = 1$ trivially (it returns to itself with probability 1, in one step). In the [[Gambler's Ruin]] problem, the two boundary states $0$ and $N$ (the gambler is ruined, or reaches their target fortune) are exactly the absorbing states of the chain.

## See also
- [[Irreducible Class]]
- [[Recurrent State]]
- [[Transient State]]
- [[Discrete-Time Markov Chain]]
- [[Gambler's Ruin]]
