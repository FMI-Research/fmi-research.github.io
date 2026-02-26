---
title: 'Voyager: An Open-Ended Embodied Agent with Large Language Models'
collection: papers
permalink: /papers/agi/voyager_an_open-ended_embodied_agent_with_large_language_models/
date: '2023-05-25'
year: 2023
field: agi
subfield: agentic-llms-tool-use
tasks:
- embodied-agents
- skill-library
- curriculum
- lifelong-learning
tier: 3
artifact_type: paper
venue: arXiv 2023
authors:
- Guanzhi Wang
- Yuqi Xie
- Yunfan Jiang
- Ajay Mandlekar
authors_short: Wang et al.
paperurl: https://arxiv.org/pdf/2305.16291.pdf
doi: 10.48550/arXiv.2305.16291
license: unspecified
summary: 'Constructs an open-ended embodied agent in Minecraft consisting of three
  tightly integrated components: an automatic curriculum that proposes progressively
  harder tasks based on the agent''s current inventory and world state, an iterative
  self-verification loop where GPT-4 writes, executes, and debugs Mineflayer JavaScript
  code until a task is confirmed complete, and a skill library that stores verified
  code snippets indexed by text embeddings for retrieval in future tasks—collectively
  discovering 3.3× more unique items than prior state-of-the-art and unlocking the
  full tech tree significantly faster.'
why_important: Established code-as-skill-representation as a viable approach to compositional,
  lifelong agent learning—where skills accumulate without catastrophic forgetting
  because they are stored externally as executable programs rather than in neural
  weights—and demonstrated that LLMs can serve as both planner and programmer in open-ended
  environments, inspiring subsequent work on code-based agent reasoning and self-improving
  skill libraries.
tags:
- embodied-agents
- minecraft
- skill-library
- lifelong-learning
---

## Summary

Voyager constructs an open-ended embodied agent in Minecraft by integrating three tightly coupled components. The **automatic curriculum** uses GPT-4 to propose the next learning objective conditioned on the agent's current inventory, skill library, and exploration history—balancing novelty-seeking with achievability to ensure the agent progressively unlocks more complex Minecraft mechanics (from wood gathering to diamond mining). The **iterative prompting mechanism** has GPT-4 generate Mineflayer JavaScript API code for the proposed task, execute it in the Minecraft environment, observe the result (success, error message, or partial completion), and iteratively debug and revise the code until the task is either solved or a budget is exhausted. The **skill library** stores verified, working code snippets indexed by GPT-3.5-generated natural-language descriptions and retrieved via embedding similarity—allowing the agent to reuse prior skills as building blocks for new tasks rather than rediscovering them from scratch.

Empirically, Voyager discovers 3.3× more unique items than the prior state-of-the-art Minecraft agent (DECKARD), reaches key milestones in the tech tree (crafting a diamond pickaxe, finding a stronghold) in roughly half the interaction steps, and demonstrates generalization to unseen biomes in zero-shot evaluation. A critical ablation shows that the skill library is essential: without it, the agent relearns wood-chopping at every session restart because it cannot retain episodic knowledge across environment resets. Without the automatic curriculum, the agent stagnates on easy tasks. Without iterative debugging, the code execution success rate drops from ~72% to ~41%.

The choice to represent skills as executable code—rather than as natural-language instructions, fine-tuned model weights, or learned latent vectors—is the central methodological innovation. Code provides precise, interpretable semantics; it composes naturally (one skill can call another); it generalizes across environment instances (the same wood-chopping script works on any tree); and it can be verified by execution, making the skill library self-curating. This stands in contrast to approaches that store skills as gradient updates or task embeddings, which lack interpretability and compositional structure.

## Why It Matters

Voyager demonstrated that LLMs can function as the cognitive core of a lifelong learning agent in an open-ended environment—without any environment-specific fine-tuning, reward shaping, or human curriculum design. This result directly bridges the LLM agent literature and the continual/lifelong learning literature, suggesting that large pretrained models can serve as universal priors over procedural knowledge that transfer to new tasks via code generation rather than gradient adaptation. The code-as-skill approach has since influenced agent systems in robotic manipulation (Code as Policies), web automation (WebAgent), and scientific experiment design.

Voyager also raises important open questions that define the frontier of embodied agent research. The agent's curriculum is bounded by GPT-4's knowledge of Minecraft mechanics, making it unclear how to extend the approach to domains where the LLM lacks strong priors. The skill library grows without pruning, raising questions about scalability and skill conflict resolution. And the iterative debugging loop is expensive—each task attempt consumes multiple LLM calls—motivating research into more sample-efficient skill acquisition, learned code critics, and hybrid approaches that combine LLM-generated code with model-free reinforcement learning for fine-grained motor control. The Voyager paradigm also remains untested in partially observable, adversarial, or physically realistic environments where the simulation-to-reality gap introduces failure modes invisible in Minecraft.

| | |
|---|---|
| **Authors** | Wang et al. |
| **Year** | 2023 |
| **Venue** | arXiv 2023 |
| **Field** | Agi |
| **Subfield** | Agentic Llms Tool Use |
| **Tasks** | embodied-agents, skill-library, curriculum, lifelong-learning |
| **Tier** | 3 — Benchmark / Auxiliary |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2305.16291.pdf){: .btn .btn--primary .btn--large}
