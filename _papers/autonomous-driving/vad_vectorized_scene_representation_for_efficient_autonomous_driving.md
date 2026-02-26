---
title: 'VAD: Vectorized Scene Representation for Efficient Autonomous Driving'
collection: papers
permalink: /papers/autonomous-driving/vad_vectorized_scene_representation_for_efficient_autonomous_driving/
date: '2023-03-21'
year: 2023
field: autonomous-driving
subfield: end-to-end-autonomous-driving
tasks:
- end-to-end-driving
- vectorized-representation
- planning
tier: 2
artifact_type: paper
venue: ICCV 2023
authors:
- Bo Jiang
- Shaoyu Chen
- Qing Xu
- Bencheng Liao
- Jiajie Chen
- Helong Zhou
- Qian Zhang
- Wenyu Liu
- Chang Huang
- Xinggang Wang
authors_short: Jiang et al.
paperurl: https://arxiv.org/pdf/2303.12077.pdf
doi: 10.48550/arXiv.2303.12077
license: unspecified
summary: Introduces VAD, an end-to-end autonomous driving framework that encodes the
  entire driving scene — map elements and dynamic agents — as vectorized polyline
  instances and uses vectorized scene-agent interaction modules to derive ego trajectory
  plans, achieving UniAD-competitive nuScenes planning performance at roughly twice
  the inference speed.
why_important: VAD demonstrated that explicit vectorized scene representations eliminate
  the inductive bias of dense grid convolutions and produce a sparser, more interpretable
  planning substrate, directly influencing SparseDrive, VADv2, and the broader shift
  away from rasterized BEV features in E2E driving.
tags:
- end-to-end
- autonomous-driving
- vectorized
- planning
- nuscenes
---

## Summary

VAD (Vectorized Autonomous Driving) replaces the dense bird's-eye-view grid representations used by UniAD and its predecessors with a fully vectorized scene encoding. Map elements — lane centerlines, road boundaries, pedestrian crossings — are represented as ordered polylines, and dynamic agents are encoded as temporally tracked bounding-box sequences. This choice avoids the memory and computational overhead of high-resolution BEV feature maps and naturally provides instance-level structural information without requiring explicit segmentation. The scene is encoded by a multi-camera backbone followed by a BEV transformer; map and agent polylines are then extracted via corresponding query decoders. Planning is performed by a trajectory decoder that conditions on vectorized map queries and agent motion queries through a series of cross-attention layers, replacing the volumetric occupancy reasoning used in UniAD with lightweight pairwise instance interactions.

On the nuScenes planning benchmark, VAD achieves an L2 displacement error of 0.54 m at 2 s and a collision rate of 0.04%, closely matching UniAD's planning performance (0.48 m L2, 0.08% collision). Crucially, VAD runs at approximately 3.6 fps — roughly 2× faster than UniAD — owing to the elimination of dense BEV convolutions and OccFormer-style occupancy reasoning. Ablation studies confirm that vectorized map constraints provide stronger signal to the planner than occupancy-based future prediction; removing vectorized map queries degrades collision rate by over 30%. On the map element extraction sub-task, VAD achieves competitive mAP relative to MapTR, confirming that the vectorized encoding does not sacrifice geometric accuracy.

VAD introduces two novel interaction modules: *vectorized scene interaction*, which models pairwise relationships between map elements and agent trajectories via attention over polyline tokens; and *vectorized scene-ego interaction*, which grounds the ego vehicle's planned motion relative to explicit map topology and predicted agent futures. A constraint-based planning loss enforces that the planned trajectory does not violate detected map boundaries and maintains safe distances from predicted agent futures. This integration of structural geometric constraints directly into the training loss is a significant departure from UniAD's occupancy-based collision avoidance, and makes the planning stage more interpretable — lane-boundary violations and proximity violations are explicit loss terms rather than emergent behaviors of an occupancy field.

## Why It Matters

VAD's open-source release alongside ICCV 2023 made it one of the most adopted baselines for E2E driving research in 2023–2024. Its central argument — that vectorized, instance-centric representations are both more efficient and more interpretable than dense BEV grids — catalyzed a broader architectural shift. SparseDrive extended the idea further to fully sparse instance queries with no BEV backbone at all. Senna (from the same research group) adopted the VAD trajectory decoder as its low-level E2E planner, coupling it with a VLM for high-level intent. The follow-up VADv2 added online HD map prediction and generalized the vectorized paradigm to richer scene topologies. VAD's explicit constraint losses also influenced later planning formulations that treat map and agent context as hard or soft geometric constraints rather than as auxiliary supervision signals.

Despite its efficiency and interpretability advantages, VAD's vectorized representation carries limitations. Polyline-based encoding imposes a fixed-cardinality assumption per scene element category and struggles with complex topology changes (e.g., construction zones, unmarked intersections) where lane connectivity is ambiguous or absent. The camera-only sensor stack inherits the depth-estimation uncertainty of monocular BEV methods, limiting precision in crowded 3D scenes. VAD's open-loop evaluation on nuScenes continues to rely on L2 and collision rate metrics that cannot capture causal agent reactions to the ego vehicle — a gap that NAVSIM's non-reactive simulation partially addresses. Additionally, VAD's focus on nuScenes leaves its generalization to geographically diverse or unstructured environments under-explored, motivating work on map-free and topology-robust planning formulations.

| | |
|---|---|
| **Authors** | Jiang et al. |
| **Year** | 2023 |
| **Venue** | ICCV 2023 |
| **Field** | Autonomous Driving |
| **Subfield** | End To End Autonomous Driving |
| **Tasks** | end-to-end-driving, vectorized-representation, planning |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2303.12077.pdf){: .btn .btn--primary .btn--large}
