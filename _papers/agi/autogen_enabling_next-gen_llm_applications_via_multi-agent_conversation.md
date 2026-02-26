---
title: 'AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation'
collection: papers
permalink: /papers/agi/autogen_enabling_next-gen_llm_applications_via_multi-agent_conversation/
date: '2023-08-16'
year: 2023
field: agi
subfield: agentic-llms-tool-use
tasks:
- multi-agent
- orchestration
- conversation
tier: 2
artifact_type: paper
venue: arXiv 2023
authors:
- Qingyun Wu
- Gagan Bansal
- Jieyu Zhang
- Yiran Wu
authors_short: Wu et al.
paperurl: https://arxiv.org/pdf/2308.08155.pdf
doi: 10.48550/arXiv.2308.08155
license: unspecified
summary: Introduces a conversation-centric multi-agent framework in which heterogeneous
  agents (AssistantAgent, UserProxyAgent, GroupChatManager) exchange structured messages,
  with each agent configurable as an LLM, a code executor, or a human-in-the-loop,
  enabling composable workflows for math reasoning, code generation, retrieval-augmented
  chat, and online decision-making.
why_important: Demonstrated that multi-agent conversation is a unifying interface
  for complex LLM applications, influencing production systems at Microsoft and catalyzing
  the orchestration-framework design pattern (alongside LangGraph, CrewAI, and similar
  projects) that now underlies most enterprise agentic deployments.
tags:
- multi-agent
- orchestration
- framework
- agents
---

## Summary

AutoGen introduces a **conversation-centric multi-agent framework** in which diverse agent types—AssistantAgent (LLM-backed), UserProxyAgent (code executor or human proxy), and GroupChatManager (orchestrator)—communicate exclusively through structured message exchanges. Each agent is independently configurable: an AssistantAgent can be backed by any LLM API, a UserProxyAgent can auto-execute code in a sandboxed Docker container or surface output to a human, and the GroupChatManager routes messages to agents using a customizable speaker-selection policy. Crucially, these conversation patterns are **composable**: two-agent dyads, group chats, and nested conversations (where one agent orchestrates a sub-conversation of other agents) can all be combined to build arbitrarily complex workflows.

The paper demonstrates AutoGen across six task categories: mathematical reasoning (solving competition-level problems by alternating between a code-writing assistant and a code-executor), retrieval-augmented code generation, automated online decision-making (web browsing), dynamic group chat with tool use, conversational chess with an engine backend, and a supply-chain optimization scenario requiring multi-step planning. Across these diverse settings, the multi-agent conversation pattern consistently outperforms single-agent baselines and matches or exceeds specialized single-purpose systems, demonstrating that the conversation interface is a genuinely general abstraction.

A key design choice—and differentiator from competing frameworks—is **human-in-the-loop integration**: UserProxyAgent can be configured to request human approval before executing any code, to override agent decisions, or to inject corrections mid-conversation. This design acknowledges that fully autonomous multi-agent execution introduces safety risks, and that practical deployment almost always requires some level of human oversight. The paper also provides an analysis of failure modes, identifying situations where agents fall into infinite conversation loops or produce syntactically valid but semantically incorrect code that passes silent execution.

## Why It Matters

AutoGen crystallized the **orchestration framework** as a design pattern and provided an open-source reference implementation that has become one of the most widely adopted LLM libraries in production environments, with adoption at Microsoft (Copilot Studio, Azure AI), as well as in academic research across dozens of application domains. Its influence is evident in successor frameworks including LangGraph, CrewAI, and OpenAI's Assistants API, all of which adopt conversation-as-interface as their central abstraction.

The framework also surfaced important research questions about multi-agent safety and reliability. In practice, AutoGen-based systems exhibit failure modes including agent hallucination propagation (one agent's incorrect output becoming ground truth for downstream agents), role confusion (agents violating their assigned persona), and non-termination in cyclic conversation graphs. These challenges have motivated subsequent work on multi-agent benchmarks (AgentBench, CAMEL), formal verification of agent interaction protocols, and reinforcement learning approaches to agent policy optimization—pushing multi-agent coordination from an engineering problem to a research frontier.

| | |
|---|---|
| **Authors** | Wu et al. |
| **Year** | 2023 |
| **Venue** | arXiv 2023 |
| **Field** | Agi |
| **Subfield** | Agentic Llms Tool Use |
| **Tasks** | multi-agent, orchestration, conversation |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2308.08155.pdf){: .btn .btn--primary .btn--large}
