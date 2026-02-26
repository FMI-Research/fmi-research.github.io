---
title: 'DriveLM: Driving with Graph Visual Question Answering'
collection: papers
permalink: /papers/autonomous-driving/drivelm_driving_with_graph_visual_question_answering/
date: '2023-12-21'
year: 2023
field: autonomous-driving
subfield: llm-vla-autonomous-driving
tasks:
- visual-qa
- language-driving
- graph-reasoning
- planning
tier: 2
artifact_type: paper
venue: ECCV 2024
authors:
- Chonghao Sima
- Katrin Renz
- Kashyap Chitta
- Li Chen
- Hanxue Zhang
- Chengen Xie
- Ping Luo
- Andreas Geiger
- Hongyang Li
authors_short: Sima et al.
paperurl: https://arxiv.org/pdf/2312.14150.pdf
doi: 10.48550/arXiv.2312.14150
license: unspecified
summary: DriveLM formulates autonomous driving reasoning as graph-structured visual
  question answering over three ordered question types — perception, prediction, and
  planning — introduces the DriveLM-nuScenes and DriveLM-CARLA benchmarks with 150k+
  language-annotated QA pairs, and establishes a VLM baseline (BLIP-2/InstructBLIP)
  that produces interpretable, language-chained driving decisions.
why_important: DriveLM established graph-VQA as a principled framework for evaluating
  and training interpretable autonomous driving systems, pioneering the use of language
  reasoning chains to connect perception outputs to planning actions in a manner verifiable
  by humans and directly influencing DriveVLM, Senna, and Agent-Driver.
tags:
- vqa
- autonomous-driving
- language-grounding
- planning
- graph-reasoning
---

## Summary

DriveLM reframes autonomous driving as a graph-structured visual question answering task. Rather than treating driving as a direct input-output mapping from images to trajectories, it organizes the reasoning process into three ordered question types — *perception QA* (what objects are present and where), *prediction QA* (what will these objects do next), and *planning QA* (what should the ego vehicle do and why) — arranged as a directed acyclic graph where answers to earlier questions form context for later ones. This graph structure encodes the causal dependency that planning decisions should be grounded in predicted agent behavior, which in turn should be grounded in perceived object states. A VLM baseline based on BLIP-2 and InstructBLIP is adapted for this multi-hop QA task by processing the graph node-by-node and conditioning each answer on previously generated answers using prompt chaining, making each reasoning step human-readable and inspectable.

DriveLM-nuScenes is the primary dataset contribution, annotating 1,000 nuScenes scenes with approximately 150,000 QA pairs covering 6,000+ key objects, with perception, prediction, and planning questions for each key frame. Annotations are collected through a structured pipeline combining automated generation (from nuScenes 3D boxes and map labels) with human verification and completion. DriveLM-CARLA provides a complementary dataset in the closed-loop CARLA simulator, allowing evaluation of language-conditioned planning with reactive agents. Models are evaluated using both language quality metrics (accuracy, BLEU-4, CIDEr) and driving quality metrics (L2 displacement, collision rate) when planning-stage answers are decoded into trajectory waypoints. The VLM baseline achieves 41.4% answer accuracy on the held-out nuScenes test split, with ablations showing that removing earlier graph stages (perception, prediction QA) degrades planning accuracy by 15+ points, confirming that the multi-hop structure carries genuine reasoning signal.

The core methodological insight is that the graph-VQA formulation provides a structured scaffold for reasoning that is simultaneously testable at each stage and interpretable by humans — a property absent from end-to-end models that output only a trajectory. By expressing perception, prediction, and planning as language tokens in a causal chain, DriveLM enables error attribution: when a collision occurs, the chain can be inspected to determine whether it originated in a perceptual miss, a prediction failure, or a planning error. The authors also introduce a graph-constrained generation procedure that enforces that child nodes attend to parent node answers via prefix-constrained decoding, preventing the VLM from ignoring earlier reasoning context.

## Why It Matters

DriveLM's contribution to the field is twofold: as a dataset resource (DriveLM-nuScenes became the standard language-annotated driving benchmark alongside nuScenes-QA) and as a methodological template (graph-VQA as an evaluation and training framework for interpretable driving). The work directly influenced DriveVLM's chain-of-thought scene analysis pipeline and the explanation modules in Senna and Agent-Driver, which use natural language to communicate VLM scene understanding to downstream planners. The DriveLM benchmark was adopted in the nuScenes language challenge track, attracting submissions from major research labs in 2024, and the dataset and model code became one of the most-starred driving language benchmarks of that year. Its language-chain approach demonstrated concretely that structured intermediate reasoning improves both final accuracy and human trust in automated decisions.

DriveLM's graph-VQA formulation, while interpretable, imposes a fixed reasoning structure that may not generalize to all driving scenarios — edge cases involving unusual road layouts, construction, or emergency vehicles often require more flexible reasoning than the fixed three-level schema permits. The VLM baseline achieves 41.4% answer accuracy, leaving substantial room for improvement; moreover, language accuracy does not guarantee trajectory safety, as a model can produce fluent, plausible language chains that lead to physically infeasible trajectories. The nuScenes-based annotations reflect the specific geographic and traffic characteristics of Boston and Singapore, limiting diversity. The CARLA-based evaluation, while offering closed-loop testing, inherits CARLA's domain gap relative to real-world sensor data. Follow-on work such as DriveVLM-Dual and Senna shifted toward tighter integration between language reasoning and continuous trajectory planning, addressing DriveLM's gap between discrete language outputs and precise ego-motion control.

| | |
|---|---|
| **Authors** | Sima et al. |
| **Year** | 2023 |
| **Venue** | ECCV 2024 |
| **Field** | Autonomous Driving |
| **Subfield** | Llm Vla Autonomous Driving |
| **Tasks** | visual-qa, language-driving, graph-reasoning, planning |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2312.14150.pdf){: .btn .btn--primary .btn--large}
