---
title: "Distance and Similarity Measures in Data Science"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Metric Spaces"
level: BSc
status: seeding
confidence: 0
tags: [metric-spaces, tda, seeding]
---
## Definition
This note collects the applied distance and similarity measures listed in the course appendix (Actividad 1.2), beyond the Euclidean metric already covered in [[Metric Space]]. For $x=(x_1,\dots,x_n), y=(y_1,\dots,y_n)$:

- **Cosine similarity**: $\cos(\theta) = \dfrac{x\cdot y}{\lVert x\rVert \lVert y\rVert}$, the cosine of the angle between $x$ and $y$ as vectors; often converted to the *cosine distance* $1-\cos(\theta)$, which is **not** a true metric (it can fail the triangle inequality and identity of indiscernibles for the zero vector) but is used pervasively for text/embedding similarity because it ignores magnitude and captures orientation.
- **Hamming distance**: for equal-length sequences (often binary strings), the number of positions at which the two sequences differ.
- **Manhattan ($\ell_1$) distance**: $d_1(x,y) = \sum_{i=1}^n |x_i-y_i|$.
- **Chebyshev ($\ell_\infty$) distance**: $d_\infty(x,y) = \max_i |x_i - y_i|$.
- **Minkowski ($\ell_p$) distance**: $d_p(x,y) = \left(\sum_{i=1}^n |x_i-y_i|^p\right)^{1/p}$, a family generalizing Manhattan ($p=1$), Euclidean ($p=2$), and (in the limit $p\to\infty$) Chebyshev.
- **Jaccard index**: for finite sets $A,B$, $J(A,B) = \dfrac{|A\cap B|}{|A\cup B|}$, a similarity in $[0,1]$; $1-J(A,B)$ gives the Jaccard distance.
- **Haversine distance**: the great-circle distance between two points on a sphere given their latitude/longitude, used for geographic data where Euclidean distance would ignore the Earth's curvature.
- **Sørensen–Dice index**: for finite sets $A,B$, $DSC(A,B) = \dfrac{2|A\cap B|}{|A|+|B|}$, a similarity closely related to but distinct from the Jaccard index (it weights the intersection more heavily).

<!-- UNVERIFIED: check against course slides/homework (Actividad 1.2) — the homework specifically asks to (a) verify which of these are metrics in the formal sense of Definition (see [[Metric Space]]), (b) identify when each is appropriate, and (c) compute unit/radius-2/radius-3 balls for a chosen dataset centered at a random observation. This note gives the standard formulas but has not yet been checked against the professor's specific notation or against which of these the homework concludes are/aren't true metrics. -->

## Properties
### Which of these are true metrics
The Manhattan, Chebyshev, and Minkowski ($p\ge1$) distances satisfy all three [[Metric Space|metric axioms]] on $\mathbb R^n$ (they are norms, and every norm induces a metric via $d(x,y)=\lVert x-y\rVert$). The Hamming distance is a metric on the space of equal-length sequences. The Jaccard *distance* ($1-J$) is a true metric on finite sets. The cosine *distance*, by contrast, generally fails to be a metric (it can be zero for distinct non-parallel vectors is false, but it fails the triangle inequality in general and is only defined up to scaling, i.e. it does not distinguish $x$ from $\lambda x$ for $\lambda>0$, so it fails the identity-of-indiscernibles axiom against the standard definition of a metric).

### Choice of metric depends on data type
Binary/categorical data typically favors Hamming or Jaccard/Sørensen–Dice; text and embedding vectors favor cosine similarity (ignoring magnitude); grid-like or high-dimensional numeric data favor Manhattan or Chebyshev depending on whether "any large single-coordinate difference" or "total accumulated difference" should dominate; geographic coordinates require Haversine rather than Euclidean distance.

## Examples
For binary vectors $x=(1,0,1,1)$, $y=(1,1,0,1)$: Hamming distance is $2$ (positions $2$ and $3$ differ); treating them as sets $A=\{1,3,4\}$, $B=\{1,2,4\}$ (indices of the $1$s), $J(A,B) = |\{1,4\}|/|\{1,2,3,4\}| = 2/4 = 0.5$, and $DSC(A,B) = 2\cdot2/(3+3) = 2/3$.

## See also
[[Metric Space]], [[Balls and Spheres]], [[Mapper Filter Functions]]
