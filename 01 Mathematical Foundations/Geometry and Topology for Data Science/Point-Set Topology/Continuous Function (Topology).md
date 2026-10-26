---
title: "Continuous Function (Topology)"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Point-Set Topology"
level: BSc
status: drafted
confidence: 0
tags: [topology, tda]
---
## Definition
Let $(X,\tau_X)$ and $(Y,\tau_Y)$ be [[Topological Space|topological spaces]]. A function $f:X\to Y$ is **continuous** if for every open set $V \in \tau_Y$, the preimage $f^{-1}(V)$ is open in $X$ (i.e. $f^{-1}(V) \in \tau_X$). This purely set-theoretic definition generalizes continuity beyond metric spaces, since it makes no reference to distance.

When $(X,d_X)$ and $(Y,d_Y)$ are metric spaces, this coincides with the calculus-style definition: $f$ is continuous at $x$ if for every $\varepsilon>0$ there is $\delta>0$ such that $d_X(x,y)<\delta \implies d_Y(f(x),f(y))<\varepsilon$; equivalently, $f^{-1}(B_{\varepsilon,d_Y}(f(x))) \supseteq B_{\delta,d_X}(x)$.

## Properties
### Continuity depends on both topologies
Whether $f$ is continuous depends on the topology chosen for *both* the domain and codomain — changing either one can turn a continuous function into a discontinuous one, and vice versa.

**Worked example.** Let $\mathbb N$ carry the topology $2\mathbb N$ (i.e., a topology whose only nontrivial building block is described via even numbers — treat this as a specific finite/countable example topology from the course) and let $2\mathbb N$ (the even positive integers) carry the trivial topology $\tau=\{\emptyset, 2\mathbb N\}$. The map $f(x)=2x$ is continuous $(\mathbb N, 2^{\mathbb N}) \to (2\mathbb N,\tau)$: $f^{-1}(\emptyset)=\emptyset$ is open, and $f^{-1}(2\mathbb N) = \mathbb N$ is open, so both preimages of open sets are open. But reversing which space gets the trivial topology, the *same formula* $f(x)=2x$ can fail to be continuous, because a set that was open in the fine topology need not have an open preimage under the identity-like map into the coarse one (a general symptom: continuity is not a property of the formula alone, but of the formula *together with* the two topologies).

### Composition and restriction preserve continuity
Continuous functions between topological spaces are also called **maps** or **morphisms** in the literature. Composing two continuous functions gives a continuous function, and restricting a continuous function to a subspace (with the subspace topology) remains continuous — properties used repeatedly, e.g. in the Continuity Theorems proofs in [[Compactness]] (see also [[Connectedness]]).

## Examples
$f:\mathbb R \to \mathbb R$, $f(x)=3x+1$ is continuous in the standard topology: for a basic open interval $(a,b)$, $f((a,b)) = (3a+1,3b+1)$, itself open, so $f^{-1}$ of any basic open set is open (using that $f$ is a bijection here and reasoning via $f^{-1}$ directly).

## See also
[[Topological Space]], [[Homeomorphism]], [[Embedding]], [[Metric Topology]]
