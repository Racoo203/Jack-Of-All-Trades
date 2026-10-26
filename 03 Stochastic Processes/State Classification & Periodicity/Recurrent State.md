---
title: Recurrent State
domain: Stochastic Processes
course: Stochastic Processes
unit: State Classification & Periodicity
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
Let $T_{ii} = \min\{n \ge 1 : X_n = i \mid X_0 = i\}$ be the **first return time** to state $i$ (a special case of the [[Discrete-Time Markov Chain|first passage time]] $T_{ij}$ with $j=i$), and let $f_{ii}^{(n)} = \Pr(T_{ii} = n \mid X_0=i)$ be the probability that the chain's *first* return to $i$ occurs at step $n$. The probability of *ever* returning to $i$ is
$$
f_i = \Pr(\text{ever return to } i \mid X_0 = i) = \sum_{n=1}^{\infty} f_{ii}^{(n)}.
$$
State $i$ is **recurrent** (also called *persistent*) if $f_i = 1$ — a return to $i$ is certain. (If $f_i < 1$, the state is [[Transient State|transient]] instead.)

A recurrent state $i$ is further classified using its [[Mean Recurrence Time]] $\mu_i = E(T_{ii}) = \sum_{n=1}^\infty n\, f_{ii}^{(n)}$:
- **positive recurrent** if $\mu_i < \infty$;
- **null recurrent** if $\mu_i = \infty$ (only possible on an infinite state space).

Recurrence is a class property: all states in the same [[Irreducible Class]] are recurrent, or none are.

## Properties
### Direct verification via the renewal identity
**Renewal-type theorem.** For a discrete-time homogeneous Markov chain,
$$
p_{ij}^{(n)} = \sum_{m=1}^n f_{ij}^{(m)}\, p_{jj}^{(n-m)} \qquad \text{for all } n \in \mathbb{N},
$$
where $f_{ij}^{(m)} = \Pr(T_{ij}=m \mid X_0=i)$. (Proof: condition on the first passage time $T_{ij}=m$ and use the Markov property, exactly as for the [[Chapman-Kolmogorov Equation]].) This lets $f_{ij}^{(n)}$ be recovered from the (usually easier to compute) $n$-step probabilities $p_{ij}^{(n)}$: e.g. for $j=i$, $n=2$, since $f_{ii}^{(1)}=p_{ii}$ and $p_{ii}^{(0)}=1$,
$$
p_{ii}^{(2)} = f_{ii}^{(1)} p_{ii}^{(1)} + f_{ii}^{(2)} p_{ii}^{(0)} = p_{ii}^2 + f_{ii}^{(2)} \implies f_{ii}^{(2)} = p_{ii}^{(2)} - p_{ii}^2.
$$

### Worked recurrence proof and mean recurrence time
For $S=\{1,2,3\}$, $P = \begin{bmatrix}0.4&0.6&0\\0&0&1\\0.7&0&0.3\end{bmatrix}$, state 1's first-return probabilities are $f_{11}^{(1)}=0.4$, $f_{11}^{(2)}=p_{12}p_{21}+p_{13}p_{31}=0$, and for $n\ge3$, $f_{11}^{(n)} = p_{12}\,p_{23}\,p_{33}^{n-3}\,p_{31} = 0.6\cdot 1\cdot(0.3)^{n-3}\cdot 0.7 = 0.42\,(0.3)^{n-3}$ (the chain must leave via state 2, cycle in state 3 for a while, then return via $3\to1$). Summing the geometric series,
$$
f_1 = 0.4 + \sum_{n=3}^\infty 0.42\,(0.3)^{n-3} = 0.4 + 0.42\cdot\frac{1}{1-0.3} = 0.4 + 0.6 = 1,
$$
so state 1 is recurrent. Its mean recurrence time follows from $\mu_1 = \sum_n n f_{11}^{(n)} = 1(0.4) + \sum_{n\ge3} n \cdot 0.42(0.3)^{n-3}$; substituting $m=n-2$ and using $E[\mathrm{Geom}(p)] = 1/p$ for the geometric-distribution sum gives $\mu_1 = 0.4 + 1.2 + 6/7 = 86/35 \approx 2.46$ — see [[Mean Recurrence Time]] for the general theory (including the shortcut $\mu_i = 1/\pi_i$ once the chain is known to be ergodic).

## Examples
A single-state closed class is automatically recurrent: see [[Absorbing State]] (return probability 1, trivially, in one step). Conversely, a finite chain's transient states are exactly those outside every closed communicating class — see [[Transient State]] and [[Irreducible Class]] for the companion derivation on the same running example.

## See also
- [[Transient State]]
- [[Irreducible Class]]
- [[Period of States]]
- [[Mean Recurrence Time]]
- [[Absorbing State]]
- [[Discrete-Time Markov Chain]]
