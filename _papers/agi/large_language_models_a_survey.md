---
title: 'Large Language Models: A Survey'
collection: papers
permalink: /papers/agi/large_language_models_a_survey/
date: '2024-02-09'
year: 2024
field: agi
subfield: llm-foundations-scaling
tasks:
- survey
- model-families
- datasets
- evaluation
tier: 1
artifact_type: paper
venue: arXiv 2024
authors:
- Shervin Minaee
- Tomas Mikolov
- Jianfeng Gao
authors_short: Minaee et al.
paperurl: https://arxiv.org/pdf/2402.06196.pdf
doi: 10.48550/arXiv.2402.06196
license: unspecified
summary: A systematic survey of post-2022 large language models covering architecture
  families, training pipelines, augmentation methods, datasets, and evaluation practices
  across GPT, LLaMA, PaLM, Gemini, and related lineages.
why_important: Provides the field's most comprehensive public taxonomy of the modern
  LLM ecosystem, surfacing cross-cutting patterns in architecture, data, and evaluation
  that are not visible from individual model papers alone.
tags:
- survey
- llm
- scaling
- evaluation
---

## Summary

Minaee et al. provide a structured survey of the large language model landscape as it stood in early 2024, organizing the field along three primary axes: model families, training methodology, and evaluation. The survey covers decoder-only architectures (GPT-3/4, LLaMA, PaLM, Mistral, Falcon), encoder-decoder models (T5, FLAN-T5), and early multimodal extensions, tracing the lineage from BERT and GPT-2 through the post-ChatGPT proliferation. Pre-training objectives, tokenization strategies, positional encoding schemes (absolute, ALiBi, RoPE), and normalization choices are compared across families, providing a unified reference for architectural decisions that are otherwise scattered across dozens of individual papers.

On the empirical side, the survey synthesizes benchmark results across MMLU, BIG-Bench, HellaSwag, ARC, TruthfulQA, HumanEval, and GSM8K, documenting the rapid progression of state-of-the-art from GPT-3 (early 2020) through GPT-4 and its contemporaries. It catalogs the augmentation methods that have extended base model capabilities: retrieval-augmented generation (RAG), tool use and code execution, chain-of-thought prompting, and instruction fine-tuning. Post-training alignment techniques—SFT, RLHF, constitutional AI, and DPO—are discussed with coverage of their tradeoffs in helpfulness, safety, and generalization.

The methodological contribution lies in the taxonomy itself: the survey introduces a consistent framing for comparing models across dimensions that individual papers handle idiosyncratically, including training data composition, context length, multilingual coverage, and open-weight vs. proprietary accessibility. It also reviews evaluation infrastructure—automated benchmarking frameworks, human preference studies, and red-teaming practices—highlighting inconsistencies in how capability claims are substantiated across organizations.

## Why It Matters

The survey arrived at a moment when the LLM ecosystem was fragmenting rapidly across multiple major labs, model families, and licensing regimes, making it difficult even for active researchers to maintain a coherent mental map of the field. By providing a unified reference at this inflection point, the paper performs a genuine organizational service: enabling researchers entering the field—or pivoting into LLM applications—to locate their work in context without reading hundreds of primary papers. The structured comparison of model families is especially valuable for understanding why specific architectural choices (RoPE vs. ALiBi, GQA vs. MHA, SwiGLU vs. GeLU) propagated across the ecosystem.

The survey also surfaces important methodological gaps that individual model papers obscure: benchmark saturation (many leading models now score above 85% on MMLU, limiting its discriminative value), evaluation contamination risks (training data overlap with benchmark test sets), and the difficulty of measuring emergent capabilities that by definition are not predicted by smooth scaling curves. These gaps point toward active research directions including harder reasoning benchmarks, contamination detection methods, and standardized evaluation protocols—an agenda that subsequent efforts like the Open LLM Leaderboard and BIG-Bench Hard have partially addressed.

| | |
|---|---|
| **Authors** | Minaee et al. |
| **Year** | 2024 |
| **Venue** | arXiv 2024 |
| **Field** | Agi |
| **Subfield** | Llm Foundations Scaling |
| **Tasks** | survey, model-families, datasets, evaluation |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2402.06196.pdf){: .btn .btn--primary .btn--large}
