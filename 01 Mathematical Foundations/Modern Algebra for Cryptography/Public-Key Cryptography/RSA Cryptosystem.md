---
title: "RSA Cryptosystem"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Public-Key Cryptography"
level: BSc
status: drafted
confidence: 0
tags: [cryptography, number-theory, group-theory]
---
## Definition
**Key generation**: choose distinct primes $p,q$; let $n=pq$ and $\varphi(n)=(p-1)(q-1)$ ([[Euler's Totient Function]]); choose a public exponent $e$ with $\gcd(e,\varphi(n))=1$; compute the private exponent $d$ via $de \equiv 1 \pmod{\varphi(n)}$ (a [[Modular Inverse]], found with the [[Extended Euclidean Algorithm]]). Public key: $(n,e)$. Private key: $d$.

**Encryption/verification** (public): $c = m^e \bmod n$.
**Decryption/signing** (private): $m = c^d \bmod n$.

As a [[Digital Signature Scheme]], signing uses $d$ and verification uses $e$ (roles reversed from encryption).

## Properties
### Correctness
$$
(m^e)^d = m^{ed} \equiv m \pmod n,
$$
which is exactly the [[Fermat-Euler Theorem]] applied with exponent $ed\equiv1\pmod{\varphi(n)}$: writing $ed=1+k\varphi(n)$, $m^{ed}=m\cdot(m^{\varphi(n)})^k\equiv m\cdot1^k=m \pmod n$ whenever $\gcd(m,n)=1$. The same identity, with $e,d$ swapped, shows $(m^d)^e\equiv m \pmod n$, which is why signing-then-verifying also recovers $m$.

### Why $\varphi(n)$ can be replaced by $\lambda(n)$
See [[Carmichael Function]]: using $\lambda(n)=\mathrm{lcm}(p-1,q-1)$ in place of $\varphi(n)=(p-1)(q-1)$ gives the same correctness guarantee with a (weakly) smaller modulus for $d$.

### Structural justification of key generation via CRT
The reason RSA's algebra reduces to two small computations mod $p$ and mod $q$ rather than one hard computation mod $n$ is the [[Direct Product of Groups]] isomorphism $(\mathbb{Z}/n\mathbb{Z})^* \cong (\mathbb{Z}/p\mathbb{Z})^*\times(\mathbb{Z}/q\mathbb{Z})^*$, itself an instance of the [[Chinese Remainder Theorem]].

## Examples
**Worked signing example** (`TareaModulo2.pdf` / `Actividad_Protocolos_criptográficos.pdf`, Ejercicio 2.1): $p=11,\ q=17,\ e=7$.
$$
n = 187, \qquad \varphi(n) = 10\cdot16 = 160.
$$
Solving $7d \equiv 1 \pmod{160}$ via the extended Euclidean algorithm ($160=7(22)+6,\ 7=6(1)+1 \Rightarrow 1=7(23)-160(1)$) gives $d\equiv 23 \pmod{160}$ (check: $7\cdot23=161\equiv1\pmod{160}$).

Signing $m=8$: $\tilde m = 8^7 \equiv 8\cdot(8^3)^2 \equiv 8\cdot138^2 \equiv 8\cdot157 \equiv 134 \pmod{187}$.

Verifying: $\hat m = 134^{23} \equiv 134\cdot(134^2)^{11} \equiv \cdots \equiv 8 \pmod{187}$, recovering $m$.

- A second instance ($p=13,q=29,e=11$): $n=377,\ \varphi(n)=336,\ d\equiv275\pmod{336}$; signing $m=37$ gives $\tilde m=32$, and verifying recovers $\hat m = 37$.
- Small textbook instance: $p=61,\ q=53,\ e=17 \Rightarrow n=3233,\ \varphi(n)=3120$ (`ActividadRSA.pdf`, Problem 5).

## See also
[[Euler's Totient Function]], [[Fermat-Euler Theorem]], [[Extended Euclidean Algorithm]], [[Carmichael Function]], [[Chinese Remainder Theorem]], [[Direct Product of Groups]], [[Digital Signature Scheme]]
