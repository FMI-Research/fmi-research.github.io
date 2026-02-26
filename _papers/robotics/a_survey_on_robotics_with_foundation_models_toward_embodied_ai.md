---
title: 'A Survey on Robotics with Foundation Models: toward Embodied AI'
collection: papers
permalink: /papers/robotics/a_survey_on_robotics_with_foundation_models_toward_embodied_ai/
date: '2024-02-04'
year: 2024
field: robotics
subfield: robot-foundation-models-vla
tasks:
- survey
- foundation-models
- datasets
- simulators
tier: 1
artifact_type: paper
venue: arXiv 2024
authors:
- Jiahang Xu
- Yunhan Huang
- Jiawei Gu
- Jiankai Sun
authors_short: Xu et al.
paperurl: https://arxiv.org/pdf/2402.02385.pdf
doi: 10.48550/arXiv.2402.02385
license: unspecified
summary: A 2024 survey that systematically maps how foundation models are deployed
  across the full robotics stack, covering perception, task planning, action generation,
  datasets, simulation platforms, and open challenges, with a detailed taxonomy of
  adaptation strategies from zero-shot prompting to full fine-tuning.
why_important: Provides the field's most comprehensive taxonomy of foundation model
  applications in robotics as of 2024, serving as an essential reference for researchers
  entering the embodied AI space and for understanding how disparate strands of work
  (VLAs, affordance models, world models) fit within a unified framework.
tags:
- survey
- foundation-models
- robotics
- embodied-ai
---

## Summary

The rapid transfer of large-scale pre-trained models from NLP and computer vision into robotics has generated a fragmented landscape of approaches with inconsistent terminology and unclear relationships between components. Xu et al. address this by providing a structured survey that organizes foundation model applications to robotics into a hierarchical taxonomy: perception (object recognition, pose estimation, scene understanding, embodied navigation); planning (task decomposition, code generation, common-sense reasoning, chain-of-thought prompting); and action (manipulation policies, locomotion controllers, safety-constrained control). Each category is reviewed with respect to the pre-training modality used (language, vision, vision-language), the adaptation method (zero-shot prompting, few-shot in-context learning, fine-tuning, LoRA), and the target robotic platform.

A substantial portion of the survey addresses the data and infrastructure layer that makes foundation model robotics tractable. The authors catalog existing datasets organized by embodiment type, annotation modality, and collection method, and survey simulation platforms—IsaacGym, MuJoCo, Habitat, AI2-THOR, Sapien—analyzing their physics fidelity, rendering quality, and suitability for foundation model pre-training and sim-to-real transfer. This infrastructure review is particularly valuable given that many primary papers assume familiarity with specific simulators or dataset formats, and the comparative treatment helps researchers select appropriate tools for their specific research questions.

The survey's third major contribution is its analysis of how foundation models enable cross-task and cross-embodiment generalization. The authors trace the progression from task-specific neural policies to multi-task transformers (RT-1), vision-language-action models (RT-2, PaLM-E), and cross-embodiment generalist policies (Octo, OpenVLA), analyzing at each step how the pre-training data distribution, model architecture, and fine-tuning strategy affect generalization. They identify emergent behaviors—capabilities not explicitly trained—as a distinctive property of sufficiently large models, and review evidence for and against emergence in the robotics domain specifically.

## Why It Matters

This survey arrives at a pivotal moment when the field is actively debating whether the large-model paradigm from NLP and computer vision will transfer fully to physical manipulation and navigation. By providing a comprehensive taxonomy and empirical synthesis, it enables researchers to navigate the rapidly expanding literature without reading hundreds of primary papers, and gives funding agencies, research groups, and practitioners a shared vocabulary for discussing the state of the field. Its infrastructure review is particularly valuable for newcomers, as the proliferation of simulators and dataset formats has created significant onboarding friction.

The survey also clarifies several open problems that define the field's research agenda: the robotics data bottleneck (even the largest robot datasets are orders of magnitude smaller than pre-training corpora), the sim-to-real transfer gap (no current simulator fully captures contact dynamics and visual diversity), and the action grounding challenge (mapping abstract language representations to precise motor commands without intermediate symbolic representations). By naming and situating these challenges within the broader foundation model framework, the survey helps the community identify where foundational scientific contributions are most needed versus where engineering execution is the primary obstacle.

| | |
|---|---|
| **Authors** | Xu et al. |
| **Year** | 2024 |
| **Venue** | arXiv 2024 |
| **Field** | Robotics |
| **Subfield** | Robot Foundation Models Vla |
| **Tasks** | survey, foundation-models, datasets, simulators |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2402.02385.pdf){: .btn .btn--primary .btn--large}
