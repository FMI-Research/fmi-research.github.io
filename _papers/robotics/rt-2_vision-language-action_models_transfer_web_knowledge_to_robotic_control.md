---
title: 'RT-2: Vision-Language-Action Models Transfer Web Knowledge to Robotic Control'
collection: papers
permalink: /papers/robotics/rt-2_vision-language-action_models_transfer_web_knowledge_to_robotic_control/
date: '2023-07-28'
year: 2023
field: robotics
subfield: robot-foundation-models-vla
tasks:
- vla
- web-knowledge-transfer
- robotic-control
tier: 1
artifact_type: paper
venue: arXiv / CoRL 2023
authors:
- Anthony Brohan
- Noah Brown
- Justice Carbajal
- Yevgen Chebotar
authors_short: Brohan et al.
paperurl: https://arxiv.org/pdf/2307.15818.pdf
doi: 10.48550/arXiv.2307.15818
license: unspecified
summary: RT-2 co-fine-tunes large pre-trained vision-language models (PaLI-X and PaLM-E)
  on robot trajectory data by representing actions as text tokens, achieving state-of-the-art
  manipulation performance and demonstrating emergent semantic reasoning capabilities
  not present in purely robot-data-trained policies.
why_important: Established the VLA paradigm as the dominant framework for robot foundation
  models by demonstrating that internet-scale pre-training knowledge transfers to
  physical robot control, enabling semantic generalization that prior robot-only trained
  policies cannot achieve.
tags:
- vla
- rt2
- web-knowledge
- robotic-control
- token-actions
---

## Summary

RT-2 (Robotic Transformer 2), presented at CoRL 2023, represents a decisive step toward treating robot control as a language modeling problem. Brohan et al. co-fine-tune two large pre-trained vision-language models—PaLI-X (55B parameters) and PaLM-E (562B parameters)—on a mixture of web image-text data and robot demonstration data, where robot actions are tokenized as strings of integers and appended to the model's text output space. This design enables the model to generate robot actions using the same autoregressive text generation machinery used for image captioning and visual question answering, requiring no architectural modifications to the underlying VLM. The robot data, comprising RT-1's dataset of approximately 130k demonstrations across 700+ tasks on 13 robot arms, is mixed with standard web VLM training data at a carefully tuned ratio to preserve language and visual reasoning capabilities while acquiring robot control competence.

The empirical evaluation demonstrates that RT-2 substantially outperforms RT-1 on standard manipulation tasks (a 66% relative improvement in success rate on novel task descriptions), but the most striking finding concerns emergent generalization. RT-2 successfully executes tasks specified through multi-step semantic reasoning—for example, "pick up the object that would be used to open a wine bottle" (identifying a corkscrew among other objects) or "move the banana to the trash"—that were never explicitly demonstrated in the robot training data. These capabilities appear to transfer from the model's web pre-training knowledge, where it learned object semantics, functional relationships, and common-sense task structure. Such reasoning is entirely absent in RT-1, which can only execute task specifications that closely match its training distribution.

The methodological contribution of RT-2 is the demonstration that action tokenization—representing discretized end-effector position and rotation deltas as tokens from the model's existing vocabulary—is sufficient for competent robot control despite the lossy discretization it introduces. The authors study the effect of discretization granularity, data mixing ratios, and model scale, finding that larger models generalize better on out-of-distribution task specifications. The paper also introduces a chain-of-thought prompting variant that explicitly generates intermediate reasoning steps before producing the action token, further improving success on tasks requiring multi-step logical inference.

## Why It Matters

RT-2 is arguably the single most important paper in establishing VLAs as the canonical architecture for robot foundation models. It provides the first compelling empirical evidence that semantic generalization—executing novel tasks through language reasoning rather than pattern matching—can be achieved in physical robot control by leveraging internet-scale pre-training. This shifted the field's thinking from "how do we train more diverse robot datasets?" toward "how do we best transfer knowledge from pre-trained VLMs into robot control?" and validated the VLA paradigm that subsequent systems including OpenVLA, Octo, and π0 all follow.

The paper also raised important questions that remain partially unresolved. How much does model scale contribute to emergent reasoning versus the quality of the robot data? Does chain-of-thought prompting reliably improve performance or does it sometimes introduce hallucinated intermediate steps? And can the VLA paradigm scale to contact-rich, dexterous, or long-horizon tasks where simple pick-and-place evaluation does not reveal the model's true limitations? These questions define the active research frontier in robot foundation models, and RT-2 remains the canonical reference that frames them.

| | |
|---|---|
| **Authors** | Brohan et al. |
| **Year** | 2023 |
| **Venue** | arXiv / CoRL 2023 |
| **Field** | Robotics |
| **Subfield** | Robot Foundation Models Vla |
| **Tasks** | vla, web-knowledge-transfer, robotic-control |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2307.15818.pdf){: .btn .btn--primary .btn--large}
