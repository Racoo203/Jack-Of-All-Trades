---
title: "Vector Geometry of the Data Matrix"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 1 - Introducción a Métodos Multivariados"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, foundations, linear-algebra]
---
## Definition
Reading the [[Data Matrix, Mean Vector, and Covariance Matrix|data matrix]] column-wise, each variable $\mathbf{x}_k=(x_{1k},\dots,x_{nk})'\in\mathbb{R}^n$ is a vector in the *individuals' space*. For $\mathbf{x},\mathbf{y}\in\mathbb{R}^n$, the **dot product** is
$$
\mathbf{x}'\mathbf{y} = \mathbf{x}\cdot\mathbf{y} = \sum_{i=1}^n x_i y_i
$$
the squared **norm** (length) is $\lVert\mathbf{x}\rVert^2 = \mathbf{x}'\mathbf{x}=\sum_i x_i^2$, and the angle $\theta\in[0,\pi]$ between $\mathbf{x}$ and $\mathbf{y}$ satisfies
$$
\cos\theta = \frac{\mathbf{x}'\mathbf{y}}{\lVert\mathbf{x}\rVert\,\lVert\mathbf{y}\rVert}
$$
This geometry — not just algebraic formulas — underlies the variance/covariance/correlation identities below.

## Properties
### Variance as squared length
Writing $s_{kk}=\frac{1}{n}(\mathbf{x}_k-\bar x_k\mathbf{1})'(\mathbf{x}_k-\bar x_k\mathbf{1}) = \frac{1}{n}\lVert \mathbf{x}_k-\bar x_k\mathbf{1}\rVert^2$: if $\bar x_k=0$ (or the variable is mean-centered), the *length* of the variable's vector is proportional to its standard deviation — $s_{kk}=\frac{1}{n}\lVert\mathbf{x}_k\rVert^2$. A "large" vector means a high-variance variable; this holds regardless of centering, since translation does not change variance.

### Correlation as cosine of an angle
If $\bar x_i=0$ and $\bar x_k=0$ (or the variables are centered),
$$
\cos\theta = \frac{\mathbf{x}_i'\mathbf{x}_k}{\lVert\mathbf{x}_i\rVert\lVert\mathbf{x}_k\rVert} = \frac{\sum_j x_{ji}x_{jk}}{\sqrt{\sum_j x_{ji}^2}\sqrt{\sum_j x_{jk}^2}} = \frac{\sum_j (x_{ji}-\bar x_i)(x_{jk}-\bar x_k)}{\sqrt{\sum_j(x_{ji}-\bar x_i)^2}\sqrt{\sum_j(x_{jk}-\bar x_k)^2}} = \frac{n\,s_{ik}}{n\sqrt{s_{ii}s_{kk}}} = r_{ik}
$$
so **the sample correlation coefficient is literally the cosine of the angle between the two (centered) variable vectors.** This gives an exact geometric dictionary: $r_{ik}=1 \iff \theta=0$ (vectors parallel, same direction); $r_{ik}=-1\iff\theta=\pi$ (parallel, opposite direction); $r_{ik}=0\iff\theta=\pi/2$ (orthogonal); $r_{ik}>0 \iff \theta<\pi/2$; $r_{ik}<0\iff\theta>\pi/2$. Since translation does not affect the relationship between $x_i$ and $x_k$, this also holds for uncentered variables.

### Cauchy–Schwarz inequality
For any $\mathbf{x}_i,\mathbf{x}_k$: $|\mathbf{x}_i'\mathbf{x}_k| \le \lVert\mathbf{x}_i\rVert\,\lVert\mathbf{x}_k\rVert$, with equality iff $\mathbf{x}_i=\mathbf{0}$ or $\mathbf{x}_k=\mathbf{0}$, or $\mathbf{x}_i=a\mathbf{x}_k$ for some scalar $a$. Combined with $\cos\theta=r_{ik}=\frac{\mathbf{x}_i'\mathbf{x}_k}{\lVert\mathbf{x}_i\rVert\lVert\mathbf{x}_k\rVert}$, dividing both sides of Cauchy–Schwarz by $\lVert\mathbf{x}_i\rVert\lVert\mathbf{x}_k\rVert$ gives $\left|\frac{\mathbf{x}_i'\mathbf{x}_k}{\lVert\mathbf{x}_i\rVert\lVert\mathbf{x}_k\rVert}\right|=1$ exactly when $\mathbf{x}_i=a\mathbf{x}_k$ — i.e., $r_{ik}=\pm1 \iff$ the two variables are exact linear functions of each other, which is exactly the boundary case algebraically, now derived geometrically.

### Correlation and independence are not equivalent
If $\mathbf{x}_i,\mathbf{x}_k \sim N(\boldsymbol\mu,\Sigma)$ jointly (see [[The Multivariate Normal Distribution]]), then $s_{ik}=0 \iff$ independence, so $r_{ik}=0\iff$ independence — but this equivalence is special to joint normality. In general, zero covariance does **not** imply independence: if $X\sim N(0,\sigma)$ and $Y=X^2$, then
$$
\operatorname{Cov}(X,Y)=E(XY)-E(X)E(Y)=E(X\cdot X^2)-0 = E(X^3)
$$
and since $X^3$ is an odd function symmetric about the origin, $E(X^3)=0$, so $\operatorname{Cov}(X,Y)=0$ and $r=0$ — yet $Y$ is a deterministic (hence maximally dependent) function of $X$.

## Examples
No numeric example is given beyond the derivations themselves in the source slides; the natural worked instance is any pair of columns of the fast-food data matrix used in [[Matrix Algebra Foundations for Multivariate Analysis]]'s exercise — computing $r_{ik}$ both as a covariance ratio and, after centering, as $\cos\theta$ between the two column vectors gives numerically identical answers.

## See also
[[Data Matrix, Mean Vector, and Covariance Matrix]], [[Statistical Distance and Mahalanobis Distance]], [[Generalized Variance]]
