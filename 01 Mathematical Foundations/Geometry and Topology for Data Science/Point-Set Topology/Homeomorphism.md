---
title: "Homeomorphism"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Point-Set Topology"
level: BSc
status: drafted
confidence: 0
tags: [topology, tda]
---
## Definition
Let $(X,\tau_X)$, $(Y,\tau_Y)$ be [[Topological Space|topological spaces]]. A function $f:X\to Y$ is a **homeomorphism** if $f$ is bijective, [[Continuous Function (Topology)|continuous]], and its inverse $f^{-1}:Y\to X$ is also continuous. If such an $f$ exists, $X$ and $Y$ are **homeomorphic**, written $X \cong Y$. Homeomorphism is the natural equivalence relation on topological spaces: homeomorphic spaces are indistinguishable as topological spaces.

## Properties
### Homeomorphism preserves all topological properties
Any property of $X$ defined purely in terms of its topology (open sets, closedness, connectedness, compactness, etc.) is automatically shared by every space homeomorphic to $X$. This is what makes properties like [[Closed Set and Closure|closedness]], [[Connectedness]], and [[Compactness]] useful **invariants**: if two spaces differ in one of these properties, they cannot be homeomorphic (see the Continuity Theorems in [[Compactness]] for the exact theorems used this way).

### Constructing an explicit homeomorphism
To show $X\cong Y$, exhibit $f$ and check bijectivity plus continuity in both directions.

**Worked example.** $\mathbb R$ (Euclidean topology) and $(0,\infty)$ (subspace topology) are homeomorphic via $f(x)=e^x$:
- *Injective*: if $f(x)=f(y)$ then $e^x=e^y \implies e^{x-y}=1 \implies x=y$.
- *Surjective*: given $y\in(0,\infty)$, $x=\ln(y)\in\mathbb R$ satisfies $f(x)=e^{\ln y}=y$.
- *Continuity of $f$*: $f((a,b)) = (e^a,e^b)$, open in $(0,\infty)$.
- *Continuity of $f^{-1}=\ln$*: similarly maps basic open sets to open sets.

Hence $f$ is a homeomorphism.

## Examples
- $(\mathbb N, 2^{\mathbb N})$ and $(2\mathbb N, 2^{2\mathbb N})$ (both discrete topologies) are homeomorphic via $f(n)=2n$, since both $f$ and $f^{-1}(m)=m/2$ are continuous in the discrete topology (every function out of a discrete space is continuous).
- Homeomorphism is strictly stronger than [[Homotopy and Homotopy Equivalence|homotopy equivalence]] and than sharing the same [[Betti Numbers]]: two spaces can agree on every homotopy invariant without an explicit homeomorphism ever being constructible in practice, which motivates the weaker tools [[Embedding]] and [[Isotopy]].

## See also
[[Continuous Function (Topology)]], [[Topological Space]], [[Closed Set and Closure]], [[Connectedness]], [[Compactness]]
