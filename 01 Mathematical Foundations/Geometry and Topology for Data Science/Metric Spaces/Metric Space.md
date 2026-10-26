---
title: "Metric Space"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Metric Spaces"
level: BSc
status: drafted
confidence: 0
tags: [metric-spaces, tda]
---
## Definition
A **metric** on a non-empty set $X$ is a function $d: X \times X \to \mathbb{R}$ such that for all $x,y,z \in X$:

1. **Non-negativity and identity of indiscernibles**: $d(x,y) \ge 0$, and $d(x,y) = 0$ if and only if $x=y$.
2. **Symmetry**: $d(x,y) = d(y,x)$.
3. **Triangle inequality**: $d(x,z) \le d(x,y) + d(y,z)$.

A pair $(X,d)$ where $d$ is a metric on $X$ is called a **metric space**. Non-negativity is actually redundant: it follows from the triangle inequality and identity of indiscernibles (see Properties).

## Properties
### Non-negativity follows from the triangle inequality
Let $x,y \in X$. By the triangle inequality, $d(x,x) \le d(x,y) + d(y,x)$. Since $d(x,x)=0$ (identity of indiscernibles) and $d(x,y)=d(y,x)$ (symmetry), this gives $0 \le 2d(x,y)$, i.e. $d(x,y) \ge 0$.

### A set can carry many non-equivalent geometries
A single set $X$ can admit more than one metric (e.g. $\mathbb{R}^n$ admits the Euclidean, Manhattan, and Chebyshev metrics among others), and changing the metric changes the metric space $(X,d)$, even though the underlying set is the same. See [[Equivalent Metrics]] for when two such choices induce the same shape.

## Examples
- **Euclidean ($\ell_2$) metric**: on $X=\mathbb{R}^n$, $d(x,y) = \sqrt{\sum_{j=1}^n (x_j-y_j)^2}$.
- **Graph metric**: given a finite graph $\Gamma(V,E)$ (see [[Graph (Topology)]]), define $d(x,y) = \min\{l(\gamma) : \gamma \text{ a path from } x \text{ to } y\}$, the length of the shortest path.
- **Hausdorff metric on subsets**: given a metric space $(X,d)$, the function $d(A,B) = \max\{d_1,d_2\}$ with $d_1 = \sup_{x\in A}\inf_{y \in B} d(x,y)$, $d_2 = \sup_{y\in B}\inf_{x\in A} d(x,y)$ is a metric on the collection of non-empty subsets of $X$. This is developed further in [[Hausdorff Distance]].
- **Discrete metric**: $d(x,y) = 0$ if $x=y$ and $1$ otherwise, defined on any set $X$.

## See also
[[Balls and Spheres]], [[Equivalent Metrics]], [[Hausdorff Distance]], [[Gromov-Hausdorff Distance]], [[Metric Topology]], [[Distance and Similarity Measures in Data Science]]
