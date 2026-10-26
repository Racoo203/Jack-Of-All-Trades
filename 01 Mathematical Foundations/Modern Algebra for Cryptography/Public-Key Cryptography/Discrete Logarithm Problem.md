---
title: "Discrete Logarithm Problem"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Public-Key Cryptography"
level: BSc
status: drafted
confidence: 0
tags: [cryptography, number-theory, group-theory]
---
## Definition
Let $G$ be a finite [[Cyclic Group]] with generator $g$. The **discrete logarithm problem (DLP)** is: given $g$ and $h = g^k \in G$, find $k$. Forward exponentiation $g \mapsto g^k$ is fast (repeated squaring), but no efficient (polynomial-time) algorithm is known for the inverse when $G$ is chosen well — this asymmetry is the hardness assumption underlying [[Diffie-Hellman Key Exchange]] and [[ElGamal Encryption]].

## Properties
### The instance used in this course: $G = U(p)$
For a prime $p$ and generator $g$ of $U(p)$ (see [[Group of Units U(n)]], [[Cyclic Group]]), the DLP is: given $p,g,g^k \bmod p$, recover $k$. Its presumed hardness (no known sub-exponential classical algorithm for well-chosen $p$) is exactly what lets Alice and Bob exchange public values $g^a \bmod p,\ g^b \bmod p$ over an open channel without exposing $a,b$.

### Why forward exponentiation is easy: repeated squaring
Computing $g^k \bmod p$ naively takes $k-1$ multiplications, but writing $k$ in binary and repeatedly squaring reduces this to $O(\log k)$ modular multiplications — exactly the computations carried out by hand in this course's Diffie–Hellman and ElGamal exercises (e.g. $5^{15} \bmod 23 = 5\cdot(5^2)^7 = 5\cdot2^7 \bmod 23$ in `Actividad_Protocolos_criptográficos.pdf`).

### The elliptic-curve analogue
Replacing $U(p)$ by the point group of an [[Elliptic Curve over a Finite Field|elliptic curve]] gives the [[Elliptic Curve Discrete Logarithm Problem]]: given a base point $P$ and $Q=kP$, find $k$. No sub-exponential algorithm is known for ECDLP either, and — unlike DLP in $U(p)$ — no sub-exponential *index-calculus*-style attack is known at all, which is why elliptic-curve keys can be much shorter than RSA/DH keys for comparable security.

## Examples
- Solving DLP is exactly what an eavesdropper ("Eve", in the course's notation) would need to break [[Diffie-Hellman Key Exchange]] after observing $p,g,g^a,g^b$.
- [[RSA Cryptosystem]] does **not** rely on DLP — its hardness assumption is integer factorization of $n=pq$ — which is why RSA and Diffie-Hellman/ElGamal are considered independent (though comparably strong, for well-chosen parameters) hardness assumptions.

## See also
[[Diffie-Hellman Key Exchange]], [[ElGamal Encryption]], [[Group of Units U(n)]], [[Cyclic Group]], [[Elliptic Curve Discrete Logarithm Problem]]
