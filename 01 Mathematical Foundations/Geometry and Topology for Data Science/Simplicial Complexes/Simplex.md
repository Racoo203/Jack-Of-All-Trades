---
title: "Simplex"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Simplicial Complexes"
level: BSc
status: drafted
confidence: 0
tags: [tda, simplicial-complexes]
---
## Definition
An **$n$-simplex** in $\mathbb R^{n+1}$ is
$$
K^n := \left\{ (x_1,\dots,x_{n+1}) \in \mathbb R^{n+1} : \sum_{j=1}^{n+1} x_j = 1,\ x_j \ge 0 \right\}.
$$
Equivalently (and more commonly in the literature), an $n$-simplex is the convex hull of $n+1$ [[Geometrically Independent vs Linearly Independent Vectors|geometrically independent]] points in $\mathbb R^m$ (often taken to be the standard basis vectors of $\mathbb R^{n+1}$). Simplices are always connected, [[Compactness|compact]] subspaces of the ambient space.

Writing a simplex as $\sigma=(v_0,v_1,\dots,v_k)$ (a $k$-simplex), the **$(k-i)$-face** of $\sigma$ is the convex hull of any $i+1$ of its vertices. The $0$-faces are the **vertices**, the $1$-faces the **edges**. A $k$-simplex has $\binom{k+1}{i+1}$ faces of dimension $k-i$.

## Properties
### Low-dimensional pictures
- A $0$-simplex is a single point.
- A $1$-simplex is a line segment joining two points.
- A $2$-simplex is a filled triangle.
- A $3$-simplex is a filled tetrahedron.

Each $n$-simplex contains, as boundary faces, simplices of every lower dimension: e.g. a $2$-simplex has three $1$-simplices (edges) and three $0$-simplices (vertices) on its boundary. This nesting of faces is exactly what the [[Boundary Operator]] formalizes algebraically.

## Examples
The standard $2$-simplex in $\mathbb R^3$ has vertices $(1,0,0),(0,1,0),(0,0,1)$; its three edges are the segments between each pair of these vertices, and its three vertices are the $0$-faces.

## See also
[[Simplicial Complex]], [[Geometrically Independent vs Linearly Independent Vectors]], [[Boundary Operator]]
