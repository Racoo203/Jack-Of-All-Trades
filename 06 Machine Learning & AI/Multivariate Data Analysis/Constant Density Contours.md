---
title: "Constant Density Contours"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 1 - Introducción a Métodos Multivariados"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, foundations, distance-measures]
---
## Definition
Given a mean vector $\boldsymbol\mu$ and covariance matrix $\Sigma$, the **constant-density contours** are the sets of points $\mathbf{x}$ at a fixed [[Statistical Distance and Mahalanobis Distance|Mahalanobis distance]] $c$ from $\boldsymbol\mu$:
$$
(\mathbf{x}-\boldsymbol\mu)'\Sigma^{-1}(\mathbf{x}-\boldsymbol\mu) = c^2
$$
In $p$ dimensions this defines the surface of an **ellipsoid** centered at $\boldsymbol\mu$. If $X\sim N_p(\boldsymbol\mu,\Sigma)$ (see [[The Multivariate Normal Distribution]]), points on this surface all have exactly the same probability density $f(\mathbf{x})$ — hence "constant density."

## Properties
### Orientation and axis lengths
Let $(\lambda_i,\mathbf{e}_i)$, $i=1,\dots,p$, be the eigenvalue/eigenvector pairs of $\Sigma$ (i.e. $\Sigma\mathbf{e}_i=\lambda_i\mathbf{e}_i$; see [[Matrix Algebra Foundations for Multivariate Analysis]]). The ellipsoid $(\mathbf{x}-\boldsymbol\mu)'\Sigma^{-1}(\mathbf{x}-\boldsymbol\mu)=c^2$ is centered at $\boldsymbol\mu$ with axes
$$
\pm c\sqrt{\lambda_i}\;\mathbf{e}_i, \qquad i=1,\dots,p
$$
i.e. the axes point along the eigenvectors of $\Sigma$, and their half-lengths are proportional to the square roots of the corresponding eigenvalues. This follows because $\Sigma^{-1}$ shares $\Sigma$'s eigenvectors with reciprocal eigenvalues ($\Sigma^{-1}\mathbf{e}_i=\tfrac{1}{\lambda_i}\mathbf{e}_i$), so translating to $\boldsymbol\mu=\mathbf{0}$ and writing $\Sigma^{-1}=\sum_i\tfrac{1}{\lambda_i}\mathbf{e}_i\mathbf{e}_i'$:
$$
c^2 = \mathbf{x}'\Sigma^{-1}\mathbf{x} = \frac{1}{\lambda_1}(\mathbf{e}_1'\mathbf{x})^2 + \cdots + \frac{1}{\lambda_p}(\mathbf{e}_p'\mathbf{x})^2 = \frac{1}{\lambda_1}Y_1^2+\cdots+\frac{1}{\lambda_p}Y_p^2
$$
where $Y_i=\mathbf{e}_i'\mathbf{x}$ is exactly the $i$-th [[Principal Component Analysis|principal component]] score — this is the standard equation of an ellipsoid in the rotated $(Y_1,\dots,Y_p)$ coordinate system, with semi-axis $c\sqrt{\lambda_i}$ along $Y_i$.

### Bivariate case: eigen-decomposition by hand
For $p=2$ with $\sigma_{11}=\sigma_{22}$, solving $|\Sigma-\lambda\mathbf{I}|=0$ for $\Sigma=\begin{pmatrix}\sigma_{11}&\sigma_{12}\\\sigma_{12}&\sigma_{11}\end{pmatrix}$ gives $(\sigma_{11}-\lambda)^2-\sigma_{12}^2=0$, so $\lambda_1=\sigma_{11}+\sigma_{12}$, $\lambda_2=\sigma_{11}-\sigma_{12}$, with eigenvectors $\mathbf{e}_1=\tfrac{1}{\sqrt2}(1,1)'$, $\mathbf{e}_2=\tfrac{1}{\sqrt2}(1,-1)'$ — always at $45°$ to the axes and passing through $\boldsymbol\mu$ regardless of the exact value of $\sigma_{12}$. If $\sigma_{12}>0$, $\lambda_1$ (the "positive-diagonal" direction) is the larger eigenvalue; if $\sigma_{12}<0$, $\lambda_2$ is larger. When $\sigma_{11}=\sigma_{22}$ and $\rho_{12}=0$ the contours are circles; otherwise they are ellipses.

### Probability content via the chi-square distribution
If $X\sim N_p(\boldsymbol\mu,\Sigma)$, the squared Mahalanobis distance $(\mathbf{x}-\boldsymbol\mu)'\Sigma^{-1}(\mathbf{x}-\boldsymbol\mu)$ is itself a random variable distributed as $\chi^2_p$ (chi-square with $p$ degrees of freedom). Consequently the solid ellipsoid
$$
(\mathbf{x}-\boldsymbol\mu)'\Sigma^{-1}(\mathbf{x}-\boldsymbol\mu) \le \chi^2_p(\alpha)
$$
has probability $1-\alpha$ under the distribution, where $\chi^2_p(\alpha)$ is the upper-$\alpha$ percentile of $\chi^2_p$. This is the basis both for confidence regions on $\boldsymbol\mu$ and for [[Validation of Multivariate Normality|chi-square QQ plots]] used to check multivariate normality.

## Examples
Worked numeric example carried through the deck: $S=\begin{pmatrix}5&4\\4&5\end{pmatrix}$, $\bar{\mathbf{x}}=(2,1)'$. Eigen-decomposition gives $\lambda_1=9$, $\mathbf{e}_1=\tfrac{1}{\sqrt2}(1,1)'$ and $\lambda_2=1$, $\mathbf{e}_2=\tfrac{1}{\sqrt2}(1,-1)'$: the ellipse's **major axis** extends $3c$ from $\bar{\mathbf{x}}$ in direction $(1,1)/\sqrt2$ and its **minor axis** extends $c$ in direction $(1,-1)/\sqrt2$, reflecting positive correlation between the two variables. Compare with $S=\begin{pmatrix}3&0\\0&3\end{pmatrix}$ (contours are circles, $\lambda_1=\lambda_2=3$, correlation zero) and $S=\begin{pmatrix}5&-4\\-4&5\end{pmatrix}$ (same eigenvalues as the first example but eigenvectors swapped in role, reflecting negative correlation). For $c^2=\chi^2_{2}(0.90)=4.605$ the ellipse contains 90% of the probability mass (10% falls outside); for $c^2=\chi^2_2(0.50)=1.386$ it contains 50%.

A second worked example computes the Mahalanobis distance of a specific observation directly: for $X\sim N_3(\boldsymbol\mu,\Sigma)$ with $\boldsymbol\mu'=(100,140,50)$ and $\Sigma=\begin{pmatrix}16&-9&10\\-9&18&-15\\10&-15&20\end{pmatrix}$, and $\mathbf{x}'=(97,130,44)$: $(\mathbf{x}-\boldsymbol\mu)'=(-3,-10,-6)$ and, using $\Sigma^{-1}=\begin{pmatrix}0.09375&0.02083&-0.03125\\0.02083&0.15278&0.10417\\-0.03125&0.10417&0.14375\end{pmatrix}$, $d^2(\mathbf{x},\boldsymbol\mu)=33.9216$, so $d(\mathbf{x},\boldsymbol\mu)=5.824$.

## See also
[[Statistical Distance and Mahalanobis Distance]], [[Matrix Algebra Foundations for Multivariate Analysis]], [[The Multivariate Normal Distribution]], [[Principal Component Analysis]], [[Validation of Multivariate Normality]]
