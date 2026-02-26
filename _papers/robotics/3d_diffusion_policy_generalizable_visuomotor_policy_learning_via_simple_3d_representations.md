---
title: '3D Diffusion Policy: Generalizable Visuomotor Policy Learning via Simple 3D
  Representations'
collection: papers
permalink: /papers/robotics/3d_diffusion_policy_generalizable_visuomotor_policy_learning_via_simple_3d_representations/
date: '2024-03-06'
year: 2024
field: robotics
subfield: manipulation-imitation-learning
tasks:
- visuomotor-policy
- 3d-perception
- diffusion-policy
tier: 2
artifact_type: paper
venue: RSS 2024
authors:
- Yanjie Ze
- Gu Zhang
- Kangning Zhang
- Chenyuan Hu
- Muhan Wang
- Huazhe Xu
authors_short: Ze et al.
paperurl: https://arxiv.org/pdf/2403.03954.pdf
doi: 10.48550/arXiv.2403.03954
license: unspecified
summary: 3D Diffusion Policy (DP3) replaces the 2D CNN or ViT image encoder in standard
  diffusion-based robot policies with a compact PointNet++ encoder operating on 1,024-point
  subsampled RGB-D point clouds, conditions a DDPM-style denoising network on the
  resulting 3D geometric features, and achieves a 24.2% average improvement over the
  2D Diffusion Policy baseline across 72 simulation tasks in 4 environments and 83%
  vs. 62% on 5 real Franka tasks — with inference latency remaining comparable to
  2D baselines at ~50ms.
why_important: Demonstrated a low-overhead integration path for 3D-aware visuomotor
  policies that sparked follow-up work on richer 3D representations (Gaussian splatting
  features, NeRF-based encoders, 3D-aware attention) and renewed interest in depth
  sensors as first-class policy inputs; sensitivity to point cloud noise and the inability
  to leverage RGB semantic features (critical for language-grounded or distractor-rich
  tasks) remain open challenges addressed by subsequent work on 3D-grounded language
  policies.
tags:
- diffusion-policy
- 3d-perception
- point-cloud
- visuomotor
- generalization
---

## Summary

3D Diffusion Policy (DP3) addresses a fundamental representational bottleneck in visuomotor policy learning: 2D image encoders discard the depth and geometric structure that are most informative for precise manipulation (object distance, surface orientation, spatial layout). DP3 replaces the standard 2D CNN or ViT observation encoder with a PointNet++-style encoder that operates directly on 3D point clouds derived from a single RGB-D camera via back-projection. The encoded 3D features — a compact 128-dimensional global descriptor from a 1,024-point subsampled cloud — condition a DDPM-style diffusion policy network that denoises action trajectories over a learned score function. The 3D encoder and diffusion network are trained end-to-end from demonstration data. Crucially, the point cloud representation requires only a single depth sensor and no multi-camera calibration infrastructure, keeping the hardware requirements modest.

DP3 is evaluated across 72 manipulation tasks drawn from 4 simulation environments — Adroit (dexterous hand tasks), DexArt (articulated object manipulation), MetaWorld (tabletop manipulation), and a custom suite — and compared against 2D Diffusion Policy, 3D-aware baselines, and several prior visuomotor approaches. DP3 achieves a 24.2% average improvement in success rate over the 2D Diffusion Policy baseline across all 72 tasks, with particularly large gains on tasks that require geometric precision: peg-in-hole insertion, drawer opening, and reorientation under pose variation. Importantly, the inference latency of DP3 (~50ms per step) matches 2D Diffusion Policy, confirming that the 3D representation adds no meaningful overhead at the architecture level. Real-robot experiments on 5 tasks with a Franka Panda arm confirm sim-to-real transfer: 83% average success vs. 62% for the 2D baseline, with the largest gains on tasks requiring sub-centimeter end-effector positioning.

The most important design choice is the *compact 3D representation* strategy: rather than feeding the full raw point cloud (which can contain 100K+ points from a VGA depth frame) to the policy, DP3 subsamples to exactly 1,024 points using farthest point sampling before the PointNet++ encoder. This keeps the 3D processing computationally cheap — the encoder adds fewer than 2M parameters — while retaining the geometric structure needed for manipulation. The paper ablates subsampling rate, encoder architecture (PointNet vs. PointNet++), and camera placement, finding that a single fixed wrist-mounted depth camera provides sufficient coverage for tabletop tasks and that most gains come from global geometric features rather than fine local point-level detail.

## Why It Matters

DP3 made 3D-aware visuomotor policies immediately practical for the broader robotics community by demonstrating a simple, low-overhead integration path: replace the image encoder with a point cloud encoder, keep the diffusion policy backbone unchanged. The 24%+ improvement over a well-tuned 2D baseline was striking and reproducible by the community, sparking a wave of follow-up work exploring richer 3D representations as policy inputs: Gaussian splatting features (GaussianPolicy), NeRF-derived scene embeddings, voxel-based diffusion, and 3D-aware cross-attention mechanisms. The paper also contributed to a broader shift in the robotics community's attitude toward depth sensors — from RGB-dominant assumptions (driven by internet-scale pretraining) toward treating depth as a first-class, low-cost signal that provides direct geometric grounding without requiring large pretraining datasets.

Key limitations of DP3 are sensitivity to point cloud noise and density variation in real deployments (sim-to-real gaps in depth sensor characteristics can cause significant performance degradation without recalibration), and the inability to incorporate semantic or appearance information present in the RGB stream. A pure geometry representation discards color, texture, and semantic features — which makes DP3 poorly suited for tasks requiring object identification among visually similar distractors or language-conditioned grasping ("pick the red mug"). Follow-up work has explored fusing RGB features with 3D geometry (RGB-point cloud fusion, 2D-3D feature concatenation), and language-grounded 3D policies (RoboPoint, 3D-VLA) that extend DP3-style encoders with vision-language pretraining — addressing the semantic gap while preserving the geometric precision advantages.

| | |
|---|---|
| **Authors** | Ze et al. |
| **Year** | 2024 |
| **Venue** | RSS 2024 |
| **Field** | Robotics |
| **Subfield** | Manipulation Imitation Learning |
| **Tasks** | visuomotor-policy, 3d-perception, diffusion-policy |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2403.03954.pdf){: .btn .btn--primary .btn--large}
