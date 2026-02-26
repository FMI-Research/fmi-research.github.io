---
title: 'AgentBench: Evaluating LLMs as Agents'
collection: papers
permalink: /papers/agi/agentbench_evaluating_llms_as_agents/
date: '2023-08-07'
year: 2023
field: agi
subfield: agentic-llms
tasks:
- agent-evaluation
- benchmark
- interactive-environments
tier: 3
artifact_type: paper
venue: ICLR 2024
authors:
- Xiao Liu
- Hao Yu
- Hanchen Zhang
- Yifan Xu
- Xuanyu Lei
- Hanyu Lai
- Yu Gu
- Hangliang Ding
- Kaiwen Men
- Kejuan Yang
- Shudan Zhang
- Xiang Deng
- Aohan Zeng
- Zhiyuan Liu
- Yuxiao Dong
- Jie Tang
authors_short: Liu et al.
paperurl: https://arxiv.org/pdf/2308.03688.pdf
doi: 10.48550/arXiv.2308.03688
license: unspecified
summary: AgentBench provides 8 interactive evaluation environments (OS Bash, database
  manipulation, knowledge-graph QA, ALFWorld, WebShop, Mind2Web, card games, lateral-thinking
  puzzles) with a unified API that connects any LLM to any environment, and introduces
  trajectory-level metrics (step efficiency, tool-call validity) alongside final success
  rate — revealing a 3–5× overall capability gap between GPT-4 and the best open-source
  models available at evaluation time.
why_important: Established the multi-environment interactive evaluation paradigm adopted
  by successor benchmarks (WebArena, τ-bench, SWE-bench) and its documented proprietary/open-source
  gap motivated large-scale agentic fine-tuning efforts (AgentTuning, AgentInstruct);
  rapid benchmark saturation within a year of publication highlighted the general
  challenge of benchmark obsolescence in LLM evaluation and drove demand for harder,
  longer-horizon tasks.
tags:
- benchmark
- agents
- evaluation
- multi-environment
---

## Summary

AgentBench defines LLM agent evaluation as a multi-dimensional, interactive problem and operationalizes it through 8 carefully constructed environments: OS (multi-step Bash command execution), DB (SQL database manipulation), KG (multi-hop knowledge graph Q&A over Freebase), ALFWorld (text-based household navigation and object manipulation), WebShop (online shopping with a simulated e-commerce interface), Mind2Web (real-website interaction with web element grounding), Card Games (strategic decision-making under uncertainty), and Lateral Thinking puzzles (open-ended natural language reasoning). Unlike static NLP benchmarks, every environment requires sequences of tool calls and actions, making it impossible to achieve good performance through memorized lookup alone. The benchmark provides a unified Python API so any LLM can be connected to any environment without custom integration code, and evaluates agents using both final-outcome success rates and trajectory-level metrics including action validity rate and step efficiency.

The headline empirical finding is a pronounced capability stratification: GPT-4 achieves an overall weighted score of ~4.0 while the best open-source model evaluated (Vicuna-13B) scores approximately 1.0 — a 3–4× gap that is consistent across nearly all environments. Code-specialized models (e.g., WizardCoder) surprisingly outperform general instruction-tuned chat models on OS and DB tasks, while performing worse on ALFWorld and Mind2Web, suggesting that task-specific capability profiles do not transfer across environment types. Performance across environments for a single model is also highly non-uniform: a model that ranks highly on KG Q&A may fail catastrophically on WebShop, indicating that no single underlying competency subsumes general agent capability. Chat models fine-tuned from open-source bases show consistent failure in multi-step tool-use scenarios that require maintaining state across many turns.

A critical methodological contribution is the benchmark's resistance to gaming: all 8 environments involve live interaction with a stateful system rather than static input-output pairs, so agents cannot exploit dataset memorization or shortcut through cached responses. The paper also contributes a taxonomy of agent failure modes — early termination, invalid tool calls, context confusion, and hallucinated observations — that provides diagnostic value beyond aggregate scores. The evaluation harness supports both API-based LLMs and locally hosted models, enabling cost-controlled comparisons across the full capability spectrum from 7B to 175B+ parameter models.

## Why It Matters

AgentBench established the multi-environment interactive evaluation paradigm that all major successor agent benchmarks adopted and extended: WebArena moved to real browser environments, τ-bench targeted tool-use under natural-language constraints, SWE-bench targeted real GitHub issue resolution, and MINT focused on multi-turn tool interaction. The 3–5× proprietary/open-source gap it documented became one of the most widely cited data points in the agent capability literature, directly motivating large-scale agentic fine-tuning efforts — AgentTuning collected 1,866 verified agent trajectories to fine-tune Llama-based models, and AgentInstruct synthesized millions of instruction-following examples specifically designed to close the gap on AgentBench-style tasks. It also shifted the community's evaluation vocabulary: "language model performance" (measured on static Q&A) gave way to "agent performance" (measured on multi-step interactive task completion), making trajectory-level evaluation a standard expectation.

The benchmark's principal limitation is obsolescence velocity: all 8 environments were substantially "solved" or leapfrogged by GPT-4-class agents within roughly a year of publication, underscoring the general benchmark saturation problem in LLM evaluation. The environment set also skews toward text-based interaction and underrepresents visual, embodied, or long-horizon planning tasks that constitute real-world agent deployment scenarios. The Mind2Web environment, while innovative at time of publication, relies on a static snapshot of real websites, which diverge from live web structure over time. These limitations drove demand for harder, more dynamic benchmarks — and motivated the broader methodological debate about whether fixed benchmarks can keep pace with frontier model capabilities or whether continuous, held-out, human-verified task generation is required.



| | |
|---|---|
| **Authors** | Liu et al. |
| **Year** | 2023 |
| **Venue** | ICLR 2024 |
| **Field** | Agi |
| **Subfield** | Agentic Llms |
| **Tasks** | agent-evaluation, benchmark, interactive-environments |
| **Tier** | 3 — Benchmark / Resource |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2308.03688.pdf){: .btn .btn--primary .btn--large}
