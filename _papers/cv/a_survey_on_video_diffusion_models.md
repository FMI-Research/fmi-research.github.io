---
title: A Survey on Video Diffusion Models
collection: papers
permalink: /papers/cv/a_survey_on_video_diffusion_models/
date: '2024-01-08'
year: 2024
field: computer-vision
subfield: generative-vision
tasks:
- survey
- video-diffusion
- generation
tier: 1
artifact_type: paper
venue: ACM Computing Surveys 2024
authors:
- Zhen Xing
- Qijun Feng
- Haoran Chen
- Qi Dai
authors_short: Xing et al.
paperurl: https://arxiv.org/pdf/2310.10647.pdf
doi: 10.1145/3696415
license: unspecified
summary: This comprehensive survey taxonomizes 50+ video diffusion models as of early
  2024 across three axes—architecture (UNet, DiT, autoregressive hybrids), training
  paradigm (text-to-video, editing, prediction), and application domain—while cataloguing
  temporal modeling strategies and open challenges.
why_important: By providing a unified taxonomy of architectures, temporal modeling
  approaches, evaluation metrics (FVD, CLIPSIM), and open challenges (scalability,
  controllability, real-time generation), this survey serves as an essential orientation
  map for researchers entering or navigating the rapidly evolving video diffusion
  landscape.
tags:
- survey
- video-diffusion
- generation
- video
---

## Summary

This survey provides a structured overview of the video diffusion model landscape as of early 2024, organizing 50+ papers along three primary axes. Architecturally, it distinguishes UNet-based models (Make-A-Video, Imagen Video, ModelScopeT2V) that extend image UNets with temporal attention layers or 3D convolutions; Diffusion Transformer (DiT)-based models (Open-Sora) that apply attention over spatial and temporal patches jointly; and autoregressive-diffusion hybrids that combine token-level autoregressive generation with diffusion-based refinement. The survey systematically characterizes the temporal modeling strategies each architecture employs: temporal self-attention layers inserted between spatial blocks, factored space-time attention, full 3D attention, and causal video transformers designed for streaming generation.

Training paradigms covered include text-to-video generation (Make-A-Video, Imagen Video, Show-1), image-to-video generation (Stable Video Diffusion), video prediction, and video editing (Tune-A-Video, FateZero, TokenFlow). The survey also covers extended application domains: 4D generation, driving video synthesis, and human motion generation. Evaluation methodology is discussed in detail, with analysis of FVD (Fréchet Video Distance), CLIPSIM (text-video alignment), and Inception Score as the primary quantitative benchmarks, alongside their known limitations for measuring temporal consistency and motion quality.

Open challenges identified include: scaling video diffusion models to long sequences without prohibitive memory cost, achieving real-time or near-real-time inference, improving fine-grained controllability over motion trajectories and object interactions, and developing evaluation metrics that better capture temporal dynamics. The survey's taxonomy provides a practical reference for situating new contributions within the existing literature and identifying underexplored directions.

## Why It Matters

Surveys of this kind serve a distinct scientific function beyond cataloguing existing work: by imposing a consistent taxonomy on a fragmented literature, they reveal which combinations of architectural choices and training paradigms have been thoroughly explored and which remain underexplored. The video diffusion survey's identification of gaps—such as the limited work on real-time video diffusion, the absence of standardized long-video benchmarks, and the underexploration of physics-constrained video generation—has practical value for researchers choosing research directions.

The survey's coverage of evaluation metrics is particularly useful, as the video generation community has not converged on a single gold-standard benchmark. The critique of FVD's sensitivity to dataset statistics and CLIPSIM's inability to measure motion quality provides grounding for understanding why quantitative results across papers are often incomparable. As video diffusion continues to evolve rapidly—with DiT-based video models (Sora, Open-Sora) and autoregressive video transformers emerging after the survey's cutoff—the architectural taxonomy it establishes provides a durable reference frame for situating new work.

| | |
|---|---|
| **Authors** | Xing et al. |
| **Year** | 2024 |
| **Venue** | ACM Computing Surveys 2024 |
| **Field** | Computer Vision |
| **Subfield** | Generative Vision |
| **Tasks** | survey, video-diffusion, generation |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2310.10647.pdf){: .btn .btn--primary .btn--large}
