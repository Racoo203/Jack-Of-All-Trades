---
title: "Digital Signature Scheme"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Public-Key Cryptography"
level: BSc
status: drafted
confidence: 0
tags: [cryptography, number-theory, group-theory]
---
## Definition
A **digital signature scheme** lets a signer with a private key produce, for a message $m$, a signature $\sigma$ that anyone holding the corresponding public key can **verify** as authentic — without being able to forge a valid signature for a different message. Formally it consists of three algorithms: key generation, $\mathrm{Sign}(m, \text{private key}) \to \sigma$, and $\mathrm{Verify}(m,\sigma,\text{public key}) \to \{\text{accept},\text{reject}\}$, with the requirement that $\mathrm{Verify}(m, \mathrm{Sign}(m,\cdot), \cdot)$ always accepts.

## Properties
### The RSA instantiation: signing is "encryption in reverse"
In [[RSA Cryptosystem]] used as a signature scheme, the roles of $e$ (public) and $d$ (private) swap relative to encryption: the signer computes $\sigma = m^d \bmod n$ using their *private* exponent $d$, and anyone can verify by checking $\sigma^e \equiv m \pmod n$ using the *public* exponent $e$. Correctness is the same [[Fermat-Euler Theorem]] identity as decryption: $(m^d)^e = m^{de} \equiv m \pmod n$.

### The ECDSA instantiation: signing produces a pair $(r,s)$
[[ECDSA]] does not sign by exponentiating the message directly; instead it derives $(r,s)$ from a random nonce $k$, the message $m$, and the private key $d$, using the [[Elliptic Curve Group Law]] and the [[Elliptic Curve Discrete Logarithm Problem]]'s hardness to prevent forgery. This is structurally different from RSA signing but plays the same role.

### Why forgery should be hard
In both instantiations, producing a valid signature without the private key would require either solving the underlying hard problem (factoring $n$ for RSA, or the ECDLP for ECDSA) or finding a specific collision/inverse that is computationally equivalent to it.

## Examples
- RSA signing (`TareaModulo2.pdf`, Problem 3): sign $m=8$ with $p=11,q=17,e=7$; $d=23$; $\sigma = 8^7 \bmod 187$; verify $\sigma^{23} \equiv 8 \pmod{187}$ — see [[RSA Cryptosystem]] for the full computation.
- [[ECDSA]] signing a message $m=9$ on $E:y^2=x^3+x+13 \pmod{29}$.

## See also
[[RSA Cryptosystem]], [[ECDSA]], [[Fermat-Euler Theorem]], [[Elliptic Curve Discrete Logarithm Problem]]
