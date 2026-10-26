---
title: "Elliptic Curve Discrete Logarithm Problem"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Elliptic Curve Cryptography"
level: BSc
status: drafted
confidence: 0
tags: [cryptography, elliptic-curves, number-theory]
---
## Definition
Let $P$ be a point of order $n$ on an [[Elliptic Curve over a Finite Field|elliptic curve]] $E$ over $\mathbb{F}_p$, generating the cyclic subgroup $\langle P \rangle$ under the [[Elliptic Curve Group Law]]. The **elliptic curve discrete logarithm problem (ECDLP)** is: given $P$ and $Q = kP$, find $k \in \{0,1,\dots,n-1\}$.

## Properties
### Structural identity with the Discrete Logarithm Problem
ECDLP is the additive-group analogue of the [[Discrete Logarithm Problem]] in $U(p)$: "generator $g$, power $g^k$" becomes "base point $P$, multiple $kP$". Every algebraic argument used for [[Diffie-Hellman Key Exchange]] and [[ElGamal Encryption]] carries over verbatim with this dictionary, which is exactly why [[ECDH]] and [[ECDSA]] exist as direct transplants of Diffie–Hellman and RSA-style signing.

### Why it is (believed) harder than DLP in $U(p)$ at comparable size
The best known general attacks on ECDLP (Pollard's rho, giving $O(\sqrt n)$ time) match the best *generic* group attacks on DLP in $U(p)$, but $U(p)$ additionally admits **index calculus**, a sub-exponential attack that exploits the specific arithmetic structure of $\mathbb{Z}/p\mathbb{Z}$. No analogous sub-exponential attack is known for well-chosen elliptic curves, so an elliptic-curve group of order $n$ offers roughly the same security as $U(p)$ with $p$ far larger — the reason a $256$-bit elliptic-curve key is considered comparable in strength to a $3072$-bit RSA/DH key.

## Examples
- Recovering Alice's or Bob's private scalar $a$ or $b$ from the public points $A=aG,\,B=bG$ in [[ECDH]] is exactly an instance of ECDLP.
- Forging an [[ECDSA]] signature without the private key $d$ reduces to solving ECDLP for the public key $Q_A = dG$.

## See also
[[Discrete Logarithm Problem]], [[Elliptic Curve Group Law]], [[Cyclic Group]], [[ECDH]], [[ECDSA]]
