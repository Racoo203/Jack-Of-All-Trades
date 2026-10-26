---
title: "Boundary Operator"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Homology"
level: BSc
status: drafted
confidence: 0
tags: [tda, homology]
---
## Definition
Let $K$ be a [[Simplicial Complex]]. The **boundary operator** $\partial_m : \mathcal C_m(K) \to \mathcal C_{m-1}(K)$ (see [[Chain Group]]) is the linear map defined on a single $m$-simplex $\sigma$ by
$$
\partial_m(\sigma) = \sum_{i=0}^m \sigma^{[i]},
$$
where $\sigma^{[i]}$ is the $i$-th $(m-1)$-face of $\sigma$, and extended linearly (over $\mathbb Z_2$) to general chains. By convention $\partial_0 c = 0$ for every $0$-chain $c$.

## Properties
### Computing on a simplex and a chain
For a $2$-simplex $\sigma=\{v_1,v_2,v_3\}$, $\partial_1\sigma = \{v_1,v_2\}+\{v_2,v_3\}+\{v_3,v_1\}$ — geometrically, the boundary of a filled triangle is its perimeter. For a $2$-chain $k=\{v_1,v_2,v_3\}+\{v_2,v_4,v_3\}$ (two triangles glued along edge $\{v_2,v_3\}$), applying $\partial_1$ to each triangle and adding over $\mathbb Z_2$ cancels the shared edge $\{v_2,v_3\}$ (it appears twice), leaving only the outer boundary of the resulting square:
$$
\partial_1 k = \{v_1,v_2\}+\{v_3,v_1\}+\{v_2,v_4\}+\{v_4,v_3\}.
$$

### Kernel and image, and their matrix form
Since $\mathcal C_m(K)$ is a vector space and $\partial_m$ is linear, it can be represented as a matrix once a basis is fixed — the natural basis of $\mathcal C_k(K)$ is the set of $k$-simplices of $K$. The **kernel** $\ker(\partial_m) = \{c \in \mathcal C_m(K) : \partial_m c = 0\}$ is the space of $m$-chains that are "closed" (have no boundary); the **image** $\operatorname{Im}(\partial_m) = \{c\in\mathcal C_{m-1}(K) : c=\partial_m d\text{ for some }d\}$ is the space of $(m-1)$-chains that arise as a boundary. Each column of the matrix of $\partial_m$ is the image, under $\partial_m$, of one basis element (one $m$-simplex).

**Worked example.** For $K=\{a,b,c,ab,bc,ca\}$: since $\partial_1(ab)=a+b$, $\partial_1(bc)=b+c$, $\partial_1(ca)=c+a$, the matrix of $\partial_1$ (columns = $ab,bc,ca$; rows = $a,b,c$) is
$$
\begin{pmatrix}1&0&1\\1&1&0\\0&1&1\end{pmatrix}.
$$
Here $\ker(\partial_0) = \mathcal C_0(K)$ trivially split as computed elsewhere, and $\ker(\partial_1) = \{0, ab+bc+ca\}$, $\operatorname{Im}(\partial_1) = \{0,a,b,c\}$ (rank $2$ over $\mathbb Z_2$, since only $2$ of the $3$ columns are linearly independent).

## Examples
For a triangle with its interior filled in, $K=\{a,b,c,ab,bc,ca,abc\}$, the matrix of $\partial_2$ (mapping the single $2$-simplex $abc$ to the three edges) is the column vector $(1,1,1)^T$, since $\partial_2(abc)=ab+bc+ca$.

## See also
[[Chain Group]], [[Homology Group]], [[Betti Numbers]]
