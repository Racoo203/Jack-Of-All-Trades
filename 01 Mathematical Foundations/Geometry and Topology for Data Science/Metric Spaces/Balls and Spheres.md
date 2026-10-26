---
title: "Balls and Spheres"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Metric Spaces"
level: BSc
status: drafted
confidence: 0
tags: [metric-spaces, tda]
---
## Definition
Let $(X,d)$ be a [[Metric Space]], $x \in X$, and $r>0$.

- The **open ball** of radius $r$ centered at $x$ is $B_r(x) = \{y \in X : d(x,y) < r\}$.
- The **closed ball** of radius $r$ centered at $x$ is $\bar B_r(x) = \{y \in X : d(x,y) \le r\}$.
- The **sphere** of radius $r$ centered at $x$ is $S_r(x) = \{y \in X : d(x,y) = r\}$.

The closed ball is the union of the open ball and the sphere: $\bar B_r(x) = B_r(x) \cup S_r(x)$.

## Properties
### The metric determines the shape of balls and spheres
Naively, the metric acts as a ruler and the balls/spheres it produces are the "shape" of the space at scale $r$. In $\mathbb{R}^2$ with the Euclidean metric, $S_r(x)$ is a circle and $B_r(x)$ its interior disk. With the **Manhattan metric** $d_1((x_1,y_1),(x_2,y_2)) = |x_1-x_2|+|y_1-y_2|$ (the *taxicab geometry*, since distance is measured by moving along coordinate axes, as a taxicab or a chess rook would), the sphere of radius $r$ centered at the origin is the set $\{(x,y): |x|+|y|=r\}$, a square with vertices $(\pm r, 0), (0,\pm r)$ — not a Euclidean circle. In general, for $\ell_p$ metrics on $\mathbb{R}^2$ with $p \ne 2$, spheres look like "rectangular circles." The shape of a sphere does not change under translation of its center; it depends only on the metric.

### Comparison of geometries in $\mathbb{R}^2$
- **Chebyshev distance**: $d_\infty((x_1,y_1),(x_2,y_2)) = \max\{|x_1-x_2|,|y_1-y_2|\}$, also called the *chessboard metric* since it is the number of moves a king needs on a chessboard.
- **Cosine distance**: $d_\theta((x_1,y_1),(x_2,y_2)) = \sqrt{1-\cos\theta}$ where $\theta$ is the angle between the two points (as vectors from the origin). This is *not* a metric in general (it can fail the axioms), but it is used pervasively in data science as an "almost-distance" — see [[Distance and Similarity Measures in Data Science]].
- **Discrete metric**: every pair of distinct points is at distance $1$, so $B_1(x)$ contains the whole space while $B_r(x) = \{x\}$ for $r<1$.

## Examples
Under the Manhattan metric on $\mathbb{R}^2$, the closed ball $\bar B_r(x,y)$ is the (filled) square with vertices $(x+r,y),(x,y+r),(x-r,y),(x,y-r)$ — a rotated square, distinct in shape from the Euclidean disk of the same radius, even though both are centered at $(x,y)$.

## See also
[[Metric Space]], [[Equivalent Metrics]], [[Metric Topology]]
