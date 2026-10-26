---
title: "Hausdorff Distance"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Metric Spaces"
level: BSc
status: drafted
confidence: 0
tags: [metric-spaces, tda]
---
## Definition
Let $A,B$ be non-empty subsets of a [[Metric Space]] $(X,d)$. The **Hausdorff distance** between $A$ and $B$ is
$$
d_H(A,B) = \max\left\{ \sup_{a\in A}\inf_{b\in B} d(a,b),\ \sup_{b\in B}\inf_{a\in A} d(a,b) \right\}.
$$
It measures how far the two sets are from each other: the largest distance one must travel from a point of one set to reach the closest point of the other, taken over both directions. Introduced by Felix Hausdorff in 1914, it is a metric on the set of non-empty compact subsets of $X$.

## Properties
### Equivalent formulation via $r$-neighborhoods
Define the **$r$-neighborhood** of a set $A$ as $A_r = \{x \in X : d(x,A) < r\}$, where $d(x,A) = \inf_{a\in A} d(x,a)$. Then
$$
d_H(A,B) = \inf\{r>0 : A \subseteq B_r \text{ and } B \subseteq A_r\},
$$
i.e. the smallest $r$ such that growing each set by $r$ swallows the other.

### Computing it on finite sets
For finite $A,B$, the two nested suprema/infima reduce to a finite max/min computation over the (finite) pairwise distance table, which makes $d_H$ tractable in practice even though the general definition is expensive for infinite sets.

## Examples
Let $A = \{(0,0),(1,0),(0,1)\}$ and $B = A \cup \{(1,1)\}$ in $\mathbb{R}^2$ with the Euclidean metric ($A \subset B$). Every point of $A$ is at distance $0$ from itself in $B$, so the "$A\to B$" term is $0$; the point $(1,1)\in B$ is at distance $\sqrt 2$ from its nearest neighbor in $A$, so the "$B \to A$" term is $\sqrt2$. Hence $d_H(A,B) = \sqrt 2$. Using the discrete metric instead on the same two sets gives $d_H(A,B)=1$, showing that $d_H$ depends on the ambient metric, not only on the sets.

As a continuous example, if $A$ is the unit circle and $B$ the unit square (both centered at the origin) in $\mathbb{R}^2$, the smallest gap is $0$ (the shapes intersect) and the largest gap is $\sqrt2 - 1$, attained between a vertex of the square and the nearest point of the circle in that direction; so $d_H(A,B)=\sqrt2-1$.

## See also
[[Metric Space]], [[Gromov-Hausdorff Distance]], [[Nerve Complex]]
