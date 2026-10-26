---
title: "Two-State Model"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 6 - Exposed To Risk and Two-State model"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, two-state-model, markov-model, mle]
---
## Definition
Rather than modelling the future lifetime $T$ directly, the **two-state model** tracks the state $Y$ occupied by an individual at time $t$: $Y=1$ ("alive") and $Y=2$ ("dead"), with a one-directional transition alive $\to$ dead. This is the simplest possible [[Stochastic Process|stochastic process]]: the process stays in state 1 until a single transition to the absorbing state 2, at which point it remains there forever. The **transition intensity** (force of mortality) $\mu_x$ is the key parameter governing this transition.

## Properties
### Assumption 1: Markov property
The probability of transitioning to another state at any age depends only on the current state and age, not on prior history — see [[Markov Property]]. E.g. past illness history does not directly affect the model (unless represented by an explicit extra state).

### Assumption 2: transition rate
As in [[Hazard Function|Chapter 1]], we assume $dt\,q_{x+t}\approx \mu_{x+t}\,dt$ for small $dt$, from which it follows (see [[Force of Mortality and Actuarial Notation]]) that
$$
{}_tp_x = \exp\left(-\int_0^t \mu_{x+s}\,ds\right), \qquad f_x(t) = {}_tp_x\,\mu_{x+t}
$$

### Assumption 3: constant rate within age
Assume $\mu_{x+t}\equiv\mu_x$ for $t\in[0,1)$: a time-homogeneous Markov process within each age band $[x,x+1)$. This is reasonable for human mortality, since (outside very early life) $\mu_x$ varies slowly with age.

### Maximum likelihood estimation of $\mu_x$
The data per individual $i$ is the total waiting time $v_i = b_i^*-a_i$ (see [[Exposed to Risk]]) and the death indicator $\delta_i$. Under constant $\mu_x$, the waiting time of a time-homogeneous process is exponentially distributed with rate $\mu_x$: pdf $\mu_x e^{-\mu_x v_i}$ and survival probability ${}_{v_i}p_x = e^{-\mu_x v_i}$.

For those who died ($\delta_i=1$), the contribution to the likelihood is $\mu_{x+a_i+v_i}\exp\left(-\int_0^{v_i}\mu_{x+a_i+t}\,dt\right)$; for those censored/surviving, it is $\exp\left(-\int_0^{v_i}\mu_{x+a_i+t}\,dt\right)$. Both cases combine as $\mu_{x+a_i+v_i}^{\delta_i}\exp\left(-\int_0^{v_i}\mu_{x+a_i+t}\,dt\right)$; since $\mu_{x+t}$ is constant for $0\leq t\leq1$, this simplifies to $\mu_x^{\delta_i}\exp(-\mu_x v_i)$. Multiplying over all individuals:
$$
L \propto \mu_x^{d_x}\exp(-\mu_x V), \qquad d_x=\sum_i \delta_i,\quad V=\sum_i v_i = E_x^C
$$
Maximising (standard exponential-family MLE):
$$
\hat\mu_x = \frac{d_x}{V} = \frac{d_x}{E_x^C}, \qquad \text{Var}(\hat\mu_x) = -\left[\frac{d^2\ln L}{d\mu^2}\right]^{-1}\bigg|_{\mu=\hat\mu} = \frac{\hat\mu^2}{d_x} = \frac{\hat\mu}{E_x^C}
$$

### Distributional facts used in the derivation
- $P(\delta_i=1) = {}_{b_i-a_i}q_{x+a_i}$, $P(\delta_i=0)=1-{}_{b_i-a_i}q_{x+a_i}$, so $\mathbb{E}[\delta_i] = {}_{b_i-a_i}q_{x+a_i}$.
- ${}_{b_i-a_i}q_{x+a_i} = \int_0^{b_i-a_i} {}_tp_{x+a_i}\,\mu_{x+a_i+t}\,dt$ (integrate the density of the time to death over the observed window).
- The pdf of $v_i$ is $\mu e^{-\mu t}$ for $v_i<(b_i-a_i)$ (death observed within the window) and a point mass $e^{-\mu(b_i-a_i)}$ at $v_i=b_i-a_i$ (censored at the window boundary).
- It can be shown that $\mathbb{E}[\delta_i-\mu v_i]=0$ and $\text{Var}(\delta_i-\mu v_i)=\mathbb{E}[\delta_i]$, obtained by differentiating $\int_0^{b_i-a_i}\mu e^{-\mu t}dt + e^{-\mu(b_i-a_i)}=1$ with respect to $\mu$.

### $\mathbb{E}[D]=\mu\,\mathbb{E}[V]$
Summing $\mathbb{E}[\delta_i-\mu v_i]=0$ over all $n$ individuals and writing $D=\sum_i\delta_i$ (total deaths), $V=\sum_i v_i$ (total waiting time $=E_x^C$):
$$
\mathbb{E}[D] = \mu\,\mathbb{E}[V]
$$
i.e. the expected number of deaths equals the transition rate times the expected total time exposed to risk — the population-level analogue of the exponential mean-waiting-time relation, and the identity underlying $\hat\mu_x = d_x/E_x^C$ being (asymptotically) unbiased for $\mu_x$.

### Generalisation: the multi-state model
The two-state (alive/dead) model is the simplest case of a **time-homogeneous Markov process on more than two states** (e.g. adding a "sick" state gives a sickness-death model) — see [[Multi-State Markov Model]] for the general Chapman-Kolmogorov/generator-matrix formulation, of which the single transition intensity $\mu_x$ here is a special case with generator matrix $\begin{pmatrix}-\mu_x & \mu_x\\ 0 & 0\end{pmatrix}$.

## See also
[[Exposed to Risk]], [[Force of Mortality and Actuarial Notation]], [[Poisson Model for Mortality]], [[Markov Property]], [[Multi-State Markov Model]]
