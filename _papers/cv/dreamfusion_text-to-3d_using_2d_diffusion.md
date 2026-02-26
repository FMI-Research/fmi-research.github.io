---
title: 'DreamFusion: Text-to-3D using 2D Diffusion'
collection: papers
permalink: /papers/cv/dreamfusion_text-to-3d_using_2d_diffusion/
date: '2022-09-29'
year: 2022
field: computer-vision
subfield: generative-vision
tasks:
- text-to-3d
- score-distillation
- nerf
tier: 2
artifact_type: paper
venue: arXiv / ICLR 2023
authors:
- Ben Poole
- Ajay Jain
- Jonathan T. Barron
- Ben Mildenhall
authors_short: Poole et al.
paperurl: https://arxiv.org/pdf/2209.14988.pdf
doi: 10.48550/arXiv.2209.14988
license: unspecified
summary: DreamFusion introduces Score Distillation Sampling (SDS) to optimize a NeRF
  representation using gradients from a pretrained 2D text-to-image diffusion model,
  enabling text-to-3D generation without any 3D training data.
why_important: SDS established the dominant paradigm for 3D generative modeling by
  bridging 2D diffusion priors and differentiable 3D rendering, directly inspiring
  Magic3D, Fantasia3D, ProlificDreamer, and dozens of subsequent works.
tags:
- text-to-3d
- dreamfusion
- score-distillation
- nerf
- diffusion
---

## Summary

DreamFusion addresses the challenge of text-to-3D generation by eliminating the need for 3D training data entirely. The core technical contribution is Score Distillation Sampling (SDS), a method that uses the score function of a pretrained 2D diffusion model (specifically Imagen) as a differentiable loss signal to optimize a Neural Radiance Field (NeRF). At each optimization step, the NeRF is rendered from a randomly sampled camera viewpoint, Gaussian noise is added to the rendering at a random noise level, and the diffusion model's score function is queried to estimate the direction in image space that increases the probability under the text-conditioned distribution. This gradient is then backpropagated through the differentiable renderer to update the NeRF parameters directly. The SDS objective is derived from the evidence lower bound of the diffusion model's log-likelihood, ensuring that the NeRF's renderings are driven toward high-probability regions of the 2D distribution from every viewpoint simultaneously.

Because the optimization is view-agnostic and relies solely on the 2D prior, DreamFusion requires no 3D supervision, no 3D datasets, and no multi-view consistency loss—only a pretrained text-to-image diffusion model and a differentiable renderer. The NeRF representation used is a shaded, geometry-aware variant with albedo, normals, and ambient occlusion, which helps produce surfaces rather than volumetric fog. Training a single object-level NeRF takes roughly 1.5 hours on a TPU.

Results demonstrate coherent 3D objects from diverse text prompts that look plausible from all viewpoints, a nontrivial achievement given the lack of 3D supervision. However, the method has a well-documented failure mode: SDS loss tends to produce over-smoothed, "plastic-looking" geometry with limited high-frequency texture detail, a consequence of the loss averaging over the score function at multiple noise levels. Evaluation is primarily qualitative, as no standardized 3D generation benchmark existed at the time of publication.

## Why It Matters

DreamFusion's most lasting contribution is not the specific NeRF architecture or the choice of Imagen as the diffusion prior, but the SDS algorithm itself. SDS generalizes immediately to any differentiable 3D representation and any pretrained diffusion model, making it a modular and reusable primitive. Within months of publication, SDS was incorporated into Magic3D (which uses an accelerated representation for higher-resolution geometry), Fantasia3D (which disentangles geometry and appearance optimization), DreamBooth3D (which personalizes SDS with a few reference images), and Zero-1-to-3 (which conditions a diffusion model on a single view for novel-view synthesis). ProlificDreamer later diagnosed and partially addressed the over-saturation and over-smoothing artifacts of SDS by introducing variational score distillation (VSD), which replaces the single-point score estimate with a distribution over NeRF parameters.

The work also crystallized a broader research agenda: how to leverage the rich statistical knowledge embedded in large 2D generative models to supervise 3D optimization problems where ground-truth 3D data is scarce or nonexistent. This agenda has since expanded to mesh generation, 4D generation, and motion synthesis, all using variants of score distillation as the core loss signal.

| | |
|---|---|
| **Authors** | Poole et al. |
| **Year** | 2022 |
| **Venue** | arXiv / ICLR 2023 |
| **Field** | Computer Vision |
| **Subfield** | Generative Vision |
| **Tasks** | text-to-3d, score-distillation, nerf |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2209.14988.pdf){: .btn .btn--primary .btn--large}
