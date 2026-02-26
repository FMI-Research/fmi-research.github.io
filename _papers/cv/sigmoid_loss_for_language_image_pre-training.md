---
title: Sigmoid Loss for Language Image Pre-Training
collection: papers
permalink: /papers/cv/sigmoid_loss_for_language_image_pre-training/
date: '2023-03-28'
year: 2023
field: computer-vision
subfield: open-world-perception
tasks:
- image-text-pretraining
- vlm
- retrieval
tier: 2
artifact_type: paper
venue: arXiv / ICCV 2023
authors:
- Xiaohua Zhai
- Basil Mustafa
- Alexander Kolesnikov
- Lucas Beyer
authors_short: Zhai et al.
paperurl: https://arxiv.org/pdf/2303.15343.pdf
doi: 10.48550/arXiv.2303.15343
license: unspecified
summary: SigLIP replaces CLIP's softmax contrastive loss with a pairwise sigmoid binary
  cross-entropy, eliminating global batch normalization and enabling efficient large-scale
  image-text pretraining with 83.1% zero-shot ImageNet accuracy.
why_important: By decoupling each image-text pair's gradient from the global batch,
  SigLIP simplifies distributed training at scale and its encoders became the standard
  visual backbone in production VLMs including PaLI-X, Gemini, and InternVL.
tags:
- siglip
- vlm
- image-text
- pretraining
- contrastive
---

## Summary

SigLIP (Sigmoid Loss for Language-Image Pre-Training) replaces the softmax-normalized contrastive loss used in CLIP with a pairwise sigmoid binary cross-entropy loss. In standard CLIP, the InfoNCE objective requires computing a softmax over all N² image-text similarity scores in a batch, which necessitates global reduction across devices: every GPU/TPU must communicate its local similarities to compute the correct normalization constant. At the batch sizes needed for strong zero-shot performance (tens of thousands of pairs), this all-reduce communication becomes a training bottleneck and complicates efficient scaling across large pod configurations. SigLIP's sigmoid loss treats each (image, text) pair independently as a binary classification problem (positive pair vs. negative), computing gradients locally without requiring global normalization, which simplifies the distributed training graph significantly.

Empirically, a SigLIP ViT-So400M/14 encoder achieves 83.1% zero-shot top-1 accuracy on ImageNet, matching or exceeding OpenCLIP models trained with comparable compute but using the softmax loss. Notably, SigLIP maintains strong performance at smaller effective batch sizes where softmax CLIP typically degrades — because the sigmoid objective does not depend on having a large pool of in-batch negatives for normalization. The paper systematically ablates batch size, model scale, and loss variants, isolating the loss function itself as the key variable rather than data or architecture differences.

The methodological innovation is simple but consequential: decoupling each pair's gradient from global batch statistics is not merely an engineering convenience but changes the optimization landscape. Each pair contributes an independent learning signal regardless of what other pairs are in the batch, making the objective robust to batch composition effects and easier to implement correctly on heterogeneous hardware. The authors also introduce a bucketed evaluation protocol to ensure fair comparison with models trained under different batch-size regimes.

## Why It Matters

SigLIP encoders have become the de facto standard visual backbone in several high-profile production VLMs, including PaLI-X, Gemini, and InternVL, precisely because their training objective scales cleanly on TPU pod infrastructure without the all-reduce communication bottlenecks of softmax CLIP. This adoption at the systems level reflects a broader truth in ML infrastructure: a loss function that is easier to parallelize can be used with more compute, which often matters more in practice than small differences in per-FLOP efficiency.

The approach also raises an interesting theoretical question about what contrastive loss is actually doing: if the sigmoid variant works as well or better without global normalization, the normalization in softmax InfoNCE may be serving as implicit regularization or difficulty calibration rather than providing fundamentally necessary gradient information. This has stimulated follow-up work on loss design for multimodal pretraining, including variants that mix sigmoid and softmax terms or use online hard negative mining — suggesting that SigLIP marks a transition rather than a final answer in image-text pretraining loss design.

| | |
|---|---|
| **Authors** | Zhai et al. |
| **Year** | 2023 |
| **Venue** | arXiv / ICCV 2023 |
| **Field** | Computer Vision |
| **Subfield** | Open World Perception |
| **Tasks** | image-text-pretraining, vlm, retrieval |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2303.15343.pdf){: .btn .btn--primary .btn--large}
