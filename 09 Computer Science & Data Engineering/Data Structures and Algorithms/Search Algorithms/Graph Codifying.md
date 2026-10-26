---
title: "Graph Codifying"
domain: "Computer Science & Data Engineering"
course: "Data Structures and Algorithms"
unit: "Search Algorithms"
level: BSc
status: drafted
confidence: 0
tags: [data-structures-algorithms]
---
Given a Graph, we define the adjacent matrix as:
$$
M = [m_{ij}]
$$
such that $$
m_{ij} = \begin{cases}
	1 & \text{if there is an edge connecting vertices i, j} \\
	0 & \text{otherwise} \\	
\end{cases}
$$
Example:
$$
M = \begin{bmatrix}
0 & 1 & 1 & 0 & 0 & 0 \\
1 & 0 & 0 & 1 & 1 & 0 \\
1 & 0 & 0 & 0 & 0 & 1 \\
0 & 1 & 0 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 & 0 & 1 \\
0 & 0 & 1 & 0 & 1 & 0 \\
\end{bmatrix}
$$

We define an adjacent list as the dictionary that assigns each vertex a list that contains all of the axis on which an edge is shared. For the same $M$ adjacent matrix, we have

```
L = {
	"A": ["B", "C"],
	"B": ["A", "D", "E"],
	"C": ["A", "F"],
	"D": ["B"],
	"E": ["B", "F"],
	"F": ["C", "E"]
}
```

