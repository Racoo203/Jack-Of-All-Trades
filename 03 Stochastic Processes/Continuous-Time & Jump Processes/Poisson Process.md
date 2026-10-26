---
title: Poisson Process
domain: Stochastic Processes
course: Stochastic Processes
unit: Continuous-Time & Jump Processes
level: MSc
status: seeding
confidence: 0
tags: [seeding]
---
## Definition
A Poisson process is a [[Counting Process|counting process]] $\{N(t), t\geq 0\}$ counting the occurrences of some event over time, and it is the special case of a [[Renewal process|renewal process]] whose i.i.d. inter-event times are exponentially distributed. Two equivalent definitions are used.

**Definition 1 (infinitesimal / rate definition).** Let $\mathcal F = \{\mathcal F_t\}_{t\geq 0}$ be a [[Filtration|filtration]] associated with $\{N(t)\}$. A Poisson process with rate (intensity) $\lambda$ is a continuous-time, integer-valued process such that $N(0)=0$ and, for $h>0$,
$$
\begin{aligned}
Pr(N(t+h)-N(t)=1 \mid \mathcal F_t) &= \lambda h + o(h), \\
Pr(N(t+h)-N(t)=0 \mid \mathcal F_t) &= 1-\lambda h + o(h), \\
Pr(N(t+h)-N(t)>1 \mid \mathcal F_t) &= o(h).
\end{aligned}
$$
The distribution of the increment $N(t+h)-N(t)$ depends only on $\lambda$ and $h$, i.e. it is independent of $\mathcal F_t$ and $t$: the process has stationary increments.

**Definition 2 (distributional definition).** $\{N(t), t \geq 0\}$ is a Poisson process with intensity $\lambda$ if
1. $N(0)=0$ with probability 1;
2. $N(t)$ has independent increments: for any $k$ and $0\leq t_1 < \cdots < t_k$, the random variables $N(t_1), N(t_2)-N(t_1), \dots, N(t_k)-N(t_{k-1})$ are mutually independent;
3. $N(t)$ has stationary increments: $N(t)-N(s) \sim \text{Pois}(\lambda(t-s))$ for $s<t$.

**Equivalence.** When the filtration $\mathcal F$ in Definition 1 is the *natural* filtration of $\{N(t)\}$, the two definitions are equivalent. Sketch: (I $\Rightarrow$ II) $N(t+h)-N(t)$ is independent of $\mathcal F_t$ by Definition 1, hence independent of every event of the form $\{N(t)-N(t_k)=a_k,\dots,N(t_1)=a_0\}$ that generates $\mathcal F_t$; repeating this for all $t$ gives independence of all increments. (II $\Rightarrow$ I) conversely, independence of increments under Definition 2 shows $N(t+h)-N(t)$ is independent of $\mathcal F_t$, and stationarity of Definition 2(3) gives $Pr(N(t+h)-N(t)=0\mid \mathcal F_t) = e^{-\lambda h} = 1-\lambda h + o(h)$, and similarly for the other two conditions.

## Properties
### Generator matrix (as a Markov jump process)
The Poisson process is a time-homogeneous [[Markov Jump Process|Markov jump process]] on $S=\{0,1,2,\dots\}$ with transition rates
$$
q_{ij} = \begin{cases} -\lambda, & j=i, \\ \lambda, & j = i+1, \\ 0, & \text{otherwise.} \end{cases}
$$
To see this, note $p_{ij}(h) = Pr(N(t+h)=j \mid N(t)=i) = Pr(N(t+h)-N(t) = j-i) = \dfrac{(\lambda h)^{j-i}}{(j-i)!}e^{-\lambda h}$ for $j\geq i$ (and $0$ for $j<i$). Taking $\lim_{h\to 0}\frac{p_{ij}(h)-p_{ij}(0)}{h}$ gives $q_{ii}=-\lambda$ (since $p_{ii}(h) = e^{-\lambda h} = 1-\lambda h + o(h)$), $q_{i,i+1}=\lambda$ (since $p_{i,i+1}(h) = \lambda h e^{-\lambda h} = \lambda h(1+o(1))$), and $q_{ij}=0$ for $j>i+1$ (since $p_{ij}(h)=o(h)$ there). So $Q$ has $-\lambda$ on the diagonal, $\lambda$ on the superdiagonal, and $0$ elsewhere.

### Kolmogorov forward equations for the Poisson process
Specializing the general [[Kolmogorov Forward Equations|Kolmogorov forward equations]] $p_{ij}'(t) = \sum_{k} p_{ik}(t) q_{kj}$ to the generator matrix above gives
$$
p_{i0}'(t) = -\lambda p_{i0}(t), \qquad p_{ij}'(t) = \lambda p_{i(j-1)}(t) - \lambda p_{ij}(t), \quad j\geq 1.
$$
Writing $p_k(h) := Pr(N(h)=k)$, these become $p_0'(h) = -\lambda p_0(h)$ and $p_k'(h) = -\lambda p_k(h) + \lambda p_{k-1}(h)$ for $k\geq 1$, with initial condition $p_0(0)=1$, $p_k(0)=0$ for $k>0$. Solving by induction on $k$ shows $N(h) \sim \text{Pois}(\lambda h)$, i.e.
$$
p_k(h) = \frac{e^{-\lambda h}(\lambda h)^k}{k!}, \qquad k=0,1,2,\dots
$$
*Base case $k=0$:* $p_0'(h)/p_0(h) = -\lambda \Rightarrow p_0(h) = Ae^{-\lambda h}$; the initial condition gives $A=1$, so $p_0(h)=e^{-\lambda h}$.

*Base case $k=1$:* substituting $p_0(h)=e^{-\lambda h}$ into $p_1'(h) + \lambda p_1(h) = \lambda e^{-\lambda h}$ and multiplying by the integrating factor $e^{\lambda h}$ gives $\frac{d}{dh}\left(e^{\lambda h}p_1(h)\right) = \lambda$, so $e^{\lambda h}p_1(h) = \lambda h + c$; the initial condition $p_1(0)=0$ gives $c=0$, so $p_1(h) = \lambda h\, e^{-\lambda h}$.

*Inductive step:* assuming $p_n(h) = \dfrac{e^{-\lambda h}(\lambda h)^n}{n!}$, substituting into $p_{n+1}'(h) + \lambda p_{n+1}(h) = \dfrac{\lambda e^{-\lambda h}(\lambda h)^n}{n!}$ and again using the integrating factor $e^{\lambda h}$ gives $\frac{d}{dh}\left(e^{\lambda h}p_{n+1}(h)\right) = \dfrac{\lambda (\lambda h)^n}{n!}$, hence $e^{\lambda h}p_{n+1}(h) = \dfrac{(\lambda h)^{n+1}}{(n+1)!} + c$; the initial condition $p_{n+1}(0)=0$ gives $c=0$, so $p_{n+1}(h) = \dfrac{(\lambda h)^{n+1}e^{-\lambda h}}{(n+1)!}$, completing the induction.

(An alternative "second proof" derives the same result as a limit of $\text{Bin}(k, \lambda h + o(h))$ via the Poisson limit theorem, by splitting $N(t)=\sum_{i=1}^{k} \xi_i$ over $k=t/h$ small subintervals and showing the contribution of subintervals with more than one event vanishes.)

### No stationary distribution exists
Although a [[Stationary Distribution|stationary distribution]] for a continuous-time Markov chain is characterized by $\pi Q = 0$, applying this to the Poisson process's generator matrix gives $-\lambda \pi_0 = 0$ and $\lambda \pi_{k-1} - \lambda \pi_k = 0$ for $k\geq 1$, forcing $\pi_k = 0$ for all $k$. Since $\sum_k \pi_k = 0 \neq 1$, no stationary distribution exists — consistent with the process being a pure-birth chain that drifts to $+\infty$ and never settles into an equilibrium.

### Markov property
For $0\leq t_1 < \cdots < t_n < t_{n+1}$, independence of increments gives
$$
Pr(N(t_{n+1})=i_{n+1} \mid N(t_n)=i_n,\dots,N(t_1)=i_1) = Pr(N(t_{n+1})-N(t_n) = i_{n+1}-i_n) = Pr(N(t_{n+1})=i_{n+1}\mid N(t_n)=i_n),
$$
so the Poisson process satisfies the [[Markov Property|Markov property]] and is indeed a Markov jump process.

### Arrival and inter-arrival times
Let $T_1$ be the time to the first event, and $T_i$ ($i\geq 2$) the inter-arrival time between the $(i-1)$th and $i$th events. Let $S_r = T_1+\cdots+T_r$ be the time of the $r$th event.
- $T_1 \sim \text{Exp}(\lambda)$: since $Pr(T_1>t) = Pr(N(t)=0) = e^{-\lambda t}$, we get $F_{T_1}(t) = 1-e^{-\lambda t}$.
- $T_1, T_2, T_3, \dots$ are i.i.d. $\text{Exp}(\lambda)$. Sketch of the proof that $T_2 \sim \text{Exp}(\lambda)$ and $T_2 \perp T_1$: by the law of total probability, conditioning on $T_1=s$ (which is $\mathcal F_s$-measurable) and using independence of $N(s+t)-N(s)$ from $\mathcal F_s$,
$$
Pr(T_2>t, T_1>u) = \int_u^\infty Pr(N(s+t)-N(s)=0)\,\lambda e^{-\lambda s}\,ds = \int_u^\infty e^{-\lambda t}\lambda e^{-\lambda s}\,ds = e^{-\lambda t}Pr(T_1>u),
$$
which (setting $u=0$) shows $T_2\sim\text{Exp}(\lambda)$ and then shows $T_2 \perp T_1$; repeating for $(T_2,T_3), (T_3,T_4),\dots$ gives the full i.i.d. claim.
- $S_r \sim \Gamma(r,\lambda)$ (Gamma distribution, sum of $r$ i.i.d. $\text{Exp}(\lambda)$).
- The time from an arbitrary time point $t$ to the next event is also $\text{Exp}(\lambda)$ (a consequence of the memoryless property of the exponential inter-arrival times).

### Superposition and thinning
- **Superposition.** If $\{N_1(t)\}$ and $\{N_2(t)\}$ are independent Poisson processes with rates $\lambda_1,\lambda_2$, then $N(t)=N_1(t)+N_2(t)$ is a Poisson process with rate $\lambda_1+\lambda_2$.
- **Thinning.** If each event of a rate-$\lambda$ Poisson process $\{N(t)\}$ is independently kept with probability $p$ (deleted with probability $1-p$), the process $\{M(t)\}$ of kept events is a Poisson process with rate $p\lambda$.

## Examples
**Expected time to start of service.** Customers arrive at a processing station as a Poisson process with rate $\lambda=6$ (one every 10 minutes); service starts once the 3rd customer arrives. The expected waiting time until service starts is $E(T_1+T_2+T_3) = 3/\lambda = 0.5$ hours. The probability no service occurs within the first hour is
$$
Pr(N(1)<3) = e^{-\lambda}\left(1+\lambda+\frac{\lambda^2}{2}\right) = e^{-6}\left(1+6+18\right) = 25e^{-6} \approx 0.062.
$$

**Thinning applied.** $N(t)$ = number of fridge failures up to day $t$, $N(t)\sim$ Poisson process, rate $\lambda$; each failed fridge is thrown away (independently) with probability $p$, otherwise a service call is made. Then the number of service calls $M(t)$ is a thinned Poisson process with rate $\lambda(1-p)$, and the number of fridges thrown away $L(t)$ is a thinned Poisson process with rate $\lambda p$. So $M(3)\sim\text{Pois}(3\lambda(1-p))$, and by independence of increments $E(L(2)-L(1)\mid L(3)-L(2)=0) = E(L(2)-L(1)) = \lambda p$.

## See also
- [[Renewal process]]
- [[Counting Process]]
- [[Markov Jump Process]]
- [[Kolmogorov Forward Equations]]
- [[Markov Property]]
- [[Stationary Distribution]]
- [[Filtration]]
- [[Exponential distribution]]
- [[Gamma distribution]]
- [[Binomial distribution]]
- [[Stochastic Process]]
