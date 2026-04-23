---
subject: Mathematics of Portfolios
type: MOC
exam_date: 2026-06-04
status: seeding
confidence: 1
tags:
  - moc
  - mathematics-of-portfolios
  - exam
---
## Concept narrative

%% Write 4–6 lines in your own words. How do these ideas build on each other? This paragraph is the most important section for Smart Connections queries — prose outperforms bullet lists. %%

The subject begins with **how investors think**: utility functions formalise preferences over wealth, and risk aversion determines whether an investor prefers a sure thing or a gamble. From there, **stochastic dominance** gives us a way to rank risky investments without specifying a utility function. Once we can describe preferences, we ask how to **measure risk** numerically — through variance, VaR, TVaR, and expected shortfall. With a risk measure in hand, **portfolio theory** asks how to combine assets to maximise return per unit of risk, leading to the Markowitz model and the capital market line. **Asset pricing models** (CAPM, APT, single-index) then explain how equilibrium returns arise when all investors optimise simultaneously. Finally, **ruin theory** applies probability to the insurer's surplus process — a separate but related strand that asks how long you survive before losses exceed reserves, with chain ladder methods used to estimate those reserves.

---

## Concept map

### Utility theory

%% foundational — must understand before portfolio theory %%

- [[Utility function]] → [[Expected utility]]
- [[Non-satiation]]
- [[Risk aversion]] — covers risk-averse / neutral / seeking (U''(x) condition)
- [[Absolute Risk Aversion]] — ARA = −U''(x)/U'(x)
- [[Relative Risk Aversion]]

### Stochastic dominance

%% ranks portfolios without specifying utility — links to utility theory %%

- [[First-order stochastic dominance]] — FA(x) ≤ FB(x) for all x
- [[Second-order stochastic dominance]] — integral condition

### Risk measures

%% quantify downside — used in portfolio construction and regulation %%

- [[Variance and semi-variance]]
- [[Shortfall probability]]
- [[Expected shortfall]]
- [[Value at Risk]] — VaR: discrete vs continuous definition
- [[Tail Value at Risk]] — TVaR: ES when L = VaR percentile

### Portfolio theory

%% core of the course — builds on utility and risk measures %%

- [[Portfolio expected return]]
- [[Portfolio variance]]
- [[Markowitz model]] — mean-variance optimisation with riskless asset
- [[Optimal risky portfolio]] — maximise Sharpe ratio, solve Zi system
- [[Capital market line]] — E(Rp) = RF + σp · (E(Rm)−RF)/σm

### Asset pricing

%% equilibrium models — require portfolio theory as foundation %%

- [[Arbitrage Pricing Theory]] — E(Ri) = λ0 + λ1·bi1 + λ2·bi2
- [[Arbitrage portfolio]] — construction when asset is off the APT plane
- [[CAPM]] — derived from APT with Rm as single factor
- [[Security market line]] — E(Ri) = RF + βi·(E(Rm)−RF)
- [[Single-index model]] — Ri = αi + βi·Rm + εi

### Ruin theory and reserving

%% actuarial strand — more standalone, but uses probability foundations %%

- [[Surplus process]] — U(t) = u + ct − S(t)
- [[Aggregate claims process]]
- [[Adjustment coefficient]] — λ + cR = λ·Mx(R)
- [[Lundberg's inequality]] — ψ(u) ≤ e^(−Ru)
- [[Probability of ruin]]
- [[Chain ladder method]] — development factors and reserve estimation
- [[Inflation-adjusted chain ladder]]
- [[Average Cost Per Claim method]]

---

## Key dependency chains

These are the sequences to study in order — each arrow means "must understand before":

```
Utility function → ARA/RRA → Risk preferences
Prior knowledge: PDF/CDF/Expectation/Variance (from Probability Theory)

Portfolio E[R] / Var → Markowitz model → Optimal risky portfolio → CML
Stochastic dominance: parallel strand, uses CDF directly

APT → (set factor = Rm) → CAPM → SML
Single-index model: parallel to APT, same β intuition

Surplus process → Adjustment coefficient → Lundberg's inequality → ψ(u)
Chain ladder: independent — data-driven, no probability model needed
```

---

## Exam focus

%% Fill this as you study. What themes keep appearing in past papers? What does your lecturer emphasise? What are you finding hardest? %%

**High priority** — appeared in revision questions:

- ARA calculation from U(x)
- VaR and TVaR for discrete distributions
- Optimal portfolio weights (solving the Zi system)
- APT plane: finding λ values and checking dominance
- Single-index model: α, residuals, σ²
- Adjustment coefficient and Lundberg bound
- Chain ladder development factors and reserves

**Likely on exam but not in revision questions:**

- Inflation-adjusted chain ladder
- Average Cost Per Claim method
- CML derivation

## **Known weak spots:**

**Exam format reminders:**

- 120 minutes, open book (restricted), formula sheet provided
- Mock exam and past papers on Moodle

---

## Open questions

## %% Things you don't understand yet — ask Ollama or your lecturer %%