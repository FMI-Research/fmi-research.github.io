---
permalink: /frontier/autonomous-driving/
title: "Autonomous Driving"
excerpt: "Frontier research in autonomous driving: end-to-end systems, LLM/VLA integration, and world models."
author_profile: false
---

[← Frontier Overview](/frontier/)

Autonomous driving has undergone a paradigm shift from modular, hand-engineered pipelines toward end-to-end learned systems and, more recently, toward LLM/VLA-augmented architectures that bring commonsense reasoning and natural language interfaces to driving. This area tracks the papers defining these transitions.

---

## Subfield 1: End-to-End Autonomous Driving

*Unified architectures that learn perception, prediction, and planning jointly from data.*

**Key tasks:** Unified E2E architecture · Vectorized/sparse scene representation · Planning-oriented training · Simulation & benchmarking

{% assign papers = site.papers | where: "subfield", "end-to-end-autonomous-driving" | sort: "date" | reverse %}
<table class="paper-table">
<thead><tr><th>Paper</th><th>Authors</th><th>Year</th><th>Venue</th></tr></thead>
<tbody>
{% for paper in papers %}
<tr>
  <td><a href="{{ paper.url }}">{{ paper.title }}</a></td>
  <td>{{ paper.authors_short }}</td>
  <td>{{ paper.year }}</td>
  <td>{{ paper.venue }}</td>
</tr>
{% endfor %}
</tbody>
</table>

---

## Subfield 2: LLM & VLA for Autonomous Driving

*Language models and vision-language-action models applied to driving reasoning and planning.*

**Key tasks:** Language-grounded driving · Chain-of-thought planning · VQA for driving · VLM-E2E integration

{% assign papers = site.papers | where: "subfield", "llm-vla-autonomous-driving" | sort: "date" | reverse %}
<table class="paper-table">
<thead><tr><th>Paper</th><th>Authors</th><th>Year</th><th>Venue</th></tr></thead>
<tbody>
{% for paper in papers %}
<tr>
  <td><a href="{{ paper.url }}">{{ paper.title }}</a></td>
  <td>{{ paper.authors_short }}</td>
  <td>{{ paper.year }}</td>
  <td>{{ paper.venue }}</td>
</tr>
{% endfor %}
</tbody>
</table>

---

## Subfield 3: World Models for Autonomous Driving

*Generative models that simulate driving environments for data augmentation, policy evaluation, and planning.*

**Key tasks:** Driving video generation · Controllable simulation · World model pre-training

{% assign papers = site.papers | where: "subfield", "world-models-autonomous-driving" | sort: "date" | reverse %}
<table class="paper-table">
<thead><tr><th>Paper</th><th>Authors</th><th>Year</th><th>Venue</th></tr></thead>
<tbody>
{% for paper in papers %}
<tr>
  <td><a href="{{ paper.url }}">{{ paper.title }}</a></td>
  <td>{{ paper.authors_short }}</td>
  <td>{{ paper.year }}</td>
  <td>{{ paper.venue }}</td>
</tr>
{% endfor %}
</tbody>
</table>

---

[← All Papers](/papers/) · [Frontier Overview →](/frontier/)
