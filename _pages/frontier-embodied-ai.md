---
permalink: /frontier/embodied-ai/
title: "Embodied AI"
excerpt: "Frontier research in embodied AI: agents that perceive, reason, and act in physical or simulated environments."
author_profile: false
---

[← Frontier Overview](/frontier/)

Embodied AI bridges perception, language, and physical action. It is the convergence point of robotics, computer vision, and language models — where agents must not only understand the world but act within it, typically in 3D environments that demand spatial reasoning and temporal planning.

---

## Embodied Agents, World Models & Data

{% assign papers = site.papers | where: "field", "embodied-ai" | sort: "date" | reverse %}
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

## Cross-Listed: VLA & Embodied Robot Learning

The following papers are filed under [Robotics → Foundation Models & VLA](/frontier/robotics/) but are directly relevant to Embodied AI:

{% assign papers = site.papers | where: "subfield", "foundation-models-vla" | sort: "date" | reverse %}
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
