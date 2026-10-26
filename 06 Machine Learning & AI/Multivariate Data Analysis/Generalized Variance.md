---
title: "Generalized Variance"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 1 - Introducción a Métodos Multivariados"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, foundations, descriptive-statistics]
---
## Definition
A single number summarizing the overall spread encoded in a whole [[Data Matrix, Mean Vector, and Covariance Matrix|covariance matrix]] $S$ (all variances *and* covariances at once) is useful, and the **generalized variance** is defined as the determinant:
$$
\text{Generalized variance} = |S|
$$
It is well defined because $|S|\ge 0$ always (a valid covariance matrix is positive semi-definite; see [[Matrix Algebra Foundations for Multivariate Analysis]]), and it measures the area ($p=2$), volume ($p=3$), or hypervolume ($p>3$) occupied by the data cloud.

## Properties
### Geometric derivation for p = 2
Center $x_1,x_2$ at their means: $\mathbf{d}_1=\mathbf{x}_1-\bar x_1\mathbf{1}$, $\mathbf{d}_2=\mathbf{x}_2-\bar x_2\mathbf{1}$, with lengths $L_{d_1}=\lVert\mathbf{d}_1\rVert=\sqrt{n\,s_{11}}$, $L_{d_2}=\lVert\mathbf{d}_2\rVert=\sqrt{n\,s_{22}}$ (see [[Vector Geometry of the Data Matrix]]) and angle $\theta$ between them with $\cos\theta=r_{12}$. The area of the parallelogram (trapezoid) they span is $L_{d_1}L_{d_2}\sin\theta = L_{d_1}L_{d_2}\sqrt{1-\cos^2\theta} = n\sqrt{s_{11}s_{22}(1-r_{12}^2)}$. Since $s_{12}=r_{12}\sqrt{s_{11}s_{22}}$,
$$
|S| = \begin{vmatrix}s_{11}&s_{12}\\s_{12}&s_{22}\end{vmatrix} = s_{11}s_{22}-s_{12}^2 = s_{11}s_{22}(1-r_{12}^2), \qquad \text{Area} = n\sqrt{|S|}
$$
so $|S| = n^{-2}(\text{area})^2$, and for general $p$, $|S| = n^{-p}(\text{volume})^2$.

### Interpretation
- If the variables are **uncorrelated** ($r_{ik}=0$ for all $i\neq k$), $|S|=\prod_k s_{kk}$: the generalized variance is exactly the product of the individual variances.
- If two variables have $r_{ik}=\pm1$ (a deterministic linear relationship), $|S|=0$: the data occupies zero volume (it collapses onto a lower-dimensional subspace) and the generalized variance vanishes even though the individual variances $s_{ii}$ can be large.
- The stronger the correlation between variables, the smaller the enclosed volume and hence the smaller $|S|$, for fixed individual variances.
- $|S|$ says nothing about the **orientation** of the data's spread (see [[Constant Density Contours]] for that) — two very differently-shaped ellipses can share the same $|S|$, as the worked example below shows. So the generalized variance summarizes total dispersion but is not a substitute for the full covariance structure.

## Examples
The three examples reused from [[Constant Density Contours]] all have $|S|=9$ despite having different correlation structures and orientations: $S=\begin{pmatrix}5&4\\4&5\end{pmatrix}$ (positive correlation, $|S|=25-16=9$), $S=\begin{pmatrix}3&0\\0&3\end{pmatrix}$ (zero correlation, $|S|=9-0=9$), and $S=\begin{pmatrix}5&-4\\-4&5\end{pmatrix}$ (negative correlation, $|S|=25-16=9$) — the determinant is identical because it equals the product of the eigenvalues ($\lambda_1\lambda_2$) in every case ($9\times1$, $3\times3$, $1\times9$ respectively), even though the ellipses point in different directions. This is the concrete illustration of "generalized variance ignores orientation."

## See also
[[Data Matrix, Mean Vector, and Covariance Matrix]], [[Vector Geometry of the Data Matrix]], [[Constant Density Contours]], [[Matrix Algebra Foundations for Multivariate Analysis]]
