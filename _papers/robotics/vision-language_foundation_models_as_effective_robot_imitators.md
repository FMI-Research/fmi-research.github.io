---
title: Vision-Language Foundation Models as Effective Robot Imitators
collection: papers
permalink: /papers/robotics/vision-language_foundation_models_as_effective_robot_imitators/
date: '2023-11-02'
year: 2023
field: robotics
subfield: foundation-models-vla
tasks:
- vla
- instruction-following
- robot-imitation
tier: 2
artifact_type: paper
venue: ICLR 2024
authors:
- Xinghang Li
- Minghuan Liu
- Hanbo Zhang
- Cunjun Yu
- Jie Xu
- Hongtao Wu
- Chilam Cheang
- Ya Jing
- Weinan Zhang
- Huaping Liu
- Hang Li
- Tao Kong
authors_short: Li et al.
paperurl: https://arxiv.org/pdf/2311.01378.pdf
doi: 10.48550/arXiv.2311.01378
license: unspecified
summary: RoboFlamingo adapts Open Flamingo to robot manipulation by parameter-efficiently
  fine-tuning only its gated cross-attention layers while appending a lightweight
  MLP policy head that outputs end-effector pose distributions; it frames manipulation
  as a multi-turn vision-language conversation — leveraging Flamingo's in-context
  learning for demonstration conditioning — and achieves 82.4% average task completion
  across 5-task chains on the CALVIN ABC→D split, outperforming prior state-of-the-art
  by a large margin.
why_important: Established the parameter-efficient VLM adaptation recipe for robot
  control (freeze backbone, fine-tune cross-attention, append action head), making
  VLA research accessible without massive compute and demonstrating that open-source
  VLMs already encode sufficient physical grounding for instruction-conditioned manipulation;
  per-step autoregressive inference through a large LLM backbone produces ~2–5Hz control
  rates incompatible with reactive tasks, motivating later decoupled architectures
  (GR-1, π0, Octo) that separate high-frequency action generation from slow VLM reasoning.
tags:
- vla
- flamingo
- robot-imitation
- instruction-following
- calvin
---

## Summary

RoboFlamingo adapts the Open Flamingo multi-modal language model — pretrained on interleaved image-text web data via a contrastive and autoregressive objective — to language-conditioned robot manipulation by appending a lightweight MLP policy head downstream of the frozen-or-partially-frozen Flamingo transformer. The policy head maps Flamingo's final hidden-state outputs (one per visual token, per timestep) to a mixture-of-Gaussians distribution over end-effector poses: 3D position, quaternion orientation, and binary gripper state. The full architecture processes a sequence of (language-instruction, image-observation) pairs as a multi-turn conversation in Flamingo's interleaved format, leveraging its in-context learning capability to condition on one or more demonstration examples provided directly in the prompt — without requiring gradient updates to utilize those demonstrations. Fine-tuning focuses selectively on Flamingo's gated cross-attention blocks (which integrate visual features into the language representation stream) while keeping the self-attention and feed-forward layers frozen, enabling effective task adaptation on a single 8-GPU node.

RoboFlamingo is evaluated on the CALVIN benchmark, a comprehensive testbed for language-conditioned long-horizon manipulation requiring a Franka Panda arm to complete sequences of up to 5 natural-language-specified sub-tasks (e.g., "push the red block left, then turn on the light, then open the drawer") in a tabletop environment with significant visual and layout variation. On the hardest evaluation split — CALVIN ABC→D, where the policy is trained on three tabletop environments and evaluated on a fourth unseen one — RoboFlamingo achieves 82.4% average task completion across 5-task chains at the time of publication, surpassing prior state-of-the-art methods including SuSIE (62.9%) and MCIL (30.3%) by large margins. The 5-task chain metric compounds per-step success rates, making it highly sensitive to early failures and a demanding measure of consistent policy performance across diverse sub-tasks and language phrasings.

The central methodological contribution is the parameter-efficient fine-tuning strategy: by updating only the gated cross-attention layers (~15% of total parameters) while keeping the rest of Flamingo frozen, RoboFlamingo achieves strong task performance without the computational cost of full fine-tuning. The gated cross-attention blocks are precisely the interface between the pre-trained language representations and the incoming visual tokens — updating them alone is sufficient to re-route Flamingo's semantic processing toward manipulation-relevant visual features without disrupting the language generation capability. An ablation over which layers to unfreeze confirms this: unfreezing more layers (or fewer) both yield worse CALVIN performance, suggesting a "sweet spot" at the cross-modal interface. The policy head uses a mixture of Gaussians rather than a unimodal Gaussian to handle the multimodal action distributions that arise from demonstration-to-demonstration style variation.

## Why It Matters

RoboFlamingo established a clear, reproducible, and computationally accessible recipe for converting a pretrained open-source VLM into a competitive manipulation policy: freeze most of the backbone, fine-tune cross-attention layers, append a lightweight action head. This "adaptation over pretraining" paradigm was influential because it democratized VLA research — labs without access to massive compute or large proprietary robot datasets could fine-tune Open Flamingo on their own robot demonstrations and achieve competitive performance. The CALVIN state-of-the-art result provided strong empirical evidence that open-source VLMs, trained entirely on web data with no robot-specific supervision, already encode sufficient physical and linguistic grounding to support complex instruction-conditioned manipulation — a claim that was contested prior to this paper and that opened VLM-to-robot transfer as a mainstream research direction.

The approach has fundamental limitations tied to its autoregressive inference architecture. At each timestep, the policy must run a complete forward pass through the full Flamingo transformer (3B+ parameters) to predict a single end-effector action, yielding inference frequencies of approximately 2–5Hz — far below the 20–50Hz rates required for reactive or contact-rich manipulation. The in-context demonstration examples consume a substantial portion of the context window, constraining the number of shots that can be provided. These latency and context-length constraints make RoboFlamingo impractical for tasks requiring rapid reactive control (e.g., catching, contact-rich assembly, dynamic object tracking). Subsequent architectures addressed the latency problem through architectural separation: GR-1 uses a smaller GPT backbone with a dedicated action head, π0 decouples the VLM from a fast flow-matching action expert, and Octo employs a compact Transformer with an action head trained via diffusion — all motivated in part by the practical deployment limitations exposed by RoboFlamingo's inference profile.

| | |
|---|---|
| **Authors** | Li et al. |
| **Year** | 2023 |
| **Venue** | ICLR 2024 |
| **Field** | Robotics |
| **Subfield** | Foundation Models Vla |
| **Tasks** | vla, instruction-following, robot-imitation |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2311.01378.pdf){: .btn .btn--primary .btn--large}
