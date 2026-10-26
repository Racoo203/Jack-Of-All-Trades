---
title: "Binary Search"
domain: "Computer Science & Data Engineering"
course: "Data Structures and Algorithms"
unit: "Search Algorithms"
level: BSc
status: drafted
confidence: 0
tags: [data-structures-algorithms]
---
Assume that we have an ordered list L and an element a. To determine if the a is in the list, we can follow this algorithm:
1. Identify the entry of the mid-point of the list.
2. If a is equal to this entry, then the search ends. If a is less than that entry, repeat step 1 with the sublist from the first element to the midpoint. Otherwise, if a is greater than the midpoint, repeat with the sublist that goes from the mid-point element to the last element.

Complexity: O(log(n))