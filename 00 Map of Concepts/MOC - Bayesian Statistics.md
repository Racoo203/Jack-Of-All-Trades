---
subject: Bayesian Statistics
type: MOC
exam_date: 2026-06-04
status: drafted
confidence: 0
tags:
  - moc
  - bayesian-statistics
  - exam
domain: Probability & Statistics
---
# Bayesian Statistics — Map of Content

> This subject (MA318, taught by Dr Yanchun Bao) is about a single question asked two ways: given data and a statistical model, what do we believe about the unknown parameter — and how should that belief drive a decision? Classical statistics answers with point estimates and pre-data error control; Bayesian statistics answers by treating the parameter itself as random and updating a prior belief into a posterior belief via [[Bayes' theorem]]. The course builds from that single update rule up through decision theory, hypothesis testing, credibility (an actuarial application of exactly the same posterior-mean machinery), and finally the machinery needed to describe insurer solvency (compound risk models, ruin theory) and regression.

## Concept narrative

The course opens by drilling the classical toolkit (Chapter 1–2): distributions, the [[Likelihood function]], and the [[Maximum Likelihood Estimate]], together with [[Classical Hypothesis Testing]] and the [[Confidence Interval]] — the frequentist baseline every Bayesian idea is later contrasted against. Chapter 3 is the pivot: [[Bayes' theorem]] turns a [[Prior distribution]] and a likelihood into a [[Posterior distribution]], and the [[Exponential family]] structure explains *why* [[Conjugate prior|conjugate priors]] exist and stay closed under sampling — with [[Jeffrey's prior]] (built from [[Fisher Information]]) supplying an "objective" prior when none is available. The same posterior machinery immediately gives both point summaries ([[Bayes estimate]], via [[Posterior distribution|posterior mean/median/mode]]) and interval summaries ([[Credible Interval]], contrasted directly with the [[Confidence Interval]]), plus forward-looking summaries ([[Prior predictive distribution]], [[Posterior predictive distribution]]).

Chapter 4 formalizes *why* the posterior mean/median/mode are the "right" answers: decision theory wraps a [[Loss function]] around the posterior to define [[Bayes risk]] and hence the [[Bayes estimate]] itself, with [[Minimax estimator|minimax]] as the frequentist-flavoured alternative criterion. Chapters 5–6 are two applications of the same posterior-updating idea: [[Bayesian hypothesis testing]] (with the [[Bayes factor]] as its headline diagnostic, and [[Highest Posterior Density (HPD) Credible Set|HPD sets]] generalizing credible intervals) and [[Bayesian Credibility Theory]] (where the posterior mean literally *is* the actuarial credibility formula, and [[Empirical Bayes]] shows how to estimate the prior's hyperparameters from data when no genuine prior belief exists).

The final third pivots from parameter inference to modelling aggregate risk. [[Convolution]] and the [[Moment Generating Function]] are the technical tools for finding the distribution of a sum of claims; the [[Collective Risk Model]] and [[Mixed Poisson Distribution]] describe the claim-count/claim-size decomposition actuaries use in practice; [[Reinsurance]] shows a real use of that aggregate distribution; and [[Ruin Theory]] with [[Adjustment Coefficient and Lundberg's Inequality|Lundberg's inequality]] extends the static risk model into continuous time to bound an insurer's probability of insolvency. The course closes with [[Bayesian Linear Regression Model]], showing that under a non-informative prior the entire apparatus — posterior mean, posterior variance, posterior predictive distribution — reproduces classical OLS exactly, tying the whole course back to its classical starting point.

---

## Concept map

### Chapter 1 — Preliminary (classical/probability refresher)
- [[Random Variable]] → [[Probability Density Function (PDF) | PDF]] / [[Probability Mass Function (PMF) | PMF]] → [[Cumulative Distribution Function (CDF) | CDF]]
- [[Independent and Identically Distributed (i.i.d) | i.i.d]]
- [[Distribution of a Function of a Random Variable]] # change-of-variable theorem

### Chapter 2 — Classical Methods of Statistics
- [[Likelihood function]] → [[Maximum Likelihood Estimate]] # differentiate log-likelihood
- [[Point estimation]] # bias, and other desirable properties of an estimator
- [[Sufficient statistic]] # factorization theorem
- [[Classical Hypothesis Testing]] → [[Confidence Interval]] # Type I/II error, critical region ↔ acceptance region

### Chapter 3 — Bayesian Inference (the core chain — this is what exams test)
- [[Prior distribution]] → [[Likelihood function]] → [[Posterior distribution]]
- [[Bayes' theorem]] # the mechanism connecting the chain above
- [[Exponential family]] → [[Conjugate prior]] # closed under sampling; Beta/Gamma/Normal worked examples
- [[Fisher Information]] → [[Jeffrey's prior]] # non-informative, reparameterization-invariant prior
- [[Prior predictive distribution]] → [[Posterior predictive distribution]]
- [[Credible Interval]] # Bayesian — compare with:
- [[Confidence Interval]] # frequentist
- [[Credible interval vs Confidence interval]] # explicit comparison note

### Chapter 4 — Bayesian Decision Theory
- [[Loss function]] # quadratic → posterior mean; absolute → posterior median; 0-1 → posterior mode
- [[Bayes risk]] → [[Bayes estimate]] # pointwise minimization of posterior expected loss
- [[Minimax estimator]] # worst-case criterion; randomized estimators

### Chapter 5 — Bayesian Hypothesis Testing
- [[Bayesian hypothesis testing]] # loss-based accept/reject rule
- [[Bayes factor]] # posterior odds / prior odds; reduces to likelihood ratio for simple vs simple
- [[Highest Posterior Density (HPD) Credible Set]] # generalizes Credible Interval to arbitrary subsets

### Chapter 6 — Empirical Bayes and Bayesian Credibility
- [[Empirical Bayes]] # estimate prior hyperparameters from the predictive distribution
- [[Hierarchical model]] # contrast: full uncertainty propagation vs. Empirical Bayes' point-estimate plug-in
- [[Bayesian Credibility Theory]] # posterior mean = credibility-weighted average; Poisson/Gamma & Normal/Normal

### Chapter 7 — Reinsurance, Convolution and CLT
- [[Reinsurance]] # stop-loss, proportional/non-proportional
- [[Convolution]] → [[Central Limit Theorem (CLT)]] # exact vs. approximate distribution of a sum
- [[Moment Generating Function]] # mgf of a sum = product of mgfs

### Chapter 8 — Risk Theory
- [[Collective Risk Model]] # S = X_1+...+X_N; compound distribution mean/variance/mgf
- [[Mixed Poisson Distribution]] # overdispersion, Poisson-mixture claim counts
- [[Ruin Theory]] # surplus process, infinite/finite ruin probability, premium loading
- [[Adjustment Coefficient and Lundberg's Inequality]] # ψ(u) ≤ e^{-Ru}

### Chapter 9 — Bayesian Linear Regression
- [[Bayesian Linear Regression Model]] # non-informative prior ⇒ Bayesian posterior mean = classical OLS estimate

---

## Key dependency chains

```
[[Bayes' theorem]]
      │
      ▼
[[Prior distribution]] ──┬──► [[Posterior distribution]] ──┬──► [[Bayes estimate]] (via [[Loss function]] / [[Bayes risk]])
      │                  │                                 ├──► [[Credible Interval]] / [[Highest Posterior Density (HPD) Credible Set]]
      ▼                  │                                 └──► [[Posterior predictive distribution]]
[[Exponential family]]   │
      │                  │
      ▼                  │
[[Conjugate prior]] ─────┘

[[Fisher Information]] ──► [[Jeffrey's prior]]  (non-informative prior, feeds into [[Bayesian Linear Regression Model]])

[[Likelihood function]] ──► [[Maximum Likelihood Estimate]] ──► [[Point estimation]] (bias)
                       └──► [[Sufficient statistic]] ──► [[Exponential family]]

[[Classical Hypothesis Testing]] ──► [[Confidence Interval]] ──► [[Credible interval vs Confidence interval]]

[[Bayesian Credibility Theory]] ◄── [[Posterior distribution]] (posterior mean = credibility formula)
[[Empirical Bayes]] ──► [[Hierarchical model]] (contrast)  ──► [[Bayesian Credibility Theory]]

[[Convolution]] / [[Moment Generating Function]] ──► [[Collective Risk Model]] ──► [[Mixed Poisson Distribution]]
                                                                              └──► [[Ruin Theory]] ──► [[Adjustment Coefficient and Lundberg's Inequality]]

[[Posterior distribution]] + [[Jeffrey's prior]] ──► [[Bayesian Linear Regression Model]]
```

---

## Exam focus

**High priority**

- The core Bayes chain: derive a posterior from a stated likelihood + prior, identify the [[Conjugate prior]] family, and report the posterior mean/mode/[[Credible Interval]] — this pattern (Beta-Binomial, Gamma-Poisson, Normal-Normal) recurs across Chapters 3, 6, and 9.
- [[Bayes risk|Bayes estimator]] derivations under the three standard loss functions (quadratic/absolute/0-1) — know which posterior summary each one produces, and be able to reproduce the proofs, not just quote the results.
- [[Bayesian Credibility Theory]]: both worked models (Poisson/Gamma claim frequency, Normal/Normal pure premium) and the credibility factor $\delta$ derivation — a strong candidate for a full past-paper question given the actuarial framing of the whole module.
- [[Adjustment Coefficient and Lundberg's Inequality]]: setting up and solving $\lambda+cR=\lambda m_X(R)$ for standard claim distributions (exponential is the canonical worked case), and being able to state (if not fully reprove) Lundberg's inequality.
- [[Bayes factor]] calculations, including the atom-prior construction for testing a point null.

**Known weak spots**

- [[Sufficient statistic]] and general [[Exponential family]] theory are not derived from first principles anywhere in the lecture slides (see the `UNVERIFIED` flag on [[Sufficient statistic]]) — worth checking against a textbook (e.g. Casella & Berger) before exam season, since the *idea* is used implicitly throughout Chapter 3 even though the formal factorization theorem is never stated in the slides.
- [[Hierarchical model]] is drafted canonically (flagged `seeding`/`UNVERIFIED`) since Chapter 6's slides only cover Empirical Bayes, not full multi-level hierarchical models — check whether MA322 (Bayesian Computational Statistics) covers this instead, or whether it's genuinely outside this module's scope.
- The multivariate-$t$ result for the [[Bayesian Linear Regression Model]] posterior predictive distribution is explicitly flagged non-examinable in the slides — don't over-invest study time there.

**Likely exam question types**

- "State the prior/likelihood, derive the posterior, and give the Bayes estimate under loss function X" — the single most repeated skeleton across the whole module.
- A ruin-theory question: set up $U(t)=u+ct-S(t)$, compute $E[S]$/$\text{Var}[S]$ for a two-portfolio aggregate, then either a Normal-approximation initial-capital question or a Lundberg-bound question.
- A reinsurance/compound-distribution expected-value integral (piecewise payoff function, as in [[Reinsurance]]).
- A Bayes-factor or credible-set calculation with a named non-conjugate-looking prior (e.g. Pareto, as in [[Bayes factor]]'s worked example) — these test whether the general formula, not just the conjugate special cases, is understood.

---

## Open questions

- Past exam papers exist for 2015–2025 (two sittings per year, `Resources/.../Past Papers/`) but have not yet been cross-checked against these notes — worth a pass to confirm notation/scope match and to mine for further worked examples once the notes are reviewed.
- `Lab Material/` (4 labs + 2 mock tests, R scripts and `.Rmd` files) has not been reviewed — may contain computational/simulation conventions (e.g. how posterior simulation is actually coded) worth cross-referencing, especially for the [[Bayesian Linear Regression Model]] and [[Bayesian Credibility Theory]] notes.
- `Exercises & Solutions/` subfolders per chapter were only spot-checked for Chapters 1–2; Chapters 3–9 exercises have not been systematically mined for additional worked examples or idiosyncratic exam-style notation.
- Chapter 5's `Exercise_ch5` / `Exercise_solutions_ch5` were not extracted in this pass — worth a follow-up to confirm the [[Bayes factor]] and [[Bayesian hypothesis testing]] notes cover everything examinable.
- Confirm whether [[Hierarchical model]] is actually taught anywhere in this module's syllabus (see Known weak spots above) before bumping its status past `seeding`.
