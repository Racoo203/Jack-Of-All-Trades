---
title: "Convex Set"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "NLP Foundations"
level: BSc
status: drafted
confidence: 0
tags: [nonlinear-optimization, convexity, ma2008b]
---
## Definition
A set $A\subseteq\mathbb R^n$ is **convex** if for any $x_1,x_2\in A$ and any $\lambda\in[0,1]$,
$$x=\lambda x_1+(1-\lambda)x_2\in A,$$
i.e. the line segment joining any two points of $A$ lies entirely in $A$. A single point is convex by definition. Examples: a sphere (ball), a triangle, a line, a hyperplane, $\mathbb R^n$ itself.

A point $\bar x\in A$ is an **extreme point** if there are no $x_1\neq x_2$ in $A$ and $\lambda\in(0,1)$ with $\bar x=\lambda x_1+(1-\lambda)x_2$ — it does not lie strictly between two points of the set. Every extreme point is a boundary point, but not conversely (the midpoint of a polygon's edge is a boundary point that is not extreme).

A **convex combination** of $x_1,\dots,x_k$ is $\sum_i\lambda_ix_i$ with $\lambda_i\ge0$, $\sum\lambda_i=1$.

## Properties
### Convex sets contain all convex combinations of their points
*Proof by induction on $k$.* $k=2$ is the definition. Suppose true for $k-1$ and take $x=\sum_{i=1}^k\lambda_ix_i$ with $\lambda_k<1$ (if $\lambda_k=1$, $x=x_k\in A$). Then
$$x=(1-\lambda_k)\underbrace{\sum_{i=1}^{k-1}\frac{\lambda_i}{1-\lambda_k}x_i}_{=:y}+\lambda_kx_k,$$
where the weights of $y$ are nonnegative and sum to $\frac{1-\lambda_k}{1-\lambda_k}=1$, so $y\in A$ by hypothesis; then $x$ is a two-point convex combination of $y,x_k\in A$, so $x\in A$. ∎

### Intersections are convex
If $x_1,x_2\in\bigcap_\alpha A_\alpha$, the segment lies in every $A_\alpha$, hence in the intersection.

### Sublevel sets of convex functions are convex
If $g$ is a [[Convex Function]] and $x_1,x_2\in S=\{x:g(x)\le b\}$, then $g(\lambda x_1+(1-\lambda)x_2)\le\lambda g(x_1)+(1-\lambda)g(x_2)\le b$. Combining with the intersection property:

> **The feasible region $\{x:g_i(x)\le b_i,\ i=1..m\}$ of an NLP is convex whenever every $g_i$ is convex** (Tema 7). Linear equality constraints also preserve convexity (hyperplanes are convex).

### Consequence for optimization
On a convex feasible set, a local minimum of a convex function is global (see [[Convex Function]]). A non-convex feasible region breaks this: there can be several local optima (Tema 7 example with $8x_1-x_1^2+14x_2-x_2^2\le49$, a *concave* constraint function, whose feasible set contains pairs of points whose connecting segment leaves the region).

## See also
[[Convex Function]], [[Nonlinear Programming Problem]], [[Karush–Kuhn–Tucker conditions]], [[Linear Programming]]
