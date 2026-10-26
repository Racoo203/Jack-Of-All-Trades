---
title: "Ergodic Markov Chain"
domain: "Optimization & Control"
course: "Stochastic Optimization"
level: BSc
status: drafted
confidence: 0
tags: [markov-chains, stochastic-optimization]
---
## Definition
A [[Discrete-Time Markov Chain]] is **ergodic** if every state is [[Recurrent State|recurrent]] and the chain is **aperiodic** (no state has [[Period of States|period]] greater than 1). Equivalently (for a finite chain), ergodicity is [[Irreducible Class|irreducibility]] plus aperiodicity: every state communicates with every other state, and there is no fixed cycle length that visits must respect.

This is the condition under which a [[Transition Matrix]] $P$ has a *unique* limiting behavior — both a unique [[Stationary Distribution]] $\pi$ solving $\pi = \pi P$, and a unique [[Equilibrium Distribution]] $\lim_{n\to\infty}P^n$, and the two coincide:
$$
\lim_{n\to\infty} P^n = \mathbf{1}\pi^\top, \qquad \text{i.e. every row of } P^n \text{ converges to } \pi.
$$

## Properties
### Independence of the initial distribution
Because every row of $\lim_{n\to\infty}P^n$ is the same vector $\pi$, the limiting distribution of $X_n$ does not depend on the initial state (or initial distribution) $X_0$: for any starting distribution $p^{(0)}$,
$$
\lim_{n\to\infty} p^{(n)} = \lim_{n\to\infty} p^{(0)}P^n = p^{(0)}\mathbf{1}\pi^\top = \pi,
$$
since $p^{(0)}\mathbf{1} = 1$ (the entries of any probability vector sum to 1).

### Worked classification example (weather chain)
Let a day be Soleado ($S$) or Nublado ($N$) with transition matrix
$$
P = \begin{bmatrix} 2/3 & 1/3 \\ 1/2 & 1/2 \end{bmatrix}, \quad \text{rows/columns ordered } (S, N).
$$
Both states communicate ($p_{SN}, p_{NS} > 0$), so the chain is irreducible; since $p_{SS} > 0$ there is a self-loop, which forces the period to be 1 (aperiodic). Hence the chain is ergodic, and $\lim_{n\to\infty}P^n$ has identical rows. Diagonalizing $P$ (see [[Spectral Decomposition of a Transition Matrix]]) gives eigenvalues $\lambda_1 = 1, \lambda_2 = 1/6$, and
$$
\lim_{n\to\infty} P^n = \begin{bmatrix} 3/5 & 2/5 \\ 3/5 & 2/5 \end{bmatrix},
$$
i.e. $\pi = (3/5, 2/5)$ regardless of whether the chain started on a sunny or cloudy day.

### Non-example: reducible chain
The 7-state chain used in the course to illustrate classification (states $a$–$g$) has a state $g$ with $p_{gg} = 1$ and no transitions in or out of it from/to any other state; $g$ is an isolated absorbing state, so the chain is **not irreducible** and therefore not ergodic. Restricted to the remaining communicating states $\{a,\dots,f\}$, state $c$ was found to have period 2 (periodic), so that sub-chain is not ergodic either — only a chain with no such absorbing or periodic states qualifies.

## Examples
The classic 3-state elevator chain (Bajo / Piso 1 / Piso 2, see [[Spectral Decomposition of a Transition Matrix]]) is ergodic: it is irreducible (every floor reachable from every other) and aperiodic (return times to any state are not all multiples of a common integer $> 1$), giving the unique stationary distribution $\pi = (8/17, 4/17, 5/17)$.

## See also
[[Discrete-Time Markov Chain]], [[Transition Matrix]], [[Irreducible Class]], [[Recurrent State]], [[Period of States]], [[Stationary Distribution]], [[Equilibrium Distribution]], [[Mean Recurrence Time]], [[Spectral Decomposition of a Transition Matrix]]
