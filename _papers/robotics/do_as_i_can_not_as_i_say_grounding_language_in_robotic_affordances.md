---
title: 'Do As I Can, Not As I Say: Grounding Language in Robotic Affordances'
collection: papers
permalink: /papers/robotics/do_as_i_can_not_as_i_say_grounding_language_in_robotic_affordances/
date: '2022-04-04'
year: 2022
field: robotics
subfield: robot-foundation-models-vla
tasks:
- language-grounding
- affordances
- planning
- language-conditioned-control
tier: 2
artifact_type: paper
venue: arXiv / CoRL 2022
authors:
- Michael Ahn
- Anthony Brohan
- Noah Brown
- Yevgen Chebotar
authors_short: Ahn et al.
paperurl: https://arxiv.org/pdf/2204.01691.pdf
doi: 10.48550/arXiv.2204.01691
license: unspecified
summary: SayCan combines the high-level planning capabilities of a large language
  model with learned value functions (affordance functions) that score the physical
  feasibility of each candidate skill in the current robot state, enabling grounded
  long-horizon task execution by selecting only skills that are both linguistically
  plausible and physically executable.
why_important: Established the language-planner plus learned-affordance architecture
  as a canonical approach to grounded robot control, demonstrating for the first time
  that frozen LLMs can direct real robot manipulation at scale when coupled with a
  mechanism that constrains outputs to physically feasible actions.
tags:
- saycan
- language-grounding
- affordances
- planning
- robotics
---

## Summary

SayCan, presented at CoRL 2022, addresses the core limitation of using large language models for robot control: LLMs are powerful planners but lack grounding in the physical state of the robot's environment. A plan that is linguistically sensible may be physically impossible if the required object is occluded, out of reach, or if the robot has not yet navigated to the correct location. Ahn et al. resolve this by factoring the skill selection problem into a product of two scores: the language model's probability that the skill is the next appropriate step toward the goal, and a learned value function that estimates whether executing the skill is feasible given the current visual observation and robot state. Skills with high language plausibility but low physical feasibility are suppressed, while the system selects the skill that best combines both criteria. This product-of-experts formulation allows a frozen LLM to be grounded without any fine-tuning on robot data.

The skill library underlying SayCan consists of approximately 551 skills across 7 categories (pick-up, place, move to, open, close, pour, and put-in), each represented by a language description and a learned value function. The value functions are trained with offline RL on approximately 68,000 robot demonstrations using a sparse reward delivered at episode completion. The robot platform is a Boston Dynamics Spot equipped with an arm, operating in a real office kitchen environment with 17 food and drink items. At inference time, the system generates candidate skill descriptions from the LLM and selects the highest-scoring feasible candidate, executing the selected skill with a learned low-level policy before re-querying the LLM.

On a suite of 101 real-robot long-horizon tasks requiring up to 11 sequential skill executions, SayCan achieves 74% task success with high-level planning success of 80%. Critically, the paper ablates the value function's contribution: the LLM-only baseline (selecting the most language-plausible skill without feasibility scoring) achieves only 29% task success, demonstrating that affordance scoring is not a minor correction but fundamentally necessary for reliable execution. The paper also studies how SayCan handles task failures by re-querying the LLM given the updated state, showing graceful recovery from skill-level mistakes that a fixed plan would propagate catastrophically.

## Why It Matters

SayCan is the foundational paper for the language-planner plus learned-affordance architecture that became one of the two dominant paradigms for language-directed robot control (the other being end-to-end VLAs). Its elegant factored scoring formulation made it possible to deploy unmodified large language models—including GPT-3 at its full 175B scale—for robot planning without any robotics-specific fine-tuning, demonstrating the practical value of keeping the LLM frozen and adaptable to new LLM generations without retraining the robot-specific components.

The paper also crystallized a set of architectural trade-offs that subsequent work has tried to resolve. The two-module design introduces an interface that can fail: the LLM must generate candidate skill descriptions in a format that exactly matches the learned value function's representation, which requires careful prompt engineering and breaks down when the LLM proposes skills outside the predefined library. End-to-end VLAs like RT-2 implicitly address this by learning the entire planning-to-action chain jointly, at the cost of requiring much larger robot datasets and losing the ability to swap in a better LLM without full retraining. The ongoing debate between these two paradigms—modular LLM plus affordance versus end-to-end VLA—remains one of the central architectural questions in robot learning, and SayCan remains the canonical reference for the modular approach.

| | |
|---|---|
| **Authors** | Ahn et al. |
| **Year** | 2022 |
| **Venue** | arXiv / CoRL 2022 |
| **Field** | Robotics |
| **Subfield** | Robot Foundation Models Vla |
| **Tasks** | language-grounding, affordances, planning, language-conditioned-control |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2204.01691.pdf){: .btn .btn--primary .btn--large}
