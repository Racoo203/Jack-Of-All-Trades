---
title: "Metric Topology"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Point-Set Topology"
level: BSc
status: drafted
confidence: 0
tags: [topology, tda]
---
## Definition
Given a [[Metric Space]] $(X,d)$, the **(induced) metric topology** $\mathcal T_d$ is the collection of sets $U \subseteq X$ such that for every $x \in U$ there is an open ball $B_\varepsilon(x)$ (see [[Balls and Spheres]]) contained in $U$, for some $\varepsilon > 0$. Every metric space is canonically a [[Topological Space]] via $\mathcal T_d$.

## Properties
### $\mathcal T_d$ is a genuine topology
Let $T = \{U \subseteq X : \forall x \in X,\ \exists\, B_r(x) \subseteq U\}$ (with the understanding that the condition is only required for $x\in U$). We check the three topology axioms:

- $\emptyset \in T$ vacuously (there is no $x \in \emptyset$ whose condition could fail); $X \in T$ since $B_r(x) \subseteq X$ for any $r>0$.
- **Finite intersections.** Let $U_1,\dots,U_n \in T$ and $x \in \bigcap_{i=1}^n U_i$. Since $U_i \in T$, there is $r_i>0$ with $B_{r_i}(x) \subseteq U_i$ for each $i$. Let $r = \min\{r_1,\dots,r_n\}$; then $B_r(x) \subseteq U_i$ for every $i$, so $B_r(x) \subseteq \bigcap_{i=1}^n U_i$.
- **Arbitrary unions.** Let $\{U_\alpha\}_{\alpha\in I}\subseteq T$ and $x \in \bigcup_{\alpha} U_\alpha$. Then $x \in U_\alpha$ for some $\alpha$, and since $U_\alpha \in T$ there is $r>0$ with $B_r(x) \subseteq U_\alpha \subseteq \bigcup_\alpha U_\alpha$.

Hence $T = \mathcal T_d$ is a topology on $X$.

### Open sets are unions of balls
Intuitively, every open set in $\mathcal T_d$ is built out of unions of open balls, which is why one might think the "shape" of $X$ depends on which balls (i.e. which metric) is chosen. [[Equivalent Metrics|Equivalent metrics]], however, produce the same metric topology, so the topology is coarser information than the metric itself.

## Examples
On $\mathbb R^2$, the Euclidean, Manhattan, and Chebyshev metrics all induce the *same* metric topology (the standard topology on $\mathbb R^2$), even though their balls have different shapes (disk vs. diamond vs. square) — this is a direct consequence of [[Equivalent Metrics]].

## See also
[[Metric Space]], [[Topological Space]], [[Coarser and Finer Topology]], [[Continuous Function (Topology)]]
