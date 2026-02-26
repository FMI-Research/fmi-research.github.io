---
title: A Survey on Imitation Learning for Contact-Rich Tasks in Robotics
collection: papers
permalink: /papers/robotics/a_survey_on_imitation_learning_for_contact-rich_tasks_in_robotics/
date: '2025-06-01'
year: 2025
field: robotics
subfield: robot-learning-manipulation
tasks:
- contact-rich
- manipulation
- imitation-learning
- force-sensing
tier: 1
artifact_type: paper
venue: arXiv 2025
authors:
- Tsuji et al.
authors_short: Tsuji et al.
paperurl: https://arxiv.org/pdf/2506.13498.pdf
doi: 10.48550/arXiv.2506.13498
license: unspecified
summary: A focused 2025 survey on imitation learning for contact-rich robotic manipulation,
  systematically reviewing force and tactile sensing modalities, teleoperation interfaces
  for conveying force profiles, and policy learning strategies tailored to tasks where
  contact dynamics are first-class concerns rather than disturbances.
why_important: Fills a critical gap left by general IL surveys by addressing the sensing,
  control, and data collection challenges unique to contact-rich manipulation, positioning
  the field to advance beyond free-space pick-and-place as tactile sensing matures
  and dexterous hardware becomes more accessible.
tags:
- survey
- contact-rich
- manipulation
- imitation-learning
- tactile
---

## Summary

Contact-rich manipulation tasks—peg insertion, gear assembly, cloth folding, door opening—impose demands that are qualitatively different from pick-and-place: the policy must reason about interaction forces, maintain stable grasps under load, and recover from contact failures. Tsuji et al. survey how imitation learning has been adapted to meet these demands, organizing the literature along three axes: sensing modalities, demonstration collection infrastructure, and policy learning algorithms. On the sensing side, the survey contrasts vision-only pipelines with approaches that incorporate force-torque (F/T) sensors at the wrist, tactile skins on the fingertips, and joint torque feedback from the robot's own actuators. It analyzes the trade-off between sensing richness and deployment practicality, noting that many tactile sensors remain lab prototypes with poor durability, calibration stability, or commercial availability.

Data collection for contact-rich tasks is substantially more demanding than for free-space manipulation because teleoperators must convey not only spatial trajectories but also the subtle force profiles that characterize skilled human manipulation. The survey reviews teleoperation interfaces ranging from bilateral force-feedback devices and motion capture gloves to kinesthetic teaching and learning from video observation. A recurring conclusion is that the quality and expressiveness of the demonstration interface strongly governs downstream policy performance, independent of the algorithm chosen. The authors also examine autonomous data collection via exploration and self-supervised contact labeling, evaluating the trade-offs between human teleoperation quality and the scalability of autonomous collection methods.

On the policy learning side, the survey covers BC variants, DMP-based approaches, energy-based models, and diffusion policies, evaluating each paradigm's capacity to represent the multimodal force profiles that arise during contact-rich manipulation. It discusses hybrid position-force control architectures that separate Cartesian motion control from contact force regulation, enabling policies parameterized in a lower-dimensional space where imitation is more tractable. Benchmarks for contact-rich tasks—including NIST Assembly Task Board, IkeaAssembly, and physical insertion benchmarks—are reviewed, with the survey noting a fragmented evaluation landscape that hinders reproducible comparison across research groups.

## Why It Matters

Contact-rich manipulation represents one of the hardest unsolved problems in robotics, yet most large-scale imitation learning datasets and foundation model evaluations focus on free-space pick-and-place tasks where vision-only control is sufficient. This survey directly addresses that blind spot, cataloging the sensing, teleoperation, and policy learning infrastructure needed to advance the contact-rich frontier. As tactile sensor technology matures and dexterous hardware becomes more accessible, the frameworks reviewed here are positioned to become central to the next generation of manipulation research and to define what new datasets and benchmarks need to be developed.

The survey also highlights important open questions at the intersection of contact-rich manipulation and foundation model robotics: How can contact information be integrated into large vision-language-action models that currently lack proprioceptive or tactile inputs? Can self-supervised methods learn to predict contact events from vision alone? And what benchmarks would enable standardized comparison of contact-rich policies across labs? These questions connect the contact-rich IL literature to ongoing debates in foundation model robotics—whether to add sensory modalities or to extract contact information from vision—making this survey a valuable bridge between specialized manipulation and general robot learning communities.

| | |
|---|---|
| **Authors** | Tsuji et al. |
| **Year** | 2025 |
| **Venue** | arXiv 2025 |
| **Field** | Robotics |
| **Subfield** | Robot Learning Manipulation |
| **Tasks** | contact-rich, manipulation, imitation-learning, force-sensing |
| **Tier** | 1 — Survey / Landmark |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2506.13498.pdf){: .btn .btn--primary .btn--large}
