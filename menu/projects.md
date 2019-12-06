---
layout: page
title: Projects
---

A list of computer science related projects that I have done in the recent years.

<ul class="projects">
  {% for proj in site.data.projects %}

    <li itemscope>
      <a href="{{ proj.url }}" class="project-title">{{ proj.title }}</a>
      <p class="project-date">
      <span>{{ proj.date-start | date: "%b %Y" }} - {{ proj.date-end | date: "%b %Y" }} | <a href="{{ proj.url }}"><i class="fa fa-link" aria-hidden="true"></i></a> |<a href="{{ proj.source }}"><i class="fa fa-github" aria-hidden="true"></i></a>
      </span>
      </p>
      <p class="project-description">{{ proj.description }}</p>
    </li>

  {% endfor %}
</ul>

