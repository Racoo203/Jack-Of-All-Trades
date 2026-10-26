---
subject: Geometry and Topology for Data Science
type: MOC
course_code: MA2007B
status: drafted
confidence: 0
tags:
  - moc
  - exam
  - topological-data-analysis
domain: Mathematical Foundations
---
## Concept narrative

The course builds Topological Data Analysis (TDA) from the ground up, in four movements. It starts from **geometry**: a [[Metric Space]] gives a dataset a notion of distance, and that distance shapes [[Balls and Spheres|balls, spheres]], and comparison tools between subsets ([[Hausdorff Distance]]) or between whole metric spaces ([[Gromov-Hausdorff Distance]]). It then strips the metric away to keep only the **topology**: a [[Topological Space]] is defined purely through open sets, metrics induce a [[Metric Topology]], and topologies can be compared as [[Coarser and Finer Topology|coarser or finer]]. [[Continuous Function (Topology)|Continuity]] and [[Homeomorphism|homeomorphisms]] let us decide when two spaces have "the same shape," and [[Closed Set and Closure|closedness]], [[Connectedness]], and [[Compactness]] are the three topological invariants used to tell spaces apart when no homeomorphism is in sight. Weaker equivalences — [[Embedding]], [[Isotopy]], and [[Homotopy and Homotopy Equivalence|homotopy]] — handle cases (the mug and the donut, a knot) where homeomorphism is too rigid or too hard to construct directly, and [[Quotient Space|quotient spaces]] show how "cutting and gluing" builds new shapes (torus, sphere, projective plane) out of old ones.

The second movement turns shapes into combinatorics. A [[Graph (Topology)|graph]] and, more generally, a [[Simplicial Complex]] built out of [[Simplex|simplices]] let us triangulate a space and read off invariants like the [[Triangulation and Euler Characteristic|Euler characteristic]] combinatorially, while [[Star and Link of a Simplex|stars and links]] describe local neighborhoods inside a complex.

The third movement is **homology**: the [[Chain Group|chain groups]] of a simplicial complex, linked by the [[Boundary Operator]], produce [[Homology Group|homology groups]] whose dimensions are the [[Betti Numbers]] — the formal count of connected components ($\beta_0$), independent 1-dimensional holes ($\beta_1$), voids ($\beta_2$), and so on. [[Singular Homology]] is the computational shortcut that lets a triangulation reuse vertices, keeping the chain complex small enough to compute by hand or in code (`mogutda`).

The final movement is **TDA proper**: turning a finite sample of points into a filtered simplicial complex and reading persistent topological features off it. [[Single Linkage Clustering and Dendrograms|Single linkage clustering]] recovers $\beta_0$ as a function of a distance threshold $R$; the general pattern is a [[Persistent Set]] — a family of objects connected by structure-preserving maps as a parameter grows. Covers of a metric space produce a [[Nerve Complex]], and the standard TDA covers — balls ([[Čech Complex]]), pairwise distance thresholds ([[Vietoris-Rips Complex]]), and Voronoi cells ([[Alpha Complex]]) — give the filtrations (`gudhi`, `scikit-tda`) whose persistent homology is the object of study. Time series are turned into point clouds via the [[Takens' Embedding Theorem|sliding-window / Takens embedding]] before this machinery is applied. Finally, the [[Mapper Algorithm]], driven by a choice of [[Mapper Filter Functions|filter function]] (density, eccentricity, PCA, UMAP), gives a graph-shaped compressed summary of a dataset's shape, used throughout Module 4's applications (protein structure, nanomaterials, epidemic spread, gravitational-wave detection, and the course's own football-analytics project).

A parallel, purely algebraic thread — [[Geometrically Independent vs Linearly Independent Vectors]] — underlies why simplices are well-defined objects, and a running appendix of [[Distance and Similarity Measures in Data Science|distance and similarity measures]] (cosine similarity, Hamming, Manhattan, Chebyshev, Minkowski, Jaccard, Haversine, Sørensen–Dice) supplies the metrics used to build these complexes on real, non-Euclidean data.

---

## Concept map

### Metric Spaces

- [[Metric Space]]: $(X,d)$, the three axioms, and examples (Euclidean, graph, Hausdorff-on-subsets metrics)
- [[Balls and Spheres]]: $B_r(x)$, $\bar B_r(x)$, $S_r(x)$, and how the metric shapes them (Euclidean disk vs. taxicab square)
- [[Equivalent Metrics]]: $c_1 d_1 \le d_2 \le c_2 d_1$, and why Euclidean/Manhattan/Chebyshev on $\mathbb{R}^n$ are equivalent
- [[Hausdorff Distance]]: $d_H(A,B) = \max\{\sup_a \inf_b d(a,b), \sup_b \inf_a d(a,b)\}$, and the $r$-neighborhood reformulation
- [[Gromov-Hausdorff Distance]]: comparing two metric spaces via isometric embeddings into a common ambient space $Z$

### Point-Set Topology

- [[Topological Space]]: $(X,\mathcal T)$ and the three topology axioms; trivial, discrete, finite-complement, product topologies
- [[Metric Topology]]: $\mathcal T_d$ induced by open balls; proof that it satisfies the topology axioms
- [[Coarser and Finer Topology]]: $\mathcal T_1 \subseteq \mathcal T_2$ and how equivalent metrics induce the same topology
- [[Continuous Function (Topology)]]: preimages of open sets are open; specializes to the $\varepsilon$-$\delta$ definition on metric spaces
- [[Homeomorphism]]: bijective, continuous, with continuous inverse; $X \cong Y$
- [[Closed Set and Closure]]: complement of an open set; $\bar A$ as intersection of closed supersets
- [[Connectedness]]: no open partition; path-connectedness implies connectedness; [[Connectedness#Connected Components|connected components]] as equivalence classes
- [[Compactness]]: every open cover has a finite subcover; on $\mathbb{R}^n$, compact $\iff$ closed and bounded
- [[Embedding]]: continuous injective map, becomes a homeomorphism onto its image
- [[Isotopy]]: a continuous family of homeomorphisms deforming $X$ into $Y$ (mug $\to$ donut, but a knot is not isotopic to the unknot)
- [[Homotopy and Homotopy Equivalence]]: $H:X\times[0,1]\to Y$; contractibility, deformation retracts
- [[Quotient Space]]: $X/\sim$, quotient topology, "crushing" a subset $A$ to a point ($X/A$), gluing constructions (torus, $S^2$)

### Simplicial Complexes

- [[Graph (Topology)]]: vertices/edges, paths, the graph topology and graph metric
- [[Simplex]]: $n$-simplex as $\{x \in \mathbb{R}^{n+1}: \sum x_j = 1, x_j \ge 0\}$; faces, vertices, edges
- [[Simplicial Complex]]: geometric vs. abstract definitions; $k$-skeleton $K^k$
- [[Triangulation and Euler Characteristic]]: $\chi(K) = \sum (-1)^i \#K^i$ as a topological invariant; singular vs. non-singular triangulations
- [[Star and Link of a Simplex]]: $St(\sigma)$, closed star $\overline{St}(\sigma)$, and $Lk(\sigma)$

### Homology

- [[Chain Group]]: $\mathcal C_m(K)$, formal sums of $m$-simplices over $\mathbb{Z}_2$
- [[Boundary Operator]]: $\partial_m : \mathcal C_m \to \mathcal C_{m-1}$, its matrix form, $\ker \partial_m$ and $\operatorname{Im}\partial_m$
- [[Homology Group]]: $H_n(K) = \ker \partial_n / \operatorname{Im}\partial_{n+1}$
- [[Betti Numbers]]: $\beta_n = \dim \ker\partial_n - \dim\operatorname{Im}\partial_{n+1}$; interpretation as components/tunnels/voids
- [[Singular Homology]]: allowing degenerate simplices to shrink the triangulation used for computation (`mogutda`)

### Topological Data Analysis

- [[Single Linkage Clustering and Dendrograms]]: $x \sim_R x'$ for $d(x,x')\le R$; the dendrogram as a combinatorial encoding of $\beta_0(R)$
- [[Persistent Set]]: $\{X_R\}_{R\ge0}$ with structure maps $X_R \to X_{R'}$ for $R\le R'$
- [[Nerve Complex]]: $N(\mathcal U)$ from a cover $\mathcal U$; Nerve Theorem (homotopy equivalence when intersections are contractible)
- [[Čech Complex]]: nerve of the cover by balls $\{B_r(p)\}_{p\in P}$
- [[Vietoris-Rips Complex]]: $\sigma \in VR_r(P) \iff d(p,q)\le 2r\ \forall p,q\in\sigma$; determined by its 1-skeleton
- [[Alpha Complex]]: nerve of the Voronoi-restricted balls $D_p^\alpha$; a computationally cheap subcomplex of Vietoris-Rips
- [[Takens' Embedding Theorem]]: sliding-window embedding $\Phi_{(\phi,y)}: M \to \mathbb{R}^{2m+1}$ of a time series

### Mapper and Applications

- [[Mapper Algorithm]]: filter $f:X\to\mathbb{R}^d$, cover with overlap, cluster preimages, build the nerve graph
- [[Mapper Filter Functions]]: density (KDE / neighbor count), eccentricity $E_p(x)$, PCA, UMAP
- [[Geometrically Independent vs Linearly Independent Vectors]]: $v_0,\dots,v_m$ geom. independent $\iff$ $v_1-v_0,\dots,v_m-v_0$ lin. independent — the fact that makes simplices well-defined
- [[Distance and Similarity Measures in Data Science]]: cosine similarity, Hamming, Manhattan, Chebyshev, Minkowski, Jaccard, Haversine, Sørensen–Dice

---

## Key dependency chains

```
Metric Space ──> Metric Topology ──> Topological Space ──> Continuity/Homeomorphism
                                          │
                                          ├─> Closedness / Connectedness / Compactness (invariants)
                                          └─> Embedding / Isotopy / Homotopy ──> Quotient Space

Simplex ──> Simplicial Complex ──> Triangulation (Euler characteristic)
                     │
                     └─> Chain Group ──Boundary Operator──> Homology Group ──> Betti Numbers
                                                                    │
                                                             Singular Homology (computation)

Finite metric space (point cloud)
        │
        ├─> Single Linkage Clustering ──> Dendrogram ──> Persistent Set (β₀ as R grows)
        │
        └─> Cover of the space ──> Nerve Complex ──┬─> Čech Complex
                                                     ├─> Vietoris-Rips Complex
                                                     └─> Alpha Complex
                                                              │
                                                     Filtration ──> Persistent Homology / Betti numbers over r

Time series ──Takens' Embedding──> point cloud in R^(2m+1) ──> (feed into TDA pipeline above)

Point cloud + filter function (density/eccentricity/PCA/UMAP) ──Mapper Algorithm──> Mapper graph
```

---

## Exam focus

### High priority

- **Metric/topology axiom-checking**: verifying the three metric axioms or the three topology axioms for a concrete $(X,d)$ or $(X,\mathcal T)$, and computing balls/spheres for non-Euclidean metrics ($\ell_1$, $\ell_\infty$, discrete).
- **Continuity via preimages**: showing a function is/isn't continuous by testing $f^{-1}(V)$ against $\tau_X$ for specific finite topologies (as in Examples 24.2–24.3 of the lecture notes).
- **Topological invariants as inequivalence proofs**: using connectedness ($\mathbb R \not\cong \mathbb R\setminus\{0\}$) or compactness ($[0,1]\not\cong(0,1)$) to show two spaces are *not* homeomorphic — this is the standard exam pattern (Theorems 33.1, 33.5 and their corollaries).
- **Simplicial-complex bookkeeping**: building $K$ from a picture or a list of simplices, computing $\chi(K)$, and identifying the underlying space from $\chi$.
- **Homology by hand**: computing chain groups, writing the boundary-operator matrix, doing Gauss-Jordan over $\mathbb Z_2$ to get ranks, and reading off $\beta_0,\beta_1$ (the fully worked triangle/cylinder examples in the lecture notes are the template).
- **Building Čech / Vietoris-Rips complexes** from a small point set at a given radius $r$, and tracking how the complex changes across a filtration (persistence, informally).
- **Single linkage clustering ↔ dendrogram ↔ $\beta_0(R)$**: reading a distance matrix into clusters at a given threshold and drawing/reading the dendrogram.
- **Mapper by hand** on a tiny dataset: applying a filter, building the cover, clustering preimages, and drawing the resulting graph.

### Common question types

- "Show that $d$ satisfies the triangle inequality / is not a metric because it fails axiom X."
- "Is $\tau$ a topology on $X$? Prove all three properties or give a counterexample."
- "Prove $f:X\to Y$ is/isn't continuous between these two (finite) topological spaces."
- "Use [connectedness/compactness] to show that [two spaces] are not homeomorphic."
- "Compute the Euler characteristic of this triangulation and identify the surface."
- "Compute the boundary-operator matrices and the Betti numbers of this simplicial complex."
- "Given this distance matrix, find the single-linkage clusters at $R = \ldots$ and draw the dendrogram."
- "Construct the Čech (or Vietoris-Rips) complex of these four points at radius $r=\ldots$."
- "Explain Takens' theorem and identify the embedding dimension / delay / stride in this `giotto-tda` call."

---

## Open questions

- _How exactly does the professor want the Gromov-Hausdorff distance computed for the graded homework — via the explicit distance-matrix-over-$Z$ construction, or is the closed-form infimum enough?_
- _Is the appendix list of Data Science metrics (cosine, Hamming, Manhattan, Chebyshev, Minkowski, Jaccard, Haversine, Sørensen–Dice) examined as proofs-that-it's-a-metric, or only as applied computations (per Actividad 1.2)?_
- _Which persistence-diagram distance is used in this course to compare diagrams — bottleneck, Wasserstein, or the Gromov-Hausdorff distance mentioned in Lecture 5? The lecture notes mention both without settling on one._
- _Module 2's homology-persistence content (persistence diagrams, barcodes, stability theorem, persistence images) is described in the syllabus but not yet covered in the lecture notes I've seen — flag as a gap once those slides arrive._
