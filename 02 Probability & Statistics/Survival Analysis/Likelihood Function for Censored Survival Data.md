---
title: "Likelihood Function for Censored Survival Data"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 3 - Curtate future lifetime, laws of mortality"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, likelihood, mle, censoring]
---
## Definition
Let $T$ have pdf $f(t\mid\theta)$ for unknown parameter $\theta$. With $n$ i.i.d. samples $t_1,\dots,t_n$ and **no censoring**, the likelihood is
$$
L(\theta) = \prod_{i=1}^n f(t_i\mid\theta)
$$

With **[[Censoring in Survival Analysis|right censoring]]**, for each individual we observe either $T=t$ (event) or censoring $C=t$ (so we only know $T>t$). Let $\delta_i=1$ if individual $i$ experiences the event and $\delta_i=0$ if censored. An event contributes $f(t_i)$ to the likelihood; a censored observation contributes $S(t_i)=P(T>t_i)$. Combining:
$$
L = \prod_{i=1}^n f(t_i)^{\delta_i}S(t_i)^{1-\delta_i}
$$
Since $f(t)=h(t)S(t)$ (see [[Hazard Function]]), this can be rewritten as
$$
L = \prod_{i=1}^n [h(t_i)S(t_i)]^{\delta_i}S(t_i)^{1-\delta_i} = \prod_{i=1}^n h(t_i)^{\delta_i}S(t_i)
$$

## Properties
### Maximum likelihood estimation under right censoring
With $f,h,S$ depending on $\theta$, the log-likelihood is
$$
l(\theta) = \sum_{i=1}^n \left[\delta_i\ln h(t_i\mid\theta) + \ln S(t_i\mid\theta)\right]
$$
The MLE $\hat\theta$ solves the score equation $U(\theta)=dl(\theta)/d\theta = 0$, and
$$
\text{Var}(\hat\theta) = -\left[\frac{d^2 l(\theta)}{d\theta^2}\right]^{-1}\bigg|_{\theta=\hat\theta}
$$
(the standard maximum-likelihood machinery: score, observed information, asymptotic variance).

### Worked example: Exponential distribution under right censoring
With $f(t\mid\theta)=\theta e^{-\theta t}$, so $S(t\mid\theta)=e^{-\theta t}$ and $h(t\mid\theta)=\theta$:
$$
L(\theta) = \prod_{i=1}^n \theta^{\delta_i}\exp(-\theta t_i), \qquad l(\theta) = \sum_{i=1}^n(\delta_i\ln\theta - \theta t_i)
$$
Score: $\dfrac{dl(\theta)}{d\theta} = \dfrac{\sum_i \delta_i}{\theta} - \sum_i t_i$. Setting to zero:
$$
\hat\theta = \frac{\sum_{i=1}^n \delta_i}{\sum_{i=1}^n t_i}
$$
Second derivative: $\dfrac{d^2l(\theta)}{d\theta^2} = -\dfrac{\sum_i\delta_i}{\theta^2} < 0$ (confirms a maximum), giving
$$
\text{Var}(\hat\theta) = \frac{\sum_{i=1}^n \delta_i}{\left(\sum_{i=1}^n t_i\right)^2}
$$

### Uncensored MLE for comparison
Without censoring (all $\delta_i=1$), the same steps give $\hat\theta = n/\sum_i t_i$ and $\text{Var}(\hat\theta) = n/(\sum_i t_i)^2$ — the censored formula reduces to this when every observation is a completed event.

### Combined likelihood across all four censoring types
For a fully **[[Parametric Survival Models|parametric]]** model (needed since [[Kaplan-Meier estimate|Kaplan-Meier]] and the [[Cox Proportional Hazards Model|Cox model]] do not handle left/interval censoring), each observation contributes to the likelihood according to its censoring type:
$$
L = \prod_{\text{event}} f(t_i)\;\prod_{\text{right cens.}} S(t_i)\;\prod_{\text{left cens.}} F(t_i)\;\prod_{\text{interval cens.}} \big(F(t_i^{(2)})-F(t_i^{(1)})\big)
$$
equivalently, writing each factor as an integral of the density (with $F(t)=\int_0^t f(s)\,ds$ and $S(t)=\int_t^\infty f(s)\,ds$):
$$
L = \prod_{\text{event}} f(t_i)\;\prod_{\text{right cens.}}\int_{t_i}^{\infty} f(s)\,ds\;\prod_{\text{left cens.}}\int_0^{t_i} f(s)\,ds\;\prod_{\text{interval cens.}}\int_{t_i^{(1)}}^{t_i^{(2)}} f(s)\,ds
$$
This generalises the right-censoring-only likelihood above: setting the left- and interval-censored products to empty recovers $L=\prod f(t_i)^{\delta_i}S(t_i)^{1-\delta_i}$.

## See also
[[Censoring in Survival Analysis]], [[Parametric Survival Models]], [[Kaplan-Meier estimate]], [[Proportional Hazards Model]], [[Accelerated Failure Time Model]]
