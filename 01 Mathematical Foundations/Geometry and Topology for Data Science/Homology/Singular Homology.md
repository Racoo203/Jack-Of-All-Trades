---
title: "Singular Homology"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Homology"
level: BSc
status: seeding
confidence: 0
tags: [tda, homology, seeding]
---
## Definition
A **singular simplex** is a simplex that need not be a genuine geometric realization: it may be degenerate, admitting an edge whose two endpoints coincide, or a triangle with only one or two *distinct* edges. A **singular simplicial complex** is a complex built from such (possibly degenerate) simplices, in contrast to the non-degenerate simplices required by an ordinary (non-singular) [[Simplicial Complex]].

<!-- UNVERIFIED: check against course slides — the course's use of "singular homology" here (via degenerate simplicial triangulations, computed with the `mogutda` package) is a simplified, computational stand-in for the standard singular homology theory of algebraic topology (built from continuous maps of the standard simplex), which the module description explicitly separates from "simplicial homology" proper. Confirm which definition the professor expects on an exam. -->

## Properties
### Why use singular (degenerate) triangulations
Computing [[Betti Numbers]] by hand from a non-singular triangulation can require a large number of simplices. Allowing degenerate simplices lets the same space be triangulated with far fewer of them, at the cost of some extra bookkeeping (tracking that formally-identical-looking simplices, e.g. multiple copies of an edge $ab$, must be treated as distinct basis elements of the chain groups).

**Comparative simplex counts (cylinder).** A non-singular triangulation of the cylinder needs $6$ vertices and $15$ simplices in total (six $0$-simplices, various $1$- and $2$-simplices); the singular triangulation $K=\{a,b,aa,ab,bb,aab,abb\}$ captures the same space with only $2$ vertices, at the cost of degenerate simplices like $aa$, $bb$.

**Comparative simplex counts (torus).** A non-singular triangulation of the torus needs $14$ triangles; a singular one can be written with a single vertex and a single filled $2$-simplex, $K=\{a,aa,aaa\}$, provided the computation correctly treats the "one vertex" as several formally-identical copies for chain-group purposes.

### Computing Betti numbers on a singular triangulation
**Worked example (cylinder).** $\beta_0(\text{cylinder})=1$, $\beta_1(\text{cylinder})=2$ are known (one component, two independent boundary circles). Using $K=\{a,b,aa,ab,bb,aab,abb\}$, and relabeling the three occurrences of the "$ab$"-type edge as distinct basis elements $u,t,v,w$ where needed, direct computation of $\partial_1,\partial_2$ and their ranks over $\mathbb Z_2$ recovers $\beta_0=1$, and (per the source computation) $\beta_1=1$ for that specific singular complex — the discrepancy with the textbook value $\beta_1=2$ in the lecture notes' own worked example is exactly the kind of subtlety singular triangulations introduce and that this note flags as UNVERIFIED above.

### Computational tooling: `mogutda`
```python
pip install mogutda
```
```python
from mogutda import SimplicialComplex
cycle1 = [(1,2),(2,3),(3,1)]
Sc = SimplicialComplex(simplices=cycle1)
Sc.draw()
for i in range(0,3):
    print(Sc.betti_numbers(i))
```
`mogutda` builds a simplicial complex from a list of maximal faces (as tuples of vertex labels) and exposes `.betti_numbers(i)` to compute $\beta_i$ directly, without manually assembling boundary-operator matrices.

## See also
[[Simplicial Complex]], [[Boundary Operator]], [[Betti Numbers]], [[Triangulation and Euler Characteristic]]
