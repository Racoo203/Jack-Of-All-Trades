---
title: "Model Selection Criteria for Regression"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo II, Unit 4 - Criterios de Selección de Modelos"
level: BSc
status: seeding
confidence: 0
tags: [multivariate-data-analysis, regression, dependence-analysis, model-selection]
---
## Definition
When several candidate sets of predictors are plausible for a [[Multiple Linear Regression|multiple regression]] model, **predictor-selection procedures** and **information criteria** choose among them systematically, rather than by ad hoc trimming of non-significant coefficients.

**Predictor-selection procedures** (iterative, re-fitting the model at each step):
- **Forward selection.** Start with no predictors; at each step add the predictor that most improves the model; stop when no addition helps significantly.
- **Backward elimination.** Start with all predictors; at each step remove the least useful one; stop when no removal is harmless.
- **Stepwise (mixed).** Alternates forward and backward steps, allowing a predictor added earlier to be dropped later if it becomes redundant once other predictors are added.

**Information criteria** are goodness-of-fit *comparison* measures between several already-fitted models — not hypothesis tests — used to rank candidate models (typically within a stepwise search).

## Properties
### Akaike Information Criterion (AIC)
$$
\text{AIC} = 2k - 2\ln(L)
$$
$k$ = number of parameters in the model, $\ln(L)$ = log-likelihood of the fitted model. Describes the trade-off between bias and variance (accuracy vs. complexity); **the model with the smallest AIC is preferred**; AIC is asymptotically efficient. R: `step(modelo, direction="both", trace=1)`.

### Bayesian Information Criterion (BIC) and the Hannan–Quinn Criterion (HQC)
Both add a complexity penalty that also depends on sample size $n$, and (like AIC) **the smaller value is preferred**:
$$
\text{BIC} = k\ln(n) - 2\ln(L), \qquad \text{HQC} = 2k\ln(\ln n) - 2\ln(L)
$$
BIC penalizes the number of parameters more heavily than AIC for large $n$ (favoring more parsimonious models with fewer predictors and/or a better fit); HQC uses a lighter, slower-growing penalty ($\ln\ln n$ grows much more slowly than $\ln n$) and, unlike BIC, is **not** asymptotically efficient. Both AIC and BIC are based on the likelihood function; a related but distinct family of criteria (e.g. Mallows' $C_p$-style measures) is instead based on the residual sum of squares.

<!-- UNVERIFIED: check against `4. Regresión Multiple - Criterios.pptx`. The slide titled "Criterio Shwarz o de información Bayesiano (BIC)" gives the formula "HQC = kln(n) − 2ln(L)" underneath it, and the following slide titled "Criterio de información Hannan-Quinn (HQC)" gives the formula "BIC = kln(SCE) + 2kln(n)" (SCE = suma de cuadrados del error, i.e. residual sum of squares) underneath *that* heading — the two slide titles and their formulas appear swapped relative to each other and relative to the standard definitions used above. The BIC and HQC formulas in this note follow the standard statistical literature (matching what the AIC slide's own style of formula would predict), not the exact labels printed in the deck. Confirm against your own copy of the slides, and note the deck's alternate SCE-based formula for what it calls "BIC" — $k\ln(\text{SCE})+2k\ln(n)$ — as a possible course-specific convention worth checking with the professor. -->

### Choosing among AIC, BIC, and HQC
Since BIC's penalty grows fastest with $n$, it tends to select the most parsimonious (fewest-predictor) model among the three when sample size is large; AIC tends to retain more predictors than BIC; HQC sits between them, favoring fit more than BIC but complexity-penalizing more than AIC as $n$ grows. In practice, all three are typically computed together and compared, with a model preferred by all three considered the strongest candidate.

## Examples
Building on [[Multiple Linear Regression]]'s shear-strength ("Al corte") experiment, the model-optimization workflow is explicitly framed as **iterative**: residuals from an initial fit are examined, the model is adjusted (predictors added/removed per the selection procedures above, or per AIC/BIC/HQC), residuals are re-examined, and the cycle repeats until reaching what is judged an optimal model — with [[Regression Diagnostics - Outliers and Influential Observations]] supplying the residual-based checks that drive each iteration.

## See also
[[Multiple Linear Regression]], [[Regression Diagnostics - Outliers and Influential Observations]], [[Simple Linear Regression and Least Squares]]
