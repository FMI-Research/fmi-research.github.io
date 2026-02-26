---
title: Large Language Models Still Can't Plan (A Benchmark for LLMs on Planning and
  Reasoning about Change)
collection: papers
permalink: /papers/agi/large_language_models_still_cant_plan_a_benchmark_for_llms_on_planning_and_reasoning_about_change/
date: '2022-06-27'
year: 2022
field: agi
subfield: agentic-llms-tool-use
tasks:
- planning
- benchmarks
- evaluation
tier: 2
artifact_type: paper
venue: arXiv 2022
authors:
- Karthik Valmeekam
- Alberto Olmo
- Sarath Sreedharan
- Subbarao Kambhampati
authors_short: Valmeekam et al.
paperurl: https://arxiv.org/pdf/2206.10498v3.pdf
doi: 10.48550/arXiv.2206.10498
license: unspecified
summary: Introduces an extensible PDDL-generated benchmark evaluating LLMs on Blocksworld
  plan generation and plan verification tasks, finding that even GPT-4 achieves below
  20% on harder instances and that models cannot reliably verify their own plans—casting
  doubt on claims that CoT prompting confers genuine planning ability.
why_important: Serves as an essential corrective to optimistic capability claims by
  demonstrating that pattern-matching on training data does not generalize to novel
  planning instances; the systematic failure on verification tasks—theoretically easier
  than generation—highlights fundamental reasoning limitations that shaped subsequent
  work on LLM+classical-solver hybrids.
tags:
- planning
- benchmarks
- evaluation
- limitations
---

## Summary

Valmeekam et al. introduce an extensible benchmark for evaluating LLM planning ability using instances generated from PDDL domain definitions, ensuring that test problems cannot appear in training corpora and that ground-truth solutions are verifiable by classical planners. The benchmark focuses on two domains—standard Blocksworld (block stacking with clear/on/ontable predicates) and Mystery Blocksworld (semantically obfuscated version with renamed objects and predicates)—and tests models on both **plan generation** (produce a valid plan to reach a goal state) and **plan verification** (determine whether a given plan correctly achieves the goal). This two-task design is crucial: verification is theoretically easier than generation, so failure on verification reveals deeper reasoning deficiencies than generation failure alone.

The key empirical findings are alarming by the standards of papers contemporaneously claiming strong LLM planning abilities. GPT-4 achieves below 20% on even moderately complex Blocksworld instances (3–5 blocks), and performance degrades further on the obfuscated Mystery variant, suggesting that any apparent successes in non-obfuscated domains reflect memorization of Blocksworld-specific patterns from training data rather than genuine planning competency. Critically, GPT-4's performance on plan verification is also well below the theoretical ceiling—the model frequently endorses invalid plans and rejects valid ones—demonstrating that the model cannot reliably simulate state transitions, a prerequisite for any meaningful planning.

The paper includes a systematic failure mode analysis showing that LLMs violate physical constraints (e.g., moving a block that is not clear, placing a block on itself), lose track of world state across multiple steps, and exhibit inconsistent behavior across semantically equivalent problem instances. The extensible PDDL-based generation framework allows future researchers to test any planning domain with controllable difficulty parameters, making PlanBench a living benchmark rather than a fixed snapshot.

## Why It Matters

PlanBench played an important corrective role at a moment when demos of GPT-4 solving simple planning problems were being cited as evidence of emergent planning ability. By demonstrating that performance collapses on slightly harder instances and on semantically obfuscated variants, the paper established that LLMs engage in planning-adjacent pattern matching rather than principled state-space search—a distinction that has significant implications for the safe deployment of LLM-based agents in consequential planning domains.

The paper directly motivated the hybrid neuro-symbolic agenda (LLM+P, SayPlan, and similar work) by establishing the performance floor that any LLM-only approach must overcome. Its findings on the verification gap also influenced work on process reward models and self-critique approaches, which attempt to give models a more reliable internal critic. Open questions include whether sufficiently large scale or targeted fine-tuning on planning traces can close the gap, and whether the failure mode is fundamentally about working memory capacity (context length) or about the absence of a learned world model—questions that remain contested and practically important as agentic systems are deployed in logistics, robotics, and scientific automation.

| | |
|---|---|
| **Authors** | Valmeekam et al. |
| **Year** | 2022 |
| **Venue** | arXiv 2022 |
| **Field** | Agi |
| **Subfield** | Agentic Llms Tool Use |
| **Tasks** | planning, benchmarks, evaluation |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2206.10498v3.pdf){: .btn .btn--primary .btn--large}
