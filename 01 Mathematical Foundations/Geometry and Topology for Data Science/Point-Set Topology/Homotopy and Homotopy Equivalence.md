---
title: "Homotopy and Homotopy Equivalence"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Point-Set Topology"
level: BSc
status: drafted
confidence: 0
tags: [topology, tda]
---
## Definition
Let $f,g:X\to Y$ be continuous functions between [[Topological Space|topological spaces]]. A **homotopy** between them is a continuous map
$$
H : X\times[0,1] \to Y, \qquad H(\cdot,0)=f,\quad H(\cdot,1)=g.
$$
$f$ and $g$ are **homotopic** if such an $H$ exists. Two spaces $X,Y$ are **homotopy equivalent** if there are continuous maps $g:X\to Y$, $h:Y\to X$ such that $h\circ g$ is homotopic to $\mathrm{id}_X$ and $g\circ h$ is homotopic to $\mathrm{id}_Y$. Homotopy equivalence is strictly weaker than [[Homeomorphism]]: it only asks the composites to be *deformable* to the identity, not equal to it.

If $X$ is homotopy equivalent to a single point, $X$ is called **contractible**.

## Properties
### Contractibility of balls and Euclidean space
The identity $f:\mathbb B^n \to \mathbb R^n$ and the constant map $g\equiv 0$ are homotopic via $H(x,t)=(1-t)x$ (a "straight-line" homotopy), so every ball in $\mathbb R^n$ (and $\mathbb R^n$ itself, by the same formula) is contractible.

### The punctured plane deformation-retracts to a circle
Let $f:\mathbb R^2\setminus\{0\}\to\mathbb R^2\setminus\{0\}$ be the identity and $g(x) = x/\lVert x\rVert$ (radial projection onto $S^1$). The straight-line homotopy $H(x,t) = (1-t)x + t\,g(x)$ never passes through $0$ (since it interpolates between $x$ and a positive scalar multiple of $x$), so it is a valid homotopy. Consequently, $\mathbb R^2\setminus\{0\}$ is homotopy equivalent to $S^1$ — even though the two are clearly not homeomorphic (one is bounded/compact-looking in cross-section, the other is not).

### Deformation retracts
A **retraction** of $X$ onto $U\subset X$ is a map $r:X\to U$ with $r(x)=x$ for all $x\in U$. $U$ is a **deformation retract** of $X$ if the identity map on $X$ can be continuously deformed into $r$ while fixing $U$ pointwise throughout. If $U$ is a deformation retract of $X$, then $X$ and $U$ are homotopy equivalent — this is the standard way homotopy equivalences are constructed in practice (e.g. a point is a deformation retract of any ball).

### Homotopy equivalence is a genuinely weaker invariant
$S^1$ is not homotopy equivalent to a point (any deformation retraction of $S^1$ to a point would have to "tear" the circle), but $S^1$ *is* homotopy equivalent to a point once embedded as a subset of $S^2$ — homotopy equivalence, unlike an intrinsic invariant, can depend on which ambient space a subset is considered inside.

## Examples
The coffee mug is homotopy equivalent to $S^1$ (both have "one hole"), but neither is homotopy equivalent to a solid ball or a point. This is the intuition underlying why $\beta_1$ (the first [[Betti Numbers|Betti number]]) — a homotopy invariant — distinguishes them, even where compactness alone (shared by both) cannot.

## See also
[[Isotopy]], [[Homeomorphism]], [[Betti Numbers]], [[Homology Group]]
