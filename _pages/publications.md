---
title: "Publications"
layout: splash
permalink: /publications/
---

## Research Publications

Welcome to the CUWALID publications page! Below, you'll find a list of research papers and articles associated with the project.

<link rel="stylesheet" href="/assets/css/publications.css">

<div class="publications-list">
  <ul>
    {% for paper in site.data.publications %}
      <li>
        {{ paper.author }} ({{ paper.year }}). 
        <em>{{ paper.title }}</em>{% if paper.journal %}. <i>{{ paper.journal }}</i>{% endif %} 
        {% if paper.volume %} <strong>{{ paper.volume }}</strong>{% endif %}
        {% if paper.number %}({{ paper.number }}){% endif %}
        {% if paper.pages %}, pp. {{ paper.pages }}{% endif %}.
        {% if paper.doi %} doi: <a href="https://doi.org/{{ paper.doi }}" target="_blank">{{ paper.doi }}</a>.{% endif %}
      </li>
    {% endfor %}
  </ul>
</div>
