---
title: 'Reflexion: Language Agents with Verbal Reinforcement Learning'
collection: papers
permalink: /papers/agi/reflexion_language_agents_with_verbal_reinforcement_learning/
date: '2023-03-20'
year: 2023
field: agi
subfield: agentic-llms
tasks:
- verbal-reinforcement
- agent-reasoning
- self-reflection
tier: 2
artifact_type: paper
venue: NeurIPS 2023
authors:
- Noah Shinn
- Federico Cassano
- Ashwin Gopinath
- Karthik Narasimhan
- Shunyu Yao
authors_short: Shinn et al.
paperurl: https://arxiv.org/pdf/2303.11366.pdf
doi: 10.48550/arXiv.2303.11366
license: unspecified
summary: 'Reflexion frames agent improvement as a verbal reinforcement loop: a dedicated
  Reflector module synthesizes natural-language diagnoses of each failure and stores
  them in a sliding episodic memory that conditions all subsequent attempts, enabling
  agents backed by black-box LLM APIs to improve across trials without any weight
  updates.'
why_important: Crystallized natural language as a gradient-free optimization signal
  for LLM agents, directly inspiring self-critique and iterative refinement methods
  (CRITIC, Self-Refine, LATS) and challenging the assumption that task improvement
  requires fine-tuning; limitations around oracle dependence and hallucinated corrections
  motivated later integration of tree search and external tool feedback.
tags:
- agents
- reflection
- verbal-rl
- reasoning
---

## Summary

Reflexion frames agent improvement as a verbal reinforcement loop that deliberately avoids any weight updates. At the end of each trial, a dedicated *Reflector* module receives the agent's action trajectory and a scalar or binary success signal from the environment, then synthesizes a natural-language diagnosis of what went wrong and how the agent should behave differently. This verbal reflection is appended to a sliding episodic memory buffer that conditions the agent's next attempt. Because no gradient computation is required, the framework applies to any LLM accessible only through an inference API — including black-box systems like GPT-4 — making it broadly deployable without access to model internals. Three distinct agent roles are separated: the *Actor* (executes task actions), the *Evaluator* (produces the success signal), and the *Self-Reflector* (generates the verbal critique). This modularity allows each component to be swapped or upgraded independently.

On sequential decision-making (AlfWorld, 25 environment types), Reflexion raises success rate from roughly 25% at trial 1 to over 90% after three reflection cycles. On the HotpotQA multi-hop retrieval task, exact-match accuracy improves by approximately 20 percentage points over chain-of-thought baselines. On HumanEval code synthesis, Reflexion paired with GPT-4 achieves 91% pass@1 — the first published result exceeding 90% on that benchmark. Across all three domains, gains plateau after 3–5 reflection cycles, consistent with the model re-converging to the same failure mode once short-term episodic memory is saturated.

The key methodological insight is that the self-reflection step can be framed as a lightweight prompting task rather than a learned module: the Reflector is simply a prompted call to the same (or a smaller) LLM with a template asking it to identify the failure cause and prescribe a specific corrective strategy. This design means no additional parameters are introduced. To prevent context overflow when reflections accumulate, Reflexion uses a fixed-size memory buffer that evicts the oldest entries, trading temporal depth for context window feasibility. The paper also introduces the concept of *memory-augmented execution traces*, where the full action history of the previous trial is included in the prompt alongside the reflection — providing the model with both a causal account of failure and a prescriptive correction.

## Why It Matters

Reflexion crystallized the idea that natural language can function as a gradient-free optimization signal for LLM agents, opening a design space in which agents improve across trials within a single deployment context without any fine-tuning infrastructure. It directly inspired a family of self-critique and iterative refinement methods — CRITIC (tool-augmented self-verification), Self-Refine (multi-turn critique-and-revision), and LATS (language agent tree search with reflection-guided rollouts) — and made reflection a standard component in agentic frameworks such as LangGraph and AutoGPT derivatives. By demonstrating that verbal feedback can substitute for reward signal in complex reasoning and coding tasks, it also blurred the boundary between "prompting strategies" and "learning algorithms," reshaping how the community thinks about in-context adaptation.

The approach has important structural limitations. It requires a reliable, task-specific success signal (oracle): binary code execution results are straightforward, but most real-world tasks lack a clean, automated evaluator. The Reflector can also produce *hallucinated corrections* — plausible-sounding but incorrect diagnoses that compound errors rather than resolve them, especially when failure is ambiguous. The sliding memory buffer imposes a hard cap on usable reflection depth. Reflexion also cannot recover from fundamental capability gaps: if the base model lacks the knowledge to solve a task at all, verbal self-reflection cannot supply it. These limitations motivated subsequent work — LATS integrates Monte Carlo Tree Search to systematically explore alternative action sequences, and OpenHands incorporates external tool feedback (test runners, linters) to ground reflections in concrete execution signals rather than model-generated diagnoses.

| | |
|---|---|
| **Authors** | Shinn et al. |
| **Year** | 2023 |
| **Venue** | NeurIPS 2023 |
| **Field** | Agi |
| **Subfield** | Agentic Llms |
| **Tasks** | verbal-reinforcement, agent-reasoning, self-reflection |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2303.11366.pdf){: .btn .btn--primary .btn--large}
