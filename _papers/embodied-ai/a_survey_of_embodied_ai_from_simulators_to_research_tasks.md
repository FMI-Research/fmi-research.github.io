---
title: 'A Survey of Embodied AI: From Simulators to Research Tasks'
collection: papers
permalink: /papers/embodied-ai/a_survey_of_embodied_ai_from_simulators_to_research_tasks/
date: '2021-03-08'
year: 2021
field: embodied-ai
subfield: embodied-agents-benchmarks-world-models
tasks:
- survey
- simulators
- task-taxonomy
- navigation
- interaction
tier: 1
artifact_type: paper
venue: IEEE TNNLS / arXiv 2021
authors:
- Jiajun Duan
- Samson Yu
- Hui Li Tan
- Hongyuan Zhen
authors_short: Duan et al.
paperurl: https://arxiv.org/pdf/2103.04918.pdf
doi: 10.48550/arXiv.2103.04918
license: unspecified
summary: Comprehensive early survey organizing embodied AI simulators and tasks (navigation,
  manipulation, EmbodiedQA, social interaction) into a taxonomic framework, and identifying
  sim-to-real transfer as the field's central challenge.
why_important: Established the shared vocabulary and benchmark taxonomy that structured
  embodied AI research through the early 2020s, making it the canonical historical
  reference for the field's simulator and task landscape.
tags:
- survey
- embodied-ai
- simulators
- benchmarks
- navigation
---

## Summary

Published in 2021 and later expanded for IEEE TPAMI, this survey stands as one of the first comprehensive attempts to map the embodied AI landscape at a moment when the field was coalescing around interactive simulation as the primary research medium. The paper's central claim — that intelligence must be grounded in physical or simulated interaction with an environment, not passive observation of static datasets — was still contested at the time, and the survey builds a systematic case for this "embodied hypothesis" by reviewing both the theoretical motivation and the practical infrastructure (simulators, benchmarks, evaluation protocols) that makes it testable. It covers a remarkably broad scope: photorealistic and physics-accurate simulators (AI2-THOR, Gibson, Habitat, iGibson, VirtualHome, ThreeDWorld), organized along axes of visual realism, physics fidelity, semantic richness, and degree of object interactivity.

The survey's most durable contribution is its four-family task taxonomy: **visual navigation** (point-goal, object-goal, vision-language navigation), **object interaction and manipulation** (rearrangement, pick-and-place, articulated object manipulation), **embodied question answering** (EmbodiedQA, multi-hop visual reasoning), and **multi-agent and social interaction** (collaborative navigation, human-robot dialogue). For each family, the authors trace dataset lineages, evaluation metrics, and the state of the art as of early 2021. The taxonomy draws a sharp and principled distinction between passive perception — the dominant paradigm of ImageNet-era computer vision — and *active*, interactive perception, where the agent's choice of viewpoint and action changes the information it receives. This distinction proved influential in framing subsequent benchmark design.

Structurally, the survey introduces a multi-axis comparison matrix for simulators that became a standard reference format for groups designing new environments. It also identifies **sim-to-real transfer** — the systematic performance gap when policies trained in simulation are deployed on physical hardware — as the field's central unresolved challenge, and discusses early mitigation strategies including domain randomization, photorealistic rendering, and physics calibration. The framing of embodied AI as the convergence of vision, language, and physical action anticipated the trajectory the field followed through 2022–2024.

## Why It Matters

Published at the pivot point between ImageNet-era computer vision and the era of interactive embodied agents, this survey gave the research community a shared vocabulary, a taxonomic anchor, and a simulator comparison framework that proved durable well beyond its publication date. Its four-task taxonomy and simulator matrix were widely adopted — and explicitly extended — by subsequent surveys and benchmark papers (e.g., Savva et al.'s Habitat series, the ALFRED benchmark, EAI workshop proceedings). For any researcher entering the embodied AI field, it remains the canonical starting point for understanding *why* simulation matters, *how* environments differ, and *what* the canonical task formulations look like before the large language model era reshaped them.

By 2025, the survey's coverage shows its age in specific ways that are themselves informative. Its treatment of language-conditioned policies predates LLM backbones and does not address in-context learning for navigation, chain-of-thought task decomposition, or vision-language-action models. The simulator landscape has also shifted substantially — Isaac Sim, Genesis, ManiSkill3, and RoboVerse have introduced new fidelity and scalability tradeoffs not covered here. These gaps are not flaws so much as a precise record of where the field stood in early 2021, and reading this survey against current frontier work is itself an illuminating exercise in how rapidly the embodied AI stack has been rebuilt atop foundation model primitives.

| | |
|---|---|
| **Authors** | Duan et al. |
| **Year** | 2021 |
| **Venue** | IEEE TNNLS / arXiv 2021 |
| **Field** | Embodied Ai |
| **Subfield** | Embodied Agents Benchmarks World Models |
| **Tasks** | survey, simulators, task-taxonomy, navigation, interaction |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2103.04918.pdf){: .btn .btn--primary .btn--large}
