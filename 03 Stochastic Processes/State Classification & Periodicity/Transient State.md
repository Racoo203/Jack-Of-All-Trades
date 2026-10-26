---
title: Transient State
domain: Stochastic Processes
course: Stochastic Processes
unit: State Classification & Periodicity
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
State $i$ is **transient** if the probability of ever returning to it, starting from $i$, is strictly less than 1:
$$
f_i = \Pr(\text{ever return to } i \mid X_0=i) = \sum_{n=1}^\infty f_{ii}^{(n)} < 1,
$$
where $f_{ii}^{(n)}$ is the probability that the *first* return to $i$ occurs exactly at step $n$ (see [[Recurrent State]] for the general renewal identity relating $f_{ii}^{(n)}$ to the $n$-step transition probabilities). Equivalently, the chain leaves $i$ with positive probability $1 - f_i > 0$ of *never* coming back. Transience, like recurrence, is a class property: every state in a given [[Irreducible Class]] is transient, or none is — so on a finite state space, the transient states are exactly those lying in an open (non-closed) irreducible class.

## Properties
### Worked derivation via a geometric series
For $S=\{1,2,3,4\}$, $P=\begin{bmatrix}1/4&3/4&0&0\\1/3&0&2/3&0\\0&0&0&1\\0&0&1&0\end{bmatrix}$, consider state 2. Its first-return probabilities are $f_{22}^{(1)}=p_{22}=0$, and for $n\ge2$ the chain must first step to state 1 ($p_{21}=1/3$), self-loop at 1 for $n-2$ steps ($p_{11}=1/4$ each), then step back to 2 ($p_{12}=3/4$):
$$
f_{22}^{(n)} = p_{21}\cdot p_{11}^{n-2}\cdot p_{12} = \frac13\left(\frac14\right)^{n-2}\frac34, \qquad n \ge 2.
$$
Summing the geometric series (common ratio $1/4$):
$$
f_2 = \sum_{n=2}^\infty \frac13\left(\frac14\right)^{n-2}\frac34 = \frac13\cdot\frac34\cdot\frac{1}{1-1/4} = \frac13\cdot\frac34\cdot\frac43 = \frac13 < 1,
$$
so state 2 is transient. Since transience is a class property and $1 \leftrightarrow 2$ (they communicate), state 1 is transient too — a full first-principles verification for state 1 would need its own geometric-series computation analogous to state 2's, but the class-property shortcut makes this unnecessary in general.

### Finite escape: leaving a transient class for good
On a finite state space, a state $i$ is transient exactly when it lies in an irreducible class that is not closed, i.e. there is a route out of $i$'s class into some other class from which there is no way back. Once the chain leaves such a class it can revisit it only finitely many times in total (the number of returns to a transient state, started from that state, is a geometric random variable with success probability $1-f_i$, where "success" means the chain never returns again), so the chain eventually settles permanently inside a recurrent (closed) class. <!-- UNVERIFIED: the geometric-number-of-visits fact is standard (e.g. Privault, "Understanding Markov Chains", Ch. 6) but was not spelled out explicitly in the lecture slides read for this note -->

## Examples
For $P=\begin{bmatrix}0.25&0.25&0.5&0\\0&0&0&1\\0&1&0&0\\0&0&1&0\end{bmatrix}$, state 1 has $f_{11}^{(n)} = 0.25$ if $n=1$ and $0$ for $n>1$ (once left, state 1 is never accessible again), giving $f_1 = 0.25 < 1$: state 1 is transient — confirming, via the direct definition, the class-based conclusion of [[Irreducible Class]] that $\{1\}$ is an open (non-closed) singleton class.

## See also
- [[Recurrent State]]
- [[Irreducible Class]]
- [[Period of States]]
- [[Absorbing State]]
- [[Discrete-Time Markov Chain]]
