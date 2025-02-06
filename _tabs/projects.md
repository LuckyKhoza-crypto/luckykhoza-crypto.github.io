---
title: Projects
layout: page
permalink: /projects/
icon: fa-solid fa-diagram-project
order: 1
---
## Below are the projects I've worked on before.

<div class="container mt-5">
  <div class="row">
    {% for project in site.projects %}
      <div class="col-md-4 mb-4">
        <div class="custom-card">
          <div class="custom-card-body">
            <h2 class="card-title">{{ project.title }}</h2>
            <p class="card-text">Published on: {{ project.date | date: "%B %d, %Y" }}</p>
            
            {% if project.tags %}
              <p><strong>Tags:</strong></p>
              <ul class="list-unstyled categories">
                {% for tag in project.tags %}
                  <li class="badge bg-secondary me-1">{{ tag }}</li>
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

<script>
  document.addEventListener("DOMContentLoaded", () => {
    const modeToggle = document.querySelector(".sidebar-bottom #mode-toggle");

    function toggleTheme() {
      const currentTheme = document.body.getAttribute("data-bs-theme");
      document.body.setAttribute("data-bs-theme", currentTheme === "dark" ? "light" : "dark");
    }

    modeToggle.addEventListener("click", toggleTheme);
  });
</script>

<style>
  .custom-card {
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out;
    padding: 15px;
    background-color: var(--bs-card-bg, #fff);
    color: #000;
  }

  .custom-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
  }

  .custom-card-body {
    padding: 20px;
  }

  /* Dark Mode Styles */
  [data-bs-theme="dark"] .custom-card {
    background-color: #333 !important;
    color: #ddd !important;
  }

  [data-bs-theme="dark"] .custom-card .card-title,
  [data-bs-theme="dark"] .custom-card .card-text,
  [data-bs-theme="dark"] .custom-card a {
    color: #fff !important;
  }

  [data-bs-theme="dark"] .custom-card .badge {
    background-color: #555 !important;
    color: #fff !important;
  }

  [data-bs-theme="dark"] .btn-secondary {
    background-color: #666 !important;
    border-color: #888 !important;
  }

  [data-bs-theme="dark"] .btn-secondary:hover {
    background-color: #777 !important;
  }
</style>
