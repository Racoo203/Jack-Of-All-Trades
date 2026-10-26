---
title: "Chain Group"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Homology"
level: BSc
status: drafted
confidence: 0
tags: [tda, homology]
---
## Definition
Let $K$ be a [[Simplicial Complex]]. An **$m$-chain** $c$ in $K$ is a formal sum of $m$-simplices of $K$,
$$
c = \sum_{\sigma \in K} a_\sigma\, \sigma, \qquad a_\sigma \in \mathbb Z_2,
$$
where the coefficients are taken over the field $\mathbb Z_2 = \{0,1\}$ (this course works with $\mathbb Z_2$ coefficients throughout, rather than $\mathbb Z$). The set of all $m$-chains in $K$ is denoted $\mathcal C_m(K)$.

## Properties
### $\mathcal C_m(K)$ is a vector space over $\mathbb Z_2$
Chain addition is performed coefficient-wise, with $1+1=0$ in $\mathbb Z_2$ (so a simplex appearing twice in a sum cancels out). This addition gives $\mathcal C_m(K)$ the structure of a group — indeed a vector space over $\mathbb Z_2$ — whose identity is the zero chain $0=\sum_\sigma 0\cdot\sigma$. $\mathcal C_m(K)$ is called the **$m$-th chain group**.

### Interpretation
The coefficient $a_\sigma \in \{0,1\}$ can be read as "the chain does/doesn't pass through simplex $\sigma$"; a chain is essentially a subset of the $m$-simplices of $K$, with addition corresponding to symmetric difference of subsets.

## Examples
Let $K=\{a,b,c,ab,bc,ca\}$ (triangle outline). Then
$$
\mathcal C_0(K) = \{0,a,b,c,a{+}b,a{+}c,b{+}c,a{+}b{+}c\}, \qquad
\mathcal C_1(K) = \{0,ab,bc,ca,ab{+}bc,bc{+}ca,ca{+}ab,ab{+}bc{+}ca\},
$$
and $\mathcal C_m(K)=\{0\}$ for $m\ge2$ (since $K$ has no $2$-simplices). Note $|\mathcal C_0(K)|=2^3=8$ and $|\mathcal C_1(K)|=2^3=8$, consistent with $\mathcal C_m(K) \cong \mathbb Z_2^{\#K^m}$.

## See also
[[Simplicial Complex]], [[Boundary Operator]], [[Homology Group]]
