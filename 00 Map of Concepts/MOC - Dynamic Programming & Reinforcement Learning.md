---
subject: Dynamic Programming & Reinforcement Learning
type: MOC
exam_date: 2026-06-01
status: drafted
confidence: 0
tags:
  - moc
  - exam
  - dp-and-rl
domain: Dynamic Programming & Reinforcement Learning
---
## Concept narrative

This domain is Essex's **MA338: Dynamic Programming and Reinforcement Learning** (Dr Felipe Maldonado), built directly on Sutton & Barto, *Reinforcement Learning: An Introduction* (2nd ed., 2018), plus a set of PGT-only "Special Topics" lectures. The module has two parts.

**Part I — Tabular Methods** treats problems small enough that value functions fit in a table. It opens with [[Multi-armed bandits]] as the single-state special case of the [[Exploration vs Exploitation]] problem, then generalises to the full sequential-decision setting via the [[Markov Decision Process]] (MDP): states, actions, rewards, and the [[Bellman equation]] that every value function must satisfy. Three families of tabular algorithm solve MDPs, distinguished by how much of the environment they need and how they update estimates: [[Dynamic programming]] (needs the full model, bootstraps), [[Monte Carlo Learning]] (needs no model, waits for the full episode, does not bootstrap), and [[Temporal-Difference Learning]] (needs no model, bootstraps after a single step — the synthesis of the other two, via SARSA and Q-learning). n-step methods and eligibility traces (SARSA(λ)) unify TD(0) and MC as the two ends of a spectrum. Planning methods (Monte Carlo Tree Search) sit alongside these as "indirect" RL: learn a model, then plan with it.

**Part II — Approximate Methods** drops the assumption that state/action spaces are small. Value functions become parametric — [[Linear MDPs & Linear Functional Approximation|linear]] or [[Nonlinear Functional Approximation|nonlinear]] (neural-network) approximators trained by stochastic gradient descent — which buys generalisation to unseen states at the cost of the tabular convergence guarantees. This is where the **Deadly Triad** (bootstrapping + function approximation + off-policy learning) becomes a real danger, and where [[Deep Reinforcement Learning]] (DQN and its variants) lives, engineered specifically to survive that triad via experience replay and target networks. The module then pivots from value-based to policy-based control via the [[Policy Gradient Theorem]], covering REINFORCE, baselines, and actor–critic methods, which scale naturally to continuous action spaces.

The **PGT Special Topics** lectures add four threads that don't fit the Part I/II split cleanly: reward shaping and policy invariance (Ng, Harada & Russell 1999), eligibility traces / TD(λ) as the backward-view counterpart of n-step methods, and a session on the DeepSeek-R1 paper as a case study of RL applied to LLM reasoning.

Beyond the taught syllabus, this domain folder also holds a broader personal reference layer of RL theory that MA338 itself does not cover but that is standard in the wider literature and directly useful for Raúl's own quant-research interests (RL in finance, PAC-MDP theory): regret and sample-complexity analysis for bandits and MDPs (UCB, Thompson sampling, [[Regret Analysis]]), theoretical tabular-exploration algorithms ([[Algorithms/R-MAX|R-MAX]], [[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]], [[Algorithms/MoRmax|MoRmax]], [[Algorithms/Upper-Confidence Fixed-Horizon (UCFH)|UCFH]], [[Algorithms/Upper Bounding the Expected Next State Value (UBEV)|UBEV]]), function-approximation-with-guarantees algorithms ([[Algorithms/Least-Squares Value Iteration (LSVI)|LSVI]], [[Algorithms/MatrixRL|MatrixRL]]), entropy-regularised control ([[Algorithms/G-learning|G-learning]], [[Algorithms/Soft-Q-learning|Soft Q-learning]]), continuous-control policy-gradient algorithms ([[Algorithms/DDPG|DDPG]], [[Algorithms/Proximal Policy Optimization|PPO]], [[Algorithms/Trust Region Policy Optimization|TRPO]]), classical optimal control ([[Linear-quadratic regulator (LQR)|LQR]], [[Hamilton-Jacobi-Bellman equation|HJB]], [[Multi-agent LQ]]), [[Inverse Reinforcement Learning]], and RL-for-portfolio-management building blocks ([[Ensemble of Identical Independent Evaluators (EIIE)]], [[Differential Sharpe ratio]]) that connect straight to the `investment-automation` project. These are flagged in the concept map below and are **not** MA338-assessed content — they are canonical literature results, drafted from general knowledge rather than grounded in the course slides.

## Concept map

### Foundations (Lecture 1)
- [[Agent-environment Interface]] — the At/Ot/Rt loop; supervised vs unsupervised vs reinforcement learning
- [[Exploration vs Exploitation]] — the central dilemma of RL
- [[Reward function]], [[Discount factor]]
- [[Value-based]] vs [[Policy-based]] methods; [[Model-free & Model-based]]
- [[On-policy & Off-policy]]
- [[Stationary & Non-stationary Environments]], [[Stationary & Non-stationary Policies]]
- [[Deterministic & Stochastic policies]]
- [[Infinite & Finite Time Horizon]]
- [[Simulator]]
- [[Performance Evaluation]]

### Unit 2 — Multi-armed Bandits (Lecture 1)
- [[Multi-armed bandits]] — single-state RL; action-value estimation
- [[Epsilon-greedy exploration]], [[UCB exploration]], [[Boltzmann exploration]], [[Thompson sampling]]
- [[Asymptotic Convergence]], [[Rate of Convergence]] of incremental estimators
- [[Regret Analysis]], [[Sample Complexity]], [[Sample Complexity of Exploration]], [[Mean-square Sample Complexity]] *(theory layer, not MA338-assessed)*

### Unit 3 — Finite Markov Decision Processes (Lecture 2)
- [[Markov Decision Process]] — states, actions, transition kernel p(s',r|s,a)
- [[State value function]] vπ, [[Action value function]] qπ
- [[Bellman equation]] — recursive consistency of vπ, qπ
- Bellman *optimality* equations for v*, q* (covered inside [[Bellman equation]])

### Unit 4 — Dynamic Programming (Lecture 3)
- [[Dynamic programming]] — policy evaluation, policy improvement, policy iteration, value iteration
- [[Value Iteration Equation]]

### Unit 5 — Monte Carlo Methods (Lecture 4)
- [[Monte Carlo Learning]] — first-visit / every-visit prediction, on-policy control, off-policy control via importance sampling

### Unit 6 — Temporal-Difference Learning (Lecture 5)
- [[Temporal-Difference Learning]] — TD(0), TD error
- [[Algorithms/SARSA|SARSA]] (on-policy TD control)
- [[Algorithms/Q-learning|Q-learning]] (off-policy TD control)

### Unit 7 — n-step Bootstrapping & Planning (Lecture 6)
- [[Algorithms/n-step SARSA|n-step SARSA]] — n-step return, spectrum between TD(0) and MC
- Monte Carlo Tree Search (Selection/Expansion/Simulation/Backup, UCT) — see [[Multi-armed bandits]] for the UCB connection

### PGT — Reward Shaping (Lecture I-PGT)
- Potential-based shaping functions, policy invariance theorem (Ng, Harada & Russell 1999)

### PGT — Eligibility Traces (Lectures III–IV PGT)
- λ-return, forward vs backward view
- [[Algorithms/SARSA(lambda)|SARSA(λ)]] — eligibility traces, TD(λ)

### Unit 8 — Value Function Approximation (Lectures 7–8)
- [[Linear MDPs & Linear Functional Approximation]] — feature vectors, SGD, semi-gradient methods
- [[Nonlinear Functional Approximation]] — the Deadly Triad, Bellman residual gradient
- [[Algorithms/Deep Q-Network|Deep Q-Network (DQN)]], [[Algorithms/Double Deep Q-Network|Double DQN]] — experience replay, target networks

### Unit 9 — Policy Gradient Methods (Lecture 8)
- [[Policy Gradient Theorem]]
- [[Algorithms/REINFORCE|REINFORCE]], REINFORCE with baseline
- [[Algorithms/Actor-Critic|Actor–Critic]] methods

### Unit 10 — Deep Reinforcement Learning (Lecture 10)
- [[Deep Reinforcement Learning]] — convergence/divergence with linear vs nonlinear approximation, off-policy divergence example, neural network basics, DQN, Double DQN

### Reference layer — theoretical RL & continuous control *(not MA338-assessed; canonical literature)*
- [[Algorithms/R-MAX|R-MAX]], [[Algorithms/Model-based Interval Estimation (MBIE)|MBIE]], [[Algorithms/MoRmax|MoRmax]] — PAC-MDP tabular exploration
- [[Algorithms/Upper-Confidence Fixed-Horizon (UCFH)|UCFH]], [[Algorithms/Upper Bounding the Expected Next State Value (UBEV)|UBEV]] — regret/PAC bounds for episodic MDPs
- [[Algorithms/Least-Squares Value Iteration (LSVI)|LSVI]], [[Algorithms/MatrixRL|MatrixRL]] — least-squares/linear function approximation with guarantees
- [[Algorithms/G-learning|G-learning]], [[Algorithms/Soft-Q-learning|Soft Q-learning]] — KL/entropy-regularised control
- [[Algorithms/Neural Fitted Q-learning|Neural Fitted Q-learning]] — batch-mode Q-learning with neural nets, DQN's predecessor
- [[Algorithms/DDPG|DDPG]], [[Algorithms/Proximal Policy Optimization|PPO]], [[Algorithms/Trust Region Policy Optimization|TRPO]] — modern continuous-control policy gradient
- [[Linear-quadratic problems]], [[Linear-quadratic regulator (LQR)]], [[Hamilton-Jacobi-Bellman equation]], [[Multi-agent LQ]] — classical optimal control, the continuous-state/action analogue of DP
- [[Inverse Reinforcement Learning]]
- [[Ensemble of Identical Independent Evaluators (EIIE)]], [[Differential Sharpe ratio]] — RL for portfolio management (links to `investment-automation`)

## Key dependency chains

```
Agent-environment Interface
        │
        ▼
Exploration vs Exploitation ──► Multi-armed bandits ──► {ε-greedy, UCB, Boltzmann, Thompson sampling}
        │                                                        │
        ▼                                                        ▼
Markov Decision Process                              Regret Analysis / Sample Complexity (theory layer)
        │
        ├──► State/Action value function ──► Bellman equation
        │                                          │
        │            ┌─────────────────────────────┼─────────────────────────────┐
        │            ▼                              ▼                              ▼
        │    Dynamic programming            Monte Carlo Learning         Temporal-Difference Learning
        │    (model-based, bootstraps)   (model-free, no bootstrap)      (model-free, bootstraps)
        │            │                              │                              │
        │       Value/Policy                  first/every-visit          TD(0) ──► SARSA / Q-learning
        │       Iteration                      MC control                          │
        │                                                                          ▼
        │                                                          n-step SARSA ──► SARSA(λ)
        │                                                          (n-step return)  (eligibility traces)
        │
        ▼
Value Function Approximation
        │
   ┌────┴─────┐
   ▼          ▼
Linear FA   Nonlinear FA ──► Deadly Triad ──► Deep RL ──► DQN ──► Double DQN
   │
   ▼
Policy Gradient Theorem ──► REINFORCE ──(+ baseline)──► Actor-Critic ──► {DDPG, TRPO, PPO}
```

## Exam focus

MA338 is assessed 70% exam / 30% coursework (10% lab assignment, 20% project). Past exam and revision-sheet questions (see `Resources/05 .../Revision/`) are numerical and concentrate very consistently on:

- **Bandit updates by hand**: incremental Qₙ₊₁ update, tracking which action is exploited vs explored across a short sequence of steps (`ε`-greedy trace).
- **Grid-world / small-MDP value iteration and policy iteration**: one or two Bellman-equation sweeps by hand, given explicit transition probabilities.
- **Monte Carlo estimation from a single given episode**: computing first-visit *and* every-visit Q(s,a) estimates from a short trajectory — these numbers differ and examiners test both on the same episode.
- **SARSA vs Q-learning update-by-hand on the same trajectory**: always asked as a pair, to test that the SARSA update uses the actually-taken next action A_{t+1} while Q-learning uses max_a Q(s',a). Compare and contrast is a recurring instruction.
- **MCTS by hand**: given a partially-built tree with q(v), n(v), compute UCT, walk through Selection → Expansion → Simulation → Backup for one iteration, then recommend the next action.
- **True/false + justification** questions on subtle properties: e.g. "does UCB visit every suboptimal action only once?" (no), "can REINFORCE improve a non-differentiable/discontinuous policy?" (no — differentiability is required), reward-shaping invariance (adding a constant to all rewards *can* change the optimal policy, even though scaling by a positive constant cannot — this is the potential-based-shaping vs arbitrary-shaping distinction).
- **Reward shaping proofs**: showing a transformation is/isn't policy-invariant, i.e. whether it can be written as $F(s,a,s') = γΦ(s') − Φ(s)$.

High-priority topics to be reviewed-confident on before the exam: iterative policy evaluation/improvement pseudocode, TD-error definition, importance-sampling ratio for off-policy MC, n-step return recursion, UCT formula, and the potential-based shaping theorem statement (sufficient + necessary directions).

## Open questions

- [ ] None of the four PGT lectures nor the ten numbered lectures explicitly cover the "theory layer" algorithms filed under `Algorithms/` (R-MAX, MBIE, MoRmax, UCFH, UBEV, LSVI, MatrixRL, G-learning, Soft-Q-learning, DDPG, PPO, TRPO) or the control-theory notes (LQR, HJB, Multi-agent LQ) — confirm whether these came from a different course/reading and, if so, which, so their `course:` frontmatter field can be corrected (currently filed under MA338 by default).
- [ ] `Ensemble of Identical Independent Evaluators (EIIE)` and `Differential Sharpe ratio` look like they belong to the `investment-automation` project (portfolio-management RL) rather than MA338 — confirm whether to keep them here or move/duplicate into a finance-RL note under `07 Finance & Markets`.
- [ ] No syllabus PDF exists for MA338 to cross-check the "Module Outline" against the final exam's actual weighting by topic — the exam-focus section above is inferred from the one available past paper + solutions set only.
- [ ] Coursework (`Assignment 1`: policy/value iteration on FrozenLake-style gridworlds; `RL-DP-Final-Project`: Q-learning, REINFORCE, SARSA, SARSA(λ), n-step SARSA compared on a discretised continuous-control task) has not yet been mined for idiosyncratic notation/conventions used in the write-up — worth a follow-up pass grounding the relevant `Algorithms/` notes against `report/MA338_DynamicRL_Final.pdf` once drafted.
