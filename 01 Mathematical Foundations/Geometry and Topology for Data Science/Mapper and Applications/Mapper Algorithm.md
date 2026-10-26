---
title: "Mapper Algorithm"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Mapper and Applications"
level: BSc
status: drafted
confidence: 0
tags: [tda, mapper]
---
## Definition
The **Mapper algorithm** produces a graph-shaped summary of the topological structure of a dataset $X$. Given a **filter function** $f: X \to \mathbb R^d$ (see [[Mapper Filter Functions]]), Mapper proceeds as:

1. Project the data via $f$ into $\mathbb R^d$.
2. Cover the image $f(X)$ with a finite collection $\{U_i\}_{i\le n}$ of overlapping intervals/regions, typically of equal size and uniformly distributed, with a chosen percentage of overlap between neighbors.
3. For each preimage $f^{-1}(U_i)$, run a clustering algorithm to split it into clusters $C_{i,j}$, $j \le m_i$.
4. Build the (undirected) **Mapper graph**: one node per cluster $C_{i,j}$, with an edge between two nodes iff their underlying clusters intersect (share at least one data point).

In the resulting graph, each node represents a subset of the original data, and each edge represents a proximity/connectivity relationship — in theory, the topological properties of the original dataset persist in this compressed representation.

## Properties
### Mapper as an approximate nerve
The cover-then-cluster-then-connect construction is, informally, an instance of building a [[Nerve Complex]] out of a cover of $X$ induced by pulling back a cover of $f(X)$ — the overlap between adjacent regions $U_i$ is what allows two different clusters (from different preimages) to be connected when they share data points, mirroring the nerve's rule of connecting sets with non-empty intersection.

### Sensitivity to filter and cover choice
Different filter functions (see [[Mapper Filter Functions]]) reveal different structure in the same dataset — since Mapper only sees the data through $f$ and the chosen cover/clustering, its output graph is not a canonical topological invariant of $X$ but a summary that depends on these modeling choices. Combining several filters (e.g. density + eccentricity + UMAP) can reveal structure that no single filter shows alone, at the cost of a more complex, harder-to-interpret graph.

## Examples
In a course project applying Mapper to European football statistics with the density and UMAP filters, the resulting graph split into four connected components; the largest ones organized players along axes such as "goals scored" and "passing/ball-touch volume," while a lone isolated node captured a small group of statistically atypical player-seasons. Different filter-pair choices (PCA+density, eccentricity+PCA, density+eccentricity+UMAP) produced visibly different groupings of the same underlying dataset, illustrating the filter-dependence above.

## See also
[[Mapper Filter Functions]], [[Nerve Complex]], [[Takens' Embedding Theorem]]
