---
title: "Coarser and Finer Topology"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Point-Set Topology"
level: BSc
status: drafted
confidence: 0
tags: [topology, tda]
---
## Definition
Let $X$ be a set and $\mathcal T_1,\mathcal T_2$ two topologies on $X$. We say $\mathcal T_1$ is **coarser** than $\mathcal T_2$ (equivalently, $\mathcal T_2$ is **finer** than $\mathcal T_1$) if $\mathcal T_1 \subseteq \mathcal T_2$, i.e. every open set of $\mathcal T_1$ is also open in $\mathcal T_2$.

## Properties
### Ordering topologies on a fixed set
This containment gives a partial order on the topologies of $X$: the trivial topology $\{\emptyset,X\}$ is the coarsest possible topology, and the discrete topology $\mathcal P(X)$ is the finest. The [[Metric Topology]] $\mathcal T_d$ induced by any metric $d$ sits strictly between these two extremes in general.

### Equivalent metrics induce comparably-ordered topologies
If $d_1,d_2$ are [[Equivalent Metrics]], their induced metric topologies coincide (neither is strictly coarser). If $d_1$ and $d_2$ are *not* equivalent, one metric topology can be strictly finer than the other: for instance the Euclidean metric topology $T_1$ on $X=\mathbb R^2$ is finer than the topology $T_2$ induced by the indiscrete (trivial) metric-like relation, because the open balls of $T_2$ are contained in the open sets of $T_1$ but not conversely.

## Examples
Let $X=\mathbb R^2$, $T_1$ the metric topology from the Euclidean metric, and $T_2$ the metric topology from the Manhattan metric. Since these metrics are equivalent, $T_1$ and $T_2$ coincide — each is coarser *and* finer than the other. Both are coarser than the discrete topology on $X$, since every open ball is a proper subset of $X$ that the discrete topology would further subdivide into individual points.

## See also
[[Topological Space]], [[Metric Topology]], [[Equivalent Metrics]]
