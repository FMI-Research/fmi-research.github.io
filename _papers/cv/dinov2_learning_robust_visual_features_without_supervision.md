---
title: 'DINOv2: Learning Robust Visual Features without Supervision'
collection: papers
permalink: /papers/cv/dinov2_learning_robust_visual_features_without_supervision/
date: '2023-04-14'
year: 2023
field: computer-vision
subfield: open-world-perception
tasks:
- self-supervised-learning
- visual-features
- transfer-learning
tier: 1
artifact_type: paper
venue: arXiv / TMLR 2024
authors:
- Maxime Oquab
- Timothee Darcet
- Theo Moutakanni
- Huy Vo
authors_short: Oquab et al.
paperurl: https://arxiv.org/pdf/2304.07193.pdf
doi: 10.48550/arXiv.2304.07193
license: unspecified
summary: DINOv2 trains ViT models via a combination of self-distillation and masked
  image modeling on a curated 142M-image dataset, producing frozen visual features
  that match or exceed supervised baselines across classification, depth, segmentation,
  and retrieval without fine-tuning.
why_important: DINOv2 demonstrated that purely vision-based self-supervised pretraining
  at scale can rival weakly supervised text-image models on dense prediction tasks,
  establishing it as a dominant frozen backbone for downstream visual applications.
tags:
- self-supervised
- vision
- features
- backbone
- dinov2
---

## Summary

DINOv2 trains Vision Transformer (ViT) models using an improved self-supervised learning recipe applied to a carefully curated large-scale dataset. Training combines two complementary objectives: a self-distillation loss (DINO) applied at the [CLS] token level for global semantic structure, and a masked image modeling loss (iBOT) applied at the patch token level for local spatial feature learning. Additional stabilization techniques include Sinkhorn-Knopp centering (to prevent representation collapse in the teacher-student framework), KoLeo regularization (to encourage uniform, non-degenerate coverage of the embedding space), and a short final phase of high-resolution fine-tuning that sharpens spatial detail in the learned patch features.

The largest DINOv2 model (ViT-g/14) achieves features that match or exceed the performance of supervised and weakly supervised baselines across a wide suite of benchmarks using only a linear probe on frozen representations—no backbone fine-tuning required. On depth estimation and semantic segmentation—tasks demanding fine spatial resolution—DINOv2 substantially outperforms OpenCLIP models of comparable scale, demonstrating that language supervision does not compensate for the richer patch-level structure learned by masked image modeling. On ImageNet classification, DINOv2 is competitive with supervised baselines at the linear probe level, and further improves with a simple k-NN classifier due to the well-structured nature of its feature space.

A key methodological contribution is the construction of LVD-142M, a curated pretraining dataset of 142 million images assembled via self-supervised retrieval and filtering from web-scale image collections. Rather than using raw internet data directly—which is noisy, redundant, and domain-imbalanced—the authors use an existing self-supervised embedding model to retrieve images similar to a set of curated seed datasets, followed by deduplication and quality filtering to select a diverse and informative subset. This data curation pipeline is shown to be critical: training on LVD-142M substantially outperforms training on raw uncurated data at similar scale, establishing dataset quality as a first-class concern in self-supervised pretraining at scale.

## Why It Matters

DINOv2 challenged a prevailing assumption that language supervision (as in CLIP and its variants) was necessary to learn rich, transferable visual representations. By demonstrating that a pure vision-based SSL pipeline—with the right data curation and training recipe—can match or beat text-supervised models on dense prediction tasks, DINOv2 re-centered attention on the quality of the visual learning objective and pretraining data distribution. Its frozen features have since become a standard backbone across robotics, medical imaging, 3D reconstruction, and satellite imagery analysis, reflecting broad applicability to domains where language supervision is sparse or unavailable.

The practical impact of DINOv2 is significant: because its features are strong without fine-tuning, researchers can use DINOv2 as a drop-in encoder for new tasks with minimal compute overhead. However, DINOv2 has known limitations—it lacks language understanding and cannot perform zero-shot classification by text query—motivating multimodal hybrids that combine DINOv2-style spatial richness with language alignment. The paper also surfaces a clear scaling story: larger ViTs trained with this recipe continue to improve consistently, with ViT-g outperforming ViT-L by meaningful margins across benchmarks, suggesting that the recipe has not yet saturated at the sizes studied.

| | |
|---|---|
| **Authors** | Oquab et al. |
| **Year** | 2023 |
| **Venue** | arXiv / TMLR 2024 |
| **Field** | Computer Vision |
| **Subfield** | Open World Perception |
| **Tasks** | self-supervised-learning, visual-features, transfer-learning |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2304.07193.pdf){: .btn .btn--primary .btn--large}
