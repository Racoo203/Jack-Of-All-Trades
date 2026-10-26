---
title: "The Multivariate Normal Distribution"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 2 - Normalidad"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, normality, probability-distributions]
---
## Definition
The univariate normal density is $f(x)=\dfrac{1}{\sqrt{2\pi}\sigma}\exp\!\left\{-\dfrac{(x-\mu)^2}{2\sigma^2}\right\}$, and $\left(\dfrac{x-\mu}{\sigma}\right)^2=(x-\mu)(\sigma^2)^{-1}(x-\mu)$ is the squared statistical distance of $x$ from $\mu$ in units of variance. Generalizing this squared term to a $p$-variate random vector $\mathbf{x}$ gives exactly the squared [[Statistical Distance and Mahalanobis Distance|Mahalanobis distance]] $(\mathbf{x}-\boldsymbol\mu)'\Sigma^{-1}(\mathbf{x}-\boldsymbol\mu)$, and replacing the normalizing constant $(2\pi\sigma^2)^{-1/2}$ with its $p$-dimensional analogue $(2\pi)^{-p/2}|\Sigma|^{-1/2}$ (needed so the density integrates to $1$ in $p$ dimensions) gives the **multivariate normal density**:
$$
f(\mathbf{x}) = \frac{1}{(2\pi)^{p/2}|\Sigma|^{1/2}}\exp\left\{-\frac12(\mathbf{x}-\boldsymbol\mu)'\Sigma^{-1}(\mathbf{x}-\boldsymbol\mu)\right\}, \qquad \mathbf{x}\sim N_p(\boldsymbol\mu,\Sigma)
$$
where $\boldsymbol\mu_{(p\times1)}=E(\mathbf{x})$ and $\Sigma_{(p\times p)}=\operatorname{Cov}(\mathbf{x})$ ([[Data Matrix, Mean Vector, and Covariance Matrix|the population mean vector and covariance matrix]]).

Most multivariate techniques in this course assume $N_p(\boldsymbol\mu,\Sigma)$; even when the population is not exactly multivariate normal, the sampling distribution of many multivariate statistics tends toward normal as $n\to\infty$ (a multivariate central limit theorem), which is part of why the assumption is so pervasive.

## Properties
### Bivariate normal density in closed form
For $p=2$ with $\mu_1=E(X_1)$, $\mu_2=E(X_2)$, $\sigma_{11}=\operatorname{Var}(X_1)$, $\sigma_{22}=\operatorname{Var}(X_2)$, $\rho_{12}=\sigma_{12}/\sqrt{\sigma_{11}\sigma_{22}}$: inverting $\Sigma=\begin{pmatrix}\sigma_{11}&\sigma_{12}\\\sigma_{12}&\sigma_{22}\end{pmatrix}$ via the $2\times 2$ formula (see [[Matrix Algebra Foundations for Multivariate Analysis]]) and substituting gives
$$
f(x_1,x_2) = \frac{1}{2\pi\sqrt{\sigma_{11}\sigma_{22}(1-\rho_{12}^2)}}\exp\left\{-\frac{1}{2(1-\rho_{12}^2)}\left[\frac{(x_1-\mu_1)^2}{\sigma_{11}}+\frac{(x_2-\mu_2)^2}{\sigma_{22}}-2\rho_{12}\frac{(x_1-\mu_1)(x_2-\mu_2)}{\sqrt{\sigma_{11}\sigma_{22}}}\right]\right\}
$$
When $\rho_{12}=0$, this factors as $f(x_1,x_2)=f(x_1)f(x_2)$ with $X_1\sim N(\mu_1,\sigma_1)$, $X_2\sim N(\mu_2,\sigma_2)$ marginally: **for the multivariate normal, zero correlation between two components implies independence between them** (not true in general — see [[Vector Geometry of the Data Matrix]]'s counterexample with $Y=X^2$).

### Constant-density contours and the chi-square relationship
Derived fully in [[Constant Density Contours]]: the ellipsoid $(\mathbf{x}-\boldsymbol\mu)'\Sigma^{-1}(\mathbf{x}-\boldsymbol\mu)=c^2$ has axes $\pm c\sqrt{\lambda_i}\,\mathbf{e}_i$, and if $\mathbf{x}\sim N_p(\boldsymbol\mu,\Sigma)$ with $\Sigma$ positive definite, then $(\mathbf{x}-\boldsymbol\mu)'\Sigma^{-1}(\mathbf{x}-\boldsymbol\mu)\sim\chi^2_p$, so the solid ellipsoid with $c^2=\chi^2_p(\alpha)$ carries probability $1-\alpha$.

### Linear combinations remain normal
If $\mathbf{X}\sim N_p(\boldsymbol\mu,\Sigma)$ and $\mathbf{A}_{(q\times p)}$ is a matrix of constants, then the $q$ linear combinations $\mathbf{AX}$ are jointly $N_q(\mathbf{A}\boldsymbol\mu, \mathbf{A}\Sigma\mathbf{A}')$. Also, $\mathbf{X}+\mathbf{d} \sim N_p(\boldsymbol\mu+\mathbf{d},\Sigma)$ for a constant vector $\mathbf{d}$. A single linear combination $\mathbf{a}'\mathbf{X}=a_1X_1+\cdots+a_pX_p$ is univariate normal, $N(\mathbf{a}'\boldsymbol\mu,\mathbf{a}'\Sigma\mathbf{a})$. This is exactly the property that makes each [[Principal Component Analysis|principal component]] $Y_i=\mathbf{e}_i'\mathbf{X}$ normal whenever $\mathbf{X}$ is.

### Sums of independent normal vectors
If $\mathbf{X}_1,\dots,\mathbf{X}_n$ are mutually independent, each $N_p(\boldsymbol\mu,\Sigma)$, then $\mathbf{V}_1=c_1\mathbf{X}_1+\cdots+c_n\mathbf{X}_n \sim N_p\!\left(\sum_j c_j\boldsymbol\mu_j,\ \sum_j c_j^2\Sigma\right)$. Two such combinations $\mathbf{V}_1$ and $\mathbf{V}_2=b_1\mathbf{X}_1+\cdots+b_n\mathbf{X}_n$ are jointly multivariate normal with cross-covariance $\mathbf{b}'\mathbf{c}\,\Sigma$, so $\mathbf{V}_1$ and $\mathbf{V}_2$ are independent iff $\mathbf{b}'\mathbf{c}=\sum_j c_jb_j = 0$.

### Subsets and conditionals
Partition $\mathbf{X}=\begin{pmatrix}\mathbf{X}_1\\\mathbf{X}_2\end{pmatrix}$, $\boldsymbol\mu=\begin{pmatrix}\boldsymbol\mu_1\\\boldsymbol\mu_2\end{pmatrix}$, $\Sigma=\begin{pmatrix}\Sigma_{11}&\Sigma_{12}\\\Sigma_{21}&\Sigma_{22}\end{pmatrix}$: every subset $\mathbf{X}_1$ of a jointly normal vector is itself multivariate normal, $\mathbf{X}_1\sim N_q(\boldsymbol\mu_1,\Sigma_{11})$; conditional distributions of subsets of $\mathbf{X}$ are also multivariate normal; and $\mathbf{X}_1,\mathbf{X}_2$ are independent iff $\Sigma_{12}=\mathbf{0}$ (a block of zero covariances).

## Examples
**Bivariate probability calculation.** If $\mathbf{X}\sim N_2\!\left(\begin{pmatrix}0\\0\end{pmatrix},\begin{pmatrix}1&0\\0&1\end{pmatrix}\right)$, then $P(\mathbf{X}\le(0,0)')=0.25$ (R: `library(mnormt); pmnorm(c(0,0), c(0,0), matrix(c(1,0,0,1),nrow=2))`). For $\mathbf{X}\sim N_2\!\left(\begin{pmatrix}2.5\\4\end{pmatrix},\begin{pmatrix}1.2&0\\0&2.3\end{pmatrix}\right)$, $P(\mathbf{X}\le(2,3)')=0.08257$ — and since $\rho=0$ here, this equals the product of the two marginal probabilities: `pnorm(2,2.5,sqrt(1.2))*pnorm(3,4,sqrt(2.3))`.

**Linear combinations exercise.** $X_1,X_2\sim N(0,1)$ independent; $Y_1=3+2X_1-X_2$, $Y_2=5+X_1+X_2$: by the linear-combination property, $(Y_1,Y_2)'$ is bivariate normal with mean $(3,5)'$ and a covariance matrix computable from $\mathbf{A}=\begin{pmatrix}2&-1\\1&1\end{pmatrix}$ via $\mathbf{A}\Sigma\mathbf{A}'$; a further combination $Z=3Y_1+4Y_2-1$ is again univariate normal by the same rule. Raúl's own graded "Actividad 1.5" works this exact type of problem on a $3\times3$ data matrix $X=\begin{pmatrix}1&4&3\\6&2&6\\8&3&3\end{pmatrix}$, computing the mean vector $\bar{\mathbf x}=(5,3,4)'$ and covariance matrix (see [[Data Matrix, Mean Vector, and Covariance Matrix]]) and then the distribution of linear combinations $T_1'X=(1,1,1)X=X_1+X_2+X_3$ and $T_2'X=(1,2,-3)X=X_1+2X_2-3X_3$.

## See also
[[Statistical Distance and Mahalanobis Distance]], [[Constant Density Contours]], [[Data Matrix, Mean Vector, and Covariance Matrix]], [[Validation of Multivariate Normality]], [[Principal Component Analysis]]
