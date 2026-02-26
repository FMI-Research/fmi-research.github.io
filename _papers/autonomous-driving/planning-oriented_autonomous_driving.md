---
title: Planning-Oriented Autonomous Driving
collection: papers
permalink: /papers/autonomous-driving/planning-oriented_autonomous_driving/
date: '2022-12-19'
year: 2022
field: autonomous-driving
subfield: end-to-end-autonomous-driving
tasks:
- end-to-end-driving
- unified-architecture
- planning
tier: 1
artifact_type: paper
venue: CVPR 2023 (Best Paper)
authors:
- Yihan Hu
- Jiazhi Yang
- Li Chen
- Keyu Li
- Chonghao Sima
- Xizhou Zhu
- Siqi Chai
- Senyao Du
- Tianwei Lin
- Wenhai Wang
- Lewei Lu
- Xiaosong Jia
- Qiang Liu
- Jifeng Dai
- Yu Qiao
- Hongyang Li
authors_short: Hu et al.
paperurl: https://arxiv.org/pdf/2212.10156.pdf
doi: 10.48550/arXiv.2212.10156
license: unspecified
summary: Proposes UniAD, a planning-oriented unified transformer that jointly optimizes
  tracking, online mapping, motion forecasting, occupancy prediction, and ego planning
  via task-aligned BEV queries, achieving state-of-the-art nuScenes planning metrics
  by treating all perception sub-tasks as instrumental to the final planning objective.
why_important: As the CVPR 2023 Best Paper, UniAD established joint planning-oriented
  optimization of all AD sub-tasks as the dominant E2E paradigm, directly inspiring
  VAD, SparseDrive, and the broader class of query-based unified driving models.
tags:
- end-to-end
- autonomous-driving
- unified-model
- planning
- transformer
---

## Summary

UniAD addresses a fundamental fragmentation problem in autonomous driving: prior work either optimized individual sub-tasks (tracking, mapping, prediction) in isolation or concatenated independently trained modules without a unifying objective. The authors propose a planning-oriented architecture composed of five sequential transformer-based modules — BEV encoder, TrackFormer, MapFormer, MotionFormer, OccFormer, and finally a planner — each interacting through shared bird's-eye-view (BEV) feature representations. A defining design principle is that every intermediate module is optimized not merely to maximize its own accuracy but to benefit downstream planning. Task-aligned queries propagate structured information through the hierarchy: track queries represent individual agents, map queries represent lane elements, and motion queries aggregate agent dynamics, all ultimately conditioning the ego-trajectory planner. The entire system is trained end-to-end from multi-camera surround video with a multi-task loss whose gradients flow back through all stages.

UniAD is evaluated on the nuScenes benchmark, which at the time of publication was the primary metric for camera-based E2E driving in the open-loop regime. It achieves a mean L2 displacement error of 0.48 m at 2 s horizon and a collision rate of 0.08% on the nuScenes val split — a reduction of over 40% in collision rate relative to the best prior modular methods. On tracking (AMOTA), map segmentation (IoU), and motion forecasting (minADE), UniAD also sets state-of-the-art or near-state-of-the-art results, demonstrating that the joint training objective does not harm individual task performance. The model uses ResNet-101 and DETR-style BEV perception; runtime is roughly 0.5 fps on a single GPU, reflecting its research rather than deployment focus.

The central methodological innovation is the framing of all sub-tasks as instrumental to planning — a paradigm shift from the common practice of cascading independently trained modules. MotionFormer introduces an agent-scene interaction mechanism where queries for individual agents attend to map queries, producing socially and spatially aware motion predictions. OccFormer aggregates motion predictions into a forward-projected occupancy field that allows the planner to reason about future free space. This cascade of structured representations replaces the need for hand-crafted intermediate losses or post-hoc integration, and demonstrates that gradient signal from a downstream planning objective meaningfully regularizes upstream intermediate tasks, establishing a blueprint for subsequent unified driving models.

## Why It Matters

UniAD's receipt of the CVPR 2023 Best Paper award marked a symbolic inflection point in autonomous driving research, signaling broad community recognition that end-to-end, planning-oriented architectures represent a more principled path than modular pipelines. Its formulation — shared BEV representation, task-aligned queries, and planning as the top-level objective — became an immediate template for follow-on work. VAD (ICCV 2023) adopted the planning-oriented spirit while replacing dense BEV grids with vectorized representations. SparseDrive extended the query-based paradigm to sparse instance representations for further efficiency gains. DriveVLM and Senna both cited UniAD's multi-task formulation as their baseline for low-level trajectory output. The codebase was open-sourced on GitHub and became a widely used comparison point in nuScenes leaderboard submissions through 2024.

UniAD's principal limitations are its computational cost — at roughly 0.5 fps, it is far from real-time deployable — and its reliance on camera-only input, which foregoes the richer geometric information provided by LiDAR. Open-loop evaluation on nuScenes measures imitation accuracy rather than actual driving safety, a limitation that motivated subsequent benchmark efforts such as NAVSIM and nuPlan. The architecture also assumes fixed scene element cardinality and does not handle partial observability or long-tail scenarios robustly. These gaps spurred a lineage of improvements: SparseDrive achieved 2× faster inference by discarding dense BEV features; DriveVLM supplemented trajectory planning with language-based scene reasoning; and NAVSIM introduced richer evaluation to replace the L2/collision metrics that UniAD optimized against.

| | |
|---|---|
| **Authors** | Hu et al. |
| **Year** | 2022 |
| **Venue** | CVPR 2023 (Best Paper) |
| **Field** | Autonomous Driving |
| **Subfield** | End To End Autonomous Driving |
| **Tasks** | end-to-end-driving, unified-architecture, planning |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2212.10156.pdf){: .btn .btn--primary .btn--large}
