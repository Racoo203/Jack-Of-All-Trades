---
title: Equilibrium Distribution
domain: Stochastic Processes
course: Stochastic Processes
unit: Discrete-Time Markov Chains
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
Consider a discrete-time, time-homogeneous [[Discrete-Time Markov Chain]] $\{X_n\}$ with a unique [[Stationary Distribution]] $\pi$. If, for *every* initial distribution $p^{(0)}$,
$$
\lim_{n\to\infty} p^{(0)} P^n = \pi,
$$
then $\pi$ is called the **equilibrium distribution** of the chain.

This is strictly stronger than stationarity: a chain can have a stationary distribution without having an equilibrium distribution, either because the stationary distribution is not unique (reducible chains, see [[Stationary Distribution]]) or because $P^n$ does not converge even though a unique $\pi$ exists (periodic chains, see [[Period of States]] and the reflecting-barrier example below).

## Properties
### Main Limit Theorem (Ergodic Theorem) for Markov chains
**Theorem.** Let $\{X_n\}$ be an irreducible, ergodic (positive recurrent + aperiodic) Markov chain with transition matrix $P$ and finite state space $S=\{1,\dots,m\}$. Then
(a) there is a unique probability row vector $\pi$ with $\pi = \pi P$;
(b) $\pi$ is the equilibrium distribution of the chain;
(c) for all $i,j \in S$, $p_{ij}^{(n)} \to \pi_j$ as $n \to \infty$ (every row of $P^{(n)}$ converges to $\pi$);
(d) $\pi_j = 1/\mu_j$ for all $j \in S$, where $\mu_j$ is the [[Mean Recurrence Time|mean recurrence time]] of state $j$.

See [[Ergodic theorem]] for further discussion. A convenient sufficient criterion: an irreducible chain is ergodic iff it is **regular**, i.e. some power $P^{(n)}$ has *all* entries strictly positive.

### Two interpretations of $\pi_j$
Part (c) says $\pi_j$ is the approximate probability of finding the chain in state $j$ after it has run a long time. A second interpretation — $\pi_j$ is also the long-run *proportion of time* the chain spends in $j$ — is derived as follows. Let $I_n = \mathbb{1}\{X_n = j\}$, so the number of visits to $j$ in the first $M$ steps is $\sum_{n=1}^M I_n$. Conditioning on $X_0 = i$,
$$
E\!\left[\sum_{n=1}^M I_n \,\middle|\, X_0=i\right] = \sum_{n=1}^M \Pr(X_n=j\mid X_0=i) = \sum_{n=1}^M p_{ij}^{(n)},
$$
so the expected proportion of time in $j$ up to time $M$ is $\frac{1}{M}\sum_{n=1}^M p_{ij}^{(n)}$. Since $p_{ij}^{(n)} \to \pi_j$ as $n \to \infty$ (part (c)), the Cesàro average of a convergent sequence converges to the same limit:
$$
\lim_{M \to \infty} \frac{1}{M}\sum_{n=1}^M p_{ij}^{(n)} = \pi_j.
$$

### Worked derivation: the two-state chain always has an equilibrium distribution
For $S=\{1,2\}$ and $P = \begin{bmatrix}1-a & a \\ b & 1-b\end{bmatrix}$ with $a,b \in (0,1)$ (so $P$ is regular, hence ergodic), diagonalising $P$ gives eigenvalues $\lambda_1 = 1$, $\lambda_2 = 1-a-b$ with $|\lambda_2| < 1$, and
$$
P^n = \frac{1}{a+b}\begin{bmatrix} b + a(1-a-b)^n & a - a(1-a-b)^n \\ b - b(1-a-b)^n & a + b(1-a-b)^n \end{bmatrix} \xrightarrow[n\to\infty]{} \frac{1}{a+b}\begin{bmatrix} b & a \\ b & a\end{bmatrix},
$$
since $(1-a-b)^n \to 0$. Every row converges to $\pi = \left(\frac{b}{a+b}, \frac{a}{a+b}\right)$, and since the limit of $P^n$ exists, $\lim_n p^{(0)}P^n = p^{(0)}\cdot \lim_n P^n = \pi$ for *any* $p^{(0)}$ (using $p^{(0)}\mathbf{1}=1$) — confirming $\pi$ is the equilibrium distribution regardless of the starting state.

### Counter-examples: stationary but not equilibrium
- **Reducible chain, two closed classes.** As in [[Stationary Distribution]], a chain with closed classes $C_1=\{1,2\}$, $C_2=\{3,4\}$ has infinitely many stationary distributions, so no single $\pi$ can be *the* limit for every $p^{(0)}$ — there is no equilibrium distribution.
- **Periodic chain, unique stationary distribution, no limit.** The reflecting-barrier chain $S=\{1,2,3\}$, $P = \begin{bmatrix}0&1&0\\ 1/2&0&1/2\\ 0&1&0\end{bmatrix}$ is irreducible with a *unique* stationary distribution $\pi=(1/4,1/2,1/4)$, but has period 2 (see [[Period of States]]), so $P^{(n)}$ oscillates between two fixed matrices depending on the parity of $n$ and never converges. Starting from $p^{(0)}=(1,0,0)$, the distribution cycles $(1,0,0)\to(0,1,0)\to(1/2,0,1/2)\to(0,1,0)\to\cdots$ forever, so $\lim_n p^{(0)}P^n$ does not exist. A unique stationary distribution is therefore *not* sufficient for an equilibrium distribution to exist — aperiodicity is also required.

## See also
- [[Stationary Distribution]]
- [[Discrete-Time Markov Chain]]
- [[Transition Matrix]]
- [[Ergodic theorem]]
- [[Period of States]]
- [[Irreducible Class]]
- [[Mean Recurrence Time]]
