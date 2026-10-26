---
title: "Equivalent Metrics"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Metric Spaces"
level: BSc
status: drafted
confidence: 0
tags: [metric-spaces, tda]
---
## Definition
Let $X$ be a non-empty set and $d_1, d_2$ two metrics on $X$. We say $d_1$ and $d_2$ are **equivalent** if there exist positive constants $c_1,c_2$ such that for all $x,y \in X$
$$
c_1 d_1(x,y) \le d_2(x,y) \le c_2 d_1(x,y).
$$

## Properties
### Equivalent metrics induce the same topology
If $d_1$ and $d_2$ are equivalent, every open ball of one metric contains, and is contained in, an open ball of the other (up to rescaling the radius by $c_1$ or $c_2$), so the collections of open sets they generate coincide. This is the bridge between [[Metric Space|metric geometry]] and [[Metric Topology|topology]]: equivalent metrics are topologically indistinguishable even though they can produce very differently *shaped* balls and spheres (see [[Balls and Spheres]]).

### The standard $\ell_p$ family on $\mathbb{R}^n$
On $X = \mathbb{R}^n$, the Euclidean ($\ell_2$), Manhattan ($\ell_1$), and Chebyshev ($\ell_\infty$) metrics are pairwise equivalent (a consequence of the general fact that all norms on a finite-dimensional vector space are equivalent). The discrete metric on $\mathbb{R}^n$, by contrast, is **not** equivalent to any of these, since no constant $c_2$ can bound $d_{\text{Euclidean}}(x,y) \le c_2 \cdot 1$ for arbitrarily distant $x,y$.

## Examples
Take $X=\mathbb{R}^2$ with $d_1((x_1,y_1),(x_2,y_2)) = |x_1-x_2|+|y_1-y_2|$ (Manhattan) and $d_2 = $ Euclidean. Then $d_2 \le d_1 \le \sqrt{2}\, d_2$, so they are equivalent with $c_1 = 1/\sqrt 2$, $c_2 = 1$ (up to how the inequality is written).

## See also
[[Metric Space]], [[Balls and Spheres]], [[Coarser and Finer Topology]], [[Metric Topology]]
