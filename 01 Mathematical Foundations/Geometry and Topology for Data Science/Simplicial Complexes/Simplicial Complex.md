---
title: "Simplicial Complex"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Simplicial Complexes"
level: BSc
status: drafted
confidence: 0
tags: [tda, simplicial-complexes]
---
## Definition
A **(geometric) simplicial complex** $K$, also called a **triangulation**, is a finite (countable, enumerable) collection of [[Simplex|simplices]] such that:

1. $K$ contains every face of each simplex in $K$.
2. For any two simplices $\sigma,\tau\in K$, $\sigma\cap\tau$ is either empty or a common face of both.

The **dimension** of $K$ is the maximal dimension among its simplices.

Equivalently, an **abstract simplicial complex** is a collection $K$ of non-empty subsets of a vertex set $V$ such that every subset of a set in $K$ is also in $K$ (downward closure). The geometric realization of an abstract simplicial complex is a geometric simplicial complex, and the course treats the two notions as interchangeable.

For $k\ge0$, the **$k$-skeleton** $K^k$ is the subcomplex formed by all simplices of dimension at most $k$ — the central object used to define [[Chain Group|chains]].

## Properties
### Neighborhoods inside a complex
Given a simplex $\sigma \in K$, the **star** of $\sigma$ is $St(\sigma) = \{\omega \in K : \sigma \subset \omega\}$ (every simplex having $\sigma$ as a face). The star is generally not itself a simplicial complex, since it need not contain all faces of its elements. The **closed star** $\overline{St}(\sigma)$ is the smallest simplicial complex inside $K$ containing $St(\sigma)$ — it adds back every missing face. The **link** $Lk(\sigma) = \{\omega \in St(\sigma) : \sigma \cap \omega = \emptyset\}$ consists of the simplices in the star that are disjoint from $\sigma$ itself. Intuitively, the star of a vertex is like an open neighborhood of it, and the link is like the boundary of that neighborhood, so the closed star is the union of the (open) star and the link. See [[Star and Link of a Simplex]] for worked examples.

### Topology of a simplicial complex
The topology of a single simplex is the subspace topology inherited from the [[Metric Topology]] on $\mathbb R^n$; the topology of a simplicial complex is again the subspace topology on the union of its simplices.

## Examples
$K=\{a,b,c,ab,bc,ca\}$ (three vertices and their connecting edges, with no filled triangle) is a $1$-dimensional simplicial complex whose geometric realization is a circle (a triangle outline).

## See also
[[Simplex]], [[Star and Link of a Simplex]], [[Triangulation and Euler Characteristic]], [[Chain Group]]
