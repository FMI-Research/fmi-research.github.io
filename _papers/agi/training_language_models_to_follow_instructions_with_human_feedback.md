---
title: Training language models to follow instructions with human feedback
collection: papers
permalink: /papers/agi/training_language_models_to_follow_instructions_with_human_feedback/
date: '2022-03-04'
year: 2022
field: agi
subfield: alignment-safety-evaluation
tasks:
- rlhf
- instruction-following
- alignment
tier: 1
artifact_type: paper
venue: NeurIPS 2022
authors:
- Long Ouyang
- Jeffrey Wu
- Xu Jiang
- Diogo Almeida
authors_short: Ouyang et al.
paperurl: https://cdn.openai.com/papers/Training_language_models_to_follow_instructions_with_human_feedback.pdf
doi: ''
license: unspecified
summary: InstructGPT combines supervised fine-tuning on human demonstrations with
  PPO-based reinforcement learning from human feedback (RLHF) via a trained reward
  model, showing that a 1.3B-parameter aligned model is preferred over unaligned GPT-3
  175B by human raters 85% of the time.
why_important: Established the three-stage SFT→RM→RLHF pipeline that became the dominant
  post-training paradigm, and directly catalyzed the development of DPO, RLAIF, and
  Constitutional AI as alternative or complementary alignment approaches.
tags:
- rlhf
- alignment
- instruction-following
- post-training
---

## Summary

InstructGPT operationalizes a three-stage post-training pipeline for aligning GPT-3 to human intent. First, supervised fine-tuning (SFT) on a dataset of human-written prompt–response demonstrations produced by a team of specialist labelers. Second, a reward model (RM) is trained on human preference comparisons between pairs of model outputs, learning a scalar quality signal. Third, the SFT model is further optimized with Proximal Policy Optimization (PPO) against the RM, subject to a KL-divergence penalty relative to the original SFT model to prevent the policy from exploiting reward-model errors (reward hacking). The resulting InstructGPT models exist at 1.3B, 6B, and 175B parameter scales.

The key empirical result is striking: InstructGPT 1.3B is preferred by human labelers over GPT-3 175B approximately 85% of the time in blind side-by-side comparisons, demonstrating that alignment quality is not simply a function of scale. InstructGPT models also score substantially higher on TruthfulQA (measuring avoidance of common human misconceptions), produce less toxic output on RealToxicityPrompts, and show improved performance on public NLP benchmarks after alignment. The KL penalty proves critical: without it, PPO-trained models collapse toward degenerate strategies that maximize reward while becoming incoherent.

Methodologically, the paper makes several important contributions beyond the pipeline itself. It introduces a rigorous labeler agreement study to verify that the RM captures broadly shared human preferences rather than idiosyncratic annotator views. The use of a mixed training distribution — combining RLHF-optimized prompts with SFT data — during the PPO stage prevents catastrophic forgetting on the original capability distribution. The paper also demonstrates that models can be steered toward helpfulness without needing explicit harm labels, as the preference data implicitly encodes harm avoidance through comparative ranking.

## Why It Matters

InstructGPT established the SFT→RM→RLHF pipeline as the de facto post-training paradigm for production LLMs, and essentially every major instruction-following model released since — including ChatGPT, Claude, Gemini, and Llama 2 Chat — uses a variant of this framework. It demonstrated empirically that alignment with human preferences is achievable at scale without degrading core capabilities, resolving early skepticism about whether RLHF would generalize beyond narrow task settings.

The paper's most significant long-term influence may be the research agenda it implicitly defined: how to scale the reward model, how to reduce dependence on expensive human labelers, and how to prevent reward hacking. These questions directly motivated Constitutional AI (RLAIF), Direct Preference Optimization (DPO), reward model ensembles, and the scalable oversight literature. Its limitations — sensitivity to annotator demographics, reward model overfitting, and the complexity of the PPO training loop — continue to drive the preference-tuning research frontier.

| | |
|---|---|
| **Authors** | Ouyang et al. |
| **Year** | 2022 |
| **Venue** | NeurIPS 2022 |
| **Field** | Agi |
| **Subfield** | Alignment Safety Evaluation |
| **Tasks** | rlhf, instruction-following, alignment |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://cdn.openai.com/papers/Training_language_models_to_follow_instructions_with_human_feedback.pdf){: .btn .btn--primary .btn--large}
