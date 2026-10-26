---
title: Period of States
domain: Stochastic Processes
course: Stochastic Processes
unit: State Classification & Periodicity
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
The **period** of state $i$, denoted $d_i$, is the greatest common divisor of the set of return times with positive probability:
$$
d_i = \gcd\{ n \ge 1 : p_{ii}^{(n)} > 0 \}.
$$
If $d_i = 1$, state $i$ is **aperiodic**. If $p_{ii}^{(n)} = 0$ for *every* $n \ge 1$ (the state can never be revisited), then by convention $i$ is also said to be aperiodic. Periodicity is a class property: all states in the same [[Irreducible Class|irreducible class]] share the same period.

## Properties
### Worked derivations of the period
For $P = \begin{bmatrix}1/4 & 3/4 & 0 & 0\\ 1/3 & 0 & 2/3 & 0\\ 0&0&0&1\\0&0&1&0\end{bmatrix}$ (see [[Irreducible Class]]): $p_{11}^{(1)}=1/4>0$ gives $d_1=1$; $p_{22}^{(2)}, p_{22}^{(3)}>0$ gives $d_2=1$ (both 2 and 3 lie in the return-time set, and $\gcd(2,3)=1$). States 3 and 4 form a closed class where the only possible transition pattern is $3\to4\to3\to4\to\cdots$, so a return to 3 is possible only in an even number of steps, giving $d_3=d_4=2$.

For $P=\begin{bmatrix}0.25&0.25&0.5&0\\0&0&0&1\\0&1&0&0\\0&0&1&0\end{bmatrix}$: it can be shown that $p_{22}^{(n)} = 1$ if $n=3$ and $0$ otherwise, so $d_2 = \gcd\{3\} = 3$; by the class property, $d_3=d_4=3$ too (state 1 is a singleton class with $p_{11}^{(1)}=0.25>0$, so $d_1=1$).

For $P=\begin{bmatrix}0&0.5&0&0.5\\0&0&1&0\\1&0&0&0\\0&0&1&0\end{bmatrix}$: the cycle structure forces $p_{11}^{(n)}>0$ only when $n=3k$ for integer $k\ge1$ (e.g. via $1\to2\to3\to1$ or $1\to4\to3\to1$, both length-3 routes), so $d_1 = \gcd\{3,6,9,\dots\}=3$, and by the class property all four states have period 3.

### Aperiodicity from a self-loop
If $p_{ii}>0$ for some state $i$ (a self-loop on the transition graph), then $1 \in \{n : p_{ii}^{(n)}>0\}$, forcing $d_i = \gcd(1, \dots) = 1$: any chain with a self-loop is automatically aperiodic on that state's class. This is the quickest way to rule out periodicity in practice.

### Periodic but irreducible: the Ehrenfest model
The Ehrenfest urn model (state = number of balls in urn 1, out of $m$) moves $\pm1$ each step, so $p_{ii}^{(n)}=0$ whenever $n$ is odd (parity is preserved only over an even number of moves), and $p_{ii}^{(n)}>0$ for even $n$ (e.g. move a ball out and the same one back). Hence $d_i = 2$ for every state: the chain is irreducible (see [[Irreducible Class]]) but has period 2, so it is not regular and, by [[Equilibrium Distribution]], has no equilibrium distribution even though it has a unique stationary distribution.

## See also
- [[Irreducible Class]]
- [[Recurrent State]]
- [[Equilibrium Distribution]]
- [[Transition Graph]]
- [[Ergodic theorem]]
