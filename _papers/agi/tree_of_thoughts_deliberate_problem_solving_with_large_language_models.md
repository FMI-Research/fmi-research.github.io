---
title: 'Tree of Thoughts: Deliberate Problem Solving with Large Language Models'
collection: papers
permalink: /papers/agi/tree_of_thoughts_deliberate_problem_solving_with_large_language_models/
date: '2023-05-17'
year: 2023
field: agi
subfield: agentic-llms-tool-use
tasks:
- inference-time-search
- reasoning
- planning
tier: 1
artifact_type: paper
venue: arXiv / NeurIPS 2023
authors:
- Shunyu Yao
- Dian Yu
- Jeffrey Zhao
- Izhak Shafran
authors_short: Yao et al.
paperurl: https://arxiv.org/pdf/2305.10601.pdf
doi: 10.48550/arXiv.2305.10601
license: unspecified
summary: Generalizes chain-of-thought prompting into a tree-structured search over
  intermediate "thoughts," using LLM-based state evaluation and BFS or DFS traversal
  to allow deliberate backtracking—achieving 74% on Game of 24 versus 4% with standard
  CoT.
why_important: Provided the conceptual framework for inference-time compute scaling,
  anticipating the o1/o3 paradigm of spending more compute at test time; directly
  inspired subsequent work on process reward models, MCTS-augmented reasoning, and
  self-refinement pipelines.
tags:
- tree-of-thoughts
- reasoning
- search
- planning
---

## Summary

Tree of Thoughts (ToT) reframes language model inference as a search problem over a tree of intermediate **thoughts**—coherent language sequences that represent partial solutions or reasoning steps. Rather than committing greedily to a single chain of reasoning (as standard CoT does), ToT generates multiple candidate thoughts at each step, evaluates them using the LLM itself as a value function (via prompts asking "is this a promising partial solution?"), and traverses the resulting tree with BFS or DFS. This allows the model to explore alternative reasoning paths and backtrack from dead ends, capabilities that are entirely absent from greedy decoding.

The empirical results are striking. On Game of 24 (find an arithmetic expression using four numbers that equals 24), standard CoT achieves approximately 4% success while ToT with BFS achieves 74%—an 18× improvement. On a mini-crossword task, ToT solves 20% of puzzles versus nearly 0% for CoT. On a creative writing task requiring passage-level coherence, ToT produces significantly more logically consistent outputs as rated by GPT-4 and humans. The value function—a simple LLM-based evaluator prompted to rate partial solutions—turns out to be surprisingly reliable at distinguishing productive from unproductive reasoning paths despite being imperfect.

The framework's modular design is a key methodological strength: thought decomposition (how to break the problem into steps), thought generation (sampling or proposing candidates), state evaluation (value function prompt design), and search algorithm (BFS/DFS/beam) are all separable design choices that can be tuned independently. The paper provides ablation studies showing that all four choices matter, and that the value function quality is the primary bottleneck—a finding that directly motivated subsequent work on training dedicated process reward models (PRMs) rather than relying on prompted LLM evaluators.

## Why It Matters

Tree of Thoughts provided the conceptual scaffolding for the inference-time compute scaling paradigm that culminated in OpenAI's o1 and o3 models. The core insight—that spending more compute at inference time via search over reasoning trajectories can substitute for or complement increases in model size—has since been validated at scale and is now a mainstream approach to frontier model development. ToT's framework also inspired direct successors including Graph of Thoughts (arbitrary DAG structure), Reasoning via Planning (MCTS with learned value functions), and Monte Carlo Tree Search augmented LLM reasoners.

The paper's limitations are equally instructive. ToT's inference cost scales with the branching factor and search depth, making it prohibitively expensive for long-horizon tasks without significant optimization. The reliance on prompted LLM value functions introduces circularity (the model evaluates its own reasoning) and noise. These limitations drove research into training dedicated verifiers and critics (process reward models, outcome reward models), into more efficient search algorithms, and ultimately into distilling search-augmented reasoning into model weights via RLHF—the approach taken by o1. The question of when to use implicit (in-weights) versus explicit (in-context) search remains an active and consequential open problem.

| | |
|---|---|
| **Authors** | Yao et al. |
| **Year** | 2023 |
| **Venue** | arXiv / NeurIPS 2023 |
| **Field** | Agi |
| **Subfield** | Agentic Llms Tool Use |
| **Tasks** | inference-time-search, reasoning, planning |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2305.10601.pdf){: .btn .btn--primary .btn--large}
