---
title: "Embedding"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Point-Set Topology"
level: BSc
status: drafted
confidence: 0
tags: [topology, tda]
---
## Definition
A function $g:(X,\tau_X) \to (Y,\tau_Y)$ is an **embedding** if it is a continuous injective function. An embedding need not be surjective, so it is generally weaker than a [[Homeomorphism]]; however, restricting the codomain to the image $g(X)$ (with the subspace topology) turns $g$ into a homeomorphism $X \cong g(X)$.

## Properties
### Embeddings let a space be seen as a subspace of another
Embeddings formalize the idea "$X$ sits inside $Y$ without distortion of its topology," even when $X$ and $Y$ are not homeomorphic to each other as a whole. This is weaker — and easier to construct — than a global homeomorphism between $X$ and $Y$.

### Injectivity alone is not enough; continuity alone is not enough
$f:[0,2\pi)\to\mathbb R^2$, $\theta \mapsto(\cos\theta,\sin\theta)$ is bijective onto the unit circle but is **not** an embedding: it is not continuous as a map into $\mathbb R^2$ at $\theta=0$, because points near $2\pi$ map close to $(1,0)=f(0)$ without $\theta$ itself being close to $0$ in $[0,2\pi)$.

### Standard families of embeddings
- **Inclusion**: if $A \subset X$ is a subspace, the inclusion $i:A \to X$ is always an embedding.
- **Product-space slices**: for $Z = X\times Y$ with the product topology, $f(x) = (x,y_0)$ and $g(y)=(x_0,y)$ (fixed $y_0\in Y$, $x_0\in X$) are embeddings of $X$ and $Y$ into $Z$.
- **Graphs of continuous functions**: if $h:\mathbb R \to \mathbb R$ is continuous, $f(x) = (x,h(x))$ is an embedding of $\mathbb R$ into $\mathbb R^2$, even when $h$ itself (e.g. $h(x)=\sin(x)$ or $h(x)=x^2$) is not injective and hence not an embedding on its own.

## Examples
The knot in [[Isotopy]] and the delay-coordinate reconstruction of a dynamical system in the [[Takens' Embedding Theorem]] are both embeddings in this sense: injective, continuous maps that let a lower-information object ($S^1$, or a time series) be studied as a subspace of a higher-dimensional space ($\mathbb R^3$, or $\mathbb R^{2m+1}$) without losing topological information.

## See also
[[Continuous Function (Topology)]], [[Homeomorphism]], [[Isotopy]], [[Takens' Embedding Theorem]]
