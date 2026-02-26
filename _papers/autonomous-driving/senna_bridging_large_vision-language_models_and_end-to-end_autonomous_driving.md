---
title: 'Senna: Bridging Large Vision-Language Models and End-to-End Autonomous Driving'
collection: papers
permalink: /papers/autonomous-driving/senna_bridging_large_vision-language_models_and_end-to-end_autonomous_driving/
date: '2024-10-28'
year: 2024
field: autonomous-driving
subfield: llm-vla-autonomous-driving
tasks:
- vla-driving
- end-to-end-driving
- llm-planning
- intent-prediction
tier: 2
artifact_type: paper
venue: arXiv 2024
authors:
- Bo Jiang
- Shaoyu Chen
- Bencheng Liao
- Xingyu Zhang
- Wei Yin
- Qian Zhang
- Chang Huang
- Wenyu Liu
- Xinggang Wang
authors_short: Jiang et al.
paperurl: https://arxiv.org/pdf/2410.21013.pdf
doi: 10.48550/arXiv.2410.21013
license: unspecified
summary: Senna couples Qwen-VL as a high-level intent predictor with a VAD-based end-to-end
  trajectory planner as a low-level controller, communicating via discrete natural
  language driving intentions and meta-actions, and trains the joint system with both
  driving trajectory supervision and language prediction losses to substantially improve
  planning in complex scenarios such as unprotected turns and pedestrian interactions.
why_important: Senna demonstrated that natural language is an effective differentiable
  interface between VLM-based semantic reasoning and E2E trajectory planning, and
  its design — by the VAD team — represents the natural evolution of vectorized E2E
  driving toward language-grounded hierarchical control, influencing LMDrive and DiMA.
tags:
- vla
- autonomous-driving
- end-to-end
- vlm
- intent-prediction
---

## Summary

Senna addresses a central limitation of pure E2E driving models: their inability to engage in semantic scene reasoning for complex, long-tail scenarios such as unprotected turns, yielding to emergency vehicles, or navigating ambiguous pedestrian interactions. Rather than replacing the E2E planner with a VLM, Senna adopts a two-tier architecture in which a VLM (Qwen-VL) serves as a high-level *intent predictor* and a VAD-based E2E model serves as the low-level *trajectory planner*. The VLM receives multi-camera driving images and generates two types of language outputs: *driving intentions* (e.g., "turn left at the intersection ahead") and *meta-actions* (e.g., "yield to the pedestrian on the right"). These discrete language tokens are converted into learned conditioning embeddings and injected into the VAD trajectory decoder via cross-attention, providing semantic context that guides geometric trajectory planning without overriding the continuous E2E controller. This design avoids the latency problems of full VLM-based planning while preserving the VLM's commonsense reasoning capacity for high-level decision-making.

Senna is evaluated on the nuScenes open-loop planning benchmark and on curated complex scenario subsets. On standard nuScenes planning, Senna achieves 0.43 m L2 at 2 s and 0.04% collision rate — comparable to VAD and SparseDrive. The significant improvements appear in complex scenario subsets: on unprotected left turns, Senna reduces collision rate by 34% relative to the VAD baseline; on pedestrian interaction scenarios, it reduces collision rate by 28%. Ablation studies show that VLM-generated intentions and meta-actions contribute independently — removing intentions alone increases L2 by 0.08 m, while removing meta-actions increases collision rate by 0.02%. The joint training strategy (simultaneous optimization of VLM language prediction loss and E2E trajectory loss) proves critical: training the VLM in isolation before freezing it and training the E2E model degrades performance, confirming that the language-trajectory interface must be learned jointly rather than in isolation.

Senna's key innovation is its *language-as-interface* design: rather than using a VLM's output as a direct trajectory (which suffers from geometric imprecision) or as a soft cost function (which is opaque), it maps VLM outputs to a finite vocabulary of structured intentions and meta-actions and trains learned embeddings for each token, creating a differentiable, learnable bridge between language reasoning and geometric planning. The discrete intention vocabulary (∼10 intention categories, ∼20 meta-action categories) is comprehensive enough to cover urban driving scenarios while small enough to enable reliable VLM prediction. Joint training with a combined loss — VLM cross-entropy on language tokens + trajectory L1 loss + collision auxiliary loss — allows gradients from the trajectory planner to flow back through the intention embeddings, enabling the VLM to learn driving-specific language representations optimized for their effect on downstream trajectory quality rather than language generation quality alone.

## Why It Matters

Senna represents the natural next step from VAD's vectorized planning framework toward language-grounded hierarchical control, and its design from the VAD team carries the credibility of an architecture evolution rather than a disconnected proposal. The work validates a key hypothesis that had motivated DriveLM, DriveVLM, and Agent-Driver: that semantic reasoning (what the ego vehicle *should* do in human terms) can reliably improve geometric trajectory planning (where the ego vehicle actually goes). The discrete intention vocabulary approach proved influential — subsequent systems including LMDrive and DiMA adopted analogous discrete language token interfaces between slow semantic reasoners and fast reactive planners, establishing it as a design pattern for two-tier VLM+E2E systems. Senna also demonstrated that jointly training the VLM and the E2E model is necessary for effective performance, an insight that has practical implications for how VLM-guided AD systems are trained and fine-tuned in production.

Senna's evaluation is limited to the nuScenes open-loop benchmark, and the complex scenario improvements — while compelling — are measured on a curated subset rather than a standardized closed-loop evaluation, making it difficult to assess whether the improvements reflect genuine safety gains or dataset-specific optimization. The discrete intention vocabulary, while enabling clean language interfacing, imposes a fixed taxonomy that may not generalize to unusual situations outside the predefined categories — if the VLM encounters a scenario that does not map cleanly to a known intention (e.g., driving through a flooded road, avoiding debris fallen from a truck), the discrete interface provides no mechanism for communicating novel semantic context. The VLM component adds inference overhead that, while smaller than DriveVLM's full chain-of-thought pipeline, still extends per-frame latency beyond a pure E2E model such as VAD. Finally, the joint training strategy requires simultaneous access to paired trajectory and language supervision data, which limits applicability to datasets annotated with both driving labels and language descriptions — a curation bottleneck that restricts scalable self-supervised training from unlabeled driving video.

| | |
|---|---|
| **Authors** | Jiang et al. |
| **Year** | 2024 |
| **Venue** | arXiv 2024 |
| **Field** | Autonomous Driving |
| **Subfield** | Llm Vla Autonomous Driving |
| **Tasks** | vla-driving, end-to-end-driving, llm-planning, intent-prediction |
| **Tier** | 2 — Method / Baseline |
| **License** | unspecified |

[View / Download PDF](https://arxiv.org/pdf/2410.21013.pdf){: .btn .btn--primary .btn--large}
