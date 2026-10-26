---
title: "Isotopy"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Point-Set Topology"
level: BSc
status: drafted
confidence: 0
tags: [topology, tda]
---
## Definition
Let $X,Y \subset \mathbb R^n$. An **isotopy** between $X$ and $Y$ is a continuous map
$$
\xi : X \times [0,1] \to \mathbb R^n
$$
such that (1) $\xi(X,0)=X$, (2) $\xi(X,1)=Y$, and (3) for every $t\in[0,1]$, $\xi(\cdot,t)$ is a [[Homeomorphism]] between $X$ and its image $\xi(X,t)$. Isotopies are continuous deformations of one shape into another that never self-intersect and never break a connected piece apart, since each intermediate stage $t$ must itself be a valid homeomorphic copy of $X$.

## Properties
### Isotopy implies homeomorphism, but not conversely
Since every stage $\xi(\cdot,t)$ is a homeomorphism onto its image, in particular $\xi(\cdot,1): X\to Y$ is a homeomorphism, so isotopic spaces are always homeomorphic. The converse fails: two spaces can be topologically equivalent without any isotopy between them, when unwinding one into the other would require passing through a self-intersection.

**Example (mathematical knots).** A mathematical knot is an embedding of $S^1$ into $\mathbb R^3$ (or $S^3$). Every knot is homeomorphic to $S^1$ (as an abstract space) — yet a genuinely knotted curve is *not* isotopic to the standard, unknotted circle, because "untying" it would force the curve to pass through itself at some intermediate stage, violating condition (3).

### The classic coffee-mug/donut deformation
The intuitive picture of continuously reshaping a coffee mug into a donut (or vice versa) is literally an isotopy: at every instant $t$, the deformed shape is still a homeomorphic copy of the mug, and the process never tears or glues the surface.

## Examples
Let $X=\{(x,y): 4x^2+y^2=1\}$ and $Y=\{(x,y):x^2+4y^2=1\}$ (two ellipses in $\mathbb R^2$). The map $\xi(\theta,t) = ((2-t)\cos\theta,\ (1+t)\sin\theta)$ is an isotopy from $X$ to $Y$: at $t=0$ it traces $X$, at $t=1$ it traces $Y$, and each intermediate $t$ traces a non-self-intersecting ellipse.

## See also
[[Homeomorphism]], [[Embedding]], [[Homotopy and Homotopy Equivalence]]
