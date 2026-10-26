---
title: "Quotient Space"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Point-Set Topology"
level: BSc
status: drafted
confidence: 0
tags: [topology, tda]
---
## Definition
Let $(X,\tau_X)$ be a [[Topological Space]] and $\sim$ an equivalence relation on $X$. The **quotient set** is $Y = X/\!\sim\ = \{[x] : x\in X\}$, the set of equivalence classes. The **quotient topology** on $Y$ declares $U \subseteq Y$ open iff $\{x\in X : [x]\in U\}$ is open in $X$. The **canonical projection** $\pi:X\to X/\!\sim$, $x\mapsto[x]$, is then continuous (in fact it is an [[Embedding|embedding]] in the appropriate sense used by the course).

## Properties
### "Crushing" a subset to a point
Given $A\subset X$, define $x\sim y \iff x,y\in A$ (with singletons otherwise unrelated to anything but themselves). The resulting quotient $X/\!\sim$ is denoted $X/A$: the subset $A$ is collapsed ("crushed") to a single point, deforming the rest of the space around that identification.

**Examples.**
- $X=[0,1]$, $A=\partial X=\{0,1\}$: $X/A \cong S^1$ (gluing the two endpoints of an interval produces a circle).
- $X=\bar B((0,0),1)\subset\mathbb R^2$ (closed disk), $A=\partial X$: $X/A \cong S^2$ (collapsing the boundary circle of a disk to a point produces a sphere).
- $X$ = the torus surface, $A$ = one of its meridian circles: $X/A$ is a "pinched torus."

### Gluing constructions build new spaces from old
More generally, an equivalence relation can identify different points of $X$ pairwise without crushing a whole subset to one point — this is the formal "cut-and-paste" construction. Gluing the two long edges of a rectangle produces a cylinder; if the two circular ends of that cylinder are then further glued, the result is a torus. Formally, on $[0,1]\times[0,1]$, declaring $(x_1,y_1)\sim(x_2,y_2)$ whenever ($x_1=x_2$ and $\{y_1,y_2\}=\{0,1\}$) or ($y_1=y_2$ and $\{x_1,x_2\}=\{0,1\}$) produces exactly four types of equivalence classes (corners identified together; opposite-edge points identified in pairs; interior points alone), and the resulting quotient space is the torus.

### Descending to the quotient
A continuous $f:X\to Y$ **descends to the quotient** if there is a continuous $\hat f : X/\!\sim\ \to Y$ with $\hat f = f\circ \pi$. This requires $f$ to be constant on each equivalence class — otherwise $\hat f$ would not even be well-defined as a function.

## Examples
$X=(\mathbb N, 2^{\mathbb N})$ with $x\sim y \iff$ ($2\mid x$ and $2\mid y$) or ($2\nmid x$ and $2\nmid y$); the quotient is the two-element set $\{[1],[2]\}$ with the discrete quotient topology, and $f(x) = x \bmod 2$ descends to the quotient since it is constant on each parity class.

## See also
[[Topological Space]], [[Homeomorphism]], [[Homotopy and Homotopy Equivalence]]
