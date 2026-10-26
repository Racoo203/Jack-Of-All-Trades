---
title: Stationary Distribution
domain: Stochastic Processes
course: Stochastic Processes
unit: Discrete-Time Markov Chains
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A probability row vector $\pi = (\pi_1, \dots, \pi_m)$ is a **stationary distribution** of a discrete-time, time-homogeneous [[Discrete-Time Markov Chain]] $\{X_n\}$ with [[Transition Matrix]] $P$ if
$$
\pi = \pi P.
$$

Remarks:
- If $p^{(0)} = \pi$, then $p^{(n)} = \pi$ for every $n \ge 1$ — if the chain *starts* in $\pi$, it stays there.
- If $p^{(n)} = \pi$ for some $n$, then $p^{(m)} = \pi$ for every $m > n$ — once the chain *arrives* at $\pi$, it stays there.
- Consequently $\pi = \pi P^{(n)}$ for every $n \ge 1$.

In practice $\pi$ is found by solving the linear system $\pi = \pi P$ together with the normalisation $\sum_i \pi_i = 1$. Because the rows of $P$ each sum to 1, the $m$ equations of $\pi = \pi P$ are linearly dependent, so it suffices to solve any $m-1$ of them together with the normalisation equation.

## Properties
### General balance equations characterise stationarity
**Lemma.** A probability row vector $\pi$ satisfies the *general balance equations*
$$
\pi_i = \sum_{j \in S} \pi_j p_{ji} \quad \text{for all } i \in S \tag{$\ast$}
$$
if and only if $\pi$ is a stationary distribution.

*Proof.* The right-hand side of ($\ast$) is exactly the $i$-th coordinate of $\pi P$ (multiplying $\pi$ into the $i$-th column of $P$), i.e. $\sum_{j} \pi_j p_{ji} = (\pi P)_i$. For the left-hand side, using $\sum_{j} p_{ij} = 1$,
$$
\pi_i = \pi_i \sum_{j \in S} p_{ij} = \sum_{j \in S} \pi_i p_{ij}.
$$
So ($\ast$) reads $\sum_j \pi_i p_{ij} = (\pi P)_i$ for every $i$, i.e. in matrix form $\pi = \pi P$. $\blacksquare$

Interpretation: the left-hand side is the total probability *leaving* state $i$ in one step, and the right-hand side is the total probability *entering* $i$; $\pi$ is stationary exactly when the chain is "balanced" state by state — see [[Transition Graph]] for the flow picture.

The stronger *detailed* balance equations $\pi_i p_{ij} = \pi_j p_{ji}$ for all $i, j$ imply the general balance equations (sum over $j$) and are computationally convenient when they hold, but a stationary $\pi$ need not satisfy them. For example, the 3-state cyclic chain
$$
P = \begin{bmatrix} 0 & 1/4 & 3/4 \\ 3/4 & 0 & 1/4 \\ 1/4 & 3/4 & 0 \end{bmatrix}
$$
has stationary distribution $\pi = (1/3, 1/3, 1/3)$ (which does satisfy general balance), but $\pi_1 p_{12} = \tfrac13\cdot\tfrac14 = \tfrac1{12} \ne \tfrac14 = \tfrac13\cdot\tfrac34 = \pi_2 p_{21}$, so detailed balance fails — and in fact no probability vector satisfies detailed balance for this particular $P$.

### Non-uniqueness on a reducible chain
If the chain is not [[Irreducible Class|irreducible]], the stationary distribution need not be unique. Consider $S = \{1,2,3,4\}$ with two disjoint closed classes $C_1 = \{1,2\}$, $C_2=\{3,4\}$ (transition matrix block-diagonal on these classes). Solving $\pi = \pi P$ gives only $m - 2$ independent constraints instead of $m-1$ (one redundant equation per closed class), so the solution set is a line segment of stationary distributions
$$
\pi = \Big(x,\ 2x,\ \tfrac{5(1-3x)}{11},\ \tfrac{6(1-3x)}{11}\Big), \qquad x \in [0, \tfrac13],
$$
interpolating between $\pi(C_1) = (1/3, 2/3, 0, 0)$ (reached from any start inside $C_1$) and $\pi(C_2) = (0,0,5/11,6/11)$ (reached from any start inside $C_2$).

**Remark.** If a Markov chain has at least two distinct stationary distributions, it automatically has infinitely many, since every convex combination of two stationary distributions is again stationary ($\pi = \pi P$ is a linear condition). This is why irreducibility is needed for $\pi$ to be unique — see [[Equilibrium Distribution]] for when it is additionally the long-run limit of $p^{(0)}P^n$.

## Examples
For the 3-state cycle $P = \begin{bmatrix}1-p & p & 0\\ 0 & 1-p & p \\ p & 0 & 1-p\end{bmatrix}$ ($0<p<1$), solving $\pi = \pi P$ gives $\pi_1=\pi_3$, $\pi_2=\pi_1$, $\pi_3=\pi_2$, so with normalisation $\pi = (1/3,1/3,1/3)$ — independent of $p$.

A No-Claims-Discount insurance scheme with 4 discount levels and $\Pr(N{=}0)=0.9$ (move up a level on a claim-free year, else reset to the bottom) has transition matrix
$$
P=\begin{bmatrix}0.1&0.9&0&0\\0.1&0&0.9&0\\0.1&0&0&0.9\\0&0.1&0&0.9\end{bmatrix},
$$
giving stationary distribution $\pi = (0.02, 0.1, 0.09, 0.79)$: most policyholders end up at the top discount level. A less claim-free portfolio with $\Pr(N{=}0)=0.5$ instead gives $\pi^*=(0.43,0.29,0.14,0.14)$ — skewed toward the *bottom* levels, showing how sensitive $\pi$ is to the transition probabilities.

## See also
- [[Equilibrium Distribution]]
- [[Discrete-Time Markov Chain]]
- [[Transition Matrix]]
- [[Transition Graph]]
- [[Irreducible Class]]
