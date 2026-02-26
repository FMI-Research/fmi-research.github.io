---
title: 'Imagen Video: High Definition Video Generation with Diffusion Models'
collection: papers
permalink: /papers/cv/imagen_video_high_definition_video_generation_with_diffusion_models/
date: '2022-10-05'
year: 2022
field: computer-vision
subfield: generative-vision
tasks:
- text-to-video
- video-diffusion
- cascade
tier: 2
artifact_type: paper
venue: arXiv 2022
authors:
- Jonathan Ho
- William Chan
- Chitwan Saharia
- Jay Whang
authors_short: Ho et al.
paperurl: https://arxiv.org/pdf/2210.02303.pdf
doi: 10.48550/arXiv.2210.02303
license: unspecified
summary: Imagen Video generates high-definition 1280×768 video at 24 FPS through a
  cascade of seven diffusion models combining temporal attention, 3D convolutions,
  and progressive spatial super-resolution, conditioned on text via classifier-free
  guidance.
why_important: Imagen Video established cascaded video diffusion as a viable path
  to high-definition, temporally consistent text-to-video synthesis, providing a canonical
  architectural blueprint that informed subsequent survey taxonomies and industrial
  video generation pipelines.
tags:
- text-to-video
- video-diffusion
- cascade
- temporal-consistency
---

## Summary

Imagen Video generates high-definition 1280×768 video at 24 FPS using a cascade of seven diffusion models. The pipeline begins with a 16-frame, 40×24 keyframe model conditioned on text via classifier-free guidance, then passes outputs through a temporal super-resolution model that densifies the frame sequence from 16 to 128 frames, followed by a series of five spatial super-resolution stages that progressively upscale resolution up to the final 1280×768 output. Each model in the cascade is a video-conditioned UNet extended with temporal attention layers (applied across the time dimension of feature maps) and 3D convolutions (factored into separate spatial and temporal components), enabling the models to capture both local appearance and global temporal dynamics without quadratic attention cost over full video sequences.

All cascade stages are trained jointly on video-text pairs using v-parameterization, a reparameterization of the diffusion denoising target that improves numerical stability at low noise levels—particularly important for high-resolution video frames where small errors accumulate. Some stages also use progressive distillation to reduce the number of denoising steps required at inference, improving throughput. Training uses a curated video-text dataset with aggressive data filtering for quality and text alignment.

Human evaluation studies show that Imagen Video is preferred over Make-A-Video and CogVideo on both visual quality and text alignment metrics. The model produces high temporal consistency (objects and scenes do not flicker between frames) and captures fine visual details at the full output resolution. The architectural choices—cascaded temporal and spatial upsampling, factored space-time attention, v-parameterization—became reference design decisions for subsequent high-definition video generation systems.

## Why It Matters

Imagen Video is significant not only for its output quality but for demonstrating that the design principles proven in image diffusion cascades (Dall-E 2, Imagen) transfer cleanly to the video domain when augmented with temporal modeling components. The cascaded design decouples the challenges of temporal coherence (handled at low resolution by the base and temporal SR models) from photorealistic appearance (handled by high-resolution spatial SR models), making the training more tractable and the failure modes more interpretable. This decomposition influenced subsequent cascaded video systems and is reflected in the architectural taxonomy of the video diffusion survey literature.

A notable limitation is that Imagen Video, like most large-scale video generation systems of its era, was not publicly released; access was restricted, limiting reproducibility and downstream research use. The v-parameterization and progressive distillation techniques introduced in Imagen Video, however, were adopted more broadly and are now standard components in video diffusion training. The system also highlights the engineering challenge of video generation at scale: training and serving a cascade of seven models requires substantial infrastructure that remains a barrier for academic researchers.

| | |
|---|---|
| **Authors** | Ho et al. |
| **Year** | 2022 |
| **Venue** | arXiv 2022 |
| **Field** | Computer Vision |
| **Subfield** | Generative Vision |
| **Tasks** | text-to-video, video-diffusion, cascade |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2210.02303.pdf){: .btn .btn--primary .btn--large}
