---
title: 'Open X-Embodiment: Robotic Learning Datasets and RT-X Models'
collection: papers
permalink: /papers/robotics/open_x-embodiment_robotic_learning_datasets_and_rt-x_models/
date: '2023-10-13'
year: 2023
field: robotics
subfield: robot-foundation-models-vla
tasks:
- cross-embodiment
- dataset
- generalist-policy
- scaling
tier: 2
artifact_type: paper
venue: arXiv / CoRL 2023
authors:
- Abhishek Padalkar
- Acorn Pooley
- Ajinkya Jain
- Alex Bewley
authors_short: Padalkar et al.
paperurl: https://arxiv.org/pdf/2310.08864.pdf
doi: 10.48550/arXiv.2310.08864
license: unspecified
summary: Open X-Embodiment aggregates over 1 million robot trajectories from 22 different
  robot types across more than 30 institutions into a unified dataset and demonstrates
  that generalist RT-X policies trained on this cross-embodiment data outperform specialist
  policies trained on single-robot datasets.
why_important: Represents the largest cross-embodiment robot learning dataset effort
  to date, establishing cross-embodiment aggregation as a viable path to generalist
  manipulation and providing the pre-training corpus used by subsequent foundation
  model policies including Octo and OpenVLA.
tags:
- cross-embodiment
- dataset
- generalist-policy
- scaling
- robotics
---

## Summary

Open X-Embodiment (OXE), presented at CoRL 2023, takes inspiration from ImageNet's role in computer vision: just as aggregating diverse images enabled visual representations that transfer broadly, aggregating diverse robot trajectories across embodiments might produce policy representations with similarly broad generalization. Padalkar et al. coordinate a large-scale data collection and standardization effort involving over 30 academic and industrial institutions, resulting in a dataset spanning 22 robot embodiments—from mobile manipulation platforms to tabletop arms to bi-manual systems—covering 527 manipulation skills and over 1 million trajectories. All data is converted to a unified RLDS format with standardized observation and action schemas, with per-dataset adapters handling the heterogeneity in camera configurations, action spaces, and control frequencies.

The paper's central experimental finding is that RT-X models—RT-1 and RT-2 fine-tuned on the OXE mixture—show improved performance on held-out tasks compared to their single-embodiment counterparts. Specifically, RT-1-X achieves a 50% relative improvement in generalization performance on tasks from embodiments with limited training data, attributable to positive transfer from other embodiments with more abundant coverage. RT-2-X shows emergent generalization to new embodiment-task combinations not present in either the web pre-training data or the OXE mixture, suggesting cross-embodiment data enables a form of compositional generalization in VLA models. The paper also studies dataset mixture weights, finding that naive uniform mixing underperforms carefully tuned mixtures accounting for dataset size and task diversity imbalance.

The data standardization methodology is a substantial technical contribution. The authors define a unified observation schema (language instruction, camera images, robot state) and action schema (end-effector Cartesian deltas or joint deltas, gripper command) accommodating heterogeneous raw data formats from participating institutions. Dataset-specific RLDS conversion scripts are open-sourced, enabling new institutions to contribute data in a compatible format. The paper characterizes the dataset quantitatively with per-embodiment trajectory counts, task coverage statistics, and visual diversity metrics, providing transparency about dataset composition that is often missing from large-scale data papers.

## Why It Matters

Open X-Embodiment transformed the robot learning landscape by demonstrating that cross-embodiment data aggregation is both tractable and beneficial—two properties that were genuinely uncertain before this work. The result that a generalist policy trained across 22 robot types outperforms specialists trained on individual robots challenges the intuition that embodiment-specific training is necessary and sufficient, suggesting that manipulation skills share transferable structure across embodiments that a sufficiently expressive model can discover.

The OXE dataset immediately became the foundational pre-training corpus for subsequent generalist policies, including Octo (trained on an 800k-trajectory subset) and OpenVLA (trained on a 970k-trajectory subset), establishing it as the ImageNet of robot manipulation. However, the dataset also reveals the limits of current scaling: despite aggregating 22 embodiments, the data is dominated by tabletop arm manipulation and lacks meaningful coverage of humanoid or legged manipulation platforms. Contact-rich tasks remain underrepresented, and the evaluation methodology primarily measures success on seen task-embodiment pairs rather than generalization to truly novel settings. These gaps define the frontier along which the next generation of cross-embodiment datasets are being developed.

| | |
|---|---|
| **Authors** | Padalkar et al. |
| **Year** | 2023 |
| **Venue** | arXiv / CoRL 2023 |
| **Field** | Robotics |
| **Subfield** | Robot Foundation Models Vla |
| **Tasks** | cross-embodiment, dataset, generalist-policy, scaling |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2310.08864.pdf){: .btn .btn--primary .btn--large}
