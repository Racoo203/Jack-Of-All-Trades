---
title: "Graph (Topology)"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Simplicial Complexes"
level: BSc
status: drafted
confidence: 0
tags: [tda, simplicial-complexes]
---
## Definition
A **directed graph** $G$ is a collection of vertices $V=\{v_j\}_{j\in I}$ and edges $E \subseteq V\times V$ (ordered pairs). $G$ is **finite** if $V,E$ are finite; **simple** if it has no loops or multiple edges; **undirected** if $E$ is closed under $(v_i,v_j)\sim(v_j,v_i)$. A **subgraph** of $G$ is a graph $H$ with $V(H)\subseteq V(G)$, $E(H)\subseteq E(G)$. A **path** of length $n$ is a sequence $v_1,\dots,v_n$ with $(v_i,v_{i+1})\in E$ for all $i$; a path whose initial and terminal vertices coincide is a **cycle**. $G$ is **connected** if there is a path between every pair of vertices.

## Properties
### Graphs carry a metric
Given a finite graph $\Gamma=(V,E)$, define $d(x,y) = \min\{l(\gamma)\}$ over all paths $\gamma$ from $x$ to $y$ (see [[Metric Space]]). This makes $(V,d)$ a metric space, the **graph metric**, used throughout TDA whenever the data naturally form a network rather than points in $\mathbb R^n$.

### Graph topology
A **graph topology** on $G=(V,E)$ is a collection of subgraphs $\mathcal T = \{G_i\}_{i\in I}$ such that: (1) the null graph $K_0$ (empty vertex set) and $G$ itself belong to $\mathcal T$; (2) $\mathcal T$ is closed under arbitrary unions; (3) $\mathcal T$ is closed under finite intersections — the same three axioms as an ordinary [[Topological Space]], but applied to subgraphs rather than subsets. A subgraph $H$ is **open in $G$** if $H\in\mathcal T$. The $\mathcal T$-neighborhood of a vertex $v$ (or edge $e$) is any open subgraph containing $v$ (resp. $e$).

## Examples
Let $\Gamma$ have $V=\{a,b,c,d\}$, $E=\{(a,d),(b,d),(c,d)\}$ (a "tripod"). The collection $\tau = 2^{T_1}\cup T_2$, with $T_1=\{\{(a,d)\},\{(b,d)\},\{(c,d)\}\}$ and $T_2$ built from vertex-inclusive subgraphs around $d$, is a graph topology for $\Gamma$ — this topology is closely tied to the metric-space structure the graph metric induces on $\Gamma$.

## See also
[[Simplex]], [[Simplicial Complex]], [[Metric Space]]
