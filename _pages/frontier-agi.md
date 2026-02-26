---
permalink: /frontier/agi/
title: "AGI & Large Language Models"
excerpt: "Frontier research in large language models: scaling, alignment, evaluation, and agentic reasoning."
author_profile: false
---

[← Frontier Overview](/frontier/)

Large Language Models have become the backbone of modern AI — from trillion-parameter pretraining runs to instruction-following, tool use, and complex reasoning. This area covers the papers that defined and continue to push the frontier.

---

## Subfield 1: LLM Foundations & Scaling

*Core architectures, training recipes, and the scaling laws that govern them.*

**Key tasks:** Pretraining · Scaling · Architecture design · Model families

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

---

## Subfield 2: Alignment, Safety & Evaluation

*Making LLMs helpful, harmless, and honestly evaluated.*

**Key tasks:** RLHF · Instruction tuning · Hallucination reduction · Benchmarking

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

---

## Subfield 3: Agentic LLMs

*LLMs that reason, plan, use tools, and act in the world.*

**Key tasks:** Tool use · Planning · Multi-agent systems · Memory · Retrieval-augmented generation

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

[← All Papers](/papers/) · [Frontier Overview →](/frontier/)
