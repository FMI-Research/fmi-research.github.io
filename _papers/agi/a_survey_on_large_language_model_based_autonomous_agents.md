---
title: A Survey on Large Language Model based Autonomous Agents
collection: papers
permalink: /papers/agi/a_survey_on_large_language_model_based_autonomous_agents/
date: '2023-08-22'
year: 2023
field: agi
subfield: agentic-llms-tool-use
tasks:
- agent-taxonomy
- planning
- memory
- evaluation
tier: 1
artifact_type: paper
venue: arXiv 2023
authors:
- Lei Wang
- Chen Ma
- Xueyang Feng
- Zeyu Zhang
authors_short: Wang et al.
paperurl: https://arxiv.org/pdf/2308.11432.pdf
doi: 10.48550/arXiv.2308.11432
license: unspecified
summary: Provides a comprehensive, four-component taxonomy of LLM-based autonomous
  agents—memory, planning, action, and perception—surveying over 100 systems and covering
  applications from software engineering to scientific discovery.
why_important: Establishes the canonical vocabulary and architectural decomposition
  that subsequent agent surveys and systems have adopted, making it the foundational
  reference for understanding how agent components interact.
tags:
- survey
- agents
- planning
- tool-use
- memory
---

## Summary

Wang et al. propose a unified four-component taxonomy for LLM-based autonomous agents, decomposing architectures into **memory** (in-context storage, external databases, and retrieval mechanisms), **planning** (task decomposition, reflection, and self-critique), **action** (tool invocation, environment interaction, inter-agent communication), and **perception** (multi-modal inputs). By applying this framework consistently across more than 100 surveyed systems, the paper enables principled cross-paper comparison that had previously been obscured by inconsistent terminology.

The survey maps these architectural components to concrete application domains including software engineering (code writing, debugging, test generation), scientific discovery (hypothesis formulation, experiment execution), social simulation (agent-based modeling of human behavior), and embodied robotics. For each domain, the authors characterize which components are emphasized, how agents are trained or prompted, and what evaluation protocols have been used—revealing significant heterogeneity in how "agent performance" is measured across the community.

A key methodological contribution is the authors' taxonomy of evaluation approaches, distinguishing subjective human ratings from objective task-completion metrics and highlighting that most agent benchmarks measure only final-answer correctness while ignoring intermediate reasoning quality, tool use efficiency, and robustness to distribution shift. The survey closes with a structured discussion of open challenges including long-horizon memory management, safe action execution, and the absence of standardized benchmarks that span multiple component types simultaneously.

## Why It Matters

This survey established the canonical vocabulary—memory, planning, action, perception—that subsequent agent papers, frameworks, and tutorials have widely adopted. Its four-component decomposition appears in the documentation of LangChain, AutoGen, and similar orchestration libraries, and its application taxonomy is frequently used to organize research agendas at major AI labs. For researchers entering the field, it provides the fastest route to understanding how disparate agent systems relate to one another architecturally.

The survey also surfaces the field's evaluation gap, which has driven subsequent work on standardized benchmarks (AgentBench, ToolBench, WebArena). The observation that most systems optimize for a single component in isolation—while realistic deployment requires all components to work together reliably—remains an open problem that motivates ongoing research into integrated evaluation frameworks and end-to-end agent training.

| | |
|---|---|
| **Authors** | Wang et al. |
| **Year** | 2023 |
| **Venue** | arXiv 2023 |
| **Field** | Agi |
| **Subfield** | Agentic Llms Tool Use |
| **Tasks** | agent-taxonomy, planning, memory, evaluation |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2308.11432.pdf){: .btn .btn--primary .btn--large}
