---
title: 'C-Eval: A Multi-Level Multi-Discipline Chinese Evaluation Suite for Foundation
  Models'
collection: papers
permalink: /papers/agi/c-eval_a_multi-level_multi-discipline_chinese_evaluation_suite_for_foundation_models/
date: '2023-05-14'
year: 2023
field: agi
subfield: alignment-safety-evaluation
tasks:
- chinese-evaluation
- benchmarks
- multilingual
tier: 2
artifact_type: paper
venue: arXiv / NeurIPS 2023
authors:
- Yuzhen Huang
- Yuzhuo Bai
- Zhihao Zhu
- Junlei Zhang
authors_short: Huang et al.
paperurl: https://arxiv.org/pdf/2305.08322.pdf
doi: 10.48550/arXiv.2305.08322
license: unspecified
summary: C-Eval comprises 13,948 expert-verified multiple-choice questions spanning
  52 disciplines across four educational levels (middle school, high school, college,
  and professional certification), sourced from standardized Chinese examinations;
  it includes a C-Eval-Hard subset targeting STEM reasoning and provides both few-
  shot and zero-shot evaluation protocols, enabling systematic analysis of how model
  scale, Chinese corpus ratio, and chain-of-thought prompting interact.
why_important: Established the first rigorous, fine-grained Chinese-language evaluation
  standard for foundation models, exposing large performance gaps between Chinese-
  specific models and general English-dominant models on professional and STEM tasks;
  it set a precedent for culturally grounded multilingual benchmarking that motivated
  subsequent Chinese benchmarks and broader non-English evaluation infrastructure.
tags:
- chinese
- evaluation
- benchmarks
- multilingual
---

## Summary

C-Eval is a Chinese-language evaluation suite comprising 13,948 multiple-choice questions spanning 52 subjects across four educational levels: middle school, high school, university, and professional certification (including law, accounting, medicine, and engineering licensure). All questions are sourced from publicly available Chinese standardized examinations, verified by human experts for correctness and difficulty calibration, and presented in standard Mandarin Chinese. The benchmark includes a C-Eval-Hard subset of 3,456 questions focused on STEM disciplines (mathematics, physics, chemistry, and logic), where reasoning depth rather than recall is the primary challenge. The evaluation protocol supports both zero-shot and five-shot settings with chain-of-thought prompting options for Hard tasks.

The key empirical findings establish a clear performance landscape at release. GPT-4 achieves approximately 68.7% overall accuracy (vs. ~54% human-comparable baseline on professional exams), while most open-source models of the period fall in the 35–50% range. Chinese-specific models such as ChatGLM-6B significantly underperform larger general models despite task-language alignment, revealing that pre-training corpus composition matters more than language match alone. Professional-level questions expose the largest gaps: most models perform near-random-chance on accounting and law exams. Chain-of-thought prompting yields meaningful gains on C-Eval-Hard but negligible improvement on recall-dominated subjects, quantifying where reasoning-based prompting strategies are effective.

Methodologically, the paper conducts systematic ablations over model scale, Chinese pre-training data fraction, and prompting strategy, showing that Chinese corpus proportion has a diminishing-returns relationship with performance — models require substantial Chinese pre-training data to reach threshold competence, but beyond that threshold, scale and general capability dominate. The benchmark design explicitly rejects machine translation of English questions, ensuring that cultural and linguistic specificity of Chinese domain knowledge (e.g., Chinese legal statutes, Mandarin grammar) is preserved.

## Why It Matters

C-Eval established the first rigorous, multi-discipline Chinese evaluation standard for foundation models and exposed fundamental gaps in how well general-purpose English-dominant models transfer to Chinese professional knowledge. Its release catalyzed rapid iteration among Chinese LLM developers (e.g., Baichuan, Qwen, InternLM), who adopted C-Eval as a primary development benchmark, making it a de facto standard for tracking Chinese LLM progress.

The benchmark's design philosophy — grounding evaluation in actual standardized examinations rather than curated or machine-translated datasets — became a template for subsequent region-specific benchmarks and raised the bar for cultural authenticity in multilingual evaluation. Its demonstration that professional-level knowledge is much harder than general subject knowledge for LLMs also sharpened research focus on domain adaptation, long-context professional reasoning, and retrieval-augmented approaches for high-stakes knowledge tasks.

| | |
|---|---|
| **Authors** | Huang et al. |
| **Year** | 2023 |
| **Venue** | arXiv / NeurIPS 2023 |
| **Field** | Agi |
| **Subfield** | Alignment Safety Evaluation |
| **Tasks** | chinese-evaluation, benchmarks, multilingual |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2305.08322.pdf){: .btn .btn--primary .btn--large}
