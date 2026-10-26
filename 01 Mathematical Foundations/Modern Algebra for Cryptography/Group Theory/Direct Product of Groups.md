---
title: "Direct Product of Groups"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Group Theory"
level: BSc
status: drafted
confidence: 0
tags: [abstract-algebra, group-theory, cryptography]
---
## Definition
Given groups $G$ and $H$, the **(external) direct product** $G\times H$ is the set of pairs $(g,h)$ with $g\in G,\ h\in H$, under the componentwise operation
$$
(g_1,h_1)\cdot(g_2,h_2) = (g_1g_2,\, h_1h_2).
$$
$G\times H$ is a group: closure and associativity hold componentwise, the identity is $(e_G,e_H)$, and $(g,h)^{-1}=(g^{-1},h^{-1})$. Its order is $|G\times H| = |G|\cdot|H|$.

## Properties
### $\mathbb{Z}/n\mathbb{Z} \cong \mathbb{Z}/p\mathbb{Z} \times \mathbb{Z}/q\mathbb{Z}$ for $n=pq$, $p,q$ distinct primes
This is a restatement of the [[Chinese Remainder Theorem]] as a ring (hence additive-group) isomorphism: the map $x \bmod n \mapsto (x\bmod p,\, x \bmod q)$ is a bijection because the system $x\equiv a\pmod p,\ x\equiv b\pmod q$ has a unique solution mod $n$ for every pair $(a,b)$, and it respects both addition and multiplication mod $n$ componentwise (since congruence is compatible with $+,\times$ — see [[Congruence Relation]]).

### $(\mathbb{Z}/n\mathbb{Z})^* \cong (\mathbb{Z}/p\mathbb{Z})^* \times (\mathbb{Z}/q\mathbb{Z})^*$
**Proof** (`ActividadRSA.pdf`, Problem 3). The ring isomorphism above restricts to a group isomorphism on units: $u \bmod n$ is a unit of $\mathbb{Z}/n\mathbb{Z}$ (i.e. $\gcd(u,n)=1$) iff $\gcd(u,p)=1$ **and** $\gcd(u,q)=1$ (since $n=pq$ with $p,q$ distinct primes), i.e. iff $u \bmod p \in (\mathbb{Z}/p\mathbb{Z})^*$ and $u\bmod q \in (\mathbb{Z}/q\mathbb{Z})^*$. So the bijection $u \mapsto (u\bmod p,\, u \bmod q)$ carries $(\mathbb{Z}/n\mathbb{Z})^*$ exactly onto $(\mathbb{Z}/p\mathbb{Z})^*\times(\mathbb{Z}/q\mathbb{Z})^*$, and it preserves multiplication componentwise. $\blacksquare$

This immediately re-derives $\varphi(pq)=\varphi(p)\varphi(q)=(p-1)(q-1)$ by comparing group orders — see [[Euler's Totient Function]].

## Examples
- [[RSA Cryptosystem]] key generation implicitly works inside $(\mathbb{Z}/p\mathbb{Z})^*\times(\mathbb{Z}/q\mathbb{Z})^*$ rather than the (much larger, harder to reason about) group $(\mathbb{Z}/n\mathbb{Z})^*$ directly.
- The [[Carmichael Function]] $\lambda(n) = \mathrm{lcm}(p-1,q-1)$ is the exponent of the group $(\mathbb{Z}/p\mathbb{Z})^*\times(\mathbb{Z}/q\mathbb{Z})^*$ — the smallest $m$ with $x^m=e$ for every element $x$ — which is why it can replace $\varphi(n)=(p-1)(q-1)$ (the group's *order*, not its exponent) in RSA.

## See also
[[Chinese Remainder Theorem]], [[Group of Units U(n)]], [[Euler's Totient Function]], [[RSA Cryptosystem]], [[Carmichael Function]]
