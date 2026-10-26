---
subject: Financial Derivatives
type: MOC
exam_date: 2026-05-22
status: drafted
confidence: 0
tags:
  - moc
  - exam
  - financial-derivatives
domain: Finance & Markets
---
## Concept narrative

> This course (MA320, Financial Derivatives, University of Essex) builds a single pricing machine — no-arbitrage plus replication — and applies it to every derivative contract it meets. It opens with the probabilistic scaffolding (Chapters 1–3): the [[Normal distribution]] and [[Lognormal distribution]] that describe share prices, [[Brownian motion]] and [[Geometric Brownian Motion]] as the driving noise, and the [[Itô Integral]] / [[Ito's Lemma|Itô's Lemma]] toolkit needed to differentiate functions of a random process. Chapter 4 introduces the actual instruments — [[Forward contract]], [[Future contract]], [[Call option]], [[Put option]], [[American Options]], [[Swap contract]] — and the one idea that prices all of them: the [[No-arbitrage principle]].

> Chapters 5–8 are the pricing core. [[Binomial option pricing model|Binomial trees]] introduce [[Replicating Portfolio|replication]] and the synthetic (risk-neutral) probability in the easy discrete setting, and [[Complete and Incomplete Financial Markets|market completeness]] tells you when replication is even possible. The [[Black-Scholes model|Black-Scholes-Merton model]] extends this to continuous time via a PDE argument, and the [[Black-Scholes formula|closed-form solution]] is the course's centrepiece. [[Risk-neutral pricing]] gives the same answer from a different direction — changing probability measure via [[Girsanov theorem|Girsanov's theorem]] so that discounted prices become martingales — and [[Equivalent Probability Measures]] and the [[Martingale Representation Theorem]] make that rigorous. Chapter 7's [[Greeks]] turn the pricing formula into a risk-management tool, and [[Hedging]] shows how a derivative desk actually uses them.

> The final third generalises the machine: [[Interest rate models|interest-rate models]] ([[Vasicek Model]], [[Cox-Ingersoll-Ross (CIR) Process|CIR]], [[Hull-White Model]]) apply the same no-arbitrage logic to the term structure instead of a share price, [[Credit Risk]] applies it to the possibility of default ([[Merton Model (Credit Risk)|Merton's structural model]] treats equity itself as a call option; [[Reduced-Form Credit Risk Model|reduced-form models]] borrow directly from survival analysis' [[Hazard Function]]), and [[Stochastic volatility]] (the Heston model) relaxes the assumption that volatility is constant. The PGT supplementary lectures round out the toolkit with [[Implied Volatility]], dividend and FX/futures extensions ([[Garman-Kohlhagen Formula]], [[Black's Model (Options on Futures)]]), [[Option Trading Strategies]], [[Bounds for Option Prices]], and embedded-derivative applications ([[Warrant]], [[Convertible Bond]]).

---

## Concept map

### Chapter 1 — Common Distributions in Finance
- [[Normal distribution]] → [[Lognormal distribution]] # canonical, cross-linked to 02 Probability Theory
- [[Terminal Share Price Distribution]] # lognormal share-price model $S_t=S_0e^{(\mu-\frac12\sigma^2)t+\sigma\sqrt t Z}$; $\Pr(S_t<K)=N(-\hat d_2)$ — the direct ancestor of $N(d_2)$ in Black-Scholes
- [[Moment Generating Function]] # used to derive lognormal mean/variance

### Chapter 2 — Brownian Motion
- [[Brownian motion]] → [[Geometric Brownian Motion]] # canonical, cross-linked to 03 Stochastic Processes
- [[Martingale]], [[Filtration]] # canonical prerequisites, cross-linked
- [[Simple Random Walk|Random Walk]] # discrete construction of BM (canonical, exists elsewhere)
- [[Efficient Market Hypothesis]] # Markov property ⇔ EMH
- [[Bachelier's Model]] # arithmetic BM for share prices — historically first, superseded by GBM

### Chapter 3 — The Itô Integral
- [[Itô Integral]] → [[Ito's Lemma|Itô's Lemma]] # canonical, Itô's Lemma cross-linked to 03
- [[Multivariate Itô's Lemma]] # 2-D extension (PGT), used by the Heston model
- [[Ornstein-Uhlenbeck Process]] # common finance model solved via Itô's Lemma
- [[Stopping time]] # canonical, cross-linked to 03

### Chapter 4 — Financial Markets
- [[Types of Financial Markets]] # stock/bond/money/commodity/currency/index markets
- [[Derivative contract]] → [[Forward contract]], [[Future contract]] # payoff, margin, no-arbitrage forward price
- [[Call option]], [[Put option]] → [[European Options]] → [[American Options]] # payoffs, moneyness
- [[Swap contract]], [[Long and Short Positions]]
- [[No-arbitrage principle]] → [[Put-call parity]] # portfolio-replication proof

### Chapter 5 — Binomial Trees
- [[Binomial option pricing model]] # one-step, multi-step, CRR parameterization, American exercise
- [[Replicating Portfolio]], [[Self-Financing Strategy]] # formal definitions (appendix)
- [[Complete and Incomplete Financial Markets]] # trinomial model as a counterexample
- [[Volatility (Financial)|Volatility]] # CRR's $u,d$ calibrated to $\sigma$
- [[Equivalent Probability Measures]] → [[Girsanov theorem]] # change of measure, GBM under $Q$

### Chapter 6 — The Black-Scholes-Merton Model
- [[Black-Scholes model]] # solving the GBM SDE, the BSM PDE via replication
- [[Black-Scholes formula]] # $c=S_0N(d_1)-Ke^{-rT}N(d_2)$, full derivation, log-normal probability results
- [[Garman-Kohlhagen Formula]] # continuous dividend yield $q$; index/FX/futures applications
- [[Implied Volatility]] # iterative inversion, volatility smile, weighted averaging
- [[Cox-Ingersoll-Ross (CIR) Process]] → [[Stochastic volatility]] # Heston model, Feller condition
- [[Variable Annuity Guarantees]] # GMMB as an embedded put option

### Chapter 7 — The Greeks & Market Risk
- [[Greeks]] # Delta, Gamma, Theta, Vega, Rho — definitions and BSM formulas
- [[Hedging]] # delta-neutral, gamma-neutral, hedge slippage, transaction costs

### Chapter 8 — Risk-Neutral Pricing and the Equivalent Martingale Measure
- [[Risk-neutral pricing]] # self-financing/replicating strategy, market completeness
- [[Equivalent Probability Measures]] → [[Girsanov theorem]] # Cameron-Martin-Girsanov theorem
- [[Martingale Representation Theorem]]

### Chapter 9 — Interest Rate Models
- [[Interest rate models]] # term structure, forward/spot rate relationships, market price of risk, pricing kernel
- [[Vasicek Model]] → [[Cox-Ingersoll-Ross (CIR) Process]] → [[Hull-White Model]]

### Chapter 10 — Credit Risk
- [[Credit Risk]] # expected loss = exposure × PD × LGD; credit events
- [[Merton Model (Credit Risk)]] # structural model, equity as a call option, distance to default
- [[Reduced-Form Credit Risk Model]] # hazard-rate/intensity approach, cross-linked to [[Hazard Function]] (Survival Analysis)

### PGT Lectures (supplementary/advanced)
- [[Multivariate Itô's Lemma]], [[Bounds for Option Prices]], [[Option Trading Strategies]]
- [[Black's Model (Options on Futures)]], [[Warrant]], [[Convertible Bond]]

---

## Key dependency chains

```
[[Normal distribution]] ──► [[Lognormal distribution]] ──► [[Terminal Share Price Distribution]]
                                                                       │
[[Brownian motion]] ──► [[Geometric Brownian Motion]] ────────────────┤
        │                                                             ▼
        ▼                                                    [[Black-Scholes model]]
[[Itô Integral]] ──► [[Ito's Lemma]] ──► [[Multivariate Itô's Lemma]]  │
        │                                        │                    ▼
        ▼                                        ▼           [[Black-Scholes formula]]
[[Ornstein-Uhlenbeck Process]]          [[Stochastic volatility]]      │
                                                                       ├──► [[Greeks]] ──► [[Hedging]]
[[Equivalent Probability Measures]] ──► [[Girsanov theorem]]           ├──► [[Garman-Kohlhagen Formula]]
        │                                        │                    └──► [[Implied Volatility]]
        ▼                                        ▼
[[Martingale Representation Theorem]]   [[Risk-neutral pricing]]
                                                  │
[[Replicating Portfolio]] ──┬──────────────────► [[Complete and Incomplete Financial Markets]]
[[Self-Financing Strategy]] ┘
        │
        ▼
[[Binomial option pricing model]] ──► [[Volatility (Financial)]] (CRR calibration)

[[No-arbitrage principle]] ──┬──► [[Forward contract]] / [[Future contract]]
                              ├──► [[Put-call parity]] ──► [[Bounds for Option Prices]]
                              └──► [[Call option]] / [[Put option]] ──► [[American Options]]

[[Interest rate models]] ──┬──► [[Vasicek Model]]
                            ├──► [[Cox-Ingersoll-Ross (CIR) Process]]
                            └──► [[Hull-White Model]]

[[Credit Risk]] ──┬──► [[Merton Model (Credit Risk)]]  (uses [[Black-Scholes formula]])
                   └──► [[Reduced-Form Credit Risk Model]]  (uses [[Hazard Function]])
```

---

## Exam focus

High-priority topics (recur across problem sheets, past papers, and revision questions):
- The Black-Scholes-Merton derivation end-to-end: SDE → PDE (replicating-portfolio proof) → closed-form formula (risk-neutral-expectation proof) → Greeks. Examiners ask for the *proof*, not just the formula.
- Binomial trees: one-step and two-step replicating-portfolio/risk-neutral pricing by hand, American early exercise, and the CRR calibration of $u,d$ to volatility.
- Change of measure: stating Girsanov's theorem correctly, and reproducing the "$e^{-rt}S_t$ is a $Q$-martingale iff $\mu=r$" argument.
- Put-call parity, including the discrete-dividend adjustment, and the option-price-bound portfolio arguments (why American calls on non-dividend stocks are never exercised early).
- Delta/Gamma/Theta/Vega derivations from the Black-Scholes formula (the appendix proofs, especially the $SN(d_1)=Ke^{-rT}N(d_2)$ lemma), and constructing delta-/gamma-neutral portfolios.
- Interest-rate models: writing down the Vasicek/CIR/Hull-White SDEs from memory, and the market-price-of-risk change-of-measure argument for bond pricing.
- Merton's credit risk model: equity-as-a-call-option setup, computing risk-neutral vs real-world default probability, distance to default.
- Implied volatility: the iterative/interpolation calculation (past papers ask for this by hand).

Common question types seen in the Problem Sheets, Past Papers, Mock tests, and Revision Questions:
- "Derive/prove..." questions on the BSM PDE, the Black-Scholes formula, or a Greek — full derivation expected, not just the result.
- Numerical binomial-tree pricing (one or two steps, European and American).
- Numerical Black-Scholes/Garman-Kohlhagen pricing given $S,K,r,\sigma,T$ (and $q$).
- Implied volatility by iteration/interpolation.
- Put-call parity numerical checks and the discrete-dividend variant.
- Merton-model default probability calculations (real-world vs risk-neutral).
- Short-answer/definition questions on model assumptions and shortcomings (fat tails, volatility smile).

## Open questions

- [ ] **Shared canonical prerequisite notes not touched in this session.** [[Brownian motion]], [[Geometric Brownian Motion]], [[Martingale]], [[Filtration]], [[Stopping time]], [[Ito's Lemma]], [[Normal distribution]], [[Lognormal distribution]], [[Moment Generating Function]] (and its duplicate-cased [[Moment generating function]]), [[Random Variable]], and [[Probability Space]] all already exist as empty/seeding stubs under `03 Stochastic Processes` and `02 Probability & Statistics/Probability Theory`. MA320's Chapters 2–3 slides derive most of their core properties in full (moments of Brownian motion via MGF, the Markov/martingale properties, the Itô multiplication table, the heuristic derivation of Itô's Lemma) — genuinely canonical content that would fill those stubs well. Not done here, to keep this session's diff scoped to the Financial Derivatives folder and avoid attributing MA320-sourced material to the Stochastic Processes / Probability Theory course frontmatter (same rationale as the Stochastic Optimization session, §12 of the vault strategy doc). Worth a short, explicitly cross-course follow-up pass.
- [ ] **Two scanned (image-only) PDFs required OCR**: `Chapter 4/OptionStrategies.pdf` and `Chapter 9/Chapter 8 IRDerivativesSummary.pdf`. OCR quality was good for OptionStrategies but the last 4 of 17 strategies (long/short call ladder, long/short call butterfly) produced unreadable text — [[Option Trading Strategies]] drafts those four from canonical knowledge only, flagged `UNVERIFIED`. The IR derivatives OCR was handwriting-heavy and noisy in places (Vasicek/CIR derivations) — cross-check [[Interest rate models]] and [[Vasicek Model]] against the original scan.
- [ ] **Duplicate/near-duplicate source files not fully reconciled**: Chapter 1 has two PDFs (a prose version and a slide-deck version of the same content — both used); Chapter 8's file is misnamed `The Greeks.pdf` but is actually the Risk-Neutral Pricing chapter (folder location was trusted over the filename); Chapter 10's file is internally numbered "Chapter 9" (the course's internal PDF numbering runs one behind the vault's folder numbering throughout — folder numbering was used consistently).
- [ ] **Not yet ingested from this course's Resources**: `Lab Material/` workbooks (6 labs + mock tests, mostly Excel spreadsheets applying the same formulas numerically — skimmed for context, not mined example-by-example); `Past Papers/MOCK` and `Past Papers/TEST` (2023–2026 sittings) and `Problems/` solution PDFs were read for verification/examples but not exhaustively cross-checked line-by-line against every drafted note.
- [ ] Confirm whether [[Option Trading Strategies]]' four UNVERIFIED strategies (ladders, butterflies) match the exact payoff-table convention O'Hara used in the original slide (the OCR lost the diagrams).
- [ ] Decide whether [[Digital Options|the asset-or-nothing/cash-or-nothing decomposition]] used in the employee-share-scheme revision question deserves its own atomic note — currently folded into [[Black-Scholes formula]]'s Examples.
