---
title: 'Constitutional AI: Harmlessness from AI Feedback'
collection: papers
permalink: /papers/agi/constitutional_ai_harmlessness_from_ai_feedback/
date: '2022-12-15'
year: 2022
field: agi
subfield: alignment-safety-evaluation
tasks:
- rlaif
- safety
- harmlessness
tier: 1
artifact_type: paper
venue: arXiv 2022
authors:
- Yuntao Bai
- Saurav Kadavath
- Sandipan Kundu
- Amanda Askell
authors_short: Bai et al.
paperurl: https://arxiv.org/pdf/2212.08073.pdf
doi: 10.48550/arXiv.2212.08073
license: unspecified
summary: Constitutional AI trains harmless assistants through two phases — a supervised
  critique-and-revision loop guided by a written "constitution," followed by RLAIF
  using AI-generated preference labels in place of human harm annotations — achieving
  strong harmlessness without requiring annotators to label harmful content directly.
why_important: Introduced RLAIF as a scalable alternative to human feedback for safety
  training, motivating the broader scalable oversight research agenda; the constitutional
  critique-revision paradigm also influenced subsequent self-refinement and self-critique
  methods for improving model outputs.
tags:
- rlaif
- safety
- constitutional-ai
- alignment
---

## Summary

Constitutional AI (CAI) addresses a core bottleneck in RLHF-based safety alignment: the need for human annotators to label harmful content at scale. CAI replaces this with a two-phase procedure. In the first phase (SL-CAI), the model is prompted to generate an initially harmful response, then asked to critique that response according to one of several natural-language "constitutional principles" (e.g., "Choose the response that is least likely to contain false or misleading information") and finally to revise its response in light of the critique. Iterating this critique-revision loop produces a dataset of self-improved responses for supervised fine-tuning. In the second phase (RLAIF), a separate feedback model — trained on helpfulness preferences but not harm labels — scores pairs of responses according to constitutional principles, generating preference data that drives RLHF without human harm annotation.

CAI-trained models achieve substantially lower harmfulness rates than vanilla RLHF baselines while maintaining comparable helpfulness scores, as measured by blind human preference judgments. Critically, the paper demonstrates that AI-generated preference labels correlate well with human harm ratings across a range of sensitive topics, validating the core scalability claim. CAI models also exhibit fewer refusals on benign but sensitive-seeming prompts (reducing the "assistant tax" of overly cautious behavior), because the constitution can be written to explicitly value both harmlessness and non-paternalism.

Methodologically, the critique-revision loop for SFT data generation is a significant innovation — it shows that models can improve their own outputs via structured self-critique, foreshadowing later self-refinement and self-critique methods. The separation between the helpfulness-trained feedback model and the harmlessness-targeted constitution is also notable: it decouples what counts as harmful (specified by the constitution's principles) from the measurement of harmfulness (delegated to the AI feedback model), enabling interpretable and updatable safety specifications.

## Why It Matters

CAI established RLAIF — reinforcement learning from AI feedback — as a credible, scalable alternative to RLHF for safety alignment, directly motivating subsequent work on scalable oversight, debate-based alignment, and AI-assisted red-teaming. The constitutional specification paradigm — encoding safety objectives as natural-language principles that can be audited and updated — has become influential in production alignment pipelines, and variations of it underpin Claude's alignment approach.

The core open question CAI raises is distributional: AI-generated feedback inherits the biases and blind spots of the feedback model, potentially creating alignment failures that human annotators would catch. This motivates research on feedback model diversity, constitutional robustness evaluation, and hybrid human–AI annotation pipelines. CAI also implicitly depends on the feedback model being trustworthy enough to reliably apply the constitution — a chicken-and-egg problem that connects to recursive reward modeling and scalable oversight.

| | |
|---|---|
| **Authors** | Bai et al. |
| **Year** | 2022 |
| **Venue** | arXiv 2022 |
| **Field** | Agi |
| **Subfield** | Alignment Safety Evaluation |
| **Tasks** | rlaif, safety, harmlessness |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2212.08073.pdf){: .btn .btn--primary .btn--large}
