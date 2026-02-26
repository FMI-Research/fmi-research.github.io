---
title: 'A Survey on Hallucination in Large Language Models: Principles, Taxonomy,
  Challenges, and Open Questions'
collection: papers
permalink: /papers/agi/a_survey_on_hallucination_in_large_language_models_principles_taxonomy_challenges_and_open_questions/
date: '2023-11-09'
year: 2023
field: agi
subfield: alignment-safety-evaluation
tasks:
- hallucination
- factuality
- evaluation
tier: 1
artifact_type: paper
venue: arXiv 2023
authors:
- Lei Huang
- Weijiang Yu
- Weitao Ma
- Weihong Zhong
authors_short: Huang et al.
paperurl: https://arxiv.org/pdf/2311.05232.pdf
doi: 10.48550/arXiv.2311.05232
license: unspecified
summary: Provides a structured taxonomy distinguishing factuality hallucination (claims
  contradicting verifiable world knowledge) from faithfulness hallucination (claims
  contradicting source context), and organizes causes across pre-training data quality,
  model architecture, and inference-time factors; reviews benchmarks such as TruthfulQA
  and FactScore alongside mitigation families including retrieval augmentation, factuality-
  aware decoding, and hallucination-aware training objectives.
why_important: Consolidated a rapidly diverging literature into a common vocabulary
  that subsequent factuality and reliability work has broadly adopted; the factuality-
  vs-faithfulness distinction in particular clarified why RAG reduces one form of
  hallucination while potentially introducing another, shaping how retrieval-augmented
  systems are evaluated.
tags:
- hallucination
- factuality
- survey
- reliability
---

## Summary

This survey establishes a principled taxonomy for LLM hallucination by introducing two orthogonal distinctions: *factuality hallucination* (model outputs contradict verifiable world knowledge, e.g., citing non-existent citations or incorrect dates) versus *faithfulness hallucination* (model outputs contradict the source context in grounded generation tasks such as summarization or RAG-based QA). Within these categories, the paper further distinguishes intrinsic hallucination (contradicting the source directly) from extrinsic hallucination (adding unverifiable information beyond the source). Causes are organized across three phases: pre-training data quality issues (noisy, contradictory, or outdated training corpora), model architecture limitations (attention mechanisms that fail to propagate distal facts), and inference-time factors (sampling temperature, nucleus sampling, repetition penalties). Benchmarks reviewed include TruthfulQA, FactScore, HaluEval, FaithDial, and BEGIN.

Empirically, the survey synthesizes findings from dozens of studies to highlight that hallucination is not a monolithic failure mode. Larger models can hallucinate more *confidently* even when they hallucinate *less frequently*, making confidence calibration a distinct concern from hallucination rate. Retrieval-augmented generation reduces factuality hallucination substantially but can introduce faithfulness hallucination when retrieved passages are incorrect or misleading. Chain-of-thought prompting reduces some categories of hallucination by externalizing intermediate reasoning, but can also propagate early errors through a reasoning chain, resulting in compounded hallucinations.

Mitigation strategies are organized into three families: retrieval-augmented approaches (reducing reliance on parametric memory), factuality-enhanced training (including data filtering, knowledge graph grounding, and hallucination-aware SFT), and decoding-time interventions (contrastive decoding, self-consistency, and factuality classifiers applied during generation). The survey concludes with a research agenda targeting automatic hallucination detection, fine-grained attribution, and hallucination-robust instruction tuning.

## Why It Matters

This survey consolidated a fragmented and rapidly growing literature under a shared vocabulary that subsequent factuality and reliability work has broadly adopted. The factuality-vs-faithfulness distinction in particular clarified why different mitigation strategies are needed for different failure modes — a RAG system that reduces factuality hallucination may simultaneously increase faithfulness hallucination if retrieval is imperfect — and shaped how retrieval-augmented systems are designed and evaluated in practice.

By framing hallucination as a multi-causal, multi-type failure rather than a single property, the paper set an important methodological precedent: that benchmarks targeting hallucination must specify *which type* of hallucination they measure, and that interventions must be evaluated against the specific failure mode they target. These principles continue to guide hallucination benchmark design and model evaluation, making this survey an essential entry point for researchers studying reliability, factuality, and grounding in language models.

| | |
|---|---|
| **Authors** | Huang et al. |
| **Year** | 2023 |
| **Venue** | arXiv 2023 |
| **Field** | Agi |
| **Subfield** | Alignment Safety Evaluation |
| **Tasks** | hallucination, factuality, evaluation |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2311.05232.pdf){: .btn .btn--primary .btn--large}
