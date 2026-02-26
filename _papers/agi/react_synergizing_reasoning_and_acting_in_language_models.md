---
title: 'ReAct: Synergizing Reasoning and Acting in Language Models'
collection: papers
permalink: /papers/agi/react_synergizing_reasoning_and_acting_in_language_models/
date: '2022-10-06'
year: 2022
field: agi
subfield: agentic-llms-tool-use
tasks:
- reasoning-acting
- tool-use
- prompting
tier: 1
artifact_type: paper
venue: arXiv / ICLR 2023
authors:
- Shunyu Yao
- Jeffrey Zhao
- Dian Yu
- Nan Du
authors_short: Yao et al.
paperurl: https://arxiv.org/pdf/2210.03629.pdf
doi: 10.48550/arXiv.2210.03629
license: unspecified
summary: Introduces a prompting strategy that interleaves chain-of-thought reasoning
  traces with environment-interaction actions (search, click, lookup) in a think–act–observe
  loop, enabling LLMs to ground their reasoning in external observations.
why_important: Established the Thought–Action–Observation loop as the dominant architectural
  primitive for tool-augmented LLM agents, directly influencing LangChain, OpenAI
  function calling, and virtually every subsequent agentic framework.
tags:
- react
- reasoning
- acting
- tool-use
- prompting
---

## Summary

ReAct introduces a prompting strategy that interleaves **Thought–Action–Observation** triplets in a single context window, allowing a language model to reason about what it knows, issue a grounded action (e.g., a Wikipedia API search, a click, or an item purchase), and then update its reasoning based on the returned observation. Unlike chain-of-thought (CoT) prompting, which generates reasoning traces entirely from parametric knowledge, ReAct grounds each reasoning step in retrieved evidence; and unlike pure action-generation approaches (e.g., WebGPT-style), it produces transparent intermediate reasoning that aids human oversight and error diagnosis.

Empirically, ReAct substantially outperforms both CoT-only and action-only baselines across four diverse benchmarks: HotpotQA and FEVER (multi-hop knowledge-intensive QA requiring Wikipedia retrieval), AlfWorld (text-based household task completion), and WebShop (simulated e-commerce navigation). On HotpotQA, ReAct improves exact-match accuracy by 7+ points over CoT, while on AlfWorld it achieves 71% task success versus 45% for the action-only baseline. Crucially, the reasoning traces produced by ReAct allow researchers to audit why the agent made specific decisions, revealing failure modes (such as over-reliance on a single search result) that are invisible in action-only logs.

A key methodological choice is that ReAct requires no model fine-tuning—it works entirely through few-shot prompting with human-authored Thought–Action–Observation exemplars. This simplicity is both a strength (it can be applied to any sufficiently capable LLM) and a limitation (quality depends heavily on exemplar design). The paper also introduces a hybrid variant, ReAct + CoT-SC (self-consistency), that uses ReAct for retrieval-heavy steps and falls back to CoT for reasoning-heavy steps, further boosting performance.

## Why It Matters

ReAct's Thought–Action–Observation loop became the architectural primitive underlying most subsequent agentic frameworks. LangChain's `AgentExecutor`, OpenAI's function-calling interface, and Microsoft's Semantic Kernel all implement variants of this pattern, making it arguably the most widely deployed prompting technique in production AI systems. Its influence on AutoGen, Voyager, and nearly every paper in this collection is direct and acknowledged.

Beyond immediate practical impact, ReAct surfaced a fundamental insight: that grounding reasoning in external observations reduces hallucination more effectively than scaling up model parameters alone, foreshadowing the "retrieval as regularization" perspective central to RAG and related work. Open questions it left unanswered—including how to design exemplars systematically, how to handle long observation chains within a fixed context window, and how to make the reasoning trace itself verifiable—remain active research problems, particularly as context windows grow and agents are tasked with increasingly long-horizon objectives.

| | |
|---|---|
| **Authors** | Yao et al. |
| **Year** | 2022 |
| **Venue** | arXiv / ICLR 2023 |
| **Field** | Agi |
| **Subfield** | Agentic Llms Tool Use |
| **Tasks** | reasoning-acting, tool-use, prompting |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2210.03629.pdf){: .btn .btn--primary .btn--large}
