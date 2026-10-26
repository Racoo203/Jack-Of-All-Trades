---
title: "Geometrically Independent vs Linearly Independent Vectors"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Simplicial Complexes"
level: BSc
status: drafted
confidence: 0
tags: [tda, simplicial-complexes, linear-algebra]
---
## Definition
Let $v_0,v_1,\dots,v_m \in \mathbb R^n$.

- The set is **geometrically independent** if, whenever real numbers $t_0,\dots,t_m$ satisfy both $\sum_{i=0}^m t_i = 0$ and $\sum_{i=0}^m t_i v_i = \vec 0$, it follows that $t_i=0$ for every $i$.
- The set is **linearly independent** if, whenever $\sum_{i=0}^m t_i v_i = \vec 0$, it follows that $t_i=0$ for every $i$.

Geometric independence is the condition a set of $m+1$ points in $\mathbb R^n$ must satisfy in order for their convex hull to be a genuine (non-degenerate) $m$-dimensional [[Simplex]] — it is exactly the notion of *affine independence* used elsewhere in the literature.

## Properties
### Equivalence theorem
**Theorem.** $v_0,v_1,\dots,v_m \in \mathbb R^n$ are geometrically independent if and only if $v_1-v_0,\ v_2-v_0,\ \dots,\ v_m-v_0$ are linearly independent.

*Proof.* ($\Rightarrow$) Suppose $v_0,\dots,v_m$ are geometrically independent, and suppose $\sum_{i=1}^m t_i'(v_i-v_0)=\vec 0$. Expanding, $\sum_{i=1}^m t_i' v_i - \left(\sum_{i=1}^m t_i'\right) v_0 = \vec 0$. Set $t_0' = -\sum_{i=1}^m t_i'$, so that $\sum_{i=0}^m t_i' = 0$ automatically. Substituting,
$$
\sum_{i=0}^m t_i' v_i = t_0' v_0 + \sum_{i=1}^m t_i' v_i = t_0' v_0 + \left(\sum_{i=1}^m t_i'\right)v_0 = v_0\sum_{i=0}^m t_i' = \vec 0.
$$
So both $\sum_{i=0}^m t_i'=0$ and $\sum_{i=0}^m t_i' v_i = \vec 0$ hold; geometric independence then forces $t_i'=0$ for all $i \in \{0,\dots,m\}$. In particular $t_i'=0$ for $i=1,\dots,m$, so $v_1-v_0,\dots,v_m-v_0$ are linearly independent.

($\Leftarrow$) Suppose $v_1-v_0,\dots,v_m-v_0$ are linearly independent, and suppose $\sum_{i=0}^m t_i'=0$ and $\sum_{i=0}^m t_i' v_i=\vec 0$. From the first equation, $t_0' = -\sum_{i=1}^m t_i'$. Substituting into the second and rearranging,
$$
\sum_{i=1}^m t_i' v_i - \left(\sum_{i=1}^m t_i'\right) v_0 = \sum_{i=1}^m t_i'(v_i-v_0) = \vec 0.
$$
By linear independence of $v_1-v_0,\dots,v_m-v_0$, this forces $t_i'=0$ for $i=1,\dots,m$, and then $t_0' = -\sum_{i=1}^m t_i' = -0 = 0$ as well. Hence $t_i'=0$ for all $i\in\{0,\dots,m\}$, proving geometric independence. $\blacksquare$

### Why this matters for simplices
The definition of an $n$-simplex as the convex hull of $n+1$ points requires those points to be geometrically (affinely) independent — otherwise the "hull" collapses into a lower-dimensional object (e.g. three collinear points do not span a genuine triangle). The theorem gives a practical linear-algebra test (row-reduce the difference vectors and check their rank) for this geometric condition.

## Examples
The three points $(0,0),(1,0),(0,1)\in\mathbb R^2$ are geometrically independent, since $(1,0)-(0,0)=(1,0)$ and $(0,1)-(0,0)=(0,1)$ are linearly independent; their convex hull is a genuine (non-degenerate) $2$-simplex (a filled triangle). By contrast, $(0,0),(1,0),(2,0)$ are *not* geometrically independent, since $(1,0)-(0,0)=(1,0)$ and $(2,0)-(0,0)=(2,0)$ are linearly dependent (parallel); the three points are collinear and their "hull" is just a segment, not a triangle.

## See also
[[Simplex]], [[Simplicial Complex]]
