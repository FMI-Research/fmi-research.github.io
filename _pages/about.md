---
permalink: /
title: "FMI-Research"
excerpt: "Frontier Machine Intelligence — a curated, structured library of landmark research in AGI, Computer Vision, Robotics, and Embodied AI."
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

## What Is FMI-Research?

**FMI-Research** (*Frontier Machine Intelligence Research*) is a structured, editorially curated library of landmark publications in five interrelated areas of contemporary AI: **Large Language Models & AGI**, **Computer Vision**, **Robotics**, **Embodied AI**, and **Autonomous Driving**. It is designed as a high-quality reference and navigation aid — not an exhaustive index, but a deliberately selective reading infrastructure for researchers, engineers, and advanced students who need to understand the field's foundations and its current frontier simultaneously.

The machine intelligence landscape has grown to a scale where no individual can track every relevant publication. Preprint servers, conference proceedings, and workshop papers accumulate faster than any reading practice can absorb. FMI-Research takes the opposite stance: careful selection, structured organization, and substantive annotation over raw completeness. Every paper in this library was chosen because it either established a paradigm, opened a new research direction, or provides indispensable methodological grounding.

---

## Why This Structure?

Research in frontier AI does not develop in isolated silos. A practitioner working on robotic manipulation needs to understand vision-language alignment from the CV literature, reasoning capabilities from the LLM literature, and policy learning paradigms from robotics — all simultaneously. FMI-Research reflects this cross-cutting reality by organizing content in a **three-level hierarchy**:

```
Area  →  Subfield  →  Task
```

**Area** corresponds to a broad research community with shared conferences, datasets, and evaluation norms (e.g., *Robotics* or *Computer Vision*). **Subfield** identifies a coherent cluster of problems within that community (e.g., *Manipulation & Imitation Learning* or *Generative Vision*). **Task** specifies the concrete computational problem that papers address (e.g., *Diffusion-based policy learning*, *Text-to-image synthesis*). This hierarchy allows a reader to navigate from broad orientation to specific technical depth without losing structural context.

Each paper entry includes a structured summary, an analysis of its significance, full authorship and venue metadata, and a link to the primary PDF source.

---

## Curation Criteria

Papers are included on one of three grounds, reflected in the **Tier** classification:

| Tier | Type | Meaning |
|---|---|---|
| **1** | Foundational / Survey | Established a paradigm or provides the canonical survey of a subfield |
| **2** | Method / Baseline | Widely adopted approach, strong empirical baseline, or key architectural innovation |
| **3** | Benchmark / Resource | Dataset, benchmark, or evaluation framework that structures downstream research |

Inclusion decisions prioritize *structural importance* over recency. A 2020 paper that every subsequent work in a subfield cites is more valuable to this library than a 2025 preprint that has not yet demonstrated lasting influence. At the same time, papers are not included simply for being old or famous — each entry must contribute meaningfully to a reader's understanding of the current frontier.

Coverage is updated periodically. The library currently covers publications through mid-2025 across its four areas.

---

## Coverage Areas

### Large Language Models & AGI

Covers the full arc from transformer pretraining at scale to alignment techniques and agentic deployment. Organized into three subfields:

- **LLM Foundations & Scaling** — The core modeling and training papers: scaling law derivations, architecture families (LLaMA, Mistral, Gemini, Qwen, PaLM), and system reports (GPT-4). These papers collectively define what a frontier language model is and how it is produced.
- **Alignment, Safety & Evaluation** — Methods for making LLMs instruction-following, factually grounded, and aligned with human values (RLHF/InstructGPT, DPO, Constitutional AI), alongside the evaluation infrastructure that measures these properties (HELM, C-Eval, CMMLU, hallucination surveys).
- **Agentic LLMs** — LLMs deployed as agents that reason over multi-step problems, use external tools, plan symbolically, and operate in interactive environments (ReAct, Toolformer, Tree of Thoughts, AutoGen, Voyager, RAG).

### Computer Vision

Covers the two dominant transformations in modern vision: the emergence of open-world, promptable foundation models, and the diffusion-based generative revolution.

- **Open-World Perception** — Foundation models for open-vocabulary segmentation (SAM, SAM2), grounded detection (Grounding DINO, Grounded SAM), self-supervised visual representation (DINOv2, EVA, InternImage), and vision-language alignment (SigLIP, BLIP-2).
- **Generative Vision** — The diffusion model paradigm from latent diffusion (LDM, Stable Diffusion), through text-conditioned image synthesis (Imagen, DALL-E 2), structural control (ControlNet), 3D generation (DreamFusion, 3DGS), and video synthesis (Imagen Video, Text2Video-Zero).

### Robotics

Covers learning-based approaches to robot control, from the foundational imitation learning methods to the large-scale, internet-pretrained foundation models now entering the field.

- **Manipulation & Imitation Learning** — Behavioral cloning and its evolution (BC-Z), diffusion-based policies (Diffusion Policy), and the large cross-embodiment datasets that enable generalization (BridgeData V2, DROID, Open X-Embodiment). Complemented by key benchmark environments (LIBERO).
- **Foundation Models & VLA** — Vision-Language-Action models that bring the generalization capacity of large pretrained models to robot control (RT-1, RT-2, PaLM-E, SayCan, Octo, OpenVLA), along with the surveys that map this emerging landscape.

### Embodied AI

The intersection of perception, language, and physical action — agents that must not merely recognize or generate, but operate in and reason about 3D environments. This area covers the comprehensive surveys that frame the embodied agent problem (Duan et al., Liu et al.), emerging world model approaches for embodied learning, and the data infrastructure that makes large-scale embodied training tractable.

### Autonomous Driving

Covers the paradigm shift from hand-engineered modular pipelines to end-to-end learned systems and, most recently, to LLM/VLA-augmented architectures that bring commonsense reasoning and natural language to driving. Organized into three subfields:

- **End-to-End Autonomous Driving** — Unified architectures (UniAD, VAD, SparseDrive) that jointly optimize perception, prediction, and planning. Includes benchmarks and simulation frameworks (NAVSIM) that enable rigorous E2E evaluation.
- **LLM & VLA for Autonomous Driving** — Systems that integrate large vision-language models into driving for scene understanding, chain-of-thought planning, and language-grounded control (DriveVLM, DriveLM, Senna). Accompanied by the surveys charting this intersection.
- **World Models for Autonomous Driving** — Generative models that simulate realistic driving scenarios for data augmentation and policy evaluation (DriveDreamer).

---

## How to Use This Site

- **[Frontier →](/frontier/)** — Start here for a structured overview by area and subfield, with curated paper groups and navigational context.
- **[Papers →](/papers/)** — Browse all 92 entries sorted by field and date. Every entry is a crawlable HTML link to the paper's dedicated abstract page.
- **[Readings →](/readings/)** — Curated non-paper resources: research lab blogs, technical writing, landmark interviews and lecture series, benchmark hubs, and essential tools.

---

## Scope, Limitations & Contribution {#scope}

FMI-Research is intentionally narrow in scope. It does not aim to cover all of machine learning, all of AI, or all subfields within its four chosen areas. Audio, speech, NLP outside of LLMs, classical computer vision, and reinforcement learning (except where it directly underlies the covered methods) are out of scope.

Within its scope, the library is selective by design. Papers are not added because they are popular or have high citation counts alone — they are added because a researcher trying to understand the current frontier of a subfield cannot do without them.

**Suggestions and corrections are welcome.** If a paper is missing that you believe belongs, or if a summary contains an error, please open an issue on the [GitHub repository](https://github.com/FMI-Research/fmi-research.github.io) with the paper title, venue, and a brief argument for inclusion.

---

*Coverage through mid-2025. 92 papers across 5 areas, 11 subfields.*
