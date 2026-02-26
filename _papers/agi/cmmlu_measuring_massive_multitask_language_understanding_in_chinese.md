---
title: 'CMMLU: Measuring massive multitask language understanding in Chinese'
collection: papers
permalink: /papers/agi/cmmlu_measuring_massive_multitask_language_understanding_in_chinese/
date: '2023-06-15'
year: 2023
field: agi
subfield: alignment-safety-evaluation
tasks:
- chinese-evaluation
- benchmarks
- multilingual
tier: 2
artifact_type: paper
venue: arXiv / ACL Findings 2024
authors:
- Haonan Li
- Yixuan Zhang
- Fajri Koto
- Yifei Yang
authors_short: Li et al.
paperurl: https://arxiv.org/pdf/2306.09212.pdf
doi: 10.48550/arXiv.2306.09212
license: unspecified
summary: CMMLU contains 11,528 multiple-choice questions across 67 subjects, including
  topics unique to Chinese culture and society — traditional medicine, Mandarin linguistics,
  Chinese history — that are absent from English benchmarks like MMLU; it provides
  separate dev and test splits to support both zero-shot and few-shot evaluation,
  and analyzes performance across STEM, social sciences, humanities, and culture-specific
  categories to reveal where multilingual transfer fails.
why_important: Demonstrated that strong English MMLU performance does not uniformly
  transfer to Chinese, and that fine-tuning on domain data yields large gains on culture-specific
  subjects but marginal gains on mathematics and logic, motivating the design of culturally
  inclusive pre-training corpora and evaluation suites for future multilingual model
  development.
tags:
- chinese
- evaluation
- benchmarks
- multilingual
---

## Summary

CMMLU (Chinese Massive Multitask Language Understanding) extends the MMLU evaluation paradigm to Chinese by constructing a benchmark of 11,528 multiple-choice questions across 67 subjects, covering STEM, social sciences, humanities, and — critically — subjects unique to Chinese culture and society that have no English equivalents: traditional Chinese medicine, Mandarin linguistics and phonetics, Chinese history and philosophy, and Chinese legal frameworks. This cultural coverage is the benchmark's defining methodological distinction from simply translating MMLU into Chinese. Questions are sourced from Chinese standardized examinations, textbooks, and professional qualification materials, with both a development set (5 questions per subject) and a test set, enabling standard zero-shot and five-shot evaluation protocols.

Empirically, GPT-4 achieves 71.0% accuracy on CMMLU, substantially outperforming open-source alternatives at the time of publication. The benchmark reveals a consistent gap between English MMLU performance and Chinese CMMLU performance across all model families tested, even for models with substantial Chinese pre-training data — demonstrating that multilingual transfer does not uniformly propagate to culturally specific knowledge. The analysis of subject-category breakdowns shows that current models systematically underperform on culture-specific subjects (traditional medicine, Chinese history, Mandarin linguistics) relative to universal STEM subjects, indicating that multilingual pre-training captures surface language patterns but not deeply culturally embedded knowledge structures. Fine-tuning on Chinese domain data yields large improvements on cultural subjects but minimal gains on mathematics and logic, further supporting this interpretation.

Methodologically, CMMLU's 67-subject breadth permits fine-grained capability profiling across model families, revealing that architecturally similar models trained on different Chinese corpora exhibit substantially different cultural knowledge profiles. The paper also evaluates chain-of-thought prompting, finding that it improves performance on STEM subjects but has negligible effect on cultural knowledge recall — consistent with the hypothesis that CoT benefits tasks where the answer requires multi-step derivation rather than retrieval.

## Why It Matters

CMMLU demonstrated that evaluation frameworks must go beyond language translation to capture culturally specific knowledge, and that strong English-language performance is not a reliable proxy for Chinese professional competence. This finding has direct implications for how multilingual LLMs are trained and marketed: corpus composition must include culturally specific materials, not just parallel corpora or translated documents.

The benchmark has been widely adopted as a standard for Chinese LLM evaluation alongside C-Eval, providing complementary coverage (CMMLU's cultural breadth vs. C-Eval's examination-level difficulty stratification). Together they have shaped the Chinese LLM evaluation ecosystem and continue to motivate investment in culturally diverse pre-training corpora, multilingual instruction tuning, and evaluation-driven corpus curation for non-English languages.

| | |
|---|---|
| **Authors** | Li et al. |
| **Year** | 2023 |
| **Venue** | arXiv / ACL Findings 2024 |
| **Field** | Agi |
| **Subfield** | Alignment Safety Evaluation |
| **Tasks** | chinese-evaluation, benchmarks, multilingual |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2306.09212.pdf){: .btn .btn--primary .btn--large}
