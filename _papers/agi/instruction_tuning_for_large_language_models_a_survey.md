---
title: 'Instruction Tuning for Large Language Models: A Survey'
collection: papers
permalink: /papers/agi/instruction_tuning_for_large_language_models_a_survey/
date: '2023-08-20'
year: 2023
field: agi
subfield: alignment-safety-evaluation
tasks:
- instruction-tuning
- sft
- post-training
tier: 3
artifact_type: paper
venue: arXiv 2023
authors:
- Shengding Hu
- Yuge Tu
- Xu Han
- Ganqu Cui
authors_short: Hu et al.
paperurl: https://arxiv.org/pdf/2308.10792.pdf
doi: 10.48550/arXiv.2308.10792
license: unspecified
summary: 'Comprehensively surveys instruction tuning — fine-tuning pre-trained LLMs
  on (instruction, output) pairs to improve zero-shot task generalization — covering
  three axes: dataset construction strategies (human-written, template-based, and
  Self-Instruct-style model-generated), training protocols (full fine-tuning vs. LoRA
  and other PEFT methods), and evaluation paradigms; finds that instruction diversity
  outweighs raw dataset size for generalization, parameter-efficient methods approach
  full fine-tuning quality, and data quality becomes the binding constraint beyond
  moderate dataset scales.'
why_important: Provided the field with a unified reference for the rapidly proliferating
  instruction-tuning literature (Alpaca, Vicuna, FLAN, etc.) and situates IT as a
  distinct post-training stage from RLHF-based alignment, clarifying both its strengths
  — strong zero-shot generalization — and its limitations in producing the value-aligned,
  preference-following behavior that RLHF targets.
tags:
- instruction-tuning
- sft
- survey
- post-training
---

## Summary

This survey provides a systematic account of instruction tuning (IT) — the process of fine-tuning pre-trained LLMs on datasets of (instruction, response) pairs to improve zero-shot generalization to new tasks described in natural language. The paper organizes the literature across three axes. First, *dataset construction*: human-written datasets (FLAN, Super-NaturalInstructions), template-based datasets that convert existing NLP task datasets into instruction format, and model-generated datasets via Self-Instruct-style prompting (Alpaca, Vicuna, WizardLM). Second, *training protocols*: full parameter fine-tuning vs. parameter-efficient methods including LoRA, prefix tuning, prompt tuning, and adapter layers. Third, *evaluation paradigms*: held-out task generalization (measuring zero-shot transfer to unseen task types), aggregate benchmark performance (MMLU, BIG-Bench), and human preference evaluation via pairwise comparison or absolute rating.

Key empirical syntheses include: instruction diversity — across task types, domains, and instruction phrasings — matters more than raw dataset size for zero-shot generalization, with models trained on 1,000 diverse high-quality instructions frequently outperforming those trained on 100,000 narrowly distributed ones. LoRA-based IT achieves performance within a few percentage points of full fine-tuning at roughly 10–30% of the compute cost, making IT accessible on consumer-grade hardware. Beyond a threshold of approximately 50,000–100,000 training examples, scaling IT data yields diminishing returns and data quality becomes the binding constraint. The survey also documents the scaling relationship between base model capability and IT effectiveness: instruction tuning amplifies existing capabilities but cannot inject fundamentally new knowledge or skills absent from pre-training.

Methodologically, the paper contributes a principled taxonomy of instruction types — *task specification* (describe what to do), *role specification* (define agent persona and constraints), and *constraint specification* (impose output format, length, or style requirements) — and analyzes how each type contributes to downstream behavior. Importantly, the survey situates IT as a distinct post-training stage from RLHF-based alignment, noting that IT shapes the model's input-output mapping for task generalization while RLHF further shapes which outputs the model prefers among feasible alternatives.

## Why It Matters

This survey arrived at a moment of rapid proliferation in instruction-tuning recipes (Alpaca, Vicuna, Dolly, OpenHermes, and dozens of others), providing a structured synthesis that enabled researchers to compare approaches on principled grounds rather than empirically reported numbers alone. Its finding that data quality and diversity dominate quantity directly influenced subsequent dataset curation efforts, including Orca, Phi-1, and the broader "textbook quality" data movement.

By clearly distinguishing instruction tuning from RLHF-based preference alignment, the survey also clarified the role of each training stage and highlighted that instruction-tuned models — while dramatically more useful than raw pre-trained models — still exhibit miscalibrated refusals, value-misaligned outputs, and reward hacking vulnerabilities that IT alone does not address. This clarification motivated the standard two-stage post-training pipeline (SFT→RLHF or SFT→DPO) used in production model development, and continues to inform decisions about where to invest compute across the post-training curriculum.

| | |
|---|---|
| **Authors** | Hu et al. |
| **Year** | 2023 |
| **Venue** | arXiv 2023 |
| **Field** | Agi |
| **Subfield** | Alignment Safety Evaluation |
| **Tasks** | instruction-tuning, sft, post-training |
| **Tier** | 3 — Benchmark / Auxiliary |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2308.10792.pdf){: .btn .btn--primary .btn--large}
