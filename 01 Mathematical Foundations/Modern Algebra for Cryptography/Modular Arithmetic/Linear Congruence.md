---
title: "Linear Congruence"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Modular Arithmetic"
level: BSc
status: drafted
confidence: 0
tags: [number-theory, modular-arithmetic, cryptography]
---
## Definition
A **linear congruence** is an equation of the form
$$
ax \equiv b \pmod n
$$
in the unknown $x$, with $a,b,n$ given integers, $n>0$. It is equivalent to the linear Diophantine equation $ax - ny = b$ for some $y \in \mathbb{Z}$.

## Properties
### Solvability condition
**Claim.** $ax \equiv b \pmod n$ has a solution if and only if $d := \gcd(a,n)$ divides $b$. When solvable, there are exactly $d$ solutions modulo $n$, congruent modulo $n/d$.

**Proof.** The congruence is solvable iff $ax - ny = b$ has an integer solution. By Bézout's identity (see [[Extended Euclidean Algorithm]]), the set of integer combinations $\{ax-ny : x,y\in\mathbb{Z}\}$ equals the set of multiples of $d=\gcd(a,n)$. Hence a solution exists iff $d \mid b$.

For the count: write $a=da', n=dn'$ with $\gcd(a',n')=1$. If $x_0$ is one solution, then $x_0 + n'$ is also a solution, since $a(x_0+n') = ax_0 + a n' = ax_0 + d a' n' \equiv ax_0 \equiv b \pmod n$ (using $n = dn'$). Iterating, $x_0, x_0+n', x_0+2n', \dots, x_0+(d-1)n'$ are $d$ pairwise-incongruent solutions mod $n$, and no others exist because cancelling the common factor $d$ from $a'dx \equiv b \pmod{dn'}$ forces $x$ to be determined mod $n'$. $\blacksquare$

### The unique-solution case
When $\gcd(a,n)=1$, $a$ has a [[Modular Inverse]] $a^{-1} \bmod n$, and the unique solution is simply $x \equiv a^{-1}b \pmod n$.

## Examples
- $5x \equiv 3 \pmod{20}$: $\gcd(5,20)=5$, and $5 \nmid 3$, so **no solution** exists.
- $3x \equiv 5 \pmod{20}$: $\gcd(3,20)=1$, so a unique solution exists; $3^{-1}\equiv 7 \pmod{20}$ (since $3\cdot 7=21\equiv1$), giving $x \equiv 7\cdot 5 \equiv 35 \equiv 15 \pmod{20}$.
- $6x \equiv 14 \pmod{20}$ (Actividad I): $\gcd(6,20)=2$ and $2\mid 14$, so there are $2$ solutions. Solving $6x-20y=14$ via the extended Euclidean algorithm on $(20,6)$ gives $x \equiv 19 \pmod{20}$ as one root; adding $n/d = 10$ gives the second, $x\equiv 9 \pmod{20}$.
- $11x \equiv 16 \pmod{23}$: $\gcd(11,23)=1$, unique solution $x \equiv 14 \pmod{23}$ via $11^{-1}\equiv 21 \pmod{23}$.

## See also
[[Modular Inverse]], [[Extended Euclidean Algorithm]], [[Congruence Relation]], [[Chinese Remainder Theorem]]
