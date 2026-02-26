---
title: Qwen2.5 Technical Report
collection: papers
permalink: /papers/agi/qwen2.5_technical_report/
date: '2024-12-19'
year: 2024
field: agi
subfield: llm-foundations-scaling
tasks:
- multilingual
- post-training
tier: 2
artifact_type: paper
venue: arXiv 2024
authors:
- Qwen Team
- Alibaba Group
authors_short: Qwen Team
paperurl: https://arxiv.org/pdf/2412.15115.pdf
doi: 10.48550/arXiv.2412.15115
license: unspecified
summary: Presents the Qwen2.5 model family (0.5B–72B) pretrained on 18T tokens with
  a 152K-token vocabulary optimized for multilingual and code coverage, achieving
  competitive or superior performance to LLaMA 3.1 70B at equivalent scale via a post-training
  pipeline combining DPO, online RLHF, and synthetic long-context data construction.
why_important: Represents the maturation of Chinese-origin open-weight models into
  global frontier competitiveness and demonstrates that specialized sub-families (Qwen2.5-Math,
  Qwen2.5-Coder) via domain-curated pretraining can substantially exceed general-purpose
  model performance, pointing toward modular specialization as a scaling strategy.
tags:
- multilingual
- llm
- post-training
- chinese-models
---

## Summary

The Qwen2.5 technical report introduces Alibaba's third-generation family of open-weight language models, spanning a parameter range from 0.5B to 72B for the general-purpose series, alongside specialized sub-families for coding (Qwen2.5-Coder, 0.5B–32B) and mathematics (Qwen2.5-Math, 1.5B–72B). The base models are pretrained on approximately 18 trillion tokens—a substantial increase over the Qwen2 corpus—with systematic improvements to data quality, composition, and multilingual coverage. The vocabulary is expanded to 152K tokens (from 151K in Qwen2), primarily to improve tokenization efficiency for source code, mathematical expressions, and non-Latin scripts. The training data pipeline emphasizes domain-proportional sampling with quality-based upweighting: a suite of trained classifiers rates documents for educational value, code quality, and mathematical rigor, and high-scoring documents receive increased sampling weight during pretraining.

Empirically, Qwen2.5-72B achieves competitive performance against the frontier at equivalent scale: 86.0% on MMLU, 79.5% on MMLU-Pro, 83.1% on MATH, and 86.6% on HumanEval, outperforming LLaMA 3.1 70B across most benchmarks and approaching LLaMA 3.1 405B on mathematical and coding tasks despite being roughly 5× smaller. The specialized sub-models achieve particularly striking results: Qwen2.5-Math-72B surpasses GPT-4 on MATH (85.9% vs. ~72%), and Qwen2.5-Coder-32B achieves competitive performance with frontier code generation models on HumanEval and LiveCodeBench. The instruction-tuned variants (Qwen2.5-72B-Instruct) consistently outperform Llama 3.1 70B Instruct and match Mistral Large 2 on multi-turn conversation, instruction following, and chat quality benchmarks.

The post-training pipeline involves multiple stages of increasing sophistication: initial supervised fine-tuning on a curated mixture of instruction-response pairs, followed by rejection sampling to filter SFT outputs by quality, followed by direct preference optimization (DPO) on human preference data, and finally online RLHF using a trained reward model and PPO for further alignment. Long-context extension to 128K tokens is achieved via a continued pretraining stage on synthetic and curated long-context data, combined with modified RoPE scaling (YaRN). A notable methodological contribution is the use of LLM-as-judge evaluation in the preference data collection loop: rather than relying solely on human annotators, model-generated responses are rated by a combination of human annotators and an internal Qwen-based judge model, enabling higher-throughput preference data collection.

## Why It Matters

Qwen2.5 marks the maturation of Chinese-origin open-weight models into global frontier competitiveness. Prior generations of Qwen models were strong within their language tier but did not consistently match Western-origin models of equivalent scale; Qwen2.5 closes and in several domains reverses this gap, demonstrating that the data curation, training methodology, and post-training alignment innovations pioneered in North American and European labs are being replicated and refined at scale by Asian AI research groups. This has meaningful implications for the global distribution of AI capability: open-weight frontier models are no longer primarily a product of a single geographic ecosystem, and Qwen models have become widely adopted alternatives to LLaMA within both the research community and industry, particularly for East Asian language tasks and applications requiring strong mathematical reasoning.

The specialized sub-family strategy—Qwen2.5-Math and Qwen2.5-Coder—demonstrates that domain-specific continued pretraining on carefully curated data can produce performance levels dramatically beyond the general base model at equivalent scale, suggesting that modular specialization may be a more efficient path to task-specific frontier performance than uniform general-purpose scaling. This has catalyzed research into domain adaptation recipes, data mixture optimization for specialized pretraining, and the conditions under which a specialized smaller model outperforms a general larger model. The Qwen2.5 series has also become a common backbone for Chinese-language NLP research and multilingual instruction tuning, highlighting the importance of geographic and linguistic diversity in the open foundation model ecosystem for ensuring that the benefits of frontier AI are accessible across languages and communities.

| | |
|---|---|
| **Authors** | Qwen Team |
| **Year** | 2024 |
| **Venue** | arXiv 2024 |
| **Field** | Agi |
| **Subfield** | Llm Foundations Scaling |
| **Tasks** | multilingual, post-training |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2412.15115.pdf){: .btn .btn--primary .btn--large}
