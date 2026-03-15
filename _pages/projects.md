---
layout: default
title: Work
permalink: /projects/
---

<div class="projects-header fade-in">
  <h1>Work</h1>
  <p class="projects-subtitle">Selected projects spanning embedded systems, aerodynamics, robotics, and fabrication.</p>
</div>

<div class="project-gallery">
  {% for project in site.projects reversed %}
    {% unless project.hidden %}
    <a href="{{ project.url | relative_url }}" class="gallery-card fade-in">
      {% if project.image %}
      <img src="{{ project.image | relative_url }}" alt="{{ project.title }}" class="gallery-card-image" />
      {% endif %}
      <div class="gallery-card-body">
        <div class="gallery-card-title">{{ project.title }}</div>
        {% if project.description %}
        <div class="gallery-card-desc">{{ project.description }}</div>
        {% endif %}
        {% if project.technologies %}
        <div class="gallery-card-tags">
          {% for tech in project.technologies %}
          <span class="card-tag">{{ tech }}</span>
          {% endfor %}
        </div>
        {% endif %}
      </div>
    </a>
    {% endunless %}
  {% endfor %}
</div>
