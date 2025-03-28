---
permalink: /about/
layout: splash
title: "About"
---

### CUWALID Modeling System  
This is a website surrounding all components of the CUWALID Climate and Water forecasting system, including information about the models, tutorials and details relating to the WujihaCast Telegram app.

### Down2Earth project  
[DOWN2EARTH](https://down2earthproject.org/) assembles a multidisciplinary project team, composed of experts and specialists in social science, rural development, media communication, climate science, meteorology, environment, hydrology, policy analysis, GIS, remote sensing, computer science, decision-support, modelling, and dryland processes. Below is a description of our project organization and a list of consortium institutions.

## Partners

Our project is supported by a range of institutions and organizations.  

<link rel="stylesheet" href="/assets/css/about.css">

<div class="partners-container">
  {% for partner in site.data.partners %}
  <div class="partner">
    <a href="{{ partner.url }}" target="_blank">
      <img src="{{ partner.image }}" alt="{{ partner.name }}" class="partner-logo">
    </a>
    <p style="font-size: 12px; font-weight: normal;">{{ partner.name }}</p>
  </div>
  {% endfor %}
</div>

---

## **Funding and Support**  

The CUWALID system and its research have been **supported by multiple organizations** and funding bodies.  

<div class="funders-container">
{% for funder in site.data.funders %}
  <a href="{{ funder.website }}" target="_blank">
    <img src="{{ funder.image }}" alt="{{ funder.name }}" class="funder-logo">
  </a>
{% endfor %}
</div>

### **Acknowledgments**  
- **E. Andrés Quichimbo** received financial support from Cardiff University through a Vice Chancellor’s Scholarship, Cardiff-UKRI-EPSRC.  
- **Mark O. Cuthbert** acknowledges funding for an Independent Research Fellowship from the UK Natural Environment Research Council (**NE/P017819/1**).  
- **Michael Bliss Singer** has been supported by the U.S. National Science Foundation (**BCS-1660490 and EAR-1700517**) and the U.S. Department of Defense (**RC18-1006**).  
- **The team** has been supported by the Global Challenges Research Fund (**GCRF**), The Royal Society (**DRIER, CHL\R1\180485**), and the European Union's Horizon 2020 programme (**DOWN2EARTH, grant no. 869550**).  
