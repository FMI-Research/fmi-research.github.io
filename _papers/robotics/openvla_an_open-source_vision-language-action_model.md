---
title: 'OpenVLA: An Open-Source Vision-Language-Action Model'
collection: papers
permalink: /papers/robotics/openvla_an_open-source_vision-language-action_model/
date: '2024-06-13'
year: 2024
field: robotics
subfield: robot-foundation-models-vla
tasks:
- vla
- open-source
- manipulation
- evaluation
tier: 2
artifact_type: paper
venue: arXiv 2024
authors:
- Moo Jin Kim
- Karl Pertsch
- Siddharth Karamcheti
- Ted Xiao
authors_short: Kim et al.
paperurl: https://arxiv.org/pdf/2406.09246.pdf
doi: 10.48550/arXiv.2406.09246
license: unspecified
summary: OpenVLA is a 7-billion-parameter open-source vision-language-action model
  built on a Prismatic VLM (DINOv2 and SigLIP visual encoders with a Llama-2 backbone)
  and fine-tuned on 970k robot trajectories from Open X-Embodiment, achieving 16.5%
  average absolute improvement over the strongest prior open-source baseline while
  releasing full training infrastructure.
why_important: The first open-source VLA at 7B parameter scale to demonstrate competitive
  performance with proprietary systems, enabling the community to reproduce, fine-tune,
  and extend VLA research without access to closed APIs, and establishing LoRA fine-tuning
  as a practical adaptation strategy for resource-constrained labs.
tags:
- vla
- open-source
- robotics
- manipulation
---

## Summary

OpenVLA, presented in 2024, directly responds to a reproducibility crisis in the VLA literature: the highest-performing VLA models (RT-2, RT-2-X) are closed-source proprietary systems, making it impossible for the broader research community to ablate their design decisions, fine-tune them for new tasks, or build on their capabilities. Kim et al. develop OpenVLA using the Prismatic framework, which combines two complementary visual encoders—DINOv2 (emphasizing semantic features) and SigLIP (emphasizing visual-language alignment)—whose outputs are projected into the embedding space of a Llama-2 7B language model. Robot actions are represented as text tokens following the RT-2 convention, with each action dimension quantized to 256 bins and expressed as a string of decimal integers. The model is fine-tuned on a carefully curated 970k-trajectory subset of Open X-Embodiment, with dataset mixture weights tuned to balance coverage across embodiments and task types.

The empirical evaluation is notable for its breadth and methodological care. OpenVLA is evaluated on the BridgeData V2 benchmark, the Google Robot benchmark (derived from RT-2's evaluation suite), and the LIBERO suite, covering both seen and unseen task distributions. It achieves an average 16.5% absolute improvement over Octo-Base across these benchmarks, and on Google Robot tasks it approaches the reported performance of RT-2 (55B parameters) despite an 8× smaller parameter count. The paper also includes a direct comparison of fine-tuning strategies—full fine-tuning versus LoRA—finding that parameter-efficient LoRA fine-tuning with as few as 200 demonstrations achieves 90%+ of full fine-tuning performance on single-task benchmarks while using 7× less GPU memory, a practically important finding for labs with limited compute.

OpenVLA's methodological contributions extend beyond the model itself. The authors release a comprehensive training codebase built on the Hugging Face Transformers ecosystem, pre-computed dataset shards for Open X-Embodiment, evaluation scripts for BridgeData and LIBERO, and model weights under an open license. They also provide a detailed analysis of failure modes: the model struggles with precise contact tasks requiring sub-centimeter positioning accuracy, tasks specified through spatial reasoning in cluttered scenes, and very long-horizon task sequences. This failure mode analysis directly informs where the community should focus architectural and data improvements.

## Why It Matters

OpenVLA is a landmark in making frontier VLA research accessible and reproducible. Its open release at 7B parameters—with weights, code, data, and evaluation infrastructure—represents a genuine scientific contribution independent of its empirical results, because it creates the conditions for cumulative community progress rather than repeatedly re-implementing closed systems. The immediate community uptake—with numerous papers fine-tuning OpenVLA within months of release—validates the model's utility as a research platform and confirms that open releases of this scale are both feasible and impactful.

The model also crystallizes several design questions actively debated in the field. The choice to represent actions as text tokens (following RT-2) rather than using a specialized action head (as in Octo's diffusion head) imposes a discretization loss that may limit performance on precision manipulation tasks, and the optimal balance between these approaches remains an open question. OpenVLA's strong LoRA fine-tuning results suggest that pre-trained VLM features already capture task-relevant representations, and that manipulation-specific adaptation can be achieved through low-rank updates to a small subset of parameters—a finding with significant practical implications for deploying VLAs across diverse real-world robot applications with heterogeneous task requirements.

| | |
|---|---|
| **Authors** | Kim et al. |
| **Year** | 2024 |
| **Venue** | arXiv 2024 |
| **Field** | Robotics |
| **Subfield** | Robot Foundation Models Vla |
| **Tasks** | vla, open-source, manipulation, evaluation |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2406.09246.pdf){: .btn .btn--primary .btn--large}
