---
title: "Factor Analysis - The Orthogonal Factor Model"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 4 - Análisis Factorial"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, dimensionality-reduction, interdependence-analysis]
---
## Definition
**Factor Analysis** assumes that the correlations among a set of $p$ observed variables are explained by a smaller number $m<p$ of unobserved, underlying **latent variables** or **common factors**. Unlike [[Principal Component Analysis]] (which re-expresses the variables as new linear combinations with no assumption about *why* they correlate), Factor Analysis posits a generative structure: the original variables *depend on* the factors, with different weights per variable.

**Uses:** understand the structure underlying a set of variables (e.g. describing "intelligence" via latent traits behind a battery of test scores); reveal emergent patterns; build/validate a questionnaire that measures underlying latent constructs; reduce a large variable set to a manageable number while retaining as much information as possible.

**Assumptions.** The main assumption is that the original variables are related and therefore expressible via common underlying factors — in practice, requiring pairwise correlations of at least roughly $0.3$. Homoscedasticity can be relaxed (though its violation reduces the observed correlations); normality is needed only if significance tests on the factors are used (rarely done); the relationship among variables must be linear; and variables must show *some* but not *excessive* correlation (too little correlation gives factors no shared structure to explain; too much makes individual variables redundant rather than jointly explained by a factor).

## Properties
### The orthogonal factor model, in matrix form
The observable vector $\mathbf{X}$ (mean $\boldsymbol\mu$, covariance $\Sigma$) is modeled as linearly dependent on $m$ unobservable **common factors** $F_1,\dots,F_m$ ($m<p$) plus $p$ **specific factors** (errors) $\varepsilon_1,\dots,\varepsilon_p$:
$$
X_1-\mu_1 = \ell_{11}F_1+\cdots+\ell_{1m}F_m+\varepsilon_1,\ \ldots,\ X_p-\mu_p = \ell_{p1}F_1+\cdots+\ell_{pm}F_m+\varepsilon_p \qquad\Longleftrightarrow\qquad \mathbf{X}-\boldsymbol\mu = \mathbf{L}\mathbf{F}+\boldsymbol\varepsilon
$$
$\mathbf{L}_{(p\times m)}$ is the **matrix of factor loadings**; $\ell_{ik}$ is the loading of variable $i$ on factor $k$. The **orthogonal factor model** additionally assumes
$$
E(\mathbf{F})=\mathbf{0},\quad \operatorname{Cov}(\mathbf{F})=E(\mathbf{FF}')=\mathbf{I}, \quad E(\boldsymbol\varepsilon)=\mathbf{0}, \quad \operatorname{Cov}(\boldsymbol\varepsilon)=E(\boldsymbol\varepsilon\boldsymbol\varepsilon')=\boldsymbol\Psi=\operatorname{diag}(\psi_1,\dots,\psi_p), \quad \operatorname{Cov}(\boldsymbol\varepsilon,\mathbf{F})=\mathbf{0}
$$
i.e. factors are uncorrelated with unit variance, specific factors are uncorrelated with each other and with the common factors.

### Covariance structure implied by the model
$$
\Sigma = \operatorname{Cov}(\mathbf{X}) = E\big[(\mathbf{LF}+\boldsymbol\varepsilon)(\mathbf{LF}+\boldsymbol\varepsilon)'\big] = \mathbf{L}E(\mathbf{FF}')\mathbf{L}' + E(\boldsymbol\varepsilon\boldsymbol\varepsilon') = \mathbf{LL}'+\boldsymbol\Psi
$$
so the total variance of $X$ splits into variance **explained by the factors** ($\mathbf{LL}'$, the *communality*) and variance **not explained by the factors** ($\boldsymbol\Psi$, the *uniqueness/specificity*). Similarly $\operatorname{Cov}(\mathbf{X},\mathbf{F})=E[(\mathbf{X}-\boldsymbol\mu)\mathbf{F}']=E[(\mathbf{LF}+\boldsymbol\varepsilon)\mathbf{F}']=\mathbf{L}E(\mathbf{FF}')=\mathbf{L}$, so **$\operatorname{Cov}(X_i,F_j)=\ell_{ij}$: a loading is literally the covariance between a variable and a factor** — the larger $|\ell_{ij}|$, the more important variable $i$ is to factor $j$.

### Communality and uniqueness
$$
\operatorname{Var}(X_i) = \sigma_{ii} = \ell_{i1}^2+\cdots+\ell_{im}^2+\psi_i = h_i^2+\psi_i
$$
$h_i^2=\ell_{i1}^2+\cdots+\ell_{im}^2$ is the **communality** of variable $i$ (variance shared with the common factors); $\psi_i$ is its **specific variance/uniqueness**. Also $\operatorname{Cov}(X_i,X_k)=\ell_{i1}\ell_{k1}+\cdots+\ell_{im}\ell_{km}$ — the covariance between two variables is entirely explained by their shared loadings on the common factors.

### Rotational (non-)uniqueness of the loading matrix
For any orthogonal matrix $\mathbf{T}$ ($\mathbf{TT}'=\mathbf{T}'\mathbf{T}=\mathbf{I}$), setting $\mathbf{L}^*=\mathbf{LT}$ and $\mathbf{F}^*=\mathbf{T}'\mathbf{F}$: $E(\mathbf{F}^*)=\mathbf{T}'E(\mathbf{F})=\mathbf{0}$, $\operatorname{Cov}(\mathbf{F}^*)=\mathbf{T}'\operatorname{Cov}(\mathbf{F})\mathbf{T}=\mathbf{T}'\mathbf{T}=\mathbf{I}$, and $\Sigma=\mathbf{LL}'+\boldsymbol\Psi=\mathbf{LTT}'\mathbf{L}'+\boldsymbol\Psi=(\mathbf{L}^*)(\mathbf{L}^*)'+\boldsymbol\Psi$: **$\mathbf{L}$ and $\mathbf{L}^*=\mathbf{LT}$ both satisfy the model equally well and generate the same $\Sigma$** — the loading matrix is not identified up to rotation. This ambiguity is not a flaw; it is exploited deliberately: since any rotation is equally valid statistically, one can choose the rotation that is easiest to *interpret* (see [[Factor Analysis - Estimation and Rotation]]).

### Exploratory vs. confirmatory factor analysis
**Exploratory Factor Analysis (EFA)** discovers the "underlying" structure of a large variable set with no strong prior theory — factors and their number emerge from the data. **Confirmatory Factor Analysis (CFA)** instead tests whether a pre-specified theoretical structure (number and identity of factors, which variables load on which) is consistent with the observed correlations.

## Examples
**Academic performance example.** Ten university course grades ($x_1$ Algebra, ..., $x_{10}$ Econometrics) are hypothesized to be explained by three latent factors: $F_1$ = abstraction ability (loads on Algebra, Calculus, Statistics, Actuarial), $F_2$ = memory (Commercial Law, Labor Law, Actuarial), $F_3$ = analytical ability (Financial Accounting, Econometrics, Actuarial) — illustrating that a single observed variable (Actuarial) can load meaningfully on more than one factor.

**Language proficiency example.** A single factor "command of the language" is measured through four observed skills: Reading, Listening, Speaking, Writing — the simplest possible case, $m=1$.

## See also
[[Factor Analysis - Estimation and Rotation]], [[Principal Component Analysis]], [[Hierarchical Cluster Analysis]], [[Matrix Algebra Foundations for Multivariate Analysis]]
