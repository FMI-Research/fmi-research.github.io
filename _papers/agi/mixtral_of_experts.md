---
title: Mixtral of Experts
collection: papers
permalink: /papers/agi/mixtral_of_experts/
date: '2024-01-08'
year: 2024
field: agi
subfield: llm-foundations-scaling
tasks:
- moe
- sparse-activation
- efficiency
tier: 2
artifact_type: paper
venue: arXiv 2024
authors:
- Albert Q. Jiang
- Alexandre Sablayrolles
- Antoine Roux
authors_short: Jiang et al.
paperurl: https://arxiv.org/pdf/2401.04088.pdf
doi: 10.48550/arXiv.2401.04088
license: unspecified
summary: Presents Mixtral 8×7B, a sparse mixture-of-experts transformer selecting
  2 of 8 expert FFN networks per token, yielding ~12.9B active parameters from a 46.7B
  total parameter pool; it matches or outperforms LLaMA 2 70B and GPT-3.5 while using
  6× fewer active parameters at inference.
why_important: Made sparse MoE architectures practically accessible to the open-weight
  community and provided compelling evidence that active-parameter efficiency unlocks
  a qualitatively different performance-cost frontier, directly influencing the design
  of subsequent open MoE models and accelerating adoption of conditional computation
  in frontier systems.
tags:
- moe
- sparse-activation
- efficiency
- llm
---

## Summary

Mixtral 8×7B is a sparse mixture-of-experts (SMoE) language model in which each transformer layer replaces the single feedforward network with 8 independent expert FFN networks, selecting 2 per token via a learned top-2 gating function. The total parameter count is approximately 46.7B, but only 12.9B parameters are active for any given token—making per-token inference cost comparable to a 12.9B dense model while the full model can draw on the representational capacity of 46.7B parameters. The architecture reuses the Mistral 7B backbone for the attention layers (including sliding window attention and GQA) and inserts MoE into the FFN layers only, maintaining the well-understood attention dynamics while concentrating the computational efficiency gains in the FFN sublayer.

The routing mechanism is a learned linear gate applied to the hidden state at each layer, producing expert selection logits that are softmax-normalized and thresholded to the top-K=2 experts. A load-balancing auxiliary loss penalizes routing distributions that concentrate tokens on a subset of experts, encouraging utilization diversity during training. Empirically, analyses of expert utilization show that experts tend to specialize by semantic domain and syntactic structure—though not cleanly—and that the specialization patterns shift across layers. Mixtral 8×7B matches or outperforms LLaMA 2 70B and GPT-3.5 on most standard benchmarks including MMLU (70.6%), HellaSwag (86.7%), Winogrande (81.2%), and GSM8K (74.4%), while requiring roughly 6× fewer active parameters at inference. Mixtral 8×7B Instruct (fine-tuned on public instruction datasets using DPO) outperforms GPT-3.5 Turbo, Gemini Pro, and Claude 2.1 on MT-Bench, with particularly strong multilingual performance attributable to the larger effective parameter pool.

The paper supports a 32K token context window—identical to Mistral 7B—and implements efficient inference via grouped expert batching, where tokens routed to the same expert within a batch can share compute. This batching strategy partially ameliorates the increased memory bandwidth requirements of loading 8 expert weight matrices versus a single FFN. Mixtral 8×7B was released under Apache 2.0 alongside its instruction-tuned variant, and the model weights are compatible with the Mistral inference stack.

## Why It Matters

Mixtral provided the most compelling publicly available demonstration that sparse MoE architectures can match dense-model quality at a fraction of inference cost, making conditional computation practically accessible to the open-weight community. Prior open MoE work (Switch Transformer, ST-MoE) existed primarily in academic settings without competitive downstream performance at the model quality levels practitioners required. Mixtral's competitive performance against LLaMA 2 70B at 12.9B active parameters validated MoE as a genuine alternative to dense scaling, and its release directly accelerated adoption of MoE in subsequent open models (Qwen MoE, DeepSeek-MoE, OLMoE) and contributed to the architectural choices of proprietary frontier systems including reportedly GPT-4 itself.

Mixtral also surfaced persistent engineering and research challenges of sparse MoE that remain active problems. Expert load balancing is fragile: the auxiliary loss must be carefully tuned to prevent expert collapse (where a few experts capture nearly all tokens) without causing the loss to dominate the language modeling objective. The total memory footprint of 46.7B parameters—while only 12.9B are active per forward pass—means the full model must reside in GPU memory, requiring high-memory-tier hardware (8×A100 40GB or equivalent) that is not universally accessible. Routing under distribution shift (when inference-time inputs differ significantly from training distribution) can degrade expert utilization patterns in ways that hurt performance. These challenges have motivated research into fine-grained MoE (more, smaller experts with K>2), expert merging for compression, and learned routing strategies beyond top-K selection.

| | |
|---|---|
| **Authors** | Jiang et al. |
| **Year** | 2024 |
| **Venue** | arXiv 2024 |
| **Field** | Agi |
| **Subfield** | Llm Foundations Scaling |
| **Tasks** | moe, sparse-activation, efficiency |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2401.04088.pdf){: .btn .btn--primary .btn--large}
