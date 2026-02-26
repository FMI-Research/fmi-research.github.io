---
title: 'LLaMA: Open and Efficient Foundation Language Models'
collection: papers
permalink: /papers/agi/llama_open_and_efficient_foundation_language_models/
date: '2023-02-27'
year: 2023
field: agi
subfield: llm-foundations-scaling
tasks:
- open-foundation-models
- efficiency
tier: 2
artifact_type: paper
venue: arXiv 2023
authors:
- Hugo Touvron
- Thibaut Lavril
- Gautier Izacard
- Xavier Martinet
authors_short: Touvron et al.
paperurl: https://arxiv.org/pdf/2302.13971.pdf
doi: 10.48550/arXiv.2302.13971
license: unspecified
summary: Introduces a family of 7B–65B parameter foundation models trained exclusively
  on publicly available data using an inference-optimal training paradigm—prioritizing
  more tokens over more parameters—that allows the 13B model to outperform GPT-3 (175B)
  on most benchmarks.
why_important: Catalyzed the open-weight LLM ecosystem by demonstrating that competitive
  foundation models require neither proprietary data nor massive parameter counts;
  directly enabled Alpaca, Vicuna, llama.cpp, and a generation of community-driven
  derivative work.
tags:
- open-weights
- llm
- efficiency
- foundation-models
---

## Summary

LLaMA introduces a family of foundation language models at four scales—7B, 13B, 33B, and 65B parameters—trained exclusively on publicly available text corpora including Common Crawl (filtered via a linear classifier), C4, GitHub code, Wikipedia (20 languages), Project Gutenberg books, ArXiv preprints, and StackExchange. The defining methodological choice is a departure from Chinchilla-optimal training: rather than training the largest feasible model to Chinchilla-optimal token counts, the LLaMA models are trained on 1T–1.4T tokens—substantially more than Chinchilla prescribes for their sizes—motivated by the observation that inference costs dominate deployment economics. A 13B model trained on more data can be cheaper to serve than a 65B model even if both achieve the same benchmark performance, because inference cost scales with active parameter count rather than training FLOP count.

The empirical results are striking: LLaMA-13B outperforms GPT-3 (175B) on most standard NLP benchmarks including BoolQ, PIQA, Winogrande, ARC, and HellaSwag, despite being over an order of magnitude smaller. LLaMA-65B is competitive with Chinchilla (70B) and PaLM (540B) on MMLU and BIG-Bench, and outperforms PaLM on tasks involving code and mathematical reasoning when chain-of-thought prompting is applied. The models are evaluated thoroughly on commonsense reasoning, reading comprehension, math word problems (GSM8K), and code generation (HumanEval), providing a wide and reproducible baseline.

Architecturally, LLaMA incorporates three modifications to the standard GPT-2 transformer that have since become near-universal in open-weight models: pre-normalization using RMSNorm (applied before each transformer sublayer rather than after, improving gradient stability), the SwiGLU activation function in the feed-forward layers (replacing ReLU, improving representational capacity per parameter), and rotary positional embeddings (RoPE) replacing learned absolute position embeddings (enabling extrapolation to longer contexts). These choices were informed by PaLM and GPT-NeoX, and their collective adoption by LLaMA established them as a de facto standard.

## Why It Matters

LLaMA's release—and the rapid subsequent leak of its weights—catalyzed the open-weight LLM ecosystem in a way that no prior release had achieved. Within weeks, the community had produced Alpaca (instruction-tuned on 52K GPT-3.5 distillation examples), Vicuna (fine-tuned on ShareGPT conversation data), and a dozen other derivatives. Critically, llama.cpp enabled 4-bit quantized inference on consumer CPUs and laptops, making LLaMA the first frontier-class model deployable without a GPU—a prerequisite for widespread experimentation outside well-resourced labs. This ecosystem has since grown to encompass hundreds of fine-tunes, domain-adapted variants (Code Llama, Med-LLaMA), and multimodal extensions (LLaVA), collectively constituting the most active open AI research community of 2023.

The inference-optimal training paradigm LLaMA introduced—prioritizing tokens over parameters given a fixed compute budget, with deployment costs as a primary constraint—was a conceptual shift that subsequent work validated and extended. It revealed that Chinchilla's compute-optimal prescriptions, while theoretically grounded, do not account for the fact that inference is typically performed millions of times while training is performed once; adjusting the optimization objective accordingly justifies training far below Chinchilla-optimal model sizes. This insight propagated directly into Mistral 7B, Llama 2, Phi, and essentially all subsequent small-model development, and continues to shape hardware and data investment decisions at scale.| | |
|---|---|
| **Authors** | Touvron et al. |
| **Year** | 2023 |
| **Venue** | arXiv 2023 |
| **Field** | Agi |
| **Subfield** | Llm Foundations Scaling |
| **Tasks** | open-foundation-models, efficiency |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2302.13971.pdf){: .btn .btn--primary .btn--large}
