---
title: 'PaLM: Scaling Language Modeling with Pathways'
collection: papers
permalink: /papers/agi/palm_scaling_language_modeling_with_pathways/
date: '2022-04-05'
year: 2022
field: agi
subfield: llm-foundations-scaling
tasks:
- large-scale-training
- scaling
tier: 1
artifact_type: paper
venue: arXiv / JMLR 2023
authors:
- Aakanksha Chowdhery
- Sharan Narang
- Jacob Devlin
- Maarten Bosma
authors_short: Chowdhery et al.
paperurl: https://jmlr.org/papers/volume24/22-1144/22-1144.pdf
doi: 10.5555/3648699.3648939
license: unspecified
summary: Presents a 540B-parameter autoregressive language model trained via Google's
  Pathways distributed infrastructure, demonstrating discontinuous emergent capabilities
  on BIG-Bench tasks and breakthrough few-shot reasoning performance with chain-of-thought
  prompting.
why_important: Established emergent capabilities as a central phenomenon of large-scale
  training and showed that cross-pod TPU infrastructure could sustain frontier training
  runs; served as backbone for Flan-PaLM, Med-PaLM, and numerous follow-on systems.
tags:
- llm
- scaling
- training-infra
- pathways
---

## Summary

PaLM (Pathways Language Model) is a 540B-parameter autoregressive transformer trained by Google using the Pathways distributed computing system across 6144 TPU v4 chips spanning two separate TPU pods, connected via a high-bandwidth datacenter network. The model achieves 46.2% hardware FLOP utilization—a significant efficiency milestone at this scale—by combining pipeline and data parallelism across the pod boundary without the communication bottlenecks that had previously limited cross-pod training. The training data is a high-quality mixture of 780B tokens drawn from multilingual web text, Wikipedia, GitHub code (39 programming languages), multilingual social media conversations, and book corpora, with explicit filtering for toxicity and deduplication.

PaLM achieves state-of-the-art few-shot performance across dozens of NLP benchmarks at the time of publication. Most dramatically, it demonstrates discontinuous performance improvements on tasks in the BIG-Bench evaluation suite—tasks where smaller models fail near-randomly—achieving 58.1% on BIG-Bench Hard. Chain-of-thought prompting amplifies these gains substantially: PaLM 540B with chain-of-thought prompting surpasses fine-tuned models on GSM8K (58%), SVAMP, and AQuA mathematical reasoning benchmarks. These results provide the first strong evidence that chain-of-thought reasoning is an emergent capability that appears reliably only beyond a critical scale threshold (approximately 62B parameters for the tasks studied).

The paper makes two notable methodological contributions beyond the model itself. First, it provides a careful analysis of memorization behavior, showing that exact n-gram memorization rates grow with model size and correlate with data repetition frequency, with implications for privacy and copyright. Second, it conducts an analysis of model bias across demographic dimensions (gender, race, religion, profession) using counterfactual evaluation, documenting systematic disparities and noting that larger models can both reduce some forms of bias and amplify others—a finding that has been replicated repeatedly in subsequent bias analyses.

## Why It Matters

PaLM played a decisive role in establishing emergent capabilities as a central phenomenon of large-scale language model training. The observation that chain-of-thought prompting is an emergent capability—absent at 8B and 62B, present and strong at 540B—prompted the field to take phase-transition-like jumps in capability seriously, influencing both how benchmarks are designed (to detect emergence) and how safety researchers think about capability surprises at scale. PaLM's results on BIG-Bench and chain-of-thought reasoning were broadly cited as motivation for subsequently scaling both model size and reasoning evaluation complexity. The Pathways infrastructure demonstration also showed that multi-pod TPU training was a viable engineering path, informing the hardware strategy for Gemini and subsequent Google frontier models.

PaLM also served as the backbone for a rich family of derivative research systems that validated its usefulness as a general-purpose base: Flan-PaLM (instruction-tuned across 1,800 tasks) demonstrated that fine-tuning dramatically improves zero-shot performance; Med-PaLM explored clinical question answering at expert-level performance; and Minerva adapted PaLM for scientific and mathematical reasoning using targeted pretraining data. These derivative works collectively established PaLM as one of the most extensible foundation models of its era. However, PaLM's emergent capability narrative also prompted important skeptical work: subsequent research by Schaeffer et al. (2023) argued that many apparent emergent capabilities are measurement artifacts produced by nonlinear evaluation metrics, raising the question of whether phase transitions in model quality are real phenomena or artifacts of how we measure performance.

| | |
|---|---|
| **Authors** | Chowdhery et al. |
| **Year** | 2022 |
| **Venue** | arXiv / JMLR 2023 |
| **Field** | Agi |
| **Subfield** | Llm Foundations Scaling |
| **Tasks** | large-scale-training, scaling |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://jmlr.org/papers/volume24/22-1144/22-1144.pdf){: .btn .btn--primary .btn--large}
