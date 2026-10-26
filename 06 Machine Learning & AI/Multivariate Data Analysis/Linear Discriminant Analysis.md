---
title: "Linear Discriminant Analysis"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo II, Unit 6 - Modelos Discriminantes"
level: BSc
status: seeding
confidence: 0
tags: [multivariate-data-analysis, discriminant-analysis, dependence-analysis, classification]
---
<!-- UNVERIFIED: no dedicated lecture slide deck for Discriminant Analysis was found in the Resources drop, even though the course's own opening slide ("0-Introduccion.pdf") explicitly lists "Modelos Discriminantes" under Módulo II. This note is drafted from canonical LDA theory and grounded wherever the course materials do touch the topic: the R-markdown practice template `G301_Análisis discriminante.rmd` (built around the `iris` dataset), the Discriminant-vs-Cluster comparison table embedded in the Cluster Analysis slides (see [[Hierarchical Cluster Analysis]]), and one applied paper. Verify the professor's exact notation and any course-specific conventions once a slide deck turns up, then re-flag status to `drafted`. -->

## Definition
**Linear Discriminant Analysis (LDA)** finds a linear combination of $p$ continuous predictor variables that best separates two or more pre-defined, categorical classes — the resulting combination is a **discriminant function**, usable as a classifier for new observations. Unlike [[Hierarchical Cluster Analysis|Cluster Analysis]] (which discovers groups with no pre-existing labels), Discriminant Analysis starts from a classification that is *already known* (a categorical dependent variable) and asks whether — and how — a set of continuous independent variables can reproduce or predict it; it is a **dependence** technique, not an interdependence one.

**Assumptions:** the predictor variables are (approximately) multivariate normal within each class ([[The Multivariate Normal Distribution]], checked per class via [[Validation of Multivariate Normality]]); and the covariance matrices of the predictors are equal across classes (**homogeneity of covariance matrices**, formally $H_0:\Sigma_1=\Sigma_2=\cdots=\Sigma_G$ vs. $H_a:$ at least two differ — tested, e.g., with Box's M test).

## Properties
### The linear discriminant function
For $G$ classes and $p$ predictors, the maximum number of *useful* discriminant functions is $\min(G-1,\,p)$ — e.g. with $3$ classes and $4$ predictors, at most $\min(2,4)=2$ discriminant functions are fit. Each discriminant function is a linear combination
$$
LDA_k = w_{k1}X_1+w_{k2}X_2+\cdots+w_{kp}X_p
$$
with coefficients (weights) chosen to maximize the separation between classes relative to the variation within classes — the same "between vs. within variance" logic as [[One-Way ANOVA]], but now optimizing over a linear combination of several predictors simultaneously rather than testing a single one. R: `library(MASS); lda(Species ~ ., data = iris)`.

### Reading an `lda()` fit
An `lda()` object reports: **prior probabilities of group membership** (each class's proportion in the training data, or a user-specified prior); **group means** (each predictor's mean within each class); **coefficients of linear discriminants** (the weights $w_{kj}$ defining each discriminant function); and **proportion of trace** (the percentage of between-class separation captured by each discriminant function, analogous to [[Principal Component Analysis|PCA's]] proportion of variance explained).

### Classifying new observations
`predict()` on a fitted `lda` object returns three components for each observation: **class** (the predicted group); **posterior** (the posterior probability of belonging to each class); and **x** (the observation's score on each linear discriminant function). Classification quality is summarized with a **confusion (contingency) table** of predicted vs. actual class, from which the **misclassification rate** (percentage of observations classified incorrectly) is computed.

### Comparison with Cluster Analysis (from the course's own slides)
| | Discriminant Analysis | Cluster Analysis |
|---|---|---|
| Starting point | A classification is already defined by a categorical dependent variable | Each individual starts as its own group; no pre-existing labels |
| Objective | Test for significant differences between the pre-defined groups | Classify individuals into homogeneous groups |
| Independent variables | Quantitative, continuous | Quantitative, continuous |
| Relationship type | Dependence | Interdependence |

Because of this relationship, **Discriminant Analysis is the course's own recommended way to validate a [[Hierarchical Cluster Analysis|cluster analysis's]] groupings** after the fact — see the electric-utilities and toothpaste worked examples in [[Hierarchical Cluster Analysis]] and [[Factor Analysis - Estimation and Rotation]], where the cluster-derived and factor-derived groupings are checked for agreement.

## Examples
**The `iris` practice template (`G301_Análisis discriminante.rmd`, "Análisis Discriminante G301").** The course's own R-markdown assignment builds an LDA classifier for the classic `iris` dataset: 150 observations of 3 species (setosa, versicolor, virginica; 50 each), using 4 numeric predictors (`Sepal.Length`, `Sepal.Width`, `Petal.Length`, `Petal.Width`) to predict `Species`. The template reports two illustrative discriminant functions,
$$
LDA_1 = 0.829\,\text{Sepal.Length}+1.534\,\text{Sepal.Width}-2.201\,\text{Petal.Length}-2.810\,\text{Petal.Width}
$$
$$
LDA_2 = 0.024\,\text{Sepal.Length}+2.165\,\text{Sepal.Width}-0.932\,\text{Petal.Length}+2.839\,\text{Petal.Width}
$$
(at most $\min(3-1,4)=2$ useful functions, matching the theory above), and structures the full workflow: visualize the data by species, fit `lda()`, interpret prior probabilities/group means/coefficients/proportion of trace, predict class membership and posterior probabilities, visualize the discriminant scores by species, build the confusion table and compute the misclassification rate, and finally validate the two assumptions — multivariate normality per species (via `library(MVN)`) and homogeneity of the three species' covariance matrices (Box's M test, $H_0:$ Σ_setosa = Σ_versicolor = Σ_virginica).

**Applied paper.** Cicres (*Síntesis Tecnológica*, 2007) applies discriminant analysis to a set of phonetic-acoustic parameters of filled pauses to identify individual speakers in forensic phonetics — a real-world instance of the same "continuous predictors, categorical class label" LDA setup, in a domain (forensic voice identification) quite different from the course's own toothpaste/utilities examples.

## See also
[[Hierarchical Cluster Analysis]], [[One-Way ANOVA]], [[The Multivariate Normal Distribution]], [[Validation of Multivariate Normality]], [[Factor Analysis - Estimation and Rotation]]
