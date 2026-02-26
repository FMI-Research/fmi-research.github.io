---
title: Segment Anything
collection: papers
permalink: /papers/cv/segment_anything/
date: '2023-04-05'
year: 2023
field: computer-vision
subfield: open-world-perception
tasks:
- promptable-segmentation
- foundation-model
- data-engine
tier: 1
artifact_type: paper
venue: arXiv / ICCV 2023
authors:
- Alexander Kirillov
- Eric Mintun
- Nikhila Ravi
- Hanzi Mao
authors_short: Kirillov et al.
paperurl: https://arxiv.org/pdf/2304.02643.pdf
doi: 10.48550/arXiv.2304.02643
license: unspecified
summary: SAM introduces a promptable segmentation paradigm—accepting points, boxes,
  or masks as input—pairing a MAE-pretrained ViT-H image encoder with a fast two-way
  transformer mask decoder to return valid segmentation masks in real time across
  23+ diverse tasks.
why_important: SAM established the de facto foundation model for image segmentation,
  enabling zero-shot generalization across diverse tasks and catalyzing a generation
  of open-world perception systems built on its promptable interface.
tags:
- segmentation
- foundation-models
- promptable
- sam
---

## Summary

SAM introduces a promptable segmentation system designed to return a valid segmentation mask for any input prompt in real time. The architecture decomposes the task into three components: a heavyweight MAE-pretrained ViT-H image encoder run once per image to produce dense image embeddings; a lightweight prompt encoder that maps geometric prompts (points, bounding boxes, free-form masks) into embedding space; and a fast two-way transformer mask decoder that cross-attends prompt and image tokens to predict masks in under 50 ms. To handle ambiguous prompts—where multiple valid segmentations coexist—SAM predicts up to three candidate masks with associated confidence scores, allowing downstream systems to select the most contextually appropriate output.

On a comprehensive zero-shot evaluation spanning 28 downstream segmentation benchmarks, SAM matches or outperforms supervised task-specific models on 23 of them without any task-specific fine-tuning. Notably strong performance is observed on edge detection, instance segmentation, and object proposal generation. The model shows reduced competitiveness on fine-grained semantic segmentation, where category-level understanding matters more than geometric mask quality—a limitation intrinsic to its prompt-only, category-agnostic design. SAM is also not designed for video, where temporal consistency across frames requires additional mechanisms beyond single-image encoding.

A central methodological contribution is the SA-1B dataset and its three-stage data engine. The process begins with assisted manual annotation (annotators use an early SAM variant as an interactive tool to accelerate labeling), proceeds to semi-automatic annotation (SAM generates mask suggestions on unannotated image regions for human review), and culminates in fully automatic annotation (SAM generates masks densely across images at scale with no human in the loop). This bootstrapping loop yielded 1.1 billion masks across 11 million images—by far the largest segmentation dataset ever constructed—and directly enabled SAM's zero-shot generalization by exposing it to an unprecedented diversity of visual concepts and spatial scales during training.

## Why It Matters

SAM represents a paradigm shift in segmentation: instead of training separate models per task or category, a single promptable model generalizes across arbitrary visual concepts at interactive speeds. Its release transformed downstream pipelines in robotics, medical imaging, remote sensing, and data annotation—domains where collecting pixel-accurate labels had previously been prohibitively expensive. The SA-1B dataset, released publicly, has itself become a benchmark resource for studying data scaling laws in dense prediction tasks.

SAM's architectural decisions also set important precedents for the field. The strict separation of image encoding (computationally expensive, done once per image) from prompt decoding (cheap, done per query) is a general design pattern since adopted in multimodal perception systems. Its limitations are equally instructive: SAM's category-agnosticism means it cannot reliably segment based on class names alone, motivating follow-up work such as Grounding DINO and Grounded SAM to add language understanding. The video segmentation gap was directly addressed by SAM 2, which grafts a streaming memory module onto SAM's core architecture.

| | |
|---|---|
| **Authors** | Kirillov et al. |
| **Year** | 2023 |
| **Venue** | arXiv / ICCV 2023 |
| **Field** | Computer Vision |
| **Subfield** | Open World Perception |
| **Tasks** | promptable-segmentation, foundation-model, data-engine |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2304.02643.pdf){: .btn .btn--primary .btn--large}
