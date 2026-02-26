---
title: 'SAM 2: Segment Anything in Images and Videos'
collection: papers
permalink: /papers/cv/sam_2_segment_anything_in_images_and_videos/
date: '2024-07-29'
year: 2024
field: computer-vision
subfield: open-world-perception
tasks:
- video-segmentation
- promptable-segmentation
- streaming-memory
tier: 1
artifact_type: paper
venue: arXiv 2024
authors:
- Nikhila Ravi
- Valentin Gabeur
- Yuan-Ting Hu
- Ronghang Hu
authors_short: Ravi et al.
paperurl: https://arxiv.org/pdf/2408.00714.pdf
doi: 10.48550/arXiv.2408.00714
license: unspecified
summary: SAM 2 extends SAM to video via a streaming memory bank attended by cross-attention,
  enabling real-time promptable segmentation at ~44 FPS and surpassing prior video
  object segmentation methods by large margins on DAVIS, MOSE, and SA-V.
why_important: SAM 2 establishes the state of the art for interactive video object
  segmentation while being 6× faster than the original SAM on images, making temporally
  coherent promptable segmentation practical for video annotation and robotics.
tags:
- segmentation
- video
- promptable
- sam
- foundation-models
---

## Summary

SAM 2 generalizes SAM's promptable segmentation paradigm from static images to video by introducing a streaming memory mechanism. The core architecture retains the prompt-guided mask decoder from SAM but replaces the heavyweight ViT-H encoder with a hierarchical image encoder (Hiera) optimized for throughput. Crucially, a memory module—comprising a memory encoder, a fixed-size FIFO memory bank of past frame features, and a memory attention layer—allows the model to propagate segmentation context forward in time. At each new frame, the memory attention layer cross-attends current frame features against the stored memory bank to condition the mask decoder, enabling temporally coherent mask propagation without reprocessing the entire video history.

SAM 2 achieves substantial improvements over prior video object segmentation (VOS) methods on standard benchmarks. On DAVIS 2017, MOSE, and the newly introduced SA-V benchmark, SAM 2 surpasses DEVA, XMem, and other state-of-the-art VOS systems by significant margins in J&F metric. Remarkably, SAM 2 also outperforms the original SAM on static image segmentation—by virtue of a more efficient encoder—while being approximately 6× faster at inference time. Real-time video processing runs at roughly 44 FPS, making interactive video annotation practically feasible within human annotation workflows.

To train SAM 2, the authors built the SA-V dataset using a video-adapted version of SAM's three-stage data engine, yielding 50,900 videos with over 642,000 masklet annotations—segmentation masks propagated coherently across frames. The memory bank design is deliberately simple: a FIFO queue of N past frames plus any user-prompted frames, preventing unbounded memory growth during long videos. SAM 2 also handles ambiguous frames by predicting multiple candidate masks, and supports both forward and backward temporal propagation during interactive annotation sessions, enabling annotators to correct and refine predictions bidirectionally.

## Why It Matters

SAM 2 closes a critical gap left by SAM by extending promptable segmentation to the temporal domain. Video understanding is central to robotics, autonomous driving, content moderation, and medical video analysis—domains where per-frame mask annotation is impractical at scale. By enabling a user to prompt a single frame and automatically propagate the mask through time, SAM 2 dramatically reduces human annotation effort for video segmentation datasets, with implications for any application requiring persistent object tracking under challenging conditions such as occlusion and motion blur.

The architectural lesson of SAM 2—that a lightweight streaming memory bank combined with cross-attention suffices for temporally coherent segmentation—is broadly applicable and has influenced subsequent streaming video perception systems. The SA-V dataset advances benchmarking for VOS in challenging, real-world conditions that prior benchmarks such as DAVIS underrepresent. Equally notable is that SAM 2 surpasses SAM on static images despite being faster: this underscores the value of rethinking architecture holistically rather than simply patching an existing model, and suggests that the Hiera encoder family may be preferable to ViT-H for general-purpose visual encoding.

| | |
|---|---|
| **Authors** | Ravi et al. |
| **Year** | 2024 |
| **Venue** | arXiv 2024 |
| **Field** | Computer Vision |
| **Subfield** | Open World Perception |
| **Tasks** | video-segmentation, promptable-segmentation, streaming-memory |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2408.00714.pdf){: .btn .btn--primary .btn--large}
