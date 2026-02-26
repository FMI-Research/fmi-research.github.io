---
permalink: /papers/
title: "All Papers"
excerpt: "Browse all curated papers organized by field and subfield."
author_profile: false
---

A structured index of all papers in the FMI-Research library. Each title links to a dedicated abstract page with full metadata, extended summary, significance analysis, and PDF access.

**{{ site.papers | size }} papers** across 4 areas and 8 subfields. Sorted by date (newest first) within each subfield.

---

## AGI & Large Language Models {#agi}

### LLM Foundations & Scaling

{% assign papers = site.papers | where: "subfield", "llm-foundations-scaling" | sort: "date" | reverse %}
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

### Alignment, Safety & Evaluation

{% assign papers = site.papers | where: "subfield", "alignment-safety-evaluation" | sort: "date" | reverse %}
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

### Agentic LLMs

{% assign papers = site.papers | where: "subfield", "agentic-llms" | sort: "date" | reverse %}
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

## Computer Vision {#computer-vision}

### Open-World Perception

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

### Generative Vision

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

## Robotics {#robotics}

### Manipulation & Imitation Learning

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

### Foundation Models & Vision-Language-Action

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

## Embodied AI {#embodied-ai}

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

*PDFs are provided where legally permitted (open access or author-deposited preprints). Abstract pages for restricted papers link to the official publisher or arXiv source.*

---

## Autonomous Driving {#autonomous-driving}

### End-to-End Autonomous Driving

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

### LLM & VLA for Autonomous Driving

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

### World Models for Autonomous Driving

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
