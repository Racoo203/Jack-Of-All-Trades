---
title: "Matrix Algebra Foundations for Multivariate Analysis"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Appendix"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, matrix-algebra, foundations]
---
## Definition
Multivariate analysis represents a sample of $n$ individuals measured on $p$ variables as the [[Data Matrix, Mean Vector, and Covariance Matrix|data matrix]] $\mathbf{X}_{(n\times p)}$, and almost every technique in the course reduces to an operation on this matrix or on its derived covariance matrix $S$. This note collects the algebraic machinery used without re-derivation everywhere else in the vault: transpose, inverse, determinant, quadratic forms, eigenvalues/eigenvectors, and positive-definiteness.

**Transpose.** For $\mathbf{A}_{(m\times n)}$, the transpose $\mathbf{A}'$ (or $\mathbf{A}^T$) is $(n\times m)$ with $(\mathbf{A}')_{ij}=A_{ji}$. Properties: $(\mathbf{A}')'=\mathbf{A}$, $(\mathbf{A}+\mathbf{B})'=\mathbf{A}'+\mathbf{B}'$, $(\mathbf{AB})'=\mathbf{B}'\mathbf{A}'$. A matrix is **symmetric** if $\mathbf{A}=\mathbf{A}'$ — every covariance and correlation matrix in this course is symmetric.

**Determinant.** For a square matrix $\mathbf{A}_{(p\times p)}$, $|\mathbf{A}|$ is a scalar computed by cofactor expansion; for $p=2$, $\begin{vmatrix}a&b\\c&d\end{vmatrix}=ad-bc$. A matrix is **singular** iff $|\mathbf{A}|=0$, in which case it has no inverse. $|\mathbf{A}|$ equals the product of the eigenvalues of $\mathbf{A}$.

**Inverse.** $\mathbf{A}^{-1}$ is the unique matrix with $\mathbf{A}\mathbf{A}^{-1}=\mathbf{A}^{-1}\mathbf{A}=\mathbf{I}$, and exists iff $|\mathbf{A}|\neq 0$. For $2\times2$: $\begin{pmatrix}a&b\\c&d\end{pmatrix}^{-1}=\frac{1}{ad-bc}\begin{pmatrix}d&-b\\-c&a\end{pmatrix}$. This exact form is used in [[The Multivariate Normal Distribution]] to invert the $2\times2$ covariance matrix of the bivariate normal.

**Eigenvalues and eigenvectors.** A scalar $\lambda$ and nonzero vector $\mathbf{e}$ satisfying $\mathbf{A}\mathbf{e}=\lambda\mathbf{e}$ are an eigenvalue/eigenvector pair of $\mathbf{A}$. Eigenvalues are the roots of the characteristic polynomial $|\mathbf{A}-\lambda\mathbf{I}|=0$. For a symmetric matrix $\Sigma$, the eigenvectors can always be chosen mutually orthogonal and normalized ($\mathbf{e}_i'\mathbf{e}_j=0$ for $i\neq j$, $\mathbf{e}_i'\mathbf{e}_i=1$).

**Quadratic forms and positive-definiteness.** For symmetric $\mathbf{A}$ and vector $\mathbf{x}\neq\mathbf{0}$, the scalar $\mathbf{x}'\mathbf{A}\mathbf{x}$ is a *quadratic form*. $\mathbf{A}$ is **positive definite** if $\mathbf{x}'\mathbf{A}\mathbf{x}>0$ for all $\mathbf{x}\neq\mathbf{0}$, equivalently iff every eigenvalue of $\mathbf{A}$ is strictly positive. Every valid covariance matrix $\Sigma$ is positive semi-definite, and positive definite whenever no variable is an exact linear combination of the others — this is exactly the condition needed for $\Sigma^{-1}$ to exist and for the [[Statistical Distance and Mahalanobis Distance|Mahalanobis distance]] to be well defined.

## Properties
### Spectral decomposition
Any symmetric $\mathbf{A}_{(p\times p)}$ can be written as
$$
\mathbf{A} = \mathbf{Q}\boldsymbol\Lambda\mathbf{Q}' = \sum_{i=1}^{p}\lambda_i \mathbf{e}_i\mathbf{e}_i'
$$
where $\boldsymbol\Lambda=\operatorname{diag}(\lambda_1,\dots,\lambda_p)$ and $\mathbf{Q}=[\mathbf{e}_1\,\cdots\,\mathbf{e}_p]$ is orthogonal ($\mathbf{Q}'\mathbf{Q}=\mathbf{Q}\mathbf{Q}'=\mathbf{I}$). Consequences used repeatedly downstream:
- $\operatorname{tr}(\mathbf{A})=\sum_i \lambda_i$ (trace equals the sum of eigenvalues) — this is exactly how the total variance of a data matrix is partitioned across [[Principal Component Analysis|principal components]]: $\operatorname{tr}(\Sigma)=\sum_i\sigma_{ii}=\sum_i\lambda_i$.
- $|\mathbf{A}|=\prod_i \lambda_i$ — used in [[Generalized Variance]] and in [[Factor Analysis - Estimation and Rotation|Bartlett's sphericity test]].
- $\mathbf{A}^{-1}=\mathbf{Q}\boldsymbol\Lambda^{-1}\mathbf{Q}'=\sum_i \tfrac{1}{\lambda_i}\mathbf{e}_i\mathbf{e}_i'$, so $\Sigma\mathbf{e}=\lambda\mathbf{e} \iff \Sigma^{-1}\mathbf{e}=\tfrac{1}{\lambda}\mathbf{e}$: $\Sigma$ and $\Sigma^{-1}$ share eigenvectors, and their eigenvalues are reciprocals of each other.

### Derivative of a quadratic form (used by Lagrange-multiplier optimizations)
For symmetric $\mathbf{A}$,
$$
\frac{d}{d\mathbf{a}}\left(\mathbf{a}'\mathbf{A}\mathbf{a}\right) = 2\mathbf{A}\mathbf{a}, \qquad \frac{d}{d\mathbf{a}}(\mathbf{a}'\mathbf{a}) = 2\mathbf{a}
$$
This is exactly the identity used to derive the first principal component in [[Principal Component Analysis]]: maximizing $\mathbf{a}'\Sigma\mathbf{a}$ subject to $\mathbf{a}'\mathbf{a}=1$ via the Lagrangian $L(\mathbf{a})=\mathbf{a}'\Sigma\mathbf{a}-\lambda(\mathbf{a}'\mathbf{a}-1)$ gives $\frac{d}{d\mathbf{a}}L = 2\Sigma\mathbf{a}-2\lambda\mathbf{a}=0 \Rightarrow \Sigma\mathbf{a}=\lambda\mathbf{a}$: the maximizing direction is an eigenvector of $\Sigma$.

## Examples
The course's own matrix-algebra warm-up exercise (`A1-Matrices.docx`, "Jugando con matrices en R") asks the student to compute, for
$$
A=\begin{pmatrix}2&4&-3\\0&-2&5\\9&0&6\end{pmatrix},\quad B=\begin{pmatrix}8&6&-2\\-7&9&-5\\-3&5&1\end{pmatrix}:
$$
$A+B$, $4A+3B$, $A'$, $A^{-1}$, and $|A|$ and $|A'|$ (note $|A|=|A'|$ always, since transposing does not change a determinant). A second problem asks for the product $AB$ of a $3\times4$ and a $4\times2$ matrix, testing that matrix multiplication requires conforming inner dimensions. A third problem asks the student to compute, from four quantitative variables of a fast-food nutrition dataset, the mean vector, the covariance matrix, the correlation matrix, and the eigenvalues/eigenvectors of both — i.e., every quantity defined in [[Data Matrix, Mean Vector, and Covariance Matrix]] and this note, applied to real data.

## See also
[[Data Matrix, Mean Vector, and Covariance Matrix]], [[Principal Component Analysis]], [[Statistical Distance and Mahalanobis Distance]], [[The Multivariate Normal Distribution]]
