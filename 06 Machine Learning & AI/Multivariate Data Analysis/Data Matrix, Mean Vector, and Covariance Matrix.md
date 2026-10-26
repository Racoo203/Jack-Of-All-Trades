---
title: "Data Matrix, Mean Vector, and Covariance Matrix"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 1 - Introducción a Métodos Multivariados"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, foundations, descriptive-statistics]
---
## Definition
A sample of $n$ individuals measured on $p$ variables is arranged as the **data matrix**
$$
\mathbf{X}_{(n\times p)} = \begin{pmatrix} x_{11} & x_{12} & \cdots & x_{1p}\\ x_{21} & x_{22} & \cdots & x_{2p}\\ \vdots & \vdots & & \vdots\\ x_{n1} & x_{n2} & \cdots & x_{np}\end{pmatrix}
$$
where rows are individuals (the unit of analysis) and columns are variables. Row $j$, $\mathbf{x}_j'=(x_{j1},\dots,x_{jp})$, is the observation vector for individual $j$; column $k$, $\mathbf{x}_{(k)}=(x_{1k},\dots,x_{nk})'$, is the vector of all observations of variable $k$. Individuals live in $\mathbb{R}^p$ (the space of variables) and variables live in $\mathbb{R}^n$ (the space of individuals) — the same matrix $\mathbf{X}$ can be read either way.

The **sample mean** of variable $k$ is $\bar{x}_k = \frac{1}{n}\sum_{j=1}^n x_{jk}$, collected into the **mean vector** $\bar{\mathbf{x}}=(\bar x_1,\dots,\bar x_p)'$.

## Properties
### Vector form of the mean
Writing $\mathbf{1}=\mathbf{1}_n=(1,\dots,1)'$, $\bar x_k = \frac{1}{n}\mathbf{x}_{(k)}'\mathbf{1}$, and stacking over $k$:
$$
\bar{\mathbf{x}} = \frac{1}{n}\mathbf{X}'\mathbf{1}
$$

### Sample variance and covariance
For the $k$-th variable, the **sample variance** is
$$
s_k^2 = s_{kk} = \frac{1}{n}\sum_{j=1}^n (x_{jk}-\bar x_k)^2 = \frac{1}{n}(\mathbf{x}_k-\bar x_k\mathbf{1})'(\mathbf{x}_k-\bar x_k\mathbf{1})
$$
(this course uses the $n$-divisor, biased, MLE-style estimator throughout — not $n-1$). For variables $i,k$, the **sample covariance** is
$$
s_{ik} = \frac{1}{n}\sum_{j=1}^n (x_{ji}-\bar x_i)(x_{jk}-\bar x_k) = \frac{1}{n}(\mathbf{x}_i-\bar x_i\mathbf{1})'(\mathbf{x}_k-\bar x_k\mathbf{1})
$$

### The covariance matrix
Collecting all pairs into the $(p\times p)$ **sample covariance matrix**:
$$
S = \frac{1}{n}(\mathbf{X}-\bar{\mathbf{X}})'(\mathbf{X}-\bar{\mathbf{X}}) = \begin{pmatrix} s_{11} & s_{12} & \cdots & s_{1p}\\ s_{21} & s_{22} & \cdots & s_{2p}\\ \vdots & & \ddots & \vdots \\ s_{p1} & s_{p2} & \cdots & s_{pp}\end{pmatrix}
$$
$S$ is symmetric ($s_{ik}=s_{ki}$) and its diagonal holds the variances. (See [[Matrix Algebra Foundations for Multivariate Analysis]] for why $S$ being positive (semi-)definite is what makes $S^{-1}$ exist.)

### The correlation matrix
The **sample correlation coefficient** (Pearson) between variables $i$ and $k$ is
$$
r_{ik} = \frac{s_{ik}}{\sqrt{s_{ii}s_{kk}}} = \frac{\sum_{j=1}^n (x_{ji}-\bar x_i)(x_{jk}-\bar x_k)}{\sqrt{\sum_{j=1}^n(x_{ji}-\bar x_i)^2}\sqrt{\sum_{j=1}^n(x_{jk}-\bar x_k)^2}} \in [-1,1]
$$
Its sign is the sign of the covariance; its magnitude is the strength of the linear association. Collected into $R$ (symmetric, unit diagonal): if $V^{1/2}=\operatorname{diag}(\sqrt{s_{11}},\dots,\sqrt{s_{pp}})$, then $R = (V^{1/2})^{-1} S (V^{1/2})^{-1}$ — correlation is covariance after standardizing each variable's scale.

### Population versions
With $n\to\infty$ (a theoretical, infinite population), the random matrix $\mathbf{X}$ has population mean $\boldsymbol\mu = E(\mathbf{X})$ (elementwise expectation) and population covariance matrix
$$
\Sigma = \operatorname{Cov}(\mathbf{x}) = \frac{1}{N}(\mathbf{x}-\boldsymbol\mu)'(\mathbf{x}-\boldsymbol\mu)
$$
For matrices of constants $\mathbf{A}_{(m\times n)}, \mathbf{B}_{(r\times p)}$ and random matrices $\mathbf{X},\mathbf{Y}$ of matching dimension: $E(\mathbf{X}+\mathbf{Y})=E(\mathbf{X})+E(\mathbf{Y})$ and $E(\mathbf{AXB})=\mathbf{A}E(\mathbf{X})\mathbf{B}$ — linearity of expectation carries over to matrices entrywise.

## Examples
The introductory slide deck works through this notation abstractly (no numeric worked example beyond the formulas themselves); the numeric worked instance is the course's own exercise in [[Matrix Algebra Foundations for Multivariate Analysis]]'s Examples section (mean vector, $S$, and $R$ for four nutrition variables of a fast-food dataset), and the graded homework "Actividad 1.5" computes $\bar{\mathbf{x}}$ and $S$ by hand in R (`colMeans`, `cov`) for a $3\times3$ toy data matrix, confirming $\bar{\mathbf{x}}=(5,3,4)'$ and $S=\begin{pmatrix}13&-2.5&1.5\\-2.5&1&-1.5\\1.5&-1.5&3\end{pmatrix}$ — see [[The Multivariate Normal Distribution]] for how this exact exercise continues into linear combinations.

## See also
[[Matrix Algebra Foundations for Multivariate Analysis]], [[Vector Geometry of the Data Matrix]], [[Statistical Distance and Mahalanobis Distance]], [[Generalized Variance]], [[The Multivariate Normal Distribution]]
