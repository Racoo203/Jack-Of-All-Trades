---
title: "Hierarchical Cluster Analysis"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 5 - Análisis de Conglomerados"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, cluster-analysis, interdependence-analysis]
---
## Definition
**Cluster analysis** groups a set of $q$ individuals (or, less commonly, variables) measured on $k$ variables into subsets of similar elements, based purely on a [[Statistical Distance and Mahalanobis Distance|distance or similarity measure]] between them — it is a **descriptive, atheoretical, non-inferential** technique (no statistical inference is drawn about a population; it is fundamentally exploratory, based on geometric criteria) that groups by *proximity*, not by any pre-existing label.

**Hierarchical methods** produce a nested sequence of partitions, visualized as a **dendrogram**: groups formed at one level are always unions of groups from the previous level, so no two clusters at the same level overlap.
- **Agglomerative** ("bottom-up"): starts with each individual as its own cluster and successively merges the closest pair.
- **Divisive** ("top-down"): starts with all individuals in one cluster and successively splits, maximizing the separation between the resulting subgroups; used with categorical variables and for a smaller number of subjects.

(Contrast with [[Non-Hierarchical Cluster Analysis (K-Means and K-Medoids)|non-hierarchical methods]], which produce a single, non-nested partition directly.)

## Properties
### Distance/association measures
For individuals, the relevant measures are dissimilarities (distances): Euclidean $d(\mathbf{x},\mathbf{y})=\sqrt{(\mathbf{x}-\mathbf{y})'(\mathbf{x}-\mathbf{y})}$ (sensitive to units, inflated by correlated variables); standardized Euclidean/statistical distance $d(\mathbf{x},\mathbf{y})=\sqrt{(\mathbf{x}-\mathbf{y})'V^{-1}(\mathbf{x}-\mathbf{y})}$ ($V$ diagonal, fixes units but not correlation); Mahalanobis $d(\mathbf{x},\mathbf{y})=\sqrt{(\mathbf{x}-\mathbf{y})'\Sigma^{-1}(\mathbf{x}-\mathbf{y})}$ (corrects for correlation too — using this distance for clustering is equivalent to clustering with Euclidean distance on the [[Principal Component Analysis|principal components]]); also Minkowski distance, the Canberra metric, and the Czekanowski coefficient (neither of the latter two requires pre-computed descriptive statistics). For variables, association is measured by the cosine of the angle between them (see [[Vector Geometry of the Data Matrix]]) or the correlation coefficient. Euclidean distance is the most widely used precisely because it needs no prior descriptive computation; when variables are on very different scales, standardization is recommended first (see [[Data Scaling and Standardization]]).

### The agglomerative algorithm
1. Start with $N$ clusters (one per individual) and an $N\times N$ symmetric distance/similarity matrix $D=\{d_{ij}\}$.
2. Find the closest (most similar) pair of clusters.
3. Merge them into a new cluster labeled $(UV)$; update $D$ by deleting the rows/columns for $U,V$ and inserting a new row/column giving the distance from $(UV)$ to every remaining cluster.
4. Repeat steps 2–3 a total of $N-1$ times, until all individuals are in one cluster.

The rule for computing the distance from a merged cluster to an individual (or another cluster) is exactly what distinguishes the linkage methods below.

### Linkage methods
Let cluster $A=\{A_1,\dots,A_m\}$, $B=\{B_1,\dots,B_n\}$.
- **Single linkage (nearest neighbor).** $d(A,B)=\min\{d(A_i,B_j)\}$. Tends to form elongated, "sausage-shaped" clusters (chaining); very sensitive to outliers, which can create a spurious chain effect linking otherwise-separate clusters.
- **Complete linkage (farthest neighbor).** $d(A,B)=\max\{d(A_i,B_j)\}$. Produces more spherical, compact clusters; eliminates the chaining effect (distances between clusters grow larger) but is still sensitive to outliers.
- **Average linkage.** $d(A,B)=\frac{1}{mn}\sum_{i,j}d(A_i,B_j)$ (average over all cross-pairs). Produces more robust clusters, with smaller and more similar within-cluster variances; one of the most commonly used methods.
- **Centroid linkage.** $d(A,B)=d(\bar{\mathbf{x}}_A,\bar{\mathbf{x}}_B)$ (distance between the two clusters' centroids). Very robust, reduces outlier influence.
- **Within-groups linkage** (weighted average). A variant of average linkage where, hypothetically merging two clusters, all resulting within-cluster pairwise distances are considered, choosing the merge that minimizes the average within-cluster distance.
- **Median (weighted centroid) linkage.** A variant of centroid linkage where the new centroid is computed without weighting by cluster size — so merging a large cluster (e.g. 10 members) with a small one (2 members) does not let the large cluster dominate the new centroid's position as much as ordinary centroid linkage would; considers the number of *clusters* merged, not the number of individuals.
- **Ward's method (minimum-variance / minimum increase in inertia).** Merging any two clusters increases within-cluster variance; Ward's method computes, for every candidate merge, the resulting increase in the total sum of squared distances of points to their cluster's mean, and merges the pair producing the smallest increase. Produces homogeneous clusters of similar size.

### Worked algorithm (single linkage, by hand)
Given a $4\times4$ dissimilarity matrix for objects $A,B,C,D$: find the global minimum distance, merge that pair, recompute the distance from the merged pair to every remaining object as the *minimum* of the two original distances (for single linkage), and repeat until one cluster remains — this produces the dendrogram directly, and the final number of clusters is chosen afterward by cutting the dendrogram at the desired height (see Examples below).

### Choosing the number of clusters
Determining the number of final groups is inherently subjective ("an art," left to the analyst's judgment) — the standard heuristic is to look for the largest "jumps" in merge distance on the dendrogram. A common workflow explores the dendrogram first, decides on a cluster count, then re-runs the algorithm targeting that count directly. Cluster solutions are typically cross-validated against another method — [[Linear Discriminant Analysis]] or [[Factor Analysis - The Orthogonal Factor Model|Factor Analysis]] — rather than trusted on their own.

## Examples
**A–B–C–D toy example (single linkage).** Distance matrix: $d(A,B)=9$, $d(A,C)=4$, $d(A,D)=7$, $d(B,C)=5$, $d(B,D)=3$, $d(C,D)=11$. Minimum is $d(B,D)=3$: merge $B,D$; recompute (single-linkage minimum) $d(A,\{BD\})=\min(9,7)=7$, $d(C,\{BD\})=\min(5,11)=5$. Next minimum is $d(A,C)=4$: merge $A,C$. Finally $d(\{AC\},\{BD\})=\min(7,5)=5$: all four merge. Cutting for two clusters gives $\{A,C\}$ and $\{B,D\}$; cutting for three gives $\{B,D\}$, $\{A\}$, $\{C\}$.

**22 electric utility companies example.** Eight financial/operational indicators (return on assets, cost per KW, load factor, peak demand, sales, % nuclear, fuel cost, etc.) are measured for 22 U.S. utility companies (data on very different scales, so standardized first). Clustering into 6 groups with single linkage gives close between-group distances (hard to justify the cut point); complete linkage gives more separated, easier-to-choose groups; average/centroid linkage on this data happens to reproduce the same grouping as complete linkage. In every case, the resulting groups are recommended for validation via [[Linear Discriminant Analysis]] or Factor Analysis, following the comparison in the properties above.

**Comparison table (from the course slides).**

| | Discriminant Analysis | Cluster Analysis |
|---|---|---|
| Starting point | Classification already defined by a categorical dependent variable | Each individual starts as its own group |
| Objective | Test for significant differences between pre-defined groups | Classify individuals into homogeneous groups |
| Independent variables | Quantitative | Quantitative |
| Relationship | Dependence | Interdependence |

| | Factor Analysis | Cluster Analysis |
|---|---|---|
| Objective | Find underlying variables depending on the original ones | Classify subjects into homogeneous groups |
| Reduces | Number of variables | Number of subjects |
| Basis | Correlations between variables | Distances between subjects |
| Assumptions | Restrictive (interval scale, correlation, normality) | Less restrictive (no linearity required, allows categorical variables) |

**Applied papers.** Knote et al. (HICSS 2019) cluster smart personal assistants empirically by feature set; Cipresso et al. (*Frontiers in Psychology* 2018) apply network and cluster analysis to map the VR/AR research literature; Fontalvo et al. (*Información Tecnológica* 2018) combine cluster analysis with discriminant analysis to profile the financial efficiency of exporting firms — a direct real-world instance of the cluster-then-validate-with-discriminant workflow described above.

## See also
[[Statistical Distance and Mahalanobis Distance]], [[Non-Hierarchical Cluster Analysis (K-Means and K-Medoids)]], [[Data Scaling and Standardization]], [[Principal Component Analysis]], [[Factor Analysis - The Orthogonal Factor Model]], [[Linear Discriminant Analysis]]
