---
title: 'Mobile ALOHA: Learning Bimanual Mobile Manipulation with Low-Cost Whole-Body
  Teleoperation'
collection: papers
permalink: /papers/robotics/mobile_aloha_learning_bimanual_mobile_manipulation_with_low-cost_whole-body_teleoperation/
date: '2024-01-04'
year: 2024
field: robotics
subfield: manipulation-imitation-learning
tasks:
- mobile-manipulation
- whole-body-control
- imitation-learning
tier: 2
artifact_type: paper
venue: arXiv 2024
authors:
- Zipeng Fu
- Tony Z. Zhao
- Chelsea Finn
authors_short: Fu et al.
paperurl: /files/papers/mobile_aloha_learning_bimanual_mobile_manipulation_with_low-cost_whole-body_teleoperation.pdf
doi: 10.48550/arXiv.2401.02117
license: unspecified
summary: Mobile ALOHA mounts the ALOHA bimanual arm system on an AgileX Tracer mobile
  base and develops a whole-body teleoperation interface (joystick base control +
  puppet-arm bimanual control simultaneously), then shows that co-training the ACT
  policy on ~825 existing static ALOHA demonstrations alongside ~50 mobile task demonstrations
  per task improves mobile success rates by ~90% over training on mobile data alone
  — demonstrating cross-platform skill transfer without any architectural changes.
why_important: Demonstrated publicly that a ~$32K robot could perform complex household
  tasks (cooking shrimp, loading a dishwasher) via imitation learning, and its co-training
  finding directly motivated large-scale cross-platform data aggregation strategies
  in RT-X and Open X-Embodiment; deployment brittleness (sensitive to object placement
  and environment setup) and degrading co-training benefit for structurally dissimilar
  tasks drove follow-on work on foundation policies (π0, RoboVLMs) that pursue generalization
  through large-scale pretraining rather than targeted data mixing.
tags:
- mobile-manipulation
- whole-body
- aloha
- imitation-learning
- household-robots
---

## Summary

Mobile ALOHA extends the static ALOHA bimanual arm platform with an AgileX Tracer differential-drive mobile base, creating a whole-body manipulation system with 16 degrees of freedom: 6 DoF per arm, mobile base planar velocities, and a torso height adjustment. The teleoperation interface is correspondingly extended: the operator controls both puppet arms via the standard ALOHA kinesthetic interface while simultaneously driving the mobile base via a joystick, enabling coordinated whole-body demonstrations where arm and base motion are recorded together in a single synchronized trajectory. The hardware additions are cost-constrained — the full mobile platform costs approximately $32K, compared to $25K for the static ALOHA — and all components are off-the-shelf. Four cameras (two wrist-mounted, one head-mounted, one wide-angle base camera) provide the observation inputs to the policy, which is an ACT Transformer identical in architecture to the original static ALOHA policy.

The paper's central experimental contribution is the *co-training* protocol and its quantitative impact. Training the mobile manipulation policy exclusively on mobile task demonstrations (~50 per task) achieves modest success on household tasks (cooking shrimp: ~45%, loading dishwasher: ~37%). Co-training the same policy jointly on these mobile demonstrations plus the existing large static ALOHA dataset (~825 demonstrations across 5 tasks) raises mobile task success by approximately 90% relative — cooking shrimp to ~85%, dishwasher loading to ~71%. A carefully controlled "arm-only co-training" baseline — mobile data plus static data but with base action dimensions masked to zero — shows smaller gains, confirming that the benefit requires jointly modeling base and arm motions together rather than treating them as independent.

The co-training protocol is the key methodological insight. The authors' hypothesis is that static ALOHA demonstrations, while lacking base motion, provide rich supervision on fine-grained arm manipulation skills — precise grasping, object reorientation, bimanual coordination — that are equally necessary in mobile tasks. The mobile demonstrations then teach the policy how to coordinate base positioning with arm state, a skill that static data cannot provide. Because the ACT architecture processes all observation modalities and action dimensions jointly, the static and mobile data naturally complement each other within a single policy without requiring separate modules or domain adaptation. The paper also ablates co-training dataset ratio, finding that roughly 1:10 (mobile:static) is near-optimal.

## Why It Matters

Mobile ALOHA demonstrated, with striking and publicly available demo footage, that a commodity robot can perform complex multi-step household tasks — including cooking a three-course meal and loading a commercial dishwasher — through imitation learning alone. The viral reach of these demonstrations made Mobile ALOHA one of the most-watched robotics research releases of 2024 and drew widespread attention to the practical potential of low-cost imitation learning systems. Technically, the co-training finding was highly influential: it directly motivated large-scale cross-platform data aggregation strategies in RT-X and Open X-Embodiment, which aggregate hundreds of datasets from different robot platforms under the hypothesis that shared manipulation primitives transfer across embodiments. The result supported a broader and actively debated conjecture — that data from morphologically different platforms can mutually benefit learning — by providing a concrete, carefully controlled experimental validation.

The main deployment limitation is brittleness: the demonstrated tasks require careful environmental setup (precise object placement, specific lighting, unobstructed base paths), and generalization to novel kitchens or unstructured environments is not reported. The ~90% relative improvement from co-training diminishes for tasks that require mobile-specific coordination patterns not well-approximated by any static analogue — pure navigation-to-grasp sequences, for instance, benefit less than tasks dominated by bimanual arm manipulation after positioning. These limitations, combined with the still-significant data collection burden (~50 demos per task), motivated the subsequent wave of foundation policy approaches (π0, RoboVLMs, OpenVLA) that seek broad generalization through large-scale pretraining rather than task-specific data collection and targeted co-training recipes.

| | |
|---|---|
| **Authors** | Fu et al. |
| **Year** | 2024 |
| **Venue** | arXiv 2024 |
| **Field** | Robotics |
| **Subfield** | Manipulation Imitation Learning |
| **Tasks** | mobile-manipulation, whole-body-control, imitation-learning |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](/files/papers/mobile_aloha_learning_bimanual_mobile_manipulation_with_low-cost_whole-body_teleoperation.pdf){: .btn .btn--primary .btn--large}
