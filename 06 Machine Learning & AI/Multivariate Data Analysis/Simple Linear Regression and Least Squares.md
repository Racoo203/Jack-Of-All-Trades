---
title: "Simple Linear Regression and Least Squares"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo II, Unit 1 - Regresión Lineal Simple"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, regression, dependence-analysis]
---
## Definition
**Regression analysis** determines the "best" functional relationship between a quantitative response $Y$ and one or more predictor variables, so that information about $Y$ can be obtained from the predictors. **Simple linear regression** assumes a straight-line relationship between one predictor $X$ and $Y$. The **probabilistic model** for the population is
$$
Y = \beta_0+\beta_1 X + \varepsilon
$$
with $\varepsilon$ a random error term; the corresponding **estimated model**, fit from a sample, is
$$
\hat y = \hat\beta_0+\hat\beta_1 x
$$

## Properties
### Measures of linear tendency: covariance and correlation
Before fitting a model, the **sample covariance** $s_{xy}=\frac1n\sum_i(x_i-\bar x)(y_i-\bar y)$ and the **sample correlation coefficient** $r=\dfrac{s_{xy}}{\sqrt{s_{xx}s_{yy}}}$ (see [[Data Matrix, Mean Vector, and Covariance Matrix]]) summarize the strength and direction of the linear association between $X$ and $Y$ prior to fitting.

### The least-squares principle
Define the **prediction error (residual)** for observation $i$ as $e_i = y_i - \hat y_i = y_i-(\hat\beta_0+\hat\beta_1 x_i)$. The **least-squares criterion** chooses $\hat\beta_0,\hat\beta_1$ to minimize the sum of squared residuals:
$$
S(\beta_0,\beta_1) = \sum_{i=1}^n \big(y_i-\beta_0-\beta_1 x_i\big)^2
$$
Setting $\partial S/\partial\beta_0=0$ and $\partial S/\partial\beta_1=0$ and solving the resulting **normal equations** gives the closed-form least-squares estimators:
$$
\hat\beta_1 = \frac{\sum_i (x_i-\bar x)(y_i-\bar y)}{\sum_i(x_i-\bar x)^2} = \frac{s_{xy}}{s_{xx}}, \qquad \hat\beta_0 = \bar y - \hat\beta_1\bar x
$$
so the fitted line always passes through the point of means $(\bar x,\bar y)$.

### Coefficient of determination
$$
R^2 = \frac{\text{variation explained by the model}}{\text{total variation}} = 1-\frac{\sum_i e_i^2}{\sum_i (y_i-\bar y)^2} \in [0,1]
$$
the proportion of the total variability in $Y$ accounted for by the fitted line; for simple linear regression, $R^2=r^2$ (the square of the correlation coefficient).

### Assumptions of the linear regression model
Validated through the residuals, as in [[One-Way ANOVA|ANOVA's residual checks]] and detailed further in [[Regression Diagnostics - Outliers and Influential Observations]]: linearity of the relationship, normality of the errors, constant error variance (homoscedasticity), and independence of the errors.

## Examples
**Cotton-dust exposure vs. lung capacity.** A scatterplot of years of occupational exposure to cotton dust (X) against PEFR (peak expiratory flow rate, a lung-capacity measure, Y) for textile workers is used to motivate the need for a formal model — visual inspection of a scatterplot alone is judged insufficient to determine the strength of the relationship, hence the need for a fitted regression.

**Wheat production vs. flour price.** Given paired data on wheat production (tons, $X$) and the price per kilo of flour ($Y$), the exercise asks the student to derive the least-squares regression equation directly from the formulas above — a direct hand computation of $\hat\beta_0,\hat\beta_1$.

## See also
[[Multiple Linear Regression]], [[Confidence and Prediction Intervals in Regression]], [[Data Matrix, Mean Vector, and Covariance Matrix]]
