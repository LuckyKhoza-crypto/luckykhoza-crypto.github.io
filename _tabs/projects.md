---
title: Projects
layout: page
permalink: /projects/
icon: fa-solid fa-diagram-project
order: 1
---

## Below are the projects I've worked on before.

<div class="container mt-3">
  <div class="row">
    {% for project in site.projects %}
      <div class="col-md-4 mb-4">
        <div class="custom-card">
          <div class="custom-card-body">
            <h3 class="card-title">{{ project.title }}</h3>
            <p class="card-text">Published: {{ project.date | date: "%B %d, %Y" }}</p>
            
            {% if project.tags %}
              <p><strong>Tags:</strong></p>
              <ul class="custom-tags">
                {% for tag in project.tags %}
                  <li class="mt-2">{{ tag }}</li>
                {% endfor %}
              </ul>


            {% endif %}
            
            <a href="{{ project.url }}" class="btn btn-secondary mt-2">View Project</a>
          </div>
        </div>
      </div>
    {% endfor %}
  </div>
</div>

<style>
  body {
    background-color: #121212;
    color: #ddd;
  }

  .custom-card {
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out;
    padding: 15px;
    background-color: #333;
    color: #ddd;
  }

  .custom-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
  }

  .custom-card-body {
    padding: 20px;
  }

  .custom-card .card-title,
  .custom-card .card-text,
  .custom-card a {
    color: #fff;
  }

  .custom-card .badge {
    background-color: #555;
    color: #fff;
  }

  .btn-secondary {
    background-color: #666;
    border-color: #888;
    color: #fff;
  }

  .btn-secondary:hover {
    background-color: #777;
  }

  .custom-tags {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
  padding: 0;
}

.custom-tags li {
  background-color: #444;
  color: white;
  padding: 5px 10px;
  border-radius: 15px;
  margin-right: 8px;
  font-size: 14px;
}

</style>
