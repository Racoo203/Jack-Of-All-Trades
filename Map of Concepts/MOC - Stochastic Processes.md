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
---
## Concept narrative

The course begins by defining **stochastic processes** through their time and space dimensions (discrete vs. continuous) and the nature of their **increments** (stationary and independent). The **Simple Random Walk (SRW)** serves as the primary example, introducing core properties like time and spatial **homogeneity** and the **Gambler's Ruin** problem. This leads into the broader study of **Discrete-Time Markov Chains (DTMC)**, where the **transition matrix** and **Chapman-Kolmogorov equations** govern how systems evolve over multiple steps. We then classify states as **recurrent, transient, or absorbing** and determine if a process reaches a **stationary or equilibrium distribution**. Moving to continuous time, the **Poisson Process** introduces Markov jump processes and the **Kolmogorov forward equations**. Finally, the course covers **Time Series Analysis**, focusing on the stationarity, invertibility, and predictive power of **MA, AR, and ARMA processes**.

---

## Concept map

### Foundations & Random Walks

- [[Stochastic Process]]: continuous vs. discrete time/space
- [[Strong Stationarity]] vs [[Independent Increments]]
- [[Simple Random Walk]]: $S_n = S_0 + \sum_t {X_t}$
- [[Spatial Homogeneity]] and [[Time Homogeneity]]
- [[Gambler's Ruin]]: ruin probability $y_k$ and [[Absorbing State|absorbing states]].

### Discrete-Time Markov Chains (DTMC)

- [[Transition Matrix]]: $P$ and $n$-step transitions $P^n$
- [[Transition Graph]]: visualizing state movements
- [[Chapman-Kolmogorov Equation]]: $p_{ij} ^{(m+n)} = \sum p_{ik}^m p_{kj}^n$
- [[Stationary Distribution]]: solving $\pi P = \pi$
- [[Equilibrium Distribution]]: limit of $p^n$ as $n \to \infty$

### State Classification & Periodicity

- [[Irreducible Class]]: states that communicate with each other.
- [[Absorbing State]]: state $i$ where $p_{ii} = 1$
- [[Recurrent State]] vs [[Transient State]]: probability of revisiting $f_i$
- [[Period of States]]: greatest common divisor of possible return steps

### Continuous-Time & Jump Processes

- [[Poisson Process]]: rate $\lambda$, [[Independent Increments]], and $N(t) \sim \text{Poisson}(\lambda t)$
- [[Markov Jump Process]]: continuous-time homogeneous chains
- [[Kolmogorov Forward Equations]]: differential equations for $p_{ij}^\prime (t)$

### Time Series Analysis

- [[Moving Average Process]]: $MA(q)$ mean, variance, and autocorrelation
- [[Autoregressive Process]]: $AR(p)$ processes and stationarity
- [[ARMA Process]]: combined $ARMA(p,q)$ models
- [[Stochastic Processes/Time Series Analysis/Stationarity]]: requirements on roots of $(1-aL)$
- [[Invertibility]]: requirements on roots of the $MA$ characteristic equation.
- [[Prediction]]: computing $\hat{y}_{t+n} = E(y_{t+n} | F_t)$  

---

## Key dependency chains

```
Increments (Stationary/Independent) → Simple Random Walk → Gambler's Ruin Transition Matrix → Chapman-Kolmogorov → n-step Probabilities → Stationary Distributions State Classification (Communication/Closed) → Recurrence/Transience → Equilibrium Poisson Process → Markov Jump Process → Kolmogorov Forward Equations White Noise → AR/MA Processes → ARMA → Stationarity/Invertibility → Prediction
```
---
## Exam focus

### **High priority**: appeared in revision questions:

- **SRW Proofs:** Proving time or spatial homogeneity.
- **DTMC Calculations:** Finding $P^n$, $p^{(n)}$, and solving for stationary distributions $\pi$.
- **Classification:** Identifying irreducible classes, periods, and recurrence/transience.
- **Poisson Processes:** Calculating $P(N(t) > k)$ and using independent increments for conditional expectations.
- **Time Series Properties:** Checking invertibility/stationarity ranges for parameters and calculating the Autocorrelation Function (ACF).
- **ARMA Prediction:** Deriving expressions for $\hat{y}_{t+n}$.

### Common Question Types:

- "Prove that the process has independent increments."
- "Calculate the probability that the gambler will ruin if $S_0 = 1$."
- "Find the range of $a$ for which the ARMA process is stationary."
- "Write down the Kolmogorov forward equations for a Poisson process."

---

## Open questions

- _How does the transition from DTMC to CTMC change the way we calculate stationary distributions (generators vs. transition matrices)?_
- _What is the specific relationship between the roots of the characteristic equation and the visual behavior of an ARMA process?_