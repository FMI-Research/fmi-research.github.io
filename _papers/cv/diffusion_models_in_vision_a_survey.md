---
title: 'Diffusion Models in Vision: A Survey'
collection: papers
permalink: /papers/cv/diffusion_models_in_vision_a_survey/
date: '2022-09-10'
year: 2022
field: computer-vision
subfield: generative-vision
tasks:
- survey
- diffusion-models
- generation
tier: 1
artifact_type: paper
venue: arXiv / IEEE TPAMI 2024
authors:
- Florinel-Alin Croitoru
- Vlad Hondru
- Radu Tudor Ionescu
- Mubarak Shah
authors_short: Croitoru et al.
paperurl: https://arxiv.org/pdf/2209.04747.pdf
doi: 10.48550/arXiv.2209.04747
license: unspecified
summary: A comprehensive survey unifying denoising diffusion probabilistic models,
  score-based generative models, and their continuous-time SDE formulations, with
  coverage of efficient sampling, improved likelihood training, conditional generation,
  and applications across vision and beyond.
why_important: Captures diffusion models at a critical inflection point when they
  surpassed GANs on FID metrics, providing the taxonomic framework and unified theory
  that subsequent work builds upon.
tags:
- survey
- diffusion
- generation
- vision
---

## Summary

Cao et al. (2022) present a comprehensive survey of diffusion-based generative models, systematically unifying three major formulations under a common framework: denoising diffusion probabilistic models (DDPM), which define a discrete Markov chain that gradually corrupts data with Gaussian noise and learns to reverse it; score-based generative models (NCSN) trained with denoising score matching to estimate the gradient of the data log-density; and the continuous-time SDE framework of Song et al. (2020), which subsumes both as special discretizations of a single stochastic differential equation. This unified perspective clarifies that DDPM's VP-SDE and NCSN's VE-SDE are complementary parameterizations of the same underlying process, making the zoo of diffusion methods far more coherent.

The survey organizes the methodological landscape into three principal axes. First, *efficient sampling* methods that reduce the typically 1000-step DDPM generation to tens of steps (DDIM via deterministic trajectories, DPM-Solver via high-order ODE solvers, Analytic-DPM via analytically optimal step sizes). Second, *improved likelihood and training stability* approaches such as IDDPM (learned noise schedules, cosine schedule), VDM (variational formulation with learned encoder noise), and EDM (normalizing the training objective and noise schedule for improved conditioning). Third, *conditional generation* mechanisms including classifier guidance (perturbing score with classifier gradients), classifier-free guidance (jointly training conditional and unconditional models), and text conditioning via CLIP or large language models. The survey also draws explicit connections between diffusion models and normalizing flows, VAEs, and energy-based models.

Applications covered span image synthesis, super-resolution, inpainting, semantic segmentation, video generation, 3D shape and NeRF generation, molecular design, and time-series modeling. The survey was written at a critical inflection point in 2022 when diffusion models had demonstrably surpassed GANs on standard FID benchmarks across multiple datasets, a shift it carefully documents with empirical comparisons across CIFAR-10, CelebA-HQ, LSUN, and ImageNet.

## Why It Matters

This survey crystallizes the theoretical convergence of what had previously appeared as disparate threads — probabilistic graphical models, score matching, stochastic differential equations — into a single coherent story, giving researchers a shared vocabulary and reference point. Its taxonomic organization of sampling methods, likelihood objectives, and conditioning mechanisms provided the structural skeleton for a generation of follow-on work, making it the most-cited diffusion survey of its period. The unified SDE view in particular has proven prescient, as subsequent models (consistency models, flow matching) are most naturally understood as modifications of the continuous-time SDE framework it explicates.

A noted limitation is that the survey, like all surveys, reflects the state of the field at snapshot time: techniques such as flow matching (Lipman et al., 2022), consistency distillation (Song et al., 2023), and diffusion transformers (Peebles & Xie, 2023) postdate its coverage. Nonetheless, the conceptual scaffolding it provides remains the standard entry point for practitioners and researchers new to diffusion-based generation.

| | |
|---|---|
| **Authors** | Croitoru et al. |
| **Year** | 2022 |
| **Venue** | arXiv / IEEE TPAMI 2024 |
| **Field** | Computer Vision |
| **Subfield** | Generative Vision |
| **Tasks** | survey, diffusion-models, generation |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2209.04747.pdf){: .btn .btn--primary .btn--large}
