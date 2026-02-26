---
title: The Llama 3 Herd of Models
collection: papers
permalink: /papers/agi/the_llama_3_herd_of_models/
date: '2024-07-31'
year: 2024
field: agi
subfield: llm-foundations-scaling
tasks:
- long-context
- open-foundation-models
- multimodal
tier: 2
artifact_type: paper
venue: arXiv 2024
authors:
- Meta AI
authors_short: Meta AI
paperurl: https://arxiv.org/pdf/2407.21783.pdf
doi: 10.48550/arXiv.2407.21783
license: unspecified
summary: Introduces the Llama 3 model family at 8B, 70B, and 405B scales trained on
  15.6T tokens with a rigorously curated data pipeline, 128K-token long-context support,
  and a sophisticated post-training stack combining SFT, rejection sampling, DPO,
  and PPO that brings the 405B model to parity with GPT-4 across broad benchmarks.
why_important: The first time an openly released model matched closed-frontier performance
  at scale, fundamentally shifting competitive dynamics between open and closed AI
  development and validating that data quality investment can substitute for incremental
  parameter scaling.
tags:
- open-weights
- llm
- long-context
- multimodal
---

## Summary

The Llama 3 herd comprises Meta's third generation of openly released foundation models, with dense transformer architectures at 8B, 70B, and 405B parameters, and multimodal extensions supporting image understanding. The flagship Llama 3.1 405B model is pretrained on approximately 15.6 trillion tokens—more than 7× the Llama 2 pretraining corpus—using a meticulously curated data pipeline that applies multiple rounds of quality filtering, deduplication, domain classification, and safety filtering before any data enters the training set. Long-context capability is extended to 128K tokens through a continued pretraining stage that gradually extends the context window using modified RoPE scaling (RoPE ABF), followed by additional training on synthetically generated and curated long-context data. The paper provides unusually detailed engineering disclosure of the training infrastructure: a custom parallelism strategy combining 4D parallelism (tensor, pipeline, context, and data parallel dimensions), gradient checkpointing, and FP8 quantization during training.

Empirically, Llama 3.1 405B achieves near-parity with GPT-4 and Claude 3.5 Sonnet on a wide range of benchmarks: MMLU (87.3%), GPQA Graduate (51.1%), HumanEval (89.0%), GSM8K (96.8%), and MATH (73.8%). This represents the first time an open-weight model has broadly matched the closed-frontier across a standard academic evaluation suite. The 8B and 70B models also substantially outperform their Llama 2 counterparts and rival the performance Llama 2 70B only achieved at 70B with just 8B parameters—attributable largely to the dramatically larger and higher-quality training dataset. The post-training pipeline combines supervised fine-tuning, rejection sampling, direct preference optimization (DPO), and proximal policy optimization (PPO) in an iterative procedure that the paper terms "iterative post-training."

The architectural changes relative to Llama 2 are modest but carefully chosen: grouped-query attention (GQA) is now applied uniformly across all model sizes (not just 34B+), the vocabulary is expanded from 32K to 128K tokens (greatly improving multilingual and code tokenization efficiency), and the model uses a new tokenizer trained on a multilingual corpus. The data quality pipeline is the primary methodological novelty: a suite of trained classifiers (quality, topic, domain, safety) and an LLM-based quality filter collectively select approximately 15T tokens from a much larger raw web crawl, achieving a data quality threshold that the paper argues is more impactful than architectural innovation at this stage of scaling.

## Why It Matters

Llama 3's release fundamentally altered the competitive dynamics between open and closed frontier AI development. The 405B model's parity with GPT-4 validated the thesis—contested by many in the field—that open-weight training at scale can match proprietary systems given sufficient data quality and training investment. This validation had downstream effects: it raised the bar for what "closed" labs need to offer beyond raw capability (such as reliability, RLHF quality, and multimodal performance), and it enabled a wave of downstream research building on a genuinely frontier-class openly available base model. The derivative ecosystem—fine-tunes, quantized versions (GGUF, GPTQ, AWQ), API wrappers, and research papers using Llama 3 as a backbone—began appearing within days of release.

The paper also raises important questions about what "open" means at frontier scale. A 405B dense model at full BF16 precision requires approximately 8 A100 80GB GPUs for inference, placing it out of reach for most academic labs and many smaller companies—making the model practically "open" only to organizations with significant GPU infrastructure. This tension between openness in principle and accessibility in practice has prompted a rethinking of what the open-weight movement can realistically deliver at the frontier. The multimodal extensions, while demonstrated in the paper, initially lagged behind GPT-4V and Gemini on complex visual reasoning, pointing to the difficulty of matching closed multimodal frontier models where proprietary data collection pipelines (for image-text pairs, video, and audio) represent a significant advantage.

| | |
|---|---|
| **Authors** | Meta AI |
| **Year** | 2024 |
| **Venue** | arXiv 2024 |
| **Field** | Agi |
| **Subfield** | Llm Foundations Scaling |
| **Tasks** | long-context, open-foundation-models, multimodal |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2407.21783.pdf){: .btn .btn--primary .btn--large}
