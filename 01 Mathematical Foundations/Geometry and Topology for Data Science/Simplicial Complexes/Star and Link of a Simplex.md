---
title: "Star and Link of a Simplex"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Simplicial Complexes"
level: BSc
status: drafted
confidence: 0
tags: [tda, simplicial-complexes]
---
## Definition
Let $K$ be a [[Simplicial Complex]] and $\sigma \in K$. The **star** of $\sigma$ is
$$
St(\sigma) = \{\omega \in K : \sigma \subset \omega\},
$$
the set of all simplices having $\sigma$ as a face. The **closed star** $\overline{St}(\sigma)$ is
$$
\overline{St}(\sigma) = \bigcup_{\omega \in St(\sigma)} \big(\{\omega\}\cup\{\sigma'\in K:\sigma'\subset\omega\}\big),
$$
i.e. $St(\sigma)$ together with every face of every simplex in $St(\sigma)$ — the smallest simplicial complex inside $K$ that contains $St(\sigma)$. The **link** of $\sigma$ is
$$
Lk(\sigma) = \{\omega \in St(\sigma) : \sigma\cap\omega = \emptyset\}.
$$

## Properties
### Star is generally not a simplicial complex
$St(\sigma)$ can fail to contain all faces of its own elements (a simplex $\omega \supset \sigma$ may be in $St(\sigma)$ while some other face of $\omega$, not containing $\sigma$, is not), so $St(\sigma)$ need not itself satisfy the closure-under-faces axiom of a simplicial complex. $\overline{St}(\sigma)$ fixes this by explicitly adding back every missing face.

### Local-neighborhood intuition
Thinking of $\sigma$ as a point (or small piece) of the complex, $St(\sigma)$ behaves like an open neighborhood of $\sigma$ inside $K$, and $Lk(\sigma)$ behaves like the boundary of that neighborhood — the "frontier" one crosses to leave the star. Consequently $\overline{St}(\sigma)$, being the union of the star and its boundary, is the closed neighborhood.

## Examples
For the two-dimensional simplicial complex on vertices $\{a,b,c,d,e,f\}$ shown in the lecture notes (with $a$ adjacent to $b,c,d,e,f$ and a filled triangle $\{a,b,c\}$):
$$
St(a) = \{\{a,f\},\{a,d\},\{a,e\},\{a,c\},\{a,b\},\{a,b,c\}\},
$$
$$
Lk(a) = \{b,d,c,e,f,\{d,b\},\{e,c\},\{b,c\}\}.
$$

## See also
[[Simplicial Complex]], [[Simplex]]
