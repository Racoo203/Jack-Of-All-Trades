---
title: "ECDSA"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Elliptic Curve Cryptography"
level: BSc
status: drafted
confidence: 0
tags: [cryptography, elliptic-curves, number-theory]
---
## Definition
**Elliptic Curve Digital Signature Algorithm.** Public parameters: curve $E$ over $\mathbb{F}_p$, base point $G$ of order $n$. Signer's key pair: private $d$, public $Q=dG$.

**Signing** a message $m$ (an integer, e.g. a hash of the real message):
1. Choose a random $k \in \{1,\dots,n-1\}$.
2. Compute $R = kG$ and let $r = x_R \bmod n$ (the $x$-coordinate of $R$, reduced mod $n$).
3. Compute $s = k^{-1}(m + r\cdot d) \bmod n$.
4. The signature is the pair $(r,s)$.

**Verification** (this course's exercises stop at reproducing the signature computation; the standard verification recomputes $R' = s^{-1}(mG + rQ)$ and checks $x_{R'} \bmod n = r$).

## Properties
### Why $s = k^{-1}(m+rd) \bmod n$ ties the signature to both $m$ and $d$
Rearranging the signing equation, $sk \equiv m + rd \pmod n$, i.e. $k \equiv s^{-1}(m+rd) \pmod n$ — the nonce $k$ is recoverable only by whoever can invert $s$, and $r$ only encodes $k$ through the hard-to-invert map $k \mapsto x$-coordinate of $kG$ (the [[Elliptic Curve Discrete Logarithm Problem]]). This is exactly why the verifier can confirm the signature via the public $Q=dG$ without ever learning $d$ or $k$.

### Reusing $k$ leaks the private key
If the same nonce $k$ signs two different messages $m_1,m_2$ producing $(r,s_1)$ and $(r,s_2)$ (same $r$, since $R=kG$ is unchanged), then $s_1k \equiv m_1+rd$ and $s_2k\equiv m_2+rd \pmod n$; subtracting eliminates $d$: $k \equiv (m_1-m_2)(s_1-s_2)^{-1} \pmod n$, immediately recovering $k$ and then $d = (s_1k-m_1)r^{-1} \bmod n$. This mirrors why $k$ must be fresh in [[ElGamal Encryption]], and is the same fragility present in classical DSA.

## Examples
**Worked setup** (`ECDSA.pdf`, Problem 1): $E:y^2=x^3+x+13 \pmod{29}$, generator $G=(4,20)$ of order $n=11$, private key $d=5$, message $m=9$, nonce $k=7$.
1. $R = 7G$ (computed via the [[Elliptic Curve Group Law]]).
2. $r = x_R \bmod 11$.
3. $s = 7^{-1}(9+5r) \bmod 11$.
4. Signature: $(r,s)$.

- A second instance: $E:y^2=x^3+2x+3 \pmod{97}$, $G=(4,47)$ of order $n=50$, $d=13$, $m=45$, $k=29$ — same four steps, larger modulus.

## See also
[[Elliptic Curve Group Law]], [[Elliptic Curve Discrete Logarithm Problem]], [[Digital Signature Scheme]], [[Modular Inverse]], [[ECDH]]
