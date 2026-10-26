---
title: "Triangulation and Euler Characteristic"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Simplicial Complexes"
level: BSc
status: drafted
confidence: 0
tags: [tda, simplicial-complexes]
---
## Definition
A **triangulation** of a topological space $X$ is a [[Simplicial Complex]] $K$ whose geometric realization is [[Homeomorphism|homeomorphic]] to $X$. A triangulation is **non-singular** if all of its simplices are non-degenerate (no edge with a repeated vertex, no triangle with fewer than three distinct vertices, etc.); otherwise it is **singular** — see [[Singular Homology]].

The **Euler characteristic** of a simplicial complex $K$ of dimension $2$ or less (as computed in this course) is
$$
\chi(K) = \sum_{i} (-1)^i \, \#K^i,
$$
where $\#K^i$ is the number of $i$-simplices of $K$. More generally the sum runs over all dimensions present in $K$.

## Properties
### $\chi$ is a topological invariant
$\chi(K)$ does not depend on which triangulation of $X$ is chosen — any two triangulations of homeomorphic spaces yield the same Euler characteristic. This makes $\chi$, together with the [[Betti Numbers]], one of the two standard combinatorial invariants used to recognize a space from a triangulation.

### Worked computations
**Circle.** $K=\{a,b,c,ab,bc,ca\}$ has $3$ vertices and $3$ edges: $\chi(K) = 3-3=0$, matching $\chi(S^1)=0$.

**Sphere.** $K=\{a,b,c,d,ab,ad,ac,bc,bd,cd,abc,acd,abd,bcd\}$ (the boundary of a tetrahedron) has $4$ vertices, $6$ edges, $4$ triangles: $\chi(K)=4-6+4=2$, matching $\chi(S^2)=2$.

**Singular triangulation of a cylinder.** $K_1=\{a,b,c,ab,ba,bc,cb,bb,ca,ac,abc,bbc\}$ contains a degenerate edge ($bb$) and a degenerate triangle, but still validly triangulates a cylinder, with $\chi(K_1)=0$ — illustrating that singular (degenerate) triangulations can be far more economical than non-singular ones while still computing the correct invariant. See [[Singular Homology]].

## Examples
A `SimplicialComplex` object (from the Python `simplicial` package) exposes an `.eulerCharacteristic()` method: after adding vertices and edges with `addSimplex`, calling it directly reproduces the by-hand count above.

## See also
[[Simplicial Complex]], [[Betti Numbers]], [[Singular Homology]]
