---
title: "Čech Complex"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Topological Data Analysis"
level: BSc
status: drafted
confidence: 0
tags: [tda]
---
## Definition
Let $(M,d)$ be a metric space and $P\subset M$ a finite subset. Given $r>0$, the **Čech complex** $\check C_r(P)$ is the [[Nerve Complex|nerve]] of the cover $\{B_r(p)\}_{p\in P}$ by open balls of radius $r$ centered at the points of $P$ (see [[Balls and Spheres]]).

## Properties
### Homotopy equivalence in Euclidean space
If $M=\mathbb R^n$ with the Euclidean metric, every ball is convex, hence contractible, and so is every intersection of balls. By the [[Nerve Complex|Nerve Theorem]], $\check C_r(P)$ is homotopy equivalent to the union of balls $\bigcup_{p\in P} B_r(p)$ for every $r$.

### The Čech complex generates a filtration
Since $\check C_r(P)$ depends on the parameter $r$, varying $r$ produces a nested filtration $\check C_{r_1}(P) \subseteq \check C_{r_2}(P) \subseteq \cdots$ for $r_1 \le r_2 \le \cdots$ — the **Čech filtration**, a [[Persistent Set]] of simplicial complexes whose persistent homology is a central object of TDA.

## Examples
Let $X=\{a,b,c,d\}=\{(0,0),(1,0),(0,1),(1,1)\}\subset\mathbb R^2$.

- At $r=0.5$: the balls do not overlap, so $\check C_{0.5}(X) = \{a,b,c,d\}$ — $4$ isolated vertices.
- At $r=1$: adjacent (unit-distance) balls now overlap and one triple intersection appears, giving $\check C_1(X) = \{a,b,c,d,ab,bc,bd,cd,abc\}$ — $4$ edges and $1$ filled triangle.
- At $r=2$: all balls mutually overlap, giving the full $3$-simplex $\check C_2(X) = \{a,b,c,d,ab,ac,ad,bc,bd,cd,abc,abd,acd,bcd\}$.

These three snapshots read, respectively, as $4$ disconnected components, a connected space with one $1$-dimensional hole, and a connected space with no holes — a filtration approximating the underlying square (topologically a disk) with increasing fidelity as $r$ grows.

## See also
[[Nerve Complex]], [[Vietoris-Rips Complex]], [[Alpha Complex]], [[Balls and Spheres]], [[Persistent Set]]
