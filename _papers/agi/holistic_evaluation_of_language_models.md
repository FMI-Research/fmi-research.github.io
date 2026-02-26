---
title: Holistic Evaluation of Language Models
collection: papers
permalink: /papers/agi/holistic_evaluation_of_language_models/
date: '2022-11-16'
year: 2022
field: agi
subfield: alignment-safety-evaluation
tasks:
- evaluation
- multi-metric
- benchmarks
tier: 1
artifact_type: paper
venue: arXiv / TMLR 2023
authors:
- Percy Liang
- Rishi Bommasani
- Tony Lee
- Dimitris Tsipras
authors_short: Liang et al.
paperurl: https://friedeggs.github.io/files/helm.pdf
doi: ''
license: unspecified
summary: HELM introduces a structured scenario-and-metric taxonomy to evaluate LLMs
  across 42 scenarios and 7 metric dimensions simultaneously, revealing that no single
  model dominates across accuracy, calibration, robustness, fairness, and toxicity.
why_important: Shifted the field's evaluation culture away from single-leaderboard
  accuracy toward multi-objective, transparency-first benchmarking, directly inspiring
  subsequent holistic evaluation efforts such as BIG-Bench Hard and Open LLM Leaderboard.
tags:
- evaluation
- benchmarks
- multi-metric
- transparency
---

## Summary

HELM proposes a two-level evaluation structure built around *scenarios* (combinations of task, domain, and language) and *metrics* (accuracy, calibration, robustness, fairness, bias, toxicity, and efficiency). Rather than collapsing model quality into a single number, each model is evaluated on 42 scenarios covering NLP classics (question answering, summarization, information retrieval), emerging capabilities (in-context learning, reasoning), and socially sensitive tasks (toxicity detection, demographic bias). The evaluation encompasses over 30 language models from six families, ranging from GPT-3 and PaLM to Codex and BioMedLM, creating the most comprehensive public comparative study of LLMs at the time of publication.

The headline empirical finding is that no model Pareto-dominates across all seven metric dimensions. Models achieving top-tier accuracy consistently sacrifice robustness or fairness — for example, GPT-3 and Codex score well on accuracy benchmarks but exhibit measurable performance degradation under prompt perturbations and produce biased outputs on demographic-sensitive tasks. Calibration scores reveal that even high-accuracy models are poorly calibrated, consistently overconfident on incorrect predictions. The multi-metric view exposes a systematic accuracy–robustness–fairness trilemma that single-leaderboard evaluations conceal.

Methodologically, HELM's key innovations are the *perturbation* protocol (testing how performance degrades under paraphrase, typo, and format perturbations), a fully public, standardized prompt format for each scenario, and an open leaderboard that releases raw model outputs rather than aggregated numbers. This transparency-first design enables downstream reproducibility and allows the research community to audit model behavior at the example level — a stark contrast to the opaque benchmark reporting norm prevalent at the time.

## Why It Matters

HELM catalyzed a shift in evaluation culture: it made explicit that accuracy alone is an inadequate model selection criterion for deployment and that multi-metric transparency must be the standard. Its scenario-and-metric vocabulary was widely adopted in subsequent evaluation work, including BIG-Bench Hard, Open LLM Leaderboard, and the AlpacaEval series. The paper also elevated calibration and robustness to first-class evaluation targets, directly motivating methodology for confidence estimation and distribution-shift robustness in LLMs.

The framework's primary limitation is that many HELM metrics require automated reference-based scoring, which correlates imperfectly with human judgment, particularly for open-ended generation tasks. The static scenario set also risks becoming saturated as models improve, a challenge the community has since addressed with dynamic, adversarial, and human-in-the-loop evaluation paradigms. Nonetheless, HELM's transparency infrastructure and its insistence on multi-objective reporting remain the standard against which subsequent holistic evaluations are measured.

| | |
|---|---|
| **Authors** | Liang et al. |
| **Year** | 2022 |
| **Venue** | arXiv / TMLR 2023 |
| **Field** | Agi |
| **Subfield** | Alignment Safety Evaluation |
| **Tasks** | evaluation, multi-metric, benchmarks |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://friedeggs.github.io/files/helm.pdf){: .btn .btn--primary .btn--large}
