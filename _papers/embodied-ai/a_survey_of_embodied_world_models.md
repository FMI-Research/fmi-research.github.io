---
title: A Survey of Embodied World Models
collection: papers
permalink: /papers/embodied-ai/a_survey_of_embodied_world_models/
date: '2025-01-15'
year: 2025
field: embodied-ai
subfield: embodied-agents-benchmarks-world-models
tasks:
- world-models
- survey
- generative-models
- planning
- sim2real
tier: 2
artifact_type: paper
venue: arXiv 2025
authors:
- Shang et al.
authors_short: Shang et al.
paperurl: https://fi.ee.tsinghua.edu.cn/public/publications/0940dda4-af15-11f0-9d60-0242ac120002.pdf
doi: ''
license: unspecified
summary: Systematic 2025 survey classifying embodied world models by functional role
  — environment simulator, policy training ground, and planning module — spanning
  latent-space, video prediction, and large generative approaches.
why_important: Arrives at the convergence of generative AI and robot learning, offering
  a functional taxonomy that helps practitioners choose architectures and surfaces
  the open problems — long-horizon fidelity, language conditioning, sim-to-real transfer
  — that define the frontier.
tags:
- world-models
- survey
- embodied-ai
- generative
- planning
---

## Summary

This 2025 survey by Shang et al. provides the most systematic mapping to date of world models as they apply to embodied AI — a distinct and more demanding setting than the standard model-based RL context in which world models were originally developed. The core observation motivating the survey is that embodied agents must predict the *physical consequences* of actions in high-dimensional, partially observable, and causally structured environments, requirements that stress-test assumptions underlying earlier world model designs. The survey spans three generations of approaches: compact **latent-space world models** (the Dreamer/RSSM family) that learn compressed dynamics representations enabling fast imagination-based planning; **video prediction models** (UniSim, IRASim, Genie, GROOT) that operate in pixel space and can function as interactive neural environment simulators; and **large generative world models** built on diffusion transformers or autoregressive architectures pretrained on internet-scale video, which can synthesize physically plausible future observations conditioned on action sequences at high visual fidelity.

The survey's central organizational contribution is a **functional taxonomy** that classifies world models not by architecture but by their role within an embodied system: as *environment simulators* (replacing or augmenting physical rollouts for policy training), as *policy training grounds* (generating synthetic experience for offline or online RL), and as *planning modules* (enabling model-predictive control or MCTS-style search in latent or pixel space). This tripartite framing clarifies which architectural choices — observation space dimensionality, action-conditioning mechanism, temporal prediction horizon, training objective — are most consequential for each use case. A latent-space model optimized for planning speed is the right tool for certain MPC applications; a high-fidelity video diffusion model is appropriate for generating synthetic training data but too slow for closed-loop inference.

The survey also addresses evaluation methodology in detail, noting that world models for embodied AI have historically been assessed on visual reconstruction quality (FID, PSNR) even when their downstream purpose is action-conditioned prediction accuracy or policy improvement. The authors survey emerging action-conditioned benchmarks and propose a standardized evaluation protocol that disentangles perceptual fidelity from behavioral fidelity — a methodological gap whose closing will be essential for rigorous comparison across architectural families. The treatment of sim-to-real aspects of world models, including physical constraint satisfaction and contact dynamics in video generation, is particularly thorough and forward-looking.

## Why It Matters

As foundation models become standard backbones for embodied policies (RT-2, π0, OpenVLA, RDT-1B), the capacity to predict consequences of actions in rich observation spaces has become a first-class component of embodied AI systems rather than an auxiliary module. This survey arrives precisely at the moment when the generative AI and robot learning communities are converging — video generation researchers and robot learning researchers are increasingly working on the same problems from different angles — and provides a structured entry point into a literature that simultaneously spans model-based RL, video generation, and large-scale pretraining. For practitioners, the functional taxonomy is immediately useful for navigating a rapidly bifurcating space: whether to use a compact RSSM for online planning, a pretrained video diffusion model for data augmentation, or a large generative backbone as an environment simulator for policy training are decisions with very different cost/quality tradeoffs that the survey helps make explicit.

The survey also surfaces the open problems that define the current frontier. Long-horizon physical plausibility — maintaining consistent object states, contact geometry, and rigid-body dynamics across many predicted frames — remains unsolved for pixel-space models at practical resolutions. Language conditioning of world models (enabling a researcher to specify "pick up the red mug and place it in the drawer" as a goal for imagination-based planning) is in early stages. And the central open question — whether world model pretraining on internet video can provide a meaningful initialization for robot manipulation policies through a kind of "embodied pretraining" — is being actively contested by multiple research groups as of 2025. This survey is the reference text for understanding where that question came from and what the current candidate answers look like.

| | |
|---|---|
| **Authors** | Shang et al. |
| **Year** | 2025 |
| **Venue** | arXiv 2025 |
| **Field** | Embodied Ai |
| **Subfield** | Embodied Agents Benchmarks World Models |
| **Tasks** | world-models, survey, generative-models, planning, sim2real |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://fi.ee.tsinghua.edu.cn/public/publications/0940dda4-af15-11f0-9d60-0242ac120002.pdf){: .btn .btn--primary .btn--large}
