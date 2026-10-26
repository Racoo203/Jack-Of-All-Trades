---
title: "Betti Numbers"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Homology"
level: BSc
status: drafted
confidence: 0
tags: [tda, homology]
---
## Definition
Let $K$ be a [[Simplicial Complex]]. The **$n$-th Betti number** of $K$ is the dimension of the $n$-th [[Homology Group]] as a $\mathbb Z_2$-vector space:
$$
\beta_n(K) = \dim H_n(K) = \dim\ker\partial_n - \dim\operatorname{Im}\partial_{n+1}.
$$

## Properties
### Computing via the rank-nullity theorem
Since $\partial_n$ is a linear map with matrix representation (see [[Boundary Operator]]), $\dim\operatorname{Im}\partial_n$ equals the rank of that matrix, and rank-nullity gives $\dim\ker\partial_n = \dim\mathcal C_n(K) - \operatorname{rank}(\partial_n)$. So computing $\beta_n$ reduces to Gauss-Jordan elimination (over $\mathbb Z_2$) on the boundary-operator matrices.

**Worked example.** For $K=\{a,b,c,ab,bc,ca\}$ (triangle outline): $\dim\mathcal C_0=3$, and $\partial_0$ is the zero map (rank $0$), so $\dim\ker\partial_0=3$. The matrix of $\partial_1$ (see [[Boundary Operator]]) has rank $2$ over $\mathbb Z_2$, so $\dim\ker\partial_1 = 3-2=1$ and $\dim\operatorname{Im}\partial_1=2$. There are no $2$-simplices, so $\operatorname{Im}\partial_2=\{0\}$. Hence
$$
\beta_0(K) = \dim\ker\partial_0 - \dim\operatorname{Im}\partial_1 = 3-2=1, \qquad
\beta_1(K) = \dim\ker\partial_1 - \dim\operatorname{Im}\partial_2 = 1-0=1.
$$
(This matches the circle: one connected component, one loop.)

### Interpretation of $\beta_n$
- $\beta_0$: number of connected components (see [[Connectedness]]).
- $\beta_1$: number of independent $1$-dimensional holes ("tunnels").
- $\beta_2$: number of $2$-dimensional voids ("cavities").
- In general, $\beta_n$ counts independent $n$-dimensional holes. $\beta_1$ is also connected to the presence of periodicity in the underlying topological space (relevant to time-series applications via [[Takens' Embedding Theorem]]).

Together, $(\beta_0,\beta_1,\beta_2,\dots)$ and the [[Triangulation and Euler Characteristic|Euler characteristic]] are the two standard combinatorial invariants used to recognize a triangulated space; unlike $\chi$, the individual Betti numbers give dimension-by-dimension information rather than a single alternating sum.

## Examples
For the tetrahedron-boundary triangulation of $S^2$ (see [[Triangulation and Euler Characteristic]]): $\beta_0=1$ (connected), $\beta_1=0$ (no independent loops — every loop bounds a disk on the sphere), $\beta_2=1$ (one enclosed void). Consistent with $\chi = \beta_0-\beta_1+\beta_2 = 1-0+1=2$.

## See also
[[Homology Group]], [[Boundary Operator]], [[Triangulation and Euler Characteristic]], [[Connectedness]]
