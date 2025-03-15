---
title: "Publications"
layout: splash
permalink: /publications/
---

## Research Publications

Welcome to the CUWALID publications page! Below, you'll find a list of research papers and articles associated with the project.

<link rel="stylesheet" href="/assets/css/publications.css">

<div class="publications-container">
  {% for paper in site.data.publications %}
  <div class="publication-card">
    <h3 class="publication-title">{{ paper.title }}</h3>
    <p class="publication-authors"><strong>Authors:</strong> {{ paper.authors }}</p>
    <p class="publication-year"><strong>Year:</strong> {{ paper.year }}</p>
    <p class="publication-abstract">{{ paper.abstract }}</p>
    
    <div class="publication-links">
      {% if paper.doi and paper.doi != "" %}
        <a href="https://doi.org/{{ paper.doi }}" target="_blank" class="btn btn--primary">DOI</a>
      {% endif %}
      
      {% if paper.arxiv and paper.arxiv != "" %}
        <a href="https://arxiv.org/abs/{{ paper.arxiv }}" target="_blank" class="btn btn--primary">arXiv</a>
      {% endif %}
      
      {% if paper.scholar and paper.scholar != "" %}
        <a href="{{ paper.scholar }}" target="_blank" class="btn btn--primary">Google Scholar</a>
      {% endif %}
      
      {% if paper.pdf and paper.pdf != "" %}
        <a href="{{ paper.pdf }}" target="_blank" class="btn btn--primary">PDF</a>
      {% endif %}
    </div>
  </div>
  {% endfor %}
</div>
