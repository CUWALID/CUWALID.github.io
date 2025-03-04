---
title: "CUWALID Team"
layout: single
permalink: /team/
author_profile: true
---

## Meet the Team

Welcome to the CUWALID team page! Below, you'll find the amazing people behind the project.

<link rel="stylesheet" href="/assets/css/team.css">

<div class="team-container">
  
{% for member in site.data.team %}
<div class="team-member">
  <img src="{{ member.image }}" alt="{{ member.name }}" class="team-photo">
  <h3>{{ member.name }}</h3>
  <p>{{ member.role }}</p>
  <p>{{ member.description }}</p>
</div>
{% endfor %}

</div>

---


