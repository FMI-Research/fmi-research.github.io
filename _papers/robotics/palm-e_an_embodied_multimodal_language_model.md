---
title: 'PaLM-E: An Embodied Multimodal Language Model'
collection: papers
permalink: /papers/robotics/palm-e_an_embodied_multimodal_language_model/
date: '2023-03-06'
year: 2023
field: robotics
subfield: robot-foundation-models-vla
tasks:
- embodied-multimodal
- grounding
- planning
- continuous-sensing
tier: 2
artifact_type: paper
venue: ICML 2023
authors:
- Danny Driess
- Fei Xia
- Mehdi S. M. Sajjadi
- Corey Lynch
authors_short: Driess et al.
paperurl: https://proceedings.mlr.press/v202/driess23a/driess23a.pdf
doi: 10.48550/arXiv.2302.14030
license: unspecified
summary: PaLM-E is a 562-billion-parameter embodied multimodal language model that
  directly incorporates continuous sensor inputs (images, robot state vectors, object
  embeddings) as prefix tokens into PaLM, enabling unified grounded reasoning over
  language and perception for embodied planning, visual question answering, and robot
  control within a single autoregressive model.
why_important: Demonstrated that continuous embodied sensor information integrates
  seamlessly into a single large language model framework, achieved positive multi-task
  transfer between robotic and non-robotic tasks, and established the sensor token
  injection architecture that directly influenced subsequent VLA designs.
tags:
- palm-e
- embodied-multimodal
- grounding
- vlm
- robotics
---

## Summary

PaLM-E, presented at ICML 2023, addresses a fundamental architectural challenge: how to ground a large language model's reasoning capabilities in continuous sensory observations from physical environments without requiring intermediate symbolic representations. Driess et al. inject continuous sensor data—RGB images encoded by a ViT, 3D scene representations encoded by an object-centric transformer, and robot state vectors—directly as sequences of embedding vectors interleaved with text tokens in PaLM's input sequence. This sensor token injection approach allows the model to process prompts combining text and sensor data and respond with either natural language or robot action commands, unifying multimodal understanding and control in a single autoregressive model. The architecture spans three scales: PaLM-E-12B, PaLM-E-84B, and PaLM-E-562B, with the largest model trained on a diverse mixture of language, visual question answering, image captioning, and robotic manipulation data.

The empirical results demonstrate performance across three qualitatively different task types: mobile manipulation (directing a SayCan-style skill execution system on a real robot), tabletop manipulation (direct end-effector control on a real WidowX arm), and visual question answering (OK-VQA benchmark). On mobile manipulation, PaLM-E achieves 79% success on a 10-step multi-task language-conditioned planning suite while requiring 75% fewer inference calls than a two-stage pipeline combining separate VLM and LLM. On OK-VQA, the 562B model achieves state-of-the-art performance, demonstrating that robotic fine-tuning data does not degrade language and visual reasoning—and in fact produces positive transfer. A particularly striking result is that PaLM-E-562B shows emergent few-shot behavior on manipulation tasks for which it received no demonstration data, executing them after seeing only a few examples in the prompt.

PaLM-E's methodological innovation lies in the generality of the sensor injection mechanism. By treating any continuous sensor embedding as a sequence of input tokens, the architecture is agnostic to the specific sensing modality: any sensor for which an embedding model exists can be incorporated without architectural modification. The paper demonstrates this with three different visual encoding strategies (ViT, object-centric NeRF, and 3D point cloud encoders), showing that the approach is robust to the encoder choice as long as the embeddings are aligned with the language model's input space through a learned projection. This modality-agnostic design principle has directly influenced subsequent embodied multimodal architectures.

## Why It Matters

PaLM-E is a landmark demonstration of the embodied foundation model concept: a single model that can reason about both language and physical sensors, plan multi-step tasks, and directly control a robot without requiring hand-designed interfaces between modules. Its positive multi-task transfer result—showing that training on robotics data improves visual question answering, not merely vice versa—provided the first strong evidence that robotics and language understanding are mutually reinforcing objectives in a shared model rather than competing ones. This finding directly motivated the co-fine-tuning approach in RT-2.

PaLM-E also highlights an important tension between model scale and practical deployability. The 562B model achieves the strongest results but requires specialized large-scale infrastructure to run inference, making it inaccessible for most robot learning research. Subsequent work (OpenVLA at 7B, Octo at 93M) has progressively shown that competitive manipulation performance is achievable at much smaller scales, but whether the semantic grounding and few-shot generalization properties of PaLM-E-562B can be fully replicated at 7B parameters—through better data curation or training recipes—remains an active research question that connects scale efficiency debates in NLP directly to the embodied AI domain.

| | |
|---|---|
| **Authors** | Driess et al. |
| **Year** | 2023 |
| **Venue** | ICML 2023 |
| **Field** | Robotics |
| **Subfield** | Robot Foundation Models Vla |
| **Tasks** | embodied-multimodal, grounding, planning, continuous-sensing |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://proceedings.mlr.press/v202/driess23a/driess23a.pdf){: .btn .btn--primary .btn--large}
