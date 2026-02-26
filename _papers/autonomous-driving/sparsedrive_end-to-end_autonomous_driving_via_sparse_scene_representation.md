---
title: 'SparseDrive: End-to-End Autonomous Driving via Sparse Scene Representation'
collection: papers
permalink: /papers/autonomous-driving/sparsedrive_end-to-end_autonomous_driving_via_sparse_scene_representation/
date: '2024-05-30'
year: 2024
field: autonomous-driving
subfield: end-to-end-autonomous-driving
tasks:
- end-to-end-driving
- sparse-representation
- planning
- simulation
tier: 2
artifact_type: paper
venue: arXiv 2024
authors:
- Wencheng Han
- Xiaokang Chen
- Zhengzhe Liu
- Jianbing Shen
authors_short: Han et al.
paperurl: https://arxiv.org/pdf/2405.19620.pdf
doi: 10.48550/arXiv.2405.19620
license: unspecified
summary: SparseDrive proposes a fully sparse end-to-end autonomous driving framework
  in which all scene elements — 3D agents, map instances, and the ego trajectory —
  are represented as sparse instance queries without any dense BEV feature grid, incorporating
  symmetry-aware occupancy optimization and a parallel motion planner to outperform
  UniAD on nuScenes L2 planning at twice the inference speed.
why_important: SparseDrive demonstrated that eliminating dense BEV feature grids in
  favor of fully sparse instance-centric representations is sufficient for high-quality
  E2E driving, advancing the efficiency frontier and reinforcing the architectural
  trend initiated by VAD toward sparser, more scalable scene representations.
tags:
- end-to-end
- autonomous-driving
- sparse-representation
- planning
- efficiency
---

## Summary

SparseDrive eliminates the dense bird's-eye-view feature map that is central to architectures like BEVFormer, UniAD, and even VAD (which still uses a BEV backbone). Instead, all scene entities — 3D agent instances, map element instances, and the ego vehicle — are encoded as sparse instance queries initialized from object-level priors and iteratively updated through transformer cross-attention with raw camera features. This creates a fully sparse scene graph where instance representations are computed only where scene elements exist, rather than over a uniform dense grid. The agent detection, tracking, and map element prediction modules share a common sparse query architecture, enabling weight sharing and reducing the total parameter count. The ego planner is implemented as a parallel module that cross-attends to the finalized sparse agent and map queries to produce trajectory waypoints, without requiring occupancy prediction or a separate future-state propagation step.

On nuScenes open-loop planning, SparseDrive achieves 0.41 m L2 at 2 s and 0.05% collision rate, outperforming UniAD (0.48 m L2, 0.08% collision) and matching or exceeding VAD. The system runs at approximately 7.7 fps on a single A100 GPU — roughly 2× faster than UniAD's ~3.7 fps — demonstrating that the efficiency gain is substantial and architecturally fundamental rather than implementation-dependent. On 3D detection (NDS, mAP), SparseDrive achieves competitive performance with Sparse4D and BEVFormer-based detectors despite the absence of a dense BEV backbone. Ablations confirm that symmetry-aware occupancy loss contributes 0.04 m L2 improvement, and the parallel motion planner (versus sequential) contributes an additional 0.03 m reduction, validating both design choices independently.

SparseDrive introduces two notable innovations beyond the sparse representation itself. First, *symmetry-aware occupancy optimization*: rather than predicting a full ego-centric occupancy grid, the system leverages the spatial symmetry of driving scenarios to impose consistency constraints on occupancy estimates, reducing parameter count and improving sample efficiency. Second, a *parallel motion planner*: conventional E2E systems execute perception → prediction → planning sequentially, introducing latency proportional to the cascade depth. SparseDrive's planner runs simultaneously with the agent motion prediction module by sharing the sparse query backbone, with outputs merged at a late fusion layer. This architectural parallelism is enabled precisely by the sparse representation — in dense BEV systems, the planner must wait for the full BEV feature map to be populated before attending to scene features, creating an unavoidable sequential bottleneck.

## Why It Matters

SparseDrive's open-source release in 2024 provided the community with a strong, efficient, and reproducible alternative to UniAD and VAD as a nuScenes planning baseline. Its demonstration that fully sparse representations can outperform dense BEV approaches on both quality and speed metrics settled an architectural debate ongoing since VAD's partial move toward vectorized encoding. The work reinforced a clear trend: BEV grid density is not necessary for E2E planning performance, and future architectures should prefer instance-centric representations for scalability. Subsequent work extended the SparseDrive paradigm: Sparse4Dv3 applied similar sparse queries to high-resolution temporal perception, and follow-up variants extended the framework to multi-modal input. SparseDrive's symmetry-aware occupancy component was also cited by NAVSIM participants as a useful auxiliary signal for open-loop metric optimization.

SparseDrive's open-loop nuScenes evaluation shares the limitations of all L2/collision-rate-based metrics: these measures reward trajectory imitation accuracy rather than closed-loop safety under reactive agents, and a model can achieve low L2 by closely copying the logged ego trajectory rather than genuinely reasoning about scene dynamics. The sparse instance representation, while efficient, depends heavily on the quality of initial query initialization — if the detector misses an object or initializes a query far from the true location, the sparse query may fail to converge, causing a hard false negative rather than the graceful degradation of dense occupancy representations. SparseDrive also does not address multi-modal sensor fusion (LiDAR + camera), limiting its practical deployment utility in production AV systems where LiDAR is standard. The symmetry-aware occupancy design assumes relatively structured road environments and may degrade in construction zones or off-road settings where the symmetry prior is violated.

| | |
|---|---|
| **Authors** | Han et al. |
| **Year** | 2024 |
| **Venue** | arXiv 2024 |
| **Field** | Autonomous Driving |
| **Subfield** | End To End Autonomous Driving |
| **Tasks** | end-to-end-driving, sparse-representation, planning, simulation |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2405.19620.pdf){: .btn .btn--primary .btn--large}
