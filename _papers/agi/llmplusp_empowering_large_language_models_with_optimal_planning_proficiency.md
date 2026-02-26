---
title: 'LLM+P: Empowering Large Language Models with Optimal Planning Proficiency'
collection: papers
permalink: /papers/agi/llmplusp_empowering_large_language_models_with_optimal_planning_proficiency/
date: '2023-04-22'
year: 2023
field: agi
subfield: agentic-llms-tool-use
tasks:
- planning
- pddl
- hybrid-systems
tier: 2
artifact_type: paper
venue: arXiv 2023
authors:
- Bo Liu
- Yuqian Jiang
- Xiaohan Zhang
- Qiang Liu
authors_short: Liu et al.
paperurl: https://arxiv.org/pdf/2304.11477.pdf
doi: 10.48550/arXiv.2304.11477
license: unspecified
summary: Proposes a pipeline in which an LLM translates natural-language task descriptions
  into PDDL problem files, delegates search to an off-the-shelf classical planner
  (Fast Downward), and then uses the LLM again to verbalize the resulting plan—achieving
  near-perfect success on Blocksworld and other classical domains where GPT-4 alone
  fails.
why_important: Established the neuro-symbolic hybrid as a principled alternative to
  end-to-end LLM planning, demonstrating that LLMs are better suited for language
  grounding than for combinatorial search—a distinction that motivates continued integration
  of verified solvers into agentic pipelines.
tags:
- planning
- pddl
- hybrid-systems
- agents
---

## Summary

LLM+P proposes a three-stage hybrid pipeline for task planning: (1) an LLM (GPT-4) translates a natural-language task description and domain description into a PDDL problem file, leveraging a provided PDDL domain template; (2) an off-the-shelf classical planner (Fast Downward) solves the PDDL problem to optimality or near-optimality; (3) the LLM verbalizes the resulting plan sequence back into natural language for the user. The entire planning burden—combinatorial search over state spaces, constraint satisfaction, and optimality guarantees—is delegated to the classical planner, while the LLM handles only the language-grounding steps at the front and back ends.

Empirically, LLM+P achieves near-perfect task completion on classical planning benchmarks including Blocksworld (stacking/unstacking colored blocks), Barman (cocktail mixing), and Floortile (robot tiling), where GPT-4 prompted directly fails on all but the simplest instances. The results demonstrate a dramatic capability gap: GPT-4 alone achieves roughly 10–20% on multi-step Blocksworld instances, while LLM+P achieves 95%+. The approach is also strictly more sample-efficient than fine-tuning a model to produce correct plans, since the planner guarantees correctness given a correct PDDL translation.

A notable methodological finding is that LLM-to-PDDL translation accuracy is the main bottleneck—the planner itself never fails given a valid PDDL file, but the LLM occasionally produces syntactically invalid or semantically incorrect PDDL (e.g., wrong predicate names or missing preconditions). The paper includes analysis of translation error types and ablations showing that providing a domain PDDL template dramatically reduces translation errors compared to asking the model to generate both domain and problem files from scratch.

## Why It Matters

LLM+P is the canonical existence proof that LLMs and classical solvers are complementary rather than competing: LLMs excel at mapping between natural language and formal representations, while symbolic planners provide soundness, completeness, and optimality that no current LLM can match on combinatorial search problems. This division of cognitive labor has influenced the broader neuro-symbolic AI agenda, appearing in subsequent work that replaces the planner with SAT solvers, constraint solvers, or theorem provers depending on the task structure.

The paper also highlights a critical open question: how to make LLM-to-PDDL translation reliable enough for real-world deployment, where domain templates may not be available and task descriptions may be ambiguous or underspecified. Subsequent work has explored fine-tuning LLMs on PDDL translation pairs, using PDDL validators in a feedback loop to correct translation errors, and extending the approach to temporal and numeric planning domains. The fundamental tension between the expressivity of natural language and the formal precision required by planners remains unresolved and is a productive area of ongoing research at the intersection of NLP and automated planning.

| | |
|---|---|
| **Authors** | Liu et al. |
| **Year** | 2023 |
| **Venue** | arXiv 2023 |
| **Field** | Agi |
| **Subfield** | Agentic Llms Tool Use |
| **Tasks** | planning, pddl, hybrid-systems |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2304.11477.pdf){: .btn .btn--primary .btn--large}
