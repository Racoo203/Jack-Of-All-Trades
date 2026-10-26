---
title: Markov Jump Process
domain: Stochastic Processes
course: Stochastic Processes
unit: Continuous-Time & Jump Processes
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A continuous-time [[Stochastic Process|stochastic process]] $\{X(t), t\geq 0\}$ defined on a discrete state space $S$ is a **continuous-time Markov chain** (also called a **Markov jump process**) if it satisfies the [[Markov Property|Markov property]] in continuous time:
$$
Pr(X(t+h)=j \mid X(t)=i, X(t_n)=i_n,\dots,X(t_0)=i_0) = Pr(X(t+h)=j\mid X(t)=i)
$$
for all $h\geq 0$, $0\leq t_0 < t_1 < \cdots < t_n < t$, and $i,j,i_0,\dots,i_n\in S$.

The chain is **time-homogeneous** if $Pr(X(t+h)=j\mid X(t)=i) = Pr(X(h)=j\mid X(0)=i) =: p_{ij}(h)$ for all $h,t\geq 0$, i.e. the transition probability depends only on the elapsed time $h$. For a homogeneous chain on $S=\{1,\dots,m\}$, the **transition matrix** $P(t)$ has entries $p_{ij}(t)$, and satisfies $p_{ij}(t)\geq 0$, $\sum_j p_{ij}(t)=1$ for all $t\geq 0$, and $P(0)=I$.

A time-homogeneous continuous-time Markov chain is fully specified by its initial distribution $p(0)$ and its **generator matrix** $Q$ of transition rates (see below), in the same way a discrete-time chain is specified by $p(0)$ and its [[Transition Matrix|transition matrix]] $P$.

## Properties
### Chapman-Kolmogorov Equations
For all $t,s\geq 0$,
$$
p_{ij}(t+s) = \sum_{k\in S} p_{ik}(t)\,p_{kj}(s), \qquad\text{i.e.}\qquad P(t+s)=P(t)P(s),
$$
the continuous-time analogue of the discrete [[Chapman-Kolmogorov Equation|Chapman-Kolmogorov equation]]. If the distribution of $X(t)$ is written $p(t)$, then $p(t) = p(0)\cdot P(t)$.

*Proof.* Using the law of total probability and the Markov property,
$$
p_{ij}(t+s) = Pr(X(t+s)=j\mid X(0)=i) = \sum_{k\in S} Pr(X(t+s)=j, X(t)=k\mid X(0)=i)
$$
$$
= \sum_{k\in S} Pr(X(t+s)=j\mid X(t)=k, X(0)=i)\, Pr(X(t)=k\mid X(0)=i) = \sum_{k\in S} Pr(X(t+s)=j\mid X(t)=k)\, Pr(X(t)=k\mid X(0)=i) = \sum_{k\in S} p_{ik}(t)\,p_{kj}(s). \quad\blacksquare
$$

### Generator Matrix
Under the assumptions that (i) $P(t)$ is continuous at $0$ (i.e. $p_{ij}(t)\to \mathbb 1\{j=i\}$ as $t\to 0$) and (ii) the entries $q_{ij} := p_{ij}'(0) = \lim_{t\to 0}\frac{p_{ij}(t)-p_{ij}(0)}{t}$ exist and are finite, we obtain, as $t\to 0$,
$$
p_{ii}(t) = 1+q_{ii}t+o(t), \qquad p_{ij}(t) = q_{ij}t + o(t)\ (j\neq i),
$$
or in matrix form $P(t) = I + Qt + o(t)$, where $Q=(q_{ij})$ is the generator matrix. Since $\sum_j p_{ij}(t)=1$ for every $t$,
$$
1 = 1+q_{ii}t+\sum_{j\neq i} q_{ij}t + o(t) \implies q_{ii} = -\sum_{j\neq i} q_{ij}.
$$
**Properties of $Q$:** rows sum to $0$ ($\sum_j q_{ij}=0$); $q_{ii}=-\sum_{j\neq i}q_{ij}$; $q_{ij}\geq 0$ for $j\neq i$ (off-diagonal transition rates); $q_{ii}\leq 0$.

Because $P'(0)=Q$, $Q$ plays the role for continuous-time chains that $P$ plays for discrete-time chains: it captures the *instantaneous rates of change* of the transition probabilities. The [[Kolmogorov Forward Equations|Kolmogorov forward equations]] $P'(t)=P(t)Q$ follow from the Chapman-Kolmogorov equations together with this local expansion (full derivation in that note).

### Holding Time
For state $i\in S$, the **holding time** is $T_i = \inf\{s\geq 0 : X(t+s)\neq i \mid X(t)=i\}$, the length of time the chain stays in $i$ before leaving.

**Lemma.** $T_i \sim \text{Exp}(-q_{ii})$, so $E(T_i) = -1/q_{ii}$. Since $-q_{ii}=\sum_{j\neq i}q_{ij}$ is the total rate of leaving $i$, a larger rate of leaving implies a shorter expected holding time.

*Proof.* Let $s_i(t) = Pr(T_i\geq t)$ (no move out of $i$ in $(0,t]$). For small $h>0$,
$$
s_i(t+h) = Pr(\text{no move in }(0,t])\cdot Pr(\text{no move in }(t,t+h]\mid X(t)=i) = s_i(t)\big(p_{ii}(h)+o(h)\big) = s_i(t)\big(1+q_{ii}h+o(h)\big).
$$
Subtracting $s_i(t)$, dividing by $h$ and letting $h\to 0$ gives $s_i'(t) = q_{ii}\,s_i(t)$, an ODE with solution $s_i(t) = Ae^{q_{ii}t}$; the initial condition $s_i(0)=1$ gives $A=1$, so $Pr(T_i\geq t) = e^{q_{ii}t}$, i.e. $T_i\sim\text{Exp}(-q_{ii})$. $\blacksquare$

### Lack-of-Memory Property
For $Y\sim\text{Exp}(\lambda)$, the survival function is $F(t) = Pr(Y>t) = e^{-\lambda t}$, so for any $h>0$,
$$
Pr(Y>t+h\mid Y>t) = \frac{Pr(Y>t+h)}{Pr(Y>t)} = \frac{e^{-\lambda(t+h)}}{e^{-\lambda t}} = e^{-\lambda h} = Pr(Y>h),
$$
i.e. $Y$ is memoryless. Since $T_i\sim\text{Exp}(-q_{ii})$, the holding time in state $i$ is memoryless: however long the chain has already spent in state $i$, the remaining time still follows $\text{Exp}(-q_{ii})$.

### Instantaneous Transition Probabilities Upon Leaving a State
When a chain leaves state $i$, the probability it jumps to a specific state $j\neq i$ (rather than any of the other reachable states) is proportional to the rate $q_{ij}$:
$$
Pr(\text{next state is } j \mid \text{leaving } i) = \frac{q_{ij}}{\sum_{k\neq i} q_{ik}} = \frac{q_{ij}}{-q_{ii}}.
$$
*Proof (for a specific target $j=D$ leaving $i=S$, generalizes directly).* Let $X_t$ denote the chain. Then
$$
P = \lim_{h\to 0} Pr(X_{t+h}=D \mid X_{t+h}\neq S, X_t=S) = \lim_{h\to 0} \frac{Pr(X_{t+h}=D, X_{t+h}\neq S, X_t=S)}{Pr(X_{t+h}\neq S, X_t=S)} = \lim_{h\to 0}\frac{Pr(X_{t+h}=D\mid X_t=S)}{Pr(X_{t+h}\neq S\mid X_t=S)}.
$$
Using $p_{SD}(h) = q_{SD}h+o(h)$, and writing the denominator as a sum of probabilities of landing in each state other than $S$ (say $S$ has other neighbours $H,T$ as well),
$$
P = \lim_{h\to 0}\frac{p_{SD}(h)}{p_{SD}(h)+p_{ST}(h)+p_{SH}(h)} = \lim_{h\to 0}\frac{q_{SD}h+o(h)}{q_{SD}h+q_{ST}h+q_{SH}h+o(h)} = \frac{q_{SD}}{q_{SD}+q_{ST}+q_{SH}}. \quad\blacksquare
$$
This gives a quick way to answer questions like "what is the probability a sick patient dies (rather than recovers) before leaving the sick state?" directly from the generator matrix's row, without solving any differential equations.

### Estimating the Transition Rates (Maximum Likelihood)
**Lemma.** Suppose that over $[0,T]$ the chain has visited state $i$ for $r$ times, with the $j$th visit lasting $T_{ij}$. Then the MLE of $q_{ii}$ is
$$
\hat q_{ii} = -\frac{r}{\sum_{j=1}^r T_{ij}} = -\frac{\text{total number of visits to } i}{\text{total time spent in } i}.
$$
*Proof.* Since $T_i\sim\text{Exp}(-q_{ii})$ with density $f(x)=-q_{ii}e^{q_{ii}x}$, and holding times are independent (Markov property), the likelihood of observing $T=(T_{i1},\dots,T_{ir})$ is $L(q_{ii};T) = \prod_j f(T_{ij})$, so the log-likelihood is
$$
\ell(q_{ii};T) = r\log(-q_{ii}) + q_{ii}\sum_{j=1}^r T_{ij}.
$$
Setting $\partial \ell/\partial q_{ii} = \frac{r}{q_{ii}} + \sum_j T_{ij} = 0$ gives $\hat q_{ii} = -r/\sum_j T_{ij}$. Since $\partial^2\ell/\partial q_{ii}^2 = -r/q_{ii}^2 < 0$ for any $q_{ii}$, this is indeed a maximum. $\blacksquare$

## Examples
### The Healthy-Sick-Dead (HSD) model
A person's health is modelled with states $\{H,S,D\}$ and generator matrix
$$
Q = \begin{pmatrix} -\rho-\mu & \rho & \mu \\ \sigma & -\sigma-\nu & \nu \\ 0 & 0 & 0 \end{pmatrix}.
$$
Row $D$ is all zero: $D$ is an [[Absorbing State|absorbing state]] — the transition *probability* from $D$ to $D$ is $1$, but the transition *rate* $q_{DD}$ is $0$ (a common point of confusion). The holding times are $T_H\sim\text{Exp}(\rho+\mu)$ and $T_S\sim\text{Exp}(\sigma+\nu)$, giving $E(T_H)=1/(\rho+\mu)$, $E(T_S)=1/(\sigma+\nu)$.

### Two-state weather chain (MLE application)
For states $R$ (Rainy) and $F$ (Fine) with $q_{RF}=\rho$, $q_{FR}=\phi$, since $q_{RR}=-\rho$, the MLE of $\rho$ is
$$
\hat\rho = \frac{\text{total number of visits to } R}{\text{total time spent in } R}.
$$

## See also
- [[Poisson Process]]
- [[Kolmogorov Forward Equations]]
- [[Markov Property]]
- [[Chapman-Kolmogorov Equation]]
- [[Transition Matrix]]
- [[Stationary Distribution]]
- [[Discrete-Time Markov Chain]]
- [[Absorbing State]]
- [[Exponential distribution]]
- [[Stochastic Process]]
