---
title: "Breadth First Search"
domain: "Computer Science & Data Engineering"
course: "Data Structures and Algorithms"
unit: "Search Algorithms"
level: BSc
status: drafted
confidence: 0
tags: [data-structures-algorithms]
---
Input: Graph $G$, Initial vertex $A$.
Output: Dictionary with the distances from $A$ and dictionary with the precedents.

Step 1: Assign a distance $0$ to the origin $A$ and mark the rest of the vertices with distance $\infty$. Assign the predecessor of all vertices as `NULL`. Add $A$ to the visited list $z$.

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
So the distance dictionary and predecessor dictionary look as follows:
```
dist = {
	"A": 0,
	"B": ∞,
	"C": ∞,
	"D": ∞,
	"E": ∞,
	"F": ∞
}
```

```
pred = {
	"A": NULL,
	"B": NULL,
	"C": NULL,
	"D": NULL,
	"E": NULL,
	"F": NULL
}
```
$$
z = [A]
$$
Step 2: While the row is not empty:
- Remove the first vertex $v$ of the row
- For each neighboring vertex $w$ of $v$ that hasn't been visited yet, 
	- Assign `dist[w] = dist[v] + 1`
	- Assign `pred[w] = v`
	- Add $w$ to the end of the visited list.

Step 3: Once the row is empty, return the dictionaries (distance and predecessors).

With $v = A$:
```
dist = {
	"A": 0,
	"B": 1,
	"C": 1,
	"D": ∞,
	"E": ∞,
	"F": ∞
}
```

```
pred = {
	"A": NULL,
	"B": "A",
	"C": "A",
	"D": NULL,
	"E": NULL,
	"F": NULL
}
```
$$
z = [A.B,C]
$$
With $v = B$:
```
dist = {
	"A": 0, # Already visited
	"B": 1,
	"C": 1,
	"D": 2, 
	"E": 2,
	"F": ∞
}
```

```
pred = {
	"A": NULL,
	"B": "A",
	"C": "A",
	"D": "B",
	"E": "B",
	"F": NULL
}
```
$$
z = [A,B,C,D,E]
$$
With $v = C$:
```
dist = {
	"A": 0, # Already visited
	"B": 1,
	"C": 1,
	"D": 2,
	"E": 2,
	"F": 2
}
```

```
pred = {
	"A": NULL,
	"B": "A",
	"C": "A",
	"D": "B",
	"E": "B",
	"F": "C"
}
```