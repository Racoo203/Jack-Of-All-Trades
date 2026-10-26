---
title: "Permutation and Cycle Notation"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Group Theory"
level: BSc
status: drafted
confidence: 0
tags: [abstract-algebra, group-theory, cryptography]
---
## Definition
A **permutation** of a finite set $\{1,\dots,n\}$ is a bijection $\alpha: \{1,\dots,n\}\to\{1,\dots,n\}$. A **cycle** $(a_1\, a_2\, \cdots\, a_k)$ denotes the permutation sending $a_1\mapsto a_2 \mapsto \cdots \mapsto a_k \mapsto a_1$ and fixing everything else; $k$ is the **length** of the cycle. Two cycles are **disjoint** if they share no elements. Composition of permutations is applied right-to-left (apply the rightmost cycle first), the convention used throughout this course.

## Properties
### Every permutation decomposes into disjoint cycles
Any permutation of a finite set can be written as a product of disjoint cycles, unique up to the order in which the (commuting) disjoint cycles are listed. This is because following the orbit of any element under repeated application of $\alpha$ must eventually return to the start (finiteness), tracing out one cycle; removing that orbit and repeating on what remains partitions the whole set into disjoint cycles.

### Disjoint cycles commute
If $\sigma,\tau$ are disjoint cycles, then for any element $x$, at most one of $\sigma,\tau$ moves $x$, so applying them in either order gives the same result: $\sigma\tau = \tau\sigma$.

### Combining overlapping cycles into disjoint form
**Worked example** (Tarea II Gran Final, Problem 7). Let $\alpha = (1\,2\,3)(1\,4\,5)$ (these two 3-cycles are *not* disjoint — both move $1$). Tracing the orbit of each element, applying the rightmost cycle first:
$$
1 \xrightarrow{(145)} 4 \xrightarrow{(123)} 4, \quad 4\xrightarrow{(145)}5\xrightarrow{(123)}5, \quad 5\xrightarrow{(145)}1\xrightarrow{(123)}2, \quad 2\xrightarrow{(145)}2\xrightarrow{(123)}3, \quad 3\xrightarrow{(145)}3\xrightarrow{(123)}1.
$$
So $1\to4\to5\to2\to3\to1$, giving the disjoint-cycle form $\alpha = (1\,4\,5\,2\,3)$, a single $5$-cycle.

## Examples
- $\alpha_1 = (1\,2\,3\,5)(4\,1\,3)$ and similar composite-cycle expressions (Ejercicios Módulo I, Problem 12) are simplified into disjoint form exactly as above, by tracing orbits.
- Once in disjoint form, a cycle of length $k$ has [[Order of an Element|order]] $k$ (it takes $k$ applications to return every element to itself), which is the basis for computing the [[Order of a Permutation]] of a product of disjoint cycles.

## See also
[[Symmetric Group]], [[Order of a Permutation]], [[Group (Definition)]]
