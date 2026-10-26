---
subject: Stochastic Processes
type: MOC
exam_date: 2026-05-13
status: seeding
confidence: 1
tags:
  - moc
  - exam
  - stochastic-processes
domain: Stochastic Processes
---
## Concept narrative

The course begins by defining **stochastic processes** through their time and space dimensions (discrete vs. continuous) and the nature of their **increments** (stationary and independent). The **Simple Random Walk (SRW)** serves as the primary example, introducing core properties like time and spatial **homogeneity** and the **Gambler's Ruin** problem, which is solved via a **second order difference equation** — a technique reused throughout the course. Chapter 1 also introduces a family of named example processes built from these primitives: **counting processes**, **renewal processes**, the **surplus (Cramér–Lundberg) process**, **martingales**, **Brownian motion**, and **geometric Brownian motion**.

This leads into the broader study of **Discrete-Time Markov Chains (DTMC)**, where the **transition matrix** and **Chapman-Kolmogorov equations** govern how systems evolve over multiple steps. We then classify states as **recurrent, transient, or absorbing**, group them into **irreducible classes** with a well-defined **period**, and determine if a process reaches a **stationary** or (strictly stronger) **equilibrium** distribution — the latter governed by the Markov-chain **ergodic theorem**.

Moving to continuous time, the **Poisson Process** (the special renewal process with i.i.d. exponential inter-arrival times) motivates **Markov jump processes** in general, specified by a **generator matrix** whose entries give instantaneous transition rates; the **Kolmogorov forward (and backward) equations** describe how the transition probabilities evolve from that generator.

Finally, the course covers **Time Series Analysis**, building **MA, AR, and ARMA processes** out of **white noise**, and studying their stationarity, invertibility, and predictive power via the **autocorrelation** and **partial autocorrelation functions**.

---

## Concept map

### Foundations & Random Walks

- [[Stochastic Process]]: continuous vs. discrete time/space — see [[State space and time classification]] for all 5 combinations
- [[Stationary Increments]] vs [[Independent Increments]]; [[Markov Property]] (general definition)
- [[Simple Random Walk]]: $S_n = S_0 + \sum_t {X_t}$, built on [[Random Walk]]
- [[Spatial Homogeneity]] and [[Time Homogeneity]]
- [[Second Order Difference Equation]]: the technique behind the derivations below
- [[Gambler's Ruin]]: ruin probability $y_k$ and [[Absorbing State|absorbing states]]
- Named example processes (Ch.1): [[Counting Process]] → [[Renewal process]] → [[Poisson Process]]; [[Surplus Process]] (Cramér–Lundberg); [[Martingale]]; [[Brownian motion]] → [[Geometric Brownian Motion]]
- Summary statistics of a process: [[Mean function]], [[Cross-moment function]], [[Autocovariance function]]; [[Weak Stationarity]] vs [[Strong Stationarity]]
- [[Ballot Theorem]]: a combinatorial result used in the random-walk unit

### Discrete-Time Markov Chains (DTMC)

- [[Discrete-Time Markov Chain]]: defined by the [[Markov Property]] on a discrete state space
- [[Transition Matrix]]: $P$ and $n$-step transitions $P^n$
- [[Transition Graph]]: visualizing state movements
- [[Chapman-Kolmogorov Equation]]: $p_{ij} ^{(m+n)} = \sum_k p_{ik}^{(m)} p_{kj}^{(n)}$
- [[Stationary Distribution]]: solving $\pi P = \pi$ (may be non-unique on a reducible chain)
- [[Equilibrium Distribution]]: limit of $p^{(0)}P^n$ as $n \to \infty$ for *every* $p^{(0)}$ — strictly stronger than stationarity
- [[Ergodic theorem]]: irreducible + positive recurrent + aperiodic ⇒ unique stationary distribution *is* the equilibrium distribution; $\pi_j = 1/\mu_j$

### State Classification & Periodicity

- [[Irreducible Class]]: states that communicate with each other
- [[Absorbing State]]: state $i$ where $p_{ii} = 1$
- [[Recurrent State]] vs [[Transient State]]: probability of revisiting, $f_{ii}$
- [[Period of States]]: greatest common divisor of possible return steps

### Continuous-Time & Jump Processes

- [[Poisson Process]]: rate $\lambda$, [[Independent Increments]], and $N(t) \sim \text{Poisson}(\lambda t)$; special case of [[Renewal process]]
- [[Markov Jump Process]]: continuous-time homogeneous chains; holding times, embedded jump chain, MLE of rates
- [[Generator Matrix]]: $Q = P'(0)$, rows sum to $0$
- [[Kolmogorov Forward Equations]]: $P'(t) = P(t)Q$ (backward equations $P'(t) = QP(t)$ covered as a subsection there too)

### Time Series Analysis

- [[White Noise]]: the i.i.d./uncorrelated building block of every model below
- [[Moving Average Process]]: $MA(q)$ mean, variance, and autocorrelation (finite memory: $\gamma_s = 0$ for $s>q$)
- [[Autoregressive Process]]: $AR(p)$ processes, Yule-Walker equations, and stationarity
- [[ARMA Process]]: combined $ARMA(p,q)$ models; $ARIMA(p,d,q)$ generalization
- [[Stationarity]]: characteristic-polynomial root condition for AR/ARMA (links out to [[Weak Stationarity]]/[[Strong Stationarity]] for the general definition)
- [[Invertibility]]: requirements on the roots of the $MA$ characteristic equation
- [[Autocorrelation Function]]: ACF and PACF, and their cutoff/decay "signature" pair for MA vs. AR
- [[Prediction]]: computing $\hat{y}_{t+n} = E(y_{t+n} \mid \mathcal{F}_t)$

---

## Key dependency chains

```
Stationary/Independent Increments + Markov Property → Simple Random Walk → Second Order Difference Equation → Gambler's Ruin
Counting Process → Renewal process → Poisson Process → Surplus Process
                                                       ↘ Markov Jump Process
Transition Matrix → Chapman-Kolmogorov → n-step Probabilities → Irreducible Class/Period → Recurrence/Transience → Stationary Distribution → Ergodic theorem → Equilibrium Distribution
Poisson Process → Generator Matrix → Markov Jump Process → Kolmogorov Forward/Backward Equations
White Noise → MA/AR Processes → ARMA → Stationarity/Invertibility → Autocorrelation Function → Prediction
Brownian motion → Geometric Brownian Motion (martingale when μ=0)
```
---
## Exam focus

### **High priority**: appeared in revision questions:

- **SRW Proofs:** Proving time or spatial homogeneity; solving the Gambler's Ruin second order difference equation (both $p\neq q$ and $p=q$ cases).
- **DTMC Calculations:** Finding $P^n$, $p^{(n)}$, and solving for stationary distributions $\pi$ via $\pi P = \pi$; general vs. detailed balance equations.
- **Classification:** Identifying irreducible classes, periods, and recurrence/transience via first-step analysis and geometric-series first-return computations $f_{ii}^{(n)}$; using the **class property** (recurrence/transience/period are constant on an irreducible class) as a shortcut.
- **Stationary vs. equilibrium (named exam trap):** a reducible chain ⇒ non-unique stationary distribution; a periodic-but-irreducible chain ⇒ unique stationary distribution but *no* equilibrium (limit doesn't exist).
- **CTMC Calculations:** constructing the generator matrix $Q$ from a rate diagram, solving $\pi Q = 0$ for the stationary distribution, writing Kolmogorov forward equations for specific entries $p_{ij}'(t)$, computing expected holding times $-1/q_{ii}$. Watch the "gotcha": $q_{ii}=0$ (not $1$) for an absorbing state, even though $p_{ii}(t)=1$.
- **Poisson Processes:** Calculating $P(N(t) > k)$ and using independent increments for conditional probabilities/expectations across disjoint intervals (e.g. $\Pr(N(1)=1\mid N(3)=5)$).
- **Time Series Properties:** Checking invertibility/stationarity ranges for parameters via characteristic-polynomial roots, and reading off model order from the ACF/PACF cutoff-vs-decay "mirror" signature (MA cuts off ACF, decays PACF; AR decays ACF, cuts off PACF).
- **ARMA Prediction:** Deriving expressions for $\hat{y}_{t+n}$ and comparing forecast accuracy (MSE) across candidate models — a real past-exam question type.

### Common Question Types:

- "Prove that the process has independent increments."
- "Calculate the probability that the gambler will ruin if $S_0 = 1$."
- "Find the range of $a$ for which the ARMA process is stationary."
- "Write down the Kolmogorov forward equations for a Poisson process."
- "Construct the generator matrix from a described transition-rate diagram, and find the stationary distribution."
- "Given a model's ACF/PACF plot, identify the order $(p,q)$."

---

## Open questions

- _How does the transition from DTMC to CTMC change the way we calculate stationary distributions (generators vs. transition matrices)?_
- _What is the specific relationship between the roots of the characteristic equation and the visual behavior of an ARMA process?_
- The lecture corpus reviewed (Chapters 1–6, revision lectures, formula sheet) never covers **Filtration**, **Stopping time**, **Optional stopping theorem**, or **Ito's Lemma** — these remain empty stubs in the vault. They may belong to a more advanced/different course (e.g. a stochastic calculus or mathematical finance module) rather than MA319; left unfilled rather than fabricated.
- **Kolmogorov Backward Equations** and **Generator Matrix** are both used constantly but the backward equations are currently only a subsection of [[Kolmogorov Forward Equations]] rather than their own note — consider promoting if they turn out to be independently examinable.
- The official "PG Lecture 1" notes containing the proof that a simple random walk returns to $0$ with probability $1-|p-q|$ (deferred to postgraduate students in the main lecture) appear to be missing from the available source corpus — only PG Lectures 2 and 3 were found. The vault's [[Simple Random Walk]] note already contains a self-consistent proof of this result via the Gambler's Ruin limiting argument, but it hasn't been cross-checked against the official PG notes; worth re-sourcing from Moodle if that specific proof technique matters for revision.
- [[Ergodic theorem]] here and [[Ergodic Markov Chain]] in the (unrelated) Stochastic Optimization course domain cover the same underlying result from two different courses' lecture material and haven't yet been merged into one canonical note.
- Minor unresolved concepts referenced in passing but without their own note: **conditional expectation**, **linearity of expectation** (general probability-theory primitives), **lag/difference operator** (time-series notational shorthand).
