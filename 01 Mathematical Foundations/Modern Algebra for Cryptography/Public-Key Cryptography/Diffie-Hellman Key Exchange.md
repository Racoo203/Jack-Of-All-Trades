---
title: "Diffie-Hellman Key Exchange"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Public-Key Cryptography"
level: BSc
status: drafted
confidence: 0
tags: [cryptography, number-theory, group-theory]
---
## Definition
**Public parameters**: a prime $p$ and a generator (or high-order element) $g$ of $U(p)$.

**Protocol**:
1. Alice picks a private secret $a$ and publishes $A = g^a \bmod p$.
2. Bob picks a private secret $b$ and publishes $B = g^b \bmod p$.
3. Alice computes the shared secret $S_A = B^a \bmod p$; Bob computes $S_B = A^b \bmod p$.

Both arrive at the same value: $S_A = (g^b)^a = g^{ab} = (g^a)^b = S_B \pmod p$.

## Properties
### Correctness
Immediate from the laws of exponents in a group: $(g^b)^a = g^{ba} = g^{ab} = (g^a)^b$, using commutativity of integer multiplication in the exponent (this holds in **any** group, not just Abelian ones, because the exponent arithmetic happens in $\mathbb{Z}$, which is commutative).

### Security rests on the Discrete Logarithm Problem
An eavesdropper who observes $p,g,A,B$ but not $a,b$ would need to solve the [[Discrete Logarithm Problem]] (recover $a$ from $A=g^a$, or $b$ from $B=g^b$) to compute $S=g^{ab}$ directly — no more efficient attack than solving DLP (or the related Computational/Decisional Diffie–Hellman problems) is known for well-chosen $p,g$.

## Examples
**Worked example** (`Actividad_Protocolos_criptográficos.pdf`, Ejercicio 1.1): $p=23,\ g=5,\ a=6,\ b=15$.
$$
A = 5^6 \equiv (5^2)^3 \equiv 2^3 \equiv 8 \pmod{23}, \qquad B = 5^{15} \equiv 5\cdot(5^2)^7 \equiv 5\cdot 2^7 \equiv 19 \pmod{23}.
$$
$$
S_A = B^a = 19^6 \equiv 2^{12} \equiv 4\cdot9^2 \equiv 2 \pmod{23}, \qquad S_B = A^b = 8^{15} \equiv 2^{45} \equiv 2 \pmod{23}.
$$
$S_A = S_B = 2$, the shared secret.

- Larger instance in the same activity: $p=97,\ g=12,\ a=21,\ b=55 \Rightarrow A=27,\ B=8,\ S_A=S_B=79 \pmod{97}$.
- [[ECDH]] is the identical protocol with the multiplicative group $U(p)$ replaced by the point group of an elliptic curve and $g^k$ replaced by scalar multiplication $kG$.

## See also
[[Discrete Logarithm Problem]], [[Group of Units U(n)]], [[Congruence Relation]], [[ECDH]], [[ElGamal Encryption]]
