---
title: "Mapper Filter Functions"
domain: "Mathematical Foundations"
course: "Geometry and Topology for Data Science"
unit: "Mapper and Applications"
level: BSc
status: drafted
confidence: 0
tags: [tda, mapper]
---
## Definition
A **filter function** (or **lens**) is the map $f:X\to\mathbb R^d$ that the [[Mapper Algorithm]] uses to project a dataset before covering and clustering it. The choice of filter determines what kind of structure the resulting Mapper graph can reveal.

## Properties
### Density filter
Assigns to each point a value reflecting the local concentration of data around it, via kernel density estimation (e.g. a Gaussian kernel) or a nearest-neighbor count within a fixed radius. High values indicate densely populated regions; low values indicate sparse or outlier regions. Useful for highlighting clusters and their relative population.

### Eccentricity filter
A family of functions built from a point's average or maximum distance to the rest of the dataset, without needing to first identify a "center." For $1\le p<\infty$ and $x,y\in X$,
$$
E_p(x) = \left( \frac{\sum_{y\in X} d(x,y)^p}{N} \right)^{1/p}, \qquad E_\infty(x) = \lim_{p\to\infty} E_p(x) = \sup_{y\in X} d(x,y).
$$
Eccentricity identifies points far from the "bulk" of the data without reference to a fixed center point.

### PCA filter
Principal Component Analysis projects the data onto its directions of maximal variance. As a Mapper filter, the pipeline is: (1) standardize variables, (2) compute the covariance matrix, (3) compute its eigenvalues/eigenvectors to identify principal components, (4) build a feature vector selecting which components to keep, (5) transform the data using the chosen components' weights. In Python, `sklearn.decomposition.PCA` implements this.

### UMAP filter
UMAP (Uniform Manifold Approximation and Projection) is a non-linear dimensionality-reduction technique that builds a connectivity graph between nearby points in the original space (using ideas from [[Metric Space|metric spaces]] and [[Simplicial Complex|simplicial complexes]]) and then projects that graph to a lower dimension, aiming to preserve both local and global structure. Unlike PCA, UMAP can capture non-linear relationships, which makes it useful as a Mapper filter on high-dimensional or non-linearly-structured data.

## Examples
On a shared dataset (the football-statistics project referenced in [[Mapper Algorithm]]): the density filter tended to dominate visually over PCA when the two were combined (its coloring correlated strongly with player performance, darker = lower performance), while UMAP produced a more heterogeneous, information-rich coloring than either density or eccentricity alone, making UMAP+density the combination judged most interpretable for that dataset.

## See also
[[Mapper Algorithm]], [[Distance and Similarity Measures in Data Science]]
