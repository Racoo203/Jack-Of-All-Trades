---
title: "Gaussian Copula"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 10 - Copulas & Measures of Association"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, copulas, gaussian-copula, implicit-copula]
---
## Definition
An **implicit copula** has no simple closed-form expression; it is implied by a well-known multivariate distribution rather than written down directly (as opposed to [[Archimedean Copula|explicit/Archimedean copulas]]). The **Gaussian copula** is the implicit copula of the bivariate normal distribution: let $\Phi_2(x,y)$ be the joint cdf of the standard bivariate normal with correlation $\alpha$, and $\Phi$ the standard univariate normal cdf. Then
$$
C_\alpha(u,v) = \Phi_2\left(\Phi^{-1}(u),\Phi^{-1}(v)\right)
$$
with copula density
$$
c_\alpha(u,v) = \frac{1}{\sqrt{1-\alpha^2}}\exp\left\{-\frac{\alpha^2\Phi^{-1}(u)^2 - 2\alpha\Phi^{-1}(u)\Phi^{-1}(v) + \alpha^2\Phi^{-1}(v)^2}{2(1-\alpha^2)}\right\}
$$
The family $\{C_\alpha, \alpha\in[-1,1]\}$ is parametrised by the correlation $\alpha$; $\alpha=0$ recovers the [[Copula|independence copula]] $\Pi(u,v)=uv$.

## Properties
### Application: joint tail probabilities
For $X,Y \sim N(0,1)$ jointly modelled with a copula $C(u,v;\theta)$, a probability such as $P(X<-1,Y>1)$ can be computed as $C(F_X(-1), 1-F_Y(1);\theta) = C(\Phi(-1), 1-\Phi(1);\theta)$, substituting the marginal normal cdf values.

## See also
[[Copula]], [[Archimedean Copula]], [[Measures of Association]], [[Normal distribution]]
