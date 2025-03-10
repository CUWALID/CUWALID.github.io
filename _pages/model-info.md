---
title: "Modelling System"
layout: single
permalink: /model-info/

sidebar:
  nav: "model-info"

---
<link rel="stylesheet" href="{{ '/assets/css/model-card.css' | relative_url }}">


{% include figure popup=true image_path="/assets/images/cuwalid_assets/CUWALID_Logo_LS_Full_Colour.png" alt="CUWALID Logo" %}


## Models

<div class="model-container">
  <div class="model-card">
    <h3>DRYP</h3>
    <p>Dryland water partitioning models.</p>
    <a href="/model-info/#dryp-model" class="btn btn--primary">More info</a>
  </div>
  <div class="model-card">
    <h3>stoPET</h3>
    <p>Stochastic potential evpotranspiration generator.</p>
    <a href="/model-info/#stopet-model" class="btn btn--primary">More info</a>
  </div>
  <div class="model-card">
    <h3>STORM</h3>
    <p>Stochastic Rainfall generator.</p>
    <a href="/model-info/#storm-model" class="btn btn--primary">More info</a>
  </div>
  <div class="model-card">
    <h3>HyCast</h3>
    <p>Probabilistic Hydrological forecast.</p>
    <a href="/model-info/#watercast-model" class="btn btn--primary">More info</a>
  </div>
  <div class="model-card">
    <h3>ImCast</h3>
    <p>Impact-based water forecast.</p>
    <a href="/model-info/#imcast-model" class="btn btn--primary">More info</a>
  </div>
</div>


---

{% include model_info/cuwalid-info.md %}

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

{% include input-helper-info.md %}
