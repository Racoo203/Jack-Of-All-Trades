---
title: "ElGamal Encryption"
domain: "Mathematical Foundations"
course: "Modern Algebra for Cryptography"
unit: "Public-Key Cryptography"
level: BSc
status: drafted
confidence: 0
tags: [cryptography, number-theory, group-theory]
---
## Definition
**Public parameters**: prime $p$, generator $g$ of $U(p)$.

**Key generation**: Alice picks a private key $x$ and publishes $y = g^x \bmod p$.

**Encryption** (Bob, sending $m$): pick a random ephemeral value $k$, compute
$$
c_1 = g^k \bmod p, \qquad c_2 = m\cdot y^k \bmod p.
$$
The ciphertext is the pair $(c_1,c_2)$.

**Decryption** (Alice): compute $s = c_1^x \bmod p$ and recover
$$
m = c_2 \cdot s^{-1} \bmod p,
$$
using the [[Modular Inverse]] of $s$.

## Properties
### Correctness
Since $c_1 = g^k$, $s = c_1^x = g^{kx} = (g^x)^k = y^k \pmod p$ — the same value Bob used to mask $m$. So
$$
c_2 \cdot s^{-1} = (m\cdot y^k)\cdot (y^k)^{-1} = m \pmod p.
$$

### Security rests on the Discrete Logarithm Problem
An eavesdropper sees $p,g,y,c_1,c_2$ but not $x$ or $k$. Recovering $m$ without the private key requires computing $y^k$ from $c_1=g^k$ and $y=g^x$ without knowing $x$ or $k$ — the [[Discrete Logarithm Problem|Diffie–Hellman problem]], believed as hard as the discrete logarithm problem itself for well-chosen $p,g$.

### Each encryption needs a fresh $k$
Re-using $k$ across two messages $m_1,m_2$ leaks their ratio: $c_2^{(1)}/c_2^{(2)} = m_1/m_2 \pmod p$ (both share the same $y^k$ mask), regardless of the discrete-log hardness assumption — this is why $k$ is chosen fresh ("random") for every encryption in the course's exercises.

## Examples
**Worked example** (`Actividad_Protocolos_criptográficos.pdf`, Ejercicio 3.1): $p=19,\ g=2,\ x=5,\ m=9,\ k=6$.
$$
y = 2^5 \equiv 13 \pmod{19}.
$$
$$
c_1 = 2^6 \equiv 7 \pmod{19}, \qquad c_2 = 9\cdot13^6 \equiv 9\cdot(13^2)^3 \equiv 9\cdot17^3 \equiv 4 \pmod{19}.
$$
Decryption: $s = 7^5 \equiv 7\cdot(7^2)^2 \equiv 7\cdot11^2 \equiv 11 \pmod{19}$; via the extended Euclidean algorithm, $11^{-1}\equiv7\pmod{19}$. So $\hat m = c_2\cdot s^{-1} \equiv 4\cdot7 \equiv 9 \pmod{19}$ — the original message, recovered.

- A second, larger instance ($p=89,g=3,x=25,m=42,k=17$) gives $(c_1,c_2)=(6,63)$ and correctly recovers $\hat m=42$.

## See also
[[Discrete Logarithm Problem]], [[Modular Inverse]], [[Group of Units U(n)]], [[Diffie-Hellman Key Exchange]]
