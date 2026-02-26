---
title: 'Grounded SAM: Assembling Open-World Models for Diverse Visual Tasks'
collection: papers
permalink: /papers/cv/grounded_sam_assembling_open-world_models_for_diverse_visual_tasks/
date: '2024-01-25'
year: 2024
field: computer-vision
subfield: open-world-perception
tasks:
- open-world
- detection
- segmentation
- pipeline
tier: 2
artifact_type: paper
venue: arXiv 2024
authors:
- Tianhe Ren
- Shilong Liu
- Ailing Zeng
- Jing Lin
authors_short: Ren et al.
paperurl: https://arxiv.org/pdf/2401.14159.pdf
doi: 10.48550/arXiv.2401.14159
license: unspecified
summary: Grounded SAM composes Grounding DINO and SAM at inference time—routing text
  queries to bounding box detections then to segmentation masks—achieving open-world
  instance segmentation without any task-specific training.
why_important: Grounded SAM demonstrated that modular inference-time composition of
  foundation models yields strong zero-shot generalization, becoming the de facto
  reference architecture and codebase for open-world segmentation research.
tags:
- open-world
- grounding
- segmentation
- detection
- pipeline
---

## Summary

Grounded SAM is a modular inference-time pipeline that composes two pretrained foundation models without any additional training or fine-tuning. Given a natural language text prompt, Grounding DINO produces axis-aligned bounding boxes for the described objects. These boxes are passed directly as geometric prompts to SAM's mask decoder, which produces pixel-accurate segmentation masks within each box region. The system requires no gradient updates, task-specific adaptation, or annotated data—it operates entirely through the sequential composition of the two models' existing inference APIs, exploiting the fact that Grounding DINO's box outputs are natively interpretable as SAM's box prompt format.

Grounded SAM achieves competitive performance on COCO panoptic segmentation and RefCOCO referential segmentation benchmarks without any task-specific training, demonstrating genuine zero-shot generalization across both open-vocabulary and referential tasks. The paper further demonstrates the system's extensibility by integrating additional foundation models: GPT-4 for query expansion and scene description, BLIP for automatic image captioning to generate detection prompts, and Stable Diffusion for inpainting—enabling end-to-end detect-segment-inpaint editing pipelines driven entirely by natural language. These multi-model integrations illustrate the composability of foundation models as interoperable inference-time components.

The central methodological contribution is the empirical demonstration that tightly sequenced modular composition of independently trained foundation models—each designed with general, well-specified interfaces—can produce emergent capabilities not present in either model alone. Grounded SAM is not a simple ensemble; the sequential routing (text → box → mask) deliberately exploits each model's specific strength: Grounding DINO's language-visual alignment for open-vocabulary localization, and SAM's geometry-driven mask quality for precise pixel-level delineation. The authors released a complete open-source codebase that accumulated 14,000+ GitHub stars, becoming a reference implementation widely used in research, annotation tooling, and robotic manipulation systems.

## Why It Matters

Grounded SAM is a proof of concept for a broader architectural philosophy: rather than training a monolithic model for every perception task, capable systems can be assembled by composing specialized foundation models at inference time with no additional training cost. This has significant practical value—each component can be independently improved, replaced with a stronger alternative, or extended to new modalities without retraining the pipeline. The paper demonstrated this modularity concretely by substituting different detectors and segmenters in ablations, showing that the pipeline's quality scales predictably with component quality.

The impact of Grounded SAM extends well beyond its benchmark numbers. Its codebase became a community resource and launchpad for open-world segmentation research, robotic manipulation, and automated data annotation workflows. However, the system inherits the limitations of its components: Grounding DINO's sensitivity to prompt phrasing propagates directly to mask quality, and SAM's category-agnostic design means the pipeline has no mechanism to resolve semantic ambiguity between similarly shaped objects detected under overlapping prompts. These known failure modes have motivated subsequent work on tighter language-vision integration within unified models rather than purely modular composition—highlighting the ongoing tension between composability and end-to-end optimization.

| | |
|---|---|
| **Authors** | Ren et al. |
| **Year** | 2024 |
| **Venue** | arXiv 2024 |
| **Field** | Computer Vision |
| **Subfield** | Open World Perception |
| **Tasks** | open-world, detection, segmentation, pipeline |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2401.14159.pdf){: .btn .btn--primary .btn--large}
