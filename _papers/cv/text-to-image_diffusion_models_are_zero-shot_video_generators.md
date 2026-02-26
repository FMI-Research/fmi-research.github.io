---
title: Text-to-Image Diffusion Models are Zero-Shot Video Generators
collection: papers
permalink: /papers/cv/text-to-image_diffusion_models_are_zero-shot_video_generators/
date: '2023-03-23'
year: 2023
field: computer-vision
subfield: generative-vision
tasks:
- text-to-video
- zero-shot
- video-generation
tier: 2
artifact_type: paper
venue: arXiv / ICCV 2023
authors:
- Levon Khachatryan
- Andranik Movsisyan
- Vahram Tadevosyan
- Roberto Henschel
authors_short: Khachatryan et al.
paperurl: https://arxiv.org/pdf/2303.13439.pdf
doi: 10.48550/arXiv.2303.13439
license: unspecified
summary: Text2Video-Zero generates temporally consistent videos from text prompts
  at inference time only, by injecting latent motion dynamics and redirecting self-attention
  keys and values to the first frame within a frozen Stable Diffusion model.
why_important: Text2Video-Zero demonstrated that temporal consistency in video generation
  can emerge from structural modifications to image diffusion attention—without any
  video training—establishing a key zero-shot paradigm that revealed how much video
  generation capacity is latent in image foundation models.
tags:
- text-to-video
- zero-shot
- diffusion
- video-generation
---

## Summary

Text2Video-Zero generates temporally consistent videos from text prompts using a completely frozen Stable Diffusion model, with no video training data and no fine-tuning of any kind. The method introduces two inference-time modifications. First, motion dynamics are simulated by applying a global translation to the initial latent noise codes across frames—effectively warping the starting noise in a manner that induces smooth camera-like motion in the output. Second, cross-frame attention consistency is enforced by replacing the keys and values in each frame's self-attention layers with those computed from the first frame, ensuring that all frames attend to a shared reference appearance and thus maintain consistent subject identity and style throughout the sequence.

These two modifications are composable with existing Stable Diffusion conditioning mechanisms: ControlNet inputs (pose skeletons, depth maps, Canny edges) can be fed per-frame to achieve controlled motion, and video-to-video translation is supported by replacing the input noise with DDIM-inverted latents from a source video. The entire pipeline adds negligible compute overhead relative to standard Stable Diffusion inference, as no additional parameters are introduced.

On CLIP-based text-video alignment scores evaluated on MSR-VTT and custom prompt sets, Text2Video-Zero achieves performance competitive with Make-A-Video and CogVideo—both of which require extensive video training—while operating with zero video data. The primary limitation is that the motion dynamics module relies on a fixed global translation heuristic, which cannot model non-rigid or complex motion patterns. Despite this, the method demonstrates that a substantial fraction of the temporal coherence needed for video generation is already encoded in the attention geometry of image foundation models.

## Why It Matters

Text2Video-Zero occupies an important position in the video generation landscape because it demonstrated—concisely and convincingly—that temporal consistency is not exclusively a property of models trained on video data. The cross-frame attention mechanism it introduced (routing all frames' attention to the first frame's keys and values) became an influential design pattern, adopted and extended in subsequent training-free video editing methods such as FateZero and TokenFlow, which use similar attention manipulation to propagate edits consistently across frames.

The method also has practical significance: it enables video generation on any hardware capable of running Stable Diffusion inference, with no additional GPU memory or training time overhead. Its main limitation—that global latent translation is a poor proxy for real camera motion—has motivated follow-up work on more principled optical-flow-guided latent manipulation and camera-conditioned video generation. Text2Video-Zero thus serves both as a strong zero-shot baseline and as a conceptual proof that the attention mechanisms of image models implicitly encode spatial-temporal structure exploitable for video synthesis.

| | |
|---|---|
| **Authors** | Khachatryan et al. |
| **Year** | 2023 |
| **Venue** | arXiv / ICCV 2023 |
| **Field** | Computer Vision |
| **Subfield** | Generative Vision |
| **Tasks** | text-to-video, zero-shot, video-generation |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2303.13439.pdf){: .btn .btn--primary .btn--large}
