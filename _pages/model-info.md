---
title: "Modelling Info"
layout: single
permalink: /model-info/

sidebar:
  nav: "model-info"
---

<link rel="stylesheet" href="{{ '/assets/css/model-card.css' | relative_url }}">

## Models

<div class="model-container">
  <div class="model-card">
    <h3>DRYP</h3>
    <p>A model for forecasting seasonal climate impacts.</p>
    <a href="/model-info/#dryp-model" class="btn btn--primary">More info</a>
  </div>
  <div class="model-card">
    <h3>StoPET</h3>
    <p>Seasonal and impact forecasting for water and vegetation.</p>
    <a href="/model-info/#stopet-model" class="btn btn--primary">More info</a>
  </div>
  <div class="model-card">
    <h3>Storm</h3>
    <p>Forecasts and weather patterns to support decision-making.</p>
    <a href="/model-info/#storm-model" class="btn btn--primary">More info</a>
  </div>
  <div class="model-card">
    <h3>WaterCast</h3>
    <p>Hydrological forecast for water availability.</p>
    <a href="/model-info/#watercast-model" class="btn btn--primary">More info</a>
  </div>
  <div class="model-card">
    <h3>ImCast</h3>
    <p>Impact-based forecast for agricultural planning.</p>
    <a href="/model-info/#imcast-model" class="btn btn--primary">More info</a>
  </div>
</div>


---

{% include model_info/dryp-info.md %}

---

{% include model_info/stopet-info.md %}

---

{% include model_info/storm-info.md %}

---

{% include model_info/watercast-info.md %}

---

{% include model_info/imcast-info.md %}

---

{% include input-helper.md %}
