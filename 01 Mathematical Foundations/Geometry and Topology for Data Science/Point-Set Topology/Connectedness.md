---
title: "Connectedness"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Point-Set Topology"
level: BSc
status: drafted
confidence: 0
tags: [topology, tda]
---
## Definition
Let $(X,\tau)$ be a [[Topological Space]] and $Y \subseteq X$. An **open partition** of $Y$ is a collection of non-empty open subsets $\{A_i\}_{i\in I}$ of $X$ such that $Y \subseteq \bigcup_i A_i$ and $A_i \cap A_j = \emptyset$ for $i\ne j$. We say $Y$ is **disconnected** if there exist $A,B$ forming an open partition of $Y$ into exactly two non-empty disjoint open (in $Y$) pieces; otherwise $Y$ is **connected**.

$A \subseteq X$ is **path-connected** if for every pair of points $x,y \in A$ there is a continuous function $\gamma:[0,1]\to A$ with $\gamma(0)=x,\gamma(1)=y$ (a *path*).

## Properties
### Basic connectedness algebra
1. $\emptyset$ and $X$ are always connected (trivially, from the definitions).
2. The intersection of any collection of connected sets is connected (assuming non-empty intersection in the relevant sense used by the course).
3. The union of a finite collection of connected sets is connected (again, under a shared-point hypothesis).

### Path-connected implies connected
**Theorem.** Every path-connected set is connected.

*Proof.* Let $A \subseteq X$ be path-connected and suppose, for contradiction, that $A$ is disconnected: $A = U \cup V$ for non-empty, disjoint, open (in $A$) $U,V$. Pick $x\in U, y\in V$. By path-connectedness there is a continuous $\gamma:[0,1]\to A$ with $\gamma(0)=x,\gamma(1)=y$. Then $\gamma^{-1}(U)$ and $\gamma^{-1}(V)$ are non-empty, disjoint, open subsets of $[0,1]$ whose union is all of $[0,1]$ — an open partition of $[0,1]$. But $[0,1]$ is connected (standard fact about intervals of $\mathbb R$), a contradiction. Hence $A$ is connected. $\blacksquare$

The converse fails in general (there exist connected sets that are not path-connected), but for the spaces used in this course (subsets of $\mathbb R^n$, simplicial complexes) the two notions coincide in practice.

### Connected components
Define $x \sim y$ if there is a connected set $A\subseteq X$ with $x,y\in A$. This is an equivalence relation, and its equivalence classes are the **connected components** of $X$ — equivalently, the maximal connected subsets of $X$ under inclusion.

**Theorem.** The connected components of $X$ form a partition of $X$, and each connected component is closed in $X$.

In data science terms, connected components are the topological analogue of *clusters*: $\beta_0$ (the zeroth [[Betti Numbers|Betti number]]) counts them, and [[Single Linkage Clustering and Dendrograms]] recovers them at a given distance threshold.

## Examples
- $X=\mathbb R$ with the discrete topology: connected components are the singletons $\{x\}$. With the standard topology, $\mathbb R$ itself is the only (hence one) connected component.
- $X=\{a,b,c,d\}$, $\tau=\{\emptyset,\{a\},\{b\},\{a,b\},X\}$: $\{a,b\}$ is disconnected (partitioned by $\{a\},\{b\}$), while $\{a,c\}$ is connected (no valid open partition exists).
- $[0,1]\cup(2,5) \subset \mathbb{R}$ is disconnected via the open partition $(-1/2,3/2)$ and $(2,5)$.

## See also
[[Compactness]], [[Continuous Function (Topology)]], [[Homeomorphism]], [[Betti Numbers]], [[Single Linkage Clustering and Dendrograms]]
