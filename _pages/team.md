---
title: "CUWALID Team"
layout: splash
permalink: /team/
---

## Meet the Team

Welcome to the CUWALID team page! Below, you'll find the amazing people behind the CUWALID model and Down2Earth project.

<link rel="stylesheet" href="/assets/css/team.css">

<div class="team-container">
  {% for member in site.data.team %}
  <div class="team-member">
    <img src="{{ member.image }}" alt="{{ member.name }}" class="team-photo">
    <h3>{{ member.name }}</h3>
    <p>{{ member.role }}</p>
    <p>{{ member.description }}</p>
    <div class="member-links">
        {% if member.orcid and member.orcid != "" %}
            <a href="{{ member.orcid }}" target="_blank" class="btn btn--primary">
                <img src="/assets/images/icons/ORCID_iD.svg" alt="ORCID" class="icon"> ORCID
            </a>
        {% endif %}

        {% if member.github and member.github != "" %}
            <a href="{{ member.github }}" target="_blank" class="btn btn--primary">
                <img src="/assets/images/icons/github-mark.svg" alt="GitHub" class="icon"> GitHub
            </a>
        {% endif %}

        {% if member.scholar and member.scholar != "" %}
            <a href="{{ member.scholar }}" target="_blank" class="btn btn--primary">
                <img src="/assets/images/icons/Google_Scholar_logo.png" alt="Google Scholar" class="icon"> Scholar
            </a>
        {% endif %}

        {% if member.website and member.website != "" %}
            <a href="{{ member.website }}" target="_blank" class="btn btn--primary">
                <img src="/assets/images/icons/internet-svgrepo-com.svg" alt="Website" class="icon"> Website
            </a>
        {% endif %}
    </div>


  </div>
  {% endfor %}
</div>



