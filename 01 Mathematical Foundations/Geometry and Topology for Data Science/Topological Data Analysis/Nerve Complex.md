---
title: "Nerve Complex"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Topological Data Analysis"
level: BSc
status: drafted
confidence: 0
tags: [tda]
---
## Definition
Given a finite collection of sets $\mathcal U = \{U_\alpha\}_{\alpha\in A}$ (a **cover**, if their union contains the ambient space), the **nerve** of $\mathcal U$ is the [[Simplicial Complex]] $N(\mathcal U)$ whose vertex set is the index set $A$, where $\{a_0,\dots,a_k\}\subseteq A$ spans a $k$-simplex iff
$$
U_{a_0}\cap U_{a_1}\cap\cdots\cap U_{a_k} \ne \emptyset.
$$

## Properties
### Nerve Theorem
**Theorem.** Given a finite cover $\mathcal U$ (open or closed) of a metric space $M$, the geometric realization $|N(\mathcal U)|$ is [[Homotopy and Homotopy Equivalence|homotopy equivalent]] to $M$, provided every non-empty intersection $\bigcap_{i=0}^k U_{a_i}$ of cover elements is itself contractible (homotopy equivalent to a point).

This theorem is the reason nerve complexes matter for data analysis: under its hypothesis, the (usually much smaller, purely combinatorial) simplicial complex $N(\mathcal U)$ retains all the homotopy-type information of the possibly complicated space $M$, so homology can be computed on $N(\mathcal U)$ instead.

### Standard TDA nerve constructions
The three standard covers used in TDA to build a nerve from a finite point cloud are: balls of a fixed radius around each point ([[Čech Complex]]), the metric-threshold condition directly on pairs ([[Vietoris-Rips Complex]], a coarser approximation that is not always literally a nerve but shares its persistence structure), and nearest-point (Voronoi) regions intersected with balls ([[Alpha Complex]]).

### Filtrations from nerves
Since nerve complexes are typically built with a scale parameter $r$ (e.g. the radius of the covering sets), varying $r$ produces a **filtration**: a nested sequence $K^0 \subseteq K^1 \subseteq \cdots$, and the resulting sequence of inclusions is exactly a [[Persistent Set]] of simplicial complexes.

## Examples
Let $X=\{a,b,c,d\}\subset\mathbb R^2$ and $\mathcal U=\{U_a,U_b,U_c,U_d\}$ with $\{a,b\}\subset U_a$, $\{a,b,c\}\subset U_b$, $\{c,d\}\subset U_c$, $\{d\}\subset U_d$. Since $U_a\cap U_b\supset\{a,b\}\ne\emptyset$ and $U_b\cap U_c\supset\{c\}\ne\emptyset$, but $U_a\cap U_c=\emptyset$, the nerve $N(\mathcal U)$ is a path graph $a-b-c-d$ (no triangle, since no triple intersection is non-empty). Choosing a different cover $\mathcal U'=\{U_1,U_2,U_3\}$ with $\{a,b,c\}\subset U_1$, $\{a,c,d\}\subset U_2$, $\{b,c,d\}\subset U_3$ instead yields a triangle-shaped nerve on three vertices — illustrating that the nerve depends entirely on the choice of cover, not only on the underlying point set.

## See also
[[Čech Complex]], [[Vietoris-Rips Complex]], [[Alpha Complex]], [[Persistent Set]], [[Homotopy and Homotopy Equivalence]]
