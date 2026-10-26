---
title: "Modular Inverse"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Modular Arithmetic"
level: BSc
status: drafted
confidence: 0
tags: [number-theory, modular-arithmetic, cryptography]
---
## Definition
For $a,n \in \mathbb{Z}$ with $n>0$, $a^{-1} \bmod n$ is an integer $x$ such that
$$
ax \equiv 1 \pmod n.
$$
When it exists, it is unique modulo $n$, and it exists **if and only if** $\gcd(a,n)=1$ (i.e. $a$ is a unit of $\mathbb{Z}/n\mathbb{Z}$ — see [[Group of Units U(n)]]).

## Properties
### Existence iff $\gcd(a,n)=1$
**($\Leftarrow$)** If $\gcd(a,n)=1$, Bézout's identity (see [[Extended Euclidean Algorithm]]) gives integers $x,y$ with $ax+ny=1$. Reducing mod $n$, $ax \equiv 1 \pmod n$, so $x$ is the inverse.

**($\Rightarrow$)** If $ax\equiv 1 \pmod n$ for some $x$, then $ax - 1 = ny$ for some $y\in\mathbb{Z}$, i.e. $ax - ny = 1$. Any common divisor $d$ of $a$ and $n$ divides the left side, hence $d \mid 1$, so $\gcd(a,n)=1$. $\blacksquare$

### Uniqueness modulo $n$
If $ax \equiv 1$ and $ax' \equiv 1 \pmod n$, then $a(x-x') \equiv 0 \pmod n$. Since $\gcd(a,n)=1$, $a$ is cancellable mod $n$ (multiplying by $a^{-1}$), so $x \equiv x' \pmod n$.

### Computation
The standard method is the [[Extended Euclidean Algorithm]] applied to $(a,n)$: back-substitute to write $1 = ax+ny$, and then $a^{-1} \equiv x \pmod n$.

## Examples
- $13^{-1}$ in $\mathbb{Z}_{20}$: $\gcd(13,20)=1$; since $13\cdot 17 = 221 = 220+1 \equiv 1 \pmod{20}$, $13^{-1}\equiv 17 \pmod{20}$.
- $12^{-1}$ in $\mathbb{F}_{13}$: $12 \equiv -1 \pmod{13}$, and $(-1)^{-1}=-1$, so $12^{-1} \equiv 12 \pmod{13}$ — used directly in the doubling-slope computation $\mu = 3x_1^2+c_1 \,\cdot\, (2y_1)^{-1}$ of the [[Elliptic Curve Group Law]].
- In ElGamal decryption (`Actividad_Protocolos_criptográficos.pdf`, Ejercicio 3.1), Alice needs $s^{-1} \bmod p$ where $s=(c_1)^x \bmod p$; with $p=19$, $s=11$, the extended Euclidean algorithm gives $11^{-1} \equiv 7 \pmod{19}$.
- $n-1 \in U(n)$ is always its own inverse, since $(n-1)^2 = n^2-2n+1 \equiv 1 \pmod n$.

## See also
[[Extended Euclidean Algorithm]], [[Linear Congruence]], [[Group of Units U(n)]], [[RSA Cryptosystem]], [[ElGamal Encryption]]
