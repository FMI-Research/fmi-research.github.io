---
title: 'Embodied AI Data Engineering: A Survey'
collection: papers
permalink: /papers/embodied-ai/embodied_ai_data_engineering_a_survey/
date: '2025-06-01'
year: 2025
field: embodied-ai
subfield: embodied-agents-benchmarks-world-models
tasks:
- data-engineering
- teleoperation
- simulation
- data-management
tier: 3
artifact_type: paper
venue: arXiv 2025
authors:
- AIRS Research Team
authors_short: AIRS Research Team
paperurl: https://airs.cuhk.edu.cn/sites/default/files/2025-06/Survey_Arxiv.pdf
doi: ''
license: unspecified
summary: Comprehensive 2025 survey of the embodied AI data ecosystem — from teleoperation
  and simulation pipelines to human video and internet-scale pretraining — framing
  data standardization and cross-embodiment generalization as first-class research
  problems.
why_important: Addresses the data bottleneck widely seen as the primary barrier to
  scaling embodied AI, consolidating the emerging consensus around open datasets and
  providing a data curation framework that connects directly to Open X-Embodiment
  and VLA pretraining efforts.
tags:
- data-engineering
- embodied-ai
- teleoperation
- simulation
- data
---

## Summary

This 2025 survey from the AIRS Research Team at CUHK reframes the central challenge of scaling embodied AI away from algorithmic or computational bottlenecks and onto the **data bottleneck**: the systematic scarcity of high-quality, diverse, and action-labeled robot interaction data. Where LLM scaling benefited from essentially unlimited web text, embodied AI policies require demonstrations that are physically grounded, time-synchronized across modalities (vision, proprioception, force/torque), and collected at a cost — in hardware, operator time, and safety overhead — that is orders of magnitude higher than data collection in NLP or even computer vision. The survey maps four major data modalities in the embodied AI ecosystem: (1) **simulation-generated data** from physics engines (Isaac Sim, MuJoCo, Genesis, SAPIEN) enabling large-scale, automated trajectory collection; (2) **real-world robot demonstrations** collected via teleoperation systems ranging from ALOHA and UMI to commercial platforms like AgiBot; (3) **human video data** from egocentric and third-person datasets (EPIC-Kitchens, Ego4D, HOI4D, Something-Something) used for representation pretraining and reward signal extraction; and (4) **internet-scale general video** used as a pretraining substrate for vision-language-action models.

The survey's organizational strength lies in its multi-axis taxonomy of data collection pipelines. It distinguishes data sources along three orthogonal dimensions: *collection modality* (leader-follower teleoperation, kinesthetic teaching, autonomous rollout with corrective interventions, motion capture retargeting); *embodiment type* (fixed-arm tabletop manipulator, mobile manipulator, dexterous hand, humanoid); and *annotation richness* (raw video only, action-labeled with joint angles or end-effector poses, language-annotated with task descriptions, reward-labeled with success signals). Treating data standardization as a research problem — not an engineering detail — is a distinguishing feature of this survey. It covers the challenges of normalizing action spaces across robot morphologies (Cartesian vs. joint-space, absolute vs. delta actions), aligning observation formats across sensor configurations, and designing data quality filters that go beyond simple heuristics like trajectory length or task success rate.

The survey also provides a substantive treatment of **data scaling laws** as they apply to robot learning. It examines whether the power-law relationship between data volume and downstream performance observed in LLMs transfers to embodied policies, finding partial evidence in the Open X-Embodiment results but noting that *data diversity* — in terms of task, environment, and embodiment — often matters more than raw volume for generalization. Cross-embodiment generalization receives dedicated attention: the survey analyzes whether policies trained on multi-robot datasets transfer across morphologies and what data mixture strategies (weighting by embodiment type, task category, or environment appearance) best promote generalizable behavior. Generative data augmentation — using video diffusion models or NeRF-based scene generation to synthesize novel training scenarios — is treated as an emerging complement to physical collection rather than a substitute.

## Why It Matters

The data bottleneck is widely recognized as the primary barrier preventing embodied AI from following the same scaling trajectory as LLMs and image generation models. This survey consolidates the community's emerging consensus around **open data initiatives** — Open X-Embodiment (1M+ demonstrations across 22 robots), DROID (76k demonstrations with diverse tasks and environments), AgiBot World (over 1M trajectories from a 100-robot fleet), and Bridge Data — while providing the analytical framework needed to reason about what kinds of data, collected how, and mixed in what proportions, produce the most capable and generalizable policies. For research groups without large hardware fleets, the survey's analysis of sim-to-real data pipelines and human video pretraining provides actionable guidance: it maps the specific capabilities that transfer from non-robot data sources (visual representations, contact-rich priors, goal understanding) and the capabilities that do not (precise manipulation dynamics, proprioceptive integration, real-time reactive control).

The survey's descriptive breadth is also its principal limitation: it stops short of establishing empirical scaling laws or benchmarking competing collection strategies head-to-head. Key open questions it surfaces — what is the optimal real-to-simulated data ratio in training mixtures, how much does embodiment heterogeneity help or hurt policy specialization, whether synthetic demonstrations from video diffusion models can substitute for physical rollouts on contact-rich tasks — are live research problems as of mid-2025. These questions connect directly to frontier model efforts like π0 (which uses a heterogeneous multi-embodiment pretraining corpus), RDT-1B (which scales a diffusion policy to 1B parameters on curated real-robot data), and the broader VLA paradigm (which imports language model pretraining infrastructure into robot policy learning). Reading this survey alongside the Open X-Embodiment technical report and the π0 paper gives a complete picture of where the embodied AI data problem stands and the competing strategies the field is pursuing to solve it.

| | |
|---|---|
| **Authors** | AIRS Research Team |
| **Year** | 2025 |
| **Venue** | arXiv 2025 |
| **Field** | Embodied Ai |
| **Subfield** | Embodied Agents Benchmarks World Models |
| **Tasks** | data-engineering, teleoperation, simulation, data-management |
| **Tier** | 3 — Benchmark / Auxiliary |
| **License** | unspecified |

[View / Download PDF](https://airs.cuhk.edu.cn/sites/default/files/2025-06/Survey_Arxiv.pdf){: .btn .btn--primary .btn--large}
