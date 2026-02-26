---
title: 3D Gaussian Splatting for Real-Time Radiance Field Rendering
collection: papers
permalink: /papers/cv/3d_gaussian_splatting_for_real-time_radiance_field_rendering/
date: '2023-08-08'
year: 2023
field: computer-vision
subfield: generative-vision
tasks:
- radiance-fields
- real-time-rendering
- 3d-reconstruction
tier: 2
artifact_type: paper
venue: SIGGRAPH 2023
authors:
- Bernhard Kerbl
- Georgios Kopanas
- Thomas Leimkuhler
- George Drettakis
authors_short: Kerbl et al.
paperurl: https://arxiv.org/pdf/2308.04079.pdf
doi: 10.1145/3592433
license: unspecified
summary: 3D Gaussian Splatting represents scenes as collections of explicit 3D Gaussian
  primitives optimized from multi-view images and rendered via a differentiable tile-based
  rasterizer, achieving real-time novel view synthesis at over 100 FPS.
why_important: 3DGS displaced NeRF as the dominant scene representation for novel
  view synthesis by offering an order-of-magnitude speed improvement with competitive
  quality, spawning a broad ecosystem of editing, generation, and SLAM applications.
tags:
- 3dgs
- gaussian-splatting
- radiance-fields
- real-time
- 3d
---

## Summary

3D Gaussian Splatting (3DGS) represents scenes as collections of anisotropic 3D Gaussian primitives, each parameterized by a 3D position (mean), a full 3D covariance matrix (encoded as a rotation and scale), an opacity scalar, and view-dependent color coefficients expressed as spherical harmonics. Unlike NeRF's implicit MLP representation, 3DGS is fully explicit: there is no network to query, no ray marching, and no numerical integration along rays. Rendering proceeds by projecting ("splatting") each Gaussian onto the image plane as a 2D Gaussian, sorting them by depth, and alpha-compositing them in a tile-based rasterizer implemented in CUDA. This rasterizer is differentiable, allowing gradients to flow back to all Gaussian parameters during training.

Optimization initializes from a sparse SfM point cloud (from COLMAP) and alternates between gradient-based parameter updates and an adaptive density control procedure that clones Gaussians in under-reconstructed regions, splits large Gaussians that span complex geometry, and prunes transparent Gaussians. This densification schedule is critical to achieving both compact and complete scene coverage. A typical outdoor scene trains in approximately 35 minutes on a single GPU.

On standard novel view synthesis benchmarks—Tanks and Temples, Deep Blending, and Mip-NeRF360—3DGS achieves PSNR of 27–29 dB, matching or slightly exceeding Mip-NeRF360 while rendering at over 100 FPS at 1080p resolution on consumer GPUs (compared to seconds per frame for NeRF variants). This combination of competitive reconstruction quality and real-time rendering at interactive resolutions represents a qualitative leap in practical usability.

## Why It Matters

3DGS's impact on novel view synthesis has been transformative. By replacing the implicit MLP of NeRF with an explicit, rasterizable set of Gaussians, 3DGS broke the throughput bottleneck that had made NeRF impractical for real-time applications. Within a year of publication, 3DGS had been extended to dynamic scenes (4D Gaussian Splatting, Deformable 3DGS), generative settings (GaussianDreamer, DreamGaussian), semantic understanding (Gaussian Grouping), and simultaneous localization and mapping (SplaTAM). The explicit nature of the representation also makes it significantly more interpretable than NeRF—individual Gaussians can be selected, edited, and composited in ways that implicit representations do not easily support.

A key limitation is that 3DGS inherits the limitations of its SfM initialization: scenes with textureless surfaces, transparent objects, or extreme viewpoint variation can produce incomplete or noisy Gaussian clouds. Storage costs are also nontrivial, as a high-quality scene may require millions of Gaussians. Nonetheless, 3DGS has become the de facto representation for real-time novel view synthesis and a foundational component in a rapidly growing ecosystem of 3D generation and reconstruction pipelines.

| | |
|---|---|
| **Authors** | Kerbl et al. |
| **Year** | 2023 |
| **Venue** | SIGGRAPH 2023 |
| **Field** | Computer Vision |
| **Subfield** | Generative Vision |
| **Tasks** | radiance-fields, real-time-rendering, 3d-reconstruction |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2308.04079.pdf){: .btn .btn--primary .btn--large}
