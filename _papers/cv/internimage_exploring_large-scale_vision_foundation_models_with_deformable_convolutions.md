---
title: 'InternImage: Exploring Large-Scale Vision Foundation Models with Deformable
  Convolutions'
collection: papers
permalink: /papers/cv/internimage_exploring_large-scale_vision_foundation_models_with_deformable_convolutions/
date: '2022-11-09'
year: 2022
field: computer-vision
subfield: open-world-perception
tasks:
- cnn-foundation-models
- detection
- segmentation
tier: 2
artifact_type: paper
venue: arXiv / CVPR 2023
authors:
- Wenhai Wang
- Jifeng Dai
- Zhe Chen
- Zhenhang Huang
authors_short: Wang et al.
paperurl: https://arxiv.org/pdf/2211.05778.pdf
doi: 10.48550/arXiv.2211.05778
license: unspecified
summary: InternImage scales deformable convolution networks to one billion parameters
  via DCNv3—achieving state-of-the-art object detection and semantic segmentation
  without masked or contrastive pretraining.
why_important: By demonstrating that a carefully modernized CNN can match or surpass
  billion-parameter transformers on dense prediction benchmarks, InternImage challenges
  the prevailing assumption that attention mechanisms are necessary for frontier vision
  foundation models.
tags:
- cnn
- foundation-models
- deformable-convolutions
- detection
---

## Summary

InternImage revisits convolutional networks at foundation-model scale by replacing standard convolution with DCNv3 — a substantially improved version of deformable convolution — as the core operator. DCNv3 introduces three key modifications over DCNv2: a multi-group design analogous to multi-head attention (allowing different spatial offset patterns per group), depth-wise convolution within each group, and softmax normalization of learned sampling weights for training stability. These changes enable the operator to learn flexible, input-adaptive receptive fields without the quadratic complexity of global self-attention, while sharing projection weights across groups to control parameter growth.

The architecture stacks DCNv3 blocks in a hierarchical, multi-scale design that produces feature pyramids suitable for dense prediction heads (e.g., Mask2Former for segmentation, DINO for detection). The model family scales from InternImage-T (30M parameters) to InternImage-H (1B parameters), all trained with standard supervised classification on ImageNet-22K followed by task-specific fine-tuning — no masked or contrastive pretraining is used. At the top end, InternImage-H achieves 65.4 mIoU on ADE20K semantic segmentation and 65.0 AP on COCO object detection, matching or exceeding transformer-based models of comparable scale at the time of publication.

The core methodological contribution is a carefully reasoned argument that inductive biases — local processing with adaptive receptive fields — are not a handicap at scale but a genuine advantage for dense prediction tasks. Deformable convolutions naturally focus computation on relevant spatial locations, which is particularly beneficial for detection and segmentation where objects appear at varied scales and positions. This locality also reduces the effective sequence length that must be processed compared to global attention, lowering wall-clock training time on high-resolution inputs.

## Why It Matters

InternImage provides a rigorous empirical challenge to the post-2021 consensus that vision transformers are categorically superior to CNNs at large scale. By demonstrating parity or superiority on the most demanding dense prediction benchmarks, it reopened serious consideration of convolutional designs and contributed to the broader "what inductive bias actually matters at scale" debate — a conversation that also includes ConvNeXt and its variants. The result is methodologically important because it disentangles scale (number of parameters, training data) from architectural choice: performance gaps between ViTs and CNNs observed in earlier work were partly a consequence of under-scaling the convolutional models.

A limitation worth noting is that InternImage's strong results on detection and segmentation do not straightforwardly extend to masked or contrastive pretraining paradigms, where transformer architectures have structural advantages (e.g., the masked token mechanism). As the field moved toward unified visual pretraining pipelines that feed both classification and generation tasks, purely convolutional backbones became harder to integrate, and subsequent large-scale foundation models generally retained attention as the primary operator.

| | |
|---|---|
| **Authors** | Wang et al. |
| **Year** | 2022 |
| **Venue** | arXiv / CVPR 2023 |
| **Field** | Computer Vision |
| **Subfield** | Open World Perception |
| **Tasks** | cnn-foundation-models, detection, segmentation |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2211.05778.pdf){: .btn .btn--primary .btn--large}
