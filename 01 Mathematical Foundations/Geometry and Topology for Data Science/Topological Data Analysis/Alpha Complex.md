---
title: "Alpha Complex"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Topological Data Analysis"
level: BSc
status: drafted
confidence: 0
tags: [tda]
---
## Definition
Let $P$ be a finite point set and $\alpha \ge 0$. For $p\in P$, let $B_\alpha(p)$ be the closed ball of radius $\alpha$ centered at $p$, and define the restricted (Voronoi-clipped) region
$$
D_p^\alpha = \{x \in B_\alpha(p) : d(x,p) \le d(x,q)\ \forall q \in P\},
$$
i.e. the part of $B_\alpha(p)$ closer to $p$ than to any other point of $P$. The **$\alpha$-complex** $\mathrm{Del}_\alpha(P)$ is the [[Nerve Complex|nerve]] of the collection of closed sets $\{D_p^\alpha\}_{p\in P}$.

## Properties
### A cheaper subcomplex of Vietoris-Rips
$\mathrm{Del}_\alpha(P)$ is always a subcomplex of the [[Vietoris-Rips Complex]] at a comparable scale, since restricting each ball to its Voronoi cell before intersecting can only produce fewer non-empty intersections. This makes the Alpha complex substantially cheaper to store and compute for large point clouds, while still forming a [[Persistent Set|persistent]] filtration in $\alpha$ suitable for computing persistent homology.

### Relation to the Delaunay triangulation
The notation $\mathrm{Del}_\alpha$ reflects that, as $\alpha \to \infty$, the Alpha complex converges to the (full) **Delaunay triangulation** of $P$ — the Voronoi-dual triangulation — since every $D_p^\infty$ region is exactly the (unrestricted) Voronoi cell of $p$.

## Examples
For four points arranged as corners of a unit square, the Alpha complex at small $\alpha$ starts as isolated vertices, gains edges once $\alpha$ is large enough for adjacent Voronoi-clipped balls to touch, and eventually (at large $\alpha$) recovers the same triangulated square that the Delaunay triangulation of those four points would give — typically using *fewer* simplices at intermediate scales than the corresponding [[Čech Complex]] or [[Vietoris-Rips Complex]] would.

## See also
[[Nerve Complex]], [[Vietoris-Rips Complex]], [[Čech Complex]], [[Persistent Set]]
