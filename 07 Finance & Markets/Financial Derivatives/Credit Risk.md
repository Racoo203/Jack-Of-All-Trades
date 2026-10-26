---
title: "Credit Risk"
domain: "Finance & Markets"
course: "Financial Derivatives"
unit: "Chapter 10 - Credit Risk"
level: MSc
status: drafted
confidence: 0
tags: [financial-derivatives, credit-risk, actuarial]
---
## Definition
A bond is **default-free** if all its cash flows will definitely be paid on time (sovereign bonds are usually treated this way); otherwise it carries **credit risk**. A **credit loss** occurs if a counterparty defaults on a contract that has positive value to the other side. Exposure varies by instrument: in a swap or forward, *both* long and short parties are exposed to credit risk as market conditions change; for options, only the option **holder** is exposed (the writer, having already been paid the premium and having no further claim on the holder, bears none).

## Properties
### Expected loss decomposition
$$
\text{Expected loss} = \text{Exposure} \times \text{Probability of default} \times \text{Loss Given Default (LGD)}.
$$
All three components are generally time-dependent. The **recovery rate** is $100\%-\text{LGD}$ — the fraction of exposure recovered from the defaulting counterparty's remaining assets.

### Credit events
There is no single universal definition of "default," but recognised triggering events include: rescheduling of a payment stream; cancellation or reduction of a payment; continued payment at a reduced amount; bankruptcy or insolvency proceedings; a credit-rating downgrade; failure to pay a coupon or principal (in full or part); a moratorium (contract validity disputed); and restructuring of payment terms.

### Three modelling approaches
1. **Structural models** — connect a firm's default explicitly to its balance-sheet structure (assets vs. liabilities); the canonical example is the [[Merton Model (Credit Risk)|Merton model]]. Gives an explicit economic link between default and the firm's condition and supports estimating default correlations across firms, but requires identifying the right model and estimating its parameters.
2. **Reduced-form models** — use statistical/empirical models fitted to rating-agency data (S&P, Fitch, Moody's), with default triggered when an *exogenous* hazard rate is realised, without modelling the firm's internal structure.
3. **Intensity-based models** — a continuous-time variant of reduced-form models, typically including jumps between discrete states (e.g. credit ratings) governed by transition intensities $\lambda$. See [[Reduced-Form Credit Risk Model]].

## See also
[[Merton Model (Credit Risk)]], [[Reduced-Form Credit Risk Model]], [[Hazard Function]], [[Black-Scholes formula]]
