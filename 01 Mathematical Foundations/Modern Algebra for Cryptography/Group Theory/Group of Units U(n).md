---
title: "Group of Units U(n)"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Group Theory"
level: BSc
status: drafted
confidence: 0
tags: [abstract-algebra, group-theory, number-theory, cryptography]
---
## Definition
For $n\in\mathbb{Z}^+$, the **group of units modulo $n$** is
$$
U(n) := \{ a \in \{1,\dots,n-1\} : \gcd(a,n)=1 \},
$$
under multiplication modulo $n$. This is exactly $\left(\mathbb{Z}/n\mathbb{Z}\right)^*$, the set of elements of $\mathbb{Z}/n\mathbb{Z}$ with a [[Modular Inverse]]. Its size is $|U(n)| = \varphi(n)$ ([[Euler's Totient Function]]).

## Properties
### $U(n)$ is a group
*Closure*: if $\gcd(a,n)=\gcd(b,n)=1$ then $\gcd(ab,n)=1$ (no prime dividing $n$ can divide $ab$, since none divides $a$ or $b$), so $ab \bmod n \in U(n)$. *Associativity* is inherited from integer multiplication. *Identity*: $1\in U(n)$. *Inverses*: every $a\in U(n)$ has a [[Modular Inverse]] because $\gcd(a,n)=1$, and that inverse is itself coprime to $n$ (else $a$ wouldn't be invertible), so it lies in $U(n)$.

### A concrete isomorphism-flavored example: $\{5,15,25,35\}$ under multiplication mod $40$
**Worked example** (Ejercicios Módulo I, Problem 3). Check $25$ is the identity: $25\cdot5=125\equiv5$, $25\cdot15=375\equiv15$, $25\cdot25=625\equiv25$, $25\cdot35=875\equiv35 \pmod{40}$ — so $25$ acts as identity on this set, confirming it is a group under multiplication mod $40$ (it is not $U(40)$ itself, since these elements aren't coprime to $40$, but a coset-like copy of $U(8)$). Writing each element as $5u$ for $u\in\{1,3,5,7\}=U(8)$, multiplication mod $40$ of $5u\cdot 5v = 25uv \equiv 5(uv \bmod 8) \pmod{40}$ — one checks the map $5u \mapsto u$ is a bijection to $U(8)$ that respects the operation, so $G \cong U(8)$.

## Examples
- $U(20) = \{1,3,7,9,11,13,17,19\}$, order $\varphi(20)=8$.
- $U(p)$ for prime $p$ is cyclic of order $p-1$ ([[Cyclic Group]]) — the group in which [[Diffie-Hellman Key Exchange]] and [[ElGamal Encryption]] operate, with the [[Discrete Logarithm Problem]] as their hardness assumption.
- $(\mathbb{Z}/n\mathbb{Z})^* \cong (\mathbb{Z}/p\mathbb{Z})^*\times(\mathbb{Z}/q\mathbb{Z})^*$ for $n=pq$ ([[Direct Product of Groups]]) — the structural fact behind [[RSA Cryptosystem]] key generation.

## See also
[[Congruence Relation]], [[Modular Inverse]], [[Euler's Totient Function]], [[Cyclic Group]], [[Discrete Logarithm Problem]]
