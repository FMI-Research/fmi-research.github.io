---
title: 'GEM: A Generalizable Ego-Vision Multimodal World Model for Fine-Grained Ego-Motion,
  Object Dynamics, and Scene Composition Control'
collection: papers
permalink: /papers/autonomous-driving/gem_a_generalizable_ego-vision_multimodal_world_model_for_fine-grained_ego-motion_object_dynamics_and_scene_composition_control/
date: '2024-12-15'
year: 2024
field: autonomous-driving
subfield: world-models-autonomous-driving
tasks:
- world-model
- video-generation
- ego-motion-control
- object-dynamics
- multimodal-generation
tier: 1
artifact_type: paper
venue: arXiv 2024
authors:
- Mariam Hassan
- Sebastian Stapf
- Ahmad Rahimi
- Pedro M B Rezende
- Yasaman Haghighi
- David Brüggemann
- Isinsu Katircioglu
- Lin Zhang
- Xiaoran Chen
- Suman Saha
- Marco Cannici
- Elie Aljalbout
- Botao Ye
- Xi Wang
- Aram Davtyan
- Mathieu Salzmann
- Davide Scaramuzza
- Marc Pollefeys
- Paolo Favaro
- Alexandre Alahi
authors_short: Hassan et al.
paperurl: /files/papers/gem_a_generalizable_ego-vision_multimodal_world_model_for_fine-grained_ego-motion_object_dynamics_and_scene_composition_control.pdf
doi: 10.48550/arXiv.2412.11198
license: open-access
summary: GEM is a generalizable ego-vision multimodal world model that predicts future
  RGB and depth frames conditioned on a reference frame, sparse visual features, human
  poses, and ego-trajectories — enabling fine-grained control over ego-motion, object
  dynamics, and scene composition across autonomous driving, drone flight, and egocentric
  human activity domains.
why_important: GEM establishes a unified world model paradigm that spans multiple
  ego-centric domains and modalities, demonstrating that a single model architecture
  can learn generalizable physics of ego-motion and object interaction from 4000+
  hours of heterogeneous video data — a key step toward scalable, domain-agnostic
  world models for embodied AI and autonomous driving.
tags:
- world-model
- autonomous-driving
- ego-vision
- video-generation
- multimodal
- depth-estimation
- object-dynamics
- open-source
---

## Summary

GEM (Generalizable Ego-vision Multimodal world model) addresses a fundamental challenge in ego-vision AI: learning a unified generative model of how the world evolves from a first-person perspective, with precise controllability over the ego-agent's motion, the dynamics of objects in the scene, and human body poses. The model conditions future frame generation on four input signals — a reference frame, sparse optical flow features (encoding scene dynamics), estimated human poses, and ego-trajectory waypoints — and generates both RGB and depth outputs jointly. This paired multimodal output enables richer spatial understanding than RGB-only generation. The architecture uses a diffusion-based video generation backbone with autoregressive noise schedules to maintain temporal consistency over long-horizon generations (beyond the training window), a known failure mode of vanilla video diffusion models.

GEM is trained on an unusually diverse dataset comprising 4,000+ hours of ego-centric video across three distinct domains: autonomous driving (vehicle dashcam), egocentric human activities (first-person wearable cameras), and drone flights (aerial ego-perspective). Domain-specific pseudo-labels — depth maps from monocular depth estimators, ego-trajectories from odometry/SLAM, and human poses from pose estimators — provide the conditioning signals without requiring ground-truth sensor data. This design makes the training scalable to any large-scale ego-centric video collection. Experiments demonstrate that GEM generates diverse and temporally consistent scenarios: object insertion and removal with realistic occlusion handling, ego-trajectory counterfactuals (what would the scene look like if the ego took a left turn?), human pose retargeting, and novel view synthesis at novel trajectories. The paper introduces a new **Control of Object Manipulation (COM)** metric to evaluate how faithfully generated scenes reflect specified object manipulations, complementing existing FID/FVD quality metrics.

The key methodological contributions are threefold. First, the **autoregressive noise schedule** conditions each generated frame on previously generated frames by injecting them as noisy conditioning signals, preventing temporal drift and enabling arbitrarily long video generation without quality collapse. Second, the **sparse feature conditioning** — using optical flow features rather than dense RGB features from prior frames — provides a compact yet informative motion signal that generalizes across domains with different visual statistics. Third, GEM is fully open-sourced (code, model weights, and dataset), which is notable given the scale and diversity of its training data. The project page is at [vita-epfl.github.io/GEM.github.io](https://vita-epfl.github.io/GEM.github.io/).

## Why It Matters

GEM represents a significant advance in world models for ego-vision by demonstrating that a single model can serve as a controllable simulator across fundamentally different ego-agent types — cars, humans, and drones. This generalization capability is important because it suggests that the physics of ego-centric perception (parallax, ego-motion, near-field dynamics) is sufficiently universal to be learned across domains. For autonomous driving specifically, GEM enables high-fidelity counterfactual scenario generation — e.g., "what would have happened if the ego had braked earlier?" or "what does this intersection look like with a pedestrian inserted at position X?" — which is directly useful for safety-critical policy evaluation and data augmentation for rare-event coverage. The paired RGB+depth generation further enables downstream 3D perception tasks to benefit from augmented data without requiring expensive LiDAR capture.

The paper also points toward an open challenge: while GEM achieves strong controllability on individual manipulation types (move an object, change trajectory), compositional control — simultaneously specifying multiple independent manipulations — remains difficult. The COM metric provides a new evaluation axis for future work. GEM sits at the intersection of embodied AI world models (learning environment dynamics from ego-data) and autonomous driving simulation (generating controllable driving scenarios), making it relevant to both communities. Its fully open-source release positions it as a baseline for the emerging field of generalist ego-vision world models, analogous to how Stable Diffusion served as a baseline for image generation research.

| | |
|---|---|
| **Authors** | Hassan et al. |
| **Year** | 2024 |
| **Venue** | arXiv 2024 |
| **Field** | Autonomous Driving |
| **Subfield** | World Models for Autonomous Driving |
| **Tasks** | world-model, video-generation, ego-motion-control, object-dynamics, multimodal-generation |
| **Tier** | 1 — Survey / Landmark |
| **License** | open-access |

[View / Download PDF](/files/papers/gem_a_generalizable_ego-vision_multimodal_world_model_for_fine-grained_ego-motion_object_dynamics_and_scene_composition_control.pdf){: .btn .btn--primary .btn--large}
