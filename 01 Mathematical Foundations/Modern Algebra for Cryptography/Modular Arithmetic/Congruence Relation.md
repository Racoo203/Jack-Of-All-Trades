---
title: "Congruence Relation"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Modular Arithmetic"
level: BSc
status: drafted
confidence: 0
tags: [number-theory, modular-arithmetic, cryptography]
---
## Definition
For $a,b \in \mathbb{Z}$ and a fixed modulus $n \in \mathbb{Z}^+$, $a$ is **congruent to** $b$ **modulo** $n$, written
$$
a \equiv b \pmod n,
$$
if $n \mid (a-b)$, i.e. $a-b = nk$ for some $k \in \mathbb{Z}$. Equivalently, $a$ and $b$ leave the same remainder when divided by $n$.

## Properties
### Congruence mod $n$ is an equivalence relation
- **Reflexive**: $a - a = 0 = n\cdot 0$, so $a \equiv a \pmod n$.
- **Symmetric**: if $a\equiv b \pmod n$ then $a-b=nk$, so $b-a = n(-k)$, giving $b\equiv a \pmod n$.
- **Transitive**: if $a\equiv b \pmod n$ and $b \equiv c \pmod n$, then $a-b=nk_1$ and $b-c=nk_2$ for some $k_1,k_2\in\mathbb{Z}$. Adding, $a-c = n(k_1+k_2)$, so $a\equiv c\pmod n$.

This partitions $\mathbb{Z}$ into $n$ equivalence classes $\mathbb{Z}/n\mathbb{Z} = \{[0],[1],\dots,[n-1]\}$.

### Congruence is compatible with addition and multiplication
**Claim.** If $a \equiv b \pmod n$ and $c \equiv d \pmod n$, then $a+c \equiv b+d \pmod n$ and $ac \equiv bd \pmod n$.

**Proof.** By hypothesis there exist $k_1,k_2 \in \mathbb{Z}$ with
$$
a = nk_1 + b, \qquad c = nk_2 + d.
$$
*Addition*: $a+c = n(k_1+k_2) + (b+d)$, so $a+c \equiv b+d \pmod n$.

*Multiplication*: $ac = (nk_1+b)(nk_2+d) = n^2k_1k_2 + nak_2 \cdot \tfrac{}{} \dots$ — expanding directly,
$$
ac = n\big[nk_1k_2 + bk_2 + dk_1\big] + bd.
$$
The bracketed term is an integer multiplied by $n$, so $ac \equiv bd \pmod n$. $\blacksquare$

A useful restatement used throughout this course: $a^k \bmod n = (a \bmod n)^k \bmod n$, which follows by repeated application of the multiplicative case with $c=a,\, d = a\bmod n$.

### Consequence: reducing large exponents
Because $a^k \bmod n$ only depends on $a \bmod n$, congruences let you replace a huge base or exponent by a small representative before multiplying — this is the entire point of **repeated squaring**, the technique used to compute $g^k \bmod p$ in [[Diffie-Hellman Key Exchange]], $m^e \bmod n$ in [[RSA Cryptosystem]], and $kP$ (via the analogous doubling in the [[Elliptic Curve Group Law]]).

## Examples
- Divisibility proof (Tarea I): to show $3^{2n+5}+2^{4n+1}$ is divisible by $7$ for all $n\ge 1$, rewrite $3^{2n+5}=243\cdot 9^n$ and $2^{4n+1}=2\cdot 16^n$; since $243\equiv 5$, $9\equiv 2$, and $16\equiv 2 \pmod 7$, the sum reduces to $5\cdot 2^n + 2\cdot 2^n = 7\cdot 2^n \equiv 0 \pmod 7$.
- Divisibility with two moduli (Tarea I): $5^n+1$ is divisible by $2$ (since $5\equiv 1 \pmod 2 \Rightarrow 5^n+1\equiv 1+1\equiv 0$) but never by $4$ (since $5\equiv 1\pmod 4 \Rightarrow 5^n+1\equiv 2 \pmod 4$).
- A playful instance from "As" (Stevie Wonder), who sings $8\times 8\times 8 = 4$: this is exactly $8^3 \equiv 4 \pmod n$, i.e. $n \mid (8^3-4) = 508 = 2^2\cdot 127$. Since the congruence $4$ requires $n>4$, the only valid moduli are $n \in \{127, 254, 508\}$.

## See also
[[Modular Inverse]], [[Linear Congruence]], [[Chinese Remainder Theorem]], [[Group of Units U(n)]], [[Fermat-Euler Theorem]]
