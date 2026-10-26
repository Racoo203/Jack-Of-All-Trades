---
title: "Multiple Linear Regression"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo II, Unit 3 - Regresión Lineal Múltiple"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, regression, dependence-analysis]
---
## Definition
**Multiple linear regression** generalizes [[Simple Linear Regression and Least Squares|simple linear regression]] to $p-1$ predictors. The theoretical (population) model is
$$
Y = \beta_0+\beta_1X_1+\beta_2X_2+\cdots+\beta_{p-1}X_{p-1}+\varepsilon
$$
and the model estimated from a sample of $n$ observations is $\hat y_i = \hat\beta_0+\hat\beta_1x_{i1}+\cdots+\hat\beta_{p-1}x_{i,p-1}$, fit in R with `lm(y ~ x1 + x2 + ...)`.

## Properties
### Least-squares estimation
As in the simple case, the **prediction error/residual** for observation $i$ is $e_i=y_i-\hat y_i$, and the **least-squares criterion** minimizes $\sum_i e_i^2$ over $\hat\beta_0,\dots,\hat\beta_{p-1}$ simultaneously — in matrix form, with design matrix $\mathbf{X}$ (a column of $1$'s plus the $p-1$ predictor columns) and response vector $\mathbf{y}$, $\hat{\boldsymbol\beta}=(\mathbf{X}'\mathbf{X})^{-1}\mathbf{X}'\mathbf{y}$ (see [[Matrix Algebra Foundations for Multivariate Analysis]] for the matrix inverse this requires).

### Conditions/assumptions
Checked primarily through the residuals: linearity, independence of errors, homoscedasticity (constant error variance across the range of fitted values), and normality of the errors — the same four conditions as simple linear regression, now checked jointly across all predictors.

### Iterative model-building workflow
A typical workflow in R: fit `A = lm(y ~ x1+x2+...)`; examine pairwise correlations among predictors; assess the fitted model's coefficients and significance; identify non-significant predictors and remove them; refit and repeat. E.g. starting from `y~x1,x2,x3,x4,x5,x6`, finding $x_4$ non-significant, refitting as `y~x1,x3,x4,x5,x6` (a typo/inconsistency in the source slide's own worked trace — the point illustrated is the *iterative remove-and-refit* process, not the exact variable list), and settling on `y~x1,x3,x5,x6`. See [[Model Selection Criteria for Regression]] for the formal criteria (rather than ad hoc significance-trimming) used to compare candidate models systematically, and [[Regression Diagnostics - Outliers and Influential Observations]] for verifying the fitted model afterward.

## Examples
**Shear strength experiment.** An experiment measures the impact of force, power, temperature, and time on shear strength (resistencia al corte) across 30 runs (a designed experiment with repeated center points), asking which combination of these four predictors best explains shear strength — a direct multiple-regression model-selection exercise, continued in [[Model Selection Criteria for Regression]] and [[Regression Diagnostics - Outliers and Influential Observations]] (which reuse the same "Al corte" dataset for diagnostics).

**Applied papers.** Quinde-Rosales et al. (*Dom. Cien.* 2018) apply multiple regression to model investment and financing for Ecuador's agricultural sector against macroeconomic predictors; Ferniza Garza's orthopedics thesis fits a multiple regression model relating bone mineral density to hip radiograph measurements — both are real-world instances of the same "several quantitative predictors, one continuous response" setup as the course's own shear-strength example.

## See also
[[Simple Linear Regression and Least Squares]], [[Model Selection Criteria for Regression]], [[Regression Diagnostics - Outliers and Influential Observations]], [[Confidence and Prediction Intervals in Regression]], [[Matrix Algebra Foundations for Multivariate Analysis]]
