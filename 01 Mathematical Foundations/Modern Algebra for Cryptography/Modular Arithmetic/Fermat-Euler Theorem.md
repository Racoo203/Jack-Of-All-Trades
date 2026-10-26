---
title: "Fermat-Euler Theorem"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Modular Arithmetic"
level: BSc
status: drafted
confidence: 0
tags: [number-theory, modular-arithmetic, cryptography]
---
## Definition
**Euler's theorem.** If $\gcd(a,n)=1$, then
$$
a^{\varphi(n)} \equiv 1 \pmod n,
$$
where $\varphi$ is [[Euler's Totient Function]]. The special case $n=p$ prime is **Fermat's little theorem**: for $\gcd(a,p)=1$,
$$
a^{p-1} \equiv 1 \pmod p.
$$

## Properties
### Proof via group theory
The residues coprime to $n$ form the [[Group of Units U(n)]] under multiplication mod $n$, with $|U(n)| = \varphi(n)$. For any $a$ with $\gcd(a,n)=1$, $a \bmod n \in U(n)$, and by [[Order of an Element|Lagrange-type order arguments]] the order of any element of a finite group divides the group's order: $|a| \mid |U(n)| = \varphi(n)$. Writing $\varphi(n) = |a|\cdot k$,
$$
a^{\varphi(n)} = \left(a^{|a|}\right)^k = e^k = e = 1 \pmod n.
$$

### RSA correctness is exactly this theorem
For $n=pq$, $e,d$ with $ed \equiv 1 \pmod{\varphi(n)}$, and message $m$ with $\gcd(m,n)=1$: write $ed = 1 + k\varphi(n)$ for some integer $k$. Then
$$
(m^e)^d = m^{ed} = m^{1+k\varphi(n)} = m\cdot\left(m^{\varphi(n)}\right)^k \equiv m \cdot 1^k \equiv m \pmod n,
$$
by Euler's theorem. This is precisely why decrypting an RSA-encrypted (or verifying an RSA-signed) message recovers the original $m$ — see [[RSA Cryptosystem]].

### Order-of-magnitude use: reducing exponents mod $\varphi(n)$ or $\mathrm{ord}(a)$
Because $a^{\varphi(n)}\equiv 1$, any exponent $k$ can be reduced modulo $\varphi(n)$ before exponentiating: $a^k \equiv a^{k \bmod \varphi(n)} \pmod n$ whenever $\gcd(a,n)=1$. This is the theoretical basis for repeated-squaring shortcuts used throughout [[Diffie-Hellman Key Exchange]] and [[RSA Cryptosystem]] computations (e.g. reducing $5^{15} \bmod 23$ by writing $15 = 2\cdot 7+1$ and squaring).

## Examples
- Divisibility proof by Fermat's little theorem: to show $5^n+1$ is divisible by $2$ but not $4$ for all $n\ge1$ (Tarea I), note $5\equiv1\pmod2$ so $5^n\equiv1\pmod2$ directly (Fermat's theorem for $p=2$ is trivial here, but the modular-power reduction is the same idea used with larger primes elsewhere in the course).
- $3^{99} \bmod 5$ pattern (analogous to Tarea II Gran Final's permutation-order reduction $99 \equiv 4 \pmod 5$): since $\gcd(3,5)=1$ and $\varphi(5)=4$, $3^{99} \equiv 3^{99\bmod 4} = 3^3 \equiv 2 \pmod 5$.
- The entire correctness argument for [[RSA Cryptosystem]] key generation with $p=11,q=17,e=7,d=23$ rests on Euler's theorem with $\varphi(187)=160$.

## See also
[[Euler's Totient Function]], [[Congruence Relation]], [[Order of an Element]], [[Group of Units U(n)]], [[RSA Cryptosystem]]
