---
title: "Linked List"
domain: "Computer Science & Data Engineering"
course: "Data Structures and Algorithms"
unit: "Data Structures"
level: BSc
status: drafted
confidence: 0
tags: [data-structures-algorithms]
---
A linked list is comprised of an integer that has the size of the list, a pointer pointing to the first node of the list, and an pointer pointing to the last element of the list. Each node is comprised of a float containing the value to store, and a pointer pointing to the next node. Their operations are as follows:
1. Data appending:
	1. Adding to the end: $\mathbb{O}(1)$ 
	2. Adding to the start: $\mathbb{O}(1)$ 
	3. Adding arbitrarily: $\mathbb{O}(n)$ 
2. Data removal:
	1. Removing to the end: $\mathbb{O}(n)$ 
	2. Removing to the start: $\mathbb{O}(1)$ 
	3. Removing arbitrarily: $\mathbb{O}(n)$ 
3. Data manipulation:
	1. Get a value: $\mathbb{O}(n)$ 
	2. Modify a value: $\mathbb{O}(n)$ 
	3. Search a value: $\mathbb{O}(n)$ 