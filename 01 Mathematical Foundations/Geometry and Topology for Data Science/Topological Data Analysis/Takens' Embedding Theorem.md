---
title: "Takens' Embedding Theorem"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Topological Data Analysis"
level: BSc
status: seeding
confidence: 0
tags: [tda, seeding]
---
## Definition
The **sliding-window method** turns a time series into a point cloud (in some Euclidean space, usually high-dimensional) by taking overlapping windows of the signal, encoding the original series' information topologically. Its theoretical justification is Takens' theorem, originally developed for dynamical systems analysis:

**Theorem (Takens, 1981).** Let $M$ be a compact manifold of dimension $m$, $\phi:M\to M$ a smooth diffeomorphism, and $y:M\to\mathbb R$ a smooth function. Then the map
$$
\Phi_{(\phi,y)} : M \to \mathbb R^{2m+1}, \qquad \Phi_{(\phi,y)}(x) = \big(y(x),\, y(\phi(x)),\, \dots,\, y(\phi^{2m}(x))\big)
$$
is a topological [[Embedding]] of $M$ into $\mathbb R^{2m+1}$.

Such an embedding is also called a **time-delay embedding**: it consists of a fixed-size window sliding across the signal, where each shift of the window produces one point in the target Euclidean space.

## Properties
### What the embedding preserves
Because $\Phi_{(\phi,y)}$ is an embedding (continuous and injective, becoming a homeomorphism onto its image), the reconstructed point cloud in $\mathbb R^{2m+1}$ retains the full topology of the original dynamical system's attractor $M$, even though only a single scalar observable $y$ of the system was recorded. This is what allows the dynamics of a system to be reconstructed from just one measured variable.

### Practical parameters
Three parameters govern the practical (`giotto-tda`) version of the embedding: the **embedding dimension** $d$ (analogous to $m$ in the theorem, though used more loosely as a tunable hyperparameter rather than derived exactly from $2m+1$), the **time delay** $\tau$ (the lag between consecutive coordinates of a window, rather than literally iterating $\phi$), and the **stride** $s$ (how far the window shifts between consecutive samples).

<!-- UNVERIFIED: check against course slides/homework (Actividad 1.3) — the exact relationship between the theorem's $(\phi, y, m)$ and giotto-tda's `SingleTakensEmbedding` parameters (embedding dimension, time delay, stride), and the recommended methods for choosing the embedding dimension and delay optimally (e.g. false-nearest-neighbors, mutual information), are assigned as open research questions in the homework rather than given directly in the lecture notes I've seen. Fill in once that research is done. -->

## Examples
The course's own homework (Actividad 1.3) applies `gtda.time_series.SingleTakensEmbedding` with embedding dimension $d=3$, time delay $\tau=7$, and stride $s=9$ to a mix of periodic and non-periodic functions $f:\mathbb R\to\mathbb R$, then visualizes the resulting embedded point cloud — periodic signals are expected to trace out closed loops (detectable via a non-trivial $\beta_1$, see [[Betti Numbers]]) while non-periodic ones do not. This feeds directly into the course's gravitational-wave-detection application, where a time series (the detector signal) is turned into a point cloud via this embedding before topological features are extracted with the rest of the TDA pipeline.

## See also
[[Embedding]], [[Betti Numbers]], [[Mapper Algorithm]]
