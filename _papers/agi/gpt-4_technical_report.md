---
title: GPT-4 Technical Report
collection: papers
permalink: /papers/agi/gpt-4_technical_report/
date: '2023-03-15'
year: 2023
field: agi
subfield: llm-foundations-scaling
tasks:
- multimodal-llm
- evaluation
- system-report
tier: 1
artifact_type: paper
venue: arXiv 2023
authors:
- OpenAI
authors_short: OpenAI
paperurl: https://arxiv.org/pdf/2303.08774.pdf
doi: 10.48550/arXiv.2303.08774
license: unspecified
summary: Presents GPT-4 as a large multimodal model accepting image and text inputs,
  documenting state-of-the-art benchmark performance across professional exams and
  academic tasks while introducing predictive scaling as a training risk-reduction
  strategy.
why_important: Established the modern template for frontier model capability disclosure
  and anchored the performance bar that subsequent models across all labs are measured
  against; its multimodal evaluation suite shaped the evaluation agenda for the field.
tags:
- llm
- multimodal
- system-report
- benchmarks
---

## Summary

The GPT-4 Technical Report presents OpenAI's large-scale multimodal model capable of processing both image and text inputs and producing text outputs. Architecturally and in terms of training details—model size, training data composition, compute budget, and infrastructure—the paper is deliberately opaque, a departure from earlier OpenAI publications. Instead, the report focuses on three areas: empirical evaluation across a broad suite of professional and academic benchmarks, a study of scaling predictability, and safety and alignment methodology. The evaluation suite includes professional licensing examinations (Uniform Bar Exam: 90th percentile, USMLE, LSAT, GRE), academic benchmarks (MMLU: 86.4%, HellaSwag: 95.3%, ARC-Challenge: 96.3%), and specialized coding and mathematical assessments. Across virtually all evaluated tasks, GPT-4 substantially improves on GPT-3.5.

A key scientific contribution is the predictive scaling study: OpenAI demonstrates that GPT-4's final cross-entropy loss on a held-out evaluation set could be accurately predicted from training runs consuming orders of magnitude less compute, using scaling laws fit to intermediate checkpoints. This "pre-flight" capability—forecasting final model loss before committing to full-scale training—has significant practical and safety implications, suggesting that catastrophic performance degradation at scale can potentially be detected early. The paper also extensively documents a red-teaming and alignment process conducted before deployment, including adversarial testing for harmful content generation, misinformation, and dangerous capability elicitation, and the use of RLHF-based alignment to reduce policy violations.

The multimodal capability—accepting images as input—is evaluated on visual question answering, chart and diagram comprehension, scientific figure interpretation, and document understanding tasks, where GPT-4V achieves state-of-the-art performance on existing benchmarks. Importantly, the paper introduces capability evaluations adapted from human professional contexts (e.g., interpreting a tax form image and answering legal questions about it), which more faithfully approximate real-world deployment scenarios than standard VQA benchmarks.

## Why It Matters

GPT-4's technical report established a new and contested template for frontier capability disclosure: extensive empirical evidence paired with minimal scientific transparency. The performance claims across professional licensing exams anchored the public discourse on LLM capability for the subsequent two years, setting the targets against which every subsequent model—Gemini, Claude, LLaMA 3, and many others—has been compared. The bar exam and MMLU results became de facto capability thresholds, and the evaluation methodology (few-shot evaluation on standardized tests) propagated broadly through the field's benchmarking infrastructure. Simultaneously, the opacity of the report sparked significant debate about scientific reproducibility and the responsibilities of frontier AI labs, contributing to policy discussions around mandatory disclosure.

The report also foregrounded enduring limitations that the community has not resolved. GPT-4 continues to hallucinate with confidence, can be manipulated through adversarial jailbreaks, and exhibits knowledge cutoffs and inconsistent calibration across domains. The gap between its performance on standardized academic benchmarks and reliability on open-ended real-world tasks became a central critique of benchmark-centric evaluation. The multimodal capability, while impressive on structured tasks, exposed weaknesses in spatial reasoning and fine-grained visual understanding that remain active research challenges. Together, these limitations catalyzed a generation of follow-on work in evaluation methodology, hallucination mitigation, and robust multimodal architectures.

| | |
|---|---|
| **Authors** | OpenAI |
| **Year** | 2023 |
| **Venue** | arXiv 2023 |
| **Field** | Agi |
| **Subfield** | Llm Foundations Scaling |
| **Tasks** | multimodal-llm, evaluation, system-report |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2303.08774.pdf){: .btn .btn--primary .btn--large}
