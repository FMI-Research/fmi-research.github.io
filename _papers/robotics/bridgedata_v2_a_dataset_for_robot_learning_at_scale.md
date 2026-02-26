---
title: 'BridgeData V2: A Dataset for Robot Learning at Scale'
collection: papers
permalink: /papers/robotics/bridgedata_v2_a_dataset_for_robot_learning_at_scale/
date: '2023-08-14'
year: 2023
field: robotics
subfield: robot-learning-manipulation
tasks:
- dataset
- cross-environment
- generalization
- scaling
tier: 2
artifact_type: paper
venue: CoRL 2023 / PMLR
authors:
- Homer Walke
- Kevin Black
- Abraham Lee
- Moo Jin Kim
authors_short: Walke et al.
paperurl: https://proceedings.mlr.press/v229/walke23a/walke23a.pdf
doi: ''
license: unspecified
summary: BridgeData V2 releases roughly 60,000 demonstrations across 24 environments
  and 13 institutions, demonstrating that cross-environment diversity in robot learning
  datasets substantially improves generalization compared to depth-only collection
  within a single lab.
why_important: Provided one of the largest openly available robot manipulation datasets
  and established the multi-institution data sharing model that directly influenced
  Open X-Embodiment, making it an essential resource for cross-environment generalization
  research.
tags:
- dataset
- robot-learning
- manipulation
- cross-environment
---

## Summary

BridgeData V2, presented at CoRL 2023, addresses a fundamental bottleneck in robot learning: the scarcity of diverse demonstration data covering the variability of real-world deployment environments. Walke et al. present a dataset of approximately 60,000 demonstrations collected across 24 distinct environments—primarily kitchen and tabletop settings—spanning 13 institutions using a standardized WidowX 250s robot arm and a shared data collection protocol. The data covers over 70 unique manipulation skills including object picking, stacking, placing into containers, pushing, and tool use, with natural language annotations for all trajectories. A key design decision was to deliberately vary background, lighting, object appearance, and scene layout across environments rather than optimizing within a single controlled lab setting.

The paper's central experimental question is how cross-environment diversity affects downstream policy performance. The authors train behavioral cloning and goal-conditioned policies on varying subsets of the dataset, comparing models trained on data from single environments versus multi-environment mixtures. Their findings consistently show that multi-environment training improves generalization to held-out environments—even when total demonstration count is held constant—supporting the hypothesis that visual and task diversity provides a regularization effect that prevents policies from overfitting to lab-specific visual features. Data collected in one lab can directly improve performance on tasks evaluated at another institution using the same robot platform, validating the case for open data sharing.

On the technical side, BridgeData V2 standardizes data collection infrastructure through a reproducible teleoperation setup using SpaceMouse controllers and a fixed camera configuration (third-person and wrist cameras). The dataset is publicly released with a well-documented API, enabling researchers to train and evaluate policies on a shared benchmark. The paper evaluates three policy classes—BC, GCBC, and RT-2—on the dataset, providing baselines that serve as reference points for subsequent work. Notably, it also studies how RT-2, trained on web data, can be fine-tuned on BridgeData V2 to inherit benefits from both data distributions, anticipating the co-training methodology that would dominate subsequent VLA work.

## Why It Matters

BridgeData V2 played a pivotal role in the scaling-up of robot learning by demonstrating that open, multi-institution data sharing is both technically feasible and empirically beneficial. Its release catalyzed a broader movement toward collaborative data collection that culminated in Open X-Embodiment, which aggregates 22 robot types from dozens of institutions using a data format directly compatible with BridgeData V2's conventions. The dataset became the de facto standard for evaluating cross-environment generalization of manipulation policies, and its teleoperation infrastructure served as a template for DROID's in-the-wild collection protocol.

The paper also raises important unresolved questions. Despite the benefits of diversity, the dataset's 60k trajectories remain orders of magnitude smaller than vision-language pre-training corpora, raising the question of how much robot data is ultimately needed for effective foundation model fine-tuning. The strong improvement from multi-environment training also suggests that marginal value of additional demonstrations within a single environment diminishes quickly, which has practical implications for how labs should allocate collection budgets. These observations about data curation and distribution—rather than sheer volume—have continued to shape how the community designs and combines datasets for foundation model pre-training.

| | |
|---|---|
| **Authors** | Walke et al. |
| **Year** | 2023 |
| **Venue** | CoRL 2023 / PMLR |
| **Field** | Robotics |
| **Subfield** | Robot Learning Manipulation |
| **Tasks** | dataset, cross-environment, generalization, scaling |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://proceedings.mlr.press/v229/walke23a/walke23a.pdf){: .btn .btn--primary .btn--large}
