---
title: 'RT-1: Robotics Transformer for Real-World Control at Scale'
collection: papers
permalink: /papers/robotics/rt-1_robotics_transformer_for_real-world_control_at_scale/
date: '2022-12-13'
year: 2022
field: robotics
subfield: robot-foundation-models-vla
tasks:
- transformer-policy
- real-world-control
- scaling
tier: 2
artifact_type: paper
venue: arXiv / RSS 2023
authors:
- Anthony Brohan
- Noah Brown
- Justice Carbajal
- Yevgen Chebotar
authors_short: Brohan et al.
paperurl: https://arxiv.org/pdf/2212.06817.pdf
doi: 10.48550/arXiv.2212.06817
license: unspecified
summary: RT-1 introduces a transformer-based robotics policy trained on 130k real-world
  demonstrations across 700+ manipulation tasks using a FiLM-conditioned EfficientNet
  visual encoder and a TokenLearner-compressed transformer, achieving 97% success
  on seen tasks and demonstrating substantial generalization to novel objects and
  backgrounds.
why_important: Established the first credible evidence that large-scale real-world
  robot datasets combined with transformer-based policies can achieve reliable manipulation
  across hundreds of tasks, directly setting the baseline RT-2 improved upon and motivating
  the Open X-Embodiment data aggregation effort.
tags:
- transformer-policy
- rt1
- real-world
- scaling
- robotics
---

## Summary

RT-1 (Robotics Transformer 1), presented at RSS 2023, demonstrates that scaling data collection and model capacity for robot manipulation produces qualitatively better policies than previous approaches trained on smaller, task-specific datasets. Brohan et al. train a single policy across 700+ manipulation tasks on 13 robot arms in a single office environment, using approximately 130,000 teleoperated demonstrations collected over 17 months. The architecture processes current and recent camera images through an EfficientNet-B3 backbone whose features are conditioned on a natural language task description using Feature-wise Linear Modulation (FiLM). A TokenLearner module then compresses the resulting spatial feature maps into a compact sequence of learned token embeddings, which are processed by a transformer decoder that autoregressively predicts discretized end-effector action tokens (7 dimensions including position, rotation, and gripper state, each discretized to 256 bins).

The model achieves 97% success rate on tasks from its training distribution and 76% on novel task generalizations (new objects, new objects in new environments). Critically, RT-1 is evaluated against single-task specialist baselines trained on the same data for individual tasks, and it outperforms specialists despite sharing parameters across all 700+ tasks—demonstrating positive transfer rather than interference. The paper also evaluates robustness to perturbations: a person interrupting the robot during execution, sudden changes in lighting, and the presence of distractors. RT-1 shows substantially better robustness than prior baselines, attributed to the rich visual representation learned across diverse training scenarios.

The data collection infrastructure described in RT-1 represents a significant engineering contribution. The paper details the teleoperation setup (VR controllers with full end-effector 6-DoF control), the episode verification pipeline (human raters verify success, providing training signal without per-task reward engineering), and the annotation procedure (natural language task descriptions written by operators in real time). This end-to-end data collection pipeline has been adopted or adapted by multiple subsequent large-scale efforts, and its compatibility with the RLDS data format facilitated the later aggregation of RT-1 data into Open X-Embodiment.

## Why It Matters

RT-1 marked the moment when transformer-based scaling moved from NLP and computer vision into the physical manipulation domain with credible, reproducible real-robot results. Its demonstration that a single policy could match or exceed per-task specialists across hundreds of tasks shattered the assumption that multi-task robot learning necessarily incurs interference costs, and it established a clear scaling hypothesis: more diverse real-world data with a sufficiently expressive architecture yields better generalization. This hypothesis directly motivated Open X-Embodiment (scaling to more embodiments) and RT-2 (scaling to larger pre-trained models).

RT-1 also established evaluation standards that shaped subsequent work. Its 700+ task evaluation suite, robustness protocol, and quantified generalization tests have been referenced as baselines in dozens of subsequent papers. However, the paper's reliance on a single robot platform and a single building environment revealed a key limitation: policies trained in controlled environments do not automatically transfer to new visual domains. This gap motivated the in-the-wild collection philosophy of DROID and BridgeData V2, and the cross-embodiment aggregation of Open X-Embodiment—both of which build directly on RT-1's demonstration that large-scale manipulation data collection is tractable and productive.

| | |
|---|---|
| **Authors** | Brohan et al. |
| **Year** | 2022 |
| **Venue** | arXiv / RSS 2023 |
| **Field** | Robotics |
| **Subfield** | Robot Foundation Models Vla |
| **Tasks** | transformer-policy, real-world-control, scaling |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2212.06817.pdf){: .btn .btn--primary .btn--large}
