---
title: "Gromov-Hausdorff Distance"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Metric Spaces"
level: BSc
status: drafted
confidence: 0
tags: [metric-spaces, tda]
---
## Definition
The [[Hausdorff Distance]] compares two *subsets* of the *same* metric space. The **Gromov-Hausdorff distance** generalizes this to compare two entire metric spaces $(X,d_X)$ and $(Y,d_Y)$ that need not live inside a common ambient space. Formally,
$$
d_{GH}(X,Y) = \inf\left\{ d_H(f(X),g(Y)) : f:X\to Z,\ g:Y\to Z \text{ isometric embeddings} \right\},
$$
where the infimum ranges over all metric spaces $Z$ and all isometric embeddings $f,g$ of $X$ and $Y$ into $Z$ (an isometric embedding is a continuous, surjective-onto-its-image map that preserves all pairwise distances).

## Properties
### Finite-space construction via a combined distance matrix
For finite $X=\{x_1,\dots,x_n\}$ and $Y=\{y_1,\dots,y_m\}$, take $Z = X \sqcup Y$ (disjoint union) and choose the cross-distances $d_{XY}(x_i,y_j)$ so that the combined distance matrix $D_Z$ (with $X$'s and $Y$'s own distance blocks fixed, and the cross-block filled by $d_{XY}$) satisfies the triangle inequality. The Gromov-Hausdorff distance is then the infimum, over all valid choices of $d_{XY}$, of the Hausdorff distance between $X$ and $Y$ inside $(Z,D_Z)$.

**Worked example.** Let $X=\{x_1\}$ (a point) and $Y=\{y_1,y_2\}$ with $d_Y(y_1,y_2)=1$. Writing $d_{XY}(x_1,y_1)=a$, $d_{XY}(x_1,y_2)=b$, the triangle inequality on $D_Z$ forces $a+b\ge 1$, $a+1\ge b$, $b+1\ge a$ — so increasing $a$ forces $b$ to decrease and vice versa. The Hausdorff distance of $X,Y$ inside $Z$ is $\max\{a,b\}$, and minimizing this over admissible $(a,b)$ gives $a=b=1/2$, so $d_{GH}(X,Y) = 1/2$.

### Computational cost
Even for finite metric spaces, computing $d_{GH}$ exactly is computationally expensive, since it optimizes over all admissible cross-distance assignments (equivalently, over all "matchings" between $X$ and $Y$). In practice this limits its direct use to small point sets.

## Examples
In TDA, $d_{GH}$ is used to compare two [[Nerve Complex|persistence diagrams]] (viewed as finite metric spaces): it is more robust to noise than the alternative bottleneck distance, though also more expensive to compute.

## See also
[[Hausdorff Distance]], [[Metric Space]], [[Persistent Set]]
