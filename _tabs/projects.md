---
title: Projects
layout: page
permalink: /projects/
icon: fa-solid fa-diagram-project
order: 1
---

## Below are the projects I've worked on before.

#### You will find live demos, videos, or even GitHub code for some of them. All projects are open-source—if you need to use them, please reach out.

<div class="container mt-5">
  <div class="row">
    {% for project in site.projects %}
      <div class="col-md-4 mb-4">
        <div class="card shadow-lg h-100 border border-warning rounded-3">
          <div class="card-body">
            <h5 class="card-title fw-bold">{{ project.title }}</h5>
            <p class="card-text">Published on: {{ project.date | date: "%B %d, %Y" }}</p>
            
            {% if project.tags %}
              <p><strong>Tags:</strong></p>
              <ul class="list-unstyled">
                {% for tag in project.tags %}
                  <li class="badge bg-secondary me-1">{{ tag }}</li>
                {% endfor %}
              </ul>
            {% endif %}
            
            <a href="{{ project.url }}" class="btn btn-primary mt-2">View Project</a>
          </div>
        </div>
      </div>
    {% endfor %}
  </div>
</div>
