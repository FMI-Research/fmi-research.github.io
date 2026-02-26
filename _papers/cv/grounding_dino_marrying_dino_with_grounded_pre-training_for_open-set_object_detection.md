---
title: 'Grounding DINO: Marrying DINO with Grounded Pre-Training for Open-Set Object
  Detection'
collection: papers
permalink: /papers/cv/grounding_dino_marrying_dino_with_grounded_pre-training_for_open-set_object_detection/
date: '2023-03-09'
year: 2023
field: computer-vision
subfield: open-world-perception
tasks:
- open-set-detection
- language-grounding
- zero-shot
tier: 2
artifact_type: paper
venue: arXiv / ECCV 2024
authors:
- Shilong Liu
- Zhaoyang Zeng
- Tianhe Ren
- Feng Li
authors_short: Liu et al.
paperurl: https://arxiv.org/pdf/2303.05499.pdf
doi: 10.48550/arXiv.2303.05499
license: unspecified
summary: Grounding DINO fuses a DINO-style detection transformer with a BERT language
  backbone via three-phase feature fusion and grounded pre-training, achieving 52.5
  AP zero-shot on COCO and state of the art on open-vocabulary detection benchmarks.
why_important: Grounding DINO established the leading open-set detection paradigm
  and became the standard text-to-box component in open-world perception pipelines,
  most notably as the detection head in Grounded SAM.
tags:
- open-set
- detection
- language-grounding
- zero-shot
---

## Summary

Grounding DINO extends the DINO detection transformer to open-set object detection by incorporating language understanding at multiple levels of the architecture. A BERT-based text encoder processes the input text query in parallel with the image backbone. Unlike late-fusion approaches that align modalities only in the decoder, Grounding DINO employs a three-phase fusion strategy: (1) a feature enhancer module in the neck performs bidirectional cross-attention between image and text feature maps to produce modality-aware representations; (2) a language-guided query selection mechanism uses text-image similarity to initialize object queries, focusing the decoder on text-relevant spatial regions from the outset; and (3) a cross-modality decoder performs joint image-text cross-attention at each decoding layer for precise box regression and text-conditioned class prediction.

On zero-shot COCO object detection—where the model has never seen COCO images during training—Grounding DINO achieves 52.5 AP, a substantial improvement over prior open-vocabulary methods and a compelling demonstration of cross-dataset generalization. When fine-tuned on COCO, it reaches 63.0 AP, competitive with the strongest closed-set detectors. On established open-vocabulary and grounding benchmarks—ODinW (Object Detection in the Wild), PhraseCut, and RefCOCO—Grounding DINO sets state of the art at the time of release, surpassing GLIP and GLIPv2 across multiple evaluation protocols, particularly on referring expression comprehension tasks that require language-guided spatial reasoning.

The grounded pre-training strategy is central to Grounding DINO's generalization. Training data is drawn from a heterogeneous mixture: standard detection datasets (Objects365, COCO, OpenImages) providing precise box annotations, grounding datasets (GoldG, Cap4M) providing phrase-region correspondences, and image-caption pairs providing weak supervision via a phrase grounding loss that aligns noun phrases to spatial regions. This mixture-of-supervision approach allows the model to learn diverse language-visual alignments—from precise noun phrases to free-form captions—without overfitting to any single annotation format or object vocabulary.

## Why It Matters

Grounding DINO operationalized the vision of open-vocabulary detection: a single model that can locate any object specified by a natural language phrase, without retraining on new categories. This has broad implications for robotics (where object vocabularies are task-specific and unpredictable), data annotation (where automating detection labeling saves enormous human effort), and visual search (where users specify queries in free text). Its strong zero-shot COCO result—52.5 AP without seeing any COCO training images—provides compelling evidence of genuine generalization rather than distribution overlap or benchmark leakage.

In practice, Grounding DINO's most widespread impact is as the detection component in the Grounded SAM pipeline, where its text-to-box outputs serve as geometric prompts for SAM's mask decoder. This pairing created a widely adopted reference architecture for open-world instance segmentation. Known limitations include sensitivity to prompt phrasing (subtle rephrasing of text queries can significantly change detection behavior), computational overhead from dual-encoder inference, and difficulty with abstract or relational language queries that require scene-level reasoning—motivating subsequent work on tighter language-vision integration within unified architectures.

| | |
|---|---|
| **Authors** | Liu et al. |
| **Year** | 2023 |
| **Venue** | arXiv / ECCV 2024 |
| **Field** | Computer Vision |
| **Subfield** | Open World Perception |
| **Tasks** | open-set-detection, language-grounding, zero-shot |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2303.05499.pdf){: .btn .btn--primary .btn--large}
