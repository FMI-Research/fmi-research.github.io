---
title: A Survey on Vision-Language-Action Models for Embodied AI
collection: papers
permalink: /papers/robotics/a_survey_on_vision-language-action_models_for_embodied_ai/
date: '2024-05-23'
year: 2024
field: robotics
subfield: robot-foundation-models-vla
tasks:
- survey
- vla
- embodied-ai
- planning
- control
tier: 1
artifact_type: paper
venue: arXiv 2024
authors:
- Yueen Ma
- Zixing Song
- Yuzheng Zhuang
- Jianye Hao
authors_short: Ma et al.
paperurl: https://arxiv.org/pdf/2405.14093.pdf
doi: 10.48550/arXiv.2405.14093
license: unspecified
summary: A 2024 survey that taxonomizes Vision-Language-Action models for embodied
  AI along four axes—pre-training backbone, action generation mechanism, training
  paradigm, and operational role—covering architecture design choices, training strategies,
  and the critical planner-versus-controller distinction.
why_important: Provides the definitive conceptual framework for understanding the
  rapidly expanding VLA model space, enabling researchers to situate specific models
  (RT-2, OpenVLA, Octo) within a coherent design space and identify which architectural
  decisions most strongly influence real-world performance.
tags:
- survey
- vla
- embodied-ai
- vision-language-action
---

## Summary

Vision-Language-Action (VLA) models represent the convergence of pre-trained visual understanding, natural language processing, and robotic control within a single neural architecture. Ma et al. survey this rapidly evolving model class as of mid-2024, when RT-2, PaLM-E, OpenVLA, and Octo had established proof-of-concept results but the field lacked a unified framework for comparing their design choices. The survey introduces a taxonomy along four dimensions: the pre-training backbone (pure language model, vision-language model, or multimodal foundation model); the action generation mechanism (autoregressive token prediction, diffusion head, or direct regression); the training paradigm (end-to-end fine-tuning versus frozen backbone with learned action head); and the operational role (high-level planner that outputs skill primitives versus low-level controller that outputs joint or end-effector commands directly).

The planner-versus-controller distinction receives particular attention, as it represents a fundamental architectural choice with cascading implications. VLAs used as high-level planners (SayCan, Code as Policies) rely on a separate low-level controller to execute generated sub-goals, enabling the use of large unmodified language models at the cost of error propagation across the interface. VLAs used as direct low-level controllers (RT-2, OpenVLA) must bridge the gap between the high-dimensional, slow language token space and the continuous, high-frequency action space, necessitating tokenization schemes or auxiliary action heads. The survey analyzes trade-offs in latency, generalization, and sample efficiency across these design choices, providing concrete guidance for researchers selecting an architecture for a specific application context.

Evaluation methodology receives rigorous treatment. The survey reviews simulation benchmarks (RLBench, LIBERO, CALVIN, MetaWorld) and real-robot evaluation protocols, critically analyzing inter-study comparability. A persistent finding is that results on simulation benchmarks do not reliably predict real-robot performance, partly due to visual distribution shift and partly due to differences in control frequency and proprioceptive feedback availability. The authors call for standardized evaluation protocols and shared held-out test suites, a recommendation that has been partially addressed by subsequent Open X-Embodiment evaluation initiatives.

## Why It Matters

The VLA survey arrives at a moment when the field is rapidly prototyping many different architectural configurations without a clear consensus on best practices. By providing a structured taxonomy, it gives researchers a principled basis for choosing among design options rather than following the latest preprint uncritically. Its analysis of the planner-controller spectrum is particularly valuable because conflating these two roles has led to misinterpretations of results across papers—a high-level planner evaluated on sub-goal selection success is solving a fundamentally different problem than a low-level controller evaluated on raw manipulation success.

The survey also highlights evaluation fragmentation as a scientific problem requiring community coordination. The lack of standardized benchmarks makes it difficult to determine whether performance improvements in recent papers reflect genuine algorithmic progress or improvements in data curation, compute budget, or hardware setup. This concern has motivated subsequent initiatives toward shared evaluation benchmarks, and the survey's call for methodological standardization has influenced how subsequent VLA papers structure their empirical contributions. Its coverage of training strategies—particularly the debate over full fine-tuning versus parameter-efficient methods like LoRA—remains directly relevant as the field scales models toward 7B+ parameters.

| | |
|---|---|
| **Authors** | Ma et al. |
| **Year** | 2024 |
| **Venue** | arXiv 2024 |
| **Field** | Robotics |
| **Subfield** | Robot Foundation Models Vla |
| **Tasks** | survey, vla, embodied-ai, planning, control |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2405.14093.pdf){: .btn .btn--primary .btn--large}
