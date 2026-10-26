---
subject: Stochastic Optimization
type: MOC
course_code: MA2004B
course_name_es: "Optimización Estocástica"
domain: Optimization & Control
level: BSc
status: drafted
confidence: 0
tags:
  - moc
  - exam
  - stochastic-optimization
  - control-theory
---
## Concept narrative

MA2004B is Tec de Monterrey's undergraduate course on decision-making and modeling under uncertainty, and it stitches together four largely independent toolkits rather than building one continuous theory. It opens with **applied [[Discrete-Time Markov Chain|Markov chains]]**: given a transition matrix, classify states, decide whether the chain is **ergodic**, and compute its long-run behavior either by solving $\pi = \pi P$ directly or, more distinctively for this course, by taking the **spectral decomposition** $P = Q\Lambda Q^{-1}$ and isolating the eigenvalue-1 term as $n \to \infty$. The second thread is classical **decision analysis**: given a payoff matrix over alternatives and states of nature, choose an action under *uncertainty* (no probabilities — Laplace, Wald, Maximax, Savage) or under *risk* (probabilities known — expected monetary value, [[Expected Value of Perfect Information]], [[Expected Opportunity Loss]]). This escalates into genuine **two-stage stochastic programming**: the canonical farmer's problem shows how a first-stage decision (planting areas) must be fixed before uncertainty (crop yield) resolves, how the extensive form encodes recourse decisions per scenario, and how [[Value of the Stochastic Solution|VSS]] and EVPI quantify what modeling the uncertainty is actually worth — extended to a risk-averse, mean-risk objective for an international sourcing problem. The third thread is **discrete-event simulation**: the [[Problem-Solving Cycle for Mathematical Modeling|problem-solving cycle]] frames simulation as one modeling strategy among several, the [[Monte Carlo Method]] is motivated rigorously via the Law of Large Numbers and Central Limit Theorem, and a full unit on **[[Pseudorandom Number Generator|pseudorandom number generation]]** (mid-square, mid-product, linear/multiplicative congruential generators, and the statistical tests used to validate them) supplies the raw uniforms that drive it. Finally, **[[Queueing System|queueing theory]]** ties several earlier threads together: a queue's state (number of customers present) evolves as a birth-death Markov chain, its steady-state probabilities are found exactly the way the first unit found $\pi$, and simulation is the fallback whenever the arrival/service assumptions ($M/M/\cdot$) don't hold in closed form. Across the whole course the recurring meta-lesson, made explicit in the farmer's problem, is that a model built on point estimates (expected values) systematically differs from — and is dominated by — a model that explicitly represents the scenarios.

---

## Concept map

### Unit 1 — Markov Chains (applied)

- [[Discrete-Time Markov Chain]], [[Markov Property]], [[Transition Matrix]], [[Chapman-Kolmogorov Equation]] — canonical definitions, linked from `03 Stochastic Processes` (not duplicated here; see Open Questions)
- [[Irreducible Class]], [[Recurrent State]], [[Transient State]], [[Absorbing State]], [[Period of States]] — state classification, also linked from `03 Stochastic Processes`
- [[Ergodic Markov Chain]]: irreducible + aperiodic $\Rightarrow$ unique limiting/[[Stationary Distribution]]
- [[Mean Recurrence Time]]: $\mu_j = 1/\pi_j$ for an ergodic chain
- [[Spectral Decomposition of a Transition Matrix]]: $P^n = Q\Lambda^nQ^{-1}$, isolating $\lambda=1$ as $n\to\infty$

### Unit 2 — Decision Analysis

- [[Decision Making Under Uncertainty]]: payoff matrix, alternatives $a_i$, states of nature $s_j$
  - [[Laplace Criterion]], [[Wald Criterion]], [[Maximax Criterion]], [[Savage Criterion]]
- [[Decision Making Under Risk]]: expected monetary value $E(A_i) = \sum_j v_{ij}P(s_j)$
- [[Expected Value of Perfect Information]] (EVPI): $EVPI = ECPI - EMV^*$
- [[Expected Opportunity Loss]] (EOL): $\arg\min_i EOL(a_i) = \arg\max_i E(a_i)$, and at the optimum $EOL = EVPI$

### Unit 3 — Stochastic Programming

- [[Two-Stage Stochastic Programming]]: first-stage vs. recourse (second-stage) decisions, scenarios, extensive form — the farmer's problem
- [[Value of the Stochastic Solution]] (VSS): $VSS = EEV - RP$
- [[Risk-Averse Stochastic Programming]]: mean-risk objective, risk-aversion weight $w$

### Unit 4 — Simulation Methodology & Monte Carlo

- [[Problem-Solving Cycle for Mathematical Modeling]]: reality $\to$ problem $\to$ model $\to$ algorithm $\to$ solution $\to$ interpretation $\to$ implementation
- [[Monte Carlo Method]]: motivated by the Weak Law of Large Numbers and the Central Limit Theorem

### Unit 5 — Pseudorandom Number Generation

- [[Pseudorandom Number Generator]]: uniformity + no serial correlation
  - [[Mid-Square Method]], [[Mid-Product Method]] — non-congruential, degenerate quickly
  - [[Linear Congruential Generator]], [[Multiplicative Congruential Generator]] — congruential, full-period selection rules
- [[Chi-Square Goodness-of-Fit Test for Randomness]]: validating a generator's output
- [[Inverse Transform Sampling]] (canonical method, linked from `02 Probability & Statistics`) $\to$ [[Discrete-Event Simulation of a Poisson Process]] (this course's worked application)

### Unit 6 — Queueing Theory

- [[Queueing System]]: arrival process, service process, servers, capacity, discipline — a [[Birth-Death process|birth-death process]] on the number-in-system
- [[Kendall's Notation]]
- [[Traffic Intensity]] $\rho = \lambda/\mu$, [[Little's Law]] $L = \lambda W$
- [[M-M-1 Queue|M/M/1 Queue]], [[M-M-1-N Queue|M/M/1/N Queue]], [[M-M-s Queue|M/M/s Queue]], [[M-M-s-N Queue|M/M/s/N Queue]]

---

## Key dependency chains

```
Markov Property → Discrete-Time Markov Chain → Transition Matrix → Chapman-Kolmogorov Equation
                                                       │
                          State Classification (Irreducible/Recurrent/Period) → Ergodic Markov Chain
                                                       │
                                    Stationary Distribution ←──── Spectral Decomposition of a Transition Matrix
                                                       │
                                              Mean Recurrence Time


Payoff Matrix → Decision Making Under Uncertainty → {Laplace, Wald, Maximax, Savage} Criteria
                          │
              probabilities known
                          ↓
            Decision Making Under Risk (EMV) → Expected Opportunity Loss ⇄ Expected Value of Perfect Information
                          │
                          ↓
            Two-Stage Stochastic Programming (first-stage / recourse, scenarios) → Value of the Stochastic Solution
                          │
                          ↓
            Risk-Averse Stochastic Programming (mean-risk objective)


Problem-Solving Cycle for Mathematical Modeling → Monte Carlo Method → Pseudorandom Number Generator
                                                                              │
                                        {Mid-Square, Mid-Product, Linear/Multiplicative Congruential}
                                                                              │
                                          Chi-Square Goodness-of-Fit Test for Randomness
                                                                              │
                                          Inverse Transform Sampling → Discrete-Event Simulation of a Poisson Process


Queueing System (birth-death process) → Kendall's Notation → Traffic Intensity → Little's Law
                                                                        │
                                        {M/M/1, M/M/1/N, M/M/s, M/M/s/N} Queue
```

---

## Exam focus

### High priority

- **Markov chain classification and long-run behavior**: given a transition matrix, classify every state (recurrent/transient/absorbing, periodic/aperiodic, irreducible or not) and compute the stationary distribution — both by solving $\pi = \pi P$ directly and via spectral decomposition of $P$. Mean recurrence time from $\pi$.
- **Decision criteria under uncertainty**: apply Laplace, Wald (maximin/minimax), Maximax, and Savage to the same payoff matrix and notice they can disagree — this is a recurring exercise format.
- **EMV / EVPI / EOL**: compute the expected value of each alternative, the expected value with perfect information (via the "ECPI/VECIP" intermediate quantity), and confirm $EVPI = EOL$ at the optimal alternative.
- **The farmer's problem (two-stage stochastic programming)**: reproduce the deterministic-equivalent (extensive form) formulation from a scenario tree, and compute EVPI and VSS by comparing the stochastic solution, the wait-and-see solution, and the expected-value solution.
- **Linear congruential generator mechanics**: compute a generated sequence by hand from $X_{n+1} = (aX_n + c) \bmod m$, find its period, and apply the full-period selection rules for $m, a, c, X_0$.
- **Steady-state queueing formulas**: derive (not just recall) $P_n$, $P_0$, $L$, $L_q$, $W$, $W_q$ for $M/M/1$, then adapt the balance equations for finite capacity and/or multiple servers.

### Common question types

- "Model this scenario as a Markov chain and find its transition matrix" (retail/inventory/weather-style word problems).
- "Classify the states of the following chain and determine whether it is irreducible."
- "Given this payoff table, what does each decision criterion recommend, and why do they disagree?"
- "Calculate the EVPI/VSS for this stochastic program."
- "Generate the first $n$ pseudorandom numbers from this LCG and find its period."
- "A queueing system has parameters $\lambda, \mu, s, N$ — find $L, L_q, W, W_q$ and the probability an arriving customer balks."

---

## Open questions

- _Cross-domain naming collisions, deliberately not duplicated:_ [[Discrete-Time Markov Chain]], [[Markov Property]], [[Transition Matrix]], and [[Chapman-Kolmogorov Equation]] already exist (partially drafted) under `03 Stochastic Processes/Discrete-Time Markov Chains/` and `Foundations & Random Walks/`; [[Stationary Distribution]], [[Equilibrium Distribution]], [[Recurrent State]], [[Transient State]], [[Absorbing State]], [[Irreducible Class]], [[Period of States]], [[Poisson Process]], and [[Birth-Death process|Birth-Death process]] exist there as **empty stubs**; [[Inverse Transform Sampling]] exists as an empty stub under `02 Probability & Statistics/Probability Theory/`. This MOC links to all of them rather than creating BSc-flavored duplicates, per the vault's own domain-not-degree design rationale (§1 of `vault-strategy.md`). They're still red/empty in practice — worth a follow-up session scoped to `03 Stochastic Processes` (and a small one for `02/Probability Theory`) to fill them in generically; several of this course's derivations (mean recurrence time, spectral decomposition, the Poisson-process examples) would ground that pass well.
- _Object-oriented simulation implementation in C#_ (`2.2.- Programacion Objetos c#.pptx`) was deliberately **not** turned into a note — it's a generic OOP-in-C# refresher (classes, structs, exceptions, iterators) used as the course's implementation vehicle for Homework 1 (implement the RNGs), not stochastic-optimization content. Flagging in case Raúl wants a `06 Machine Learning & AI` or general-CS note for it later.
- _Not covered anywhere in the resources_: the goodness-of-fit unit only names the chi-square test explicitly (with a passing mention of testing $S$-dimensional uniformity over the hypercube) — the Kolmogorov-Smirnov and runs/serial-correlation tests common in RNG validation aren't in the slides. [[Chi-Square Goodness-of-Fit Test for Randomness]] is drafted canonically and flagged for verification.
- _Chapter/activity dates suggest this course was taken Aug–Nov 2024_ (`Tomadedecisionesbajoincertidumbre.pptx` is dated Agosto 2021 as a template, but Raúl's own homework is dated Nov 2024) — i.e. this is **completed coursework**, not an upcoming exam; it feeds the cumulative BSc exam rather than a course-specific one, so no `exam_date` frontmatter field was set (matching the convention already used for `MOC - Non-linear Optimization`).
- _`Actividad_1.1` (branch-placement decision tree) and `Actividad_3.1`/`Actividad_3.2` (a hands-on carwash queueing data-collection assignment: goodness-of-fit for $M/M/k$ input distributions, then inference on service/interarrival times) are graded-assignment prompts with no worked solution in the resources — worth checking whether Raúl's own submitted solutions exist elsewhere before treating the corresponding notes as fully worked.
