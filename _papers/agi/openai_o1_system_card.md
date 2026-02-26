---
title: OpenAI o1 System Card
collection: papers
permalink: /papers/agi/openai_o1_system_card/
date: '2024-09-12'
year: 2024
field: agi
subfield: alignment-safety-evaluation
tasks:
- safety-evaluation
- red-teaming
- system-report
tier: 2
artifact_type: paper
venue: OpenAI Technical Report 2024
authors:
- Aaron Jaech
- Adam Kalai
- Adam Lerer
authors_short: Jaech et al.
paperurl: https://cdn.openai.com/o1-system-card.pdf
doi: ''
license: unspecified
summary: Documents the safety evaluation framework for the o1 reasoning model series,
  which uses reinforcement learning over chain-of-thought traces to solve complex
  tasks; safety evaluations span CBRN uplift, cyberoffense capability, persuasion
  and manipulation resistance, and jailbreak robustness, with o1 receiving a "medium"
  CBRN risk rating — higher than predecessor models — reflecting its greater scientific
  reasoning depth; the card introduces "deliberative alignment," a training approach
  that teaches o1 to reason explicitly about safety policies within its chain of thought
  before generating responses.
why_important: Represents a methodological shift from implicit RLHF-based safety fine-tuning
  to explicit reasoning-time alignment, raising important open questions about whether
  visible chain-of-thought reasoning can be trusted as a safety signal or whether
  it creates new attack surfaces through adversarial reasoning manipulation.
tags:
- system-card
- safety
- red-teaming
- reasoning
---

## Summary

The o1 System Card documents the safety evaluation and risk management framework applied to OpenAI's o1 model series, which uses large-scale reinforcement learning over extended chain-of-thought reasoning traces to solve multi-step problems in mathematics, science, and coding. The safety evaluation architecture spans four risk categories aligned with OpenAI's Preparedness Framework: CBRN (chemical, biological, radiological, nuclear) uplift, cyberoffense capability, persuasion and manipulation, and catastrophic or WMD-adjacent risks. Evaluations combine automated red-teaming (using adversarial prompting at scale), expert human red teams drawn from relevant technical domains, and external safety board review. o1 receives a "medium" risk rating on CBRN uplift — higher than predecessor models — reflecting its substantially greater scientific reasoning capability: it can provide meaningful uplift to actors seeking to synthesize dangerous biological or chemical agents.

On jailbreak and prompt injection robustness, o1 shows significant improvement over GPT-4o across most attack vectors, attributed to the model's deliberative chain-of-thought: longer internal reasoning allows the model to detect adversarial framing that shorter-context models miss. However, evaluations also identify novel "chain-of-thought manipulation" vectors in which adversarially structured prompts embed false premises into the model's own reasoning trace, steering it toward policy-violating conclusions through an internally coherent but corrupted reasoning path. The card introduces *deliberative alignment* as o1's safety training approach: rather than encoding safety behavior implicitly through RLHF, o1 is trained to explicitly reference and reason about OpenAI's safety policies within its chain of thought before generating responses, making safety reasoning visible and auditable.

Methodologically, the System Card sets a new standard for reasoning model safety documentation by reporting per-category risk ratings with explicit uncertainty ranges, documenting the composition and methodology of expert red teams, and describing model-specific mitigations (e.g., refusal refinement for CBRN queries, policy-aware CoT training). It also addresses the oversight paradox specific to reasoning models: longer CoTs provide more auditable reasoning but also surface more potential manipulation attack surface.

## Why It Matters

The o1 System Card represents a methodological shift from RLHF-based safety fine-tuning — where safety is implicit in the policy's learned behavior — to explicit reasoning-time alignment, where safety constraints are enforced through the model's visible reasoning process. This shift raises a fundamental question that will define AI safety research for reasoning-capable models: can visible reasoning be trusted as a faithful safety signal, or does deliberative alignment create a new attack surface through adversarial reasoning manipulation?

The card also established CBRN uplift as a first-class safety evaluation criterion for frontier models, elevating the standard for what constitutes adequate pre-deployment safety documentation. Its structured risk-rating framework and public reporting of red-team findings set a precedent that subsequent system cards and model safety disclosures are measured against, and its identification of chain-of-thought manipulation as a novel attack class has motivated a new research direction at the intersection of adversarial robustness and chain-of-thought interpretability.

| | |
|---|---|
| **Authors** | Jaech et al. |
| **Year** | 2024 |
| **Venue** | OpenAI Technical Report 2024 |
| **Field** | Agi |
| **Subfield** | Alignment Safety Evaluation |
| **Tasks** | safety-evaluation, red-teaming, system-report |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://cdn.openai.com/o1-system-card.pdf){: .btn .btn--primary .btn--large}
