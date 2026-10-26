---
title: "Compactness"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Point-Set Topology"
level: BSc
status: drafted
confidence: 0
tags: [topology, tda]
---
## Definition
Let $(X,\tau)$ be a [[Topological Space]]. A subset $A \subseteq X$ is **compact** if every open cover of $A$ has a finite subcover: whenever $A \subseteq \bigcup_{i\in I} U_i$ with each $U_i$ open, there is a finite subset $\{i_1,\dots,i_n\}\subseteq I$ with $A \subseteq \bigcup_{k=1}^n U_{i_k}$. Intuitively, $A$ can always be covered using only finitely many "small" open pieces — compactness generalizes finiteness.

## Properties
### Diameter and boundedness
The **diameter** of $Q \subseteq X$ (in a metric space) is $\operatorname{diam}(Q) = \sup_{x,y\in Q} d(x,y)$ (possibly $\infty$). $Q$ is **bounded** if $\operatorname{diam}(Q) < \infty$.

### Compactness in $\mathbb R^n$: closed and bounded
**Theorem.** $Q \subset \mathbb R^n$ (Euclidean metric) is compact if and only if $Q$ is closed and bounded.

This is a special feature of $\mathbb R^n$; in general metric spaces, compact sets are always closed and bounded, but the converse can fail. **Example.** $Q = \{1/n : n\in\mathbb N\} \subset \mathbb R$ has diameter $1$ (bounded) but is not closed (it does not contain its limit point $0$), so by the theorem it is not compact.

**Consequence used throughout the course.** Any finite point-cloud dataset viewed as a subset of $\mathbb R^n$ is automatically compact, since finite sets are always closed and bounded.

### Continuity theorems (used to prove non-homeomorphism)
**Theorem.** The continuous image of a connected space is connected.

*Proof sketch.* Let $f:X\to Y$ be continuous, $X$ connected, and (WLOG, restricting to the image) $f$ surjective onto $Z=f(X)$. If $Z = A\cup B$ were an open partition, then $f^{-1}(A), f^{-1}(B)$ would be an open partition of $X$ (since $f$ is continuous and surjective, these preimages are open, non-empty, and disjoint), contradicting connectedness of $X$. $\blacksquare$

**Theorem.** The continuous image of a compact space is compact.

*Proof sketch.* Let $f:X\to Y$ continuous, $X$ compact, and $\mathcal A$ an open cover of $f(X)$. By continuity, $\{f^{-1}(A):A\in\mathcal A\}$ is an open cover of $X$; by compactness of $X$, finitely many $f^{-1}(A_1),\dots,f^{-1}(A_n)$ already cover $X$, so $A_1,\dots,A_n$ cover $f(X)$. $\blacksquare$

These two theorems are the standard tools for proving two spaces are **not** [[Homeomorphism|homeomorphic]]: if a candidate homeomorphism existed, the image of a connected (resp. compact) space would have to be connected (resp. compact), so exhibiting a mismatch rules it out.

## Examples
- $\mathbb R \not\cong \mathbb R\setminus\{0\}$: $\mathbb R\setminus\{0\} = (-\infty,0)\cup(0,\infty)$ is disconnected while $\mathbb R$ is connected.
- $[0,1]\not\cong(0,1)$: $[0,1]$ is compact (closed and bounded) while $(0,1)$ is not (not closed).
- Compactness alone is not sufficient to prove equivalence: $S^1$ and $S^2$ are both compact but not homeomorphic — that distinction needs [[Homotopy and Homotopy Equivalence|homotopy theory]] (or [[Betti Numbers]]) rather than compactness.

## See also
[[Connectedness]], [[Closed Set and Closure]], [[Homeomorphism]], [[Betti Numbers]]
