---
title: Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks
collection: papers
permalink: /papers/agi/retrieval-augmented_generation_for_knowledge-intensive_nlp_tasks/
date: '2020-10-22'
year: 2020
field: agi
subfield: agentic-llms-tool-use
tasks:
- rag
- retrieval
- knowledge-intensive
tier: 2
artifact_type: paper
venue: arXiv / NeurIPS 2020
authors:
- Patrick Lewis
- Ethan Perez
- Aleksandra Piktus
- Fabio Petroni
authors_short: Lewis et al.
paperurl: https://arxiv.org/pdf/2005.11401.pdf
doi: 10.48550/arXiv.2005.11401
license: unspecified
summary: Proposes Retrieval-Augmented Generation (RAG), which couples a dense passage
  retriever (DPR over a Wikipedia index) with a BART seq2seq generator trained end-to-end
  by marginalizing over top-k retrieved documents, introducing two variants—RAG-Sequence
  and RAG-Token—that achieved state-of-the-art on Natural Questions, TriviaQA, and
  WebQuestions while producing more factually specific outputs than purely parametric
  T5.
why_important: Established the retrieve-then-generate paradigm that now underlies
  virtually all production knowledge-grounded LLM systems, from enterprise Q&A chatbots
  to scientific literature assistants; the end-to-end differentiable retriever-generator
  training objective remains the reference point against which modern dense retrieval
  and re-ranking methods are benchmarked.
tags:
- rag
- retrieval
- knowledge
- factuality
---

## Summary

Lewis et al. introduce Retrieval-Augmented Generation (RAG), a hybrid architecture that combines a **non-parametric memory** (a dense retrieval index over 21 million Wikipedia passages) with a **parametric generator** (BART-large seq2seq model) in an end-to-end differentiable system. The retriever is a bi-encoder DPR model that maps query and passage to dense vector representations and retrieves the top-k passages by maximum inner product search; the generator conditions on the concatenation of the input query and each retrieved passage to produce the final output. Two variants are introduced: **RAG-Sequence**, which uses the same set of retrieved documents for the entire output sequence and marginalizes over them at the sequence level, and **RAG-Token**, which allows different documents to influence different output tokens by marginalizing the retrieval distribution at each generation step—making RAG-Token more expressive at the cost of higher inference complexity.

Empirically, RAG achieves state-of-the-art results on Natural Questions (44.5 exact match), TriviaQA (56.8), and WebQuestions (45.5) in the open-domain (no provided passage) setting, outperforming both the T5 parametric baseline and prior retrieval-augmented approaches including REALM and DPR+reader pipelines. A qualitative analysis demonstrates that RAG generates answers that are more factually specific—naming particular people, dates, and places—compared to T5, which tends to produce plausible but vague responses drawn from parametric knowledge. The system is also more gracefully updateable: swapping the retrieval index to a more recent Wikipedia snapshot improves factual accuracy without any retraining.

The training procedure is a methodological highlight: because the retriever index is fixed during training (gradient does not flow through the MIPS index), the system is trained by marginalizing over the top-k retrieved documents using the sum of their joint probabilities—effectively treating retrieval as a latent variable. This approximation makes training tractable and allows the retriever and generator to be jointly optimized using standard backpropagation through the generator alone, with periodic retriever refresh. The paper also introduces a practical finding that top-5 to top-10 retrieved documents provide most of the benefit, with diminishing returns beyond that.

## Why It Matters

RAG established the **retrieve-then-generate** paradigm that is now the dominant architecture for knowledge-grounded NLP systems. Its influence permeates production deployments across virtually every major AI provider—from Azure OpenAI's on-your-data feature and Amazon Bedrock's knowledge bases to open-source stacks (LlamaIndex, LangChain RAG chains) used in thousands of enterprise applications. The paper's core insight—that separating world knowledge from reasoning capability allows each to be optimized and updated independently—remains the primary justification for RAG over purely parametric approaches, even as model sizes have grown dramatically.

The limitations of the original RAG formulation have shaped an active research agenda. Fixed retrieval granularity (passage-level), single-hop retrieval, and the MIPS approximation all degrade performance on complex multi-hop questions, motivating work on iterative and recursive RAG (IRCoT, FLARE, Self-RAG), hierarchical retrieval architectures, and learned query rewriting. The tension between retrieving relevant context and maintaining generation fluency—especially when retrieved passages are noisy or contradictory—remains an open problem at the frontier of factuality research, with practical implications for deploying LLM-based systems in high-stakes domains where hallucination is unacceptable.

| | |
|---|---|
| **Authors** | Lewis et al. |
| **Year** | 2020 |
| **Venue** | arXiv / NeurIPS 2020 |
| **Field** | Agi |
| **Subfield** | Agentic Llms Tool Use |
| **Tasks** | rag, retrieval, knowledge-intensive |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2005.11401.pdf){: .btn .btn--primary .btn--large}
