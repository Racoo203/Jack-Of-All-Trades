---
title: "Non-Hierarchical Cluster Analysis (K-Means and K-Medoids)"
domain: "Machine Learning & AI"
course: "Multivariate Data Analysis"
unit: "Módulo I, Unit 5 - Análisis de Conglomerados"
level: BSc
status: drafted
confidence: 0
tags: [multivariate-data-analysis, cluster-analysis, interdependence-analysis]
---
## Definition
**Non-hierarchical ("partitioning") cluster methods** start from the raw data scores (not from a precomputed distance matrix, unlike [[Hierarchical Cluster Analysis]]) and produce groupings that are **not nested**: they are independent partitions directly into $k$ clusters, rather than a hierarchy. They are recommended when the researcher does not need the hierarchical structure itself, only the final grouping of individuals and each group's characteristics — and they require the number of clusters $k$ to be decided in advance (often taken from a prior hierarchical run). Non-hierarchical methods are used only to group individuals, never variables.

## Properties
### The general algorithm ("moving averages" / centroid-based)
Every non-hierarchical algorithm begins from some initial centroid or grouping (which can itself come from a hierarchical method) and iterates: compute the distance from every point to each current centroid/seed, assign each point to its nearest one, recompute centroids from the new assignments, and repeat until no point changes cluster. Different algorithms vary only in *how* the initial partition and the sequencing of updates are chosen:
- **Sequential threshold.** Clusters are formed one at a time; individuals already classified are not reconsidered for a new cluster once assigned.
- **Parallel threshold.** All cluster centroids are updated simultaneously; the process stops once no individual changes cluster.
- **Optimizing partition.** Individuals are reassigned iteratively so as to optimize some overall criterion (rather than simple nearest-centroid assignment).

### K-means
Each individual belongs to whichever of $k$ cluster centroids is closest (in Euclidean distance, by default). Centroids are recomputed as the mean of the points currently assigned to them, and the process repeats to convergence.

### K-medoids (Partitioning Around Medoids, PAM)
A **medoid** is defined as the object *within* a cluster whose average dissimilarity to all other objects in that same cluster is minimal — i.e. an actual observed data point located most centrally within the group, unlike a k-means centroid (which is an arithmetic average and need not correspond to any real observation). The **Voronoi iteration** method:
1. Select $k$ initial medoids.
2. While the average dissimilarity keeps decreasing: within each cluster, designate as the new medoid the point that minimizes the sum of within-cluster distances; then reassign every point to the cluster of its nearest medoid (using the updated medoids from the previous step).

K-medoids is generally preferred over K-means when the data contains outliers or when a "typical" real observation (rather than an averaged, possibly non-representative point) is wanted as the cluster's representative.

## Examples
A small PAM walk-through: with $k=2$ initial medoids $c_1=(3,4)$ and $c_2=(7,4)$ (using Manhattan/city-block distance rather than Euclidean), the algorithm checks whether reassigning the medoid role to a candidate alternative point improves the total within-cluster dissimilarity; in the worked instance, swapping $c_2$ for a nearby candidate point does not improve the objective, so the original medoids are retained.

## See also
[[Hierarchical Cluster Analysis]], [[Statistical Distance and Mahalanobis Distance]], [[Data Scaling and Standardization]]
