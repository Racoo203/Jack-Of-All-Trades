---
title: "Homology Group"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Homology"
level: BSc
status: drafted
confidence: 0
tags: [tda, homology]
---
## Definition
Let $K$ be a [[Simplicial Complex]]. The **$n$-th homology group** of $K$ is the quotient vector space (over $\mathbb Z_2$)
$$
H_n(K) = \frac{\ker \partial_n}{\operatorname{Im}\partial_{n+1}},
$$
where $\partial_n$ is the [[Boundary Operator]]. Concretely, $H_n(K)$ is the set of equivalence classes of $n$-chains that are closed (in $\ker\partial_n$), where two closed chains are declared equivalent if they differ by the boundary of some $(n+1)$-chain.

## Properties
### The intuition: chains equivalent up to a filled-in boundary
Two $n$-chains represent the *same* class in $H_n(K)$ iff they are both boundaries of a shared $(n+1)$-chain (up to $\mathbb Z_2$ addition), i.e. they can be continuously "swept" into one another across a higher-dimensional piece of the complex. An **$n$-hole** is, informally, an $n$-chain that is closed ($\ker\partial_n$) but is *not* itself the boundary of any $(n+1)$-chain — it is not in $\operatorname{Im}\partial_{n+1}$, so it survives as a non-trivial class in $H_n(K)$.

**Worked example (annulus).** Consider $K$ triangulating an annulus with an inner boundary cycle $ab+bc+cd+da$ and an outer one $ef+fg+gh+he$. Both $1$-chains bound the same $2$-chain (the annular region between them), so they represent the same class of $H_1(K)$ — the surviving class corresponds to the "hole" left empty by the annulus, and deformation-retracting the annulus onto a circle makes this visible directly.

**Worked example (filled disk).** For $K$ triangulating a disk with center vertex $e$, the boundary cycle $ab+bc+cd+da$ *is* the boundary of the $2$-chain covering the whole disk, so it is equivalent to $0$ in $H_1(K)$ — consistent with the disk being contractible and having no $1$-dimensional holes.

## Examples
$H_0(K)$ counts connected components (see [[Connectedness]]); $H_1(K)$ counts "tunnels"; $H_2(K)$ counts "voids"; and so on for higher $n$. The dimension of $H_n(K)$ as a vector space is the $n$-th [[Betti Numbers|Betti number]] $\beta_n(K)$.

## See also
[[Chain Group]], [[Boundary Operator]], [[Betti Numbers]], [[Singular Homology]]
