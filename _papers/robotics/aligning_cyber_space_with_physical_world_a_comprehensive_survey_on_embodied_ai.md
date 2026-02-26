---
title: 'Aligning Cyber Space with Physical World: A Comprehensive Survey on Embodied
  AI'
collection: papers
permalink: /papers/robotics/aligning_cyber_space_with_physical_world_a_comprehensive_survey_on_embodied_ai/
date: '2024-07-09'
year: 2024
field: robotics
subfield: robot-foundation-models-vla
tasks:
- survey
- embodied-ai
- simulators
- sim2real
- perception
tier: 3
artifact_type: paper
venue: arXiv 2024
authors:
- Yang Liu
- Weixing Chen
- Yongjie Bai
- Guanbin Li
authors_short: Liu et al.
paperurl: https://arxiv.org/pdf/2407.06886.pdf
doi: 10.48550/arXiv.2407.06886
license: unspecified
summary: A comprehensive 2024 survey mapping the embodied AI landscape across physical
  platforms (robots, autonomous vehicles, drones), simulation environments, perception
  and interaction systems, and foundation model integration, with emphasis on the
  alignment challenge between digital knowledge representations and physical world
  constraints.
why_important: Provides the broadest cross-disciplinary perspective on embodied AI
  as of 2024, connecting robotics, computer vision, NLP, and cognitive science communities
  through a shared framework, and identifying sim-to-real transfer and physical grounding
  as the defining challenges for the field's next development phase.
tags:
- survey
- embodied-ai
- simulators
- sim2real
- robotics
---

## Summary

Liu et al. organize a comprehensive survey of embodied AI that extends beyond robot manipulation to encompass the full range of agents that sense and act in physical environments: manipulation robots, mobile robots, humanoids, autonomous vehicles, and UAVs. The survey's central organizing thesis—captured in its title "Aligning Cyber Space with Physical World"—is that the field's core challenge is bridging the gap between the rich symbolic and semantic knowledge encoded in large pre-trained models and the continuous, noisy, contact-rich physical world in which deployed systems must act. This framing positions embodied AI as an alignment problem: how to ground digital knowledge in physical action constraints, sensorimotor contingencies, and real-world dynamics that no amount of text or image data can fully capture.

The survey covers four interconnected research areas. First, it reviews embodied perception—object detection, 3D scene understanding, embodied question answering, and active exploration—analyzing how physical co-location of sensing and action enables perception strategies unavailable to passive observers. The treatment of embodied QA and visual navigation benchmarks (EQA, R2R, REVERIE) is particularly detailed, situating these tasks as natural evaluation environments for embodied reasoning. Second, the survey catalogs embodied interaction methods, covering language-directed manipulation, human-robot collaboration, and social navigation, with attention to how context-dependent human instructions complicate grounding compared to template-based task specifications. The simulation infrastructure section reviews over 20 platforms across photo-realistic rendering (Habitat-Matterport, iGibson), physics fidelity (MuJoCo, Isaac), and interactive scene generation (AI2-THOR, ThreeDWorld), providing a comparative treatment that helps researchers select appropriate simulators.

The survey's final section examines foundation model integration, tracing the progression from task-specific neural policies to multi-task transformers, VLAs, and world models that can simulate physical dynamics for model-based planning. The authors identify three integration strategies: use of LLMs as high-level planners (SayCan paradigm), joint fine-tuning of VLMs as visuomotor controllers (RT-2 paradigm), and pre-training on large-scale video data to acquire world model priors. Each strategy is analyzed for its data requirements, computational cost, and generalization potential, providing a comparative framework that complements the more architecture-focused taxonomies in the VLA and foundation model surveys.

## Why It Matters

This survey serves a unique bridging function in the rapidly expanding embodied AI literature: it provides a single reference that connects robotics, computer vision, NLP, and cognitive science communities that often publish in separate venues and cite different literatures. For researchers from any one of these communities, it provides an accessible on-ramp to the others and situates their specific focus within the broader embodied intelligence agenda. Its breadth is also its differentiator relative to more focused surveys (e.g., the VLA survey by Ma et al. or the robotics foundation model survey by Xu et al.), making it particularly useful as an introduction for graduate students entering the field.

The survey's emphasis on the digital-physical alignment challenge also identifies what may be the field's most fundamental open problem: the current generation of foundation models encode rich world knowledge derived from text and images, but this knowledge is not automatically grounded in the continuous sensorimotor experience that characterizes physical agency. Bridging this gap requires either massive amounts of physical interaction data (motivating DROID and Open X-Embodiment), improved simulation that captures physical reality with sufficient fidelity for sim-to-real transfer, or architectural innovations that can extract embodiment-relevant structure from non-embodied pre-training signals. The survey's comprehensive coverage makes it an essential reference for research proposals and course syllabi seeking to situate specific contributions within this broader challenge.

| | |
|---|---|
| **Authors** | Liu et al. |
| **Year** | 2024 |
| **Venue** | arXiv 2024 |
| **Field** | Robotics |
| **Subfield** | Robot Foundation Models Vla |
| **Tasks** | survey, embodied-ai, simulators, sim2real, perception |
| **Tier** | 3 — Benchmark / Auxiliary |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2407.06886.pdf){: .btn .btn--primary .btn--large}
