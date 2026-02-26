---
title: 'End-to-End Autonomous Driving: Challenges and Frontiers'
collection: papers
permalink: /papers/autonomous-driving/end-to-end_autonomous_driving_challenges_and_frontiers/
date: '2023-06-28'
year: 2023
field: autonomous-driving
subfield: end-to-end-autonomous-driving
tasks:
- survey
- end-to-end-driving
- imitation-learning
- reinforcement-learning
tier: 1
artifact_type: paper
venue: IEEE TPAMI 2024
authors:
- Li Chen
- Penghao Wu
- Kashyap Chitta
- Bernhard Jaeger
- Andreas Geiger
- Hongyang Li
authors_short: Chen et al.
paperurl: https://arxiv.org/pdf/2306.16927.pdf
doi: 10.48550/arXiv.2306.16927
license: unspecified
summary: A comprehensive survey of end-to-end autonomous driving that taxonomizes
  architectures by learning paradigm (imitation, reinforcement, and hybrid), surveys
  sensor fusion strategies, representation learning methods, and evaluation benchmarks,
  and identifies distribution shift, safety guarantees, and sim-to-real transfer as
  primary open challenges.
why_important: This IEEE TPAMI survey is the canonical reference for the E2E autonomous
  driving paradigm, providing the most complete structured taxonomy and benchmark
  analysis available as of 2023–2024 and directly shaping the research agenda that
  motivated NAVSIM, nuPlan, and subsequent closed-loop evaluation initiatives.
tags:
- survey
- end-to-end
- autonomous-driving
- imitation-learning
---

## Summary

Chen et al. conduct a systematic review of end-to-end autonomous driving systems that directly map raw sensor observations to driving actions or trajectory waypoints, bypassing the classical modular decomposition into perception, prediction, and planning sub-systems. The survey proposes a multi-dimensional taxonomy covering: (1) sensor input modalities and fusion strategies (camera-only, LiDAR, radar, multi-modal); (2) scene representation types (rasterized BEV, point cloud, vectorized, implicit neural); (3) learning paradigms (behavior cloning / imitation learning, offline RL, online RL, and knowledge distillation from expert systems); and (4) architecture families (one-stage reactive policies, two-stage systems with explicit intermediate representations, and modular-but-differentiable pipelines). The survey covers over 270 papers published from early ALVINN-era work through mid-2023, organized around the conceptual arc from open-loop imitation to closed-loop policy optimization.

A substantial portion of the survey is dedicated to evaluation methodology, where the authors identify a troubling disconnect between benchmark metrics and real-world driving competence. CARLA's leaderboard (Town05, Longest6, LAV, and Bench2Drive variants) is analyzed in detail, with discussion of how route completion and infraction metrics can be gamed by conservative agents. nuScenes open-loop metrics (L2, collision rate) are critiqued for rewarding trajectory imitation over actual safety reasoning. The survey also covers nuPlan's closed-loop reactive simulation — at the time the most realistic publicly available closed-loop benchmark — and analyzes the IDM and PDM baselines that dominate its leaderboards. Critically, the authors show that correlation between open-loop and closed-loop metrics is weak, making benchmark selection a first-order methodological decision.

The survey synthesizes three families of fundamental open problems. *Distribution shift and long-tail generalization*: E2E models trained by behavior cloning collapse on out-of-distribution scenarios, and even DAgger-style aggregation provides limited coverage of rare but safety-critical events. *Safety and formal guarantees*: current learned policies offer no formal certificates of collision avoidance or rule compliance, and integrating formal verification with neural policies remains nascent. *Sim-to-real transfer*: despite photorealistic simulators (CARLA, nuPlan, Waymo Open), domain gaps in sensor noise, agent behavior, and traffic density degrade transferred policies. The authors call for hybrid architectures that combine the generalization of learned representations with the reliability of rule-based fallbacks — a recommendation that DriveVLM's dual-system design and later work would begin to address.

## Why It Matters

This survey has become the standard first reference for researchers entering the E2E autonomous driving field, providing both historical grounding and a structured map of contemporary methods. Its publication in IEEE TPAMI — the discipline's most selective transactions journal — gave it wide visibility beyond the computer vision conference community. The taxonomy the authors propose (particularly the imitation vs. RL vs. hybrid axis and the representation type axis) is now routinely cited in papers proposing new architectures or benchmarks. Its analysis of metric inadequacy was particularly influential: it directly motivated NAVSIM's design of PDMS as a richer, non-reactive alternative to nuScenes L2, and nuPlan's continued development of reactive simulation. The survey also documented the rapid influx of transformer-based architectures and BEV-centric representations that began with BEVFormer (2022) and UniAD (2022), contextualizing those contributions within the longer E2E arc.

As a snapshot of a rapidly moving field, the survey's coverage of LLM and VLM integration into driving is limited to a brief prospective section — the field had not yet produced the volume of work that would emerge in 2024 (DriveVLM, DriveLM, Senna, etc.). Reinforcement learning approaches are surveyed primarily through CARLA-based results, underrepresenting real-world online learning challenges that require safe exploration. The survey's benchmark analysis was accurate at time of writing but has been partially superseded by Bench2Drive, NAVSIM, and the nuScenes planning challenge updates. Finally, the survey does not address cooperative or vehicle-to-infrastructure (V2X) driving, multi-agent learning, or the deployment gap between academic benchmarks and production-scale autonomous vehicle systems — all areas of active research that have grown substantially since publication.

| | |
|---|---|
| **Authors** | Chen et al. |
| **Year** | 2023 |
| **Venue** | IEEE TPAMI 2024 |
| **Field** | Autonomous Driving |
| **Subfield** | End To End Autonomous Driving |
| **Tasks** | survey, end-to-end-driving, imitation-learning, reinforcement-learning |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2306.16927.pdf){: .btn .btn--primary .btn--large}
