---
title: High-Resolution Image Synthesis with Latent Diffusion Models
collection: papers
permalink: /papers/cv/high-resolution_image_synthesis_with_latent_diffusion_models/
date: '2022-06-01'
year: 2022
field: computer-vision
subfield: generative-vision
tasks:
- text-to-image
- latent-diffusion
- generation
tier: 1
artifact_type: paper
venue: CVPR 2022
authors:
- Robin Rombach
- Andreas Blattmann
- Dominik Lorenz
- Patrick Esser
authors_short: Rombach et al.
paperurl: https://openaccess.thecvf.com/content/CVPR2022/papers/Rombach_High-Resolution_Image_Synthesis_With_Latent_Diffusion_Models_CVPR_2022_paper.pdf
doi: 10.1109/CVPR52688.2022.01042
license: unspecified
summary: Latent Diffusion Models decouple perceptual compression from semantic generation
  by running the diffusion process in the latent space of a pretrained autoencoder,
  achieving pixel-space diffusion quality at a fraction of the computational cost.
why_important: LDMs are the direct technical foundation of Stable Diffusion, democratizing
  high-resolution generative modeling and enabling the explosion of open-source text-to-image
  tooling.
tags:
- latent-diffusion
- stable-diffusion
- text-to-image
- generation
---

## Summary

Rombach et al. introduce Latent Diffusion Models (LDMs), which address the prohibitive computational cost of pixel-space diffusion by cleanly separating two concerns: *perceptual compression* and *semantic generation*. A VQ-regularized or KL-regularized convolutional autoencoder is first trained to compress images into a spatially downsampled latent space (4× or 8× reduction per spatial dimension). The diffusion model is then trained entirely within this compact latent space, and a decoder maps generated latents back to full-resolution pixels. This decomposition is not merely a computational trick — the authors argue that the majority of image information is perceptual redundancy that the autoencoder handles, while the diffusion model can devote all its capacity to the semantically meaningful variation in the latent space.

The architecture uses a UNet backbone operating on latents, augmented with cross-attention layers that enable flexible, modality-agnostic conditioning. Text conditioning is implemented by projecting BERT or CLIP text embeddings through learned key/value projections into every cross-attention layer of the UNet, making the model naturally attend to text at multiple resolutions. This design accommodates class labels, segmentation maps, layout information, or other spatially structured conditions without architectural changes. Empirically, LDMs achieve an FID of 1.45 on CelebA-HQ 256×256 and competitive results on FFHQ, LSUN-Bedrooms, and LSUN-Churches — matching or surpassing prior pixel-space diffusion models and GANs — while requiring substantially less GPU memory and training compute than contemporaries like GLIDE or DALL-E 1.

A key methodological insight is that the optimal compression rate is task-dependent: too little compression and the diffusion model still wastes capacity on pixel-level details; too much and the autoencoder loses semantically important structure. The paper maps out this tradeoff empirically across different downsampling factors. The publicly released weights, fine-tuned with CLIP text conditioning by CompVis and subsequently Stability AI, became Stable Diffusion 1.x — the first openly available high-quality text-to-image model, which democratized generative image research and application.

## Why It Matters

LDMs resolve the accessibility problem that plagued pixel-space diffusion models: training GLIDE or similar models required hundreds of A100-GPU-days and inference was slow, placing frontier generative modeling exclusively in the hands of large research labs. By shifting diffusion to latent space, LDMs enabled training on consumer-grade clusters and inference on single GPUs, which directly led to Stable Diffusion's open release and the subsequent proliferation of community fine-tunes, ControlNet adapters, LoRA modules, and editing tools built on top of the SD backbone.

The cross-attention conditioning mechanism introduced here also became the dominant paradigm for all subsequent conditional diffusion architectures. Nearly every major text-to-image model released after 2022 — whether built on LDMs directly or not — uses cross-attention for conditioning, testifying to the architectural correctness of the design. A limitation worth noting is that latent-space generation introduces an inversion gap: editing real images requires an encoder pass (or DDIM inversion) that may not perfectly reconstruct fine details, a challenge that motivated follow-on work on null-text inversion and exact DDIM inversion.

| | |
|---|---|
| **Authors** | Rombach et al. |
| **Year** | 2022 |
| **Venue** | CVPR 2022 |
| **Field** | Computer Vision |
| **Subfield** | Generative Vision |
| **Tasks** | text-to-image, latent-diffusion, generation |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://openaccess.thecvf.com/content/CVPR2022/papers/Rombach_High-Resolution_Image_Synthesis_With_Latent_Diffusion_Models_CVPR_2022_paper.pdf){: .btn .btn--primary .btn--large}
