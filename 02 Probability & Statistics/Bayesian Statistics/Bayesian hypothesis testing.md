---
title: "Bayesian hypothesis testing"
domain: "Probability & Statistics"
course: "Bayesian Statistics"
unit: "Chapter 5 - Bayesian Hypothesis Testing"
level: MSc
status: drafted
confidence: 0
tags: [bayesian-statistics, decision-theory]
---
## Definition
Testing $H_0:\theta\in\Theta_0$ vs $H_1:\theta\in\Theta_1$ is framed as a decision problem: $D=\{\text{accept }H_0,\text{reject }H_0\}$, identified with $\{1,0\}$. Using the asymmetric [[Loss function]]
$$
L(\theta,\delta) = \begin{cases} 0 & \theta\in\Theta_0,\ \delta=1\ (\text{correct accept})\\ a_0 & \theta\in\Theta_0,\ \delta=0\ (\text{erroneous reject})\\ 0 & \theta\notin\Theta_0,\ \delta=0\ (\text{correct reject})\\ a_1 & \theta\notin\Theta_0,\ \delta=1\ (\text{erroneous accept})\end{cases}
$$

## Properties
### Bayes decision rule (Proposition 5.1)
The [[Bayes estimate|Bayes rule]] associated with prior $\pi$ under this loss is
$$
\delta^\pi(x) = \begin{cases}1 & P^\pi(\theta\in\Theta_0|x) > \dfrac{a_1}{a_1+a_0}\\ 0 & \text{otherwise}\end{cases}
$$
**Proof.** The posterior expected loss is $\rho(\pi,\delta|x) = a_0 P^\pi(\theta\in\Theta_0|x)\mathbb 1_{\delta=0} + a_1 P^\pi(\theta\notin\Theta_0|x)\mathbb 1_{\delta=1}$, minimized by the stated rule. In the symmetric case $a_0=a_1$, this reduces to "accept $H_0$ iff $P^\pi(\theta\in\Theta_0|x) > 1/2$." The larger $a_0/a_1$ (the more costly a false rejection), the smaller the posterior probability of $\Theta_0$ needed to accept it.

### Worked derivation: Normal one-sided test
For $x\sim N(\theta,\sigma^2)$ ($\sigma^2$ known) and prior $\theta\sim N(\mu,\tau^2)$, the posterior is $N(\mu(x), w^2)$ with $\mu(x)=\frac{\sigma^2\mu+\tau^2 x}{\sigma^2+\tau^2}$, $w^2=\frac{\sigma^2\tau^2}{\sigma^2+\tau^2}$ (see [[Posterior distribution]]). Testing $H_0:\theta<0$:
$$
P^\pi(\theta<0|x) = \Phi\left(\frac{-\mu(x)}{w}\right)
$$
Letting $z_{a_0,a_1}$ be the $a_1/(a_0+a_1)$ quantile, $H_0$ is accepted iff $-\mu(x) > z_{a_0,a_1}w$, i.e.
$$
x < -\frac{\sigma^2}{\tau^2}\mu - \left(1+\frac{\sigma^2}{\tau^2}\right)wz_{a_0,a_1}
$$
As $\tau^2\to\infty$ (non-informative prior) with $\mu=0,\sigma^2=1$, this becomes "accept $H_0$ if $x<-z_{a_0,a_1}$." The classical test at level $\alpha$ accepts $H_0$ if $x<-z_\alpha$, which matches the Bayesian rule when $a_0/a_1 = 1/\alpha - 1$ — e.g. $a_0/a_1=19$ for $\alpha=0.05$. The heavy asymmetry required to reproduce a classical test reflects the "special", privileged status the null hypothesis is given in the classical approach.

### Prior mass on a point null
If $\Theta_0=\{\theta_0\}$ is a single point, the posterior probability of $H_0$ is zero unless the prior places positive mass (an atom) at $\theta_0$ — a purely continuous prior cannot support testing a point null in this framework (see [[Bayes factor]] for the atom-prior construction used instead).

## See also
[[Bayes factor]], [[Loss function]], [[Bayes estimate]], [[Classical Hypothesis Testing]]
