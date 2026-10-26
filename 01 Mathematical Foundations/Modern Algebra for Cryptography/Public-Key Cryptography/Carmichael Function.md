---
title: "Carmichael Function"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Public-Key Cryptography"
level: BSc
status: drafted
confidence: 0
tags: [cryptography, number-theory, group-theory]
---
## Definition
For $n=pq$ with $p,q$ distinct primes, the **Carmichael function** is
$$
\lambda(n) = \frac{(p-1)(q-1)}{\gcd(p-1,q-1)} = \mathrm{lcm}(p-1,q-1).
$$
More generally $\lambda(n)$ is the exponent of the group $(\mathbb{Z}/n\mathbb{Z})^*$: the smallest $m$ such that $a^m \equiv 1 \pmod n$ for **every** $a$ coprime to $n$.

## Properties
### $\lambda(n)$ can replace $\varphi(n)$ in RSA
**Claim** (`ActividadRSA.pdf`, Problem 4). If $de \equiv 1 \pmod{\lambda(n)}$, then $m^{ed} \equiv m \pmod n$ for all $m$ with $\gcd(m,n)=1$ — the same correctness guarantee as using $\varphi(n)=(p-1)(q-1)$.

**Proof.** By the [[Direct Product of Groups]] isomorphism $(\mathbb{Z}/n\mathbb{Z})^* \cong (\mathbb{Z}/p\mathbb{Z})^*\times(\mathbb{Z}/q\mathbb{Z})^*$, an element $a\in(\mathbb{Z}/n\mathbb{Z})^*$ corresponds to a pair $(a_p,a_q)$ with $a_p \in (\mathbb{Z}/p\mathbb{Z})^*,\ a_q\in(\mathbb{Z}/q\mathbb{Z})^*$. By Fermat's little theorem, $a_p^{p-1}\equiv1 \pmod p$ and $a_q^{q-1}\equiv1\pmod q$. Since $\lambda(n)=\mathrm{lcm}(p-1,q-1)$ is a multiple of both $p-1$ and $q-1$, $a_p^{\lambda(n)}\equiv1\pmod p$ and $a_q^{\lambda(n)}\equiv1\pmod q$ as well, so $a^{\lambda(n)}\equiv1\pmod n$ componentwise. Now write $ed = 1+k\lambda(n)$: then $m^{ed} = m\cdot(m^{\lambda(n)})^k \equiv m\cdot1^k \equiv m \pmod n$, exactly as in the [[Fermat-Euler Theorem]] argument for $\varphi(n)$. $\blacksquare$

### $\lambda(n) \mid \varphi(n)$, and often strictly smaller
Since $\lambda(n)=\mathrm{lcm}(p-1,q-1)$ divides $(p-1)(q-1)=\varphi(n)$ (a general fact: $\mathrm{lcm}(x,y)\mid xy$, with equality iff $\gcd(x,y)=1$), $\lambda(n) \le \varphi(n)$, with strict inequality whenever $\gcd(p-1,q-1)>1$ — which gives a smaller, still-valid private exponent $d$.

## Examples
- For the RSA example $p=61,\ q=53$: $\varphi(n)=60\cdot52=3120$, while $\lambda(n) = \mathrm{lcm}(60,52) = \dfrac{60\cdot52}{\gcd(60,52)} = \dfrac{3120}{4} = 780$ — a factor of $4$ smaller, since $\gcd(60,52)=4$.
- Any valid RSA private exponent found via $\varphi(n)$ is automatically valid via $\lambda(n)$ too (since $\lambda(n)\mid\varphi(n)$), but not conversely — $\lambda(n)$ gives *all* valid exponents, while $\varphi(n)$ only gives a subset.

## See also
[[Euler's Totient Function]], [[Direct Product of Groups]], [[RSA Cryptosystem]], [[Fermat-Euler Theorem]]
