---
title: 'DriveDreamer: Towards Real-world-driven World Models for Autonomous Driving'
collection: papers
permalink: /papers/autonomous-driving/drivedreamer_towards_real-world-driven_world_models_for_autonomous_driving/
date: '2023-09-18'
year: 2023
field: autonomous-driving
subfield: world-models-autonomous-driving
tasks:
- world-model
- driving-simulation
- video-generation
tier: 2
artifact_type: paper
venue: ECCV 2024
authors:
- Xiaofeng Wang
- Zheng Zhu
- Guan Huang
- Xinze Chen
- Jiwen Lu
authors_short: Wang et al.
paperurl: https://arxiv.org/pdf/2309.09777.pdf
doi: 10.48550/arXiv.2309.09777
license: unspecified
summary: DriveDreamer is a diffusion-based driving world model that generates controllable
  multi-camera video sequences from structured HD map, 3D bounding box, and text conditioning
  signals, achieving FID 52.6 on nuScenes video generation and enabling both data
  augmentation and policy evaluation in simulation.
why_important: As one of the first driving world models grounded in real-world structured
  conditioning rather than purely generative priors, DriveDreamer established a template
  for controllable video-based simulation that prefigured a lineage of generative
  AD world models including GAIA-1, WoVGen, and Vista.
tags:
- world-model
- autonomous-driving
- video-generation
- simulation
- diffusion
---

## Summary

DriveDreamer proposes a two-stage diffusion framework for generating realistic, physically consistent driving video sequences conditioned on structured scene representations. The first stage trains a ControlNet-style adapter that injects structural guidance — rendered HD map grids, projected 3D bounding boxes of surrounding agents, and optional text descriptions of driving conditions — into a latent video diffusion backbone. The second stage performs temporal refinement to enforce inter-frame consistency and smooth camera motion across the six surrounding camera views used in the nuScenes multi-camera setup. Conditioning on HD maps and bounding boxes provides geometric grounding, ensuring that generated videos respect the spatial layout of roads, intersections, and traffic participants. Text conditioning (e.g., "heavy rain," "highway merging") enables scene-level diversity without requiring distinct training splits per condition.

DriveDreamer is trained and evaluated on the nuScenes dataset using standard video generation metrics. It achieves a Fréchet Inception Distance (FID) of 52.6 on held-out nuScenes scenes — substantially better than unconditional or text-only video generation baselines, which exceed FID 100 on the same splits. The structured conditioning also improves FVD (Fréchet Video Distance) by 38% relative to ablations that remove map conditioning, demonstrating that geometric structure is the dominant information source for visual realism. Qualitative evaluations show that the model correctly generates lane markings, traffic sign placements, and agent trajectories consistent with the input HD map topology. In a data augmentation experiment, detection models trained with DriveDreamer-augmented datasets show 2–4% mAP improvement over those trained on real data alone, confirming downstream utility beyond perceptual quality metrics.

The key methodological contribution is the structured conditioning pipeline: unlike prior generative driving models that condition on ego speed, steering angle, or abstract latent codes, DriveDreamer conditions directly on explicit semantic and geometric annotations in a form compatible with standard HD map formats. This makes the generation process interpretable and directly controllable — a practitioner can modify an input HD map or agent bounding box and observe the resulting video change predictably. The two-stage architecture addresses a key failure mode of single-stage video diffusion, which tends to produce temporally incoherent frames. DriveDreamer also introduces a driving-condition-aware text tokenizer that maps structured ego-state and traffic-density descriptions into CLIP-compatible embeddings, enabling semantic diversity while preserving structural fidelity.

## Why It Matters

DriveDreamer was among the first works to demonstrate that modern latent diffusion models can be controlled by the structured annotations already produced by AD perception stacks, bridging generative AI and autonomous driving in a practically useful way. Its publication coincided with and helped catalyze a wave of driving world model papers in 2023–2024: GAIA-1 (Wayve) used a transformer-based world model conditioned on ego actions; WoVGen extended spatial-temporal conditioning to multi-agent future roll-outs; Vista pursued higher fidelity using rectified flow models; and MagicDrive and DriveX explored richer scene layouts. The data augmentation use case proved particularly compelling for perception teams lacking access to rare-scenario real-world data, and the controllability angle positioned DriveDreamer as a simulation tool rather than merely a content generation system.

DriveDreamer's primary limitations are resolution and temporal length: generated videos are short-horizon (typically 8–16 frames at 256×448 resolution) and exhibit accumulated temporal drift in longer sequences due to the two-stage refinement approach rather than end-to-end temporal modeling. The model relies on nuScenes HD map annotations, which are not available at deployment time, limiting its applicability to systems that can generate HD maps online. FID and FVD metrics measure distributional similarity rather than semantic correctness — a generated video with realistic textures but impossible physics can achieve a low FID. Subsequent work such as DriveWM and WoVGen addressed multi-agent consistency and longer roll-out horizons; the closed-loop utility of DriveDreamer-generated video as a policy training signal also remains limited because the model is non-reactive and cannot respond to ego deviations from the conditioning trajectory.

| | |
|---|---|
| **Authors** | Wang et al. |
| **Year** | 2023 |
| **Venue** | ECCV 2024 |
| **Field** | Autonomous Driving |
| **Subfield** | World Models Autonomous Driving |
| **Tasks** | world-model, driving-simulation, video-generation |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2309.09777.pdf){: .btn .btn--primary .btn--large}
