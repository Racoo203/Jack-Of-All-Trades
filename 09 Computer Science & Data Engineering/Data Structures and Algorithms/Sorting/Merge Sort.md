---
title: "Merge Sort"
domain: "Computer Science & Data Engineering"
course: "Data Structures and Algorithms"
unit: "Sorting"
level: BSc
status: drafted
confidence: 0
tags: [data-structures-algorithms]
---
- Step 1: Divide the list in half until having sublists of only one element
- Step 2: Combine the sublists following this algorithm:
	- Step 2.1: Point to the first element of both lists
	- Step 2.2: Choose the minimum of these elements.
	- Step 2.3: Point to the next element of the sublist of the previously chosen element.
	- Step 2.4: Apply steps 2.2 and 2.3 until all elements are merged.

Example:
1. $L=[7,3,5,2,6,4,8,1]$
2. $L=[7 \vert 3 \vert 5 \vert 2 \vert 6 \vert 4 \vert 8 \vert 1]$
3. $L=[3, 7 \vert 2, 5 \vert 4, 6 \vert 1, 8]$
4. $L=[3, 7 \vert 2, 5 \vert 4, 6 \vert 1, 8]$
5. $L=[2,3,5,7 \vert 1,4,6,8]$
6. $L=[1,2,3,4,5,6,7,8]$

Complexity: $n \log n$
