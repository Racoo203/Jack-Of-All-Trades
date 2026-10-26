---
title: "Multi-State Markov Model"
domain: Probability & Statistics
course: Survival Analysis
unit: "PGT Lectures"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, multi-state-model, markov-model, pgt-extension]
---
## Definition
The [[Two-State Model|two-state (alive/dead) model]] generalises to a **multi-state time-homogeneous Markov process** on states $S=\{0,1,\dots\}$ — e.g. a sickness-death model with states Healthy (0), Sick (1), Dead (2). Time-homogeneity means the transition probability $p_{ij}(t) = P(X_t=j\mid X_0=i)$ depends only on the elapsed time $t$, not on the starting time. As with a [[Discrete-Time Markov Chain|discrete-time chain]], these obey the **Chapman-Kolmogorov equations**:
$$
p_{ij}(t+s) = \sum_{k\in S} p_{ik}(s)p_{kj}(t), \qquad P(s+t) = P(s)P(t) \text{ (matrix form)}
$$

**Transition intensities** $\mu^{ij}$ are defined via, for small $dt$,
$$
p_{ij}(dt) \approx \begin{cases} dt\,\mu^{ij} & i\neq j \\ 1+dt\,\mu^{ii} & i=j \end{cases}
$$
Since $\sum_{j\in S} p_{ij}(t)=1$, this forces $\mu^{ii} = -\sum_{j\neq i}\mu^{ij}$. The matrix $\{\mu^{ij}\}$ is the **generator matrix**. For the sickness-death model with intensities $\mu^{01}_x,\mu^{02}_x,\mu^{10}_x,\mu^{12}_x$ (all constant in $t\in[0,1)$, i.e. $\mu^{ij}_{x+t}\equiv\mu^{ij}_x$), the generator matrix is
$$
\begin{pmatrix} -\mu^{01}_x-\mu^{02}_x & \mu^{01}_x & \mu^{02}_x \\ \mu^{10}_x & -\mu^{10}_x-\mu^{12}_x & \mu^{12}_x \\ 0 & 0 & 0 \end{pmatrix}
$$

## Properties
### Kolmogorov forward equations
From the Chapman-Kolmogorov equations, for small $h$: $p_{ij}(t+h) = \sum_k p_{ik}(t)p_{kj}(h) \approx p_{ij}(t) + h\sum_k p_{ik}(t)\mu^{kj}$. Rearranging and taking $h\to0$:
$$
\frac{d}{dt}p_{ij}(t) = \sum_{k\in S} p_{ik}(t)\mu^{kj} \qquad \text{for all } i,j
$$
matching the [[Kolmogorov Forward Equations]] already seen for the [[Poisson Process]]. For the two-state alive/dead (AD) model this reduces to $\frac{d}{dt}p_{AA}(t)=-\mu_x p_{AA}(t)$, $\frac{d}{dt}p_{AD}(t)=\mu_x p_{AD}(t)$. Solving the first via the integrating factor $e^{\mu_x t}$: multiplying through, $e^{\mu_x t}\frac{d}{dt}p_{AA}(t)+e^{\mu_x t}\mu_x p_{AA}(t)=0 \implies \frac{d}{dt}(p_{AA}(t)e^{\mu_x t})=0$; integrating gives $p_{AA}(t)=Ce^{-\mu_x t}$ — recovering ${}_tp_x=\exp(-\mu_x t)$ from [[Two-State Model]] as the special case with two states.

### Waiting time and jump distribution
The waiting time in state $i$ before the next transition is exponentially distributed with parameter $\lambda_i=\sum_{j\neq i}\mu^{ij}$ (the total rate of leaving state $i$): $P(T_0>t\mid X_0=i)=e^{-\lambda_i t}$. The joint distribution of the elapsed time and the state jumped to is
$$
P(X_t=j\mid X_s=i,\, 0\leq s\leq t) = \mu^{ij}e^{-\lambda_i t} = \mu^{ij}\times {}_tp_i^{ii}
$$

### Likelihood construction
Partition each observed life's history into intervals, each ending in a transition or censorship. Each interval contributes the product of a survival-type factor (time spent in the current state without transitioning) and, if the interval ends in a transition, the relevant intensity. E.g. for a life observed: State 0 at $t=0$ → State 1 at $t=0.1$ → State 0 at $t=0.5$ → State 1 at $t=0.8$ → still State 1 at $t=1$, the four intervals contribute ${}_{0.1}p^{00}_x\mu^{01}_x$, ${}_{0.4}p^{11}_{x+0.1}\mu^{10}_x$, ${}_{0.3}p^{00}_{x+0.5}\mu^{01}_x$, ${}_{0.2}p^{11}_{x+0.8}$ respectively, using ${}_sp^{00}_{x+t}=e^{-s(\mu^{01}_x+\mu^{02}_x)}$ and ${}_sp^{11}_{x+t}=e^{-s(\mu^{10}_x+\mu^{12}_x)}$ for $s+t\leq1$. Multiplying out, the full contribution collapses to $e^{-0.4(\mu^{01}_x+\mu^{02}_x)}e^{-0.6(\mu^{10}_x+\mu^{12}_x)}(\mu^{01}_x)^2\mu^{10}_x$: the life spent $0.4$ years in State 0, $0.6$ years in State 1, made 2 transitions $0\to1$ and 1 transition $1\to0$.

**General result.** Let $t_j^{(k)}$ be the total time the $j$th life spent in state $k$ between ages $x$ and $x+1$ (waiting time in state $k$), and $d_j^{ik}$ the number of direct $i\to k$ transitions for that life. For the sickness-death model, life $j$ contributes
$$
e^{-t_j^{(0)}(\mu^{01}_x+\mu^{02}_x)}\,e^{-t_j^{(1)}(\mu^{10}_x+\mu^{12}_x)}\,(\mu^{01}_x)^{d_j^{01}}(\mu^{02}_x)^{d_j^{02}}(\mu^{10}_x)^{d_j^{10}}(\mu^{12}_x)^{d_j^{12}}
$$

### Maximum likelihood estimation
For $n$ lives, let $T^{(i)}=\sum_j t_j^{(i)}$ (total waiting time in state $i$) and $D^{ik}=\sum_j d_j^{ik}$ (total $i\to k$ transitions). The full likelihood simplifies to
$$
L = e^{-T^{(0)}(\mu^{01}_x+\mu^{02}_x)}e^{-T^{(1)}(\mu^{10}_x+\mu^{12}_x)}(\mu^{01}_x)^{D^{01}}(\mu^{02}_x)^{D^{02}}(\mu^{10}_x)^{D^{10}}(\mu^{12}_x)^{D^{12}}
$$
Log-likelihood: $l=-T^{(0)}(\mu^{01}_x+\mu^{02}_x)-T^{(1)}(\mu^{10}_x+\mu^{12}_x)+D^{01}\ln\mu^{01}_x+D^{02}\ln\mu^{02}_x+D^{10}\ln\mu^{10}_x+D^{12}\ln\mu^{12}_x$. Differentiating with respect to each $\mu^{ik}_x$ and setting to zero (e.g. $\partial l/\partial\mu^{01}_x = -T^{(0)}+D^{01}/\mu^{01}_x=0$) gives, for every $(i,k)$ pair:
$$
\hat\mu^{ik}_x = \frac{D^{ik}}{T^{(i)}}
$$
generalising $\hat\mu_x=d_x/E_x^C$ from the [[Two-State Model]]. The second derivatives $\partial^2l/\partial(\mu^{ik}_x)^2 = -D^{ik}/(\mu^{ik}_x)^2$ are all cross-independent (all cross-partials are zero), so the MLEs of different intensities are asymptotically independent, with
$$
\text{Var}(\hat\mu^{ik}_x) \approx \frac{(\hat\mu^{ik}_x)^2}{D^{ik}}
$$

## Examples
Three lives observed between ages $x$ and $x+1$: Life 1 in State 0 throughout ($t^{(0)}_1=1$); Life 2: State 1 → State 0 at $t=0.3$ → State 1 at $t=0.5$ → State 2 at $t=0.8$ ($t^{(0)}_2=0.2$, $t^{(1)}_2=0.6$, one $1\to0$, one $0\to1$, one $1\to2$); Life 3: State 0 → State 1 at $t=0.4$ → State 0 at $t=0.6$ → State 1 at $t=0.9$, still State 1 at $t=1$ ($t^{(0)}_3=0.7$, $t^{(1)}_3=0.3$, two $0\to1$, one $1\to0$). Totals: $T^{(0)}=1.9$, $T^{(1)}=0.9$, $D^{01}=3$, $D^{02}=0$, $D^{10}=2$, $D^{12}=1$. Estimates: $\hat\mu^{01}_x=3/1.9$, $\hat\mu^{02}_x=0$, $\hat\mu^{10}_x=2/0.9$, $\hat\mu^{12}_x=1/0.9$; ${}_1p^{00}_x=\exp(-(\hat\mu^{01}_x+\hat\mu^{02}_x)) = e^{-3/1.9}$; $\text{Var}(\hat\mu^{01}_x)=(\hat\mu^{01}_x)^2/D^{01}=3/1.9^2$, and a Wald-type CI follows as $\hat\mu^{01}_x \pm 1.96\sqrt{\text{Var}(\hat\mu^{01}_x)}$.

## See also
[[Two-State Model]], [[Exposed to Risk]], [[Chapman-Kolmogorov Equation]], [[Kolmogorov Forward Equations]], [[Wald Test]]
