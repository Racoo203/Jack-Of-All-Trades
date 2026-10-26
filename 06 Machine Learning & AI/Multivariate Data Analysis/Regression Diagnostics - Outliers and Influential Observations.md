---
title: "Regression Diagnostics - Outliers and Influential Observations"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo II, Unit 4 - Criterios de Selección de Modelos"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, regression, dependence-analysis, diagnostics]
---
## Definition
After fitting a [[Multiple Linear Regression|multiple regression]] model, its residuals ($e_i=y_i-\hat y_i$) must be examined to (a) verify the model's assumptions and (b) detect individual observations that are unusual or that distort the fit. Two distinct concepts are involved and are easy to conflate:
- An **outlier** is an observation whose *response* value is far from what the model predicts (large residual) — it need not affect the fitted model much.
- An **influential observation** substantially changes the fitted model when removed — it need not have a large residual, and need not be an outlier or have high leverage on its own, though in practice an influential point is usually one or the other.

## Properties
### Standardized and studentized residuals
Assuming residuals are approximately normal, they can be standardized and any exceeding $3$ in absolute value flagged as atypical (R: `rstudent(residuos)`, "extreme" studentization). **Limitation:** if an outlier is influential enough to pull the fitted line toward itself, its own residual can shrink and go undetected by simple standardization — a genuinely important outlier can "hide" this way. The practical fix is **extreme (deleted) studentization**: refit the model with the $i$-th observation removed, then measure how much $\hat{\boldsymbol\beta}$ changes as a result, rather than relying on the in-sample residual alone.

### Leverage (the hat matrix)
The diagonal of the **hat matrix** (from $\hat{\mathbf{y}}=\mathbf{H}\mathbf{y}$, $\mathbf{H}=\mathbf{X}(\mathbf{X}'\mathbf{X})^{-1}\mathbf{X}'$) gives each observation's relative distance from the centroid of the predictor space — its **leverage**. R: `hatvalues(modelo)`. High leverage means an observation's predictor values are unusual (far from the bulk of the $X$'s), independent of whether its response value fits the model well.

### Cook's distance
Measures how much *all* fitted values change when the $i$-th observation is deleted — combining, in a single number, both the magnitude of the residual and the degree of leverage. R: `cooks.distance(modelo)`. A large Cook's distance signals a strongly influential point.

### Relationship among outliers, leverage, and influence
Being an outlier or having high leverage does **not**, by itself, imply an observation is influential; however, if an observation *is* influential, it is usually either an outlier, of high leverage, or both. So Cook's distance (which folds in both residual size and leverage) is the more direct diagnostic for influence specifically, while standardized residuals and leverage separately diagnose the two contributing factors.

## Examples
Continuing the shear-strength ("Al corte") multiple-regression example from [[Multiple Linear Regression]] and [[Model Selection Criteria for Regression]], the course's own workflow explicitly sequences: fit the model $\to$ examine standardized/studentized residuals for outliers $\to$ examine `hatvalues()` for leverage $\to$ compute `cooks.distance()` to flag influential points $\to$ verify the four regression assumptions $\to$ refit if needed — the same iterative "fit, diagnose, refine" loop referenced in [[Model Selection Criteria for Regression]].

## See also
[[Multiple Linear Regression]], [[Model Selection Criteria for Regression]], [[Confidence and Prediction Intervals in Regression]], [[Matrix Algebra Foundations for Multivariate Analysis]]
