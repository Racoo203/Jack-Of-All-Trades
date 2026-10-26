---
title: "Extended Euclidean Algorithm"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Modular Arithmetic"
level: BSc
status: drafted
confidence: 0
tags: [number-theory, modular-arithmetic, cryptography, algorithm]
---
## Definition
For $a,b \in \mathbb{Z}$, not both zero, the **extended Euclidean algorithm** computes $\gcd(a,b)$ together with integers $x,y$ (Bézout coefficients) satisfying **Bézout's identity**
$$
ax + by = \gcd(a,b).
$$
It runs the ordinary Euclidean algorithm forward (repeated division) and then substitutes backward to express the final nonzero remainder as an integer combination of $a$ and $b$.

## Properties
### Correctness of the forward pass (Euclidean algorithm)
Repeated division gives a sequence $r_0=a,\, r_1=b,\, r_{i+1} = r_{i-1} \bmod r_i$, stopping when $r_{k+1}=0$; then $\gcd(a,b)=r_k$. This is valid because $\gcd(r_{i-1},r_i) = \gcd(r_i, r_{i-1}\bmod r_i)$: writing $r_{i-1}=q_ir_i+r_{i+1}$, any common divisor of $r_{i-1},r_i$ divides $r_{i+1}$, and any common divisor of $r_i,r_{i+1}$ divides $r_{i-1}$, so the two pairs have the same common divisors, hence the same gcd. Since the remainders strictly decrease, the process terminates.

### Back-substitution produces Bézout's identity
Each step $r_{i+1} = r_{i-1} - q_i r_i$ expresses a remainder as a combination of the two previous ones. Starting from the last nonzero remainder and substituting each $r_{i+1}$ upward in terms of $r_{i-1}, r_i$ eventually rewrites $\gcd(a,b)$ purely in terms of $a=r_0$ and $b=r_1$.

**Worked derivation** (as used to find $d$ with $7d \equiv 1 \pmod{160}$ in [[RSA Cryptosystem]]): solve $7d + 160k = 1$.
$$
160 = 7(22) + 6 \;\Rightarrow\; 6 = 160 - 7(22)
$$
$$
7 = 6(1) + 1 \;\Rightarrow\; 1 = 7 - 6
$$
Substituting the first equation into the second:
$$
1 = 7 - \big(160 - 7(22)\big) = 7(23) - 160(1)
$$
So $x=23,\, y=-1$ is a Bézout pair for $\gcd(7,160)=1$, giving $7(23) \equiv 1 \pmod{160}$, i.e. $d = 23$.

### Existence of a modular inverse
Bézout's identity gives $ax \equiv \gcd(a,n) \pmod n$. When $\gcd(a,n)=1$, this reads $ax \equiv 1 \pmod n$, so $x \bmod n$ is the [[Modular Inverse]] of $a$. This is the mechanism behind every modular-inverse computation in the course (RSA's $d$, ElGamal's $s^{-1}$, the slope denominators $\lambda,\mu$ in the [[Elliptic Curve Group Law]]).

## Examples
- $12^{-1} \bmod 13$: from $13(1) + 12(-1) = 1$, $12^{-1} \equiv -1 \equiv 12 \pmod {13}$ (used in the elliptic-curve doubling worked in `A01722401_Actividad_Criptografía_Elíptica.pdf`).
- $6x \equiv 14 \pmod{20}$: written as $6x - 20y = 14$; the extended Euclidean algorithm on $(20,6)$ gives $20=6(3)+2,\ 6=2(3)+0$, so $\gcd=2$ and (since $2\mid 14$) the congruence has $2$ solutions, $x \equiv 9, 19 \pmod{20}$ (see [[Linear Congruence]]).
- $11x \equiv 16 \pmod{23}$: since $\gcd(11,23)=1$, back-substitution gives $11^{-1}\equiv -2 \equiv 21 \pmod{23}$, so $x \equiv 16 \cdot 21 \equiv 14 \pmod{23}$.

## See also
[[Modular Inverse]], [[Linear Congruence]], [[Congruence Relation]], [[RSA Cryptosystem]]
