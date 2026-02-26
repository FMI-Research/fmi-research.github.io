---
title: A Survey on Multimodal Large Language Models for Autonomous Driving
collection: papers
permalink: /papers/autonomous-driving/a_survey_on_multimodal_large_language_models_for_autonomous_driving/
date: '2023-11-20'
year: 2023
field: autonomous-driving
subfield: llm-vla-autonomous-driving
tasks:
- survey
- llm-for-driving
- multimodal
tier: 1
artifact_type: paper
venue: WACV 2024 Workshop
authors:
- Can Cui
- Yunsheng Ma
- Xu Cao
- Wenqian Ye
- Yang Zhou
- Kaizhao Liang
- Jintai Chen
- Juanwu Lu
- Zichong Yang
- Kuei-Da Liao
- Tianren Gao
- Erlong Li
- Tang-Hsien Chang
- Qing Lian
- Zhengzhong Tu
- Tianheng Cheng
- Cheng Ruan
- Rui Chen
- Qi Ye
authors_short: Cui et al.
paperurl: https://arxiv.org/pdf/2311.12320.pdf
doi: 10.48550/arXiv.2311.12320
license: unspecified
summary: A systematic survey of multimodal large language model integration across
  the full autonomous driving stack — from perception-level grounding and prediction
  through LLM-based motion planning and natural language explanation — covering datasets,
  models, and open challenges at this rapidly evolving intersection.
why_important: This was the first comprehensive survey to document and taxonomize
  the integration of MLLMs into autonomous driving across all pipeline stages, providing
  an early structured map of a field that has since expanded rapidly with work including
  DriveLM, DriveVLM, and Senna.
tags:
- survey
- llm
- autonomous-driving
- multimodal
- vla
---

## Summary

Cui et al. survey the growing body of work that applies multimodal large language models (MLLMs) — systems combining large language model backbones with visual encoders — to autonomous driving. The paper proposes a four-tier taxonomy aligned with the classical AD pipeline: (1) *Perception-level grounding*, where MLLMs are used for open-vocabulary object detection, scene description, and visual question answering over driving scenes; (2) *Prediction*, where language models provide priors over agent intent and future state from natural language scene descriptions; (3) *Motion planning*, where LLM or VLM-based systems generate trajectory waypoints, high-level commands, or driving decisions in natural language; and (4) *Explanation and QA*, where models provide post-hoc or inline natural language justifications for driving decisions. This taxonomy is applied to over 60 papers spanning GPT-4V applied to driving, LLaVA-based scene understanding, RT-2-style visuomotor policies, and specialized driving language models.

A significant contribution is the structured review of datasets developed at the LLM–AD intersection. nuScenes-Text and nuScenes-QA provide language annotations layered on the nuScenes sensor data, enabling vision-language alignment training. DriveLM-nuScenes provides graph-structured perception–prediction–planning QA pairs. The CARLA-based Talk2Drive and nuPrompt datasets are reviewed for their role in instruction-following driving benchmarks. On the model side, the survey covers GPT-4V applied in a zero-shot prompting regime for driving scene analysis, LLaVA fine-tuned on driving imagery, DriveGPT4 (pairing video and control commands), and LanguageMPC (using LLM-generated high-level plans to parameterize a low-level MPC controller). The review notes the heterogeneity of evaluation: some works measure trajectory L2, others use language-based metrics (BLEU, CIDEr), and few standardize across both.

Beyond cataloguing individual methods, the survey surfaces several systemic observations. First, the field exhibits a strong granularity mismatch: LLMs operate at the level of semantic descriptions and discrete commands, while planners require precise continuous trajectory outputs; bridging this gap without losing either semantic richness or geometric precision is unsolved. Second, most evaluated models use nuScenes or CARLA-based datasets, raising questions about geographic and cultural generalizability, especially for models that inherit biases from internet-scale LLM pretraining. Third, explainability is identified as a double-edged feature: language-based justifications improve human interpretability and regulatory transparency, but current systems lack grounding mechanisms that guarantee the generated explanation reflects actual internal model reasoning — a form of post-hoc rationalization that the survey explicitly flags as a safety concern.

## Why It Matters

Published at the WACV 2024 workshop dedicated to this intersection, this survey arrived at a moment when the field was fragmenting rapidly across perception-centric VLMs (GPT-4V, LLaVA), driving-specific instruction-following systems (DriveGPT4, LanguageMPC), and graph-VQA frameworks (DriveLM). By providing a shared taxonomy and organizing these contributions into coherent themes, it gave the community a common vocabulary for discussing what "LLM for AD" means in different contexts. Its dataset catalogue became a reference for practitioners choosing which language-annotated driving dataset to adopt. Subsequent surveys in 2024 built directly on its four-tier structure, extending coverage to systems like DriveVLM, Senna, and Agent-Driver that emerged after this survey's cutoff.

As with any survey in a rapidly developing area, temporal scope is the main limitation: the work was written before DriveVLM's chain-of-thought planning pipeline, Senna's VLM-as-intent-predictor paradigm, and the broader chain-of-thought driving approaches that defined 2024 were published. The survey's treatment of safety-critical evaluation is brief — it does not systematically review how proposed LLM-AD systems handle distribution shift, adversarial inputs, or out-of-distribution scenarios, which are first-order concerns for deployment. The evaluation heterogeneity the survey identifies remains unresolved: there is still no community consensus on how to jointly evaluate language quality and trajectory quality in a single unified metric, and NAVSIM's PDMS and DriveLM's graph-VQA accuracy address different slices of this problem without a unifying solution.

| | |
|---|---|
| **Authors** | Cui et al. |
| **Year** | 2023 |
| **Venue** | WACV 2024 Workshop |
| **Field** | Autonomous Driving |
| **Subfield** | Llm Vla Autonomous Driving |
| **Tasks** | survey, llm-for-driving, multimodal |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2311.12320.pdf){: .btn .btn--primary .btn--large}
