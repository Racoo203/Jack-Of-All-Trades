---
title: "Order of a Permutation"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Group Theory"
level: BSc
status: drafted
confidence: 0
tags: [abstract-algebra, group-theory, cryptography]
---
## Definition
For a permutation $\alpha \in S_n$ written in disjoint-cycle form $\alpha = c_1 c_2 \cdots c_r$ with cycle lengths $\ell_1,\dots,\ell_r$, the **order** of $\alpha$ (see [[Order of an Element]]) is
$$
|\alpha| = \mathrm{lcm}(\ell_1,\dots,\ell_r).
$$

## Properties
### Why the order is the lcm of the cycle lengths
Disjoint cycles commute (see [[Permutation and Cycle Notation]]), so $\alpha^k = c_1^k c_2^k \cdots c_r^k$, and this equals the identity iff **every** $c_i^k$ is separately the identity (disjoint cycles act on disjoint elements, so they can only jointly fix everything by each fixing its own elements). A cycle of length $\ell_i$ satisfies $c_i^k = e$ iff $\ell_i \mid k$. So $\alpha^k=e$ iff $k$ is a common multiple of all $\ell_i$, and the smallest such $k$ is $\mathrm{lcm}(\ell_1,\dots,\ell_r)$.

### Computing large powers via the order
Once $|\alpha|=m$ is known, any power reduces mod $m$: $\alpha^k = \alpha^{k \bmod m}$, exactly as in [[Fermat-Euler Theorem]] for $U(n)$.

**Worked example** (Tarea II Gran Final, Problem 7). $\alpha=(1\,4\,5\,2\,3)$ is a single $5$-cycle, so $|\alpha|=5$. To compute $\alpha^{99}$, reduce $99 \equiv 4 \pmod 5$, so $\alpha^{99}=\alpha^4$. Squaring successively:
$$
\alpha = (1\,4\,5\,2\,3), \quad \alpha^2=(1\,5\,3\,4\,2), \quad \alpha^3=(1\,2\,4\,3\,5), \quad \alpha^4=(1\,3\,2\,5\,4).
$$
So $\alpha^{99}=\alpha^4=(1\,3\,2\,5\,4)$.

## Examples
- $\beta_1=(1\,4)(2)(3)$ has order $\mathrm{lcm}(2,1,1)=2$.
- $\beta_3 = (1\,4\,7\,6\,2)(3\,6\,5)$ once rewritten in disjoint form (Ejercicios Módulo I, Problem 13) has order equal to the lcm of the resulting disjoint cycle lengths.
- Finding the least $n$ such that $S_n$ has an element of order $30$ (see [[Symmetric Group]]) is a direct application: distribute the prime factors $2,3,5$ of $30$ into disjoint cycles of those lengths.

## See also
[[Permutation and Cycle Notation]], [[Symmetric Group]], [[Order of an Element]]
