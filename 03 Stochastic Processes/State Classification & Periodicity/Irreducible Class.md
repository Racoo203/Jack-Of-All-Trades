---
title: Irreducible Class
domain: Stochastic Processes
course: Stochastic Processes
unit: State Classification & Periodicity
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
State $j$ is **accessible** from state $i$ (written $i \to j$) if $p_{ij}^{(n)} > 0$ for some $n \ge 0$ — starting from $i$, the chain hits $j$ eventually with positive probability (see [[Transition Graph]] for the graphical reading: a directed path from $i$ to $j$). Two states **communicate**, written $i \leftrightarrow j$, if $i \to j$ *and* $j \to i$.

Communication is an equivalence relation on $S$:
- **Reflexivity:** $i \leftrightarrow i$ for every state (take $n=0$, since $p_{ii}^{(0)}=1>0$).
- **Symmetry:** $i \leftrightarrow j \implies j \leftrightarrow i$ (immediate from the definition).
- **Transitivity:** $i \leftrightarrow j$ and $j \leftrightarrow k$ $\implies$ $i \leftrightarrow k$ (concatenate the positive-probability paths $i\to j\to k$ and $k\to j\to i$).

Because it is an equivalence relation, communication partitions $S$ into disjoint **irreducible classes** (equivalence classes of mutually communicating states). An irreducible class $C$ is **closed** if the chain can never leave it once it enters, i.e. $p_{ij}=0$ for every $i \in C$, $j \notin C$; otherwise $C$ is **open** (non-closed).

A Markov chain itself is called **irreducible** if there is only one irreducible class, i.e. every pair of states communicates. A chain is **regular** if some power $P^{(n)}$ has every entry strictly positive; regularity implies irreducibility, but not conversely — irreducible chains can fail to be regular if they are periodic (see [[Period of States]]).

## Properties
### Recurrence, transience and periodicity are class properties
If $i \leftrightarrow j$, then $i$ and $j$ are either both [[Recurrent State|recurrent]] or both [[Transient State|transient]], and they have the same [[Period of States|period]]. So it suffices to check these properties once per irreducible class, not once per state. <!-- UNVERIFIED: proof not given in the slides read for this note; standard reference is Corollary 6.6 in Privault, "Understanding Markov Chains" -->

A finite closed irreducible class is always recurrent (every state in it is visited infinitely often), while an open irreducible class on a finite state space is always transient (the chain eventually leaves it for good and cannot return). A single-state closed class is exactly an [[Absorbing State]].

### Worked classification examples
For $S=\{1,2,3,4\}$, $P = \begin{bmatrix}1/4 & 3/4 & 0 & 0\\ 1/3 & 0 & 2/3 & 0\\ 0&0&0&1\\0&0&1&0\end{bmatrix}$: state 2 is accessible from state 1 ($p_{12}=3/4>0$), and $1\leftrightarrow 2$, giving $C_1=\{1,2\}$; state 1 is *not* accessible from state 3 ($p_{31}^{(n)}=0$ for all $n$), and $3\leftrightarrow 4$ gives $C_2=\{3,4\}$. $C_2$ is closed (the chain never leaves $\{3,4\}$ once there); $C_1$ is not closed (it can escape to $C_2$ via $p_{23}=2/3$). Hence states 1, 2 are transient and states 3, 4 are recurrent.

For $S=\{1,2,3,4\}$, $P=\begin{bmatrix}0.25&0.25&0.5&0\\0&0&0&1\\0&1&0&0\\0&0&1&0\end{bmatrix}$: state 1 cannot be returned to once left, so $C_1=\{1\}$ is its own (open, transient) class, while the cycle $2\to4\to3\to2$ shows $2,3,4$ all communicate, giving a closed recurrent class $C_2=\{2,3,4\}$ — so this chain is *not* irreducible (two classes).

By contrast, for $S=\{1,2,3,4\}$, $P=\begin{bmatrix}0&0&0&1\\0&0&0&1\\1/2&1/2&0&0\\0&0&1&0\end{bmatrix}$: chaining $1\to4\to3\to1$ and $4\leftrightarrow3\leftrightarrow2$ shows $1\leftrightarrow4\leftrightarrow3\leftrightarrow2$, so all four states communicate — this chain *is* irreducible (a single class $C=S$).

## Examples
The Ehrenfest urn model ($m$ balls moved one at a time between two urns) has transition graph a simple path $0\leftrightarrow1\leftrightarrow\cdots\leftrightarrow m$: it is irreducible (every state reachable from every other, since $p_{i,i-1}, p_{i,i+1}>0$ throughout) but **not regular**, because parity constraints ($p_{ii}^{(n)}=0$ for odd $n$; $p_{i,i+1}^{(n)}=0$ for even $n$) prevent any power $P^{(n)}$ from having every entry positive.

## See also
- [[Transition Graph]]
- [[Absorbing State]]
- [[Recurrent State]]
- [[Transient State]]
- [[Period of States]]
- [[Discrete-Time Markov Chain]]
