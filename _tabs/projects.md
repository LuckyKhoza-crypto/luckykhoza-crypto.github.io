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
  document.addEventListener("DOMContentLoaded", function () {
    const modeToggle = document.querySelector(".sidebar-bottom #mode-toggle");

    function applyTheme() {
      if (document.body.getAttribute("theme_mode") === "dark") {
        document.body.setAttribute("theme_mode", "light");
      } else {
        document.body.setAttribute("theme_mode", "dark");
      }
    }

    // Set default theme to dark if not already set
    if (!document.body.getAttribute("theme_mode")) {
      document.body.setAttribute("theme_mode", "dark");
    }

    modeToggle.addEventListener("click", applyTheme);
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

  /* Dark Mode Styles (default theme) */
  [theme_mode="dark"] .custom-card {
    background-color: #333 !important;
    color: #ddd !important;
  }

  [theme_mode="dark"] .custom-card .card-title,
  [theme_mode="dark"] .custom-card .card-text,
  [theme_mode="dark"] .custom-card a {
    color: #fff !important;
  }

  [theme_mode="dark"] .custom-card .badge {
    background-color: #555 !important;
    color: #fff !important;
  }

  [theme_mode="dark"] .btn-secondary {
    background-color: #666 !important;
    border-color: #888 !important;
  }

  [theme_mode="dark"] .btn-secondary:hover {
    background-color: #777 !important;
  }

  /* Light Mode Styles */
  [theme_mode="light"] .custom-card {
    background-color: #fff !important;
    color: #000 !important;
  }

  [theme_mode="light"] .custom-card .card-title,
  [theme_mode="light"] .custom-card .card-text,
  [theme_mode="light"] .custom-card a {
    color: #000 !important;
  }

  [theme_mode="light"] .custom-card .badge {
    background-color: #ddd !important;
    color: #000 !important;
  }

  [theme_mode="light"] .btn-secondary {
    background-color: #007bff !important;
    border-color: #0056b3 !important;
  }

  [theme_mode="light"] .btn-secondary:hover {
    background-color: #0056b3 !important;
  }
</style>
