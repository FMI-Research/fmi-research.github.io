---
title: 'Diffusion Policy: Visuomotor Policy Learning via Action Diffusion'
collection: papers
permalink: /papers/robotics/diffusion_policy_visuomotor_policy_learning_via_action_diffusion/
date: '2023-03-06'
year: 2023
field: robotics
subfield: robot-learning-manipulation
tasks:
- visuomotor-policy
- diffusion
- action-prediction
tier: 2
artifact_type: paper
venue: arXiv / RSS 2023
authors:
- Cheng Chi
- Siyuan Feng
- Yilun Du
- Zhenjia Xu
authors_short: Chi et al.
paperurl: https://arxiv.org/pdf/2303.04137.pdf
doi: 10.48550/arXiv.2303.04137
license: unspecified
summary: Diffusion Policy parameterizes a robot visuomotor policy as a conditional
  denoising diffusion probabilistic model over action sequences, achieving state-of-the-art
  performance across diverse manipulation tasks by modeling complex multimodal action
  distributions through iterative denoising.
why_important: Introduced diffusion-based policy learning as the dominant paradigm
  for robot manipulation, establishing the action-chunking diffusion head now standard
  in generalist policies including Octo, and inspiring follow-on work on flow matching
  and consistency policies.
tags:
- diffusion-policy
- visuomotor
- manipulation
- action-diffusion
---

## Summary

Chi et al. introduce Diffusion Policy at RSS 2023, framing robot policy learning as a conditional score-matching problem: rather than predicting a single action or parameterizing a unimodal Gaussian, the policy learns to denoise a sequence of actions from Gaussian noise conditioned on visual observations. During inference, action sequences are sampled by iteratively applying the learned denoising network starting from pure noise, converging to a coherent, executable trajectory. The authors implement two variants of the denoising backbone: a CNN-based architecture operating on temporal feature maps and a transformer-based architecture using cross-attention to condition on observation tokens. Both are conditioned on current and recent camera images, enabling closed-loop visuomotor control through receding-horizon execution of predicted action chunks.

The empirical evaluation spans 11 manipulation tasks including simulated benchmarks (Push-T, Block Pushing, Robomimic) and real hardware tasks (robotic brushing, spreading, and pouring), representing a systematic coverage of multi-modal, contact-rich, and precision-demanding scenarios. Diffusion Policy outperforms prior BC baselines—including Implicit Behavioral Cloning (IBC) and Behavior Transformer (BET)—by substantial margins across nearly all tasks, with particularly strong improvements on tasks exhibiting multimodal action distributions where multiple qualitatively different trajectories solve the task. The transformer variant achieves the highest overall performance while the CNN variant provides a better speed-accuracy trade-off for real-time control at 10 Hz.

A key methodological contribution is the empirical analysis of what makes diffusion policies work well. Action chunking—predicting a sequence of future actions rather than a single step—proves critical for stability, smoothing out noisy denoising artifacts and enabling temporally consistent motion. The authors also study the impact of observation history, noise schedule selection, and the choice between DDPM and DDIM samplers, with DDIM enabling 10× faster inference with minimal quality degradation. The paper's thorough ablation study provides practical guidance that has shaped how diffusion policies are implemented in every subsequent system that adopts this architecture.

## Why It Matters

Diffusion Policy fundamentally changed how the robotics community thinks about action representation. Prior to this work, behavioral cloning was almost universally implemented with mean squared error regression to a single predicted action, which implicitly assumes a unimodal action distribution—an assumption violated whenever a task has multiple valid solution strategies. By directly addressing this limitation with compelling empirical results, Diffusion Policy prompted rapid adoption of diffusion-based action heads across the field. Within two years, diffusion action heads had become the default architecture in generalist systems like Octo and a competitive alternative to autoregressive token prediction in VLA systems.

The paper also opened a rich set of follow-on research questions that remain actively studied. Can diffusion policies be made fast enough for high-frequency control (>100 Hz) without consistency model approximations? How should diffusion be combined with language conditioning in a VLA framework? And can the expressiveness of diffusion over long action horizons be exploited for contact-rich tasks where force profiles are inherently multimodal? The consistency policy, flow matching policy, and diffusion-VLA hybrid architectures that appeared in 2024 all trace their direct lineage to this paper's formulation, cementing its position as one of the most influential works in modern robot learning.

| | |
|---|---|
| **Authors** | Chi et al. |
| **Year** | 2023 |
| **Venue** | arXiv / RSS 2023 |
| **Field** | Robotics |
| **Subfield** | Robot Learning Manipulation |
| **Tasks** | visuomotor-policy, diffusion, action-prediction |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2303.04137.pdf){: .btn .btn--primary .btn--large}
