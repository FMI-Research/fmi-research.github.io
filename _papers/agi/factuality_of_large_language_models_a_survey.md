---
title: 'Factuality of Large Language Models: A Survey'
collection: papers
permalink: /papers/agi/factuality_of_large_language_models_a_survey/
date: '2024-02-04'
year: 2024
field: agi
subfield: alignment-safety-evaluation
tasks:
- factuality
- evaluation
- automated-scoring
tier: 1
artifact_type: paper
venue: arXiv / EMNLP 2024
authors:
- Yike Wang
- Shangbin Feng
- Heng Wang
- Weijia Shi
authors_short: Wang et al.
paperurl: https://arxiv.org/pdf/2402.02420.pdf
doi: 10.48550/arXiv.2402.02420
license: unspecified
summary: Surveys factuality in LLMs along three axes — parametric knowledge accuracy,
  contextual faithfulness, and reasoning-chain grounding — and critically examines
  automated evaluation methods (NLI-based, retrieval-augmented, and LLM-as-judge pipelines),
  identifying systematic gaps between fluency-based metrics and true factual correctness;
  proposes a four-dimensional factuality decomposition covering accuracy, completeness,
  consistency, and attribution.
why_important: Articulated why single-metric factuality evaluation is insufficient
  and showed that instruction-tuned models can be more helpful but less factually
  reliable than their base counterparts, a finding that has become a recurring concern
  in deployment-focused reliability research and motivates attribution-aware evaluation
  frameworks.
tags:
- factuality
- evaluation
- reliability
- hallucination
---

## Summary

This survey examines factuality in LLMs along three axes: *parametric factuality* (whether the model's stored knowledge is accurate), *contextual factuality* (whether the model correctly and completely uses information provided in context), and *reasoning factuality* (whether multi-step reasoning chains produce factually grounded intermediate and final conclusions). For each axis, the paper reviews the state of automated evaluation, cataloguing NLI-based scorers, retrieval-augmented verification pipelines (e.g., FactScore), and LLM-as-judge approaches, while critically assessing their reliability and correlation with human judgment. A central finding is the systematic gap between fluency-based metrics and factual correctness: models that score highly on coherence and ROUGE are frequently factually unreliable, particularly on knowledge-intensive generation tasks.

The survey proposes a four-dimensional decomposition of factual correctness: *accuracy* (is the claim verifiably true?), *completeness* (are all relevant facts included without material omission?), *consistency* (do claims within the document contradict each other?), and *attribution* (are claims traceable to cited or retrievable evidence?). This decomposition reveals why single-metric factuality evaluation is insufficient: a model can achieve high accuracy on verifiable claims while systematically omitting important qualifications, or produce internally consistent but fabricated content. The paper also documents that instruction-tuned models can be *less* factually reliable than their base counterparts on knowledge-intensive tasks, because SFT and RLHF optimize for user preference signals that reward confident, fluent responses even when the underlying knowledge is uncertain.

Automated factuality scoring remains a significant open challenge. NLI-based verifiers exhibit high inter-annotator disagreement on borderline claims; retrieval-augmented scorers inherit the biases of the retrieval system; and LLM-as-judge pipelines show factuality evaluation artifacts from the judge model's own parametric knowledge. The paper calls for multi-aspect evaluation protocols that assess all four dimensions independently and for factuality-specific evaluation models trained on high-agreement human annotations.

## Why It Matters

By articulating the fluency–factuality gap, this survey provided the research community with a principled argument for why deploying fluent language models without factuality controls poses reliability risks in high-stakes domains. The four-dimensional decomposition (accuracy, completeness, consistency, attribution) has been influential in structuring subsequent factuality evaluation frameworks and in justifying why attribution-aware generation methods — citation grounding, retrieval-augmented generation with verifiable provenance — are necessary complements to fluency optimization.

The survey also raised a practically important concern about the side effects of alignment: instruction tuning and RLHF, while improving helpfulness and perceived quality, can reduce factual reliability by training models to hedge less and assert more confidently. This tension between preference optimization and factual calibration remains an open research problem, motivating work on calibration-aware RLHF, uncertainty-expressing training objectives, and factuality reward models.

| | |
|---|---|
| **Authors** | Wang et al. |
| **Year** | 2024 |
| **Venue** | arXiv / EMNLP 2024 |
| **Field** | Agi |
| **Subfield** | Alignment Safety Evaluation |
| **Tasks** | factuality, evaluation, automated-scoring |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2402.02420.pdf){: .btn .btn--primary .btn--large}
