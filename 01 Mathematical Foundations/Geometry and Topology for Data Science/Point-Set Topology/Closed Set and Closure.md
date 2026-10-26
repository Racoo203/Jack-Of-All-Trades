---
title: "Closed Set and Closure"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Point-Set Topology"
level: BSc
status: drafted
confidence: 0
tags: [topology, tda]
---
## Definition
Let $(X,\tau)$ be a [[Topological Space]]. A subset $A \subseteq X$ is **closed** if its complement $X\setminus A$ is open. Since closedness is defined via the complement's openness, whether a set is closed depends on the ambient topology — a set closed in one topology on $X$ need not be closed in another.

Given $A \subseteq X$, its **closure** $\overline A$ is the intersection of all closed sets containing $A$ — the smallest closed set that contains $A$.

## Properties
### Basic closed-set algebra
1. $\emptyset$ and $X$ are always closed (they are the complements of $X$ and $\emptyset$, both open by the topology axioms).
2. The intersection of any collection of closed sets is closed (complement of a union of open sets, which is open).
3. The union of a *finite* collection of closed sets is closed (complement of a finite intersection of open sets).

### Characterizing the closure via open neighborhoods
**Theorem.** $x \in \overline A$ if and only if every open set $U$ containing $x$ intersects $A$.

This gives a practical way to test membership in the closure without enumerating every closed superset of $A$: one only needs to check, for each candidate $x$, whether every open neighborhood of $x$ meets $A$.

## Examples
- In $\mathbb R$ with the standard topology: $\overline{(0,1)} = [0,1]$, $\overline{[0,1]} = [0,1]$, and $\overline{[0,1)} = [0,1]$ — a set and sets differing from it by boundary points can share the same closure.
- With the trivial topology on $X$, the closure of *any* non-empty subset is all of $X$ (the only closed sets are $\emptyset$ and $X$).
- With the finite-complement topology $\tau_{cf}$, the only closed sets are $X$ itself and the finite subsets of $X$.
- $X = \mathbb{R}$ with the discrete topology: every subset is both open and closed, so every set equals its own closure.

## See also
[[Topological Space]], [[Connectedness]], [[Compactness]], [[Homeomorphism]]
