---
title: Agentic Large Language Models, a survey
collection: papers
permalink: /papers/agi/agentic_large_language_models_a_survey/
date: '2025-01-15'
year: 2025
field: agi
subfield: agentic-llms-tool-use
tasks:
- agent-taxonomy
- reasoning
- interaction
tier: 1
artifact_type: paper
venue: arXiv 2025
authors:
- Aske Plaat
- Annie Wong
- Suzan Verberne
- Jan van Rijn
authors_short: Plaat et al.
paperurl: https://liacs.leidenuniv.nl/~plaata1/papers/Agentic_LLM__a_Survey.pdf
doi: ''
license: unspecified
summary: Organizes agentic LLMs around three core dimensions—reasoning, acting, and
  interacting—providing a rigorous conceptual framework that distinguishes genuine
  agents from LLMs that merely call APIs, with coverage of multi-agent collaboration
  and environment grounding.
why_important: Offers a sharper definitional grounding than tool-use-centric taxonomies,
  which is critical as the field risks conflating any prompted LLM with a true agent;
  particularly valuable for calibrating capability claims.
tags:
- survey
- agents
- reasoning
- interaction
---

## Summary

Plaat et al. organize the agentic LLM landscape around three orthogonal dimensions: **reasoning** (the capacity to plan, decompose, and self-evaluate before acting), **acting** (the ability to invoke tools, execute code, or modify environments), and **interacting** (communication with humans, other agents, or external systems). Unlike earlier surveys that categorize agents primarily by the tools they access, this framework emphasizes that agenthood requires all three dimensions working together—a model that can retrieve documents but cannot plan how to use them or communicate its uncertainty is not, in any meaningful sense, an agent.

The survey covers the state of the field as of early 2025, including single-agent systems with extended reasoning (o1-style deliberation, chain-of-thought with verification), multi-agent architectures with explicit role differentiation (planners, critics, executors), and hybrid systems that combine LLM reasoning with symbolic search or reinforcement learning. The authors evaluate a range of benchmarks across coding, mathematical reasoning, web navigation, and embodied control, noting that performance gains on standard benchmarks often do not transfer to open-ended deployment settings.

A notable contribution is the survey's treatment of **interaction patterns**: how agents maintain shared state across turns, how they resolve conflicts in multi-agent settings, and how they escalate uncertainty to human overseers. This dimension is often underemphasized in tool-use surveys, yet it is precisely where deployed systems most frequently fail—agents that reason and act correctly in isolation frequently break down when interoperating with other agents or receiving ambiguous human instructions.

## Why It Matters

By grounding the definition of "agent" in behavioral dimensions rather than architectural components alone, this survey helps the field avoid the terminological inflation that emerged circa 2023–2024, when any LLM with a function-calling API was labeled an agent. The reasoning–acting–interacting framework provides a checklist against which concrete systems can be evaluated for genuine agenthood, which is practically important for setting appropriate expectations in product settings and for identifying which capability gaps remain most critical.

The survey also provides one of the most up-to-date analyses of multi-agent interaction dynamics, an area that is growing rapidly with the deployment of frameworks like AutoGen, CrewAI, and OpenAI's Swarm. Open questions it highlights—including emergent coordination failures in large agent networks, the alignment challenge of maintaining consistent values across agent roles, and the absence of interaction-level benchmarks—define a productive research agenda for the near term.

| | |
|---|---|
| **Authors** | Plaat et al. |
| **Year** | 2025 |
| **Venue** | arXiv 2025 |
| **Field** | Agi |
| **Subfield** | Agentic Llms Tool Use |
| **Tasks** | agent-taxonomy, reasoning, interaction |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://liacs.leidenuniv.nl/~plaata1/papers/Agentic_LLM__a_Survey.pdf){: .btn .btn--primary .btn--large}
