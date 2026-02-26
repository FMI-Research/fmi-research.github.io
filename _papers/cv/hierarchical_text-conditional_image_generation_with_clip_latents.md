---
title: Hierarchical Text-Conditional Image Generation with CLIP Latents
collection: papers
permalink: /papers/cv/hierarchical_text-conditional_image_generation_with_clip_latents/
date: '2022-04-13'
year: 2022
field: computer-vision
subfield: generative-vision
tasks:
- text-to-image
- clip-latents
- generation
tier: 1
artifact_type: paper
venue: arXiv 2022
authors:
- Aditya Ramesh
- Prafulla Dhariwal
- Alex Nichol
- Casey Chu
authors_short: Ramesh et al.
paperurl: https://arxiv.org/pdf/2204.06125.pdf
doi: 10.48550/arXiv.2204.06125
license: unspecified
summary: DALL-E 2 (unCLIP) introduces a hierarchical two-stage pipeline that first
  maps CLIP text embeddings to CLIP image embeddings via a diffusion prior, then decodes
  images from those embeddings, enabling composable CLIP-space operations such as
  image variation and interpolation.
why_important: Demonstrates that CLIP's embedding space encodes rich visual semantics
  sufficient for high-quality generation, while also revealing compositionality limitations
  that motivated subsequent approaches using pure language model encoders.
tags:
- dalle
- text-to-image
- clip
- generation
- hierarchical
---

## Summary

Ramesh et al. introduce DALL-E 2 (also called unCLIP), which reframes text-to-image generation as a two-stage hierarchical problem in CLIP embedding space. In the first stage, a *prior* model maps a CLIP text embedding to the corresponding CLIP image embedding — either via an autoregressive transformer over discretized embeddings or a diffusion model over continuous embeddings, with the latter found to perform marginally better. In the second stage, a *decoder* (a modified GLIDE diffusion model) generates a 64×64 image conditioned on the predicted CLIP image embedding and projected CLIP text embeddings, then upsamples it through cascaded super-resolution stages to 256×256 and 1024×1024. The prior is critical: directly conditioning the decoder on text embeddings produces lower-fidelity results than routing through the CLIP image embedding, which encodes richer, more visual semantic structure.

A distinctive methodological contribution is what the CLIP embedding space affords beyond generation. Because CLIP image embeddings are geometrically structured, encoding a real image and re-decoding from the same embedding with different noise yields *image variations* that preserve semantic content while changing low-level details. Linear interpolation between two image embeddings produces smooth morphs. Text-driven image editing is possible by subtracting one CLIP text embedding from another and adding the difference to the image embedding — a CLIP analogue of word vector arithmetic. These operations make DALL-E 2 not just a text-to-image model but a composable CLIP-space generative engine. On MS-COCO zero-shot generation, DALL-E 2 achieves an FID of 10.39, competitive with contemporaries on photorealism and diversity in human evaluations.

The paper also provides a careful analysis of failure modes, most notably the model's difficulty with compositional prompts such as "a red cube on top of a blue sphere." CLIP's training objective is global image-text matching, which does not strongly penalize attribute misassignment between objects. This failure mode is reproducible and systematic, motivating the use of alternative text representations (such as T5 in Imagen) that have stronger structural language understanding.

## Why It Matters

DALL-E 2 established the viability of using CLIP's embedding space as an intermediate latent for generative modeling, demonstrating that a contrastive representation trained without any explicit generation objective could nonetheless serve as a powerful bridge between language and images. This insight influenced a generation of CLIP-conditioned models and editing methods, and the image variation and interpolation capabilities it demonstrated remain among the most intuitively compelling demonstrations of what a well-structured vision-language embedding space can do.

The compositionality limitation documented in the paper proved highly influential for subsequent research. It directly motivated Imagen's T5 encoder design and prompted a broader rethinking of how text representations for generation should be trained, ultimately contributing to the shift toward large language model encoders (T5, Flan-T5, eventually full LLM backbones) in frontier text-to-image systems. The two-stage prior-decoder framework also foreshadowed later work on embedding-space generation (e.g., masked image modeling with diffusion), where generating in a semantic embedding space before decoding to pixels has become an increasingly attractive design pattern.

| | |
|---|---|
| **Authors** | Ramesh et al. |
| **Year** | 2022 |
| **Venue** | arXiv 2022 |
| **Field** | Computer Vision |
| **Subfield** | Generative Vision |
| **Tasks** | text-to-image, clip-latents, generation |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2204.06125.pdf){: .btn .btn--primary .btn--large}
