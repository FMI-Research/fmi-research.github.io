---
title: Training Compute-Optimal Large Language Models
collection: papers
permalink: /papers/agi/training_compute-optimal_large_language_models/
date: '2022-03-29'
year: 2022
field: agi
subfield: llm-foundations-scaling
tasks:
- scaling-laws
- data-compute-tradeoff
tier: 1
artifact_type: paper
venue: arXiv / NeurIPS 2022
authors:
- Jordan Hoffmann
- Sebastian Borgeaud
- Arthur Mensch
- Elena Buchatskaya
authors_short: Hoffmann et al.
paperurl: https://arxiv.org/pdf/2203.15556.pdf
doi: 10.48550/arXiv.2203.15556
license: unspecified
summary: Derives compute-optimal scaling laws showing that model size and training
  tokens should scale in roughly equal proportion (~20 tokens per parameter), demonstrating
  that prior large models such as GPT-3 and Gopher were significantly undertrained.
why_important: Reshaped how every major lab allocates compute budgets between parameters
  and data; directly motivated the inference-efficient training paradigm adopted by
  LLaMA and its successors.
tags:
- scaling-laws
- compute-optimal
- training
---

## Summary

Hoffmann et al. investigate the optimal allocation of a fixed compute budget between model size (parameters) and the number of training tokens. The earlier Kaplan et al. (2020) scaling laws—which informed GPT-3, Gopher, and Megatron-Turing NLG—suggested that parameters should scale faster than tokens, leading the community toward ever-larger models trained on comparatively modest datasets. This paper challenges that prescription using three independent empirical estimation approaches: (1) training a large set of models across a grid of sizes and token counts at fixed compute, (2) fitting IsoFLOP profiles that vary model size while holding total compute constant, and (3) fitting a parametric functional form to the joint loss surface over model size and token count. All three approaches converge on a qualitatively different conclusion from Kaplan et al.: for compute-optimal training, model size and training tokens should scale in roughly equal proportion, with approximately 20 tokens per parameter being near-optimal.

To validate the derived laws, the authors train Chinchilla—a 70B-parameter model trained on 1.4T tokens—under the same compute budget as Gopher (280B parameters, 300B tokens). Chinchilla outperforms Gopher, GPT-3 (175B), Jurassic-1 (178B), and Megatron-Turing NLG (530B) on nearly every downstream evaluation, including MMLU, BIG-Bench, and the Massive Text Embedding Benchmark. The result is striking: a model roughly 4× smaller than Gopher, trained on nearly 5× as many tokens, achieves uniformly better performance—demonstrating that all of those larger models were substantially undertrained for their compute budgets.

The methodological innovation is the three-pronged estimation strategy, which reduces the risk that any single experimental design biases the conclusions. The paper is also notable for fitting a continuous parametric loss model of the form L(N, D) = E + A/N^α + B/D^β, where N is parameter count and D is token count, which enables extrapolation to arbitrary compute budgets. This framework gives practitioners a principled tool for planning training runs rather than relying on ad hoc heuristics.

## Why It Matters

The Chinchilla scaling laws immediately and durably reshaped how frontier labs allocate compute budgets. Within months, the major implication was internalized: GPT-3, Gopher, and similar models were substantially undertrained, and the same performance could have been achieved at a fraction of the parameter count by simply training on more data. This insight directly motivated LLaMA (7B–65B models trained on 1T–1.4T tokens, far more than Chinchilla-optimal for those sizes) and has since become the default planning heuristic for nearly every subsequent pretraining run at scale. The practical consequence was a shift in research investment from model architecture toward data curation, filtering, and sourcing.

Despite its influence, the Chinchilla analysis carries important caveats that subsequent work has surfaced. Most significantly, it optimizes for minimizing training-time cross-entropy loss subject to a compute constraint, without accounting for inference cost: a 70B model is considerably more expensive to serve than a 7B model even if both achieve the same loss at their respective Chinchilla-optimal training budgets. This observation motivated the inference-optimal paradigm of LLaMA—training smaller models on far more data than Chinchilla prescribes—which dominates open-weight model development. Additionally, the scaling laws are fit on a specific loss metric (next-token prediction on held-out text) and may not transfer to downstream task performance or human preference, an increasingly important concern as post-training alignment diverges base model loss from final deployed quality.

| | |
|---|---|
| **Authors** | Hoffmann et al. |
| **Year** | 2022 |
| **Venue** | arXiv / NeurIPS 2022 |
| **Field** | Agi |
| **Subfield** | Llm Foundations Scaling |
| **Tasks** | scaling-laws, data-compute-tradeoff |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2203.15556.pdf){: .btn .btn--primary .btn--large}
