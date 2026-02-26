---
title: 'OpenHands: An Open Platform for AI Software Developers as Generalist Agents'
collection: papers
permalink: /papers/agi/openhands_an_open_platform_for_ai_software_developers_as_generalist_agents/
date: '2024-07-23'
year: 2024
field: agi
subfield: agentic-llms
tasks:
- software-development
- agent-platform
- code-execution
tier: 2
artifact_type: paper
venue: arXiv 2024
authors:
- Xingyao Wang
- Boxuan Li
- Yufan Song
- Frank F. Xu
- Xiangru Tang
- Mingchen Zhuge
- Jiayi Pan
- Yueqi Song
- Bowen Li
- Jaskirat Singh
- Hoang H. Tran
- Fuqiang Li
- Ren Ma
- Mingzhang Zheng
- Bill Qian
- Yanjun Shao
- Niklas Muennighoff
- Yizhe Zhang
- Binyuan Hui
- Junyang Lin
- Robert Brennan
- Hao Peng
- Heng Ji
- Graham Neubig
authors_short: Wang et al.
paperurl: https://arxiv.org/pdf/2407.16741.pdf
doi: 10.48550/arXiv.2407.16741
license: unspecified
summary: 'OpenHands provides three integrated layers for software-agent research:
  a Docker-sandboxed execution environment (terminal, file system, browser), a pluggable
  agent runtime compatible with any LLM backend, and a unified EventStream architecture
  that serializes all observations and actions into a typed, replayable event log
  — enabling reproducible, inspectable agent trajectories across SWE-Bench, WebArena,
  and GAIA evaluations.'
why_important: Became the de-facto open platform for software-engineering agent research,
  enabling fair ablation studies and motivating specialized agent architectures (SWE-agent,
  Agentless, Moatless Tools) against a common baseline; current resolve rates on full
  SWE-Bench remain substantially lower than on the easier Verified subset, exposing
  persistent gaps in multi-file refactoring, long-context navigation, and project-convention
  understanding that drive ongoing research into retrieval-augmented code agents.
tags:
- agents
- software-engineering
- open-source
- code-generation
---

## Summary

OpenHands (previously OpenDevin) is organized around three integrated layers. The execution layer provides Docker-sandboxed environments in which agents can run arbitrary bash commands, edit files, spawn subprocesses, and interact with a real browser — each task gets a fresh container, preventing environment state from leaking between runs. The agent runtime layer provides a pluggable interface that accepts any LLM backend (OpenAI, Anthropic, local models via vLLM) and exposes a standardized action space: `run`, `write`, `browse`, `think`, and `finish`. The observation-action loop is serialized by a unified *EventStream* architecture that logs every observation and action as a typed, timestamped event, making full trajectory replay and post-hoc analysis straightforward. The default *CodeActAgent* follows a ReAct-style interleaving of natural-language reasoning traces and concrete tool calls, closely mirroring how a human engineer would approach an unfamiliar codebase.

On SWE-Bench Verified — a curated subset of 500 GitHub issues judged to have unambiguous acceptance criteria — OpenHands with GPT-4o as backend resolves a competitive fraction of issues, placing near the top of the public leaderboard at time of publication. The platform also supports multi-agent orchestration through a *delegator/solver* pattern: a high-level orchestrator agent decomposes a complex task into subtasks and dispatches them to specialized solver agents, with results aggregated back to the orchestrator. This architecture is evaluated on GAIA (general assistant benchmark) and WebArena alongside SWE-Bench, enabling a unified evaluation across diverse agent task types within the same infrastructure.

The key engineering contribution is the EventStream design, which provides a single canonical representation for all agent–environment interactions. This makes it possible to implement trajectory-level analysis tools (e.g., action replay, failure attribution, agent comparison) as generic EventStream consumers rather than environment-specific scripts. OpenHands also introduces a standardized task specification format used across SWE-Bench, WebArena, and GAIA evaluations, enabling direct cross-benchmark comparisons without reformatting prompts. The sandboxed execution model — which isolates each agent run at the OS level — allows researchers to safely run agents against real codebases and websites without risking host system modification.

## Why It Matters

OpenHands became the de-facto open research platform for software-engineering agents, enabling fair ablation studies, reproducible baselines, and community comparisons that are impossible on closed commercial systems. Its public availability catalyzed a wave of specialized agent architectures — SWE-agent (shell-based file editor), Agentless (localization-then-patch decomposition), Moatless Tools (semantic code search + targeted editing) — all benchmarked against a common infrastructure, making result comparisons meaningful across papers. The EventStream logging enabled systematic failure mode analysis: researchers identified that agents frequently produce syntactically valid but semantically incorrect patches, make redundant file edits that reintroduce already-fixed bugs, and fail to locate relevant code when repositories exceed ~50K lines — insights that directly shaped subsequent retrieval-augmented code navigation work.

The platform's current limitations reflect the state of the art in software agent research rather than design choices. Resolve rates on full SWE-Bench (as opposed to the easier "Verified" subset) remain substantially lower, exposing persistent gaps in multi-file refactoring, long-range context management across large codebases, and understanding of project-specific conventions not captured in the issue description alone. Agents also struggle to distinguish between a correct patch that passes tests and a patch that games the test suite without fixing the underlying issue — a subtle but critical reliability problem. These gaps are driving active research into hierarchical multi-agent orchestration, repository-level retrieval augmentation (RepoGraph, SWE-RAG), and fine-tuning on agent trajectories collected via OpenHands itself to produce more capable base policies.

| | |
|---|---|
| **Authors** | Wang et al. |
| **Year** | 2024 |
| **Venue** | arXiv 2024 |
| **Field** | Agi |
| **Subfield** | Agentic Llms |
| **Tasks** | software-development, agent-platform, code-execution |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2407.16741.pdf){: .btn .btn--primary .btn--large}
