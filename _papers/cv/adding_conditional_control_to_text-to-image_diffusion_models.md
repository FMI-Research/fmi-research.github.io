---
title: Adding Conditional Control to Text-to-Image Diffusion Models
collection: papers
permalink: /papers/cv/adding_conditional_control_to_text-to-image_diffusion_models/
date: '2023-02-10'
year: 2023
field: computer-vision
subfield: generative-vision
tasks:
- controllable-generation
- edges
- pose
- depth
tier: 2
artifact_type: paper
venue: ICCV 2023
authors:
- Lvmin Zhang
- Anyi Rao
- Maneesh Agrawala
authors_short: Zhang et al.
paperurl: /files/papers/adding_conditional_control_to_text-to-image_diffusion_models.pdf
doi: 10.1109/ICCV51070.2023.00929
license: unspecified
summary: ControlNet adds spatial conditioning to frozen pretrained text-to-image diffusion
  models by attaching a trainable copy of the UNet encoder connected via zero-initialized
  convolutions, enabling precise structural control from cues such as edges, depth
  maps, and human pose without altering original weights.
why_important: Became the standard framework for controllable diffusion generation
  by elegantly solving the weight-corruption problem through zero convolutions, and
  spawned a broad ecosystem of extensions covering video, 3D, and domain-specific
  control signals.
tags:
- controlnet
- controllable-generation
- diffusion
- conditioning
---

## Summary

Zhang et al. address a fundamental limitation of large pretrained text-to-image diffusion models: while they produce high-quality images, they offer little control over spatial structure, making it difficult to reliably specify object layout, human pose, or scene geometry through text prompts alone. ControlNet solves this by attaching a trainable auxiliary network to a frozen copy of the original model without modifying any original weights. Concretely, it creates a duplicate of the UNet encoder blocks (12 blocks in Stable Diffusion's UNet), connects these trainable copies to the original frozen decoder via *zero convolutions* — 1×1 convolutional layers initialized with both weights and biases set to zero — and injects conditioning signals (Canny edges, HED edges, depth maps from MiDaS, human pose from OpenPose, segmentation maps, normal maps, scribbles, M-LSD straight lines) through this auxiliary pathway. At initialization, zero convolutions ensure the auxiliary network contributes nothing to the output, so training starts from exactly the pretrained model's behavior and avoids catastrophic interference with learned representations.

During training, only the auxiliary encoder and zero convolution weights are updated; the original UNet remains frozen. This allows ControlNet to be trained on datasets as small as 50k–1M image-condition pairs on a single consumer GPU (e.g., RTX 3080) and typically converges in hours to a day. The zero convolution mechanism provides a particularly elegant solution to the gradient noise problem: because early in training the auxiliary signal is weak and the zero convolutions suppress it, the original model's rich pretrained features are preserved through the critical early training phase. Once the auxiliary network begins to learn, the zero convolutions open up progressively, injecting a growing conditioning signal in a curriculum-like fashion.

Quantitative and qualitative evaluation demonstrates that ControlNet dramatically outperforms competing controllability approaches — including textual inversion, LoRA-based conditioning, and direct fine-tuning — on spatial and structural control metrics. Human preference studies show a strong preference for ControlNet outputs when prompts specify precise structural arrangements. The authors further show that multiple ControlNets can be composed at inference time (e.g., simultaneously conditioning on pose and depth) by summing their zero-convolution outputs, providing modular and additive control.

## Why It Matters

ControlNet solved one of the most practically important gaps in the open text-to-image ecosystem: how to add precise spatial control to a pretrained generative model without expensive full retraining. Its release in early 2023 triggered immediate, widespread adoption in creative tools and research workflows, and the zero-convolution architecture became a template for subsequent parameter-efficient adaptation methods across diffusion models. Within months of publication, ControlNet variants had been extended to video generation (ControlVideo), 3D generation, medical image synthesis, and domain-specific industrial applications.

The zero-convolution insight is methodologically significant beyond ControlNet itself: it provides a principled solution to the problem of injecting new information into a pretrained model without early-training gradient corruption. This idea has connections to LoRA (which freezes and adds low-rank perturbations) and adapter methods from NLP, but differs in that zero convolutions operate as learned gates rather than additive perturbations, giving the model explicit control over when to begin incorporating the new signal. A current limitation is that training a ControlNet requires paired data (image, condition-map), which is available for geometric signals like edges and depth but harder to obtain for semantic or high-level structural conditions, constraining the types of control that can be easily added.

| | |
|---|---|
| **Authors** | Zhang et al. |
| **Year** | 2023 |
| **Venue** | ICCV 2023 |
| **Field** | Computer Vision |
| **Subfield** | Generative Vision |
| **Tasks** | controllable-generation, edges, pose, depth |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](/files/papers/adding_conditional_control_to_text-to-image_diffusion_models.pdf){: .btn .btn--primary .btn--large}
