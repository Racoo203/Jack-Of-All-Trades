---
title: "Censoring in Survival Analysis"
domain: Probability & Statistics
course: Survival Analysis
unit: "Chapter 3 - Curtate future lifetime, laws of mortality"
level: MSc
status: drafted
confidence: 0
tags: [survival-analysis, censoring]
---
## Definition
**Censoring** occurs when the event of interest either never happens, or happens after the end of a study, so the exact survival time is not observed for every subject. E.g. in a 3-year cancer study, participants still alive at the end are known only to have survived to $t=3$ years (their exact death time is unknown); a participant who drops out is known only to have survived to the time of dropout.

## Properties
### Types of censoring
- **Right censoring**: the event happens after the end of study, or the individual is lost to follow-up.
  - **Type I**: observation time is fixed, the number of censored individuals is random (e.g. a study with a fixed end date).
  - **Type II**: the number of events is fixed, observation time is random (e.g. a trial that stops once $r<n$ deaths have occurred).
  - **Non-informative censoring**: censoring reveals no information about the lifetime, i.e. the censoring mechanism is unrelated to the event of interest (e.g. leaving a study for reasons unrelated to disease severity).
- **Left censoring**: the individual's entry time (or exact starting condition) is unknown — e.g. a patient already has cancer metastasis at their first visit, but the actual onset time is unknown.
- **Interval censoring**: the event is known to lie within an interval but not at an exact time — e.g. a patient seen only at periodic visits, where the event is detected at one visit but occurred sometime since the last.

### Modelling left- and interval-censored data
The [[Kaplan-Meier estimate|Kaplan-Meier estimator]] and the [[Cox Proportional Hazards Model|Cox model]] do not directly accommodate left- or interval-censored observations (modifications exist, but are not covered here). A simpler alternative is to use a fully **[[Parametric Survival Models|parametric survival model]]**, where $S(t)$ (and hence $F(t)=1-S(t)$) has a known closed form: a left-censored observation at time $x$ contributes $F(x)$ to the likelihood, and an interval-censored observation $(x_1,x_2)$ contributes $F(x_2)-F(x_1)$ — see [[Likelihood Function for Censored Survival Data]] for the full combined likelihood across all four censoring types.

## See also
[[Likelihood Function for Censored Survival Data]], [[Kaplan-Meier estimate]], [[Exposed to Risk]], [[Parametric Survival Models]], [[Accelerated Failure Time Model]]
