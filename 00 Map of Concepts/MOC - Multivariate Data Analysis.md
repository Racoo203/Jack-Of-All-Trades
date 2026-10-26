---
subject: Multivariate Data Analysis
type: MOC
course_code: MA2003B
course_name_es: "Aplicación de Métodos Multivariados en Ciencia de Datos"
domain: Machine Learning & AI
level: BSc
status: drafted
confidence: 0
tags:
  - moc
  - exam
  - multivariate-data-analysis
---
## Concept narrative

MA2003B (Tec de Monterrey) is taught as two back-to-back modules by two professors, and the course's own opening slide names the split explicitly: **Módulo I — Relaciones de Interdependencia** (Blanca R. Ruiz Hernández) and **Módulo II — Relaciones de Dependencia** (Rodolfo Fernández de Lara). That split is the organizing idea of the whole subject. In an interdependence analysis no variable is singled out as the one being explained — the goal is to describe the *structure* that a large set of correlated variables has, using nothing but their [[Data Matrix, Mean Vector, and Covariance Matrix|covariance/correlation structure]]. In a dependence analysis one variable (or a categorical grouping) *is* singled out, and the other variables are used to explain or predict it.

**Módulo I** opens with the geometric and probabilistic scaffolding every later technique leans on: the [[Data Matrix, Mean Vector, and Covariance Matrix|data matrix]] and its mean/covariance/correlation summaries, read geometrically through [[Vector Geometry of the Data Matrix|dot products and angles]], and compared through [[Statistical Distance and Mahalanobis Distance|statistical distance]] — Euclidean distance ignores that variables have different variance and are correlated, so it is generalized first to a variance-weighted distance and then, allowing correlation, to the **Mahalanobis distance**. That distance immediately explains why [[Constant Density Contours|constant-density contours]] of correlated data are tilted ellipses rather than circles, and the [[Generalized Variance|generalized variance]] $|S|$ gives a single number for the volume those ellipses enclose. Before any technique can lean on normality, the course teaches how to check it: [[Skewness and Kurtosis|third/fourth-moment shape measures]] feed into [[Graphical and Statistical Tests for Normality|QQ plots and formal normality tests]], and when a variable fails those tests, [[Data Transformations for Normality (Box-Cox and Yeo-Johnson)|Box–Cox/Yeo–Johnson transformations]] (not to be confused with [[Data Scaling and Standardization|scaling]], which changes units but never distribution shape) are the fix. All of this converges on **[[The Multivariate Normal Distribution]]** — the assumption nearly every downstream technique either requires or is judged against — together with the battery of checks in [[Validation of Multivariate Normality]].

With that foundation in place, Módulo I teaches four families of interdependence technique, each answering a different question about the same correlated data matrix: **[[Principal Component Analysis]]** re-expresses $p$ correlated variables as $p$ uncorrelated linear combinations ordered by variance, to *reduce dimensionality*; **[[Factor Analysis - The Orthogonal Factor Model|Factor Analysis]]** (in its estimation half, [[Factor Analysis - Estimation and Rotation]]) instead *explains* the correlations by positing a smaller number of latent common factors; **[[Hierarchical Cluster Analysis]]** and **[[Non-Hierarchical Cluster Analysis (K-Means and K-Medoids)|Non-Hierarchical Cluster Analysis]]** group the *individuals* rather than the variables, using the same distance measures from earlier in the module; and **[[Time Series - Stationarity and Forecast Accuracy|Time Series analysis]]** (continued in [[Time Series - Trend and Seasonal Decomposition]]) treats a single variable observed repeatedly over time as a special interdependence structure (autocorrelation) rather than a cross-section.

**Módulo II** pivots to dependence: **[[Simple Linear Regression and Least Squares]]** and its generalization **[[Multiple Linear Regression]]** model a continuous response as a linear function of predictors, with **[[Model Selection Criteria for Regression]]** (AIC/BIC/HQC, forward/backward/stepwise selection) choosing among competing models and **[[Regression Diagnostics - Outliers and Influential Observations]]** checking whether any single observation is distorting the fit. **[[One-Way ANOVA]]** is the dependence technique for a *categorical* predictor (comparing means across groups), and **[[Confidence and Prediction Intervals in Regression]]** quantifies the uncertainty around a fitted regression's coefficients and its predictions. Finally **[[Linear Discriminant Analysis]]** closes the dependence half exactly where the syllabus places it — "Modelos Discriminantes" — using a *categorical* response the way regression uses a continuous one, and is the natural technique to validate a cluster analysis's groupings after the fact.

Throughout, **[[Matrix Algebra Foundations for Multivariate Analysis]]** is the appendix every technique in both modules quietly assumes: transpose, inverse, determinant, eigenvalues/eigenvectors and positive-definiteness are used without re-derivation from [[Principal Component Analysis|PCA's]] eigen-decomposition of $\Sigma$ onward.

---

## Concept map

### Foundations (shared scaffolding)
- [[Matrix Algebra Foundations for Multivariate Analysis]]
- [[Data Matrix, Mean Vector, and Covariance Matrix]]
- [[Vector Geometry of the Data Matrix]]
- [[Statistical Distance and Mahalanobis Distance]]
- [[Constant Density Contours]]
- [[Generalized Variance]]
- [[Chebyshev's Theorem]]

### Módulo I, Unit 2 — Normality and the Multivariate Normal
- [[Skewness and Kurtosis]]
- [[Graphical and Statistical Tests for Normality]]
- [[Data Transformations for Normality (Box-Cox and Yeo-Johnson)]]
- [[Data Scaling and Standardization]]
- [[The Multivariate Normal Distribution]]
- [[Validation of Multivariate Normality]]

### Módulo I, Unit 3-4 — Variable-reduction techniques
- [[Principal Component Analysis]]
- [[Factor Analysis - The Orthogonal Factor Model]]
- [[Factor Analysis - Estimation and Rotation]]

### Módulo I, Unit 5 — Grouping individuals
- [[Hierarchical Cluster Analysis]]
- [[Non-Hierarchical Cluster Analysis (K-Means and K-Medoids)]]

### Módulo I, Unit 6 — Time series
- [[Time Series - Stationarity and Forecast Accuracy]]
- [[Time Series - Trend and Seasonal Decomposition]]

### Módulo II — Dependence relations
- [[Simple Linear Regression and Least Squares]]
- [[Multiple Linear Regression]]
- [[Model Selection Criteria for Regression]]
- [[Regression Diagnostics - Outliers and Influential Observations]]
- [[One-Way ANOVA]]
- [[Confidence and Prediction Intervals in Regression]]
- [[Linear Discriminant Analysis]]

---

## Key dependency chains

```
[Matrix Algebra Foundations] ─┬─> [Data Matrix, Mean Vector, Covariance Matrix]
                               │         │
                               │         ├─> [Vector Geometry of the Data Matrix]
                               │         │
                               │         └─> [Statistical Distance and Mahalanobis Distance]
                               │                   │
                               │                   ├─> [Constant Density Contours] ─┐
                               │                   │                                │
                               │                   └─> [Generalized Variance]       │
                               │                                                    v
                               └───────────────────────────────────────> [The Multivariate Normal Distribution]
                                                                                     │
                    [Skewness and Kurtosis] ──> [Graphical and Statistical           │
                              │                   Tests for Normality]              │
                              │                          │                          │
                              v                          v                          v
                [Data Transformations for Normality] <───┴──────────> [Validation of Multivariate Normality]
                              │
                              └──> [Data Scaling and Standardization]  (distinct: shape vs. units)

[Matrix Algebra Foundations] ──eigen-decomposition of Σ──> [Principal Component Analysis]
                                                                     │
                                                                     v
                                          [Factor Analysis: The Orthogonal Factor Model]
                                                                     │
                                                                     v
                                          [Factor Analysis: Estimation and Rotation]

[Statistical Distance and Mahalanobis Distance] ──> [Hierarchical Cluster Analysis]
                                                              │
                                                              v
                              [Non-Hierarchical Cluster Analysis (K-Means and K-Medoids)]
                                                              │
                                             validated post hoc by
                                                              v
                                              [Linear Discriminant Analysis]

[Simple Linear Regression and Least Squares] ──> [Multiple Linear Regression] ─┬─> [Model Selection Criteria for Regression]
                                                                                ├─> [Regression Diagnostics: Outliers …]
                                                                                └─> [Confidence and Prediction Intervals in Regression]

[One-Way ANOVA]  (categorical-predictor analogue of regression; shares the residual/F-test machinery)

[Time Series: Stationarity and Forecast Accuracy] ──> [Time Series: Trend and Seasonal Decomposition]
```

---

## Exam focus

High-priority topics (recur across lecture examples, in-class activities, and the applied papers dropped alongside the slides):

- **Mahalanobis distance and quadratic forms.** Computing $d^2=(\mathbf{x}-\boldsymbol\mu)'\Sigma^{-1}(\mathbf{x}-\boldsymbol\mu)$ by hand for a small $p$, and reading off the axes of the associated confidence ellipse from the eigenvalues/eigenvectors of $\Sigma$ — this exact calculation recurs in [[Statistical Distance and Mahalanobis Distance]], [[Constant Density Contours]], [[The Multivariate Normal Distribution]] and [[Principal Component Analysis]].
- **Normality testing, end to end**: compute skewness/kurtosis, build a QQ plot by hand from ranked data and $p_i=(i-0.5)/n$, and know which formal test (Anderson–Darling, Shapiro–Wilk, Kolmogorov–Smirnov/Lilliefors, Ryan–Joiner, Jarque–Bera) is preferred for which sample size. Raúl's own graded "Actividad 1.2" (univariate normality on `cars$speed`) is a direct worked template — see [[Graphical and Statistical Tests for Normality]].
- **PCA by hand for $p=2,3$**: set up $\Sigma\mathbf{a}=\lambda\mathbf{a}$ via Lagrange multipliers, order eigenvalues, write $Y_i=\mathbf{e}_i'\mathbf{X}$, and compute the proportion of variance explained. Know the PCA-vs-standardized-PCA distinction (covariance matrix vs. correlation matrix as input).
- **Factor Analysis assumption checks**: Bartlett's sphericity test and the KMO index, by formula, plus interpreting communality vs. uniqueness and deciding the number of factors (Kaiser's rule, scree plot).
- **Linkage methods in hierarchical clustering**: single/complete/average/centroid/Ward, worked by hand on a small distance matrix (as in the A–B–C–D example), and knowing which linkage is robust to outliers vs. prone to chaining.
- **Model selection criteria** (AIC, BIC, HQC): know the direction of optimization (smaller is better) and which term penalizes model complexity. *(See the open question below — the slide deck's HQC/BIC formula labels look swapped against the standard definitions; resolve this against Raúl's own copy of the slides before treating either formula as exam-ready.)*
- **ANOVA table construction**: SSTr/SSE/TSS, degrees of freedom $k-1$ and $k(n-1)$, and the $F=\text{MSTr}/\text{MSE}$ decision rule — the detergent whiteness example is the lecture's worked template.
- **Regression diagnostics vocabulary**: standardized vs. studentized residuals, leverage (hat matrix diagonal), Cook's distance, and why an influential point need not be an outlier and vice versa.
- **Discriminant Analysis workflow in R**: `lda()` output (prior probabilities, group means, coefficients of linear discriminants, proportion of trace), and the two assumptions (multivariate normality per class, equal covariance matrices across classes) — grounded in Raúl's own course template, `G301_Análisis discriminante.rmd`, built around the `iris` dataset.

Common question types seen across the activities and annotated exercises: "compute X by hand for this small dataset and confirm with R output"; "state and check the assumptions before running technique Y"; "interpret this R output" (eigenanalysis table, `lda()` summary, ANOVA table, `mvn()` output); and "which technique is appropriate for this applied scenario" (the dropped journal articles — PCA for bioprocess monitoring, factor analysis for a psychometric scale, MANOVA for a morphology-vs-altitude study, discriminant analysis for forensic speaker identification — are exactly this question type in the wild).

## Open questions

- [ ] `4. Regresión Multiple - Criterios.pptx` labels its BIC and HQC slides with what look like swapped formulas relative to the standard definitions ($\mathrm{BIC}=k\ln n - 2\ln L$ appears under the "HQC" heading, and a residual-sum-of-squares-based formula appears under "BIC"). The atomic note [[Model Selection Criteria for Regression]] uses the standard textbook formulas and flags this discrepancy inline — check it against your own copy of the slide deck before relying on the course's exact labels in an exam.
- [ ] No lecture slide deck for Discriminant Analysis itself was found in the Resources drop — only the R-markdown practice template (`G301_Análisis discriminante.rmd`, built around `iris`), a comparison table embedded in the Cluster Analysis slides, and one applied paper (forensic speaker identification). [[Linear Discriminant Analysis]] was drafted from canonical theory and grounded wherever the course materials touch it; verify the professor's exact notation/conventions once slides turn up.
- [ ] The academic papers dropped alongside the slides (PCA for antibody fermentation, factor analysis for the Okasha suicidality scale, MANOVA on *Diabrotica* population growth and on Colombian wasp morphology, cluster analysis of smart personal assistants and of VR/AR research trends, a combined cluster+discriminant method for financial efficiency profiles, multiple regression on Ecuadorian agricultural GDP and on bone mineral density) were skimmed for topic/method only, not fully extracted — they are referenced as real-world examples in the relevant atomic notes but are worth a closer read before an exam that draws case-study questions from them.
- [ ] MANOVA (multivariate ANOVA) appears only inside two of the applied papers, never in a lecture slide — no atomic note was created for it since there is no course-taught theory to ground one in yet; flag this as a gap if MANOVA turns out to be examinable.
- [ ] The annotated/graded homework PDFs (`annotated-Actividad...`) were identified by filename and cross-referenced where already transcribed (Actividad 1.2, Actividad 1.5) but not all individually transcribed into note Examples sections — worth a follow-up pass if more worked examples are wanted per note.
