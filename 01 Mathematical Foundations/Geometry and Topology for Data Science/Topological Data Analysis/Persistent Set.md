---
title: "Persistent Set"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Topological Data Analysis"
level: BSc
status: drafted
confidence: 0
tags: [tda]
---
## Definition
A **persistent set** is a family of sets $\{X_R\}_{R\ge0}$ together with maps $X_R \to X_{R'}$ defined whenever $R\le R'$, such that:

1. The map $X_R \to X_R$ is the identity.
2. The composite $X_R \to X_{R'} \to X_{R''}$ equals the direct map $X_R \to X_{R''}$ (functoriality).

This is the abstract pattern underlying persistence in TDA: it can be instantiated with "sets" replaced by simplicial complexes, vector spaces, or topological spaces, and it packages "how a structure evolves as a scale parameter grows" into a single coherent algebraic object.

## Properties
### Instances of a persistent set in this course
- **Single-linkage clusters** $\{X_R\}$ from [[Single Linkage Clustering and Dendrograms]], with $X_R \to X_{R'}$ sending a cluster to the (unique) coarser cluster containing it.
- **Filtrations of simplicial complexes**: a nested sequence $K^0 \subseteq K^1 \subseteq \cdots \subseteq K^n = K$ (see [[Triangulation and Euler Characteristic]] for a static analogue), such as the [[Čech Complex]], [[Vietoris-Rips Complex]], or [[Alpha Complex]] built at increasing radius $r$, with the maps being simplicial inclusions.
- Applying [[Homology Group|homology]] to a filtration of complexes turns a persistent set of spaces into a persistent set of vector spaces — this is **persistent homology**, whose "how long does a feature survive across the filtration" question is the central object the module's persistence-diagram material addresses (module content flagged as an open question in the course MOC, pending slides).

## Examples
The three snapshots of a [[Čech Complex]] at increasing radius $r=0.5,1,2$ around four corner points of a unit square form a persistent set of simplicial complexes: at $r=0.5$ the complex is $4$ isolated vertices, at $r=1$ it gains edges and one filled triangle, and at $r=2$ it becomes the full $3$-simplex — three "snapshots," connected by inclusion maps, of the same underlying filtration.

## See also
[[Single Linkage Clustering and Dendrograms]], [[Čech Complex]], [[Vietoris-Rips Complex]], [[Gromov-Hausdorff Distance]]
