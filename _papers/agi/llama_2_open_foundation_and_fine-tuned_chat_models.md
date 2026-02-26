---
title: 'Llama 2: Open Foundation and Fine-Tuned Chat Models'
collection: papers
permalink: /papers/agi/llama_2_open_foundation_and_fine-tuned_chat_models/
date: '2023-07-19'
year: 2023
field: agi
subfield: llm-foundations-scaling
tasks:
- instruction-tuning
- safety
- chat
tier: 2
artifact_type: paper
venue: arXiv 2023
authors:
- Hugo Touvron
- Louis Martin
- Kevin Stone
- Peter Albert
authors_short: Touvron et al.
paperurl: https://arxiv.org/pdf/2307.09288.pdf
doi: 10.48550/arXiv.2307.09288
license: unspecified
summary: Presents updated pretrained Llama 2 base models (7B–70B) alongside RLHF-aligned
  Llama 2-Chat variants, with detailed disclosure of reward model training, PPO-based
  alignment, ghost attention for multi-turn consistency, and both helpfulness and
  safety evaluations.
why_important: Became the de facto open-weight baseline for post-training alignment
  research through 2023–2024, providing a reproducible RLHF template and commercially
  usable weights that shaped downstream fine-tuning and safety evaluation practices
  across the field.
tags:
- open-weights
- llm
- rlhf
- instruction-tuning
- safety
---

## Summary

Llama 2 presents updated pretrained base models at 7B, 13B, 34B, and 70B parameters, alongside Llama 2-Chat, a series of dialogue-optimized models trained using reinforcement learning from human feedback (RLHF). Relative to the original LLaMA, the base models are trained on 40% more data (approximately 2T tokens from a higher-quality filtered pretraining corpus), use a doubled context window (4096 tokens), and incorporate grouped-query attention (GQA) at the 34B and 70B scales to improve inference throughput. The paper is unusual in the depth of its methodological disclosure: the RLHF pipeline, annotation procedures, reward model architecture, and safety evaluation methodology are described with a level of detail rarely seen in frontier model publications.

The alignment pipeline proceeds in stages: supervised fine-tuning (SFT) on ~27,500 high-quality human-written demonstrations, followed by training two separate reward models—one optimized for helpfulness and one for safety—on human preference comparisons. These reward models then supervise proximal policy optimization (PPO) on the base models, iteratively improving the chat variants across multiple rounds of RLHF. A key architectural innovation is ghost attention (GAtt), which addresses a failure mode where multi-turn models forget system prompt constraints partway through a long conversation; GAtt trains the model to attend to the system prompt at every position, improving instruction-following consistency. Human evaluation studies show Llama 2-Chat 70B matching or outperforming GPT-3.5 Turbo on single-turn and multi-turn helpfulness, while maintaining competitive safety rates as measured by a trained safety classifier.

The safety evaluation methodology is notably thorough: the paper reports both automated safety scoring and human red-team evaluation results, tracking violation rates across categories including violence, sexual content, and self-harm. It also discloses annotator guidelines, inter-rater reliability statistics, and the demographic distribution of annotation workers—a level of transparency that enables critique and replication. The commercial license (permitting deployment with a usage restriction for services exceeding 700M monthly active users) was carefully structured to enable broad adoption while maintaining some guardrails.

## Why It Matters

Llama 2 became the standard open-weight baseline for post-training alignment research through most of 2023 and into 2024, serving as the starting point for hundreds of downstream fine-tuning studies, domain adaptation projects, and alignment technique evaluations. Its detailed documentation of the RLHF pipeline provided practitioners with a reproducible template: subsequent open-source alignment projects including OpenHermes, Zephyr (which replaced PPO with DPO), and Orca 2 either built directly on Llama 2 or used its pipeline documentation as a design reference. The concurrent release of weights and a commercially permissive license enabled the first wave of small-business and enterprise deployment of openly available aligned models.

The paper also surfaced important unresolved tensions in aligned model evaluation that remain active research problems. Human preference evaluations are sensitive to annotator demographics, question framing, and the specific comparison baseline—making it difficult to make absolute claims about helpfulness from preference studies alone. Optimizing simultaneously for helpfulness and safety through two separate reward models creates tension: the safety reward model can suppress legitimate responses, while the helpfulness reward model can reward verbosity and sycophancy. The paper's honest acknowledgment of these tradeoffs—rather than presenting clean, positive results—made it a valuable reference for understanding the fundamental challenges of RLHF-based alignment, motivating subsequent work on DPO, RLAIF, and constitutional AI approaches that attempt to sidestep some of these difficulties.

| | |
|---|---|
| **Authors** | Touvron et al. |
| **Year** | 2023 |
| **Venue** | arXiv 2023 |
| **Field** | Agi |
| **Subfield** | Llm Foundations Scaling |
| **Tasks** | instruction-tuning, safety, chat |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2307.09288.pdf){: .btn .btn--primary .btn--large}
