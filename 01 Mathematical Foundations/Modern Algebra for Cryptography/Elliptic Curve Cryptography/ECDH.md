---
title: "ECDH"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Elliptic Curve Cryptography"
level: BSc
status: drafted
confidence: 0
tags: [cryptography, elliptic-curves, number-theory]
---
## Definition
**Elliptic Curve Diffie–Hellman (ECDH)** is [[Diffie-Hellman Key Exchange]] transported to the point group of an [[Elliptic Curve over a Finite Field|elliptic curve]] $E$ over $\mathbb{F}_p$ via the [[Elliptic Curve Group Law]].

**Public parameters**: the curve $E$, a base point $G \in E$ (of known order $n$).

**Protocol**:
1. Alice picks private $a$, publishes $A=aG$.
2. Bob picks private $b$, publishes $B=bG$.
3. Alice computes $S = aB$; Bob computes $S = bA$.

Both reach the same point: $S = a(bG) = (ab)G = b(aG)$.

## Properties
### Correctness
Scalar multiplication distributes exactly like exponentiation, since $kP$ means "$P$ added to itself $k$ times" and repeated addition composes: $a(bG) = (ab)G = b(aG)$, using that integer multiplication is commutative — the identical argument to [[Diffie-Hellman Key Exchange]]'s correctness proof, with $g^k \leftrightarrow kP$.

### Security rests on the ECDLP
An eavesdropper observing $E,G,A,B$ but not $a,b$ would need to solve the [[Elliptic Curve Discrete Logarithm Problem]] (recover $a$ from $A=aG$) to compute $S=abG$ — no known algorithm does this faster than generic square-root-time attacks for well-chosen curves.

## Examples
**Worked example** (`ECDH.pdf`): $E:y^2=x^3+x+1 \pmod{17}$, base point $G=(9,5)$, $a=7,\ b=11$. Compute:
$$
A=7G, \qquad B=11G, \qquad S = aB = bA,
$$
using the [[Elliptic Curve Group Law]] (doubling and adding via the binary expansions of $7$ and $11$), then verify $aB=bA$.

- A second instance uses $E:y^2=x^3+2x+3 \pmod{97}$, $G=(17,10)$, $a=45,\ b=72$.
- `TareaModulo3-1.pdf`, Problem 2 works the same protocol on $E:y^2=x^3+x+1 \pmod{23}$ with $G=(6,4),\ a=5,\ b=8$, giving public keys $A=5G,\ B=8G$ and shared secret $S=aB=bA$.

## See also
[[Diffie-Hellman Key Exchange]], [[Elliptic Curve Group Law]], [[Elliptic Curve Discrete Logarithm Problem]], [[Elliptic Curve over a Finite Field]]
