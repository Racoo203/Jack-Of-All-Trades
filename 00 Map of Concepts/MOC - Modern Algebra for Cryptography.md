---
subject: Modern Algebra for Cryptography
type: MOC
course_code: MA2006B
course_name_es: "Uso de Álgebras Modernas para Seguridad y Criptografía"
domain: Mathematical Foundations
level: BSc
status: drafted
confidence: 0
tags:
  - moc
  - exam
  - abstract-algebra
  - cryptography
  - number-theory
---
## Concept narrative

MA2006B (Tecnológico de Monterrey) is a two-half course: **Module I** builds the abstract-algebra toolkit — [[Congruence Relation|modular arithmetic]] and [[Group (Definition)|group theory]] — and **Modules II–III** spend that toolkit on public-key cryptography, first over $(\mathbb{Z}/p\mathbb{Z})^*$ and then over elliptic curves. The throughline is that every cryptosystem in the course is "hard to invert, easy to verify" precisely because of a group-theoretic fact: it's cheap to compute $g^k$ (or $kP$) but expensive to recover $k$ from it.

**Module I — the algebra.** Everything starts from the [[Congruence Relation]] $a \equiv b \pmod n$ and the machinery to compute with it: the [[Extended Euclidean Algorithm]] produces Bézout coefficients, which give the [[Modular Inverse]] (exists iff $\gcd(a,n)=1$) and solve any solvable [[Linear Congruence]]. Several simultaneous congruences with coprime moduli combine via the [[Chinese Remainder Theorem]]. Counting the invertible residues gives [[Euler's Totient Function]] $\varphi(n)$, and the [[Fermat-Euler Theorem]] says $a^{\varphi(n)} \equiv 1 \pmod n$ whenever $\gcd(a,n)=1$ — the fact RSA is built on.

The same residues, now viewed abstractly, are the first example of a [[Group (Definition)|group]]: $\left(\mathbb{Z}/n\mathbb{Z}\right)^*$ is the [[Group of Units U(n)]], $U(n)$, of order $\varphi(n)$. From there the course develops the standard toolkit — [[Subgroup|subgroups]], the [[Order of an Element|order of an element]], [[Cyclic Group|cyclic groups]] and their generators, [[Direct Product of Groups|direct products]], [[Group Homomorphism|homomorphisms]] and [[Automorphism|automorphisms]] — using $U(n)$ and the [[Symmetric Group]] $S_n$ (built from [[Permutation and Cycle Notation|permutations]]) as the two running examples. This is exactly the algebra needed to justify why RSA, Diffie–Hellman and ElGamal work.

**Modules II–III — classical and elliptic-curve cryptography.** [[Diffie-Hellman Key Exchange]] and [[ElGamal Encryption]] both rely on the [[Discrete Logarithm Problem]] in $U(p)$: computing $g^k \bmod p$ is fast, recovering $k$ from $g^k$ is (believed) hard. [[RSA Cryptosystem|RSA]] instead relies on factoring: its correctness is the Fermat–Euler theorem, and its key generation is justified by the group isomorphism $(\mathbb{Z}/n\mathbb{Z})^* \cong (\mathbb{Z}/p\mathbb{Z})^* \times (\mathbb{Z}/q\mathbb{Z})^*$ (a [[Direct Product of Groups|direct-product]] instance of the [[Chinese Remainder Theorem]]); the [[Carmichael Function]] $\lambda(n)$ gives the tightest possible decryption exponent.

The last module replaces $U(p)$ with the point group of an [[Elliptic Curve over a Finite Field|elliptic curve over $\mathbb{F}_p$]]. The [[Elliptic Curve Group Law|group law]] (chord-and-tangent addition) turns the curve's points into an abelian group, and the same [[Discrete Logarithm Problem|discrete-log hardness]] — now the [[Elliptic Curve Discrete Logarithm Problem|ECDLP]] — reappears with no known sub-exponential attack, which is why 160-bit elliptic-curve keys match 1024-bit RSA keys in strength. [[ECDH|ECDH]] repeats Diffie–Hellman verbatim with $kP$ in place of $g^k$; [[ECDSA]] is the elliptic-curve analogue of a [[Digital Signature Scheme]].

## Concept map

### Unit 1 — Modular arithmetic
- [[Congruence Relation]] — $a\equiv b \pmod n \iff n\mid(a-b)$; equivalence relation, compatible with $+,\times$
- [[Extended Euclidean Algorithm]] — Bézout's identity $ax+by=\gcd(a,b)$ by back-substitution
- [[Modular Inverse]] — $a^{-1} \bmod n$ exists iff $\gcd(a,n)=1$
- [[Linear Congruence]] — $ax\equiv b \pmod n$ solvable iff $\gcd(a,n)\mid b$
- [[Chinese Remainder Theorem]] — pairwise-coprime moduli combine to a unique solution mod $M=\prod m_i$
- [[Euler's Totient Function]] — $\varphi(n)=|U(n)|$; multiplicative
- [[Fermat-Euler Theorem]] — $a^{\varphi(n)}\equiv 1 \pmod n$ for $\gcd(a,n)=1$

### Unit 2 — Group theory
- [[Group (Definition)]] — closure, associativity, identity, inverses; Abelian case
- [[Subgroup]] — one-step subgroup test
- [[Order of an Element]] — smallest $n$ with $g^n=e$; $|ab|=|ba|$
- [[Cyclic Group]] — $G=\langle a\rangle$; $\langle a\rangle=\langle a^{-1}\rangle$
- [[Group of Units U(n)]] — $(\mathbb{Z}/n\mathbb{Z})^*$ under multiplication, $|U(n)|=\varphi(n)$
- [[Direct Product of Groups]] — $G\times H$; CRT as a group isomorphism
- [[Permutation and Cycle Notation]] — disjoint-cycle decomposition
- [[Symmetric Group]] — $S_n$, $|S_n|=n!$
- [[Order of a Permutation]] — $\mathrm{lcm}$ of disjoint cycle lengths
- [[Group Homomorphism]] — structure-preserving maps; isomorphism as bijective homomorphism
- [[Automorphism]] — $\mathrm{Aut}(G)$; automorphisms of $\mathbb{Z}_n$ correspond to $U(n)$

### Unit 3 — Public-key cryptography over $U(p)$
- [[Discrete Logarithm Problem]] — hardness assumption behind DH, ElGamal
- [[Diffie-Hellman Key Exchange]] — $g,p$ public; shared secret $g^{ab} \bmod p$
- [[Digital Signature Scheme]] — sign/verify with public/private keys
- [[RSA Cryptosystem]] — $n=pq$, $ed\equiv 1 \pmod{\varphi(n)}$; encrypt/sign, decrypt/verify
- [[Carmichael Function]] — $\lambda(n) = \dfrac{(p-1)(q-1)}{\gcd(p-1,q-1)}$, valid in place of $\varphi(n)$
- [[ElGamal Encryption]] — $(c_1,c_2) = (g^k, m\cdot y^k) \bmod p$

### Unit 4 — Elliptic-curve cryptography
- [[Elliptic Curve over a Finite Field]] — $E: y^2 = x^3+c_1x+c_0 \pmod p$
- [[Elliptic Curve Group Law]] — chord-and-tangent addition/doubling; point at infinity $\mathcal{O}$
- [[Elliptic Curve Discrete Logarithm Problem]] — recover $k$ from $P, kP$
- [[ECDH]] — Diffie–Hellman with $kP$ in place of $g^k$
- [[ECDSA]] — signature $(r,s)$ from $R=kG$, $s=k^{-1}(m+rd) \bmod n$

## Key dependency chains

```
Congruence Relation ──> Extended Euclidean Algorithm ──┬──> Modular Inverse ──> Linear Congruence
                                                        │
                                                        └──> Chinese Remainder Theorem ──> Direct Product of Groups
                                                                     │                            │
Congruence Relation ──> Euler's Totient Function ───────────────────┘                            │
        │                        │                                                                │
        │                        └──> Fermat-Euler Theorem ──> RSA Cryptosystem <── Carmichael Function
        │                                                          ▲                     ▲
        └──> Group of Units U(n) ──> Order of an Element           └─────────────────────┘
                    │                       │                    (n = pq via CRT + φ multiplicativity)
                    ├──> Cyclic Group       ├──> Automorphism
                    │                       │
                    └──> Subgroup           └──> Group Homomorphism (isomorphism)

Group (Definition) ──> Symmetric Group ──(built from)── Permutation and Cycle Notation ──> Order of a Permutation

Group of Units U(p) ──> Discrete Logarithm Problem ──┬──> Diffie-Hellman Key Exchange
                                                      └──> ElGamal Encryption
Digital Signature Scheme ──> RSA Cryptosystem (sign/verify variant)

Elliptic Curve over a Finite Field ──> Elliptic Curve Group Law ──> Elliptic Curve Discrete Logarithm Problem
                                                                              │
                                              ┌───────────────────────────────┼────────────────────┐
                                              ▼                                                     ▼
                                            ECDH  (≅ Diffie-Hellman Key Exchange)      ECDSA  (≅ Digital Signature Scheme)
```

## Exam focus

The graded material (Actividades and Tareas in `Resources/01 Mathematical Foundations/MA2006B/`) is entirely hand-worked computation and proof, not multiple choice. High-priority, in rough order of how often the pattern repeats:

1. **Modular arithmetic proof techniques** — proving divisibility via congruences (e.g. $3^{2n+5}+2^{4n+1}\equiv 0 \pmod 7$), solving linear congruences and Diophantine equations with the extended Euclidean algorithm, and systems of congruences with the [[Chinese Remainder Theorem]] (the "chapatis" puzzle style: reduce redundant congruences first, then combine by pairs).
2. **Group-theory proof-writing** — the recurring pattern is "prove $G$ is Abelian iff [identity]", "prove $|ab|=|ba|$", "prove $H\cap K$ is a subgroup", using the [[Subgroup|one-step subgroup test]] and the definitions directly rather than citing named theorems.
3. **$U(n)$ structure** — deciding whether $U(n)$ is cyclic (it fails for $U(2^n)$, $n\ge 3$), finding automorphisms of $\mathbb{Z}_n$ satisfying a constraint and matching them to a subgroup of $U(n)$ via the Cayley-table isomorphism.
4. **RSA end-to-end by hand**: choose $p,q,e$ → compute $n,\varphi(n)$ → extended Euclid for $d$ → sign/encrypt $m^e \bmod n$ → verify $c^d \bmod n$.
5. **Diffie–Hellman and ElGamal end-to-end by hand**, using repeated-squaring to keep the modular exponentiation tractable.
6. **Elliptic-curve arithmetic by hand**: verify a point lies on $E$, compute $P+Q$ and $2P$ with the $\lambda/\mu$ formulas, then scalar multiplication $kP$ by repeated doubling+addition (binary expansion of $k$) for [[ECDH]] and [[ECDSA]].

Question types: "verify then compute" (elliptic curve problem sets), "generate keys, encrypt, decrypt, verify" (RSA/ElGamal/ECDH/ECDSA), and "prove the following group-theoretic statement" (Módulo I homework).

## Open questions

- The professor's elliptic-curve notation writes $E : y^2 = x^3 + c_1 x + c_0 \pmod p$ (coefficients $c_1, c_0$) rather than the more common $y^2=x^3+ax+b$ — kept as the primary notation in [[Elliptic Curve over a Finite Field]] and [[Elliptic Curve Group Law]], with the standard $a,b$ form noted as an alias.
- None of the graded elliptic-curve or ElGamal/RSA activities in `Resources/` include an answer key; the worked numeric examples in these notes are taken only from Raúl's own submitted solutions (`Tarea II.pdf`, `Actividad_Protocolos_criptográficos.pdf`, `A01722401_Actividad_Criptografía_Elíptica.pdf`, `Act1_v2.pdf`) or independently re-derived — flag anything that doesn't match the graded feedback once it comes back.
- `Tarea II-1.pdf` (Problem 9, unsolved in the "Gran Final" submission) asks for automorphisms $\phi:\mathbb{Z}_{20}\to\mathbb{Z}_{20}$ with $\phi(5)=5$; the solved version in `Tarea II.pdf` identifies $\{\alpha_1,\alpha_9,\alpha_{13},\alpha_{17}\}\cong\{1,9,13,17\}\le U(20)$ — worth double-checking the Cayley table in [[Automorphism]] against the professor's own solution once available.
