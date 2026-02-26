---
title: 'Direct Preference Optimization: Your Language Model is Secretly a Reward Model'
collection: papers
permalink: /papers/agi/direct_preference_optimization_your_language_model_is_secretly_a_reward_model/
date: '2023-05-29'
year: 2023
field: agi
subfield: alignment-safety-evaluation
tasks:
- preference-optimization
- alignment
tier: 1
artifact_type: paper
venue: arXiv / ICLR 2024
authors:
- Rafael Rafailov
- Archit Sharma
- Eric Mitchell
- Christopher D. Manning
authors_short: Rafailov et al.
paperurl: https://arxiv.org/pdf/2305.18290.pdf
doi: 10.48550/arXiv.2305.18290
license: unspecified
summary: DPO derives a closed-form reparameterization of the KL-constrained RLHF objective,
  expressing the optimal policy as a function of the reference policy and enabling
  preference data to supervise the policy directly via a binary cross-entropy loss
  — without a separately trained reward model or online RL sampling.
why_important: Dramatically simplified the alignment training pipeline, making preference
  optimization accessible without PPO infrastructure, and spawned an active research
  area of DPO variants (IPO, KTO, ORPO) that continue to refine its theoretical and
  empirical properties.
tags:
- dpo
- preference-optimization
- alignment
- post-training
---

## Summary

DPO derives a surprising equivalence: the optimal policy under the KL-penalized RLHF objective can be expressed in closed form as a function of the reference policy and the (unknown) reward function. By inverting this relationship, the reward can be written as a function of the policy ratio between the current policy and a frozen reference policy, allowing the reward to be eliminated from training entirely. The resulting DPO loss is a binary cross-entropy objective over preference pairs (preferred response *y_w* vs. rejected response *y_l*), weighted by the log-ratio of policy probabilities, which increases the likelihood of preferred responses and decreases the likelihood of rejected ones relative to the reference — all without ever instantiating an explicit reward model.

Empirically, DPO matches or outperforms PPO-based RLHF on the summarization task (TL;DR dataset) and single-turn dialogue (Anthropic HH dataset) evaluated by both automatic metrics and GPT-4 judge comparisons. On sentiment-controlled generation, DPO achieves reward scores comparable to PPO at substantially lower KV-memory and compute cost, since it eliminates the separate RM inference pass and the online rollout loop required by PPO. The implicit reward learned by DPO — recoverable from the policy ratio — correlates with human preference annotations at rates similar to explicitly trained reward models.

Methodologically, the key innovation is the reparameterization of the Bradley–Terry preference model in terms of the policy ratio, collapsing the two-stage RM-then-RL training into a single offline supervised optimization. This also eliminates several PPO-specific engineering challenges: no reward model to overfit, no separate rollout buffer to maintain, and no clipping hyperparameters to tune. The paper provides a theoretical proof that DPO converges to the same fixed point as RLHF under mild assumptions, while also identifying conditions under which the two diverge in practice.

## Why It Matters

DPO's combination of theoretical elegance and practical simplicity made it immediately influential: within months of release it became the default preference-tuning baseline for open-source alignment research, replacing PPO in most academic alignment papers. Its accessibility catalyzed a wave of variants — IPO (which regularizes more conservatively), KTO (which uses individual binary feedback without paired preferences), ORPO (which unifies SFT and preference learning), and SimPO (which removes the reference model) — each probing the boundary conditions of the DPO reparameterization.

Despite its adoption, DPO has known limitations that continue to motivate research. Because it operates offline on a fixed preference dataset, it does not improve the distribution of generations seen during preference learning — unlike PPO, which actively generates and evaluates new responses. This offline bias can cause reward underoptimization on out-of-distribution prompts. Addressing this gap, through hybrid online/offline DPO variants and iterative self-play, remains an active and productive research direction.

| | |
|---|---|
| **Authors** | Rafailov et al. |
| **Year** | 2023 |
| **Venue** | arXiv / ICLR 2024 |
| **Field** | Agi |
| **Subfield** | Alignment Safety Evaluation |
| **Tasks** | preference-optimization, alignment |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2305.18290.pdf){: .btn .btn--primary .btn--large}
