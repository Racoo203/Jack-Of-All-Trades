---
title: Kolmogorov Forward Equations
domain: Stochastic Processes
course: Stochastic Processes
unit: Continuous-Time & Jump Processes
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
For a time-homogeneous [[Markov Jump Process|continuous-time Markov chain]] $\{X(t)\}$ with transition probabilities $p_{ij}(t)$ and generator matrix $Q=(q_{ij})$, the **Kolmogorov forward equations** state that
$$
p_{ij}'(t) = \sum_{k\in S} p_{ik}(t)\, q_{kj} \qquad \text{for all } i,j\in S,
$$
or in matrix form,
$$
P'(t) = P(t)\,Q.
$$
The left-hand side of the scalar equation is the $(i,j)$ entry of $P'(t)$; the right-hand side is the $(i,j)$ entry of $P(t)Q$. The equations describe how the transition probabilities evolve "forward" in the *destination* time argument.

## Properties
### Derivation from the Chapman-Kolmogorov Equations
Starting from the [[Chapman-Kolmogorov Equation|Chapman-Kolmogorov equations]] and splitting off the $k=j$ term,
$$
p_{ij}(t+h) = \sum_{k\in S} p_{ik}(t)p_{kj}(h) = p_{ij}(t)p_{jj}(h) + \sum_{k\neq j} p_{ik}(t)p_{kj}(h).
$$
Using the local expansions $p_{jj}(h) = 1+q_{jj}h+o(h)$ and $p_{kj}(h) = q_{kj}h+o(h)$ for $k\neq j$ (from the definition of the [[Markov Jump Process|generator matrix]]),
$$
p_{ij}(t+h) = p_{ij}(t)\big(1+q_{jj}h+o(h)\big) + \sum_{k\neq j} p_{ik}(t)\big(q_{kj}h+o(h)\big) = p_{ij}(t) + \left(\sum_{k\in S} p_{ik}(t)q_{kj}\right)h + o(h).
$$
Subtracting $p_{ij}(t)$, dividing by $h$, and letting $h\to 0$ gives
$$
p_{ij}'(t) = \sum_{k\in S} p_{ik}(t)\,q_{kj}. \qquad\blacksquare
$$

### Kolmogorov Backward Equations (related result)
An analogous argument, splitting the Chapman-Kolmogorov equations near $t=0$ instead of near $t+h$ (i.e. writing $p_{ik}(h)$ in terms of $q_{ik}$ rather than $p_{kj}(h)$ in terms of $q_{kj}$), gives the **backward** equations
$$
p_{ij}'(t) = \sum_{k\in S} q_{ik}\, p_{kj}(t), \qquad P'(t) = Q\,P(t).
$$
*Sketch.* $p_{ij}(t+h) = \sum_k p_{ik}(h)p_{kj}(t) = p_{ij}(h)p_{jj}(t) \cdot [\text{split off } k=i] = p_{ii}(h)p_{ij}(t) + \sum_{k\neq i}p_{ik}(h)p_{kj}(t) = p_{ij}(t) + \left(\sum_k q_{ik}p_{kj}(t)\right)h + o(h)$; subtracting $p_{ij}(t)$, dividing by $h$ and letting $h\to 0$ gives the result. Note the asymmetry with the forward case: $P'(t)=P(t)Q$ (forward) vs. $P'(t)=QP(t)$ (backward) — $Q$ is multiplied on the right vs. the left.

<!-- UNVERIFIED: "Kolmogorov Backward Equations" has no dedicated vault note yet; flagged for the MOC as a candidate note since it is used repeatedly alongside the forward equations. -->

### Worked example: the HSD model
For the Healthy-Sick-Dead chain (states ordered $H,S,D$) with generator matrix
$$
Q = \begin{pmatrix} -\rho-\mu & \rho & \mu \\ \sigma & -\sigma-\nu & \nu \\ 0 & 0 & 0 \end{pmatrix},
$$
the forward equations for specific entries follow immediately by picking out the relevant column of $Q$:
$$
p_{HS}'(t) = \sum_{k} p_{Hk}(t)q_{kS} = p_{HH}(t)\cdot\rho + p_{HS}(t)\cdot(-\sigma-\nu) + p_{HD}(t)\cdot 0,
$$
$$
p_{SD}'(t) = \sum_{k} p_{Sk}(t)q_{kD} = p_{SH}(t)\cdot\mu + p_{SS}(t)\cdot\nu + p_{SD}(t)\cdot 0.
$$
As a sanity check, $p_{DH}'(t) = p_{DH}(t)(-\rho-\mu) + p_{DS}(t)\cdot\sigma + p_{DD}(t)\cdot 0$; since $D$ is absorbing, $p_{DH}(t)=p_{DS}(t)=0$ for all $t$, so this correctly evaluates to $0$ (a transition out of the absorbing state is impossible).

### Application: the Poisson process
Specializing to the generator matrix of the [[Poisson Process|Poisson process]] ($q_{ii}=-\lambda$, $q_{i,i+1}=\lambda$, else $0$) gives the pair of forward equations
$$
p_{i0}'(t) = -\lambda\, p_{i0}(t), \qquad p_{ij}'(t) = \lambda\, p_{i(j-1)}(t) - \lambda\, p_{ij}(t)\ (j\geq 1),
$$
whose solution (by induction, worked out fully in [[Poisson Process]]) recovers $p_{ij}(t) = \dfrac{e^{-\lambda t}(\lambda t)^{j-i}}{(j-i)!}$, confirming $N(t)-N(0) \sim \text{Pois}(\lambda t)$.

## See also
- [[Markov Jump Process]]
- [[Poisson Process]]
- [[Chapman-Kolmogorov Equation]]
- [[Transition Matrix]]
- [[Discrete-Time Markov Chain]]
