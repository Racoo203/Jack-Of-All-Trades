---
title: "Principal Component Analysis"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 3 - Componentes Principales"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, dimensionality-reduction, interdependence-analysis]
---
## Definition
**Principal Component Analysis (PCA)** re-expresses a data matrix of $p$ correlated variables $X_1,\dots,X_p$ as $r<p$ new, uncorrelated variables (**components**) $Y_1,\dots,Y_r$ that are linear combinations of the originals, chosen so that the retained $r$ components capture as much of the total variability as possible while the discarded $p-r$ are (ideally) negligible. Geometrically, PCA selects a new coordinate system — a rotation of the original axes $X_1,\dots,X_p$ — obtained from the directions of maximum variability of the data; algebraically, the components are found from the eigenvalues and eigenvectors of the covariance matrix $\Sigma$ (see [[Matrix Algebra Foundations for Multivariate Analysis]]).

Objectives: reduce dimensionality, and assess similarity between individuals or variables via a simpler representation.

**Assumptions.** Variables must be numeric; $n$ should be at least $\approx 10\times p$; **no normality assumption is required** (though if $\mathbf{X}\sim N_p(\boldsymbol\mu,\Sigma)$ the components have a richer interpretation, see below); no homoscedasticity requirement; **variables must be correlated** (uncorrelated variables give no reduction — each would need its own component).

## Properties
### The optimization problem and its solution via Lagrange multipliers
The $i$-th component is $Y_i=\mathbf{a}_i'\mathbf{X}$, and the components are built sequentially: find $\mathbf{a}_1$ maximizing $\operatorname{Var}(\mathbf{a}_1'\mathbf{X})=\mathbf{a}_1'\Sigma\mathbf{a}_1$ subject to $\mathbf{a}_1'\mathbf{a}_1=1$ (a normalization — without it, variance could be inflated arbitrarily by scaling $\mathbf{a}_1$); find $\mathbf{a}_2$ maximizing $\operatorname{Var}(\mathbf{a}_2'\mathbf{X})$ subject to $\mathbf{a}_2'\mathbf{a}_2=1$ **and** $\operatorname{Cov}(\mathbf{a}_1'\mathbf{X},\mathbf{a}_2'\mathbf{X})=0$ (i.e. $\mathbf{a}_1'\mathbf{a}_2=0$); and so on up to $\mathbf{a}_p$, each new component uncorrelated with all previous ones.

For the first component, using a Lagrange multiplier on $L(\mathbf{a})=\mathbf{a}'\Sigma\mathbf{a}-\lambda(\mathbf{a}'\mathbf{a}-1)$:
$$
\frac{d}{d\mathbf{a}}L(\mathbf{a}) = 2\Sigma\mathbf{a}-2\lambda\mathbf{a} = 0 \quad\Longrightarrow\quad \Sigma\mathbf{a}=\lambda\mathbf{a}
$$
i.e. $(\mathbf{a},\lambda)$ must be an eigenvector/eigenvalue pair of $\Sigma$. Then $\operatorname{Var}(\mathbf{a}'\mathbf{X})=\operatorname{Var}(\mathbf{e}_1'\mathbf{X})=\mathbf{e}_1'\Sigma\mathbf{e}_1=\mathbf{e}_1'(\lambda_1\mathbf{e}_1)=\lambda_1(\mathbf{e}_1'\mathbf{e}_1)=\lambda_1$: **to maximize the variance, $\lambda_1$ must be the largest eigenvalue of $\Sigma$**, and $\mathbf{e}_1$ its corresponding eigenvector. Ordering all $p$ eigenvalues $\lambda_1>\lambda_2>\cdots>\lambda_p$ (largest to smallest) gives the $i$-th component's eigenvalue/eigenvector pair directly: $\lambda_i$ is the $i$-th largest eigenvalue of $\Sigma$, $\mathbf{e}_i$ its eigenvector.

### Total variance is preserved and partitioned
Since $\Sigma$ is diagonalizable, $\Sigma=\mathbf{Q}\boldsymbol\Lambda\mathbf{Q}'$ with $\mathbf{Q}$ orthogonal. Total variance $\operatorname{Var}_T(\mathbf{X})=\sigma_{11}+\cdots+\sigma_{pp}=\operatorname{tr}(\Sigma)=\operatorname{tr}(\mathbf{Q}\boldsymbol\Lambda\mathbf{Q}')=\operatorname{tr}(\boldsymbol\Lambda\mathbf{Q}\mathbf{Q}')=\operatorname{tr}(\boldsymbol\Lambda)=\lambda_1+\cdots+\lambda_p$. So $\operatorname{Var}_T(\mathbf{X})=\operatorname{Var}_T(\mathbf{Y})$: PCA does not lose or create variance, it only reallocates it across uncorrelated components. The **proportion of variance explained** by component $i$ is therefore
$$
\text{Prop}(\operatorname{Var}(Y_i)) = \frac{\lambda_i}{\sum_{k=1}^p \lambda_k}
$$
and components are retained until a cumulative proportion is judged "high enough," or via a scree plot ("gráfico de sedimentación") looking for the elbow where added components stop contributing meaningfully.

### Component–variable correlations
The correlation between component $Y_i$ and original variable $X_k$ is
$$
\rho_{Y_i,X_k} = \frac{e_{ik}\sqrt{\lambda_i}}{\sqrt{\sigma_{kk}}}
$$
so a variable's weight/importance within a component depends jointly on its eigenvector coefficient $e_{ik}$, the component's variance $\lambda_i$, and the variable's own variance $\sigma_{kk}$ — a raw eigenvector coefficient alone can be a misleading measure of a variable's importance if variables are on very different scales.

### Standardized principal components
If variables have very different scales, standardize first: $\mathbf{Z}=\mathbf{V}^{-1/2}(\mathbf{X}-\boldsymbol\mu)$ where $\mathbf{V}^{1/2}=\operatorname{diag}(\sqrt{\sigma_{11}},\dots,\sqrt{\sigma_{pp}})$. Then $\operatorname{Cov}(\mathbf{Z})=\mathbf{V}^{-1/2}\Sigma\mathbf{V}^{-1/2}=\rho$ (the correlation matrix), so **running PCA on standardized variables is the same as running the eigen-decomposition on the correlation matrix $R$ instead of the covariance matrix $S$** — a different (in general) set of components than unstandardized PCA, since $S$ and $R$ do not share eigenvectors unless all variances are equal.

### Relationship to the multivariate normal
If $\mathbf{X}\sim N_p(\boldsymbol\mu,\Sigma)$, the [[Constant Density Contours|constant-density ellipsoids]] $(\mathbf{x}-\boldsymbol\mu)'\Sigma^{-1}(\mathbf{x}-\boldsymbol\mu)=c^2$ have axes exactly along the eigenvectors $\mathbf{e}_i$ of $\Sigma$ with half-length $c\sqrt{\lambda_i}$ — i.e. **the principal components are precisely the axes of the normal distribution's elliptical contours**, and the standardized principal component scores $\hat Y_i = \hat{\mathbf{e}}_i'(\mathbf{x}-\bar{\mathbf{x}})$ behave as $N_p(\mathbf{0},\boldsymbol\Lambda)$. When the data has no clear directions of unequal variability (contours close to circular, similar variance in every direction), dimension reduction by PCA is not meaningful — there is no dominant direction to retain.

## Examples
A 6-variable numeric example (`x1`–`x6`) gives, from the covariance matrix, eigenvalues $107936, 54574, 15544, 2262, 1324, 91$ with cumulative proportions $0.594, 0.894, 0.980, 0.992, 0.999, 1.000$ — the first two components already explain $89.4\%$ of total variance, e.g. $Y_1=0.077X_1-0.151X_2+0.981X_3+0.069X_4-0.017X_5-0.059X_6$ (dominated by $X_3$). Re-running on the **correlation matrix** (standardized variables) gives entirely different eigenvalues $2.4209, 1.8857, 1.0566, 0.3744, 0.2491, 0.0134$ (proportions summing to $1$ over $p=6$, since $\operatorname{tr}(R)=p$) and different loadings — confirming that standardized and unstandardized PCA are genuinely different analyses.

A smaller, fully-worked $p=3$ example uses $\Sigma=\begin{pmatrix}1&-2&0\\-2&5&0\\0&0&2\end{pmatrix}$: eigenvalues $\lambda_1=5.8284,\lambda_2=2,\lambda_3=0.17157$ with proportions of variance $72.86\%$ (first component alone) and $97.86\%$ (first two together); the second component is exactly $Y_2=X_3$ because $X_3$ is uncorrelated with $X_1,X_2$. Analyzing $Y_1=\mathbf{e}_1'\mathbf{X}=0.383X_1-0.924X_2$: since $|{-0.924}|>|0.383|$, $X_2$ contributes more to $Y_1$ than $X_1$, and the opposite signs mean both variables matter (in opposing directions) to the component's interpretation.

Applied case study: a Cuban biotechnology paper (Mesa-Ramos et al., *VacciMonitor* 2018) applies PCA to monitor a monoclonal-antibody fermentation process, reducing many process variables to two principal components that jointly explain over 99% of the variance and identify the main sources of process variability — a direct real-world instance of "reduce dimensionality while retaining nearly all the information."

## See also
[[Matrix Algebra Foundations for Multivariate Analysis]], [[Constant Density Contours]], [[The Multivariate Normal Distribution]], [[Factor Analysis - The Orthogonal Factor Model]], [[Data Scaling and Standardization]], [[Hierarchical Cluster Analysis]]
