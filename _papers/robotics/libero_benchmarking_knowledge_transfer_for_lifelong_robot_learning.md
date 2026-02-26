---
title: 'LIBERO: Benchmarking Knowledge Transfer for Lifelong Robot Learning'
collection: papers
permalink: /papers/robotics/libero_benchmarking_knowledge_transfer_for_lifelong_robot_learning/
date: '2023-05-24'
year: 2023
field: robotics
subfield: robot-learning-manipulation
tasks:
- lifelong-learning
- knowledge-transfer
- benchmark
- procedural-generation
tier: 2
artifact_type: paper
venue: NeurIPS 2023
authors:
- Bo Liu
- Yifeng Zhu
- Chongkai Gao
- Yihao Feng
authors_short: Liu et al.
paperurl: https://papers.neurips.cc/paper_files/paper/2023/file/8c3c666820ea055a77726d66fc7d447f-Paper-Datasets_and_Benchmarks.pdf
doi: ''
license: unspecified
summary: LIBERO introduces a procedurally generated benchmark suite of 130 manipulation
  tasks organized into four knowledge-transfer splits (spatial, object, goal, and
  long-horizon), enabling controlled study of catastrophic forgetting, forward transfer,
  and backward transfer in lifelong robot learning.
why_important: Provides the field's first purpose-built evaluation framework for lifelong
  manipulation learning, enabling researchers to disentangle types of knowledge transfer
  and measure how well policies retain prior skills while acquiring new ones.
tags:
- lifelong-learning
- benchmark
- manipulation
- knowledge-transfer
---

## Summary

LIBERO (Lifelong Learning Benchmark for Robot Environments), presented at NeurIPS 2023 as a datasets and benchmarks contribution, addresses a critical gap in robot learning evaluation: despite growing interest in continual and lifelong learning for manipulation, no standardized benchmark existed to systematically measure knowledge transfer across diverse task sequences. Liu et al. design four task suites—LIBERO-Spatial (same objects, different spatial arrangements), LIBERO-Object (same spatial layout, different objects), LIBERO-Goal (same objects and layout, different task goals), and LIBERO-Long (sequences of up to 8 sub-goals requiring long-horizon reasoning)—each containing 50 tasks with procedurally varied parameters. A total of 500 teleoperated demonstrations per task are provided, collected on a Franka Panda arm in a tabletop environment using a standardized simulation framework built on MuJoCo and Robosuite.

The benchmark's design philosophy centers on controlled factor variation: by changing only one dimension at a time across task sequences, LIBERO makes it possible to attribute changes in policy performance to specific types of knowledge transfer. The authors evaluate several continual learning approaches—sequential fine-tuning, elastic weight consolidation (EWC), PackNet, and progressive networks—alongside a multi-task upper bound, revealing that all existing methods suffer significant forgetting on LIBERO-Long while showing more modest drops on the simpler suites. These results quantify for the first time how the difficulty of knowledge retention scales with task sequence length and complexity, establishing a concrete measurement framework where previously only qualitative characterizations existed.

LIBERO also introduces standardized evaluation metrics based on the forward transfer ratio (FTR) and backward transfer ratio (BTR) that allow direct comparison across methods and papers. The authors provide a reproducible data collection pipeline, pretrained behavioral cloning and LSTM-GMM baselines, and an open-source codebase that integrates with standard robot learning frameworks. The simulation environment supports both image-based and state-based observation spaces, enabling comparison between vision-only policies relevant to real-world deployment and privileged-state policies useful for algorithmic development and debugging.

## Why It Matters

LIBERO fills a foundational role analogous to what ImageNet played for visual recognition: it provides a shared, reproducible benchmark that allows the lifelong robot learning community to measure progress with comparable baselines. Prior to LIBERO, continual learning for manipulation was evaluated on ad hoc task sequences chosen differently by each paper, making it impossible to determine whether improvements reflected genuine algorithmic progress or favorable task selection. By standardizing task suites and evaluation metrics, LIBERO creates the conditions for cumulative scientific progress in a subfield that was previously too fragmented to build on itself effectively.

The benchmark also reveals a clear empirical gap between what existing continual learning methods achieve and what a truly capable lifelong learning system would require. On LIBERO-Long, virtually all methods show dramatic catastrophic forgetting of early tasks—highlighting that architectural solutions developed in the continual learning literature (EWC, PackNet) do not transfer cleanly to the visuomotor manipulation domain. This motivates research into parameter-efficient fine-tuning, modular policy architectures, and episodic memory mechanisms that retain task-specific knowledge without interference. LIBERO's four-split design also provides natural subproblems for ablation studies in papers focused on cross-task generalization and foundation model fine-tuning, making it a versatile benchmark that extends beyond its original lifelong learning scope.

| | |
|---|---|
| **Authors** | Liu et al. |
| **Year** | 2023 |
| **Venue** | NeurIPS 2023 |
| **Field** | Robotics |
| **Subfield** | Robot Learning Manipulation |
| **Tasks** | lifelong-learning, knowledge-transfer, benchmark, procedural-generation |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://papers.neurips.cc/paper_files/paper/2023/file/8c3c666820ea055a77726d66fc7d447f-Paper-Datasets_and_Benchmarks.pdf){: .btn .btn--primary .btn--large}
