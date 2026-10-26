---
title: "Definiteness of Quadratic Forms"
domain: "Optimization & Control"
course: "Non-linear Optimization"
unit: "NLP Foundations"
level: BSc
status: drafted
confidence: 0
tags: [linear-algebra, nonlinear-optimization, ma2008b]
---
## Definition
A **quadratic form** is a scalar field $q:\mathbb R^n\to\mathbb R$ of the form
$$q(x)=\sum_{i=1}^n\sum_{j=1}^na_{ij}x_ix_j=x^TAx,$$
with no linear or constant terms. Since only $a_{ij}+a_{ji}$ matters, many matrices represent the same form, but there is a **unique symmetric** one, $D=\frac12(A+A^T)$, i.e. $d_{ij}=d_{ji}=\frac{a_{ij}+a_{ji}}{2}$. For example $q=ax_1^2+bx_1x_2+cx_2^2=x^T\begin{pmatrix}a&b/2\\b/2&c\end{pmatrix}x$.

$q$ (and $D$) is
- **positive definite** if $q(x)>0$ for all $x\ne0$;
- **positive semidefinite** if $q(x)\ge0$ for all $x$ (and not positive definite);
- **negative definite / semidefinite** analogously with $<0$ / $\le0$;
- **indefinite** if $q(x_1)>0$ and $q(x_2)<0$ for some $x_1,x_2$.

## Properties
### Eigenvalue test
Let $\lambda_1,\dots,\lambda_n$ be the [[Eigenvalues and Eigenvectors|eigenvalues]] of the symmetric $D$. Then $q$ is PD ⇔ all $\lambda_i>0$; ND ⇔ all $\lambda_i<0$; PSD ⇔ all $\lambda_i\ge0$ with some $=0$; NSD ⇔ all $\le0$ with some $=0$; indefinite ⇔ some $\lambda_i>0$ and some $\lambda_j<0$.

*Proof.* By the [[Spectral Theorem]], $D=Q\Lambda Q^T$ with $Q$ orthogonal. Put $y=Q^Tx$ (a bijection, $y\ne0\iff x\ne0$):
$$q(x)=x^TQ\Lambda Q^Tx=y^T\Lambda y=\sum_i\lambda_iy_i^2.$$
This is positive for every $y\ne0$ iff every $\lambda_i>0$ (choose $y=e_i$ for necessity). The other cases follow the same way. ∎

### Principal-minor (Sylvester) test
$D$ is PD ⇔ all leading principal minors $\Delta_k=\det(D_{1..k,1..k})>0$. $D$ is ND ⇔ $(-1)^k\Delta_k>0$ (signs alternate, starting negative). For $2\times2$, $D=\begin{pmatrix}a&b\\b&c\end{pmatrix}$: PD ⇔ $a>0$ and $ac-b^2>0$.
*$2\times2$ proof by completing the square* ($a\ne0$):
$$q=ax_1^2+2bx_1x_2+cx_2^2=a\Big(x_1+\frac bax_2\Big)^2+\frac{ac-b^2}{a}x_2^2,$$
positive for all $x\ne0$ iff $a>0$ and $ac-b^2>0$.
For **semi**definiteness *all* principal minors (not only the leading ones) must be $\ge0$; Tema 7's shortcut "$f_{xx}\ge0$ and $\det H\ge0$" is valid for $2\times2$ only if one also checks $f_{yy}\ge0$ (e.g. $\begin{pmatrix}0&0\\0&-1\end{pmatrix}$ passes the first two but is NSD).

### Useful facts (slides)
If $D$ is symmetric PD then $D^{-1}$ exists and is PD, and $ADA^T$ is PSD for any $m\times n$ matrix $A$ ($y^TADA^Ty=(A^Ty)^TD(A^Ty)\ge0$). A PD matrix admits a **Cholesky factorization** $D=LL^T$ with $L$ lower triangular with positive diagonal — attempting it is a practical PD test (see [[Newton's Method (Optimization)]]).

### Role in optimization
The Hessian's definiteness classifies critical points ([[Optimality Conditions (Unconstrained)]]) and decides convexity ([[Convex Function]]).

## Examples
- $q=x_1^2+10x_2^2$: PD. $q=-x_1^2-10x_2^2$: ND.
- $q=7x_1^2+4x_1x_2+8x_2^2$: $D=\begin{pmatrix}7&2\\2&8\end{pmatrix}$, $\Delta_1=7$, $\Delta_2=52$ → PD.
- $A=\begin{pmatrix}2&-2\\8&-1\end{pmatrix}$ gives $q=2x_1^2+6x_1x_2-x_2^2$; symmetric $D=\begin{pmatrix}2&3\\3&-1\end{pmatrix}$, $\det=-11<0$ → indefinite.

## See also
[[Convex Function]], [[Optimality Conditions (Unconstrained)]], [[Hessian Matrix]], [[Eigenvalues and Eigenvectors]]
