---
title: "Factor Analysis - Estimation and Rotation"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 4 - Análisis Factorial"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, dimensionality-reduction, interdependence-analysis]
---
## Definition
Fitting [[Factor Analysis - The Orthogonal Factor Model|the orthogonal factor model]] $\Sigma=\mathbf{LL}'+\boldsymbol\Psi$ to data proceeds in phases: (1) verify the assumption that variables are correlated enough to justify factor analysis; (2) estimate the loading matrix $\mathbf{L}$ (and hence the communalities) via one of several methods; (3) decide the optimal number of factors $m$; (4) rotate $\mathbf{L}$ to ease interpretation; (5) estimate factor scores for each individual.

## Properties
### Verifying the assumptions: Bartlett's test of sphericity
Tests whether the population correlation matrix is the identity (no correlation at all, in which case factor analysis is pointless):
$$
H_0: \Sigma=\Sigma_0 \text{ (diagonal, no correlation)} \qquad\text{vs.}\qquad H_1:\Sigma\neq\Sigma_0
$$
Test statistic:
$$
\chi^2_{\frac{p^2-p}{2}} = -2\left(1-\frac{2p+11}{6n}\right)\ln|R|
$$
where $|R|$ is the determinant of the sample correlation matrix, $p$ the number of variables, $n$ the number of observations, and $\frac{p^2-p}{2}$ the degrees of freedom. Since $|R|=\prod_i \lambda_i$ (product of $R$'s eigenvalues; see [[Matrix Algebra Foundations for Multivariate Analysis]]), $|R|$ near $1$ (near-identity $R$) gives $\ln|R|\approx 0$ (small statistic, fail to reject $H_0$ — factor analysis not warranted), while $|R|$ near $0$ (highly correlated variables) gives a large-magnitude negative $\ln|R|$ and hence a large statistic (reject $H_0$ — proceed with factor analysis).

### Verifying the assumptions: partial correlations and the KMO index
The **partial correlation** between $X_i,X_k$ measures their association after removing the shared influence of the other variables — e.g. controlling for $X_1$:
$$
r_{23.1} = \frac{r_{23}-r_{21}r_{31}}{\sqrt{1-r_{21}^2}\sqrt{1-r_{31}^2}}
$$
and generally $a_{ij}^* = -\dfrac{R_{ij}}{\sqrt{R_{ii}R_{jj}}} = -\dfrac{s^{ij}}{\sqrt{s^{ii}s^{jj}}}$, where $|R_{ij}|$ is the determinant of $R$ with row $i$/column $j$ removed and $s^{ij}$ is entry $(i,j)$ of $\Sigma^{-1}$. If variables genuinely share common factors, their *partial* correlations (controlling for everything else) should be low even though their *simple* correlations are high. The **Kaiser–Meyer–Olkin (KMO) index** formalizes this trade-off:
$$
KMO = \frac{\sum_i\sum_j r_{ij}^2}{\sum_i\sum_j r_{ij}^2 + \sum_i\sum_j (a_{ij}^*)^2} \in [0,1]
$$
Interpretation: $0.8\le KMO\le1$ high correlation (good for FA); $0.7\le KMO<0.8$ medium; $KMO\le0.5$ low (FA not advisable); values near $0$ indicate the partial correlations dominate the simple correlations, a sign of generalized correlation that is problematic for factor analysis. General rule of thumb: proceed with FA if $KMO>0.5$.

### Estimation methods
- **Principal Components method.** From the spectral decomposition $\Sigma=\lambda_1\mathbf{e}_1\mathbf{e}_1'+\cdots+\lambda_p\mathbf{e}_p\mathbf{e}_p' = \mathbf{LL}'$ with $\mathbf{L}=[\sqrt{\lambda_1}\mathbf{e}_1\ \cdots\ \sqrt{\lambda_p}\mathbf{e}_p]$, taking all $p$ factors reproduces $\Sigma$ exactly with $\boldsymbol\Psi=\mathbf{0}$ (impractical); truncating to the $m$ largest eigenvalues gives $\Sigma\approx\mathbf{L}_{(p\times m)}\mathbf{L}'+\boldsymbol\Psi$ with $\boldsymbol\Psi\approx\Sigma-\mathbf{LL}'$ and communalities $\hat h_i^2=\tilde\ell_{i1}^2+\cdots+\tilde\ell_{im}^2$. Advantage: always gives a solution. Disadvantage: not based on the factor model itself, so it can produce biased loading estimates (especially with low communalities).
- **Principal (Common) Factor method (PAF/PFA).** Iterative: start from an initial $\mathbf{L}_0$ (via PCA on the correlation matrix $R$), estimate $\boldsymbol\Psi$ from $R-\boldsymbol\Psi=\mathbf{LL}'$, re-estimate $\mathbf{L}$, and iterate to convergence — applies the PCA-like strategy but to a correlation matrix whose diagonal holds estimated communalities rather than $1$'s. Advantage: better estimates than the PCA method. Disadvantage: convergence is not guaranteed, especially in small samples.
- **Maximum Likelihood method.** Assumes $\mathbf{F}$ and $\boldsymbol\varepsilon$ jointly normal (so $\mathbf{X}-\boldsymbol\mu=\mathbf{LF}+\boldsymbol\varepsilon$ is normal too) and maximizes the multivariate normal likelihood over $\mathbf{L},\boldsymbol\Psi$ subject to $\mathbf{L}\boldsymbol\Psi^{-1}\mathbf{L}'=\boldsymbol\Delta$ (diagonal, for identifiability). Fit iteratively, increasing $m$ one factor at a time until satisfactory. Advantage: scale-invariant, asymptotically unbiased and efficient estimates, factors normally distributed, and a formal $\chi^2$ goodness-of-fit test is available for the chosen $m$. Disadvantage: convergence problems if multivariate normality fails.
- Other, less common: unweighted and generalized least squares.

### Number of factors: hypothesis test under Maximum Likelihood
$$
H_0: \Sigma = \mathbf{LL}'+\boldsymbol\Psi \quad (m \text{ factors suffice})
$$
Test statistic (with Bartlett's correction):
$$
\left[n-1-\frac{2p+4m+5}{6}\right]\ln\left(\frac{|\mathbf{LL}'+\boldsymbol\Psi|}{|S_n|}\right) \sim \chi^2_{\text{(df depending on }m,p)}
$$
### Number of factors: Kaiser's rule and the scree plot
**Kaiser's criterion** (most common in statistical packages): retain factors with eigenvalue $>1.0$ (i.e. each retained factor should explain at least as much variance as one original variable). Can under-detect the true number of factors when $p$ is small, and over-detect when $p$ is large. **Percentage of variance explained**: retain enough factors to explain a "sufficient" cumulative percentage; the **scree plot** (eigenvalues vs. factor number) looks for the "elbow" where the slope changes, suggesting the count of factors worth keeping.

### Rotation
Exploiting the rotational ambiguity derived in [[Factor Analysis - The Orthogonal Factor Model]] ($\mathbf{L}^*=\mathbf{LT}$ for any orthogonal $\mathbf{T}$): rotation changes the loadings, the proportion of variance attributed to each factor, and hence the ease of interpretation, but leaves $\Sigma=\mathbf{LL}'+\boldsymbol\Psi$ unchanged. **Orthogonal rotations** keep factors uncorrelated: **Varimax** (the most-used method) maximizes the variance of the squared loadings within each factor, pushing loadings toward either very high or very low, which sharpens interpretation; **Quartimax** minimizes the number of factors needed to explain each variable; **Equimax** is a compromise between the two. **Oblique rotations** (e.g. Oblimin, Promax, Equamax) allow the resulting factors to be correlated — useful when the underlying constructs are plausibly related, at the cost of a more complex interpretation.

### Comparing the Principal Components and Maximum Likelihood methods
On the same dataset (Johnson & Wichern's Example 9.6, four track-and-field events), the Principal Components method explains more total variance ($0.76$ vs. $0.62$) and gives no specific variance above $0.4$ (high communalities across the board, small residual matrix $R=\mathbf{LL}'+\boldsymbol\Psi$ close to zero), while Maximum Likelihood explains less variance but reproduces the correlation matrix *better* (residual matrix closer to zero) and gives more interpretable, sharply-separated factors (e.g. splitting "running endurance" and "throwing strength" into distinct factors that PCA leaves partly mixed) — illustrating that the two methods can disagree on both the amount of variance explained and the interpretability of the result, and that a smaller residual matrix (not a larger proportion of variance explained) is the better indicator of model fit.

## Examples
**The toothpaste ("dentífrico") study.** 30 respondents rate agreement (1–7 scale) with 6 statements about toothpaste-purchase motivations ($V_1$ prevents cavities, $V_2$ leaves teeth shiny, $V_3$ strengthens gums, $V_4$ freshens breath, $V_5$ prevention of weakening teeth is not important [reverse-coded], $V_6$ whiteness is the most important consideration). Correlation inspection shows $V_1,V_3,V_5$ correlate strongly (health-benefit cluster) and $V_2,V_4,V_6$ correlate moderately (cosmetic-benefit cluster) — a visual preview of the two factors to come. Bartlett's test rejects $H_0$ (independence) and $KMO>0.5$, both confirming factor analysis is appropriate. Using the Principal Components method (the most commonly used method in practice, since it always gives a solution), the two resulting factor scores separate respondents cleanly: individuals who value the health benefit (negative $F_1$) score low on the cosmetic factor $F_2$ regardless, while cosmetic-oriented respondents score high on $F_2$ — and this factor-based grouping is later shown to match the groups found independently by [[Hierarchical Cluster Analysis|hierarchical cluster analysis]] on the same data, cross-validating both methods.

**Applied paper.** Campo-Arias et al. (*Revista Cubana de Salud Pública*, 2019) apply factor analysis (and internal-consistency/reliability analysis) to the Okasha Suicidality Scale in adolescents — a psychometric-scale-validation use case of exactly the kind Factor Analysis is designed for (confirming that a questionnaire's items load on the intended latent construct).

## See also
[[Factor Analysis - The Orthogonal Factor Model]], [[Principal Component Analysis]], [[Hierarchical Cluster Analysis]], [[Matrix Algebra Foundations for Multivariate Analysis]]
