---
title: "Statistical Distance and Mahalanobis Distance"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 1 - Introducción a Métodos Multivariados"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, foundations, distance-measures]
---
## Definition
The **Euclidean distance** between two points $P(x_1,\dots,x_p)$ and $Q(y_1,\dots,y_p)$ in $\mathbb{R}^p$ is
$$
d(P,Q) = \sqrt{(x_1-y_1)^2+\cdots+(x_p-y_p)^2}
$$
Euclidean distance treats every coordinate as equally informative, but when the variables have different variances or are correlated this is misleading: a variable with large variance will naturally produce larger deviations, inflating its apparent contribution to dissimilarity. The **statistical distance** corrects for this. First, standardizing each coordinate by its own standard deviation, $x_1^*=x_1/\sqrt{s_{11}}$, $x_2^*=x_2/\sqrt{s_{22}}$, the statistical distance of $P(x_1,x_2)$ to the origin is
$$
d(P,O) = \sqrt{(x_1^*)^2+(x_2^*)^2} = \sqrt{\frac{x_1^2}{s_{11}}+\frac{x_2^2}{s_{22}}}
$$
This still assumes the variables are uncorrelated. Allowing correlation ($\sigma_{ik}\neq 0$) generalizes further to the **Mahalanobis distance**: for a data matrix with mean vector $\boldsymbol\mu$ and covariance matrix $\Sigma$,
$$
d^2 = (\mathbf{x}-\boldsymbol\mu)'\Sigma^{-1}(\mathbf{x}-\boldsymbol\mu)
$$
and between two points $P,Q$ with values $\mathbf{x},\mathbf{y}$,
$$
d^2(P,Q) = (\mathbf{x}-\mathbf{y})'\Sigma^{-1}(\mathbf{x}-\mathbf{y})
$$

## Properties
### Derivation via axis rotation
If $x_1,x_2$ are correlated, rotating the axes by angle $\theta$ to $(\tilde x_1,\tilde x_2)$ with $\tilde x_1 = x_1\cos\theta+x_2\sin\theta$, $\tilde x_2=-x_1\sin\theta+x_2\cos\theta$ (a choice of $\theta$ makes $\tilde x_1,\tilde x_2$ uncorrelated), the statistical distance in the rotated, uncorrelated frame is
$$
d(P,O) = \sqrt{\frac{\tilde x_1^2}{\tilde s_{11}}+\frac{\tilde x_2^2}{\tilde s_{22}}} = \sqrt{a_{11}x_1^2+2a_{12}x_1x_2+a_{22}x_2^2}
$$
a quadratic form in the *original* coordinates, where the $a_{ij}$ are trigonometric functions of $\theta,s_{11},s_{12},s_{22}$. In matrix form, $d^2(P,O)=\mathbf{x}'\begin{pmatrix}a_{11}&a_{12}\\a_{12}&a_{22}\end{pmatrix}\mathbf{x} > 0$ for $\mathbf{x}\neq\mathbf{0}$, so the matrix of coefficients is symmetric positive definite (see [[Matrix Algebra Foundations for Multivariate Analysis]]). Generalizing to $\mathbb{R}^p$,
$$
d(P,O) = \sqrt{\sum_{i=1}^p a_{ii}x_i^2 + 2\sum_{i<j}a_{ij}x_ix_j} = \sqrt{\mathbf{x}'\mathbf{A}\mathbf{x}}, \qquad \mathbf{A}\text{ symmetric}
$$
and identifying $\mathbf{A}=\Sigma^{-1}$ recovers the Mahalanobis form.

### Axioms of a distance function
Any function $d$ used to measure "closeness" must satisfy, for all points $P,Q,R$:
$$
d(P,Q)=d(Q,P), \qquad d(P,Q) > 0 \text{ if } P\neq Q, \qquad d(P,Q)=0 \text{ if } P=Q, \qquad d(P,Q)\le d(P,R)+d(R,Q)\ (\text{triangle inequality})
$$
Euclidean, statistical, and Mahalanobis distance all satisfy these; this is why all three are legitimate "distances" usable inside [[Hierarchical Cluster Analysis]] and [[Non-Hierarchical Cluster Analysis (K-Means and K-Medoids)|non-hierarchical clustering]], even though they weight coordinates differently.

### Why the correction matters geometrically
Points whose squared statistical distance to a fixed centroid equals a constant $c^2$ trace out an **ellipse** (not a circle as with Euclidean distance) — see [[Constant Density Contours]] for the full derivation of the ellipse's orientation and axis lengths from the eigenvalues/eigenvectors of $\Sigma$. Intuitively, the correction "shrinks" the influence of high-variance directions and can make a point that looks Euclidean-far from the data's centroid actually be *closer* in the statistical sense, because it lies along the data's natural direction of spread.

## Examples
The lecture motivates this with a scatterplot centroid $Q$ (sample means) and a point $P$ near the edge of the data cloud along the direction of maximum spread: the Euclidean distance from $Q$ to $P$ looks larger than the Euclidean distance from the origin to $Q$, suggesting $P$ is an outlier — but $P$ lies along the data's principal direction of variability, so the Mahalanobis distance correctly judges $P$ to belong to the sample. A fully worked numeric example (same $\Sigma=\begin{pmatrix}5&4\\4&5\end{pmatrix}$, $\bar{\mathbf{x}}=(2,1)'$ used repeatedly across the deck) is carried through in [[Constant Density Contours]] and [[Generalized Variance]].

## See also
[[Data Matrix, Mean Vector, and Covariance Matrix]], [[Constant Density Contours]], [[Generalized Variance]], [[The Multivariate Normal Distribution]], [[Hierarchical Cluster Analysis]]
