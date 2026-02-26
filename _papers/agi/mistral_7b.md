---
title: Mistral 7B
collection: papers
permalink: /papers/agi/mistral_7b/
date: '2023-10-10'
year: 2023
field: agi
subfield: llm-foundations-scaling
tasks:
- efficiency
- attention-variants
tier: 2
artifact_type: paper
venue: arXiv 2023
authors:
- Albert Q. Jiang
- Alexandre Sablayrolles
- Arthur Mensch
authors_short: Jiang et al.
paperurl: https://arxiv.org/pdf/2310.06825.pdf
doi: 10.48550/arXiv.2310.06825
license: unspecified
summary: Presents a 7.3B-parameter model combining grouped-query attention and sliding
  window attention to reduce inference memory and extend effective context, achieving
  performance that exceeds LLaMA 2 13B and rivals LLaMA 2 34B across all evaluated
  benchmarks while using an Apache 2.0 license.
why_important: Demonstrated that architectural efficiency innovations decisively outweigh
  raw parameter count at the 7B scale; its permissive licensing and benchmark results
  made it one of the most widely adopted community fine-tuning bases and reignited
  interest in inference-efficient small models.
tags:
- llm
- efficiency
- attention
- small-models
---

## Summary

Mistral 7B is a 7.3B-parameter dense transformer language model from Mistral AI that incorporates two attention mechanism innovations absent in the LLaMA series: grouped-query attention (GQA) and sliding window attention (SWA). GQA partitions the query heads into groups that share a single key-value head, reducing the KV cache memory footprint during inference without materially degrading model quality—the same technique applied selectively at 34B and 70B in Llama 2, here applied at 7B scale. SWA restricts each attention head to attend over a local window of W tokens (W=4096 in Mistral 7B), rather than the full context sequence, reducing the theoretical complexity of attention from O(n²) toward O(n·W). Through the depth of the transformer stack, information can propagate across the full context via multiple layers even when individual layers attend locally, yielding an effective receptive field substantially larger than W for any given token.

Empirically, Mistral 7B outperforms LLaMA 2 13B on every benchmark evaluated—despite being roughly half the parameter count—and matches or exceeds LLaMA 2 34B on many tasks. On coding (HumanEval: 30.5%), mathematics (passing rate on MATH subset), and reading comprehension (TriviaQA), Mistral 7B sets new state-of-the-art results at the ≤7B scale. A fine-tuned instruction variant (Mistral 7B Instruct v0.1), trained on publicly available instruction datasets, achieves an MT-Bench score of 6.84 compared to Llama 2 13B Chat's 6.27, demonstrating that the instruction-following quality advantage persists through fine-tuning.

A notable systems contribution is the deployment approach: the paper presents an implementation using sliding-window KV cache with a rolling buffer that bounds memory usage to a fixed O(W) window regardless of input length, enabling efficient batched long-document processing without quadratic memory growth. This implementation, combined with flash attention and xformers integration, enables Mistral 7B to run efficiently on a single consumer-grade GPU. The model was released under Apache 2.0—a deliberately permissive license that contrasts with LLaMA's more restrictive research license—signaling Mistral AI's positioning strategy and enabling unrestricted commercial deployment.

## Why It Matters

Mistral 7B decisively demonstrated that architectural efficiency innovations can overcome the performance disadvantage of a smaller parameter count, reframing the dominant "bigger is better" narrative in open-weight model development. By outperforming a model nearly twice its size, it validated that inference-efficient architectures—not just Chinchilla-optimal training—are a primary lever for the performance-cost frontier. This sparked renewed investment in sub-10B model research (Phi-2, Gemma 2B, SmolLM), all of which cite or build on Mistral's demonstrations. The Apache 2.0 licensing decision also had substantial ecosystem consequences: it made Mistral 7B the first frontier-class model without any restriction on commercial use, enabling its adoption in production systems by organizations that could not accept the LLaMA research license.

The sliding window attention mechanism, while effective for its context range, carries a fundamental limitation: tasks requiring precise global attention over very long documents (e.g., cross-reference resolution between distant passages) may degrade because information must propagate through many layers of local windows rather than being directly attended to. This limitation motivated Mixtral and later Mistral models to expand context handling and use alternative positional embedding strategies. Mistral 7B also highlighted the growing importance of benchmark-beyond-scale evaluation: while it achieves remarkable results on standard NLP benchmarks, subsequent work on real-world task performance showed more mixed results, motivating development of more deployment-realistic evaluation frameworks.

| | |
|---|---|
| **Authors** | Jiang et al. |
| **Year** | 2023 |
| **Venue** | arXiv 2023 |
| **Field** | Agi |
| **Subfield** | Llm Foundations Scaling |
| **Tasks** | efficiency, attention-variants |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2310.06825.pdf){: .btn .btn--primary .btn--large}
