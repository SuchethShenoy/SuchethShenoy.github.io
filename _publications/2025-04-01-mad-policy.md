---
title: "MAD: A Magnitude and Direction Policy Parametrization for Stability Constrained Reinforcement Learning"
collection: publications
category: conferences
permalink: /publication/2025-mad-policy
excerpt: "A structured policy parametrization for stability-constrained reinforcement learning."
date: 2025-04-01
venue: "arXiv (accepted at CDC 2025)"
paperurl: "https://arxiv.org/pdf/2504.02565"
citation: "Furieri, L., Shenoy, S., Saccani, D., Martin, A., & Ferrari-Trecate, G. (2025). <i>MAD: A Magnitude and Direction Policy Parametrization for Stability Constrained Reinforcement Learning</i>. arXiv:2504.02565."
---

**Abstract**  
We introduce magnitude and direction (MAD) policies, a policy parameterization for reinforcement learning (RL) that preserves Lp closed-loop stability for nonlinear dynamical systems. Despite their completeness in describing all stabilizing controllers, methods based on nonlinear Youla and system-level synthesis are significantly impacted by the difficulty of parametrizing Lp-stable operators. In contrast, MAD policies introduce explicit feedback on state-dependent features - a key element behind the success of reinforcement learning pipelines - without jeopardizing closed-loop stability. This is achieved by letting the magnitude of the control input be described by a disturbance-feedback Lp-stable operator, while selecting its direction based on state-dependent features through a universal function approximator. We further characterize the robust stability properties of MAD policies under model mismatch. Unlike existing disturbance-feedback policy parametrizations, MAD policies introduce state-feedback components compatible with model-free RL pipelines, ensuring closed-loop stability with no model information beyond assuming open-loop stability. Numerical experiments show that MAD policies trained with deep deterministic policy gradient (DDPG) methods generalize to unseen scenarios - matching the performance of standard neural network policies while guaranteeing closed-loop stability by design.