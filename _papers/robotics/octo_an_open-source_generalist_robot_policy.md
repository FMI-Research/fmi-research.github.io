---
title: 'Octo: An Open-Source Generalist Robot Policy'
collection: papers
permalink: /papers/robotics/octo_an_open-source_generalist_robot_policy/
date: '2024-05-20'
year: 2024
field: robotics
subfield: robot-foundation-models-vla
tasks:
- generalist-policy
- open-source
- multi-robot
- diffusion
tier: 2
artifact_type: paper
venue: arXiv / RSS 2024
authors:
- Octo Model Team
- Dibya Ghosh
- Homer Walke
- Karl Pertsch
authors_short: Octo Model Team
paperurl: https://arxiv.org/pdf/2405.12213.pdf
doi: 10.48550/arXiv.2405.12213
license: unspecified
summary: Octo is an open-source generalist robot policy trained on 800k trajectories
  from Open X-Embodiment using a transformer backbone with a diffusion action head,
  supporting both language and goal-image conditioning, and designed for rapid fine-tuning
  to new robot platforms with minimal additional data.
why_important: The most widely used open-source generalist robot policy baseline,
  enabling reproducible research on foundation model fine-tuning and cross-robot transfer
  without access to proprietary systems, and its diffusion action head architecture
  has become a reference design for open generalist policies.
tags:
- generalist-policy
- open-source
- robotics
- diffusion
- multi-robot
---

## Summary

Octo, presented at RSS 2024 by the Octo Model Team, is designed to address a practical gap in the robot learning ecosystem: while proprietary systems like RT-2 demonstrate impressive generalist capabilities, they are unavailable for community research, ablation, and fine-tuning. Octo is trained on approximately 800,000 trajectories drawn from the Open X-Embodiment dataset, representing 25 robot embodiments across diverse manipulation tasks. The architecture consists of a transformer trunk that processes tokenized observations (current and historical camera images encoded via a small CNN, plus optionally language instructions or goal images) and produces learned observation tokens that are passed to a diffusion action head for action generation. The diffusion head predicts action chunks—sequences of 4 future actions—following the receding-horizon execution paradigm from Diffusion Policy.

The design choices in Octo reflect deliberate decisions to balance generality with practical usability. Language conditioning is implemented through cross-attention between observation tokens and CLIP text embeddings, while goal-image conditioning replaces the text pathway with image embeddings, enabling deployment in settings where natural language instruction is impractical. The model comes in two sizes—Octo-Small (27M parameters) and Octo-Base (93M parameters)—both trained with publicly available weights and training code, along with standardized fine-tuning recipes. The authors demonstrate that a new robot platform and task can be incorporated into Octo in under an hour on a single GPU using as few as 200 demonstrations, substantially lowering the barrier to deploying a generalist policy on custom hardware.

Empirical evaluation covers both zero-shot performance (evaluating the pre-trained model without fine-tuning on held-out robot platforms from OXE) and fine-tuned performance. On zero-shot evaluation across OXE's held-out test split, Octo outperforms single-embodiment specialist baselines on most platforms, confirming positive cross-embodiment transfer. Fine-tuned Octo matches or exceeds state-of-the-art single-task policies on several manipulation benchmarks including tasks from BridgeData V2 and LIBERO with significantly less fine-tuning data than training specialists from scratch. The paper also evaluates the trade-off between language and goal-image conditioning, finding that goal-image conditioning yields better performance when goal images are available while language conditioning provides more task flexibility.

## Why It Matters

Octo occupies a unique position in the robot learning ecosystem: it is the most accessible fully-trained generalist policy available to the research community, serving as a standard baseline against which new methods are evaluated. Its open release of weights, code, and training recipes has enabled a wave of fine-tuning and adaptation research that would not be possible with proprietary systems. For labs without the infrastructure to train large models from scratch, Octo provides a high-quality starting point for downstream manipulation research and a reproducible reference implementation.

The model also highlights important architectural design questions that remain active research topics. The diffusion action head achieves better expressiveness than mean-regression heads but introduces latency from multiple denoising steps, and while action chunking improves temporal consistency, determining the optimal chunk length for different tasks remains empirical. The tension between language and goal-image conditioning modalities has not been fully resolved architecturally—a unified conditioning mechanism that gracefully handles both remains an open challenge. These questions, along with how to scale Octo-style training to 7B+ parameter backbones (as OpenVLA attempts), define the active frontier in open-source generalist policy research.

| | |
|---|---|
| **Authors** | Octo Model Team |
| **Year** | 2024 |
| **Venue** | arXiv / RSS 2024 |
| **Field** | Robotics |
| **Subfield** | Robot Foundation Models Vla |
| **Tasks** | generalist-policy, open-source, multi-robot, diffusion |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2405.12213.pdf){: .btn .btn--primary .btn--large}
