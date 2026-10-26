---
title: "Chinese Remainder Theorem"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Modular Arithmetic"
level: BSc
status: drafted
confidence: 0
tags: [number-theory, modular-arithmetic, cryptography]
---
## Definition
Let $m_1, \dots, m_r$ be pairwise coprime positive integers and $M = m_1 m_2 \cdots m_r$. The system of congruences
$$
x \equiv a_1 \pmod{m_1}, \quad x \equiv a_2 \pmod{m_2}, \quad \dots, \quad x \equiv a_r \pmod{m_r}
$$
has a solution $x$, and this solution is unique modulo $M$.

The professor's explicit construction (as used in `Act1_v2.pdf`): let $M_i = M/m_i$ and let $M_i^{-1}$ be the [[Modular Inverse]] of $M_i$ modulo $m_i$. Then
$$
x = \left(\sum_{i=1}^r a_i M_i M_i^{-1}\right) \bmod M.
$$

## Properties
### Existence
Since $M_i = M/m_i$ is a product of all moduli except $m_i$, and the $m_j$ are pairwise coprime, $\gcd(M_i, m_i)=1$, so $M_i^{-1} \bmod m_i$ exists (see [[Modular Inverse]]). Also $M_i \equiv 0 \pmod{m_j}$ for every $j \ne i$. Hence, reducing the proposed $x$ modulo $m_i$:
$$
x \equiv a_i M_i M_i^{-1} \equiv a_i \cdot 1 \equiv a_i \pmod{m_i},
$$
since every other term vanishes mod $m_i$ and $M_iM_i^{-1}\equiv 1 \pmod{m_i}$ by construction. So $x$ satisfies every congruence simultaneously.

### Uniqueness modulo $M$
If $x$ and $x'$ both solve the system, then $x \equiv x' \pmod{m_i}$ for every $i$, i.e. $m_i \mid (x-x')$ for all $i$. Since the $m_i$ are pairwise coprime, their product also divides $x-x'$ (an induction on the number of coprime factors), so $x \equiv x' \pmod M$.

### Two-modulus case and reduction of redundant congruences
For $r=2$: $x = (a_1M_1M_1^{-1} + a_2M_2M_2^{-1}) \bmod M$, with $M_1=m_2,\ M_2=m_1$.

In systems with many congruences (e.g. the "chapatis" puzzle below), it is common for one congruence to be implied by another with a multiple modulus: if $n \equiv c \pmod{km}$ then automatically $n \equiv c \bmod m \pmod m$ for $m \mid km$, so overlapping congruences can be discarded before applying CRT to the reduced, pairwise-coprime system.

## Examples
- **Two congruences** (`Act1_v2.pdf`, Problem 4): $x \equiv 4 \pmod 8,\ x \equiv -1 \pmod{15}$. With $M=120$, $M_1=15,\ M_2=8$, $M_1^{-1}\equiv 7 \pmod 8$, $M_2^{-1}\equiv 2\pmod{15}$: $x = (4\cdot15\cdot7 + (-1)\cdot8\cdot2) \bmod 120 = 404 \bmod 120 = 44$.
- **The "chapatis" puzzle** (Tarea I / `Act1_v2.pdf`, Problem 9): find the least $n\ge0$ with
$$
n\equiv1(\text{mod }2),\ n\equiv2(\text{mod }3),\ n\equiv3(\text{mod }4),\ n\equiv4(\text{mod }5),\ n\equiv5(\text{mod }6),\ n\equiv0(\text{mod }7).
$$
Since $n\equiv3\pmod4 \Rightarrow n\equiv1\pmod2$ and $n\equiv5\pmod6\Rightarrow n\equiv2\pmod3$, those two congruences are redundant. Combining $n\equiv3\pmod4$ and $n\equiv5\pmod6$ modulo $\mathrm{lcm}(4,6)=12$ forces $n\equiv11\pmod{12}$. The reduced, pairwise-coprime system $n\equiv4\pmod5,\ n\equiv0\pmod7,\ n\equiv11\pmod{12}$ has modulus $M=420$; solving gives $n=119$.
- **RSA's key-generation justification** uses CRT in ring form: $\mathbb{Z}/n\mathbb{Z} \cong \mathbb{Z}/p\mathbb{Z} \times \mathbb{Z}/q\mathbb{Z}$ for $n=pq$ with $p,q$ distinct primes, which restricts to the group isomorphism $(\mathbb{Z}/n\mathbb{Z})^* \cong (\mathbb{Z}/p\mathbb{Z})^* \times (\mathbb{Z}/q\mathbb{Z})^*$ — see [[Direct Product of Groups]] and [[RSA Cryptosystem]].

## See also
[[Congruence Relation]], [[Modular Inverse]], [[Direct Product of Groups]], [[Euler's Totient Function]], [[RSA Cryptosystem]]
