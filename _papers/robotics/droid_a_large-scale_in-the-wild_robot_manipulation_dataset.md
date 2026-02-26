---
title: 'DROID: A Large-Scale In-The-Wild Robot Manipulation Dataset'
collection: papers
permalink: /papers/robotics/droid_a_large-scale_in-the-wild_robot_manipulation_dataset/
date: '2024-03-20'
year: 2024
field: robotics
subfield: robot-learning-manipulation
tasks:
- dataset
- in-the-wild
- real-world
- diversity
tier: 2
artifact_type: paper
venue: arXiv / RSS 2024
authors:
- Alexander Khazatsky
- Karl Pertsch
- Suraj Nair
- Ashwin Balakrishna
authors_short: Khazatsky et al.
paperurl: https://arxiv.org/pdf/2403.12945.pdf
doi: 10.48550/arXiv.2403.12945
license: unspecified
summary: DROID presents 76,000 robot manipulation trajectories collected by 50 operators
  across 86 distinct unscripted environments, demonstrating that environmental and
  operator diversity at collection time translates to measurably improved policy generalization.
why_important: Represents the most diversity-focused large-scale robot dataset prior
  to cross-embodiment aggregations, establishing that in-the-wild uncontrolled collection
  produces training data with qualitatively different and more generalizable properties
  than lab-controlled datasets.
tags:
- dataset
- in-the-wild
- manipulation
- real-world
- diversity
---

## Summary

DROID (Distributed Robot Interaction Dataset), presented at RSS 2024, takes an explicit stance that the diversity of data collection settings is as important as raw volume when building generalizable robot manipulation policies. Khazatsky et al. organize a large-scale data collection campaign in which 50 different human operators collect demonstrations across a variety of unscripted real-world environments—offices, kitchens, garages, and conference rooms—using a standardized Franka Emika Panda arm equipped with a parallel-jaw gripper. The resulting dataset contains approximately 76,000 trajectories across 86 distinct environments, covering a broad set of everyday manipulation tasks annotated with natural language descriptions. Two synchronized cameras—a third-person view and a wrist-mounted fisheye camera—are used throughout, providing richer spatial context than single-view setups.

The paper's core claim is that in-the-wild diversity, achieved by not constraining the collection environment, produces a qualitatively different data distribution than controlled lab datasets. To test this, the authors train policies on DROID alone, on BridgeData V2 alone, and on combinations, evaluating on held-out novel environments. DROID-trained policies demonstrate substantially better zero-shot generalization to visually novel settings, attributed to greater visual background diversity, lighting variation, and object clutter present in DROID's uncontrolled settings. Fine-tuning on small amounts of data from the evaluation environment further closes the gap, confirming that diverse pre-training data provides a strong prior that adapts efficiently to specific deployment contexts.

The logistical infrastructure developed for DROID is itself a contribution: the authors describe a decentralized data collection protocol in which operators at different institutions use a standardized hardware kit and software stack (built on the RLDS data format) to contribute to a shared repository. This protocol—combining reproducible hardware with minimal constraints on the collection environment—represents a middle path between fully standardized single-lab data (more controlled, less diverse) and fully heterogeneous crowd-sourced data (more diverse, harder to quality-control). The paper also studies the effect of operator diversity, finding that trajectories from multiple operators with different movement styles improve the robustness of downstream policies.

## Why It Matters

DROID demonstrates that the source environment of demonstrations matters as much as their number—a lesson with significant practical implications for data collection strategy. Policies trained on DROID show meaningfully better generalization to deployment environments they have never seen, suggesting that in-the-wild collection is not merely more convenient but produces fundamentally more useful training data. This finding reinforces the field's trajectory toward distributed, crowd-sourced data collection models rather than centralized, controlled recording setups.

The dataset also reveals important gaps in current policy architectures. Even with diverse training data, DROID-trained policies struggle with tasks requiring precise force regulation, long-horizon planning, and tasks involving deformable objects. These failure modes suggest data diversity alone cannot compensate for architectural limitations, pointing toward future work on hybrid sensing, hierarchical planning, and physics-informed policy representations. DROID's public release—and its compatibility with Open X-Embodiment's data format—makes it a natural component in mixture-of-datasets training regimes for next-generation generalist policies.

| | |
|---|---|
| **Authors** | Khazatsky et al. |
| **Year** | 2024 |
| **Venue** | arXiv / RSS 2024 |
| **Field** | Robotics |
| **Subfield** | Robot Learning Manipulation |
| **Tasks** | dataset, in-the-wild, real-world, diversity |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2403.12945.pdf){: .btn .btn--primary .btn--large}
