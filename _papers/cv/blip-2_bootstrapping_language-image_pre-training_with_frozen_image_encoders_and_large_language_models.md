---
title: 'BLIP-2: Bootstrapping Language-Image Pre-training with Frozen Image Encoders
  and Large Language Models'
collection: papers
permalink: /papers/cv/blip-2_bootstrapping_language-image_pre-training_with_frozen_image_encoders_and_large_language_models/
date: '2023-01-30'
year: 2023
field: computer-vision
subfield: open-world-perception
tasks:
- vlm
- multimodal
- bridge-module
tier: 2
artifact_type: paper
venue: arXiv / ICML 2023
authors:
- Junnan Li
- Dongxu Li
- Silvio Savarese
- Steven Hoi
authors_short: Li et al.
paperurl: https://arxiv.org/pdf/2301.12597.pdf
doi: 10.48550/arXiv.2301.12597
license: unspecified
summary: BLIP-2 introduces Q-Former—a lightweight querying transformer with learned
  tokens that bridges a frozen image encoder and a frozen LLM through two-stage pretraining—
  achieving state-of-the-art VQA and captioning with a fraction of trainable parameters.
why_important: Q-Former's design of compressing visual information into a small fixed
  set of query tokens became the canonical bridge-module pattern, directly inspiring
  InstructBLIP, MiniGPT-4, and LLaVA and shaping how the field connects vision encoders
  to language models.
tags:
- vlm
- multimodal
- bridge
- blip
- efficient-training
---

## Summary

BLIP-2 addresses a fundamental challenge in building vision-language models: how to connect a powerful frozen image encoder with a powerful frozen LLM without retraining either, given that they operate in entirely different representation spaces. The proposed solution is the Q-Former (Querying Transformer) — a lightweight transformer initialized from BERT that maintains a fixed set of learned query tokens (32 by default). These queries attend to image features from the frozen encoder (EVA-CLIP ViT-G) via cross-attention, and interact with each other via self-attention, learning to extract the most language-relevant visual information from the full patch sequence.

Q-Former is pre-trained in two sequential stages. In the first stage, the image encoder is frozen and the Q-Former is optimized with three objectives jointly: Image-Text Contrastive (ITC) loss, which aligns query-extracted features with text representations; Image-Text Matching (ITM) loss, which trains the model to classify whether an image-query output and a text description match; and Image-grounded Text Generation (ITG) loss, which forces the queries to capture information sufficient to generate the associated caption. This stage teaches the Q-Former to compress image content into query tokens in a language-aligned way. In the second stage, the Q-Former's output is projected via a linear layer into the LLM's embedding space (FlanT5 or OPT variants), and the system is fine-tuned for conditional text generation with the LLM frozen. Only Q-Former parameters and the linear projection are trained throughout — the image encoder and LLM remain fixed.

Empirically, BLIP-2 achieves state-of-the-art results on VQAv2, COCO image captioning, NoCaps, and zero-shot visual question answering benchmarks at the time of publication. The OPT-6.7B-backed variant matches prior fully fine-tuned VLMs while training a fraction of the parameters, and the model demonstrates emergent zero-shot image-to-text capabilities — including instruction following and multi-step visual reasoning — that arise from the LLM without visual fine-tuning. This positions Q-Former as a general-purpose visual adapter compatible with any sufficiently capable LLM.

## Why It Matters

Q-Former's design — fixed learned queries compressing image information into a small bottleneck that feeds into a language model — became the canonical architecture for efficient VLM construction, directly influencing InstructBLIP (which added instruction-specific query conditioning), MiniGPT-4 (which simplified the bridge to a single projection layer, validating that even minimal bridges can work with aligned encoders), and LLaVA (which replaced Q-Former with a linear projection while keeping the two-stage training philosophy). The broader principle that frozen large models can be composed via lightweight trainable adapters proved highly generative and shaped the parameter-efficient fine-tuning literature for multimodal systems.

A key limitation is that Q-Former introduces a fixed information bottleneck: 32 query tokens must capture all task-relevant visual content, which can be lossy for fine-grained visual reasoning, dense spatial tasks, or high-resolution inputs. Subsequent models addressed this by increasing query counts, using dynamic resolution processing (e.g., LLaVA-1.5's tile-based encoding), or abandoning the bottleneck entirely in favor of feeding all patch tokens to the LLM with positional compression — each approach trading compute against visual fidelity and revealing that the right bottleneck size remains an open design question.

| | |
|---|---|
| **Authors** | Li et al. |
| **Year** | 2023 |
| **Venue** | arXiv / ICML 2023 |
| **Field** | Computer Vision |
| **Subfield** | Open World Perception |
| **Tasks** | vlm, multimodal, bridge-module |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2301.12597.pdf){: .btn .btn--primary .btn--large}
