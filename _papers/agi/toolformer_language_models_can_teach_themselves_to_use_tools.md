---
title: 'Toolformer: Language Models Can Teach Themselves to Use Tools'
collection: papers
permalink: /papers/agi/toolformer_language_models_can_teach_themselves_to_use_tools/
date: '2023-02-09'
year: 2023
field: agi
subfield: agentic-llms-tool-use
tasks:
- tool-use
- self-supervised
- api-calls
tier: 1
artifact_type: paper
venue: arXiv / NeurIPS 2023
authors:
- Timo Schick
- Jane Dwivedi-Yu
- Roberto Dessi
- Roberta Raileanu
authors_short: Schick et al.
paperurl: https://arxiv.org/pdf/2302.04761.pdf
doi: 10.48550/arXiv.2302.04761
license: unspecified
summary: Introduces a self-supervised pipeline that bootstraps tool-use annotations
  via in-context learning and then fine-tunes a language model on tool calls that
  demonstrably reduce next-token prediction loss, covering a calculator, QA system,
  Wikipedia search, calendar, and translation API.
why_important: Demonstrated that tool-use can be learned through self-supervision
  rather than requiring expensive human annotation or hand-crafted prompts, establishing
  the key distinction between prompt-driven and weight-integrated tool use that shapes
  agent architecture taxonomies.
tags:
- tool-use
- self-supervised
- api
- agents
---

## Summary

Toolformer presents a self-supervised pipeline for teaching a language model to invoke external APIs at the right moment and with the right arguments. The core idea is to use an existing LLM (GPT-3) to speculatively annotate a large text corpus with candidate API call insertions—for five tools: a calculator, a Wikipedia search engine, a QA model, a calendar, and a machine translation API—and then filter those annotations to retain only calls that reduce next-token prediction loss on the surrounding context. The filtered dataset is used to fine-tune a GPT-J (6.7B parameter) model, producing Toolformer: a model that has internalized when tool use is genuinely helpful rather than being prompted to use tools unconditionally.

Empirically, Toolformer achieves performance competitive with or exceeding GPT-3 (175B) on several downstream tasks when tool use is relevant: outperforming GPT-3 on TriviaQA (Wikipedia search), SVAMP and ASDiv (calculator), and language identification (translation API), all with a model more than 25× smaller. The perplexity-based filtering criterion is critical to this success—without it, the model learns to insert spurious API calls that hurt generation quality. The paper also demonstrates that Toolformer generalizes to holding out individual tools during training, suggesting it learns a general tool-invocation competency rather than task-specific shortcuts.

The annotation pipeline itself is a methodological innovation: by using few-shot prompting to generate and then score hypothetical API calls, Toolformer avoids the expensive human annotation that previous tool-augmented models required (e.g., WebGPT). The loss-reduction filtering criterion operationalizes a principled notion of "useful tool call"—one that provides information the model could not have inferred from its parameters alone—and this principle has influenced subsequent work on self-supervised reward signals for tool-use fine-tuning.

## Why It Matters

Toolformer established the distinction between **prompt-driven tool use** (telling a model to use a tool via in-context instructions, as in ReAct) and **weight-integrated tool use** (training a model so that tool invocation is part of its generative prior). This distinction matters architecturally: prompt-driven approaches are flexible but depend on prompt quality and context length; weight-integrated approaches are more robust and efficient but require curated training data and a fine-tuning budget. Subsequent systems such as Gorilla, ToolLLM, and OpenAI's function-calling fine-tuned models all operate in the weight-integrated regime Toolformer pioneered.

The paper's limitations also shaped the field's research agenda. Toolformer cannot compose multiple tool calls in sequence (it sees at most one API result per call site), cannot learn new tools without retraining, and its filtering heuristic can miss beneficial tool calls with high variance outputs. These gaps motivated work on multi-step tool-use reasoning (ToolChain, AnyTool), dynamic tool discovery (Gorilla with tool retrieval), and reinforcement learning approaches to tool-use optimization that treat the full action sequence as a trajectory rather than an independent insertion problem.

| | |
|---|---|
| **Authors** | Schick et al. |
| **Year** | 2023 |
| **Venue** | arXiv / NeurIPS 2023 |
| **Field** | Agi |
| **Subfield** | Agentic Llms Tool Use |
| **Tasks** | tool-use, self-supervised, api-calls |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2302.04761.pdf){: .btn .btn--primary .btn--large}
