---
title: 'NAVSIM: Data-Driven Non-Reactive Autonomous Vehicle Simulation and Benchmarking'
collection: papers
permalink: /papers/autonomous-driving/navsim_data-driven_non-reactive_autonomous_vehicle_simulation_and_benchmarking/
date: '2024-06-21'
year: 2024
field: autonomous-driving
subfield: end-to-end-autonomous-driving
tasks:
- benchmark
- simulation
- planning
- evaluation
tier: 3
artifact_type: paper
venue: NeurIPS 2024
authors:
- Daniel Dauner
- Marcel Hallgarten
- Tianyu Li
- Xinshuo Weng
- Zhiyu Huang
- Zetong Yang
- Hongyang Li
- Igor Gilitschenski
- Boris Ivanovic
- Marco Pavone
- Andreas Geiger
- Kashyap Chitta
authors_short: Dauner et al.
paperurl: https://arxiv.org/pdf/2406.15349.pdf
doi: 10.48550/arXiv.2406.15349
license: unspecified
summary: NAVSIM is a data-driven, non-reactive autonomous driving simulation and benchmarking
  framework that evaluates planner quality on real sensor data using the PDM-Score
  (PDMS) — a composite metric integrating progress, comfort, no-at-fault collision,
  drivable area compliance, and time-to-collision — without requiring expensive closed-loop
  simulation.
why_important: NAVSIM's PDMS metric and non-reactive simulation paradigm bridged the
  evaluation gap between naïve open-loop L2 metrics and computationally prohibitive
  closed-loop simulation, and its adoption as the NeurIPS 2024 competition benchmark
  with 150+ teams established it as the community-standard planner evaluation framework
  for 2024–2025.
tags:
- benchmark
- autonomous-driving
- simulation
- planning
- evaluation
---

## Summary

NAVSIM addresses a fundamental evaluation problem in autonomous driving research: open-loop metrics such as L2 displacement and collision rate reward trajectory imitation but poorly predict real-world safety and comfort, while closed-loop simulation (as in nuPlan or CARLA) is computationally expensive, requires calibrated agent behavior models, and is difficult to reproduce at scale. NAVSIM's solution is *non-reactive simulation*: it replays recorded real-world sensor data from the OpenScene/nuPlan dataset (thousands of hours of diverse driving across Boston, Pittsburgh, Singapore, and Las Vegas), extracts a short planning context window (4–8 seconds) around each scene, and evaluates a planner's proposed trajectory using the recorded scene as a non-reactive world model. The planner cannot influence other agents (hence "non-reactive"), but it is evaluated on how well its proposed trajectory would have performed in the real world in terms of progress, safety margins, and comfort, using the PDM-Score.

The PDM-Score (PDMS) is a composite scalar aggregating five sub-metrics: (1) *Progress*: forward displacement normalized by expert progress; (2) *Comfort*: penalizing jerk, acceleration, and steering rate exceeding human-comfort thresholds; (3) *No-at-fault collision*: binary penalty for trajectories intersecting any recorded static or dynamic obstacle; (4) *Drivable area compliance*: penalty for trajectories leaving the drivable surface; and (5) *Time-to-collision (TTC)*: continuous penalty for approaching agents below a safety margin. The IDM-based PDM planner (which uses privileged map and agent information) achieves 88.0 PDMS on the navsim-v1 dataset. End-to-end camera-based models that perform strongly on nuScenes open-loop — e.g., UniAD-style architectures — score substantially lower (~70–75 PDMS), revealing the gap between L2-optimized policies and genuinely safe driving behavior. At the NeurIPS 2024 competition, over 150 teams competed, with top submissions reaching ~92 PDMS using trajectory ensembling and scene-specific optimization.

NAVSIM's primary methodological innovation is the non-reactive simulation design, which achieves a practical trade-off: unlike open-loop replay, PDMS evaluates planned trajectory quality on multiple dimensions; unlike closed-loop simulation, it requires no agent behavior model and runs in seconds per scenario rather than minutes. The PDMS metric is carefully calibrated so that sub-metrics are not independently optimizable — maximizing progress will violate comfort and TTC constraints, forcing genuine multi-objective optimization rather than metric gaming. The authors provide an open-source evaluation toolkit (navsim-devkit) and standardized splits, making the benchmark reproducible and adversarially robust. The dataset's geographic diversity (four cities, multiple weather conditions, varied road topologies) substantially exceeds nuScenes' Boston/Singapore coverage, challenging planners with a broader distribution of scenarios.

## Why It Matters

NAVSIM became the de facto standard benchmark for E2E planner evaluation in the 2024–2025 research cycle, filling the gap the community had long recognized between nuScenes open-loop metrics and expensive closed-loop nuPlan simulation. Its adoption as the official NeurIPS 2024 Autonomous Driving competition venue brought over 150 competing teams and produced a leaderboard now routinely cited alongside nuScenes in E2E driving papers. Several state-of-the-art methods — including SparseDrive variants and reinforcement-learning-based planners — used NAVSIM PDMS as their primary metric in 2024, and the benchmark's five-dimensional scoring decomposition became a standard reporting format. NAVSIM also influenced how researchers think about the open-loop vs. closed-loop evaluation trade-off, prompting nuPlan and Bench2Drive developers to adopt composite metrics with similar sub-dimension structure.

NAVSIM's non-reactive simulation design has an inherent limitation: because other agents do not respond to the ego planner's trajectory, unsafe trajectories that would have triggered evasive maneuvers by other drivers are evaluated against a world that ignores the ego action, allowing overly aggressive planners to appear safer than they are in deployment. The benchmark also inherits the sensor characteristics of the nuPlan/OpenScene collection hardware, which may not transfer to vehicles with different sensor configurations. The 4–8 second evaluation horizon is insufficient for long-horizon planning scenarios (highway lane changes, complex intersection negotiation) requiring multi-second lookahead beyond the replay window. Despite its geographic diversity, OpenScene's data is predominantly from North American and Singaporean structured environments, with limited coverage of unstructured rural roads or developing-world traffic patterns — a gap that will grow in importance as AD deployment expands globally.

| | |
|---|---|
| **Authors** | Dauner et al. |
| **Year** | 2024 |
| **Venue** | NeurIPS 2024 |
| **Field** | Autonomous Driving |
| **Subfield** | End To End Autonomous Driving |
| **Tasks** | benchmark, simulation, planning, evaluation |
| **Tier** | 3 — Benchmark / Resource |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2406.15349.pdf){: .btn .btn--primary .btn--large}
