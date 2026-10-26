---
title: "Euler's Totient Function"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Modular Arithmetic"
level: BSc
status: drafted
confidence: 0
tags: [number-theory, modular-arithmetic, cryptography]
---
## Definition
For $n \in \mathbb{Z}^+$, **Euler's totient function** counts the residues coprime to $n$:
$$
\varphi(n) = \big|\{k \in \{1,\dots,n\} : \gcd(k,n)=1\}\big| = |U(n)|,
$$
where $U(n)$ is the [[Group of Units U(n)]]. In particular $\varphi(p) = p-1$ for prime $p$, since every $1\le k \le p-1$ is coprime to $p$.

## Properties
### Multiplicativity: $\varphi(mn) = \varphi(m)\varphi(n)$ when $\gcd(m,n)=1$
This follows from the ring isomorphism of the [[Chinese Remainder Theorem]], $\mathbb{Z}/mn\mathbb{Z} \cong \mathbb{Z}/m\mathbb{Z}\times\mathbb{Z}/n\mathbb{Z}$, restricted to units: $u \in (\mathbb{Z}/mn\mathbb{Z})^*$ corresponds to a pair $(u \bmod m,\, u\bmod n)$, and $u$ is a unit mod $mn$ iff $u\bmod m$ is a unit mod $m$ **and** $u \bmod n$ is a unit mod $n$ (since $\gcd(u,mn)=1 \iff \gcd(u,m)=1 \wedge \gcd(u,n)=1$ when $\gcd(m,n)=1$). So
$$
(\mathbb{Z}/mn\mathbb{Z})^* \cong (\mathbb{Z}/m\mathbb{Z})^* \times (\mathbb{Z}/n\mathbb{Z})^*,
$$
and taking cardinalities gives $\varphi(mn) = \varphi(m)\varphi(n)$.

### Three-prime case: $\varphi(pqr) = \varphi(p)\varphi(q)\varphi(r) = (p-1)(q-1)(r-1)$
**Proof** (`ActividadRSA.pdf`, Problem 1). Since $p,q,r$ are distinct primes, they are pairwise coprime. Apply multiplicativity twice:
$$
\varphi(pqr) = \varphi(p)\cdot\varphi(qr) = \varphi(p)\cdot\varphi(q)\cdot\varphi(r),
$$
using $\gcd(p,qr)=1$ for the first step and $\gcd(q,r)=1$ for the second. Substituting $\varphi(p)=p-1$, $\varphi(q)=q-1$, $\varphi(r)=r-1$ (each prime) gives $\varphi(pqr)=(p-1)(q-1)(r-1)$. $\blacksquare$

### $\varphi(n)$ is the order of $U(n)$, and hence of the RSA modulus
For $n=pq$ with $p,q$ distinct primes, $\varphi(n) = (p-1)(q-1)$ — this is exactly the modulus used to find the RSA private exponent $d$ (see [[RSA Cryptosystem]]) via $de \equiv 1 \pmod{\varphi(n)}$.

## Examples
- $\varphi(20) = \varphi(4)\varphi(5) = 2\cdot 4 = 8$; indeed $U(20)=\{1,3,7,9,11,13,17,19\}$ has $8$ elements (used in the automorphism problem for $\mathbb{Z}_{20}$, see [[Automorphism]]).
- RSA example (`ActividadRSA.pdf`): $p=61,\ q=53 \Rightarrow \varphi(n) = 60\cdot 52 = 3120$.
- $\varphi(n)$ can be replaced in RSA by the strictly smaller [[Carmichael Function]] $\lambda(n)$, which still satisfies $a^{\lambda(n)}\equiv 1 \pmod n$ for $\gcd(a,n)=1$.

## See also
[[Group of Units U(n)]], [[Chinese Remainder Theorem]], [[Fermat-Euler Theorem]], [[RSA Cryptosystem]], [[Carmichael Function]]
