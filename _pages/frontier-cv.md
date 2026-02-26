---
permalink: /frontier/cv/
title: "Computer Vision"
excerpt: "Frontier research in computer vision: open-world perception and generative visual synthesis."
author_profile: false
---

[← Frontier Overview](/frontier/)

Computer vision has undergone two simultaneous transformations: the rise of open-world foundation models for perception, and the diffusion-based revolution in visual synthesis. This area covers both.

---

## Subfield 1: Open-World Perception

*Foundation models for open-vocabulary detection, segmentation, and visual representation.*

**Key tasks:** Promptable segmentation · Grounded detection · Visual pretraining · Vision-language alignment

{% assign papers = site.papers | where: "subfield", "open-world-perception" | sort: "date" | reverse %}
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

## Subfield 2: Generative Vision

*Diffusion models for image, 3D, and video synthesis.*

**Key tasks:** Text-to-image · Text-to-3D · Text-to-video · Controllable generation · Novel view synthesis

{% assign papers = site.papers | where: "subfield", "generative-vision" | sort: "date" | reverse %}
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
