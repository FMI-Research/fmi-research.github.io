---
permalink: /frontier/robotics/
title: "Robotics"
excerpt: "Frontier research in robot learning: imitation learning, manipulation, and vision-language-action models."
author_profile: false
---

[← Frontier Overview](/frontier/)

Robot learning has advanced from narrow task-specific policies to general-purpose foundation models that follow language instructions across diverse embodiments. This area tracks both the learning methods and the large-scale datasets enabling this progress.

---

## Subfield 1: Manipulation & Imitation Learning

*Data-driven methods for teaching robots to manipulate objects.*

**Key tasks:** Behavior cloning · Diffusion-based policies · Large-scale robot datasets · Benchmarks

{% assign papers = site.papers | where: "subfield", "manipulation-imitation-learning" | sort: "date" | reverse %}
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

## Subfield 2: Foundation Models & Vision-Language-Action

*Scaling robot policies with language and vision.*

**Key tasks:** VLA pretraining · Cross-embodiment generalization · Language-conditioned control · Grounded planning

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
