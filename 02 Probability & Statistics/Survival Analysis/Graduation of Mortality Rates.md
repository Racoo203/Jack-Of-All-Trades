---
title: "Graduation of Mortality Rates"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 8 - Graduation"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, graduation, smoothing, standard-tables]
---
## Definition
Crude mortality rates (estimated directly from data, e.g. via [[Binomial Model for Mortality|Binomial]] or [[Poisson Model for Mortality|Poisson]] models) are rarely used directly in practice. **Graduation** is the process of smoothing crude rates $\hat\mu_x$ into a smooth progression $\mu_x^o$ across age. A **standard table** is a life table computed over a large volume of data and published by an official source (e.g. ONS, an insurer, or via the UK's Continuous Mortality Investigation, CMI); graduation is often assessed by comparison against one.

## Properties
### Why graduate
- Large investigations support the view that $\mu_x$ should vary smoothly with age.
- An estimate at age $x$ carries information about ages $x\pm1$; smoothing borrows strength from adjacent ages.
- Jumps in mortality with age are hard to justify substantively.
- Smoothing reduces sampling error (though it cannot remove bias).
- Graduated rates should always be compared against standard tables.

### Desirable features
Smoothness vs. adherence to data (a trade-off), and suitability (accurate estimates — neither systematically over- nor under-estimating mortality). Both **overgraduation** (too smooth, ignoring real data structure) and **undergraduation** (too rough, not smoothing enough) are failure modes.

### Method 1: Graduation using a parametric model
Assume $\mu_x$ follows a parametric form, e.g. [[Gompertz' Law|Gompertz]] ($\mu_x=Bc^x$), Makeham ($\mu_x=A+Bc^x$), or more generally $\mu_x = \text{polynomial}_1(x) + \exp(\text{polynomial}_2(x))$ (also Lee–Carter and other models). Under the Poisson model (see [[Poisson Model for Mortality]]), $P(D_x=d_x) = \dfrac{(E_x^C\mu_x)^{d_x}\exp(-E_x^C\mu_x)}{d_x!}$; writing $\mu_x=f(\alpha_1,\dots,\alpha_{r+s},x)$, the likelihood (ignoring the constant $d_x!$) is
$$
\prod_{\text{all ages }x} f(\vec\alpha,x)^{d_x}\exp\left(-f(\vec\alpha,x)E_x^C\right)
$$
maximised numerically for $\hat\alpha_1,\dots,\hat\alpha_{r+s}$. General process: select a graduation formula, estimate its parameters, compute graduated rates $\mu_x^o$, and test for fitness (see [[Statistical Tests for Graduation]]).

### Method 2: Graduation by reference to a standard table
Let $\mu_x^s$ be the standard-table rate. Choose a simple **link function** $f$ so that $\mu_x^o = f(\mu_x^s)$, e.g. $\mu_x^o = a+b\mu_x^s$, $(a+bx)\mu_x^s$, $\mu_x^s+k$, or $(\mu_x^s)^k$. The relationship is usually identified by plotting crude rates against the standard table's rates. General process: select a standard table, select a link function $f$, estimate its parameters (e.g. $a,b$), compute $\mu_x^o$, and test for fitness.

### Method 3: Graduation by spline functions
Splines are piecewise polynomials of a given degree, continuous at specified knots, of the general form $\mu_x^o = \alpha_0+\alpha_1 x + \sum_{j=1}^n \beta_j\phi_j(x)$. Options include lowess, B-splines, and P-splines.

### Comparing the three methods
- **Parametric formula**: fully automated, smooth, performs well with abundant data but poorly with sparse data; hard to fit all ages with one curve; caution needed extrapolating to extreme ages.
- **Standard table reference**: relies on choosing a suitable table; simple link functions make fitting easy; works even with small amounts of data; smoothness inherited from the (usually smooth) standard table.
- **Splines**: high flexibility via choice of spline type/knots; requires more tuning; smoothness depends on the complexity chosen; caution needed extrapolating.

## See also
[[Statistical Tests for Graduation]], [[Gompertz' Law]], [[Poisson Model for Mortality]], [[Binomial Model for Mortality]]
