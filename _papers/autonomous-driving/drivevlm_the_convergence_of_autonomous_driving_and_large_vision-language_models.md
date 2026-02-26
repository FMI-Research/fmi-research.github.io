---
title: 'DriveVLM: The Convergence of Autonomous Driving and Large Vision-Language
  Models'
collection: papers
permalink: /papers/autonomous-driving/drivevlm_the_convergence_of_autonomous_driving_and_large_vision-language_models/
date: '2024-02-19'
year: 2024
field: autonomous-driving
subfield: llm-vla-autonomous-driving
tasks:
- vla-driving
- chain-of-thought
- scene-understanding
- planning
tier: 1
artifact_type: paper
venue: CoRL 2024
authors:
- Xiaoyu Tian
- Junru Gu
- Bailin Li
- Yicheng Liu
- Yang Wang
- Zhiyong Zhao
- Kun Zhan
- Peng Jia
- Xianpeng Lang
- Hang Zhao
authors_short: Tian et al.
paperurl: https://arxiv.org/pdf/2402.12289.pdf
doi: 10.48550/arXiv.2402.12289
license: unspecified
summary: DriveVLM integrates Qwen-VL into autonomous driving via a three-stage chain-of-thought
  pipeline — scene description, scene analysis, and hierarchical trajectory planning
  — and introduces DriveVLM-Dual, which runs VLM reasoning asynchronously alongside
  a conventional modular planner to overcome the 2–3 second VLM inference latency.
why_important: DriveVLM established the dual-system VLM+conventional-planner architecture
  as a practical solution to the latency-capability trade-off in language-guided driving,
  influencing subsequent systems including Senna and Agent-Driver that adopted analogous
  two-tier asynchronous designs.
tags:
- vla
- autonomous-driving
- chain-of-thought
- vlm
- planning
---

## Summary

DriveVLM integrates Qwen-VL, a large vision-language model, into the autonomous driving planning loop via a structured chain-of-thought (CoT) reasoning pipeline consisting of three sequential stages: *Scene Description*, where the VLM generates a natural language description of the current driving environment from multi-camera images (agents, road conditions, traffic signs, weather); *Scene Analysis*, where it reasons about scene semantics relevant to ego decisions (e.g., pedestrian intent, right-of-way determination, merge conflicts); and *Hierarchical Planning*, where the VLM first selects high-level driving intentions (e.g., "change lane left," "decelerate for crossing pedestrian") and then decodes them into a coarse trajectory waypoint sequence. The full DriveVLM system achieves strong performance on complex scenarios but suffers 2–3 seconds of inference latency due to VLM autoregressive generation, which is incompatible with real-time operation. DriveVLM-Dual addresses this by running the VLM asynchronously at a slow cadence (∼1 Hz) while a conventional modular planner provides high-frequency (∼10 Hz) trajectory updates, with VLM outputs serving as soft constraints on the conventional planner's objective function.

DriveVLM is evaluated on two settings: the nuScenes open-loop benchmark and a large in-house dataset collected under diverse Chinese urban traffic conditions. On nuScenes, DriveVLM-Dual achieves 0.40 m L2 at 2 s (surpassing UniAD's 0.48 m) and 0.06% collision rate. On the in-house dataset, which includes night driving, rain, construction zones, and unusual traffic scenarios, DriveVLM demonstrates significant qualitative advantages over purely modular systems — correctly handling unprotected left turns, pedestrian jaywalking, and vehicles running red lights where rule-based planners fail silently. Ablation studies show that removing the Scene Analysis stage (jumping directly from description to planning) degrades planning quality by 18% on complex scenario subsets, confirming that intermediate semantic reasoning is load-bearing rather than decorative.

DriveVLM's primary architectural innovation is the formalization of hierarchical VLM-based planning: by decomposing "what trajectory should the ego take?" into natural language scene understanding, semantic decision selection, and geometric waypoint generation, it creates a modular reasoning scaffold substantially more interpretable than direct image-to-waypoint mapping. The dual-system design assigns temporal responsibilities by frequency — VLM at semantic update rate, conventional planner at control rate — and uses a soft-constraint interface (VLM-generated trajectory envelopes) to communicate between the two without requiring full VLM retraining. The authors also introduce VLM-specific training augmentations for driving, including scene description generation from nuScenes annotations and multi-scenario instruction tuning that specializes Qwen-VL's outputs toward driving-relevant semantic categories.

## Why It Matters

DriveVLM's dual-system architecture resolved a practical impasse that had blocked VLM adoption in driving: the observation that VLMs reason richly but too slowly for 10+ Hz vehicle control. Its CoRL 2024 publication gave the community a concrete design pattern — asynchronous VLM reasoning coupled with synchronous conventional planning — that has since been adopted in Senna (intent + trajectory), Agent-Driver (reflective reasoning + IDM execution), and DiMA (asynchronous language planning modules). The chain-of-thought formulation reinforced the case made by DriveLM that structured language reasoning improves driving interpretability, and DriveVLM-Dual's quantitative improvements over UniAD on nuScenes provided strong evidence that VLM integration adds measurable planning value beyond interpretability alone.

DriveVLM's evaluation relies on a mix of public (nuScenes) and proprietary in-house data, limiting full reproducibility and independent comparison. The fine-tuning dataset for driving-specific instruction tuning is not publicly released, creating a reproducibility gap that affects the research community's ability to build directly on the work. The soft-constraint interface between VLM and conventional planner is heuristic — the weight assigned to VLM-generated trajectory envelopes relative to the conventional planner's cost function is manually tuned and may not generalize across diverse environments. The system still operates in an open-loop evaluation setting for nuScenes, and the in-house closed-loop results are reported without standardized metrics, complicating comparison with NAVSIM or nuPlan leaderboards. The 2–3 second VLM latency — while mitigated by the dual-system design — remains a fundamental bottleneck for scenarios requiring rapid semantic re-evaluation, such as sudden pedestrian emergence or unexpected signal changes.

| | |
|---|---|
| **Authors** | Tian et al. |
| **Year** | 2024 |
| **Venue** | CoRL 2024 |
| **Field** | Autonomous Driving |
| **Subfield** | Llm Vla Autonomous Driving |
| **Tasks** | vla-driving, chain-of-thought, scene-understanding, planning |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2402.12289.pdf){: .btn .btn--primary .btn--large}
