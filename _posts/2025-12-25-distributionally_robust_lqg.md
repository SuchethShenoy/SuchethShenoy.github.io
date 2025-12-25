---
title: "Distributionally Robust LQG"
date: 2025-12-25
permalink: /posts/2025/distributionally-robust-lqg/
tags:
  - control
  - robustness
  - distributionally-robust-optimization
---

Classical **Linear Quadratic Gaussian (LQG)** control occupies a central position in control theory due to its analytical tractability and elegant structure. For linear system dynamics, quadratic performance costs, and Gaussian disturbances, the optimal control policy is linear, and the design problem admits a clean separation between state estimation and feedback control.

This structural simplicity, however, rests on a strong modeling assumption:

> **the probability distributions of the exogenous disturbances are known exactly.**

In practical settings, this assumption is rarely satisfied. Even modest discrepancies between the assumed and true disturbance distributions can result in substantial performance degradation and loss of robustness. This fragility is closely connected to a classical observation by John C. Doyle in his seminal result *“Guaranteed Margins for LQG: There Are None,”* which demonstrates that LQG controllers, despite their optimality under nominal assumptions, do not enjoy guaranteed robustness margins, even arbitrarily close to the nominal model.

These considerations motivate the study of **Distributionally Robust LQG (DRLQ)** control, where uncertainty in disturbance distributions is explicitly modeled and incorporated into the control design.

---

## Classical LQG in Brief

Consider the discrete-time linear system
\[
x_{t+1} = A_t x_t + B_t u_t + w_t, \qquad
y_t = C_t x_t + v_t,
\]
with quadratic cost
\[
J = \mathbb{E}\!\left[
\sum_{t=0}^{T-1} \left( x_t^\top Q_t x_t + u_t^\top R_t u_t \right)
+ x_T^\top Q_T x_T
\right].
\]

Under the standard assumptions
\[
w_t \sim \mathcal{N}(0, W_t), \quad v_t \sim \mathcal{N}(0, V_t),
\]
the optimal policy has the form
\[
u_t = K_t \hat{x}_t,
\]
where \(\hat{x}_t = \mathbb{E}[x_t \mid y_{0:t}]\) is the Kalman filter estimate.

This is the celebrated **separation principle**.

---

## Distributional Robustness: A Min–Max View

Distributionally robust control replaces the single assumed noise distribution with an **ambiguity set**
\[
\mathcal{B} = \{ \mathbb{P} : \mathbb{D}(\mathbb{P}, \hat{\mathbb{P}}) \le \rho \},
\]
where:
- \(\hat{\mathbb{P}}\) is a nominal distribution (assumed Gaussian),
- \(\mathbb{D}(\cdot,\cdot)\) is a divergence (e.g., Wasserstein, KL),
- \(\rho\) controls the size of uncertainty.

The control problem becomes
\[
\min_{\pi} \; \max_{\mathbb{P} \in \mathcal{B}} \;
\mathbb{E}_{\mathbb{P}} \!\left[ J(\pi) \right],
\]
which is referred to as the Distributionally Robust Linear Quadratic (DRLQ) problem.

This is a **two-player zero-sum game**:
- the controller chooses a policy \(\pi\),
- an adversary (nature) chooses a distribution \(\mathbb{P}\).

---

## The Central Question

> **What is the structure of the worst-case disturbance distribution?**
> **Are linear policies still optimal under distributional uncertainty?**

---

## Main Result (Finite Horizon)

Assume:
- linear dynamics and quadratic costs,
- nominal disturbances are zero-mean Gaussian,
- ambiguity sets are defined using divergences such as
  - 2-Wasserstein distance,
  - Kullback–Leibler divergence,
  - moment-based divergences,
- ambiguity sets satisfy mild convexity and compactness conditions.

Then:
- the **worst-case disturbance distribution is Gaussian**, and
- the **optimal control policy is affine in the observations**.

Moreover, if the nominal disturbances are zero-mean, the optimal policy is **purely linear**:
\[
u_t = K_t \hat{x}_t.
\]

Thus, **distributional robustness does not alter the structural form of the LQG controller**.

---

## What Does the Adversary Do?

The adversary does *not* introduce exotic non-Gaussian noise.

Instead, it chooses disturbances with:
\[
\mathbb{E}[w_t] = 0, \qquad
\Sigma_{w_t} \succeq \hat{\Sigma}_{w_t},
\]
where \(\succeq\) denotes the Loewner (positive semidefinite) order.

**Interpretation:**  
Nature optimally inflates the disturbance covariance.

From a control perspective, this implies:
\[
\text{DRLQ} \;\approx\; \text{LQG with inflated noise covariance}.
\]

From a control-theoretic perspective, this result shows that covariance inflation is not merely a heuristic but emerges as the optimal response to distributional uncertainty: the worst-case disturbance distribution within the ambiguity set corresponds to a Gaussian with inflated covariance, and the robust controller is precisely the LQG controller designed for this worst-case covariance.

> *When you are unsure how noisy the world really is, the safest assumption is that it is noisier than you think — and distributional robustness shows that this instinct is mathematically optimal.*

---

## Affine vs Linear Policies

If nonzero noise means are allowed, the optimal policy takes the affine form
\[
u_t = K_t \hat{x}_t + k_t.
\]

However, under zero-mean nominal noise:
- the adversary’s optimal mean is also zero,
- the bias term vanishes,
- and the optimal policy is **linear**.

This explains why zero-mean assumptions are not merely convenient, but **worst-case optimal**. Intuitively, when the controller is allowed to plan for worst-case uncertainty, introducing a systematic bias in the disturbances is less harmful than increasing their variance. As a result, the adversary gains more by amplifying fluctuations than by shifting the mean, and the controller correspondingly has no incentive to introduce a constant bias term. In the worst case, the safest—and optimal—strategy is therefore to remain centered and respond linearly to deviations.

> *From a worst-case perspective, shifting the mean is less damaging than increasing uncertainty. The adversary therefore chooses zero-mean noise with larger variance, and the optimal controller has no reason to include a bias term.*

---

## Infinite-Horizon Case

In the infinite-horizon average-cost setting, the same structure persists:
- the optimal controller is **stationary and linear**,
- the worst-case noise is **time-invariant Gaussian**,

In the infinite-horizon setting, transient effects vanish and only long-term average behavior matters. Any time-varying or nonstationary strategy by the adversary would introduce patterns that the controller could eventually learn and exploit, reducing their worst-case impact. The most damaging strategy is therefore one that is stationary and persistent, repeatedly injecting uncertainty in the same statistical form.

> *Over an infinite horizon, the worst case is not changing uncertainty, but persistent uncertainty—and linear, time-invariant control is exactly what is needed to handle it.*

---

## Computational Insight

The problem admits an efficient solution using a **Frank–Wolfe algorithm** over covariance matrices.

Each iteration solves a **standard LQG subproblem**:
- Kalman filtering for estimation,
- Riccati recursions for control.

The Frank–Wolfe method is particularly well suited to this setting because it exploits the convex structure of the ambiguity sets while avoiding expensive projections onto semidefinite constraints. Instead of solving a full semidefinite program at each step, the algorithm iteratively moves toward a worst-case covariance by solving linearized subproblems, each of which reduces to a classical LQG problem. As a result, the distributionally robust control problem can be solved using familiar Kalman filtering and Riccati recursions, retaining both computational efficiency and interpretability.

> *Frank–Wolfe preserves the structure of LQG by pushing all computational complexity into covariance updates, leaving the control problem itself untouched.*

---

## Why This Matters for Learning-Based Control

These results have implications that extend well beyond classical LQG. Most notably, they demonstrate that **robustness and structure are not inherently in conflict**: principled uncertainty modeling can preserve, rather than destroy, the structural simplicity of optimal controllers.

A key insight is that adversarial uncertainty does not necessarily induce pathological behavior or complex control laws. Instead, in this setting, worst-case uncertainty manifests primarily as **increased variance**, rather than as a need for fundamentally different policy structures. This observation helps explain why structured controllers often remain effective even under significant model mismatch.

From a learning perspective, this supports approaches that:
- incorporate **control-theoretic structure** into policy parameterizations,
- treat uncertainty as a first-class modeling element rather than an afterthought,
- and avoid relying solely on black-box robustness mechanisms.

Taken together, these insights suggest a productive direction for learning-based control: leveraging learning to handle complexity and uncertainty, while retaining structure where it provides reliability, interpretability, and guarantees.

---

## Takeaway

> *Even under distributional uncertainty, the LQG structure survives: linear policies remain optimal, and Gaussian disturbances remain worst-case.*

---

### Reference
- B. Taşkesen, D. A. Iancu, Ç. Koçyiğit, D. Kuhn,  
  *Optimality of Linear Policies in Distributionally Robust Linear Quadratic Control*,  
  arXiv:2508.11858.  
  [[paper]](https://arxiv.org/pdf/2508.11858) [[slides]](/files/blog_drlq_slides.pdf)
