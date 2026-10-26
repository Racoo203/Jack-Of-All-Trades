---
title: "Vietoris-Rips Complex"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Topological Data Analysis"
level: BSc
status: drafted
confidence: 0
tags: [tda]
---
## Definition
Let $(P,d)$ be a finite [[Metric Space]] and $r>0$. The **Vietoris-Rips complex** (or **Rips complex**) $VR_r(P)$ is the abstract [[Simplicial Complex]] where a simplex $\sigma \in VR_r(P)$ is included iff
$$
d(p,q) \le 2r \qquad \text{for every pair of vertices } p,q \in \sigma.
$$

## Properties
### Determined entirely by its $1$-skeleton
Unlike the general [[Nerve Complex]] construction, $VR_r(P)$ is completely determined by its $0$-skeleton (the vertex set) and $1$-skeleton (which pairs are within $2r$ of each other): a higher-dimensional simplex is added automatically whenever *all* of its vertex pairs already satisfy the distance condition ("complete the clique"). This is a key practical advantage over the [[Čech Complex]], since only pairwise distances need to be checked.

### Agreement with the Čech complex
If, for every $r>0$ and every $p,q\in M$ with $d(p,q)\le 2r$, the balls $B_r(p)$ and $B_r(q)$ are guaranteed to intersect (a condition satisfied by Euclidean space), then the $1$-skeletons of the Čech and Vietoris-Rips complexes at that radius coincide. However, their higher-dimensional simplices can differ, since Vietoris-Rips only checks pairwise conditions while Čech checks genuine multi-way ball intersections.

### Combinatorial cost
For $n$ points in $\mathbb R^d$, the Rips complex can have $O(n^d)$ $d$-simplices, so in practice the complexes used in TDA pipelines are usually truncated at a fixed maximum dimension.

## Examples
For $X=\{a,b,c,d\}=\{(0,0),(1,0),(0,1),(1,1)\}\subset\mathbb R^2$ with $r=1$ (so the pairwise-distance threshold is $2r=2$): all pairs except the two "diagonal" pairs ($a$–$d$ at distance $\sqrt2 \approx 1.41 < 2$, so actually all six pairs qualify since $\sqrt2 < 2$) satisfy $d(p,q)\le2$, giving the full $3$-simplex $VR_1(X) = \{a,b,c,d,ab,ac,ad,bc,bd,cd,abc,abd,acd,bcd\}$. At smaller radii ($r=0.1,\,r=0.5$) the resulting complexes on this point set coincide with the corresponding [[Čech Complex]] complexes, since the four points are arranged so that ball intersections and pairwise-distance conditions agree at those scales.

## See also
[[Nerve Complex]], [[Čech Complex]], [[Alpha Complex]], [[Metric Space]]
