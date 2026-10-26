---
title: "Single Linkage Clustering and Dendrograms"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Topological Data Analysis"
level: BSc
status: drafted
confidence: 0
tags: [tda]
---
## Definition
Let $X$ be a finite [[Metric Space]] and $R>0$. Define $x \sim_R x'$ if $d(x,x')\le R$. This relation is reflexive and symmetric but **not transitive** in general, so it is not itself an equivalence relation; taking the equivalence relation it *generates* (transitive closure) and partitioning $X$ by its classes produces the **Single Linkage Clustering** of $X$ at threshold $R$.

A **dendrogram** of $X$ is a tree such that: (1) the leaves are the points of $X$; (2) the internal nodes are clusters of $X$; (3) the root is the cluster containing all of $X$; (4) the distance between two clusters is the minimum distance between a point of one and a point of the other. It is built by: starting with each point as its own leaf-cluster, repeatedly merging the two closest clusters into a new one, until a single cluster remains.

## Properties
### Reading $\beta_0$ off the dendrogram
Drawing a horizontal line across the dendrogram at height $R$, the number of tree-branches it crosses equals the number of single-linkage clusters at threshold $R$ — equivalently, $\beta_0(R)$, the zeroth [[Betti Numbers|Betti number]] of the Vietoris-Rips-type complex at scale $R$ (see [[Connectedness#Connected Components]]). As $R$ increases the partition **coarsens**: clusters only ever merge, never split, which is what makes the dendrogram a valid tree rather than a general graph.

### Persistence of the clustering
Because clusters only merge as $R$ grows, there are well-defined maps $X_R \to X_{R'}$ (send each cluster at level $R$ to the unique cluster at level $R'$ containing it) whenever $R \le R'$. This is exactly the structure of a [[Persistent Set]]: $\{X_R\}_{R\ge0}$, with the identity map at $R=R$ and compatible composition $X_R\to X_{R'}\to X_{R''}$ equal to the direct map $X_R \to X_{R''}$.

## Examples
Let $X=\{x_1,\dots,x_6\}\subset\mathbb R^2$ with pairwise distances given by a distance matrix such that $d(x_1,x_2)=d(x_3,x_4)=d(x_5,x_6)=1/2$, $d(x_1,x_3)=d(x_1,x_4)=d(x_2,x_3)=d(x_2,x_4)=1$, $d(x_1,x_5)=d(x_1,x_6)=d(x_2,x_5)=d(x_2,x_6)=2$, $d(x_3,x_5)=d(x_3,x_6)=d(x_4,x_5)=d(x_4,x_6)=1$, $d(x_5,x_6)=1/2$ (and symmetric otherwise). At $R=1/4$: $6$ clusters (each point alone). At $R=1$: $3$ clusters ($\{x_1,x_2\},\{x_3,x_4\},\{x_5,x_6\}$). At $R=2$: $2$ clusters. At $R=3$: $1$ cluster. The dendrogram encodes this by first merging $\{x_1,x_2\}$, $\{x_3,x_4\}$, $\{x_5,x_6\}$ at height $1/2$, then $\{x_1,x_2,x_3,x_4\}$ at height $1$, then the whole set at height $2$.

## See also
[[Connectedness]], [[Persistent Set]], [[Betti Numbers]], [[Metric Space]]
